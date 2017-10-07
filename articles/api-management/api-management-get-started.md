---
title: "aaaManage pierwszy interfejs API usługi Azure API Management | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak dodać operacje toocreate interfejsów API i wprowadzenie do interfejsu API zarządzania."
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 51b7df8b-1c43-43c6-90c9-0aa24f48206b
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 7d43f33aa359c4d1e605e9fb41e43d323ca6a777
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-your-first-api-in-azure-api-management"></a>Zarządzanie pierwszym interfejsem API w usłudze Azure API Management
## <a name="overview"> </a>Omówienie
W tym przewodniku pokazano, jak tooquickly Rozpoczynanie pracy za pomocą usługi Azure API Management i upewnij się Twoje pierwsze wywołanie interfejsu API.

## <a name="concepts"> </a>Co to jest usługa Azure API Management?
Można użyć dowolnego zaplecza Azure API Management tootake i uruchomić pełni funkcjonalnymi program interfejsu API na ich podstawie.

Typowe scenariusze obejmują:

* **Zabezpieczanie infrastruktury mobilnej** przez uzyskanie dostępu bramowego z kluczami interfejsu API, zapobieganie atakom DOS przy użyciu ograniczania przepływności lub korzystanie z zaawansowanych zasad zabezpieczeń, takich jak sprawdzanie poprawności tokenu JWT.
* **Włączanie ekosystemami partnerów niezależnego dostawcy oprogramowania** oferując dołączania szybkiego partnera przez dewelopera hello portalu i tworzenia toodecouple fasad interfejsu API z wewnętrznej implementacji, które nie są dojrzałe do użycia przez partnera.
* **Uruchomiony program wewnętrznego interfejsu API** oferując scentralizowanej lokalizacji hello organizacji toocommunicate o dostępności hello i najnowszych zmian tooAPIs, uzyskania dostępu na podstawie organizacyjnego kont bramowego wszystkie oparte na bezpiecznego kanału między Brama Hello interfejsu API i hello wewnętrznej bazy danych.

Hello system składa się z hello następujące składniki:

* Witaj **bramy interfejsu API** jest punkt końcowy hello który:
  
  * Akceptuje wywołuje interfejs API i kieruje je zapleczy tooyour.
  * Weryfikowanie kluczy interfejsu API, tokenów JWT, certyfikatów i innych poświadczeń.
  * Wymuszanie przydziałów użycia i ograniczeń liczby wywołań.
  * Przy użyciu interfejsu API na bieżąco hello bez modyfikacji kodu.
  * Buforowanie odpowiedzi zaplecza w skonfigurowanym miejscu.
  * Rejestrowanie w dzienniku metadanych wywołań w celu analizy.
* Witaj **portal wydawcy** jest hello interfejsu administracyjnego skonfigurowanie programu interfejsu API. Jego zastosowania to:
  
  * Definiowanie lub importowanie schematu interfejsu API.
  * Tworzenie pakietów interfejsów API do produktów.
  * Skonfiguruj zasady, takie jak przydziałów lub przekształcenia na powitania interfejsów API.
  * Uzyskiwanie szczegółowych informacji analitycznych.
  * Zarządzanie użytkownikami.
* Witaj **portalu dla deweloperów** służy jako hello głównego witrynę internetową dla deweloperów, gdzie można:
  
  * Czytanie dokumentacji interfejsu API.
  * Wypróbuj interfejsu API za pomocą konsoli interakcyjne hello.
  * Utworzyć konto i Subskrypcja klucze tooget interfejsu API.
  * Zyskanie dostępu do analiz własnego użycia.

## <a name="create-service-instance"> </a>Tworzenie wystąpienia usługi API Management
> [!NOTE]
> toocomplete tego samouczka jest potrzebne konto platformy Azure. Jeśli go nie masz, możesz utworzyć bezpłatne konto próbne w zaledwie kilka minut. Aby uzyskać szczegółowe informacje, zobacz artykuł [Bezpłatna wersja próbna platformy Azure][Azure Free Trial].
> 
> 

pierwszym krokiem Hello w pracy z interfejsu API zarządzania jest toocreate wystąpienie usługi. Zaloguj się toohello [Azure Portal] [ Azure Portal] i kliknij przycisk **nowy**, **sieci Web i mobilność**, **zarządzanie interfejsami API**.

![Nowe wystąpienie usługi API Management][api-management-create-instance-menu]

Aby uzyskać **nazwa**, określ toouse nazwę domeny podrzędnej unikatowy adres URL usługi hello.

Wybierz żądaną hello **subskrypcji**, **grupy zasobów** i **lokalizacji** wystąpienia usługi.

Wprowadź **firmy Contoso, Ltd.** dla hello **nazwa organizacji**i wprowadź swój adres e-mail w hello **E-Mail administratora** pola.

