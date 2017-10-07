---
title: "tooConfigure aaaHow v1 środowiska usługi aplikacji"
description: "Konfigurowanie, zarządzanie i monitorowanie hello v1 środowiska usługi aplikacji"
services: app-service
documentationcenter: 
author: ccompy
manager: stefsch
editor: 
ms.assetid: b5a1da49-4cab-460d-b5d2-edd086ec32f4
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: ccompy
ms.openlocfilehash: f9539a72517276d8a1e340a408841561e8b8f56d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-an-app-service-environment-v1"></a>Konfigurowanie aplikacji usługi v1 środowiska

> [!NOTE]
> Ten artykuł dotyczy hello v1 środowiska usługi aplikacji.  Istnieje nowsza wersja hello środowiska usługi aplikacji jest łatwiejsze toouse, który jest uruchamiany na bardziej zaawansowanych infrastruktury. więcej informacji na temat nowej wersji hello rozpoczynać hello toolearn [toohello wprowadzenie środowiska usługi aplikacji](../app-service/app-service-environment/intro.md).
> 

## <a name="overview"></a>Omówienie
Na wysokim poziomie środowiska usługi aplikacji Azure składa się z kilku głównych składników:

* Usługa hostowana zasoby obliczeniowe, których są uruchomione w hello środowiska usługi aplikacji
* Magazyn
* Bazy danych
* Classic(V1) lub zasobów Azure Manager(V2) sieć wirtualną (VNet) 
* Podsieć o usługi hostowanej środowiska usługi aplikacji hello uruchomionej w nim

### <a name="compute-resources"></a>Zasoby obliczeniowe
Zasoby obliczeniowe hello są używane z pul zasobów cztery.  Każdego środowiska usługi aplikacji (ASE) ma zestaw punktów końcowych front i trzy pule procesów roboczych możliwe. Nie ma potrzeby toouse wszystkie pule procesów roboczych trzy — Jeśli chcesz, można użyć jednego lub dwóch.

hosty Hello w pulach zasobów hello (interfejsy i pracowników) nie są bezpośrednio dostępne tootenants. Nie można użyć toothem tooconnect protokołu RDP (Remote Desktop), zmienić ich inicjowania obsługi lub działać jako administrator na nich.

Można ustawić liczby puli zasobów i rozmiaru. W elemencie ASE masz cztery opcje rozmiaru, które są oznaczone jako P1 za pośrednictwem P4. Aby uzyskać więcej informacji o tych rozmiary i ich ceny, zobacz [cennik usługi aplikacji](../app-service/app-service-value-prop-what-is.md).
Zmiana liczby hello lub rozmiar nosi nazwę operacji skalowania.  Operacja skalowania tylko jedna może być w toku w czasie.

**Zakończenia przód**: hello front końce są punktów końcowych HTTP/HTTPS hello do pracy z aplikacjami, które są wstrzymane w Twojej ASE. Nie uruchamiaj obciążeń w hello interfejsy.

* ASE rozpoczyna się od dwóch P2s, który jest wystarczająca dla obciążeń i testowania i obciążeń produkcyjnych niskiego poziomu. Zdecydowanie zaleca się P3s dla tooheavy umiarkowane obciążeń produkcyjnych.
* W przypadku obciążeń produkcyjnych umiarkowane tooheavy zaleca się, czy masz co najmniej cztery tooensure P3s są wystarczające front kończy się uruchomione podczas zaplanowanej konserwacji. Działania zaplanowanej konserwacji zostanie wyświetlone w dół jeden fronton naraz. Zmniejsza to całkowita dostępna pojemność frontonu podczas działania obsługi.
* Interfejsy może potrwać tooan tooprovision godzinę. 
* Dalsze szczegóły skali, należy monitorować hello procent użycia procesora CPU i pamięci oraz metryki aktywnych żądań hello puli frontonu. Jeśli wartości procentowe procesora CPU lub pamięci hello powyżej 70 procent podczas uruchamiania P3s, dodać więcej front kończy się. Limit too15, 000 too20 000 żądań na frontonu oblicza średnią hello wartość aktywnych żądań, należy również dodać więcej front kończy się. Witaj ogólnym celem jest tookeep procesora CPU i procent pamięci poniżej 70% i aktywnych żądań uśrednianie limit toobelow 15 000 żądań na frontonu, gdy używasz P3s.  

