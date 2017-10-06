---
title: "aaaAuthentication i autoryzację w usłudze Azure Mobile Apps | Dokumentacja firmy Microsoft"
description: "Odwołanie koncepcyjne i przegląd hello uwierzytelniania / autoryzacji funkcji usługi Azure Mobile Apps"
services: app-service\mobile
documentationcenter: 
author: mattchenderson
manager: syntaxc4
editor: 
ms.assetid: a46dbf70-867d-48f6-8885-7f5207ad102e
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 10/01/2016
ms.author: mahender
ms.openlocfilehash: 5255734481ada11afb65982aebe45c2a349402fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="authentication-and-authorization-in-azure-mobile-apps"></a>Uwierzytelnianie i autoryzacja w usłudze Azure Mobile Apps
## <a name="what-is-app-service-authentication--authorization"></a>Co to jest aplikacja usługi uwierzytelniania / autoryzacji?
> [!NOTE]
> W tym temacie zostaną zmigrowane tooa skonsolidowane [aplikacji usługi uwierzytelniania / autoryzacji](../app-service/app-service-authentication-overview.md) temat, który obejmuje aplikacje interfejsu API, mobilne i sieci Web.
> 
> 

Aplikacja usługi uwierzytelniania / autoryzacji jest funkcją, dzięki czemu toolog Twojej aplikacji w użytkowników z nie zmian w kodzie wymaganych aplikacji hello wewnętrznej bazy danych. Zapewnia prosty sposób tooprotect aplikacji i pracy z danymi użytkownika.

Korzysta z usługi aplikacji tożsamości federacyjnych, w którym strona 3rd **dostawcy tożsamości** ("IDP") przechowuje konta i uwierzytelnia użytkowników, a aplikacja hello używa tej tożsamości zamiast własny. Usługi aplikacji obsługuje pięć dostawców tożsamości fabrycznej hello: *usługi Azure Active Directory*, *Facebook*, *Google*, *Account Microsoft*, i *Twitter*. Ta obsługa można również rozwinąć dla aplikacji, integrując innego dostawcy tożsamości lub rozwiązania tożsamości niestandardowej.

Aplikację można wykorzystać dowolną liczbę tych dostawców tożsamości, więc możesz zapewnić użytkownikom końcowym opcje dotyczące sposobu logowania.

Jeśli chcesz tooget pracę już teraz, zobacz jedną z następujących samouczków hello:

* [Dodawanie aplikacji dla systemu iOS tooyour uwierzytelniania]
* [Dodaj aplikację platformy Xamarin.iOS tooyour uwierzytelniania]
* [Dodawanie aplikacji platformy Xamarin.Android tooyour uwierzytelniania]
* [Dodawanie aplikacji dla systemu Windows tooyour uwierzytelniania]

## <a name="how-authentication-works"></a>Jak działa uwierzytelniania
W kolejności tooauthenticate przy użyciu jednego z dostawców tożsamości hello musisz najpierw tooknow dostawcy tożsamości hello tooconfigure dotyczące Twojej aplikacji. Dostawca tożsamości Hello następnie zapewnia identyfikatory i hasła, musisz zapewnić wstecz toohello aplikacji. To kończy hello relacji zaufania i umożliwia tooit tożsamości podane toovalidate usługi aplikacji.

Te kroki są szczegółowo opisane hello następujące tematy:

* [Jak tooconfigure Logowanie usługi Azure Active Directory toouse aplikacji]
* [Jak tooconfigure logowanie Facebook toouse aplikacji]
* [Jak tooconfigure logowanie Google toouse aplikacji]
* [Jak tooconfigure logowanie Account Microsoft toouse aplikacji]
* [Jak tooconfigure logowanie Twitter toouse aplikacji]

Po skonfigurowaniu wszystkich hello wewnętrznej bazy danych można zmodyfikować toolog Twojego klienta w. Istnieją dwie metody w tym miejscu:

* Za pomocą jednego wiersza kodu, umożliwiają hello Mobile Apps klienta SDK logowania użytkowników.
* Korzystaj z zestawu SDK opublikowanych przez tożsamością tooestablish tożsamości danego dostawcy i uzyskać tooApp dostępu do usługi.

> [!TIP]
> Większość aplikacji należy używać tooget SDK dostawcy mogą logować się bardziej wrażenie macierzystego i tooleverage odświeżania w pomocy technicznej i inne korzyści specyficznego dla dostawcy.
> 
> 

### <a name="how-authentication-without-a-provider-sdk-works"></a>Jak działa uwierzytelniania bez dostawcy zestawu SDK
Jeśli nie chcesz, aby tooset się dostawcy SDK, można zezwolić Mobile Apps tooperform hello logowania dla Ciebie. powitania klienta Mobile Apps SDK spowoduje otwarcie dostawca toohello widoku sieci web po wybraniu i pełne hello logowania. Od czasu do czasu na blogi i fora, które będą wyświetlane to określane tooas hello "serwera przepływ" lub "skierowane do serwera przepływ", ponieważ powitania serwera jest zarządzany hello logowania i powitania klienta SDK nigdy nie otrzyma hello dostawcy tokenu.

Kod Hello potrzebne toostart tego przepływu jest objęte hello samouczka uwierzytelniania dla każdej platformy. W końcu hello przepływu hello powitania klienta SDK ma token usługi aplikacji, a hello token jest automatycznie dołączone tooall żądań toohello wewnętrznej bazy danych.

