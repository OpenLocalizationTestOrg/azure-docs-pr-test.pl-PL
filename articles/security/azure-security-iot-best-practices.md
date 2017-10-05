---
title: "Internet rzeczy najlepsze rozwiązania w zakresie zabezpieczeń | Dokumentacja firmy Microsoft"
description: "Artykuł zawiera listę nadzorowaną dotyczącą programu Microsoft Internet rzeczy najlepsze rozwiązania i ogólne zalecenia."
services: security
documentationcenter: na
author: TomShinder
manager: StevenPo
editor: TomSh
ms.assetid: 2d5598c5-4c30-481d-b8f4-51ee024ea9a7
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/04/2017
ms.author: yurid
ms.openlocfilehash: 8efc0053458e338ac1afe98d9ce970c1d5cbfa81
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="internet-of-things-security-best-practices"></a><span data-ttu-id="c1635-103">Internet rzeczy najlepsze rozwiązania w zakresie zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="c1635-103">Internet of Things Security Best Practices</span></span>
<span data-ttu-id="c1635-104">Zabezpieczanie infrastruktury Internetu rzeczy (IoT) jest krytyczne przedsiębiorstwa dla każdego związanego z rozwiązania IoT.</span><span class="sxs-lookup"><span data-stu-id="c1635-104">Securing the Internet of Things (IoT) infrastructure is a critical undertaking for anyone involved with IoT solutions.</span></span> <span data-ttu-id="c1635-105">Ze względu na liczbę urządzeń i Rozproszony charakter tych urządzeń wpływ zdarzeń zabezpieczeń związane z naruszenia miliony urządzenia IoT jest nieuproszczony i może mieć wpływ powszechnie.</span><span class="sxs-lookup"><span data-stu-id="c1635-105">Because of the number of devices involved and the distributed nature of these devices, the impact a security event related to compromise of millions of IoT devices is non-trivial and can have widespread impact.</span></span>

<span data-ttu-id="c1635-106">Z tego powodu podejście zabezpieczeń zabezpieczeń w zakresie zabezpieczeń IoT.</span><span class="sxs-lookup"><span data-stu-id="c1635-106">For this reason, IoT security needs a security-in-depth approach.</span></span> <span data-ttu-id="c1635-107">Dane muszą być bezpieczne w chmurze i przesyłane za pośrednictwem sieci prywatnej i publicznej.</span><span class="sxs-lookup"><span data-stu-id="c1635-107">Data needs to be secure in the cloud and as it moves over private and public networks.</span></span> <span data-ttu-id="c1635-108">Metody muszą być spełnione, aby bezpiecznie udostępnić z samymi urządzeniami IoT.</span><span class="sxs-lookup"><span data-stu-id="c1635-108">Methods need to be in place to securely provision the IoT devices themselves.</span></span> <span data-ttu-id="c1635-109">Każda warstwa z urządzenia do sieci wewnętrznej w chmurze musi silne zabezpieczenie gwarancji.</span><span class="sxs-lookup"><span data-stu-id="c1635-109">Each layer, from device, to network, to cloud back-end needs strong security assurances.</span></span>

<span data-ttu-id="c1635-110">Najlepsze rozwiązania IoT mogą zostać podzielone w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="c1635-110">IoT best practices can be categorized in the following way:</span></span>

* <span data-ttu-id="c1635-111">IoT producenta sprzętu lub integrator</span><span class="sxs-lookup"><span data-stu-id="c1635-111">IoT hardware manufacturer or integrator</span></span>
* <span data-ttu-id="c1635-112">Deweloper rozwiązania IoT</span><span class="sxs-lookup"><span data-stu-id="c1635-112">IoT solution developer</span></span>
* <span data-ttu-id="c1635-113">Narzędzie wdrażania rozwiązania IoT</span><span class="sxs-lookup"><span data-stu-id="c1635-113">IoT solution deployer</span></span>
* <span data-ttu-id="c1635-114">Operator rozwiązania IoT</span><span class="sxs-lookup"><span data-stu-id="c1635-114">IoT solution operator</span></span>

<span data-ttu-id="c1635-115">Ten artykuł zawiera podsumowanie [Internet z innymi najlepszych rozwiązań dotyczących zabezpieczeń](../iot-suite/iot-security-best-practices.md).</span><span class="sxs-lookup"><span data-stu-id="c1635-115">This article summarizes [Internet of Things Security Best Practices](../iot-suite/iot-security-best-practices.md).</span></span> <span data-ttu-id="c1635-116">Można znaleźć w tym artykule, aby uzyskać szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="c1635-116">Please refer to that article for more detailed information.</span></span>

