---
title: MDocArchiveToMsxDocConverter.exe no se encuentra rver. BaseCommand.OnRequest
ms.topic: article
ms.prod: xamarin
ms.assetid: F5AC6AC4-0E7C-4746-A7CF-872F0E75AFF4
ms.technology: xamarin-ios
author: bradumbaugh
ms.author: brumbaug
ms.date: 03/21/2017
ms.openlocfilehash: 1e49c270d5836379d60f50ec72960ddc83bfbba4
ms.sourcegitcommit: 73bd0c7e5f237f0a1be70a6c1384309bb26609d5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/22/2018
---
# <a name="mdocarchivetomsxdocconverterexe-not-found-rverbasecommandonrequest"></a>MDocArchiveToMsxDocConverter.exe no se encuentra rver. BaseCommand.OnRequest

> [!IMPORTANT]
> Este problema se ha resuelto en versiones recientes de Xamarin. Sin embargo, si el problema se produce en la versión más reciente del software, registre una [nuevo error](~/cross-platform/troubleshooting/questions/howto-file-bug.md) con el control de versiones completo completa y la información de los resultados de registro de compilación.


## <a name="error-message"></a>Mensaje de error

Este error puede aparecer en el *registro del servidor Mac* en Visual Studio:

```
Error: /Developer/MonoTouch/usr/share/doc/MonoTouch/MDocArchiveToMsxDocConverter.exe not found
 rver.BaseCommand.OnRequest (System.Net.HttpListenerContext context, System.Object commandRequestState) [0x00000] in <filename unknown>:0
  at Mtb.Server.Listener.OnRequest (System.Object state) [0x00000] in <filename unknown>:0
```

Hay 2 problemas independientes en este mensaje:

1.  `Error: /Developer/MonoTouch/usr/share/doc/MonoTouch/MDocArchiveToMsxDocConverter.exe not found`

    Este error resulta inofensivo, pero también se presta a confusión. Se [se quitarán](https://bugzilla.xamarin.com/show_bug.cgi?id=21667) en una versión futura.

2.  `rver.BaseCommand.OnRequest (System.Net.HttpListenerContext context …`

    Este error es el problema real. Desafortunadamente, debido a un [limitación](https://bugzilla.xamarin.com/show_bug.cgi?id=22080) este seguimiento de pila de excepción es *incompleta*. Si observa un seguimiento de pila incompleta similar al siguiente en el registro de servidor de Mac, puede comprobar la `~/Library/Logs/Xamarin/MonoTouchVS/mtbserver.log` archivo en el host de compilación de Mac para encontrar el seguimiento de pila completo.
