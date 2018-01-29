---
title: "Tworzenie funkcji na platformie Azure wyzwalanej przez magazyn obiektów Blob | Microsoft Docs"
description: "Utwórz za pomocą usługi Azure Functions funkcję niewymagającą użycia serwera wywoływaną za pomocą elementów dodanych do magazynu obiektów Blob platformy Azure."
services: azure-functions
documentationcenter: na
author: ggailey777
manager: cfowler
editor: 
tags: 
ms.assetid: d6bff41c-a624-40c1-bbc7-80590df29ded
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 12/07/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: e34d3634b592efe4581135f9dee52bf77d7506cd
ms.sourcegitcommit: fa28ca091317eba4e55cef17766e72475bdd4c96
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/14/2017
---
# <a name="create-a-function-triggered-by-azure-blob-storage"></a>Tworzenie funkcji wyzwalanej przez magazyn obiektów Blob

Dowiedz się, jak utworzyć funkcję wyzwalaną w momencie przekazania plików do magazynu obiektów Blob platformy Azure lub zaktualizowania w magazynie.

![Wyświetlanie komunikatu w dziennikach.](./media/functions-create-storage-blob-triggered-function/function-app-in-portal-editor.png)

## <a name="prerequisites"></a>Wymagania wstępne

+ Pobrać i zainstalować program [Microsoft Azure Storage Explorer](http://storageexplorer.com/).
+ Subskrypcja platformy Azure. Jeśli nie masz subskrypcji, przed rozpoczęciem utwórz [bezpłatne konto](https://azure.microsoft.com/free/?WT.mc_id=A261C142F).

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

## <a name="create-an-azure-function-app"></a>Tworzenie aplikacji funkcji platformy Azure

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

![Pomyślnie utworzona aplikacja funkcji.](./media/functions-create-first-azure-function/function-app-create-success.png)

Następnie należy utworzyć funkcję w nowej aplikacji funkcji.

<a name="create-function"></a>

## <a name="create-a-blob-storage-triggered-function"></a>Tworzenie funkcji wyzwalanej przez magazyn obiektów Blob

1. Rozwiń aplikację funkcji i kliknij przycisk **+** obok pozycji **Funkcje**. Jeśli jest to pierwsza funkcja w aplikacji funkcji, wybierz pozycję **Funkcja niestandardowa**. Spowoduje to wyświetlenie pełnego zestawu szablonów funkcji.

    ![Strona szybkiego rozpoczynania pracy z usługą Functions w witrynie Azure Portal](./media/functions-create-storage-blob-triggered-function/add-first-function.png)

2. W polu wyszukiwania wpisz `blob`, a następnie wybierz żądany język dla szablonu wyzwalacza usługi Blob Storage.

    ![Wybierz szablon wyzwalacza usługi Blob Storage.](./media/functions-create-storage-blob-triggered-function/functions-create-blob-storage-trigger-portal.png)
 
3. Użyj ustawień w sposób określony w tabeli znajdującej się poniżej obrazu.

    ![Tworzenie funkcji wyzwalanej przez magazyn obiektów Blob.](./media/functions-create-storage-blob-triggered-function/functions-create-blob-storage-trigger-portal-2.png)

    | Ustawienie | Sugerowana wartość | Opis |
    |---|---|---|
    | **Nazwa** | Unikatowa w obrębie aplikacji funkcji | Nazwa funkcji wyzwalanej przez obiekt blob. |
    | **Ścieżka**   | samples-workitems/{name}    | Lokalizacja w monitorowanym magazynie obiektów Blob. Nazwa pliku obiektu Blob jest przekazywana w powiązaniu jako parametr _nazwa_.  |
    | **Połączenie konta magazynu** | AzureWebJobsStorage | Możesz skorzystać z połączenia konta magazynu już używanego przez aplikację funkcji lub utworzyć nowe.  |

3. Kliknij przycisk **Utwórz**, aby utworzyć funkcję.

Następnie nawiąż połączenie z kontem usługi Azure Storage i utwórz kontener **samples-workitems**.

## <a name="create-the-container"></a>Tworzenie kontenera

1. W funkcji kliknij pozycję **Integracja**, rozwiń pozycję **Dokumentacja** i skopiuj wartości pól **Nazwa konta** oraz **Klucz konta**. Te poświadczenia służą do nawiązywania połączenia z kontem magazynu. Jeśli już nawiązano połączenie z kontem magazynu, przejdź do kroku 4.

    ![Uzyskiwanie poświadczeń połączenia konta magazynu.](./media/functions-create-storage-blob-triggered-function/functions-storage-account-connection.png)

1. Uruchom narzędzie [Microsoft Azure Storage Explorer](http://storageexplorer.com/), kliknij ikonę połączenia po lewej stronie, wybierz pozycję **Użyj klucza i nazwy konta magazynu** i kliknij przycisk **Dalej**.

    ![Uruchamianie narzędzia Storage Account Explorer.](./media/functions-create-storage-blob-triggered-function/functions-storage-manager-connect-1.png)

1. Wprowadź wartości **Nazwa konta** i **Klucz konta** z kroku 1, kliknij przycisk **Dalej**, a następnie przycisk **Połącz**. 

    ![Wprowadzanie poświadczeń magazynu i nawiązywanie połączenia.](./media/functions-create-storage-blob-triggered-function/functions-storage-manager-connect-2.png)

1. Rozwiń dołączone konto magazynu, kliknij prawym przyciskiem myszy pozycję **Blob containers** (Kontenery obiektów Blob), kliknij polecenie **Create blob container** (Utwórz kontener obiektów Blob), wpisz nazwę `samples-workitems`, a następnie naciśnij klawisz Enter.

    ![Tworzenie kolejki magazynu.](./media/functions-create-storage-blob-triggered-function/functions-storage-manager-create-blob-container.png)

Teraz, gdy masz już kontener obiektów Blob, możesz przetestować funkcję, przekazując plik do kontenera.

## <a name="test-the-function"></a>Testowanie funkcji

1. Wróć do witryny Azure Portal, przejdź do swoich funkcji, rozwiń pozycję **Dzienniki** w dolnej części strony i upewnij się, że strumieniowe przesyłanie dzienników nie jest wstrzymane.

1. W Eksploratorze usługi Storage rozwiń swoje konto magazynu, pozycję **Blob containers** (Kontenery obiektów Blob) oraz kontener **samples-workitems**. Kliknij pozycję **Upload** (Przekaż), a następnie pozycję **Upload files...** (Przekaż pliki...).

    ![Przekazywanie pliku do kontenera obiektów Blob.](./media/functions-create-storage-blob-triggered-function/functions-storage-manager-upload-file-blob.png)

1. W oknie dialogowym **Upload files** (Przekazywanie plików) kliknij pole **Files** (Pliki). Przejdź do pliku na komputerze lokalnym, na przykład pliku obrazu, zaznacz go i kliknij przycisk **Open** (Otwórz), a następnie przycisk **Upload** (Przekaż).

1. Wróć do dzienników funkcji i sprawdź, czy obiekt Blob został odczytany.

   ![Wyświetlanie komunikatu w dziennikach.](./media/functions-create-storage-blob-triggered-function/functions-blob-storage-trigger-view-logs.png)

    >[!NOTE]
    > Gdy aplikacja funkcji zostanie uruchomiona w domyślnym planie Zużycie, może wystąpić nawet kilkuminutowe opóźnienie między dodaniem lub zaktualizowaniem obiektu Blob a wyzwoleniem funkcji. Jeśli zależy Ci na małych opóźnieniach w funkcjach wyzwalanych przez obiekty Blob, rozważ uruchomienie aplikacji funkcji w planie usługi App Service.

## <a name="clean-up-resources"></a>Oczyszczanie zasobów

[!INCLUDE [Next steps note](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a>Następne kroki

Utworzono funkcję, która jest uruchamiana w momencie dodania obiektu Blob do magazynu obiektów Blob lub zaktualizowania obiektu Blob w magazynie. 

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

Aby uzyskać więcej informacji na temat wyzwalaczy magazynu obiektów Blob, zobacz [Powiązania magazynu obiektów Blob w usłudze Azure Functions](functions-bindings-storage-blob.md).
