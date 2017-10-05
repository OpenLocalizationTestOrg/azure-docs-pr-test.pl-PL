---
title: "Autoryzowanie konta dewelopera przy użyciu usługi Azure Active Directory B2C - Azure API Management | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak i autoryzacji użytkowników przy użyciu usługi Azure Active Directory B2C w usłudze API Management."
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
ms.openlocfilehash: eb7deb1a79d9db9ac5cfbea69b8d3c564eb55577
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-authorize-developer-accounts-by-using-azure-active-directory-b2c-in-azure-api-management"></a><span data-ttu-id="1e368-103">Sposób autoryzowania konta dewelopera przy użyciu usługi Azure Active Directory B2C w usłudze Azure API Management</span><span class="sxs-lookup"><span data-stu-id="1e368-103">How to authorize developer accounts by using Azure Active Directory B2C in Azure API Management</span></span>
## <a name="overview"></a><span data-ttu-id="1e368-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="1e368-104">Overview</span></span>
<span data-ttu-id="1e368-105">Usługa Azure Active Directory B2C jest chmury rozwiązania do zarządzania tożsamościami internetowych i aplikacji dla urządzeń przenośnych.</span><span class="sxs-lookup"><span data-stu-id="1e368-105">Azure Active Directory B2C is a cloud identity management solution for consumer-facing web and mobile applications.</span></span> <span data-ttu-id="1e368-106">Można go użyć do zarządzania dostępem do swojego portalu dla deweloperów.</span><span class="sxs-lookup"><span data-stu-id="1e368-106">You can use it to manage access to your developer portal.</span></span> <span data-ttu-id="1e368-107">Ten przewodnik przedstawia konfigurację, która jest wymagana w usłudze API Management do integracji z usługi Azure Active Directory B2C.</span><span class="sxs-lookup"><span data-stu-id="1e368-107">This guide shows you the configuration that's required in your API Management service to integrate with Azure Active Directory B2C.</span></span> <span data-ttu-id="1e368-108">Aby uzyskać informacje na temat włączania dostępu do portalu dla deweloperów przy użyciu klasycznego Azure Active Directory, zobacz [sposób autoryzowania konta dewelopera przy użyciu usługi Azure Active Directory].</span><span class="sxs-lookup"><span data-stu-id="1e368-108">For information about enabling access to the developer portal by using classic Azure Active Directory, see [How to authorize developer accounts using Azure Active Directory].</span></span>

> [!NOTE]
> <span data-ttu-id="1e368-109">Aby wykonać kroki opisane w tym przewodniku, najpierw musi mieć dzierżawy usługi Azure Active Directory B2C, aby utworzyć aplikację w.</span><span class="sxs-lookup"><span data-stu-id="1e368-109">To complete the steps in this guide, you must first have an Azure Active Directory B2C tenant to create an application in.</span></span> <span data-ttu-id="1e368-110">Ponadto konieczne są gotowe zasady rejestracji i logowania.</span><span class="sxs-lookup"><span data-stu-id="1e368-110">Also, you need to have signup and signin policies ready.</span></span> <span data-ttu-id="1e368-111">Aby uzyskać więcej informacji, zobacz [Omówienie usługi Azure Active Directory B2C].</span><span class="sxs-lookup"><span data-stu-id="1e368-111">For more information, see [Azure Active Directory B2C overview].</span></span>

## <a name="authorize-developer-accounts-by-using-azure-active-directory-b2c"></a><span data-ttu-id="1e368-112">Autoryzowanie konta dewelopera przy użyciu usługi Azure Active Directory B2C</span><span class="sxs-lookup"><span data-stu-id="1e368-112">Authorize developer accounts by using Azure Active Directory B2C</span></span>

