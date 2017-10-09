---
title: "aaaManage punktów końcowych w usłudze Azure Traffic Manager | Dokumentacja firmy Microsoft"
description: "W tym artykule omówiono dodawanie, usuwanie, włączanie i wyłączanie punktów końcowych w usłudze Azure Traffic Manager."
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
editor: 
ms.assetid: ade2bbc2-35a7-43c5-8001-4698f7254526
ms.service: traffic-manager
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/08/2017
ms.author: kumud
ms.openlocfilehash: fc65874ae2eaeb6fca5d8c4f33403c258307bdb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="add-disable-enable-or-delete-endpoints"></a>Dodawanie, usuwanie, włączanie i wyłączanie punktów końcowych

Witaj funkcja Web Apps w usłudze Azure App Service udostępnia już trybu failover i funkcji routingu ruchu okrężnego dla witryn sieci Web w centrum danych, niezależnie od trybu witryny sieci Web hello. Menedżer ruchu Azure umożliwia toospecify trybu failover i routingu ruchu okrężnego dla witryn sieci Web i usług w chmurze w różnych centrach danych. Witaj pierwszy krok niezbędne tooprovide działa tooadd hello chmury usługi lub witryny sieci Web punktu końcowego tooTraffic Manager.

Można również wyłączyć poszczególne punkty końcowe, które są częścią profilu usługi Traffic Manager. Wyłączenie punktu końcowego pozostawia go jako część profilu hello, ale hello profil działa tak, jakby hello punktu końcowego nie znajduje się w nim. Ta akcja przydaje się do tymczasowego usunięcia punktu końcowego, który jest w trybie konserwacji lub jest ponownie wdrażany. Gdy punkt końcowy hello jest ponownie uruchomiony, można ją włączyć.

> [!NOTE]
> Wyłączenie punktu końcowego nie ma nic toodo z jego stanem wdrożenia na platformie Azure. Punkt końcowy w dobrej kondycji pozostaje aktualne i stanie tooreceive ruch nawet po wyłączeniu w usłudze Traffic Manager. Ponadto wyłączenie punktu końcowego w jednym profilu nie wpływa na jego stan w innym profilu.

## <a name="tooadd-a-cloud-service-or-an-app-service-endpoint-tooa-traffic-manager-profile"></a>usługi w chmurze tooadd lub tooa punktu końcowego usługi aplikacji profilu Menedżera ruchu

