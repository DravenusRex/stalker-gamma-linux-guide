
<h1>A guide to getting S.T.A.L.K.E.R. - G.A.M.M.A. running on GNU/Linux.</h1>  
<h4>(Henceforth referred to as Linux, cope.)</h4>



*If you are looking for a Steam Deck guide, check [this guide](https://github.com/maxastyler/S.T.A.L.K.E.R.-Gamma-Steam-Deck-Install-Guide/) out.*

<h4>DISCLAIMER:</h4>

This guide is a compilation of info that I have gathered together from others in the GAMMA and Linux community.  
This guide may not work *for you,* everybody has a different set-up.  
This guide assumes you have pre-requisite knowledge to use tools like Lutris, Wine, Proton, or whatever you choose.  
If you do not know how to use these tools, there are other resources out there.  
If you need help or have a problem; make an issue.  
If you have any info to add to the guide; feel free to make a PR.  

<ins>***Avoid asking GAMMA support for help with Linux,***</ins> they do not currently support Linux, and can only do so much to help anyway.

As of May 4, 2023, the GAMMA installer uses powershell;  
As far as I know, <ins>there is not a way to run the installer on Linux.</ins>  
A few people have tried it with powershell for Linux, it has not worked so far.  
Grok has plans to rebuild the installer without powershell eventually.  

Boot up Windows (VM or otherwise), and install GAMMA there following the standard installation instructions, <ins>***CONFIRM IT WORKS***</ins>, including that the proper number of mods are enabled and that the game launches to the main menu, and then copy the files over to Linux;
- Depending on how you choose to copy the files over, you may leave some behind in the process due to folder/file name lengths.  
- You can avoid that by compressing before transferring. This also saves you a lot of time transferring back to Linux if you have a decent CPU.
- A shared folder in your VM between your Linux host and Windows guest would be good for this, if your VM can do it, here's a guide for [QEMU/KVM](https://blog.sergeantbiggs.net/posts/file-sharing-with-qemu-and-virt-manager/).
- Consider using an external storage drive, a USB drive, or something like that. You could also upload to a cloud service.

<br>

<h4>Okay, you have the GAMMA files installed, copied over, and ready to go, now what?</h4>

<br>

You have two good options, running the game through Lutris with Wine, or through Steam with Proton.  
I recommend Lutris, using Wine 8.0+ since it now supports ReShade. 
<ins>If you are interested in going down the Steam/Proton road, then look at [this guide](https://github.com/maxastyler/S.T.A.L.K.E.R.-Gamma-Steam-Deck-Install-Guide/).</ins>

Quick rundown for Lutris:  
1. Disable Lutris Runtime  
2. Wineprefix DLLs:  
&nbsp;&nbsp;&nbsp;&nbsp;- cmd  
&nbsp;&nbsp;&nbsp;&nbsp;- d3dcompiler_47  
&nbsp;&nbsp;&nbsp;&nbsp;- d3dx10  
&nbsp;&nbsp;&nbsp;&nbsp;- d3d11_43  
&nbsp;&nbsp;&nbsp;&nbsp;- d3dx9  
&nbsp;&nbsp;&nbsp;&nbsp;- dx8vb  
&nbsp;&nbsp;&nbsp;&nbsp;- dxvk  
&nbsp;&nbsp;&nbsp;&nbsp;- quartz  
&nbsp;&nbsp;&nbsp;&nbsp;- vcrun2019  
3. Make sure DXVK and VKD3D are enabled, Esync and Fsync may cause issues, disable it if unsure.

With that, you should now atleast be able to launch Mod Organizer and configure further from there;

Since you installed GAMMA in Windows, your file paths will be messed up, this is why Mod Organizer is asking you where your game is, when you click browse it will open up the Wine file system, find your Anomaly folder and point Mod Organizer to it.

You should be looking at the main MO2 window now, if UI elements are missing (black boxes etc.), try changing your runner.  
If you did it right, you should have the proper number of mods, this number can be found in the GAMMA discord.  
If this number is 0, you didn't give it the correct path to your game, you can change it in the settings (Ctrl+S).  
If it's another number, you are going to have to do some troubleshooting.  
In settings(Ctrl+S), go to the Theme tab and choose 1809 Dark Mode, then go to the General tab and untick "Check for updates".   
All done with settings.

In the large drop down menu next to the Play button, click "<Edit...>"
Select Anomaly Launcher in the list, for the Binary path, you want to point it to <Anomaly path>\AnomalyLauncher.exe.
For the Start in path, point it at the Anomaly folder, you can copy the path you set from above and remove "AnomalyLauncher.exe" from it.

If you need to configure the other executables (if AnomalyLauncher doesn't work), they are contained within the bin folder at the root of the game.

<br>

At this point, you should be able to run the game through MO2, if AnomalyLauncher doesn't work try running DX# from the drop down instead. 
Some issues you may or may not encounter:

1.  The game window might not properly size to your screen (especially if you alt tab), or may appear as a small black window, if this is the case:  
&nbsp;&nbsp;&nbsp;&nbsp;- Edit the user.ltx file found in \<Anomaly path\>/appdata/  
&nbsp;&nbsp;&nbsp;&nbsp;- Change rs__screenmode (fullscreen|borderless|windowed), different options work for different set-ups.  
&nbsp;&nbsp;&nbsp;&nbsp;- Double check that vid_mode is set correctly according to your display, e.g. vid_mode 1920x1080  


2.  The FPS limiter present in the graphics settings may lead to choppiness and sharp screen tearing.  
&nbsp;&nbsp;&nbsp;&nbsp;- Consider using VSync without the FPS limiter instead.  
 
3. Stuttering when you move and look around, this is because you're using ReShade but aren't running the game with Wine 8.0+ or an equivalent fork, you can fix this by:
* [Removing Reshade.](https://reshade.me/forum/general-discussion/4398-howto-uninstall-reshade)
* Then deleting shaders_cache \<Anomaly path\>/appdata/.
* Then removing these mods:
  * 188- Enhanced Shaders - KennShade
  * 189- Beef's NVG - theRealBeef
  * 190- Screen Space Shaders - Ascii1457
  * 290- Atmospherics Shaders Weathers and Reshade - Hippobot


<h4>By now, you should have a fully playable (though likely imperfect) S.T.A.L.K.E.R. - G.A.M.M.A. experience on Linux.</h4>


<h3>Thanks to:</h3>
 
[All the Contributors](https://github.com/DravenusRex/stalker-gamma-linux-guide/graphs/contributors)  

no.#3094 (LafreSita) - Groundwork for the wineprefix.  

yeyande#9033 (yeyande) - Unintentionally helping me find the cause of the key repeat stutter.  

maxastyler and his [Steam Deck Guide](https://github.com/maxastyler/S.T.A.L.K.E.R.-Gamma-Steam-Deck-Install-Guide/)




