---
title: "aaaLearn jak toouse hello łącznik MQ w programie Azure Logic Apps | Dokumentacja firmy Microsoft"
description: "Podłącz tooan lokalnymi lub serwer Azure MQ z Twojej toobrowse przepływu pracy aplikacji logiki, odbierania i wysyłania wiadomości tooWebSphere MQ"
services: logic-apps
author: valthom
manager: anneta
documentationcenter: 
editor: 
tags: connectors
ms.assetid: 
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 06/01/2017
ms.author: valthom; ladocs
ms.openlocfilehash: 8b36d53b457ced1a7461c229aecfcf8e4ae668a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooan-ibm-mq-server-from-logic-apps-using-hello-mq-connector"></a>Łączenie z tooan IBM MQ serwera z aplikacji logiki przy użyciu łącznika MQ hello 

Microsoft Connector dla programu MQ wysyła i pobiera wiadomości przechowywanych w MQ serwera lokalnego lub na platformie Azure. Ten łącznik obejmuje klienta MQ firmy Microsoft, który komunikuje się ze zdalnym serwerem IBM MQ w sieci TCP/IP. Ten dokument jest łącznikiem starter przewodnik toouse hello MQ. Zaleca się rozpocząć przechodząc pojedynczej wiadomości w kolejce, a następnie próby hello inne akcje.    

Łącznik MQ Hello obejmuje hello następujące akcje. Nie ma żadnych wyzwalaczy.

-   Przeglądaj pojedynczą wiadomość bez usuwania wiadomości powitania od hello IBM MQ serwera
-   Przeglądaj komunikaty zbiorczo, bez usuwania wiadomości powitania od hello IBM MQ serwera
-   Pojedynczy komunikat o błędzie i Usuń wiadomości powitania od hello IBM MQ serwera
-   Odbieranie partię komunikatów i usuwanie wiadomości powitania od hello IBM MQ serwera
-   Wysyłanie wiadomości toohello IBM MQ serwera 

## <a name="prerequisites"></a>Wymagania wstępne

* Jeśli za pomocą lokalnego serwera MQ [instalowanie bramy danych lokalne powitania](../logic-apps/logic-apps-gateway-install.md) na serwerze w sieci. W przypadku powitania serwera MQ publicznie dostępne, lub dostępne w systemie Azure, brama danych hello jest nie używane lub wymagane.

    > [!NOTE]
    > Serwer Hello gdzie hello jest zainstalowana brama lokalna danych musi mieć również .net Framework 4.6 zainstalowane dla hello toofunction łącznika MQ.

* Utwórz hello zasobów platformy Azure dla bramy danych lokalne powitania - [Konfigurowanie połączenia bramy danych hello](../logic-apps/logic-apps-gateway-connection.md).

* Oficjalnie obsługiwane wersje programu IBM WebSphere MQ:
   * MQ W WERSJI 7.5
   * MQ 8.0

## <a name="create-a-logic-app"></a>Tworzenie aplikacji logiki

1. W hello **Azure start tablicy**, wybierz pozycję  **+**  (znak plus) **sieci Web i mobilność**, a następnie **aplikacji logiki**. 
2. Wprowadź hello **nazwa**, takich jak MQTestApp, **subskrypcji**, **grupy zasobów**, i **lokalizacji** (Użyj lokalizacji hello gdzie hello połączenie bramy danych lokalnych jest skonfigurowane). Wybierz **toodashboard numeru Pin**i wybierz **Utwórz**.  
![Tworzenie aplikacji logiki](media/connectors-create-api-mq/Create_Logic_App.png)

## <a name="add-a-trigger"></a>Dodaj wyzwalacz

> [!NOTE]
> Hello MQ łącznika nie ma żadnych wyzwalaczy. Tak, użyj innego toostart wyzwalacza aplikację logiki, takich jak hello **cyklu** wyzwalacza. 

1. Hello **projektanta aplikacji logiki** zostanie otwarta, wybierz opcję **cyklu** liście hello wspólnej wyzwalaczy.
2. Wybierz **Edytuj** w hello cyklu wyzwalacza. 
3. Zestaw hello **częstotliwość** zbyt**dzień**i zestaw hello **interwał** za**7**. 

## <a name="browse-a-single-message"></a>Przeglądaj w pojedynczym komunikacie
1. Wybierz **+ nowy krok**i wybierz **Dodaj akcję**.
2. W polu wyszukiwania hello wpisz `mq`, a następnie wybierz **MQ - przeglądania wiadomości**.  
![Przeglądaj wiadomości](media/connectors-create-api-mq/Browse_message.png)

3. Jeśli nie ma istniejącego połączenia MQ, należy utworzyć połączenie hello:  

    1. Wybierz **Połącz za pośrednictwem bramy danych lokalnych**, a następnie wprowadź właściwości powitania serwera MQ.  
    Aby uzyskać **serwera**, wprowadź nazwę serwera MQ hello, lub wprowadź adres IP hello następuje dwukropek i hello numer portu. 
    2. Witaj **bramy** lista rozwijana zawiera listę istniejących połączeń bramy, które zostały skonfigurowane. Wybierz bramę.
    3. Wybierz **Utwórz** po zakończeniu. Połączenie wygląda podobnie toohello następujące:   
    ![Właściwości połączenia](media/connectors-create-api-mq/Connection_Properties.png)

