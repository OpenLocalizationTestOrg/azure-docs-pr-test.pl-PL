---
title: "aaaAzure składników podręcznika dotyczącego fazy weryfikacji koncepcji w usłudze Active Directory | Dokumentacja firmy Microsoft"
description: "Eksploruj i szybkie rozpoczęcie scenariusze Zarządzanie tożsamościami i dostępem"
services: active-directory
keywords: "Usługa Azure active directory, podręcznika dotyczącego koncepcji, aby zapewnić"
documentationcenter: 
author: dstefanMSFT
manager: asuthar
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 4/12/2017
ms.author: dstefan
ms.openlocfilehash: 0a7f5cd659b9d62ac86e3c27e5727294d481f4a2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-proof-of-concept-playbook-ingredients"></a><span data-ttu-id="8a05f-104">Usługa Azure Active Directory dowód koncepcji podręcznika dotyczącego składników</span><span class="sxs-lookup"><span data-stu-id="8a05f-104">Azure Active Directory Proof of Concept Playbook Ingredients</span></span> 

## <a name="theme"></a><span data-ttu-id="8a05f-105">Motyw</span><span class="sxs-lookup"><span data-stu-id="8a05f-105">Theme</span></span>
<span data-ttu-id="8a05f-106">Usługa Azure AD zapewnia rozwiązania tożsamościami i dostępem w wielu obszarach w przedsiębiorstwie hello.</span><span class="sxs-lookup"><span data-stu-id="8a05f-106">Azure AD provides identity and access solutions across multiple areas in hello enterprise.</span></span> <span data-ttu-id="8a05f-107">Firma Microsoft klasyfikowania scenariusze hello w hello następujące obszary:</span><span class="sxs-lookup"><span data-stu-id="8a05f-107">We classify hello scenarios in hello following areas:</span></span> 

