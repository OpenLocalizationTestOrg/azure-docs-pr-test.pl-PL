---
title: "Przy użyciu usługi Twilio głosowych, VoIP i wiadomości SMS na platformie Azure"
description: "Dowiedz się, jak wykonać połączenie telefoniczne i wysłać wiadomość SMS z usługi interfejsu API usługi Twilio na platformie Azure. Przykłady kodu napisane w środowisku Node.js."
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
ms.openlocfilehash: 44ec97812130d41d75be98fc8e2d846b7cb5c913
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="using-twilio-for-voice-voip-and-sms-messaging-in-azure"></a><span data-ttu-id="ff489-104">Przy użyciu usługi Twilio głosowych, VoIP i wiadomości SMS na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="ff489-104">Using Twilio for Voice, VoIP, and SMS Messaging in Azure</span></span>
<span data-ttu-id="ff489-105">W tym przewodniku pokazano, jak tworzyć aplikacje, które komunikują się z usługi Twilio i node.js na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="ff489-105">This guide demonstrates how to build apps that communicate with Twilio and node.js on Azure.</span></span>

<a id="whatis"/>

## <a name="what-is-twilio"></a><span data-ttu-id="ff489-106">Co to jest usługi Twilio?</span><span class="sxs-lookup"><span data-stu-id="ff489-106">What is Twilio?</span></span>
<span data-ttu-id="ff489-107">Usługi Twilio to platforma interfejsu API, która ułatwia deweloperom upewnij i odbieranie połączeń telefonicznych, wysyłanie i odbieranie wiadomości tekstowych i osadzić VoIP wywołanie przeglądarki i natywnych aplikacji dla urządzeń przenośnych.</span><span class="sxs-lookup"><span data-stu-id="ff489-107">Twilio is an API platform that makes it easy for developers to make and receive phone calls, send and receive text messages, and embed VoIP calling into browser-based and native mobile applications.</span></span> <span data-ttu-id="ff489-108">Załóżmy krótko przekazywane jak to działa przed rozpoczęciem pracy.</span><span class="sxs-lookup"><span data-stu-id="ff489-108">Let's briefly go over how this works before diving in.</span></span>

### <a name="receiving-calls-and-text-messages"></a><span data-ttu-id="ff489-109">Odbieranie wywołań i wiadomości SMS</span><span class="sxs-lookup"><span data-stu-id="ff489-109">Receiving Calls and Text Messages</span></span>
<span data-ttu-id="ff489-110">Usługi Twilio umożliwia deweloperom [zakupu numery telefonów programowalny] [ purchase_phone] które mogą służyć do wysyłać i odbierać wywołań i wiadomości SMS.</span><span class="sxs-lookup"><span data-stu-id="ff489-110">Twilio allows developers to [purchase programmable phone numbers][purchase_phone] which can be used to both send and receive calls and text messages.</span></span> <span data-ttu-id="ff489-111">W odebrania połączenia przychodzącego lub wiadomości SMS numer usługi Twilio usługi Twilio wyśle aplikacji sieci web HTTP POST lub GET żądania, zapytaniem instrukcje na temat sposobu obsługi połączenia lub wiadomości SMS.</span><span class="sxs-lookup"><span data-stu-id="ff489-111">When a Twilio number receives an inbound call or text, Twilio will send your web application an HTTP POST or GET request, asking you for instructions on how to handle the call or text.</span></span> <span data-ttu-id="ff489-112">Serwer będzie odpowiadać na żądania HTTP dla usługi Twilio z [TwiML][twiml], zbiór prostych tagów XML, które zawierają instrukcje dotyczące sposobu obsługi połączenia lub wiadomości SMS.</span><span class="sxs-lookup"><span data-stu-id="ff489-112">Your server will respond to Twilio's HTTP request with [TwiML][twiml], a simple set of XML tags that contain instructions on how to handle a call or text.</span></span> <span data-ttu-id="ff489-113">Przykłady TwiML zostaną podane w chwilę.</span><span class="sxs-lookup"><span data-stu-id="ff489-113">We will see examples of TwiML in just a moment.</span></span>

