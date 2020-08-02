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
