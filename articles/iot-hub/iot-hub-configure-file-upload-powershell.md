---
title: Przekazywanie pliku tooconfigure aaaUse hello Azure PowerShell | Dokumentacja firmy Microsoft
description: "Jak tooconfigure poleceń cmdlet programu Azure PowerShell hello toouse Twojego pliku tooenable Centrum IoT przekazuje z połączonych urządzeń. Zawiera informacje o konfigurowaniu hello miejsce docelowe konto magazynu Azure."
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 915f1597-272d-4fd4-8c5b-a0ccb1df0d91
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.openlocfilehash: 9dcdc41693c09cece411921b30c91d7b3db47395
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-iot-hub-file-uploads-using-powershell"></a>Konfigurowanie Centrum IoT przekazywania plików przy użyciu programu PowerShell

[!INCLUDE [iot-hub-file-upload-selector](../../includes/iot-hub-file-upload-selector.md)]

Witaj toouse [plików funkcji przekazywania w Centrum IoT][lnk-upload], należy najpierw powiązać konta magazynu platformy Azure z Centrum IoT. Możesz użyć istniejącego konta magazynu lub Utwórz nową.

toocomplete tego samouczka należy hello następujące:

* Aktywne konto platformy Azure. Jeśli go nie masz, możesz utworzyć [bezpłatne konto][lnk-free-trial] w zaledwie kilka minut.
* [Polecenia cmdlet programu PowerShell systemu Azure][lnk-powershell-install].
* Centrum Azure IoT. Jeśli nie masz Centrum IoT, możesz użyć hello [polecenia cmdlet New-AzureRmIoTHub] [ lnk-powershell-iothub] toocreate jeden lub użyj hello portalu zbyt[tworzenia Centrum IoT] [ lnk-portal-hub].
* Konto usługi Azure Storage. Jeśli nie masz konta magazynu platformy Azure, możesz użyć hello [poleceń cmdlet programu PowerShell magazynu Azure] [ lnk-powershell-storage] toocreate jeden lub użyj hello portalu zbyt[Utwórz konto magazynu] [ lnk-portal-storage].

## <a name="sign-in-and-set-your-azure-account"></a>Zaloguj się i ustawić konta platformy Azure

Zaloguj się tooyour konto platformy Azure i wyboru subskrypcji.

1. W wierszu polecenia programu PowerShell hello, uruchom hello **Login-AzureRmAccount** polecenia cmdlet:

    ```powershell
    Login-AzureRmAccount
    ```

1. Jeśli masz wiele subskrypcji Azure, logowanie tooAzure umożliwiają dostęp tooall hello subskrypcji platformy Azure skojarzonych z poświadczeniami użytkownika. Użyj następującego polecenia toolist hello subskrypcji platformy Azure, dostępne dla Ciebie toouse hello:

    ```powershell
    Get-AzureRMSubscription
    ```

    Użyj następującego polecenia tooselect subskrypcji ma się, że toouse toorun hello polecenia toomanage Centrum IoT hello. Identyfikator lub Nazwa subskrypcji hello można użyć z danych wyjściowych hello hello poprzednie polecenie:

    ```powershell
    Select-AzureRMSubscription `
        -SubscriptionName "{your subscription name}"
    ```

## <a name="retrieve-your-storage-account-details"></a>Pobieranie informacji o koncie magazynu

Hello kroków założono, że utworzone konto magazynu przy użyciu hello **Resource Manager** modelu wdrażania i nie hello **klasycznego** modelu wdrażania.

Plik tooconfigure przekazuje z urządzeń, należy hello parametry połączenia dla konta magazynu platformy Azure. Konto magazynu Hello musi znajdować się w hello tej samej subskrypcji co Centrum IoT. Należy również hello nazwa kontenera obiektów blob na koncie magazynu hello. Użyj następującego polecenia tooretrieve hello kluczy konta magazynu:

```powershell
Get-AzureRmStorageAccountKey `
  -Name {your storage account name} `
  -ResourceGroupName {your storage account resource group}
