---
title: "Autoryzowanie konta dewelopera przy użyciu usługi Azure Active Directory — Zarządzanie interfejsami API Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak i autoryzacji użytkowników w usłudze API Management przy użyciu usługi Azure Active Directory."
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
ms.openlocfilehash: 7637e6419d17a2d75904fbe63df5f27d4be4bbe3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-authorize-developer-accounts-using-azure-active-directory-in-azure-api-management"></a><span data-ttu-id="7c55d-103">Sposób autoryzowania konta dewelopera przy użyciu usługi Azure Active Directory w usłudze Azure API Management</span><span class="sxs-lookup"><span data-stu-id="7c55d-103">How to authorize developer accounts using Azure Active Directory in Azure API Management</span></span>
## <a name="overview"></a><span data-ttu-id="7c55d-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="7c55d-104">Overview</span></span>
<span data-ttu-id="7c55d-105">Ten przewodnik zawiera instrukcje umożliwić dostęp do portalu dla deweloperów dla użytkowników z usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="7c55d-105">This guide shows you how to enable access to the developer portal for users from Azure Active Directory.</span></span> <span data-ttu-id="7c55d-106">W tym przewodniku przedstawiono również sposób zarządzać grupami użytkowników usługi Azure Active Directory przez dodanie zewnętrznej grupy, które zawierają użytkowników usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="7c55d-106">This guide also shows you how to manage groups of Azure Active Directory users by adding external groups that contain the users of an Azure Active Directory.</span></span>

> <span data-ttu-id="7c55d-107">Aby wykonać kroki opisane w tym przewodniku najpierw musi mieć usługi Azure Active Directory, umożliwiający tworzenie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="7c55d-107">To complete the steps in this guide you must first have an Azure Active Directory in which to create an application.</span></span>
> 
> 

## <a name="how-to-authorize-developer-accounts-using-azure-active-directory"></a><span data-ttu-id="7c55d-108">Sposób autoryzowania konta dewelopera przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7c55d-108">How to authorize developer accounts using Azure Active Directory</span></span>
<span data-ttu-id="7c55d-109">Aby rozpocząć, kliknij przycisk **portal wydawcy** w portalu Azure usługi Zarządzanie interfejsami API.</span><span class="sxs-lookup"><span data-stu-id="7c55d-109">To get started, click **Publisher portal** in the Azure portal for your API Management service.</span></span> <span data-ttu-id="7c55d-110">Spowoduje to przejście do portalu wydawcy usługi API Management.</span><span class="sxs-lookup"><span data-stu-id="7c55d-110">This takes you to the API Management publisher portal.</span></span>

![Portal wydawcy][api-management-management-console]

> <span data-ttu-id="7c55d-112">Jeśli jeszcze nie masz utworzonego wystąpienia usługi API Management, zobacz [Tworzenie wystąpienia usługi API Management][Create an API Management service instance] w samouczku [Wprowadzenie do usługi Azure API Management][Get started with Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="7c55d-112">If you have not yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Get started with Azure API Management][Get started with Azure API Management] tutorial.</span></span>
> 
> 

<span data-ttu-id="7c55d-113">Kliknij przycisk **zabezpieczeń** z **zarządzanie interfejsami API** menu po lewej stronie i kliknij przycisk **tożsamości zewnętrznych**.</span><span class="sxs-lookup"><span data-stu-id="7c55d-113">Click **Security** from the **API Management** menu on the left and click **External Identities**.</span></span>

![Tożsamości zewnętrznych][api-management-security-external-identities]

<span data-ttu-id="7c55d-115">Kliknij przycisk **usługi Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7c55d-115">Click **Azure Active Directory**.</span></span> <span data-ttu-id="7c55d-116">Zanotuj **adresem URL przekierowania** i przełączyć się do usługi Azure Active Directory w klasycznym portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="7c55d-116">Make a note of the **Redirect URL** and switch over to your Azure Active Directory in the Azure Classic Portal.</span></span>

![Tożsamości zewnętrznych][api-management-security-aad-new]

<span data-ttu-id="7c55d-118">Kliknij przycisk **Dodaj** przycisk, aby utworzyć nową aplikację usługi Azure Active Directory, a następnie wybierz pozycję **Dodaj aplikację moją organizację**.</span><span class="sxs-lookup"><span data-stu-id="7c55d-118">Click the **Add** button to create a new Azure Active Directory application, and choose **Add an application my organization is developing**.</span></span>

