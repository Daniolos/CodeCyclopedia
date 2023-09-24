# Composite Pattern Example in C#

The Composite pattern is used to treat individual objects and compositions of objects uniformly. 
his pattern composes objects into tree structures to represent part-whole hierarchies. Here, we'll use the `IComponent` interface to build a hierarchy of graphic objects (like circles, rectangles) and composite objects (graphics group).

## The IComponent Interface

The `IComponent` interface provides a common interface for all graphic objects.

```C#
public interface IComponent
{
    void Draw();
}
```

## Primitive Graphic Classes

We have two primitive graphics classes: `Circle` and `Rectangle`.

```C#
public class Circle : IComponent
{
    public void Draw()
    {
        Console.WriteLine("Drawing a circle");
    }
}

public class Rectangle : IComponent
{
    public void Draw()
    {
        Console.WriteLine("Drawing a rectangle");
    }
}
```

## Composite Graphic Class

The `GraphicGroup` class can contain both primitive graphics and other graphic groups, making it a composite.

```C#
public class GraphicGroup : IComponent
{
    private List<IComponent> _components = new List<IComponent>();

    public void Draw()
    {
        Console.WriteLine("Drawing a group of graphics:");
        foreach (var component in _components)
        {
            component.Draw();
        }
    }

    public void Add(IComponent component)
    {
        _components.Add(component);
    }

    public void Remove(IComponent component)
    {
        _components.Remove(component);
    }

    public IComponent GetChild(int index)
    {
        return _components[index];
    }
}
```

## Usage

```C#
class Program
{
    static void Main(string[] args)
    {
        var circle = new Circle();
        var rectangle = new Rectangle();

        var graphicGroup = new GraphicGroup();
        graphicGroup.Add(circle);
        graphicGroup.Add(rectangle);

        graphicGroup.Draw();
    }
}
```

In this example, the Composite pattern allows the `GraphicGroup` to contain a mix of individual graphics and groups of graphics. When `Draw` is called on the `GraphicGroup`, it calls `Draw` on each contained graphic, resulting in the individual graphics being rendered.