**Pracownicy**: hello pracownicy są, gdy uruchamiane aplikacje. Skalowanie w górę planów usługi aplikacji, którymi używa się pracowników hello skojarzone puli procesów roboczych.

* Nie można dodać natychmiast pracowników. Może zajmowały tooan tooprovision godzinę.
* Skalowanie hello rozmiar dla każdej puli zasobów obliczeniowych potrwa < 1 godzina na domenę aktualizacji. W elemencie ASE jest 20 domen aktualizacji. W przypadku zmiany skali hello obliczeń rozmiar puli procesów roboczych z 10 wystąpień może potrwać too10 toocomplete godzin.
* Zmiana rozmiaru hello hello zasoby obliczeniowe, które są używane w puli procesów roboczych spowoduje zimnych startów aplikacji hello, które działają w tej puli procesów roboczych.

Najszybszą metodą Hello toochange hello obliczeniowe rozmiar zasobu puli procesów roboczych, który nie działa dla wszystkich aplikacji, jest:

* Skalowanie w dół hello ilość too2 pracowników.  Minimalna skali Hello w dół w portalu hello rozmiar wynosi 2. Potrwa kilka minut toodeallocate swoich wystąpień. 
* Wybierz nowy rozmiar obliczeń hello i liczba wystąpień. W tym miejscu zajmuje on too2 toocomplete godzin.

Jeśli aplikacje wymagają większy rozmiar zasobów obliczeniowych, możesz nie może korzystać z poprzedniej wskazówki hello. Zamiast zmieniania rozmiaru hello hello procesu roboczego puli, która obsługuje te aplikacje, można wypełnić innej puli procesów roboczych z pracowników hello żądany rozmiar i przenieść je przez toothat puli aplikacji.

* Utwórz dodatkowe wystąpienia hello hello potrzebne obliczeniowe rozmiar w innej puli procesów roboczych. Zajmuje to tooan toocomplete godzinę.
* Ponownie przypisać obsługujące hello aplikacje, które muszą większy rozmiar puli procesów roboczych toohello nowo skonfigurowane planów usługi aplikacji. Jest to szybkie operacji, które powinny zająć mniej niż minutę toocomplete.  
* Jeśli nie musisz już tych nieużywane wystąpienia skali hello pierwszej puli procesów roboczych. Ta operacja trwa kilka minut toocomplete.

**Skalowanie automatyczne**: jeden hello narzędzi, które mogą pomóc Ci toomanage użycia zasobów obliczeniowych jest automatycznie. Umożliwia skalowanie automatyczne dla frontonu lub pule procesów roboczych. Możesz wykonywanie czynności takich jak zwiększenie swoich wystąpień dowolnego typu puli w rano hello i jej zmniejszenia w wieczorem hello. Lub może dodać wystąpienia podczas hello liczbę procesów roboczych, które są dostępne w puli procesów roboczych spadnie poniżej określonego progu.

Jeśli zasady automatycznego skalowania tooset wokół metryki puli zasobów obliczeniowych, a następnie zachować w czasie hello zdanie udostępniania tego wymaga. Aby uzyskać więcej informacji na temat Skalowanie automatyczne środowiska usługi App Service, zobacz [sposób skalowania automatycznego tooconfigure w środowisku usługi aplikacji][ASEAutoscale].

### <a name="storage"></a>Magazyn
Każdy ASE skonfigurowano 500 GB miejsca do magazynowania. Ten obszar jest używany przez wszystkie aplikacje hello hello ASE. To miejsce do magazynowania jest częścią hello ASE i obecnie nie może być wyłączone toouse miejsca do magazynowania. Podczas wprowadzania korekt tooyour sieci wirtualnej routingu lub zabezpieczeń, należy toostill Zezwalaj tooAzure dostępu do magazynu — lub hello ASE nie może działać.

