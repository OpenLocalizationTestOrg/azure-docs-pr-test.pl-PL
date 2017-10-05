---
title: "Konfigurowanie przekazywania pliku z Centrum IoT przy użyciu wiersza polecenia platformy Azure (az.py) | Dokumentacja firmy Microsoft"
description: "Jak skonfigurować fileuploads z Centrum IoT Azure przy użyciu interfejsu wiersza polecenia Azure i platform w 2.0 (az.py)."
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
ms.openlocfilehash: a9af26d7ebacf5513952786621aaa92f64be263b
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="configure-iot-hub-file-uploads-using-azure-cli"></a><span data-ttu-id="0d7b7-103">Konfigurowanie Centrum IoT przekazywania plików przy użyciu wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="0d7b7-103">Configure IoT Hub file uploads using Azure CLI</span></span>

[!INCLUDE [iot-hub-file-upload-selector](../../includes/iot-hub-file-upload-selector.md)]

<span data-ttu-id="0d7b7-104">Aby użyć [plików funkcji przekazywania w Centrum IoT][lnk-upload], należy najpierw powiązać konta usługi Azure Storage z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="0d7b7-104">To use the [file upload functionality in IoT Hub][lnk-upload], you must first associate an Azure Storage account with your IoT hub.</span></span> <span data-ttu-id="0d7b7-105">Możesz użyć istniejącego konta magazynu lub Utwórz nową.</span><span class="sxs-lookup"><span data-stu-id="0d7b7-105">You can use an existing storage account or create a new one.</span></span>

<span data-ttu-id="0d7b7-106">Do wykonania kroków tego samouczka niezbędne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="0d7b7-106">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="0d7b7-107">Aktywne konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="0d7b7-107">An active Azure account.</span></span> <span data-ttu-id="0d7b7-108">Jeśli go nie masz, możesz utworzyć [bezpłatne konto][lnk-free-trial] w zaledwie kilka minut.</span><span class="sxs-lookup"><span data-stu-id="0d7b7-108">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="0d7b7-109">[Azure CLI 2.0][lnk-CLI-install].</span><span class="sxs-lookup"><span data-stu-id="0d7b7-109">[Azure CLI 2.0][lnk-CLI-install].</span></span>
* <span data-ttu-id="0d7b7-110">Centrum Azure IoT.</span><span class="sxs-lookup"><span data-stu-id="0d7b7-110">An Azure IoT hub.</span></span> <span data-ttu-id="0d7b7-111">Jeśli nie masz Centrum IoT, możesz użyć `az iot hub create` [polecenia] [ lnk-cli-create-iothub] można utworzyć jeden lub za pomocą portalu [tworzenia Centrum IoT] [lnk-portal Centrum].</span><span class="sxs-lookup"><span data-stu-id="0d7b7-111">If you don't have an IoT hub, you can use the `az iot hub create` [command][lnk-cli-create-iothub] to create one or use the portal to [Create an IoT hub][lnk-portal-hub].</span></span>
* <span data-ttu-id="0d7b7-112">Konto magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="0d7b7-112">An Azure Storage account.</span></span> <span data-ttu-id="0d7b7-113">Jeśli nie masz konta usługi Azure Storage, możesz użyć [2.0 interfejsu wiersza polecenia platformy Azure — Zarządzanie kontami magazynu] [ lnk-manage-storage] można utworzyć jeden lub Portal umożliwia [Utwórz konto magazynu][lnk-portal-storage].</span><span class="sxs-lookup"><span data-stu-id="0d7b7-113">If you don't have an Azure Storage account, you can use the [Azure CLI 2.0 - Manage storage accounts][lnk-manage-storage] to create one or use the portal to [Create a storage account][lnk-portal-storage].</span></span>

## <a name="sign-in-and-set-your-azure-account"></a><span data-ttu-id="0d7b7-114">Zaloguj się i ustawić konta platformy Azure</span><span class="sxs-lookup"><span data-stu-id="0d7b7-114">Sign in and set your Azure account</span></span>

<span data-ttu-id="0d7b7-115">Zaloguj się do konta platformy Azure i wyboru subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="0d7b7-115">Sign in to your Azure account and select your subscription.</span></span>

