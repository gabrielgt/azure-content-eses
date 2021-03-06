<properties
	pageTitle="Servicios de dominio de Azure AD: creación del grupo de administradores de controlador de dominio de AAD | Microsoft Azure"
	description="Introducción a los Servicios de dominio de Azure Active Directory (versión preliminar)"
	services="active-directory-ds"
	documentationCenter=""
	authors="mahesh-unnikrishnan"
	manager="stevenpo"
	editor="curtand"/>

<tags
	ms.service="active-directory-ds"
	ms.workload="identity"
	ms.tgt_pltfrm="na"
	ms.devlang="na"
	ms.topic="article"
	ms.date="07/06/2016"
	ms.author="maheshu"/>

# Servicios de dominio de Azure AD *(versión preliminar)*: creación del grupo "Administradores de controlador de dominio de AAD"

Este artículo le guía por las tareas de configuración necesarias para habilitar los Servicios de dominio de Azure AD para su inquilino de Azure AD.

## Paso 1: Creación del grupo "Administradores de controladores de dominio de AAD"
El primer paso es crear un grupo administrativo en el inquilino de Azure Active Directory. Este grupo administrativo especial se llama **Administradores de DC de AAD**. A los miembros de este grupo se les concederán privilegios administrativos en las máquinas unidas a un dominio para el dominio de los Servicios de dominio de Azure AD que va a configurar. Después de unirse a un dominio, este grupo se agregará al grupo 'Administradores' en estas máquinas unidas a un dominio. Además, los miembros de este grupo también podrá usar Escritorio remoto para conectarse de forma remota a las máquinas unidas a un dominio.

> [AZURE.NOTE] No cuenta con privilegios de administrador de dominio o administrador de empresa en el dominio administrado creado mediante los Servicios de dominio de Azure AD. Puesto que se trata de un dominio administrado, estos privilegios están reservados por el servicio y no están disponibles para los usuarios del directorio. Sin embargo, podrá usar el grupo de administradores especial creado en esta tarea de configuración para realizar algunas operaciones con privilegios. Estas operaciones incluyen unir equipos al dominio, formar parte del grupo de administradores en los equipos unidos a un dominio, configurar una directiva de grupo, etc.

En esta tarea de configuración, creará el grupo administrativo y agregará uno o varios usuarios del directorio al grupo. Realice los pasos siguientes para crear el grupo administrativo para los Servicios de dominio de Azure AD:

1. Desplácese al **Portal de Azure clásico** ([https://manage.windowsazure.com](https://manage.windowsazure.com)).

2. En el panel izquierdo, seleccione **Active Directory**.

3. Seleccione al inquilino (directorio) de Azure AD para el que quiere habilitar los Servicios de dominio de Azure AD. Tenga en cuenta que solo puede crear un dominio para cada directorio de Azure AD.

    ![Selección de un directorio de Azure AD](./media/active-directory-domain-services-getting-started/select-aad-directory.png)

4. Haga clic en la pestaña **Grupos**.

5. Haga clic en **Agregar grupo** en el panel de tareas de la parte inferior de la página, para agregar un grupo a su directorio.

6. Cree un grupo denominado **Administradores de DC de AAD**.

    > [AZURE.WARNING] Debe crear un grupo con este nombre exacto para permitir el acceso dentro de los Servicios de dominio de Azure AD.

	![Creación del grupo de administradores](./media/active-directory-domain-services-getting-started/create-admin-group.png)

7. Puede agregar una descripción para este grupo que permita a otros usuarios dentro del inquilino de Azure AD comprender que dicho grupo se usará para conceder privilegios administrativos dentro de los Servicios de dominio de Azure AD.

8. Después de crear el grupo, haga clic en su nombre para ver las propiedades. Haga clic en el botón **Agregar miembros** en el panel inferior, para agregar a los usuarios como miembros de este grupo.

9. En el cuadro de diálogo **Agregar miembros**, seleccione los usuarios que deben ser miembros de este grupo y active la casilla cuando haya terminado.

    ![Incorporación de usuarios al grupo de administradores](./media/active-directory-domain-services-getting-started/add-group-members.png)

<br>

## Tarea 2: Creación o selección de una red virtual de Azure.
La siguiente tarea de configuración es [crear o seleccionar una red virtual de Azure](active-directory-ds-getting-started-vnet.md).

<!---HONumber=AcomDC_0706_2016-->