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
# <a name="configure-iot-hub-file-uploads-using-powershell"></a><span data-ttu-id="6f62b-104">Konfigurowanie Centrum IoT przekazywania plików przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="6f62b-104">Configure IoT Hub file uploads using PowerShell</span></span>

[!INCLUDE [iot-hub-file-upload-selector](../../includes/iot-hub-file-upload-selector.md)]

<span data-ttu-id="6f62b-105">Witaj toouse [plików funkcji przekazywania w Centrum IoT][lnk-upload], należy najpierw powiązać konta magazynu platformy Azure z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="6f62b-105">toouse hello [file upload functionality in IoT Hub][lnk-upload], you must first associate an Azure storage account with your IoT hub.</span></span> <span data-ttu-id="6f62b-106">Możesz użyć istniejącego konta magazynu lub Utwórz nową.</span><span class="sxs-lookup"><span data-stu-id="6f62b-106">You can use an existing storage account or create a new one.</span></span>

<span data-ttu-id="6f62b-107">toocomplete tego samouczka należy hello następujące:</span><span class="sxs-lookup"><span data-stu-id="6f62b-107">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="6f62b-108">Aktywne konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="6f62b-108">An active Azure account.</span></span> <span data-ttu-id="6f62b-109">Jeśli go nie masz, możesz utworzyć [bezpłatne konto][lnk-free-trial] w zaledwie kilka minut.</span><span class="sxs-lookup"><span data-stu-id="6f62b-109">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="6f62b-110">[Polecenia cmdlet programu PowerShell systemu Azure][lnk-powershell-install].</span><span class="sxs-lookup"><span data-stu-id="6f62b-110">[Azure PowerShell cmdlets][lnk-powershell-install].</span></span>
* <span data-ttu-id="6f62b-111">Centrum Azure IoT.</span><span class="sxs-lookup"><span data-stu-id="6f62b-111">An Azure IoT hub.</span></span> <span data-ttu-id="6f62b-112">Jeśli nie masz Centrum IoT, możesz użyć hello [polecenia cmdlet New-AzureRmIoTHub] [ lnk-powershell-iothub] toocreate jeden lub użyj hello portalu zbyt[tworzenia Centrum IoT] [ lnk-portal-hub].</span><span class="sxs-lookup"><span data-stu-id="6f62b-112">If you don't have an IoT hub, you can use hello [New-AzureRmIoTHub cmdlet][lnk-powershell-iothub] toocreate one or use hello portal too[Create an IoT hub][lnk-portal-hub].</span></span>
* <span data-ttu-id="6f62b-113">Konto usługi Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="6f62b-113">An Azure storage account.</span></span> <span data-ttu-id="6f62b-114">Jeśli nie masz konta magazynu platformy Azure, możesz użyć hello [poleceń cmdlet programu PowerShell magazynu Azure] [ lnk-powershell-storage] toocreate jeden lub użyj hello portalu zbyt[Utwórz konto magazynu] [ lnk-portal-storage].</span><span class="sxs-lookup"><span data-stu-id="6f62b-114">If you don't have an Azure storage account, you can use hello [Azure Storage PowerShell cmdlets][lnk-powershell-storage] toocreate one or use hello portal too[Create a storage account][lnk-portal-storage].</span></span>

## <a name="sign-in-and-set-your-azure-account"></a><span data-ttu-id="6f62b-115">Zaloguj się i ustawić konta platformy Azure</span><span class="sxs-lookup"><span data-stu-id="6f62b-115">Sign in and set your Azure account</span></span>

<span data-ttu-id="6f62b-116">Zaloguj się tooyour konto platformy Azure i wyboru subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="6f62b-116">Sign in tooyour Azure account and select your subscription.</span></span>

1. <span data-ttu-id="6f62b-117">W wierszu polecenia programu PowerShell hello, uruchom hello **Login-AzureRmAccount** polecenia cmdlet:</span><span class="sxs-lookup"><span data-stu-id="6f62b-117">At hello PowerShell prompt, run hello **Login-AzureRmAccount** cmdlet:</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

