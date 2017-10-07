---
title: "Wprowadzenie do raportów usługi Azure Active Directory | Microsoft Docs"
description: "Wyświetla hello raportów dostępnych w usłudze Azure Active Directory"
services: active-directory
documentationcenter: 
author: dhanyahk
manager: femila
editor: 
ms.assetid: 7ac99919-8df5-4424-9298-fc7c025ba949
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/16/2017
ms.author: dhanyahk;markvi
ms.openlocfilehash: f47875708398391dd7f3efdc56a741fdba273b76
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-active-directory-reporting"></a><span data-ttu-id="25bc1-103">Wprowadzenie do raportów usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="25bc1-103">Getting started with Azure Active Directory Reporting</span></span>
## <a name="what-it-is"></a><span data-ttu-id="25bc1-104">Co to jest</span><span class="sxs-lookup"><span data-stu-id="25bc1-104">What it is</span></span>
<span data-ttu-id="25bc1-105">W usłudze Azure Active Directory (Azure AD) uwzględniono raporty dotyczące zabezpieczeń, działań i inspekcji dla katalogu.</span><span class="sxs-lookup"><span data-stu-id="25bc1-105">Azure Active Directory (Azure AD) includes security, activity, and audit reports for your directory.</span></span> <span data-ttu-id="25bc1-106">Poniżej przedstawiono listę raportów hello uwzględnionych:</span><span class="sxs-lookup"><span data-stu-id="25bc1-106">Here's a list of hello reports included:</span></span>

### <a name="security-reports"></a><span data-ttu-id="25bc1-107">Raporty dotyczące zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="25bc1-107">Security reports</span></span>
* <span data-ttu-id="25bc1-108">Logowania z nieznanych źródeł</span><span class="sxs-lookup"><span data-stu-id="25bc1-108">Sign-ins from unknown sources</span></span>
* <span data-ttu-id="25bc1-109">Logowania po wielokrotnych niepowodzeniach</span><span class="sxs-lookup"><span data-stu-id="25bc1-109">Sign-ins after multiple failures</span></span>
* <span data-ttu-id="25bc1-110">Logowania z wielu lokalizacji geograficznych</span><span class="sxs-lookup"><span data-stu-id="25bc1-110">Sign-ins from multiple geographies</span></span>
* <span data-ttu-id="25bc1-111">Logowania z adresów IP związanych z podejrzanymi działaniami</span><span class="sxs-lookup"><span data-stu-id="25bc1-111">Sign-ins from IP addresses with suspicious activity</span></span>
* <span data-ttu-id="25bc1-112">Nieregularne działania związane z logowaniem</span><span class="sxs-lookup"><span data-stu-id="25bc1-112">Irregular sign-in activity</span></span>
* <span data-ttu-id="25bc1-113">Logowania z urządzeń, które mogą być zainfekowane</span><span class="sxs-lookup"><span data-stu-id="25bc1-113">Sign-ins from possibly infected devices</span></span>
* <span data-ttu-id="25bc1-114">Nietypowe działania użytkowników związane z logowaniem</span><span class="sxs-lookup"><span data-stu-id="25bc1-114">Users with anomalous sign-in activity</span></span>

### <a name="activity-reports"></a><span data-ttu-id="25bc1-115">Raporty dotyczące działań</span><span class="sxs-lookup"><span data-stu-id="25bc1-115">Activity reports</span></span>
* <span data-ttu-id="25bc1-116">Podsumowanie użycia aplikacji</span><span class="sxs-lookup"><span data-stu-id="25bc1-116">Application usage: summary</span></span>
* <span data-ttu-id="25bc1-117">Szczegóły użycia aplikacji</span><span class="sxs-lookup"><span data-stu-id="25bc1-117">Application usage: detailed</span></span>
* <span data-ttu-id="25bc1-118">Pulpit nawigacyjny aplikacji</span><span class="sxs-lookup"><span data-stu-id="25bc1-118">Application dashboard</span></span>
* <span data-ttu-id="25bc1-119">Błędy aprowizacji kont</span><span class="sxs-lookup"><span data-stu-id="25bc1-119">Account provisioning errors</span></span>
* <span data-ttu-id="25bc1-120">Urządzenia indywidualnych użytkowników</span><span class="sxs-lookup"><span data-stu-id="25bc1-120">Individual user devices</span></span>
* <span data-ttu-id="25bc1-121">Działania indywidualnych użytkowników</span><span class="sxs-lookup"><span data-stu-id="25bc1-121">Individual user Activity</span></span>
* <span data-ttu-id="25bc1-122">Raport dotyczący działań grup</span><span class="sxs-lookup"><span data-stu-id="25bc1-122">Groups activity report</span></span>
* <span data-ttu-id="25bc1-123">Raport dotyczący działań związanych z rejestracją resetowania haseł</span><span class="sxs-lookup"><span data-stu-id="25bc1-123">Password Reset Registration Activity Report</span></span>
* <span data-ttu-id="25bc1-124">Działania związane z resetowaniem haseł</span><span class="sxs-lookup"><span data-stu-id="25bc1-124">Password reset activity</span></span>