![Dodaj nową aplikację usługi Azure Active Directory][api-management-new-aad-application-menu]

<span data-ttu-id="7c55d-120">Wprowadź nazwę aplikacji, wybierz pozycję **sieci Web, aplikacji i/lub interfejs API sieci Web**i kliknij przycisk Dalej.</span><span class="sxs-lookup"><span data-stu-id="7c55d-120">Enter a name for the application, select **Web application and/or Web API**, and click the next button.</span></span>

![Nową aplikację usługi Azure Active Directory][api-management-new-aad-application-1]

<span data-ttu-id="7c55d-122">Aby uzyskać **adres URL logowania**, wprowadź adres URL rejestracji z portalu dla deweloperów.</span><span class="sxs-lookup"><span data-stu-id="7c55d-122">For **Sign-on URL**, enter the sign-on URL of your developer portal.</span></span> <span data-ttu-id="7c55d-123">W tym przykładzie **adres URL logowania** jest `https://aad03.portal.current.int-azure-api.net/signin`.</span><span class="sxs-lookup"><span data-stu-id="7c55d-123">In this example, the **Sign-on URL** is `https://aad03.portal.current.int-azure-api.net/signin`.</span></span> 

<span data-ttu-id="7c55d-124">Aby uzyskać **adres URL Identyfikatora aplikacji**, wprowadź w domenie domyślnej lub niestandardowej domeny dla usługi Azure Active Directory i Dołącz unikatowy ciąg do niego.</span><span class="sxs-lookup"><span data-stu-id="7c55d-124">For the **App ID URL**, enter either the default domain or a custom domain for the Azure Active Directory, and append a unique string to it.</span></span> <span data-ttu-id="7c55d-125">W tym przykładzie domyślnej domeny **https://contoso5api.onmicrosoft.com** jest używana z sufiksem **/api** określony.</span><span class="sxs-lookup"><span data-stu-id="7c55d-125">In this example, the default domain of **https://contoso5api.onmicrosoft.com** is used with the suffix of **/api** specified.</span></span>

![Nowe właściwości aplikacji usługi Azure Active Directory][api-management-new-aad-application-2]

<span data-ttu-id="7c55d-127">Kliknij przycisk wyboru, aby zapisać i utworzyć aplikację, a następnie przejdź do **Konfiguruj** kartę, aby skonfigurować nową aplikację.</span><span class="sxs-lookup"><span data-stu-id="7c55d-127">Click the check button to save and create the application, and switch to the **Configure** tab to configure the new application.</span></span>

![Nowej aplikacji usługi Azure Active Directory][api-management-new-aad-app-created]

<span data-ttu-id="7c55d-129">Jeśli wiele Azure Active Directory mają być używany dla tej aplikacji, kliknij przycisk **tak** dla **aplikacji jest wielodostępne**.</span><span class="sxs-lookup"><span data-stu-id="7c55d-129">If multiple Azure Active Directories are going to be used for this application, click **Yes** for **Application is multi-tenant**.</span></span> <span data-ttu-id="7c55d-130">Wartość domyślna to **nr**.</span><span class="sxs-lookup"><span data-stu-id="7c55d-130">The default is **No**.</span></span>

![Aplikacja jest wieloma dzierżawcami][api-management-aad-app-multi-tenant]

<span data-ttu-id="7c55d-132">Kopiuj **adresem URL przekierowania** z **usługi Azure Active Directory** sekcji **tożsamości zewnętrznych** w portalu wydawcy i wklej ją do **odpowiedzi Adres URL** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="7c55d-132">Copy the **Redirect URL** from the **Azure Active Directory** section of the **External Identities** tab in the publisher portal and paste it into the **Reply URL** text box.</span></span> 

![Adres URL odpowiedzi][api-management-aad-reply-url]

<span data-ttu-id="7c55d-134">Przewiń w dół na karcie Konfiguracja, wybierz opcję **uprawnienia aplikacji** listy rozwijanej i sprawdź **odczytuj dane katalogu**.</span><span class="sxs-lookup"><span data-stu-id="7c55d-134">Scroll to the bottom of the configure tab, select the **Application Permissions** drop-down, and check **Read directory data**.</span></span>

