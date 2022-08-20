---
layout: default
title: "App Registration"
nav_order: 3
---

# ¿Cómo crear una App Registration en Azure y vincularla a Power BI? 

En los pasos siguientes vamos a ver como registrar una App en Azure Active Directory la cual nos permitirá que la plataforma de identidad de Microsoft nos provea servicios de autenticación y autorización. 
1. Como primer paso ingresamos al portal de [Azure](https://portal.azure.com/) y una vez dentro pulsamos en el menú ubicado en el margen superior izquierdo. 
<br>![app1](Media/App%20registration/menu%20azure.PNG)
2. Se desplegará un menú en donde buscamos y seleccionamos la opción *Azure Active Directory*. 
3. En la sección *Administrar*, seleccionamos la opción *Registro de Aplicaciones*.
4. En la nueva pantalla pulsamos en *Nuevo registro*.
<br>![app2](Media/App%20registration/nueva%20app.PNG)
5. Definimos un nombre a la aplicación. Recordemos que este será el nombre que se muestra al momento de pedir permisos de acceso a nuestra información básica, por lo que tenemos que ingresar un nombre significativo y acorde a la empresa. También en este paso tenemos la posibilidad de seleccionar quiénes se podrán autenticar a través de esta aplicación. Una vez completado pulsamos en *Registrar*. 
<br>![app3](Media/App%20registration/Registrar%20app.PNG)
6. En este momento ya podemos ver el *Id de la aplicación* (Copiar y conservar este valor). 
<br>![app4](Media/App%20registration/app%20id.PNG)
7. El próximo paso es generar la *Secret Key*. Para eso, ubicamos la sección de *Credenciales de cliente*, y pulsamos en Agregar un certificado o secreto. Tengamos en cuenta que este paso es necesario para configurar la conexión con *Service Principal*. 
8. Una vez dentro de *Certificados y secretos*, vamos a la sección de Secretos de cliente, donde pulsamos en el botón *Nuevo Secreto de Cliente*.
9. Luego, simplemente completamos la descripción a nuestro secreto, ingresamos un tiempo de caducidad y pulsamos en *Agregar*. 
<br>![app6](Media/App%20registration/nuevo%20secreto.PNG)
10. En este momento vamos a copiar el contenido del campo valor. Este se va a ver mientras permanezcamos en la página, una vez que cerremos o cambiemos no lo volveremos a ver, por lo que es muy importante que guardemos este valor para utilizarlo como *Secret Id* en la configuración de SimplePBIX
11. Para poder comunicarnos con Power BI tenemos que configurar los permisos de la aplicación que acabamos de registrar. Para eso en el panel de la izquierda buscamos Permisos de Api, pulsamos en *Agregar un Permiso*, y en la lista de los servicios seleccionamos *Power Bi Services*. 
<br>![app7](Media/App%20registration/agregar%20permisos.PNG)
12. Una vez seleccionada esa opción se nos va a desplegar una ventana donde debemos elegir el tipo de permiso que va a necesitar la aplicación creada. Para el caso de Service Principal de deployment seleccionamos *Permisos delegados*, luego seleccionamos los permisos *Read.WriteAll* sobre datasets, y por último aplicamos los cambios en *Agregar Permisos*.
<br>![app8](Media/App%20registration/permisos%20admin.PNG)
>*Nota: Estos permisos no serán requeridos para un Service Principal Administrador*
13. Por último, para poder comunicarnos por completo con los servicios de *Power Bi*, debemos acceder al portal de [*Power Bi*](https://app.powerbi.com/), ingresar a *Configuración, Portal de Administración* y en la ventana que nos aparece habilitar el *“allow service principals to use Power BI APIs”*.  
<br>![app14](Media/App%20registration/PBI%20embed%20content.png)
14. Tengamos en cuenta que para que poder utilizar un Service Principal Administrador, se tiene que habilitar el servicio de autenticación por API en el portal de Azure. En el siguiente enlace se describe como llevar a cabo esto, [Enable service principal authentication for read-only admin APIs](https://docs.microsoft.com/en-us/power-bi/admin/read-only-apis-service-principal-authentication).
Se puede obtener más información ingresando a: 
<a href="https://docs.microsoft.com/en-us/azure/active-directory/develop/quickstart-register-app?source=docs">Inicio rápido: registrar una aplicación en la plataforma de identidad de Microsoft | Documentos de Microsoft</a>