---
title: Przekazywanie pliku tooconfigure portalu Azure hello aaaUse | Dokumentacja firmy Microsoft
description: "Jak toouse hello tooconfigure portalu Azure IoT hub tooenable pliku przekazuje z połączonych urządzeń. Zawiera informacje o konfigurowaniu hello miejsce docelowe konto magazynu Azure."
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
ms.date: 07/03/2017
ms.author: dobett
ms.openlocfilehash: b90c3fbed47b4eb144d3cb7480068b7cfc776ba6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-iot-hub-file-uploads-using-hello-azure-portal"></a><span data-ttu-id="e8c0e-104">Konfigurowanie Centrum IoT przekazywania plików przy użyciu hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="e8c0e-104">Configure IoT Hub file uploads using hello Azure portal</span></span>

[!INCLUDE [iot-hub-file-upload-selector](../../includes/iot-hub-file-upload-selector.md)]

## <a name="file-upload"></a><span data-ttu-id="e8c0e-105">Przekazywanie pliku</span><span class="sxs-lookup"><span data-stu-id="e8c0e-105">File upload</span></span>

<span data-ttu-id="e8c0e-106">Witaj toouse [plików funkcji przekazywania w Centrum IoT][lnk-upload], należy najpierw powiązać konta usługi Azure Storage w Centrum.</span><span class="sxs-lookup"><span data-stu-id="e8c0e-106">toouse hello [file upload functionality in IoT Hub][lnk-upload], you must first associate an Azure Storage account with your hub.</span></span> <span data-ttu-id="e8c0e-107">Wybierz **przekazywania pliku** toodisplay listę właściwości przekazywania plików do Centrum IoT hello, która jest modyfikowana.</span><span class="sxs-lookup"><span data-stu-id="e8c0e-107">Select **File upload** toodisplay a list of file upload properties for hello IoT hub that is being modified.</span></span>

![Przekazywanie pliku Centrum IoT widoku ustawień w portalu hello][13]

<span data-ttu-id="e8c0e-109">**Kontener magazynu**: Użyj hello Azure tooselect portalu kontenera obiektów blob na koncie magazynu Azure w Twojej bieżącej subskrypcji platformy Azure tooassociate z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="e8c0e-109">**Storage container**: Use hello Azure portal tooselect a blob container in an Azure Storage account in your current Azure subscription tooassociate with your IoT Hub.</span></span> <span data-ttu-id="e8c0e-110">Jeśli to konieczne, tworzenia konta usługi Azure Storage na powitania **kont magazynu** kontenera bloku oraz obiektów blob na powitania **kontenery** bloku.</span><span class="sxs-lookup"><span data-stu-id="e8c0e-110">If necessary, you can create an Azure Storage account on hello **Storage accounts** blade and blob container on hello **Containers** blade.</span></span> <span data-ttu-id="e8c0e-111">Centrum IoT automatycznie generuje identyfikator URI SAS z kontenera obiektów blob toothis uprawnienia zapisu dla urządzeń toouse podczas ich przekazywania plików.</span><span class="sxs-lookup"><span data-stu-id="e8c0e-111">IoT Hub automatically generates SAS URIs with write permissions toothis blob container for devices toouse when they upload files.</span></span>

![Wyświetl kontenery magazynu dla przekazywania pliku w portalu hello][14]

<span data-ttu-id="e8c0e-113">**Odbieranie powiadomień dla przekazanych plików**: Włącz lub Wyłącz powiadomienia o przekazywania plików za pomocą przełącznika hello.</span><span class="sxs-lookup"><span data-stu-id="e8c0e-113">**Receive notifications for uploaded files**: Enable or disable file upload notifications via hello toggle.</span></span>

<span data-ttu-id="e8c0e-114">**Czas wygaśnięcia SAS**: to ustawienie jest hello time-to-live z hello identyfikatorów URI SAS zwrócony toohello urządzenia przez Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="e8c0e-114">**SAS TTL**: This setting is hello time-to-live of hello SAS URIs returned toohello device by IoT Hub.</span></span> <span data-ttu-id="e8c0e-115">Domyślnie tooone godzinę, ale może być tooother dostosowanych wartości za pomocą suwaka hello.</span><span class="sxs-lookup"><span data-stu-id="e8c0e-115">Set tooone hour by default but can be customized tooother values using hello slider.</span></span>

