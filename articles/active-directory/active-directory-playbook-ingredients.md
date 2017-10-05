---
title: "Składniki fazy weryfikacji koncepcji podręcznika dotyczącego usługi Azure Active Directory | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: d2a0fe280f143d390f5e4ba40e0ebe92d8a4a837
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-active-directory-proof-of-concept-playbook-ingredients"></a><span data-ttu-id="eb3a4-104">Usługa Azure Active Directory dowód koncepcji podręcznika dotyczącego składników</span><span class="sxs-lookup"><span data-stu-id="eb3a4-104">Azure Active Directory Proof of Concept Playbook Ingredients</span></span> 

## <a name="theme"></a><span data-ttu-id="eb3a4-105">Motyw</span><span class="sxs-lookup"><span data-stu-id="eb3a4-105">Theme</span></span>
<span data-ttu-id="eb3a4-106">Usługa Azure AD zapewnia rozwiązania tożsamościami i dostępem w wielu obszarach w przedsiębiorstwie.</span><span class="sxs-lookup"><span data-stu-id="eb3a4-106">Azure AD provides identity and access solutions across multiple areas in the enterprise.</span></span> <span data-ttu-id="eb3a4-107">Firma Microsoft klasyfikowania scenariusze w następujących obszarach:</span><span class="sxs-lookup"><span data-stu-id="eb3a4-107">We classify the scenarios in the following areas:</span></span> 

