<properties
	pageTitle="Información general de la funcionalidad de escalado automático en Microsoft Azure Virtual Machines, Cloud Services y Web Apps | Microsoft Azure"
	description="Información general sobre el escalado automático en Microsoft Azure. Esta funcionalidad se utiliza en Microsoft Azure Virtual Machines, Cloud Services y Web Apps."
	authors="rboucher"
	manager=""
	editor=""
	services="monitoring-and-diagnostics"
	documentationCenter="monitoring-and-diagnostics"/>

<tags
	ms.service="monitoring-and-diagnostics"
	ms.workload="na"
	ms.tgt_pltfrm="na"
	ms.devlang="na"
	ms.topic="article"
	ms.date="09/06/2016"
	ms.author="robb"/>

# Información general de la funcionalidad de escalado automático de Microsoft Azure Virtual Machines, Cloud Services y Web Apps

En este artículo se explican el concepto del escalado automático de Microsoft Azure y las ventajas que aporta, y se realiza una introducción para empezar a usarlo.

El escalado automático de Azure Insights solo se aplica a los [conjuntos de escalado de máquina virtual](https://azure.microsoft.com/services/virtual-machine-scale-sets/), [Cloud Services](https://azure.microsoft.com/services/cloud-services/) y [App Service - Web Apps](https://azure.microsoft.com/services/app-service/web/).

>[AZURE.NOTE] Azure tiene dos métodos de escalado automático. Una versión anterior del escalado automático se aplica a Virtual Machines (conjuntos de disponibilidad). Esta característica tiene una compatibilidad limitada, por lo que, para poder utilizar el escalado automático de manera más rápida y fiable, recomendamos la migración a los conjuntos de escalado de máquina virtual. En este artículo, se incluye un vínculo sobre cómo utilizar la tecnología antigua.


## ¿Qué es el escalado automático?

Gracias al escalado automático, puede ejecutar la cantidad correcta de recursos para administrar la carga de la aplicación. Permite agregar recursos para controlar el aumento de la carga y ahorrar dinero mediante la eliminación de recursos inactivos. Especifique un número mínimo y máximo de instancias para ejecutar y agregue o quite máquinas virtuales automáticamente en función de un conjunto de reglas. Tener un mínimo garantiza la ejecución de la aplicación aunque no exista carga. Tener un máximo limita el posible costo total por hora. Se escala automáticamente entre estos dos extremos en función de las reglas que se creen.

 ![Explicación del escalado automático. Agregar y quitar máquinas virtuales](./media/monitoring-autoscale-overview/AutoscaleConcept.png)

Cuando se cumplen las condiciones de las reglas, se desencadenan una o varias acciones de escalado automático. Puede agregar y quitar máquinas virtuales o realizar otras acciones. En el siguiente diagrama conceptual se muestra este proceso.

 ![Flujograma conceptual del escalado automático](./media/monitoring-autoscale-overview/AutoscaleOverview3.png)
 

## Explicación del proceso de escalado automático
La explicación siguiente se aplica a las partes del diagrama anterior.

### Métricas de los recursos 
Los recursos generan métricas, que procesan posteriormente las reglas. Las métricas proceden de métodos diferentes. Los conjuntos de escala de máquina virtual utilizan datos de telemetría de los agentes de Diagnósticos de Azure, mientras que la telemetría de Web Apps y Cloud Services proviene directamente de la infraestructura de Azure. Algunas de las estadísticas que se utilizan frecuentemente son el uso de CPU, el uso de memoria, el número de subprocesos, la longitud de la cola y el uso del disco. Para ver una lista de los datos de telemetría que se pueden utilizar, consulte [Métricas comunes de escalado automático de Azure Insights](insights-autoscale-common-metrics.md).

### Hora
Las reglas basadas en programaciones emplean el huso horario UTC. Debe establecer la zona horaria correctamente al configurar las reglas.

### Reglas
El diagrama solo muestra una única regla de escalado automático, pero puede tener muchas. Puede crear reglas complejas de superposición según su situación. Estos son algunos de los tipos de reglas:
 
 - **Basadas en métricas**: por ejemplo, realizar esta acción cuando el uso de CPU sea superior al 50 %.
 - **Basadas en tiempo** : por ejemplo, desencadenar un webhook todos los sábados a las 8:00 en una zona horaria determinada.

Las reglas basadas en métricas miden la carga de la aplicación y agregan o quitan máquinas virtuales en función de ella. Las reglas de programación permiten escalar al ver los modelos de tiempo de la carga, si quiere escalar antes de un posible aumento de carga o si esta disminuye.

 
### Acciones y escalado automático

Las reglas pueden desencadenar uno o varios tipos de acciones.

- **Escalar**: escalar o reducir horizontalmente máquinas virtuales
- **Enviar correo electrónico**: enviar correo electrónico a los administradores y coadministradores de la suscripción, así como a otras direcciones de correo electrónico que especifique
- **Automate via webhooks** (Automatizar mediante webhooks): llamar a webhooks, que pueden desencadenar varias acciones dentro o fuera de Azure. Dentro de Azure, puede iniciar runbooks de Azure Automation, Azure Function o Azure Logic Apps. La URL de terceros de ejemplo fuera de Azure incluye servicios como Slack y Twilio.


## Configuración de escalado automático
El escalado automático utiliza la siguiente terminología y estructura.

- El motor de escalado automático lee la **configuración de escalado automático** para determinar si se debe escalar hacia arriba o hacia abajo. Contiene uno o más perfiles, información sobre el recurso de destino y la configuración de las notificaciones.
    - Un **perfil de escalado automático** es una combinación de una configuración de capacidad, un conjunto de reglas que rigen los desencadenadores, acciones de escalado para el perfil y una periodicidad. Puede tener varios perfiles, lo cual le permitirá ocuparse de diferentes requisitos coincidentes.
        - La **configuración de capacidad** indica el los valores mínimo, máximo y predeterminados para el número de instancias. [lugar adecuado utilizar la fig. 1].
        - Las **reglas** incluyen desencadenadores (ya sea de métricas o de tiempo) y una acción de escalado, que indican si el escalado automático debe dirigirse hacia arriba o hacia abajo cuando se cumpla esta regla.
        - La **periodicidad** indica cuándo el escalado automático debe hacer entrar en vigor el perfil. Puede tener perfiles de escalado automático diferentes, por ejemplo, para distintos momentos del día o días de la semana.
- La **configuración de las notificaciones** define qué notificaciones deben aparecer cuando se produce un evento de escalado automático en función de los criterios de los perfiles de configuración de escalado automático que cumpla. Con el escalado automático se pueden notificar a una o más direcciones de correo electrónico o realizar llamadas a uno o más webhooks.
 
![Configuración, perfil y estructura de las reglas de escalado automático de Azure](./media/monitoring-autoscale-overview/AzureResourceManagerRuleStructure3.png)

La lista íntegra de campos y descripciones configurables se encuentra en la [API de REST de escalado automático](https://msdn.microsoft.com/library/dn931928.aspx).

Para ver ejemplos de código, consulte los siguientes artículos:

* [Configuración avanzada de escalado automático con plantillas de Resource Manager para conjuntos de escala de máquina virtual](insights-advanced-autoscale-virtual-machine-scale-sets.md)
* [API de REST de escalado automático](https://msdn.microsoft.com/library/dn931953.aspx)



## Escalado horizontal frente a escalado vertical
  
El escalado automático aumenta los recursos únicamente en horizontal, lo que supone el aumento o la reducción del número de instancias de máquina virtual. El escalado horizontal (más flexible en un entorno en la nube) permite ejecutar miles de máquinas virtuales para administrar la carga. El escalado vertical es diferente. Mantiene el mismo número de máquinas virtuales, pero hace que sean más o menos potentes. La potencia se mide en memoria, velocidad de CPU, espacio en disco, etc. El escalado vertical tiene más limitaciones, ya que depende de la disponibilidad de hardware de mayor tamaño, que puede variar según la región y que supera el límite rápidamente. El escalado vertical también suele requerir que se detenga e inicie una máquina virtual. Para obtener más información, consulte [Escalado vertical de máquinas virtuales de Azure con Automatización de Azure](../virtual-machines/virtual-machines-linux-vertical-scaling-automation.md).


## Métodos de acceso 
Puede configurar el escalado automático en los siguientes lugares:

- [Portal de Azure](insights-how-to-scale.md)
- [PowerShell](insights-powershell-samples.md#create-and-manage-autoscale-settings)
- [Interfaz de línea de comandos (CLI) multiplataforma ](insights-cli-samples.md#autoscale)
- [API de REST de Insights](https://msdn.microsoft.com/library/azure/dn931953.aspx)

## Servicios compatibles con el escalado automático


| Servicio | Esquema y documentos |
|--------------------------------------|-----------------------------------------------------|
| Aplicaciones web | [Escalado en Web Apps](insights-how-to-scale.md) |
| Servicios en la nube | [Escalado automático de un servicio en la nube](../cloud-services/cloud-services-how-to-scale.md) |
| Virtual Machines: clásico | [Escalado de conjuntos de disponibilidad clásicos de máquina virtual](https://blogs.msdn.microsoft.com/kaevans/2015/02/20/autoscaling-azurevirtual-machines/) |
| Virtual Machines: conjuntos de escalado de Windows| [Escalado de conjuntos de disponibilidad de máquina virtual en Windows](../virtual-machine-scale-sets/virtual-machine-scale-sets-windows-autoscale.md) |
| Virtual Machines : conjuntos de escalado de Linux | [Escalado de conjuntos de disponibilidad de máquina virtual en Linux](../virtual-machine-scale-sets/virtual-machine-scale-sets-linux-autoscale.md) |
| Virtual Machines: ejemplo de Windows | [Configuración avanzada de escalado automático con plantillas de Resource Manager para conjuntos de escala de máquina virtual](insights-advanced-autoscale-virtual-machine-scale-sets.md) |

## Pasos siguientes

Para más información sobre el escalado automático, consulte los tutoriales de escalado automático anteriores o los siguientes recursos:

- [Métricas comunes de escalado automático de Azure Insights](insights-autoscale-common-metrics.md)
- [Procedimientos recomendados de escalado automático en Azure Insights](insights-autoscale-best-practices.md)
- [Uso de acciones de escalado automático para enviar notificaciones de alerta por correo electrónico y Webhook en Azure Insights](insights-autoscale-to-webhook-email.md)
- [API de REST de escalado automático](https://msdn.microsoft.com/library/dn931953.aspx)
- [Solución de problemas de escalado automático de conjuntos de escalado de máquinas virtuales](../virtual-machine-scale-sets/virtual-machine-scale-sets-troubleshoot.md)

<!---HONumber=AcomDC_0914_2016-->