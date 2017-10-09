---
title: "Magazyn obiektów blob aaaUse dla usług IIS i tabeli magazynu dla zdarzeń w Azure Log Analytics | Dokumentacja firmy Microsoft"
description: "Analiza dzienników mogą odczytywać hello dzienników dla usług Azure, które zapisać tootable magazynu diagnostyki lub zapisywane magazynu tooblob dzienniki programu IIS."
services: log-analytics
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: bf444752-ecc1-4306-9489-c29cb37d6045
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/12/2017
ms.author: magoedte
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ff3de04dc8cb6729c1443372ec31a0e8dc47f273
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-blob-storage-for-iis-and-azure-table-storage-for-events-with-log-analytics"></a>Użyj magazynu obiektów blob platformy Azure dla usług IIS i Azure magazyn tabel zdarzeń o analizy dzienników

Analiza dzienników można przeczytać hello dzienniki hello następujące usługi, które zapisu diagnostyki tootable dzienniki magazynu lub IIS napisane tooblob magazynu:

* Sieć szkieletowa usług klastrów (wersja zapoznawcza)
* Maszyny wirtualne
* Role sieć Web/proces roboczy.

Analiza dzienników można zbierać dane dla tych zasobów, należy włączyć diagnostyki Azure.

Po włączeniu diagnostyki, można użyć hello portalu Azure lub programu PowerShell skonfiguruj dzienniki hello toocollect analizy dzienników.

Diagnostyka Azure to rozszerzenie Azure umożliwiającą toocollect danych diagnostycznych z rolą proces roboczy, roli sieci web lub maszynę wirtualną działającą na platformie Azure. Witaj dane są przechowywane na koncie magazynu Azure i następnie mogą zostać zebrane przez analizy dzienników.

Dla analizy dzienników toocollect tych dzienników diagnostyki Azure dzienniki hello należy hello następujących lokalizacji:

| Typ dziennika | Typ zasobu | Lokalizacja |
| --- | --- | --- |
| Dzienniki usług IIS |Maszyny wirtualne <br> Role sieci Web <br> Role procesów roboczych |wad iis logfiles (magazynu obiektów Blob) |
| Dziennik systemu |Maszyny wirtualne |LinuxsyslogVer2v0 (Tabela magazynu) |
| Zdarzenia operacyjne sieci szkieletowej usług |Węzły sieci szkieletowej usług |WADServiceFabricSystemEventTable |
| Zdarzenia niezawodnego aktora sieci szkieletowej usług |Węzły sieci szkieletowej usług |WADServiceFabricReliableActorEventTable |
| Zdarzenia niezawodnej usługi sieci szkieletowej usług |Węzły sieci szkieletowej usług |WADServiceFabricReliableServiceEventTable |
| Dzienniki zdarzeń systemu Windows |Węzły sieci szkieletowej usług <br> Maszyny wirtualne <br> Role sieci Web <br> Role procesów roboczych |WADWindowsEventLogsTable (Table Storage) |
| Dzienniki zdarzeń systemu Windows ETW |Węzły sieci szkieletowej usług <br> Maszyny wirtualne <br> Role sieci Web <br> Role procesów roboczych |WADETWEventTable (Table Storage) |

> [!NOTE]
> Dzienniki programu IIS z witryn sieci Web Azure nie są obecnie obsługiwane.
>
>

W przypadku maszyn wirtualnych ma hello opcji instalacji hello [analizy dzienników agenta](log-analytics-azure-vm-extension.md) w szczegółowe dane dodatkowe tooenable maszyny wirtualnej. Ponadto w dziennikach zdarzeń i dzienniki programu IIS stanie tooanalyze toobeing, można wykonywać dodatkowe analizy, w tym śledzenia zmian konfiguracji, SQL do oceny i oceny aktualizacji.

## <a name="enable-azure-diagnostics-in-a-virtual-machine-for-event-log-and-iis-log-collection"></a>Włącz diagnostykę Azure na maszynie wirtualnej dla dziennika zdarzeń i IIS zbierania dzienników
Hello użyj następującej procedury tooenable diagnostycznych platformy Azure na maszynie wirtualnej dziennika zdarzeń i IIS dziennika kolekcji za pomocą portalu Microsoft Azure hello.

### <a name="tooenable-azure-diagnostics-in-a-virtual-machine-with-hello-azure-portal"></a>tooenable diagnostycznych platformy Azure na maszynie wirtualnej z hello portalu Azure
1. Podczas tworzenia maszyny wirtualnej, należy zainstalować hello agenta maszyny Wirtualnej. Jeśli maszyna wirtualna hello już istnieje, sprawdź hello, że Agent maszyny Wirtualnej jest już zainstalowana.

   * W portalu Azure hello Przejdź toohello maszyny wirtualnej, wybierz **konfiguracji opcjonalnej**, następnie **diagnostyki** i ustaw **stan** zbyt**na**.

     Po zakończeniu hello maszyny Wirtualnej ma rozszerzenie Azure Diagnostics hello zainstalowany i uruchomiony. To rozszerzenie jest odpowiedzialny za zbierania danych diagnostycznych.
