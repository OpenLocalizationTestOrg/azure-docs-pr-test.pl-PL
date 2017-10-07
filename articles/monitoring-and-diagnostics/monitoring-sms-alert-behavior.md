---
title: zachowanie alertu aaaSMS w grupach akcji | Dokumentacja firmy Microsoft
description: "Format wiadomości SMS i odpowiada tooSMS toounsubscribe wiadomości, dokonać ponownej subskrypcji lub prosić o pomoc."
author: anirudhcavale
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: ancav
ms.openlocfilehash: 3cd09b1903e3472f6402f62b74409d97e7e7ea97
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="sms-alert-behavior-in-action-groups"></a>Zachowanie w grupach akcji alertów programu SMS
## <a name="overview"></a>Omówienie ##
Grupy akcji Włącz tooconfigure listy odbiorców. Następnie można użyć tych grup, podczas definiowania alerty dziennika aktywności; zapewnienie, że po wyzwoleniu alertu dziennika aktywności hello jest powiadamiany o grupy określonej akcji. Jeden z alertów obsługiwane mechanizmy hello jest SMS; alerty Hello obsługuje komunikację dwukierunkową. Użytkownik może odpowiadać tooan alertu:

- **Anulowanie subskrypcji alertów:** użytkownik może zrezygnować z wszystkich alertów programu SMS dla wszystkich grup akcji lub grupy pojedynczej akcji.  
- **Dokonać ponownej subskrypcji tooalerts:** użytkownika możesz dokonać ponownej subskrypcji tooall alerty programu SMS dla wszystkich grup akcji lub grupy pojedynczej akcji.  
- **Prosić o pomoc:** użytkownik może uzyskać więcej informacji na temat hello programu SMS. Będą one przekierowanego toothis artykułu

W tym artykule omówiono zachowanie hello hello SMS alertów i hello użytkownika hello akcji odpowiedzi może przyjmować na podstawie ustawień regionalnych hello hello użytkownika:

## <a name="usacanada-sms-behavior"></a>Zachowanie USA i Kanady SMS
### <a name="receiving-an-sms-alert"></a>Otrzymywanie alertów programu SMS
Odbiornik programu SMS, który jest skonfigurowany jako część grupy akcji, otrzymają wiadomość SMS, po zgłoszeniu alertu. Witaj SMS prowadzi hello następujących informacji:
* Nazwa_skrócona grupy akcji hello ten alert został wysłany do
- Tytuł hello alertu

### <a name="unsubscribing-from-sms-alerts-for-one-action-group"></a>Anulowanie subskrypcji alertów programu SMS dla jednej grupy akcji
Użytkownika można zrezygnować z programu SMS dla alertów dla grupy jedną akcję przez odpowiada kodu toohello 20873 hello słów kluczowych: "Wyłączanie &lt;nazwa_skrócona grupy akcji&gt;".

Przykład. Użytkownika toounsubscribe alertów dla grupy akcji z nazwa_skrócona hello "Azure" wyśle kodu toohello SMS 20873 informacją "Wyłącz Azure"

### <a name="unsubscribing-from-sms-alerts-for-all-action-groups"></a>Anulowanie subskrypcji alertów programu SMS dla wszystkich grup, akcja
Użytkownik może zrezygnować z wszystkie alerty programu SMS dla wszystkich grup działań przez odpowiada toohello kodu 20873 ze wszystkimi hello następujące słowa kluczowe:
* ZATRZYMAJ

Przykład. Użytkownika toounsubscribe wszystkich alertów programu SMS dla wszystkich grup akcji, są wysyłane kodu toohello SMS 20873 informacją stop (Zatrzymaj)"

>[!NOTE]
>Jeśli użytkownik anulował z alertów programu SMS, ale jest następnie dodawana tooa nowej grupy akcji; BĘDĄ one otrzymywać alerty programu SMS dla tej nowej grupy akcji, ale pozostaje anulować ze wszystkich grup poprzedniej akcji.
>
>

### <a name="resubscribing-toosms-alerts-for-one-action-group"></a>Resubscribing tooSMS alerty dla jednej grupy akcji
Użytkownika można dokonać ponownej subskrypcji tooSMS alertów dla grupy jedną akcję przez odpowiada kodu toohello 20873 hello słów kluczowych: "Włącz &lt;nazwa_skrócona grupy akcji&gt;".

Przykład. Użytkownika tooalerts tooresubscribe dla grupy akcji z nazwa_skrócona hello "Azure" wyśle kodu toohello SMS 20873 informacją "Włącz Azure"

### <a name="resubscribing-toosms-alerts-for-all-action-groups"></a>Resubscribing tooSMS alertów dla wszystkich grup, akcja
Użytkownik może dokonać ponownej subskrypcji tooall programu SMS dla alertów dla wszystkich grup akcji ze odpowiada toohello kodu 20873 ze wszystkimi hello następujące słowa kluczowe:

* POCZĄTEK

Przykład. Użytkownika toounsubscribe wszystkich alertów programu SMS dla wszystkich grup akcji, są wysyłane kodu toohello SMS 20873 informacją "START"

### <a name="requesting-help-via-sms"></a>Żądanie pomocy przy użyciu usługi SMS
Użytkownika można zadawać uzyskać więcej informacji o hello programu SMS, że otrzymał przez odpowiada kodu toohello 20873 za pomocą dowolnego z następujących słów kluczowych hello:
* POMOC

Toohello użytkownika z artykułem toothis łącza zostanie wysłana odpowiedź.

## <a name="next-steps"></a>Następne kroki
Pobierz [Przegląd alertów dotyczących działań w dzienniku](monitoring-overview-alerts.md) i Dowiedz się, jak tooget alerty  
Dowiedz się więcej o [limitów szybkości programu SMS](monitoring-alerts-rate-limiting.md)  
Dowiedz się więcej o [grupy akcji](monitoring-action-groups.md)
