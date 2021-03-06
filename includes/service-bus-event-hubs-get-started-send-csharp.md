## Envío de mensajes a Centros de eventos

En esta sección se escribirá una aplicación de consola Windows que envía eventos al Centro de eventos.

1. En Visual Studio, cree un nuevo proyecto de aplicación de escritorio de Visual C# con la plantilla de proyecto **Aplicación de consola**. Asigne al proyecto el nombre **Remitente**.

	![](./media/service-bus-event-hubs-getstarted-send-csharp/create-sender-csharp1.png)

2. En el Explorador de soluciones, haga clic con el botón derecho en la solución y luego haga clic en **Administrar paquetes NuGet para la solución**.

3. Haga clic en la pestaña **Examinar** y, después, busque `Microsoft Azure Service Bus`. Asegúrese de que el nombre del proyecto (**Remitente**) se especifica en el cuadro **Versiones**. Haga clic en **Instalar** y acepte las condiciones de uso.

	![](./media/service-bus-event-hubs-getstarted-send-csharp/create-sender-csharp2.png)

	Visual Studio descarga, instala y agrega una referencia al [paquete NuGet de la biblioteca del Bus de servicio de Azure](https://www.nuget.org/packages/WindowsAzure.ServiceBus).

4. Agregue las siguientes instrucciones `using` al principio del archivo **Program.cs**:

	```
	using System.Threading;
	using Microsoft.ServiceBus.Messaging;
	```

5. Agregue los siguientes campos a la clase **Program**; para ello, sustituya los valores del marcador de posición por el nombre del Centro de eventos creado en la sección anterior y la cadena de conexión de nivel del espacio de nombres que ha guardado anteriormente.

	```
	static string eventHubName = "{Event Hub name}";
	static string connectionString = "{send connection string}";
	```

6. Agregue el método siguiente a la clase **Program**:

	```
	static void SendingRandomMessages()
	{
	    var eventHubClient = EventHubClient.CreateFromConnectionString(connectionString, eventHubName);
	    while (true)
	    {
	        try
	        {
	            var message = Guid.NewGuid().ToString();
	            Console.WriteLine("{0} > Sending message: {1}", DateTime.Now, message);
	            eventHubClient.Send(new EventData(Encoding.UTF8.GetBytes(message)));
	        }
	        catch (Exception exception)
	        {
	            Console.ForegroundColor = ConsoleColor.Red;
	            Console.WriteLine("{0} > Exception: {1}", DateTime.Now, exception.Message);
	            Console.ResetColor();
	        }

	        Thread.Sleep(200);
	    }
	}
	```

	Este método envía continuamente los eventos al Centro de eventos con un retraso de 200 ms.

7. Por último, agregue las líneas siguientes al método **Main**:

	```
	Console.WriteLine("Press Ctrl-C to stop the sender process");
	Console.WriteLine("Press Enter to start now");
	Console.ReadLine();
	SendingRandomMessages();
	```

<!---HONumber=AcomDC_0921_2016-->