2. Aby włączyć monitorowanie i skonfigurować rejestrowanie zdarzeń w istniejącej maszyny Wirtualnej. Można włączyć diagnostyki na powitania poziom maszyny Wirtualnej. Diagnostyka tooenable, a następnie skonfiguruj rejestrowanie zdarzeń, wykonaj następujące kroki hello:

   1. Wybierz hello maszyny Wirtualnej.
   2. Kliknij przycisk **monitorowania**.
   3. Kliknij przycisk **diagnostyki**.
   4. Zestaw hello **stan** za**ON**.
   5. Wybierz każdego dziennika diagnostyki, które mają toocollect.
   6. Kliknij przycisk **OK**.

## <a name="enable-azure-diagnostics-in-a-web-role-for-iis-log-and-event-collection"></a>Włącz diagnostykę Azure w roli sieci Web dla usług IIS dziennika i zdarzenie kolekcji
Odwołuje się zbyt[jak tooEnable diagnostyki w usłudze w chmurze](../cloud-services/cloud-services-dotnet-diagnostics.md) ogólne instrukcje na temat włączania diagnostyki Azure. Poniższe instrukcje Hello te informacje i dostosować go do użytku z analizy dzienników.

Diagnostyka Azure włączone:

* Dzienniki programu IIS są przechowywane domyślnie przenoszone w odstępach czasu transferu scheduledTransferPeriod hello danych dziennika.
* Dzienniki zdarzeń systemu Windows nie są przesyłane domyślnie.

### <a name="tooenable-diagnostics"></a>Diagnostyka tooenable
tooenable dzienniki zdarzeń systemu Windows lub toochange hello scheduledTransferPeriod, skonfiguruj diagnostyki Azure za pomocą pliku konfiguracji XML hello (diagnostics.wadcfg), jak pokazano w [krok 4: Tworzenie pliku konfiguracji diagnostyki i instalacja hello rozszerzenia](../cloud-services/cloud-services-dotnet-diagnostics.md)

Witaj następujący przykładowy plik konfiguracji zbiera dzienniki programu IIS i wszystkie zdarzenia z aplikacji hello i dzienniki systemu:

```
    <?xml version="1.0" encoding="utf-8" ?>
    <DiagnosticMonitorConfiguration xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration"
          configurationChangePollInterval="PT1M"
          overallQuotaInMB="4096">

      <Directories bufferQuotaInMB="0"
         scheduledTransferPeriod="PT10M">  
        <!-- IISLogs are only relevant tooWeb roles -->
        <IISLogs container="wad-iis" directoryQuotaInMB="0" />
      </Directories>

      <WindowsEventLog bufferQuotaInMB="0"
         scheduledTransferLogLevelFilter="Verbose"
         scheduledTransferPeriod="PT10M">
        <DataSource name="Application!*" />
        <DataSource name="System!*" />
      </WindowsEventLog>

    </DiagnosticMonitorConfiguration>
```

Upewnij się, że Twoje appSettings określa konta magazynu, tak jak hello poniższy przykład:

```
    <ConfigurationSettings>
       <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="DefaultEndpointsProtocol=https;AccountName=<AccountName>;AccountKey=<AccountKey>"/>
    </ConfigurationSettings>
```

Witaj **AccountName** i **AccountKey** wartości znajdują się w hello portalu Azure w hello konta pulpitu nawigacyjnego magazynu, w obszarze Zarządzanie kluczami dostępu. Protokół Hello hello ciągu połączenia musi być **https**.

Po zastosowaniu zaktualizowanej konfiguracji diagnostycznych hello tooyour usługi w chmurze i zapisuje tooAzure diagnostyki magazynu, wówczas są gotowe tooconfigure analizy dzienników.

## <a name="use-hello-azure-portal-toocollect-logs-from-azure-storage"></a>Użyj dzienników toocollect portalu Azure hello z usługi Azure Storage
Witaj tooconfigure portalu Azure Log Analytics toocollect hello dzienniki służącego do powitania po usług Azure:

* Klastrów sieci szkieletowej usług
* Maszyny wirtualne
* Role sieć Web/proces roboczy.

W hello portalu Azure przejdź do obszaru roboczego analizy dzienników tooyour i wykonaj hello następujące zadania:

1. Kliknij przycisk *dzienników kont magazynu*
2. Kliknij przycisk hello *Dodaj* zadań
3. Wybierz konto magazynu hello zawierający hello dzienników diagnostycznych
   * To konto może być konto magazynu classic lub konta magazynu usługi Azure Resource Manager
