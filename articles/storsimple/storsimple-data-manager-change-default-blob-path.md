---
title: "Ścieżka obiektu blob aaaChange z domyślnej hello | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooset zapasowej Azure funkcji toorename ścieżka pliku obiektów blob (w podglądzie prywatnym)"
services: storsimple
documentationcenter: NA
author: vidarmsft
manager: syadav
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 03/16/2017
ms.author: vidarmsft
ms.openlocfilehash: 2c414603514223c701ab1a3bd0b81ee18f1af666
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="change-a-blob-path-from-hello-default-path-private-preview"></a>Zmień ścieżkę obiektu blob z hello domyślna ścieżka (w podglądzie prywatnym)

W tym artykule opisano, jak tooset zapasowej Azure funkcji toorename domyślna ścieżka pliku obiektu blob. 

## <a name="prerequisites"></a>Wymagania wstępne

Upewnij się, że masz definicji zadania, który został poprawnie skonfigurowany w zasobie danych hybrydowych w grupie zasobów.

## <a name="create-an-azure-function"></a>Tworzenie funkcji platformy Azure

toocreate funkcję Azure hello następujące:

1. Przejdź toohello [portalu Azure](http://portal.azure.com/).

2. Witaj górnej części okienka po lewej stronie powitania kliknij **nowy**. 

3. W hello **wyszukiwania** wpisz **aplikacji funkcji**, a następnie naciśnij klawisz Enter.

    ![W polu wyszukiwania hello wpisz "Funkcja aplikacji"](./media/storsimple-data-manager-change-default-blob-path/goto-function-app-resource.png)

4. W hello **wyniki** kliknij **aplikacji funkcji**.

    ![Wybierz zasób aplikacji hello funkcja hello listy wyników](./media/storsimple-data-manager-change-default-blob-path/select-function-app-resource.png)

    Witaj **aplikacji funkcji** zostanie otwarte okno.

5. Kliknij przycisk **Utwórz**.

    ![przycisk "Utwórz" okna funkcji aplikacji Hello](./media/storsimple-data-manager-change-default-blob-path/create-new-function-app.png)

6. Na powitania **aplikacji funkcji** blok konfiguracji hello następujące:

    a. W hello **Nazwa aplikacji** okno, nazwa aplikacji hello typu.
    
    b. W hello **subskrypcji** okno, nazwa typu hello hello subskrypcji.

    c. W obszarze **grupy zasobów**, kliknij przycisk **Utwórz nowy**, a następnie nazwę hello typu hello grupy zasobów.

    d. W hello **Plan hostingu** wpisz **zaplanować użycie**.

    e. W hello **lokalizacji** pole lokalizacji hello typu.

    f. W obszarze **konta magazynu**wybierz istniejące konto magazynu lub Utwórz nowe konto magazynu. Konto magazynu jest używana wewnętrznie do funkcji hello.

    ![Wprowadź nowe dane konfiguracji funkcji aplikacji](./media/storsimple-data-manager-change-default-blob-path/enter-new-funcion-app-data.png)

7. Kliknij przycisk **Utwórz**.  
    Utworzono Hello funkcji aplikacji.

8. W okienku po lewej stronie powitania kliknij **więcej usług**, a następnie hello następujące:
    
    a. W hello **filtru** wpisz **usługi aplikacji**.
    
    b. Kliknij przycisk **usługi aplikacji**. 

    ![Łącze "Więcej usług" w okienku po lewej stronie powitania](./media/storsimple-data-manager-change-default-blob-path/more-services.png)

9. Na liście hello usług aplikacji kliknij nazwę hello hello funkcji aplikacji.  
    zostanie otwarta strona aplikacji funkcja Hello.

10. W okienku po lewej stronie powitania kliknij **nową funkcję**, a następnie hello następujące: 

    a. W hello **języka** listy, wybierz **C#**.
    
    b. W tablicy hello Kafelki szablonu, wybierz **QueueTrigger CSharp**.

    c. W hello **nazwy funkcji** wpisz nazwę funkcji.

    d. W hello **Nazwa kolejki** wpisz nazwę definicji zadania transformacji danych.

    e. W obszarze **połączenia konta magazynu**, kliknij przycisk **nowe**, a następnie wybierz konto hello, odpowiadający toohello transformacji danych zadania.  
        Zanotuj nazwę połączenia hello. wymagana jest nazwa Hello później w hello funkcji platformy Azure.

       ![Utwórz nową funkcję C#](./media/storsimple-data-manager-change-default-blob-path/create-new-csharp-function.png)

    f. Kliknij przycisk **Utwórz**.  
    Witaj **funkcja** zostanie otwarte okno.

11. W hello **funkcja** okna, uruchom _csx_ pliku, a następnie hello następujące:

    a. Wklej hello następującego kodu:

    ```
    using System;
    using System.Configuration;
    using Microsoft.WindowsAzure.Storage.Blob;
    using Microsoft.WindowsAzure.Storage.Queue;
    using Microsoft.WindowsAzure.Storage;
    using System.Collections.Generic;
    using System.Linq;

    public static void Run(QueueItem myQueueItem, TraceWriter log)
    {
        CloudStorageAccount storageAccount = CloudStorageAccount.Parse(ConfigurationManager.AppSettings["STORAGE_CONNECTIONNAME"]);

        string storageAccUriEndswith = "windows.net/";
        string uri = myQueueItem.TargetLocation.Replace("%20", " ");
        log.Info($"Blob Uri: {uri}");

        // Remove storage account uri string
        uri = uri.Substring(uri.IndexOf(storageAccUriEndswith) + storageAccUriEndswith.Length);

        string containerName = uri.Substring(0, uri.IndexOf("/")); 

        // Remove container name string
        uri = uri.Substring(containerName.Length + 1);

        // Current blob path
        string blobName = uri; 

        string volumeName = uri.Substring(containerName.Length + 1);
        volumeName = uri.Substring(0, uri.IndexOf("/"));

        // Remove volume name string
        uri = uri.Substring(volumeName.Length + 1);

        string newContainerName = uri.Substring(0, uri.IndexOf("/")).ToLower();
        string newBlobName = uri.Substring(newContainerName.Length + 1);

        log.Info($"Container name: {containerName}");
        log.Info($"Volume name: {volumeName}");
        log.Info($"New container name: {newContainerName}");

        log.Info($"Blob name: {blobName}");
        log.Info($"New blob name: {newBlobName}");

        // Create hello blob client.
        CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

        // Container reference
        CloudBlobContainer container = blobClient.GetContainerReference(containerName);
        CloudBlobContainer newContainer = blobClient.GetContainerReference(newContainerName);
        newContainer.CreateIfNotExists();

        if(!container.Exists())
        {
            log.Info($"Container - {containerName} not exists");
            return;
        }

        if(!newContainer.Exists())
        {
            log.Info($"Container - {newContainerName} not exists");
            return;
        }

        CloudBlockBlob blob = container.GetBlockBlobReference(blobName);
        if (!blob.Exists())
        {
            // Skip toocopy hello blob toonew container, if source blob doesn't exist
            log.Info($"hello specified blob does not exist.");
            log.Info($"Blob Uri: {blob.Uri}");
            return;
        }

        CloudBlockBlob blobCopy = newContainer.GetBlockBlobReference(newBlobName);
        if (!blobCopy.Exists())
        {
            blobCopy.StartCopy(blob);
            // Delete old blob, after copy toonew container
            blob.DeleteIfExists();
            log.Info($"Blob file path renamed completed successfully");
        }
        else
        {
            log.Info($"Blob file path renamed already done");
            // Delete old blob, if already exists.
            blob.DeleteIfExists();
        }
    }

    public class QueueItem
    {
        public string SourceLocation {get;set;}
        public long SizeInBytes {get;set;}
        public string Status {get;set;}
        public string JobID {get;set;}
        public string TargetLocation {get; set;}
    }

    ```

    b. Zastąp **STORAGE_CONNECTIONNAME** w wierszu 11 z połączeniem konta magazynu (zobacz punkt 8 c).

    c. W lewej górnej powitania kliknij **zapisać**.

    ![Zapisz — funkcja](./media/storsimple-data-manager-change-default-blob-path/save-function.png)

12. toocomplete hello funkcję, Dodaj więcej plików, wykonując następujące hello:

    a. Kliknij przycisk **wyświetlać pliki**.

       ![łącze "Wyświetl pliki" Hello](./media/storsimple-data-manager-change-default-blob-path/view-files.png)

    b. Kliknij pozycję **Dodaj**.
    
    c. Typ **project.json**, a następnie naciśnij klawisz Enter.
    
    d. W hello **project.json** plików, Wklej hello następującego kodu:

    ```
    {
    "frameworks": {
        "net46":{
        "dependencies": {
            "windowsazure.storage": "8.1.1"
        }
        }
    }
    }

    ```

    e. Kliknij pozycję **Zapisz**.

Utworzono funkcji platformy Azure. Ta funkcja jest wywoływane zawsze, gdy nowy obiekt blob jest generowany przez zadanie transformacji danych hello.

## <a name="next-steps"></a>Następne kroki

[Użyj interfejsu użytkownika Menedżera danych StorSimple tootransform danych](storsimple-data-manager-ui.md)
