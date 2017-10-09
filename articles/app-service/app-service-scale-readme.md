---
title: "Usługa aplikacji Azure: Skalowanie aplikacji usługi aplikacji"
description: "Dowiedz się, dokumentów i ins hello skalowania aplikacji w usłudze App Service."
keywords: app service, azure app service, scale, scalable, app service plan, app service cost
services: app-service
documentationcenter: 
author: btardif
manager: erikre
editor: 
ms.assetid: f403c971-4450-432b-8cea-3eeb426c0147
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/07/2016
ms.author: byvinyal
ms.openlocfilehash: d8cd12f73915a916a75d46da2f751a40d567b189
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-scaling-app-service-applications"></a>Usługa aplikacji Azure: Skalowanie aplikacji usługi aplikacji
Aplikacje hostowane w usłudze Azure App Service można [osiągnięcia bardzo dużej skali](https://azure.microsoft.com/blog/canadian-broadcasting-corporation-radio-canada-leverage-azure-for-smooth-election-coverage/).
Jednak skalowanie aplikacji to złożony problem, który nie ma rozwiązania "dostosowane do wszystkich". toocorrectly skalowanie aplikacji przyczyni Powodzenie aplikacji tooyour 3 klucza obszary:

1. Opis architektury aplikacji i jej słabe strony algorytmu.
   * To jest Twoje Stateful aplikacji? Bezstanowe?
   * Co to są wszystkie składniki hello aplikacji?
     * Gdzie są wąskich gardeł hello w aplikacji hello?
   * Gdy obciążenie zastosowane tooyour aplikacji, co spowoduje przerwanie pierwszy?
2. Opis hello oczekiwano wymagania dotyczące wydajności i obciążenia.
   * Czy aplikacja hello musi tooserve tysiąca użytkowników? lub milion?
   * Zostanie ruchu pochodzić z jednej lokalizacji geograficznej lub globalnie?
   * Czy istnieją różnice w okresach? pików ruchu?
   * Szybkość aplikacji hello powinno odpowiedzieć? 1 sekundę? 1 milisekundy?
3. Opis i poprawnie platformy hello wykorzystać hosting aplikacji.
   * Funkcje należy wykorzystać I tooachieve Moje cele skali?

W tej sekcji pomoże Ci zrozumieć wszystkie czynniki hello i pomocy opracować strategię wykorzystującego hello niezbędne usługi aplikacji — funkcje tooachieve cele skalowalności.

[!INCLUDE [app-service-blueprint-scaling-app-service-applications](../../includes/app-service-blueprint-scaling-app-service-applications.md)]