### <a name="database"></a>Database (Baza danych)
bazy danych Hello przechowuje informacje hello, definiujący hello środowiska, a także hello szczegóły dotyczące aplikacji hello, które są uruchomione w nim. Zbyt jest częścią hello przechowywać Azure subskrypcji. Nie jest coś czy masz toomanipulate bezpośredniego możliwości. Podczas wprowadzania korekt tooyour sieci wirtualnej routingu lub zabezpieczeń, należy toostill Zezwalaj na dostęp tooSQL Azure--lub hello ASE nie może działać.

### <a name="network"></a>Sieć
Hello sieci wirtualnej, który jest używany z Twojej ASE może być jedną utworzonego podczas tworzenia hello ASE lub jedną, który zgłosił wcześniejsze. Po utworzeniu podsieci hello podczas tworzenia ASE wymusi toobe hello ASE w hello tej samej grupie zasobów co sieć wirtualna hello. Grupa zasobów hello używany przez Twoje toobe ASE inne niż w sieci wirtualnej, należy następnie należy toocreate Twojego ASE przy użyciu szablonu usługi resource manager.

Istnieją pewne ograniczenia dotyczące hello sieć wirtualna, która jest używana do ASE:

* sieć wirtualna Hello musi być regionalną sieć wirtualną.
* Musi toobe podsieci z co najmniej 8 adresów wdrożonym hello ASE.
* Podsieć po toohost używane ASE hello zakres adresów podsieci hello nie można zmienić. Z tego powodu zaleca się, że tej podsieci hello zawiera co najmniej 64 adresy tooaccommodate przyszłego rozwoju ASE.
* Może istnieć nic w podsieci hello, ale hello ASE.

W przeciwieństwie do usługi hostowanej hello zawierający hello ASE, hello [sieci wirtualnej] [ virtualnetwork] i podsieci są pod kontrolą użytkownika.  Można administrować sieci wirtualnej za pomocą hello wirtualnych sieci interfejsu użytkownika lub środowiska PowerShell.  ASE można wdrożyć w klasyczny lub Menedżera zasobów w sieci wirtualnej.  Hello portal i środowiska interfejsu API są nieco inne między Classic i sieci wirtualnych Menedżera zasobów, ale hello ASE środowisko jest hello takie same.

Witaj sieci wirtualnej, która jest używana toohost ASE można użyć albo prywatnych adresów RFC1918 IP lub może używać publicznych adresów IP.  Jeśli chcesz toouse zakres IP, który nie pasuje do żadnego RFC1918 (10.0.0.0/8 172.16.0.0/12, 192.168.0.0/16), a następnie należy toocreate Twojej sieci wirtualnej i podsieci toobe używany przez Twoje ASE wcześniejsze tworzenie ASE.

Ponieważ ta funkcja wprowadza hello Azure App Service w sieci wirtualnej, oznacza to, że Twoje aplikacje, które znajdują się w sieci ASE można teraz uzyskiwać dostęp do zasobów, które są dostępne za pośrednictwem programu ExpressRoute lub wirtualnych sieci prywatnych (VPN) lokacja lokacja bezpośrednio. aplikacje Hello, znajdujące się w ramach środowiska usługi aplikacji nie wymagają dodatkowych sieci funkcje tooaccess zasoby dostępne toohello sieci wirtualnej obsługujący środowiska usługi aplikacji. Oznacza to, że nie jest wymagane toouse tooresources tooget integracji sieci Wirtualnej lub połączeń hybrydowych w lub tooyour połączenia wirtualnej sieci. Można nadal używać jednej z tych funkcji, chociaż tooaccess zasobów w sieci, które nie są połączone sieci wirtualnej tooyour łącze.

Na przykład można użyć toointegrate integracji sieci Wirtualnej z siecią wirtualną, która jest w ramach subskrypcji, ale nie ma podłączonych toohello sieci wirtualnej z ASE znajduje się w. Nadal można połączeń hybrydowych tooaccess zasobów, które znajdują się w innych sieciach, podobnie jak zwykle.  

