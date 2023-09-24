# Bridge Pattern Example in C#

The Bridge pattern is about separating an abstraction from its implementation, so that both can evolve without depending on each other.
This decoupling allows the implementation to be interchangeable.

In this example, we'll illustrate a simplified scenario where different `RemoteControl` types are used to operate different `Device` types.

## The Device Interface

The `IDevice` interface defines common operations for all devices.

```C#
public interface IDevice
{
    bool IsEnabled();
    void Enable();
    void Disable();
    int GetVolume();
    void SetVolume(int volume);
}
```

## Concrete Device Classes

We have two concrete device classes: `Television` and `Radio`.

```C#
public class Television : IDevice
{
    private bool _isEnabled = false;
    private int _volume = 50;  // Default volume

    public bool IsEnabled() => _isEnabled;
    public void Enable() => _isEnabled = true;
    public void Disable() => _isEnabled = false;
    public int GetVolume() => _volume;
    public void SetVolume(int volume) => _volume = volume;
}

public class Radio : IDevice
{
    private bool _isEnabled = false;
    private int _volume = 40;  // Default volume

    public bool IsEnabled() => _isEnabled;
    public void Enable() => _isEnabled = true;
    public void Disable() => _isEnabled = false;
    public int GetVolume() => _volume;
    public void SetVolume(int volume) => _volume = volume;
}
```

## The RemoteControl Abstract Class

The `RemoteControl` acts as the abstraction in the Bridge pattern.
It references the `IDevice` and defines methods that delegate calls to the device.

```C#
public abstract class RemoteControl
{
    protected IDevice _device;

    public RemoteControl(IDevice device)
    {
        _device = device;
    }

    public void TogglePower()
    {
        if (_device.IsEnabled())
            _device.Disable();
        else
            _device.Enable();
    }

    public abstract void VolumeUp();
    public abstract void VolumeDown();
}
```

## Concrete Remote Classes

We can have varying types of remote controls.
Here's a basic one and an advanced one as an example.

```C#
public class BasicRemote : RemoteControl
{
    public BasicRemote(IDevice device) : base(device) {}

    public override void VolumeUp()
    {
        int currentVolume = _device.GetVolume();
        _device.SetVolume(currentVolume + 10);
    }

    public override void VolumeDown()
    {
        int currentVolume = _device.GetVolume();
        _device.SetVolume(currentVolume - 10);
    }
}

public class AdvancedRemote : RemoteControl
{
    public AdvancedRemote(IDevice device) : base(device) {}

    public override void VolumeUp()
    {
        int currentVolume = _device.GetVolume();
        _device.SetVolume(currentVolume + 15);
    }

    public override void VolumeDown()
    {
        int currentVolume = _device.GetVolume();
        _device.SetVolume(currentVolume - 15);
    }

    public void Mute()
    {
        _device.SetVolume(0);
    }
}
```

## Usage

```C#
class Program
{
    static void Main(string[] args)
    {
        IDevice tv = new Television();
        RemoteControl basicRemote = new BasicRemote(tv);
        basicRemote.TogglePower();
        basicRemote.VolumeUp();

        IDevice radio = new Radio();
        RemoteControl advancedRemote = new AdvancedRemote(radio);
        advancedRemote.VolumeUp();
        ((AdvancedRemote)advancedRemote).Mute();
    }
}
```

In this example, the `RemoteControl` abstraction and the `IDevice` implementation can both vary independently.
The Bridge pattern effectively bridges the two without intertwining their functionalities.
