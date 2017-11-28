---
title: "Umożliwia skonfigurowanie przekazywania pliku programu Azure PowerShell | Dokumentacja firmy Microsoft"
description: "Sposób użycia poleceń cmdlet programu Azure PowerShell do konfigurowania Centrum IoT włączyć plik zostanie przesłany z połączonych urządzeń. Zawiera informacje o konfigurowaniu docelowym kontem magazynu platformy Azure."
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
ms.openlocfilehash: a72bda794b2da3e044c46249559610d06b1f1843
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="configure-iot-hub-file-uploads-using-powershell"></a><span data-ttu-id="709a1-104">Konfigurowanie Centrum IoT przekazywania plików przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="709a1-104">Configure IoT Hub file uploads using PowerShell</span></span>

[!INCLUDE [iot-hub-file-upload-selector](../../includes/iot-hub-file-upload-selector.md)]

<span data-ttu-id="709a1-105">Aby użyć [plików funkcji przekazywania w Centrum IoT][lnk-upload], należy najpierw powiązać konta magazynu platformy Azure z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="709a1-105">To use the [file upload functionality in IoT Hub][lnk-upload], you must first associate an Azure storage account with your IoT hub.</span></span> <span data-ttu-id="709a1-106">Możesz użyć istniejącego konta magazynu lub Utwórz nową.</span><span class="sxs-lookup"><span data-stu-id="709a1-106">You can use an existing storage account or create a new one.</span></span>

<span data-ttu-id="709a1-107">Do wykonania kroków tego samouczka niezbędne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="709a1-107">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="709a1-108">Aktywne konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="709a1-108">An active Azure account.</span></span> <span data-ttu-id="709a1-109">Jeśli go nie masz, możesz utworzyć [bezpłatne konto][lnk-free-trial] w zaledwie kilka minut.</span><span class="sxs-lookup"><span data-stu-id="709a1-109">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="709a1-110">[Polecenia cmdlet programu PowerShell systemu Azure][lnk-powershell-install].</span><span class="sxs-lookup"><span data-stu-id="709a1-110">[Azure PowerShell cmdlets][lnk-powershell-install].</span></span>
* <span data-ttu-id="709a1-111">Centrum Azure IoT.</span><span class="sxs-lookup"><span data-stu-id="709a1-111">An Azure IoT hub.</span></span> <span data-ttu-id="709a1-112">Jeśli nie masz Centrum IoT, możesz użyć [polecenia cmdlet New-AzureRmIoTHub] [ lnk-powershell-iothub] można utworzyć jeden lub Portal umożliwia [tworzenia Centrum IoT][lnk-portal-hub].</span><span class="sxs-lookup"><span data-stu-id="709a1-112">If you don't have an IoT hub, you can use the [New-AzureRmIoTHub cmdlet][lnk-powershell-iothub] to create one or use the portal to [Create an IoT hub][lnk-portal-hub].</span></span>
* <span data-ttu-id="709a1-113">Konto usługi Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="709a1-113">An Azure storage account.</span></span> <span data-ttu-id="709a1-114">Jeśli nie masz konta magazynu platformy Azure, możesz użyć [poleceń cmdlet programu PowerShell magazynu Azure] [ lnk-powershell-storage] można utworzyć jeden lub Portal umożliwia [Utwórz konto magazynu] [lnk-portal-storage].</span><span class="sxs-lookup"><span data-stu-id="709a1-114">If you don't have an Azure storage account, you can use the [Azure Storage PowerShell cmdlets][lnk-powershell-storage] to create one or use the portal to [Create a storage account][lnk-portal-storage].</span></span>

## <a name="sign-in-and-set-your-azure-account"></a><span data-ttu-id="709a1-115">Zaloguj się i ustawić konta platformy Azure</span><span class="sxs-lookup"><span data-stu-id="709a1-115">Sign in and set your Azure account</span></span>

<span data-ttu-id="709a1-116">Zaloguj się do konta platformy Azure i wyboru subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="709a1-116">Sign in to your Azure account and select your subscription.</span></span>

1. <span data-ttu-id="709a1-117">W wierszu polecenia programu PowerShell, uruchom **Login-AzureRmAccount** polecenia cmdlet:</span><span class="sxs-lookup"><span data-stu-id="709a1-117">At the PowerShell prompt, run the **Login-AzureRmAccount** cmdlet:</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