1. <span data-ttu-id="6f62b-118">Jeśli masz wiele subskrypcji Azure, logowanie tooAzure umożliwiają dostęp tooall hello subskrypcji platformy Azure skojarzonych z poświadczeniami użytkownika.</span><span class="sxs-lookup"><span data-stu-id="6f62b-118">If you have multiple Azure subscriptions, signing in tooAzure grants you access tooall hello Azure subscriptions associated with your credentials.</span></span> <span data-ttu-id="6f62b-119">Użyj następującego polecenia toolist hello subskrypcji platformy Azure, dostępne dla Ciebie toouse hello:</span><span class="sxs-lookup"><span data-stu-id="6f62b-119">Use hello following command toolist hello Azure subscriptions available for you toouse:</span></span>

    ```powershell
    Get-AzureRMSubscription
    ```

    <span data-ttu-id="6f62b-120">Użyj następującego polecenia tooselect subskrypcji ma się, że toouse toorun hello polecenia toomanage Centrum IoT hello.</span><span class="sxs-lookup"><span data-stu-id="6f62b-120">Use hello following command tooselect subscription that you want toouse toorun hello commands toomanage your IoT hub.</span></span> <span data-ttu-id="6f62b-121">Identyfikator lub Nazwa subskrypcji hello można użyć z danych wyjściowych hello hello poprzednie polecenie:</span><span class="sxs-lookup"><span data-stu-id="6f62b-121">You can use either hello subscription name or ID from hello output of hello previous command:</span></span>

    ```powershell
    Select-AzureRMSubscription `
        -SubscriptionName "{your subscription name}"
    ```

## <a name="retrieve-your-storage-account-details"></a><span data-ttu-id="6f62b-122">Pobieranie informacji o koncie magazynu</span><span class="sxs-lookup"><span data-stu-id="6f62b-122">Retrieve your storage account details</span></span>

<span data-ttu-id="6f62b-123">Hello kroków założono, że utworzone konto magazynu przy użyciu hello **Resource Manager** modelu wdrażania i nie hello **klasycznego** modelu wdrażania.</span><span class="sxs-lookup"><span data-stu-id="6f62b-123">hello following steps assume that you created your storage account using hello **Resource Manager** deployment model, and not hello **Classic** deployment model.</span></span>

<span data-ttu-id="6f62b-124">Plik tooconfigure przekazuje z urządzeń, należy hello parametry połączenia dla konta magazynu platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="6f62b-124">tooconfigure file uploads from your devices, you need hello connection string for an Azure storage account.</span></span> <span data-ttu-id="6f62b-125">Konto magazynu Hello musi znajdować się w hello tej samej subskrypcji co Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="6f62b-125">hello storage account must be in hello same subscription as your IoT hub.</span></span> <span data-ttu-id="6f62b-126">Należy również hello nazwa kontenera obiektów blob na koncie magazynu hello.</span><span class="sxs-lookup"><span data-stu-id="6f62b-126">You also need hello name of a blob container in hello storage account.</span></span> <span data-ttu-id="6f62b-127">Użyj następującego polecenia tooretrieve hello kluczy konta magazynu:</span><span class="sxs-lookup"><span data-stu-id="6f62b-127">Use hello following command tooretrieve your storage account keys:</span></span>

```powershell
Get-AzureRmStorageAccountKey `
  -Name {your storage account name} `
  -ResourceGroupName {your storage account resource group}
```

<span data-ttu-id="6f62b-128">Zanotuj hello **klucz1** wartość klucza konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="6f62b-128">Make a note of hello **key1** storage account key value.</span></span> <span data-ttu-id="6f62b-129">Należy go hello następujące kroki.</span><span class="sxs-lookup"><span data-stu-id="6f62b-129">You need it in hello following steps.</span></span>

<span data-ttu-id="6f62b-130">Można użyć istniejącego kontenera obiektów blob z przekazywania plików lub Utwórz nowe:</span><span class="sxs-lookup"><span data-stu-id="6f62b-130">You can either use an existing blob container for your file uploads or create new one:</span></span>

* <span data-ttu-id="6f62b-131">toolist hello istniejących kontenerów obiektów blob na koncie magazynu, należy użyć hello następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="6f62b-131">toolist hello existing blob containers in your storage account, use hello following commands:</span></span>

    ```powershell
    $ctx = New-AzureStorageContext `
        -StorageAccountName {your storage account name} `
        -StorageAccountKey {your storage account key}
    Get-AzureStorageContainer -Context $ctx
    ```

* <span data-ttu-id="6f62b-132">toocreate kontenera obiektów blob na koncie magazynu hello Użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="6f62b-132">toocreate a blob container in your storage account, use hello following commands:</span></span>

    ```powershell
    $ctx = New-AzureStorageContext `
        -StorageAccountName {your storage account name} `
        -StorageAccountKey {your storage account key}
    New-AzureStorageContainer `
        -Name {your new container name} `
        -Permission Off `
        -Context $ctx
    ```

## <a name="configure-your-iot-hub"></a><span data-ttu-id="6f62b-133">Konfigurowanie Centrum IoT</span><span class="sxs-lookup"><span data-stu-id="6f62b-133">Configure your IoT hub</span></span>

<span data-ttu-id="6f62b-134">Można teraz skonfigurować Twoje tooenable Centrum IoT [plików funkcji przekazywania] [ lnk-upload] przy użyciu informacji o koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="6f62b-134">You can now configure your IoT hub tooenable [file upload functionality][lnk-upload] using your storage account details.</span></span>

<span data-ttu-id="6f62b-135">Konfiguracja Hello wymaga hello następujące wartości:</span><span class="sxs-lookup"><span data-stu-id="6f62b-135">hello configuration requires hello following values:</span></span>

