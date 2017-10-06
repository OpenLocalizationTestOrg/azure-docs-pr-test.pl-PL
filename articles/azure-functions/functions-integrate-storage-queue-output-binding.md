---
title: "Funkcja w systemie Azure wyzwalane przez wiadomości w kolejce aaaCreate | Dokumentacja firmy Microsoft"
description: "Użyj usługi Azure Functions toocreate niekorzystającą funkcji, który jest wywoływany przez komunikaty przesłać tooan kolejki magazynu Azure."
services: azure-functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
ms.assetid: 0b609bc0-c264-4092-8e3e-0784dcc23b5d
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 08/17/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 44db90fa80bf77e31bf53dddabd7136de5800b11
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="add-messages-tooan-azure-storage-queue-using-functions"></a>Kolejka usługi Azure Storage tooan wiadomości przy użyciu funkcji Dodaj

W środowisku Azure Functions powiązań wejściowych i wyjściowych Podaj dane deklaratywne tooconnect tooexternal usługi z funkcji. Dowiedz się jak tooupdate istniejącej funkcji przez dodawanie danych wyjściowych powiązania, który wysyła wiadomości tooAzure kolejki magazynu, w tym temacie.  

![Przeglądanie wiadomości w dziennikach hello.](./media/functions-integrate-storage-queue-output-binding/functions-integrate-storage-binding-in-portal.png)

## <a name="prerequisites"></a>Wymagania wstępne 

[!INCLUDE [Previous topics](../../includes/functions-quickstart-previous-topics.md)]

* Zainstaluj hello [Eksploratora usługi Microsoft Azure Storage](http://storageexplorer.com/).

## <a name="add-binding"></a>Dodawanie powiązania danych wyjściowych
 
1. Rozwiń aplikację funkcji i funkcję.

2. Wybierz **integracji** i **+ nowe dane wyjściowe**, a następnie wybierz **magazynu kolejek Azure** i wybierz polecenie **wybierz**.
    
    ![Dodaj funkcję tooa powiązania kolejki magazynu danych wyjściowych w hello portalu Azure.](./media/functions-integrate-storage-queue-output-binding/function-add-queue-storage-output-binding.png)

3. Użyj hello ustawień określonych w tabeli hello: 

    ![Dodaj funkcję tooa powiązania kolejki magazynu danych wyjściowych w hello portalu Azure.](./media/functions-integrate-storage-queue-output-binding/function-add-queue-storage-output-binding-2.png)

    | Ustawienie      |  Sugerowana wartość   | Opis                              |
    | ------------ |  ------- | -------------------------------------------------- |
    | **Nazwa kolejki**   | myqueue-items    | Nazwa Hello hello kolejki tooconnect tooin Twojego konta magazynu. |
    | **Połączenie konta magazynu** | AzureWebJobStorage | Użyj połączenia konta magazynu hello już używana przez aplikację funkcji lub Utwórz nową.  |
    | **Nazwa parametru komunikatu** | outputQueueItem | Nazwa Hello hello dane wyjściowe wiązania parametru. | 

4. Kliknij przycisk **zapisać** tooadd hello powiązania.
 
Teraz, gdy masz powiązania wyjściowego zdefiniowana, należy tooupdate hello kodu toouse hello powiązania tooadd tooa kolejka wiadomości.  

## <a name="update-hello-function-code"></a>Zaktualizuj kod funkcja hello

1. Wybierz funkcja toodisplay hello funkcja kodu w edytorze hello. 

2. C# funkcji, należy zaktualizować definicję funkcji następujący tooadd hello **outputQueueItem** parametr wiązania magazynu. Pomiń ten krok w przypadku funkcji JavaScript.

    ```cs   
    public static async Task<HttpResponseMessage> Run(HttpRequestMessage req, 
        ICollector<string> outputQueueItem, TraceWriter log)
    {
        ....
    }
    ```

3. Dodaj hello następującego kodu toohello funkcja tuż przed hello metoda zwraca. Użyj hello odpowiedni fragment kodu dla języka hello funkcji.

    ```javascript
    context.bindings.outputQueueItem = "Name passed toohello function: " + 
                (req.query.name || req.body.name);
    ```

    ```cs
    outputQueueItem.Add("Name passed toohello function: " + name);     
    ```

4. Wybierz **zapisać** toosave zmiany.

wartość Hello wyzwalacza HTTP toohello znajduje się w kolejce toohello dodany komunikat.
 
## <a name="test-hello-function"></a>Funkcja hello testu 

1. Po zapisaniu zmian w kodzie hello wybierz **Uruchom**. 

    ![Dodaj funkcję tooa powiązania kolejki magazynu danych wyjściowych w hello portalu Azure.](./media/functions-integrate-storage-queue-output-binding/functions-test-run-function.png)

2. Sprawdź toomake dzienniki hello się upewnić, że funkcja hello zakończyła się pomyślnie. Nową kolejkę o nazwie **outqueue** jest tworzony na koncie magazynu przez hello runtime funkcje powiązania wyjściowego hello najpierw jest używany.

Następnie możesz połączyć tooyour magazynu konta tooverify hello nowej kolejki i wiadomości powitania dodać tooit. 

## <a name="connect-toohello-queue"></a>Połącz toohello kolejki

Pomiń hello pierwsze trzy kroki, jeśli masz już zainstalowany Eksploratora usługi Storage i podłączone tooyour konta magazynu.    

1. W funkcji, wybierz **integracji** i hello nowe **magazynu kolejek Azure** powiązania wyjściowego, a następnie rozwiń węzeł **dokumentacji**. Skopiuj wartości **Nazwa konta** i **Klucz konta**. Używasz konta magazynu te poświadczenia tooconnect toohello.
 
    ![Uzyskaj konto magazynu hello poświadczeń dla połączenia.](./media/functions-integrate-storage-queue-output-binding/function-get-storage-account-credentials.png)

2. Uruchom hello [Eksploratora usługi Microsoft Azure Storage](http://storageexplorer.com/) narzędzie, wybierz hello połączenia powitania po lewej stronie, wybierz **użyć nazwy konta magazynu i klucza**i wybierz **dalej**.

    ![Uruchom narzędzie Eksploratora usługi Storage konta hello.](./media/functions-integrate-storage-queue-output-binding/functions-storage-manager-connect-1.png)
    
3. Wklej hello **nazwa konta** i **klucz konta** z kroku 1 w odpowiednich polach, a następnie wybierz **dalej**, i **Connect**. 
  
    ![Wklej hello poświadczeń magazynu i nawiąż połączenie.](./media/functions-integrate-storage-queue-output-binding/functions-storage-manager-connect-2.png)

4. Rozwiń hello dołączony konta magazynu, rozwiń **kolejek** i sprawdź, czy kolejka o nazwie **elementów Moja_kolejka** istnieje. Należy również sprawdzić już wiadomość hello kolejki.  
 
    ![Tworzenie kolejki magazynu.](./media/functions-integrate-storage-queue-output-binding/function-queue-storage-output-view-queue.png)
 

## <a name="clean-up-resources"></a>Oczyszczanie zasobów

[!INCLUDE [Next steps note](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a>Następne kroki

Dodano dane wyjściowe powiązania tooan istniejącej funkcji. 

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

Aby uzyskać więcej informacji na temat wiązania tooQueue magazynu, zobacz [powiązania kolejki usługi Azure Storage funkcji](functions-bindings-storage-queue.md). 



