---
title: Plantillas de datos
description: "Un objeto DataTemplate que se usa para especificar la apariencia de los datos en controles que se admiten y normalmente se enlaza a los datos que se mostrará."
ms.topic: article
ms.prod: xamarin
ms.assetid: 838F4BDB-B719-457F-8633-27E9B267A2A0
ms.technology: xamarin-forms
author: davidbritch
ms.author: dabritch
ms.date: 09/11/2017
ms.openlocfilehash: 99a00c98471ae85af2a8cba2e1e52444370a9332
ms.sourcegitcommit: 6cd40d190abe38edd50fc74331be15324a845a28
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/27/2018
---
# <a name="data-templates"></a>Plantillas de datos

_Un objeto DataTemplate que se usa para especificar la apariencia de los datos en controles que se admiten y normalmente se enlaza a los datos que se mostrará._

## <a name="introductionintroductionmd"></a>[Introducción](introduction.md)

Plantillas de Xamarin.Forms de datos proporcionan la capacidad para definir la presentación de datos en controles que se admiten. Este artículo proporciona una introducción a las plantillas de datos, Examinar por qué son necesarios.

## <a name="creating-a-datatemplatecreatingmd"></a>[Crear una plantilla de datos](creating.md)

Plantillas de datos se pueden crear en línea, en un [ `ResourceDictionary` ](https://developer.xamarin.com/api/type/Xamarin.Forms.ResourceDictionary/), o desde un tipo personalizado o un tipo de celda Xamarin.Forms adecuado. Si no hay ninguna necesidad de volver a usar la plantilla de datos en otra parte, debe usarse una plantilla en línea. Como alternativa, se puede reutilizar una plantilla de datos definiendo como un tipo personalizado, o como un recurso de nivel de página o el nivel de aplicación de nivel de control.

## <a name="creating-a-datatemplateselectorselectormd"></a>[Crear un DataTemplateSelector](selector.md)

A [ `DataTemplateSelector` ](https://developer.xamarin.com/api/type/Xamarin.Forms.DataTemplateSelector/) puede usarse para elegir un [ `DataTemplate` ](https://developer.xamarin.com/api/type/Xamarin.Forms.DataTemplate/) en tiempo de ejecución en función del valor de una propiedad enlazada a datos. Esto permite que varios `DataTemplate` instancias que se aplicará al mismo tipo de objeto, para personalizar la apariencia de los objetos concretos. En este artículo se muestra cómo crear y consumir un `DataTemplateSelector`.


## <a name="related-links"></a>Vínculos relacionados

- [Plantillas de datos (ejemplo)](https://developer.xamarin.com/samples/xamarin-forms/templates/datatemplates/)
