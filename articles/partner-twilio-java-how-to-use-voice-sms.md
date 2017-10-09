---
title: "tooUse aaaHow usługi Twilio głosowe i programu SMS (Java) | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak komunikatów toomake połączeń telefonicznych i Wyślij wiadomość SMS z usługi interfejsu API usługi Twilio hello na platformie Azure. Przykłady kodu napisane w języku Java."
services: 
documentationcenter: java
author: devinrader
manager: twilio
editor: mollybos
ms.assetid: f3508965-5527-4255-9d51-5d5f926f4d43
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 11/25/2014
ms.author: microsofthelp@twilio.com
ms.openlocfilehash: a186e2c8e73ced928bd0dec348971034f10ba82c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-twilio-for-voice-and-sms-capabilities-in-java"></a>Jak tooUse usługi Twilio głosowe i możliwości programu SMS w języku Java
W tym przewodniku pokazano, jak tooperform typowych zadań programowania hello interfejsu API usługi Twilio usługi na platformie Azure. omówione scenariusze Hello obejmują tworzenie połączeń telefonicznych i wysyłanie wiadomości krótką wiadomość usługi (SMS). Aby uzyskać więcej informacji na temat usługi Twilio i komunikacja głosowa programu SMS w aplikacji, zobacz hello [następne kroki](#NextSteps) sekcji.

## <a id="WhatIs"></a>Co to jest usługi Twilio?
Usługi Twilio jest telefonii API usługi sieci web, która umożliwia korzystanie z istniejących języków sieci web i umiejętności toobuild głosu aplikacji i programu SMS. Usługi Twilio jest usługą innych firm (nie funkcji platformy Azure i nie produkt firmy Microsoft).

**Usługi Twilio głosu** umożliwia toomake Twojej aplikacji i odbieranie połączeń telefonicznych. **SMS usługi Twilio** umożliwia toomake Twojej aplikacji i odbieranie wiadomości SMS. **Klient usługi Twilio** umożliwia aplikacji komunikację głosową tooenable przy użyciu istniejących połączeń internetowych, w tym przenośnych połączenia.

## <a id="Pricing"></a>Cennik usługi Twilio i oferty specjalne
Informacje o cenach usługi Twilio znajduje się w temacie [cennik usługi Twilio][twilio_pricing]. Azure klienci otrzymają [oferta specjalna][special_offer]: wolnego środki tekstów 1000 lub 1000 ruchu przychodzącego minut. toosign dla to oferty lub uzyskać więcej informacji, odwiedź stronę [http://ahoy.twilio.com/azure][special_offer].

## <a id="Concepts"></a>Pojęcia
Witaj interfejsu API usługi Twilio jest interfejs API RESTful, która zapewnia funkcje programu SMS i komunikacja głosowa aplikacji. Klient biblioteki są dostępne w wielu językach; Aby uzyskać listę, zobacz [bibliotek interfejsu API usługi Twilio][twilio_libraries].

Kluczowe aspekty hello interfejsu API usługi Twilio są zleceń usługi Twilio i usługi Twilio Markup Language (TwiML).

### <a id="Verbs"></a>Usługi Twilio zlecenia
Witaj interfejs API korzysta z usługi Twilio zleceń; na przykład Witaj  **&lt;powiedzieć&gt;**  zlecenie powoduje, że usługi Twilio tooaudibly dostarczenia komunikatu w wywołaniu.

Witaj poniżej przedstawiono listę poleceń usługi Twilio.

* **&lt;Wybierania&gt;**: łączy hello wywołującego tooanother telefonu.
* **&lt;Zbierz&gt;**: zbiera wprowadzony na klawiaturze telefonu hello cyfr.
* **&lt;Rozłączanie&gt;**: kończy wywołanie.
* **&lt;Odtwórz&gt;**: odtwarzania pliku audio.
* **&lt;Kolejka&gt;**: Dodaj kolejkę tooa hello obiekty wywołujące.
* **&lt;Wstrzymaj&gt;**: dyskretnie czeka na określoną liczbę sekund.
* **&lt;Rekord&gt;**: rejestruje wywołującego hello głosu i zwraca adres URL pliku zawierającego hello rejestrowania.
* **&lt;Przekieruj&gt;**: przekazuje kontrolę nad wywołania lub SMS toohello TwiML na inny adres URL.
* **&lt;Odrzuć&gt;**: odrzuca jako przychodzące wywołania numer usługi Twilio tooyour bez rozliczeń można.
* **&lt;Powiedz&gt;**: Konwertuje tekst toospeech, które zostało utworzone w wywołaniu.
* **&lt;SMS&gt;**: wysyła wiadomość SMS.

### <a id="TwiML"></a>TwiML
Zestaw instrukcji oparte na języku XML, oparte na powitania usługi Twilio zlecenia, które informują usługi Twilio, jak jest TwiML tooprocess wywołania lub wiadomości SMS.

Na przykład powitania po TwiML może dokonać konwersji tekstu hello **Hello World!** toospeech.

```xml
    <?xml version="1.0" encoding="UTF-8" ?>
    <Response>
       <Say>Hello World!</Say>
    </Response>
```

Podczas wywołania aplikacji hello interfejsu API usługi Twilio, jeden z parametrów interfejsu API hello jest adres URL hello, która zwraca odpowiedź TwiML hello. Do celów programistycznych możesz użyć wprowadzone do usługi Twilio adresy URL tooprovide hello TwiML odpowiedzi są używane przez aplikacje. Może również udostępniać swoje własne adresy URL tooproduce hello TwiML odpowiedzi, a inną opcją jest toouse hello **TwiMLResponse** obiektu.

Aby uzyskać więcej informacji na temat usługi Twilio zlecenia i ich atrybuty oraz TwiML, zobacz [TwiML][twiml]. Aby uzyskać dodatkowe informacje na temat hello interfejsu API usługi Twilio, zobacz [interfejsu API usługi Twilio][twilio_api].

## <a id="CreateAccount"></a>Tworzenie konta usługi Twilio
Jeśli wszystko jest gotowe tooget konta usługi Twilio, zarejestruj się w [spróbuj usługi Twilio][try_twilio]. Można rozpoczynać bezpłatne konto, a następnie Uaktualnij swoje konto później.

Po utworzeniu konta dla konta usługi Twilio, otrzymasz Identyfikatora konta oraz tokenu uwierzytelniania. Zarówno będzie potrzebne toomake wywołania interfejsu API usługi Twilio. tooprevent nieautoryzowany dostęp do konta tooyour, bezpieczeństwo Twojego tokenu uwierzytelniania. Twój identyfikator konta i uwierzytelniania token jest wyświetlana na powitania [usługi Twilio Console][twilio_console]w hello pola oznaczone **identyfikator SID konta** i **TOKEN uwierzytelniania**odpowiednio.

## <a id="create_app"></a>Tworzenie aplikacji Java
1. Uzyskaj hello JAR usługi Twilio i dodać tooyour ścieżkę i używanemu zestawowi wdrożenia WAR kompilacji języka Java. W [https://github.com/twilio/twilio-java][twilio_java], możesz pobrać hello GitHub źródeł i tworzyć własne JAR lub pobrać wbudowanych JAR (z lub bez zależności).
2. Upewnij się, Twoje JDK **cacerts** magazynu kluczy zawiera hello firmy Equifax Secure urzędu certyfikacji certyfikatu z 67:CB:9 odcisk palca MD5 D: C0:13:24:8A:82:9B:B2:17:1E:D1:1B:EC:D4 (numer seryjny hello jest 35:DE:F4:CF i hello SHA1 Odcisk palca jest D2:32:09:AD:23:D3:14:23:21:74:E4:0 D: 7F:9 D: 62:13:97:86:63:3A). Jest to hello certyfikat urzędu certyfikacji dla hello [https://api.twilio.com] [ twilio_api_service] usługi, która jest wywoływana, gdy używasz interfejsów API usługi Twilio. Informacji o sprawdzeniu Twojej JDK **cacerts** keystore zawiera hello prawidłowy certyfikat urzędu certyfikacji, zobacz [Dodawanie certyfikatu toohello magazynu certyfikatów urzędu certyfikacji Java][add_ca_cert].

Szczegółowe instrukcje dotyczące języka Java za pomocą biblioteki klienta usługi Twilio hello są dostępne pod adresem [jak tooMake rozwiązania usługi przy użyciu Twilio w aplikacji Java na platformie Azure rozmowy telefonicznej][howto_phonecall_java].

## <a id="configure_app"></a>Konfigurowanie bibliotek usługi Twilio tooUse Twoja aplikacja
W kodzie, możesz dodać **zaimportować** instrukcji u góry hello plików źródłowych dla hello usługi Twilio pakietów lub klasy można mają toouse w aplikacji.

Dla plików źródłowych Java:

```java
    import com.twilio.*;
    import com.twilio.rest.api.*;
    import com.twilio.type.*;
    import com.twilio.twiml.*;
```

Dla plików źródłowych Java strony serwera (JSP):

```java
    import="com.twilio.*"
    import="com.twilio.rest.api.*"
    import="com.twilio.type.*"
    import="com.twilio.twiml.*"
 ```
 
W zależności od tego, które pakiety usługi Twilio lub klasy mają toouse, Twoje **zaimportować** instrukcje mogą się różnić.

## <a id="howto_make_call"></a>Porady: wykonywanie połączenia wychodzące
Witaj poniżej pokazano, jak toomake wychodzące wywołanie przy użyciu hello **wywołać** klasy. Ten kod zawiera również hello tooreturn lokacja dostarczonych do usługi Twilio odpowiedzi usługi Twilio Markup Language (TwiML). Podstaw wartości hello **z** i **do** numerów telefonów i upewnij się, że sprawdzisz hello **z** numer telefonu dla kodu hello toorunning poprzedniego konta usługi Twilio.

```java
    // Use your account SID and authentication token instead
    // of hello placeholders shown here.
    String accountSID = "your_twilio_account_SID";
    String authToken = "your_twilio_authentication_token";

    // Initialize hello Twilio client.
    Twilio.init(accountSID, authToken);

    // Use hello Twilio-provided site for hello TwiML response.
    URI uri = new URI("http://twimlets.com/message" +
            "?Message%5B0%5D=Hello%20World%21");

    // Declare tooand From numbers
    PhoneNumber too= new PhoneNumber("NNNNNNNNNN");
    PhoneNumber from = new PhoneNumber("NNNNNNNNNN");

    // Create a Call creator passing From, tooand URL values
    // then make hello call by executing hello create() method
    Call.creator(to, from, uri).create();
```

Aby uzyskać więcej informacji o parametrach hello przekazano toohello **Call.creator** metody, zobacz [http://www.twilio.com/docs/api/rest/making-calls][twilio_rest_making_calls].

Jak wspomniano, ten kod używa hello tooreturn lokacja dostarczonych do usługi Twilio TwiML odpowiedzi. Zamiast tego można użyć własnych lokacji tooprovide hello odpowiedzi TwiML; Aby uzyskać więcej informacji, zobacz [jak tooProvide TwiML odpowiedzi w aplikacji Java na platformie Azure](#howto_provide_twiml_responses).

## <a id="howto_send_sms"></a>Porady: Wyślij wiadomość SMS
Witaj poniżej pokazano, jak hello toosend wiadomość SMS przy użyciu **komunikat** klasy. Witaj **z** numer, **4155992671**, jest obsługiwane przez usługi Twilio, dla wersji próbnej kont toosend wiadomości SMS. Witaj **do** należy sprawdzić liczbę dla kodu hello toorunning poprzedniego konta usługi Twilio.

```java
    // Use your account SID and authentication token instead
    // of hello placeholders shown here.
    String accountSID = "your_twilio_account_SID";
    String authToken = "your_twilio_authentication_token";

    // Initialize hello Twilio client.
    Twilio.init(accountSID, authToken);

    // Declare tooand From numbers and hello Body of hello SMS message
    PhoneNumber too= new PhoneNumber("+14159352345"); // Replace with a valid phone number for your account.
    PhoneNumber from = new PhoneNumber("+14158141829"); // Replace with a valid phone number for your account.
    String body = "Where's Wallace?";

    // Create a Message creator passing From, tooand Body values
    // then send hello SMS message by calling hello create() method
    Message sms = Message.creator(to, from, body).create();
```

Aby uzyskać więcej informacji o parametrach hello przekazano toohello **Message.creator** metody, zobacz [http://www.twilio.com/docs/api/rest/sending-sms][twilio_rest_sending_sms].

## <a id="howto_provide_twiml_responses"></a>Porady: Podaj TwiML odpowiedzi z własnej witryny sieci Web
Gdy aplikacja inicjuje toohello wywołania interfejsu API usługi Twilio, na przykład za pośrednictwem hello **CallCreator.create** metody usługi Twilio wyśle adres URL tooa żądania, który jest oczekiwanym tooreturn TwiML odpowiedź. w powyższym przykładzie Hello używa adresu URL dostarczony do usługi Twilio hello [http://twimlets.com/message][twimlet_message_url]. (Podczas TwiML jest przeznaczony do użytku przez usługi sieci Web, można wyświetlić hello TwiML w przeglądarce. Na przykład kliknij pozycję [http://twimlets.com/message] [ twimlet_message_url] toosee pustą  **&lt;odpowiedzi&gt;**  element; inny przykład kliknij [http://twimlets.com/message?Message%5B0%5D=Hello%20World%21] [ twimlet_message_url_hello_world] toosee  **&lt;odpowiedzi&gt;**  element, który zawiera  **&lt;powiedzieć? &gt;**  elementu.)

Zamiast polegania na adres URL udostępniony do usługi Twilio hello, można utworzyć własny adres URL w witrynie odpowiedzi HTTP. Można utworzyć witrynę hello w dowolnym języku, który zwraca odpowiedzi HTTP; w tym temacie założono, że będzie obsługiwać hello adres URL strony JSP.

Witaj po JSP wyników strony w odpowiedzi TwiML z informacją, **Hello World!** na powitania wywołania.

```xml
    <%@ page contentType="text/xml" %>
    <Response>
        <Say>Hello World!</Say>
    </Response>
```

powitania po JSP wyników strony w odpowiedzi TwiML informacją część tekstu, ma kilka pauzy i mówi informacje o wersji interfejsu API usługi Twilio hello i nazwy roli Azure hello.

```xml
    <%@ page contentType="text/xml" %>
    <Response>
        <Say>Hello from Azure!</Say>
        <Pause></Pause>
        <Say>hello Twilio API version is <%= request.getParameter("ApiVersion") %>.</Say>
        <Say>hello Azure role name is <%= System.getenv("RoleName") %>.</Say>
        <Pause></Pause>
        <Say>Good bye.</Say>
    </Response>
```

Witaj **ApiVersion** parametr jest dostępny w żądaniach głosu usługi Twilio (nie liczba żądań programu SMS). Parametry żądania dostępne hello toosee głosowe usługi Twilio i żądań programu SMS, zobacz <https://www.twilio.com/docs/api/twiml/twilio_request> i <https://www.twilio.com/docs/api/twiml/sms/twilio_request >odpowiednio. Witaj **RoleName** zmiennej środowiskowej jest dostępna jako część wdrożenia usługi Azure. (Zmiennych środowiskowych niestandardowych tooadd ma tak one może zostać pobrana z **System.getenv**, zobacz sekcję zmiennych środowiska hello na [dodatkowych ustawień konfiguracji roli] [misc_role_config_settings].)

Po utworzeniu strony JSP Konfigurowanie odpowiedzi TwiML tooprovide, użyj hello adres URL strony JSP hello hello adres URL przekazany hello **Call.creator** metody. Na przykład, jeśli masz aplikację sieci Web o nazwie tooan MyTwiML wdrożone Azure hostowanej usługi i hello nazwa strony JSP hello jest mytwiml.jsp, hello adres URL, które mogą zostać przekazane za**Call.creator** jak pokazano poniżej hello:

```java
    // Declare tooand From numbers and hello URL of your JSP page
    PhoneNumber too= new PhoneNumber("NNNNNNNNNN");
    PhoneNumber from = new PhoneNumber("NNNNNNNNNN");
    URI uri = new URI("http://<your_hosted_service>.cloudapp.net/MyTwiML/mytwiml.jsp");

    // Create a Call creator passing From, tooand URL values
    // then make hello call by executing hello create() method
    Call.creator(to, from, uri).create();
```

Inną opcją w przypadku odpowiadać TwiML odbywa się za pośrednictwem hello **VoiceResponse** klasy, która jest dostępna w hello **com.twilio.twiml** pakietu.

Aby uzyskać dodatkowe informacje dotyczące korzystania z usługi Twilio w platformie Azure za pomocą języka Java, zobacz [jak tooMake rozwiązania usługi przy użyciu Twilio w aplikacji Java na platformie Azure rozmowy telefonicznej][howto_phonecall_java].

## <a id="AdditionalServices"></a>Porady: korzystania z usługi Twilio dodatkowych usług
Ponadto przykłady toohello pokazane, usługi Twilio oferuje API sieci web można używać tooleverage dodatkowe usługi Twilio funkcji z aplikacji Azure. Aby uzyskać szczegółowe informacje, zobacz hello [dokumentacji interfejsu API usługi Twilio][twilio_api_documentation].

## <a id="NextSteps"></a>Następne kroki
Teraz, kiedy znasz już podstawy hello hello usługi usługi Twilio, wykonaj te więcej toolearn łącza:

* [Wytyczne dotyczące zabezpieczeń usługi Twilio][twilio_security_guidelines]
* [Porada usługi Twilio i przykładowy kod][twilio_howtos]
* [Samouczki usługi Twilio Szybki Start][twilio_quickstarts]
* [Usługi Twilio w witrynie GitHub][twilio_on_github]
* [Porozmawiaj tooTwilio pomocy technicznej][twilio_support]

[twilio_java]: https://github.com/twilio/twilio-java
[twilio_api_service]: https://api.twilio.com
[add_ca_cert]: java-add-certificate-ca-store.md
[howto_phonecall_java]: partner-twilio-java-phone-call-example.md
[misc_role_config_settings]: http://msdn.microsoft.com/library/windowsazure/hh690945.aspx
[twimlet_message_url]: http://twimlets.com/message
[twimlet_message_url_hello_world]: http://twimlets.com/message?Message%5B0%5D=Hello%20World%21
[twilio_rest_making_calls]: http://www.twilio.com/docs/api/rest/making-calls
[twilio_rest_sending_sms]: http://www.twilio.com/docs/api/rest/sending-sms
[twilio_pricing]: http://www.twilio.com/pricing
[special_offer]: http://ahoy.twilio.com/azure
[twilio_libraries]: https://www.twilio.com/docs/libraries
[twiml]: http://www.twilio.com/docs/api/twiml
[twilio_api]: http://www.twilio.com/api
[try_twilio]: https://www.twilio.com/try-twilio
[twilio_console]:  https://www.twilio.com/console
[verify_phone]: https://www.twilio.com/console/phone-numbers/verified#
[twilio_api_documentation]: http://www.twilio.com/docs
[twilio_security_guidelines]: http://www.twilio.com/docs/security
[twilio_howtos]: http://www.twilio.com/docs/howto
[twilio_on_github]: https://github.com/twilio
[twilio_support]: http://www.twilio.com/help/contact
[twilio_quickstarts]: http://www.twilio.com/docs/quickstart
