---
title: "Instalación en el equipo Windows"
description: "En esta guía se describen los pasos necesarios para instalar Xamarin.Android para Visual Studio en Windows y se explica cómo configurar Xamarin.Android para compilar su primera aplicación de Xamarin.Android."
ms.topic: article
ms.prod: xamarin
ms.assetid: 2BE4D5AD-D468-B177-8F96-837D084E7DE1
ms.technology: xamarin-android
author: mgmclemore
ms.author: mamcle
ms.date: 03/01/2018
ms.openlocfilehash: 7cf21e75c9ae2f3c27b07cb20f1044779b42b06b
ms.sourcegitcommit: 0fdb243b46cf21be47584900805cadcd077121bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/12/2018
---
# <a name="windows-installation"></a>Instalación en el equipo Windows

_En esta guía se describen los pasos necesarios para instalar Xamarin.Android para Visual Studio en Windows y se explica cómo configurar Xamarin.Android para compilar su primera aplicación de Xamarin.Android._


## <a name="overview"></a>Información general

Gracias a que ahora Xamarin se incluye con todas las ediciones de Visual Studio sin ningún costo adicional y no requiere ninguna licencia independiente, puede usar el instalador de Visual Studio para descargar e instalar las herramientas de Xamarin.Android
(los pasos relacionados con la instalación manual y la configuración de las licencias que eran necesarios para las versiones anteriores de Xamarin.Android ya no son necesarios). En esta guía aprenderá lo siguiente:

-   Cómo configurar las ubicaciones personalizadas para Java Development Kit, el SDK de Android y el NDK de Android.

-   Cómo iniciar Android SDK Manager para descargar e instalar componentes adicionales del SDK de Android.

-   Cómo preparar un emulador o dispositivo de Android para la depuración y las pruebas.

-   Cómo crear el primer proyecto de aplicación de Xamarin.Android.

Cuando acabe esta guía, tendrá una instalación operativa de Xamarin.Android integrada en Visual Studio y podrá empezar a compilar su primera aplicación de Xamarin.Android.

## <a name="installation"></a>Instalación

Para obtener información detallada sobre la instalación de Xamarin para su uso con Visual Studio en Windows, consulte la guía de [instalación de Windows](~/cross-platform/get-started/installation/windows.md).


## <a name="configuration"></a>Configuración

Xamarin.Android usa Java Development Kit (JDK) y el SDK de Android para compilar las aplicaciones. Durante la instalación, el instalador de Visual Studio coloca estas herramientas en sus ubicaciones predeterminadas y configura el entorno de desarrollo con la configuración de ruta de acceso adecuada. Puede ver y cambiar estas ubicaciones haciendo clic en **Herramientas > Opciones > Xamarin > Configuración de Android**:

![Captura de pantalla del cuadro de diálogo Configuración de Android de Xamarin](windows-images/07-settings.png)

Para la mayoría de los usuarios, estas ubicaciones predeterminadas funcionarán correctamente y no habrá que efectuar más cambios, pero tal vez quiera configurar Visual Studio con unas ubicaciones personalizadas para estas herramientas (por ejemplo, en el caso de que haya instalado el JDK de Java, el SDK de Android o el NDK en otra ubicación). Haga clic en **Cambiar** junto a la ruta de acceso que quiera cambiar; luego, desplácese hasta la nueva ubicación.

