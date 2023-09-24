
# Adjusted Builder Pattern Example in C#

In this example, an adjusted form of the Builder pattern is used to create a `Car` object.

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

## The CarBuilder Class

**Fluent Interface**:
Methods in CarBuilder enable method chaining by returning the `CarBuilder` itself.

**Immutability**:
A new `Car` is instantiated at the initiation of the `CarBuilder` and after every build.
This ensures immutability of every created `Car` object.

```C#
public class CarBuilder
{
    private Car _car = new Car();

    public CarBuilder SetEngine(string engine)
    {
        _car.Engine = engine;
        return this;
    }

    public CarBuilder SetTransmission(string transmission)
    {
        _car.Transmission = transmission;
        return this;
    }

    public CarBuilder SetBody(string body)
    {
        _car.Body = body;
        return this;
    }

    public CarBuilder SetAccessories(string accessories)
    {
        _car.Accessories = accessories;
        return this;
    }

    public Car Build()
    {
        var result = _car;
        _car = new Car();        
        return result;
    }
}
```

## Usage


```C#
class Program
{
    static void Main(string[] args)
    {
        var carBuilder = new CarBuilder();
        
        var car = carBuilder.SetEngine("1500 cc")
                            .SetTransmission("Manual")
                            .SetBody("Metal")
                            .SetAccessories("Leather seats")
                            .Build();
    }
}
```

For a complete overview of the Builder pattern, go to the [[Builder]].
