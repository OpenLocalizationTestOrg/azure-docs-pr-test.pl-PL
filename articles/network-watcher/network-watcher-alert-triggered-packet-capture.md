---
title: "aktywne toodo przechwytywania pakietów aaaUse sieci, monitorowanie za pomocą alertów i usługi Azure Functions | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak toocreate alert wyzwolony przechwytywania pakietów z obserwatora sieciowego Azure"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 75e6e7c4-b3ba-4173-8815-b00d7d824e11
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 4722a831f3a9d5537c0e6f53daba4dfc35d0cf24
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-packet-capture-for-proactive-network-monitoring-with-alerts-and-azure-functions"></a>Użyj przechwytywania pakietów dla sieci aktywnego monitorowania za pomocą alertów i usługi Azure Functions

Przechwytywania pakietów obserwatora sieciowego tworzy sesji przechwytywania tootrack ruch do i z maszyn wirtualnych. Witaj pliku przechwytywania może mieć zdefiniowany filtr tootrack hello tylko ruchu, które mają toomonitor. Dane te są następnie przechowywane w obiekcie blob magazynu lub lokalnie na maszynie gościa hello.

Ta funkcja może być uruchomiona zdalnie na inne scenariusze automatyzacji, takich jak usługi Azure Functions. Zapewnia przechwytywania pakietów hello możliwości toorun aktywnego przechwytywania na podstawie zdefiniowanych anomalii sieci. Innych celów obejmują zbieranie statystyk sieciowych, pobieranie informacji na temat sieci atakami, debugowania komunikacja klient serwer i inne.

Zasoby, które są wdrażane na platformie Azure Uruchom 24/7. Możesz i pracownicy działu aktywnie nie można monitorować stan hello wszystkich zasobów 24/7. Na przykład co się stanie, jeśli wystąpi problem w 2 AM?

Dzięki użyciu obserwatora sieciowego, alerty i funkcji w ramach hello ekosystemu platformy Azure aktywne mogą odpowiadać hello danych i narzędzia toosolve problemów w sieci.

![Scenariusz][scenario]

## <a name="prerequisites"></a>Wymagania wstępne

* Witaj najnowszą wersję [programu Azure PowerShell](/powershell/azure/install-azurerm-ps).
* Istniejące wystąpienie obserwatora sieciowego. Jeśli nie masz już konto, [utworzyć wystąpienia obserwatora sieciowego](network-watcher-create.md).
* Istniejącej maszyny wirtualnej w hello tego samego regionu obserwatora sieciowego z hello [rozszerzenie systemu Windows](../virtual-machines/windows/extensions-nwa.md) lub [rozszerzenie maszyny wirtualnej systemu Linux](../virtual-machines/linux/extensions-nwa.md).

## <a name="scenario"></a>Scenariusz

W tym przykładzie maszyna wirtualna wysyła więcej segmentów TCP niż zwykle, i chcesz toobe alerty. Segmentów TCP są używane jako w tym przykładzie, ale można użyć dowolnego warunku alertu.

Po wyświetleniu powiadomienia, ma tooreceive toounderstand danych na poziomie pakietów, dlaczego wzrosło komunikacji. Następnie możesz wykonać czynności tooreturn hello maszyny wirtualnej tooregular komunikacji.

W tym scenariuszu założono, że istniejące wystąpienie programu obserwatora sieciowego i grupy zasobów z prawidłową maszyną wirtualną.

następujące listy Hello znajduje się przegląd hello przepływu pracy, który ma miejsce:

1. Alert zostanie wywołany na maszynie Wirtualnej.
1. Hello alert wywołania funkcji platformy Azure za pomocą elementu webhook.
1. Funkcja Azure przetwarza hello alert i uruchamia sesję przechwytywania pakietów obserwatora sieciowego.
1. przechwytywania pakietów Hello jest uruchamiany na powitania maszyny Wirtualnej i zbiera ruchu.
1. Witaj pliku przechwytywania pakietów jest przekazywany tooa konta magazynu do przeglądu i diagnostyki.

tooautomate ten proces, możemy utworzyć i na naszych tootrigger maszyny Wirtualnej połączenie alert, gdy wystąpi zdarzenie hello. Możemy również utworzyć toocall funkcji do obserwatora sieciowego.

