# Server Setup
## HLDS
Currently there is a build of ReHLDS packaged with the install for MS Rebirth, though this may change in the future, but if you're running a dedicated server from the install you play the game from, you're good to go, skip directly to port forwarding. If you want to separate these on your desktop, or set a server up on a dedicated host that you're not going to install Steam on, you'll need to use SteamCMD to install MS Rebirth.

## SteamCMD
You can find instructions for installing SteamCMD on various operating systems on the [Valve dev wiki page.](https://developer.valvesoftware.com/wiki/SteamCMD)  

Once you have SteamCMD setup, you'll need to follow these steps:  

- force_install_dir [directory] - Do this before logging in to tell SteamCMD where you want to install MSR. Ordinarily you wouldn't have to login with your Steam account to download files, but MSR being in beta testing requires a full login for now.  

As ReHDLS is currently packaged in, we can skip installing HLDS and go directly to the game files. Run the command:  
- app_update 1961680 - This is the Steam AppID for MS Rebirth. Should you want to install base HLDS for a different mod, instructions are on the SteamCMD page, but it's not recommended to run base HLDS at this time for Rebirth.  

Run this command if you want to verify the install and overwrite any wonky files if it happens:  
- app_update 1961680 validate  

Since you don't have Steam to auto-update for you, you'll need to log in to SteamCMD and do the above whenever a patch for MSR is deployed. I suggest creating a batch script to save you a few seconds. If you're unfamiliar with the process, simply create a new text file in your SteamCMD directory, drop in this line:  
- steamcmd +force_install_dir [Your MSR install directory] +login [Username] [Password] +app_update 1961680 +quit  

Then change the .txt file extension to .bat, and run it.  
I'm lazy, so I create a shortcut to this file in my MSR install folder.  

## Port Forwarding
You'll need to forward these ports:  
- 27015 UDP (game transmission, pings)  
- 27015 TCP (RCON)  
- 27020 UDP (HLTV transmission)  
Source: [https://developer.valvesoftware.com/wiki/Half-Life_Dedicated_Server](https://developer.valvesoftware.com/wiki/Half-Life_Dedicated_Server)  

The default server host port for pretty much all Valve games is 27015, but if you intend to run multiple servers, you may want to open a range of ports such as 27015-270XX, to give yourself some room.  

If you've never port forwarded before, you'll want to figure out the brand and model name of your router, then track it down on [PortForward.com](https://portforward.com/) to find a guide tailored to your specific setup.  

## Server.cfg
The server.cfg file can be found in msrebirth/msr/server.cfg, it should be mostly good to go by default, but you will at least need to scroll to the bottom to enable central server connection, and put in the address you were given when you were whitelisted as a host.  

Commands you may want to look at:  
- hostname - You'll want to remove this if running multiple servers, as you'll have to define the hostname via launch parameters.  
- rcon_password - This will allow you to login to the server and send admin commands in-game, worth setting just in case.  
- msvote_map_enable - Turn this off if you want an "immersive experience."  
- ms_admin_contact - I dunno that anybody even knows this exists, but this will tell them who to whine to by typing "contact" in console  
- ms_chatlog - **Turn this on.** It doesn't work at the moment, but it will.  
- ms_timelimit - This will reset the server to Edana when it's empty for a period of time, though the default should be fine. (There's two of these in the default config, remove one of them. Dunno why.)  
- ms_reset_if_empty - This will reboot the server whenever it resets to Edana via the timelimit. Stuff gets wonky when servers stay up too long, so this helps.  

#### Commands so the server doesn't ban everyone constantly
ReHLDS has a built-in command spam filter that will auto-ban anybody sending too many commands to the server. Trouble is, Master Sword sends a lot of commands from the client to the server, so it is guaranteed to ban someone pretty quickly. Paste these at the bottom of your msr/server.cfg to prevent this:

> sv_rehlds_movecmdrate_max_avg 99999  
> sv_rehlds_movecmdrate_max_burst 99999  
> sv_rehlds_stringcmdrate_max_avg 99999  
> sv_rehlds_stringcmdrate_max_burst 9999  
> sv_rehlds_stringcmdrate_burst_punish -1  
> sv_rehlds_stringcmdrate_avg_punish -1  
> sv_rehlds_movecmdrate_burst_punish -1  
> sv_rehlds_movecmdrate_avg_punish -1  


## Auto-restarter script
You can launch ReHLDS using the executable, but launching via command line will allow you to set additional parameters. Greatguys has made a very useful [auto-restarter batch file](https://github.com/MSRevive/website/files/10714271/Restarter.zip) which includes the launch command along with a few default parameters you will want for MSR. Just drop this script into the base msrebirth folder, where the hlds.exe is located. It will launch and bind to ReHLDS, rebooting it whenever it disappears/crashes, and it will crash.  

Depending on your setup or how many servers you want to run, you may need a few additional parameters:  
- +hostname [Name] - Use this if you're running more than one server, and remove it from your server.cfg, else all servers will use that instead.  
- +ip [LAN IP] - Use this if you need to force HLDS to bind to a specific IP on your network.  
- -port - The default port is 27015, but if you want to run multiple servers or you just don't like 27015 for some reason, you'll need to specify with this.  

To run multiple servers, you can simply create a copy of the restarter script, make the hostname changes in server.cfg and this script, and specify your port, and it will run cleanly off of a single install of MSR. By default, MSR will generate a crashed.cfg file in its directory whenever the server changes maps, which is executed as a launch parameter in the restarter script to boot the server back up on that map in case of a crash. Next patch will bring the ability to specify the name of the crashed.cfg for running multiple servers, and I will add those commands to this list when they are released.  

Note: if running multiple servers, don't launch all the batch files at once, as one restarter will bind to all of the servers and it will not reboot until they all crash.
