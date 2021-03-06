---
title: "Corrector ortográfico mediante la API de Bing corrector ortográfico"
description: "Bing corrector ortográfico realiza la revisión ortográfica contextual para el texto, proporciona sugerencias de en línea para las palabras mal escritas. En este artículo se explica cómo utilizar la API de REST comprobar de Bing corrector para corregir los errores de ortografía en una aplicación de Xamarin.Forms."
ms.topic: article
ms.prod: xamarin
ms.assetid: B40EB103-FDC0-45C6-9940-FB4ACDC2F4F9
ms.technology: xamarin-forms
author: davidbritch
ms.author: dabritch
ms.date: 02/08/2017
ms.openlocfilehash: ad2bdf27323fd7d7e108a25387cd6aea6d442098
ms.sourcegitcommit: 61f5ecc5a2b5dcfbefdef91664d7460c0ee2f357
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/28/2018
---
# <a name="spell-checking-using-the-bing-spell-check-api"></a>Corrector ortográfico mediante la API de Bing corrector ortográfico

_Bing corrector ortográfico realiza la revisión ortográfica contextual para el texto, proporciona sugerencias de en línea para las palabras mal escritas. En este artículo se explica cómo utilizar la API de REST comprobar de Bing corrector para corregir los errores de ortografía en una aplicación de Xamarin.Forms._

## <a name="overview"></a>Información general

La API de REST comprobar de Bing corrector tiene dos modos de funcionamiento, y se debe especificar un modo al realizar una solicitud a la API:

- `Spell` corrige un texto breve (hasta 9 palabras vacías) sin realizar ningún cambio de mayúsculas y minúsculas.
- `Proof` corrige texto largo, proporciona correcciones de mayúsculas y minúsculas y signos de puntuación básica y suprime correcciones rigurosa.