Jeśli masz sieci wirtualnej skonfigurowaną ExpressRoute sieci VPN, należy zwrócić uwagę niektórych hello potrzeb routingu, które ma ASE. Istnieją pewne konfiguracje trasy zdefiniowane przez użytkownika (przez), które są niezgodne z ASE. Aby uzyskać więcej informacji o uruchamianiu ASE w sieci wirtualnej z usługi ExpressRoute, zobacz [uruchamianie środowiska usługi aplikacji w sieci wirtualnej z ExpressRoute][ExpressRoute].

#### <a name="securing-inbound-traffic"></a>Zabezpieczanie ruchu przychodzącego
Istnieją dwie podstawowe metody toocontrol ASE tooyour ruchu przychodzącego.  Można użyć toocontrol Groups(NSGs) zabezpieczeń sieci IP, jakie adresy mogą uzyskiwać dostęp do Twojego ASE, zgodnie z opisem w tym miejscu [jak toocontrol ruchu przychodzącego ruchu sieciowego w środowisku usługi aplikacji](app-service-app-service-environment-control-inbound-traffic.md) i obciążenia wewnętrznego można również skonfigurować Twoje ASE Balancer(ILB).  Te funkcje można również ze sobą Chcąc toorestrict dostępu za pomocą grup NSG tooyour ILB ASE.

Po utworzeniu ASE utworzy adresu VIP w sieci wirtualnej.  Istnieją dwa typy adresów VIP, wewnętrznych i zewnętrznych.  Po utworzeniu ASE z zewnętrznego adresu VIP aplikacji w Twojej ASE zostaną dostępny za pośrednictwem adresu IP routingu internetowego. Po wybraniu wewnętrzne Twojej ASE zostaną skonfigurowane ILB i nie będzie bezpośrednio dostępny internet.  ASE ILB nadal wymaga zewnętrznego adresu VIP, ale jest używana tylko dla platformy Azure, zarządzanie i obsługę dostępu.  

Podczas tworzenia ILB ASE Podaj hello poddomeny używane przez hello ILB ASE i będzie miał toomanage własne DNS w domenie podrzędnej hello, które określisz.  Ponieważ wartość nazwy poddomeny hello należy również toomanage hello certyfikatu używanego na potrzeby dostępu protokołu HTTPS.  Po ASE tworzenia, które monitowany tooprovide hello certyfikatu.  Przeczytaj toolearn więcej informacji na temat tworzenia i używania ASE ILB [przy użyciu wewnętrznego modułu równoważenia obciążenia z środowiska usługi aplikacji][ILBASE]. 

## <a name="portal"></a>Portal
Można zarządzać i monitorować za pomocą hello interfejsu użytkownika w portalu Azure hello środowiska usługi aplikacji. Jeśli masz ASE, to prawdopodobnie toosee hello symbol usługi aplikacji na Twoje paska bocznego. Ten symbol jest używany toorepresent środowiska usługi App Service w portalu Azure hello:

![Symbol środowiska usługi aplikacji][1]

tooopen hello interfejsu użytkownika, który zawiera listę wszystkich środowisk usługi aplikacji, możesz użyć ikony hello lub wybierz hello cudzysłów ostrokątny (">" symbol) u dołu hello tooselect paska bocznego hello środowiska usługi App Service. Wybranie jednego z wymienionych ASEs hello, otwórz hello interfejsu użytkownika, który jest używany toomonitor i nim zarządzać.

![Interfejs umożliwiający monitorowanie i zarządzanie środowiskiem usługi aplikacji][2]

Ten pierwszy blok zawiera niektóre właściwości sieci ASE wraz z wykresu metryki dla każdej puli zasobów. Niektóre właściwości hello, które przedstawiono w hello **Essentials** bloku są również hiperłącza, które spowoduje to otwarcie bloku hello, który jest skojarzony z nim. Na przykład można wybrać hello **sieci wirtualnej** tooopen nazwa zapasowej hello interfejsu użytkownika skojarzonego z hello sieci wirtualnej z ASE działa w. **Planów usługi App Service** i **aplikacji** Otwórz każdy bloków, których te elementów, które znajdują się w sieci ASE.  

