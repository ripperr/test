Mobile Mon application in Phonegap with JQuery Mobile
=====================================================
This guide explains how to run this phonegap application in Ubuntu/Debian, Mac os X and on the phonegap.com website.


#Building on phonegap.com#
##Notes
For phonegap to build for iOS, you have to create a certificate.
##Instructions
Download this project. Unzip. Remove the folders in the platforms folder. Finally, rezip the project. 

Go to [http://www.phonegap.com](http://www.phonegap.com) and register for a free account.

Upload the .zip and build.

#Building on Ubuntu/Debian
##Notes
In order to build this phonegap application manually in ubuntu, you have to install node.js, the android development kit and finally phonegap from node.js. It is not possible to build the application locally for iOS on Ubuntu/Debian.
##Prerequisites
###Installation node.js
####Download from node.js:
[node.js download page](http://nodejs.org/download/)
####Unpack and configure:
```bash
tar -xvf node-v0.10.26.tar.gz
./configure
```
####Install packages to compile node.js
```bash
sudo apt-get install gcc
sudo apt-get install make
sudo apt-get install build-essential
```
####Compile node.js
Navigate to the directory where you unpacked node.
After that, run the following commands:
```bash
sudo make
sudo make install
```
###Install Phonegap
```bash
sudo npm install -g phonegap
```
###Installation android development kit and eclipse
####Download from developer.android.com
[https://developer.android.com/sdk/installing/index.html](https://developer.android.com/sdk/installing/index.html)
####Unpack the android development kit
```bash
sudo unzip adt-bundle-linux-x86_64-20131030.zip
```
Remember the location of the unpacked adt-bundle.
####Add the adt-bundle location to your build-path
```bash
export PATH=${PATH}:[YOUR_UNPACK_LOCATION]/adt-bundle-linux-x86_64-20131030/sdk/platform-tools/:[YOUR_UNPACK_LOCATION]/adt-bundle-linux-x86_64-20131030/sdk/tools
```
##Running the app
Download and unpack the project.
Finally, run the following commands in the project folder:
```bash
phonegap run android
```
##Installing and removing plugins
Installing a plugin:

```bash
phonegap local plugin add [url of your plugin].git
```
Removing a plugin:

```bash
phonegap plugin remove [package name of your plugin]
```
##Folder structure

| Folders       | Content       			    |
| ------------- |:-----------------------------------------:| 
| /merges     	| Is used to merge/override the /www folder | 
| /platforms    | Is automatically populated with code if you compile for a specific platform(android,iOS)      |
| /plugins      | Contains added plugins     |
| /www	        | HTML, CSS and JavaScript code has to be placed here   | 

##Known issues
###Plugin issues
Sometimes, on a new build machine, you have to manually remove and reinstall all the phonegap plugins that are currently installed for the project.

Remove plugins/android.json file.

Remove platforms/android map.

After that, run the following commands:
```bash
phonegap plugin remove com.phonegap.plugins.PushPlugin
phonegap plugin remove org.apache.cordova.dialogs
phonegap plugin remove org.apache.cordova.vibration
phonegap plugin remove org.apache.cordova.device
phonegap plugin remove org.apache.cordova.network-information

phonegap local plugin add https://git-wip-us.apache.org/repos/asf/cordova-plugin-device.git

phonegap local plugin add https://git-wip-us.apache.org/repos/asf/cordova-plugin-vibration.git

phonegap local plugin add https://git-wip-us.apache.org/repos/asf/cordova-plugin-dialogs.git

phonegap local plugin add https://github.com/phonegap-build/PushPlugin.git

phonegap local plugin add https://git-wip-us.apache.org/repos/asf/cordova-plugin-network-information.git
```
#Pushnotifications
In the following paragraphs you can find instructions on how to configure to Google Cloud Message for Android and 
Apple Push Notifications for iOS.
##Google Cloud Message(GCM)
In this section you can find detailed instructions on how to configure Google Cloud Messaging(GCM) for Phonegap from scratch. Google Cloud Message allows you to send pushnotifications to Android devices.
###Creating a Google API project

Goto the [Google Api Console](https://code.google.com/apis/console)

Click on 'Create Project'

![screenshot of create project](images-readme/image 1.png)

Click on 'Overview' and note down the project number

![screenshot of create project](images-readme/image 2.png)

###Enabling Google Cloud messaging for Android
Enable Google Cloud Messaging for Android in ‘APIs & auth>APIs’ and click on ‘Google Cloud Messaging for Android’
![screenshot of enabling Google Cloud Messaging for Android](images-readme/image 3.png)
Accept
![screenshot of accept dialog](images-readme/image 4.png)
###Creating a new API Key
In ‘APIs & auth > Credentials’ section click on ‘Create new Key’
![screenshot of creation of a new key](images-readme/image 5.png)

Click on 'Server Key'

![screenshot of accept dialog](images-readme/image 6.png)

Click on 'Create'

![screenshot of accept dialog](images-readme/image 7.png)

Note down the API key

![screenshot of accept dialog](images-readme/image 8.png)
###Implementing the API key in Phonegap
Replace senderID in ‘phonegap/www/js/push/pushImplementation.js’ with your project number

![screenshot of accept dialog](images-readme/image 9.png)

##Apple Push Notifications(APN)
In this section you can find detailed instructions on how to configure Apple Push Notifications(APN) for Phonegap from scratch. Apple Push Notifications allows you to send pushnotifications to iOS devices.
###Creating iOS Distribution certificate
Goto [iOS Dev Center](https://developer.apple.com)

Click on 'iOS Dev Center'

![screenshot of accept dialog](images-readme/image 10.png)

Click on 'Certificates, Identifiers & Profiles'

![screenshot of accept dialog](images-readme/image 11.png)

Click on ‘Certificates’

![screenshot of accept dialog](images-readme/image 12.png)

Click on ‘Certificates’ (left navigation panel) and click on the +-button on the right

![screenshot of accept dialog](images-readme/image 13.png)

Check ‘In-House and Ad Hoc’ and click on continue

![screenshot of accept dialog](images-readme/image 14.png)

Create a certificate signing request on your mac

![screenshot of accept dialog](images-readme/image 15.png)

Fill in an Email Address en check ’Saved to disk’

![screenshot of accept dialog](images-readme/image 16.png)

Click ‘Continue’

![screenshot of accept dialog](images-readme/image 17.png)

Upload the .certSigningRequest you’ve created in step 6 and click ‘Generate’

![screenshot of accept dialog](images-readme/image 18.png)

Note: This is how your keychain access will look before implementing the iOS Distribution certificate

![screenshot of accept dialog](images-readme/image 19.png)

Download and install the distribution certificate

![screenshot of accept dialog](images-readme/image 20.png)

Note: This is how your keychain access will look after implementing the iOS Distribution certificate

![screenshot of accept dialog](images-readme/image 21.png)

###Creating an application id

On the developer portal, click on ‘Identifiers > App IDs’ and click then on the +-button on the right

![screenshot of accept dialog](images-readme/image 22.png)

Fill in your application name and select an ‘Explicit App ID’

Fill in a bundle ID and remember it!!!! You will need it when you configure your app in xcode. We will use com.document.app here.

![screenshot of accept dialog](images-readme/image 23.png)

Enable all the services your app needs and click on ‘Continue’

![screenshot of accept dialog](images-readme/image 24.png)

Confirm your app and click on submit

![screenshot of accept dialog](images-readme/image 25.png)

Click on ‘Done’

![screenshot of accept dialog](images-readme/image 26.png)
###Creating SSL-certificates for your push server

Click on ‘Edit’ in the iOS app id summary

![screenshot of accept dialog](images-readme/image 27.png)

Click on ‘Create Certificate’. The rest of the steps are completely the same as step 6 - step 10 of Creating iOS distribution certificate.

![screenshot of accept dialog](images-readme/image 28.png)

In the end, you will end up with something like this:
If you want to send push notifications on your server, you have to download the push notification certificates and configure your webserver to use these certificates.

![screenshot of accept dialog](images-readme/image 29.png)

###Creating provisioning profile(Distribution)

On the developer portal, click on ‘Provisioning profiles > All’ and click then on the +-button on the right

![screenshot of accept dialog](images-readme/image 30.png)

Select ‘In-house’

![screenshot of accept dialog](images-readme/image 31.png)

Select your ‘app id’ from the drop down list

![screenshot of accept dialog](images-readme/image 32.png)

Select the (right!!) certificate you’ve created earlier

![screenshot of accept dialog](images-readme/image 33.png)

Fill in a provisioning profile name en click on generate

![screenshot of accept dialog](images-readme/image 34.png)

Click on download and install the provisioning profile

![screenshot of accept dialog](images-readme/image 35.png)

###Configuring your application in Xcode

Open your project in xcode and click on HelloWorld(one time, two times opens a new screen). If xcode was already open, close it and reopen as it will sometimes lead to problems.

Fill in your ‘Bundle identifier’ you’ve created in [Creating an application id](#creating-an-application-id) and select your ‘Team’(Developer id)

![screenshot of accept dialog](images-readme/image 36.png)

Go to tab ‘Build settings’ and fill in your ‘code signing Identity’ and the ‘provisioning profile’

![screenshot of accept dialog](images-readme/image 37.png)

#Exporting your application
##Android
!You can only export the application after you've run:
``` bash
phonegap run android
```
After the command, the folder platforms/android will be created.

Import your project in eclipse(platforms/android)

![screenshot of accept dialog](images-readme/image 49.png)

![screenshot of accept dialog](images-readme/image 50.png)

![screenshot of accept dialog](images-readme/image 51.png)

Press ‘Project > Clean…’

![screenshot of accept dialog](images-readme/image 43.png)

Right click on the project and click on ‘Android Tools > Export Signed Application Package’

![screenshot of accept dialog](images-readme/image 44.png)

Select your project

![screenshot of accept dialog](images-readme/image 45.png)

Select ‘Create new keystore’ and create a password

![screenshot of accept dialog](images-readme/image 46.png)

Fill in the required fields

![screenshot of accept dialog](images-readme/image 47.png)

Click finish. After that your application is ready to deploy.

![screenshot of accept dialog](images-readme/image 48.png)

Make a html file like this and replace the text in red with your url. Place this html file on your web server.
``` html
<html>
<head></head>
<body>
<p>
<a href="https://dl.dropboxusercontent.com/s/ik6fkuo7jscde8i/HelloWorld.apk">Install for Android</a>
</p>
</body>
</html>
```

Navigate to your web server with your mobile device. You should now be able to install your application on your iOS device by clicking on ‘Install for Android’.

##iOS(in-house distribution)

!You can only export the application after you've run:
``` bash
phonegap run ios
```
After the command, the folder platforms/ios will be created.

Open your project in Xcode(platforms/ios/your-app-name.xcodeproj)

Click on Product > Archive

![screenshot of accept dialog](images-readme/image 38.png)

The following screen will come up were you will have to click on distribute(the identifier should normally be com.document.app):

![screenshot of accept dialog](images-readme/image 39.png)

Click on ‘Save for Enterprise or Ad Hoc Deployment’

![screenshot of accept dialog](images-readme/image 40.png)

Select the ‘Provisioning Profile’ (=> documentation profile distribution)

![screenshot of accept dialog](images-readme/image 41.png)

Fill in the application url. For example https://yourserver.com/HelloWorld.ipa

![screenshot of accept dialog](images-readme/image 42.png)


Go to the folder where you’ve exported the application.

You should now see HelloWorld.ipa and HelloWorld.plist
These 2 files need to be uploaded to a web server with a valid ssl certificate.


Make a html file like this and replace the text in red with your url. Place this html file on your web server.
```html
<html>
<head></head>
<body>
<p>
<a href="itms-services://?action=download-manifest&url=https://dl.dropboxusercontent.com/s/agkpjg4j252qt3t/HelloWorld.plist">Install for IOS</a>
</p>
</body>
</html>
```

Navigate to your web server with your mobile device. You should now be able to install your application on your iOS device by clicking on ‘Install for IOS’.


