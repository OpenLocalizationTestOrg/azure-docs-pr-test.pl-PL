---
title: "aaaAzure Traffic Manager — metody routingu ruchu | Dokumentacja firmy Microsoft"
description: "Ten artykuł pomaga zrozumieć metody routingu ruchu innego hello użyty przez Menedżera ruchu"
services: traffic-manager
documentationcenter: 
author: KumudD
manager: timlt
editor: 
ms.assetid: db1efbf6-6762-4c7a-ac99-675d4eeb54d0
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/13/2017
ms.author: kumud
ms.openlocfilehash: b3eeca63ab5f2b9cd4a3a6b6a8fd3e40059e32b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="traffic-manager-routing-methods"></a>Metody routingu w usłudze Traffic Manager

Azure Traffic Manager toodetermine metody routingu ruchu obsługuje czterech jak tooroute sieci toohello ruchu różnych punktów końcowych usługi. Menedżera ruchu stosuje hello routingu ruchu metody tooeach DNS kwerendę. Metoda routingu ruchu Hello Określa, które punkt końcowy zwrócił w odpowiedzi DNS hello.

Dostępne są cztery metody routingu ruchu w usłudze Traffic Manager:

* **[Priorytet](#priority):** wybierz **priorytet** po toouse podstawowego punktu końcowego dla całego ruchu, a następnie podaj kopii zapasowych w przypadku hello podstawowego lub kopii zapasowej punktów końcowych hello są niedostępne.
* **[Ważone](#weighted):** wybierz **ważone** zużycia toodistribute ruch między zbiorem punktów końcowych, albo równomiernie lub zgodnie z tooweights, który zdefiniowano.
* **[Wydajność](#performance):** wybierz **wydajności** gdy masz punktów końcowych w różnych lokalizacjach geograficznych i chcesz, aby użytkownicy końcowi toouse hello "najbliższy" punktu końcowego pod względem hello najniższe opóźnienia sieci.
* **[Geograficzne](#geographic):** wybierz **geograficzne** tak, aby użytkownicy są toospecific ukierunkowanej punktów końcowych (Azure, zewnętrzne lub zagnieżdżone) na podstawie których lokalizacji geograficznej pochodzi ich zapytanie DNS. Umożliwia to Menedżera ruchu klientów tooenable zastosowaniach wiedząc regionu geograficznego użytkownika oraz routing ich oparta na ważne. Przykładami zgodnych z danych suwerenności zleceń, lokalizacja środowiska użytkownika & zawartości i pomiar ruchu z różnych regionów.

Wszystkie profile Menedżera ruchu obejmują monitorowania kondycji punktu końcowego i punktu końcowego automatycznej pracy awaryjnej. Aby uzyskać więcej informacji, zobacz [monitorowanie punktu końcowego Menedżera ruchu](traffic-manager-monitoring.md). Jeden profil usługi Traffic Manager można użyć tylko jedna metoda routingu ruchu. W dowolnym momencie można wybrać metodę routingu ruchu innego profilu. Zmiany zostaną zastosowane w ciągu jednej minuty, a poniesienia bez przestojów. Metody routingu ruchu można łączyć, używając zagnieżdżonych profilów usługi Traffic Manager. Zagnieżdżanie umożliwia zaawansowane i elastyczne routingu ruchu konfiguracje, które potrzeb hello większych i złożonych aplikacji. Aby uzyskać więcej informacji, zobacz [zagnieżdżonych profilów usługi Traffic Manager](traffic-manager-nested-profiles.md).

## <a name = "priority"></a>Metody routingu ruchu o priorytecie

Często organizacja chce tooprovide niezawodności jego usług przez wdrożenie co najmniej jednej usługi tworzenia kopii zapasowych w przypadku, gdy ich podstawowa usługa przestanie działać. Metoda routingu ruchu 'Priority' Hello umożliwia Azure tooeasily klientów implementacji tego wzorca trybu failover.

![Menedżer ruchu Azure 'Priority' routingu ruchu — metoda][1]

Witaj profilu usługi Traffic Manager zawiera priorytetową listą punktów końcowych usługi. Domyślnie usługi Traffic Manager wysyła wszystkie ruchu toohello głównej (najwyższy priorytet) punktu końcowego. Jeśli hello podstawowy punkt końcowy nie jest dostępna, trasy menedżera ruchu hello ruchu toohello drugiego punktu końcowego. Jeśli oba hello podstawowych i pomocniczych punkty końcowe nie są dostępne, hello ruch przechodzi toohello innej itd. Dostępność punktu końcowego hello opiera się na stan hello skonfigurowane (włączona lub wyłączona) i hello monitorowania bieżących punktów końcowych.

### <a name="configuring-endpoints"></a>Konfigurowanie punktów końcowych

Usługi Azure Resource Manager można skonfigurować priorytet punktu końcowego hello jawnie za pomocą właściwości "priority" hello, dla każdego punktu końcowego. Ta właściwość jest wartość z zakresu od 1 do 1000. Niższe wartości reprezentują wyższy priorytet. Punkty końcowe nie mogą mieć wartości priorytetu. Ustawienie właściwości hello jest opcjonalna. W przypadku pominięcia będzie używana domyślna wartość priorytetu na podstawie kolejności punktu końcowego hello jest używany.

##<a name = "weighted"></a>Ważoną metody routingu ruchu
metody routingu ruchu "Ważone" Hello pozwala toodistribute ruch równomiernie lub toouse wagi wstępnie zdefiniowane.

![Azure Traffic Manager "Ważoną" routingu ruchu — metoda][2]

Witaj metody ważoną routingu ruchu przypisaniu punktu końcowego tooeach wag w konfiguracji profilu Menedżera ruchu hello. Waga Hello jest liczba całkowita od 1 too1000. Ten parametr jest opcjonalny. Pominięcie menedżerów ruchu korzysta z domyślną wagę "1".

Dla każdego zapytania DNS Odebrano Traffic Manager losowo wybiera dostępnego punktu końcowego. prawdopodobieństwo Hello wybrać punkt końcowy jest oparta na wag hello przypisane tooall dostępnych punktów końcowych. Przy użyciu hello sama waga we wszystkich wyników punktów końcowych w nawet Dystrybucja ruchu. Za pomocą wag wyższe lub niższe w określonych punktach końcowych sprawia, że te toobe punkty końcowe częściej lub rzadziej zwracany w odpowiedzi DNS hello.

Metoda Hello ważone umożliwia niektórych przydatne w scenariuszach:

* Uaktualnienie stopniowe aplikacji: przydzielić procent ruchu tooroute tooa nowy punkt końcowy, a następnie stopniowo zwiększać hello ruchu w czasie too100%.
* TooAzure migracji aplikacji: Tworzenie profilu z zarówno dla platformy Azure, jak i zewnętrznych punktów końcowych. Dostosuj hello wagę hello punkty końcowe tooprefer hello nowe punkty końcowe.
* Chmura poszerzająca dodatkowej pojemności: szybko rozwiń lokalnego wdrożenia w chmurze hello umieszczając za profilu usługi Traffic Manager. Jeśli potrzebujesz dodatkowej pojemności w chmurze hello można dodać lub włączyć więcej punktów końcowych i określić, jaka część ruchu przechodzi tooeach punktu końcowego.

Hello portal Azure Resource Manager obsługuje hello Konfigurowanie routingu ruchu ważoną.  Można skonfigurować wag używane wersje hello Menedżera zasobów Azure PowerShell, interfejsu wiersza polecenia i hello interfejsów API REST.

Jest ważne toounderstand czy odpowiedzi DNS jest buforowany przez klientów i przez serwery DNS cykliczne hello hello klientów za pomocą tooresolve nazwy DNS. To buforowanie może mieć wpływ na dystrybucje ważoną ruchu. W przypadku dużych hello liczba klientów i serwery DNS cykliczne Dystrybucja ruchu działa zgodnie z oczekiwaniami. Jednak w przypadku małych hello liczbę klientów lub serwerów DNS cykliczne buforowanie może znacznie pochylanie hello Dystrybucja ruchu.

Typowe przypadki użycia obejmują:

* Projektowanie i środowisk testowych
* Komunikacja aplikacji do aplikacji
* Aplikacje celem wąskie użytkownika — podstawowy, które używają wspólnej infrastruktury DNS cykliczne (na przykład pracownicy firmy łączących się za pośrednictwem serwera proxy)

Efekty buforowania te DNS to typowe tooall ruchem DNS routingu systemy, nie tylko usługi Azure Traffic Manager. W niektórych przypadkach jawnie wyczyszczenie pamięci podręcznej DNS hello może udostępnić obejście tego problemu. W innych przypadkach może być bardziej odpowiednie alternatywną metodę routingu ruchu.

## <a name = "performance"></a>Metody routingu ruchu wydajności

Wdrażanie punktów końcowych w co najmniej dwie lokalizacje w Witaj świecie może zwiększyć szybkość reakcji hello wiele aplikacji przez routingu ruchu toohello lokalizacji tooyou "najbliższy". metody routingu ruchu "Performance" Hello, obsługuje tę funkcję.

![Menedżer ruchu Azure "Performance" routingu ruchu — metoda][3]

punkt końcowy "najbliższy" Hello nie jest niekoniecznie najbliższego mierzony odległość geograficznej. Zamiast tego metody routingu ruchu "Performance" hello określa hello najbliższego punktu końcowego, mierząc opóźnienia sieci. Menedżer ruchu zapisuje tabeli opóźnienia Internet tootrack hello czasu Rundy między zakresów adresów IP i każdego centrum danych Azure.

Menedżer ruchu wyszukuje hello źródłowy adres IP żądania przychodzącego DNS hello w hello Internet opóźnienia tabeli. Menedżer ruchu wybiera dostępnego punktu końcowego w hello ma hello można uzyskać najmniejsze opóźnienia dla tego zakresu adresów IP, a następnie zwraca w odpowiedzi DNS hello tego punktu końcowego centrum danych Azure.

Zgodnie z objaśnieniem w [sposób działania usługi Traffic Manager](traffic-manager-overview.md#how-traffic-manager-works), Menedżera ruchu nie odbiera zapytania DNS bezpośrednio od klientów. Zamiast zapytania DNS pochodzą z usługi DNS cykliczne hello klientom Witaj czy toouse skonfigurowany. W związku z tym hello endpoint "najbliższy" hello toodetermine użyty adres IP nie jest adres IP powitania klienta, ale jest adres IP hello hello cykliczne DNS usługi. W praktyce ten adres IP jest dobrym serwera proxy dla powitania klienta.


Ruch Menedżer regularnie aktualizacje hello tooaccount Internet opóźnienia tabeli zmian w hello globalne internetowe i nowe regiony platformy Azure. Jednakże wydajność aplikacji w zależności od w czasie rzeczywistym wahania obciążenia między hello Internet. Routing ruchu wydajności nie monitoruje obciążenie danego punktu końcowego. Jednak jeśli punkt końcowy jest niedostępny, usługi Traffic Manager nie ma go w odpowiedzi na zapytania DNS.


Toonote punktów:

* Jeśli Twój profil zawiera wiele punktów końcowych w hello tego samego regionu Azure, a następnie Traffic Manager dystrybuuje ruch równomiernie między hello dostępnych punktów końcowych w tym regionie. Jeśli wolisz dystrybucji różnych ruchu w obrębie regionu, możesz użyć [zagnieżdżonych profilów usługi Traffic Manager](traffic-manager-nested-profiles.md).
* Włączenie wszystkich punktów końcowych w hello najbliższy region platformy Azure są obniżeniem, Traffic Manager przenosi punkty końcowe toohello ruchu hello dalej najbliższy region platformy Azure. Toodefine sekwencji preferowany tryb failover, należy użyć [zagnieżdżonych profilów usługi Traffic Manager](traffic-manager-nested-profiles.md).
* Jeśli używasz metody routingu ruchu wydajności hello z zewnętrznych punktów końcowych lub zagnieżdżone punktów końcowych, należy toospecify hello lokalizacji tych punktów końcowych. Wybierz najbliższą wdrożenia tooyour hello region platformy Azure. Te lokalizacje są wartości hello hello Internet opóźnienia tabeli.
* Algorytm Hello, który wybiera punkt końcowy hello jest deterministyczna. Powtarzany toohello skierowane do zapytania DNS z hello są tego samego klienta tego samego punktu końcowego. Zazwyczaj klienci używają serwerów DNS innej cykliczne podczas podróży. powitania klienta może być kierowany tooa innym punktem końcowym. Routing można również zostaną objęte toohello aktualizacji tabeli opóźnienia Internet. W związku z tym hello wydajności metody routingu ruchu nie gwarantuje, że klient jest zawsze kierowane toohello tego samego punktu końcowego.
* Po zmianie hello Internet opóźnienia tabeli można zauważyć, że niektórzy klienci są ukierunkowanej tooa innym punktem końcowym. Ta zmiana routingu jest dokładniejsze na podstawie bieżących danych opóźnienia. Te aktualizacje są istotne toomaintain hello dokładność wydajności-routingu ruchu jako powitalne Internet stale rozwoju środowisko.

## <a name = "geographic"></a>Geograficzne metody routingu ruchu

Profile Menedżera ruchu może być skonfigurowany toouse powitalne Geographic metody routingu, dzięki czemu użytkownicy są przekierowywane toospecific endpoints (Azure, zewnętrzne lub zagnieżdżone), na podstawie której lokalizacji geograficznej ich zapytanie DNS pochodzi z. Umożliwia to Menedżera ruchu klientów tooenable zastosowaniach wiedząc regionu geograficznego użytkownika oraz routing ich oparta na ważne. Przykładami zgodnych z danych suwerenności zleceń, lokalizacja środowiska użytkownika & zawartości i pomiar ruchu z różnych regionów.
Po skonfigurowaniu profilu geograficznego routingu każdego punktu końcowego skojarzone z wymagane przez profil toohave zestaw tooit regionów geograficznych przypisane. W następujących poziomów szczegółowości może być regionu geograficznego 
- World — dowolny region
- Regionalne grupowania — na przykład Afryka Bliski Wschód, Australia/pacyficzny itp. 
- Kraj/Region — na przykład Irlandii Peru, Hongkong SAR itp. 
- Województwo — na przykład Kalifornijskiej USA, Australia-Queensland, Kanada Alberta itp. (Uwaga: ten poziom szczegółowości jest obsługiwana tylko w przypadku stanów / prowincje w Australii, Kanady UK i USA).

Po przypisaniu punktu końcowego tooan region lub zestawie regionów, wszystkie żądania z tych regionów pobiera routingiem tylko punkt końcowy toothat. Menedżer ruchu używa adresu IP źródłowego hello hello DNS zapytania toodetermine hello regionu, w którym pyta użytkownika z — zazwyczaj jest to adres IP hello hello lokalny program rozpoznawania nazw DNS wykonywania zapytania hello w imieniu użytkownika hello.  

![Azure Traffic Manager "Geograficzne" routingu ruchu — metoda](./media/traffic-manager-routing-methods/geographic.png)

Menedżera ruchu odczytuje źródłowy adres IP hello hello zapytania DNS i decyduje o tym, które regionu geograficznego jest z. Następnie wygląda toosee w przypadku punktu końcowego, który ma tooit tego regionu geograficznego zamapowane. Tego odnośnika rozpoczyna się na najniższym poziomie szczegółowości hello (województwo gdzie jest obsługiwany, else na poziomie Kraj/Region hello) i przejdzie do końca hello się toohello najwyższego poziomu, który jest **World**. Pierwsze dopasowanie Hello ustalił, że przy użyciu tego przechodzenie jest oznaczony jako hello tooreturn punkt końcowy w odpowiedzi na zapytanie hello. Dopasowywanie za punkt końcowy typu zagnieżdżone w tym profilu podrzędnego punktu końcowego jest zwracany, oparty na jego metody routingu. Hello następujące punkty są odpowiednie toothis zachowanie:

- Region geograficzny mogą być mapowane tylko końcowego tooone w profilu Menedżera ruchu, gdy typ routingu hello jest geograficzne routingu. Dzięki temu routingu użytkowników jest deterministyczna, a mogą umożliwić scenariusze, które wymagają jednoznaczne granice geograficzne.
- Jeśli regionu użytkownika zawiera mapowania geograficznej w dwóch różnych punktów końcowych, Menedżer ruchu wybiera hello punktu końcowego z hello najniższy poziom szczegółowości i nie należy wziąć pod uwagę routingu żądań z tego regionu toohello innych punktów końcowych. Rozważmy na przykład typ profilu geograficznego routingu z dwoma punktami końcowymi - Punk końcowy 1 i Punk końcowy 2. Skonfigurowano Punk końcowy 1 skonfigurowano tooreceive ruch z Irlandii i Punk końcowy 2 tooreceive ruch z Europy. Jeśli żądanie pochodzi z Irlandii, zawsze jest kierowany tooEndpoint1.
- Ponieważ region mogą być mapowane tylko punkt końcowy tooone, Traffic Manager zwraca niezależnie od tego, czy punkt końcowy hello jest w dobrej kondycji lub nie.

    >[!IMPORTANT]
    >Zdecydowanie zaleca się, że klientów przy użyciu metody routingu geograficzne hello skojarzyć go z punktów hello zagnieżdżone typu końcowych, które ma profile podrzędnych zawierające co najmniej dwa punkty końcowe w ramach każdej.
- Jeśli znaleziono punktu końcowego i tego punktu końcowego jest hello **zatrzymane** stanu odpowiedzi NODATA zwraca Menedżera ruchu. W takim przypadku nie dalsze wyszukiwań następuje wyższego rzędu w hierarchii regionu geograficznego hello. To zachowanie mają też zastosowanie dla typów zagnieżdżonych punktu końcowego, gdy hello podrzędne profil jest hello **zatrzymane** lub **wyłączone** stanu.
- Jeśli punkt końcowy Wyświetla **wyłączone** stanu, nie będą uwzględniane w regionie hello zgodny proces. To zachowanie mają też zastosowanie dla typów zagnieżdżonych punktu końcowego, gdy punkt końcowy hello hello **wyłączone** stanu.
- Jeśli zapytanie pochodzi od regionu geograficznego, który nie ma mapowania w tym profilu, Traffic Manager zwraca odpowiedź NODATA. W związku z tym zdecydowanie zaleca się klienci powinni korzystać geograficzne routingu o jeden punkt końcowy, najlepszym rozwiązaniem typu zagnieżdżone z co najmniej dwa punkty końcowe w ramach profilu podrzędnych hello z regionu hello **World** przypisane tooit. Dzięki temu, że wszystkie adresy IP, które mapują tooa region są obsługiwane.

Zgodnie z objaśnieniem w [sposób działania usługi Traffic Manager](traffic-manager-how-traffic-manager-works.md), Menedżera ruchu nie odbiera zapytania DNS bezpośrednio od klientów. Zamiast zapytania DNS pochodzą z usługi DNS cykliczne hello klientom Witaj czy toouse skonfigurowany. W związku z tym hello IP adres używany toodetermine hello region nie jest hello adres IP klienta, ale jest adres IP hello hello cykliczne DNS usługi. W praktyce ten adres IP jest dobrym serwera proxy dla powitania klienta.


## <a name="next-steps"></a>Następne kroki

Dowiedz się, jak toodevelop wysokiej dostępności aplikacji przy użyciu [monitorowania punktu końcowego Menedżera ruchu](traffic-manager-monitoring.md)

Dowiedz się, jak za[Tworzenie profilu Menedżera ruchu](traffic-manager-create-profile.md)

<!--Image references-->
[1]: ./media/traffic-manager-routing-methods/priority.png
[2]: ./media/traffic-manager-routing-methods/weighted.png
[3]: ./media/traffic-manager-routing-methods/performance.png