### <a name="monitoring"></a>Monitorowanie
Wykresy Hello pozwalają toosee różne metryki wydajności w każdej puli zasobów. Witaj puli frontonu można monitorować hello średnie wykorzystanie Procesora i pamięci. Pule procesów roboczych można monitorować ilość hello jest używany, a ilość hello, która jest dostępna.

Użyj wielu usługi aplikacji, jakie można wprowadzać planów hello pracowników w puli procesów roboczych. Witaj obciążenia nie zostały rozprowadzone hello sam sposób jak w przypadku serwerów frontonu hello, tak hello użycia Procesora i pamięci nie udostępniają sposób hello przydatnych informacji. Jest większe znaczenie tootrack liczbę pracowników, które zostały użyte i są dostępne — zwłaszcza, jeśli zarządzasz tego systemu dla innych toouse.  

Umożliwia także wszystkie metryki hello można śledzić w tooset wykresy hello alerty. Konfigurowanie alertów w tym miejscu się, że działa hello takie same jak w innych miejscach w usłudze App Service. Można ustawić alert przy każdej hello **alerty** interfejsu użytkownika należą do lub z przechodzenia do dowolnego metryki interfejsu użytkownika i wybierając szczegółów **dodać Alert**.

![Metryki interfejsu użytkownika][3]

Witaj metryk, które zostały omówione wystarczy są hello metryki środowiska usługi aplikacji. Dostępne są także metryki, które są dostępne pod adresem hello poziom planu usługi aplikacji. Jest to, gdzie monitorowanie procesora CPU i pamięci sprawia, że wiele znaczeniu.

W elemencie ASE powitalne planów usługi App Service są dedykowane planów usługi aplikacji. Oznacza to, że hello tylko aplikacje, które są uruchomione na powitania hostów przydzielone toothat planu usługi aplikacji są aplikacji hello w tym planie usługi aplikacji. Szczegóły toosee na swój plan usługi aplikacji wyświetlić swój plan usługi aplikacji z dowolnego z listy hello hello ASE interfejsu użytkownika lub z **planów usługi App Service Przeglądaj** (które wyświetla listę wszystkich z nich).   

### <a name="settings"></a>Ustawienia
W bloku hello ASE jest **ustawienia** sekcja, która zawiera kilka ważnych funkcji:

**Ustawienia** > **właściwości**: hello **ustawienia** automatycznie zostanie otwarty blok po uruchomieniu z bloku ASE. Na powitania górna jest **właściwości**. Liczba elementów w tym miejscu, które są nadmiarowe toowhat w **Essentials**, ale jest to bardzo przydatne **wirtualnego adresu IP**, jak również **wychodzących adresów IP**.

![Blok ustawień i właściwości][4]

**Ustawienia** > **adresów IP**: po utworzeniu aplikacji IP Secure Sockets Layer (SSL) w Twojej ASE należy adresów IP protokołu SSL. W kolejności tooobtain jedną z ASE musi adresów IP protokołu SSL, które jest właścicielem które mogą być przydzielone. Po utworzeniu ASE ma jeden adres IP SSL do tego celu, ale można dodać więcej. Brak opłat dla dodatkowych SSL z adresu IP, adresy, jak pokazano w [cennik usługi aplikacji] [ AppServicePricing] (w sekcji hello na połączenia SSL). Cena dodatkowe Hello jest hello cen SSL z adresu IP.

**Ustawienia** > **Front End puli** / **pule procesów roboczych**: każdego z tych blokach puli zasobów oferuje hello możliwości toosee informacje tylko w tej puli zasobów , oprócz tooproviding steruje skali toofully tej puli zasobów.  

Witaj bloku podstawowego dla każdej puli zasobów zawiera wykres z metryki dla tej puli zasobów. Podobnie jak w przypadku wykresów hello z bloku ASE hello, można przejdź do wykresu hello i Konfigurowanie alertów, zgodnie z potrzebami. Ustawianie alertu z bloku ASE hello puli zasobów dla określonych hello samo, jak to zrobić z hello puli zasobów. Z puli procesów roboczych hello **ustawienia** bloku masz hello tooall dostępu do aplikacji lub planów usługi App Service, które działają w tej puli procesów roboczych.

![Proces roboczy puli ustawienia interfejsu użytkownika][5]

### <a name="portal-scale-capabilities"></a>Możliwości skalowania portalu
Istnieją trzy operacje skalowania:

* Zmiana hello liczba adresów IP w hello ASE, które są dostępne do użycia protokołu SSL z adresu IP.
* Zmiana rozmiaru hello hello obliczeń zasobu, który jest używany w puli zasobów.
* Zmiana liczby hello zasoby obliczeniowe, które są używane w puli zasobów, ręcznie lub za pośrednictwem Skalowanie automatyczne.

W portalu hello istnieją trzy sposoby toocontrol liczby serwerów znajdujących się w sieci pule zasobów:

* Operację skalowania za pomocą hello głównego bloku ASE u góry hello. Możesz wprowadzić wielu skali zmiany konfiguracji toohello frontonu i pule procesów roboczych. Są one wszystkich stosowane jako jedna operacja.
* Operację skalowania ręczne z puli zasobów poszczególnych hello **skali** bloku, która znajduje się w **ustawienia**.
* Skalowanie automatyczne, który został skonfigurowany z puli zasobów poszczególnych hello **skali** bloku.

Operacja skalowania hello toouse w bloku ASE hello, przeciągnij hello suwaka toohello ilość i Zapisz. Ten interfejs obsługuje również zmieniania rozmiaru hello.  

![Skala interfejsu użytkownika][6]

toouse możliwości ręcznego i automatycznego skalowania hello w puli zasobów dla określonych zbyt Przejdź**ustawienia** > **Front End puli** / **pule procesów roboczych** jako odpowiednie. Następnie otwarcie hello puli, które mają toochange. Przejdź za**ustawienia** > **Skaluj w poziomie** lub **ustawienia** > **Skaluj w górę**. Witaj **Skaluj w poziomie** bloku umożliwia toocontrol ilości wystąpieniu. **Skaluj w górę** pozwala toocontrol rozmiaru zasobu.  

![Ustawienia skalowania interfejsu użytkownika][7]

## <a name="fault-tolerance-considerations"></a>Zagadnienia dotyczące odporności na uszkodzenia
Można skonfigurować środowisko usługi aplikacji toouse too55 zasobów obliczeniowych całkowita. Tych 55 zasoby obliczeniowe tylko 50 może być używane toohost obciążeń. Witaj przyczyną tego błędu jest podwójny. Brak co najmniej 2 zasoby obliczeniowe frontonu.  Który pozostawia się too53 toosupport hello puli procesów roboczych alokacji. W kolejności tooprovide odporność na uszkodzenia należy toohave zasobu dodatkowe zasoby obliczeniowe przydzielonego zgodnie z toohello następujące reguły:

* Każdego procesu roboczego puli wymaga co najmniej 1 zasobów dodatkowe zasoby obliczeniowe, który nie jest dostępny toobe przypisane obciążenia.
* Gdy hello ilość zasobów obliczeniowych w puli procesów roboczych przekracza określoną wartość, inne zasoby obliczeniowe jest wymagany dla odporność na uszkodzenia. To nie jest hello hello puli frontonu.

W każdej puli pojedynczego procesu roboczego wymagania dotyczące odporności na uszkodzenia hello są dla danej wartości x zasoby przydzielone tooa puli procesów roboczych:

* Jeśli X to od 2 do 20, hello ilość zasoby obliczeniowe można używać, których można użyć w przypadku obciążeń jest X-1.
* Jeśli X to od 21 do 40, hello ilość zasoby obliczeniowe można używać, których można użyć w przypadku obciążeń jest X-2.
* Jeśli X jest między 41 i 53, hello ilość zasoby obliczeniowe można używać, których można użyć w przypadku obciążeń jest X-3.

Witaj minimalnego miejsca zajmowanego ma 2 serwerów frontonu i 2 procesy robocze.  Hello powyżej następnie instrukcje Oto kilka przykładów tooclarify:  

* Jeśli masz 30 pracowników w jednej puli 28 z nich może być używane toohost obciążeń.
* Jeśli masz 2 procesy robocze w jednej puli 1 może być używane toohost obciążeń.
* Jeśli masz 20 pracowników w jednej puli 19 może być używane toohost obciążeń.  
* Jeśli masz 21 pracowników w jednej puli nadal tylko 19 mogą być używane toohost obciążeń.  

aspekt odporności na uszkodzenia Hello jest ważne, ale należy tookeep go na uwadze podczas skalowania niektórych progi. Jeśli chcesz tooadd większej pojemności z 20 wystąpienia, a następnie przejdź too22 lub nowszej ponieważ 21 nie dodaje żadnych większej pojemności. Witaj, który dotyczy mają powyżej 40, gdzie hello kolejny numer, który dodaje pojemności jest 42.  

## <a name="deleting-an-app-service-environment"></a>Usuwanie środowiska usługi aplikacji
Jeśli chcesz toodelete środowiska usługi aplikacji, po prostu użyj hello **usunąć** akcji u góry bloku środowiska usługi aplikacji hello hello. Gdy to zrobisz, będziesz tooenter zostanie wyświetlony monit o nazwę hello tooconfirm Twojego środowiska usługi aplikacji, czy na pewno chcesz toodo to. Należy pamiętać, usunięcie środowiska usługi aplikacji powoduje usunięcie całej zawartości o hello znajdujące się w nim również.  

![Usuwanie środowiska usługi aplikacji interfejsu użytkownika][9]  

## <a name="getting-started"></a>Wprowadzenie
tooget wprowadzenie do środowiska usługi App Service, zobacz [jak toocreate środowiska usługi aplikacji](app-service-web-how-to-create-an-app-service-environment.md).

Aby uzyskać więcej informacji na temat hello platformy Azure App Service, zobacz [usłudze Azure App Service](../app-service/app-service-value-prop-what-is.md).

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!--Image references-->
[1]: ./media/app-service-web-configure-an-app-service-environment/ase-icon.png
[2]: ./media/app-service-web-configure-an-app-service-environment/aseconfig-aseblade.png
[3]: ./media/app-service-web-configure-an-app-service-environment/aseconfig-poolchart.png
[4]: ./media/app-service-web-configure-an-app-service-environment/aseconfig-properties.png
[5]: ./media/app-service-web-configure-an-app-service-environment/aseconfig-poolblade.png
[6]: ./media/app-service-web-configure-an-app-service-environment/aseconfig-scalecommand.png
[7]: ./media/app-service-web-configure-an-app-service-environment/aseconfig-poolscale.png
[8]: ./media/app-service-web-configure-an-app-service-environment/aseconfig-pricingtiers.png
[9]: ./media/app-service-web-configure-an-app-service-environment/aseconfig-deletease.png

<!--Links-->
[WhatisASE]: http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-intro/
[Appserviceplans]: http://azure.microsoft.com/documentation/articles/azure-web-sites-web-hosting-plans-in-depth-overview/
[HowtoCreateASE]: http://azure.microsoft.com/documentation/articles/app-service-web-how-to-create-an-app-service-environment/
[HowtoScale]: http://azure.microsoft.com/documentation/articles/app-service-web-scale-a-web-app-in-an-app-service-environment/
[ControlInbound]: http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-control-inbound-traffic/
[virtualnetwork]: https://azure.microsoft.com/documentation/articles/virtual-networks-faq/
[AppServicePricing]: http://azure.microsoft.com/pricing/details/app-service/
[AzureAppService]: http://azure.microsoft.com/documentation/articles/app-service-value-prop-what-is/
[ASEAutoscale]: http://azure.microsoft.com/documentation/articles/app-service-environment-auto-scale/
[ExpressRoute]: http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-network-configuration-expressroute/
[ILBASE]: http://azure.microsoft.com/documentation/articles/app-service-environment-with-internal-load-balancer/
