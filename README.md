- [Procedural Biome Generator](#procedural-biome-generator) 
     - [Description](#description)      
- [How it works](#how-it-works)
- [Adjustability](#adjustability)



# Procedural Biome Generator

#### Description

This project procedurally generates biomes for a generated piece of terrain taking altitude, precipitation, and temperature into account. Written in version 2020.3.12f1 of the Unity engine

![Various Examples](https://i.imgur.com/TMBpgdz.png)


#### How it works

A perlin noise map is generated from a seed. A falloff map is subtracted from it to create the height map of the continents. It then generates a temperature map, assigning each tile a temperature based on its altitude and distance from the equator. Note that the boolean `UseTrueEquator` changes where the equator is ("true" equator is exactly in the middle of the map, while a "false" equator is exactly between the northern and southernmost points of land). Next, a humidity map is generated, which is then used to generate a precipitation map. Using the temperature map and the precipitation map, the biomes are generated via an approximation of the [Whittaker Biome classifications](https://upload.wikimedia.org/wikipedia/commons/thumb/6/68/Climate_influence_on_terrestrial_biome.svg/1024px-Climate_influence_on_terrestrial_biome.svg.png). 


#### Adjustability
![variables](https://i.imgur.com/PAan8Hz.png)

All the variables that can be adjusted are found in the ProcGen script on the `Brain` gameobject. The Draw Mode dropdown near the top changes which map is drawn on the screen: the original height map, falloff map, height map, temperature map, precipitation map, and the biome map. The values shown in the image are the default (and optimal) values for each corresponding variable. Changing any value will automatically update in real time. However, you may choose to turn this off by unchecking the checkbox next to `AutoUpdate` under the `Booleans` section. Doing so will require you to hit the `Generate` button at the bottom to generate a new map with your changes. 

![biome variables](https://i.imgur.com/ofoS21W.png)

The dropdown labelled `Biomes` slides open to reveal the Whittaker biome values for each biome: the minimum and maximum temperature range, the minimum and maximum precipitation, and the color the biome appears on the map. 
