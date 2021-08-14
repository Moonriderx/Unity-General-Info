# Finite State Machines (The State Pattern)

The **State Pattern** is super useful when dealing with simple to moderate systems.
Simply, the state pattern **distinct different behaviors**.
Anytime we have an object **that needs to change its behavior** based on any game parameters, then the state pattern may be used.

We could have many different states in our game for example:

- Menu state
- Level state
- Waiting to do something state (start a race)

There are lots of different permutations of this pattern. We can use simple **switch** statements or just doing **if-blocks** to more complex cases where we use 
**class-state** pattern.

So to summarize, if we have an object that changes its behavior at different points of the game, we probably want to use this particular pattern.

From **image 1** we can see what the state patterns look like from a high level of abstraction.

To work with the state pattern we are going to have a **class** that is going to function as a **state machine**

That will be the **engine** (motor) that drives the **state changes** and keep track of which state is the **current state** and which state will be executed.

Inside of our state machine, we will have a **series of states**. They will provide different functions for each state.
We want to know what the current state is at any point in time. We will want to change the state on different conditions.

If we have a player, for example, we could have a **running** state, an **idle** state a **dead** state, etc...

Each of these states applies to the **player** can show different animations for example or handle more complex logic. The system is very modular. We can get almost anything different states like **bosses** that have to change their attack pattern on different conditions.

Each of the states has **own isolated behavior**.

Let's take a look at **Image 2**. (**State Pattern**)

We are going to have two base classes that are going to do most of the work inside of our example.

It's important to understand the "high level of abstraction".

We are going to have an **IState** interface. **Anything that is a type of state will be implementing this interface!**

In order to be an **IState** it needs to implement an **enter** , **exit** and **tick** states. We can imagine the **tick()** here like an **update()** in **Unity**

The **State Machine** will handle our base class and changing states. Also, it will keep track of whatever the current **IState** is.
This principle applies for the same (no matter what state machine we use).

On top of this, we will have our concrete implementations. 

So, if we want to make a **state machine** on our player, we would have the player state machine and it would **inherit** from **state machine**.

And then on the **Player State Machine** we would have the three different states: (**Walking**, **Idle**, and **Attacking** states). They will be specific to the player.

We will be using the state machine (the base class) to control how we are changing the states and all the functionality behind there. 
The **Specifics** of what happens inside of **each state** will be controlled by **Enter**, **Exit**, and **Tick** 

We can be at only **1** State at the time. If we are idle-ing we will be only doing the behavior of the **idle** state.
If we are attacking, we are going to do the behavior of the **attacking** state and so on.

**Only one state can be active at the time**.

TODO: Add a little project later to show and explain better:


