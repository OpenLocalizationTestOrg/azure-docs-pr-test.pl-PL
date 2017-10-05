---
title: "Rozwiązania platformy Azure dla Internetu rzeczy (Pakiet IoT) | Microsoft Docs"
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
ms.date: 06/16/2017
ms.author: dobett
ms.openlocfilehash: 1d54f090a0e07cd5102cb48cd70a1377845d6654
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
[!INCLUDE [iot-azure-and-iot](../../includes/iot-azure-and-iot.md)]

## <a name="next-steps"></a><span data-ttu-id="51b01-103">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="51b01-103">Next steps</span></span>

<span data-ttu-id="51b01-104">Azure IoT Hub jest usługą platformy Azure, która umożliwia bezpieczną i niezawodną dwukierunkową komunikację między zapleczem rozwiązania a milionami urządzeń.</span><span class="sxs-lookup"><span data-stu-id="51b01-104">Azure IoT Hub is an Azure service that enables secure and reliable bi-directional communications between your solution back end and millions of devices.</span></span> <span data-ttu-id="51b01-105">Umożliwia zapleczu rozwiązania:</span><span class="sxs-lookup"><span data-stu-id="51b01-105">It enables the solution back end to:</span></span>

* <span data-ttu-id="51b01-106">Otrzymywanie danych telemetrycznych w odpowiedniej skali z urządzeń użytkownika.</span><span class="sxs-lookup"><span data-stu-id="51b01-106">Receive telemetry at scale from your devices.</span></span>
* <span data-ttu-id="51b01-107">Przekazywanie danych z urządzeń użytkownika do strumieniowego procesora zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="51b01-107">Route data from your devices to a stream event processor.</span></span>
* <span data-ttu-id="51b01-108">Odbieranie przekazywanych plików z urządzeń.</span><span class="sxs-lookup"><span data-stu-id="51b01-108">Receive file uploads from devices.</span></span>
* <span data-ttu-id="51b01-109">Wysyłanie komunikatów chmura-urządzenie do określonych urządzeń.</span><span class="sxs-lookup"><span data-stu-id="51b01-109">Send cloud-to-device messages to specific devices.</span></span>

<span data-ttu-id="51b01-110">Za pomocą usługi IoT Hub można implementować własne zaplecze rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="51b01-110">You can use IoT Hub to implement your own solution back end.</span></span> <span data-ttu-id="51b01-111">Ponadto usługa IoT Hub zawiera rejestr tożsamości używany do aprowizacji urządzeń, ich poświadczeń zabezpieczeń oraz praw do łączenia się z centrum IoT.</span><span class="sxs-lookup"><span data-stu-id="51b01-111">In addition, IoT Hub includes an identity registry used to provision devices, their security credentials, and their rights to connect to the IoT hub.</span></span> <span data-ttu-id="51b01-112">Aby dowiedzieć się więcej na temat usługi IoT Hub, zobacz [Co to jest usługa IoT Hub?][lnk-iot-hub].</span><span class="sxs-lookup"><span data-stu-id="51b01-112">To learn more about IoT Hub, see [What is IoT Hub?][lnk-iot-hub].</span></span>

<span data-ttu-id="51b01-113">Aby dowiedzieć się, jak usługa Azure IoT Hub umożliwia oparte na standardach zarządzanie urządzeniami pozwalające na zdalne konfigurowanie i aktualizowanie urządzeń oraz zarządzanie nimi, zobacz [Omówienie zarządzania urządzeniami za pomocą usługi IoT Hub][lnk-device-management].</span><span class="sxs-lookup"><span data-stu-id="51b01-113">To learn how Azure IoT Hub enables standards-based device management for you to remotely manage, configure, and update your devices, see [Overview of device management with IoT Hub][lnk-device-management].</span></span>

<span data-ttu-id="51b01-114">W celu wdrożenia aplikacji klienckich na wielu różnych platformach sprzętowych i w różnych systemach operacyjnych można użyć zestawów SDK urządzeń Azure IoT.</span><span class="sxs-lookup"><span data-stu-id="51b01-114">To implement client applications on a wide variety of device hardware platforms and operating systems, you can use the Azure IoT device SDKs.</span></span> <span data-ttu-id="51b01-115">Te zestawy SDK urządzeń zawierają biblioteki, które ułatwiają wysyłanie danych telemetrycznych do centrum IoT Hub i odbieranie komunikatów wysyłanych z chmury do urządzeń.</span><span class="sxs-lookup"><span data-stu-id="51b01-115">The device SDKs include libraries that facilitate sending telemetry to an IoT hub and receiving cloud-to-device messages.</span></span> <span data-ttu-id="51b01-116">Korzystając z zestawów SDK urządzeń, można wybierać spośród wielu protokołów sieciowych służących do komunikowania się z usługą IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="51b01-116">When you use the device SDKs, you can choose from several network protocols to communicate with IoT Hub.</span></span> <span data-ttu-id="51b01-117">Aby dowiedzieć się więcej, zobacz [informacje dotyczące zestawów SDK urządzeń][lnk-device-sdks].</span><span class="sxs-lookup"><span data-stu-id="51b01-117">To learn more, see the [information about device SDKs][lnk-device-sdks].</span></span>

<span data-ttu-id="51b01-118">Aby rozpocząć pisanie kodu i uruchomić kilka przykładów, zobacz samouczek [Wprowadzenie do usługi IoT Hub][lnk-getstarted].</span><span class="sxs-lookup"><span data-stu-id="51b01-118">To get started writing some code and running some samples, see the [Get started with IoT Hub][lnk-getstarted] tutorial.</span></span>

<span data-ttu-id="51b01-119">Warto również zainteresować się [Pakietem IoT Azure][lnk-iot-suite], który stanowi kolekcję wstępnie skonfigurowanych rozwiązań.</span><span class="sxs-lookup"><span data-stu-id="51b01-119">You may also be interested in [Azure IoT Suite][lnk-iot-suite], which is a collection of preconfigured solutions.</span></span> <span data-ttu-id="51b01-120">Pakiet IoT pozwala szybko rozpocząć pracę i skalować projekty IoT na potrzeby typowych scenariuszy, takich jak zdalne monitorowanie, zarządzanie zasobami i konserwacja predykcyjna.</span><span class="sxs-lookup"><span data-stu-id="51b01-120">IoT Suite enables you to get started quickly and scale IoT projects to address common IoT scenarios--such as remote monitoring, asset management, and predictive maintenance.</span></span>

[lnk-getstarted]: iot-hub-csharp-csharp-getstarted.md
[lnk-device-sdks]: https://github.com/Azure/azure-iot-sdks
[lnk-iot-hub]: iot-hub-what-is-iot-hub.md
[lnk-iot-suite]: https://azure.microsoft.com/documentation/suites/iot-suite/
[lnk-iotdev]: https://azure.microsoft.com/develop/iot/
[lnk-device-management]: iot-hub-device-management-overview.md
