---
layout: post
title: How to Make Mustang Lights Using Digital Logic
author: Ryan Rabello
---

This past quarter I took a course in Digital Logic. I loved learning about how to create systems that solely used simple logic to complete tasks.

## Finished product
`Insert video here`

## Goals

1. Recreate mustang tail-lights with animation. Specific sub goals are as follows.
    * System inputs are left (L), right (R), and brake (B).
    * System outputs are each of the six lights.
    * Appropriate turn signal animation should be enabled when either L or R is high.
    * Turn signal overrides brake.
    * Emergency flashers are on when both L and R are high.
    * B overrides Emergency Flasher.
2. Minimize the number of IC's used in the final version. (We ended up using only 7).


![Mustang Left Turn Signal Animation](http://stream1.gifsoup.com/view1/3851713/2013-mustang-tail-lights-o.gif)

 Here is a GIF of the animation we are going for.

## Procedure

In class we talked about a 7 step procedure to accomplish almost any system design. For the purpose of this post I'm going to only talk about the more prominent features.

### Design

With digital logic there are three things we can work with.

1. **Memory** - In order to make decisions about what lights we are going to output we need to know what lights are currently on. (We are going to use rising edge triggered D-flip flops for this memory.)

2. **Next State Logic** - This is the digital logic that decides what the next state needs to be based off of all the inputs as well as the previous state of the memory.

3. **Output Decoder Logic** - The output decoder takes the memory states (and sometimes the main inputs) and converts those into outputs. This is particularly useful when there are multiple memory states for different outputs.

#### Brute force Design

This method has a bit of memory for each output, which means that there isn't any output decoding. With this method you have an complicated next state logic and therefore a very complicated truth table (6 lights + 3 inputs = 9 variable truth table) which no matter how you slice it would render a very ugly next state logic.

#### Simplifying memory

We recognized the symmetry of the two lights from the start and we knew we could use this to simplify our project. We decided that we would end up using only 3 bits of memory to represent all the lights in the animation. Turns out this 3 bit animation is called a [johnson counter](http://electronics-course.com/johnson-counter).

#### Minimum Logic decoder

Reducing the amount of memory stored has repercussions that need to be taken care of in the decoder. This is the minimum logic for the left right decoder extracted from the truth table.

![Minimum logic output decoder](/images/minimum-decoder-logic.png)

YAY!! We have minimum logic for all of the six LED's. Sure this would be great if we were designing a single IC and we wanted it to go as fast as possible. However, for this project we have limited basic logic gates.

#### Multiplexers to the Rescue

Our final design is the same as the above project but are going to use multiplexers. To find out that the minimum logic of the multiplexer needs to be we have to compress our truth table (or k-map).

### Divide and Conquer

`More content comming`


### Put it all together

`More content comming`


## Conclusion

`More content comming`