![Uprawnienia aplikacji][api-management-aad-app-permissions]

<span data-ttu-id="7c55d-136">Wybierz **delegowanie uprawnień** listy rozwijanej i sprawdź **włączenia logowania jednokrotnego i odczytu profilów użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="7c55d-136">Select the **Delegate Permissions** drop-down, and check **Enable sign-on and read users' profiles**.</span></span>

![Delegowane uprawnienia][api-management-aad-delegated-permissions]

> <span data-ttu-id="7c55d-138">Aby uzyskać więcej informacji o aplikacji i uprawnień delegowanych, zobacz [podczas uzyskiwania dostępu do interfejsu API programu Graph][Accessing the Graph API].</span><span class="sxs-lookup"><span data-stu-id="7c55d-138">For more information about application and delegated permissions, see [Accessing the Graph API][Accessing the Graph API].</span></span>
> 
> 

<span data-ttu-id="7c55d-139">Kopiuj **identyfikator klienta** do Schowka.</span><span class="sxs-lookup"><span data-stu-id="7c55d-139">Copy the **Client Id** to the clipboard.</span></span>

![Identyfikator klienta][api-management-aad-app-client-id]

<span data-ttu-id="7c55d-141">Przełączyć się do portalu wydawcy i Wklej w **identyfikator klienta** skopiowanych z konfiguracji aplikacji usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="7c55d-141">Switch back to the publisher portal and paste in the **Client Id** copied from the Azure Active Directory application configuration.</span></span>

![Identyfikator klienta][api-management-client-id]

<span data-ttu-id="7c55d-143">Wrócić do konfiguracji usługi Azure Active Directory, a następnie kliknij przycisk **wybierz czas trwania** listy rozwijanej w **klucze** sekcji i określ interwał.</span><span class="sxs-lookup"><span data-stu-id="7c55d-143">Switch back to the Azure Active Directory configuration, and click the **Select duration** drop-down in the **Keys** section and specify an interval.</span></span> <span data-ttu-id="7c55d-144">W tym przykładzie **1 rok** jest używany.</span><span class="sxs-lookup"><span data-stu-id="7c55d-144">In this example, **1 year** is used.</span></span>

![Klucz][api-management-aad-key-before-save]

<span data-ttu-id="7c55d-146">Kliknij przycisk **zapisać** do zapisania konfiguracji, a następnie wyświetlić klucz.</span><span class="sxs-lookup"><span data-stu-id="7c55d-146">Click **Save** to save the configuration and display the key.</span></span> <span data-ttu-id="7c55d-147">Skopiuj klucz do Schowka.</span><span class="sxs-lookup"><span data-stu-id="7c55d-147">Copy the key to the clipboard.</span></span>

> <span data-ttu-id="7c55d-148">Zanotuj tego klucza.</span><span class="sxs-lookup"><span data-stu-id="7c55d-148">Make a note of this key.</span></span> <span data-ttu-id="7c55d-149">Po zamknięciu okna konfiguracji usługi Azure Active Directory, klucz nie może ponownie wyświetlone.</span><span class="sxs-lookup"><span data-stu-id="7c55d-149">Once you close the Azure Active Directory configuration window, the key cannot be displayed again.</span></span>
> 
> 

![Klucz][api-management-aad-key-after-save]

<span data-ttu-id="7c55d-151">Przełączyć się do portalu wydawcy i Wklej klucz do **klucz tajny klienta** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="7c55d-151">Switch back to the publisher portal and paste the key into the **Client Secret** text box.</span></span>

![Klucz tajny klienta][api-management-client-secret]

<span data-ttu-id="7c55d-153">**Dozwolone dzierżaw** Określa, które katalogi mają dostęp do interfejsów API wystąpienia usługi Zarządzanie interfejsami API.</span><span class="sxs-lookup"><span data-stu-id="7c55d-153">**Allowed Tenants** specifies which directories have access to the APIs of the API Management service instance.</span></span> <span data-ttu-id="7c55d-154">Określ domeny wystąpień usługi Azure Active Directory, do których chcesz udzielić dostępu.</span><span class="sxs-lookup"><span data-stu-id="7c55d-154">Specify the domains of the Azure Active Directory instances to which you want to grant access.</span></span> <span data-ttu-id="7c55d-155">Wiele domen można oddzielić newlines, spacjami lub przecinkami.</span><span class="sxs-lookup"><span data-stu-id="7c55d-155">You can separate multiple domains with newlines, spaces, or commas.</span></span>

