---
title: "aaaOperations zabezpieczeń pakietu administracyjnego i inspekcji rozwiązanie sieci Web bazową | Dokumentacja firmy Microsoft"
description: "W tym dokumencie opisano sposób toouse OMS zabezpieczeń i inspekcji rozwiązania tooperform oceny linii bazowej sieci web, wszystkich serwerów sieci web monitorowane w celu zgodności i zabezpieczeń."
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
ms.openlocfilehash: 8aa87fa404ff97ab549dda3f9bebb75766055963
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="web-baseline-assessment-in-operations-management-suite-security-and-audit-solution"></a><span data-ttu-id="858ab-103">Ocena linii bazowej sieci Web w rozwiązaniu Zabezpieczenia i inspekcja w pakiecie Operations Management Suite</span><span class="sxs-lookup"><span data-stu-id="858ab-103">Web Baseline Assessment in Operations Management Suite Security and Audit Solution</span></span>
<span data-ttu-id="858ab-104">Ten dokument ułatwia toouse [zabezpieczeń Operations Management Suite (OMS) i rozwiązania inspekcji](operations-management-suite-overview.md) oceny linii bazowej tooaccess możliwości hello bezpieczny stan monitorowanych zasobów w sieci web.</span><span class="sxs-lookup"><span data-stu-id="858ab-104">This document helps you toouse [Operations Management Suite (OMS) Security and Audit Solution](operations-management-suite-overview.md) web baseline assessment capabilities tooaccess hello secure state of your monitored resources.</span></span>

## <a name="what-is-web-baseline-assessment"></a><span data-ttu-id="858ab-105">Co to jest ocena linii bazowej sieci Web?</span><span class="sxs-lookup"><span data-stu-id="858ab-105">What is Web Baseline Assessment?</span></span>
<span data-ttu-id="858ab-106">Obecnie rozwiązanie Zabezpieczenia w pakiecie OMS umożliwia ocenę podstawy linii bazowej zabezpieczeń systemów operacyjnych.</span><span class="sxs-lookup"><span data-stu-id="858ab-106">Currently OMS Security provides security baseline assessment for operating systems.</span></span> <span data-ttu-id="858ab-107">Skanuje hello ustawień systemu operacyjnego serwerów co 24 godziny i zapewnia wgląd do ustawienia potencjalnie narażone.</span><span class="sxs-lookup"><span data-stu-id="858ab-107">It scans hello operating system settings of your servers every 24 hours and provides a view into potentially vulnerable settings.</span></span> <span data-ttu-id="858ab-108">Przeczytaj artykuł [Ocena linii bazowej w rozwiązaniu Zabezpieczenia i inspekcja w pakiecie Operations Management Suite](oms-security-baseline.md), aby uzyskać więcej informacji na ten temat.</span><span class="sxs-lookup"><span data-stu-id="858ab-108">Read [Baseline Assessment in Operations Management Suite Security and Audit Solution](oms-security-baseline.md) for more information on this.</span></span>

<span data-ttu-id="858ab-109">Celem Hello oceny linii bazowej sieci web hello jest ustawień serwera sieci web potencjalnie narażone toofind.</span><span class="sxs-lookup"><span data-stu-id="858ab-109">hello goal of hello web baseline assessment is toofind potentially vulnerable web server settings.</span></span> <span data-ttu-id="858ab-110">Witaj trzech źródeł podstawowy to hello web linii bazowej konfiguracji: konfiguracji platformy .NET, ASP.NET oraz usług IIS.</span><span class="sxs-lookup"><span data-stu-id="858ab-110">hello three primary sources for hello web baseline configurations are: .NET, ASP.NET, and IIS configuration.</span></span>  <span data-ttu-id="858ab-111">Podobnie jak hello ocenę linii bazowej systemu operacyjnego, OMS zabezpieczeń będzie tooscan Twojego serwery sieci web co 24hrs i podaj zapewnia wgląd w ich stanie zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="858ab-111">Just like hello operating system baseline assessment, OMS Security is going tooscan your web servers every 24hrs and provide a view into security state of them.</span></span>  <span data-ttu-id="858ab-112">W konsoli Internet Information Service (IIS) konfiguracje są dużym stopniu dostosowywane umożliwiającą różnych witryny i aplikacji toobe poziomy zastąpiona.</span><span class="sxs-lookup"><span data-stu-id="858ab-112">In Internet Information Service (IIS), configurations are highly customizable, which allows various site and application levels toobe overridden.</span></span> <span data-ttu-id="858ab-113">Skaner Hello sprawdza ustawienia hello na każdym poziomie witryny/aplikacji dodanie toohello domyślnego katalogu głównego poziomu.</span><span class="sxs-lookup"><span data-stu-id="858ab-113">hello scanner checks hello settings at each application/site level in addition toohello default root level.</span></span> <span data-ttu-id="858ab-114">To ułatwia tooidentify potencjalnych luk w zabezpieczeniach ustawienia lokalizacji i szybko skorygować.</span><span class="sxs-lookup"><span data-stu-id="858ab-114">This helps you tooidentify potential vulnerability settings locations and quickly remediate.</span></span>


