---
title: "Funkcja w systemie Azure wyzwalane przez ogólny element webhook aaaCreate | Dokumentacja firmy Microsoft"
description: "Za pomocą usługi Azure Functions toocreate niekorzystającą funkcji, który jest wywoływany przez element webhook na platformie Azure."
services: functions
documentationcenter: na
author: ggailey777
manager: cfowler
editor: 
tags: 
ms.assetid: fafc10c0-84da-4404-b4fa-eea03c7bf2b1
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 08/12/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 0a4868da91d216c8d20930ce7ec82eaa059c75ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-function-triggered-by-a-generic-webhook"></a>Utwórz funkcję wyzwalane przez ogólny element webhook

Środowisko Azure Functions umożliwia wykonywanie kodu w środowisku bez serwera bez konieczności toofirst tworzenie maszyny Wirtualnej lub opublikować aplikację sieci web. Na przykład można skonfigurować toobe funkcji wyzwalanych alertu zgłoszonego przez Azure Monitor. W tym temacie pokazano, jak tooexecute C# kodu, gdy grupa zasobów jest dodany tooyour subskrypcji.   

![Ogólny element webhook wyzwalane w portalu Azure hello — funkcja](./media/functions-create-generic-webhook-triggered-function/function-completed.png)

## <a name="prerequisites"></a>Wymagania wstępne 

toocomplete tego samouczka:

