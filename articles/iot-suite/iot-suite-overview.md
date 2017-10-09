---
title: "Omówienie pakiet IoT Azure aaaMicrosoft | Dokumentacja firmy Microsoft"
description: "Omówienie sposobu pakiet IoT Azure oferuje internet rzeczy toocollect wstępnie skonfigurowanych rozwiązań, analizować i przechowywania danych, podaj wizualizacje i integracji z innymi systemami."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 2d38d08a-4133-4e5c-8b28-f93cadb5df05
ms.service: iot-suite
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/24/2017
ms.author: dobett
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 385025c5ec0d37c74689a928bc09e85b33439634
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-azure-iot-suite"></a><span data-ttu-id="01c0f-103">Przegląd Pakietu IoT Azure</span><span class="sxs-lookup"><span data-stu-id="01c0f-103">Overview of Azure IoT Suite</span></span>

<span data-ttu-id="01c0f-104">Hello Azure Internetu rzeczy (IoT) usług oferuje szeroką gamę możliwości.</span><span class="sxs-lookup"><span data-stu-id="01c0f-104">hello Azure internet of things (IoT) services offer a broad range of capabilities.</span></span> <span data-ttu-id="01c0f-105">Są to usługi klasy korporacyjnej, które pozwalają wykonywać następujące operacje:</span><span class="sxs-lookup"><span data-stu-id="01c0f-105">These enterprise grade services enable you to:</span></span>

* <span data-ttu-id="01c0f-106">Zbieranie danych z urządzeń</span><span class="sxs-lookup"><span data-stu-id="01c0f-106">Collect data from devices</span></span>
* <span data-ttu-id="01c0f-107">Analizowanie strumieni danych w ruchu</span><span class="sxs-lookup"><span data-stu-id="01c0f-107">Analyze data streams in-motion</span></span>
* <span data-ttu-id="01c0f-108">Przechowywanie dużych zestawów danych i tworzenie dotyczących ich zapytań</span><span class="sxs-lookup"><span data-stu-id="01c0f-108">Store and query large data sets</span></span>
* <span data-ttu-id="01c0f-109">Wizualizowanie danych w czasie rzeczywistym i danych historycznych</span><span class="sxs-lookup"><span data-stu-id="01c0f-109">Visualize both real-time and historical data</span></span>
* <span data-ttu-id="01c0f-110">Integrowanie z systemami zaplecza biura</span><span class="sxs-lookup"><span data-stu-id="01c0f-110">Integrate with back-office systems</span></span>
* <span data-ttu-id="01c0f-111">Zarządzanie urządzeniami</span><span class="sxs-lookup"><span data-stu-id="01c0f-111">Manage your devices</span></span>

<span data-ttu-id="01c0f-112">toodeliver te możliwości pakiet IoT Azure razem pakietów wiele usług platformy Azure z rozszerzeniami niestandardowymi jako *wstępnie rozwiązań*.</span><span class="sxs-lookup"><span data-stu-id="01c0f-112">toodeliver these capabilities, Azure IoT Suite packages together multiple Azure services with custom extensions as *preconfigured solutions*.</span></span> <span data-ttu-id="01c0f-113">Te wstępnie skonfigurowanych rozwiązań jest podstawowych implementacji typowe wzorce rozwiązania IoT pomagających w czasie hello tooreduce zająć toodeliver Twojego rozwiązania IoT.</span><span class="sxs-lookup"><span data-stu-id="01c0f-113">These preconfigured solutions are base implementations of common IoT solution patterns that help tooreduce hello time you take toodeliver your IoT solutions.</span></span> <span data-ttu-id="01c0f-114">Przy użyciu hello [IoT software development kit][lnk-sdks], można dostosować i rozszerzyć toomeet tych rozwiązań do własnych wymagań.</span><span class="sxs-lookup"><span data-stu-id="01c0f-114">Using hello [IoT software development kits][lnk-sdks], you can customize and extend these solutions toomeet your own requirements.</span></span> <span data-ttu-id="01c0f-115">Można ich także użyć jako przykładów lub szablonów podczas tworzenia nowych rozwiązań IoT.</span><span class="sxs-lookup"><span data-stu-id="01c0f-115">You can also use these solutions as examples or templates when you are developing new IoT solutions.</span></span>

<span data-ttu-id="01c0f-116">Witaj poniższego klipu wideo zapewnia tooAzure wprowadzenie pakiet IoT:</span><span class="sxs-lookup"><span data-stu-id="01c0f-116">hello following video provides an introduction tooAzure IoT Suite:</span></span>

