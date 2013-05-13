Superconductor - Parallel Web Programming for Massive Visualizations

==

Open Source Release in May 2013! (BSD3)

Superconductor is a collection of compilers for scripting large, interactive visualizations. 

By supporting data sets of hundreds of thousands of data points, Superconductor enables new classes of interactive visualizations that were previously out of reach.

== 

Superconductor uses three key ideas:

1. DSLs: Programs are written in high-level languages (mostly standard web DSLs). 
  
  It supports the full pipeline: data loading, styling, layout, rendering, interaction

2. Automatic Parallelism: Aggressive compilers that employ program synthesis and modern parallel algorithms

  These are aggressive, yet hidden from typical programming interactions.

3. Parallel JavaScript: Portability and scriptability is through exploiting modern web standards from multicore and GPU processing:

  We automate use of: web workers (multicore), WebCL (GPU), WebGL (GPU). 


=== Domain specific languages (DSLs)

Superconductor supports web languages:

  -- JSON for data
  -- CSS selectors for styling
  -- JavaScript for interaction

It also introduces FTL for custom layouts:

  -- FTL is a declarative constraint-based ("attribute grammar") language
  -- A layout is a tree schema with local constraints between node attributes
  
  Ex:   
    class HBox : Node { 
      children { left: Node; right : Node }
      actions {
        width := left.width + right.width
      }
    }
    class VBox : Node { ... }
  
  -- The constraints must be solvable as a sequenence of parallel tree traversals (the compiler automatically figures this out)


=== Automatic Parallelism

Superconductor provides compilers for each of its high-level DSLs. It automatically finds and exploits parallelism.

-- It uses the GPU for the basic animation/interaction loop, except for data loading (parsing), which is multicore
-- It optimizes data representation and scheduling, but largely hides this from the programming API
-- It uses modern data parallel compilation techniques when viable
-- It uses new techniques in program synthesis to find parallelism in the layout language

=== Parallel JavaScript

For portability and scriptability, Superconductor uses parallel JavaScript: 

 -- multicore (web workers) and GPU (WebCL, and WebGL)

 -- programming is in our DSLs; Superconductor generates the parallel JavaScript code
 
 -- visualizations live in standard webpages, meaning they interact normally with the surrounding page through standard JavaScript

 -- we are working on supporting multiple backends, but the focus is on enabling new types of experiences on modern clients

