---
title: "Przykładowe akcji alertu aaaWebhook w OMS Log Analytics | Dokumentacja firmy Microsoft"
description: "Jedną z akcji hello można uruchomić w odpowiedzi tooa alert analizy dzienników jest * webhook *, dzięki czemu można tooinvoke procesu zewnętrznego przez pojedyncze żądanie HTTP. W tym artykule przedstawiono przykład tworzenia akcji elementu webhook w alercie analizy dzienników, przy użyciu zapas czasu."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 13c39f0f-fd3c-472d-8324-ddf7538be45e
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/27/2017
ms.author: bwren
ms.openlocfilehash: e60bdc4922347073d572c2e4719461b13e8e7d1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-alert-webhook-action-in-oms-log-analytics-toosend-message-tooslack"></a>Tworzy akcję alertu elementu webhook w tooSlack komunikat toosend OMS analizy dzienników
Jedną z akcji hello można uruchomić w odpowiedzi tooa [alert analizy dzienników](log-analytics-alerts.md) jest *webhook*, co pozwala tooinvoke procesu zewnętrznego przez pojedyncze żądanie HTTP.  Możesz przeczytać o szczegółach alertów i elementów webhook w [alertów w analizy dzienników](log-analytics-alerts.md)

W tym artykule omówimy przykładem tworzenia akcji elementu webhook w przypadku wystąpienia alertu analizy dzienników przy użyciu zapas czasu, która jest usługą obsługi wiadomości.

> [!NOTE]
> Toocomplete Slack konto musi mieć w tym przykładzie.  Można założyć bezpłatne konto w [slack.com](http://slack.com).
> 
> 

## <a name="step-1---enable-webhooks-in-slack"></a>Krok 1 — elementów webhook Włącz w zapas czasu
1. Zaloguj się tooSlack na [slack.com](http://slack.com).
2. Wybierz kanał hello **kanałów** sekcji w okienku po lewej stronie powitania.  Jest to kanał hello otrzyma tę wiadomość hello.  Można wybrać jedną z kanałów domyślne hello takich jak **ogólne** lub **losowe**.  W środowisku produkcyjnym, należy prawdopodobnie utworzyć kanał specjalne takie jak **criticalservicealerts**. <br>
   
   ![Kanałach Slack](media/log-analytics-alerts-webhooks/oms-webhooks01.png)
3. Kliknij przycisk **Dodawanie aplikacji lub niestandardowej integracji** tooopen hello katalogu aplikacji.
4. Typ *elementów webhook* do pola wyszukiwania hello, a następnie wybierz **przychodzące elementów Webhook**. <br>
   
   ![Kanałach Slack](media/log-analytics-alerts-webhooks/oms-webhooks02.png)
5. Kliknij przycisk **zainstalować** Nazwa zespołu tooyour dalej.
6. Kliknij przycisk **Dodaj konfigurację**.
7. Wybierz hello hello kanału zacząć toouse w tym przykładzie, a następnie kliknij przycisk **integracji dodać przychodzące elementów Webhook**.  
8. Kopiuj hello **adresu URL elementu Webhook**.  Będzie można wklejane to w konfiguracji alertu hello. <br>
   
    ![Kanałach Slack](media/log-analytics-alerts-webhooks/oms-webhooks05.png)

## <a name="step-2---create-alert-rule-in-log-analytics"></a>Krok 2 — Tworzenie reguły alertu w analizy dzienników
1. [Tworzenie reguły alertu](log-analytics-alerts.md) z hello następujące ustawienia.
   * Zapytanie:```    Type=Event EventLevelName=error ```
   * Sprawdź, czy ten alert co: 5 minut
   * Witaj liczba wyników to: większe niż 10
   * W tym oknie: 60 minut
   * Wybierz **tak** dla **Webhook** i **nr** dla hello innych działań.
2. Witaj Wklej adres URL zapas czasu na powitania **adresu URL elementu Webhook** pola.
3. Wybierz opcję hello zbyt**Uwzględnij niestandardowy ładunek JSON**.
4. Zapas oczekuje ładunku zapisany w formacie JSON z parametru o nazwie *tekstu*.  Jest to hello tekst, który będzie wyświetlany w wiadomości powitania, który tworzy.  Można użyć co najmniej jednego hello alert parametry, używając hello  *#*  symboli, takie jak hello poniższy przykład.
   
    ```
    {
    "text":"#alertrulename fired with #searchresultcount records which exceeds hello over threshold of #thresholdvalue ."
    }
    ```
   
    ![Przykładowy ładunek JSON](media/log-analytics-alerts-webhooks/oms-webhooks07.png)
5. Kliknij przycisk **zapisać** toosave hello alertu.
6. Poczekaj wystarczającą ilość czasu alertu toobe utworzone, a następnie sprawdź zapas czasu dla komunikatu, którego będzie podobne następujące toohello.
   
   ![przykład webhook w zapas czasu](media/log-analytics-alerts-webhooks/oms-webhooks08.png)

### <a name="advanced-webhook-payload-for-slack"></a>Zaawansowane ładunku elementu webhook dla zapas czasu
Często można dostosować komunikaty przychodzące z zapas czasu. Aby uzyskać więcej informacji, zobacz [przychodzące elementów Webhook](https://api.slack.com/incoming-webhooks) na powitania Slack witryny sieci Web. Poniżej przedstawiono bardziej złożonych toocreate ładunku sformatowany komunikat z formatowaniem.

    {
        "attachments": [
            {
                "title":"OMS Alerts Custom Payload",
                "fields": [
                    {
                        "title": "Alert Rule Name",
                        "value": "#alertrulename"},
                    {
                        "title": "Link tooSearchResults",
                        "value": "<#linktosearchresults|OMS Search Results>"},
                    {
                        "title": "Search Interval",
                        "value": "#searchinterval"},
                    {
                        "title": "Threshold Operator",
                        "value": "#thresholdoperator"},
                    {
                        "title": "Threshold Value",
                        "value": "#thresholdvalue"}
                ],
                "color": "#F35A00"
            }
        ]
    }


Spowoduje to generowanie wiadomości w Slack następujące toohello podobne.

![Przykładowy komunikat w zapas czasu](media/log-analytics-alerts-webhooks/oms-webhooks09.png)

## <a name="summary"></a>Podsumowanie
Przy użyciu tej reguły alertów w miejscu trzeba tooSlack komunikatu wysłanego za każdym razem, gdy są spełnione kryteria hello.  

Jest tylko jeden przykład działań można tworzyć w odpowiedzi tooan alertu.  Można utworzyć akcję elementu webhook, wywołującą innej usługi zewnętrzne toostart działania elementu runbook, element runbook w automatyzacji Azure lub toosend akcji poczty e-mail, tooyourself poczty lub innych odbiorców.   

## <a name="next-steps"></a>Następne kroki
* Dowiedz się więcej o innych [alertów akcje w analizy dzienników](log-analytics-alerts-actions.md) łącznie z czynności.


