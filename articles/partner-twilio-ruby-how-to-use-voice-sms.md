---
title: "tooUse aaaHow usługi Twilio głosowe i programu SMS (Ruby) | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak komunikatów toomake połączeń telefonicznych i Wyślij wiadomość SMS z usługi interfejsu API usługi Twilio hello na platformie Azure. Przykłady kodu napisane w języku Ruby."
services: 
documentationcenter: ruby
author: devinrader
manager: twilio
editor: 
ms.assetid: 60e512f6-fa47-47c0-aedc-f19bb72a1158
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: ruby
ms.topic: article
ms.date: 11/25/2014
ms.author: MicrosoftHelp@twilio.com
ms.openlocfilehash: aca5ccb4663ff03c9c1f39c848469415f06dfb45
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-twilio-for-voice-and-sms-capabilities-in-ruby"></a>Jak tooUse usługi Twilio głosowe i możliwości programu SMS w języku Ruby
W tym przewodniku pokazano, jak tooperform typowych zadań programowania hello interfejsu API usługi Twilio usługi na platformie Azure. omówione scenariusze Hello obejmują tworzenie połączeń telefonicznych i wysyłanie wiadomości krótką wiadomość usługi (SMS). Aby uzyskać więcej informacji na temat usługi Twilio i komunikacja głosowa programu SMS w aplikacji, zobacz hello [następne kroki](#NextSteps) sekcji.

## <a id="WhatIs"></a>Co to jest usługi Twilio?
Usługi Twilio jest telefonii API usługi sieci web, która umożliwia korzystanie z istniejących języków sieci web i umiejętności toobuild głosu aplikacji i programu SMS. Usługi Twilio jest usługą innych firm (nie funkcji platformy Azure i nie produkt firmy Microsoft).

**Usługi Twilio głosu** umożliwia toomake Twojej aplikacji i odbieranie połączeń telefonicznych. **SMS usługi Twilio** umożliwia toomake Twojej aplikacji i odbieranie wiadomości SMS. **Klient usługi Twilio** umożliwia aplikacji komunikację głosową tooenable przy użyciu istniejących połączeń internetowych, w tym przenośnych połączenia.

## <a id="Pricing"></a>Cennik usługi Twilio i oferty specjalne
Informacje o cenach usługi Twilio znajduje się w temacie [cennik usługi Twilio][twilio_pricing]. Azure klienci otrzymają [oferta specjalna][special_offer]: wolnego środki tekstów 1000 lub 1000 ruchu przychodzącego minut. toosign dla to oferty lub uzyskać więcej informacji, odwiedź stronę [http://ahoy.twilio.com/azure][special_offer].  

## <a id="Concepts"></a>Pojęcia
Witaj interfejsu API usługi Twilio jest interfejs API RESTful, która zapewnia funkcje programu SMS i komunikacja głosowa aplikacji. Klient biblioteki są dostępne w wielu językach; Aby uzyskać listę, zobacz [bibliotek interfejsu API usługi Twilio][twilio_libraries].

### <a id="TwiML"></a>TwiML
Zestaw instrukcji opartych na języku XML, które informują usługi Twilio, jak jest TwiML tooprocess wywołania lub wiadomości SMS.

Na przykład powitania po TwiML może dokonać konwersji tekstu hello **Hello World** toospeech.

    <?xml version="1.0" encoding="UTF-8" ?>
    <Response>
       <Say>Hello World</Say>
    </Response>

Wszystkie dokumenty TwiML mają `<Response>` jako ich elementu głównego. Z tego miejsca korzystając z usługi Twilio zleceń toodefine hello działanie aplikacji.

### <a id="Verbs"></a>TwiML zlecenia
Usługi Twilio zlecenia są tagi XML, które informują usługi Twilio, co to za**czy**. Na przykład Witaj  **&lt;powiedzieć&gt;**  zlecenie powoduje, że usługi Twilio tooaudibly dostarczenia komunikatu w wywołaniu. 

Witaj poniżej przedstawiono listę poleceń usługi Twilio.

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

Aby uzyskać więcej informacji na temat usługi Twilio zlecenia i ich atrybuty oraz TwiML, zobacz [TwiML][twiml]. Aby uzyskać dodatkowe informacje na temat hello interfejsu API usługi Twilio, zobacz [interfejsu API usługi Twilio][twilio_api].

## <a id="CreateAccount"></a>Tworzenie konta usługi Twilio
Jeśli wszystko jest gotowe tooget konta usługi Twilio, zarejestruj się w [spróbuj usługi Twilio][try_twilio]. Można rozpoczynać bezpłatne konto, a następnie Uaktualnij swoje konto później.

Po utworzeniu konta dla konta usługi Twilio, otrzymasz numer telefonu bezpłatnej aplikacji. Otrzymasz również identyfikatora SID konta, a token uwierzytelniania. Zarówno będzie potrzebne toomake wywołania interfejsu API usługi Twilio. tooprevent nieautoryzowany dostęp do konta tooyour, bezpieczeństwo Twojego tokenu uwierzytelniania. Identyfikator SID konta, a token uwierzytelniania jest wyświetlana na powitania [strony konta usługi Twilio][twilio_account]w hello pola oznaczone **identyfikator SID konta** i **TOKEN uwierzytelniania** , odpowiednio.

### <a id="VerifyPhoneNumbers"></a>Sprawdź numery telefonów
Dodanie wiele toohello są podane przez usługi Twilio można również sprawdzić numery kontroli (np. telefon komórkowy lub głównej numer telefonu) do użycia w aplikacji. 

Aby uzyskać informacje na temat tooverify numer telefonu, zobacz [Zarządzanie numery][verify_phone].

## <a id="create_app"></a>Tworzenie aplikacji Ruby
Nie różni się od innych dopisków fonetycznych aplikacji, która przy użyciu usługi usługi Twilio hello się dopisków fonetycznych aplikacji, która używa usługi usługi Twilio hello i działa na platformie Azure. Usługi Twilio usług są RESTful i może zostać wywołana z Ruby na kilka sposobów, w tym artykule koncentruje się na jak toouse usługi Twilio usług za pomocą [usługi Twilio biblioteki pomocnika dla środowiska Ruby][twilio_ruby].

Najpierw [konfiguracji nowej maszyny Wirtualnej systemu Linux Azure] [ azure_vm_setup] tooact jako hosta dla nowej aplikacji sieci web dopisków fonetycznych. Pomiń kroki hello obejmujący tworzenie hello szyny aplikacji, po prostu hello konfiguracji maszyny Wirtualnej. Upewnij się, że utworzono punkt końcowy z zewnętrznego portu 80 i wewnętrzny port 5000.

W poniższych przykładach hello, użyjemy [Sinatra][sinatra], ramy bardzo proste sieci web dla środowiska Ruby. Ale pewnością służy hello usługi Twilio pomocnika biblioteki dla środowiska Ruby z żadnych innych platforma sieci web, w tym Ruby na szyny.

SSH do nowej maszyny Wirtualnej i Utwórz katalog dla nowej aplikacji. W tym katalogu Utwórz plik o nazwie hello Gemfile i skopiuj następujące kodu do niej:

    source 'https://rubygems.org'
    gem 'sinatra'
    gem 'thin'

Uruchom w wierszu polecenia hello `bundle install`. Spowoduje to zainstalowanie hello zależności powyżej. Następnie utwórz plik o nazwie `web.rb`. Są to, gdzie znajduje się kod powitania dla aplikacji sieci web. Wklej hello następującego kodu do niej:

    require 'sinatra'

    get '/' do
        "Hello Monkey!"
    end

Na tym etapie należy hello można uruchomić polecenie hello `ruby web.rb -p 5000`. To spowoduje rozkręcenia serwera sieci web małej na port 5000. Powinno być możliwe toobrowse toothis aplikacji w przeglądarce, przechodząc na stronę hello adresu URL skonfigurowanych dla maszyny Wirtualnej Azure. Po osiągnięciu można aplikacji sieci web w przeglądarce hello, wszystko jest gotowe toostart tworzeniem aplikacji usługi Twilio.

## <a id="configure_app"></a>Skonfiguruj tooUse Twoja aplikacja usługi Twilio
Biblioteki usługi Twilio hello toouse aplikacji sieci web można skonfigurować, aktualizując Twojej `Gemfile` tooinclude ten wiersz:

    gem 'twilio-ruby'

W wierszu polecenia hello, uruchom `bundle install`. Teraz otworzyć `web.rb` i, w tym wierszem u góry hello:

    require 'twilio-ruby'

Wszystko jest teraz gotowe toouse hello usługi Twilio pomocnika biblioteki dla środowiska Ruby w aplikacji sieci web.

## <a id="howto_make_call"></a>Porady: wykonywanie połączenia wychodzące
powitania po pokazuje, jak wywołać toomake wychodzące. Kluczowe założenia obejmują przy użyciu biblioteki Pomocnik usługi Twilio powitania dla toomake dopisków fonetycznych, które wywołuje interfejs API REST i renderowania TwiML. Podstaw wartości hello **z** i **do** numerów telefonów i upewnij się, że sprawdzisz hello **z** numer telefonu dla kodu hello toorunning poprzedniego konta usługi Twilio.

Dodaj tę funkcję za`web.md`:

    # Set your account ID and authentication token.
    sid = "your_twilio_account_sid";
    token = "your_twilio_authentication_token";

    # hello number of hello phone initiating hello hello call.
    # This should either be a Twilio number or a number that you've verified
    from = "NNNNNNNNNNN";

    # hello number of hello phone receiving call.
    too= "NNNNNNNNNNN";

    # Use hello Twilio-provided site for hello TwiML response.
    url = "http://yourdomain.cloudapp.net/voice_url";

    get '/make_call' do
      # Create hello call client.
      client = Twilio::REST::Client.new(sid, token);

      # Make hello call
      client.account.calls.create(to: to, from: from, url: url)
    end

    post '/voice_url' do
      "<Response>
         <Say>Hello Monkey!</Say>
       </Response>"
    end

Jeśli otwarty up `http://yourdomain.cloudapp.net/make_call` w przeglądarce, która wyzwoli rozmowy telefonicznej hello toomake interfejsu API usługi Twilio hello wywołania toohello. Witaj pierwszych dwóch parametrów w `client.account.calls.create` dość wyjaśnień: numer wywołanie hello hello jest `from` i numer wywołanie hello hello jest `to`. 

Witaj trzeci parametr (`url`) jest adresem URL hello usługi Twilio żądań instrukcje tooget na jakie toodo, po wywołaniu hello jest połączony. W tym przypadku firma Microsoft konfiguracji, a adres URL (`http://yourdomain.cloudapp.net`) zwraca prosty dokumentu TwiML i używa hello `<Say>` wywołać toodo zlecenie niektóre tekst na mowę i wypowiedz odbieranie osoby toohello "Hello małp" hello.

## <a id="howto_recieve_sms"></a>Porady: Odbierz wiadomość SMS
W poprzednim przykładzie hello możemy zainicjować **wychodzących** rozmowy telefonicznej. Ten czas, Użyjmy hello numer telefonu, który usługi Twilio podał podczas tworzenia konta tooprocess **przychodzące** wiadomości SMS.

Po pierwsze, w dzienniku tooyour [pulpitu nawigacyjnego usługi Twilio][twilio_account]. Kliknij przycisk "Numery" w górnym nav hello, a następnie kliknij na powitania numer usługi Twilio, które zostały podane. Zostanie wyświetlone dwa adresy URL, które można skonfigurować. Adres URL żądania adresie URL żądania głosu i programu SMS. Są to adresy URL hello, wprowadzone wywołania usługi Twilio, gdy połączenie telefoniczne lub programu SMS są wysyłane tooyour numer. adresy URL Hello są również znane jako "punkty zaczepienia sieci web".

Chcielibyśmy tooprocess przychodzących wiadomości SMS, więc warto aktualizacja adresu URL hello zbyt`http://yourdomain.cloudapp.net/sms_url`. Przejdź dalej i kliknij przycisk Zapisz zmiany u dołu hello hello strony. Teraz, ponownie `web.rb` toohandle naszej aplikacji umożliwia programu, to:

    post '/sms_url' do
      "<Response>
         <Message>Hey, thanks for hello ping! Twilio and Azure rock!</Message>
       </Response>"
    end

Po wprowadzeniu zmian hello, upewnij się, że początkowy toore aplikacji sieci web. Teraz Wyjmij telefonu i wysyłanie SMS tooyour numer usługi Twilio. Należy niezwłocznie pobrać odpowiedzi programu SMS z informacją, "Witaj, Dziękujemy za ping Witaj! Skale usługi Twilio i na platformie Azure! ".

## <a id="additional_services"></a>Porady: korzystania z usługi Twilio dodatkowych usług
Ponadto przykłady toohello pokazane, usługi Twilio oferuje API sieci web można używać tooleverage dodatkowe usługi Twilio funkcji z aplikacji Azure. Aby uzyskać szczegółowe informacje, zobacz hello [dokumentacji interfejsu API usługi Twilio][twilio_api_documentation].

### <a id="NextSteps"></a>Następne kroki
Teraz, kiedy znasz już podstawy hello hello usługi usługi Twilio, wykonaj te więcej toolearn łącza:

* [Wytyczne dotyczące zabezpieczeń usługi Twilio][twilio_security_guidelines]
* [HowTos usługi Twilio i przykładowy kod][twilio_howtos]
* [Samouczki usługi Twilio Szybki Start][twilio_quickstarts] 
* [Usługi Twilio w witrynie GitHub][twilio_on_github]
* [Porozmawiaj tooTwilio pomocy technicznej][twilio_support]

[twilio_ruby]: https://www.twilio.com/docs/ruby/install





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
[sinatra]: http://www.sinatrarb.com/
[azure_vm_setup]: http://www.windowsazure.com/develop/ruby/tutorials/web-app-with-linux-vm/
