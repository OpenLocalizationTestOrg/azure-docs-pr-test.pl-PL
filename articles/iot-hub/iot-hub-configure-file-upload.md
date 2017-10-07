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
# <a name="configure-iot-hub-file-uploads-using-hello-azure-portal"></a>Konfigurowanie Centrum IoT przekazywania plików przy użyciu hello portalu Azure

[!INCLUDE [iot-hub-file-upload-selector](../../includes/iot-hub-file-upload-selector.md)]

## <a name="file-upload"></a>Przekazywanie pliku

Witaj toouse [plików funkcji przekazywania w Centrum IoT][lnk-upload], należy najpierw powiązać konta usługi Azure Storage w Centrum. Wybierz **przekazywania pliku** toodisplay listę właściwości przekazywania plików do Centrum IoT hello, która jest modyfikowana.

![Przekazywanie pliku Centrum IoT widoku ustawień w portalu hello][13]

**Kontener magazynu**: Użyj hello Azure tooselect portalu kontenera obiektów blob na koncie magazynu Azure w Twojej bieżącej subskrypcji platformy Azure tooassociate z Centrum IoT. Jeśli to konieczne, tworzenia konta usługi Azure Storage na powitania **kont magazynu** kontenera bloku oraz obiektów blob na powitania **kontenery** bloku. Centrum IoT automatycznie generuje identyfikator URI SAS z kontenera obiektów blob toothis uprawnienia zapisu dla urządzeń toouse podczas ich przekazywania plików.

![Wyświetl kontenery magazynu dla przekazywania pliku w portalu hello][14]

**Odbieranie powiadomień dla przekazanych plików**: Włącz lub Wyłącz powiadomienia o przekazywania plików za pomocą przełącznika hello.

**Czas wygaśnięcia SAS**: to ustawienie jest hello time-to-live z hello identyfikatorów URI SAS zwrócony toohello urządzenia przez Centrum IoT. Domyślnie tooone godzinę, ale może być tooother dostosowanych wartości za pomocą suwaka hello.

**Plik powiadomienia, ustawienia domyślne TTL**: hello time-to-live powiadomienia przekazywania pliku przed jego wygaśnięciem. Domyślnie ustawiony dzień tooone, ale może być tooother dostosowanych wartości za pomocą suwaka hello.

**Powiadomienie dostarczania maksymalna liczba plików**: hello liczba hello Centrum IoT prób toodeliver powiadomienie przekazywania plików. Domyślnie too10, ale może być tooother dostosowanych wartości za pomocą suwaka hello.

![Konfigurowanie przekazywania pliku Centrum IoT w portalu hello][15]

## <a name="next-steps"></a>Następne kroki

Aby uzyskać więcej informacji na temat możliwości przekazywania plików hello Centrum IoT, zobacz [przekazywania plików z urządzeniem] [ lnk-upload] w hello przewodnik dewelopera Centrum IoT.

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
