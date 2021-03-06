<properties
	pageTitle="Tutorial: integración de Azure Active Directory con BetterWorks | Microsoft Azure"
	description="Aprenda a configurar el inicio de sesión único entre Azure Active Directory y BetterWorks."
	services="active-directory"
	documentationCenter=""
	authors="jeevansd"
	manager="femila"
	editor=""/>

<tags
	ms.service="active-directory"
	ms.workload="identity"
	ms.tgt_pltfrm="na"
	ms.devlang="na"
	ms.topic="article"
	ms.date="07/11/2016"
	ms.author="jeedes"/>


# Tutorial: Integración de Azure Active Directory con BetterWorks

El objetivo de este tutorial es mostrar cómo integrar BetterWorks con Azure Active Directory (Azure AD).

La integración de BetterWorks con Azure AD proporciona las siguientes ventajas:

- Puede controlar en Azure AD quién tiene acceso a BetterWorks.
- Puede permitir que los usuarios inicien sesión automáticamente en BetterWorks (inicio de sesión único) con sus cuentas de Azure AD.
- Puede administrar sus cuentas en una ubicación central: el Portal de Azure clásico.

Si desea obtener más información sobre la integración de aplicaciones SaaS con Azure AD, vea [Qué es el acceso a las aplicaciones y el inicio de sesión único en Azure Active Directory](active-directory-appssoaccess-whatis.md).

## Requisitos previos

Para configurar la integración de Azure AD con BetterWorks, necesita los siguientes elementos:

- Una suscripción de Azure AD
- Una suscripción habilitada para inicio de sesión único en BetterWorks


> [AZURE.NOTE] Para probar los pasos de este tutorial, no se recomienda el uso de un entorno de producción.


Para probar los pasos de este tutorial, debe seguir estas recomendaciones:

- No debe usar el entorno de producción, a menos que sea necesario.
- Si no dispone de un entorno de prueba de Azure AD, puede obtener una versión de prueba de un mes [aquí](https://azure.microsoft.com/pricing/free-trial/).


## Descripción del escenario
El objetivo de este tutorial es permitirle probar el inicio de sesión único de Azure AD en un entorno de prueba.

La situación descrita en este tutorial consta de dos bloques de creación principales:

1. Adición de BetterWorks desde la galería
2. Configuración y comprobación del inicio de sesión único de Azure AD


## Adición de BetterWorks desde la galería
Para configurar la integración de BetterWorks en Azure AD, es preciso agregar BetterWorks desde la galería a la lista de aplicaciones SaaS administradas.

**Para agregar BetterWorks desde la galería, siga estos pasos:**

1. En el panel de navegación izquierdo del **Portal de Azure clásico**, haga clic en **Active Directory**.

	![Active Directory][1]

2. En la lista **Directory**, seleccione el directorio cuya integración desee habilitar.

3. Para abrir la vista de aplicaciones, haga clic en **Applications**, en el menú superior de la vista de directorios.
	
	![Aplicaciones][2]

4. Haga clic en **Agregar** en la parte inferior de la página.
	
	![Aplicaciones][3]

5. En el cuadro de diálogo **¿Qué desea hacer?**, haga clic en **Agregar una aplicación de la galería**.

	![Aplicaciones][4]

6. En el cuadro de búsqueda, escriba **BetterWorks**.

	![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_01.png)

7. En el panel de resultados, seleccione **BetterWorks** y, luego, haga clic en **Completar** para agregar la aplicación.

	![Selección de la aplicación en la galería](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_001.png)

##  Configuración y comprobación del inicio de sesión único de Azure AD
El objetivo de esta sección es mostrar cómo configurar y probar el inicio de sesión único de Azure AD con BetterWorks con un usuario de prueba llamado "Britta Simon".

Para que el inicio de sesión único funcione, Azure AD debe saber cuál es el usuario homólogo de BetterWorks para un usuario de Azure AD. Es decir, es preciso establecer una relación de vínculo entre un usuario de Azure AD y el usuario relacionado de BetterWorks.

Esta relación de vínculo se establece asignando el valor del **nombre de usuario** en Azure AD como el valor del **nombre de usuario** en BetterWorks.

Para configurar y probar el inicio de sesión único de Azure AD con BetterWorks, es preciso completar los siguientes bloques de creación:

1. **[Configuración del inicio de sesión único de Azure AD](#configuring-azure-ad-single-single-sign-on)**: para permitir a los usuarios usar esta característica.
2. **[Creación de un usuario de prueba de Azure AD](#creating-an-azure-ad-test-user)**: para probar el inicio de sesión único de Azure AD con Britta Simon.
3. **[Creación de un usuario de prueba de BetterWorks](#creating-a-betterworks-test-user)**: para tener un homólogo de Britta Simon en BetterWorks que esté vinculado a la representación de ella en Azure AD.
4. **[Asignación del usuario de prueba de Azure AD](#assigning-the-azure-ad-test-user)**: para permitir que Britta Simon use el inicio de sesión único de Azure AD.
5. **[Prueba del inicio de sesión único](#testing-single-sign-on)**: para comprobar si funciona la configuración.

### Configuración del inicio de sesión único de Azure AD

El objetivo de esta sección es habilitar el inicio de sesión único de Azure AD en el Portal de Azure clásico y configurar el inicio de sesión único en la aplicación BetterWorks.

La aplicación BetterWorks espera que las aserciones SAML se encuentren en un formato concreto. Configure las siguientes notificaciones para esta aplicación. Puede administrar el valor de estos atributos desde la pestaña **Atributo** de la aplicación. La siguiente captura de pantalla le muestra un ejemplo de esto.

![Configurar inicio de sesión único](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_06.png)

**Para configurar el inicio de sesión único de Azure AD con BetterWorks, realice los pasos siguientes:**

1. En el Portal de Azure clásico, en la página de integración de aplicaciones de **BetterWorks**, en el menú de la parte superior, haga clic en **Atributos**.

    ![Configurar inicio de sesión único](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_07.png)

2. En el cuadro de diálogo **Atributos de token de SAML**, para cada fila de la tabla siguiente, realice los pasos que se indican a continuación:
    

	| Nombre del atributo | Valor de atributo |
	| --- | --- |    
    | saml\_token | bd189cf6-1701-11e6-8f90-d26992eca2a5 |

	a. Haga clic en **agregar atributo de usuario** para abrir el cuadro de diálogo **Agregar atributo de usuario**.

	![Configurar inicio de sesión único](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_12.png)
	
	b. En el cuadro de texto **Nombre de atributo**, escriba el nombre de atributo que se muestra para esa fila.
	
	c. En la lista **Valor de atributo**, escriba el id. del token SAML que se muestra para esa fila.
	
	d. Haga clic en **Completar**.

3. En el menú de la parte superior, haga clic en **Inicio rápido**.

	![Configurar inicio de sesión único](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_11.png)

4. En la página **¿Cómo desea que los usuarios inicien sesión en BetterWorks?**, seleccione **Inicio de sesión único de Azure AD** y, a continuación, haga clic en **Siguiente**.
    
	![Configurar inicio de sesión único](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_03.png)

5. En la página de diálogo **Configurar las opciones de la aplicación**, si quiere configurar la aplicación en el **modo iniciado por el proveedor de identidades**, siga estos pasos:

    ![Configurar inicio de sesión único](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_04.png)


	a. En el cuadro de texto **Identificador**, escriba la dirección URL con el siguiente patrón: `https://app.betterworks.com/saml2/metadata/`


    b. En el cuadro de texto **URL de respuesta**, escriba la dirección URL con el siguiente patrón: `https://app.betterworks.com/saml2/acs/`


	c. Haga clic en **Siguiente**.

6. En la página de diálogo **Configurar las opciones de la aplicación**, si desea configurar la aplicación en el **modo iniciado por el proveedor de servicios**, siga estos pasos:

	![Configurar inicio de sesión único](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_10.png)

	a. Seleccione **Mostrar la configuración avanzada (opcional)**.



	b. En el cuadro de texto **URL de inicio de sesión**, escriba la dirección URL que usan los usuarios para iniciar sesión en su aplicación de BetterWorks con el siguiente patrón: `https://app.betterworks.com`

	b. Haga clic en **Siguiente**.

7. En la página **Configurar inicio de sesión único en BetterWorks**, lleve a cabo estos pasos y haga clic en **Siguiente**:

	![Configurar inicio de sesión único](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_05.png)

    a. Haga clic en **Descargar metadatos** y luego guarde el archivo en el equipo.

    b. Haga clic en **Siguiente**.

8. Si quiere configurar el inicio de sesión único para la aplicación, póngase en contacto con el equipo de soporte de BetterWorks a través de <mailto:support@betterworks.com>. Adjunte el archivo de metadatos descargado y compártalo con el equipo de BetterWorks para que le configure el inicio de sesión único.

9. En el portal clásico, seleccione la confirmación de la configuración de inicio de sesión único y haga clic en **Siguiente**.
    
	![Inicio de sesión único de Azure AD][10]

10. En la página **Confirmación del inicio de sesión único**, haga clic en **Completar**.
    
	![Inicio de sesión único de Azure AD][11]



### Creación de un usuario de prueba de Azure AD
El objetivo de esta sección es crear un usuario de prueba en el Portal clásico llamado Britta Simon.

![Creación de un usuario de Azure AD][20]

**Siga estos pasos para crear un usuario de prueba en Azure AD:**

1. En el panel de navegación izquierdo del **Portal de Azure clásico**, haga clic en **Active Directory**.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-betterworks-tutorial/create_aaduser_09.png)

2. En la lista **Directory**, seleccione el directorio cuya integración desee habilitar.

3. Para mostrar la lista de usuarios, en el menú de la parte superior, haga clic en **Usuarios**.
    
	![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-betterworks-tutorial/create_aaduser_03.png)

4. Para abrir el diálogo **Agregar usuario**, en la barra de herramientas de la parte inferior, haga clic en **Agregar usuario**.

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-betterworks-tutorial/create_aaduser_04.png)

5. En la página de diálogo **Proporcione información sobre este usuario**, realice los pasos siguientes:

    ![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-betterworks-tutorial/create_aaduser_05.png)

    a. En Tipo de usuario, seleccione Nuevo usuario de la organización.

    b. En el cuadro de texto **Nombre de usuario**, escriba **BrittaSimon**.

    c. Haga clic en **Siguiente**.

6.  En la página de diálogo **Perfil de usuario**, realice los siguientes pasos:
    
	![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-betterworks-tutorial/create_aaduser_06.png)

    a. En el cuadro de texto **Nombre**, escriba **Britta**.

    b. En el cuadro de texto **Apellidos**, escriba **Simon**.

    c. En el cuadro de texto **Nombre para mostrar**, escriba **Britta Simon**.

    d. En la lista **Rol**, seleccione **Usuario**.

    e. Haga clic en **Siguiente**.

7. En la página de diálogo **Obtener contraseña temporal**, haga clic en **Crear**.
    
	![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-betterworks-tutorial/create_aaduser_07.png)

8. En la página de diálogo **Obtener contraseña temporal**, realice los pasos siguientes:
    
	![Creación de un usuario de prueba de Azure AD](./media/active-directory-saas-betterworks-tutorial/create_aaduser_08.png)

    a. Anote el valor del campo **Nueva contraseña**.

    b. Haga clic en **Completo**.



### Creación de un usuario de prueba en BetterWorks

En esta sección, creará un usuario llamado Britta Simon en BetterWorks.

Colabore con el equipo de soporte técnico de BetterWorks a través de <mailto:support@betterworks.com> para agregar los usuarios a la plataforma BetterWorks.


### Asignación del usuario de prueba de Azure AD

El objetivo de esta sección es permitir que Britta Simon use el inicio de sesión único de Azure concediéndole acceso a BetterWorks.
	
   ![Asignar usuario][200]

**Para asignar Britta Simon a BetterWorks, realice los pasos siguientes:**

1. En el portal clásico, para abrir la vista de aplicaciones, en la vista del directorio, haga clic en **Aplicaciones** en el menú superior.
    
	![Asignar usuario][201]

2. En la lista de aplicaciones, seleccione **BetterWorks**.
    
	![Configurar inicio de sesión único](./media/active-directory-saas-betterworks-tutorial/tutorial_betterworks_50.png)

1. En el menú de la parte superior, haga clic en **Usuarios**.
    
	![Asignar usuario][203]

1. En la lista Usuarios, seleccione **Britta Simon**.

2. En la barra de herramientas de la parte inferior, haga clic en **Asignar**.
    
	![Asignar usuario][205]



### Prueba del inicio de sesión único

El objetivo de esta sección es probar la configuración del inicio de sesión único de Azure AD mediante el panel de acceso.
 
Al hacer clic en el icono de BetterWorks en el panel de acceso, debería iniciar sesión automáticamente en su aplicación BetterWorks.


## Recursos adicionales

* [Lista de tutoriales sobre cómo integrar aplicaciones SaaS con Azure Active Directory](active-directory-saas-tutorial-list.md)
* [¿Qué es el acceso a aplicaciones y el inicio de sesión único con Azure Active Directory?](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-betterworks-tutorial/tutorial_general_205.png

<!---HONumber=AcomDC_0713_2016-->