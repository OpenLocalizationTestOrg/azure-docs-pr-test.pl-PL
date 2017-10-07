---
title: "aaaAdd opóźnienia w aplikacji logiki | Dokumentacja firmy Microsoft"
description: "Omówienie hello opóźnienia i opóźnienie — do akcji i w jaki sposób toouse z aplikacji logiki platformy Azure."
services: 
documentationcenter: 
author: jeffhollan
manager: erikre
editor: 
tags: connectors
ms.assetid: 915f48bf-3bd8-4656-be73-91a941d0afcd
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2016
ms.author: jehollan
ms.openlocfilehash: e5bc9d639adbddc01ee0f6a4c68716f586d4344a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-delay-and-delay-until-actions"></a>Rozpoczynanie pracy z hello opóźnienia i opóźnienie — do działania
Za pomocą hello opóźnienia i "opóźnienie — do momentu" akcje, ukończeniem scenariuszy przepływu pracy.

Można na przykład:

* Poczekaj, aż toosend dzień tygodnia, stan aktualizacji za pośrednictwem poczty e-mail.
* Przepływ pracy hello opóźnienie do wywołania HTTP ma toofinish czasu przed wznowieniem i pobierania wyniku hello.

tooget pracy z hello opóźnienie akcji w aplikacji logiki, zobacz [tworzenie aplikacji logiki](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="use-hello-delay-actions"></a>Używanie hello opóźnienie akcji
Akcja jest operacja odbywa się przez hello przepływ pracy, który jest zdefiniowany w aplikacji logiki. [Dowiedz się więcej o akcjach](connectors-overview.md).

Oto przykład sekwencji jak toouse opóźnienia kroku w aplikacji logiki:

1. Po dodaniu wyzwalacza, kliknij przycisk **nowy krok** tooadd akcji.
2. Wyszukaj **opóźnienie** toobring się hello opóźnienie akcji. W tym przykładzie firma Microsoft będzie wybierać **opóźnienie**.
   
    ![Opóźnienie akcji](./media/connectors-native-delay/using-action-1.png)
3. Ukończ wszelkie hello akcji właściwości tooconfigure hello opóźnienia.
   
    ![Opóźnienie konfiguracji](./media/connectors-native-delay/using-action-2.png)
4. Kliknij przycisk **zapisać** toopublish i aktywować aplikację logiki hello.

## <a name="action-details"></a>Szczegóły akcji
wyzwalacz cyklu Hello ma następujące właściwości, które można skonfigurować hello.

### <a name="delay-action"></a>Opóźnienie akcji
Ta akcja opóźnienia hello Uruchom określonym przedziale czasu.
A * oznacza, że jest polem wymaganym.

| Nazwa wyświetlana | Nazwa właściwości | Opis |
| --- | --- | --- |
| Liczba * |Liczba |Liczba Hello toodelay jednostki czasu |
| Jednostka * |jednostki |Jednostka czasu Hello: `Second`, `Minute`, `Hour`, lub`Day` |

<br>

### <a name="delay-until-action"></a>Opóźnienie — do akcji
Ta akcja opóźnia hello uruchomić do określonej daty/godziny.
A * oznacza, że jest polem wymaganym.

| Nazwa wyświetlana | Nazwa właściwości | Opis |
| --- | --- | --- |
| Rok * |sygnatura czasowa |Witaj toodelay roku do (GMT) |
| Miesiąc * |sygnatura czasowa |Witaj toodelay miesiąc aż do (GMT) |
| Dzień * |sygnatura czasowa |Witaj toodelay dzień do (GMT) |

<br>

## <a name="next-steps"></a>Następne kroki
Teraz, wypróbuj hello platformy i [tworzenie aplikacji logiki](../logic-apps/logic-apps-create-a-logic-app.md). Można eksplorować hello innych dostępnych łączników w aplikacjach logiki analizując naszych [listy interfejsów API](apis-list.md).

