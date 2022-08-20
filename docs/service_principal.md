---
layout: default
title: "Apps"
nav_order: 2
---
# Service Principals

Para tener un poco de contexto iniciamos dando a conocer un poco de Apps registradas y Service Principals de palabras de la documentación de Microsoft:
	Al registrar una aplicación en Azure Portal, se crean automáticamente un objeto de aplicación y un objeto de service principal en su inquilino principal. Si registra o crea una aplicación mediante las API de Microsoft Graph, la creación del objeto de service principal se hace en un paso independiente.
	Una aplicación de Azure AD se define por su único objeto de aplicación, que reside en el inquilino de Azure AD donde se registró la aplicación, (conocido como inquilino "principal" de la aplicación). El objeto de aplicación se usa como plantilla o plano técnico para crear uno o varios objetos de service principal. La service principal se crea en todos los inquilinos en los que se utiliza la aplicación. De forma similar a una clase en la programación orientada a objetos, el objeto de aplicación tiene algunas propiedades estáticas que se aplican a todas las entidades de servicio creadas (o instancias de aplicación).

Para poder implementar SimplePBIX en nuestro tenant será necesario registrar dos Apps.
- Service Principal para deploy: un app registrada con permisos mínimos y necesarios para que los servicios de LaDataWeb deployen los pbix en nuestro PowerBi Service.
- Service Principal Admin (depende): una app registrada con permisos de administración para actualizar el informes de SimplePBIX que lo requieran.

