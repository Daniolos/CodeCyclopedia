# Flyweight Pattern Example in C#

The Flyweight pattern is used to minimize memory usage or computational costs by sharing as much as possible with similar objects.
In this example, we'll use the Flyweight pattern to manage shared properties for various shapes, thereby reducing memory overhead for these shared properties.

## The IShape Interface

The `IShape` interface defines the methods that all shape types must implement.

```C#
public interface IShape
{
    void Draw();
}
```

## The ShapeProperties Class (Flyweight)

This is the class which represents shared properties among shapes.

```C#
public class ShapeProperties
{
    public string Color { get; }
    public double LineWidth { get; }

    public ShapeProperties(string color, double lineWidth)
    {
        Color = color;
        LineWidth = lineWidth;
    }
}
```

## Concrete Shape Classes

We have two shape classes: Circle and Rectangle. Each uses `ShapeProperties` to store their shared properties.

```C#
public class Circle : IShape
{
    private readonly ShapeProperties _properties;
    public double Radius { get; set; }

    public Circle(ShapeProperties properties)
    {
        _properties = properties;
    }

    public void Draw()
    {
        Console.WriteLine($"Drawing a Circle of Color: {_properties.Color}, LineWidth: {_properties.LineWidth}, and Radius: {Radius}");
    }
}

public class Rectangle : IShape
{
    private readonly ShapeProperties _properties;
    public double Length { get; set; }
    public double Width { get; set; }

    public Rectangle(ShapeProperties properties)
    {
        _properties = properties;
    }

    public void Draw()
    {
        Console.WriteLine($"Drawing a Rectangle of Color: {_properties.Color}, LineWidth: {_properties.LineWidth}, Length: {Length} and Width: {Width}");
    }
}
```

## The ShapeFactory Class

The `ShapeFactory` class has a method called `GetShapeProperties` that returns shared properties based on a given color and lineWidth.

```C#
public class ShapeFactory
{
    private readonly Dictionary<string, ShapeProperties> _propertiesCache = new();

    public ShapeProperties GetShapeProperties(string color, double lineWidth)
    {
        var key = $"{color}-{lineWidth}";

        if (!_propertiesCache.ContainsKey(key))
        {
            _propertiesCache[key] = new ShapeProperties(color, lineWidth);
        }

        return _propertiesCache[key];
    }
}
```

## Usage

```C#
class Program
{
    static void Main(string[] args)
    {
        var factory = new ShapeFactory();

        var blueProperties = factory.GetShapeProperties("Blue", 2.5);
        var redProperties = factory.GetShapeProperties("Red", 3.0);

        var circle = new Circle(blueProperties) { Radius = 5.0 };
        var rectangle = new Rectangle(redProperties) { Length = 4.0, Width = 6.0 };

        circle.Draw();
        rectangle.Draw();
    }
}
```

In this example, we use the Flyweight pattern to ensure that shape properties (like color and line width) that are shared across various shapes are stored in a central location and reused wherever needed. This helps in reducing memory consumption.