---
title: Punto flotante
ms.topic: article
ms.prod: xamarin
ms.assetid: 003F25C1-B430-4339-9C95-7DF527EBC699
ms.technology: xamarin-ios
author: bradumbaugh
ms.author: brumbaug
ms.openlocfilehash: 73681a37f15f3dd93c85bafb6bb9d71ab30af85c
ms.sourcegitcommit: 0fdb243b46cf21be47584900805cadcd077121bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/12/2018
---
# <a name="floating-point"></a>Punto flotante

Xamarin.iOS realizará 32 bits y 64 bits operaciones de punto flotante con precisión de 64 bits en ARM de forma predeterminada.  

Mientras esta una mayor precisión está más próximo a los programadores para esperar de operaciones de punto flotante en C# en el escritorio, en dispositivos móviles, que el impacto en el rendimiento puede ser considerable.

Es posible compilar el código de punto flotante de 32 bits para usar operaciones de punto flotante de 32 bits.  Para ello, debe usar al menos Xamarin.iOS 8.10 y conjunto en su iOS basan el panel de opciones en la "mtouch argumentos adicionales" el valor siguiente de la línea de entrada:

     --aot-options=-O=float32

Esto le informará de los compiladores estáticos (compilador estático integrado de Mono, o uno con tecnología de LLVM) para realizar operaciones de punto flotante con valores de punto flotante de 32 bits.
