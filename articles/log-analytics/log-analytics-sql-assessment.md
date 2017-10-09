---
title: "aaaOptimize środowiskiem programu SQL Server na platformie Azure Log Analytics | Dokumentacja firmy Microsoft"
description: "Z usługi Analiza dzienników Azure możesz użyć hello oceny SQL tooassess rozwiązania hello ryzyka i kondycji środowisk programu SQL server w regularnych odstępach czasu."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: e297eb57-1718-4cfe-a241-b9e84b2c42ac
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: banders
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f31326d8cdad3ef5d5a190614d1a18c1dac826ed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-your-sql-server-environment-with-hello-sql-assessment-solution-in-log-analytics"></a><span data-ttu-id="930ac-103">Optymalizuj środowisko programu SQL Server z hello oceny SQL rozwiązania analizy dzienników</span><span class="sxs-lookup"><span data-stu-id="930ac-103">Optimize your SQL Server environment with hello SQL Assessment solution in Log Analytics</span></span>

![Symbol oceny SQL](./media/log-analytics-sql-assessment/sql-assessment-symbol.png)

<span data-ttu-id="930ac-105">Możesz użyć hello oceny SQL tooassess rozwiązania hello ryzyka i kondycji środowisk serwera w regularnych odstępach czasu.</span><span class="sxs-lookup"><span data-stu-id="930ac-105">You can use hello SQL Assessment solution tooassess hello risk and health of your server environments on a regular interval.</span></span> <span data-ttu-id="930ac-106">Ten artykuł pomoże Ci zainstalować rozwiązanie hello tak, aby można podjąć działania naprawcze potencjalnych problemów.</span><span class="sxs-lookup"><span data-stu-id="930ac-106">This article will help you install hello solution so that you can take corrective actions for potential problems.</span></span>

<span data-ttu-id="930ac-107">To rozwiązanie zapewnia priorytetową listą zaleceń tooyour określonego wdrożonego serwera infrastruktury.</span><span class="sxs-lookup"><span data-stu-id="930ac-107">This solution provides a prioritized list of recommendations specific tooyour deployed server infrastructure.</span></span> <span data-ttu-id="930ac-108">Hello zalecenia są podzielone na sześć fokus, zrozumiałą dla obszarów, które pomagają w szybkim hello ryzyka i podejmowanie działań naprawczych.</span><span class="sxs-lookup"><span data-stu-id="930ac-108">hello recommendations are categorized across six focus areas which help you quickly understand hello risk and take corrective action.</span></span>

<span data-ttu-id="930ac-109">Witaj zalecenia są oparte na powitania wiedzy i doświadczenia przez pracownicy firmy Microsoft z tysięcy wizyt klienta.</span><span class="sxs-lookup"><span data-stu-id="930ac-109">hello recommendations made are based on hello knowledge and experience gained by Microsoft engineers from thousands of customer visits.</span></span> <span data-ttu-id="930ac-110">Każde zalecenie znajdują się wskazówki dotyczące przyczyny problemu może być niezależnie od tego, tooyou i jak tooimplement hello sugerowane zmiany.</span><span class="sxs-lookup"><span data-stu-id="930ac-110">Each recommendation provides guidance about why an issue might matter tooyou and how tooimplement hello suggested changes.</span></span>

<span data-ttu-id="930ac-111">Można wybrać fokus obszarów, które są najważniejsze tooyour organizacji i śledzić postęp w kierunku uruchomionym środowiskiem ryzyka bezpłatne i działa prawidłowo.</span><span class="sxs-lookup"><span data-stu-id="930ac-111">You can choose focus areas that are most important tooyour organization and track your progress toward running a risk free and healthy environment.</span></span>

<span data-ttu-id="930ac-112">Po dodaniu hello rozwiązania i ocenę jest zakończone, podsumowanie informacji o obszarach zainteresowań jest wyświetlany na powitania **oceny SQL** pulpitu nawigacyjnego dla infrastruktury hello w danym środowisku.</span><span class="sxs-lookup"><span data-stu-id="930ac-112">After you've added hello solution and an assessment is completed, summary information for focus areas is shown on hello **SQL Assessment** dashboard for hello infrastructure in your environment.</span></span> <span data-ttu-id="930ac-113">Witaj poniższych sekcjach opisano sposób toouse hello informacji na temat hello **oceny SQL** pulpitu nawigacyjnego, gdzie można przeglądać i wykonaj zalecane akcje dotyczące infrastruktury serwera SQL.</span><span class="sxs-lookup"><span data-stu-id="930ac-113">hello following sections describe how toouse hello information on hello **SQL Assessment** dashboard, where you can view and then take recommended actions for your SQL server infrastructure.</span></span>

![Obraz kafelka oceny SQL](./media/log-analytics-sql-assessment/sql-assess-tile.png)

![Obraz pulpitu nawigacyjnego oceny SQL](./media/log-analytics-sql-assessment/sql-assess-dash.png)

## <a name="installing-and-configuring-hello-solution"></a><span data-ttu-id="930ac-116">Instalowanie i konfigurowanie hello rozwiązania</span><span class="sxs-lookup"><span data-stu-id="930ac-116">Installing and configuring hello solution</span></span>
<span data-ttu-id="930ac-117">Ocena SQL współpracuje z wszystkich aktualnie obsługiwanych wersjach programu SQL Server dla hello wersje Standard, Developer i Enterprise.</span><span class="sxs-lookup"><span data-stu-id="930ac-117">SQL Assessment works with all currently supported versions of SQL Server for hello Standard, Developer, and Enterprise editions.</span></span>

<span data-ttu-id="930ac-118">Użyj powitania po tooinstall informacji i skonfiguruj hello rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="930ac-118">Use hello following information tooinstall and configure hello solution.</span></span>

