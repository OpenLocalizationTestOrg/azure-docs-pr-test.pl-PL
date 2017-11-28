---
title: "Rozwiązywanie problemów: Brak danych w dzienniku aktywności usługi Azure Active Directory | Microsoft Docs"
description: "Lista raportów dostępnych w ramach usługi Azure Active Directory"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 7cbe4337-bb77-4ee0-b254-3e368be06db7
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/15/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 47617f8f727027de113a0f503308c8accc58859e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="i-cant-find-some-actions-that-i-performed-in-the-azure-active-directory-activity-log"></a><span data-ttu-id="36c87-103">W dzienniku aktywności usługi Azure Active Directory nie można znaleźć niektórych wykonywanych akcji</span><span class="sxs-lookup"><span data-stu-id="36c87-103">I can’t find some actions that I performed in the Azure Active Directory activity log</span></span>


## <a name="symptoms"></a><span data-ttu-id="36c87-104">Objawy</span><span class="sxs-lookup"><span data-stu-id="36c87-104">Symptoms</span></span>

<span data-ttu-id="36c87-105">W witrynie Azure Portal wykonano pewne akcje, które powinny zostać odzwierciedlone w dziennikach inspekcji w bloku `Activity logs > Audit Logs`, ale nie można ich znaleźć.</span><span class="sxs-lookup"><span data-stu-id="36c87-105">I performed some actions in the Azure portal and expected to see the audit logs for those actions in the `Activity logs > Audit Logs` blade, but I can’t find them.</span></span>

 ![Raportowanie](./media/active-directory-reporting-troubleshoot-missing-audit-data/01.png)
 

## <a name="cause"></a><span data-ttu-id="36c87-107">Przyczyna</span><span class="sxs-lookup"><span data-stu-id="36c87-107">Cause</span></span>

<span data-ttu-id="36c87-108">Akcje nie pojawiają się natychmiast w dzienniku inspekcji aktywności.</span><span class="sxs-lookup"><span data-stu-id="36c87-108">Actions don’t appear immediately in the Activity Audit log.</span></span> <span data-ttu-id="36c87-109">Dzienniki inspekcji pojawiają się w portalu dopiero po pewnym czasie (od 15 minut do godziny) od momentu wykonania operacji.</span><span class="sxs-lookup"><span data-stu-id="36c87-109">It can take anywhere from 15 minutes to an hour to see the audit logs in the portal from the time the operation is performed.</span></span>

## <a name="resolution"></a><span data-ttu-id="36c87-110">Rozwiązanie</span><span class="sxs-lookup"><span data-stu-id="36c87-110">Resolution</span></span>

<span data-ttu-id="36c87-111">Poczekaj od 15 minut do godziny i sprawdź, czy akcje pojawią się w dzienniku.</span><span class="sxs-lookup"><span data-stu-id="36c87-111">Wait for 15 minutes to an hour and see if the actions appear in the log.</span></span> <span data-ttu-id="36c87-112">Jeśli nadal nie są one wyświetlane, zgłoś do nas bilet pomocy technicznej, abyśmy mogli przeanalizować tę sytuację.</span><span class="sxs-lookup"><span data-stu-id="36c87-112">If you still don’t see them, please raise a support ticket with us and we will look into it.</span></span>


## <a name="next-steps"></a><span data-ttu-id="36c87-113">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="36c87-113">Next steps</span></span>
<span data-ttu-id="36c87-114">Zobacz temat[Azure Active Directory reporting FAQ](active-directory-reporting-faq.md) (Często zadawane pytania dotyczące raportowania usługi Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="36c87-114">See the [Azure Active Directory reporting FAQ](active-directory-reporting-faq.md).</span></span>

