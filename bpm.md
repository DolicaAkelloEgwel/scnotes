```supercollider
~bpm = 400;
x = {LFSaw.ar(50).dup * LFNoise2.ar * Pulse.ar(~bpm/60, 0.01,2).distort.distort.distort}.play;
x.free;
```
