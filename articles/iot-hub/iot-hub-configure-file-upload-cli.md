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
# <a name="configure-iot-hub-file-uploads-using-azure-cli"></a><span data-ttu-id="1b3bb-103">Konfigurowanie Centrum IoT przekazywania plików przy użyciu wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="1b3bb-103">Configure IoT Hub file uploads using Azure CLI</span></span>

[!INCLUDE [iot-hub-file-upload-selector](../../includes/iot-hub-file-upload-selector.md)]

<span data-ttu-id="1b3bb-104">Witaj toouse [plików funkcji przekazywania w Centrum IoT][lnk-upload], należy najpierw powiązać konta usługi Azure Storage z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="1b3bb-104">toouse hello [file upload functionality in IoT Hub][lnk-upload], you must first associate an Azure Storage account with your IoT hub.</span></span> <span data-ttu-id="1b3bb-105">Możesz użyć istniejącego konta magazynu lub Utwórz nową.</span><span class="sxs-lookup"><span data-stu-id="1b3bb-105">You can use an existing storage account or create a new one.</span></span>

<span data-ttu-id="1b3bb-106">toocomplete tego samouczka należy hello następujące:</span><span class="sxs-lookup"><span data-stu-id="1b3bb-106">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="1b3bb-107">Aktywne konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="1b3bb-107">An active Azure account.</span></span> <span data-ttu-id="1b3bb-108">Jeśli go nie masz, możesz utworzyć [bezpłatne konto][lnk-free-trial] w zaledwie kilka minut.</span><span class="sxs-lookup"><span data-stu-id="1b3bb-108">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="1b3bb-109">[Azure CLI 2.0][lnk-CLI-install].</span><span class="sxs-lookup"><span data-stu-id="1b3bb-109">[Azure CLI 2.0][lnk-CLI-install].</span></span>
* <span data-ttu-id="1b3bb-110">Centrum Azure IoT.</span><span class="sxs-lookup"><span data-stu-id="1b3bb-110">An Azure IoT hub.</span></span> <span data-ttu-id="1b3bb-111">Jeśli nie masz Centrum IoT, możesz użyć hello `az iot hub create` [polecenia] [ lnk-cli-create-iothub] toocreate jeden lub użyj hello portalu zbyt [tworzenia Centrum IoT] [lnk-portal Centrum].</span><span class="sxs-lookup"><span data-stu-id="1b3bb-111">If you don't have an IoT hub, you can use hello `az iot hub create` [command][lnk-cli-create-iothub] toocreate one or use hello portal too[Create an IoT hub][lnk-portal-hub].</span></span>
* <span data-ttu-id="1b3bb-112">Konto magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="1b3bb-112">An Azure Storage account.</span></span> <span data-ttu-id="1b3bb-113">Jeśli nie masz konta usługi Azure Storage, można użyć hello [2.0 interfejsu wiersza polecenia platformy Azure — Zarządzanie kontami magazynu] [ lnk-manage-storage] toocreate jedną lub użyj hello portalu zbyt[Utwórz konto magazynu] [lnk-portal-storage].</span><span class="sxs-lookup"><span data-stu-id="1b3bb-113">If you don't have an Azure Storage account, you can use hello [Azure CLI 2.0 - Manage storage accounts][lnk-manage-storage] toocreate one or use hello portal too[Create a storage account][lnk-portal-storage].</span></span>

## <a name="sign-in-and-set-your-azure-account"></a><span data-ttu-id="1b3bb-114">Zaloguj się i ustawić konta platformy Azure</span><span class="sxs-lookup"><span data-stu-id="1b3bb-114">Sign in and set your Azure account</span></span>

<span data-ttu-id="1b3bb-115">Zaloguj się tooyour konto platformy Azure i wyboru subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="1b3bb-115">Sign in tooyour Azure account and select your subscription.</span></span>

1. <span data-ttu-id="1b3bb-116">W wierszu polecenia hello Uruchom hello [polecenia logowania][lnk-login-command]:</span><span class="sxs-lookup"><span data-stu-id="1b3bb-116">At hello command prompt, run hello [login command][lnk-login-command]:</span></span>

    ```azurecli
    az login
    ```

    <span data-ttu-id="1b3bb-117">Postępuj zgodnie z tooauthenticate instrukcje hello przy użyciu kodu hello i zaloguj się na tooyour konto platformy Azure za pośrednictwem przeglądarki sieci web.</span><span class="sxs-lookup"><span data-stu-id="1b3bb-117">Follow hello instructions tooauthenticate using hello code and sign in tooyour Azure account through a web browser.</span></span>

