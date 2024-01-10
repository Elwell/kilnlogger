# ESPhome Kiln Logger
First attempt at getting the firing log from an Orton AF4 controller sent to Home Assistant

There's a UART on the back of the PCB - pinout is as follows
```
  1 - 3.3v
  2 - Tx
  3 - Rx
  4 - Gnd (nearest buzzer)
```
Pictures of PCB at https://photos.app.goo.gl/Moq7YLs8qn5hLejYA

sample data from UART
```
0,1,0,102,0,0,0,5,68.7,0,68.5,68.5,-5000.0,-5000.0,0.7,0.0,0.0,255,79.9,0.0,0.0
0,1,0,102,0,0,0,10,69.0,0,68.5,68.5,-5000.0,-5000.0,1.7,0.0,0.0,255,79.9,0.0,0.0
0,1,0,102,0,0,0,15,69.3,0,68.4,68.4,-5000.0,-5000.0,3.7,0.0,0.0,255,79.9,0.0,0.0
0,1,0,102,0,0,0,20,69.5,0,68.6,68.6,-5000.0,-5000.0,4.1,0.0,0.0,255,79.9,0.0,0.0
0,1,0,102,0,0,0,25,69.8,0,68.6,68.6,-5000.0,-5000.0,4.9,0.0,0.0,255,80.1,0.0,0.0
0,1,0,102,0,0,0,30,70.1,0,68.6,68.6,-5000.0,-5000.0,5.8,0.0,0.0,255,80.1,0.0,0.0
0,1,0,102,0,0,0,35,70.4,0,68.8,68.8,-5000.0,-5000.0,6.5,0.0,0.0,255,80.2,0.0,0.0
0,1,0,102,0,0,0,40,70.7,0,68.8,68.8,-5000.0,-5000.0,7.4,0.0,0.0,255,80.2,0.0,0.0
0,1,0,102,0,0,0,45,70.9,0,69.2,69.2,-5000.0,-5000.0,6.8,0.0,0.0,255,80.3,0.0,0.0
0,1,0,102,0,0,0,50,71.2,0,69.2,69.2,-5000.0,-5000.0,7.7,0.0,0.0,255,80.5,0.0,0.0
```

and relevant snippet from manual (https://www.ortonceramic.com/remote-monitoring-software)
```
controllerType      0=AF4X, 1=AF4000
kilnMode            Configured mode of the controller
controllerConfig    AF4000 - current TC/relay config setting
activeProgram       Index of the current running program
segmentIndex        Index of the program segment (0-19)
programState        0=Ramp state active, 1=Hold state active
WallTime            Clock time from beginning of a firing
FiringTime          Elapsed time from beginning of a firing
heatWorkAdjusted    0=Set Point not adjusted, 1=Heatwork calculated Set Point
Setpoint            Controller temperature setpoint
AvgT                Average temperature in F or C of all thermocouples
Rate                Calculated ramp rate from start of ramp 
TopT                Top thermocouple temperature in F or C
MidT                Middle thermocouple temperature in F or C
BtmT                Bottom thermocouple temperature in F or C
TopP                Top relay power output (0-100)
MidP                Middle relay power output (0-100)
BtmP                Bottom relay power output (0-100)
activeAlarm         Current active alarm, 255 = no alarm
AmbT                Temperature of the electronics board in F or C
currentXfmr         Value of current transformer in Amps
```

