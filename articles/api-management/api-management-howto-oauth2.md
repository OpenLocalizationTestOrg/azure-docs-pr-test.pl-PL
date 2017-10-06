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
# <a name="how-tooauthorize-developer-accounts-using-oauth-20-in-azure-api-management"></a>Jak kont przy użyciu narzędzia Projektant tooauthorize OAuth 2.0 w usłudze Azure API Management
Obsługuje wiele interfejsów API [OAuth 2.0](http://oauth.net/2/) toosecure hello interfejsu API i upewnij się, że tylko prawidłowe użytkownicy mają dostęp, i ich tylko dostęp do zasobów toowhich one są uprawnione. W kolejności toouse Azure API Management w interakcyjne konsoli dewelopera z tych interfejsów API usługi hello pozwala tooconfigure Twojego toowork wystąpienia usługi z Twojej OAuth 2.0 włączone interfejsu API.

## <a name="prerequisites"></a>Wymagania wstępne
W tym przewodniku przedstawiono sposób tooconfigure Twojego toouse wystąpienia usługi Zarządzanie interfejsami API autoryzacji OAuth 2.0 dla deweloperów kont, ale nie są wyświetlane jak dostawca tooconfigure OAuth 2.0. Witaj konfiguracji dla każdego protokołu OAuth 2.0 dostawcy jest inny, mimo że hello kroki są podobne, a hello wymagane informacje używane do konfigurowania protokołu OAuth 2.0 w wystąpieniu usługi API Management jest hello takie same. W tym temacie przedstawiono przykłady użycia usługi Azure Active Directory jako dostawcy uwierzytelniania OAuth 2.0.

> [!NOTE]
> Aby uzyskać więcej informacji na temat konfigurowania uwierzytelniania OAuth 2.0 przy użyciu usługi Azure Active Directory, zobacz hello [aplikacji sieci Web-GraphAPI-DotNet] [ WebApp-GraphAPI-DotNet] próbki.
> 
> 

## <a name="step1"></a>Skonfigurować serwer autoryzacji OAuth 2.0 w zarządzanie interfejsami API
tooget pracę, kliknij przycisk **portal wydawcy** w hello portalu Azure usługi Zarządzanie interfejsami API.

![Portal wydawcy][api-management-management-console]

> [!NOTE]
> Jeśli jeszcze nie utworzono wystąpienie usługi API Management, zobacz [Utwórz wystąpienie usługi Zarządzanie interfejsami API] [ Create an API Management service instance] w hello [wprowadzenie do usługi Azure API Management] [ Get started with Azure API Management] samouczka.
> 
> 

Kliknij przycisk **zabezpieczeń** z hello **zarządzanie interfejsami API** menu po lewej stronie, kliknij hello **OAuth 2.0**, a następnie kliknij przycisk **serwera autoryzacji Dodaj**.

![Uwierzytelnianie OAuth 2.0][api-management-oauth2]

Po kliknięciu przycisku **serwera autoryzacji Dodaj**, zostanie wyświetlony nowy formularz serwera autoryzacji hello.

![Nowy serwer][api-management-oauth2-server-1]

Wprowadź nazwę i opcjonalny opis w hello **nazwa** i **opis** pola. 

> [!NOTE]
> Te pola są używane tooidentify serwera autoryzacji hello OAuth 2.0 w ramach bieżącego wystąpienia usługi Zarządzanie interfejsami API hello i ich wartości nie pochodzą z serwera hello OAuth 2.0.
> 
> 

Wprowadź hello **adres URL strony rejestracji klienta**. Ta strona jest, gdzie użytkownicy mogą tworzyć i zarządzać ich kont i może być różna w zależności od dostawcy hello OAuth 2.0 używane. Witaj **adres URL strony rejestracji klienta** punktów toohello strony przez użytkowników, można użyć toocreate i skonfiguruj swoje własne konta dla dostawcy OAuth 2.0, które obsługują zarządzanie kontami użytkowników. Niektóre organizacje nie Konfiguruj lub korzystać z tej funkcji, nawet jeśli obsługuje dostawcy hello OAuth 2.0. Jeśli dostawcy OAuth 2.0 nie zarządzania skonfigurowano kont użytkownika, wprowadź symbolu zastępczego adresu URL w tym miejscu, takie jak adres URL hello firmy, lub takie jak `https://placeholder.contoso.com`.

Następna sekcja Hello hello formularza zawiera hello **typy przydziałów kod autoryzacji**, **adres URL punktu końcowego autoryzacji**, i **metoda żądania autoryzacji** ustawienia.

![Nowy serwer][api-management-oauth2-server-2]

Określ hello **typy przydziałów kod autoryzacji** sprawdzając hello żądanego typu. **Kod autoryzacji** jest określony, domyślnie.

Wprowadź hello **adres URL punktu końcowego autoryzacji**. Dla usługi Azure Active Directory, ten adres URL będzie podobne toohello następującego adresu URL, gdzie `<client_id>` jest zastępowany hello identyfikatora klienta, który identyfikuje serwer aplikacji toohello OAuth 2.0.

`https://login.microsoftonline.com/<client_id>/oauth2/authorize`

Witaj **metoda żądania autoryzacji** określa sposób przesyłania żądania autoryzacji powitania serwera toohello OAuth 2.0. Domyślnie **UZYSKAĆ** jest zaznaczone.

Następna sekcja Hello jest gdzie hello **tokenu końcowego adresu URL**, **metody uwierzytelniania klienta**, **token dostępu wysyłania — metoda**, i **zakresudomyślnego** zostały określone.

![Nowy serwer][api-management-oauth2-server-3]

W przypadku serwera usługi Azure Active Directory OAuth 2.0 hello **tokenu końcowego adresu URL** będą miały hello zgodny z formatem, gdzie `<APPID>` ma hello format `yourapp.onmicrosoft.com`.

`https://login.microsoftonline.com/<APPID>/oauth2/token`

Hello domyślne ustawienie dla **metody uwierzytelniania klienta** jest **podstawowe**, i **token dostępu metody wysyłania** jest **nagłówek autoryzacji**. Te wartości są skonfigurowane w tej sekcji formularza hello, wraz z hello **zakresu domyślnego**.

Witaj **poświadczeń klienta** sekcja zawiera hello **identyfikator klienta** i **klucz tajny klienta**, które są uzyskiwane podczas procesu tworzenia i konfiguracji hello użytkownika OAuth 2.0 serwer. Raz hello **identyfikator klienta** i **klucz tajny klienta** są określone, hello **redirect_uri** dla hello **kod autoryzacji** jest generowany. Ten identyfikator URI jest adres URL odpowiedzi hello tooconfigure używane w konfiguracji serwera OAuth 2.0.

![Nowy serwer][api-management-oauth2-server-4]

Jeśli **typy przydziałów kod autoryzacji** ustawiono zbyt**hasło właściciela zasobów**, hello **poświadczenia hasła właściciela zasobu** sekcja jest używane toospecify te poświadczenia; w przeciwnym razie można pozostawić on pusty.

![Nowy serwer][api-management-oauth2-server-5]

Po zakończeniu formularza powitania kliknij **zapisać** toosave hello interfejsu API zarządzania OAuth 2.0 autoryzacji serwera konfiguracji. Po zapisaniu hello konfiguracji serwera można skonfigurować toouse interfejsów API tej konfiguracji, jak pokazano w następnej sekcji hello.

## <a name="step2"></a>Skonfigurować toouse interfejsu API autoryzacji użytkownika OAuth 2.0
Kliknij przycisk **interfejsów API** z hello **zarządzanie interfejsami API** menu na powitania po lewej, kliknij nazwę hello hello żądanego interfejsu API, kliknij przycisk **zabezpieczeń**, a następnie sprawdź pole hello **OAuth 2.0**.

![Uwierzytelnianie użytkownika][api-management-user-authorization]

Wybierz hello potrzeby **serwera autoryzacji** z listy rozwijanej hello, a następnie kliknij przycisk **zapisać**.

![Uwierzytelnianie użytkownika][api-management-user-authorization-save]

## <a name="step3"></a>Testowanie autoryzacji użytkownika hello OAuth 2.0 w hello portalu dla deweloperów
Po skonfigurowaniu serwera autoryzacji OAuth 2.0 i skonfigurowana z toouse interfejsu API serwera, przetestować go, przechodząc toohello portalu dla deweloperów i wywoływanie interfejsu API.  Kliknij przycisk **portalu dla deweloperów** w menu u góry prawo hello.

![Portal dla deweloperów][api-management-developer-portal-menu]

Kliknij przycisk **interfejsów API** w menu u góry hello i wybierz **Echo API**.

![Interfejs Echo API][api-management-apis-echo-api]

> [!NOTE]
> Jeśli masz tylko jeden interfejs API skonfigurowane lub tooyour widoczne konta, klikając interfejsów API przejście bezpośrednio toohello operacji dla tego interfejsu API.
> 
> 

Wybierz hello **UZYSKAĆ zasobu** operacji, kliknij przycisk **Otwórz konsolę**, a następnie wybierz **kod autoryzacji** z listy rozwijanej hello.

![Otwarta konsola][api-management-open-console]

Gdy **kod autoryzacji** jest zaznaczona, wyskakujące okienko zostanie wyświetlony z hello logowania w formie dostawcy hello OAuth 2.0. W tym przykładzie hello logowania w formularzu są udostępniane przez usługi Azure Active Directory.

> [!NOTE]
> Jeśli masz wyskakujące okienka wyłączone, będzie monitowany tooenable ich hello przeglądarki. Po włączeniu je wybrać **kod autoryzacji** ponownie i hello formularz logowania będzie wyświetlany.
> 
> 

![Logowanie][api-management-oauth2-signin]

Po zalogowaniu się hello **nagłówki żądań** są wypełniane przy użyciu `Authorization : Bearer` autoryzuje żądanie hello nagłówek.

![Token nagłówka żądania][api-management-request-header-token]

W tym momencie możesz skonfigurować wartości hello potrzeby hello pozostałe parametry i przesłać Żądanie hello. 

## <a name="next-steps"></a>Następne kroki
Aby uzyskać więcej informacji na temat korzystania z protokołu OAuth 2.0 i zarządzanie interfejsami API, zobacz następujące hello wideo i towarzyszące [artykułu](api-management-howto-protect-backend-with-aad.md).

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

