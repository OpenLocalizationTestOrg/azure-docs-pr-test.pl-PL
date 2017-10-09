---
title: "za pomocą usługi Azure Active Directory — Zarządzanie interfejsami API Azure konta dewelopera aaaAuthorize | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak użytkownicy tooauthorize przy użyciu usługi Azure Active Directory w usłudze API Management."
services: api-management
documentationcenter: API Management
author: steved0x
manager: erikre
editor: 
ms.assetid: 33a69a83-94f2-4e4e-9cef-f2a5af3c9732
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: ebf5447a509a47df35e4262138bfcf423cb1dd5c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooauthorize-developer-accounts-using-azure-active-directory-in-azure-api-management"></a><span data-ttu-id="62023-103">Jak tooauthorize developer kont przy użyciu narzędzia Azure Active Directory w usłudze Azure API Management</span><span class="sxs-lookup"><span data-stu-id="62023-103">How tooauthorize developer accounts using Azure Active Directory in Azure API Management</span></span>
## <a name="overview"></a><span data-ttu-id="62023-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="62023-104">Overview</span></span>
<span data-ttu-id="62023-105">Ten przewodnik przedstawia, jak tooenable uzyskują dostęp do portalu dla deweloperów toohello dla użytkowników z usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="62023-105">This guide shows you how tooenable access toohello developer portal for users from Azure Active Directory.</span></span> <span data-ttu-id="62023-106">W tym przewodniku także przedstawiono sposób toomanage grupy użytkowników usługi Azure Active Directory przez dodanie zewnętrznego grup, które zawierają hello użytkowników usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="62023-106">This guide also shows you how toomanage groups of Azure Active Directory users by adding external groups that contain hello users of an Azure Active Directory.</span></span>

> <span data-ttu-id="62023-107">Witaj toocomplete kroków w tym przewodniku musi działać usługa Azure Active Directory w których toocreate aplikacji.</span><span class="sxs-lookup"><span data-stu-id="62023-107">toocomplete hello steps in this guide you must first have an Azure Active Directory in which toocreate an application.</span></span>
> 
> 

## <a name="how-tooauthorize-developer-accounts-using-azure-active-directory"></a><span data-ttu-id="62023-108">Jak tooauthorize developer kont przy użyciu narzędzia Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="62023-108">How tooauthorize developer accounts using Azure Active Directory</span></span>
<span data-ttu-id="62023-109">tooget pracę, kliknij przycisk **portal wydawcy** w portalu Azure usługi Zarządzanie interfejsami API hello.</span><span class="sxs-lookup"><span data-stu-id="62023-109">tooget started, click **Publisher portal** in hello Azure portal for your API Management service.</span></span> <span data-ttu-id="62023-110">Trwa toohello zarządzanie interfejsami API wydawcy portalu.</span><span class="sxs-lookup"><span data-stu-id="62023-110">This takes you toohello API Management publisher portal.</span></span>

![Portal wydawcy][api-management-management-console]

