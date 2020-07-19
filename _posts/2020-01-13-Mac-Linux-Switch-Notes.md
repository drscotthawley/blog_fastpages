---
toc: true
image: https://i.imgur.com/ebIVLhK.png
description: Mac and I aren't breaking up, we're just seeing other people.
---



# Mac ⇒ Linux Switch Notes

*Mac and I aren't breaking up, we're just seeing other people.*

## Intro 

I'd been jonesing for a laptop with a real GPU for a couple years.  Granted, most of my computation occurs on remote servers, but sometimes when I'm traveling, those connections can be spotty.  And heck, I might want to play the occasional video game (without NVIDIA GeForce NOW). 

Twenty years ago, I switched from Linux/Windows dual-boot to Mac so I could get shiny apps, and to not have to worry about device drivers, etc.  But with Apple dragging their feet re. hardware upgrades, I finally took the plunge -- *before* my Mac died, so I'd have plenty of time to transition.    

Got a [System76 Oryx Pro](https://system76.com/laptops/oryx). With Pop!\_OS 19.10 --- I'm used to Ubuntu, so this is a bit new.  I'm so impressed with the System76 folks that I want to try to stay with their Pop!\_OS because I know they've been doing the tweaking so it'll work well with their laptops, and also so I can legit bug them when I hit problems. ;-)  Like Ubuntu, Pop!_OS is a Debian variant, so much of the same actions apply.

Similar posts by others:

*  https://www.theportlandcompany.com/2017/08/14/switching-mac-ubuntu-gnome-17-04/
* http://www.matthewbuscemi.com/blog/2019-06-05-the-great-linux-migration-of-2019.html



## Syncing with Apple Ecosystem

*(from within Linux. See below for alleged VirtualBox installation of MacOS)*

I still have an iPad & iPhone, so finding a solution that could sync with what I already have (rather than, e.g., going with Google Calendars) was helpful.

One could simply use iCloud.com via a web browser, but I\'d like to integrate a bit more with the Linux ecosystem.

* **Mail:**

  I tried Geary, Thunderbird & Evolution. Found more online instructions for using Evolution.  Evolution doesn't to do like Mac's Mail.app does, namely integrate all your inboxes into one unified Inbox -- you have to go an check each inbox for each account. [But here's a workaround to fake it](https://www.svenbit.com/2011/05/create-a-unified-inbox-folder-in-evolution/).   (Thunderbird supports a [nice unified inbox](https://support.mozilla.org/en-US/questions/1009047) view. Note that Thunderbird's font size is minuscule, but [you can rescale it](https://support.mozilla.org/en-US/questions/1276127).)

  My account types: Gmail and Microsoft Exchange.

* **Calendar:**

  Evolution will integrate with Apple: https://ar.al/2018/08/05/using-icloud-calendars-on-gnu-linux/

  Note that accounts added in Evolution will propagate to default Gnome Calendar app too, but there's no way to get Gnome to add new Apple calendars; only Evolution provides this functionality, it seems. 

* **Contacts:**

  Evolution again: https://ar.al/2018/08/05/getting-your-icloud-contacts-on-gnu-linux/

  Sadly, unlike the Mac, when you try to *use* the contacts, for example when you start addressing an email, it won't prioritize the search/matching list by the most recent people you've actually contacted.  Rather the names of people you haven't interacted with in years will dominate the list of names. 

* **Notes (wrapper to web app):**

  iCloud Notes Snap: https://www.addictivetips.com/ubuntu-linux-tips/use-icloud-on-linux/

  All this thing is is a web browser that connects to Apple\'s iCloud notes page. So no using this offline.  Note that you have to log out & back in before you see Snap apps.  **Also note** that Hide/Minimize on this window will make it *almost impossible to recover*. (??) Thus I tend to move the window to another desktop. 

* **Messages (SMS)**

  TL/DR: It's a no-go. 

  There is no iCloud version of Messages. Apple won\'t allow 3rd party apps.

  [Gnome Phone Manager](https://wiki.gnome.org/Attic/PhoneManager) was supposed to let you pair with your phone via Bluetooth and then send & receive messages, but it's obsolete now and I couldn't get it to work. 

  KDE has a \"Connect\" app, but I\'m not abandoning all the Gnome setup I've done to switch to KDE!  And it probably only works with Android.

  [Wammu](https://wammu.eu/) is unable to connect to my (Bluetooth-paired) phone.

  You could configure your old Mac as a remote Messages server, but this implementation is insecure: https://github.com/cvincent/umessage

  Verizon doesn\'t offer a Linux version of their Message+ app, but you can send/receive via their web site.

  ...One could always use some alternate messaging 'ecosystem' like [WhatsApp's web app](https://web.whatsapp.com/) or Signal, but I was looking for ways to get 'regular' SMS messages for my existing number. :-/

* **Files**: 

  Honestly Dropbox is fine!  I turned on ssh 'sharing' on my Mac so I can `scp` files if I need to, but Dropbox on Linux is as easy as one would imagine. 

* **Music**:

  For actual audio production, I'll need to keep the Mac around for Logic & Pro Tools.  As far as casual listening to music,...eh. I'm fine with Pandora.  (I'm not a Spotify user.)  **Note:** Did get [studio audio working under Linux](https://twitter.com/drscotthawley/status/1214424186464194560) though! See below under "Audio".

* **Backups:** 

  I have an Apple "Time Capsule" WiFi-cum-backup server.  [It's not going to be possible to back up *both* the Mac and the Linux machine to the same device](https://apple.stackexchange.com/questions/160250/backup-of-a-debian-machine-to-an-apple-time-capsule).  I'll need to choose which machine to back up there. Some have suggested getting a Raspberry Pi and mount a $30 2TB HD to it for backing up the Linux machine. **TODO.**

  

## CUDA / Tensorflow / PyTorch

TL/DR: this was the grand hope of buying this computer. Still not able to run yet, but I'll never give up. ;-) 

This main challenge, as with any system really, is grabbing a version of CUDA that will allow you to grab at least a few binaries:

* Latest CUDA via [system76\'s distro](https://support.system76.com/articles/cuda/) is 10.2.  They don't offer 10.1 anymore.

* PyTorch builds only support up to 10.1.  To get CUDA 10.2 support, I built PyTorch from source.  My research code isn't running...I suspect because something in PyTorch changed re. multiprocessing support. :-(.
* System76 made a \"[tensorman](https://github.com/pop-os/tensorman)\" docker util. I confess to my shame that I still find docker to be rather confusing.  Using tensorman, I was able to run their tiny demo but not my own research codes.  I tried building my own docker image but....didn\'t enjoy it. Went back to what I know: Anaconda.  Still no success.  TODO: Will update. 

* Tensorflow binaries go up to CUDA 10.0.   I\'d built tensorflow-gpu from source multiple times on Ubuntu systems\...but I spent 3 days on this thing and still haven\'t gotten it to build. Some kind of error with grpc at gettid. :-/  **OOoo! Got it!**  Uh, at least, it compiles. 



## Document Editing

* **Markdown**: Over the years, I've tried a number of Markdown editors -- Haroopad, Mou, Ghost, StackEdit.  Then today I discovered [Typora](https://typora.io).  It is my favorite by far!   

* **Code:** I like Atom or VSCode for code (same as I did on the Mac).

* **Office:** LibreOffice seems, so far, to be able to read & write my Microsoft Office files without mangling them!  It's *uglier*, but that's par for the course. 

* **(Nonfiction) Book authorship:** 
  * I'd been working on a book using Scrivener 3.  Scrivener released a(n unofficial) [Linux port](https://www.steinberg.net/forums/viewtopic.php?f=157&t=62290&sid=83ae2e7f166857420498e68412dfea4f&start=25) but it's old.  Linux users now typically either run the Windows or Mac versions however they can.  See "MacOS on Linux via VirtualBox", below. (**Score!** Mac license key successfully-hypothetically accepted in VirtualBox guest OS.)
  * Alternatives: [Manuskript](https://www.theologeek.ch/manuskript/) (cf. novelist [Matthew Buscemi's notes on switching from Scrivener to Manuskript](http://matthewbuscemi.com/blog/2019-06-07-hello-manuskript.html)), or [Sigil](https://github.com/Sigil-Ebook/Sigil) for EPUBs, [Scribus](https://www.scribus.net/) for print layout,...?   ...Well and of course LaTeX! ;-) 



## Peripherals

One doesn't hope for much with Linux, but I've succeeded with more than I'd hoped for.  As follows...

### Audio

* **Bluetooth pairing** to a Bose Soundlink works fine: Ooo, and the volume buttons on the keyboard control the Bluetooth speaker volume! 

* My **Focusrite** 2i2 USB box works right away -- *sort of*.  The OS recognizes it but then ignores it and just keeps using the laptop defaults regardless of what you set for the System Settings.  Yet Audacity will actually use it correctly. ¯\\\_(ツ)\_/¯.  Officially, Focusrite claims [no Linux support](https://support.focusrite.com/hc/en-gb/articles/208530735-Is-my-Focusrite-Product-compatible-with-Linux-), but allows that you might get lucky since they are USB class-compliant.  **UPDATE:** If you manually set the Sound setting to Internal Speakers and *then* set it to the Focusrite, then the Focusrite gets used for everything.  (Seems that the Plug'n'Play is a bit messed up.)

* My **Steinberg UR44** USB audio interface... was not recognized at first.  There's a [thread from 2014 on the Steinberg forums](https://www.steinberg.net/forums/viewtopic.php?f=157&t=62290&sid=f9bd688247495effd78eecc481c321a2&start=25) for setting up both the UR22 and UR44 on Linux.  They say you need to flip the switch on the back of the device to "Class Compliant (CC)" mode.  Then turn the Steinberg off & on (i.e. unplug the power cable & plug it in) and...voila!  It now shows up!  **[I have studio-quality audio I/O!!](https://twitter.com/drscotthawley/status/1214424186464194560)**

### Video 

* **External Displays (HDMI):**  One thing that will require getting used to will be the fact that you can only use the HDMI port on the Oryx Pro when the NVIDIA GPU is fully enabled.  You can't use it with the Intel Graphics or Hybrid Graphics.  And switching graphics modes requires a reboot. :-/   But after rebooting, it works!  Too bad the battery life isn't so hot with the NVIDIA card, but that's ok. ;-) 

  ....Uh, and apparently it refuses to route audio through HDMI even though it should.  Hmm.  Found this out the hard way when teaching a university class to audio engineering students. :-(

### Apple Wireless Keyboard

* The Pop!\_OS/Gnome GUI-based Bluetooth pairing method wasn't working super great, so I started out following [these command-line instructions](http://freewisdoms.com/apple-wireless-keyboard-on-ubuntu/) and then switched over to to Pop!_OS GUI once the scan was in progress.  

  >  Currently typing these words on my wireless keyboard, with the laptop in the closet, looking at my external monitor connected via HDMI, listening to external monitor speakers controlled by the Steinberg UR44! :)

  

## Customization 

* **Gnome:**  
  
  * System76 posted a [list of handy Gnome extensions](https://support.system76.com/articles/customize-gnome/).
  * [Gnome Tweaks](https://itsfoss.com/gnome-tweak-tool/), e.g. for adding Minimize/Maximize buttons to the windows!  The default Gnome desktop...I do not understand what those developers are thinking, other than "Let's waste screen real estate."
  
* **Keyboard Colors (on Oryx Pro):** There are a few utilities out there. I went with [this one](https://github.com/davemcphee/oryx-kb-leds). Note that there are only three \"zones\" of color definable, not controls for each key. Also had to use `sudo` to enable user writing to appropriate `/sys/` devices.

* **Scrolling:** Unlike the Mac, the trackpad scrolling behavior seems to be app-specific.  As I write this, Typora doesn't offer any inertia -- also called "coasting" -- whereas a few Gnome apps (except Terminal!) offer near-perfect Mac-like inertia scrolling, whereas Thunderbird, Atom & VSCode offer none.  **SOLUTION:**  Install the "Synaptics" (legacy) driver:

  `sudo apt install xserver-xorg-input-synaptics`

  ...then log out & log back in. Now things are *much* better; it's a  **pretty buggy** and sometimes the kinetic scrolling won't kick in, and other times it will. But this is a vast improvement.  (Note: I did *not* uninstall `libinput` but rather left it in.)
  
  **Oh but wait!**  On reboot the trackpad was dead!  The only solution was to *uninstall* the synaptics driver :-( and now the trackpad works again. 
  
  

## MacOS on Linux via VirtualBox

(Given Apple's EULA, the following is purely a hypothetical scenario *for discussion purposes only.*..)

Sometimes one may simply need a particular Mac app.  This ["semi-automated install script" described on the VirtualBox Wikibooks page](https://en.wikibooks.org/wiki/VirtualBox/Setting_up_a_Virtual_Machine/Mac_OS_X) is...I am told, hypothetically...awesome!  It will -- allegedly, mind you -- automatically grab the MacOS ISO and set everything up!   *(Note that the first time that hypothetical-me might have tried this, hypothetical-me may have missed a bunch of the prompts from the script because the VirtualBox window had obscured the Terminal.  Don't be like said hypothetical-me -- hypothetically you should follow the script, and just press enter at the appropriate moments.)*   And it allegedly mostly "just works." 

 Also: Catalina won't work yet; only Mojave for now.

* **Main Issues:**

  * **Guest Additions** don't get set up. For a long time, VirtualBox didn't have Guest Additions for Mac guests, and then it did, and now the newest VirtualBox (version 6.1) doesn't.  *But* the above script installs version 6.0.14, and for versions 6.0.12 to 6.0.14 there *were* Guest Additions for Mac! [Still available for download here](https://download.virtualbox.org/virtualbox/6.0.14/VBoxGuestAdditions_6.0.14.iso).  Then [following these instructions](https://stackoverflow.com/questions/41691803/how-to-install-guest-addition-in-mac-os-as-guest-and-windows-machine-as-host), one might download this .iso file from within the macOS guest, then mount it (via the Finder), then double-click on the file `VBoxDarwinAdditions.pkg` to install them.  Doing this will enable shared clipboards and...

  * **Shared Folders -- not.**  Once the Guest Additions are up, one may try to create a directory on the Mac client, e.g. `mkdir ~/linux` as a mount point, and set up a shared folder in Virtual Box that could auto-mount to this location.... and then one can hypothetically waste HOURS AND HOURS and never it get it to work, at which point one may give up and just use Dropbox or some \*\*\*\*.  Really I just wanted this for Scrivener, so syncing `~/Dropbox/Documents`  would be sufficient.  

    *Alternatively,* you could use "File Sharing" to setup a Samba server, but...Not gonna. 

  * **Insanely Slow Execution.** Lots of issues with the Mac guest, one of which is that it'll only utilize 1 CPU!

  * **Low Display Resolution** by default. But fixable by changing the EFI resolution, such as by running on the host system the command 

    `$ VBoxManage setextradata "macOS" VBoxInternal2/EfiGraphicsResolution 1600x900`

* For some reason, iMessages won't hypothetically login, even though other aspects of iCloud & AppleID link. No errors, just...doesn't seem to work....so I'm told.

* "Obviously", hardware-stuff like the Facetime camera probably will never work. Don't care. 

  

## Dual Boot - adding Windows

*(Let's be honest: this is just for playing video games.)*

The [System76 instructions](https://pop.system76.com/docs/dual-booting-windows/) seem to start in the middle of something; pretty confusing.  And there's a [second set of System76 instructions](https://pop.system76.com/docs/dual-booting-windows/) with almost the same title.  Turns out the former is for adding Pop!\_OS to Windows, and the latter is for adding Windows to Pop!\_OS. The latter is what I wanted... but... wasn't able to follow what they did.  So....here's what I did:

1. You can't repartition your hard drive while it's being used.  So create a bootable USB image of either [all of Pop!\_OS](https://support.system76.com/articles/pop-live-disk/) or else just the [GParted partitioning tool](https://gparted.org/liveusb.php).  The Popsicle utility is good for flashing USBs. 

2. Restart the machine, hold F7, and select the USB from the boot menu.  Then you can run GParted.  My version looked like the following, where /dev/sda3 is the main partition that started as all Pop!\_OS: 

   ![gparted screenshot](https://i.imgur.com/ebIVLhK.png)

3. All you need to do is resize the big partition to a smaller size.  I made mine such that it would free up 120 GB. You don't need to create a new partition in the newly-unallocated space or format it; Windows will do that. 

4. Get a legit bootable Windows 10 ISO somehow, e.g. by downloading from Microsoft or (mumble mumble).  Mine was super-old which made what follows extra-fun.  (I used a second USB stick by the way).  At least it still had a valid Activation Key. :-) 

5. Restart with with Windows ISO USB inserted, hold F7, boot to the Windows installer.  In the installer, when choosing a partition, choose the empty space that was leftover after you shrunk (shrank?) your main Linux partition. Install Windows there. 

6. Windows installs itself at the *front* of the machine's *rudimentary* boot-loading menu (the F7 thing), meaning that, congratulations, your machine now boots to Windows by default, and I haven't figured out how to change that.  Good news is, the Windows install process will require restarting a *bunch* of times, so at least that will happen automatically (without you having to choose not-Linux over & over).

7. When Windows finally came up, it couldn't detect the WiFI device on the laptop!  That was a bit scary, and  made it rather challenging to download any sort of updates.  Thankfully the Ethernet jack worked, and so I was able to download enough updates so that eventually (after many incremental update-installs and reboot cycles) the WiFi device started working. 

8. Managed to install everything I wanted, included Steam and Uplay.  Got "Rise of the Tomb Raider" for $12 and played it on max settings at 80 to 100 FPS with no trouble. :-)   (Well, note that the machine gets super-hot and the fan runs like crazy, but what do you expect?)

9. Now, every time I want to boot to Linux, I have to remember to hold F7.  ...Oh well.   

## Trouble! 

When I came back to Linux from Windows, the system started hanging intermittently.  I though maybe it was limited to the trackpad but it seems there are [many reports of freezing with Ubuntu 19.10](https://askubuntu.com/questions/1185491/ubuntu-19-10-freezes-and-lags-reguarly) (which Pop!\_OS inherits from) for certain video drivers, and in fact I was in "full NVIDIA mode" when I came back to Linux from Windows.   Tonight I've been typing the rest of this in Hybrid Graphics mode with not a single hang. So...maybe that's all I can hope for for now.  

I'll get by.

....How about we stop there for now.  I'll post another edit of this once PyTorch & Tensorflow are working to my satisfaction.

**P.S.-** Oh hey. I was going to end that last line with a fingers-crossed emoji, only to find out that [Ubuntu and most Linux distributions don't supoort emoji](https://www.omgubuntu.co.uk/2014/11/see-install-use-emoji-symbols-ubuntu-linux) by default, but there is a [Gnome Characters](https://wiki.gnome.org/Design/Apps/CharacterMap) package, which after installing, will let you do this: 🤞😃👍

------

-SH, 1/13/2020. 



