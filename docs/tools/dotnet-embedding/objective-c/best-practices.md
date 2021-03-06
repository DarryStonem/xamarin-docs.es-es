---
title: "Prácticas recomendadas de 4000 Embeddinator para ObjC"
ms.topic: article
ms.prod: xamarin
ms.assetid: 63C7F5D2-8933-4D4A-8348-E9CBDA45C472
ms.technology: xamarin-cross-platform
author: topgenorth
ms.author: toopge
ms.date: 11/14/2017
ms.openlocfilehash: bd2863fec2bd6cbec2efc0441db8d7aa8f3343d0
ms.sourcegitcommit: 0fdb243b46cf21be47584900805cadcd077121bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/12/2018
---
# <a name="embeddinator-4000-best-practices-for-objc"></a>Prácticas recomendadas de 4000 Embeddinator para ObjC

Se trata de un borrador y podrían no ser sincronizados con las características actualmente compatibles con la herramienta. Esperamos que este documento se evolucionar por separado y finalmente coincide con el final de la herramienta, es decir, le sugerimos mejores métodos a largo plazo - soluciones alternativas no inmediatas.

Gran parte de este documento también se aplica a otros idiomas admitidos. Sin embargo todos los ejemplos se encuentran en C# y objetivo de C.


# <a name="exposing-a-subset-of-the-managed-code"></a>Exponer un subconjunto del código administrado

La biblioteca/marco generado nativo contiene código Objective-C para llamar a cada una de las API administradas que se exponen. La API más que expuesta (hacer público), a continuación, mayor nativo _adherencia_ se convertirá en la biblioteca.

Sería una buena idea crear un ensamblado diferente y más pequeño, para exponer solo las API necesarias para el desarrollador nativo. Ese fachada también le permitirá más control sobre la visibilidad, nombres, comprobación de errores... del código generado.


# <a name="exposing-a-chunkier-api"></a>Exponer una API chunkier

Hay un precio para realizar la transición de nativo a administrado (y viceversa). Por lo tanto, es mejor exponer _en bloque en lugar de locuaz_ API para los desarrolladores nativo, p. ej.

**Locuaz**
```
public class Person {
    public string FirstName { get; set; }
    public string LastName { get; set; }
}
```

```csharp
// this requires 3 calls / transitions to initialize the instance
Person *p = [[Person alloc] init];
p.firstName = @"Sebastien";
p.lastName = @"Pouliot";
```

**Chunky**
```
public class Person {
    public Person (string firstName, string lastName) {}
}
```

```csharp
// a single call / transition will perform better
Person *p = [[Person alloc] initWithFirstName:@"Sebastien" lastName:@"Pouliot"];
```

Puesto que el número de transiciones es menor será mejor el rendimiento. También requiere menos código que se genera, por lo que esto creará una biblioteca nativa más pequeña.


# <a name="naming"></a>Nomenclatura

Nomenclatura cosas es uno de estos dos problemas más difíciles en informática, las demás que se va a caché de errores de invalidación y desactivar-por-1. Espero que incrustar .NET puede evitan todos menos de nomenclatura.

## <a name="types"></a>Tipos

Objective-C no admite espacios de nombres. En general, sus tipos tienen como prefijo un 2 (para Apple) o 3 (para partes 3rd) como prefijo, de caracteres `UIView` para la vista del UIKit, que indica el marco de trabajo.

Para los tipos de .NET el omitir el espacio de nombres no es posible que se pueden introducir nombres duplicados o confusos. Esto hace que los tipos .NET existentes muy largos, p. ej.

```csharp
namespace Xamarin.Xml.Configuration {
    public class Reader {}
}
```

se utilizaría como:

```csharp
id reader = [[Xamarin_Xml_Configuration_Reader alloc] init];
```

Sin embargo volver a puede exponer el tipo como:

```csharp
public class XAMXmlConfigReader : Xamarin.Xml.Configuration.Reader {}
```

lo más sencillo de Objective-C para usarlo, p. ej.:

```csharp
id reader = [[XAMXmlConfigReader alloc] init];
```

## <a name="methods"></a>Métodos

Los nombres de .NET incluso buenos podrían no ser ideales para una API de C de objetivo.

Convenciones de nomenclatura en Objective C son diferentes de .NET (mayúsculas y minúsculas camel en lugar de mayúsculas y minúsculas pascal, más detallado).
Lea la [directrices de programación para cacao](https://developer.apple.com/library/content/documentation/Cocoa/Conceptual/CodingGuidelines/Articles/NamingMethods.html#//apple_ref/doc/uid/20001282-BCIGIJJF).

Desde el punto de vista de un desarrollador objetivo-C, un método con un `Get` prefijo implica no posee la instancia, es decir, el [obtener regla](https://developer.apple.com/library/content/documentation/CoreFoundation/Conceptual/CFMemoryMgmt/Concepts/Ownership.html#//apple_ref/doc/uid/20001148-SW1).

Esta regla de nomenclatura no tiene correspondencia alguna en el mundo de GC de .NET; un método de .NET con un `Create` prefijo se comportará de forma idéntica en. NET. Sin embargo, para los desarrolladores Objective-C, normalmente significa que posee la instancia devuelta, es decir, el [crear regla](https://developer.apple.com/library/content/documentation/CoreFoundation/Conceptual/CFMemoryMgmt/Concepts/Ownership.html#//apple_ref/doc/uid/20001148-103029).

# <a name="exceptions"></a>Excepciones

Es muy commont en .NET para utilizar excepciones ampliamente para informar de errores. Sin embargo, son lentas y no bastante idénticos en ObjC. Siempre que sea posible se debe ocultar del programador de C de objetivo.

Por ejemplo, .NET `Try` patrón será mucho más fácil de consumir de código Objective-C:

```csharp
public int Parse (string number)
{
    return Int32.Parse (number);
}
```

frente a

```csharp
public bool TryParse (string number, out int value)
{
    return Int32.TryParse (number, out value);
}
```

## <a name="exceptions-inside-init"></a>Excepciones dentro de `init*`

En .NET un constructor debe tener éxito y devolver un (_espero_) instancia válida o produce una excepción.

En cambio, permite Objective-C `init*` para devolver `nil` cuando no se puede crear una instancia. Se trata de un patrón común, pero no general, que se usa en muchos de los marcos de Apple. En otros casos un `assert` puede ocurrir (y finalice el proceso actual).

El generador de seguir el mismo `return nil` de patrón de generadas `init*` métodos. Si se produce una excepción administrada, se imprimirá (mediante `NSLog`) y `nil` se devolverá al autor de la llamada.

## <a name="operators"></a>Operadores

ObjC no permitir que los operadores sobrecargados como C#, por lo que estos se convierten en los selectores de clase.

["Descriptivo"](https://msdn.microsoft.com/en-us/library/ms229032(v=vs.110).aspx) método con nombre se generan con preferencia a las sobrecargas de operador cuando se encuentra y pueden generar un más fáciles de consumir API.

Las clases que se anulan los operadores == o! = debe invalidar el método Equals (objeto) estándar también.