### <a name="making-calls-and-sending-text-messages"></a><span data-ttu-id="ff489-114">Wykonywanie wywołań i wysyłanie wiadomości tekstowych</span><span class="sxs-lookup"><span data-stu-id="ff489-114">Making Calls and Sending Text Messages</span></span>
<span data-ttu-id="ff489-115">Dokonując żądania HTTP do interfejsu API usługi sieci web usługi Twilio, deweloperzy mogą wiadomości tekstowych lub zainicjować wychodzących rozmów telefonicznych.</span><span class="sxs-lookup"><span data-stu-id="ff489-115">By making HTTP requests to the Twilio web service API, developers can send text messages or initiate outbound phone calls.</span></span> <span data-ttu-id="ff489-116">Wychodzący deweloper musi również określić adres URL, który zwraca TwiML instrukcje dotyczące sposobu obsługi ruchu wychodzącego wywołania po podłączeniu.</span><span class="sxs-lookup"><span data-stu-id="ff489-116">For outbound calls, the developer must also specify a URL that returns TwiML instructions for how to handle the outbound call once it is connected.</span></span>

### <a name="embedding-voip-capabilities-in-ui-code-javascript-ios-or-android"></a><span data-ttu-id="ff489-117">Osadzanie możliwości VoIP w kodzie interfejsu użytkownika (JavaScript, iOS lub Android)</span><span class="sxs-lookup"><span data-stu-id="ff489-117">Embedding VoIP Capabilities in UI code (JavaScript, iOS, or Android)</span></span>
<span data-ttu-id="ff489-118">Usługi Twilio zawiera zestaw SDK klienta, który można przekształcić w dowolnej przeglądarki sieci web, aplikacji dla systemu iOS lub aplikacji systemu Android telefonu VoIP.</span><span class="sxs-lookup"><span data-stu-id="ff489-118">Twilio provides a client-side SDK which can turn any desktop web browser, iOS app, or Android app into a VoIP phone.</span></span> <span data-ttu-id="ff489-119">W tym artykule firma Microsoft będzie skupić się na temat korzystania z połączeń VoIP w przeglądarce.</span><span class="sxs-lookup"><span data-stu-id="ff489-119">In this article, we will focus on how to use VoIP calling in the browser.</span></span> <span data-ttu-id="ff489-120">Oprócz *usługi Twilio JavaScript SDK* uruchomiona w przeglądarce, aplikację po stronie serwera (naszej aplikacji node.js) musi używane do wystawiania tokenu"funkcji" do klienta kodu JavaScript.</span><span class="sxs-lookup"><span data-stu-id="ff489-120">In addition to the *Twilio JavaScript SDK* running in the browser, a server-side application (our node.js application) must be used to issue a "capability token" to the JavaScript client.</span></span> <span data-ttu-id="ff489-121">Więcej o korzystaniu z node.js VoIP [na blogu deweloperów usługi Twilio][voipnode].</span><span class="sxs-lookup"><span data-stu-id="ff489-121">You can read more about using VoIP with node.js [on the Twilio dev blog][voipnode].</span></span>

<a id="signup"/>

## <a name="sign-up-for-twilio-microsoft-discount"></a><span data-ttu-id="ff489-122">Utwórz konto usługi Twilio (Microsoft rabat)</span><span class="sxs-lookup"><span data-stu-id="ff489-122">Sign Up For Twilio (Microsoft Discount)</span></span>
<span data-ttu-id="ff489-123">Przed rozpoczęciem korzystania z usługi Twilio usługi, należy najpierw [konto][signup].</span><span class="sxs-lookup"><span data-stu-id="ff489-123">Before using Twilio services, you must first [sign up for an account][signup].</span></span> <span data-ttu-id="ff489-124">Microsoft Azure klienci uzyskać rabat specjalne — [Pamiętaj zarejestrować się tutaj][signup]!</span><span class="sxs-lookup"><span data-stu-id="ff489-124">Microsoft Azure customers receive a special discount - [be sure to sign up here][signup]!</span></span>

