# Table of Contents

- [Procedural Biome Generator](#procedural-biome-generator)
 
     - [Description](#description)
     - [Project Files](#project-files)
- [How it works](#how-it-works)

     - [The Height Map](#the-height-map)
     - [The Temperature Map](#the-temperature-map)
     - [Precipitation Map](#precipitation-map)
     - [Biome Map](#biome-map)
- [Adjustability](#adjustability)



# Procedural Biome Generator

#### Description

This project procedurally generates biomes for a generated piece of terrain taking altitude, precipitation, and temperature into account. 

![Various Examples](https://cdn.discordapp.com/attachments/690652979036028929/872971883149160458/examples.png)

#### Project Files
This project was written in C# in version 2020.3.12f1 of the Unity engine. To install this project, unzip the folder and add the `Procedural Biome Generation` folder to
your Unity projects folder. Then, simply open it in Unity by hitting `Add` in Unity Hub.

# How it works
#### The Height Map
![the noise maps](https://cdn.discordapp.com/attachments/690652979036028929/872975048196112474/heightmap.png)

First, a noise map of a given size (500 by 500, in this case) is generated using 
multiple octaves of Perlin Noise. Values below a predefined sea level values are 
automatically set to be equal to the sea level. Next a falloff map is generated: a map in which the
values go from 1 near the edges to 0 near the center, then run through a formula 
to allow for adjustment. These two maps are subtracted from 
each other to create the Height map, which is grid of values from 0 to 1. 

#### The Temperature Map
![temperature map](https://cdn.discordapp.com/attachments/690652979036028929/872979046248632360/unknown.png)

Using the newly generated height map, the temperature map is calculated next. To do this, first the position of the equator is calculated. Equator placement is dependent on whether the boolean `UseTrueEquator` is true or not. 

![equator placement](https://cdn.discordapp.com/attachments/690652979036028929/872978640365834280/equator.png)

Using this information, temperature is then calculated as a combination of the distance from the equator, plus the altitude of the terrain. 

#### Precipitation Map
![Precipitation map](https://cdn.discordapp.com/attachments/690652979036028929/872979775927484487/unknown.png)

The next step is to use the height and temperature maps to generate precipitation. However, to do this the program must first calculate humidity. Getting humidity involves the temperature in celcius as well as a predefined dew point value. This is run through several formulas to get the precipitation. 

#### Biome Map
![the biome map](https://cdn.discordapp.com/attachments/690652979036028929/872981297985892392/unknown.png)

The last step is to determine what biomes go where. This is done using the Whittaker Biome classifications, a simplified model of biome definitions using only precipitation and altitude. 

![whittaker biomes](https://upload.wikimedia.org/wikipedia/commons/thumb/6/68/Climate_influence_on_terrestrial_biome.svg/1024px-Climate_influence_on_terrestrial_biome.svg.png)

# Adjustability
![variables](https://cdn.discordapp.com/attachments/690652979036028929/872982857755287572/unknown.png)

All the variables that can be adjusted are found in the ProcGen script on the `Brain` gameobject. The Draw Mode dropdown near the top changes which map is drawn on the screen: the original height map, falloff map, height map, temperature map, precipitation map, and the biome map. The values shown in the image are the default (and optimal) values for each corresponding variable. Changing any value will automatically update in real time. However, you may choose to turn this off by unchecking the checkbox next to `AutoUpdate` under the `Booleans` section. Doing so will require you to hit the `Generate` button at the bottom to generate a new map with your changes. 

![biome variables](https://cdn.discordapp.com/attachments/690652979036028929/872985040500453376/unknown.png)

The dropdown labelled `Biomes` slides open to reveal the Whittaker biome values for each biome: the minimum and maximum temperature range, the minimum and maximum precipitation, and the color the biome appears on the map. Once again, these values are default (and optimal). 
