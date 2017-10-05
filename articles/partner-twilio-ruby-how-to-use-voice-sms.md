---
title: "Jak używać usługi Twilio głosowe i programu SMS (Ruby) | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak wykonać połączenie telefoniczne i wysłać wiadomość SMS z usługi interfejsu API usługi Twilio na platformie Azure. Przykłady kodu napisane w języku Ruby."
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
ms.openlocfilehash: 69e50e7fe0e1f302e96c309878b8dea6869dff4a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-twilio-for-voice-and-sms-capabilities-in-ruby"></a><span data-ttu-id="42e3e-104">Jak używać usługi Twilio głosowe i możliwości programu SMS w języku Ruby</span><span class="sxs-lookup"><span data-stu-id="42e3e-104">How to Use Twilio for Voice and SMS Capabilities in Ruby</span></span>
<span data-ttu-id="42e3e-105">W tym przewodniku przedstawiono sposób wykonywania typowych zadań programowania usługi interfejsu API usługi Twilio na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="42e3e-105">This guide demonstrates how to perform common programming tasks with the Twilio API service on Azure.</span></span> <span data-ttu-id="42e3e-106">Omówione scenariusze obejmują tworzenie połączeń telefonicznych i wysyłanie wiadomości krótką wiadomość usługi (SMS).</span><span class="sxs-lookup"><span data-stu-id="42e3e-106">The scenarios covered include making a phone call and sending a Short Message Service (SMS) message.</span></span> <span data-ttu-id="42e3e-107">Aby uzyskać więcej informacji na temat usługi Twilio i komunikacja głosowa programu SMS w aplikacji, zobacz [następne kroki](#NextSteps) sekcji.</span><span class="sxs-lookup"><span data-stu-id="42e3e-107">For more information on Twilio and using voice and SMS in your applications, see the [Next Steps](#NextSteps) section.</span></span>

## <span data-ttu-id="42e3e-108"><a id="WhatIs"></a>Co to jest usługi Twilio?</span><span class="sxs-lookup"><span data-stu-id="42e3e-108"><a id="WhatIs"></a>What is Twilio?</span></span>
<span data-ttu-id="42e3e-109">Usługi Twilio jest interfejs API usługi sieci web telefonii, które umożliwia tworzenie aplikacji programu SMS i komunikacja głosowa przy użyciu istniejących języków sieci web i umiejętności.</span><span class="sxs-lookup"><span data-stu-id="42e3e-109">Twilio is a telephony web-service API that lets you use your existing web languages and skills to build voice and SMS applications.</span></span> <span data-ttu-id="42e3e-110">Usługi Twilio jest usługą innych firm (nie funkcji platformy Azure i nie produkt firmy Microsoft).</span><span class="sxs-lookup"><span data-stu-id="42e3e-110">Twilio is a third-party service (not an Azure feature and not a Microsoft product).</span></span>

<span data-ttu-id="42e3e-111">**Usługi Twilio głosu** umożliwia aplikacjom wykonywanie i odbieranie połączeń telefonicznych.</span><span class="sxs-lookup"><span data-stu-id="42e3e-111">**Twilio Voice** allows your applications to make and receive phone calls.</span></span> <span data-ttu-id="42e3e-112">**SMS usługi Twilio** umożliwia aplikacjom wykonywanie i odbieranie wiadomości SMS.</span><span class="sxs-lookup"><span data-stu-id="42e3e-112">**Twilio SMS** allows your applications to make and receive SMS messages.</span></span> <span data-ttu-id="42e3e-113">**Klient usługi Twilio** umożliwia aplikacjom włączyć komunikację głosową, przy użyciu istniejących połączeń internetowych, w tym przenośnych połączenia.</span><span class="sxs-lookup"><span data-stu-id="42e3e-113">**Twilio Client** allows your applications to enable voice communication using existing Internet connections, including mobile connections.</span></span>

## <span data-ttu-id="42e3e-114"><a id="Pricing"></a>Cennik usługi Twilio i oferty specjalne</span><span class="sxs-lookup"><span data-stu-id="42e3e-114"><a id="Pricing"></a>Twilio Pricing and Special Offers</span></span>
<span data-ttu-id="42e3e-115">Informacje o cenach usługi Twilio znajduje się w temacie [cennik usługi Twilio][twilio_pricing].</span><span class="sxs-lookup"><span data-stu-id="42e3e-115">Information about Twilio pricing is available at [Twilio Pricing][twilio_pricing].</span></span> <span data-ttu-id="42e3e-116">Azure klienci otrzymają [oferta specjalna][special_offer]: wolnego środki tekstów 1000 lub 1000 ruchu przychodzącego minut.</span><span class="sxs-lookup"><span data-stu-id="42e3e-116">Azure customers receive a [special offer][special_offer]: a free credit of 1000 texts or 1000 inbound minutes.</span></span> <span data-ttu-id="42e3e-117">Zapisz się do tej oferty lub uzyskać więcej informacji, odwiedź [http://ahoy.twilio.com/azure][special_offer].</span><span class="sxs-lookup"><span data-stu-id="42e3e-117">To sign up for this offer or get more information, please visit [http://ahoy.twilio.com/azure][special_offer].</span></span>  

## <span data-ttu-id="42e3e-118"><a id="Concepts"></a>Pojęcia</span><span class="sxs-lookup"><span data-stu-id="42e3e-118"><a id="Concepts"></a>Concepts</span></span>
<span data-ttu-id="42e3e-119">Interfejs API usługi Twilio jest interfejs API RESTful, która zapewnia funkcje programu SMS i komunikacja głosowa aplikacji.</span><span class="sxs-lookup"><span data-stu-id="42e3e-119">The Twilio API is a RESTful API that provides voice and SMS functionality for applications.</span></span> <span data-ttu-id="42e3e-120">Klient biblioteki są dostępne w wielu językach; Aby uzyskać listę, zobacz [bibliotek interfejsu API usługi Twilio][twilio_libraries].</span><span class="sxs-lookup"><span data-stu-id="42e3e-120">Client libraries are available in multiple languages; for a list, see [Twilio API Libraries][twilio_libraries].</span></span>

### <span data-ttu-id="42e3e-121"><a id="TwiML"></a>TwiML</span><span class="sxs-lookup"><span data-stu-id="42e3e-121"><a id="TwiML"></a>TwiML</span></span>
<span data-ttu-id="42e3e-122">TwiML to zestaw instrukcji oparte na języku XML, które informują usługi Twilio sposobu przetwarzania połączenia lub wiadomości SMS.</span><span class="sxs-lookup"><span data-stu-id="42e3e-122">TwiML is a set of XML-based instructions that inform Twilio of how to process a call or SMS.</span></span>

<span data-ttu-id="42e3e-123">Na przykład następujące TwiML czy Konwertuj tekst **Hello World** do rozpoznawania mowy.</span><span class="sxs-lookup"><span data-stu-id="42e3e-123">As an example, the following TwiML would convert the text **Hello World** to speech.</span></span>

    <?xml version="1.0" encoding="UTF-8" ?>
    <Response>
       <Say>Hello World</Say>
    </Response>

<span data-ttu-id="42e3e-124">Wszystkie dokumenty TwiML mają `<Response>` jako ich elementu głównego.</span><span class="sxs-lookup"><span data-stu-id="42e3e-124">All TwiML documents have `<Response>` as their root element.</span></span> <span data-ttu-id="42e3e-125">Dostępne usługi Twilio zleceń służą do definiowania zachowania aplikacji.</span><span class="sxs-lookup"><span data-stu-id="42e3e-125">From there, you use Twilio Verbs to define the behavior of your application.</span></span>

### <span data-ttu-id="42e3e-126"><a id="Verbs"></a>TwiML zlecenia</span><span class="sxs-lookup"><span data-stu-id="42e3e-126"><a id="Verbs"></a>TwiML Verbs</span></span>
<span data-ttu-id="42e3e-127">Usługi Twilio zlecenia są tagi XML, które informują usługi Twilio, co **czy**.</span><span class="sxs-lookup"><span data-stu-id="42e3e-127">Twilio Verbs are XML tags that tell Twilio what to **do**.</span></span> <span data-ttu-id="42e3e-128">Na przykład  **&lt;powiedzieć&gt;**  zlecenie powoduje, że usługi Twilio komputerowi dostarczenia komunikatu w wywołaniu.</span><span class="sxs-lookup"><span data-stu-id="42e3e-128">For example, the **&lt;Say&gt;** verb instructs Twilio to audibly deliver a message on a call.</span></span> 

<span data-ttu-id="42e3e-129">Poniżej znajduje się lista zleceń usługi Twilio.</span><span class="sxs-lookup"><span data-stu-id="42e3e-129">The following is a list of Twilio verbs.</span></span>

* <span data-ttu-id="42e3e-130">**&lt;Wybierania&gt;**: łączy wywołującego innego numeru telefonu.</span><span class="sxs-lookup"><span data-stu-id="42e3e-130">**&lt;Dial&gt;**: Connects the caller to another phone.</span></span>
* <span data-ttu-id="42e3e-131">**&lt;Zbierz&gt;**: zbiera cyfry wprowadzone na klawiaturze telefonu.</span><span class="sxs-lookup"><span data-stu-id="42e3e-131">**&lt;Gather&gt;**: Collects numeric digits entered on the telephone keypad.</span></span>
* <span data-ttu-id="42e3e-132">**&lt;Rozłączanie&gt;**: kończy wywołanie.</span><span class="sxs-lookup"><span data-stu-id="42e3e-132">**&lt;Hangup&gt;**: Ends a call.</span></span>
* <span data-ttu-id="42e3e-133">**&lt;Odtwórz&gt;**: odtwarzania pliku audio.</span><span class="sxs-lookup"><span data-stu-id="42e3e-133">**&lt;Play&gt;**: Plays an audio file.</span></span>
* <span data-ttu-id="42e3e-134">**&lt;Wstrzymaj&gt;**: dyskretnie czeka na określoną liczbę sekund.</span><span class="sxs-lookup"><span data-stu-id="42e3e-134">**&lt;Pause&gt;**: Waits silently for a specified number of seconds.</span></span>
* <span data-ttu-id="42e3e-135">**&lt;Rekord&gt;**: rejestruje wywołującego głosu i zwraca adres URL pliku zawierającego nagrywania.</span><span class="sxs-lookup"><span data-stu-id="42e3e-135">**&lt;Record&gt;**: Records the caller's voice and returns a URL of a file that contains the recording.</span></span>
* <span data-ttu-id="42e3e-136">**&lt;Przekieruj&gt;**: przekazuje kontrolę nad wywołania lub wiadomości SMS do TwiML na inny adres URL.</span><span class="sxs-lookup"><span data-stu-id="42e3e-136">**&lt;Redirect&gt;**: Transfers control of a call or SMS to the TwiML at a different URL.</span></span>
* <span data-ttu-id="42e3e-137">**&lt;Odrzuć&gt;**: odrzucanie połączenia przychodzącego na numer usługi Twilio bez rozliczeń można</span><span class="sxs-lookup"><span data-stu-id="42e3e-137">**&lt;Reject&gt;**: Rejects an incoming call to your Twilio number without billing you</span></span>
* <span data-ttu-id="42e3e-138">**&lt;Powiedz&gt;**: Konwertuje tekst na mowę, które zostało utworzone w wywołaniu.</span><span class="sxs-lookup"><span data-stu-id="42e3e-138">**&lt;Say&gt;**: Converts text to speech that is made on a call.</span></span>
* <span data-ttu-id="42e3e-139">**&lt;SMS&gt;**: wysyła wiadomość SMS.</span><span class="sxs-lookup"><span data-stu-id="42e3e-139">**&lt;Sms&gt;**: Sends an SMS message.</span></span>

<span data-ttu-id="42e3e-140">Aby uzyskać więcej informacji na temat usługi Twilio zlecenia i ich atrybuty oraz TwiML, zobacz [TwiML][twiml].</span><span class="sxs-lookup"><span data-stu-id="42e3e-140">For more information about Twilio verbs, their attributes, and TwiML, see [TwiML][twiml].</span></span> <span data-ttu-id="42e3e-141">Aby uzyskać dodatkowe informacje na temat interfejsu API usługi Twilio, zobacz [interfejsu API usługi Twilio][twilio_api].</span><span class="sxs-lookup"><span data-stu-id="42e3e-141">For additional information about the Twilio API, see [Twilio API][twilio_api].</span></span>

## <span data-ttu-id="42e3e-142"><a id="CreateAccount"></a>Tworzenie konta usługi Twilio</span><span class="sxs-lookup"><span data-stu-id="42e3e-142"><a id="CreateAccount"></a>Create a Twilio Account</span></span>
<span data-ttu-id="42e3e-143">Po przygotowaniu można uzyskać konta usługi Twilio, zarejestruj się w [spróbuj usługi Twilio][try_twilio].</span><span class="sxs-lookup"><span data-stu-id="42e3e-143">When you're ready to get a Twilio account, sign up at [Try Twilio][try_twilio].</span></span> <span data-ttu-id="42e3e-144">Można rozpoczynać bezpłatne konto, a następnie Uaktualnij swoje konto później.</span><span class="sxs-lookup"><span data-stu-id="42e3e-144">You can start with a free account, and upgrade your account later.</span></span>

<span data-ttu-id="42e3e-145">Po utworzeniu konta dla konta usługi Twilio, otrzymasz numer telefonu bezpłatnej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="42e3e-145">When you sign up for a Twilio account, you'll get a free phone number for your application.</span></span> <span data-ttu-id="42e3e-146">Otrzymasz również identyfikatora SID konta, a token uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="42e3e-146">You'll also receive an account SID and an auth token.</span></span> <span data-ttu-id="42e3e-147">Zarówno będą potrzebne w celu wykonywania wywołań interfejsu API usługi Twilio.</span><span class="sxs-lookup"><span data-stu-id="42e3e-147">Both will be needed to make Twilio API calls.</span></span> <span data-ttu-id="42e3e-148">Aby uniemożliwić nieautoryzowany dostęp do Twojego konta, bezpieczeństwo Twojego tokenu uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="42e3e-148">To prevent unauthorized access to your account, keep your authentication token secure.</span></span> <span data-ttu-id="42e3e-149">Identyfikator SID konta, a token uwierzytelniania jest wyświetlana w [strony konta usługi Twilio][twilio_account], w polach etykietą **identyfikator SID konta** i **TOKEN uwierzytelniania**odpowiednio.</span><span class="sxs-lookup"><span data-stu-id="42e3e-149">Your account SID and auth token are viewable at the [Twilio account page][twilio_account], in the fields labeled **ACCOUNT SID** and **AUTH TOKEN**, respectively.</span></span>

### <span data-ttu-id="42e3e-150"><a id="VerifyPhoneNumbers"></a>Sprawdź numery telefonów</span><span class="sxs-lookup"><span data-stu-id="42e3e-150"><a id="VerifyPhoneNumbers"></a>Verify Phone Numbers</span></span>
<span data-ttu-id="42e3e-151">Oprócz numer podano przez usługi Twilio, można również sprawdzić numery skonfigurujesz kontrolowaną (np. telefon komórkowy lub głównej numer telefonu) do użycia w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="42e3e-151">In addition to the number you are given by Twilio, you can also verify numbers that you control (i.e. your cell phone or home phone number) for use in your applications.</span></span> 

<span data-ttu-id="42e3e-152">Aby uzyskać informacje o zweryfikowanie numeru telefonu, zobacz [Zarządzanie numery][verify_phone].</span><span class="sxs-lookup"><span data-stu-id="42e3e-152">For information on how to verify a phone number, see [Manage Numbers][verify_phone].</span></span>

## <span data-ttu-id="42e3e-153"><a id="create_app"></a>Tworzenie aplikacji Ruby</span><span class="sxs-lookup"><span data-stu-id="42e3e-153"><a id="create_app"></a>Create a Ruby Application</span></span>
<span data-ttu-id="42e3e-154">Nie różni się od innych dopisków fonetycznych aplikację korzystającą z usługi Twilio usługi się dopisków fonetycznych aplikacji, która używa usługi usługi Twilio i działa na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="42e3e-154">A Ruby application that uses the Twilio service and is running in Azure is no different than any other Ruby application that uses the Twilio service.</span></span> <span data-ttu-id="42e3e-155">Usługi Twilio usług są RESTful i może zostać wywołana z Ruby na kilka sposobów, w tym artykule dotyczą sposobu korzystania z usługi Twilio usług w programie [usługi Twilio biblioteki pomocnika dla środowiska Ruby][twilio_ruby].</span><span class="sxs-lookup"><span data-stu-id="42e3e-155">While Twilio services are RESTful and can be called from Ruby in several ways, this article will focus on how to use Twilio services with [Twilio helper library for Ruby][twilio_ruby].</span></span>

<span data-ttu-id="42e3e-156">Najpierw [konfiguracji nowej maszyny Wirtualnej systemu Linux Azure] [ azure_vm_setup] do działania jako hosta dla nowej aplikacji sieci web dopisków fonetycznych.</span><span class="sxs-lookup"><span data-stu-id="42e3e-156">First, [set-up a new Azure Linux VM][azure_vm_setup] to act as a host for your new Ruby web application.</span></span> <span data-ttu-id="42e3e-157">Pomiń kroki dotyczące tworzenia aplikacji szyny, po prostu konfiguracji maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="42e3e-157">Ignore the steps involving the creation of a Rails app, just set-up the VM.</span></span> <span data-ttu-id="42e3e-158">Upewnij się, że utworzono punkt końcowy z zewnętrznego portu 80 i wewnętrzny port 5000.</span><span class="sxs-lookup"><span data-stu-id="42e3e-158">Make sure you create an Endpoint with an external port of 80 and an internal port of 5000.</span></span>

<span data-ttu-id="42e3e-159">W poniższych przykładach użyjemy [Sinatra][sinatra], ramy bardzo proste sieci web dla środowiska Ruby.</span><span class="sxs-lookup"><span data-stu-id="42e3e-159">In the examples below, we will be using [Sinatra][sinatra], a very simple web framework for Ruby.</span></span> <span data-ttu-id="42e3e-160">Ale pewnością służy biblioteki Pomocnik usługi Twilio dla środowiska Ruby z żadnych innych platforma sieci web, w tym Ruby na szyny.</span><span class="sxs-lookup"><span data-stu-id="42e3e-160">But you can certainly use the Twilio helper library for Ruby with any other web framework, including Ruby on Rails.</span></span>

<span data-ttu-id="42e3e-161">SSH do nowej maszyny Wirtualnej i Utwórz katalog dla nowej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="42e3e-161">SSH into your new VM and create a directory for your new app.</span></span> <span data-ttu-id="42e3e-162">W tym katalogu Utwórz plik o nazwie Gemfile i skopiuj do niego następujący kod:</span><span class="sxs-lookup"><span data-stu-id="42e3e-162">Inside that directory, create a file called Gemfile and copy the following code into it:</span></span>

    source 'https://rubygems.org'
    gem 'sinatra'
    gem 'thin'

<span data-ttu-id="42e3e-163">W wierszu polecenia Uruchom `bundle install`.</span><span class="sxs-lookup"><span data-stu-id="42e3e-163">On the command line run `bundle install`.</span></span> <span data-ttu-id="42e3e-164">Spowoduje to zainstalowanie zależności powyżej.</span><span class="sxs-lookup"><span data-stu-id="42e3e-164">This will install the dependencies above.</span></span> <span data-ttu-id="42e3e-165">Następnie utwórz plik o nazwie `web.rb`.</span><span class="sxs-lookup"><span data-stu-id="42e3e-165">Next create a file called `web.rb`.</span></span> <span data-ttu-id="42e3e-166">Są to, gdzie znajduje się kod aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="42e3e-166">This will be where the code for your web app lives.</span></span> <span data-ttu-id="42e3e-167">Wklej następujący kod do niej:</span><span class="sxs-lookup"><span data-stu-id="42e3e-167">Paste the following code into it:</span></span>

    require 'sinatra'

    get '/' do
        "Hello Monkey!"
    end

<span data-ttu-id="42e3e-168">W tym momencie powinno być możliwe uruchomienie polecenia `ruby web.rb -p 5000`.</span><span class="sxs-lookup"><span data-stu-id="42e3e-168">At this point you should be able the run the command `ruby web.rb -p 5000`.</span></span> <span data-ttu-id="42e3e-169">To spowoduje rozkręcenia serwera sieci web małej na port 5000.</span><span class="sxs-lookup"><span data-stu-id="42e3e-169">This will spin-up a small web server on port 5000.</span></span> <span data-ttu-id="42e3e-170">Można będzie przejdź do tej aplikacji w przeglądarce, przechodząc na stronę adres URL należy konfiguracji maszyny Wirtualnej Azure.</span><span class="sxs-lookup"><span data-stu-id="42e3e-170">You should be able to browse to this app in your browser by visiting the URL you set-up for your Azure VM.</span></span> <span data-ttu-id="42e3e-171">Gdy aplikacja sieci web w przeglądarce może nawiązać połączenie, możesz rozpocząć tworzenie aplikacji usługi Twilio.</span><span class="sxs-lookup"><span data-stu-id="42e3e-171">Once you can reach your web app in the browser, you're ready to start building a Twilio app.</span></span>

## <span data-ttu-id="42e3e-172"><a id="configure_app"></a>Skonfigurować aplikację do używania usługi Twilio</span><span class="sxs-lookup"><span data-stu-id="42e3e-172"><a id="configure_app"></a>Configure Your Application to Use Twilio</span></span>
<span data-ttu-id="42e3e-173">Można skonfigurować aplikację sieci web do korzystania z biblioteki usługi Twilio, aktualizując Twojej `Gemfile` do uwzględnienia w tym wierszu:</span><span class="sxs-lookup"><span data-stu-id="42e3e-173">You can configure your web app to use the Twilio library by updating your `Gemfile` to include this line:</span></span>

    gem 'twilio-ruby'

<span data-ttu-id="42e3e-174">W wierszu polecenia Uruchom `bundle install`.</span><span class="sxs-lookup"><span data-stu-id="42e3e-174">On the command line, run `bundle install`.</span></span> <span data-ttu-id="42e3e-175">Teraz otworzyć `web.rb` i ten wiersz na początku, w tym:</span><span class="sxs-lookup"><span data-stu-id="42e3e-175">Now open `web.rb` and including this line at the top:</span></span>

    require 'twilio-ruby'

<span data-ttu-id="42e3e-176">Teraz wszystko jest gotowe do korzystania z usługi Twilio pomocnika biblioteki dla środowiska Ruby w aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="42e3e-176">You're now all set to use the Twilio helper library for Ruby in your web app.</span></span>

## <span data-ttu-id="42e3e-177"><a id="howto_make_call"></a>Porady: wykonywanie połączenia wychodzące</span><span class="sxs-lookup"><span data-stu-id="42e3e-177"><a id="howto_make_call"></a>How to: Make an outgoing call</span></span>
<span data-ttu-id="42e3e-178">Poniżej przedstawiono sposób wywoływania wychodzących.</span><span class="sxs-lookup"><span data-stu-id="42e3e-178">The following shows how to make an outgoing call.</span></span> <span data-ttu-id="42e3e-179">Kluczowe założenia obejmują za pomocą usługi Twilio biblioteki pomocnika dla środowiska Ruby do wykonywania wywołań interfejsu API REST i renderowania TwiML.</span><span class="sxs-lookup"><span data-stu-id="42e3e-179">Key concepts include using the Twilio helper library for Ruby to make REST API calls and rendering TwiML.</span></span> <span data-ttu-id="42e3e-180">Podstaw wartości **z** i **do** numerów telefonów i upewnij się, że sprawdzisz **z** numer telefonu dla konta usługi Twilio przed uruchomieniem kodu.</span><span class="sxs-lookup"><span data-stu-id="42e3e-180">Substitute your values for the **From** and **To** phone numbers, and ensure that you verify the **From** phone number for your Twilio account prior to running the code.</span></span>

<span data-ttu-id="42e3e-181">Dodaj tę funkcję, aby `web.md`:</span><span class="sxs-lookup"><span data-stu-id="42e3e-181">Add this function to `web.md`:</span></span>

    # Set your account ID and authentication token.
    sid = "your_twilio_account_sid";
    token = "your_twilio_authentication_token";

    # The number of the phone initiating the the call.
    # This should either be a Twilio number or a number that you've verified
    from = "NNNNNNNNNNN";

    # The number of the phone receiving call.
    to = "NNNNNNNNNNN";

    # Use the Twilio-provided site for the TwiML response.
    url = "http://yourdomain.cloudapp.net/voice_url";

    get '/make_call' do
      # Create the call client.
      client = Twilio::REST::Client.new(sid, token);

      # Make the call
      client.account.calls.create(to: to, from: from, url: url)
    end

    post '/voice_url' do
      "<Response>
         <Say>Hello Monkey!</Say>
       </Response>"
    end

<span data-ttu-id="42e3e-182">Jeśli otwarty up `http://yourdomain.cloudapp.net/make_call` w przeglądarce, która wyzwoli wywołanie interfejsu API usługi Twilio rozmowę telefoniczną.</span><span class="sxs-lookup"><span data-stu-id="42e3e-182">If you open-up `http://yourdomain.cloudapp.net/make_call` in a browser, that will trigger the call to the Twilio API to make the phone call.</span></span> <span data-ttu-id="42e3e-183">Pierwsze dwa parametry w `client.account.calls.create` dość wyjaśnień: liczba wywołanie jest `from` i liczba wywołanie jest `to`.</span><span class="sxs-lookup"><span data-stu-id="42e3e-183">The first two parameters in `client.account.calls.create` are fairly self-explanatory: the number the call is `from` and the number the call is `to`.</span></span> 

<span data-ttu-id="42e3e-184">Trzeci parametr (`url`) jest adres URL, który żąda usługi Twilio, aby uzyskać instrukcje, co należy zrobić po wywołaniu jest połączony.</span><span class="sxs-lookup"><span data-stu-id="42e3e-184">The third parameter (`url`) is the URL that Twilio requests to get instructions on what to do once the call is connected.</span></span> <span data-ttu-id="42e3e-185">W tym przypadku firma Microsoft konfiguracji, a adres URL (`http://yourdomain.cloudapp.net`) zwraca prosty dokumentu TwiML i używa `<Say>` zlecenie czy niektóre tekst na mowę i wypowiedz "Hello małp" osobie odbierającej wywołania.</span><span class="sxs-lookup"><span data-stu-id="42e3e-185">In this case we set-up a URL (`http://yourdomain.cloudapp.net`) that returns a simple TwiML document and uses the `<Say>` verb to do some text-to-speech and say "Hello Monkey" to the person recieving the call.</span></span>

## <span data-ttu-id="42e3e-186"><a id="howto_recieve_sms"></a>Porady: Odbierz wiadomość SMS</span><span class="sxs-lookup"><span data-stu-id="42e3e-186"><a id="howto_recieve_sms"></a>How to: Recieve an SMS message</span></span>
<span data-ttu-id="42e3e-187">W poprzednim przykładzie mamy zainicjowano **wychodzących** rozmowy telefonicznej.</span><span class="sxs-lookup"><span data-stu-id="42e3e-187">In the previous example we initiated an **outgoing** phone call.</span></span> <span data-ttu-id="42e3e-188">Tego czasu, można użyć numer telefonu, który usługi Twilio podał podczas tworzenia konta do procesu **przychodzące** wiadomości SMS.</span><span class="sxs-lookup"><span data-stu-id="42e3e-188">This time, let's use the phone number that Twilio gave us during sign-up to process an **incoming** SMS message.</span></span>

<span data-ttu-id="42e3e-189">Po pierwsze, zaloguj się do Twojego [pulpitu nawigacyjnego usługi Twilio][twilio_account].</span><span class="sxs-lookup"><span data-stu-id="42e3e-189">First, log-in to your [Twilio dashboard][twilio_account].</span></span> <span data-ttu-id="42e3e-190">Kliknij przycisk "Numery" w górnym nav, a następnie kliknij przycisk z liczbą usługi Twilio, które zostały podane.</span><span class="sxs-lookup"><span data-stu-id="42e3e-190">Click on "Numbers" in the top nav and then click on the Twilio number you were provided.</span></span> <span data-ttu-id="42e3e-191">Zostanie wyświetlone dwa adresy URL, które można skonfigurować.</span><span class="sxs-lookup"><span data-stu-id="42e3e-191">You'll see two URLs that you can configure.</span></span> <span data-ttu-id="42e3e-192">Adres URL żądania adresie URL żądania głosu i programu SMS.</span><span class="sxs-lookup"><span data-stu-id="42e3e-192">A Voice Request URL and an SMS Request URL.</span></span> <span data-ttu-id="42e3e-193">Są to adresy URL, które wywołuje usługi Twilio, zawsze, gdy nawiązuje połączenie telefoniczne lub programu SMS są wysyłane na numer.</span><span class="sxs-lookup"><span data-stu-id="42e3e-193">These are the URLs that Twilio calls whenever a phone call is made or an SMS is sent to your number.</span></span> <span data-ttu-id="42e3e-194">Adresy URL są również znane jako "punkty zaczepienia sieci web".</span><span class="sxs-lookup"><span data-stu-id="42e3e-194">The URLs are also known as "web hooks".</span></span>

<span data-ttu-id="42e3e-195">Chcielibyśmy przetwarza przychodzące wiadomości SMS, więc warto aktualizacja adresu URL do `http://yourdomain.cloudapp.net/sms_url`.</span><span class="sxs-lookup"><span data-stu-id="42e3e-195">We would like to process incoming SMS messages, so let's update the URL to `http://yourdomain.cloudapp.net/sms_url`.</span></span> <span data-ttu-id="42e3e-196">Przejdź dalej i kliknij przycisk Zapisz zmiany w dolnej części strony.</span><span class="sxs-lookup"><span data-stu-id="42e3e-196">Go ahead and click Save Changes at the bottom of the page.</span></span> <span data-ttu-id="42e3e-197">Teraz, ponownie `web.rb` teraz program naszą aplikację do obsługi to:</span><span class="sxs-lookup"><span data-stu-id="42e3e-197">Now, back in `web.rb` let's program our application to handle this:</span></span>

    post '/sms_url' do
      "<Response>
         <Message>Hey, thanks for the ping! Twilio and Azure rock!</Message>
       </Response>"
    end

<span data-ttu-id="42e3e-198">Po wprowadzeniu zmian, upewnij się ponownie uruchomić aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="42e3e-198">After making the change, make sure to re-start your web app.</span></span> <span data-ttu-id="42e3e-199">Teraz Wyjmij telefonu i Wyślij wiadomość SMS na numer usługi Twilio.</span><span class="sxs-lookup"><span data-stu-id="42e3e-199">Now, take out your phone and send an SMS to your Twilio number.</span></span> <span data-ttu-id="42e3e-200">Należy niezwłocznie pobrać odpowiedzi programu SMS z informacją, "Witaj, Dziękujemy ping!</span><span class="sxs-lookup"><span data-stu-id="42e3e-200">You should promptly get an SMS response that says "Hey, thanks for the ping!</span></span> <span data-ttu-id="42e3e-201">Skale usługi Twilio i na platformie Azure! ".</span><span class="sxs-lookup"><span data-stu-id="42e3e-201">Twilio and Azure rock!".</span></span>

## <span data-ttu-id="42e3e-202"><a id="additional_services"></a>Porady: korzystania z usługi Twilio dodatkowych usług</span><span class="sxs-lookup"><span data-stu-id="42e3e-202"><a id="additional_services"></a>How to: Use Additional Twilio Services</span></span>
<span data-ttu-id="42e3e-203">Oprócz przykładach pokazano poniżej usługi Twilio oferuje opartych na sieci web interfejsów API, które można wykorzystać dodatkowych funkcji usługi Twilio z aplikacji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="42e3e-203">In addition to the examples shown here, Twilio offers web-based APIs that you can use to leverage additional Twilio functionality from your Azure application.</span></span> <span data-ttu-id="42e3e-204">Aby uzyskać szczegółowe informacje, zobacz [dokumentacji interfejsu API usługi Twilio][twilio_api_documentation].</span><span class="sxs-lookup"><span data-stu-id="42e3e-204">For full details, see the [Twilio API documentation][twilio_api_documentation].</span></span>

### <span data-ttu-id="42e3e-205"><a id="NextSteps"></a>Następne kroki</span><span class="sxs-lookup"><span data-stu-id="42e3e-205"><a id="NextSteps"></a>Next Steps</span></span>
<span data-ttu-id="42e3e-206">Teraz, kiedy znasz już podstawy usługi usługi Twilio, skorzystaj z poniższych linków, aby dowiedzieć się więcej:</span><span class="sxs-lookup"><span data-stu-id="42e3e-206">Now that you've learned the basics of the Twilio service, follow these links to learn more:</span></span>

* <span data-ttu-id="42e3e-207">[Wytyczne dotyczące zabezpieczeń usługi Twilio][twilio_security_guidelines]</span><span class="sxs-lookup"><span data-stu-id="42e3e-207">[Twilio Security Guidelines][twilio_security_guidelines]</span></span>
* <span data-ttu-id="42e3e-208">[HowTos usługi Twilio i przykładowy kod][twilio_howtos]</span><span class="sxs-lookup"><span data-stu-id="42e3e-208">[Twilio HowTos and Example Code][twilio_howtos]</span></span>
* <span data-ttu-id="42e3e-209">[Samouczki usługi Twilio Szybki Start][twilio_quickstarts]</span><span class="sxs-lookup"><span data-stu-id="42e3e-209">[Twilio Quickstart Tutorials][twilio_quickstarts]</span></span> 
* <span data-ttu-id="42e3e-210">[Usługi Twilio w witrynie GitHub][twilio_on_github]</span><span class="sxs-lookup"><span data-stu-id="42e3e-210">[Twilio on GitHub][twilio_on_github]</span></span>
* <span data-ttu-id="42e3e-211">[Zwróć się do pomocy technicznej usługi Twilio][twilio_support]</span><span class="sxs-lookup"><span data-stu-id="42e3e-211">[Talk to Twilio Support][twilio_support]</span></span>

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
