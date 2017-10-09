---
title: "aaaInternet rzeczy najlepsze rozwiązania w zakresie zabezpieczeń | Dokumentacja firmy Microsoft"
description: "Witaj artykuł zawiera listę nadzorowaną dotyczącą programu Microsoft Internet rzeczy najlepsze rozwiązania i ogólne zalecenia."
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
ms.openlocfilehash: 7ee31c912e8ac230ffa5efcd5b4c2b0b0713584f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="internet-of-things-security-best-practices"></a><span data-ttu-id="9469d-103">Internet rzeczy najlepsze rozwiązania w zakresie zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="9469d-103">Internet of Things Security Best Practices</span></span>
<span data-ttu-id="9469d-104">Zabezpieczanie infrastruktury Internetu rzeczy (IoT) hello jest krytyczne przedsiębiorstwa dla każdego związanego z rozwiązania IoT.</span><span class="sxs-lookup"><span data-stu-id="9469d-104">Securing hello Internet of Things (IoT) infrastructure is a critical undertaking for anyone involved with IoT solutions.</span></span> <span data-ttu-id="9469d-105">Ze względu na powitania liczbę urządzeń i hello toocompromise miliony urządzenia IoT jest nieuproszczony i może mieć wpływ powszechnie związanych z Rozproszony charakter tych urządzeń, hello wpływ zdarzeń zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="9469d-105">Because of hello number of devices involved and hello distributed nature of these devices, hello impact a security event related toocompromise of millions of IoT devices is non-trivial and can have widespread impact.</span></span>

<span data-ttu-id="9469d-106">Z tego powodu podejście zabezpieczeń zabezpieczeń w zakresie zabezpieczeń IoT.</span><span class="sxs-lookup"><span data-stu-id="9469d-106">For this reason, IoT security needs a security-in-depth approach.</span></span> <span data-ttu-id="9469d-107">Przenosi danych potrzeb toobe bezpiecznego w chmurze hello i jak w sieciach prywatnych i publicznych.</span><span class="sxs-lookup"><span data-stu-id="9469d-107">Data needs toobe secure in hello cloud and as it moves over private and public networks.</span></span> <span data-ttu-id="9469d-108">Metody muszą toobe w miejscu toosecurely udostępniania hello urządzenia IoT samodzielnie.</span><span class="sxs-lookup"><span data-stu-id="9469d-108">Methods need toobe in place toosecurely provision hello IoT devices themselves.</span></span> <span data-ttu-id="9469d-109">Każda warstwa z urządzenia, toonetwork, toocloud zaplecza musi silne zabezpieczenie gwarancji.</span><span class="sxs-lookup"><span data-stu-id="9469d-109">Each layer, from device, toonetwork, toocloud back-end needs strong security assurances.</span></span>

<span data-ttu-id="9469d-110">Najlepsze rozwiązania IoT mogą być podzielone na hello w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="9469d-110">IoT best practices can be categorized in hello following way:</span></span>

* <span data-ttu-id="9469d-111">IoT producenta sprzętu lub integrator</span><span class="sxs-lookup"><span data-stu-id="9469d-111">IoT hardware manufacturer or integrator</span></span>
* <span data-ttu-id="9469d-112">Deweloper rozwiązania IoT</span><span class="sxs-lookup"><span data-stu-id="9469d-112">IoT solution developer</span></span>
* <span data-ttu-id="9469d-113">Narzędzie wdrażania rozwiązania IoT</span><span class="sxs-lookup"><span data-stu-id="9469d-113">IoT solution deployer</span></span>
* <span data-ttu-id="9469d-114">Operator rozwiązania IoT</span><span class="sxs-lookup"><span data-stu-id="9469d-114">IoT solution operator</span></span>

<span data-ttu-id="9469d-115">Ten artykuł zawiera podsumowanie [Internet z innymi najlepszych rozwiązań dotyczących zabezpieczeń](../iot-suite/iot-security-best-practices.md).</span><span class="sxs-lookup"><span data-stu-id="9469d-115">This article summarizes [Internet of Things Security Best Practices](../iot-suite/iot-security-best-practices.md).</span></span> <span data-ttu-id="9469d-116">Bardziej szczegółowe informacje można znaleźć w artykule toothat.</span><span class="sxs-lookup"><span data-stu-id="9469d-116">Please refer toothat article for more detailed information.</span></span>

