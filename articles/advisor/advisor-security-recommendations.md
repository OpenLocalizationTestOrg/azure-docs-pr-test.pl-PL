---
title: "aaaAzure zalecenia doradcy w zakresie zabezpieczeń | Dokumentacja firmy Microsoft"
description: "Użyj doradcy Azure toohelp zwiększyć poziom bezpieczeństwa hello Azure wdrożeń."
services: advisor
documentationcenter: NA
author: kumudd
manager: carmonm
editor: 
ms.assetid: 
ms.service: advisor
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 11/16/2016
ms.author: kumud
ms.openlocfilehash: e01ac29eb6e02bff0b1e846e320e7c36f85c7343
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="advisor-security-recommendations"></a><span data-ttu-id="387b0-103">Zalecenia doradcy w zakresie zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="387b0-103">Advisor Security recommendations</span></span>

<span data-ttu-id="387b0-104">Klasyfikator Azure zapewnia spójne, skonsolidowanego widoku zaleceń dla wszystkich zasobów na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="387b0-104">Azure Advisor provides you with a consistent, consolidated view of recommendations for all your Azure resources.</span></span> <span data-ttu-id="387b0-105">Umożliwia integrację z Centrum zabezpieczeń Azure toobring możesz zalecenia dotyczące zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="387b0-105">It integrates with Azure Security Center toobring you security recommendations.</span></span> <span data-ttu-id="387b0-106">Zalecenia dotyczące zabezpieczeń można uzyskać z hello **zabezpieczeń** kartę na pulpicie nawigacyjnym usługi Advisor hello.</span><span class="sxs-lookup"><span data-stu-id="387b0-106">You can get security recommendations from hello **Security** tab on hello Advisor dashboard.</span></span>

![przycisk zabezpieczeń usługi Advisor Hello](./media/advisor-security-recommendations/advisor-security-tab.png)

<span data-ttu-id="387b0-108">Centrum zabezpieczeń ułatwia zapobieganie, wykrywania i odpowie toothreats lepszy wgląd w i kontroli nad hello zabezpieczeń zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="387b0-108">Security Center helps you prevent, detect, and respond toothreats with increased visibility into and control over hello security of your Azure resources.</span></span> <span data-ttu-id="387b0-109">Okresowo analizuje ona hello stan zabezpieczeń zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="387b0-109">It periodically analyzes hello security state of your Azure resources.</span></span> <span data-ttu-id="387b0-110">Po znalezieniu potencjalnych luk w zabezpieczeniach usługa Security Center tworzy odpowiednie zalecenia.</span><span class="sxs-lookup"><span data-stu-id="387b0-110">When Security Center identifies potential security vulnerabilities, it creates recommendations.</span></span> <span data-ttu-id="387b0-111">zalecenia Hello pomocne hello proces konfigurowania hello formantów, które są potrzebne.</span><span class="sxs-lookup"><span data-stu-id="387b0-111">hello recommendations guide you through hello process of configuring hello controls you need.</span></span> 

![Karta Zabezpieczenia Advisor Hello](./media/advisor-security-recommendations/advisor-security-recommendations.png)

