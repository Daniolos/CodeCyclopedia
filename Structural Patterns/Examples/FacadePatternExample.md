# Facade Pattern Example in C#

In this example, the Facade Pattern is used to provide a simplified interface to a set of interfaces in a subsystem, making the subsystem easier to use.
This pattern involves a single class, the `Facade`, which provides simplified methods required by the client and delegates the call to methods of existing system classes.

## Subsystem Classes

Assume that we have a subsystem that has several classes like `Engine`, `Transmission`, and `FuelSystem` to represent parts of a car.

```C#
public class Engine
{
    public void Start() => Console.WriteLine("Engine Started");
    public void Stop() => Console.WriteLine("Engine Stopped");
}

public class Transmission
{
    public void Shift() => Console.WriteLine("Transmission Shifted");
}

public class FuelSystem
{
    public void PumpFuel() => Console.WriteLine("Fuel Pumped");
}
```

## The Facade Class

The `CarFacade` class simplifies the interface for starting and stopping a car by aggregating methods from the subsystem classes.

```C#
public class CarFacade
{
    private readonly Engine _engine;
    private readonly Transmission _transmission;
    private readonly FuelSystem _fuelSystem;
    
    public CarFacade()
    {
        _engine = new Engine();
        _transmission = new Transmission();
        _fuelSystem = new FuelSystem();
    }
    
    public void StartCar()
    {
        _fuelSystem.PumpFuel();
        _engine.Start();
        _transmission.Shift();
    }
    
    public void StopCar()
    {
        _engine.Stop();
    }
}
```

## Usage

```C#
class Program
{
    static void Main(string[] args)
    {
        CarFacade car = new CarFacade();
        car.StartCar();
        Console.WriteLine("Car is running");
        car.StopCar();
    }
}
```

In this example, we're using a facade class `CarFacade` to start and stop a car.
The actual implementations of starting and stopping the car, such as pumping fuel, starting the engine, and shifting the transmission, are abstracted away from the client.
The client interacts only with the facade, which internally manages the state and behavior of the subsystem classes, making it easier to use the subsystem.
