# Abstract Factory Pattern Example in C#

In this example, the Abstract Factory Pattern is used to produce families of related `IVehicle` objects.
An Abstract Factory provides an interface for creating families of related or dependent objects without specifying their concrete classes.

## The IVehicle Interface

The `IVehicle` interface defines the properties that all vehicle types must implement.

```C#
public interface IVehicle
{
    public string Make { get; set; }
    public string Model { get; set; }
}
```

## Derived Vehicle Classes

We have two derived vehicle classes: Sedan and SUV.

```C#
public class Sedan : IVehicle
{
    public string Make { get; set; }
    public string Model { get; set; }
    public int Doors { get; set; } = 4;
}

public class SUV : IVehicle
{
    public string Make { get; set; }
    public string Model { get; set; }
    public int Seats { get; set; } = 7;
}
```

## The Abstract Factory Interface and Concrete Factories

```C#
public interface IVehicleFactory
{
    IVehicle CreateSedan();
    IVehicle CreateSUV();
}

public class HondaFactory : IVehicleFactory
{
    public IVehicle CreateSedan()
    {
        return new Sedan { Make = "Honda", Model = "Accord" };
    }

    public IVehicle CreateSUV()
    {
        return new SUV { Make = "Honda", Model = "CR-V" };
    }
}

public class ToyotaFactory : IVehicleFactory
{
    public IVehicle CreateSedan()
    {
        return new Sedan { Make = "Toyota", Model = "Camry" };
    }

    public IVehicle CreateSUV()
    {
        return new SUV { Make = "Toyota", Model = "RAV4" };
    }
}
```

## Usage

```C#
class Program
{
    static void Main(string[] args)
    {
        IVehicleFactory hondaFactory = new HondaFactory();
        var hondaSedan = hondaFactory.CreateSedan();
        var hondaSUV = hondaFactory.CreateSUV();

        IVehicleFactory toyotaFactory = new ToyotaFactory();
        var toyotaSedan = toyotaFactory.CreateSedan();
        var toyotaSUV = toyotaFactory.CreateSUV();
    }
}
```

In this example, the Abstract Factory pattern is demonstrated with two vehicle factories: `HondaFactory` and `ToyotaFactory`.
Both factories can produce related families of vehicles (`Sedan` and `SUV`), but each factory creates vehicles of a specific brand.
This ensures that objects are produced from a single factory and are consistent with each other.