* <span data-ttu-id="930ac-119">Agenci musi być zainstalowany na serwerach, które mają zainstalowany program SQL Server.</span><span class="sxs-lookup"><span data-stu-id="930ac-119">Agents must be installed on servers that have SQL Server installed.</span></span>
* <span data-ttu-id="930ac-120">Witaj rozwiązanie do oceny SQL wymaga obsługiwanej wersji programu .NET Framework 4 zainstalowane na każdym komputerze, na którym agent pakietu OMS.</span><span class="sxs-lookup"><span data-stu-id="930ac-120">hello SQL Assessment solution requires a supported version of .NET Framework 4 installed on each computer that has an OMS agent.</span></span>
* <span data-ttu-id="930ac-121">W rozwiązaniu hello tooinstall kolejności użytkownik hello musi być administratorem lub współautora toohello subskrypcji platformy Azure przy użyciu hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="930ac-121">In order tooinstall hello solution, hello user must be an administrator or contributor toohello Azure subscription when using hello Azure portal.</span></span> <span data-ttu-id="930ac-122">Ponadto hello użytkownik musi być członkiem hello OMS obszaru roboczego współautora lub administrator roli w portalu OMS hello.</span><span class="sxs-lookup"><span data-stu-id="930ac-122">In addition, hello user must be a member of hello OMS workspace contributor or administrator role in hello OMS portal.</span></span>
* <span data-ttu-id="930ac-123">Jeśli agent programu Operations Manager hello z SQL do oceny, konieczne będzie toouse konta programu Operations Manager Run-As.</span><span class="sxs-lookup"><span data-stu-id="930ac-123">When using hello Operations Manager agent with SQL Assessment, you'll need toouse an Operations Manager Run-As account.</span></span> <span data-ttu-id="930ac-124">Zobacz [konta programu Operations Manager, Uruchom jako dla OMS](#operations-manager-run-as-accounts-for-oms) poniżej Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="930ac-124">See [Operations Manager run-as accounts for OMS](#operations-manager-run-as-accounts-for-oms) below for more information.</span></span>

  > [!NOTE]
  > <span data-ttu-id="930ac-125">Hello MMA agent nie obsługuje programu Operations Manager Run-As kont.</span><span class="sxs-lookup"><span data-stu-id="930ac-125">hello MMA agent does not support Operations Manager Run-As accounts.</span></span>
  >
  >
