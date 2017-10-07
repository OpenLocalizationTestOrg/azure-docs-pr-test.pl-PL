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
# <a name="how-toouse-twilio-for-voice-and-sms-capabilities-in-php"></a><span data-ttu-id="35d4e-104">Jak tooUse usługi Twilio głosowe i możliwości programu SMS w języku PHP</span><span class="sxs-lookup"><span data-stu-id="35d4e-104">How tooUse Twilio for Voice and SMS Capabilities in PHP</span></span>
<span data-ttu-id="35d4e-105">W tym przewodniku pokazano, jak tooperform typowych zadań programowania hello interfejsu API usługi Twilio usługi na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="35d4e-105">This guide demonstrates how tooperform common programming tasks with hello Twilio API service on Azure.</span></span> <span data-ttu-id="35d4e-106">omówione scenariusze Hello obejmują tworzenie połączeń telefonicznych i wysyłanie wiadomości krótką wiadomość usługi (SMS).</span><span class="sxs-lookup"><span data-stu-id="35d4e-106">hello scenarios covered include making a phone call and sending a Short Message Service (SMS) message.</span></span> <span data-ttu-id="35d4e-107">Aby uzyskać więcej informacji na temat usługi Twilio i komunikacja głosowa programu SMS w aplikacji, zobacz hello [następne kroki](#NextSteps) sekcji.</span><span class="sxs-lookup"><span data-stu-id="35d4e-107">For more information on Twilio and using voice and SMS in your applications, see hello [Next Steps](#NextSteps) section.</span></span>

## <span data-ttu-id="35d4e-108"><a id="WhatIs"></a>Co to jest usługi Twilio?</span><span class="sxs-lookup"><span data-stu-id="35d4e-108"><a id="WhatIs"></a>What is Twilio?</span></span>
<span data-ttu-id="35d4e-109">Usługi Twilio jest włączanie hello przyszłych komunikacji biznesowej, włączanie deweloperzy tooembed głosu VoIP i wiadomości do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="35d4e-109">Twilio is powering hello future of business communications, enabling developers tooembed voice, VoIP, and messaging into applications.</span></span> <span data-ttu-id="35d4e-110">Zwirtualizuj one wszystkich infrastrukturę potrzebną w środowisku chmury, globalnych ujawnienie go za pośrednictwem platformy hello API komunikacji usługi Twilio.</span><span class="sxs-lookup"><span data-stu-id="35d4e-110">They virtualize all infrastructure needed in a cloud-based, global environment, exposing it through hello Twilio communications API platform.</span></span> <span data-ttu-id="35d4e-111">Aplikacje są proste toobuild i skalowalność.</span><span class="sxs-lookup"><span data-stu-id="35d4e-111">Applications are simple toobuild and scalable.</span></span> <span data-ttu-id="35d4e-112">Kredyty elastyczność Tobie płatności — jako Przejdź ceny i korzystać z niej niezawodności chmury.</span><span class="sxs-lookup"><span data-stu-id="35d4e-112">Enjoy flexibility with pay-as-you go pricing, and benefit from cloud reliability.</span></span>

<span data-ttu-id="35d4e-113">**Usługi Twilio głosu** umożliwia toomake Twojej aplikacji i odbieranie połączeń telefonicznych.</span><span class="sxs-lookup"><span data-stu-id="35d4e-113">**Twilio Voice** allows your applications toomake and receive phone calls.</span></span> <span data-ttu-id="35d4e-114">**SMS usługi Twilio** umożliwia toosend Twojej aplikacji i odbieranie wiadomości tekstowych.</span><span class="sxs-lookup"><span data-stu-id="35d4e-114">**Twilio SMS** enables your application toosend and receive text messages.</span></span> <span data-ttu-id="35d4e-115">**Klient usługi Twilio** pozwala toomake VoIP wywołania z dowolnego telefonu, tabletu lub przeglądarki i obsługuje WebRTC.</span><span class="sxs-lookup"><span data-stu-id="35d4e-115">**Twilio Client** allows you toomake VoIP calls from any phone, tablet, or browser and supports WebRTC.</span></span>

## <span data-ttu-id="35d4e-116"><a id="Pricing"></a>Cennik usługi Twilio i oferty specjalne</span><span class="sxs-lookup"><span data-stu-id="35d4e-116"><a id="Pricing"></a>Twilio Pricing and Special Offers</span></span>
<span data-ttu-id="35d4e-117">Azure klienci otrzymają [oferta specjalna](http://www.twilio.com/azure): bezpłatnych 10 środków usługi Twilio po uaktualnieniu konta usługi Twilio.</span><span class="sxs-lookup"><span data-stu-id="35d4e-117">Azure customers receive a [special offer](http://www.twilio.com/azure): complimentary $10 of Twilio Credit when you upgrade your Twilio Account.</span></span> <span data-ttu-id="35d4e-118">Środki tej usługi Twilio może być zastosowane tooany użycia usługi Twilio (10 środki równoważne toosending maksymalnie 1000 wiadomości SMS lub odbieranie się too1000 ruchu przychodzącego głosu minut w zależności od lokalizacji hello przeznaczenia numer i komunikatu lub wywołania telefonu).</span><span class="sxs-lookup"><span data-stu-id="35d4e-118">This Twilio Credit can be applied tooany Twilio usage ($10 credit equivalent toosending as many as 1,000 SMS messages or receiving up too1000 inbound Voice minutes, depending on hello location of your phone number and message or call destination).</span></span> <span data-ttu-id="35d4e-119">Realizowanie tego środki usługi Twilio i rozpocząć pracę w: [http://ahoy.twilio.com/azure](http://ahoy.twilio.com/azure).</span><span class="sxs-lookup"><span data-stu-id="35d4e-119">Redeem this Twilio credit and get started at: [http://ahoy.twilio.com/azure](http://ahoy.twilio.com/azure).</span></span>

<span data-ttu-id="35d4e-120">Usługi Twilio jest z usługą.</span><span class="sxs-lookup"><span data-stu-id="35d4e-120">Twilio is a pay-as-you-go service.</span></span> <span data-ttu-id="35d4e-121">Nie żadne opłaty konfiguracji i w dowolnej chwili możesz zamknąć konto.</span><span class="sxs-lookup"><span data-stu-id="35d4e-121">There are no set-up fees and you can close your account at any time.</span></span> <span data-ttu-id="35d4e-122">Można znaleźć więcej szczegółów na [cennik usługi Twilio][twilio_pricing].</span><span class="sxs-lookup"><span data-stu-id="35d4e-122">You can find more details at [Twilio Pricing][twilio_pricing].</span></span>

## <span data-ttu-id="35d4e-123"><a id="Concepts"></a>Pojęcia</span><span class="sxs-lookup"><span data-stu-id="35d4e-123"><a id="Concepts"></a>Concepts</span></span>
<span data-ttu-id="35d4e-124">Witaj interfejsu API usługi Twilio jest interfejs API RESTful, która zapewnia funkcje programu SMS i komunikacja głosowa aplikacji.</span><span class="sxs-lookup"><span data-stu-id="35d4e-124">hello Twilio API is a RESTful API that provides voice and SMS functionality for applications.</span></span> <span data-ttu-id="35d4e-125">Klient biblioteki są dostępne w wielu językach; Aby uzyskać listę, zobacz [bibliotek interfejsu API usługi Twilio][twilio_libraries].</span><span class="sxs-lookup"><span data-stu-id="35d4e-125">Client libraries are available in multiple languages; for a list, see [Twilio API Libraries][twilio_libraries].</span></span>

<span data-ttu-id="35d4e-126">Kluczowe aspekty hello interfejsu API usługi Twilio są zleceń usługi Twilio i usługi Twilio Markup Language (TwiML).</span><span class="sxs-lookup"><span data-stu-id="35d4e-126">Key aspects of hello Twilio API are Twilio verbs and Twilio Markup Language (TwiML).</span></span>

### <span data-ttu-id="35d4e-127"><a id="Verbs"></a>Usługi Twilio zlecenia</span><span class="sxs-lookup"><span data-stu-id="35d4e-127"><a id="Verbs"></a>Twilio Verbs</span></span>
<span data-ttu-id="35d4e-128">Witaj interfejs API korzysta z usługi Twilio zleceń; na przykład Witaj  **&lt;powiedzieć&gt;**  zlecenie powoduje, że usługi Twilio tooaudibly dostarczenia komunikatu w wywołaniu.</span><span class="sxs-lookup"><span data-stu-id="35d4e-128">hello API makes use of Twilio verbs; for example, hello **&lt;Say&gt;** verb instructs Twilio tooaudibly deliver a message on a call.</span></span>

<span data-ttu-id="35d4e-129">Witaj poniżej przedstawiono listę poleceń usługi Twilio.</span><span class="sxs-lookup"><span data-stu-id="35d4e-129">hello following is a list of Twilio verbs.</span></span> <span data-ttu-id="35d4e-130">Dowiedz się więcej o hello innych poleceń i możliwości za pośrednictwem [dokumentacji usługi Twilio Markup Language](http://www.twilio.com/docs/api/twiml).</span><span class="sxs-lookup"><span data-stu-id="35d4e-130">Learn about hello other verbs and capabilities via [Twilio Markup Language documentation](http://www.twilio.com/docs/api/twiml).</span></span>

* <span data-ttu-id="35d4e-131">**&lt;Wybierania&gt;**: łączy hello wywołującego tooanother telefonu.</span><span class="sxs-lookup"><span data-stu-id="35d4e-131">**&lt;Dial&gt;**: Connects hello caller tooanother phone.</span></span>
* <span data-ttu-id="35d4e-132">**&lt;Zbierz&gt;**: zbiera wprowadzony na klawiaturze telefonu hello cyfr.</span><span class="sxs-lookup"><span data-stu-id="35d4e-132">**&lt;Gather&gt;**: Collects numeric digits entered on hello telephone keypad.</span></span>
* <span data-ttu-id="35d4e-133">**&lt;Rozłączanie&gt;**: kończy wywołanie.</span><span class="sxs-lookup"><span data-stu-id="35d4e-133">**&lt;Hangup&gt;**: Ends a call.</span></span>
* <span data-ttu-id="35d4e-134">**&lt;Odtwórz&gt;**: odtwarzania pliku audio.</span><span class="sxs-lookup"><span data-stu-id="35d4e-134">**&lt;Play&gt;**: Plays an audio file.</span></span>
* <span data-ttu-id="35d4e-135">**&lt;Wstrzymaj&gt;**: dyskretnie czeka na określoną liczbę sekund.</span><span class="sxs-lookup"><span data-stu-id="35d4e-135">**&lt;Pause&gt;**: Waits silently for a specified number of seconds.</span></span>
* <span data-ttu-id="35d4e-136">**&lt;Rekord&gt;**: rejestruje wywołującego hello głosu i zwraca adres URL pliku zawierającego hello rejestrowania.</span><span class="sxs-lookup"><span data-stu-id="35d4e-136">**&lt;Record&gt;**: Records hello caller's voice and returns a URL of a file that contains hello recording.</span></span>
* <span data-ttu-id="35d4e-137">**&lt;Przekieruj&gt;**: przekazuje kontrolę nad wywołania lub SMS toohello TwiML na inny adres URL.</span><span class="sxs-lookup"><span data-stu-id="35d4e-137">**&lt;Redirect&gt;**: Transfers control of a call or SMS toohello TwiML at a different URL.</span></span>
* <span data-ttu-id="35d4e-138">**&lt;Odrzuć&gt;**: odrzuca jako przychodzące wywołania numer usługi Twilio tooyour bez rozliczeń można</span><span class="sxs-lookup"><span data-stu-id="35d4e-138">**&lt;Reject&gt;**: Rejects an incoming call tooyour Twilio number without billing you</span></span>
* <span data-ttu-id="35d4e-139">**&lt;Powiedz&gt;**: Konwertuje tekst toospeech, które zostało utworzone w wywołaniu.</span><span class="sxs-lookup"><span data-stu-id="35d4e-139">**&lt;Say&gt;**: Converts text toospeech that is made on a call.</span></span>
* <span data-ttu-id="35d4e-140">**&lt;SMS&gt;**: wysyła wiadomość SMS.</span><span class="sxs-lookup"><span data-stu-id="35d4e-140">**&lt;Sms&gt;**: Sends an SMS message.</span></span>

### <span data-ttu-id="35d4e-141"><a id="TwiML"></a>TwiML</span><span class="sxs-lookup"><span data-stu-id="35d4e-141"><a id="TwiML"></a>TwiML</span></span>
<span data-ttu-id="35d4e-142">Zestaw instrukcji oparte na języku XML, oparte na powitania usługi Twilio zlecenia, które informują usługi Twilio, jak jest TwiML tooprocess wywołania lub wiadomości SMS.</span><span class="sxs-lookup"><span data-stu-id="35d4e-142">TwiML is a set of XML-based instructions based on hello Twilio verbs that inform Twilio of how tooprocess a call or SMS.</span></span>

<span data-ttu-id="35d4e-143">Na przykład powitania po TwiML może dokonać konwersji tekstu hello **Hello World** toospeech.</span><span class="sxs-lookup"><span data-stu-id="35d4e-143">As an example, hello following TwiML would convert hello text **Hello World** toospeech.</span></span>

    <?xml version="1.0" encoding="UTF-8" ?>
    <Response>
       <Say>Hello World</Say>
    </Response>

<span data-ttu-id="35d4e-144">Podczas wywołania aplikacji hello interfejsu API usługi Twilio, jeden z parametrów interfejsu API hello jest adres URL hello, która zwraca odpowiedź TwiML hello.</span><span class="sxs-lookup"><span data-stu-id="35d4e-144">When your application calls hello Twilio API, one of hello API parameters is hello URL that returns hello TwiML response.</span></span> <span data-ttu-id="35d4e-145">Do celów programistycznych możesz użyć wprowadzone do usługi Twilio adresy URL tooprovide hello TwiML odpowiedzi są używane przez aplikacje.</span><span class="sxs-lookup"><span data-stu-id="35d4e-145">For development purposes, you can use Twilio-provided URLs tooprovide hello TwiML responses used by your applications.</span></span> <span data-ttu-id="35d4e-146">Może również udostępniać swoje własne adresy URL tooproduce hello TwiML odpowiedzi, a inną opcją jest toouse hello **TwiMLResponse** obiektu.</span><span class="sxs-lookup"><span data-stu-id="35d4e-146">You could also host your own URLs tooproduce hello TwiML responses, and another option is toouse hello **TwiMLResponse** object.</span></span>

<span data-ttu-id="35d4e-147">Aby uzyskać więcej informacji na temat usługi Twilio zlecenia i ich atrybuty oraz TwiML, zobacz [TwiML][twiml].</span><span class="sxs-lookup"><span data-stu-id="35d4e-147">For more information about Twilio verbs, their attributes, and TwiML, see [TwiML][twiml].</span></span> <span data-ttu-id="35d4e-148">Aby uzyskać dodatkowe informacje na temat hello interfejsu API usługi Twilio, zobacz [interfejsu API usługi Twilio][twilio_api].</span><span class="sxs-lookup"><span data-stu-id="35d4e-148">For additional information about hello Twilio API, see [Twilio API][twilio_api].</span></span>

## <span data-ttu-id="35d4e-149"><a id="CreateAccount"></a>Tworzenie konta usługi Twilio</span><span class="sxs-lookup"><span data-stu-id="35d4e-149"><a id="CreateAccount"></a>Create a Twilio Account</span></span>
<span data-ttu-id="35d4e-150">Jeśli wszystko jest gotowe tooget konta usługi Twilio, zarejestruj się w [spróbuj usługi Twilio][try_twilio].</span><span class="sxs-lookup"><span data-stu-id="35d4e-150">When you're ready tooget a Twilio account, sign up at [Try Twilio][try_twilio].</span></span> <span data-ttu-id="35d4e-151">Można rozpoczynać bezpłatne konto, a następnie Uaktualnij swoje konto później.</span><span class="sxs-lookup"><span data-stu-id="35d4e-151">You can start with a free account, and upgrade your account later.</span></span>

<span data-ttu-id="35d4e-152">Po utworzeniu konta dla konta usługi Twilio, otrzymasz Identyfikatora konta oraz tokenu uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="35d4e-152">When you sign up for a Twilio account, you'll receive an account ID and an authentication token.</span></span> <span data-ttu-id="35d4e-153">Zarówno będzie potrzebne toomake wywołania interfejsu API usługi Twilio.</span><span class="sxs-lookup"><span data-stu-id="35d4e-153">Both will be needed toomake Twilio API calls.</span></span> <span data-ttu-id="35d4e-154">tooprevent nieautoryzowany dostęp do konta tooyour, bezpieczeństwo Twojego tokenu uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="35d4e-154">tooprevent unauthorized access tooyour account, keep your authentication token secure.</span></span> <span data-ttu-id="35d4e-155">Twój identyfikator konta i uwierzytelniania tokenu jest wyświetlana na powitania [strony konta usługi Twilio][twilio_account]w hello pola oznaczone **identyfikator SID konta** i **TOKEN uwierzytelniania**odpowiednio.</span><span class="sxs-lookup"><span data-stu-id="35d4e-155">Your account ID and authentication token are viewable at hello [Twilio account page][twilio_account], in hello fields labeled **ACCOUNT SID** and **AUTH TOKEN**, respectively.</span></span>

## <span data-ttu-id="35d4e-156"><a id="create_app"></a>Tworzenie aplikacji PHP</span><span class="sxs-lookup"><span data-stu-id="35d4e-156"><a id="create_app"></a>Create a PHP Application</span></span>
<span data-ttu-id="35d4e-157">Nie różni się od innych aplikacji PHP, który korzysta z usługi usługi Twilio hello się aplikacji PHP, która używa usługi usługi Twilio hello i działa na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="35d4e-157">A PHP application that uses hello Twilio service and is running in Azure is no different than any other PHP application that uses hello Twilio service.</span></span> <span data-ttu-id="35d4e-158">Usługi Twilio usług są opartego na interfejsie REST i może zostać wywołana z PHP na kilka sposobów, w tym artykule koncentruje się na jak toouse usługi Twilio usług za pomocą [biblioteki usługi Twilio dla programów PHP i z usługi GitHub][twilio_php].</span><span class="sxs-lookup"><span data-stu-id="35d4e-158">While Twilio services are REST-based and can be called from PHP in several ways, this article will focus on how toouse Twilio services with [Twilio library for PHP from GitHub][twilio_php].</span></span> <span data-ttu-id="35d4e-159">Aby uzyskać więcej informacji o korzystaniu z biblioteki usługi Twilio hello for PHP, zobacz [http://readthedocs.org/docs/twilio-php/en/latest/index.html][twilio_lib_docs].</span><span class="sxs-lookup"><span data-stu-id="35d4e-159">For more information about using hello Twilio library for PHP, see [http://readthedocs.org/docs/twilio-php/en/latest/index.html][twilio_lib_docs].</span></span>

<span data-ttu-id="35d4e-160">Szczegółowe instrukcje umożliwiające tworzenie i wdrażanie tooAzure aplikacji usługi Twilio/PHP są dostępne pod adresem [jak tooMake rozwiązania usługi przy użyciu Twilio w aplikacji PHP na platformie Azure rozmowy telefonicznej][howto_phonecall_php].</span><span class="sxs-lookup"><span data-stu-id="35d4e-160">Detailed instructions for building and deploying a Twilio/PHP application tooAzure are available at [How tooMake a Phone Call Using Twilio in a PHP Application on Azure][howto_phonecall_php].</span></span>

## <span data-ttu-id="35d4e-161"><a id="configure_app"></a>Konfigurowanie bibliotek usługi Twilio tooUse Twoja aplikacja</span><span class="sxs-lookup"><span data-stu-id="35d4e-161"><a id="configure_app"></a>Configure Your Application tooUse Twilio Libraries</span></span>
<span data-ttu-id="35d4e-162">Biblioteki usługi Twilio hello toouse aplikacji dla programu PHP można skonfigurować na dwa sposoby:</span><span class="sxs-lookup"><span data-stu-id="35d4e-162">You can configure your application toouse hello Twilio library for PHP in two ways:</span></span>

1. <span data-ttu-id="35d4e-163">Pobierz hello usługi Twilio biblioteki dla PHP z serwisu GitHub ([https://github.com/twilio/twilio-php][twilio_php]) i Dodaj hello **usług** katalogu tooyour aplikacji.</span><span class="sxs-lookup"><span data-stu-id="35d4e-163">Download hello Twilio library for PHP from GitHub ([https://github.com/twilio/twilio-php][twilio_php]) and add hello **Services** directory tooyour application.</span></span>
   
    <span data-ttu-id="35d4e-164">— Lub —</span><span class="sxs-lookup"><span data-stu-id="35d4e-164">-OR-</span></span>
2. <span data-ttu-id="35d4e-165">Zainstaluj biblioteki usługi Twilio hello dla programów PHP w pakiecie GRUSZKOWA.</span><span class="sxs-lookup"><span data-stu-id="35d4e-165">Install hello Twilio library for PHP as a PEAR package.</span></span> <span data-ttu-id="35d4e-166">Można zainstalować go z hello następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="35d4e-166">It can be installed with hello following commands:</span></span>
   
        $ pear channel-discover twilio.github.com/pear
        $ pear install twilio/Services_Twilio

<span data-ttu-id="35d4e-167">Po zainstalowaniu biblioteki usługi Twilio hello for PHP można dodać **require_once** instrukcji u góry hello programu PHP pliki tooreference hello biblioteki:</span><span class="sxs-lookup"><span data-stu-id="35d4e-167">Once you have installed hello Twilio library for PHP, you can then add a **require_once** statement at hello top of your PHP files tooreference hello library:</span></span>

        require_once 'Services/Twilio.php';

<span data-ttu-id="35d4e-168">Aby uzyskać więcej informacji, zobacz [https://github.com/twilio/twilio-php/blob/master/README.md][twilio_github_readme].</span><span class="sxs-lookup"><span data-stu-id="35d4e-168">For more information, see [https://github.com/twilio/twilio-php/blob/master/README.md][twilio_github_readme].</span></span>

## <span data-ttu-id="35d4e-169"><a id="howto_make_call"></a>Porady: wykonywanie połączenia wychodzące</span><span class="sxs-lookup"><span data-stu-id="35d4e-169"><a id="howto_make_call"></a>How to: Make an outgoing call</span></span>
<span data-ttu-id="35d4e-170">Witaj poniżej pokazano, jak toomake wychodzące wywołanie przy użyciu hello **Services_Twilio** klasy.</span><span class="sxs-lookup"><span data-stu-id="35d4e-170">hello following shows how toomake an outgoing call using hello **Services_Twilio** class.</span></span> <span data-ttu-id="35d4e-171">Ten kod zawiera również hello tooreturn lokacja dostarczonych do usługi Twilio odpowiedzi usługi Twilio Markup Language (TwiML).</span><span class="sxs-lookup"><span data-stu-id="35d4e-171">This code also uses a Twilio-provided site tooreturn hello Twilio Markup Language (TwiML) response.</span></span> <span data-ttu-id="35d4e-172">Podstaw wartości hello **z** i **do** numerów telefonów i upewnij się, że sprawdzisz hello **z** numer telefonu dla kodu hello toorunning poprzedniego konta usługi Twilio.</span><span class="sxs-lookup"><span data-stu-id="35d4e-172">Substitute your values for hello **From** and **To** phone numbers, and ensure that you verify hello **From** phone number for your Twilio account prior toorunning hello code.</span></span>

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

<span data-ttu-id="35d4e-173">Jak wspomniano, ten kod używa hello tooreturn lokacja dostarczonych do usługi Twilio TwiML odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="35d4e-173">As mentioned, this code uses a Twilio-provided site tooreturn hello TwiML response.</span></span> <span data-ttu-id="35d4e-174">Zamiast tego można użyć własnych lokacji tooprovide hello odpowiedzi TwiML; Aby uzyskać więcej informacji, zobacz [jak tooProvide TwiML odpowiedzi z Twoje własne witryny sieci Web](#howto_provide_twiml_responses).</span><span class="sxs-lookup"><span data-stu-id="35d4e-174">You could instead use your own site tooprovide hello TwiML response; for more information, see [How tooProvide TwiML Responses from Your Own Web Site](#howto_provide_twiml_responses).</span></span>

* <span data-ttu-id="35d4e-175">**Uwaga**: tootroubleshoot błędy sprawdzania poprawności certyfikatów SSL, zobacz [http://readthedocs.org/docs/twilio-php/en/latest/usage/rest.html][ssl_validation]</span><span class="sxs-lookup"><span data-stu-id="35d4e-175">**Note**: tootroubleshoot SSL certificate validation errors, see [http://readthedocs.org/docs/twilio-php/en/latest/usage/rest.html][ssl_validation]</span></span> 

## <span data-ttu-id="35d4e-176"><a id="howto_send_sms"></a>Porady: Wyślij wiadomość SMS</span><span class="sxs-lookup"><span data-stu-id="35d4e-176"><a id="howto_send_sms"></a>How to: Send an SMS message</span></span>
<span data-ttu-id="35d4e-177">Witaj poniżej pokazano, jak hello toosend wiadomość SMS przy użyciu **Services_Twilio** klasy.</span><span class="sxs-lookup"><span data-stu-id="35d4e-177">hello following shows how toosend an SMS message using hello **Services_Twilio** class.</span></span> <span data-ttu-id="35d4e-178">Witaj **z** numer jest udostępniany przez usługi Twilio dla wersji próbnej kont toosend wiadomości SMS.</span><span class="sxs-lookup"><span data-stu-id="35d4e-178">hello **From** number is provided by Twilio for trial accounts toosend SMS messages.</span></span> <span data-ttu-id="35d4e-179">Witaj **do** należy sprawdzić liczbę dla kodu hello toorunning poprzedniego konta usługi Twilio.</span><span class="sxs-lookup"><span data-stu-id="35d4e-179">hello **To** number must be verified for your Twilio account prior toorunning hello code.</span></span>

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

## <span data-ttu-id="35d4e-180"><a id="howto_provide_twiml_responses"></a>Porady: Podaj TwiML odpowiedzi z własnej witryny sieci Web</span><span class="sxs-lookup"><span data-stu-id="35d4e-180"><a id="howto_provide_twiml_responses"></a>How to: Provide TwiML Responses from your own Website</span></span>
<span data-ttu-id="35d4e-181">Gdy aplikacja inicjuje toohello wywołania interfejsu API usługi Twilio, usługi Twilio będzie wysyłać adres URL tooa żądania, który jest oczekiwany tooreturn odpowiedzi TwiML.</span><span class="sxs-lookup"><span data-stu-id="35d4e-181">When your application initiates a call toohello Twilio API, Twilio will send your request tooa URL that is expected tooreturn a TwiML response.</span></span> <span data-ttu-id="35d4e-182">w powyższym przykładzie Hello używa adresu URL dostarczony do usługi Twilio hello [http://twimlets.com/message][twimlet_message_url].</span><span class="sxs-lookup"><span data-stu-id="35d4e-182">hello example above uses hello Twilio-provided URL [http://twimlets.com/message][twimlet_message_url].</span></span> <span data-ttu-id="35d4e-183">(Podczas TwiML jest przeznaczony do użytku przez usługi Twilio, można wyświetlić hello go w przeglądarce.</span><span class="sxs-lookup"><span data-stu-id="35d4e-183">(While TwiML is designed for use by Twilio, you can view hello it in your browser.</span></span> <span data-ttu-id="35d4e-184">Na przykład kliknij pozycję [http://twimlets.com/message] [ twimlet_message_url] toosee pustą `<Response>` element; inny przykład kliknij [http://twimlets.com/message? Komunikat % 5B0 %5 D = Hello % 20World] [ twimlet_message_url_hello_world] toosee `<Response>` element, który zawiera `<Say>` elementu.)</span><span class="sxs-lookup"><span data-stu-id="35d4e-184">For example, click [http://twimlets.com/message][twimlet_message_url] toosee an empty `<Response>` element; as another example, click [http://twimlets.com/message?Message%5B0%5D=Hello%20World][twimlet_message_url_hello_world] toosee a `<Response>` element that contains a `<Say>` element.)</span></span>

<span data-ttu-id="35d4e-185">Zamiast polegania na adres URL udostępniony do usługi Twilio hello, można utworzyć własne lokacji, która zwraca odpowiedzi HTTP.</span><span class="sxs-lookup"><span data-stu-id="35d4e-185">Instead of relying on hello Twilio-provided URL, you can create your own site that returns HTTP responses.</span></span> <span data-ttu-id="35d4e-186">Można utworzyć witrynę hello w dowolnym języku, który zwraca odpowiedzi XML; w tym temacie założono, że należy używać PHP toocreate hello TwiML.</span><span class="sxs-lookup"><span data-stu-id="35d4e-186">You can create hello site in any language that returns XML responses; this topic assumes you'll be using PHP toocreate hello TwiML.</span></span>

<span data-ttu-id="35d4e-187">Witaj po PHP wyników strony w odpowiedzi TwiML stwierdzający, **Hello World** na powitania wywołania.</span><span class="sxs-lookup"><span data-stu-id="35d4e-187">hello following PHP page results in a TwiML response that says **Hello World** on hello call.</span></span>

    <?php    
        header("content-type: text/xml");    
        echo "<?xml version=\"1.0\" encoding=\"UTF-8\"?>\n";
    ?>
    <Response>    
        <Say>Hello world.</Say>
    </Response>

<span data-ttu-id="35d4e-188">Jak widać w powyższym przykładzie hello hello TwiML odpowiedzi jest po prostu dokumentu XML.</span><span class="sxs-lookup"><span data-stu-id="35d4e-188">As you can see from hello example above, hello TwiML response is simply an XML document.</span></span> <span data-ttu-id="35d4e-189">Biblioteka usługi Twilio Hello dla programów PHP i zawiera klasy, które generuje TwiML dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="35d4e-189">hello Twilio library for PHP contains classes that will generate TwiML for you.</span></span> <span data-ttu-id="35d4e-190">w poniższym przykładzie Hello tworzy hello równoważne odpowiedzi, jak pokazano powyżej, ale używa hello **usług\_usługi Twilio\_Twiml** klasy w bibliotece usługi Twilio hello programu PHP:</span><span class="sxs-lookup"><span data-stu-id="35d4e-190">hello example below produces hello equivalent response as shown above, but uses hello **Services\_Twilio\_Twiml** class in hello Twilio library for PHP:</span></span>

    require_once('Services/Twilio.php');

    $response = new Services_Twilio_Twiml();
    $response->say("Hello world.");
    print $response;

<span data-ttu-id="35d4e-191">Aby uzyskać więcej informacji o TwiML, zobacz [https://www.twilio.com/docs/api/twiml][twiml_reference].</span><span class="sxs-lookup"><span data-stu-id="35d4e-191">For more information about TwiML, see [https://www.twilio.com/docs/api/twiml][twiml_reference].</span></span> 

<span data-ttu-id="35d4e-192">Po utworzeniu strony PHP Konfigurowanie odpowiedzi TwiML tooprovide, użyj hello adres URL strony PHP hello hello adres URL przekazany hello `Services_Twilio->account->calls->create` metody.</span><span class="sxs-lookup"><span data-stu-id="35d4e-192">Once you have your PHP page set up tooprovide TwiML responses, use hello URL of hello PHP page as hello URL passed into hello  `Services_Twilio->account->calls->create`  method.</span></span> <span data-ttu-id="35d4e-193">Na przykład, jeśli masz aplikację sieci Web o nazwie **MyTwiML** wdrożonej tooan Azure usługi hostowanej, a nazwa hello strony PHP hello jest **mytwiml.php**, adres URL, które mogą zostać przekazane za hello **Services_ Usługi Twilio -> konta -> wywołania -> Utwórz** pokazane na powitania poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="35d4e-193">For example, if you have a Web application named **MyTwiML** deployed tooan Azure hosted service, and hello name of hello PHP page is **mytwiml.php**, hello URL can be passed too **Services_Twilio->account->calls->create**  as shown in hello following example:</span></span>

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

<span data-ttu-id="35d4e-194">Aby uzyskać dodatkowe informacje dotyczące korzystania z usługi Twilio na platformie Azure za pomocą języka PHP, zobacz [jak tooMake rozwiązania usługi przy użyciu Twilio w aplikacji PHP na platformie Azure rozmowy telefonicznej][howto_phonecall_php].</span><span class="sxs-lookup"><span data-stu-id="35d4e-194">For additional information about using Twilio in Azure with PHP, see [How tooMake a Phone Call Using Twilio in a PHP Application on Azure][howto_phonecall_php].</span></span>

## <span data-ttu-id="35d4e-195"><a id="AdditionalServices"></a>Porady: korzystania z usługi Twilio dodatkowych usług</span><span class="sxs-lookup"><span data-stu-id="35d4e-195"><a id="AdditionalServices"></a>How to: Use Additional Twilio Services</span></span>
<span data-ttu-id="35d4e-196">Ponadto przykłady toohello pokazane, usługi Twilio oferuje API sieci web można używać tooleverage dodatkowe usługi Twilio funkcji z aplikacji Azure.</span><span class="sxs-lookup"><span data-stu-id="35d4e-196">In addition toohello examples shown here, Twilio offers web-based APIs that you can use tooleverage additional Twilio functionality from your Azure application.</span></span> <span data-ttu-id="35d4e-197">Aby uzyskać szczegółowe informacje, zobacz hello [dokumentacji interfejsu API usługi Twilio][twilio_api_documentation].</span><span class="sxs-lookup"><span data-stu-id="35d4e-197">For full details, see hello [Twilio API documentation][twilio_api_documentation].</span></span>

## <span data-ttu-id="35d4e-198"><a id="NextSteps"></a>Następne kroki</span><span class="sxs-lookup"><span data-stu-id="35d4e-198"><a id="NextSteps"></a>Next Steps</span></span>
<span data-ttu-id="35d4e-199">Teraz, kiedy znasz już podstawy hello hello usługi usługi Twilio, wykonaj te więcej toolearn łącza:</span><span class="sxs-lookup"><span data-stu-id="35d4e-199">Now that you've learned hello basics of hello Twilio service, follow these links toolearn more:</span></span>

* <span data-ttu-id="35d4e-200">[Wytyczne dotyczące zabezpieczeń usługi Twilio][twilio_security_guidelines]</span><span class="sxs-lookup"><span data-stu-id="35d4e-200">[Twilio Security Guidelines][twilio_security_guidelines]</span></span>
* <span data-ttu-id="35d4e-201">[Porada usługi Twilio i przykładowy kod][twilio_howtos]</span><span class="sxs-lookup"><span data-stu-id="35d4e-201">[Twilio HowTo's and Example Code][twilio_howtos]</span></span>
* <span data-ttu-id="35d4e-202">[Samouczki usługi Twilio Szybki Start][twilio_quickstarts]</span><span class="sxs-lookup"><span data-stu-id="35d4e-202">[Twilio Quickstart Tutorials][twilio_quickstarts]</span></span> 
* <span data-ttu-id="35d4e-203">[Usługi Twilio w witrynie GitHub][twilio_on_github]</span><span class="sxs-lookup"><span data-stu-id="35d4e-203">[Twilio on GitHub][twilio_on_github]</span></span>
* <span data-ttu-id="35d4e-204">[Porozmawiaj tooTwilio pomocy technicznej][twilio_support]</span><span class="sxs-lookup"><span data-stu-id="35d4e-204">[Talk tooTwilio Support][twilio_support]</span></span>

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
