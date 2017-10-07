---
title: aaaConnect programu Operations Manager tooLog Analytics | Dokumentacja firmy Microsoft
description: "toomaintain z istniejących inwestycji w programie System Center Operations Manager i użyj rozszerzone możliwości za pomocą analizy dzienników, Operations Manager można zintegrować z obszarem roboczym pakietu OMS."
services: log-analytics
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: 245ef71e-15a2-4be8-81a1-60101ee2f6e6
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/21/2017
ms.author: magoedte
ms.openlocfilehash: b2841c7aa209fec7357dc4c8b1ff4325fdaa37ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-operations-manager-toolog-analytics"></a>Łączenie programu Operations Manager tooLog analityka
toomaintain z istniejących inwestycji w programie System Center Operations Manager i użyj rozszerzone możliwości za pomocą analizy dzienników, Operations Manager można zintegrować z obszarem roboczym pakietu OMS.  Dzięki temu wykorzystać możliwości hello OMS pozostawiając toouse programu Operations Manager do:

* Kontynuować monitorowanie kondycji hello usług IT z programem Operations Manager
* Obsługa integracji z rozwiązaniami Zarządzanie usługami IT — Obsługa zarządzania zdarzeniami i problemów
* Zarządzanie cyklem życia hello agentów wdrożonych tooon lokalne i maszyny wirtualne IaaS chmury publicznej, które należy monitorować za pomocą programu Operations Manager

Integracja z programem System Center Operations Manager dodaje wartość tooyour usługi operations strategii za pomocą hello szybkości i wydajności OMS w zbierania, przechowywania i analizowania danych z programu Operations Manager.  Korelując pomaga OMS i pracy w kierunku identyfikowanie hello usterek, problemów i udostępniając cykle w związku z procesu zarządzania istniejący problem.   Witaj elastyczność hello wyszukiwania aparatu tooexamine wydajności, zdarzeń i alert danych, za pomocą zaawansowanych pulpitów nawigacyjnych i tooexpose możliwości raportowania tych danych w przejrzysty sposób prezentuje siły hello, który dostarcza OMS complimenting programu Operations Manager.

agenci Hello grupy zarządzania programu Operations Manager toohello zbieranie danych z serwerów na podstawie źródeł danych analizy dzienników hello i rozwiązania, jakie włączono w ramach subskrypcji pakietu OMS.  W zależności od rozwiązania hello, które aktywowano są albo wysyłane bezpośrednio z serwera zarządzania programu Operations Manager toohello OMS usługi sieci web lub z powodu hello ilość danych zebranych w systemie zarządzane z wykorzystaniem agentów hello są wysyłane bezpośrednio dane z tych rozwiązań z hello agenta tooOMS usługi sieci web. Serwer zarządzania Hello przekazuje dane OMS hello bezpośrednio toohello OMS sieci web usługi; Baza danych programu Operations Manager lub OperationsManagerDW toohello nigdy nie zostaną zapisane.  Gdy serwer zarządzania utraci łączność z usługą sieci web OMS hello, buforuje hello danych lokalnie, dopóki komunikacji nie zostanie nawiązane ponownie z usługą OMS.  Jeśli serwer zarządzania hello jest w trybie offline, ponieważ tooplanned konserwacji i nieplanowanych awarii, inny serwer zarządzania w grupie zarządzania hello wznawia łączność z usługą OMS.  

Witaj Poniższy diagram przedstawia hello połączenia między serwerami zarządzania hello i agentów w grupie zarządzania programu System Center Operations Manager i OMS, w tym kierunku hello i portów.   

![OMS — operacji manager integracji — diagram](./media/log-analytics-om-agents/oms-operations-manager-connection.png)

Jeśli zasady zabezpieczeń IT nie zezwalają na toohello tooconnect Twojego sieci Internet komputerów, serwerów zarządzania można informacje o konfiguracji tooreceive skonfigurowanych tooconnect toohello OMS bramy i wysyłania danych zebranych w zależności od rozwiązania hello włączono.  Aby uzyskać więcej informacji i kroki na tooconfigure toocommunicate grupy zarządzania programu Operations Manager, tak za pośrednictwem bramy OMS toohello usługę, zobacz temat [połączyć tooOMS komputerów przy użyciu hello bramy OMS](log-analytics-oms-gateway.md).  

