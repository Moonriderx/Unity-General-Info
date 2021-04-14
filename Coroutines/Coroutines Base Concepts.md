 
 
 # Coroutine

 ```
 IEnumerator Move()
    {
        for (int i = 0; i < 10; i++)
        {
            transform.Translate(-0.05f, 0f, 0f);
            yield return new WaitForSeconds(0.5f);
        }
    }
 ```


  
 When this simple coroutine function is attached to an gameObject and executed, the gameobject will move on the Xaxis once, then 
 ```yield return new WaitForSecond()``` will be executed waiting a 0.5 seconds. 
 Then the function will go back in the loop for the second loop and it will move again the gameObject.
 That will repeat 10 times.

 WaitForSeconds points the ability to "pause" the execution of the process and return control to Unity but then to continue where it left off the following frame.

 Coroutine exectuion:

```
using UnityEngine;
using System.Collections;

// In this example we show how to invoke a coroutine and
// continue executing the function in parallel.

public class ExampleClass : MonoBehaviour
{
    // In this example we show how to invoke a coroutine and
    // continue executing the function in parallel.

    private IEnumerator coroutine;

    void Start()
    {
        // - After 0 seconds, prints "Starting 0.0"
        // - After 0 seconds, prints "Before WaitAndPrint Finishes 0.0"
        // - After 2 seconds, prints "WaitAndPrint 2.0"
        print("Starting " + Time.time);

        // Start function WaitAndPrint as a coroutine.

        coroutine = WaitAndPrint(2.0f);
        StartCoroutine(coroutine);

        print("Before WaitAndPrint Finishes " + Time.time);
    }

    // every 2 seconds perform the print()
    private IEnumerator WaitAndPrint(float waitTime)
    {
        while (true)
        {
            yield return new WaitForSeconds(waitTime);
            print("WaitAndPrint " + Time.time);
        }
    }
}
```

This is the example taken directly from the unity documentation.
It shows how the coroutine execution handles.
We must use "StartCoroutine" method.
    
// Modify the example if you will use it for learning purposes

StartCoroutine returns a class Coroutine
We can use it like this 

var coroutine = StartCoroutine(Move());
StopCoroutine(coroutine);

This way we are terminating the execution of the coroutine Move();

In the bigger projects is good practice to use a gameObject specially for coroutines handling.
Something like Coroutine Manager.

We can also pass a paramether in the coroutine.

```
IEnumerator TestCoroutime(string randomString) {

    Debug.Log("Start" + randomString);
    yield return new WaitForSeconds(10);
    Debug.Log("End");

}
```

That way, the parameter will live in the life time of the execution of the coroutine.



Another most common usage of the coroutines is downloading a textures / sprites or making a connection to a web server.

(Unity Web Request) (add more info to the topic above)