<a id="azuresite"/>

## <a name="create-and-deploy-a-nodejs-azure-website"></a><span data-ttu-id="ff489-125">Tworzenie i wdrażanie witryny sieci Web Azure node.js</span><span class="sxs-lookup"><span data-stu-id="ff489-125">Create and Deploy a node.js Azure Website</span></span>
<span data-ttu-id="ff489-126">Następnie należy utworzyć witrynę sieci Web node.js działających na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="ff489-126">Next, you will need to create a node.js website running on Azure.</span></span> <span data-ttu-id="ff489-127">[Oficjalnej dokumentacji dla tej czynności znajduje się tutaj][azure_new_site].</span><span class="sxs-lookup"><span data-stu-id="ff489-127">[The official documentation for doing this is located here][azure_new_site].</span></span> <span data-ttu-id="ff489-128">Na wysokim poziomie użytkownik będzie można wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="ff489-128">At a high level, you will be doing the following:</span></span>

* <span data-ttu-id="ff489-129">Podczas tworzenia konta platformy Azure, jeśli nie masz już</span><span class="sxs-lookup"><span data-stu-id="ff489-129">Signing up for an Azure account, if you don't have one already</span></span>
* <span data-ttu-id="ff489-130">Aby utworzyć nową witrynę sieci Web przy użyciu konsoli administracyjnej usługi Azure</span><span class="sxs-lookup"><span data-stu-id="ff489-130">Using the Azure admin console to create a new website</span></span>
* <span data-ttu-id="ff489-131">Dodawanie obsługi kontroli źródła (zakładamy, że używane git)</span><span class="sxs-lookup"><span data-stu-id="ff489-131">Adding source control support (we will assume you used git)</span></span>
* <span data-ttu-id="ff489-132">Tworzenie pliku `server.js` z aplikacją sieci web node.js proste</span><span class="sxs-lookup"><span data-stu-id="ff489-132">Creating a file `server.js` with a simple node.js web application</span></span>
* <span data-ttu-id="ff489-133">Wdrażanie Ta prosta aplikacja na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="ff489-133">Deploying this simple application to Azure</span></span>

<a id="twiliomodule"/>

## <a name="configure-the-twilio-module"></a><span data-ttu-id="ff489-134">Konfigurowanie modułu usługi Twilio</span><span class="sxs-lookup"><span data-stu-id="ff489-134">Configure the Twilio Module</span></span>
<span data-ttu-id="ff489-135">Następnie możemy zacząć pisanie aplikacji node.js proste, która korzysta z interfejsu API usługi Twilio.</span><span class="sxs-lookup"><span data-stu-id="ff489-135">Next, we will begin to write a simple node.js application which makes use of the Twilio API.</span></span> <span data-ttu-id="ff489-136">Zanim zaczniemy, należy skonfigurować naszych poświadczenia konta usługi Twilio.</span><span class="sxs-lookup"><span data-stu-id="ff489-136">Before we begin, we need to configure our Twilio account credentials.</span></span>

### <a name="configuring-twilio-credentials-in-system-environment-variables"></a><span data-ttu-id="ff489-137">Konfigurowanie poświadczeń usługi Twilio w zmiennych środowiskowych systemu</span><span class="sxs-lookup"><span data-stu-id="ff489-137">Configuring Twilio Credentials in System Environment Variables</span></span>
<span data-ttu-id="ff489-138">Aby wprowadzić uwierzytelnionego żądania kierowane do zaplecza usługi Twilio, potrzebujemy naszych identyfikatora SID konta i token uwierzytelniania, funkcji jako nazwy użytkownika i hasło określone dla naszego konta usługi Twilio.</span><span class="sxs-lookup"><span data-stu-id="ff489-138">In order to make authenticated requests against the Twilio back end, we need our account SID and auth token, which function as the username and password set for our Twilio account.</span></span> <span data-ttu-id="ff489-139">Najbezpieczniejszą metodą, aby skonfigurować je do użycia z modułem węzła na platformie Azure jest za pomocą zmiennych środowiskowych systemu, które można ustawić bezpośrednio w konsoli administracyjnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="ff489-139">The most secure way to configure these for use with the node module in Azure is via system environment variables, which you can set directly in the Azure admin console.</span></span>