### <a name="audit-reports"></a><span data-ttu-id="25bc1-125">Raporty dotyczące inspekcji</span><span class="sxs-lookup"><span data-stu-id="25bc1-125">Audit reports</span></span>
* <span data-ttu-id="25bc1-126">Raport dotyczący inspekcji katalogu</span><span class="sxs-lookup"><span data-stu-id="25bc1-126">Directory audit report</span></span>

> [!TIP]
> <span data-ttu-id="25bc1-127">Więcej informacji dotyczących dokumentacji raportów usługi Azure AD zawiera temat [Wyświetlanie raportów dotyczących dostępu i użycia](active-directory-view-access-usage-reports.md).</span><span class="sxs-lookup"><span data-stu-id="25bc1-127">For more documentation on Azure AD Reporting, check out [View your access and usage reports](active-directory-view-access-usage-reports.md).</span></span>
> 
> 

## <a name="how-it-works"></a><span data-ttu-id="25bc1-128">Jak to działa</span><span class="sxs-lookup"><span data-stu-id="25bc1-128">How it works</span></span>
### <a name="reporting-pipeline"></a><span data-ttu-id="25bc1-129">Potok raportowania</span><span class="sxs-lookup"><span data-stu-id="25bc1-129">Reporting pipeline</span></span>
<span data-ttu-id="25bc1-130">Witaj potok raportowania składa się z trzech głównych kroków.</span><span class="sxs-lookup"><span data-stu-id="25bc1-130">hello reporting pipeline consists of three main steps.</span></span> <span data-ttu-id="25bc1-131">Każdym zalogowaniu użytkownika lub uwierzytelnianie jest dokonywane, hello wykonywane są następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="25bc1-131">Every time a user signs in, or an authentication is made, hello following happens:</span></span>

* <span data-ttu-id="25bc1-132">Najpierw hello użytkownik jest uwierzytelniany (pomyślnie lub nie) i hello wynik jest zapisywany w bazach danych usługi Azure Active Directory hello.</span><span class="sxs-lookup"><span data-stu-id="25bc1-132">First, hello user is authenticated (successfully or unsuccessfully), and hello result is stored in hello Azure Active Directory service databases.</span></span>
* <span data-ttu-id="25bc1-133">W regularnych odstępach czasu przetwarzane są wszystkie ostatnie logowania.</span><span class="sxs-lookup"><span data-stu-id="25bc1-133">At regular intervals, all recent sign ins are processed.</span></span> <span data-ttu-id="25bc1-134">W tym momencie nasze algorytmy analizy zabezpieczeń i nietypowych działań przeszukują wszystkie ostatnie logowania pod kątem podejrzanych działań.</span><span class="sxs-lookup"><span data-stu-id="25bc1-134">At this point, our security and anomalous activity algorithms are searching all recent sign ins for suspicious activity.</span></span>
* <span data-ttu-id="25bc1-135">Po zakończeniu przetwarzania hello raporty są zapisywane, w pamięci podręcznej, a następnie w hello klasycznego portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="25bc1-135">After processing, hello reports are written, cached, and served in hello Azure classic portal.</span></span>

