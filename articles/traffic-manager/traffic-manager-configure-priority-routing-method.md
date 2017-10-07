---
title: "priorytet aaaConfigure ruchu metody routingu za pomocą usługi Azure Traffic Manager | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak priorytet hello tooconfigure ruchu metody routingu w usłudze Traffic Manager"
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
editor: 
ms.assetid: 6dca6de1-18f7-4962-bd98-6055771fab22
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/20/2017
ms.author: kumud
ms.openlocfilehash: dd3e3bb2a727e5ea087cee35962c8e6f7c357282
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-priority-traffic-routing-method-in-traffic-manager"></a>Konfigurowanie metody routingu ruchu priorytet w usłudze Traffic Manager

Niezależnie od hello trybu witryny sieci Web witryn sieci Web Azure już udostępniają funkcje trybu failover dla witryn sieci Web w centrum danych (regionu). Menedżer ruchu zapewnia tryb failover dla witryn sieci Web w różnych centrach danych.

Wzorzec wspólnej pracy awaryjnej usługi toosend ruchu tooa podstawowej usługi i zapewnia zbiór identyczne usługi tworzenia kopii zapasowych w trybie failover. Witaj poniższych krokach opisano sposób tooconfigure to priorytety trybu failover z usług w chmurze Azure i witryn sieci Web:

## <a name="tooconfigure-hello-priority-traffic-routing-method"></a>metody routingu ruchu tooconfigure hello priorytet

1. W przeglądarce, zaloguj się toohello [portalu Azure](http://portal.azure.com). Jeśli jeszcze nie masz konta, możesz skorzystać z [bezpłatnej miesięcznej wersji próbnej](https://azure.microsoft.com/free/). 
2. Na pasku wyszukiwania portalu hello, wyszukaj hello **profilów usługi Traffic Manager** a następnie kliknij nazwę profilu hello, które tooconfigure hello metody routingu dla.
3. W hello **profilu usługi Traffic Manager** bloku, sprawdź, czy oba hello usługi w chmurze i witryn sieci Web mają tooinclude w konfiguracji są obecne.
4. W hello **ustawienia** kliknij **konfiguracji**w hello **konfiguracji** bloku ukończenia w następujący sposób:
    1. Dla **ustawienia metody routingu ruchu**, sprawdź, czy metody routingu ruchu hello **priorytet**. Jeśli nie, kliknij przycisk **priorytet** z listy rozwijanej hello.
    2. Zestaw hello **ustawienia monitora punktu końcowego** identyczne dla wszystkich każdego punktu końcowego, w tym profilu w następujący sposób:
        1. Wybierz odpowiednie hello **protokołu**i określ hello **portu** numer. 
        2. Aby uzyskać **ścieżki** wpisz ukośnik  */* . punkty końcowe toomonitor, należy określić ścieżkę i nazwę pliku. A ukośnika "/" jest prawidłowym wpisem hello ścieżki względnej i wskazuje, czy plik hello znajduje się w katalogu głównym hello (ustawienie domyślne).
        3. U góry hello hello strony, kliknij przycisk **zapisać**.
5. W hello **ustawienia** kliknij **punkty końcowe**.
6. W hello **punkty końcowe** bloku, przejrzyj hello kolejność priorytetów punktów końcowych. Po wybraniu hello **priorytet** ma znaczenie kolejności hello punktów końcowych hello wybrane metody routingu ruchu. Sprawdź hello kolejność priorytetów punktów końcowych.  podstawowy punkt końcowy: Hello jest u góry. Sprawdź w kolejności hello jest wyświetlany. wszystkie żądania zostanie routingiem toohello pierwszym punktem końcowym i w przypadku wykrycia przez Menedżera ruchu jest zła, ruch hello automatycznie przełącza toohello następnego punktu końcowego. 
7. toochange hello priorytetu punktu końcowego, kliknij punkt końcowy hello w hello **punktu końcowego** bloku, który jest wyświetlany, kliknij przycisk **Edytuj** i zmień hello **priorytet** wartości zgodnie z potrzebami . 
8. Kliknij przycisk **zapisać** toosave hello ustawień punktu końcowego.
9. Po zakończeniu zmiany w konfiguracji, kliknij przycisk **zapisać** u dołu hello hello strony.
10. Przetestuj hello zmiany w konfiguracji w następujący sposób:
    1.  Na pasku wyszukiwania portalu hello Wyszukaj nazwę profilu usługi Traffic Manager hello, a następnie kliknij przycisk hello profilu usługi Traffic Manager w wynikach hello tego hello wyświetlane.
    2.  W hello **Traffic Manager** bloku, kliknij opcję **omówienie**.
    3.  Witaj **profilu usługi Traffic Manager** bloku Wyświetla nazwę DNS hello nowo utworzony profil Menedżera ruchu. Może to posłużyć żadnych klientów (na przykład, przechodząc opcję tooit za pomocą przeglądarki sieci web) tooget kierowane toohello prawy punkt końcowy określone przez typ routingu hello. W takim przypadku wszystkie żądania są routingiem toohello pierwszym punktem końcowym i w przypadku wykrycia przez Menedżera ruchu jest zła, ruch hello automatycznie przełącza toohello następnego punktu końcowego.
11. Po działa profilu Menedżera ruchu, należy edytować rekord DNS hello z autorytatywnych toopoint serwera DNS nazwę domeny firmowej domeny nazwa toohello Menedżera ruchu.

![Konfigurowanie metody routingu ruchu priorytet przy użyciu Menedżera ruchu][1]

## <a name="next-steps"></a>Następne kroki


- Dowiedz się więcej o [ważone metody routingu ruchu](traffic-manager-configure-weighted-routing-method.md).
- Dowiedz się więcej o [metody routingu wydajności](traffic-manager-configure-performance-routing-method.md).
- Dowiedz się więcej o [geograficzne metody routingu](traffic-manager-configure-geographic-routing-method.md).
- Dowiedz się, jak za[Menedżera ruchu ustawienia testu](traffic-manager-testing-settings.md).

<!--Image references-->
[1]: ./media/traffic-manager-priority-routing-method/traffic-manager-priority-routing-method.png