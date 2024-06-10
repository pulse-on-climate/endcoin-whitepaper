# Antenna


## Dipole
We initially tested with a simple dipole antenna, the one your grandparents used to have on top of their TV with the big cathode ray tube screen. This worked surprisingly well, and I managed to get a half-scrambled image of the earth from inside my apartment surrounded by big in-the-way buildings.

## Quadrifilar
Our next port of call was to investigate the use of Quadrifilar helix antennas. These are great because you don't need to point them at a satellite directly (so now we don't need to build a motorized base for our antenna! $$$) but the issue is they need to match in size the wavelength your actively trying to communicate on. 
There are some beautiful examples of students working on collapsable quadrifilar helix antennas like [this one](https://news.stanford.edu/2024/01/18/new-portable-antenna-help-disasters/) from earlier in 2023. 
Quadrifilar antenna feels like the best solution as you don't really need to worry about polarization as an end user, so installation will be a breeze, but the issue you might have is where the heck do you put it? 
As an example, NOAA satellites send out cool pictures on the frequency 137.5Mhz, and from high school physics we remember that:
> 𝜆=𝑣/𝑓


The velocity(𝑣) of microwaves is around the speed of light, so (in m/s)
> 𝑣=299,792,458, and 𝑓=137.5Mhz.
This gives us the value of around 2.18 Meters (λ = 2.1803087854545 M if you're calculating along) 

So this is how long we make our quadrifilar helix antenna. Easy! But I probably couldn't stick one of these conspicuously outside of my apartment without anyone knowing. Theres a way around that though! 

### Half it, or half it again 
With microwave reception, you can basically decide to have your antenna be half the wavelength or a quarter of the wavelength in size, and you should still capture something, but you need to have a pretty high gain amplifier in the right frequency range. If we can solve the amplification stage to a good degree, we can make the antenna for this sort of collection around 50CM tall(ish) which is definitely more reasonable and I could probably get away with it being outside my apartment. 

## Parabolic Dishes
These are the boujee option, and probably required if we want to start downloading HRPT (High-Resolution Picture Transmission)

