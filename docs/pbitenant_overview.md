---
layout: default
title: "TenantOverview"
nav_order: 5
---

# PBI Tenant Overview

El informe PBITenantOverview nos permite tener un primer vistazo a los componentes creados en la organización para comprender mejor el uso de Power Bi.

## Configuración

Para ver datos de nuestra organización primero debemos configurar el origen de datos. Si nos dirigimos a configurar las actualizaciones programadas de nuestro dataset o configuración del conjunto de datos encontraremos que tenemos credenciales pendientes para corregir.
Antes de editar esas credenciales de nuestros orígenes, primero debemos cambiar los parametros del informe.
El archivo del informe cuenta con parámetros de configuración.
![parametros](Media/PBI%20Tenant%20overview/config1.PNG)
- CredentialsExcel: dirección web de un excel con credenciales de un Service Principal que tenga permisos de administrador en Power Bi. Recomendamos el uso de Sharepoint o Onedrive puesto que sería información sensible.
- Logo: dirección web a una imagen que podemos usar como logo inicial. Sino por defecto aparecerá una de LaDataWeb.
- SimplePBIX_Key: key o clave enviada por correo al solicitar la demo.

#### Excel de credenciales

El archivo de credenciales es sumamente sencillo. Debemos abrir un excel y en su primera hoja crear una tabla que tenga tres columnas: 

TenantId | ClientId | SecretId

En la primera fila completamos los valores necesarios según nuestro Service Principal con permisos de administrador. Lo dejamos en un entorno accesible web y copiamos su dirección. En caso de estar usando Sharepoint o Onedrive puede ver este post sobre <a href="https://blog.ladataweb.com.ar/post/185337134590/alternativa-para-conectar-power-bi-a-onedrive">como obtener el enlace</a>.

>*Nota: dado que Power Bi no permite cifrar parámetros, usaremos un archivo excel cloud con ubicado donde usted lo desee con permisos y credenciales que puede setear al momento de actualizar para mantener la seguridad.*

## Credenciales de orígenes de datos

Una vez configurado los parámetros podremos editar las credenciales de los orígenes de datos. Vamos a mantener todas las credenciales con nivel de privacidad Organizacional que nos permitiría la vinculación entre los origines con ciertos grados de seguridad. Para el caso de el enlace de simplepbix y el login microsoft podrémos dejarlo como Anonymous puesto que sus chequeos se hacen en el request. Nuestro archivo excel podría requerir credenciales profesionales de Microsoft si siguieron la recomendación de Sharepoint y Onedrive. Por último, para el caso de credenciales de la API vamos a dejarlo anonymous pero hacer un skip del test de conexión.
![parametros](Media/PBI%20Tenant%20overview/config2.PNG)

Así concluimos la configuración y podemos iniciar el uso del informe corriendo una actualización del conjunto de datos.