## <a name="web-security-baseline-assessment"></a><span data-ttu-id="858ab-115">Ocena linii bazowej zabezpieczeń sieci Web</span><span class="sxs-lookup"><span data-stu-id="858ab-115">Web Security Baseline Assessment</span></span>
<span data-ttu-id="858ab-116">Dla tej wersji zapoznawczej tej funkcji będzie toobe dostęp za pomocą opcji wyszukiwania OMS hello.</span><span class="sxs-lookup"><span data-stu-id="858ab-116">For this preview this feature is going toobe accessed using hello OMS Search option.</span></span> <span data-ttu-id="858ab-117">Wykonaj kroki hello poniżej tooperform hello przeznaczona zapytania:</span><span class="sxs-lookup"><span data-stu-id="858ab-117">Follow hello steps below tooperform hello appropriated query:</span></span>

1. <span data-ttu-id="858ab-118">W hello **programu Microsoft Operations Management Suite** głównym pulpicie nawigacyjnym kliknij **zabezpieczeń i inspekcji** kafelka.</span><span class="sxs-lookup"><span data-stu-id="858ab-118">In hello **Microsoft Operations Management Suite** main dashboard click **Security and Audit** tile.</span></span>
2. <span data-ttu-id="858ab-119">W hello **zabezpieczeń i inspekcji** pulpitu nawigacyjnego, kliknij przycisk **wyszukiwania dziennika** przycisku.</span><span class="sxs-lookup"><span data-stu-id="858ab-119">In hello **Security and Audit** dashboard, click **Log Search** button.</span></span>
3. <span data-ttu-id="858ab-120">Hello pierwszego zapytania, którego można używać jest hello **podsumowanie oceny linii bazowej sieci Web**.</span><span class="sxs-lookup"><span data-stu-id="858ab-120">hello first query that you can use is hello **Web Baseline Assessment Summary**.</span></span> <span data-ttu-id="858ab-121">W hello **tutaj wyszukiwania Begin** wpisz tego zapytania: typ*= SecurityBaselineSummary BaselineType = sieci web*.</span><span class="sxs-lookup"><span data-stu-id="858ab-121">In hello **Begin search here** field, type this query: Type*=SecurityBaselineSummary BaselineType=web*.</span></span> <span data-ttu-id="858ab-122">po ekranie powitania zawiera przykładowe dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="858ab-122">hello following screen has an output sample:</span></span>

![Podsumowanie oceny linii bazowej sieci Web](./media/oms-security-web-baseline/oms-security-web-baseline-fig1-new.png)

> [!NOTE]
> <span data-ttu-id="858ab-124">W tym zapytaniu każdy rekord wskazuje podsumowanie oceny na jednym serwerze.</span><span class="sxs-lookup"><span data-stu-id="858ab-124">In this query, each record indicates assessment summary on a single server.</span></span>

<span data-ttu-id="858ab-125">Po przejściu do hello **wyszukiwania dziennika**, można wpisać tooobtain różne zapytania więcej informacji na temat oceny linii bazowej sieci web hello.</span><span class="sxs-lookup"><span data-stu-id="858ab-125">Once you are in hello **Log Search**, you can type different queries tooobtain more information about hello web baseline assessment.</span></span> <span data-ttu-id="858ab-126">Ponadto toohello poprzednie zapytanie, umożliwia także powitania od tych w tej wersji zapoznawczej.</span><span class="sxs-lookup"><span data-stu-id="858ab-126">In addition toohello previous query, you can also use hello following ones in this preview.</span></span>

<span data-ttu-id="858ab-127">**Ocena reguły linii bazowej sieci Web**: każdy rekord reprezentuje jedną ocenę reguły linii bazowej sieci Web na jednym serwerze.</span><span class="sxs-lookup"><span data-stu-id="858ab-127">**Web Baseline Rule Assessment**: Each record represents a single web baseline rule evaluation on a single server.</span></span> <span data-ttu-id="858ab-128">Zawiera wszystkie dane dla reguły hello, lokalizacji hello oczekiwano wyników i hello rzeczywisty wynik.</span><span class="sxs-lookup"><span data-stu-id="858ab-128">It includes all data for hello rule, location, hello expected result, and hello actual result.</span></span>

<span data-ttu-id="858ab-129">**Zapytanie**: Type*=SecurityBaseline BaselineType=web*</span><span class="sxs-lookup"><span data-stu-id="858ab-129">**Query**: Type*=SecurityBaseline BaselineType=web*</span></span>

![Ocena reguły linii bazowej sieci Web](./media/oms-security-web-baseline/oms-security-web-baseline-fig2.png)

