---
title: "aaaAzure Active Directory fazy weryfikacji koncepcji podręcznika dotyczącego wprowadzenie | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 655524e9692de46e831fc68e1636e6c20d41958f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-proof-of-concept-playbook-introduction"></a><span data-ttu-id="5e231-104">Dowód koncepcji podręcznika dotyczącego usługi Azure Active Directory: wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="5e231-104">Azure Active Directory Proof of Concept Playbook: Introduction</span></span>

<span data-ttu-id="5e231-105">Ten artykuł zawiera wskazówki dotyczące możliwości tooexplore różne usługi Azure AD w koncepcji (PoC).</span><span class="sxs-lookup"><span data-stu-id="5e231-105">This article provides guidelines tooexplore different Azure AD capabilities in a Proof of Concept (PoC).</span></span> <span data-ttu-id="5e231-106">Witaj, przeznaczone odbiorcami tego dokumentu są architekci tożsamości, specjalistów IT i integratorów systemów. platforma</span><span class="sxs-lookup"><span data-stu-id="5e231-106">hello intended audience of this document is Identity Architects, IT Professionals, and System Integrators</span></span>

## <a name="how-toouse-this-playbook"></a><span data-ttu-id="5e231-107">Jak toouse tego podręcznika dotyczącego</span><span class="sxs-lookup"><span data-stu-id="5e231-107">How toouse this Playbook</span></span>

1. <span data-ttu-id="5e231-108">Użyj hello [motyw](active-directory-playbook-ingredients.md#theme) sekcji, a następnie wybierz tła hello zainteresowania na podstawie Twoich potrzeb.</span><span class="sxs-lookup"><span data-stu-id="5e231-108">Use hello [Theme](active-directory-playbook-ingredients.md#theme) section and pick hello area(s) of interest based on your needs.</span></span>  
2. <span data-ttu-id="5e231-109">Zakres hello fazy weryfikacji koncepcji, wybierając hello scenariusze, które umożliwia im dopasowanie celów biznesowych.</span><span class="sxs-lookup"><span data-stu-id="5e231-109">Scope hello PoC by choosing hello scenarios that align with your business goals.</span></span> <span data-ttu-id="5e231-110">Hello krótszą hello lepiej.</span><span class="sxs-lookup"><span data-stu-id="5e231-110">hello shorter hello better.</span></span> <span data-ttu-id="5e231-111">Zaleca się zrobienie go jako krótki i zwięzłe jako wartość hello możliwe tooconvey uczestników toohello przy jednoczesnym zmniejszeniu hello toorealize złożoności go.</span><span class="sxs-lookup"><span data-stu-id="5e231-111">We recommend doing it as short and concise as possible tooconvey hello value toohello stakeholders while minimizing hello complexity toorealize it.</span></span>  
3. <span data-ttu-id="5e231-112">Użyj hello [implementacji](active-directory-playbook-implementation.md) sekcji toounderstand hello scenariuszy i będzie ich znaczenie dla danego środowiska.</span><span class="sxs-lookup"><span data-stu-id="5e231-112">Use hello [Implementation](active-directory-playbook-implementation.md) section toounderstand hello scenarios, and what would they mean for your environment.</span></span> <span data-ttu-id="5e231-113">W każdym scenariuszu opisano sposób tooset go (zwany [bloków konstrukcyjnych](active-directory-playbook-building-blocks.md)), i jak toonavigate hello scenariuszy.</span><span class="sxs-lookup"><span data-stu-id="5e231-113">In each scenario, we describe how tooset it up (what we call [Building Blocks](active-directory-playbook-building-blocks.md)), and how toonavigate hello scenarios.</span></span> 
4. <span data-ttu-id="5e231-114">Poszczególne bloki konstrukcyjne wyjaśniono hello wymagań wstępnych, a także toocomplete przybliżony czas.</span><span class="sxs-lookup"><span data-stu-id="5e231-114">Each building block explains hello pre-requisites needed, as well as an approximate time toocomplete.</span></span> <span data-ttu-id="5e231-115">Może to ułatwić podczas hello procesu planowania.</span><span class="sxs-lookup"><span data-stu-id="5e231-115">This can help you during hello planning process.</span></span> 
5. <span data-ttu-id="5e231-116">W oparciu o 1-3 powyżej, zdefiniuj hello [środowiska](active-directory-playbook-ingredients.md#environment) w których tooexecute.</span><span class="sxs-lookup"><span data-stu-id="5e231-116">Based on 1-3 Above, define hello [Environment](active-directory-playbook-ingredients.md#environment) in which tooexecute.</span></span> <span data-ttu-id="5e231-117">Firma Microsoft zachęca toostrive dla produkcyjnego środowiska tooget dobrej działania hello środowisko dla użytkowników.</span><span class="sxs-lookup"><span data-stu-id="5e231-117">We encourage toostrive for a production environment tooget a good feel of hello experience for your users.</span></span> 
6. <span data-ttu-id="5e231-118">Jeśli występuje konflikt wymagania, użyj tej macierzy przydatne zależnościami</span><span class="sxs-lookup"><span data-stu-id="5e231-118">When having conflicting requirements, use this helpful tradeoff matrix</span></span> 
   * <span data-ttu-id="5e231-119">Skoncentrowane na motywu przedstawiający wartości</span><span class="sxs-lookup"><span data-stu-id="5e231-119">Theme-centric showing of value</span></span>  
   * <span data-ttu-id="5e231-120">Scenariusze hello tooprepare tooset się i tooexecute wygładzania</span><span class="sxs-lookup"><span data-stu-id="5e231-120">Smoothness tooprepare, tooset up, and tooexecute hello scenarios</span></span> 
   * <span data-ttu-id="5e231-121">Scenariusze docelowe hello tooexecute minimalny czas</span><span class="sxs-lookup"><span data-stu-id="5e231-121">Minimal time tooexecute hello target scenarios</span></span> 
   * <span data-ttu-id="5e231-122">Jako tooproduction Zamknij wszelkie możliwe zgodnie z ograniczeniami</span><span class="sxs-lookup"><span data-stu-id="5e231-122">As close tooproduction as feasible within your constraints</span></span> 

>[!NOTE]
> <span data-ttu-id="5e231-123">W tym artykule pojawi się niektóre określonego działania aplikacji innych producentów i produktów wymienione jako przykłady dla wygody.</span><span class="sxs-lookup"><span data-stu-id="5e231-123">Throughout this article, you will see some specific third party applications and products mentioned as examples for convenience.</span></span> <span data-ttu-id="5e231-124">Usługi Azure AD obsługuje tysiące aplikacji w naszym [galerii aplikacji](https://azuremarketplace.microsoft.com/marketplace/apps/category/azure-active-directory-apps) których można używać na podstawie Twoich potrzeb i środowiska.</span><span class="sxs-lookup"><span data-stu-id="5e231-124">Azure AD supports thousands of applications in our [application gallery](https://azuremarketplace.microsoft.com/marketplace/apps/category/azure-active-directory-apps) that you can use based on your needs and environment.</span></span> 



[!INCLUDE [active-directory-playbook-toc](../../includes/active-directory-playbook-steps.md)]