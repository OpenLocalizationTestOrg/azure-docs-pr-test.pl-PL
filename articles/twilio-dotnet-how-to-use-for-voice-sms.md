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
# <a name="how-toouse-twilio-for-voice-and-sms-capabilities-from-azure"></a><span data-ttu-id="78df2-104">Jak toouse usługi Twilio głosowe i możliwości programu SMS z platformy Azure</span><span class="sxs-lookup"><span data-stu-id="78df2-104">How toouse Twilio for voice and SMS capabilities from Azure</span></span>
<span data-ttu-id="78df2-105">W tym przewodniku pokazano, jak tooperform typowych zadań programowania hello interfejsu API usługi Twilio usługi na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="78df2-105">This guide demonstrates how tooperform common programming tasks with hello Twilio API service on Azure.</span></span> <span data-ttu-id="78df2-106">omówione scenariusze Hello obejmują tworzenie połączeń telefonicznych i wysyłanie wiadomości krótką wiadomość usługi (SMS).</span><span class="sxs-lookup"><span data-stu-id="78df2-106">hello scenarios covered include making a phone call and sending a Short Message Service (SMS) message.</span></span> <span data-ttu-id="78df2-107">Aby uzyskać więcej informacji na temat usługi Twilio i komunikacja głosowa programu SMS w aplikacji, zobacz hello [następne kroki](#NextSteps) sekcji.</span><span class="sxs-lookup"><span data-stu-id="78df2-107">For more information on Twilio and using voice and SMS in your applications, see hello [Next steps](#NextSteps) section.</span></span>

## <span data-ttu-id="78df2-108"><a id="WhatIs"></a>Co to jest usługi Twilio?</span><span class="sxs-lookup"><span data-stu-id="78df2-108"><a id="WhatIs"></a>What is Twilio?</span></span>
<span data-ttu-id="78df2-109">Usługi Twilio jest włączanie hello przyszłych komunikacji biznesowej, włączanie deweloperzy tooembed głosu VoIP i wiadomości do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="78df2-109">Twilio is powering hello future of business communications, enabling developers tooembed voice, VoIP, and messaging into applications.</span></span> <span data-ttu-id="78df2-110">Zwirtualizuj one wszystkich infrastrukturę potrzebną w środowisku chmury, globalnych ujawnienie go za pośrednictwem platformy hello API komunikacji usługi Twilio.</span><span class="sxs-lookup"><span data-stu-id="78df2-110">They virtualize all infrastructure needed in a cloud-based, global environment, exposing it through hello Twilio communications API platform.</span></span> <span data-ttu-id="78df2-111">Aplikacje są proste toobuild i skalowalność.</span><span class="sxs-lookup"><span data-stu-id="78df2-111">Applications are simple toobuild and scalable.</span></span> <span data-ttu-id="78df2-112">Kredyty elastyczność z płatność za rzeczywiste użycie ceny i korzystać z niej niezawodności chmury.</span><span class="sxs-lookup"><span data-stu-id="78df2-112">Enjoy flexibility with pay-as-you-go pricing, and benefit from cloud reliability.</span></span>

<span data-ttu-id="78df2-113">**Usługi Twilio głosu** umożliwia toomake Twojej aplikacji i odbieranie połączeń telefonicznych.</span><span class="sxs-lookup"><span data-stu-id="78df2-113">**Twilio Voice** allows your applications toomake and receive phone calls.</span></span> <span data-ttu-id="78df2-114">**SMS usługi Twilio** umożliwia toosend Twojej aplikacji i odbieranie wiadomości SMS.</span><span class="sxs-lookup"><span data-stu-id="78df2-114">**Twilio SMS** enables your applications toosend and receive SMS messages.</span></span> <span data-ttu-id="78df2-115">**Klient usługi Twilio** pozwala toomake VoIP wywołania z dowolnego telefonu, tabletu lub przeglądarki i obsługuje WebRTC.</span><span class="sxs-lookup"><span data-stu-id="78df2-115">**Twilio Client** allows you toomake VoIP calls from any phone, tablet, or browser and supports WebRTC.</span></span>

## <span data-ttu-id="78df2-116"><a id="Pricing"></a>Cennik usługi Twilio i oferty specjalne</span><span class="sxs-lookup"><span data-stu-id="78df2-116"><a id="Pricing"></a>Twilio Pricing and Special Offers</span></span>
<span data-ttu-id="78df2-117">Azure klienci otrzymają [oferta specjalna](http://www.twilio.com/azure): bezpłatnych 10 środków usługi Twilio po uaktualnieniu konta usługi Twilio.</span><span class="sxs-lookup"><span data-stu-id="78df2-117">Azure customers receive a [special offer](http://www.twilio.com/azure): complimentary $10 of Twilio Credit when you upgrade your Twilio Account.</span></span> <span data-ttu-id="78df2-118">Środki tej usługi Twilio może być zastosowane tooany użycia usługi Twilio (10 środki równoważne toosending maksymalnie 1000 wiadomości SMS lub odbieranie się too1000 ruchu przychodzącego głosu minut w zależności od lokalizacji hello przeznaczenia numer i komunikatu lub wywołania telefonu).</span><span class="sxs-lookup"><span data-stu-id="78df2-118">This Twilio Credit can be applied tooany Twilio usage ($10 credit equivalent toosending as many as 1,000 SMS messages or receiving up too1000 inbound Voice minutes, depending on hello location of your phone number and message or call destination).</span></span> <span data-ttu-id="78df2-119">Realizowanie tego środki usługi Twilio i rozpocząć pracę w [ahoy.twilio.com/azure](http://ahoy.twilio.com/azure).</span><span class="sxs-lookup"><span data-stu-id="78df2-119">Redeem this Twilio credit and get started at [ahoy.twilio.com/azure](http://ahoy.twilio.com/azure).</span></span>

<span data-ttu-id="78df2-120">Usługi Twilio jest z usługą.</span><span class="sxs-lookup"><span data-stu-id="78df2-120">Twilio is a pay-as-you-go service.</span></span> <span data-ttu-id="78df2-121">Istnieją żadne opłaty konfiguracji, a konto zostanie zamknięte w dowolnym momencie.</span><span class="sxs-lookup"><span data-stu-id="78df2-121">There are no set-up fees, and you can close your account at any time.</span></span> <span data-ttu-id="78df2-122">Można znaleźć więcej szczegółów na [cennik usługi Twilio](http://www.twilio.com/voice/pricing).</span><span class="sxs-lookup"><span data-stu-id="78df2-122">You can find more details at [Twilio Pricing](http://www.twilio.com/voice/pricing).</span></span>

## <span data-ttu-id="78df2-123"><a id="Concepts"></a>Pojęcia</span><span class="sxs-lookup"><span data-stu-id="78df2-123"><a id="Concepts"></a>Concepts</span></span>
<span data-ttu-id="78df2-124">Witaj interfejsu API usługi Twilio jest interfejs API RESTful, która zapewnia funkcje programu SMS i komunikacja głosowa aplikacji.</span><span class="sxs-lookup"><span data-stu-id="78df2-124">hello Twilio API is a RESTful API that provides voice and SMS functionality for applications.</span></span> <span data-ttu-id="78df2-125">Klient biblioteki są dostępne w wielu językach; Aby uzyskać listę, zobacz [bibliotek interfejsu API usługi Twilio][twilio_libraries].</span><span class="sxs-lookup"><span data-stu-id="78df2-125">Client libraries are available in multiple languages; for a list, see [Twilio API Libraries][twilio_libraries].</span></span>

<span data-ttu-id="78df2-126">Kluczowe aspekty hello interfejsu API usługi Twilio są zleceń usługi Twilio i usługi Twilio Markup Language (TwiML).</span><span class="sxs-lookup"><span data-stu-id="78df2-126">Key aspects of hello Twilio API are Twilio verbs and Twilio Markup Language (TwiML).</span></span>

### <span data-ttu-id="78df2-127"><a id="Verbs"></a>Usługi Twilio zlecenia</span><span class="sxs-lookup"><span data-stu-id="78df2-127"><a id="Verbs"></a>Twilio verbs</span></span>
<span data-ttu-id="78df2-128">Witaj interfejs API korzysta z usługi Twilio zleceń; na przykład Witaj  **&lt;powiedzieć&gt;**  zlecenie powoduje, że usługi Twilio tooaudibly dostarczenia komunikatu w wywołaniu.</span><span class="sxs-lookup"><span data-stu-id="78df2-128">hello API makes use of Twilio verbs; for example, hello **&lt;Say&gt;** verb instructs Twilio tooaudibly deliver a message on a call.</span></span>

<span data-ttu-id="78df2-129">Witaj poniżej przedstawiono listę poleceń usługi Twilio.</span><span class="sxs-lookup"><span data-stu-id="78df2-129">hello following is a list of Twilio verbs.</span></span>  <span data-ttu-id="78df2-130">Dowiedz się więcej o hello innych poleceń i możliwości za pośrednictwem [dokumentacji usługi Twilio Markup Language](http://www.twilio.com/docs/api/twiml).</span><span class="sxs-lookup"><span data-stu-id="78df2-130">Learn about hello other verbs and capabilities via [Twilio Markup Language documentation](http://www.twilio.com/docs/api/twiml).</span></span>

* <span data-ttu-id="78df2-131">**&lt;Wybierania&gt;**: łączy hello wywołującego tooanother telefonu.</span><span class="sxs-lookup"><span data-stu-id="78df2-131">**&lt;Dial&gt;**: Connects hello caller tooanother phone.</span></span>
* <span data-ttu-id="78df2-132">**&lt;Zbierz&gt;**: zbiera wprowadzony na klawiaturze telefonu hello cyfr.</span><span class="sxs-lookup"><span data-stu-id="78df2-132">**&lt;Gather&gt;**: Collects numeric digits entered on hello telephone keypad.</span></span>
* <span data-ttu-id="78df2-133">**&lt;Rozłączanie&gt;**: kończy wywołanie.</span><span class="sxs-lookup"><span data-stu-id="78df2-133">**&lt;Hangup&gt;**: Ends a call.</span></span>
* <span data-ttu-id="78df2-134">**&lt;Odtwórz&gt;**: odtwarzania pliku audio.</span><span class="sxs-lookup"><span data-stu-id="78df2-134">**&lt;Play&gt;**: Plays an audio file.</span></span>
* <span data-ttu-id="78df2-135">**&lt;Wstrzymaj&gt;**: dyskretnie czeka na określoną liczbę sekund.</span><span class="sxs-lookup"><span data-stu-id="78df2-135">**&lt;Pause&gt;**: Waits silently for a specified number of seconds.</span></span>
* <span data-ttu-id="78df2-136">**&lt;Rekord&gt;**: rejestruje wywołującego hello głosu i zwraca adres URL pliku zawierającego hello rejestrowania.</span><span class="sxs-lookup"><span data-stu-id="78df2-136">**&lt;Record&gt;**: Records hello caller's voice and returns an URL of a file that contains hello recording.</span></span>
* <span data-ttu-id="78df2-137">**&lt;Przekieruj&gt;**: przekazuje kontrolę nad wywołania lub SMS toohello TwiML na inny adres URL.</span><span class="sxs-lookup"><span data-stu-id="78df2-137">**&lt;Redirect&gt;**: Transfers control of a call or SMS toohello TwiML at a different URL.</span></span>
* <span data-ttu-id="78df2-138">**&lt;Odrzuć&gt;**: odrzuca jako przychodzące wywołania numer usługi Twilio tooyour bez rozliczeń można</span><span class="sxs-lookup"><span data-stu-id="78df2-138">**&lt;Reject&gt;**: Rejects an incoming call tooyour Twilio number without billing you</span></span>
* <span data-ttu-id="78df2-139">**&lt;Powiedz&gt;**: Konwertuje tekst toospeech, które zostało utworzone w wywołaniu.</span><span class="sxs-lookup"><span data-stu-id="78df2-139">**&lt;Say&gt;**: Converts text toospeech that is made on a call.</span></span>
* <span data-ttu-id="78df2-140">**&lt;SMS&gt;**: wysyła wiadomość SMS.</span><span class="sxs-lookup"><span data-stu-id="78df2-140">**&lt;Sms&gt;**: Sends an SMS message.</span></span>

### <span data-ttu-id="78df2-141"><a id="TwiML"></a>TwiML</span><span class="sxs-lookup"><span data-stu-id="78df2-141"><a id="TwiML"></a>TwiML</span></span>
<span data-ttu-id="78df2-142">Zestaw instrukcji oparte na języku XML, oparte na powitania usługi Twilio zlecenia, które informują usługi Twilio, jak jest TwiML tooprocess wywołania lub wiadomości SMS.</span><span class="sxs-lookup"><span data-stu-id="78df2-142">TwiML is a set of XML-based instructions based on hello Twilio verbs that inform Twilio of how tooprocess a call or SMS.</span></span>

<span data-ttu-id="78df2-143">Na przykład powitania po TwiML może dokonać konwersji tekstu hello **Hello World** toospeech.</span><span class="sxs-lookup"><span data-stu-id="78df2-143">As an example, hello following TwiML would convert hello text **Hello World** toospeech.</span></span>

    <?xml version="1.0" encoding="UTF-8" ?>
    <Response>
      <Say>Hello World</Say>
    </Response>

<span data-ttu-id="78df2-144">Podczas wywołania aplikacji hello interfejsu API usługi Twilio, jeden z parametrów interfejsu API hello jest adres URL hello, która zwraca odpowiedź TwiML hello.</span><span class="sxs-lookup"><span data-stu-id="78df2-144">When your application calls hello Twilio API, one of hello API parameters is hello URL that returns hello TwiML response.</span></span> <span data-ttu-id="78df2-145">Do celów programistycznych możesz użyć wprowadzone do usługi Twilio adresy URL tooprovide hello TwiML odpowiedzi są używane przez aplikacje.</span><span class="sxs-lookup"><span data-stu-id="78df2-145">For development purposes, you can use Twilio-provided URLs tooprovide hello TwiML responses used by your applications.</span></span> <span data-ttu-id="78df2-146">Może również udostępniać swoje własne adresy URL tooproduce hello TwiML odpowiedzi, a inną opcją jest toouse hello **TwiMLResponse** obiektu.</span><span class="sxs-lookup"><span data-stu-id="78df2-146">You could also host your own URLs tooproduce hello TwiML responses, and another option is toouse hello **TwiMLResponse** object.</span></span>

<span data-ttu-id="78df2-147">Aby uzyskać więcej informacji na temat usługi Twilio zlecenia i ich atrybuty oraz TwiML, zobacz [TwiML][twiml].</span><span class="sxs-lookup"><span data-stu-id="78df2-147">For more information about Twilio verbs, their attributes, and TwiML, see [TwiML][twiml].</span></span> <span data-ttu-id="78df2-148">Aby uzyskać dodatkowe informacje na temat hello interfejsu API usługi Twilio, zobacz [interfejsu API usługi Twilio][twilio_api].</span><span class="sxs-lookup"><span data-stu-id="78df2-148">For additional information about hello Twilio API, see [Twilio API][twilio_api].</span></span>

## <span data-ttu-id="78df2-149"><a id="CreateAccount"></a>Tworzenie konta usługi Twilio</span><span class="sxs-lookup"><span data-stu-id="78df2-149"><a id="CreateAccount"></a>Create a Twilio Account</span></span>
<span data-ttu-id="78df2-150">Jeśli wszystko jest gotowe tooget konta usługi Twilio, zarejestruj się w [spróbuj usługi Twilio][try_twilio].</span><span class="sxs-lookup"><span data-stu-id="78df2-150">When you're ready tooget a Twilio account, sign up at [Try Twilio][try_twilio].</span></span> <span data-ttu-id="78df2-151">Można rozpoczynać bezpłatne konto, a następnie Uaktualnij swoje konto później.</span><span class="sxs-lookup"><span data-stu-id="78df2-151">You can start with a free account, and upgrade your account later.</span></span>

<span data-ttu-id="78df2-152">Po utworzeniu konta dla konta usługi Twilio, otrzymasz Identyfikatora konta oraz tokenu uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="78df2-152">When you sign up for a Twilio account, you'll receive an account ID and an authentication token.</span></span> <span data-ttu-id="78df2-153">Zarówno będzie potrzebne toomake wywołania interfejsu API usługi Twilio.</span><span class="sxs-lookup"><span data-stu-id="78df2-153">Both will be needed toomake Twilio API calls.</span></span> <span data-ttu-id="78df2-154">tooprevent nieautoryzowany dostęp do konta tooyour, bezpieczeństwo Twojego tokenu uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="78df2-154">tooprevent unauthorized access tooyour account, keep your authentication token secure.</span></span> <span data-ttu-id="78df2-155">Twój identyfikator konta i uwierzytelniania tokenu jest wyświetlana na powitania [strony konta usługi Twilio][twilio_account]w hello pola oznaczone **identyfikator SID konta** i **TOKEN uwierzytelniania**odpowiednio.</span><span class="sxs-lookup"><span data-stu-id="78df2-155">Your account ID and authentication token are viewable at hello [Twilio account page][twilio_account], in hello fields labeled **ACCOUNT SID** and **AUTH TOKEN**, respectively.</span></span>

## <span data-ttu-id="78df2-156"><a id="create_app"></a>Tworzenie aplikacji Azure</span><span class="sxs-lookup"><span data-stu-id="78df2-156"><a id="create_app"></a>Create an Azure Application</span></span>
<span data-ttu-id="78df2-157">Azure aplikacji, która obsługuje aplikację usługi Twilio włączone nie różni się od innych aplikacji Azure.</span><span class="sxs-lookup"><span data-stu-id="78df2-157">An Azure application that hosts a Twilio enabled application is no different from any other Azure application.</span></span> <span data-ttu-id="78df2-158">Dodawanie biblioteki .NET usługi Twilio hello i skonfigurować hello roli toouse hello .NET usługi Twilio biblioteki.</span><span class="sxs-lookup"><span data-stu-id="78df2-158">You add hello Twilio .NET library and configure hello role toouse hello Twilio .NET libraries.</span></span>
<span data-ttu-id="78df2-159">Informacje dotyczące tworzenia początkowej projektu platformy Azure, zobacz [Tworzenie projektu platformy Azure z programem Visual Studio][vs_project].</span><span class="sxs-lookup"><span data-stu-id="78df2-159">For information on creating an initial Azure project, see [Creating an Azure project with Visual Studio][vs_project].</span></span>

## <span data-ttu-id="78df2-160"><a id="configure_app"></a>Konfigurowanie bibliotek usługi Twilio toouse Twoja aplikacja</span><span class="sxs-lookup"><span data-stu-id="78df2-160"><a id="configure_app"></a>Configure Your Application toouse Twilio Libraries</span></span>
<span data-ttu-id="78df2-161">Usługi Twilio zawiera zestaw .NET pomocnika bibliotek, które otaczają różnych aspektów usługi Twilio tooprovide prosty i łatwy sposób toointeract hello interfejsu API REST usługi Twilio i klienta usługi Twilio toogenerate TwiML odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="78df2-161">Twilio provides a set of .NET helper libraries that wrap various aspects of Twilio tooprovide simple and easy ways toointeract with hello Twilio REST API and Twilio Client toogenerate TwiML responses.</span></span>

<span data-ttu-id="78df2-162">Usługi Twilio zawiera pięć bibliotek dla deweloperów platformy .NET:</span><span class="sxs-lookup"><span data-stu-id="78df2-162">Twilio provides five libraries for .NET developers:</span></span>
<span data-ttu-id="78df2-163">Biblioteka</span><span class="sxs-lookup"><span data-stu-id="78df2-163">Library</span></span>|<span data-ttu-id="78df2-164">Opis</span><span class="sxs-lookup"><span data-stu-id="78df2-164">Description</span></span>
---|---
<span data-ttu-id="78df2-165">Twilio.API</span><span class="sxs-lookup"><span data-stu-id="78df2-165">Twilio.API</span></span>|<span data-ttu-id="78df2-166">Hello podstawowe usługi Twilio biblioteki, która opakowuje hello interfejsu API REST usługi Twilio przyjazną biblioteki .NET.</span><span class="sxs-lookup"><span data-stu-id="78df2-166">hello core Twilio library that wraps hello Twilio REST API in a friendly .NET library.</span></span> <span data-ttu-id="78df2-167">Ta biblioteka jest dostępna dla platformy .NET, Silverlight i Windows Phone 7.</span><span class="sxs-lookup"><span data-stu-id="78df2-167">This library is available for .NET, Silverlight, and Windows Phone 7.</span></span>
<span data-ttu-id="78df2-168">Twilio.TwiML</span><span class="sxs-lookup"><span data-stu-id="78df2-168">Twilio.TwiML</span></span>|<span data-ttu-id="78df2-169">Zawiera znacznik TwiML toogenerate przyjazną sposób .NET.</span><span class="sxs-lookup"><span data-stu-id="78df2-169">Provides a .NET friendly way toogenerate TwiML markup.</span></span>
<span data-ttu-id="78df2-170">Twilio.MVC</span><span class="sxs-lookup"><span data-stu-id="78df2-170">Twilio.MVC</span></span>|<span data-ttu-id="78df2-171">Dla deweloperów przy użyciu platformy ASP.NET MVC Ta biblioteka zawiera TwilioController, TwiML ActionResult i atrybutu sprawdzania poprawności żądania.</span><span class="sxs-lookup"><span data-stu-id="78df2-171">For developers using ASP.NET MVC, this library includes a TwilioController, TwiML ActionResult, and request validation attribute.</span></span>
<span data-ttu-id="78df2-172">Twilio.WebMatrix</span><span class="sxs-lookup"><span data-stu-id="78df2-172">Twilio.WebMatrix</span></span>|<span data-ttu-id="78df2-173">Dla deweloperów korzystających bezpłatne narzędzie programistyczne WebMatrix firmy Microsoft Ta biblioteka zawiera pomocników składni Razor do wykonywania różnych akcji usługi Twilio.</span><span class="sxs-lookup"><span data-stu-id="78df2-173">For developers using Microsoft's free WebMatrix development tool, this library contains Razor syntax helpers for various Twilio actions.</span></span>
<span data-ttu-id="78df2-174">Twilio.Client.Capability</span><span class="sxs-lookup"><span data-stu-id="78df2-174">Twilio.Client.Capability</span></span>|<span data-ttu-id="78df2-175">Zawiera hello generatora tokenów możliwości do użycia z hello zestawu JavaScript SDK klienta usługi Twilio.</span><span class="sxs-lookup"><span data-stu-id="78df2-175">Contains hello Capability token generator for use with hello Twilio Client JavaScript SDK.</span></span>

<span data-ttu-id="78df2-176">Należy pamiętać, że wszystkie biblioteki wymaga .NET 3.5, Silverlight 4 lub Windows Phone 7 lub nowszy.</span><span class="sxs-lookup"><span data-stu-id="78df2-176">Note that all libraries require .NET 3.5, Silverlight 4, or Windows Phone 7 or later.</span></span>

<span data-ttu-id="78df2-177">Przykłady Hello podanych w tym przewodniku używać hello Twilio.API biblioteki.</span><span class="sxs-lookup"><span data-stu-id="78df2-177">hello samples provided in this guide use hello Twilio.API library.</span></span>

<span data-ttu-id="78df2-178">Witaj bibliotek mogą być [zainstalowane przy użyciu rozszerzenia Menedżera pakietów NuGet hello](http://www.twilio.com/docs/csharp/install) dostępne dla programu Visual Studio 2010 w górę too2015.</span><span class="sxs-lookup"><span data-stu-id="78df2-178">hello libraries can be [installed using hello NuGet package manager extension](http://www.twilio.com/docs/csharp/install) available for Visual Studio 2010 up too2015.</span></span>  <span data-ttu-id="78df2-179">Witaj kod źródłowy jest hostowana na [GitHub][twilio_github_repo], w tym typu Wiki, który zawiera pełną dokumentację dla przy użyciu bibliotek hello.</span><span class="sxs-lookup"><span data-stu-id="78df2-179">hello source code is hosted on [GitHub][twilio_github_repo], which includes a Wiki that contains complete documentation for using hello libraries.</span></span>

<span data-ttu-id="78df2-180">Domyślnie program Microsoft Visual Studio 2010 instaluje NuGet w wersji 1.2.</span><span class="sxs-lookup"><span data-stu-id="78df2-180">By default, Microsoft Visual Studio 2010 installs version 1.2 of NuGet.</span></span> <span data-ttu-id="78df2-181">Instalacja bibliotek usługi Twilio hello wymaga wersji 1.6 NuGet lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="78df2-181">Installing hello Twilio libraries requires version 1.6 of NuGet or higher.</span></span> <span data-ttu-id="78df2-182">Aby uzyskać informacje dotyczące instalowania lub aktualizowania NuGet, zobacz [http://nuget.org/][nuget].</span><span class="sxs-lookup"><span data-stu-id="78df2-182">For information on installing or updating NuGet, see [http://nuget.org/][nuget].</span></span>

> [!NOTE]
> <span data-ttu-id="78df2-183">tooinstall hello najnowszą wersję programu NuGet, należy najpierw odinstalować hello wersji załadowanego za pomocą hello Menedżera rozszerzeń programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="78df2-183">tooinstall hello latest version of NuGet, you must first uninstall hello loaded version using hello Visual Studio Extension Manager.</span></span> <span data-ttu-id="78df2-184">toodo tak, możesz uruchomić program Visual Studio jako administrator.</span><span class="sxs-lookup"><span data-stu-id="78df2-184">toodo so, you must run Visual Studio as administrator.</span></span> <span data-ttu-id="78df2-185">W przeciwnym razie przycisk Odinstaluj hello jest wyłączona.</span><span class="sxs-lookup"><span data-stu-id="78df2-185">Otherwise, hello Uninstall button is disabled.</span></span>
>
>

### <span data-ttu-id="78df2-186"><a id="use_nuget"></a>tooadd hello usługi Twilio biblioteki tooyour projektu Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="78df2-186"><a id="use_nuget"></a>tooadd hello Twilio libraries tooyour Visual Studio project:</span></span>
1. <span data-ttu-id="78df2-187">Otwórz rozwiązanie w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="78df2-187">Open your solution in Visual Studio.</span></span>
2. <span data-ttu-id="78df2-188">Kliknij prawym przyciskiem myszy **odwołania**.</span><span class="sxs-lookup"><span data-stu-id="78df2-188">Right-click **References**.</span></span>
3. <span data-ttu-id="78df2-189">Kliknij przycisk **Zarządzaj pakietami NuGet...**</span><span class="sxs-lookup"><span data-stu-id="78df2-189">Click **Manage NuGet Packages...**</span></span>
4. <span data-ttu-id="78df2-190">Kliknij przycisk **Online**.</span><span class="sxs-lookup"><span data-stu-id="78df2-190">Click **Online**.</span></span>
5. <span data-ttu-id="78df2-191">W hello wyszukiwania online wpisz *usługi twilio*.</span><span class="sxs-lookup"><span data-stu-id="78df2-191">In hello search online box, type *twilio*.</span></span>
6. <span data-ttu-id="78df2-192">Kliknij przycisk **zainstalować** na powitania pakietu usługi Twilio.</span><span class="sxs-lookup"><span data-stu-id="78df2-192">Click **Install** on hello Twilio package.</span></span>

## <span data-ttu-id="78df2-193"><a id="howto_make_call"></a>Porady: wykonywanie połączenia wychodzące</span><span class="sxs-lookup"><span data-stu-id="78df2-193"><a id="howto_make_call"></a>How to: Make an outgoing call</span></span>
<span data-ttu-id="78df2-194">Witaj poniżej pokazano, jak toomake wychodzące wywołanie przy użyciu hello **CallResource** klasy.</span><span class="sxs-lookup"><span data-stu-id="78df2-194">hello following shows how toomake an outgoing call using hello **CallResource** class.</span></span> <span data-ttu-id="78df2-195">Ten kod zawiera również hello tooreturn lokacja dostarczonych do usługi Twilio odpowiedzi usługi Twilio Markup Language (TwiML).</span><span class="sxs-lookup"><span data-stu-id="78df2-195">This code also uses a Twilio-provided site tooreturn hello Twilio Markup Language (TwiML) response.</span></span> <span data-ttu-id="78df2-196">Podstaw wartości hello **do** i **z** numerów telefonów i upewnij się, że sprawdzisz hello **z** numer telefonu dla konta usługi Twilio przed uruchomieniem kodu hello.</span><span class="sxs-lookup"><span data-stu-id="78df2-196">Substitute your values for hello **to** and **from** phone numbers, and ensure that you verify hello **from** phone number for your Twilio account before running hello code.</span></span>

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

<span data-ttu-id="78df2-197">Aby uzyskać więcej informacji o parametrach hello przekazano toohello **CallResource.Create** metody, zobacz [http://www.twilio.com/docs/api/rest/making-calls][twilio_rest_making_calls].</span><span class="sxs-lookup"><span data-stu-id="78df2-197">For more information about hello parameters passed in toohello **CallResource.Create** method, see [http://www.twilio.com/docs/api/rest/making-calls][twilio_rest_making_calls].</span></span>

<span data-ttu-id="78df2-198">Jak wspomniano, ten kod używa hello tooreturn lokacja dostarczonych do usługi Twilio TwiML odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="78df2-198">As mentioned, this code uses a Twilio-provided site tooreturn hello TwiML response.</span></span> <span data-ttu-id="78df2-199">Zamiast tego można użyć własnych lokacji tooprovide hello TwiML odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="78df2-199">You could instead use your own site tooprovide hello TwiML response.</span></span> <span data-ttu-id="78df2-200">Aby uzyskać więcej informacji, zobacz [porady: Podaj TwiML odpowiedzi z własnej witryny sieci Web](#howto_provide_twiml_responses).</span><span class="sxs-lookup"><span data-stu-id="78df2-200">For more information, see [How to: Provide TwiML responses from your own website](#howto_provide_twiml_responses).</span></span>

## <span data-ttu-id="78df2-201"><a id="howto_send_sms"></a>Porady: Wyślij wiadomość SMS</span><span class="sxs-lookup"><span data-stu-id="78df2-201"><a id="howto_send_sms"></a>How to: Send an SMS message</span></span>
<span data-ttu-id="78df2-202">Witaj Poniższy zrzut ekranu przedstawia sposób hello toosend wiadomość SMS przy użyciu **MessageResource** klasy.</span><span class="sxs-lookup"><span data-stu-id="78df2-202">hello following screenshot shows how toosend an SMS message using hello **MessageResource**  class.</span></span> <span data-ttu-id="78df2-203">Witaj **z** numer jest udostępniany przez usługi Twilio dla wersji próbnej kont toosend wiadomości SMS.</span><span class="sxs-lookup"><span data-stu-id="78df2-203">hello **from** number is provided by Twilio for trial accounts toosend SMS messages.</span></span> <span data-ttu-id="78df2-204">Witaj **do** numer muszą być weryfikowane dla konta usługi Twilio, przed rozpoczęciem powitalne kodu.</span><span class="sxs-lookup"><span data-stu-id="78df2-204">hello **to** number must be verified for your Twilio account before you run hello code.</span></span>

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

## <span data-ttu-id="78df2-205"><a id="howto_provide_twiml_responses"></a>Porady: Podaj TwiML odpowiedzi z własnej witryny sieci Web</span><span class="sxs-lookup"><span data-stu-id="78df2-205"><a id="howto_provide_twiml_responses"></a>How to: Provide TwiML Responses from your own website</span></span>
<span data-ttu-id="78df2-206">Gdy aplikacja inicjuje toohello wywołania interfejsu API usługi Twilio — na przykład za pośrednictwem hello **CallResource.Create** metody — usługi Twilio wysyła adres URL tooan żądania, który jest oczekiwanym tooreturn TwiML odpowiedź.</span><span class="sxs-lookup"><span data-stu-id="78df2-206">When your application initiates a call toohello Twilio API - for example, via hello **CallResource.Create** method - Twilio sends your request tooan URL that is expected tooreturn a TwiML response.</span></span> <span data-ttu-id="78df2-207">przykład Witaj w [porady: wykonania wywołania wychodzącego](#howto_make_call) używa hello adres URL udostępniony do usługi Twilio [http://twimlets.com/message] [ twimlet_message_url] tooreturn hello odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="78df2-207">hello example in [How to: Make an outgoing call](#howto_make_call) uses hello Twilio-provided URL [http://twimlets.com/message][twimlet_message_url] tooreturn hello response.</span></span>

> [!NOTE]
> <span data-ttu-id="78df2-208">Gdy TwiML jest przeznaczony do użytku przez usługi sieci web, można wyświetlić hello TwiML w przeglądarce.</span><span class="sxs-lookup"><span data-stu-id="78df2-208">While TwiML is designed for use by web services, you can view hello TwiML in your browser.</span></span> <span data-ttu-id="78df2-209">Na przykład kliknij pozycję [http://twimlets.com/message] [ twimlet_message_url] toosee pustą &lt;odpowiedzi&gt; element; inny przykład kliknij [http://twimlets.com/message ? Komunikat 5B0 %% 5 D = Hello % 20World](http://twimlets.com/message?Message%5B0%5D=Hello%20World) toosee &lt;odpowiedzi&gt; element, który zawiera &lt;powiedzieć&gt; elementu.</span><span class="sxs-lookup"><span data-stu-id="78df2-209">For example, click [http://twimlets.com/message][twimlet_message_url] toosee an empty &lt;Response&gt; element; as another example, click [http://twimlets.com/message?Message%5B0%5D=Hello%20World](http://twimlets.com/message?Message%5B0%5D=Hello%20World) toosee a &lt;Response&gt; element that contains a &lt;Say&gt; element.</span></span>
>
>

<span data-ttu-id="78df2-210">Zamiast polegania na adres URL udostępniony do usługi Twilio hello, można utworzyć własny adres URL w witrynie odpowiedzi HTTP.</span><span class="sxs-lookup"><span data-stu-id="78df2-210">Instead of relying on hello Twilio-provided URL, you can create your own URL site that returns HTTP responses.</span></span> <span data-ttu-id="78df2-211">Można utworzyć witrynę hello w dowolnym języku, który zwraca odpowiedzi HTTP.</span><span class="sxs-lookup"><span data-stu-id="78df2-211">You can create hello site in any language that returns HTTP responses.</span></span> <span data-ttu-id="78df2-212">W tym temacie założono, że będzie obsługiwać hello adresu URL, z ogólnego obsługi ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="78df2-212">This topic assumes you'll be hosting hello URL from an ASP.NET generic handler.</span></span>

<span data-ttu-id="78df2-213">powitania po obsługi ASP.NET crafts odpowiedzi TwiML informacją **Hello World** na powitania wywołania.</span><span class="sxs-lookup"><span data-stu-id="78df2-213">hello following ASP.NET Handler crafts a TwiML response that says **Hello World** on hello call.</span></span>

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
    
<span data-ttu-id="78df2-214">Jak widać w powyższym przykładzie hello hello TwiML odpowiedzi jest po prostu dokumentu XML.</span><span class="sxs-lookup"><span data-stu-id="78df2-214">As you can see from hello example above, hello TwiML response is simply an XML document.</span></span> <span data-ttu-id="78df2-215">Biblioteka Twilio.TwiML Hello zawiera klasy, które generuje TwiML dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="78df2-215">hello Twilio.TwiML library contains classes that will generate TwiML for you.</span></span> <span data-ttu-id="78df2-216">Hello poniższy przykład tworzy hello równoważne odpowiedzi, jak pokazano powyżej, ale używa hello **VoiceResponse** klasy.</span><span class="sxs-lookup"><span data-stu-id="78df2-216">hello example below produces hello equivalent response as shown above, but uses hello **VoiceResponse** class.</span></span>

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

<span data-ttu-id="78df2-217">Aby uzyskać więcej informacji o TwiML, zobacz [https://www.twilio.com/docs/api/twiml](https://www.twilio.com/docs/api/twiml).</span><span class="sxs-lookup"><span data-stu-id="78df2-217">For more information about TwiML, see [https://www.twilio.com/docs/api/twiml](https://www.twilio.com/docs/api/twiml).</span></span>

<span data-ttu-id="78df2-218">Po skonfigurowaniu odpowiedzi TwiML tooprovide sposób można przekazać ten adres URL toohello **CallResource.Create** metody.</span><span class="sxs-lookup"><span data-stu-id="78df2-218">Once you have set up a way tooprovide TwiML responses, you can pass that URL toohello **CallResource.Create** method.</span></span> <span data-ttu-id="78df2-219">Na przykład, jeśli masz aplikację sieci web o nazwie tooan MyTwiML wdrożona usługa w chmurze platformy Azure, a nazwa hello obsługi programu ASP.NET jest mytwiml.ashx, adres URL hello mogą zostać przekazane za**CallResource.Create** pokazane na powitania następującego kodu przykład:</span><span class="sxs-lookup"><span data-stu-id="78df2-219">For example, if you have a web application named MyTwiML deployed tooan Azure cloud service, and hello name of your ASP.NET Handler is mytwiml.ashx, hello URL can be passed too**CallResource.Create** as shown in hello following code sample:</span></span>

    // This sample uses hello sandbox number provided by Twilio toomake hello call.
    // Place hello call.
    var call = CallResource.Create(
        to: new PhoneNumber("+NNNNNNNNNN"),
        from: new PhoneNumber("NNNNNNNNNN"),
        url: new Uri("http://<your_hosted_service>.cloudapp.net/MyTwiML/mytwiml.ashx"));
        }

<span data-ttu-id="78df2-220">Aby uzyskać dodatkowe informacje dotyczące korzystania z usługi Twilio na platformie Azure za pomocą programu ASP.NET, zobacz [jak toomake rozmowy telefonicznej z rolą sieci web na platformie Azure przy użyciu usługi Twilio][howto_phonecall_dotnet].</span><span class="sxs-lookup"><span data-stu-id="78df2-220">For additional information about using Twilio on Azure with ASP.NET, see [How toomake a phone call using Twilio in a web role on Azure][howto_phonecall_dotnet].</span></span>

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