> [!NOTE]
> Ten adres e-mail jest używany dla powiadomień z hello system zarządzania interfejsu API. Aby uzyskać więcej informacji, zobacz [jak tooconfigure powiadomienia i szablonów w usłudze Azure API Management wiadomości e-mail][How tooconfigure notifications and email templates in Azure API Management].
> 
> 

![Nowa usługa API Management][api-management-create-instance-step1]

Wystąpienia usługi API Management są dostępne w trzech warstwach: Deweloper, Standardowej i Premium.

> [!NOTE]
> jest Hello warstwy deweloperów do tworzenia, testowania i programy pilotażowe interfejsu API, gdzie wysokiej dostępności nie ma znaczenia. W hello Standard i Premium warstw można skalować Twojej toohandle liczba zarezerwowanych jednostek większego ruchu. Witaj warstwy standardowa i Premium zapewniają usługi API Management z hello większość mocy obliczeniowej i wydajności. W tym samouczku można korzystać z dowolnej warstwy. Aby uzyskać więcej informacji na temat warstw usługi API Management, zobacz [API Management — cennik][API Management pricing].
> 
> 

Kliknij przycisk **Utwórz** toostart inicjowania obsługi administracyjnej wystąpienia usługi.

![Nowa usługa API Management][api-management-instance-created]

Po utworzeniu wystąpienia usługi hello hello następnym krokiem jest toocreate lub zaimportować interfejsu API.

## <a name="create-api"> </a>Importowanie interfejsu API
Interfejs API składa się z zestawu operacji, które mogą być wywoływane z poziomu aplikacji klienckiej. Operacje interfejsu API są tooexisting serwerem proxy usługi sieci web.

Interfejsy API mogą być tworzone ręcznie (wraz z dodawaniem operacji) lub importowane. W tym samouczku zaimportujemy hello interfejsu API dla przykładowych Kalkulator usługi sieci web obsługiwane przez firmę Microsoft i hostowanej na platformie Azure.

> [!NOTE]
> Aby uzyskać wskazówki na temat tworzenia interfejsu API i ręczne dodanie czynności, zobacz [jak toocreate interfejsów API](api-management-howto-create-apis.md) i [jak tooadd tooan operacje interfejsu API](api-management-howto-add-operations.md).
> 
> 

Interfejsy API są skonfigurowane z hello wydawcy portalu. tooreach, kliknij przycisk **wydawcy portalu** z paska narzędzi usługi hello.

![Portal wydawcy][api-management-management-console]

Kalkulator hello tooimport interfejsu API, kliknij przycisk **interfejsów API** z hello **zarządzanie interfejsami API** menu na powitania po lewej, a następnie kliknij **Import API**.

![Przycisk do importowania interfejsu API][api-management-import-api]

Wykonaj następujące kroki tooconfigure hello Kalkulator API hello:

1. Kliknij przycisk **z adresu URL**, wprowadź **http://calcapi.cloudapp.net/calcapi.json** do hello **Specyfikacja adresu URL** tekst i kliknij hello **programu Swagger**  przycisk radiowy.
2. Typ **obliczenia** do hello **sufiks adresu URL interfejsu API sieci Web** pola tekstowego.
3. Kliknij hello **produktów (opcjonalnie)** polu i wybierz polecenie **Starter**.
4. Kliknij przycisk **zapisać** hello tooimport interfejsu API.

![Dodawanie nowego interfejsu API][api-management-import-new-api]

