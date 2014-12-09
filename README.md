grandfatherclock
================
A simple cron job to simulate a grandfather clock. 

Designed for a server installation of Ubuntu (wife says: gotta make that server do something cool than watch it sitting around doing nothing and taking up space.)

Manual Ubuntu Install

# Part 1 - Enable audio on server (if needed)
## Step 1 - Login as `root`
    user@machine:~$ sudo -i


## Step 2 - Install audio packages
    root@machine:~$ apt-get install libasound2 libasound2-plugins alsa alsa-utils alsa-oss pulseaudio pulseaudio-utils


## Step 3 - Finish setup of audio
    root@machine:~$ usermod -aG pulse,pulse-access root
    root@machine:~$ pulseaudio -D --system


## Step 4 - Reboot the server and log back in as `root`
    root@machine:~$ shutdown now -r


## Step 5 - Adjust audio levels, if needed
Note: if this is a server, the levels maybe muted and.or turned down.

    root@machine:~$ alsamixer

* What does the alsa mixer look like? (http://howto.blbosti.com/2010/03/ubuntu-server-install-alsa-sound-and-moc-music-on-console/)

# Part 2 - Install `grandfatherclock`
## Step 1 - Login as `root`
    user@machine:~$ sudo -i

## Step 2 - Install `git` if not installed
    root@machine:~$ apt-get install git
    
    
## Step 3 - Clone the `grandfatherclock` project
    root@machine:~$  git clone https://github.com/wanchic/grandfatherclock.git


## Step 4 - Move the `grandfatherclock` cron file to `/etc`
    root@machine:~$  cd grandfatherclock
    root@machine:~/grandfatherclock$  mv grandfatherclock /etc/cron.d/. 


## Step 5 - Move the audio files over
    root@machine:~/grandfatherclock$  mv westminster_bells /usr/share/grandfatherclock 


## Step 6 - Test the audio
    root@machine:~/grandfatherclock$  mplayer /usr/share/grandfatherclock/westminster-01.wav 

* Be sure you plugged some speakers into your server.  (^_^)
* Be sure they are turned on, turned up a bit, and working. (^_^)
* If this does not work, try adjusting the alsamixer back in Part 1 - Step 5.
 

## Step 7 - use `vi`, `vim`, or `nano` to edit or observer the cron file
    root@machine:~/grandfatherclock$  cd /etc/cron.d/grandfatherclock

* See Part 3 - Setup, for more information.

## Step 8 - Restart CRON service
    root@machine:~$ /etc/init.d/cron restart


# Part 3 - Setup

## Notes
The cron is currently setup to play from 7am to 10pm, 7 days a week. It will also play on every quarter of the hour. With this being a simple cron file, you have the flexibility to adjusting the times however you want! Enjoy (^_^)

    15 07-21  * * *   root   mplayer /usr/share/grandfatherclock/westminster-15.wav
    30 07-21  * * *   root   mplayer /usr/share/grandfatherclock/westminster-30.wav
    45 07-21  * * *   root   mplayer /usr/share/grandfatherclock/westminster-45.wav
    
    00 13     * * *   root   mplayer /usr/share/grandfatherclock/westminster-01.wav
    00 14     * * *   root   mplayer /usr/share/grandfatherclock/westminster-02.wav
    00 15     * * *   root   mplayer /usr/share/grandfatherclock/westminster-03.wav
    00 16     * * *   root   mplayer /usr/share/grandfatherclock/westminster-04.wav
    00 17     * * *   root   mplayer /usr/share/grandfatherclock/westminster-05.wav
    00 18     * * *   root   mplayer /usr/share/grandfatherclock/westminster-06.wav
    00 07,19  * * *   root   mplayer /usr/share/grandfatherclock/westminster-07.wav
    00 08,20  * * *   root   mplayer /usr/share/grandfatherclock/westminster-08.wav
    00 09,21  * * *   root   mplayer /usr/share/grandfatherclock/westminster-09.wav
    00 10,22  * * *   root   mplayer /usr/share/grandfatherclock/westminster-10.wav
    00 11     * * *   root   mplayer /usr/share/grandfatherclock/westminster-11.wav
    00 12     * * *   root   mplayer /usr/share/grandfatherclock/westminster-12.wav



