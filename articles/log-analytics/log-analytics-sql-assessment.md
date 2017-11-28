---
title: "Optymalizuj środowisko programu SQL Server z Azure Log Analytics | Dokumentacja firmy Microsoft"
description: "Z usługi Analiza dzienników Azure rozwiązanie do oceny SQL służy do oceny ryzyka i kondycji środowisk programu SQL server w regularnych odstępach czasu."
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
ms.openlocfilehash: d2aed3315fe60ace46dfb4176dc13aa417257b0c
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="optimize-your-sql-server-environment-with-the-sql-assessment-solution-in-log-analytics"></a><span data-ttu-id="217b7-103">Optymalizuj środowisko programu SQL Server z rozwiązaniem oceny SQL w analizy dzienników</span><span class="sxs-lookup"><span data-stu-id="217b7-103">Optimize your SQL Server environment with the SQL Assessment solution in Log Analytics</span></span>

![Symbol oceny SQL](./media/log-analytics-sql-assessment/sql-assessment-symbol.png)

<span data-ttu-id="217b7-105">Rozwiązanie do oceny SQL można użyć do oceny ryzyka i kondycji środowisk serwera w regularnych odstępach czasu.</span><span class="sxs-lookup"><span data-stu-id="217b7-105">You can use the SQL Assessment solution to assess the risk and health of your server environments on a regular interval.</span></span> <span data-ttu-id="217b7-106">Ten artykuł pomoże Ci zainstalować rozwiązania, dzięki czemu można wykonać działania naprawcze potencjalnych problemów.</span><span class="sxs-lookup"><span data-stu-id="217b7-106">This article will help you install the solution so that you can take corrective actions for potential problems.</span></span>

<span data-ttu-id="217b7-107">To rozwiązanie zapewnia priorytetową listą zalecenia dotyczące infrastruktury serwera wdrożone.</span><span class="sxs-lookup"><span data-stu-id="217b7-107">This solution provides a prioritized list of recommendations specific to your deployed server infrastructure.</span></span> <span data-ttu-id="217b7-108">Zalecenia są podzielone na sześć obszarów fokus, które pomagają w szybkim świadomość ryzyka i podjęcia działań naprawczych.</span><span class="sxs-lookup"><span data-stu-id="217b7-108">The recommendations are categorized across six focus areas which help you quickly understand the risk and take corrective action.</span></span>

<span data-ttu-id="217b7-109">Zalecenia są oparte na wiedzy i doświadczenia przez pracownicy firmy Microsoft z tysięcy wizyt klienta.</span><span class="sxs-lookup"><span data-stu-id="217b7-109">The recommendations made are based on the knowledge and experience gained by Microsoft engineers from thousands of customer visits.</span></span> <span data-ttu-id="217b7-110">Każde zalecenie znajdują się wskazówki dotyczące przyczyny problemu może być uwzględniana i implementowania sugerowane zmiany.</span><span class="sxs-lookup"><span data-stu-id="217b7-110">Each recommendation provides guidance about why an issue might matter to you and how to implement the suggested changes.</span></span>

<span data-ttu-id="217b7-111">Można wybrać obszarach zainteresowań, które są najbardziej ważne dla organizacji i śledzić postęp w kierunku uruchomionym środowiskiem ryzyka bezpłatne i działa prawidłowo.</span><span class="sxs-lookup"><span data-stu-id="217b7-111">You can choose focus areas that are most important to your organization and track your progress toward running a risk free and healthy environment.</span></span>

<span data-ttu-id="217b7-112">Po dodaniu rozwiązania i ocenę jest zakończone, podsumowanie informacji o obszarach zainteresowań jest wyświetlany na **oceny SQL** pulpitu nawigacyjnego dla infrastruktury w danym środowisku.</span><span class="sxs-lookup"><span data-stu-id="217b7-112">After you've added the solution and an assessment is completed, summary information for focus areas is shown on the **SQL Assessment** dashboard for the infrastructure in your environment.</span></span> <span data-ttu-id="217b7-113">W poniższych sekcjach opisano sposób użyć informacji na temat **oceny SQL** pulpitu nawigacyjnego, gdzie można przeglądać i wykonaj zalecane akcje dotyczące infrastruktury serwera SQL.</span><span class="sxs-lookup"><span data-stu-id="217b7-113">The following sections describe how to use the information on the **SQL Assessment** dashboard, where you can view and then take recommended actions for your SQL server infrastructure.</span></span>

![Obraz kafelka oceny SQL](./media/log-analytics-sql-assessment/sql-assess-tile.png)

![Obraz pulpitu nawigacyjnego oceny SQL](./media/log-analytics-sql-assessment/sql-assess-dash.png)

## <a name="installing-and-configuring-the-solution"></a><span data-ttu-id="217b7-116">Instalowanie i konfigurowanie rozwiązania</span><span class="sxs-lookup"><span data-stu-id="217b7-116">Installing and configuring the solution</span></span>
<span data-ttu-id="217b7-117">Ocena SQL współpracuje z wszystkich aktualnie obsługiwanych wersjach programu SQL Server w wersjach Standard, Developer i Enterprise.</span><span class="sxs-lookup"><span data-stu-id="217b7-117">SQL Assessment works with all currently supported versions of SQL Server for the Standard, Developer, and Enterprise editions.</span></span>

<span data-ttu-id="217b7-118">Skorzystaj z poniższych informacji, aby zainstalować i skonfigurować rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="217b7-118">Use the following information to install and configure the solution.</span></span>

