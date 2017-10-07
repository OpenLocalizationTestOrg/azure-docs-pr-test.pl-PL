---
title: "tooAzure komputerów z systemem Windows aaaConnect Log Analytics | Dokumentacja firmy Microsoft"
description: "W tym artykule zawiera komputery Windows hello tooconnect kroki hello w Twojej toohello infrastruktury lokalnej usługi analizy dzienników przy użyciu dostosowanej wersji hello Microsoft Monitoring Agent (MMA)."
services: log-analytics
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: 932f7b8c-485c-40c1-98e3-7d4c560876d2
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/03/2017
ms.author: magoedte
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 7e15f9eeb0440bd2f6557d7215df701526e4f9aa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-windows-computers-toohello-log-analytics-service-in-azure"></a>Połączenie usługi analizy dzienników toohello komputerach systemu Windows na platformie Azure

Tym artykule przedstawiono kroki hello tooconnect komputerów z systemem Windows w lokalnych obszarach roboczych tooOMS infrastruktury przy użyciu dostosowanej wersji hello Microsoft Monitoring Agent (MMA). Należy tooinstall i połączyć agentów dla wszystkich komputerów hello, które mają tooonboard w kolejności ich toosend danych toohello analizy dzienników usługi i tooview oraz działanie tych danych. Każdy agent może raportować toomultiple obszarów roboczych.

Można zainstalować agentów przy użyciu wiersza polecenia Instalatora lub z żądanego stanu konfiguracji (DSC) w automatyzacji Azure.  

>[!NOTE]
Dla maszyn wirtualnych działających na platformie Azure, można uprościć instalacji przy użyciu hello [rozszerzenie maszyny wirtualnej](log-analytics-azure-vm-extension.md).

Na komputerach z połączeniem internetowym hello agent używa hello połączenia toohello Internet toosend danych tooOMS. Dla komputerów, które nie ma łączności z Internetem, można użyć serwera proxy lub hello [bramy OMS](log-analytics-oms-gateway.md).

Łączenie tooOMS komputerów z systemem Windows jest proste, przy użyciu trzech prostych kroków:

1. Pobierz plik Instalatora agenta hello z hello portalu OMS
2. Zainstaluj agenta hello przy użyciu wybranej metody hello
3. Skonfiguruj agenta hello lub Dodaj dodatkowe obszary robocze, w razie potrzeby

Witaj Poniższy diagram przedstawia hello relacji między komputerami z systemem Windows i pakietu OMS po zainstalowaniu i skonfigurować agentów.

![OMS — direct — agent — diagram](./media/log-analytics-windows-agents/oms-direct-agent-diagram.png)

Jeśli zasady zabezpieczeń IT nie zezwalają na toohello tooconnect Twojego sieci Internet komputerów, można skonfigurować Twoje komputery tooconnect toohello OMS bramy. Aby uzyskać więcej informacji i kroki na tooconfigure Twojego toocommunicate serwerami za pośrednictwem bramy OMS toohello usługę, zobacz temat [połączyć tooOMS komputerów przy użyciu hello bramy OMS](log-analytics-oms-gateway.md).

## <a name="system-requirements-and-required-configuration"></a>Wymagania systemowe i wymaganej konfiguracji
Przed zainstalowaniem lub wdrożyć agentów, przejrzyj następujące szczegóły tooensure wymagań hello hello.

- Witaj OMS MMA można zainstalować tylko na komputerach z systemem Windows Server 2008 z dodatkiem SP 1 lub nowszym lub Windows 7 z dodatkiem SP1 lub nowszym.
- Potrzebujesz subskrypcji platformy Azure.  Aby uzyskać więcej informacji, zobacz [wprowadzenie do analizy dzienników](log-analytics-get-started.md).
- Każdy komputer z systemem Windows musi być w stanie tooconnect toohello Internet przy użyciu protokołu HTTPS lub toohello OMS bramy. To połączenie może być bezpośrednio, za pośrednictwem serwera proxy lub za pośrednictwem hello OMS bramy.
- Witaj OMS MMA można zainstalować na komputerach autonomicznych, serwerów i maszyn wirtualnych. Jeśli tooconnect tooOMS maszynami wirtualnymi hostowanymi na platformie Azure, zobacz [tooLog maszyny wirtualne Azure połączyć Analytics](log-analytics-azure-vm-extension.md).
- Hello agent wymaga toouse TCP port 443 dla różnych zasobów.

### <a name="network"></a>Sieć