4. W oknie dialogowym właściwości akcji hello można:  

    * Użyj hello **kolejki** właściwości tooaccess nazwę kolejki innego niż zdefiniowana w hello połączenia
    * Użyj hello **MessageId**, **CorrelationId**, **GroupId**i inne właściwości toobrowse wiadomości oparte na różne właściwości MQ wiadomość hello
    * Ustaw **IncludeInfo** za**True** tooinclude komunikat dodatkowych informacji w danych wyjściowych hello. Lub ustaw ją za**False** toonot zawierają informacje dodatkowe wiadomość hello danych wyjściowych.
    * Wprowadź **limitu czasu** toodetermine wartość jak długo toowait dla tooarrive wiadomości w pustej kolejce. Jeśli nic nie zostanie wprowadzona, hello pierwszej wiadomości w kolejce hello są pobierane i nie ma żadnych czas oczekiwania na tooappear wiadomości.  
    ![Przeglądaj właściwości wiadomości](media/connectors-create-api-mq/Browse_message_Props.png)

5. **Zapisz** zmiany, a następnie **Uruchom** aplikację logiki:  
![Zapisz i uruchom](media/connectors-create-api-mq/Save_Run.png)

6. Po kilku sekundach przedstawiono kroki hello hello Uruchom, a można przyjrzeć się hello danych wyjściowych. Wybierz hello zielonym znacznikiem wyboru toosee szczegóły każdego kroku. Wybierz **Zobacz nieprzetworzone dane wyjściowe** toosee dodatkowe szczegóły dotyczące hello dane wyjściowe.  
![Przeglądaj dane wyjściowe komunikatu](media/connectors-create-api-mq/Browse_message_output.png)  

    Nieprzetworzone dane wyjściowe:  
    ![Przeglądaj nieprzetworzone dane wyjściowe komunikatu](media/connectors-create-api-mq/Browse_message_raw_output.png)

7. Gdy hello **IncludeInfo** wartość tootrue, zostanie wyświetlony hello następujące dane wyjściowe:  
![Przeglądaj wiadomości zawierają informacje o](media/connectors-create-api-mq/Browse_message_Include_Info.png)

## <a name="browse-multiple-messages"></a>Przeglądaj wiele komunikatów
Witaj **Przeglądaj wiadomości** akcja zawiera **BatchSize** tooindicate opcji powinny być zwracane ile komunikatów z kolejki hello.  Jeśli **BatchSize** nie ma wpisu, zwracane są wszystkie komunikaty. Witaj zwracany wyjściem jest tablica komunikatów.

1. Podczas dodawania hello **Przeglądaj wiadomości** akcji, hello pierwszego połączenia, który jest skonfigurowany jest domyślnie zaznaczona. Wybierz **zmienić połączenie** toocreate nowe połączenie, lub wybierz inne połączenie.

2. dane wyjściowe Hello przeglądania wiadomości pokazuje:  
![Przeglądaj wiadomości w danych wyjściowych](media/connectors-create-api-mq/Browse_messages_output.png)

## <a name="receive-a-single-message"></a>Pojedynczy komunikat o błędzie
Witaj **odbieranie wiadomości** akcji ma hello tego samego wejściami i wyjściami jako hello **przeglądania wiadomości** akcji. Korzystając z **odbieranie wiadomości**, wiadomość hello jest usuwane z kolejki hello.

## <a name="receive-multiple-messages"></a>Wiele komunikaty
Hello **komunikaty** akcji ma hello tego samego wejściami i wyjściami jako hello **Przeglądaj wiadomości** akcji. Korzystając z **komunikaty**, wiadomości powitania są usuwane z kolejki hello.

Jeśli w nie ma żadnych wiadomości powitania kolejki podczas przeglądania lub receive, krok hello kończy się niepowodzeniem z hello następujące dane wyjściowe:  
![Błąd wiadomości nie MQ](media/connectors-create-api-mq/MQ_No_Msg_Error.png)

## <a name="send-a-message"></a>Wysyłanie komunikatu
1. Podczas dodawania hello **wysyła komunikat** akcji, hello pierwszego połączenia, który jest skonfigurowany jest domyślnie zaznaczona. Wybierz **zmienić połączenie** toocreate nowe połączenie, lub wybierz inne połączenie. Nieprawidłowa Hello **typów komunikatów** są **Datagram**, **odpowiedzi**, lub **żądania**.  
![Wyślij Msg właściwości](media/connectors-create-api-mq/Send_Msg_Props.png)

2. Witaj dane wyjściowe wysyła komunikat wygląda hello:  
![Wyślij dane wyjściowe Msg](media/connectors-create-api-mq/Send_Msg_Output.png)

## <a name="connector-specific-details"></a>Szczegóły dotyczące łącznika

Wyświetl wszystkie wyzwalacze i akcje zdefiniowane w hello swagger i zobacz też żadnych limitów w hello [szczegóły łącznika](/connectors/mq/).

## <a name="next-steps"></a>Następne kroki
[Tworzenie aplikacji logiki](../logic-apps/logic-apps-create-a-logic-app.md). Eksploruj hello innych dostępnych łączników w aplikacjach logiki w naszym [listy interfejsów API](apis-list.md).