1. <span data-ttu-id="0d7b7-116">W wierszu polecenia Uruchom [polecenia logowania][lnk-login-command]:</span><span class="sxs-lookup"><span data-stu-id="0d7b7-116">At the command prompt, run the [login command][lnk-login-command]:</span></span>

    ```azurecli
    az login
    ```

    <span data-ttu-id="0d7b7-117">Postępuj zgodnie z instrukcjami w celu uwierzytelnienia przy użyciu kodu i zaloguj się do konta platformy Azure za pośrednictwem przeglądarki sieci web.</span><span class="sxs-lookup"><span data-stu-id="0d7b7-117">Follow the instructions to authenticate using the code and sign in to your Azure account through a web browser.</span></span>

1. <span data-ttu-id="0d7b7-118">Jeśli masz wiele subskrypcji Azure, logowanie do platformy Azure przydziela dostęp do wszystkich kont platformy Azure skojarzone z poświadczeniami użytkownika.</span><span class="sxs-lookup"><span data-stu-id="0d7b7-118">If you have multiple Azure subscriptions, signing in to Azure grants you access to all the Azure accounts associated with your credentials.</span></span> <span data-ttu-id="0d7b7-119">Należy użyć następującego [polecenia do listy kont Azure] [ lnk-az-account-command] dostępne do użycia:</span><span class="sxs-lookup"><span data-stu-id="0d7b7-119">Use the following [command to list the Azure accounts][lnk-az-account-command] available for you to use:</span></span>

    ```azurecli
    az account list
    ```

    <span data-ttu-id="0d7b7-120">Użyj następującego polecenia, aby wybrać subskrypcję, która ma być używany do uruchamiania poleceń, aby utworzyć Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="0d7b7-120">Use the following command to select subscription that you want to use to run the commands to create your IoT hub.</span></span> <span data-ttu-id="0d7b7-121">Przy użyciu subskrypcji nazwa lub identyfikator z danych wyjściowych poprzednie polecenie:</span><span class="sxs-lookup"><span data-stu-id="0d7b7-121">You can use either the subscription name or ID from the output of the previous command:</span></span>

    ```azurecli
    az account set --subscription {your subscription name or id}
    ```

## <a name="retrieve-your-storage-account-details"></a><span data-ttu-id="0d7b7-122">Pobieranie informacji o koncie magazynu</span><span class="sxs-lookup"><span data-stu-id="0d7b7-122">Retrieve your storage account details</span></span>

<span data-ttu-id="0d7b7-123">W następujących krokach założono, używając konta magazynu utworzone **Resource Manager** modelu wdrażania i nie **klasycznego** modelu wdrażania.</span><span class="sxs-lookup"><span data-stu-id="0d7b7-123">The following steps assume that you created your storage account using the **Resource Manager** deployment model, and not the **Classic** deployment model.</span></span>

<span data-ttu-id="0d7b7-124">Aby skonfigurować przekazywania plików z urządzeń, należy parametry połączenia dla konta magazynu platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="0d7b7-124">To configure file uploads from your devices, you need the connection string for an Azure storage account.</span></span> <span data-ttu-id="0d7b7-125">Konta magazynu musi być w tej samej subskrypcji co Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="0d7b7-125">The storage account must be in the same subscription as your IoT hub.</span></span> <span data-ttu-id="0d7b7-126">Należy również nazwę kontenera obiektów blob na koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="0d7b7-126">You also need the name of a blob container in the storage account.</span></span> <span data-ttu-id="0d7b7-127">Aby pobrać kluczy konta magazynu, użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="0d7b7-127">Use the following command to retrieve your storage account keys:</span></span>

```azurecli
az storage account show-connection-string --name {your storage account name} --resource-group {your storage account resource group}
```

<span data-ttu-id="0d7b7-128">Zanotuj **connectionString** wartość.</span><span class="sxs-lookup"><span data-stu-id="0d7b7-128">Make a note of the **connectionString** value.</span></span> <span data-ttu-id="0d7b7-129">Należy go w kolejnych krokach.</span><span class="sxs-lookup"><span data-stu-id="0d7b7-129">You need it in the following steps.</span></span>

<span data-ttu-id="0d7b7-130">Można użyć istniejącego kontenera obiektów blob z przekazywania plików lub Utwórz nowe:</span><span class="sxs-lookup"><span data-stu-id="0d7b7-130">You can either use an existing blob container for your file uploads or create new one:</span></span>

* <span data-ttu-id="0d7b7-131">Aby wyświetlić listę istniejących kontenerów obiektów blob na koncie magazynu, użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="0d7b7-131">To list the existing blob containers in your storage account, use the following command:</span></span>

    ```azurecli
    az storage container list --connection-string "{your storage account connection string}"
    ```

