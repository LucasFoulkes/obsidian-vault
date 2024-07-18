# Remote SSH
## Goal
make a target computer accessible over ssh with a static domain. for free , no access to the router. ideally without installing anything
## Log
1. Serveo seems to work when testing locally. `ssh -R foxeyes:22:localhost:22 serveo.net`.  you connect with `ssh -J serveo.net <user>@foxwatch`
2. does not work on remote for some insane reason ngrok does work but not Serveo
3. does work sometimes on remote but sometimes it stops working, as it no longer runs not that it suddenly stops working while working although that also happens. 
	1. test cmd admin does not work for some again insane reason
	2. powershell both admin and not. also does not work. 
	3. is there a program already using port 22. nothing connected, still doesnt work 
	could becouse serveo itself is blocking the stuff for some reason different still dont work for some reason tho.
4.  new strategy. target tries to connect (pings or something lighter) to a server (known with its own domain). once it alive (target) does a localtunnel and sends new address to server. client sends a command to server server comes alive (becouse i think this is cheaper using cloud run instead of a instance) once server has target new domain it tells this to client . now client connects directly to target forgeting and not dealing with server. features. if client losses to target . first asks server whatsup . if server is not getting anything tells client target dead or something. in the middle time target if lost internet it does the local tunnel again . once internet is back . if reseted computer does local tunnel again . if for any reason ssh localtunnel dead it kills clean and tries to localtunnel again. if server has new target id it tells this to client and now client program connects to this new one .