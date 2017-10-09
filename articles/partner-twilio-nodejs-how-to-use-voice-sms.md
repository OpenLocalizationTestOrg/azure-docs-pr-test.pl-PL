---
title: "aaaUsing usługi Twilio głosowych, VoIP i wiadomości SMS na platformie Azure"
description: "Dowiedz się, jak komunikatów toomake połączeń telefonicznych i Wyślij wiadomość SMS z usługi interfejsu API usługi Twilio hello na platformie Azure. Przykłady kodu napisane w środowisku Node.js."
services: 
documentationcenter: nodejs
author: devinrader
manager: wpickett
editor: 
ms.assetid: f558cbbd-13d2-416f-b9b1-33a99c426af9
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 11/25/2014
ms.author: wpickett
ms.openlocfilehash: 6c44d60e217fcdf51e69fd2a8197f979afbb507a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="using-twilio-for-voice-voip-and-sms-messaging-in-azure"></a>Przy użyciu usługi Twilio głosowych, VoIP i wiadomości SMS na platformie Azure
W tym przewodniku pokazano, jak toobuild aplikacje, które do komunikacji z usługi Twilio i node.js na platformie Azure.

<a id="whatis"/>

## <a name="what-is-twilio"></a>Co to jest usługi Twilio?
Usługi Twilio to platforma interfejsu API, która ułatwia deweloperom toomake i odbieranie połączeń telefonicznych, wysyłanie i odbieranie wiadomości tekstowych i osadzić VoIP wywołanie przeglądarki i natywnych aplikacji dla urządzeń przenośnych. Załóżmy krótko przekazywane jak to działa przed rozpoczęciem pracy.

### <a name="receiving-calls-and-text-messages"></a>Odbieranie wywołań i wiadomości SMS
Usługi Twilio umożliwia deweloperom stosowanie zbyt[zakupu numery telefonów programowalny] [ purchase_phone] które mogą być używane tooboth wysyłać i odbierać wywołania i wiadomości SMS. W odebrania połączenia przychodzącego lub wiadomości SMS numer usługi Twilio usługi Twilio wyśle aplikacji sieci web HTTP POST lub GET żądania, zapytaniem instrukcje w sposób toohandle hello połączenia lub wiadomości SMS. Serwer będzie odpowiadać na żądania HTTP przez tooTwilio z [TwiML][twiml], prosty zestaw tagi XML, które zawierają instrukcje na temat toohandle połączenia lub wiadomości SMS. Przykłady TwiML zostaną podane w chwilę.

### <a name="making-calls-and-sending-text-messages"></a>Wykonywanie wywołań i wysyłanie wiadomości tekstowych
Dzięki toohello żądań HTTP interfejsu API usługi sieci web usługi Twilio, deweloperzy mogą wiadomości tekstowych lub zainicjować wychodzących połączeń telefonicznych. Wychodzący deweloperów hello należy także określić adres URL, który zwraca TwiML instrukcje dotyczące sposobu hello toohandle wychodzącego wywołać po podłączeniu.

### <a name="embedding-voip-capabilities-in-ui-code-javascript-ios-or-android"></a>Osadzanie możliwości VoIP w kodzie interfejsu użytkownika (JavaScript, iOS lub Android)
Usługi Twilio zawiera zestaw SDK klienta, który można przekształcić w dowolnej przeglądarki sieci web, aplikacji dla systemu iOS lub aplikacji systemu Android telefonu VoIP. W tym artykule, firma Microsoft będzie skupić się na temat toouse VoIP wywoływania w przeglądarce hello. W przypadku dodawania toohello *usługi Twilio JavaScript SDK* uruchomiony w przeglądarce hello, aplikację po stronie serwera (naszej aplikacji node.js) musi być używane tooissue toohello "możliwości tokenu" JavaScript klienta. Więcej o korzystaniu z node.js VoIP [na blogu deweloperów usługi Twilio hello][voipnode].

<a id="signup"/>

## <a name="sign-up-for-twilio-microsoft-discount"></a>Utwórz konto usługi Twilio (Microsoft rabat)
Przed rozpoczęciem korzystania z usługi Twilio usługi, należy najpierw [konto][signup]. Microsoft Azure klienci uzyskać rabat specjalne — [można toosign się tutaj][signup]!

<a id="azuresite"/>

## <a name="create-and-deploy-a-nodejs-azure-website"></a>Tworzenie i wdrażanie witryny sieci Web Azure node.js
Następnie należy toocreate witryny sieci Web node.js działających na platformie Azure. [Witaj oficjalnej dokumentacji dla tej czynności znajduje się tutaj][azure_new_site]. Na wysokim poziomie będzie realizacji hello następujące czynności:

