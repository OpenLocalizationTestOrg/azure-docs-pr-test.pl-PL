---
title: "aaaEnable inspekcji i wykrywania zagrożeń na serwerach SQL w Centrum zabezpieczeń Azure | Dokumentacja firmy Microsoft"
description: "Ten dokument przedstawia sposób tooimplement hello zalecenia Centrum zabezpieczeń Azure ** Włączanie inspekcji i wykrywanie zagrożeń na serwerach SQL **."
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
ms.openlocfilehash: b082c48cdbc386f14e677f4e13a7f306f37fd0e8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="enable-auditing-and-threat-detection-on-sql-servers-in-azure-security-center"></a><span data-ttu-id="4ed4a-103">Włącz inspekcję i wykrywania zagrożeń na serwerach SQL w Centrum zabezpieczeń Azure</span><span class="sxs-lookup"><span data-stu-id="4ed4a-103">Enable auditing and threat detection on SQL servers in Azure Security Center</span></span>
<span data-ttu-id="4ed4a-104">Centrum zabezpieczeń Azure zostanie zaleca włączenie inspekcji i wykrywanie zagrożeń dla wszystkich baz danych na serwerach Azure SQL, jeśli inspekcji nie jest jeszcze włączone.</span><span class="sxs-lookup"><span data-stu-id="4ed4a-104">Azure Security Center will recommend that you turn on auditing and threat detection for all databases on your Azure SQL servers if auditing is not already enabled.</span></span> <span data-ttu-id="4ed4a-105">Inspekcja i jakie wykrywania pomaga zachować zgodność z przepisami, analizować aktywność bazy danych oraz uzyskać wgląd w odchylenia i anomalie, które mogą oznaczać problemy biznesowe lub podejrzane naruszenia zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="4ed4a-105">Auditing and threat detection can help you maintain regulatory compliance, understand database activity, and gain insight into discrepancies and anomalies that could indicate business concerns or suspected security violations.</span></span>

<span data-ttu-id="4ed4a-106">Po włączeniu inspekcji można skonfigurować wykrywanie zagrożeń ustawienia i wiadomości e-mail tooreceive alertów zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="4ed4a-106">Once you’ve turned on auditing you can configure Threat Detection settings and emails tooreceive security alerts.</span></span> <span data-ttu-id="4ed4a-107">Wykrywanie zagrożeń wykrywa nietypowe działania bazy danych wskazujące toohello zagrożenia potencjalnych zabezpieczeń bazy danych.</span><span class="sxs-lookup"><span data-stu-id="4ed4a-107">Threat Detection detects anomalous database activities indicating potential security threats toohello database.</span></span> <span data-ttu-id="4ed4a-108">To pozwala toodetect i odpowiadać toopotential zagrożeń w miarę ich występowania.</span><span class="sxs-lookup"><span data-stu-id="4ed4a-108">This enables you toodetect and respond toopotential threats as they occur.</span></span>

<span data-ttu-id="4ed4a-109">To zalecenie dotyczy toohello usługi Azure SQL. nie ma wśród nich programu SQL Server uruchomionego na maszynach wirtualnych w usługi infrastruktury platformy Azure (IaaS platformy Azure).</span><span class="sxs-lookup"><span data-stu-id="4ed4a-109">This recommendation applies toohello Azure SQL service only; it doesn’t include SQL Server running on your virtual machines in Azure Infrastructure Services (Azure IaaS).</span></span>

> [!NOTE]
> <span data-ttu-id="4ed4a-110">Tym dokumencie przedstawiono hello usługi za pomocą przykładowego wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="4ed4a-110">This document introduces hello service by using an example deployment.</span></span>  <span data-ttu-id="4ed4a-111">Nie jest to przewodnik krok po kroku.</span><span class="sxs-lookup"><span data-stu-id="4ed4a-111">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-hello-recommendation"></a><span data-ttu-id="4ed4a-112">Implementowanie hello zalecenia</span><span class="sxs-lookup"><span data-stu-id="4ed4a-112">Implement hello recommendation</span></span>
1. <span data-ttu-id="4ed4a-113">W hello **zalecenia** bloku, wybierz opcję **Włączanie inspekcji i wykrywanie zagrożeń na serwerach SQL**.</span><span class="sxs-lookup"><span data-stu-id="4ed4a-113">In hello **Recommendations** blade, select **Enable Auditing & Threat detection on SQL servers**.</span></span>  <span data-ttu-id="4ed4a-114">Spowoduje to otwarcie hello **Włączanie inspekcji i wykrywanie zagrożeń na serwerach SQL** bloku.</span><span class="sxs-lookup"><span data-stu-id="4ed4a-114">This opens hello **Enable Auditing & Threat detection on SQL servers** blade.</span></span>

   ![Włączanie inspekcji dla serwerów SQL][1]
2. <span data-ttu-id="4ed4a-116">Wybierz program SQL server tooenable inspekcji i wykrywania zagrożeń.</span><span class="sxs-lookup"><span data-stu-id="4ed4a-116">Select a SQL server tooenable auditing and threat detection on.</span></span> <span data-ttu-id="4ed4a-117">Spowoduje to otwarcie hello **Inspekcja i wykrywanie zagrożeń** bloku.</span><span class="sxs-lookup"><span data-stu-id="4ed4a-117">This opens hello **Auditing & Threat Detection** blade.</span></span>

