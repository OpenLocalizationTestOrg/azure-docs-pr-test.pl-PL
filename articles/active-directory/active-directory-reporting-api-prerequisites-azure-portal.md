---
title: "interfejsu API raportowania usługi Azure AD hello tooaccess aaaPrerequisites | Dokumentacja firmy Microsoft"
description: "Dowiedz się więcej o API raportowania hello wymagania wstępne tooaccess hello Azure AD"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: ada19f69-665c-452a-8452-701029bf4252
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/15/2017
ms.author: dhanyahk;markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: ec28a7530f341dda31268a978754b615c727d66f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="prerequisites-tooaccess-hello-azure-ad-reporting-api"></a><span data-ttu-id="e3a62-103">Wymagania wstępne tooaccess hello Azure AD raportowania interfejsu API</span><span class="sxs-lookup"><span data-stu-id="e3a62-103">Prerequisites tooaccess hello Azure AD reporting API</span></span>

<span data-ttu-id="e3a62-104">Witaj [raportowania interfejsów API usługi Azure AD](https://msdn.microsoft.com/library/azure/ad/graph/howto/azure-ad-reports-and-events-preview) umożliwiają dostęp programistyczny toohello danych za pomocą zestawu opartego na interfejsie REST API.</span><span class="sxs-lookup"><span data-stu-id="e3a62-104">hello [Azure AD reporting APIs](https://msdn.microsoft.com/library/azure/ad/graph/howto/azure-ad-reports-and-events-preview) provide you with programmatic access toohello data through a set of REST-based APIs.</span></span> <span data-ttu-id="e3a62-105">Te interfejsy API można wywoływać przy użyciu różnych języków i narzędzi do programowania.</span><span class="sxs-lookup"><span data-stu-id="e3a62-105">You can call these APIs from a variety of programming languages and tools.</span></span>

<span data-ttu-id="e3a62-106">Witaj reporting używa interfejsu API [OAuth](https://msdn.microsoft.com/library/azure/dn645545.aspx) tooauthorize dostępu toohello interfejsów API sieci web.</span><span class="sxs-lookup"><span data-stu-id="e3a62-106">hello reporting API uses [OAuth](https://msdn.microsoft.com/library/azure/dn645545.aspx) tooauthorize access toohello web APIs.</span></span> 

<span data-ttu-id="e3a62-107">tooget uzyskiwać dostęp do interfejsu API hello toohello danych raportowania, należy toohave jedną powitania po przypisanych ról:</span><span class="sxs-lookup"><span data-stu-id="e3a62-107">tooget access toohello reporting data through hello API, you need toohave one of hello following roles assigned:</span></span>

- <span data-ttu-id="e3a62-108">Czytnik zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="e3a62-108">Security Reader</span></span>
- <span data-ttu-id="e3a62-109">Administrator zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="e3a62-109">Security Admin</span></span>
- <span data-ttu-id="e3a62-110">Administrator globalny</span><span class="sxs-lookup"><span data-stu-id="e3a62-110">Global Admin</span></span>


<span data-ttu-id="e3a62-111">tooprepare z interfejsem API raportowania toohello dostępu, musi:</span><span class="sxs-lookup"><span data-stu-id="e3a62-111">tooprepare your access toohello reporting API, you must:</span></span>

1. <span data-ttu-id="e3a62-112">Rejestrowanie aplikacji</span><span class="sxs-lookup"><span data-stu-id="e3a62-112">Register an application</span></span> 
2. <span data-ttu-id="e3a62-113">Udzielanie uprawnień</span><span class="sxs-lookup"><span data-stu-id="e3a62-113">Grant permissions</span></span> 
3. <span data-ttu-id="e3a62-114">Zbierz ustawienia konfiguracji</span><span class="sxs-lookup"><span data-stu-id="e3a62-114">Gather configuration settings</span></span> 

<span data-ttu-id="e3a62-115">Pytania, problemy lub opinie, użyj funkcji [pliku biletu pomocy technicznej](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-troubleshooting-support-howto).</span><span class="sxs-lookup"><span data-stu-id="e3a62-115">For questions, issues or feedback, please [file a support ticket](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-troubleshooting-support-howto).</span></span>

## <a name="register-an-azure-active-directory-application"></a><span data-ttu-id="e3a62-116">Rejestrowanie aplikacji usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e3a62-116">Register an Azure Active Directory application</span></span>

<span data-ttu-id="e3a62-117">Należy tooregister aplikacji, nawet jeśli uzyskują dostęp do hello raportowania interfejsu API za pomocą skryptu.</span><span class="sxs-lookup"><span data-stu-id="e3a62-117">You need tooregister an app even if you are accessing hello reporting API using a script.</span></span> <span data-ttu-id="e3a62-118">Zapewnia to **identyfikator aplikacji**, który jest wymagany przez wywołanie autoryzacji i umożliwia tokenów tooreceive kodu.</span><span class="sxs-lookup"><span data-stu-id="e3a62-118">This gives you an **Application ID**, which is required for an authorization call and it enables your code tooreceive tokens.</span></span>

<span data-ttu-id="e3a62-119">tooconfigure katalogu tooaccess hello Azure AD raportowania interfejsu API, musisz zalogować się toohello portalu Azure przy użyciu konta administratora platformy Azure, który jest również członkiem hello **administratora globalnego** roli katalogu w dzierżawie usługi Azure AD .</span><span class="sxs-lookup"><span data-stu-id="e3a62-119">tooconfigure your directory tooaccess hello Azure AD reporting API, you must sign in toohello Azure portal with an Azure administrator account that is also a member of hello **Global Administrator** directory role in your Azure AD tenant.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e3a62-120">Aplikacje uruchomione w ramach poświadczeń z uprawnieniami "Administrator", jak mogą być bardzo zaawansowane, więc należy być bezpieczne czy tookeep hello identyfikator/klucz tajny poświadczenia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e3a62-120">Applications running under credentials with "admin" privileges like this can be very powerful, so please be sure tookeep hello application's ID/secret credentials secure.</span></span>
> 


<span data-ttu-id="e3a62-121">**tooregister aplikację usługi Azure Active Directory:**</span><span class="sxs-lookup"><span data-stu-id="e3a62-121">**tooregister an Azure Active Directory application:**</span></span>

1. <span data-ttu-id="e3a62-122">W hello [portalu Azure](https://portal.azure.com)na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e3a62-122">In hello [Azure portal](https://portal.azure.com), on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![Zarejestrować aplikację](./media/active-directory-reporting-api-prerequisites-azure-portal/01.png) 

2. <span data-ttu-id="e3a62-124">Na powitania **usługi Azure Active Directory** bloku, kliknij przycisk **rejestracji aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="e3a62-124">On hello **Azure Active Directory** blade, click **App registrations**.</span></span>

    ![Zarejestrować aplikację](./media/active-directory-reporting-api-prerequisites-azure-portal/02.png) 

3. <span data-ttu-id="e3a62-126">Na powitania **rejestracji aplikacji** bloku na powitania narzędzi u góry hello kliknij **nowej rejestracji aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="e3a62-126">On hello **App registrations** blade, in hello toolbar on hello top, click **New application registration**.</span></span>

    ![Zarejestrować aplikację](./media/active-directory-reporting-api-prerequisites-azure-portal/03.png)

4. <span data-ttu-id="e3a62-128">Na powitania **Utwórz** blok, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="e3a62-128">On hello **Create** blade, perform hello following steps:</span></span>

    ![Zarejestrować aplikację](./media/active-directory-reporting-api-prerequisites-azure-portal/04.png)

    <span data-ttu-id="e3a62-130">a.</span><span class="sxs-lookup"><span data-stu-id="e3a62-130">a.</span></span> <span data-ttu-id="e3a62-131">W hello **nazwa** pole tekstowe, typ `Reporting API application`.</span><span class="sxs-lookup"><span data-stu-id="e3a62-131">In hello **Name** textbox, type `Reporting API application`.</span></span>

    <span data-ttu-id="e3a62-132">b.</span><span class="sxs-lookup"><span data-stu-id="e3a62-132">b.</span></span> <span data-ttu-id="e3a62-133">Jako **typu aplikacji**, wybierz pozycję **aplikacji sieci Web / interfejs API**.</span><span class="sxs-lookup"><span data-stu-id="e3a62-133">As **Application type**, select **Web app / API**.</span></span>

    <span data-ttu-id="e3a62-134">c.</span><span class="sxs-lookup"><span data-stu-id="e3a62-134">c.</span></span> <span data-ttu-id="e3a62-135">W hello **adres URL logowania** pole tekstowe, typ `https://localhost`.</span><span class="sxs-lookup"><span data-stu-id="e3a62-135">In hello **Sign-on URL** textbox, type `https://localhost`.</span></span>

    <span data-ttu-id="e3a62-136">d.</span><span class="sxs-lookup"><span data-stu-id="e3a62-136">d.</span></span> <span data-ttu-id="e3a62-137">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="e3a62-137">Click **Create**.</span></span> 


## <a name="grant-permissions"></a><span data-ttu-id="e3a62-138">Udzielanie uprawnień</span><span class="sxs-lookup"><span data-stu-id="e3a62-138">Grant permissions</span></span> 

<span data-ttu-id="e3a62-139">Celem tego kroku Hello jest toogrant aplikacji **odczytuj dane katalogu** toohello uprawnienia **Windows Azure Active Directory** interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="e3a62-139">hello objective of this step is toogrant your application **Read directory data** permissions toohello **Windows Azure Active Directory** API.</span></span>

![Zarejestrować aplikację](./media/active-directory-reporting-api-prerequisites-azure-portal/16.png)
 

<span data-ttu-id="e3a62-141">**toogrant Twojego hello toouse uprawnienia aplikacji interfejsu API:**</span><span class="sxs-lookup"><span data-stu-id="e3a62-141">**toogrant your application permission toouse hello API:**</span></span>

1. <span data-ttu-id="e3a62-142">Na powitania **rejestracji aplikacji** bloku, na liście aplikacji hello, kliknij przycisk **aplikacji interfejsu API raportowania**.</span><span class="sxs-lookup"><span data-stu-id="e3a62-142">On hello **App registrations** blade, in hello apps list, click **Reporting API application**.</span></span>

2. <span data-ttu-id="e3a62-143">Na powitania **aplikacji interfejsu API raportowania** bloku na powitania narzędzi u góry hello kliknij **ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="e3a62-143">On hello **Reporting API application** blade, in hello toolbar on hello top, click **Settings**.</span></span> 

    ![Zarejestrować aplikację](./media/active-directory-reporting-api-prerequisites-azure-portal/05.png)

3. <span data-ttu-id="e3a62-145">Na powitania **ustawienia** bloku, kliknij przycisk **wymagane uprawnienia**.</span><span class="sxs-lookup"><span data-stu-id="e3a62-145">On hello **Settings** blade, click **Required permissions**.</span></span> 

    ![Zarejestrować aplikację](./media/active-directory-reporting-api-prerequisites-azure-portal/06.png)

4. <span data-ttu-id="e3a62-147">Na powitania **wymagane uprawnienia** bloku w hello **interfejsu API** kliknij **Windows Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e3a62-147">On hello **Required permissions** blade, in hello **API** list, click **Windows Azure Active Directory**.</span></span> 

    ![Zarejestrować aplikację](./media/active-directory-reporting-api-prerequisites-azure-portal/07.png)

5. <span data-ttu-id="e3a62-149">Na powitania **Włącz dostęp** bloku, wybierz opcję **odczytuj dane katalogu**.</span><span class="sxs-lookup"><span data-stu-id="e3a62-149">On hello **Enable Access** blade, select **Read directory data**.</span></span> 

    ![Zarejestrować aplikację](./media/active-directory-reporting-api-prerequisites-azure-portal/08.png)

6. <span data-ttu-id="e3a62-151">Witaj pasku narzędzi u góry hello, kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="e3a62-151">In hello toolbar on hello top, click **Save**.</span></span>

    ![Zarejestrować aplikację](./media/active-directory-reporting-api-prerequisites-azure-portal/15.png)

## <a name="gather-configuration-settings"></a><span data-ttu-id="e3a62-153">Zbierz ustawienia konfiguracji</span><span class="sxs-lookup"><span data-stu-id="e3a62-153">Gather configuration settings</span></span> 
<span data-ttu-id="e3a62-154">W tej sekcji opisano sposób hello tooget następujące ustawienia z katalogu:</span><span class="sxs-lookup"><span data-stu-id="e3a62-154">This section shows you how tooget hello following settings from your directory:</span></span>

* <span data-ttu-id="e3a62-155">Nazwa domeny</span><span class="sxs-lookup"><span data-stu-id="e3a62-155">Domain name</span></span>
* <span data-ttu-id="e3a62-156">Identyfikator klienta</span><span class="sxs-lookup"><span data-stu-id="e3a62-156">Client ID</span></span>
* <span data-ttu-id="e3a62-157">Klucz tajny klienta</span><span class="sxs-lookup"><span data-stu-id="e3a62-157">Client secret</span></span>

<span data-ttu-id="e3a62-158">Należy korzystać z tych wartości podczas konfigurowania raportowania interfejsu API toohello wywołania.</span><span class="sxs-lookup"><span data-stu-id="e3a62-158">You need these values when configuring calls toohello reporting API.</span></span> 

### <a name="get-your-domain-name"></a><span data-ttu-id="e3a62-159">Pobierz nazwę domeny</span><span class="sxs-lookup"><span data-stu-id="e3a62-159">Get your domain name</span></span>

<span data-ttu-id="e3a62-160">**tooget nazwy domeny:**</span><span class="sxs-lookup"><span data-stu-id="e3a62-160">**tooget your domain name:**</span></span>

1. <span data-ttu-id="e3a62-161">W hello [portalu Azure](https://portal.azure.com)na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e3a62-161">In hello [Azure portal](https://portal.azure.com), on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![Zarejestrować aplikację](./media/active-directory-reporting-api-prerequisites-azure-portal/01.png) 

2. <span data-ttu-id="e3a62-163">Na powitania **usługi Azure Active Directory** bloku, kliknij przycisk **nazwy domen**.</span><span class="sxs-lookup"><span data-stu-id="e3a62-163">On hello **Azure Active Directory** blade, click **Domain names**.</span></span>

    ![Zarejestrować aplikację](./media/active-directory-reporting-api-prerequisites-azure-portal/09.png) 

3. <span data-ttu-id="e3a62-165">Skopiuj nazwę domeny z hello listy domen.</span><span class="sxs-lookup"><span data-stu-id="e3a62-165">Copy your domain name from hello list of domains.</span></span>


### <a name="get-your-applications-client-id"></a><span data-ttu-id="e3a62-166">Pobieranie Identyfikatora klienta aplikacji</span><span class="sxs-lookup"><span data-stu-id="e3a62-166">Get your application's client ID</span></span>

<span data-ttu-id="e3a62-167">**tooget identyfikator klienta aplikacji:**</span><span class="sxs-lookup"><span data-stu-id="e3a62-167">**tooget your application's client ID:**</span></span>

1. <span data-ttu-id="e3a62-168">W hello [portalu Azure](https://portal.azure.com)na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e3a62-168">In hello [Azure portal](https://portal.azure.com), on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![Zarejestrować aplikację](./media/active-directory-reporting-api-prerequisites-azure-portal/01.png) 

2. <span data-ttu-id="e3a62-170">Na powitania **rejestracji aplikacji** bloku, na liście aplikacji hello, kliknij przycisk **aplikacji interfejsu API raportowania**.</span><span class="sxs-lookup"><span data-stu-id="e3a62-170">On hello **App registrations** blade, in hello apps list, click **Reporting API application**.</span></span>

3. <span data-ttu-id="e3a62-171">Na powitania **aplikacji interfejsu API raportowania** bloku na powitania **identyfikator aplikacji**, kliknij przycisk **kliknij toocopy**.</span><span class="sxs-lookup"><span data-stu-id="e3a62-171">On hello **Reporting API application** blade, at hello **Application ID**, click **Click toocopy**.</span></span>

    ![Zarejestrować aplikację](./media/active-directory-reporting-api-prerequisites-azure-portal/11.png) 



### <a name="get-your-applications-client-secret"></a><span data-ttu-id="e3a62-173">Pobierz klucz tajny klienta aplikacji</span><span class="sxs-lookup"><span data-stu-id="e3a62-173">Get your application's client secret</span></span>
<span data-ttu-id="e3a62-174">tooget klienta aplikacji tajne, należy toocreate nowy klucz i zapisz jego wartości podczas zapisywania nowego klucza hello, ponieważ nie jest możliwe tooretrieve później już tej wartości.</span><span class="sxs-lookup"><span data-stu-id="e3a62-174">tooget your application's client secret, you need toocreate a new key and save its value upon saving hello new key because it is not possible tooretrieve this value later anymore.</span></span>

<span data-ttu-id="e3a62-175">**tooget klucz tajny klienta aplikacji:**</span><span class="sxs-lookup"><span data-stu-id="e3a62-175">**tooget your application's client secret:**</span></span>

1. <span data-ttu-id="e3a62-176">W hello [portalu Azure](https://portal.azure.com)na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e3a62-176">In hello [Azure portal](https://portal.azure.com), on hello left navigation pane, click **Active Directory**.</span></span>
   
    ![Zarejestrować aplikację](./media/active-directory-reporting-api-prerequisites-azure-portal/01.png) 

2. <span data-ttu-id="e3a62-178">Na powitania **rejestracji aplikacji** bloku, na liście aplikacji hello, kliknij przycisk **aplikacji interfejsu API raportowania**.</span><span class="sxs-lookup"><span data-stu-id="e3a62-178">On hello **App registrations** blade, in hello apps list, click **Reporting API application**.</span></span>


3. <span data-ttu-id="e3a62-179">Na powitania **aplikacji interfejsu API raportowania** bloku na powitania narzędzi u góry hello kliknij **ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="e3a62-179">On hello **Reporting API application** blade, in hello toolbar on hello top, click **Settings**.</span></span> 

    ![Zarejestrować aplikację](./media/active-directory-reporting-api-prerequisites-azure-portal/05.png)

4. <span data-ttu-id="e3a62-181">Na powitania **ustawienia** bloku w hello **dostępu APIR** kliknij **klucze**.</span><span class="sxs-lookup"><span data-stu-id="e3a62-181">On hello **Settings** blade, in hello **APIR Access** section, click **Keys**.</span></span> 

    ![Zarejestrować aplikację](./media/active-directory-reporting-api-prerequisites-azure-portal/12.png)


5. <span data-ttu-id="e3a62-183">Na powitania **klucze** blok, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="e3a62-183">On hello **Keys** blade, perform hello following steps:</span></span>

    ![Zarejestrować aplikację](./media/active-directory-reporting-api-prerequisites-azure-portal/14.png)

    <span data-ttu-id="e3a62-185">a.</span><span class="sxs-lookup"><span data-stu-id="e3a62-185">a.</span></span> <span data-ttu-id="e3a62-186">W hello **opis** pole tekstowe, typ `Reporting API`.</span><span class="sxs-lookup"><span data-stu-id="e3a62-186">In hello **Description** textbox, type `Reporting API`.</span></span>

    <span data-ttu-id="e3a62-187">b.</span><span class="sxs-lookup"><span data-stu-id="e3a62-187">b.</span></span> <span data-ttu-id="e3a62-188">Jako **Expires**, wybierz pozycję **w 2 lata**.</span><span class="sxs-lookup"><span data-stu-id="e3a62-188">As **Expires**, select **In 2 years**.</span></span>

    <span data-ttu-id="e3a62-189">c.</span><span class="sxs-lookup"><span data-stu-id="e3a62-189">c.</span></span> <span data-ttu-id="e3a62-190">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="e3a62-190">Click **Save**.</span></span>

    <span data-ttu-id="e3a62-191">d.</span><span class="sxs-lookup"><span data-stu-id="e3a62-191">d.</span></span> <span data-ttu-id="e3a62-192">Skopiuj wartość klucza hello.</span><span class="sxs-lookup"><span data-stu-id="e3a62-192">Copy hello key value.</span></span>


## <a name="next-steps"></a><span data-ttu-id="e3a62-193">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e3a62-193">Next Steps</span></span>
* <span data-ttu-id="e3a62-194">Czy można tak, jak dane z usługi Azure AD hello hello tooaccess raportowania interfejsu API w sposób programowy</span><span class="sxs-lookup"><span data-stu-id="e3a62-194">Would you like tooaccess hello data from hello Azure AD reporting API in a programmatic manner?</span></span> <span data-ttu-id="e3a62-195">Zapoznaj się z [wprowadzenie hello Azure Active Directory interfejsu API raportowania](active-directory-reporting-api-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="e3a62-195">Check out [Getting started with hello Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md).</span></span>
* <span data-ttu-id="e3a62-196">Jeśli chcesz toofind się więcej o usłudze Azure Active Directory, zobacz hello [Azure Active Directory Przewodnik po raportach](active-directory-reporting-guide.md).</span><span class="sxs-lookup"><span data-stu-id="e3a62-196">If you would like toofind out more about Azure Active Directory reporting, see hello [Azure Active Directory Reporting Guide](active-directory-reporting-guide.md).</span></span>  

