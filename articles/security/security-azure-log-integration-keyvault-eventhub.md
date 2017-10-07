---
title: "Dzienniki aaaIntegrate z usługi Azure Key Vault za pomocą usługi Event Hubs | Dokumentacja firmy Microsoft"
description: "Samouczek, który udostępnia hello niezbędne kroki toomake Key Vault dzienniki dostępne tooa SIEM za pomocą integracji dziennika Azure"
services: security
author: barclayn
manager: MBaldwin
editor: TomShinder
ms.assetid: 
ms.service: security
ms.topic: article
ms.date: 08/07/2017
ms.author: Barclayn
ms.custom: AzLog
ms.openlocfilehash: ada2fc846cc6bf09e12cc2c016815b27afef0d50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-log-integration-tutorial-process-azure-key-vault-events-by-using-event-hubs"></a>Samouczek usługi Azure integracji dziennika: zdarzeń procesu usługi Azure Key Vault za pomocą usługi Event Hubs

Można użyć zdarzenia rejestrowane tooretrieve integracji dziennika Azure i były dostępne tooyour zabezpieczeń systemu informacji i zdarzeń zarządzania (SIEM). W tym samouczku przedstawiono sposób integracji dziennika Azure może być używane tooprocess dzienniki, które zostały zakupione w ramach usługi Azure Event Hubs.
 
Użyj tego samouczka tooget zapoznanie się z sposób integracji dziennika Azure i usługi Event Hubs pracy ze sobą następuje hello przykładowe kroki i zrozumienie, jak każdy krok obsługuje hello rozwiązanie. Następnie należy wykonać co znasz tutaj toocreate własne toosupport kroki unikatowe wymagania firmy.

>[!WARNING]
Witaj kroków i poleceń, w tym samouczku nie są zamierzone toobe skopiowane i wklejone. Są one tylko przykładowe. Nie należy używać poleceń programu PowerShell hello "w jakim jest" w środowisku na żywo. Należy dostosować oparte na środowisku unikatowy.


Ten samouczek przeprowadzi Cię przez proces hello Centrum zdarzeń zarejestrowanych tooan działania usługi Azure Key Vault pobieranie oraz udostępnianie go jako system SIEM tooyour pliki JSON. Następnie można skonfigurować pliki JSON hello tooprocess system SIEM.

>[!NOTE]
>Większość hello kroków w tym samouczku obejmują konfigurowanie magazynów kluczy konta magazynu i usługi event hubs. określone kroki integracji dziennika Azure Hello są hello na końcu tego samouczka. Nie należy wykonywać następujące czynności w środowisku produkcyjnym. Są one przeznaczone dla środowiska laboratoryjnego. Należy dostosować hello kroki przed ich użyciem w środowisku produkcyjnym.

Informacje udostępniane wzdłuż hello sposób pomaga się, że rozumiesz hello przyczynami każdego kroku. Artykuły tooother łącza umożliwiają bardziej szczegółowo na niektóre tematy.

Aby uzyskać więcej informacji o usługach hello, które w tym samouczku uwagi zobacz: 

- [Usługa Azure Key Vault](../key-vault/key-vault-whatis.md)
- [Azure Event Hubs](../event-hubs/event-hubs-what-is-event-hubs.md)
- [Integracja z dzienników Azure](security-azure-log-integration-overview.md)


## <a name="initial-setup"></a>Początkowej konfiguracji

Przed ukończeniem hello opisanych w tym artykule, potrzebne są następujące hello:

