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
# <a name="send-events-tooazure-event-hubs-using-c"></a>Wysyłanie zdarzeń tooAzure Event Hubs przy użyciu C

## <a name="introduction"></a>Wprowadzenie
Event Hubs to wysoce skalowalny system przyjmowania może obsługiwać miliony zdarzeń na sekundę, włączanie tooprocess aplikacji i analizowanie olbrzymich ilości danych wytworzonych przez podłączone urządzenia i aplikacje hello. Po zebraniu danych do Centrum zdarzeń, można przekształcić i przechowywanie danych przy użyciu dowolnego dostawcy analiz w czasie rzeczywistym lub magazynu klastra.

Aby uzyskać więcej informacji, zobacz hello [Przegląd usługi Event Hubs] [Przegląd usługi Event Hubs].

W tym samouczku przedstawiono sposób toosend zdarzenia tooan Centrum zdarzeń za pomocą aplikacji konsoli w zdarzeniach C. tooreceive kliknij odpowiedni język odbierania hello w tabeli po lewej stronie powitania treści.

toocomplete tego samouczka należy hello następujące:

* Środowisko deweloperskie C. W tym samouczku zakładamy, że stos gcc hello na maszynie Wirtualnej platformy Azure Linux z Ubuntu 14.04.
* [Microsoft Visual Studio](https://www.visualstudio.com/).
* Aktywne konto platformy Azure. Jeśli jej nie masz, możesz utworzyć bezpłatne konto próbne w zaledwie kilka minut. Aby uzyskać szczegółowe informacje, zobacz artykuł [Bezpłatna wersja próbna platformy Azure](https://azure.microsoft.com/pricing/free-trial/).

## <a name="send-messages-tooevent-hubs"></a>Wysyłanie komunikatów tooEvent koncentratory
W tej sekcji możemy zapisać C aplikacji toosend zdarzenia tooyour zdarzenia koncentratora. Kod Hello korzysta z biblioteki AMQP protonów hello z hello [projektu Apache Qpid](http://qpid.apache.org/). Jak pokazano jest analogiczna toousing usługi Service Bus kolejek i tematów z protokołu AMQP z C [tutaj](https://code.msdn.microsoft.com/Using-Apache-Qpid-Proton-C-afd76504). Aby uzyskać więcej informacji, zobacz [dokumentacji protonów Qpid](http://qpid.apache.org/proton/index.html).

1. Z hello [strony Qpid AMQP Messenger](https://qpid.apache.org/proton/messenger.html), wykonaj hello instrukcje tooinstall protonów Qpid, w zależności od środowiska.
2. toocompile hello protonów biblioteki, zainstaluj następujące pakiety hello:
   
    ```shell
    sudo apt-get install build-essential cmake uuid-dev openssl libssl-dev
    ```
3. Pobierz hello [biblioteki protonów Qpid](http://qpid.apache.org/proton/index.html)i wyodrębnij go, np.:
   
    ```shell
    wget http://archive.apache.org/dist/qpid/proton/0.7/qpid-proton-0.7.tar.gz
    tar xvfz qpid-proton-0.7.tar.gz
    ```
4. Utwórz katalog kompilacji, kompilacji i instalacji:
   
    ```shell
    cd qpid-proton-0.7
    mkdir build
    cd build
    cmake -DCMAKE_INSTALL_PREFIX=/usr ..
    sudo make install
    ```
5. W katalogu roboczego, Utwórz nowy plik o nazwie **sender.c** z hello następującego kodu. Należy pamiętać, toosubstitute hello wartość nazwy Centrum zdarzeń i przestrzeni nazw. Należy również podstawić zakodowane w adresie URL wersję klucza hello hello **SendRule** utworzony wcześniej. Możesz kodowania adresu URL go [tutaj](http://www.w3schools.com/tags/ref_urlencode.asp).
   
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
6. Skompiluj plik hello przy założeniu **gcc**:
   
    ```
    gcc sender.c -o sender -lqpid-proton
    ```

    > [!NOTE]
    > W ten kod używany wychodzących okna 1 wiadomości powitania tooforce się jak najszybciej. Ogólnie rzecz biorąc aplikacji, należy spróbować toobatch wiadomości tooincrease przepływności. Zobacz hello [Qpid AMQP Messenger strony](https://qpid.apache.org/proton/messenger.html) uzyskać informacji na temat sposobu toouse hello protonów Qpid biblioteki w tym i innych środowisk i z platformy, dla których wiązania są udostępniane (obecnie Perl, PHP, Python i Ruby).


## <a name="next-steps"></a>Następne kroki
Więcej informacji na temat usługi Event Hubs można poznać, przechodząc na stronę hello następującego łącza:

* [Omówienie usługi Event Hubs](event-hubs-what-is-event-hubs.md
)
* [Tworzenie centrum zdarzeń](event-hubs-create.md)
* [Event Hubs — często zadawane pytania](event-hubs-faq.md)

<!-- Images. -->
[21]: ./media/event-hubs-c-ephcs-getstarted/run-csharp-ephcs1.png
[24]: ./media/event-hubs-c-ephcs-getstarted/receive-eph-c.png
