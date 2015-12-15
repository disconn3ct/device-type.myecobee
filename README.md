# device-type.myecobee           Ecobee-SmartThings integration

My Ecobee Device:  Custom ecobee device to enable more smart thermostat's capabilities within SmartThings 

Based on work by Yves Racine

Contributing Authors: Disconn3ct

/*********************************************************************************************

 This is a fork of the original code, before the developer put it behind a pay-wall. This fork is pushed back 
 to before the project was changed. 
 
 So far, the bulk of the repository is unchanged. **WARNING**: The code cannot be used commercially,
 as required by the original author's license. (Kinda.)
 
 (As to why the fork, I literally just bought an ecobee last week after seeing the support. I haven't
 even had enough time using it to consider contributing. Had it been closed source already,
 I would not have changed thermostats to begin with. Additionally, the working rewritten version
 does not exist, so the original author is asking for users to pay for a broken version and hope the
 fixes appear someday.)

Note the [GitHub ToS](https://help.github.com/articles/github-terms-of-service/#f-copyright-and-content-ownership) explicitly permits this fork in paragraph F1.

/*********************************************************************************************

Setup time: about 5 minutes

=====================
INSTALLATION STEPS
=====================
**NOTE: These directions need testing.**

For ease of and update, you can use the SmartThings github integration.

(This guide will assume you are not doing any development and do not need to create your own
copy of the code.)

You will need a github account, but there is no need to do anything with it beyond signing in.

Once you have an account, follow steps 1 and 2 of the [SmartThings GitHub](http://docs.smartthings.com/en/latest/tools-and-ide/github-integration.html#setup) guide.

After the accounts are tied together, you can go back to the SmartThings "My Device Types" page and pick "Settings".
That will give you the option to add a new repository. In this case, the new repository should look like this:

* **Owner**: disconn3ct
* **Name**: device-type.myecobee
* **Branch**: Master

Once you have added the repository, you can click "Update from Repo" and select
the "device-type.myecobee (master)" repository. This will show the device under
"New (only in GitHub)" as "devicetypes/yracine/myecobee-devicetype.src/myecobee-devicetype.groovy".
Select the checkbox and (at the bottom) the "Publish" checkbox, then select "Execute Update".

**Warning:** If the green box says "Updated 0 devices and created 0 new devices (1 skipped due to errors)"
the update did not take. (I'm still working on a fix that does not involve
removing the associated devices and apps and recreating them, but that is
the "SmartThings Way" so there may be no easy option.)

**Create the SmartApp**

Go to https://graph.api.smartthings.com/ide/apps

Select "Update from Repo" and pick the "device-type.myecobee (master)" repository again.

This time you should have a lot of entries in "New (only in GitHub)". You can add as few or many as
you need, but at a minimum you need "smartapps/yracine/myecobeeinit.src/myecobeeinit".

Again, select "Publish" and "Execute Update".

Make sure that enable OAuth in Smartapp is active by selecting the "Properties"
icon for the "MyEcobeeInit" application.

At the bottom is the OAuth fold. Expand that by selecting it and enable it.

Then select "Update".

=====================
Update Applications
=====================

To update the apps and incorporate any changes from the repository, you will
need to sync again ("Update from Repo" as above). Any applications with the
update icon (magnifying glass) can be updated.

Select the icon, then it will show local and remote versions with changes 
highlighted.

You can review the changes, or simply click "Overwrite local version" and "Save"
to include them automatically.

This same process can be used to update the device type.

=====================
Configure the App
=====================

From your phone or tablet, within the smartThings app and on the main screen, click on the Smartapps link in the upper
section of the Home or Marketspace page, and then select My Apps at the end of the list.

/*********************************************************************************************

<b>4) Connect Smartthings to the Ecobee portal</b>

/*********************************************************************************************

You should already have an ecobee username and password, if not go to https://www.ecobee.com/home/ecobeeLogin.jsp

Go through the authentication process using My ecobee Init.

If needed, watch "how to setup ecobee" video (but use My ecobee Init instead of the Smarttings labs script) as the authentication process is similar.

http://blog.smartthings.com/news/smartthings-updates/new-additions-to-smartthings-labs

After being connected, click 'Next' and select your ecobee thermostat(s) (SMART, SMART-SI, ecobee3, EMS) 
that you want to control from Smartthings and, then press 'Next' for the 'Other Settings &Notification' page, 
and then 'Done' when finished.

If you get a blank screen after pressing 'Next or you get the following error: " Error - bad state. Unable to complete page configuration", you'd need to enable oAuth as specified in step 2f) above.


/*********************************************************************************************

<b>5) Your device(s) should now be ready to process your commands</b>

/*********************************************************************************************

You should see your device under

https://graph.api.smartthings.com/device/list

/*********************************************************************************************

<b>6) To populate the UI fields for your newly created device(s)</b>
/*********************************************************************************************

You may have to hit the My Ecobee device 'refresh' button several times as the smartThings app is not always responsive. 
You may want to stop and restart your smartthings app if needed.


/*********************************************************************************************

<b>7) Update device's preferences (optional, input parameters)</b>

/*********************************************************************************************

Go to https://graph.api.smartthings.com/device/list

Click on the My ecobee device that you just created

Click on Preferences (edit)

You only need to edit the following parameters


    (a) <trace> when needed, set to true to get more tracing (no spaces)
    (b) <holdType> set to nextTransition or indefinite (by default, no spaces) 
    see http://www.ecobee.com/home/developer/api/documentation/v1/functions/SetHold.shtml 
    for more details 

/*********************************************************************************************

<b>8) Use some of the Smartapps available (optional)</b>
/*********************************************************************************************

You can also use some of my smartapps that I've developed.

http://github.com/disconn3ct/device-type.myecobee/tree/master/smartapps

Amongst others:

/****************************************************

<b>a) ecobee3RemoteSensorInit</b>

/****************************************************

This smartapp will expose your ecobee3's remote sensors as Motion and Temperature Sensors in SmartThings, so
that you can use them in your automation scenarios.

See the following readme file for instructions 

http://github.com/disconn3ct/device-type.myecobee/blob/master/smartapps/readme.ecobee3RemoteSensor


/****************************************************

<b>b) Monitor And Set Ecobee Temp</b>

/****************************************************


In brief, the smartapp allows automatic adjustments of your programmed cooling/heating setpoints according to indoor/outdoor conditions. This is particularly useful in Winter/Summer where outdoor temperature and humidity can vary throughout the day. It can also set your thermostat to 'Away' or 'Home' based on your indoor motion sensors.  It will ajust your thermostat's programmed or scheduled setpoints based on occupied rooms (similar to ecobee3, but with ST connected sensors).

You can enable/disable the smartapp with a button on/off tile (ex.virtual switch).

The smartapp can use an outdoor sensor or a virtual weather station, such as

https://github.com/disconn3ct/device-type.weatherstation

to get the oudoor temperature and humidity.

/****************************************************

<b>c) Monitor And Set Ecobee Humidity</b>

/****************************************************

Monitor humidity level indoor vs. outdoor at regular intervals (in minutes) and set the humidifier/dehumidifier/HRV/ERV to a target humidity level.

P.S. Your humidifier/dehumidifier/HRV/ERV needs to be physically connected to ecobee.

/****************************************************

<b>d) ecobeeChangeMode</b>

/****************************************************

Change your ecobee climate (Away,Home) according to your hello home mode.

/****************************************************

<b>e) AwayFromHome and ecobeeResumeProg</b>

/****************************************************

Use presence/motion sensors or ST hello modes to set a target climate or heating/cooling setpoints based on your presence/absence.

/****************************************************

<b>f) ecobeeSetClimate</b>

/****************************************************

This smartapp allows a ST user to set the ecobee thermostat(s) to a given climate (Away,Home,Awake,Sleep, other custom programs) at a given day&time.


/****************************************************

<b>g) ecobeeSetZoneWithSchedule</b>

/****************************************************


The smartapp that enables Multi Zoned Heating/Cooling Solutions based on your ecobee schedule(s)- coupled with smart vents (optional) for better temp settings control throughout your home"


And many others...
