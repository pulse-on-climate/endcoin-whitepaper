# endcoin-whitepaper

# Table of contents
1. [Introduction](#introduction)
2. [Some paragraph](#paragraph1)
    1. [Sub paragraph](#subparagraph1)
3. [Another paragraph](#paragraph2)

# Introduction to Endcoin <a name="introduction"></a>
Endcoin is a multifaceted entity with a lot of really big problems that the team here are trying to solve. From climate indiference in politics, to underpinning the entire DeFi market, to creating satellite receivers and putting them in space, to buying land and building bubbledomes, we've got something for everyone so buckle up! 

This whitepaper will hopefully provide a glimpse into our thought processes. We will follow the flow of data, from the Sea Surface temperature that underpins the whole system, through to new DeFi systems, and where we will all end up if the world continues to produce carbon at the current rate with zero tangible offset. 

>"We should not underestimate the obstacles. Some are real, such as the need to develop new technologies and to forge international institutions that will promote cooperation. Some obstacles are unnecessary and man-made, such as those posed by the financial interests of polluters or the ludicrous arguments of some of our politicians." 
**- William D. Nordhaus**

# A refresher on Sea Surface Temperature and its Importance to our climate.
The ocean covers 71 percent of Earth's surface. Scientists record sea surface temperature (SST) to understand how the ocean communicates with Earth's atmosphere. SST provides fundamental information on the global climate system. 

Some examples of SSTs role in our climate systems: 
1. **Heat Exchange:** SST is pivotal for the exchange of heat between the ocean and the atmosphere. Heat absorbed by the ocean is moved from one place to another, but it doesn’t disappear. The heat energy eventually re-enters the rest of the Earth system by melting ice shelves, evaporating water, or directly reheating the atmosphere. Thus, heat energy in the ocean can warm the planet for decades after it was absorbed. ("Climate Change: Ocean Heat Content" BY REBECCA LINDSEY AND LUANN DAHLMAN
PUBLISHED SEPTEMBER 6, 2023, https://www.climate.gov/news-features/understanding-climate/climate-change-ocean-heat-content).

2. **Atmospheric Circulation:** SSTs help to drive atmospheric circulation patterns, which determine weather conditions globally. 'ENSO' stands for 'El Niño Southern Oscillation'. The name 'ENSO' is a reminder that close interaction between the atmosphere and ocean is an essential part of the process. While the global climate system contains many processes, ENSO is by far the dominant feature of climate variability on inter-annual timescales. ("Atmospheric Circulation," Met Office, https://www.metoffice.gov.uk/weather/learn-about/weather/atmosphere/global-circulation-patterns).

3. **Climate Projections:** SST data are essential for calibrating and validating climate models, ensuring their accuracy in representing current climate systems and projecting future conditions. These projections are crucial for understanding potential changes in climate, including global warming and extreme weather events. An example can be found in the following link, showing an increase of 1.28°C in and around Japan, which is higher than the global average of 0.61°C. (Sea surface Temperature Around Japan, Japanese Meterological Agency, https://www.data.jma.go.jp/gmd/kaiyou/english/long_term_sst_japan/sea_surface_temperature_around_japan.html).

Hopefully this gets our point across that its a pretty big issue for everyone who exists, and everyone who will exist. 

# Satellite Receiver Device
"... but what if we built a decentrilsed antenna for downloading raw data from satellites?" he asks... 
So thats what we're doing. 
We've built a small POC satellite receiver device, which was kit-bashed together over a weekend to successfully download some image data from a satellite passing overhead. 
Hardware wise, this comprises of a few components: 
1. SDR (Software Defined Radio)
2. Antenna (more on these below)
3. A low noise Amplifier (LNA) ((Also more on this below too!))

Its deceptively simple to get some data directly form a satellite carrying Sea Surface Temperature data collection equipment, but getting the best quality images every time requires a few key areas of improvement:
## Antenna
We initially tested with a simple dipole antenna, the one your grandparents used to have on top of their TV with the big cathode ray tube screen. This worked suprisingly well, and I managed to get a half-scrambled image of the earth from inside my apartment surrounded by big in-the-way buildings. 
Our next port of call was to investigate the use of quadrifilar helix antennas. These are great because you don't need to point them at a satellite directly (so now we don't need to build a motorised base for our antenna! $$$) but the issue is they need to match in size the wavelength your actively trying to communicate on. 
There are some beautiful examples of students working on collapsable quadrifilar helix antennas like [this one](https://news.stanford.edu/2024/01/18/new-portable-antenna-help-disasters/) from earlier in 2023. 

Quadrifilar antenna feel like the best solution as you don't really need to worry about polarization as an end user, so installation will be a breeze, but the issue you might have is where the heck do you put it? 
As an example, NOAA satellites send out cool pictures on the frequency 137.5Mhz, and from high school physics we remember that 𝜆=𝑣/𝑓. 
The velocity(𝑣) of microwaves is around the speed of light, so in m/s 𝑣=299,792,458, and 𝑓=137.5Mhz.
This gives us the value of around 2.18 Meters (λ = 2.1803087854545 M if you're calculating along) so this is how long we make our quadrifilar helix antenna. Easy! But I probably couldn't stick one of these conspicuously outside of my apartment without anyone knowing. Theres a way around that though! 

### Half it, or half it again
With microwave reception, you can basically decide to have your antenna be half the wavelength or a quarter of the wavelength in size, and you should still capture something, but you need to have a pretty high gain amplifier in the right frequency range. If we can solve the amplification stage to a good degree, we can make the antenna for this sort of collection around 50CM tall(ish) which is definitely more reasonable and I could probably get away with it being outside my apartment. 

## Low Noise Amplifiers (LNAs)

Low noise amplifiers are cool. You can buy a bunch of these off the shelf for under $50 and they work a treat in amplifying the signal of an incoming satellite image. One issue with current models however is the inability to tune them. 

We want to talk to all the satellites to get as many data communication sessions as possible, so in order to do this effectively, we might need to amplify or boost a whole bunch of different freqeuncies. 

As part of my ongoaing deep dive, I found [this great paper](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC6471504/) from 2019 from Aayush Aneja and Xue Jun Li discussing the feasibility of a tunable low noise amplifier for Software Defined Radios (I know, JACKPOT!)

If we can tune this programatically, then this opens the doors for finer control when a satellite passes by, can counteract doppler effects, and allows us to boost a single from any source frequency we desire. 

## Still with me? 
That was a bit of a tangent, but shows there is still innovation to be done in low cost satellite ground reception technology. 

NOAA (National Oceanic and Atmospheric Administration) brought out [this guide](https://noaasis.noaa.gov/NOAASIS/pubs/Users_Guide-Building_Receive_Stations_March_2009.pdf) on how to create your own satellite receiver in 2009. 
On page 9 (don't worry you don't have to read it all) they discuss the fact that ground station technology due to technological advancements have dropped from 100,000USD to only 10,000USD. We believe there is a space here for us to drop this entry price further. 