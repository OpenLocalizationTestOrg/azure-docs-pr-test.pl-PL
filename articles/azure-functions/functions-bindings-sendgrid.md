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
# <a name="azure-functions-sendgrid-bindings"></a><span data-ttu-id="284b9-103">Powiązania włączenie funkcji platformy Azure</span><span class="sxs-lookup"><span data-stu-id="284b9-103">Azure Functions SendGrid bindings</span></span>

<span data-ttu-id="284b9-104">W tym artykule opisano sposób tooconfigure i pracować z SendGrid powiązania usługi Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="284b9-104">This article explains how tooconfigure and work with SendGrid bindings in Azure Functions.</span></span> <span data-ttu-id="284b9-105">Sendgrid można użyć usługi Azure Functions toosend dostosowane e-mail programowo.</span><span class="sxs-lookup"><span data-stu-id="284b9-105">With SendGrid, you can use Azure Functions toosend customized email programmatically.</span></span>

<span data-ttu-id="284b9-106">W tym artykule jest informacje dla deweloperów usługi Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="284b9-106">This article is reference information for Azure Functions developers.</span></span> <span data-ttu-id="284b9-107">W przypadku nowych funkcji tooAzure należy rozpocząć hello następujące zasoby:</span><span class="sxs-lookup"><span data-stu-id="284b9-107">If you're new tooAzure Functions, start with hello following resources:</span></span>

