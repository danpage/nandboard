<!--- -------------------------------------------------------------------- --->

# High-level structure

At a high level, (the top-side of) a given 
NANDboard
is organised into a set of somewhat groups (or regions) reflected 
by annotation on the 
[PCB](https://en.wikipedia.org/wiki/Printed_circuit_board):

```
+----------+----------+----------+----------+
|   button |     NAND |     NAND |    power |
|    group |    group |    group |    group |
|          |       #0 |       #1 |          |
|          +----------+----------|          |~~~~ USB
|          |     NAND |     NAND |          |
|          |    group |    group |          |
|          |       #2 |       #3 |          |
+----------+----------+----------+----------+
```

Each group designed to support a specific purpose, as explained
in detail below.  Again
at a high level,
however, use of the 
NANDboard 
can be summarised as follows.  Imagine you are tasked with using 
a
NANDboard
to implement some 4-input, 1-output Boolean function
`R = f( X_0, X_1, X_2, X_3 )`
To do so, the idea is you

- use the  input group  to model (and   control) the  input, 
- use the   NAND groups to implement `f` by decomposing it into a NAND-based expression,
- use the output group  to model (and visualise) the output, 
  
using
[jumper wire](https://en.wikipedia.org/wiki/Jump_wire)
to form connections to inputs, outputs, and between intermediate 
signals.

<!--- -------------------------------------------------------------------- --->

# Low-level detail

### The power    group

The  power  group houses
a micro-B [USB](https://en.wikipedia.org/wiki/USB) connector,
which
  supplies the 
  NANDboard 
  with power from some host (e.g., a workstation).

### The input    group

Viewed from left-to-right, 
the   input group comprises

- 4 [switches](http://en.wikipedia.org/wiki/Switch) (or buttons),
  and
- an 8x2          [pin header](https://en.wikipedia.org/wiki/Pin_header).

so can be thought of conceptually as the following block diagram:
   
```
switches           pins 
 __|__         _____|_____ 
/     \       /           \
               +-----+-----+
+-----+       | X_0 | X_0 |
| X_0 | ~~~>  +-----+-----+
+-----+       | X_0 | X_0 |
              +-----+-----+
+-----+       | X_1 | X_1 |
| X_1 | ~~~>  +-----+-----+
+-----+       | X_1 | X_1 |
              +-----+-----+
+-----+       | X_2 | X_2 |
| X_2 | ~~~>  +-----+-----+
+-----+       | X_2 | X_2 |
              +-----+-----+
+-----+       | X_3 | X_3 |
| X_3 | ~~~>  +-----+-----+
+-----+       | X_3 | X_3 |
              +-----+-----+
```

The basic idea is that
each switch is connected to a group of 4 pins:
the state of each group of pins (i.e., 0 or 1)
is determined by
that of the associated switch,
so when the switch is pressed (resp. not pressed) the pins will be 1 (resp. 0).

## The NAND     group(s)

Viewed from left-to-right, 
each NAND   group comprises

- an 8x1 constant [pin header](https://en.wikipedia.org/wiki/Pin_header),
- an 8x2    input [pin header](https://en.wikipedia.org/wiki/Pin_header),
- an [IC](http://www.ti.com/lit/gpn/sn74ac00) that houses 4 [NAND gates](https://en.wikipedia.org/wiki/NAND_gate),
- an 8x2   output [pin header](https://en.wikipedia.org/wiki/Pin_header).
  and
- 4 [LEDs](https://en.wikipedia.org/wiki/Light-emitting_diode).

so can be thought of conceptually as the following block diagram:

```
constant pins   input pins                NAND gates             output pins         LEDs
 _____|_____    _____|_____        ___________|__________        _____|_____        __|__
/           \  /           \      /                      \      /           \      /     \

+-----------+  +-----+-----+      +----------------------+      +-----+-----+
|     1     |  | x_0 | x_0 | ~~~> |                      |      | r_0 | r_0 |      +-----+
+-----------+  +-----+-----+      | r_0 = ~( x_0 & y_0 ) | ~~~> +-----+-----+ ~~~> | r_0 |
|     1     |  | y_0 | y_0 | ~~~> |                      |      | r_0 | r_0 |      +-----+
+-----------+  +-----+-----+      |                      |      +-----+-----+
|     1     |  | x_1 | x_1 | ~~~> |                      |      | r_1 | r_1 |      +-----+
+-----------+  +-----+-----+      | r_1 = ~( x_1 & y_1 ) | ~~~> +-----+-----+ ~~~> | r_1 |
|     1     |  | y_1 | y_1 | ~~~> |                      |      | r_1 | r_1 |      +-----+
+-----------+  +-----+-----+      |                      |      +-----+-----+
|     1     |  | x_2 | x_2 | ~~~> |                      |      | r_2 | r_2 |      +-----+
+-----------+  +-----+-----+      | r_2 = ~( x_2 & y_2 ) | ~~~> +-----+-----+ ~~~> | r_2 |
|     1     |  | y_2 | y_2 | ~~~> |                      |      | r_2 | r_2 |      +-----+
+-----------+  +-----+-----+      |                      |      +-----+-----+
|     1     |  | x_3 | x_3 | ~~~> |                      |      | r_3 | r_3 |      +-----+
+-----------+  +-----+-----+      | r_3 = ~( x_3 & y_3 ) | ~~~> +-----+-----+ ~~~> | r_3 |
|     1     |  | y_3 | y_3 | ~~~> |                      |      | r_3 | r_3 |      +-----+
+-----------+  +-----+-----+      +----------------------+      +-----+-----+
```
   
The basic idea is that:

- Each group houses 4 replicated instances of the same structure,
  the `i`-th of which computes 
  `r_i = ~( x_i & y_i )`.
  We use on the 0-th, top-most instance as an example throughout
  the following.  

- The computation of
  `r_0 = ~( x_0 & y_0 )`
  relates to the top 4 pins (i.e., top 2 rows) of both the input
  and output pins headers: the input pins marked `x_0` and `y_0` 
  provided an input to the NAND gate, which produces a result 
  reflected on the output pins marked `r_0`.  
  Each output pin is also connected to an LED, allowing the state
  (i.e., 0 or 1) to be visualised.

- Note there are 2 pins marked `x_0` and `y_0` on the input pin
  header: since they are connected together, either of the 2 pins
  (i.e., the left- *or* right-hand pin marked `x_0`) can be used 
  to provide the associated input.  Likewise, there are 4 pins
  marked `r_0` on the output pin header: the NAND gate output is
  replicated on each of those pins.

- Each input pin is 
  [pulled-down](http://en.wikipedia.org/wiki/Pull-up_resistor), 
  meaning that `x_0` and `y_0` are 0 and `r_0` is 1 by default.
  However, an input pin can be freely connected (via jumper wire)
  to any other

  - constant           pin,
  - input group        pin,
  - NAND  group input  pin,
  - NAND  group output pin

  elsewhere on the NANDboard.

- Since each input pin is 0-by-default, the constant pins can be
  used to "override" this.  Imagine that rather than
  `r_0 = ~( x_0 & y_0 )`,
  you need to compute
  `r_0 = ~( x_0 & 1   )`
  for some reason: a reasonable approach is to connect the `y_0` 
  input pin of the NAND gate to one of the 1-by-default constant
  pins.

- The NAND groups and hence operators are independent, meaning 
  you can form inter- and intra-group connections (i.e., inside 
  one group and between two groups).

<!--- -------------------------------------------------------------------- --->