+ Jeśli nie masz subskrypcji platformy Azure, przed rozpoczęciem utwórz [bezpłatne konto](https://azure.microsoft.com/free/?WT.mc_id=A261C142F).

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

## <a name="create-an-azure-function-app"></a>Tworzenie aplikacji funkcji platformy Azure

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

Następnie należy utworzyć funkcji w hello nowej funkcji aplikacji.

## <a name="create-function"></a>Utwórz funkcję ogólny element webhook wyzwalane

1. Rozwiń węzeł funkcji aplikacji, a następnie kliknij przycisk hello  **+**  obok przycisku zbyt**funkcji**. Jeśli ta funkcja jest hello pierwsza z nich w aplikacji funkcji, wybierz **Niestandardowa funkcja**. Spowoduje to wyświetlenie hello pełny zestaw szablonów funkcji.

    ![Funkcje strony szybkiego startu w hello portalu Azure](./media/functions-create-generic-webhook-triggered-function/add-first-function.png)

2. Wybierz hello **ogólny element WebHook - C#** szablonu. Wpisz nazwę dla funkcji języka C#, a następnie wybierz **Utwórz**.

     ![Utwórz funkcję ogólny element webhook wyzwalane w hello portalu Azure](./media/functions-create-generic-webhook-triggered-function/functions-create-generic-webhook-trigger.png) 

2. W nowych funkcji, kliknij przycisk **adres URL funkcji <> / Get**, następnie skopiuj i Zapisz wartość hello. Możesz użyć tej wartości tooconfigure hello elementu webhook. 

    ![Przegląd kodu funkcji hello](./media/functions-create-generic-webhook-triggered-function/functions-copy-function-url.png)
         
Następnie należy utworzyć punkt końcowy elementu webhook w alertu dziennika aktywności w monitorze Azure. 

## <a name="create-an-activity-log-alert"></a>Utwórz alert dziennika aktywności

1. W portalu Azure hello kolejno toohello **Monitor** usługi, wybierz opcję **alerty**i kliknij przycisk **alert dziennika aktywności Dodaj**.   

    ![Monitorowanie](./media/functions-create-generic-webhook-triggered-function/functions-monitor-add-alert.png)

2. Użyj hello ustawień określonych w tabeli hello:

    ![Utwórz alert dziennika aktywności](./media/functions-create-generic-webhook-triggered-function/functions-monitor-add-alert-settings.png)

    | Ustawienie      |  Sugerowana wartość   | Opis                              |
    | ------------ |  ------- | -------------------------------------------------- |
    | **Nazwa alertu dziennika aktywności** | zasobów grupy Tworzenie alertu | Nazwa alertu dziennika aktywności hello. |
    | **Subskrypcja** | Twoja subskrypcja | Subskrypcja Hello są używane w tym samouczku. | 
    |  **Grupa zasobów** | myResourceGroup | Grupa zasobów Hello są wdrażane zasoby alertu hello. Jak funkcja aplikacji ułatwia łatwiejsze tooclean po ukończeniu samouczka hello przy użyciu hello tej samej grupie zasobów. |
    | **Kategoria zdarzenia** | Administracyjne | Ta kategoria zawiera zmiany tooAzure zasobów.  |
    | **Typ zasobu** | Grupy zasobów | Filtry działań grupowych tooresource alertów. |
    | **Grupa zasobów**<br/>i **zasobów** | Wszystkie | Monitoruj wszystkie zasoby. |
    | **Nazwa operacji** | Tworzenie grupy zasobów | Filtry działań toocreate alertów. |
    | **Poziom** | Informacyjny | Obejmują alerty informacyjne poziomu. | 
    | **Stan** | Powodzenie | Filtry tooactions alerty, które zostały ukończone pomyślnie. |
    | **Grupy akcji** | Nowy | Utwórz nową grupę działań, definiującą hello przyjmuje akcji, gdy zostanie zgłoszony alert. |
    | **Nazwa grupy akcji** | Element webhook — funkcja | Grupa działań hello tooidentify nazwy.  | 
    | **Krótka nazwa** | funcwebhook | Krótka nazwa grupy akcji hello. |  

3. W **akcje**, Dodaj akcję przy użyciu ustawień hello określoną w tabeli hello: 

    ![Dodaj grupę](./media/functions-create-generic-webhook-triggered-function/functions-monitor-add-alert-settings-2.png)

    | Ustawienie      |  Sugerowana wartość   | Opis                              |
    | ------------ |  ------- | -------------------------------------------------- |
    | **Nazwa** | CallFunctionWebhook | Nazwa akcji hello. |
    | **Typ akcji** | Webhook | alert toohello odpowiedzi Hello jest nosi adresu URL elementu Webhook. |
    | **Szczegóły** | Adres URL funkcji | Wklej adres URL elementu webhook hello hello funkcji, które wcześniej zostały skopiowane. |v

4. Kliknij przycisk **OK** hello toocreate grupy alert i akcji.  

Element webhook Hello nosi teraz, po utworzeniu grupy zasobów w ramach subskrypcji. Następnie zaktualizuj kod hello w sieci funkcja toohandle hello dane dziennika JSON w treści żądania hello hello.   

## <a name="update-hello-function-code"></a>Zaktualizuj kod funkcja hello

1. Przejdź wstecz tooyour funkcji aplikacji w portalu hello, a następnie rozwiń funkcji. 

2. Zastąp kod skryptu hello C# w funkcji hello w portalu hello hello następującego kodu:

    ```csharp
    #r "Newtonsoft.Json"
    
    using System;
    using System.Net;
    using Newtonsoft.Json;
    using Newtonsoft.Json.Linq;
    
    public static async Task<object> Run(HttpRequestMessage req, TraceWriter log)
    {
        log.Info($"Webhook was triggered!");
    
        // Get hello activityLog object from hello JSON in hello message body.
        string jsonContent = await req.Content.ReadAsStringAsync();
        JToken activityLog = JObject.Parse(jsonContent.ToString())
            .SelectToken("data.context.activityLog");
    
        // Return an error if hello resource in hello activity log isn't a resource group. 
        if (activityLog == null || !string.Equals((string)activityLog["resourceType"], 
            "Microsoft.Resources/subscriptions/resourcegroups"))
        {
            log.Error("An error occured");
            return req.CreateResponse(HttpStatusCode.BadRequest, new
            {
                error = "Unexpected message payload or wrong alert received."
            });
        }
    
        // Write information about hello created resource group toohello streaming log.
        log.Info(string.Format("Resource group '{0}' was {1} on {2}.",
            (string)activityLog["resourceGroupName"],
            ((string)activityLog["subStatus"]).ToLower(), 
            (DateTime)activityLog["submissionTimestamp"]));
    
        return req.CreateResponse(HttpStatusCode.OK);    
    }
    ```

Teraz można przetestować funkcji hello przez utworzenie nowej grupy zasobów w ramach subskrypcji.

## <a name="test-hello-function"></a>Funkcja hello testu

1. Kliknij ikonę grupy zasobów hello w lewej hello hello portalu Azure, wybierz opcję **+ Dodaj**, wpisz **Nazwa grupy zasobów**i wybierz **Utwórz** toocreate pustej grupy zasobów.
    
    ![Utwórz grupę zasobów.](./media/functions-create-generic-webhook-triggered-function/functions-create-resource-group.png)

2. Funkcja tooyour wrócić do poprzedniej strony i rozwiń hello **dzienniki** okna. Po utworzeniu grupy zasobów hello hello wyzwalaczy alertu dziennika aktywności hello elementu webhook i wykonuje hello funkcji. Zostanie wyświetlony hello nazwę hello zapisane dzienniki toohello nową grupę zasobów.  

    ![Dodaj ustawienie aplikacji testu.](./media/functions-create-generic-webhook-triggered-function/function-view-logs.png)

3. (Opcjonalnie) Przejdź wstecz i Usuń grupę zasobów hello, który został utworzony. Należy pamiętać, że to działanie nie powoduje wyzwolenia hello funkcji. Jest to spowodowane Usuń operacje są odfiltrowywane przez hello alertu. 

## <a name="clean-up-resources"></a>Oczyszczanie zasobów

[!INCLUDE [Next steps note](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a>Następne kroki

Funkcja, która jest uruchamiana, gdy żądanie zostanie odebrane z ogólny element webhook został utworzony. 

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

Aby uzyskać więcej informacji na temat wyzwalaczy elementów webhook, zobacz temat [Powiązania protokołu HTTP i elementów webhook w usłudze Azure Functions](functions-bindings-http-webhook.md). Zobacz toolearn więcej informacji na temat tworzenia funkcji w języku C# [dokumentacja dla deweloperów usług Azure funkcje C# skrypt](functions-reference-csharp.md).