1. <span data-ttu-id="709a1-118">Jeśli masz wiele subskrypcji Azure, logowanie do platformy Azure udziela dostępu do subskrypcji platformy Azure skojarzone z poświadczeniami użytkownika.</span><span class="sxs-lookup"><span data-stu-id="709a1-118">If you have multiple Azure subscriptions, signing in to Azure grants you access to all the Azure subscriptions associated with your credentials.</span></span> <span data-ttu-id="709a1-119">Aby wyświetlić listę dostępnych przy użyciu subskrypcji platformy Azure, użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="709a1-119">Use the following command to list the Azure subscriptions available for you to use:</span></span>

    ```powershell
    Get-AzureRMSubscription
    ```

    <span data-ttu-id="709a1-120">Użyj następującego polecenia, aby wybrać subskrypcję, która ma być używany do uruchamiania polecenia do zarządzania Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="709a1-120">Use the following command to select subscription that you want to use to run the commands to manage your IoT hub.</span></span> <span data-ttu-id="709a1-121">Przy użyciu subskrypcji nazwa lub identyfikator z danych wyjściowych poprzednie polecenie:</span><span class="sxs-lookup"><span data-stu-id="709a1-121">You can use either the subscription name or ID from the output of the previous command:</span></span>

    ```powershell
    Select-AzureRMSubscription `
        -SubscriptionName "{your subscription name}"
    ```

## <a name="retrieve-your-storage-account-details"></a><span data-ttu-id="709a1-122">Pobieranie informacji o koncie magazynu</span><span class="sxs-lookup"><span data-stu-id="709a1-122">Retrieve your storage account details</span></span>

<span data-ttu-id="709a1-123">W następujących krokach założono, używając konta magazynu utworzone **Resource Manager** modelu wdrażania i nie **klasycznego** modelu wdrażania.</span><span class="sxs-lookup"><span data-stu-id="709a1-123">The following steps assume that you created your storage account using the **Resource Manager** deployment model, and not the **Classic** deployment model.</span></span>

<span data-ttu-id="709a1-124">Aby skonfigurować przekazywania plików z urządzeń, należy parametry połączenia dla konta magazynu platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="709a1-124">To configure file uploads from your devices, you need the connection string for an Azure storage account.</span></span> <span data-ttu-id="709a1-125">Konta magazynu musi być w tej samej subskrypcji co Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="709a1-125">The storage account must be in the same subscription as your IoT hub.</span></span> <span data-ttu-id="709a1-126">Należy również nazwę kontenera obiektów blob na koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="709a1-126">You also need the name of a blob container in the storage account.</span></span> <span data-ttu-id="709a1-127">Aby pobrać kluczy konta magazynu, użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="709a1-127">Use the following command to retrieve your storage account keys:</span></span>

```powershell
Get-AzureRmStorageAccountKey `
  -Name {your storage account name} `
  -ResourceGroupName {your storage account resource group}
```

<span data-ttu-id="709a1-128">Zanotuj **klucz1** wartość klucza konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="709a1-128">Make a note of the **key1** storage account key value.</span></span> <span data-ttu-id="709a1-129">Należy go w kolejnych krokach.</span><span class="sxs-lookup"><span data-stu-id="709a1-129">You need it in the following steps.</span></span>

<span data-ttu-id="709a1-130">Można użyć istniejącego kontenera obiektów blob z przekazywania plików lub Utwórz nowe:</span><span class="sxs-lookup"><span data-stu-id="709a1-130">You can either use an existing blob container for your file uploads or create new one:</span></span>

* <span data-ttu-id="709a1-131">Aby wyświetlić listę istniejących kontenerów obiektów blob na koncie magazynu, użyj następujących poleceń:</span><span class="sxs-lookup"><span data-stu-id="709a1-131">To list the existing blob containers in your storage account, use the following commands:</span></span>

    ```powershell
    $ctx = New-AzureStorageContext `
        -StorageAccountName {your storage account name} `
        -StorageAccountKey {your storage account key}
    Get-AzureStorageContainer -Context $ctx
    ```

* <span data-ttu-id="709a1-132">Aby utworzyć kontener obiektów blob na koncie magazynu, należy użyć następujących poleceń:</span><span class="sxs-lookup"><span data-stu-id="709a1-132">To create a blob container in your storage account, use the following commands:</span></span>

    ```powershell
    $ctx = New-AzureStorageContext `
        -StorageAccountName {your storage account name} `
        -StorageAccountKey {your storage account key}
    New-AzureStorageContainer `
        -Name {your new container name} `
        -Permission Off `
        -Context $ctx
    ```

## <a name="configure-your-iot-hub"></a><span data-ttu-id="709a1-133">Konfigurowanie Centrum IoT</span><span class="sxs-lookup"><span data-stu-id="709a1-133">Configure your IoT hub</span></span>

<span data-ttu-id="709a1-134">Aby włączyć Centrum IoT można teraz skonfigurować [plików funkcji przekazywania] [ lnk-upload] przy użyciu informacji o koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="709a1-134">You can now configure your IoT hub to enable [file upload functionality][lnk-upload] using your storage account details.</span></span>

<span data-ttu-id="709a1-135">Konfiguracja wymaga następujących wartości:</span><span class="sxs-lookup"><span data-stu-id="709a1-135">The configuration requires the following values:</span></span>

