Time-Constrained Samples in TidalCycles
=======================================

> Prepared for a TidalCycles workshop at the 2nd International Conference on
> Live Coding, 2016-10-12, Hamilton, ON, Canada.

This is an outline of techniques and features you can use with the TidalCycles
live-coding environment to work with rhythmic or "time-constrained" audio
samples.

## What is a Time-Constrained Sample?

A time-constrained sample can be a sample that:

- has a specific duration
- has a tempo-specific rhythm that lasts multiple beats

## long loops  

### trigger at different points

Good for precise, rhythmic loops, like breakbeats.

```
bps (180/120)

let steps = take 16 [0,0.0625..]

d1 $ every 2 (density 2) $ degradeBy 0.5 $ sound "break*8"
|=| cut "1"
|=| gain "1.2"
|=| begin (choose steps)
```

Can also work for melodic sequences:

```
bps (170/120)

let steps = take 16 [0,0.0625..]

d1 $ every 2 (density 2) $ degradeBy 0.5 $ sound "alone*8"
|=| cut "1"
|=| gain "1.2"
|=| begin (choose steps)
|=| speed "{1 1 1 1 2}%4"
```

*Advantages:*

- Can work with a long sample without cutting it up

*Disadvantages:*

- Requires a specific `bps`
- Requires precise placement of notes in the sample
- Requires a `steps` list
- Requires `cut`

### loopAt

```
bps (170/120)

d1 $ loopAt 4 $ sound "calm"
|=| gain "1.2"
```

*Advantages:*

- Very fast method for time-stretching long loops


### striate

```
d1 $ jux (iter 4) $ slow 8 $ (striate' 128 (1/100) $ sound "calm")
|=| speed "[2, 3 5 4]"
|=| gain "1.2"
```

```
d1 $ every 3 (|*| speed "-1") $ slow 8 $
(spread' (striate' 256) (scale 0.01 0.05 $ slow 1.25 sine1) $ sound "break")
|=| speed "[1 0.5, {2 3 4}%2]"
|=| gain "1.2"

d1 $ every 3 (|*| speed "-1") $ slowspread (slow) [8,16,4,8,32] $
(spread' (striate' 256) (scale 0.01 0.05 $ slow 1.25 sine1) $ sound "break")
|=| speed "[1 0.5, {2 3 4}%2]"
|=| gain "1.2"
```

*Advantages:*

- extreme granualization control
- sequence <-> grain alignment creates interesting effects
- high-risk / high-benefit live-coding :D :D :D :D

*Disadvantages:*

- high-risk / high-benefit live-coding


## short samples

If you have the patience and means to do a little slicing, try creating
smaller units of sequences for more control and options.

### unit and speed synth params

With a rhythmic melodic sequence:

```
d1 $ s "{seq3 seq2 [~ seq3] ~ seq2 [~ seq3] ~}%2"
  # n (slow (4/3) $ run 9)
  # gain "1.2"
  # unit "c"
  # speed "1"
```

With chopped up drum breaks:

```
d1 $ s "funky*4"
  # n (irand 8)
  # gain "1.2"
  # unit "c"
  # speed "4"

```

> NOTE: when slicing up a drum break into individual samples  to use with
> "unit" and "speed", just make sure that each slice is for the same number
> of beats.

> TIP: for drum break slices, try slicing at quarter or half cycle durations.
> Let one sample contain multiple drum hits (but make sure each sample is the
> same number of beats).

### begin variation

```
d1 $ s "think*8"
  # n (irand 8)
  # gain "1.2"
  # unit "c"
  # speed "4"
  # begin (choose [0.5,0])
  # cut "1"
```

## re-sampling
