
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

As of May 1, 2023, the GAMMA installer uses powershell;
As far as I know, <ins>there is not a way to run the installer on Linux.</ins>  
A few people have tried it with powershell for Linux, it has not worked so far.  
Grok has plans to rebuild the installer without powershell eventually.  

However, Mord3rca built a [Linux compatible python-based launcher here.](https://github.com/Mord3rca/gamma-launcher)  
You should go and get that installed and ready to go before you continue.  
If you don't want to go that route, or difficulties crop up, your other option is using Grok's launcher on a Windows VM/dual boot, check this [old branch.](https://github.com/DravenusRex/stalker-gamma-linux-guide/tree/vm-method)  
I very highly recommend using Mord3rca's launcher, it already works wonderfully, and he's continuing to improve it.  
Everything will be setup as close as the official installer as possible.  

<h4>Okay, you have Mord3rca's launcher set up and ready to go, now what?</h4>

Follow the installation instructions as normal in the GAMMA discord server, all the way up until it says to use Grok's launcher.
When it tells you to run Anomaly for the set-up, use your preferred method, I recommend Lutris with Wine 8.0+ since it now supports ReShade.  

**Quick rundown for Lutris:**
1. Install the newest stable Wine runner that your system can run. <sup><sub>**(Recommend using your system package manager, the Lutris built in version manager, or ProtonUp-Qt.)**</sub></sup>
2. Disable Lutris Runtime if your system ones are better for games/if there are issues.
3. Wineprefix DLLs to install:  
&nbsp;- cmd  
&nbsp;- d3dcompiler_47  
&nbsp;- d3dx10  
&nbsp;- d3dx11_43  
&nbsp;- d3dx9  
&nbsp;- dx8vb  
&nbsp;- dxvk <sub><sup>**(Major performance boost, but you need a DXVK-marked driver, if you are unsure, install this seperately from the other DLLs so they don't fail.)**</sup></sub><br>
&nbsp;- quartz  
&nbsp;- vcrun2019  
4. Make sure DXVK and VKD3D are enabled, Esync *may* cause issues, disable it if unsure, Fsync may or may not work on some Wine versions.
  
  
After doing this, the key things you should have at this point are:  
- A GAMMA directory which contains the extracted contents of GAMMA RC3.7z and downloads.7z
- An Anomaly directory containing the extracted contents of Anomaly-1.5.1.7z and Anomaly-1.5.1-to-1.5.2-Update.7z, which you ran.

Once you've done this, you may wish to check the integrity of your GAMMA folder:  
`gamma-launcher check-md5 --gamma <GAMMA path>`  
Then you can run the installer with:  
`gamma-launcher full-install --anomaly <anomaly path> --gamma <GAMMA path>`

After that, add Mod Organizer (\<GAMMA path\>/ModOrganizer.exe) to Lutris, you can use the same wineprefix and settings as before.  
Launch Mod Organizer. It might provide an error saying "Cannot open instance 'Portable'..."  
Click OK, and then Browse and select your Anomaly folder; an easy way to find it is clicking "My Computer" and going to the "Z" drive.  
You will notice it represents your native Linux filesystem.  
After you select your Anomaly folder, another error may appear saying "The selected profile 'Default' does not exist...", you can ignore this.

If you did it right, you should have the proper number of mods, this number can be found in the GAMMA discord.  
If this number is 0, you didn't give it the correct path to your game, you can change it in the settings (Ctrl+S).  
If it's another number, you are going to have to do some troubleshooting.  
In settings(Ctrl+S), go to the General tab and untick "Check for updates".   
*Optional:* Go to the Theme tab and choose 1809 Dark Mode.  
All done with settings.  

<br>

At this point, you should be able to run the game through MO2, if AnomalyLauncher doesn't work try running DX# from the drop down instead. 
Some issues you may or may not encounter:

**1.  The game window might not properly size to your screen (especially if you alt tab), or may appear as a small black window, if this is the case:**
  * Edit the user.ltx file found in \<Anomaly path\>/appdata/  
  * Change rs__screenmode (fullscreen|borderless|windowed), different options work for different set-ups.  
  * Double check that vid_mode is set correctly according to your display, e.g. vid_mode 1920x1080  

**2.  The FPS limiter present in the graphics settings may lead to choppiness and sharp screen tearing.**
  * Mangohud is a good choice for an FPS limiter, for example: Setting `MANGOHUD_CONFIG=no_display,fps_limit=60 mangohud` as the launch options for the game executable you'd like to use (such as DX10.exe) in MO2 would limit it to 60 FPS. It doesn't do anything if set for the Anomaly launcher rather than the game .exes themselves.<br>
  * Consider using VSync without the FPS limiter enabled instead.  
  
**3. Stuttering when you move and look around, this is because you're using ReShade but aren't running the game with Wine 8.0+ or an equivalent fork, you can fix this by:**

* Running the game with Wine 8.0+ or an equivalent fork.

	***If that doesn't work, or if you insist on using old versions:***

* Removing Reshade: ```gamma-launcher remove-reshade --anomaly <Anomaly path>```
* Then purging the shader cache ```gamma-launcher purge-shader-cache --anomaly <Anomaly path>```
* Then removing these mods:
  * 188- Enhanced Shaders - KennShade
  * 189- Beef's NVG - theRealBeef
  * 190- Screen Space Shaders - Ascii1457
  * 290- Atmospherics Shaders Weathers and Reshade - Hippobot
  <br>
<h3>By now, you should have a playable S.T.A.L.K.E.R. - G.A.M.M.A. on Linux.</h3>
  <br>
<h3>Thanks to:</h3>
 
[All the Contributors](https://github.com/DravenusRex/stalker-gamma-linux-guide/graphs/contributors)  

no.#3094 (LafreSita) - Groundwork for the wineprefix.  

yeyande#9033 (yeyande) - Helping me solve key repeat stutter.  
 
<h3>Special thanks:</h3>
  
[maxastyler](https://github.com/maxastyler) for his [Steam Deck Guide.](https://github.com/maxastyler/S.T.A.L.K.E.R.-Gamma-Steam-Deck-Install-Guide/)  
 
[Mord3rca](https://github.com/Mord3rca) for his [launcher.](https://github.com/Mord3rca/gamma-launcher)




