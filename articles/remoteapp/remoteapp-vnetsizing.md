---
title: "Ustawianie rozmiaru informacji dla sieci Wirtualnej w usłudze Azure RemoteApp | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat wymagania dotyczące adresów IP dla usługi Azure RemoteApp z sieci Wirtualnej"
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
ms.openlocfilehash: 9375981db64ec4a1ae523e958423b5f5787cec33
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="sizing-information-for-a-vnet-in-azure-remoteapp"></a>Informacje dotyczące zmiany rozmiaru sieci wirtualnej w usłudze Azure RemoteApp
> [!IMPORTANT]
> Usługa Azure RemoteApp nie będzie obsługiwana od 31 sierpnia 2017 r. Szczegółowe informacje zawiera [powiadomienie](https://go.microsoft.com/fwlink/?linkid=821148).
> 
> 

Gdy używasz usługi Azure RemoteApp z siecią wirtualną (VNET), programów RemoteApp używa adresów IP w podsieci. Oparte na skali z usługą RemoteApp, należy się upewnić, że podsieć ma za mało adresów IP dostępnej dla maszyn wirtualnych usługi RemoteApp. Gdy w tych wskazówkach zmiany rozmiaru nie jest idealne jak RemoteApp dynamicznie się obraca i obraca dół maszyn wirtualnych w ramach kolekcji, pomoże Ci oszacować zakres podsieci. Jest to szczególnie ważne, ponieważ po usługi RemoteApp znajduje się w sieci Wirtualnej, nie można zwiększyć rozmiar podsieci bez usuwania programów RemoteApp.

Dla każdej kolekcji usługi RemoteApp, którą chcesz uruchomić maksymalnie wykorzystując swoje możliwości powinien mieć 100 dostępnych adresów IP. Na przykład jeśli masz jednej kolekcji usługi RemoteApp w planie Standard i mają maksymalną 500 użytkowników, powinien mieć 100 adresów IP dla tej kolekcji. Podobnie należy 100 adresów IP dla kolekcji usługi RemoteApp w planie Basic mającą 800 użytkownicy. Jeśli planujesz mniejszą liczbę użytkowników (mniejszy niż maksymalny), można zmniejszyć adresy IP wymagane na kolekcję. Wymagany rozmiar minimalny podsieci to 30 adresów IP (/ 27).

Sprawdź następujące informacje, aby upewnić się, że sieć wirtualna jest skonfigurowana i działa propertly:

* [Migracja z osobistego sieci Wirtualnej do sieć Wirtualną platformy Azure](remoteapp-migratevnet.md)
* [Sprawdzanie poprawności sieci Wirtualnej platformy Azure do użycia z usługą Azure RemoteApp](remoteapp-vnet.md)

