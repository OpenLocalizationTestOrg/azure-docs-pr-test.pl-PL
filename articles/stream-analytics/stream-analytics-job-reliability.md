---
title: "Uniknąć przerw w działaniu usługi z zadania usługi analiza strumienia Azure | Dokumentacja firmy Microsoft"
description: "Wskazówki na temat tworzenia Twojej usługi analiza strumienia zadań uaktualniania odporność."
services: stream-analytics
documentationCenter: 
authors: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 3ac65c93ecb47e93e963dd9869a7af70f73b19c7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="guarantee-stream-analytics-job-reliability-during-service-updates"></a>Zagwarantować niezawodność zadania usługi analiza strumienia podczas aktualizacji usługi

Część jest w pełni zarządzana usługa jest hello możliwości toointroduce nowej usługi funkcji i ulepszeń w tempie szybkie. W związku z tym usługi analiza strumienia może mieć aktualizacji usługi wdrażanie na podstawie co tydzień (lub częstsze). Niezależnie od tego, ile testów jest wykonywane jest nadal ryzyko, że istniejący, uruchomione zadania mogą być dzielone powodu wprowadzenia toohello usterki. Dla klientów, którzy uruchomić krytycznego zadania przesyłania strumieniowego przetwarzania te zagrożenia, należy unikać toobe. Mechanizm mogą używać tooreduce to zagrożenie jest platformy Azure  **[sparowanego region](https://docs.microsoft.com/azure/best-practices-availability-paired-regions)**  modelu. 

## <a name="how-do-azure-paired-regions-address-this-concern"></a>Jak regiony platformy Azure sparowanym rozwiązania tego problemu?

Analiza strumienia gwarantuje, że zadania w parach regiony są aktualizowane w oddzielnych partiach. W związku z tym istnieje wystarczająca odstęp czasu między aktualizacjami hello tooidentify potencjalne dzielenie usterek i usuwać z nich.

_Z wyjątkiem hello Indie środkowe_ (których sparowanego regionu, Indie Południowe nie ma obecności Stream Analytics), wdrożenie hello tooStream aktualizacji Analytics nie może mieć miejsce, w hello sam czasu w zestawie regionów sparowany. Wdrożenia w wielu regionach **w hello tej samej grupie** może wystąpić **na powitania jednocześnie**.

Artykuł Hello na  **[dostępności i regiony sparowanego](https://docs.microsoft.com/azure/best-practices-availability-paired-regions)**  ma hello najbardziej aktualne informacje, na którym są skojarzone regionów.

Klienci są toodeploy zaleca identyczne zadania tooboth łączyć regionów. Ponadto zaleca się tooStream Analytics wewnętrznego, możliwości, klienci są również toomonitor hello zadania tak, jakby **zarówno** zadań produkcji. Jeśli podział toobe zidentyfikowanego w wyniku aktualizacji usługi Stream Analytics hello, eskalować odpowiednio i tryb failover wszelkie dane wyjściowe zadania w dobrej kondycji toohello podrzędne konsumentów. Toosupport eskalacji region sparowanego hello zapobiec wpływowi hello nowe wdrożenie, a zachowanie spójności hello hello łączyć zadań.