### <a name="how-authentication-with-a-provider-sdk-works"></a>Jak działa uwierzytelniania za pomocą dostawcy zestawu SDK
Praca z dostawcy zestawu SDK umożliwia toointeract logowania hello ściślej z platformą hello, aplikacja hello systemu operacyjnego na którym działa. Zapewnia to również token dostawcy i niektóre informacje użytkownika na powitania klienta, co pozwala znacznie łatwiejsze wykres tooconsume interfejsów API i dostosować hello środowisko użytkownika. Od czasu do czasu na blogi i fora będą widzieli tej hello tooas określonego "przebieg klienta" lub "klient skierowany przepływu" od kodu na powitania klienta jest obsługa logowania hello i powitania klienta kod ma dostęp tooa dostawcy tokenu.

Po uzyskaniu tokenu dostawcy musi toobe wysyłane tooApp usługi do sprawdzania poprawności. W końcu hello przepływu hello powitania klienta SDK ma token usługi aplikacji, a hello token jest automatycznie dołączone tooall żądań toohello wewnętrznej bazy danych. Hello developer można również zarejestrować tokenu odwołania toohello dostawcy, gdy wybiera on.

## <a name="how-authorization-works"></a>Jak działa autoryzacji
Aplikacja usługi uwierzytelniania / autoryzacji udostępnia kilka opcji **tootake akcji w przypadku nieuwierzytelnionego żądania**. Przed kodu odbiera danego żądania, można mieć toosee wyboru usługi aplikacji, jeśli Żądanie hello jest uwierzytelniony i jeśli nie, go odrzucić i spróbować toohave hello logowanie użytkownika przed podjęciem ponownej próby.

Jedną z opcji jest toohave nieuwierzytelnione żądania przekierowania tooone hello dostawców tożsamości. W przeglądarce sieci web to zajmie faktycznie hello użytkownika tooa nowej strony. Jednak nie można przekierować z klientów urządzeń przenośnych w ten sposób i nieuwierzytelnione odpowiedzi będą otrzymywać HTTP *401 nieautoryzowane* odpowiedzi. Biorąc pod uwagę to, hello pierwsze żądanie, sprawia, że klient powinien zawsze być punktu końcowego logowania toohello, a następnie możesz wprowadzić wywołuje tooany innych interfejsów API. Jeśli toocall innego interfejsu API przed zalogowaniem się, że klient zostanie zwrócony błąd.

Jeśli chcesz toohave bardziej szczegółowego kontrolowania, przez które punkty końcowe wymagają uwierzytelniania, można również wybrać "żadna akcja ze strony (Zezwalaj na żądanie)" dla nieuwierzytelnione żądania. W takim przypadku wszystkie decyzje uwierzytelniania są odroczone tooyour kodu aplikacji. To pozwala również użytkowników toospecific dostępu tooallow na podstawie reguł autoryzacji niestandardowej.

## <a name="documentation"></a>Dokumentacja
Witaj, jak następujące samouczki Pokaż tooadd uwierzytelniania tooyour klientów mobilnych za pomocą usługi aplikacji:

* [Dodawanie aplikacji dla systemu iOS tooyour uwierzytelniania]
* [Dodaj aplikację platformy Xamarin.iOS tooyour uwierzytelniania]
* [Dodawanie aplikacji platformy Xamarin.Android tooyour uwierzytelniania]
* [Dodawanie aplikacji dla systemu Windows tooyour uwierzytelniania]

Witaj, jak następujące samouczki Pokaż dostawców uwierzytelniania różnych tooleverage usługi aplikacji tooconfigure:

* [Jak tooconfigure Logowanie usługi Azure Active Directory toouse aplikacji]
* [Jak tooconfigure logowanie Facebook toouse aplikacji]
* [Jak tooconfigure logowanie Google toouse aplikacji]
* [Jak tooconfigure logowanie Account Microsoft toouse aplikacji]
* [Jak tooconfigure logowanie Twitter toouse aplikacji]

W razie potrzeby toouse systemu tożsamości inne niż hello te podane w tym miejscu można też skorzystać hello [obsługę uwierzytelniania niestandardowego w powitania serwera .NET SDK w wersji preview](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#custom-auth).

[Dodawanie aplikacji dla systemu iOS tooyour uwierzytelniania]: app-service-mobile-ios-get-started-users.md
[Dodaj aplikację platformy Xamarin.iOS tooyour uwierzytelniania]: app-service-mobile-xamarin-ios-get-started-users.md
[Dodawanie aplikacji platformy Xamarin.Android tooyour uwierzytelniania]: app-service-mobile-xamarin-android-get-started-users.md
[Dodawanie aplikacji dla systemu Windows tooyour uwierzytelniania]: app-service-mobile-windows-store-dotnet-get-started-users.md

[Jak tooconfigure Logowanie usługi Azure Active Directory toouse aplikacji]: app-service-mobile-how-to-configure-active-directory-authentication.md
[Jak tooconfigure logowanie Facebook toouse aplikacji]: app-service-mobile-how-to-configure-facebook-authentication.md
[Jak tooconfigure logowanie Google toouse aplikacji]: app-service-mobile-how-to-configure-google-authentication.md
[Jak tooconfigure logowanie Account Microsoft toouse aplikacji]: app-service-mobile-how-to-configure-microsoft-authentication.md
[Jak tooconfigure logowanie Twitter toouse aplikacji]: app-service-mobile-how-to-configure-twitter-authentication.md
