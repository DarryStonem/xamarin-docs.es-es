---
title: Trabajar con derechos
description: Los derechos son funciones especiales de las aplicaciones y permisos de seguridad que se conceden a las aplicaciones que están configuradas correctamente para usarlos.
ms.topic: article
ms.prod: xamarin
ms.assetid: 8A3961A2-02AB-4228-A41D-06CB4108D9D0
ms.technology: xamarin-ios
author: bradumbaugh
ms.author: brumbaug
ms.date: 03/15/2017
ms.openlocfilehash: 8b5c88f4af3087f980b586113c274016935585c0
ms.sourcegitcommit: 73bd0c7e5f237f0a1be70a6c1384309bb26609d5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/22/2018
---
# <a name="working-with-entitlements"></a>Trabajar con derechos

_Los derechos son funcionalidades especiales de las aplicaciones y permisos de seguridad que se conceden a las aplicaciones que están configuradas correctamente para usarlos._

En iOS, las aplicaciones se ejecutan en un _espacio aislado_, que proporciona un conjunto de reglas que limitan el acceso entre la aplicación y determinados recursos del sistema o datos de usuario. Los _derechos_ se usan para solicitar que el sistema expanda el espacio aislado para proporcionar capacidades adicionales a la aplicación.

Para extender las capacidades de la aplicación, se debe proporcionar un derecho en el archivo Entitlements.plist de la aplicación. Solo se pueden extender ciertas capacidades, que se muestran en la guía [Trabajar con capacidades](~/ios/deploy-test/provisioning/capabilities/index.md) y se describen [a continuación](#keyreference). Los derechos se pasan al sistema como un par de clave/valor (normalmente solo se necesita uno por capacidad). Las claves y los valores específicos se describen en la sección [Referencia sobre las claves de derechos](#keyreference), que aparece más adelante en esta guía.
Visual Studio para Mac y Visual Studio proporcionan una interfaz clara para agregar derechos a una aplicación de Xamarin.iOS mediante el editor de Entitlements.plist.
En esta guía se presenta el editor de Entitlements.plist y se muestra cómo usarlo. También se proporciona una referencia de todos los derechos que se pueden agregar a un proyecto de iOS para cada capacidad.

## <a name="entitlements-and-provisioning"></a>Derechos y aprovisionamiento


El archivo Entitlements.plist se usa para especificar derechos y para firmar el paquete de aplicaciones.

Pero se deben seguir algunos pasos de aprovisionamiento adicionales para garantizar que la aplicación tiene un código firmado correctamente. El perfil de aprovisionamiento usado debe contener un identificador de aplicación que tenga habilitada la capacidad necesaria. Para obtener información sobre cómo hacerlo, consulte la guía [Trabajar con capacidades](~/ios/deploy-test/provisioning/capabilities/index.md).

> [!IMPORTANT]
> El archivo Entitlements.plist ayuda a rellenar las propiedades correctas para una aplicación usando funcionalidades, pero no puede generar ningún perfil de aprovisionamiento porque no está vinculado a ninguna cuenta de desarrollador de Apple. Tendrá que generar igualmente un perfil de aprovisionamiento mediante el portal para desarrolladores para implementar y distribuir la aplicación.

## <a name="set-entitlements-in-a-xamarinios-project"></a>Establecer derechos en un proyecto de Xamarin.iOS

Además de seleccionar y configurar los servicios de aplicaciones necesarios al definir el identificador de aplicación, los derechos también se deben configurar en el proyecto de Xamarin.iOS. Para ello, edite los archivos **Info.plist** y **Entitlements.plist**.

# <a name="visual-studio-for-mactabvsmac"></a>[Visual Studio para Mac](#tab/vsmac)

Para configurar los derechos en Visual Studio para Mac, haga lo siguiente:

1. En el **Explorador de soluciones**, haga doble clic en el archivo **Info.plist** para abrirlo para su edición.
2. En la sección **iOS Application Target** (Destino de la aplicación de iOS), escriba un nombre para la aplicación y el **identificador de paquete** que se creó al definir el identificador de aplicación:

  ![](entitlements-images/servicexs01.png "Especifique un identificador de lote")

3. Guarde los cambios en el archivo **Info.plist**.
4. En el **Explorador de soluciones**, haga doble clic en el archivo **Entitlements.plist** para abrirlo para su edición:

    ![](entitlements-images/servicexs02.png "Edición de los derechos")

5. Seleccione y configure los derechos necesarios para la aplicación de Xamarin.iOS, de manera que coincidan con la configuración que se definió al crear el identificador de aplicación.
6. Guarde los cambios en el archivo **Entitlements.plist**.

# <a name="visual-studiotabvswin"></a>[Visual Studio](#tab/vswin)

Para configurar los derechos en Visual Studio, haga lo siguiente:

1. En el **Explorador de soluciones**, haga clic con el botón derecho en el archivo **Info.plist**, seleccione **Abrir con...** y seleccione el archivo **Editor de lista de propiedades** para abrirlo y editarlo.
2. En la sección **iOS Application Target** (Destino de la aplicación de iOS), escriba un nombre para la aplicación y el **identificador de paquete** que se creó al definir el identificador de aplicación:

  ![](entitlements-images/servicevs01.png "Establecimiento del identificador de lote")

3. Guarde los cambios en el archivo **Info.plist**.
4. En el **Explorador de soluciones**, haga clic con el botón derecho en el archivo **Entitlements.plist**, seleccione **Abrir con...** y seleccione el archivo **Editor de lista de propiedades** para abrirlo y editarlo:

    ![](entitlements-images/servicevs02.png "Edición de los derechos")

    Como alternativa, haga doble clic en el archivo **Entitlements.plist** para abrir el editor de código fuente XML, con el que podrá establecer el valor de la propiedad y la clave del derecho como se detalla en la sección [Referencia sobre las claves de derechos](#keyreference).

5. Seleccione y configure los derechos necesarios para la aplicación de Xamarin.iOS, de manera que coincidan con la configuración que se definió al crear el identificador de aplicación.
6. Guarde los cambios en el archivo **Entitlements.plist**.


-----

<a name="add-new" />

## <a name="adding-a-new-entitlementsplist-file"></a>Agregar un nuevo archivo Entitlements.plist

Los derechos se agregan a una aplicación mediante el archivo Entitlements.plist. Este archivo se incluye en los proyectos de Xamarin.iOS de forma predeterminada, pero es posible que no se incluya en proyectos anteriores.

Para agregar un archivo Entitlements.plist a Xamarin.iOS, haga lo siguiente:

1.  Haga clic con el botón derecho en el archivo del proyecto y vaya a **Agregar > Nuevo archivo…**:

    ![Menú contextual para agregar archivos](entitlements-images/image1.png)
2.  En el cuadro de diálogo Nuevo archivo, seleccione **iOS > Lista de propiedades** y asígnele el nombre Derechos:

    ![Cuadro de diálogo Nuevo archivo](entitlements-images/image2.png)

<a name="keyreference" />

## <a name="entitlement-key-reference"></a>Referencia sobre las claves de derechos

Las claves de derechos se pueden agregar a través del panel de código fuente del editor de Entitlements.plist. Las claves necesarias se suelen agregar al usar el editor de Entitlements.plist, aunque se muestran a continuación como referencia.

### <a name="wallet"></a>Cartera

*   **Descripción**: Formalmente llamado Passbook, Wallet es una aplicación que almacena y administra pases. Estos pases pueden ser tarjetas de crédito, tarjetas de fidelización, tarjetas de embarque o entradas.

    - **Identificador de tipo de pase**
        * **Claves**: com.apple.developer.pass-type-identifiers
        * **Cadena**: `$(TeamIdentifierPrefix)*`

* **Notas**:
    - De esta manera, la aplicación admitirá todos los tipos de pases. Para restringir la aplicación y admitir únicamente un subconjunto de tipos de pase de equipo, establezca el valor de la cadena en: `$(TeamIdentifierPrefix)pass.$(CFBundleIdentifier)`

    Donde pass.$(CFBundleIdentifier) es el identificador de pase creado [anteriormente](~/ios/platform/passkit.md).

<a name="icloud" />

### <a name="icloud"></a>iCloud

*   **Descripción**: iCloud proporciona a los usuarios de iOS una forma sencilla y cómoda para almacenar su contenido y compartirlo entre dispositivos. Los desarrolladores tienen cuatro maneras para usar iCloud para proporcionar un medio de almacenamiento para sus usuarios: el almacenamiento de pares clave-valor, el almacenamiento UIDocument, CoreData y el uso directo de CloudKit para proporcionar almacenamiento para archivos y directorios específicos. Para más información, consulte la guía Introduction to iCloud (Introducción a iCloud).

    - **Documentos de iCloud y CloudKit**
        - **Claves**: com.apple.developer.ubiquity-container-identifiers
        - **Cadena**: `$(TeamIdentifierPrefix)$(CFBundleIdentifier)`
    - **Almacenamiento de KeyValue de iCloud**
        - **Clave**: com.apple.developer.ubiquity-kvstore-identifier
        - **Cadena**: `$(TeamIdentifierPrefix)$(CFBundleIdentifier)`

* **Notas**:
    - Para buscar la cadena `$(TeamIdentifierPrefix)`, regístrese en developer.apple.com y vaya **Member Center > Your Account > Developer Account Summary** (Centro para miembros > Su cuenta > Resumen de la cuenta de desarrollador) para obtener el identificador de equipo (o el identificador personal en el caso de los desarrolladores). Será una cadena de 10 caracteres (por ejemplo, A93A5CM278).
    - La cadena `$(CFBundleIdentifier)` comienza por `iCloud` y se establece al crear el contenedor de iCloud, de acuerdo con los pasos descritos en la guía [Trabajar con capacidades](~/ios/deploy-test/provisioning/capabilities/icloud-capabilities.md).
    - Se pueden usar los marcadores de posición $`(TeamIdentifierPrefix)` y `$(CFBundleIdentifier)`, que se sustituirán por los valores correctos en tiempo de compilación.

### <a name="app-groups"></a>Grupos de aplicaciones

- **Descripción**: Un grupo de aplicaciones permite que aplicaciones diferentes (o una aplicación y sus extensiones) tengan acceso a una ubicación de almacenamiento de archivos compartidos.

    - **Clave**: com.apple.security.application-groups
    - **Cadena**: group.$(CFBundleIdentifier)

<a name="apple-pay" />

### <a name="apple-pay"></a>Apple Pay

- **Descripción**: Con Apple Pay, los usuarios pueden pagar bienes físicos con su dispositivo iOS.
    - **Clave**: com.apple.developer.in-app-payments
    - **Cadena**: merchant.your.mechantid

### <a name="push-notifications"></a>Notificaciones push

- **Clave**: aps-environment
- **Cadena**: `production` O `development`

### <a name="siri"></a>Siri

- **Descripción**: Con SiriKit, una aplicación iOS puede proporcionar servicios que pueden obtener acceso a Siri y a la aplicación Mapas de un dispositivo iOS mediante App Extensions y las nuevas plataformas Intents e Intents UI. Para más información, consulte la guía Introduction to SiriKit (Introducción a SiriKit).
    - **Clave**: com.apple.developer.siri

### <a name="personal-vpn"></a>VPN personal

- **Clave**: com.apple.developer.networking.vpn.api
- **Cadena**: allow-vpn

### <a name="keychain-sharing"></a>Uso compartido de cadenas de claves

- **Descripción**: El uso compartido de cadenas de claves permite a los desarrolladores de aplicaciones compartir las contraseñas almacenadas en la cadena de claves del dispositivo con otras aplicaciones desarrolladas por el mismo equipo. Se puede restringir el acceso pasando en la cadena un identificador de grupo de acceso de cadena de claves.
    - **Clave**: keychain-access-groups
    - **Cadena**: $(AppIdentifierPrefix) $(CFBundleIdentifier)

### <a name="inter-app-audio"></a>Inter-App Audio

- **Descripción**: Con Inter-App Audio, los desarrolladores pueden transmitir audio entre aplicaciones.
    - **Clave**: inter-app-audio
    - **Booleano**: SÍ

### <a name="associated-domains"></a>Dominios asociados

- **Descripción**: Los dominios asociados que se deben controlar como vínculos universales se deben pasar con este derecho. Los vínculos universales se pueden implementar para permitir una vinculación en profundidad entre la aplicación y un sitio web. Debe proporcionar una entrada a cada dominio que la aplicación admita; además, cada entrada debe empezar por `applinks:`.
    - **Clave**: com.apple.developer.associated-domains
    - **Cadena**: webcredentials:example.com

### <a name="data-protection"></a>Protección de datos

- **Descripción**: La protección de datos usa el hardware de cifrado integrado para almacenar los datos confidenciales usados en la aplicación con un formato cifrado. De forma predeterminada, el nivel de protección se establece en una protección completa (solo se puede obtener acceso a los archivos cuando se desbloquea el dispositivo).
    - **Clave**: com.apple.developer.default-data-protection
    - **Cadena**: NSFileProtectionComplete

### <a name="homekit"></a>HomeKit

- **Descripción**: HomeKit proporciona una plataforma para configurar y administrar dispositivos de automatización del hogar admitidos (todo desde un dispositivo iOS). Para más información sobre cómo usar HomeKit, consulte la guía Introduction to HomeKit (Introducción a HomeKit).
    - **Clave**: com.apple.developer.homekit
    - **Booleano**: SÍ

### <a name="healthkit"></a>HealthKit

- **Descripción**: HealthKit es un marco que se introdujo en iOS 8 que proporciona un almacén de datos centralizado, coordinado y seguro para obtener información relacionada con la salud. Para más información sobre cómo usar HealthKit, consulte la guía Introduction to HealthKit (Introducción a HealthKit).
    - **Clave**: com.apple.developer.healthkit
    - **Booleano**: SÍ

### <a name="wireless-accessory-configuration"></a>Configuración inalámbrica de accesorios

- **Descripción**: La configuración inalámbrica de accesorios permite configurar accesorios Wi-Fi MFi en la aplicación.
    - **Clave**: com.apple.external-accessory.wireless-configuration
    - **Booleano**: SÍ

## <a name="summary"></a>Resumen

En esta guía se presentan los derechos y cómo usarlos en Visual Studio para Mac y en Visual Studio. También se proporciona una referencia de los pares clave/valor para cada capacidad.