<span data-ttu-id="284b9-108">[Tworzenie pierwszej funkcji platformy Azure](functions-create-first-azure-function.md).</span><span class="sxs-lookup"><span data-stu-id="284b9-108">[Create your first Azure Function](functions-create-first-azure-function.md).</span></span> 
<span data-ttu-id="284b9-109">[C#](functions-reference-csharp.md), [F #](functions-reference-fsharp.md), lub [węzła](functions-reference-node.md) odwołuje się do projektanta.</span><span class="sxs-lookup"><span data-stu-id="284b9-109">[C#](functions-reference-csharp.md), [F#](functions-reference-fsharp.md), or [Node](functions-reference-node.md) developer references.</span></span>

## <a name="functionjson-for-sendgrid-bindings"></a><span data-ttu-id="284b9-110">Function.JSON dla powiązania SendGrid</span><span class="sxs-lookup"><span data-stu-id="284b9-110">function.json for SendGrid bindings</span></span>

<span data-ttu-id="284b9-111">Środowisko Azure Functions zapewnia SendGrid powiązania danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="284b9-111">Azure Functions provides an output binding for SendGrid.</span></span> <span data-ttu-id="284b9-112">Witaj SendGrid wyjściowe powiązanie umożliwia toocreate i wysyłania wiadomości e-mail programowo.</span><span class="sxs-lookup"><span data-stu-id="284b9-112">hello SendGrid output binding enables you toocreate and send email programmatically.</span></span> 

<span data-ttu-id="284b9-113">Powiązanie SendGrid Hello obsługuje hello następujące właściwości:</span><span class="sxs-lookup"><span data-stu-id="284b9-113">hello SendGrid binding supports hello following properties:</span></span>

- <span data-ttu-id="284b9-114">`name`: Wymagana — nazwa zmiennej hello używane w kodzie funkcji żądania hello lub treści żądania.</span><span class="sxs-lookup"><span data-stu-id="284b9-114">`name` : Required - hello variable name used in function code for hello request or request body.</span></span> <span data-ttu-id="284b9-115">Ta wartość jest ```$return``` po tylko jednej wartości zwracanej.</span><span class="sxs-lookup"><span data-stu-id="284b9-115">This value is ```$return``` when there is only one return value.</span></span> 
- <span data-ttu-id="284b9-116">`type`: Wymagana — musi być ustawiona zbyt "sendGrid."</span><span class="sxs-lookup"><span data-stu-id="284b9-116">`type` : Required - must be set too"sendGrid."</span></span>
- <span data-ttu-id="284b9-117">`direction`: Wymagana — musi być ustawiona zbyt "out".</span><span class="sxs-lookup"><span data-stu-id="284b9-117">`direction` : Required - must be set too"out."</span></span>
- <span data-ttu-id="284b9-118">`apiKey`: Wymagana — musi być nazwą toohello zestaw klucza interfejsu API przechowywane w ustawieniach aplikacji hello funkcji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="284b9-118">`apiKey` : Required - must be set toohello name of your API key stored in hello Function App's app settings.</span></span>
- <span data-ttu-id="284b9-119">`to`: hello adres e-mail adresata.</span><span class="sxs-lookup"><span data-stu-id="284b9-119">`to` : hello recipient's email address.</span></span>
- <span data-ttu-id="284b9-120">`from`: hello adres e-mail nadawcy.</span><span class="sxs-lookup"><span data-stu-id="284b9-120">`from` : hello sender's email address.</span></span>
- <span data-ttu-id="284b9-121">`subject`: hello podmiotu hello poczty e-mail.</span><span class="sxs-lookup"><span data-stu-id="284b9-121">`subject` : hello subject of hello email.</span></span>
- <span data-ttu-id="284b9-122">`text`: hello treść wiadomości e-mail.</span><span class="sxs-lookup"><span data-stu-id="284b9-122">`text` : hello email content.</span></span>

<span data-ttu-id="284b9-123">Przykład **function.json**:</span><span class="sxs-lookup"><span data-stu-id="284b9-123">Example of **function.json**:</span></span>

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
> <span data-ttu-id="284b9-124">Azure Functions przechowuje informacje dotyczące połączenia, a klucze interfejsu API zgodnie z ustawieniami aplikacji, dzięki czemu nie są sprawdzane w Twoim repozytorium kontroli źródła.</span><span class="sxs-lookup"><span data-stu-id="284b9-124">Azure Functions stores your connection information and API keys as app settings so that they are not checked into your source control repository.</span></span> <span data-ttu-id="284b9-125">Ta akcja chroni poufne informacje.</span><span class="sxs-lookup"><span data-stu-id="284b9-125">This action safeguards your sensitive information.</span></span>
>
>

## <a name="c-example-of-hello-sendgrid-output-binding"></a><span data-ttu-id="284b9-126">C# przykład hello SendGrid powiązania wyjściowego</span><span class="sxs-lookup"><span data-stu-id="284b9-126">C# example of hello SendGrid output binding</span></span>

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

## <a name="node-example-of-hello-sendgrid-output-binding"></a><span data-ttu-id="284b9-127">Przykład węzła hello SendGrid output powiązania</span><span class="sxs-lookup"><span data-stu-id="284b9-127">Node example of hello SendGrid output binding</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="284b9-128">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="284b9-128">Next steps</span></span>
<span data-ttu-id="284b9-129">Aby uzyskać informacje o innych powiązań i Wyzwalacze dla usługi Azure Functions zobacz</span><span class="sxs-lookup"><span data-stu-id="284b9-129">For information about other bindings and triggers for Azure Functions, see</span></span> 
- [<span data-ttu-id="284b9-130">Azure funkcje wyzwalaczy i powiązań dewelopera</span><span class="sxs-lookup"><span data-stu-id="284b9-130">Azure Functions triggers and bindings developer reference</span></span>](functions-triggers-bindings.md)

- <span data-ttu-id="284b9-131">[Najlepsze rozwiązania dotyczące usługi Azure Functions](functions-best-practices.md) wymieniono niektóre najlepszych praktyk toouse podczas tworzenia usługi Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="284b9-131">[Best practices for Azure Functions](functions-best-practices.md) Lists some best practices toouse when creating Azure Functions.</span></span>

- <span data-ttu-id="284b9-132">[Dokumentacja dla deweloperów usługi Azure funkcji](functions-reference.md) programisty dokumentacja dotycząca kodowania funkcji oraz definiowania wyzwalaczy i powiązań.</span><span class="sxs-lookup"><span data-stu-id="284b9-132">[Azure Functions developer reference](functions-reference.md) Programmer reference for coding functions and defining triggers and bindings.</span></span>