## <a name="system-requirements"></a>Wymagania systemowe
Przed rozpoczęciem należy przejrzeć powitania po tooverify szczegółowe informacje, które spełniają wymagania wstępne.

* OMS obsługuje tylko programu Operations Manager 2016, UR6 dodatku SP1 dla programu Operations Manager 2012 lub nowszej, a programu Operations Manager 2012 R2 UR2 i większa.  Obsługa serwera proxy została dodana w programach Operations Manager 2012 SP1 UR7 i Operations Manager 2012 R2 UR3.
* Wszystkie agenty programu Operations Manager musi spełniać wymagania minimalne pomocy technicznej. Upewnij się, że agenci są przy minimalnej aktualizacji hello, w przeciwnym razie ruchu agenta systemu Windows może zakończyć się niepowodzeniem i wiele błędów może wypełnić dziennik zdarzeń programu Operations Manager hello.
* Subskrypcja pakietu OMS.  Aby uzyskać więcej informacji, przejrzyj [wprowadzenie do analizy dzienników](log-analytics-get-started.md).

### <a name="network"></a>Sieć
Witaj informacje poniżej listy powitania serwera proxy i zapory informacje konfiguracyjne wymagane hello agenta programu Operations Manager, serwerów zarządzania i toocommunicate konsoli operacje z usługą OMS.  Ruch z każdego składnika jest wychodzący z usługą OMS toohello sieci.     

|Zasób | Numer portu| Obejście kontroli HTTP|  
|---------|------|-----------------------|  
|**Agent**|||  
|\*.ods.opinsights.azure.com| 443 |Tak|  
|\*.oms.opinsights.azure.com| 443|Tak|  
|\*.blob.core.windows.net| 443|Tak|  
|\*.azure-automation.net| 443|Tak|  
|**Serwer zarządzania**|||  
|\*.service.opinsights.azure.com| 443||  
|\*.blob.core.windows.net| 443| Tak|  
|\*.ods.opinsights.azure.com| 443| Tak|  
|*.azure-automation.net | 443| Tak|  
|**TooOMS konsoli programu Operations Manager**|||  
|service.systemcenteradvisor.com| 443||  
|\*.service.opinsights.azure.com| 443||  
|\*.live.com| 80 i 443||  
|\*.microsoft.com| 80 i 443||  
|\*.microsoftonline.com| 80 i 443||  
|\*.mms.microsoft.com| 80 i 443||  
|login.windows.net| 80 i 443||  


## <a name="connecting-operations-manager-toooms"></a>Łączenie tooOMS programu Operations Manager
Wykonaj powitania po serii kroków tooconfigure Twojego programu Operations Manager management grupy tooconnect tooone Twoich obszarów roboczych OMS.

1. W konsoli programu Operations Manager hello wybierz hello **administracji** obszaru roboczego.
2. Rozwiń węzeł usługi Operations Management Suite hello, a następnie kliknij przycisk **połączenia**.
3. Kliknij przycisk hello **zarejestrować tooOperations Management Suite** łącza.
4. Na powitania **Kreator dołączania Operations Management Suite: uwierzytelnianie** strony, wprowadź adres e-mail hello lub numeru telefonu i hasło konta administratora hello, który jest skojarzony z subskrypcją pakietu OMS, a następnie kliknij przycisk  **Zaloguj się**.
5. Po możesz pomyślnym uwierzytelnieniu, na powitania **Kreator dołączania Operations Management Suite: Wybierz obszar roboczy** strony, zostanie wyświetlony monit tooselect obszar roboczy OMS.  Jeśli masz więcej niż jednego obszaru roboczego wybierz hello obszaru roboczego można tooregister z grupą zarządzania programu Operations Manager hello z listy rozwijanej hello, a następnie kliknij przycisk **dalej**.
   
   > [!NOTE]
   > Operations Manager obsługuje tylko jeden obszar roboczy OMS naraz. połączenia Hello i hello komputerów, które były zarejestrowane tooOMS z obszarem roboczym poprzedniej hello są usuwane z usługą OMS.
   > 
   > 
