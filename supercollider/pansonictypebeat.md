Breking down the "Pan Sonic Type Beat"

```supercollider
    n = 12;
	c = LFSaw.ar(50) * Env.perc(1/100,1/10).ar(0, TDuty.ar(Dseq([7/40,7/40,7/40,7/40],2))) * ({ LFNoise1.ar(0.1).range(1,1.01) } ! n);
	10.do{ c = (c.distort + c)*0.7};
	c = c * 1.5;
    c = DelayC.ar(c, delaytime: 0.01, feedback: 1);
    c = FreeVerb.ar(c, 0.8, 0.7);

	d = LPF.ar(Saw.ar([20,47]).sum , XLine.ar(4000,200,0.5)) * Env.perc.ar(0, Impulse.ar(1/16)) * 0.5;
	d = (GVerb.ar( d , roomsize:10, revtime:6) * 200).clip(-1.0,1.0) * 0.3;
```
The ~400BPM sound, with a bit of distortion and reverb thrown in. Note to self: look into `Dseq`.
