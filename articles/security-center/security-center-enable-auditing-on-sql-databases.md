---
title: "aaaEnable inspekcji i wykrywania zagrożeń SQL bazy danych w Centrum zabezpieczeń Azure | Dokumentacja firmy Microsoft"
description: "Ten dokument przedstawia sposób tooimplement hello zalecenia Centrum zabezpieczeń Azure ** włączyć inspekcję i wykrywania zagrożeń na baz danych SQL **."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 224b6755-2b36-4ecd-9af8-139a198e0df1
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: terrylan
ms.openlocfilehash: c94140acf37cabaca3e681ba5db79d6827e7b9db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="enable-auditing-and-threat-detection-on-sql-databases-in-azure-security-center"></a><span data-ttu-id="6611d-103">Włącz inspekcję i wykrywania zagrożeń baz danych SQL w Centrum zabezpieczeń Azure</span><span class="sxs-lookup"><span data-stu-id="6611d-103">Enable auditing and threat detection on SQL databases in Azure Security Center</span></span>
<span data-ttu-id="6611d-104">Centrum zabezpieczeń Azure zostanie zaleca włączenie inspekcji i wykrywania zagrożeń dla wszystkich baz danych SQL, jeśli inspekcja i wykrywanie zagrożeń nie jest jeszcze włączone.</span><span class="sxs-lookup"><span data-stu-id="6611d-104">Azure Security Center will recommend that you turn on auditing and threat detection for all SQL databases if auditing and threat detection is not already enabled.</span></span> <span data-ttu-id="6611d-105">Inspekcja i jakie wykrywania pomaga zachować zgodność z przepisami, analizować aktywność bazy danych oraz uzyskać wgląd w odchylenia i anomalie, które mogą oznaczać problemy biznesowe lub podejrzane naruszenia zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="6611d-105">Auditing and threat detection can help you maintain regulatory compliance, understand database activity, and gain insight into discrepancies and anomalies that could indicate business concerns or suspected security violations.</span></span>

<span data-ttu-id="6611d-106">Po włączeniu inspekcji można skonfigurować wykrywanie zagrożeń ustawienia i wiadomości e-mail tooreceive alertów zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="6611d-106">Once you’ve turned on auditing you can configure Threat Detection settings and emails tooreceive security alerts.</span></span> <span data-ttu-id="6611d-107">Wykrywanie zagrożeń wykrywa nietypowe działania bazy danych wskazujące toohello zagrożenia potencjalnych zabezpieczeń bazy danych.</span><span class="sxs-lookup"><span data-stu-id="6611d-107">Threat Detection detects anomalous database activities indicating potential security threats toohello database.</span></span> <span data-ttu-id="6611d-108">To pozwala toodetect i odpowiadać toopotential zagrożeń w miarę ich występowania.</span><span class="sxs-lookup"><span data-stu-id="6611d-108">This enables you toodetect and respond toopotential threats as they occur.</span></span>

<span data-ttu-id="6611d-109">To zalecenie dotyczy toohello usługi Azure SQL. nie ma wśród nich SQL uruchomionych na maszynach wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="6611d-109">This recommendation applies toohello Azure SQL service only; it doesn't include SQL running on your virtual machines.</span></span>

> [!NOTE]
> <span data-ttu-id="6611d-110">Tym dokumencie przedstawiono hello usługi za pomocą przykładowego wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="6611d-110">This document introduces hello service by using an example deployment.</span></span>  <span data-ttu-id="6611d-111">Nie jest to przewodnik krok po kroku.</span><span class="sxs-lookup"><span data-stu-id="6611d-111">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-hello-recommendation"></a><span data-ttu-id="6611d-112">Implementowanie hello zalecenia</span><span class="sxs-lookup"><span data-stu-id="6611d-112">Implement hello recommendation</span></span>
1. <span data-ttu-id="6611d-113">W hello **zalecenia** bloku, wybierz opcję **Włączanie inspekcji i wykrywanie zagrożeń baz danych SQL**.</span><span class="sxs-lookup"><span data-stu-id="6611d-113">In hello **Recommendations** blade, select **Enable Auditing & Threat detection on SQL databases**.</span></span>  <span data-ttu-id="6611d-114">Spowoduje to otwarcie hello **Włączanie inspekcji i wykrywanie zagrożeń baz danych SQL** bloku.</span><span class="sxs-lookup"><span data-stu-id="6611d-114">This opens hello **Enable Auditing & Threat detection on SQL databases** blade.</span></span>

   ![Włączanie inspekcji dla baz danych SQL][1]
2. <span data-ttu-id="6611d-116">Wybierz tooenable bazy danych SQL inspekcji na.</span><span class="sxs-lookup"><span data-stu-id="6611d-116">Select a SQL database tooenable auditing on.</span></span> <span data-ttu-id="6611d-117">Spowoduje to otwarcie hello **Inspekcja i wykrywanie zagrożeń** bloku.</span><span class="sxs-lookup"><span data-stu-id="6611d-117">This opens hello **Auditing & Threat Detection** blade.</span></span>

