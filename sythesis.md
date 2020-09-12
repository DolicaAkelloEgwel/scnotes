# Synthesis

## UGens (Unit Generators)

### Mouse Theremin
```supercollider
{SinOsc.ar(freq: MouseX.kr(300, 2500), mul: MouseY.kr(0, 1))}.play;
```
TODO: Animation with scope?
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

## Audio Rate and Control Rate
UGens are typically followed by the letters `.ar` and `.kr`. These stand for Audio Rate and Control Rate.