* Podczas tworzenia konta platformy Azure, jeśli nie masz już
* Przy użyciu toocreate konsoli administratora usługi Azure hello nowej witryny sieci Web
* Dodawanie obsługi kontroli źródła (zakładamy, że używane git)
* Tworzenie pliku `server.js` z aplikacją sieci web node.js proste
* Wdrażanie tego tooAzure prostej aplikacji

<a id="twiliomodule"/>

## <a name="configure-hello-twilio-module"></a>Skonfiguruj hello modułu usługi Twilio
Następnie Rozpoczniemy toowrite aplikacji node.js proste, co sprawia, że użycie hello interfejsu API usługi Twilio. Zanim zaczniemy, potrzebujemy tooconfigure naszych poświadczenia konta usługi Twilio.

### <a name="configuring-twilio-credentials-in-system-environment-variables"></a>Konfigurowanie poświadczeń usługi Twilio w zmiennych środowiskowych systemu
W kolejności toomake uwierzytelnione żądania do zaplecza usługi Twilio hello potrzebujemy naszych identyfikatora SID konta i uwierzytelniania tokenu, która funkcja jako hello nazwę użytkownika i hasło określone dla naszego konta usługi Twilio. Witaj najbezpieczniejszą tooconfigure sposób ich do użytku z modułu węzeł hello na platformie Azure jest za pomocą zmiennych środowiskowych systemu, które można ustawić bezpośrednio w konsoli administracyjnej Azure hello.

Wybierz witrynę sieci Web node.js, a następnie kliknij łącze "Konfiguruj" hello.  Przewiń w dół bit zobaczysz obszaru, w którym można ustawić właściwości konfiguracji dla aplikacji.  Wprowadź poświadczenia konta usługi Twilio ([znaleziono w konsoli usługi Twilio][twilio_console]) jak pokazano — upewnij się, że tooname je `TWILIO_ACCOUNT_SID` i `TWILIO_AUTH_TOKEN`odpowiednio:

![Konsola administracyjna platformy Azure][azure-admin-console]

Po skonfigurowaniu tych zmiennych, ponownie uruchom aplikację w hello konsoli platformy Azure.

### <a name="declaring-hello-twilio-module-in-packagejson"></a>Deklarowanie hello usługi Twilio modułu w pliku package.json
Następnie potrzebujemy toocreate package.json toomanage naszych węzeł zależności modułu za pośrednictwem [npm]. Na powitania sam poziom jako hello `server.js` pliku utworzonego w hello *Azure/node.js* samouczek, Utwórz plik o nazwie `package.json`.  Wewnątrz tego pliku umieść hello następujące czynności:

```json
{
  "name": "application-name",
  "version": "0.0.1",
  "private": true,
  "scripts": {
    "start": "node server"
  },
  "dependencies": {
    "body-parser": "^1.16.1",
    "ejs": "^2.5.5",
    "errorhandler": "^1.5.0",
    "express": "^4.14.1",
    "morgan": "^1.8.1",
    "twilio": "^2.11.1"
  }
}
```

To deklaruje modułu usługi twilio hello jako zależności, jak i hello popularnych [Express platforma sieci web] [ express] i hello EJS szablonu aparatu.  Zgoda teraz możemy wszystko jest gotowe — Napiszmy kod!

<a id="makecall"/>

## <a name="make-an-outbound-call"></a>Wywoływania ruchu wychodzącego
Umożliwia tworzenie prostego formularz, który spowoduje umieszczenie numeru tooa wywołania wybranej. Otwórz `server.js`i wprowadź hello następującego kodu. Należy zwrócić uwagę, gdy wyświetlany jest tekst "CHANGE_ME" - umieszczono hello nazwa witryny sieci Web platformy azure:

```javascript
// Module dependencies
const express = require('express');
const path = require('path');
const http = require('http');
const twilio = require('twilio');
const logger = require('morgan');
const bodyParser = require('body-parser');
const errorHandler = require('errorhandler');
const accountSid = process.env.TWILIO_ACCOUNT_SID;
const authToken = process.env.TWILIO_AUTH_TOKEN;
// Create Express web application
const app = express();

// Express configuration
app.set('port', process.env.PORT || 3000);
app.set('views', __dirname + '/views');
app.set('view engine', 'ejs');
app.use(logger('tiny'));
app.use(bodyParser.urlencoded({ extended: false }))
app.use(bodyParser.json())
app.use(express.static(path.join(__dirname, 'public')));

if (app.get('env') !== 'production') {
  app.use(errorHandler());
}

// Render an HTML user interface for hello application's home page
app.get('/', (request, response) => response.render('index'));

// Handle hello form POST tooplace a call
app.post('/call', (request, response) => {
  var client = twilio(accountSid, authToken);

  client.makeCall({
    // make a call toothis number
    to:request.body.number,

    // Change tooa Twilio number you bought - see:
    // https://www.twilio.com/console/phone-numbers/incoming
    from:'+15558675309',

    // A URL in our app which generates TwiML
    // Change "CHANGE_ME" tooyour app's name
    url:'https://CHANGE_ME.azurewebsites.net/outbound_call'
  }, () => {
      // Go back toohello home page
      response.redirect('/');
  });
});

// Generate TwiML toohandle an outbound call
app.post('/outbound_call', (request, response) => {
  var twiml = new twilio.TwimlResponse();

  // Say a message toohello call's receiver
  twiml.say('hello - thanks for checking out Twilio and Azure', {
      voice:'woman'
  });

  response.set('Content-Type', 'text/xml');
  response.send(twiml.toString());
});

// Start server
app.listen(app.get('port'), function(){
  console.log(`Express server listening on port ${app.get('port')}`);
});
```

