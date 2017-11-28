---
title: "aaaGet wprowadzenie wykrywanie zagrożeń magazynu danych SQL"
description: "Jak tooget pracę z wykrywanie zagrożeń"
services: sql-data-warehouse
documentationcenter: 
author: ronortloff
manager: jhubbard
editor: 
ms.assetid: c9073dd9-6c62-4735-8457-dfb9f859c900
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: security
ms.date: 10/31/2016
ms.author: rortloff;barbkess
ms.openlocfilehash: dec0b734849e7f52434e099db0b38fbf0bf6ad53
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-threat-detection"></a><span data-ttu-id="73b09-103">Rozpoczynanie pracy z wykrywanie zagrożeń</span><span class="sxs-lookup"><span data-stu-id="73b09-103">Get started with threat detection</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="73b09-104">Inspekcja</span><span class="sxs-lookup"><span data-stu-id="73b09-104">Auditing</span></span>](sql-data-warehouse-auditing-overview.md)
> * [<span data-ttu-id="73b09-105">Wykrywanie zagrożeń</span><span class="sxs-lookup"><span data-stu-id="73b09-105">Threat detection</span></span>](sql-data-warehouse-security-threat-detection.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="73b09-106">Omówienie</span><span class="sxs-lookup"><span data-stu-id="73b09-106">Overview</span></span>
<span data-ttu-id="73b09-107">Wykrywanie zagrożeń wykrywa nietypowe działania bazy danych wskazujące toohello zagrożenia potencjalnych zabezpieczeń bazy danych.</span><span class="sxs-lookup"><span data-stu-id="73b09-107">Threat Detection detects anomalous database activities indicating potential security threats toohello database.</span></span> <span data-ttu-id="73b09-108">Wykrywanie zagrożeń jest w wersji zapoznawczej i jest obsługiwana dla usługi SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="73b09-108">Threat Detection is in preview and is supported for SQL Data Warehouse.</span></span>

<span data-ttu-id="73b09-109">Wykrywanie zagrożeń udostępnia nową warstwę zabezpieczeń, co umożliwia klientom toodetect i odpowiadać toopotential zagrożeń w miarę ich występowania, zapewniając alerty zabezpieczeń w nietypowych działań.</span><span class="sxs-lookup"><span data-stu-id="73b09-109">Threat Detection provides a new layer of security, which enables customers toodetect and respond toopotential threats as they occur by providing security alerts on anomalous activities.</span></span> <span data-ttu-id="73b09-110">Użytkownicy mogą Eksploruj hello zdarzenia podejrzane przy użyciu [inspekcję magazynu danych SQL Azure](sql-data-warehouse-auditing-overview.md) toodetermine, jeśli są one wynikiem tooaccess próby naruszenia lub wykorzystać hello magazynu danych programu.</span><span class="sxs-lookup"><span data-stu-id="73b09-110">Users can explore hello suspicious events using [Azure SQL Data Warehouse Auditing](sql-data-warehouse-auditing-overview.md) toodetermine if they result from an attempt tooaccess, breach or exploit data in hello data warehouse.</span></span>
<span data-ttu-id="73b09-111">Wykrywanie zagrożeń umożliwia proste tooaddress potencjalne zagrożenia danych toohello magazynu bez toobe potrzeby hello ekspert zabezpieczeń lub zarządzać zabezpieczeniami zaawansowanymi, monitorowanie systemów.</span><span class="sxs-lookup"><span data-stu-id="73b09-111">Threat Detection makes it simple tooaddress potential threats toohello data warehouse without hello need toobe a security expert or manage advanced security monitoring systems.</span></span>

<span data-ttu-id="73b09-112">Na przykład wykrywanie zagrożeń wykrywa niektóre działania nietypowych bazy danych, które wskazują potencjalne prób iniekcji kodu SQL.</span><span class="sxs-lookup"><span data-stu-id="73b09-112">For example, Threat Detection detects certain anomalous database activities indicating potential SQL injection attempts.</span></span> <span data-ttu-id="73b09-113">Iniekcja kodu SQL jest jednym z hello typowych problemów sieci Web aplikacji zabezpieczeń na powitania internetowe, aplikacje używane tooattack opartych na danych.</span><span class="sxs-lookup"><span data-stu-id="73b09-113">SQL injection is one of hello common Web application security issues on hello Internet, used tooattack data-driven applications.</span></span> <span data-ttu-id="73b09-114">Osoby atakujące korzystać z aplikacji tooinject luk w zabezpieczeniach złośliwego instrukcji SQL do pola wejścia aplikacji, naruszenia i modyfikacji danych w bazie danych hello.</span><span class="sxs-lookup"><span data-stu-id="73b09-114">Attackers take advantage of application vulnerabilities tooinject malicious SQL statements into application entry fields, for breaching or modifying data in hello database.</span></span>

## <a name="set-up-threat-detection-for-your-database"></a><span data-ttu-id="73b09-115">Skonfiguruj wykrywanie zagrożeń dla bazy danych</span><span class="sxs-lookup"><span data-stu-id="73b09-115">Set up threat detection for your database</span></span>
1. <span data-ttu-id="73b09-116">Uruchom hello portalu Azure pod adresem [https://portal.azure.com](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="73b09-116">Launch hello Azure Portal at [https://portal.azure.com](https://portal.azure.com).</span></span>
2. <span data-ttu-id="73b09-117">Przejdź bloku konfiguracji toohello hello ma toomonitor usługi SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="73b09-117">Navigate toohello configuration blade of hello SQL Data Warehouse you want toomonitor.</span></span> <span data-ttu-id="73b09-118">W bloku ustawienia hello, wybierz **Inspekcja i wykrywanie zagrożeń**.</span><span class="sxs-lookup"><span data-stu-id="73b09-118">In hello Settings blade, select **Auditing & Threat Detection**.</span></span>
   
    ![Okienko nawigacji][1]
3. <span data-ttu-id="73b09-120">W hello **Inspekcja i wykrywanie zagrożeń** Włącz bloku konfiguracji **ON** inspekcji, które będzie wyświetlane ustawienia wykrywania zagrożeń hello.</span><span class="sxs-lookup"><span data-stu-id="73b09-120">In hello **Auditing & Threat Detection** configuration blade turn **ON** auditing, which will display hello Threat detection settings.</span></span>
   
    ![Okienko nawigacji][2]
4. <span data-ttu-id="73b09-122">Włącz **ON** wykrywanie zagrożeń.</span><span class="sxs-lookup"><span data-stu-id="73b09-122">Turn **ON** Threat detection.</span></span>
5. <span data-ttu-id="73b09-123">Skonfiguruj listę hello wiadomości e-mail, które będą wysyłane alerty zabezpieczeń po wykryciu nietypowych danych magazynu działań.</span><span class="sxs-lookup"><span data-stu-id="73b09-123">Configure hello list of emails that will receive security alerts upon detection of anomalous data warehouse activities.</span></span>
6. <span data-ttu-id="73b09-124">Kliknij przycisk **zapisać** w hello **Inspekcja i wykrywanie zagrożeń** toosave bloku konfiguracji hello nowych lub zaktualizowanych inspekcji i zagrożeń zasady wykrywania.</span><span class="sxs-lookup"><span data-stu-id="73b09-124">Click **Save** in hello **Auditing & Threat detection** configuration blade toosave hello new or updated auditing and threat detection policy.</span></span>
   
    ![Okienko nawigacji][3]

## <a name="explore-anomalous-data-warehouse-activities-upon-detection-of-a-suspicious-event"></a><span data-ttu-id="73b09-126">Eksplorowanie danych nietypowych działań magazynu po wykryciu podejrzanych zdarzeń</span><span class="sxs-lookup"><span data-stu-id="73b09-126">Explore anomalous data warehouse activities upon detection of a suspicious event</span></span>
1. <span data-ttu-id="73b09-127">Otrzymasz wiadomość e-mail z powiadomieniem po wykryciu nietypowe działania bazy danych.</span><span class="sxs-lookup"><span data-stu-id="73b09-127">You will receive an email notification upon detection of anomalous database activities.</span></span> <br/>
   <span data-ttu-id="73b09-128">e-mail Hello dostarcza informacji o zdarzeń zabezpieczeń podejrzane hello tym rodzaj hello hello nietypowych działań, nazwa bazy danych, server name i hello czas trwania zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="73b09-128">hello email will provide information on hello suspicious security event including hello nature of hello anomalous activities, database name, server name and hello event time.</span></span> <span data-ttu-id="73b09-129">Ponadto zawierają informacje dotyczące możliwe przyczyny i zalecane akcje tooinvestigate i ograniczyć hello potencjalne zagrożenie toohello w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="73b09-129">In addition, it will provide information on possible causes and recommended actions tooinvestigate and mitigate hello potential threat toohello database.</span></span><br/>
   
    ![Okienko nawigacji][4]
2. <span data-ttu-id="73b09-131">W wiadomości powitania kliknij hello **dziennik inspekcji SQL Azure** łącza, co spowoduje uruchomienie hello klasycznego portalu Azure i wyświetlić odpowiednie rekordy inspekcji hello wokół czasu hello hello podejrzane zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="73b09-131">In hello email, click on hello **Azure SQL Auditing Log** link, which will launch hello Azure Classic Portal and show hello relevant Auditing records around hello time of hello suspicious event.</span></span>
   
    ![Okienko nawigacji][5]
3. <span data-ttu-id="73b09-133">Polecenie tooview rekordów inspekcji hello więcej szczegółów na powitania bazy danych podejrzane działania, takie jak instrukcji SQL, Niepowodzenie IP Przyczyna i klienta.</span><span class="sxs-lookup"><span data-stu-id="73b09-133">Click on hello audit records tooview more details on hello suspicious database activities such as SQL statement, failure reason and client IP.</span></span>
   
    ![Okienko nawigacji][6]
4. <span data-ttu-id="73b09-135">W bloku rekordów inspekcji powitania kliknij **Otwórz w programie Excel** tooopen wstępnie skonfigurowane w programie excel tooimport szablonu i wykonywania dokładniejszej analizy dziennika inspekcji hello wokół czasu hello hello podejrzane zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="73b09-135">In hello Auditing Records blade, click  **Open in Excel** tooopen a pre-configured excel template tooimport and run deeper analysis of hello audit log around hello time of hello suspicious event.</span></span><br/><span data-ttu-id="73b09-136">
   **Uwaga:** programu Excel 2010 lub nowszej, dodatku Power Query i hello **szybkie łączenie** ustawienie jest wymagane</span><span class="sxs-lookup"><span data-stu-id="73b09-136">
**Note:** In Excel 2010 or later, Power Query and hello **Fast Combine** setting is required</span></span>
   
    ![Okienko nawigacji][7]
5. <span data-ttu-id="73b09-138">Witaj tooconfigure **szybkie łączenie** ustawienie - hello **dodatku POWER QUERY** karty wstążki, wybierz opcję **opcje** toodisplay hello opcje w oknie dialogowym.</span><span class="sxs-lookup"><span data-stu-id="73b09-138">tooconfigure hello **Fast Combine** setting - In hello **POWER QUERY** ribbon tab, select **Options** toodisplay hello Options dialog.</span></span> <span data-ttu-id="73b09-139">Zaznacz hello sekcji prywatności i wybierz opcję drugi hello — "Ignoruj hello poziomów prywatności i potencjalne poprawianie wydajności":</span><span class="sxs-lookup"><span data-stu-id="73b09-139">Select hello Privacy section and choose hello second option - 'Ignore hello Privacy Levels and potentially improve performance':</span></span>
   
    ![Okienko nawigacji][8]
6. <span data-ttu-id="73b09-141">tooload dzienników inspekcji SQL, upewnij się, że parametry hello na karcie Ustawienia hello są poprawnie ustawione i wybierz wstążki "Dane" hello i kliknij przycisk "Odśwież wszystko" hello.</span><span class="sxs-lookup"><span data-stu-id="73b09-141">tooload SQL audit logs, ensure that hello parameters in hello settings tab are set correctly and then select hello 'Data' ribbon and click hello 'Refresh All' button.</span></span>
   
    ![Okienko nawigacji][9]
7. <span data-ttu-id="73b09-143">Witaj wyniki są wyświetlane na powitania **dzienników inspekcji SQL** arkusza, co pozwala toorun dokładniejszej analizy hello nietypowych działań, które zostały wykryte i ograniczyć wpływ hello hello zdarzeń zabezpieczeń w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="73b09-143">hello results appear in hello **SQL Audit Logs** sheet which enables you toorun deeper analysis of hello anomalous activities that were detected, and mitigate hello impact of hello security event in your application.</span></span>

<!--Image references-->
[1]: ./media/sql-data-warehouse-security-threat-detection/1_td_click_on_settings.png
[2]: ./media/sql-data-warehouse-security-threat-detection/2_td_turn_on_auditing.png
[3]: ./media/sql-data-warehouse-security-threat-detection/3_td_turn_on_threat_detection.png
[4]: ./media/sql-data-warehouse-security-threat-detection/4_td_email.png
[5]: ./media/sql-data-warehouse-security-threat-detection/5_td_audit_records.png
[6]: ./media/sql-data-warehouse-security-threat-detection/6_td_audit_record_details.png
[7]: ./media/sql-data-warehouse-security-threat-detection/7_td_audit_records_open_excel.png
[8]: ./media/sql-data-warehouse-security-threat-detection/8_td_excel_fast_combine.png
[9]: ./media/sql-data-warehouse-security-threat-detection/9_td_excel_parameters.png
