---
title: "Ocena linii bazowej sieci Web w rozwiązaniu Zabezpieczenia i inspekcja w pakiecie Operations Management Suite | Microsoft Docs"
description: "W tym dokumencie wyjaśniono, jak korzystać z rozwiązania Zabezpieczenia i inspekcja w pakiecie OMS w celu oceny linii bazowej sieci Web wszystkich monitorowanych serwerów sieci Web pod kątem zgodności i zabezpieczeń."
services: operations-management-suite
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ROBOTS: NOINDEX
redirect_url: https://www.microsoft.com/cloud-platform/security-and-compliance
ms.assetid: 17837c8b-3e79-47c0-9b83-a51c6ca44ca6
ms.service: operations-management-suite
ms.custom: oms-security
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/27/2017
ms.author: yurid
ms.openlocfilehash: 0d4707dc0c0ffbf40d0d10a6d12b9709a9655258
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="web-baseline-assessment-in-operations-management-suite-security-and-audit-solution"></a><span data-ttu-id="6663a-103">Ocena linii bazowej sieci Web w rozwiązaniu Zabezpieczenia i inspekcja w pakiecie Operations Management Suite</span><span class="sxs-lookup"><span data-stu-id="6663a-103">Web Baseline Assessment in Operations Management Suite Security and Audit Solution</span></span>
<span data-ttu-id="6663a-104">Ten dokument ułatwia korzystanie z funkcji oceny linii bazowej sieci Web w [rozwiązaniu Zabezpieczenia i inspekcja w pakiecie Operations Management Suite (OMS)](operations-management-suite-overview.md) w celu zapewnienia bezpieczeństwa monitorowanych zasobów.</span><span class="sxs-lookup"><span data-stu-id="6663a-104">This document helps you to use [Operations Management Suite (OMS) Security and Audit Solution](operations-management-suite-overview.md) web baseline assessment capabilities to access the secure state of your monitored resources.</span></span>

## <a name="what-is-web-baseline-assessment"></a><span data-ttu-id="6663a-105">Co to jest ocena linii bazowej sieci Web?</span><span class="sxs-lookup"><span data-stu-id="6663a-105">What is Web Baseline Assessment?</span></span>
<span data-ttu-id="6663a-106">Obecnie rozwiązanie Zabezpieczenia w pakiecie OMS umożliwia ocenę podstawy linii bazowej zabezpieczeń systemów operacyjnych.</span><span class="sxs-lookup"><span data-stu-id="6663a-106">Currently OMS Security provides security baseline assessment for operating systems.</span></span> <span data-ttu-id="6663a-107">Skanuje ono ustawienia systemu operacyjnego serwerów co 24 godziny i zapewnia wgląd w ich potencjalnie zagrożone ustawienia.</span><span class="sxs-lookup"><span data-stu-id="6663a-107">It scans the operating system settings of your servers every 24 hours and provides a view into potentially vulnerable settings.</span></span> <span data-ttu-id="6663a-108">Przeczytaj artykuł [Ocena linii bazowej w rozwiązaniu Zabezpieczenia i inspekcja w pakiecie Operations Management Suite](oms-security-baseline.md), aby uzyskać więcej informacji na ten temat.</span><span class="sxs-lookup"><span data-stu-id="6663a-108">Read [Baseline Assessment in Operations Management Suite Security and Audit Solution](oms-security-baseline.md) for more information on this.</span></span>

<span data-ttu-id="6663a-109">Ocena linii bazowej sieci Web ma na celu znalezienie potencjalnie zagrożonych ustawień serwera sieci Web.</span><span class="sxs-lookup"><span data-stu-id="6663a-109">The goal of the web baseline assessment is to find potentially vulnerable web server settings.</span></span> <span data-ttu-id="6663a-110">Trzy podstawowe źródła konfiguracji linii bazowej sieci Web to konfiguracja platformy .NET, platformy ASP.NET i usług IIS.</span><span class="sxs-lookup"><span data-stu-id="6663a-110">The three primary sources for the web baseline configurations are: .NET, ASP.NET, and IIS configuration.</span></span>  <span data-ttu-id="6663a-111">Podobnie jak w przypadku oceny linii bazowej systemu operacyjnego rozwiązanie Zabezpieczenia w pakiecie OMS skanuje serwery sieci Web co 24 godziny i zapewnia wgląd w ich stan zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="6663a-111">Just like the operating system baseline assessment, OMS Security is going to scan your web servers every 24hrs and provide a view into security state of them.</span></span>  <span data-ttu-id="6663a-112">W przypadku usługi Internet Information Service (IIS) konfiguracje mogą być w znaczącym stopniu dostosowywane, co pozwala na zastępowanie różnych poziomów witryny i aplikacji.</span><span class="sxs-lookup"><span data-stu-id="6663a-112">In Internet Information Service (IIS), configurations are highly customizable, which allows various site and application levels to be overridden.</span></span> <span data-ttu-id="6663a-113">Skaner sprawdza ustawienia na każdym poziomie witryny/aplikacji oraz na domyślnym poziomie głównym.</span><span class="sxs-lookup"><span data-stu-id="6663a-113">The scanner checks the settings at each application/site level in addition to the default root level.</span></span> <span data-ttu-id="6663a-114">Ułatwia to znajdowanie lokalizacji potencjalnie zagrożonych ustawień i szybkie rozwiązywanie problemów.</span><span class="sxs-lookup"><span data-stu-id="6663a-114">This helps you to identify potential vulnerability settings locations and quickly remediate.</span></span>


