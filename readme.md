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
```

*Problems with this approach:*

- Require a specific `bps`
- Require precise placement of notes in the sample


### loopAt

```
bps (170/120)

d1 $ loopAt 4 $ sound "calm"
|=| gain "1.2"
```

### striate

```
d1 $ jux (iter 4) $ slow 8 $ (striate' 128 (1/100) $ sound "calm")
|=| speed "[2, 3 5 4]"
|=| gain "1.2"
```



## short samples

### unit and speed synth params

### begin and end variation

### other synth param variation

## re-sampling