1. W przeglądarce, zaloguj się toohello [portalu Azure](http://portal.azure.com).
2. Na pasku wyszukiwania portalu hello, wyszukaj hello **profilu usługi Traffic Manager** nazwę mają toomodify, a następnie kliknij profil Menedżera ruchu hello hello wyniki tego hello wyświetlane.
3. W hello **profilu usługi Traffic Manager** bloku w hello **ustawienia** kliknij **punkty końcowe**.
4. W hello **punkty końcowe** bloku, który jest wyświetlany, kliknij przycisk **Dodaj**.
5. W hello **dodać punkt końcowy** bloku ukończenia w następujący sposób:
    1. Dla opcji **Typ** kliknij pozycję **Punkt końcowy platformy Azure**.
    2. Podaj **nazwa** za pomocą którego chcesz toorecognize tego punktu końcowego.
    3. Aby uzyskać **typu zasobu docelowego**, z listy rozwijanej Witaj, wybierz hello odpowiedni typ zasobu.
    4. Dla **zasób docelowy**, z hello listy rozwijanej, wybierz zasób docelowy odpowiednie hello tooshow hello listy zasobów w ramach hello tej samej subskrypcji w hello **bloku zasobów**. W hello **zasobów** bloku, który jest wyświetlany, wybierz hello usługi, które mają tooadd jako hello pierwszym punktem końcowym.
    5. Dla opcji **Priorytet** wybierz wartość **1**. Powoduje to całego ruchu kierowanego toothis punktu końcowego, jeśli jest w dobrej kondycji.
    6. Pozycję **Dodaj jako wyłączone** pozostaw niezaznaczoną.
    7. Kliknij przycisk **OK**.
6.  Powtórz kroki 4 i 5 tooadd hello następnego punktu końcowego platformy Azure. Upewnij się, że tooadd go z jego **priorytet** ustawioną wartość **2**.
7.  Po zakończeniu dodawania hello oba punkty końcowe są wyświetlane w hello **profilu usługi Traffic Manager** bloku wraz z ich monitorowania statusu **Online**.

> [!NOTE]
> Po dodaniu lub usunięciu punktu końcowego z profilu przy użyciu hello *pracy awaryjnej* Metoda routingu ruchu, listy priorytetów trybu failover hello może nie być uporządkowane one sposób. Można dostosować kolejność hello hello listy priorytetów trybu Failover na stronie konfiguracji hello. Aby uzyskać więcej informacji, zobacz [Konfigurowanie routingu ruchu dla trybu failover](traffic-manager-configure-failover-routing-method.md).

## <a name="toodisable-an-endpoint"></a>toodisable punktu końcowego

1. W przeglądarce, zaloguj się toohello [portalu Azure](http://portal.azure.com).
2. Na pasku wyszukiwania portalu hello, wyszukaj hello **profilu usługi Traffic Manager** nazwa, że chcesz toomodify, a następnie kliknij profil Menedżera ruchu hello w wynikach hello, które są wyświetlane.
3. W hello **profilu usługi Traffic Manager** bloku w hello **ustawienia** kliknij **punkty końcowe**. 
4. Kliknij punkt końcowy hello, które mają toodisable, a następnie na powitania **punktu końcowego** bloku, który jest wyświetlany, kliknij przycisk **Edytuj**.
5. W hello **punktu końcowego** bloku za zmianę stanu punktu końcowego hello**wyłączone**, a następnie kliknij przycisk **zapisać**.
6. Klienci kontynuują punktu końcowego toohello ruchu toosend hello okres czasu wygaśnięcia (TTL). Możesz zmienić hello TTL na stronie konfiguracji hello hello profilu usługi Traffic Manager.

## <a name="tooenable-an-endpoint"></a>tooenable punktu końcowego

1. W przeglądarce, zaloguj się toohello [portalu Azure](http://portal.azure.com).
2. Na pasku wyszukiwania portalu hello, wyszukaj hello **profilu usługi Traffic Manager** nazwa, że chcesz toomodify, a następnie kliknij profil Menedżera ruchu hello w wynikach hello, które są wyświetlane.
3. W hello **profilu usługi Traffic Manager** bloku w hello **ustawienia** kliknij **punkty końcowe**. 
4. Kliknij punkt końcowy hello, które mają toodisable, a następnie na powitania **punktu końcowego** bloku, który jest wyświetlany, kliknij przycisk **Edytuj**.
5. W hello **punktu końcowego** bloku za zmianę stanu punktu końcowego hello**włączone**, a następnie kliknij przycisk **zapisać**.
6. Klienci kontynuują punktu końcowego toohello ruchu toosend hello okres czasu wygaśnięcia (TTL). Możesz zmienić hello TTL na stronie konfiguracji hello hello profilu usługi Traffic Manager.

## <a name="toodelete-an-endpoint"></a>toodelete punktu końcowego

1. W przeglądarce, zaloguj się toohello [portalu Azure](http://portal.azure.com).
2. Na pasku wyszukiwania portalu hello, wyszukaj hello **profilu usługi Traffic Manager** nazwa, że chcesz toomodify, a następnie kliknij profil Menedżera ruchu hello w wynikach hello, które są wyświetlane.
3. W hello **profilu usługi Traffic Manager** bloku w hello **ustawienia** kliknij **punkty końcowe**. 
4. Kliknij punkt końcowy hello, które mają toodisable, a następnie na powitania **punktu końcowego** bloku, który jest wyświetlany, kliknij przycisk **Edytuj**.
5. W hello **punktu końcowego** bloku za zmianę stanu punktu końcowego hello**włączone**, a następnie kliknij przycisk **zapisać**.


## <a name="next-steps"></a>Następne kroki

* [Zarządzanie profilami usługi Traffic Manager](traffic-manager-manage-profiles.md)
* [Konfigurowanie metod routingu](traffic-manager-configure-routing-method.md)
* [Rozwiązywanie problemów ze stanem obniżonej wydajności usługi Traffic Manager](traffic-manager-troubleshooting-degraded.md)
* [Zagadnienia dotyczące wydajności usługi Traffic Manager](traffic-manager-performance-considerations.md)
* [Operacje w usłudze Traffic Manager (dokumentacja interfejsu API REST)](http://go.microsoft.com/fwlink/p/?LinkID=313584)

