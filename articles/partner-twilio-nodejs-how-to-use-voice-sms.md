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
# <a name="using-twilio-for-voice-voip-and-sms-messaging-in-azure"></a><span data-ttu-id="34220-104">Przy użyciu usługi Twilio głosowych, VoIP i wiadomości SMS na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="34220-104">Using Twilio for Voice, VoIP, and SMS Messaging in Azure</span></span>
<span data-ttu-id="34220-105">W tym przewodniku pokazano, jak toobuild aplikacje, które do komunikacji z usługi Twilio i node.js na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="34220-105">This guide demonstrates how toobuild apps that communicate with Twilio and node.js on Azure.</span></span>

<a id="whatis"/>

## <a name="what-is-twilio"></a><span data-ttu-id="34220-106">Co to jest usługi Twilio?</span><span class="sxs-lookup"><span data-stu-id="34220-106">What is Twilio?</span></span>
<span data-ttu-id="34220-107">Usługi Twilio to platforma interfejsu API, która ułatwia deweloperom toomake i odbieranie połączeń telefonicznych, wysyłanie i odbieranie wiadomości tekstowych i osadzić VoIP wywołanie przeglądarki i natywnych aplikacji dla urządzeń przenośnych.</span><span class="sxs-lookup"><span data-stu-id="34220-107">Twilio is an API platform that makes it easy for developers toomake and receive phone calls, send and receive text messages, and embed VoIP calling into browser-based and native mobile applications.</span></span> <span data-ttu-id="34220-108">Załóżmy krótko przekazywane jak to działa przed rozpoczęciem pracy.</span><span class="sxs-lookup"><span data-stu-id="34220-108">Let's briefly go over how this works before diving in.</span></span>

### <a name="receiving-calls-and-text-messages"></a><span data-ttu-id="34220-109">Odbieranie wywołań i wiadomości SMS</span><span class="sxs-lookup"><span data-stu-id="34220-109">Receiving Calls and Text Messages</span></span>
<span data-ttu-id="34220-110">Usługi Twilio umożliwia deweloperom stosowanie zbyt[zakupu numery telefonów programowalny] [ purchase_phone] które mogą być używane tooboth wysyłać i odbierać wywołania i wiadomości SMS.</span><span class="sxs-lookup"><span data-stu-id="34220-110">Twilio allows developers too[purchase programmable phone numbers][purchase_phone] which can be used tooboth send and receive calls and text messages.</span></span> <span data-ttu-id="34220-111">W odebrania połączenia przychodzącego lub wiadomości SMS numer usługi Twilio usługi Twilio wyśle aplikacji sieci web HTTP POST lub GET żądania, zapytaniem instrukcje w sposób toohandle hello połączenia lub wiadomości SMS.</span><span class="sxs-lookup"><span data-stu-id="34220-111">When a Twilio number receives an inbound call or text, Twilio will send your web application an HTTP POST or GET request, asking you for instructions on how toohandle hello call or text.</span></span> <span data-ttu-id="34220-112">Serwer będzie odpowiadać na żądania HTTP przez tooTwilio z [TwiML][twiml], prosty zestaw tagi XML, które zawierają instrukcje na temat toohandle połączenia lub wiadomości SMS.</span><span class="sxs-lookup"><span data-stu-id="34220-112">Your server will respond tooTwilio's HTTP request with [TwiML][twiml], a simple set of XML tags that contain instructions on how toohandle a call or text.</span></span> <span data-ttu-id="34220-113">Przykłady TwiML zostaną podane w chwilę.</span><span class="sxs-lookup"><span data-stu-id="34220-113">We will see examples of TwiML in just a moment.</span></span>

### <a name="making-calls-and-sending-text-messages"></a><span data-ttu-id="34220-114">Wykonywanie wywołań i wysyłanie wiadomości tekstowych</span><span class="sxs-lookup"><span data-stu-id="34220-114">Making Calls and Sending Text Messages</span></span>
<span data-ttu-id="34220-115">Dzięki toohello żądań HTTP interfejsu API usługi sieci web usługi Twilio, deweloperzy mogą wiadomości tekstowych lub zainicjować wychodzących połączeń telefonicznych.</span><span class="sxs-lookup"><span data-stu-id="34220-115">By making HTTP requests toohello Twilio web service API, developers can send text messages or initiate outbound phone calls.</span></span> <span data-ttu-id="34220-116">Wychodzący deweloperów hello należy także określić adres URL, który zwraca TwiML instrukcje dotyczące sposobu hello toohandle wychodzącego wywołać po podłączeniu.</span><span class="sxs-lookup"><span data-stu-id="34220-116">For outbound calls, hello developer must also specify a URL that returns TwiML instructions for how toohandle hello outbound call once it is connected.</span></span>