<span data-ttu-id="ff489-140">Wybierz witrynę sieci Web node.js, a następnie kliknij łącze "Konfiguruj".</span><span class="sxs-lookup"><span data-stu-id="ff489-140">Select your node.js website, and click the "CONFIGURE" link.</span></span>  <span data-ttu-id="ff489-141">Przewiń w dół bit zobaczysz obszaru, w którym można ustawić właściwości konfiguracji dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ff489-141">If you scroll down a bit, you will see an area where you can set configuration properties for your application.</span></span>  <span data-ttu-id="ff489-142">Wprowadź poświadczenia konta usługi Twilio ([znaleziono w konsoli usługi Twilio][twilio_console]) jak pokazano — upewnij się, że nazwa je `TWILIO_ACCOUNT_SID` i `TWILIO_AUTH_TOKEN`odpowiednio:</span><span class="sxs-lookup"><span data-stu-id="ff489-142">Enter your Twilio account credentials ([found on your Twilio Console][twilio_console]) as shown - make sure to name them `TWILIO_ACCOUNT_SID` and `TWILIO_AUTH_TOKEN`, respectively:</span></span>

![Konsola administracyjna platformy Azure][azure-admin-console]

<span data-ttu-id="ff489-144">Po skonfigurowaniu tych zmiennych, ponownie uruchom aplikację w konsoli platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="ff489-144">Once you have configured these variables, restart your application in the Azure console.</span></span>

### <a name="declaring-the-twilio-module-in-packagejson"></a><span data-ttu-id="ff489-145">Deklarowanie w module usługi Twilio w pliku package.json</span><span class="sxs-lookup"><span data-stu-id="ff489-145">Declaring the Twilio module in package.json</span></span>
<span data-ttu-id="ff489-146">Następnie należy utworzyć package.json do zarządzania naszych węzeł zależności modułu za pośrednictwem [npm].</span><span class="sxs-lookup"><span data-stu-id="ff489-146">Next, we need to create a package.json to manage our node module dependencies via [npm].</span></span> <span data-ttu-id="ff489-147">Na tym samym poziomie jako `server.js` pliku utworzonego w *Azure/node.js* samouczek, Utwórz plik o nazwie `package.json`.</span><span class="sxs-lookup"><span data-stu-id="ff489-147">At the same level as the `server.js` file you created in the *Azure/node.js* tutorial, create a file named `package.json`.</span></span>  <span data-ttu-id="ff489-148">Wewnątrz tego pliku należy umieścić następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="ff489-148">Inside this file, place the following:</span></span>

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

<span data-ttu-id="ff489-149">Moduł usługi twilio to deklarowana jako zależności, a także popularnych [Express platforma sieci web] [ express] i EJS aparatu szablonu.</span><span class="sxs-lookup"><span data-stu-id="ff489-149">This declares the twilio module as a dependency, as well as the popular [Express web framework][express] and the EJS template engine.</span></span>  <span data-ttu-id="ff489-150">Zgoda teraz możemy wszystko jest gotowe — Napiszmy kod!</span><span class="sxs-lookup"><span data-stu-id="ff489-150">Okay, now we're all set - let's write some code!</span></span>

<a id="makecall"/>

## <a name="make-an-outbound-call"></a><span data-ttu-id="ff489-151">Wywoływania ruchu wychodzącego</span><span class="sxs-lookup"><span data-stu-id="ff489-151">Make an Outbound Call</span></span>
<span data-ttu-id="ff489-152">Umożliwia tworzenie prostych formularz, który będzie nawiązać połączenie z liczbą się, że wybrany.</span><span class="sxs-lookup"><span data-stu-id="ff489-152">Let's create a simple form that will place a call to a number we choose.</span></span> <span data-ttu-id="ff489-153">Otwórz `server.js`, a następnie wprowadź poniższy kod.</span><span class="sxs-lookup"><span data-stu-id="ff489-153">Open up `server.js`, and enter the following code.</span></span> <span data-ttu-id="ff489-154">Należy zwrócić uwagę, gdy wyświetlany jest tekst "CHANGE_ME" - umieszczono nazwę witryny sieci Web platformy azure:</span><span class="sxs-lookup"><span data-stu-id="ff489-154">Note where it says "CHANGE_ME" - put the name of your azure website there:</span></span>

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

