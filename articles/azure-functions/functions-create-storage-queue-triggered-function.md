---
title: "Funkcja w systemie Azure wyzwalane przez wiadomości w kolejce aaaCreate | Dokumentacja firmy Microsoft"
description: "Użyj usługi Azure Functions toocreate niekorzystającą funkcji, który jest wywoływany przez komunikaty przesłać tooan kolejki magazynu Azure."
services: azure-functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
ms.assetid: 361da2a4-15d1-4903-bdc4-cc4b27fc3ff4
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/31/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: e9501ed336b502eaeee3fa62ec4ae085c76de0ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-function-triggered-by-azure-queue-storage"></a>Tworzenie funkcji wyzwalanej przez usługę Azure Queue Storage

Dowiedz się, jak toocreate funkcji wyzwalane, gdy wiadomości są przesyłane tooan kolejki magazynu Azure.

![Przeglądanie wiadomości w dziennikach hello.](./media/functions-create-storage-queue-triggered-function/function-app-in-portal-editor.png)

## <a name="prerequisites"></a>Wymagania wstępne

- Pobierz i zainstaluj hello [Eksploratora usługi Microsoft Azure Storage](http://storageexplorer.com/).

- Subskrypcja platformy Azure. Jeśli nie masz subskrypcji, przed rozpoczęciem utwórz [bezpłatne konto](https://azure.microsoft.com/free/?WT.mc_id=A261C142F).

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

## <a name="create-an-azure-function-app"></a>Tworzenie aplikacji funkcji platformy Azure

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

![Pomyślnie utworzona aplikacja funkcji.](./media/functions-create-first-azure-function/function-app-create-success.png)

Następnie należy utworzyć funkcji w hello nowej funkcji aplikacji.

<a name="create-function"></a>

## <a name="create-a-queue-triggered-function"></a>Tworzenie funkcji wyzwalanej przez kolejkę

1. Rozwiń węzeł funkcji aplikacji, a następnie kliknij przycisk hello  **+**  obok przycisku zbyt**funkcji**. Jeśli hello pierwszej funkcji w funkcji aplikacji, wybierz **Niestandardowa funkcja**. Spowoduje to wyświetlenie hello pełny zestaw szablonów funkcji.

    ![Funkcje strony szybkiego startu w hello portalu Azure](./media/functions-create-storage-queue-triggered-function/add-first-function.png)

2. Wybierz hello **QueueTrigger** szablonu żądany język i użyj hello ustawień określonych w tabeli hello.

    ![Tworzenie funkcji wyzwalane kolejki magazynu hello.](./media/functions-create-storage-queue-triggered-function/functions-create-queue-storage-trigger-portal.png)
    
    | Ustawienie | Sugerowana wartość | Opis |
    |---|---|---|
    | **Nazwa kolejki**   | myqueue-items    | Nazwa hello kolejki tooconnect tooin Twojego konta magazynu. |
    | **Połączenie konta magazynu** | AzureWebJobStorage | Użyj połączenia konta magazynu hello już używana przez aplikację funkcji lub Utwórz nową.  |
    | **Nazwa funkcji** | Unikatowa w obrębie aplikacji funkcji | Nazwa funkcji wyzwalanej przez kolejkę. |

3. Kliknij przycisk **Utwórz** toocreate funkcji.

Następnie połączyć konto magazynu Azure tooyour i utworzyć hello **elementów Moja_kolejka** kolejki magazynu.

## <a name="create-hello-queue"></a>Utwórz kolejkę hello

1. W funkcji kliknij pozycję **Integracja**, rozwiń pozycję **Dokumentacja** i skopiuj wartości pól **Nazwa konta** oraz **Klucz konta**. Używasz konta magazynu te poświadczenia tooconnect toohello. Jeśli nawiązano już połączenie konta magazynu, Pomiń toostep 4.

    ![Uzyskaj konto magazynu hello poświadczeń dla połączenia.](./media/functions-create-storage-queue-triggered-function/functions-storage-account-connection.png)v

1. Uruchom hello [Eksploratora usługi Microsoft Azure Storage](http://storageexplorer.com/) narzędzia, kliknij przycisk hello połączenia powitania po lewej stronie, wybierz **użyć nazwy konta magazynu i klucza**i kliknij przycisk **dalej**.

    ![Uruchom narzędzie Eksploratora usługi Storage konta hello.](./media/functions-create-storage-queue-triggered-function/functions-storage-manager-connect-1.png)

1. Wprowadź hello **nazwa konta** i **klucz konta** z kroku 1, kliknij przycisk **dalej** , a następnie **Connect**.

    ![Wprowadź poświadczenia magazynu hello i połącz.](./media/functions-create-storage-queue-triggered-function/functions-storage-manager-connect-2.png)

1. Rozwiń hello dołączony konta magazynu, kliknij prawym przyciskiem myszy **kolejek**, kliknij przycisk **Tworzenie kolejki**, typ `myqueue-items`, a następnie naciśnij klawisz enter.

    ![Tworzenie kolejki magazynu.](./media/functions-create-storage-queue-triggered-function/functions-storage-manager-create-queue.png)

Teraz, gdy masz kolejki magazynu można przetestować funkcji hello przez dodanie toohello kolejki komunikatów.

## <a name="test-hello-function"></a>Funkcja hello testu

1. W portalu Azure hello, funkcja tooyour przeglądania rozwiń hello **dzienniki** u dołu strony hello i upewnij się, że hello przesyłania strumieniowego tego dziennika nie jest wstrzymana.

1. W programie Storage Explorer rozwiń swoje konto magazynu, wybierz kolejno pozycje **Queues** (Kolejki) i **myqueue-items**, a następnie kliknij pozycję **Add message** (Dodaj komunikat).

    ![Dodaj toohello kolejki komunikatów.](./media/functions-create-storage-queue-triggered-function/functions-storage-manager-add-message.png)

1. Wpisz komunikat „Hello World!” w polu **Message text** (Tekst komunikatu) i kliknij przycisk **OK**.

1. Zaczekaj kilka sekund, a następnie wróć tooyour dzienniki funkcji i sprawdź, czy tej nowej wiadomości powitania został odczytany z kolejki hello.

    ![Przeglądanie wiadomości w dziennikach hello.](./media/functions-create-storage-queue-triggered-function/functions-queue-storage-trigger-view-logs.png)

1. W Eksploratorze magazynu kliknij **Odśwież** i sprawdź, że wiadomość hello został przetworzony i nie jest już w kolejce hello.

## <a name="clean-up-resources"></a>Oczyszczanie zasobów

[!INCLUDE [Next steps note](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a>Następne kroki

Utworzono funkcję, która jest uruchamiana, gdy wiadomość zostanie dodany tooa magazynu kolejki.

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

Aby uzyskać więcej informacji na temat wyzwalaczy usługi Queue Storage, zobacz [Powiązania usługi Queue Storage w usłudze Azure Functions](functions-bindings-storage-queue.md).