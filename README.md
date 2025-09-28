# Dependensy-inversion-principle
Цей приклад демонструє застосування DIP у C#.  

---

code:

```csharp
using System;
using System.IO;

namespace Dependency_inversion_principle
{
    interface ILogger
    {
        void Log(string message);
    }

    class FileLogger : ILogger
    {
        public void Log(string message)
        {
            File.WriteAllText("log.txt", message);
        }
    }

    class ConsoleLogger : ILogger
    {
        public void Log(string message)
        {
            Console.WriteLine(message);
        }
    }

    class OrderService
    {
        private readonly ILogger _logger;

        public OrderService(ILogger logger)
        {
            _logger = logger;
        }

        public void CreateOrder(string order)
        {
            // логіка створення
            _logger.Log("Замовлення створено: " + order);
        }
    }
}
