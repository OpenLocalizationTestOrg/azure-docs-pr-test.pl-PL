---
title: "konta dewelopera aaaAuthorize za pomocą usługi Azure Active Directory B2C - Azure API Management | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooauthorize użytkowników za pomocą usługi Azure Active Directory B2C w usłudze API Management."
services: api-management
documentationcenter: API Management
author: miaojiang
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
ms.openlocfilehash: 28f7cae53138938dbbc848b4afcbf08b72690e37
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooauthorize-developer-accounts-by-using-azure-active-directory-b2c-in-azure-api-management"></a><span data-ttu-id="622e1-103">Jak tooauthorize developer kont przy użyciu narzędzia Azure Active Directory B2C w usłudze Azure API Management</span><span class="sxs-lookup"><span data-stu-id="622e1-103">How tooauthorize developer accounts by using Azure Active Directory B2C in Azure API Management</span></span>
## <a name="overview"></a><span data-ttu-id="622e1-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="622e1-104">Overview</span></span>
<span data-ttu-id="622e1-105">Usługa Azure Active Directory B2C jest chmury rozwiązania do zarządzania tożsamościami internetowych i aplikacji dla urządzeń przenośnych.</span><span class="sxs-lookup"><span data-stu-id="622e1-105">Azure Active Directory B2C is a cloud identity management solution for consumer-facing web and mobile applications.</span></span> <span data-ttu-id="622e1-106">Służy on toomanage dostępu tooyour developer portal.</span><span class="sxs-lookup"><span data-stu-id="622e1-106">You can use it toomanage access tooyour developer portal.</span></span> <span data-ttu-id="622e1-107">Ten przewodnik przedstawia hello konfiguracji, który jest wymagany w Twojej toointegrate usługi Zarządzanie interfejsami API z usługi Azure Active Directory B2C.</span><span class="sxs-lookup"><span data-stu-id="622e1-107">This guide shows you hello configuration that's required in your API Management service toointegrate with Azure Active Directory B2C.</span></span> <span data-ttu-id="622e1-108">Aby uzyskać informacje na temat włączania dostępu do portalu dla deweloperów toohello przy użyciu klasycznego Azure Active Directory, zobacz [jak tooauthorize developer kont przy użyciu narzędzia Azure Active Directory].</span><span class="sxs-lookup"><span data-stu-id="622e1-108">For information about enabling access toohello developer portal by using classic Azure Active Directory, see [How tooauthorize developer accounts using Azure Active Directory].</span></span>

> [!NOTE]
> <span data-ttu-id="622e1-109">toocomplete hello kroków tego podręcznika, najpierw musisz toocreate dzierżawy usługi Azure Active Directory B2C aplikacja.</span><span class="sxs-lookup"><span data-stu-id="622e1-109">toocomplete hello steps in this guide, you must first have an Azure Active Directory B2C tenant toocreate an application in.</span></span> <span data-ttu-id="622e1-110">Ponadto należy zasad rejestracji i logowania toohave gotowe.</span><span class="sxs-lookup"><span data-stu-id="622e1-110">Also, you need toohave signup and signin policies ready.</span></span> <span data-ttu-id="622e1-111">Aby uzyskać więcej informacji, zobacz [Omówienie usługi Azure Active Directory B2C].</span><span class="sxs-lookup"><span data-stu-id="622e1-111">For more information, see [Azure Active Directory B2C overview].</span></span>

## <a name="authorize-developer-accounts-by-using-azure-active-directory-b2c"></a><span data-ttu-id="622e1-112">Autoryzowanie konta dewelopera przy użyciu usługi Azure Active Directory B2C</span><span class="sxs-lookup"><span data-stu-id="622e1-112">Authorize developer accounts by using Azure Active Directory B2C</span></span>

