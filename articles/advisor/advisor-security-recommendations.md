---
title: "Zalecenia dotyczące zabezpieczeń Azure Advisor | Dokumentacja firmy Microsoft"
description: "Za pomocą usługi Azure doradcy poprawić zabezpieczenia wdrożeń platformy Azure."
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
ms.openlocfilehash: 53be05593c3733ccb27979a3a026414013125779
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="advisor-security-recommendations"></a><span data-ttu-id="af825-103">Zalecenia doradcy w zakresie zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="af825-103">Advisor Security recommendations</span></span>

<span data-ttu-id="af825-104">Klasyfikator Azure zapewnia spójne, skonsolidowanego widoku zaleceń dla wszystkich zasobów na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="af825-104">Azure Advisor provides you with a consistent, consolidated view of recommendations for all your Azure resources.</span></span> <span data-ttu-id="af825-105">Umożliwia integrację z Centrum zabezpieczeń Azure, aby wyświetlić zalecenia dotyczące zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="af825-105">It integrates with Azure Security Center to bring you security recommendations.</span></span> <span data-ttu-id="af825-106">Możesz uzyskać zalecenia dotyczące zabezpieczeń wynikające z **zabezpieczeń** na pulpicie nawigacyjnym usługi Advisor.</span><span class="sxs-lookup"><span data-stu-id="af825-106">You can get security recommendations from the **Security** tab on the Advisor dashboard.</span></span>

![Przycisk zabezpieczeń usługi Advisor](./media/advisor-security-recommendations/advisor-security-tab.png)

<span data-ttu-id="af825-108">Usługa Security Center ułatwia zapobieganie zagrożeniom, ich wykrywanie i reagowanie na nie, a przy tym zapewnia lepszy wgląd i większą kontrolę w zakresie bezpieczeństwa zasobów na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="af825-108">Security Center helps you prevent, detect, and respond to threats with increased visibility into and control over the security of your Azure resources.</span></span> <span data-ttu-id="af825-109">Ją okresowo analizuje stan zabezpieczeń zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="af825-109">It periodically analyzes the security state of your Azure resources.</span></span> <span data-ttu-id="af825-110">Po znalezieniu potencjalnych luk w zabezpieczeniach usługa Security Center tworzy odpowiednie zalecenia.</span><span class="sxs-lookup"><span data-stu-id="af825-110">When Security Center identifies potential security vulnerabilities, it creates recommendations.</span></span> <span data-ttu-id="af825-111">Zalecenia ułatwiają konfigurowanie kontrolek, które są potrzebne.</span><span class="sxs-lookup"><span data-stu-id="af825-111">The recommendations guide you through the process of configuring the controls you need.</span></span> 

![Karta Zabezpieczenia usługi Advisor](./media/advisor-security-recommendations/advisor-security-recommendations.png)

