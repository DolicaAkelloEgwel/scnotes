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

`SinOsc.ar` creates a unit generator that runs at the audio rate. If the computer is running at the common 
sampling rate of 44100 Hz, the sine oscillator will generate 44100 samples per second to send to the 
loudspeaker.

`SinOsc.kr` creates a unit generator that runs at the control rate. The job of generating the samples is
performed by the server. The amount of numbers generated per second with `.kr` is much smaller. The signal
generated with `.kr` does not go to the loudspeaker. Instead it is normally used to control the parameters of 
other signals -- for example, the `Mouse.kr` in the theremin was controlling the frequency of `SinOsc`.

❗UGens generate numbers. Some of these numbers become sound signals while others become control signals.

```supercollider
{SinOsc.ar(freq: SinOsc.kr * 200, mul: SinOsc.kr(200))}.play;
```

*Unipolar Ugens* generate numbers between 0 and 1.  
*Bipolar UGens* generate numbers between -1 and +1.

### `.poll` output
```supercollider
{SinOsc.kr(1).poll}.play;
```
This doesn't generate any sound.
```
-> Synth('temp__18' : 1000)
UGen(SinOsc): 0.00837747
UGen(SinOsc): 0.594541
UGen(SinOsc): 0.953611
UGen(SinOsc): 0.948435
UGen(SinOsc): 0.58099
UGen(SinOsc): -0.0083736
UGen(SinOsc): -0.594538
UGen(SinOsc): -0.95361
UGen(SinOsc): -0.948436
UGen(SinOsc): -0.580993
UGen(SinOsc): 0.00836973
```

## Scaling Ranges
### The `range` method
```supercollider
{SinOsc.ar(freq: LFNoise0.kr(5).range(500, 1500), mul: 0.1)}.play;
```
`LFNoise0` is a bipolar UGen. Scaling the output of `LFNoise0.kr` to set the frequency of `SinOsc.ar` allows it 
to be used for "hearable" frequencies.

### `mul` and `add` arguments
Most UGens have `mul` and `add` arguments.
```supercollider
{SinOsc.kr(1).range(100,200).poll}.play;
{SinOsc.kr(1, mul: 50, add: 150).poll}.play;
```
These produce the same result.
