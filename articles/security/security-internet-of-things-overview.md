---
title: aaaSecure z Internetu rzeczy (IoT) na platformie Azure | Dokumentacja firmy Microsoft
description: " Azure Internetu rzeczy (IoT) usług oferuje szeroką gamę możliwości. Ten artykuł pomaga w zrozumieniu sposobu toosecure Twojego rozwiązania IoT na platformie Azure. "
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
ms.openlocfilehash: b6cb2ea1c1facada854fb52c55066f34a8289e47
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="internet-of-things-security-overview"></a><span data-ttu-id="ca18d-104">Przegląd zabezpieczeń Internetu rzeczy</span><span class="sxs-lookup"><span data-stu-id="ca18d-104">Internet of Things security overview</span></span>
<span data-ttu-id="ca18d-105">Azure Internetu rzeczy (IoT) usług oferuje szeroką gamę możliwości.</span><span class="sxs-lookup"><span data-stu-id="ca18d-105">Azure internet of things (IoT) services offer a broad range of capabilities.</span></span> <span data-ttu-id="ca18d-106">Są to usługi klasy korporacyjnej, które pozwalają wykonywać następujące operacje:</span><span class="sxs-lookup"><span data-stu-id="ca18d-106">These enterprise grade services enable you to:</span></span>

* <span data-ttu-id="ca18d-107">Zbieranie danych z urządzeń</span><span class="sxs-lookup"><span data-stu-id="ca18d-107">Collect data from devices</span></span>
* <span data-ttu-id="ca18d-108">Analizowanie strumieni danych w ruchu</span><span class="sxs-lookup"><span data-stu-id="ca18d-108">Analyze data streams in-motion</span></span>
* <span data-ttu-id="ca18d-109">Przechowywanie dużych zestawów danych i tworzenie dotyczących ich zapytań</span><span class="sxs-lookup"><span data-stu-id="ca18d-109">Store and query large data sets</span></span>
* <span data-ttu-id="ca18d-110">Wizualizowanie danych w czasie rzeczywistym i danych historycznych</span><span class="sxs-lookup"><span data-stu-id="ca18d-110">Visualize both real-time and historical data</span></span>
* <span data-ttu-id="ca18d-111">Integrowanie z systemami zaplecza biura</span><span class="sxs-lookup"><span data-stu-id="ca18d-111">Integrate with back-office systems</span></span>

<span data-ttu-id="ca18d-112">toodeliver te możliwości pakiet IoT Azure pakiety ze sobą Azure wielu usług z rozszerzeniami niestandardowymi jako wstępnie skonfigurowanych rozwiązań.</span><span class="sxs-lookup"><span data-stu-id="ca18d-112">toodeliver these capabilities, Azure IoT Suite packages together multiple Azure services with custom extensions as preconfigured solutions.</span></span> <span data-ttu-id="ca18d-113">Te wstępnie skonfigurowanych rozwiązań jest podstawowych implementacji typowe wzorce rozwiązania IoT pomagających w czasie hello tooreduce zająć toodeliver Twojego rozwiązania IoT.</span><span class="sxs-lookup"><span data-stu-id="ca18d-113">These preconfigured solutions are base implementations of common IoT solution patterns that help tooreduce hello time you take toodeliver your IoT solutions.</span></span> <span data-ttu-id="ca18d-114">Przy użyciu hello IoT software development kit, można dostosowywanie i rozszerzanie toomeet tych rozwiązań do własnych wymagań.</span><span class="sxs-lookup"><span data-stu-id="ca18d-114">Using hello IoT software development kits, you can customize and extend these solutions toomeet your own requirements.</span></span> <span data-ttu-id="ca18d-115">Można ich także użyć jako przykładów lub szablonów podczas tworzenia nowych rozwiązań IoT.</span><span class="sxs-lookup"><span data-stu-id="ca18d-115">You can also use these solutions as examples or templates when you are developing new IoT solutions.</span></span>

<span data-ttu-id="ca18d-116">Pakiet Azure IoT Hello jest niezwykle wydajnym rozwiązaniem dla potrzeb IoT.</span><span class="sxs-lookup"><span data-stu-id="ca18d-116">hello Azure IoT suite is a powerful solution for your IoT needs.</span></span> <span data-ttu-id="ca18d-117">Warto jednak znaczenie upmost czy Twojego rozwiązania IoT zostały zaprojektowane z myślą od początku hello o bezpieczeństwie.</span><span class="sxs-lookup"><span data-stu-id="ca18d-117">However, it’s of upmost importance that your IoT solutions are designed with security in mind from hello start.</span></span> <span data-ttu-id="ca18d-118">Z powodu wielość hello urządzeń IoT wszystkie zdarzenia zabezpieczeń może szybko stać się powszechnie zdarzeń z znaczący wpływ.</span><span class="sxs-lookup"><span data-stu-id="ca18d-118">Because of hello sheer number of IoT devices, any security incident can quickly become a widespread event with significant consequences.</span></span>

