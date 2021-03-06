---
title: "Solución de problemas de enlace"
description: "Esta guía explica qué hacer si tiene dificultades para enlazar una biblioteca de C de objetivo."
ms.topic: article
ms.prod: xamarin
ms.assetid: 7C65A55C-71FA-46C5-A1B4-955B82559844
ms.technology: xamarin-cross-platform
author: asb3993
ms.author: amburns
ms.date: 10/19/2016
ms.openlocfilehash: 2db7fe30f05224f6b74b4d2189606da59946bda0
ms.sourcegitcommit: 6cd40d190abe38edd50fc74331be15324a845a28
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/27/2018
---
# <a name="binding-troubleshooting"></a>Solución de problemas de enlace

Algunas sugerencias para solucionar problemas de enlaces para macOS (anteriormente conocido como OS X) API en Xamarin.Mac.

## <a name="missing-bindings"></a>Enlaces que faltan

Mientras Xamarin.Mac cubre gran parte de las API de Apple, en ocasiones puede que necesite llamar a algunas API de Apple que no tiene un enlace todavía. En otros casos, debe llamar a terceros C/Objective-C que TI fuera del ámbito de los enlaces de Xamarin.Mac.

Si está trabajando con una API de Apple, el primer paso es que Xamarin sepan que está alcanzando una sección de la API que no tenemos cobertura para todavía. [Registre un error](#reporting-bugs) teniendo en cuenta la API que faltan. Informes de los clientes se usan para dar prioridad a las API que trabajamos en siguiente. Además, si tiene una licencia comercial o empresarial y esta falta de un enlace está bloqueando el progreso, seguir las instrucciones de [soporte](http://xamarin.com/support) para presentar una incidencia. No podemos prometemos un enlace, pero en algunos casos, obtenemos es un trabajo.

Una vez notificar Xamarin (si procede) de su enlace falta, el siguiente paso es considere la posibilidad de enlace usted mismo. Tenemos una guía completa [aquí](~/cross-platform/macios/binding/overview.md) y algunos documentos no oficiales [aquí](http://brendanzagaeski.appspot.com/xamarin/0002.html) para englobar Objective-C enlaces a mano. Si se llama a una API de C, puede utilizar el mecanismo de P/Invoke de C#, documentación está [aquí](http://www.mono-project.com/docs/advanced/pinvoke/).

Si decide trabajar en el enlace usted mismo, tenga en cuenta que los errores en el enlace pueden generar todo tipo de bloqueos interesantes en el tiempo de ejecución nativo. En concreto, tenga mucho cuidado de que su firma en C# coincide con la signatura nativo en número de argumentos y el tamaño de cada argumento. Si no lo hace pueden dañar la memoria o la pila y se puede bloquearse en el futuro inmediato o en algún momento arbitrario o dañar los datos.

## <a name="argument-exceptions-when-passing-null-to-a-binding"></a>Excepciones del argumento al pasar null a un enlace

Aunque Xamarin funciona para proporcionar alta calidad y bien probados enlaces para las API de Apple, en ocasiones, errores y errores slip en. Problema con mucho más comunes que pueden surgir de es una API producir `ArgumentNullException` cuando pase un valor nulo cuando la API subyacente acepta `nil`. Los archivos de encabezado nativo definir la API a menudo no proporcionan suficiente información en el que las API acepten nulo y que se bloqueará si se le pasa.

Si se ejecuta en un caso donde pasando `null` produce una `ArgumentNullException` pero piense deben trabajar, siga estos pasos:

1. Compruebe la documentación de Apple o ejemplos para ver si puede encontrar la prueba que acepta `nil`. Si está familiarizado con el objetivo de C, puede escribir un programa de prueba pequeñas para verificarlo.
2. [Registre un error](#reporting-bugs).
3. ¿Puede solucionar el error? Si no puede llamar a la API con `null`, una comprobación de null simple alrededor de las llamadas puede ser una solución sencilla.
4. Sin embargo, algunas API requiere pasar null para desactivar o deshabilitar algunas características. En estos casos, se puede solucionar el problema al abrir el Explorador de ensamblado (vea [buscar el miembro de C# para un selector dado](~/mac/app-fundamentals/mac-apis.md#finding_selector)), copiar el enlace y la eliminación de la comprobación de valores null. Asegúrese de registrar el error (paso 2) si hace esto, como su enlace copiado no recibirá actualizaciones y revisiones que se realizan en Xamarin.Mac y esto debe considerarse una solución a corto plazo.

<a name="reporting-bugs"/>

## <a name="reporting-bugs"></a>Informes errores

Sus comentarios son importantes para nosotros. Si encuentra algún problema con Xamarin.Mac:

- Compruebe el [Xamarin.Mac foros](https://forums.xamarin.com/categories/mac)
- Buscar el [repositorio de problema](https://github.com/xamarin/xamarin-macios/issues) 
- Antes de pasar a problemas de GitHub, se realiza un seguimiento de problemas de Xamarin en [Bugzilla](https://bugzilla.xamarin.com/describecomponents.cgi). Por favor, busca allí para la coincidencia de problemas.
- Si no se encuentra un problema de búsqueda de coincidencias, registre un nuevo asunto en la [repositorio de problema de GitHub](https://github.com/xamarin/xamarin-macios/issues/new).

Problemas de GitHub son todos los públicos. No es posible ocultar comentarios o datos adjuntos. 

Incluya como gran parte de las acciones siguientes como sea posible:

- Un ejemplo sencillo reproducir el problema. Se trata de **inestimable** siempre que sea posible. 
- El seguimiento de pila completo del bloqueo.
- El código C# que rodea el bloqueo. 