### <a name="report-generation-times"></a><span data-ttu-id="25bc1-136">Czas trwania generowania raportów</span><span class="sxs-lookup"><span data-stu-id="25bc1-136">Report generation times</span></span>
<span data-ttu-id="25bc1-137">Ze względu na dużą toohello liczbę uwierzytelnień i zaloguj się, że ins przetworzonych przez program hello platformy Azure AD hello najnowszych przetwarzane sesje logowania są, średnio o jedną godzinę.</span><span class="sxs-lookup"><span data-stu-id="25bc1-137">Due toohello large volume of authentications and sign ins processed by hello Azure AD platform, hello most recent sign-ins processed are, on average, one hour old.</span></span> <span data-ttu-id="25bc1-138">W rzadkich przypadkach może potrwać too8 godziny tooprocess hello ostatniego logowania.</span><span class="sxs-lookup"><span data-stu-id="25bc1-138">In rare cases, it may take up too8 hours tooprocess hello most recent sign-ins.</span></span>

<span data-ttu-id="25bc1-139">Logowanie hello najnowsze przetworzone można znaleźć, sprawdzając tekst pomocy hello na powitania na początku każdego raportu.</span><span class="sxs-lookup"><span data-stu-id="25bc1-139">You can find hello most recent processed sign-in by examining hello help text at hello top of each report.</span></span>

![Tekst pomocy na powitania na początku każdego raportu](./media/active-directory-reporting-getting-started/reportingWatermark.PNG)

> [!TIP]
> <span data-ttu-id="25bc1-141">Więcej informacji dotyczących dokumentacji raportów usługi Azure AD zawiera temat [Wyświetlanie raportów dotyczących dostępu i użycia](active-directory-view-access-usage-reports.md).</span><span class="sxs-lookup"><span data-stu-id="25bc1-141">For more documentation on Azure AD Reporting, check out [View your access and usage reports](active-directory-view-access-usage-reports.md).</span></span>
> 
> 