## <a name="iot-hardware-manufacturer-or-integrator"></a><span data-ttu-id="9469d-117">IoT producenta sprzętu lub integrator</span><span class="sxs-lookup"><span data-stu-id="9469d-117">IoT hardware manufacturer or integrator</span></span>
<span data-ttu-id="9469d-118">Wykonaj hello najlepsze rozwiązania w zakresie poniżej IoT produkcji sprzętu lub integrator sprzętu:</span><span class="sxs-lookup"><span data-stu-id="9469d-118">Follow hello best practices below if you are an IoT hardware manufacture or a hardware integrator:</span></span>

* <span data-ttu-id="9469d-119">**Zakres wymagania sprzętowe toominimum**: projekt sprzętu hello powinna zawierać minimalne funkcje wymagane dla operacji hello sprzętu i nic więcej.</span><span class="sxs-lookup"><span data-stu-id="9469d-119">**Scope hardware toominimum requirements**: hello hardware design should include minimum features required for operation of hello hardware, and nothing more.</span></span> 
* <span data-ttu-id="9469d-120">**Należy sprzętu manipulację dowód**: kompilacji w mechanizmów toodetect fizycznego manipulowania sprzętu, takich jak otwieranie hello urządzenia pokrycia, usunięcie części urządzenia hello itp.</span><span class="sxs-lookup"><span data-stu-id="9469d-120">**Make hardware tamper proof**: build in mechanisms toodetect physical tampering of hardware, such as opening hello device cover, removing a part of hello device, etc.</span></span> 
* <span data-ttu-id="9469d-121">**Tworzenie wokół bezpiecznych składników sprzętowych**: Jeśli [kst](https://en.wikipedia.org/wiki/Cost_of_goods_sold) zezwolić, tworzenia funkcji zabezpieczeń, takich jak bezpieczna i szyfrowana magazynowania i funkcji rozruchowego opartego na modułu TPM.</span><span class="sxs-lookup"><span data-stu-id="9469d-121">**Build around secure hardware**: if [COGS](https://en.wikipedia.org/wiki/Cost_of_goods_sold) permit, build security features such as secure and encrypted storage and Trusted Platform Module (TPM)-based boot functionality.</span></span>
* <span data-ttu-id="9469d-122">**Zabezpieczyć uaktualnień**: uaktualnienie oprogramowania układowego okres istnienia hello urządzenia są nieuniknione.</span><span class="sxs-lookup"><span data-stu-id="9469d-122">**Make upgrades secure**: upgrading firmware during lifetime of hello device is inevitable.</span></span>

## <a name="iot-solution-developer"></a><span data-ttu-id="9469d-123">Deweloper rozwiązania IoT</span><span class="sxs-lookup"><span data-stu-id="9469d-123">IoT solution developer</span></span>
<span data-ttu-id="9469d-124">Jeśli jesteś deweloperem rozwiązania IoT, wykonaj hello najlepsze rozwiązania w zakresie poniżej:</span><span class="sxs-lookup"><span data-stu-id="9469d-124">Follow hello best practices below if you are an IoT solution developer:</span></span>

* <span data-ttu-id="9469d-125">**Postępuj zgodnie z metodologii rozwoju oprogramowania bezpiecznego**: tworzenie bezpiecznej oprogramowania wymaga podstaw pomyśleć o zabezpieczeń z hello incepcja projektu hello wszystkich hello sposób tooits implementacji, testowania i wdrażania.</span><span class="sxs-lookup"><span data-stu-id="9469d-125">**Follow secure software development methodology**: developing secure software requires ground-up thinking about security from hello inception of hello project all hello way tooits implementation, testing, and deployment.</span></span>
* <span data-ttu-id="9469d-126">**Wybierz oprogramowanie typu open source z rozwagą**: oprogramowanie typu open source zapewnia tooquickly opracowywania rozwiązań.</span><span class="sxs-lookup"><span data-stu-id="9469d-126">**Choose open source software with care**: open source software provides an opportunity tooquickly develop solutions.</span></span>
* <span data-ttu-id="9469d-127">**Integracja z rozwagą**: istnieje wiele luk w zabezpieczeniach oprogramowania hello w granic hello bibliotek i interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="9469d-127">**Integrate with care**: many of hello software security flaws exist at hello boundary of libraries and APIs.</span></span> 

## <a name="iot-solution-deployer"></a><span data-ttu-id="9469d-128">Narzędzie wdrażania rozwiązania IoT</span><span class="sxs-lookup"><span data-stu-id="9469d-128">IoT solution deployer</span></span>
<span data-ttu-id="9469d-129">W przypadku wdrażania rozwiązania IoT, wykonaj hello najlepsze rozwiązania w zakresie poniżej:</span><span class="sxs-lookup"><span data-stu-id="9469d-129">Follow hello best practices below if you are an IoT solution deployer:</span></span>

* <span data-ttu-id="9469d-130">**Wdrażanie sprzętu bezpiecznie**: IoT wdrożenia może wymagać toobe sprzęt wdrożony w lokalizacjach niezabezpieczone, taki jak publiczny spacji lub ustawień nienadzorowanych.</span><span class="sxs-lookup"><span data-stu-id="9469d-130">**Deploy hardware securely**: IoT deployments may require hardware toobe deployed in unsecure locations, such as in public spaces or unsupervised locales.</span></span>
* <span data-ttu-id="9469d-131">**Bezpieczeństwa kluczy uwierzytelniania**: podczas wdrażania, każde urządzenie wymaga identyfikatory urządzeń i skojarzonych kluczy uwierzytelniania generowane przez usługę w chmurze hello.</span><span class="sxs-lookup"><span data-stu-id="9469d-131">**Keep authentication keys safe**: during deployment, each device requires device IDs and associated authentication keys generated by hello cloud service.</span></span> <span data-ttu-id="9469d-132">Zachowaj te klucze fizycznie bezpieczne nawet po wdrożeniu hello.</span><span class="sxs-lookup"><span data-stu-id="9469d-132">Keep these keys physically safe even after hello deployment.</span></span> <span data-ttu-id="9469d-133">Dowolny klawisz, którego bezpieczeństwo zostało naruszone mogą posłużyć toomasquerade złośliwe urządzenia jako istniejące urządzenie.</span><span class="sxs-lookup"><span data-stu-id="9469d-133">Any compromised key can be used by a malicious device toomasquerade as an existing device.</span></span>

## <a name="iot-solution-operator"></a><span data-ttu-id="9469d-134">Operator rozwiązania IoT</span><span class="sxs-lookup"><span data-stu-id="9469d-134">IoT solution operator</span></span>
<span data-ttu-id="9469d-135">Jeśli jesteś operator rozwiązania IoT, wykonaj hello najlepsze rozwiązania w zakresie poniżej:</span><span class="sxs-lookup"><span data-stu-id="9469d-135">Follow hello best practices below if you are an IoT solution operator:</span></span>

* <span data-ttu-id="9469d-136">**Zachowaj systemu toodate**: Upewnij się, systemów operacyjnych urządzeń i wszystkie sterowniki urządzeń są zaktualizowane toohello najnowszych wersji.</span><span class="sxs-lookup"><span data-stu-id="9469d-136">**Keep systems up toodate**: ensure device operating systems and all device drivers are updated toohello latest versions.</span></span> 
* <span data-ttu-id="9469d-137">**Ochrona przed złośliwych działań**: pozwala na powitania systemu operacyjnego, umieść hello najnowszych funkcji oprogramowania antywirusowego i przed złośliwym oprogramowaniem w każdym systemie operacyjnym urządzenia.</span><span class="sxs-lookup"><span data-stu-id="9469d-137">**Protect against malicious activity**: if hello operating system permits, place hello latest anti-virus and anti-malware capabilities on each device operating system.</span></span> 
* <span data-ttu-id="9469d-138">**Inspekcji, często**: inspekcja IoT infrastruktury zabezpieczeń związanych z problemów jest kluczem wysyłanej toosecurity zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="9469d-138">**Audit frequently**: auditing IoT infrastructure for security related issues is key when responding toosecurity incidents.</span></span>
* <span data-ttu-id="9469d-139">**Fizycznie ochrona powitalnych IoT infrastruktury**: hello najgorszy zabezpieczeń ataków na infrastrukturę IoT jest uruchomiony przy użyciu toodevices fizyczny dostęp.</span><span class="sxs-lookup"><span data-stu-id="9469d-139">**Physically protect hello IoT infrastructure**: hello worst security attacks against IoT infrastructure are launched using physical access toodevices.</span></span>
* <span data-ttu-id="9469d-140">**Ochrona poświadczeń w chmurze**: chmury uwierzytelniania poświadczenia używane do konfigurowania i obsługi wdrażania IoT są prawdopodobnie hello Najprostszym sposobem toogain dostępu i złamanie IoT.</span><span class="sxs-lookup"><span data-stu-id="9469d-140">**Protect cloud credentials**: cloud authentication credentials used for configuring and operating an IoT deployment are possibly hello easiest way toogain access and compromise an IoT system.</span></span> 

