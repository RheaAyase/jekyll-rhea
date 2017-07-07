---
layout: post
title:  "Migrating from unRAID to Fedora"
date:   2017-07-07 16:10:00
categories: [code]
comments: true
---
I spent the last few weeks slowly setting up a Fedora server with OpenShift on my old unRAID machine. It's an overclocked, watercooled i7 with 16GB memory, and a bunch of HDDs. One very old 500GB drive that is irrelevant to me right now, as it is too small. One 2TB and one 3TB, which is what I would like to migrate into this new Fedora server. It has one unRAID share on these two drives, using up just under 3TBs total, split evenly. I will need to think really hard about what of that data am I going to keep, there is some sentimental value to it... Oh and I used the formerly cache drive, 120GB SSD, as the system drive for the new setup. One simple 100g root partition and a bunch for swap space if I would happen to need it (currently disabled.)

#### The problem

How to move the data that I want to keep, from two drives, into one RAID1, where I will be formatting these drives and setting up that raid on top of them. I don't have a few TBs of a drive laying around!

<!--more-->

#### File Puzzle

So to begin with I managed to shrink my data down to some 1.5TB and move it into the 2TB sized drive. Then I also moved the contents of the 500GB drive there since there was enough space for it. I was left with less than 50GBs of free space.

#### The idea

I would like to have RAID1 between the 2TB and the 3TB drive, which will leave me with 1TB of free space on the bigger drive. I decided to use that 1TB leftover and the small 500GB drive in LVM, then to move all the data from the 2TB drive over there, and whatever won't fit into my desktop over network. This meant NFS or Samba...

#### Partitions

To begin with I used `parted` to create partitions on the 3TB drive - I had to figure out the right sector alignment numbers... Don't ask me how, but it worked and `parted align-check` is happy with it.

Then I did the same with the 500GB drive.

I did some LVM magic next:

