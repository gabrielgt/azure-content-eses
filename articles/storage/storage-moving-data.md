<properties
	pageTitle="Movimiento de datos hacia y desde Almacenamiento de Azure | Microsoft Azure"
	description="Este artículo ofrece información general sobre los distintos métodos de mover los datos hacia y desde Almacenamiento de Azure."
	services="storage"
	documentationCenter=""
	authors="micurd"
	manager="jahogg"
	editor="tysonn"/>

<tags
	ms.service="storage"
	ms.workload="storage"
	ms.tgt_pltfrm="na"
	ms.devlang="na"
	ms.topic="article"
	ms.date="07/27/2016"
	ms.author="micurd"/>

# Movimiento de datos hacia y desde Almacenamiento de Azure

Si desea mover los datos locales al Almacenamiento de Azure (o viceversa), hay varias maneras de hacerlo. El método que le resulte más adecuado dependerá de su escenario. Este artículo ofrece una breve descripción de diferentes escenarios y ofertas adecuadas para cada uno.

## Creación de aplicaciones

Si está creando una aplicación, desarrollando con la API de REST o con una de nuestras muchas bibliotecas de cliente es una excelente manera de mover datos hacia y desde Almacenamiento de Azure.

Almacenamiento de Azure proporciona bibliotecas de cliente enriquecidas para .NET, iOS, Java, Android, Plataforma universal de Windows (UWP), Xamarin, C++, Node.JS, PHP, Ruby y Python. Las bibliotecas de cliente ofrecen capacidades avanzadas, como lógica de reintentos, registro y cargas paralelas. También se puede desarrollar directamente en la API de REST, a la que se puede llamar con cualquier lenguaje que genere solicitudes HTTP/HTTPS.

Consulte [Introducción al Almacenamiento de blobs de Azure mediante .NET](storage-dotnet-how-to-use-blobs.md) para más información.

Además, también ofrecemos [Data Movement Library de Almacenamiento de Azure](https://www.nuget.org/packages/Microsoft.Azure.Storage.DataMovement) que es una biblioteca diseñada para copia de datos de alto rendimiento en Azure y desde Azure. Consulte nuestra [documentación](https://github.com/Azure/azure-storage-net-data-movement) de Data Movement Library para más información.

## Visualización o interacción rápida con los datos

Si desea una manera fácil de ver los datos de Almacenamiento de Azure y también disponer de la capacidad para cargar y descargar los datos, considere la posibilidad de utilizar el Explorador de Almacenamiento de Azure.

Consulte nuestra lista de [Exploradores de almacenamiento de Azure](storage-explorers.md) para más información.

## Administración del sistema

Si requiere una utilidad de línea de comandos (por ejemplo, administradores del sistema), o se siente más cómodo con ella, estas son unas cuantas opciones para tener en cuenta:

### AzCopy

AzCopy es una utilidad de línea de comandos de Windows diseñada para la copia de datos de alto rendimiento a y desde Almacenamiento de Azure. También puede copiar datos de blobs en la cuenta de almacenamiento o entre distintas cuentas de este tipo.

Consulte [Transferencia de datos con la utilidad en línea de comandos AzCopy](storage-use-azcopy.md) para más información.

### Azure PowerShell

Azure PowerShell es un módulo que proporciona cmdlets para administrar servicios en Azure. Se trata de un shell de línea de comandos basado en tareas y un lenguaje de scripts especialmente diseñados para administración del sistema.

Consulte [Usar Azure PowerShell con Almacenamiento de Azure](storage-powershell-guide-full.md) para más información.

### Azure CLI

CLI de Azure proporciona un conjunto de comandos de código abierto y multiplataforma para trabajar con los servicios de Azure. CLI de Azure está disponible en Windows, OSX y Linux.

Consulte [Uso de la CLI de Azure con Almacenamiento de Azure](storage-azure-cli.md) para más información.

## Movimiento de grandes cantidades de datos con una red lenta

Uno de los mayores desafíos asociado a mover grandes cantidades de datos es el tiempo de transferencia. Si desea obtener datos desde y hacia Almacenamiento de Azure sin preocuparse por los costos de la red o la escritura de código, Importación/Exportación de Azure es una solución adecuada.

Consulte [Importación/Exportación de Azure](storage-import-export-service.md) para más información.

## Realización de una copia de seguridad de los datos

Si solo necesita hacer una copia de seguridad de los datos en Almacenamiento de Azure, Copia de seguridad de Azure es la mejor opción. Se trata de una solución eficaz para la copia de seguridad de los datos locales y máquinas virtuales de Azure.

Consulte [Copia de seguridad de Azure](../backup/backup-introduction-to-azure-backup.md) para más información.

## Acceso a los datos locales y de la nube

Si necesita una solución para acceder a los datos locales y de la nube, considere el uso de la solución de almacenamiento en la nube híbrida de Azure, StorSimple. Esta solución consta de un dispositivo físico de StorSimple que almacena de manera inteligente los datos usados con más frecuencia en las unidades SSD, los datos menos usados en unidades de disco duro y los datos inactivos, de copia de seguridad o de archivado en Almacenamiento de Azure.

Consulte [StorSimple](../storsimple/storsimple-overview.md) para más información.

## Recuperación de los datos

Si tiene aplicaciones y cargas de trabajo locales, necesitará una solución que permita que su negocio siga funcionando en caso de desastre. Azure Site Recovery controla la replicación, la conmutación por error y la recuperación de máquinas virtuales y servidores físicos. Los datos replicados se almacenan en Almacenamiento de Azure, lo que le permite eliminar la necesidad de un centro de datos secundario en el sitio.

Consulte [Azure Site Recovery](../site-recovery/site-recovery-overview.md) para más información.

<!---HONumber=AcomDC_0727_2016-->