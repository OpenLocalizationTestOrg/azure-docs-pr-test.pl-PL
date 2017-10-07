---
title: "Ustawienia usługi Azure Traffic Manager aaaVerify | Dokumentacja firmy Microsoft"
description: "Ten artykuł pomoże Ci Sprawdź ustawienia Menedżera ruchu"
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
editor: 
ms.assetid: 2180b640-596e-4fb2-be59-23a38d606d12
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/16/2017
ms.author: kumud
ms.openlocfilehash: c670be6cf55e140c7ab63d5d526de08e14774d2a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="verify-traffic-manager-settings"></a>Sprawdź ustawienia Menedżera ruchu

tootest ustawienia Menedżera ruchu należy toohave wielu klientów w różnych lokalizacjach, z których można uruchomić testy. Następnie przełącz hello punktów końcowych w Twoim profilu Menedżera ruchu w dół pojedynczo.

* Ustaw wartość DNS TTL hello niski Propaguj zmiany szybko (na przykład 30 sekund).
* Znać hello adresy IP usług w chmurze Azure i witryn sieci Web w profilu hello podczas testowania.
* Użyj narzędzia, które pozwalają rozwiązać adres IP tooan nazwy DNS i wyświetlenie tego adresu.

Podczas sprawdzania toosee, że nazwy DNS hello rozpoznać tooIP adresy punktów końcowych hello w Twoim profilu. nazwy Hello powinna być rozpoznawana w sposób zgodny z metody routingu ruchu hello zdefiniowane w hello profilu usługi Traffic Manager. Można użyć narzędzia hello, takie jak **nslookup** lub **dig** tooresolve nazwy DNS.

Witaj następujące przykłady pomocy można przetestować profilu Menedżera ruchu.

### <a name="check-traffic-manager-profile-using-nslookup-and-ipconfig-in-windows"></a>Sprawdź profil usługi Traffic Manager przy użyciu polecenia nslookup i ipconfig w systemie Windows

1. Uruchom polecenia lub w wierszu polecenia Windows PowerShell jako administrator.
2. Typ `ipconfig /flushdns` hello tooflush pamięci podręcznej programu rozpoznawania nazw DNS.
3. Wpisz polecenie `nslookup <your Traffic Manager domain name>`. Na przykład Witaj następujące polecenia kontroli hello nazwy domeny z prefiksem hello *myapp.contoso*

        nslookup myapp.contoso.trafficmanager.net

    Typowy wynik pokazuje hello następujących informacji:

    + Witaj nazwy DNS i adres IP jest serwer DNS hello dostępne tooresolve tej nazwy domeny usługi Traffic Manager.
    + Nazwa domeny usługi Traffic Manager Hello został wpisany w wierszu polecenia powitania po "nslookup" i domeny Menedżera ruchu hello toowhich adres IP hello jest rozpoznawana. Witaj drugiego adresu IP jest ważne toocheck jeden hello. Publiczny wirtualny adres IP (VIP) dla jednego z hello usługi w chmurze lub witryny sieci Web w hello profilu Menedżera ruchu, testowany powinien być zgodny.

## <a name="how-tootest-hello-failover-traffic-routing-method"></a>Jak metoda routingu ruchu tootest hello w tryb failover

1. Pozostaw wszystkie punkty końcowe w górę.
2. Za pomocą jednego klienta, żądanie rozpoznawania nazw DNS dla nazwy domeny firmy przy użyciu polecenia nslookup lub podobne narzędzia.
3. Upewnij się, że hello rozwiązane, czy adres IP odpowiada hello podstawowy punkt końcowy.
4. Przenieś w dół podstawowego punktu końcowego lub usuń hello monitorowania pliku tak, aby sądzi Menedżera ruchu, które aplikacji hello jest wyłączony.
5. Poczekaj, aż hello DNS Time-to-Live (TTL) hello profilu usługi Traffic Manager oraz kolejnych dwóch minut. Na przykład jeśli Twoje czas wygaśnięcia DNS to 300 sekund (5 minut), należy poczekać na siedem minut.
6. Flush że klienta pamięci podręcznej i żądania DNS rozpoznawanie nazw DNS za pomocą polecenia nslookup. W systemie Windows możesz opróżnić pamięć podręczną DNS przy użyciu hello ipconfig/flushdns polecenia.
7. Upewnij się, że hello rozpoznać adres IP zgodny dodatkowej punktu końcowego.
8. Powtórz kroki hello, z kolei wyłączania każdego punktu końcowego. Sprawdź, czy ten hello DNS zwraca hello adres IP następnego punktu końcowego hello hello listy. W przypadku wszystkich punktów końcowych w dół, należy uzyskać hello adres IP punktu końcowego podstawowego hello ponownie.

## <a name="how-tootest-hello-weighted-traffic-routing-method"></a>Jak tootest hello ważone metody routingu ruchu

1. Pozostaw wszystkie punkty końcowe w górę.
2. Za pomocą jednego klienta, żądanie rozpoznawania nazw DNS dla nazwy domeny firmy przy użyciu polecenia nslookup lub podobne narzędzia.
3. Upewnij się, że hello rozwiązane, czy adres IP jest zgodny z punktami końcowymi.
4. Opróżnienia pamięci podręcznej klienta DNS i powtórz kroki 2 i 3 dla każdego punktu końcowego. Powinny pojawić różne adresy IP zwrócona dla każdego z punktów końcowych.

## <a name="how-tootest-hello-performance-traffic-routing-method"></a>Jak metoda routingu ruchu tootest hello wydajności

tooeffectively test wydajności metody routingu ruchu, musi mieć klienci znajdujący się w różnych części hello world. Klientów można utworzyć w różnych regionach platformy Azure, które mogą być używane tootest usług. Jeśli masz globalnej sieci można zdalnie Zaloguj tooclients w innych częściach Witaj świecie i uruchamiania testów z tego miejsca.

Alternatywnie istnieją Zwolnij opartych na sieci web wyszukiwania DNS i szczegółowej dostępność usług. Nadaj hello rozpoznawania nazw DNS toocheck możliwości z różnych lokalizacji na całym świecie hello niektórych z tych narzędzi. Czy na "Wyszukiwania DNS" Wyszukiwanie przykłady. Usług innych firm, takich jak Gomez lub prelekcji mogą być używane tooconfirm profile są Dystrybucja ruchu zgodnie z oczekiwaniami.

## <a name="next-steps"></a>Następne kroki

* [O metodach routingu ruchu Menedżera ruchu](traffic-manager-routing-methods.md)
* [Zagadnienia dotyczące wydajności usługi Traffic Manager](traffic-manager-performance-considerations.md)
* [Rozwiązywanie problemów ze stanem obniżonej wydajności usługi Traffic Manager](traffic-manager-troubleshooting-degraded.md)