### <a name="embedding-voip-capabilities-in-ui-code-javascript-ios-or-android"></a><span data-ttu-id="34220-117">Osadzanie możliwości VoIP w kodzie interfejsu użytkownika (JavaScript, iOS lub Android)</span><span class="sxs-lookup"><span data-stu-id="34220-117">Embedding VoIP Capabilities in UI code (JavaScript, iOS, or Android)</span></span>
<span data-ttu-id="34220-118">Usługi Twilio zawiera zestaw SDK klienta, który można przekształcić w dowolnej przeglądarki sieci web, aplikacji dla systemu iOS lub aplikacji systemu Android telefonu VoIP.</span><span class="sxs-lookup"><span data-stu-id="34220-118">Twilio provides a client-side SDK which can turn any desktop web browser, iOS app, or Android app into a VoIP phone.</span></span> <span data-ttu-id="34220-119">W tym artykule, firma Microsoft będzie skupić się na temat toouse VoIP wywoływania w przeglądarce hello.</span><span class="sxs-lookup"><span data-stu-id="34220-119">In this article, we will focus on how toouse VoIP calling in hello browser.</span></span> <span data-ttu-id="34220-120">W przypadku dodawania toohello *usługi Twilio JavaScript SDK* uruchomiony w przeglądarce hello, aplikację po stronie serwera (naszej aplikacji node.js) musi być używane tooissue toohello "możliwości tokenu" JavaScript klienta.</span><span class="sxs-lookup"><span data-stu-id="34220-120">In addition toohello *Twilio JavaScript SDK* running in hello browser, a server-side application (our node.js application) must be used tooissue a "capability token" toohello JavaScript client.</span></span> <span data-ttu-id="34220-121">Więcej o korzystaniu z node.js VoIP [na blogu deweloperów usługi Twilio hello][voipnode].</span><span class="sxs-lookup"><span data-stu-id="34220-121">You can read more about using VoIP with node.js [on hello Twilio dev blog][voipnode].</span></span>

<a id="signup"/>

## <a name="sign-up-for-twilio-microsoft-discount"></a><span data-ttu-id="34220-122">Utwórz konto usługi Twilio (Microsoft rabat)</span><span class="sxs-lookup"><span data-stu-id="34220-122">Sign Up For Twilio (Microsoft Discount)</span></span>
<span data-ttu-id="34220-123">Przed rozpoczęciem korzystania z usługi Twilio usługi, należy najpierw [konto][signup].</span><span class="sxs-lookup"><span data-stu-id="34220-123">Before using Twilio services, you must first [sign up for an account][signup].</span></span> <span data-ttu-id="34220-124">Microsoft Azure klienci uzyskać rabat specjalne — [można toosign się tutaj][signup]!</span><span class="sxs-lookup"><span data-stu-id="34220-124">Microsoft Azure customers receive a special discount - [be sure toosign up here][signup]!</span></span>

<a id="azuresite"/>

## <a name="create-and-deploy-a-nodejs-azure-website"></a><span data-ttu-id="34220-125">Tworzenie i wdrażanie witryny sieci Web Azure node.js</span><span class="sxs-lookup"><span data-stu-id="34220-125">Create and Deploy a node.js Azure Website</span></span>
<span data-ttu-id="34220-126">Następnie należy toocreate witryny sieci Web node.js działających na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="34220-126">Next, you will need toocreate a node.js website running on Azure.</span></span> <span data-ttu-id="34220-127">[Witaj oficjalnej dokumentacji dla tej czynności znajduje się tutaj][azure_new_site].</span><span class="sxs-lookup"><span data-stu-id="34220-127">[hello official documentation for doing this is located here][azure_new_site].</span></span> <span data-ttu-id="34220-128">Na wysokim poziomie będzie realizacji hello następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="34220-128">At a high level, you will be doing hello following:</span></span>

