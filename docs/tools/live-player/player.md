---
title: "Aplicación de Xamarin Player en vivo"
description: Editar y probar aplicaciones en tiempo real en el dispositivo iOS o Android
ms.topic: article
ms.prod: xamarin
ms.assetid: A7EB73C1-38D7-46C5-9AF6-4C571C168BE7
ms.technology: xamarin-cross-platform
author: topgenorth
ms.author: toopge
ms.date: 05/10/2017
ms.openlocfilehash: 6b0d62a9026c1248a66166e75ed41bb0148547a6
ms.sourcegitcommit: 0fdb243b46cf21be47584900805cadcd077121bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/12/2018
---
# <a name="xamarin-live-player-app"></a>Aplicación de Xamarin Player en vivo

![Característica de vista previa](~/media/shared/preview.png)

## <a name="get-the-app"></a>Obtener la aplicación

### <a name="xamarin-live-player-for-android"></a>Xamarin Player en vivo para Android
Xamarin Player en vivo está disponible para Android desde Google Play:

[ ![Disponible en Google Play](images/google-play-badge.png)](https://play.google.com/store/apps/details?id=com.xamarin.live)

Para dispositivos Android sin Google Play está disponible a través de Xamarin Player Live [HockeyApp](https://aka.ms/xlp-hockeyapp) distribución. Además, anticipo genera para Android se puede instalar directamente desde Google Play mediante la aceptación de los [programa beta abierta](https://play.google.com/apps/testing/com.xamarin.live)

### <a name="xamarin-live-player-for-ios"></a>Xamarin Player Live para iOS
Le animamos a los usuarios unir el [aplicación Xamarin Player Live _iOS Preview_ ](https://aka.ms/liveplayeralpha) para disfrutar de un acceso rápido a las mejoras más recientes a través de TestFlight.



## <a name="using-the-app"></a>Uso de la aplicación

Una vez haya instalado la aplicación en su teléfono, siga el [instrucciones de instalación](~/tools/live-player/install.md) para conectarse a su equipo. Pruebe una de las [aplicaciones de ejemplo](~/tools/live-player/samples.md) para que funcione.

En el inicio, la aplicación de Xamarin Player Live aspecto (en iOS y Android respectivamente):

![Captura de pantalla de aplicación de iOS de Reproductor de Live](player-images/app-iphone-sml.png) ![Captura de pantalla de aplicación Reproductor Android en vivo](player-images/app-android-sml.png)

Cuando se presiona **par de claves para Visual Studio**, use la cámara para escanear el código de barras que muestra en el equipo:

![Captura de pantalla del analizador de código de barras de iOS](player-images/scan-iphone-sml.png) ![Captura de pantalla del analizador de código de barras Android](player-images/scan-android-sml.png)

Si la conexión es correcta, el código debe ejecutarse en el dispositivo prácticamente inmediata (por ejemplo, el ejemplo de la Calculadora):

![Aplicación de calculadora de ejemplo con el dispositivo](player-images/basic-calculator-iphone-sml.png)

## <a name="options"></a>Opciones

Presione el botón información **(i)** en la parte inferior de la aplicación para revelar el **opciones** menú:

![Captura de pantalla del menú de opciones](player-images/options.png)

### <a name="logs"></a>Registros

Ver los registros para diagnosticar problemas.

### <a name="settings"></a>Configuración

* Alternar visualización de errores de compilación y en tiempo de ejecución.
* Información de versión.
* Envíe sus comentarios.

![Captura de pantalla de la configuración](player-images/settings.png)

## <a name="managing-devices"></a>Administración de dispositivos

Para conectar un dispositivo por primera vez, siga las instrucciones que aparecen en [requisitos y el programa de instalación](~/tools/live-player/install.md). Puede asociar varios dispositivos (por ejemplo un iOS y un Android) y administrarlos a través del IDE.

# <a name="visual-studiotabvswin"></a>[Visual Studio](#tab/vswin)

En Visual Studio, elija **Herramientas > Xamarin Player Live > Administrar dispositivos...**

![Administrar la ventana de dispositivos](player-images/manage-tools-menu-vs.png)

Esta ventana permite hacer lo siguiente:

- Par de un nuevo dispositivo examinando el código
- O bien emparejar un dispositivo escribiendo el código que se muestra en su pantalla
- Quitar dispositivos existentes de la lista

También puede tener acceso a esta ventana desde la lista de dispositivos.

# <a name="visual-studio-for-mactabvsmac"></a>[Visual Studio para Mac](#tab/vsmac)

En Visual Studio para Mac, elija **Herramientas > (Xamarin Player Live) administrar dispositivos...**

![Administrar la ventana de dispositivos](player-images/manage-tools-menu.png)

Esta ventana permite hacer lo siguiente:

- Par de un nuevo dispositivo examinando el código
- O bien emparejar un dispositivo escribiendo el código que se muestra en su pantalla
- Quitar dispositivos existentes de la lista

![Administrar la ventana de dispositivos](player-images/manage.png)

También puede tener acceso a esta ventana desde la lista de dispositivos:

![Elegir los dispositivos de Reproductor de Xamarin en directo de la lista de dispositivos](player-images/manage-device-menu.png)

-----

Si experimenta algún problema, vea [limitaciones y solución de problemas](~/tools/live-player/troubleshooting.md).


## <a name="related-links"></a>Vínculos relacionados

- [Limitaciones](~/tools/live-player/limitations.md)
- [Solución de problemas](~/tools/live-player/troubleshooting.md)
- [Ejemplos de Xamarin Player en vivo](~/tools/livehttps://developer.xamarin.com/samples.md)
