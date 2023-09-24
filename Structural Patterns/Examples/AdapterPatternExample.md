# Adapter Pattern Example in C#

In this example, the Adapter Pattern is used to allow incompatible interfaces to work together.
This makes one class appear as another class by providing a wrapper around it.
Here, the Adapter Pattern is exemplified to make the `ITarget` interface work with the `Adaptee` class, which has a different interface.

## The ITarget Interface

The `ITarget` interface declares the operations that can be performed on `Adaptee` objects through an adapter.

```C#
public interface ITarget
{
    string GetRequest();
}
```

## The Adaptee Class

`Adaptee` contains some useful behavior, but its interface is incompatible with the existing client code.

```C#
public class Adaptee
{
    public string GetSpecificRequest()
    {
        return "Specific request.";
    }
}
```

## The Adapter Class

`Adapter` makes the `Adaptee`'s interface compatible with the `ITarget` interface.

```C#
public class Adapter : ITarget
{
    private readonly Adaptee _adaptee;

    public Adapter(Adaptee adaptee)
    {
        _adaptee = adaptee;
    }

    public string GetRequest()
    {
        return $"This is '{_adaptee.GetSpecificRequest()}'";
    }
}
```

## Usage

```C#
class Program
{
    static void Main(string[] args)
    {
        Adaptee adaptee = new Adaptee();
        ITarget target = new Adapter(adaptee);

        Console.WriteLine(target.GetRequest());
    }
}
```

In this example, `Adapter` is used to wrap an instance of the `Adaptee` class, transforming the interface of `Adaptee` into the `ITarget` interface.
The `Program` class can then use this adapter as if it was an instance of `ITarget`, allowing for communication between the `Adaptee` and the existing code without modifying their existing definitions.
