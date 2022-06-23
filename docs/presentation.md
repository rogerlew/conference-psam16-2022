class: center, middle

## Development of a Dynamic Cognitive Modeling Architecture of Human Reliability Simulation using the Rancor Microworld Simulator

##### Roger Lew<sup>a</sup>, Torrey Mortenson<sup>b</sup>, Ronald L Boring<sup>c</sup>, and Thomas A Ulrich<sup>d</sup>

<sup>b</sup>,University of Idaho, Moscow, ID, USA, rogerlew@uidaho.edu

<sup>b</sup>,Idaho National Laborarory, Idaho Falls, ID, USA, torrey.mortenson@inl.gov

<sup>c</sup>,Idaho National Laborarory, Idaho Falls, ID, USA, ronald.boring@inl.gov

<sup>d</sup>,Idaho National Laborarory, Idaho Falls, ID, USA, thomas.ulrich@inl.gov

---

## Introduction

- Nuclear Plants are complex socio-technical systems
- Need to understand propensity and implications of human-error
- Traditional HRA methods are static (estimated per task) and subjective

---


## Dynamic Human Reliability Analysis

### Broad goals

- Utilize symbolic model of human cognition rather than expert-based empirical models
  - ACT-R's declarative memory model (PyACTUp, PyIBL)
- Integrative modeling with plant simulators
  - important to understand the impact of decisions to plant performance
  - estimate PSFs based on dynamic plant conditions
- Couple to HUNTER to create virtual operator
  - real-time operator
  - monte-carlo simulations

---

## ACT-R (Adaptive Control of Thought—Rational)

- Originated in 1973 (John R. Anderson)
- Cognitive modeling framework
- Specifies how the brain is organized, and how its organization gives birth to what is perceived, remembered, and retrieved
- Modules
  - Perceptual Motor
  - Declarative Memory
  - Procedural Memory

---

## ACT-R Declarative Memory

Knowledge of facts (e.g. Paris is the capital of France)

Can model several known memory limitations:
- fan effect
- primacy and recency effects
- serial recall performance

Decades of studies, good understanding of default parameters that yield reasonable results

---

## Cognitive Model

### How does it work?

- Model learns vectorized problem space
- Learns "chunks" which are vectorized representations of the plant state
- Can also explicitly be given "utility" of chunks
- Once trained can be given a partial representation and retrieves closest match with utility weighting

---

## Rancor Microworld 

Full-scope simulators contain tens-thousands of parameters.
Need something easier to decompose to build and validate cognitive model.

- Rancor Microworld is a Simplified Nuclear Power Plant Simulator
- Has the major systems and components of a PWR
- Reduced complexity to allow naive operators to quickly learn and operate it
- Lots of experience and available data
  - (Plants have data but it is inaccessible)

---

### Example: Controlling Steam Generator Levels

<pre>
plant       alarm       alarm       SG A        SG B        Δ SG A      Δ SG B      response            comments
mode        high sg     low sg      level       level       level       level
------------------------------------------------------------------------------------------------------------------------
Shutdown    *           *           *           *           *           *           None
*           *           *           *           *           *           *           determine plant     low SA
                                                                                    mode
Online/     *           *           normal      *           ↑           *           ↓CV A               ahead of alarm
Startup
Online/     *           *           high        *           ↑           *           ↓CV A               after alarm 
Startup
Online/     *           *           high        *           ~           *           ↓CV A               way after alarm 
Startup
Online/     *           *           *           normal      *           ↑           ↓CV B               ahead of alarm
Startup
Online/     *           *           *           high        *           ↑           ↓CV B               after alarm 
Startup
Online/     *           *           *           high        *           ~           ↓CV B               way after alarm 
Startup
Online/     *           *           normal      *           ↓           *           ↑CV A               ahead of alarm
Startup
Online/     *           *           low         *           ↓           *           ↑CV A               after alarm 
Startup
Online/     *           *           low         *           ~           *           ↑CV A               way after alarm 
Startup
Online/     *           *           *           normal      *           ↓           ↑CV B               ahead of alarm
Startup
Online/     *           *           *           low         *           ↓           ↑CV B               after alarm 
Startup
Online/     *           *           *           low         *           ~           ↑CV B               way after alarm 
Startup
Online/     True        *           None        None        None        None        investigate high    low SA 
Startup
Online/     *           True        None        None        None        None        investigate low     low SA 
Startup
</pre>

---

### Lessons Learned

- Models require discretization of continuous variables
- ACT-R
  - Can learn 1 to 1 alarm mappings
  - Can learn alarm prioritization of multiple alarms
  - Can learn to ignore extraneous variables
  - Can learn how to qualitatively identify plant state
  - Can learn control actions
- Larger dimensional chunks take more time to train
- Extraneous variables take longer to train
- Performance can be calibrated by
  - manipulating training repetitions
  - manipulating the accuracy of the learning chunks
  - adding extraneous variables

## Rancor Microworld

---

## Cognitive Model

---

### Lessons Learned

---


## Model Architecture

---

## HUNTER Integration

---

## Future Implications

---

### Understand human resilience

- spidey sense awareness of plant state