<properties
	pageTitle="Implementar un servicio web de Aprendizaje automático de Microsoft Azure | Microsoft Azure"
	description="Cómo convertir un experimento de entrenamiento en un experimento predictivo, prepararlo para la implementación y luego implementarlo como servicio web de Aprendizaje automático de Azure."
	services="machine-learning"
	documentationCenter=""
	authors="garyericson"
	manager="jhubbard"
	editor="cgronlun"/>

<tags
	ms.service="machine-learning"
	ms.workload="data-services"
	ms.tgt_pltfrm="na"
	ms.devlang="na"
	ms.topic="article"
	ms.date="07/06/2016"
	ms.author="garye"/>

# Implementar un servicio web de Aprendizaje automático de Azure

Aprendizaje automático de Azure permite compilar, probar e implementar soluciones de análisis predictivo.

Desde una perspectiva general, esto se realiza en tres pasos:

- **[Crear un experimento de formación]**: el Estudio de aprendizaje automático de Azure es un entorno de desarrollo visual de colaboración que se utiliza para entrenar y probar un modelo de análisis predictivo con los datos de entrenamiento que proporcione.
- **[Convertirlo en un experimento predictivo]**: una vez que se ha entrenado el modelo con datos existentes y está listo para usarse con el objetivo de puntuar nuevos datos, debe prepararlo y simplificarlo para realizar predicciones.
- **Implementarlo como un servicio web**: puede implementar el experimento de puntuación como un servicio web de Azure [nuevo] o [clásico]. Los usuarios pueden enviar datos al modelo y recibir las predicciones de su modelo.

