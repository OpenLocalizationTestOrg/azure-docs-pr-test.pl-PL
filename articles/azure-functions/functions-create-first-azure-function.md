---
title: aaaCreate pierwszej funkcji z hello portalu Azure | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak toocreate platformy Azure pierwsze działać przez wykonanie niekorzystającą hello portalu Azure."
services: functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
ms.assetid: 96cf87b9-8db6-41a8-863a-abb828e3d06d
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 08/07/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 84283d7d4bc6015061946af4589f9a70ae61f36b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-function-in-hello-azure-portal"></a>Tworzenie pierwszej funkcji w hello portalu Azure

Środowisko Azure Functions umożliwia wykonywanie kodu w środowisku bez serwera bez konieczności toofirst tworzenie maszyny Wirtualnej lub opublikować aplikację sieci web. W tym temacie Dowiedz się, jak toouse funkcjonuje toocreate funkcję "hello world" hello portalu Azure.

![Tworzenie aplikacji funkcji w hello portalu Azure](./media/functions-create-first-azure-function/function-app-in-portal-editor.png)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="log-in-tooazure"></a>Zaloguj się za tooAzure

Zaloguj się za toohello [portalu Azure](https://portal.azure.com/).

## <a name="create-a-function-app"></a>Tworzenie aplikacji funkcji

Funkcja aplikacji toohost hello wykonywanie funkcji są wymagane. Aplikacja funkcji umożliwia grupowanie funkcji jako jednostki logicznej, co ułatwia wdrażanie i udostępnianie zasobów oraz zarządzanie nimi. 

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

Następnie należy utworzyć funkcji w hello nowej funkcji aplikacji.

## <a name="create-function"></a>Tworzenie funkcji wyzwalanej przez protokół HTTP

1. Rozwiń węzeł nowej aplikacji funkcji, a następnie kliknij przycisk hello  **+**  obok przycisku zbyt**funkcji**.

2.  W hello **szybkie rozpoczęcie pracy** wybierz pozycję **element WebHook i interfejs API**, **wybierz język** Twojego funkcji, a następnie kliknij przycisk **tworzenia tej funkcji** . 
   
    ![Funkcji szybkiego startu w hello portalu Azure.](./media/functions-create-first-azure-function/function-app-quickstart-node-webhook.png)

Funkcja jest tworzony w wybrany język przy użyciu szablonu hello funkcji HTTP wyzwolone. Możesz uruchomić hello nową funkcję, wysyłając żądania HTTP.

## <a name="test-hello-function"></a>Funkcja hello testu

1. W nowej funkcji kliknij przycisk **</> Pobierz adres URL funkcji**, wybierz pozycję **domyślne (klawisz funkcji)**, a następnie kliknij przycisk **Kopiuj**. 

    ![Skopiuj adres URL funkcji hello z hello portalu Azure](./media/functions-create-first-azure-function/function-app-develop-tab-testing.png)

2. Wklej adres URL funkcji hello w pasku adresu przeglądarki. Dołącz ciągu zapytania hello `&name=<yourname>` toothis hello adresu URL i naciśnij klawisz `Enter` klucza na żądanie hello tooexecute klawiatury. Witaj poniżej znajduje się przykład hello odpowiedź zwrócona przez funkcję hello w przeglądarce Edge hello:

    ![Funkcja odpowiedzi w przeglądarce hello.](./media/functions-create-first-azure-function/function-app-browser-testing.png)

    adres URL zawiera klucz, który jest wymagany, domyślnie tooaccess żądania Hello funkcji za pośrednictwem protokołu HTTP.   

3. Po uruchomieniu funkcji informacje śledzenia są zapisywane toohello dzienniki. wyniki śledzenia hello toosee hello poprzednie wykonanie powróć tooyour funkcji w portalu hello i kliknij przycisk hello Strzałka u dołu hello tooexpand ekranie powitania w górę **dzienniki**. 

   ![Funkcje logowania podglądu hello portalu Azure.](./media/functions-create-first-azure-function/function-view-logs.png)

## <a name="clean-up-resources"></a>Oczyszczanie zasobów

[!INCLUDE [Clean up resources](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a>Następne kroki

Utworzono aplikację funkcji z prostą funkcją wyzwalaną przez protokół HTTP.  

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

Aby uzyskać więcej informacji, zobacz [Powiązania protokołu HTTP i elementów webhook w usłudze Azure Functions](functions-bindings-http-webhook.md).



