---
title: aaaOverview typowe wzorce skalowania automatycznego | Dokumentacja firmy Microsoft
description: "Dowiedz się, że niektóre hello typowe wzorce tooauto skalowania zasobu na platformie Azure."
author: anirudhcavale
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: d37d3fda-8ef1-477c-a360-a855b418de84
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/07/2017
ms.author: ancav
ms.openlocfilehash: fc5bd97852e0af01aa32940c99721ab8e21033ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-common-autoscale-patterns"></a>Omówienie typowe wzorce skalowania automatycznego
W tym artykule opisano niektóre typowe tooscale wzorce hello zasobu na platformie Azure.

Azure automatyczne skalowanie monitora dotyczy tylko tooVirtual zestawy skalowania maszyny (VMSS), usługi w chmurze, planów usługi aplikacji i środowiska usługi app service. 

# <a name="lets-get-started"></a>Umożliwia wprowadzenie

W tym artykule przyjęto założenie, że czytelnik zna automatyczne skalowanie. Możesz [Pobierz wprowadzenie tooscale tutaj zasobu][1]. Witaj poniżej przedstawiono niektóre typowe wzorce skali hello.

## <a name="scale-based-on-cpu"></a>Oparte na Procesorze skali

Aplikacja sieci web (/ VMSS/chmury usługi roli) i 

- Ma tooscale poza/skali w na podstawie procesora CPU.
- Ponadto chcesz tooensure jest minimalna liczba wystąpień. 
- Ponadto chcesz tooensure ustawioną maksymalny limit toohello liczba wystąpień, które można skalować.

![Oparte na Procesorze skali][2]

## <a name="scale-differently-on-weekdays-vs-weekends"></a>Skalowanie inaczej w weekendy vs dni tygodnia

Aplikacja sieci web (/ VMSS/chmury usługi roli) i

- Ma domyślnie wystąpień 3 (w dni robocze)
- Nieoczekiwanie ruchu w weekendy, i dlatego należy tooscale dół too1 wystąpienia w weekendy.

![Skalowanie inaczej w weekendy vs dni tygodnia][3]

## <a name="scale-differently-during-holidays"></a>Skalowanie inaczej w dni wolne

Aplikacja sieci web (/ VMSS/chmury usługi roli) i 

- Ma tooscale góra/dół oparte na użycie procesora CPU domyślnie
- Jednak podczas świąt (lub określone dni, które są ważne dla biznesu) ma domyślne hello toooverride i mieć większej pojemności do Twojej dyspozycji.

![Święta inaczej w skali][4]

## <a name="scale-based-on-custom-metric"></a>Skalowanie w oparciu metryki niestandardowe

Masz frontonu sieci web i warstwy interfejsu API, który komunikuje się z hello wewnętrznej bazy danych. 

- Ma tooscale hello interfejsu API warstwy na podstawie zdarzeń niestandardowych w frontonu hello (przykład: chcesz tooscale procesu wyewidencjonowania na podstawie hello liczby elementów w koszyku hello)

![Skalowanie w oparciu metryki niestandardowe][5]

<!--Reference-->
[1]: ./monitoring-autoscale-get-started.md
[2]: ./media/monitoring-autoscale-common-scale-patterns/scale-based-on-cpu.png
[3]: ./media/monitoring-autoscale-common-scale-patterns/weekday-weekend-scale.png
[4]: ./media/monitoring-autoscale-common-scale-patterns/holidays-scale.png
[5]: ./media/monitoring-autoscale-common-scale-patterns/custom-metric-scale.png