1. <span data-ttu-id="1b3bb-118">Jeśli masz wiele subskrypcji Azure, logowanie tooAzure umożliwiają dostęp tooall hello Azure konta skojarzone z poświadczeniami użytkownika.</span><span class="sxs-lookup"><span data-stu-id="1b3bb-118">If you have multiple Azure subscriptions, signing in tooAzure grants you access tooall hello Azure accounts associated with your credentials.</span></span> <span data-ttu-id="1b3bb-119">Poniższych hello [toolist polecenia hello Azure kont] [ lnk-az-account-command] dostępne dla toouse możesz:</span><span class="sxs-lookup"><span data-stu-id="1b3bb-119">Use hello following [command toolist hello Azure accounts][lnk-az-account-command] available for you toouse:</span></span>

    ```azurecli
    az account list
    ```

    <span data-ttu-id="1b3bb-120">Użyj następującego polecenia tooselect subskrypcji ma się, że toouse toorun hello polecenia toocreate Centrum IoT hello.</span><span class="sxs-lookup"><span data-stu-id="1b3bb-120">Use hello following command tooselect subscription that you want toouse toorun hello commands toocreate your IoT hub.</span></span> <span data-ttu-id="1b3bb-121">Identyfikator lub Nazwa subskrypcji hello można użyć z danych wyjściowych hello hello poprzednie polecenie:</span><span class="sxs-lookup"><span data-stu-id="1b3bb-121">You can use either hello subscription name or ID from hello output of hello previous command:</span></span>

    ```azurecli
    az account set --subscription {your subscription name or id}
    ```

## <a name="retrieve-your-storage-account-details"></a><span data-ttu-id="1b3bb-122">Pobieranie informacji o koncie magazynu</span><span class="sxs-lookup"><span data-stu-id="1b3bb-122">Retrieve your storage account details</span></span>

<span data-ttu-id="1b3bb-123">Hello kroków założono, że utworzone konto magazynu przy użyciu hello **Resource Manager** modelu wdrażania i nie hello **klasycznego** modelu wdrażania.</span><span class="sxs-lookup"><span data-stu-id="1b3bb-123">hello following steps assume that you created your storage account using hello **Resource Manager** deployment model, and not hello **Classic** deployment model.</span></span>

<span data-ttu-id="1b3bb-124">Plik tooconfigure przekazuje z urządzeń, należy hello parametry połączenia dla konta magazynu platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="1b3bb-124">tooconfigure file uploads from your devices, you need hello connection string for an Azure storage account.</span></span> <span data-ttu-id="1b3bb-125">Konto magazynu Hello musi znajdować się w hello tej samej subskrypcji co Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="1b3bb-125">hello storage account must be in hello same subscription as your IoT hub.</span></span> <span data-ttu-id="1b3bb-126">Należy również hello nazwa kontenera obiektów blob na koncie magazynu hello.</span><span class="sxs-lookup"><span data-stu-id="1b3bb-126">You also need hello name of a blob container in hello storage account.</span></span> <span data-ttu-id="1b3bb-127">Użyj następującego polecenia tooretrieve hello kluczy konta magazynu:</span><span class="sxs-lookup"><span data-stu-id="1b3bb-127">Use hello following command tooretrieve your storage account keys:</span></span>

```azurecli
az storage account show-connection-string --name {your storage account name} --resource-group {your storage account resource group}
```

<span data-ttu-id="1b3bb-128">Zanotuj hello **connectionString** wartość.</span><span class="sxs-lookup"><span data-stu-id="1b3bb-128">Make a note of hello **connectionString** value.</span></span> <span data-ttu-id="1b3bb-129">Należy go hello następujące kroki.</span><span class="sxs-lookup"><span data-stu-id="1b3bb-129">You need it in hello following steps.</span></span>

<span data-ttu-id="1b3bb-130">Można użyć istniejącego kontenera obiektów blob z przekazywania plików lub Utwórz nowe:</span><span class="sxs-lookup"><span data-stu-id="1b3bb-130">You can either use an existing blob container for your file uploads or create new one:</span></span>

* <span data-ttu-id="1b3bb-131">toolist hello istniejących kontenerów obiektów blob na koncie magazynu, należy użyć hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="1b3bb-131">toolist hello existing blob containers in your storage account, use hello following command:</span></span>

    ```azurecli
    az storage container list --connection-string "{your storage account connection string}"
    ```

