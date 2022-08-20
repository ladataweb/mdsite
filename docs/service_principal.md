---
layout: default
title: "Service Principals"
nav_order: 2
---
# Service Principals

Para tener un poco de contexto iniciamos dando a conocer un poco de Apps registradas y Service Principals de palabras de la documentación de Microsoft:
	Al registrar una aplicación en Azure Portal, se crean automáticamente un objeto de aplicación y un objeto de service principal en su inquilino principal. Si registra o crea una aplicación mediante las API de Microsoft Graph, la creación del objeto de service principal se hace en un paso independiente.
	Una aplicación de Azure AD se define por su único objeto de aplicación, que reside en el inquilino de Azure AD donde se registró la aplicación, (conocido como inquilino "principal" de la aplicación). El objeto de aplicación se usa como plantilla o plano técnico para crear uno o varios objetos de service principal. La service principal se crea en todos los inquilinos en los que se utiliza la aplicación. De forma similar a una clase en la programación orientada a objetos, el objeto de aplicación tiene algunas propiedades estáticas que se aplican a todas las entidades de servicio creadas (o instancias de aplicación).

Para poder implementar SimplePBIX en nuestro tenant será necesario registrar dos Apps.
- Service Principal para deploy: un app registrada con permisos mínimos y necesarios para que los servicios de LaDataWeb deployen los pbix en nuestro PowerBi Service.
- Service Principal Admin (depende): una app registrada con permisos de administración para actualizar el informes de SimplePBIX que lo requieran.

## Service Principal para deploy

Luego de registrar una aplicación en azure como indica nuestra documentación o tantas otras numerosas que podemos encontrar en internet, vamos a determinar los permisos para ejecutar el deploy.
Permisos:
- **Portal Azure:** Dentro de la configuración de la App en el Azure Active Directory vamos a asignar un permiso delegado de Power Bi Service correspondiente a Dataset.ReadWrite.All. Éste es el único que necesitará para permitir a la aplicación publicar informes de SimplePBIX en un area de trabajo que nuestra App tenga accesos.
- **Power Bi Service:** para que nuestra aplicación puede ser usada efectivamente contra Power Bi necesitamos asegurarnos que los Service Principals tiene acceso a utilizar la Rest API. Para ello nos dirigimos a configuración -> Portal de Administración -> Tenant Settings.
![serviceprincipals](Media/Service%20principals/pbi_sp.PNG)
Bajo la opción de desarrollo encontraremos lo que tenemos que cambiar. Podemos permitir a toda la organización o en caso que querramos tenerlo más controlado, podríamos agregar a nuestra App dentro de un grupo de seguridad al cual le habilitaríamos la opción
- **Power Bi Service Workspace:** finalmente vamos a agregar nuestra App dentro del area de trabajo en la cual queremos tener implementado el informe. Hasta el momento el Service Principal no podía ejecutar muchas acciones pero al asignarle el workspace podría publicar sobre el mismo.
![workspaceaccess](Media/Service%20principals/workspace.PNG)
Será necesario que el permiso sea uno con escritura como es el caso de Admin o Member de lo contrario no podríamos publicar tal como sucedería con un usuario.

## Service Principal Admin 

De ser necesario, algunos informes de SimplePBIX van a necesitar acceso a la API con permisos de Administrador de Power Bi. Para ello necesitaremos la misma configuración de Power Bi Service antes mencionada y una más.
La configuración adicional restante es la que permitiría a un Service Principal usar la Admin Rest API como solo lectura. Antes de cambiar nuestro Power Bi será obligatorio crear un Grupo de Seguridad con la App incluida para poder asignarle la opción del Portal de Administración de Power Bi Service directamente. Para más información puede ver el detalle de la acción en la siguiente dirección de la documentación de Microsoft: https://docs.microsoft.com/es-es/power-bi/enterprise/read-only-apis-service-principal-authentication
