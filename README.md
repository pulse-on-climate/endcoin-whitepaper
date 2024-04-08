![Rad looking Endcoin Image](https://gcdnb.pbrd.co/images/MOyZaxX4iiKc.png?o=1)
# Table of contents
1. [Introduction to Endcoin](#introduction)
2. [A refresher on Sea Surface Temperature and its Importance to our climate.](#climate-change-refresh)
3. [Satellite Receiver Device](#satellitereceiverdevice")
4. [ A foreword on data ](#foreword-on-data)
5. [Satellite data collection ](#datacollection)
6. [Take a break](#another-break)
7. [The bigger infrastructure picture](#big-picture)
8. [A word or two on other sources](#other-sources)
9. [Storage and Network](#storage-and-network)
10. [Cell and Map Creation](#cell-and-map-creation)
11. [OMG Are we on-chain yet??!?](#omg)
12. [Switchboard](#switchboard)
13. [AMM and token emission](#amm-and-token-emission)
14. [Emission formula](#formula)
15. [Data point as a constant](#datapoint)
16. [Emission distribution](#emission-distribution)
17. [A word on bubbledomes](#bubbledomes)
18. [Summary](#summary)
# Introduction to Endcoin <a name="introduction"></a>
Endcoin starts by building A DePin Satellite receiver network to produce a reading of sea surface temperatures. This acts as a price feed to drive existing DeFi systems towards positive climate impact: A standard rate for the global economy that is owned by the Earth.

## Some more details: <a name="moredetails"></a>
Endcoin is a multifaceted entity with a lot of really big problems that the team here are trying to solve. From climate indiference in politics, to underpinning the entire DeFi market, to creating satellite receivers and putting them in space, to buying land and building bubbledomes, we've got something for everyone so buckle up! 

This whitepaper will hopefully provide a glimpse into our thought processes. We will follow the flow of data, from the Sea Surface temperature that underpins the whole system, through to new DeFi systems, and where we will all end up if the world continues to produce carbon at the current rate with zero tangible offset. 

>"We should not underestimate the obstacles. Some are real, such as the need to develop new technologies and to forge international institutions that will promote cooperation. Some obstacles are unnecessary and man-made, such as those posed by the financial interests of polluters or the ludicrous arguments of some of our politicians." 
**- William D. Nordhaus**

# A refresher on Sea Surface Temperature and its Importance to our climate. <a name="climate-change-refresh"></a>
The ocean covers 71 percent of Earth's surface. Scientists record sea surface temperature (SST) to understand how the ocean communicates with Earth's atmosphere. SST provides fundamental information on the global climate system. 

Some examples of SSTs role in our climate systems: 
1. **Heat Exchange:** SST is pivotal for the exchange of heat between the ocean and the atmosphere. Heat absorbed by the ocean is moved from one place to another, but it doesn’t disappear. The heat energy eventually re-enters the rest of the Earth system by melting ice shelves, evaporating water, or directly reheating the atmosphere. Thus, heat energy in the ocean can warm the planet for decades after it was absorbed. ("Climate Change: Ocean Heat Content" BY REBECCA LINDSEY AND LUANN DAHLMAN
PUBLISHED SEPTEMBER 6, 2023, https://www.climate.gov/news-features/understanding-climate/climate-change-ocean-heat-content).

2. **Atmospheric Circulation:** SSTs help to drive atmospheric circulation patterns, which determine weather conditions globally. 'ENSO' stands for 'El Niño Southern Oscillation'. The name 'ENSO' is a reminder that close interaction between the atmosphere and ocean is an essential part of the process. While the global climate system contains many processes, ENSO is by far the dominant feature of climate variability on inter-annual timescales. ("Atmospheric Circulation," Met Office, https://www.metoffice.gov.uk/weather/learn-about/weather/atmosphere/global-circulation-patterns).

3. **Climate Projections:** SST data are essential for calibrating and validating climate models, ensuring their accuracy in representing current climate systems and projecting future conditions. These projections are crucial for understanding potential changes in climate, including global warming and extreme weather events. An example can be found in the following link, showing an increase of 1.28°C in and around Japan, which is higher than the global average of 0.61°C. (Sea surface Temperature Around Japan, Japanese Meterological Agency, https://www.data.jma.go.jp/gmd/kaiyou/english/long_term_sst_japan/sea_surface_temperature_around_japan.html).

Hopefully this gets our point across that its a pretty big issue for everyone who exists, and everyone who will exist. 

# Satellite Receiver Device <a name="satellitereceiverdevice"></a>
"... but what if we built a decentralized antenna for downloading raw data from satellites?" he asks... 
So thats what we're doing. 
We've built a small POC satellite receiver device, which was kit-bashed together over a weekend to successfully download some image data from a satellite passing overhead. 
Hardware wise, this comprises of a few components: 
1. SDR (Software Defined Radio)
2. Antenna (more on these below)
3. A low noise Amplifier (LNA) ((Also more on this below too!))

Its deceptively simple to get some data directly from a satellite carrying Sea Surface Temperature data collection equipment, but getting the best quality images every time requires a few key areas of improvement:
## Antenna 

**Dipole**
We initially tested with a simple dipole antenna, the one your grandparents used to have on top of their TV with the big cathode ray tube screen. This worked surprisingly well, and I managed to get a half-scrambled image of the earth from inside my apartment surrounded by big in-the-way buildings.

**Quadrifilar**
Our next port of call was to investigate the use of Quadrifilar helix antennas. These are great because you don't need to point them at a satellite directly (so now we don't need to build a motorized base for our antenna! $$$) but the issue is they need to match in size the wavelength your actively trying to communicate on. 
There are some beautiful examples of students working on collapsable quadrifilar helix antennas like [this one](https://news.stanford.edu/2024/01/18/new-portable-antenna-help-disasters/) from earlier in 2023. 
Quadrifilar antenna feels like the best solution as you don't really need to worry about polarization as an end user, so installation will be a breeze, but the issue you might have is where the heck do you put it? 
As an example, NOAA satellites send out cool pictures on the frequency 137.5Mhz, and from high school physics we remember that 𝜆=𝑣/𝑓. 
The velocity(𝑣) of microwaves is around the speed of light, so in m/s 𝑣=299,792,458, and 𝑓=137.5Mhz.
This gives us the value of around 2.18 Meters (λ = 2.1803087854545 M if you're calculating along) so this is how long we make our quadrifilar helix antenna. Easy! But I probably couldn't stick one of these conspicuously outside of my apartment without anyone knowing. Theres a way around that though! 

**Parabolic Dishes**
These are the boujee option, and probably required if we want to start downloading HRPT (High-Resolution Picture Transmission)

### Half it, or half it again 
With microwave reception, you can basically decide to have your antenna be half the wavelength or a quarter of the wavelength in size, and you should still capture something, but you need to have a pretty high gain amplifier in the right frequency range. If we can solve the amplification stage to a good degree, we can make the antenna for this sort of collection around 50CM tall(ish) which is definitely more reasonable and I could probably get away with it being outside my apartment. 

## Low Noise Amplifiers (LNAs)

Low noise amplifiers are cool. You can buy a bunch of these off the shelf for under $50 and they work a treat in amplifying the signal of an incoming satellite image. One issue with current models however is the inability to tune them. 

We want to talk to all the satellites to get as many data communication sessions as possible, so in order to do this effectively, we might need to amplify or boost a whole bunch of different frequencies. 

As part of my ongoing deep dive, I found [this great paper](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC6471504/) from 2019 from Aayush Aneja and Xue Jun Li discussing the feasibility of a tunable low noise amplifier for Software Defined Radios (I know, JACKPOT!)

If we can tune this programmatically, then this opens the doors for finer control when a satellite passes by, can counteract doppler effects, and allows us to boost a signal from any source frequency we desire. 

## Still with me? 
That was a bit of a tangent, but shows there is still innovation to be done in low cost satellite ground reception technology. 

NOAA (National Oceanic and Atmospheric Administration) brought out [this guide](https://noaasis.noaa.gov/NOAASIS/pubs/Users_Guide-Building_Receive_Stations_March_2009.pdf) on how to create your own satellite receiver in 2009. 
On page 9 (don't worry you don't have to read it all) they discuss the fact that ground station technology due to technological advancements have dropped from 100,000USD to only 10,000USD. We believe there is a space here for us to drop this entry price further, without compromise on quality of data.

# A foreword on data <a name="foreword-on-data"></a>
The above details our work on making more accessibly priced ground stations. Next we will be discussing the data we collect, how we validate it, and how we intend to use it. We have some pretty dry diagrams showing the software logic, but will try to keep it high level. 
## What is a fragment?
In this context, a fragment is a square of usable information that can be cross checked with other squares to provide consensus of data accuracy. 
We gather data from a satellite, we re-project the image onto the earth to get accurate latitude and longitude values, we then randomly offset the grid to create fragments. This means if me and my neighbor both have satellite receivers, and collect the same image, we will both have a slightly different collection of fragments. We'll discuss this further shortly. 
We are currently defining a fragment as a 0.25 degree square of latitude and longitude values, which covers around 40km of earths surface, but this is subject to change after more R&D cycles. 
## What is a Cell? 
A cell is the smallest amount of data that is verified from a collection of fragments. Fragments with their own random gridded offset are overlay on top of each other, consensus is made from the overlapping information provided from each. This gives us a confidence value for each of the pixels representing a temperature value in the data, which could be used as part of the sea surface model to weight the data appropriately. 
We also define a cell as the same size of a fragment, so 0.25 degrees square at this moment. 
# A foreword on data <a name="foreword-on-data"></a>
Our satellite receiver POC device will be able to listen to and receive data agnostically from all satellites. 
We will now discuss the format of that data and how we shape it from satellite, to POC device, to averaged SST value underpinning the worlds economy. Ready?  

![Data Pipeline](https://gcdnb.pbrd.co/images/UbCDwNnOE8dl.jpg?o=1)

We're going to dive into each of the steps within the diagram. Go and make a coffee, then read on.  

# Satellite data collection <a name="datacollection"></a>
Modern satellites use a bunch of different instruments to collect information about our planet, and beam them back down to earth for scientists to consume and make sense of the world. For Sea Surface Temperature (Sea Surface Skin temperature actually) we use a super precise radiometer to capture this data. 

## Satellite Data Transmission
There are two common transmission types: 
- HRPT (High Resolution Picture Transmission): HRPT is transmitting in L-band (1670-1710 MHz) range and can provide the resolution of 1km per pixel.
- APT (Automatic Picture Transmission): APT is transmitting in VHF (137-138 MHz) range and can provide the lower resolution of 4km per pixel.

A lot of our tests up to now have focused on APT data, its a bit easier to consume, but HRPT is definitely the future and where we want to get to for more accurate temperature values. 

## Receiver - Scheduler
The scheduler is the main app running on our device. This will be responsible for getting positional data of the device (how accurate we need to be is still in the works). 
The main purpose of this is actually to ensure we can run the device in a very low power state for as long as possible, and only spin up data recording services when a known satellite is actually close by. 
Once the satellite is in proximity, we will wake up, and start recording the data being streamed from the satellite. Currently our tests have revolved around recording the data, waiting until all data has been collected, then we process the data. We may look to make this more of a continual stream but more R&D needed. 

Depending on the type of receiver antenna we go with, this could also be the app responsible for driving some motors to track the path of the passing satellite. 

## Processing and signing
In the processing and signing stage, we are effectively encrypting and verifying data at each individual step, outputting a [Merkle tree](https://en.wikipedia.org/wiki/Merkle_tree) which can be interrogated to establish the data integrity. 
With accurate device position, time data, and satellite positional data, we can improve our confidence that our device recorded data from the right source. This data is added to the overall signed data collection. 

We decode audio file and sign all of the output. 


## Fragment Creation
We next begin our fragment creation! We take our image file and the metadata decoded from the satellite, and re-project this onto Earth to get accurate latitude and longitude values. 
We then grid the data as 0.25 degree square grid, with a random offset value generated by the hardware security module (HSM) in our device. As we discussed above, this means two people could get the same image from a satellite, but have a unique collection of fragments, which can all be added together to prove the resulting information is accurate. 
As part of this step, we can also bin grids that are not relevant for example grids that totally cover a piece of land. 

We sign each fragment with the random number generated, lat + lon values of the fragment and a reference to previous data to continue the merkle tree.


# Take a break<a name="another-break"></a>
Phew, that was a lot. If you've finished your coffee, grab a water. We're gonna take a look at the wider scope now of where this data goes, and what it means for the world as a whole.


# The bigger infrastructure picture<a name="big-picture"></a>
This image gives a wider overview, we'll work on more granular details of this as we go, and will be reaching out to industry experts to help shape all of this. 

![The overall Picture](https://gcdnb.pbrd.co/images/k359UcpBazlr.jpg?o=1)

# A word or two on other sources<a name="other-sources"></a>
This still requires fleshed out, but there is a plethora of data products, sensor networks etc. that already exist in centralized entities. We believe in science, and as such treat the scientific community with respect, admiration and trust, but we also agree that any centralized system can be swayed by opinion and personal gain. We aim to be another voice in that crowd, to help bolster scientific endeavors and validate the hard work of so many brilliant minds in climate science and technology.

We need to work out how these systems are currently verified, and how we fit into that stack. We believe there is space. 
# Storage and Network (The middle bit)<a name="storage-and-network"></a>
## Storage
This is an area we have experience in from previous work, but we're still unsure on how exactly we will approach this for Endcoin. 
We have written apps to interface with IPFS - but because we have a proof of all data, we could potentially just dump it all in an S3 bucket for the next step. 

Ultimately this step is fairly low risk due to the steps taken on proofs and data verification throughout the process, so we will likely be driven by cost and ease of access in this section. If you have suggestions, please let us know. 

## Network
We aim to have a flexible approach to networking and are fairly confident on our data integrity due to signing, so enabling our device to communicate over WiFi, Ethernet (With cool POE support) or 5G will be our focus. We have expressed an interest in working with the folks at Helium to be able to agnostically use their infrastructure and the noises they've made so far are really positive. 

# Cell and Map Creation<a name="cell-and-map-creation"></a>
## Working theory
![Creation of a map](https://gcdnb.pbrd.co/images/q4VCCjPcqhe5.jpg?o=1)
Bringing this all together with the above image. 
- We made a bunch of fragments earlier with our cool POC receiver. 
- We stored all of them in a storage medium. 
- We make some cells
- We stitch those cells together
- We make a map
- We have completed our dataset for SST for 1x day. 

## Cell creation 
The first step here is cell creation. 
We will develop the app for this, and it will exist independently of running a satellite receiver, so it gives people who aren't ready to purchase a hardware device, or who live underground already and don't have the luxury of direct line of sight to a satellite the chance to also contribute to verifying the data, and farm tokens in preparation for the end of the world (more on that coming up!). 
Our cell builder app with grab a bunch of fragments in a latitude and longitude range, and will verify them against each other. As there will be a large overlay in the center of the cell, we will be very confident about the value of this. In the outer edges of the cell we are slightly less confident.

## Map building
When building the entire map, we begin to stitch all of the cells together. This is almost a repeat of the fragments to cells program, but allows for extra scrutiny to ensure we have an accurate representation of temperature values for each cell. 
I guess we can sort of look at this as rounds of consensuses.

# OMG Are we on-chain yet??!?<a name="omg"></a>
Yes! (almost)

# Switchboard <a name="switchboard"></a>
As part of recent work, we ended up discovering Switchboard, who have a really great community, and a fairly cheap oracle system, allowing us to check our data against those other sources we mentioned earlier. 

We use switchboard to aggregate all of the data together and get a average SST value of the earth. 
We do this once a day, and this value becomes instrumental in the emission function of our AMM. 
(hell yeah on chain lets goooooooo)

# AMM and token emission <a name="amm-and-token-emission"></a>
We currently have the Endcoin base program on Devnet. We submit through switchboard using a known centralized data point for now to alter the number of Endcoin and Gaiacoin that are emitted daily. 
## Who the f**hell is Gaia? 
Gaia is the Earth. Coined by James Lovelock, Gaia is a proposed theory that the Earth is constantly self-regulating. This is a pretty nice article that explains his theories in more detail than I can be bothered regurgitating. 
TLDR; GAIA = Earth. 

`Sadly, its much easier to create a desert than a forest` - James Lovelock

# Emission formula <a name="formula"></a>
Our current working formula is: 
- death (d) = 35 (when its too hot to handle)
- endrate (e) = 1.125
- gaiarate (g) = 0.75
- meanTemperature (T) = current average sst temp on a daily basis

#### Endcoin
$$ endemission = Math.exp(endrate * (death - meanTemperature)) - 1 $$

$$ E = exp(e* (d - T)) -1 $$


#### Gaiacoin
$$ gaiaemission = Math.exp(gaiarate * (meanTemperature)) - 1 $$

$$ G = exp(g * T) - 1     $$

 	


This graphs as two exponential functions, with Endcoin hitting exactly 0 when global average Sea Surface Temperature hits 35 degrees (Spoiler alert, we'll all be dead). When this happens, you see Gaiacoin spin wildly out of control, emitting around 293 billion into the economy each day temperatures are at 35 degrees... It'll still be the least of our worries though so DON'T PANIC. 

![The graph](https://gcdnb.pbrd.co/images/Y01a0sKy6CFo.png?o=1)

## Some reasoning
Q: Why are the endrate and gaiarate different? 


`A: The world can be damaged faster than it can be fixed, this adds that to the underpinning of the system`


Q: Why is the crossover point neatly pegged at 21 degrees C? 


`A: In 2023 the average sea surface temp for the whole year is around 21 degrees, so we use this as the crossover point, as this is when our new financial system starts in the wake of.`

# Data point as a constant <a name="datapoint"></a>
We have now successfully emitted tokens based on a real world data point which has climate impact. This begins to bridge the gap between financial markets and climate science for people not directly interested in ReFi opportunities. 


If I'm just an oil barron degen, I can still invest in Endcoin and short the end of the world for unlimited gains, but this is now proveable, on chain, for the whole world to see. 


# Emission distribution <a name="emission-distribution"></a>
Currently, we emit all tokens directly to a pool. For mainnet launch, we will also implement swap functionality and distribution to people running a satellite receiver or a cell/map builder app. This allows the tokens to enter the market, and begin to flow. The swap functionality will allow people to swap their Endcoin for Gaiacoin and vice versa, but will not allow people to stake in the pool. 

This pool therefore gives us: 
$$ SST + market sentiment = Pulse on Climate $$

This is a realtime value that can be displayed to show the current state of the planet and our opinion as a society towards it rolled into one data source. 

## Emission period
Similar to index funds, we will update the SST value once a day. This gives us the following benefits which we think align with our mission: 

1. **Simplicity and Transparency:** The daily emission of tokens based on SST values introduces a straightforward and transparent mechanism for token generation. Users and investors can easily understand the criteria for token issuance, which is based on measurable, external environmental data. This transparency can build trust in the system.

2. **Stabilization of Token Value:** Emitting tokens once a day based on SST stabilizes the token's value by reducing its exposure to short-term speculative trading and market volatility. The value of the tokens becomes more closely tied to the actual changes in SST, rather than speculative market movements, which could make the tokens more attractive to long-term investors interested in environmental trends.

3. **Cost Efficiency:** A system that operates on a set schedule (once daily) can optimize its computational and operational resources, potentially lowering the costs associated with token emission. These savings can be passed on to the community or reinvested into the project, for example, by enhancing the system's data accuracy or contributing to ocean conservation efforts.

4. **Reduced Market Impact:** By aggregating transactions and emissions to a once-daily event, the potential market impact of large trades or emissions is minimized. This can help maintain a more stable trading environment for the tokens, benefiting all participants by reducing price manipulation and extreme volatility.

5. **Ease of Investment Decision Making:** Investors can make more informed decisions without the pressure to react to minute-by-minute changes. Knowing that token emissions are tied to daily SST values allows investors to research and understand the environmental factors that might influence the token's value, leading to more strategic, informed investment decisions.

6. **Mitigates Timing Risk:** The daily update mechanism mitigates risks associated with timing in the market. Investors focus on the longer-term trends in SST values and their implications for token emissions, rather than attempting to time the market for short-term gains.

7. **Alignment with Environmental and Long-term Investment Strategies:** By linking token emissions to SST values, the system naturally aligns with long-term environmental monitoring and conservation goals. It offers a novel way for investors to engage with climate-related issues, supporting a sustainable investment strategy that looks beyond immediate financial returns to consider broader environmental impacts.


For such a system to be effective, it's crucial to ensure the accuracy and integrity of the SST data used for token emission, incorporating multiple data sources and verification mechanisms to prevent manipulation and ensure reliability. Additionally, clear communication about how SST values translate into token emissions can further enhance transparency and trust in the system. Hopefully this whitepaper has shown that this is our ultimate goal. 

# A word on bubbledomes <a name="bubbledomes"></a>
![Rad looking Endcoin Image](https://cdn.imgpaste.net/2024/04/05/SxVuxp.png)
Bubbledomes are our version of future real estate that we foresee humanity sheltering in when the world begins to end. 
Cities over the course of humanity have risen and fallen and entire civilisations have collapsed before, and usually there is an element of climate change that causes this. 
We talked about this internally more as a meme, but the reality when we actually decided to dig in a bit more is quite alarming, sinister, and so ludicrous that it becomes reality. 

[Here's an article from Business Insider showing 12 locations to go if the world goes to hell](https://www.businessinsider.com/places-to-go-during-apocalypse-2011-5)
[Here's a link from the guardian talking about where Billionaires have began constructing bunkers](https://www.theguardian.com/news/2022/sep/04/super-rich-prepper-bunkers-apocalypse-survival-richest-rushkoff)
[Here's a cool little slide deck from Forbes on the subject too](https://www.forbes.com/stories/billionaires/inside-billionaire-bunkers/)

Basically theres big business in creating end of the world doomsday bunkers. We want to reach more than just 50-100 billionaires driving daddy's lambo around the cool streets of LA. We want to reach all of humanity and build areas where art, technology and life can continue to prosper, because what the hell else will we do when we can't buy crypto punks anymore? 

Endcoin will eventually position itself to create a REIT in charge of buying land and developing bubbledomes for humanity's inevitable end should we not heed scientific warnings of climate change. 

# Summary <a name="summary"></a>
We've made it! We've gotten to the end of this whitepaper! Congrats if you read all the way through, go and touch some grass immediately. 

What have we learned? 
- Sea Surface Temperatures are important to climate science
- Data collection from satellites is getting easier, and cheaper, and we are the ones to do it. 
- Satellite and space are areas that are highly regulated and shared within the global community, making alignment of this data and blockchain technology simple to integrate with each other. 
- There's a huge increase in focus and funding for space industries across the world, which Endcoin slots in to effectively to help shape the instruments that we will send to space. 
- Tying financial infrastructure to climate change is a worthwhile cause, and gives sovereignty back to the earth through a single data point.  
- Billionaires are buying bunkers for the end of the world, so you should too. Invest in Bubbledomes today. 