* <span data-ttu-id="1b3bb-132">toocreate kontenera obiektów blob na koncie magazynu hello Użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="1b3bb-132">toocreate a blob container in your storage account, use hello following command:</span></span>

    ```azurecli
    az storage container create --name {container name} --connection-string "{your storage account connection string}"
    ```

## <a name="file-upload"></a><span data-ttu-id="1b3bb-133">Przekazywanie pliku</span><span class="sxs-lookup"><span data-stu-id="1b3bb-133">File upload</span></span>

<span data-ttu-id="1b3bb-134">Można teraz skonfigurować Twoje tooenable Centrum IoT [plików funkcji przekazywania] [ lnk-upload] przy użyciu informacji o koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="1b3bb-134">You can now configure your IoT hub tooenable [file upload functionality][lnk-upload] using your storage account details.</span></span>

<span data-ttu-id="1b3bb-135">Konfiguracja Hello wymaga hello następujące wartości:</span><span class="sxs-lookup"><span data-stu-id="1b3bb-135">hello configuration requires hello following values:</span></span>

<span data-ttu-id="1b3bb-136">**Kontener magazynu**: kontener obiektów blob na koncie magazynu Azure w Twojej bieżącej subskrypcji platformy Azure tooassociate z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="1b3bb-136">**Storage container**: A blob container in an Azure storage account in your current Azure subscription tooassociate with your IoT hub.</span></span> <span data-ttu-id="1b3bb-137">Można pobrać informacji o koncie magazynu niezbędne hello w powyższej sekcji hello.</span><span class="sxs-lookup"><span data-stu-id="1b3bb-137">You retrieved hello necessary storage account information in hello preceding section.</span></span> <span data-ttu-id="1b3bb-138">Centrum IoT automatycznie generuje identyfikator URI SAS z kontenera obiektów blob toothis uprawnienia zapisu dla urządzeń toouse podczas ich przekazywania plików.</span><span class="sxs-lookup"><span data-stu-id="1b3bb-138">IoT Hub automatically generates SAS URIs with write permissions toothis blob container for devices toouse when they upload files.</span></span>

<span data-ttu-id="1b3bb-139">**Odbieranie powiadomień dla przekazanych plików**: Włącz lub Wyłącz powiadomienia o przekazywania plików.</span><span class="sxs-lookup"><span data-stu-id="1b3bb-139">**Receive notifications for uploaded files**: Enable or disable file upload notifications.</span></span>

<span data-ttu-id="1b3bb-140">**Czas wygaśnięcia SAS**: to ustawienie jest hello time-to-live z hello identyfikatorów URI SAS zwrócony toohello urządzenia przez Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="1b3bb-140">**SAS TTL**: This setting is hello time-to-live of hello SAS URIs returned toohello device by IoT Hub.</span></span> <span data-ttu-id="1b3bb-141">Domyślnie tooone godzinę.</span><span class="sxs-lookup"><span data-stu-id="1b3bb-141">Set tooone hour by default.</span></span>

<span data-ttu-id="1b3bb-142">**Plik powiadomienia, ustawienia domyślne TTL**: hello time-to-live powiadomienia przekazywania pliku przed jego wygaśnięciem.</span><span class="sxs-lookup"><span data-stu-id="1b3bb-142">**File notification settings default TTL**: hello time-to-live of a file upload notification before it is expired.</span></span> <span data-ttu-id="1b3bb-143">Domyślnie tooone dnia.</span><span class="sxs-lookup"><span data-stu-id="1b3bb-143">Set tooone day by default.</span></span>

<span data-ttu-id="1b3bb-144">**Powiadomienie dostarczania maksymalna liczba plików**: hello liczba hello Centrum IoT prób toodeliver powiadomienie przekazywania plików.</span><span class="sxs-lookup"><span data-stu-id="1b3bb-144">**File notification maximum delivery count**: hello number of times hello IoT Hub attempts toodeliver a file upload notification.</span></span> <span data-ttu-id="1b3bb-145">Domyślnie too10.</span><span class="sxs-lookup"><span data-stu-id="1b3bb-145">Set too10 by default.</span></span>

<span data-ttu-id="1b3bb-146">Użyj hello następujące ustawienia przekazywania plików hello tooconfigure polecenia wiersza polecenia platformy Azure w Centrum IoT:</span><span class="sxs-lookup"><span data-stu-id="1b3bb-146">Use hello following Azure CLI commands tooconfigure hello file upload settings on your IoT hub:</span></span>

