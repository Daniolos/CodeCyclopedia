# Decorator Pattern Example in C#

In this example, the Decorator pattern is used to add responsibilities dynamically to an object.
The Decorator pattern provides a flexible alternative to subclassing for extending functionality.
Here, we'll extend the features of a `Coffee` object by adding different ingredients as decorators.

## The ICoffee Interface

The `ICoffee` interface defines the properties and methods that all coffee types and decorators must implement.

```C#
public interface ICoffee
{
    double Cost { get; }
    string Description { get; }
}
```

## Basic Coffee Class

We have a basic coffee class to represent a simple coffee.

```C#
public class SimpleCoffee : ICoffee
{
    public double Cost => 5.0;
    public string Description => "Simple coffee";
}
```

## Coffee Decorators

These classes will be our decorators, which can be wrapped around any `ICoffee` object to enhance its features.

```C#
public class MilkDecorator : ICoffee
{
    private ICoffee _coffee;

    public MilkDecorator(ICoffee coffee)
    {
        _coffee = coffee;
    }

    public double Cost => _coffee.Cost + 1.5;
    public string Description => _coffee.Description + ", with milk";
}

public class SugarDecorator : ICoffee
{
    private ICoffee _coffee;

    public SugarDecorator(ICoffee coffee)
    {
        _coffee = coffee;
    }

    public double Cost => _coffee.Cost + 0.5;
    public string Description => _coffee.Description + ", with sugar";
}
```

## Usage

```C#
class Program
{
    static void Main(string[] args)
    {
        ICoffee simpleCoffee = new SimpleCoffee();
        Console.WriteLine($"Cost: {simpleCoffee.Cost}; Description: {simpleCoffee.Description}");

        ICoffee milkCoffee = new MilkDecorator(simpleCoffee);
        Console.WriteLine($"Cost: {milkCoffee.Cost}; Description: {milkCoffee.Description}");

        ICoffee sugarMilkCoffee = new SugarDecorator(milkCoffee);
        Console.WriteLine($"Cost: {sugarMilkCoffee.Cost}; Description: {sugarMilkCoffee.Description}");
    }
}
```

In this example, we start with a basic `SimpleCoffee`.
We then extend its functionality by wrapping it with decorators like `MilkDecorator` and `SugarDecorator`.
This allows us to dynamically add features to the coffee at runtime.