1. <span data-ttu-id="1e368-113">Aby rozpocząć, kliknij przycisk **portal wydawcy** w portalu Azure usługi Zarządzanie interfejsami API.</span><span class="sxs-lookup"><span data-stu-id="1e368-113">To get started, click **Publisher portal** in the Azure portal for your API Management service.</span></span> <span data-ttu-id="1e368-114">Spowoduje to przejście do portalu wydawcy usługi API Management.</span><span class="sxs-lookup"><span data-stu-id="1e368-114">This takes you to the API Management publisher portal.</span></span>

   ![Portal wydawcy][api-management-management-console]

   > [!NOTE]
   > <span data-ttu-id="1e368-116">Jeśli jeszcze nie utworzono wystąpienie usługi API Management, zobacz [Utwórz wystąpienie usługi Zarządzanie interfejsami API] [ Create an API Management service instance] w [Wprowadzenie — samouczek usługi Azure API Management][Get started with Azure API Management].</span><span class="sxs-lookup"><span data-stu-id="1e368-116">If you haven't yet created an API Management service instance, see [Create an API Management service instance][Create an API Management service instance] in the [Get started with Azure API Management tutorial][Get started with Azure API Management].</span></span>

2. <span data-ttu-id="1e368-117">Na **zarządzanie interfejsami API** menu, kliknij przycisk **zabezpieczeń**.</span><span class="sxs-lookup"><span data-stu-id="1e368-117">On the **API Management** menu, click **Security**.</span></span> <span data-ttu-id="1e368-118">Na **tożsamości** , wybierz pozycję **usługi Azure Active Directory B2C**.</span><span class="sxs-lookup"><span data-stu-id="1e368-118">On the **Identities** tab, choose **Azure Active Directory B2C**.</span></span>

  ![1 tożsamości zewnętrznych][api-management-howto-aad-b2c-security-tab]

3. <span data-ttu-id="1e368-120">Zanotuj **adresem URL przekierowania** i przełączyć się do usługi Azure Active Directory B2C w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="1e368-120">Make a note of the **Redirect URL** and switch over to Azure Active Directory B2C in the Azure portal.</span></span>

  ![2 tożsamości zewnętrznych][api-management-howto-aad-b2c-security-tab-reply-url]

4. <span data-ttu-id="1e368-122">Kliknij przycisk **aplikacji** przycisku.</span><span class="sxs-lookup"><span data-stu-id="1e368-122">Click the **Applications** button.</span></span>

  ![Zarejestrować nową aplikację 1][api-management-howto-aad-b2c-portal-menu]

5. <span data-ttu-id="1e368-124">Kliknij przycisk **Dodaj** przycisk, aby utworzyć nową aplikację usługi Azure Active Directory B2C.</span><span class="sxs-lookup"><span data-stu-id="1e368-124">Click the **Add** button to create a new Azure Active Directory B2C application.</span></span>

  ![Zarejestrować nową aplikację 2][api-management-howto-aad-b2c-add-button]

6. <span data-ttu-id="1e368-126">W **nowej aplikacji** bloku, wprowadź nazwę aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1e368-126">In the **New application** blade, enter a name for the application.</span></span> <span data-ttu-id="1e368-127">Wybierz **tak** w obszarze **interfejsu API sieci Web i aplikacji sieci Web**i wybierz polecenie **tak** w obszarze **Zezwalaj przepływu niejawnego**.</span><span class="sxs-lookup"><span data-stu-id="1e368-127">Choose **Yes** under **Web App/Web API**, and choose **Yes** under **Allow implicit flow**.</span></span> <span data-ttu-id="1e368-128">Następnie skopiuj **adresem URL przekierowania** z **usługi Azure Active Directory B2C** sekcji **tożsamości** w portalu wydawcy, a następnie wklej ją do **adres URL odpowiedzi** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="1e368-128">Then copy the **Redirect URL** from the **Azure Active Directory B2C** section of the **Identities** tab in the publisher portal, and paste it into the **Reply URL** text box.</span></span>

  ![Zarejestrować nową aplikację 3][api-management-howto-aad-b2c-app-details]

