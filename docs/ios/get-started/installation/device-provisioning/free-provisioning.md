---
title: Aprovisionamiento gratuito
description: Con el lanzamiento de Apple de Xcode 7 se incluye un cambio importante para el aprovisionamiento gratuito de los desarrolladores de iOS y Mac.
ms.topic: article
ms.prod: xamarin
ms.assetid: A5CE2ECF-8057-49ED-8393-EB0C5977FE4C
ms.technology: xamarin-ios
author: asb3993
ms.author: amburns
ms.date: 03/19/2017
ms.openlocfilehash: 26ac40360b4e706180f4154f4fddcd9c992ad94b
ms.sourcegitcommit: 8e722d72c5d1384889f70adb26c5675544897b1f
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/15/2018
---
# <a name="free-provisioning"></a>Aprovisionamiento gratuito

_Con el lanzamiento de Apple de Xcode 7 se incluye un cambio importante para el aprovisionamiento gratuito de los desarrolladores de iOS y Mac._

El aprovisionamiento gratuito permite a los desarrolladores implementar su aplicación de Xamarin.iOS en sus dispositivos iOS **sin** formar parte de ningún **programa de Apple Developer**. Esto es una enorme ventaja para los desarrolladores, ya que realizar pruebas en un dispositivo supone muchos beneficios en comparación con realizarlas en un simulador, incluyendo pero sin limitarse a la memoria, el almacenamiento y la conectividad de red, entre otros.

El aprovisionamiento sin una cuenta de Apple Developer debe realizarse mediante Xcode, que crea una *Identidad de firma* (que contiene un certificado de desarrollador y una clave privada), y un *Perfil de aprovisionamiento* (que contiene un id. de aplicación explícito y el número UDID del dispositivo iOS conectado).

## <a name="requirements"></a>Requisitos

Para aprovecharse de la implementación de sus aplicaciones de Xamarin.iOS en un dispositivo con aprovisionamiento gratuito debe usar Xcode 7 o versiones anteriores.

**El id. de Apple que se está usando no debe estar conectado a ningún programa de Apple Developer.**

El identificador de agrupación utilizado en la aplicación debe ser único y no se ha podido usar en otra aplicación anteriormente. Cualquier identificador de agrupación que se usa con libre aprovisionamiento no puede volver a utilizarse otra vez. Si ya ha distribuido una aplicación, no puede aprovisionar esa aplicación con el aprovisionamiento gratuito. 

Para más información, consulte las [guías de distribución de aplicaciones](~/ios/deploy-test/app-distribution/index.md).

