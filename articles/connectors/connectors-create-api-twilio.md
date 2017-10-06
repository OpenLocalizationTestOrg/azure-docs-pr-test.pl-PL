---
title: "aaaAdd hello łącznika usługi Twilio w aplikacjach logiki platformy Azure | Dokumentacja firmy Microsoft"
description: "Omówienie hello łącznika usługi Twilio z parametrami interfejsu API REST"
services: logic-apps
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 43116187-4a2f-42e5-9852-a0d62f08c5fc
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 09/19/2016
ms.author: mandia; ladocs
ms.openlocfilehash: b2b487f34bc76bee24b4237a71ee767d0d22ff7d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-twilio-connector"></a>Rozpoczynanie pracy z łącznikiem usługi Twilio hello
Połącz tooTwilio toosend i odbierać globalne wiadomości SMS i MMS, adresu IP. Za pomocą usługi Twilio można:

* Tworzenie sieci przepływu biznesowe na podstawie danych hello, które można uzyskać z usługi Twilio. 
* Użyj akcje, które pobierają wiadomości, lista wiadomości i inne. Te akcje odpowiedzi, a następnie wprowadź dane wyjściowe hello dostępne dla innych działań. Na przykład gdy pojawi się nowy komunikat usługi Twilio, można ten komunikat i używać go w przepływie pracy usługi Service Bus. 

Rozpoczynanie pracy przez tworzenie aplikacji logiki; zobacz [tworzenie aplikacji logiki](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="create-a-connection-tootwilio"></a>Tworzenie tooTwilio połączenia
Po dodaniu aplikacji logiki tooyour tego łącznika, wprowadź następujące wartości usługi Twilio hello:

| Właściwość | Wymagane | Opis |
| --- | --- | --- |
| Identyfikator konta |Tak |Wprowadź identyfikator konta usługi Twilio |
| Token dostępu |Tak |Wprowadź token dostępu usługi Twilio |

> [!INCLUDE [Steps toocreate a connection tooTwilio](../../includes/connectors-create-api-twilio.md)]
> 
> 

Jeśli nie masz tokenu dostępu usługi Twilio, zobacz [tożsamości użytkowników i tokenów dostępu](https://www.twilio.com/docs/api/chat/guides/identity).

## <a name="connector-specific-details"></a>Szczegóły dotyczące łącznika

Wyświetl wszystkie wyzwalacze i akcje zdefiniowane w hello swagger i zobacz też żadnych limitów w hello [szczegóły łącznika](/connectors/twilio/).

## <a name="more-connectors"></a>Więcej łączników
Przejdź wstecz toohello [listy interfejsów API](apis-list.md).
