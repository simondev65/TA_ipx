this addon is useful if you collect data from GCE IPX system.

First configure IPX to send push notification to splunk. check IPX docs to do so. 
The idea is to create several pushes
for regular push i set IPX to send this URL : (i call this a heartbeat)

/ipx?action=hb&temp_salon=$THL01&hygro_salon=$THL02&lum_salon=$THL03&temp_bas=$THL04&hygro_bas=$THL05&lum_bas=$THL06&temp_ext=$THL07&hygro_ext=$THL08&lum_ext=$THL09&temp_cave=$THL10&hygro_cave=$THL11&lum_cave=$THL12

=>this way splunk receives the value for X-THL, digital input, ouputs, etc...
(of course you need to create in IPX a scenario to push this every 3 minutes, the scenario is : NO SV1=>ON=>SV1+push heartbeat

Other push are usefull to force ipx to send an event on actions, this way splunk has an event for every action
ex : when light turn on, the scenario exectue a push : 

/ipx?action=light_exterior&entree_digital=$D&relais=$R&e_virtu=$VI&s_virtu=$VO

---once IPx is setup : 
a/install the webhook app on splunk to receive the http request : 
b/install this addon to parse the ipx data
c/configure your aliases in splunk (settings->fields->aliases) to rename the input and output according to your ipx setup


