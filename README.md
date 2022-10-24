# stalker-gamma-linux-guide
A guide to getting S.T.A.L.K.E.R. - G.A.M.M.A. running on GNU/LINUX.

DISCLAIMER:
This guide is more of a compilation of info that I have gathered together from others in the GAMMA and Linux community that I have simply put together along with a few of my own findings, and (hopefully) made more digestible. This guide may not work for you, your setup is almost certainly different, this is Linux after all, there may also be things I have forgotten to mention here, and there are probably typos. That being said I am fairly confident this will work for most people.

You can message me on Discord, EXTRAORDINARY INTELLECT#5373, please avoid asking GAMMA support for help, they do not currently support Linux, and probably can only do so much to help anyway.

As of October 23, 2022, the GAMMA installer uses powershell, currently, as far as I know, there is not a way to run the installer on Linux.<br />I recommend you boot up a Windows VM and install GAMMA there, confirm it works, and then copy the files over to Linux.<br />This guide will not be covering that part in depth, but a word of advice; depending on how you choose to copy the files over, you may leave some behind in the process due to folder/file name lengths.<br />One easy although brute way to avoid this is by compressing it before transferring, and then extracting it in Linux.

Okay, you have the GAMMA files on your distro ready to go, now what?

You have two options, running the game through Lutris with Wine, or you can try adding MO2 (Mod Organizer 2) to Steam, and running it through Proton, this has worked for atleast one person on SteamDeck. I will be covering the Lutris+Wine route, because that is what has worked for me and a few others.

I will be assuming that you have used Lutris/Wine before and know atleast the basics of configuration.
You'll want to add ModOrganizer.exe to Lutris, and then configure as follows:
The version of Wine I got GAMMA working on is the latest development build (7.19 as of writing). For me, the built in Wine versions that come with Lutris did not work. They may or may not for you, if not, experiment; try the latest wine-devel first.
Make sure DXVK and VKD3D are enabled, Esync caused issues for me so I disabled it.
For the Winetricks prefix, I enabled the following DLLs:
- cmd
- d3dcompiler_47
- d3dx10
- d3d11_43
- d3dx9
- dx8vb
- dxvk
- quartz
- vcrun2019

With that, you should now atleast be able to launch MO2, and configure further from there;

If you installed GAMMA in Windows, and then copied over the files, your file paths will certainly be messed up, this is why MO2 is asking you where your game is, when you click browse it will open up the Wine file system, you will notice it is similar to your Linux file system, simply with "Z:\" appended to the front, find your Anomaly folder and point Mod Organizer to it.

You should be looking at the main MO2 window now, if it looks like UI elements are missing (black boxes etc.), try changing Wine versions.
Ctrl+S will open a settings window, if that doesn't work, top left>Tools>Settings.
Go to the Theme tab and choose 1809 Dark Mode.
Go to the General tab on untick "Check for updates", this hasn't caused any issues yet, but just in case.
You can close the settings window now, next you need to tell MO2 where the game executables are.

In the large drop down menu next to the Play button, click <Edit...>
Select Anomaly Launcher in the list, for the Binary path, you want to point it to AnomalyLauncher.exe, it will be in the root folder of the game (Anomaly), it will probably take you to the right place by default.
For the Start in path, point it at the folder which AnomalyLauncher.exe is in, you can copy the path you set from above and remove "AnomalyLauncher.exe" from it.
If you want to configure the other executables, you can do so, they are contained within the bin folder at the root of the game, however it isn't necessary.

At this point, you should be able to run AnomalyLauncher through MO2, launch the game, and the game should at least run, but you may have severe stuttering if you press keys rapidly and move your mouse simultaneously, if this is the case, you must remove reshade;
Close the game and MO2, navigate to the Anomaly folder, open the bin folder, and inside delete (or better yet move to another location):
- reshade-shaders
- d3d9.dll
- dxgi.dll
- G.A.M.M.A.Reshade.ini
- ReShade.ini

By now, you should have a fully playable (though likely imperfect) S.T.A.L.K.E.R. - G.A.M.M.A. experience on Linux.


Thanks:<br />no.#3094 (LafreSita) - Groundwork for the wineprefix.<br />yeyande#9033 (yeyande) - Unintentionally helping me find the cause of the key repeat stutter.





