---
title: Zabezpieczanie Internetu rzeczy (IoT) na platformie Azure | Dokumentacja firmy Microsoft
description: " Azure Internetu rzeczy (IoT) usług oferuje szeroką gamę możliwości. Ten artykuł pomaga zrozumieć, jak zabezpieczyć Twojego rozwiązania IoT na platformie Azure. "
services: security
documentationcenter: na
author: TomShinder
manager: MBaldwin
editor: TomSh
ms.assetid: 1473c8dd-8669-48fb-86db-b3c50e2eaf59
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/23/2017
ms.author: terrylan
ms.openlocfilehash: 3793f5453b74b6c06d9e58b426d89099298e1288
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="internet-of-things-security-overview"></a><span data-ttu-id="00bfe-104">Przegląd zabezpieczeń Internetu rzeczy</span><span class="sxs-lookup"><span data-stu-id="00bfe-104">Internet of Things security overview</span></span>
<span data-ttu-id="00bfe-105">Azure Internetu rzeczy (IoT) usług oferuje szeroką gamę możliwości.</span><span class="sxs-lookup"><span data-stu-id="00bfe-105">Azure internet of things (IoT) services offer a broad range of capabilities.</span></span> <span data-ttu-id="00bfe-106">Są to usługi klasy korporacyjnej, które pozwalają wykonywać następujące operacje:</span><span class="sxs-lookup"><span data-stu-id="00bfe-106">These enterprise grade services enable you to:</span></span>

* <span data-ttu-id="00bfe-107">Zbieranie danych z urządzeń</span><span class="sxs-lookup"><span data-stu-id="00bfe-107">Collect data from devices</span></span>
* <span data-ttu-id="00bfe-108">Analizowanie strumieni danych w ruchu</span><span class="sxs-lookup"><span data-stu-id="00bfe-108">Analyze data streams in-motion</span></span>
* <span data-ttu-id="00bfe-109">Przechowywanie dużych zestawów danych i tworzenie dotyczących ich zapytań</span><span class="sxs-lookup"><span data-stu-id="00bfe-109">Store and query large data sets</span></span>
* <span data-ttu-id="00bfe-110">Wizualizowanie danych w czasie rzeczywistym i danych historycznych</span><span class="sxs-lookup"><span data-stu-id="00bfe-110">Visualize both real-time and historical data</span></span>
* <span data-ttu-id="00bfe-111">Integrowanie z systemami zaplecza biura</span><span class="sxs-lookup"><span data-stu-id="00bfe-111">Integrate with back-office systems</span></span>

<span data-ttu-id="00bfe-112">Aby dostarczyć te możliwości, pakiet IoT Azure pakiety ze sobą wiele usług platformy Azure z rozszerzeniami niestandardowymi jako wstępnie skonfigurowanych rozwiązań.</span><span class="sxs-lookup"><span data-stu-id="00bfe-112">To deliver these capabilities, Azure IoT Suite packages together multiple Azure services with custom extensions as preconfigured solutions.</span></span> <span data-ttu-id="00bfe-113">Te wstępnie skonfigurowane rozwiązania stanowią podstawowe implementacje typowych wzorców rozwiązań IoT i pomagają skrócić czas dostarczania własnych rozwiązań IoT.</span><span class="sxs-lookup"><span data-stu-id="00bfe-113">These preconfigured solutions are base implementations of common IoT solution patterns that help to reduce the time you take to deliver your IoT solutions.</span></span> <span data-ttu-id="00bfe-114">Przy użyciu IoT software development kit, można dostosować i rozszerzyć tych rozwiązań, aby spełniały określone wymagania.</span><span class="sxs-lookup"><span data-stu-id="00bfe-114">Using the IoT software development kits, you can customize and extend these solutions to meet your own requirements.</span></span> <span data-ttu-id="00bfe-115">Można ich także użyć jako przykładów lub szablonów podczas tworzenia nowych rozwiązań IoT.</span><span class="sxs-lookup"><span data-stu-id="00bfe-115">You can also use these solutions as examples or templates when you are developing new IoT solutions.</span></span>

<span data-ttu-id="00bfe-116">Pakiet Azure IoT jest niezwykle wydajnym rozwiązaniem dla potrzeb IoT.</span><span class="sxs-lookup"><span data-stu-id="00bfe-116">The Azure IoT suite is a powerful solution for your IoT needs.</span></span> <span data-ttu-id="00bfe-117">Warto jednak znaczenie upmost czy Twojego rozwiązania IoT zostały zaprojektowane z myślą od początku o bezpieczeństwie.</span><span class="sxs-lookup"><span data-stu-id="00bfe-117">However, it’s of upmost importance that your IoT solutions are designed with security in mind from the start.</span></span> <span data-ttu-id="00bfe-118">Z powodu wielość urządzenia IoT wszystkie zdarzenia zabezpieczeń może szybko stać się powszechnie zdarzeń z znaczący wpływ.</span><span class="sxs-lookup"><span data-stu-id="00bfe-118">Because of the sheer number of IoT devices, any security incident can quickly become a widespread event with significant consequences.</span></span>

