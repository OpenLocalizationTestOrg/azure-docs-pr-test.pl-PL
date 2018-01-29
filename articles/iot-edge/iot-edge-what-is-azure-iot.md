---
title: "Rozwiązania platformy Azure dla Internetu rzeczy (IoT Edge) | Microsoft Docs"
description: "Przegląd przykładowej architektury rozwiązania IoT i jej relacji z urządzeniami, usługą Azure IoT Hub, zestawami SDK urządzeń Azure IoT, zestawami SDK usługi Azure IoT i innymi usługami Azure."
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: a859e379-dca7-42fa-bdf6-1125c86ad140
ms.service: iot-hub
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 09/15/2017
ms.author: dobett
ms.openlocfilehash: 587b733106d511ec63d71f67a06e520324a3e594
ms.sourcegitcommit: 9a61faf3463003375a53279e3adce241b5700879
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 11/15/2017
---
[!INCLUDE [iot-azure-and-iot](../../includes/iot-azure-and-iot.md)]

## <a name="next-steps"></a>Następne kroki

Azure IoT Edge to usługa platformy Azure, która umożliwia wykonywanie analiz i przetwarzanie danych na urządzeniach brzegowych. Korzystając z usługi IoT Edge, możesz zwiększać możliwości urządzeń za pomocą kodu umieszczonego w kontenerze obejmującego już używaną logikę pobieraną bezpośrednio z usług platformy Azure lub kodu specyficznego dla rozwiązania. Dzięki niej urządzenia uzyskują następujące możliwości:

* Działanie jako urządzenia bramy (agregowanie i przetwarzanie danych z wielu urządzeń liścia).
* Wykrywanie anomalii i reagowanie na zmiany w środowisku bez potrzeby czekania na instrukcje z chmury.
* Minimalizowanie kosztu przepustowości i magazynu przez wstępne przetwarzanie danych i wysyłanie wyników. 

Usługa IoT Edge obejmuje również interfejs chmurowy, który umożliwia zdalne zarządzanie urządzeniami. Bez konieczności uzyskiwania fizycznego dostępu do urządzeń można wdrażać kod, monitorować stan i aktualizować go. Zdalnie można zarządzać pojedynczymi urządzeniami lub tworzyć wdrożenia, które mają wpływ na duże, zdefiniowane przez Ciebie zestawy urządzeń. Aby uzyskać więcej informacji, zobacz [Understand IoT Edge deployments for single devices or at scale (Informacje o wdrożeniach usługi IoT Edge dla pojedynczych urządzeń lub na dużą skalę)][lnk-deployment].

Aby dowiedzieć się więcej o składnikach, które umożliwiają korzystanie z usługi IoT Edge, zobacz [How Azure IoT Edge works (Jak działa usługa Azure IoT Edge)][lnk-overview].

Jeśli pierwszy raz używasz usługi Azure IoT Hub, możesz rozpocząć od artykułu [Omówienie usługi Azure IoT Hub][lnk-iot-hub].

[lnk-deployment]: module-deployment-monitoring.md
[lnk-overview]: how-iot-edge-works.md
[lnk-iot-hub]: ../iot-hub/iot-hub-what-is-iot-hub.md
[lnk-iot-suite]: https://azure.microsoft.com/documentation/suites/iot-suite/
[lnk-iotdev]: https://azure.microsoft.com/develop/iot/
[lnk-device-management]: ../iot-hub/iot-hub-device-management-overview.md
