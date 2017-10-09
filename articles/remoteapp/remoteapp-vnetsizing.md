---
title: "informacje o aaaSizing dla sieci Wirtualnej w usłudze Azure RemoteApp | Dokumentacja firmy Microsoft"
description: "Dowiedz się więcej o hello wymagania dotyczące adresów IP dla usługi Azure RemoteApp z sieci Wirtualnej"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: b6e1c4ba-0236-42b2-bced-69353bf211be
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: f98b831af32c41740b258d122b3e18765be08d97
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="sizing-information-for-a-vnet-in-azure-remoteapp"></a>Informacje dotyczące zmiany rozmiaru sieci wirtualnej w usłudze Azure RemoteApp
> [!IMPORTANT]
> Usługa Azure RemoteApp nie będzie obsługiwana od 31 sierpnia 2017 r. Witaj odczytu [anonsu](https://go.microsoft.com/fwlink/?linkid=821148) szczegółowe informacje.
> 
> 

Gdy używasz usługi Azure RemoteApp z siecią wirtualną (VNET), programów RemoteApp używa adresów IP w podsieci hello. W oparciu o skali hello usługi RemoteApp, należy tooensure czy podsieć ma za mało adresów IP dostępnej dla maszyn wirtualnych usługi RemoteApp. Gdy w tych wskazówkach zmiany rozmiaru nie jest idealne jak RemoteApp dynamicznie się obraca i obraca dół maszyn wirtualnych w ramach kolekcji, pomoże Ci oszacować zakres podsieci. Jest to szczególnie ważne, ponieważ po usługi RemoteApp znajduje się w sieci Wirtualnej, nie możesz zwiększyć rozmiar podsieci hello bez usuwania programów RemoteApp.

Dla każdej kolekcji usługi RemoteApp, które mają toorun maksymalnie wykorzystując swoje możliwości powinien mieć 100 dostępnych adresów IP. Na przykład jeśli masz jednej kolekcji usługi RemoteApp w planie Standard hello i użytkownicy toohave hello maksymalną 500, powinien mieć 100 adresów IP dla tej kolekcji. Podobnie należy 100 adresów IP dla kolekcji usługi RemoteApp w planie Basic hello mającą 800 użytkownicy. Jeśli planujesz toohave mniejszą liczbę użytkowników (mniejsze niż maksymalna hello), można zmniejszyć adresów IP hello wymaganych na kolekcję. wymagany rozmiar minimalny podsieci Hello to 30 adresów IP (/ 27).

Wyewidencjonuj hello następujące informacje toomake upewnić się, że sieć wirtualna jest skonfigurowana i działa propertly:

* [Migracja z osobistego tooan sieci Wirtualnej sieci Wirtualnej Azure](remoteapp-migratevnet.md)
* [Sprawdź poprawność hello toouse sieci Wirtualnej platformy Azure z usługą Azure RemoteApp](remoteapp-vnet.md)

