---
title: "Jak używać usługi Twilio głosowe i programu SMS (Python) | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak wykonać połączenie telefoniczne i wysłać wiadomość SMS z usługi interfejsu API usługi Twilio na platformie Azure. Przykłady kodu napisane w języku Python."
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
ms.openlocfilehash: f4a02bb7a7c46e7a0e3c75b870c522eae8294339
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-twilio-for-voice-and-sms-capabilities-in-python"></a><span data-ttu-id="d4a37-104">Jak używać usługi Twilio głosowe i możliwości programu SMS w języku Python</span><span class="sxs-lookup"><span data-stu-id="d4a37-104">How to Use Twilio for Voice and SMS Capabilities in Python</span></span>
<span data-ttu-id="d4a37-105">W tym przewodniku przedstawiono sposób wykonywania typowych zadań programowania usługi interfejsu API usługi Twilio na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="d4a37-105">This guide demonstrates how to perform common programming tasks with the Twilio API service on Azure.</span></span> <span data-ttu-id="d4a37-106">Omówione scenariusze obejmują tworzenie połączeń telefonicznych i wysyłanie wiadomości krótką wiadomość usługi (SMS).</span><span class="sxs-lookup"><span data-stu-id="d4a37-106">The scenarios covered include making a phone call and sending a Short Message Service (SMS) message.</span></span> <span data-ttu-id="d4a37-107">Aby uzyskać więcej informacji na temat usługi Twilio i komunikacja głosowa programu SMS w aplikacji, zobacz [następne kroki](#NextSteps) sekcji.</span><span class="sxs-lookup"><span data-stu-id="d4a37-107">For more information on Twilio and using voice and SMS in your applications, see the [Next Steps](#NextSteps) section.</span></span>

## <span data-ttu-id="d4a37-108"><a id="WhatIs"></a>Co to jest usługi Twilio?</span><span class="sxs-lookup"><span data-stu-id="d4a37-108"><a id="WhatIs"></a>What is Twilio?</span></span>
<span data-ttu-id="d4a37-109">Usługi Twilio jest włączanie przyszłości komunikacji biznesowej, umożliwiają deweloperom osadzać głosowych, VoIP i wiadomości do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d4a37-109">Twilio is powering the future of business communications, enabling developers to embed voice, VoIP, and messaging into applications.</span></span> <span data-ttu-id="d4a37-110">Zwirtualizuj one wszystkich infrastrukturę potrzebną w środowisku chmury, globalnych ujawnienie go za pośrednictwem platformy komunikacji interfejsu API usługi Twilio.</span><span class="sxs-lookup"><span data-stu-id="d4a37-110">They virtualize all infrastructure needed in a cloud-based, global environment, exposing it through the Twilio communications API platform.</span></span> <span data-ttu-id="d4a37-111">Aplikacje są proste tworzenie i skalowalności.</span><span class="sxs-lookup"><span data-stu-id="d4a37-111">Applications are simple to build and scalable.</span></span> <span data-ttu-id="d4a37-112">Kredyty elastyczność Tobie płatności — jako Przejdź ceny i korzystać z niej niezawodności chmury.</span><span class="sxs-lookup"><span data-stu-id="d4a37-112">Enjoy flexibility with pay-as-you go pricing, and benefit from cloud reliability.</span></span>

<span data-ttu-id="d4a37-113">**Usługi Twilio głosu** umożliwia aplikacjom wykonywanie i odbieranie połączeń telefonicznych.</span><span class="sxs-lookup"><span data-stu-id="d4a37-113">**Twilio Voice** allows your applications to make and receive phone calls.</span></span>
<span data-ttu-id="d4a37-114">**SMS usługi Twilio** umożliwia aplikacji wysyłanie i odbieranie wiadomości tekstowych.</span><span class="sxs-lookup"><span data-stu-id="d4a37-114">**Twilio SMS** enables your application to send and receive text messages.</span></span>
<span data-ttu-id="d4a37-115">**Klient usługi Twilio** służy do nawiązywania połączeń VoIP z dowolnego telefonu, tabletu lub przeglądarki i obsługuje WebRTC.</span><span class="sxs-lookup"><span data-stu-id="d4a37-115">**Twilio Client** allows you to make VoIP calls from any phone, tablet, or browser and supports WebRTC.</span></span>

## <span data-ttu-id="d4a37-116"><a id="Pricing"></a>Cennik usługi Twilio i oferty specjalne</span><span class="sxs-lookup"><span data-stu-id="d4a37-116"><a id="Pricing"></a>Twilio Pricing and Special Offers</span></span>
<span data-ttu-id="d4a37-117">Azure klienci otrzymają [oferta specjalna] [ special_offer] 10 $ środków usługi Twilio po uaktualnieniu konta usługi Twilio.</span><span class="sxs-lookup"><span data-stu-id="d4a37-117">Azure customers receive a [special offer][special_offer] $10 of Twilio Credit when you upgrade your Twilio Account.</span></span> <span data-ttu-id="d4a37-118">Środki tej usługi Twilio można zastosować do bez użycia usługi Twilio (równoznaczne z wysyłaniem wiadomości SMS maksymalnie 1000 lub odbieranie maksymalnie 1000 przychodzących minut głosu w zależności od lokalizacji telefonu przeznaczenia numer i komunikatu lub wywołania kredyt $10).</span><span class="sxs-lookup"><span data-stu-id="d4a37-118">This Twilio Credit can be applied to any Twilio usage ($10 credit equivalent to sending as many as 1,000 SMS messages or receiving up to 1000 inbound Voice minutes, depending on the location of your phone number and message or call destination).</span></span> <span data-ttu-id="d4a37-119">Zrealizować to [środki usługi Twilio] [ special_offer] i rozpocząć pracę.</span><span class="sxs-lookup"><span data-stu-id="d4a37-119">Redeem this [Twilio credit][special_offer] and get started.</span></span>

<span data-ttu-id="d4a37-120">Usługi Twilio jest z usługą.</span><span class="sxs-lookup"><span data-stu-id="d4a37-120">Twilio is a pay-as-you-go service.</span></span> <span data-ttu-id="d4a37-121">Nie żadne opłaty konfiguracji i w dowolnej chwili możesz zamknąć konto.</span><span class="sxs-lookup"><span data-stu-id="d4a37-121">There are no set-up fees and you can close your account at any time.</span></span> <span data-ttu-id="d4a37-122">Można znaleźć więcej szczegółów na [cennik usługi Twilio][twilio_pricing].</span><span class="sxs-lookup"><span data-stu-id="d4a37-122">You can find more details at [Twilio Pricing][twilio_pricing].</span></span>

## <span data-ttu-id="d4a37-123"><a id="Concepts"></a>Pojęcia</span><span class="sxs-lookup"><span data-stu-id="d4a37-123"><a id="Concepts"></a>Concepts</span></span>
<span data-ttu-id="d4a37-124">Interfejs API usługi Twilio jest interfejs API RESTful, która zapewnia funkcje programu SMS i komunikacja głosowa aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d4a37-124">The Twilio API is a RESTful API that provides voice and SMS functionality for applications.</span></span> <span data-ttu-id="d4a37-125">Klient biblioteki są dostępne w wielu językach; Aby uzyskać listę, zobacz [bibliotek interfejsu API usługi Twilio][twilio_libraries].</span><span class="sxs-lookup"><span data-stu-id="d4a37-125">Client libraries are available in multiple languages; for a list, see [Twilio API Libraries][twilio_libraries].</span></span>

<span data-ttu-id="d4a37-126">Kluczowe aspekty interfejsu API usługi Twilio są zleceń usługi Twilio i usługi Twilio Markup Language (TwiML).</span><span class="sxs-lookup"><span data-stu-id="d4a37-126">Key aspects of the Twilio API are Twilio verbs and Twilio Markup Language (TwiML).</span></span>

### <span data-ttu-id="d4a37-127"><a id="Verbs"></a>Usługi Twilio zlecenia</span><span class="sxs-lookup"><span data-stu-id="d4a37-127"><a id="Verbs"></a>Twilio Verbs</span></span>
<span data-ttu-id="d4a37-128">Interfejs API korzysta z usługi Twilio zleceń; na przykład  **&lt;powiedzieć&gt;**  zlecenie powoduje, że usługi Twilio komputerowi dostarczenia komunikatu w wywołaniu.</span><span class="sxs-lookup"><span data-stu-id="d4a37-128">The API makes use of Twilio verbs; for example, the **&lt;Say&gt;** verb instructs Twilio to audibly deliver a message on a call.</span></span>

<span data-ttu-id="d4a37-129">Poniżej znajduje się lista zleceń usługi Twilio.</span><span class="sxs-lookup"><span data-stu-id="d4a37-129">The following is a list of Twilio verbs.</span></span> <span data-ttu-id="d4a37-130">Dowiedz się więcej o innych poleceń i możliwości za pośrednictwem [dokumentacji usługi Twilio Markup Language][twiml].</span><span class="sxs-lookup"><span data-stu-id="d4a37-130">Learn about the other verbs and capabilities via [Twilio Markup Language documentation][twiml].</span></span>

* <span data-ttu-id="d4a37-131">**&lt;Wybierania&gt;**: łączy wywołującego innego numeru telefonu.</span><span class="sxs-lookup"><span data-stu-id="d4a37-131">**&lt;Dial&gt;**: Connects the caller to another phone.</span></span>
* <span data-ttu-id="d4a37-132">**&lt;Zbierz&gt;**: zbiera cyfry wprowadzone na klawiaturze telefonu.</span><span class="sxs-lookup"><span data-stu-id="d4a37-132">**&lt;Gather&gt;**: Collects numeric digits entered on the telephone keypad.</span></span>
* <span data-ttu-id="d4a37-133">**&lt;Rozłączanie&gt;**: kończy wywołanie.</span><span class="sxs-lookup"><span data-stu-id="d4a37-133">**&lt;Hangup&gt;**: Ends a call.</span></span>
* <span data-ttu-id="d4a37-134">**&lt;Wstrzymaj&gt;**: dyskretnie czeka na określoną liczbę sekund.</span><span class="sxs-lookup"><span data-stu-id="d4a37-134">**&lt;Pause&gt;**: Waits silently for a specified number of seconds.</span></span>
* <span data-ttu-id="d4a37-135">**&lt;Odtwórz&gt;**: odtwarzania pliku audio.</span><span class="sxs-lookup"><span data-stu-id="d4a37-135">**&lt;Play&gt;**: Plays an audio file.</span></span>
* <span data-ttu-id="d4a37-136">**&lt;Kolejka&gt;**: Dodaj do kolejki obiekty wywołujące.</span><span class="sxs-lookup"><span data-stu-id="d4a37-136">**&lt;Queue&gt;**: Add the to a queue of callers.</span></span>
* <span data-ttu-id="d4a37-137">**&lt;Rekord&gt;**: rejestruje głos wywołującego i zwraca adres URL pliku zawierającego nagrywania.</span><span class="sxs-lookup"><span data-stu-id="d4a37-137">**&lt;Record&gt;**: Records the voice of the caller and returns a URL of a file that contains the recording.</span></span>
* <span data-ttu-id="d4a37-138">**&lt;Przekieruj&gt;**: przekazuje kontrolę nad wywołania lub wiadomości SMS do TwiML na inny adres URL.</span><span class="sxs-lookup"><span data-stu-id="d4a37-138">**&lt;Redirect&gt;**: Transfers control of a call or SMS to the TwiML at a different URL.</span></span>
* <span data-ttu-id="d4a37-139">**&lt;Odrzuć&gt;**: odrzucanie połączenia przychodzącego na numer usługi Twilio bez rozliczeń można.</span><span class="sxs-lookup"><span data-stu-id="d4a37-139">**&lt;Reject&gt;**: Rejects an incoming call to your Twilio number without billing you.</span></span>
* <span data-ttu-id="d4a37-140">**&lt;Powiedz&gt;**: Konwertuje tekst na mowę, które zostało utworzone w wywołaniu.</span><span class="sxs-lookup"><span data-stu-id="d4a37-140">**&lt;Say&gt;**: Converts text to speech that is made on a call.</span></span>
* <span data-ttu-id="d4a37-141">**&lt;SMS&gt;**: wysyła wiadomość SMS.</span><span class="sxs-lookup"><span data-stu-id="d4a37-141">**&lt;Sms&gt;**: Sends an SMS message.</span></span>

### <span data-ttu-id="d4a37-142"><a id="TwiML"></a>TwiML</span><span class="sxs-lookup"><span data-stu-id="d4a37-142"><a id="TwiML"></a>TwiML</span></span>
<span data-ttu-id="d4a37-143">TwiML to zestaw instrukcji oparte na języku XML, oparte na zlecenia usługi Twilio, które informują usługi Twilio sposobu przetwarzania połączenia lub wiadomości SMS.</span><span class="sxs-lookup"><span data-stu-id="d4a37-143">TwiML is a set of XML-based instructions based on the Twilio verbs that inform Twilio of how to process a call or SMS.</span></span>

<span data-ttu-id="d4a37-144">Na przykład następujące TwiML czy Konwertuj tekst **Hello World** do rozpoznawania mowy.</span><span class="sxs-lookup"><span data-stu-id="d4a37-144">As an example, the following TwiML would convert the text **Hello World** to speech.</span></span>

    <?xml version="1.0" encoding="UTF-8" ?>
    <Response>
      <Say>Hello World</Say>
    </Response>

<span data-ttu-id="d4a37-145">Gdy aplikacja wywołuje interfejs API usługi Twilio, jeden z parametrów interfejsu API jest adres URL, który zwraca odpowiedź TwiML.</span><span class="sxs-lookup"><span data-stu-id="d4a37-145">When your application calls the Twilio API, one of the API parameters is the URL that returns the TwiML response.</span></span> <span data-ttu-id="d4a37-146">Do celów programistycznych wprowadzone do usługi Twilio adresy URL służy do nadania odpowiedzi TwiML używane przez aplikacje.</span><span class="sxs-lookup"><span data-stu-id="d4a37-146">For development purposes, you can use Twilio-provided URLs to provide the TwiML responses used by your applications.</span></span> <span data-ttu-id="d4a37-147">Może również udostępniać swoje własne adresy URL do tworzenia odpowiedzi TwiML i inną opcją jest użycie `TwiMLResponse` obiektu.</span><span class="sxs-lookup"><span data-stu-id="d4a37-147">You could also host your own URLs to produce the TwiML responses, and another option is to use the `TwiMLResponse` object.</span></span>

<span data-ttu-id="d4a37-148">Aby uzyskać więcej informacji na temat usługi Twilio zlecenia i ich atrybuty oraz TwiML, zobacz [TwiML][twiml].</span><span class="sxs-lookup"><span data-stu-id="d4a37-148">For more information about Twilio verbs, their attributes, and TwiML, see [TwiML][twiml].</span></span> <span data-ttu-id="d4a37-149">Aby uzyskać dodatkowe informacje na temat interfejsu API usługi Twilio, zobacz [interfejsu API usługi Twilio][twilio_api].</span><span class="sxs-lookup"><span data-stu-id="d4a37-149">For additional information about the Twilio API, see [Twilio API][twilio_api].</span></span>

## <span data-ttu-id="d4a37-150"><a id="CreateAccount"></a>Tworzenie konta usługi Twilio</span><span class="sxs-lookup"><span data-stu-id="d4a37-150"><a id="CreateAccount"></a>Create a Twilio Account</span></span>
<span data-ttu-id="d4a37-151">Gdy wszystko będzie gotowe, można uzyskać konta usługi Twilio, zarejestruj się w [spróbuj usługi Twilio][try_twilio].</span><span class="sxs-lookup"><span data-stu-id="d4a37-151">When you are ready to get a Twilio account, sign up at [Try Twilio][try_twilio].</span></span> <span data-ttu-id="d4a37-152">Można rozpoczynać bezpłatne konto, a następnie Uaktualnij swoje konto później.</span><span class="sxs-lookup"><span data-stu-id="d4a37-152">You can start with a free account, and upgrade your account later.</span></span>

<span data-ttu-id="d4a37-153">Po utworzeniu konta dla konta usługi Twilio, otrzymasz identyfikator SID konta i tokenu uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="d4a37-153">When you sign up for a Twilio account, you receive an account SID and an authentication token.</span></span> <span data-ttu-id="d4a37-154">Zarówno będą potrzebne w celu wykonywania wywołań interfejsu API usługi Twilio.</span><span class="sxs-lookup"><span data-stu-id="d4a37-154">Both will be needed to make Twilio API calls.</span></span> <span data-ttu-id="d4a37-155">Aby uniemożliwić nieautoryzowany dostęp do Twojego konta, bezpieczeństwo Twojego tokenu uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="d4a37-155">To prevent unauthorized access to your account, keep your authentication token secure.</span></span> <span data-ttu-id="d4a37-156">Identyfikator SID konta, a token uwierzytelniania jest wyświetlana w [usługi Twilio Console][twilio_console], w polach etykietą **identyfikator SID konta** i **TOKEN uwierzytelniania**odpowiednio.</span><span class="sxs-lookup"><span data-stu-id="d4a37-156">Your account SID and authentication token are viewable in the [Twilio Console][twilio_console], in the fields labeled **ACCOUNT SID** and **AUTH TOKEN**, respectively.</span></span>

## <span data-ttu-id="d4a37-157"><a id="create_app"></a>Tworzenie aplikacji Python</span><span class="sxs-lookup"><span data-stu-id="d4a37-157"><a id="create_app"></a>Create a Python Application</span></span>
<span data-ttu-id="d4a37-158">Nie różni się od innych aplikacji Python, korzystającą z usługi Twilio usługi się aplikacji Python, która używa usługi usługi Twilio i działa na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="d4a37-158">A Python application that uses the Twilio service and is running in Azure is no different than any other Python application that uses the Twilio service.</span></span> <span data-ttu-id="d4a37-159">Usługi Twilio usług są opartego na interfejsie REST i może zostać wywołana z Python na kilka sposobów, w tym artykule dotyczą sposobu korzystania z usługi Twilio usług w programie [biblioteki usługi Twilio dla języka Python z witryny GitHub][twilio_python].</span><span class="sxs-lookup"><span data-stu-id="d4a37-159">While Twilio services are REST-based and can be called from Python in several ways, this article will focus on how to use Twilio services with [Twilio library for Python from GitHub][twilio_python].</span></span> <span data-ttu-id="d4a37-160">Aby uzyskać więcej informacji dotyczących korzystania z biblioteki usługi Twilio dla języka Python, zobacz [http://readthedocs.org/docs/twilio-python/en/latest/index.html][twilio_lib_docs].</span><span class="sxs-lookup"><span data-stu-id="d4a37-160">For more information about using the Twilio library for Python, see [http://readthedocs.org/docs/twilio-python/en/latest/index.html][twilio_lib_docs].</span></span>

<span data-ttu-id="d4a37-161">Pierwsza strona, [konfiguracji nowej maszyny Wirtualnej systemu Linux Azure] [azure_vm_setup] do działania jako hosta dla aplikacji sieci web z nowego języka Python.</span><span class="sxs-lookup"><span data-stu-id="d4a37-161">First, [set-up a new Azure Linux VM][azure_vm_setup] to act as a host for your new Python web application.</span></span> <span data-ttu-id="d4a37-162">Gdy maszyna wirtualna jest uruchomiona, należy udostępnić aplikacji na port publiczny, zgodnie z poniższym opisem.</span><span class="sxs-lookup"><span data-stu-id="d4a37-162">Once the Virtual Machine is running, you will need to expose your application on a public port as described below.</span></span>

### <a name="add-an-incoming-rule"></a><span data-ttu-id="d4a37-163">Dodawanie reguły przychodzące</span><span class="sxs-lookup"><span data-stu-id="d4a37-163">Add An Incoming Rule</span></span>
  1. <span data-ttu-id="d4a37-164">Przejdź do strony [sieciowej grupy zabezpieczeń] [azure_nsg].</span><span class="sxs-lookup"><span data-stu-id="d4a37-164">Go to the [Network Security Group][azure_nsg] page.</span></span>
  2. <span data-ttu-id="d4a37-165">Wybierz grupy zabezpieczeń sieci, która odpowiada z maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="d4a37-165">Select the Network Security Group that corresponds with your Virtual Machine.</span></span>
  3. <span data-ttu-id="d4a37-166">Dodaj i **reguły wychodzące** dla **port 80**.</span><span class="sxs-lookup"><span data-stu-id="d4a37-166">Add and **Outgoing Rule** for **port 80**.</span></span> <span data-ttu-id="d4a37-167">Pamiętaj umożliwić przychodzące z dowolnego adresu.</span><span class="sxs-lookup"><span data-stu-id="d4a37-167">Be sure to allow incoming from any address.</span></span>

### <a name="set-the-dns-name-label"></a><span data-ttu-id="d4a37-168">Ustaw etykieta nazwy DNS</span><span class="sxs-lookup"><span data-stu-id="d4a37-168">Set the DNS Name Label</span></span>
  1. <span data-ttu-id="d4a37-169">Przejdź do strony [publicznego adresu IP adresów] [azure_ips].</span><span class="sxs-lookup"><span data-stu-id="d4a37-169">Go to the [The Public IP Adresses][azure_ips] page.</span></span>
  2. <span data-ttu-id="d4a37-170">Wybierz publiczny adres IP tego correspends z maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="d4a37-170">Select the Public IP that correspends with your Virtual Machine.</span></span>
  3. <span data-ttu-id="d4a37-171">Ustaw **etykieta nazwy DNS** w **konfiguracji** sekcji.</span><span class="sxs-lookup"><span data-stu-id="d4a37-171">Set the **DNS Name Label** in the **Configuration** section.</span></span> <span data-ttu-id="d4a37-172">W tym przykładzie ekran będzie wyglądać następująco *your etykieta domeny*. centralus.cloudapp.azure.com</span><span class="sxs-lookup"><span data-stu-id="d4a37-172">In the case of this example it will look something like this *your-domain-label*.centralus.cloudapp.azure.com</span></span>

<span data-ttu-id="d4a37-173">Po przejściu łączenie się za pośrednictwem protokołu SSH z maszyną wirtualną można zainstalować struktura sieci Web dowolnego (najbardziej dobrze znany jest Python dwa [Flask](http://flask.pocoo.org/) i [Django](https://www.djangoproject.com)).</span><span class="sxs-lookup"><span data-stu-id="d4a37-173">Once you are able to connect through SSH to the Virtual Machine you can install the Web Framework of your choice (the two most well known in Python being [Flask](http://flask.pocoo.org/) and [Django](https://www.djangoproject.com)).</span></span> <span data-ttu-id="d4a37-174">Można zainstalować jedną z nich tylko przez uruchomienie `pip install` polecenia.</span><span class="sxs-lookup"><span data-stu-id="d4a37-174">You can install either of them just by running the `pip install` command.</span></span>

<span data-ttu-id="d4a37-175">Należy pamiętać, że został skonfigurowany maszynę wirtualną, aby zezwolić na ruch tylko na porcie 80.</span><span class="sxs-lookup"><span data-stu-id="d4a37-175">Keep in mind that we configured the Virtual Machine to allow traffic only on port 80.</span></span> <span data-ttu-id="d4a37-176">Dlatego upewnij się skonfigurować aplikację do użycia tego portu.</span><span class="sxs-lookup"><span data-stu-id="d4a37-176">So make sure to configure the application to use this port.</span></span>

## <span data-ttu-id="d4a37-177"><a id="configure_app"></a>Konfigurowanie aplikacji przy użyciu bibliotek usługi Twilio</span><span class="sxs-lookup"><span data-stu-id="d4a37-177"><a id="configure_app"></a>Configure Your Application to Use Twilio Libraries</span></span>
<span data-ttu-id="d4a37-178">Można skonfigurować aplikację do korzystania z biblioteki usługi Twilio dla języka Python na dwa sposoby:</span><span class="sxs-lookup"><span data-stu-id="d4a37-178">You can configure your application to use the Twilio library for Python in two ways:</span></span>

* <span data-ttu-id="d4a37-179">Zainstaluj biblioteki usługi Twilio dla języka Python w pakiecie narzędzia Pip.</span><span class="sxs-lookup"><span data-stu-id="d4a37-179">Install the Twilio library for Python as a Pip package.</span></span> <span data-ttu-id="d4a37-180">Można go zainstalować za pomocą następujących poleceń:</span><span class="sxs-lookup"><span data-stu-id="d4a37-180">It can be installed with the following commands:</span></span>
   
        $ pip install twilio

    <span data-ttu-id="d4a37-181">— Lub —</span><span class="sxs-lookup"><span data-stu-id="d4a37-181">-OR-</span></span>

* <span data-ttu-id="d4a37-182">Pobierz biblioteki usługi Twilio dla języka Python z witryny GitHub ([https://github.com/twilio/twilio-python][twilio_python]) i zainstaluj go w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="d4a37-182">Download the Twilio library for Python from GitHub ([https://github.com/twilio/twilio-python][twilio_python]) and install it like this:</span></span>

        $ python setup.py install

<span data-ttu-id="d4a37-183">Po zainstalowaniu biblioteki usługi Twilio dla języka Python, możesz następnie `import` go w plikach języka Python:</span><span class="sxs-lookup"><span data-stu-id="d4a37-183">Once you have installed the Twilio library for Python, you can then `import` it in your Python files:</span></span>

        import twilio

<span data-ttu-id="d4a37-184">Aby uzyskać więcej informacji, zobacz [https://github.com/twilio/twilio-python/blob/master/README.md][twilio_github_readme].</span><span class="sxs-lookup"><span data-stu-id="d4a37-184">For more information, see [https://github.com/twilio/twilio-python/blob/master/README.md][twilio_github_readme].</span></span>

## <span data-ttu-id="d4a37-185"><a id="howto_make_call"></a>Porady: wykonywanie połączenia wychodzące</span><span class="sxs-lookup"><span data-stu-id="d4a37-185"><a id="howto_make_call"></a>How to: Make an outgoing call</span></span>
<span data-ttu-id="d4a37-186">Poniżej przedstawiono sposób wywoływania wychodzących.</span><span class="sxs-lookup"><span data-stu-id="d4a37-186">The following shows how to make an outgoing call.</span></span> <span data-ttu-id="d4a37-187">Ten kod zawiera również lokacja dostarczonych do usługi Twilio do zwracania odpowiedzi usługi Twilio Markup Language (TwiML).</span><span class="sxs-lookup"><span data-stu-id="d4a37-187">This code also uses a Twilio-provided site to return the Twilio Markup Language (TwiML) response.</span></span> <span data-ttu-id="d4a37-188">Podstaw wartości **from_number** i **to_number** numerów telefonów i upewnij się, że zostały zweryfikowane **from_number** numer telefonu dla konta usługi Twilio przed uruchomieniem kodu.</span><span class="sxs-lookup"><span data-stu-id="d4a37-188">Substitute your values for the **from_number** and **to_number** phone numbers, and ensure that you've verified the **from_number** phone number for your Twilio account before running the code.</span></span>

    from urllib.parse import urlencode

    # Import the Twilio Python Client.
    from twilio.rest import TwilioRestClient

    # Set your account ID and authentication token.
    account_sid = "your_twilio_account_sid"
    auth_token = "your_twilio_authentication_token"

    # The number of the phone initiating the the call.
    # This should either be a Twilio number or a number that you've verified
    from_number = "NNNNNNNNNNN"

    # The number of the phone receiving call.
    to_number = "NNNNNNNNNNN"

    # Use the Twilio-provided site for the TwiML response.
    url = "http://twimlets.com/message?"

    # The phone message text.
    message = "Hello world."

    # Initialize the Twilio client.
    client = TwilioRestClient(account_sid, auth_token)

    # Make the call.
    call = client.calls.create(to=to_number,
                               from_=from_number,
                               url=url + urlencode({'Message': message}))
    print(call.sid)

<span data-ttu-id="d4a37-189">Jak wspomniano, ten kod używa lokacja dostarczonych do usługi Twilio do zwracania odpowiedzi TwiML.</span><span class="sxs-lookup"><span data-stu-id="d4a37-189">As mentioned, this code uses a Twilio-provided site to return the TwiML response.</span></span> <span data-ttu-id="d4a37-190">Własnej witryny można zamiast tego użyć, aby zapewnić odpowiedzi TwiML; Aby uzyskać więcej informacji, zobacz [jak zapewnić TwiML odpowiedzi z Twoje własne witryny sieci Web](#howto_provide_twiml_responses).</span><span class="sxs-lookup"><span data-stu-id="d4a37-190">You could instead use your own site to provide the TwiML response; for more information, see [How to Provide TwiML Responses from Your Own Web Site](#howto_provide_twiml_responses).</span></span>

## <span data-ttu-id="d4a37-191"><a id="howto_send_sms"></a>Porady: Wyślij wiadomość SMS</span><span class="sxs-lookup"><span data-stu-id="d4a37-191"><a id="howto_send_sms"></a>How to: Send an SMS message</span></span>
<span data-ttu-id="d4a37-192">Poniżej pokazano, jak wysyłać wiadomość SMS przy użyciu `TwilioRestClient` klasy.</span><span class="sxs-lookup"><span data-stu-id="d4a37-192">The following shows how to send an SMS message using the `TwilioRestClient` class.</span></span> <span data-ttu-id="d4a37-193">**From_number** numer jest udostępniany przez usługi Twilio dla konta wersji próbnej można wysłać wiadomości SMS.</span><span class="sxs-lookup"><span data-stu-id="d4a37-193">The **from_number** number is provided by Twilio for trial accounts to send SMS messages.</span></span> <span data-ttu-id="d4a37-194">**To_number** numer muszą być weryfikowane dla konta usługi Twilio przed uruchomieniem kodu.</span><span class="sxs-lookup"><span data-stu-id="d4a37-194">The **to_number** number must be verified for your Twilio account before running the code.</span></span>

    # Import the Twilio Python Client.
    from twilio.rest import TwilioRestClient

    # Set your account ID and authentication token.
    account_sid = "your_twilio_account_sid"
    auth_token = "your_twilio_authentication_token"

    from_number = "NNNNNNNNNNN"  # With trial account, texts can only be sent from your Twilio number.
    to_number = "NNNNNNNNNNN"
    message = "Hello world."

    # Initialize the Twilio client.
    client = TwilioRestClient(account_sid, auth_token)

    # Send the SMS message.
    message = client.messages.create(to=to_number,
                                     from_=from_number,
                                     body=message)

## <span data-ttu-id="d4a37-195"><a id="howto_provide_twiml_responses"></a>Porady: Podaj TwiML odpowiedzi z własnej witryny sieci Web</span><span class="sxs-lookup"><span data-stu-id="d4a37-195"><a id="howto_provide_twiml_responses"></a>How to: Provide TwiML Responses from your own Website</span></span>
<span data-ttu-id="d4a37-196">Gdy aplikacja jest inicjowany przez wywołanie interfejsu API usługi Twilio, usługi Twilio wysyła żądanie do adresu URL, który powinien zwrócić odpowiedzi TwiML.</span><span class="sxs-lookup"><span data-stu-id="d4a37-196">When your application initiates a call to the Twilio API, Twilio will send your request to a URL that is expected to return a TwiML response.</span></span> <span data-ttu-id="d4a37-197">W powyższym przykładzie korzysta z adresu URL dostarczony do usługi Twilio [http://twimlets.com/message][twimlet_message_url].</span><span class="sxs-lookup"><span data-stu-id="d4a37-197">The example above uses the Twilio-provided URL [http://twimlets.com/message][twimlet_message_url].</span></span> <span data-ttu-id="d4a37-198">(Podczas TwiML jest przeznaczony do użytku przez usługi Twilio, można wyświetlić ją w przeglądarce.</span><span class="sxs-lookup"><span data-stu-id="d4a37-198">(While TwiML is designed for use by Twilio, you can view it in your browser.</span></span> <span data-ttu-id="d4a37-199">For example, kliknij przycisk [http://twimlets.com/message] [ twimlet_message_url] wyświetlić pustą `<Response>` element; inny przykład kliknij [http://twimlets.com/message?Message%5B0%5D=Hello%20World] [ twimlet_message_url_hello_world] wyświetlić `<Response>` element, który zawiera `<Say>` elementu.)</span><span class="sxs-lookup"><span data-stu-id="d4a37-199">For example, click [http://twimlets.com/message][twimlet_message_url] to see an empty `<Response>` element; as another example, click [http://twimlets.com/message?Message%5B0%5D=Hello%20World][twimlet_message_url_hello_world] to see a `<Response>` element that contains a `<Say>` element.)</span></span>

<span data-ttu-id="d4a37-200">Zamiast polegania na adres URL dostarczony do usługi Twilio, można utworzyć własne lokacji, która zwraca odpowiedzi HTTP.</span><span class="sxs-lookup"><span data-stu-id="d4a37-200">Instead of relying on the Twilio-provided URL, you can create your own site that returns HTTP responses.</span></span> <span data-ttu-id="d4a37-201">Można utworzyć witryny w dowolnym języku, który zwraca odpowiedzi XML; w tym temacie założono, że będziesz używać języka Python do utworzenia TwiML.</span><span class="sxs-lookup"><span data-stu-id="d4a37-201">You can create the site in any language that returns XML responses; this topic assumes you will be using Python to create the TwiML.</span></span>

<span data-ttu-id="d4a37-202">Poniższe przykłady dane wyjściowe obejmują odpowiedzi TwiML, informujący o **Hello World** przy wywołaniu.</span><span class="sxs-lookup"><span data-stu-id="d4a37-202">The following examples will output a TwiML response that says **Hello World** on the call.</span></span>

<span data-ttu-id="d4a37-203">Z Flask:</span><span class="sxs-lookup"><span data-stu-id="d4a37-203">With Flask:</span></span>

    from flask import Response
    @app.route("/")
    def hello():
        xml = '<Response><Say>Hello world.</Say></Response>'
        return Response(xml, mimetype='text/xml')

<span data-ttu-id="d4a37-204">Przy użyciu platformy Django:</span><span class="sxs-lookup"><span data-stu-id="d4a37-204">With Django:</span></span>

    from django.http import HttpResponse
    def hello(request):
        xml = '<Response><Say>Hello world.</Say></Response>'
        return HttpResponse(xml, content_type='text/xml')

<span data-ttu-id="d4a37-205">Jak widać w powyższym przykładzie, odpowiedź TwiML jest po prostu dokumentu XML.</span><span class="sxs-lookup"><span data-stu-id="d4a37-205">As you can see from the example above, the TwiML response is simply an XML document.</span></span> <span data-ttu-id="d4a37-206">Biblioteka usługi Twilio dla języka Python zawiera klasy, które generuje TwiML dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="d4a37-206">The Twilio library for Python contains classes that will generate TwiML for you.</span></span> <span data-ttu-id="d4a37-207">Poniższy przykład tworzy równoważne odpowiedzi, jak pokazano powyżej, ale używa `twiml` modułu w bibliotece usługi Twilio dla języka Python:</span><span class="sxs-lookup"><span data-stu-id="d4a37-207">The example below produces the equivalent response as shown above, but uses the `twiml` module in the Twilio library for Python:</span></span>

    from twilio import twiml

    response = twiml.Response()
    response.say("Hello world.")
    print(str(response))

<span data-ttu-id="d4a37-208">Aby uzyskać więcej informacji o TwiML, zobacz [https://www.twilio.com/docs/api/twiml][twiml_reference].</span><span class="sxs-lookup"><span data-stu-id="d4a37-208">For more information about TwiML, see [https://www.twilio.com/docs/api/twiml][twiml_reference].</span></span>

<span data-ttu-id="d4a37-209">Po utworzeniu aplikacji Python zdefiniowano udzielenie odpowiedzi TwiML, użyj adres URL aplikacji, adres URL przekazany `client.calls.create` metody.</span><span class="sxs-lookup"><span data-stu-id="d4a37-209">Once you have your Python application set up to provide TwiML responses, use the URL of the application as the URL passed into the `client.calls.create`  method.</span></span> <span data-ttu-id="d4a37-210">Na przykład, jeśli masz aplikację sieci Web o nazwie **MyTwiML** wdrożone do platformy Azure hostowanej usługi, możesz użyć adresu url jako elementu webhook, jak pokazano w poniższym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="d4a37-210">For example, if you have a Web application named **MyTwiML** deployed to an Azure hosted service, you can use its url as webhook as shown in the following example:</span></span>

    from twilio.rest import TwilioRestClient

    account_sid = "your_twilio_account_sid"
    auth_token = "your_twilio_authentication_token"
    from_number = "NNNNNNNNNNN"
    to_number = "NNNNNNNNNNN"
    url = "http://your-domain-label.centralus.cloudapp.azure.com/MyTwiML/"

    # Initialize the Twilio client.
    client = TwilioRestClient(account_sid, auth_token)

    # Make the call.
    call = client.calls.create(to=to_number,
                               from_=from_number,
                               url=url)
    print(call.sid)

## <span data-ttu-id="d4a37-211"><a id="AdditionalServices"></a>Porady: korzystania z usługi Twilio dodatkowych usług</span><span class="sxs-lookup"><span data-stu-id="d4a37-211"><a id="AdditionalServices"></a>How to: Use Additional Twilio Services</span></span>
<span data-ttu-id="d4a37-212">Oprócz przykładach pokazano poniżej usługi Twilio oferuje opartych na sieci web interfejsów API, które można wykorzystać dodatkowych funkcji usługi Twilio z aplikacji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="d4a37-212">In addition to the examples shown here, Twilio offers web-based APIs that you can use to leverage additional Twilio functionality from your Azure application.</span></span> <span data-ttu-id="d4a37-213">Aby uzyskać szczegółowe informacje, zobacz [dokumentacji interfejsu API usługi Twilio][twilio_api].</span><span class="sxs-lookup"><span data-stu-id="d4a37-213">For full details, see the [Twilio API documentation][twilio_api].</span></span>

## <span data-ttu-id="d4a37-214"><a id="NextSteps"></a>Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d4a37-214"><a id="NextSteps"></a>Next Steps</span></span>
<span data-ttu-id="d4a37-215">Teraz, kiedy znasz już podstawy usługi usługi Twilio, skorzystaj z poniższych linków, aby dowiedzieć się więcej:</span><span class="sxs-lookup"><span data-stu-id="d4a37-215">Now that you have learned the basics of the Twilio service, follow these links to learn more:</span></span>

* <span data-ttu-id="d4a37-216">[Wytyczne dotyczące zabezpieczeń usługi Twilio][twilio_security_guidelines]</span><span class="sxs-lookup"><span data-stu-id="d4a37-216">[Twilio Security Guidelines][twilio_security_guidelines]</span></span>
* <span data-ttu-id="d4a37-217">[Porada usługi Twilio prowadnice i przykładowy kod][twilio_howtos]</span><span class="sxs-lookup"><span data-stu-id="d4a37-217">[Twilio HowTo Guides and Example Code][twilio_howtos]</span></span>
* <span data-ttu-id="d4a37-218">[Samouczki usługi Twilio Szybki Start][twilio_quickstarts]</span><span class="sxs-lookup"><span data-stu-id="d4a37-218">[Twilio Quickstart Tutorials][twilio_quickstarts]</span></span>
* <span data-ttu-id="d4a37-219">[Usługi Twilio w witrynie GitHub][twilio_on_github]</span><span class="sxs-lookup"><span data-stu-id="d4a37-219">[Twilio on GitHub][twilio_on_github]</span></span>
* <span data-ttu-id="d4a37-220">[Zwróć się do pomocy technicznej usługi Twilio][twilio_support]</span><span class="sxs-lookup"><span data-stu-id="d4a37-220">[Talk to Twilio Support][twilio_support]</span></span>

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
