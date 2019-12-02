---
layout: blog
title: 'Advent of Code 2019: Let''s learn a new language'
date: 2019-12-02T15:30:19.198Z
thumbnail: /img/uploads/560.jpg
---
## Prologue

Advent of Code 2019 is an annual competition, in the vein of advent calendars, in which every day a new code challenge is unlocked.  This year I'll be taking AoC as an excuse to learn the basics of two new programming languages -- [Rust](https://julialang.org/) and [Julia](https://julialang.org/).  Both have been seeing increasing usage in bioinformatics-land and I've been meaning to get my feet wet with them.  

AoC is a great opportunity to do this since the challenges start small and build their way up.  With the first few usually needing only the very basics of a language - conditional logic, IO, basic math and string operations.  

As a baseline, I plan on producing answers in Python3 since I do most of my day-to-day data munging and programming with it.  Hopefully the Python code is acceptable "fine" in terms of style and bigO... I am making no such promises about the Rust and Julia solutions.  I'll try and do as much as possible without the use of modules.  It's way more fun that way!

## Python

```python
nums = []
with open('Day1.input', 'r') as fh:
    [nums.append(int(int(l.rstrip())/3.) - 2) for l in fh]
total = sum(nums)
print(f"You need {total} units of fuel, without accounting for fuel mass")
for n in nums:
    while (n/3) > 2:
        n = int(n/3.) - 2
        total += n
print(f"You need {total} units of fuel, accounting for fuel mass")
```

> You need 3311492 units of fuel, without accounting for fuel mass  
> You need 4964376 units of fuel, accounting for fuel mass

## Julia

```julia
total = 0
nums = Vector{Int}()
open("Day1.input") do fh
    for l in eachline(fh)
        push!(nums, div(parse(Int,l), 3) - 2)
    end
end
tot = sum(nums)
println("You need $tot units of fuel, without accounting for fuel mass")
for n in nums
    while div(n, 3) > 2
        n = div(n, 3) - 2
        global tot += n
    end
end
println("You need $tot units of fuel, accounting for fuel mass")
```
