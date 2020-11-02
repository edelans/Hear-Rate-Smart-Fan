# Heart-Rate-Smart-Fan

Control your fan speed with your heart beat.

## Use case

I created this while setting up a home trainier for bike training in my garage during the lockdown in 2020. One issue with home trainers, unlike biking outdoor, is that you don't get the benefit of the wind generated by your speed that cool you down. So you sweat a lot, and this creates dehydratation. not cool (pun intended). 

The solution is to use a fan. But when you are lazy (and focused on your workout) you don't want to have to get up and adjust fan speed (and  I don't have a remote for my fan, and it's much cooler to have it automated instead). 

## Parts 

### smartFan

- ESP32 ~10€ (cheaper if you can wait from China imports)
- cheap used fan ~20€ on Leboncoin
- Light dimmer ~12€
- Dual (BT + Ant+) Heart Rate Monitor (HRM)
- wires

### other equipments of my setup

- Garmin Forerunner 945 watch
- Elite Direto XR home trainer
- Samsung S5e tablet or Apple TV to run Zwift
- OnePlus 6 to run the Zwift companion app

## Wiring 
todo


## why ESP32 ? 

It's cheap
It's small
It's popular


## Why driving the fan with heart rate ? 

### speed-based smartFan 
❌ You **don't** get wind when you need it the most
Good idea to mimic the outdoor experience, but then you realize that when you are @170bpm attempting Alpe d'Huez ascension at 12km/h, you won't get a lot of fan wind, but I promise you'll crave for it !

### Power-based smartFan 
👍 You get wind when you need it the most
❌ Technical obstable : your home trainer can probably connect to 1 device in BT and 1 device in ANT+. ESP32 doesn't support ANT+ but supports bluetooth natively. Pairing your home trainer with zwift in ANT+ can only be done if you have an ANT+ compatible device running zwift (which is not the case of the Apple TV, unless their should be a workaroung with the Zwift companion app running on your phone if it supports ANT+). 

 
### Heartrate-based smartFan
👍 You get wind when you need it the most
👍 Easy to find an HRM compatible with ANT+ and Bluetooth at the same time. Be careful as if you pair your heart rate monitor to the esp32 in bluetooth, you probably won't be able to pair it to something else in BT (unless you have some very recent heart rate monitor like the Wahoo tickr which can pair to up to 3 devices simultaneously). 
➡️ Seems to be the most versatile setup! 

## Who connects to what ? 

### Tablet setup 

- Home trainer connects to tablet via ANT+
- HRM connects to the smartFan via BT
- HRM connects to garmin forerunner watch via ANT+, which in turn connects to tablet via BT (I could skip the garmin watch intermediary byt connecting the HRM to the tablet via BT, but I want to keep my records clean in garmin connect. Maybe zwift integration could be enough ?)

### Apple TV setup

You only have 2 bouetooth connections available to the Apple TV, the workaround is to use the Zwift companion app on your spartphone to proxy all connected devices through a single BT connection to the Apple TV.

- Home trainer connects to smartphone (Zwift companion app) via BT 
- HRM connects to smartFan via BT
- HRM connects to garmin watch with ANT+, which in turn connects to smartphone (Zwift companion app) via BT
- smartphone (Zwift companion app) connects to Apple TV via BT


That's a lot of conenctions... I can simplify by removing the garmin watch and connecting the HRM directly to the phone/tablet via ANT+.




# Inspiration 

Thanks a lot to @jmlopezdona and his project here https://github.com/jmlopezdona/smartfan-esp32 for a speed controlled smart fan for paving the way for the present project (Heart rate controlled). 


