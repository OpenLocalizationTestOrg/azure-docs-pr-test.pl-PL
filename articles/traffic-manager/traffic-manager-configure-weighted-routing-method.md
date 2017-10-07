---
title: "aaaConfigure ważone działanie okrężne ruchu metody routingu za pomocą usługi Azure Traffic Manager | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak tooload równoważenie ruchu przy użyciu metody okrężnego w usłudze Traffic Manager"
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
ms.openlocfilehash: 7e2866ead0b2b653845435dd420a763c5e175f4b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-hello-weighted-traffic-routing-method-in-traffic-manager"></a>Konfigurowanie metody routingu ruchu hello ważone w usłudze Traffic Manager

Wzorzec typowe metody routingu ruchu jest tooprovide zbiór identyczne punkty końcowe, które obejmują usługi w chmurze i witryn sieci Web i wysyłania ruchu tooeach w działaniu okrężnym. Witaj następujące kroki przedstawiają sposób tooconfigure to typ Metoda routingu ruchu.

> [!NOTE]
> Witryn sieci Web Azure zapewniają już obciążenia okrężnego równoważenia funkcji dla witryn sieci Web w centrum danych (regionu). Menedżer ruchu umożliwia toospecify metody routingu ruchu okrężnego dla witryn sieci Web w różnych centrach danych.

## <a name="tooconfigure-hello-weighted-traffic-routing-method"></a>metody routingu ruchu hello ważone tooconfigure

1. W przeglądarce, zaloguj się toohello [portalu Azure](http://portal.azure.com). Jeśli jeszcze nie masz konta, możesz skorzystać z [bezpłatnej miesięcznej wersji próbnej](https://azure.microsoft.com/free/). 
2. Na pasku wyszukiwania portalu hello, wyszukaj hello **profilów usługi Traffic Manager** a następnie kliknij nazwę profilu hello, które tooconfigure hello metody routingu dla.
3. W hello **profilu usługi Traffic Manager** bloku, sprawdź, czy oba hello usługi w chmurze i witryn sieci Web mają tooinclude w konfiguracji są obecne.
4. W hello **ustawienia** kliknij **konfiguracji**w hello **konfiguracji** bloku ukończenia w następujący sposób:
    1. Aby uzyskać **ustawienia metody routingu ruchu**, sprawdź, czy metody routingu ruchu hello **ważone**. Jeśli nie, kliknij przycisk **ważone** z listy rozwijanej hello.
    2. Zestaw hello **ustawienia monitora punktu końcowego** identyczne dla wszystkich każdego punktu końcowego, w tym profilu w następujący sposób:
        1. Wybierz odpowiednie hello **protokołu**i określ hello **portu** numer. 
        2. Aby uzyskać **ścieżki** wpisz ukośnik  */* . punkty końcowe toomonitor, należy określić ścieżkę i nazwę pliku. A ukośnika "/" jest prawidłowym wpisem hello ścieżki względnej i wskazuje, czy plik hello znajduje się w katalogu głównym hello (ustawienie domyślne).
        3. U góry hello hello strony, kliknij przycisk **zapisać**.
5. Przetestuj hello zmiany w konfiguracji w następujący sposób:
    1.  Na pasku wyszukiwania portalu hello Wyszukaj nazwę profilu usługi Traffic Manager hello, a następnie kliknij przycisk hello profilu usługi Traffic Manager w wynikach hello tego hello wyświetlane.
    2.  W hello **Traffic Manager** bloku, kliknij opcję **omówienie**.
    3.  Witaj **profilu usługi Traffic Manager** bloku Wyświetla nazwę DNS hello nowo utworzony profil Menedżera ruchu. Może to posłużyć żadnych klientów (na przykład, przechodząc opcję tooit za pomocą przeglądarki sieci web) tooget kierowane toohello prawy punkt końcowy określone przez typ routingu hello. W takim przypadku wszystkie żądania są kierowane każdego punktu końcowego w działaniu okrężnym.
6. Po działa profilu Menedżera ruchu, należy edytować rekord DNS hello z autorytatywnych toopoint serwera DNS nazwę domeny firmowej domeny nazwa toohello Menedżera ruchu.

![Konfigurowanie metody routingu ruchu ważoną przy użyciu Menedżera ruchu][1]

## <a name="next-steps"></a>Następne kroki

- Dowiedz się więcej o [Metoda routingu ruchu priorytet](traffic-manager-configure-priority-routing-method.md).
- Dowiedz się więcej o [wydajności Metoda routingu ruchu](traffic-manager-configure-performance-routing-method.md).
- Dowiedz się więcej o [geograficzne metody routingu](traffic-manager-configure-geographic-routing-method.md).
- Dowiedz się, jak za[Menedżera ruchu ustawienia testu](traffic-manager-testing-settings.md).

<!--Image references-->
[1]: ./media/traffic-manager-weighted-routing-method/traffic-manager-weighted-routing-method.png
