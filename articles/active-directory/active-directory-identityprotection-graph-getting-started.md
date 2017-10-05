---
title: "Wprowadzenie do usługi Azure Active Directory Identity Protection oraz Microsoft Graph | Dokumentacja firmy Microsoft"
description: "Wprowadzenie do zapytań programu Microsoft Graph listę zdarzeń o podwyższonym ryzyku i skojarzonych informacji z usługi Azure Active Directory."
services: active-directory
keywords: "ochronę tożsamości usługi Azure active directory, zdarzenie ryzyka, luki w zabezpieczeniach, zasady zabezpieczeń, Microsoft Graph"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: fa109ba7-a914-437b-821d-2bd98e681386
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 9b01ff86da6a1fd4a439a6ba59ea15ed6480cdad
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="get-started-with-azure-active-directory-identity-protection-and-microsoft-graph"></a><span data-ttu-id="e4ee3-104">Wprowadzenie do usługi Azure Active Directory Identity Protection oraz Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="e4ee3-104">Get started with Azure Active Directory Identity Protection and Microsoft Graph</span></span>
<span data-ttu-id="e4ee3-105">Program Microsoft Graph jest Microsoft unified punkt końcowy interfejsu API i stroną główną [Azure Active Directory Identity Protection](active-directory-identityprotection.md) interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="e4ee3-105">Microsoft Graph is the Microsoft unified API endpoint and the home of [Azure Active Directory Identity Protection](active-directory-identityprotection.md) APIs.</span></span> <span data-ttu-id="e4ee3-106">Pierwszy interfejsu API, **identityRiskEvents**, pozwala na zapytanie Microsoft Graph listę [ryzyka zdarzenia](active-directory-identityprotection-risk-events-types.md) i skojarzonych informacji.</span><span class="sxs-lookup"><span data-stu-id="e4ee3-106">The first API, **identityRiskEvents**, allows you to query Microsoft Graph for a list of [risk events](active-directory-identityprotection-risk-events-types.md) and associated information.</span></span> <span data-ttu-id="e4ee3-107">W tym artykule pobiera pracę podczas badania tego interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="e4ee3-107">This article gets you started querying this API.</span></span> <span data-ttu-id="e4ee3-108">Szczegółowe wprowadzenie, pełną dokumentację i dostęp do Eksploratora wykresu, zobacz [witryny Microsoft Graph](https://graph.microsoft.io/).</span><span class="sxs-lookup"><span data-stu-id="e4ee3-108">For an in-depth introduction, full documentation, and access to the Graph Explorer, see the [Microsoft Graph site](https://graph.microsoft.io/).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e4ee3-109">Firma Microsoft zaleca zarządzanie usługą Azure AD przy użyciu [centrum administracyjnego usługi Azure AD](https://aad.portal.azure.com) w witrynie Azure Portal zamiast korzystania z klasycznej witryny Azure Portal przywołanej w niniejszym artykule.</span><span class="sxs-lookup"><span data-stu-id="e4ee3-109">Microsoft recommends that you manage Azure AD using the [Azure AD admin center](https://aad.portal.azure.com) in the Azure portal instead of using the Azure classic portal referenced in this article.</span></span>

<span data-ttu-id="e4ee3-110">Istnieją trzy kroki w celu uzyskiwania dostępu do danych tożsamości ochrony za pomocą programu Microsoft Graph:</span><span class="sxs-lookup"><span data-stu-id="e4ee3-110">There are three steps to accessing Identity Protection data through Microsoft Graph:</span></span>

1. <span data-ttu-id="e4ee3-111">Dodawanie aplikacji przy użyciu klucza tajnego klienta.</span><span class="sxs-lookup"><span data-stu-id="e4ee3-111">Add an application with a client secret.</span></span> 
2. <span data-ttu-id="e4ee3-112">Użyć ten klucz tajny i kilka innych rodzajów informacji do uwierzytelnienia do programu Microsoft Graph, sposób ich otrzymywania tokenu uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="e4ee3-112">Use this secret and a few other pieces of information to authenticate to Microsoft Graph, where you receive an authentication token.</span></span> 
3. <span data-ttu-id="e4ee3-113">Użyj tego tokenu, aby żądania do punktu końcowego interfejsu API i wrócić tożsamości ochrony danych.</span><span class="sxs-lookup"><span data-stu-id="e4ee3-113">Use this token to make requests to the API endpoint and get Identity Protection data back.</span></span>

<span data-ttu-id="e4ee3-114">Przed rozpoczęciem pracy należy:</span><span class="sxs-lookup"><span data-stu-id="e4ee3-114">Before you get started, you’ll need:</span></span>

* <span data-ttu-id="e4ee3-115">Uprawnienia administratora, aby utworzyć aplikację w usłudze Azure AD</span><span class="sxs-lookup"><span data-stu-id="e4ee3-115">Administrator privileges to create the application in Azure AD</span></span>
* <span data-ttu-id="e4ee3-116">Nazwa domeny Twojej dzierżawy (np. contoso.onmicrosoft.com)</span><span class="sxs-lookup"><span data-stu-id="e4ee3-116">The name of your tenant's domain (for example, contoso.onmicrosoft.com)</span></span>

## <a name="add-an-application-with-a-client-secret"></a><span data-ttu-id="e4ee3-117">Dodawanie aplikacji z klucz tajny klienta</span><span class="sxs-lookup"><span data-stu-id="e4ee3-117">Add an application with a client secret</span></span>
1. <span data-ttu-id="e4ee3-118">[Zaloguj się](https://manage.windowsazure.com) do portalu klasycznego Azure jako administrator.</span><span class="sxs-lookup"><span data-stu-id="e4ee3-118">[Sign in](https://manage.windowsazure.com) to your Azure classic portal as an administrator.</span></span> 
2. <span data-ttu-id="e4ee3-119">W lewym okienku nawigacji, wybierz polecenie **usługi Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e4ee3-119">On on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Tworzenie aplikacji](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_01.png)
3. <span data-ttu-id="e4ee3-121">Z **katalogu** listy, wybierz katalog, dla którego chcesz włączyć integracji katalogów.</span><span class="sxs-lookup"><span data-stu-id="e4ee3-121">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
4. <span data-ttu-id="e4ee3-122">W menu u góry kliknij **aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="e4ee3-122">In the menu on the top, click **Applications**.</span></span>
   
    ![Tworzenie aplikacji](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_02.png)
5. <span data-ttu-id="e4ee3-124">Kliknij przycisk **Dodaj** w dolnej części strony.</span><span class="sxs-lookup"><span data-stu-id="e4ee3-124">Click **Add** at the bottom of the page.</span></span>
   
    ![Tworzenie aplikacji](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_03.png)
6. <span data-ttu-id="e4ee3-126">Na **co chcesz zrobić** okna dialogowego, kliknij przycisk **Dodaj aplikację moją organizację**.</span><span class="sxs-lookup"><span data-stu-id="e4ee3-126">On the **What do you want to do** dialog, click **Add an application my organization is developing**.</span></span>
   
    ![Tworzenie aplikacji](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_04.png)
7. <span data-ttu-id="e4ee3-128">Na **Powiedz nam o aplikacji** okna dialogowego, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="e4ee3-128">On the **Tell us about your application** dialog, perform the following steps:</span></span>
   
    ![Tworzenie aplikacji](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_05.png)
   
    <span data-ttu-id="e4ee3-130">a.</span><span class="sxs-lookup"><span data-stu-id="e4ee3-130">a.</span></span> <span data-ttu-id="e4ee3-131">W **nazwa** tekstowym, wpisz nazwę dla aplikacji (np.: Aplikacja interfejsu API zdarzenia ryzyka AADIP).</span><span class="sxs-lookup"><span data-stu-id="e4ee3-131">In the **Name** textbox, type a name for your application (e.g.: AADIP Risk Event API Application).</span></span>
   
    <span data-ttu-id="e4ee3-132">b.</span><span class="sxs-lookup"><span data-stu-id="e4ee3-132">b.</span></span> <span data-ttu-id="e4ee3-133">Jako **typu**, wybierz pozycję **aplikacji sieci Web i / lub interfejs API sieci Web**.</span><span class="sxs-lookup"><span data-stu-id="e4ee3-133">As **Type**, select **Web Application And / Or Web API**.</span></span>
   
    <span data-ttu-id="e4ee3-134">c.</span><span class="sxs-lookup"><span data-stu-id="e4ee3-134">c.</span></span> <span data-ttu-id="e4ee3-135">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="e4ee3-135">Click **Next**.</span></span>
8. <span data-ttu-id="e4ee3-136">Na **właściwości aplikacji** okna dialogowego, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="e4ee3-136">On the **App properties** dialog, perform the following steps:</span></span>
   
    ![Tworzenie aplikacji](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_06.png)
   
    <span data-ttu-id="e4ee3-138">a.</span><span class="sxs-lookup"><span data-stu-id="e4ee3-138">a.</span></span> <span data-ttu-id="e4ee3-139">W **adres URL logowania** pole tekstowe, typ `http://localhost`.</span><span class="sxs-lookup"><span data-stu-id="e4ee3-139">In the **Sign-On URL** textbox, type `http://localhost`.</span></span>
   
    <span data-ttu-id="e4ee3-140">b.</span><span class="sxs-lookup"><span data-stu-id="e4ee3-140">b.</span></span> <span data-ttu-id="e4ee3-141">W **identyfikator URI aplikacji** pole tekstowe, typ `http://localhost`.</span><span class="sxs-lookup"><span data-stu-id="e4ee3-141">In the **App ID URI** textbox, type `http://localhost`.</span></span>
   
    <span data-ttu-id="e4ee3-142">c.</span><span class="sxs-lookup"><span data-stu-id="e4ee3-142">c.</span></span> <span data-ttu-id="e4ee3-143">Kliknij przycisk **Complete** (Zakończ).</span><span class="sxs-lookup"><span data-stu-id="e4ee3-143">Click **Complete**.</span></span>

<span data-ttu-id="e4ee3-144">Możesz teraz skonfigurować aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e4ee3-144">Your can now configure your application.</span></span>

![Tworzenie aplikacji](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_07.png)

## <a name="grant-your-application-permission-to-use-the-api"></a><span data-ttu-id="e4ee3-146">Zezwolić aplikacji za pomocą interfejsu API</span><span class="sxs-lookup"><span data-stu-id="e4ee3-146">Grant your application permission to use the API</span></span>
1. <span data-ttu-id="e4ee3-147">Na stronie aplikacji, w menu u góry, kliknij przycisk **Konfiguruj**.</span><span class="sxs-lookup"><span data-stu-id="e4ee3-147">On your application's page, in the menu on the top, click **Configure**.</span></span> 
   
    ![Tworzenie aplikacji](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_08.png)
2. <span data-ttu-id="e4ee3-149">W **uprawnień dotyczących innych aplikacji** kliknij **Dodaj aplikację**.</span><span class="sxs-lookup"><span data-stu-id="e4ee3-149">In the **permissions to other applications** section, click **Add application**.</span></span>
   
    ![Tworzenie aplikacji](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_09.png)
3. <span data-ttu-id="e4ee3-151">Na **uprawnień dotyczących innych aplikacji** okna dialogowego, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="e4ee3-151">On the **permissions to other applications** dialog, perform the following steps:</span></span>
   
    ![Tworzenie aplikacji](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_10.png)
   
    <span data-ttu-id="e4ee3-153">a.</span><span class="sxs-lookup"><span data-stu-id="e4ee3-153">a.</span></span> <span data-ttu-id="e4ee3-154">Wybierz **Microsoft Graph**.</span><span class="sxs-lookup"><span data-stu-id="e4ee3-154">Select **Microsoft Graph**.</span></span>
   
    <span data-ttu-id="e4ee3-155">b.</span><span class="sxs-lookup"><span data-stu-id="e4ee3-155">b.</span></span> <span data-ttu-id="e4ee3-156">Kliknij przycisk **Complete** (Zakończ).</span><span class="sxs-lookup"><span data-stu-id="e4ee3-156">Click **Complete**.</span></span>
4. <span data-ttu-id="e4ee3-157">Kliknij przycisk **uprawnienia aplikacji: 0**, a następnie wybierz **odczytać wszystkie informacje dotyczące zdarzenia ryzyka tożsamości**.</span><span class="sxs-lookup"><span data-stu-id="e4ee3-157">Click **Application Permissions: 0**, and then select **Read all identity risk event information**.</span></span>
   
    ![Tworzenie aplikacji](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_11.png)
5. <span data-ttu-id="e4ee3-159">Kliknij przycisk **Zapisz** w dolnej części strony.</span><span class="sxs-lookup"><span data-stu-id="e4ee3-159">Click **Save** at the bottom of the page.</span></span>
   
    ![Tworzenie aplikacji](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_12.png)

## <a name="get-an-access-key"></a><span data-ttu-id="e4ee3-161">Uzyskiwanie klucza dostępu</span><span class="sxs-lookup"><span data-stu-id="e4ee3-161">Get an access key</span></span>
1. <span data-ttu-id="e4ee3-162">Na stronie aplikacji w **klucze** wybierz 1 rok jako czas trwania.</span><span class="sxs-lookup"><span data-stu-id="e4ee3-162">On your application's page, in the **keys** section, select 1 year as duration.</span></span>
   
    ![Tworzenie aplikacji](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_13.png)
2. <span data-ttu-id="e4ee3-164">Kliknij przycisk **Zapisz** w dolnej części strony.</span><span class="sxs-lookup"><span data-stu-id="e4ee3-164">Click **Save** at the bottom of the page.</span></span>
   
    ![Tworzenie aplikacji](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_12.png)
3. <span data-ttu-id="e4ee3-166">w sekcji klucze skopiować wartości z nowo utworzony klucz, a następnie wklej go w bezpiecznym miejscu.</span><span class="sxs-lookup"><span data-stu-id="e4ee3-166">in the keys section, copy the value of your newly created key, and then paste it into a safe location.</span></span>
   
    ![Tworzenie aplikacji](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_14.png)
   
   > [!NOTE]
   > <span data-ttu-id="e4ee3-168">Jeśli ten klucz zostanie utracone, konieczne będzie wróć do tej sekcji i Utwórz nowy klucz.</span><span class="sxs-lookup"><span data-stu-id="e4ee3-168">If you lose this key, you will have to return to this section and create a new key.</span></span> <span data-ttu-id="e4ee3-169">Zachowaj ten klucz tajny: każdy użytkownik, który można uzyskać dostęp do danych.</span><span class="sxs-lookup"><span data-stu-id="e4ee3-169">Keep this key a secret: anyone who has it can access your data.</span></span>
   > 
   > 
4. <span data-ttu-id="e4ee3-170">W **właściwości** sekcji, skopiuj **identyfikator klienta**, a następnie wklej go w bezpiecznym miejscu.</span><span class="sxs-lookup"><span data-stu-id="e4ee3-170">In the **properties** section, copy the **Client ID**, and then paste it into a safe location.</span></span> 

## <a name="authenticate-to-microsoft-graph-and-query-the-identity-risk-events-api"></a><span data-ttu-id="e4ee3-171">Uwierzytelnianie Microsoft Graph i wykonywać zapytania interfejsu API zdarzenia ryzyka tożsamości</span><span class="sxs-lookup"><span data-stu-id="e4ee3-171">Authenticate to Microsoft Graph and query the Identity Risk Events API</span></span>
<span data-ttu-id="e4ee3-172">W tym momencie powinny mieć:</span><span class="sxs-lookup"><span data-stu-id="e4ee3-172">At this point, you should have:</span></span>

* <span data-ttu-id="e4ee3-173">Identyfikator klienta skopiowane powyżej</span><span class="sxs-lookup"><span data-stu-id="e4ee3-173">The client ID you copied above</span></span>
* <span data-ttu-id="e4ee3-174">Klucz skopiowane powyżej</span><span class="sxs-lookup"><span data-stu-id="e4ee3-174">The key you copied above</span></span>
* <span data-ttu-id="e4ee3-175">Nazwa domeny Twojej dzierżawy</span><span class="sxs-lookup"><span data-stu-id="e4ee3-175">The name of your tenant's domain</span></span>

<span data-ttu-id="e4ee3-176">W celu uwierzytelnienia wysłanie żądania post do `https://login.microsoft.com` z następującymi parametrami w treści:</span><span class="sxs-lookup"><span data-stu-id="e4ee3-176">To authenticate, send a post request to `https://login.microsoft.com` with the following parameters in the body:</span></span>

* <span data-ttu-id="e4ee3-177">Typ grant_type: "**client_credentials**"</span><span class="sxs-lookup"><span data-stu-id="e4ee3-177">grant_type: “**client_credentials**”</span></span>
* <span data-ttu-id="e4ee3-178">Zasób: "**https://graph.microsoft.com**"</span><span class="sxs-lookup"><span data-stu-id="e4ee3-178">resource: “**https://graph.microsoft.com**”</span></span>
* <span data-ttu-id="e4ee3-179">client_id:<your client ID></span><span class="sxs-lookup"><span data-stu-id="e4ee3-179">client_id: <your client ID></span></span>
* <span data-ttu-id="e4ee3-180">client_secret:<your key></span><span class="sxs-lookup"><span data-stu-id="e4ee3-180">client_secret: <your key></span></span>

> [!NOTE]
> <span data-ttu-id="e4ee3-181">Należy podać wartości **client_id** i **client_secret** parametru.</span><span class="sxs-lookup"><span data-stu-id="e4ee3-181">You need to provide values for the **client_id** and the **client_secret** parameter.</span></span>
> 
> 

<span data-ttu-id="e4ee3-182">Jeśli to się powiedzie, to zwraca token uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="e4ee3-182">If successful, this returns an authentication token.</span></span>  
<span data-ttu-id="e4ee3-183">Aby wywołać interfejs API, należy utworzyć nagłówek z następującym parametrem:</span><span class="sxs-lookup"><span data-stu-id="e4ee3-183">To call the API, create a header with the following parameter:</span></span>

    `Authorization`=”<token_type> <access_token>"


<span data-ttu-id="e4ee3-184">Podczas uwierzytelniania, można znaleźć typu token i token dostępu w tokenie zwrócony.</span><span class="sxs-lookup"><span data-stu-id="e4ee3-184">When authenticating, you can find the token type and access token in the returned token.</span></span>

<span data-ttu-id="e4ee3-185">Wyślij ten nagłówek jako żądania do następującego adresu URL interfejsu API:`https://graph.microsoft.com/beta/identityRiskEvents`</span><span class="sxs-lookup"><span data-stu-id="e4ee3-185">Send this header as a request to the following API URL: `https://graph.microsoft.com/beta/identityRiskEvents`</span></span>

<span data-ttu-id="e4ee3-186">Odpowiedź, w przypadku powodzenia jest zbierania zdarzeń o podwyższonym ryzyku tożsamości i skojarzone dane w formacie OData JSON, który może być analizowana i obsługiwane zgodnie z własnymi potrzebami.</span><span class="sxs-lookup"><span data-stu-id="e4ee3-186">The response, if successful, is a collection of identity risk events and associated data in the OData JSON format, which can be parsed and handled as see fit.</span></span>

<span data-ttu-id="e4ee3-187">Oto przykładowy kod do uwierzytelniania i wywołanie interfejsu API przy użyciu programu Powershell.</span><span class="sxs-lookup"><span data-stu-id="e4ee3-187">Here’s sample code for authenticating and calling the API using Powershell.</span></span>  
<span data-ttu-id="e4ee3-188">Wystarczy dodać Identyfikatora klienta, a dla klucza dzierżawy domeny.</span><span class="sxs-lookup"><span data-stu-id="e4ee3-188">Just add your client ID, key, and tenant domain.</span></span>

    $ClientID       = "<your client ID here>"        # Should be a ~36 hex character string; insert your info here
    $ClientSecret   = "<your client secret here>"    # Should be a ~44 character string; insert your info here
    $tenantdomain   = "<your tenant domain here>"    # For example, contoso.onmicrosoft.com

    $loginURL       = "https://login.microsoft.com"
    $resource       = "https://graph.microsoft.com"

    $body       = @{grant_type="client_credentials";resource=$resource;client_id=$ClientID;client_secret=$ClientSecret}
    $oauth      = Invoke-RestMethod -Method Post -Uri $loginURL/$tenantdomain/oauth2/token?api-version=1.0 -Body $body

    Write-Output $oauth

    if ($oauth.access_token -ne $null) {
        $headerParams = @{'Authorization'="$($oauth.token_type) $($oauth.access_token)"}

        $url = "https://graph.microsoft.com/beta/identityRiskEvents"
        Write-Output $url

        $myReport = (Invoke-WebRequest -UseBasicParsing -Headers $headerParams -Uri $url)

        foreach ($event in ($myReport.Content | ConvertFrom-Json).value) {
            Write-Output $event
        }

    } else {
        Write-Host "ERROR: No Access Token"
    } 


## <a name="next-steps"></a><span data-ttu-id="e4ee3-189">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e4ee3-189">Next steps</span></span>
<span data-ttu-id="e4ee3-190">Gratulacje, wystarczy wprowadzić Twoje pierwsze wywołanie do programu Microsoft Graph!</span><span class="sxs-lookup"><span data-stu-id="e4ee3-190">Congratulations, you just made your first call to Microsoft Graph!</span></span>  
<span data-ttu-id="e4ee3-191">Teraz można zbadać zdarzenia o podwyższonym ryzyku tożsamości i korzystanie z danych, jednak użytkownik mieści się w temacie.</span><span class="sxs-lookup"><span data-stu-id="e4ee3-191">Now you can query identity risk events and use the data however you see fit.</span></span>

<span data-ttu-id="e4ee3-192">Aby dowiedzieć się więcej na temat programu Microsoft Graph i jak tworzyć aplikacje przy użyciu interfejsu API programu Graph, zapoznaj się [dokumentacji](https://graph.microsoft.io/docs) i znacznie więcej informacji na temat [witryny Microsoft Graph](https://graph.microsoft.io/).</span><span class="sxs-lookup"><span data-stu-id="e4ee3-192">To learn more about Microsoft Graph and how to build applications using the Graph API, check out the [documentation](https://graph.microsoft.io/docs) and much more on the [Microsoft Graph site](https://graph.microsoft.io/).</span></span> <span data-ttu-id="e4ee3-193">Ponadto upewnij się, że zakładki [Azure AD Identity Protection API](https://graph.microsoft.io/docs/api-reference/beta/resources/identityprotection_root) strony, która zawiera listę wszystkich interfejsów API ochrony tożsamości, które są dostępne na wykresie.</span><span class="sxs-lookup"><span data-stu-id="e4ee3-193">Also, make sure to bookmark the [Azure AD Identity Protection API](https://graph.microsoft.io/docs/api-reference/beta/resources/identityprotection_root) page that lists all of the Identity Protection APIs available in Graph.</span></span> <span data-ttu-id="e4ee3-194">Jak możemy dodać nowe sposoby pracy z ochrony tożsamości za pomocą interfejsu API, zobaczysz je na tej stronie.</span><span class="sxs-lookup"><span data-stu-id="e4ee3-194">As we add new ways to work with Identity Protection via API, you’ll see them on that page.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e4ee3-195">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="e4ee3-195">Additional resources</span></span>
* [<span data-ttu-id="e4ee3-196">Ochronę tożsamości usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e4ee3-196">Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection.md)
* [<span data-ttu-id="e4ee3-197">Rodzaje zdarzeń o podwyższonym ryzyku wykrywanych przez Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="e4ee3-197">Types of risk events detected by Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection-risk-events-types.md)
* [<span data-ttu-id="e4ee3-198">Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="e4ee3-198">Microsoft Graph</span></span>](https://graph.microsoft.io/)
* [<span data-ttu-id="e4ee3-199">Omówienie programu Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="e4ee3-199">Overview of Microsoft Graph</span></span>](https://graph.microsoft.io/docs)
* [<span data-ttu-id="e4ee3-200">Katalogu głównego usługi programu Azure AD Identity Protection</span><span class="sxs-lookup"><span data-stu-id="e4ee3-200">Azure AD Identity Protection Service Root</span></span>](https://graph.microsoft.io/docs/api-reference/beta/resources/identityprotection_root)