`pvcreate /dev/sdc2 /dev/sdd1` - Initialize my two partitions of choice to be used as LVM physical volumes.
<br>`vgcreate unraid /dev/sdc2 /dev/sdd1` - Create a volume group with a name _"unraid"_ with these two volumes.
<br>`lvcreate -l 100%VG -n unraid unraid` - Create the logical volume using 100% of the above group size. _(I hope that having the same name won't break it haha)_
<br>`mkfs.ext4 -b 4096 /dev/unraid/unraid` - Filesystem. Going with ext4 because for some reason I don't have gfs2 mounting ability. I couldn't figure that one out :<
<br>`mount -t ext4 /dev/unraid/unraid /mnt/unraid` - Finally mount it... 

Time to copy the files over while I sleep!

##### The next morning...

_\*nyawn*_ good morning :D
<br />
It worked just fine and the two drives are full, but I still have 463GBs leftover. I'll need to transfer this over network to my desktop PC.

`dnf install -y samba` - I've set it up without any security, with just allowed hosts. I just need my local desktop to eat some files temporarily. I have different filesharing solution in mind for the final setup - keep reading to find out what ;)

All the files are in their temporary locations, I can now create my little raid. I decided for LVM because it's the same thing mdadm with a bit more stuff... So after re-doing the above pvcreate and vgcreate on the last drive, I went ahead and create my raid as follows:
<br>`lvcreate --type raid1 -l100%VG -n raid raid` - I totally used this type of stupid names :D
<br>...and here I created ext4 and mounted it to `/mnt/raid` the same way as the unraid drives.

Oh and... fstab of course.

#### Nextcloud

 &nbsp; And I did all this, in order to store my files on mirrored raid. Keep them a little safer. And to throw away dropbox/mega/googledrive/whatever... Our little cute cloud solution with 2TB space, isn't that cute?

 &nbsp; So, how did I set this up? I followed the documentation for some bits and pieces, I googled for the other stuff... I got so carried away that I totally forgot to keep writing it down what I'm doing though, so the below may or may not be accurate.

 &nbsp; `dnf install httpd mariadb-server php php-pecl-apcu nextcloud` - This is the core of it that we need on Fedora. There may have been some other bits and pieces that I may have forgotten tho, you will see if it doesn't work for you! :D _(Feel free to message me if you have questions!)_
<br> &nbsp; Then, I moved all the files for it to the raid storage. Those were in `/usr/share/nextcloud` and `/var/opt/nextcloud` iirc, I had to fix up nextcloud's configuration (the `config/config.php` file) and also the httpd configuration (nextcloud created `/etc/httpd/conf.d/nextcloud*` files. The main one contains some reference to those directories.) And while i was at it I also fixed up the httpd config file `nextcloud-auth-local.inc` to allow usage from my LAN network, not just localhost.

 &nbsp; I ran the mariadb secure install thing, and then I also moved the whole mariadb database over to the raid and created a new user and a database for nextcloud.
<br>`mysql -u root -p` -> `select @@datadir;` - Here is the default location, cause I can never remember where is what.
<br>`systemctl stop mariadb` - Need to stop it right?
<br>`sudo mv /var/lib/mysql /mnt/raid/mysql` - or something along those lines, anyway.
<br>`vim /etc/my.cnf` - changing two values here, the `datadir` and the `socket` to reflect the new location.
<br> &nbsp; Save and fire the thing back up again!

 &nbsp; Now I changed the `/etc/php.d/30-pdo_mysql.ini` to reflect the database changes plus whatever else did they mention in the nextcloud docs:

```
 1 ; Enable pdo_mysql extension module
 2 extension=pdo_mysql.so
 3
 4 [mysql]
 5 mysql.allow_local_infile=On
 6 mysql.allow_persistent=On
 7 mysql.cache_size=2000
 8 mysql.max_persistent=-1
 9 mysql.max_links=-1
10 mysql.default_port=
11 mysql.default_socket=/mnt/raid/mysql/mysql.sock
12 mysql.default_host=127.0.0.1
13 mysql.default_user=project
14 mysql.default_password=
15 mysql.connect_timeout=60
16 mysql.trace_mode=Off
```

 &nbsp; Next, ports and firewall stuffs... I am not running it on default http and https so I had to open that up, plus set it up in my router and the usual network nonsense.

 &nbsp; Finally, a bit of actual nextcloud configuration, right? I used the web-config - i've simply hit the thing in my browser, and entered my desired admin username, password, and configuration for my database - I assume that you either know how did I create that and the dbuser (or you can use google.)
<br> &nbsp; Cool, that totally did **not** work right! :D
<br> &nbsp; So I had to go to the `config/config.php` file and fix the database user and password in it, because it saved it all wrong. And I had to rewrite everything referencing `localhost` to `127.0.0.1` due to another bug that wouldn't let me actually access the database.
<br> &nbsp; And while doing so, I also added the `trusted_domains` - these are thingies that you enter in your browser. It will not let you log in if you're not coming from one of these.
<br> &nbsp; Remember how it also contained `APCu` php thingie in the `dnf` command earlier? It comes into play now, added the memory cache line: `'memcache.local' => '\OC\Memcache\APCu',`

 &nbsp; That's it. Logged in via browser, created some user accounts, groups, uploaded a logo (an image of a bunny of course) and renamed it to Bunnycloud. :]

{% include image.html
  img="assets/bunnycloud.png"
  title="A Bunnycloud."
  caption="A Bunnycloud."
  url="http://rhea-ayase.eu/assets/bunnycloud.png"
  align="left"
  float="false"
  border="1px"
%}

##### Houston, we have a problem...

 &nbsp; So nextcloud has some cron stuff that it would like to run periodically. I fixed it up to run from cron, and it turns out, that it's killing my `httpd` :D
<br> &nbsp; Second issue that was bugging me was that it would just timeout from outside of my network. The problem turned out to be in my Cloudflare configuration...



 &nbsp; Thank you for taking the time to read this insane journey. It took two days, more than eight hours each. I used the two days of public holiday for it.

 &nbsp; [Check out my awesome website running in my OpenShift!](http://example.openshift.persephone.cloud:8080/)

