---
title: aaaPrerequisites tooaccess hello Azure AD raportowania interfejsu API. | Microsoft Docs
description: "Dowiedz się więcej o API raportowania hello wymagania wstępne tooaccess hello Azure AD"
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
ms.openlocfilehash: e9d7ceaedb07d18fbd75b70d68b5cfbebc756c36
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="prerequisites-tooaccess-hello-azure-ad-reporting-api"></a><span data-ttu-id="7f2ec-104">Wymagania wstępne tooaccess hello Azure AD raportowania interfejsu API</span><span class="sxs-lookup"><span data-stu-id="7f2ec-104">Prerequisites tooaccess hello Azure AD reporting API</span></span>
<span data-ttu-id="7f2ec-105">Witaj [raportowania interfejsów API usługi Azure AD](https://msdn.microsoft.com/library/azure/ad/graph/howto/azure-ad-reports-and-events-preview) umożliwiają dostęp programistyczny toohello danych za pomocą zestawu opartego na interfejsie REST API.</span><span class="sxs-lookup"><span data-stu-id="7f2ec-105">hello [Azure AD reporting APIs](https://msdn.microsoft.com/library/azure/ad/graph/howto/azure-ad-reports-and-events-preview) provide you with programmatic access toohello data through a set of REST-based APIs.</span></span> <span data-ttu-id="7f2ec-106">Te interfejsy API można wywoływać przy użyciu różnych języków i narzędzi do programowania.</span><span class="sxs-lookup"><span data-stu-id="7f2ec-106">You can call these APIs from a variety of programming languages and tools.</span></span>

<span data-ttu-id="7f2ec-107">Witaj reporting używa interfejsu API [OAuth](https://msdn.microsoft.com/library/azure/dn645545.aspx) tooauthorize dostępu toohello interfejsów API sieci web.</span><span class="sxs-lookup"><span data-stu-id="7f2ec-107">hello reporting API uses [OAuth](https://msdn.microsoft.com/library/azure/dn645545.aspx) tooauthorize access toohello web APIs.</span></span> 

<span data-ttu-id="7f2ec-108">tooprepare z interfejsem API raportowania toohello dostępu, musi:</span><span class="sxs-lookup"><span data-stu-id="7f2ec-108">tooprepare your access toohello reporting API, you must:</span></span>

1. <span data-ttu-id="7f2ec-109">Tworzenie aplikacji w dzierżawie usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="7f2ec-109">Create an application in your Azure AD tenant</span></span> 
2. <span data-ttu-id="7f2ec-110">Tooaccess odpowiednie uprawnienia aplikacji hello GRANT hello danych usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="7f2ec-110">Grant hello application appropriate permissions tooaccess hello Azure AD data</span></span>
3. <span data-ttu-id="7f2ec-111">Zbierz ustawienia konfiguracji z katalogu</span><span class="sxs-lookup"><span data-stu-id="7f2ec-111">Gather configuration settings from your directory</span></span>

<span data-ttu-id="7f2ec-112">Pytania, problemy lub opinie, skontaktuj się z [Pomoc raportowania usługi AAD](mailto:aadreportinghelp@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="7f2ec-112">For questions, issues or feedback, please contact [AAD Reporting Help](mailto:aadreportinghelp@microsoft.com).</span></span>

## <a name="create-an-azure-ad-application"></a><span data-ttu-id="7f2ec-113">Tworzenie aplikacji usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="7f2ec-113">Create an Azure AD application</span></span>
<span data-ttu-id="7f2ec-114">tooconfigure katalogu tooaccess hello Azure AD raportowania interfejsu API, musisz zalogować się toohello klasycznego portalu Azure przy użyciu konta administratora subskrypcji platformy Azure, który jest członkiem roli hello administratora globalnego katalogu, w dzierżawie usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7f2ec-114">tooconfigure your directory tooaccess hello Azure AD reporting API, you must sign in toohello Azure classic portal with an Azure subscription administrator account that is also a member of hello Global Administrator directory role in your Azure AD tenant.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7f2ec-115">Aplikacje uruchomione w ramach poświadczeń z uprawnieniami "Administrator", jak mogą być bardzo zaawansowane, więc należy być bezpieczne czy tookeep hello identyfikator/klucz tajny poświadczenia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="7f2ec-115">Applications running under credentials with "admin" privileges like this can be very powerful, so please be sure tookeep hello application's ID/secret credentials secure.</span></span>
> 
> 

1. <span data-ttu-id="7f2ec-116">W hello [klasycznego portalu Azure](https://manage.windowsazure.com)na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7f2ec-116">In hello [Azure classic portal](https://manage.windowsazure.com), on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![Zarejestrować aplikację](./media/active-directory-reporting-api-prerequisites/01.png) 
2. <span data-ttu-id="7f2ec-118">Z hello **usługi active directory** listy, wybierz swój katalog.</span><span class="sxs-lookup"><span data-stu-id="7f2ec-118">From hello **active directory** list, select your directory.</span></span>
3. <span data-ttu-id="7f2ec-119">W menu hello na górze hello, kliknij przycisk **aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="7f2ec-119">In hello menu on hello top, click **Applications**.</span></span>
   
    ![Zarejestrować aplikację](./media/active-directory-reporting-api-prerequisites/02.png) 
4. <span data-ttu-id="7f2ec-121">Na pasku dolnej powitania kliknij **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="7f2ec-121">On hello bottom bar, click **Add**.</span></span>
   
    ![Zarejestrować aplikację](./media/active-directory-reporting-api-prerequisites/03.png) 
5. <span data-ttu-id="7f2ec-123">Na powitania **co chcesz toodo?** okna dialogowego, kliknij przycisk **Dodaj aplikację moją organizację**.</span><span class="sxs-lookup"><span data-stu-id="7f2ec-123">On hello **What do you want toodo?** dialog, click **Add an application my organization is developing**.</span></span> 
   
    ![Zarejestrować aplikację](./media/active-directory-reporting-api-prerequisites/04.png) 
6. <span data-ttu-id="7f2ec-125">Na powitania **Powiedz nam o aplikacji** okna dialogowego, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="7f2ec-125">On hello **Tell us about your application** dialog, perform hello following steps:</span></span> 
   
    ![Zarejestrować aplikację](./media/active-directory-reporting-api-prerequisites/05.png) 
   
    <span data-ttu-id="7f2ec-127">a.</span><span class="sxs-lookup"><span data-stu-id="7f2ec-127">a.</span></span> <span data-ttu-id="7f2ec-128">W hello **nazwa** tekstowym, wpisz nazwę (np.: Aplikacja interfejsu API raportowania).</span><span class="sxs-lookup"><span data-stu-id="7f2ec-128">In hello **Name** textbox, type a name (e.g.: Reporting API Application).</span></span>
   
    <span data-ttu-id="7f2ec-129">b.</span><span class="sxs-lookup"><span data-stu-id="7f2ec-129">b.</span></span> <span data-ttu-id="7f2ec-130">Wybierz **aplikacji sieci Web i/lub interfejs API sieci web**.</span><span class="sxs-lookup"><span data-stu-id="7f2ec-130">Select **Web application and/or web API**.</span></span>
   
    <span data-ttu-id="7f2ec-131">c.</span><span class="sxs-lookup"><span data-stu-id="7f2ec-131">c.</span></span> <span data-ttu-id="7f2ec-132">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="7f2ec-132">Click **Next**.</span></span>
7. <span data-ttu-id="7f2ec-133">Na powitania **właściwości aplikacji** okna dialogowego, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="7f2ec-133">On hello **App properties** dialog, perform hello following steps:</span></span> 
   
    ![Zarejestrować aplikację](./media/active-directory-reporting-api-prerequisites/06.png) 
   
    <span data-ttu-id="7f2ec-135">a.</span><span class="sxs-lookup"><span data-stu-id="7f2ec-135">a.</span></span> <span data-ttu-id="7f2ec-136">W hello **adres URL logowania** pole tekstowe, typ `https://localhost`.</span><span class="sxs-lookup"><span data-stu-id="7f2ec-136">In hello **Sign-on URL** textbox, type `https://localhost`.</span></span>
   
    <span data-ttu-id="7f2ec-137">b.</span><span class="sxs-lookup"><span data-stu-id="7f2ec-137">b.</span></span> <span data-ttu-id="7f2ec-138">W hello **identyfikator URI aplikacji** pole tekstowe, typ ```https://localhost/ReportingApiApp```.</span><span class="sxs-lookup"><span data-stu-id="7f2ec-138">In hello **App ID URI** textbox, type ```https://localhost/ReportingApiApp```.</span></span>
   
    <span data-ttu-id="7f2ec-139">c.</span><span class="sxs-lookup"><span data-stu-id="7f2ec-139">c.</span></span> <span data-ttu-id="7f2ec-140">Kliknij przycisk **Complete** (Zakończ).</span><span class="sxs-lookup"><span data-stu-id="7f2ec-140">Click **Complete**.</span></span>

## <a name="grant-your-application-permission-toouse-hello-api"></a><span data-ttu-id="7f2ec-141">Przyznaj hello toouse uprawnień z aplikacji interfejsu API</span><span class="sxs-lookup"><span data-stu-id="7f2ec-141">Grant your application permission toouse hello API</span></span>
1. <span data-ttu-id="7f2ec-142">W hello [klasycznego portalu Azure](https://manage.windowsazure.com/)na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7f2ec-142">In hello [Azure classic portal](https://manage.windowsazure.com/), on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![Zarejestrować aplikację](./media/active-directory-reporting-api-prerequisites/01.png) 
2. <span data-ttu-id="7f2ec-144">Z hello **usługi active directory** listy, wybierz swój katalog.</span><span class="sxs-lookup"><span data-stu-id="7f2ec-144">From hello **active directory** list, select your directory.</span></span>
3. <span data-ttu-id="7f2ec-145">W menu hello na górze hello, kliknij przycisk **aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="7f2ec-145">In hello menu on hello top, click **Applications**.</span></span>
   
    ![Zarejestrować aplikację](./media/active-directory-reporting-api-prerequisites/02.png)
4. <span data-ttu-id="7f2ec-147">Z listy aplikacji hello wybierz nowo utworzonej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="7f2ec-147">In hello applications list, select your newly created application.</span></span>
   
    ![Zarejestrować aplikację](./media/active-directory-reporting-api-prerequisites/07.png)
5. <span data-ttu-id="7f2ec-149">W menu hello na górze hello, kliknij przycisk **Konfiguruj**.</span><span class="sxs-lookup"><span data-stu-id="7f2ec-149">In hello menu on hello top, click **Configure**.</span></span>
   
    ![Zarejestrować aplikację](./media/active-directory-reporting-api-prerequisites/08.png)
6. <span data-ttu-id="7f2ec-151">W hello **uprawnienia aplikacji tooother** sekcji, aby hello **usługi Azure Active Directory** zasobów, kliknij hello **uprawnienia aplikacji** listy rozwijanej, a następnie Wybierz **odczytuj dane katalogu**.</span><span class="sxs-lookup"><span data-stu-id="7f2ec-151">In hello **Permissions tooother applications** section, for hello **Azure Active Directory** resource, click hello **Application Permissions** drop-down list, and then select **Read directory data**.</span></span>
   
    ![Zarejestrować aplikację](./media/active-directory-reporting-api-prerequisites/09.png)
7. <span data-ttu-id="7f2ec-153">Na pasku dolnej powitania kliknij **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="7f2ec-153">On hello bottom bar, click **Save**.</span></span>
   
    ![Zarejestrować aplikację](./media/active-directory-reporting-api-prerequisites/10.png)

## <a name="gather-configuration-settings-from-your-directory"></a><span data-ttu-id="7f2ec-155">Zbierz ustawienia konfiguracji z katalogu</span><span class="sxs-lookup"><span data-stu-id="7f2ec-155">Gather configuration settings from your directory</span></span>
<span data-ttu-id="7f2ec-156">W tej sekcji opisano sposób hello tooget następujące ustawienia z katalogu:</span><span class="sxs-lookup"><span data-stu-id="7f2ec-156">This section shows you how tooget hello following settings from your directory:</span></span>

* <span data-ttu-id="7f2ec-157">Nazwa domeny</span><span class="sxs-lookup"><span data-stu-id="7f2ec-157">Domain name</span></span>
* <span data-ttu-id="7f2ec-158">Identyfikator klienta</span><span class="sxs-lookup"><span data-stu-id="7f2ec-158">Client ID</span></span>
* <span data-ttu-id="7f2ec-159">Klucz tajny klienta</span><span class="sxs-lookup"><span data-stu-id="7f2ec-159">Client secret</span></span>

<span data-ttu-id="7f2ec-160">Należy korzystać z tych wartości podczas konfigurowania raportowania interfejsu API toohello wywołania.</span><span class="sxs-lookup"><span data-stu-id="7f2ec-160">You need these values when configuring calls toohello reporting API.</span></span> 

### <a name="get-your-domain-name"></a><span data-ttu-id="7f2ec-161">Pobierz nazwę domeny</span><span class="sxs-lookup"><span data-stu-id="7f2ec-161">Get your domain name</span></span>
1. <span data-ttu-id="7f2ec-162">W hello [klasycznego portalu Azure](https://manage.windowsazure.com)na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7f2ec-162">In hello [Azure classic portal](https://manage.windowsazure.com), on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![Zarejestrować aplikację](./media/active-directory-reporting-api-prerequisites/01.png) 
2. <span data-ttu-id="7f2ec-164">Z hello **usługi active directory** listy, wybierz swój katalog.</span><span class="sxs-lookup"><span data-stu-id="7f2ec-164">From hello **active directory** list, select your directory.</span></span>
3. <span data-ttu-id="7f2ec-165">W menu hello na górze hello, kliknij przycisk **domen**.</span><span class="sxs-lookup"><span data-stu-id="7f2ec-165">In hello menu on hello top, click **Domains**.</span></span>
   
    ![Zarejestrować aplikację](./media/active-directory-reporting-api-prerequisites/11.png) 
4. <span data-ttu-id="7f2ec-167">W hello **nazwy domeny** kolumny, skopiuj nazwę domeny.</span><span class="sxs-lookup"><span data-stu-id="7f2ec-167">In hello **Domain Name** column, copy your domain name.</span></span>
   
    ![Zarejestrować aplikację](./media/active-directory-reporting-api-prerequisites/12.png) 

### <a name="get-hello-applications-client-id"></a><span data-ttu-id="7f2ec-169">Pobieranie Identyfikatora klienta aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="7f2ec-169">Get hello application's client ID</span></span>
1. <span data-ttu-id="7f2ec-170">W hello [klasycznego portalu Azure](https://manage.windowsazure.com)na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7f2ec-170">In hello [Azure classic portal](https://manage.windowsazure.com), on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![Zarejestrować aplikację](./media/active-directory-reporting-api-prerequisites/01.png) 
2. <span data-ttu-id="7f2ec-172">Z hello **usługi active directory** listy, wybierz swój katalog.</span><span class="sxs-lookup"><span data-stu-id="7f2ec-172">From hello **active directory** list, select your directory.</span></span>
3. <span data-ttu-id="7f2ec-173">W menu hello na górze hello, kliknij przycisk **aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="7f2ec-173">In hello menu on hello top, click **Applications**.</span></span>
   
    ![Zarejestrować aplikację](./media/active-directory-reporting-api-prerequisites/02.png) 
4. <span data-ttu-id="7f2ec-175">Z listy aplikacji hello wybierz nowo utworzonej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="7f2ec-175">In hello applications list, select your newly created application.</span></span>
   
    ![Zarejestrować aplikację](./media/active-directory-reporting-api-prerequisites/07.png)
5. <span data-ttu-id="7f2ec-177">W menu hello na górze hello, kliknij przycisk **Konfiguruj**.</span><span class="sxs-lookup"><span data-stu-id="7f2ec-177">In hello menu on hello top, click **Configure**.</span></span>
   
    ![Zarejestrować aplikację](./media/active-directory-reporting-api-prerequisites/08.png)
6. <span data-ttu-id="7f2ec-179">Kopiowanie z **identyfikator klienta**.</span><span class="sxs-lookup"><span data-stu-id="7f2ec-179">Copy your **Client ID**.</span></span>
   
    ![Zarejestrować aplikację](./media/active-directory-reporting-api-prerequisites/13.png)

### <a name="get-hello-applications-client-secret"></a><span data-ttu-id="7f2ec-181">Pobierz klucz tajny klienta aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="7f2ec-181">Get hello application's client secret</span></span>
<span data-ttu-id="7f2ec-182">tooget klienta aplikacji tajne, należy toocreate nowy klucz i zapisz jego wartości podczas zapisywania nowego klucza hello, ponieważ nie jest możliwe tooretrieve później już tej wartości.</span><span class="sxs-lookup"><span data-stu-id="7f2ec-182">tooget your application's client secret, you need toocreate a new key and save its value upon saving hello new key because it is not possible tooretrieve this value later anymore.</span></span>

1. <span data-ttu-id="7f2ec-183">W hello [klasycznego portalu Azure](https://manage.windowsazure.com)na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7f2ec-183">In hello [Azure classic portal](https://manage.windowsazure.com), on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![Zarejestrować aplikację](./media/active-directory-reporting-api-prerequisites/01.png) 
2. <span data-ttu-id="7f2ec-185">Z hello **usługi active directory** listy, wybierz swój katalog.</span><span class="sxs-lookup"><span data-stu-id="7f2ec-185">From hello **active directory** list, select your directory.</span></span>
3. <span data-ttu-id="7f2ec-186">W menu hello na górze hello, kliknij przycisk **aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="7f2ec-186">In hello menu on hello top, click **Applications**.</span></span>
   
    ![Zarejestrować aplikację](./media/active-directory-reporting-api-prerequisites/02.png) 
4. <span data-ttu-id="7f2ec-188">Z listy aplikacji hello wybierz nowo utworzonej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="7f2ec-188">In hello applications list, select your newly created application.</span></span>
   
    ![Zarejestrować aplikację](./media/active-directory-reporting-api-prerequisites/07.png)
5. <span data-ttu-id="7f2ec-190">W menu hello na górze hello, kliknij przycisk **Konfiguruj**.</span><span class="sxs-lookup"><span data-stu-id="7f2ec-190">In hello menu on hello top, click **Configure**.</span></span>
   
    ![Zarejestrować aplikację](./media/active-directory-reporting-api-prerequisites/08.png)
6. <span data-ttu-id="7f2ec-192">W hello **klucze** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="7f2ec-192">In hello **Keys** section, perform hello following steps:</span></span> 
   
    ![Zarejestrować aplikację](./media/active-directory-reporting-api-prerequisites/14.png)
   
    <span data-ttu-id="7f2ec-194">a.</span><span class="sxs-lookup"><span data-stu-id="7f2ec-194">a.</span></span> <span data-ttu-id="7f2ec-195">Z listy czas trwania hello wybierz czas trwania</span><span class="sxs-lookup"><span data-stu-id="7f2ec-195">From hello duration list, select a duration</span></span>
   
    <span data-ttu-id="7f2ec-196">b.</span><span class="sxs-lookup"><span data-stu-id="7f2ec-196">b.</span></span> <span data-ttu-id="7f2ec-197">Na pasku dolnej powitania kliknij **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="7f2ec-197">On hello bottom bar, click **Save**.</span></span>
   
    ![Zarejestrować aplikację](./media/active-directory-reporting-api-prerequisites/10.png)
   
    <span data-ttu-id="7f2ec-199">c.</span><span class="sxs-lookup"><span data-stu-id="7f2ec-199">c.</span></span> <span data-ttu-id="7f2ec-200">Skopiuj wartość klucza hello.</span><span class="sxs-lookup"><span data-stu-id="7f2ec-200">Copy hello key value.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7f2ec-201">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="7f2ec-201">Next Steps</span></span>
* <span data-ttu-id="7f2ec-202">Czy można tak, jak dane z usługi Azure AD hello hello tooaccess raportowania interfejsu API w sposób programowy</span><span class="sxs-lookup"><span data-stu-id="7f2ec-202">Would you like tooaccess hello data from hello Azure AD reporting API in a programmatic manner?</span></span> <span data-ttu-id="7f2ec-203">Zapoznaj się z [wprowadzenie hello Azure Active Directory interfejsu API raportowania](active-directory-reporting-api-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="7f2ec-203">Check out [Getting started with hello Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md).</span></span>
* <span data-ttu-id="7f2ec-204">Jeśli chcesz toofind się więcej o usłudze Azure Active Directory, zobacz hello [Azure Active Directory Przewodnik po raportach](active-directory-reporting-guide.md).</span><span class="sxs-lookup"><span data-stu-id="7f2ec-204">If you would like toofind out more about Azure Active Directory reporting, see hello [Azure Active Directory Reporting Guide](active-directory-reporting-guide.md).</span></span>  

