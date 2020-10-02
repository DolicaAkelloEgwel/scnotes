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
![](scalingexample.png##)
### `linlin` and friends
`linlin` - Linear to linear.  
`linexp` - Linear to exponential.  
`explin` - Exponential to linear.  
`expexp` - Exponential to exponential.  

TODO: example
```supercollider
a = [1,2,3,4,5,6,7];
a.linexp(1,7,0.01,127).round(1);
```
```
-> [ 1, 2, 3, 4, 5, 6, 7 ]
-> [ 0.0, 0.0, 0.0, 1.0, 5.0, 26.0, 127 ]
```
TODO: How does it decide steps?
## Stopping Individual Synths with `free`
```supercollider
s.boot;

a = { Saw.ar(LFNoise2.kr(8).range(1000,2000), mul: 0.2) }.play;
b = { Saw.ar(LFNoise2.kr(7).range(100,1000), mul: 0.2) }.play;
c = { Saw.ar(LFNoise2.kr(15).range(2000,3000), mul: 0.2) }.play;

a.free;
b.free;
c.free;
```
## The `set` message
Allows changing synth parameters while the synth is still running.
```supercollider
x = {arg freq = 440, amp = 0.1; SinOsc.ar(freq, 0, amp)}.play;

x.set(\amp, 0.01);
x.set(\freq, 778);
x.set(\freq, 920, \amp, 0.1);
x.free;
```
## Audio Buses
Audio buses are used for routing audio signals. SuperCollider has 128 audio buses by default.  
  
Ctrl + M opens the Meter window. It shows the levels of all inputs and outputs. TODO: Screenshot in book doesn't match what I see?
## `Out` and `In` UGens
```supercollider
{Out.ar(1, SinOsc.ar(440, 0, 0.01))}.play;
{Out.ar(0, SinOsc.ar(440, 0, 0.01))}.play;
```
The `Out` UGen routes signals to specific buses. The first argument is the target bus, the second argument is the signal
that you want to send.  
```supercollider
// start the effect
f = {Out.ar(0, BPF.ar(in: In.ar(55), freq: MouseY.kr(1000,5000), rq: 0.1))}.play;
// start the source
n = {Out.ar(55, WhiteNoise.ar(0.5))}.play;
```
The first line declates a synth stored in variable `f` consisting of a Band Pass Filter UGen. A band pass filter
takes any sound as input and filters out all frequences except the region that you want to let through. `In.ar` is
the UGen we use to read from an audio bus; so with `In.ar(55)` being used as input of the `BPF`, any sound that we
send to bus 55 will be passed to the band pass filter.  
  
Note that the first synth does not make any sound at first. It will only make sound when the second line is
evaluated and we send some sound to bus 55. Noise synth -> Bus 55 -> Filter Synth.  
  
The order of execution is important. The example would not work if the lines were swapped.
## Microphone Input
```supercollider
// Takes sound from first input bus
{SoundIn.ar(0)}.play;
// Takes sound from first and second input bus
{SoundIn.ar([0,1])}.play;
// Reverb
{FreeVerb.ar(SoundIn.ar([0,1]), mix: 0.5, room: 0.9)}.play;
```
TODO: get working