> [!NOTE]
> Usługa **API Management** obecnie obsługuje importowanie obu wersji dokumentu Swagger (1.2 i 2.0). Zwróć uwagę, że chociaż w [specyfikacji Swagger 2.0](http://swagger.io/specification) zadeklarowano, że właściwości `host`, `basePath`, i `schemes` są opcjonalne, dokument Swagger 2.0 **MUSI** zawierać te właściwości. W przeciwnym razie nie zostanie zaimportowany. 
> 
> 

Po zaimportowaniu hello API hello strony podsumowania dla interfejsu API hello jest wyświetlana w hello wydawcy portalu.

![Podsumowanie interfejsu API][api-management-imported-api-summary]

Witaj sekcji interfejsu API ma kilka kart. Witaj **Podsumowanie** karta zawiera podstawowe metryki i informacji na temat hello interfejsu API. Witaj [ustawienia](api-management-howto-create-apis.md#configure-api-settings) karta jest używane tooview i edytowanie hello konfigurację interfejsu API. Witaj [operacji](api-management-howto-add-operations.md) karta jest używane toomanage hello interfejsu API operacji. Witaj **zabezpieczeń** karty mogą być używane tooconfigure bramy uwierzytelniania na powitania serwera wewnętrznej bazy danych przy użyciu uwierzytelniania podstawowego lub [uwierzytelnianie wzajemne certyfikatu](api-management-howto-mutual-certificates.md)i tooconfigure [ Autoryzacja użytkownika przy użyciu protokołu OAuth 2.0](api-management-howto-oauth2.md).  Witaj **problemów** karta jest używane tooview problemy zgłoszone przez hello deweloperów, którzy korzystają z interfejsów API. Witaj **produktów** karta jest używane tooconfigure hello produktów, które zawierają ten interfejs API.

Domyślnie każde wystąpienie usługi API Management zawiera dwa produkty przykładowe:

* **Starter (początkowy)**
* **Unlimited (nieograniczony)**

W tym samouczku hello podstawowe Kalkulator interfejsu API dodano produktu Starter toohello importowane hello interfejsu API.

W kolejności toomake wywołania tooan interfejsu API deweloperzy najpierw uzyskać subskrypcję produktu tooa, co umożliwia im tooit dostępu. Deweloperzy mogą subskrybować tooproducts w portalu dla deweloperów hello lub Administratorzy mogą subskrybować tooproducts deweloperów w portalu wydawcy hello. Od czasu utworzenia wystąpienia interfejsu API zarządzania hello w hello poprzednie kroki w samouczku hello tak, aby już subskrybowany tooevery produktu domyślnie są przeznaczone dla administratorów.

## <a name="call-operation"></a>Wywołać operację z portalu dla deweloperów hello
Operacje mogą być wywoływane bezpośrednio z portalu dla deweloperów hello, która zapewnia tooview wygodny sposób i przetestować hello operacje interfejsu API. W tym kroku samouczka wywoła API Kalkulator podstawowe hello **Dodaj dwie liczb całkowitych** operacji. Kliknij przycisk **portalu dla deweloperów** menu hello w hello górnego prawego hello wydawcy portalu.

![Portal dla deweloperów][api-management-developer-portal-menu]

Kliknij przycisk **interfejsów API** z hello menu u góry, a następnie kliknij przycisk **podstawowe Kalkulator** toosee hello dostępnych operacji.

![Portal dla deweloperów][api-management-developer-portal-calc-api]

Należy pamiętać, hello próbki opisy i parametrów, które zostały zaimportowane wraz z hello interfejsu API i operacje, Udostępnianie dokumentacji dla deweloperów hello, które będą korzystać z tej operacji. Te opisy można również dodawać podczas ręcznego dodawania operacji.

Witaj toocall **Dodaj dwie liczb całkowitych** operacji, kliknij przycisk **wypróbuj**.

![Wypróbuj][api-management-developer-portal-calc-api-console]

Wpisz część wartości parametrów hello lub zachować ustawienia domyślne hello a następnie kliknij przycisk **wysyłania**.

![HTTP Get][api-management-invoke-get]

Po wywołaniu operacji portalu dla deweloperów hello Wyświetla hello **stanu odpowiedzi**, hello **nagłówki odpowiedzi**, natomiast dla ustawienia **zawartości odpowiedzi**.

![Odpowiedź][api-management-invoke-get-response]

## <a name="view-analytics"> </a>Wyświetlanie analiz
Analiza tooview podstawowe Kalkulator, przełącznik wstecz toohello wydawcy portalu, wybierając **Zarządzaj** menu hello w hello górnego prawego hello portalu dla deweloperów.

![Zarządzanie][api-management-manage-menu]

Witaj domyślny widok portalu wydawcy hello jest hello **pulpitu nawigacyjnego**, który zawiera omówienie wystąpienia interfejsu API zarządzania.

![Pulpit nawigacyjny][api-management-dashboard]

Przesuwania myszy hello wykres hello **podstawowe Kalkulator** toosee hello określonych metryk hello użyciem hello interfejsu API dla danego okresu.

> [!NOTE]
> Na wykresie nie ma żadnych wierszy, Przełącz portalu dla deweloperów toohello Wstecz i wywołań do hello interfejsu API, poczekaj chwilę, a następnie powrotu toohello pulpitu nawigacyjnego.
> 
> 

Kliknij przycisk **Wyświetl szczegóły** tooview hello stronę podsumowania hello interfejsu API, łącznie z większą wersję metryki hello wyświetlane.

![Analiza][api-management-mouse-over]

![Podsumowanie][api-management-api-summary-metrics]

Szczegółowe metryki i raportów, kliknij przycisk **Analytics** z hello **zarządzanie interfejsami API** menu po lewej stronie powitania.

![Omówienie][api-management-analytics-overview]

Witaj **Analytics** sekcja zawiera następujące cztery karty hello:

* **Jeden rzut oka** udostępnia ogólne użycie i metryki kondycji również hello top deweloperzy najlepszych produktów, top interfejsów API operacje i top.
* **Użycie** zapewnia głębszy wgląd w wywołania interfejsu API i przepustowość, w tym reprezentację geograficzną.
* **Kondycja** koncentruje się na kodach stanu, współczynnikach pomyślnego użycia pamięci podręcznej, czasach odpowiedzi oraz czasach odpowiedzi interfejsu API i usług.
* **Działanie** udostępnia raporty, które przechodzenie na powitania określonego działania przez deweloperów, produktu, interfejsu API i operację.

## <a name="next-steps"> </a>Następne kroki
* Dowiedz się, jak za[chronić interfejs API limity szybkości](api-management-howto-product-with-rules.md).

[Azure Free Trial]: http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=api_management_hero_a

[Create an API Management instance]: #create-service-instance
[Create an API]: #create-api
[Add an operation]: #add-operation
[Add hello new API tooa product]: #add-api-to-product
[Subscribe toohello product that contains hello API]: #subscribe
[Call an operation from hello Developer Portal]: #call-operation
[View analytics]: #view-analytics
[Next steps]: #next-steps


[How toomanage developer accounts in Azure API Management]: api-management-howto-create-or-invite-developers.md
[Configure API settings]: api-management-howto-create-apis.md#configure-api-settings
[How tooconfigure notifications and email templates in Azure API Management]: api-management-howto-configure-notifications.md
[Responses]: api-management-howto-add-operations.md#responses
[How create and publish a product]: api-management-howto-add-products.md
[API Management pricing]: http://azure.microsoft.com/pricing/details/api-management/

[Azure Portal]: https://portal.azure.com/

[api-management-management-console]: ./media/api-management-get-started/api-management-management-console.png
[api-management-create-instance-menu]: ./media/api-management-get-started/api-management-create-instance-menu.png
[api-management-create-instance-step1]: ./media/api-management-get-started/api-management-create-instance-step1.png
[api-management-create-instance-step2]: ./media/api-management-get-started/api-management-create-instance-step2.png
[api-management-instance-created]: ./media/api-management-get-started/api-management-instance-created.png
[api-management-import-api]: ./media/api-management-get-started/api-management-import-api.png
[api-management-import-new-api]: ./media/api-management-get-started/api-management-import-new-api.png
[api-management-imported-api-summary]: ./media/api-management-get-started/api-management-imported-api-summary.png
[api-management-calc-operations]: ./media/api-management-get-started/api-management-calc-operations.png
[api-management-list-products]: ./media/api-management-get-started/api-management-list-products.png
[api-management-add-api-to-product]: ./media/api-management-get-started/api-management-add-api-to-product.png
[api-management-add-myechoapi-to-product]: ./media/api-management-get-started/api-management-add-myechoapi-to-product.png
[api-management-api-added-to-product]: ./media/api-management-get-started/api-management-api-added-to-product.png
[api-management-developers]: ./media/api-management-get-started/api-management-developers.png
[api-management-add-subscription]: ./media/api-management-get-started/api-management-add-subscription.png
[api-management-add-subscription-window]: ./media/api-management-get-started/api-management-add-subscription-window.png
[api-management-subscription-added]: ./media/api-management-get-started/api-management-subscription-added.png
[api-management-developer-portal-menu]: ./media/api-management-get-started/api-management-developer-portal-menu.png
[api-management-developer-portal-calc-api]: ./media/api-management-get-started/api-management-developer-portal-calc-api.png
[api-management-developer-portal-calc-api-console]: ./media/api-management-get-started/api-management-developer-portal-calc-api-console.png
[api-management-invoke-get]: ./media/api-management-get-started/api-management-invoke-get.png
[api-management-invoke-get-response]: ./media/api-management-get-started/api-management-invoke-get-response.png
[api-management-manage-menu]: ./media/api-management-get-started/api-management-manage-menu.png
[api-management-dashboard]: ./media/api-management-get-started/api-management-dashboard.png

[api-management-add-response]: ./media/api-management-get-started/api-management-add-response.png
[api-management-add-response-window]: ./media/api-management-get-started/api-management-add-response-window.png
[api-management-developer-key]: ./media/api-management-get-started/api-management-developer-key.png
[api-management-mouse-over]: ./media/api-management-get-started/api-management-mouse-over.png
[api-management-api-summary-metrics]: ./media/api-management-get-started/api-management-api-summary-metrics.png
[api-management-analytics-overview]: ./media/api-management-get-started/api-management-analytics-overview.png
[api-management-analytics-usage]: ./media/api-management-get-started/api-management-analytics-usage.png
[api-management-]: ./media/api-management-get-started/api-management-.png
[api-management-]: ./media/api-management-get-started/api-management-.png
