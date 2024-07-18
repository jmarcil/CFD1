# CFD1
Connection flow diagrams, also called CFDs or threat modeling diagrams. My special twist on the worldwidely popular DFDs.

## Goal
Many people have presented various different ways to craft data flow diagrams over the years. This page is a fork of [Adam Shostack's "v3 DFD"](https://github.com/adamshostack/DFD3) and defines an alternative notation named "Connection Flow Diagram (CFD)". Simply, this replaces data flows with connections flows between processes, but don't worry it also add complexity due to added flexiblity of some symbols.

### Symbols/Elements used

| Element | Symbol | Discussion |
|---------|--------|------------|
| External entity| ▭ | A sharp-cornered rectangle. Anything interacting with the system outside your control or the realm of computing. Examples include people and user-agents executing on the behalf of people.
| Process| ◯ | A circle.  Any running code, including compiled, scripts, shell commands, SQL stored procedures, et cetera.
| Data store|  = 🛢️ | A double line or cylinder (drum). Anywhere data is stored, including files, databases, shared memory, bucket, cookies, etc.
| Connection flows| → | An arrow. All the ways that processes can connect to data stores or each others.
| Data flows| ⇢ | A dotted arrow. All the ways that data can flow between entities, processes and data stores.
| Trust boundary | . . . | A closed shape drawn with a dashed line. Usually a box.
| Cloud | ☁️ | A cloud (like in cloud computing). Anything that is not under your control and is not a direct user. Usually outbound connection but can be inbound like with callbacks and hooks.


## Definition
1. A CFD uses more than 6 symbols up to the flexiblity of the author.
   1. A rectangle represents an external entity, a person or code outside your control. 
   2. A circles represents a process. They're connected by arrows, which can be flat for connections and dotted for data flows.
   3. Data stores are represented by cylinder (drums).
   4. Connection flows are represented by arrows. These are usually one way (uni-directional).
   5. Data flows are optionally used and represented by dotted arrows. These are usually one way (uni-directional) to indicate the flow direction of the data.
   6. A trust boundary is a closed shape, usually a box. Can also be a demi-circle, which should be oriented like a protective shield to denotate a boundary that is to be crossed over but we are not certain what it encompass.
   7. A double circle can be a temporary abstraction of multiple processes you have the control of.
   8. A cloud is a process that you don't have the control over and is most likely composited of many processes.
2. All lines are solid, except those used for trust boundaries, which are dashed and for dotted arrows to indicate data flows.
3. It must not* depend on the use of color, but can use color for additional information.
4. All elements should have a label. They can optionally have tags of them to further add details about target implementation. For example a SQL database named "mydata" hosted on postgres can be labelled "postgres mydata".
5. Adam had a rule of: _You may have a context diagram if the system is complex. One is not required._ which I agree with, but my guideline on complexity is: if your diagram is deemded to have too many elements to the eyes (more than 10 maybe, or definately more than 20), it means that your scope is too big and you should break down into multiple diagrams.
6. Flexible notations should be used uniformally everywhere in the diagram. If you choose a cylider for data all data should be cylinder. If you call it a drum, you should call any cylinder a drum (I'll be watching you Adam 👀, a AA battery is the form of a drum).
</ol>
* Must, must not, should, should not are used per IETF norms.



# Rationales

DFD3, which is what CFD1 is based on, is what people have come to call 'opinionated.' The design is aggressively simple to prioritize easy learning and use over expressiveness. It's just enough information to enable threat modeling and put type information into the picture.

## Rounded rectangles
Adam said that Rounded rectangles _are more space-efficient in a large diagram than circles_, which I agree with. However most of the documentation and tools I've seen are using circle. Also, have you tried to actually draw a rounded rectangle on a whiteboard? For me and my band hand writing, it ends up being either a really ugly circle or a double lined between parentheis (<ins>‾</ins>) 😅.

## Boxed boundaries
Clearly show what's inside, in a way that arcs often fail to do. Dashes and dots are clearly different from other elements and reproduce clearly with black and white printers.

## Connection flow arrows
Are easier to draw and be understood than having two arrow heads per data flow. They show initiation of a connection, which is joyful and simplier than DFD3.

## Dotted data flow arrows
Are used when the emphasis on a given data flow is important to the message the diagram is trying to convey. Unlike a regular DFD, they are optional as the CFD are the core of the diagrams and required everywhere there's a conneciton happening.

## No "Complex Processes"
Adam said: _Some approaches refer to complex processes, indicated by a doubled (concentric) circle. When to use them was never made clear, and so they're a bit of a distraction and I recommend against them._ I actually embrace them for drafting but blow them out into very big circle where little circles are giving away the processes that were initially abstracted. I also like to use clouds for something we don't control and we have no idea how many actual processes are happening (but we can still connect or send data to it).

## Cylinders (Drums) vs double lines
Adam said: _The drum is easier to draw and label with software drawing tools. The parallel lines in Yourdon and other early DFDs are trivial to draw using a physical stencil: You just draw the top and bottom of a rectangle. But with software, you draw the two lines, you add text, you maybe align the text, then you group them. So with software, adding a drum to a diagram is 2 actions (draw drum, label) while the classic doubles lines is 4-5._ Pretty much all super simple software I use for threat modeling are having double lines as an element.. which makes these argument moots. However, I do tell people that the cylinders (drums? really? 😂) are fine to use too, with the caveat that for some people (living in the prior millenium, which I respect still) they are databases only and not buckets or key stores.

## History and Relationships
Adam said: _I'm told that Gane and Sarson also used rounded rectangles long before me.  (Gane, Chris; Sarson, Trish. *Structured Systems Analysis: Tools and Techniques*, 1979.).  According to Richard Botting's CS372 [course notes](http://www.csci.csusb.edu/dick/cs372/a4.html) Yourdon and De Marco also used sharp rectangles for external entities._ I'm a firm beleiver on rounded rectangle having a better acceptance value to human beings than sharp ones ([Curve Appeal: Exploring Individual Differences in Preference for Curved Versus Angular Objects](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC5405906/)), however by transposition they would also have less acceptances than circles. So, sorry Adam, I'm sticking to circles!