* <span data-ttu-id="34220-129">Podczas tworzenia konta platformy Azure, jeśli nie masz już</span><span class="sxs-lookup"><span data-stu-id="34220-129">Signing up for an Azure account, if you don't have one already</span></span>
* <span data-ttu-id="34220-130">Przy użyciu toocreate konsoli administratora usługi Azure hello nowej witryny sieci Web</span><span class="sxs-lookup"><span data-stu-id="34220-130">Using hello Azure admin console toocreate a new website</span></span>
* <span data-ttu-id="34220-131">Dodawanie obsługi kontroli źródła (zakładamy, że używane git)</span><span class="sxs-lookup"><span data-stu-id="34220-131">Adding source control support (we will assume you used git)</span></span>
* <span data-ttu-id="34220-132">Tworzenie pliku `server.js` z aplikacją sieci web node.js proste</span><span class="sxs-lookup"><span data-stu-id="34220-132">Creating a file `server.js` with a simple node.js web application</span></span>
* <span data-ttu-id="34220-133">Wdrażanie tego tooAzure prostej aplikacji</span><span class="sxs-lookup"><span data-stu-id="34220-133">Deploying this simple application tooAzure</span></span>

<a id="twiliomodule"/>

## <a name="configure-hello-twilio-module"></a><span data-ttu-id="34220-134">Skonfiguruj hello modułu usługi Twilio</span><span class="sxs-lookup"><span data-stu-id="34220-134">Configure hello Twilio Module</span></span>
<span data-ttu-id="34220-135">Następnie Rozpoczniemy toowrite aplikacji node.js proste, co sprawia, że użycie hello interfejsu API usługi Twilio.</span><span class="sxs-lookup"><span data-stu-id="34220-135">Next, we will begin toowrite a simple node.js application which makes use of hello Twilio API.</span></span> <span data-ttu-id="34220-136">Zanim zaczniemy, potrzebujemy tooconfigure naszych poświadczenia konta usługi Twilio.</span><span class="sxs-lookup"><span data-stu-id="34220-136">Before we begin, we need tooconfigure our Twilio account credentials.</span></span>

### <a name="configuring-twilio-credentials-in-system-environment-variables"></a><span data-ttu-id="34220-137">Konfigurowanie poświadczeń usługi Twilio w zmiennych środowiskowych systemu</span><span class="sxs-lookup"><span data-stu-id="34220-137">Configuring Twilio Credentials in System Environment Variables</span></span>
<span data-ttu-id="34220-138">W kolejności toomake uwierzytelnione żądania do zaplecza usługi Twilio hello potrzebujemy naszych identyfikatora SID konta i uwierzytelniania tokenu, która funkcja jako hello nazwę użytkownika i hasło określone dla naszego konta usługi Twilio.</span><span class="sxs-lookup"><span data-stu-id="34220-138">In order toomake authenticated requests against hello Twilio back end, we need our account SID and auth token, which function as hello username and password set for our Twilio account.</span></span> <span data-ttu-id="34220-139">Witaj najbezpieczniejszą tooconfigure sposób ich do użytku z modułu węzeł hello na platformie Azure jest za pomocą zmiennych środowiskowych systemu, które można ustawić bezpośrednio w konsoli administracyjnej Azure hello.</span><span class="sxs-lookup"><span data-stu-id="34220-139">hello most secure way tooconfigure these for use with hello node module in Azure is via system environment variables, which you can set directly in hello Azure admin console.</span></span>

<span data-ttu-id="34220-140">Wybierz witrynę sieci Web node.js, a następnie kliknij łącze "Konfiguruj" hello.</span><span class="sxs-lookup"><span data-stu-id="34220-140">Select your node.js website, and click hello "CONFIGURE" link.</span></span>  <span data-ttu-id="34220-141">Przewiń w dół bit zobaczysz obszaru, w którym można ustawić właściwości konfiguracji dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="34220-141">If you scroll down a bit, you will see an area where you can set configuration properties for your application.</span></span>  <span data-ttu-id="34220-142">Wprowadź poświadczenia konta usługi Twilio ([znaleziono w konsoli usługi Twilio][twilio_console]) jak pokazano — upewnij się, że tooname je `TWILIO_ACCOUNT_SID` i `TWILIO_AUTH_TOKEN`odpowiednio:</span><span class="sxs-lookup"><span data-stu-id="34220-142">Enter your Twilio account credentials ([found on your Twilio Console][twilio_console]) as shown - make sure tooname them `TWILIO_ACCOUNT_SID` and `TWILIO_AUTH_TOKEN`, respectively:</span></span>

