## How it works

A sync generator counts through the 640 by 480 pixels of each frame at 60 Hz. You select the place a worm will appear, and must dodge a duck! The duck learns a 2nd order Markov approximation of you. You have got 4 attempts; each time you are hit the screen flashes and the grass colour changes.

## How to test

Use a 25.175 MHz clock and hold rst_n low for a few cycles, then raise it. The game appears on a monitor connected through a TinyVGA PMOD. Use ui[0], ui[1], ui[2], and ui[3] to select where the worm will go.

## External hardware

A TinyVGA PMOD, a VGA monitor, and four buttons or switches on ui[0], ui[1] and ui[2] and ui[3]
