---
title: "Korzystanie z pakietu zawartości usługi Power BI dla usługi Azure Active Directory | Microsoft Docs"
description: "Dowiedz się, jak używać pakietu zawartości usługi Power BI dla usługi Azure Active Directory"
services: active-directory
author: MarkusVi
manager: femila
ms.assetid: addd60fe-d5ac-4b8b-983c-0736c80ace02
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/15/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 5c642bb814a279756e8391f12fdc86b6ec0b4a8f
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-use-the-azure-active-directory-power-bi-content-pack"></a><span data-ttu-id="2e49f-103">Korzystanie z pakietu zawartości usługi Power BI dla usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2e49f-103">How to use the Azure Active Directory Power BI Content Pack</span></span>

<span data-ttu-id="2e49f-104">Zrozumienie, jak użytkownicy korzystają z funkcji usługi Azure Active Directory, jest bardzo ważne dla Ciebie jako administratora IT.</span><span class="sxs-lookup"><span data-stu-id="2e49f-104">Understanding how your users adopt and use Azure Active Directory features is critical for you as an IT admin.</span></span> <span data-ttu-id="2e49f-105">Dzięki temu można zaplanować infrastrukturę IT oraz komunikację w celu zwiększenia użycia i maksymalnego wykorzystania funkcji usługi AAD.</span><span class="sxs-lookup"><span data-stu-id="2e49f-105">It allows you to plan your IT infrastructure and communication to increase usage and to get the most out of AAD features.</span></span> <span data-ttu-id="2e49f-106">Pakiet zawartości usługi Power BI dla usługi Azure Active Directory umożliwia pogłębioną analizę danych, ułatwiającą zrozumienie sposobu działania usługi Azure Active Directory w przypadku różnych funkcji, na których polegasz.</span><span class="sxs-lookup"><span data-stu-id="2e49f-106">Power BI Content Pack for Azure Active Directory gives you the ability to further analyze your data to understand how you can use this data to gather richer insights into what’s going on with their Azure Active Directory for the various capabilities you heavily rely on.</span></span>  <span data-ttu-id="2e49f-107">Dzięki integracji interfejsów API usługi Azure Active Directory z usługą Power BI można łatwo pobrać gotowe pakiety zawartości i uzyskać informacje o wszystkich działaniach usługi Azure Active Directory za pomocą rozbudowanego środowiska wizualizacji oferowanego przez usługę Power BI.</span><span class="sxs-lookup"><span data-stu-id="2e49f-107">With the integration of Azure Active Directory APIs into Power BI, you can easily download the pre-built content packs and gain insights to all the activities within your Azure Active Directory using rich visualization experience Power BI offers.</span></span> <span data-ttu-id="2e49f-108">Możesz utworzyć własny pulpit nawigacyjny i w prosty sposób udostępnić go innym osobom w organizacji.</span><span class="sxs-lookup"><span data-stu-id="2e49f-108">You can create your own dashboard and share it easily with anyone in your organization.</span></span> 

<span data-ttu-id="2e49f-109">W tym temacie przedstawiono instrukcje krok po kroku dotyczące instalacji i używania pakietu zawartości w danym środowisku.</span><span class="sxs-lookup"><span data-stu-id="2e49f-109">This topic provides you with step-by-step instructions on how to install and use the content pack in your environment.</span></span>

## <a name="installation"></a><span data-ttu-id="2e49f-110">Instalacja</span><span class="sxs-lookup"><span data-stu-id="2e49f-110">Installation</span></span>  

<span data-ttu-id="2e49f-111">**Aby zainstalować pakiet zawartości usługi Power BI:**</span><span class="sxs-lookup"><span data-stu-id="2e49f-111">**To install the Power BI Content Pack:**</span></span>