> [!VIDEO https://channel9.msdn.com/Events/Microsoft-Azure/AzureCon-2015/ACON309/player]
> 
> 

## <a name="azure-iot-services-in-azure-iot-suite"></a><span data-ttu-id="01c0f-117">Usługi Azure IoT w Pakiecie IoT Azure</span><span class="sxs-lookup"><span data-stu-id="01c0f-117">Azure IoT services in Azure IoT Suite</span></span>
<span data-ttu-id="01c0f-118">Witaj wstępnie rozwiązaniach jest zwykle używany hello następujące usługi:</span><span class="sxs-lookup"><span data-stu-id="01c0f-118">hello preconfigured solutions typically use hello following services:</span></span>

* <span data-ttu-id="01c0f-119">Podstawowe tooAzure pakiet IoT jest hello [Centrum IoT Azure] [ lnk-iot-hub] usługi.</span><span class="sxs-lookup"><span data-stu-id="01c0f-119">Core tooAzure IoT Suite is hello [Azure IoT Hub][lnk-iot-hub] service.</span></span> <span data-ttu-id="01c0f-120">Ta usługa udostępnia hello urządzenia do chmury i możliwości obsługi komunikatów chmury do urządzenia i działania jako brama toohello hello chmury hello inne klucza usługi pakiet IoT.</span><span class="sxs-lookup"><span data-stu-id="01c0f-120">This service provides hello device-to-cloud and cloud-to-device messaging capabilities and acts as hello gateway toohello cloud and hello other key IoT Suite services.</span></span> <span data-ttu-id="01c0f-121">usługi Hello pozwala tooreceive wiadomości z urządzeń na dużą skalę i wysyłać polecenia tooyour urządzeń.</span><span class="sxs-lookup"><span data-stu-id="01c0f-121">hello service enables you tooreceive messages from your devices at scale, and send commands tooyour devices.</span></span> <span data-ttu-id="01c0f-122">Usługa Hello pozwala również zbyt[zarządzania urządzeniami][lnk-device-management].</span><span class="sxs-lookup"><span data-stu-id="01c0f-122">hello service also enables you too[manage your devices][lnk-device-management].</span></span> <span data-ttu-id="01c0f-123">Na przykład można skonfigurować, ponownie uruchomić system lub wykonaj resetowania co najmniej jednego koncentratora toohello podłączonego urządzenia do ustawień fabrycznych.</span><span class="sxs-lookup"><span data-stu-id="01c0f-123">For example, you can configure, reboot, or perform a factory reset on one or more devices connected toohello hub.</span></span>
* <span data-ttu-id="01c0f-124">Usługa [Azure Stream Analytics][lnk-asa] umożliwia analizowanie danych w ruchu.</span><span class="sxs-lookup"><span data-stu-id="01c0f-124">[Azure Stream Analytics][lnk-asa] provides in-motion data analysis.</span></span> <span data-ttu-id="01c0f-125">Pakiet IoT używa telemetrii przychodzące tooprocess usługi, wykonywanie agregacji i wykrywa zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="01c0f-125">IoT Suite uses this service tooprocess incoming telemetry, perform aggregation, and detect events.</span></span> <span data-ttu-id="01c0f-126">rozwiązania Hello wstępnie również używają stream analytics tooprocess komunikaty informacyjne, które zawierają dane, takie jak metadanych lub polecenia odpowiedzi z urządzeń.</span><span class="sxs-lookup"><span data-stu-id="01c0f-126">hello preconfigured solutions also use stream analytics tooprocess informational messages that contain data such as metadata or command responses from devices.</span></span> <span data-ttu-id="01c0f-127">rozwiązania Hello Użyj wiadomości powitania tooprocess Stream Analytics z urządzeń i świadczenia usług pod tooother tych wiadomości.</span><span class="sxs-lookup"><span data-stu-id="01c0f-127">hello solutions use Stream Analytics tooprocess hello messages from your devices and deliver those messages tooother services.</span></span>
* <span data-ttu-id="01c0f-128">[Usługa Azure Storage] [ lnk-azure-storage] i [bazy danych Azure rozwiązania Cosmos] [ lnk-document-db] zapewniają funkcji magazynowania danych hello.</span><span class="sxs-lookup"><span data-stu-id="01c0f-128">[Azure Storage][lnk-azure-storage] and [Azure Cosmos DB][lnk-document-db] provide hello data storage capabilities.</span></span> <span data-ttu-id="01c0f-129">Witaj wstępnie skonfigurowanych rozwiązań Użyj telemetrii toostore magazynu obiektów blob i toomake je do analizy.</span><span class="sxs-lookup"><span data-stu-id="01c0f-129">hello preconfigured solutions use blob storage toostore telemetry and toomake it available for analysis.</span></span> <span data-ttu-id="01c0f-130">rozwiązania Hello używać rozwiązania Cosmos DB toostore urządzenia metadanych i umożliwiają możliwości zarządzania urządzeniami hello hello rozwiązań.</span><span class="sxs-lookup"><span data-stu-id="01c0f-130">hello solutions use Cosmos DB toostore device metadata and enable hello device management capabilities of hello solutions.</span></span>
* <span data-ttu-id="01c0f-131">[Aplikacje sieci Web platformy Azure] [ lnk-web-apps] i [Microsoft Power BI] [ lnk-power-bi] zapewniają możliwości wizualizacji danych hello.</span><span class="sxs-lookup"><span data-stu-id="01c0f-131">[Azure Web Apps][lnk-web-apps] and [Microsoft Power BI][lnk-power-bi] provide hello data visualization capabilities.</span></span> <span data-ttu-id="01c0f-132">elastyczność Hello usługi Power BI pozwala tooquickly tworzenie własnych interaktywnych pulpitów nawigacyjnych, korzystających z danych pakiet IoT.</span><span class="sxs-lookup"><span data-stu-id="01c0f-132">hello flexibility of Power BI enables you tooquickly build your own interactive dashboards that use IoT Suite data.</span></span>

<span data-ttu-id="01c0f-133">Omówienie architektury hello typowe rozwiązania IoT, zobacz [Microsoft Azure i hello Internetu rzeczy (IoT)][iot-suite-what-is-azure-iot].</span><span class="sxs-lookup"><span data-stu-id="01c0f-133">For an overview of hello architecture of a typical IoT solution, see [Microsoft Azure and hello Internet of Things (IoT)][iot-suite-what-is-azure-iot].</span></span>

## <a name="preconfigured-solutions"></a><span data-ttu-id="01c0f-134">Wstępnie skonfigurowane rozwiązania</span><span class="sxs-lookup"><span data-stu-id="01c0f-134">Preconfigured solutions</span></span>

<span data-ttu-id="01c0f-135">Pakiet IoT zawiera wstępnie skonfigurowanego rozwiązania tego wprowadzenie tooquickly można włączyć i tooexplore hello typowych scenariuszy IoT, takich jak:</span><span class="sxs-lookup"><span data-stu-id="01c0f-135">IoT Suite includes preconfigured solutions that enable you tooquickly get started with and tooexplore hello common IoT scenarios, such as:</span></span>

* <span data-ttu-id="01c0f-136">Zdalne monitorowanie</span><span class="sxs-lookup"><span data-stu-id="01c0f-136">Remote monitoring</span></span>
* <span data-ttu-id="01c0f-137">Konserwacja zapobiegawcza</span><span class="sxs-lookup"><span data-stu-id="01c0f-137">Predictive maintenance</span></span>
* <span data-ttu-id="01c0f-138">Połączona fabryka</span><span class="sxs-lookup"><span data-stu-id="01c0f-138">Connected factory</span></span>

<span data-ttu-id="01c0f-139">Można wdrożyć te rozwiązania tooyour subskrypcji platformy Azure, a następnie uruchom scenariusz IoT pełną, end-to-end.</span><span class="sxs-lookup"><span data-stu-id="01c0f-139">You can deploy these solutions tooyour Azure subscription and then run a complete, end-to-end IoT scenario.</span></span>

## <a name="next-steps"></a><span data-ttu-id="01c0f-140">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="01c0f-140">Next steps</span></span>

<span data-ttu-id="01c0f-141">Teraz, gdy masz omówienie czynności pakiet IoT i jakie są jej główne składniki można Dowiedz się więcej o rozwiązaniach hello wstępnie skonfigurowane w pakiet IoT.</span><span class="sxs-lookup"><span data-stu-id="01c0f-141">Now that you have an overview of what IoT Suite can do and what are its main components, you can learn more about hello preconfigured solutions in IoT Suite.</span></span> <span data-ttu-id="01c0f-142">Aby uzyskać więcej informacji, zobacz [co hello Azure IoT wstępnie rozwiązania?][lnk-what-are-preconfig]</span><span class="sxs-lookup"><span data-stu-id="01c0f-142">For more information, see [What are hello Azure IoT preconfigured solutions?][lnk-what-are-preconfig]</span></span>

[lnk-sdks]: https://azure.microsoft.com/documentation/articles/iot-hub-sdks-summary/
[lnk-iot-hub]: https://azure.microsoft.com/documentation/services/iot-hub/
[lnk-asa]: https://azure.microsoft.com/documentation/services/stream-analytics/
[lnk-azure-storage]: https://azure.microsoft.com/documentation/services/storage/
[lnk-document-db]: https://azure.microsoft.com/documentation/services/documentdb/
[lnk-power-bi]: https://powerbi.microsoft.com/
[lnk-web-apps]: https://azure.microsoft.com/documentation/services/app-service/web/
[iot-suite-what-is-azure-iot]: iot-suite-what-is-azure-iot.md
[lnk-what-are-preconfig]: iot-suite-what-are-preconfigured-solutions.md
[lnk-device-management]: ../iot-hub/iot-hub-device-management-overview.md
