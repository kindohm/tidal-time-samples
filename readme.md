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

## long breaks

```
bps (180/120)

let sixteenths = [0, 0.0625, 0.125, 0.1875, 0.25, 0.3125, 0.375, 0.4375, 0.5, 0.5625, 0.625, 0.6875, 0.75, 0.8125, 0.875, 0.9375]

d1 $ every 2 (density 2) $ degradeBy 0.5 $ sound "break*8"
|=| cut "1"
|=| gain "1.2"
|=| begin (choose sixteenths)
```

## long loops  

### striate

### loopAt

## short samples

### unit and speed synth params

### begin and end variation

### other synth param variation

## re-sampling
