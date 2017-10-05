---
title: "Jak używać usługi Twilio głosowe i programu SMS (PHP) | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak wykonać połączenie telefoniczne i wysłać wiadomość SMS z usługi interfejsu API usługi Twilio na platformie Azure. Przykłady kodu napisane w języku PHP."
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
ms.openlocfilehash: bd50eac7390e8639f77894689388e6926cdb619c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-twilio-for-voice-and-sms-capabilities-in-php"></a><span data-ttu-id="d9497-104">Jak używać usługi Twilio głosowe i możliwości programu SMS w języku PHP</span><span class="sxs-lookup"><span data-stu-id="d9497-104">How to Use Twilio for Voice and SMS Capabilities in PHP</span></span>
<span data-ttu-id="d9497-105">W tym przewodniku przedstawiono sposób wykonywania typowych zadań programowania usługi interfejsu API usługi Twilio na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="d9497-105">This guide demonstrates how to perform common programming tasks with the Twilio API service on Azure.</span></span> <span data-ttu-id="d9497-106">Omówione scenariusze obejmują tworzenie połączeń telefonicznych i wysyłanie wiadomości krótką wiadomość usługi (SMS).</span><span class="sxs-lookup"><span data-stu-id="d9497-106">The scenarios covered include making a phone call and sending a Short Message Service (SMS) message.</span></span> <span data-ttu-id="d9497-107">Aby uzyskać więcej informacji na temat usługi Twilio i komunikacja głosowa programu SMS w aplikacji, zobacz [następne kroki](#NextSteps) sekcji.</span><span class="sxs-lookup"><span data-stu-id="d9497-107">For more information on Twilio and using voice and SMS in your applications, see the [Next Steps](#NextSteps) section.</span></span>

## <span data-ttu-id="d9497-108"><a id="WhatIs"></a>Co to jest usługi Twilio?</span><span class="sxs-lookup"><span data-stu-id="d9497-108"><a id="WhatIs"></a>What is Twilio?</span></span>
<span data-ttu-id="d9497-109">Usługi Twilio jest włączanie przyszłości komunikacji biznesowej, umożliwiają deweloperom osadzać głosowych, VoIP i wiadomości do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d9497-109">Twilio is powering the future of business communications, enabling developers to embed voice, VoIP, and messaging into applications.</span></span> <span data-ttu-id="d9497-110">Zwirtualizuj one wszystkich infrastrukturę potrzebną w środowisku chmury, globalnych ujawnienie go za pośrednictwem platformy komunikacji interfejsu API usługi Twilio.</span><span class="sxs-lookup"><span data-stu-id="d9497-110">They virtualize all infrastructure needed in a cloud-based, global environment, exposing it through the Twilio communications API platform.</span></span> <span data-ttu-id="d9497-111">Aplikacje są proste tworzenie i skalowalności.</span><span class="sxs-lookup"><span data-stu-id="d9497-111">Applications are simple to build and scalable.</span></span> <span data-ttu-id="d9497-112">Kredyty elastyczność Tobie płatności — jako Przejdź ceny i korzystać z niej niezawodności chmury.</span><span class="sxs-lookup"><span data-stu-id="d9497-112">Enjoy flexibility with pay-as-you go pricing, and benefit from cloud reliability.</span></span>

<span data-ttu-id="d9497-113">**Usługi Twilio głosu** umożliwia aplikacjom wykonywanie i odbieranie połączeń telefonicznych.</span><span class="sxs-lookup"><span data-stu-id="d9497-113">**Twilio Voice** allows your applications to make and receive phone calls.</span></span> <span data-ttu-id="d9497-114">**SMS usługi Twilio** umożliwia aplikacji wysyłanie i odbieranie wiadomości tekstowych.</span><span class="sxs-lookup"><span data-stu-id="d9497-114">**Twilio SMS** enables your application to send and receive text messages.</span></span> <span data-ttu-id="d9497-115">**Klient usługi Twilio** służy do nawiązywania połączeń VoIP z dowolnego telefonu, tabletu lub przeglądarki i obsługuje WebRTC.</span><span class="sxs-lookup"><span data-stu-id="d9497-115">**Twilio Client** allows you to make VoIP calls from any phone, tablet, or browser and supports WebRTC.</span></span>

## <span data-ttu-id="d9497-116"><a id="Pricing"></a>Cennik usługi Twilio i oferty specjalne</span><span class="sxs-lookup"><span data-stu-id="d9497-116"><a id="Pricing"></a>Twilio Pricing and Special Offers</span></span>
<span data-ttu-id="d9497-117">Azure klienci otrzymają [oferta specjalna](http://www.twilio.com/azure): bezpłatnych 10 środków usługi Twilio po uaktualnieniu konta usługi Twilio.</span><span class="sxs-lookup"><span data-stu-id="d9497-117">Azure customers receive a [special offer](http://www.twilio.com/azure): complimentary $10 of Twilio Credit when you upgrade your Twilio Account.</span></span> <span data-ttu-id="d9497-118">Środki tej usługi Twilio można zastosować do bez użycia usługi Twilio (równoznaczne z wysyłaniem wiadomości SMS maksymalnie 1000 lub odbieranie maksymalnie 1000 przychodzących minut głosu w zależności od lokalizacji telefonu przeznaczenia numer i komunikatu lub wywołania kredyt $10).</span><span class="sxs-lookup"><span data-stu-id="d9497-118">This Twilio Credit can be applied to any Twilio usage ($10 credit equivalent to sending as many as 1,000 SMS messages or receiving up to 1000 inbound Voice minutes, depending on the location of your phone number and message or call destination).</span></span> <span data-ttu-id="d9497-119">Realizowanie tego środki usługi Twilio i rozpocząć pracę w: [http://ahoy.twilio.com/azure](http://ahoy.twilio.com/azure).</span><span class="sxs-lookup"><span data-stu-id="d9497-119">Redeem this Twilio credit and get started at: [http://ahoy.twilio.com/azure](http://ahoy.twilio.com/azure).</span></span>

<span data-ttu-id="d9497-120">Usługi Twilio jest z usługą.</span><span class="sxs-lookup"><span data-stu-id="d9497-120">Twilio is a pay-as-you-go service.</span></span> <span data-ttu-id="d9497-121">Nie żadne opłaty konfiguracji i w dowolnej chwili możesz zamknąć konto.</span><span class="sxs-lookup"><span data-stu-id="d9497-121">There are no set-up fees and you can close your account at any time.</span></span> <span data-ttu-id="d9497-122">Można znaleźć więcej szczegółów na [cennik usługi Twilio][twilio_pricing].</span><span class="sxs-lookup"><span data-stu-id="d9497-122">You can find more details at [Twilio Pricing][twilio_pricing].</span></span>

## <span data-ttu-id="d9497-123"><a id="Concepts"></a>Pojęcia</span><span class="sxs-lookup"><span data-stu-id="d9497-123"><a id="Concepts"></a>Concepts</span></span>
<span data-ttu-id="d9497-124">Interfejs API usługi Twilio jest interfejs API RESTful, która zapewnia funkcje programu SMS i komunikacja głosowa aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d9497-124">The Twilio API is a RESTful API that provides voice and SMS functionality for applications.</span></span> <span data-ttu-id="d9497-125">Klient biblioteki są dostępne w wielu językach; Aby uzyskać listę, zobacz [bibliotek interfejsu API usługi Twilio][twilio_libraries].</span><span class="sxs-lookup"><span data-stu-id="d9497-125">Client libraries are available in multiple languages; for a list, see [Twilio API Libraries][twilio_libraries].</span></span>

<span data-ttu-id="d9497-126">Kluczowe aspekty interfejsu API usługi Twilio są zleceń usługi Twilio i usługi Twilio Markup Language (TwiML).</span><span class="sxs-lookup"><span data-stu-id="d9497-126">Key aspects of the Twilio API are Twilio verbs and Twilio Markup Language (TwiML).</span></span>

### <span data-ttu-id="d9497-127"><a id="Verbs"></a>Usługi Twilio zlecenia</span><span class="sxs-lookup"><span data-stu-id="d9497-127"><a id="Verbs"></a>Twilio Verbs</span></span>
<span data-ttu-id="d9497-128">Interfejs API korzysta z usługi Twilio zleceń; na przykład  **&lt;powiedzieć&gt;**  zlecenie powoduje, że usługi Twilio komputerowi dostarczenia komunikatu w wywołaniu.</span><span class="sxs-lookup"><span data-stu-id="d9497-128">The API makes use of Twilio verbs; for example, the **&lt;Say&gt;** verb instructs Twilio to audibly deliver a message on a call.</span></span>

<span data-ttu-id="d9497-129">Poniżej znajduje się lista zleceń usługi Twilio.</span><span class="sxs-lookup"><span data-stu-id="d9497-129">The following is a list of Twilio verbs.</span></span> <span data-ttu-id="d9497-130">Dowiedz się więcej o innych poleceń i możliwości za pośrednictwem [dokumentacji usługi Twilio Markup Language](http://www.twilio.com/docs/api/twiml).</span><span class="sxs-lookup"><span data-stu-id="d9497-130">Learn about the other verbs and capabilities via [Twilio Markup Language documentation](http://www.twilio.com/docs/api/twiml).</span></span>

* <span data-ttu-id="d9497-131">**&lt;Wybierania&gt;**: łączy wywołującego innego numeru telefonu.</span><span class="sxs-lookup"><span data-stu-id="d9497-131">**&lt;Dial&gt;**: Connects the caller to another phone.</span></span>
* <span data-ttu-id="d9497-132">**&lt;Zbierz&gt;**: zbiera cyfry wprowadzone na klawiaturze telefonu.</span><span class="sxs-lookup"><span data-stu-id="d9497-132">**&lt;Gather&gt;**: Collects numeric digits entered on the telephone keypad.</span></span>
* <span data-ttu-id="d9497-133">**&lt;Rozłączanie&gt;**: kończy wywołanie.</span><span class="sxs-lookup"><span data-stu-id="d9497-133">**&lt;Hangup&gt;**: Ends a call.</span></span>
* <span data-ttu-id="d9497-134">**&lt;Odtwórz&gt;**: odtwarzania pliku audio.</span><span class="sxs-lookup"><span data-stu-id="d9497-134">**&lt;Play&gt;**: Plays an audio file.</span></span>
* <span data-ttu-id="d9497-135">**&lt;Wstrzymaj&gt;**: dyskretnie czeka na określoną liczbę sekund.</span><span class="sxs-lookup"><span data-stu-id="d9497-135">**&lt;Pause&gt;**: Waits silently for a specified number of seconds.</span></span>
* <span data-ttu-id="d9497-136">**&lt;Rekord&gt;**: rejestruje wywołującego głosu i zwraca adres URL pliku zawierającego nagrywania.</span><span class="sxs-lookup"><span data-stu-id="d9497-136">**&lt;Record&gt;**: Records the caller's voice and returns a URL of a file that contains the recording.</span></span>
* <span data-ttu-id="d9497-137">**&lt;Przekieruj&gt;**: przekazuje kontrolę nad wywołania lub wiadomości SMS do TwiML na inny adres URL.</span><span class="sxs-lookup"><span data-stu-id="d9497-137">**&lt;Redirect&gt;**: Transfers control of a call or SMS to the TwiML at a different URL.</span></span>
* <span data-ttu-id="d9497-138">**&lt;Odrzuć&gt;**: odrzucanie połączenia przychodzącego na numer usługi Twilio bez rozliczeń można</span><span class="sxs-lookup"><span data-stu-id="d9497-138">**&lt;Reject&gt;**: Rejects an incoming call to your Twilio number without billing you</span></span>
* <span data-ttu-id="d9497-139">**&lt;Powiedz&gt;**: Konwertuje tekst na mowę, które zostało utworzone w wywołaniu.</span><span class="sxs-lookup"><span data-stu-id="d9497-139">**&lt;Say&gt;**: Converts text to speech that is made on a call.</span></span>
* <span data-ttu-id="d9497-140">**&lt;SMS&gt;**: wysyła wiadomość SMS.</span><span class="sxs-lookup"><span data-stu-id="d9497-140">**&lt;Sms&gt;**: Sends an SMS message.</span></span>

### <span data-ttu-id="d9497-141"><a id="TwiML"></a>TwiML</span><span class="sxs-lookup"><span data-stu-id="d9497-141"><a id="TwiML"></a>TwiML</span></span>
<span data-ttu-id="d9497-142">TwiML to zestaw instrukcji oparte na języku XML, oparte na zlecenia usługi Twilio, które informują usługi Twilio sposobu przetwarzania połączenia lub wiadomości SMS.</span><span class="sxs-lookup"><span data-stu-id="d9497-142">TwiML is a set of XML-based instructions based on the Twilio verbs that inform Twilio of how to process a call or SMS.</span></span>

<span data-ttu-id="d9497-143">Na przykład następujące TwiML czy Konwertuj tekst **Hello World** do rozpoznawania mowy.</span><span class="sxs-lookup"><span data-stu-id="d9497-143">As an example, the following TwiML would convert the text **Hello World** to speech.</span></span>

    <?xml version="1.0" encoding="UTF-8" ?>
    <Response>
       <Say>Hello World</Say>
    </Response>

<span data-ttu-id="d9497-144">Gdy aplikacja wywołuje interfejs API usługi Twilio, jeden z parametrów interfejsu API jest adres URL, który zwraca odpowiedź TwiML.</span><span class="sxs-lookup"><span data-stu-id="d9497-144">When your application calls the Twilio API, one of the API parameters is the URL that returns the TwiML response.</span></span> <span data-ttu-id="d9497-145">Do celów programistycznych wprowadzone do usługi Twilio adresy URL służy do nadania odpowiedzi TwiML używane przez aplikacje.</span><span class="sxs-lookup"><span data-stu-id="d9497-145">For development purposes, you can use Twilio-provided URLs to provide the TwiML responses used by your applications.</span></span> <span data-ttu-id="d9497-146">Może również udostępniać swoje własne adresy URL do tworzenia odpowiedzi TwiML i inną opcją jest użycie **TwiMLResponse** obiektu.</span><span class="sxs-lookup"><span data-stu-id="d9497-146">You could also host your own URLs to produce the TwiML responses, and another option is to use the **TwiMLResponse** object.</span></span>

<span data-ttu-id="d9497-147">Aby uzyskać więcej informacji na temat usługi Twilio zlecenia i ich atrybuty oraz TwiML, zobacz [TwiML][twiml].</span><span class="sxs-lookup"><span data-stu-id="d9497-147">For more information about Twilio verbs, their attributes, and TwiML, see [TwiML][twiml].</span></span> <span data-ttu-id="d9497-148">Aby uzyskać dodatkowe informacje na temat interfejsu API usługi Twilio, zobacz [interfejsu API usługi Twilio][twilio_api].</span><span class="sxs-lookup"><span data-stu-id="d9497-148">For additional information about the Twilio API, see [Twilio API][twilio_api].</span></span>

## <span data-ttu-id="d9497-149"><a id="CreateAccount"></a>Tworzenie konta usługi Twilio</span><span class="sxs-lookup"><span data-stu-id="d9497-149"><a id="CreateAccount"></a>Create a Twilio Account</span></span>
<span data-ttu-id="d9497-150">Po przygotowaniu można uzyskać konta usługi Twilio, zarejestruj się w [spróbuj usługi Twilio][try_twilio].</span><span class="sxs-lookup"><span data-stu-id="d9497-150">When you're ready to get a Twilio account, sign up at [Try Twilio][try_twilio].</span></span> <span data-ttu-id="d9497-151">Można rozpoczynać bezpłatne konto, a następnie Uaktualnij swoje konto później.</span><span class="sxs-lookup"><span data-stu-id="d9497-151">You can start with a free account, and upgrade your account later.</span></span>

<span data-ttu-id="d9497-152">Po utworzeniu konta dla konta usługi Twilio, otrzymasz Identyfikatora konta oraz tokenu uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="d9497-152">When you sign up for a Twilio account, you'll receive an account ID and an authentication token.</span></span> <span data-ttu-id="d9497-153">Zarówno będą potrzebne w celu wykonywania wywołań interfejsu API usługi Twilio.</span><span class="sxs-lookup"><span data-stu-id="d9497-153">Both will be needed to make Twilio API calls.</span></span> <span data-ttu-id="d9497-154">Aby uniemożliwić nieautoryzowany dostęp do Twojego konta, bezpieczeństwo Twojego tokenu uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="d9497-154">To prevent unauthorized access to your account, keep your authentication token secure.</span></span> <span data-ttu-id="d9497-155">Twój identyfikator konta i uwierzytelniania tokenu jest wyświetlana w [strony konta usługi Twilio][twilio_account], w polach etykietą **identyfikator SID konta** i **TOKEN uwierzytelniania**odpowiednio.</span><span class="sxs-lookup"><span data-stu-id="d9497-155">Your account ID and authentication token are viewable at the [Twilio account page][twilio_account], in the fields labeled **ACCOUNT SID** and **AUTH TOKEN**, respectively.</span></span>

## <span data-ttu-id="d9497-156"><a id="create_app"></a>Tworzenie aplikacji PHP</span><span class="sxs-lookup"><span data-stu-id="d9497-156"><a id="create_app"></a>Create a PHP Application</span></span>
<span data-ttu-id="d9497-157">Nie różni się od innych aplikacji PHP, który korzysta z usługi Twilio usługi się aplikacji PHP, która używa usługi usługi Twilio i działa na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="d9497-157">A PHP application that uses the Twilio service and is running in Azure is no different than any other PHP application that uses the Twilio service.</span></span> <span data-ttu-id="d9497-158">Usługi Twilio usług są opartego na interfejsie REST i może zostać wywołana z PHP na kilka sposobów, w tym artykule dotyczą sposobu korzystania z usługi Twilio usług w programie [biblioteki usługi Twilio dla programów PHP i z usługi GitHub][twilio_php].</span><span class="sxs-lookup"><span data-stu-id="d9497-158">While Twilio services are REST-based and can be called from PHP in several ways, this article will focus on how to use Twilio services with [Twilio library for PHP from GitHub][twilio_php].</span></span> <span data-ttu-id="d9497-159">Aby uzyskać więcej informacji dotyczących korzystania z biblioteki usługi Twilio dla programu PHP, zobacz [http://readthedocs.org/docs/twilio-php/en/latest/index.html][twilio_lib_docs].</span><span class="sxs-lookup"><span data-stu-id="d9497-159">For more information about using the Twilio library for PHP, see [http://readthedocs.org/docs/twilio-php/en/latest/index.html][twilio_lib_docs].</span></span>

<span data-ttu-id="d9497-160">Szczegółowe instrukcje dotyczące tworzenia i wdrażania aplikacji usługi Twilio/PHP na platformie Azure są dostępne pod adresem [porady: Tworzenie usługi przy użyciu połączenia telefonicznego Twilio w aplikacji PHP na platformie Azure][howto_phonecall_php].</span><span class="sxs-lookup"><span data-stu-id="d9497-160">Detailed instructions for building and deploying a Twilio/PHP application to Azure are available at [How to Make a Phone Call Using Twilio in a PHP Application on Azure][howto_phonecall_php].</span></span>

## <span data-ttu-id="d9497-161"><a id="configure_app"></a>Konfigurowanie aplikacji przy użyciu bibliotek usługi Twilio</span><span class="sxs-lookup"><span data-stu-id="d9497-161"><a id="configure_app"></a>Configure Your Application to Use Twilio Libraries</span></span>
<span data-ttu-id="d9497-162">Można skonfigurować aplikację do korzystania z biblioteki usługi Twilio dla PHP na dwa sposoby:</span><span class="sxs-lookup"><span data-stu-id="d9497-162">You can configure your application to use the Twilio library for PHP in two ways:</span></span>

1. <span data-ttu-id="d9497-163">Pobierz biblioteki usługi Twilio dla PHP z serwisu GitHub ([https://github.com/twilio/twilio-php][twilio_php]) i Dodaj **usług** katalogu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d9497-163">Download the Twilio library for PHP from GitHub ([https://github.com/twilio/twilio-php][twilio_php]) and add the **Services** directory to your application.</span></span>
   
    <span data-ttu-id="d9497-164">— Lub —</span><span class="sxs-lookup"><span data-stu-id="d9497-164">-OR-</span></span>
2. <span data-ttu-id="d9497-165">Zainstaluj biblioteki usługi Twilio dla programu PHP w pakiecie GRUSZKOWA.</span><span class="sxs-lookup"><span data-stu-id="d9497-165">Install the Twilio library for PHP as a PEAR package.</span></span> <span data-ttu-id="d9497-166">Można go zainstalować za pomocą następujących poleceń:</span><span class="sxs-lookup"><span data-stu-id="d9497-166">It can be installed with the following commands:</span></span>
   
        $ pear channel-discover twilio.github.com/pear
        $ pear install twilio/Services_Twilio

<span data-ttu-id="d9497-167">Po zainstalowaniu usługi Twilio biblioteki dla programu PHP, można dodać **require_once** instrukcji w górnej części plików PHP, aby odwołać biblioteki:</span><span class="sxs-lookup"><span data-stu-id="d9497-167">Once you have installed the Twilio library for PHP, you can then add a **require_once** statement at the top of your PHP files to reference the library:</span></span>

        require_once 'Services/Twilio.php';

<span data-ttu-id="d9497-168">Aby uzyskać więcej informacji, zobacz [https://github.com/twilio/twilio-php/blob/master/README.md][twilio_github_readme].</span><span class="sxs-lookup"><span data-stu-id="d9497-168">For more information, see [https://github.com/twilio/twilio-php/blob/master/README.md][twilio_github_readme].</span></span>

## <span data-ttu-id="d9497-169"><a id="howto_make_call"></a>Porady: wykonywanie połączenia wychodzące</span><span class="sxs-lookup"><span data-stu-id="d9497-169"><a id="howto_make_call"></a>How to: Make an outgoing call</span></span>
<span data-ttu-id="d9497-170">Poniżej pokazano, jak wykonać wychodzące wywołanie przy użyciu **Services_Twilio** klasy.</span><span class="sxs-lookup"><span data-stu-id="d9497-170">The following shows how to make an outgoing call using the **Services_Twilio** class.</span></span> <span data-ttu-id="d9497-171">Ten kod zawiera również lokacja dostarczonych do usługi Twilio do zwracania odpowiedzi usługi Twilio Markup Language (TwiML).</span><span class="sxs-lookup"><span data-stu-id="d9497-171">This code also uses a Twilio-provided site to return the Twilio Markup Language (TwiML) response.</span></span> <span data-ttu-id="d9497-172">Podstaw wartości **z** i **do** numerów telefonów i upewnij się, że sprawdzisz **z** numer telefonu dla konta usługi Twilio przed uruchomieniem kodu.</span><span class="sxs-lookup"><span data-stu-id="d9497-172">Substitute your values for the **From** and **To** phone numbers, and ensure that you verify the **From** phone number for your Twilio account prior to running the code.</span></span>

    // Include the Twilio PHP library.
    require_once 'Services/Twilio.php';

    // Library version.
    $version = "2010-04-01";

    // Set your account ID and authentication token.
    $sid = "your_twilio_account_sid";
    $token = "your_twilio_authentication_token";

    // The number of the phone initiating the the call.
    $from_number = "NNNNNNNNNNN";

    // The number of the phone receiving call.
    $to_number = "NNNNNNNNNNN";

    // Use the Twilio-provided site for the TwiML response.
    $url = "http://twimlets.com/message";

    // The phone message text.
    $message = "Hello world.";

    // Create the call client.
    $client = new Services_Twilio($sid, $token, $version);

    //Make the call.
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

<span data-ttu-id="d9497-173">Jak wspomniano, ten kod używa lokacja dostarczonych do usługi Twilio do zwracania odpowiedzi TwiML.</span><span class="sxs-lookup"><span data-stu-id="d9497-173">As mentioned, this code uses a Twilio-provided site to return the TwiML response.</span></span> <span data-ttu-id="d9497-174">Własnej witryny można zamiast tego użyć, aby zapewnić odpowiedzi TwiML; Aby uzyskać więcej informacji, zobacz [jak zapewnić TwiML odpowiedzi z Twoje własne witryny sieci Web](#howto_provide_twiml_responses).</span><span class="sxs-lookup"><span data-stu-id="d9497-174">You could instead use your own site to provide the TwiML response; for more information, see [How to Provide TwiML Responses from Your Own Web Site](#howto_provide_twiml_responses).</span></span>

* <span data-ttu-id="d9497-175">**Uwaga**: Aby rozwiązać błędy sprawdzania poprawności certyfikatów SSL, zobacz [http://readthedocs.org/docs/twilio-php/en/latest/usage/rest.html][ssl_validation]</span><span class="sxs-lookup"><span data-stu-id="d9497-175">**Note**: To troubleshoot SSL certificate validation errors, see [http://readthedocs.org/docs/twilio-php/en/latest/usage/rest.html][ssl_validation]</span></span> 

## <span data-ttu-id="d9497-176"><a id="howto_send_sms"></a>Porady: Wyślij wiadomość SMS</span><span class="sxs-lookup"><span data-stu-id="d9497-176"><a id="howto_send_sms"></a>How to: Send an SMS message</span></span>
<span data-ttu-id="d9497-177">Poniżej pokazano, jak wysyłać wiadomość SMS przy użyciu **Services_Twilio** klasy.</span><span class="sxs-lookup"><span data-stu-id="d9497-177">The following shows how to send an SMS message using the **Services_Twilio** class.</span></span> <span data-ttu-id="d9497-178">**z** numer jest udostępniany przez usługi Twilio dla konta wersji próbnej można wysłać wiadomości SMS.</span><span class="sxs-lookup"><span data-stu-id="d9497-178">The **From** number is provided by Twilio for trial accounts to send SMS messages.</span></span> <span data-ttu-id="d9497-179">**Do** numer muszą być weryfikowane dla konta usługi Twilio przed uruchomieniem kodu.</span><span class="sxs-lookup"><span data-stu-id="d9497-179">The **To** number must be verified for your Twilio account prior to running the code.</span></span>

    // Include the Twilio PHP library.
    require_once 'Services/Twilio.php';

    // Library version.
    $version = "2010-04-01";

    // Set your account ID and authentication token.
    $sid = "your_twilio_account_sid";
    $token = "your_twilio_authentication_token";


    $from_number = "NNNNNNNNNNN"; // With trial account, texts can only be sent from your Twilio number.
    $to_number = "NNNNNNNNNNN";
    $message = "Hello world.";

    // Create the call client.
    $client = new Services_Twilio($sid, $token, $version);

    // Send the SMS message.
    try
    {
        $client->$client->account->messages->sendMessage($from_number, $to_number, $message);
    }
    catch (Exception $e) 
    {
        echo 'Error: ' . $e->getMessage();
    }

## <span data-ttu-id="d9497-180"><a id="howto_provide_twiml_responses"></a>Porady: Podaj TwiML odpowiedzi z własnej witryny sieci Web</span><span class="sxs-lookup"><span data-stu-id="d9497-180"><a id="howto_provide_twiml_responses"></a>How to: Provide TwiML Responses from your own Website</span></span>
<span data-ttu-id="d9497-181">Gdy aplikacja jest inicjowany przez wywołanie interfejsu API usługi Twilio, usługi Twilio wysyła żądanie do adresu URL, który powinien zwrócić odpowiedzi TwiML.</span><span class="sxs-lookup"><span data-stu-id="d9497-181">When your application initiates a call to the Twilio API, Twilio will send your request to a URL that is expected to return a TwiML response.</span></span> <span data-ttu-id="d9497-182">W powyższym przykładzie korzysta z adresu URL dostarczony do usługi Twilio [http://twimlets.com/message][twimlet_message_url].</span><span class="sxs-lookup"><span data-stu-id="d9497-182">The example above uses the Twilio-provided URL [http://twimlets.com/message][twimlet_message_url].</span></span> <span data-ttu-id="d9497-183">(Podczas TwiML jest przeznaczony do użytku przez usługi Twilio, można wyświetlić it w przeglądarce.</span><span class="sxs-lookup"><span data-stu-id="d9497-183">(While TwiML is designed for use by Twilio, you can view the it in your browser.</span></span> <span data-ttu-id="d9497-184">For example, kliknij przycisk [http://twimlets.com/message] [ twimlet_message_url] wyświetlić pustą `<Response>` element; inny przykład kliknij [http://twimlets.com/message?Message%5B0%5D=Hello%20World] [ twimlet_message_url_hello_world] wyświetlić `<Response>` element, który zawiera `<Say>` elementu.)</span><span class="sxs-lookup"><span data-stu-id="d9497-184">For example, click [http://twimlets.com/message][twimlet_message_url] to see an empty `<Response>` element; as another example, click [http://twimlets.com/message?Message%5B0%5D=Hello%20World][twimlet_message_url_hello_world] to see a `<Response>` element that contains a `<Say>` element.)</span></span>

<span data-ttu-id="d9497-185">Zamiast polegania na adres URL dostarczony do usługi Twilio, można utworzyć własne lokacji, która zwraca odpowiedzi HTTP.</span><span class="sxs-lookup"><span data-stu-id="d9497-185">Instead of relying on the Twilio-provided URL, you can create your own site that returns HTTP responses.</span></span> <span data-ttu-id="d9497-186">Można utworzyć witryny w dowolnym języku, który zwraca odpowiedzi XML; w tym temacie założono, że należy używać PHP do utworzenia TwiML.</span><span class="sxs-lookup"><span data-stu-id="d9497-186">You can create the site in any language that returns XML responses; this topic assumes you'll be using PHP to create the TwiML.</span></span>

<span data-ttu-id="d9497-187">Na następującej stronie PHP powoduje odpowiedzi TwiML informacją **Hello World** przy wywołaniu.</span><span class="sxs-lookup"><span data-stu-id="d9497-187">The following PHP page results in a TwiML response that says **Hello World** on the call.</span></span>

    <?php    
        header("content-type: text/xml");    
        echo "<?xml version=\"1.0\" encoding=\"UTF-8\"?>\n";
    ?>
    <Response>    
        <Say>Hello world.</Say>
    </Response>

<span data-ttu-id="d9497-188">Jak widać w powyższym przykładzie, odpowiedź TwiML jest po prostu dokumentu XML.</span><span class="sxs-lookup"><span data-stu-id="d9497-188">As you can see from the example above, the TwiML response is simply an XML document.</span></span> <span data-ttu-id="d9497-189">Biblioteka usługi Twilio dla programów PHP i zawiera klasy, które generuje TwiML dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="d9497-189">The Twilio library for PHP contains classes that will generate TwiML for you.</span></span> <span data-ttu-id="d9497-190">Poniższy przykład tworzy równoważne odpowiedzi, jak pokazano powyżej, ale używa **usług\_usługi Twilio\_Twiml** klasy w bibliotece usługi Twilio dla programu PHP:</span><span class="sxs-lookup"><span data-stu-id="d9497-190">The example below produces the equivalent response as shown above, but uses the **Services\_Twilio\_Twiml** class in the Twilio library for PHP:</span></span>

    require_once('Services/Twilio.php');

    $response = new Services_Twilio_Twiml();
    $response->say("Hello world.");
    print $response;

<span data-ttu-id="d9497-191">Aby uzyskać więcej informacji o TwiML, zobacz [https://www.twilio.com/docs/api/twiml][twiml_reference].</span><span class="sxs-lookup"><span data-stu-id="d9497-191">For more information about TwiML, see [https://www.twilio.com/docs/api/twiml][twiml_reference].</span></span> 

<span data-ttu-id="d9497-192">Po utworzeniu strony PHP zdefiniowano udzielenie odpowiedzi TwiML, użyj adres URL strony PHP adres URL przekazany `Services_Twilio->account->calls->create` metody.</span><span class="sxs-lookup"><span data-stu-id="d9497-192">Once you have your PHP page set up to provide TwiML responses, use the URL of the PHP page as the URL passed into the  `Services_Twilio->account->calls->create`  method.</span></span> <span data-ttu-id="d9497-193">Na przykład, jeśli masz aplikację sieci Web o nazwie **MyTwiML** wdrożone usługi hostowanej platformy Azure i nazwa strony PHP jest **mytwiml.php**, adres URL można przekazać do **Services_Twilio -> wywołania -> konta -> Utwórz** jak pokazano w poniższym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="d9497-193">For example, if you have a Web application named **MyTwiML** deployed to an Azure hosted service, and the name of the PHP page is **mytwiml.php**, the URL can be passed to  **Services_Twilio->account->calls->create**  as shown in the following example:</span></span>

    require_once 'Services/Twilio.php';

    $sid = "your_twilio_account_sid";
    $token = "your_twilio_authentication_token";
    $from_number = "NNNNNNNNNNN";
    $to_number = "NNNNNNNNNNN";
    $url = "http://<your_hosted_service>.cloudapp.net/MyTwiML/mytwiml.php";

    // The phone message text.
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

<span data-ttu-id="d9497-194">Aby uzyskać dodatkowe informacje dotyczące korzystania z usługi Twilio na platformie Azure za pomocą języka PHP, zobacz [porady: Tworzenie usługi przy użyciu połączenia telefonicznego Twilio w aplikacji PHP na platformie Azure][howto_phonecall_php].</span><span class="sxs-lookup"><span data-stu-id="d9497-194">For additional information about using Twilio in Azure with PHP, see [How to Make a Phone Call Using Twilio in a PHP Application on Azure][howto_phonecall_php].</span></span>

## <span data-ttu-id="d9497-195"><a id="AdditionalServices"></a>Porady: korzystania z usługi Twilio dodatkowych usług</span><span class="sxs-lookup"><span data-stu-id="d9497-195"><a id="AdditionalServices"></a>How to: Use Additional Twilio Services</span></span>
<span data-ttu-id="d9497-196">Oprócz przykładach pokazano poniżej usługi Twilio oferuje opartych na sieci web interfejsów API, które można wykorzystać dodatkowych funkcji usługi Twilio z aplikacji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="d9497-196">In addition to the examples shown here, Twilio offers web-based APIs that you can use to leverage additional Twilio functionality from your Azure application.</span></span> <span data-ttu-id="d9497-197">Aby uzyskać szczegółowe informacje, zobacz [dokumentacji interfejsu API usługi Twilio][twilio_api_documentation].</span><span class="sxs-lookup"><span data-stu-id="d9497-197">For full details, see the [Twilio API documentation][twilio_api_documentation].</span></span>

## <span data-ttu-id="d9497-198"><a id="NextSteps"></a>Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d9497-198"><a id="NextSteps"></a>Next Steps</span></span>
<span data-ttu-id="d9497-199">Teraz, kiedy znasz już podstawy usługi usługi Twilio, skorzystaj z poniższych linków, aby dowiedzieć się więcej:</span><span class="sxs-lookup"><span data-stu-id="d9497-199">Now that you've learned the basics of the Twilio service, follow these links to learn more:</span></span>

* <span data-ttu-id="d9497-200">[Wytyczne dotyczące zabezpieczeń usługi Twilio][twilio_security_guidelines]</span><span class="sxs-lookup"><span data-stu-id="d9497-200">[Twilio Security Guidelines][twilio_security_guidelines]</span></span>
* <span data-ttu-id="d9497-201">[Porada usługi Twilio i przykładowy kod][twilio_howtos]</span><span class="sxs-lookup"><span data-stu-id="d9497-201">[Twilio HowTo's and Example Code][twilio_howtos]</span></span>
* <span data-ttu-id="d9497-202">[Samouczki usługi Twilio Szybki Start][twilio_quickstarts]</span><span class="sxs-lookup"><span data-stu-id="d9497-202">[Twilio Quickstart Tutorials][twilio_quickstarts]</span></span> 
* <span data-ttu-id="d9497-203">[Usługi Twilio w witrynie GitHub][twilio_on_github]</span><span class="sxs-lookup"><span data-stu-id="d9497-203">[Twilio on GitHub][twilio_on_github]</span></span>
* <span data-ttu-id="d9497-204">[Zwróć się do pomocy technicznej usługi Twilio][twilio_support]</span><span class="sxs-lookup"><span data-stu-id="d9497-204">[Talk to Twilio Support][twilio_support]</span></span>

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
