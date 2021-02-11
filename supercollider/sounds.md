Wacking a pan/gong-ish sound
```supercollider
(
x = {
	var a, out, blip_freq;

    blip_freq = 0.2; // It sounds more intense when this is higher
    a = Saw.ar(blip_freq) * 1.5; // boring saw sound
    a = a * 0.1 * WhiteNoise.ar; // noisy saw sound
    a = GVerb.ar(a, roomsize: 10, damping: 0.5, drylevel: 2); // noisy saw sound /w reverb
    a = DelayC.ar(a, delaytime: 0.01, feedback: 1.5); // noisy saw sound w/ reverb and THEN delay

    out = a ! 2;
    out = out * 0.2;

}.play
)
```
Not using Saw messes the whole thing up. Use triangle?