// Render an HTML user interface for the application's home page
app.get('/', (request, response) => response.render('index'));

// Handle the form POST to place a call
app.post('/call', (request, response) => {
  var client = twilio(accountSid, authToken);

  client.makeCall({
    // make a call to this number
    to:request.body.number,

    // Change to a Twilio number you bought - see:
    // https://www.twilio.com/console/phone-numbers/incoming
    from:'+15558675309',

    // A URL in our app which generates TwiML
    // Change "CHANGE_ME" to your app's name
    url:'https://CHANGE_ME.azurewebsites.net/outbound_call'
  }, () => {
      // Go back to the home page
      response.redirect('/');
  });
});

// Generate TwiML to handle an outbound call
app.post('/outbound_call', (request, response) => {
  var twiml = new twilio.TwimlResponse();

  // Say a message to the call's receiver
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

<span data-ttu-id="ff489-155">Następnie należy utworzyć katalog o nazwie `views` — w tym katalogu, Utwórz plik o nazwie `index.ejs` z następującą zawartość:</span><span class="sxs-lookup"><span data-stu-id="ff489-155">Next, create a directory called `views` - inside this directory, create a file named `index.ejs` with the following contents:</span></span>

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
      <input type="submit" value="Call the number above"/>
  </form>
</body>
</html>
```

<span data-ttu-id="ff489-156">Teraz Wdrażanie witryny sieci Web na platformie Azure i otworzyć domu.</span><span class="sxs-lookup"><span data-stu-id="ff489-156">Now, deploy your website to Azure and open your home.</span></span> <span data-ttu-id="ff489-157">Można wprowadzić numer telefonu w polu tekstowym i odbierać rozmowę z numer usługi Twilio!</span><span class="sxs-lookup"><span data-stu-id="ff489-157">You should be able to enter your phone number in the text field, and receive a call from your Twilio number!</span></span>

<a id="sendmessage"/>

## <a name="send-an-sms-message"></a><span data-ttu-id="ff489-158">Wyślij wiadomość SMS</span><span class="sxs-lookup"><span data-stu-id="ff489-158">Send an SMS Message</span></span>
<span data-ttu-id="ff489-159">Teraz Skonfigurujmy interfejsu użytkownika i obsługi logiki formularzy do wysyłania wiadomości tekstowej.</span><span class="sxs-lookup"><span data-stu-id="ff489-159">Now, let's set up a user interface and form handling logic to send a text message.</span></span> <span data-ttu-id="ff489-160">Otwórz `server.js`i Dodaj następujący kod po ostatnim wywołaniem `app.post`:</span><span class="sxs-lookup"><span data-stu-id="ff489-160">Open up `server.js`, and add the following code after the last call to `app.post`:</span></span>

```javascript
app.post('/sms', (request, response) => {
  const client = twilio(accountSid, authToken);

  client.sendSms({
      // send a text to this number
      to:request.body.number,

      // A Twilio number you bought - see:
      // https://www.twilio.com/console/phone-numbers/incoming
      from:'+15558675309',

      // The body of the text message
      body: request.body.message

  }, () => {
      // Go back to the home page
      response.redirect('/');
  });
});
```

<span data-ttu-id="ff489-161">W `views/index.ejs`, Dodaj innej formy w obszarze pierwsza z nich można przesłać numer i wiadomości SMS:</span><span class="sxs-lookup"><span data-stu-id="ff489-161">In `views/index.ejs`, add another form under the first one to submit a number and a text message:</span></span>

```html
<form action="/sms" method="POST">
  <input placeholder="Enter a phone number" name="number"/>
  <br/>
  <input placeholder="Enter a message to send" name="message"/>
  <br/>
  <input type="submit" value="Send text to the number above"/>
</form>
```

<span data-ttu-id="ff489-162">Teraz należy może przesyłać, które tworzą i wysłać wiadomość SMS samodzielnie (lub któregokolwiek z Twoich znajomych najbliższego) i ponownie wdrożyć aplikację na platformie Azure!</span><span class="sxs-lookup"><span data-stu-id="ff489-162">Re-deploy your application to Azure, and you should now be able to submit that form and send yourself (or any of your closest friends) a text message!</span></span>

<a id="nextsteps"/>

## <a name="next-steps"></a><span data-ttu-id="ff489-163">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="ff489-163">Next Steps</span></span>
<span data-ttu-id="ff489-164">Ma teraz znasz już podstawy do tworzenia aplikacji, które komunikują się za pomocą środowiska node.js i usługi Twilio.</span><span class="sxs-lookup"><span data-stu-id="ff489-164">You have now learned the basics of using node.js and Twilio to build apps that communicate.</span></span> <span data-ttu-id="ff489-165">Jednak te przykłady prawie pliki tymczasowe powierzchni co to jest możliwe za pomocą usługi Twilio i node.js.</span><span class="sxs-lookup"><span data-stu-id="ff489-165">But these examples barely scratch the surface of what's possible with Twilio and node.js.</span></span> <span data-ttu-id="ff489-166">Aby uzyskać więcej informacji o node.js przy użyciu usługi Twilio zobacz następujące zasoby:</span><span class="sxs-lookup"><span data-stu-id="ff489-166">For more information using Twilio with node.js, check out the following resources:</span></span>

* <span data-ttu-id="ff489-167">[Moduł oficjalna dokumentacja][docs]</span><span class="sxs-lookup"><span data-stu-id="ff489-167">[Official module docs][docs]</span></span>
* <span data-ttu-id="ff489-168">[Samouczek dotyczący VoIP z aplikacji node.js][voipnode]</span><span class="sxs-lookup"><span data-stu-id="ff489-168">[Tutorial on VoIP with node.js applications][voipnode]</span></span>
* <span data-ttu-id="ff489-169">[Votr - wiadomość SMS w czasie rzeczywistym głosowania aplikacji node.js i CouchDB (trzy części)][votr]</span><span class="sxs-lookup"><span data-stu-id="ff489-169">[Votr - a real-time SMS voting application with node.js and CouchDB (three parts)][votr]</span></span>
* <span data-ttu-id="ff489-170">[Programowanie pary w przeglądarce, za pomocą języka node.js][pair]</span><span class="sxs-lookup"><span data-stu-id="ff489-170">[Pair programming in the browser with node.js][pair]</span></span>

<span data-ttu-id="ff489-171">Mamy nadzieję, że lubisz przejęcie node.js i usługi Twilio na platformie Azure!</span><span class="sxs-lookup"><span data-stu-id="ff489-171">We hope you love hacking node.js and Twilio on Azure!</span></span>

[purchase_phone]: https://www.twilio.com/console/phone-numbers/search
[twiml]: https://www.twilio.com/docs/api/twiml
[signup]: http://ahoy.twilio.com/azure
[azure_new_site]: app-service-web/app-service-web-get-started-nodejs.md
[twilio_console]: https://www.twilio.com/console
<span data-ttu-id="ff489-172">[npm]: http://npmjs.org</span><span class="sxs-lookup"><span data-stu-id="ff489-172">[npm]: http://npmjs.org</span></span>
[express]: http://expressjs.com
[voipnode]: http://www.twilio.com/blog/2013/04/introduction-to-twilio-client-with-node-js.html
[docs]: http://twilio.github.io/twilio-node/
[votr]: http://www.twilio.com/blog/2012/09/building-a-real-time-sms-voting-app-part-1-node-js-couchdb.html
[pair]: http://www.twilio.com/blog/2013/06/pair-programming-in-the-browser-with-twilio.html
[azure-admin-console]: ./media/partner-twilio-nodejs-how-to-use-voice-sms/twilio_1.png
