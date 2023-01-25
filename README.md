
<h1>A guide to getting S.T.A.L.K.E.R. - G.A.M.M.A. running on GNU/Linux.</h1>  
<h4>(Henceforth referred to as Linux, cope.)</h4>



*If you are looking for a Steam Deck guide, check [this guide](https://github.com/maxastyler/S.T.A.L.K.E.R.-Gamma-Steam-Deck-Install-Guide/) out.*

<h4>DISCLAIMER:</h4>

This guide is more of a compilation of info that I have gathered together from others in the GAMMA and Linux community that I have simply put together along with a few of my own findings. This guide may not work *for you,* everybody has a different set-up, there may also be things I have forgotten to mention here, my methodology may seem strange to experienced users, and there are liekly typos. That being said I am fairly confident this will work for most people.  

I don't use Discord anymore, if you need help and you can't get it anywhere else, make an issue.  
I will _still be merging pull requests_, but since I'm not using Discord, and it is a prerequesite to install GAMMA, I won't be updating the guide with my own findings. If you are unhappy about this, please fork it and do it yourself.

<br>

<ins>***Avoid asking GAMMA support for help with Linux,***</ins> they do not currently support Linux, and can only do so much to help anyway.
If you have any info to add to the guide; make a _pull request_.

As of November 29, 2022, the GAMMA installer uses powershell;  
As far as I know, <ins>there is not a way to run the installer on Linux.</ins>  
A few people have tried it with powershell for Linux, it has not worked so far.  
Grok has plans to rebuild the installer without powershell eventually.  

I recommend you boot up Windows (VM or otherwise), with 130GB (or 140GB to be safe) of free storage, and install GAMMA there following the standard installation instructions, <ins>***CONFIRM IT WORKS***</ins>, including that the proper number of mods are enabled and that the game launches to the main menu, and then copy the files over.
Depending on how you choose to copy the files over, you may leave some behind in the process due to folder/file name lengths.  
- An easy way to avoid this is by compressing before transferring, and then extracting in Linux. A .7z with a compression level of 5 leaves this with a bit over 30GB to transfer.
- A shared folder in your VM between your Linux host and Windows 10 guest would be optimal for this, if supported by your choice of VM.
- Otherwise, consider using an external storage drive, a USB drive, or similar physical methods for high speed transferring. You could upload the compressed file to a service such as Mega and re-download it if not possible, but it may not be viable depending on your internet upload/download speed or data caps.

<br>

<h4>Okay, you have the GAMMA files installed, copied over, and ready to go, now what?</h4>

<br>

You have two good options, running the game through Lutris with Wine, or through Steam with Proton.  
I will be covering the Lutris/Wine route, because that is what has worked *for me* and a few others.  
<ins>If you are interested in going down the Steam/Proton road, then look at [this guide](https://github.com/maxastyler/S.T.A.L.K.E.R.-Gamma-Steam-Deck-Install-Guide/).</ins>

I will be assuming that you have used Lutris/Wine before and know the basics of configuration.  
Add ModOrganizer.exe to Lutris, and then configure as follows:  

Try using the Proton Wine version. It should offer you higher FPS (almost native) and smoother mouse movement compared to other runners.
If Lutris Proton is your choice, consider setting your GAMMA Wineconfig's version to Windows 10. It should help with FPS even more.

However, the built in Wine versions that come with Lutris may not work *for you*, if not, experiment (Possibly try the latest Wine development branch.)

Make sure DXVK and VKD3D are enabled.
- Esync *may* cause issues, disable it if unsure.

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
- Eg. Z:\home\yourusername\Games\GAMMA\Anomaly Vanilla\AnomalyLauncher.exe  -->  Z:\home\yourusername\Games\GAMMA\Anomaly Vanilla\
- Mod Organizer 2 will automatically turn a forward slash into a backslash, so you can copy the path of your .exe file directly from your file browser. However, you will have to add Z: in front of / before clicking Apply/OK.

If you want to configure the other executables, you can do so, they are contained within the bin folder at the root of the game, however it isn't necessary.

<br>

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
- G.A.M.M.A.Reshade.ini    (If following the next step to use shaders on Linux, do not delete this file.)
- ReShade.ini

iia.
If you cannot go without fancy shaders, consider using [GShade](https://github.com/HereInPlainSight/gshade_installer) instead. 

It's compatible with existing ReShade presets, and runs natively on Linux. 
- Do install to custom game, say yes to dxgi, and point the executable selection to the single specific /bin/ .exe you wish to use it with (Eg. AnomalyDX10.exe OR AnomalyDX10AVX.exe)
- Move your G.A.M.M.A.Reshade.ini from the /bin/ folder into the newly created /bin/gshade-presets/Custom/ folder and navigate to it in GShade while loaded into GAMMA. It might need a moment to compile after being selected.
- Should work out of the box, but it will lag GAMMA hard on your first save load as it has to compile ~230 shaders.
- If you want to mess around with the shader menu in game, make a save first. It does not block mouse input from the game, and you might end up throwing a grenade and causing a faction war. Also, for this reason it would not be recommended for a permadeath run.

iii.
The FPS limiter present in the graphics settings may lead to choppiness and sharp screen tearing. Consider using VSync without the FPS limiter instead. (This was tested with Nvidia's proprietary Linux drivers on plain Arch Linux and may not at all apply to you.)


<h4>By now, you should have a fully playable (though likely imperfect) S.T.A.L.K.E.R. - G.A.M.M.A. experience on Linux.</h4>


<h3>Thanks to:</h3>
 
[All the Contributors](https://github.com/DravenusRex/stalker-gamma-linux-guide/graphs/contributors)  

no.#3094 (LafreSita) - Groundwork for the wineprefix.  

yeyande#9033 (yeyande) - Unintentionally helping me find the cause of the key repeat stutter.  

maxastyler and his [Steam Deck Guide](https://github.com/maxastyler/S.T.A.L.K.E.R.-Gamma-Steam-Deck-Install-Guide/)