6. Na powitania **Kreator dołączania Operations Management Suite: Podsumowanie** , Potwierdź ustawienia i jeśli są poprawne, kliknij przycisk **Utwórz**.
7. Na powitania **Kreator dołączania Operations Management Suite: Zakończ** kliknij przycisk **Zamknij**.

### <a name="add-agent-managed-computers"></a>Dodaj komputery zarządzane z wykorzystaniem agentów
Po skonfigurowaniu integracji z obszarem roboczym pakietu OMS, to tylko nawiąże połączenie z usługą OMS, zbierane żadne dane z agentów hello raportowania tooyour grupy zarządzania. Nie będzie to nastąpić dopiero po skonfigurowaniu, które określone komputery zarządzane z wykorzystaniem agentów zbiera dane analizy dziennika. Możesz wybrać obiekty komputerów hello indywidualnie lub wybrać grupy, który zawiera obiekty typu komputer z systemem Windows. Nie można wybrać grupę zawierającą wystąpienia klasy innego, takich jak dyski logiczne w systemie lub bazy danych SQL.

1. Witaj Otwórz konsolę programu Operations Manager i wybierz hello **administracji** obszaru roboczego.
2. Rozwiń węzeł usługi Operations Management Suite hello, a następnie kliknij przycisk **połączenia**.
3. Kliknij przycisk hello **dodać grupy** łącze pod hello akcje pozycji na powitania po prawej stronie powitania okienka.
4. W hello **wyszukiwanie komputera** okno dialogowe, możesz wyszukać komputerów lub grup monitorowanych przez program Operations Manager. Wybierz tooOMS tooonboard komputery lub grupy, kliknij przycisk **Dodaj**, a następnie kliknij przycisk **OK**.

Możesz wyświetlić komputerów i grup skonfigurowane toocollect danych z komputerów zarządzanych hello węźle Operations Management Suite w hello **administracji** roboczym hello konsoli operacje.  W tym miejscu można Dodaj lub usuń komputery i grupy odpowiednio do potrzeb.

### <a name="configure-oms-proxy-settings-in-hello-operations-console"></a>Skonfiguruj ustawienia serwera proxy OMS w konsoli operacje hello
Wykonaj następujące kroki, jeśli wewnętrzny serwer proxy jest między grupą zarządzania hello a usługę sieci web hello.  Te ustawienia są zarządzane centralnie z hello grupy zarządzania i zarządzanych tooagent systemów rozproszonych uwzględnionych w hello zakres toocollect dane dla OMS.  Jest to przydatne w przypadku podczas niektórych rozwiązań obejścia hello zarządzania serwera i wysyłania danych bezpośrednio tooOMS usługi sieci web.

1. Witaj Otwórz konsolę programu Operations Manager i wybierz hello **administracji** obszaru roboczego.
2. Rozwiń pozycję Operations Management Suite, a następnie kliknij przycisk **połączenia**.
3. W hello połączenia OMS widok, kliknij przycisk **Konfiguracja serwera Proxy**.
4. Na **Kreator Operations Management Suite: serwer Proxy** wybierz pozycję **Użyj powitania tooaccess serwera proxy usługi Operations Management Suite**, a następnie wpisz adres URL hello z hello numer portu, na przykład http:// corpproxy:80, a następnie kliknij przycisk **Zakończ**.

Jeśli serwer proxy wymaga uwierzytelniania, wykonaj następujące hello kroki tooconfigure poświadczeń i ustawień, które muszą toopropagate toomanaged komputerów, które raporty tooOMS w grupie zarządzania hello.

