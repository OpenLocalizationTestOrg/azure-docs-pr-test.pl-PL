---
title: "Włącz inspekcję i wykrywania zagrożeń na serwerach SQL w Centrum zabezpieczeń Azure | Dokumentacja firmy Microsoft"
description: "Ten dokument przedstawia sposób wykonania zalecenia Centrum zabezpieczeń Azure ** Włączanie inspekcji i wykrywanie zagrożeń na serwerach SQL **."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 042fca4d-7dab-4172-8614-e8c21ccb4960
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: terrylan
ms.openlocfilehash: 660b537aef8d175a478ff93d60b8391d55fc92ad
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="enable-auditing-and-threat-detection-on-sql-servers-in-azure-security-center"></a><span data-ttu-id="6d8b3-103">Włącz inspekcję i wykrywania zagrożeń na serwerach SQL w Centrum zabezpieczeń Azure</span><span class="sxs-lookup"><span data-stu-id="6d8b3-103">Enable auditing and threat detection on SQL servers in Azure Security Center</span></span>
<span data-ttu-id="6d8b3-104">Centrum zabezpieczeń Azure zostanie zaleca włączenie inspekcji i wykrywanie zagrożeń dla wszystkich baz danych na serwerach Azure SQL, jeśli inspekcji nie jest jeszcze włączone.</span><span class="sxs-lookup"><span data-stu-id="6d8b3-104">Azure Security Center will recommend that you turn on auditing and threat detection for all databases on your Azure SQL servers if auditing is not already enabled.</span></span> <span data-ttu-id="6d8b3-105">Inspekcja i jakie wykrywania pomaga zachować zgodność z przepisami, analizować aktywność bazy danych oraz uzyskać wgląd w odchylenia i anomalie, które mogą oznaczać problemy biznesowe lub podejrzane naruszenia zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="6d8b3-105">Auditing and threat detection can help you maintain regulatory compliance, understand database activity, and gain insight into discrepancies and anomalies that could indicate business concerns or suspected security violations.</span></span>

<span data-ttu-id="6d8b3-106">Po włączeniu inspekcji można skonfigurować ustawienia wykrywanie zagrożeń i wiadomości e-mail, aby otrzymywać alerty zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="6d8b3-106">Once you’ve turned on auditing you can configure Threat Detection settings and emails to receive security alerts.</span></span> <span data-ttu-id="6d8b3-107">Wykrywanie zagrożeń wykrywa nietypowe działania bazy danych wskazują możliwe zagrożenia bezpieczeństwa w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="6d8b3-107">Threat Detection detects anomalous database activities indicating potential security threats to the database.</span></span> <span data-ttu-id="6d8b3-108">Umożliwia to wykrywanie i odpowiadanie na potencjalne zagrożenia w miarę ich występowania.</span><span class="sxs-lookup"><span data-stu-id="6d8b3-108">This enables you to detect and respond to potential threats as they occur.</span></span>

<span data-ttu-id="6d8b3-109">To zalecenie stosuje się do usługi Azure SQL. nie ma wśród nich programu SQL Server uruchomionego na maszynach wirtualnych w usługi infrastruktury platformy Azure (IaaS platformy Azure).</span><span class="sxs-lookup"><span data-stu-id="6d8b3-109">This recommendation applies to the Azure SQL service only; it doesn’t include SQL Server running on your virtual machines in Azure Infrastructure Services (Azure IaaS).</span></span>

> [!NOTE]
> <span data-ttu-id="6d8b3-110">Informacje na temat usługi przedstawiono w tym dokumencie za pomocą przykładowego wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="6d8b3-110">This document introduces the service by using an example deployment.</span></span>  <span data-ttu-id="6d8b3-111">Nie jest to przewodnik krok po kroku.</span><span class="sxs-lookup"><span data-stu-id="6d8b3-111">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-the-recommendation"></a><span data-ttu-id="6d8b3-112">Wykonania zalecenia</span><span class="sxs-lookup"><span data-stu-id="6d8b3-112">Implement the recommendation</span></span>
1. <span data-ttu-id="6d8b3-113">W **zalecenia** bloku, wybierz opcję **Włączanie inspekcji i wykrywanie zagrożeń na serwerach SQL**.</span><span class="sxs-lookup"><span data-stu-id="6d8b3-113">In the **Recommendations** blade, select **Enable Auditing & Threat detection on SQL servers**.</span></span>  <span data-ttu-id="6d8b3-114">Spowoduje to otwarcie **Włączanie inspekcji i wykrywanie zagrożeń na serwerach SQL** bloku.</span><span class="sxs-lookup"><span data-stu-id="6d8b3-114">This opens the **Enable Auditing & Threat detection on SQL servers** blade.</span></span>

   ![Włączanie inspekcji dla serwerów SQL][1]
2. <span data-ttu-id="6d8b3-116">Wybierz serwer SQL, Włącz inspekcję i wykrywania zagrożeń.</span><span class="sxs-lookup"><span data-stu-id="6d8b3-116">Select a SQL server to enable auditing and threat detection on.</span></span> <span data-ttu-id="6d8b3-117">Spowoduje to otwarcie **Inspekcja i wykrywanie zagrożeń** bloku.</span><span class="sxs-lookup"><span data-stu-id="6d8b3-117">This opens the **Auditing & Threat Detection** blade.</span></span>