Si su aplicación usa App Services, entonces necesitará crear un perfil de aprovisionamiento como se detalla en la guía [Aprovisionamiento de dispositivos](~/ios/get-started/installation/device-provisioning/index.md#appservices). Puede ver más limitaciones en la siguiente [sección correspondiente](#limitations).


## <a name="a-namelaunching--launching-your-app"></a><a name="launching" /> Inicio de la aplicación

Para usar el aprovisionamiento gratuito para implementar una aplicación en un dispositivo, utilice Xcode para crear la identidad de firma y los perfiles de aprovisionamiento y, después, utilice Visual Studio para Mac o Visual Studio para elegir el perfil correcto con el que firmar la aplicación. Siga el siguiente tutorial paso a paso para realizar esto:

1. Si no tiene un id. de Apple, cree uno en [appleid.apple.com](https://appleid.apple.com/account).
2. Abra Xcode y vaya a **Xcode > Preferences** (Xcode > Preferencias).
3. En **Cuentas**, use el botón **+** para agregar su id. de Apple existente. Debería tener un aspecto similar al de la siguiente captura de pantalla:

  [![](free-provisioning-images/launchapp1.png "Cuentas de preferencias de Xcode")](free-provisioning-images/launchapp1.png#lightbox)

4. Conecte el dispositivo iOS en el que quiere realizar la implementación y cree un nuevo proyecto de iOS vacío de vista única en Xcode. Establezca el menú desplegable **Team** (Equipo) en el ID de Apple que acaba de agregar. Debe tener un formato similar a `your name (Personal Team - your Apple ID)`:

  [![](free-provisioning-images/launchapp2.png "Crear la identidad de firma")](free-provisioning-images/launchapp2.png#lightbox)

5. En la sección **General > Identidad**, asegúrese de que el identificador de agrupación coincide _exactamente_ con el identificador de agrupación de su aplicación de Xamarin.iOS, y asegúrese de que el destino de la implementación coincide con el dispositivo iOS conectado, o es inferior. Este paso es extremadamente importante, ya que Xcode solo creará un perfil de aprovisionamiento con un id. de aplicación explícito:

  [![](free-provisioning-images/launchapp5.png "Crear un perfil de aprovisionamiento con un identificador de aplicación explícito")](free-provisioning-images/launchapp5.png#lightbox)

6. En la sección de firma, seleccione **Automatically Manage Signing (Administrar firma automáticamente)** y su equipo de la lista desplegable:

  [![](free-provisioning-images/launchapp6.png "Seleccionar Automatically Manage Signing (Administrar firma automáticamente) y su equipo de la lista desplegable")](free-provisioning-images/launchapp6.png#lightbox)

7. En el paso anterior se generará automáticamente un perfil de aprovisionamiento y una identidad de firma. Puede verlo haciendo clic en el icono de información, situado junto al perfil de aprovisionamiento:

  [![](free-provisioning-images/launchapp7.png "Ver el perfil de aprovisionamiento")](free-provisioning-images/launchapp7.png#lightbox)

8. Para realizar pruebas en Xcode, implemente la aplicación vacía en su dispositivo haciendo clic en el botón Ejecutar.

9. Vuelva a su IDE, con el mismo dispositivo conectado, y haga clic con el botón derecho en su nombre de proyecto de Xamarin.iOS para abrir el cuadro de diálogo **Opciones de proyecto**. Vaya a la sección Firma de agrupación iOS y establezca explícitamente su identidad de firma y su perfil de aprovisionamiento:

  [![](free-provisioning-images/launchapp8.png "Establecer la identidad de firma y el perfil de aprovisionamiento")](free-provisioning-images/launchapp8.png#lightbox)

Si no puede ver su identidad de firma o el perfil de aprovisionamiento correcto en su IDE, puede que necesite reiniciarlo.


## <a name="a-namelimitations-limitations"></a><a name="limitations" />Limitaciones

Apple ha impuesto varias limitaciones sobre cuándo y cómo puede usar el aprovisionamiento gratuito para ejecutar su aplicación en un dispositivo iOS, garantizando que solo puede implementar en *su* dispositivo. Estas se enumeran en esta sección.

El acceso a iTunes Connect también está limitado y, por lo tanto, los servicios como la publicación en el App Store y TestFlight no están disponibles para desarrolladores que aprovisionan sus aplicaciones de manera gratuita. Se necesita una cuenta de Apple Developer (Enterprise o Personal) para distribuir mediante medios Ad Hoc e internos.

Los perfiles de aprovisionamiento que se han creado de esta manera expirarán después de una semana; las identidades de firma después de un año. Además, los perfiles de aprovisionamiento solo se crearán mediante identificadores de aplicación explícitos, por lo que necesitará seguir las instrucciones [anteriores](#launching) para cada aplicación que quiera instalar.

El aprovisionamiento para la mayoría de los servicios de aplicación tampoco es posible con el aprovisionamiento gratuito. Esto incluye:

- Apple Pay
- Game Center
- iCloud
- Compra desde la aplicación
- Notificaciones push
- Wallet (anteriormente Passbook)

Apple proporciona una lista completa en su guía [Supported Capabilities (Funciones admitidas)](https://developer.apple.com/library/prerelease/ios/documentation/IDEs/Conceptual/AppDistributionGuide/SupportedCapabilities/SupportedCapabilities.html#//apple_ref/doc/uid/TP40012582-CH38-SW1). Para aprovisionar su aplicación para su uso con servicios de aplicación, consulte las guías [Trabajar con capacidades](~/ios/deploy-test/provisioning/capabilities/index.md).


## <a name="summary"></a>Resumen

En esta guía se han explorado las ventajas y limitaciones de usar el aprovisionamiento gratuito para instalar aplicaciones en un dispositivo iOS. También ha recorrido, paso a paso, el aprovisionamiento gratuito para instalar una aplicación de Xamarin.iOS.

## <a name="related-links"></a>Vínculos relacionados

- [Aprovisionamiento de dispositivos](~/ios/get-started/installation/device-provisioning/index.md)
- [Aprovisionamiento de servicios de aplicación](~/ios/get-started/installation/device-provisioning/index.md#appservices)
