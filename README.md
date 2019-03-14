# Wrapping Up Subroutines

## Learning Goals

- Identify techniques for breaking down large problems: hide work in subroutines
- Identify techniques for breaking down large problems: DRY, prefer subroutines

## Introduction

We've seen how subroutines can help us battle complexity when it threatens to
sink the readability of our programs. We'd like to share some final tips on
using subroutines and also show a "professional" implementation of the PBJ
cutting code for your reference.

### Subroutine Tips

* Methods should perform one task only
* Most methods should be about 5-8 lines
* Methods should have meaningful names
* Methods' parameters should have meaningful names **or** the method should be
  so short and "general purpose" that simple names are appropriate
* Donald Knuth said: "Premature optimization is the root of all evil." There's
  no shame in writing very specific or repetitive code while you're getting it
  to work. Once you have the code working and know how to test it to make sure
  you haven't broken it, _then_ look for opportunities to DRY out the code. Don't
  try to "think DRY" _as you code_. Do a second pass. With version control in
  place, you can feel safe to try and throw away, if necessary.

## Stretch (Optional): How a Professional Would Write This

Most professional programmers think like chefs: prepare the ingredients before
you do the work. In this case, we start the work, `make_pbj_sandwich` and, in
its first step, prepare the ingredient of the bread loaf. A professional
implementation would probably build on this insight and look something like
following. If you see a technique that you're unfamiliar with, try it out in
IRB!

```ruby
# Required to make the Ruby work.
require 'ostruct'
demo_loaf = OpenStruct.new(:type => "light rye", :length => 60)
# (end GIVEN CODE)

def get_two_slices_from_loaf(loaf, width)
  slices = Array.new(loaf.length / width, "slice of #{loaf.type}")
  raise(ArgumentError, "Could not make enough bread from the loaf!") if slices.length < 2
  return slices[0,2]
end

def join_ingredients(i1, i2)
  o = [i1, i2].join(' and ')
  puts "You join #{o}"
  "(#{o})"
end

def make_pbj_sandwich(bread1, bread2, peanut_butter, jelly)
  side1 = join_ingredients(bread1, peanut_butter)
  side2 = join_ingredients(bread2, jelly)
  join_ingredients(side1, side2)
end

make_pbj_sandwich(*get_two_slices_from_loaf(demo_loaf, 2),
  "Poodle Byron's Peanut Butter", "Pappy Burgess' Grape Jelly")
```
