zenircbot-hue
=============
Provides Philips Hue light service for a ZenIRCBot

Installation & Configuration
============
* Install the Philips Hue lights and bridge
* Install node.js
* Install the glorious [ZenIRCBot](https://github.com/wraithan/zenircbot) software.
* Install the terrific [node-hue-api](https://github.com/peter-murray/node-hue-api) through npm
<pre>
npm install node-hue-api
</pre>
* cd to zenircbot/services
* git clone http://github.com/bschlief/zenircbot-hue zenircbot-hue
* edit the zenircbot/services/admin.json file to add "zenircbot-hue/hue.js" into services loaded.
<pre>
{ 
      "services": ["semantics.js", "zenircbot-hue/hue.js"] 
}
</pre>
* cd to zenircbot/services/zenircbot-hue
* cp hue.json.dist hue.json
* Edit the new hue.json file
* put in the ip address of the Philips Hue bridge if you know it.  if you don't, start the services by running the 'node admin.js' command, then join the irc channel with the bot and send the command 'hue locate'.  You'll get a message like so:
<pre>
23:20:37 < bschlief> hue locate
23:20:38 <@rms-bot> bschlief: locating hue bridges...
23:20:44 <@rms-bot> bschlief: bridges found -- [{"host":"192.168.1.135","port":"80"}]
</pre>
* Use that value to fill in the hostname in hue.json, and stop and start the 'node admin.js' task again.
* Press the connect button the hue bridge, then in the IRC channel, type 'hue register'.  The IRC Bot will create a 40 digit MD5 sum and install it in your hue.json under the key "username".  You should only have to do that once.
* Try a few commands
<pre>
hue #ff00ff time=10
hue #00ff00 time=2 @2
hue hsl=(230,65535,100) @all
hue group odd_lights=(1,3)
hue rgb=(128,0,128) @odd_lights
</pre>

Light Commands
=============
Any ZenIRCBot that implements the hue service will have the following commands available:

* <code>on</code>
* <code>off</code>
* <code>white=(colorTemp, brightPercent)</code> where colorTemp is a value between 154 (cool) and 500 (warm) and brightPercent is 0 to 100
* <code>brightness=(percent)</code> where percent is the brightness from 0 to 100
* <code>hsl=(hue, saturation, brightPercent)</code> where hue is a value from 0 to 65534, saturation is a value from 0 to 254, and brightPercent is from 0 to 100
* <code>rgb=(red, green, blue)</code> where red, green and blue are values from 0 to 255 - Not all colors can be created by the lights
* <code>#RRGGBBY</code> where RR is red value in hex, GG is the green value in hex, and BB is the blue value in hex
* <code>time=seconds</code> this can be used with <code>white</code>, <code>brightness</code>, <code>hsl</code>, <code>rgb</code>, <code>#RRGGBB</code> commands to apply a state over a number of seconds.  
* <code>effect=state</code> where state is either 'colorloop' or 'none'.  The 'colorloop' setting cycles through available colors at the current saturation and brightness.



