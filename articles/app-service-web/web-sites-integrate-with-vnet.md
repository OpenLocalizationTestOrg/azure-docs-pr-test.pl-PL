---
title: "aaaIntegrate aplikację z sieci wirtualnej platformy Azure"
description: "Pokazano, jak tooconnect aplikacji w usłudze Azure App Service tooa nowej lub istniejącej sieci wirtualnej platformy Azure"
services: app-service
documentationcenter: 
author: ccompy
manager: erikre
editor: cephalin
ms.assetid: 90bc6ec6-133d-4d87-a867-fcf77da75f5a
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/23/2017
ms.author: ccompy
ms.openlocfilehash: a93c504481400245b02220b541a008a7c874d10a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-your-app-with-an-azure-virtual-network"></a>Integracja aplikacji z sieci wirtualnej platformy Azure
Ten dokument zawiera opis funkcji integracji sieci wirtualnej hello w usłudze Azure App Service i przedstawia sposób tooset go z aplikacji w [usłudze Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714). Jeśli znasz sieci wirtualnych Azure (sieci wirtualne), jest możliwość, która pozwala tooplace przez wiele zasobów platformy Azure w sieci routeable internet nie możesz kontrolować dostęp do. Sieci te można następnie tooyour połączonych sieciach lokalnych przy użyciu różnych technologii sieci VPN. więcej informacji o sieciach wirtualnych platformy Azure, toolearn zaczynają tutaj informacje hello: [omówienie sieci wirtualnych Azure][VNETOverview]. 

Witaj w usłudze Azure App Service ma dwie formy. 

1. Witaj wielodostępne systemów, które obsługują pełnego zakresu hello planów cenowych
2. Witaj środowiska usługi aplikacji (ASE) premium funkcja wdraża do sieci wirtualnej. 

Ten dokument jest przesyłany przez integrację sieci wirtualnej i nie środowiska usługi aplikacji. Jeśli chcesz, dodatkowe informacje o funkcji hello ASE toolearn, zaczynać się tutaj informacje hello: [wprowadzenie środowiska usługi aplikacji][ASEintro].

Integracji sieci wirtualnej umożliwia tooresources dostępu do aplikacji sieci web w sieci wirtualnej, ale nie powoduje przyznania dostępu prywatnego tooyour sieci web aplikacji z hello sieci wirtualnej. Dostęp do witryny prywatnej odwołuje się toomaking swojej aplikacji, które są dostępne tylko z sieci prywatnej takich jak z wewnątrz sieci wirtualnej platformy Azure. Dostęp do witryny prywatny jest dostępny tylko dla ASE skonfigurowane z wewnętrznego obciążenia równoważenia (ILB). Aby uzyskać więcej informacji na temat używania ASE ILB, zaczynać się tutaj artykułu hello: [tworzenie i używanie ASE ILB][ILBASE]. 

Typowy scenariusz, w której można zastosować integrację sieci wirtualnej jest umożliwienie dostępu z bazy danych tooa aplikacji sieci web lub usługi sieci web uruchomiony na maszynie wirtualnej w sieci wirtualnej platformy Azure. Dzięki integracji sieci wirtualnej nie ma potrzeby tooexpose publiczny punkt końcowy dla aplikacji na maszynie Wirtualnej, ale zamiast tego użyć hello z systemem innym niż internet rutowalne adresy prywatne. 

Funkcja integracji z sieciami wirtualnymi Hello:

* wymaga Standard, Premium lub izolowany cenową planu 
* działa z klasycznym lub Menedżera zasobów w sieci wirtualnej 
* obsługuje TCP i UDP
* współpracuje z aplikacjami sieci Web, mobilnych i interfejsu API
* umożliwia aplikacji tooconnect tooonly 1 sieci wirtualnej w czasie
* Włącza się toofive toobe sieci wirtualnych zintegrowany z planu usługi App Service 
* Umożliwia hello tej samej sieci wirtualnej toobe używany przez wiele aplikacji w planie usługi aplikacji
* obsługuje 99,9% umowy SLA dla powodu toohello SLA na powitania bramy sieci wirtualnej

Istnieje kilka kwestii, które integracji sieci wirtualnej nie obsługuje łącznie:

* zainstalowanie dysku
* Funkcja integracji usługi AD 
* NetBios
* dostęp do witryny prywatnej

### <a name="getting-started"></a>Wprowadzenie
Poniżej przedstawiono niektóre tookeep rzeczy pamiętać przed połączeniem sieci wirtualnych tooa aplikacji sieci web:

* Integracja z sieciami wirtualnymi działa tylko w przypadku aplikacji w **standardowe**, **Premium**, lub **izolowany** cenową planu. Włącz funkcję hello, a następnie skalować tooan Twojego planu usługi aplikacji, nieobsługiwany cenową planu aplikacji utratę ich toohello połączenia używają sieci wirtualnych. 
* Jeśli sieci wirtualnej docelowy już istnieje, musi on mieć włączone z bramą routingu dynamicznego, aby można było tooan połączonych aplikacji VPN punkt lokacja. Jeśli brama jest skonfigurowana z routingiem statycznym, nie można włączyć punkt lokacja wirtualnej sieci prywatnej (VPN).
* Witaj sieć wirtualna musi być w hello tej samej subskrypcji co Twoje Plan(ASP) usługi aplikacji. 
* aplikacji Hello, które integrują się z sieci wirtualnej Użyj hello DNS, który jest określony dla tej sieci wirtualnej.
* Domyślnie aplikacje całkującej tylko kierować ruchem w sieci wirtualnej oparte na trasach hello, które są zdefiniowane w sieci wirtualnej. 

## <a name="enabling-vnet-integration"></a>Włączanie integracji sieci wirtualnej
Ten dokument koncentruje się przede wszystkim na potrzeby integracji sieci wirtualnej przy użyciu hello portalu Azure. tooenable integracji sieci wirtualnej z aplikacji przy użyciu programu PowerShell, postępuj zgodnie ze wskazówkami hello w tym miejscu: [połączyć sieci wirtualnej tooyour aplikacji przy użyciu programu PowerShell][IntPowershell].

Masz tooconnect opcji hello aplikacji tooa nowej lub istniejącej sieci wirtualnej. Jeśli tworzysz nową sieć jako część integracją, następnie dodatkowo hello toojust tworzenie sieci wirtualnej, dynamiczne bramy routingu jest wstępnie skonfigurowana dla Ciebie i włączona jest sieć VPN tooSite punktu. 

> [!NOTE]
> Konfigurowanie nowego integracji sieci wirtualnej może potrwać kilka minut. 
> 
> 

tooenable integracji sieci wirtualnej, Otwórz aplikację ustawienia, a następnie wybierz sieć. Witaj interfejsu użytkownika, który zostaje otwarty oferuje trzy opcje sieci. Ten przewodnik jest tylko do integracji sieci wirtualnej jednak połączeń hybrydowych i środowiska usługi App Service zostały omówione w dalszej części tego dokumentu. 

Jeśli aplikacja nie jest w hello poprawne cenową planu, hello interfejsu użytkownika umożliwia tooscale Twojego tooa planu wyższy cenową planu wybranych przez użytkownika.

![][1]

### <a name="enabling-vnet-integration-with-a-pre-existing-vnet"></a>Włączanie integracji sieci wirtualnej z istniejącej sieci wirtualnej
Witaj interfejsu użytkownika integracji sieci wirtualnej umożliwia tooselect z listy Twojej sieci wirtualnych. Hello klasyczne sieci wirtualne wskazuje, że są takie wyrazem hello "Klasyczny" w nawiasach następnej toohello nazwy sieci wirtualnej. Witaj lista jest sortowana tak, aby hello sieci wirtualnych Menedżera zasobów jest wyświetlana na początku listy. Witaj obraz poniżej możesz zawiera można wybrać tylko jedną sieć wirtualną. Istnieje wiele przyczyn, że sieć wirtualną można wyszarzone w tym:

* Witaj sieci wirtualnej jest w innej subskrypcji, czy Twoje konto ma dostęp do
* Witaj sieci wirtualnej nie ma punktu tooSite włączone
* Witaj sieci wirtualnej nie ma dynamicznych bramy routingu

![][2]

Integracja tooenable po prostu kliknij hello mają toointegrate z sieci wirtualnej. Po wybraniu hello sieci wirtualnej aplikacji jest automatycznie uruchamiany ponownie hello zmiany tootake efektu. 

##### <a name="enable-point-toosite-in-a-classic-vnet"></a>Włącz tooSite punktu w klasycznej sieci wirtualnej
Jeśli nie ma bramy sieci wirtualnej, ani ma tooSite punktu, następnie należy tooset się pierwsza. toodo to klasycznej sieci wirtualnej, przejdź toohello [portalu Azure] [ AzurePortal] i wyświetlić listę hello Networks(classic) wirtualnego. W tym miejscu kliknij sieć hello toointegrate z i kliknij na powitania big pole w obszarze Essentials o nazwie połączeń sieci VPN. W tym miejscu można utworzyć sieć VPN toosite punktu i nawet została ona utworzyć bramę. Po przejściu hello punktu toosite doświadczenie w tworzeniu bramy jest około 30 minut, zanim będzie gotowy. 

![][8]

##### <a name="enabling-point-toosite-in-a-resource-manager-vnet"></a>Włączanie tooSite punkt w sieci wirtualnej Resource Manager
tooconfigure Menedżera zasobów sieci wirtualnej z bramą i tooSite punktu służy albo PowerShell zgodnie z opisem w tym miejscu [konfigurowania lokacji punktu połączenia tooa sieć wirtualną przy użyciu programu PowerShell] [ V2VNETP2S] lub użyj hello portalu Azure zgodnie z opisem w tym miejscu [Skonfiguruj punkt do lokacji połączenie tooa sieci wirtualnej przy użyciu hello portalu Azure][V2VNETPortal]. Witaj tooperform interfejsu użytkownika tej możliwości nie jest jeszcze dostępna. Należy pamiętać, wymagają certyfikatów toocreate hello tooSite punktu konfiguracji. To jest automatycznie konfigurowany podczas łączenia z aplikacji sieci Web toohello sieci wirtualnej. 

### <a name="creating-a-pre-configured-vnet"></a>Tworzenie wstępnie skonfigurowane sieci wirtualnej
Jeśli chcesz toocreate nowej sieci wirtualnej jest skonfigurowany przy użyciu bramy i punkt-lokacja, następnie hello sieci interfejsu użytkownika usługi aplikacji ma toodo możliwości hello ale tylko dla sieci wirtualnej Menedżera zasobów. Jeśli chcesz toocreate klasycznej sieci wirtualnej z bramą i punkt-lokacja, następnie należy toodo to ręcznie za pomocą interfejsu użytkownika sieci hello. 

toocreate Menedżera zasobów sieci wirtualnej za pośrednictwem hello interfejsu użytkownika integracji sieci wirtualnej, po prostu wybierz **Utwórz nową sieć wirtualną** i podaj:

* Nazwa sieci wirtualnej
* Blok adresów sieci wirtualnej
* Nazwa podsieci
* Blok adresów podsieci
* Blok adresów bramy
* Blok adresów punkt lokacja

Jeśli chcesz tooany tooconnect tej sieci wirtualnej innych sieci, następnie należy unikać pobrania przestrzeń adresów IP, który pokrywa się z tych sieci. 

> [!NOTE]
> Tworzenie sieci wirtualnej usługi Resource Manager przy użyciu bramy trwa około 30 minut i aktualnie nie obsługują hello sieci wirtualnej z aplikacją. Po utworzeniu sieci wirtualnej z bramą hello muszą toocome wstecz tooyour aplikacji integracji sieci wirtualnej w interfejsie użytkownika i wybierz nowej sieci.
> 
> 

![][3]

Sieci wirtualne Azure zwykle są tworzone w sieci prywatnej adresów. Przez domyślny hello integracji sieci wirtualnej funkcji rozsyła cały ruch kierowany do tych zakresów adresów IP w sieci wirtualnej. Witaj zakresów prywatnych adresów IP są:

* -to jest hello sam jako 10.0.0.0 - 10.0.0.0/8 10.255.255.255
* -to jest hello takie same jak 172.16.0.0 - 172.16.0.0/12 172.31.255.255 
* 192.168.0.0/16 - to jest hello takie same jak 192.168.0.0 - 192.168.255.255

Witaj przestrzeni adresowej sieci wirtualnej musi toobe określone w notacji CIDR. Jeśli nie znasz w notacji CIDR, to metoda określania bloki adresów przy użyciu adresu IP i liczba całkowita, która reprezentuje hello maska sieci. Jako podręczny wykaz należy wziąć pod uwagę że 10.1.0.0/24 byłyby 256 adresów i 10.1.0.0/25 byłoby 128 adresów. Adres IPv4 z /32 będą tylko 1 adres. 

Jeśli ustawisz tutaj hello informacji o serwerze DNS, który jest ustawić sieci wirtualnej. Po utworzeniu sieci wirtualnej można edytować te informacje z możliwości użytkowników hello sieci wirtualnej. Jeśli zmienisz hello DNS hello sieci wirtualnej, należy tooperform operacji synchronizacji sieci.

Podczas tworzenia klasycznych sieci wirtualnej przy użyciu hello interfejsu użytkownika integracji sieci wirtualnej, tworzy sieć wirtualną w hello tej samej grupie zasobów co aplikacja. 

## <a name="how-hello-system-works"></a>Jak działa hello system
W obszarze obejmuje hello ta funkcja kompilacje ponad tooconnect technologii sieci VPN typu punkt-lokacja tooyour Twojej aplikacji sieci wirtualnej. Aplikacje w usłudze Azure App Service mają architektury wielodostępnej systemu, co wyklucza Inicjowanie obsługi aplikacji bezpośrednio w sieci wirtualnej, co jest wykonywane z maszynami wirtualnymi. Tworzenie na technologii punkt lokacja jest ograniczona sieci dostępu toojust hello hostowania maszyn wirtualnych aplikacji hello. Dostępu do sieci toohello dalsze jest ograniczone na tych hostach aplikacji, dzięki czemu aplikacje mogą uzyskiwać dostęp tylko do hello sieci należy skonfigurować je tooaccess. 

![][4]

Jeśli nie skonfigurowano serwera DNS z sieci wirtualnej, aplikacji należy toouse zasobu tooreach adresów IP w hello sieci wirtualnej. Podczas korzystania z adresów IP, należy pamiętać, że hello najważniejszych korzyści z tej funkcji jest możliwość toouse hello prywatnych adresów w sieci prywatnej. Jeśli ustawisz aplikację w górę toouse publicznych adresów IP dla jednej z maszyn wirtualnych, nie za pomocą funkcji integracji z sieciami wirtualnymi hello i komunikują się za pośrednictwem hello internet.

## <a name="managing-hello-vnet-integrations"></a>Zarządzanie hello integracji sieci wirtualnej
Witaj tooconnect możliwości i Odłącz tooa sieci wirtualnej jest na poziomie aplikacji. Operacje, które mogą wpłynąć na powitania integracji sieci wirtualnej wielu aplikacjom są na poziomie ASP. W hello interfejsu użytkownika, który jest wyświetlany na poziomie aplikacji hello można uzyskać szczegółowe informacje na Twojej sieci wirtualnej. Większość tych samych informacji jest także pokazany na powitania ASP poziomu powitalne. 

![][5]

Na stronie Stan funkcji sieci hello widać, jeśli aplikacja jest tooyour połączonych sieci wirtualnej. Jeśli bramy sieci wirtualnej działa niezależnie od przyczyny, następnie to będzie wyświetlane jako połączony nie. 

informacje Hello się, że masz teraz tooyou dostępne w aplikacji hello z poziomu interfejsu użytkownika integracji sieci wirtualnej jest sama hello jako hello szczegółowych informacji uzyskasz od hello ASP. Poniżej przedstawiono te elementy:

* Nazwa sieci wirtualnej — to łącze powoduje otwarcie hello sieci wirtualnej platformy Azure, interfejsu użytkownika
* Lokalizacja — odzwierciedla hello lokalizacji sieci wirtualnej. Jest możliwe toointegrate z sieci wirtualnej w innej lokalizacji.
* Stan certyfikatu — Brak połączenia sieci VPN hello toosecure certyfikaty używane między aplikacją hello i hello sieci wirtualnej. Ta właściwość odzwierciedla tooensure testu, są one zsynchronizowane.
* Stan bramy — z bram należy dół jakiegoś powodu następnie aplikacji nie może uzyskać dostęp do zasobów hello sieci wirtualnej. 
* Sieci wirtualnej przestrzeni adresowej — jest to hello przestrzeń adresową sieci wirtualnej. 
* Przestrzeń adresowa tooSite punktu — jest to hello toosite punktu przestrzeń adresową sieci wirtualnej. Aplikacja zawiera komunikatu jako pochodzących z jednego z hello adresów IP w tej przestrzeni adresowej. 
* Przestrzeń adresowa toosite lokacji — można użyć witryny tooSite VPN tooconnect tooyour Twojej sieci wirtualnej lokalnych zasobów lub tooother sieci wirtualnej. Powinien mieć, skonfigurowanego, a następnie zakresów IP hello zdefiniowane z tutaj pokazano połączenia sieci VPN.
* Serwery DNS — Jeśli masz serwerom DNS skonfigurowanym z sieci wirtualnej, a następnie są one wyświetlane tutaj.
* Adresy IP kierowane toohello sieci wirtualnej — ma listę adresów IP sieci wirtualnej ma routingu zdefiniowane dla, a tu wyświetlone tych adresów. 

Hello jedyną operacją, które można wykonać w widoku aplikacji hello integracją sieci wirtualnej jest toodisconnect aplikacji z hello jest podłączony do sieci wirtualnej. toodo to po prostu kliknij przycisk Odłącz u góry hello. Ta akcja nie powoduje zmiany sieci wirtualnej. Hello sieci wirtualnej i jej konfiguracja, łącznie z bram hello pozostaje niezmieniona. Następnie chcesz toodelete sieci wirtualnej, należy najpierw toofirst delete hello zasobów w nim tym hello bram. 

Witaj widoku Plan usługi App Service ma liczbę dodatkowych operacji. Jest on również dostępny inaczej niż z aplikacji hello. hello tooreach interfejsu użytkownika sieci w ASP po prostu otworzyć ASP interfejsu użytkownika i przewiń w dół. Brak elementu interfejsu użytkownika o nazwie stan funkcji sieci. Udostępnia pewne szczegóły pomocnicza wokół integracją sieci wirtualnej. Kliknięcie tego interfejsu użytkownika zostanie otwarty hello interfejsu użytkownika stanu funkcji sieci. Po kliknięciu na "kliknij tutaj toomanage", hello interfejsu użytkownika, który zawiera listę powitalne otwiera integracji sieci wirtualnej w tym ASP.

![][6]

lokalizację Hello hello ASP jest dobrym tooremember podczas przeglądania hello lokalizacje hello jest integrowany z sieciami wirtualnymi. Witaj sieci wirtualnej jest w innej lokalizacji są znacznie bardziej prawdopodobne toosee opóźnień. 

Hello zintegrowany z sieci wirtualnych jest przypomnienie na liczbę sieci wirtualnych się, że aplikacje są zintegrowane z usługą, w tym ASP i ile można mieć. 

toosee dodać szczegóły w każdej sieci wirtualnej, wystarczy kliknąć hello w sieci wirtualnej. Ponadto toohello szczegółowe informacje, które zostały wcześniej zapisany, również widać listę aplikacji hello w tym ASP, które korzystają z tej sieci wirtualnej. 

W odniesieniu tooactions dostępne są dwie podstawowe akcje. Hello jest najpierw hello możliwości tooadd tras, którzy sterują ruchu wychodzącego aplikacji w sieci wirtualnej. Witaj drugiej akcji jest hello możliwości toosync certyfikaty i informacje o sieci.

![][7]

**Routing** jak wspomniano wcześniej hello tras, które są zdefiniowane w sieci wirtualnej są przeznaczenia kierowanie ruchu w sieci wirtualnej z aplikacji. Brak niektórych zastosowaniach chociaż klienci miejscu toosend dodatkowy ruch wychodzący z aplikacji do hello sieciami wirtualnymi i ich ta możliwość jest dostępne. Co się stanie, toohello ruch będzie toohow hello odbiorców konfiguruje ich sieci wirtualnej. 

**Certyfikaty** hello stanu certyfikatu odzwierciedla kontrola wykonywana przez hello toovalidate usługi aplikacji nadal dobrej czy certyfikatom hello jest używany dla hello połączenia sieci VPN. Po włączeniu integracji sieci wirtualnej, jeśli jest to hello pierwszy toothat integracji sieci wirtualnej z dowolnej aplikacji, w tym ASP występuje wymagane wymiany certyfikatów tooensure hello zabezpieczeń hello połączenia. Wraz z certyfikatami hello uzyskujemy hello konfiguracji serwera DNS, tras i innymi podobne opisujące hello sieci.
Zmiana tych certyfikatów lub informacje o sieci należy tooclick "Synchronizacji sieci". **Uwaga**: po kliknięciu "Synchronizacji sieci", a następnie spowodować chwilowa niedostępność w łączności między aplikacji i sieci wirtualnej. Gdy aplikacja nie zostanie ponownie uruchomiony, hello utraty połączenia może spowodować funkcji toonot lokacji poprawnie. 

## <a name="accessing-on-premises-resources"></a>Uzyskiwanie dostępu do zasobów lokalnych
Czy jeśli sieci wirtualnej jest podłączona tooyour lokalną sieć z lokacji tooSite sieci VPN aplikacji może mieć dostęp do zasobów lokalnych tooyour z aplikacji, a następnie jedną z zalet funkcji integracji z sieciami wirtualnymi hello hello jest. Dla tego toowork chociaż może być konieczne tooupdate bramy sieci VPN lokalnej z hello trasy dla zakresowi adresów IP tooSite punktu. Gdy hello lokacji tooSite sieci VPN najpierw, a następnie tooconfigure używane skrypty hello należy skonfigurować tras w tym serwera VPN tooSite punktu. Jeśli dodasz hello tooSite punktu sieci VPN po utworzeniu tooSite Twojego witryny sieci VPN, należy tooupdate hello tras ręcznie. Szczegółowe informacje na jak toodo, który zmienia się wraz z bramy i nie są opisane w tym miejscu. 

> [!NOTE]
> Funkcja integracji z sieciami wirtualnymi Hello nie obsługują aplikacji sieć wirtualną, która ma bramę usługi ExpressRoute. Nawet jeśli skonfigurowano hello bramę usługi ExpressRoute w [tryb współistnienie] [ VPNERCoex] hello integracji sieci wirtualnej nie działa. Jeśli potrzebujesz tooaccess zasobów za pośrednictwem połączenia ExpressRoute, a następnie można użyć [środowiska usługi aplikacji][ASE], które uruchamia się w sieci wirtualnej.
> 
> 

## <a name="pricing-details"></a>Szczegóły cennika
Istnieje kilka wszystkie szczegóły, które należy zwrócić uwagę podczas korzystania z funkcji integracji z sieciami wirtualnymi hello cennik. Istnieją 3 opłat powiązanych toohello używanie tej funkcji:

* Wymagania dotyczące warstwy cenowej ASP
* Koszty transferu danych
* Koszty bramy sieci VPN.

Dla twojej aplikacji toobe stanie toouse tej funkcji, potrzebują toobe w normie lub Plan usługi aplikacji — warstwa Premium. Można wyświetlić więcej szczegółów tych kosztów tutaj: [App Service — ceny][ASPricing]. 

Ze względu na sposób toohello tooSite punktu obsługi sieci VPN, zawsze mają opłat dla danych wychodzących za pośrednictwem połączenia integracji sieci wirtualnej, nawet jeśli hello sieci wirtualnej jest w hello sam centrum danych. toosee co to są tych opłat, zapoznaj się z informacjami w tym miejscu: [szczegóły cennika transferu danych][DataPricing]. 

ostatni element Hello jest koszt hello hello bramy sieci wirtualnej. Jeśli nie potrzebujesz hello bramy do czegoś innego, takich jak witryny tooSite sieci VPN, dokonujesz płatności dla funkcji integracji sieci wirtualnej hello toosupport bram. Brak szczegółów kosztów tych tutaj: [cennik bramy sieci VPN][VNETPricing]. 

## <a name="troubleshooting"></a>Rozwiązywanie problemów
Gdy funkcja hello jest łatwe tooset się, nie oznacza to, że czynności będą wolne problem. Powinien wystąpić problemy z dostępem do żądanego punktu końcowego są niektóre narzędzia można użyć tootest łączności z hello aplikacji konsoli. Istnieją dwa środowiska konsoli, których można używać. Jest jednym z konsoli Kudu hello i hello innych jest konsoli hello, którego można używać w hello portalu Azure. tooget toohello Kudu konsoli z aplikacji przejdź tooTools -> Kudu. To jest hello takie same jak będzie zbyt [sitename]. scm.azurewebsites.net. Po tym otwiera Przejdź po prostu toohello debugowania konsoli kartę tooget toohello konsoli platformy Azure portalu hostowanej następnie z aplikacji przejdź tooTools -> konsoli. 

#### <a name="tools"></a>Narzędzia
polecenie ping narzędzi Hello, nslookup i tracert nie będzie działać za pośrednictwem konsoli hello powodu toosecurity ograniczenia. Brak void hello toofill zostały dwóch oddzielnych narzędzi dodane. Narzędzie o nazwie nameresolver.exe dodaliśmy w kolejności tootest DNS funkcji. Składnia Hello jest następująca:

    nameresolver.exe hostname [optional: DNS Server]

Można użyć nazwy nameresolver toocheck hello hostów, która zależy od aplikacji. W ten sposób można przetestować niczego źle skonfigurowany systemie DNS lub prawdopodobnie nie masz serwera DNS tooyour dostępu.

Narzędzie dalej Hello pozwala tootest TCP łączności tooa hosta i portu kombinacji. To narzędzie jest nazywany tcpping.exe i składnia hello jest:

    tcpping.exe hostname [optional: port]

Narzędzie tcpping Hello informuje, jeżeli można osiągnąć konkretnego hosta i portu. Tylko może sygnalizować Powodzenie jeśli: Brak aplikacji nasłuchującej na powitania kombinacja hosta i portu i Brak dostępu do sieci z aplikacji toohello określonego hosta i portu.

#### <a name="debugging-access-toovnet-hosted-resources"></a>Debugowanie tooVNet dostępu do hostowanych zasobów
Istnieje kilka rzeczy, które mogą uniemożliwić aplikacji osiągnięcia konkretnego hosta i portu. W większości przypadków hello jest jednym z trzech zdarzeń:

* **Znajduje się zapora w hello sposób** Jeśli masz zapory w sposób hello nastąpi trafienie hello limitu czasu TCP. W takim przypadku to 21 sekund. Użyj hello tcpping narzędzie tootest łączności. Limity czasu protokołu TCP można powodu rzeczy toomany poza zaporą, ale uruchomić. 
* **Usługa DNS nie jest dostępny** limit czasu DNS hello jest trzech sekund na serwerze DNS. Mając dwa serwery DNS, limit czasu hello jest 6 sekund. Użyj nameresolver toosee, jeśli serwer DNS działa. Należy pamiętać, że nie można używać polecenia nslookup, ponieważ nie używa hello DNS skonfigurowano sieci wirtualnej.
* **Nieprawidłowy zakres adresów IP P2S** zakres adresów IP toosite punktu hello musi toobe w prywatnej zakresów IP hello RFC 1918 (10.0.0.0-10.255.255.255 / 172.16.0.0-172.31.255.255 / 192.168.0.0-192.168.255.255). Jeśli zakres hello używa adresów IP poza który, czynności nie będzie działać. 

Jeśli problemu nie można znaleźć odpowiedzi tych elementów, Szukaj pierwszego dla hello prostych operacji, takich jak: 

* Witaj bramy są wyświetlane jako znajdujące się w portalu hello?
* Certyfikaty są wyświetlane jako znajdujące się w synchronizacji?
* Każdy zmieniły się konfigurację sieci hello nie robiąc "Synchronizacji sieci" w ASP hello, których dotyczy problem? 

Jeśli brama nie działa, następnie włączenie go kopii zapasowych. Jeśli certyfikaty nie są zsynchronizowane, przejdź do widoku ASP toohello Twojego integracji sieci wirtualnej i kliknij przycisk "Synchronizacji sieci". Jeśli podejrzewasz, że zostało wprowadzone zmiany konfiguracji sieci wirtualnej tooyour i nie był synchronizacji będzie z programu ASP następnie przejdź do widoku ASP toohello Twojego integracji sieci wirtualnej i kliknij "Synchronizacji sieci" Just przypomnieniem, powoduje to chwilowa niedostępność z połączeniem sieci wirtualnej i aplikacji . 

Jeśli wszystko jest poprawnie, należy toodig w bardziej bit:

* Są dostępne wszystkie inne aplikacje przy użyciu integracji sieci wirtualnej tooreach zasobów w hello tej samej sieci wirtualnej? 
* Można go toohello aplikacji konsoli i użyj tcpping tooreach żadnych innych zasobów w sieci wirtualnej? 

Jeśli powyższe hello jest spełniony jeden z, następnie Integracja sieci wirtualnej jest poprawnie i hello problem jest gdzie indziej. Jest to, gdzie staje się toobe więcej wyzwanie, ponieważ nie istnieje żadne toosee mówiąc w uproszczeniu, dlaczego nie można osiągnąć hosta: port.. Hello przyczyny są między innymi:

* masz zaporę na hoście uniemożliwia port aplikacji toohello dostępu z zakresowi adresów IP toosite punktu. Często przekroczenie granic podsieci wymaga dostępu publicznego.
* dostęp do hosta docelowego nie działa
* Aplikacja nie działa
* konieczne było hello niewłaściwy adres IP lub nazwa hosta
* aplikacja nasłuchuje na innym porcie niż oczekiwano. Można to sprawdzić, przechodząc na tym hoście i za pomocą "netstat - aon" z hello wiersz polecenia. Przedstawia identyfikator nasłuchuje na porcie co procesu. 
* grupy zabezpieczeń sieci są skonfigurowane w taki sposób, aby zapobiec dostępu tooyour aplikacji hosta i portu z zakresowi adresów IP toosite punktu

Należy pamiętać, że nie znasz jakie IP z zakresu tooSite punktu IP, które Twoja aplikacja będzie używać w związku z czym należy tooallow dostęp z hello cały zakres. 

Debugowania dodatkowe kroki obejmują:

* Zaloguj się na inną maszynę Wirtualną w Twojej sieci wirtualnej, a następnie spróbuj tooreach zasobów hosta: port stamtąd. Istnieją pewne narzędzia polecenia ping protokołu TCP w tym celu można użyć, lub nawet służy telnet, jeśli muszą być. Witaj w tym miejscu ma toodetermine tylko w przypadku łączności z tej maszyny Wirtualnej. 
* Wywołaj okno aplikacji na inną maszynę Wirtualną i testowanie dostępu toothat hosta i portu z konsoli hello z aplikacji

#### <a name="on-premises-resources"></a>Zasobów lokalnych ####
Jeśli aplikację można nawiązać połączenia z zasobami lokalnymi, hello najpierw należy sprawdzić, jest, jeżeli można osiągnąć zasobu w sieci wirtualnej. Jeśli to zrobić, spróbuj tooreach hello lokalnej aplikacji z maszyny Wirtualnej w hello sieci wirtualnej. Można użyć narzędzia telnet lub narzędzie ping protokołu TCP. Jeśli maszyny Wirtualnej nie może uzyskać dostęp do zasobu lokalnego, upewnij się, że połączenie sieci VPN tooSite lokacji działa. Jeżeli działa, sprawdź hello same elementy wymienione wcześniej oraz konfiguracji bramy lokalne powitania i stan. 

Teraz Jeśli hostowana w sieci wirtualnej maszyny Wirtualnej można osiągnąć systemu lokalnego, ale aplikacji nie Przyczyna hello jest prawdopodobnie jednym z następujących hello:

* nie skonfigurowano trasy z toosite punktu zakresy IP bramy sieci lokalnej
* grupy zabezpieczeń sieci blokuje dostęp do punktu tooSite zakres IP
* lokalnej zapory blokuje ruch z zakresowi adresów IP tooSite punktu
* masz użytkownika Route(UDR) zdefiniowana w sieci uniemożliwia ruchu na podstawie tooSite punktu nawiązywania połączenia z siecią lokalną

## <a name="hybrid-connections-and-app-service-environments"></a>Połączenia hybrydowe i środowiska usługi aplikacji
Istnieją trzy funkcje, które umożliwiają dostęp do zasobów hostowanych tooVNet. Są to:

* Integracja sieci wirtualnej
* Połączenia hybrydowe
* Środowiska usługi App Service

Połączenia hybrydowe wymaga tooinstall agenta przekazywania o nazwie hello Manager(HCM) połączeń hybrydowych w sieci. Witaj HCM musi tooAzure stanie tooconnect toobe, a także tooyour aplikacji. To rozwiązanie jest szczególnie dużą z sieci zdalnej, takich jak sieci lokalnej lub nawet innej chmury hostowanej sieci, ponieważ nie wymaga dostępnym punkcie końcowym internet. działa tylko w systemie Windows Hello HCM i może zawierać maksymalnie wystąpień toofive tooprovide wysokiej dostępności. Mimo że połączeń hybrydowych TCP obsługuje tylko i każdego punktu końcowego HC ma toomatch tooa określonego hosta: port. kombinację. 

funkcja środowiska usługi aplikacji Hello pozwala toorun wystąpienia hello Azure App Service w sieci wirtualnej. Umożliwia to aplikacji dostęp do zasobów w sieci wirtualnej bez żadnych dodatkowych czynności. Niektóre hello inne korzyści środowiska usługi aplikacji są służy pracowników na podstawie Dv2 się too14 GB pamięci RAM. Innego korzyścią jest to, że można skalować hello systemu toomeet potrzeb. W odróżnieniu od środowiskach wielodostępnych hello strona ASP w przypadku wystąpienia too20 ograniczona w elemencie ASE można zwiększać too100 ASP wystąpień. Jedną z hello rzeczy, o których możesz uzyskać z ASE, który nie dzięki integracji sieci wirtualnej jest, czy środowisko usługi aplikacji może współpracować z sieci VPN usługi ExpressRoute. 

Wprawdzie jest korzystanie z niektórych przypadków nakładają się na siebie, żaden z tych funkcji można zastąpić żadnego hello innym. Mamy do czynienia jakie toouse funkcja wiązana tooyour potrzeb. Na przykład:

* Deweloperzy i po prostu toorun witryny na platformie Azure i mają dostęp bazy danych hello na stacji roboczej hello w obszarze biurku, to najprostszy toouse operacją hello jest połączeń hybrydowych było możliwe. 
* Jeśli jesteś dużej organizacji, która chce tooput dużej liczby właściwości sieci web w chmurze publicznej hello i zarządzanie nimi we własnej sieci, ma toogo z hello środowiska usługi aplikacji. 
* Jeśli masz wiele aplikacji usługi hostowanej aplikacji i po prostu chcesz tooaccess zasobów w sieci wirtualnej, wówczas hello toogo sposób integracji sieci wirtualnej. 

Poza przypadkami użycia hello, istnieją pewne prostota aspektach. Jeśli w Twojej sieci wirtualnej jest już połączony tooyour lokalnej sieci przy użyciu integracji sieci wirtualnej lub środowiska usługi aplikacji to prosty sposób tooconsume zasobów lokalnych. Na powitania drugiej strony, jeśli w Twojej sieci wirtualnej nie jest połączona sieć lokalną tooyour, a następnie jest dużo więcej tooset ogólnych zapasowych toosite witryny sieć VPN z sieci wirtualnej w porównaniu z instalowaniem hello HCM. 

Ponad hello różnice funkcjonalne, są również cennik różnice. funkcja środowiska usługi aplikacji Hello to usługa Premium oferty ale hello oferuje większość możliwości konfiguracji sieci poza tooother funkcje. Integracja sieci wirtualnej może być używany z Standard lub Premium ASP i idealne w przypadku bezpieczne korzystanie z zasobów w sieci wirtualnej z hello wielodostępne usługi aplikacji. Połączeń hybrydowych obecnie zależy od usług BizTalk — wersja konta, które ma cennik poziomy uruchamianych wolnego i następnie pobrać progresywnie droższe na podstawie hello kwoty potrzebne. Napotka tooworking wiele sieci jednak, nie ma żadnych innych funkcji połączeń hybrydowych było możliwe, która może umożliwić tooaccess zasobów w różnych sieciach dobrze ponad 100. 

<!--Image references-->
[1]: ./media/web-sites-integrate-with-vnet/vnetint-upgradeplan.png
[2]: ./media/web-sites-integrate-with-vnet/vnetint-existingvnet.png
[3]: ./media/web-sites-integrate-with-vnet/vnetint-createvnet.png
[4]: ./media/web-sites-integrate-with-vnet/vnetint-howitworks.png
[5]: ./media/web-sites-integrate-with-vnet/vnetint-appmanage.png
[6]: ./media/web-sites-integrate-with-vnet/vnetint-aspmanage.png
[7]: ./media/web-sites-integrate-with-vnet/vnetint-aspmanagedetail.png
[8]: ./media/web-sites-integrate-with-vnet/vnetint-vnetp2s.png

<!--Links-->
[VNETOverview]: http://azure.microsoft.com/documentation/articles/virtual-networks-overview/ 
[AzurePortal]: http://portal.azure.com/
[ASPricing]: http://azure.microsoft.com/pricing/details/app-service/
[VNETPricing]: http://azure.microsoft.com/pricing/details/vpn-gateway/
[DataPricing]: http://azure.microsoft.com/pricing/details/data-transfers/
[V2VNETP2S]: http://azure.microsoft.com/documentation/articles/vpn-gateway-howto-point-to-site-rm-ps/
[IntPowershell]: http://azure.microsoft.com/documentation/articles/app-service-vnet-integration-powershell/
[ASEintro]: http://docs.microsoft.com/azure/app-service/app-service-environment/intro
[ILBASE]: http://docs.microsoft.com/azure/app-service/app-service-environment/create-ilb-ase
[V2VNETPortal]: https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-howto-point-to-site-resource-manager-portal
[VPNERCoex]: http://docs.microsoft.com/en-us/azure/expressroute/expressroute-howto-coexist-resource-manager
[ASE]: http://docs.microsoft.com/azure/app-service/app-service-environment/intro