## <a name="iot-hardware-manufacturer-or-integrator"></a><span data-ttu-id="c1635-117">IoT producenta sprzętu lub integrator</span><span class="sxs-lookup"><span data-stu-id="c1635-117">IoT hardware manufacturer or integrator</span></span>
<span data-ttu-id="c1635-118">Wykonaj poniższe najlepsze rozwiązania IoT produkcji sprzętu lub integrator sprzętu:</span><span class="sxs-lookup"><span data-stu-id="c1635-118">Follow the best practices below if you are an IoT hardware manufacture or a hardware integrator:</span></span>

* <span data-ttu-id="c1635-119">**Zakres sprzętu do minimalnych wymagań**: projekt sprzętu powinna zawierać minimalne funkcje wymagane dla operacji sprzętu i nic więcej.</span><span class="sxs-lookup"><span data-stu-id="c1635-119">**Scope hardware to minimum requirements**: the hardware design should include minimum features required for operation of the hardware, and nothing more.</span></span> 
* <span data-ttu-id="c1635-120">**Należy sprzętu manipulację dowód**: kompilacji w mechanizmów przed naruszeniem fizycznego sprzętu, takich jak otwieranie pokrywy urządzenia, usunięcie części urządzenia itd.</span><span class="sxs-lookup"><span data-stu-id="c1635-120">**Make hardware tamper proof**: build in mechanisms to detect physical tampering of hardware, such as opening the device cover, removing a part of the device, etc.</span></span> 
* <span data-ttu-id="c1635-121">**Tworzenie wokół bezpiecznych składników sprzętowych**: Jeśli [kst](https://en.wikipedia.org/wiki/Cost_of_goods_sold) zezwolić, tworzenia funkcji zabezpieczeń, takich jak bezpieczna i szyfrowana magazynowania i funkcji rozruchowego opartego na modułu TPM.</span><span class="sxs-lookup"><span data-stu-id="c1635-121">**Build around secure hardware**: if [COGS](https://en.wikipedia.org/wiki/Cost_of_goods_sold) permit, build security features such as secure and encrypted storage and Trusted Platform Module (TPM)-based boot functionality.</span></span>
* <span data-ttu-id="c1635-122">**Zabezpieczyć uaktualnień**: uaktualnienie oprogramowania układowego okres istnienia urządzenia są nieuniknione.</span><span class="sxs-lookup"><span data-stu-id="c1635-122">**Make upgrades secure**: upgrading firmware during lifetime of the device is inevitable.</span></span>

## <a name="iot-solution-developer"></a><span data-ttu-id="c1635-123">Deweloper rozwiązania IoT</span><span class="sxs-lookup"><span data-stu-id="c1635-123">IoT solution developer</span></span>
<span data-ttu-id="c1635-124">Jeśli jesteś deweloperem rozwiązania IoT, wykonaj poniższe najlepsze rozwiązania:</span><span class="sxs-lookup"><span data-stu-id="c1635-124">Follow the best practices below if you are an IoT solution developer:</span></span>

* <span data-ttu-id="c1635-125">**Postępuj zgodnie z metodologii rozwoju oprogramowania bezpiecznego**: tworzenie bezpiecznej oprogramowania wymaga podstaw planowania zabezpieczeń od momentu rozpoczęcia projektu aż do jej wdrożenia, testowania i wdrażania.</span><span class="sxs-lookup"><span data-stu-id="c1635-125">**Follow secure software development methodology**: developing secure software requires ground-up thinking about security from the inception of the project all the way to its implementation, testing, and deployment.</span></span>
* <span data-ttu-id="c1635-126">**Wybierz oprogramowanie typu open source z rozwagą**: oprogramowanie typu open source zapewnia możliwość szybkiego opracowywania rozwiązań.</span><span class="sxs-lookup"><span data-stu-id="c1635-126">**Choose open source software with care**: open source software provides an opportunity to quickly develop solutions.</span></span>
* <span data-ttu-id="c1635-127">**Integracja z rozwagą**: istnieje wiele luk w zabezpieczeniach oprogramowania na granicy bibliotek i interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="c1635-127">**Integrate with care**: many of the software security flaws exist at the boundary of libraries and APIs.</span></span> 

## <a name="iot-solution-deployer"></a><span data-ttu-id="c1635-128">Narzędzie wdrażania rozwiązania IoT</span><span class="sxs-lookup"><span data-stu-id="c1635-128">IoT solution deployer</span></span>
<span data-ttu-id="c1635-129">Wykonaj poniższe najlepsze rozwiązania w przypadku wdrażania rozwiązania IoT:</span><span class="sxs-lookup"><span data-stu-id="c1635-129">Follow the best practices below if you are an IoT solution deployer:</span></span>

* <span data-ttu-id="c1635-130">**Wdrażanie sprzętu bezpiecznie**: IoT wdrożenia może wymagać sprzętu, który ma zostać wdrożony w lokalizacjach niezabezpieczone, taki jak publiczny spacji lub ustawień nienadzorowanych.</span><span class="sxs-lookup"><span data-stu-id="c1635-130">**Deploy hardware securely**: IoT deployments may require hardware to be deployed in unsecure locations, such as in public spaces or unsupervised locales.</span></span>
* <span data-ttu-id="c1635-131">**Bezpieczeństwa kluczy uwierzytelniania**: podczas wdrażania, każde urządzenie wymaga identyfikatory urządzeń i skojarzonych kluczy uwierzytelniania generowane przez usługę w chmurze.</span><span class="sxs-lookup"><span data-stu-id="c1635-131">**Keep authentication keys safe**: during deployment, each device requires device IDs and associated authentication keys generated by the cloud service.</span></span> <span data-ttu-id="c1635-132">Zachowaj te klucze fizycznie bezpieczne nawet po wdrożeniu.</span><span class="sxs-lookup"><span data-stu-id="c1635-132">Keep these keys physically safe even after the deployment.</span></span> <span data-ttu-id="c1635-133">Dowolny klawisz, którego bezpieczeństwo zostało naruszone można za pomocą złośliwych urządzenia udają istniejące urządzenie.</span><span class="sxs-lookup"><span data-stu-id="c1635-133">Any compromised key can be used by a malicious device to masquerade as an existing device.</span></span>

## <a name="iot-solution-operator"></a><span data-ttu-id="c1635-134">Operator rozwiązania IoT</span><span class="sxs-lookup"><span data-stu-id="c1635-134">IoT solution operator</span></span>
<span data-ttu-id="c1635-135">Wykonaj poniższe najlepsze rozwiązania w przypadku operator rozwiązania IoT:</span><span class="sxs-lookup"><span data-stu-id="c1635-135">Follow the best practices below if you are an IoT solution operator:</span></span>

* <span data-ttu-id="c1635-136">**Aktualności systemów**: Upewnij się, systemów operacyjnych urządzeń i wszystkie sterowniki zostały zaktualizowane do najnowszej wersji.</span><span class="sxs-lookup"><span data-stu-id="c1635-136">**Keep systems up to date**: ensure device operating systems and all device drivers are updated to the latest versions.</span></span> 
* <span data-ttu-id="c1635-137">**Ochrona przed złośliwych działań**: pozwala na system operacyjny, umieść najnowszych funkcji oprogramowania antywirusowego i przed złośliwym oprogramowaniem w każdym systemie operacyjnym urządzenia.</span><span class="sxs-lookup"><span data-stu-id="c1635-137">**Protect against malicious activity**: if the operating system permits, place the latest anti-virus and anti-malware capabilities on each device operating system.</span></span> 
* <span data-ttu-id="c1635-138">**Inspekcji, często**: inspekcja IoT infrastruktury zabezpieczeń związanych z problemów jest kluczem podczas reagowania na przypadki naruszenia zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="c1635-138">**Audit frequently**: auditing IoT infrastructure for security related issues is key when responding to security incidents.</span></span>
* <span data-ttu-id="c1635-139">**Fizycznie ochrona infrastruktury IoT**: najgorszy ataki zabezpieczeń infrastruktury IoT jest uruchomiony przy użyciu fizyczny dostęp do urządzeń.</span><span class="sxs-lookup"><span data-stu-id="c1635-139">**Physically protect the IoT infrastructure**: the worst security attacks against IoT infrastructure are launched using physical access to devices.</span></span>
* <span data-ttu-id="c1635-140">**Ochrona poświadczeń w chmurze**: chmury uwierzytelniania poświadczenia używane do konfigurowania i obsługi wdrażania IoT są prawdopodobnie najłatwiejszym sposobem na uzyskanie dostępu i złamanie IoT.</span><span class="sxs-lookup"><span data-stu-id="c1635-140">**Protect cloud credentials**: cloud authentication credentials used for configuring and operating an IoT deployment are possibly the easiest way to gain access and compromise an IoT system.</span></span> 

