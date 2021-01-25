## Basics

### Hello World
```supercollider
"Hello World".postln;
```
Press Ctrl + Enter to evaluate.

### Server and Language

![](statusbar.png)

The interpreter is active by default. The server needs to be enabled.

The server makes sounds. The language (or client/interpreter) is used to control the server.

### Starting/Stopping A Server
#### Boot The server
Ctrl + B

### Making Sounds
#### Boring Sine Wave
```supercollider
{SinOSc.ar}.play;
```
#### Changing the Volume
```supercollider
s.volume.gui;
```
#### Stopping Sound
Ctrl + .
#### Goofy Sci-Fi Robot Sound Effect Sine Wave
```supercollider
{SinOsc.ar(LFNoise0.kr(10).range(500, 1500), mul: 0.1)}.play;
```
#### "Geiger Counter"/Space/Arctic Sound
```supercollider
{RLPF.ar(Dust.ar([12,15]), LFNoise1.ar([0.3,0.2]).range(100,3000),0.2)}.play;
```
### Code Blocks
Everything inside the brackets is evaluated.
```supercollider
(
// A little poem
"Today is Sunday".postln;
"Foot of pipe".postln;
"The pipe is made of gold".postln;
"It can beat the bull".postIn;
)
```
As long as the cursor is anywhere within the parentheses, a single Ctrl+Enter will evaluate all of the lines.
### Recording
```supercollider
// QUICK RECORD
// Start recording:
s.record;
// Make some cool sound
{Saw.ar(LFNoise0.kr([2, 3]).range(100, 2000), LFPulse.kr([4, 5]) * 0.1)}.play;
// Stop recording:
s.stopRecording;
// Optional: GUI with record button, volume control, mute button:
s.makeWindow;
```
### Variables
#### Global Variables
```supercollider
a = "Hello, World"; // a string of characters
b = [0, 1, 2, 3, 5]; // a list
c = Pbind(\note, Pwhite(0, 10), \dur, 0.1); 
a.postln; // post it
b + 100; // do some math
c.play; // play that Pbind
d = b * 5; // take b, multiply by 5, and assign that to a new variable

~myFreqs = [415, 220, 440, 880, 220, 990];
~myDurs = [0.1, 0.2, 0.2, 0.5, 0.2, 0.1];
Pbind(\freq, Pseq(~myFreqs), \dur, Pseq(~myDurs)).play;
```
Tilde is used for longer variable names. Variable names must begin with lower case letters.
#### Local Variables
```supercollider
// Local variables: valid only within the code block.
// Evaluate the block once and watch the Post window:
(
var apples = 4, oranges = 3, lemons = 8, bananas = 10;
["Citrus fruits", oranges + lemons].postln;
["Non−citrus fruits", bananas + apples].postln;
"End".postln;
)
```
