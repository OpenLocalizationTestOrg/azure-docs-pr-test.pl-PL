---
title: "tooUse aaaHow usługi Twilio głosowe i programu SMS (Python) | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak komunikatów toomake połączeń telefonicznych i Wyślij wiadomość SMS z usługi interfejsu API usługi Twilio hello na platformie Azure. Przykłady kodu napisane w języku Python."
services: 
documentationcenter: python
author: devinrader
manager: twilio
editor: 
ms.assetid: 561bc75b-4ac4-40ba-bcba-48e901f27cc3
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 02/19/2015
ms.author: MicrosoftHelp@twilio.com
ms.openlocfilehash: 1f16a107d95c94589b8d61a0971c5b62d639c571
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-twilio-for-voice-and-sms-capabilities-in-python"></a><span data-ttu-id="41aac-104">Jak tooUse usługi Twilio głosowe i możliwości programu SMS w języku Python</span><span class="sxs-lookup"><span data-stu-id="41aac-104">How tooUse Twilio for Voice and SMS Capabilities in Python</span></span>
<span data-ttu-id="41aac-105">W tym przewodniku pokazano, jak tooperform typowych zadań programowania hello interfejsu API usługi Twilio usługi na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="41aac-105">This guide demonstrates how tooperform common programming tasks with hello Twilio API service on Azure.</span></span> <span data-ttu-id="41aac-106">omówione scenariusze Hello obejmują tworzenie połączeń telefonicznych i wysyłanie wiadomości krótką wiadomość usługi (SMS).</span><span class="sxs-lookup"><span data-stu-id="41aac-106">hello scenarios covered include making a phone call and sending a Short Message Service (SMS) message.</span></span> <span data-ttu-id="41aac-107">Aby uzyskać więcej informacji na temat usługi Twilio i komunikacja głosowa programu SMS w aplikacji, zobacz hello [następne kroki](#NextSteps) sekcji.</span><span class="sxs-lookup"><span data-stu-id="41aac-107">For more information on Twilio and using voice and SMS in your applications, see hello [Next Steps](#NextSteps) section.</span></span>

## <span data-ttu-id="41aac-108"><a id="WhatIs"></a>Co to jest usługi Twilio?</span><span class="sxs-lookup"><span data-stu-id="41aac-108"><a id="WhatIs"></a>What is Twilio?</span></span>
<span data-ttu-id="41aac-109">Usługi Twilio jest włączanie hello przyszłych komunikacji biznesowej, włączanie deweloperzy tooembed głosu VoIP i wiadomości do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="41aac-109">Twilio is powering hello future of business communications, enabling developers tooembed voice, VoIP, and messaging into applications.</span></span> <span data-ttu-id="41aac-110">Zwirtualizuj one wszystkich infrastrukturę potrzebną w środowisku chmury, globalnych ujawnienie go za pośrednictwem platformy hello API komunikacji usługi Twilio.</span><span class="sxs-lookup"><span data-stu-id="41aac-110">They virtualize all infrastructure needed in a cloud-based, global environment, exposing it through hello Twilio communications API platform.</span></span> <span data-ttu-id="41aac-111">Aplikacje są proste toobuild i skalowalność.</span><span class="sxs-lookup"><span data-stu-id="41aac-111">Applications are simple toobuild and scalable.</span></span> <span data-ttu-id="41aac-112">Kredyty elastyczność Tobie płatności — jako Przejdź ceny i korzystać z niej niezawodności chmury.</span><span class="sxs-lookup"><span data-stu-id="41aac-112">Enjoy flexibility with pay-as-you go pricing, and benefit from cloud reliability.</span></span>

<span data-ttu-id="41aac-113">**Usługi Twilio głosu** umożliwia toomake Twojej aplikacji i odbieranie połączeń telefonicznych.</span><span class="sxs-lookup"><span data-stu-id="41aac-113">**Twilio Voice** allows your applications toomake and receive phone calls.</span></span>
<span data-ttu-id="41aac-114">**SMS usługi Twilio** umożliwia toosend Twojej aplikacji i odbieranie wiadomości tekstowych.</span><span class="sxs-lookup"><span data-stu-id="41aac-114">**Twilio SMS** enables your application toosend and receive text messages.</span></span>
<span data-ttu-id="41aac-115">**Klient usługi Twilio** pozwala toomake VoIP wywołania z dowolnego telefonu, tabletu lub przeglądarki i obsługuje WebRTC.</span><span class="sxs-lookup"><span data-stu-id="41aac-115">**Twilio Client** allows you toomake VoIP calls from any phone, tablet, or browser and supports WebRTC.</span></span>

## <span data-ttu-id="41aac-116"><a id="Pricing"></a>Cennik usługi Twilio i oferty specjalne</span><span class="sxs-lookup"><span data-stu-id="41aac-116"><a id="Pricing"></a>Twilio Pricing and Special Offers</span></span>
<span data-ttu-id="41aac-117">Azure klienci otrzymają [oferta specjalna] [ special_offer] 10 $ środków usługi Twilio po uaktualnieniu konta usługi Twilio.</span><span class="sxs-lookup"><span data-stu-id="41aac-117">Azure customers receive a [special offer][special_offer] $10 of Twilio Credit when you upgrade your Twilio Account.</span></span> <span data-ttu-id="41aac-118">Środki tej usługi Twilio może być zastosowane tooany użycia usługi Twilio (10 środki równoważne toosending maksymalnie 1000 wiadomości SMS lub odbieranie się too1000 ruchu przychodzącego głosu minut w zależności od lokalizacji hello przeznaczenia numer i komunikatu lub wywołania telefonu).</span><span class="sxs-lookup"><span data-stu-id="41aac-118">This Twilio Credit can be applied tooany Twilio usage ($10 credit equivalent toosending as many as 1,000 SMS messages or receiving up too1000 inbound Voice minutes, depending on hello location of your phone number and message or call destination).</span></span> <span data-ttu-id="41aac-119">Zrealizować to [środki usługi Twilio] [ special_offer] i rozpocząć pracę.</span><span class="sxs-lookup"><span data-stu-id="41aac-119">Redeem this [Twilio credit][special_offer] and get started.</span></span>

<span data-ttu-id="41aac-120">Usługi Twilio jest z usługą.</span><span class="sxs-lookup"><span data-stu-id="41aac-120">Twilio is a pay-as-you-go service.</span></span> <span data-ttu-id="41aac-121">Nie żadne opłaty konfiguracji i w dowolnej chwili możesz zamknąć konto.</span><span class="sxs-lookup"><span data-stu-id="41aac-121">There are no set-up fees and you can close your account at any time.</span></span> <span data-ttu-id="41aac-122">Można znaleźć więcej szczegółów na [cennik usługi Twilio][twilio_pricing].</span><span class="sxs-lookup"><span data-stu-id="41aac-122">You can find more details at [Twilio Pricing][twilio_pricing].</span></span>

## <span data-ttu-id="41aac-123"><a id="Concepts"></a>Pojęcia</span><span class="sxs-lookup"><span data-stu-id="41aac-123"><a id="Concepts"></a>Concepts</span></span>
<span data-ttu-id="41aac-124">Witaj interfejsu API usługi Twilio jest interfejs API RESTful, która zapewnia funkcje programu SMS i komunikacja głosowa aplikacji.</span><span class="sxs-lookup"><span data-stu-id="41aac-124">hello Twilio API is a RESTful API that provides voice and SMS functionality for applications.</span></span> <span data-ttu-id="41aac-125">Klient biblioteki są dostępne w wielu językach; Aby uzyskać listę, zobacz [bibliotek interfejsu API usługi Twilio][twilio_libraries].</span><span class="sxs-lookup"><span data-stu-id="41aac-125">Client libraries are available in multiple languages; for a list, see [Twilio API Libraries][twilio_libraries].</span></span>

<span data-ttu-id="41aac-126">Kluczowe aspekty hello interfejsu API usługi Twilio są zleceń usługi Twilio i usługi Twilio Markup Language (TwiML).</span><span class="sxs-lookup"><span data-stu-id="41aac-126">Key aspects of hello Twilio API are Twilio verbs and Twilio Markup Language (TwiML).</span></span>

### <span data-ttu-id="41aac-127"><a id="Verbs"></a>Usługi Twilio zlecenia</span><span class="sxs-lookup"><span data-stu-id="41aac-127"><a id="Verbs"></a>Twilio Verbs</span></span>
<span data-ttu-id="41aac-128">Witaj interfejs API korzysta z usługi Twilio zleceń; na przykład Witaj  **&lt;powiedzieć&gt;**  zlecenie powoduje, że usługi Twilio tooaudibly dostarczenia komunikatu w wywołaniu.</span><span class="sxs-lookup"><span data-stu-id="41aac-128">hello API makes use of Twilio verbs; for example, hello **&lt;Say&gt;** verb instructs Twilio tooaudibly deliver a message on a call.</span></span>

<span data-ttu-id="41aac-129">Witaj poniżej przedstawiono listę poleceń usługi Twilio.</span><span class="sxs-lookup"><span data-stu-id="41aac-129">hello following is a list of Twilio verbs.</span></span> <span data-ttu-id="41aac-130">Dowiedz się więcej o hello innych poleceń i możliwości za pośrednictwem [dokumentacji usługi Twilio Markup Language][twiml].</span><span class="sxs-lookup"><span data-stu-id="41aac-130">Learn about hello other verbs and capabilities via [Twilio Markup Language documentation][twiml].</span></span>

* <span data-ttu-id="41aac-131">**&lt;Wybierania&gt;**: łączy hello wywołującego tooanother telefonu.</span><span class="sxs-lookup"><span data-stu-id="41aac-131">**&lt;Dial&gt;**: Connects hello caller tooanother phone.</span></span>
* <span data-ttu-id="41aac-132">**&lt;Zbierz&gt;**: zbiera wprowadzony na klawiaturze telefonu hello cyfr.</span><span class="sxs-lookup"><span data-stu-id="41aac-132">**&lt;Gather&gt;**: Collects numeric digits entered on hello telephone keypad.</span></span>
* <span data-ttu-id="41aac-133">**&lt;Rozłączanie&gt;**: kończy wywołanie.</span><span class="sxs-lookup"><span data-stu-id="41aac-133">**&lt;Hangup&gt;**: Ends a call.</span></span>
* <span data-ttu-id="41aac-134">**&lt;Wstrzymaj&gt;**: dyskretnie czeka na określoną liczbę sekund.</span><span class="sxs-lookup"><span data-stu-id="41aac-134">**&lt;Pause&gt;**: Waits silently for a specified number of seconds.</span></span>
* <span data-ttu-id="41aac-135">**&lt;Odtwórz&gt;**: odtwarzania pliku audio.</span><span class="sxs-lookup"><span data-stu-id="41aac-135">**&lt;Play&gt;**: Plays an audio file.</span></span>
* <span data-ttu-id="41aac-136">**&lt;Kolejka&gt;**: Dodaj kolejkę tooa hello obiekty wywołujące.</span><span class="sxs-lookup"><span data-stu-id="41aac-136">**&lt;Queue&gt;**: Add hello tooa queue of callers.</span></span>
* <span data-ttu-id="41aac-137">**&lt;Rekord&gt;**: rejestruje głosu hello hello wywołującego i zwraca adres URL pliku zawierającego hello rejestrowania.</span><span class="sxs-lookup"><span data-stu-id="41aac-137">**&lt;Record&gt;**: Records hello voice of hello caller and returns a URL of a file that contains hello recording.</span></span>
* <span data-ttu-id="41aac-138">**&lt;Przekieruj&gt;**: przekazuje kontrolę nad wywołania lub SMS toohello TwiML na inny adres URL.</span><span class="sxs-lookup"><span data-stu-id="41aac-138">**&lt;Redirect&gt;**: Transfers control of a call or SMS toohello TwiML at a different URL.</span></span>
* <span data-ttu-id="41aac-139">**&lt;Odrzuć&gt;**: odrzuca jako przychodzące wywołania numer usługi Twilio tooyour bez rozliczeń można.</span><span class="sxs-lookup"><span data-stu-id="41aac-139">**&lt;Reject&gt;**: Rejects an incoming call tooyour Twilio number without billing you.</span></span>
* <span data-ttu-id="41aac-140">**&lt;Powiedz&gt;**: Konwertuje tekst toospeech, które zostało utworzone w wywołaniu.</span><span class="sxs-lookup"><span data-stu-id="41aac-140">**&lt;Say&gt;**: Converts text toospeech that is made on a call.</span></span>
* <span data-ttu-id="41aac-141">**&lt;SMS&gt;**: wysyła wiadomość SMS.</span><span class="sxs-lookup"><span data-stu-id="41aac-141">**&lt;Sms&gt;**: Sends an SMS message.</span></span>

### <span data-ttu-id="41aac-142"><a id="TwiML"></a>TwiML</span><span class="sxs-lookup"><span data-stu-id="41aac-142"><a id="TwiML"></a>TwiML</span></span>
<span data-ttu-id="41aac-143">Zestaw instrukcji oparte na języku XML, oparte na powitania usługi Twilio zlecenia, które informują usługi Twilio, jak jest TwiML tooprocess wywołania lub wiadomości SMS.</span><span class="sxs-lookup"><span data-stu-id="41aac-143">TwiML is a set of XML-based instructions based on hello Twilio verbs that inform Twilio of how tooprocess a call or SMS.</span></span>

<span data-ttu-id="41aac-144">Na przykład powitania po TwiML może dokonać konwersji tekstu hello **Hello World** toospeech.</span><span class="sxs-lookup"><span data-stu-id="41aac-144">As an example, hello following TwiML would convert hello text **Hello World** toospeech.</span></span>

    <?xml version="1.0" encoding="UTF-8" ?>
    <Response>
      <Say>Hello World</Say>
    </Response>

<span data-ttu-id="41aac-145">Podczas wywołania aplikacji hello interfejsu API usługi Twilio, jeden z parametrów interfejsu API hello jest adres URL hello, która zwraca odpowiedź TwiML hello.</span><span class="sxs-lookup"><span data-stu-id="41aac-145">When your application calls hello Twilio API, one of hello API parameters is hello URL that returns hello TwiML response.</span></span> <span data-ttu-id="41aac-146">Do celów programistycznych możesz użyć wprowadzone do usługi Twilio adresy URL tooprovide hello TwiML odpowiedzi są używane przez aplikacje.</span><span class="sxs-lookup"><span data-stu-id="41aac-146">For development purposes, you can use Twilio-provided URLs tooprovide hello TwiML responses used by your applications.</span></span> <span data-ttu-id="41aac-147">Może również udostępniać swoje własne adresy URL tooproduce hello TwiML odpowiedzi, a inną opcją jest toouse hello `TwiMLResponse` obiektu.</span><span class="sxs-lookup"><span data-stu-id="41aac-147">You could also host your own URLs tooproduce hello TwiML responses, and another option is toouse hello `TwiMLResponse` object.</span></span>

<span data-ttu-id="41aac-148">Aby uzyskać więcej informacji na temat usługi Twilio zlecenia i ich atrybuty oraz TwiML, zobacz [TwiML][twiml].</span><span class="sxs-lookup"><span data-stu-id="41aac-148">For more information about Twilio verbs, their attributes, and TwiML, see [TwiML][twiml].</span></span> <span data-ttu-id="41aac-149">Aby uzyskać dodatkowe informacje na temat hello interfejsu API usługi Twilio, zobacz [interfejsu API usługi Twilio][twilio_api].</span><span class="sxs-lookup"><span data-stu-id="41aac-149">For additional information about hello Twilio API, see [Twilio API][twilio_api].</span></span>

## <span data-ttu-id="41aac-150"><a id="CreateAccount"></a>Tworzenie konta usługi Twilio</span><span class="sxs-lookup"><span data-stu-id="41aac-150"><a id="CreateAccount"></a>Create a Twilio Account</span></span>
<span data-ttu-id="41aac-151">Gdy wszystko jest gotowe tooget konta usługi Twilio, zarejestruj się w [spróbuj usługi Twilio][try_twilio].</span><span class="sxs-lookup"><span data-stu-id="41aac-151">When you are ready tooget a Twilio account, sign up at [Try Twilio][try_twilio].</span></span> <span data-ttu-id="41aac-152">Można rozpoczynać bezpłatne konto, a następnie Uaktualnij swoje konto później.</span><span class="sxs-lookup"><span data-stu-id="41aac-152">You can start with a free account, and upgrade your account later.</span></span>

<span data-ttu-id="41aac-153">Po utworzeniu konta dla konta usługi Twilio, otrzymasz identyfikator SID konta i tokenu uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="41aac-153">When you sign up for a Twilio account, you receive an account SID and an authentication token.</span></span> <span data-ttu-id="41aac-154">Zarówno będzie potrzebne toomake wywołania interfejsu API usługi Twilio.</span><span class="sxs-lookup"><span data-stu-id="41aac-154">Both will be needed toomake Twilio API calls.</span></span> <span data-ttu-id="41aac-155">tooprevent nieautoryzowany dostęp do konta tooyour, bezpieczeństwo Twojego tokenu uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="41aac-155">tooprevent unauthorized access tooyour account, keep your authentication token secure.</span></span> <span data-ttu-id="41aac-156">Identyfikator SID konta, a token uwierzytelniania jest wyświetlana w hello [usługi Twilio Console][twilio_console]w hello pola oznaczone **identyfikator SID konta** i **TOKEN uwierzytelniania**odpowiednio.</span><span class="sxs-lookup"><span data-stu-id="41aac-156">Your account SID and authentication token are viewable in hello [Twilio Console][twilio_console], in hello fields labeled **ACCOUNT SID** and **AUTH TOKEN**, respectively.</span></span>

## <span data-ttu-id="41aac-157"><a id="create_app"></a>Tworzenie aplikacji Python</span><span class="sxs-lookup"><span data-stu-id="41aac-157"><a id="create_app"></a>Create a Python Application</span></span>
<span data-ttu-id="41aac-158">Nie różni się od innych aplikacji Python, korzystającej z usługi usługi Twilio hello się aplikacji Python, która używa usługi usługi Twilio hello i działa na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="41aac-158">A Python application that uses hello Twilio service and is running in Azure is no different than any other Python application that uses hello Twilio service.</span></span> <span data-ttu-id="41aac-159">Usługi Twilio usług są opartego na interfejsie REST i może zostać wywołana z Python na kilka sposobów, w tym artykule koncentruje się na jak toouse usługi Twilio usług za pomocą [biblioteki usługi Twilio dla języka Python z witryny GitHub][twilio_python].</span><span class="sxs-lookup"><span data-stu-id="41aac-159">While Twilio services are REST-based and can be called from Python in several ways, this article will focus on how toouse Twilio services with [Twilio library for Python from GitHub][twilio_python].</span></span> <span data-ttu-id="41aac-160">Aby uzyskać więcej informacji o używaniu biblioteki usługi Twilio powitania dla języka Python, zobacz [http://readthedocs.org/docs/twilio-python/en/latest/index.html][twilio_lib_docs].</span><span class="sxs-lookup"><span data-stu-id="41aac-160">For more information about using hello Twilio library for Python, see [http://readthedocs.org/docs/twilio-python/en/latest/index.html][twilio_lib_docs].</span></span>

<span data-ttu-id="41aac-161">Pierwsza strona, [konfiguracji nowej maszyny Wirtualnej systemu Linux Azure] [azure_vm_setup] tooact jako hosta dla nowej aplikacji sieci web języka Python.</span><span class="sxs-lookup"><span data-stu-id="41aac-161">First, [set-up a new Azure Linux VM][azure_vm_setup] tooact as a host for your new Python web application.</span></span> <span data-ttu-id="41aac-162">Po hello maszyna wirtualna jest uruchomiona, należy tooexpose aplikacji na port publiczny zgodnie z poniższym opisem.</span><span class="sxs-lookup"><span data-stu-id="41aac-162">Once hello Virtual Machine is running, you will need tooexpose your application on a public port as described below.</span></span>

### <a name="add-an-incoming-rule"></a><span data-ttu-id="41aac-163">Dodawanie reguły przychodzące</span><span class="sxs-lookup"><span data-stu-id="41aac-163">Add An Incoming Rule</span></span>
  1. <span data-ttu-id="41aac-164">Przejdź toohello [sieciowej grupy zabezpieczeń] [azure_nsg] strony.</span><span class="sxs-lookup"><span data-stu-id="41aac-164">Go toohello [Network Security Group][azure_nsg] page.</span></span>
  2. <span data-ttu-id="41aac-165">Wybierz hello grupy zabezpieczeń sieci, która odpowiada z maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="41aac-165">Select hello Network Security Group that corresponds with your Virtual Machine.</span></span>
  3. <span data-ttu-id="41aac-166">Dodaj i **reguły wychodzące** dla **port 80**.</span><span class="sxs-lookup"><span data-stu-id="41aac-166">Add and **Outgoing Rule** for **port 80**.</span></span> <span data-ttu-id="41aac-167">Należy się tooallow przychodzące z dowolnego adresu.</span><span class="sxs-lookup"><span data-stu-id="41aac-167">Be sure tooallow incoming from any address.</span></span>

### <a name="set-hello-dns-name-label"></a><span data-ttu-id="41aac-168">Ustaw hello etykieta nazwy DNS</span><span class="sxs-lookup"><span data-stu-id="41aac-168">Set hello DNS Name Label</span></span>
  1. <span data-ttu-id="41aac-169">Przejdź toohello [hello publicznych adresów IP] [azure_ips] strony.</span><span class="sxs-lookup"><span data-stu-id="41aac-169">Go toohello [hello Public IP Adresses][azure_ips] page.</span></span>
  2. <span data-ttu-id="41aac-170">Wybierz hello publicznego adresu IP tego correspends z maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="41aac-170">Select hello Public IP that correspends with your Virtual Machine.</span></span>
  3. <span data-ttu-id="41aac-171">Zestaw hello **etykieta nazwy DNS** w hello **konfiguracji** sekcji.</span><span class="sxs-lookup"><span data-stu-id="41aac-171">Set hello **DNS Name Label** in hello **Configuration** section.</span></span> <span data-ttu-id="41aac-172">W przypadku hello w tym przykładzie ekran będzie wyglądać następująco *your etykieta domeny*. centralus.cloudapp.azure.com</span><span class="sxs-lookup"><span data-stu-id="41aac-172">In hello case of this example it will look something like this *your-domain-label*.centralus.cloudapp.azure.com</span></span>

<span data-ttu-id="41aac-173">Po tooconnect za pośrednictwem toohello SSH maszyny wirtualnej, można zainstalować hello platforma sieci Web dowolnego (Witaj dwie najbardziej dobrze znany jest Python [Flask](http://flask.pocoo.org/) i [Django](https://www.djangoproject.com)).</span><span class="sxs-lookup"><span data-stu-id="41aac-173">Once you are able tooconnect through SSH toohello Virtual Machine you can install hello Web Framework of your choice (hello two most well known in Python being [Flask](http://flask.pocoo.org/) and [Django](https://www.djangoproject.com)).</span></span> <span data-ttu-id="41aac-174">Każdej z nich można zainstalować tylko uruchamiając hello `pip install` polecenia.</span><span class="sxs-lookup"><span data-stu-id="41aac-174">You can install either of them just by running hello `pip install` command.</span></span>

<span data-ttu-id="41aac-175">Należy pamiętać o tym, czy został skonfigurowany ruchu tooallow maszyn wirtualnych hello tylko na porcie 80.</span><span class="sxs-lookup"><span data-stu-id="41aac-175">Keep in mind that we configured hello Virtual Machine tooallow traffic only on port 80.</span></span> <span data-ttu-id="41aac-176">Upewnij się, że toouse aplikacji hello tooconfigure tego portu.</span><span class="sxs-lookup"><span data-stu-id="41aac-176">So make sure tooconfigure hello application toouse this port.</span></span>

## <span data-ttu-id="41aac-177"><a id="configure_app"></a>Konfigurowanie bibliotek usługi Twilio tooUse Twoja aplikacja</span><span class="sxs-lookup"><span data-stu-id="41aac-177"><a id="configure_app"></a>Configure Your Application tooUse Twilio Libraries</span></span>
<span data-ttu-id="41aac-178">Biblioteki usługi Twilio hello toouse aplikacji dla języka Python można skonfigurować na dwa sposoby:</span><span class="sxs-lookup"><span data-stu-id="41aac-178">You can configure your application toouse hello Twilio library for Python in two ways:</span></span>

* <span data-ttu-id="41aac-179">Zainstaluj biblioteki usługi Twilio powitania dla języka Python w pakiecie narzędzia Pip.</span><span class="sxs-lookup"><span data-stu-id="41aac-179">Install hello Twilio library for Python as a Pip package.</span></span> <span data-ttu-id="41aac-180">Można zainstalować go z hello następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="41aac-180">It can be installed with hello following commands:</span></span>
   
        $ pip install twilio

    <span data-ttu-id="41aac-181">— Lub —</span><span class="sxs-lookup"><span data-stu-id="41aac-181">-OR-</span></span>

* <span data-ttu-id="41aac-182">Pobierz hello usługi Twilio biblioteki dla języka Python z witryny GitHub ([https://github.com/twilio/twilio-python][twilio_python]) i zainstaluj go w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="41aac-182">Download hello Twilio library for Python from GitHub ([https://github.com/twilio/twilio-python][twilio_python]) and install it like this:</span></span>

        $ python setup.py install

<span data-ttu-id="41aac-183">Po zainstalowaniu hello usługi Twilio biblioteki dla języka Python, możesz następnie `import` go w plikach języka Python:</span><span class="sxs-lookup"><span data-stu-id="41aac-183">Once you have installed hello Twilio library for Python, you can then `import` it in your Python files:</span></span>

        import twilio

<span data-ttu-id="41aac-184">Aby uzyskać więcej informacji, zobacz [https://github.com/twilio/twilio-python/blob/master/README.md][twilio_github_readme].</span><span class="sxs-lookup"><span data-stu-id="41aac-184">For more information, see [https://github.com/twilio/twilio-python/blob/master/README.md][twilio_github_readme].</span></span>

## <span data-ttu-id="41aac-185"><a id="howto_make_call"></a>Porady: wykonywanie połączenia wychodzące</span><span class="sxs-lookup"><span data-stu-id="41aac-185"><a id="howto_make_call"></a>How to: Make an outgoing call</span></span>
<span data-ttu-id="41aac-186">powitania po pokazuje, jak wywołać toomake wychodzące.</span><span class="sxs-lookup"><span data-stu-id="41aac-186">hello following shows how toomake an outgoing call.</span></span> <span data-ttu-id="41aac-187">Ten kod zawiera również hello tooreturn lokacja dostarczonych do usługi Twilio odpowiedzi usługi Twilio Markup Language (TwiML).</span><span class="sxs-lookup"><span data-stu-id="41aac-187">This code also uses a Twilio-provided site tooreturn hello Twilio Markup Language (TwiML) response.</span></span> <span data-ttu-id="41aac-188">Podstaw wartości hello **from_number** i **to_number** numerów telefonów i upewnij się, że zostały zweryfikowane hello **from_number** numer telefonu dla konta usługi Twilio przed hello kodu.</span><span class="sxs-lookup"><span data-stu-id="41aac-188">Substitute your values for hello **from_number** and **to_number** phone numbers, and ensure that you've verified hello **from_number** phone number for your Twilio account before running hello code.</span></span>

    from urllib.parse import urlencode

    # Import hello Twilio Python Client.
    from twilio.rest import TwilioRestClient

    # Set your account ID and authentication token.
    account_sid = "your_twilio_account_sid"
    auth_token = "your_twilio_authentication_token"

    # hello number of hello phone initiating hello hello call.
    # This should either be a Twilio number or a number that you've verified
    from_number = "NNNNNNNNNNN"

    # hello number of hello phone receiving call.
    to_number = "NNNNNNNNNNN"

    # Use hello Twilio-provided site for hello TwiML response.
    url = "http://twimlets.com/message?"

    # hello phone message text.
    message = "Hello world."

    # Initialize hello Twilio client.
    client = TwilioRestClient(account_sid, auth_token)

    # Make hello call.
    call = client.calls.create(to=to_number,
                               from_=from_number,
                               url=url + urlencode({'Message': message}))
    print(call.sid)

<span data-ttu-id="41aac-189">Jak wspomniano, ten kod używa hello tooreturn lokacja dostarczonych do usługi Twilio TwiML odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="41aac-189">As mentioned, this code uses a Twilio-provided site tooreturn hello TwiML response.</span></span> <span data-ttu-id="41aac-190">Zamiast tego można użyć własnych lokacji tooprovide hello odpowiedzi TwiML; Aby uzyskać więcej informacji, zobacz [jak tooProvide TwiML odpowiedzi z Twoje własne witryny sieci Web](#howto_provide_twiml_responses).</span><span class="sxs-lookup"><span data-stu-id="41aac-190">You could instead use your own site tooprovide hello TwiML response; for more information, see [How tooProvide TwiML Responses from Your Own Web Site](#howto_provide_twiml_responses).</span></span>

## <span data-ttu-id="41aac-191"><a id="howto_send_sms"></a>Porady: Wyślij wiadomość SMS</span><span class="sxs-lookup"><span data-stu-id="41aac-191"><a id="howto_send_sms"></a>How to: Send an SMS message</span></span>
<span data-ttu-id="41aac-192">Witaj poniżej pokazano, jak hello toosend wiadomość SMS przy użyciu `TwilioRestClient` klasy.</span><span class="sxs-lookup"><span data-stu-id="41aac-192">hello following shows how toosend an SMS message using hello `TwilioRestClient` class.</span></span> <span data-ttu-id="41aac-193">Witaj **from_number** numer jest udostępniany przez usługi Twilio dla wersji próbnej kont toosend wiadomości SMS.</span><span class="sxs-lookup"><span data-stu-id="41aac-193">hello **from_number** number is provided by Twilio for trial accounts toosend SMS messages.</span></span> <span data-ttu-id="41aac-194">Witaj **to_number** numer muszą być weryfikowane dla konta usługi Twilio przed uruchomieniem kodu hello.</span><span class="sxs-lookup"><span data-stu-id="41aac-194">hello **to_number** number must be verified for your Twilio account before running hello code.</span></span>

    # Import hello Twilio Python Client.
    from twilio.rest import TwilioRestClient

    # Set your account ID and authentication token.
    account_sid = "your_twilio_account_sid"
    auth_token = "your_twilio_authentication_token"

    from_number = "NNNNNNNNNNN"  # With trial account, texts can only be sent from your Twilio number.
    to_number = "NNNNNNNNNNN"
    message = "Hello world."

    # Initialize hello Twilio client.
    client = TwilioRestClient(account_sid, auth_token)

    # Send hello SMS message.
    message = client.messages.create(to=to_number,
                                     from_=from_number,
                                     body=message)

## <span data-ttu-id="41aac-195"><a id="howto_provide_twiml_responses"></a>Porady: Podaj TwiML odpowiedzi z własnej witryny sieci Web</span><span class="sxs-lookup"><span data-stu-id="41aac-195"><a id="howto_provide_twiml_responses"></a>How to: Provide TwiML Responses from your own Website</span></span>
<span data-ttu-id="41aac-196">Gdy aplikacja inicjuje toohello wywołania interfejsu API usługi Twilio, usługi Twilio będzie wysyłać adres URL tooa żądania, który jest oczekiwany tooreturn odpowiedzi TwiML.</span><span class="sxs-lookup"><span data-stu-id="41aac-196">When your application initiates a call toohello Twilio API, Twilio will send your request tooa URL that is expected tooreturn a TwiML response.</span></span> <span data-ttu-id="41aac-197">w powyższym przykładzie Hello używa adresu URL dostarczony do usługi Twilio hello [http://twimlets.com/message][twimlet_message_url].</span><span class="sxs-lookup"><span data-stu-id="41aac-197">hello example above uses hello Twilio-provided URL [http://twimlets.com/message][twimlet_message_url].</span></span> <span data-ttu-id="41aac-198">(Podczas TwiML jest przeznaczony do użytku przez usługi Twilio, można wyświetlić ją w przeglądarce.</span><span class="sxs-lookup"><span data-stu-id="41aac-198">(While TwiML is designed for use by Twilio, you can view it in your browser.</span></span> <span data-ttu-id="41aac-199">Na przykład kliknij pozycję [http://twimlets.com/message] [ twimlet_message_url] toosee pustą `<Response>` element; inny przykład kliknij [http://twimlets.com/message? Komunikat % 5B0 %5 D = Hello % 20World] [ twimlet_message_url_hello_world] toosee `<Response>` element, który zawiera `<Say>` elementu.)</span><span class="sxs-lookup"><span data-stu-id="41aac-199">For example, click [http://twimlets.com/message][twimlet_message_url] toosee an empty `<Response>` element; as another example, click [http://twimlets.com/message?Message%5B0%5D=Hello%20World][twimlet_message_url_hello_world] toosee a `<Response>` element that contains a `<Say>` element.)</span></span>

<span data-ttu-id="41aac-200">Zamiast polegania na adres URL udostępniony do usługi Twilio hello, można utworzyć własne lokacji, która zwraca odpowiedzi HTTP.</span><span class="sxs-lookup"><span data-stu-id="41aac-200">Instead of relying on hello Twilio-provided URL, you can create your own site that returns HTTP responses.</span></span> <span data-ttu-id="41aac-201">Można utworzyć witrynę hello w dowolnym języku, który zwraca odpowiedzi XML; w tym temacie założono, że będziesz używać języka Python toocreate hello TwiML.</span><span class="sxs-lookup"><span data-stu-id="41aac-201">You can create hello site in any language that returns XML responses; this topic assumes you will be using Python toocreate hello TwiML.</span></span>

<span data-ttu-id="41aac-202">Hello następujące przykłady dane wyjściowe obejmują odpowiedzi TwiML informacją **Hello World** na powitania wywołania.</span><span class="sxs-lookup"><span data-stu-id="41aac-202">hello following examples will output a TwiML response that says **Hello World** on hello call.</span></span>

<span data-ttu-id="41aac-203">Z Flask:</span><span class="sxs-lookup"><span data-stu-id="41aac-203">With Flask:</span></span>

    from flask import Response
    @app.route("/")
    def hello():
        xml = '<Response><Say>Hello world.</Say></Response>'
        return Response(xml, mimetype='text/xml')

<span data-ttu-id="41aac-204">Przy użyciu platformy Django:</span><span class="sxs-lookup"><span data-stu-id="41aac-204">With Django:</span></span>

    from django.http import HttpResponse
    def hello(request):
        xml = '<Response><Say>Hello world.</Say></Response>'
        return HttpResponse(xml, content_type='text/xml')

<span data-ttu-id="41aac-205">Jak widać w powyższym przykładzie hello hello TwiML odpowiedzi jest po prostu dokumentu XML.</span><span class="sxs-lookup"><span data-stu-id="41aac-205">As you can see from hello example above, hello TwiML response is simply an XML document.</span></span> <span data-ttu-id="41aac-206">Biblioteka usługi Twilio Hello dla języka Python zawiera klasy, które generuje TwiML dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="41aac-206">hello Twilio library for Python contains classes that will generate TwiML for you.</span></span> <span data-ttu-id="41aac-207">Hello poniższy przykład tworzy hello równoważne odpowiedzi, jak pokazano powyżej, ale używa hello `twiml` modułu w bibliotece usługi Twilio hello for Python:</span><span class="sxs-lookup"><span data-stu-id="41aac-207">hello example below produces hello equivalent response as shown above, but uses hello `twiml` module in hello Twilio library for Python:</span></span>

    from twilio import twiml

    response = twiml.Response()
    response.say("Hello world.")
    print(str(response))

<span data-ttu-id="41aac-208">Aby uzyskać więcej informacji o TwiML, zobacz [https://www.twilio.com/docs/api/twiml][twiml_reference].</span><span class="sxs-lookup"><span data-stu-id="41aac-208">For more information about TwiML, see [https://www.twilio.com/docs/api/twiml][twiml_reference].</span></span>

<span data-ttu-id="41aac-209">Po utworzeniu aplikacji Python Konfigurowanie odpowiedzi TwiML tooprovide, użyj hello adres URL aplikacji hello hello adres URL przekazany hello `client.calls.create` metody.</span><span class="sxs-lookup"><span data-stu-id="41aac-209">Once you have your Python application set up tooprovide TwiML responses, use hello URL of hello application as hello URL passed into hello `client.calls.create`  method.</span></span> <span data-ttu-id="41aac-210">Na przykład, jeśli masz aplikację sieci Web o nazwie **MyTwiML** usługi hostowanej wdrożonej tooan Azure, możesz użyć adresu url jako elementu webhook pokazane na powitania poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="41aac-210">For example, if you have a Web application named **MyTwiML** deployed tooan Azure hosted service, you can use its url as webhook as shown in hello following example:</span></span>

    from twilio.rest import TwilioRestClient

    account_sid = "your_twilio_account_sid"
    auth_token = "your_twilio_authentication_token"
    from_number = "NNNNNNNNNNN"
    to_number = "NNNNNNNNNNN"
    url = "http://your-domain-label.centralus.cloudapp.azure.com/MyTwiML/"

    # Initialize hello Twilio client.
    client = TwilioRestClient(account_sid, auth_token)

    # Make hello call.
    call = client.calls.create(to=to_number,
                               from_=from_number,
                               url=url)
    print(call.sid)

## <span data-ttu-id="41aac-211"><a id="AdditionalServices"></a>Porady: korzystania z usługi Twilio dodatkowych usług</span><span class="sxs-lookup"><span data-stu-id="41aac-211"><a id="AdditionalServices"></a>How to: Use Additional Twilio Services</span></span>
<span data-ttu-id="41aac-212">Ponadto przykłady toohello pokazane, usługi Twilio oferuje API sieci web można używać tooleverage dodatkowe usługi Twilio funkcji z aplikacji Azure.</span><span class="sxs-lookup"><span data-stu-id="41aac-212">In addition toohello examples shown here, Twilio offers web-based APIs that you can use tooleverage additional Twilio functionality from your Azure application.</span></span> <span data-ttu-id="41aac-213">Aby uzyskać szczegółowe informacje, zobacz hello [dokumentacji interfejsu API usługi Twilio][twilio_api].</span><span class="sxs-lookup"><span data-stu-id="41aac-213">For full details, see hello [Twilio API documentation][twilio_api].</span></span>

## <span data-ttu-id="41aac-214"><a id="NextSteps"></a>Następne kroki</span><span class="sxs-lookup"><span data-stu-id="41aac-214"><a id="NextSteps"></a>Next Steps</span></span>
<span data-ttu-id="41aac-215">Teraz, kiedy znasz już podstawy hello hello usługi usługi Twilio, wykonaj te więcej toolearn łącza:</span><span class="sxs-lookup"><span data-stu-id="41aac-215">Now that you have learned hello basics of hello Twilio service, follow these links toolearn more:</span></span>

* <span data-ttu-id="41aac-216">[Wytyczne dotyczące zabezpieczeń usługi Twilio][twilio_security_guidelines]</span><span class="sxs-lookup"><span data-stu-id="41aac-216">[Twilio Security Guidelines][twilio_security_guidelines]</span></span>
* <span data-ttu-id="41aac-217">[Porada usługi Twilio prowadnice i przykładowy kod][twilio_howtos]</span><span class="sxs-lookup"><span data-stu-id="41aac-217">[Twilio HowTo Guides and Example Code][twilio_howtos]</span></span>
* <span data-ttu-id="41aac-218">[Samouczki usługi Twilio Szybki Start][twilio_quickstarts]</span><span class="sxs-lookup"><span data-stu-id="41aac-218">[Twilio Quickstart Tutorials][twilio_quickstarts]</span></span>
* <span data-ttu-id="41aac-219">[Usługi Twilio w witrynie GitHub][twilio_on_github]</span><span class="sxs-lookup"><span data-stu-id="41aac-219">[Twilio on GitHub][twilio_on_github]</span></span>
* <span data-ttu-id="41aac-220">[Porozmawiaj tooTwilio pomocy technicznej][twilio_support]</span><span class="sxs-lookup"><span data-stu-id="41aac-220">[Talk tooTwilio Support][twilio_support]</span></span>

[special_offer]: http://ahoy.twilio.com/azure
[twilio_python]: https://github.com/twilio/twilio-python
[twilio_lib_docs]: http://readthedocs.org/docs/twilio-python/en/latest/index.html
[twilio_github_readme]: https://github.com/twilio/twilio-python/blob/master/README.md

[twimlet_message_url]: http://twimlets.com/message
[twimlet_message_url_hello_world]: http://twimlets.com/message?Message%5B0%5D=Hello%20World
[twiml_reference]: https://www.twilio.com/docs/api/twiml
[twilio_pricing]: http://www.twilio.com/pricing

[twilio_libraries]: https://www.twilio.com/docs/libraries
[twiml]: http://www.twilio.com/docs/api/twiml
[twilio_api]: http://www.twilio.com/api
[try_twilio]: https://www.twilio.com/try-twilio
[twilio_console]:  https://www.twilio.com/console
[twilio_security_guidelines]: http://www.twilio.com/docs/security
[twilio_howtos]: http://www.twilio.com/docs/howto
[twilio_on_github]: https://github.com/twilio
[twilio_support]: http://www.twilio.com/help/contact
[twilio_quickstarts]: http://www.twilio.com/docs/quickstart
