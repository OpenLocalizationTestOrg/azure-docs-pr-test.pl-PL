---
title: "aaaSend tooAzure zdarzeń usługi Event Hubs za pomocą C | Dokumentacja firmy Microsoft"
description: "Wysyłanie zdarzeń tooAzure Event Hubs przy użyciu C"
services: event-hubs
documentationcenter: 
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: event-hubs
ms.workload: na
ms.tgt_pltfrm: c
ms.devlang: csharp
ms.topic: article
ms.date: 08/15/2017
ms.author: sethm
ms.openlocfilehash: bb53300c070debb4a3658a38df9d3966f08e81ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="send-events-tooazure-event-hubs-using-c"></a><span data-ttu-id="d65a7-103">Wysyłanie zdarzeń tooAzure Event Hubs przy użyciu C</span><span class="sxs-lookup"><span data-stu-id="d65a7-103">Send events tooAzure Event Hubs using C</span></span>

## <a name="introduction"></a><span data-ttu-id="d65a7-104">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="d65a7-104">Introduction</span></span>
<span data-ttu-id="d65a7-105">Event Hubs to wysoce skalowalny system przyjmowania może obsługiwać miliony zdarzeń na sekundę, włączanie tooprocess aplikacji i analizowanie olbrzymich ilości danych wytworzonych przez podłączone urządzenia i aplikacje hello.</span><span class="sxs-lookup"><span data-stu-id="d65a7-105">Event Hubs is a highly scalable ingestion system that can ingest millions of events per second, enabling an application tooprocess and analyze hello massive amounts of data produced by your connected devices and applications.</span></span> <span data-ttu-id="d65a7-106">Po zebraniu danych do Centrum zdarzeń, można przekształcić i przechowywanie danych przy użyciu dowolnego dostawcy analiz w czasie rzeczywistym lub magazynu klastra.</span><span class="sxs-lookup"><span data-stu-id="d65a7-106">Once collected into an event hub, you can transform and store data using any real-time analytics provider or storage cluster.</span></span>

<span data-ttu-id="d65a7-107">Aby uzyskać więcej informacji, zobacz hello [Przegląd usługi Event Hubs] [Przegląd usługi Event Hubs].</span><span class="sxs-lookup"><span data-stu-id="d65a7-107">For more information, please see hello [Event Hubs overview][Event Hubs overview].</span></span>

<span data-ttu-id="d65a7-108">W tym samouczku przedstawiono sposób toosend zdarzenia tooan Centrum zdarzeń za pomocą aplikacji konsoli w zdarzeniach C. tooreceive kliknij odpowiedni język odbierania hello w tabeli po lewej stronie powitania treści.</span><span class="sxs-lookup"><span data-stu-id="d65a7-108">In this tutorial, you will learn how toosend events tooan event hub using a console application in C. tooreceive events, click hello appropriate receiving language in hello left-hand table of contents.</span></span>

<span data-ttu-id="d65a7-109">toocomplete tego samouczka należy hello następujące:</span><span class="sxs-lookup"><span data-stu-id="d65a7-109">toocomplete this tutorial, you will need hello following:</span></span>

