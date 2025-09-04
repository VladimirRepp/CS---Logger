# CS---Logger
The entity for logging the message

## Key features of the implementation:
1. **Singleton pattern** - guarantees a single instance of the logger in the application
2. **Thread Safety** - using lock for secure operation from multiple threads
3. **Flexible configuration** - you can configure logging levels, output ports, and file path
4. **Multiple outputs** - Supports console, file, and events simultaneously
5. **Error Handling** - protection against file writing errors
6. **Formatting** - automatic addition of timestamps and logging levels
7. **Color selection** - different colors for different levels in the console

## Usage example
```csharp
class Program
{
    static void Main()
    {
        // Configuring the logger
        Logger.Instance.Configure(
            logFilePath: @"C:\Logs\myapp\log.txt", // опционально
            minimumLogLevel: LogLevel.Info,
            outputPorts: Logger.OutputPort.Console | Logger.OutputPort.File | Logger.OutputPort.Event
        );
        
        // Subscribing to a logging event
        Logger.Instance.OnLogMessage += message => 
        {
            // Additional message processing
            Console.WriteLine($"Событие: {message}");
        };
        
        // Logging examples
        Logger.Instance.Info("Приложение запущено");
        Logger.Instance.Warning("Нехватка памяти");
        Logger.Instance.Error("Критическая ошибка в модуле X");
        
        // Or via a direct Log call
        Logger.Instance.Log("Тестовое сообщение", LogLevel.Info);
    }
}
```