<span data-ttu-id="6f62b-136">**Kontener magazynu**: kontener obiektów blob na koncie magazynu Azure w Twojej bieżącej subskrypcji platformy Azure tooassociate z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="6f62b-136">**Storage container**: A blob container in an Azure storage account in your current Azure subscription tooassociate with your IoT hub.</span></span> <span data-ttu-id="6f62b-137">Można pobrać informacji o koncie magazynu niezbędne hello w powyższej sekcji hello.</span><span class="sxs-lookup"><span data-stu-id="6f62b-137">You retrieved hello necessary storage account information in hello preceding section.</span></span> <span data-ttu-id="6f62b-138">Centrum IoT automatycznie generuje identyfikator URI SAS z kontenera obiektów blob toothis uprawnienia zapisu dla urządzeń toouse podczas ich przekazywania plików.</span><span class="sxs-lookup"><span data-stu-id="6f62b-138">IoT Hub automatically generates SAS URIs with write permissions toothis blob container for devices toouse when they upload files.</span></span>

<span data-ttu-id="6f62b-139">**Odbieranie powiadomień dla przekazanych plików**: Włącz lub Wyłącz powiadomienia o przekazywania plików.</span><span class="sxs-lookup"><span data-stu-id="6f62b-139">**Receive notifications for uploaded files**: Enable or disable file upload notifications.</span></span>

<span data-ttu-id="6f62b-140">**Czas wygaśnięcia SAS**: to ustawienie jest hello time-to-live z hello identyfikatorów URI SAS zwrócony toohello urządzenia przez Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="6f62b-140">**SAS TTL**: This setting is hello time-to-live of hello SAS URIs returned toohello device by IoT Hub.</span></span> <span data-ttu-id="6f62b-141">Domyślnie tooone godzinę.</span><span class="sxs-lookup"><span data-stu-id="6f62b-141">Set tooone hour by default.</span></span>

<span data-ttu-id="6f62b-142">**Plik powiadomienia, ustawienia domyślne TTL**: hello time-to-live powiadomienia przekazywania pliku przed jego wygaśnięciem.</span><span class="sxs-lookup"><span data-stu-id="6f62b-142">**File notification settings default TTL**: hello time-to-live of a file upload notification before it is expired.</span></span> <span data-ttu-id="6f62b-143">Domyślnie tooone dnia.</span><span class="sxs-lookup"><span data-stu-id="6f62b-143">Set tooone day by default.</span></span>

<span data-ttu-id="6f62b-144">**Powiadomienie dostarczania maksymalna liczba plików**: hello liczba hello Centrum IoT prób toodeliver powiadomienie przekazywania plików.</span><span class="sxs-lookup"><span data-stu-id="6f62b-144">**File notification maximum delivery count**: hello number of times hello IoT Hub attempts toodeliver a file upload notification.</span></span> <span data-ttu-id="6f62b-145">Domyślnie too10.</span><span class="sxs-lookup"><span data-stu-id="6f62b-145">Set too10 by default.</span></span>

<span data-ttu-id="6f62b-146">Użyj następującego ustawienia przekazywania plików hello tooconfigure polecenia cmdlet programu PowerShell w Centrum IoT hello:</span><span class="sxs-lookup"><span data-stu-id="6f62b-146">Use hello following PowerShell cmdlet tooconfigure hello file upload settings on your IoT hub:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="6f62b-147">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="6f62b-147">Next steps</span></span>

<span data-ttu-id="6f62b-148">Aby uzyskać więcej informacji na temat możliwości przekazywania plików hello Centrum IoT, zobacz [przekazywania plików z urządzeniem][lnk-upload].</span><span class="sxs-lookup"><span data-stu-id="6f62b-148">For more information about hello file upload capabilities of IoT Hub, see [Upload files from a device][lnk-upload].</span></span>

<span data-ttu-id="6f62b-149">Wykonaj te toolearn łącza więcej informacji na temat zarządzania Centrum IoT Azure:</span><span class="sxs-lookup"><span data-stu-id="6f62b-149">Follow these links toolearn more about managing Azure IoT Hub:</span></span>

* <span data-ttu-id="6f62b-150">[Zbiorcze zarządzania urządzeniami IoT][lnk-bulk]</span><span class="sxs-lookup"><span data-stu-id="6f62b-150">[Bulk manage IoT devices][lnk-bulk]</span></span>
* <span data-ttu-id="6f62b-151">[Metryki Centrum IoT][lnk-metrics]</span><span class="sxs-lookup"><span data-stu-id="6f62b-151">[IoT Hub metrics][lnk-metrics]</span></span>
* <span data-ttu-id="6f62b-152">[Operacje monitorowania][lnk-monitor]</span><span class="sxs-lookup"><span data-stu-id="6f62b-152">[Operations monitoring][lnk-monitor]</span></span>

<span data-ttu-id="6f62b-153">toofurther Poznaj możliwości hello Centrum IoT, zobacz:</span><span class="sxs-lookup"><span data-stu-id="6f62b-153">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="6f62b-154">[Przewodnik dewelopera Centrum IoT][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="6f62b-154">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="6f62b-155">[Symuluje urządzenia IoT krawędzi][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="6f62b-155">[Simulating a device with IoT Edge][lnk-iotedge]</span></span>
* <span data-ttu-id="6f62b-156">[Zabezpieczanie rozwiązania IoT z hello tła w][lnk-securing]</span><span class="sxs-lookup"><span data-stu-id="6f62b-156">[Secure your IoT solution from hello ground up][lnk-securing]</span></span>

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