---
title: "aaaThreat wykrywania — baza danych SQL Azure | Dokumentacja firmy Microsoft"
description: "Wykrywanie zagrożeń wykrywa nietypowe działania bazy danych wskazujące toohello zagrożenia potencjalnych zabezpieczeń bazy danych."
services: sql-database
documentationcenter: 
author: rmatchoro
manager: jhubbard
editor: v-romcal
ms.assetid: b50d232a-4225-46ed-91e7-75288f55ee84
ms.service: sql-database
ms.custom: security
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 06/19/2017
ms.author: ronmat; ronitr
ms.openlocfilehash: 0879d20eff515a4e69358b5a98ceccf57fbd0ea2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="sql-database-threat-detection"></a><span data-ttu-id="30c71-103">Wykrywanie zagrożeń bazy danych SQL</span><span class="sxs-lookup"><span data-stu-id="30c71-103">SQL Database Threat Detection</span></span>

<span data-ttu-id="30c71-104">SQL wykrywanie zagrożeń wykrywa nietypowe działania wskazują nietypowe i potencjalnie szkodliwe prób tooaccess lub wykorzystać baz danych.</span><span class="sxs-lookup"><span data-stu-id="30c71-104">SQL Threat Detection detects anomalous activities indicating unusual and potentially harmful attempts tooaccess or exploit databases.</span></span>

## <a name="overview"></a><span data-ttu-id="30c71-105">Omówienie</span><span class="sxs-lookup"><span data-stu-id="30c71-105">Overview</span></span>

<span data-ttu-id="30c71-106">Wykrywanie zagrożeń SQL zawiera nową warstwę zabezpieczeń, co umożliwia klientom toodetect i odpowiadać toopotential zagrożeń w miarę ich występowania, zapewniając alerty zabezpieczeń w nietypowych działań.</span><span class="sxs-lookup"><span data-stu-id="30c71-106">SQL Threat Detection provides a new layer of security, which enables customers toodetect and respond toopotential threats as they occur by providing security alerts on anomalous activities.</span></span>  <span data-ttu-id="30c71-107">Użytkownicy będą otrzymywać alert po bazy danych podejrzanych działań, potencjalnych luk i ataki, a także bazy danych nietypowe wzorce dostępu.</span><span class="sxs-lookup"><span data-stu-id="30c71-107">Users will receive an alert upon suspicious database activities, potential vulnerabilities, and SQL injection attacks, as well as anomalous database access patterns.</span></span> <span data-ttu-id="30c71-108">Wykrywanie zagrożeń SQL alerty zawierają szczegółowe informacje o podejrzanych działaniach i zalecane działania dotyczące tooinvestigate i uniknięcie hello zagrożenia.</span><span class="sxs-lookup"><span data-stu-id="30c71-108">SQL Threat Detection alerts provide details of suspicious activity and recommend action on how tooinvestigate and mitigate hello threat.</span></span> <span data-ttu-id="30c71-109">Użytkownicy mogą Eksploruj hello zdarzenia podejrzane przy użyciu [SQL Database Auditing](sql-database-auditing.md) toodetermine, jeśli są one wynikiem tooaccess próby naruszenia lub wykorzystania danych w bazie danych hello.</span><span class="sxs-lookup"><span data-stu-id="30c71-109">Users can explore hello suspicious events using [SQL Database Auditing](sql-database-auditing.md) toodetermine if they result from an attempt tooaccess, breach, or exploit data in hello database.</span></span> <span data-ttu-id="30c71-110">Wykrywanie zagrożeń umożliwia proste tooaddress potencjalne zagrożenia toohello bazy danych bez toobe potrzeby hello ekspert zabezpieczeń lub zarządzać zabezpieczeniami zaawansowanymi, monitorowanie systemów.</span><span class="sxs-lookup"><span data-stu-id="30c71-110">Threat Detection makes it simple tooaddress potential threats toohello database without hello need toobe a security expert or manage advanced security monitoring systems.</span></span>