![Konsola administracyjna platformy Azure][azure-admin-console]

<span data-ttu-id="34220-144">Po skonfigurowaniu tych zmiennych, ponownie uruchom aplikację w hello konsoli platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="34220-144">Once you have configured these variables, restart your application in hello Azure console.</span></span>

### <a name="declaring-hello-twilio-module-in-packagejson"></a><span data-ttu-id="34220-145">Deklarowanie hello usługi Twilio modułu w pliku package.json</span><span class="sxs-lookup"><span data-stu-id="34220-145">Declaring hello Twilio module in package.json</span></span>
<span data-ttu-id="34220-146">Następnie potrzebujemy toocreate package.json toomanage naszych węzeł zależności modułu za pośrednictwem [npm].</span><span class="sxs-lookup"><span data-stu-id="34220-146">Next, we need toocreate a package.json toomanage our node module dependencies via [npm].</span></span> <span data-ttu-id="34220-147">Na powitania sam poziom jako hello `server.js` pliku utworzonego w hello *Azure/node.js* samouczek, Utwórz plik o nazwie `package.json`.</span><span class="sxs-lookup"><span data-stu-id="34220-147">At hello same level as hello `server.js` file you created in hello *Azure/node.js* tutorial, create a file named `package.json`.</span></span>  <span data-ttu-id="34220-148">Wewnątrz tego pliku umieść hello następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="34220-148">Inside this file, place hello following:</span></span>

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

<span data-ttu-id="34220-149">To deklaruje modułu usługi twilio hello jako zależności, jak i hello popularnych [Express platforma sieci web] [ express] i hello EJS szablonu aparatu.</span><span class="sxs-lookup"><span data-stu-id="34220-149">This declares hello twilio module as a dependency, as well as hello popular [Express web framework][express] and hello EJS template engine.</span></span>  <span data-ttu-id="34220-150">Zgoda teraz możemy wszystko jest gotowe — Napiszmy kod!</span><span class="sxs-lookup"><span data-stu-id="34220-150">Okay, now we're all set - let's write some code!</span></span>

<a id="makecall"/>

## <a name="make-an-outbound-call"></a><span data-ttu-id="34220-151">Wywoływania ruchu wychodzącego</span><span class="sxs-lookup"><span data-stu-id="34220-151">Make an Outbound Call</span></span>
<span data-ttu-id="34220-152">Umożliwia tworzenie prostego formularz, który spowoduje umieszczenie numeru tooa wywołania wybranej.</span><span class="sxs-lookup"><span data-stu-id="34220-152">Let's create a simple form that will place a call tooa number we choose.</span></span> <span data-ttu-id="34220-153">Otwórz `server.js`i wprowadź hello następującego kodu.</span><span class="sxs-lookup"><span data-stu-id="34220-153">Open up `server.js`, and enter hello following code.</span></span> <span data-ttu-id="34220-154">Należy zwrócić uwagę, gdy wyświetlany jest tekst "CHANGE_ME" - umieszczono hello nazwa witryny sieci Web platformy azure:</span><span class="sxs-lookup"><span data-stu-id="34220-154">Note where it says "CHANGE_ME" - put hello name of your azure website there:</span></span>

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

<span data-ttu-id="34220-155">Następnie należy utworzyć katalog o nazwie `views` — w tym katalogu, Utwórz plik o nazwie `index.ejs` z hello następującej zawartości:</span><span class="sxs-lookup"><span data-stu-id="34220-155">Next, create a directory called `views` - inside this directory, create a file named `index.ejs` with hello following contents:</span></span>

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

<span data-ttu-id="34220-156">Teraz Wdróż tooAzure Twojego witryny sieci Web i otworzyć domu.</span><span class="sxs-lookup"><span data-stu-id="34220-156">Now, deploy your website tooAzure and open your home.</span></span> <span data-ttu-id="34220-157">Powinny być możliwe tooenter numer telefonu w polu tekstowym hello i odbierać rozmowę z numer usługi Twilio!</span><span class="sxs-lookup"><span data-stu-id="34220-157">You should be able tooenter your phone number in hello text field, and receive a call from your Twilio number!</span></span>

<a id="sendmessage"/>

