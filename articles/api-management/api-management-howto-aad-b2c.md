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
# <a name="how-tooauthorize-developer-accounts-by-using-azure-active-directory-b2c-in-azure-api-management"></a>Jak tooauthorize developer kont przy użyciu narzędzia Azure Active Directory B2C w usłudze Azure API Management
## <a name="overview"></a>Omówienie
Usługa Azure Active Directory B2C jest chmury rozwiązania do zarządzania tożsamościami internetowych i aplikacji dla urządzeń przenośnych. Służy on toomanage dostępu tooyour developer portal. Ten przewodnik przedstawia hello konfiguracji, który jest wymagany w Twojej toointegrate usługi Zarządzanie interfejsami API z usługi Azure Active Directory B2C. Aby uzyskać informacje na temat włączania dostępu do portalu dla deweloperów toohello przy użyciu klasycznego Azure Active Directory, zobacz [jak tooauthorize developer kont przy użyciu narzędzia Azure Active Directory].

> [!NOTE]
> toocomplete hello kroków tego podręcznika, najpierw musisz toocreate dzierżawy usługi Azure Active Directory B2C aplikacja. Ponadto należy zasad rejestracji i logowania toohave gotowe. Aby uzyskać więcej informacji, zobacz [Omówienie usługi Azure Active Directory B2C].

## <a name="authorize-developer-accounts-by-using-azure-active-directory-b2c"></a>Autoryzowanie konta dewelopera przy użyciu usługi Azure Active Directory B2C

1. tooget pracę, kliknij przycisk **portal wydawcy** w portalu Azure usługi Zarządzanie interfejsami API hello. Trwa toohello zarządzanie interfejsami API wydawcy portalu.

   ![Portal wydawcy][api-management-management-console]

   > [!NOTE]
   > Jeśli jeszcze nie utworzono wystąpienie usługi API Management, zobacz [Utwórz wystąpienie usługi Zarządzanie interfejsami API] [ Create an API Management service instance] w hello [wprowadzenie do usługi Azure API Management samouczek][Get started with Azure API Management].

2. Na powitania **zarządzanie interfejsami API** menu, kliknij przycisk **zabezpieczeń**. Na powitania **tożsamości** , wybierz pozycję **usługi Azure Active Directory B2C**.

  ![1 tożsamości zewnętrznych][api-management-howto-aad-b2c-security-tab]

3. Zanotuj hello **adresem URL przekierowania** i przełączyć na tooAzure Active Directory B2C w portalu Azure hello.

  ![2 tożsamości zewnętrznych][api-management-howto-aad-b2c-security-tab-reply-url]

4. Kliknij przycisk hello **aplikacji** przycisku.

  ![Zarejestrować nową aplikację 1][api-management-howto-aad-b2c-portal-menu]

5. Kliknij przycisk hello **Dodaj** przycisk aplikacji toocreate nowej usługi Azure Active Directory B2C.

  ![Zarejestrować nową aplikację 2][api-management-howto-aad-b2c-add-button]

6. W hello **nowej aplikacji** bloku, wprowadź nazwę aplikacji hello. Wybierz **tak** w obszarze **interfejsu API sieci Web i aplikacji sieci Web**i wybierz polecenie **tak** w obszarze **Zezwalaj przepływu niejawnego**. Następnie hello kopiowania **adresem URL przekierowania** z hello **usługi Azure Active Directory B2C** sekcji hello **tożsamości** karcie w portalu wydawcy hello i wklej go do hello **Adres URL odpowiedzi** pola tekstowego.

  ![Zarejestrować nową aplikację 3][api-management-howto-aad-b2c-app-details]

7. Kliknij przycisk hello **Utwórz** przycisku. Po utworzeniu aplikacji hello jest wyświetlana w hello **aplikacji** bloku. Kliknij przycisk toosee Nazwa aplikacji hello jego szczegóły.

  ![Zarejestrować nową aplikację 4][api-management-howto-aad-b2c-app-created]

8. Z hello **właściwości** bloku, hello kopiowania **identyfikator aplikacji** toohello Schowka.

  ![Identyfikator aplikacji 1][api-management-howto-aad-b2c-app-id]

