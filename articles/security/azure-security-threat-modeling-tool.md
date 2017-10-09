---
title: "aaaMicrosoft narzędzia do modelowania zagrożeń - Azure | Dokumentacja firmy Microsoft"
description: "Strona główna programu Microsoft Threat modelowania narzędzia, zawierający informacje o wprowadzenie do korzystania z narzędzia hello, w tym procesie modelowania zagrożeń hello hello"
services: security
documentationcenter: na
author: RodSan
manager: RodSan
editor: RodSan
ms.assetid: na
ms.service: security
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: rodsan
ms.openlocfilehash: 923225a30c592ffdb1d254000451cfaac54a0e68
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-threat-modeling-tool"></a><span data-ttu-id="2eb03-103">Microsoft Threat Modeling Tool</span><span class="sxs-lookup"><span data-stu-id="2eb03-103">Microsoft Threat Modeling Tool</span></span>

<span data-ttu-id="2eb03-104">Narzędzia do modelowania zagrożeń Hello jest elementem core hello Microsoft Security Development Lifecycle (SDL).</span><span class="sxs-lookup"><span data-stu-id="2eb03-104">hello Threat Modeling Tool is a core element of hello Microsoft Security Development Lifecycle (SDL).</span></span> <span data-ttu-id="2eb03-105">Umożliwia oprogramowania architects tooidentify i wcześnie łagodzenia potencjalnych problemów z zabezpieczeniami, jeśli są one względnie łatwe i ekonomiczne tooresolve.</span><span class="sxs-lookup"><span data-stu-id="2eb03-105">It allows software architects tooidentify and mitigate potential security issues early, when they are relatively easy and cost-effective tooresolve.</span></span> <span data-ttu-id="2eb03-106">W związku z tym znacznie zmniejsza całkowity koszt hello rozwoju.</span><span class="sxs-lookup"><span data-stu-id="2eb03-106">As a result, it greatly reduces hello total cost of development.</span></span> <span data-ttu-id="2eb03-107">Możemy zaprojektowany narzędzia hello z ekspertami z systemem innym niż zabezpieczeń pamiętać, ułatwiając modelowanie zagrożeń dla wszystkich deweloperów zapewniając wyraźnych wskazówek dotyczących tworzenia i analizowanie modeli zagrożeń.</span><span class="sxs-lookup"><span data-stu-id="2eb03-107">Also, we designed hello tool with non-security experts in mind, making threat modeling easier for all developers by providing clear guidance on creating and analyzing threat models.</span></span> 

<span data-ttu-id="2eb03-108">Narzędzie Hello umożliwia każdemu:</span><span class="sxs-lookup"><span data-stu-id="2eb03-108">hello tool enables anyone to:</span></span>

* <span data-ttu-id="2eb03-109">Komunikować się o hello projektowania zabezpieczeń systemu</span><span class="sxs-lookup"><span data-stu-id="2eb03-109">Communicate about hello security design of their systems</span></span>
* <span data-ttu-id="2eb03-110">Analizowanie tych projektów dla potencjalnych problemów z zabezpieczeniami przy użyciu sprawdzonych metod</span><span class="sxs-lookup"><span data-stu-id="2eb03-110">Analyze those designs for potential security issues using a proven methodology</span></span>
* <span data-ttu-id="2eb03-111">Sugeruj i zarządzanie nimi czynniki związane z zabezpieczeniami</span><span class="sxs-lookup"><span data-stu-id="2eb03-111">Suggest and manage mitigations for security issues</span></span>

<span data-ttu-id="2eb03-112">Oto niektóre funkcje narzędzi i innowacji, tooname tylko kilka:</span><span class="sxs-lookup"><span data-stu-id="2eb03-112">Here are some tooling capabilities and innovations, just tooname a few:</span></span>