Para usar la API de Bing corrector comprobar, se debe obtener una clave de API. Esto se puede obtener en [Introducción gratuitamente](https://www.microsoft.com/cognitive-services/sign-up?ReturnUrl=/cognitive-services/subscriptions?productId=%2fproducts%2fBing.Speech.Preview) en microsoft.com.

Para obtener una lista de los idiomas admitidos por la API de Bing corrector comprobar, consulte [compatibilidad con idiomas](https://www.microsoft.com/cognitive-services/Bing-Spell-check-API/documentation#language-support) en microsoft.com. Para obtener más información acerca de la API de Bing corrector comprobar, consulte [API de Bing corrector comprobar](https://www.microsoft.com/cognitive-services/bing-spell-check-api/documentation) en microsoft.com.

## <a name="authentication"></a>Autenticación

Todas las solicitudes realizadas a la API de Bing corrector comprobar requiere una clave de API que se debe especificar como el valor de la `Ocp-Apim-Subscription-Key` encabezado. En el ejemplo de código siguiente se muestra cómo agregar la clave de API para el `Ocp-Apim-Subscription-Key` encabezado de una solicitud:

```csharp
using (var httpClient = new HttpClient())
{
  httpClient.DefaultRequestHeaders.Add("Ocp-Apim-Subscription-Key", apiKey);
  ...
}
```

Error al pasar una clave de API válida a la API de Bing corrector comprobar producirá un error de 401 respuesta.

## <a name="performing-spell-checking"></a>Realizar la revisión ortográfica

Corrector ortográfico se puede lograr mediante la realización de una solicitud GET o POST para la `SpellCheck` API en `https://api.cognitive.microsoft.com/bing/v5.0/SpellCheck`. Al realizar una solicitud GET, el texto que se va a comprobar la ortografía se envía como un parámetro de consulta. Al realizar una solicitud POST, se envía el texto que se va a comprobar la ortografía en el cuerpo de solicitud. Las solicitudes GET se limitan a 1500 caracteres debido a la limitación de longitud de cadena de parámetro de consulta de revisión ortográfica. Por lo tanto, las solicitudes POST normalmente se realizará a menos que cadenas cortas se va a comprobar la ortografía.

En la aplicación de ejemplo, el `SpellCheckTextAsync` método invoca el proceso de revisión ortográfica:

```csharp
public async Task<SpellCheckResult> SpellCheckTextAsync(string text)
{
  string requestUri = GenerateRequestUri(Constants.BingSpellCheckEndpoint, text, SpellCheckMode.Spell);
  var response = await SendRequestAsync(requestUri, Constants.BingSpellCheckApiKey);
  var spellCheckResults = JsonConvert.DeserializeObject<SpellCheckResult>(response);
  return spellCheckResults;
}
```

El `SpellCheckTextAsync` método genera un URI de solicitud y, a continuación, envía la solicitud a la `SpellCheck` API, que devuelve una respuesta JSON que contiene el resultado. La respuesta JSON se deserializa, con lo que se devuelve al método de llamada para su presentación.

Para obtener más información acerca de la API de REST comprobar corrector de Bing, consulte [corrector comprobar API](https://dev.cognitive.microsoft.com/docs/services/56e73033cf5ff80c2008c679/operations/57855119bca1df1c647bc358) en microsoft.com.

### <a name="configuring-spell-checking"></a>Configuración de la revisión ortográfica

El proceso de revisión ortográfica puede configurarse mediante la especificación de parámetros de consulta HTTP. Hay parámetros obligatorios y opcionales, con el método siguiente que muestra los parámetros obligatorios que se deben establecer para una solicitud GET:

```csharp
string GenerateRequestUri(string spellCheckEndpoint, string text, SpellCheckMode mode)
{
  string requestUri = spellCheckEndpoint;
  requestUri += string.Format("?text={0}", text);                         // text to spell check
  requestUri += string.Format("&mode={0}", mode.ToString().ToLower());    // spellcheck mode - proof or spell
  return requestUri;
}
```

Este método establece el texto que se va a comprobar la ortografía y el modo de comprobación de corrección ortográfica.

Para obtener más información acerca de los parámetros obligatorios y opcionales, consulte [corrector comprobar API](https://dev.cognitive.microsoft.com/docs/services/56e73033cf5ff80c2008c679/operations/57855119bca1df1c647bc358) en microsoft.com.

### <a name="sending-the-request"></a>Enviar la solicitud

El `SendRequestAsync` método realiza la solicitud GET a la API de REST Bing corrector comprobar y devuelve la respuesta:

```csharp
async Task<string> SendRequestAsync(string url, string apiKey)
{
  using (var httpClient = new HttpClient())
  {
    httpClient.DefaultRequestHeaders.Add("Ocp-Apim-Subscription-Key", apiKey);
    var response = await httpClient.GetAsync(url);
    return await response.Content.ReadAsStringAsync();
  }
}
```

Este método crea la solicitud GET mediante la adición de la clave de API como el valor de la `Ocp-Apim-Subscription-Key` encabezado. A continuación, se envía la solicitud GET a la `SpellCheck` API, con la dirección URL de solicitud especifica el texto que se deben traducir y el modo de comprobación de corrección ortográfica. La respuesta, a continuación, lee y devuelve al método de llamada.

El `SpellCheck` API enviará el código de estado HTTP 200 (OK) en la respuesta, siempre que la solicitud es válida, lo que indica que la solicitud es correcta y que la información solicitada está en la respuesta. Para obtener una lista de posibles respuestas de error, vea las respuestas en [corrector comprobar API](https://dev.cognitive.microsoft.com/docs/services/56e73033cf5ff80c2008c679/operations/57855119bca1df1c647bc358) en microsoft.com.

### <a name="processing-the-response"></a>Procesamiento de la respuesta

La respuesta de la API se devuelve en formato JSON. Los siguientes datos JSON muestran el mensaje de respuesta para el texto mal escrito `Go shappin tommorow`:

```csharp
{
  "_type": "SpellCheck",
  "flaggedTokens": [
    {
      "offset": 3,
      "token": "shappin",
      "type": "UnknownToken",
      "suggestions": [
        {
          "suggestion": "shopping",
          "score": 1
        }
      ]
    },
    {
      "offset": 11,
      "token": "tommorow",
      "type": "UnknownToken",
      "suggestions": [
        {
          "suggestion": "tomorrow",
          "score": 1
        }
      ]
    }
  ]
}
```

El `flaggedTokens` matriz contiene una matriz de palabras del texto que se marcaron como no se ha escrito correctamente o se gramaticalmente incorrecto. La matriz estará vacía si no se encuentran ningún errores ortográficos o gramaticales. Las etiquetas dentro de la matriz son:

- `offset` : un desplazamiento de base cero desde el principio de la cadena de texto a la palabra que se marcó.
- `token` : la palabra en la cadena de texto que no se ha escrito correctamente o no es gramaticalmente correcto.
- `type` : el tipo de error que provocó la palabra se indique. Hay dos valores posibles: `RepeatedToken` y `UnknownToken`.
- `suggestions` : una matriz de palabras que se corregirá el error de ortografía o gramática. La matriz está formada por un `suggestion` y `score`, lo que indica el nivel de confianza de que la corrección sugerida es correcta.

En la aplicación de ejemplo, la respuesta JSON se deserializa en un `SpellCheckResult` instancia, con lo que se devuelve al método de llamada para su presentación. El siguiente ejemplo de código muestra cómo el `SpellCheckResult` instancia se procesa para su presentación:

```csharp
var spellCheckResult = await bingSpellCheckService.SpellCheckTextAsync(TodoItem.Name);
foreach (var flaggedToken in spellCheckResult.FlaggedTokens)
{
  TodoItem.Name = TodoItem.Name.Replace(flaggedToken.Token, flaggedToken.Suggestions.FirstOrDefault().Suggestion);
}
```

Este código recorre en iteración la `FlaggedTokens` colección y reemplaza cualquier mal escrita o palabras gramaticalmente incorrectas en el texto de origen con la primera sugerencia. Las capturas de pantalla siguientes se muestran antes y después de la revisión ortográfica:

![](spell-check-images/before-spell-check.png "Antes de comprobar la ortografía")

![](spell-check-images/after-spell-check.png "Después de comprobar la ortografía")

## <a name="summary"></a>Resumen

Este artículo explica cómo usar la API de REST de deletrear comprobar de Bing para corregir los errores de ortografía en una aplicación de Xamarin.Forms. Bing corrector ortográfico realiza la revisión ortográfica contextual para el texto, proporciona sugerencias de en línea para las palabras mal escritas.



## <a name="related-links"></a>Vínculos relacionados

- [Compruebe la ortografía Bing documentación](https://www.microsoft.com/cognitive-services/bing-spell-check-api/documentation)
- [Consumir un servicio Web RESTful](~/xamarin-forms/data-cloud/consuming/rest.md)
- [Lista de tareas cognitivos servicios (ejemplo)](https://developer.xamarin.com/samples/xamarin-forms/WebServices/TodoCognitiveServices/)
- [API de Bing corrector ortográfico](https://dev.cognitive.microsoft.com/docs/services/56e73033cf5ff80c2008c679/operations/57855119bca1df1c647bc358)