Xamarin.Android usa [JDK 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html), necesario para el desarrollo en el nivel de API 24 o superior. JDK 8 también admite niveles de API anteriores al 24. Si está desarrollando contenido específicamente para el nivel de API 23 o uno anterior, puede continuar usando [JDK 7](http://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html).

> [!IMPORTANT]
> Xamarin.Android no admite JDK 9.


### <a name="android-sdk-manager"></a>Administrador de SDK de Android

Android usa varias opciones de nivel de API de Android para determinar la compatibilidad de su aplicación entre las distintas versiones de Android (para obtener más información sobre los niveles de la API de Android, consulte [Understanding Android API Levels](~/android/app-fundamentals/android-api-levels.md) [Información de los niveles de API de Android]).
En función de los niveles de API de Android que quiera establecer como objetivo, es posible que tenga que descargar e instalar componentes adicionales del SDK de Android. Además, puede que tenga que instalar herramientas opcionales, así como las imágenes del emulador que se proporcionan en el SDK de Android. Para ello, use **Android SDK Manager**. Puede iniciar **Android SDK Manager** haciendo clic en **Herramientas > Android > Android SDK Manager**:

[![Cómo iniciar Android SDK Manager](windows-images/08-sdk-manager-sml.png)](windows-images/08-sdk-manager.png#lightbox)

De forma predeterminada, Visual Studio instala Android SDK Manager de Google:

![Captura de pantalla de ejemplo de Android SDK Manager de Google](windows-images/09-google-sdk-manager.png)

Puede usar Android SDK Manager de Google para instalar las versiones del paquete de Android SDK Tools hasta la versión 25.2.3, pero si necesita usar una versión posterior del paquete de Android SDK Tools, debe instalar el complemento de Android SDK Manager de Xamarin para Visual Studio (disponible en Visual Studio Marketplace). Esto es necesario porque el SDK Manager independiente de Google ha quedado en desuso en la versión 25.2.3 del paquete de Android SDK Tools. 

Para más información sobre cómo usar Android SDK Manager de Xamarin, vea [Configuración de Android SDK](~/android/get-started/installation/android-sdk.md).


### <a name="android-emulator"></a>Emulador Android

Si no dispone de ningún dispositivo Android físico para efectuar las pruebas, puede usar un emulador de Android para probar la aplicación. Para más información sobre Android Emulator de Google, vea [Android SDK Emulator](~/android/deploy-test/debugging/android-sdk-emulator/index.md) (Emulador de Android SDK).

El emulador de Google Android usa Intel HAXM (Hardware Accelerated Execution Manager), que puede entrar en conflicto con las tecnologías de virtualización que usan otros emuladores. Las tres tecnologías de virtualización principales son:

-   **Hyper-V** (usado por el emulador de Visual Studio para Android y el emulador de Windows Phone) 

-   **Virtual Box** (usado por Genymotion)

-   **Intel HAXM** (usado por el emulador de Android SDK de Google) 

Dado que la CPU de un equipo de desarrollo solo puede admitir una tecnología de virtualización a la vez, es mejor tener solo una en uso en un equipo de desarrollo.

<a name="device" />

### <a name="android-device"></a>Dispositivo Android

Si dispone de un dispositivo Android físico para efectuar las pruebas, ahora es un buen momento para configurarlo para su uso de desarrollo. Consulte [Configurar el dispositivo para el desarrollo](~/android/get-started/installation/set-up-device-for-development.md) para configurar el dispositivo Android para el desarrollo; luego, conéctelo al equipo para ejecutar y depurar aplicaciones de Xamarin.Android.


## <a name="create-an-application"></a>Crear una aplicación

Ahora que ha instalado Xamarin.Android, puede iniciar Visual Studio para crear un proyecto. Haga clic en **Archivo > Nuevo > Proyecto** para comenzar a crear la aplicación:

![Cómo crear un proyecto](windows-images/10-new-project.png)

En el cuadro de diálogo **Nuevo proyecto**, seleccione **Android** en **Plantillas** y haga clic en **Aplicación en blanco (Android)** en el panel de la derecha. Escriba un nombre para la aplicación (en la siguiente captura de pantalla, la aplicación se llama **MyApp**); luego, haga clic en **Aceptar**:

[![Captura de pantalla del cuadro de diálogo Nuevo proyecto, en el que se crea una aplicación en blanco para Android](windows-images/11-first-app-sml.png)](windows-images/11-first-app.png#lightbox)

Ya está. Ahora ya puede usar Xamarin.Android para crear aplicaciones de Android.


## <a name="summary"></a>Resumen

En este artículo ha aprendido a configurar e instalar la plataforma de Xamarin.Android en Windows, a configurar (opcional) Visual Studio con ubicaciones de instalación personalizadas de Java JDK y del SDK de Android, a iniciar SDK Manager para instalar componentes adicionales del SDK de Android, a configurar un emulador o dispositivo de Android y a empezar a compilar su primera aplicación.

El siguiente paso consiste en echar un vistazo a los tutoriales de [Hello, Android](~/android/get-started/hello-android/index.md) para aprender a crear una aplicación operativa de Xamarin.Android.


## <a name="related-links"></a>Vínculos relacionados

- [Descarga de Visual Studio](https://www.visualstudio.com/vs/)
- [Instalación de Visual Studio Tools para Xamarin](~/cross-platform/get-started/installation/windows.md)
- [Requisitos del sistema](~/cross-platform/get-started/requirements.md)
- [Configuración de Android SDK](~/android/get-started/installation/android-sdk.md)
- [Emulador de Android SDK](~/android/get-started/installation/android-emulator/index.md)
- [Configurar el dispositivo para el desarrollo](~/android/get-started/installation/set-up-device-for-development.md)
