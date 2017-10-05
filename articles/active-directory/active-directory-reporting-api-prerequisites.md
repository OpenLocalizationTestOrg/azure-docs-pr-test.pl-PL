---
title: "Wymagania wstępne dotyczące raportowania interfejsu API usługi Azure AD dostęp. | Microsoft Docs"
description: "Dowiedz się więcej o wymaganiach wstępnych można uzyskać dostępu do raportowania interfejsu API usługi Azure AD"
services: active-directory
documentationcenter: 
author: dhanyahk
manager: femila
editor: 
ms.assetid: ada19f69-665c-452a-8452-701029bf4252
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/16/2017
ms.author: dhanyahk;markvi
ms.openlocfilehash: 6e409fc56b77f37dac7f37382e664c577666ad4d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="prerequisites-to-access-the-azure-ad-reporting-api"></a><span data-ttu-id="5bee4-104">Wymagania wstępne dotyczące raportowania interfejsu API usługi Azure AD dostęp</span><span class="sxs-lookup"><span data-stu-id="5bee4-104">Prerequisites to access the Azure AD reporting API</span></span>
<span data-ttu-id="5bee4-105">[Raportowania interfejsów API usługi Azure AD](https://msdn.microsoft.com/library/azure/ad/graph/howto/azure-ad-reports-and-events-preview) umożliwiają programowy dostęp do danych za pomocą zestawu opartego na interfejsie REST API.</span><span class="sxs-lookup"><span data-stu-id="5bee4-105">The [Azure AD reporting APIs](https://msdn.microsoft.com/library/azure/ad/graph/howto/azure-ad-reports-and-events-preview) provide you with programmatic access to the data through a set of REST-based APIs.</span></span> <span data-ttu-id="5bee4-106">Te interfejsy API można wywoływać przy użyciu różnych języków i narzędzi do programowania.</span><span class="sxs-lookup"><span data-stu-id="5bee4-106">You can call these APIs from a variety of programming languages and tools.</span></span>

<span data-ttu-id="5bee4-107">Raportowania używa interfejsu API [OAuth](https://msdn.microsoft.com/library/azure/dn645545.aspx) do autoryzacji dostępu do interfejsów API sieci web.</span><span class="sxs-lookup"><span data-stu-id="5bee4-107">The reporting API uses [OAuth](https://msdn.microsoft.com/library/azure/dn645545.aspx) to authorize access to the web APIs.</span></span> 

<span data-ttu-id="5bee4-108">Aby przygotować dostęp do interfejsu API raportowania, należy:</span><span class="sxs-lookup"><span data-stu-id="5bee4-108">To prepare your access to the reporting API, you must:</span></span>

1. <span data-ttu-id="5bee4-109">Tworzenie aplikacji w dzierżawie usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="5bee4-109">Create an application in your Azure AD tenant</span></span> 
2. <span data-ttu-id="5bee4-110">Udziel aplikacji uprawnień dostępu do danych usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="5bee4-110">Grant the application appropriate permissions to access the Azure AD data</span></span>
3. <span data-ttu-id="5bee4-111">Zbierz ustawienia konfiguracji z katalogu</span><span class="sxs-lookup"><span data-stu-id="5bee4-111">Gather configuration settings from your directory</span></span>

<span data-ttu-id="5bee4-112">Pytania, problemy lub opinie, skontaktuj się z [Pomoc raportowania usługi AAD](mailto:aadreportinghelp@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="5bee4-112">For questions, issues or feedback, please contact [AAD Reporting Help](mailto:aadreportinghelp@microsoft.com).</span></span>

## <a name="create-an-azure-ad-application"></a><span data-ttu-id="5bee4-113">Tworzenie aplikacji usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="5bee4-113">Create an Azure AD application</span></span>
<span data-ttu-id="5bee4-114">Aby skonfigurować dostęp raportowania interfejsu API usługi Azure AD do katalogu, należy zalogować się do klasycznego portalu Azure przy użyciu konta administratora subskrypcji platformy Azure, który jest członkiem roli administratora globalnego katalogu w dzierżawie usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5bee4-114">To configure your directory to access the Azure AD reporting API, you must sign in to the Azure classic portal with an Azure subscription administrator account that is also a member of the Global Administrator directory role in your Azure AD tenant.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5bee4-115">Aplikacje uruchomione w ramach poświadczeń z uprawnieniami "Administrator", jak mogą być bardzo zaawansowane, więc Pamiętaj zapewnić bezpieczeństwo poświadczeń identyfikator/klucz tajny aplikacji.</span><span class="sxs-lookup"><span data-stu-id="5bee4-115">Applications running under credentials with "admin" privileges like this can be very powerful, so please be sure to keep the application's ID/secret credentials secure.</span></span>
> 
> 

1. <span data-ttu-id="5bee4-116">W [klasycznego portalu Azure](https://manage.windowsazure.com), w lewym okienku nawigacji, kliknij polecenie **usługi Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="5bee4-116">In the [Azure classic portal](https://manage.windowsazure.com), on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Zarejestrować aplikację](./media/active-directory-reporting-api-prerequisites/01.png) 
2. <span data-ttu-id="5bee4-118">Z **usługi active directory** listy, wybierz swój katalog.</span><span class="sxs-lookup"><span data-stu-id="5bee4-118">From the **active directory** list, select your directory.</span></span>
3. <span data-ttu-id="5bee4-119">W menu u góry kliknij **aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="5bee4-119">In the menu on the top, click **Applications**.</span></span>
   
    ![Zarejestrować aplikację](./media/active-directory-reporting-api-prerequisites/02.png) 
4. <span data-ttu-id="5bee4-121">Na dolnym pasku kliknij **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="5bee4-121">On the bottom bar, click **Add**.</span></span>
   
    ![Zarejestrować aplikację](./media/active-directory-reporting-api-prerequisites/03.png) 
5. <span data-ttu-id="5bee4-123">Na **co chcesz zrobić?** okna dialogowego, kliknij przycisk **Dodaj aplikację moją organizację**.</span><span class="sxs-lookup"><span data-stu-id="5bee4-123">On the **What do you want to do?** dialog, click **Add an application my organization is developing**.</span></span> 
   
    ![Zarejestrować aplikację](./media/active-directory-reporting-api-prerequisites/04.png) 
6. <span data-ttu-id="5bee4-125">Na **Powiedz nam o aplikacji** okna dialogowego, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="5bee4-125">On the **Tell us about your application** dialog, perform the following steps:</span></span> 
   
    ![Zarejestrować aplikację](./media/active-directory-reporting-api-prerequisites/05.png) 
   
    <span data-ttu-id="5bee4-127">a.</span><span class="sxs-lookup"><span data-stu-id="5bee4-127">a.</span></span> <span data-ttu-id="5bee4-128">W **nazwa** tekstowym, wpisz nazwę (np.: Aplikacja interfejsu API raportowania).</span><span class="sxs-lookup"><span data-stu-id="5bee4-128">In the **Name** textbox, type a name (e.g.: Reporting API Application).</span></span>
   
    <span data-ttu-id="5bee4-129">b.</span><span class="sxs-lookup"><span data-stu-id="5bee4-129">b.</span></span> <span data-ttu-id="5bee4-130">Wybierz **aplikacji sieci Web i/lub interfejs API sieci web**.</span><span class="sxs-lookup"><span data-stu-id="5bee4-130">Select **Web application and/or web API**.</span></span>
   
    <span data-ttu-id="5bee4-131">c.</span><span class="sxs-lookup"><span data-stu-id="5bee4-131">c.</span></span> <span data-ttu-id="5bee4-132">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="5bee4-132">Click **Next**.</span></span>
7. <span data-ttu-id="5bee4-133">Na **właściwości aplikacji** okna dialogowego, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="5bee4-133">On the **App properties** dialog, perform the following steps:</span></span> 
   
    ![Zarejestrować aplikację](./media/active-directory-reporting-api-prerequisites/06.png) 
   
    <span data-ttu-id="5bee4-135">a.</span><span class="sxs-lookup"><span data-stu-id="5bee4-135">a.</span></span> <span data-ttu-id="5bee4-136">W **adres URL logowania** pole tekstowe, typ `https://localhost`.</span><span class="sxs-lookup"><span data-stu-id="5bee4-136">In the **Sign-on URL** textbox, type `https://localhost`.</span></span>
   
    <span data-ttu-id="5bee4-137">b.</span><span class="sxs-lookup"><span data-stu-id="5bee4-137">b.</span></span> <span data-ttu-id="5bee4-138">W **identyfikator URI aplikacji** pole tekstowe, typ ```https://localhost/ReportingApiApp```.</span><span class="sxs-lookup"><span data-stu-id="5bee4-138">In the **App ID URI** textbox, type ```https://localhost/ReportingApiApp```.</span></span>
   
    <span data-ttu-id="5bee4-139">c.</span><span class="sxs-lookup"><span data-stu-id="5bee4-139">c.</span></span> <span data-ttu-id="5bee4-140">Kliknij przycisk **Complete** (Zakończ).</span><span class="sxs-lookup"><span data-stu-id="5bee4-140">Click **Complete**.</span></span>

## <a name="grant-your-application-permission-to-use-the-api"></a><span data-ttu-id="5bee4-141">Zezwolić aplikacji za pomocą interfejsu API</span><span class="sxs-lookup"><span data-stu-id="5bee4-141">Grant your application permission to use the API</span></span>
1. <span data-ttu-id="5bee4-142">W [klasycznego portalu Azure](https://manage.windowsazure.com/), w lewym okienku nawigacji, kliknij polecenie **usługi Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="5bee4-142">In the [Azure classic portal](https://manage.windowsazure.com/), on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Zarejestrować aplikację](./media/active-directory-reporting-api-prerequisites/01.png) 
2. <span data-ttu-id="5bee4-144">Z **usługi active directory** listy, wybierz swój katalog.</span><span class="sxs-lookup"><span data-stu-id="5bee4-144">From the **active directory** list, select your directory.</span></span>
3. <span data-ttu-id="5bee4-145">W menu u góry kliknij **aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="5bee4-145">In the menu on the top, click **Applications**.</span></span>
   
    ![Zarejestrować aplikację](./media/active-directory-reporting-api-prerequisites/02.png)
4. <span data-ttu-id="5bee4-147">Na liście aplikacji zaznacz nowo utworzonej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="5bee4-147">In the applications list, select your newly created application.</span></span>
   
    ![Zarejestrować aplikację](./media/active-directory-reporting-api-prerequisites/07.png)
5. <span data-ttu-id="5bee4-149">W menu u góry kliknij **Konfiguruj**.</span><span class="sxs-lookup"><span data-stu-id="5bee4-149">In the menu on the top, click **Configure**.</span></span>
   
    ![Zarejestrować aplikację](./media/active-directory-reporting-api-prerequisites/08.png)
6. <span data-ttu-id="5bee4-151">W **uprawnień dotyczących innych aplikacji** sekcji dla **usługi Azure Active Directory** zasobów, kliknij przycisk **uprawnienia aplikacji** listy rozwijanej, a następnie wybierz **Odczytuj dane katalogu**.</span><span class="sxs-lookup"><span data-stu-id="5bee4-151">In the **Permissions to other applications** section, for the **Azure Active Directory** resource, click the **Application Permissions** drop-down list, and then select **Read directory data**.</span></span>
   
    ![Zarejestrować aplikację](./media/active-directory-reporting-api-prerequisites/09.png)
7. <span data-ttu-id="5bee4-153">Na dolnym pasku kliknij **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="5bee4-153">On the bottom bar, click **Save**.</span></span>
   
    ![Zarejestrować aplikację](./media/active-directory-reporting-api-prerequisites/10.png)

## <a name="gather-configuration-settings-from-your-directory"></a><span data-ttu-id="5bee4-155">Zbierz ustawienia konfiguracji z katalogu</span><span class="sxs-lookup"><span data-stu-id="5bee4-155">Gather configuration settings from your directory</span></span>
<span data-ttu-id="5bee4-156">W tej sekcji przedstawiono sposób uzyskać następujące ustawienia z katalogiem:</span><span class="sxs-lookup"><span data-stu-id="5bee4-156">This section shows you how to get the following settings from your directory:</span></span>

* <span data-ttu-id="5bee4-157">Nazwa domeny</span><span class="sxs-lookup"><span data-stu-id="5bee4-157">Domain name</span></span>
* <span data-ttu-id="5bee4-158">Identyfikator klienta</span><span class="sxs-lookup"><span data-stu-id="5bee4-158">Client ID</span></span>
* <span data-ttu-id="5bee4-159">Klucz tajny klienta</span><span class="sxs-lookup"><span data-stu-id="5bee4-159">Client secret</span></span>

<span data-ttu-id="5bee4-160">Te wartości są wymagane podczas konfigurowania wywołania interfejsu API raportowania.</span><span class="sxs-lookup"><span data-stu-id="5bee4-160">You need these values when configuring calls to the reporting API.</span></span> 

### <a name="get-your-domain-name"></a><span data-ttu-id="5bee4-161">Pobierz nazwę domeny</span><span class="sxs-lookup"><span data-stu-id="5bee4-161">Get your domain name</span></span>
1. <span data-ttu-id="5bee4-162">W [klasycznego portalu Azure](https://manage.windowsazure.com), w lewym okienku nawigacji, kliknij polecenie **usługi Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="5bee4-162">In the [Azure classic portal](https://manage.windowsazure.com), on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Zarejestrować aplikację](./media/active-directory-reporting-api-prerequisites/01.png) 
2. <span data-ttu-id="5bee4-164">Z **usługi active directory** listy, wybierz swój katalog.</span><span class="sxs-lookup"><span data-stu-id="5bee4-164">From the **active directory** list, select your directory.</span></span>
3. <span data-ttu-id="5bee4-165">W menu u góry kliknij **domen**.</span><span class="sxs-lookup"><span data-stu-id="5bee4-165">In the menu on the top, click **Domains**.</span></span>
   
    ![Zarejestrować aplikację](./media/active-directory-reporting-api-prerequisites/11.png) 
4. <span data-ttu-id="5bee4-167">W **nazwy domeny** kolumny, skopiuj nazwę domeny.</span><span class="sxs-lookup"><span data-stu-id="5bee4-167">In the **Domain Name** column, copy your domain name.</span></span>
   
    ![Zarejestrować aplikację](./media/active-directory-reporting-api-prerequisites/12.png) 

### <a name="get-the-applications-client-id"></a><span data-ttu-id="5bee4-169">Pobieranie Identyfikatora klienta aplikacji</span><span class="sxs-lookup"><span data-stu-id="5bee4-169">Get the application's client ID</span></span>
1. <span data-ttu-id="5bee4-170">W [klasycznego portalu Azure](https://manage.windowsazure.com), w lewym okienku nawigacji, kliknij polecenie **usługi Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="5bee4-170">In the [Azure classic portal](https://manage.windowsazure.com), on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Zarejestrować aplikację](./media/active-directory-reporting-api-prerequisites/01.png) 
2. <span data-ttu-id="5bee4-172">Z **usługi active directory** listy, wybierz swój katalog.</span><span class="sxs-lookup"><span data-stu-id="5bee4-172">From the **active directory** list, select your directory.</span></span>
3. <span data-ttu-id="5bee4-173">W menu u góry kliknij **aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="5bee4-173">In the menu on the top, click **Applications**.</span></span>
   
    ![Zarejestrować aplikację](./media/active-directory-reporting-api-prerequisites/02.png) 
4. <span data-ttu-id="5bee4-175">Na liście aplikacji zaznacz nowo utworzonej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="5bee4-175">In the applications list, select your newly created application.</span></span>
   
    ![Zarejestrować aplikację](./media/active-directory-reporting-api-prerequisites/07.png)
5. <span data-ttu-id="5bee4-177">W menu u góry kliknij **Konfiguruj**.</span><span class="sxs-lookup"><span data-stu-id="5bee4-177">In the menu on the top, click **Configure**.</span></span>
   
    ![Zarejestrować aplikację](./media/active-directory-reporting-api-prerequisites/08.png)
6. <span data-ttu-id="5bee4-179">Kopiowanie z **identyfikator klienta**.</span><span class="sxs-lookup"><span data-stu-id="5bee4-179">Copy your **Client ID**.</span></span>
   
    ![Zarejestrować aplikację](./media/active-directory-reporting-api-prerequisites/13.png)

### <a name="get-the-applications-client-secret"></a><span data-ttu-id="5bee4-181">Pobierz klucz tajny klienta aplikacji</span><span class="sxs-lookup"><span data-stu-id="5bee4-181">Get the application's client secret</span></span>
<span data-ttu-id="5bee4-182">Aby uzyskać klucz tajny klienta aplikacji, musisz utworzyć nowy klucz i zapisać jego wartości podczas zapisywania nowego klucza, ponieważ nie jest możliwe później już pobierania tej wartości.</span><span class="sxs-lookup"><span data-stu-id="5bee4-182">To get your application's client secret, you need to create a new key and save its value upon saving the new key because it is not possible to retrieve this value later anymore.</span></span>

1. <span data-ttu-id="5bee4-183">W [klasycznego portalu Azure](https://manage.windowsazure.com), w lewym okienku nawigacji, kliknij polecenie **usługi Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="5bee4-183">In the [Azure classic portal](https://manage.windowsazure.com), on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Zarejestrować aplikację](./media/active-directory-reporting-api-prerequisites/01.png) 
2. <span data-ttu-id="5bee4-185">Z **usługi active directory** listy, wybierz swój katalog.</span><span class="sxs-lookup"><span data-stu-id="5bee4-185">From the **active directory** list, select your directory.</span></span>
3. <span data-ttu-id="5bee4-186">W menu u góry kliknij **aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="5bee4-186">In the menu on the top, click **Applications**.</span></span>
   
    ![Zarejestrować aplikację](./media/active-directory-reporting-api-prerequisites/02.png) 
4. <span data-ttu-id="5bee4-188">Na liście aplikacji zaznacz nowo utworzonej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="5bee4-188">In the applications list, select your newly created application.</span></span>
   
    ![Zarejestrować aplikację](./media/active-directory-reporting-api-prerequisites/07.png)
5. <span data-ttu-id="5bee4-190">W menu u góry kliknij **Konfiguruj**.</span><span class="sxs-lookup"><span data-stu-id="5bee4-190">In the menu on the top, click **Configure**.</span></span>
   
    ![Zarejestrować aplikację](./media/active-directory-reporting-api-prerequisites/08.png)
6. <span data-ttu-id="5bee4-192">W **klucze** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="5bee4-192">In the **Keys** section, perform the following steps:</span></span> 
   
    ![Zarejestrować aplikację](./media/active-directory-reporting-api-prerequisites/14.png)
   
    <span data-ttu-id="5bee4-194">a.</span><span class="sxs-lookup"><span data-stu-id="5bee4-194">a.</span></span> <span data-ttu-id="5bee4-195">Na liście czas trwania wybierz czas trwania</span><span class="sxs-lookup"><span data-stu-id="5bee4-195">From the duration list, select a duration</span></span>
   
    <span data-ttu-id="5bee4-196">b.</span><span class="sxs-lookup"><span data-stu-id="5bee4-196">b.</span></span> <span data-ttu-id="5bee4-197">Na dolnym pasku kliknij **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="5bee4-197">On the bottom bar, click **Save**.</span></span>
   
    ![Zarejestrować aplikację](./media/active-directory-reporting-api-prerequisites/10.png)
   
    <span data-ttu-id="5bee4-199">c.</span><span class="sxs-lookup"><span data-stu-id="5bee4-199">c.</span></span> <span data-ttu-id="5bee4-200">Skopiuj wartość klucza.</span><span class="sxs-lookup"><span data-stu-id="5bee4-200">Copy the key value.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5bee4-201">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="5bee4-201">Next Steps</span></span>
* <span data-ttu-id="5bee4-202">Czy chcesz uzyskać dostęp do danych raportowania interfejsu API w sposób programowy usługi Azure AD?</span><span class="sxs-lookup"><span data-stu-id="5bee4-202">Would you like to access the data from the Azure AD reporting API in a programmatic manner?</span></span> <span data-ttu-id="5bee4-203">Zapoznaj się z [wprowadzenie do usługi Azure Active Directory interfejsu API raportowania](active-directory-reporting-api-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="5bee4-203">Check out [Getting started with the Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md).</span></span>
* <span data-ttu-id="5bee4-204">Jeśli chcesz dowiedzieć się więcej o usłudze Azure Active Directory, zobacz [Azure Active Directory Przewodnik po raportach](active-directory-reporting-guide.md).</span><span class="sxs-lookup"><span data-stu-id="5bee4-204">If you would like to find out more about Azure Active Directory reporting, see the [Azure Active Directory Reporting Guide](active-directory-reporting-guide.md).</span></span>  

