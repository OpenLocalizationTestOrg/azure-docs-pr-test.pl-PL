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
# <a name="how-tooauthorize-developer-accounts-using-azure-active-directory-in-azure-api-management"></a>Jak tooauthorize developer kont przy użyciu narzędzia Azure Active Directory w usłudze Azure API Management
## <a name="overview"></a>Omówienie
Ten przewodnik przedstawia, jak tooenable uzyskują dostęp do portalu dla deweloperów toohello dla użytkowników z usługi Azure Active Directory. W tym przewodniku także przedstawiono sposób toomanage grupy użytkowników usługi Azure Active Directory przez dodanie zewnętrznego grup, które zawierają hello użytkowników usługi Azure Active Directory.

> Witaj toocomplete kroków w tym przewodniku musi działać usługa Azure Active Directory w których toocreate aplikacji.
> 
> 

## <a name="how-tooauthorize-developer-accounts-using-azure-active-directory"></a>Jak tooauthorize developer kont przy użyciu narzędzia Azure Active Directory
tooget pracę, kliknij przycisk **portal wydawcy** w portalu Azure usługi Zarządzanie interfejsami API hello. Trwa toohello zarządzanie interfejsami API wydawcy portalu.

![Portal wydawcy][api-management-management-console]

> Jeśli jeszcze nie utworzono wystąpienie usługi API Management, zobacz [Utwórz wystąpienie usługi Zarządzanie interfejsami API] [ Create an API Management service instance] w hello [wprowadzenie do usługi Azure API Management] [ Get started with Azure API Management] samouczka.
> 
> 

Kliknij przycisk **zabezpieczeń** z hello **zarządzanie interfejsami API** menu po lewej stronie powitania oraz kliknij **tożsamości zewnętrznych**.

![Tożsamości zewnętrznych][api-management-security-external-identities]

Kliknij przycisk **usługi Azure Active Directory**. Zanotuj hello **adresem URL przekierowania** i przełączyć na tooyour usługi Azure Active Directory w hello klasycznego portalu Azure.

![Tożsamości zewnętrznych][api-management-security-aad-new]

Kliknij przycisk hello **Dodaj** przycisk toocreate nową aplikację usługi Azure Active Directory, a następnie wybierz pozycję **Dodaj aplikację moją organizację**.

![Dodaj nową aplikację usługi Azure Active Directory][api-management-new-aad-application-menu]

Wprowadź nazwę aplikacji hello, wybierz pozycję **sieci Web, aplikacji i/lub interfejs API sieci Web**i kliknij przycisk Dalej hello.

![Nową aplikację usługi Azure Active Directory][api-management-new-aad-application-1]

Aby uzyskać **adres URL logowania**, wprowadź hello jednokrotnej adres URL swojego portalu dla deweloperów. W tym przykładzie hello **adres URL logowania** jest `https://aad03.portal.current.int-azure-api.net/signin`. 

Dla hello **adres URL Identyfikatora aplikacji**, wprowadź hello domyślnej domeny i domeny niestandardowej dla hello Azure Active Directory i Dołącz tooit unikatowy ciąg. W tym przykładzie hello domyślnej domeny **https://contoso5api.onmicrosoft.com** jest używana z sufiksem hello **/api** określony.

![Nowe właściwości aplikacji usługi Azure Active Directory][api-management-new-aad-application-2]

Kliknij toosave przycisk wyboru hello i tworzenie aplikacji hello i przełączyć toohello **Konfiguruj** karcie tooconfigure hello nowej aplikacji.

![Nowej aplikacji usługi Azure Active Directory][api-management-new-aad-app-created]

Jeśli wiele katalogów Active Azure będą toobe używany dla tej aplikacji, kliknij przycisk **tak** dla **aplikacji jest wielodostępne**. Domyślnie Hello **nr**.

![Aplikacja jest wieloma dzierżawcami][api-management-aad-app-multi-tenant]

Kopiuj hello **adresem URL przekierowania** z hello **usługi Azure Active Directory** sekcji hello **tożsamości zewnętrznych** w portalu wydawcy hello i wklej go do hello **Adres URL odpowiedzi** pola tekstowego. 