<span data-ttu-id="ca18d-119">toohelp rozumiesz sposób toosecure Twojego rozwiązania IoT mamy hello następujących informacji.</span><span class="sxs-lookup"><span data-stu-id="ca18d-119">toohelp you understand how toosecure your IoT solutions, we have hello following information.</span></span>

## <a name="security-architecture"></a><span data-ttu-id="ca18d-120">Architektura zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="ca18d-120">Security architecture</span></span>
<span data-ttu-id="ca18d-121">Podczas projektowania systemu, jest ważne toounderstand hello potencjalne zagrożenia toothat systemu i dodaj odpowiednie zabezpieczenia w związku z tym, jak hello system został zaprojektowany i zaprojektowana.</span><span class="sxs-lookup"><span data-stu-id="ca18d-121">When designing a system, it is important toounderstand hello potential threats toothat system, and add appropriate defenses accordingly, as hello system is designed and architected.</span></span> <span data-ttu-id="ca18d-122">Koniecznie toodesign ponieważ zrozumienie, jak osoba atakująca może być możliwe toocompromise systemu pomaga, upewnij się, że odpowiednie środki zaradcze są stosowane od początku hello hello produktu od początku hello z myślą o bezpieczeństwie.</span><span class="sxs-lookup"><span data-stu-id="ca18d-122">It is important toodesign hello product from hello start with security in mind because understanding how an attacker might be able toocompromise a system helps make sure appropriate mitigations are in place from hello beginning.</span></span>

<span data-ttu-id="ca18d-123">Informacje na temat architektury IoT zabezpieczeń, odczytując [Internet rzeczy Architektura zabezpieczeń](../iot-suite/iot-security-architecture.md).</span><span class="sxs-lookup"><span data-stu-id="ca18d-123">You can learn about IoT security architecture by reading [Internet of Things Security Architecture](../iot-suite/iot-security-architecture.md).</span></span>

<span data-ttu-id="ca18d-124">W tym artykule omówiono hello następujące tematy:</span><span class="sxs-lookup"><span data-stu-id="ca18d-124">This article discusses hello following topics:</span></span>

