---
title: "Kod aaaCustom dla usługi Azure Logic Apps w środowisku Azure Functions | Dokumentacja firmy Microsoft"
description: "Tworzenie i uruchamianie niestandardowych kodów dla usługi Azure Logic Apps w środowisku Azure Functions"
services: logic-apps,functions
documentationcenter: .net,nodejs,java
author: jeffhollan
manager: anneta
editor: 
ms.assetid: 9fab1050-cfbc-4a8b-b1b3-5531bee92856
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.custom: H1Hack27Feb2017
ms.date: 10/18/2016
ms.author: LADocs; jehollan
ms.openlocfilehash: 18b3821ed7e434feb568b9b96e9a5a2189dba3bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="add-and-run-custom-code-for-logic-apps-through-azure-functions"></a>Dodaj i uruchomienia niestandardowego kodu dla usługi logic apps za pomocą usługi Azure Functions

toorun niestandardowych fragmenty kodu języka C# lub node.js w aplikacji logiki, można utworzyć funkcji niestandardowych za pomocą usługi Azure Functions. 
[Środowisko Azure Functions](../azure-functions/functions-overview.md) oferuje wolny od serwera przetwarzania danych w Microsoft Azure i są użyteczne do wykonywania tych zadań:

* Zaawansowane, formatowanie lub obliczeniowych pól w aplikacji logiki
* Wykonywanie obliczeń w przepływie pracy.
* Rozszerzenia funkcji aplikacji logiki hello z funkcjami, które są obsługiwane w języku C# lub node.js

## <a name="create-custom-functions-for-your-logic-apps"></a>Tworzenie funkcji niestandardowych dla aplikacji logiki

Zaleca się utworzenie funkcji w portalu usługi Azure Functions hello z hello **ogólny element Webhook - węzła** lub **ogólny element Webhook - C#** szablonów. wynik Hello tworzy wypełniana automatycznie szablon, który akceptuje `application/json` z aplikacji logiki. Funkcje, które utworzono z tych szablonów są automatycznie wykrywane i są wyświetlane w hello projektanta aplikacji logiki w obszarze **usługi Azure Functions w moim regionie.**

W portalu Azure na powitania hello **integracji** okienku dla funkcji szablon powinien pokazują, że **tryb** ustawić także**Webhook** i **typu elementu Webhook** ustawiono zbyt**ogólnego JSON**. 

Funkcje elementu Webhook zaakceptować żądania i przekaż go do metody hello za pośrednictwem `data` zmiennej. Uzyskać dostęp do właściwości hello Twojej ładunku, używając zapisu kropkowego jak `data.function-name`. Na przykład prosty funkcji JavaScript, który konwertuje wartości daty i godziny do ciągu daty wygląda hello poniższy przykład:

```
function start(req, res){
    var data = req.body;
    res = {
        body: data.date.ToDateString();
    }
}
```

## <a name="call-azure-functions-from-logic-apps"></a>Wywołanie usługi Azure Functions w aplikacjach logic apps

kontenery hello toolist w Twojej subskrypcji i wybierz hello funkcji, które mają toocall w Projektancie aplikacji logiki, kliknij przycisk hello **akcje** menu, a następnie wybierz z **usługi Azure Functions w moim regionie**.

Po wybraniu funkcji hello są zadawane toospecify obiektu wprowadzony ładunek. Ten obiekt jest wiadomość hello hello logiki aplikacji wysyła toohello funkcji i musi być obiektem JSON. Na przykład, jeśli chcesz, aby toopass w hello **ostatniej modyfikacji** daty z wyzwalacza Salesforce ładunku funkcja hello może wyglądać w tym przykładzie:

![Data ostatniej modyfikacji][1]

## <a name="trigger-logic-apps-from-a-function"></a>Aplikacje logiki wyzwalacza w funkcji

Możesz wyzwolić aplikacji logiki z wewnątrz funkcji. Zobacz [logiki aplikacji jako punkty końcowe można wywołać](logic-apps-http-endpoint.md). Tworzenie aplikacji logiki, która zawiera wyzwalacz ręcznego, a następnie z wewnątrz funkcji, wygeneruj adres URL ręczne wyzwalacza toohello HTTP POST z ładunku hello, który ma być wysyłane toohello aplikacji logiki.

### <a name="create-a-function-from-logic-app-designer"></a>Tworzenie funkcji przy użyciu projektanta aplikacji logiki

Można również utworzyć funkcję webhook node.js przy użyciu projektanta hello. Najpierw wybierz **usługi Azure Functions w moim regionie** , a następnie wybierz kontener dla funkcji. Jeśli jeszcze nie masz kontenera, należy toocreate jedną z hello [portalu Azure Functions](https://functions.azure.com/signin). Następnie wybierz **Utwórz nowy**.  

toogenerate szablon na podstawie danych hello, które mają toocompute, określić obiekt kontekstu hello planowanie toopass funkcji. Ten obiekt musi być obiektem JSON. Na przykład jeśli przekazać zawartość pliku hello z akcji FTP, ładunku kontekstu hello wygląda w tym przykładzie:

![Kontekst ładunku][2]

> [!NOTE]
> Ponieważ ten obiekt nie był rzutowany jako ciąg, hello zawartość jest dodawana bezpośrednio toohello ładunek JSON. Jednak występuje błąd, jeśli obiekt hello nie jest tokenem JSON (to znaczy, że ciąg lub JSON/Tablica obiektów). toocast hello obiekt jako ciąg, Dodaj cudzysłowy, jak pokazano w pierwszym rysunku hello w tym artykule.
> 

Projektant Hello następnie generuje szablonu funkcji, możesz utworzyć wbudowany. Zmienne wstępnie są tworzone na podstawie kontekstu hello planowanie toopass do funkcji hello.

<!--Image references-->
[1]: ./media/logic-apps-azure-functions/callfunction.png
[2]: ./media/logic-apps-azure-functions/createfunction.png
