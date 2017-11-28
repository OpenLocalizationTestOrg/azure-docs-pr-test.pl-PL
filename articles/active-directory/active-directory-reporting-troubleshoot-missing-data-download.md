---
title: "Rozwiązywanie problemów: Brak danych w hello pobrać Dzienniki aktywności w usłudze Azure Active Directory | Dokumentacja firmy Microsoft"
description: "Udostępnia rozpoznawanie danych toomissing w pobranych Dzienniki aktywności usługi Azure Active Directory."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: ffce7eb1-99da-4ea7-9c4d-2322b755c8ce
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/15/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 027b70e6efc570f81d3c836f50ee52aaa89be71a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="i-cant-find-any-data-in-hello-azure-active-directory-activity-logs-i-have-downloaded"></a><span data-ttu-id="02312-103">Nie można znaleźć żadnych danych w dziennikach hello działania usługi Azure Active Directory, który został pobrany</span><span class="sxs-lookup"><span data-stu-id="02312-103">I can’t find any data in hello Azure Active Directory activity logs I have downloaded</span></span>


## <a name="symptoms"></a><span data-ttu-id="02312-104">Objawy</span><span class="sxs-lookup"><span data-stu-id="02312-104">Symptoms</span></span>

<span data-ttu-id="02312-105">Pobrany Dzienniki aktywności hello (inspekcji lub logowania) i wszystkie rekordy hello nie jest widoczny dla czasu hello, które zostało określone.</span><span class="sxs-lookup"><span data-stu-id="02312-105">I downloaded hello activity logs (audit or sign-ins) and I don’t see all hello records for hello time I chose.</span></span> <span data-ttu-id="02312-106">Dlaczego?</span><span class="sxs-lookup"><span data-stu-id="02312-106">Why?</span></span> 

 ![Raportowanie](./media/active-directory-reporting-troubleshoot-missing-data-download/01.png)
 

## <a name="cause"></a><span data-ttu-id="02312-108">Przyczyna</span><span class="sxs-lookup"><span data-stu-id="02312-108">Cause</span></span>

<span data-ttu-id="02312-109">Podczas pobierania dzienników aktywności w portalu Azure hello jest ograniczona rekordy too120K skali hello posortowane przez większość ostatnie.</span><span class="sxs-lookup"><span data-stu-id="02312-109">When you download activity logs in hello Azure portal, we limit hello scale too120K records, sorted by most recent.</span></span> 

## <a name="resolution"></a><span data-ttu-id="02312-110">Rozwiązanie</span><span class="sxs-lookup"><span data-stu-id="02312-110">Resolution</span></span>

<span data-ttu-id="02312-111">Można wykorzystać [API Azure AD raportowania](active-directory-reporting-api-getting-started.md) toofetch tooa miliony rekordów na dowolnym etapie.</span><span class="sxs-lookup"><span data-stu-id="02312-111">You can leverage [Azure AD Reporting APIs](active-directory-reporting-api-getting-started.md) toofetch up tooa million records at any given point.</span></span> <span data-ttu-id="02312-112">Nasze podejście zalecane jest toorun skryptu zgodnie z harmonogramem wywołującą hello raportowania interfejsów API toofetch rejestruje w sposób przyrostowy w danym okresie czasu (np., codziennie lub co tydzień).</span><span class="sxs-lookup"><span data-stu-id="02312-112">Our recommended approach is toorun a script on a scheduled basis that calls hello reporting APIs toofetch records in an incremental fashion over a period of time (e.g., daily or weekly).</span></span>

## <a name="next-steps"></a><span data-ttu-id="02312-113">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="02312-113">Next steps</span></span>
<span data-ttu-id="02312-114">Zobacz hello [raportowania często zadawane pytania dotyczące usługi Azure Active Directory](active-directory-reporting-faq.md).</span><span class="sxs-lookup"><span data-stu-id="02312-114">See hello [Azure Active Directory reporting FAQ](active-directory-reporting-faq.md).</span></span>