1. <span data-ttu-id="622e1-113">tooget pracę, kliknij przycisk **portal wydawcy** w portalu Azure usługi Zarządzanie interfejsami API hello.</span><span class="sxs-lookup"><span data-stu-id="622e1-113">tooget started, click **Publisher portal** in hello Azure portal for your API Management service.</span></span> <span data-ttu-id="622e1-114">Trwa toohello zarządzanie interfejsami API wydawcy portalu.</span><span class="sxs-lookup"><span data-stu-id="622e1-114">This takes you toohello API Management publisher portal.</span></span>

   ![Portal wydawcy][api-management-management-console]

   > [!NOTE]
   > <span data-ttu-id="622e1-116">Jeśli jeszcze nie utworzono wystąpienie usługi API Management, zobacz [Utwórz wystąpienie usługi Zarządzanie interfejsami API] [ Create an API Management service instance] w hello [wprowadzenie do usługi Azure API Management samouczek][Get started with Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="622e1-116">If you haven't yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in hello [Get started with Azure API Management tutorial][Get started with Azure API Management].</span></span>

2. <span data-ttu-id="622e1-117">Na powitania **zarządzanie interfejsami API** menu, kliknij przycisk **zabezpieczeń**.</span><span class="sxs-lookup"><span data-stu-id="622e1-117">On hello **API Management** menu, click **Security**.</span></span> <span data-ttu-id="622e1-118">Na powitania **tożsamości** , wybierz pozycję **usługi Azure Active Directory B2C**.</span><span class="sxs-lookup"><span data-stu-id="622e1-118">On hello **Identities** tab, choose **Azure Active Directory B2C**.</span></span>

  ![1 tożsamości zewnętrznych][api-management-howto-aad-b2c-security-tab]

3. <span data-ttu-id="622e1-120">Zanotuj hello **adresem URL przekierowania** i przełączyć na tooAzure Active Directory B2C w portalu Azure hello.</span><span class="sxs-lookup"><span data-stu-id="622e1-120">Make a note of hello **Redirect URL** and switch over tooAzure Active Directory B2C in hello Azure portal.</span></span>

  ![2 tożsamości zewnętrznych][api-management-howto-aad-b2c-security-tab-reply-url]

4. <span data-ttu-id="622e1-122">Kliknij przycisk hello **aplikacji** przycisku.</span><span class="sxs-lookup"><span data-stu-id="622e1-122">Click hello **Applications** button.</span></span>

  ![Zarejestrować nową aplikację 1][api-management-howto-aad-b2c-portal-menu]

5. <span data-ttu-id="622e1-124">Kliknij przycisk hello **Dodaj** przycisk aplikacji toocreate nowej usługi Azure Active Directory B2C.</span><span class="sxs-lookup"><span data-stu-id="622e1-124">Click hello **Add** button toocreate a new Azure Active Directory B2C application.</span></span>

  ![Zarejestrować nową aplikację 2][api-management-howto-aad-b2c-add-button]

6. <span data-ttu-id="622e1-126">W hello **nowej aplikacji** bloku, wprowadź nazwę aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="622e1-126">In hello **New application** blade, enter a name for hello application.</span></span> <span data-ttu-id="622e1-127">Wybierz **tak** w obszarze **interfejsu API sieci Web i aplikacji sieci Web**i wybierz polecenie **tak** w obszarze **Zezwalaj przepływu niejawnego**.</span><span class="sxs-lookup"><span data-stu-id="622e1-127">Choose **Yes** under **Web App/Web API**, and choose **Yes** under **Allow implicit flow**.</span></span> <span data-ttu-id="622e1-128">Następnie hello kopiowania **adresem URL przekierowania** z hello **usługi Azure Active Directory B2C** sekcji hello **tożsamości** karcie w portalu wydawcy hello i wklej go do hello **Adres URL odpowiedzi** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="622e1-128">Then copy hello **Redirect URL** from hello **Azure Active Directory B2C** section of hello **Identities** tab in hello publisher portal, and paste it into hello **Reply URL** text box.</span></span>

  ![Zarejestrować nową aplikację 3][api-management-howto-aad-b2c-app-details]

7. <span data-ttu-id="622e1-130">Kliknij przycisk hello **Utwórz** przycisku.</span><span class="sxs-lookup"><span data-stu-id="622e1-130">Click hello **Create** button.</span></span> <span data-ttu-id="622e1-131">Po utworzeniu aplikacji hello jest wyświetlana w hello **aplikacji** bloku.</span><span class="sxs-lookup"><span data-stu-id="622e1-131">When hello application is created, it appears in hello **Applications** blade.</span></span> <span data-ttu-id="622e1-132">Kliknij przycisk toosee Nazwa aplikacji hello jego szczegóły.</span><span class="sxs-lookup"><span data-stu-id="622e1-132">Click hello application name toosee its details.</span></span>

  ![Zarejestrować nową aplikację 4][api-management-howto-aad-b2c-app-created]

8. <span data-ttu-id="622e1-134">Z hello **właściwości** bloku, hello kopiowania **identyfikator aplikacji** toohello Schowka.</span><span class="sxs-lookup"><span data-stu-id="622e1-134">From hello **Properties** blade, copy hello **Application ID** toohello clipboard.</span></span>

  ![Identyfikator aplikacji 1][api-management-howto-aad-b2c-app-id]

9. <span data-ttu-id="622e1-136">Przełącz wstecz toohello wydawcy portalu i wklej identyfikator hello w hello **identyfikator klienta** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="622e1-136">Switch back toohello publisher portal and paste hello ID into hello **Client Id** text box.</span></span>

  ![Identyfikator aplikacji 2][api-management-howto-aad-b2c-client-id]

10. <span data-ttu-id="622e1-138">Przełącz wstecz toohello portalu Azure, kliknij hello **klucze** przycisk, a następnie kliknij przycisk **generowanie klucza**.</span><span class="sxs-lookup"><span data-stu-id="622e1-138">Switch back toohello Azure portal, click hello **Keys** button, and then click **Generate key**.</span></span> <span data-ttu-id="622e1-139">Kliknij przycisk **zapisać** hello konfiguracji oraz wyświetlania hello toosave **klucz aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="622e1-139">Click **Save** toosave hello configuration and display hello **App key**.</span></span> <span data-ttu-id="622e1-140">Kopiuj hello klucza toohello Schowka.</span><span class="sxs-lookup"><span data-stu-id="622e1-140">Copy hello key toohello clipboard.</span></span>

  ![Klucz aplikacji 1][api-management-howto-aad-b2c-app-key]

11. <span data-ttu-id="622e1-142">Przełącznik wstecz toohello wydawcy portalu i Wklej hello klucza do hello **klucz tajny klienta** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="622e1-142">Switch back toohello publisher portal and paste hello key into hello **Client Secret** text box.</span></span>

  ![Klucz aplikacji 2][api-management-howto-aad-b2c-client-secret]

12. <span data-ttu-id="622e1-144">Określ nazwę domeny dzierżawy usługi Azure Active Directory B2C hello w hello **dozwolone dzierżawy**.</span><span class="sxs-lookup"><span data-stu-id="622e1-144">Specify hello domain name of hello Azure Active Directory B2C tenant in **Allowed Tenant**.</span></span>

  ![Dozwolone dzierżawy][api-management-howto-aad-b2c-allowed-tenant]

13. <span data-ttu-id="622e1-146">Określ hello **zasad rejestracji** i **zasad Signin**.</span><span class="sxs-lookup"><span data-stu-id="622e1-146">Specify hello **Signup Policy** and **Signin Policy**.</span></span> <span data-ttu-id="622e1-147">Opcjonalnie można też podać hello **zasady edycji profilu** i **zasady resetowania hasła**.</span><span class="sxs-lookup"><span data-stu-id="622e1-147">Optionally, you can also provide hello **Profile Editing Policy** and **Password Reset Policy**.</span></span>

  ![Zasady][api-management-howto-aad-b2c-policies]

  > [!NOTE]
  > <span data-ttu-id="622e1-149">Aby uzyskać więcej informacji dotyczących zasad, zobacz [usługi Azure Active Directory B2C: rozszerzona platforma zasad].</span><span class="sxs-lookup"><span data-stu-id="622e1-149">For more information on policies, see [Azure Active Directory B2C: Extensible policy framework].</span></span>

14. <span data-ttu-id="622e1-150">Po określeniu wymaganą konfiguracją powitania kliknij **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="622e1-150">After you've specified hello desired configuration, click **Save**.</span></span>

  <span data-ttu-id="622e1-151">Gdy hello zmiany zostaną zapisane, deweloperzy zostanie toocreate stanie nowych kont i logowania w portalu dla deweloperów toohello przy użyciu usługi Azure Active Directory B2C.</span><span class="sxs-lookup"><span data-stu-id="622e1-151">After hello changes are saved, developers will be able toocreate new accounts and sign in toohello developer portal by using Azure Active Directory B2C.</span></span>

## <a name="sign-up-for-a-developer-account-by-using-azure-active-directory-b2c"></a><span data-ttu-id="622e1-152">Załóż konto dewelopera przy użyciu usługi Azure Active Directory B2C</span><span class="sxs-lookup"><span data-stu-id="622e1-152">Sign up for a developer account by using Azure Active Directory B2C</span></span>

1. <span data-ttu-id="622e1-153">toosign dla konta dewelopera, za pomocą usługi Azure Active Directory B2C, Otwórz nowe okno przeglądarki i przejdź toohello portalu dla deweloperów.</span><span class="sxs-lookup"><span data-stu-id="622e1-153">toosign up for a developer account by using Azure Active Directory B2C, open a new browser window and go toohello developer portal.</span></span> <span data-ttu-id="622e1-154">Kliknij przycisk hello **Zarejestruj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="622e1-154">Click hello **Sign up** button.</span></span>

   ![Portalu dla deweloperów 1][api-management-howto-aad-b2c-dev-portal]

2. <span data-ttu-id="622e1-156">Wybierz polecenie toosign z **usługi Azure Active Directory B2C**.</span><span class="sxs-lookup"><span data-stu-id="622e1-156">Choose toosign up with **Azure Active Directory B2C**.</span></span>

   ![Portalu dla deweloperów 2][api-management-howto-aad-b2c-dev-portal-b2c-button]

3. <span data-ttu-id="622e1-158">Możesz teraz skonfigurowane w poprzedniej sekcji hello zasady rejestracji toohello przekierowane.</span><span class="sxs-lookup"><span data-stu-id="622e1-158">You're redirected toohello signup policy that you configured in hello previous section.</span></span> <span data-ttu-id="622e1-159">Wybierz toosign przy użyciu adresu e-mail lub jeden z istniejących kont społecznościowych.</span><span class="sxs-lookup"><span data-stu-id="622e1-159">Choose toosign up by using your email address or one of your existing social accounts.</span></span>

   > [!NOTE]
   > <span data-ttu-id="622e1-160">Jeśli usługi Azure Active Directory B2C jest jedyną opcją hello, który został włączony na powitania **tożsamości** kartę w portalu wydawcy hello będzie zasad rejestracji toohello przekierowane bezpośrednio.</span><span class="sxs-lookup"><span data-stu-id="622e1-160">If Azure Active Directory B2C is hello only option that's enabled on hello **Identities** tab in hello publisher portal, you'll be redirected toohello signup policy directly.</span></span>

   ![Portal dla deweloperów][api-management-howto-aad-b2c-dev-portal-b2c-options]

   <span data-ttu-id="622e1-162">Po zakończeniu rejestracji hello możesz przekierowanego toohello wstecz portalu dla deweloperów.</span><span class="sxs-lookup"><span data-stu-id="622e1-162">When hello signup is complete, you're redirected back toohello developer portal.</span></span> <span data-ttu-id="622e1-163">Obecnie zalogowano Cię w portalu dla deweloperów toohello wystąpienia usługi Zarządzanie interfejsami API.</span><span class="sxs-lookup"><span data-stu-id="622e1-163">You're now signed in toohello developer portal for your API Management service instance.</span></span>

    ![Zakończono rejestrację][api-management-registration-complete]

## <a name="next-steps"></a><span data-ttu-id="622e1-165">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="622e1-165">Next steps</span></span>

*  <span data-ttu-id="622e1-166">[Omówienie usługi Azure Active Directory B2C]</span><span class="sxs-lookup"><span data-stu-id="622e1-166">[Azure Active Directory B2C overview]</span></span>
*  <span data-ttu-id="622e1-167">[usługi Azure Active Directory B2C: rozszerzona platforma zasad]</span><span class="sxs-lookup"><span data-stu-id="622e1-167">[Azure Active Directory B2C: Extensible policy framework]</span></span>
*  <span data-ttu-id="622e1-168">[Użyj konta Microsoft jako dostawca tożsamości w usłudze Azure Active Directory B2C]</span><span class="sxs-lookup"><span data-stu-id="622e1-168">[Use a Microsoft account as an identity provider in Azure Active Directory B2C]</span></span>
*  <span data-ttu-id="622e1-169">[Użyj konta Google funkcję dostawcy tożsamości w usłudze Azure Active Directory B2C]</span><span class="sxs-lookup"><span data-stu-id="622e1-169">[Use a Google account as an identity provider in Azure Active Directory B2C]</span></span>
*  <span data-ttu-id="622e1-170">[Użyj konta LinkedIn funkcję dostawcy tożsamości w usłudze Azure Active Directory B2C]</span><span class="sxs-lookup"><span data-stu-id="622e1-170">[Use a LinkedIn account as an identity provider in Azure Active Directory B2C]</span></span>
*  <span data-ttu-id="622e1-171">[Użyj konta usługi Facebook jako dostawca tożsamości w usłudze Azure Active Directory B2C]</span><span class="sxs-lookup"><span data-stu-id="622e1-171">[Use a Facebook account as an identity provider in Azure Active Directory B2C]</span></span>




[api-management-howto-aad-b2c-security-tab]: ./media/api-management-howto-aad-b2c/api-management-b2c-security-tab.PNG
[api-management-howto-aad-b2c-security-tab-reply-url]: ./media/api-management-howto-aad-b2c/api-management-b2c-security-tab-reply-url.PNG
[api-management-howto-aad-b2c-portal-menu]: ./media/api-management-howto-aad-b2c/api-management-b2c-portal-menu.PNG
[api-management-howto-aad-b2c-add-button]: ./media/api-management-howto-aad-b2c/api-management-b2c-add-button.PNG
[api-management-howto-aad-b2c-app-details]: ./media/api-management-howto-aad-b2c/api-management-b2c-app-details.PNG
[api-management-howto-aad-b2c-app-created]: ./media/api-management-howto-aad-b2c/api-management-b2c-app-created.PNG
[api-management-howto-aad-b2c-app-id]: ./media/api-management-howto-aad-b2c/api-management-b2c-app-id.PNG
[api-management-howto-aad-b2c-client-id]: ./media/api-management-howto-aad-b2c/api-management-b2c-client-id.PNG
[api-management-howto-aad-b2c-app-key]: ./media/api-management-howto-aad-b2c/api-management-b2c-app-key.PNG
[api-management-howto-aad-b2c-app-key-saved]: ./media/api-management-howto-aad-b2c/api-management-b2c-app-key-saved.PNG
[api-management-howto-aad-b2c-client-secret]: ./media/api-management-howto-aad-b2c/api-management-b2c-client-secret.PNG
[api-management-howto-aad-b2c-allowed-tenant]: ./media/api-management-howto-aad-b2c/api-management-b2c-allowed-tenant.PNG
[api-management-howto-aad-b2c-policies]: ./media/api-management-howto-aad-b2c/api-management-b2c-policies.PNG
[api-management-howto-aad-b2c-dev-portal]: ./media/api-management-howto-aad-b2c/api-management-b2c-dev-portal.PNG
[api-management-howto-aad-b2c-dev-portal-b2c-button]: ./media/api-management-howto-aad-b2c/api-management-b2c-dev-portal-b2c-button.PNG
[api-management-howto-aad-b2c-dev-portal-b2c-options]: ./media/api-management-howto-aad-b2c/api-management-b2c-dev-portal-b2c-options.PNG
[api-management-complete-registration]: ./media/api-management-howto-aad/api-management-complete-registration.PNG
[api-management-registration-complete]: ./media/api-management-howto-aad/api-management-registration-complete.png

[api-management-management-console]: ./media/api-management-howto-aad/api-management-management-console.png
[api-management-security-external-identities]: ./media/api-management-howto-aad/api-management-b2c-security-tab.png
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
[api-management-aad-app-multi-tenant]: ./media/api-management-howto-aad/api-management-aad-app-multi-tenant.png
[api-management-aad-reply-url]: ./media/api-management-howto-aad/api-management-aad-reply-url.png
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
[Omówienie usługi Azure Active Directory B2C]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-overview
[jak tooauthorize developer kont przy użyciu narzędzia Azure Active Directory]: https://docs.microsoft.com/azure/api-management/api-management-howto-aad
[usługi Azure Active Directory B2C: rozszerzona platforma zasad]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-reference-policies
[Użyj konta Microsoft jako dostawca tożsamości w usłudze Azure Active Directory B2C]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-setup-msa-app
[Użyj konta Google funkcję dostawcy tożsamości w usłudze Azure Active Directory B2C]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-setup-goog-app
[Użyj konta usługi Facebook jako dostawca tożsamości w usłudze Azure Active Directory B2C]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-setup-fb-app
[Użyj konta LinkedIn funkcję dostawcy tożsamości w usłudze Azure Active Directory B2C]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-setup-li-app

[Prerequisites]: #prerequisites
[Configure an OAuth 2.0 authorization server in API Management]: #step1
[Configure an API toouse OAuth 2.0 user authorization]: #step2
[Test hello OAuth 2.0 user authorization in hello Developer Portal]: #step3
[Next steps]: #next-steps

[Log in toohello Developer portal using an Azure Active Directory account]: #Log-in-to-the-Developer-portal-using-an-Azure-Active-Directory-account