* <span data-ttu-id="217b7-119">Agenci musi być zainstalowany na serwerach, które mają zainstalowany program SQL Server.</span><span class="sxs-lookup"><span data-stu-id="217b7-119">Agents must be installed on servers that have SQL Server installed.</span></span>
* <span data-ttu-id="217b7-120">Rozwiązanie do oceny SQL wymaga obsługiwanej wersji programu .NET Framework 4 zainstalowane na każdym komputerze, na którym agent pakietu OMS.</span><span class="sxs-lookup"><span data-stu-id="217b7-120">The SQL Assessment solution requires a supported version of .NET Framework 4 installed on each computer that has an OMS agent.</span></span>
* <span data-ttu-id="217b7-121">Aby można było zainstalować rozwiązania, użytkownik musi być administratorem lub współpracownikiem subskrypcji platformy Azure przy użyciu portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="217b7-121">In order to install the solution, the user must be an administrator or contributor to the Azure subscription when using the Azure portal.</span></span> <span data-ttu-id="217b7-122">Ponadto użytkownik musi być członkiem roli administratora lub współautora obszaru roboczego pakietu OMS w portalu pakietu OMS.</span><span class="sxs-lookup"><span data-stu-id="217b7-122">In addition, the user must be a member of the OMS workspace contributor or administrator role in the OMS portal.</span></span>
* <span data-ttu-id="217b7-123">Za pomocą agenta programu Operations Manager z oceną SQL, należy użyć konta Run-As menedżera operacji.</span><span class="sxs-lookup"><span data-stu-id="217b7-123">When using the Operations Manager agent with SQL Assessment, you'll need to use an Operations Manager Run-As account.</span></span> <span data-ttu-id="217b7-124">Zobacz [konta programu Operations Manager, Uruchom jako dla OMS](#operations-manager-run-as-accounts-for-oms) poniżej Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="217b7-124">See [Operations Manager run-as accounts for OMS](#operations-manager-run-as-accounts-for-oms) below for more information.</span></span>

  > [!NOTE]
  > <span data-ttu-id="217b7-125">MMA agent nie obsługuje programu Operations Manager Run-As kont.</span><span class="sxs-lookup"><span data-stu-id="217b7-125">The MMA agent does not support Operations Manager Run-As accounts.</span></span>
  >
  >
