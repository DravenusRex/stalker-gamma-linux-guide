# stalker-gamma-linux-guide
<h3>A guide to getting S.T.A.L.K.E.R. - G.A.M.M.A. running on GNU/Linux.</h3>  
<h4>(Henceforth referred to as Linux, cope.)</h4>
<br>

If you are looking for a Steam Deck guide, check [this guide](https://github.com/maxastyler/S.T.A.L.K.E.R.-Gamma-Steam-Deck-Install-Guide/) out.  

DISCLAIMER:
This guide is more of a compilation of info that I have gathered together from others in the GAMMA and Linux community that I have simply put together along with a few of my own findings. This guide may not work *for you*, everybody has a different set-up, there may also be things I have forgotten to mention here, my methodology may seem strange to experienced users, and there are liekly typos. That being said I am fairly confident this will work for most people.

You can message me on Discord, "Dravenus Rex#5373", please avoid asking GAMMA support for help, they do not currently support Linux, and can only do so much to help anyway.  
If you have any info to add to the guide; message me on Discord or make a pull request.

As of November 29, 2022, the GAMMA installer uses powershell;  
As far as I know, <ins>there is not a way to run the installer on Linux.</ins>  
A few people have tried it with powershell for Linux, it has not worked so far.  
Grok has plans to rebuild the installer without powershell eventually.  
I recommend you boot up Windows (VM or otherwise) and install GAMMA there following the standard installation instructions, <ins>***CONFIRM IT WORKS***</ins>, including that the proper number of mods are enabled and that the game runs, and then copy the files over;  
Depending on how you choose to copy the files over, you may leave some behind in the process due to folder/file name lengths.  
An easy way to avoid this is by compressing before transferring, and then extracting in Linux.

Okay, you have the GAMMA files installed, copied over, and ready to go, now what?

You have two good options, running the game through Lutris with Wine, or through Steam with Proton.  
I will be covering the Lutris/Wine route, because that is what has worked *for me* and a few others.  
<ins>If you are interested in going down the Steam/Proton road, then look at [this guide](https://github.com/maxastyler/S.T.A.L.K.E.R.-Gamma-Steam-Deck-Install-Guide/).</ins>

I will be assuming that you have used Lutris/Wine before and know the basics of configuration.  
Add ModOrganizer.exe to Lutris, and then configure as follows:  
The built in Wine versions that come with Lutris did not work *for me*. They may or may not *for you*, if not, experiment;  
Try the latest Wine development branch next. *For me*, Wine 7.19 worked fine.  
Make sure DXVK and VKD3D are enabled.  
Esync caused issues *for me* so I disabled it.  
For the wineprefix, enable the following DLLs:  
- cmd
- d3dcompiler_47
- d3dx10
- d3d11_43
- d3dx9
- dx8vb
- dxvk
- quartz
- vcrun2019

With that, you should now atleast be able to launch Mod Organizer (henceforth MO2), and configure further from there;

Since you installed GAMMA in Windows, and then copied over the files, your file paths will be messed up, this is why MO2 is asking you where your game is, when you click browse it will open up the Wine file system, find your Anomaly folder and point MO2 to it.

You should be looking at the main MO2 window now, if UI elements are missing (black boxes etc.), try changing Wine versions.  
Confirm that the proper number of mods are enabled, you can find the correct number in the GAMMA discord.  
If this number is 0, you did not give MO2 the correct path to your game, you can change the path to your game in the following settings window under the "Paths" tab.  
If it's another number, something bad happened during the file transfer, or you didn't confirm the game was proper under Windows.  
Ctrl+S will open a settings window, if that doesn't work, top left>Tools>Settings.  
Go to the Theme tab and choose 1809 Dark Mode.  
Go to the General tab on untick "Check for updates", this hasn't caused any issues yet, but just in case.  
You can close the settings window now, next you need to tell MO2 where the game executables are.  

In the large drop down menu next to the Play button, click "<Edit...>"
Select Anomaly Launcher in the list, for the Binary path, you want to point it to AnomalyLauncher.exe, it will be in the root folder of the game (Anomaly), it will probably take you to the right place by default.
For the Start in path, point it at the folder which AnomalyLauncher.exe is in, you can copy the path you set from above and remove "AnomalyLauncher.exe" from it.
If you want to configure the other executables, you can do so, they are contained within the bin folder at the root of the game, however it isn't necessary.

At this point, you should be able to run AnomalyLauncher through MO2, launch the game, and the game should at least run, although with a few issues:

i.  
The game window might not properly size to your screen, and might just even appear as a small black window, if this is the case:
- Edit the user.ltx file found in /Anomaly/appdata/
- Change rs__screenmode (fullscreen/borderless/windowed), different options work for different set-ups.
- Double check that vid_mode is set correctly according to your display, e.g. vid_mode 1920x1080

ii.  
You may have severe stuttering if you press keys rapidly and move your mouse simultaneously, if this is the case, remove reshade;  
Close GAMMA and MO2, navigate to the Anomaly folder, open the bin folder, and inside delete (or better yet move to another location):
- reshade-shaders
- d3d9.dll
- dxgi.dll
- G.A.M.M.A.Reshade.ini
- ReShade.ini

iia.  
If you remove Reshade it is recommended that you disable the mods that use it:
* Screen Space Shaders - Ascii1457
* Shaders Cumulative Pack for GAMMA
* Right click Beef’s NVG addon, click “reinstall mod” and tick the following options:
  * Beef’s NVG
  * Beef’s NVG - Patch ES
* Delete anomaly/appdata/shaders_cache folder

By now, you should have a fully playable (though likely imperfect) S.T.A.L.K.E.R. - G.A.M.M.A. experience on Linux.


Thanks:  
no.#3094 (LafreSita) - Groundwork for the wineprefix.  
yeyande#9033 (yeyande) - Unintentionally helping me find the cause of the key repeat stutter.  
maxastyler and his [Steam Deck Guide](https://github.com/maxastyler/S.T.A.L.K.E.R.-Gamma-Steam-Deck-Install-Guide/)