![Dozwolone dzierżawcy][api-management-client-allowed-tenants]


<span data-ttu-id="7c55d-157">Po wymaganą konfiguracją jest określony, kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="7c55d-157">Once the desired configuration is specified, click **Save**.</span></span>

![Zapisz][api-management-client-allowed-tenants-save]

<span data-ttu-id="7c55d-159">Po zmiany zostaną zapisane, użytkownicy w określonej usługi Azure Active Directory mogą zalogować się do portalu dla deweloperów wykonując kroki opisane w [zalogować się do portalu dla deweloperów przy użyciu konta usługi Azure Active Directory] [ Log in to the Developer portal using an Azure Active Directory account].</span><span class="sxs-lookup"><span data-stu-id="7c55d-159">Once the changes are saved, the users in the specified Azure Active Directory can sign in to the Developer portal by following the steps in [Log in to the Developer portal using an Azure Active Directory account][Log in to the Developer portal using an Azure Active Directory account].</span></span>

<span data-ttu-id="7c55d-160">Można określić wiele domen w **dozwolone dzierżaw** sekcji.</span><span class="sxs-lookup"><span data-stu-id="7c55d-160">Multiple domains can be specified in the **Allowed Tenants** section.</span></span> <span data-ttu-id="7c55d-161">Przed każdy użytkownik może zalogować się z innej domeny niż domena oryginalnego rejestracji aplikacji, administrator globalny innej domeny musi udzielić uprawnień do dostępu do danych katalogu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="7c55d-161">Before any user can log in from a different domain than the original domain where the application was registered, a global administrator of the different domain must grant permission for the application to access directory data.</span></span> <span data-ttu-id="7c55d-162">Aby udzielić uprawnień, przejść do administratora globalnego `https://<URL of your developer portal>/aadadminconsent` (na przykład https://contoso.portal.azure-api.net/aadadminconsent), wpisz nazwę domeny dzierżawy usługi Active Directory, które chcą, aby przyznać dostęp, a następnie kliknij przycisk Prześlij.</span><span class="sxs-lookup"><span data-stu-id="7c55d-162">To grant permission, the global administrator should go to `https://<URL of your developer portal>/aadadminconsent` (for example, https://contoso.portal.azure-api.net/aadadminconsent), type in the domain name of the Active Directory tenant they want to give access to and click Submit.</span></span> <span data-ttu-id="7c55d-163">W poniższym przykładzie administrator globalny `miaoaad.onmicrosoft.com` chce się nadać uprawnienia do tego portalu dewelopera w konkretnym.</span><span class="sxs-lookup"><span data-stu-id="7c55d-163">In the following example, a global administrator from `miaoaad.onmicrosoft.com` is trying to give permission to this particular developer portal.</span></span> 

![Uprawnienia][api-management-aad-consent]

<span data-ttu-id="7c55d-165">Na następnym ekranie administratora globalnego pojawi się monit o potwierdzenie nadanie uprawnień.</span><span class="sxs-lookup"><span data-stu-id="7c55d-165">In the next screen, the global administrator will be prompted to confirm giving the permission.</span></span> 

![Uprawnienia][api-management-permissions-form]

> <span data-ttu-id="7c55d-167">Jeśli administrator globalny nie próbuje zalogować przed uprawnienia są udzielane przez administratora globalnego, próba logowania nie powiedzie się i zostanie wyświetlony komunikat o błędzie.</span><span class="sxs-lookup"><span data-stu-id="7c55d-167">If a non-global administrator tries to log in before permissions are granted by a global administrator, the login attempt fails and an error screen is displayed.</span></span>
> 
> 

## <a name="how-to-add-an-external-azure-active-directory-group"></a><span data-ttu-id="7c55d-168">Jak dodać zewnętrznych Azure grupy usługi Active Directory</span><span class="sxs-lookup"><span data-stu-id="7c55d-168">How to add an external Azure Active Directory Group</span></span>
<span data-ttu-id="7c55d-169">Po włączeniu dostępu dla użytkowników w usłudze Azure Active Directory, można dodać grupy usługi Azure Active Directory interfejsu API do zarządzania w celu skojarzenia deweloperów w grupie z żądaną produktów w prostszy sposób zarządzać.</span><span class="sxs-lookup"><span data-stu-id="7c55d-169">After enabling access for users in an Azure Active Directory, you can add Azure Active Directory groups into API Management to more easily manage the association of the developers in the group with the desired products.</span></span>

> <span data-ttu-id="7c55d-170">Aby skonfigurować zewnętrznego grupy usługi Azure Active Directory, usługi Azure Active Directory należy najpierw skonfigurować na karcie tożsamości wykonując poniższe kroki w poprzedniej sekcji.</span><span class="sxs-lookup"><span data-stu-id="7c55d-170">To configure an external Azure Active Directory group, the Azure Active Directory must first be configured in the Identities tab by following the procedure in the previous section.</span></span> 
> 
> 

<span data-ttu-id="7c55d-171">Zewnętrzne grup usługi Azure Active Directory są dodawane z **widoczność** na karcie produktu, dla którego chcesz udzielić dostępu do grupy.</span><span class="sxs-lookup"><span data-stu-id="7c55d-171">External Azure Active Directory groups are added from the **Visibility** tab of the product for which you wish to grant access to the group.</span></span> <span data-ttu-id="7c55d-172">Kliknij przycisk **produktów**, a następnie kliknij nazwę żądanego produktu.</span><span class="sxs-lookup"><span data-stu-id="7c55d-172">Click **Products**, and then click the name of the desired product.</span></span>

![Konfigurowanie produktu][api-management-configure-product]

<span data-ttu-id="7c55d-174">Przełącz się do **widoczność** , a następnie kliknij pozycję **Dodawanie grup z usługi Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7c55d-174">Switch to the **Visibility** tab, and click **Add Groups from Azure Active Directory**.</span></span>

![Dodaj grupy][api-management-add-groups]

<span data-ttu-id="7c55d-176">Wybierz **Azure Active Directory dzierżawy** z listy rozwijanej liście, a następnie wpisz nazwę w odpowiedniej grupy **grup** do dodania pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="7c55d-176">Select the **Azure Active Directory Tenant** from the drop-down list, and then type the name of the desired group in the **Groups** to be added text box.</span></span>

![Wybierz grupę][api-management-select-group]

<span data-ttu-id="7c55d-178">Ta nazwa grupy można znaleźć w **grup** lista dla usługi Azure Active Directory, jak pokazano w poniższym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="7c55d-178">This group name can be found in the **Groups** list for your Azure Active Directory, as shown in the following example.</span></span>

![Lista grup usługi Azure Active Directory][api-management-aad-groups-list]

<span data-ttu-id="7c55d-180">Kliknij przycisk **Dodaj** do sprawdzania poprawności nazwy grupy i Dodaj grupę.</span><span class="sxs-lookup"><span data-stu-id="7c55d-180">Click **Add** to validate the group name and add the group.</span></span> <span data-ttu-id="7c55d-181">W tym przykładzie **deweloperzy 5 Contoso** jest dodana grupa zewnętrzna.</span><span class="sxs-lookup"><span data-stu-id="7c55d-181">In this example, the **Contoso 5 Developers** external group is added.</span></span> 

![Grupy dodane][api-management-aad-group-added]

<span data-ttu-id="7c55d-183">Kliknij przycisk **zapisać** można zapisać nowego wybranej grupy.</span><span class="sxs-lookup"><span data-stu-id="7c55d-183">Click **Save** to save the new group selection.</span></span>

<span data-ttu-id="7c55d-184">Po grupy usługi Azure Active Directory zostało skonfigurowane z jednym z produktów, jest ona dostępna do sprawdzenia na **widoczność** kartę dla innych produktów w wystąpieniu usługi Zarządzanie interfejsami API.</span><span class="sxs-lookup"><span data-stu-id="7c55d-184">Once an Azure Active Directory group has been configured from one product, it is available to be checked on the **Visibility** tab for the other products in the API Management service instance.</span></span>

<span data-ttu-id="7c55d-185">Aby przejrzeć i skonfiguruj właściwości dla zewnętrznych grup po ich dodaniu, kliknij nazwę grupy z **grup** kartę.</span><span class="sxs-lookup"><span data-stu-id="7c55d-185">To review and configure the properties for external groups once they have been added, click the name of the group from the **Groups** tab.</span></span>

![Zarządzanie grupami][api-management-groups]

<span data-ttu-id="7c55d-187">W tym miejscu można edytować **nazwa** i **opis** grupy.</span><span class="sxs-lookup"><span data-stu-id="7c55d-187">From here you can edit the **Name** and the **Description** of the group.</span></span>

![Edytowanie grupy][api-management-edit-group]

<span data-ttu-id="7c55d-189">Użytkownikom skonfigurowane usługi Azure Active Directory można zalogować się do portalu dla deweloperów i widoku oraz subskrybować żadnej z grup, do których mają widoczność, postępując zgodnie z instrukcjami w następnej sekcji.</span><span class="sxs-lookup"><span data-stu-id="7c55d-189">Users from the configured Azure Active Directory can sign in to the Developer portal and view and subscribe to any groups for which they have visibility by following the instructions in the following section.</span></span>

## <a name="how-to-log-in-to-the-developer-portal-using-an-azure-active-directory-account"></a><span data-ttu-id="7c55d-190">Jak zalogować się do portalu dla deweloperów przy użyciu konta usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7c55d-190">How to log in to the Developer portal using an Azure Active Directory account</span></span>
<span data-ttu-id="7c55d-191">Aby zalogować się do portalu dla deweloperów przy użyciu konta usługi Azure Active Directory skonfigurowanych w poprzednich sekcjach, Otwórz nowe okno przeglądarki, za pomocą **adres URL logowania** konfiguracji aplikacji usługi Active Directory i kliknij przycisk **Usługi azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7c55d-191">To log into the Developer portal using an Azure Active Directory account configured in the previous sections, open a new browser window using the **Sign-on URL** from the Active Directory application configuration, and click **Azure Active Directory**.</span></span>

![Portalu dla deweloperów][api-management-dev-portal-signin]

<span data-ttu-id="7c55d-193">Wprowadź poświadczenia użytkowników w usłudze Azure Active Directory, a następnie kliknij przycisk **Zaloguj**.</span><span class="sxs-lookup"><span data-stu-id="7c55d-193">Enter the credentials of one of the users in your Azure Active Directory, and click **Sign in**.</span></span>

![Logowanie][api-management-aad-signin]

<span data-ttu-id="7c55d-195">Może pojawić się prośba o formularz rejestracji Jeśli żadnych dodatkowych informacji jest wymagane.</span><span class="sxs-lookup"><span data-stu-id="7c55d-195">You may be prompted with a registration form if any additional information is required.</span></span> <span data-ttu-id="7c55d-196">Wypełnij formularz rejestracji, a następnie kliknij przycisk **Zarejestruj**.</span><span class="sxs-lookup"><span data-stu-id="7c55d-196">Complete the registration form and click **Sign up**.</span></span>

![Rejestracja][api-management-complete-registration]

<span data-ttu-id="7c55d-198">Użytkownika jest obecnie zalogowany do portalu dla deweloperów wystąpienia usługi Zarządzanie interfejsami API.</span><span class="sxs-lookup"><span data-stu-id="7c55d-198">Your user is now logged into the developer portal for your API Management service instance.</span></span>

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

[How to add operations to an API]: api-management-howto-add-operations.md
[How to add and publish a product]: api-management-howto-add-products.md
[Monitoring and analytics]: api-management-monitoring.md
[Add APIs to a product]: api-management-howto-add-products.md#add-apis
[Publish a product]: api-management-howto-add-products.md#publish-product
[Get started with Azure API Management]: api-management-get-started.md
[API Management policy reference]: api-management-policy-reference.md
[Caching policies]: api-management-policy-reference.md#caching-policies
[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[http://oauth.net/2/]: http://oauth.net/2/
[WebApp-GraphAPI-DotNet]: https://github.com/AzureADSamples/WebApp-GraphAPI-DotNet
[Accessing the Graph API]: http://msdn.microsoft.com/library/azure/dn132599.aspx#BKMK_Graph

[Prerequisites]: #prerequisites
[Configure an OAuth 2.0 authorization server in API Management]: #step1
[Configure an API to use OAuth 2.0 user authorization]: #step2
[Test the OAuth 2.0 user authorization in the Developer Portal]: #step3
[Next steps]: #next-steps

[Log in to the Developer portal using an Azure Active Directory account]: #Log-in-to-the-Developer-portal-using-an-Azure-Active-Directory-account

