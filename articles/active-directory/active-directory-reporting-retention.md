---
title: "zasady przechowywania raportów usługi Active Directory aaaAzure | Dokumentacja firmy Microsoft"
description: "Zasady przechowywania danych raportu w usłudze Azure Active Directory"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 183e53b0-0647-42e7-8abe-3e9ff424de12
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/05/2017
ms.author: dhanyahk;markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: c46a68198cb34e9c92662b2f8461010745392c04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-report-retention-policies"></a><span data-ttu-id="3c81d-103">Zasady przechowywania raportów w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3c81d-103">Azure Active Directory report retention policies</span></span>


<span data-ttu-id="3c81d-104">W tym temacie przedstawiono odpowiedzi toohello często zadawane pytania w połączeniu z przechowywaniem danych hello hello raportów innej aktywności w usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="3c81d-104">This topic provides you with answers toohello most common questions in conjunction with hello data retention for hello different activity reports in Azure Active Directory.</span></span> 

<span data-ttu-id="3c81d-105">**Pytanie: jak uzyskać hello gromadzenia danych dotyczących działalności uruchomiona?**</span><span class="sxs-lookup"><span data-stu-id="3c81d-105">**Q: How can you get hello collection of activity data started?**</span></span>

<span data-ttu-id="3c81d-106">**ODP.:**</span><span class="sxs-lookup"><span data-stu-id="3c81d-106">**A:**</span></span>

