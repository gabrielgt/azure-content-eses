<properties
	pageTitle="Comparación de Servicio de aplicaciones de Azure, Máquinas virtuales, Service Fabric y Servicios en la nube | Microsoft Azure"
	description="Aprenda a elegir entre el Servicio de aplicaciones de Azure, Máquinas virtuales, Service Fabric y Servicios en la nube para hospedar aplicaciones web."
	services="app-service\web, virtual-machines, cloud-services"
	documentationCenter=""
	authors="tdykstra"
	manager="wpickett"
	editor="jimbe"/>

<tags
	ms.service="app-service-web"
	ms.workload="web"
	ms.tgt_pltfrm="na"
	ms.devlang="na"
	ms.topic="article"
	ms.date="07/07/2016"
	ms.author="tdykstra"/>

# Comparación de Servicio de aplicaciones de Azure, Máquinas virtuales, Service Fabric y Servicios en la nube

## Información general

Azure ofrece varias formas de hospedar sitios web: [Servicio de aplicaciones de Azure][], [Máquinas virtuales][], [Service Fabric][] y [Servicios en la nube][]. Este artículo le ayuda a comprender las opciones y a tomar la decisión correcta para su aplicación web.

El Servicio de aplicaciones de Azure es la opción más adecuada para la mayoría de aplicaciones web. La implementación y la administración están integradas en la plataforma, los sitios pueden escalarse rápidamente para asumir altas cargas de tráfico y el equilibrio de carga y el administrador de tráfico incluidos ofrecen una gran disponibilidad. Puede mover los sitios actuales al Servicio de aplicaciones de Azure fácilmente con una [herramienta de migración en línea](https://www.migratetoazure.net/), utilizar una aplicación de código abierto de la galería de aplicaciones web o crear un sitio nuevo usando el marco y las herramientas que prefiera. La característica [Trabajos web][] facilita la tarea de agregar procesamiento de trabajo en segundo plano a su aplicación web del Servicio de aplicaciones.

Service Fabric es una buena opción si se va a crear una aplicación nueva o se va a volver a escribir una aplicación existente para que use una arquitectura de microservicios. Las aplicaciones, que se ejecutan en un grupo compartido de máquinas, pueden empezar con pocas máquinas y crecer a gran escala con cientos o miles de máquinas, en caso de que sea necesario. Los servicios con estado facilitan el almacenaniento consistente y confiable del estado de la aplicación, mientras que Service Fabric administra automáticamente la creación de particiones, el escalado y la disponibilidad de los servicios. Service Fabric también admite WebAPI con Open Web Interface para .NET (OWIN) y ASP.NET Core. En comparación con el Servicio de aplicaciones, Service Fabric también proporciona más control sobre la infraestructura subyacente o acceso directo a ella. Puede acceder de forma remota a los servidores o configurar las tareas de inicio de los servidores. Servicios en la nube es similar a Service Fabric en lo que se refiere al grado de control frente a la facilidad de uso, pero es un servicio heredado y Service Fabric se recomienda para los desarrollos nuevos.

Si tiene una aplicación que requiera modificaciones sustanciales para ejecutarse en el Servicio de aplicaciones o en Service Fabric, puede elegir Máquinas virtuales para simplificar la migración a la nube. Sin embargo, la configuración, la protección y el mantenimiento adecuados de las máquinas virtuales requieren mucho más tiempo y conocimientos de TI, en comparación con el Servicio de aplicaciones de Azure y Service Fabric. Si está considerando la opción de Máquinas virtuales Azure, tenga en cuenta el esfuerzo constante de mantenimiento requerido para aplicar revisiones al entorno de Máquina virtual, así como para actualizarlo y administrarlo. Máquinas virtuales de Azure es una infraestructura como servicio (IaaS), mientras que Servicio de aplicaciones y Service Fabric son plataformas como servicio (Paas).

## <a name="features"></a>Comparación de características

La siguiente tabla compara las funcionalidades de Servicio de aplicaciones, Servicios en la nube, Máquinas virtuales y Service Fabric para ayudarle a tomar la mejor decisión. Para obtener más información acerca de los contratos de nivel de servicio para cada opción, consulte [Contratos de nivel de servicio de Azure](/support/legal/sla/).

Característica|Servicio de aplicaciones (aplicaciones web)|Servicios en la nube (roles web)|Máquinas virtuales|Service Fabric|Notas
---|---|---|---|---|---
Implementación casi instantánea|X|||X|La implementación de una aplicación o la actualización de una aplicación a un Servicio en la nube, o la creación de una máquina virtual, toma varios minutos; la implementación de una aplicación a una aplicación web tarda segundos.
Escalado vertical a máquinas más grandes sin volver a implementar|X|||X|
Las instancias de un servidor web comparten contenido y configuración; esto significa que no es necesario volver a implementar o configurar a medida que escale.|X|||X|
Varios entornos de implementación (producción y ensayo)|X|X||X|Service Fabric le permite tener varios entornos para las aplicaciones o para implementar versiones diferentes de su aplicación en paralelo.
Administración de actualización automática del SO|X|X|||Las actualizaciones automáticas del SO están previstas para las próximas versiones de Service Fabric.
Intercambio fluido entre plataformas (mover fácilmente entre 32 bits y 64 bits)|X|X|||
Código de implementación con GIT, FTP|X||X||
Código de implementación con Web Deploy|X||X||Servicios en la nube admite el uso de Web Deploy para implementar actualizaciones en instancias de rol individuales. Sin embargo, no puede utilizarlo para la implementación inicial de un rol, y si utiliza Web Deploy para una actualización, tiene que realizar la implementación por separado para cada instancia de un rol. Se requieren múltiples instancias para optar al contrato de nivel de servicio de Servicio en la nube para entornos de producción.
Soporte para WebMatrix|X||X||
Acceso a servicios como Bus de servicio, Almacenamiento, Base de datos SQL|X|X|X|X|
Web de host o nivel de servicios web de una arquitectura multinivel|X|X|X|X|
Nivel medio del host de una arquitectura multinivel|X|X|X|X|Las aplicaciones web del Servicio de aplicaciones pueden hospedar con facilidad un nivel medio de la API de REST y la característica [Trabajos web](http://go.microsoft.com/fwlink/?linkid=390226) puede hospedar trabajos de procesamiento en segundo plano. Puede ejecutar Trabajos web en un sitio web dedicado para alcanzar una escalabilidad independiente para el nivel. La característica de [aplicaciones de API](../app-service-api/app-service-api-apps-why-best-platform.md) de vista previa proporciona incluso más características para hospedar servicios REST.
Soporte integrado de MySQL como servicio|X|X|X||Servicios en la nube puede integrar MySQL como servicio mediante las ofertas de ClearDB, pero no como parte del flujo de trabajo del Portal de Azure.
Soporte para ASP.NET, ASP clásico, Node.js, PHP, Python|X|X|X|X|Service Fabric admite la creación de un front-end web con [ASP.NET 5](../service-fabric/service-fabric-add-a-web-frontend.md), o bien se puede implementar cualquier tipo de aplicación (Node.js, Java, etc.) como un [ejecutable invitado](../service-fabric/service-fabric-deploy-existing-app.md).
Escalado horizontal a varias instancias sin volver a implementar|X|X|X|X|Máquinas virtuales puede escalar horizontalmente hasta varias instancias, pero los servicios que se ejecutan en este servicio se deben escribir para controlar este escalado horizontal. Tiene que configurar un equilibrador de carga para que dirija solicitudes entre las máquinas y crear un Grupo de afinidad para evitar que todas las instancias se reinicien simultáneamente debido a errores de mantenimiento o hardware.
Soporte para SSL|X|X|X|X|En el caso de las aplicaciones web del Servicio de aplicaciones, solo se admite SSL para nombres de dominio personalizados para el modo Básico y Estándar. Para obtener más información sobre el uso de SSL con aplicaciones web, consulte [Configuración de un certificado SSL para un Sitio web Azure](../app-service-web/web-sites-configure-ssl-certificate.md).
Integración de Visual Studio|X|X|X|X|
Depuración remota|X|X|X||
Código de implementación con TFS|X|X|X|X|
Aislamiento de red con [Red virtual de Azure](/services/virtual-network/)|X|X|X|X|Consulte también [Integración de redes virtuales de Sitios web Azure](/blog/2014/09/15/azure-websites-virtual-network-integration/)
Soporte técnico para el [Administrador de tráfico de Azure](/services/traffic-manager/)|X|X|X|X|
Supervisión de extremo integrado|X|X|X||
Acceso de escritorio remoto a los servidores||X|X|X|
Instalación de cualquier MSI personalizado||X|X|X|Service Fabric permite hospedar cualquier archivo ejecutable como un [ejecutable invitado](../service-fabric/service-fabric-deploy-existing-app.md), o bien puede instalar cualquier aplicación en las máquinas virtuales.
Capacidad de definir/ejecutar tareas de inicio||X|X|X|
Puede atender eventos de ETW||X|X|X|

## <a name="scenarios"></a>Escenarios y recomendaciones

Aquí se presentan algunas situaciones habituales de aplicaciones con recomendaciones acerca de la opción de hospedaje web de Azure que podría ser más apropiada en cada caso.

- [Necesito un front-end web con procesamiento en segundo plano y back-end de base de datos para ejecutar aplicaciones empresariales integradas con recursos locales.](#onprem)
- [Necesito un método confiable para hospedar mi sitio web corporativo que se escale correctamente y ofrezca un alcance global.](#corp)
- [Tengo una aplicación IIS6 ejecutándose en Windows Server 2003.](#iis6)
- [Soy dueño de un negocio pequeño y necesito una forma económica de hospedar mi sitio, pero con un crecimiento a futuro en mente.](#smallbusiness)
- [Soy diseñador gráfico o web y deseo diseñar y crear sitios web para mis clientes.](#designer)
- [Estoy migrando mi aplicación de niveles múltiples con un front-end web a la nube.](#multitier)
- [Mi aplicación depende de entornos Windows o Linux altamente personalizados y deseo moverla a la nube.](#custom)
- [Mi sitio usa software de código abierto y deseo hospedarlo en Azure.](#oss)
- [Tengo una aplicación de línea de negocio que necesita conectarse a la red corporativa.](#lob)
- [Deseo hospedar una API de REST o un servicio web para los clientes móviles.](#mobile)


### <a id="onprem"></a> Necesito un front-end web con procesamiento en segundo plano y back-end de base de datos para ejecutar aplicaciones empresariales integradas con recursos locales.

El Servicio de aplicaciones de Azure es una solución excelente para aplicaciones empresariales complejas. Le permite desarrollar aplicaciones que se escalan automáticamente en una plataforma con equilibrio de carga, se protegen con Active Directory y se conectan con sus recursos locales. Esta opción consigue que la administración de estas aplicaciones resulte sencilla gracias a un portal y unas API de categoría superior, y le permite obtener información acerca del uso que los clientes están haciendo de ellas con herramientas específicamente diseñadas. La característica [Webjobs][] permite ejecutar tareas y procesos en segundo plano como parte de su nivel web, mientras que la conectividad híbrida y las características de VNET facilitan la reconexión con los recursos locales. El Servicio de aplicaciones de Azure proporciona SLA con un tiempo activo garantizado del 99,9% para las aplicaciones web y le permite:

* Ejecutar sus aplicaciones de manera confiable en una plataforma en la nube que se mantiene por sí misma y aplica revisiones automáticamente.
* Escalar automáticamente entre una red global de centros de datos.
* Realizar copias de seguridad y restaurar para la recuperación ante desastres.
* Cumplir con ISO, SOC2 y PCI.
* Integrarse con Active Directory

### <a id="corp"></a> Necesito un método confiable para hospedar mi sitio web corporativo que se escale correctamente y ofrezca un alcance global.

El Servicio de aplicaciones de Azure es una excelente solución para hospedar sitios web corporativos. Permite a las aplicaciones web escalarse de manera rápida y sencilla para atender con facilidad la demanda en una red global de centros de datos. Ofrece alcance local, tolerancia a errores y administración del tráfico inteligente. Todo en una plataforma que proporciona herramientas de administración de clase superior, con lo que podrá obtener información sobre el estado y el tráfico del sitio rápidamente y con toda facilidad. El Servicio de aplicaciones de Azure proporciona SLA con un tiempo activo garantizado del 99,9% para las aplicaciones web y le permite:

* Ejecutar sus sitios web de manera confiable en una plataforma en la nube que se mantiene por sí misma y aplica revisiones automáticamente.
* Escalar automáticamente entre una red global de centros de datos.
* Realizar copias de seguridad y restaurar para la recuperación ante desastres.
* Administrar registros y tráfico con herramientas integradas.
* Cumplir con ISO, SOC2 y PCI.
* Integrarse con Active Directory

### <a id="iis6"></a> Tengo una aplicación IIS6 ejecutándose en Windows Server 2003.

El Servicio de aplicaciones de Azure permite evitar fácilmente los costes de infraestructura asociados a la migración de aplicaciones IIS6 antiguas. Microsoft ha creado [herramientas de migración fáciles de utilizar y una detallada guía sobre migración](https://www.movemetowebsites.net/) que le permiten comprobar la compatibilidad e identificar aquellos cambios que deban realizarse. La integración con Visual Studio, TFS y las herramientas CMS más habituales facilitan la implementación de aplicaciones IIS6 directamente en la nube. Una vez implementadas, el Portal de Azure proporciona potentes herramientas de administración que permiten reducir verticalmente para administrar costes y aumentar verticalmente para atender la demanda cuando sea necesario. Con la herramienta de migración puede hacer lo siguiente:

* Migrar con rapidez y sencillez su aplicación web de Windows Server 2003 heredada a la nube.
* Optar por dejar la base de datos SQL adjunta en el entorno local para crear una aplicación híbrida.
* Mover automáticamente su base de datos SQL junto con la aplicación heredada.

### <a id="smallbusiness"></a>Soy dueño de un negocio pequeño y necesito una forma económica de hospedar mi sitio, pero con un crecimiento a futuro en mente.

El Servicio de aplicaciones de Azure es una solución excelente para este escenario, porque puede empezar a usarlo gratis y luego agregar más capacidades cuando las necesite. Cada aplicación web gratuita incluye un dominio proporcionado por Azure (*su\_compañía*.azurewebsites.net), y la plataforma incluye tanto herramientas de administración e implementación integradas como una galería de aplicaciones que permiten empezar a usarla sin complicaciones. Hay muchos otros servicios y opciones de escalado que permiten que el sitio evolucione con cuando aumente la demanda de los usuarios. Con el Servicio de aplicaciones de Azure, puede:

- Comenzar con el nivel gratis y luego escalar, según sea necesario.
- Usar la Galería de aplicaciones para configurar rápidamente aplicaciones web conocidas, como WordPress.
- Agregar servicios y características de Azure adicionales a su aplicación, según sea necesario.
- Proteger su aplicación web con HTTPS.

### <a id="designer"></a> Soy un diseñador gráfico o web y deseo diseñar y compilar sitios web para mis clientes.

Para diseñadores y desarrolladores web, el Servicio de aplicaciones de Azure se integra fácilmente con diversos marcos y herramientas, admite la implementación de Git y FTP y ofrece una integración estrecha con herramientas y servicios como Visual Studio y Base de datos SQL. Con el Servicio de aplicaciones, puede:

- Usar herramientas de línea de comandos para [tareas automatizadas][scripting].
- Trabajar con lenguajes populares como [.Net][dotnet], [PHP][], [Node.js][nodejs] y [Python][].
- Seleccionar tres niveles de escala diferentes para escalar hasta capacidades muy altas.
- Integrarse con otros servicios de Azure, como [Base de datos SQL][sqldatabase], [Bus de servicio][servicebus] y [Almacenamiento][] u ofertas de asociados de la [Tienda de Azure][azurestore], como MySQL y MongoDB.
- Integrarse con herramientas como Visual Studio, Git, WebMatrix, WebDeploy, TFS y FTP.

### <a id="multitier"></a>Estoy migrando mi aplicación de niveles múltiples con un front-end web a la nube.

Si está ejecutando una aplicación de niveles múltiples, como por ejemplo un servidor web que se conecta con una base de datos, el Servicio de aplicaciones de Azure es una opción excelente que ofrece una integración estrecha con Base de datos SQL. Y puede utilizar la característica WebJobs para ejecutar procesos de back-end.

Elija Service Fabric para uno o varios de los niveles si necesita más control sobre el entorno del servidor, como la posibilidad de tener acceso remoto al servidor o de configurar las tareas de inicio del servidor.

Elija Máquinas virtuales para uno o varios de los niveles si desea utilizar la imagen de su propia máquina o ejecutar servicios o software de servidor que se no puedan configurar en Service Fabric.

### <a id="custom"></a>Mi aplicación depende de entornos Windows o Linux altamente personalizados y deseo moverla a la nube.

Si su aplicación requiere una instalación o configuración compleja del software y el sistema operativo, Máquinas virtuales es probablemente la mejor solución. Con Máquinas virtuales, puede hacer lo siguiente:

- Usar la galería de Máquina virtual para que se inicie con un sistema operativo, como Windows o Linux y, a continuación, personalizarla según los requisitos de su aplicación.
- Crear y cargar una imagen personalizada de un servidor en un entorno local existente para que ejecute en una máquina virtual en Azure.

### <a id="oss"></a>Mi sitio usa software de código abierto y deseo hospedarlo en Azure.

Si el marco de código abierto se admite en el Servicio de aplicaciones, los lenguajes y los marcos requeridos por su aplicación se configuran automáticamente sin necesidad de que realice ninguna acción. El Servicio de aplicaciones le permite:

- Usar muchos lenguajes de código abierto populares, como [.NET][dotnet], [PHP][], [Node.js][nodejs] y [Python][].
- Configurar WordPress, Drupal, Umbraco, DNN y muchas otras aplicaciones web de terceros.
- Migrar una aplicación existente o crear una nueva a partir de la galería de aplicaciones.

Si el marco de código abierto no es compatible con el Servicio de aplicaciones, puede ejecutarlo en una de las otras opciones de hospedaje web de Azure. Con Máquinas virtuales, puede instalar y configurar el software en una imagen de la máquina, que puede basarse en Windows o Linux.

### <a id="lob"></a>Tengo una aplicación de línea de negocio que necesita conectarse a la red corporativa.

Si desea crear una aplicación de línea de negocio, puede que su sitio web requiera un acceso directo a los servicios o datos de la red corporativa. Esto se puede hacer en el Servicio de aplicaciones, Service Fabric y Máquinas virtuales mediante el [servicio Red virtual de Azure](/services/virtual-network/). En el Servicio de aplicaciones puede usar la nueva [característica de integración de VNET](https://azure.microsoft.com/blog/2014/09/15/azure-websites-virtual-network-integration/), que permite la ejecución de las aplicaciones de Azure como si se encontraran en su red corporativa.

### <a id="mobile"></a>Deseo hospedar una API de REST o un servicio web para los clientes móviles.

Los servicios web HTTP le permiten admitir una amplia variedad de clientes, incluidos los clientes móviles. Los marcos como ASP.NET Web API se integran con Visual Studio para facilitar la creación y el consumo de los servicios REST. Estos servicios se exponen desde un extremo web, por lo que es posible usar cualquier técnica de hospedaje web en Azure para admitir este escenario. Sin embargo, el Servicio de aplicaciones es una elección excelente para hospedar las API de REST. Con el Servicio de aplicaciones, puede:

- Crear rápidamente una [aplicación móvil](../app-service-mobile/app-service-mobile-value-prop.md) o [una aplicación de API](../app-service-api/app-service-api-apps-why-best-platform.md) que hospede el servicio web HTTP en uno de los centros de datos distribuidos globalmente de Azure.
- Migrar los servicios existentes o crear otros nuevos.
- Conseguir contratos de nivel de servicio para disponibilidad con una sola instancia, o escalar horizontalmente a varias máquinas dedicadas.
- Usar el sitio publicado para proporcionar API de REST a cualquier cliente HTTP, incluidos los clientes móviles.

> [AZURE.NOTE]
Si desea empezar a usar el Servicio de aplicaciones de Azure antes de registrarse para crear una cuenta, vaya a <a href="https://trywebsites.azurewebsites.net/">https://trywebsites.azurewebsites.net</a>, donde puede crear inmediatamente y de forma gratuita una aplicación básica de ASP.NET de corta duración en el Servicio de aplicaciones de Azure. No es necesario proporcionar ninguna tarjeta de crédito ni asumir ningún compromiso.

## <a id="nextsteps"></a> Pasos siguientes

Para más información acerca de las tres opciones de hospedaje web, consulte [Introducción a Microsoft Azure](../fundamentals-introduction-to-azure.md).

Para conocer con mayor profundidad las opciones que ha elegido para su aplicación, consulte los recursos siguientes:

* [Servicio de aplicaciones de Azure](/documentation/services/app-service/)
* [Servicios en la nube de Azure](/documentation/services/cloud-services/)
* [Máquinas virtuales de Azure](/documentation/services/virtual-machines/)
* [Service Fabric](/documentation/services/service-fabric)

<!-- URL List -->

[Servicio de aplicaciones de Azure]: /services/app-service/
[Servicios en la nube]: http://go.microsoft.com/fwlink/?LinkId=306052
[Máquinas virtuales]: http://go.microsoft.com/fwlink/?LinkID=306053
[Service Fabric]: /services/service-fabric
[ClearDB]: http://www.cleardb.com/
[WebJobs]: http://go.microsoft.com/fwlink/?linkid=390226&clcid=0x409
[Trabajos web]: http://go.microsoft.com/fwlink/?linkid=390226&clcid=0x409
[Configuring an SSL certificate for an Azure Website]: http://www.windowsazure.com/develop/net/common-tasks/enable-ssl-web-site/
[azurestore]: http://www.windowsazure.com/gallery/store/
[scripting]: http://www.windowsazure.com/documentation/scripts/?services=web-sites
[dotnet]: http://www.windowsazure.com/develop/net/
[nodejs]: http://www.windowsazure.com/develop/nodejs/
[PHP]: http://www.windowsazure.com/develop/php/
[Python]: http://www.windowsazure.com/develop/python/
[servicebus]: http://www.windowsazure.com/documentation/services/service-bus/
[sqldatabase]: http://www.windowsazure.com/documentation/services/sql-database/
[Almacenamiento]: http://www.windowsazure.com/documentation/services/storage/

<!-- IMG List -->

[ChoicesDiagram]: ./media/choose-web-site-cloud-service-vm/Websites_CloudServices_VMs_3.png

<!---HONumber=AcomDC_0720_2016-->
