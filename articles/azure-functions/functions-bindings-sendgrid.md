---
title: "powiązania funkcji SendGrid aaaAzure | Dokumentacja firmy Microsoft"
description: "Azure odwołania wiązania włączenie funkcji"
services: functions
documentationcenter: na
author: rachelappel
manager: erikre
ms.service: functions
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 03/16/2017
ms.author: rachelap
ms.openlocfilehash: 10a3837875eb6ae18e6c789bcf64cc401cf5f26a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-sendgrid-bindings"></a>Powiązania włączenie funkcji platformy Azure

W tym artykule opisano sposób tooconfigure i pracować z SendGrid powiązania usługi Azure Functions. Sendgrid można użyć usługi Azure Functions toosend dostosowane e-mail programowo.

W tym artykule jest informacje dla deweloperów usługi Azure Functions. W przypadku nowych funkcji tooAzure należy rozpocząć hello następujące zasoby:

[Tworzenie pierwszej funkcji platformy Azure](functions-create-first-azure-function.md). 
[C#](functions-reference-csharp.md), [F #](functions-reference-fsharp.md), lub [węzła](functions-reference-node.md) odwołuje się do projektanta.

## <a name="functionjson-for-sendgrid-bindings"></a>Function.JSON dla powiązania SendGrid

Środowisko Azure Functions zapewnia SendGrid powiązania danych wyjściowych. Witaj SendGrid wyjściowe powiązanie umożliwia toocreate i wysyłania wiadomości e-mail programowo. 

Powiązanie SendGrid Hello obsługuje hello następujące właściwości:

- `name`: Wymagana — nazwa zmiennej hello używane w kodzie funkcji żądania hello lub treści żądania. Ta wartość jest ```$return``` po tylko jednej wartości zwracanej. 
- `type`: Wymagana — musi być ustawiona zbyt "sendGrid."
- `direction`: Wymagana — musi być ustawiona zbyt "out".
- `apiKey`: Wymagana — musi być nazwą toohello zestaw klucza interfejsu API przechowywane w ustawieniach aplikacji hello funkcji aplikacji.
- `to`: hello adres e-mail adresata.
- `from`: hello adres e-mail nadawcy.
- `subject`: hello podmiotu hello poczty e-mail.
- `text`: hello treść wiadomości e-mail.

Przykład **function.json**:

```json 
{
    "bindings": [
        {
            "name": "$return",
            "type": "sendGrid",
            "direction": "out",
            "apiKey" : "MySendGridKey",
            "to": "{ToEmail}",
            "from": "{FromEmail}",
            "subject": "SendGrid output bindings"
        }
    ]
}
```

> [!NOTE]
> Azure Functions przechowuje informacje dotyczące połączenia, a klucze interfejsu API zgodnie z ustawieniami aplikacji, dzięki czemu nie są sprawdzane w Twoim repozytorium kontroli źródła. Ta akcja chroni poufne informacje.
>
>

## <a name="c-example-of-hello-sendgrid-output-binding"></a>C# przykład hello SendGrid powiązania wyjściowego

```csharp
#r "SendGrid"
using System;
using SendGrid.Helpers.Mail;

public static Mail Run(TraceWriter log, string input, out Mail message)
{
     message = new Mail
    {        
        Subject = "Azure news"          
    };

    var personalization = new Personalization();
    personalization.AddTo(new Email("recipient@contoso.com"));   

    Content content = new Content
    {
        Type = "text/plain",
        Value = input
    };
    message.AddContent(content);
    message.AddPersonalization(personalization);
}
```

## <a name="node-example-of-hello-sendgrid-output-binding"></a>Przykład węzła hello SendGrid output powiązania

```javascript
module.exports = function (context, input) {    
    var message = {
         "personalizations": [ { "to": [ { "email": "sample@sample.com" } ] } ],
        from: "sender@contoso.com",        
        subject: "Azure news",
        content: [{
            type: 'text/plain',
            value: input
        }]
    };

    context.done(null, message);
};

```

## <a name="next-steps"></a>Następne kroki
Aby uzyskać informacje o innych powiązań i Wyzwalacze dla usługi Azure Functions zobacz 
- [Azure funkcje wyzwalaczy i powiązań dewelopera](functions-triggers-bindings.md)

- [Najlepsze rozwiązania dotyczące usługi Azure Functions](functions-best-practices.md) wymieniono niektóre najlepszych praktyk toouse podczas tworzenia usługi Azure Functions.

- [Dokumentacja dla deweloperów usługi Azure funkcji](functions-reference.md) programisty dokumentacja dotycząca kodowania funkcji oraz definiowania wyzwalaczy i powiązań.