W tym scenariuszu hello następujące:

* Tworzy funkcję platformy Azure, która rozpoczyna się przechwytywania pakietów.
* Tworzy regułę alertu na maszynie wirtualnej i konfiguruje hello reguły alertu toocall hello funkcji platformy Azure.

## <a name="create-an-azure-function"></a>Tworzenie funkcji platformy Azure

pierwszym krokiem Hello toocreate alert hello tooprocess funkcji platformy Azure i utworzyć przechwytywania pakietów.

1. W hello [portalu Azure](https://portal.azure.com), wybierz pozycję **nowy** > **obliczeniowe** > **aplikacji funkcji**.

    ![Tworzenie aplikacji — funkcja][1-1]

2. Na powitania **aplikacji funkcji** bloku, wprowadź następujące wartości hello, a następnie wybierz **OK** aplikacji hello toocreate:

    |**Ustawienie** | **Wartość** | **Szczegóły** |
    |---|---|---|
    |**Nazwa aplikacji**|PacketCaptureExample|Nazwa Hello hello funkcji aplikacji.|
    |**Subskrypcja**|[Subskrypcji] hello subskrypcji dla aplikacji funkcja hello toocreate.||
    |**Grupa zasobów**|PacketCaptureRG|Witaj zasobów grupy toocontain hello funkcji aplikacji.|
    |**Plan hostingu**|Użycie planu| Typ Hello planowanie używany przez funkcję aplikacji. Dostępne opcje to zużycie lub plan usługi aplikacji Azure. |
    |**Lokalizacja**|Środkowe stany USA| region Hello toocreate hello funkcji aplikacji.|
    |**Konto magazynu**|{automatycznie wygenerowaną}| Konto magazynu Hello Azure Functions potrzeb magazynu ogólnego przeznaczenia.|

3. Na powitania **aplikacji funkcji PacketCaptureExample** bloku, wybierz opcję **funkcje** > **Niestandardowa funkcja**  >  **+**.

4. Wybierz **HttpTrigger Powershell**, a następnie wprowadź hello pozostałe informacje. Na koniec toocreate hello funkcji, wybierz opcję **Utwórz**.

    |**Ustawienie** | **Wartość** | **Szczegóły** |
    |---|---|---|
    |**Scenariusz**|Eksperymentalne|Scenariusz|
    |**Nazwa funkcji**|AlertPacketCapturePowerShell|Nazwa funkcji hello|
    |**Poziom dostępu**|Funkcja|Poziom dostępu dla hello — funkcja|

![Przykład funkcji][functions1]

> [!NOTE]
> Szablon programu PowerShell Hello jest eksperymentalna i nie ma pełnej obsługi.

Dostosowania są wymagane w ramach tego przykładu i opisano szczegółowo w hello następujące kroki.

### <a name="add-modules"></a>Dodawanie modułów

toouse poleceń cmdlet programu PowerShell obserwatora sieciowego, przekazać hello najnowsze PowerShell modułu toohello funkcja aplikację.

1. Na komputerze lokalnym hello zainstalowane najnowsze modułów programu Azure PowerShell uruchom następujące polecenia programu PowerShell hello:

    ```powershell
    (Get-Module AzureRM.Network).Path
    ```

    Dzięki temu przykład Witaj ścieżki lokalnej z modułów programu Azure PowerShell. Te foldery są używane w kolejnym kroku. Moduły Hello, które są używane w tym scenariuszu są:

    * AzureRM.Network

    * AzureRM.Profile

    * AzureRM.Resources

    ![Foldery programu PowerShell][functions5]

1. Wybierz **funkcji ustawienia aplikacji** > **Przejdź tooApp Edytor usługi**.

    ![Ustawienia aplikacji — funkcja][functions2]

1. Kliknij prawym przyciskiem myszy hello **AlertPacketCapturePowershell** folder, a następnie utwórz folder o nazwie **azuremodules**. 

4. Utwórz podfolder dla poszczególnych modułów, które są potrzebne.

    ![Folderze i jego podfolderach][functions3]

    * AzureRM.Network

    * AzureRM.Profile

    * AzureRM.Resources

1. Kliknij prawym przyciskiem myszy hello **AzureRM.Network** podfolder, a następnie wybierz **Przekaż**. 

6. Przejdź tooyour Azure modułów. W lokalnej hello **AzureRM.Network** folderu, wybierz wszystkie pliki hello w folderze hello. Następnie wybierz **OK**. 

7. Powtórz te kroki dla **AzureRM.Profile** i **AzureRM.Resources**.

    ![Przekazywanie plików][functions6]

1. Po zakończeniu, każdy folder powinien mieć hello pliki modułu programu PowerShell z komputera lokalnego.

    ![Pliki środowiska PowerShell][functions7]

### <a name="authentication"></a>Authentication

polecenia cmdlet programu PowerShell hello toouse, wymagane jest uwierzytelnienie. Możesz skonfigurować uwierzytelnianie w hello funkcji aplikacji. tooconfigure uwierzytelniania, należy skonfigurować zmienne środowiskowe i przekazać aplikację funkcja toohello zaszyfrowanego pliku klucza.

> [!NOTE]
> Ten scenariusz zawiera tylko jeden przykład jak tooimplement uwierzytelniania za pomocą usługi Azure Functions. Istnieją inne sposoby toodo to.

#### <a name="encrypted-credentials"></a>Zaszyfrowane poświadczenia

Witaj następującego skryptu programu PowerShell tworzy plik klucza o nazwie **PassEncryptKey.key**. Umożliwia także zaszyfrowana wersja hello hasła, które jest dostarczone. To hasło jest hello tego samego hasła, który jest zdefiniowany dla aplikacji usługi Azure Active Directory hello, który jest używany do uwierzytelniania.

```powershell
#Variables
$keypath = "C:\temp\PassEncryptKey.key"
$AESKey = New-Object Byte[] 32
$Password = "<insert a password here>"

#Keys
[Security.Cryptography.RNGCryptoServiceProvider]::Create().GetBytes($AESKey) 
Set-Content $keypath $AESKey

#Get encrypted password
$secPw = ConvertTo-SecureString -AsPlainText $Password -Force
$AESKey = Get-content $KeyPath
$Encryptedpassword = $secPw | ConvertFrom-SecureString -Key $AESKey
$Encryptedpassword
```

W hello Edytor usług aplikacji hello funkcji aplikacji, Utwórz folder o nazwie **klucze** w obszarze **AlertPacketCapturePowerShell**. Następnie przekaż hello **PassEncryptKey.key** pliku, który został utworzony w hello powyższego przykładu środowiska PowerShell.

![Funkcje klucza][functions8]

### <a name="retrieve-values-for-environment-variables"></a>Pobieranie wartości zmiennych środowiskowych

wymaganie końcowego Hello jest tooset się hello zmiennych środowiskowych, które są niezbędne tooaccess hello wartości dla uwierzytelniania. Witaj poniższej liście przedstawiono hello zmiennych środowiskowych, które są tworzone:

* AzureClientID

* AzureTenant

* AzureCredPassword


#### <a name="azureclientid"></a>AzureClientID

Identyfikator klienta Hello jest hello identyfikator aplikacji w usłudze Azure Active Directory.

1. Jeśli nie masz jeszcze toouse aplikacji, należy uruchomić powitania po toocreate przykład aplikację.

    ```powershell
    $app = New-AzureRmADApplication -DisplayName "ExampleAutomationAccount_MF" -HomePage "https://exampleapp.com" -IdentifierUris "https://exampleapp1.com/ExampleFunctionsAccount" -Password "<same password as defined earlier>"
    New-AzureRmADServicePrincipal -ApplicationId $app.ApplicationId
    Start-Sleep 15
    New-AzureRmRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $app.ApplicationId
    ```

   > [!NOTE]
   > hasło Hello, który jest używany podczas tworzenia aplikacji hello powinna być hello tego samego hasła utworzonego wcześniej podczas zapisywania pliku klucza hello.

1. Hello portalu Azure, wybierz **subskrypcje**. Wybierz hello toouse subskrypcji, a następnie wybierz **(IAM) kontroli dostępu**.

    ![Funkcje IAM][functions9]

1. Wybierz hello toouse konta, a następnie wybierz **właściwości**. Skopiuj hello identyfikator aplikacji.

    ![Identyfikator aplikacji funkcji][functions10]

#### <a name="azuretenant"></a>AzureTenant

Uzyskaj identyfikator dzierżawcy hello uruchamiając hello następujące przykładowe środowiska PowerShell:

```powershell
(Get-AzureRmSubscription -SubscriptionName "<subscriptionName>").TenantId
```

#### <a name="azurecredpassword"></a>AzureCredPassword

Witaj wartości zmiennej środowiskowej AzureCredPassword hello jest wartość hello, który można pobrać z systemem hello następujące przykładowe programu PowerShell. W tym przykładzie jest hello sam, co przedstawiono w poprzednim hello **zaszyfrowane poświadczenia** sekcji. Witaj wartość, która jest potrzebna jest wyjściem hello hello `$Encryptedpassword` zmiennej.  To jest hello usługi głównej hasło szyfrowane przy użyciu skryptu PowerShell hello.

```powershell
#Variables
$keypath = "C:\temp\PassEncryptKey.key"
$AESKey = New-Object Byte[] 32
$Password = "<insert a password here>"

#Keys
[Security.Cryptography.RNGCryptoServiceProvider]::Create().GetBytes($AESKey) 
Set-Content $keypath $AESKey

#Get encrypted password
$secPw = ConvertTo-SecureString -AsPlainText $Password -Force
$AESKey = Get-content $KeyPath
$Encryptedpassword = $secPw | ConvertFrom-SecureString -Key $AESKey
$Encryptedpassword
```

### <a name="store-hello-environment-variables"></a>Zmienne środowiskowe hello magazynu

1. Przejdź toohello funkcji aplikacji. Następnie wybierz **funkcji ustawienia aplikacji** > **Konfiguruj ustawienia aplikacji**.

    ![Konfigurowanie ustawień aplikacji][functions11]

1. Dodaj hello zmienne środowiskowe i ich ustawienia aplikacji toohello wartości, a następnie wybierz **zapisać**.

    ![Ustawienia aplikacji][functions12]

### <a name="add-powershell-toohello-function"></a>Dodawanie funkcji toohello programu PowerShell

Jest teraz toomake czasu wywołuje obserwatora sieciowego z wewnątrz hello funkcji platformy Azure. W zależności od wymagań hello hello stosowania tej funkcji może się różnić. Jednak hello ogólny przebieg kodu hello jest następujący:

1. Parametry wejściowe procesu.
2. Istniejący pakiet kwerendy przechwytuje limity tooverify i rozwiązać konflikty nazw.
3. Utwórz przechwytywania pakietów z odpowiednimi parametrami.
4. Przechwytywania pakietów sondowania okresowo czasu jego ukończenia.
5. Powiadomienie użytkownika hello, że sesja przechwytywania pakietów hello jest pełny.

Witaj poniższym przykładzie jest kod programu PowerShell, który może być używana w funkcji hello. Brak wartości, które wymagają toobe zastąpione dla **subscriptionId**, **resourceGroupName**, i **storageAccountName**.

```powershell
            #Import Azure PowerShell modules required toomake calls tooNetwork Watcher
            Import-Module "D:\home\site\wwwroot\AlertPacketCapturePowerShell\azuremodules\AzureRM.Profile\AzureRM.Profile.psd1" -Global
            Import-Module "D:\home\site\wwwroot\AlertPacketCapturePowerShell\azuremodules\AzureRM.Network\AzureRM.Network.psd1" -Global
            Import-Module "D:\home\site\wwwroot\AlertPacketCapturePowerShell\azuremodules\AzureRM.Resources\AzureRM.Resources.psd1" -Global

            #Process alert request body
            $requestBody = Get-Content $req -Raw | ConvertFrom-Json

            #Storage account ID toosave captures in
            $storageaccountid = "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{storageAccountName}"

            #Packet capture vars
            $packetcapturename = "PSAzureFunction"
            $packetCaptureLimit = 10
            $packetCaptureDuration = 10

            #Credentials
            $tenant = $env:AzureTenant
            $pw = $env:AzureCredPassword
            $clientid = $env:AzureClientId
            $keypath = "D:\home\site\wwwroot\AlertPacketCapturePowerShell\keys\PassEncryptKey.key"

            #Authentication
            $secpassword = $pw | ConvertTo-SecureString -Key (Get-Content $keypath)
            $credential = New-Object System.Management.Automation.PSCredential ($clientid, $secpassword)
            Add-AzureRMAccount -ServicePrincipal -Tenant $tenant -Credential $credential #-WarningAction SilentlyContinue | out-null


            #Get hello VM that fired hello alert
            if($requestBody.context.resourceType -eq "Microsoft.Compute/virtualMachines")
            {
                Write-Output ("Subscription ID: {0}" -f $requestBody.context.subscriptionId)
                Write-Output ("Resource Group:  {0}" -f $requestBody.context.resourceGroupName)
                Write-Output ("Resource Name:  {0}" -f $requestBody.context.resourceName)
                Write-Output ("Resource Type:  {0}" -f $requestBody.context.resourceType)

                #Get hello Network Watcher in hello VM's region
                $nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq $requestBody.context.resourceRegion}
                $networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName

                #Get existing packetCaptures
                $packetCaptures = Get-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher

                #Remove existing packet capture created by hello function (if it exists)
                $packetCaptures | %{if($_.Name -eq $packetCaptureName)
                { 
                    Remove-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -PacketCaptureName $packetCaptureName
                }}

                #Initiate packet capture on hello VM that fired hello alert
                if ((Get-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher).Count -lt $packetCaptureLimit){
                    echo "Initiating Packet Capture"
                    New-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -TargetVirtualMachineId $requestBody.context.resourceId -PacketCaptureName $packetCaptureName -StorageAccountId $storageaccountid -TimeLimitInSeconds $packetCaptureDuration
                    Out-File -Encoding Ascii -FilePath $res -inputObject "Packet Capture created on ${requestBody.context.resourceID}"
                }
            } 
 ``` 
#### <a name="retrieve-hello-function-url"></a>Pobierz adres URL funkcji hello 
1. Po utworzeniu funkcji, należy skonfigurować adres URL hello alertu toocall skojarzoną z hello funkcji. tooget tę wartość, adres URL funkcji hello kopiowania z funkcji aplikacji.

    ![Znajdowanie hello adres URL funkcji][functions13]

2. Skopiuj adres URL funkcji hello aplikacji funkcji.

    ![Kopiowanie hello adres URL funkcji][2]

Jeśli potrzebujesz właściwości niestandardowe w ładunku żądania POST webhook hello hello odwoływać się za[skonfigurować elementu webhook na alert metryki Azure](../monitoring-and-diagnostics/insights-webhooks-alerts.md).

## <a name="configure-an-alert-on-a-vm"></a>Konfigurowanie alertu dla maszyny Wirtualnej

Alerty, które mogą zostać skonfigurowane toonotify osób po określonej metryki przekracza wartość progową, który jest przypisany tooit. W tym przykładzie hello alertu znajduje się na powitania segmentów TCP, które są wysyłane, ale hello alertu można wywoływać dla innych metryk. W tym przykładzie alert jest skonfigurowany toocall funkcji hello toocall elementu webhook.

### <a name="create-hello-alert-rule"></a>Utwórz regułę alertu hello

Przejdź tooan istniejącej maszyny wirtualnej, a następnie dodaj regułę alertu. Bardziej szczegółowa dokumentacja na temat konfigurowania alertów można znaleźć w folderze [w monitorze Azure tworzyć alerty dla usług Azure - Azure portal](../monitoring-and-diagnostics/insights-alerts-portal.md). Wprowadź następujące wartości w hello hello **reguły alertu** bloku, a następnie wybierz **OK**.

  |**Ustawienie** | **Wartość** | **Szczegóły** |
  |---|---|---|
  |**Nazwa**|TCP_Segments_Sent_Exceeded|Nazwa reguły alertów hello.|
  |**Opis**|Przekroczono próg wysyłane segmentów TCP|Opis Hello hello reguły alertów.||
  |**Metryka**|Wysłane segmenty protokołu TCP| Witaj metryki toouse tootrigger hello alert. |
  |**Warunek**|Więcej niż| toouse warunek Hello podczas obliczania metryki hello.|
  |**Próg**|100| wartość Hello hello metryki, które wyzwala hello alert. Ta wartość musi być ustawiona tooa prawidłową wartość dla danego środowiska.|
  |**Okres**|Za pośrednictwem hello ostatnich pięciu minut| Określa okres hello w których toolook próg hello na powitania metryki.|
  |**Element Webhook**|[adres URL elementu webhook z funkcji aplikacji]| adres URL elementu webhook Hello z hello funkcji aplikacji, który został utworzony w poprzednich krokach hello.|

> [!NOTE]
> Metryka segmentów TCP Hello nie jest domyślnie włączona. Dowiedz się więcej na temat tooenable dodatkowe metryki, odwiedzając [włączania monitorowania i diagnostyki](../monitoring-and-diagnostics/insights-how-to-use-diagnostics.md).

## <a name="review-hello-results"></a>Przejrzyj wyniki hello

Po hello kryteria alertu wyzwalaczy hello jest tworzony przechwytywania pakietów. Przejdź tooNetwork obserwatora, a następnie wybierz **przechwytywania pakietów**. Na tej stronie możesz wybrać hello pakietów przechwytywania pliku łącza toodownload hello pakietów przechwytywania.

![Widok przechwytywania pakietów][functions14]

Jeśli plik przechwytywania hello jest przechowywany lokalnie, można je pobrać, logując się toohello maszyny wirtualnej.

Aby uzyskać instrukcje dotyczące pobierania plików z kontami magazynu Azure, zobacz [Rozpoczynanie pracy z magazynem obiektów Blob platformy Azure przy użyciu platformy .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md). Kolejnym narzędziem służy jest [Eksploratora usługi Storage](http://storageexplorer.com/).

Po pobraniu programu przechwytywania można wyświetlić go przy użyciu dowolnego narzędzia, który może odczytywać **CAP** pliku. Poniżej podano linki tootwo tych narzędzi:

- [Microsoft Message Analyzer](https://technet.microsoft.com/library/jj649776.aspx)
- [WireShark](https://www.wireshark.org/)

## <a name="next-steps"></a>Następne kroki

Dowiedz się, jak tooview Twojego pakietów przechwytuje odwiedzając [analizy przechwytywania pakietu z programu Wireshark](network-watcher-deep-packet-inspection.md).


[1]: ./media/network-watcher-alert-triggered-packet-capture/figure1.png
[1-1]: ./media/network-watcher-alert-triggered-packet-capture/figure1-1.png
[2]: ./media/network-watcher-alert-triggered-packet-capture/figure2.png
[3]: ./media/network-watcher-alert-triggered-packet-capture/figure3.png
[functions1]:./media/network-watcher-alert-triggered-packet-capture/functions1.png
[functions2]:./media/network-watcher-alert-triggered-packet-capture/functions2.png
[functions3]:./media/network-watcher-alert-triggered-packet-capture/functions3.png
[functions4]:./media/network-watcher-alert-triggered-packet-capture/functions4.png
[functions5]:./media/network-watcher-alert-triggered-packet-capture/functions5.png
[functions6]:./media/network-watcher-alert-triggered-packet-capture/functions6.png
[functions7]:./media/network-watcher-alert-triggered-packet-capture/functions7.png
[functions8]:./media/network-watcher-alert-triggered-packet-capture/functions8.png
[functions9]:./media/network-watcher-alert-triggered-packet-capture/functions9.png
[functions10]:./media/network-watcher-alert-triggered-packet-capture/functions10.png
[functions11]:./media/network-watcher-alert-triggered-packet-capture/functions11.png
[functions12]:./media/network-watcher-alert-triggered-packet-capture/functions12.png
[functions13]:./media/network-watcher-alert-triggered-packet-capture/functions13.png
[functions14]:./media/network-watcher-alert-triggered-packet-capture/functions14.png
[scenario]:./media/network-watcher-alert-triggered-packet-capture/scenario.png