* <span data-ttu-id="2eb03-113">**Automatyzacja:** wskazówki i opinie w modelu rysowania.</span><span class="sxs-lookup"><span data-stu-id="2eb03-113">**Automation:** Guidance and feedback in drawing a model</span></span>
* <span data-ttu-id="2eb03-114">**STRIDE dla każdego elementu:** z przewodnikiem analizy zagrożeń i środki zaradcze</span><span class="sxs-lookup"><span data-stu-id="2eb03-114">**STRIDE per Element:** Guided analysis of threats and mitigations</span></span>
* <span data-ttu-id="2eb03-115">**Raportowanie:** działania dotyczące zabezpieczeń i testowania w fazie weryfikacji hello</span><span class="sxs-lookup"><span data-stu-id="2eb03-115">**Reporting:** Security activities and testing in hello verification phase</span></span>
* <span data-ttu-id="2eb03-116">**Metodologia unikatowy:** toobetter użytkowników umożliwia zwizualizować i zrozumieć zagrożeń</span><span class="sxs-lookup"><span data-stu-id="2eb03-116">**Unique Methodology:** Enables users toobetter visualize and understand threats</span></span>
* <span data-ttu-id="2eb03-117">**Przeznaczony dla deweloperów i wyśrodkowane na oprogramowanie:** wiele metod jest wyśrodkowywana w zasoby lub osoby atakujące.</span><span class="sxs-lookup"><span data-stu-id="2eb03-117">**Designed for Developers and Centered on Software:** many approaches are centered on assets or attackers.</span></span> <span data-ttu-id="2eb03-118">Czy firma Microsoft skupia się na oprogramowanie.</span><span class="sxs-lookup"><span data-stu-id="2eb03-118">We are centered on software.</span></span> <span data-ttu-id="2eb03-119">Oprzemy się na działania, które wszystkich deweloperów oprogramowania i architektów znasz — takie jak rysowanie obrazów na ich architektura oprogramowania</span><span class="sxs-lookup"><span data-stu-id="2eb03-119">We build on activities that all software developers and architects are familiar with -- such as drawing pictures for their software architecture</span></span>
* <span data-ttu-id="2eb03-120">**Wskazówki dotyczące projektowania analizy:** hello termin "modelowanie zagrożeń" może odnosić się tooeither, wymagania lub technika analizy projektu.</span><span class="sxs-lookup"><span data-stu-id="2eb03-120">**Focused on Design Analysis:** hello term "threat modeling" can refer tooeither a requirements or a design analysis technique.</span></span> <span data-ttu-id="2eb03-121">Czasami odwołuje się tooa złożonych mieszankę hello dwa.</span><span class="sxs-lookup"><span data-stu-id="2eb03-121">Sometimes, it refers tooa complex blend of hello two.</span></span> <span data-ttu-id="2eb03-122">modelowanie toothreat podejście Microsoft SDL Hello to technika analizy ukierunkowanych projektu</span><span class="sxs-lookup"><span data-stu-id="2eb03-122">hello Microsoft SDL approach toothreat modeling is a focused design analysis technique</span></span>

## <a name="next-steps"></a><span data-ttu-id="2eb03-123">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="2eb03-123">Next steps</span></span>

<span data-ttu-id="2eb03-124">w poniższej tabeli Hello zawiera tooget ważne łącza, uruchomienia z hello narzędzie modelowania zagrożeń:</span><span class="sxs-lookup"><span data-stu-id="2eb03-124">hello table below contains important links tooget you started with hello Threat Modeling Tool:</span></span>