3. <span data-ttu-id="6d8b3-118">Na **Inspekcja i wykrywanie zagrożeń** bloku, wybierz opcję **ON** w obszarze **inspekcji**.</span><span class="sxs-lookup"><span data-stu-id="6d8b3-118">On the **Auditing & Threat Detection** blade, select **ON** under **Auditing**.</span></span>

   ![Włączanie ustawień inspekcji][2]
4. <span data-ttu-id="6d8b3-120">Postępuj zgodnie z instrukcjami [inspekcja bazy danych SQL w portalu Azure](../sql-database/sql-database-auditing-portal.md) skonfigurować Magazyn przechowywania dzienników inspekcji.</span><span class="sxs-lookup"><span data-stu-id="6d8b3-120">Follow the steps in [SQL database auditing in the Azure portal](../sql-database/sql-database-auditing-portal.md) to configure storage where your audit logs will be stored.</span></span> <span data-ttu-id="6d8b3-121">Konto magazynu subskrypcji na potrzeby zbierania danych jest domyślne konto magazynu.</span><span class="sxs-lookup"><span data-stu-id="6d8b3-121">The subscription's storage account for data collection is the default storage account.</span></span>
5. <span data-ttu-id="6d8b3-122">Postępuj zgodnie z instrukcjami [wprowadzenie wykrywanie zagrożeń bazy danych SQL](../sql-database/sql-database-threat-detection.md) włączać i konfigurować wykrywanie zagrożeń i skonfigurować listę wiadomości e-mail, które będą wysyłane alerty zabezpieczeń po wykryciu nietypowych działań.</span><span class="sxs-lookup"><span data-stu-id="6d8b3-122">Follow the steps in [Get started with SQL Database Threat Detection](../sql-database/sql-database-threat-detection.md) to turn on and configure Threat Detection and to configure the list of emails that will receive security alerts upon detection of anomalous activities.</span></span>

## <a name="see-also"></a><span data-ttu-id="6d8b3-123">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="6d8b3-123">See also</span></span>
<span data-ttu-id="6d8b3-124">W tym artykule przedstawiono sposób wdrożenia Centrum zabezpieczeń zalecenie "włączania inspekcji i wykrywania zagrożeń na serwerach SQL."</span><span class="sxs-lookup"><span data-stu-id="6d8b3-124">This article showed you how to implement the Security Center recommendation "Enable auditing and threat detection on SQL servers."</span></span> <span data-ttu-id="6d8b3-125">Aby dowiedzieć się więcej na temat zabezpieczania bazy danych SQL, zobacz następujące tematy:</span><span class="sxs-lookup"><span data-stu-id="6d8b3-125">To learn more about securing your SQL database, see the following:</span></span>

* [<span data-ttu-id="6d8b3-126">Zabezpieczanie bazy danych SQL</span><span class="sxs-lookup"><span data-stu-id="6d8b3-126">Securing your SQL Database</span></span>](../sql-database/sql-database-security-overview.md)

<span data-ttu-id="6d8b3-127">Aby dowiedzieć się więcej na temat Centrum zabezpieczeń, zobacz następujące artykuły:</span><span class="sxs-lookup"><span data-stu-id="6d8b3-127">To learn more about Security Center, see the following:</span></span>

* <span data-ttu-id="6d8b3-128">[Ustawianie zasad zabezpieczeń w usłudze Azure Security Center](security-center-policies.md) — informacje na temat konfigurowania zasad zabezpieczeń dla subskrypcji i grup zasobów na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="6d8b3-128">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how to configure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="6d8b3-129">[Zarządzanie zaleceniami dotyczącymi zabezpieczeń w Centrum zabezpieczeń Azure](security-center-recommendations.md) — Dowiedz się, w jaki sposób zalecenia ułatwiają ochronę zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="6d8b3-129">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="6d8b3-130">[Monitorowanie kondycji zabezpieczeń w Centrum zabezpieczeń Azure](security-center-monitoring.md) — informacje o sposobie monitorowania kondycji zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="6d8b3-130">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="6d8b3-131">[Reagowanie na alerty zabezpieczeń i zarządzanie nimi w usłudze Azure Security Center](security-center-managing-and-responding-alerts.md) — informacje na temat reagowania na alerty zabezpieczeń i zarządzania nimi.</span><span class="sxs-lookup"><span data-stu-id="6d8b3-131">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="6d8b3-132">[Monitorowanie rozwiązań partnerskich w Centrum zabezpieczeń Azure](security-center-partner-solutions.md) — informacje na temat monitorowania stanu kondycji rozwiązań partnerskich.</span><span class="sxs-lookup"><span data-stu-id="6d8b3-132">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how to monitor the health status of your partner solutions.</span></span>
* <span data-ttu-id="6d8b3-133">[Azure Security Center — często zadawane pytania](security-center-faq.md) — odpowiedzi na często zadawane pytania dotyczące korzystania z usługi.</span><span class="sxs-lookup"><span data-stu-id="6d8b3-133">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="6d8b3-134">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) — Uzyskaj najnowsze informacje zabezpieczeń platformy Azure i informacje.</span><span class="sxs-lookup"><span data-stu-id="6d8b3-134">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Get the latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-enable-auditing-on-sql-server/enable-auditing-on-sql-servers.png
[2]: ./media/security-center-enable-auditing-on-sql-server/auditing-settings-blade.png