![Adres URL odpowiedzi][api-management-aad-reply-url]

Przewiń w dół toohello hello skonfigurować kartę, zaznacz hello **uprawnienia aplikacji** listy rozwijanej i sprawdź **odczytuj dane katalogu**.

![Uprawnienia aplikacji][api-management-aad-app-permissions]

Wybierz hello **delegowanie uprawnień** listy rozwijanej i sprawdź **włączenia logowania jednokrotnego i odczytu profilów użytkowników**.

![Delegowane uprawnienia][api-management-aad-delegated-permissions]

> Aby uzyskać więcej informacji o aplikacji i uprawnień delegowanych, zobacz [hello dostęp do interfejsu API programu Graph][Accessing hello Graph API].
> 
> 

Kopiuj hello **identyfikator klienta** toohello Schowka.

![Identyfikator klienta][api-management-aad-app-client-id]

Przełącz wstecz toohello wydawcy portalu i Wklej w hello **identyfikator klienta** skopiowanych z konfiguracji aplikacji hello Azure Active Directory.

![Identyfikator klienta][api-management-client-id]

Konfiguracji usługi Azure Active Directory toohello tyłu przełącznika, a następnie kliknij przycisk hello **wybierz czas trwania** listy rozwijanej w hello **klucze** sekcji i określ interwał. W tym przykładzie **1 rok** jest używany.

![Klucz][api-management-aad-key-before-save]

Kliknij przycisk **zapisać** toosave hello konfiguracji oraz wyświetlania hello klucza. Kopiuj hello klucza toohello Schowka.

> Zanotuj tego klucza. Po zamknięciu okna konfiguracji usługi Azure Active Directory hello hello klucza nie może ponownie wyświetlone.
> 
> 

![Klucz][api-management-aad-key-after-save]

Przełącznik wstecz toohello wydawcy portalu i Wklej hello klucza do hello **klucz tajny klienta** pola tekstowego.

![Klucz tajny klienta][api-management-client-secret]

**Dozwolone dzierżaw** Określa, które katalogi mają toohello dostępu do interfejsów API wystąpienia usługi Zarządzanie interfejsami API hello. Określ hello domen hello program toogrant access toowhich wystąpienia usługi Azure Active Directory. Wiele domen można oddzielić newlines, spacjami lub przecinkami.

![Dozwolone dzierżawcy][api-management-client-allowed-tenants]


Po hello potrzeby określana jest konfiguracja, kliknij przycisk **zapisać**.

![Zapisz][api-management-client-allowed-tenants-save]

Po hello zmiany zostaną zapisane, użytkownicy hello hello określone usługi Azure Active Directory można Zaloguj się w portalu dla deweloperów toohello wykonując kroki hello w [Zaloguj się przy użyciu konta usługi Azure Active Directory portalu dla deweloperów toohello] [Log in toohello Developer portal using an Azure Active Directory account].