<span data-ttu-id="30c71-111">Na przykład iniekcja kodu SQL jest jednym z hello typowych problemów sieci Web aplikacji zabezpieczeń na powitania internetowe, aplikacje używane tooattack opartych na danych.</span><span class="sxs-lookup"><span data-stu-id="30c71-111">For example, SQL injection is one of hello common Web application security issues on hello Internet, used tooattack data-driven applications.</span></span> <span data-ttu-id="30c71-112">Osoby atakujące korzystać z tooinject luk w zabezpieczeniach aplikacji złośliwego instrukcji SQL do pola wejścia aplikacji, mogą spowodować lub modyfikowanie danych w bazie danych hello.</span><span class="sxs-lookup"><span data-stu-id="30c71-112">Attackers take advantage of application vulnerabilities tooinject malicious SQL statements into application entry fields, breaching or modifying data in hello database.</span></span>

<span data-ttu-id="30c71-113">Wykrywanie zagrożeń SQL integruje alerty z [Centrum zabezpieczeń Azure](https://azure.microsoft.com/en-us/services/security-center/), a każdy chroniony serwer bazy danych SQL zostanie rozliczony na powitania same ceny warstwy standardowa Centrum zabezpieczeń Azure, w $15 węzła/miesięcznie, gdzie każdy chronione SQL Serwer bazy danych jest liczone jako jeden węzeł.</span><span class="sxs-lookup"><span data-stu-id="30c71-113">SQL Threat Detection integrates alerts with [Azure Security Center](https://azure.microsoft.com/en-us/services/security-center/), and, each protected SQL Database server will be billed at hello same price as Azure Security Center Standard tier, at $15/node/month, where each protected SQL Database server is counted as one node.</span></span> <span data-ttu-id="30c71-114">Zachęcamy tootry go przez 60 dni do zwolnienia.</span><span class="sxs-lookup"><span data-stu-id="30c71-114">We invite you tootry it out for 60 days for free.</span></span> 

## <a name="set-up-threat-detection-for-your-database-in-hello-azure-portal"></a><span data-ttu-id="30c71-115">Skonfiguruj wykrywanie zagrożeń dla bazy danych w hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="30c71-115">Set up threat detection for your database in hello Azure portal</span></span>
1. <span data-ttu-id="30c71-116">Uruchamianie hello Azure w portalu [https://portal.azure.com](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="30c71-116">Launch hello Azure portal at [https://portal.azure.com](https://portal.azure.com).</span></span>
2. <span data-ttu-id="30c71-117">Przejdź bloku konfiguracji toohello hello ma toomonitor bazy danych SQL.</span><span class="sxs-lookup"><span data-stu-id="30c71-117">Navigate toohello configuration blade of hello SQL Database you want toomonitor.</span></span> <span data-ttu-id="30c71-118">W bloku ustawienia hello, wybierz **Inspekcja i wykrywanie zagrożeń**.</span><span class="sxs-lookup"><span data-stu-id="30c71-118">In hello Settings blade, select **Auditing & Threat Detection**.</span></span> 
    <span data-ttu-id="30c71-119">![Okienko nawigacji][1]</span><span class="sxs-lookup"><span data-stu-id="30c71-119">![Navigation pane][1]</span></span>
3. <span data-ttu-id="30c71-120">W hello **Inspekcja i wykrywanie zagrożeń** Włącz bloku konfiguracji **ON** inspekcji, w którym będą wyświetlane ustawienia wykrywania zagrożeń hello.</span><span class="sxs-lookup"><span data-stu-id="30c71-120">In hello **Auditing & Threat Detection** configuration blade turn **ON** Auditing, which will display hello threat detection settings.</span></span>
  
    ![Okienko nawigacji][2]
4. <span data-ttu-id="30c71-122">Włącz **ON** wykrywanie zagrożeń.</span><span class="sxs-lookup"><span data-stu-id="30c71-122">Turn **ON** Threat detection.</span></span>
5. <span data-ttu-id="30c71-123">Skonfiguruj listę hello wiadomości e-mail, które będą wysyłane alerty zabezpieczeń po wykryciu nietypowe działania bazy danych.</span><span class="sxs-lookup"><span data-stu-id="30c71-123">Configure hello list of emails that will receive security alerts upon detection of anomalous database activities.</span></span>
6. <span data-ttu-id="30c71-124">Kliknij przycisk **zapisać** w hello **Inspekcja i wykrywanie zagrożeń** toosave bloku hello nowych lub zaktualizowanych inspekcji i zagrożeń ustawienia wykrywania.</span><span class="sxs-lookup"><span data-stu-id="30c71-124">Click **Save** in hello **Auditing & Threat detection** blade toosave hello new or updated auditing and threat detection settings.</span></span>
       
    ![Okienko nawigacji][3]

## <a name="set-up-threat-detection-using-powershell"></a><span data-ttu-id="30c71-126">Skonfiguruj wykrywanie zagrożeń przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="30c71-126">Set up threat detection using PowerShell</span></span>

<span data-ttu-id="30c71-127">Na przykład skryptu, zobacz [konfigurowania inspekcji i wykrywania zagrożeń przy użyciu programu PowerShell](scripts/sql-database-auditing-and-threat-detection-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="30c71-127">For a script example, see [Configure auditing and threat detection using PowerShell](scripts/sql-database-auditing-and-threat-detection-powershell.md).</span></span>

## <a name="explore-anomalous-database-activities-upon-detection-of-a-suspicious-event"></a><span data-ttu-id="30c71-128">Eksploruj nietypowe działania bazy danych w przypadku wykrycia podejrzanych zdarzeń</span><span class="sxs-lookup"><span data-stu-id="30c71-128">Explore anomalous database activities upon detection of a suspicious event</span></span>
1. <span data-ttu-id="30c71-129">Otrzymasz wiadomość e-mail z powiadomieniem po wykryciu nietypowe działania bazy danych.</span><span class="sxs-lookup"><span data-stu-id="30c71-129">You will receive an email notification upon detection of anomalous database activities.</span></span> <br/>
   <span data-ttu-id="30c71-130">Hello poczty e-mail będzie zawierał informacje w tym rodzaj hello hello nietypowych działań, nazwa bazy danych, nazwę serwera, nazwa aplikacji i czas trwania zdarzenia hello zdarzenia zabezpieczeń podejrzane hello.</span><span class="sxs-lookup"><span data-stu-id="30c71-130">hello email will provide information on hello suspicious security event including hello nature of hello anomalous activities, database name, server name, application name, and hello event time.</span></span> <span data-ttu-id="30c71-131">Ponadto hello poczty e-mail zawierają informacje dotyczące przyczyny i zalecane akcje tooinvestigate i ograniczyć hello potencjalne zagrożenie toohello w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="30c71-131">In addition, hello email will provide information on possible causes and recommended actions tooinvestigate and mitigate hello potential threat toohello database.</span></span><br/>
     
    ![Okienko nawigacji][4]
2. <span data-ttu-id="30c71-133">alerty e-mail Hello zawiera dziennik inspekcji SQL toohello bezpośredniego łącza.</span><span class="sxs-lookup"><span data-stu-id="30c71-133">hello email alert includes a direct link toohello SQL Audit log.</span></span> <span data-ttu-id="30c71-134">Kliknięcie tego łącza spowoduje uruchomienie hello Azure portal i otwiera hello SQL rekordów inspekcji wokół czasu hello hello podejrzane zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="30c71-134">Clicking on this link launches hello Azure portal and opens hello SQL Audit records around hello time of hello suspicious event.</span></span> <span data-ttu-id="30c71-135">Polecenie tooview rekordów inspekcji więcej szczegółów na powitania podejrzane bazy danych działań, dzięki czemu można łatwiej toofind hello instrukcji SQL, które zostały wykonane (kto uzyskiwał dostęp do, co zostało i kiedy) i określenie, czy zdarzenie hello uzasadnionych lub złośliwymi (np. aplikacji wydaniem iniekcji tooSQL luki w zabezpieczeniach, kogoś naruszone poufnych danych itp.).</span><span class="sxs-lookup"><span data-stu-id="30c71-135">Click on an audit record tooview more details on hello suspicious database activities, making it easier toofind hello SQL statements that were executed (who accessed, what they did and when) and determine if hello event was legitimate or malicious (e.g. application vulnerability tooSQL injection was exploited, someone breached sensitive data, etc.).</span></span><br/><span data-ttu-id="30c71-136">
   ![Okienko nawigacji][5]</span><span class="sxs-lookup"><span data-stu-id="30c71-136">
![Navigation pane][5]</span></span>


## <a name="explore-threat-detection-alerts-for-your-database-in-hello-azure-portal"></a><span data-ttu-id="30c71-137">Eksploruj alertów wykrywania zagrożeń dla bazy danych w hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="30c71-137">Explore threat detection alerts for your database in hello Azure portal</span></span>

<span data-ttu-id="30c71-138">Wykrywanie zagrożeń bazy danych SQL integruje się jego alerty z [Centrum zabezpieczeń Azure](https://azure.microsoft.com/en-us/services/security-center/).</span><span class="sxs-lookup"><span data-stu-id="30c71-138">SQL Database Threat Detection integrates its alerts with [Azure Security Center](https://azure.microsoft.com/en-us/services/security-center/).</span></span> <span data-ttu-id="30c71-139">Na żywo Kafelek zabezpieczenia SQL w bloku bazy danych hello hello Azure śledzi portalu hello stan active zagrożeń.</span><span class="sxs-lookup"><span data-stu-id="30c71-139">A live SQL security tile within hello database blade in hello Azure portal tracks hello status of active threats.</span></span> 

   ![Okienko nawigacji][6]
   
1. <span data-ttu-id="30c71-141">Kliknięcie kafelka zabezpieczeń SQL hello uruchamia blok alerty Centrum zabezpieczeń Azure hello i zawiera omówienie active zagrożeń SQL wykryte na powitania bazy danych.</span><span class="sxs-lookup"><span data-stu-id="30c71-141">Clicking on hello SQL security tile launches hello Azure Security Center alerts blade and provides an overview of active SQL threats detected on hello database.</span></span> 

  ![Okienko nawigacji][7]

2. <span data-ttu-id="30c71-143">Kliknij określony alert zawiera dodatkowe szczegóły oraz do badania tego zagrożenia i korygowania przyszłych zagrożenia.</span><span class="sxs-lookup"><span data-stu-id="30c71-143">Clicking on a specific alert provides additional details and actions for investigating this threat and remediating future threats.</span></span>

  ![Okienko nawigacji][8]


## <a name="next-steps"></a><span data-ttu-id="30c71-145">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="30c71-145">Next steps</span></span>

* <span data-ttu-id="30c71-146">Dowiedz się więcej o wykrywanie zagrożeń, odwiedź hello [Azure blog](https://azure.microsoft.com/en-us/blog/azure-sql-database-threat-detection-general-availability-in-spring-2017/)</span><span class="sxs-lookup"><span data-stu-id="30c71-146">Learn more about Threat Detection, visit hello [Azure blog](https://azure.microsoft.com/en-us/blog/azure-sql-database-threat-detection-general-availability-in-spring-2017/)</span></span> 
* <span data-ttu-id="30c71-147">Dowiedz się więcej o [inspekcja bazy danych SQL Azure](sql-database-auditing.md)</span><span class="sxs-lookup"><span data-stu-id="30c71-147">Learn more about [Azure SQL Database Auditing](sql-database-auditing.md)</span></span>
* <span data-ttu-id="30c71-148">Dowiedz się więcej o [Centrum zabezpieczeń Azure](https://docs.microsoft.com/en-us/azure/security-center/security-center-intro)</span><span class="sxs-lookup"><span data-stu-id="30c71-148">Learn more about [Azure Security Center](https://docs.microsoft.com/en-us/azure/security-center/security-center-intro)</span></span>
* <span data-ttu-id="30c71-149">Aby uzyskać więcej informacji o cenach, zobacz hello [stronie cennika bazy danych SQL](https://azure.microsoft.com/en-us/pricing/details/sql-database/)</span><span class="sxs-lookup"><span data-stu-id="30c71-149">For more details on pricing, please see hello [SQL Database Pricing page](https://azure.microsoft.com/en-us/pricing/details/sql-database/)</span></span>  
* <span data-ttu-id="30c71-150">Na przykład skryptu programu PowerShell, zobacz [konfigurowania inspekcji i wykrywania zagrożeń przy użyciu programu PowerShell](scripts/sql-database-auditing-and-threat-detection-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="30c71-150">For a PowerShell script example, see [Configure auditing and threat detection using PowerShell](scripts/sql-database-auditing-and-threat-detection-powershell.md)</span></span>



<!--Image references-->
[1]: ./media/sql-database-threat-detection/1_td_click_on_settings.png
[2]: ./media/sql-database-threat-detection/2_td_turn_on_auditing.png
[3]: ./media/sql-database-threat-detection/3_td_turn_on_threat_detection.png
[4]: ./media/sql-database-threat-detection/4_td_email.png
[5]: ./media/sql-database-threat-detection/5_td_audit_record_details.png
[6]: ./media/sql-database-threat-detection/6_td_security_tile_view_alerts.png
[7]: ./media/sql-database-threat-detection/7_td_SQL_security_alerts_list.png
[8]: ./media/sql-database-threat-detection/8_td_SQL_security_alert_details.png


