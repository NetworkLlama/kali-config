# kali-config
Scripts and files for how I use Kali so I can automate new setups

One of the hardest things to do in infosec is to develop a comfortable working environment. When you do get it
where you want it, you don't always remember to save it, or where you got things, or why you did stuff. That's
what this is for, because I'm tired of spinning up one-off Kali instances because my main isn't convenient and
then getting annoyed because I forgot to enable or disable some aspect.

I made this repo mostly for my convenience, but you're welcome to use it yourself. If you have ideas to make
something work better, please do bring it up. Please note that some of the configuration items here presume
the presence of certain software packages; if you don't have them, it may throw some errors. I'll try to keep
that to a minimum.

I tend to use apt instead of apt-install, apt-remove, etc. This may cause problems with and require some
adjustment for certain shell environments.

## Requirements
Use of these scripts may presume presence of git. You probably downloaded this via git, but in case you didn't
and some git commands failed, you'll need to run `apt install git` for it to complete properly.

Minimum VM Specs:
* 2 CPU cores
* 4GB RAM
* 20GB drive

Recommended VM Specs:
* 4+ CPU cores
* 16GB RAM
* 60GB drive

Recommended specs are for running on a pretty beefy system. My two personal computers have 4-core Intel i7 and
8-core Intel i9 CPUs with 64GB of RAM and 500GB or larger drives dedicated to VMs. You can get by with the
minimum specs, but expand where you can. I have successfully run this config on a Macbook Pro using two CPU
cores, 8GB of RAM, and 40GB drive, but depending on what you're doing and how much you're sending off to
Shared Folders, it's possible to eat that up quickly.

## kali_setup
A script to set up the basic environment. Note that I usually build for general purpose, so there's a *lot*
that typically gets installed up front. If you need a smaller environment, make sure you reduce or remove at
least some of these.

Things I install:
* Pretty much all the kali-tools packages. Comment out what you don't want. Things that might not be handy on
a VM include -bluetooth, -gpu, -passwords, -rfid, -sdr, and perhaps -wireless. These all require additional
hardware that is not necessarily available, and not installing these reduces download and installation size.
Leaving it as-is may mean a very large and long download.
* I have a preference for Mate over Gnome, especially for VMs where resources may be limited.
* Add Chromium, Tor service, and Tor Browser
* A few other tools that for some reason don't seem to always (or ever) come with, especially vim, plus
initialization of the Metasploit database. I don't use it as much anymore, but better to be ready.
* Git clones (not necessarily installed):
** Rubber Ducky material
** MSSQL-CLI, a lifesaver when accessing (oddly enough) Microsoft SQL database servers. Virtually no setup
required.


## Home files
### .bash_aliases
This mostly contains stuff I got from alexpad's StackExchange answer for automating saving console output. It
saves both raw bash output as well as a simpler text. If you need the color-coded output, cat the appropriate
content and you get all the pretty rainbows back. Otherwise, copy and pase from the text log.

Reference: https://unix.stackexchange.com/questions/200637/save-all-the-terminal-output-to-a-file/318967

Note that these files can get very large over time, so it's a good idea to check in on the directory size once
in a while.

### .bashrc
This has some little things I've done over the years including:
* Disabling history limitations
* Adding timestamps to the history entries
* Adding a timestamp to the bash prompt
* Enabling some ls aliases
* Executing smart_script (see .bash_aliases above)
* Instant history write

NB: Instant history write means that every command is immediately written to history. If you have multiple
tabs/TTYs/sessions/whatever, this can get confusing because pressing up to access previous commands can and
usually will result in a mix of commands from those sessions. This helps keep all your commands, but if
you're bouncing between a bunch of shells, you're going to be hitting the up arrow more often.

### update_all
A simple bash script to update all the various components of Kali, plus some selected additional items. Right
now, it only includes Cobalt Strike (located in /opt/cobaltstrike), but will include some other things later
as they come to mind. Feel free to remove things you don't have.

As this is meant for VMs, it also includes an option to shrink the VM image. Be aware that this can cause
corruption of the image. It's happened two or three times to me, so either be comfortable recreating things or
have a backup--ideally both.

# Feedback
I'm happy to take suggestions or look at bugs here, or you can drop me a line at jfrates at gmail dot com.