4. Wybierz hello ma toocollect dzienniki dla typu danych
   * Wybór Hello jest dzienniki programu IIS; Zdarzenia; SYSLOG (Linux); Dzienniki zdarzeń systemu Windows; Zdarzenia sieci szkieletowej usług
5. wartość Hello źródła jest automatycznie wypełniane oparte na powitania typ danych i nie można zmienić
6. Kliknij przycisk OK toosave hello konfiguracji

Powtórz kroki od 2 do 6 dla dodatkowego magazynu kont i typy danych, które mają toocollect analizy dzienników.

W ciągu 30 minut jesteś stanie toosee dane z konta magazynu hello w analizy dzienników. Wyświetlany tylko dane zapisane toostorage po zastosowaniu hello konfiguracji. Analiza dzienników nie odczytywać dane istniejące hello hello konta magazynu.

> [!NOTE]
> Hello portal nie można zweryfikować tego hello źródło istnieje na koncie magazynu hello, lub jeśli nowe dane zostają zapisane.
>
>

## <a name="enable-azure-diagnostics-in-a-virtual-machine-for-event-log-and-iis-log-collection-using-powershell"></a>Włącz diagnostykę Azure na maszynie wirtualnej dziennika zdarzeń i IIS dziennika kolekcję przy użyciu programu PowerShell
Użyj hello czynnościach w ramach [tooindex Konfigurowanie analizy dzienników diagnostycznych platformy Azure](log-analytics-powershell-workspace-configuration.md#configuring-log-analytics-to-index-azure-diagnostics) toouse tooread programu PowerShell z diagnostyki Azure są zapisywane tootable magazynu.

Przy użyciu programu Azure PowerShell można bardziej precyzyjnie określić hello zdarzenia, które są zapisywane tooAzure magazynu.
Aby uzyskać więcej informacji, zobacz [Włączanie diagnostyki w maszynach wirtualnych platformy Azure](../virtual-machines-dotnet-diagnostics.md).

Można włączyć i zaktualizować diagnostyki Azure za pomocą hello następującego skryptu programu PowerShell.
Ten skrypt można również używać z konfiguracji rejestrowania niestandardowego.
Modyfikowanie konta magazynu hello hello skryptu tooset, nazwę usługi i nazwy maszyny wirtualnej.
skrypt Hello używa poleceń cmdlet klasycznej maszyn wirtualnych.

Przejrzyj powitania po przykładowym skrypcie, skopiuj go, w razie potrzeby, Zapisz przykładowy hello jako plik skryptu programu PowerShell, a następnie uruchom skrypt hello.

```
    #Connect tooAzure
    Add-AzureAccount

    # settings toochange:
    $wad_storage_account_name = "myStorageAccount"
    $service_name = "myService"
    $vm_name = "myVM"

    #Construct Azure Diagnostics public config and convert tooconfig format

    # Collect just system error events:
    $wad_xml_config = "<WadCfg><DiagnosticMonitorConfiguration><WindowsEventLog scheduledTransferPeriod=""PT1M""><DataSource name=""System!* "" /></WindowsEventLog></DiagnosticMonitorConfiguration></WadCfg>"

    $wad_b64_config = [System.Convert]::ToBase64String([System.Text.Encoding]::UTF8.GetBytes($wad_xml_config))
    $wad_public_config = [string]::Format("{{""xmlCfg"":""{0}""}}",$wad_b64_config)

    #Construct Azure diagnostics private config

    $wad_storage_account_key = (Get-AzureStorageKey $wad_storage_account_name).Primary
    $wad_private_config = [string]::Format("{{""storageAccountName"":""{0}"",""storageAccountKey"":""{1}""}}",$wad_storage_account_name,$wad_storage_account_key)

    #Enable Diagnostics Extension for Virtual Machine

    $wad_extension_name = "IaaSDiagnostics"
    $wad_publisher = "Microsoft.Azure.Diagnostics"
    $wad_version = (Get-AzureVMAvailableExtension -Publisher $wad_publisher -ExtensionName $wad_extension_name).Version # Gets latest version of hello extension

    (Get-AzureVM -ServiceName $service_name -Name $vm_name) | Set-AzureVMExtension -ExtensionName $wad_extension_name -Publisher $wad_publisher -PublicConfiguration $wad_public_config -PrivateConfiguration $wad_private_config -Version $wad_version | Update-AzureVM
```


## <a name="next-steps"></a>Następne kroki
* [Zbieranie dzienników i metryki dla usługi Azure](log-analytics-azure-storage.md) obsługiwanych usług platformy Azure.
* [Włącz rozwiązań](log-analytics-add-solutions.md) tooprovide wgląd w dane hello.
* [Użyj zapytań wyszukiwania](log-analytics-log-searches.md) tooanalyze hello danych.