3. <span data-ttu-id="6611d-118">Na powitania **Inspekcja i wykrywanie zagrożeń** bloku, wybierz opcję **ON** w obszarze **inspekcji**.</span><span class="sxs-lookup"><span data-stu-id="6611d-118">On hello **Auditing & Threat Detection** blade, select **ON** under **Auditing**.</span></span>

   ![Włączanie inspekcji i wykrywania zagrożeń][2]
4. <span data-ttu-id="6611d-120">Wykonaj kroki hello w [wykrywanie zagrożeń bazy danych SQL w portalu Azure hello](../sql-database/sql-database-threat-detection-portal.md) tooturn na i skonfiguruj wykrywanie zagrożeń i tooconfigure hello listę wiadomości e-mail, które będą wysyłane alerty zabezpieczeń po wykryciu nietypowych działań.</span><span class="sxs-lookup"><span data-stu-id="6611d-120">Follow hello steps in [SQL Database Threat Detection in hello Azure portal](../sql-database/sql-database-threat-detection-portal.md) tooturn on and configure Threat Detection and tooconfigure hello list of emails that will receive security alerts upon detection of anomalous activities.</span></span>

## <a name="see-also"></a><span data-ttu-id="6611d-121">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="6611d-121">See also</span></span>
<span data-ttu-id="6611d-122">W tym artykule pokazano, jak tooimplement hello Centrum zabezpieczeń zalecenie "Włącz Inspekcja i wykrywanie zagrożeń baz danych SQL."</span><span class="sxs-lookup"><span data-stu-id="6611d-122">This article showed you how tooimplement hello Security Center recommendation "Enable Auditing & Threat detection on SQL databases."</span></span> <span data-ttu-id="6611d-123">toolearn więcej informacji na temat zabezpieczania bazy danych SQL, zobacz następujące hello:</span><span class="sxs-lookup"><span data-stu-id="6611d-123">toolearn more about securing your SQL database, see hello following:</span></span>

* [<span data-ttu-id="6611d-124">Zabezpieczanie bazy danych SQL</span><span class="sxs-lookup"><span data-stu-id="6611d-124">Securing your SQL Database</span></span>](../sql-database/sql-database-security-overview.md)

<span data-ttu-id="6611d-125">toolearn więcej informacji na temat Centrum zabezpieczeń, zobacz następujące hello:</span><span class="sxs-lookup"><span data-stu-id="6611d-125">toolearn more about Security Center, see hello following:</span></span>

* <span data-ttu-id="6611d-126">[Ustawianie zasad zabezpieczeń w Centrum zabezpieczeń Azure](security-center-policies.md) — Dowiedz się, jak tooconfigure zasad zabezpieczeń dla subskrypcji platformy Azure i grup zasobów.</span><span class="sxs-lookup"><span data-stu-id="6611d-126">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="6611d-127">[Zarządzanie zaleceniami dotyczącymi zabezpieczeń w Centrum zabezpieczeń Azure](security-center-recommendations.md) — Dowiedz się, w jaki sposób zalecenia ułatwiają ochronę zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="6611d-127">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="6611d-128">[Monitorowanie kondycji zabezpieczeń w Centrum zabezpieczeń Azure](security-center-monitoring.md) — Dowiedz się, jak toomonitor hello kondycji zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="6611d-128">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="6611d-129">[Zarządzanie i odpowiada toosecurity alertów w Centrum zabezpieczeń Azure](security-center-managing-and-responding-alerts.md) — Dowiedz się, jak alerty toosecurity toomanage i odpowiada.</span><span class="sxs-lookup"><span data-stu-id="6611d-129">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="6611d-130">[Monitorowanie rozwiązań partnerskich w Centrum zabezpieczeń Azure](security-center-partner-solutions.md) — Dowiedz się, jak toomonitor hello stanu kondycji rozwiązań partnerskich.</span><span class="sxs-lookup"><span data-stu-id="6611d-130">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how toomonitor hello health status of your partner solutions.</span></span>
* <span data-ttu-id="6611d-131">[Centrum zabezpieczeń Azure — często zadawane pytania](security-center-faq.md) — często zadawane pytania dotyczące korzystania z usługi hello Znajdź.</span><span class="sxs-lookup"><span data-stu-id="6611d-131">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="6611d-132">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) --hello najnowsze zabezpieczeń platformy Azure i informacji.</span><span class="sxs-lookup"><span data-stu-id="6611d-132">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Get hello latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-enable-auditing-on-sql-databases/enable-auditing-on-sql-databases.png
[2]: ./media/security-center-enable-auditing-on-sql-databases/auditing-threat-detection-blade.png