* [<span data-ttu-id="ca18d-125">Rozpoczyna się modelu zagrożeń zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="ca18d-125">Security Starts with a Threat Model</span></span>](../iot-suite/iot-security-architecture.md#security-starts-with-a-threat-model)
* [<span data-ttu-id="ca18d-126">Zabezpieczenia w IoT</span><span class="sxs-lookup"><span data-stu-id="ca18d-126">Security in IoT</span></span>](../iot-suite/iot-security-architecture.md#security-in-iot)
* [<span data-ttu-id="ca18d-127">Witaj modelowania zagrożeń architektura referencyjna IoT Azure</span><span class="sxs-lookup"><span data-stu-id="ca18d-127">Threat Modeling hello Azure IoT Reference Architecture</span></span>](../iot-suite/iot-security-architecture.md#threat-modeling-the-azure-iot-reference-architecture)

## <a name="security-from-hello-ground-up"></a><span data-ttu-id="ca18d-128">Zabezpieczeń z hello tła w</span><span class="sxs-lookup"><span data-stu-id="ca18d-128">Security from hello ground up</span></span>
<span data-ttu-id="ca18d-129">Witaj IoT stanowi unikatowy zabezpieczeń, prywatności i zgodności wyzwania toobusinesses na całym świecie.</span><span class="sxs-lookup"><span data-stu-id="ca18d-129">hello IoT poses unique security, privacy, and compliance challenges toobusinesses worldwide.</span></span> <span data-ttu-id="ca18d-130">W przeciwieństwie do tradycyjnych przez technologii gdzie te problemy koncentrują się wokół oprogramowania i jak jest implementowane IoT dotyczy, co się stanie po hello ataków i hello względem fizycznego łączenia.</span><span class="sxs-lookup"><span data-stu-id="ca18d-130">Unlike traditional cyber technology where these issues revolve around software and how it is implemented, IoT concerns what happens when hello cyber and hello physical worlds converge.</span></span> <span data-ttu-id="ca18d-131">Ochrona rozwiązania IoT wymaga zapewnienia bezpiecznego inicjowania obsługi urządzeń i bezpieczna łączność między tymi urządzeniami i chmury hello i ochronę danych w chmurze hello podczas przetwarzania i przechowywania.</span><span class="sxs-lookup"><span data-stu-id="ca18d-131">Protecting IoT solutions requires ensuring secure provisioning of devices, secure connectivity between these devices and hello cloud, and secure data protection in hello cloud during processing and storage.</span></span> <span data-ttu-id="ca18d-132">Praca z takich funkcji, są jednak ograniczone zasobów urządzeń, rozmieszczenie geograficzne wdrożeń i wiele urządzeń w ramach rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="ca18d-132">Working against such functionality, however, are resource-constrained devices, geographic distribution of deployments, and many devices within a solution.</span></span>

<span data-ttu-id="ca18d-133">Dowiedz się jak toohandle zabezpieczeń w następujących obszarach odczytując [zabezpieczeń Internetu rzeczy z hello tła](../iot-suite/securing-iot-ground-up.md).</span><span class="sxs-lookup"><span data-stu-id="ca18d-133">You can learn how toohandle security in these areas by reading [Internet of Things security from hello ground up](../iot-suite/securing-iot-ground-up.md).</span></span>

<span data-ttu-id="ca18d-134">Witaj omówiono hello następujące tematy:</span><span class="sxs-lookup"><span data-stu-id="ca18d-134">hello article discusses hello following topics:</span></span>

* [<span data-ttu-id="ca18d-135">Zabezpieczanie infrastruktury z hello tła w</span><span class="sxs-lookup"><span data-stu-id="ca18d-135">Secure infrastructure from hello ground up</span></span>](../iot-suite/securing-iot-ground-up.md#secure-infrastructure-from-the-ground-up)
* [<span data-ttu-id="ca18d-136">Microsoft Azure — bezpiecznej infrastruktury IoT dla biznesu</span><span class="sxs-lookup"><span data-stu-id="ca18d-136">Microsoft Azure – secure IoT infrastructure for your business</span></span>](../iot-suite/securing-iot-ground-up.md#microsoft-azure---secure-iot-infrastructure-for-your-business)

## <a name="best-practices"></a><span data-ttu-id="ca18d-137">Najlepsze rozwiązania</span><span class="sxs-lookup"><span data-stu-id="ca18d-137">Best Practices</span></span>
<span data-ttu-id="ca18d-138">Zabezpieczanie infrastruktury IoT wymaga rygorystyczne strategii zabezpieczeń zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="ca18d-138">Securing an IoT infrastructure requires a rigorous security-in-depth strategy.</span></span> <span data-ttu-id="ca18d-139">Z Zabezpieczanie danych w chmurze hello ochronę integralności danych podczas przesyłania w hello publicznej sieci internet, inicjowania obsługi administracyjnej urządzeń toosecurely, każda warstwa kompilacje gwarancję zabezpieczeń hello całej infrastruktury.</span><span class="sxs-lookup"><span data-stu-id="ca18d-139">From securing data in hello cloud, protecting data integrity while in transit over hello public internet, toosecurely provisioning devices, each layer builds greater security assurance in hello overall infrastructure.</span></span>

<span data-ttu-id="ca18d-140">Informacje na temat zabezpieczeń Internetu rzeczy najlepsze rozwiązania w zakresie odczytując [najlepszych rozwiązań dotyczących zabezpieczeń Internetu rzeczy](../iot-suite/iot-security-best-practices.md).</span><span class="sxs-lookup"><span data-stu-id="ca18d-140">You can learn about Internet of Things security best practices by reading [Internet of Things security best practices](../iot-suite/iot-security-best-practices.md).</span></span>

<span data-ttu-id="ca18d-141">Witaj omówiono hello następujące tematy:</span><span class="sxs-lookup"><span data-stu-id="ca18d-141">hello article discusses hello following topics:</span></span>

* [<span data-ttu-id="ca18d-142">Producenta sprzętu IoT/integrator</span><span class="sxs-lookup"><span data-stu-id="ca18d-142">IoT hardware manufacturer/integrator</span></span>](../iot-suite/iot-security-best-practices.md#iot-hardware-manufacturerintegrator)
* [<span data-ttu-id="ca18d-143">Deweloper rozwiązania IoT</span><span class="sxs-lookup"><span data-stu-id="ca18d-143">IoT solution developer</span></span>](../iot-suite/iot-security-best-practices.md#iot-solution-developer)
* [<span data-ttu-id="ca18d-144">Narzędzie wdrażania rozwiązania IoT</span><span class="sxs-lookup"><span data-stu-id="ca18d-144">IoT solution deployer</span></span>](../iot-suite/iot-security-best-practices.md#iot-solution-deployer)
* [<span data-ttu-id="ca18d-145">Operator rozwiązania IoT</span><span class="sxs-lookup"><span data-stu-id="ca18d-145">IoT solution operator</span></span>](../iot-suite/iot-security-best-practices.md#iot-solution-operator)