## <a name="web-security-baseline-assessment"></a><span data-ttu-id="6663a-115">Ocena linii bazowej zabezpieczeń sieci Web</span><span class="sxs-lookup"><span data-stu-id="6663a-115">Web Security Baseline Assessment</span></span>
<span data-ttu-id="6663a-116">Dostęp do tej wersji zapoznawczej funkcji będzie można uzyskać za pomocą opcji wyszukiwania w pakiecie OMS.</span><span class="sxs-lookup"><span data-stu-id="6663a-116">For this preview this feature is going to be accessed using the OMS Search option.</span></span> <span data-ttu-id="6663a-117">Aby uruchomić odpowiednie zapytanie, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="6663a-117">Follow the steps below to perform the appropriated query:</span></span>

1. <span data-ttu-id="6663a-118">Na głównym pulpicie nawigacyjnym pakietu **Microsoft Operations Management Suite** kliknij kafelek **Zabezpieczenia i inspekcja**.</span><span class="sxs-lookup"><span data-stu-id="6663a-118">In the **Microsoft Operations Management Suite** main dashboard click **Security and Audit** tile.</span></span>
2. <span data-ttu-id="6663a-119">Na pulpicie nawigacyjnym **Zabezpieczenia i inspekcja** kliknij przycisk **Przeszukiwanie dzienników**.</span><span class="sxs-lookup"><span data-stu-id="6663a-119">In the **Security and Audit** dashboard, click **Log Search** button.</span></span>
3. <span data-ttu-id="6663a-120">Pierwszym zapytaniem, którego możesz użyć, jest zapytanie **podsumowania oceny linii bazowej sieci Web**.</span><span class="sxs-lookup"><span data-stu-id="6663a-120">The first query that you can use is the **Web Baseline Assessment Summary**.</span></span> <span data-ttu-id="6663a-121">W polu **Rozpocznij wyszukiwanie tutaj** wpisz to zapytanie: Type*=SecurityBaselineSummary BaselineType=web*.</span><span class="sxs-lookup"><span data-stu-id="6663a-121">In the **Begin search here** field, type this query: Type*=SecurityBaselineSummary BaselineType=web*.</span></span> <span data-ttu-id="6663a-122">Następujący ekran zawiera przykładowe dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="6663a-122">The following screen has an output sample:</span></span>

![Podsumowanie oceny linii bazowej sieci Web](./media/oms-security-web-baseline/oms-security-web-baseline-fig1-new.png)

> [!NOTE]
> <span data-ttu-id="6663a-124">W tym zapytaniu każdy rekord wskazuje podsumowanie oceny na jednym serwerze.</span><span class="sxs-lookup"><span data-stu-id="6663a-124">In this query, each record indicates assessment summary on a single server.</span></span>

<span data-ttu-id="6663a-125">Po otwarciu **przeszukiwania dzienników** możesz wpisywać różne zapytania, aby uzyskać więcej informacji o ocenie linii bazowej sieci Web.</span><span class="sxs-lookup"><span data-stu-id="6663a-125">Once you are in the **Log Search**, you can type different queries to obtain more information about the web baseline assessment.</span></span> <span data-ttu-id="6663a-126">Oprócz poprzedniego zapytania w tej wersji zapoznawczej można użyć poniższych zapytań.</span><span class="sxs-lookup"><span data-stu-id="6663a-126">In addition to the previous query, you can also use the following ones in this preview.</span></span>

<span data-ttu-id="6663a-127">**Ocena reguły linii bazowej sieci Web**: każdy rekord reprezentuje jedną ocenę reguły linii bazowej sieci Web na jednym serwerze.</span><span class="sxs-lookup"><span data-stu-id="6663a-127">**Web Baseline Rule Assessment**: Each record represents a single web baseline rule evaluation on a single server.</span></span> <span data-ttu-id="6663a-128">Zawiera wszystkie dane dotyczące reguły, lokalizacji, oczekiwanego wyniku i rzeczywistego wyniku.</span><span class="sxs-lookup"><span data-stu-id="6663a-128">It includes all data for the rule, location, the expected result, and the actual result.</span></span>

<span data-ttu-id="6663a-129">**Zapytanie**: Type*=SecurityBaseline BaselineType=web*</span><span class="sxs-lookup"><span data-stu-id="6663a-129">**Query**: Type*=SecurityBaseline BaselineType=web*</span></span>