* [<span data-ttu-id="eb3a4-108">Wiele aplikacji i jednej tożsamości</span><span class="sxs-lookup"><span data-stu-id="eb3a4-108">Lots of apps, one identity</span></span>](active-directory-playbook-implementation.md#theme---lots-of-apps-one-identity) 
* [<span data-ttu-id="eb3a4-109">Zwiększające bezpieczeństwo</span><span class="sxs-lookup"><span data-stu-id="eb3a4-109">Increase your security</span></span>](active-directory-playbook-implementation.md#theme---increase-your-security) 
* [<span data-ttu-id="eb3a4-110">Skalowalność samoobsługi</span><span class="sxs-lookup"><span data-stu-id="eb3a4-110">Scale with Self Service</span></span>](active-directory-playbook-implementation.md#theme---scale-with-self-service) 

<span data-ttu-id="eb3a4-111">Definiowanie motyw do ramki fazy weryfikacji koncepcji pozwala skupić się wysiłków o korzyściach z cele biznesowe, które często są wyzwalacze zainteresowanie weryfikacji koncepcji w pierwszej kolejności.</span><span class="sxs-lookup"><span data-stu-id="eb3a4-111">Defining a theme to frame the PoC helps to focus the efforts that resonates with business goals, which oftentimes are the triggers of the interest in a proof of concept in the first place.</span></span> 

## <a name="environment"></a><span data-ttu-id="eb3a4-112">Środowisko</span><span class="sxs-lookup"><span data-stu-id="eb3a4-112">Environment</span></span>

<span data-ttu-id="eb3a4-113">Należy określić szczegóły środowisko, w którym będzie dostarczać fazy weryfikacji koncepcji.</span><span class="sxs-lookup"><span data-stu-id="eb3a4-113">It is important to determine the details of the environment where you will deliver the PoC.</span></span> <span data-ttu-id="eb3a4-114">W idealnym przypadku można tworzyć na niej po zakończeniu weryfikacji koncepcji.</span><span class="sxs-lookup"><span data-stu-id="eb3a4-114">Ideally you can build upon it after the PoC is completed.</span></span> <span data-ttu-id="eb3a4-115">Środowisko docelowe odgrywa kluczową rolę i powinna być widoczna kompromisu między go jako prawdziwe, jak to możliwe i koszty ograniczeń lub dodatkowe zagadnienia.</span><span class="sxs-lookup"><span data-stu-id="eb3a4-115">The target environment is crucial and you should find the right balance between making it as real as possible and the overhead of constraints or extra considerations.</span></span> <span data-ttu-id="eb3a4-116">Środowisk do weryfikacji koncepcji są:</span><span class="sxs-lookup"><span data-stu-id="eb3a4-116">The typical environments for PoCs are:</span></span>
* <span data-ttu-id="eb3a4-117">**Produkcja:** scenariusze są realizowane w środowisku na żywo i już wdrożone usługi Microsoft Cloud (środowisko produkcyjne AD, Office 365, rozwiązanie SSO/dzierżawy usługi Azure AD).</span><span class="sxs-lookup"><span data-stu-id="eb3a4-117">**Production:** The scenarios will be implemented in your live environment and already deployed Microsoft Cloud services (production AD, Office 365, Azure AD tenant/SSO solution).</span></span> 
* <span data-ttu-id="eb3a4-118">**Użytkownik akceptacji testu Akceptacyjne / środowiska deweloperskiego:** infrastruktury testu (równoległe AD i potencjalnie Azure AD rozwiązania dzierżawy/logowania jednokrotnego) z danych testowych, podobny do produkcji.</span><span class="sxs-lookup"><span data-stu-id="eb3a4-118">**User Acceptance Test (UAT)/Dev environment:** You have test infrastructure (parallel AD and potentially Azure AD tenant/SSO solution) with test data that resembles production.</span></span> <span data-ttu-id="eb3a4-119">Zazwyczaj środowiska testowego jest współużytkowana przez wielu projektów w przedsiębiorstwie.</span><span class="sxs-lookup"><span data-stu-id="eb3a4-119">Typically, the test environment is shared across multiple projects in the enterprise.</span></span>

<span data-ttu-id="eb3a4-120">Większość scenariuszy, w tym przewodniku są addytywne charakter.</span><span class="sxs-lookup"><span data-stu-id="eb3a4-120">Most scenarios in this guide are additive in nature.</span></span> <span data-ttu-id="eb3a4-121">W związku z tym ich można wdrożyć w dzierżawie produkcyjnego bez wpływu na użytkowników spoza fazy weryfikacji koncepcji.</span><span class="sxs-lookup"><span data-stu-id="eb3a4-121">As a result, they can be deployed in the production tenant without affecting users outside the PoC.</span></span> <span data-ttu-id="eb3a4-122">W tym dokumencie Zadzwonimy limit scenariusze, które ma wpływ na poziomie dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="eb3a4-122">Throughout this document, we will be calling out which scenarios would have tenant-wide effect.</span></span> <span data-ttu-id="eb3a4-123">W takich przypadkach można wziąć pod uwagę środowiskach nieprodukcyjnych.</span><span class="sxs-lookup"><span data-stu-id="eb3a4-123">In those cases, you might want to consider a non-production environment.</span></span> 


## <a name="target-users"></a><span data-ttu-id="eb3a4-124">Użytkownicy docelowi</span><span class="sxs-lookup"><span data-stu-id="eb3a4-124">Target Users</span></span>

<span data-ttu-id="eb3a4-125">Należy ustalić docelowy zbiór użytkowników, które wykonują scenariuszy, szczególnie w przypadku, gdy środowisko jest środowisko produkcyjne lub testu.</span><span class="sxs-lookup"><span data-stu-id="eb3a4-125">It is important to determine the target set of users that will exercise the scenarios, especially when the environment is production or test.</span></span> <span data-ttu-id="eb3a4-126">Kategorie użytkowników docelowych do weryfikacji koncepcji są:</span><span class="sxs-lookup"><span data-stu-id="eb3a4-126">The categories of target users for PoC are:</span></span>
* <span data-ttu-id="eb3a4-127">**Użytkownicy pilotażowi:** rzeczywistych użytkowników w środowisku, który będzie używany w rozwiązaniu przy użyciu konta, które używają w swoich funkcji codzienne zadania</span><span class="sxs-lookup"><span data-stu-id="eb3a4-127">**Pilot Users:** Real users in the environment that will be using the solution with the account they use for their day to day job functions</span></span>
* <span data-ttu-id="eb3a4-128">**Użytkowników testowych:** konta tworzone w środowisko testowe</span><span class="sxs-lookup"><span data-stu-id="eb3a4-128">**Test Users:** Test accounts created in the environment</span></span> 

<span data-ttu-id="eb3a4-129">Większość scenariuszy, w tym przewodniku może być wykonywane przez użytkowników pilotażowych.</span><span class="sxs-lookup"><span data-stu-id="eb3a4-129">Most scenarios in this guide can be exercised by pilot users.</span></span> <span data-ttu-id="eb3a4-130">W tym dokumencie Zadzwonimy limit uwagi dotyczące użytkownika docelowego w razie potrzeby.</span><span class="sxs-lookup"><span data-stu-id="eb3a4-130">Throughout this document, we will be calling out target user considerations if needed.</span></span>


[!INCLUDE [active-directory-playbook-toc](../../includes/active-directory-playbook-steps.md)]