* <span data-ttu-id="0d7b7-132">Aby utworzyć kontener obiektów blob na koncie magazynu, użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="0d7b7-132">To create a blob container in your storage account, use the following command:</span></span>

    ```azurecli
    az storage container create --name {container name} --connection-string "{your storage account connection string}"
    ```

## <a name="file-upload"></a><span data-ttu-id="0d7b7-133">Przekazywanie pliku</span><span class="sxs-lookup"><span data-stu-id="0d7b7-133">File upload</span></span>

<span data-ttu-id="0d7b7-134">Aby włączyć Centrum IoT można teraz skonfigurować [plików funkcji przekazywania] [ lnk-upload] przy użyciu informacji o koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="0d7b7-134">You can now configure your IoT hub to enable [file upload functionality][lnk-upload] using your storage account details.</span></span>

<span data-ttu-id="0d7b7-135">Konfiguracja wymaga następujących wartości:</span><span class="sxs-lookup"><span data-stu-id="0d7b7-135">The configuration requires the following values:</span></span>

<span data-ttu-id="0d7b7-136">**Kontener magazynu**: kontener obiektów blob na koncie magazynu Azure w Twojej bieżącej subskrypcji platformy Azure do skojarzenia z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="0d7b7-136">**Storage container**: A blob container in an Azure storage account in your current Azure subscription to associate with your IoT hub.</span></span> <span data-ttu-id="0d7b7-137">Możesz pobrać informacje o koncie magazynu niezbędne w poprzedniej sekcji.</span><span class="sxs-lookup"><span data-stu-id="0d7b7-137">You retrieved the necessary storage account information in the preceding section.</span></span> <span data-ttu-id="0d7b7-138">Centrum IoT automatycznie generuje identyfikator URI sygnatury dostępu Współdzielonego z uprawnieniami do zapisu do tego kontenera obiektów blob dla urządzeń do użycia podczas ich przekazywania plików.</span><span class="sxs-lookup"><span data-stu-id="0d7b7-138">IoT Hub automatically generates SAS URIs with write permissions to this blob container for devices to use when they upload files.</span></span>

<span data-ttu-id="0d7b7-139">**Odbieranie powiadomień dla przekazanych plików**: Włącz lub Wyłącz powiadomienia o przekazywania plików.</span><span class="sxs-lookup"><span data-stu-id="0d7b7-139">**Receive notifications for uploaded files**: Enable or disable file upload notifications.</span></span>

<span data-ttu-id="0d7b7-140">**Czas wygaśnięcia SAS**: to ustawienie jest time-to-live identyfikatorów SAS zwrócony do urządzenia przez Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="0d7b7-140">**SAS TTL**: This setting is the time-to-live of the SAS URIs returned to the device by IoT Hub.</span></span> <span data-ttu-id="0d7b7-141">Domyślnie do godzinę.</span><span class="sxs-lookup"><span data-stu-id="0d7b7-141">Set to one hour by default.</span></span>

<span data-ttu-id="0d7b7-142">**Plik powiadomienia, ustawienia domyślne TTL**: czas wygaśnięcia pliku Przekaż powiadomienia przed jego wygaśnięciem.</span><span class="sxs-lookup"><span data-stu-id="0d7b7-142">**File notification settings default TTL**: The time-to-live of a file upload notification before it is expired.</span></span> <span data-ttu-id="0d7b7-143">Domyślnie na jeden dzień.</span><span class="sxs-lookup"><span data-stu-id="0d7b7-143">Set to one day by default.</span></span>

<span data-ttu-id="0d7b7-144">**Powiadomienie dostarczania maksymalna liczba plików**: liczba prób Centrum IoT dostarczyć plik Przekaż powiadomień.</span><span class="sxs-lookup"><span data-stu-id="0d7b7-144">**File notification maximum delivery count**: The number of times the IoT Hub attempts to deliver a file upload notification.</span></span> <span data-ttu-id="0d7b7-145">Domyślnie do 10.</span><span class="sxs-lookup"><span data-stu-id="0d7b7-145">Set to 10 by default.</span></span>

<span data-ttu-id="0d7b7-146">Użyj następujących poleceń interfejsu wiersza polecenia Azure, aby skonfigurować ustawienia przekazywania pliku w Centrum IoT:</span><span class="sxs-lookup"><span data-stu-id="0d7b7-146">Use the following Azure CLI commands to configure the file upload settings on your IoT hub:</span></span>

