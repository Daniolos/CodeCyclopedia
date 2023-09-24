# Builder Pattern Example in C#

In this example, the classic Builder pattern is used to create a `Car` object. The process is managed by a `Director` and uses a `Builder` interface.

## The Car Class

```C#
public class Car
{
    public string Engine { get; set; }
    public string Transmission { get; set; }
    public string Body { get; set; }
    public string Accessories { get; set; }
}
```

## The ICarBuilder Interface

```C#
public interface ICarBuilder
{
    void SetEngine(string engine);
    void SetTransmission(string transmission);
    void SetBody(string body);
    void SetAccessories(string accessories);
    Car Build();
}
```

## The CarBuilder Class

Implements the `ICarBuilder` interface to provide concrete implementation for building parts of a `Car`.

```C#
public class CarBuilder : ICarBuilder
{
    private Car _car = new Car();

    public void SetEngine(string engine)
    {
        _car.Engine = engine;
    }

    public void SetTransmission(string transmission)
    {
        _car.Transmission = transmission;
    }

    public void SetBody(string body)
    {
        _car.Body = body;
    }

    public void SetAccessories(string accessories)
    {
        _car.Accessories = accessories;
    }

    public Car Build()
    {
        return _car;
    }
}
```

## The CarDirector Class

Responsible for managing the construction process. The `CarDirector` uses an instance of `ICarBuilder` to construct a car according to certain specifications.

```C#
public class CarDirector
{
    private ICarBuilder _builder;

    public CarDirector(ICarBuilder builder)
    {
        _builder = builder;
    }

    public void Construct()
    {
        _builder.SetEngine("1500 cc");
        _builder.SetTransmission("Manual");
        _builder.SetBody("Metal");
        _builder.SetAccessories("Leather seats");
    }
}
```

## Usage

```C#
class Program
{
    static void Main(string[] args)
    {
        ICarBuilder builder = new CarBuilder();
        CarDirector director = new CarDirector(builder);

        director.Construct();
        
        Car car = builder.Build();
    }
}
```

For a complete overview of the Builder pattern, go to the [[Builder]].
