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

## <a name="next-steps"></a><span data-ttu-id="9ae5b-103">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="9ae5b-103">Next steps</span></span>

<span data-ttu-id="9ae5b-104">Azure IoT Hub jest usługą platformy Azure, która umożliwia bezpieczną i niezawodną dwukierunkową komunikację między zapleczem rozwiązania a milionami urządzeń.</span><span class="sxs-lookup"><span data-stu-id="9ae5b-104">Azure IoT Hub is an Azure service that enables secure and reliable bi-directional communications between your solution back end and millions of devices.</span></span> <span data-ttu-id="9ae5b-105">Umożliwia ona hello zaplecza rozwiązania do:</span><span class="sxs-lookup"><span data-stu-id="9ae5b-105">It enables hello solution back end to:</span></span>

* <span data-ttu-id="9ae5b-106">Otrzymywanie danych telemetrycznych w odpowiedniej skali z urządzeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="9ae5b-106">Receive telemetry at scale from your devices.</span></span>
* <span data-ttu-id="9ae5b-107">Dane trasy z procesora urządzenia tooa strumienia zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="9ae5b-107">Route data from your devices tooa stream event processor.</span></span>
* <span data-ttu-id="9ae5b-108">Odbieranie przekazywanych plików z urządzeń.</span><span class="sxs-lookup"><span data-stu-id="9ae5b-108">Receive file uploads from devices.</span></span>
* <span data-ttu-id="9ae5b-109">Wysyłanie wiadomości chmury do urządzenia toospecific urządzeń.</span><span class="sxs-lookup"><span data-stu-id="9ae5b-109">Send cloud-to-device messages toospecific devices.</span></span>

<span data-ttu-id="9ae5b-110">Można użyć Centrum IoT tooimplement zaplecze własne rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="9ae5b-110">You can use IoT Hub tooimplement your own solution back end.</span></span> <span data-ttu-id="9ae5b-111">Ponadto Centrum IoT zawiera tożsamości rejestru używane tooprovision urządzeń, ich poświadczenia zabezpieczeń i ich Centrum IoT toohello tooconnect praw.</span><span class="sxs-lookup"><span data-stu-id="9ae5b-111">In addition, IoT Hub includes an identity registry used tooprovision devices, their security credentials, and their rights tooconnect toohello IoT hub.</span></span> <span data-ttu-id="9ae5b-112">Zobacz toolearn więcej informacji na temat Centrum IoT [co to jest Centrum IoT?] [lnk-iot-hub].</span><span class="sxs-lookup"><span data-stu-id="9ae5b-112">toolearn more about IoT Hub, see [What is IoT Hub?][lnk-iot-hub].</span></span>

<span data-ttu-id="9ae5b-113">toolearn Centrum IoT Azure umożliwia zarządzanie urządzeniami oparte na standardach tooremotely można zarządzać, konfigurowanie i zaktualizować urządzenia, zobacz [omówienie zarządzania urządzeniami z Centrum IoT][lnk-device-management].</span><span class="sxs-lookup"><span data-stu-id="9ae5b-113">toolearn how Azure IoT Hub enables standards-based device management for you tooremotely manage, configure, and update your devices, see [Overview of device management with IoT Hub][lnk-device-management].</span></span>

<span data-ttu-id="9ae5b-114">aplikacje klienckie tooimplement w różnych systemach operacyjnych i platform sprzętowych urządzeń, można użyć urządzenia Azure IoT hello zestawów SDK.</span><span class="sxs-lookup"><span data-stu-id="9ae5b-114">tooimplement client applications on a wide variety of device hardware platforms and operating systems, you can use hello Azure IoT device SDKs.</span></span> <span data-ttu-id="9ae5b-115">urządzenie Hello zestawów SDK obejmują bibliotek, które ułatwiają wysyłanie danych telemetrycznych tooan IoT hub i odbieranie chmury do urządzenia wiadomości.</span><span class="sxs-lookup"><span data-stu-id="9ae5b-115">hello device SDKs include libraries that facilitate sending telemetry tooan IoT hub and receiving cloud-to-device messages.</span></span> <span data-ttu-id="9ae5b-116">Jeśli używasz urządzenia hello zestawów SDK, możesz wybrać spośród kilku toocommunicate protokoły sieci z Centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="9ae5b-116">When you use hello device SDKs, you can choose from several network protocols toocommunicate with IoT Hub.</span></span> <span data-ttu-id="9ae5b-117">toolearn więcej, zobacz hello [informacji o urządzeniu zestawów SDK][lnk-device-sdks].</span><span class="sxs-lookup"><span data-stu-id="9ae5b-117">toolearn more, see hello [information about device SDKs][lnk-device-sdks].</span></span>

<span data-ttu-id="9ae5b-118">tooget uruchomiono pisanie kodu i systemem niektóre przykłady, zobacz hello [Rozpoczynanie pracy z Centrum IoT] [ lnk-getstarted] samouczka.</span><span class="sxs-lookup"><span data-stu-id="9ae5b-118">tooget started writing some code and running some samples, see hello [Get started with IoT Hub][lnk-getstarted] tutorial.</span></span>

<span data-ttu-id="9ae5b-119">Warto również zainteresować się [Pakietem IoT Azure][lnk-iot-suite], który stanowi kolekcję wstępnie skonfigurowanych rozwiązań.</span><span class="sxs-lookup"><span data-stu-id="9ae5b-119">You may also be interested in [Azure IoT Suite][lnk-iot-suite], which is a collection of preconfigured solutions.</span></span> <span data-ttu-id="9ae5b-120">Pakiet IoT umożliwia tooget szybko rozpocząć pracę i skalować IoT projekty tooaddress typowych scenariuszach IoT — takie jak zdalne monitorowanie, zarządzanie zasobami i konserwacji predykcyjnej.</span><span class="sxs-lookup"><span data-stu-id="9ae5b-120">IoT Suite enables you tooget started quickly and scale IoT projects tooaddress common IoT scenarios--such as remote monitoring, asset management, and predictive maintenance.</span></span>

[lnk-getstarted]: iot-hub-csharp-csharp-getstarted.md
[lnk-device-sdks]: https://github.com/Azure/azure-iot-sdks
[lnk-iot-hub]: iot-hub-what-is-iot-hub.md
[lnk-iot-suite]: https://azure.microsoft.com/documentation/suites/iot-suite/
[lnk-iotdev]: https://azure.microsoft.com/develop/iot/
[lnk-device-management]: iot-hub-device-management-overview.md
