A GUI interface using jbaiter's pyomxplayer wrapper to control omxplayer

INSTALLATION
============

Instructions for installation on the official Raspbian image:

You can use the automatic installer, or if that does not work for some reason you can install it manually.

To download and run the installer, from a terminal window, type (or copy-paste):

        cd ~ && wget https://github.com/KenT2/tboplayer/tarball/master -O - | tar xz &&
        cd KenT2-tboplayer-* && chmod +x setup.sh && ./setup.sh
	
After that, TBOPlayer will have been installed on your system. To run it, just type 'tboplayer', or use the shortcut created in your Desktop.

If you prefer to install it manually, do as follows:
	
Update omxplayer
-----------------------------

Ensure you have the latest version of omxplayer by typing the following in a terminal window:

        sudo apt-get update
        sudo apt-get install --only-upgrade -y omxplayer

Install dependencies
-----------------------------

Type this into the terminal to install TBOPlayer's dependencies:

        # install pip, gobject, gtk, requests, avconv, ffmpeg
        sudo apt-get install -y python-pip python-gobject-2 python-gtk2 python-requests libav-tools ffmpeg
        # install pexpect, ptyprocess
        yes | pip install --user pexpect ptyprocess
        # install youtube-dl
        sudo wget https://yt-dl.org/downloads/latest/youtube-dl -O /usr/local/bin/youtube-dl
        sudo chmod a+rx /usr/local/bin/youtube-dl
        # or update youtube-dl
        sudo youtube-dl -U

Download and Install TBOPlayer
------------------------------

From a terminal window, type:

        cd ~ && wget https://github.com/KenT2/tboplayer/tarball/master -O - | tar xz

There should now be a directory 'KenT2-tboplayer-xxxx' in your home directory. Rename the directory to tboplayer.

To run TBOPlayer, type in a terminal window:

        python /home/pi/tboplayer/tboplayer.py

where pi is the name of your system's user.

TBOPlayer is developed on Raspbian Wheezy with python 2.7

OPERATION
=========

Buttons
-------

* `ADD` - duplicates the Track>Add menu item

* `ADD DIR` - duplicates the Track>Add Dir menu item

* `EDIT` - duplicates the Track>Edit menu item

* `OPEN/SAVE/CLEAR LIST` - duplicates the Playlist>Open,Save,Clear menu item

* `PLAY/PAUSE` - Play the selected track or pause if playing

* `STOP` - Stop playing, operational only during playing

* `PREVIOUS` - Play previous track, operational only after played some track

* `NEXT` - Play next track, up to mode that you set

* `- VOL +` - Minus/plus volume control

Menus
-----
* `Track` - add tracks (for selecting multiple tracks, hold ctrl when clicking) or directories, edit or remove tracks (or URLs) from the current playlist
 
* `Playlist` - save the current playlist or open a saved one or load youtube playlist
 
* `OMX` - display the track information for the last played track (needs to be enabled in options)
 
* `Options` -

    * Audio Output - play sound to hdmi or local output, auto does not send an audio option to omxplayer.
	
    * Mode - play the Single selected track, Repeat the single track, rotate around the Playlist starting from the selected track, randomly play a track from the Playlist.
	
    * Initial directory for tracks - where Add Track starts looking.
	
    * Initial directory for playlists - where Open Playlist starts looking
	
    * Enable subtitles

    * OMXPlayer location - path to omxplayer binary

    * OMXplayer options - add your own (no validation so be careful)
    
    * Download from Youtube - defines whether to download video and audio or audio only from Youtube (other online video services will always be asked for "video and audio")
     
    * Download actual media URL [when] - defines when to extract the actual media from the given URL, either upon adding the URL or when playing it
    
    * Youtube media quality - lets you choose among "small", "medium" and "high" qualities (Youtube only feature)
    
    * youtube-dl location - path to youtube-dl binary
    
    * youtube-dl transcoder - prefer to use either avconv or ffmpeg when using youtube-dl for extracting data from online supported services
    
    * Start/End track paused - Pauses the track both in the beginning and in the end of the track
    
    * Forbid windowed mode - if enabled will make videos always show in full screen, disabling the video window mode and video progress bar - useful if you're using tboplayer through a remote desktop
	
    * Debug - prints some debug text to the command line
	
    * Generate Track Information - parses the output of omxplayer, disabled by default as it may cause problems with some tracks


A track is selected using a single click of the mouse or up-down arrow key, playing is started by pressing the Play/Pause button, the . key or the Return key.

Removing the selected track can be done by pressing the Delete key.

During playing of a track, a clickable progress bar will appear below the playlist, which lets you seek a position, and if playing a video it's possible to see the progress bar if you move your mouse to the lowest side of the video.

Again during playing of a track, a slightly modified set of omxplayer commands can be used from the keyboard but there must be FOCUS on TBOPlayer. A list of commands is provided in the help menu. Note: some of the commands are not implemented by omxplayer. 

While playing videos, you can hit the F11 key for toggling full screen mode. In windowed mode, to move the video window, click and hold the first mouse button over the video area and then move the mouse; and to resize the video, hold left Control, click and hold the first mouse button over the video area and then move the mouse.

For a list of streaming services supported by youtube-dl, see this link: https://rg3.github.io/youtube-dl/supportedsites.html (not all of them were tested with TBOPlayer/OMXplayer)

TROUBLESHOOTING
=========

If you have problems playing a track try it from the command line with `omxplayer -o hdmi filename` or `omxplayer -o local filename` to make sure it's not a problem with omxplayer.

If the progress bar, volume bar, or windowed video mode don't work for you, it may be that you have another instance of omxplayer running in the background. In that case, you can try to close that instance, and then play the track again. You can force omxplayer to terminate by typing in a terminal: `sudo pkill -9 omxplayer`

In Raspbian, youtube-dl should always be up-to-date, but if you use another OS and keep getting a lot of "Content may be copyrighted or the link invalid" when trying to play videos from streaming services supported by youtube-dl, you can try to update youtube-dl by typing in a terminal: `sudo youtube-dl -U`

If the videos appear displaced by any amount of pixels, you must be having overscan problems. To disable overscan go to Menu>Preferences>Raspberry Pi Configuration and then set Overscan to Disabled.

Contributors:
-------------

KenT2 - Original idea and implementation

popiazaza - GUI enhancements

heniotierra - GUI enhancements and youtube-dl integration

krugg - GUI enhancements
