# Synthesis

## UGens (Unit Generators)

### Mouse Theramin
```supercollider
{SinOsc.ar(freq: MouseX.kr(300, 2500), mul: MouseY.kr(0, 1))}.play;
```
### Plotting
![](sinoscplot.png)
```supercollider
{SinOsc.ar}.plot;
```
![](sawplot.png)
```supercollider
{Saw.ar}.plot;
```
![](pulseplot.png)
```supercollider
{Pulse.ar}.plot;
```
