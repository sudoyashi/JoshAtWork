---
layout: post
title:  "New aluminum radiator for the Cabby"
date:   2023-07-18 00:00:00 -1000
categories: Volkswagen golf cabby projectcar bikecarburetors
image: /cabby/badrad/badrad-1.jpg
---
With obvious repairs needed, I might as well take this chance to upgrade some parts! The cooling system takes the highest priority and from there we can do some necessary changes to the fuel system and steering components. Some of these changes were long overdue, and this is the cab inadvertently telling me it needs my attention.

After a couple of weeks of work installing new parts and refurbishing old ones, the cab is back up and running. Better than before, I'd say!

## Cooling system - New radiator, fans, and checking my electrical

Estimated time: 3 hours

![New parts](https://www.sudoyashi.com/assets/img/cabby/badrad/badrad-6.jpg)

Not a bad look for an old car, I'd say.

*A pedantic note on semantics. Radiator vs Heat exchanger: A radiator is a type of heat exchanger used to cool something. It's not only found in cars but has various applications. Heat exchangers can both cool or heat depending on their purpose. While engines need to be heated up to reach their optimal temperature, we usually don't pay much attention to the heating aspect in everyday cars, unless they are high-performance vehicles.*

### 12V, the reason why I overheated

The radiator failed. Overheating caused the radiator burst. But what caused the overheating? My only fan should have kept it cool in the traffic temperature, so let's inspect the fan circuit and what do you know, my constant 12V power wire (red) was not powering anything! The entire circuit never closed and my fans never came on. I've remade a new 12AWG wire to supply constant 12V to the fan switch.

![No power at the red wire](https://www.sudoyashi.com/assets/img/cabby/badrad/badrad-5.jpg)

Well there's your problem, there wasn't any power going to my cooling fans!

## Alu radiator for the shitty racecar

![New aluminum radiator](https://www.sudoyashi.com/assets/img/cabby/badrad/badrad-1.jpg)

*This car is comically slow.*

I got an aluminum radiator, a new fan shroud and two fans. I also replaced the fan switch with a lower-rated one at ~165F to turn the fans on. Originally, I also had the 165F thermostat, but I didn't replace both at the same time. I guess I learned my lesson on that too.

In an A/C configuration, the dual fan setup would run separately, but because cooling for this car is paramount, and I'm just paranoid about overheating again, I wired them in line so both fans will run at the same time.

For anyone running the same universal fan, you want to fuse this with a 15A or 20A fuse, which will depend if you're running additional parts on the same circuit. I will be running a 15A fuse as the power that is accessing this will be relayed, therefore, isolated from other circuits.

### Calculating my fuse for the new fan circuit

To get the amp rating of our circuit, you need the voltage and watt rating of our equipment:

- One fan: 12V at 80W
- Two fans: 12V at 80W * 2

**Amps = Watts/Volts**

- Amps = 80*2/12
- Amps = 13.33A

To get the fuse we need, we want the amp rating + 10%, then round it to the nearest available fuse:

- Fuse = 1.1 * 13.33
- Fuse = 14.663 > 15A blue fuse

... I'm pretty sure this is correct!

I might separate them later on if it's too much cooling. I connected them with quick disconnects, so if two fans provide too much cooling, I can re-configure my circuit later on. The fans were wired in series to the ground and switched power. With the shroud and the fan connected with M6 bolts and rivet nuts, mount it in the car and we're good to go.

## Like my self-care regimen, the aluminum radiator fitment needs work

![New parts](https://www.sudoyashi.com/assets/img/cabby/badrad/badrad-2.jpg)

The size difference between the two radiators meant the mounting points to hold the radiator in place changed. I made some brackets out of scrap metal around my house to hold in place. The factory part is also known as a Radiator Top Retaining Bracket, or Radiator retaining bracket and they are fastened with M6 x 1.0 x 15mm bolts.

I also had the chance to get a lower temp thermoswitch. I actually already had a lower temp thermostat (this 165F range) but got too lazy to buy the matching switch. One bad rad later and we've fixed the mismatch.

![New Radiator thermoswitch](https://www.sudoyashi.com/assets/img/cabby/badrad/badrad-3.jpg)
As always, TEST YOUR PARTS and make sure your critical components are built to its spec. It'll bite you sooner than later.

![New Radiator thermoswitch](https://www.sudoyashi.com/assets/img/cabby/badrad/badrad-4.jpg)

*The new thermoswitch opens around 165F instead of 188F.*

Testing is straightforward! We have 3 pins, looking with the notch up, from left to right we designate each pin as pin 1, 2 and 3.

1. Heat the sensor up to the specified temperature range and see if the circuit opens at 2 of the pins. Which two pins? Pick 2 and find out with your multimeter.
2. Thermoswitches are Normally Open (NO), which means that the circuit is not complete until the condition is met. If you measure resistance, it will be infinite because they are not connected. When the sensor reaches the correct temperature, the condition will be met and the circuit will close. So, once the circuit closes, we will see that resistance is 0 and the circuit is complete.
3. Connect pin 1 to 12V always on, connect pin 2 to switched end, connect this pin to the 12V wire on the fans. Pin 3 will not be used in this configuration, otherwise it would be powering the second fan in an A/C setup.

Tldr, the fans will turn on once the condition is met; the thermoswitch must read 160F to close. Done!

## Cooling system part list

**Total damage: $432.34**

| Item                                                         | Quantity  | Cost (shipping + taxes) |
| ------------------------------------------------------------ | --------- | ----------------------- |
| [Radiator shroud with fans](https://www.ebay.com/itm/275849398540) | 1         | $294.22                 |
| [Low temp fan thermoswitch](https://www.fcpeuro.com/products/audi-vw-engine-cooling-fan-switch-25195948175my) | 1         | $15.79                  |
| Temperature gauge adapter, 32mm                              | 1         | $9.99                   |
| [Electric temperature gauge kit](https://www.amazon.com/dp/B000EVU8YI?psc=1&ref=ppx_yo2ov_dt_b_product_details) | 1         | $22.34                  |
| DIY Retaining brackets                                       | 2         | $0                      |
| VW G12 Coolant  (1 gal)                                      | 2         | $45                     |
| Distilled water (1 gal)                                      | 5         | $15                     |
| Miscellaneous fittings, clamps, etc.                         |           | $30                     |
|                                                              |           |                         |
|                                                              | **Total** | $432.34                 |

Bonus damage to my confidence in safety with this car. I'll probably take it easy again before I bring a passenger lol.

### Cooling System summary

- Parts:
  - Install new radiator, shroud, fans
  - Install lower temperature thermoswitch; tested and opened ~160F. Closed around ~150F
  - Install new temperature gauge adapter for 32mm ID hose
  - Install electric temperature gauge
  - DIY Retaining brackets
  - Flush with distilled water
  - Finish with coolant

- To do:
    - Inspect coolant hoses and othre damage
    - Fit new coolant temp sensor adapter
    - Install new thermoswitch
    - Install radiator assembly
    - Re-route wiring where needed
    - Flush cooling system
    - Fill  new coolant

## Conclusion: Take your time, but not without trying

I don't want to rush the build process just to get it on the road. My skills and approach toward fixing and rebuilding a project have come settled down into my rhythm.  I want to do the work more responsibly, so I'm taking my time and spending a bit more money to get the job done safer.

When I started on my project car, I didn't have as much money or know-how to fix or diagnose anything.  My work was less than average at best and I don't know how I got by with the work I put in before. I like to believe I'm a little smarter now and I'm writing more notes for future me. Hopefully, this helps me out and maybe some other people too.
