---
title: .NET Standard
ms.topic: article
ms.prod: xamarin
ms.assetid: 8C30F8D3-1920-453E-9E8B-D40696736FF2
ms.technology: xamarin-cross-platform
author: asb3993
ms.author: amburns
ms.date: 04/12/2017
ms.openlocfilehash: ab22881f383e00a67fda8d3e8ffc5d9a4f7f993e
ms.sourcegitcommit: 8e722d72c5d1384889f70adb26c5675544897b1f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/15/2018
---
# <a name="net-standard"></a>.NET Standard

## <a name="using-net-standard-library-projects-to-share-code"></a>Usar proyectos de biblioteca estándar de .NET para compartir código

La biblioteca estándar .NET es una especificación formal de las API de .NET que están pensadas para estar disponibles en todos los entornos de ejecución de .NET. La finalidad de la biblioteca estándar consiste en establecer una mayor uniformidad en el ecosistema de .NET.
[ECMA 335](https://github.com/dotnet/coreclr/blob/master/Documentation/project-docs/dotnet-standards.md) sigue estableciendo uniformidad en el comportamiento del tiempo de ejecución de .NET, pero no hay ninguna especificación parecida para las bibliotecas de clases base (BCL) de .NET para implementaciones de la biblioteca de .NET.

Se puede considerar como una representación simplificada de próxima generación [biblioteca de clases Portable](https://msdn.microsoft.com/library/gg597391.aspx).
Es una sola biblioteca con una API uniforme para todas las plataformas. NET, incluido .NET Core. Simplemente cree una sola biblioteca estándar de .NET y usarlo desde cualquier runtime compatible con la plataforma estándar. NET.

# <a name="visual-studio-for-mactabvsmac"></a>[Visual Studio para Mac](#tab/vsmac)

## <a name="visual-studio-for-mac"></a>Visual Studio para Mac

Esta sección se explica cómo crear y utilizar una biblioteca estándar de .NET con Visual Studio para Mac. Consulte la sección de ejemplo de biblioteca estándar de .NET para una implementación completa.

### <a name="creating-a-net-standard-library"></a>Crear una biblioteca estándar de .NET

Agregar una biblioteca estándar de .NET a la solución es bastante sencillo.

1. En el cuadro de diálogo Agregar nuevo proyecto, seleccione la `.NET Core` categoría y, a continuación, seleccione `Class Library(.NET Core)`.

  **Nota:** esta plantilla se cambiará a `.NET Standard` en una versión futura de Visual Studio para Mac.

  ![Crear una biblioteca de clases de .NET Core](net-standard-images/vsm01.png)

2. El proyecto de biblioteca estándar de .NET aparecerá como se muestra en el Explorador de soluciones. El nodo dependencias indicará que la biblioteca usa la [NETStandard.Library](https://www.nuget.org/packages/NETStandard.Library/).

  ![Nodo de dependencias de la solución indica estándar de .NET](net-standard-images/vsm02.png)

#### <a name="editing-net-standard-library-settings"></a>Editar configuración de la biblioteca estándar de .NET

La configuración de la biblioteca estándar de .NET se pueden ver y cambiar, haga doble clic en el proyecto y seleccione `Options` tal y como se muestra en esta captura de pantalla:

![Edición estándar de .NET framework de destino en Opciones de proyecto](net-standard-images/vsm03.png)

En puede cambiar la versión de `netstandard` cambiando la `Target Framework` valor de la lista desplegable.

**Además:** puede editar la `.csproj` directamente para cambiar este valor.

# <a name="visual-studiotabvswin"></a>[Visual Studio](#tab/vswin)

## <a name="visual-studio-2017-windows"></a>Visual Studio 2017 (Windows)

Esta sección le guía por el proceso de crear y utilizar una biblioteca estándar de .NET con Visual Studio. Consulte la sección de ejemplo de biblioteca estándar de .NET para una implementación completa.

### <a name="creating-a-net-standard-library"></a>Crear una biblioteca estándar de .NET

#### <a name="visual-studio-2017"></a>Visual Studio 2017

Agregar una biblioteca estándar de .NET a la solución es bastante sencillo.

1. En el cuadro de diálogo Agregar nuevo proyecto, seleccione la `.NET Standard` categoría y, a continuación, seleccione `Class Library(.NET Standard)`.

  ![](net-standard-images/vs01.png "Crear nueva biblioteca de clases .NET estándar")

2. El proyecto de biblioteca estándar de .NET aparecerá como se muestra en el Explorador de soluciones. El nodo dependencias indicará que la biblioteca usa la [NETStandard.Library](https://www.nuget.org/packages/NETStandard.Library/).

  ![](net-standard-images/vs02.png "Proyecto .NET estándar de la solución")

#### <a name="editing-net-standard-library-settings"></a>Editar configuración de la biblioteca estándar de .NET

La configuración de la biblioteca estándar de .NET se pueden ver y cambiar, haga doble clic en el proyecto y seleccione `Properties` tal y como se muestra en esta captura de pantalla:

![](net-standard-images/vs03.png "Hacer referencia a una biblioteca estándar de .NET de la misma manera que otros proyectos")

En puede cambiar la versión de `netstandard` cambiando la `Target Framework` valor de la lista desplegable.

**Además:** puede editar la `.csproj` directamente para cambiar este valor.

#### <a name="using-net-standard-library"></a>Uso de la biblioteca estándar de .NET

Una vez que se ha creado una biblioteca estándar. NET, puede agregar una referencia a él desde cualquier aplicación compatible o biblioteca de proyectos de la misma manera normalmente agregar referencias. En Visual Studio, haga doble clic en el nodo referencias y elija `Add Reference...` , a continuación, cambie a la `Solution : Projects` ficha tal como se muestra:

![](net-standard-images/vs04.png "En Visual Studio, haga doble clic en el nodo referencias y elija Agregar referencia …, a continuación, cambie a la ficha de proyectos de la solución, como se muestra")

-----

