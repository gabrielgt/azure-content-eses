<properties
   pageTitle="Integración continua para Service Fabric | Microsoft Azure"
   description="Obtenga información general sobre cómo configurar la integración continua para una aplicación de Service Fabric mediante Visual Studio Team Services (VSTS)."
   services="service-fabric"
   documentationCenter="na"
   authors="mthalman-msft"
   manager="timlt"
   editor="" />
<tags
   ms.service="multiple"
   ms.devlang="dotnet"
   ms.topic="article"
   ms.tgt_pltfrm="na"
   ms.workload="multiple"
   ms.date="08/01/2016"
   ms.author="mthalman" />

# Configuración de la integración continua de una aplicación de Service Fabric mediante Visual Studio Team Services

En este artículo se describen los pasos para configurar la integración continua para una aplicación de Azure Service Fabric mediante Visual Studio Team Services (VSTS), a fin de asegurarse de que la aplicación se pueda compilar, empaquetar e implementar de una manera automática.

Este documento refleja el procedimiento actual y se espera que cambie con el tiempo.

## Requisitos previos

Para comenzar, asegúrese de lo siguiente:

1. Tiene acceso a una cuenta de Team Services; en caso contrario, [cree una](https://www.visualstudio.com/docs/setup-admin/team-services/sign-up-for-visual-studio-team-services).

2. Puede acceder a un proyecto de equipo de Team Services; en caso contrario, [cree uno](https://www.visualstudio.com/docs/setup-admin/create-team-project).

3. Cuenta con un clúster de Service Fabric en el que puede implementar la aplicación; en caso contrario, cree uno mediante el [Portal de Azure](service-fabric-cluster-creation-via-portal.md), una [plantilla de Azure Resource Manager](service-fabric-cluster-creation-via-arm.md) o [Visual Studio](service-fabric-cluster-creation-via-visual-studio.md).

4. Ya ha creado un proyecto de aplicación de Service Fabric (.sfproj). Debe tener un proyecto creado o actualizado con el SDK de Service Fabric 2.1 o una versión posterior (el archivo .sfproj debe contener un valor de propiedad ProjectVersion de 1.1 o superior).

>[AZURE.NOTE] Ya no se requieren agentes de compilación personalizados. Ahora, los agentes hospedados de Team Services vienen preinstalados con el software de administración de clústeres de Service Fabric, con lo que las aplicaciones pueden implementarse directamente desde dichos agentes.

## Configuración y uso compartido de los archivos de origen

En primer lugar, se recomienda preparar un perfil de publicación que se utilice durante el proceso de implementación que se ejecutará en Team Services. El perfil de publicación debe configurarse para que tenga como destino el clúster que preparó anteriormente:

1.	Elija un perfil de publicación en el proyecto de aplicación que quiera utilizar para el flujo de trabajo de integración continua y siga las [instrucciones](service-fabric-publish-app-remote-cluster.md) sobre cómo publicar una aplicación en un clúster remoto. En realidad, no hace falta publicar la aplicación. Basta con hacer clic en el hipervínculo **Guardar** del cuadro de diálogo Publicar cuando haya terminado de configurar correctamente las opciones.
2.	Si quiere que la aplicación se actualice durante cada implementación que se realice en Team Services, tendrá que configurar el perfil de publicación para habilitar la opción de actualización. En el mismo cuadro de diálogo Publicar del paso 1, asegúrese de activar la casilla **Actualizar la aplicación**. Obtenga más información sobre [cómo configurar más opciones de actualización](service-fabric-visualstudio-configure-upgrade.md). Haga clic en el hipervínculo **Guardar** para guardar la configuración en el perfil de publicación.
3.	No se olvide de guardar los cambios en el perfil de publicación y de hacer clic en la opción Cancelar del cuadro de diálogo Publicar.
4.	Ya puede [compartir los archivos de origen del proyecto de aplicación](https://www.visualstudio.com/docs/setup-admin/team-services/connect-to-visual-studio-team-services#vs) con Team Services. Cuando pueda acceder a los archivos de origen en Team Services, podrá avanzar al paso siguiente sobre generación de compilaciones.

## Creación de una definición de compilación

Una definición de compilación de Team Services describe un flujo de trabajo compuesto por una serie de pasos de compilación que se ejecutan de manera secuencial. El objetivo de la definición de compilación que va a crearse consiste en generar un paquete de aplicación de Service Fabric, además de incluir otros archivos complementarios, que pueden utilizarse para implementar finalmente la aplicación en un clúster. Obtenga más información sobre las [definiciones de compilación](https://www.visualstudio.com/docs/build/define/create) de Team Services.

### Creación de una definición de la plantilla de compilación

1.	Abra el proyecto de equipo en Visual Studio Team Services.
2.	Seleccione la pestaña **Compilar**.
3.	Haga clic en el signo **+** verde para crear una nueva definición de compilación.
4.	En el cuadro de diálogo que se abre, seleccione la opción **Aplicación de Azure Service Fabric** en la categoría de plantilla **Compilar**.
5.	Seleccione **Siguiente**.
6.	Seleccione el repositorio y la rama asociados a la aplicación de Service Fabric.
7.	Seleccione la cola del agente que quiera usar. Se admiten agentes hospedados.
8.	Seleccione **Crear**.
9. Guarde la definición de compilación y asígnele un nombre.
10. A continuación, se muestra una descripción de los pasos de compilación que se generan con la plantilla:

| Paso de compilación | Descripción |
| --- | --- |
| Nuget restore (Restauración de NuGet) | Restaura los paquetes de NuGet de la solución. |
| Build solution *.sln (Compilar solución *.sln) | Compila la solución completa. |
| Build solution *.sln (Compilar solución *.sfproj) | Genera el paquete de aplicación de Service Fabric que se utilizará para implementar la aplicación. Tenga en cuenta la ubicación del paquete de aplicación estará en el directorio de artefactos de la compilación. |
| Update Service Fabric App Versions (Actualizar versiones de la aplicación de Service Fabric) | Actualiza los valores de versión de los archivos de manifiesto del paquete de aplicación para habilitar la opción de actualización. Para obtener más información, consulte la [página de documentación de tareas](https://go.microsoft.com/fwlink/?LinkId=820529). |
| Copiar archivos | Copia los archivos de parámetros de la aplicación y el perfil de publicación en los artefactos de la compilación para que puedan utilizarse durante la implementación. |
| Publish Artifact (Publicar artefacto) | Publica los artefactos de la compilación. Gracias a esto, las definiciones de versión podrán utilizar los artefactos de la compilación. |

### Comprobación del conjunto predeterminado de tareas

1.	Compruebe el campo de entrada **Solución** de los pasos de compilación **Nuget restore** (Restauración de NuGet) y **Compilar solución**. De forma predeterminada, estos pasos de compilación se ejecutarán en todos los archivos de solución del repositorio asociado. Si solo quiere que la definición de compilación se utilice en uno de los archivos de solución, debe actualizar expresamente la ruta a dicho archivo.
2.	Compruebe el campo de entrada **Solución** del paso de compilación **Package application (Empaquetar aplicación)**. De forma predeterminada, en este paso de compilación se da por hecho que solo hay un proyecto de aplicación de Service Fabric (.sfproj) en el repositorio. Si tiene varios archivos de este tipo en el repositorio y solo quiere seleccionar como destino uno de ellos en esta definición de compilación, debe actualizar expresamente la ruta a ese archivo. Si quiere empaquetar varios proyectos de aplicación en el repositorio, debe crear más pasos de **compilación de Visual Studio** en las definiciones de compilación que tengan como destino un proyecto de aplicación. Después, tendría que actualizar el campo **MSBuild Arguments** de cada uno de esos pasos de compilación para que la ubicación del paquete sea única en cada uno de ellos.
3.	Compruebe el comportamiento de control de versiones definido en el paso de compilación **Update Service Fabric App Versions** (Actualizar versiones de la aplicación de Service Fabric). De forma predeterminada, en este paso de compilación se anexa el número de compilación a todos los valores de versión de los archivos de manifiesto del paquete de aplicación. Para obtener más información, consulte la [página de documentación de tareas](https://go.microsoft.com/fwlink/?LinkId=820529). Esto resulta útil para habilitar la opción de actualización de la aplicación, ya que cada implementación de actualización requiere valores de versión distintos de la implementación anterior. Si no pretende usar la opción de actualización de la aplicación en el flujo de trabajo, puede plantearse deshabilitar este paso de compilación. De hecho, debe deshabilitarse si pretende producir una compilación que se puede utilizar para sobrescribir una aplicación de Service Fabric existente, ya que se producirá un error si la versión de la aplicación generada por la compilación no coincide con la versión de la aplicación en el clúster.
4.	Si la solución contiene un proyecto de .NET Core, debe asegurarse de que la definición de compilación contiene un paso de compilación que restaure las dependencias definidas por los archivos project.json. Para ello, siga estos pasos.
   1. Seleccione **Agregar el paso de compilación**.
   2. Busque la **línea de comandos** dentro de la pestaña Utilidad y haga clic en el botón Agregar.
   3. Para los campos de entrada de la tarea, utilice los siguientes valores:
      1. Herramienta: dotnet
      2. Argumentos: restore
   4. Arrastre la tarea para que esté inmediatamente después del paso **Nuget restore** (Restauración de NuGet).
5.	Guarde los cambios realizados en la definición de compilación.

### Pruébelo

Seleccione **Poner compilación en cola** para iniciar manualmente una compilación. También se desencadenarán compilaciones tras la inserción o protección. Cuando haya comprobado que la compilación se ejecuta correctamente, podrá avanzar al paso de creación de una definición de versión que implementará la aplicación en un clúster.

## Creación de una definición de versión

Una definición de versión de Team Services describe un flujo de trabajo compuesto por una serie de tareas que se ejecutan de manera secuencial. El objetivo de la definición de versión que va a crear consiste en seleccionar un paquete de aplicación e implementarlo en un clúster. Cuando se usan juntas, la definición de compilación y la de versión pueden ejecutar el flujo de trabajo completo empezando por los archivos de origen y terminando por la ejecución de una aplicación en el clúster. Obtenga más información sobre las [definiciones de versión](https://www.visualstudio.com/docs/release/author-release-definition/more-release-definition) de Team Services.

### Creación de una definición de la plantilla de versión

1.	Abra el proyecto en Visual Studio Team Services.
2.	Seleccione la pestaña **Versión**.
3.	Haga clic en el signo **+** verde para generar una nueva definición de versión y seleccione **Crear definición de versión** en el menú.
4.	En el cuadro de diálogo que se abre, seleccione la opción **Aplicación de Azure Service Fabric** en la categoría de plantilla **Implementación**.
5.	Seleccione **Siguiente**.
6.	Seleccione la definición de compilación que quiera utilizar como origen de esta definición de versión. La definición de versión hará referencia a los artefactos que se crearon con la definición de compilación seleccionada.
7.	Active la casilla **Implementación continua** si quiere que Team Services cree automáticamente una nueva versión e implemente la aplicación de Service Fabric cuando se complete una compilación.
8.	Seleccione la cola del agente que quiera usar. Se admiten agentes hospedados.
9.	Seleccione **Crear**.
10.	Edite el nombre de la definición haciendo clic en el icono de lápiz de la parte superior de la página.
11.	Seleccione el clúster en el que quiera que se implemente la aplicación. Esto se realiza en el campo de entrada **Cluster Connection** (Conexión de clúster) de la tarea. La conexión de clúster proporciona la información necesaria que permite que la tarea de implementación se conecte al clúster. Si aún no dispone de una conexión de clúster para el clúster, seleccione el hipervínculo **Administrar** junto al campo para agregar uno. En la página que se abre, realice los pasos siguientes:
    1. Seleccione **Nuevo punto de conexión de servicio** y, después, elija **Azure Service Fabric** en el menú.
    2. Seleccione el tipo de autenticación que utilizará el clúster que tiene como destino este punto de conexión.
    2. Defina un nombre para la conexión en el campo **Nombre de la conexión**. Normalmente, utilizará el nombre del clúster.
    3. Defina la URL del punto de conexión del cliente en el campo **Punto de conexión de clúster**. Ejemplo: https://contoso.westus.cloudapp.azure.com:19000.
    4. Para las credenciales de Azure Active Directory, defina las que quiera utilizar para conectarse al clúster en los campos **Nombre de usuario** y **Contraseña**.
    5. Para la autenticación basada en certificados, defina la codificación Base64 del archivo de certificado de cliente en el campo **Certificado de cliente**. Consulte la ventana emergente de ayuda de ese campo para saber cómo obtener ese valor. Si el certificado está protegido por contraseña, defina la contraseña en el campo **Contraseña**.
    6. Confirme los cambios haciendo clic en **Aceptar**. Cuando regrese al paso de definición de versión, haga clic en el icono de actualización del campo **Cluster Connection** (Conexión de clúster) para ver el punto de conexión que acaba de agregar.
12.	Guarde la definición de versión.

La definición que se crea está formada por una tarea de tipo **Deploy Service Fabric Application** (Implementar aplicación de Service Fabric). Para obtener más información sobre esta tarea, consulte la [página de documentación de tareas](https://go.microsoft.com/fwlink/?LinkId=820528).

### Comprobación de los valores predeterminados de la plantilla

1.	Compruebe el campo de entrada **Perfil de publicación** de la tarea **Deploy Service Fabric Application** (Implementar aplicación de Service Fabric). De forma predeterminada, este campo hace referencia a un perfil de publicación denominado "Cloud.xml" que se encuentra en los artefactos de la compilación. Si quiere hacer referencia a otro perfil de publicación o si la compilación contiene varios paquetes de aplicación en los artefactos, debe actualizar la ruta de forma adecuada.
2.	Compruebe el campo de entrada **Paquete de la aplicación** de la tarea **Deploy Service Fabric Application** (Implementar aplicación de Service Fabric). De forma predeterminada, este campo hace referencia a la ruta predeterminada del paquete de aplicación que se utiliza en la plantilla de definición de compilación. Si ha modificado la ruta predeterminada del paquete de aplicación en la definición de compilación, aquí también debe actualizar la ruta de forma adecuada.

### Pruébelo

Seleccione la opción **Crear versión** del menú de botón **Versión** para generar manualmente una versión. En el cuadro de diálogo que se abre, seleccione la compilación en la que quiera basar la versión; después, haga clic en **Crear**. Si habilitó la implementación continua, las versiones también se crearán automáticamente cuando la definición de compilación asociada complete una compilación.

## Pasos siguientes

Para obtener más información sobre la integración continua con las aplicaciones de Service Fabric, lea los artículos siguientes:

 - [Página de inicio de la documentación de Team Services](https://www.visualstudio.com/docs/overview)
 - [Administración de compilaciones en Team Services](https://www.visualstudio.com/docs/build/overview)
 - [Administración de versiones en Team Services](https://www.visualstudio.com/docs/release/overview)

<!---HONumber=AcomDC_0803_2016-->