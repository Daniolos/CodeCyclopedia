# Proxy Pattern Example in C#

In this example, the Proxy pattern is used to provide a placeholder for another object to control access to it.
It can be used to control the instantiation of the real object or to control the access to its methods.

## The IImage Interface

The `IImage` interface defines the methods that all image types must implement.

```C#
public interface IImage
{
    void Display();
}
```

## RealImage Class

The `RealImage` class implements the `IImage` interface and represents the actual object that will do the real operations.

```C#
public class RealImage : IImage
{
    private string _filename;

    public RealImage(string filename)
    {
        _filename = filename;
        LoadFromDisk();
    }

    private void LoadFromDisk()
    {
        Console.WriteLine("Loading " + _filename);
    }

    public void Display()
    {
        Console.WriteLine("Displaying " + _filename);
    }
}
```

## ProxyImage Class

The `ProxyImage` class also implements the `IImage` interface.
It maintains a reference that lets the proxy access the real subject.
`Proxy` might be responsible for creating and destroying the `RealImage`, and it acts as an intermediary.

```C#
public class ProxyImage : IImage
{
    private RealImage _realImage;
    private string _filename;

    public ProxyImage(string filename)
    {
        _filename = filename;
    }

    public void Display()
    {
        if (_realImage == null)
        {
            _realImage = new RealImage(_filename);
        }
        _realImage.Display();
    }
}
```

## Usage

```C#
class Program
{
    static void Main(string[] args)
    {
        IImage image = new ProxyImage("test_image.jpg");

        // Image will be loaded from disk
        image.Display(); 

        // Image will not be loaded from disk this time
        image.Display();
    }
}
```

In this example, the `ProxyImage` class acts as a proxy for the `RealImage` class.
On the first call to the Display method, the image is loaded from disk, but on subsequent calls, the already loaded image is used, thus avoiding redundant operations.