3. <span data-ttu-id="4ed4a-118">Na powitania **Inspekcja i wykrywanie zagrożeń** bloku, wybierz opcję **ON** w obszarze **inspekcji**.</span><span class="sxs-lookup"><span data-stu-id="4ed4a-118">On hello **Auditing & Threat Detection** blade, select **ON** under **Auditing**.</span></span>

   ![Włączanie ustawień inspekcji][2]
4. <span data-ttu-id="4ed4a-120">Wykonaj kroki hello w [inspekcja bazy danych SQL w hello portalu Azure](../sql-database/sql-database-auditing-portal.md) magazynu tooconfigure przechowywania dzienników inspekcji.</span><span class="sxs-lookup"><span data-stu-id="4ed4a-120">Follow hello steps in [SQL database auditing in hello Azure portal](../sql-database/sql-database-auditing-portal.md) tooconfigure storage where your audit logs will be stored.</span></span> <span data-ttu-id="4ed4a-121">Witaj konta magazynu dla tej subskrypcji do zbierania danych jest hello domyślne konto magazynu.</span><span class="sxs-lookup"><span data-stu-id="4ed4a-121">hello subscription's storage account for data collection is hello default storage account.</span></span>
5. <span data-ttu-id="4ed4a-122">Wykonaj kroki hello w [wprowadzenie wykrywanie zagrożeń bazy danych SQL](../sql-database/sql-database-threat-detection.md) tooturn na i skonfiguruj wykrywanie zagrożeń i tooconfigure hello listę wiadomości e-mail, które będą wysyłane alerty zabezpieczeń po wykryciu nietypowych działań.</span><span class="sxs-lookup"><span data-stu-id="4ed4a-122">Follow hello steps in [Get started with SQL Database Threat Detection](../sql-database/sql-database-threat-detection.md) tooturn on and configure Threat Detection and tooconfigure hello list of emails that will receive security alerts upon detection of anomalous activities.</span></span>

## <a name="see-also"></a><span data-ttu-id="4ed4a-123">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="4ed4a-123">See also</span></span>
<span data-ttu-id="4ed4a-124">W tym artykule pokazano, jak tooimplement hello zalecenia Centrum zabezpieczeń "Włączania inspekcji i wykrywanie na serwerach SQL zagrożeń".</span><span class="sxs-lookup"><span data-stu-id="4ed4a-124">This article showed you how tooimplement hello Security Center recommendation "Enable auditing and threat detection on SQL servers."</span></span> <span data-ttu-id="4ed4a-125">toolearn więcej informacji na temat zabezpieczania bazy danych SQL, zobacz następujące hello:</span><span class="sxs-lookup"><span data-stu-id="4ed4a-125">toolearn more about securing your SQL database, see hello following:</span></span>

* [<span data-ttu-id="4ed4a-126">Zabezpieczanie bazy danych SQL</span><span class="sxs-lookup"><span data-stu-id="4ed4a-126">Securing your SQL Database</span></span>](../sql-database/sql-database-security-overview.md)

<span data-ttu-id="4ed4a-127">toolearn więcej informacji na temat Centrum zabezpieczeń, zobacz następujące hello:</span><span class="sxs-lookup"><span data-stu-id="4ed4a-127">toolearn more about Security Center, see hello following:</span></span>

* <span data-ttu-id="4ed4a-128">[Ustawianie zasad zabezpieczeń w Centrum zabezpieczeń Azure](security-center-policies.md) — Dowiedz się, jak tooconfigure zasad zabezpieczeń dla subskrypcji platformy Azure i grup zasobów.</span><span class="sxs-lookup"><span data-stu-id="4ed4a-128">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="4ed4a-129">[Zarządzanie zaleceniami dotyczącymi zabezpieczeń w Centrum zabezpieczeń Azure](security-center-recommendations.md) — Dowiedz się, w jaki sposób zalecenia ułatwiają ochronę zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="4ed4a-129">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="4ed4a-130">[Monitorowanie kondycji zabezpieczeń w Centrum zabezpieczeń Azure](security-center-monitoring.md) — Dowiedz się, jak toomonitor hello kondycji zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="4ed4a-130">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="4ed4a-131">[Zarządzanie i odpowiada toosecurity alertów w Centrum zabezpieczeń Azure](security-center-managing-and-responding-alerts.md) — Dowiedz się, jak alerty toosecurity toomanage i odpowiada.</span><span class="sxs-lookup"><span data-stu-id="4ed4a-131">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="4ed4a-132">[Monitorowanie rozwiązań partnerskich w Centrum zabezpieczeń Azure](security-center-partner-solutions.md) — Dowiedz się, jak toomonitor hello stanu kondycji rozwiązań partnerskich.</span><span class="sxs-lookup"><span data-stu-id="4ed4a-132">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how toomonitor hello health status of your partner solutions.</span></span>
* <span data-ttu-id="4ed4a-133">[Centrum zabezpieczeń Azure — często zadawane pytania](security-center-faq.md) — często zadawane pytania dotyczące korzystania z usługi hello Znajdź.</span><span class="sxs-lookup"><span data-stu-id="4ed4a-133">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="4ed4a-134">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) --hello najnowsze zabezpieczeń platformy Azure i informacji.</span><span class="sxs-lookup"><span data-stu-id="4ed4a-134">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Get hello latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-enable-auditing-on-sql-server/enable-auditing-on-sql-servers.png
[2]: ./media/security-center-enable-auditing-on-sql-server/auditing-settings-blade.png