Tooand tooconnect rejestru systemu Windows agentów z usługą OMS hello muszą mieć dostęp do zasobów toonetwork, w tym adresy URL domeny i numery portów hello.

- W przypadku serwerów proxy należy tooensure, który hello serwera proxy odpowiednie, zasoby są konfigurowane w ustawieniach agenta.
- Dla zapór, które ograniczają dostęp toohello Internet Twojej sieci inżynierów potrzebować tooconfigure Twojego tooOMS dostępu toopermit zapory. W ustawieniach agenta nie jest wymagana żadna akcja.

Witaj w poniższej tabeli przedstawiono zasoby wymagane do komunikacji.

>[!NOTE]
>Niektóre hello następujące zasoby wspomina Operational Insights, który został poprzednia nazwa protokołu analizy dzienników.

| Zasób agenta | Porty | Obejście inspekcji HTTPS |
|---|---|---|
| *.ods.opinsights.azure.com | 443 | Tak |
| *.oms.opinsights.azure.com | 443 | Tak |
| *.blob.core.windows.net | 443 | Tak |
| *.azure-automation.net | 443 | Tak |



## <a name="download-hello-agent-setup-file-from-oms"></a>Pobierz plik Instalatora agenta hello z usługą OMS
1. W portalu OMS hello na powitania **omówienie** kliknij przycisk hello **ustawienia** kafelka.  Kliknij przycisk hello **połączonych źródeł** u góry hello.  
    ![Połączone kartę źródła](./media/log-analytics-windows-agents/oms-direct-agent-connected-sources.png)
2. Kliknij przycisk **serwerów z systemem Windows** , a następnie kliknij przycisk **Pobierz agenta systemu Windows** procesora komputera dotyczy tooyour typ pliku Instalatora hello toodownload.
3. Na powitania po prawej **identyfikator obszaru roboczego**, kliknij ikonę kopiowania hello i wklej identyfikator hello do Notatnika.
4. Na powitania po prawej **klucz podstawowy**, kliknij ikonę kopiowania hello i Wklej klucz hello do Notatnika.     

## <a name="install-hello-agent-using-setup"></a>Instalowanie agenta hello za pomocą Instalatora
1. Należy uruchomić Instalator tooinstall hello agenta na komputerze, które mają toomanage.
2. Na stronie powitalnej powitania kliknij **dalej**.
3. Na stronie powitania postanowienia licencyjne przeczytaj hello licencji, a następnie kliknij przycisk **zgadzam się**.
4. Na stronie powitania, Folder docelowy, zmienić lub zachować hello domyślny folder instalacji, a następnie kliknij przycisk **dalej**.
5. Na stronie Opcje instalacji agenta hello można wybrać tooconnect hello agenta tooAzure analizy dzienników (OMS) programu Operations Manager lub puste opcje hello jeśli agenci mają przechodzić tooconfigure hello później. Kliknij przycisk **Dalej**.   
    - W przypadku wybrania tooAzure tooconnect analizy dzienników (OMS) Wklej hello **identyfikator obszaru roboczego** i **klucz obszaru roboczego (klucz podstawowy)** , który został skopiowany do Notatnika w poprzedniej procedurze hello, a następnie kliknij przycisk  **Następny**.  
        ![Wklej klucz podstawowy i identyfikator obszaru roboczego](./media/log-analytics-windows-agents/connect-workspace.png)
    - W przypadku wybrania tooconnect tooOperations Manager wpisz hello **Nazwa grupy zarządzania**, **serwera zarządzania** nazwa, i **Port serwera zarządzania**, a następnie kliknij przycisk **Dalej**. Na stronie konto akcji agenta hello wybierz hello lokalne konto systemowe lub konto domeny lokalnych, a następnie kliknij przycisk **dalej**.  
        ![Konfiguracja grupy zarządzania](./media/log-analytics-windows-agents/oms-mma-om-setup01.png)![konto akcji agenta](./media/log-analytics-windows-agents/oms-mma-om-setup02.png)

6. Na stronie gotowe tooInstall hello, przejrzyj wybrane opcje, a następnie kliknij przycisk **zainstalować**.
7. Na powitania konfiguracji została ukończona pomyślnie kliknij pozycję **Zakończ**.
8. Po zakończeniu hello **programu Microsoft Monitoring Agent** pojawia się w **Panelu sterowania**. Można sprawdzić konfigurację istnieje i sprawdź, czy hello agent jest połączonych tooOperational Insights (OMS). Gdy hello połączonych tooOMS agenta wyświetla komunikat z informacją: **hello Microsoft Monitoring Agent pomyślnie nawiązało połączenie toohello usługi programu Microsoft Operations Management Suite.**

