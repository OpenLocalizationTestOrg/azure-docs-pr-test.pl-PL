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
# <a name="how-toouse-twilio-for-voice-and-sms-capabilities-in-ruby"></a><span data-ttu-id="32ccf-104">Jak tooUse usługi Twilio głosowe i możliwości programu SMS w języku Ruby</span><span class="sxs-lookup"><span data-stu-id="32ccf-104">How tooUse Twilio for Voice and SMS Capabilities in Ruby</span></span>
<span data-ttu-id="32ccf-105">W tym przewodniku pokazano, jak tooperform typowych zadań programowania hello interfejsu API usługi Twilio usługi na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="32ccf-105">This guide demonstrates how tooperform common programming tasks with hello Twilio API service on Azure.</span></span> <span data-ttu-id="32ccf-106">omówione scenariusze Hello obejmują tworzenie połączeń telefonicznych i wysyłanie wiadomości krótką wiadomość usługi (SMS).</span><span class="sxs-lookup"><span data-stu-id="32ccf-106">hello scenarios covered include making a phone call and sending a Short Message Service (SMS) message.</span></span> <span data-ttu-id="32ccf-107">Aby uzyskać więcej informacji na temat usługi Twilio i komunikacja głosowa programu SMS w aplikacji, zobacz hello [następne kroki](#NextSteps) sekcji.</span><span class="sxs-lookup"><span data-stu-id="32ccf-107">For more information on Twilio and using voice and SMS in your applications, see hello [Next Steps](#NextSteps) section.</span></span>

## <span data-ttu-id="32ccf-108"><a id="WhatIs"></a>Co to jest usługi Twilio?</span><span class="sxs-lookup"><span data-stu-id="32ccf-108"><a id="WhatIs"></a>What is Twilio?</span></span>
<span data-ttu-id="32ccf-109">Usługi Twilio jest telefonii API usługi sieci web, która umożliwia korzystanie z istniejących języków sieci web i umiejętności toobuild głosu aplikacji i programu SMS.</span><span class="sxs-lookup"><span data-stu-id="32ccf-109">Twilio is a telephony web-service API that lets you use your existing web languages and skills toobuild voice and SMS applications.</span></span> <span data-ttu-id="32ccf-110">Usługi Twilio jest usługą innych firm (nie funkcji platformy Azure i nie produkt firmy Microsoft).</span><span class="sxs-lookup"><span data-stu-id="32ccf-110">Twilio is a third-party service (not an Azure feature and not a Microsoft product).</span></span>

<span data-ttu-id="32ccf-111">**Usługi Twilio głosu** umożliwia toomake Twojej aplikacji i odbieranie połączeń telefonicznych.</span><span class="sxs-lookup"><span data-stu-id="32ccf-111">**Twilio Voice** allows your applications toomake and receive phone calls.</span></span> <span data-ttu-id="32ccf-112">**SMS usługi Twilio** umożliwia toomake Twojej aplikacji i odbieranie wiadomości SMS.</span><span class="sxs-lookup"><span data-stu-id="32ccf-112">**Twilio SMS** allows your applications toomake and receive SMS messages.</span></span> <span data-ttu-id="32ccf-113">**Klient usługi Twilio** umożliwia aplikacji komunikację głosową tooenable przy użyciu istniejących połączeń internetowych, w tym przenośnych połączenia.</span><span class="sxs-lookup"><span data-stu-id="32ccf-113">**Twilio Client** allows your applications tooenable voice communication using existing Internet connections, including mobile connections.</span></span>

## <span data-ttu-id="32ccf-114"><a id="Pricing"></a>Cennik usługi Twilio i oferty specjalne</span><span class="sxs-lookup"><span data-stu-id="32ccf-114"><a id="Pricing"></a>Twilio Pricing and Special Offers</span></span>
<span data-ttu-id="32ccf-115">Informacje o cenach usługi Twilio znajduje się w temacie [cennik usługi Twilio][twilio_pricing].</span><span class="sxs-lookup"><span data-stu-id="32ccf-115">Information about Twilio pricing is available at [Twilio Pricing][twilio_pricing].</span></span> <span data-ttu-id="32ccf-116">Azure klienci otrzymają [oferta specjalna][special_offer]: wolnego środki tekstów 1000 lub 1000 ruchu przychodzącego minut.</span><span class="sxs-lookup"><span data-stu-id="32ccf-116">Azure customers receive a [special offer][special_offer]: a free credit of 1000 texts or 1000 inbound minutes.</span></span> <span data-ttu-id="32ccf-117">toosign dla to oferty lub uzyskać więcej informacji, odwiedź stronę [http://ahoy.twilio.com/azure][special_offer].</span><span class="sxs-lookup"><span data-stu-id="32ccf-117">toosign up for this offer or get more information, please visit [http://ahoy.twilio.com/azure][special_offer].</span></span>  

## <span data-ttu-id="32ccf-118"><a id="Concepts"></a>Pojęcia</span><span class="sxs-lookup"><span data-stu-id="32ccf-118"><a id="Concepts"></a>Concepts</span></span>
<span data-ttu-id="32ccf-119">Witaj interfejsu API usługi Twilio jest interfejs API RESTful, która zapewnia funkcje programu SMS i komunikacja głosowa aplikacji.</span><span class="sxs-lookup"><span data-stu-id="32ccf-119">hello Twilio API is a RESTful API that provides voice and SMS functionality for applications.</span></span> <span data-ttu-id="32ccf-120">Klient biblioteki są dostępne w wielu językach; Aby uzyskać listę, zobacz [bibliotek interfejsu API usługi Twilio][twilio_libraries].</span><span class="sxs-lookup"><span data-stu-id="32ccf-120">Client libraries are available in multiple languages; for a list, see [Twilio API Libraries][twilio_libraries].</span></span>

### <span data-ttu-id="32ccf-121"><a id="TwiML"></a>TwiML</span><span class="sxs-lookup"><span data-stu-id="32ccf-121"><a id="TwiML"></a>TwiML</span></span>
<span data-ttu-id="32ccf-122">Zestaw instrukcji opartych na języku XML, które informują usługi Twilio, jak jest TwiML tooprocess wywołania lub wiadomości SMS.</span><span class="sxs-lookup"><span data-stu-id="32ccf-122">TwiML is a set of XML-based instructions that inform Twilio of how tooprocess a call or SMS.</span></span>

<span data-ttu-id="32ccf-123">Na przykład powitania po TwiML może dokonać konwersji tekstu hello **Hello World** toospeech.</span><span class="sxs-lookup"><span data-stu-id="32ccf-123">As an example, hello following TwiML would convert hello text **Hello World** toospeech.</span></span>

    <?xml version="1.0" encoding="UTF-8" ?>
    <Response>
       <Say>Hello World</Say>
    </Response>

<span data-ttu-id="32ccf-124">Wszystkie dokumenty TwiML mają `<Response>` jako ich elementu głównego.</span><span class="sxs-lookup"><span data-stu-id="32ccf-124">All TwiML documents have `<Response>` as their root element.</span></span> <span data-ttu-id="32ccf-125">Z tego miejsca korzystając z usługi Twilio zleceń toodefine hello działanie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="32ccf-125">From there, you use Twilio Verbs toodefine hello behavior of your application.</span></span>

### <span data-ttu-id="32ccf-126"><a id="Verbs"></a>TwiML zlecenia</span><span class="sxs-lookup"><span data-stu-id="32ccf-126"><a id="Verbs"></a>TwiML Verbs</span></span>
<span data-ttu-id="32ccf-127">Usługi Twilio zlecenia są tagi XML, które informują usługi Twilio, co to za**czy**.</span><span class="sxs-lookup"><span data-stu-id="32ccf-127">Twilio Verbs are XML tags that tell Twilio what too**do**.</span></span> <span data-ttu-id="32ccf-128">Na przykład Witaj  **&lt;powiedzieć&gt;**  zlecenie powoduje, że usługi Twilio tooaudibly dostarczenia komunikatu w wywołaniu.</span><span class="sxs-lookup"><span data-stu-id="32ccf-128">For example, hello **&lt;Say&gt;** verb instructs Twilio tooaudibly deliver a message on a call.</span></span> 

<span data-ttu-id="32ccf-129">Witaj poniżej przedstawiono listę poleceń usługi Twilio.</span><span class="sxs-lookup"><span data-stu-id="32ccf-129">hello following is a list of Twilio verbs.</span></span>

* <span data-ttu-id="32ccf-130">**&lt;Wybierania&gt;**: łączy hello wywołującego tooanother telefonu.</span><span class="sxs-lookup"><span data-stu-id="32ccf-130">**&lt;Dial&gt;**: Connects hello caller tooanother phone.</span></span>
* <span data-ttu-id="32ccf-131">**&lt;Zbierz&gt;**: zbiera wprowadzony na klawiaturze telefonu hello cyfr.</span><span class="sxs-lookup"><span data-stu-id="32ccf-131">**&lt;Gather&gt;**: Collects numeric digits entered on hello telephone keypad.</span></span>
* <span data-ttu-id="32ccf-132">**&lt;Rozłączanie&gt;**: kończy wywołanie.</span><span class="sxs-lookup"><span data-stu-id="32ccf-132">**&lt;Hangup&gt;**: Ends a call.</span></span>
* <span data-ttu-id="32ccf-133">**&lt;Odtwórz&gt;**: odtwarzania pliku audio.</span><span class="sxs-lookup"><span data-stu-id="32ccf-133">**&lt;Play&gt;**: Plays an audio file.</span></span>
* <span data-ttu-id="32ccf-134">**&lt;Wstrzymaj&gt;**: dyskretnie czeka na określoną liczbę sekund.</span><span class="sxs-lookup"><span data-stu-id="32ccf-134">**&lt;Pause&gt;**: Waits silently for a specified number of seconds.</span></span>
* <span data-ttu-id="32ccf-135">**&lt;Rekord&gt;**: rejestruje wywołującego hello głosu i zwraca adres URL pliku zawierającego hello rejestrowania.</span><span class="sxs-lookup"><span data-stu-id="32ccf-135">**&lt;Record&gt;**: Records hello caller's voice and returns a URL of a file that contains hello recording.</span></span>
* <span data-ttu-id="32ccf-136">**&lt;Przekieruj&gt;**: przekazuje kontrolę nad wywołania lub SMS toohello TwiML na inny adres URL.</span><span class="sxs-lookup"><span data-stu-id="32ccf-136">**&lt;Redirect&gt;**: Transfers control of a call or SMS toohello TwiML at a different URL.</span></span>
* <span data-ttu-id="32ccf-137">**&lt;Odrzuć&gt;**: odrzuca jako przychodzące wywołania numer usługi Twilio tooyour bez rozliczeń można</span><span class="sxs-lookup"><span data-stu-id="32ccf-137">**&lt;Reject&gt;**: Rejects an incoming call tooyour Twilio number without billing you</span></span>
* <span data-ttu-id="32ccf-138">**&lt;Powiedz&gt;**: Konwertuje tekst toospeech, które zostało utworzone w wywołaniu.</span><span class="sxs-lookup"><span data-stu-id="32ccf-138">**&lt;Say&gt;**: Converts text toospeech that is made on a call.</span></span>
* <span data-ttu-id="32ccf-139">**&lt;SMS&gt;**: wysyła wiadomość SMS.</span><span class="sxs-lookup"><span data-stu-id="32ccf-139">**&lt;Sms&gt;**: Sends an SMS message.</span></span>

<span data-ttu-id="32ccf-140">Aby uzyskać więcej informacji na temat usługi Twilio zlecenia i ich atrybuty oraz TwiML, zobacz [TwiML][twiml].</span><span class="sxs-lookup"><span data-stu-id="32ccf-140">For more information about Twilio verbs, their attributes, and TwiML, see [TwiML][twiml].</span></span> <span data-ttu-id="32ccf-141">Aby uzyskać dodatkowe informacje na temat hello interfejsu API usługi Twilio, zobacz [interfejsu API usługi Twilio][twilio_api].</span><span class="sxs-lookup"><span data-stu-id="32ccf-141">For additional information about hello Twilio API, see [Twilio API][twilio_api].</span></span>

## <span data-ttu-id="32ccf-142"><a id="CreateAccount"></a>Tworzenie konta usługi Twilio</span><span class="sxs-lookup"><span data-stu-id="32ccf-142"><a id="CreateAccount"></a>Create a Twilio Account</span></span>
<span data-ttu-id="32ccf-143">Jeśli wszystko jest gotowe tooget konta usługi Twilio, zarejestruj się w [spróbuj usługi Twilio][try_twilio].</span><span class="sxs-lookup"><span data-stu-id="32ccf-143">When you're ready tooget a Twilio account, sign up at [Try Twilio][try_twilio].</span></span> <span data-ttu-id="32ccf-144">Można rozpoczynać bezpłatne konto, a następnie Uaktualnij swoje konto później.</span><span class="sxs-lookup"><span data-stu-id="32ccf-144">You can start with a free account, and upgrade your account later.</span></span>

<span data-ttu-id="32ccf-145">Po utworzeniu konta dla konta usługi Twilio, otrzymasz numer telefonu bezpłatnej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="32ccf-145">When you sign up for a Twilio account, you'll get a free phone number for your application.</span></span> <span data-ttu-id="32ccf-146">Otrzymasz również identyfikatora SID konta, a token uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="32ccf-146">You'll also receive an account SID and an auth token.</span></span> <span data-ttu-id="32ccf-147">Zarówno będzie potrzebne toomake wywołania interfejsu API usługi Twilio.</span><span class="sxs-lookup"><span data-stu-id="32ccf-147">Both will be needed toomake Twilio API calls.</span></span> <span data-ttu-id="32ccf-148">tooprevent nieautoryzowany dostęp do konta tooyour, bezpieczeństwo Twojego tokenu uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="32ccf-148">tooprevent unauthorized access tooyour account, keep your authentication token secure.</span></span> <span data-ttu-id="32ccf-149">Identyfikator SID konta, a token uwierzytelniania jest wyświetlana na powitania [strony konta usługi Twilio][twilio_account]w hello pola oznaczone **identyfikator SID konta** i **TOKEN uwierzytelniania** , odpowiednio.</span><span class="sxs-lookup"><span data-stu-id="32ccf-149">Your account SID and auth token are viewable at hello [Twilio account page][twilio_account], in hello fields labeled **ACCOUNT SID** and **AUTH TOKEN**, respectively.</span></span>

### <span data-ttu-id="32ccf-150"><a id="VerifyPhoneNumbers"></a>Sprawdź numery telefonów</span><span class="sxs-lookup"><span data-stu-id="32ccf-150"><a id="VerifyPhoneNumbers"></a>Verify Phone Numbers</span></span>
<span data-ttu-id="32ccf-151">Dodanie wiele toohello są podane przez usługi Twilio można również sprawdzić numery kontroli (np. telefon komórkowy lub głównej numer telefonu) do użycia w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="32ccf-151">In addition toohello number you are given by Twilio, you can also verify numbers that you control (i.e. your cell phone or home phone number) for use in your applications.</span></span> 

<span data-ttu-id="32ccf-152">Aby uzyskać informacje na temat tooverify numer telefonu, zobacz [Zarządzanie numery][verify_phone].</span><span class="sxs-lookup"><span data-stu-id="32ccf-152">For information on how tooverify a phone number, see [Manage Numbers][verify_phone].</span></span>

## <span data-ttu-id="32ccf-153"><a id="create_app"></a>Tworzenie aplikacji Ruby</span><span class="sxs-lookup"><span data-stu-id="32ccf-153"><a id="create_app"></a>Create a Ruby Application</span></span>
<span data-ttu-id="32ccf-154">Nie różni się od innych dopisków fonetycznych aplikacji, która przy użyciu usługi usługi Twilio hello się dopisków fonetycznych aplikacji, która używa usługi usługi Twilio hello i działa na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="32ccf-154">A Ruby application that uses hello Twilio service and is running in Azure is no different than any other Ruby application that uses hello Twilio service.</span></span> <span data-ttu-id="32ccf-155">Usługi Twilio usług są RESTful i może zostać wywołana z Ruby na kilka sposobów, w tym artykule koncentruje się na jak toouse usługi Twilio usług za pomocą [usługi Twilio biblioteki pomocnika dla środowiska Ruby][twilio_ruby].</span><span class="sxs-lookup"><span data-stu-id="32ccf-155">While Twilio services are RESTful and can be called from Ruby in several ways, this article will focus on how toouse Twilio services with [Twilio helper library for Ruby][twilio_ruby].</span></span>

<span data-ttu-id="32ccf-156">Najpierw [konfiguracji nowej maszyny Wirtualnej systemu Linux Azure] [ azure_vm_setup] tooact jako hosta dla nowej aplikacji sieci web dopisków fonetycznych.</span><span class="sxs-lookup"><span data-stu-id="32ccf-156">First, [set-up a new Azure Linux VM][azure_vm_setup] tooact as a host for your new Ruby web application.</span></span> <span data-ttu-id="32ccf-157">Pomiń kroki hello obejmujący tworzenie hello szyny aplikacji, po prostu hello konfiguracji maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="32ccf-157">Ignore hello steps involving hello creation of a Rails app, just set-up hello VM.</span></span> <span data-ttu-id="32ccf-158">Upewnij się, że utworzono punkt końcowy z zewnętrznego portu 80 i wewnętrzny port 5000.</span><span class="sxs-lookup"><span data-stu-id="32ccf-158">Make sure you create an Endpoint with an external port of 80 and an internal port of 5000.</span></span>

<span data-ttu-id="32ccf-159">W poniższych przykładach hello, użyjemy [Sinatra][sinatra], ramy bardzo proste sieci web dla środowiska Ruby.</span><span class="sxs-lookup"><span data-stu-id="32ccf-159">In hello examples below, we will be using [Sinatra][sinatra], a very simple web framework for Ruby.</span></span> <span data-ttu-id="32ccf-160">Ale pewnością służy hello usługi Twilio pomocnika biblioteki dla środowiska Ruby z żadnych innych platforma sieci web, w tym Ruby na szyny.</span><span class="sxs-lookup"><span data-stu-id="32ccf-160">But you can certainly use hello Twilio helper library for Ruby with any other web framework, including Ruby on Rails.</span></span>

<span data-ttu-id="32ccf-161">SSH do nowej maszyny Wirtualnej i Utwórz katalog dla nowej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="32ccf-161">SSH into your new VM and create a directory for your new app.</span></span> <span data-ttu-id="32ccf-162">W tym katalogu Utwórz plik o nazwie hello Gemfile i skopiuj następujące kodu do niej:</span><span class="sxs-lookup"><span data-stu-id="32ccf-162">Inside that directory, create a file called Gemfile and copy hello following code into it:</span></span>

    source 'https://rubygems.org'
    gem 'sinatra'
    gem 'thin'

<span data-ttu-id="32ccf-163">Uruchom w wierszu polecenia hello `bundle install`.</span><span class="sxs-lookup"><span data-stu-id="32ccf-163">On hello command line run `bundle install`.</span></span> <span data-ttu-id="32ccf-164">Spowoduje to zainstalowanie hello zależności powyżej.</span><span class="sxs-lookup"><span data-stu-id="32ccf-164">This will install hello dependencies above.</span></span> <span data-ttu-id="32ccf-165">Następnie utwórz plik o nazwie `web.rb`.</span><span class="sxs-lookup"><span data-stu-id="32ccf-165">Next create a file called `web.rb`.</span></span> <span data-ttu-id="32ccf-166">Są to, gdzie znajduje się kod powitania dla aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="32ccf-166">This will be where hello code for your web app lives.</span></span> <span data-ttu-id="32ccf-167">Wklej hello następującego kodu do niej:</span><span class="sxs-lookup"><span data-stu-id="32ccf-167">Paste hello following code into it:</span></span>

    require 'sinatra'

    get '/' do
        "Hello Monkey!"
    end

<span data-ttu-id="32ccf-168">Na tym etapie należy hello można uruchomić polecenie hello `ruby web.rb -p 5000`.</span><span class="sxs-lookup"><span data-stu-id="32ccf-168">At this point you should be able hello run hello command `ruby web.rb -p 5000`.</span></span> <span data-ttu-id="32ccf-169">To spowoduje rozkręcenia serwera sieci web małej na port 5000.</span><span class="sxs-lookup"><span data-stu-id="32ccf-169">This will spin-up a small web server on port 5000.</span></span> <span data-ttu-id="32ccf-170">Powinno być możliwe toobrowse toothis aplikacji w przeglądarce, przechodząc na stronę hello adresu URL skonfigurowanych dla maszyny Wirtualnej Azure.</span><span class="sxs-lookup"><span data-stu-id="32ccf-170">You should be able toobrowse toothis app in your browser by visiting hello URL you set-up for your Azure VM.</span></span> <span data-ttu-id="32ccf-171">Po osiągnięciu można aplikacji sieci web w przeglądarce hello, wszystko jest gotowe toostart tworzeniem aplikacji usługi Twilio.</span><span class="sxs-lookup"><span data-stu-id="32ccf-171">Once you can reach your web app in hello browser, you're ready toostart building a Twilio app.</span></span>

## <span data-ttu-id="32ccf-172"><a id="configure_app"></a>Skonfiguruj tooUse Twoja aplikacja usługi Twilio</span><span class="sxs-lookup"><span data-stu-id="32ccf-172"><a id="configure_app"></a>Configure Your Application tooUse Twilio</span></span>
<span data-ttu-id="32ccf-173">Biblioteki usługi Twilio hello toouse aplikacji sieci web można skonfigurować, aktualizując Twojej `Gemfile` tooinclude ten wiersz:</span><span class="sxs-lookup"><span data-stu-id="32ccf-173">You can configure your web app toouse hello Twilio library by updating your `Gemfile` tooinclude this line:</span></span>

    gem 'twilio-ruby'

<span data-ttu-id="32ccf-174">W wierszu polecenia hello, uruchom `bundle install`.</span><span class="sxs-lookup"><span data-stu-id="32ccf-174">On hello command line, run `bundle install`.</span></span> <span data-ttu-id="32ccf-175">Teraz otworzyć `web.rb` i, w tym wierszem u góry hello:</span><span class="sxs-lookup"><span data-stu-id="32ccf-175">Now open `web.rb` and including this line at hello top:</span></span>

    require 'twilio-ruby'

<span data-ttu-id="32ccf-176">Wszystko jest teraz gotowe toouse hello usługi Twilio pomocnika biblioteki dla środowiska Ruby w aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="32ccf-176">You're now all set toouse hello Twilio helper library for Ruby in your web app.</span></span>

## <span data-ttu-id="32ccf-177"><a id="howto_make_call"></a>Porady: wykonywanie połączenia wychodzące</span><span class="sxs-lookup"><span data-stu-id="32ccf-177"><a id="howto_make_call"></a>How to: Make an outgoing call</span></span>
<span data-ttu-id="32ccf-178">powitania po pokazuje, jak wywołać toomake wychodzące.</span><span class="sxs-lookup"><span data-stu-id="32ccf-178">hello following shows how toomake an outgoing call.</span></span> <span data-ttu-id="32ccf-179">Kluczowe założenia obejmują przy użyciu biblioteki Pomocnik usługi Twilio powitania dla toomake dopisków fonetycznych, które wywołuje interfejs API REST i renderowania TwiML.</span><span class="sxs-lookup"><span data-stu-id="32ccf-179">Key concepts include using hello Twilio helper library for Ruby toomake REST API calls and rendering TwiML.</span></span> <span data-ttu-id="32ccf-180">Podstaw wartości hello **z** i **do** numerów telefonów i upewnij się, że sprawdzisz hello **z** numer telefonu dla kodu hello toorunning poprzedniego konta usługi Twilio.</span><span class="sxs-lookup"><span data-stu-id="32ccf-180">Substitute your values for hello **From** and **To** phone numbers, and ensure that you verify hello **From** phone number for your Twilio account prior toorunning hello code.</span></span>

<span data-ttu-id="32ccf-181">Dodaj tę funkcję za`web.md`:</span><span class="sxs-lookup"><span data-stu-id="32ccf-181">Add this function too`web.md`:</span></span>

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

<span data-ttu-id="32ccf-182">Jeśli otwarty up `http://yourdomain.cloudapp.net/make_call` w przeglądarce, która wyzwoli rozmowy telefonicznej hello toomake interfejsu API usługi Twilio hello wywołania toohello.</span><span class="sxs-lookup"><span data-stu-id="32ccf-182">If you open-up `http://yourdomain.cloudapp.net/make_call` in a browser, that will trigger hello call toohello Twilio API toomake hello phone call.</span></span> <span data-ttu-id="32ccf-183">Witaj pierwszych dwóch parametrów w `client.account.calls.create` dość wyjaśnień: numer wywołanie hello hello jest `from` i numer wywołanie hello hello jest `to`.</span><span class="sxs-lookup"><span data-stu-id="32ccf-183">hello first two parameters in `client.account.calls.create` are fairly self-explanatory: hello number hello call is `from` and hello number hello call is `to`.</span></span> 

<span data-ttu-id="32ccf-184">Witaj trzeci parametr (`url`) jest adresem URL hello usługi Twilio żądań instrukcje tooget na jakie toodo, po wywołaniu hello jest połączony.</span><span class="sxs-lookup"><span data-stu-id="32ccf-184">hello third parameter (`url`) is hello URL that Twilio requests tooget instructions on what toodo once hello call is connected.</span></span> <span data-ttu-id="32ccf-185">W tym przypadku firma Microsoft konfiguracji, a adres URL (`http://yourdomain.cloudapp.net`) zwraca prosty dokumentu TwiML i używa hello `<Say>` wywołać toodo zlecenie niektóre tekst na mowę i wypowiedz odbieranie osoby toohello "Hello małp" hello.</span><span class="sxs-lookup"><span data-stu-id="32ccf-185">In this case we set-up a URL (`http://yourdomain.cloudapp.net`) that returns a simple TwiML document and uses hello `<Say>` verb toodo some text-to-speech and say "Hello Monkey" toohello person recieving hello call.</span></span>

## <span data-ttu-id="32ccf-186"><a id="howto_recieve_sms"></a>Porady: Odbierz wiadomość SMS</span><span class="sxs-lookup"><span data-stu-id="32ccf-186"><a id="howto_recieve_sms"></a>How to: Recieve an SMS message</span></span>
<span data-ttu-id="32ccf-187">W poprzednim przykładzie hello możemy zainicjować **wychodzących** rozmowy telefonicznej.</span><span class="sxs-lookup"><span data-stu-id="32ccf-187">In hello previous example we initiated an **outgoing** phone call.</span></span> <span data-ttu-id="32ccf-188">Ten czas, Użyjmy hello numer telefonu, który usługi Twilio podał podczas tworzenia konta tooprocess **przychodzące** wiadomości SMS.</span><span class="sxs-lookup"><span data-stu-id="32ccf-188">This time, let's use hello phone number that Twilio gave us during sign-up tooprocess an **incoming** SMS message.</span></span>

<span data-ttu-id="32ccf-189">Po pierwsze, w dzienniku tooyour [pulpitu nawigacyjnego usługi Twilio][twilio_account].</span><span class="sxs-lookup"><span data-stu-id="32ccf-189">First, log-in tooyour [Twilio dashboard][twilio_account].</span></span> <span data-ttu-id="32ccf-190">Kliknij przycisk "Numery" w górnym nav hello, a następnie kliknij na powitania numer usługi Twilio, które zostały podane.</span><span class="sxs-lookup"><span data-stu-id="32ccf-190">Click on "Numbers" in hello top nav and then click on hello Twilio number you were provided.</span></span> <span data-ttu-id="32ccf-191">Zostanie wyświetlone dwa adresy URL, które można skonfigurować.</span><span class="sxs-lookup"><span data-stu-id="32ccf-191">You'll see two URLs that you can configure.</span></span> <span data-ttu-id="32ccf-192">Adres URL żądania adresie URL żądania głosu i programu SMS.</span><span class="sxs-lookup"><span data-stu-id="32ccf-192">A Voice Request URL and an SMS Request URL.</span></span> <span data-ttu-id="32ccf-193">Są to adresy URL hello, wprowadzone wywołania usługi Twilio, gdy połączenie telefoniczne lub programu SMS są wysyłane tooyour numer.</span><span class="sxs-lookup"><span data-stu-id="32ccf-193">These are hello URLs that Twilio calls whenever a phone call is made or an SMS is sent tooyour number.</span></span> <span data-ttu-id="32ccf-194">adresy URL Hello są również znane jako "punkty zaczepienia sieci web".</span><span class="sxs-lookup"><span data-stu-id="32ccf-194">hello URLs are also known as "web hooks".</span></span>

<span data-ttu-id="32ccf-195">Chcielibyśmy tooprocess przychodzących wiadomości SMS, więc warto aktualizacja adresu URL hello zbyt`http://yourdomain.cloudapp.net/sms_url`.</span><span class="sxs-lookup"><span data-stu-id="32ccf-195">We would like tooprocess incoming SMS messages, so let's update hello URL too`http://yourdomain.cloudapp.net/sms_url`.</span></span> <span data-ttu-id="32ccf-196">Przejdź dalej i kliknij przycisk Zapisz zmiany u dołu hello hello strony.</span><span class="sxs-lookup"><span data-stu-id="32ccf-196">Go ahead and click Save Changes at hello bottom of hello page.</span></span> <span data-ttu-id="32ccf-197">Teraz, ponownie `web.rb` toohandle naszej aplikacji umożliwia programu, to:</span><span class="sxs-lookup"><span data-stu-id="32ccf-197">Now, back in `web.rb` let's program our application toohandle this:</span></span>

    post '/sms_url' do
      "<Response>
         <Message>Hey, thanks for hello ping! Twilio and Azure rock!</Message>
       </Response>"
    end

<span data-ttu-id="32ccf-198">Po wprowadzeniu zmian hello, upewnij się, że początkowy toore aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="32ccf-198">After making hello change, make sure toore-start your web app.</span></span> <span data-ttu-id="32ccf-199">Teraz Wyjmij telefonu i wysyłanie SMS tooyour numer usługi Twilio.</span><span class="sxs-lookup"><span data-stu-id="32ccf-199">Now, take out your phone and send an SMS tooyour Twilio number.</span></span> <span data-ttu-id="32ccf-200">Należy niezwłocznie pobrać odpowiedzi programu SMS z informacją, "Witaj, Dziękujemy za ping Witaj!</span><span class="sxs-lookup"><span data-stu-id="32ccf-200">You should promptly get an SMS response that says "Hey, thanks for hello ping!</span></span> <span data-ttu-id="32ccf-201">Skale usługi Twilio i na platformie Azure! ".</span><span class="sxs-lookup"><span data-stu-id="32ccf-201">Twilio and Azure rock!".</span></span>

## <span data-ttu-id="32ccf-202"><a id="additional_services"></a>Porady: korzystania z usługi Twilio dodatkowych usług</span><span class="sxs-lookup"><span data-stu-id="32ccf-202"><a id="additional_services"></a>How to: Use Additional Twilio Services</span></span>
<span data-ttu-id="32ccf-203">Ponadto przykłady toohello pokazane, usługi Twilio oferuje API sieci web można używać tooleverage dodatkowe usługi Twilio funkcji z aplikacji Azure.</span><span class="sxs-lookup"><span data-stu-id="32ccf-203">In addition toohello examples shown here, Twilio offers web-based APIs that you can use tooleverage additional Twilio functionality from your Azure application.</span></span> <span data-ttu-id="32ccf-204">Aby uzyskać szczegółowe informacje, zobacz hello [dokumentacji interfejsu API usługi Twilio][twilio_api_documentation].</span><span class="sxs-lookup"><span data-stu-id="32ccf-204">For full details, see hello [Twilio API documentation][twilio_api_documentation].</span></span>

### <span data-ttu-id="32ccf-205"><a id="NextSteps"></a>Następne kroki</span><span class="sxs-lookup"><span data-stu-id="32ccf-205"><a id="NextSteps"></a>Next Steps</span></span>
<span data-ttu-id="32ccf-206">Teraz, kiedy znasz już podstawy hello hello usługi usługi Twilio, wykonaj te więcej toolearn łącza:</span><span class="sxs-lookup"><span data-stu-id="32ccf-206">Now that you've learned hello basics of hello Twilio service, follow these links toolearn more:</span></span>

* <span data-ttu-id="32ccf-207">[Wytyczne dotyczące zabezpieczeń usługi Twilio][twilio_security_guidelines]</span><span class="sxs-lookup"><span data-stu-id="32ccf-207">[Twilio Security Guidelines][twilio_security_guidelines]</span></span>
* <span data-ttu-id="32ccf-208">[HowTos usługi Twilio i przykładowy kod][twilio_howtos]</span><span class="sxs-lookup"><span data-stu-id="32ccf-208">[Twilio HowTos and Example Code][twilio_howtos]</span></span>
* <span data-ttu-id="32ccf-209">[Samouczki usługi Twilio Szybki Start][twilio_quickstarts]</span><span class="sxs-lookup"><span data-stu-id="32ccf-209">[Twilio Quickstart Tutorials][twilio_quickstarts]</span></span> 
* <span data-ttu-id="32ccf-210">[Usługi Twilio w witrynie GitHub][twilio_on_github]</span><span class="sxs-lookup"><span data-stu-id="32ccf-210">[Twilio on GitHub][twilio_on_github]</span></span>
* <span data-ttu-id="32ccf-211">[Porozmawiaj tooTwilio pomocy technicznej][twilio_support]</span><span class="sxs-lookup"><span data-stu-id="32ccf-211">[Talk tooTwilio Support][twilio_support]</span></span>

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