<span data-ttu-id="858ab-131">**Pokaż wszystkie wyniki dla określonego serwera**: to zapytanie pokazuje, jak toosee wyniki z określonego serwera.</span><span class="sxs-lookup"><span data-stu-id="858ab-131">**Show all results for a specific server**: This query shows how toosee results of a specific server.</span></span>

<span data-ttu-id="858ab-132">**Zapytanie**: *Type=SecurityBaseline BaselineType=web Computer=BaselineTestVM1*</span><span class="sxs-lookup"><span data-stu-id="858ab-132">**Query**: *Type=SecurityBaseline BaselineType=web Computer=BaselineTestVM1*</span></span>

![Wszystkie wyniki](./media/oms-security-web-baseline/oms-security-web-baseline-fig3.png)

<span data-ttu-id="858ab-134">Umożliwia także te rekordy/kwerendy toocreate własne pulpity nawigacyjne, raporty lub alerty.</span><span class="sxs-lookup"><span data-stu-id="858ab-134">You can also use these records/queries toocreate your own dashboards, reports, or alerts.</span></span> <span data-ttu-id="858ab-135">Witaj ekranu poniżej zawiera formant interfejsu użytkownika próbki dodać tooyour pulpitu nawigacyjnego.</span><span class="sxs-lookup"><span data-stu-id="858ab-135">hello screen below has a sample UI control that you can add tooyour dashboard.</span></span> <span data-ttu-id="858ab-136">Aby dowiedzieć się jak toovisualize dane przy użyciu projektanta widoków OMS [tutaj](https://blogs.technet.microsoft.com/msoms/2016/06/30/oms-view-designer-visualize-your-data-your-way/).</span><span class="sxs-lookup"><span data-stu-id="858ab-136">You can learn how toovisualize your data using OMS View Designer [here](https://blogs.technet.microsoft.com/msoms/2016/06/30/oms-view-designer-visualize-your-data-your-way/).</span></span> <span data-ttu-id="858ab-137">poniższym zrzucie ekranu Hello jest przykładem sposobu hello kafelka będzie wyglądać po wprowadzeniu takie dostosowanie.</span><span class="sxs-lookup"><span data-stu-id="858ab-137">hello screen below is an example of how hello tile will look like once you make this customization.</span></span>

![Przykładowy interfejs użytkownika](./media/oms-security-web-baseline/oms-security-web-baseline-fig4.png)

> [!NOTE]
> <span data-ttu-id="858ab-139">Jeśli chcesz tooknow hello ustawień, które są sprawdzane pod kątem oceny linii bazowej hello, możesz pobrać [ten arkusz kalkulacyjny programu Excel](https://gallery.technet.microsoft.com/OMS-Web-Baseline-1e811690) zawiera tych ustawień.</span><span class="sxs-lookup"><span data-stu-id="858ab-139">If you would like tooknow hello settings that are checked for hello baseline assessment, you can download [this Excel spreadsheet](https://gallery.technet.microsoft.com/OMS-Web-Baseline-1e811690) that contains these settings.</span></span>

## <a name="see-also"></a><span data-ttu-id="858ab-140">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="858ab-140">See also</span></span>
<span data-ttu-id="858ab-141">Ten dokument przedstawia informacje na temat oceny linii bazowej sieci Web w rozwiązaniu Zabezpieczenia i inspekcja w pakiecie OMS.</span><span class="sxs-lookup"><span data-stu-id="858ab-141">In this document, you learned about OMS Security and Audit web baseline assessment.</span></span> <span data-ttu-id="858ab-142">toolearn więcej informacji na temat zabezpieczeń OMS, zobacz następujące artykuły hello:</span><span class="sxs-lookup"><span data-stu-id="858ab-142">toolearn more about OMS Security, see hello following articles:</span></span>

* [<span data-ttu-id="858ab-143">Omówienie pakietu Operations Management Suite (OMS)</span><span class="sxs-lookup"><span data-stu-id="858ab-143">Operations Management Suite (OMS) overview</span></span>](operations-management-suite-overview.md)
* [<span data-ttu-id="858ab-144">Monitorowanie i alerty tooSecurity odpowiada Operations Management Suite zabezpieczeń i rozwiązanie inspekcji</span><span class="sxs-lookup"><span data-stu-id="858ab-144">Monitoring and Responding tooSecurity Alerts in Operations Management Suite Security and Audit Solution</span></span>](oms-security-responding-alerts.md)
* [<span data-ttu-id="858ab-145">Monitorowanie zasobów w rozwiązaniu Zabezpieczenia i inspekcja w pakiecie Operations Management Suite</span><span class="sxs-lookup"><span data-stu-id="858ab-145">Monitoring Resources in Operations Management Suite Security and Audit Solution</span></span>](oms-security-monitoring-resources.md)