<span data-ttu-id="00bfe-119">Aby ułatwić zrozumienie, jak zabezpieczyć Twojego rozwiązania IoT, zostały następujące informacje.</span><span class="sxs-lookup"><span data-stu-id="00bfe-119">To help you understand how to secure your IoT solutions, we have the following information.</span></span>

## <a name="security-architecture"></a><span data-ttu-id="00bfe-120">Architektura zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="00bfe-120">Security architecture</span></span>
<span data-ttu-id="00bfe-121">Podczas projektowania systemu, ważne jest zrozumienie potencjalnych zagrożeń dla tego systemu, a Dodaj odpowiednie zabezpieczenia w związku z tym system został zaprojektowany i zaprojektowana.</span><span class="sxs-lookup"><span data-stu-id="00bfe-121">When designing a system, it is important to understand the potential threats to that system, and add appropriate defenses accordingly, as the system is designed and architected.</span></span> <span data-ttu-id="00bfe-122">Należy zaprojektować produktu od początku z myślą o bezpieczeństwie, ponieważ Opis ułatwia sposób atakujący może być w stanie naruszyć bezpieczeństwo systemu, upewnij się, że odpowiednie środki zaradcze są stosowane od początku.</span><span class="sxs-lookup"><span data-stu-id="00bfe-122">It is important to design the product from the start with security in mind because understanding how an attacker might be able to compromise a system helps make sure appropriate mitigations are in place from the beginning.</span></span>

<span data-ttu-id="00bfe-123">Informacje na temat architektury IoT zabezpieczeń, odczytując [Internet rzeczy Architektura zabezpieczeń](../iot-suite/iot-security-architecture.md).</span><span class="sxs-lookup"><span data-stu-id="00bfe-123">You can learn about IoT security architecture by reading [Internet of Things Security Architecture](../iot-suite/iot-security-architecture.md).</span></span>

<span data-ttu-id="00bfe-124">W tym artykule omówiono następujące zagadnienia:</span><span class="sxs-lookup"><span data-stu-id="00bfe-124">This article discusses the following topics:</span></span>