<span data-ttu-id="e8c0e-116">**Plik powiadomienia, ustawienia domyślne TTL**: hello time-to-live powiadomienia przekazywania pliku przed jego wygaśnięciem.</span><span class="sxs-lookup"><span data-stu-id="e8c0e-116">**File notification settings default TTL**: hello time-to-live of a file upload notification before it is expired.</span></span> <span data-ttu-id="e8c0e-117">Domyślnie ustawiony dzień tooone, ale może być tooother dostosowanych wartości za pomocą suwaka hello.</span><span class="sxs-lookup"><span data-stu-id="e8c0e-117">Set tooone day by default but can be customized tooother values using hello slider.</span></span>

<span data-ttu-id="e8c0e-118">**Powiadomienie dostarczania maksymalna liczba plików**: hello liczba hello Centrum IoT prób toodeliver powiadomienie przekazywania plików.</span><span class="sxs-lookup"><span data-stu-id="e8c0e-118">**File notification maximum delivery count**: hello number of times hello IoT Hub attempts toodeliver a file upload notification.</span></span> <span data-ttu-id="e8c0e-119">Domyślnie too10, ale może być tooother dostosowanych wartości za pomocą suwaka hello.</span><span class="sxs-lookup"><span data-stu-id="e8c0e-119">Set too10 by default but can be customized tooother values using hello slider.</span></span>

![Konfigurowanie przekazywania pliku Centrum IoT w portalu hello][15]

## <a name="next-steps"></a><span data-ttu-id="e8c0e-121">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e8c0e-121">Next steps</span></span>

<span data-ttu-id="e8c0e-122">Aby uzyskać więcej informacji na temat możliwości przekazywania plików hello Centrum IoT, zobacz [przekazywania plików z urządzeniem] [ lnk-upload] w hello przewodnik dewelopera Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="e8c0e-122">For more information about hello file upload capabilities of IoT Hub, see [Upload files from a device][lnk-upload] in hello IoT Hub developer guide.</span></span>

<span data-ttu-id="e8c0e-123">Wykonaj te toolearn łącza więcej informacji na temat zarządzania Centrum IoT Azure:</span><span class="sxs-lookup"><span data-stu-id="e8c0e-123">Follow these links toolearn more about managing Azure IoT Hub:</span></span>

* <span data-ttu-id="e8c0e-124">[Zbiorcze zarządzania urządzeniami IoT][lnk-bulk]</span><span class="sxs-lookup"><span data-stu-id="e8c0e-124">[Bulk manage IoT devices][lnk-bulk]</span></span>
* <span data-ttu-id="e8c0e-125">[Metryki Centrum IoT][lnk-metrics]</span><span class="sxs-lookup"><span data-stu-id="e8c0e-125">[IoT Hub metrics][lnk-metrics]</span></span>
* <span data-ttu-id="e8c0e-126">[Operacje monitorowania][lnk-monitor]</span><span class="sxs-lookup"><span data-stu-id="e8c0e-126">[Operations monitoring][lnk-monitor]</span></span>

<span data-ttu-id="e8c0e-127">toofurther Poznaj możliwości hello Centrum IoT, zobacz:</span><span class="sxs-lookup"><span data-stu-id="e8c0e-127">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="e8c0e-128">[Przewodnik dewelopera Centrum IoT][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="e8c0e-128">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="e8c0e-129">[Symuluje urządzenia IoT krawędzi][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="e8c0e-129">[Simulating a device with IoT Edge][lnk-iotedge]</span></span>
* <span data-ttu-id="e8c0e-130">[Zabezpieczanie rozwiązania IoT z hello tła w][lnk-securing]</span><span class="sxs-lookup"><span data-stu-id="e8c0e-130">[Secure your IoT solution from hello ground up][lnk-securing]</span></span>

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