## <a name="send-an-sms-message"></a><span data-ttu-id="34220-158">Wyślij wiadomość SMS</span><span class="sxs-lookup"><span data-stu-id="34220-158">Send an SMS Message</span></span>
<span data-ttu-id="34220-159">Teraz Skonfigurujmy interfejsu użytkownika i obsługi logiki toosend formularzy wiadomości tekstowej.</span><span class="sxs-lookup"><span data-stu-id="34220-159">Now, let's set up a user interface and form handling logic toosend a text message.</span></span> <span data-ttu-id="34220-160">Otwórz `server.js`i Dodaj hello następującego kodu po ostatnim wywołaniu hello zbyt`app.post`:</span><span class="sxs-lookup"><span data-stu-id="34220-160">Open up `server.js`, and add hello following code after hello last call too`app.post`:</span></span>

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

<span data-ttu-id="34220-161">W `views/index.ejs`, Dodaj innej formy w obszarze hello toosubmit pierwszy z nich liczbę i wiadomości SMS:</span><span class="sxs-lookup"><span data-stu-id="34220-161">In `views/index.ejs`, add another form under hello first one toosubmit a number and a text message:</span></span>

```html
<form action="/sms" method="POST">
  <input placeholder="Enter a phone number" name="number"/>
  <br/>
  <input placeholder="Enter a message toosend" name="message"/>
  <br/>
  <input type="submit" value="Send text toohello number above"/>
</form>
```

<span data-ttu-id="34220-162">Ponownie wdróż tooAzure Twojej aplikacji i powinno być teraz możliwe toosubmit, tworzą i wysłać wiadomość SMS samodzielnie (lub któregokolwiek z Twoich znajomych najbliższego)!</span><span class="sxs-lookup"><span data-stu-id="34220-162">Re-deploy your application tooAzure, and you should now be able toosubmit that form and send yourself (or any of your closest friends) a text message!</span></span>

<a id="nextsteps"/>

## <a name="next-steps"></a><span data-ttu-id="34220-163">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="34220-163">Next Steps</span></span>
<span data-ttu-id="34220-164">Ma teraz znasz już podstawy hello przy użyciu środowiska node.js i usługi Twilio toobuild aplikacje, które komunikują się.</span><span class="sxs-lookup"><span data-stu-id="34220-164">You have now learned hello basics of using node.js and Twilio toobuild apps that communicate.</span></span> <span data-ttu-id="34220-165">Jednak te przykłady prawie pliki tymczasowe powierzchni hello co to jest możliwe za pomocą usługi Twilio i node.js.</span><span class="sxs-lookup"><span data-stu-id="34220-165">But these examples barely scratch hello surface of what's possible with Twilio and node.js.</span></span> <span data-ttu-id="34220-166">Aby uzyskać więcej informacji o node.js przy użyciu usługi Twilio zapoznaj się hello następujące zasoby:</span><span class="sxs-lookup"><span data-stu-id="34220-166">For more information using Twilio with node.js, check out hello following resources:</span></span>

* <span data-ttu-id="34220-167">[Moduł oficjalna dokumentacja][docs]</span><span class="sxs-lookup"><span data-stu-id="34220-167">[Official module docs][docs]</span></span>
* <span data-ttu-id="34220-168">[Samouczek dotyczący VoIP z aplikacji node.js][voipnode]</span><span class="sxs-lookup"><span data-stu-id="34220-168">[Tutorial on VoIP with node.js applications][voipnode]</span></span>
* <span data-ttu-id="34220-169">[Votr - wiadomość SMS w czasie rzeczywistym głosowania aplikacji node.js i CouchDB (trzy części)][votr]</span><span class="sxs-lookup"><span data-stu-id="34220-169">[Votr - a real-time SMS voting application with node.js and CouchDB (three parts)][votr]</span></span>
* <span data-ttu-id="34220-170">[Programowanie pary w przeglądarce hello za pomocą języka node.js][pair]</span><span class="sxs-lookup"><span data-stu-id="34220-170">[Pair programming in hello browser with node.js][pair]</span></span>

<span data-ttu-id="34220-171">Mamy nadzieję, że lubisz przejęcie node.js i usługi Twilio na platformie Azure!</span><span class="sxs-lookup"><span data-stu-id="34220-171">We hope you love hacking node.js and Twilio on Azure!</span></span>

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