9. Przełącz wstecz toohello wydawcy portalu i wklej identyfikator hello w hello **identyfikator klienta** pola tekstowego.

  ![Identyfikator aplikacji 2][api-management-howto-aad-b2c-client-id]

10. Przełącz wstecz toohello portalu Azure, kliknij hello **klucze** przycisk, a następnie kliknij przycisk **generowanie klucza**. Kliknij przycisk **zapisać** hello konfiguracji oraz wyświetlania hello toosave **klucz aplikacji**. Kopiuj hello klucza toohello Schowka.

  ![Klucz aplikacji 1][api-management-howto-aad-b2c-app-key]

11. Przełącznik wstecz toohello wydawcy portalu i Wklej hello klucza do hello **klucz tajny klienta** pola tekstowego.

  ![Klucz aplikacji 2][api-management-howto-aad-b2c-client-secret]

12. Określ nazwę domeny dzierżawy usługi Azure Active Directory B2C hello w hello **dozwolone dzierżawy**.

  ![Dozwolone dzierżawy][api-management-howto-aad-b2c-allowed-tenant]

13. Określ hello **zasad rejestracji** i **zasad Signin**. Opcjonalnie można też podać hello **zasady edycji profilu** i **zasady resetowania hasła**.

  ![Zasady][api-management-howto-aad-b2c-policies]

  > [!NOTE]
  > Aby uzyskać więcej informacji dotyczących zasad, zobacz [usługi Azure Active Directory B2C: rozszerzona platforma zasad].

14. Po określeniu wymaganą konfiguracją powitania kliknij **zapisać**.

  Gdy hello zmiany zostaną zapisane, deweloperzy zostanie toocreate stanie nowych kont i logowania w portalu dla deweloperów toohello przy użyciu usługi Azure Active Directory B2C.

## <a name="sign-up-for-a-developer-account-by-using-azure-active-directory-b2c"></a>Załóż konto dewelopera przy użyciu usługi Azure Active Directory B2C

1. toosign dla konta dewelopera, za pomocą usługi Azure Active Directory B2C, Otwórz nowe okno przeglądarki i przejdź toohello portalu dla deweloperów. Kliknij przycisk hello **Zarejestruj** przycisku.

   ![Portalu dla deweloperów 1][api-management-howto-aad-b2c-dev-portal]

2. Wybierz polecenie toosign z **usługi Azure Active Directory B2C**.

   ![Portalu dla deweloperów 2][api-management-howto-aad-b2c-dev-portal-b2c-button]

3. Możesz teraz skonfigurowane w poprzedniej sekcji hello zasady rejestracji toohello przekierowane. Wybierz toosign przy użyciu adresu e-mail lub jeden z istniejących kont społecznościowych.

   > [!NOTE]
   > Jeśli usługi Azure Active Directory B2C jest jedyną opcją hello, który został włączony na powitania **tożsamości** kartę w portalu wydawcy hello będzie zasad rejestracji toohello przekierowane bezpośrednio.

   ![Portal dla deweloperów][api-management-howto-aad-b2c-dev-portal-b2c-options]

   Po zakończeniu rejestracji hello możesz przekierowanego toohello wstecz portalu dla deweloperów. Obecnie zalogowano Cię w portalu dla deweloperów toohello wystąpienia usługi Zarządzanie interfejsami API.

    ![Zakończono rejestrację][api-management-registration-complete]

## <a name="next-steps"></a>Następne kroki

*  [Omówienie usługi Azure Active Directory B2C]
*  [usługi Azure Active Directory B2C: rozszerzona platforma zasad]
*  [Użyj konta Microsoft jako dostawca tożsamości w usłudze Azure Active Directory B2C]
*  [Użyj konta Google funkcję dostawcy tożsamości w usłudze Azure Active Directory B2C]
*  [Użyj konta LinkedIn funkcję dostawcy tożsamości w usłudze Azure Active Directory B2C]
*  [Użyj konta usługi Facebook jako dostawca tożsamości w usłudze Azure Active Directory B2C]




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
