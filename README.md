# NANDboard: hands-on Boolean algebra

## History

Starting in the 2012/13 academic year, the
[CS Department](http://www.cs.bris.ac.uk/)
at the
[University of Bristol](http://www.bris.ac.uk/)
changed how the Undergraduate-level, 1st year (or "freshman") Computer
Architecture unit was delivered.  Although it *always* had a practical
emphasis, there was a view it should be even more hands-on: various
motivations included the fact that
a) by doing so the topic could be more engaging,
   but also
b) it seeds an ethos and skills that are of general use: for example,
   it could mean students participate more actively in
   [maker-like](http://en.wikipedia.org/wiki/Maker_culture)
   projects.
   
Among various innovations was the NANDboard, designed by
[Simon Hollis](http://www.cs.bris.ac.uk/home/simon/).
The concept and design are both simple.  In short, Boolean algebra is
a notoriously dry topic when presented via paper-and-pencil exercises;
in addition, it's not *always* clear to students how this relates to
physical computation.  So to *physically* compute Boolean expressions,
one approach might be to get a breadboard and some
[7400 series](https://en.wikipedia.org/wiki/List_of_7400_series_integrated_circuits)
chips, then hook them up so circuit replicates expression.  At least
for us (doing so might work perfectly well in another context), this
presented some problems:
a) unfamiliarity, and sometimes outright dislike of electronics,
   plus
b) the pure logistics involved in supporting large (150 or so) class
   sizes.
The NANDboard attempts to solve, or at least lessen these problems: it
is, basically, a USB-powered breadboard pre-populated with NAND gates.
Or, if you prefer, a kind of NAND-only
[PLA](http://en.wikipedia.org/wiki/Programmable_logic_array)
with the planes and fuses replaced by pin headers and jumper wire.
The gate inputs and outputs are connected to pin headers to allow
formation of circuits via jumper wire; each output also drives an LED,
partly to provide some gratuitous
[blinkenlights](http://en.wikipedia.org/wiki/Blinkenlights)
but mainly to visualise the result.

## Design

The design has gone through several revisions, illustrated below:

Revision | Photograph                                                                                        | Design files
:------: | :-----------------------------------------------------------------------------------------------: | :----------------------------------------------------------------------------:
B        | <a href='./image/nandboard-rev_b_r.jpg'><img src='./image/nandboard-rev_b_r.jpg' width='200'></a> |
C        | <a href='./image/nandboard-rev_c_r.jpg'><img src='./image/nandboard-rev_c_r.jpg' width='200'></a> |
D        | <a href='./image/nandboard-rev_d_r.jpg'><img src='./image/nandboard-rev_d_r.jpg' width='200'></a> | [schematic](./nandboard.sch), [board](./nandboard.brd), [BOM](./nandboard.csv)

Simon left the University at the end of the 2014/15 academic year, so
when I needed more boards (re)designing my own version was the ideal
opportunity to learn about PCB design then open-up the end result:
this repository, and revision D is the outcome of doing that.

I used [Eagle](http://www.cadsoftusa.com/) 7.2.0, plus some 3rd-party
libraries for

- the surface mount [pin headers](http://drazzy.com/e/eaglelibs.shtml),
- the [switches](http://github.com/LonghornEngineer/PP_Eagle_Part_Libraries/blob/master/Libraries/PP_Electromechanical.lbr),
  and
- the [USB connector](http://github.com/daspilker/daspilker-eagle-library).

[CircuitHub](http://circuithub.com/)
did the prototype and production fabrication runs: I really can't say
enough good things about them or the service they've built.  Among a
host of great features, the 
[design](https://circuithub.com/projects/danpage/nandboard)
is available online with a pre-populated BOM.  So *if* you want one,
however unlikely that is, you can actually order a board with just a
few clicks *or* download the
[Gerber files](http://en.wikipedia.org/wiki/Gerber_format)
(which is why they aren't included in here).

As an aside, there are some cosmetic differences between the revision
D photograph shown above and the corresponding board design files:

- I eventually worked out how to import images onto the silk screen
  in Eagle, so decided to add a logo for the
  [license](http://creativecommons.org/licenses/by-sa/4.0/),
  and
- I *thought* calling the switches "push buttons" would be easier to
  understand, but apparently not so reverted this.

## "User Manual"

At a high level, the board looks like

```
+-----+----------+----------+---+
|  s  |          |          | U |
|  w  | NAND     | NAND     | S |
|  i  | group #1 | group #3 | B |
|  t  |          |          |   |
|  c  +----------+----------+   |
|  h  |          |          |   |
|  e  | NAND     | NAND     |   |
|  s  | group #2 | group #4 |   |
|     |          |          |   |
+-----+---------------------+---+
```

provided you have it the right way up, noting that

- the  left-hand end of the board houses 
              the switch group,
- the         middle of the board houses 4 identical component groups,
  each termed a   NAND   group,
  and
- the right-hand end of the board houses a micro-B USB connector which
  acts as a power supply.

#### Switch group

Viewed from left-to-right, the  switch group comprises

-      4 switches,
  and
- an 8x2 pin header.

and can be thought of conceptually as the following block diagram:

```
           +-----+-----+
+-----+    | s_0 | s_0 |
| s_0 |    +-----+-----+
+-----+    | s_0 | s_0 |
           +-----+-----+
+-----+    | s_1 | s_1 |
| s_1 |    +-----+-----+
+-----+    | s_1 | s_1 |
           +-----+-----+
+-----+    | s_2 | s_2 |
| s_2 |    +-----+-----+
+-----+    | s_2 | s_2 |
           +-----+-----+
+-----+    | s_3 | s_3 |
| s_3 |    +-----+-----+
+-----+    | s_3 | s_3 |
           +-----+-----+
```

The basic idea is simple: each switch is connected directly to 4 switch
pins on the 8x2 pin header: if the switch is pressed those pins are 1,
otherwise they are 0.

#### NAND group

Viewed from left-to-right, each NAND   group comprises

- an 8x1 pin header,
- an 8x2 pin header,
- a  4-gate NAND chip plus 4 LEDs,
  and
- an 8x2 pin header

and can be thought of conceptually as the following block diagram:

```
+-----+    +-----+-----+                          +-----+-----+
|  1  |    | x_0 | x_0 |                          | r_0 | r_0 |
+-----+    +-----+-----+   r_0 = ~( x_0 & y_0 )   +-----+-----+
|  1  |    | y_0 | y_0 |                          | r_0 | r_0 |
+-----+    +-----+-----+                          +-----+-----+
|  1  |    | x_1 | x_1 |                          | r_1 | r_1 |
+-----+    +-----+-----+   r_1 = ~( x_1 & y_1 )   +-----+-----+
|  1  |    | y_1 | y_1 |                          | r_1 | r_1 |
+-----+    +-----+-----+                          +-----+-----+
|  1  |    | x_2 | x_2 |                          | r_2 | r_2 |
+-----+    +-----+-----+   r_2 = ~( x_2 & y_2 )   +-----+-----+
|  1  |    | y_2 | y_2 |                          | r_2 | r_2 |
+-----+    +-----+-----+                          +-----+-----+
|  1  |    | x_3 | x_3 |                          | r_3 | r_3 |
+-----+    +-----+-----+   r_3 = ~( x_3 & y_3 )   +-----+-----+
|  1  |    | y_3 | y_3 |                          | r_3 | r_3 |
+-----+    +-----+-----+                          +-----+-----+
```

The basic idea is:

- The NAND gates accept input from the left-most 8x2 pin header, and
  produce output on the right-most 8x2 pin header; each output is
  mirrored by an associated LED.
- For example, the top-most LED relates to the top-most 4 output pins
  labelled `r_0` which are driven by a NAND gate which computes

  ```
  r_0 = ~( x_0 & y_0 )
  ```

  using inputs on the top and second from top 2 input pins labelled
  `x_0` and `y_0`.
- Each input pin is pulled-down, i.e.,  each `x_i` and `y_i` is 0 and
  hence each `r_i` is 1 by default.  However, the input pins can be
  freely connected (via jumper wire) to

  - pins on the 8x1 pin header that supply a constant 1,
  - switch pins,
  - input  pins
    or
  - output pins.

## Possible Improvements

- Although I used Eagle for the design, I didn't have a good reason
  beyond the fact there were people around who knew it and so could
  help out.  In hindsight it would have been more useful to use
  [KiCad](http://www.kicad-pcb.org/)
  or
  [CircuitMaker](http://www.circuitmaker.com/),
  for example; porting the design might be worthwhile in the longer
  term.
- Clearly one could produce a NORboard equivalent: you don't need a
  separate design really, because replacing the
  NAND-based SN74AC00DR
  components
  with
   NOR-based SN74HCT02D
  should be enough.
- I'm in love with, and in awe of, the beautiful PCBs designed by
  [Boldport](http://www.boldport.com/).
  I'm not sure what it'd look like, but you could argue it'd be
  interesting to explore a more creative, aesthetically pleasing 
  designed NANDboard along similar lines.
- Like the predecessors, the revision D board includes a dedicated
  8x1 pin header for constant 1 in *every* NAND group.  There is an
  argument this is overkill: it'd make the board smaller, plus make
  the description a bit easier, if a single such header is combined
  into the switch group to form an "input group".