![Ocena reguły linii bazowej sieci Web](./media/oms-security-web-baseline/oms-security-web-baseline-fig2.png)

<span data-ttu-id="6663a-131">**Pokaż wszystkie wyniki dla określonego serwera**: to zapytanie pozwala wyświetlić wyniki z określonego serwera.</span><span class="sxs-lookup"><span data-stu-id="6663a-131">**Show all results for a specific server**: This query shows how to see results of a specific server.</span></span>

<span data-ttu-id="6663a-132">**Zapytanie**: *Type=SecurityBaseline BaselineType=web Computer=BaselineTestVM1*</span><span class="sxs-lookup"><span data-stu-id="6663a-132">**Query**: *Type=SecurityBaseline BaselineType=web Computer=BaselineTestVM1*</span></span>

![Wszystkie wyniki](./media/oms-security-web-baseline/oms-security-web-baseline-fig3.png)

<span data-ttu-id="6663a-134">Te rekordy/zapytania umożliwiają również tworzenie własnych pulpitów nawigacyjnych, raportów i alertów.</span><span class="sxs-lookup"><span data-stu-id="6663a-134">You can also use these records/queries to create your own dashboards, reports, or alerts.</span></span> <span data-ttu-id="6663a-135">Na poniższym ekranie pokazano przykładową kontrolkę interfejsu użytkownika, którą można dodać do pulpitu nawigacyjnego.</span><span class="sxs-lookup"><span data-stu-id="6663a-135">The screen below has a sample UI control that you can add to your dashboard.</span></span> <span data-ttu-id="6663a-136">Aby dowiedzieć się, jak wizualizować dane przy użyciu projektanta widoku w pakiecie OMS, kliknij [tutaj](https://blogs.technet.microsoft.com/msoms/2016/06/30/oms-view-designer-visualize-your-data-your-way/).</span><span class="sxs-lookup"><span data-stu-id="6663a-136">You can learn how to visualize your data using OMS View Designer [here](https://blogs.technet.microsoft.com/msoms/2016/06/30/oms-view-designer-visualize-your-data-your-way/).</span></span> <span data-ttu-id="6663a-137">Na poniższym ekranie pokazano przykładowy wygląd kafelka po wprowadzeniu tego dostosowania.</span><span class="sxs-lookup"><span data-stu-id="6663a-137">The screen below is an example of how the tile will look like once you make this customization.</span></span>

![Przykładowy interfejs użytkownika](./media/oms-security-web-baseline/oms-security-web-baseline-fig4.png)

> [!NOTE]
> <span data-ttu-id="6663a-139">Aby dowiedzieć się, które ustawienia są sprawdzane pod kątem oceny linii bazowej, pobierz [ten arkusz kalkulacyjny programu Excel](https://gallery.technet.microsoft.com/OMS-Web-Baseline-1e811690) z informacjami o tych ustawieniach.</span><span class="sxs-lookup"><span data-stu-id="6663a-139">If you would like to know the settings that are checked for the baseline assessment, you can download [this Excel spreadsheet](https://gallery.technet.microsoft.com/OMS-Web-Baseline-1e811690) that contains these settings.</span></span>

## <a name="see-also"></a><span data-ttu-id="6663a-140">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="6663a-140">See also</span></span>
<span data-ttu-id="6663a-141">Ten dokument przedstawia informacje na temat oceny linii bazowej sieci Web w rozwiązaniu Zabezpieczenia i inspekcja w pakiecie OMS.</span><span class="sxs-lookup"><span data-stu-id="6663a-141">In this document, you learned about OMS Security and Audit web baseline assessment.</span></span> <span data-ttu-id="6663a-142">Więcej informacji na temat zabezpieczeń w pakiecie OMS zawierają następujące artykuły:</span><span class="sxs-lookup"><span data-stu-id="6663a-142">To learn more about OMS Security, see the following articles:</span></span>

* [<span data-ttu-id="6663a-143">Omówienie pakietu Operations Management Suite (OMS)</span><span class="sxs-lookup"><span data-stu-id="6663a-143">Operations Management Suite (OMS) overview</span></span>](operations-management-suite-overview.md)
* [<span data-ttu-id="6663a-144">Monitorowanie alertów zabezpieczeń i reagowanie na nie w rozwiązaniu Zabezpieczenia i inspekcja w pakiecie Operations Management Suite</span><span class="sxs-lookup"><span data-stu-id="6663a-144">Monitoring and Responding to Security Alerts in Operations Management Suite Security and Audit Solution</span></span>](oms-security-responding-alerts.md)
* [<span data-ttu-id="6663a-145">Monitorowanie zasobów w rozwiązaniu Zabezpieczenia i inspekcja w pakiecie Operations Management Suite</span><span class="sxs-lookup"><span data-stu-id="6663a-145">Monitoring Resources in Operations Management Suite Security and Audit Solution</span></span>](oms-security-monitoring-resources.md)