| <span data-ttu-id="2eb03-125">Krok</span><span class="sxs-lookup"><span data-stu-id="2eb03-125">Step</span></span>  | <span data-ttu-id="2eb03-126">Opis</span><span class="sxs-lookup"><span data-stu-id="2eb03-126">Description</span></span>                                                                                   |
| ----- | --------------------------------------------------------------------------------------------- |
| <span data-ttu-id="2eb03-127">**1**</span><span class="sxs-lookup"><span data-stu-id="2eb03-127">**1**</span></span> | [<span data-ttu-id="2eb03-128">Pobierz hello narzędzie modelowania zagrożeń</span><span class="sxs-lookup"><span data-stu-id="2eb03-128">Download hello Threat Modeling Tool</span></span>](https://aka.ms/tmtpreview)                                |
| <span data-ttu-id="2eb03-129">**2**</span><span class="sxs-lookup"><span data-stu-id="2eb03-129">**2**</span></span> | [<span data-ttu-id="2eb03-130">Przeczytać nasze Wprowadzenie — przewodnik</span><span class="sxs-lookup"><span data-stu-id="2eb03-130">Read Our getting started guide</span></span>](./azure-security-threat-modeling-tool-getting-started.md)    |
| <span data-ttu-id="2eb03-131">**3**</span><span class="sxs-lookup"><span data-stu-id="2eb03-131">**3**</span></span> | [<span data-ttu-id="2eb03-132">Zapoznaj się z funkcjami hello</span><span class="sxs-lookup"><span data-stu-id="2eb03-132">Get familiar with hello features</span></span>](./azure-security-threat-modeling-tool-feature-overview.md)   |
| <span data-ttu-id="2eb03-133">**4**</span><span class="sxs-lookup"><span data-stu-id="2eb03-133">**4**</span></span> | [<span data-ttu-id="2eb03-134">Dowiedz się więcej o kategoriach wygenerowanego zagrożeń</span><span class="sxs-lookup"><span data-stu-id="2eb03-134">Learn about generated threat categories</span></span>](./azure-security-threat-modeling-tool-threats.md)   |
| <span data-ttu-id="2eb03-135">**5**</span><span class="sxs-lookup"><span data-stu-id="2eb03-135">**5**</span></span> | [<span data-ttu-id="2eb03-136">Znajdź środki zaradcze toogenerated zagrożeń</span><span class="sxs-lookup"><span data-stu-id="2eb03-136">Find mitigations toogenerated threats</span></span>](./azure-security-threat-modeling-tool-mitigations.md) |

## <a name="resources"></a><span data-ttu-id="2eb03-137">Zasoby</span><span class="sxs-lookup"><span data-stu-id="2eb03-137">Resources</span></span>

<span data-ttu-id="2eb03-138">Poniżej przedstawiono kilka starsze artykuły nadal obowiązują toothreat modelowania dzisiaj:</span><span class="sxs-lookup"><span data-stu-id="2eb03-138">Here are a few older articles still relevant toothreat modeling today:</span></span>

* [<span data-ttu-id="2eb03-139">Artykuł na powitania znaczenie modelowania zagrożeń</span><span class="sxs-lookup"><span data-stu-id="2eb03-139">Article on hello Importance of Threat Modeling</span></span>](https://msdn.microsoft.com/magazine/dd347831.aspx)
* [<span data-ttu-id="2eb03-140">Szkolenie opublikowanych przez wiarygodne technologie komputerowe</span><span class="sxs-lookup"><span data-stu-id="2eb03-140">Training Published by Trustworthy Computing</span></span>](https://www.microsoft.com/download/details.aspx?id=16420)

<span data-ttu-id="2eb03-141">Wyewidencjonuj co zrobić ma kilka ekspertów narzędzie modelowania zagrożeń:</span><span class="sxs-lookup"><span data-stu-id="2eb03-141">Check out what a few Threat Modeling Tool experts have done:</span></span>

* [<span data-ttu-id="2eb03-142">Menedżer zagrożeń</span><span class="sxs-lookup"><span data-stu-id="2eb03-142">Threats Manager</span></span>](https://simoneonsecurity.com/threatsmanagersetup-v1-5-10/)
* [<span data-ttu-id="2eb03-143">Blog zabezpieczeń Simone Curzi</span><span class="sxs-lookup"><span data-stu-id="2eb03-143">Simone Curzi Security Blog</span></span>](https://simoneonsecurity.com/)