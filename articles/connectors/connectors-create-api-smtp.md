---
title: "Łącznik aaaSMTP w programie Azure Logic Apps | Dokumentacja firmy Microsoft"
description: "Tworzenie aplikacji logiki z usługi aplikacji Azure. Połącz tooSMTP toosend w wiadomości e-mail."
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: d4141c08-88d7-4e59-a757-c06d0dc74300
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 07/15/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 36bb836851014d24f2e069fda8376ad7a08c943b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-smtp-connector"></a>Rozpoczynanie pracy z hello SMTP łącznika
Połącz tooSMTP toosend w wiadomości e-mail.

toouse [każdy łącznik](apis-list.md), należy najpierw toocreate aplikacji logiki. Możesz rozpocząć pracę przez [teraz tworzenie aplikacji logiki](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="connect-toosmtp"></a>Połącz tooSMTP
Zanim aplikację logiki można uzyskać dostęp do dowolnej usługi, należy najpierw toocreate *połączenia* toohello usługi. A [połączenia](connectors-overview.md) udostępnia łączność między aplikacji logiki i innej usługi. Na przykład tooconnect tooSMTP, należy najpierw SMTP *połączenia*. toocreate połączenie, wprowadź poświadczenia hello tooaccess hello usługi, gdy połączysz się zwykle jest używana. Tak w przykładzie hello SMTP, wprowadź nazwę połączenia tooyour poświadczenia hello, adresu serwera SMTP i użytkownika logowania informacji toocreate hello połączenia tooSMTP.  

### <a name="create-a-connection-toosmtp"></a>Tworzenie tooSMTP połączenia
> [!INCLUDE [Steps toocreate a connection tooSMTP](../../includes/connectors-create-api-smtp.md)]
> 
> 

## <a name="use-an-smtp-trigger"></a>Użyj wyzwalacz SMTP
Wyzwalacz jest zdarzenie, które mogą być zdefiniowane w aplikacji logiki hello toostart używane w przepływie pracy. [Dowiedz się więcej o wyzwalaczy](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).

W tym przykładzie, ponieważ SMTP nie ma wyzwalacz własnych, użyjemy hello **Salesforce — po utworzeniu obiektu** wyzwalacza. Wyzwalacz aktywuje po utworzeniu nowego obiektu w usłudze Salesforce. W naszym przykładzie skonfigurujemy Twoje go tak, aby zawsze nowego potencjalnego klienta jest tworzony w Salesforce, *wysyłania wiadomości e-mail* akcja jest wykonywana za pośrednictwem łącznika hello SMTP z powiadomienie z informacją o hello realizacji nowego tworzona.

1. Wprowadź *salesforce* w polu wyszukiwania hello hello logiki aplikacji designer wybierz hello **Salesforce — po utworzeniu obiektu** wyzwalacza.  
   ![](../../includes/media/connectors-create-api-salesforce/trigger-1.png)  
2. Witaj **podczas tworzenia obiektu** formant jest wyświetlany.
   ![](../../includes/media/connectors-create-api-salesforce/trigger-2.png)  
3. Wybierz hello **typ obiektu** następnie wybierz *prowadzić* z listy hello obiektów. W tym kroku wskazujesz, tworzysz wyzwalacz, który powiadomi aplikację logiki, zawsze, gdy nowy realizacji jest tworzony w usłudze Salesforce.  
   ![](../../includes/media/connectors-create-api-salesforce/trigger3.png)  
4. Witaj wyzwalacz został utworzony.  
   ![](../../includes/media/connectors-create-api-salesforce/trigger-4.png)  

## <a name="use-an-smtp-action"></a>Za pomocą akcji SMTP
Akcja jest wykonywane przez przepływ pracy hello zdefiniowanych w aplikacji logiki operacji. [Dowiedz się więcej o akcjach](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).

Teraz, gdy hello wyzwalacz został dodany, wykonaj te kroki akcję tooadd serwera SMTP, która zostanie przeprowadzona po utworzeniu nowego potencjalnego klienta w usłudze Salesforce.

1. Wybierz **+ nowy krok** akcji hello tooadd chcesz tootake po utworzeniu nowego potencjalnego klienta.  
   ![](../../includes/media/connectors-create-api-salesforce/trigger4.png)  
2. Wybierz **Dodaj akcję**. To pole wyszukiwania hello otwiera gdzie możesz wyszukać dowolną akcję należy chcieliby tootake.  
   ![](../../includes/media/connectors-create-api-smtp/using-smtp-action-2.png)  
3. Wprowadź *smtp* toosearch dla tooSMTP powiązanych działań.  
4. Wybierz **SMTP — Wyślij wiadomość E-mail** jako hello tootake akcji po utworzeniu nowego potencjalnego klienta hello. zostanie otwarty blok kontroli Hello akcji. Konieczne będzie tooestablish połączenia smtp w bloku projektanta hello Jeśli nie zostało zrobione to wcześniej.  
   ![](../../includes/media/connectors-create-api-smtp/smtp-2.png)    
5. Wprowadzania informacji żądaną poczty e-mail w programie hello **SMTP — Wyślij wiadomość E-mail** bloku.  
   ![](../../includes/media/connectors-create-api-smtp/using-smtp-action-4.PNG)  
6. Zapisz swoją pracę w kolejności tooactivate przepływ pracy.  

## <a name="connector-specific-details"></a>Szczegóły dotyczące łącznika

Wyświetl wszystkie wyzwalacze i akcje zdefiniowane w hello swagger i zobacz też żadnych limitów w hello [szczegóły łącznika](/connectors/smtpconnector/).

## <a name="more-connectors"></a>Więcej łączników
Przejdź wstecz toohello [listy interfejsów API](apis-list.md).
