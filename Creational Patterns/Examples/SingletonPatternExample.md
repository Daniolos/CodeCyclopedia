# Singleton Pattern Example in C#

In this example, the Singleton pattern ensures that a class has only one instance and provides a global point of access to this instance.
This is particularly useful when you need to ensure that only one instance of a class is created throughout the application's lifetime.

## The Singleton Class

Here's a simple example of a Singleton implementation in C#:

```C#
public sealed class Singleton
{
    private static Singleton _instance = null;
    private static readonly object _lock = new object();

    private Singleton() { }

    public static Singleton Instance
    {
        get
        {
            lock (_lock)
            {
                if (_instance == null)
                {
                    _instance = new Singleton();
                }
                return _instance;
            }
        }
    }
}
```

## Features of the Singleton

* The constructor is made `private` to prevent any other class from instantiating.
* The `Instance` property is the global point of access. It ensures that only one instance of the Singleton class exists by using a locking mechanism.
* The `_lock` object is used to ensure thread safety, preventing multiple threads from creating multiple instances of the Singleton.

## Usage

```C#
class Program
{
    static void Main(string[] args)
    {
        Singleton instance1 = Singleton.Instance;
        Singleton instance2 = Singleton.Instance;

        if (instance1 == instance2)
        {
            Console.WriteLine("Both instances are the same.");
        }
        else
        {
            Console.WriteLine("Different instances.");
        }
    }
}
```

In the usage example, `instance1` and `instance2` point to the same instance of the `Singleton` class.
The console will output: "Both instances are the same.
