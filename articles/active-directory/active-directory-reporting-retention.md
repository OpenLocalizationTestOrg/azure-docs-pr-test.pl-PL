---
title: "Zasady przechowywania raportów w usłudze Azure Active Directory | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: ffeba8a6c32a21c75af21f948bbd6ea88dd9278c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="azure-active-directory-report-retention-policies"></a><span data-ttu-id="b5d12-103">Zasady przechowywania raportów w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b5d12-103">Azure Active Directory report retention policies</span></span>


<span data-ttu-id="b5d12-104">W tym temacie przedstawiono odpowiedzi na często zadawane pytania w połączeniu z przechowywaniem danych dla raportów innej aktywności w usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="b5d12-104">This topic provides you with answers to the most common questions in conjunction with the data retention for the different activity reports in Azure Active Directory.</span></span> 

<span data-ttu-id="b5d12-105">**Pytanie: jak możesz uzyskać zbierania danych działania uruchomiona?**</span><span class="sxs-lookup"><span data-stu-id="b5d12-105">**Q: How can you get the collection of activity data started?**</span></span>

<span data-ttu-id="b5d12-106">**ODP.:**</span><span class="sxs-lookup"><span data-stu-id="b5d12-106">**A:**</span></span>

| <span data-ttu-id="b5d12-107">Wersja usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="b5d12-107">Azure AD Edition</span></span> | <span data-ttu-id="b5d12-108">Początkowy kolekcji</span><span class="sxs-lookup"><span data-stu-id="b5d12-108">Collection Start</span></span> |
| :--              | :--   |
| <span data-ttu-id="b5d12-109">Usługa Azure AD — warstwa Premium P1</span><span class="sxs-lookup"><span data-stu-id="b5d12-109">Azure AD Premium P1</span></span> <br /> <span data-ttu-id="b5d12-110">Usługa Azure AD — warstwa Premium P2</span><span class="sxs-lookup"><span data-stu-id="b5d12-110">Azure AD Premium P2</span></span> | <span data-ttu-id="b5d12-111">Jeśli możesz przystąpić do subskrypcji</span><span class="sxs-lookup"><span data-stu-id="b5d12-111">When you sign-up for a subscription</span></span> |
| <span data-ttu-id="b5d12-112">Usługa Azure AD — warstwa Bezpłatna</span><span class="sxs-lookup"><span data-stu-id="b5d12-112">Azure AD Free</span></span> | <span data-ttu-id="b5d12-113">Przy pierwszym otwarciu [bloku usługi Azure Active Directory](https://ms.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview) lub użyj [raportowania interfejsów API](https://aka.ms/aadreports)</span><span class="sxs-lookup"><span data-stu-id="b5d12-113">The first time you open the [Azure Active Directory blade](https://ms.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview) or use the [reporting APIs](https://aka.ms/aadreports)</span></span>  |

---
<span data-ttu-id="b5d12-114">**Pytanie: kiedy dane działanie jest dostępne w portalu Azure**</span><span class="sxs-lookup"><span data-stu-id="b5d12-114">**Q: When is your activity data available in the Azure portal?**</span></span>

<span data-ttu-id="b5d12-115">**ODP.:**</span><span class="sxs-lookup"><span data-stu-id="b5d12-115">**A:**</span></span>

- <span data-ttu-id="b5d12-116">**Natychmiast** — Jeśli już pracy z raportami w klasycznym portalu Azure</span><span class="sxs-lookup"><span data-stu-id="b5d12-116">**Immediately** - If you have already been working with reports in the Azure classic portal</span></span>
- <span data-ttu-id="b5d12-117">**W ciągu 2 godzin** — Jeśli nie włączono raportowania w klasycznym portalu Azure</span><span class="sxs-lookup"><span data-stu-id="b5d12-117">**Within 2 hours** - If you haven’t turned reporting on  in the Azure classic portal</span></span>

---
<span data-ttu-id="b5d12-118">**Pytanie: jak uzyskać kolekcja sygnałów zabezpieczeń uruchomić?**</span><span class="sxs-lookup"><span data-stu-id="b5d12-118">**Q: How can you get the collection of security signals started?**</span></span>  

<span data-ttu-id="b5d12-119">**Odpowiedź:** dla sygnałów zabezpieczeń procesu zbierania rozpoczyna się, gdy należy wyrazić zgodę na Użyj Centrum ochrony tożsamości.</span><span class="sxs-lookup"><span data-stu-id="b5d12-119">**A:** For security signals, the collection process starts when you opt-in to use the Identity Protection Center.</span></span> 


---
<span data-ttu-id="b5d12-120">**Pytanie: na jak długo są zebrane dane przechowywane?**</span><span class="sxs-lookup"><span data-stu-id="b5d12-120">**Q: For how long is the collected data stored?**</span></span>

<span data-ttu-id="b5d12-121">**ODP.:**</span><span class="sxs-lookup"><span data-stu-id="b5d12-121">**A:**</span></span>

<span data-ttu-id="b5d12-122">**Raporty dotyczące działań**</span><span class="sxs-lookup"><span data-stu-id="b5d12-122">**Activity reports**</span></span>    

| <span data-ttu-id="b5d12-123">Raport</span><span class="sxs-lookup"><span data-stu-id="b5d12-123">Report</span></span>                 | <span data-ttu-id="b5d12-124">Usługa Azure AD — warstwa Bezpłatna</span><span class="sxs-lookup"><span data-stu-id="b5d12-124">Azure AD Free</span></span> | <span data-ttu-id="b5d12-125">Usługa Azure AD — warstwa Premium P1</span><span class="sxs-lookup"><span data-stu-id="b5d12-125">Azure AD Premium P1</span></span> | <span data-ttu-id="b5d12-126">Usługa Azure AD — warstwa Premium P2</span><span class="sxs-lookup"><span data-stu-id="b5d12-126">Azure AD Premium P2</span></span> |
| :--                    | :--           | :--                 | :--                 |
| <span data-ttu-id="b5d12-127">Inspekcja katalogu</span><span class="sxs-lookup"><span data-stu-id="b5d12-127">Directory Audit</span></span>        | <span data-ttu-id="b5d12-128">7 dni</span><span class="sxs-lookup"><span data-stu-id="b5d12-128">7 days</span></span>        | <span data-ttu-id="b5d12-129">30 dni</span><span class="sxs-lookup"><span data-stu-id="b5d12-129">30 days</span></span>             | <span data-ttu-id="b5d12-130">30 dni</span><span class="sxs-lookup"><span data-stu-id="b5d12-130">30 days</span></span>             |
| <span data-ttu-id="b5d12-131">Aktywność związana z logowaniem</span><span class="sxs-lookup"><span data-stu-id="b5d12-131">Sign-in Activity</span></span>       | <span data-ttu-id="b5d12-132">7 dni</span><span class="sxs-lookup"><span data-stu-id="b5d12-132">7 days</span></span>        | <span data-ttu-id="b5d12-133">30 dni</span><span class="sxs-lookup"><span data-stu-id="b5d12-133">30 days</span></span>             | <span data-ttu-id="b5d12-134">30 dni</span><span class="sxs-lookup"><span data-stu-id="b5d12-134">30 days</span></span>             |

<span data-ttu-id="b5d12-135">**Sygnały zabezpieczeń**</span><span class="sxs-lookup"><span data-stu-id="b5d12-135">**Security Signals**</span></span>

| <span data-ttu-id="b5d12-136">Raport</span><span class="sxs-lookup"><span data-stu-id="b5d12-136">Report</span></span>         | <span data-ttu-id="b5d12-137">Usługa Azure AD — warstwa Bezpłatna</span><span class="sxs-lookup"><span data-stu-id="b5d12-137">Azure AD Free</span></span> | <span data-ttu-id="b5d12-138">Usługa Azure AD — warstwa Premium P1</span><span class="sxs-lookup"><span data-stu-id="b5d12-138">Azure AD Premium P1</span></span> | <span data-ttu-id="b5d12-139">Usługa Azure AD — warstwa Premium P2</span><span class="sxs-lookup"><span data-stu-id="b5d12-139">Azure AD Premium P2</span></span> |
| :--            | :--           | :--                 | :--                 |
| <span data-ttu-id="b5d12-140">Narażeni użytkownicy</span><span class="sxs-lookup"><span data-stu-id="b5d12-140">Users at risk</span></span>  | <span data-ttu-id="b5d12-141">7 dni</span><span class="sxs-lookup"><span data-stu-id="b5d12-141">7 days</span></span>        | <span data-ttu-id="b5d12-142">30 dni</span><span class="sxs-lookup"><span data-stu-id="b5d12-142">30 days</span></span>             | <span data-ttu-id="b5d12-143">90 dni</span><span class="sxs-lookup"><span data-stu-id="b5d12-143">90 days</span></span>             |
| <span data-ttu-id="b5d12-144">Ryzykowne logowania</span><span class="sxs-lookup"><span data-stu-id="b5d12-144">Risky sign-ins</span></span> | <span data-ttu-id="b5d12-145">7 dni</span><span class="sxs-lookup"><span data-stu-id="b5d12-145">7 days</span></span>        | <span data-ttu-id="b5d12-146">30 dni</span><span class="sxs-lookup"><span data-stu-id="b5d12-146">30 days</span></span>             | <span data-ttu-id="b5d12-147">90 dni</span><span class="sxs-lookup"><span data-stu-id="b5d12-147">90 days</span></span>             |

---