7. <span data-ttu-id="1e368-130">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="1e368-130">Click the **Create** button.</span></span> <span data-ttu-id="1e368-131">Po utworzeniu aplikacji jest wyświetlany w **aplikacji** bloku.</span><span class="sxs-lookup"><span data-stu-id="1e368-131">When the application is created, it appears in the **Applications** blade.</span></span> <span data-ttu-id="1e368-132">Kliknij nazwę aplikacji, aby wyświetlić jego szczegóły.</span><span class="sxs-lookup"><span data-stu-id="1e368-132">Click the application name to see its details.</span></span>

  ![Zarejestrować nową aplikację 4][api-management-howto-aad-b2c-app-created]

8. <span data-ttu-id="1e368-134">Z **właściwości** bloku, kopiowania **identyfikator aplikacji** do Schowka.</span><span class="sxs-lookup"><span data-stu-id="1e368-134">From the **Properties** blade, copy the **Application ID** to the clipboard.</span></span>

  ![Identyfikator aplikacji 1][api-management-howto-aad-b2c-app-id]

9. <span data-ttu-id="1e368-136">Przełączyć się do portalu wydawcy i wklej identyfikator do **identyfikator klienta** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="1e368-136">Switch back to the publisher portal and paste the ID into the **Client Id** text box.</span></span>

  ![Identyfikator aplikacji 2][api-management-howto-aad-b2c-client-id]

10. <span data-ttu-id="1e368-138">Wrócić do portalu Azure, kliknij przycisk **klucze** przycisk, a następnie kliknij przycisk **generowanie klucza**.</span><span class="sxs-lookup"><span data-stu-id="1e368-138">Switch back to the Azure portal, click the **Keys** button, and then click **Generate key**.</span></span> <span data-ttu-id="1e368-139">Kliknij przycisk **zapisać** Aby zapisać konfigurację i wyświetlić **klucz aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="1e368-139">Click **Save** to save the configuration and display the **App key**.</span></span> <span data-ttu-id="1e368-140">Skopiuj klucz do Schowka.</span><span class="sxs-lookup"><span data-stu-id="1e368-140">Copy the key to the clipboard.</span></span>

  ![Klucz aplikacji 1][api-management-howto-aad-b2c-app-key]

11. <span data-ttu-id="1e368-142">Przełączyć się do portalu wydawcy i Wklej klucz do **klucz tajny klienta** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="1e368-142">Switch back to the publisher portal and paste the key into the **Client Secret** text box.</span></span>

  ![Klucz aplikacji 2][api-management-howto-aad-b2c-client-secret]

12. <span data-ttu-id="1e368-144">Określ nazwę domeny dzierżawy usługi Azure Active Directory B2C w **dozwolone dzierżawy**.</span><span class="sxs-lookup"><span data-stu-id="1e368-144">Specify the domain name of the Azure Active Directory B2C tenant in **Allowed Tenant**.</span></span>

  ![Dozwolone dzierżawy][api-management-howto-aad-b2c-allowed-tenant]

13. <span data-ttu-id="1e368-146">Określ **zasad rejestracji** i **zasad Signin**.</span><span class="sxs-lookup"><span data-stu-id="1e368-146">Specify the **Signup Policy** and **Signin Policy**.</span></span> <span data-ttu-id="1e368-147">Opcjonalnie można też podać **zasady edycji profilu** i **zasady resetowania hasła**.</span><span class="sxs-lookup"><span data-stu-id="1e368-147">Optionally, you can also provide the **Profile Editing Policy** and **Password Reset Policy**.</span></span>

  ![Zasady][api-management-howto-aad-b2c-policies]

  > [!NOTE]
  > <span data-ttu-id="1e368-149">Aby uzyskać więcej informacji dotyczących zasad, zobacz [usługi Azure Active Directory B2C: rozszerzona platforma zasad].</span><span class="sxs-lookup"><span data-stu-id="1e368-149">For more information on policies, see [Azure Active Directory B2C: Extensible policy framework].</span></span>

14. <span data-ttu-id="1e368-150">Po określeniu odpowiednią konfigurację, kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="1e368-150">After you've specified the desired configuration, click **Save**.</span></span>

  <span data-ttu-id="1e368-151">Po zapisaniu zmian deweloperzy będzie mógł tworzyć nowych kont i zaloguj się do portalu dla deweloperów przy użyciu usługi Azure Active Directory B2C.</span><span class="sxs-lookup"><span data-stu-id="1e368-151">After the changes are saved, developers will be able to create new accounts and sign in to the developer portal by using Azure Active Directory B2C.</span></span>