* [<span data-ttu-id="8a05f-108">Wiele aplikacji i jednej tożsamości</span><span class="sxs-lookup"><span data-stu-id="8a05f-108">Lots of apps, one identity</span></span>](active-directory-playbook-implementation.md#theme---lots-of-apps-one-identity) 
* [<span data-ttu-id="8a05f-109">Zwiększające bezpieczeństwo</span><span class="sxs-lookup"><span data-stu-id="8a05f-109">Increase your security</span></span>](active-directory-playbook-implementation.md#theme---increase-your-security) 
* [<span data-ttu-id="8a05f-110">Skalowalność samoobsługi</span><span class="sxs-lookup"><span data-stu-id="8a05f-110">Scale with Self Service</span></span>](active-directory-playbook-implementation.md#theme---scale-with-self-service) 

<span data-ttu-id="8a05f-111">Definiowania motywu tooframe hello fazy weryfikacji koncepcji pomaga wysiłków hello toofocus o korzyściach z cele biznesowe, które często są hello wyzwalaczy hello zainteresowanie weryfikacji koncepcji w miejscu pierwszego hello.</span><span class="sxs-lookup"><span data-stu-id="8a05f-111">Defining a theme tooframe hello PoC helps toofocus hello efforts that resonates with business goals, which oftentimes are hello triggers of hello interest in a proof of concept in hello first place.</span></span> 

## <a name="environment"></a><span data-ttu-id="8a05f-112">Środowisko</span><span class="sxs-lookup"><span data-stu-id="8a05f-112">Environment</span></span>

<span data-ttu-id="8a05f-113">Jest ważne toodetermine hello szczegóły środowiska hello, gdzie będzie dostarczać hello fazy weryfikacji koncepcji.</span><span class="sxs-lookup"><span data-stu-id="8a05f-113">It is important toodetermine hello details of hello environment where you will deliver hello PoC.</span></span> <span data-ttu-id="8a05f-114">W idealnym przypadku tworzenie można na niej po zakończeniu weryfikacji koncepcji powitalne.</span><span class="sxs-lookup"><span data-stu-id="8a05f-114">Ideally you can build upon it after hello PoC is completed.</span></span> <span data-ttu-id="8a05f-115">środowisko docelowe Hello odgrywa kluczową rolę i powinna być widoczna hello kompromisu między go jako prawdziwe, jak to możliwe i koszty hello ograniczeń lub dodatkowe zagadnienia.</span><span class="sxs-lookup"><span data-stu-id="8a05f-115">hello target environment is crucial and you should find hello right balance between making it as real as possible and hello overhead of constraints or extra considerations.</span></span> <span data-ttu-id="8a05f-116">Witaj środowisk weryfikacji koncepcji są:</span><span class="sxs-lookup"><span data-stu-id="8a05f-116">hello typical environments for PoCs are:</span></span>
* <span data-ttu-id="8a05f-117">**Produkcja:** scenariusze hello są realizowane w środowisku na żywo i już wdrożone usługi Microsoft Cloud (środowisko produkcyjne AD, Office 365, rozwiązanie SSO/dzierżawy usługi Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8a05f-117">**Production:** hello scenarios will be implemented in your live environment and already deployed Microsoft Cloud services (production AD, Office 365, Azure AD tenant/SSO solution).</span></span> 
* <span data-ttu-id="8a05f-118">**Użytkownik akceptacji testu Akceptacyjne / środowiska deweloperskiego:** infrastruktury testu (równoległe AD i potencjalnie Azure AD rozwiązania dzierżawy/logowania jednokrotnego) z danych testowych, podobny do produkcji.</span><span class="sxs-lookup"><span data-stu-id="8a05f-118">**User Acceptance Test (UAT)/Dev environment:** You have test infrastructure (parallel AD and potentially Azure AD tenant/SSO solution) with test data that resembles production.</span></span> <span data-ttu-id="8a05f-119">Zazwyczaj środowiska testowego hello jest współużytkowana przez wielu projektów w przedsiębiorstwie hello.</span><span class="sxs-lookup"><span data-stu-id="8a05f-119">Typically, hello test environment is shared across multiple projects in hello enterprise.</span></span>

<span data-ttu-id="8a05f-120">Większość scenariuszy, w tym przewodniku są addytywne charakter.</span><span class="sxs-lookup"><span data-stu-id="8a05f-120">Most scenarios in this guide are additive in nature.</span></span> <span data-ttu-id="8a05f-121">W związku z tym ich można wdrożyć w dzierżawie produkcji hello bez wpływu na użytkowników spoza hello fazy weryfikacji koncepcji.</span><span class="sxs-lookup"><span data-stu-id="8a05f-121">As a result, they can be deployed in hello production tenant without affecting users outside hello PoC.</span></span> <span data-ttu-id="8a05f-122">W tym dokumencie Zadzwonimy limit scenariusze, które ma wpływ na poziomie dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="8a05f-122">Throughout this document, we will be calling out which scenarios would have tenant-wide effect.</span></span> <span data-ttu-id="8a05f-123">W takich przypadkach możesz tooconsider środowiskach nieprodukcyjnych.</span><span class="sxs-lookup"><span data-stu-id="8a05f-123">In those cases, you might want tooconsider a non-production environment.</span></span> 


## <a name="target-users"></a><span data-ttu-id="8a05f-124">Użytkownicy docelowi</span><span class="sxs-lookup"><span data-stu-id="8a05f-124">Target Users</span></span>

<span data-ttu-id="8a05f-125">Jest ważne toodetermine hello docelowy zbiór użytkowników, które wykonują hello scenariuszy, szczególnie w przypadku, gdy środowisko hello jest środowisko produkcyjne lub testu.</span><span class="sxs-lookup"><span data-stu-id="8a05f-125">It is important toodetermine hello target set of users that will exercise hello scenarios, especially when hello environment is production or test.</span></span> <span data-ttu-id="8a05f-126">kategorie Hello użytkowników docelowych do weryfikacji koncepcji są:</span><span class="sxs-lookup"><span data-stu-id="8a05f-126">hello categories of target users for PoC are:</span></span>
* <span data-ttu-id="8a05f-127">**Użytkownicy pilotażowi:** funkcji zadań rzeczywistych użytkowników w środowisku hello, który będzie używany w rozwiązaniu hello z kontem hello używają w swoich tooday dnia</span><span class="sxs-lookup"><span data-stu-id="8a05f-127">**Pilot Users:** Real users in hello environment that will be using hello solution with hello account they use for their day tooday job functions</span></span>
* <span data-ttu-id="8a05f-128">**Użytkowników testowych:** konta tworzone w środowisku hello testowe</span><span class="sxs-lookup"><span data-stu-id="8a05f-128">**Test Users:** Test accounts created in hello environment</span></span> 

<span data-ttu-id="8a05f-129">Większość scenariuszy, w tym przewodniku może być wykonywane przez użytkowników pilotażowych.</span><span class="sxs-lookup"><span data-stu-id="8a05f-129">Most scenarios in this guide can be exercised by pilot users.</span></span> <span data-ttu-id="8a05f-130">W tym dokumencie Zadzwonimy limit uwagi dotyczące użytkownika docelowego w razie potrzeby.</span><span class="sxs-lookup"><span data-stu-id="8a05f-130">Throughout this document, we will be calling out target user considerations if needed.</span></span>


[!INCLUDE [active-directory-playbook-toc](../../includes/active-directory-playbook-steps.md)]