---
title: "tooIoT przekazywania pliku aaaConfigure Centrum przy użyciu wiersza polecenia platformy Azure (az.py) | Dokumentacja firmy Microsoft"
description: "Jak tooconfigure fileuploads tooAzure Centrum IoT przy użyciu hello 2.0 interfejsu wiersza polecenia platformy Azure i platform (az.py)."
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
ms.openlocfilehash: 390113df2d96df9833b6aa383ed66805528614a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-iot-hub-file-uploads-using-azure-cli"></a>Konfigurowanie Centrum IoT przekazywania plików przy użyciu wiersza polecenia platformy Azure

[!INCLUDE [iot-hub-file-upload-selector](../../includes/iot-hub-file-upload-selector.md)]

Witaj toouse [plików funkcji przekazywania w Centrum IoT][lnk-upload], należy najpierw powiązać konta usługi Azure Storage z Centrum IoT. Możesz użyć istniejącego konta magazynu lub Utwórz nową.

toocomplete tego samouczka należy hello następujące:

* Aktywne konto platformy Azure. Jeśli go nie masz, możesz utworzyć [bezpłatne konto][lnk-free-trial] w zaledwie kilka minut.
* [Azure CLI 2.0][lnk-CLI-install].
* Centrum Azure IoT. Jeśli nie masz Centrum IoT, możesz użyć hello `az iot hub create` [polecenia] [ lnk-cli-create-iothub] toocreate jeden lub użyj hello portalu zbyt [tworzenia Centrum IoT] [lnk-portal Centrum].
* Konto magazynu Azure. Jeśli nie masz konta usługi Azure Storage, można użyć hello [2.0 interfejsu wiersza polecenia platformy Azure — Zarządzanie kontami magazynu] [ lnk-manage-storage] toocreate jedną lub użyj hello portalu zbyt[Utwórz konto magazynu] [lnk-portal-storage].

## <a name="sign-in-and-set-your-azure-account"></a>Zaloguj się i ustawić konta platformy Azure

Zaloguj się tooyour konto platformy Azure i wyboru subskrypcji.

1. W wierszu polecenia hello Uruchom hello [polecenia logowania][lnk-login-command]:

    ```azurecli
    az login
    ```

    Postępuj zgodnie z tooauthenticate instrukcje hello przy użyciu kodu hello i zaloguj się na tooyour konto platformy Azure za pośrednictwem przeglądarki sieci web.

1. Jeśli masz wiele subskrypcji Azure, logowanie tooAzure umożliwiają dostęp tooall hello Azure konta skojarzone z poświadczeniami użytkownika. Poniższych hello [toolist polecenia hello Azure kont] [ lnk-az-account-command] dostępne dla toouse możesz:

    ```azurecli
    az account list
    ```

    Użyj następującego polecenia tooselect subskrypcji ma się, że toouse toorun hello polecenia toocreate Centrum IoT hello. Identyfikator lub Nazwa subskrypcji hello można użyć z danych wyjściowych hello hello poprzednie polecenie:

    ```azurecli
    az account set --subscription {your subscription name or id}
    ```

## <a name="retrieve-your-storage-account-details"></a>Pobieranie informacji o koncie magazynu

Hello kroków założono, że utworzone konto magazynu przy użyciu hello **Resource Manager** modelu wdrażania i nie hello **klasycznego** modelu wdrażania.

Plik tooconfigure przekazuje z urządzeń, należy hello parametry połączenia dla konta magazynu platformy Azure. Konto magazynu Hello musi znajdować się w hello tej samej subskrypcji co Centrum IoT. Należy również hello nazwa kontenera obiektów blob na koncie magazynu hello. Użyj następującego polecenia tooretrieve hello kluczy konta magazynu:

```azurecli
az storage account show-connection-string --name {your storage account name} --resource-group {your storage account resource group}
```

Zanotuj hello **connectionString** wartość. Należy go hello następujące kroki.

Można użyć istniejącego kontenera obiektów blob z przekazywania plików lub Utwórz nowe:

* toolist hello istniejących kontenerów obiektów blob na koncie magazynu, należy użyć hello następujące polecenie:

    ```azurecli
    az storage container list --connection-string "{your storage account connection string}"
    ```

* toocreate kontenera obiektów blob na koncie magazynu hello Użyj następującego polecenia:

    ```azurecli
    az storage container create --name {container name} --connection-string "{your storage account connection string}"
    ```

## <a name="file-upload"></a>Przekazywanie pliku

Można teraz skonfigurować Twoje tooenable Centrum IoT [plików funkcji przekazywania] [ lnk-upload] przy użyciu informacji o koncie magazynu.

Konfiguracja Hello wymaga hello następujące wartości:

**Kontener magazynu**: kontener obiektów blob na koncie magazynu Azure w Twojej bieżącej subskrypcji platformy Azure tooassociate z Centrum IoT. Można pobrać informacji o koncie magazynu niezbędne hello w powyższej sekcji hello. Centrum IoT automatycznie generuje identyfikator URI SAS z kontenera obiektów blob toothis uprawnienia zapisu dla urządzeń toouse podczas ich przekazywania plików.

**Odbieranie powiadomień dla przekazanych plików**: Włącz lub Wyłącz powiadomienia o przekazywania plików.

**Czas wygaśnięcia SAS**: to ustawienie jest hello time-to-live z hello identyfikatorów URI SAS zwrócony toohello urządzenia przez Centrum IoT. Domyślnie tooone godzinę.

**Plik powiadomienia, ustawienia domyślne TTL**: hello time-to-live powiadomienia przekazywania pliku przed jego wygaśnięciem. Domyślnie tooone dnia.

**Powiadomienie dostarczania maksymalna liczba plików**: hello liczba hello Centrum IoT prób toodeliver powiadomienie przekazywania plików. Domyślnie too10.

Użyj hello następujące ustawienia przekazywania plików hello tooconfigure polecenia wiersza polecenia platformy Azure w Centrum IoT:

Użycie powłoki bash:

```azurecli
az iot hub update --name {your iot hub name} --set properties.storageEndpoints.'$default'.connectionString="{your storage account connection string}"
az iot hub update --name {your iot hub name} --set properties.storageEndpoints.'$default'.containerName="{your storage container name}"
az iot hub update --name {your iot hub name} --set properties.storageEndpoints.'$default'.sasTtlAsIso8601=PT1H0M0S

az iot hub update --name {your iot hub name} --set properties.enableFileUploadNotifications=true
az iot hub update --name {your iot hub name} --set properties.messagingEndpoints.fileNotifications.maxDeliveryCount=10
az iot hub update --name {your iot hub name} --set properties.messagingEndpoints.fileNotifications.ttlAsIso8601=PT1H0M0S
```

W przypadku systemu Windows użyj wiersza polecenia:

```azurecli
az iot hub update --name {your iot hub name} --set "properties.storageEndpoints.$default.connectionString="{your storage account connection string}""
az iot hub update --name {your iot hub name} --set "properties.storageEndpoints.$default.containerName="{your storage container name}""
az iot hub update --name {your iot hub name} --set "properties.storageEndpoints.$default.sasTtlAsIso8601=PT1H0M0S"

az iot hub update --name {your iot hub name} --set properties.enableFileUploadNotifications=true
az iot hub update --name {your iot hub name} --set properties.messagingEndpoints.fileNotifications.maxDeliveryCount=10
az iot hub update --name {your iot hub name} --set properties.messagingEndpoints.fileNotifications.ttlAsIso8601=PT1H0M0S
```

Możesz przejrzeć konfiguracji przekazywania plików hello na Centrum IoT przy użyciu hello następujące polecenie:

```azurecli
az iot hub show --name {your iot hub name}
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

[13]: ./media/iot-hub-configure-file-upload/file-upload-settings.png
[14]: ./media/iot-hub-configure-file-upload/file-upload-container-selection.png
[15]: ./media/iot-hub-configure-file-upload/file-upload-selected-container.png

[lnk-upload]: iot-hub-devguide-file-upload.md

[lnk-bulk]: iot-hub-bulk-identity-mgmt.md
[lnk-metrics]: iot-hub-metrics.md
[lnk-monitor]: iot-hub-operations-monitoring.md

[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
[lnk-securing]: iot-hub-security-ground-up.md


[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-CLI-install]: https://docs.microsoft.com/cli/azure/install-az-cli2
[lnk-login-command]: https://docs.microsoft.com/cli/azure/get-started-with-az-cli2
[lnk-az-account-command]: https://docs.microsoft.com/cli/azure/account
[lnk-az-register-command]: https://docs.microsoft.com/cli/azure/provider
[lnk-az-addcomponent-command]: https://docs.microsoft.com/cli/azure/component
[lnk-az-resource-command]: https://docs.microsoft.com/cli/azure/resource
[lnk-az-iot-command]: https://docs.microsoft.com/cli/azure/iot
[lnk-iot-pricing]: https://azure.microsoft.com/pricing/details/iot-hub/
[lnk-manage-storage]:../storage/common/storage-azure-cli.md#manage-storage-accounts
[lnk-portal-storage]:../storage/common/storage-create-storage-account.md
[lnk-cli-create-iothub]: https://docs.microsoft.com/cli/azure/iot/hub#create