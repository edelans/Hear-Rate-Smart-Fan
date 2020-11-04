# Heart-Rate-Smart-Fan

Control your fan speed with your heart beat.

## Use case

I created this while setting up a home trainier for bike training in my garage during the lockdown in 2020. One issue with home trainers, unlike biking outdoor, is that you don't get the benefit of the wind generated by your speed that cool you down. So you sweat a lot, and this creates dehydratation. not cool (pun intended). 

The solution is to use a fan. But when you are lazy (and focused on your workout) you don't want to have to get up and adjust fan speed (and  I don't have a remote for my fan, and it's much cooler to have it automated instead). 


## Parts 

### SmartFan

- ESP32 [~10€ on amazon](https://www.amazon.fr/gp/product/B074RGW2VQ/ref=ppx_yo_dt_b_asin_title_o00_s00?ie=UTF8&psc=1), [~3€ on AliExpress](https://www.aliexpress.com/wholesale?catId=0&initiative_id=SB_20201104000602&origin=y&SearchText=esp32)
- cheap used fan, aim for ~100W (mine was ~20€ on [Leboncoin](https://www.leboncoin.fr/recherche/?category=20&text=ventilateur&price=5-100))
- Light dimmer module with PWM control [~12€ on Amazon](https://www.amazon.fr/gp/product/B07FCF1YSY/ref=ppx_yo_dt_b_asin_title_o05_s00?ie=UTF8&psc=1), [~2€ on Aliexpress](https://es.aliexpress.com/item/32802025086.html?spm=a219c.search0104.3.1.55b65ca8lFJTgG&ws_ab_test=searchweb0_0,searchweb201602_2_10065_10068_10547_319_10891_317_10)
- Dual (BT + Ant+) Heart Rate Monitor (HRM)
- wires

### Other equipments of my setup

- Garmin Forerunner 945 watch
- Elite Direto XR home trainer
- Samsung S5e tablet or Apple TV to run Zwift
- OnePlus 6 to run the Zwift companion app

## Wiring 

4 wires between AC Dimmer and ESP32 : 

(AC dimmer -> ESP32)
VCC -> 3V3
GND -> GND
Z-C -> Pin 4
PWM -> Pin 23

Beware : different implementation of the ESP32 exist, they don't have the same pin pattern, so you'd better rely on pin readings rather than blindlessly following a wiring schema on the internet.

For the 220V part, I just cut a power extension cord in 2, and wired the "incoming" part to "AC-IN", and the "outgoing" part to "LOAD". I didn't find any indication regarding which wire (phase/neutrol) should go where... So either I got lucky, either it doesn't matter... If you are reading this and you have the answer, please [help me](https://github.com/edelans/Heart-Rate-Smart-Fan/issues) !


## Why ESP32 ? 

It's cheap

It's small

It's popular



## Why driving the fan with heart rate ? 

### Speed-based smartFan 
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


