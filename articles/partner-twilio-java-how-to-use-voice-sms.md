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
# <a name="how-toouse-twilio-for-voice-and-sms-capabilities-in-java"></a><span data-ttu-id="1c74b-104">Jak tooUse usługi Twilio głosowe i możliwości programu SMS w języku Java</span><span class="sxs-lookup"><span data-stu-id="1c74b-104">How tooUse Twilio for Voice and SMS Capabilities in Java</span></span>
<span data-ttu-id="1c74b-105">W tym przewodniku pokazano, jak tooperform typowych zadań programowania hello interfejsu API usługi Twilio usługi na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="1c74b-105">This guide demonstrates how tooperform common programming tasks with hello Twilio API service on Azure.</span></span> <span data-ttu-id="1c74b-106">omówione scenariusze Hello obejmują tworzenie połączeń telefonicznych i wysyłanie wiadomości krótką wiadomość usługi (SMS).</span><span class="sxs-lookup"><span data-stu-id="1c74b-106">hello scenarios covered include making a phone call and sending a Short Message Service (SMS) message.</span></span> <span data-ttu-id="1c74b-107">Aby uzyskać więcej informacji na temat usługi Twilio i komunikacja głosowa programu SMS w aplikacji, zobacz hello [następne kroki](#NextSteps) sekcji.</span><span class="sxs-lookup"><span data-stu-id="1c74b-107">For more information on Twilio and using voice and SMS in your applications, see hello [Next Steps](#NextSteps) section.</span></span>

## <span data-ttu-id="1c74b-108"><a id="WhatIs"></a>Co to jest usługi Twilio?</span><span class="sxs-lookup"><span data-stu-id="1c74b-108"><a id="WhatIs"></a>What is Twilio?</span></span>
<span data-ttu-id="1c74b-109">Usługi Twilio jest telefonii API usługi sieci web, która umożliwia korzystanie z istniejących języków sieci web i umiejętności toobuild głosu aplikacji i programu SMS.</span><span class="sxs-lookup"><span data-stu-id="1c74b-109">Twilio is a telephony web-service API that lets you use your existing web languages and skills toobuild voice and SMS applications.</span></span> <span data-ttu-id="1c74b-110">Usługi Twilio jest usługą innych firm (nie funkcji platformy Azure i nie produkt firmy Microsoft).</span><span class="sxs-lookup"><span data-stu-id="1c74b-110">Twilio is a third-party service (not an Azure feature and not a Microsoft product).</span></span>

<span data-ttu-id="1c74b-111">**Usługi Twilio głosu** umożliwia toomake Twojej aplikacji i odbieranie połączeń telefonicznych.</span><span class="sxs-lookup"><span data-stu-id="1c74b-111">**Twilio Voice** allows your applications toomake and receive phone calls.</span></span> <span data-ttu-id="1c74b-112">**SMS usługi Twilio** umożliwia toomake Twojej aplikacji i odbieranie wiadomości SMS.</span><span class="sxs-lookup"><span data-stu-id="1c74b-112">**Twilio SMS** allows your applications toomake and receive SMS messages.</span></span> <span data-ttu-id="1c74b-113">**Klient usługi Twilio** umożliwia aplikacji komunikację głosową tooenable przy użyciu istniejących połączeń internetowych, w tym przenośnych połączenia.</span><span class="sxs-lookup"><span data-stu-id="1c74b-113">**Twilio Client** allows your applications tooenable voice communication using existing Internet connections, including mobile connections.</span></span>

## <span data-ttu-id="1c74b-114"><a id="Pricing"></a>Cennik usługi Twilio i oferty specjalne</span><span class="sxs-lookup"><span data-stu-id="1c74b-114"><a id="Pricing"></a>Twilio Pricing and Special Offers</span></span>
<span data-ttu-id="1c74b-115">Informacje o cenach usługi Twilio znajduje się w temacie [cennik usługi Twilio][twilio_pricing].</span><span class="sxs-lookup"><span data-stu-id="1c74b-115">Information about Twilio pricing is available at [Twilio Pricing][twilio_pricing].</span></span> <span data-ttu-id="1c74b-116">Azure klienci otrzymają [oferta specjalna][special_offer]: wolnego środki tekstów 1000 lub 1000 ruchu przychodzącego minut.</span><span class="sxs-lookup"><span data-stu-id="1c74b-116">Azure customers receive a [special offer][special_offer]: a free credit of 1000 texts or 1000 inbound minutes.</span></span> <span data-ttu-id="1c74b-117">toosign dla to oferty lub uzyskać więcej informacji, odwiedź stronę [http://ahoy.twilio.com/azure][special_offer].</span><span class="sxs-lookup"><span data-stu-id="1c74b-117">toosign up for this offer or get more information, please visit [http://ahoy.twilio.com/azure][special_offer].</span></span>

## <span data-ttu-id="1c74b-118"><a id="Concepts"></a>Pojęcia</span><span class="sxs-lookup"><span data-stu-id="1c74b-118"><a id="Concepts"></a>Concepts</span></span>
<span data-ttu-id="1c74b-119">Witaj interfejsu API usługi Twilio jest interfejs API RESTful, która zapewnia funkcje programu SMS i komunikacja głosowa aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1c74b-119">hello Twilio API is a RESTful API that provides voice and SMS functionality for applications.</span></span> <span data-ttu-id="1c74b-120">Klient biblioteki są dostępne w wielu językach; Aby uzyskać listę, zobacz [bibliotek interfejsu API usługi Twilio][twilio_libraries].</span><span class="sxs-lookup"><span data-stu-id="1c74b-120">Client libraries are available in multiple languages; for a list, see [Twilio API Libraries][twilio_libraries].</span></span>

<span data-ttu-id="1c74b-121">Kluczowe aspekty hello interfejsu API usługi Twilio są zleceń usługi Twilio i usługi Twilio Markup Language (TwiML).</span><span class="sxs-lookup"><span data-stu-id="1c74b-121">Key aspects of hello Twilio API are Twilio verbs and Twilio Markup Language (TwiML).</span></span>

### <span data-ttu-id="1c74b-122"><a id="Verbs"></a>Usługi Twilio zlecenia</span><span class="sxs-lookup"><span data-stu-id="1c74b-122"><a id="Verbs"></a>Twilio Verbs</span></span>
<span data-ttu-id="1c74b-123">Witaj interfejs API korzysta z usługi Twilio zleceń; na przykład Witaj  **&lt;powiedzieć&gt;**  zlecenie powoduje, że usługi Twilio tooaudibly dostarczenia komunikatu w wywołaniu.</span><span class="sxs-lookup"><span data-stu-id="1c74b-123">hello API makes use of Twilio verbs; for example, hello **&lt;Say&gt;** verb instructs Twilio tooaudibly deliver a message on a call.</span></span>

<span data-ttu-id="1c74b-124">Witaj poniżej przedstawiono listę poleceń usługi Twilio.</span><span class="sxs-lookup"><span data-stu-id="1c74b-124">hello following is a list of Twilio verbs.</span></span>

* <span data-ttu-id="1c74b-125">**&lt;Wybierania&gt;**: łączy hello wywołującego tooanother telefonu.</span><span class="sxs-lookup"><span data-stu-id="1c74b-125">**&lt;Dial&gt;**: Connects hello caller tooanother phone.</span></span>
* <span data-ttu-id="1c74b-126">**&lt;Zbierz&gt;**: zbiera wprowadzony na klawiaturze telefonu hello cyfr.</span><span class="sxs-lookup"><span data-stu-id="1c74b-126">**&lt;Gather&gt;**: Collects numeric digits entered on hello telephone keypad.</span></span>
* <span data-ttu-id="1c74b-127">**&lt;Rozłączanie&gt;**: kończy wywołanie.</span><span class="sxs-lookup"><span data-stu-id="1c74b-127">**&lt;Hangup&gt;**: Ends a call.</span></span>
* <span data-ttu-id="1c74b-128">**&lt;Odtwórz&gt;**: odtwarzania pliku audio.</span><span class="sxs-lookup"><span data-stu-id="1c74b-128">**&lt;Play&gt;**: Plays an audio file.</span></span>
* <span data-ttu-id="1c74b-129">**&lt;Kolejka&gt;**: Dodaj kolejkę tooa hello obiekty wywołujące.</span><span class="sxs-lookup"><span data-stu-id="1c74b-129">**&lt;Queue&gt;**: Add hello tooa queue of callers.</span></span>
* <span data-ttu-id="1c74b-130">**&lt;Wstrzymaj&gt;**: dyskretnie czeka na określoną liczbę sekund.</span><span class="sxs-lookup"><span data-stu-id="1c74b-130">**&lt;Pause&gt;**: Waits silently for a specified number of seconds.</span></span>
* <span data-ttu-id="1c74b-131">**&lt;Rekord&gt;**: rejestruje wywołującego hello głosu i zwraca adres URL pliku zawierającego hello rejestrowania.</span><span class="sxs-lookup"><span data-stu-id="1c74b-131">**&lt;Record&gt;**: Records hello caller's voice and returns a URL of a file that contains hello recording.</span></span>
* <span data-ttu-id="1c74b-132">**&lt;Przekieruj&gt;**: przekazuje kontrolę nad wywołania lub SMS toohello TwiML na inny adres URL.</span><span class="sxs-lookup"><span data-stu-id="1c74b-132">**&lt;Redirect&gt;**: Transfers control of a call or SMS toohello TwiML at a different URL.</span></span>
* <span data-ttu-id="1c74b-133">**&lt;Odrzuć&gt;**: odrzuca jako przychodzące wywołania numer usługi Twilio tooyour bez rozliczeń można.</span><span class="sxs-lookup"><span data-stu-id="1c74b-133">**&lt;Reject&gt;**: Rejects an incoming call tooyour Twilio number without billing you.</span></span>
* <span data-ttu-id="1c74b-134">**&lt;Powiedz&gt;**: Konwertuje tekst toospeech, które zostało utworzone w wywołaniu.</span><span class="sxs-lookup"><span data-stu-id="1c74b-134">**&lt;Say&gt;**: Converts text toospeech that is made on a call.</span></span>
* <span data-ttu-id="1c74b-135">**&lt;SMS&gt;**: wysyła wiadomość SMS.</span><span class="sxs-lookup"><span data-stu-id="1c74b-135">**&lt;Sms&gt;**: Sends an SMS message.</span></span>

### <span data-ttu-id="1c74b-136"><a id="TwiML"></a>TwiML</span><span class="sxs-lookup"><span data-stu-id="1c74b-136"><a id="TwiML"></a>TwiML</span></span>
<span data-ttu-id="1c74b-137">Zestaw instrukcji oparte na języku XML, oparte na powitania usługi Twilio zlecenia, które informują usługi Twilio, jak jest TwiML tooprocess wywołania lub wiadomości SMS.</span><span class="sxs-lookup"><span data-stu-id="1c74b-137">TwiML is a set of XML-based instructions based on hello Twilio verbs that inform Twilio of how tooprocess a call or SMS.</span></span>

<span data-ttu-id="1c74b-138">Na przykład powitania po TwiML może dokonać konwersji tekstu hello **Hello World!**</span><span class="sxs-lookup"><span data-stu-id="1c74b-138">As an example, hello following TwiML would convert hello text **Hello World!**</span></span> <span data-ttu-id="1c74b-139">toospeech.</span><span class="sxs-lookup"><span data-stu-id="1c74b-139">toospeech.</span></span>

```xml
    <?xml version="1.0" encoding="UTF-8" ?>
    <Response>
       <Say>Hello World!</Say>
    </Response>
```

<span data-ttu-id="1c74b-140">Podczas wywołania aplikacji hello interfejsu API usługi Twilio, jeden z parametrów interfejsu API hello jest adres URL hello, która zwraca odpowiedź TwiML hello.</span><span class="sxs-lookup"><span data-stu-id="1c74b-140">When your application calls hello Twilio API, one of hello API parameters is hello URL that returns hello TwiML response.</span></span> <span data-ttu-id="1c74b-141">Do celów programistycznych możesz użyć wprowadzone do usługi Twilio adresy URL tooprovide hello TwiML odpowiedzi są używane przez aplikacje.</span><span class="sxs-lookup"><span data-stu-id="1c74b-141">For development purposes, you can use Twilio-provided URLs tooprovide hello TwiML responses used by your applications.</span></span> <span data-ttu-id="1c74b-142">Może również udostępniać swoje własne adresy URL tooproduce hello TwiML odpowiedzi, a inną opcją jest toouse hello **TwiMLResponse** obiektu.</span><span class="sxs-lookup"><span data-stu-id="1c74b-142">You could also host your own URLs tooproduce hello TwiML responses, and another option is toouse hello **TwiMLResponse** object.</span></span>

<span data-ttu-id="1c74b-143">Aby uzyskać więcej informacji na temat usługi Twilio zlecenia i ich atrybuty oraz TwiML, zobacz [TwiML][twiml].</span><span class="sxs-lookup"><span data-stu-id="1c74b-143">For more information about Twilio verbs, their attributes, and TwiML, see [TwiML][twiml].</span></span> <span data-ttu-id="1c74b-144">Aby uzyskać dodatkowe informacje na temat hello interfejsu API usługi Twilio, zobacz [interfejsu API usługi Twilio][twilio_api].</span><span class="sxs-lookup"><span data-stu-id="1c74b-144">For additional information about hello Twilio API, see [Twilio API][twilio_api].</span></span>

## <span data-ttu-id="1c74b-145"><a id="CreateAccount"></a>Tworzenie konta usługi Twilio</span><span class="sxs-lookup"><span data-stu-id="1c74b-145"><a id="CreateAccount"></a>Create a Twilio Account</span></span>
<span data-ttu-id="1c74b-146">Jeśli wszystko jest gotowe tooget konta usługi Twilio, zarejestruj się w [spróbuj usługi Twilio][try_twilio].</span><span class="sxs-lookup"><span data-stu-id="1c74b-146">When you're ready tooget a Twilio account, sign up at [Try Twilio][try_twilio].</span></span> <span data-ttu-id="1c74b-147">Można rozpoczynać bezpłatne konto, a następnie Uaktualnij swoje konto później.</span><span class="sxs-lookup"><span data-stu-id="1c74b-147">You can start with a free account, and upgrade your account later.</span></span>

<span data-ttu-id="1c74b-148">Po utworzeniu konta dla konta usługi Twilio, otrzymasz Identyfikatora konta oraz tokenu uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="1c74b-148">When you sign up for a Twilio account, you'll receive an account ID and an authentication token.</span></span> <span data-ttu-id="1c74b-149">Zarówno będzie potrzebne toomake wywołania interfejsu API usługi Twilio.</span><span class="sxs-lookup"><span data-stu-id="1c74b-149">Both will be needed toomake Twilio API calls.</span></span> <span data-ttu-id="1c74b-150">tooprevent nieautoryzowany dostęp do konta tooyour, bezpieczeństwo Twojego tokenu uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="1c74b-150">tooprevent unauthorized access tooyour account, keep your authentication token secure.</span></span> <span data-ttu-id="1c74b-151">Twój identyfikator konta i uwierzytelniania token jest wyświetlana na powitania [usługi Twilio Console][twilio_console]w hello pola oznaczone **identyfikator SID konta** i **TOKEN uwierzytelniania**odpowiednio.</span><span class="sxs-lookup"><span data-stu-id="1c74b-151">Your account ID and authentication token are viewable at hello [Twilio Console][twilio_console], in hello fields labeled **ACCOUNT SID** and **AUTH TOKEN**, respectively.</span></span>

## <span data-ttu-id="1c74b-152"><a id="create_app"></a>Tworzenie aplikacji Java</span><span class="sxs-lookup"><span data-stu-id="1c74b-152"><a id="create_app"></a>Create a Java Application</span></span>
1. <span data-ttu-id="1c74b-153">Uzyskaj hello JAR usługi Twilio i dodać tooyour ścieżkę i używanemu zestawowi wdrożenia WAR kompilacji języka Java.</span><span class="sxs-lookup"><span data-stu-id="1c74b-153">Obtain hello Twilio JAR and add it tooyour Java build path and your WAR deployment assembly.</span></span> <span data-ttu-id="1c74b-154">W [https://github.com/twilio/twilio-java][twilio_java], możesz pobrać hello GitHub źródeł i tworzyć własne JAR lub pobrać wbudowanych JAR (z lub bez zależności).</span><span class="sxs-lookup"><span data-stu-id="1c74b-154">At [https://github.com/twilio/twilio-java][twilio_java], you can download hello GitHub sources and create your own JAR, or download a pre-built JAR (with or without dependencies).</span></span>
2. <span data-ttu-id="1c74b-155">Upewnij się, Twoje JDK **cacerts** magazynu kluczy zawiera hello firmy Equifax Secure urzędu certyfikacji certyfikatu z 67:CB:9 odcisk palca MD5 D: C0:13:24:8A:82:9B:B2:17:1E:D1:1B:EC:D4 (numer seryjny hello jest 35:DE:F4:CF i hello SHA1 Odcisk palca jest D2:32:09:AD:23:D3:14:23:21:74:E4:0 D: 7F:9 D: 62:13:97:86:63:3A).</span><span class="sxs-lookup"><span data-stu-id="1c74b-155">Ensure your JDK's **cacerts** keystore contains hello Equifax Secure Certificate Authority certificate with MD5 fingerprint 67:CB:9D:C0:13:24:8A:82:9B:B2:17:1E:D1:1B:EC:D4 (hello serial number is 35:DE:F4:CF and hello SHA1 fingerprint is D2:32:09:AD:23:D3:14:23:21:74:E4:0D:7F:9D:62:13:97:86:63:3A).</span></span> <span data-ttu-id="1c74b-156">Jest to hello certyfikat urzędu certyfikacji dla hello [https://api.twilio.com] [ twilio_api_service] usługi, która jest wywoływana, gdy używasz interfejsów API usługi Twilio.</span><span class="sxs-lookup"><span data-stu-id="1c74b-156">This is hello certificate authority (CA) certificate for hello [https://api.twilio.com][twilio_api_service] service, which is called when you use Twilio APIs.</span></span> <span data-ttu-id="1c74b-157">Informacji o sprawdzeniu Twojej JDK **cacerts** keystore zawiera hello prawidłowy certyfikat urzędu certyfikacji, zobacz [Dodawanie certyfikatu toohello magazynu certyfikatów urzędu certyfikacji Java][add_ca_cert].</span><span class="sxs-lookup"><span data-stu-id="1c74b-157">For information about ensuring your JDK's **cacerts** keystore contains hello correct CA certificate, see [Adding a Certificate toohello Java CA Certificate Store][add_ca_cert].</span></span>

<span data-ttu-id="1c74b-158">Szczegółowe instrukcje dotyczące języka Java za pomocą biblioteki klienta usługi Twilio hello są dostępne pod adresem [jak tooMake rozwiązania usługi przy użyciu Twilio w aplikacji Java na platformie Azure rozmowy telefonicznej][howto_phonecall_java].</span><span class="sxs-lookup"><span data-stu-id="1c74b-158">Detailed instructions for using hello Twilio client library for Java are available at [How tooMake a Phone Call Using Twilio in a Java Application on Azure][howto_phonecall_java].</span></span>

## <span data-ttu-id="1c74b-159"><a id="configure_app"></a>Konfigurowanie bibliotek usługi Twilio tooUse Twoja aplikacja</span><span class="sxs-lookup"><span data-stu-id="1c74b-159"><a id="configure_app"></a>Configure Your Application tooUse Twilio Libraries</span></span>
<span data-ttu-id="1c74b-160">W kodzie, możesz dodać **zaimportować** instrukcji u góry hello plików źródłowych dla hello usługi Twilio pakietów lub klasy można mają toouse w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1c74b-160">Within your code, you can add **import** statements at hello top of your source files for hello Twilio packages or classes you want toouse in your application.</span></span>

<span data-ttu-id="1c74b-161">Dla plików źródłowych Java:</span><span class="sxs-lookup"><span data-stu-id="1c74b-161">For Java source files:</span></span>

```java
    import com.twilio.*;
    import com.twilio.rest.api.*;
    import com.twilio.type.*;
    import com.twilio.twiml.*;
```

<span data-ttu-id="1c74b-162">Dla plików źródłowych Java strony serwera (JSP):</span><span class="sxs-lookup"><span data-stu-id="1c74b-162">For Java Server Page (JSP) source files:</span></span>

```java
    import="com.twilio.*"
    import="com.twilio.rest.api.*"
    import="com.twilio.type.*"
    import="com.twilio.twiml.*"
 ```
 
<span data-ttu-id="1c74b-163">W zależności od tego, które pakiety usługi Twilio lub klasy mają toouse, Twoje **zaimportować** instrukcje mogą się różnić.</span><span class="sxs-lookup"><span data-stu-id="1c74b-163">Depending on which Twilio packages or classes you want toouse, your **import** statements may be different.</span></span>

## <span data-ttu-id="1c74b-164"><a id="howto_make_call"></a>Porady: wykonywanie połączenia wychodzące</span><span class="sxs-lookup"><span data-stu-id="1c74b-164"><a id="howto_make_call"></a>How to: Make an outgoing call</span></span>
<span data-ttu-id="1c74b-165">Witaj poniżej pokazano, jak toomake wychodzące wywołanie przy użyciu hello **wywołać** klasy.</span><span class="sxs-lookup"><span data-stu-id="1c74b-165">hello following shows how toomake an outgoing call using hello **Call** class.</span></span> <span data-ttu-id="1c74b-166">Ten kod zawiera również hello tooreturn lokacja dostarczonych do usługi Twilio odpowiedzi usługi Twilio Markup Language (TwiML).</span><span class="sxs-lookup"><span data-stu-id="1c74b-166">This code also uses a Twilio-provided site tooreturn hello Twilio Markup Language (TwiML) response.</span></span> <span data-ttu-id="1c74b-167">Podstaw wartości hello **z** i **do** numerów telefonów i upewnij się, że sprawdzisz hello **z** numer telefonu dla kodu hello toorunning poprzedniego konta usługi Twilio.</span><span class="sxs-lookup"><span data-stu-id="1c74b-167">Substitute your values for hello **from** and **to** phone numbers, and ensure that you verify hello **from** phone number for your Twilio account prior toorunning hello code.</span></span>

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

<span data-ttu-id="1c74b-168">Aby uzyskać więcej informacji o parametrach hello przekazano toohello **Call.creator** metody, zobacz [http://www.twilio.com/docs/api/rest/making-calls][twilio_rest_making_calls].</span><span class="sxs-lookup"><span data-stu-id="1c74b-168">For more information about hello parameters passed in toohello **Call.creator** method, see [http://www.twilio.com/docs/api/rest/making-calls][twilio_rest_making_calls].</span></span>

<span data-ttu-id="1c74b-169">Jak wspomniano, ten kod używa hello tooreturn lokacja dostarczonych do usługi Twilio TwiML odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="1c74b-169">As mentioned, this code uses a Twilio-provided site tooreturn hello TwiML response.</span></span> <span data-ttu-id="1c74b-170">Zamiast tego można użyć własnych lokacji tooprovide hello odpowiedzi TwiML; Aby uzyskać więcej informacji, zobacz [jak tooProvide TwiML odpowiedzi w aplikacji Java na platformie Azure](#howto_provide_twiml_responses).</span><span class="sxs-lookup"><span data-stu-id="1c74b-170">You could instead use your own site tooprovide hello TwiML response; for more information, see [How tooProvide TwiML Responses in a Java Application on Azure](#howto_provide_twiml_responses).</span></span>

## <span data-ttu-id="1c74b-171"><a id="howto_send_sms"></a>Porady: Wyślij wiadomość SMS</span><span class="sxs-lookup"><span data-stu-id="1c74b-171"><a id="howto_send_sms"></a>How to: Send an SMS message</span></span>
<span data-ttu-id="1c74b-172">Witaj poniżej pokazano, jak hello toosend wiadomość SMS przy użyciu **komunikat** klasy.</span><span class="sxs-lookup"><span data-stu-id="1c74b-172">hello following shows how toosend an SMS message using hello **Message** class.</span></span> <span data-ttu-id="1c74b-173">Witaj **z** numer, **4155992671**, jest obsługiwane przez usługi Twilio, dla wersji próbnej kont toosend wiadomości SMS.</span><span class="sxs-lookup"><span data-stu-id="1c74b-173">hello **from** number, **4155992671**, is provided by Twilio for trial accounts toosend SMS messages.</span></span> <span data-ttu-id="1c74b-174">Witaj **do** należy sprawdzić liczbę dla kodu hello toorunning poprzedniego konta usługi Twilio.</span><span class="sxs-lookup"><span data-stu-id="1c74b-174">hello **to** number must be verified for your Twilio account prior toorunning hello code.</span></span>

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

<span data-ttu-id="1c74b-175">Aby uzyskać więcej informacji o parametrach hello przekazano toohello **Message.creator** metody, zobacz [http://www.twilio.com/docs/api/rest/sending-sms][twilio_rest_sending_sms].</span><span class="sxs-lookup"><span data-stu-id="1c74b-175">For more information about hello parameters passed in toohello **Message.creator** method, see [http://www.twilio.com/docs/api/rest/sending-sms][twilio_rest_sending_sms].</span></span>

## <span data-ttu-id="1c74b-176"><a id="howto_provide_twiml_responses"></a>Porady: Podaj TwiML odpowiedzi z własnej witryny sieci Web</span><span class="sxs-lookup"><span data-stu-id="1c74b-176"><a id="howto_provide_twiml_responses"></a>How to: Provide TwiML Responses from your own Website</span></span>
<span data-ttu-id="1c74b-177">Gdy aplikacja inicjuje toohello wywołania interfejsu API usługi Twilio, na przykład za pośrednictwem hello **CallCreator.create** metody usługi Twilio wyśle adres URL tooa żądania, który jest oczekiwanym tooreturn TwiML odpowiedź.</span><span class="sxs-lookup"><span data-stu-id="1c74b-177">When your application initiates a call toohello Twilio API, for example via hello **CallCreator.create** method, Twilio will send your request tooa URL that is expected tooreturn a TwiML response.</span></span> <span data-ttu-id="1c74b-178">w powyższym przykładzie Hello używa adresu URL dostarczony do usługi Twilio hello [http://twimlets.com/message][twimlet_message_url].</span><span class="sxs-lookup"><span data-stu-id="1c74b-178">hello example above uses hello Twilio-provided URL [http://twimlets.com/message][twimlet_message_url].</span></span> <span data-ttu-id="1c74b-179">(Podczas TwiML jest przeznaczony do użytku przez usługi sieci Web, można wyświetlić hello TwiML w przeglądarce.</span><span class="sxs-lookup"><span data-stu-id="1c74b-179">(While TwiML is designed for use by Web services, you can view hello TwiML in your browser.</span></span> <span data-ttu-id="1c74b-180">Na przykład kliknij pozycję [http://twimlets.com/message] [ twimlet_message_url] toosee pustą  **&lt;odpowiedzi&gt;**  element; inny przykład kliknij [http://twimlets.com/message?Message%5B0%5D=Hello%20World%21] [ twimlet_message_url_hello_world] toosee  **&lt;odpowiedzi&gt;**  element, który zawiera  **&lt;powiedzieć? &gt;**  elementu.)</span><span class="sxs-lookup"><span data-stu-id="1c74b-180">For example, click [http://twimlets.com/message][twimlet_message_url] toosee an empty **&lt;Response&gt;** element; as another example, click [http://twimlets.com/message?Message%5B0%5D=Hello%20World%21][twimlet_message_url_hello_world] toosee a **&lt;Response&gt;** element that contains a **&lt;Say&gt;** element.)</span></span>

<span data-ttu-id="1c74b-181">Zamiast polegania na adres URL udostępniony do usługi Twilio hello, można utworzyć własny adres URL w witrynie odpowiedzi HTTP.</span><span class="sxs-lookup"><span data-stu-id="1c74b-181">Instead of relying on hello Twilio-provided URL, you can create your own URL site that returns HTTP responses.</span></span> <span data-ttu-id="1c74b-182">Można utworzyć witrynę hello w dowolnym języku, który zwraca odpowiedzi HTTP; w tym temacie założono, że będzie obsługiwać hello adres URL strony JSP.</span><span class="sxs-lookup"><span data-stu-id="1c74b-182">You can create hello site in any language that returns HTTP responses; this topic assumes you'll be hosting hello URL in a JSP page.</span></span>

<span data-ttu-id="1c74b-183">Witaj po JSP wyników strony w odpowiedzi TwiML z informacją, **Hello World!**</span><span class="sxs-lookup"><span data-stu-id="1c74b-183">hello following JSP page results in a TwiML response that says **Hello World!**</span></span> <span data-ttu-id="1c74b-184">na powitania wywołania.</span><span class="sxs-lookup"><span data-stu-id="1c74b-184">on hello call.</span></span>

```xml
    <%@ page contentType="text/xml" %>
    <Response>
        <Say>Hello World!</Say>
    </Response>
```

<span data-ttu-id="1c74b-185">powitania po JSP wyników strony w odpowiedzi TwiML informacją część tekstu, ma kilka pauzy i mówi informacje o wersji interfejsu API usługi Twilio hello i nazwy roli Azure hello.</span><span class="sxs-lookup"><span data-stu-id="1c74b-185">hello following JSP page results in a TwiML response that says some text, has several pauses, and says information about hello Twilio API version and hello Azure role name.</span></span>

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

<span data-ttu-id="1c74b-186">Witaj **ApiVersion** parametr jest dostępny w żądaniach głosu usługi Twilio (nie liczba żądań programu SMS).</span><span class="sxs-lookup"><span data-stu-id="1c74b-186">hello **ApiVersion** parameter is available in Twilio voice requests (not SMS requests).</span></span> <span data-ttu-id="1c74b-187">Parametry żądania dostępne hello toosee głosowe usługi Twilio i żądań programu SMS, zobacz <https://www.twilio.com/docs/api/twiml/twilio_request> i <https://www.twilio.com/docs/api/twiml/sms/twilio_request >odpowiednio.</span><span class="sxs-lookup"><span data-stu-id="1c74b-187">toosee hello available request parameters for Twilio voice and SMS requests, see <https://www.twilio.com/docs/api/twiml/twilio_request> and <https://www.twilio.com/docs/api/twiml/sms/twilio_request>, respectively.</span></span> <span data-ttu-id="1c74b-188">Witaj **RoleName** zmiennej środowiskowej jest dostępna jako część wdrożenia usługi Azure.</span><span class="sxs-lookup"><span data-stu-id="1c74b-188">hello **RoleName** environment variable is available as part of an Azure deployment.</span></span> <span data-ttu-id="1c74b-189">(Zmiennych środowiskowych niestandardowych tooadd ma tak one może zostać pobrana z **System.getenv**, zobacz sekcję zmiennych środowiska hello na [dodatkowych ustawień konfiguracji roli] [misc_role_config_settings].)</span><span class="sxs-lookup"><span data-stu-id="1c74b-189">(If you want tooadd custom environment variables so they could be picked up from **System.getenv**, see hello environment variables section at [Miscellaneous Role Configuration Settings][misc_role_config_settings].)</span></span>

<span data-ttu-id="1c74b-190">Po utworzeniu strony JSP Konfigurowanie odpowiedzi TwiML tooprovide, użyj hello adres URL strony JSP hello hello adres URL przekazany hello **Call.creator** metody.</span><span class="sxs-lookup"><span data-stu-id="1c74b-190">Once you have your JSP page set up tooprovide TwiML responses, use hello URL of hello JSP page as hello URL passed into hello **Call.creator** method.</span></span> <span data-ttu-id="1c74b-191">Na przykład, jeśli masz aplikację sieci Web o nazwie tooan MyTwiML wdrożone Azure hostowanej usługi i hello nazwa strony JSP hello jest mytwiml.jsp, hello adres URL, które mogą zostać przekazane za**Call.creator** jak pokazano poniżej hello:</span><span class="sxs-lookup"><span data-stu-id="1c74b-191">For example, if you have a Web application named MyTwiML deployed tooan Azure hosted service, and hello name of hello JSP page is mytwiml.jsp, hello URL can be passed too**Call.creator** as shown in hello following:</span></span>

```java
    // Declare tooand From numbers and hello URL of your JSP page
    PhoneNumber too= new PhoneNumber("NNNNNNNNNN");
    PhoneNumber from = new PhoneNumber("NNNNNNNNNN");
    URI uri = new URI("http://<your_hosted_service>.cloudapp.net/MyTwiML/mytwiml.jsp");

    // Create a Call creator passing From, tooand URL values
    // then make hello call by executing hello create() method
    Call.creator(to, from, uri).create();
```

<span data-ttu-id="1c74b-192">Inną opcją w przypadku odpowiadać TwiML odbywa się za pośrednictwem hello **VoiceResponse** klasy, która jest dostępna w hello **com.twilio.twiml** pakietu.</span><span class="sxs-lookup"><span data-stu-id="1c74b-192">Another option for responding with TwiML is via hello **VoiceResponse** class, which is available in hello **com.twilio.twiml** package.</span></span>

<span data-ttu-id="1c74b-193">Aby uzyskać dodatkowe informacje dotyczące korzystania z usługi Twilio w platformie Azure za pomocą języka Java, zobacz [jak tooMake rozwiązania usługi przy użyciu Twilio w aplikacji Java na platformie Azure rozmowy telefonicznej][howto_phonecall_java].</span><span class="sxs-lookup"><span data-stu-id="1c74b-193">For additional information about using Twilio in Azure with Java, see [How tooMake a Phone Call Using Twilio in a Java Application on Azure][howto_phonecall_java].</span></span>

## <span data-ttu-id="1c74b-194"><a id="AdditionalServices"></a>Porady: korzystania z usługi Twilio dodatkowych usług</span><span class="sxs-lookup"><span data-stu-id="1c74b-194"><a id="AdditionalServices"></a>How to: Use Additional Twilio Services</span></span>
<span data-ttu-id="1c74b-195">Ponadto przykłady toohello pokazane, usługi Twilio oferuje API sieci web można używać tooleverage dodatkowe usługi Twilio funkcji z aplikacji Azure.</span><span class="sxs-lookup"><span data-stu-id="1c74b-195">In addition toohello examples shown here, Twilio offers web-based APIs that you can use tooleverage additional Twilio functionality from your Azure application.</span></span> <span data-ttu-id="1c74b-196">Aby uzyskać szczegółowe informacje, zobacz hello [dokumentacji interfejsu API usługi Twilio][twilio_api_documentation].</span><span class="sxs-lookup"><span data-stu-id="1c74b-196">For full details, see hello [Twilio API documentation][twilio_api_documentation].</span></span>

## <span data-ttu-id="1c74b-197"><a id="NextSteps"></a>Następne kroki</span><span class="sxs-lookup"><span data-stu-id="1c74b-197"><a id="NextSteps"></a>Next Steps</span></span>
<span data-ttu-id="1c74b-198">Teraz, kiedy znasz już podstawy hello hello usługi usługi Twilio, wykonaj te więcej toolearn łącza:</span><span class="sxs-lookup"><span data-stu-id="1c74b-198">Now that you've learned hello basics of hello Twilio service, follow these links toolearn more:</span></span>

* <span data-ttu-id="1c74b-199">[Wytyczne dotyczące zabezpieczeń usługi Twilio][twilio_security_guidelines]</span><span class="sxs-lookup"><span data-stu-id="1c74b-199">[Twilio Security Guidelines][twilio_security_guidelines]</span></span>
* <span data-ttu-id="1c74b-200">[Porada usługi Twilio i przykładowy kod][twilio_howtos]</span><span class="sxs-lookup"><span data-stu-id="1c74b-200">[Twilio HowTo's and Example Code][twilio_howtos]</span></span>
* <span data-ttu-id="1c74b-201">[Samouczki usługi Twilio Szybki Start][twilio_quickstarts]</span><span class="sxs-lookup"><span data-stu-id="1c74b-201">[Twilio Quickstart Tutorials][twilio_quickstarts]</span></span>
* <span data-ttu-id="1c74b-202">[Usługi Twilio w witrynie GitHub][twilio_on_github]</span><span class="sxs-lookup"><span data-stu-id="1c74b-202">[Twilio on GitHub][twilio_on_github]</span></span>
* <span data-ttu-id="1c74b-203">[Porozmawiaj tooTwilio pomocy technicznej][twilio_support]</span><span class="sxs-lookup"><span data-stu-id="1c74b-203">[Talk tooTwilio Support][twilio_support]</span></span>

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
