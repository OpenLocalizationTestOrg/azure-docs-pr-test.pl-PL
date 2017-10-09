---
title: "tooUse aaaHow usługi Twilio głosowe i programu SMS (Python) | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak komunikatów toomake połączeń telefonicznych i Wyślij wiadomość SMS z usługi interfejsu API usługi Twilio hello na platformie Azure. Przykłady kodu napisane w języku Python."
services: 
documentationcenter: python
author: devinrader
manager: twilio
editor: 
ms.assetid: 561bc75b-4ac4-40ba-bcba-48e901f27cc3
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 02/19/2015
ms.author: MicrosoftHelp@twilio.com
ms.openlocfilehash: 1f16a107d95c94589b8d61a0971c5b62d639c571
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-twilio-for-voice-and-sms-capabilities-in-python"></a>Jak tooUse usługi Twilio głosowe i możliwości programu SMS w języku Python
W tym przewodniku pokazano, jak tooperform typowych zadań programowania hello interfejsu API usługi Twilio usługi na platformie Azure. omówione scenariusze Hello obejmują tworzenie połączeń telefonicznych i wysyłanie wiadomości krótką wiadomość usługi (SMS). Aby uzyskać więcej informacji na temat usługi Twilio i komunikacja głosowa programu SMS w aplikacji, zobacz hello [następne kroki](#NextSteps) sekcji.

## <a id="WhatIs"></a>Co to jest usługi Twilio?
Usługi Twilio jest włączanie hello przyszłych komunikacji biznesowej, włączanie deweloperzy tooembed głosu VoIP i wiadomości do aplikacji. Zwirtualizuj one wszystkich infrastrukturę potrzebną w środowisku chmury, globalnych ujawnienie go za pośrednictwem platformy hello API komunikacji usługi Twilio. Aplikacje są proste toobuild i skalowalność. Kredyty elastyczność Tobie płatności — jako Przejdź ceny i korzystać z niej niezawodności chmury.

**Usługi Twilio głosu** umożliwia toomake Twojej aplikacji i odbieranie połączeń telefonicznych.
**SMS usługi Twilio** umożliwia toosend Twojej aplikacji i odbieranie wiadomości tekstowych.
**Klient usługi Twilio** pozwala toomake VoIP wywołania z dowolnego telefonu, tabletu lub przeglądarki i obsługuje WebRTC.

## <a id="Pricing"></a>Cennik usługi Twilio i oferty specjalne
Azure klienci otrzymają [oferta specjalna] [ special_offer] 10 $ środków usługi Twilio po uaktualnieniu konta usługi Twilio. Środki tej usługi Twilio może być zastosowane tooany użycia usługi Twilio (10 środki równoważne toosending maksymalnie 1000 wiadomości SMS lub odbieranie się too1000 ruchu przychodzącego głosu minut w zależności od lokalizacji hello przeznaczenia numer i komunikatu lub wywołania telefonu). Zrealizować to [środki usługi Twilio] [ special_offer] i rozpocząć pracę.

Usługi Twilio jest z usługą. Nie żadne opłaty konfiguracji i w dowolnej chwili możesz zamknąć konto. Można znaleźć więcej szczegółów na [cennik usługi Twilio][twilio_pricing].

## <a id="Concepts"></a>Pojęcia
Witaj interfejsu API usługi Twilio jest interfejs API RESTful, która zapewnia funkcje programu SMS i komunikacja głosowa aplikacji. Klient biblioteki są dostępne w wielu językach; Aby uzyskać listę, zobacz [bibliotek interfejsu API usługi Twilio][twilio_libraries].

Kluczowe aspekty hello interfejsu API usługi Twilio są zleceń usługi Twilio i usługi Twilio Markup Language (TwiML).

### <a id="Verbs"></a>Usługi Twilio zlecenia
Witaj interfejs API korzysta z usługi Twilio zleceń; na przykład Witaj  **&lt;powiedzieć&gt;**  zlecenie powoduje, że usługi Twilio tooaudibly dostarczenia komunikatu w wywołaniu.

Witaj poniżej przedstawiono listę poleceń usługi Twilio. Dowiedz się więcej o hello innych poleceń i możliwości za pośrednictwem [dokumentacji usługi Twilio Markup Language][twiml].

* **&lt;Wybierania&gt;**: łączy hello wywołującego tooanother telefonu.
* **&lt;Zbierz&gt;**: zbiera wprowadzony na klawiaturze telefonu hello cyfr.
* **&lt;Rozłączanie&gt;**: kończy wywołanie.
* **&lt;Wstrzymaj&gt;**: dyskretnie czeka na określoną liczbę sekund.
* **&lt;Odtwórz&gt;**: odtwarzania pliku audio.
* **&lt;Kolejka&gt;**: Dodaj kolejkę tooa hello obiekty wywołujące.
* **&lt;Rekord&gt;**: rejestruje głosu hello hello wywołującego i zwraca adres URL pliku zawierającego hello rejestrowania.
* **&lt;Przekieruj&gt;**: przekazuje kontrolę nad wywołania lub SMS toohello TwiML na inny adres URL.
* **&lt;Odrzuć&gt;**: odrzuca jako przychodzące wywołania numer usługi Twilio tooyour bez rozliczeń można.
* **&lt;Powiedz&gt;**: Konwertuje tekst toospeech, które zostało utworzone w wywołaniu.
* **&lt;SMS&gt;**: wysyła wiadomość SMS.

### <a id="TwiML"></a>TwiML
Zestaw instrukcji oparte na języku XML, oparte na powitania usługi Twilio zlecenia, które informują usługi Twilio, jak jest TwiML tooprocess wywołania lub wiadomości SMS.

Na przykład powitania po TwiML może dokonać konwersji tekstu hello **Hello World** toospeech.

    <?xml version="1.0" encoding="UTF-8" ?>
    <Response>
      <Say>Hello World</Say>
    </Response>

Podczas wywołania aplikacji hello interfejsu API usługi Twilio, jeden z parametrów interfejsu API hello jest adres URL hello, która zwraca odpowiedź TwiML hello. Do celów programistycznych możesz użyć wprowadzone do usługi Twilio adresy URL tooprovide hello TwiML odpowiedzi są używane przez aplikacje. Może również udostępniać swoje własne adresy URL tooproduce hello TwiML odpowiedzi, a inną opcją jest toouse hello `TwiMLResponse` obiektu.

Aby uzyskać więcej informacji na temat usługi Twilio zlecenia i ich atrybuty oraz TwiML, zobacz [TwiML][twiml]. Aby uzyskać dodatkowe informacje na temat hello interfejsu API usługi Twilio, zobacz [interfejsu API usługi Twilio][twilio_api].

## <a id="CreateAccount"></a>Tworzenie konta usługi Twilio
Gdy wszystko jest gotowe tooget konta usługi Twilio, zarejestruj się w [spróbuj usługi Twilio][try_twilio]. Można rozpoczynać bezpłatne konto, a następnie Uaktualnij swoje konto później.

Po utworzeniu konta dla konta usługi Twilio, otrzymasz identyfikator SID konta i tokenu uwierzytelniania. Zarówno będzie potrzebne toomake wywołania interfejsu API usługi Twilio. tooprevent nieautoryzowany dostęp do konta tooyour, bezpieczeństwo Twojego tokenu uwierzytelniania. Identyfikator SID konta, a token uwierzytelniania jest wyświetlana w hello [usługi Twilio Console][twilio_console]w hello pola oznaczone **identyfikator SID konta** i **TOKEN uwierzytelniania**odpowiednio.

## <a id="create_app"></a>Tworzenie aplikacji Python
Nie różni się od innych aplikacji Python, korzystającej z usługi usługi Twilio hello się aplikacji Python, która używa usługi usługi Twilio hello i działa na platformie Azure. Usługi Twilio usług są opartego na interfejsie REST i może zostać wywołana z Python na kilka sposobów, w tym artykule koncentruje się na jak toouse usługi Twilio usług za pomocą [biblioteki usługi Twilio dla języka Python z witryny GitHub][twilio_python]. Aby uzyskać więcej informacji o używaniu biblioteki usługi Twilio powitania dla języka Python, zobacz [http://readthedocs.org/docs/twilio-python/en/latest/index.html][twilio_lib_docs].

Pierwsza strona, [konfiguracji nowej maszyny Wirtualnej systemu Linux Azure] [azure_vm_setup] tooact jako hosta dla nowej aplikacji sieci web języka Python. Po hello maszyna wirtualna jest uruchomiona, należy tooexpose aplikacji na port publiczny zgodnie z poniższym opisem.

### <a name="add-an-incoming-rule"></a>Dodawanie reguły przychodzące
  1. Przejdź toohello [sieciowej grupy zabezpieczeń] [azure_nsg] strony.
  2. Wybierz hello grupy zabezpieczeń sieci, która odpowiada z maszyny wirtualnej.
  3. Dodaj i **reguły wychodzące** dla **port 80**. Należy się tooallow przychodzące z dowolnego adresu.

### <a name="set-hello-dns-name-label"></a>Ustaw hello etykieta nazwy DNS
  1. Przejdź toohello [hello publicznych adresów IP] [azure_ips] strony.
  2. Wybierz hello publicznego adresu IP tego correspends z maszyny wirtualnej.
  3. Zestaw hello **etykieta nazwy DNS** w hello **konfiguracji** sekcji. W przypadku hello w tym przykładzie ekran będzie wyglądać następująco *your etykieta domeny*. centralus.cloudapp.azure.com

Po tooconnect za pośrednictwem toohello SSH maszyny wirtualnej, można zainstalować hello platforma sieci Web dowolnego (Witaj dwie najbardziej dobrze znany jest Python [Flask](http://flask.pocoo.org/) i [Django](https://www.djangoproject.com)). Każdej z nich można zainstalować tylko uruchamiając hello `pip install` polecenia.

Należy pamiętać o tym, czy został skonfigurowany ruchu tooallow maszyn wirtualnych hello tylko na porcie 80. Upewnij się, że toouse aplikacji hello tooconfigure tego portu.

## <a id="configure_app"></a>Konfigurowanie bibliotek usługi Twilio tooUse Twoja aplikacja
Biblioteki usługi Twilio hello toouse aplikacji dla języka Python można skonfigurować na dwa sposoby:

* Zainstaluj biblioteki usługi Twilio powitania dla języka Python w pakiecie narzędzia Pip. Można zainstalować go z hello następującego polecenia:
   
        $ pip install twilio

    — Lub —

* Pobierz hello usługi Twilio biblioteki dla języka Python z witryny GitHub ([https://github.com/twilio/twilio-python][twilio_python]) i zainstaluj go w następujący sposób:

        $ python setup.py install

Po zainstalowaniu hello usługi Twilio biblioteki dla języka Python, możesz następnie `import` go w plikach języka Python:

        import twilio

Aby uzyskać więcej informacji, zobacz [https://github.com/twilio/twilio-python/blob/master/README.md][twilio_github_readme].

## <a id="howto_make_call"></a>Porady: wykonywanie połączenia wychodzące
powitania po pokazuje, jak wywołać toomake wychodzące. Ten kod zawiera również hello tooreturn lokacja dostarczonych do usługi Twilio odpowiedzi usługi Twilio Markup Language (TwiML). Podstaw wartości hello **from_number** i **to_number** numerów telefonów i upewnij się, że zostały zweryfikowane hello **from_number** numer telefonu dla konta usługi Twilio przed hello kodu.

    from urllib.parse import urlencode

    # Import hello Twilio Python Client.
    from twilio.rest import TwilioRestClient

    # Set your account ID and authentication token.
    account_sid = "your_twilio_account_sid"
    auth_token = "your_twilio_authentication_token"

    # hello number of hello phone initiating hello hello call.
    # This should either be a Twilio number or a number that you've verified
    from_number = "NNNNNNNNNNN"

    # hello number of hello phone receiving call.
    to_number = "NNNNNNNNNNN"

    # Use hello Twilio-provided site for hello TwiML response.
    url = "http://twimlets.com/message?"

    # hello phone message text.
    message = "Hello world."

    # Initialize hello Twilio client.
    client = TwilioRestClient(account_sid, auth_token)

    # Make hello call.
    call = client.calls.create(to=to_number,
                               from_=from_number,
                               url=url + urlencode({'Message': message}))
    print(call.sid)

Jak wspomniano, ten kod używa hello tooreturn lokacja dostarczonych do usługi Twilio TwiML odpowiedzi. Zamiast tego można użyć własnych lokacji tooprovide hello odpowiedzi TwiML; Aby uzyskać więcej informacji, zobacz [jak tooProvide TwiML odpowiedzi z Twoje własne witryny sieci Web](#howto_provide_twiml_responses).

## <a id="howto_send_sms"></a>Porady: Wyślij wiadomość SMS
Witaj poniżej pokazano, jak hello toosend wiadomość SMS przy użyciu `TwilioRestClient` klasy. Witaj **from_number** numer jest udostępniany przez usługi Twilio dla wersji próbnej kont toosend wiadomości SMS. Witaj **to_number** numer muszą być weryfikowane dla konta usługi Twilio przed uruchomieniem kodu hello.

    # Import hello Twilio Python Client.
    from twilio.rest import TwilioRestClient

    # Set your account ID and authentication token.
    account_sid = "your_twilio_account_sid"
    auth_token = "your_twilio_authentication_token"

    from_number = "NNNNNNNNNNN"  # With trial account, texts can only be sent from your Twilio number.
    to_number = "NNNNNNNNNNN"
    message = "Hello world."

    # Initialize hello Twilio client.
    client = TwilioRestClient(account_sid, auth_token)

    # Send hello SMS message.
    message = client.messages.create(to=to_number,
                                     from_=from_number,
                                     body=message)

## <a id="howto_provide_twiml_responses"></a>Porady: Podaj TwiML odpowiedzi z własnej witryny sieci Web
Gdy aplikacja inicjuje toohello wywołania interfejsu API usługi Twilio, usługi Twilio będzie wysyłać adres URL tooa żądania, który jest oczekiwany tooreturn odpowiedzi TwiML. w powyższym przykładzie Hello używa adresu URL dostarczony do usługi Twilio hello [http://twimlets.com/message][twimlet_message_url]. (Podczas TwiML jest przeznaczony do użytku przez usługi Twilio, można wyświetlić ją w przeglądarce. Na przykład kliknij pozycję [http://twimlets.com/message] [ twimlet_message_url] toosee pustą `<Response>` element; inny przykład kliknij [http://twimlets.com/message? Komunikat % 5B0 %5 D = Hello % 20World] [ twimlet_message_url_hello_world] toosee `<Response>` element, który zawiera `<Say>` elementu.)

Zamiast polegania na adres URL udostępniony do usługi Twilio hello, można utworzyć własne lokacji, która zwraca odpowiedzi HTTP. Można utworzyć witrynę hello w dowolnym języku, który zwraca odpowiedzi XML; w tym temacie założono, że będziesz używać języka Python toocreate hello TwiML.

Hello następujące przykłady dane wyjściowe obejmują odpowiedzi TwiML informacją **Hello World** na powitania wywołania.

Z Flask:

    from flask import Response
    @app.route("/")
    def hello():
        xml = '<Response><Say>Hello world.</Say></Response>'
        return Response(xml, mimetype='text/xml')

Przy użyciu platformy Django:

    from django.http import HttpResponse
    def hello(request):
        xml = '<Response><Say>Hello world.</Say></Response>'
        return HttpResponse(xml, content_type='text/xml')

Jak widać w powyższym przykładzie hello hello TwiML odpowiedzi jest po prostu dokumentu XML. Biblioteka usługi Twilio Hello dla języka Python zawiera klasy, które generuje TwiML dla Ciebie. Hello poniższy przykład tworzy hello równoważne odpowiedzi, jak pokazano powyżej, ale używa hello `twiml` modułu w bibliotece usługi Twilio hello for Python:

    from twilio import twiml

    response = twiml.Response()
    response.say("Hello world.")
    print(str(response))

Aby uzyskać więcej informacji o TwiML, zobacz [https://www.twilio.com/docs/api/twiml][twiml_reference].

Po utworzeniu aplikacji Python Konfigurowanie odpowiedzi TwiML tooprovide, użyj hello adres URL aplikacji hello hello adres URL przekazany hello `client.calls.create` metody. Na przykład, jeśli masz aplikację sieci Web o nazwie **MyTwiML** usługi hostowanej wdrożonej tooan Azure, możesz użyć adresu url jako elementu webhook pokazane na powitania poniższy przykład:

    from twilio.rest import TwilioRestClient

    account_sid = "your_twilio_account_sid"
    auth_token = "your_twilio_authentication_token"
    from_number = "NNNNNNNNNNN"
    to_number = "NNNNNNNNNNN"
    url = "http://your-domain-label.centralus.cloudapp.azure.com/MyTwiML/"

    # Initialize hello Twilio client.
    client = TwilioRestClient(account_sid, auth_token)

    # Make hello call.
    call = client.calls.create(to=to_number,
                               from_=from_number,
                               url=url)
    print(call.sid)

## <a id="AdditionalServices"></a>Porady: korzystania z usługi Twilio dodatkowych usług
Ponadto przykłady toohello pokazane, usługi Twilio oferuje API sieci web można używać tooleverage dodatkowe usługi Twilio funkcji z aplikacji Azure. Aby uzyskać szczegółowe informacje, zobacz hello [dokumentacji interfejsu API usługi Twilio][twilio_api].

## <a id="NextSteps"></a>Następne kroki
Teraz, kiedy znasz już podstawy hello hello usługi usługi Twilio, wykonaj te więcej toolearn łącza:

* [Wytyczne dotyczące zabezpieczeń usługi Twilio][twilio_security_guidelines]
* [Porada usługi Twilio prowadnice i przykładowy kod][twilio_howtos]
* [Samouczki usługi Twilio Szybki Start][twilio_quickstarts]
* [Usługi Twilio w witrynie GitHub][twilio_on_github]
* [Porozmawiaj tooTwilio pomocy technicznej][twilio_support]

[special_offer]: http://ahoy.twilio.com/azure
[twilio_python]: https://github.com/twilio/twilio-python
[twilio_lib_docs]: http://readthedocs.org/docs/twilio-python/en/latest/index.html
[twilio_github_readme]: https://github.com/twilio/twilio-python/blob/master/README.md

[twimlet_message_url]: http://twimlets.com/message
[twimlet_message_url_hello_world]: http://twimlets.com/message?Message%5B0%5D=Hello%20World
[twiml_reference]: https://www.twilio.com/docs/api/twiml
[twilio_pricing]: http://www.twilio.com/pricing

[twilio_libraries]: https://www.twilio.com/docs/libraries
[twiml]: http://www.twilio.com/docs/api/twiml
[twilio_api]: http://www.twilio.com/api
[try_twilio]: https://www.twilio.com/try-twilio
[twilio_console]:  https://www.twilio.com/console
[twilio_security_guidelines]: http://www.twilio.com/docs/security
[twilio_howtos]: http://www.twilio.com/docs/howto
[twilio_on_github]: https://github.com/twilio
[twilio_support]: http://www.twilio.com/help/contact
[twilio_quickstarts]: http://www.twilio.com/docs/quickstart