<span data-ttu-id="387b0-113">Aby uzyskać więcej informacji o zalecenia dotyczące zabezpieczeń, zobacz [Zarządzanie zaleceniami dotyczącymi zabezpieczeń w Centrum zabezpieczeń Azure](https://azure.microsoft.com/en-us/documentation/articles/security-center-recommendations/).</span><span class="sxs-lookup"><span data-stu-id="387b0-113">For more information about security recommendations, see [Managing security recommendations in Azure Security Center](https://azure.microsoft.com/en-us/documentation/articles/security-center-recommendations/).</span></span>

## <a name="how-tooaccess-security-recommendations-in-azure-advisor"></a><span data-ttu-id="387b0-114">Jak tooaccess zalecenia dotyczące zabezpieczeń w programie Azure Advisor</span><span class="sxs-lookup"><span data-stu-id="387b0-114">How tooaccess Security recommendations in Azure Advisor</span></span>

1. <span data-ttu-id="387b0-115">Zaloguj się toohello [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="387b0-115">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="387b0-116">W okienku po lewej stronie powitania kliknij **więcej usług**.</span><span class="sxs-lookup"><span data-stu-id="387b0-116">In hello left pane, click **More services**.</span></span>

3. <span data-ttu-id="387b0-117">W hello usługa okienku menu, w obszarze **monitorowanie i zarządzanie**, kliknij przycisk **Azure Advisor**.</span><span class="sxs-lookup"><span data-stu-id="387b0-117">In hello service menu pane, under **Monitoring and Management**, click **Azure Advisor**.</span></span>  
 <span data-ttu-id="387b0-118">pulpit nawigacyjny usługi Advisor Hello jest wyświetlany.</span><span class="sxs-lookup"><span data-stu-id="387b0-118">hello Advisor dashboard is displayed.</span></span>

4. <span data-ttu-id="387b0-119">Na pulpicie nawigacyjnym usługi Advisor hello, kliknij przycisk hello **zabezpieczeń** kartę.</span><span class="sxs-lookup"><span data-stu-id="387b0-119">On hello Advisor dashboard, click hello **Security** tab.</span></span>

5. <span data-ttu-id="387b0-120">Wybierz subskrypcję hello, dla którego chcesz tooreceive zalecenia, a następnie kliknij **Uzyskaj zalecenia**.</span><span class="sxs-lookup"><span data-stu-id="387b0-120">Select hello subscription for which you want tooreceive recommendations, and then click **Get recommendations**.</span></span>

> [!NOTE]
> <span data-ttu-id="387b0-121">tooaccess zalecenia doradcy w zakresie, należy najpierw *zarejestrować swoją subskrypcję* usłudze Advisor.</span><span class="sxs-lookup"><span data-stu-id="387b0-121">tooaccess Advisor recommendations, you must first *register your subscription* with Advisor.</span></span> <span data-ttu-id="387b0-122">Subskrypcja jest zarejestrowana przy *właściciela subskrypcji* powoduje uruchomienie hello Advisor hello pulpitu nawigacyjnego i klika przycisk **Uzyskaj zalecenia** przycisku.</span><span class="sxs-lookup"><span data-stu-id="387b0-122">A subscription is registered when a *subscription Owner* launches hello Advisor dashboard and clicks hello **Get recommendations** button.</span></span> <span data-ttu-id="387b0-123">Jest to *jednorazowa operacja*.</span><span class="sxs-lookup"><span data-stu-id="387b0-123">This is a *one-time operation*.</span></span> <span data-ttu-id="387b0-124">Po zarejestrowaniu subskrypcji hello są dostępne zalecenia doradcy w zakresie jako *właściciela*, *współautora*, lub *czytnika* subskrypcji, grupy zasobów, lub określonego zasobu.</span><span class="sxs-lookup"><span data-stu-id="387b0-124">After hello subscription is registered, you can access Advisor recommendations as *Owner*, *Contributor*, or *Reader* for a subscription, a resource group, or a specific resource.</span></span>

## <a name="next-steps"></a><span data-ttu-id="387b0-125">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="387b0-125">Next steps</span></span>

<span data-ttu-id="387b0-126">toolearn więcej informacji na temat zalecenia doradcy w zakresie, zobacz:</span><span class="sxs-lookup"><span data-stu-id="387b0-126">toolearn more about Advisor recommendations, see:</span></span>
* [<span data-ttu-id="387b0-127">Wprowadzenie tooAdvisor</span><span class="sxs-lookup"><span data-stu-id="387b0-127">Introduction tooAdvisor</span></span>](advisor-overview.md)
* [<span data-ttu-id="387b0-128">Wprowadzenie do usługi Advisor</span><span class="sxs-lookup"><span data-stu-id="387b0-128">Get started with Advisor</span></span>](advisor-get-started.md)
* [<span data-ttu-id="387b0-129">Zalecenia doradcy w zakresie koszt</span><span class="sxs-lookup"><span data-stu-id="387b0-129">Advisor Cost recommendations</span></span>](advisor-performance-recommendations.md)
* [<span data-ttu-id="387b0-130">Zalecenia doradcy w zakresie wydajności</span><span class="sxs-lookup"><span data-stu-id="387b0-130">Advisor Performance recommendations</span></span>](advisor-performance-recommendations.md)
* [<span data-ttu-id="387b0-131">Zalecenia doradcy w zakresie wysokiej dostępności</span><span class="sxs-lookup"><span data-stu-id="387b0-131">Advisor High Availability recommendations</span></span>](advisor-high-availability-recommendations.md)


 
