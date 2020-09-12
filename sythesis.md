# Synthesis

## UGens (Unit Generators)

### Mouse Theramin
```supercollider
{SinOsc.ar(freq: MouseX.kr(300, 2500), mul: MouseY.kr(0, 1))}.play;
```
### Plotting
```supercollider
{SinOsc.ar}.plot;
```
![](sinoscplot.png)
```supercollider
{Saw.ar}.plot;
```
![](sawplot.png)
```supercollider
{Pulse.ar}.plot;
```
![](pulseplot.png)