1. Witaj Otwórz konsolę programu Operations Manager i wybierz hello **administracji** obszaru roboczego.
2. W obszarze **Konfiguracja Uruchom jako** wybierz pozycję **Profile**.
3. Otwórz hello **System Center Advisor jako serwera Proxy profilu Uruchom** profilu.
4. W hello Kreatora profilu Uruchom jako kliknij przycisk Dodaj toouse konto Uruchom jako. Można utworzyć [konta Uruchom jako](https://technet.microsoft.com/library/hh321655.aspx) lub użyj istniejącego konta. To konto musi toohave wystarczające uprawnienia toopass za pośrednictwem serwera proxy hello.
5. tooset hello toomanage konta, wybierz **wybraną klasę, grupę lub obiekt**, kliknij przycisk **wybierz...** a następnie kliknij przycisk **grupy...** Witaj tooopen **wyszukiwania grupy** pole.
6. Wyszukaj, a następnie wybierz **grupy monitorowania serwera programu Microsoft System Center Advisor**.  Kliknij przycisk **OK** po wybraniu hello grupy tooclose hello **wyszukiwania grupy** pole.
7. Kliknij przycisk **OK** tooclose hello **Dodaj konto Uruchom jako** pola.
8. Kliknij przycisk **zapisać** toocomplete hello kreatora i Zapisz zmiany.

Po utworzeniu połączenia hello i konfigurowanie agentów, które będą zbierania i raportowania danych tooOMS, hello następującej konfiguracji jest stosowane w grupie zarządzania hello, niekoniecznie w kolejności:

* Konto Uruchom jako Hello **Microsoft.SystemCenter.Advisor.RunAsAccount.Certificate** jest tworzony.  Jest on skojarzony z profilem Uruchom jako hello **Microsoft System Center Advisor Uruchom jako profil obiektu Blob** i dotyczy dwóch klas - **serwera zbierania** i **grupa zarządzania programu Operations Manager** .
* Są tworzone dwa łączniki.  Witaj najpierw nosi nazwę **Microsoft.SystemCenter.Advisor.DataConnector** i jest automatycznie konfigurowana subskrypcji, która przekazuje wszystkie alerty wygenerowane z wystąpień wszystkie klasy w tooOMS grupy zarządzania hello dziennika Analityka. drugi łącznik Hello jest **łącznik usługi Advisor**, który jest odpowiedzialny za udostępnianie danych i komunikacji z usługą sieci web OMS.
* Agentów i grup, że wybrano toocollect danych w grupie zarządzania hello jest dodawany toohello **grupy monitorowania serwera programu Microsoft System Center Advisor**.

## <a name="management-pack-updates"></a>Aktualizacji pakietu administracyjnego
Po zakończeniu konfiguracji grupy zarządzania programu Operations Manager hello ustanawia połączenie z hello usługę.  Serwer zarządzania Hello synchronizuje się z usługą sieci web hello i odbierać informacje o zaktualizowanej konfiguracji w postaci hello pakietów administracyjnych dla rozwiązania hello włączonego integrujące się z programem Operations Manager.   Operations Manager sprawdza dostępność aktualizacji tych pakietów administracyjnych i automatycznie pobrać i importowane, gdy są one dostępne.  Istnieją dwie reguły w szczególności kontrolować to zachowanie, które:

* **Microsoft.SystemCenter.Advisor.MPUpdate** -aktualizuje hello podstawowej OMS pakietów administracyjnych. Domyślnie uruchamiane co 12 godzin.
* **Microsoft.SystemCenter.Advisor.Core.GetIntelligencePacksRule** — aktualizacje pakietów administracyjnych rozwiązania włączona w obszarze roboczym. Domyślnie uruchamiane co pięć (5) minut.

Można zastąpić te dwie reguły tooeither uniemożliwiają automatyczne pobieranie wyłączając je, lub zmodyfikować częstotliwości hello częstotliwość hello serwera zarządzania synchronizuje się z usługą OMS toodetermine Jeśli nowy pakiet zarządzania jest dostępny i powinien zostać pobrany.  Wykonaj kroki hello [jak tooOverride zasady lub monitora](https://technet.microsoft.com/library/hh212869.aspx) toomodify hello **częstotliwość** parametru z wartością w sekundach toochange hello harmonogram synchronizacji lub zmodyfikować hello **włączone**  parametr toodisable hello reguły.  Docelowy hello przesłania tooall obiektów klasy grupa zarządzania programu Operations Manager.

Toocontinue następujące istniejące zmiany kontroli procesu kontroli wersji pakietu zarządzania w danej grupie zarządzania w środowisku produkcyjnym należy można wyłączyć reguły hello i włączyć je w określonych godzinach, kiedy aktualizacje są dozwolone. Jeśli masz rozwoju lub grupy zarządzania w odpowiedzi na pytania w danym środowisku i ma toohello połączenia internetowego, można skonfigurować tej grupy zarządzania z toosupport obszar roboczy OMS tego scenariusza.  To pozwala tooreview i ocenić hello iteracyjne wersje pakietów administracyjnych OMS hello przed ich do grupy zarządzania produkcji.

## <a name="switch-an-operations-manager-group-tooa-new-oms-workspace"></a>Przełącz tooa grupę programu Operations Manager nowy obszar roboczy OMS
1. Zaloguj się za tooyour OMS subskrypcji i Utwórz obszar roboczy w [programu Microsoft Operations Management Suite](http://oms.microsoft.com/).
2. Witaj Otwórz konsolę programu Operations Manager przy użyciu konta należącego do roli Administratorzy programu Operations Manager hello i wybierz hello **administracji** obszaru roboczego.
3. Rozwiń pozycję Operations Management Suite, a następnie wybierz **połączenia**.
4. Wybierz hello **skonfiguruj ponownie operację Management Suite** łącze na powitania bliski po stronie powitania okienka.
5. Wykonaj hello **Kreator dołączania Operations Management Suite** i wprowadź hello wiadomości e-mail adres lub numer telefonu i hasło konta administratora hello, który jest skojarzony z nowy obszar roboczy OMS.
   
   > [!NOTE]
   > Witaj **Kreator dołączania Operations Management Suite: Wybierz obszar roboczy** strona przedstawia hello istniejący obszar roboczy, który jest używany.
   > 
   > 

## <a name="validate-operations-manager-integration-with-oms"></a>Sprawdź poprawność integracji programu Operations Manager z usługą OMS
Istnieje kilka sposobów można sprawdzić, czy Twoje tooOperations OMS integracji Manager zakończy się pomyślnie.

### <a name="tooconfirm-integration-from-hello-oms-portal"></a>Integracja tooconfirm hello portalu OMS
1. W portalu OMS hello, kliknij przycisk hello **ustawienia** kafelka
2. Wybierz **połączone źródła**.
3. W tabeli hello w obszarze hello sekcji System Center Operations Manager powinny pojawić się hello Nazwa grupy zarządzania hello wyświetlone hello liczby agentów i stan po ostatniej Odebrano dane.
   
   ![connectedsources-OMS — ustawienia](./media/log-analytics-om-agents/oms-settings-connectedsources.png)
4. Uwaga hello **identyfikator obszaru roboczego** wartości w ramach powitania po lewej stronie powitania ustawienia strony.  Należy sprawdzić jego poprawność poniżej grupy zarządzania programu Operations Manager.  

### <a name="tooconfirm-integration-from-hello-operations-console"></a>Integracja tooconfirm z konsoli operacje hello
1. Witaj Otwórz konsolę programu Operations Manager i wybierz hello **administracji** obszaru roboczego.
2. Wybierz **pakietów administracyjnych** w hello **Wyszukaj:** polu tekstowym wpisz **Advisor** lub **analizy**.
3. W zależności od rozwiązania hello, które aktywowano zostanie wyświetlony odpowiedni pakiet administracyjny, w wynikach wyszukiwania hello.  Na przykład po włączeniu hello rozwiązania zarządzania alertami hello pakiet administracyjny programu Microsoft System Center Advisor alertu Management znajduje się liście hello.
4. Z hello **monitorowanie** wyświetlić, przejdź toohello **operacji zarządzania Suite\Health stanu** widoku.  Wybierz serwer zarządzania, w obszarze hello **stan serwera zarządzania** okienku w hello **: widok szczegółów** okienko potwierdzić hello wartość właściwości **adres URI usługi uwierzytelniania** zgodny z identyfikatorem hello obszarem roboczym pakietu OMS.
   
   ![OMS-OpsMgr-mg-authsvcuri-Property-MS](./media/log-analytics-om-agents/oms-opsmgr-mg-authsvcuri-property-ms.png)

## <a name="remove-integration-with-oms"></a>Usuń integrację z usługą OMS
Podczas integracji między grupą zarządzania programu Operations Manager a obszarem roboczym pakietu OMS nie są już potrzebne, istnieje kilka kroków wymaganych tooproperly Usuń hello połączenia i konfiguracji w grupie zarządzania hello. Witaj Poniższa procedura ma możesz zaktualizować obszar roboczy OMS przez usunięcie odwołania hello grupy zarządzania, Usuń hello OMS łączniki, a następnie usuń pakiety administracyjne obsługujące OMS.   

Pakiety administracyjne dla rozwiązania hello włączonego integrujące się z programem Operations Manager i hello zarządzania pakietów wymagane toosupport integracji z hello usługę nie można łatwo usunąć z grupy zarządzania hello.  Jest tak, ponieważ niektóre z pakietów administracyjnych OMS hello są zależne od innych pakietów administracyjnych pokrewne.  Pakiety administracyjne toodelete ma zależność od innych pakietów administracyjnych, Pobierz skrypt hello [Usuń pakiet administracyjny z zależnościami](https://gallery.technet.microsoft.com/scriptcenter/Script-to-remove-a-84f6873e) z Centrum skryptów w witrynie TechNet.  

1. Otwórz hello powłoka poleceń programu Operations Manager przy użyciu konta należącego do roli Administratorzy programu Operations Manager hello.
   
    > [!WARNING]
    > Upewnij się, nie masz żadnych niestandardowych pakietów administracyjnych z hello word Advisor lub IntelligencePack w nazwie hello przed kontynuowaniem, w przeciwnym razie hello następujące kroki, usunąć je z hello grupy zarządzania.
    > 

2. W wierszu polecenia powłoki poleceń hello wpisz polecenie`Get-SCOMManagementPack -name "*Advisor*" | Remove-SCOMManagementPack -ErrorAction SilentlyContinue`
3. Typ następnego`Get-SCOMManagementPack -name “*IntelligencePack*” | Remove-SCOMManagementPack -ErrorAction SilentlyContinue`
4. tooremove żadnych pakietów administracyjnych, które pozostały, które mają zależności na inne zarządzania programu System Center Advisor pakietów, użyj skryptu hello *RecursiveRemove.ps1* pobranego z Centrum skryptów w witrynie TechNet hello wcześniej.  
 
    > [!NOTE]
    > Nie należy usuwać hello Microsoft System Center Advisor lub programu Microsoft System Center Advisor wewnętrzny pakietów administracyjnych.  
    >  

5. Otwórz konsolę operacje programu Operations Manager hello przy użyciu konta należącego do roli Administratorzy programu Operations Manager hello.
6. W obszarze **administracji**, wybierz pozycję hello **pakietów administracyjnych** węzła w hello **Wyszukaj:** wpisz **Advisor** i sprawdź hello następujące pakiety administracyjne są nadal zaimportowane w grupie zarządzania:
   
   * Microsoft System Center Advisor
   * Microsoft System Center Advisor wewnętrzny
7. W portalu OMS hello, kliknij przycisk hello **ustawienia** kafelka.
8. Wybierz **połączone źródła**.
9. W tabeli hello hello sekcji System Center Operations Manager, powinna zostać wyświetlona nazwa hello grupy zarządzania hello ma tooremove z hello obszaru roboczego.  W kolumnie hello **dane o ostatniej**, kliknij przycisk **Usuń**.  
   
    > [!NOTE]
    > Witaj **Usuń** łącze nie będą dostępne dopiero po 14 dniach od Jeśli nic się nie wykryto z hello podłączonej grupy zarządzania.  
    > 

10. Zostanie wyświetlone okno z pytaniem, które mają tooproceed z usuwaniem hello tooconfirm.  Kliknij przycisk **tak** tooproceed. 

toodelete hello dwa łączniki - Microsoft.SystemCenter.Advisor.DataConnector i łącznik usługi Advisor, Zapisz skrypt programu PowerShell hello poniżej tooyour komputera i wykonywanie za pomocą hello następujące przykłady:

```
    .\OM2012_DeleteConnector.ps1 “Advisor Connector” <ManagementServerName>
    .\OM2012_DeleteConnectors.ps1 “Microsoft.SytemCenter.Advisor.DataConnector” <ManagementServerName>
```

> [!NOTE]
> Hello Uruchom ten skrypt z komputera, jeśli nie serwer zarządzania powinien mieć powłoki poleceń programu Operations Manager hello zainstalowane w zależności od wersji hello grupy zarządzania.
> 
> 

```
    `param(
    [String] $connectorName,
    [String] $msName="localhost"
    )
    $mg = new-object Microsoft.EnterpriseManagement.ManagementGroup $msName
    $admin = $mg.GetConnectorFrameworkAdministration()
    ##########################################################################################
    # Configures a connector with hello specified name.
    ##########################################################################################
    function New-Connector([String] $name)
    {
         $connectorForTest = $null;
         foreach($connector in $admin.GetMonitoringConnectors())
    {
    if($connectorName.Name -eq ${name})
    {
         $connectorForTest = Get-SCOMConnector -id $connector.id
    }
    }
    if ($connectorForTest -eq $null)
    {
         $testConnector = New-Object Microsoft.EnterpriseManagement.ConnectorFramework.ConnectorInfo
         $testConnector.Name = $name
         $testConnector.Description = "${name} Description"
         $testConnector.DiscoveryDataIsManaged = $false
         $connectorForTest = $admin.Setup($testConnector)
         $connectorForTest.Initialize();
    }
    return $connectorForTest
    }
    ##########################################################################################
    # Removes a connector with hello specified name.
    ##########################################################################################
    function Remove-Connector([String] $name)
    {
        $testConnector = $null
        foreach($connector in $admin.GetMonitoringConnectors())
       {
        if($connector.Name -eq ${name})
       {
         $testConnector = Get-SCOMConnector -id $connector.id
       }
      }
     if ($testConnector -ne $null)
     {
        if($testConnector.Initialized)
     {
     foreach($alert in $testConnector.GetMonitoringAlerts())
     {
       $alert.ConnectorId = $null;
       $alert.Update("Delete Connector");
     }
     $testConnector.Uninitialize()
     }
     $connectorIdForTest = $admin.Cleanup($testConnector)
     }
    }
    ##########################################################################################
    # Delete a connector's Subscription
    ##########################################################################################
    function Delete-Subscription([String] $name)
    {
      foreach($testconnector in $admin.GetMonitoringConnectors())
      {
      if($testconnector.Name -eq $name)
      {
        $connector = Get-SCOMConnector -id $testconnector.id
      }
    }
    $subs = $admin.GetConnectorSubscriptions()
    foreach($sub in $subs)
    {
      if($sub.MonitoringConnectorId -eq $connector.id)
      {
        $admin.DeleteConnectorSubscription($admin.GetConnectorSubscription($sub.Id))
      }
     }
    }
    #New-Connector $connectorName
    write-host "Delete-Subscription"
    Delete-Subscription $connectorName
    write-host "Remove-Connector"
    Remove-Connector $connectorName
```

W przyszłości hello Jeśli planujesz ponowne nawiązywanie połączenia z zarządzania grupy tooan obszarem roboczym pakietu OMS należy hello importu toore `Microsoft.SystemCenter.Advisor.Resources.\<Language>\.mpb` pliku pakietu administracyjnego z pakietu zbiorczego aktualizacji najnowszych hello stosowane tooyour grupy zarządzania.  Ten plik znajduje się w hello `%ProgramFiles%\Microsoft System Center 2012` lub hello `System Center 2012 R2\Operations Manager\Server\Management Packs for Update Rollups` folderu.

## <a name="next-steps"></a>Następne kroki
Funkcje tooadd i zbieranie danych, zobacz [rozwiązań analizy dzienników dodać hello galerii rozwiązań](log-analytics-add-solutions.md).