> <span data-ttu-id="62023-112">Jeśli jeszcze nie utworzono wystąpienie usługi API Management, zobacz [Utwórz wystąpienie usługi Zarządzanie interfejsami API] [ Create an API Management service instance] w hello [wprowadzenie do usługi Azure API Management] [ Get started with Azure API Management] samouczka.</span><span class="sxs-lookup"><span data-stu-id="62023-112">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in hello [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="62023-113">Kliknij przycisk **zabezpieczeń** z hello **zarządzanie interfejsami API** menu po lewej stronie powitania oraz kliknij **tożsamości zewnętrznych**.</span><span class="sxs-lookup"><span data-stu-id="62023-113">Click **Security** from hello **API Management** menu on hello left and click **External Identities**.</span></span>

![Tożsamości zewnętrznych][api-management-security-external-identities]

<span data-ttu-id="62023-115">Kliknij przycisk **usługi Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="62023-115">Click **Azure Active Directory**.</span></span> <span data-ttu-id="62023-116">Zanotuj hello **adresem URL przekierowania** i przełączyć na tooyour usługi Azure Active Directory w hello klasycznego portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="62023-116">Make a note of hello **Redirect URL** and switch over tooyour Azure Active Directory in hello Azure Classic Portal.</span></span>

![Tożsamości zewnętrznych][api-management-security-aad-new]

<span data-ttu-id="62023-118">Kliknij przycisk hello **Dodaj** przycisk toocreate nową aplikację usługi Azure Active Directory, a następnie wybierz pozycję **Dodaj aplikację moją organizację**.</span><span class="sxs-lookup"><span data-stu-id="62023-118">Click hello **Add** button toocreate a new Azure Active Directory application, and choose **Add an application my organization is developing**.</span></span>

![Dodaj nową aplikację usługi Azure Active Directory][api-management-new-aad-application-menu]

<span data-ttu-id="62023-120">Wprowadź nazwę aplikacji hello, wybierz pozycję **sieci Web, aplikacji i/lub interfejs API sieci Web**i kliknij przycisk Dalej hello.</span><span class="sxs-lookup"><span data-stu-id="62023-120">Enter a name for hello application, select **Web application and/or Web API**, and click hello next button.</span></span>

![Nową aplikację usługi Azure Active Directory][api-management-new-aad-application-1]

<span data-ttu-id="62023-122">Aby uzyskać **adres URL logowania**, wprowadź hello jednokrotnej adres URL swojego portalu dla deweloperów.</span><span class="sxs-lookup"><span data-stu-id="62023-122">For **Sign-on URL**, enter hello sign-on URL of your developer portal.</span></span> <span data-ttu-id="62023-123">W tym przykładzie hello **adres URL logowania** jest `https://aad03.portal.current.int-azure-api.net/signin`.</span><span class="sxs-lookup"><span data-stu-id="62023-123">In this example, hello **Sign-on URL** is `https://aad03.portal.current.int-azure-api.net/signin`.</span></span> 

<span data-ttu-id="62023-124">Dla hello **adres URL Identyfikatora aplikacji**, wprowadź hello domyślnej domeny i domeny niestandardowej dla hello Azure Active Directory i Dołącz tooit unikatowy ciąg.</span><span class="sxs-lookup"><span data-stu-id="62023-124">For hello **App ID URL**, enter either hello default domain or a custom domain for hello Azure Active Directory, and append a unique string tooit.</span></span> <span data-ttu-id="62023-125">W tym przykładzie hello domyślnej domeny **https://contoso5api.onmicrosoft.com** jest używana z sufiksem hello **/api** określony.</span><span class="sxs-lookup"><span data-stu-id="62023-125">In this example, hello default domain of **https://contoso5api.onmicrosoft.com** is used with hello suffix of **/api** specified.</span></span>

![Nowe właściwości aplikacji usługi Azure Active Directory][api-management-new-aad-application-2]

<span data-ttu-id="62023-127">Kliknij toosave przycisk wyboru hello i tworzenie aplikacji hello i przełączyć toohello **Konfiguruj** karcie tooconfigure hello nowej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="62023-127">Click hello check button toosave and create hello application, and switch toohello **Configure** tab tooconfigure hello new application.</span></span>

![Nowej aplikacji usługi Azure Active Directory][api-management-new-aad-app-created]

<span data-ttu-id="62023-129">Jeśli wiele katalogów Active Azure będą toobe używany dla tej aplikacji, kliknij przycisk **tak** dla **aplikacji jest wielodostępne**.</span><span class="sxs-lookup"><span data-stu-id="62023-129">If multiple Azure Active Directories are going toobe used for this application, click **Yes** for **Application is multi-tenant**.</span></span> <span data-ttu-id="62023-130">Domyślnie Hello **nr**.</span><span class="sxs-lookup"><span data-stu-id="62023-130">hello default is **No**.</span></span>

![Aplikacja jest wieloma dzierżawcami][api-management-aad-app-multi-tenant]

<span data-ttu-id="62023-132">Kopiuj hello **adresem URL przekierowania** z hello **usługi Azure Active Directory** sekcji hello **tożsamości zewnętrznych** w portalu wydawcy hello i wklej go do hello **Adres URL odpowiedzi** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="62023-132">Copy hello **Redirect URL** from hello **Azure Active Directory** section of hello **External Identities** tab in hello publisher portal and paste it into hello **Reply URL** text box.</span></span> 

![Adres URL odpowiedzi][api-management-aad-reply-url]

<span data-ttu-id="62023-134">Przewiń w dół toohello hello skonfigurować kartę, zaznacz hello **uprawnienia aplikacji** listy rozwijanej i sprawdź **odczytuj dane katalogu**.</span><span class="sxs-lookup"><span data-stu-id="62023-134">Scroll toohello bottom of hello configure tab, select hello **Application Permissions** drop-down, and check **Read directory data**.</span></span>

![Uprawnienia aplikacji][api-management-aad-app-permissions]

<span data-ttu-id="62023-136">Wybierz hello **delegowanie uprawnień** listy rozwijanej i sprawdź **włączenia logowania jednokrotnego i odczytu profilów użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="62023-136">Select hello **Delegate Permissions** drop-down, and check **Enable sign-on and read users' profiles**.</span></span>

![Delegowane uprawnienia][api-management-aad-delegated-permissions]

> <span data-ttu-id="62023-138">Aby uzyskać więcej informacji o aplikacji i uprawnień delegowanych, zobacz [hello dostęp do interfejsu API programu Graph][Accessing hello Graph API].</span><span class="sxs-lookup"><span data-stu-id="62023-138">For more information about application and delegated permissions, see [Accessing hello Graph API][Accessing hello Graph API].</span></span>
> 
> 

<span data-ttu-id="62023-139">Kopiuj hello **identyfikator klienta** toohello Schowka.</span><span class="sxs-lookup"><span data-stu-id="62023-139">Copy hello **Client Id** toohello clipboard.</span></span>

![Identyfikator klienta][api-management-aad-app-client-id]

<span data-ttu-id="62023-141">Przełącz wstecz toohello wydawcy portalu i Wklej w hello **identyfikator klienta** skopiowanych z konfiguracji aplikacji hello Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="62023-141">Switch back toohello publisher portal and paste in hello **Client Id** copied from hello Azure Active Directory application configuration.</span></span>

![Identyfikator klienta][api-management-client-id]

<span data-ttu-id="62023-143">Konfiguracji usługi Azure Active Directory toohello tyłu przełącznika, a następnie kliknij przycisk hello **wybierz czas trwania** listy rozwijanej w hello **klucze** sekcji i określ interwał.</span><span class="sxs-lookup"><span data-stu-id="62023-143">Switch back toohello Azure Active Directory configuration, and click hello **Select duration** drop-down in hello **Keys** section and specify an interval.</span></span> <span data-ttu-id="62023-144">W tym przykładzie **1 rok** jest używany.</span><span class="sxs-lookup"><span data-stu-id="62023-144">In this example, **1 year** is used.</span></span>

![Klucz][api-management-aad-key-before-save]

<span data-ttu-id="62023-146">Kliknij przycisk **zapisać** toosave hello konfiguracji oraz wyświetlania hello klucza.</span><span class="sxs-lookup"><span data-stu-id="62023-146">Click **Save** toosave hello configuration and display hello key.</span></span> <span data-ttu-id="62023-147">Kopiuj hello klucza toohello Schowka.</span><span class="sxs-lookup"><span data-stu-id="62023-147">Copy hello key toohello clipboard.</span></span>

> <span data-ttu-id="62023-148">Zanotuj tego klucza.</span><span class="sxs-lookup"><span data-stu-id="62023-148">Make a note of this key.</span></span> <span data-ttu-id="62023-149">Po zamknięciu okna konfiguracji usługi Azure Active Directory hello hello klucza nie może ponownie wyświetlone.</span><span class="sxs-lookup"><span data-stu-id="62023-149">Once you close hello Azure Active Directory configuration window, hello key cannot be displayed again.</span></span>
> 
> 

![Klucz][api-management-aad-key-after-save]

<span data-ttu-id="62023-151">Przełącznik wstecz toohello wydawcy portalu i Wklej hello klucza do hello **klucz tajny klienta** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="62023-151">Switch back toohello publisher portal and paste hello key into hello **Client Secret** text box.</span></span>

![Klucz tajny klienta][api-management-client-secret]

<span data-ttu-id="62023-153">**Dozwolone dzierżaw** Określa, które katalogi mają toohello dostępu do interfejsów API wystąpienia usługi Zarządzanie interfejsami API hello.</span><span class="sxs-lookup"><span data-stu-id="62023-153">**Allowed Tenants** specifies which directories have access toohello APIs of hello API Management service instance.</span></span> <span data-ttu-id="62023-154">Określ hello domen hello program toogrant access toowhich wystąpienia usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="62023-154">Specify hello domains of hello Azure Active Directory instances toowhich you want toogrant access.</span></span> <span data-ttu-id="62023-155">Wiele domen można oddzielić newlines, spacjami lub przecinkami.</span><span class="sxs-lookup"><span data-stu-id="62023-155">You can separate multiple domains with newlines, spaces, or commas.</span></span>

![Dozwolone dzierżawcy][api-management-client-allowed-tenants]


<span data-ttu-id="62023-157">Po hello potrzeby określana jest konfiguracja, kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="62023-157">Once hello desired configuration is specified, click **Save**.</span></span>

![Zapisz][api-management-client-allowed-tenants-save]

<span data-ttu-id="62023-159">Po hello zmiany zostaną zapisane, użytkownicy hello hello określone usługi Azure Active Directory można Zaloguj się w portalu dla deweloperów toohello wykonując kroki hello w [Zaloguj się przy użyciu konta usługi Azure Active Directory portalu dla deweloperów toohello] [Log in toohello Developer portal using an Azure Active Directory account].</span><span class="sxs-lookup"><span data-stu-id="62023-159">Once hello changes are saved, hello users in hello specified Azure Active Directory can sign in toohello Developer portal by following hello steps in [Log in toohello Developer portal using an Azure Active Directory account][Log in toohello Developer portal using an Azure Active Directory account].</span></span>

<span data-ttu-id="62023-160">Można określić wiele domen w hello **dozwolone dzierżaw** sekcji.</span><span class="sxs-lookup"><span data-stu-id="62023-160">Multiple domains can be specified in hello **Allowed Tenants** section.</span></span> <span data-ttu-id="62023-161">Przed każdy użytkownik może zalogować się z innej domeny niż domena oryginalnego hello rejestracji aplikacji hello, administrator globalny innej domeny hello musi udzielić uprawnień tooaccess aplikacji hello dane katalogu.</span><span class="sxs-lookup"><span data-stu-id="62023-161">Before any user can log in from a different domain than hello original domain where hello application was registered, a global administrator of hello different domain must grant permission for hello application tooaccess directory data.</span></span> <span data-ttu-id="62023-162">uprawnienie toogrant administratora globalnego hello powinien pojawiać się zbyt`https://<URL of your developer portal>/aadadminconsent` (na przykład https://contoso.portal.azure-api.net/aadadminconsent), typ w nazwie domeny hello hello mają toogive tooand dostęp do dzierżawy usługi Active Directory kliknij przycisk Prześlij.</span><span class="sxs-lookup"><span data-stu-id="62023-162">toogrant permission, hello global administrator should go too`https://<URL of your developer portal>/aadadminconsent` (for example, https://contoso.portal.azure-api.net/aadadminconsent), type in hello domain name of hello Active Directory tenant they want toogive access tooand click Submit.</span></span> <span data-ttu-id="62023-163">W następujących hello przykład, administrator globalny `miaoaad.onmicrosoft.com` próbuje toogive uprawnienia toothis określonego developer portal.</span><span class="sxs-lookup"><span data-stu-id="62023-163">In hello following example, a global administrator from `miaoaad.onmicrosoft.com` is trying toogive permission toothis particular developer portal.</span></span> 

![Uprawnienia][api-management-aad-consent]

<span data-ttu-id="62023-165">W następnym ekranie powitania administratora globalnego hello będzie tooconfirm zostanie wyświetlony monit o nadanie uprawnień hello.</span><span class="sxs-lookup"><span data-stu-id="62023-165">In hello next screen, hello global administrator will be prompted tooconfirm giving hello permission.</span></span> 

![Uprawnienia][api-management-permissions-form]

> <span data-ttu-id="62023-167">Jeśli administrator globalny nie próbuje toolog w przed uprawnienia przyznane przez administratora globalnego, hello próba logowania nie powiedzie się i zostanie wyświetlony komunikat o błędzie.</span><span class="sxs-lookup"><span data-stu-id="62023-167">If a non-global administrator tries toolog in before permissions are granted by a global administrator, hello login attempt fails and an error screen is displayed.</span></span>
> 
> 

## <a name="how-tooadd-an-external-azure-active-directory-group"></a><span data-ttu-id="62023-168">Jak tooadd zewnętrznych usługi Azure Active Directory grupy</span><span class="sxs-lookup"><span data-stu-id="62023-168">How tooadd an external Azure Active Directory Group</span></span>
<span data-ttu-id="62023-169">Po włączeniu dostępu dla użytkowników w usłudze Azure Active Directory, można dodać grupy usługi Azure Active Directory do usługi API Management toomore łatwe zarządzanie skojarzenia hello deweloperów hello w grupie hello z produktami hello potrzebne.</span><span class="sxs-lookup"><span data-stu-id="62023-169">After enabling access for users in an Azure Active Directory, you can add Azure Active Directory groups into API Management toomore easily manage hello association of hello developers in hello group with hello desired products.</span></span>

> <span data-ttu-id="62023-170">tooconfigure zewnętrznych Azure grupy usługi Active Directory, hello Azure Active Directory należy najpierw skonfigurować na karcie tożsamości hello wykonując procedurę hello w poprzedniej sekcji hello.</span><span class="sxs-lookup"><span data-stu-id="62023-170">tooconfigure an external Azure Active Directory group, hello Azure Active Directory must first be configured in hello Identities tab by following hello procedure in hello previous section.</span></span> 
> 
> 

<span data-ttu-id="62023-171">Zewnętrzne grup usługi Azure Active Directory są dodawane z hello **widoczność** kartę hello produktu, dla którego chcesz toogrant dostępu toohello grupy.</span><span class="sxs-lookup"><span data-stu-id="62023-171">External Azure Active Directory groups are added from hello **Visibility** tab of hello product for which you wish toogrant access toohello group.</span></span> <span data-ttu-id="62023-172">Kliknij przycisk **produktów**, a następnie kliknij nazwę hello hello żądaną produktu.</span><span class="sxs-lookup"><span data-stu-id="62023-172">Click **Products**, and then click hello name of hello desired product.</span></span>

![Konfigurowanie produktu][api-management-configure-product]

<span data-ttu-id="62023-174">Przełącz toohello **widoczność** , a następnie kliknij pozycję **Dodawanie grup z usługi Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="62023-174">Switch toohello **Visibility** tab, and click **Add Groups from Azure Active Directory**.</span></span>

![Dodaj grupy][api-management-add-groups]

<span data-ttu-id="62023-176">Wybierz hello **Azure Active Directory dzierżawy** z listy rozwijanej hello, a następnie nazwę hello typu hello odpowiednią grupę w hello **grup** toobe dodać pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="62023-176">Select hello **Azure Active Directory Tenant** from hello drop-down list, and then type hello name of hello desired group in hello **Groups** toobe added text box.</span></span>

![Wybierz grupę][api-management-select-group]

<span data-ttu-id="62023-178">Ta nazwa grupy można znaleźć w hello **grup** lista dla usługi Azure Active Directory, jak pokazano w hello poniższy przykład.</span><span class="sxs-lookup"><span data-stu-id="62023-178">This group name can be found in hello **Groups** list for your Azure Active Directory, as shown in hello following example.</span></span>

![Lista grup usługi Azure Active Directory][api-management-aad-groups-list]

<span data-ttu-id="62023-180">Kliknij przycisk **Dodaj** toovalidate hello Nazwa grupy i Dodaj grupę hello.</span><span class="sxs-lookup"><span data-stu-id="62023-180">Click **Add** toovalidate hello group name and add hello group.</span></span> <span data-ttu-id="62023-181">W tym przykładzie hello **deweloperzy 5 Contoso** jest dodana grupa zewnętrzna.</span><span class="sxs-lookup"><span data-stu-id="62023-181">In this example, hello **Contoso 5 Developers** external group is added.</span></span> 

![Grupy dodane][api-management-aad-group-added]

<span data-ttu-id="62023-183">Kliknij przycisk **zapisać** toosave hello nowe wybranej grupy.</span><span class="sxs-lookup"><span data-stu-id="62023-183">Click **Save** toosave hello new group selection.</span></span>

<span data-ttu-id="62023-184">Po grupy usługi Azure Active Directory została skonfigurowana z jednego produktu, jest dostępny toobe zaznaczone na powitania **widoczność** kartę hello innych produktów w wystąpieniu usługi Zarządzanie interfejsami API hello.</span><span class="sxs-lookup"><span data-stu-id="62023-184">Once an Azure Active Directory group has been configured from one product, it is available toobe checked on hello **Visibility** tab for hello other products in hello API Management service instance.</span></span>

<span data-ttu-id="62023-185">tooreview i skonfigurować właściwości hello zewnętrznych grup po zostały dodane, kliknij nazwę hello hello grupy z hello **grup** kartę.</span><span class="sxs-lookup"><span data-stu-id="62023-185">tooreview and configure hello properties for external groups once they have been added, click hello name of hello group from hello **Groups** tab.</span></span>

![Zarządzanie grupami][api-management-groups]

<span data-ttu-id="62023-187">W tym miejscu można edytować hello **nazwa** i hello **opis** hello grupy.</span><span class="sxs-lookup"><span data-stu-id="62023-187">From here you can edit hello **Name** and hello **Description** of hello group.</span></span>

![Edytowanie grupy][api-management-edit-group]

<span data-ttu-id="62023-189">Użytkownikom hello skonfigurowane usługi Azure Active Directory można zarejestrować się w portalu dla deweloperów toohello i widoku i subskrybowania tooany grup, do których mają widoczność, wykonując instrukcje hello hello następujących sekcji.</span><span class="sxs-lookup"><span data-stu-id="62023-189">Users from hello configured Azure Active Directory can sign in toohello Developer portal and view and subscribe tooany groups for which they have visibility by following hello instructions in hello following section.</span></span>

## <a name="how-toolog-in-toohello-developer-portal-using-an-azure-active-directory-account"></a><span data-ttu-id="62023-190">Jak toolog w portalu dla deweloperów toohello przy użyciu konta usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="62023-190">How toolog in toohello Developer portal using an Azure Active Directory account</span></span>
<span data-ttu-id="62023-191">toolog w portalu dla deweloperów hello przy użyciu konta usługi Azure Active Directory skonfigurowanych w poprzednich sekcjach hello, Otwórz nowe okno przeglądarki, za pomocą hello **adres URL logowania** z konfiguracji aplikacji hello usługi Active Directory, a następnie kliknij przycisk **Usługi azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="62023-191">toolog into hello Developer portal using an Azure Active Directory account configured in hello previous sections, open a new browser window using hello **Sign-on URL** from hello Active Directory application configuration, and click **Azure Active Directory**.</span></span>

![Portalu dla deweloperów][api-management-dev-portal-signin]

<span data-ttu-id="62023-193">Wprowadź poświadczenia hello jednego hello użytkowników w usłudze Azure Active Directory, a następnie kliknij przycisk **Zaloguj**.</span><span class="sxs-lookup"><span data-stu-id="62023-193">Enter hello credentials of one of hello users in your Azure Active Directory, and click **Sign in**.</span></span>

![Logowanie][api-management-aad-signin]

<span data-ttu-id="62023-195">Może pojawić się prośba o formularz rejestracji Jeśli żadnych dodatkowych informacji jest wymagane.</span><span class="sxs-lookup"><span data-stu-id="62023-195">You may be prompted with a registration form if any additional information is required.</span></span> <span data-ttu-id="62023-196">Wypełnij formularz rejestracji hello i kliknij przycisk **Zarejestruj**.</span><span class="sxs-lookup"><span data-stu-id="62023-196">Complete hello registration form and click **Sign up**.</span></span>

![Rejestracja][api-management-complete-registration]

<span data-ttu-id="62023-198">Użytkownika jest teraz zalogowany do portalu dla deweloperów hello wystąpienia usługi Zarządzanie interfejsami API.</span><span class="sxs-lookup"><span data-stu-id="62023-198">Your user is now logged into hello developer portal for your API Management service instance.</span></span>

![Zakończono rejestrację][api-management-registration-complete]

[api-management-management-console]: ./media/api-management-howto-aad/api-management-management-console.png
[api-management-security-external-identities]: ./media/api-management-howto-aad/api-management-security-external-identities.png
[api-management-security-aad-new]: ./media/api-management-howto-aad/api-management-security-aad-new.png
[api-management-new-aad-application-menu]: ./media/api-management-howto-aad/api-management-new-aad-application-menu.png
[api-management-new-aad-application-1]: ./media/api-management-howto-aad/api-management-new-aad-application-1.png
[api-management-new-aad-application-2]: ./media/api-management-howto-aad/api-management-new-aad-application-2.png
[api-management-new-aad-app-created]: ./media/api-management-howto-aad/api-management-new-aad-app-created.png
[api-management-aad-app-permissions]: ./media/api-management-howto-aad/api-management-aad-app-permissions.png
[api-management-aad-app-client-id]: ./media/api-management-howto-aad/api-management-aad-app-client-id.png
[api-management-client-id]: ./media/api-management-howto-aad/api-management-client-id.png
[api-management-aad-key-before-save]: ./media/api-management-howto-aad/api-management-aad-key-before-save.png
[api-management-aad-key-after-save]: ./media/api-management-howto-aad/api-management-aad-key-after-save.png
[api-management-client-secret]: ./media/api-management-howto-aad/api-management-client-secret.png
[api-management-client-allowed-tenants]: ./media/api-management-howto-aad/api-management-client-allowed-tenants.png
[api-management-client-allowed-tenants-save]: ./media/api-management-howto-aad/api-management-client-allowed-tenants-save.png
[api-management-aad-delegated-permissions]: ./media/api-management-howto-aad/api-management-aad-delegated-permissions.png
[api-management-dev-portal-signin]: ./media/api-management-howto-aad/api-management-dev-portal-signin.png
[api-management-aad-signin]: ./media/api-management-howto-aad/api-management-aad-signin.png
[api-management-complete-registration]: ./media/api-management-howto-aad/api-management-complete-registration.png
[api-management-registration-complete]: ./media/api-management-howto-aad/api-management-registration-complete.png
[api-management-aad-app-multi-tenant]: ./media/api-management-howto-aad/api-management-aad-app-multi-tenant.png
[api-management-aad-reply-url]: ./media/api-management-howto-aad/api-management-aad-reply-url.png
[api-management-aad-consent]: ./media/api-management-howto-aad/api-management-aad-consent.png
[api-management-permissions-form]: ./media/api-management-howto-aad/api-management-permissions-form.png
[api-management-configure-product]: ./media/api-management-howto-aad/api-management-configure-product.png
[api-management-add-groups]: ./media/api-management-howto-aad/api-management-add-groups.png
[api-management-select-group]: ./media/api-management-howto-aad/api-management-select-group.png
[api-management-aad-groups-list]: ./media/api-management-howto-aad/api-management-aad-groups-list.png
[api-management-aad-group-added]: ./media/api-management-howto-aad/api-management-aad-group-added.png
[api-management-groups]: ./media/api-management-howto-aad/api-management-groups.png
[api-management-edit-group]: ./media/api-management-howto-aad/api-management-edit-group.png

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
[Accessing hello Graph API]: http://msdn.microsoft.com/library/azure/dn132599.aspx#BKMK_Graph

[Prerequisites]: #prerequisites
[Configure an OAuth 2.0 authorization server in API Management]: #step1
[Configure an API toouse OAuth 2.0 user authorization]: #step2
[Test hello OAuth 2.0 user authorization in hello Developer Portal]: #step3
[Next steps]: #next-steps

[Log in toohello Developer portal using an Azure Active Directory account]: #Log-in-to-the-Developer-portal-using-an-Azure-Active-Directory-account

