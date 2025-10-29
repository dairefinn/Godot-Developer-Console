<img width="100%" alt="image" src="https://github.com/user-attachments/assets/63a179a7-6904-4ed1-aeec-713298d006d6" />

<br/>

A simple developer console for Godot which uses BBCode syntax for additional styling.

# Using the console

The developer console can be accessed using these static methods eg. `DeveloperConsole.PrintErr("Something went wrong")`

Static properties and methods:

- `IsFocused`: Boolean value which will indicate if the console input is focused
- `Print()`: Prints some basic text without any BBCode styling.
- `PrintSuccess()`: Prints in green
- `PrintInfo()`: Prints in blue
- `PrintWarning()`: Prints in yellow
- `PrintErr()`: Prints in red
- `Clear()`: Clears everything in the console

## Instances

Technically multiple console instances are supported but by default there is only one. The console instance can be accessed via `DeveloperConsole.Instance`.

Instance properties and methods:

- `PrintToDebugConsole`: Determines if logs are also sent to the Godot console output
- `IsInstanceFocused`: Boolean value which will indicate if the console input is focused
- `ClearInstance()`: Clears the console
- `ClearInput()`: Clears the console input
- `ShowPreviousCommand()`: Populates the input with the previously entered command
- `FocusConsoleInput()`: Focuses the console input

## Printing to the Godot output

This wraps GD.Print so ideally you would use this in place of GD.Print. By default anything sent to the console will not print in the Godot output but the `developer_console/print_to_debug_console` setting can be toggled to allow printing to both. This can also be toggled in code by using `DeveloperConsole.Instance.PrintToDebugConsole = true`.

**project.godot example:**

```
[developer_console]

print_to_debug_console="true"
```

# Commands

## Built-in commands

The console comes with a few built-in commands by default.

- `timescale`: Sets the time scale of the game.
- `clear`: Clears the console.
- `quit`: Quits the application.
- `help`: Lists all available commands.

## Registering commands

The power in the console comes from the ability to register commands with custom callbacks. This means that you can enter a command into the console and have it take an action elsewhere in the games files.

To register a command, you can use the `DeveloperConsoleCommandHandler.RegisterCommand` method. This takes a command name, a callback function, and a description.

```csharp
DeveloperConsoleCommandHandler.RegisterCommand("mycommand", MyCommandCallback, "My command description");
```

The callback function takes an array of arguments.

```csharp
void MyCommandCallback(string[] args)
{
    GD.Print("My command was called with arguments: ", args);
}
```

The command name is case-insensitive and the arguments are split by spaces.

## Unregistering commands

To unregister a command, you can use the `DeveloperConsoleCommandHandler.UnregisterCommand` method. This takes a command name and returns a boolean indicating if the command was unregistered.

```csharp
bool wasUnregistered = DeveloperConsoleCommandHandler.UnregisterCommand("mycommand");
```

If you want to unregister all commands, you can use the `DeveloperConsoleCommandHandler.UnregisterAllCommands` method.

```csharp
DeveloperConsoleCommandHandler.UnregisterAllCommands();
```
