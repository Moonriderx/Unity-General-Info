# Generics

To understand the concepts around generics, you must be familiar with the OOP principles.

Let's take a look at the following simple example:

First - create an empty scene in Unity.

Let's say that we want to have a sword game object in our game.
Create an empty game object and name it "Sword".

Now, create an empty c# script and name it "Sword"
Attach the script to the "Sword" game object.

```
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class Sword : MonoBehaviour
{
    
    void Start()
    {
        Print();
    }

    void Print()
    {
        Debug.Log("Hello, I am a " + typeof(Sword));
    }
}

```

The script itself can be very simple. In this case we are declaring a function at the start that will print to the console
"Hello, I am a sword"

Now, lets add one more game objects "Rifle" for example with the "rifle" script.

```
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class Rifle : MonoBehaviour
{
    
    void Start()
    {
        Print();
    }

    void Print()
    {
        Debug.Log("Hello, I am a " + typeof(Rifle));
    }
}

```


We can add one more class called "Shotgun" with the basic same logic

```
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class Sniper : MonoBehaviour
{
    
    void Start()
    {
        Print();
    }

    void Print()
    {
        Debug.Log("Hello, I am a " + typeof(Sniper));
    }
}

```

Now, on starting the game we will have a 3 different game objects with 3 different scripts attached to each of the objects.
We can see a pattern there.
The problem is that we don't wanna be copy pasting our code everytime we create a new weapon. 
Also, if we want to edit something, we must go through every single weapon script and changes the lines there.

Here comes the need of generic class where each of the weapons inherit from.

Let's create a new script and called it "Weapon"

We wanna have the same code inside, but now the important difference is that we do not know what class will be there.
So we will use "T" after typeof instead of the class itself.
Also in the beginning after the class. That signature means it is generic class.

And now instead of each weapon (The sniper, the Rifle, the Sword) having the same script, we can delete the meaningful code inside the scripts and leave them empty.


They are all gonna inherit from the weapon class

```
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class Sniper : Weapon<Sniper>
{
    
}

```

```
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class Rifle : Weapon<Rifle>
{
    
}

```

```
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class Sword : Weapon<Sword>
{
    
}

```

Let's take a look on how our "Weapon" script will look

```
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class Weapon<T> : MonoBehaviour
{
    
    void Start()
    {
        Print();
    }

    void Print()
    {
        Debug.Log("Hello, I am a " + typeof(T));
    }
}

```

After playing again, we will have the exactly same result, but with much cleaner code.
We will not copy pasting code anymore
We have a single generic class that all 3 weapons inherit from

# Copying Weapons

Now, lets add a twist there.

We want to add a copy of that weapons in runtime. (after hitting play button)

What we will do?

Let's modify our Weapon script:

```
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class Weapon<T> : MonoBehaviour
{
    
    void Start()
    {
        Print();
    }

    void Print()
    {
        Debug.Log("Hello, I am a " + typeof(T));
        GameObject copy = new GameObject();
        copy.name = "copy of a " + typeof(T);
    }
}

```

Now, after hiting the play button we will have a six weapons (the 3 original weapons, and a 3 copied weapons in our game hierarchy)
You will notice that the "original" weapons had the scripts, and the coppied weapons does not.

If we go back to the code and type

```
copy.AddComponent<T>();
```

We will get an error message. This is because we cannot attach a generic script to an gameObject.

The script is Monobehavior and the "T" itself can be anything - string, int, double etc....
We cannot attach "whatever" to an game object so we need to specify that T inherit from the monobehavior.

We need to modify this line in our code:

```
public class Weapon<T> : MonoBehaviour where T: MonoBehavior
```

Now all the T from the class will be class inherited from the MonoBehavior


Now, the problem is that when we click play we will have infinity loop. Lets fix that adding a simple statement to our code:

```
if (!this.gameObject.name.Contains("copy"))
{

}
```

Let's take a look at the final code 

```
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class Weapon<T> : MonoBehaviour where T: MonoBehavior
 
    
    void Start()
    {
        Print();
    }

    void Print()
    {
        Debug.Log("Hello, I am a " + typeof(T));

        if (!this.gameObject.name.Contains("copy"))
    {
        GameObject copy = new GameObject();
        copy.name = "copy of a " + typeof(T);

        copy.AddComponent<T>();
    }
    }
}

```