Można określić wiele domen w hello **dozwolone dzierżaw** sekcji. Przed każdy użytkownik może zalogować się z innej domeny niż domena oryginalnego hello rejestracji aplikacji hello, administrator globalny innej domeny hello musi udzielić uprawnień tooaccess aplikacji hello dane katalogu. uprawnienie toogrant administratora globalnego hello powinien pojawiać się zbyt`https://<URL of your developer portal>/aadadminconsent` (na przykład https://contoso.portal.azure-api.net/aadadminconsent), typ w nazwie domeny hello hello mają toogive tooand dostęp do dzierżawy usługi Active Directory kliknij przycisk Prześlij. W następujących hello przykład, administrator globalny `miaoaad.onmicrosoft.com` próbuje toogive uprawnienia toothis określonego developer portal. 

![Uprawnienia][api-management-aad-consent]

W następnym ekranie powitania administratora globalnego hello będzie tooconfirm zostanie wyświetlony monit o nadanie uprawnień hello. 

![Uprawnienia][api-management-permissions-form]

> Jeśli administrator globalny nie próbuje toolog w przed uprawnienia przyznane przez administratora globalnego, hello próba logowania nie powiedzie się i zostanie wyświetlony komunikat o błędzie.
> 
> 

## <a name="how-tooadd-an-external-azure-active-directory-group"></a>Jak tooadd zewnętrznych usługi Azure Active Directory grupy
Po włączeniu dostępu dla użytkowników w usłudze Azure Active Directory, można dodać grupy usługi Azure Active Directory do usługi API Management toomore łatwe zarządzanie skojarzenia hello deweloperów hello w grupie hello z produktami hello potrzebne.

> tooconfigure zewnętrznych Azure grupy usługi Active Directory, hello Azure Active Directory należy najpierw skonfigurować na karcie tożsamości hello wykonując procedurę hello w poprzedniej sekcji hello. 
> 
> 

Zewnętrzne grup usługi Azure Active Directory są dodawane z hello **widoczność** kartę hello produktu, dla którego chcesz toogrant dostępu toohello grupy. Kliknij przycisk **produktów**, a następnie kliknij nazwę hello hello żądaną produktu.

![Konfigurowanie produktu][api-management-configure-product]

Przełącz toohello **widoczność** , a następnie kliknij pozycję **Dodawanie grup z usługi Azure Active Directory**.

![Dodaj grupy][api-management-add-groups]

Wybierz hello **Azure Active Directory dzierżawy** z listy rozwijanej hello, a następnie nazwę hello typu hello odpowiednią grupę w hello **grup** toobe dodać pola tekstowego.

![Wybierz grupę][api-management-select-group]

Ta nazwa grupy można znaleźć w hello **grup** lista dla usługi Azure Active Directory, jak pokazano w hello poniższy przykład.

![Lista grup usługi Azure Active Directory][api-management-aad-groups-list]

Kliknij przycisk **Dodaj** toovalidate hello Nazwa grupy i Dodaj grupę hello. W tym przykładzie hello **deweloperzy 5 Contoso** jest dodana grupa zewnętrzna. 

![Grupy dodane][api-management-aad-group-added]

Kliknij przycisk **zapisać** toosave hello nowe wybranej grupy.

Po grupy usługi Azure Active Directory została skonfigurowana z jednego produktu, jest dostępny toobe zaznaczone na powitania **widoczność** kartę hello innych produktów w wystąpieniu usługi Zarządzanie interfejsami API hello.

tooreview i skonfigurować właściwości hello zewnętrznych grup po zostały dodane, kliknij nazwę hello hello grupy z hello **grup** kartę.

![Zarządzanie grupami][api-management-groups]

W tym miejscu można edytować hello **nazwa** i hello **opis** hello grupy.

![Edytowanie grupy][api-management-edit-group]

Użytkownikom hello skonfigurowane usługi Azure Active Directory można zarejestrować się w portalu dla deweloperów toohello i widoku i subskrybowania tooany grup, do których mają widoczność, wykonując instrukcje hello hello następujących sekcji.

## <a name="how-toolog-in-toohello-developer-portal-using-an-azure-active-directory-account"></a>Jak toolog w portalu dla deweloperów toohello przy użyciu konta usługi Azure Active Directory
toolog w portalu dla deweloperów hello przy użyciu konta usługi Azure Active Directory skonfigurowanych w poprzednich sekcjach hello, Otwórz nowe okno przeglądarki, za pomocą hello **adres URL logowania** z konfiguracji aplikacji hello usługi Active Directory, a następnie kliknij przycisk **Usługi azure Active Directory**.

![Portalu dla deweloperów][api-management-dev-portal-signin]

Wprowadź poświadczenia hello jednego hello użytkowników w usłudze Azure Active Directory, a następnie kliknij przycisk **Zaloguj**.

![Logowanie][api-management-aad-signin]

Może pojawić się prośba o formularz rejestracji Jeśli żadnych dodatkowych informacji jest wymagane. Wypełnij formularz rejestracji hello i kliknij przycisk **Zarejestruj**.

![Rejestracja][api-management-complete-registration]

Użytkownika jest teraz zalogowany do portalu dla deweloperów hello wystąpienia usługi Zarządzanie interfejsami API.

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