* [<span data-ttu-id="00bfe-125">Rozpoczyna się modelu zagrożeń zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="00bfe-125">Security Starts with a Threat Model</span></span>](../iot-suite/iot-security-architecture.md#security-starts-with-a-threat-model)
* [<span data-ttu-id="00bfe-126">Zabezpieczenia w IoT</span><span class="sxs-lookup"><span data-stu-id="00bfe-126">Security in IoT</span></span>](../iot-suite/iot-security-architecture.md#security-in-iot)
* [<span data-ttu-id="00bfe-127">Modelowanie architektury Azure IoT odwołanie zagrożeń</span><span class="sxs-lookup"><span data-stu-id="00bfe-127">Threat Modeling the Azure IoT Reference Architecture</span></span>](../iot-suite/iot-security-architecture.md#threat-modeling-the-azure-iot-reference-architecture)

## <a name="security-from-the-ground-up"></a><span data-ttu-id="00bfe-128">Zabezpieczenia od podstaw</span><span class="sxs-lookup"><span data-stu-id="00bfe-128">Security from the ground up</span></span>
<span data-ttu-id="00bfe-129">IoT stanowi wyjątkowe wyzwanie zabezpieczeń, prywatności i zgodności dla firm na całym świecie.</span><span class="sxs-lookup"><span data-stu-id="00bfe-129">The IoT poses unique security, privacy, and compliance challenges to businesses worldwide.</span></span> <span data-ttu-id="00bfe-130">W przeciwieństwie do tradycyjnych przez technologii gdzie te problemy koncentrują się wokół oprogramowania i jak jest implementowane IoT dotyczy, co się stanie po zbieżne ataków i względem fizycznych.</span><span class="sxs-lookup"><span data-stu-id="00bfe-130">Unlike traditional cyber technology where these issues revolve around software and how it is implemented, IoT concerns what happens when the cyber and the physical worlds converge.</span></span> <span data-ttu-id="00bfe-131">Ochrona rozwiązania IoT wymaga zapewnienia bezpiecznego inicjowania obsługi urządzeń i bezpieczna łączność między tymi urządzeniami i chmurą i ochronę danych w chmurze podczas przetwarzania i przechowywania.</span><span class="sxs-lookup"><span data-stu-id="00bfe-131">Protecting IoT solutions requires ensuring secure provisioning of devices, secure connectivity between these devices and the cloud, and secure data protection in the cloud during processing and storage.</span></span> <span data-ttu-id="00bfe-132">Praca z takich funkcji, są jednak ograniczone zasobów urządzeń, rozmieszczenie geograficzne wdrożeń i wiele urządzeń w ramach rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="00bfe-132">Working against such functionality, however, are resource-constrained devices, geographic distribution of deployments, and many devices within a solution.</span></span>

<span data-ttu-id="00bfe-133">Znajdują się informacje dotyczące obsługi zabezpieczeń w następujących obszarach odczytując [zabezpieczeń Internetu rzeczy od podstaw](../iot-suite/securing-iot-ground-up.md).</span><span class="sxs-lookup"><span data-stu-id="00bfe-133">You can learn how to handle security in these areas by reading [Internet of Things security from the ground up](../iot-suite/securing-iot-ground-up.md).</span></span>

<span data-ttu-id="00bfe-134">W tym artykule omówiono następujące tematy:</span><span class="sxs-lookup"><span data-stu-id="00bfe-134">The article discusses the following topics:</span></span>

* [<span data-ttu-id="00bfe-135">Bezpiecznej infrastruktury od podstaw</span><span class="sxs-lookup"><span data-stu-id="00bfe-135">Secure infrastructure from the ground up</span></span>](../iot-suite/securing-iot-ground-up.md#secure-infrastructure-from-the-ground-up)
* [<span data-ttu-id="00bfe-136">Microsoft Azure — bezpiecznej infrastruktury IoT dla biznesu</span><span class="sxs-lookup"><span data-stu-id="00bfe-136">Microsoft Azure – secure IoT infrastructure for your business</span></span>](../iot-suite/securing-iot-ground-up.md#microsoft-azure---secure-iot-infrastructure-for-your-business)

## <a name="best-practices"></a><span data-ttu-id="00bfe-137">Najlepsze rozwiązania</span><span class="sxs-lookup"><span data-stu-id="00bfe-137">Best Practices</span></span>
<span data-ttu-id="00bfe-138">Zabezpieczanie infrastruktury IoT wymaga rygorystyczne strategii zabezpieczeń zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="00bfe-138">Securing an IoT infrastructure requires a rigorous security-in-depth strategy.</span></span> <span data-ttu-id="00bfe-139">Z Zabezpieczanie danych w chmurze, ochrony integralności danych przesyłanych za pośrednictwem publicznego Internetu do bezpiecznego inicjowania obsługi urządzeń, każda warstwa kompilacje gwarancję zabezpieczeń w całej infrastruktury.</span><span class="sxs-lookup"><span data-stu-id="00bfe-139">From securing data in the cloud, protecting data integrity while in transit over the public internet, to securely provisioning devices, each layer builds greater security assurance in the overall infrastructure.</span></span>

<span data-ttu-id="00bfe-140">Informacje na temat zabezpieczeń Internetu rzeczy najlepsze rozwiązania w zakresie odczytując [najlepszych rozwiązań dotyczących zabezpieczeń Internetu rzeczy](../iot-suite/iot-security-best-practices.md).</span><span class="sxs-lookup"><span data-stu-id="00bfe-140">You can learn about Internet of Things security best practices by reading [Internet of Things security best practices](../iot-suite/iot-security-best-practices.md).</span></span>

<span data-ttu-id="00bfe-141">W tym artykule omówiono następujące tematy:</span><span class="sxs-lookup"><span data-stu-id="00bfe-141">The article discusses the following topics:</span></span>

* [<span data-ttu-id="00bfe-142">Producenta sprzętu IoT/integrator</span><span class="sxs-lookup"><span data-stu-id="00bfe-142">IoT hardware manufacturer/integrator</span></span>](../iot-suite/iot-security-best-practices.md#iot-hardware-manufacturerintegrator)
* [<span data-ttu-id="00bfe-143">Deweloper rozwiązania IoT</span><span class="sxs-lookup"><span data-stu-id="00bfe-143">IoT solution developer</span></span>](../iot-suite/iot-security-best-practices.md#iot-solution-developer)
* [<span data-ttu-id="00bfe-144">Narzędzie wdrażania rozwiązania IoT</span><span class="sxs-lookup"><span data-stu-id="00bfe-144">IoT solution deployer</span></span>](../iot-suite/iot-security-best-practices.md#iot-solution-deployer)
* [<span data-ttu-id="00bfe-145">Operator rozwiązania IoT</span><span class="sxs-lookup"><span data-stu-id="00bfe-145">IoT solution operator</span></span>](../iot-suite/iot-security-best-practices.md#iot-solution-operator)