| <span data-ttu-id="3c81d-107">Wersja usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="3c81d-107">Azure AD Edition</span></span> | <span data-ttu-id="3c81d-108">Początkowy kolekcji</span><span class="sxs-lookup"><span data-stu-id="3c81d-108">Collection Start</span></span> |
| :--              | :--   |
| <span data-ttu-id="3c81d-109">Usługa Azure AD — warstwa Premium P1</span><span class="sxs-lookup"><span data-stu-id="3c81d-109">Azure AD Premium P1</span></span> <br /> <span data-ttu-id="3c81d-110">Usługa Azure AD — warstwa Premium P2</span><span class="sxs-lookup"><span data-stu-id="3c81d-110">Azure AD Premium P2</span></span> | <span data-ttu-id="3c81d-111">Jeśli możesz przystąpić do subskrypcji</span><span class="sxs-lookup"><span data-stu-id="3c81d-111">When you sign-up for a subscription</span></span> |
| <span data-ttu-id="3c81d-112">Usługa Azure AD — warstwa Bezpłatna</span><span class="sxs-lookup"><span data-stu-id="3c81d-112">Azure AD Free</span></span> | <span data-ttu-id="3c81d-113">Witaj pierwszym otwarciu hello [bloku usługi Azure Active Directory](https://ms.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview) lub użyj hello [raportowania interfejsów API](https://aka.ms/aadreports)</span><span class="sxs-lookup"><span data-stu-id="3c81d-113">hello first time you open hello [Azure Active Directory blade](https://ms.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview) or use hello [reporting APIs](https://aka.ms/aadreports)</span></span>  |

---
<span data-ttu-id="3c81d-114">**Pytanie: kiedy dane o aktywności jest dostępne w portalu Azure hello**</span><span class="sxs-lookup"><span data-stu-id="3c81d-114">**Q: When is your activity data available in hello Azure portal?**</span></span>

<span data-ttu-id="3c81d-115">**ODP.:**</span><span class="sxs-lookup"><span data-stu-id="3c81d-115">**A:**</span></span>

- <span data-ttu-id="3c81d-116">**Natychmiast** — Jeśli już pracy z raportami w hello klasycznego portalu Azure</span><span class="sxs-lookup"><span data-stu-id="3c81d-116">**Immediately** - If you have already been working with reports in hello Azure classic portal</span></span>
- <span data-ttu-id="3c81d-117">**W ciągu 2 godzin** — Jeśli nie włączono raportowania w hello klasycznego portalu Azure</span><span class="sxs-lookup"><span data-stu-id="3c81d-117">**Within 2 hours** - If you haven’t turned reporting on  in hello Azure classic portal</span></span>

---
<span data-ttu-id="3c81d-118">**Pytanie: jak uzyskać hello kolekcja sygnałów zabezpieczeń uruchomić?**</span><span class="sxs-lookup"><span data-stu-id="3c81d-118">**Q: How can you get hello collection of security signals started?**</span></span>  

<span data-ttu-id="3c81d-119">**Odpowiedź:** dla sygnałów zabezpieczeń hello proces zbierania rozpoczyna się, gdy użytkownik uczestnictwa w Centrum ochrony tożsamości hello toouse.</span><span class="sxs-lookup"><span data-stu-id="3c81d-119">**A:** For security signals, hello collection process starts when you opt-in toouse hello Identity Protection Center.</span></span> 


---
<span data-ttu-id="3c81d-120">**Pytanie: jak długo ma hello zebrane dane przechowywane?**</span><span class="sxs-lookup"><span data-stu-id="3c81d-120">**Q: For how long is hello collected data stored?**</span></span>

<span data-ttu-id="3c81d-121">**ODP.:**</span><span class="sxs-lookup"><span data-stu-id="3c81d-121">**A:**</span></span>

<span data-ttu-id="3c81d-122">**Raporty dotyczące działań**</span><span class="sxs-lookup"><span data-stu-id="3c81d-122">**Activity reports**</span></span>    

| <span data-ttu-id="3c81d-123">Raport</span><span class="sxs-lookup"><span data-stu-id="3c81d-123">Report</span></span>                 | <span data-ttu-id="3c81d-124">Usługa Azure AD — warstwa Bezpłatna</span><span class="sxs-lookup"><span data-stu-id="3c81d-124">Azure AD Free</span></span> | <span data-ttu-id="3c81d-125">Usługa Azure AD — warstwa Premium P1</span><span class="sxs-lookup"><span data-stu-id="3c81d-125">Azure AD Premium P1</span></span> | <span data-ttu-id="3c81d-126">Usługa Azure AD — warstwa Premium P2</span><span class="sxs-lookup"><span data-stu-id="3c81d-126">Azure AD Premium P2</span></span> |
| :--                    | :--           | :--                 | :--                 |
| <span data-ttu-id="3c81d-127">Inspekcja katalogu</span><span class="sxs-lookup"><span data-stu-id="3c81d-127">Directory Audit</span></span>        | <span data-ttu-id="3c81d-128">7 dni</span><span class="sxs-lookup"><span data-stu-id="3c81d-128">7 days</span></span>        | <span data-ttu-id="3c81d-129">30 dni</span><span class="sxs-lookup"><span data-stu-id="3c81d-129">30 days</span></span>             | <span data-ttu-id="3c81d-130">30 dni</span><span class="sxs-lookup"><span data-stu-id="3c81d-130">30 days</span></span>             |
| <span data-ttu-id="3c81d-131">Aktywność związana z logowaniem</span><span class="sxs-lookup"><span data-stu-id="3c81d-131">Sign-in Activity</span></span>       | <span data-ttu-id="3c81d-132">7 dni</span><span class="sxs-lookup"><span data-stu-id="3c81d-132">7 days</span></span>        | <span data-ttu-id="3c81d-133">30 dni</span><span class="sxs-lookup"><span data-stu-id="3c81d-133">30 days</span></span>             | <span data-ttu-id="3c81d-134">30 dni</span><span class="sxs-lookup"><span data-stu-id="3c81d-134">30 days</span></span>             |

<span data-ttu-id="3c81d-135">**Sygnały zabezpieczeń**</span><span class="sxs-lookup"><span data-stu-id="3c81d-135">**Security Signals**</span></span>

| <span data-ttu-id="3c81d-136">Raport</span><span class="sxs-lookup"><span data-stu-id="3c81d-136">Report</span></span>         | <span data-ttu-id="3c81d-137">Usługa Azure AD — warstwa Bezpłatna</span><span class="sxs-lookup"><span data-stu-id="3c81d-137">Azure AD Free</span></span> | <span data-ttu-id="3c81d-138">Usługa Azure AD — warstwa Premium P1</span><span class="sxs-lookup"><span data-stu-id="3c81d-138">Azure AD Premium P1</span></span> | <span data-ttu-id="3c81d-139">Usługa Azure AD — warstwa Premium P2</span><span class="sxs-lookup"><span data-stu-id="3c81d-139">Azure AD Premium P2</span></span> |
| :--            | :--           | :--                 | :--                 |
| <span data-ttu-id="3c81d-140">Narażeni użytkownicy</span><span class="sxs-lookup"><span data-stu-id="3c81d-140">Users at risk</span></span>  | <span data-ttu-id="3c81d-141">7 dni</span><span class="sxs-lookup"><span data-stu-id="3c81d-141">7 days</span></span>        | <span data-ttu-id="3c81d-142">30 dni</span><span class="sxs-lookup"><span data-stu-id="3c81d-142">30 days</span></span>             | <span data-ttu-id="3c81d-143">90 dni</span><span class="sxs-lookup"><span data-stu-id="3c81d-143">90 days</span></span>             |
| <span data-ttu-id="3c81d-144">Ryzykowne logowania</span><span class="sxs-lookup"><span data-stu-id="3c81d-144">Risky sign-ins</span></span> | <span data-ttu-id="3c81d-145">7 dni</span><span class="sxs-lookup"><span data-stu-id="3c81d-145">7 days</span></span>        | <span data-ttu-id="3c81d-146">30 dni</span><span class="sxs-lookup"><span data-stu-id="3c81d-146">30 days</span></span>             | <span data-ttu-id="3c81d-147">90 dni</span><span class="sxs-lookup"><span data-stu-id="3c81d-147">90 days</span></span>             |

---