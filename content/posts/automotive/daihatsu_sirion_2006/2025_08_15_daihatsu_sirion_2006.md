+++
date = '2025-08-15T20:48:27+02:00'
draft = false
title = 'Car inspection: Daihatsu Sirion 2006 - Day 1'
summary = "Since i have been working in the automotive industry for almost 2 years now, i think it's kind of time to get into cars. My very first project will be a FULL checkup of a Daihatsu Sirion 2006 from the internals to the externals and there will be soooooo much to learn. Lets dive in."
+++

## Preliminary knowledge

Lets talk about my knowledge state and what i did to ramp up.

### My current skill set

The skill set goes as far:
- Drivers license achieved 2 years ago, but haven't driven since (just picked up driving again)
- Knowledge about steering system due to my job
- Okay physics
- Shit ton of motivation for learning/ understanding new things and researching.
  
Hardest part will be to identify not obvious deviations that happen during driving, since i have almost no expertise in feeling out the car, hear things etc.


## Theoretical ramp-up

Multiple videos were digested in a couple of days (see [#References](#references)) to get a basic understanding of the internal workings of the car. I think i get the general idea now.

### Key technical parameters of a car

| Attribute | Value | Meaning |
|-----------|-------|-------|
| **Car Model** | text  | Name and version of the car |
| **Top Speed** | km/h | The maximum speed the car can achieve under ideal conditions |
| **Power** | PS(Pferdestärke) / kW | Engine power in metric horsepower and kilowatts. Measures how much work the engine can do over time. It shows how fast the engine can move the car. Conversion: 1 PS ≈ 0.7355 kW - 1kW . Approximate formula: **PS = (Torque × RPM) / 7127** for metric. |
| **Engine Displacement** | ccm / L | Total volume of all engine cylinders. Larger displacement usually means the engine can burn more fuel-air mixture, producing more power and torque. |
| **Torque** | Nm | Rotational force the engine produces. High torque improves acceleration and how well the car pulls, especially at low speeds.|
| **Engine Type / Configuration** | text | e.g., V6, V8, Inline-4 |
| **Weight** | kg | The curb weight of the car (without passengers or cargo). Lighter cars tend to accelerate faster and handle better. |
| **Power-to-Weight Ratio** | PP | Power per weight unit, performance indicator. Shows engine power relative to the car’s weight. Higher values indicate better performance—how “quick” the car is compared to its mass.|


### Car specific stuff

The only thing i know about the car is that its a Daihatsu Sirion 2006. When i first tried to google these exact phrase couldn't really find the proper model because of the lot of results.

I tried to search for something like a database that has information on car models so somehow i could identify the car and its internal parts.

Found a site called [ultimateSPECS](https://www.ultimatespecs.com/) which was recommended on multiple forums. It even seemed alright, had a category for Daihatsu and also the specific model, however i could not match the tested car to any of the ones on the site. There where even 2 models:

![ultimatespecs_daihatsu_categories](/images/daihatsu_sirion_2006/ultimatespecs_daihatsu_categories.png)

In the normal variant no 2006 model listed, however in the Sirion II there is one from the year 2006.

![ultimatespecs_daihatsu_list](/images/daihatsu_sirion_2006/ultimatespecs_daihatsu_list.png)

It looks good however, i feel like a more accurate and authentic source is needed. After more thinking...

### Gathering more stuff

More information was needed to accurately identify the parts of the car. I knew about VIN ( Vehicle Identification Number) which is a unique id for every car. Based on this, things could be looked up. Lot of shitty ass paid databases, i checked some of them with the cars VIN, however didn't really find a hit.

One other thing you can do in my country (and probably in others) to lookup a cars detailed information based on the name plate. So I did that.

Information gathered:

| **Category**           | **Field**                          | **Value**                                |
|------------------------|------------------------------------|------------------------------------------|
| **Vehicle Data**       | Manufacturer                       | Daihatsu                                 |
|                        | Model Code                         | M3                                       |
|                        | Commercial Description             | Sirion                                   |
|                        | Vehicle Category                   | M1 – Passenger car                       |
|                        | Vehicle Type                       | Passenger car                            |
|                        | Year of Manufacture                | 2006                                     |
|                        | EU Type Approval Number            | e13*2003/97*0147*00                      |
| **Engine Data**        | Engine Number/Code                 | 1KR0179895                               |
|                        | Engine Code                        | 1KR                                      |
|                        | Engine displacement                    | 998 cm³                                  |
|                        | Power Output                       | 51 kW                                    |
|                        | Operating Mode                     | Otto                                     |
|                        | Fuel Type                          | Unleaded petrol                          |
|                        | Environmental Classification       | 09                                       |
|                        | Gearbox                            | Manual (5-speed)                         |
| **Other Technical Data** | Vehicle Body Style               | Hatchback sedan                          |
|                        | Combined Weight                    | 1,390 kg                                 |
|                        | Curb Weight                        | 928 kg                                   |
|                        | Maximum Permissible Gross Weight   | 2,140 kg                                 |
|                        | Passenger Capacity                 | 5                                        |
|                        | Number of Seats (including driver) | 5                                        |
|                        | All-Wheel Drive                    | No                                       |
|                        | Number of Axles                    | 2                                        |
|                        | Number of Driven Axles             | 1                                        |


Got the engine number, thats awesome, also the actual model M3. Remember the engine displacement from the [ultimateSPECS](https://www.ultimatespecs.com/) site? The engine displacement differs so that information is considered invalid for us. Good thinking we kept looking.

### The full description of the car based on the key parameters

| Attribute | Value |
|-----------|-------|
| Car Model | Daihatsu Sirion M3 |
| Top Speed | ~165 km/h |
| Power | 51 kW / 69 PS |
| Engine Displacement | 998 cm³ / 0.998 L |
| Torque | ~81 Nm |
| Engine Type / Configuration | Inline-3 (1KR engine) |
| Weight | 928 kg |
| Power-to-Weight Ratio | ~0.074 kW/kg (~0.093 PS/kg) |1


*Estimations:*

```
Top speed:

Power: 51 kW (~69 PS)
Weight: 928 kg
Small 3-cylinder engine, manual 5-speed gearbox
```

```
Torque (Nm):

Torque (Nm) = (Power (kW) * 9550) / RPM
Torque ≈ (51 * 9550) / 6000 ≈ 81 Nm
```

```
Power-to-Weight Ratio:

Power-to-Weight (kW/kg) = Power (kW) / Weight (kg)
Power-to-Weight ≈ 51 / 928 ≈ 0.074 kW/kg
Power-to-Weight (PS/kg) ≈ 69 / 928 ≈ 0.093 PS/kg
```


## Testing of the car

The car will be inspected from 3 main perspective during the weekends, trying to identify as many deviation as possible:
- Test drive
- Engine bay
- Interior and exterior

Unfortunately because of the lack of tools i cannot view the car from the bottom.

The fixes will be applied after the full inspection, however possible fix's are provided.

### Preparation

We identified the model of the car and now we need something to test against. The owners manual would be the best however the one i got hands on is Dutch and I am so not want to translate continuously. So i did some search on the Internet, but actually i could not find the same owners manual in english, heck in any other language.

First im just gonna test the feature without guide based on common sense, and in the meantime I will try to find and english owners manual, or translate the Dutch one.

*[x] means the feature is working as intended*

*[ ] means the feature has some fault*

## Interior features

### Turn signal stalk

![turn_signal_stalk](/images/daihatsu_sirion_2006/turn_signal_stalk.jpg)

- [X] 1. Parking light / Sidelight (2 frontal, 2 rear)
- [X] 2. Low beam headlight (2 frontal, 2 rear)
- [ ] **3. Fog lamp** (2 frontal, 2 rear)
  - Right rear not working
- [X] 4. Right turn signal (frontal/ rear)
- [X] 5. Left turn signal (frontal/ rear)
- [X] 6. High beam headlight to pull
- [X] 7. High beam headlight to push 

### Wiper stalk

![wiper_stalk](/images/daihatsu_sirion_2006/wiper_stalk.jpg)

![wiper_stalk_docs](/images/daihatsu_sirion_2006/wiper_stalk_docs.png)

The mechanical part works fine for every state, however there is one finding:
- [ ] No liquid for the rear wiper

## Day 1 findings summarized
- On the turn signal stalk in the fog lamp mode the right rear lamp is not working, the reason is not clear yet.
- No liquid for the rear wiper. Theoretically it should be provided from the front tank therefore there could be some clogging issue maybe.

## References

### Ramp-up, general car stuff:
- [ How a Car Engine Works ](https://www.youtube.com/watch?v=ZQvfHyfgBtA)
- [ TORQUE vs HORSEPOWER Explained In Less Than 3 Minutes](https://www.youtube.com/watch?v=a3LYCsG02IM)
- [BRAKES: How They Work | Science Garage](https://www.youtube.com/watch?v=6H7nwlT_qNY)
- [ Animation on How Power Brakes Work ](https://www.youtube.com/watch?v=LY_0REE-g0c)
- [ How do hydraulic brakes in cars and light vehicles work 3D animation ](https://www.youtube.com/watch?v=82qBBJ8iwcc)
- [ Understanding your Car's Steering & Power Steering ! ](https://www.youtube.com/watch?v=em1O8mz7sF0)
- [ How To Properly Inspect a Used Car So You Wouldn't Buy a Lemon](https://www.youtube.com/watch?v=PAxh4gqwHbY&t=2554s)


### About the Daihatsu Sirion 2006
- [ Cara Buka Cover Head unit Sirion Old ](https://www.youtube.com/watch?v=BAIDmIEkS4o)
- [Daihatsu Sirion Service Manual & Technical Information & Body Repair Manual & P.D.I Manual](https://www.scribd.com/document/557197107/Daihatsu-Sirion-Service-Manual-Technical-Information-Body-Repair-Manual-p-d-i-Manual#page=400) - this is not the correct manual