* <span data-ttu-id="930ac-126">Dodaj tooyour rozwiązania oceny SQL hello obszarem roboczym pakietu OMS za pomocą hello procesu opisanego w [rozwiązań analizy dzienników dodać hello galerii rozwiązań](log-analytics-add-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="930ac-126">Add hello SQL Assessment solution tooyour OMS workspace using hello process described in [Add Log Analytics solutions from hello Solutions Gallery](log-analytics-add-solutions.md).</span></span> <span data-ttu-id="930ac-127">Nie są wymagane żadne dalsze czynności konfiguracyjne.</span><span class="sxs-lookup"><span data-stu-id="930ac-127">There is no further configuration required.</span></span>

> [!NOTE]
> <span data-ttu-id="930ac-128">Po dodaniu rozwiązania hello hello AdvisorAssessment.exe plik zostanie dodany tooservers z agentami.</span><span class="sxs-lookup"><span data-stu-id="930ac-128">After you've added hello solution, hello AdvisorAssessment.exe file is added tooservers with agents.</span></span> <span data-ttu-id="930ac-129">Dane konfiguracji jest do odczytu i następnie wysyłane toohello usługę w chmurze hello do przetwarzania.</span><span class="sxs-lookup"><span data-stu-id="930ac-129">Configuration data is read and then sent toohello OMS service in hello cloud for processing.</span></span> <span data-ttu-id="930ac-130">Logika jest stosowane toohello odebranych danych i usługi w chmurze hello rejestruje dane hello.</span><span class="sxs-lookup"><span data-stu-id="930ac-130">Logic is applied toohello received data and hello cloud service records hello data.</span></span>

## <a name="sql-assessment-data-collection-details"></a><span data-ttu-id="930ac-131">Szczegóły pobierania danych SQL do oceny</span><span class="sxs-lookup"><span data-stu-id="930ac-131">SQL Assessment data collection details</span></span>
<span data-ttu-id="930ac-132">Ocena SQL służy do zbierania danych usługi WMI, dane rejestru dane dotyczące wydajności i wyników widoku dynamicznego zarządzania programu SQL Server za pomocą hello agentów, które mają włączone.</span><span class="sxs-lookup"><span data-stu-id="930ac-132">SQL Assessment collects WMI data, registry data, performance data, and SQL Server dynamic management view results using hello agents that you have enabled.</span></span>

<span data-ttu-id="930ac-133">Witaj poniższej tabeli przedstawiono metody zbierania danych dla agentów, czy Operations Manager (SCOM) jest wymagany i jak często dane są zbierane przez agenta.</span><span class="sxs-lookup"><span data-stu-id="930ac-133">hello following table shows data collection methods for agents, whether Operations Manager (SCOM) is required, and how often data is collected by an agent.</span></span>

| <span data-ttu-id="930ac-134">Platformy</span><span class="sxs-lookup"><span data-stu-id="930ac-134">platform</span></span> | <span data-ttu-id="930ac-135">Bezpośrednie agenta</span><span class="sxs-lookup"><span data-stu-id="930ac-135">Direct Agent</span></span> | <span data-ttu-id="930ac-136">Agenta programu SCOM</span><span class="sxs-lookup"><span data-stu-id="930ac-136">SCOM agent</span></span> | <span data-ttu-id="930ac-137">Azure Storage</span><span class="sxs-lookup"><span data-stu-id="930ac-137">Azure Storage</span></span> | <span data-ttu-id="930ac-138">SCOM wymagane?</span><span class="sxs-lookup"><span data-stu-id="930ac-138">SCOM required?</span></span> | <span data-ttu-id="930ac-139">Dane agenta programu SCOM wysyłane za pośrednictwem grupy zarządzania</span><span class="sxs-lookup"><span data-stu-id="930ac-139">SCOM agent data sent via management group</span></span> | <span data-ttu-id="930ac-140">Częstotliwość kolekcji</span><span class="sxs-lookup"><span data-stu-id="930ac-140">collection frequency</span></span> |
| --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="930ac-141">Windows</span><span class="sxs-lookup"><span data-stu-id="930ac-141">Windows</span></span> | <span data-ttu-id="930ac-142">&#8226;</span><span class="sxs-lookup"><span data-stu-id="930ac-142">&#8226;</span></span> | <span data-ttu-id="930ac-143">&#8226;</span><span class="sxs-lookup"><span data-stu-id="930ac-143">&#8226;</span></span> |  |  | <span data-ttu-id="930ac-144">&#8226;</span><span class="sxs-lookup"><span data-stu-id="930ac-144">&#8226;</span></span> |<span data-ttu-id="930ac-145">7 dni</span><span class="sxs-lookup"><span data-stu-id="930ac-145">7 days</span></span> |

## <a name="operations-manager-run-as-accounts-for-oms"></a><span data-ttu-id="930ac-146">Uruchom jako konta programu Operations Manager dla OMS</span><span class="sxs-lookup"><span data-stu-id="930ac-146">Operations Manager run-as accounts for OMS</span></span>
<span data-ttu-id="930ac-147">Analiza dzienników w OMS używa hello agenta programu Operations Manager i toocollect grupy zarządzania i wysyłać dane toohello usługę.</span><span class="sxs-lookup"><span data-stu-id="930ac-147">Log Analytics in OMS uses hello Operations Manager agent and management group toocollect and send data toohello OMS service.</span></span> <span data-ttu-id="930ac-148">Kompilacje OMS na pakiety administracyjne dla obciążeń tooprovide wartość — Dodawanie usług.</span><span class="sxs-lookup"><span data-stu-id="930ac-148">OMS builds upon management packs for workloads tooprovide value-add services.</span></span> <span data-ttu-id="930ac-149">Pakiety administracyjne toorun uprawnienia specyficznego dla obciążenia w innym kontekście zabezpieczeń, takie jak konto domeny wymaga poszczególnych obciążeń.</span><span class="sxs-lookup"><span data-stu-id="930ac-149">Each workload requires workload-specific privileges toorun management packs in a different security context, such as a domain account.</span></span> <span data-ttu-id="930ac-150">Potrzebujesz informacji o poświadczeniach tooprovide przez skonfigurowanie konta Operations Manager uruchom jako.</span><span class="sxs-lookup"><span data-stu-id="930ac-150">You need tooprovide credential information by configuring an Operations Manager Run As account.</span></span>

<span data-ttu-id="930ac-151">Użyj hello następujące informacje tooset hello programu Operations Manager konto Uruchom jako w celu oceny SQL.</span><span class="sxs-lookup"><span data-stu-id="930ac-151">Use hello following information tooset hello Operations Manager run-as account for SQL Assessment.</span></span>

### <a name="set-hello-run-as-account-for-sql-assessment"></a><span data-ttu-id="930ac-152">Ustaw hello konta Uruchom jako w celu oceny SQL</span><span class="sxs-lookup"><span data-stu-id="930ac-152">Set hello Run As account for SQL assessment</span></span>
 <span data-ttu-id="930ac-153">Jeśli korzystasz już z hello pakiet administracyjny programu SQL Server, należy użyć tego konta Uruchom jako.</span><span class="sxs-lookup"><span data-stu-id="930ac-153">If you are already using hello SQL Server management pack, you should use that Run As account.</span></span>

#### <a name="tooconfigure-hello-sql-run-as-account-in-hello-operations-console"></a><span data-ttu-id="930ac-154">Witaj tooconfigure konta Uruchom jako SQL w konsoli operacje hello</span><span class="sxs-lookup"><span data-stu-id="930ac-154">tooconfigure hello SQL Run As account in hello Operations console</span></span>
> [!NOTE]
> <span data-ttu-id="930ac-155">Jeśli używasz hello OMS bezpośrednio agenta, a nie hello agenta programu SCOM, pakiet administracyjny hello zawsze działa w kontekście zabezpieczeń hello hello lokalnego konta systemowego.</span><span class="sxs-lookup"><span data-stu-id="930ac-155">If you are using hello OMS direct agent, rather than hello SCOM agent, hello management pack always runs in hello security context of hello Local System account.</span></span> <span data-ttu-id="930ac-156">Pomiń kroki 1 – 5 poniżej i uruchom hello albo próbki T-SQL lub programu Powershell określającego NT AUTHORITY\SYSTEM jako hello nazwy użytkownika.</span><span class="sxs-lookup"><span data-stu-id="930ac-156">Skip steps 1-5 below, and run either hello T-SQL or Powershell sample, specifying NT AUTHORITY\SYSTEM as hello user name.</span></span>
>
>

1. <span data-ttu-id="930ac-157">W programie Operations Manager, otwórz konsolę operacje hello, a następnie kliknij przycisk **administracji**.</span><span class="sxs-lookup"><span data-stu-id="930ac-157">In Operations Manager, open hello Operations console, and then click **Administration**.</span></span>
2. <span data-ttu-id="930ac-158">W obszarze **Konfiguracja Uruchom jako**, kliknij przycisk **profile**i Otwórz **OMS SQL oceny profilu Uruchom jako**.</span><span class="sxs-lookup"><span data-stu-id="930ac-158">Under **Run As Configuration**, click **Profiles**, and open **OMS SQL Assessment Run As Profile**.</span></span>
3. <span data-ttu-id="930ac-159">Na powitania **konta Uruchom jako** kliknij przycisk **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="930ac-159">On hello **Run As Accounts** page, click **Add**.</span></span>
4. <span data-ttu-id="930ac-160">Wybierz konto systemu Windows uruchom jako, które zawiera poświadczenia hello wymagane dla programu SQL Server, lub kliknij przycisk **nowy** toocreate jeden.</span><span class="sxs-lookup"><span data-stu-id="930ac-160">Select a Windows Run As account that contains hello credentials needed for SQL Server, or click **New** toocreate one.</span></span>

   > [!NOTE]
   > <span data-ttu-id="930ac-161">Witaj typ konta Uruchom jako musi być systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="930ac-161">hello Run As account type must be Windows.</span></span> <span data-ttu-id="930ac-162">Witaj konta Uruchom jako musi być również częścią lokalnej grupy administratorów na wszystkich serwerach systemu Windows obsługującego wystąpienia programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="930ac-162">hello Run As account must also be part of Local Administrators group on all Windows Servers hosting SQL Server Instances.</span></span>
   >
   >
5. <span data-ttu-id="930ac-163">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="930ac-163">Click **Save**.</span></span>
6. <span data-ttu-id="930ac-164">Modyfikuj, a następnie wykonaj hello następujące przykładowe T-SQL w każdej wystąpienie programu SQL Server toogrant minimalne uprawnienia wymagane tooRun tooperform jako konto programu SQL do oceny.</span><span class="sxs-lookup"><span data-stu-id="930ac-164">Modify and then execute hello following T-SQL sample on each SQL Server Instance toogrant minimum permissions required tooRun As Account tooperform SQL Assessment.</span></span> <span data-ttu-id="930ac-165">Jednak nie toodo to konieczne, jeśli konto Uruchom jako jest już częścią roli serwera sysadmin hello na wystąpienia programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="930ac-165">However, you don’t need toodo this if a Run As Account is already part of hello sysadmin server role on SQL Server Instances.</span></span>

```
---
    -- Replace <UserName> with hello actual user name being used as Run As Account.
    USE master

    -- Create login for hello user, comment this line if login is already created.
    CREATE LOGIN [<UserName>] FROM WINDOWS

    -- Grant permissions toouser.
    GRANT VIEW SERVER STATE too[<UserName>]
    GRANT VIEW ANY DEFINITION too[<UserName>]
    GRANT VIEW ANY DATABASE too[<UserName>]

    -- Add database user for all hello databases on SQL Server Instance, this is required for connecting tooindividual databases.
    -- NOTE: This command must be run anytime new databases are added tooSQL Server instances.
    EXEC sp_msforeachdb N'USE [?]; CREATE USER [<UserName>] FOR LOGIN [<UserName>];'

```
#### <a name="tooconfigure-hello-sql-run-as-account-using-windows-powershell"></a><span data-ttu-id="930ac-166">Witaj tooconfigure SQL Uruchom jako konta przy użyciu programu Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="930ac-166">tooconfigure hello SQL Run As account using Windows PowerShell</span></span>
<span data-ttu-id="930ac-167">Otwórz okno programu PowerShell i uruchom hello następującego skryptu po zaktualizowaniu z informacjami:</span><span class="sxs-lookup"><span data-stu-id="930ac-167">Open a PowerShell window and run hello following script after you’ve updated it with your information:</span></span>

```

    import-module OperationsManager
    New-SCOMManagementGroupConnection "<your management group name>"

    $profile = Get-SCOMRunAsProfile -DisplayName "OMS SQL Assessment Run As Profile"
    $account = Get-SCOMrunAsAccount | Where-Object {$_.Name -eq "<your run as account name>"}
    Set-SCOMRunAsProfile -Action "Add" -Profile $Profile -Account $Account
```

## <a name="understanding-how-recommendations-are-prioritized"></a><span data-ttu-id="930ac-168">Opis sposobu mają pierwszeństwo zalecenia</span><span class="sxs-lookup"><span data-stu-id="930ac-168">Understanding how recommendations are prioritized</span></span>
<span data-ttu-id="930ac-169">Każdy zalecenia otrzymuje wartość wagi, która identyfikuje hello względnego hello zalecenia.</span><span class="sxs-lookup"><span data-stu-id="930ac-169">Every recommendation made is given a weighting value that identifies hello relative importance of hello recommendation.</span></span> <span data-ttu-id="930ac-170">Wyświetlane są tylko hello 10 najważniejszych zalecenia.</span><span class="sxs-lookup"><span data-stu-id="930ac-170">Only hello ten most important recommendations are shown.</span></span>

### <a name="how-weights-are-calculated"></a><span data-ttu-id="930ac-171">Jak są obliczane wagi</span><span class="sxs-lookup"><span data-stu-id="930ac-171">How weights are calculated</span></span>
<span data-ttu-id="930ac-172">Wagi są wartości zagregowanych oparte na trzech kluczowych czynników:</span><span class="sxs-lookup"><span data-stu-id="930ac-172">Weightings are aggregate values based on three key factors:</span></span>

* <span data-ttu-id="930ac-173">Witaj *prawdopodobieństwo* czy problemu może powodować problemy.</span><span class="sxs-lookup"><span data-stu-id="930ac-173">hello *probability* that an issue identified will cause problems.</span></span> <span data-ttu-id="930ac-174">Większe prawdopodobieństwo oznacza większe ogólny wynik tooa rekomendację hello.</span><span class="sxs-lookup"><span data-stu-id="930ac-174">A higher probability equates tooa larger overall score for hello recommendation.</span></span>
* <span data-ttu-id="930ac-175">Witaj *wpływ* wydania hello w Twojej organizacji, jeśli spowodować problem.</span><span class="sxs-lookup"><span data-stu-id="930ac-175">hello *impact* of hello issue on your organization if it does cause a problem.</span></span> <span data-ttu-id="930ac-176">Większy wpływ oznacza większe ogólny wynik tooa rekomendację hello.</span><span class="sxs-lookup"><span data-stu-id="930ac-176">A higher impact equates tooa larger overall score for hello recommendation.</span></span>
* <span data-ttu-id="930ac-177">Witaj *nakładu* wymagane tooimplement hello zalecenia.</span><span class="sxs-lookup"><span data-stu-id="930ac-177">hello *effort* required tooimplement hello recommendation.</span></span> <span data-ttu-id="930ac-178">Wyższy nakładu pracy oznacza tooa mniejszych ogólny wynik dla hello zalecenia.</span><span class="sxs-lookup"><span data-stu-id="930ac-178">A higher effort equates tooa smaller overall score for hello recommendation.</span></span>

<span data-ttu-id="930ac-179">Witaj wag każde zalecenie jest wyrażona jako procent hello łącznym wynikiem dostępne dla każdego obszaru fokus.</span><span class="sxs-lookup"><span data-stu-id="930ac-179">hello weighting for each recommendation is expressed as a percentage of hello total score available for each focus area.</span></span> <span data-ttu-id="930ac-180">Na przykład jeśli zalecenia w hello zabezpieczeń i zgodności fokus obszaru ma wynik % 5, wdrażanie tego zalecenia spowoduje zwiększenie ogólnej % wynik przez 5 zabezpieczeń i zgodności.</span><span class="sxs-lookup"><span data-stu-id="930ac-180">For example, if a recommendation in hello Security and Compliance focus area has a score of 5%, implementing that recommendation will increase your overall Security and Compliance score by 5%.</span></span>

### <a name="focus-areas"></a><span data-ttu-id="930ac-181">Obszarach zainteresowań</span><span class="sxs-lookup"><span data-stu-id="930ac-181">Focus areas</span></span>
<span data-ttu-id="930ac-182">**Zabezpieczeń i zgodności** — w tym obszarze fokus zawiera zalecenia dotyczące potencjalnego zagrożenia bezpieczeństwa i naruszeń, zasad firmowych i wymagania techniczne, prawne i przepisami zgodności.</span><span class="sxs-lookup"><span data-stu-id="930ac-182">**Security and Compliance** - This focus area shows recommendations for potential security threats and breaches, corporate policies, and technical, legal and regulatory compliance requirements.</span></span>

<span data-ttu-id="930ac-183">**Dostępność i ciągłość prowadzenia działalności biznesowej** — w tym obszarze fokus zawiera zalecenia dotyczące odporności infrastruktury i ochronę biznesowej, dostępności usług.</span><span class="sxs-lookup"><span data-stu-id="930ac-183">**Availability and Business Continuity** - This focus area shows recommendations for service availability, resiliency of your infrastructure, and business protection.</span></span>

<span data-ttu-id="930ac-184">**Wydajność i skalowalność** — ten obszar fokus zawiera zalecenia dotyczące toohelp organizacji infrastruktury IT zwiększania, sprawdź, czy spełnia bieżące wymagania dotyczące wydajności środowiska informatycznego i jest w stanie toorespond toochanging wymaga infrastruktury.</span><span class="sxs-lookup"><span data-stu-id="930ac-184">**Performance and Scalability** - This focus area shows recommendations toohelp your organization's IT infrastructure grow, ensure that your IT environment meets current performance requirements, and is able toorespond toochanging infrastructure needs.</span></span>

<span data-ttu-id="930ac-185">**Uaktualniania, wdrażania i migracji** — toohelp zalecenia dotyczące uaktualniania zawiera ten obszar fokus, migrację i wdrażanie programu SQL Server tooyour istniejącej infrastruktury.</span><span class="sxs-lookup"><span data-stu-id="930ac-185">**Upgrade, Migration and Deployment** - This focus area shows recommendations toohelp you upgrade, migrate, and deploy SQL Server tooyour existing infrastructure.</span></span>

<span data-ttu-id="930ac-186">**Operacje i monitorowanie** — w tym obszarze fokus zawiera zalecenia dotyczące usprawnienia toohelp operacji IT, zaimplementować program prewencyjnej konserwacji i zmaksymalizować wydajność.</span><span class="sxs-lookup"><span data-stu-id="930ac-186">**Operations and Monitoring** - This focus area shows recommendations toohelp streamline your IT operations, implement preventative maintenance, and maximize performance.</span></span>

<span data-ttu-id="930ac-187">**Zarządzanie zmianami i konfiguracją** — w tym obszarze fokus zawiera zalecenia dotyczące toohelp Chroń bieżącą działalność, upewnij się, że zmiany negatywnie nie mają wpływ na infrastrukturę, ustal procedury sterowania zmianami i tootrack i inspekcji konfiguracje systemu.</span><span class="sxs-lookup"><span data-stu-id="930ac-187">**Change and Configuration Management** - This focus area shows recommendations toohelp protect day-to-day operations, ensure that changes don't negatively affect your infrastructure, establish change control procedures, and tootrack and audit system configurations.</span></span>

### <a name="should-you-aim-tooscore-100-in-every-focus-area"></a><span data-ttu-id="930ac-188">Należy należy dążyć tooscore 100% w każdym obszarze fokus?</span><span class="sxs-lookup"><span data-stu-id="930ac-188">Should you aim tooscore 100% in every focus area?</span></span>
<span data-ttu-id="930ac-189">Niekoniecznie.</span><span class="sxs-lookup"><span data-stu-id="930ac-189">Not necessarily.</span></span> <span data-ttu-id="930ac-190">zalecenia Hello są oparte na powitania wiedzy i doświadczeń zdobytych Microsoft inżynierowie między tysięcy wizyt klienta.</span><span class="sxs-lookup"><span data-stu-id="930ac-190">hello recommendations are based on hello knowledge and experiences gained by Microsoft engineers across thousands of customer visits.</span></span> <span data-ttu-id="930ac-191">Jednak nie infrastruktury serwerowe są hello takie same i szczegółowe zalecenia mogą być bardziej lub mniej istotne tooyou.</span><span class="sxs-lookup"><span data-stu-id="930ac-191">However, no two server infrastructures are hello same, and specific recommendations may be more or less relevant tooyou.</span></span> <span data-ttu-id="930ac-192">Na przykład niektóre zalecenia dotyczące zabezpieczeń może być mniej istotne, jeśli maszyny wirtualne nie są uwidocznione toohello Internet.</span><span class="sxs-lookup"><span data-stu-id="930ac-192">For example, some security recommendations might be less relevant if your virtual machines are not exposed toohello Internet.</span></span> <span data-ttu-id="930ac-193">Kilka zaleceń dostępności może być mniej istotne dla usług, które umożliwiają zbieranie danych ad hoc — niski priorytet i raportowania.</span><span class="sxs-lookup"><span data-stu-id="930ac-193">Some availability recommendations may be less relevant for services that provide low priority ad hoc data collection and reporting.</span></span> <span data-ttu-id="930ac-194">Problemy, które są ważne tooa dojrzałe firm może być mniej ważne tooa rozruchu.</span><span class="sxs-lookup"><span data-stu-id="930ac-194">Issues that are important tooa mature business may be less important tooa start-up.</span></span> <span data-ttu-id="930ac-195">Może mają tooidentify obszarach zainteresowań, które są zebranych i przyjrzyj się jak zmienić wyniki wraz z upływem czasu.</span><span class="sxs-lookup"><span data-stu-id="930ac-195">You may want tooidentify which focus areas are your priorities and then look at how your scores change over time.</span></span>

<span data-ttu-id="930ac-196">Każdy zalecenie obejmuje wskazówek dotyczących Dlaczego ważne jest.</span><span class="sxs-lookup"><span data-stu-id="930ac-196">Every recommendation includes guidance about why it is important.</span></span> <span data-ttu-id="930ac-197">Należy użyć tego tooevaluate wskazówki czy wdrażanie zalecenie hello jest odpowiednie dla Ciebie, charakter hello IT usługi i hello potrzeby biznesowe danej organizacji.</span><span class="sxs-lookup"><span data-stu-id="930ac-197">You should use this guidance tooevaluate whether implementing hello recommendation is appropriate for you, given hello nature of your IT services and hello business needs of your organization.</span></span>

## <a name="use-assessment-focus-area-recommendations"></a><span data-ttu-id="930ac-198">Użyj zaleceń obszaru fokus oceny</span><span class="sxs-lookup"><span data-stu-id="930ac-198">Use assessment focus area recommendations</span></span>
<span data-ttu-id="930ac-199">Zanim użyjesz rozwiązanie do oceny w pakietu OMS musi mieć zainstalowane oprogramowanie hello.</span><span class="sxs-lookup"><span data-stu-id="930ac-199">Before you can use an assessment solution in OMS, you must have hello solution installed.</span></span> <span data-ttu-id="930ac-200">tooread więcej na temat instalowania rozwiązań, zobacz [rozwiązań analizy dzienników dodać hello galerii rozwiązań](log-analytics-add-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="930ac-200">tooread more about installing solutions, see [Add Log Analytics solutions from hello Solutions Gallery](log-analytics-add-solutions.md).</span></span> <span data-ttu-id="930ac-201">Po jego zainstalowaniu, można wyświetlić podsumowanie hello zalecenia za pomocą kafelka oceny SQL hello na stronie Przegląd hello OMS.</span><span class="sxs-lookup"><span data-stu-id="930ac-201">After it is installed, you can view hello summary of recommendations by using hello SQL Assessment tile on hello Overview page in OMS.</span></span>

<span data-ttu-id="930ac-202">Witaj w widoku Podsumowanie oceny zgodności dla Twojej infrastruktury, a następnie wejdź do zalecenia.</span><span class="sxs-lookup"><span data-stu-id="930ac-202">View hello summarized compliance assessments for your infrastructure and then drill-into recommendations.</span></span>

### <a name="tooview-recommendations-for-a-focus-area-and-take-corrective-action"></a><span data-ttu-id="930ac-203">tooview zalecenia dotyczące fokus obszaru i podejmij akcję korekcyjną</span><span class="sxs-lookup"><span data-stu-id="930ac-203">tooview recommendations for a focus area and take corrective action</span></span>
1. <span data-ttu-id="930ac-204">Na powitania **omówienie** kliknij przycisk hello **oceny SQL** kafelka.</span><span class="sxs-lookup"><span data-stu-id="930ac-204">On hello **Overview** page, click hello **SQL Assessment** tile.</span></span>
2. <span data-ttu-id="930ac-205">Na powitania **oceny SQL** strony, przejrzyj hello informacje podsumowania w jednym z bloków obszaru fokus hello, a następnie kliknij jedną tooview zalecenia dla tego obszaru fokus.</span><span class="sxs-lookup"><span data-stu-id="930ac-205">On hello **SQL Assessment** page, review hello summary information in one of hello focus area blades and then click one tooview recommendations for that focus area.</span></span>
3. <span data-ttu-id="930ac-206">Na dowolnym hello fokus obszaru stron można wyświetlić hello priorytety zalecenia dla danego środowiska.</span><span class="sxs-lookup"><span data-stu-id="930ac-206">On any of hello focus area pages, you can view hello prioritized recommendations made for your environment.</span></span> <span data-ttu-id="930ac-207">Kliknij zalecenie, w obszarze **dotyczy obiektów** tooview szczegółowych informacji o Dlaczego hello tworzone są zalecenia.</span><span class="sxs-lookup"><span data-stu-id="930ac-207">Click a recommendation under **Affected Objects** tooview details about why hello recommendation is made.</span></span>  
    <span data-ttu-id="930ac-208">![Obraz zalecenia oceny SQL](./media/log-analytics-sql-assessment/sql-assess-focus.png)</span><span class="sxs-lookup"><span data-stu-id="930ac-208">![image of SQL Assessment recommendations](./media/log-analytics-sql-assessment/sql-assess-focus.png)</span></span>
4. <span data-ttu-id="930ac-209">Należy wykonać działania naprawcze sugerowane w **sugerowanych akcji**.</span><span class="sxs-lookup"><span data-stu-id="930ac-209">You can take corrective actions suggested in **Suggested Actions**.</span></span> <span data-ttu-id="930ac-210">Gdy element hello został rozwiązany, ocen nowsze zarejestruje które zalecane akcje zostały pobrane i zwiększa wynik zgodności.</span><span class="sxs-lookup"><span data-stu-id="930ac-210">When hello item has been addressed, later assessments will record that recommended actions were taken and your compliance score will increase.</span></span> <span data-ttu-id="930ac-211">Poprawione elementy są wyświetlane jako **przekazany obiektów**.</span><span class="sxs-lookup"><span data-stu-id="930ac-211">Corrected items appear as **Passed Objects**.</span></span>

## <a name="ignore-recommendations"></a><span data-ttu-id="930ac-212">Ignoruj zalecenia</span><span class="sxs-lookup"><span data-stu-id="930ac-212">Ignore recommendations</span></span>
<span data-ttu-id="930ac-213">Jeśli masz zaleceń, które mają tooignore, można utworzyć plik tekstowy, który będzie używany przez OMS tooprevent zaleceń znajdujących się w wynikach oceny.</span><span class="sxs-lookup"><span data-stu-id="930ac-213">If you have recommendations that you want tooignore, you can create a text file that OMS will use tooprevent recommendations from appearing in your assessment results.</span></span>

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

### <a name="tooidentify-recommendations-that-you-will-ignore"></a><span data-ttu-id="930ac-214">zalecenia dotyczące tooidentify, które będzie ignorować</span><span class="sxs-lookup"><span data-stu-id="930ac-214">tooidentify recommendations that you will ignore</span></span>
1. <span data-ttu-id="930ac-215">Zaloguj się w obszarze roboczym tooyour i Otwórz dziennik wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="930ac-215">Sign in tooyour workspace and open Log Search.</span></span> <span data-ttu-id="930ac-216">Użyj hello następujące zalecenia toolist zapytania, które nie powiodły się na komputerach w danym środowisku.</span><span class="sxs-lookup"><span data-stu-id="930ac-216">Use hello following query toolist recommendations that have failed for computers in your environment.</span></span>

   ```
   Type=SQLAssessmentRecommendation RecommendationResult=Failed | select  Computer, RecommendationId, Recommendation | sort  Computer
   ```

   <span data-ttu-id="930ac-217">Poniżej przedstawiono zrzut ekranu przedstawiający hello dziennik wyszukiwania: ![nie powiodło się zalecenia](./media/log-analytics-sql-assessment/sql-assess-failed-recommendations.png)</span><span class="sxs-lookup"><span data-stu-id="930ac-217">Here's a screen shot showing hello Log Search query: ![failed recommendations](./media/log-analytics-sql-assessment/sql-assess-failed-recommendations.png)</span></span>
2. <span data-ttu-id="930ac-218">Wybierz, które mają tooignore zalecenia.</span><span class="sxs-lookup"><span data-stu-id="930ac-218">Choose recommendations that you want tooignore.</span></span> <span data-ttu-id="930ac-219">Użyjesz wartości hello RecommendationId w następnej procedurze hello.</span><span class="sxs-lookup"><span data-stu-id="930ac-219">You’ll use hello values for RecommendationId in hello next procedure.</span></span>

### <a name="toocreate-and-use-an-ignorerecommendationstxt-text-file"></a><span data-ttu-id="930ac-220">toocreate i użyj pliku tekstowego IgnoreRecommendations.txt</span><span class="sxs-lookup"><span data-stu-id="930ac-220">toocreate and use an IgnoreRecommendations.txt text file</span></span>
1. <span data-ttu-id="930ac-221">Utwórz plik o nazwie IgnoreRecommendations.txt.</span><span class="sxs-lookup"><span data-stu-id="930ac-221">Create a file named IgnoreRecommendations.txt.</span></span>
2. <span data-ttu-id="930ac-222">Wklej lub wpisz każdego RecommendationId dla każde zalecenie ma tooignore OMS w osobnym wierszu, a następnie zapisz i zamknij plik hello.</span><span class="sxs-lookup"><span data-stu-id="930ac-222">Paste or type each RecommendationId for each recommendation that you want OMS tooignore on a separate line and then save and close hello file.</span></span>
3. <span data-ttu-id="930ac-223">Umieść plik hello w hello następującego folderu na każdym komputerze miejscu zalecenia tooignore OMS.</span><span class="sxs-lookup"><span data-stu-id="930ac-223">Put hello file in hello following folder on each computer where you want OMS tooignore recommendations.</span></span>
   * <span data-ttu-id="930ac-224">Na komputerach z usługą Microsoft Monitoring Agent (połączony bezpośrednio lub za pośrednictwem programu Operations Manager) - hello *SystemDrive*: \Program Files\Microsoft Agent\Agent monitorowania</span><span class="sxs-lookup"><span data-stu-id="930ac-224">On computers with hello Microsoft Monitoring Agent (connected directly or through Operations Manager) - *SystemDrive*:\Program Files\Microsoft Monitoring Agent\Agent</span></span>
   * <span data-ttu-id="930ac-225">Na serwerze zarządzania programu Operations Manager hello - *SystemDrive*: System Center 2012 R2\Operations Manager\Server \Program Files\Microsoft</span><span class="sxs-lookup"><span data-stu-id="930ac-225">On hello Operations Manager management server - *SystemDrive*:\Program Files\Microsoft System Center 2012 R2\Operations Manager\Server</span></span>

### <a name="tooverify-that-recommendations-are-ignored"></a><span data-ttu-id="930ac-226">tooverify, że zalecenia są ignorowane</span><span class="sxs-lookup"><span data-stu-id="930ac-226">tooverify that recommendations are ignored</span></span>
1. <span data-ttu-id="930ac-227">Po uruchomieniu hello następnej zaplanowanej oceny domyślnie co 7 dni hello określone zalecenia są oznaczone ignorowany i nie będą wyświetlane na pulpicie nawigacyjnym oceny hello.</span><span class="sxs-lookup"><span data-stu-id="930ac-227">After hello next scheduled assessment runs, by default every 7 days, hello specified recommendations are marked Ignored and will not appear on hello assessment dashboard.</span></span>
2. <span data-ttu-id="930ac-228">Możesz użyć powitania po toolist zapytania wyszukiwania dziennika wszystkie zalecenia hello ignorowane.</span><span class="sxs-lookup"><span data-stu-id="930ac-228">You can use hello following Log Search queries toolist all hello ignored recommendations.</span></span>

   ```
   Type=SQLAssessmentRecommendation RecommendationResult=Ignored | select  Computer, RecommendationId, Recommendation | sort  Computer
   ```
3. <span data-ttu-id="930ac-229">Jeśli później zdecydujesz, które mają toosee zignorowane zalecenia, Usuń wszystkie pliki IgnoreRecommendations.txt lub RecommendationIDs można usunąć z nich.</span><span class="sxs-lookup"><span data-stu-id="930ac-229">If you decide later that you want toosee ignored recommendations, remove any IgnoreRecommendations.txt files, or you can remove RecommendationIDs from them.</span></span>

## <a name="sql-assessment-solution-faq"></a><span data-ttu-id="930ac-230">Rozwiązanie do oceny SQL — często zadawane pytania</span><span class="sxs-lookup"><span data-stu-id="930ac-230">SQL Assessment solution FAQ</span></span>
<span data-ttu-id="930ac-231">*Częstotliwość oceny, czy działa?*</span><span class="sxs-lookup"><span data-stu-id="930ac-231">*How often does an assessment run?*</span></span>

* <span data-ttu-id="930ac-232">Ocena Hello jest uruchamiane co 7 dni.</span><span class="sxs-lookup"><span data-stu-id="930ac-232">hello assessment runs every 7 days.</span></span>

<span data-ttu-id="930ac-233">*Czy istnieje sposób tooconfigure częstotliwość oceny hello działa?*</span><span class="sxs-lookup"><span data-stu-id="930ac-233">*Is there a way tooconfigure how often hello assessment runs?*</span></span>

* <span data-ttu-id="930ac-234">Nie w tej chwili.</span><span class="sxs-lookup"><span data-stu-id="930ac-234">Not at this time.</span></span>

<span data-ttu-id="930ac-235">*Jeśli inny serwer zostanie odnaleziony po hello rozwiązanie SQL do oceny zostały dodane, zostanie on oceniane?*</span><span class="sxs-lookup"><span data-stu-id="930ac-235">*If another server is discovered after I’ve added hello SQL assessment solution, will it be assessed?*</span></span>

* <span data-ttu-id="930ac-236">Tak, gdy okaże się, że jest oceniane z następnie, co 7 dni.</span><span class="sxs-lookup"><span data-stu-id="930ac-236">Yes, once it is discovered it is assessed from then on, every 7 days.</span></span>

<span data-ttu-id="930ac-237">*Jeśli serwer jest likwidowany, gdy zostanie ono zostać usunięte z hello oceny?*</span><span class="sxs-lookup"><span data-stu-id="930ac-237">*If a server is decommissioned, when will it be removed from hello assessment?*</span></span>

* <span data-ttu-id="930ac-238">Jeśli serwer nie przedstawi danych do 3 tygodni, zostanie ono usunięte.</span><span class="sxs-lookup"><span data-stu-id="930ac-238">If a server does not submit data for 3 weeks, it is removed.</span></span>

<span data-ttu-id="930ac-239">*Co to jest nazwa hello procesu hello hello zbierania danych?*</span><span class="sxs-lookup"><span data-stu-id="930ac-239">*What is hello name of hello process that does hello data collection?*</span></span>

* <span data-ttu-id="930ac-240">AdvisorAssessment.exe</span><span class="sxs-lookup"><span data-stu-id="930ac-240">AdvisorAssessment.exe</span></span>

<span data-ttu-id="930ac-241">*Jak długo trwa toobe dane zbierane?*</span><span class="sxs-lookup"><span data-stu-id="930ac-241">*How long does it take for data toobe collected?*</span></span>

* <span data-ttu-id="930ac-242">Hello zbierania danych rzeczywistych na powitania serwera trwa około 1 godziny.</span><span class="sxs-lookup"><span data-stu-id="930ac-242">hello actual data collection on hello server takes about 1 hour.</span></span> <span data-ttu-id="930ac-243">Może trwać dłużej na serwerach, które mają wiele wystąpień programu SQL lub bazy danych.</span><span class="sxs-lookup"><span data-stu-id="930ac-243">It may take longer on servers that have a large number of SQL instances or databases.</span></span>

<span data-ttu-id="930ac-244">*Jakiego typu dane są zbierane?*</span><span class="sxs-lookup"><span data-stu-id="930ac-244">*What type of data is collected?*</span></span>

* <span data-ttu-id="930ac-245">zbierane są następujące typy danych Hello:</span><span class="sxs-lookup"><span data-stu-id="930ac-245">hello following types of data are collected:</span></span>
  * <span data-ttu-id="930ac-246">USŁUGI WMI</span><span class="sxs-lookup"><span data-stu-id="930ac-246">WMI</span></span>
  * <span data-ttu-id="930ac-247">Rejestru</span><span class="sxs-lookup"><span data-stu-id="930ac-247">Registry</span></span>
  * <span data-ttu-id="930ac-248">Liczniki wydajności</span><span class="sxs-lookup"><span data-stu-id="930ac-248">Performance counters</span></span>
  * <span data-ttu-id="930ac-249">SQL dynamicznych widoków zarządzania (DMV).</span><span class="sxs-lookup"><span data-stu-id="930ac-249">SQL dynamic management views (DMV).</span></span>

<span data-ttu-id="930ac-250">*Istnieje już tooconfigure sposób podczas zbierania danych?*</span><span class="sxs-lookup"><span data-stu-id="930ac-250">*Is there a way tooconfigure when data is collected?*</span></span>

* <span data-ttu-id="930ac-251">Nie w tej chwili.</span><span class="sxs-lookup"><span data-stu-id="930ac-251">Not at this time.</span></span>

<span data-ttu-id="930ac-252">*Dlaczego ma tooconfigure konto Uruchom jako?*</span><span class="sxs-lookup"><span data-stu-id="930ac-252">*Why do I have tooconfigure a Run As Account?*</span></span>

* <span data-ttu-id="930ac-253">Dla programu SQL Server są uruchamiane niewielkiej liczby zapytania SQL.</span><span class="sxs-lookup"><span data-stu-id="930ac-253">For SQL Server, a small number of SQL queries are run.</span></span> <span data-ttu-id="930ac-254">Aby je toorun, konto Uruchom jako z tooSQL uprawnienia VIEW SERVER STATE musi być używany.</span><span class="sxs-lookup"><span data-stu-id="930ac-254">In order for them toorun, a Run As Account with VIEW SERVER STATE permissions tooSQL must be used.</span></span>  <span data-ttu-id="930ac-255">Ponadto w kolejności tooquery WMI, wymagane są poświadczenia administratora lokalnego.</span><span class="sxs-lookup"><span data-stu-id="930ac-255">In addition, in order tooquery WMI, local administrator credentials are required.</span></span>

<span data-ttu-id="930ac-256">*Dlaczego są wyświetlane tylko zalecenia 10 pierwszych hello?*</span><span class="sxs-lookup"><span data-stu-id="930ac-256">*Why display only hello top 10 recommendations?*</span></span>

* <span data-ttu-id="930ac-257">Zamiast daje utrudnione kompletnej zadań, zaleca się skupić się na najpierw adresowania hello priorytety zalecenia.</span><span class="sxs-lookup"><span data-stu-id="930ac-257">Instead of giving you an exhaustive overwhelming list of tasks, we recommend that you focus on addressing hello prioritized recommendations first.</span></span> <span data-ttu-id="930ac-258">Po adresu im dodatkowe zalecenia staną się dostępne.</span><span class="sxs-lookup"><span data-stu-id="930ac-258">After you address them, additional recommendations will become available.</span></span> <span data-ttu-id="930ac-259">Jeśli wolisz toosee hello szczegółową listę, można wyświetlić wszystkie zalecenia w wyszukiwaniu hello OMS dziennika.</span><span class="sxs-lookup"><span data-stu-id="930ac-259">If you prefer toosee hello detailed list, you can view all recommendations using hello OMS log search.</span></span>

<span data-ttu-id="930ac-260">*Istnieje już tooignore sposób zalecenia?*</span><span class="sxs-lookup"><span data-stu-id="930ac-260">*Is there a way tooignore a recommendation?*</span></span>

* <span data-ttu-id="930ac-261">Tak, zobacz [zignorowanie zalecenia](#ignore-recommendations) powyższej sekcji.</span><span class="sxs-lookup"><span data-stu-id="930ac-261">Yes, see [Ignore recommendations](#ignore-recommendations) section above.</span></span>

## <a name="next-steps"></a><span data-ttu-id="930ac-262">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="930ac-262">Next steps</span></span>
* <span data-ttu-id="930ac-263">[Wyszukaj dzienniki](log-analytics-log-searches.md) tooview szczegółowych danych SQL do oceny i zalecenia.</span><span class="sxs-lookup"><span data-stu-id="930ac-263">[Search logs](log-analytics-log-searches.md) tooview detailed SQL Assessment data and recommendations.</span></span>