* <span data-ttu-id="217b7-126">Dodaj rozwiązanie do oceny SQL na obszar roboczy OMS zastosowanie procesu opisanego w [rozwiązań dodać analizy dzienników z galerii rozwiązań](log-analytics-add-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="217b7-126">Add the SQL Assessment solution to your OMS workspace using the process described in [Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md).</span></span> <span data-ttu-id="217b7-127">Nie są wymagane żadne dalsze czynności konfiguracyjne.</span><span class="sxs-lookup"><span data-stu-id="217b7-127">There is no further configuration required.</span></span>

> [!NOTE]
> <span data-ttu-id="217b7-128">Po dodaniu rozwiązania, plik AdvisorAssessment.exe jest dodawany do serwerów z agentami.</span><span class="sxs-lookup"><span data-stu-id="217b7-128">After you've added the solution, the AdvisorAssessment.exe file is added to servers with agents.</span></span> <span data-ttu-id="217b7-129">Dane konfiguracji jest do odczytu i następnie wysyłane do usługę w chmurze do przetwarzania.</span><span class="sxs-lookup"><span data-stu-id="217b7-129">Configuration data is read and then sent to the OMS service in the cloud for processing.</span></span> <span data-ttu-id="217b7-130">Logika jest stosowany do odebranych danych i usługi w chmurze rejestruje dane.</span><span class="sxs-lookup"><span data-stu-id="217b7-130">Logic is applied to the received data and the cloud service records the data.</span></span>

## <a name="sql-assessment-data-collection-details"></a><span data-ttu-id="217b7-131">Szczegóły pobierania danych SQL do oceny</span><span class="sxs-lookup"><span data-stu-id="217b7-131">SQL Assessment data collection details</span></span>
<span data-ttu-id="217b7-132">Ocena SQL służy do zbierania danych usługi WMI, dane rejestru dane dotyczące wydajności i wyników widoku dynamicznego zarządzania programu SQL Server za pomocą agentów, które mają włączone.</span><span class="sxs-lookup"><span data-stu-id="217b7-132">SQL Assessment collects WMI data, registry data, performance data, and SQL Server dynamic management view results using the agents that you have enabled.</span></span>

<span data-ttu-id="217b7-133">W poniższej tabeli przedstawiono metody zbierania danych dla agentów, czy Operations Manager (SCOM) jest wymagany i jak często dane są zbierane przez agenta.</span><span class="sxs-lookup"><span data-stu-id="217b7-133">The following table shows data collection methods for agents, whether Operations Manager (SCOM) is required, and how often data is collected by an agent.</span></span>

| <span data-ttu-id="217b7-134">Platformy</span><span class="sxs-lookup"><span data-stu-id="217b7-134">platform</span></span> | <span data-ttu-id="217b7-135">Bezpośrednie agenta</span><span class="sxs-lookup"><span data-stu-id="217b7-135">Direct Agent</span></span> | <span data-ttu-id="217b7-136">Agenta programu SCOM</span><span class="sxs-lookup"><span data-stu-id="217b7-136">SCOM agent</span></span> | <span data-ttu-id="217b7-137">Azure Storage</span><span class="sxs-lookup"><span data-stu-id="217b7-137">Azure Storage</span></span> | <span data-ttu-id="217b7-138">SCOM wymagane?</span><span class="sxs-lookup"><span data-stu-id="217b7-138">SCOM required?</span></span> | <span data-ttu-id="217b7-139">Dane agenta programu SCOM wysyłane za pośrednictwem grupy zarządzania</span><span class="sxs-lookup"><span data-stu-id="217b7-139">SCOM agent data sent via management group</span></span> | <span data-ttu-id="217b7-140">Częstotliwość kolekcji</span><span class="sxs-lookup"><span data-stu-id="217b7-140">collection frequency</span></span> |
| --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="217b7-141">Windows</span><span class="sxs-lookup"><span data-stu-id="217b7-141">Windows</span></span> | <span data-ttu-id="217b7-142">&#8226;</span><span class="sxs-lookup"><span data-stu-id="217b7-142">&#8226;</span></span> | <span data-ttu-id="217b7-143">&#8226;</span><span class="sxs-lookup"><span data-stu-id="217b7-143">&#8226;</span></span> |  |  | <span data-ttu-id="217b7-144">&#8226;</span><span class="sxs-lookup"><span data-stu-id="217b7-144">&#8226;</span></span> |<span data-ttu-id="217b7-145">7 dni</span><span class="sxs-lookup"><span data-stu-id="217b7-145">7 days</span></span> |

## <a name="operations-manager-run-as-accounts-for-oms"></a><span data-ttu-id="217b7-146">Uruchom jako konta programu Operations Manager dla OMS</span><span class="sxs-lookup"><span data-stu-id="217b7-146">Operations Manager run-as accounts for OMS</span></span>
<span data-ttu-id="217b7-147">Analiza dzienników w OMS używa grupy zarządzania i agent programu Operations Manager w celu wysyłają i zbierają dane z usługą OMS.</span><span class="sxs-lookup"><span data-stu-id="217b7-147">Log Analytics in OMS uses the Operations Manager agent and management group to collect and send data to the OMS service.</span></span> <span data-ttu-id="217b7-148">Kompilacje OMS na pakiety administracyjne dla obciążeń w celu zapewnienia wartość — Dodawanie usług.</span><span class="sxs-lookup"><span data-stu-id="217b7-148">OMS builds upon management packs for workloads to provide value-add services.</span></span> <span data-ttu-id="217b7-149">Poszczególnych obciążeń wymaga uprawnień specyficznego dla obciążenia uruchomione pakiety administracyjne w innym kontekście zabezpieczeń, takie jak konto domeny.</span><span class="sxs-lookup"><span data-stu-id="217b7-149">Each workload requires workload-specific privileges to run management packs in a different security context, such as a domain account.</span></span> <span data-ttu-id="217b7-150">Musisz podać poświadczenia informacji przez skonfigurowanie konta Operations Manager uruchom jako.</span><span class="sxs-lookup"><span data-stu-id="217b7-150">You need to provide credential information by configuring an Operations Manager Run As account.</span></span>

<span data-ttu-id="217b7-151">Skorzystaj z poniższych informacji, aby ustawić konto Uruchom jako programu Operations Manager w celu oceny SQL.</span><span class="sxs-lookup"><span data-stu-id="217b7-151">Use the following information to set the Operations Manager run-as account for SQL Assessment.</span></span>

### <a name="set-the-run-as-account-for-sql-assessment"></a><span data-ttu-id="217b7-152">Ustaw konto Uruchom jako w celu oceny SQL</span><span class="sxs-lookup"><span data-stu-id="217b7-152">Set the Run As account for SQL assessment</span></span>
 <span data-ttu-id="217b7-153">Jeśli korzystasz już z pakietu administracyjnego programu SQL Server, należy użyć tego konta Uruchom jako.</span><span class="sxs-lookup"><span data-stu-id="217b7-153">If you are already using the SQL Server management pack, you should use that Run As account.</span></span>

#### <a name="to-configure-the-sql-run-as-account-in-the-operations-console"></a><span data-ttu-id="217b7-154">Aby skonfigurować konto Uruchom jako SQL w konsoli operacje</span><span class="sxs-lookup"><span data-stu-id="217b7-154">To configure the SQL Run As account in the Operations console</span></span>
> [!NOTE]
> <span data-ttu-id="217b7-155">Jeśli używasz bezpośredniej agent pakietu OMS zamiast agenta programu SCOM, pakiet zarządzania jest zawsze uruchamiany w kontekście zabezpieczeń konta systemu lokalnego.</span><span class="sxs-lookup"><span data-stu-id="217b7-155">If you are using the OMS direct agent, rather than the SCOM agent, the management pack always runs in the security context of the Local System account.</span></span> <span data-ttu-id="217b7-156">Pomiń kroki od 1 do 5 poniżej, a następnie uruchomić T-SQL lub próbki programu Powershell, określając NT AUTHORITY\SYSTEM z nazwą użytkownika.</span><span class="sxs-lookup"><span data-stu-id="217b7-156">Skip steps 1-5 below, and run either the T-SQL or Powershell sample, specifying NT AUTHORITY\SYSTEM as the user name.</span></span>
>
>

1. <span data-ttu-id="217b7-157">W programie Operations Manager, otwórz konsolę operacje, a następnie kliknij przycisk **administracji**.</span><span class="sxs-lookup"><span data-stu-id="217b7-157">In Operations Manager, open the Operations console, and then click **Administration**.</span></span>
2. <span data-ttu-id="217b7-158">W obszarze **Konfiguracja Uruchom jako**, kliknij przycisk **profile**i Otwórz **OMS SQL oceny profilu Uruchom jako**.</span><span class="sxs-lookup"><span data-stu-id="217b7-158">Under **Run As Configuration**, click **Profiles**, and open **OMS SQL Assessment Run As Profile**.</span></span>
3. <span data-ttu-id="217b7-159">Na **konta Uruchom jako** kliknij przycisk **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="217b7-159">On the **Run As Accounts** page, click **Add**.</span></span>
4. <span data-ttu-id="217b7-160">Wybierz konto systemu Windows uruchom jako, które zawiera poświadczenia wymagane dla programu SQL Server, lub kliknij przycisk **nowy** go utworzyć.</span><span class="sxs-lookup"><span data-stu-id="217b7-160">Select a Windows Run As account that contains the credentials needed for SQL Server, or click **New** to create one.</span></span>

   > [!NOTE]
   > <span data-ttu-id="217b7-161">Typ konta Uruchom jako musi być systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="217b7-161">The Run As account type must be Windows.</span></span> <span data-ttu-id="217b7-162">Konta Uruchom jako musi także być częścią lokalnej grupy administratorów na wszystkich serwerach systemu Windows obsługującego wystąpienia programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="217b7-162">The Run As account must also be part of Local Administrators group on all Windows Servers hosting SQL Server Instances.</span></span>
   >
   >
5. <span data-ttu-id="217b7-163">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="217b7-163">Click **Save**.</span></span>
6. <span data-ttu-id="217b7-164">Modyfikuj, a następnie wykonaj w poniższym przykładzie T-SQL w każdym wystąpieniu serwera SQL udzielenia minimalne uprawnienia wymagane do konta Uruchom jako w celu wykonania oceny SQL.</span><span class="sxs-lookup"><span data-stu-id="217b7-164">Modify and then execute the following T-SQL sample on each SQL Server Instance to grant minimum permissions required to Run As Account to perform SQL Assessment.</span></span> <span data-ttu-id="217b7-165">Jednak nie należy to zrobić, jeśli konto Uruchom jako jest już częścią roli serwera sysadmin na wystąpienia programu SQL Server.</span><span class="sxs-lookup"><span data-stu-id="217b7-165">However, you don’t need to do this if a Run As Account is already part of the sysadmin server role on SQL Server Instances.</span></span>

```
---
    -- Replace <UserName> with the actual user name being used as Run As Account.
    USE master

    -- Create login for the user, comment this line if login is already created.
    CREATE LOGIN [<UserName>] FROM WINDOWS

    -- Grant permissions to user.
    GRANT VIEW SERVER STATE TO [<UserName>]
    GRANT VIEW ANY DEFINITION TO [<UserName>]
    GRANT VIEW ANY DATABASE TO [<UserName>]

    -- Add database user for all the databases on SQL Server Instance, this is required for connecting to individual databases.
    -- NOTE: This command must be run anytime new databases are added to SQL Server instances.
    EXEC sp_msforeachdb N'USE [?]; CREATE USER [<UserName>] FOR LOGIN [<UserName>];'

```
#### <a name="to-configure-the-sql-run-as-account-using-windows-powershell"></a><span data-ttu-id="217b7-166">Aby skonfigurować konto Uruchom jako SQL przy użyciu programu Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="217b7-166">To configure the SQL Run As account using Windows PowerShell</span></span>
<span data-ttu-id="217b7-167">Otwórz okno programu PowerShell i uruchom następujący skrypt po zaktualizowaniu z informacjami:</span><span class="sxs-lookup"><span data-stu-id="217b7-167">Open a PowerShell window and run the following script after you’ve updated it with your information:</span></span>

```

    import-module OperationsManager
    New-SCOMManagementGroupConnection "<your management group name>"

    $profile = Get-SCOMRunAsProfile -DisplayName "OMS SQL Assessment Run As Profile"
    $account = Get-SCOMrunAsAccount | Where-Object {$_.Name -eq "<your run as account name>"}
    Set-SCOMRunAsProfile -Action "Add" -Profile $Profile -Account $Account
```

## <a name="understanding-how-recommendations-are-prioritized"></a><span data-ttu-id="217b7-168">Opis sposobu mają pierwszeństwo zalecenia</span><span class="sxs-lookup"><span data-stu-id="217b7-168">Understanding how recommendations are prioritized</span></span>
<span data-ttu-id="217b7-169">Każdy zalecenie wprowadzone otrzymuje wartość wagi, która identyfikuje względnego zalecenia.</span><span class="sxs-lookup"><span data-stu-id="217b7-169">Every recommendation made is given a weighting value that identifies the relative importance of the recommendation.</span></span> <span data-ttu-id="217b7-170">10 najważniejszych zalecenia są wyświetlane.</span><span class="sxs-lookup"><span data-stu-id="217b7-170">Only the ten most important recommendations are shown.</span></span>

### <a name="how-weights-are-calculated"></a><span data-ttu-id="217b7-171">Jak są obliczane wagi</span><span class="sxs-lookup"><span data-stu-id="217b7-171">How weights are calculated</span></span>
<span data-ttu-id="217b7-172">Wagi są wartości zagregowanych oparte na trzech kluczowych czynników:</span><span class="sxs-lookup"><span data-stu-id="217b7-172">Weightings are aggregate values based on three key factors:</span></span>

* <span data-ttu-id="217b7-173">*Prawdopodobieństwo* czy problemu może powodować problemy.</span><span class="sxs-lookup"><span data-stu-id="217b7-173">The *probability* that an issue identified will cause problems.</span></span> <span data-ttu-id="217b7-174">Większe prawdopodobieństwo równa większych ogólny wynik dla zalecenia.</span><span class="sxs-lookup"><span data-stu-id="217b7-174">A higher probability equates to a larger overall score for the recommendation.</span></span>
* <span data-ttu-id="217b7-175">*Wpływ* problemu w Twojej organizacji, jeśli spowodować problem.</span><span class="sxs-lookup"><span data-stu-id="217b7-175">The *impact* of the issue on your organization if it does cause a problem.</span></span> <span data-ttu-id="217b7-176">Większy wpływ równa większych ogólny wynik dla zalecenia.</span><span class="sxs-lookup"><span data-stu-id="217b7-176">A higher impact equates to a larger overall score for the recommendation.</span></span>
* <span data-ttu-id="217b7-177">*Nakładu* wymagane do wykonania zalecenia.</span><span class="sxs-lookup"><span data-stu-id="217b7-177">The *effort* required to implement the recommendation.</span></span> <span data-ttu-id="217b7-178">Wyższy nakładu równa mniejszych ogólny wynik dla zalecenia.</span><span class="sxs-lookup"><span data-stu-id="217b7-178">A higher effort equates to a smaller overall score for the recommendation.</span></span>

<span data-ttu-id="217b7-179">Wagi dla każde zalecenie jest wyrażona jako procent całkowitej wynik dostępne dla każdego obszaru fokus.</span><span class="sxs-lookup"><span data-stu-id="217b7-179">The weighting for each recommendation is expressed as a percentage of the total score available for each focus area.</span></span> <span data-ttu-id="217b7-180">Na przykład jeśli zalecenia w obszarze fokus zabezpieczeń i zgodności ma wynik % 5, wdrażanie tego zalecenia spowoduje zwiększenie ogólnej % wynik przez 5 zabezpieczeń i zgodności.</span><span class="sxs-lookup"><span data-stu-id="217b7-180">For example, if a recommendation in the Security and Compliance focus area has a score of 5%, implementing that recommendation will increase your overall Security and Compliance score by 5%.</span></span>

### <a name="focus-areas"></a><span data-ttu-id="217b7-181">Obszarach zainteresowań</span><span class="sxs-lookup"><span data-stu-id="217b7-181">Focus areas</span></span>
<span data-ttu-id="217b7-182">**Zabezpieczeń i zgodności** — w tym obszarze fokus zawiera zalecenia dotyczące potencjalnego zagrożenia bezpieczeństwa i naruszeń, zasad firmowych i wymagania techniczne, prawne i przepisami zgodności.</span><span class="sxs-lookup"><span data-stu-id="217b7-182">**Security and Compliance** - This focus area shows recommendations for potential security threats and breaches, corporate policies, and technical, legal and regulatory compliance requirements.</span></span>

<span data-ttu-id="217b7-183">**Dostępność i ciągłość prowadzenia działalności biznesowej** — w tym obszarze fokus zawiera zalecenia dotyczące odporności infrastruktury i ochronę biznesowej, dostępności usług.</span><span class="sxs-lookup"><span data-stu-id="217b7-183">**Availability and Business Continuity** - This focus area shows recommendations for service availability, resiliency of your infrastructure, and business protection.</span></span>

<span data-ttu-id="217b7-184">**Wydajność i skalowalność** — w tym obszarze fokus zawiera zalecenia ułatwiające organizacji infrastruktury IT zwiększania, upewnij się, że spełnia bieżące wymagania dotyczące wydajności środowiska informatycznego i jest w stanie reagować na zmieniające się infrastruktury wymagania związane z.</span><span class="sxs-lookup"><span data-stu-id="217b7-184">**Performance and Scalability** - This focus area shows recommendations to help your organization's IT infrastructure grow, ensure that your IT environment meets current performance requirements, and is able to respond to changing infrastructure needs.</span></span>

<span data-ttu-id="217b7-185">**Uaktualniania, wdrażania i migracji** — w tym obszarze fokus zawiera zalecenia ułatwiające uaktualniania, migracji i wdrożenia programu SQL Server w istniejącej infrastrukturze.</span><span class="sxs-lookup"><span data-stu-id="217b7-185">**Upgrade, Migration and Deployment** - This focus area shows recommendations to help you upgrade, migrate, and deploy SQL Server to your existing infrastructure.</span></span>

<span data-ttu-id="217b7-186">**Operacje i monitorowanie** — w tym obszarze fokus zawiera zalecenia ułatwiające usprawnić operacji IT, wdrożenia program prewencyjnej konserwacji i zmaksymalizować wydajność.</span><span class="sxs-lookup"><span data-stu-id="217b7-186">**Operations and Monitoring** - This focus area shows recommendations to help streamline your IT operations, implement preventative maintenance, and maximize performance.</span></span>

<span data-ttu-id="217b7-187">**Zarządzanie zmianami i konfiguracją** — w tym obszarze fokus zawiera zalecenia dotyczące ochrony codziennej pracy, należy zapewnić, że zmiany nie mieć negatywny wpływ na infrastrukturę, ustanowić procedury sterowania zmianami oraz do śledzenia i inspekcji konfiguracje systemu.</span><span class="sxs-lookup"><span data-stu-id="217b7-187">**Change and Configuration Management** - This focus area shows recommendations to help protect day-to-day operations, ensure that changes don't negatively affect your infrastructure, establish change control procedures, and to track and audit system configurations.</span></span>

### <a name="should-you-aim-to-score-100-in-every-focus-area"></a><span data-ttu-id="217b7-188">Należy dążyć wynik 100% w każdym obszarze fokus?</span><span class="sxs-lookup"><span data-stu-id="217b7-188">Should you aim to score 100% in every focus area?</span></span>
<span data-ttu-id="217b7-189">Niekoniecznie.</span><span class="sxs-lookup"><span data-stu-id="217b7-189">Not necessarily.</span></span> <span data-ttu-id="217b7-190">Zalecenia są oparte na wiedzy i doświadczeń zdobytych Microsoft inżynierowie między tysięcy wizyt klienta.</span><span class="sxs-lookup"><span data-stu-id="217b7-190">The recommendations are based on the knowledge and experiences gained by Microsoft engineers across thousands of customer visits.</span></span> <span data-ttu-id="217b7-191">Jednak nie infrastruktury serwerowe są takie same i szczegółowe zalecenia mogą być bardziej lub mniej istotne dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="217b7-191">However, no two server infrastructures are the same, and specific recommendations may be more or less relevant to you.</span></span> <span data-ttu-id="217b7-192">Na przykład niektóre zalecenia dotyczące zabezpieczeń może być mniej ważne, jeśli maszyny wirtualne nie są widoczne w Internecie.</span><span class="sxs-lookup"><span data-stu-id="217b7-192">For example, some security recommendations might be less relevant if your virtual machines are not exposed to the Internet.</span></span> <span data-ttu-id="217b7-193">Kilka zaleceń dostępności może być mniej istotne dla usług, które umożliwiają zbieranie danych ad hoc — niski priorytet i raportowania.</span><span class="sxs-lookup"><span data-stu-id="217b7-193">Some availability recommendations may be less relevant for services that provide low priority ad hoc data collection and reporting.</span></span> <span data-ttu-id="217b7-194">Problemy, które są ważne dla dorosłych firm może być mniej ważne do rozruchu.</span><span class="sxs-lookup"><span data-stu-id="217b7-194">Issues that are important to a mature business may be less important to a start-up.</span></span> <span data-ttu-id="217b7-195">Można zidentyfikować obszary fokus, które mają zebranych i przyjrzyj się jak zmienić wyniki wraz z upływem czasu.</span><span class="sxs-lookup"><span data-stu-id="217b7-195">You may want to identify which focus areas are your priorities and then look at how your scores change over time.</span></span>

<span data-ttu-id="217b7-196">Każdy zalecenie obejmuje wskazówek dotyczących Dlaczego ważne jest.</span><span class="sxs-lookup"><span data-stu-id="217b7-196">Every recommendation includes guidance about why it is important.</span></span> <span data-ttu-id="217b7-197">Do oceny, czy wdrażanie zalecenie jest odpowiednie dla Ciebie, biorąc pod uwagę rodzaj usług informatycznych i potrzeb biznesowych w organizacji, należy skorzystać z poniższych wskazówek.</span><span class="sxs-lookup"><span data-stu-id="217b7-197">You should use this guidance to evaluate whether implementing the recommendation is appropriate for you, given the nature of your IT services and the business needs of your organization.</span></span>

## <a name="use-assessment-focus-area-recommendations"></a><span data-ttu-id="217b7-198">Użyj zaleceń obszaru fokus oceny</span><span class="sxs-lookup"><span data-stu-id="217b7-198">Use assessment focus area recommendations</span></span>
<span data-ttu-id="217b7-199">Zanim użyjesz rozwiązanie do oceny w pakietu OMS musi mieć zainstalowane oprogramowanie.</span><span class="sxs-lookup"><span data-stu-id="217b7-199">Before you can use an assessment solution in OMS, you must have the solution installed.</span></span> <span data-ttu-id="217b7-200">Aby uzyskać więcej informacji na temat instalowania rozwiązań, zobacz [rozwiązań dodać analizy dzienników z galerii rozwiązań](log-analytics-add-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="217b7-200">To read more about installing solutions, see [Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md).</span></span> <span data-ttu-id="217b7-201">Po jego zainstalowaniu, można wyświetlić podsumowanie zaleceń za pomocą kafelka oceny SQL na stronie Przegląd w OMS.</span><span class="sxs-lookup"><span data-stu-id="217b7-201">After it is installed, you can view the summary of recommendations by using the SQL Assessment tile on the Overview page in OMS.</span></span>

<span data-ttu-id="217b7-202">Wyświetl oceny zgodności podsumowania dla Twojej infrastruktury, a następnie wejdź do zalecenia.</span><span class="sxs-lookup"><span data-stu-id="217b7-202">View the summarized compliance assessments for your infrastructure and then drill-into recommendations.</span></span>

### <a name="to-view-recommendations-for-a-focus-area-and-take-corrective-action"></a><span data-ttu-id="217b7-203">Aby wyświetlić zalecenia dla obszaru fokus i podjąć działania naprawcze</span><span class="sxs-lookup"><span data-stu-id="217b7-203">To view recommendations for a focus area and take corrective action</span></span>
1. <span data-ttu-id="217b7-204">Na **omówienie** kliknij przycisk **oceny SQL** kafelka.</span><span class="sxs-lookup"><span data-stu-id="217b7-204">On the **Overview** page, click the **SQL Assessment** tile.</span></span>
2. <span data-ttu-id="217b7-205">Na **oceny SQL** strony, sprawdź informacje w jednym z bloków obszaru fokus, a następnie kliknij przycisk jedna, aby wyświetlić zalecenia dla tego obszaru fokus.</span><span class="sxs-lookup"><span data-stu-id="217b7-205">On the **SQL Assessment** page, review the summary information in one of the focus area blades and then click one to view recommendations for that focus area.</span></span>
3. <span data-ttu-id="217b7-206">Na wszystkich stronach obszaru fokus można wyświetlić priorytetową zalecenia dla danego środowiska.</span><span class="sxs-lookup"><span data-stu-id="217b7-206">On any of the focus area pages, you can view the prioritized recommendations made for your environment.</span></span> <span data-ttu-id="217b7-207">Kliknij zalecenie, w obszarze **dotyczy obiektów** Aby wyświetlić szczegóły dotyczące Dlaczego tworzone są zalecenia.</span><span class="sxs-lookup"><span data-stu-id="217b7-207">Click a recommendation under **Affected Objects** to view details about why the recommendation is made.</span></span>  
    <span data-ttu-id="217b7-208">![Obraz zalecenia oceny SQL](./media/log-analytics-sql-assessment/sql-assess-focus.png)</span><span class="sxs-lookup"><span data-stu-id="217b7-208">![image of SQL Assessment recommendations](./media/log-analytics-sql-assessment/sql-assess-focus.png)</span></span>
4. <span data-ttu-id="217b7-209">Należy wykonać działania naprawcze sugerowane w **sugerowanych akcji**.</span><span class="sxs-lookup"><span data-stu-id="217b7-209">You can take corrective actions suggested in **Suggested Actions**.</span></span> <span data-ttu-id="217b7-210">Jeśli element został rozwiązany, ocen nowsze zarejestruje które zalecane akcje zostały pobrane i zwiększa wynik zgodności.</span><span class="sxs-lookup"><span data-stu-id="217b7-210">When the item has been addressed, later assessments will record that recommended actions were taken and your compliance score will increase.</span></span> <span data-ttu-id="217b7-211">Poprawione elementy są wyświetlane jako **przekazany obiektów**.</span><span class="sxs-lookup"><span data-stu-id="217b7-211">Corrected items appear as **Passed Objects**.</span></span>

## <a name="ignore-recommendations"></a><span data-ttu-id="217b7-212">Ignoruj zalecenia</span><span class="sxs-lookup"><span data-stu-id="217b7-212">Ignore recommendations</span></span>
<span data-ttu-id="217b7-213">Jeśli masz zaleceń, które chcesz zignorować, można utworzyć pliku tekstowego używanego OMS zapobiegające zaleceń znajdujących się w wynikach oceny.</span><span class="sxs-lookup"><span data-stu-id="217b7-213">If you have recommendations that you want to ignore, you can create a text file that OMS will use to prevent recommendations from appearing in your assessment results.</span></span>

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

### <a name="to-identify-recommendations-that-you-will-ignore"></a><span data-ttu-id="217b7-214">Aby zidentyfikować zaleceń, które będzie ignorować</span><span class="sxs-lookup"><span data-stu-id="217b7-214">To identify recommendations that you will ignore</span></span>
1. <span data-ttu-id="217b7-215">Zaloguj się do swojego obszaru roboczego i Otwórz dziennik wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="217b7-215">Sign in to your workspace and open Log Search.</span></span> <span data-ttu-id="217b7-216">Użyj następującego zapytania do listy zaleceń, które nie powiodły, na komputerach w danym środowisku.</span><span class="sxs-lookup"><span data-stu-id="217b7-216">Use the following query to list recommendations that have failed for computers in your environment.</span></span>

   ```
   Type=SQLAssessmentRecommendation RecommendationResult=Failed | select  Computer, RecommendationId, Recommendation | sort  Computer
   ```

   <span data-ttu-id="217b7-217">Poniżej przedstawiono zrzut ekranu przedstawiający zapytania wyszukiwania dziennika: ![nie powiodło się zalecenia](./media/log-analytics-sql-assessment/sql-assess-failed-recommendations.png)</span><span class="sxs-lookup"><span data-stu-id="217b7-217">Here's a screen shot showing the Log Search query: ![failed recommendations](./media/log-analytics-sql-assessment/sql-assess-failed-recommendations.png)</span></span>
2. <span data-ttu-id="217b7-218">Wybierz zaleceń, które chcesz zignorować.</span><span class="sxs-lookup"><span data-stu-id="217b7-218">Choose recommendations that you want to ignore.</span></span> <span data-ttu-id="217b7-219">Użyjesz wartości RecommendationId w następnej procedurze.</span><span class="sxs-lookup"><span data-stu-id="217b7-219">You’ll use the values for RecommendationId in the next procedure.</span></span>

### <a name="to-create-and-use-an-ignorerecommendationstxt-text-file"></a><span data-ttu-id="217b7-220">Tworzenie i używanie IgnoreRecommendations.txt pliku tekstowego</span><span class="sxs-lookup"><span data-stu-id="217b7-220">To create and use an IgnoreRecommendations.txt text file</span></span>
1. <span data-ttu-id="217b7-221">Utwórz plik o nazwie IgnoreRecommendations.txt.</span><span class="sxs-lookup"><span data-stu-id="217b7-221">Create a file named IgnoreRecommendations.txt.</span></span>
2. <span data-ttu-id="217b7-222">Wklej lub wpisz każdego RecommendationId dla każde zalecenie, które mają OMS można zignorować w osobnym wierszu, a następnie zapisz i zamknij plik.</span><span class="sxs-lookup"><span data-stu-id="217b7-222">Paste or type each RecommendationId for each recommendation that you want OMS to ignore on a separate line and then save and close the file.</span></span>
3. <span data-ttu-id="217b7-223">Umieść plik w następującym folderze na każdym komputerze, w którym ma OMS zignorowanie zalecenia.</span><span class="sxs-lookup"><span data-stu-id="217b7-223">Put the file in the following folder on each computer where you want OMS to ignore recommendations.</span></span>
   * <span data-ttu-id="217b7-224">Na komputerach z usługą Microsoft Monitoring Agent (połączony bezpośrednio lub za pośrednictwem programu Operations Manager) - *SystemDrive*: \Program Files\Microsoft Agent\Agent monitorowania</span><span class="sxs-lookup"><span data-stu-id="217b7-224">On computers with the Microsoft Monitoring Agent (connected directly or through Operations Manager) - *SystemDrive*:\Program Files\Microsoft Monitoring Agent\Agent</span></span>
   * <span data-ttu-id="217b7-225">Na serwerze zarządzania programu Operations Manager — *SystemDrive*: System Center 2012 R2\Operations Manager\Server \Program Files\Microsoft</span><span class="sxs-lookup"><span data-stu-id="217b7-225">On the Operations Manager management server - *SystemDrive*:\Program Files\Microsoft System Center 2012 R2\Operations Manager\Server</span></span>

### <a name="to-verify-that-recommendations-are-ignored"></a><span data-ttu-id="217b7-226">Aby zweryfikować, że zalecenia są ignorowane</span><span class="sxs-lookup"><span data-stu-id="217b7-226">To verify that recommendations are ignored</span></span>
1. <span data-ttu-id="217b7-227">Po na następną zaplanowaną ocenę działa, domyślnie co 7 dni, określonego zalecenia są oznaczane ignorowany i nie będą wyświetlane na pulpicie nawigacyjnym oceny.</span><span class="sxs-lookup"><span data-stu-id="217b7-227">After the next scheduled assessment runs, by default every 7 days, the specified recommendations are marked Ignored and will not appear on the assessment dashboard.</span></span>
2. <span data-ttu-id="217b7-228">Następujące zapytania wyszukiwania dziennika służy do tworzenia listy wszystkich zignorowane zalecenia.</span><span class="sxs-lookup"><span data-stu-id="217b7-228">You can use the following Log Search queries to list all the ignored recommendations.</span></span>

   ```
   Type=SQLAssessmentRecommendation RecommendationResult=Ignored | select  Computer, RecommendationId, Recommendation | sort  Computer
   ```
3. <span data-ttu-id="217b7-229">Jeśli później zdecydujesz chcesz zobaczyć zignorowane zalecenia dotyczące, Usuń wszystkie pliki IgnoreRecommendations.txt lub RecommendationIDs można usunąć z nich.</span><span class="sxs-lookup"><span data-stu-id="217b7-229">If you decide later that you want to see ignored recommendations, remove any IgnoreRecommendations.txt files, or you can remove RecommendationIDs from them.</span></span>

## <a name="sql-assessment-solution-faq"></a><span data-ttu-id="217b7-230">Rozwiązanie do oceny SQL — często zadawane pytania</span><span class="sxs-lookup"><span data-stu-id="217b7-230">SQL Assessment solution FAQ</span></span>
<span data-ttu-id="217b7-231">*Częstotliwość oceny, czy działa?*</span><span class="sxs-lookup"><span data-stu-id="217b7-231">*How often does an assessment run?*</span></span>

* <span data-ttu-id="217b7-232">Ocena jest uruchamiane co 7 dni.</span><span class="sxs-lookup"><span data-stu-id="217b7-232">The assessment runs every 7 days.</span></span>

<span data-ttu-id="217b7-233">*Czy istnieje sposób konfigurowania, jak często jest uruchamiana oceny?*</span><span class="sxs-lookup"><span data-stu-id="217b7-233">*Is there a way to configure how often the assessment runs?*</span></span>

* <span data-ttu-id="217b7-234">Nie w tej chwili.</span><span class="sxs-lookup"><span data-stu-id="217b7-234">Not at this time.</span></span>

<span data-ttu-id="217b7-235">*Jeśli inny serwer zostanie odnaleziony po rozwiązanie do oceny SQL zostały dodane, zostanie on oceniane?*</span><span class="sxs-lookup"><span data-stu-id="217b7-235">*If another server is discovered after I’ve added the SQL assessment solution, will it be assessed?*</span></span>

* <span data-ttu-id="217b7-236">Tak, gdy okaże się, że jest oceniane z następnie, co 7 dni.</span><span class="sxs-lookup"><span data-stu-id="217b7-236">Yes, once it is discovered it is assessed from then on, every 7 days.</span></span>

<span data-ttu-id="217b7-237">*Jeśli serwer jest likwidowany, gdy zostanie ono zostać usunięte z oceny?*</span><span class="sxs-lookup"><span data-stu-id="217b7-237">*If a server is decommissioned, when will it be removed from the assessment?*</span></span>

* <span data-ttu-id="217b7-238">Jeśli serwer nie przedstawi danych do 3 tygodni, zostanie ono usunięte.</span><span class="sxs-lookup"><span data-stu-id="217b7-238">If a server does not submit data for 3 weeks, it is removed.</span></span>

<span data-ttu-id="217b7-239">*Co to jest nazwa procesu, który wykonuje zbierania danych?*</span><span class="sxs-lookup"><span data-stu-id="217b7-239">*What is the name of the process that does the data collection?*</span></span>

* <span data-ttu-id="217b7-240">AdvisorAssessment.exe</span><span class="sxs-lookup"><span data-stu-id="217b7-240">AdvisorAssessment.exe</span></span>

<span data-ttu-id="217b7-241">*Jak długo trwa do zebrania danych?*</span><span class="sxs-lookup"><span data-stu-id="217b7-241">*How long does it take for data to be collected?*</span></span>

* <span data-ttu-id="217b7-242">Kolekcja rzeczywistymi danymi na serwerze trwa około 1 godziny.</span><span class="sxs-lookup"><span data-stu-id="217b7-242">The actual data collection on the server takes about 1 hour.</span></span> <span data-ttu-id="217b7-243">Może trwać dłużej na serwerach, które mają wiele wystąpień programu SQL lub bazy danych.</span><span class="sxs-lookup"><span data-stu-id="217b7-243">It may take longer on servers that have a large number of SQL instances or databases.</span></span>

<span data-ttu-id="217b7-244">*Jakiego typu dane są zbierane?*</span><span class="sxs-lookup"><span data-stu-id="217b7-244">*What type of data is collected?*</span></span>

* <span data-ttu-id="217b7-245">Zbierane są następujące typy danych:</span><span class="sxs-lookup"><span data-stu-id="217b7-245">The following types of data are collected:</span></span>
  * <span data-ttu-id="217b7-246">USŁUGI WMI</span><span class="sxs-lookup"><span data-stu-id="217b7-246">WMI</span></span>
  * <span data-ttu-id="217b7-247">Rejestru</span><span class="sxs-lookup"><span data-stu-id="217b7-247">Registry</span></span>
  * <span data-ttu-id="217b7-248">Liczniki wydajności</span><span class="sxs-lookup"><span data-stu-id="217b7-248">Performance counters</span></span>
  * <span data-ttu-id="217b7-249">SQL dynamicznych widoków zarządzania (DMV).</span><span class="sxs-lookup"><span data-stu-id="217b7-249">SQL dynamic management views (DMV).</span></span>

<span data-ttu-id="217b7-250">*Czy istnieje sposób konfigurowania, gdy dane są zbierane?*</span><span class="sxs-lookup"><span data-stu-id="217b7-250">*Is there a way to configure when data is collected?*</span></span>

* <span data-ttu-id="217b7-251">Nie w tej chwili.</span><span class="sxs-lookup"><span data-stu-id="217b7-251">Not at this time.</span></span>

<span data-ttu-id="217b7-252">*Dlaczego trzeba skonfigurować konto Uruchom jako?*</span><span class="sxs-lookup"><span data-stu-id="217b7-252">*Why do I have to configure a Run As Account?*</span></span>

* <span data-ttu-id="217b7-253">Dla programu SQL Server są uruchamiane niewielkiej liczby zapytania SQL.</span><span class="sxs-lookup"><span data-stu-id="217b7-253">For SQL Server, a small number of SQL queries are run.</span></span> <span data-ttu-id="217b7-254">Aby je uruchomić należy użyć konto Uruchom jako z uprawnieniami VIEW SERVER STATE do bazy danych SQL.</span><span class="sxs-lookup"><span data-stu-id="217b7-254">In order for them to run, a Run As Account with VIEW SERVER STATE permissions to SQL must be used.</span></span>  <span data-ttu-id="217b7-255">Ponadto aby można było wykonać kwerendę usługi WMI, wymagane są poświadczenia administratora lokalnego.</span><span class="sxs-lookup"><span data-stu-id="217b7-255">In addition, in order to query WMI, local administrator credentials are required.</span></span>

<span data-ttu-id="217b7-256">*Dlaczego są wyświetlane tylko zalecenia 10 pierwszych?*</span><span class="sxs-lookup"><span data-stu-id="217b7-256">*Why display only the top 10 recommendations?*</span></span>

* <span data-ttu-id="217b7-257">Zamiast daje utrudnione kompletnej zadań, zaleca się skupić się na najpierw adresowania priorytetową zalecenia.</span><span class="sxs-lookup"><span data-stu-id="217b7-257">Instead of giving you an exhaustive overwhelming list of tasks, we recommend that you focus on addressing the prioritized recommendations first.</span></span> <span data-ttu-id="217b7-258">Po adresu im dodatkowe zalecenia staną się dostępne.</span><span class="sxs-lookup"><span data-stu-id="217b7-258">After you address them, additional recommendations will become available.</span></span> <span data-ttu-id="217b7-259">Jeśli wolisz wyświetlić listę szczegółowych, można wyświetlić wszystkie zalecenia, używając przycisku Wyszukaj dziennika OMS.</span><span class="sxs-lookup"><span data-stu-id="217b7-259">If you prefer to see the detailed list, you can view all recommendations using the OMS log search.</span></span>

<span data-ttu-id="217b7-260">*Czy istnieje sposób, aby zignorować zalecenie?*</span><span class="sxs-lookup"><span data-stu-id="217b7-260">*Is there a way to ignore a recommendation?*</span></span>

* <span data-ttu-id="217b7-261">Tak, zobacz [zignorowanie zalecenia](#ignore-recommendations) powyższej sekcji.</span><span class="sxs-lookup"><span data-stu-id="217b7-261">Yes, see [Ignore recommendations](#ignore-recommendations) section above.</span></span>

## <a name="next-steps"></a><span data-ttu-id="217b7-262">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="217b7-262">Next steps</span></span>
* <span data-ttu-id="217b7-263">[Wyszukaj dzienniki](log-analytics-log-searches.md) do wyświetlenia szczegółowych danych SQL do oceny i zalecenia.</span><span class="sxs-lookup"><span data-stu-id="217b7-263">[Search logs](log-analytics-log-searches.md) to view detailed SQL Assessment data and recommendations.</span></span>