[AZURE.INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## Crear un experimento de entrenamiento

Para entrenar un modelo de análisis predictivo, utilice el Estudio de aprendizaje automático de Azure para crear un experimento de entrenamiento en el que incluya varios módulos para cargar los datos de entrenamiento, prepare los datos según sea necesario, aplique los algoritmos de aprendizaje automático y evalúe los resultados. Puede iterar en un experimento y probar algoritmos distintos de aprendizaje automático para comparar y evaluar los resultados.

El proceso de creación y administración de experimentos de entrenamiento se trata más detenidamente en otros artículos; vea los siguientes artículos para obtener más información y ejemplos:

- [Creación de un experimento sencillo en el Estudio de aprendizaje automático de Azure](machine-learning-create-experiment.md)
- [Desarrollo de una solución predictiva con Aprendizaje automático de Azure](machine-learning-walkthrough-develop-predictive-solution.md)
- [Importar datos de entrenamiento en Estudio de aprendizaje automático de Azure](machine-learning-data-science-import-data.md)
- [Administrar iteraciones de experimentos en Estudio de aprendizaje automático de Azure](machine-learning-manage-experiment-iterations.md)

## Convertir un experimento de entrenamiento en experimento predictivo

Una vez entrenado el modelo, está listo para usarlo para puntuar nuevos datos. Para ello, convierta el experimento de entrenamiento en un experimento predictivo.

Al efectuar la conversión a un experimento predictivo, estará preparando el modelo entrenado para implementarlo como servicio web de puntuación. Los usuarios del servicio web enviarán datos de entrada a su modelo y el modelo devolverá los resultados de predicción. Por lo tanto, cuando efectúe la conversión a un experimento predictivo, deberá tener en cuenta cómo espera que usen el modelo los demás.

Para convertir su experimento de entrenamiento en un experimento predictivo, haga clic en **Ejecutar** en la parte inferior del lienzo de experimento, haga clic en **Configurar servicio web** y luego en **Servicio web predictivo**.

![Convertir en experimento de puntuación](./media/machine-learning-publish-a-machine-learning-web-service/figure-1.png)

Para obtener más información sobre cómo realizar esta conversión, consulte [Convertir un experimento de entrenamiento en Aprendizaje automático en un experimento predictivo](machine-learning-convert-training-experiment-to-scoring-experiment.md).

En los pasos siguientes se muestra cómo implementar el experimento predictivo como servicio web nuevo.

A continuación, se describe el proceso de implementación de un experimento de predicción como servicio web [nuevo]. También puede implementarlo como servicio web [clásico].

## Implementación del experimento predictivo como servicio web nuevo

Ahora que ha preparado el experimento predictivo suficientemente, puede implementarlo como servicio web de Azure. Mediante el servicio web, los usuarios pueden enviar datos a su modelo y el modelo devolverá las predicciones.

Para implementar un experimento predictivo, haga clic en la opción **Ejecutar** de la parte inferior del lienzo del experimento. Cuando el experimento haya terminado de ejecutarse, haga clic en **Deploy Web Service** (Implementar servicio web) y seleccione **Deploy Web Service [New]** (Implementar un servicio web [nuevo]). Se abrirá la página de implementación del portal de servicios web de Aprendizaje automático.

### Página de implementación de experimentos del portal de servicios web de Aprendizaje automático
En la página de implementación de experimentos, escriba un nombre para el servicio web. Seleccione un plan de tarifa. Si ya tiene uno, puede seleccionarlo; si no, debe crear uno nuevo para el servicio.

1.	En el menú desplegable **Price Plan** (Plan de precios), seleccione un plan existente o elija la opción **Select new plan** (Seleccionar nuevo plan).
2.	En **Nombre del plan**, escriba un nombre que identifique el plan en la factura.
3.	Seleccione uno de los **niveles de planes mensuales**. Tenga en cuenta que los niveles de los planes predeterminados son los de la región predeterminada y que el servicio web se implementa en dicha región.

Haga clic en las páginas **Implementar** e **Inicio rápido** del servicio web que se abre.

A través de la página Inicio rápido del servicio web podrá acceder a las tareas más comunes que se realizarán después de crear un servicio web nuevo, así como instrucciones sobre cómo hacerlo. También puede acceder fácilmente a las páginas de prueba y de consumo.

<!-- ![Deploy the web service](./media/machine-learning-publish-a-machine-learning-web-service/figure-2.png)-->

### Pruebas del servicio web

Para probar el nuevo servicio web, haga clic en la opción **Test web service** (Probar servicio web) de las tareas comunes. En la página de prueba puede probar el servicio web como servicio de solicitud-respuesta (RRS) o de ejecución por lotes (BES).

En la página de pruebas RRS se muestran las entradas, las salidas y los parámetros globales definidos para el experimento. Para probar el servicio web, puede escribir manualmente los valores adecuados de las entradas, o bien proporcionar un archivo con formato de valores separados por comas (CSV) que contenga los valores de prueba.

Para realizar pruebas RRS, en el modo de vista de lista, escriba los valores adecuados de las entradas y haga clic en **Test Request-Response** (Probar solicitud-respuesta). Los resultados de predicción se mostrarán a la izquierda de la columna de salidas.

![Implementación del servicio web](./media/machine-learning-publish-a-machine-learning-web-service/figure-5-test-request-response.png)

Para realizar pruebas BES, haga clic en **Lote**. En la página de pruebas por lotes, haga clic en la opción Examinar de la entrada y seleccione un archivo CSV que contenga los valores de ejemplo adecuados. Si no dispone de un archivo CSV y ha creado el experimento predictivo con Estudio de aprendizaje automático de Microsoft Azure, puede descargar el conjunto de datos del experimento predictivo y utilizarlo.

Para ello, abra Estudio de aprendizaje automático de Microsoft Azure. Abra el experimento predictivo y haga clic con el botón derecho en la entrada del experimento. En el menú contextual, seleccione **conjunto de datos** y, después, haga clic en **Descargar**.

![Implementación del servicio web](./media/machine-learning-publish-a-machine-learning-web-service/figure-7-mls-download.png)

Haga clic en **Probar**. El estado del trabajo de ejecución por lotes se mostrará a la derecha de **Test Batch Jobs** (Trabajos de pruebas por lotes).

![Implementación del servicio web](./media/machine-learning-publish-a-machine-learning-web-service/figure-6-test-batch-execution.png)

<!--![Test the web service](./media/machine-learning-publish-a-machine-learning-web-service/figure-3.png)-->

En la página **CONFIGURACIÓN**, puede cambiar la descripción y el título, actualizar la clave de la cuenta de almacenamiento, y habilitar los datos de ejemplo para el servicio web.

![Configurar el servicio web](./media/machine-learning-publish-a-machine-learning-web-service/figure-8-arm-configure.png)

Una vez que haya implementado el servicio web, puede hacer lo siguiente:

- **Acceder** a él través de la API del servicio web
- **Administrarlo** a través del portal de servicios web de Aprendizaje automático de Azure o el portal de Azure clásico
- **Actualizarlo** si cambia el modelo

### Acceso al servicio web

Cuando implementa el servicio web desde el Estudio de aprendizaje automático, puede enviar datos al servicio y recibir respuestas mediante programación.

La página **Consume** (Consumo) proporciona toda la información que necesita para acceder al servicio web. Por ejemplo, la clave de API se ofrece para permitir el acceso autorizado al servicio.

Para obtener más información sobre el acceso a un servicio web de Aprendizaje automático, vea [Cómo consumir un servicio web de Aprendizaje automático de Azure implementado](machine-learning-consume-web-services.md).

### Administración de servicios web nuevos

Puede administrar los servicios web clásicos mediante el portal de servicios web de Aprendizaje automático. En la [página principal del portal](https://services.azureml-test.net/), haga clic en **Servicios web**. En la página de servicios web, puede eliminar o copiar servicios. Para supervisar un servicio concreto, haga clic en el servicio y, después, haga clic en **Panel**. Para supervisar los trabajos por lotes asociados con el servicio web, haga clic en **Batch Request Log** (Registro de solicitudes por lotes).

## Implementación del experimento predictivo como servicio web clásico

Ahora que ha preparado el experimento predictivo suficientemente, puede implementarlo como servicio web de Azure. Mediante el servicio web, los usuarios pueden enviar datos a su modelo y el modelo devolverá las predicciones.

Para publicar su experimento predictivo, haga clic en **Ejecutar** en la parte inferior del lienzo del experimento y luego haga clic en **Implementar servicio web**. El servicio web está configurado y se colocará en el panel del servicio web.

![Implementación del servicio web](./media/machine-learning-publish-a-machine-learning-web-service/figure-2.png)

Para probar el servicio web, haga clic en el vínculo **Probar** del panel del servicio web. Aparecerá un cuadro de diálogo que le pide los datos de entrada del servicio. Estas son las columnas esperadas del experimento puntuación. Escriba un conjunto de datos y haga clic en **Aceptar**. Los resultados generados por el servicio web se muestran en la parte inferior del panel.

![Prueba del servicio web](./media/machine-learning-publish-a-machine-learning-web-service/figure-3.png)

En la pestaña **CONFIGURACIÓN** puede cambiar el nombre para mostrar del servicio y darle una descripción. El nombre y la descripción se muestran en el [Portal de Azure clásico](http://manage.windowsazure.com/), donde se administran los servicios web.

Puede proporcionar una descripción para la entrada de datos, los datos de salida y los parámetros de servicio web al escribir una cadena para cada columna en **INPUT SCHEMA**, **OUTPUT SCHEMA** y **WEB SERVICE PARAMETER**. Estas descripciones se utilizan en la documentación de código de ejemplo proporcionada para el servicio web. También puede habilitar el registro para diagnosticar los errores que ve al acceder a su servicio web.

Para más información, vea [Habilitar el registro para los servicios web de Aprendizaje automático](machine-learning-web-services-logging.md).

![Configurar el servicio web](./media/machine-learning-publish-a-machine-learning-web-service/figure-4.png)

### Acceso al servicio web

Cuando implementa el servicio web desde el Estudio de aprendizaje automático, puede enviar datos al servicio y recibir respuestas mediante programación.

El panel proporciona toda la información que necesita para tener acceso a su servicio web. Por ejemplo, la clave de API se proporciona para permitir el acceso autorizado al servicio, y las páginas de ayuda de API sirven para ayudarle a empezar a escribir el código.

Para obtener más información sobre el acceso a un servicio web de Aprendizaje automático, vea [Cómo consumir un servicio web de Aprendizaje automático de Azure implementado](machine-learning-consume-web-services.md).

### Administrar el servicio web en el Portal de Azure clásico

En el [Portal de Azure clásico](http://manage.windowsazure.com/), puede administrar los servicios web haciendo clic en el servicio **Aprendizaje automático** abriendo el área de trabajo de Aprendizaje automático y, luego, el servicio web desde la pestaña **SERVICIOS WEB**. Desde esta página, puede supervisar el servicio web, actualizarlo y eliminarlo. También puede agregar un segundo extremo para el servicio web además del extremo predeterminado que se crea cuando se implementa.

Para más información, consulte [Administrar un área de trabajo de Aprendizaje automático de Azure](machine-learning-manage-workspace.md).
<!-- When this article gets published, fix the link and uncomment
For more information on how to manage Azure Machine Learning web service endpoints using the REST API, see **Azure machine learning web service endpoints**.
-->

## Actualizar el servicio web

Puede realizar cambios en el servicio web, como actualizar el modelo con datos de entrenamiento adicionales y volver a implementarlo, sobrescribiendo el servicio web original.

Para actualizar el servicio web, abra el experimento predictivo original que usó para implementar el servicio web y haga una copia modificable haciendo clic en **GUARDAR COMO**. Realice los cambios y haga clic en **Publicar servicio web**.

Como ya ha implementado este experimento antes, se le preguntará si quiere sobrescribir (servicio web clásico) o actualizar (servicio web nuevo) el servicio existente. Al hacer clic en **SÍ** o **Actualizar**, el servicio web existente se detendrá y, en su lugar, se implementará el nuevo experimento predictivo.

> [AZURE.NOTE] Si ha realizado cambios de configuración en el servicio web original, como, por ejemplo, escribir un nuevo nombre para mostrar o una descripción, necesitará escribir esos valores de nuevo.

Una opción para actualizar el servicio web es volver a entrenar el modelo mediante programación. Para obtener más información, consulte [Volver a entrenar modelos de aprendizaje automático mediante programación](machine-learning-retrain-models-programmatically.md).


<!-- internal links -->
[Crear un experimento de formación]: #create-a-training-experiment
[Convertirlo en un experimento predictivo]: #convert-the-training-experiment-to-a-predictive-experiment
[new]: #deploy-the-predictive-experiment-as-a-new-web-service
[nuevo]: #deploy-the-predictive-experiment-as-a-new-web-service
[clásico]: #deploy-the-predictive-experiment-as-a-new-web-service
[Access]: #access-the-web-service
[Manage]: #manage-the-web-service-in-the-azure-management-portal
[Update]: #update-the-web-service

<!---HONumber=AcomDC_0914_2016-->