<span data-ttu-id="1b3bb-147">Użycie powłoki bash:</span><span class="sxs-lookup"><span data-stu-id="1b3bb-147">In a bash shell use:</span></span>

```azurecli
az iot hub update --name {your iot hub name} --set properties.storageEndpoints.'$default'.connectionString="{your storage account connection string}"
az iot hub update --name {your iot hub name} --set properties.storageEndpoints.'$default'.containerName="{your storage container name}"
az iot hub update --name {your iot hub name} --set properties.storageEndpoints.'$default'.sasTtlAsIso8601=PT1H0M0S

az iot hub update --name {your iot hub name} --set properties.enableFileUploadNotifications=true
az iot hub update --name {your iot hub name} --set properties.messagingEndpoints.fileNotifications.maxDeliveryCount=10
az iot hub update --name {your iot hub name} --set properties.messagingEndpoints.fileNotifications.ttlAsIso8601=PT1H0M0S
```

<span data-ttu-id="1b3bb-148">W przypadku systemu Windows użyj wiersza polecenia:</span><span class="sxs-lookup"><span data-stu-id="1b3bb-148">At a Windows command prompt use:</span></span>

```azurecli
az iot hub update --name {your iot hub name} --set "properties.storageEndpoints.$default.connectionString="{your storage account connection string}""
az iot hub update --name {your iot hub name} --set "properties.storageEndpoints.$default.containerName="{your storage container name}""
az iot hub update --name {your iot hub name} --set "properties.storageEndpoints.$default.sasTtlAsIso8601=PT1H0M0S"

az iot hub update --name {your iot hub name} --set properties.enableFileUploadNotifications=true
az iot hub update --name {your iot hub name} --set properties.messagingEndpoints.fileNotifications.maxDeliveryCount=10
az iot hub update --name {your iot hub name} --set properties.messagingEndpoints.fileNotifications.ttlAsIso8601=PT1H0M0S
```

<span data-ttu-id="1b3bb-149">Możesz przejrzeć konfiguracji przekazywania plików hello na Centrum IoT przy użyciu hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="1b3bb-149">You can review hello file upload configuration on your IoT hub using hello following command:</span></span>

```azurecli
az iot hub show --name {your iot hub name}
```

## <a name="next-steps"></a><span data-ttu-id="1b3bb-150">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="1b3bb-150">Next steps</span></span>

<span data-ttu-id="1b3bb-151">Aby uzyskać więcej informacji na temat możliwości przekazywania plików hello Centrum IoT, zobacz [przekazywania plików z urządzeniem][lnk-upload].</span><span class="sxs-lookup"><span data-stu-id="1b3bb-151">For more information about hello file upload capabilities of IoT Hub, see [Upload files from a device][lnk-upload].</span></span>

<span data-ttu-id="1b3bb-152">Wykonaj te toolearn łącza więcej informacji na temat zarządzania Centrum IoT Azure:</span><span class="sxs-lookup"><span data-stu-id="1b3bb-152">Follow these links toolearn more about managing Azure IoT Hub:</span></span>

* <span data-ttu-id="1b3bb-153">[Zbiorcze zarządzania urządzeniami IoT][lnk-bulk]</span><span class="sxs-lookup"><span data-stu-id="1b3bb-153">[Bulk manage IoT devices][lnk-bulk]</span></span>
* <span data-ttu-id="1b3bb-154">[Metryki Centrum IoT][lnk-metrics]</span><span class="sxs-lookup"><span data-stu-id="1b3bb-154">[IoT Hub metrics][lnk-metrics]</span></span>
* <span data-ttu-id="1b3bb-155">[Operacje monitorowania][lnk-monitor]</span><span class="sxs-lookup"><span data-stu-id="1b3bb-155">[Operations monitoring][lnk-monitor]</span></span>

<span data-ttu-id="1b3bb-156">toofurther Poznaj możliwości hello Centrum IoT, zobacz:</span><span class="sxs-lookup"><span data-stu-id="1b3bb-156">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="1b3bb-157">[Przewodnik dewelopera Centrum IoT][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="1b3bb-157">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="1b3bb-158">[Symuluje urządzenia IoT krawędzi][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="1b3bb-158">[Simulating a device with IoT Edge][lnk-iotedge]</span></span>
* <span data-ttu-id="1b3bb-159">[Zabezpieczanie rozwiązania IoT z hello tła w][lnk-securing]</span><span class="sxs-lookup"><span data-stu-id="1b3bb-159">[Secure your IoT solution from hello ground up][lnk-securing]</span></span>

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