1. Subskrypcja platformy Azure i konta dla tej subskrypcji z uprawnieniami administratora. Jeśli nie masz subskrypcji, możesz utworzyć [bezpłatne konto](https://azure.microsoft.com/free/).
 
2. System z toohello dostęp do Internetu, który spełnia wymagania hello Azure integracji dziennika instalacji. Hello system może znajdować się na usługi w chmurze lub obsługiwanego lokalnie.

3. [Integracja z usługą Azure dziennika](https://www.microsoft.com/download/details.aspx?id=53324) zainstalowane. tooinstall go:

   a. Należy używać systemu toohello tooconnect pulpitu zdalnego wspomnianego w kroku 2.   
   b. Skopiuj hello Azure integracji dziennika Instalatora toohello systemu. Możesz [pobierane pliki instalacyjne hello](https://www.microsoft.com/download/details.aspx?id=53324).   
   c. Uruchom Instalator hello i zaakceptuj postanowienia licencyjne dotyczące oprogramowania firmy Microsoft hello.   
   d. Jeśli będzie zawierał informacje telemetryczne, pozostaw zaznaczone pole wyboru hello. Jeśli użytkownik nie wysłać tooMicrosoft informacji użycia, wyczyść pole wyboru hello.
   
   Aby uzyskać więcej informacji o integracji z dziennika Azure i w jaki sposób tooinstall, zobacz [Azure dziennika Integracja z usługą rejestrowania diagnostyki Azure i funkcji przekazywania zdarzeń systemu Windows](security-azure-log-integration-get-started.md).

4. Witaj najnowsza wersja programu PowerShell.
 
   Jeśli masz zainstalowany program Windows Server 2016, musisz mieć co najmniej PowerShell 5.0. Jeśli używasz wersji systemu Windows Server może być starsza wersja programu PowerShell jest zainstalowane. Można sprawdzić wersji hello wprowadzając ```get-host``` w oknie programu PowerShell. Jeśli nie masz programu PowerShell 5.0 zainstalowany, możesz [go pobrać](https://www.microsoft.com/download/details.aspx?id=50395).

   Po utworzeniu co najmniej PowerShell 5.0, możesz przejść tooinstall hello najnowszej wersji:
   
   a. W oknie programu PowerShell, wprowadź hello ```Install-Module Azure``` polecenia. Wykonaj kroki instalacji hello.    
   b. Wprowadź hello ```Install-Module AzureRM``` polecenia. Wykonaj kroki instalacji hello.

   Aby uzyskać więcej informacji, zobacz [instalacji programu Azure PowerShell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.0.0).


## <a name="create-supporting-infrastructure-elements"></a>Utwórz elementy infrastruktury obsługi

1. Otwórz okno programu PowerShell z podwyższonym poziomem uprawnień i przejdź zbyt**C:\Program Files\Microsoft Azure dziennika integracji**.
2. Zaimportuj polecenia cmdlet AzLog hello przez uruchomienie skryptu hello LoadAzLogModule.ps1. Wprowadź hello `.\LoadAzLogModule.ps1` polecenia. (Uwaga hello ". \" w tym poleceniu.) Powinny zostać wyświetlone informacje podobne do następujących:</br>

   ![Listę załadowanych modułów](./media/security-azure-log-integration-keyvault-eventhub/loaded-modules.png)

3. Wprowadź hello `Login-AzureRmAccount` polecenia. Okno logowania hello wprowadzanie informacji o poświadczeniach hello hello subskrypcji, która będzie używana w tym samouczku.

   >[!NOTE]
   >Jeśli jest to hello jest rejestrowanie w tooAzure z tego komputera po raz pierwszy, zobaczysz komunikat o dane użycia programu PowerShell toocollect firmy Microsoft. Firma Microsoft zaleca włączyć tej kolekcji danych, ponieważ będzie ona używana tooimprove programu Azure PowerShell.

4. Po pomyślnym uwierzytelnieniu użytkownik zalogował się i pojawi się informacja hello w hello następującego zrzutu ekranu. Zanotuj nazwę subskrypcji hello identyfikator i subskrypcji, ponieważ konieczne będzie ich toocomplete później kroków.

   ![Okno programu PowerShell](./media/security-azure-log-integration-keyvault-eventhub/login-azurermaccount.png)
5. Utwórz zmienne toostore wartości, które będą używane później. Wprowadź każdy hello następujące wiersze programu PowerShell. Może być konieczne tooadjust hello wartości toomatch środowiska.
    - ```$subscriptionName = ‘Visual Studio Ultimate with MSDN’```(Nazwa Twojej subskrypcji mogą się różnić. Można to sprawdzić jako część hello dane wyjściowe poprzedniego polecenia hello.)
    - ```$location = 'West US'```(Ta zmienna będzie toopass używane hello lokalizacji, gdzie utworzone zasoby. Można zmienić tej zmiennej toobe dowolnej lokalizacji wybrane.)
    - ```$random = Get-Random```
    - ``` $name = 'azlogtest' + $random```(nazwa hello może być dowolna, ale powinien zawierać tylko małe litery i cyfry).
    - ``` $storageName = $name```(Ta zmienna będzie można używać nazwy konta magazynu hello).
    - ```$rgname = $name ```(Ta zmienna będzie służyć do nazwy grupy zasobów hello.)
    - ``` $eventHubNameSpaceName = $name```(Jest hello nazwę przestrzeni nazw Centrum zdarzeń hello).
6. Określ hello subskrypcji, która będzie działać z:
    
    ```Select-AzureRmSubscription -SubscriptionName $subscriptionName```
7. Utwórz grupę zasobów:
    
    ```$rg = New-AzureRmResourceGroup -Name $rgname -Location $location```
    
   Po wprowadzeniu `$rg` w tym momencie powinny być widoczne dane wyjściowe podobne toothis w zrzut ekranu:

   ![Dane wyjściowe po utworzeniu grupy zasobów](./media/security-azure-log-integration-keyvault-eventhub/create-rg.png)
8. Utwórz konto magazynu, które będzie używane tookeep śledzenie informacji o stanie:
    
    ```$storage = New-AzureRmStorageAccount -ResourceGroupName $rgname -Name $storagename -Location $location -SkuName Standard_LRS```
9. Utwórz hello przestrzeni nazw z Centrum zdarzeń. Jest to wymagane toocreate Centrum zdarzeń.
    
    ```$eventHubNameSpace = New-AzureRmEventHubNamespace -ResourceGroupName $rgname -NamespaceName $eventHubnamespaceName -Location $location```
10. Pobierz identyfikator reguły hello, który będzie używany z dostawcą insights hello:
    
    ```$sbruleid = $eventHubNameSpace.Id +'/authorizationrules/RootManageSharedAccessKey' ```
11. Pobierz wszystkie możliwe lokalizacji platformy Azure i Dodaj hello nazwy tooa zmiennej, która może być używany w kolejnym kroku:
    
    a. ```$locationObjects = Get-AzureRMLocation```    
    b. ```$locations = @('global') + $locationobjects.location```
    
    Po wprowadzeniu `$locations` w tym momencie wyświetlić nazwy lokalizacji hello bez dodatkowych informacji hello zwrócony przez Get-AzureRmLocation.
12. Utwórz profil usługi Azure Resource Manager dziennika: 
    
    ```Add-AzureRmLogProfile -Name $name -ServiceBusRuleId $sbruleid -Locations $locations```
    
    Aby uzyskać więcej informacji na temat hello profilu dzienników Azure, zobacz [omówienie hello dziennika aktywności platformy Azure](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md).

> [!NOTE]
> Podczas próby toocreate profilu dziennika, może być wyświetlony komunikat o błędzie. Można następnie przejrzyj dokumentację hello Get AzureRmLogProfile i Usuń AzureRmLogProfile. Po uruchomieniu Get-AzureRmLogProfile pojawi się informacja o hello dziennika profilu. Można usunąć istniejącego profilu dziennika hello wprowadzając hello ```Remove-AzureRmLogProfile -name 'Log Profile Name' ``` polecenia.
>
>![Błąd profilu usługi Resource Manager](./media/security-azure-log-integration-keyvault-eventhub/rm-profile-error.png)

## <a name="create-a-key-vault"></a>Tworzenie magazynu kluczy

1. Utwórz magazyn kluczy hello:

   ```$kv = New-AzureRmKeyVault -VaultName $name -ResourceGroupName $rgname -Location $location ```

2. Konfiguruj rejestrowanie dla magazynu kluczy hello:

   ```Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -ServiceBusRuleId $sbruleid -Enabled $true ```

## <a name="generate-log-activity"></a>Wygenerować dziennik aktywności

Żądania muszą toobe wysyłane tooKey magazynu toogenerate dziennik aktywności. Generowania kluczy, przechowywanie kluczy tajnych, takie jak akcje lub odczytu klucze tajne z magazynu kluczy zostanie utworzona wpisy dziennika.

1. Wyświetl hello bieżącego magazynu kluczy:
    
   ```Get-AzureRmStorageAccountKey -Name $storagename -ResourceGroupName $rgname  | ft -a```
2. Generuj nową **klucz2**:
    
   ```New-AzureRmStorageAccountKey -Name $storagename -ResourceGroupName $rgname -KeyName key2```
3. Ponownie wyświetlić hello kluczy i zobacz, który **klucz2** zawiera inną wartość:
    
   ```Get-AzureRmStorageAccountKey -Name $storagename -ResourceGroupName $rgname  | ft -a```
4. Ustaw i odczytu tajny toogenerate wpisy dziennika dodatkowe:
    
   a. ```Set-AzureKeyVaultSecret -VaultName $name -Name TestSecret -SecretValue (ConvertTo-SecureString -String 'Hi There!' -AsPlainText -Force)``` b. ```(Get-AzureKeyVaultSecret -VaultName $name -Name TestSecret).SecretValueText```

   ![Zwrócony tajny](./media/security-azure-log-integration-keyvault-eventhub/keyvaultsecret.png)


## <a name="configure-azure-log-integration"></a>Konfigurowanie integracji dzienników Azure

Skonfigurowano wszystkie hello wymaganych elementów toohave rejestrowania usługi Key Vault tooan zdarzenia koncentratora, trzeba tooconfigure Azure dziennika integracji:

1. ```$storage = Get-AzureRmStorageAccount -ResourceGroupName $rgname -Name $storagename```
2. ```$eventHubKey = Get-AzureRmEventHubNamespaceKey -ResourceGroupName $rgname -NamespaceName $eventHubNamespace.name -AuthorizationRuleName RootManageSharedAccessKey```
3. ```$storagekeys = Get-AzureRmStorageAccountKey -ResourceGroupName $rgname -Name $storagename```
4. ``` $storagekey = $storagekeys[0].Value```

Uruchom polecenie AzLog powitania dla każdego Centrum zdarzeń:

1. ```$eventhubs = Get-AzureRmEventHub -ResourceGroupName $rgname -NamespaceName $eventHubNamespaceName```
2. ```$eventhubs.Name | %{Add-AzLogEventSource -Name $sub' - '$_ -StorageAccount $storage.StorageAccountName -StorageKey $storageKey -EventHubConnectionString $eventHubKey.PrimaryConnectionString -EventHubName $_}```

Po minucie lub sposób uruchamiania hello ostatnich dwóch poleceń powinna zostać wyświetlona generowaną pliki w formacie JSON. Użytkownik może upewnij się, że przez monitorowanie katalogu hello **C:\users\AzLog\EventHubJson**.

## <a name="next-steps"></a>Następne kroki

- [Integracja dzienników Azure — często zadawane pytania](security-azure-log-integration-faq.md)
- [Wprowadzenie do integracji dziennika Azure](security-azure-log-integration-get-started.md)
- [Integrowanie dzienników z zasobów platformy Azure z systemów SIEM](security-azure-log-integration-overview.md)