## <a name="sign-up-for-a-developer-account-by-using-azure-active-directory-b2c"></a><span data-ttu-id="1e368-152">Załóż konto dewelopera przy użyciu usługi Azure Active Directory B2C</span><span class="sxs-lookup"><span data-stu-id="1e368-152">Sign up for a developer account by using Azure Active Directory B2C</span></span>

1. <span data-ttu-id="1e368-153">Aby utworzyć konto dewelopera przy użyciu usługi Azure Active Directory B2C, Otwórz nowe okno przeglądarki i przejdź do portalu dla deweloperów.</span><span class="sxs-lookup"><span data-stu-id="1e368-153">To sign up for a developer account by using Azure Active Directory B2C, open a new browser window and go to the developer portal.</span></span> <span data-ttu-id="1e368-154">Kliknij przycisk **Zarejestruj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="1e368-154">Click the **Sign up** button.</span></span>

   ![Portalu dla deweloperów 1][api-management-howto-aad-b2c-dev-portal]

2. <span data-ttu-id="1e368-156">Wybierz konto z **usługi Azure Active Directory B2C**.</span><span class="sxs-lookup"><span data-stu-id="1e368-156">Choose to sign up with **Azure Active Directory B2C**.</span></span>

   ![Portalu dla deweloperów 2][api-management-howto-aad-b2c-dev-portal-b2c-button]

3. <span data-ttu-id="1e368-158">Możesz są przekierowywane do zasad rejestracji, skonfigurowanego w poprzedniej sekcji.</span><span class="sxs-lookup"><span data-stu-id="1e368-158">You're redirected to the signup policy that you configured in the previous section.</span></span> <span data-ttu-id="1e368-159">Wybierz utworzyć konto przy użyciu adresu e-mail lub jeden z istniejących kont społecznościowych.</span><span class="sxs-lookup"><span data-stu-id="1e368-159">Choose to sign up by using your email address or one of your existing social accounts.</span></span>

   > [!NOTE]
   > <span data-ttu-id="1e368-160">Jeśli usługi Azure Active Directory B2C jest jedyną opcją jest włączona na **tożsamości** kartę w portalu wydawcy użytkownik zostanie przekierowany do zasad rejestracji bezpośrednio.</span><span class="sxs-lookup"><span data-stu-id="1e368-160">If Azure Active Directory B2C is the only option that's enabled on the **Identities** tab in the publisher portal, you'll be redirected to the signup policy directly.</span></span>

   ![Portal dla deweloperów][api-management-howto-aad-b2c-dev-portal-b2c-options]

   <span data-ttu-id="1e368-162">Po zakończeniu rejestracja jest przekierowany do portalu dla deweloperów.</span><span class="sxs-lookup"><span data-stu-id="1e368-162">When the signup is complete, you're redirected back to the developer portal.</span></span> <span data-ttu-id="1e368-163">Obecnie zalogowano Cię do portalu dla deweloperów wystąpienia usługi Zarządzanie interfejsami API.</span><span class="sxs-lookup"><span data-stu-id="1e368-163">You're now signed in to the developer portal for your API Management service instance.</span></span>

    ![Zakończono rejestrację][api-management-registration-complete]

## <a name="next-steps"></a><span data-ttu-id="1e368-165">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="1e368-165">Next steps</span></span>

