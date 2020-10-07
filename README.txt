Step 1: Downloading and Installing the Blynk App on the Smartphone.
1. Open Play store and download and install the Blynk App.
2. Once the app is installed either login to it using Facebook or create a new account on Blynk and login using that. In this case I have logged in using Facebook.
3. After logging in, create a new project by clicking ‘New Project’
4. Give the project a name of your liking. Select the hardware device as NodeMCU and select the connection type as WIFI, and hit create.
5. At this point Blynk will send an Auth token to your email id. We will use this ‘Auth token’ later in the tutorial to link our app with the NodeMCU.
6. Now since I’m using a four-channel relay, I’ll add 4 buttons on the blank project. To add a new button just click anywhere on the blank area and select button from the side menu that pops up. You can place the button anywhere on the screen.
7. Click on the Button and give it a name. I’ll name it ‘Relay 1’ as I’ll use it to control the first relay. Below the name, in the textbox select the pin as digital pin D3.
8. Repeat the process 3 more times and add three more buttons. Naming them Relay 2, Relay 3 and Relay 4 And choosing their Digital Pins as D4, D5 and D6 respectively.
9. Now, the Blynk app is all set.

Step 2: Downloading Arduino IDE and Configuring Blynk Libraries.
1. Now let’s install the Arduino IDE. Go to this link and download the IDE for your preferred operating system.
2. Download the latest Blynk libraries from this link. These libraries will help us connect the Blynk app with the NodeMCU.
3. Extract the download zip file in a folder.
4. Open up Arduino IDE, go to: File > Preferences and under the Settings tab, copy the sketchbook location path.
5. Now open the file explorer and go to the copied path location. This is the path where all the Blynk libraries are installed. So, we’ll have to copy all the newly downloaded Blynk libraries into this folder.
6. Copy the files/folders from the Libraries folder of the downloaded Blynk directory, and paste it to the Libraries folder of your Arduino IDE’s directory (The path that we copied in step 5).
7. Similarly, copy the files/folder from the Tools folder of the downloaded Blynk directory, and paste it to the Tools folder of your Arduino IDE’s directory.

Step 3: Uploading the code to NodeMCU.
1. Connect the NodeMCU to your PC using a USB cable.
2. Now, we’ll set up the Arduino IDE by changing some settings. So, open up the Arduino IDE.
3. Go to Tools > Port and make sure an appropriate port is selected. In my case it’s COM 4. This is the USB port in which the NodeMCU is connected.
4. Now Go to Tools > Board and select ‘NodeMCU 1.0 (ESP-12E Module)’ as the board. And that’s all the settings we need to change. So now let’s begin writing some code.
5. Go to Files > Examples > Blynk > Boards_WIFI > ESP8266_Standalone. A new file with some prewritten code will open.
6. Now, in this file we only need to change 3 lines of code.
	Change the line where it says ‘char auth[] = “YourAuthToken”’ and replace the ‘YourAuthToken’ part with your Blynk’s auth token that you received in your email.Change the line where it says ‘char ssid[] = “YourNetworkName”’ and replace the ‘YourNetworkName’ part with the name of your WIFI network that you want your NodeMCU to connect to. In my case the name of my WIFI network is ‘The Network’Change the line where it says ‘char pass[] = “YourPassword”’ and replace the ‘YourPassword’ part with the password of your WIFI network. In my case password of my WIFI network is ‘The Network’ is ‘abcd1234’.
7. That’s really all the code that we need to write! We are now ready to upload this code to the NodeMCU. So directly hit upload button at the top (besides the button that has a checkmark), and wait for it to process.
8. The code will be uploaded to the NodeMCU and the next time you power it on, it will automatically connect to the specified WIFI network.

Step 4: Hardware Assembly.
1. We’ll have to connect the NodeMCU with the Relay board, you can choose to do it with a bread board or without. But I prefer doing it using a Breadboard.
2. Connect the D3 pin of NodeMCU with Pin 1 of Relay. Similarly connect D4 pin of NodeMCU with Relay pin 2, D5 with Relay 3 and D6 with Relay 4.
3. Connect Ground Pin of Relay with Ground Pin of NodeMCU.
4. Now to power up the NodeMCU you can use a normal phone charger, just make sure its voltage is not too high. And to power up the Relay board, you can use a battery or a separate breadboard power supplier.
5. As we are using a four-channel relay you can connect at most 4 electronic appliances to the Relay and control them over the internet.
6. Now if you want to connect your household appliances like Fan, Lights etc. which are connected to the main power of your house, I would recommend you take the help of a professional electrician and ask him/her to connect those appliances to the relay. Because working with the mains is no joke and if not done properly, can cause a serious damage.

Step 5: Connecting Google Assistant (using IFTTT) to make the NodeMCU work with voice commands.
1. Enough said, lets configure IFTTT. Go to IFTTT’s website and sign up to it using your Google Account.
2. After Signing in click on My Applets from the header and select New Applet.
3. Click on ‘this’.
4. Search for Google Assistant and select it. And then Click on Connect.
5. At this point IFTTT will ask you permission to use your google account to add voice commands to it. Which you simply allow by clicking on ‘Allow’.
6. Select the card that says “Say a simple phrase”.
7. Next, for the first textbox type the phrase that you want to say to Google Assistant. It can be anything such as “Turn on the T.V”, “Turn on the fan” or anything you like.
8. For the next two text boxes, you write some other ways to say the first command. For example, if in the first textbox you wrote “Turn on the T.V”, then in the second and third textboxes you can write something like “Turn the T.V On” or “Please Turn on the T.V” or “Turn the Idiot Box On”.
9. In the fourth textbox type the reply that Google Assistant should respond with. For example, “Okay, Turning on the T.V”.
10. Finally, click on ‘Create Trigger’.
11. Now, click on that
12. Now, in the URL field type this URL:
http://188.166.206.43/ YourAuthTokenHere / update / DigitalPinToBeUpdateHere
13. Next, Select the ‘Method’ field as PUT
14. Select ‘Content type’ as Application/JSON.
15. For the ‘Body’ type this:   [“0”]
16. Now click on ‘Create Action’ and then Finish.