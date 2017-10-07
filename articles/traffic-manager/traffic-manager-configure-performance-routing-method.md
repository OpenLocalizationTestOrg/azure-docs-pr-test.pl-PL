---
title: "wydajność aaaConfigure ruchu metody routingu za pomocą usługi Azure Traffic Manager | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak tooconfigure tooroute Traffic Manager ruchu toohello punktu końcowego o najniższym opóźnieniu"
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
ms.openlocfilehash: d0ccd4c9de411844c6f36068859265244f4aa52b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-hello-performance-traffic-routing-method"></a>Konfigurowanie metody routingu ruchu hello wydajności

Witaj metody routingu ruchu wydajności umożliwia punktu końcowego toohello ruchu toodirect z hello można uzyskać najmniejsze opóźnienia sieci powitania klienta. Zazwyczaj datacenter hello o najniższym opóźnieniu hello jest hello najbliższej w odległości geograficznych. Tej metody routingu ruchu nie można uwzględnić w czasie rzeczywistym zmiany w konfiguracji sieci lub obciążenia.

##  <a name="tooconfigure-performance-routing-method"></a>Metoda routingu tooconfigure wydajności

1. W przeglądarce, zaloguj się toohello [portalu Azure](http://portal.azure.com). Jeśli jeszcze nie masz konta, możesz skorzystać z [bezpłatnej miesięcznej wersji próbnej](https://azure.microsoft.com/free/). 
2. Na pasku wyszukiwania portalu hello, wyszukaj hello **profilów usługi Traffic Manager** a następnie kliknij nazwę profilu hello, które tooconfigure hello metody routingu dla.
3. W hello **profilu usługi Traffic Manager** bloku, sprawdź, czy oba hello usługi w chmurze i witryn sieci Web mają tooinclude w konfiguracji są obecne.
4. W hello **ustawienia** kliknij **konfiguracji**w hello **konfiguracji** bloku ukończenia w następujący sposób:
    1. Dla **ustawienia metody routingu ruchu**, dla **metody routingu** wybierz **wydajności**.
    2. Zestaw hello **ustawienia monitora punktu końcowego** identyczne dla wszystkich każdego punktu końcowego, w tym profilu w następujący sposób:
        1. Wybierz odpowiednie hello **protokołu**i określ hello **portu** numer. 
        2. Aby uzyskać **ścieżki** wpisz ukośnik  */* . punkty końcowe toomonitor, należy określić ścieżkę i nazwę pliku. A ukośnika "/" jest prawidłowym wpisem hello ścieżki względnej i wskazuje, czy plik hello znajduje się w katalogu głównym hello (ustawienie domyślne).
        3. U góry hello hello strony, kliknij przycisk **zapisać**.
5.  Przetestuj hello zmiany w konfiguracji w następujący sposób:
    1.  Na pasku wyszukiwania portalu hello Wyszukaj nazwę profilu usługi Traffic Manager hello, a następnie kliknij przycisk hello profilu usługi Traffic Manager w wynikach hello tego hello wyświetlane.
    2.  W hello **Traffic Manager** bloku, kliknij opcję **omówienie**.
    3.  Witaj **profilu usługi Traffic Manager** bloku Wyświetla nazwę DNS hello nowo utworzony profil Menedżera ruchu. Może to posłużyć żadnych klientów (na przykład, przechodząc opcję tooit za pomocą przeglądarki sieci web) tooget kierowane toohello prawy punkt końcowy określone przez typ routingu hello. W takim przypadku wszystkie żądania są punkt końcowy routingiem toohello o najniższym opóźnieniu hello z sieci powitania klienta.
6. Po działa profilu Menedżera ruchu, należy edytować rekord DNS hello z autorytatywnych toopoint serwera DNS nazwę domeny firmowej domeny nazwa toohello Menedżera ruchu.

![Konfigurowanie metody routingu ruchu wydajności przy użyciu Menedżera ruchu][1]

## <a name="next-steps"></a>Następne kroki

- Dowiedz się więcej o [ważone metody routingu ruchu](traffic-manager-configure-weighted-routing-method.md).
- Dowiedz się więcej o [metody routingu priorytet](traffic-manager-configure-priority-routing-method.md).
- Dowiedz się więcej o [geograficzne metody routingu](traffic-manager-configure-geographic-routing-method.md).
- Dowiedz się, jak za[Menedżera ruchu ustawienia testu](traffic-manager-testing-settings.md).

<!--Image references-->
[1]: ./media/traffic-manager-performance-routing-method/traffic-manager-performance-routing-method.png