<span data-ttu-id="0d7b7-147">Użycie powłoki bash:</span><span class="sxs-lookup"><span data-stu-id="0d7b7-147">In a bash shell use:</span></span>

```azurecli
az iot hub update --name {your iot hub name} --set properties.storageEndpoints.'$default'.connectionString="{your storage account connection string}"
az iot hub update --name {your iot hub name} --set properties.storageEndpoints.'$default'.containerName="{your storage container name}"
az iot hub update --name {your iot hub name} --set properties.storageEndpoints.'$default'.sasTtlAsIso8601=PT1H0M0S

az iot hub update --name {your iot hub name} --set properties.enableFileUploadNotifications=true
az iot hub update --name {your iot hub name} --set properties.messagingEndpoints.fileNotifications.maxDeliveryCount=10
az iot hub update --name {your iot hub name} --set properties.messagingEndpoints.fileNotifications.ttlAsIso8601=PT1H0M0S
```

<span data-ttu-id="0d7b7-148">W przypadku systemu Windows użyj wiersza polecenia:</span><span class="sxs-lookup"><span data-stu-id="0d7b7-148">At a Windows command prompt use:</span></span>

```azurecli
az iot hub update --name {your iot hub name} --set "properties.storageEndpoints.$default.connectionString="{your storage account connection string}""
az iot hub update --name {your iot hub name} --set "properties.storageEndpoints.$default.containerName="{your storage container name}""
az iot hub update --name {your iot hub name} --set "properties.storageEndpoints.$default.sasTtlAsIso8601=PT1H0M0S"

az iot hub update --name {your iot hub name} --set properties.enableFileUploadNotifications=true
az iot hub update --name {your iot hub name} --set properties.messagingEndpoints.fileNotifications.maxDeliveryCount=10
az iot hub update --name {your iot hub name} --set properties.messagingEndpoints.fileNotifications.ttlAsIso8601=PT1H0M0S
```

<span data-ttu-id="0d7b7-149">Możesz przejrzeć konfigurację przekazywania pliku, na Centrum IoT przy użyciu następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="0d7b7-149">You can review the file upload configuration on your IoT hub using the following command:</span></span>

```azurecli
az iot hub show --name {your iot hub name}
```

## <a name="next-steps"></a><span data-ttu-id="0d7b7-150">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="0d7b7-150">Next steps</span></span>

<span data-ttu-id="0d7b7-151">Aby uzyskać więcej informacji na temat możliwości przekazywania plików Centrum IoT, zobacz [przekazywania plików z urządzeniem][lnk-upload].</span><span class="sxs-lookup"><span data-stu-id="0d7b7-151">For more information about the file upload capabilities of IoT Hub, see [Upload files from a device][lnk-upload].</span></span>

<span data-ttu-id="0d7b7-152">Skorzystaj z poniższych linków, aby dowiedzieć się więcej o zarządzaniu Centrum IoT Azure:</span><span class="sxs-lookup"><span data-stu-id="0d7b7-152">Follow these links to learn more about managing Azure IoT Hub:</span></span>

* <span data-ttu-id="0d7b7-153">[Zbiorcze zarządzania urządzeniami IoT][lnk-bulk]</span><span class="sxs-lookup"><span data-stu-id="0d7b7-153">[Bulk manage IoT devices][lnk-bulk]</span></span>
* <span data-ttu-id="0d7b7-154">[Metryki Centrum IoT][lnk-metrics]</span><span class="sxs-lookup"><span data-stu-id="0d7b7-154">[IoT Hub metrics][lnk-metrics]</span></span>
* <span data-ttu-id="0d7b7-155">[Operacje monitorowania][lnk-monitor]</span><span class="sxs-lookup"><span data-stu-id="0d7b7-155">[Operations monitoring][lnk-monitor]</span></span>

<span data-ttu-id="0d7b7-156">Aby dokładniej analizować możliwości Centrum IoT, zobacz:</span><span class="sxs-lookup"><span data-stu-id="0d7b7-156">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="0d7b7-157">[Przewodnik dewelopera Centrum IoT][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="0d7b7-157">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="0d7b7-158">[Symuluje urządzenia IoT krawędzi][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="0d7b7-158">[Simulating a device with IoT Edge][lnk-iotedge]</span></span>
* <span data-ttu-id="0d7b7-159">[Zabezpieczanie rozwiązania IoT od podstaw w górę][lnk-securing]</span><span class="sxs-lookup"><span data-stu-id="0d7b7-159">[Secure your IoT solution from the ground up][lnk-securing]</span></span>

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