f. I have a Quest 3
q. software for VR development compatible with the quest
a. 
- Unity
- Unreal 
- Godot 
d. unity
qfl. tools or libraries? seems i can use a specific like tools set or something. i mean are there environments that if using them can use other tools? are there mutually exclusive
q. how to make game for quest 3 using unity
o. https://developer.oculus.com/quest/ it talks about something called native 
q. what is OpenXR . https://developer.oculus.com/documentation/native/
o. seems needlessly complex
d. lets start with unity even tho unreal might have better graphics?
o. https://developer.oculus.com/documentation/unity/unity-gs-overview/
i. quest3 and meta quest pro characteristics. this info should be maybe a link to a different file. depends on how much is used. 

|  | Meta Quest 3 | Meta Quest Pro |
| ---- | ---- | ---- |
| **Maximum Screen Refresh Rate** | 120 Hz | 90 Hz |
| **Display** | LCD | LCD with local dimming |
| **Display Resolution, PPD (Per Eye)** | 2064x2208, 25 PPD | 1800x1920, 22 PPD |
| **On-board Memory** | 8 GB | 12 GB |
| **Chipset** | Snapdragon XR2 Gen 2 | Snapdragon XR2+ Gen 1 |
| **Tracking** | Head tracking, Hand tracking | Head tracking, Hand tracking, Face tracking, Eye tracking |
| **Mixed Reality** | Color stereoscopic 4 MP (18 PPD) passthrough with depth sensor | Color stereoscopic 1 MP (8 PPD) passthrough |
| **Field of View** | 110° horizontal, 96° vertical | 106° horizontal, 90° vertical |
| **Audio** | 2 speakers, 1x 3.5mm jack | 4 speakers, 2x 3.5mm jacks |
| **IPD Adjustments** | Continuous with slider | Continuous with slider |
| **Wi-Fi** | Wi-Fi 6E certified | Wi-Fi 6E capable |
| **Bluetooth®** | Bluetooth 5.2 | Bluetooth 5.2 |
| **Battery Life** | ~2 hours | ~2.5 hours |

a. setup https://developer.oculus.com/documentation/unity/unity-env-device-setup/
the links leads to instructions nothing complex
e. this allows to ADB to headset https://developer.oculus.com/downloads/package/oculus-adb-drivers/ this explains how to use it. https://developer.oculus.com/documentation/unity/unity-env-device-setup/#enable-adb
1. this helps a better workflow . https://developer.oculus.com/documentation/unity/unity-quickstart-mqdh/
- Use either a cable or WIFI connection between your headset and the computer
- Disable the proximity sensor and Boundary (Guardian) for an uninterrupted testing workflow
- View the device logs to help with debugging
- Capture screenshots and record videos of what you see in the headset (see [Record a Video](https://developer.oculus.com/documentation/unity/ts-odh-media/#record-a-video) for more information.)
- Deploy apps directly to your headset from your computer
- Upload apps to the [developer dashboard](https://developer.oculus.com/manage/) for store distribution
- Share your VR experience by casting the headset display to the computer
- Download the latest Meta Quest tools and SDKs you need to build apps
2.  aparently 3d Core?
qfl. unity has diferent options like profiles? what are they called. how are they diferent . test?
	e. this is to be able to build without having it connected i think. https://developer.oculus.com/documentation/unity/unity-link

1/29/2024

p. testing is very slow. building and running takes a while
o. airlink , or like cable. cable needs to be longer so money. airlink . my wifi is to slow. 
q. how does airlink and cable work when using unity. is the program run in the computer and just shown on the headset?
a. that kinda seems the only why anything would be posible . it needs to run somewhere

1/31/2024
**using airlink**
3d urp > change to android > edit > project settings > install xr pluggin manaager, im using open xr [https://www.youtube.com/watch?v=7mAAkB1WGpk]

2/2/2024
a. seems to fix a cable with unity the trick was having open oculus app and fix the pc issues on  the fix tool in unity
qfl. there are several sdk to do vr in  unity. wich ones are the best ones? also i need to use the depth api so need to use one that makes use of it? are they mixable somehow? 
p. Cozy > Editor Version 2022.3.18f1 > 3D URP 

a. Meta XR All-in-One SDK
b. OpenXR
c. UnityXR
d. SteamVR

5/2/2024
Desiciont for sdk
1. Meta 
2. UnityXR and OpenXR if it is diferent from UnityXR
I want to use the depth and passthrough so need to know if Unity can do this becouse i know Meta can. also the other thing is i want to use grab move or world locomotion wathever is called . to resize and move around like in TownScapper. 

**1** Resize World and move by pinching or grabbing. 
1. we will try meta sdk until something breaks or proves unusable
	1. meta sdk does not seem to work with urp. lets try normal 3d and see if there is a meaningfull diference in quality ( this seems like something to try latter)
	2. try the world moving in meta using like code. 
		1. rezize the entire world check if breaks physics.
			1. this might need something to be moving to test ( maybe **2** should go first)
		2. resize character (wich seem obvious )
**2** Robot Simulation light seeking 