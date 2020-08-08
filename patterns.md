# Patterns

## The Patern Family

### `Pbind`
`Pbind` is a member of the Pattern family in SuperCollider. The capital P in `Pbind` and `Pseries` stands for pattern.
```supercollider
Pbind(\degree, 0).play;
```
This plays the note middle C onces per second. `\degree` refers to scale degrees, and the number 0 means the first scale degree.

White keys to the right or left of middle C can be selected by using positive or negative numbers.

#### `Pbind` Duration
```supercollider
Pbind(\degree, 16, \dur, 0.5).play;
```
This plays a note twice in one second?

#### `Pseq` for `\degree` arguments
```supercollider
Pbind(\degree, Pseq([0,1,2,3,4,5,6,7], 1) \dur, 0.5).play;
```
`Pbind` plays several notes in sequence. Its arguments are a list of notes/numbers, and a number of repitions. `Pbind` is
being used as the input for the `\degree` argument in place of a fixed number.

#### `Pseq` for `\dur` arguments
```supercollider
Pbind(\degree, Pseq([0,1,2,3,4,5,6,7], 5) \dur, Pseq([0.2, 0.1, 0.1, 0.2, 0.2, 0.35], inf)).play;
```
- `\degree` argument causes the entire scale to play five times.
- `\dur` argument causes the notes to have the given durations. The duration is infinite, which causes the duration
  array to be cycled. This means that the last two notes will be played with a duration from the first two elements of
  the duration value array.

