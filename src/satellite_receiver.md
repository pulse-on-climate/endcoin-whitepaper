# Our Satellite Receiver Device

> "... but what if we built a decentralized antenna for downloading raw data from satellites?" he asks...

So thats what we're doing. 



We've built a small POC satellite receiver device, which was kit-bashed together over a weekend to successfully download some image data from a satellite passing overhead. 
Hardware wise, this comprises of a few components: 
1. SDR (Software Defined Radio)
2. Antenna (more on these below)
3. A low noise Amplifier (LNA) ((Also more on this below too!))

Its deceptively simple to get some data directly from a satellite carrying Sea Surface Temperature data collection equipment, but getting the best quality images every time requires a few key areas of improvement: