---
title: "aaaConnect tooOMS komputerów przy użyciu hello bramy OMS | Dokumentacja firmy Microsoft"
description: "Połącz komputery urządzeń zarządzanych OMS i monitorowania programu Operations Manager komputery z hello bramy OMS toosend danych toohello usługę, gdy nie mają dostępu do Internetu."
services: log-analytics
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: ae9a1623-d2ba-41d3-bd97-36e65d3ca119
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/20/2017
ms.author: magoedte
ms.openlocfilehash: 0cfa8f2fb66016e494f22c780e328be472b5fdee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-computers-without-internet-access-toooms-using-hello-oms-gateway"></a>Łączenie komputerów bez tooOMS dostęp do Internetu za pomocą hello bramy OMS

W tym dokumencie opisano, jak z zarządzanych OMS i System Center Operations Manager monitorowanych komputerów mogą wysyłać usługę toohello danych gdy nie mają dostępu do Internetu. Hello bramy OMS, czyli protokołu HTTP do przodu serwera proxy, który obsługuje tunelowania HTTP przy użyciu połączenia HTTP polecenia hello może zbierać dane i wysyłać je toohello usługę w ich imieniu.  

Witaj bramy OMS obsługuje:

* Hybrydowymi elementami roboczymi Runbook usługi Automatyzacja Azure  
* Komputery z systemem Windows z programu Microsoft Monitoring Agent hello bezpośrednio podłączone tooan obszarem roboczym pakietu OMS
* Komputery z systemem Linux z hello Agent pakietu OMS Linux bezpośrednio podłączone tooan obszarem roboczym pakietu OMS  
* System Center Operations Manager 2012 z dodatkiem SP1 z pakietem UR7, programu Operations Manager 2012 R2 z UR3 lub programu Operations Manager w grupie zarządzania 2016 zintegrowane z usługą OMS.  

Jeśli zasady zabezpieczeń IT nie zezwalaj na komputerach na Twojej toohello tooconnect sieci Internet, takie jak punkt urządzeń sprzedaży (POS) lub serwerach obsługujących usług IT, ale należy tooconnect toomanage tooOMS je i monitorować je, można skonfigurować toocommunicate bezpośrednio z konfiguracji tooreceive bramy OMS hello i przekazują dane w ich imieniu.  Jeśli te komputery są skonfigurowane przy użyciu toodirectly agent pakietu OMS hello połączyć z obszarem roboczym pakietu OMS tooan, wszystkie komputery zamiast tego będzie komunikować się z hello OMS bramy.  Hello bramy przesyła dane z tooOMS agentów hello bezpośrednio, nie zostaną przeanalizowane żadnego hello danych podczas przesyłania.

Gdy grupy zarządzania programu Operations Manager jest zintegrowany z usługą OMS, serwery zarządzania hello można toohello skonfigurowanych tooconnect informacje o konfiguracji tooreceive OMS bramy i wysyłania danych zebranych w zależności od rozwiązania hello, które aktywowano.  Agenci programu Operations Manager wysyłać niektóre dane, takie jak alerty programu Operations Manager, oceny konfiguracji, miejsce zajmowane przez wystąpienia i serwera zarządzania toohello danych wydajności. Inne dane dużych, takich jak dzienniki programu IIS, wydajności i zdarzeń zabezpieczeń są wysyłane bezpośrednio toohello OMS bramy.  Jeśli istnieje jeden lub więcej serwerów bramę programu Operations Manager wdrożony w strefa DMZ lub innych toomonitor sieci izolowanej niezaufanych systemów, nie mogą komunikować się z bramą OMS.  Serwery programu Operations Manager bramy można tylko tooa zarządzania serwera raportów.  Gdy grupa zarządzania programu Operations Manager jest skonfigurowany toocommunicate z hello OMS bramy, informacje o konfiguracji serwera proxy hello jest automatyczna dystrybucja tooevery komputer zarządzany przez agenta ilości danych toocollect skonfigurowanych dla analizy dzienników nawet wtedy, gdy Ustawienie Hello jest puste.    

połączona tooprovide wysoka dostępność dla bezpośrednich lub grup zarządzania operacji, które komunikują się z OMS za pośrednictwem bramy hello, można użyć tooredirect równoważenia obciążenia sieciowego i dystrybucji hello ruchu na wielu serwerach bramy.  Jeśli jeden serwer bramy jest wyłączona, hello jest przekierowane tooanother dostępnego węzła.  

Zalecane jest zainstalowanie agenta pakietu OMS hello na komputerze hello systemem hello bramy OMS oprogramowania toomonitor hello OMS bramy i analizowanie danych wydajności lub zdarzeń. Ponadto hello agenta pomaga hello bramy OMS zidentyfikować hello punktami końcowymi usług, które wymaga toocommunicate z.

Każdy agent musi mieć bramy tooits łączność w sieci, tak aby agentów automatycznie przenosić dane tooand z hello bramy. Nie zaleca się instalowania bramy hello na kontrolerze domeny.

powitania po diagram przedstawia przepływ danych z tooOMS bezpośredniego agentów przy użyciu serwera bramy hello.  Agenci musi mieć ich dopasowania konfiguracji serwera proxy hello sam port hello OMS bramy jest skonfigurowany toocommunicate z tooOMS.  

![Komunikacja agenta bezpośrednio z diagramu OMS](./media/log-analytics-oms-gateway/oms-omsgateway-agentdirectconnect.png)

Witaj Poniższy diagram przedstawia przepływ danych z tooOMS grupy zarządzania programu Operations Manager.   

![Operations Manager komunikację z diagramu OMS](./media/log-analytics-oms-gateway/oms-omsgateway-opsmgrconnect.png)

## <a name="prerequisites"></a>Wymagania wstępne

Podczas wyznaczania hello toorun komputera bramy OMS, ten komputer musi mieć następujące hello:

* Windows 10, Windows 8.1, Windows 7
* Windows Server 2016, w systemie Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server 2008
* Program .net framework 4.5
* Co najmniej 4 rdzenie procesora i 8 GB pamięci

### <a name="language-availability"></a>Dostępność języka

Hello OMS brama jest dostępna w hello następujące języki:

- Chiński (uproszczony)
- Chiński (tradycyjny)
- Czeski
- Holenderski
- Polski
- Francuski
- Niemiecki
- Węgierski
- Włoski
- Japoński
- Koreański
- Polski
- Portugalski (Brazylia)
- Portugalski (Portugalia)
- Rosyjski
- Hiszpański (Międzynarodowa)

## <a name="download-hello-oms-gateway"></a>Pobierz hello bramy OMS

Istnieją trzy sposoby tooget hello najnowszą wersję pliku instalacyjnego bramy OMS hello.

1. Pobierz z hello [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=54443).

2. Pobrać z portalu OMS hello.  Po zalogowaniu tooyour obszarem roboczym pakietu OMS Przejdź zbyt**ustawienia** > **połączonych źródeł** > **serwerów z systemem Windows** i kliknij przycisk **Pobierz bramy OMS**.

3. Pobierz z hello [portalu Azure](https://portal.azure.com).  Po zalogowaniu:  

   1. Przeglądaj listę hello usług, a następnie wybierz **analizy dzienników**.  
   2. Wybierz obszar roboczy.
   3. W bloku w obszarze roboczym **ogólne**, kliknij przycisk **Szybki Start**.
   4. W obszarze **wybierz roboczym toohello tooconnect źródła danych**, kliknij przycisk **komputerów**.
   5. W hello **bezpośredniego agenta** bloku, kliknij przycisk **Pobierz bramy OMS**.<br><br> ![Pobierz OMS bramy](./media/log-analytics-oms-gateway/download-gateway.png)


## <a name="install-hello-oms-gateway"></a>Zainstaluj hello bramy OMS

tooinstall bramę, wykonaj hello następujące kroki.  Jeśli zainstalowano poprzednią wersję, nazywanych *dziennika analizy usługi przesyłania dalej*, będzie on uaktualniony toothis wersji.  

1. Folder docelowy hello, kliknij dwukrotnie **OMS Gateway.msi**.
2. Na powitania **powitalnej** kliknij przycisk **dalej**.<br><br> ![Kreator instalacji bramy](./media/log-analytics-oms-gateway/gateway-wizard01.png)<br>
3. Na powitania **umowy licencyjnej** wybierz pozycję **akceptuję warunki hello hello umowy licencyjnej** toohello tooagree umowy licencyjnej, a następnie kliknij przycisk **dalej**.
4. Na powitania **portu i serwera proxy adres** strony:
   1. Toobe numer portu TCP hello typu używanym na potrzeby hello bramy. Instalator konfiguruje regułę ruchu przychodzącego z tego numeru portu w Zaporze systemu Windows.  Wartość domyślna Hello jest 8080.
      prawidłowy zakres Hello hello numer portu to od 1 do 65535. Jeśli dane wejściowe hello należy do tego zakresu, zostanie wyświetlony komunikat o błędzie.
   2. Opcjonalnie hello gdy brama hello jest zainstalowany serwer toocommunicate potrzeb przez serwer proxy, wpisz adres serwera proxy hello gdy hello bramy musi tooconnect. Na przykład `http://myorgname.corp.contoso.com:80`.  Jeżeli pole pozostanie puste, bramy hello spróbuje bezpośrednio tooconnect toohello Internet.  Jeśli serwer proxy wymaga uwierzytelnienia, wprowadź nazwę użytkownika i hasło.<br><br> ![Konfiguracja serwera proxy kreatora bramy](./media/log-analytics-oms-gateway/gateway-wizard02.png)<br>   
   3. Kliknij przycisk **Dalej**.
5. Jeśli nie ma włączone usługi Microsoft Update, zostanie wyświetlona strona Microsoft Update hello, w którym można wybrać tooenable go. Wybierz odpowiednią opcję, a następnie kliknij przycisk **dalej**. W przeciwnym razie kontynuuj toohello następnego kroku.
6. Na powitania **Folder docelowy** strony, pozostaw hello domyślnej bramy Files\OMS C:\Program lub typ hello lokalizacji folderu gdzie chcesz tooinstall bramy, a następnie kliknij **dalej**.
7. Na powitania **gotowe tooinstall** kliknij przycisk **zainstalować**. Kontrola konta użytkownika może pojawiać się żądania tooinstall uprawnienia. Jeśli tak, kliknij przycisk **tak**.
8. Po zakończeniu instalacji kliknij przycisk **Zakończ**. Można sprawdzić, czy usługa hello jest uruchomiona przez otwarcie przystawki services.msc hello i upewnij się, że **bramy OMS** jest widoczna na liście hello usług i jego stan jest **systemem**.<br><br> ![Usługi — Brama OMS](./media/log-analytics-oms-gateway/gateway-service.png)  

## <a name="configure-network-load-balancing"></a>Konfigurowanie równoważenia obciążenia sieciowego
Można skonfigurować bramę hello wysokiej dostępności przy użyciu równoważenia obciążenia sieciowego (NLB) firmy Microsoft sieci równoważenia obciążenia (NLB) lub usługi równoważenia obciążenia oparte na sprzęcie.  Witaj modułu równoważenia obciążenia zarządza ruchu przez przekierowywanie hello żądanego połączenia z hello OMS agentów lub serwery zarządzania programu Operations Manager jego węzłach. Jeśli jeden serwer bramy ulegnie awarii, ruch hello pobiera przekierowanego tooother węzłów.

toolearn jak toodesign i wdrożyć klaster równoważenia obciążenia sieciowego systemu Windows Server 2016, zobacz [równoważenia obciążenia sieciowego](https://technet.microsoft.com/windows-server-docs/networking/technologies/network-load-balancing).  Witaj poniższych krokach opisano sposób klaster równoważenia obciążenia tooconfigure sieci firmy Microsoft.  

1.  Zaloguj się na serwerze z systemem Windows hello, należącego do klastra równoważenia obciążenia Sieciowego hello przy użyciu konta administracyjnego.  
2.  Otwórz Menedżera równoważenia obciążenia sieciowego w Menedżerze serwera, kliknij przycisk **narzędzia**, a następnie kliknij przycisk **Menedżera równoważenia obciążenia sieciowego**.
3. tooconnect z serwerem bramy OMS z hello Microsoft Monitoring Agent został zainstalowany, kliknij prawym przyciskiem myszy adres IP klastra hello, a następnie kliknij przycisk **tooCluster Dodaj hosta**.<br><br> ![Menedżer równoważenia obciążenia sieci — Dodawanie tooCluster hosta](./media/log-analytics-oms-gateway/nlb02.png)<br>
4. Wprowadź adres IP hello powitania serwera bramy, które mają tooconnect.<br><br> ![Menedżer równoważenia obciążenia sieci — Dodawanie hosta tooCluster: połączenie](./media/log-analytics-oms-gateway/nlb03.png)

## <a name="configure-oms-agent-and-operations-manager-management-group"></a>Konfigurowanie agenta pakietu OMS i grupy zarządzania programu Operations Manager
Hello Poniższa sekcja zawiera kroki na jak tooconfigure bezpośrednio połączony OMS agentów grupy zarządzania programu Operations Manager i Azure Automation hybrydowymi elementami roboczymi Runbook z hello toocommunicate OMS bramy z usługą OMS.  

toounderstand wymagania i kroki na jak tooinstall hello agent pakietu OMS na komputerach z systemem Windows bezpośredniego połączenia tooOMS, zobacz [tooOMS komputerów Windows połączyć](log-analytics-windows-agents.md) lub Linux komputerów znajduje się w temacie [komputery z połączenia z systemem Linux tooOMS](log-analytics-linux-agents.md).

### <a name="configuring-hello-oms-agent-and-operations-manager-toouse-hello-oms-gateway-as-a-proxy-server"></a>Konfigurowanie agenta pakietu OMS hello i Operations Manager toouse hello OMS bramy jako serwer proxy

### <a name="configure-standalone-oms-agent"></a>Konfigurowanie agenta pakietu OMS autonomiczny
Zobacz [skonfigurować ustawienia serwera proxy i zapory za pomocą programu Microsoft Monitoring Agent hello](log-analytics-proxy-firewall.md) informacji o konfigurowaniu toouse agent serwera proxy, który w tym przypadku jest hello bramy.  Jeśli wdrożono wiele serwerów bramy za modułem równoważenia obciążenia sieciowego, konfiguracji serwera proxy agenta pakietu OMS hello jest hello wirtualnego adresu IP hello równoważenia obciążenia Sieciowego:<br><br> ![Microsoft Monitoring Agent właściwości — ustawienia serwera Proxy](./media/log-analytics-oms-gateway/nlb04.png)

### <a name="configure-operations-manager---all-agents-use-hello-same-proxy-server"></a>Konfigurowanie programu Operations Manager — Wszyscy agenci Użyj hello tego samego serwera proxy
Możesz skonfigurować serwer bramy programu Operations Manager tooadd hello.  Hello programu Operations Manager, konfiguracja serwera proxy jest automatycznie stosowane agenci tooall tooOperations menedżera, nawet jeśli ustawienie hello jest pusta.

toouse hello bramy toosupport programu Operations Manager wymagane są:

* Microsoft Monitoring Agent (wersja agenta — **8.0.10900.0** i nowsze) zainstalowany na serwerze bramy hello i skonfigurowany do obszarów roboczych z OMS hello, z których ma zostać toocommunicate.
* Hello bramy musi mieć łączność z Internetem lub być tooa podłączonego serwera proxy, który wykonuje.

> [!NOTE]
> Jeśli nie określisz wartości dla bramy hello puste wartości są wypychana agentów tooall.


1. Witaj Otwórz konsolę programu Operations Manager i w obszarze **Operations Management Suite**, kliknij przycisk **połączenia** , a następnie kliknij przycisk **Konfiguracja serwera Proxy**.<br><br> ![Operations Manager — Konfiguracja serwera Proxy](./media/log-analytics-oms-gateway/scom01.png)<br>
2. Wybierz **Użyj powitania tooaccess serwera proxy usługi Operations Management Suite** a następnie wpisz adres IP powitania serwera bramy OMS hello lub wirtualny adres IP hello równoważenia obciążenia Sieciowego. Upewnij się, rozpoczynać hello `http://` prefiks.<br><br> ![Operations Manager — adres serwera proxy](./media/log-analytics-oms-gateway/scom02.png)<br>
3. Kliknij przycisk **Zakończ**. Serwer programu Operations Manager jest połączonych tooyour obszarem roboczym pakietu OMS.

### <a name="configure-operations-manager---specific-agents-use-proxy-server"></a>Konfigurowanie programu Operations Manager — określonych agentów Użyj serwera proxy
W przypadku środowisk dużych lub złożonych można tylko określonych serwerów (lub grup) toouse powitania serwera bramy OMS.  Na tych serwerach nie można zaktualizować hello agenta bezpośrednio jako ta wartość zostanie zastąpiona hello wartości globalnej hello grupy zarządzania programu Operations Manager.  Zamiast tego należy toooverride hello zasada używana toopush tych wartości.

> [!NOTE]
> Ten sam sposób konfiguracji mogą być używane w środowisku używanie hello tooallow wiele serwerów bramy OMS.  Na przykład może wymagać określonych toobe serwerów bramy OMS określony na podstawie na region.

1. Witaj Otwórz konsolę programu Operations Manager i wybierz hello **tworzenie** obszaru roboczego.  
2. W obszarze roboczym tworzenie hello, wybierz **reguły** i kliknij przycisk hello **zakres** przycisk na powitania narzędzi programu Operations Manager. Jeśli ten przycisk jest niedostępny, sprawdź toomake się, że wybrany obiekt, nie folder, w okienku monitorowanie hello. Witaj **zakres obiektów pakietu administracyjnego** okno dialogowe wyświetla listę typowych klasy docelowej, grupami lub obiektami.
3. Typ **usługi kondycji** w hello **Wyszukaj** pola i wybierz ją z listy hello.  Kliknij przycisk **OK**.  
4. Wyszukaj regułę hello **regułę ustawienie serwera Proxy usługi Advisor** i hello pasku narzędzi konsoli operacje, kliknij przycisk **zastępuje** , a następnie wskaż zbyt**hello zastąpienie Rule\For konkretnego obiektu klasy: kondycji Usługa** i wybierz z listy hello określonego obiektu.  Opcjonalnie można utworzyć grupę niestandardowego obiektu usługi kondycji hello hello serwerów ma tooapply tooand to zastąpienie, zastosuj hello zastąpienie toothat grupy.
5. W hello **właściwości zastąpienia** okna dialogowego kliknij znacznik wyboru w hello tooplace **zastąpienia** toohello dalej kolumny **WebProxyAddress** parametru.  W hello **wartość zastąpienia** wprowadź URL hello zapewnienia serwera bramy OMS hello rozpoczynać hello `http://` prefiks.
   >[!NOTE]
   > Nie trzeba tooenable hello reguły, ponieważ jest już zarządzany automatycznie za pomocą zastąpienia zawiera hello Microsoft System Center Advisor bezpiecznego odwołania Override pakiet administracyjny przeznaczonych dla hello grupy monitorowania serwera programu Microsoft System Center Advisor.
   >
6. Wybierz pakiet administracyjny z hello **wybierz docelowy pakiet administracyjny** listy lub utworzenie nowego niezapieczętowanego pakietu przez kliknięcie przycisku **nowy**.
7. Po zakończeniu zmiany, kliknij przycisk **OK**.

### <a name="configure-for-automation-hybrid-workers"></a>Konfigurowanie dla automatyzacji hybrydowych procesów roboczych
Jeśli masz automatyzacji hybrydowymi elementami roboczymi Runbook w środowisku hello następujące kroki, podaj ręczne, tymczasowego obejścia tooconfigure hello bramy toosupport je.

Hello następujące kroki należy tooknow hello region platformy Azure, w którym znajduje się hello konta automatyzacji. Lokalizacja hello toolocate:

1. Zaloguj się toohello [portalu Azure](https://portal.azure.com/).
2. Wybierz hello usługi Automatyzacja Azure.
3. Wybierz odpowiednie konto usługi Automatyzacja Azure hello.
4. Wyświetl jego regionu, w obszarze **lokalizacji**.<br><br> ![Portal Azure — Lokalizacja konta automatyzacji](./media/log-analytics-oms-gateway/location.png)  

Użyj następującego adresu URL hello tooidentify tabel dla każdej lokalizacji hello:

**Zadanie adresy URL usługi danych dla środowiska uruchomieniowego**

| **location** | **ADRES URL** |
| --- | --- |
| Środkowo-północne stany USA |ncus-jobruntimedata produkcyjną su1.azure-automation.net |
| Europa Zachodnia |we-jobruntimedata-prod-su1.azure-automation.net |
| Środkowo-południowe stany USA |scus-jobruntimedata-prod-su1.azure-automation.net |
| Wschodnie stany USA 2 |eus2-jobruntimedata-prod-su1.azure-automation.net |
| Kanada centralnej |cc-jobruntimedata-prod-su1.azure-automation.net |
| Europa Północna |ne-jobruntimedata-prod-su1.azure-automation.net |
| Azja Południowo-Wschodnia |sea-jobruntimedata-prod-su1.azure-automation.net |
| Indie Środkowe |cid-jobruntimedata-prod-su1.azure-automation.net |
| Japonia |jpe-jobruntimedata-prod-su1.azure-automation.net |
| Australia |ase-jobruntimedata-prod-su1.azure-automation.net |

**Adresy URL usługi agenta**

| **location** | **ADRES URL** |
| --- | --- |
| Środkowo-północne stany USA |ncus-agentservice produkcyjną 1.azure-automation.net |
| Europa Zachodnia |nie możemy agentservice produkcyjną 1.azure-automation.net |
| Środkowo-południowe stany USA |scus-agentservice produkcyjną 1.azure-automation.net |
| Wschodnie stany USA 2 |eus2-agentservice produkcyjną 1.azure-automation.net |
| Kanada centralnej |DW — agentservice produkcyjną 1.azure-automation.net |
| Europa Północna |ne — agentservice produkcyjną 1.azure-automation.net |
| Azja Południowo-Wschodnia |SEA-agentservice produkcyjną 1.azure-automation.net |
| Indie Środkowe |CID-agentservice produkcyjną 1.azure-automation.net |
| Japonia |jpe-agentservice produkcyjną 1.azure-automation.net |
| Australia |ASE-agentservice produkcyjną 1.azure-automation.net |

Jeśli komputer jest zarejestrowany jako hybrydowy proces roboczy elementu Runbook automatycznie dla stosowania poprawek za pomocą rozwiązania zarządzania aktualizacjami hello, wykonaj następujące kroki:

1. Dodawanie listy hostów dozwolone toohello adresy URL hello danych czasu wykonywania zadania usługi na powitania OMS bramy. Na przykład: `Add-OMSGatewayAllowedHost we-jobruntimedata-prod-su1.azure-automation.net`
2. Ponownie uruchom usługę bramy OMS hello za pomocą następującego polecenia cmdlet programu PowerShell hello:`Restart-Service OMSGatewayService`

Jeśli komputer jest na dodawanej tooAzure automatyzacji za pomocą polecenia cmdlet rejestracji hello hybrydowy proces roboczy elementu Runbook, wykonaj następujące kroki:

1. Dodawanie listy hostów dozwolone toohello adres URL rejestracji hello agenta usługi na powitania OMS bramy. Na przykład: `Add-OMSGatewayAllowedHost ncus-agentservice-prod-1.azure-automation.net`
2. Dodawanie listy hostów dozwolone toohello adresy URL hello danych czasu wykonywania zadania usługi na powitania OMS bramy. Na przykład: `Add-OMSGatewayAllowedHost we-jobruntimedata-prod-su1.azure-automation.net`
3. Uruchom ponownie usługę bramy OMS hello.
    `Restart-Service OMSGatewayService`

## <a name="useful-powershell-cmdlets"></a>Przydatne poleceń cmdlet programu PowerShell
Polecenia cmdlet ułatwiają wykonanie zadania, które są ustawieniami konfiguracji bram wymaganych tooupdate hello OMS. Przed ich użyciem, należy koniecznie:

1. Zainstaluj hello OMS bramy (MSI).
2. Otwórz okno konsoli programu PowerShell.
3. Moduł hello tooimport, wpisz następujące polecenie:`Import-Module OMSGateway`
4. Jeśli w poprzednim kroku hello nie wystąpił żaden błąd, moduł hello została pomyślnie zaimportowana i hello polecenia cmdlet mogą być używane. Typ`Get-Module OMSGateway`
5. Po wprowadzeniu zmian przy użyciu poleceń cmdlet hello, upewnij się, ponownie uruchom usługę bramy hello.

Jeśli wystąpi błąd w kroku 3 hello moduł nie został zaimportowany. Błąd Hello może występować po toofind hello modułu programu PowerShell. Możesz go znaleźć w ścieżce instalacji bramy hello: *C:\Program Files\Microsoft OMS Gateway\PowerShell*.

| **Polecenia cmdlet** | **Parametry** | **Opis** | **Przykład** |
| --- | --- | --- | --- |  
| `Get-OMSGatewayConfig` |Klucz |Pobiera konfigurację hello hello usługi |`Get-OMSGatewayConfig` |  
| `Set-OMSGatewayConfig` |Klucz (wymagane) <br> Wartość |Konfiguracji usługi hello hello zmiany |`Set-OMSGatewayConfig -Name ListenPort -Value 8080` |  
| `Get-OMSGatewayRelayProxy` | |Pobiera hello adres serwera proxy (nadrzędnego) przekazywania |`Get-OMSGatewayRelayProxy` |  
| `Set-OMSGatewayRelayProxy` |Adres<br> Nazwa użytkownika<br> Hasło |Ustawia adres hello (i poświadczeń) przekazywania (nadrzędnego) serwera proxy |1. Ustaw proxy przekazywania i poświadczeń:<br> `Set-OMSGatewayRelayProxy`<br>`-Address http://www.myproxy.com:8080`<br>`-Username user1 -Password 123` <br><br> 2. Ustaw przekazywania serwer proxy, który nie wymaga uwierzytelniania:`Set-OMSGatewayRelayProxy`<br> `-Address http://www.myproxy.com:8080` <br><br> 3. Wyczyść hello przekazywania ustawienie serwera proxy:<br> `Set-OMSGatewayRelayProxy` <br> `-Address ""` |  
| `Get-OMSGatewayAllowedHost` | |Pobiera hello obecnie dozwolone hosta (tylko hello lokalnie skonfigurowanym hostem dozwolone, nie ma automatycznie pobrane dozwolonych hostów) |`Get-OMSGatewayAllowedHost` |
| `Add-OMSGatewayAllowedHost` |Host (wymagane) |Dodaje toohello hosta hello listy dozwolonych |`Add-OMSGatewayAllowedHost -Host www.test.com` |  
| `Remove-OMSGatewayAllowedHost` |Host (wymagane) |Usuwa hello hosta z listy dozwolonych hello |`Remove-OMSGatewayAllowedHost`<br> `-Host www.test.com` |  
| `Add-OMSGatewayAllowedClientCertificate` |Temat (wymagane) |Dodaje powitania klienta certyfikatu podmiotu toohello listy dozwolonych |`Add-OMSGatewayAllowed`<br>`ClientCertificate` <br> `-Subject mycert` |  
| `Remove-OMSGatewayAllowedClientCertificate` |Temat (wymagane) |Usuwa z listy dozwolonych hello podmiotu certyfikatu powitania klienta |`Remove-OMSGatewayAllowed` <br> `ClientCertificate` <br> `-Subject mycert` |  
| `Get-OMSGatewayAllowedClientCertificate` | |Pobiera hello obecnie dozwolone klienta podmiotom certyfikatów (tylko lokalne powitania skonfigurowane dozwolonych tematów, nie ma automatycznie pobrane tematów dozwolonych) |`Get-`<br>`OMSGatewayAllowed`<br>`ClientCertificate` |  

## <a name="troubleshooting"></a>Rozwiązywanie problemów
toocollect zdarzenia rejestrowane przez bramę hello, należy tooalso został zainstalowany agent pakietu OMS hello.<br><br> ![Podgląd zdarzeń — dziennik bramy OMS](./media/log-analytics-oms-gateway/event-viewer.png)

**Identyfikatory zdarzeń bramy OMS wraz z opisami**

Witaj poniższej tabeli hello identyfikatory zdarzeń i opisy zdarzeń w dzienniku bramy OMS.

| **Identyfikator** | **Opis** |
| --- | --- |
| 400 |Błąd żadnych aplikacji, który nie ma identyfikator unikatowy |
| 401 |Złej konfiguracji. Na przykład: listenPort = "tekst", a liczba całkowita |
| 402 |Wyjątek podczas analizowania wiadomości uzgadnianie TLS |
| 403 |Wystąpił błąd sieci. Na przykład: nie można połączyć z serwerem tootarget |
| 100 |Informacje ogólne |
| 101 |Usługa została uruchomiona |
| 102 |Usługa została zatrzymana |
| 103 |Odebrano polecenie połączenia HTTP z klienta |
| 104 |Nie poleceń POŁĄCZYĆ HTTP |
| 105 |Serwer docelowy nie jest na liście dozwolonych lub hello port docelowy nie jest bezpieczny port (port 443) <br> <br> Upewnij się, że agent MMA hello na serwerze bramy oraz agentów hello komunikacji z hello bramy są połączone toohello tego samego obszaru roboczego analizy dzienników. |
| 105 |Błąd TcpConnection — nieprawidłowy certyfikat: CN = bramy <br><br> Upewnij się, że: <br>    <br> & #149; Korzystania z bramy z numerem wersji 1.0.395.0 lub nowszej. <br> & #149; Witaj agent MMA na serwerze bramy oraz agentów hello komunikacji z hello bramy są połączone toohello tego samego obszaru roboczego analizy dzienników. |
| 106 |Jakiegokolwiek powodu sesji TLS hello jest podejrzane i odrzucone |
| 107 |Zweryfikowano Hello sesji protokołu TLS |

**Toocollect liczniki wydajności**

Witaj poniższej tabeli przedstawiono dostępne dla bramy OMS hello liczniki wydajności hello. Możesz dodać liczniki hello korzystanie z Monitora wydajności.

| **Nazwa** | **Opis** |
| --- | --- |
| Połączenie klienta bramy/aktywny OMS |Liczba aktywnych połączeń z klientami sieci (TCP) |
| Liczba błędów/bramy OMS |Liczba błędów |
| OMS/połączenia bramy klienta |Liczba połączonych klientów |
| Liczba bramy/odrzucenia OMS |Liczba odrzuceń ze względu na błąd sprawdzania poprawności tooany TLS |

![Liczniki wydajności bramy OMS](./media/log-analytics-oms-gateway/counters.png)

## <a name="get-assistance"></a>Uzyskiwanie pomocy
Gdy użytkownik jest zalogowany toohello portalu Azure, można utworzyć żądanie pomocy z hello OMS bramy lub innych usług Azure lub funkcji usługi.
Kliknij symbol znaku zapytania hello w hello prawym górnym rogu portalu hello pomocy toorequest, a następnie kliknij przycisk **nowy obsługuje żądania**. Następnie należy wykonać hello nowego formularza żądania pomocy technicznej.

![Nowe żądanie pomocy technicznej](./media/log-analytics-oms-gateway/support.png)

Można także pozostawić swoją opinię na temat OMS lub analizy dzienników na powitania [forum opinii Microsoft Azure](https://feedback.azure.com/forums/267889).

## <a name="next-steps"></a>Następne kroki
* [Dodaj źródła danych](log-analytics-data-sources.md) toocollect danych z hello połączonych źródeł w obszarze roboczym pakietu OMS i zapisze go w repozytorium OMS hello.