```

Zanotuj hello **klucz1** wartość klucza konta magazynu. Należy go hello następujące kroki.

Można użyć istniejącego kontenera obiektów blob z przekazywania plików lub Utwórz nowe:

* toolist hello istniejących kontenerów obiektów blob na koncie magazynu, należy użyć hello następującego polecenia:

    ```powershell
    $ctx = New-AzureStorageContext `
        -StorageAccountName {your storage account name} `
        -StorageAccountKey {your storage account key}
    Get-AzureStorageContainer -Context $ctx
    ```

* toocreate kontenera obiektów blob na koncie magazynu hello Użyj następującego polecenia:

    ```powershell
    $ctx = New-AzureStorageContext `
        -StorageAccountName {your storage account name} `
        -StorageAccountKey {your storage account key}
    New-AzureStorageContainer `
        -Name {your new container name} `
        -Permission Off `
        -Context $ctx
    ```

## <a name="configure-your-iot-hub"></a>Konfigurowanie Centrum IoT

Można teraz skonfigurować Twoje tooenable Centrum IoT [plików funkcji przekazywania] [ lnk-upload] przy użyciu informacji o koncie magazynu.

Konfiguracja Hello wymaga hello następujące wartości:

**Kontener magazynu**: kontener obiektów blob na koncie magazynu Azure w Twojej bieżącej subskrypcji platformy Azure tooassociate z Centrum IoT. Można pobrać informacji o koncie magazynu niezbędne hello w powyższej sekcji hello. Centrum IoT automatycznie generuje identyfikator URI SAS z kontenera obiektów blob toothis uprawnienia zapisu dla urządzeń toouse podczas ich przekazywania plików.

**Odbieranie powiadomień dla przekazanych plików**: Włącz lub Wyłącz powiadomienia o przekazywania plików.

**Czas wygaśnięcia SAS**: to ustawienie jest hello time-to-live z hello identyfikatorów URI SAS zwrócony toohello urządzenia przez Centrum IoT. Domyślnie tooone godzinę.

**Plik powiadomienia, ustawienia domyślne TTL**: hello time-to-live powiadomienia przekazywania pliku przed jego wygaśnięciem. Domyślnie tooone dnia.

**Powiadomienie dostarczania maksymalna liczba plików**: hello liczba hello Centrum IoT prób toodeliver powiadomienie przekazywania plików. Domyślnie too10.

Użyj następującego ustawienia przekazywania plików hello tooconfigure polecenia cmdlet programu PowerShell w Centrum IoT hello:

```powershell
Set-AzureRmIotHub `
    -ResourceGroupName "{your iot hub resource group}" `
    -Name "{your iot hub name}" `
    -FileUploadNotificationTtl "01:00:00" `
    -FileUploadSasUriTtl "01:00:00" `
    -EnableFileUploadNotifications $true `
    -FileUploadStorageConnectionString "DefaultEndpointsProtocol=https;AccountName={your storage account name};AccountKey={your storage account key};EndpointSuffix=core.windows.net" `
    -FileUploadContainerName "{your blob container name}" `
    -FileUploadNotificationMaxDeliveryCount 10
```

## <a name="next-steps"></a>Następne kroki

Aby uzyskać więcej informacji na temat możliwości przekazywania plików hello Centrum IoT, zobacz [przekazywania plików z urządzeniem][lnk-upload].

Wykonaj te toolearn łącza więcej informacji na temat zarządzania Centrum IoT Azure:

* [Zbiorcze zarządzania urządzeniami IoT][lnk-bulk]
* [Metryki Centrum IoT][lnk-metrics]
* [Operacje monitorowania][lnk-monitor]

toofurther Poznaj możliwości hello Centrum IoT, zobacz:

* [Przewodnik dewelopera Centrum IoT][lnk-devguide]
* [Symuluje urządzenia IoT krawędzi][lnk-iotedge]
* [Zabezpieczanie rozwiązania IoT z hello tła w][lnk-securing]

[lnk-upload]: iot-hub-devguide-file-upload.md

[lnk-bulk]: iot-hub-bulk-identity-mgmt.md
[lnk-metrics]: iot-hub-metrics.md
[lnk-monitor]: iot-hub-operations-monitoring.md

[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
[lnk-securing]: iot-hub-security-ground-up.md
[lnk-powershell-install]: https://docs.microsoft.com/powershell/azure/install-azurerm-ps
[lnk-powershell-storage]: https://docs.microsoft.com/powershell/module/azurerm.storage/
[lnk-powershell-iothub]: https://docs.microsoft.com/powershell/module/azurerm.iothub/new-azurermiothub
[lnk-portal-hub]: iot-hub-create-through-portal.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-portal-storage]:../storage/common/storage-create-storage-account.md