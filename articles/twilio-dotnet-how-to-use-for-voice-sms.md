---
title: "tooUse aaaHow usługi Twilio głosowe i programu SMS (.NET) | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak komunikatów toomake połączeń telefonicznych i Wyślij wiadomość SMS z usługi interfejsu API usługi Twilio hello na platformie Azure. Przykłady kodu napisane w programie .NET."
services: 
documentationcenter: .net
author: devinrader
manager: twilio
editor: 
ms.assetid: 74d4f3c9-f1cb-4968-b744-36b32cd0e834
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 04/24/2015
ms.author: MicrosoftHelp@twilio.com
ms.openlocfilehash: f568da87ef15e9f540fee9674de31e983d4acb6d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-twilio-for-voice-and-sms-capabilities-from-azure"></a>Jak toouse usługi Twilio głosowe i możliwości programu SMS z platformy Azure
W tym przewodniku pokazano, jak tooperform typowych zadań programowania hello interfejsu API usługi Twilio usługi na platformie Azure. omówione scenariusze Hello obejmują tworzenie połączeń telefonicznych i wysyłanie wiadomości krótką wiadomość usługi (SMS). Aby uzyskać więcej informacji na temat usługi Twilio i komunikacja głosowa programu SMS w aplikacji, zobacz hello [następne kroki](#NextSteps) sekcji.

## <a id="WhatIs"></a>Co to jest usługi Twilio?
Usługi Twilio jest włączanie hello przyszłych komunikacji biznesowej, włączanie deweloperzy tooembed głosu VoIP i wiadomości do aplikacji. Zwirtualizuj one wszystkich infrastrukturę potrzebną w środowisku chmury, globalnych ujawnienie go za pośrednictwem platformy hello API komunikacji usługi Twilio. Aplikacje są proste toobuild i skalowalność. Kredyty elastyczność z płatność za rzeczywiste użycie ceny i korzystać z niej niezawodności chmury.

**Usługi Twilio głosu** umożliwia toomake Twojej aplikacji i odbieranie połączeń telefonicznych. **SMS usługi Twilio** umożliwia toosend Twojej aplikacji i odbieranie wiadomości SMS. **Klient usługi Twilio** pozwala toomake VoIP wywołania z dowolnego telefonu, tabletu lub przeglądarki i obsługuje WebRTC.

## <a id="Pricing"></a>Cennik usługi Twilio i oferty specjalne
Azure klienci otrzymają [oferta specjalna](http://www.twilio.com/azure): bezpłatnych 10 środków usługi Twilio po uaktualnieniu konta usługi Twilio. Środki tej usługi Twilio może być zastosowane tooany użycia usługi Twilio (10 środki równoważne toosending maksymalnie 1000 wiadomości SMS lub odbieranie się too1000 ruchu przychodzącego głosu minut w zależności od lokalizacji hello przeznaczenia numer i komunikatu lub wywołania telefonu). Realizowanie tego środki usługi Twilio i rozpocząć pracę w [ahoy.twilio.com/azure](http://ahoy.twilio.com/azure).

Usługi Twilio jest z usługą. Istnieją żadne opłaty konfiguracji, a konto zostanie zamknięte w dowolnym momencie. Można znaleźć więcej szczegółów na [cennik usługi Twilio](http://www.twilio.com/voice/pricing).

## <a id="Concepts"></a>Pojęcia
Witaj interfejsu API usługi Twilio jest interfejs API RESTful, która zapewnia funkcje programu SMS i komunikacja głosowa aplikacji. Klient biblioteki są dostępne w wielu językach; Aby uzyskać listę, zobacz [bibliotek interfejsu API usługi Twilio][twilio_libraries].

Kluczowe aspekty hello interfejsu API usługi Twilio są zleceń usługi Twilio i usługi Twilio Markup Language (TwiML).

### <a id="Verbs"></a>Usługi Twilio zlecenia
Witaj interfejs API korzysta z usługi Twilio zleceń; na przykład Witaj  **&lt;powiedzieć&gt;**  zlecenie powoduje, że usługi Twilio tooaudibly dostarczenia komunikatu w wywołaniu.

Witaj poniżej przedstawiono listę poleceń usługi Twilio.  Dowiedz się więcej o hello innych poleceń i możliwości za pośrednictwem [dokumentacji usługi Twilio Markup Language](http://www.twilio.com/docs/api/twiml).

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

## <a id="create_app"></a>Tworzenie aplikacji Azure
Azure aplikacji, która obsługuje aplikację usługi Twilio włączone nie różni się od innych aplikacji Azure. Dodawanie biblioteki .NET usługi Twilio hello i skonfigurować hello roli toouse hello .NET usługi Twilio biblioteki.
Informacje dotyczące tworzenia początkowej projektu platformy Azure, zobacz [Tworzenie projektu platformy Azure z programem Visual Studio][vs_project].

## <a id="configure_app"></a>Konfigurowanie bibliotek usługi Twilio toouse Twoja aplikacja
Usługi Twilio zawiera zestaw .NET pomocnika bibliotek, które otaczają różnych aspektów usługi Twilio tooprovide prosty i łatwy sposób toointeract hello interfejsu API REST usługi Twilio i klienta usługi Twilio toogenerate TwiML odpowiedzi.

Usługi Twilio zawiera pięć bibliotek dla deweloperów platformy .NET:
Biblioteka|Opis
---|---
Twilio.API|Hello podstawowe usługi Twilio biblioteki, która opakowuje hello interfejsu API REST usługi Twilio przyjazną biblioteki .NET. Ta biblioteka jest dostępna dla platformy .NET, Silverlight i Windows Phone 7.
Twilio.TwiML|Zawiera znacznik TwiML toogenerate przyjazną sposób .NET.
Twilio.MVC|Dla deweloperów przy użyciu platformy ASP.NET MVC Ta biblioteka zawiera TwilioController, TwiML ActionResult i atrybutu sprawdzania poprawności żądania.
Twilio.WebMatrix|Dla deweloperów korzystających bezpłatne narzędzie programistyczne WebMatrix firmy Microsoft Ta biblioteka zawiera pomocników składni Razor do wykonywania różnych akcji usługi Twilio.
Twilio.Client.Capability|Zawiera hello generatora tokenów możliwości do użycia z hello zestawu JavaScript SDK klienta usługi Twilio.

Należy pamiętać, że wszystkie biblioteki wymaga .NET 3.5, Silverlight 4 lub Windows Phone 7 lub nowszy.

Przykłady Hello podanych w tym przewodniku używać hello Twilio.API biblioteki.

Witaj bibliotek mogą być [zainstalowane przy użyciu rozszerzenia Menedżera pakietów NuGet hello](http://www.twilio.com/docs/csharp/install) dostępne dla programu Visual Studio 2010 w górę too2015.  Witaj kod źródłowy jest hostowana na [GitHub][twilio_github_repo], w tym typu Wiki, który zawiera pełną dokumentację dla przy użyciu bibliotek hello.

Domyślnie program Microsoft Visual Studio 2010 instaluje NuGet w wersji 1.2. Instalacja bibliotek usługi Twilio hello wymaga wersji 1.6 NuGet lub nowszej. Aby uzyskać informacje dotyczące instalowania lub aktualizowania NuGet, zobacz [http://nuget.org/][nuget].

> [!NOTE]
> tooinstall hello najnowszą wersję programu NuGet, należy najpierw odinstalować hello wersji załadowanego za pomocą hello Menedżera rozszerzeń programu Visual Studio. toodo tak, możesz uruchomić program Visual Studio jako administrator. W przeciwnym razie przycisk Odinstaluj hello jest wyłączona.
>
>

### <a id="use_nuget"></a>tooadd hello usługi Twilio biblioteki tooyour projektu Visual Studio:
1. Otwórz rozwiązanie w programie Visual Studio.
2. Kliknij prawym przyciskiem myszy **odwołania**.
3. Kliknij przycisk **Zarządzaj pakietami NuGet...**
4. Kliknij przycisk **Online**.
5. W hello wyszukiwania online wpisz *usługi twilio*.
6. Kliknij przycisk **zainstalować** na powitania pakietu usługi Twilio.

## <a id="howto_make_call"></a>Porady: wykonywanie połączenia wychodzące
Witaj poniżej pokazano, jak toomake wychodzące wywołanie przy użyciu hello **CallResource** klasy. Ten kod zawiera również hello tooreturn lokacja dostarczonych do usługi Twilio odpowiedzi usługi Twilio Markup Language (TwiML). Podstaw wartości hello **do** i **z** numerów telefonów i upewnij się, że sprawdzisz hello **z** numer telefonu dla konta usługi Twilio przed uruchomieniem kodu hello.

    // Use your account SID and authentication token instead
    // of hello placeholders shown here.
    const string accountSID = "your_twilio_account";
    const string authToken = "your_twilio_authentication_token";

    // Initialize hello TwilioClient.
    TwilioClient.Init(accountSID, authToken);

    // Use hello Twilio-provided site for hello TwiML response.
    var url = "http://twimlets.com/message";
    url = $"{url}?Message%5B0%5D=Hello%20World";

    // Set hello call From, To, and URL values toouse for hello call.
    // This sample uses hello sandbox number provided by
    // Twilio toomake hello call.
    var call = CallResource.Create(
        to: new PhoneNumber("+NNNNNNNNNN"),
        from: new PhoneNumber("NNNNNNNNNN"),
        url: new Uri(url));
        }

Aby uzyskać więcej informacji o parametrach hello przekazano toohello **CallResource.Create** metody, zobacz [http://www.twilio.com/docs/api/rest/making-calls][twilio_rest_making_calls].

Jak wspomniano, ten kod używa hello tooreturn lokacja dostarczonych do usługi Twilio TwiML odpowiedzi. Zamiast tego można użyć własnych lokacji tooprovide hello TwiML odpowiedzi. Aby uzyskać więcej informacji, zobacz [porady: Podaj TwiML odpowiedzi z własnej witryny sieci Web](#howto_provide_twiml_responses).

## <a id="howto_send_sms"></a>Porady: Wyślij wiadomość SMS
Witaj Poniższy zrzut ekranu przedstawia sposób hello toosend wiadomość SMS przy użyciu **MessageResource** klasy. Witaj **z** numer jest udostępniany przez usługi Twilio dla wersji próbnej kont toosend wiadomości SMS. Witaj **do** numer muszą być weryfikowane dla konta usługi Twilio, przed rozpoczęciem powitalne kodu.

    // Use your account SID and authentication token instead
    // of hello placeholders shown here.
    const string accountSID = "your_twilio_account";
    const string authToken = "your_twilio_authentication_token";

    // Initialize hello TwilioClient.
    TwilioClient.Init(accountSID, authToken);

    try
    {
        // Send an SMS message.
        var message = MessageResource.Create(
            to: new PhoneNumber("+12069419717"),
            from: new PhoneNumber("+14155992671"),
            body: "This is my SMS message.");
    }
    catch (TwilioException ex)
    {
        // An exception occurred making hello REST call
        Console.WriteLine(ex.Message);
    }

## <a id="howto_provide_twiml_responses"></a>Porady: Podaj TwiML odpowiedzi z własnej witryny sieci Web
Gdy aplikacja inicjuje toohello wywołania interfejsu API usługi Twilio — na przykład za pośrednictwem hello **CallResource.Create** metody — usługi Twilio wysyła adres URL tooan żądania, który jest oczekiwanym tooreturn TwiML odpowiedź. przykład Witaj w [porady: wykonania wywołania wychodzącego](#howto_make_call) używa hello adres URL udostępniony do usługi Twilio [http://twimlets.com/message] [ twimlet_message_url] tooreturn hello odpowiedzi.

> [!NOTE]
> Gdy TwiML jest przeznaczony do użytku przez usługi sieci web, można wyświetlić hello TwiML w przeglądarce. Na przykład kliknij pozycję [http://twimlets.com/message] [ twimlet_message_url] toosee pustą &lt;odpowiedzi&gt; element; inny przykład kliknij [http://twimlets.com/message ? Komunikat 5B0 %% 5 D = Hello % 20World](http://twimlets.com/message?Message%5B0%5D=Hello%20World) toosee &lt;odpowiedzi&gt; element, który zawiera &lt;powiedzieć&gt; elementu.
>
>

Zamiast polegania na adres URL udostępniony do usługi Twilio hello, można utworzyć własny adres URL w witrynie odpowiedzi HTTP. Można utworzyć witrynę hello w dowolnym języku, który zwraca odpowiedzi HTTP. W tym temacie założono, że będzie obsługiwać hello adresu URL, z ogólnego obsługi ASP.NET.

powitania po obsługi ASP.NET crafts odpowiedzi TwiML informacją **Hello World** na powitania wywołania.

    using System.Text;
    using System.Web;

    namespace WebRole1
    {
        /// <summary>
        /// Summary description for Handler1
        /// </summary>
        public class Handler1 : IHttpHandler
        {
            public void ProcessRequest(HttpContext context)
            {
                const string twiMLResponse =
                    "<Response><Say>Hello World.</Say></Response>";
                
                context.Response.Clear();
                context.Response.ContentType = "text/xml";
                context.Response.ContentEncoding = Encoding.UTF8;
                context.Response.Write(twiMLResponse);
                context.Response.End();
            }

            public bool IsReusable
            {
                get
                {
                    return false;
                }
            }
        }
    }
    
Jak widać w powyższym przykładzie hello hello TwiML odpowiedzi jest po prostu dokumentu XML. Biblioteka Twilio.TwiML Hello zawiera klasy, które generuje TwiML dla Ciebie. Hello poniższy przykład tworzy hello równoważne odpowiedzi, jak pokazano powyżej, ale używa hello **VoiceResponse** klasy.

    using System.Web;
    using Twilio.TwiML;

    namespace WebRole1
    {
        /// <summary>
        /// Summary description for Handler1
        /// </summary>
        public class Handler1 : IHttpHandler
        {

            public void ProcessRequest(HttpContext context)
            {
                var twiml = new VoiceResponse();
                twiml.Say("Hello World.");

                context.Response.Clear();
                context.Response.ContentType = "text/xml";
                context.Response.Write(twiml.ToString());
                context.Response.End();
            }

            public bool IsReusable
            {
                get
                {
                    return false;
                }
            }
        }
    }

Aby uzyskać więcej informacji o TwiML, zobacz [https://www.twilio.com/docs/api/twiml](https://www.twilio.com/docs/api/twiml).

Po skonfigurowaniu odpowiedzi TwiML tooprovide sposób można przekazać ten adres URL toohello **CallResource.Create** metody. Na przykład, jeśli masz aplikację sieci web o nazwie tooan MyTwiML wdrożona usługa w chmurze platformy Azure, a nazwa hello obsługi programu ASP.NET jest mytwiml.ashx, adres URL hello mogą zostać przekazane za**CallResource.Create** pokazane na powitania następującego kodu przykład:

    // This sample uses hello sandbox number provided by Twilio toomake hello call.
    // Place hello call.
    var call = CallResource.Create(
        to: new PhoneNumber("+NNNNNNNNNN"),
        from: new PhoneNumber("NNNNNNNNNN"),
        url: new Uri("http://<your_hosted_service>.cloudapp.net/MyTwiML/mytwiml.ashx"));
        }

Aby uzyskać dodatkowe informacje dotyczące korzystania z usługi Twilio na platformie Azure za pomocą programu ASP.NET, zobacz [jak toomake rozmowy telefonicznej z rolą sieci web na platformie Azure przy użyciu usługi Twilio][howto_phonecall_dotnet].

[!INCLUDE [twilio-additional-services-and-next-steps](../includes/twilio-additional-services-and-next-steps.md)]

[howto_phonecall_dotnet]: partner-twilio-cloud-services-dotnet-phone-call-web-role.md

[twimlet_message_url]: http://twimlets.com/message

[twilio_rest_making_calls]: http://www.twilio.com/docs/api/rest/making-calls

[vs_project]:http://msdn.microsoft.com/library/windowsazure/ee405487.aspx
[nuget]:http://nuget.org/
[twilio_github_repo]:https://github.com/twilio/twilio-csharp

[twilio_libraries]: https://www.twilio.com/docs/libraries
[twiml]: http://www.twilio.com/docs/api/twiml
[twilio_api]: http://www.twilio.com/api
[try_twilio]: https://www.twilio.com/try-twilio
[twilio_account]:  https://www.twilio.com/console
[verify_phone]: https://www.twilio.com/console/phone-numbers/verified
