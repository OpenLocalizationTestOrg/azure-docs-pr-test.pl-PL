---
title: "Wprowadzenie fazy weryfikacji koncepcji podręcznika dotyczącego usługi Azure Active Directory | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 567f3373594bc53435e8c0bd0a3445dd318af1cd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-active-directory-proof-of-concept-playbook-introduction"></a><span data-ttu-id="58de0-104">Dowód koncepcji podręcznika dotyczącego usługi Azure Active Directory: wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="58de0-104">Azure Active Directory Proof of Concept Playbook: Introduction</span></span>

<span data-ttu-id="58de0-105">Ten artykuł zawiera wskazówki, aby zapoznać się z różnych Azure AD możliwości w koncepcji (PoC).</span><span class="sxs-lookup"><span data-stu-id="58de0-105">This article provides guidelines to explore different Azure AD capabilities in a Proof of Concept (PoC).</span></span> <span data-ttu-id="58de0-106">Docelowa grupa odbiorców tego dokumentu jest architektów tożsamości, specjalistów IT i integratorów systemów. platforma</span><span class="sxs-lookup"><span data-stu-id="58de0-106">The intended audience of this document is Identity Architects, IT Professionals, and System Integrators</span></span>

## <a name="how-to-use-this-playbook"></a><span data-ttu-id="58de0-107">Jak używać tego podręcznika dotyczącego</span><span class="sxs-lookup"><span data-stu-id="58de0-107">How to use this Playbook</span></span>

1. <span data-ttu-id="58de0-108">Użyj [motyw](active-directory-playbook-ingredients.md#theme) sekcji, a następnie wybierz tła zainteresowania na podstawie Twoich potrzeb.</span><span class="sxs-lookup"><span data-stu-id="58de0-108">Use the [Theme](active-directory-playbook-ingredients.md#theme) section and pick the area(s) of interest based on your needs.</span></span>  
2. <span data-ttu-id="58de0-109">Zakres fazy weryfikacji koncepcji, wybierając scenariusze, które umożliwia im dopasowanie celów biznesowych.</span><span class="sxs-lookup"><span data-stu-id="58de0-109">Scope the PoC by choosing the scenarios that align with your business goals.</span></span> <span data-ttu-id="58de0-110">Krótszą tym lepiej.</span><span class="sxs-lookup"><span data-stu-id="58de0-110">The shorter the better.</span></span> <span data-ttu-id="58de0-111">Zaleca się zrobienie go jako krótko- i zwięzła, jak to możliwe, przekazując wartość osobom zainteresowanym przy jednoczesnym zmniejszeniu złożoności do osiągnięcia go.</span><span class="sxs-lookup"><span data-stu-id="58de0-111">We recommend doing it as short and concise as possible to convey the value to the stakeholders while minimizing the complexity to realize it.</span></span>  
3. <span data-ttu-id="58de0-112">Użyj [implementacji](active-directory-playbook-implementation.md) sekcji, aby zrozumieć scenariusze, a także ich oznaczałoby dla danego środowiska.</span><span class="sxs-lookup"><span data-stu-id="58de0-112">Use the [Implementation](active-directory-playbook-implementation.md) section to understand the scenarios, and what would they mean for your environment.</span></span> <span data-ttu-id="58de0-113">W każdym scenariuszu opisano sposób skonfigurować ją (zwany [bloków konstrukcyjnych](active-directory-playbook-building-blocks.md)) i jak przechodzić w scenariuszach.</span><span class="sxs-lookup"><span data-stu-id="58de0-113">In each scenario, we describe how to set it up (what we call [Building Blocks](active-directory-playbook-building-blocks.md)), and how to navigate the scenarios.</span></span> 
4. <span data-ttu-id="58de0-114">Poszczególne bloki konstrukcyjne wyjaśniono wymagań wstępnych, a także przybliżony czas do ukończenia.</span><span class="sxs-lookup"><span data-stu-id="58de0-114">Each building block explains the pre-requisites needed, as well as an approximate time to complete.</span></span> <span data-ttu-id="58de0-115">Może to pomóc w procesie planowania.</span><span class="sxs-lookup"><span data-stu-id="58de0-115">This can help you during the planning process.</span></span> 
5. <span data-ttu-id="58de0-116">W oparciu o 1-3 powyżej, zdefiniuj [środowiska](active-directory-playbook-ingredients.md#environment) w którym ma być wykonane.</span><span class="sxs-lookup"><span data-stu-id="58de0-116">Based on 1-3 Above, define the [Environment](active-directory-playbook-ingredients.md#environment) in which to execute.</span></span> <span data-ttu-id="58de0-117">Firma Microsoft zachęca do środowiska produkcyjnego uzyskać dobrą działania środowisko dla użytkowników.</span><span class="sxs-lookup"><span data-stu-id="58de0-117">We encourage to strive for a production environment to get a good feel of the experience for your users.</span></span> 
6. <span data-ttu-id="58de0-118">Jeśli występuje konflikt wymagania, użyj tej macierzy przydatne zależnościami</span><span class="sxs-lookup"><span data-stu-id="58de0-118">When having conflicting requirements, use this helpful tradeoff matrix</span></span> 
   * <span data-ttu-id="58de0-119">Skoncentrowane na motywu przedstawiający wartości</span><span class="sxs-lookup"><span data-stu-id="58de0-119">Theme-centric showing of value</span></span>  
   * <span data-ttu-id="58de0-120">Wygładzania, aby przygotować się, aby skonfigurować i do wykonania w scenariuszach</span><span class="sxs-lookup"><span data-stu-id="58de0-120">Smoothness to prepare, to set up, and to execute the scenarios</span></span> 
   * <span data-ttu-id="58de0-121">Minimalny czas wykonywania scenariusze docelowe</span><span class="sxs-lookup"><span data-stu-id="58de0-121">Minimal time to execute the target scenarios</span></span> 
   * <span data-ttu-id="58de0-122">Jak blisko produkcji, jak to możliwe, zgodnie z ograniczeniami</span><span class="sxs-lookup"><span data-stu-id="58de0-122">As close to production as feasible within your constraints</span></span> 

>[!NOTE]
> <span data-ttu-id="58de0-123">W tym artykule pojawi się niektóre określonego działania aplikacji innych producentów i produktów wymienione jako przykłady dla wygody.</span><span class="sxs-lookup"><span data-stu-id="58de0-123">Throughout this article, you will see some specific third party applications and products mentioned as examples for convenience.</span></span> <span data-ttu-id="58de0-124">Usługi Azure AD obsługuje tysiące aplikacji w naszym [galerii aplikacji](https://azuremarketplace.microsoft.com/marketplace/apps/category/azure-active-directory-apps) których można używać na podstawie Twoich potrzeb i środowiska.</span><span class="sxs-lookup"><span data-stu-id="58de0-124">Azure AD supports thousands of applications in our [application gallery](https://azuremarketplace.microsoft.com/marketplace/apps/category/azure-active-directory-apps) that you can use based on your needs and environment.</span></span> 



[!INCLUDE [active-directory-playbook-toc](../../includes/active-directory-playbook-steps.md)]