<span data-ttu-id="af825-113">Aby uzyskać więcej informacji o zalecenia dotyczące zabezpieczeń, zobacz [Zarządzanie zaleceniami dotyczącymi zabezpieczeń w Centrum zabezpieczeń Azure](https://azure.microsoft.com/en-us/documentation/articles/security-center-recommendations/).</span><span class="sxs-lookup"><span data-stu-id="af825-113">For more information about security recommendations, see [Managing security recommendations in Azure Security Center](https://azure.microsoft.com/en-us/documentation/articles/security-center-recommendations/).</span></span>

## <a name="how-to-access-security-recommendations-in-azure-advisor"></a><span data-ttu-id="af825-114">Jak uzyskać dostęp zalecenia dotyczące zabezpieczeń w programie Azure Advisor</span><span class="sxs-lookup"><span data-stu-id="af825-114">How to access Security recommendations in Azure Advisor</span></span>

1. <span data-ttu-id="af825-115">Zaloguj się w witrynie [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="af825-115">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="af825-116">W okienku po lewej stronie kliknij **więcej usług**.</span><span class="sxs-lookup"><span data-stu-id="af825-116">In the left pane, click **More services**.</span></span>

3. <span data-ttu-id="af825-117">W okienku usługi menu w obszarze **monitorowanie i zarządzanie**, kliknij przycisk **Azure Advisor**.</span><span class="sxs-lookup"><span data-stu-id="af825-117">In the service menu pane, under **Monitoring and Management**, click **Azure Advisor**.</span></span>  
 <span data-ttu-id="af825-118">Zostanie wyświetlony pulpit nawigacyjny usługi Advisor.</span><span class="sxs-lookup"><span data-stu-id="af825-118">The Advisor dashboard is displayed.</span></span>

4. <span data-ttu-id="af825-119">Na pulpicie nawigacyjnym usługi Advisor, kliknij przycisk **zabezpieczeń** kartę.</span><span class="sxs-lookup"><span data-stu-id="af825-119">On the Advisor dashboard, click the **Security** tab.</span></span>

5. <span data-ttu-id="af825-120">Wybierz subskrypcję, dla którego chcesz otrzymywać zalecenia, a następnie kliknij przycisk **Uzyskaj zalecenia**.</span><span class="sxs-lookup"><span data-stu-id="af825-120">Select the subscription for which you want to receive recommendations, and then click **Get recommendations**.</span></span>

> [!NOTE]
> <span data-ttu-id="af825-121">Aby uzyskać dostęp do zalecenia doradcy w zakresie, należy najpierw *zarejestrować swoją subskrypcję* usłudze Advisor.</span><span class="sxs-lookup"><span data-stu-id="af825-121">To access Advisor recommendations, you must first *register your subscription* with Advisor.</span></span> <span data-ttu-id="af825-122">Subskrypcja jest zarejestrowana przy *właściciela subskrypcji* uruchamia pulpitu nawigacyjnego usługi Advisor i klika pozycję **Uzyskaj zalecenia** przycisk.</span><span class="sxs-lookup"><span data-stu-id="af825-122">A subscription is registered when a *subscription Owner* launches the Advisor dashboard and clicks the **Get recommendations** button.</span></span> <span data-ttu-id="af825-123">Jest to *jednorazowa operacja*.</span><span class="sxs-lookup"><span data-stu-id="af825-123">This is a *one-time operation*.</span></span> <span data-ttu-id="af825-124">Po zarejestrowaniu subskrypcji są dostępne zalecenia doradcy w zakresie jako *właściciela*, *współautora*, lub *czytnika* dla określonego zasobu, grupy zasobów lub subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="af825-124">After the subscription is registered, you can access Advisor recommendations as *Owner*, *Contributor*, or *Reader* for a subscription, a resource group, or a specific resource.</span></span>

## <a name="next-steps"></a><span data-ttu-id="af825-125">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="af825-125">Next steps</span></span>

<span data-ttu-id="af825-126">Aby dowiedzieć się więcej na temat zalecenia doradcy w zakresie, zobacz:</span><span class="sxs-lookup"><span data-stu-id="af825-126">To learn more about Advisor recommendations, see:</span></span>
* [<span data-ttu-id="af825-127">Wprowadzenie do usługi Advisor</span><span class="sxs-lookup"><span data-stu-id="af825-127">Introduction to Advisor</span></span>](advisor-overview.md)
* [<span data-ttu-id="af825-128">Wprowadzenie do usługi Advisor</span><span class="sxs-lookup"><span data-stu-id="af825-128">Get started with Advisor</span></span>](advisor-get-started.md)
* [<span data-ttu-id="af825-129">Zalecenia doradcy w zakresie koszt</span><span class="sxs-lookup"><span data-stu-id="af825-129">Advisor Cost recommendations</span></span>](advisor-performance-recommendations.md)
* [<span data-ttu-id="af825-130">Zalecenia doradcy w zakresie wydajności</span><span class="sxs-lookup"><span data-stu-id="af825-130">Advisor Performance recommendations</span></span>](advisor-performance-recommendations.md)
* [<span data-ttu-id="af825-131">Zalecenia doradcy w zakresie wysokiej dostępności</span><span class="sxs-lookup"><span data-stu-id="af825-131">Advisor High Availability recommendations</span></span>](advisor-high-availability-recommendations.md)


 
