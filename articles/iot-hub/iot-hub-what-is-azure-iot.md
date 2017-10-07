---
title: "rozwiązania aaaAzure Internetu rzeczy (IoT pakiet) | Dokumentacja firmy Microsoft"
description: "Omówienie architektury rozwiązania IoT próbki i jego powiązań toodevices, hello usługa Azure IoT Hub, zestawy SDK urządzenia Azure IoT zestawów SDK usługi Azure IoT i innymi usługami Azure."
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
ms.date: 06/16/2017
ms.author: dobett
ms.openlocfilehash: 2d934e3f988c530de6a242869c021712d2aa1576
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
[!INCLUDE [iot-azure-and-iot](../../includes/iot-azure-and-iot.md)]

## <a name="next-steps"></a>Następne kroki

Azure IoT Hub jest usługą platformy Azure, która umożliwia bezpieczną i niezawodną dwukierunkową komunikację między zapleczem rozwiązania a milionami urządzeń. Umożliwia ona hello zaplecza rozwiązania do:

* Otrzymywanie danych telemetrycznych w odpowiedniej skali z urządzeń użytkownika.
* Dane trasy z procesora urządzenia tooa strumienia zdarzeń.
* Odbieranie przekazywanych plików z urządzeń.
* Wysyłanie wiadomości chmury do urządzenia toospecific urządzeń.

Można użyć Centrum IoT tooimplement zaplecze własne rozwiązania. Ponadto Centrum IoT zawiera tożsamości rejestru używane tooprovision urządzeń, ich poświadczenia zabezpieczeń i ich Centrum IoT toohello tooconnect praw. Zobacz toolearn więcej informacji na temat Centrum IoT [co to jest Centrum IoT?] [lnk-iot-hub].

toolearn Centrum IoT Azure umożliwia zarządzanie urządzeniami oparte na standardach tooremotely można zarządzać, konfigurowanie i zaktualizować urządzenia, zobacz [omówienie zarządzania urządzeniami z Centrum IoT][lnk-device-management].

aplikacje klienckie tooimplement w różnych systemach operacyjnych i platform sprzętowych urządzeń, można użyć urządzenia Azure IoT hello zestawów SDK. urządzenie Hello zestawów SDK obejmują bibliotek, które ułatwiają wysyłanie danych telemetrycznych tooan IoT hub i odbieranie chmury do urządzenia wiadomości. Jeśli używasz urządzenia hello zestawów SDK, możesz wybrać spośród kilku toocommunicate protokoły sieci z Centrum IoT. toolearn więcej, zobacz hello [informacji o urządzeniu zestawów SDK][lnk-device-sdks].

tooget uruchomiono pisanie kodu i systemem niektóre przykłady, zobacz hello [Rozpoczynanie pracy z Centrum IoT] [ lnk-getstarted] samouczka.

Warto również zainteresować się [Pakietem IoT Azure][lnk-iot-suite], który stanowi kolekcję wstępnie skonfigurowanych rozwiązań. Pakiet IoT umożliwia tooget szybko rozpocząć pracę i skalować IoT projekty tooaddress typowych scenariuszach IoT — takie jak zdalne monitorowanie, zarządzanie zasobami i konserwacji predykcyjnej.

[lnk-getstarted]: iot-hub-csharp-csharp-getstarted.md
[lnk-device-sdks]: https://github.com/Azure/azure-iot-sdks
[lnk-iot-hub]: iot-hub-what-is-iot-hub.md
[lnk-iot-suite]: https://azure.microsoft.com/documentation/suites/iot-suite/
[lnk-iotdev]: https://azure.microsoft.com/develop/iot/
[lnk-device-management]: iot-hub-device-management-overview.md
