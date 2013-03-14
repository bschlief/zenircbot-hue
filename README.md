zenircbot-hue
=============
Provides Philips Hue light service for a ZenIRCBot

Installation & Configuration
============
* Install the glorious ZenIRCBot software.
* Install the Philips Hue lights and bridge
* cd to zenircbot/services
* git clone http://github.com/bschlief/zenircbot-hue
* edit the zenircbot/services/admin.json file to add "zenircbot-hue/hue.js" into services loaded.
```
{
      "services": ["semantics.js", "zenircbot-hue/hue.js"]
}
```
* cd to zenircbot/services/zenircbot-hue
* Copy the sample hue.json.dist to hue.json
* Edit the hue.json file
** put in the ip address of the Philips Hue bridge if you know it.  if you don't, start the services by running the 'node admin.js' command, then join the irc channel with the bot and send the command 'hue locate'.  You'll get a message like so:
```
23:20:37 < bschlief> hue locate
23:20:38 <@rms-bot> bschlief: locating hue bridges...
23:20:44 <@rms-bot> bschlief: bridges found -- [{"host":"192.168.1.135","port":"80"}]
```
** Use that value to fill in the hostname, and stop and start the 'node admin.js' task again.
** Note: You may also edit the groups lists in hue.json.  For example, if you have 6 lights, you'd want to change the "all" group to be like so:
"all": "(1,2,3,4,5,6)"
* Press the connect button the hue bridge, then in the IRC channel, type 'hue register'.  The IRC Bot will create a 40 digit MD5 sum and install it in your hue.json under the key "username".  You should only have to do that once.
* Try a few commands
** hue #ff00ff time=10
** hue #00ff00 time=2 @2
** hue hsl=(230,65535,100) @all


Light Commands
=============
Any ZenIRCBot that implements the hue service will have the following commands available:

* on 
* off
* white=(colorTemp, brightPercent) where colorTemp is a value between 154 (cool) and 500 (warm) and brightPercent is 0 to 100
* brightness=(percent) where percent is the brightness from 0 to 100
* hsl=(hue, saturation, brightPercent) where hue is a value from 0 to 65535, saturation is a value from 0 to 254, and brightPercent is from 0 to 100
* rgb=(red, green, blue) where red, green and blue are values from 0 to 255 - Not all colors can be created by the lights
* #XXxxYY where XX is red value in hex, xx is the green value in hex, and YY is the blue value in hex
* time=seconds this can be used with another setting to create a transition effect (like change brightness over 10 seconds, or change the color over 3600 seconds)
* effect=state where state is either 'colorloop' or 'none'.  The 'colorloop' setting cycles through available colors at the current saturation and brightness.

