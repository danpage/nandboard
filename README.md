# NANDboard: hands-on Boolean algebra

<!--- -------------------------------------------------------------------- --->

## History

Starting in the 2012/13 academic year, the
[Computer Science Department](http://www.cs.bris.ac.uk)
at the
[University of Bristol](http://www.bris.ac.uk)
changed how the Undergraduate-level, 1st year (or "freshman") Computer
Architecture unit was delivered.  Although it *always* had a practical
emphasis, there was a view it should be even more hands-on.
There were various motivations, included the fact that
a) by doing so the topic could be more engaging,
   but also
b) it seeds an ethos and skills that are of general use: for example,
   it could mean students participate more actively in
   [maker-like](http://en.wikipedia.org/wiki/Maker_culture),
   hardware-based (versus software-only) projects.

The NANDboard, whose original concept and design was due to
[Simon Hollis](http://www.cs.bris.ac.uk/home/simon),
was among various innovations introduced; Simon left at the end of the
2014/15 academic year, ~~prompting~~ forcing me to learn the basics of
PCB design and subsequently revise his initial NANDboard version.

<!--- -------------------------------------------------------------------- --->

## Concept

Although fundamentally important in Computer Science,
[Boolean algebra](http://en.wikipedia.org/wiki/Boolean_algebra)
is a notoriously dry topic.  The problem is exacerbated when hands-on 
experience amounts to solving paper-and-pencil exercises; the typical
result is for students to be increasingly uninterested and disengaged.
The underlying causes are varied, and differ from student to student.
However, anecdotally at least, the following are common:

- There is a disconnection between theory and practice, in the sense
  it is unclear how Boolean algebra directly relates to intuitively 
  useful forms of computation;
  this typically leads to students disengaging,
  based on the view that said theory has no practical use (to them).
- Paper-and-pencil exercises are of a necessarily small scale, which
  can mean 
  [toy problems](http://en.wikipedia.org/wiki/Toy_problem)
  dominate; 
  this typically leads to students disengaging, e.g., because they
  can easily solve said problems so avoid any deeper investigation
  of physical constraints and properties, and unusual designs
  (e.g., a [C-element](https://en.wikipedia.org/wiki/C-element)).
- In part due to the wealth of resources available, modern students 
  are used to and excited by the immediacy of software development;
  this is often direct motivation for studying Computer Science in 
  the first place, with Boolean algebra feeling like a regression 
  towards Mathematics (which, for some, is less popular).

Put another way, this approach is similar, by analogy, to learning
[C](http://en.wikipedia.org/wiki/C_(programming_language))
by studying the language and 
["hello world"](https://en.wikipedia.org/wiki/"Hello,_World!"_program)
style programs *without* ever actually compiling and executing them.

An obvious alternative is to connect theory and practice directly, by
supporting genuinely hands-on, experimental tasks.  One way to do so
might be to equip each student with a breadboard and some
[7400 series](https://en.wikipedia.org/wiki/List_of_7400_series_integrated_circuits)
ICs.  However, for us at least, this presented some problems:
a) large cohort sizes
   (of say 200+ students)
   make the logistics involved quite challenging,
b) said cohorts are typically unfamiliar with, and sometimes have an
   outright dislike for electronics.
The NANDboard attempts to manage these problems.  Conceptually, it is 
just a USB-powered breadboard pre-populated with NAND gates: it could
be viewed as a form of NAND-only
[PLA](http://en.wikipedia.org/wiki/Programmable_logic_array),
where implementation of a Boolean expression (cf. programming the PLA)
amounts to connecting pin headers (i.e., the gate inputs and outputs)
using jumper wire.  There are, of course, some gratuitous
[blinkenlights](http://en.wikipedia.org/wiki/Blinkenlights)
to visualise the inputs and outputs.

<!--- -------------------------------------------------------------------- --->

## Design

Motivated in part by observing how students use them, the NANDboard 
design has gone through several revisions as is illustrated below:

Revision | Image                                                                             | Design
:------: | :-------------------------------------------------------------------------------: | :-----------
B        | <a href='./rev_b/image/pcb.jpg'><img src='./rev_b/image/pcb.jpg' width='200'></a> | [files](./rev_b)
C        | <a href='./rev_c/image/pcb.jpg'><img src='./rev_c/image/pcb.jpg' width='200'></a> | [files](./rev_c)
D        | <a href='./rev_d/image/pcb.jpg'><img src='./rev_d/image/pcb.jpg' width='200'></a> | [files](./rev_d)
E        | <a href='./rev_e/image/pcb.jpg'><img src='./rev_e/image/pcb.jpg' width='200'></a> | [files](./rev_e) [user guide](./rev_e/README.md)
F        | <a href='./rev_f/image/pcb.jpg'><img src='./rev_f/image/pcb.jpg' width='200'></a> | [files](./rev_f) [user guide](./rev_f/README.md)



[schematic](./rev_e/nandboard.sch) (plus [PDF](./rev_e/nandboard.pdf)), [board](./rev_e/nandboard.brd), [BOM](./rev_e/nandboard.csv), [OSH Park (PCB)](http://www.oshpark.com/shared_projects/4jmm6cXa), [Octopart (BOM)](http://www.octopart.com/bom-tool/1i1poH1i) |
[schematic](./rev_d/nandboard.sch) (plus [PDF](./rev_d/nandboard.pdf)), [board](./rev_d/nandboard.brd), [BOM](./rev_d/nandboard.csv), [OSH Park (PCB)](http://www.oshpark.com/shared_projects/KMYK0yGx), [Octopart (BOM)](http://www.octopart.com/bom-tool/RcuUFO2Y)         |

<!--- -------------------------------------------------------------------- --->

## Acknowledgements

Later revisions 
(e.g., rev. F) 
were designed and manufactured with generous support from 
[Elliptic Systems](https://elliptic-systems.com).

<!--- -------------------------------------------------------------------- --->