<span data-ttu-id="709a1-136">**Kontener magazynu**: kontener obiektów blob na koncie magazynu Azure w Twojej bieżącej subskrypcji platformy Azure do skojarzenia z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="709a1-136">**Storage container**: A blob container in an Azure storage account in your current Azure subscription to associate with your IoT hub.</span></span> <span data-ttu-id="709a1-137">Możesz pobrać informacje o koncie magazynu niezbędne w poprzedniej sekcji.</span><span class="sxs-lookup"><span data-stu-id="709a1-137">You retrieved the necessary storage account information in the preceding section.</span></span> <span data-ttu-id="709a1-138">Centrum IoT automatycznie generuje identyfikator URI sygnatury dostępu Współdzielonego z uprawnieniami do zapisu do tego kontenera obiektów blob dla urządzeń do użycia podczas ich przekazywania plików.</span><span class="sxs-lookup"><span data-stu-id="709a1-138">IoT Hub automatically generates SAS URIs with write permissions to this blob container for devices to use when they upload files.</span></span>

<span data-ttu-id="709a1-139">**Odbieranie powiadomień dla przekazanych plików**: Włącz lub Wyłącz powiadomienia o przekazywania plików.</span><span class="sxs-lookup"><span data-stu-id="709a1-139">**Receive notifications for uploaded files**: Enable or disable file upload notifications.</span></span>

<span data-ttu-id="709a1-140">**Czas wygaśnięcia SAS**: to ustawienie jest time-to-live identyfikatorów SAS zwrócony do urządzenia przez Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="709a1-140">**SAS TTL**: This setting is the time-to-live of the SAS URIs returned to the device by IoT Hub.</span></span> <span data-ttu-id="709a1-141">Domyślnie do godzinę.</span><span class="sxs-lookup"><span data-stu-id="709a1-141">Set to one hour by default.</span></span>

<span data-ttu-id="709a1-142">**Plik powiadomienia, ustawienia domyślne TTL**: czas wygaśnięcia pliku Przekaż powiadomienia przed jego wygaśnięciem.</span><span class="sxs-lookup"><span data-stu-id="709a1-142">**File notification settings default TTL**: The time-to-live of a file upload notification before it is expired.</span></span> <span data-ttu-id="709a1-143">Domyślnie na jeden dzień.</span><span class="sxs-lookup"><span data-stu-id="709a1-143">Set to one day by default.</span></span>

<span data-ttu-id="709a1-144">**Powiadomienie dostarczania maksymalna liczba plików**: liczba prób Centrum IoT dostarczyć plik Przekaż powiadomień.</span><span class="sxs-lookup"><span data-stu-id="709a1-144">**File notification maximum delivery count**: The number of times the IoT Hub attempts to deliver a file upload notification.</span></span> <span data-ttu-id="709a1-145">Domyślnie do 10.</span><span class="sxs-lookup"><span data-stu-id="709a1-145">Set to 10 by default.</span></span>

<span data-ttu-id="709a1-146">Użyj następującego polecenia cmdlet programu PowerShell umożliwiają skonfigurowanie pliku Przekaż ustawienia Centrum IoT:</span><span class="sxs-lookup"><span data-stu-id="709a1-146">Use the following PowerShell cmdlet to configure the file upload settings on your IoT hub:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="709a1-147">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="709a1-147">Next steps</span></span>

<span data-ttu-id="709a1-148">Aby uzyskać więcej informacji na temat możliwości przekazywania plików Centrum IoT, zobacz [przekazywania plików z urządzeniem][lnk-upload].</span><span class="sxs-lookup"><span data-stu-id="709a1-148">For more information about the file upload capabilities of IoT Hub, see [Upload files from a device][lnk-upload].</span></span>

<span data-ttu-id="709a1-149">Skorzystaj z poniższych linków, aby dowiedzieć się więcej o zarządzaniu Centrum IoT Azure:</span><span class="sxs-lookup"><span data-stu-id="709a1-149">Follow these links to learn more about managing Azure IoT Hub:</span></span>

* <span data-ttu-id="709a1-150">[Zbiorcze zarządzania urządzeniami IoT][lnk-bulk]</span><span class="sxs-lookup"><span data-stu-id="709a1-150">[Bulk manage IoT devices][lnk-bulk]</span></span>
* <span data-ttu-id="709a1-151">[Metryki Centrum IoT][lnk-metrics]</span><span class="sxs-lookup"><span data-stu-id="709a1-151">[IoT Hub metrics][lnk-metrics]</span></span>
* <span data-ttu-id="709a1-152">[Operacje monitorowania][lnk-monitor]</span><span class="sxs-lookup"><span data-stu-id="709a1-152">[Operations monitoring][lnk-monitor]</span></span>

<span data-ttu-id="709a1-153">Aby dokładniej analizować możliwości Centrum IoT, zobacz:</span><span class="sxs-lookup"><span data-stu-id="709a1-153">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="709a1-154">[Przewodnik dewelopera Centrum IoT][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="709a1-154">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="709a1-155">[Symuluje urządzenia IoT krawędzi][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="709a1-155">[Simulating a device with IoT Edge][lnk-iotedge]</span></span>
* <span data-ttu-id="709a1-156">[Zabezpieczanie rozwiązania IoT od podstaw w górę][lnk-securing]</span><span class="sxs-lookup"><span data-stu-id="709a1-156">[Secure your IoT solution from the ground up][lnk-securing]</span></span>

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