1. <span data-ttu-id="2e49f-112">Zaloguj się do [usługi Power BI](https://app.powerbi.com/groups/me/getdata/services) za pomocą konta Power BI (jest to to samo konto, co w przypadku usługi O365 lub Azure AD).</span><span class="sxs-lookup"><span data-stu-id="2e49f-112">Log into [Power BI](https://app.powerbi.com/groups/me/getdata/services) with your Power BI Account (this is the same account as your O365 or Azure AD Account).</span></span>

2. <span data-ttu-id="2e49f-113">W dolnej części okienka nawigacji po lewej stronie wybierz opcję **Pobierz dane**.</span><span class="sxs-lookup"><span data-stu-id="2e49f-113">At the bottom of the left navigation pane, select **Get Data**.</span></span>

    ![Pakiet zawartości usługi Power BI dla usługi Azure Active Directory](./media/active-directory-reporting-power-bi-content-pack-how-to/01.png)
 
3. <span data-ttu-id="2e49f-115">W polu **Usługi** kliknij opcję **Pobierz**.</span><span class="sxs-lookup"><span data-stu-id="2e49f-115">In the **Services** box, click **Get**.</span></span>
   
    ![Pakiet zawartości usługi Power BI dla usługi Azure Active Directory](./media/active-directory-reporting-power-bi-content-pack-how-to/02.png)

4.  <span data-ttu-id="2e49f-117">Wyszukaj usługę **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="2e49f-117">Search for **Azure Active Directory**.</span></span>

    ![Pakiet zawartości usługi Power BI dla usługi Azure Active Directory](./media/active-directory-reporting-power-bi-content-pack-how-to/03.png)
 
5.  <span data-ttu-id="2e49f-119">Po wyświetleniu monitu wpisz swój identyfikator dzierżawy Azure AD, a następnie kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="2e49f-119">When prompted, type your Azure AD Tenant ID, and then click **Next**.</span></span>

    > [!TIP] 
    > <span data-ttu-id="2e49f-120">Szybkim sposobem uzyskania identyfikatora dzierżawy dla dzierżawcy usługi Office 365/Azure AD jest zalogowanie się do portalu usługi Azure AD, przejście do katalogu i skopiowanie identyfikatora z następującego adresu URL: https://manage.windowsazure.com/woodgroveonline.com#Workspaces/ActiveDirectoryExtension/Directory/<tenantid>/directoryQuickStart</span><span class="sxs-lookup"><span data-stu-id="2e49f-120">A quick way to get the Tenant Id for your Office 365 / Azure AD tenant is to login to the Azure AD Portal, drill down to the directory and copy the ID from the following URL: https://manage.windowsazure.com/woodgroveonline.com#Workspaces/ActiveDirectoryExtension/Directory/<tenantid>/directoryQuickStart</span></span>

    ![Pakiet zawartości usługi Power BI dla usługi Azure Active Directory](./media/active-directory-reporting-power-bi-content-pack-how-to/04.png) 

6.  <span data-ttu-id="2e49f-122">Kliknij przycisk **Zaloguj**.</span><span class="sxs-lookup"><span data-stu-id="2e49f-122">Click **Sign-in**.</span></span> 
 
    ![Pakiet zawartości usługi Power BI dla usługi Azure Active Directory](./media/active-directory-reporting-power-bi-content-pack-how-to/05.png) 



7.  <span data-ttu-id="2e49f-124">Wprowadź nazwę użytkownika i hasło, a następnie kliknij przycisk **Zaloguj**.</span><span class="sxs-lookup"><span data-stu-id="2e49f-124">Enter your username and password, and then click **Sign in**.</span></span>
 
    ![Pakiet zawartości usługi Power BI dla usługi Azure Active Directory](./media/active-directory-reporting-power-bi-content-pack-how-to/06.png) 

8.  <span data-ttu-id="2e49f-126">W oknie dialogowym zgody na aplikację kliknij przycisk **Akceptuj**.</span><span class="sxs-lookup"><span data-stu-id="2e49f-126">On the app consent dialog, click **Accept**.</span></span>
 
9.  <span data-ttu-id="2e49f-127">Po utworzeniu pulpitu nawigacyjnego dzienników aktywności usługi Azure Active Directory kliknij go.</span><span class="sxs-lookup"><span data-stu-id="2e49f-127">When your Azure Active Directory Activity logs dashboard has been created, click it.</span></span>
 
    ![Pakiet zawartości usługi Power BI dla usługi Azure Active Directory](./media/active-directory-reporting-power-bi-content-pack-how-to/08.png) 

## <a name="what-can-i-do-with-this-content-pack"></a><span data-ttu-id="2e49f-129">Co można zrobić z tym pakietem zawartości?</span><span class="sxs-lookup"><span data-stu-id="2e49f-129">What can I do with this content pack?</span></span>

<span data-ttu-id="2e49f-130">Zanim przejdziemy do tego, co można zrobić z tym pakietem zawartości, omówimy pokrótce znajdujące się w nim raporty.</span><span class="sxs-lookup"><span data-stu-id="2e49f-130">Before we jump into what you can do with this content pack, here’s quick preview of the various reports in the content pack.</span></span> <span data-ttu-id="2e49f-131">Dane raportu dotyczą **ostatnich 30 dni**.</span><span class="sxs-lookup"><span data-stu-id="2e49f-131">Report data goes back to the **last 30 days**.</span></span>

### <a name="reports-included-in-this-version-of-azure-active-directory-logs-content-pack"></a><span data-ttu-id="2e49f-132">Raporty zawarte w tej wersji pakietu zawartości usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2e49f-132">Reports included in this version of Azure Active Directory logs Content Pack</span></span>

<span data-ttu-id="2e49f-133">**App Usage and Trend report** (Raport dotyczący użycia i trendu aplikacji): uzyskaj wgląd w aplikacje używane w organizacji oraz dowiedz się, które są najczęściej używane i kiedy.</span><span class="sxs-lookup"><span data-stu-id="2e49f-133">**App Usage and Trend report**:  Get insights into the apps used in your organization and which ones are being used the most and when.</span></span> <span data-ttu-id="2e49f-134">Ten raport służy do gromadzenia informacji dotyczących sposobu używania aplikacji, które zostały niedawno wdrożone w organizacji, lub sprawdzenia popularności poszczególnych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="2e49f-134">You can use this report to gather insights into how an app you recently rolled out in your organization is being used or find out which apps are popular.</span></span> <span data-ttu-id="2e49f-135">W ten sposób można poprawić sposób korzystania z nich, jeśli dana aplikacja nie jest używana.</span><span class="sxs-lookup"><span data-stu-id="2e49f-135">By doing this, you can improve usage if you see if the app is not being used.</span></span>

<span data-ttu-id="2e49f-136">**Sign-ins by location and users** (Logowania według lokalizacji i użytkowników): uzyskaj wgląd w informacje o wszystkich logowaniach wykonywanych przy użyciu tożsamości Azure i poznaj tożsamość użytkowników.</span><span class="sxs-lookup"><span data-stu-id="2e49f-136">**Sign-ins by location and users**: Get insights into all the sign-ins performed using Azure Identity and gives insights into the identity of the users.</span></span> <span data-ttu-id="2e49f-137">Dzięki temu możesz zagłębić się w szczegóły poszczególnych logowań i odpowiedzieć na pytania:</span><span class="sxs-lookup"><span data-stu-id="2e49f-137">With this, you can dig deeper into individual sign-ins and answer questions like:</span></span>

- <span data-ttu-id="2e49f-138">Skąd loguje się dany użytkownik?</span><span class="sxs-lookup"><span data-stu-id="2e49f-138">From where did this user sign-ins?</span></span>
- <span data-ttu-id="2e49f-139">Który użytkownik logował się najczęściej i skąd następowały logowania?</span><span class="sxs-lookup"><span data-stu-id="2e49f-139">Which user has the most sign-ins and where do they sign-in from?</span></span> 
- <span data-ttu-id="2e49f-140">Czy logowanie zakończyło się pomyślnie?</span><span class="sxs-lookup"><span data-stu-id="2e49f-140">Was the sign-in successful?</span></span>  
 
<span data-ttu-id="2e49f-141">Możesz przejść do szczegółów, klikając określoną datę lub lokalizację.</span><span class="sxs-lookup"><span data-stu-id="2e49f-141">You can drill into details by clicking on a specific date or location.</span></span>

<span data-ttu-id="2e49f-142">**Unique users per app** (Liczba unikatowych użytkowników aplikacji): wyświetla wszystkich unikatowych użytkowników korzystających z danej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="2e49f-142">**Unique users per app**:  Get a view of all unique users using a given app.</span></span> <span data-ttu-id="2e49f-143">Dotyczy tylko użytkowników, którzy *pomyślnie* zalogowali się do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="2e49f-143">This includes only users who have “*successfully*” signed into an application.</span></span>

<span data-ttu-id="2e49f-144">**Device sign-ins** (Logowania do urządzeń): wyświetla typ systemu operacyjnego i przeglądarki używane przez użytkowników w organizacji oraz szczegółowe informacje dotyczące użytkowników, takie jak:</span><span class="sxs-lookup"><span data-stu-id="2e49f-144">**Device sign-ins**: Get a view of the type of OS and browsers are being used by users in your organization with detailed information on the users including:</span></span>

- <span data-ttu-id="2e49f-145">Nazwa użytkownika</span><span class="sxs-lookup"><span data-stu-id="2e49f-145">User Name</span></span>
- <span data-ttu-id="2e49f-146">Adres IP</span><span class="sxs-lookup"><span data-stu-id="2e49f-146">IP Address</span></span>
- <span data-ttu-id="2e49f-147">Lokalizacja</span><span class="sxs-lookup"><span data-stu-id="2e49f-147">Location</span></span> 
- <span data-ttu-id="2e49f-148">Stan logowania</span><span class="sxs-lookup"><span data-stu-id="2e49f-148">Sign-in status</span></span> 

<span data-ttu-id="2e49f-149">Dzięki temu raportowi można zapoznać się z różnymi profilami urządzeń używanych w organizacji i określić zasady zarządzania urządzeniami w oparciu o informacje o ich użyciu.</span><span class="sxs-lookup"><span data-stu-id="2e49f-149">With this report, you can understand the various device profiles used within your organization and determine device policies based on what’s used</span></span>

<span data-ttu-id="2e49f-150">**SSPR Funnel** (Lejek SSPR): pomaga w zrozumieniu procesu resetowania haseł w Twojej organizacji.</span><span class="sxs-lookup"><span data-stu-id="2e49f-150">**SSPR Funnel**: Get an understanding on how password resets are being done in your organization.</span></span> <span data-ttu-id="2e49f-151">Dowiedz się, ile wystąpiło prób resetowania haseł przy użyciu narzędzia SSPR oraz ile spośród nich zakończyło się pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="2e49f-151">Get a peek into how many password resets were attempted through the SSPR tool and how many of them were successful.</span></span> <span data-ttu-id="2e49f-152">Posługując się raportem, przeanalizuj próby zresetowania hasła zakończone niepowodzeniem i poznaj ich przyczyny.</span><span class="sxs-lookup"><span data-stu-id="2e49f-152">Dig deeper into the Password resets failure using the SSPR funnel and understand why certain failures occurred.</span></span> <span data-ttu-id="2e49f-153">Ten raport pozwala lepiej zrozumieć sposób używania narzędzia SSPR w organizacji, co może pomóc w podejmowaniu prawidłowych decyzji.</span><span class="sxs-lookup"><span data-stu-id="2e49f-153">This report gives a deeper understanding of how the SSPR tool is used within your organization so you can make the right decisions.</span></span>

## <a name="customizing-azure-ad-activity-content-pack"></a><span data-ttu-id="2e49f-154">Dostosowywanie pakietu zawartości usługi Azure AD Activity</span><span class="sxs-lookup"><span data-stu-id="2e49f-154">Customizing Azure AD Activity content pack</span></span>

<span data-ttu-id="2e49f-155">**Zmień wizualizację**: możesz zmienić wizualizację raportu, klikając opcję **Edytuj raport** i wybierając wizualizację.</span><span class="sxs-lookup"><span data-stu-id="2e49f-155">**Change Visualization**:  You can change a report visualization by clicking **Edit Report** and select the visualization you want.</span></span>
 
![Pakiet zawartości usługi Power BI dla usługi Azure Active Directory](./media/active-directory-reporting-power-bi-content-pack-how-to/09.png) 
 
![Pakiet zawartości usługi Power BI dla usługi Azure Active Directory](./media/active-directory-reporting-power-bi-content-pack-how-to/10.png) 

<span data-ttu-id="2e49f-158">**Dołącz dodatkowe pola**: w raporcie można dodawać pola i je usuwać. W tym celu wystarczy wybrać element wizualny, którego ma dotyczyć zmiana.</span><span class="sxs-lookup"><span data-stu-id="2e49f-158">**Include additional fields**:  You can add a field to the report or remove it by selecting the visual to which you want to add/remove the field.</span></span> <span data-ttu-id="2e49f-159">W poniższym przykładzie w widoku tabeli zostanie dodane pole „Sign-in Status” (Stan zalogowania).</span><span class="sxs-lookup"><span data-stu-id="2e49f-159">In the example below, I am adding “sign-in status” field to the table view.</span></span> 
 
![Pakiet zawartości usługi Power BI dla usługi Azure Active Directory](./media/active-directory-reporting-power-bi-content-pack-how-to/11.png) 

<span data-ttu-id="2e49f-161">**Przypnij wizualizacje do pulpitu nawigacyjnego**: można dostosować pulpit nawigacyjny, dołączając własne wizualizacje do raportu i przypinając je do pulpitu nawigacyjnego.</span><span class="sxs-lookup"><span data-stu-id="2e49f-161">**Pin visualizations to your dashboard**:  You can customize your dashboard and include your own visualizations to the report and pin it to the dashboard.</span></span> <span data-ttu-id="2e49f-162">W poniższym przykładzie nowy filtr o nazwie „Sign-in Status” został dodany i dołączony do raportu.</span><span class="sxs-lookup"><span data-stu-id="2e49f-162">In the example below, I added a new filter called “Sign-in Status” and included it in the report.</span></span> <span data-ttu-id="2e49f-163">Zmieniono również wizualizację z wykresu słupkowego na liniowy. Ten nowy element wizualny można przypiąć do pulpitu nawigacyjnego.</span><span class="sxs-lookup"><span data-stu-id="2e49f-163">I also changed the visualization from bar chart to a line chart and can pin this new visual to the dashboard.</span></span>

![Pakiet zawartości usługi Power BI dla usługi Azure Active Directory](./media/active-directory-reporting-power-bi-content-pack-how-to/12.png) 

![Pakiet zawartości usługi Power BI dla usługi Azure Active Directory](./media/active-directory-reporting-power-bi-content-pack-how-to/13.png) 
 

 


<span data-ttu-id="2e49f-166">**Udostępnianie pulpitu nawigacyjnego**: po utworzeniu własnej zawartości można udostępnić pulpit nawigacyjny użytkownikom w organizacji.</span><span class="sxs-lookup"><span data-stu-id="2e49f-166">**Sharing your dashboard**: Once you have created the content you want, you can share the dashboard with the users in your organization.</span></span> <span data-ttu-id="2e49f-167">Należy pamiętać, że po udostępnieniu raportu jego użytkownicy widzą pola, które zostały wybrane w raporcie.</span><span class="sxs-lookup"><span data-stu-id="2e49f-167">Please remember that once you share the report, they can see the fields you have selected in the report.</span></span>
 
![Pakiet zawartości usługi Power BI dla usługi Azure Active Directory](./media/active-directory-reporting-power-bi-content-pack-how-to/14.png) 



## <a name="scheduling-a-daily-refresh-of-your-power-bi-report"></a><span data-ttu-id="2e49f-169">Planowanie codziennego odświeżania raportu usługi Power BI</span><span class="sxs-lookup"><span data-stu-id="2e49f-169">Scheduling a daily refresh of your Power BI report</span></span>

<span data-ttu-id="2e49f-170">Aby zaplanować codzienne odświeżanie raportu usługi Power BI, przejdź do obszaru **Zestawy danych > Ustawienia > Zaplanuj odświeżanie** i ustaw go, jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="2e49f-170">To schedule a daily refresh of your Power BI report, go to **Datasets > Settings > Schedule Refresh** and set it as shown below.</span></span>
 
![Pakiet zawartości usługi Power BI dla usługi Azure Active Directory](./media/active-directory-reporting-power-bi-content-pack-how-to/15.png) 

## <a name="updating-to-newer-version-of-content-pack"></a><span data-ttu-id="2e49f-172">Aktualizacja do nowszej wersji pakietu zawartości</span><span class="sxs-lookup"><span data-stu-id="2e49f-172">Updating to newer version of content pack</span></span>

<span data-ttu-id="2e49f-173">Jeśli chcesz zaktualizować pakiet zawartości do nowszej wersji:</span><span class="sxs-lookup"><span data-stu-id="2e49f-173">If you want to update your content pack to get a newer version:</span></span>

- <span data-ttu-id="2e49f-174">Pobierz nowy pakiet zawartości i skonfiguruj go zgodnie z instrukcjami zawartymi w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="2e49f-174">Download the new content pack and set it up as per instructions listed in this article.</span></span>

- <span data-ttu-id="2e49f-175">Po skonfigurowaniu pakietu przejdź do obszaru **Źródło danych > Ustawienia > Poświadczenia dostępu do źródła danych** i ponownie wprowadź swoje poświadczenia, jak pokazano poniżej</span><span class="sxs-lookup"><span data-stu-id="2e49f-175">Once you have set it up, go to **Data Source > Settings > Data source credentials** and re-enter your credentials as shown below</span></span>

    ![Pakiet zawartości usługi Power BI dla usługi Azure Active Directory](./media/active-directory-reporting-power-bi-content-pack-how-to/16.png) 

<span data-ttu-id="2e49f-177">Po uruchomieniu nowej wersji pakietu zawartości można w razie potrzeby pozbyć się starej wersji, usuwając skojarzone z nim raporty i zestawy danych.</span><span class="sxs-lookup"><span data-stu-id="2e49f-177">As soon as the new version of the content pack is working, you can remove the old version if needed by deleting the underlying reports and datasets associated with that content pack.</span></span>

## <a name="still-having-issues"></a><span data-ttu-id="2e49f-178">Nadal masz problemy?</span><span class="sxs-lookup"><span data-stu-id="2e49f-178">Still having issues?</span></span> 

<span data-ttu-id="2e49f-179">Zapoznaj się z [przewodnikiem rozwiązywania problemów](active-directory-reporting-troubleshoot-content-pack.md).</span><span class="sxs-lookup"><span data-stu-id="2e49f-179">Check out our [troubleshooting guide](active-directory-reporting-troubleshoot-content-pack.md).</span></span> <span data-ttu-id="2e49f-180">Ogólną pomoc dotyczącą usługi Power BI można znaleźć w następujących [artykułach pomocy](https://powerbi.microsoft.com/en-us/documentation/powerbi-service-get-started/).</span><span class="sxs-lookup"><span data-stu-id="2e49f-180">For general help with Power BI, check out these [help articles](https://powerbi.microsoft.com/en-us/documentation/powerbi-service-get-started/).</span></span>
 

## <a name="next-steps"></a><span data-ttu-id="2e49f-181">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="2e49f-181">Next steps</span></span>

<span data-ttu-id="2e49f-182">Omówienie funkcji raportowania można znaleźć w temacie [Raporty w usłudze Azure Active Directory](active-directory-reporting-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="2e49f-182">For an overview of reporting, see the [Azure Active Directory reporting](active-directory-reporting-azure-portal.md).</span></span>
