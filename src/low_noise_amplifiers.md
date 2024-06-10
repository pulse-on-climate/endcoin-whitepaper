# Low Noise Amplifiers
Low noise amplifiers are cool. You can buy a bunch of these off the shelf for under $50 and they work a treat in amplifying the signal of an incoming satellite image. One issue with current models however is the inability to tune them to work with multiple specific frequencies. 

We want to talk to **all** the satellites to get as many data communication sessions as possible, so in order to do this effectively, we might need to amplify or boost a whole bunch of different frequencies. 

As part of our ongoing deep dive, we found [this great paper](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC6471504/) from 2019 from Aayush Aneja and Xue Jun Li discussing the feasibility of a tunable low noise amplifier for Software Defined Radios (I know, JACKPOT!)

If we can tune this programmatically, then this opens the doors for finer control when a satellite passes by, can counteract doppler effects, and allows us to boost a signal from any source frequency we desire. 