*  <span data-ttu-id="1e368-166">[Omówienie usługi Azure Active Directory B2C]</span><span class="sxs-lookup"><span data-stu-id="1e368-166">[Azure Active Directory B2C overview]</span></span>
*  <span data-ttu-id="1e368-167">[usługi Azure Active Directory B2C: rozszerzona platforma zasad]</span><span class="sxs-lookup"><span data-stu-id="1e368-167">[Azure Active Directory B2C: Extensible policy framework]</span></span>
*  <span data-ttu-id="1e368-168">[Użyj konta Microsoft jako dostawca tożsamości w usłudze Azure Active Directory B2C]</span><span class="sxs-lookup"><span data-stu-id="1e368-168">[Use a Microsoft account as an identity provider in Azure Active Directory B2C]</span></span>
*  <span data-ttu-id="1e368-169">[Użyj konta Google funkcję dostawcy tożsamości w usłudze Azure Active Directory B2C]</span><span class="sxs-lookup"><span data-stu-id="1e368-169">[Use a Google account as an identity provider in Azure Active Directory B2C]</span></span>
*  <span data-ttu-id="1e368-170">[Użyj konta LinkedIn funkcję dostawcy tożsamości w usłudze Azure Active Directory B2C]</span><span class="sxs-lookup"><span data-stu-id="1e368-170">[Use a LinkedIn account as an identity provider in Azure Active Directory B2C]</span></span>
*  <span data-ttu-id="1e368-171">[Użyj konta usługi Facebook jako dostawca tożsamości w usłudze Azure Active Directory B2C]</span><span class="sxs-lookup"><span data-stu-id="1e368-171">[Use a Facebook account as an identity provider in Azure Active Directory B2C]</span></span>




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
<span data-ttu-id="1e368-172">[Omówienie usługi Azure Active Directory B2C]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-overview</span><span class="sxs-lookup"><span data-stu-id="1e368-172">[Azure Active Directory B2C overview]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-overview</span></span>
<span data-ttu-id="1e368-173">[sposób autoryzowania konta dewelopera przy użyciu usługi Azure Active Directory]: https://docs.microsoft.com/azure/api-management/api-management-howto-aad</span><span class="sxs-lookup"><span data-stu-id="1e368-173">[How to authorize developer accounts using Azure Active Directory]: https://docs.microsoft.com/azure/api-management/api-management-howto-aad</span></span>
<span data-ttu-id="1e368-174">[usługi Azure Active Directory B2C: rozszerzona platforma zasad]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-reference-policies</span><span class="sxs-lookup"><span data-stu-id="1e368-174">[Azure Active Directory B2C: Extensible policy framework]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-reference-policies</span></span>
<span data-ttu-id="1e368-175">[Użyj konta Microsoft jako dostawca tożsamości w usłudze Azure Active Directory B2C]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-setup-msa-app</span><span class="sxs-lookup"><span data-stu-id="1e368-175">[Use a Microsoft account as an identity provider in Azure Active Directory B2C]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-setup-msa-app</span></span>
<span data-ttu-id="1e368-176">[Użyj konta Google funkcję dostawcy tożsamości w usłudze Azure Active Directory B2C]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-setup-goog-app</span><span class="sxs-lookup"><span data-stu-id="1e368-176">[Use a Google account as an identity provider in Azure Active Directory B2C]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-setup-goog-app</span></span>
<span data-ttu-id="1e368-177">[Użyj konta usługi Facebook jako dostawca tożsamości w usłudze Azure Active Directory B2C]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-setup-fb-app</span><span class="sxs-lookup"><span data-stu-id="1e368-177">[Use a Facebook account as an identity provider in Azure Active Directory B2C]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-setup-fb-app</span></span>
<span data-ttu-id="1e368-178">[Użyj konta LinkedIn funkcję dostawcy tożsamości w usłudze Azure Active Directory B2C]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-setup-li-app</span><span class="sxs-lookup"><span data-stu-id="1e368-178">[Use a LinkedIn account as an identity provider in Azure Active Directory B2C]: https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-setup-li-app</span></span>

[Prerequisites]: #prerequisites
[Configure an OAuth 2.0 authorization server in API Management]: #step1
[Configure an API to use OAuth 2.0 user authorization]: #step2
[Test the OAuth 2.0 user authorization in the Developer Portal]: #step3
[Next steps]: #next-steps

[Log in to the Developer portal using an Azure Active Directory account]: #Log-in-to-the-Developer-portal-using-an-Azure-Active-Directory-account
