# Remark.js presentation

## Transcript

### slide 1
Aloha, I'm Roger Lew from the University of Idaho. I wasn't able to make it to Hawaii, but I hope you'll are enjoying Hawaii and I'd like to thank Ron for letting me present remotely.

Here I will be discussing the development of a cognitive modeling architecture for dynamic HRA using the Rancor Microworld Simulator. I'd like to acknowledge my co-authors Torrey Mortenson, Ron Boring, and Tom Ulrich.

### slide 2

Traditional HRA methods are static and subjective, relying on the estimates of subject matter experts. The subjective nature can result in unreliable estimates and potential biases.

Ideally, we would like a method that is less subjective. Here we use a symbolic model of human cognition rather than an expert-based empirical model. It is symbolic in that the model incorporates abstract psychological constructs that interact with one another to produce outcomes. As opposed to a model that fit to data. Specifically, we are using an implementation of ACT-R's declarative memory model.

Secondly, we would like to know how operator decisions impact performance. Humans commit many errors, some are more consquential than others. We want to know how decisions impact plant performance. To accomplish this we are utilizing an integrative modeling approach. Where the cognitive model is integrated with a simplified plant model, the Rancor Microworld, which I will tell you about in a bit. 

Another possibility with this integrated modeling framework is the ability to estimate performance shaping factors based on dynamic plant conditions and take them into account for modeling human performance.

### slide 3

Why ACT-R?

Honestly, I'm new to ACT-R. 

ACT-R or the Adaptive Control of Thought-Rational was an attractive option because it is mature having originated in 1973. It is a fairly extensive cognitive modeling framework. The model attempts to incorporate our best understanding of cognitive neuroscience and decades of psychology experiments.<strike> There are three main types of modules in ACT-R: perceptual motor, declarative, and procedural.</strike>

### slide 4

Here we are mostly interested in the declarative memory module. Declarative memory is the knowledge of facts like knowing that Paris is the capital of France. For the operator model we want a model that can remember the correct action for a given plant state. The ACT-R declarative memory model can accurately model several memory limitiations including the fan effect, primacy and recency effects, and serial recall performance. Enough studies have been performed such that we have a good understanding of default parameters that yield reasonable results.

### slide 5

So how does cognitive model work?

The model learns a vectorized (discrete) problem space. These vectors are called chunks. In this context the chunks are vectors representing the state of the plant. Such as knowing the reactor temperature is normal, both reactor coolant pumps are operational, the turbine/generator load is above 0 MW, no alarms are annuciated. In addition to the chunks the model learns how the chunks indicate the state of the plant: e.g. online, startup, abnormal, or the appropriate procedure to enter.

Once trained the models can retrieve the chunk (and the remembered decision) or be given a partial chunk and retrieve the closest match with the highest utility.

### slide 6
### slide 7

Nuclear power plants have full-scope simulators with literally tens-of thousands of parameters in the model and complex interactions between systems. Here we need something simplier and more decomposible to start with. We are utilizing the Rancor Microworld, a Simplified Nuclear Power Plant Simulator. It has the major systems and components of a PWR, but with reduced complexity. The reduced complexity allows naive operators to quickly learn and operate it. We also have lots of experience with Rancor and a fair amount of data available to use for modeling.

### slide 8

One challenge is that the cogntive model needs discrete states, but many of the parameters in Rancor are continuous. So we need a way of discretizing the parameters for the cognitive models. This table highlights some of the discretization schemes used to train the cognitive models. It would be better if the discretation schemes could be decided by the model. At this point they are explicitly defined based on our operational experience with Rancor. The perceived model states are also nullable or allow for unknown states.

### slide 9

Here is a bit more of a concrete example of how this works and what the model is capable of. This table depicts the responses needed to control steam generator levels for the Rancor Microworld. 
- Hypothetically, we might not care about SG levels if the plant is shutdown. So the model can learn that it needs to pay attention to the plant mode. If the plant is shutdown the state of the other parameters is irrelevant and the appropriate response is to do nothing. 
- The model can also learn that if the plant mode is unknown then the appropriate response is to determine the plant mode and the other paramerers are irrelevent.
- If the plant is online or in startup and the SG levels are normal and stable than no response is required
- If a SG level is normal but increasing the appropriate response would be to lower the feed water control valve for that SG to limit the inflow to that SG.
- Or vice-versa if the level is normal but decreasing the appropriate response would be to raise the feed water control valve

In the table below we can see the other possible mappings between plant state and the appropriate response. In the table below the * are used as wildcards. This information could be known or unknown, that model has to learn the precedence of what information is important and what information can be ignored.

### slide 10

Up to this point, we are able to successfully train models to recognize mapping like those depicted on the previous slide. We have developed cognitive models for rancor that:
- can map alarms to alarm response procedures
- learn to prioritize multiple alarms
- can ignore extraneous variables
- can learn to qualitively identify plant states (online, shutdown, startup)
- can learn control action responses

We have also learned that the required training increased exponentially as more parameters are added.

Learning to ignore extraneous variable also increases the required training repetitions

We know that performance can be calibrated by
- manipulating the number of training repetitions
- manipulating the accuracy of the training data
- and by adding in extraneous variables

### slide 11

The next step is to develop a hierarchical framework for the cognitive memory models. The models could learn things like:
- how to identify plant state
- how to carry out immediate actions following an annuciation
- how to identify the correct procedure

The overall "control loop" of an operator would resemble what we've observed operators doing during scenarios in our full-scope simulator.

### slide 12

Hopefully this provided some insight into how we think cognitive models can be applied to dynamic HRA. The overall gol is to model human performance. 

Beyond that are numerous possibilities. 

Other work is developing an operator model for procedure following called HUNTER, Human Unimodel for Nuclear Technology to Enhance Reliability. This cognitive modeling is complementary to HUNTER and could be integrated with HUNTER. HUNTER can execute procedures, but doesn't know how to select the appropriate procedures to follow. 
 
 Hollnagel talks about Safety I vs. Safety II approaches. Safety I is traditional approach were we try to understand what leads to human error and work to prevent it. Safety II is the other side of the coin and examines how humans contribute to human machine peformance. We heavily rely on humans in the control room to ensure operational resilience. Good operators have a sort of "spidey sense" for how things are going. Operators develop intuitions for what can go wrong that aid in diagnostic troubleshooting.

Perhaps cognitive models could provide a means of capturing operator actions and decisions that lead to resilience. For example, cognitive models can take context into consideration. There could even be potential to build automated supervisory systems based on virtual operator models.