## <a name="configure-proxy-settings"></a>Skonfiguruj ustawienia serwera proxy

Możesz użyć hello następujące ustawienia serwera proxy tooconfigure procedury dla hello za pomocą Panelu sterowania agenta monitorowania firmy Microsoft. Należy toouse tę procedurę dla każdego serwera. Jeśli masz wiele serwerów należy tooconfigure, może być łatwiejsze toouse tooautomate skrypt tego procesu. Jeśli tak, zobacz następną procedurę hello [tooconfigure ustawienia serwera proxy dla hello Microsoft Monitoring Agent za pomocą skryptu](#to-configure-proxy-settings-for-the-microsoft-monitoring-agent-using-a-script).

### <a name="tooconfigure-proxy-settings-for-hello-microsoft-monitoring-agent-using-control-panel"></a>ustawienia serwera proxy tooconfigure hello za pomocą Panelu sterowania agenta monitorowania firmy Microsoft
1. Otwórz **Panel sterowania**.
2. Otwórz program **Microsoft Monitoring Agent**.
3. Kliknij przycisk hello **ustawienia serwera Proxy** kartę.  
    ![karta Ustawienia serwera proxy](./media/log-analytics-windows-agents/proxy-direct-agent-proxy.png)
4. Wybierz **Użyj serwera proxy** i wpisz hello adres URL i numer portu, jeśli jest wymagane, podobne toohello przykładzie. Jeśli serwer proxy wymaga uwierzytelniania, wpisz hello nazwy użytkownika i hasła tooaccess powitania serwera proxy.


### <a name="verify-agent-connectivity-toooms"></a>Sprawdź tooOMS łączności agenta

Można łatwo sprawdzić, czy agentów komunikują się z OMS przy użyciu hello następujące procedury:

1.  Na komputerze hello z agentem systemu Windows hello Otwórz Panel sterowania.
2.  Otwórz program Microsoft Monitoring Agent.
3.  Kliknij kartę Analiza dzienników Azure (OMS) hello.
4.  W kolumnie Stan hello powinny pojawić się, że hello agent Połączono pomyślnie toohello usługi Operations Management Suite.

![Agent połączone](./media/log-analytics-windows-agents/mma-connected.png)


### <a name="tooconfigure-proxy-settings-for-hello-microsoft-monitoring-agent-using-a-script"></a>ustawienia serwera proxy tooconfigure hello Microsoft Monitoring Agent za pomocą skryptu
Skopiuj hello następujące przykładowe, zaktualizowania go ze środowiska tooyour określonych informacji, Zapisz plik z rozszerzeniem nazwy pliku PS1, a następnie uruchom skrypt hello na każdym komputerze, który łączy się bezpośrednio toohello usługę.

    param($ProxyDomainName="http://proxy.contoso.com:80", $cred=(Get-Credential))

    # First we get hello Health Service configuration object.  We need toodetermine if we
    #have hello right update rollup with hello API we need.  If not, no need toorun hello rest of hello script.
    $healthServiceSettings = New-Object -ComObject 'AgentConfigManager.MgmtSvcCfg'

    $proxyMethod = $healthServiceSettings | Get-Member -Name 'SetProxyInfo'

    if (!$proxyMethod)
    {
         Write-Output 'Health Service proxy API not present, will not update settings.'
         return
    }

    Write-Output "Clearing proxy settings."
    $healthServiceSettings.SetProxyInfo('', '', '')

    $ProxyUserName = $cred.username

    Write-Output "Setting proxy too$ProxyDomainName with proxy username $ProxyUserName."
    $healthServiceSettings.SetProxyInfo($ProxyDomainName, $ProxyUserName, $cred.GetNetworkCredential().password)



## <a name="install-hello-agent-using-hello-command-line"></a>Instalowanie agenta hello za pomocą wiersza polecenia hello
- Modyfikowanie, a następnie użyj następującego agenta hello tooinstall przykład przy użyciu wiersza polecenia hello hello. przykład Witaj wykonanie pełni dyskretnej instalacji.

    >[!NOTE]
    Jeśli chcesz tooupgrade agenta należy hello toouse analizy dzienników interfejs API obsługi skryptów. Zobacz hello następnej sekcji tooupgrade agenta.

    ```dos
    MMASetup-AMD64.exe /Q:A /R:N /C:"setup.exe /qn ADD_OPINSIGHTS_WORKSPACE=1 OPINSIGHTS_WORKSPACE_ID=<your workspace id> OPINSIGHTS_WORKSPACE_KEY=<your workspace key> AcceptEndUserLicenseAgreement=1"
    ```

Hello agent używa IExpress jako jego samorozpakowujący się plik typu przy użyciu hello `/c` polecenia. Widać hello przełączniki wiersza polecenia w [przełączniki wiersza polecenia dla IExpress](https://support.microsoft.com/help/197147/command-line-switches-for-iexpress-software-update-packages) , a następnie aktualizację hello toosuit przykład potrzeb.

|Opcje MMA                   |Uwagi         |
|---------------------------------------|--------------|
|ADD_OPINSIGHTS_WORKSPACE               | 1 = obszar roboczy tooa tooreport Konfiguruj hello agenta                |
|OPINSIGHTS_WORKSPACE_ID                | Identyfikator obszaru roboczego (guid) dla hello tooadd obszaru roboczego                    |
|OPINSIGHTS_WORKSPACE_KEY               | Obszar roboczy klucza tooinitially używane uwierzytelniania za pomocą obszaru roboczego hello |
|OPINSIGHTS_WORKSPACE_AZURE_CLOUD_TYPE  | Określ hello środowiska chmury, gdzie znajduje się obszar roboczy hello <br> 0 = komercyjnych chmury azure (ustawienie domyślne) <br> 1 = azure dla instytucji rządowych |
|OPINSIGHTS_PROXY_URL               | Identyfikator URI dla hello toouse serwera proxy |
|OPINSIGHTS_PROXY_USERNAME               | Nazwa użytkownika tooaccess uwierzytelnionego serwera proxy |
|OPINSIGHTS_PROXY_PASSWORD               | Hasło tooaccess uwierzytelnionego serwera proxy |

>[!NOTE]
tooavoid naciśnięcie hello wiersza polecenia limit długości IExpress, zainstaluj hello agenta z obszarem roboczym, nie skonfigurowany, a następnie użyj konfigurację tooset skryptu hello obszaru roboczego.

>[!NOTE]
Jeśli otrzymasz `Command line option syntax error.` przy użyciu hello `OPINSIGHTS_WORKSPACE_AZURE_CLOUD_TYPE` parametru, można użyć hello następujące rozwiązania:
```dos
MMASetup-AMD64.exe /C /T:.\MMAExtract
cd .\MMAExtract
setup.exe /qn ADD_OPINSIGHTS_WORKSPACE=1 OPINSIGHTS_WORKSPACE_AZURE_CLOUD_TYPE=1 OPINSIGHTS_WORKSPACE_ID=<your workspace id> OPINSIGHTS_WORKSPACE_KEY=<your workspace key> AcceptEndUserLicenseAgreement=1
```

## <a name="add-a-workspace-using-a-script"></a>Dodaj obszar roboczy za pomocą skryptu
Dodaj obszar roboczy przy użyciu interfejsu API hello analizy dzienników agenta skryptów z hello poniższy przykład:

```PowerShell
$mma = New-Object -ComObject 'AgentConfigManager.MgmtSvcCfg'
$mma.AddCloudWorkspace($workspaceId, $workspaceKey)
$mma.ReloadConfiguration()
```

tooadd obszaru roboczego platformy Azure dla instytucji rządowych Stanów Zjednoczonych, użyj powitania po przykładowym skrypcie:
```PowerShell
$mma = New-Object -ComObject 'AgentConfigManager.MgmtSvcCfg'
$mma.AddCloudWorkspace($workspaceId, $workspaceKey, 1)
$mma.ReloadConfiguration()
```

>[!NOTE]
Jeśli używano hello wiersza polecenia lub skryptu wcześniej tooinstall lub skonfigurować agenta hello `EnableAzureOperationalInsights` została zastąpiona `AddCloudWorkspace`.

## <a name="install-hello-agent-using-dsc-in-azure-automation"></a>Zainstaluj agenta hello przy użyciu usługi Konfiguracja DSC automatyzacji Azure

Możesz użyć hello następującego skryptu przykład tooinstall hello agenta przy użyciu usługi Konfiguracja DSC automatyzacji Azure. przykład Witaj instaluje hello agent 64-bitowe, zidentyfikowane przez hello `URI` wartość. Umożliwia także hello 32-bitowej wersji zastępując hello wartość identyfikatora URI. Witaj identyfikatorów URI dla obu wersji są:

- Agent 64-bitowego systemu Windows — https://go.microsoft.com/fwlink/?LinkId=828603
- Agent 32-bitowego systemu Windows — https://go.microsoft.com/fwlink/?LinkId=828604


>[!NOTE]
W tym przykładzie procedury i skrypt nie spowoduje uaktualnienie istniejącego agenta.

1. Importuj xPSDesiredStateConfiguration hello DSC modułu z [http://www.powershellgallery.com/packages/xPSDesiredStateConfiguration](http://www.powershellgallery.com/packages/xPSDesiredStateConfiguration) w automatyzacji Azure.  
2.  Tworzenie zasobów zmiennej usługi Automatyzacja Azure *OPSINSIGHTS_WS_ID* i *OPSINSIGHTS_WS_KEY*. Ustaw *OPSINSIGHTS_WS_ID* identyfikator obszaru roboczego analizy dzienników OMS tooyour i ustaw *OPSINSIGHTS_WS_KEY* toohello klucza podstawowego obszaru roboczego.
3.  Użyj hello następujący skrypt i zapisać go jako MMAgent.ps1
4.  Modyfikuj, a następnie użyj powitania po agenta hello tooinstall przykład przy użyciu usługi Konfiguracja DSC automatyzacji Azure. Zaimportuj MMAgent.ps1 do automatyzacji Azure przy użyciu interfejsu usługi Automatyzacja Azure hello lub polecenia cmdlet.
5.  Przypisywanie konfiguracji toohello węzła. W ciągu 15 minut węzeł hello sprawdza konfigurację i hello MMA spoczywa toohello węzła.

```PowerShell
Configuration MMAgent
{
    $OIPackageLocalPath = "C:\MMASetup-AMD64.exe"
    $OPSINSIGHTS_WS_ID = Get-AutomationVariable -Name "OPSINSIGHTS_WS_ID"
    $OPSINSIGHTS_WS_KEY = Get-AutomationVariable -Name "OPSINSIGHTS_WS_KEY"


    Import-DscResource -ModuleName xPSDesiredStateConfiguration

    Node OMSnode {
        Service OIService
        {
            Name = "HealthService"
            State = "Running"
            DependsOn = "[Package]OI"
        }

        xRemoteFile OIPackage {
            Uri = "https://go.microsoft.com/fwlink/?LinkId=828603"
            DestinationPath = $OIPackageLocalPath
        }

        Package OI {
            Ensure = "Present"
            Path  = $OIPackageLocalPath
            Name = "Microsoft Monitoring Agent"
            ProductId = "8A7F2C51-4C7D-4BFD-9014-91D11F24AAE2"
            Arguments = '/C:"setup.exe /qn ADD_OPINSIGHTS_WORKSPACE=1 OPINSIGHTS_WORKSPACE_ID=' + $OPSINSIGHTS_WS_ID + ' OPINSIGHTS_WORKSPACE_KEY=' + $OPSINSIGHTS_WS_KEY + ' AcceptEndUserLicenseAgreement=1"'
            DependsOn = "[xRemoteFile]OIPackage"
        }
    }
}


```

### <a name="get-hello-latest-productid-value"></a>Pobierz najnowszą wartość ProductId hello

Witaj `ProductId value` w hello MMAgent.ps1 skryptów jest unikatowy tooeach wersja agenta. Po opublikowaniu zaktualizowaną wersję każdego agenta hello wartość ProductId zmiany. Tak po zmianie w przyszłych hello hello ProductId można znaleźć wersji agenta hello za pomocą prostego skryptu. Po umieszczeniu hello najnowszą wersję agenta zainstalowana na serwerze testowym, można użyć hello następującego skryptu tooget hello zainstalowany ProductId wartość. Za pomocą najnowszej wartości ProductId hello, można zaktualizować wartości hello hello MMAgent.ps1 skryptu.

```PowerShell
$InstalledApplications  = Get-ChildItem hklm:\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall


foreach ($Application in $InstalledApplications)

{

     $Key = Get-ItemProperty $Application.PSPath

     if ($Key.DisplayName -eq "Microsoft Monitoring Agent")

     {

        $Key.DisplayName

        Write-Output ("Product ID is: " + $Key.PSChildName.Substring(1,$Key.PSChildName.Length -2))

     }

}  
```

## <a name="configure-an-agent-manually-or-add-additional-workspaces"></a>Ręcznie skonfigurować agenta, lub Dodaj dodatkowe obszary robocze
Jeśli po zainstalowaniu agentów, ale ich nie skonfigurowano lub jeśli użytkownik chce hello agenta tooreport toomultiple w obszary robocze, możesz użyć hello następujące informacje tooenable agenta lub ponownej konfiguracji. Po skonfigurowaniu hello agent, będą rejestrować się z usługą agenta hello i niezbędnych informacji konfiguracyjnych oraz pakietów administracyjnych, które zawierają informacje o rozwiązaniu.

1. Po zainstalowaniu programu Microsoft Monitoring Agent hello Otwórz **Panelu sterowania**.
2. Otwórz **programu Microsoft Monitoring Agent** , a następnie kliknij przycisk hello **Analiza dzienników Azure (OMS)** kartę.   
3. Kliknij przycisk **Dodaj** tooopen hello **Dodaj obszar roboczy analizy dzienników** pole.
4. Wklej hello **identyfikator obszaru roboczego** i **klucz obszaru roboczego (klucz podstawowy)** skopiowane do Notatnika w poprzedniej procedurze hello obszaru roboczego, mają tooadd, a następnie kliknij przycisk **OK**.  
    ![Konfigurowanie usługi Operational Insights](./media/log-analytics-windows-agents/add-workspace.png)

Po zebraniu danych z komputerów monitorowanych przez agenta hello, hello liczbę komputerów monitorowanych przez OMS będą wyświetlane w portalu OMS hello na powitania **połączonych źródeł** karcie **ustawienia** jako  **Serwery połączone**.


## <a name="toodisable-an-agent"></a>toodisable agenta
1. Po zainstalowaniu agenta hello, otwórz **Panelu sterowania**.
2. Otwórz program Microsoft Monitoring Agent, a następnie kliknij przycisk hello **Analiza dzienników Azure (OMS)** kartę.
3. Wybierz obszar roboczy, a następnie kliknij przycisk **Usuń**. Powtórz ten krok dla wszystkich innych obszarów roboczych.


## <a name="optionally-configure-agents-tooreport-tooan-operations-manager-management-group"></a>Opcjonalnie możesz skonfigurować grupy zarządzania programu Operations Manager tooan tooreport agentów

Jeśli używasz programu Operations Manager w infrastrukturze IT, umożliwia także hello MMA agent jako agent programu Operations Manager.

### <a name="tooconfigure-mma-agents-tooreport-tooan-operations-manager-management-group"></a>Grupa zarządzania programu Operations Manager tooan tooreport tooconfigure MMA agentów
1.  Witaj gdzie hello agent jest zainstalowany, Otwórz na komputerze **Panelu sterowania**.  
2.  Otwórz **programu Microsoft Monitoring Agent** , a następnie kliknij przycisk hello **programu Operations Manager** kartę.  
    ![Karta Microsoft Monitoring Agent programu Operations Manager](./media/log-analytics-windows-agents/om-mg01.png)
3.  Jeśli serwery programu Operations Manager są zintegrowane z usługą Active Directory, kliknij przycisk **automatycznie Aktualizuj przypisania grupy zarządzania z usług AD DS**.
4.  Kliknij przycisk **Dodaj** tooopen hello **Dodaj grupę zarządzania** okno dialogowe.  
    ![Program Microsoft Monitoring Agent Dodaj grupę zarządzania](./media/log-analytics-windows-agents/oms-mma-om02.png)
5.  W **Nazwa grupy zarządzania** okno, nazwa typu hello grupy zarządzania.
6.  W hello **podstawowego serwera zarządzania** okno, wpisz nazwę komputera hello z hello podstawowego serwera zarządzania.
7.  W hello **port serwera zarządzania** wpisz numer portu TCP hello typu.
8.  W obszarze **konto akcji agenta**, wybierz hello lokalne konto systemowe lub konto domeny lokalnych.
9.  Kliknij przycisk **OK** tooclose hello **Dodaj grupę zarządzania** okno dialogowe, a następnie kliknij przycisk **OK** tooclose hello **właściwości agenta monitorowania firmy Microsoft**okno dialogowe.


## <a name="next-steps"></a>Następne kroki

- [Dodawanie rozwiązania analizy dzienników z galerii rozwiązań hello](log-analytics-add-solutions.md) tooadd funkcjonalność i zbieranie danych.
