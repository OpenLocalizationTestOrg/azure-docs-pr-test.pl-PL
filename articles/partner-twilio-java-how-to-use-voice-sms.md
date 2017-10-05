---
title: "Jak używać usługi Twilio głosowe i programu SMS (Java) | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak wykonać połączenie telefoniczne i wysłać wiadomość SMS z usługi interfejsu API usługi Twilio na platformie Azure. Przykłady kodu napisane w języku Java."
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
ms.openlocfilehash: 5a1b2ffa160a31b639605242b651dc8d14e7a01b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-twilio-for-voice-and-sms-capabilities-in-java"></a><span data-ttu-id="10d38-104">Jak używać usługi Twilio głosowe i możliwości programu SMS w języku Java</span><span class="sxs-lookup"><span data-stu-id="10d38-104">How to Use Twilio for Voice and SMS Capabilities in Java</span></span>
<span data-ttu-id="10d38-105">W tym przewodniku przedstawiono sposób wykonywania typowych zadań programowania usługi interfejsu API usługi Twilio na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="10d38-105">This guide demonstrates how to perform common programming tasks with the Twilio API service on Azure.</span></span> <span data-ttu-id="10d38-106">Omówione scenariusze obejmują tworzenie połączeń telefonicznych i wysyłanie wiadomości krótką wiadomość usługi (SMS).</span><span class="sxs-lookup"><span data-stu-id="10d38-106">The scenarios covered include making a phone call and sending a Short Message Service (SMS) message.</span></span> <span data-ttu-id="10d38-107">Aby uzyskać więcej informacji na temat usługi Twilio i komunikacja głosowa programu SMS w aplikacji, zobacz [następne kroki](#NextSteps) sekcji.</span><span class="sxs-lookup"><span data-stu-id="10d38-107">For more information on Twilio and using voice and SMS in your applications, see the [Next Steps](#NextSteps) section.</span></span>

## <span data-ttu-id="10d38-108"><a id="WhatIs"></a>Co to jest usługi Twilio?</span><span class="sxs-lookup"><span data-stu-id="10d38-108"><a id="WhatIs"></a>What is Twilio?</span></span>
<span data-ttu-id="10d38-109">Usługi Twilio jest interfejs API usługi sieci web telefonii, które umożliwia tworzenie aplikacji programu SMS i komunikacja głosowa przy użyciu istniejących języków sieci web i umiejętności.</span><span class="sxs-lookup"><span data-stu-id="10d38-109">Twilio is a telephony web-service API that lets you use your existing web languages and skills to build voice and SMS applications.</span></span> <span data-ttu-id="10d38-110">Usługi Twilio jest usługą innych firm (nie funkcji platformy Azure i nie produkt firmy Microsoft).</span><span class="sxs-lookup"><span data-stu-id="10d38-110">Twilio is a third-party service (not an Azure feature and not a Microsoft product).</span></span>

<span data-ttu-id="10d38-111">**Usługi Twilio głosu** umożliwia aplikacjom wykonywanie i odbieranie połączeń telefonicznych.</span><span class="sxs-lookup"><span data-stu-id="10d38-111">**Twilio Voice** allows your applications to make and receive phone calls.</span></span> <span data-ttu-id="10d38-112">**SMS usługi Twilio** umożliwia aplikacjom wykonywanie i odbieranie wiadomości SMS.</span><span class="sxs-lookup"><span data-stu-id="10d38-112">**Twilio SMS** allows your applications to make and receive SMS messages.</span></span> <span data-ttu-id="10d38-113">**Klient usługi Twilio** umożliwia aplikacjom włączyć komunikację głosową, przy użyciu istniejących połączeń internetowych, w tym przenośnych połączenia.</span><span class="sxs-lookup"><span data-stu-id="10d38-113">**Twilio Client** allows your applications to enable voice communication using existing Internet connections, including mobile connections.</span></span>

## <span data-ttu-id="10d38-114"><a id="Pricing"></a>Cennik usługi Twilio i oferty specjalne</span><span class="sxs-lookup"><span data-stu-id="10d38-114"><a id="Pricing"></a>Twilio Pricing and Special Offers</span></span>
<span data-ttu-id="10d38-115">Informacje o cenach usługi Twilio znajduje się w temacie [cennik usługi Twilio][twilio_pricing].</span><span class="sxs-lookup"><span data-stu-id="10d38-115">Information about Twilio pricing is available at [Twilio Pricing][twilio_pricing].</span></span> <span data-ttu-id="10d38-116">Azure klienci otrzymają [oferta specjalna][special_offer]: wolnego środki tekstów 1000 lub 1000 ruchu przychodzącego minut.</span><span class="sxs-lookup"><span data-stu-id="10d38-116">Azure customers receive a [special offer][special_offer]: a free credit of 1000 texts or 1000 inbound minutes.</span></span> <span data-ttu-id="10d38-117">Zapisz się do tej oferty lub uzyskać więcej informacji, odwiedź [http://ahoy.twilio.com/azure][special_offer].</span><span class="sxs-lookup"><span data-stu-id="10d38-117">To sign up for this offer or get more information, please visit [http://ahoy.twilio.com/azure][special_offer].</span></span>

## <span data-ttu-id="10d38-118"><a id="Concepts"></a>Pojęcia</span><span class="sxs-lookup"><span data-stu-id="10d38-118"><a id="Concepts"></a>Concepts</span></span>
<span data-ttu-id="10d38-119">Interfejs API usługi Twilio jest interfejs API RESTful, która zapewnia funkcje programu SMS i komunikacja głosowa aplikacji.</span><span class="sxs-lookup"><span data-stu-id="10d38-119">The Twilio API is a RESTful API that provides voice and SMS functionality for applications.</span></span> <span data-ttu-id="10d38-120">Klient biblioteki są dostępne w wielu językach; Aby uzyskać listę, zobacz [bibliotek interfejsu API usługi Twilio][twilio_libraries].</span><span class="sxs-lookup"><span data-stu-id="10d38-120">Client libraries are available in multiple languages; for a list, see [Twilio API Libraries][twilio_libraries].</span></span>

<span data-ttu-id="10d38-121">Kluczowe aspekty interfejsu API usługi Twilio są zleceń usługi Twilio i usługi Twilio Markup Language (TwiML).</span><span class="sxs-lookup"><span data-stu-id="10d38-121">Key aspects of the Twilio API are Twilio verbs and Twilio Markup Language (TwiML).</span></span>

### <span data-ttu-id="10d38-122"><a id="Verbs"></a>Usługi Twilio zlecenia</span><span class="sxs-lookup"><span data-stu-id="10d38-122"><a id="Verbs"></a>Twilio Verbs</span></span>
<span data-ttu-id="10d38-123">Interfejs API korzysta z usługi Twilio zleceń; na przykład  **&lt;powiedzieć&gt;**  zlecenie powoduje, że usługi Twilio komputerowi dostarczenia komunikatu w wywołaniu.</span><span class="sxs-lookup"><span data-stu-id="10d38-123">The API makes use of Twilio verbs; for example, the **&lt;Say&gt;** verb instructs Twilio to audibly deliver a message on a call.</span></span>

<span data-ttu-id="10d38-124">Poniżej znajduje się lista zleceń usługi Twilio.</span><span class="sxs-lookup"><span data-stu-id="10d38-124">The following is a list of Twilio verbs.</span></span>

* <span data-ttu-id="10d38-125">**&lt;Wybierania&gt;**: łączy wywołującego innego numeru telefonu.</span><span class="sxs-lookup"><span data-stu-id="10d38-125">**&lt;Dial&gt;**: Connects the caller to another phone.</span></span>
* <span data-ttu-id="10d38-126">**&lt;Zbierz&gt;**: zbiera cyfry wprowadzone na klawiaturze telefonu.</span><span class="sxs-lookup"><span data-stu-id="10d38-126">**&lt;Gather&gt;**: Collects numeric digits entered on the telephone keypad.</span></span>
* <span data-ttu-id="10d38-127">**&lt;Rozłączanie&gt;**: kończy wywołanie.</span><span class="sxs-lookup"><span data-stu-id="10d38-127">**&lt;Hangup&gt;**: Ends a call.</span></span>
* <span data-ttu-id="10d38-128">**&lt;Odtwórz&gt;**: odtwarzania pliku audio.</span><span class="sxs-lookup"><span data-stu-id="10d38-128">**&lt;Play&gt;**: Plays an audio file.</span></span>
* <span data-ttu-id="10d38-129">**&lt;Kolejka&gt;**: Dodaj do kolejki obiekty wywołujące.</span><span class="sxs-lookup"><span data-stu-id="10d38-129">**&lt;Queue&gt;**: Add the to a queue of callers.</span></span>
* <span data-ttu-id="10d38-130">**&lt;Wstrzymaj&gt;**: dyskretnie czeka na określoną liczbę sekund.</span><span class="sxs-lookup"><span data-stu-id="10d38-130">**&lt;Pause&gt;**: Waits silently for a specified number of seconds.</span></span>
* <span data-ttu-id="10d38-131">**&lt;Rekord&gt;**: rejestruje wywołującego głosu i zwraca adres URL pliku zawierającego nagrywania.</span><span class="sxs-lookup"><span data-stu-id="10d38-131">**&lt;Record&gt;**: Records the caller's voice and returns a URL of a file that contains the recording.</span></span>
* <span data-ttu-id="10d38-132">**&lt;Przekieruj&gt;**: przekazuje kontrolę nad wywołania lub wiadomości SMS do TwiML na inny adres URL.</span><span class="sxs-lookup"><span data-stu-id="10d38-132">**&lt;Redirect&gt;**: Transfers control of a call or SMS to the TwiML at a different URL.</span></span>
* <span data-ttu-id="10d38-133">**&lt;Odrzuć&gt;**: odrzucanie połączenia przychodzącego na numer usługi Twilio bez rozliczeń można.</span><span class="sxs-lookup"><span data-stu-id="10d38-133">**&lt;Reject&gt;**: Rejects an incoming call to your Twilio number without billing you.</span></span>
* <span data-ttu-id="10d38-134">**&lt;Powiedz&gt;**: Konwertuje tekst na mowę, które zostało utworzone w wywołaniu.</span><span class="sxs-lookup"><span data-stu-id="10d38-134">**&lt;Say&gt;**: Converts text to speech that is made on a call.</span></span>
* <span data-ttu-id="10d38-135">**&lt;SMS&gt;**: wysyła wiadomość SMS.</span><span class="sxs-lookup"><span data-stu-id="10d38-135">**&lt;Sms&gt;**: Sends an SMS message.</span></span>

### <span data-ttu-id="10d38-136"><a id="TwiML"></a>TwiML</span><span class="sxs-lookup"><span data-stu-id="10d38-136"><a id="TwiML"></a>TwiML</span></span>
<span data-ttu-id="10d38-137">TwiML to zestaw instrukcji oparte na języku XML, oparte na zlecenia usługi Twilio, które informują usługi Twilio sposobu przetwarzania połączenia lub wiadomości SMS.</span><span class="sxs-lookup"><span data-stu-id="10d38-137">TwiML is a set of XML-based instructions based on the Twilio verbs that inform Twilio of how to process a call or SMS.</span></span>

<span data-ttu-id="10d38-138">Na przykład następujące TwiML czy Konwertuj tekst **Hello World!**</span><span class="sxs-lookup"><span data-stu-id="10d38-138">As an example, the following TwiML would convert the text **Hello World!**</span></span> <span data-ttu-id="10d38-139">Aby mowy.</span><span class="sxs-lookup"><span data-stu-id="10d38-139">to speech.</span></span>

```xml
    <?xml version="1.0" encoding="UTF-8" ?>
    <Response>
       <Say>Hello World!</Say>
    </Response>
```

<span data-ttu-id="10d38-140">Gdy aplikacja wywołuje interfejs API usługi Twilio, jeden z parametrów interfejsu API jest adres URL, który zwraca odpowiedź TwiML.</span><span class="sxs-lookup"><span data-stu-id="10d38-140">When your application calls the Twilio API, one of the API parameters is the URL that returns the TwiML response.</span></span> <span data-ttu-id="10d38-141">Do celów programistycznych wprowadzone do usługi Twilio adresy URL służy do nadania odpowiedzi TwiML używane przez aplikacje.</span><span class="sxs-lookup"><span data-stu-id="10d38-141">For development purposes, you can use Twilio-provided URLs to provide the TwiML responses used by your applications.</span></span> <span data-ttu-id="10d38-142">Może również udostępniać swoje własne adresy URL do tworzenia odpowiedzi TwiML i inną opcją jest użycie **TwiMLResponse** obiektu.</span><span class="sxs-lookup"><span data-stu-id="10d38-142">You could also host your own URLs to produce the TwiML responses, and another option is to use the **TwiMLResponse** object.</span></span>

<span data-ttu-id="10d38-143">Aby uzyskać więcej informacji na temat usługi Twilio zlecenia i ich atrybuty oraz TwiML, zobacz [TwiML][twiml].</span><span class="sxs-lookup"><span data-stu-id="10d38-143">For more information about Twilio verbs, their attributes, and TwiML, see [TwiML][twiml].</span></span> <span data-ttu-id="10d38-144">Aby uzyskać dodatkowe informacje na temat interfejsu API usługi Twilio, zobacz [interfejsu API usługi Twilio][twilio_api].</span><span class="sxs-lookup"><span data-stu-id="10d38-144">For additional information about the Twilio API, see [Twilio API][twilio_api].</span></span>

## <span data-ttu-id="10d38-145"><a id="CreateAccount"></a>Tworzenie konta usługi Twilio</span><span class="sxs-lookup"><span data-stu-id="10d38-145"><a id="CreateAccount"></a>Create a Twilio Account</span></span>
<span data-ttu-id="10d38-146">Po przygotowaniu można uzyskać konta usługi Twilio, zarejestruj się w [spróbuj usługi Twilio][try_twilio].</span><span class="sxs-lookup"><span data-stu-id="10d38-146">When you're ready to get a Twilio account, sign up at [Try Twilio][try_twilio].</span></span> <span data-ttu-id="10d38-147">Można rozpoczynać bezpłatne konto, a następnie Uaktualnij swoje konto później.</span><span class="sxs-lookup"><span data-stu-id="10d38-147">You can start with a free account, and upgrade your account later.</span></span>

<span data-ttu-id="10d38-148">Po utworzeniu konta dla konta usługi Twilio, otrzymasz Identyfikatora konta oraz tokenu uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="10d38-148">When you sign up for a Twilio account, you'll receive an account ID and an authentication token.</span></span> <span data-ttu-id="10d38-149">Zarówno będą potrzebne w celu wykonywania wywołań interfejsu API usługi Twilio.</span><span class="sxs-lookup"><span data-stu-id="10d38-149">Both will be needed to make Twilio API calls.</span></span> <span data-ttu-id="10d38-150">Aby uniemożliwić nieautoryzowany dostęp do Twojego konta, bezpieczeństwo Twojego tokenu uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="10d38-150">To prevent unauthorized access to your account, keep your authentication token secure.</span></span> <span data-ttu-id="10d38-151">Twój identyfikator konta i uwierzytelniania tokenu jest wyświetlana w [usługi Twilio Console][twilio_console], w polach etykietą **identyfikator SID konta** i **TOKEN uwierzytelniania**odpowiednio.</span><span class="sxs-lookup"><span data-stu-id="10d38-151">Your account ID and authentication token are viewable at the [Twilio Console][twilio_console], in the fields labeled **ACCOUNT SID** and **AUTH TOKEN**, respectively.</span></span>

## <span data-ttu-id="10d38-152"><a id="create_app"></a>Tworzenie aplikacji Java</span><span class="sxs-lookup"><span data-stu-id="10d38-152"><a id="create_app"></a>Create a Java Application</span></span>
1. <span data-ttu-id="10d38-153">Uzyskaj JAR usługi Twilio i dodaj go do ścieżka kompilacji języka Java i używanemu zestawowi wdrożenia WAR.</span><span class="sxs-lookup"><span data-stu-id="10d38-153">Obtain the Twilio JAR and add it to your Java build path and your WAR deployment assembly.</span></span> <span data-ttu-id="10d38-154">W [https://github.com/twilio/twilio-java][twilio_java], możesz pobrać źródeł GitHub i tworzyć własne JAR lub pobrać wbudowanych JAR (z lub bez zależności).</span><span class="sxs-lookup"><span data-stu-id="10d38-154">At [https://github.com/twilio/twilio-java][twilio_java], you can download the GitHub sources and create your own JAR, or download a pre-built JAR (with or without dependencies).</span></span>
2. <span data-ttu-id="10d38-155">Upewnij się, Twoje JDK **cacerts** magazynu kluczy zawiera certyfikat firmy Equifax Secure urzędu certyfikacji z 67:CB:9 odcisk palca MD5 D: C0:13:24:8A:82:9B:B2:17:1E:D1:1B:EC:D4 (numer seryjny jest 35:DE:F4:CF i SHA1 Odcisk palca jest D2:32:09:AD:23:D3:14:23:21:74:E4:0 D: 7F:9 D: 62:13:97:86:63:3A).</span><span class="sxs-lookup"><span data-stu-id="10d38-155">Ensure your JDK's **cacerts** keystore contains the Equifax Secure Certificate Authority certificate with MD5 fingerprint 67:CB:9D:C0:13:24:8A:82:9B:B2:17:1E:D1:1B:EC:D4 (the serial number is 35:DE:F4:CF and the SHA1 fingerprint is D2:32:09:AD:23:D3:14:23:21:74:E4:0D:7F:9D:62:13:97:86:63:3A).</span></span> <span data-ttu-id="10d38-156">Jest to certyfikat urzędu certyfikacji dla [https://api.twilio.com] [ twilio_api_service] usługi, która jest wywoływana, gdy używasz interfejsów API usługi Twilio.</span><span class="sxs-lookup"><span data-stu-id="10d38-156">This is the certificate authority (CA) certificate for the [https://api.twilio.com][twilio_api_service] service, which is called when you use Twilio APIs.</span></span> <span data-ttu-id="10d38-157">Informacji o sprawdzeniu Twojej JDK **cacerts** keystore zawiera prawidłowy certyfikat urzędu certyfikacji, zobacz [Dodawanie certyfikatu do magazynu certyfikatów urzędu certyfikacji Java][add_ca_cert].</span><span class="sxs-lookup"><span data-stu-id="10d38-157">For information about ensuring your JDK's **cacerts** keystore contains the correct CA certificate, see [Adding a Certificate to the Java CA Certificate Store][add_ca_cert].</span></span>

<span data-ttu-id="10d38-158">Szczegółowe instrukcje dotyczące korzystania z biblioteki klienta usługi Twilio dla języka Java są dostępne pod adresem [porady: Tworzenie usługi przy użyciu połączenia telefonicznego Twilio w aplikacji Java na platformie Azure][howto_phonecall_java].</span><span class="sxs-lookup"><span data-stu-id="10d38-158">Detailed instructions for using the Twilio client library for Java are available at [How to Make a Phone Call Using Twilio in a Java Application on Azure][howto_phonecall_java].</span></span>

## <span data-ttu-id="10d38-159"><a id="configure_app"></a>Konfigurowanie aplikacji przy użyciu bibliotek usługi Twilio</span><span class="sxs-lookup"><span data-stu-id="10d38-159"><a id="configure_app"></a>Configure Your Application to Use Twilio Libraries</span></span>
<span data-ttu-id="10d38-160">W kodzie, możesz dodać **zaimportować** instrukcje w górnej części plików źródłowych dla pakietów usługi Twilio lub klasy, które ma być używany w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="10d38-160">Within your code, you can add **import** statements at the top of your source files for the Twilio packages or classes you want to use in your application.</span></span>

<span data-ttu-id="10d38-161">Dla plików źródłowych Java:</span><span class="sxs-lookup"><span data-stu-id="10d38-161">For Java source files:</span></span>

```java
    import com.twilio.*;
    import com.twilio.rest.api.*;
    import com.twilio.type.*;
    import com.twilio.twiml.*;
```

<span data-ttu-id="10d38-162">Dla plików źródłowych Java strony serwera (JSP):</span><span class="sxs-lookup"><span data-stu-id="10d38-162">For Java Server Page (JSP) source files:</span></span>

```java
    import="com.twilio.*"
    import="com.twilio.rest.api.*"
    import="com.twilio.type.*"
    import="com.twilio.twiml.*"
 ```
 
<span data-ttu-id="10d38-163">W zależności od tego, które pakiety usługi Twilio lub klasy, do którego chcesz użyć, Twoje **zaimportować** instrukcje mogą się różnić.</span><span class="sxs-lookup"><span data-stu-id="10d38-163">Depending on which Twilio packages or classes you want to use, your **import** statements may be different.</span></span>

## <span data-ttu-id="10d38-164"><a id="howto_make_call"></a>Porady: wykonywanie połączenia wychodzące</span><span class="sxs-lookup"><span data-stu-id="10d38-164"><a id="howto_make_call"></a>How to: Make an outgoing call</span></span>
<span data-ttu-id="10d38-165">Poniżej pokazano, jak wykonać wychodzące wywołanie przy użyciu **wywołać** klasy.</span><span class="sxs-lookup"><span data-stu-id="10d38-165">The following shows how to make an outgoing call using the **Call** class.</span></span> <span data-ttu-id="10d38-166">Ten kod zawiera również lokacja dostarczonych do usługi Twilio do zwracania odpowiedzi usługi Twilio Markup Language (TwiML).</span><span class="sxs-lookup"><span data-stu-id="10d38-166">This code also uses a Twilio-provided site to return the Twilio Markup Language (TwiML) response.</span></span> <span data-ttu-id="10d38-167">Podstaw wartości **z** i **do** numerów telefonów i upewnij się, że sprawdzisz **z** numer telefonu dla konta usługi Twilio przed uruchomieniem kodu.</span><span class="sxs-lookup"><span data-stu-id="10d38-167">Substitute your values for the **from** and **to** phone numbers, and ensure that you verify the **from** phone number for your Twilio account prior to running the code.</span></span>

```java
    // Use your account SID and authentication token instead
    // of the placeholders shown here.
    String accountSID = "your_twilio_account_SID";
    String authToken = "your_twilio_authentication_token";

    // Initialize the Twilio client.
    Twilio.init(accountSID, authToken);

    // Use the Twilio-provided site for the TwiML response.
    URI uri = new URI("http://twimlets.com/message" +
            "?Message%5B0%5D=Hello%20World%21");

    // Declare To and From numbers
    PhoneNumber to = new PhoneNumber("NNNNNNNNNN");
    PhoneNumber from = new PhoneNumber("NNNNNNNNNN");

    // Create a Call creator passing From, To and URL values
    // then make the call by executing the create() method
    Call.creator(to, from, uri).create();
```

<span data-ttu-id="10d38-168">Aby uzyskać więcej informacji na temat parametrów przekazanych do **Call.creator** metody, zobacz [http://www.twilio.com/docs/api/rest/making-calls][twilio_rest_making_calls].</span><span class="sxs-lookup"><span data-stu-id="10d38-168">For more information about the parameters passed in to the **Call.creator** method, see [http://www.twilio.com/docs/api/rest/making-calls][twilio_rest_making_calls].</span></span>

<span data-ttu-id="10d38-169">Jak wspomniano, ten kod używa lokacja dostarczonych do usługi Twilio do zwracania odpowiedzi TwiML.</span><span class="sxs-lookup"><span data-stu-id="10d38-169">As mentioned, this code uses a Twilio-provided site to return the TwiML response.</span></span> <span data-ttu-id="10d38-170">Własnej witryny można zamiast tego użyć, aby zapewnić odpowiedzi TwiML; Aby uzyskać więcej informacji, zobacz [jak zapewnić TwiML odpowiedzi w aplikacji Java na platformie Azure](#howto_provide_twiml_responses).</span><span class="sxs-lookup"><span data-stu-id="10d38-170">You could instead use your own site to provide the TwiML response; for more information, see [How to Provide TwiML Responses in a Java Application on Azure](#howto_provide_twiml_responses).</span></span>

## <span data-ttu-id="10d38-171"><a id="howto_send_sms"></a>Porady: Wyślij wiadomość SMS</span><span class="sxs-lookup"><span data-stu-id="10d38-171"><a id="howto_send_sms"></a>How to: Send an SMS message</span></span>
<span data-ttu-id="10d38-172">Poniżej pokazano, jak wysyłać wiadomość SMS przy użyciu **komunikat** klasy.</span><span class="sxs-lookup"><span data-stu-id="10d38-172">The following shows how to send an SMS message using the **Message** class.</span></span> <span data-ttu-id="10d38-173">**z** numer, **4155992671**, są udostępniane przez usługi Twilio dla konta wersji próbnej można wysłać wiadomości SMS.</span><span class="sxs-lookup"><span data-stu-id="10d38-173">The **from** number, **4155992671**, is provided by Twilio for trial accounts to send SMS messages.</span></span> <span data-ttu-id="10d38-174">**Do** numer muszą być weryfikowane dla konta usługi Twilio przed uruchomieniem kodu.</span><span class="sxs-lookup"><span data-stu-id="10d38-174">The **to** number must be verified for your Twilio account prior to running the code.</span></span>

```java
    // Use your account SID and authentication token instead
    // of the placeholders shown here.
    String accountSID = "your_twilio_account_SID";
    String authToken = "your_twilio_authentication_token";

    // Initialize the Twilio client.
    Twilio.init(accountSID, authToken);

    // Declare To and From numbers and the Body of the SMS message
    PhoneNumber to = new PhoneNumber("+14159352345"); // Replace with a valid phone number for your account.
    PhoneNumber from = new PhoneNumber("+14158141829"); // Replace with a valid phone number for your account.
    String body = "Where's Wallace?";

    // Create a Message creator passing From, To and Body values
    // then send the SMS message by calling the create() method
    Message sms = Message.creator(to, from, body).create();
```

<span data-ttu-id="10d38-175">Aby uzyskać więcej informacji na temat parametrów przekazanych do **Message.creator** metody, zobacz [http://www.twilio.com/docs/api/rest/sending-sms][twilio_rest_sending_sms].</span><span class="sxs-lookup"><span data-stu-id="10d38-175">For more information about the parameters passed in to the **Message.creator** method, see [http://www.twilio.com/docs/api/rest/sending-sms][twilio_rest_sending_sms].</span></span>

## <span data-ttu-id="10d38-176"><a id="howto_provide_twiml_responses"></a>Porady: Podaj TwiML odpowiedzi z własnej witryny sieci Web</span><span class="sxs-lookup"><span data-stu-id="10d38-176"><a id="howto_provide_twiml_responses"></a>How to: Provide TwiML Responses from your own Website</span></span>
<span data-ttu-id="10d38-177">Gdy aplikacja inicjuje wywołanie interfejsu API usługi Twilio, na przykład za pomocą **CallCreator.create** metody usługi Twilio wyśle żądanie do adresu URL, który powinien zwrócić odpowiedzi TwiML.</span><span class="sxs-lookup"><span data-stu-id="10d38-177">When your application initiates a call to the Twilio API, for example via the **CallCreator.create** method, Twilio will send your request to a URL that is expected to return a TwiML response.</span></span> <span data-ttu-id="10d38-178">W powyższym przykładzie korzysta z adresu URL dostarczony do usługi Twilio [http://twimlets.com/message][twimlet_message_url].</span><span class="sxs-lookup"><span data-stu-id="10d38-178">The example above uses the Twilio-provided URL [http://twimlets.com/message][twimlet_message_url].</span></span> <span data-ttu-id="10d38-179">(Podczas TwiML jest przeznaczony do użytku przez usługi sieci Web, można wyświetlić TwiML w przeglądarce.</span><span class="sxs-lookup"><span data-stu-id="10d38-179">(While TwiML is designed for use by Web services, you can view the TwiML in your browser.</span></span> <span data-ttu-id="10d38-180">Na przykład kliknij pozycję [http://twimlets.com/message] [ twimlet_message_url] wyświetlić pustą  **&lt;odpowiedzi&gt;**  element; inny przykład kliknij [http://twimlets.com/message?Message%5B0%5D=Hello%20World%21] [ twimlet_message_url_hello_world] wyświetlić  **&lt;odpowiedzi&gt;**  element, który zawiera  **&lt;powiedzieć? &gt;**  elementu.)</span><span class="sxs-lookup"><span data-stu-id="10d38-180">For example, click [http://twimlets.com/message][twimlet_message_url] to see an empty **&lt;Response&gt;** element; as another example, click [http://twimlets.com/message?Message%5B0%5D=Hello%20World%21][twimlet_message_url_hello_world] to see a **&lt;Response&gt;** element that contains a **&lt;Say&gt;** element.)</span></span>

<span data-ttu-id="10d38-181">Zamiast polegania na adres URL dostarczony do usługi Twilio, można utworzyć własny adres URL w witrynie odpowiedzi HTTP.</span><span class="sxs-lookup"><span data-stu-id="10d38-181">Instead of relying on the Twilio-provided URL, you can create your own URL site that returns HTTP responses.</span></span> <span data-ttu-id="10d38-182">Można utworzyć witryny w dowolnym języku, który zwraca odpowiedzi HTTP; w tym temacie założono, że będzie obsługiwać adres URL strony JSP.</span><span class="sxs-lookup"><span data-stu-id="10d38-182">You can create the site in any language that returns HTTP responses; this topic assumes you'll be hosting the URL in a JSP page.</span></span>

<span data-ttu-id="10d38-183">Na następującej stronie JSP powoduje odpowiedzi TwiML informacją **Hello World!**</span><span class="sxs-lookup"><span data-stu-id="10d38-183">The following JSP page results in a TwiML response that says **Hello World!**</span></span> <span data-ttu-id="10d38-184">w wywołaniu.</span><span class="sxs-lookup"><span data-stu-id="10d38-184">on the call.</span></span>

```xml
    <%@ page contentType="text/xml" %>
    <Response>
        <Say>Hello World!</Say>
    </Response>
```

<span data-ttu-id="10d38-185">Następująca strona JSP powoduje odpowiedzi TwiML mówi część tekstu, ma kilka pauzy i mówi informacje o wersji interfejsu API usługi Twilio i nazwę roli platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="10d38-185">The following JSP page results in a TwiML response that says some text, has several pauses, and says information about the Twilio API version and the Azure role name.</span></span>

```xml
    <%@ page contentType="text/xml" %>
    <Response>
        <Say>Hello from Azure!</Say>
        <Pause></Pause>
        <Say>The Twilio API version is <%= request.getParameter("ApiVersion") %>.</Say>
        <Say>The Azure role name is <%= System.getenv("RoleName") %>.</Say>
        <Pause></Pause>
        <Say>Good bye.</Say>
    </Response>
```

<span data-ttu-id="10d38-186">**ApiVersion** parametr jest dostępny w żądaniach głosu usługi Twilio (nie liczba żądań programu SMS).</span><span class="sxs-lookup"><span data-stu-id="10d38-186">The **ApiVersion** parameter is available in Twilio voice requests (not SMS requests).</span></span> <span data-ttu-id="10d38-187">Aby wyświetlić dostępne parametrów głosowe usługi Twilio i żądań programu SMS, zobacz <https://www.twilio.com/docs/api/twiml/twilio_request> i <https://www.twilio.com/docs/api/twiml/sms/twilio_request>odpowiednio.</span><span class="sxs-lookup"><span data-stu-id="10d38-187">To see the available request parameters for Twilio voice and SMS requests, see <https://www.twilio.com/docs/api/twiml/twilio_request> and <https://www.twilio.com/docs/api/twiml/sms/twilio_request>, respectively.</span></span> <span data-ttu-id="10d38-188">**RoleName** zmiennej środowiskowej jest dostępna jako część wdrożenia usługi Azure.</span><span class="sxs-lookup"><span data-stu-id="10d38-188">The **RoleName** environment variable is available as part of an Azure deployment.</span></span> <span data-ttu-id="10d38-189">(Jeśli chcesz dodać zmienne środowiskowe niestandardowych, tak aby ich może zostać pobrana z **System.getenv**, zobacz sekcję zmienne środowiskowe w [dodatkowych ustawień konfiguracji roli] [ misc_role_config_settings].)</span><span class="sxs-lookup"><span data-stu-id="10d38-189">(If you want to add custom environment variables so they could be picked up from **System.getenv**, see the environment variables section at [Miscellaneous Role Configuration Settings][misc_role_config_settings].)</span></span>

<span data-ttu-id="10d38-190">Po utworzeniu strony JSP zdefiniowano udzielenie odpowiedzi TwiML, użyj adres URL strony JSP adres URL przekazany **Call.creator** metody.</span><span class="sxs-lookup"><span data-stu-id="10d38-190">Once you have your JSP page set up to provide TwiML responses, use the URL of the JSP page as the URL passed into the **Call.creator** method.</span></span> <span data-ttu-id="10d38-191">Na przykład, jeśli masz aplikację sieci Web o nazwie MyTwiML wdrożone do platformy Azure hostowanej usługi i nazwa strony JSP jest mytwiml.jsp, adres URL można przekazać do **Call.creator** jak pokazano poniżej:</span><span class="sxs-lookup"><span data-stu-id="10d38-191">For example, if you have a Web application named MyTwiML deployed to an Azure hosted service, and the name of the JSP page is mytwiml.jsp, the URL can be passed to **Call.creator** as shown in the following:</span></span>

```java
    // Declare To and From numbers and the URL of your JSP page
    PhoneNumber to = new PhoneNumber("NNNNNNNNNN");
    PhoneNumber from = new PhoneNumber("NNNNNNNNNN");
    URI uri = new URI("http://<your_hosted_service>.cloudapp.net/MyTwiML/mytwiml.jsp");

    // Create a Call creator passing From, To and URL values
    // then make the call by executing the create() method
    Call.creator(to, from, uri).create();
```

<span data-ttu-id="10d38-192">Inną opcją w przypadku odpowiadać TwiML odbywa się za pośrednictwem **VoiceResponse** klasy, która jest dostępna w **com.twilio.twiml** pakietu.</span><span class="sxs-lookup"><span data-stu-id="10d38-192">Another option for responding with TwiML is via the **VoiceResponse** class, which is available in the **com.twilio.twiml** package.</span></span>

<span data-ttu-id="10d38-193">Aby uzyskać dodatkowe informacje dotyczące korzystania z usługi Twilio w platformie Azure za pomocą języka Java, zobacz [porady: Tworzenie usługi przy użyciu połączenia telefonicznego Twilio w aplikacji Java na platformie Azure][howto_phonecall_java].</span><span class="sxs-lookup"><span data-stu-id="10d38-193">For additional information about using Twilio in Azure with Java, see [How to Make a Phone Call Using Twilio in a Java Application on Azure][howto_phonecall_java].</span></span>

## <span data-ttu-id="10d38-194"><a id="AdditionalServices"></a>Porady: korzystania z usługi Twilio dodatkowych usług</span><span class="sxs-lookup"><span data-stu-id="10d38-194"><a id="AdditionalServices"></a>How to: Use Additional Twilio Services</span></span>
<span data-ttu-id="10d38-195">Oprócz przykładach pokazano poniżej usługi Twilio oferuje opartych na sieci web interfejsów API, które można wykorzystać dodatkowych funkcji usługi Twilio z aplikacji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="10d38-195">In addition to the examples shown here, Twilio offers web-based APIs that you can use to leverage additional Twilio functionality from your Azure application.</span></span> <span data-ttu-id="10d38-196">Aby uzyskać szczegółowe informacje, zobacz [dokumentacji interfejsu API usługi Twilio][twilio_api_documentation].</span><span class="sxs-lookup"><span data-stu-id="10d38-196">For full details, see the [Twilio API documentation][twilio_api_documentation].</span></span>

## <span data-ttu-id="10d38-197"><a id="NextSteps"></a>Następne kroki</span><span class="sxs-lookup"><span data-stu-id="10d38-197"><a id="NextSteps"></a>Next Steps</span></span>
<span data-ttu-id="10d38-198">Teraz, kiedy znasz już podstawy usługi usługi Twilio, skorzystaj z poniższych linków, aby dowiedzieć się więcej:</span><span class="sxs-lookup"><span data-stu-id="10d38-198">Now that you've learned the basics of the Twilio service, follow these links to learn more:</span></span>

* <span data-ttu-id="10d38-199">[Wytyczne dotyczące zabezpieczeń usługi Twilio][twilio_security_guidelines]</span><span class="sxs-lookup"><span data-stu-id="10d38-199">[Twilio Security Guidelines][twilio_security_guidelines]</span></span>
* <span data-ttu-id="10d38-200">[Porada usługi Twilio i przykładowy kod][twilio_howtos]</span><span class="sxs-lookup"><span data-stu-id="10d38-200">[Twilio HowTo's and Example Code][twilio_howtos]</span></span>
* <span data-ttu-id="10d38-201">[Samouczki usługi Twilio Szybki Start][twilio_quickstarts]</span><span class="sxs-lookup"><span data-stu-id="10d38-201">[Twilio Quickstart Tutorials][twilio_quickstarts]</span></span>
* <span data-ttu-id="10d38-202">[Usługi Twilio w witrynie GitHub][twilio_on_github]</span><span class="sxs-lookup"><span data-stu-id="10d38-202">[Twilio on GitHub][twilio_on_github]</span></span>
* <span data-ttu-id="10d38-203">[Zwróć się do pomocy technicznej usługi Twilio][twilio_support]</span><span class="sxs-lookup"><span data-stu-id="10d38-203">[Talk to Twilio Support][twilio_support]</span></span>

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
