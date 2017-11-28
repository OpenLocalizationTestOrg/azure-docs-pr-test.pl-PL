---
title: "przy użyciu protokołu OAuth 2.0 w usłudze Azure API Management konta dewelopera aaaAuthorize | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak użytkownicy tooauthorize w usłudze API Management przy użyciu protokołu OAuth 2.0."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 78c48247-64f0-4708-b2d0-98b61a821283
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: 934901dd6df399470a3257bf7a3a9b9fb5f40d5e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooauthorize-developer-accounts-using-oauth-20-in-azure-api-management"></a><span data-ttu-id="16ae4-103">Jak kont przy użyciu narzędzia Projektant tooauthorize OAuth 2.0 w usłudze Azure API Management</span><span class="sxs-lookup"><span data-stu-id="16ae4-103">How tooauthorize developer accounts using OAuth 2.0 in Azure API Management</span></span>
<span data-ttu-id="16ae4-104">Obsługuje wiele interfejsów API [OAuth 2.0](http://oauth.net/2/) toosecure hello interfejsu API i upewnij się, że tylko prawidłowe użytkownicy mają dostęp, i ich tylko dostęp do zasobów toowhich one są uprawnione.</span><span class="sxs-lookup"><span data-stu-id="16ae4-104">Many APIs support [OAuth 2.0](http://oauth.net/2/) toosecure hello API and ensure that only valid users have access, and they can only access resources toowhich they're entitled.</span></span> <span data-ttu-id="16ae4-105">W kolejności toouse Azure API Management w interakcyjne konsoli dewelopera z tych interfejsów API usługi hello pozwala tooconfigure Twojego toowork wystąpienia usługi z Twojej OAuth 2.0 włączone interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="16ae4-105">In order toouse Azure API Management's interactive Developer Console with such APIs, hello service allows you tooconfigure your service instance toowork with your OAuth 2.0 enabled API.</span></span>

## <span data-ttu-id="16ae4-106"><a name="prerequisites"></a>Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="16ae4-106"><a name="prerequisites"> </a>Prerequisites</span></span>
<span data-ttu-id="16ae4-107">W tym przewodniku przedstawiono sposób tooconfigure Twojego toouse wystąpienia usługi Zarządzanie interfejsami API autoryzacji OAuth 2.0 dla deweloperów kont, ale nie są wyświetlane jak dostawca tooconfigure OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="16ae4-107">This guide shows you how tooconfigure your API Management service instance toouse OAuth 2.0 authorization for developer accounts, but does not show you how tooconfigure an OAuth 2.0 provider.</span></span> <span data-ttu-id="16ae4-108">Witaj konfiguracji dla każdego protokołu OAuth 2.0 dostawcy jest inny, mimo że hello kroki są podobne, a hello wymagane informacje używane do konfigurowania protokołu OAuth 2.0 w wystąpieniu usługi API Management jest hello takie same.</span><span class="sxs-lookup"><span data-stu-id="16ae4-108">hello configuration for each OAuth 2.0 provider is different, although hello steps are similar, and hello required pieces of information used in configuring OAuth 2.0 in your API Management service instance are hello same.</span></span> <span data-ttu-id="16ae4-109">W tym temacie przedstawiono przykłady użycia usługi Azure Active Directory jako dostawcy uwierzytelniania OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="16ae4-109">This topic shows examples using Azure Active Directory as an OAuth 2.0 provider.</span></span>

> [!NOTE]
> <span data-ttu-id="16ae4-110">Aby uzyskać więcej informacji na temat konfigurowania uwierzytelniania OAuth 2.0 przy użyciu usługi Azure Active Directory, zobacz hello [aplikacji sieci Web-GraphAPI-DotNet] [ WebApp-GraphAPI-DotNet] próbki.</span><span class="sxs-lookup"><span data-stu-id="16ae4-110">For more information on configuring OAuth 2.0 using Azure Active Directory, see hello [WebApp-GraphAPI-DotNet][WebApp-GraphAPI-DotNet] sample.</span></span>
> 
> 

## <span data-ttu-id="16ae4-111"><a name="step1"></a>Skonfigurować serwer autoryzacji OAuth 2.0 w zarządzanie interfejsami API</span><span class="sxs-lookup"><span data-stu-id="16ae4-111"><a name="step1"> </a>Configure an OAuth 2.0 authorization server in API Management</span></span>
<span data-ttu-id="16ae4-112">tooget pracę, kliknij przycisk **portal wydawcy** w hello portalu Azure usługi Zarządzanie interfejsami API.</span><span class="sxs-lookup"><span data-stu-id="16ae4-112">tooget started, click **Publisher portal** in hello Azure Portal for your API Management service.</span></span>

![Portal wydawcy][api-management-management-console]

> [!NOTE]
> <span data-ttu-id="16ae4-114">Jeśli jeszcze nie utworzono wystąpienie usługi API Management, zobacz [Utwórz wystąpienie usługi Zarządzanie interfejsami API] [ Create an API Management service instance] w hello [wprowadzenie do usługi Azure API Management] [ Get started with Azure API Management] samouczka.</span><span class="sxs-lookup"><span data-stu-id="16ae4-114">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in hello [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="16ae4-115">Kliknij przycisk **zabezpieczeń** z hello **zarządzanie interfejsami API** menu po lewej stronie, kliknij hello **OAuth 2.0**, a następnie kliknij przycisk **serwera autoryzacji Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="16ae4-115">Click **Security** from hello **API Management** menu on hello left, click **OAuth 2.0**, and then click **Add authorization server**.</span></span>

![Uwierzytelnianie OAuth 2.0][api-management-oauth2]

<span data-ttu-id="16ae4-117">Po kliknięciu przycisku **serwera autoryzacji Dodaj**, zostanie wyświetlony nowy formularz serwera autoryzacji hello.</span><span class="sxs-lookup"><span data-stu-id="16ae4-117">After clicking **Add authorization server**, hello new authorization server form is displayed.</span></span>

![Nowy serwer][api-management-oauth2-server-1]

<span data-ttu-id="16ae4-119">Wprowadź nazwę i opcjonalny opis w hello **nazwa** i **opis** pola.</span><span class="sxs-lookup"><span data-stu-id="16ae4-119">Enter a name and an optional description in hello **Name** and **Description** fields.</span></span> 

> [!NOTE]
> <span data-ttu-id="16ae4-120">Te pola są używane tooidentify serwera autoryzacji hello OAuth 2.0 w ramach bieżącego wystąpienia usługi Zarządzanie interfejsami API hello i ich wartości nie pochodzą z serwera hello OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="16ae4-120">These fields are used tooidentify hello OAuth 2.0 authorization server within hello current API Management service instance and their values do not come from hello OAuth 2.0 server.</span></span>
> 
> 

<span data-ttu-id="16ae4-121">Wprowadź hello **adres URL strony rejestracji klienta**.</span><span class="sxs-lookup"><span data-stu-id="16ae4-121">Enter hello **Client registration page URL**.</span></span> <span data-ttu-id="16ae4-122">Ta strona jest, gdzie użytkownicy mogą tworzyć i zarządzać ich kont i może być różna w zależności od dostawcy hello OAuth 2.0 używane.</span><span class="sxs-lookup"><span data-stu-id="16ae4-122">This page is where users can create and manage their accounts, and varies depending on hello OAuth 2.0 provider used.</span></span> <span data-ttu-id="16ae4-123">Witaj **adres URL strony rejestracji klienta** punktów toohello strony przez użytkowników, można użyć toocreate i skonfiguruj swoje własne konta dla dostawcy OAuth 2.0, które obsługują zarządzanie kontami użytkowników.</span><span class="sxs-lookup"><span data-stu-id="16ae4-123">hello **Client registration page URL** points toohello page that users can use toocreate and configure their own accounts for OAuth 2.0 providers that support user management of accounts.</span></span> <span data-ttu-id="16ae4-124">Niektóre organizacje nie Konfiguruj lub korzystać z tej funkcji, nawet jeśli obsługuje dostawcy hello OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="16ae4-124">Some organizations do not configure or use this functionality even if hello OAuth 2.0 provider supports it.</span></span> <span data-ttu-id="16ae4-125">Jeśli dostawcy OAuth 2.0 nie zarządzania skonfigurowano kont użytkownika, wprowadź symbolu zastępczego adresu URL w tym miejscu, takie jak adres URL hello firmy, lub takie jak `https://placeholder.contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="16ae4-125">If your OAuth 2.0 provider does not have user management of accounts configured, enter a placeholder URL here such as hello URL of your company, or a URL such as `https://placeholder.contoso.com`.</span></span>

<span data-ttu-id="16ae4-126">Następna sekcja Hello hello formularza zawiera hello **typy przydziałów kod autoryzacji**, **adres URL punktu końcowego autoryzacji**, i **metoda żądania autoryzacji** ustawienia.</span><span class="sxs-lookup"><span data-stu-id="16ae4-126">hello next section of hello form contains hello **Authorization code grant types**, **Authorization endpoint URL**, and **Authorization request method** settings.</span></span>

![Nowy serwer][api-management-oauth2-server-2]

<span data-ttu-id="16ae4-128">Określ hello **typy przydziałów kod autoryzacji** sprawdzając hello żądanego typu.</span><span class="sxs-lookup"><span data-stu-id="16ae4-128">Specify hello **Authorization code grant types** by checking hello desired types.</span></span> <span data-ttu-id="16ae4-129">**Kod autoryzacji** jest określony, domyślnie.</span><span class="sxs-lookup"><span data-stu-id="16ae4-129">**Authorization code** is specified by default.</span></span>

<span data-ttu-id="16ae4-130">Wprowadź hello **adres URL punktu końcowego autoryzacji**.</span><span class="sxs-lookup"><span data-stu-id="16ae4-130">Enter hello **Authorization endpoint URL**.</span></span> <span data-ttu-id="16ae4-131">Dla usługi Azure Active Directory, ten adres URL będzie podobne toohello następującego adresu URL, gdzie `<client_id>` jest zastępowany hello identyfikatora klienta, który identyfikuje serwer aplikacji toohello OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="16ae4-131">For Azure Active Directory, this URL will be similar toohello following URL, where `<client_id>` is replaced with hello client id that identifies your application toohello OAuth 2.0 server.</span></span>

`https://login.microsoftonline.com/<client_id>/oauth2/authorize`

<span data-ttu-id="16ae4-132">Witaj **metoda żądania autoryzacji** określa sposób przesyłania żądania autoryzacji powitania serwera toohello OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="16ae4-132">hello **Authorization request method** specifies how hello authorization request is sent toohello OAuth 2.0 server.</span></span> <span data-ttu-id="16ae4-133">Domyślnie **UZYSKAĆ** jest zaznaczone.</span><span class="sxs-lookup"><span data-stu-id="16ae4-133">By default **GET** is selected.</span></span>

<span data-ttu-id="16ae4-134">Następna sekcja Hello jest gdzie hello **tokenu końcowego adresu URL**, **metody uwierzytelniania klienta**, **token dostępu wysyłania — metoda**, i **zakresudomyślnego** zostały określone.</span><span class="sxs-lookup"><span data-stu-id="16ae4-134">hello next section is where hello **Token endpoint URL**, **Client authentication methods**, **Access token sending method**, and **Default scope** are specified.</span></span>

![Nowy serwer][api-management-oauth2-server-3]

<span data-ttu-id="16ae4-136">W przypadku serwera usługi Azure Active Directory OAuth 2.0 hello **tokenu końcowego adresu URL** będą miały hello zgodny z formatem, gdzie `<APPID>` ma hello format `yourapp.onmicrosoft.com`.</span><span class="sxs-lookup"><span data-stu-id="16ae4-136">For an Azure Active Directory OAuth 2.0 server, hello **Token endpoint URL** will have hello following format, where `<APPID>`  has hello format of `yourapp.onmicrosoft.com`.</span></span>

`https://login.microsoftonline.com/<APPID>/oauth2/token`

<span data-ttu-id="16ae4-137">Hello domyślne ustawienie dla **metody uwierzytelniania klienta** jest **podstawowe**, i **token dostępu metody wysyłania** jest **nagłówek autoryzacji**.</span><span class="sxs-lookup"><span data-stu-id="16ae4-137">hello default setting for **Client authentication methods** is **Basic**, and  **Access token sending method** is **Authorization header**.</span></span> <span data-ttu-id="16ae4-138">Te wartości są skonfigurowane w tej sekcji formularza hello, wraz z hello **zakresu domyślnego**.</span><span class="sxs-lookup"><span data-stu-id="16ae4-138">These values are configured on this section of hello form, along with hello **Default scope**.</span></span>

<span data-ttu-id="16ae4-139">Witaj **poświadczeń klienta** sekcja zawiera hello **identyfikator klienta** i **klucz tajny klienta**, które są uzyskiwane podczas procesu tworzenia i konfiguracji hello użytkownika OAuth 2.0 serwer.</span><span class="sxs-lookup"><span data-stu-id="16ae4-139">hello **Client credentials** section contains hello **Client ID** and **Client secret**, which are obtained during hello creation and configuration process of your OAuth 2.0 server.</span></span> <span data-ttu-id="16ae4-140">Raz hello **identyfikator klienta** i **klucz tajny klienta** są określone, hello **redirect_uri** dla hello **kod autoryzacji** jest generowany.</span><span class="sxs-lookup"><span data-stu-id="16ae4-140">Once hello **Client ID** and **Client secret** are specified, hello **redirect_uri** for hello **authorization code** is generated.</span></span> <span data-ttu-id="16ae4-141">Ten identyfikator URI jest adres URL odpowiedzi hello tooconfigure używane w konfiguracji serwera OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="16ae4-141">This URI is used tooconfigure hello reply URL in your OAuth 2.0 server configuration.</span></span>

![Nowy serwer][api-management-oauth2-server-4]

<span data-ttu-id="16ae4-143">Jeśli **typy przydziałów kod autoryzacji** ustawiono zbyt**hasło właściciela zasobów**, hello **poświadczenia hasła właściciela zasobu** sekcja jest używane toospecify te poświadczenia; w przeciwnym razie można pozostawić on pusty.</span><span class="sxs-lookup"><span data-stu-id="16ae4-143">If **Authorization code grant types** is set too**Resource owner password**, hello **Resource owner password credentials** section is used toospecify those credentials; otherwise you can leave it blank.</span></span>

![Nowy serwer][api-management-oauth2-server-5]

<span data-ttu-id="16ae4-145">Po zakończeniu formularza powitania kliknij **zapisać** toosave hello interfejsu API zarządzania OAuth 2.0 autoryzacji serwera konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="16ae4-145">Once hello form is complete, click **Save** toosave hello API Management OAuth 2.0 authorization server configuration.</span></span> <span data-ttu-id="16ae4-146">Po zapisaniu hello konfiguracji serwera można skonfigurować toouse interfejsów API tej konfiguracji, jak pokazano w następnej sekcji hello.</span><span class="sxs-lookup"><span data-stu-id="16ae4-146">Once hello server configuration is saved, you can configure APIs toouse this configuration, as shown in hello next section.</span></span>

## <span data-ttu-id="16ae4-147"><a name="step2"></a>Skonfigurować toouse interfejsu API autoryzacji użytkownika OAuth 2.0</span><span class="sxs-lookup"><span data-stu-id="16ae4-147"><a name="step2"> </a>Configure an API toouse OAuth 2.0 user authorization</span></span>
<span data-ttu-id="16ae4-148">Kliknij przycisk **interfejsów API** z hello **zarządzanie interfejsami API** menu na powitania po lewej, kliknij nazwę hello hello żądanego interfejsu API, kliknij przycisk **zabezpieczeń**, a następnie sprawdź pole hello **OAuth 2.0**.</span><span class="sxs-lookup"><span data-stu-id="16ae4-148">Click **APIs** from hello **API Management** menu on hello left, click hello name of hello desired API, click **Security**, and then check hello box for **OAuth 2.0**.</span></span>

![Uwierzytelnianie użytkownika][api-management-user-authorization]

<span data-ttu-id="16ae4-150">Wybierz hello potrzeby **serwera autoryzacji** z listy rozwijanej hello, a następnie kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="16ae4-150">Select hello desired **Authorization server** from hello drop-down list, and click **Save**.</span></span>

![Uwierzytelnianie użytkownika][api-management-user-authorization-save]

## <span data-ttu-id="16ae4-152"><a name="step3"></a>Testowanie autoryzacji użytkownika hello OAuth 2.0 w hello portalu dla deweloperów</span><span class="sxs-lookup"><span data-stu-id="16ae4-152"><a name="step3"> </a>Test hello OAuth 2.0 user authorization in hello Developer Portal</span></span>
<span data-ttu-id="16ae4-153">Po skonfigurowaniu serwera autoryzacji OAuth 2.0 i skonfigurowana z toouse interfejsu API serwera, przetestować go, przechodząc toohello portalu dla deweloperów i wywoływanie interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="16ae4-153">Once you have configured your OAuth 2.0 authorization server and configured your API toouse that server, you can test it by going toohello Developer Portal and calling an API.</span></span>  <span data-ttu-id="16ae4-154">Kliknij przycisk **portalu dla deweloperów** w menu u góry prawo hello.</span><span class="sxs-lookup"><span data-stu-id="16ae4-154">Click **Developer portal** in hello top right menu.</span></span>

![Portal dla deweloperów][api-management-developer-portal-menu]

<span data-ttu-id="16ae4-156">Kliknij przycisk **interfejsów API** w menu u góry hello i wybierz **Echo API**.</span><span class="sxs-lookup"><span data-stu-id="16ae4-156">Click **APIs** in hello top menu and select **Echo API**.</span></span>

![Interfejs Echo API][api-management-apis-echo-api]

> [!NOTE]
> <span data-ttu-id="16ae4-158">Jeśli masz tylko jeden interfejs API skonfigurowane lub tooyour widoczne konta, klikając interfejsów API przejście bezpośrednio toohello operacji dla tego interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="16ae4-158">If you have only one API configured or visible tooyour account, then clicking APIs takes you directly toohello operations for that API.</span></span>
> 
> 

<span data-ttu-id="16ae4-159">Wybierz hello **UZYSKAĆ zasobu** operacji, kliknij przycisk **Otwórz konsolę**, a następnie wybierz **kod autoryzacji** z listy rozwijanej hello.</span><span class="sxs-lookup"><span data-stu-id="16ae4-159">Select hello **GET Resource** operation, click **Open Console**, and then select **Authorization code** from hello drop-down.</span></span>

![Otwarta konsola][api-management-open-console]

<span data-ttu-id="16ae4-161">Gdy **kod autoryzacji** jest zaznaczona, wyskakujące okienko zostanie wyświetlony z hello logowania w formie dostawcy hello OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="16ae4-161">When **Authorization code** is selected, a pop-up window is displayed with hello sign-in form of hello OAuth 2.0 provider.</span></span> <span data-ttu-id="16ae4-162">W tym przykładzie hello logowania w formularzu są udostępniane przez usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="16ae4-162">In this example hello sign-in form is provided by Azure Active Directory.</span></span>

> [!NOTE]
> <span data-ttu-id="16ae4-163">Jeśli masz wyskakujące okienka wyłączone, będzie monitowany tooenable ich hello przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="16ae4-163">If you have pop-ups disabled you will be prompted tooenable them by hello browser.</span></span> <span data-ttu-id="16ae4-164">Po włączeniu je wybrać **kod autoryzacji** ponownie i hello formularz logowania będzie wyświetlany.</span><span class="sxs-lookup"><span data-stu-id="16ae4-164">After you enable them, select **Authorization code** again and hello sign-in form will be displayed.</span></span>
> 
> 

![Logowanie][api-management-oauth2-signin]

<span data-ttu-id="16ae4-166">Po zalogowaniu się hello **nagłówki żądań** są wypełniane przy użyciu `Authorization : Bearer` autoryzuje żądanie hello nagłówek.</span><span class="sxs-lookup"><span data-stu-id="16ae4-166">Once you have signed in, hello **Request headers** are populated with an `Authorization : Bearer` header that authorizes hello request.</span></span>

![Token nagłówka żądania][api-management-request-header-token]

<span data-ttu-id="16ae4-168">W tym momencie możesz skonfigurować wartości hello potrzeby hello pozostałe parametry i przesłać Żądanie hello.</span><span class="sxs-lookup"><span data-stu-id="16ae4-168">At this point you can configure hello desired values for hello remaining parameters, and submit hello request.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="16ae4-169">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="16ae4-169">Next steps</span></span>
<span data-ttu-id="16ae4-170">Aby uzyskać więcej informacji na temat korzystania z protokołu OAuth 2.0 i zarządzanie interfejsami API, zobacz następujące hello wideo i towarzyszące [artykułu](api-management-howto-protect-backend-with-aad.md).</span><span class="sxs-lookup"><span data-stu-id="16ae4-170">For more information about using OAuth 2.0 and API Management, see hello following video and accompanying [article](api-management-howto-protect-backend-with-aad.md).</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Protecting-Web-API-Backend-with-Azure-Active-Directory-and-API-Management/player]
> 
> 

[api-management-management-console]: ./media/api-management-howto-oauth2/api-management-management-console.png
[api-management-oauth2]: ./media/api-management-howto-oauth2/api-management-oauth2.png
[api-management-user-authorization]: ./media/api-management-howto-oauth2/api-management-user-authorization.png
[api-management-user-authorization-save]: ./media/api-management-howto-oauth2/api-management-user-authorization-save.png
[api-management-oauth2-signin]: ./media/api-management-howto-oauth2/api-management-oauth2-signin.png
[api-management-request-header-token]: ./media/api-management-howto-oauth2/api-management-request-header-token.png
[api-management-developer-portal-menu]: ./media/api-management-howto-oauth2/api-management-developer-portal-menu.png
[api-management-open-console]: ./media/api-management-howto-oauth2/api-management-open-console.png
[api-management-oauth2-server-1]: ./media/api-management-howto-oauth2/api-management-oauth2-server-1.png
[api-management-oauth2-server-2]: ./media/api-management-howto-oauth2/api-management-oauth2-server-2.png
[api-management-oauth2-server-3]: ./media/api-management-howto-oauth2/api-management-oauth2-server-3.png
[api-management-oauth2-server-4]: ./media/api-management-howto-oauth2/api-management-oauth2-server-4.png
[api-management-oauth2-server-5]: ./media/api-management-howto-oauth2/api-management-oauth2-server-5.png
[api-management-apis-echo-api]: ./media/api-management-howto-oauth2/api-management-apis-echo-api.png


[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How tooadd and publish a product]: api-management-howto-add-products.md
[Monitoring and analytics]: api-management-monitoring.md
[Add APIs tooa product]: api-management-howto-add-products.md#add-apis
[Publish a product]: api-management-howto-add-products.md#publish-product
[Get started with Azure API Management]: api-management-get-started.md
[API Management policy reference]: api-management-policy-reference.md
[Caching policies]: api-management-policy-reference.md#caching-policies
[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[http://oauth.net/2/]: http://oauth.net/2/
[WebApp-GraphAPI-DotNet]: https://github.com/AzureADSamples/WebApp-GraphAPI-DotNet

[Prerequisites]: #prerequisites
[Configure an OAuth 2.0 authorization server in API Management]: #step1
[Configure an API toouse OAuth 2.0 user authorization]: #step2
[Test hello OAuth 2.0 user authorization in hello Developer Portal]: #step3
[Next steps]: #next-steps