* <span data-ttu-id="d65a7-110">Środowisko deweloperskie C.</span><span class="sxs-lookup"><span data-stu-id="d65a7-110">A C development environment.</span></span> <span data-ttu-id="d65a7-111">W tym samouczku zakładamy, że stos gcc hello na maszynie Wirtualnej platformy Azure Linux z Ubuntu 14.04.</span><span class="sxs-lookup"><span data-stu-id="d65a7-111">For this tutorial, we will assume hello gcc stack on an Azure Linux VM with Ubuntu 14.04.</span></span>
* <span data-ttu-id="d65a7-112">[Microsoft Visual Studio](https://www.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="d65a7-112">[Microsoft Visual Studio](https://www.visualstudio.com/).</span></span>
* <span data-ttu-id="d65a7-113">Aktywne konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="d65a7-113">An active Azure account.</span></span> <span data-ttu-id="d65a7-114">Jeśli jej nie masz, możesz utworzyć bezpłatne konto próbne w zaledwie kilka minut.</span><span class="sxs-lookup"><span data-stu-id="d65a7-114">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="d65a7-115">Aby uzyskać szczegółowe informacje, zobacz artykuł [Bezpłatna wersja próbna platformy Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d65a7-115">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="send-messages-tooevent-hubs"></a><span data-ttu-id="d65a7-116">Wysyłanie komunikatów tooEvent koncentratory</span><span class="sxs-lookup"><span data-stu-id="d65a7-116">Send messages tooEvent Hubs</span></span>
<span data-ttu-id="d65a7-117">W tej sekcji możemy zapisać C aplikacji toosend zdarzenia tooyour zdarzenia koncentratora.</span><span class="sxs-lookup"><span data-stu-id="d65a7-117">In this section we write a C app toosend events tooyour event hub.</span></span> <span data-ttu-id="d65a7-118">Kod Hello korzysta z biblioteki AMQP protonów hello z hello [projektu Apache Qpid](http://qpid.apache.org/).</span><span class="sxs-lookup"><span data-stu-id="d65a7-118">hello code uses hello Proton AMQP library from hello [Apache Qpid project](http://qpid.apache.org/).</span></span> <span data-ttu-id="d65a7-119">Jak pokazano jest analogiczna toousing usługi Service Bus kolejek i tematów z protokołu AMQP z C [tutaj](https://code.msdn.microsoft.com/Using-Apache-Qpid-Proton-C-afd76504).</span><span class="sxs-lookup"><span data-stu-id="d65a7-119">This is analogous toousing Service Bus queues and topics with AMQP from C as shown [here](https://code.msdn.microsoft.com/Using-Apache-Qpid-Proton-C-afd76504).</span></span> <span data-ttu-id="d65a7-120">Aby uzyskać więcej informacji, zobacz [dokumentacji protonów Qpid](http://qpid.apache.org/proton/index.html).</span><span class="sxs-lookup"><span data-stu-id="d65a7-120">For more information, see [Qpid Proton documentation](http://qpid.apache.org/proton/index.html).</span></span>

1. <span data-ttu-id="d65a7-121">Z hello [strony Qpid AMQP Messenger](https://qpid.apache.org/proton/messenger.html), wykonaj hello instrukcje tooinstall protonów Qpid, w zależności od środowiska.</span><span class="sxs-lookup"><span data-stu-id="d65a7-121">From hello [Qpid AMQP Messenger page](https://qpid.apache.org/proton/messenger.html), follow hello instructions tooinstall Qpid Proton, depending on your environment.</span></span>
2. <span data-ttu-id="d65a7-122">toocompile hello protonów biblioteki, zainstaluj następujące pakiety hello:</span><span class="sxs-lookup"><span data-stu-id="d65a7-122">toocompile hello Proton library, install hello following packages:</span></span>
   
    ```shell
    sudo apt-get install build-essential cmake uuid-dev openssl libssl-dev
    ```
3. <span data-ttu-id="d65a7-123">Pobierz hello [biblioteki protonów Qpid](http://qpid.apache.org/proton/index.html)i wyodrębnij go, np.:</span><span class="sxs-lookup"><span data-stu-id="d65a7-123">Download hello [Qpid Proton library](http://qpid.apache.org/proton/index.html), and extract it, e.g.:</span></span>
   
    ```shell
    wget http://archive.apache.org/dist/qpid/proton/0.7/qpid-proton-0.7.tar.gz
    tar xvfz qpid-proton-0.7.tar.gz
    ```
4. <span data-ttu-id="d65a7-124">Utwórz katalog kompilacji, kompilacji i instalacji:</span><span class="sxs-lookup"><span data-stu-id="d65a7-124">Create a build directory, compile and install:</span></span>
   
    ```shell
    cd qpid-proton-0.7
    mkdir build
    cd build
    cmake -DCMAKE_INSTALL_PREFIX=/usr ..
    sudo make install
    ```
5. <span data-ttu-id="d65a7-125">W katalogu roboczego, Utwórz nowy plik o nazwie **sender.c** z hello następującego kodu.</span><span class="sxs-lookup"><span data-stu-id="d65a7-125">In your work directory, create a new file called **sender.c** with hello following code.</span></span> <span data-ttu-id="d65a7-126">Należy pamiętać, toosubstitute hello wartość nazwy Centrum zdarzeń i przestrzeni nazw.</span><span class="sxs-lookup"><span data-stu-id="d65a7-126">Remember toosubstitute hello value for your event hub name and namespace name.</span></span> <span data-ttu-id="d65a7-127">Należy również podstawić zakodowane w adresie URL wersję klucza hello hello **SendRule** utworzony wcześniej.</span><span class="sxs-lookup"><span data-stu-id="d65a7-127">You must also substitute a URL-encoded version of hello key for hello **SendRule** created earlier.</span></span> <span data-ttu-id="d65a7-128">Możesz kodowania adresu URL go [tutaj](http://www.w3schools.com/tags/ref_urlencode.asp).</span><span class="sxs-lookup"><span data-stu-id="d65a7-128">You can URL-encode it [here](http://www.w3schools.com/tags/ref_urlencode.asp).</span></span>
   
    ```c
    #include "proton/message.h"
    #include "proton/messenger.h"
   
    #include <getopt.h>
    #include <proton/util.h>
    #include <sys/time.h>
    #include <stddef.h>
    #include <stdio.h>
    #include <string.h>
    #include <unistd.h>
    #include <stdlib.h>
   
    #define check(messenger)                                                     
      {                                                                          
        if(pn_messenger_errno(messenger))                                        
        {                                                                        
          printf("check\n");                                                     
          die(__FILE__, __LINE__, pn_error_text(pn_messenger_error(messenger))); 
        }                                                                        
      }  
   
    pn_timestamp_t time_now(void)
    {
      struct timeval now;
      if (gettimeofday(&now, NULL)) pn_fatal("gettimeofday failed\n");
      return ((pn_timestamp_t)now.tv_sec) * 1000 + (now.tv_usec / 1000);
    }  
   
    void die(const char *file, int line, const char *message)
    {
      printf("Dead\n");
      fprintf(stderr, "%s:%i: %s\n", file, line, message);
      exit(1);
    }
   
    int sendMessage(pn_messenger_t * messenger) {
        char * address = (char *) "amqps://SendRule:{Send Rule key}@{namespace name}.servicebus.windows.net/{event hub name}";
        char * msgtext = (char *) "Hello from C!";
   
        pn_message_t * message;
        pn_data_t * body;
        message = pn_message();
   
        pn_message_set_address(message, address);
        pn_message_set_content_type(message, (char*) "application/octect-stream");
        pn_message_set_inferred(message, true);
   
        body = pn_message_body(message);
        pn_data_put_binary(body, pn_bytes(strlen(msgtext), msgtext));
   
        pn_messenger_put(messenger, message);
        check(messenger);
        pn_messenger_send(messenger, 1);
        check(messenger);
   
        pn_message_free(message);
    }
   
    int main(int argc, char** argv) {
        printf("Press Ctrl-C toostop hello sender process\n");
   
        pn_messenger_t *messenger = pn_messenger(NULL);
        pn_messenger_set_outgoing_window(messenger, 1);
        pn_messenger_start(messenger);
   
        while(true) {
            sendMessage(messenger);
            printf("Sent message\n");
            sleep(1);
        }
   
        // release messenger resources
        pn_messenger_stop(messenger);
        pn_messenger_free(messenger);
   
        return 0;
    }
    ```
6. <span data-ttu-id="d65a7-129">Skompiluj plik hello przy założeniu **gcc**:</span><span class="sxs-lookup"><span data-stu-id="d65a7-129">Compile hello file, assuming **gcc**:</span></span>
   
    ```
    gcc sender.c -o sender -lqpid-proton
    ```

    > [!NOTE]
    > <span data-ttu-id="d65a7-130">W ten kod używany wychodzących okna 1 wiadomości powitania tooforce się jak najszybciej.</span><span class="sxs-lookup"><span data-stu-id="d65a7-130">In this code, we use an outgoing window of 1 tooforce hello messages out as soon as possible.</span></span> <span data-ttu-id="d65a7-131">Ogólnie rzecz biorąc aplikacji, należy spróbować toobatch wiadomości tooincrease przepływności.</span><span class="sxs-lookup"><span data-stu-id="d65a7-131">In general, your application should try toobatch messages tooincrease throughput.</span></span> <span data-ttu-id="d65a7-132">Zobacz hello [Qpid AMQP Messenger strony](https://qpid.apache.org/proton/messenger.html) uzyskać informacji na temat sposobu toouse hello protonów Qpid biblioteki w tym i innych środowisk i z platformy, dla których wiązania są udostępniane (obecnie Perl, PHP, Python i Ruby).</span><span class="sxs-lookup"><span data-stu-id="d65a7-132">See hello [Qpid AMQP Messenger page](https://qpid.apache.org/proton/messenger.html) for information about how toouse hello Qpid Proton library in this and other environments, and from platforms for which bindings are provided (currently Perl, PHP, Python, and Ruby).</span></span>


## <a name="next-steps"></a><span data-ttu-id="d65a7-133">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d65a7-133">Next steps</span></span>
<span data-ttu-id="d65a7-134">Więcej informacji na temat usługi Event Hubs można poznać, przechodząc na stronę hello następującego łącza:</span><span class="sxs-lookup"><span data-stu-id="d65a7-134">You can learn more about Event Hubs by visiting hello following links:</span></span>

* [<span data-ttu-id="d65a7-135">Omówienie usługi Event Hubs</span><span class="sxs-lookup"><span data-stu-id="d65a7-135">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md
)
* [<span data-ttu-id="d65a7-136">Tworzenie centrum zdarzeń</span><span class="sxs-lookup"><span data-stu-id="d65a7-136">Create an event hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="d65a7-137">Event Hubs — często zadawane pytania</span><span class="sxs-lookup"><span data-stu-id="d65a7-137">Event Hubs FAQ</span></span>](event-hubs-faq.md)

<!-- Images. -->
[21]: ./media/event-hubs-c-ephcs-getstarted/run-csharp-ephcs1.png
[24]: ./media/event-hubs-c-ephcs-getstarted/receive-eph-c.png
