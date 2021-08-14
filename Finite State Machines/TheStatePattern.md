# Finite State Machines (The State Pattern)

The **State Pattern** is super useful when dealing with simple to moderate systems.
Simply, the state pattern **disctinct different behaviors**.
Anytime we have an object **that needs to change its behavior** based on any game parameters, then the state pattern may be used.

We could have many different states in our game for example:

- Menu state
- Level state
- Waiting to do something state (start a race)

There are lots of difference permutations of this pattern. We can use simple **switch** statements or just doing **if-blocks** to more complex cases where we use 
**class-state** pattern.

So to summarize, if we have an object that changes its behavior at different points of the game, we probably want to use this particular pattern.

From the image 1 we can see what the state patterns look from a high level of abstraction.

To work with the state pattern we are going to have a **class** that is going to function as a **state machine**

That will be the **engine** (motor) that drives the **state changes** and keep track of which state is the **current state** and which state will be executed.