Następnie należy utworzyć katalog o nazwie `views` — w tym katalogu, Utwórz plik o nazwie `index.ejs` z hello następującej zawartości:

```html
<!DOCTYPE html>
<html>
<head>
  <title>Twilio Test</title>
  <style>
    input { height:20px; width:300px; font-size:18px; margin:5px; padding:5px; }
  </style>
</head>
<body>
  <h1>Twilio Test</h1>
  <form action="/call" method="POST">
      <input placeholder="Enter a phone number" name="number"/>
      <br/>
      <input type="submit" value="Call hello number above"/>
  </form>
</body>
</html>
```

Teraz Wdróż tooAzure Twojego witryny sieci Web i otworzyć domu. Powinny być możliwe tooenter numer telefonu w polu tekstowym hello i odbierać rozmowę z numer usługi Twilio!

<a id="sendmessage"/>

## <a name="send-an-sms-message"></a>Wyślij wiadomość SMS
Teraz Skonfigurujmy interfejsu użytkownika i obsługi logiki toosend formularzy wiadomości tekstowej. Otwórz `server.js`i Dodaj hello następującego kodu po ostatnim wywołaniu hello zbyt`app.post`:

```javascript
app.post('/sms', (request, response) => {
  const client = twilio(accountSid, authToken);

  client.sendSms({
      // send a text toothis number
      to:request.body.number,

      // A Twilio number you bought - see:
      // https://www.twilio.com/console/phone-numbers/incoming
      from:'+15558675309',

      // hello body of hello text message
      body: request.body.message

  }, () => {
      // Go back toohello home page
      response.redirect('/');
  });
});
```

W `views/index.ejs`, Dodaj innej formy w obszarze hello toosubmit pierwszy z nich liczbę i wiadomości SMS:

```html
<form action="/sms" method="POST">
  <input placeholder="Enter a phone number" name="number"/>
  <br/>
  <input placeholder="Enter a message toosend" name="message"/>
  <br/>
  <input type="submit" value="Send text toohello number above"/>
</form>
```

Ponownie wdróż tooAzure Twojej aplikacji i powinno być teraz możliwe toosubmit, tworzą i wysłać wiadomość SMS samodzielnie (lub któregokolwiek z Twoich znajomych najbliższego)!

<a id="nextsteps"/>

## <a name="next-steps"></a>Następne kroki
Ma teraz znasz już podstawy hello przy użyciu środowiska node.js i usługi Twilio toobuild aplikacje, które komunikują się. Jednak te przykłady prawie pliki tymczasowe powierzchni hello co to jest możliwe za pomocą usługi Twilio i node.js. Aby uzyskać więcej informacji o node.js przy użyciu usługi Twilio zapoznaj się hello następujące zasoby:

* [Moduł oficjalna dokumentacja][docs]
* [Samouczek dotyczący VoIP z aplikacji node.js][voipnode]
* [Votr - wiadomość SMS w czasie rzeczywistym głosowania aplikacji node.js i CouchDB (trzy części)][votr]
* [Programowanie pary w przeglądarce hello za pomocą języka node.js][pair]

Mamy nadzieję, że lubisz przejęcie node.js i usługi Twilio na platformie Azure!

[purchase_phone]: https://www.twilio.com/console/phone-numbers/search
[twiml]: https://www.twilio.com/docs/api/twiml
[signup]: http://ahoy.twilio.com/azure
[azure_new_site]: app-service-web/app-service-web-get-started-nodejs.md
[twilio_console]: https://www.twilio.com/console
[npm]: http://npmjs.org
[express]: http://expressjs.com
[voipnode]: http://www.twilio.com/blog/2013/04/introduction-to-twilio-client-with-node-js.html
[docs]: http://twilio.github.io/twilio-node/
[votr]: http://www.twilio.com/blog/2012/09/building-a-real-time-sms-voting-app-part-1-node-js-couchdb.html
[pair]: http://www.twilio.com/blog/2013/06/pair-programming-in-the-browser-with-twilio.html
[azure-admin-console]: ./media/partner-twilio-nodejs-how-to-use-voice-sms/twilio_1.png
