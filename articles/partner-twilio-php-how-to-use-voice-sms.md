---
title: "tooUse aaaHow usługi Twilio głosowe i programu SMS (PHP) | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak komunikatów toomake połączeń telefonicznych i Wyślij wiadomość SMS z usługi interfejsu API usługi Twilio hello na platformie Azure. Przykłady kodu napisane w języku PHP."
documentationcenter: php
services: 
author: devinrader
manager: twilio
editor: mollybos
ms.assetid: 007f22e3-ac75-4868-8315-da000c2e0dd0
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 11/25/2014
ms.author: microsofthelp@twilio.com
ms.openlocfilehash: 9354df8de694826a0ff7ea92620ec4d7e5c2fd70
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-twilio-for-voice-and-sms-capabilities-in-php"></a>Jak tooUse usługi Twilio głosowe i możliwości programu SMS w języku PHP
W tym przewodniku pokazano, jak tooperform typowych zadań programowania hello interfejsu API usługi Twilio usługi na platformie Azure. omówione scenariusze Hello obejmują tworzenie połączeń telefonicznych i wysyłanie wiadomości krótką wiadomość usługi (SMS). Aby uzyskać więcej informacji na temat usługi Twilio i komunikacja głosowa programu SMS w aplikacji, zobacz hello [następne kroki](#NextSteps) sekcji.

## <a id="WhatIs"></a>Co to jest usługi Twilio?
Usługi Twilio jest włączanie hello przyszłych komunikacji biznesowej, włączanie deweloperzy tooembed głosu VoIP i wiadomości do aplikacji. Zwirtualizuj one wszystkich infrastrukturę potrzebną w środowisku chmury, globalnych ujawnienie go za pośrednictwem platformy hello API komunikacji usługi Twilio. Aplikacje są proste toobuild i skalowalność. Kredyty elastyczność Tobie płatności — jako Przejdź ceny i korzystać z niej niezawodności chmury.

**Usługi Twilio głosu** umożliwia toomake Twojej aplikacji i odbieranie połączeń telefonicznych. **SMS usługi Twilio** umożliwia toosend Twojej aplikacji i odbieranie wiadomości tekstowych. **Klient usługi Twilio** pozwala toomake VoIP wywołania z dowolnego telefonu, tabletu lub przeglądarki i obsługuje WebRTC.

## <a id="Pricing"></a>Cennik usługi Twilio i oferty specjalne
Azure klienci otrzymają [oferta specjalna](http://www.twilio.com/azure): bezpłatnych 10 środków usługi Twilio po uaktualnieniu konta usługi Twilio. Środki tej usługi Twilio może być zastosowane tooany użycia usługi Twilio (10 środki równoważne toosending maksymalnie 1000 wiadomości SMS lub odbieranie się too1000 ruchu przychodzącego głosu minut w zależności od lokalizacji hello przeznaczenia numer i komunikatu lub wywołania telefonu). Realizowanie tego środki usługi Twilio i rozpocząć pracę w: [http://ahoy.twilio.com/azure](http://ahoy.twilio.com/azure).

Usługi Twilio jest z usługą. Nie żadne opłaty konfiguracji i w dowolnej chwili możesz zamknąć konto. Można znaleźć więcej szczegółów na [cennik usługi Twilio][twilio_pricing].

## <a id="Concepts"></a>Pojęcia
Witaj interfejsu API usługi Twilio jest interfejs API RESTful, która zapewnia funkcje programu SMS i komunikacja głosowa aplikacji. Klient biblioteki są dostępne w wielu językach; Aby uzyskać listę, zobacz [bibliotek interfejsu API usługi Twilio][twilio_libraries].

Kluczowe aspekty hello interfejsu API usługi Twilio są zleceń usługi Twilio i usługi Twilio Markup Language (TwiML).

### <a id="Verbs"></a>Usługi Twilio zlecenia
Witaj interfejs API korzysta z usługi Twilio zleceń; na przykład Witaj  **&lt;powiedzieć&gt;**  zlecenie powoduje, że usługi Twilio tooaudibly dostarczenia komunikatu w wywołaniu.

Witaj poniżej przedstawiono listę poleceń usługi Twilio. Dowiedz się więcej o hello innych poleceń i możliwości za pośrednictwem [dokumentacji usługi Twilio Markup Language](http://www.twilio.com/docs/api/twiml).

* **&lt;Wybierania&gt;**: łączy hello wywołującego tooanother telefonu.
* **&lt;Zbierz&gt;**: zbiera wprowadzony na klawiaturze telefonu hello cyfr.
* **&lt;Rozłączanie&gt;**: kończy wywołanie.
* **&lt;Odtwórz&gt;**: odtwarzania pliku audio.
* **&lt;Wstrzymaj&gt;**: dyskretnie czeka na określoną liczbę sekund.
* **&lt;Rekord&gt;**: rejestruje wywołującego hello głosu i zwraca adres URL pliku zawierającego hello rejestrowania.
* **&lt;Przekieruj&gt;**: przekazuje kontrolę nad wywołania lub SMS toohello TwiML na inny adres URL.
* **&lt;Odrzuć&gt;**: odrzuca jako przychodzące wywołania numer usługi Twilio tooyour bez rozliczeń można
* **&lt;Powiedz&gt;**: Konwertuje tekst toospeech, które zostało utworzone w wywołaniu.
* **&lt;SMS&gt;**: wysyła wiadomość SMS.

### <a id="TwiML"></a>TwiML
Zestaw instrukcji oparte na języku XML, oparte na powitania usługi Twilio zlecenia, które informują usługi Twilio, jak jest TwiML tooprocess wywołania lub wiadomości SMS.

Na przykład powitania po TwiML może dokonać konwersji tekstu hello **Hello World** toospeech.

    <?xml version="1.0" encoding="UTF-8" ?>
    <Response>
       <Say>Hello World</Say>
    </Response>

Podczas wywołania aplikacji hello interfejsu API usługi Twilio, jeden z parametrów interfejsu API hello jest adres URL hello, która zwraca odpowiedź TwiML hello. Do celów programistycznych możesz użyć wprowadzone do usługi Twilio adresy URL tooprovide hello TwiML odpowiedzi są używane przez aplikacje. Może również udostępniać swoje własne adresy URL tooproduce hello TwiML odpowiedzi, a inną opcją jest toouse hello **TwiMLResponse** obiektu.

Aby uzyskać więcej informacji na temat usługi Twilio zlecenia i ich atrybuty oraz TwiML, zobacz [TwiML][twiml]. Aby uzyskać dodatkowe informacje na temat hello interfejsu API usługi Twilio, zobacz [interfejsu API usługi Twilio][twilio_api].

## <a id="CreateAccount"></a>Tworzenie konta usługi Twilio
Jeśli wszystko jest gotowe tooget konta usługi Twilio, zarejestruj się w [spróbuj usługi Twilio][try_twilio]. Można rozpoczynać bezpłatne konto, a następnie Uaktualnij swoje konto później.

Po utworzeniu konta dla konta usługi Twilio, otrzymasz Identyfikatora konta oraz tokenu uwierzytelniania. Zarówno będzie potrzebne toomake wywołania interfejsu API usługi Twilio. tooprevent nieautoryzowany dostęp do konta tooyour, bezpieczeństwo Twojego tokenu uwierzytelniania. Twój identyfikator konta i uwierzytelniania tokenu jest wyświetlana na powitania [strony konta usługi Twilio][twilio_account]w hello pola oznaczone **identyfikator SID konta** i **TOKEN uwierzytelniania**odpowiednio.

## <a id="create_app"></a>Tworzenie aplikacji PHP
Nie różni się od innych aplikacji PHP, który korzysta z usługi usługi Twilio hello się aplikacji PHP, która używa usługi usługi Twilio hello i działa na platformie Azure. Usługi Twilio usług są opartego na interfejsie REST i może zostać wywołana z PHP na kilka sposobów, w tym artykule koncentruje się na jak toouse usługi Twilio usług za pomocą [biblioteki usługi Twilio dla programów PHP i z usługi GitHub][twilio_php]. Aby uzyskać więcej informacji o korzystaniu z biblioteki usługi Twilio hello for PHP, zobacz [http://readthedocs.org/docs/twilio-php/en/latest/index.html][twilio_lib_docs].

Szczegółowe instrukcje umożliwiające tworzenie i wdrażanie tooAzure aplikacji usługi Twilio/PHP są dostępne pod adresem [jak tooMake rozwiązania usługi przy użyciu Twilio w aplikacji PHP na platformie Azure rozmowy telefonicznej][howto_phonecall_php].

## <a id="configure_app"></a>Konfigurowanie bibliotek usługi Twilio tooUse Twoja aplikacja
Biblioteki usługi Twilio hello toouse aplikacji dla programu PHP można skonfigurować na dwa sposoby:

1. Pobierz hello usługi Twilio biblioteki dla PHP z serwisu GitHub ([https://github.com/twilio/twilio-php][twilio_php]) i Dodaj hello **usług** katalogu tooyour aplikacji.
   
    — Lub —
2. Zainstaluj biblioteki usługi Twilio hello dla programów PHP w pakiecie GRUSZKOWA. Można zainstalować go z hello następującego polecenia:
   
        $ pear channel-discover twilio.github.com/pear
        $ pear install twilio/Services_Twilio

Po zainstalowaniu biblioteki usługi Twilio hello for PHP można dodać **require_once** instrukcji u góry hello programu PHP pliki tooreference hello biblioteki:

        require_once 'Services/Twilio.php';

Aby uzyskać więcej informacji, zobacz [https://github.com/twilio/twilio-php/blob/master/README.md][twilio_github_readme].

## <a id="howto_make_call"></a>Porady: wykonywanie połączenia wychodzące
Witaj poniżej pokazano, jak toomake wychodzące wywołanie przy użyciu hello **Services_Twilio** klasy. Ten kod zawiera również hello tooreturn lokacja dostarczonych do usługi Twilio odpowiedzi usługi Twilio Markup Language (TwiML). Podstaw wartości hello **z** i **do** numerów telefonów i upewnij się, że sprawdzisz hello **z** numer telefonu dla kodu hello toorunning poprzedniego konta usługi Twilio.

    // Include hello Twilio PHP library.
    require_once 'Services/Twilio.php';

    // Library version.
    $version = "2010-04-01";

    // Set your account ID and authentication token.
    $sid = "your_twilio_account_sid";
    $token = "your_twilio_authentication_token";

    // hello number of hello phone initiating hello hello call.
    $from_number = "NNNNNNNNNNN";

    // hello number of hello phone receiving call.
    $to_number = "NNNNNNNNNNN";

    // Use hello Twilio-provided site for hello TwiML response.
    $url = "http://twimlets.com/message";

    // hello phone message text.
    $message = "Hello world.";

    // Create hello call client.
    $client = new Services_Twilio($sid, $token, $version);

    //Make hello call.
    try
    {
        $call = $client->account->calls->create(
            $from_number, 
            $to_number,
              $url.'?Message='.urlencode($message)
        );
    }
    catch (Exception $e) 
    {
        echo 'Error: ' . $e->getMessage();
    }

Jak wspomniano, ten kod używa hello tooreturn lokacja dostarczonych do usługi Twilio TwiML odpowiedzi. Zamiast tego można użyć własnych lokacji tooprovide hello odpowiedzi TwiML; Aby uzyskać więcej informacji, zobacz [jak tooProvide TwiML odpowiedzi z Twoje własne witryny sieci Web](#howto_provide_twiml_responses).

* **Uwaga**: tootroubleshoot błędy sprawdzania poprawności certyfikatów SSL, zobacz [http://readthedocs.org/docs/twilio-php/en/latest/usage/rest.html][ssl_validation] 

## <a id="howto_send_sms"></a>Porady: Wyślij wiadomość SMS
Witaj poniżej pokazano, jak hello toosend wiadomość SMS przy użyciu **Services_Twilio** klasy. Witaj **z** numer jest udostępniany przez usługi Twilio dla wersji próbnej kont toosend wiadomości SMS. Witaj **do** należy sprawdzić liczbę dla kodu hello toorunning poprzedniego konta usługi Twilio.

    // Include hello Twilio PHP library.
    require_once 'Services/Twilio.php';

    // Library version.
    $version = "2010-04-01";

    // Set your account ID and authentication token.
    $sid = "your_twilio_account_sid";
    $token = "your_twilio_authentication_token";


    $from_number = "NNNNNNNNNNN"; // With trial account, texts can only be sent from your Twilio number.
    $to_number = "NNNNNNNNNNN";
    $message = "Hello world.";

    // Create hello call client.
    $client = new Services_Twilio($sid, $token, $version);

    // Send hello SMS message.
    try
    {
        $client->$client->account->messages->sendMessage($from_number, $to_number, $message);
    }
    catch (Exception $e) 
    {
        echo 'Error: ' . $e->getMessage();
    }

## <a id="howto_provide_twiml_responses"></a>Porady: Podaj TwiML odpowiedzi z własnej witryny sieci Web
Gdy aplikacja inicjuje toohello wywołania interfejsu API usługi Twilio, usługi Twilio będzie wysyłać adres URL tooa żądania, który jest oczekiwany tooreturn odpowiedzi TwiML. w powyższym przykładzie Hello używa adresu URL dostarczony do usługi Twilio hello [http://twimlets.com/message][twimlet_message_url]. (Podczas TwiML jest przeznaczony do użytku przez usługi Twilio, można wyświetlić hello go w przeglądarce. Na przykład kliknij pozycję [http://twimlets.com/message] [ twimlet_message_url] toosee pustą `<Response>` element; inny przykład kliknij [http://twimlets.com/message? Komunikat % 5B0 %5 D = Hello % 20World] [ twimlet_message_url_hello_world] toosee `<Response>` element, który zawiera `<Say>` elementu.)

Zamiast polegania na adres URL udostępniony do usługi Twilio hello, można utworzyć własne lokacji, która zwraca odpowiedzi HTTP. Można utworzyć witrynę hello w dowolnym języku, który zwraca odpowiedzi XML; w tym temacie założono, że należy używać PHP toocreate hello TwiML.

Witaj po PHP wyników strony w odpowiedzi TwiML stwierdzający, **Hello World** na powitania wywołania.

    <?php    
        header("content-type: text/xml");    
        echo "<?xml version=\"1.0\" encoding=\"UTF-8\"?>\n";
    ?>
    <Response>    
        <Say>Hello world.</Say>
    </Response>

Jak widać w powyższym przykładzie hello hello TwiML odpowiedzi jest po prostu dokumentu XML. Biblioteka usługi Twilio Hello dla programów PHP i zawiera klasy, które generuje TwiML dla Ciebie. w poniższym przykładzie Hello tworzy hello równoważne odpowiedzi, jak pokazano powyżej, ale używa hello **usług\_usługi Twilio\_Twiml** klasy w bibliotece usługi Twilio hello programu PHP:

    require_once('Services/Twilio.php');

    $response = new Services_Twilio_Twiml();
    $response->say("Hello world.");
    print $response;

Aby uzyskać więcej informacji o TwiML, zobacz [https://www.twilio.com/docs/api/twiml][twiml_reference]. 

Po utworzeniu strony PHP Konfigurowanie odpowiedzi TwiML tooprovide, użyj hello adres URL strony PHP hello hello adres URL przekazany hello `Services_Twilio->account->calls->create` metody. Na przykład, jeśli masz aplikację sieci Web o nazwie **MyTwiML** wdrożonej tooan Azure usługi hostowanej, a nazwa hello strony PHP hello jest **mytwiml.php**, adres URL, które mogą zostać przekazane za hello **Services_ Usługi Twilio -> konta -> wywołania -> Utwórz** pokazane na powitania poniższy przykład:

    require_once 'Services/Twilio.php';

    $sid = "your_twilio_account_sid";
    $token = "your_twilio_authentication_token";
    $from_number = "NNNNNNNNNNN";
    $to_number = "NNNNNNNNNNN";
    $url = "http://<your_hosted_service>.cloudapp.net/MyTwiML/mytwiml.php";

    // hello phone message text.
    $message = "Hello world.";

    $client = new Services_Twilio($sid, $token, "2010-04-01");

    try
    {
        $call = $client->account->calls->create(
            $from_number, 
            $to_number,
              $url.'?Message='.urlencode($message)
        );
    }
    catch (Exception $e) 
    {
        echo 'Error: ' . $e->getMessage();
    }

Aby uzyskać dodatkowe informacje dotyczące korzystania z usługi Twilio na platformie Azure za pomocą języka PHP, zobacz [jak tooMake rozwiązania usługi przy użyciu Twilio w aplikacji PHP na platformie Azure rozmowy telefonicznej][howto_phonecall_php].

## <a id="AdditionalServices"></a>Porady: korzystania z usługi Twilio dodatkowych usług
Ponadto przykłady toohello pokazane, usługi Twilio oferuje API sieci web można używać tooleverage dodatkowe usługi Twilio funkcji z aplikacji Azure. Aby uzyskać szczegółowe informacje, zobacz hello [dokumentacji interfejsu API usługi Twilio][twilio_api_documentation].

## <a id="NextSteps"></a>Następne kroki
Teraz, kiedy znasz już podstawy hello hello usługi usługi Twilio, wykonaj te więcej toolearn łącza:

* [Wytyczne dotyczące zabezpieczeń usługi Twilio][twilio_security_guidelines]
* [Porada usługi Twilio i przykładowy kod][twilio_howtos]
* [Samouczki usługi Twilio Szybki Start][twilio_quickstarts] 
* [Usługi Twilio w witrynie GitHub][twilio_on_github]
* [Porozmawiaj tooTwilio pomocy technicznej][twilio_support]

[twilio_php]: https://github.com/twilio/twilio-php
[twilio_lib_docs]: http://readthedocs.org/docs/twilio-php/en/latest/index.html
[twilio_github_readme]: https://github.com/twilio/twilio-php/blob/master/README.md
[ssl_validation]: http://readthedocs.org/docs/twilio-php/en/latest/usage/rest.html
[twilio_api_service]: https://api.twilio.com
[howto_phonecall_php]: partner-twilio-php-make-phone-call.md
[twilio_voice_request]: https://www.twilio.com/docs/api/twiml/twilio_request
[twilio_sms_request]: https://www.twilio.com/docs/api/twiml/sms/twilio_request
[misc_role_config_settings]: http://msdn.microsoft.com/library/windowsazure/hh690945.aspx
[twimlet_message_url]: http://twimlets.com/message
[twimlet_message_url_hello_world]: http://twimlets.com/message?Message%5B0%5D=Hello%20World
[twiml_reference]: https://www.twilio.com/docs/api/twiml
[twilio_pricing]: http://www.twilio.com/pricing
[special_offer]: http://ahoy.twilio.com/azure
[twilio_libraries]: https://www.twilio.com/docs/libraries
[twiml]: http://www.twilio.com/docs/api/twiml
[twilio_api]: http://www.twilio.com/api
[try_twilio]: https://www.twilio.com/try-twilio
[twilio_account]:  https://www.twilio.com/user/account
[verify_phone]: https://www.twilio.com/user/account/phone-numbers/verified#
[twilio_api_documentation]: http://www.twilio.com/api
[twilio_security_guidelines]: http://www.twilio.com/docs/security
[twilio_howtos]: http://www.twilio.com/docs/howto
[twilio_on_github]: https://github.com/twilio
[twilio_support]: http://www.twilio.com/help/contact
[twilio_quickstarts]: http://www.twilio.com/docs/quickstart
