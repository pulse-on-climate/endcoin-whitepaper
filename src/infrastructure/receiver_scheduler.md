# Receiver Scheduler
The scheduler is the main app running on our device. This will be responsible for getting positional data of the device (how accurate we need to be is still in the works). 
The main purpose of this is actually to ensure we can run the device in a very low power state for as long as possible, and only spin up data recording services when a known satellite is actually close by. 
Once the satellite is in proximity, we will wake up, and start recording the data being streamed from the satellite. Currently our tests have revolved around recording the data, waiting until all data has been collected, then we process the data. We may look to make this more of a continual stream but more R&D needed. 

Depending on the type of receiver antenna we go with, this could also be the app responsible for driving some motors to track the path of the passing satellite. 