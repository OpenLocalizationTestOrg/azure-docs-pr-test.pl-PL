---
title: "aaaGet wprowadzenie do usługi Azure Active Directory Identity Protection oraz Microsoft Graph | Dokumentacja firmy Microsoft"
description: "Zawiera wprowadzenie tooquery Microsoft Graph listę zdarzeń o podwyższonym ryzyku i skojarzonych informacji z usługi Azure Active Directory."
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
ms.openlocfilehash: 75b8b7629a0120d8101f6fde0d9163122503d276
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-active-directory-identity-protection-and-microsoft-graph"></a><span data-ttu-id="1ef85-104">Wprowadzenie do usługi Azure Active Directory Identity Protection oraz Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="1ef85-104">Get started with Azure Active Directory Identity Protection and Microsoft Graph</span></span>
<span data-ttu-id="1ef85-105">Program Microsoft Graph jest hello Microsoft unified punkt końcowy interfejsu API i hello macierzystego z [Azure Active Directory Identity Protection](active-directory-identityprotection.md) interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="1ef85-105">Microsoft Graph is hello Microsoft unified API endpoint and hello home of [Azure Active Directory Identity Protection](active-directory-identityprotection.md) APIs.</span></span> <span data-ttu-id="1ef85-106">pierwszy interfejsu API Hello **identityRiskEvents**, pozwala tooquery Microsoft Graph, aby uzyskać listę z [ryzyka zdarzenia](active-directory-identityprotection-risk-events-types.md) i skojarzone z nimi informacje.</span><span class="sxs-lookup"><span data-stu-id="1ef85-106">hello first API, **identityRiskEvents**, allows you tooquery Microsoft Graph for a list of [risk events](active-directory-identityprotection-risk-events-types.md) and associated information.</span></span> <span data-ttu-id="1ef85-107">W tym artykule pobiera pracę podczas badania tego interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="1ef85-107">This article gets you started querying this API.</span></span> <span data-ttu-id="1ef85-108">Szczegółowe wprowadzenie, pełną dokumentację i toohello dostępu Explorer wykresu, zobacz hello [witryny Microsoft Graph](https://graph.microsoft.io/).</span><span class="sxs-lookup"><span data-stu-id="1ef85-108">For an in-depth introduction, full documentation, and access toohello Graph Explorer, see hello [Microsoft Graph site](https://graph.microsoft.io/).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1ef85-109">Firma Microsoft zaleca się, że zarządzania usługi Azure AD przy użyciu hello [Centrum administracyjnego usługi Azure AD](https://aad.portal.azure.com) w hello portalu Azure zamiast hello klasycznego portalu Azure, do którego odwołuje się w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="1ef85-109">Microsoft recommends that you manage Azure AD using hello [Azure AD admin center](https://aad.portal.azure.com) in hello Azure portal instead of using hello Azure classic portal referenced in this article.</span></span>

<span data-ttu-id="1ef85-110">Istnieją trzy kroki tooaccessing tożsamości ochrony danych za pomocą programu Microsoft Graph:</span><span class="sxs-lookup"><span data-stu-id="1ef85-110">There are three steps tooaccessing Identity Protection data through Microsoft Graph:</span></span>

1. <span data-ttu-id="1ef85-111">Dodawanie aplikacji przy użyciu klucza tajnego klienta.</span><span class="sxs-lookup"><span data-stu-id="1ef85-111">Add an application with a client secret.</span></span> 
2. <span data-ttu-id="1ef85-112">Użyj tego klucza tajnego i kilka innych części informacji tooauthenticate tooMicrosoft wykresu służący do otrzymywania tokenu uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="1ef85-112">Use this secret and a few other pieces of information tooauthenticate tooMicrosoft Graph, where you receive an authentication token.</span></span> 
3. <span data-ttu-id="1ef85-113">Użyj tego punktu końcowego tokenu toomake żądań toohello interfejsu API i wrócić tożsamości ochrony danych.</span><span class="sxs-lookup"><span data-stu-id="1ef85-113">Use this token toomake requests toohello API endpoint and get Identity Protection data back.</span></span>

<span data-ttu-id="1ef85-114">Przed rozpoczęciem pracy należy:</span><span class="sxs-lookup"><span data-stu-id="1ef85-114">Before you get started, you’ll need:</span></span>

* <span data-ttu-id="1ef85-115">Aplikacji hello toocreate uprawnień administratora w usłudze Azure AD</span><span class="sxs-lookup"><span data-stu-id="1ef85-115">Administrator privileges toocreate hello application in Azure AD</span></span>
* <span data-ttu-id="1ef85-116">Witaj nazwy domeny Twojej dzierżawy (np. contoso.onmicrosoft.com)</span><span class="sxs-lookup"><span data-stu-id="1ef85-116">hello name of your tenant's domain (for example, contoso.onmicrosoft.com)</span></span>

## <a name="add-an-application-with-a-client-secret"></a><span data-ttu-id="1ef85-117">Dodawanie aplikacji z klucz tajny klienta</span><span class="sxs-lookup"><span data-stu-id="1ef85-117">Add an application with a client secret</span></span>
1. <span data-ttu-id="1ef85-118">[Zaloguj się](https://manage.windowsazure.com) tooyour klasycznego portalu Azure jako administrator.</span><span class="sxs-lookup"><span data-stu-id="1ef85-118">[Sign in](https://manage.windowsazure.com) tooyour Azure classic portal as an administrator.</span></span> 
2. <span data-ttu-id="1ef85-119">W okienku nawigacji po lewej stronie powitania polecenie **usługi Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="1ef85-119">On on hello left navigation pane, click **Active Directory**.</span></span> 
   
    ![Tworzenie aplikacji](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_01.png)
3. <span data-ttu-id="1ef85-121">Z hello **katalogu** listy, wybierz hello katalogu, dla której ma zostać tooenable integracji katalogów.</span><span class="sxs-lookup"><span data-stu-id="1ef85-121">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
4. <span data-ttu-id="1ef85-122">W menu hello na górze hello, kliknij przycisk **aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="1ef85-122">In hello menu on hello top, click **Applications**.</span></span>
   
    ![Tworzenie aplikacji](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_02.png)
5. <span data-ttu-id="1ef85-124">Kliknij przycisk **Dodaj** u dołu hello hello strony.</span><span class="sxs-lookup"><span data-stu-id="1ef85-124">Click **Add** at hello bottom of hello page.</span></span>
   
    ![Tworzenie aplikacji](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_03.png)
6. <span data-ttu-id="1ef85-126">Na powitania **co chcesz toodo** okna dialogowego, kliknij przycisk **Dodaj aplikację moją organizację**.</span><span class="sxs-lookup"><span data-stu-id="1ef85-126">On hello **What do you want toodo** dialog, click **Add an application my organization is developing**.</span></span>
   
    ![Tworzenie aplikacji](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_04.png)
7. <span data-ttu-id="1ef85-128">Na powitania **Powiedz nam o aplikacji** okna dialogowego, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="1ef85-128">On hello **Tell us about your application** dialog, perform hello following steps:</span></span>
   
    ![Tworzenie aplikacji](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_05.png)
   
    <span data-ttu-id="1ef85-130">a.</span><span class="sxs-lookup"><span data-stu-id="1ef85-130">a.</span></span> <span data-ttu-id="1ef85-131">W hello **nazwa** tekstowym, wpisz nazwę dla aplikacji (np.: Aplikacja interfejsu API zdarzenia ryzyka AADIP).</span><span class="sxs-lookup"><span data-stu-id="1ef85-131">In hello **Name** textbox, type a name for your application (e.g.: AADIP Risk Event API Application).</span></span>
   
    <span data-ttu-id="1ef85-132">b.</span><span class="sxs-lookup"><span data-stu-id="1ef85-132">b.</span></span> <span data-ttu-id="1ef85-133">Jako **typu**, wybierz pozycję **aplikacji sieci Web i / lub interfejs API sieci Web**.</span><span class="sxs-lookup"><span data-stu-id="1ef85-133">As **Type**, select **Web Application And / Or Web API**.</span></span>
   
    <span data-ttu-id="1ef85-134">c.</span><span class="sxs-lookup"><span data-stu-id="1ef85-134">c.</span></span> <span data-ttu-id="1ef85-135">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="1ef85-135">Click **Next**.</span></span>
8. <span data-ttu-id="1ef85-136">Na powitania **właściwości aplikacji** okna dialogowego, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="1ef85-136">On hello **App properties** dialog, perform hello following steps:</span></span>
   
    ![Tworzenie aplikacji](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_06.png)
   
    <span data-ttu-id="1ef85-138">a.</span><span class="sxs-lookup"><span data-stu-id="1ef85-138">a.</span></span> <span data-ttu-id="1ef85-139">W hello **adres URL logowania** pole tekstowe, typ `http://localhost`.</span><span class="sxs-lookup"><span data-stu-id="1ef85-139">In hello **Sign-On URL** textbox, type `http://localhost`.</span></span>
   
    <span data-ttu-id="1ef85-140">b.</span><span class="sxs-lookup"><span data-stu-id="1ef85-140">b.</span></span> <span data-ttu-id="1ef85-141">W hello **identyfikator URI aplikacji** pole tekstowe, typ `http://localhost`.</span><span class="sxs-lookup"><span data-stu-id="1ef85-141">In hello **App ID URI** textbox, type `http://localhost`.</span></span>
   
    <span data-ttu-id="1ef85-142">c.</span><span class="sxs-lookup"><span data-stu-id="1ef85-142">c.</span></span> <span data-ttu-id="1ef85-143">Kliknij przycisk **Complete** (Zakończ).</span><span class="sxs-lookup"><span data-stu-id="1ef85-143">Click **Complete**.</span></span>

<span data-ttu-id="1ef85-144">Możesz teraz skonfigurować aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1ef85-144">Your can now configure your application.</span></span>

![Tworzenie aplikacji](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_07.png)

## <a name="grant-your-application-permission-toouse-hello-api"></a><span data-ttu-id="1ef85-146">Przyznaj hello toouse uprawnień z aplikacji interfejsu API</span><span class="sxs-lookup"><span data-stu-id="1ef85-146">Grant your application permission toouse hello API</span></span>
1. <span data-ttu-id="1ef85-147">Na stronie aplikacji hello menu u góry hello kliknij **Konfiguruj**.</span><span class="sxs-lookup"><span data-stu-id="1ef85-147">On your application's page, in hello menu on hello top, click **Configure**.</span></span> 
   
    ![Tworzenie aplikacji](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_08.png)
2. <span data-ttu-id="1ef85-149">W hello **uprawnienia aplikacji tooother** kliknij **Dodaj aplikację**.</span><span class="sxs-lookup"><span data-stu-id="1ef85-149">In hello **permissions tooother applications** section, click **Add application**.</span></span>
   
    ![Tworzenie aplikacji](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_09.png)
3. <span data-ttu-id="1ef85-151">Na powitania **uprawnienia aplikacji tooother** okna dialogowego, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="1ef85-151">On hello **permissions tooother applications** dialog, perform hello following steps:</span></span>
   
    ![Tworzenie aplikacji](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_10.png)
   
    <span data-ttu-id="1ef85-153">a.</span><span class="sxs-lookup"><span data-stu-id="1ef85-153">a.</span></span> <span data-ttu-id="1ef85-154">Wybierz **Microsoft Graph**.</span><span class="sxs-lookup"><span data-stu-id="1ef85-154">Select **Microsoft Graph**.</span></span>
   
    <span data-ttu-id="1ef85-155">b.</span><span class="sxs-lookup"><span data-stu-id="1ef85-155">b.</span></span> <span data-ttu-id="1ef85-156">Kliknij przycisk **Complete** (Zakończ).</span><span class="sxs-lookup"><span data-stu-id="1ef85-156">Click **Complete**.</span></span>
4. <span data-ttu-id="1ef85-157">Kliknij przycisk **uprawnienia aplikacji: 0**, a następnie wybierz **odczytać wszystkie informacje dotyczące zdarzenia ryzyka tożsamości**.</span><span class="sxs-lookup"><span data-stu-id="1ef85-157">Click **Application Permissions: 0**, and then select **Read all identity risk event information**.</span></span>
   
    ![Tworzenie aplikacji](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_11.png)
5. <span data-ttu-id="1ef85-159">Kliknij przycisk **zapisać** u dołu hello hello strony.</span><span class="sxs-lookup"><span data-stu-id="1ef85-159">Click **Save** at hello bottom of hello page.</span></span>
   
    ![Tworzenie aplikacji](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_12.png)

## <a name="get-an-access-key"></a><span data-ttu-id="1ef85-161">Uzyskiwanie klucza dostępu</span><span class="sxs-lookup"><span data-stu-id="1ef85-161">Get an access key</span></span>
1. <span data-ttu-id="1ef85-162">Na stronie aplikacji hello **klucze** wybierz 1 rok jako czas trwania.</span><span class="sxs-lookup"><span data-stu-id="1ef85-162">On your application's page, in hello **keys** section, select 1 year as duration.</span></span>
   
    ![Tworzenie aplikacji](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_13.png)
2. <span data-ttu-id="1ef85-164">Kliknij przycisk **zapisać** u dołu hello hello strony.</span><span class="sxs-lookup"><span data-stu-id="1ef85-164">Click **Save** at hello bottom of hello page.</span></span>
   
    ![Tworzenie aplikacji](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_12.png)
3. <span data-ttu-id="1ef85-166">w sekcji klucze hello skopiuj wartość hello nowo utworzony klucz i wklej go w bezpiecznym miejscu.</span><span class="sxs-lookup"><span data-stu-id="1ef85-166">in hello keys section, copy hello value of your newly created key, and then paste it into a safe location.</span></span>
   
    ![Tworzenie aplikacji](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_14.png)
   
   > [!NOTE]
   > <span data-ttu-id="1ef85-168">W przypadku utraty tego klucza, będzie zawierać sekcję toothis tooreturn i Utwórz nowy klucz.</span><span class="sxs-lookup"><span data-stu-id="1ef85-168">If you lose this key, you will have tooreturn toothis section and create a new key.</span></span> <span data-ttu-id="1ef85-169">Zachowaj ten klucz tajny: każdy użytkownik, który można uzyskać dostęp do danych.</span><span class="sxs-lookup"><span data-stu-id="1ef85-169">Keep this key a secret: anyone who has it can access your data.</span></span>
   > 
   > 
4. <span data-ttu-id="1ef85-170">W hello **właściwości** hello kopiowania, sekcji **identyfikator klienta**, a następnie wklej go w bezpiecznym miejscu.</span><span class="sxs-lookup"><span data-stu-id="1ef85-170">In hello **properties** section, copy hello **Client ID**, and then paste it into a safe location.</span></span> 

## <a name="authenticate-toomicrosoft-graph-and-query-hello-identity-risk-events-api"></a><span data-ttu-id="1ef85-171">Uwierzytelnianie tooMicrosoft wykres i hello zapytania interfejsu API zdarzenia ryzyka tożsamości</span><span class="sxs-lookup"><span data-stu-id="1ef85-171">Authenticate tooMicrosoft Graph and query hello Identity Risk Events API</span></span>
<span data-ttu-id="1ef85-172">W tym momencie powinny mieć:</span><span class="sxs-lookup"><span data-stu-id="1ef85-172">At this point, you should have:</span></span>

* <span data-ttu-id="1ef85-173">Identyfikator klienta Hello skopiowane powyżej</span><span class="sxs-lookup"><span data-stu-id="1ef85-173">hello client ID you copied above</span></span>
* <span data-ttu-id="1ef85-174">klucz Hello, skopiowane powyżej</span><span class="sxs-lookup"><span data-stu-id="1ef85-174">hello key you copied above</span></span>
* <span data-ttu-id="1ef85-175">Witaj nazwy domeny Twojej dzierżawy</span><span class="sxs-lookup"><span data-stu-id="1ef85-175">hello name of your tenant's domain</span></span>

<span data-ttu-id="1ef85-176">tooauthenticate, wysyłania post żądania zbyt`https://login.microsoft.com` z następujących parametrów w treści hello hello:</span><span class="sxs-lookup"><span data-stu-id="1ef85-176">tooauthenticate, send a post request too`https://login.microsoft.com` with hello following parameters in hello body:</span></span>

* <span data-ttu-id="1ef85-177">Typ grant_type: "**client_credentials**"</span><span class="sxs-lookup"><span data-stu-id="1ef85-177">grant_type: “**client_credentials**”</span></span>
* <span data-ttu-id="1ef85-178">Zasób: "**https://graph.microsoft.com**"</span><span class="sxs-lookup"><span data-stu-id="1ef85-178">resource: “**https://graph.microsoft.com**”</span></span>
* <span data-ttu-id="1ef85-179">client_id:<your client ID></span><span class="sxs-lookup"><span data-stu-id="1ef85-179">client_id: <your client ID></span></span>
* <span data-ttu-id="1ef85-180">client_secret:<your key></span><span class="sxs-lookup"><span data-stu-id="1ef85-180">client_secret: <your key></span></span>

> [!NOTE]
> <span data-ttu-id="1ef85-181">Wymagane wartości tooprovide dla hello **client_id** i hello **client_secret** parametru.</span><span class="sxs-lookup"><span data-stu-id="1ef85-181">You need tooprovide values for hello **client_id** and hello **client_secret** parameter.</span></span>
> 
> 

<span data-ttu-id="1ef85-182">Jeśli to się powiedzie, to zwraca token uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="1ef85-182">If successful, this returns an authentication token.</span></span>  
<span data-ttu-id="1ef85-183">Witaj toocall interfejsu API, Utwórz nagłówek z hello następującego parametru:</span><span class="sxs-lookup"><span data-stu-id="1ef85-183">toocall hello API, create a header with hello following parameter:</span></span>

    `Authorization`=”<token_type> <access_token>"


<span data-ttu-id="1ef85-184">Podczas uwierzytelniania, można znaleźć typu tokenu hello i token dostępu w hello zwrócił token.</span><span class="sxs-lookup"><span data-stu-id="1ef85-184">When authenticating, you can find hello token type and access token in hello returned token.</span></span>

<span data-ttu-id="1ef85-185">Wyślij ten nagłówek jako toohello żądania, po adresem URL interfejsu API:`https://graph.microsoft.com/beta/identityRiskEvents`</span><span class="sxs-lookup"><span data-stu-id="1ef85-185">Send this header as a request toohello following API URL: `https://graph.microsoft.com/beta/identityRiskEvents`</span></span>

<span data-ttu-id="1ef85-186">odpowiedź Hello w przypadku powodzenia jest kolekcją tożsamości zdarzenia o podwyższonym ryzyku i skojarzone dane w formacie OData JSON, który może być analizowana i obsługiwane zgodnie z własnymi potrzebami hello.</span><span class="sxs-lookup"><span data-stu-id="1ef85-186">hello response, if successful, is a collection of identity risk events and associated data in hello OData JSON format, which can be parsed and handled as see fit.</span></span>

<span data-ttu-id="1ef85-187">Oto przykładowy kod do uwierzytelniania i wywoływanie interfejsu API hello przy użyciu programu Powershell.</span><span class="sxs-lookup"><span data-stu-id="1ef85-187">Here’s sample code for authenticating and calling hello API using Powershell.</span></span>  
<span data-ttu-id="1ef85-188">Wystarczy dodać Identyfikatora klienta, a dla klucza dzierżawy domeny.</span><span class="sxs-lookup"><span data-stu-id="1ef85-188">Just add your client ID, key, and tenant domain.</span></span>

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


## <a name="next-steps"></a><span data-ttu-id="1ef85-189">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="1ef85-189">Next steps</span></span>
<span data-ttu-id="1ef85-190">Gratulacje, właśnie utworzony pierwszy tooMicrosoft wywołania wykresu!</span><span class="sxs-lookup"><span data-stu-id="1ef85-190">Congratulations, you just made your first call tooMicrosoft Graph!</span></span>  
<span data-ttu-id="1ef85-191">Teraz można zbadać zdarzenia o podwyższonym ryzyku tożsamości i użyć hello danych, jednak użytkownik mieści się w temacie.</span><span class="sxs-lookup"><span data-stu-id="1ef85-191">Now you can query identity risk events and use hello data however you see fit.</span></span>

<span data-ttu-id="1ef85-192">toolearn więcej informacji na temat programu Microsoft Graph i jak toobuild aplikacji przy użyciu hello interfejsu API programu Graph, zobacz hello [dokumentacji](https://graph.microsoft.io/docs) i znacznie więcej informacji na temat hello [witryny Microsoft Graph](https://graph.microsoft.io/).</span><span class="sxs-lookup"><span data-stu-id="1ef85-192">toolearn more about Microsoft Graph and how toobuild applications using hello Graph API, check out hello [documentation](https://graph.microsoft.io/docs) and much more on hello [Microsoft Graph site](https://graph.microsoft.io/).</span></span> <span data-ttu-id="1ef85-193">Ponadto upewnij się, że hello toobookmark [Azure AD Identity Protection API](https://graph.microsoft.io/docs/api-reference/beta/resources/identityprotection_root) strony, która zawiera listę wszystkich hello tożsamości ochrony interfejsami API dostępnymi w wykresie.</span><span class="sxs-lookup"><span data-stu-id="1ef85-193">Also, make sure toobookmark hello [Azure AD Identity Protection API](https://graph.microsoft.io/docs/api-reference/beta/resources/identityprotection_root) page that lists all of hello Identity Protection APIs available in Graph.</span></span> <span data-ttu-id="1ef85-194">Jak możemy dodać nowe sposoby toowork z ochrony tożsamości za pomocą interfejsu API, zobaczysz je na tej stronie.</span><span class="sxs-lookup"><span data-stu-id="1ef85-194">As we add new ways toowork with Identity Protection via API, you’ll see them on that page.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1ef85-195">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="1ef85-195">Additional resources</span></span>
* [<span data-ttu-id="1ef85-196">Ochronę tożsamości usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1ef85-196">Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection.md)
* [<span data-ttu-id="1ef85-197">Rodzaje zdarzeń o podwyższonym ryzyku wykrywanych przez Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="1ef85-197">Types of risk events detected by Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection-risk-events-types.md)
* [<span data-ttu-id="1ef85-198">Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="1ef85-198">Microsoft Graph</span></span>](https://graph.microsoft.io/)
* [<span data-ttu-id="1ef85-199">Omówienie programu Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="1ef85-199">Overview of Microsoft Graph</span></span>](https://graph.microsoft.io/docs)
* [<span data-ttu-id="1ef85-200">Katalogu głównego usługi programu Azure AD Identity Protection</span><span class="sxs-lookup"><span data-stu-id="1ef85-200">Azure AD Identity Protection Service Root</span></span>](https://graph.microsoft.io/docs/api-reference/beta/resources/identityprotection_root)

