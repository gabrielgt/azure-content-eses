<properties
   pageTitle="Polimorfismo en el marco de Reliable Actors | Microsoft Azure"
   description="Cree jerarquías de tipos e interfaces de .NET en el marco de trabajo de Reliable Actors para volver a usar la funcionalidad y las definiciones de la API."
   services="service-fabric"
   documentationCenter=".net"
   authors="seanmck"
   manager="timlt"
   editor="vturecek"/>

<tags
   ms.service="service-fabric"
   ms.devlang="dotnet"
   ms.topic="article"
   ms.tgt_pltfrm="NA"
   ms.workload="NA"
   ms.date="07/07/2016"
   ms.author="seanmck"/>

# Polimorfismo en el marco de trabajo de Reliable Actors

El marco de Reliable Actors permite compilar actores empleando muchas de las mismas técnicas que usaría en el diseño orientado a objetos. Una de esas técnicas es el polimorfismo, que los tipos y las interfaces hereden de elementos primarios más generalizados. La herencia en el marco de Reliable Actors suele seguir el modelo de .NET con algunas restricciones adicionales.

## Interfaces

El marco Reliable Actors requiere la definición de al menos una interfaz que se implementará por el tipo de actor. Esta interfaz se usa para generar una clase de proxy que se puede usar por los clientes para comunicarse con los actores. Las interfaces pueden heredar de otras interfaces, siempre y cuando todas las interfaces implementadas por un tipo de actor y todos sus elementos principales deriven de IActor en última instancia. IActor es la interfaz base definida por la plataforma para los actores. Así, el ejemplo clásico de polimorfismo en el que se usan formas sería algo parecido a lo siguiente:

![Jerarquía de la interfaz de los actores de forma][shapes-interface-hierarchy]


## Tipos

También puede crear una jerarquía de tipos de actores, que se derivan de la clase Actor base proporcionada por la plataforma. En el caso de las formas, es posible tener un tipo `Shape` base:

```csharp
public abstract class Shape : Actor, IShape
{
    public abstract Task<int> GetVerticeCount();

    public abstract Task<double> GetAreaAsync();
}
```

Los subtipos de `Shape` pueden invalidar métodos del tipo base.

```csharp
[ActorService(Name = "Circle")]
[StatePersistence(StatePersistence.Persisted)]
public class Circle : Shape, ICircle
{
    public override Task<int> GetVerticeCount()
    {
        return Task.FromResult(0);
    }

    public override async Task<double> GetAreaAsync()
    {
        CircleState state = await this.StateManager.GetStateAsync<CircleState>("circle");

        return Math.PI *
            state.Radius *
            state.Radius;
    }
}
```

Observe el atributo `ActorService` en el tipo de actor. Este atributo indica al marco de Reliable Actors que debe crear automáticamente un servicio para hospedar actores de este tipo. En algunos casos, quizás quiera crear un tipo base que esté pensado únicamente para compartir la funcionalidad con subtipos y que nunca se usará para crear instancias de actores concretos. En esos casos, debe usar la palabra clave `abstract` para indicar que nunca va a crear un actor basado en ese tipo.


## Pasos siguientes

- Consulte [cómo el marco de trabajo de Reliable Actors aprovecha la plataforma de Service Fabric](service-fabric-reliable-actors-platform.md) para ofrecer confiabilidad, escalabilidad y un estado coherente.
- Obtenga información sobre el [ciclo de vida de los actores](service-fabric-reliable-actors-lifecycle.md).

<!-- Image references -->

[shapes-interface-hierarchy]: ./media/service-fabric-reliable-actors-polymorphism/Shapes-Interface-Hierarchy.png

<!---HONumber=AcomDC_0713_2016-->