## <a name="getting-started"></a><span data-ttu-id="25bc1-142">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="25bc1-142">Getting started</span></span>
### <a name="sign-into-hello-azure-classic-portal"></a><span data-ttu-id="25bc1-143">Zaloguj się do hello klasycznego portalu Azure</span><span class="sxs-lookup"><span data-stu-id="25bc1-143">Sign into hello Azure classic portal</span></span>
<span data-ttu-id="25bc1-144">Najpierw należy toosign do hello [klasycznego portalu Azure](https://manage.windowsazure.com) jako administrator globalny lub zgodności.</span><span class="sxs-lookup"><span data-stu-id="25bc1-144">First, you'll need toosign into hello [Azure classic portal](https://manage.windowsazure.com)  as a global or compliance administrator.</span></span> <span data-ttu-id="25bc1-145">Możesz również musi być administratorem usługi subskrypcji platformy Azure lub współadministratorem lub używać hello "dostępu tooAzure AD" subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="25bc1-145">You must also be an Azure subscription service administrator or co-administrator, or be using hello "Access tooAzure AD" Azure subscription.</span></span>

### <a name="navigate-tooreports"></a><span data-ttu-id="25bc1-146">Przejdź tooReports</span><span class="sxs-lookup"><span data-stu-id="25bc1-146">Navigate tooReports</span></span>
<span data-ttu-id="25bc1-147">tooview raporty, przejdź na karcie raporty toohello u góry hello katalogu.</span><span class="sxs-lookup"><span data-stu-id="25bc1-147">tooview Reports, navigate toohello Reports tab at hello top of your directory.</span></span>

<span data-ttu-id="25bc1-148">Jeśli jest to pierwsza wyświetlania raportów hello, musisz okno dialogowe tooa tooagree Aby móc wyświetlać raporty hello.</span><span class="sxs-lookup"><span data-stu-id="25bc1-148">If this is your first time viewing hello reports, you'll need tooagree tooa dialog box before you can view hello reports.</span></span> <span data-ttu-id="25bc1-149">To jest możliwa do administratorów w Twojej organizacji tooview tooensure te dane, które mogą być uznawane za informacje osobiste w niektórych krajach.</span><span class="sxs-lookup"><span data-stu-id="25bc1-149">This is tooensure that it's acceptable for admins in your organization tooview this data, which may be considered private information in some countries.</span></span>

![Okno dialogowe](./media/active-directory-reporting-getting-started/dialogBox.png)

### <a name="explore-each-report"></a><span data-ttu-id="25bc1-151">Eksplorowanie każdego raportu</span><span class="sxs-lookup"><span data-stu-id="25bc1-151">Explore each report</span></span>
<span data-ttu-id="25bc1-152">Przejdź do każdego raportu toosee hello zbieranych danych i przetwarzane sesje logowania hello.</span><span class="sxs-lookup"><span data-stu-id="25bc1-152">Navigate into each report toosee hello data being collected and hello sign-ins processed.</span></span> <span data-ttu-id="25bc1-153">Można znaleźć [listę wszystkich raportów tutaj hello](active-directory-reporting-guide.md).</span><span class="sxs-lookup"><span data-stu-id="25bc1-153">You can find a [list of all hello reports here](active-directory-reporting-guide.md).</span></span>

![Wszystkie raporty](./media/active-directory-reporting-getting-started/reportsMain.png)

### <a name="download-hello-reports-as-csv"></a><span data-ttu-id="25bc1-155">Pobierz raporty hello jako woluminu CSV</span><span class="sxs-lookup"><span data-stu-id="25bc1-155">Download hello reports as CSV</span></span>
<span data-ttu-id="25bc1-156">Każdy raport można pobrać jako plik CSV (wartości rozdzielane przecinkami).</span><span class="sxs-lookup"><span data-stu-id="25bc1-156">Each report can be downloaded as a CSV (comma-separated value) file.</span></span> <span data-ttu-id="25bc1-157">Można używać tych plików w programie Excel, usługa Power bi lub programy toofurther analizowania danych analitycznych innych firm.</span><span class="sxs-lookup"><span data-stu-id="25bc1-157">You can use these files in Excel, PowerBI or third-party analysis programs toofurther analyze your data.</span></span>

<span data-ttu-id="25bc1-158">toodownload żadnego raportu jako woluminu CSV, przejdź toohello raportu i kliknij przycisk "Pobierz" u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="25bc1-158">toodownload any report as a CSV, navigate toohello report and click "Download" at hello bottom.</span></span>

![Przycisk Pobierz](./media/active-directory-reporting-getting-started/downloadButton.png)

> [!TIP]
> <span data-ttu-id="25bc1-160">Więcej informacji dotyczących dokumentacji raportów usługi Azure AD zawiera temat [Wyświetlanie raportów dotyczących dostępu i użycia](active-directory-view-access-usage-reports.md).</span><span class="sxs-lookup"><span data-stu-id="25bc1-160">For more documentation on Azure AD Reporting, check out [View your access and usage reports](active-directory-view-access-usage-reports.md).</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="25bc1-161">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="25bc1-161">Next steps</span></span>
### <a name="customize-alerts-for-anomalous-sign-in-activity"></a><span data-ttu-id="25bc1-162">Dostosowywanie alertów dotyczących nietypowych działań związanych z logowaniem</span><span class="sxs-lookup"><span data-stu-id="25bc1-162">Customize alerts for anomalous sign in activity</span></span>
<span data-ttu-id="25bc1-163">Przejdź toohello karty "Konfiguruj" katalogu.</span><span class="sxs-lookup"><span data-stu-id="25bc1-163">Navigate toohello "Configure" tab of your directory.</span></span>

<span data-ttu-id="25bc1-164">Przewiń w sekcji "Powiadomienia" toohello.</span><span class="sxs-lookup"><span data-stu-id="25bc1-164">Scroll toohello "Notifications" section.</span></span>

<span data-ttu-id="25bc1-165">Włącz lub wyłącz sekcji "Powiadomienia E-mail o nietypowych logowania" hello.</span><span class="sxs-lookup"><span data-stu-id="25bc1-165">Enable or disable hello "Email Notifications of Anomalous sign-ins" section.</span></span>

![Witaj sekcja powiadomienia](./media/active-directory-reporting-getting-started/notificationsSection.png)

### <a name="integrate-with-hello-azure-ad-reporting-api"></a><span data-ttu-id="25bc1-167">Integracja z hello Azure AD interfejsu API raportowania</span><span class="sxs-lookup"><span data-stu-id="25bc1-167">Integrate with hello Azure AD Reporting API</span></span>
<span data-ttu-id="25bc1-168">Zobacz [wprowadzenie hello interfejsu API raportowania](active-directory-reporting-api-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="25bc1-168">See [Getting started with hello Reporting API](active-directory-reporting-api-getting-started.md).</span></span>

### <a name="engage-multi-factor-authentication-on-users"></a><span data-ttu-id="25bc1-169">Włączanie usługi Multi-Factor Authentication dla użytkowników</span><span class="sxs-lookup"><span data-stu-id="25bc1-169">Engage Multi-Factor Authentication on users</span></span>
<span data-ttu-id="25bc1-170">Wybierz użytkownika w raporcie.</span><span class="sxs-lookup"><span data-stu-id="25bc1-170">Select a user in a report.</span></span>

<span data-ttu-id="25bc1-171">Kliknij przycisk "Włącz usługę MFA" hello u dołu hello hello ekranu.</span><span class="sxs-lookup"><span data-stu-id="25bc1-171">Click hello "Enable MFA" button at hello bottom of hello screen.</span></span>

![przycisk usługi Multi-Factor Authentication Hello u dołu hello hello ekranu](./media/active-directory-reporting-getting-started/mfaButton.png)

> [!TIP]
> <span data-ttu-id="25bc1-173">Więcej informacji dotyczących dokumentacji raportów usługi Azure AD zawiera temat [Wyświetlanie raportów dotyczących dostępu i użycia](active-directory-view-access-usage-reports.md).</span><span class="sxs-lookup"><span data-stu-id="25bc1-173">For more documentation on Azure AD Reporting, check out [View your access and usage reports](active-directory-view-access-usage-reports.md).</span></span>
> 
> 

## <a name="learn-more"></a><span data-ttu-id="25bc1-174">Dowiedz się więcej</span><span class="sxs-lookup"><span data-stu-id="25bc1-174">Learn more</span></span>
### <a name="audit-events"></a><span data-ttu-id="25bc1-175">Inspekcja zdarzeń</span><span class="sxs-lookup"><span data-stu-id="25bc1-175">Audit events</span></span>
<span data-ttu-id="25bc1-176">Dowiedz się, jakie zdarzenia są poddawane inspekcji w katalogu hello [Azure Active Directory zdarzenia inspekcji raportowania](active-directory-reporting-audit-events.md).</span><span class="sxs-lookup"><span data-stu-id="25bc1-176">Learn about what events are audited in hello directory in [Azure Active Directory Reporting Audit Events](active-directory-reporting-audit-events.md).</span></span>

### <a name="api-integration"></a><span data-ttu-id="25bc1-177">Integracja z interfejsem API</span><span class="sxs-lookup"><span data-stu-id="25bc1-177">API Integration</span></span>
<span data-ttu-id="25bc1-178">Zobacz [wprowadzenie hello interfejsu API raportowania](active-directory-reporting-api-getting-started.md) i hello [dokumentacji interfejsu API](https://msdn.microsoft.com/library/azure/mt126081.aspx).</span><span class="sxs-lookup"><span data-stu-id="25bc1-178">See [Getting started with hello Reporting API](active-directory-reporting-api-getting-started.md) and hello [API reference documentation](https://msdn.microsoft.com/library/azure/mt126081.aspx).</span></span>

### <a name="get-in-touch"></a><span data-ttu-id="25bc1-179">Kontakt</span><span class="sxs-lookup"><span data-stu-id="25bc1-179">Get in touch</span></span>
<span data-ttu-id="25bc1-180">Jeśli chcesz przesłać opinię, potrzebujesz pomocy lub masz pytania, wyślij wiadomość e-mail na adres [aadreportinghelp@microsoft.com](mailto:aadreportinghelp@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="25bc1-180">Email [aadreportinghelp@microsoft.com](mailto:aadreportinghelp@microsoft.com) for feedback, help, or any questions you might have.</span></span>

> [!TIP]
> <span data-ttu-id="25bc1-181">Więcej informacji dotyczących dokumentacji raportów usługi Azure AD zawiera temat [Wyświetlanie raportów dotyczących dostępu i użycia](active-directory-view-access-usage-reports.md).</span><span class="sxs-lookup"><span data-stu-id="25bc1-181">For more documentation on Azure AD Reporting, check out [View your access and usage reports](active-directory-view-access-usage-reports.md).</span></span>
> 
> 

