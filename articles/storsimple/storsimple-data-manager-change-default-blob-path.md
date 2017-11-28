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
# <a name="change-a-blob-path-from-hello-default-path-private-preview"></a><span data-ttu-id="afa3d-103">Zmień ścieżkę obiektu blob z hello domyślna ścieżka (w podglądzie prywatnym)</span><span class="sxs-lookup"><span data-stu-id="afa3d-103">Change a blob path from hello default path (private preview)</span></span>

<span data-ttu-id="afa3d-104">W tym artykule opisano, jak tooset zapasowej Azure funkcji toorename domyślna ścieżka pliku obiektu blob.</span><span class="sxs-lookup"><span data-stu-id="afa3d-104">This article describes how tooset up an Azure function toorename a default blob file path.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="afa3d-105">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="afa3d-105">Prerequisites</span></span>

<span data-ttu-id="afa3d-106">Upewnij się, że masz definicji zadania, który został poprawnie skonfigurowany w zasobie danych hybrydowych w grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="afa3d-106">Ensure that you have a job definition that has been correctly configured in a hybrid data resource within a resource group.</span></span>

## <a name="create-an-azure-function"></a><span data-ttu-id="afa3d-107">Tworzenie funkcji platformy Azure</span><span class="sxs-lookup"><span data-stu-id="afa3d-107">Create an Azure function</span></span>

<span data-ttu-id="afa3d-108">toocreate funkcję Azure hello następujące:</span><span class="sxs-lookup"><span data-stu-id="afa3d-108">toocreate an Azure function, do hello following:</span></span>

1. <span data-ttu-id="afa3d-109">Przejdź toohello [portalu Azure](http://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="afa3d-109">Go toohello [Azure portal](http://portal.azure.com/).</span></span>

2. <span data-ttu-id="afa3d-110">Witaj górnej części okienka po lewej stronie powitania kliknij **nowy**.</span><span class="sxs-lookup"><span data-stu-id="afa3d-110">At hello top of hello left pane, click **New**.</span></span> 

3. <span data-ttu-id="afa3d-111">W hello **wyszukiwania** wpisz **aplikacji funkcji**, a następnie naciśnij klawisz Enter.</span><span class="sxs-lookup"><span data-stu-id="afa3d-111">In hello **Search** box, type **Function App**, and then press Enter.</span></span>

    ![W polu wyszukiwania hello wpisz "Funkcja aplikacji"](./media/storsimple-data-manager-change-default-blob-path/goto-function-app-resource.png)

4. <span data-ttu-id="afa3d-113">W hello **wyniki** kliknij **aplikacji funkcji**.</span><span class="sxs-lookup"><span data-stu-id="afa3d-113">In hello **Results** list, click **Function App**.</span></span>

    ![Wybierz zasób aplikacji hello funkcja hello listy wyników](./media/storsimple-data-manager-change-default-blob-path/select-function-app-resource.png)

    <span data-ttu-id="afa3d-115">Witaj **aplikacji funkcji** zostanie otwarte okno.</span><span class="sxs-lookup"><span data-stu-id="afa3d-115">hello **Function App** window opens.</span></span>

5. <span data-ttu-id="afa3d-116">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="afa3d-116">Click **Create**.</span></span>

    ![przycisk "Utwórz" okna funkcji aplikacji Hello](./media/storsimple-data-manager-change-default-blob-path/create-new-function-app.png)

6. <span data-ttu-id="afa3d-118">Na powitania **aplikacji funkcji** blok konfiguracji hello następujące:</span><span class="sxs-lookup"><span data-stu-id="afa3d-118">On hello **Function App** configuration blade, do hello following:</span></span>

    <span data-ttu-id="afa3d-119">a.</span><span class="sxs-lookup"><span data-stu-id="afa3d-119">a.</span></span> <span data-ttu-id="afa3d-120">W hello **Nazwa aplikacji** okno, nazwa aplikacji hello typu.</span><span class="sxs-lookup"><span data-stu-id="afa3d-120">In hello **App name** box, type hello app name.</span></span>
    
    <span data-ttu-id="afa3d-121">b.</span><span class="sxs-lookup"><span data-stu-id="afa3d-121">b.</span></span> <span data-ttu-id="afa3d-122">W hello **subskrypcji** okno, nazwa typu hello hello subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="afa3d-122">In hello **Subscription** box, type hello name of hello subscription.</span></span>

    <span data-ttu-id="afa3d-123">c.</span><span class="sxs-lookup"><span data-stu-id="afa3d-123">c.</span></span> <span data-ttu-id="afa3d-124">W obszarze **grupy zasobów**, kliknij przycisk **Utwórz nowy**, a następnie nazwę hello typu hello grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="afa3d-124">Under **Resource Group**, click **Create new**, and then type hello name of hello resource group.</span></span>

    <span data-ttu-id="afa3d-125">d.</span><span class="sxs-lookup"><span data-stu-id="afa3d-125">d.</span></span> <span data-ttu-id="afa3d-126">W hello **Plan hostingu** wpisz **zaplanować użycie**.</span><span class="sxs-lookup"><span data-stu-id="afa3d-126">In hello **Hosting Plan** box, type **Consumption Plan**.</span></span>

    <span data-ttu-id="afa3d-127">e.</span><span class="sxs-lookup"><span data-stu-id="afa3d-127">e.</span></span> <span data-ttu-id="afa3d-128">W hello **lokalizacji** pole lokalizacji hello typu.</span><span class="sxs-lookup"><span data-stu-id="afa3d-128">In hello **Location** box, type hello location.</span></span>

    <span data-ttu-id="afa3d-129">f.</span><span class="sxs-lookup"><span data-stu-id="afa3d-129">f.</span></span> <span data-ttu-id="afa3d-130">W obszarze **konta magazynu**wybierz istniejące konto magazynu lub Utwórz nowe konto magazynu.</span><span class="sxs-lookup"><span data-stu-id="afa3d-130">Under **Storage account**, select an existing storage account or create a new storage account.</span></span> <span data-ttu-id="afa3d-131">Konto magazynu jest używana wewnętrznie do funkcji hello.</span><span class="sxs-lookup"><span data-stu-id="afa3d-131">A storage account is used internally for hello function.</span></span>

    ![Wprowadź nowe dane konfiguracji funkcji aplikacji](./media/storsimple-data-manager-change-default-blob-path/enter-new-funcion-app-data.png)

7. <span data-ttu-id="afa3d-133">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="afa3d-133">Click **Create**.</span></span>  
    <span data-ttu-id="afa3d-134">Utworzono Hello funkcji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="afa3d-134">hello function app is created.</span></span>

8. <span data-ttu-id="afa3d-135">W okienku po lewej stronie powitania kliknij **więcej usług**, a następnie hello następujące:</span><span class="sxs-lookup"><span data-stu-id="afa3d-135">In hello left pane, click **More services**, and then do hello following:</span></span>
    
    <span data-ttu-id="afa3d-136">a.</span><span class="sxs-lookup"><span data-stu-id="afa3d-136">a.</span></span> <span data-ttu-id="afa3d-137">W hello **filtru** wpisz **usługi aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="afa3d-137">In hello **Filter** box, type **App services**.</span></span>
    
    <span data-ttu-id="afa3d-138">b.</span><span class="sxs-lookup"><span data-stu-id="afa3d-138">b.</span></span> <span data-ttu-id="afa3d-139">Kliknij przycisk **usługi aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="afa3d-139">Click **App Services**.</span></span> 

    ![Łącze "Więcej usług" w okienku po lewej stronie powitania](./media/storsimple-data-manager-change-default-blob-path/more-services.png)

9. <span data-ttu-id="afa3d-141">Na liście hello usług aplikacji kliknij nazwę hello hello funkcji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="afa3d-141">In hello list of app services, click hello name of hello function app.</span></span>  
    <span data-ttu-id="afa3d-142">zostanie otwarta strona aplikacji funkcja Hello.</span><span class="sxs-lookup"><span data-stu-id="afa3d-142">hello function app page opens.</span></span>

10. <span data-ttu-id="afa3d-143">W okienku po lewej stronie powitania kliknij **nową funkcję**, a następnie hello następujące:</span><span class="sxs-lookup"><span data-stu-id="afa3d-143">In hello left pane, click **New Function**, and then do hello following:</span></span> 

    <span data-ttu-id="afa3d-144">a.</span><span class="sxs-lookup"><span data-stu-id="afa3d-144">a.</span></span> <span data-ttu-id="afa3d-145">W hello **języka** listy, wybierz **C#**.</span><span class="sxs-lookup"><span data-stu-id="afa3d-145">In hello **Language** list, select **C#**.</span></span>
    
    <span data-ttu-id="afa3d-146">b.</span><span class="sxs-lookup"><span data-stu-id="afa3d-146">b.</span></span> <span data-ttu-id="afa3d-147">W tablicy hello Kafelki szablonu, wybierz **QueueTrigger CSharp**.</span><span class="sxs-lookup"><span data-stu-id="afa3d-147">In hello array of template tiles, select **QueueTrigger-CSharp**.</span></span>

    <span data-ttu-id="afa3d-148">c.</span><span class="sxs-lookup"><span data-stu-id="afa3d-148">c.</span></span> <span data-ttu-id="afa3d-149">W hello **nazwy funkcji** wpisz nazwę funkcji.</span><span class="sxs-lookup"><span data-stu-id="afa3d-149">In hello **Name your function** box, type a name for your function.</span></span>

    <span data-ttu-id="afa3d-150">d.</span><span class="sxs-lookup"><span data-stu-id="afa3d-150">d.</span></span> <span data-ttu-id="afa3d-151">W hello **Nazwa kolejki** wpisz nazwę definicji zadania transformacji danych.</span><span class="sxs-lookup"><span data-stu-id="afa3d-151">In hello **Queue name** box, type your data-transformation job definition name.</span></span>

    <span data-ttu-id="afa3d-152">e.</span><span class="sxs-lookup"><span data-stu-id="afa3d-152">e.</span></span> <span data-ttu-id="afa3d-153">W obszarze **połączenia konta magazynu**, kliknij przycisk **nowe**, a następnie wybierz konto hello, odpowiadający toohello transformacji danych zadania.</span><span class="sxs-lookup"><span data-stu-id="afa3d-153">Under **Storage account connection**, click **new**, and then select hello account that corresponds toohello data-transformation job.</span></span>  
        <span data-ttu-id="afa3d-154">Zanotuj nazwę połączenia hello.</span><span class="sxs-lookup"><span data-stu-id="afa3d-154">Make a note of hello connection name.</span></span> <span data-ttu-id="afa3d-155">wymagana jest nazwa Hello później w hello funkcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="afa3d-155">hello name is required later in hello Azure function.</span></span>

       ![Utwórz nową funkcję C#](./media/storsimple-data-manager-change-default-blob-path/create-new-csharp-function.png)

    <span data-ttu-id="afa3d-157">f.</span><span class="sxs-lookup"><span data-stu-id="afa3d-157">f.</span></span> <span data-ttu-id="afa3d-158">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="afa3d-158">Click **Create**.</span></span>  
    <span data-ttu-id="afa3d-159">Witaj **funkcja** zostanie otwarte okno.</span><span class="sxs-lookup"><span data-stu-id="afa3d-159">hello **Function** window opens.</span></span>

11. <span data-ttu-id="afa3d-160">W hello **funkcja** okna, uruchom _csx_ pliku, a następnie hello następujące:</span><span class="sxs-lookup"><span data-stu-id="afa3d-160">In hello **Function** window, run _.csx_ file, and then do hello following:</span></span>

    <span data-ttu-id="afa3d-161">a.</span><span class="sxs-lookup"><span data-stu-id="afa3d-161">a.</span></span> <span data-ttu-id="afa3d-162">Wklej hello następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="afa3d-162">Paste hello following code:</span></span>

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

    <span data-ttu-id="afa3d-163">b.</span><span class="sxs-lookup"><span data-stu-id="afa3d-163">b.</span></span> <span data-ttu-id="afa3d-164">Zastąp **STORAGE_CONNECTIONNAME** w wierszu 11 z połączeniem konta magazynu (zobacz punkt 8 c).</span><span class="sxs-lookup"><span data-stu-id="afa3d-164">Replace **STORAGE_CONNECTIONNAME** on line 11 with your storage account connection (refer point 8c).</span></span>

    <span data-ttu-id="afa3d-165">c.</span><span class="sxs-lookup"><span data-stu-id="afa3d-165">c.</span></span> <span data-ttu-id="afa3d-166">W lewej górnej powitania kliknij **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="afa3d-166">At hello top left, click **Save**.</span></span>

    ![Zapisz — funkcja](./media/storsimple-data-manager-change-default-blob-path/save-function.png)

12. <span data-ttu-id="afa3d-168">toocomplete hello funkcję, Dodaj więcej plików, wykonując następujące hello:</span><span class="sxs-lookup"><span data-stu-id="afa3d-168">toocomplete hello function, add one more file by doing hello following:</span></span>

    <span data-ttu-id="afa3d-169">a.</span><span class="sxs-lookup"><span data-stu-id="afa3d-169">a.</span></span> <span data-ttu-id="afa3d-170">Kliknij przycisk **wyświetlać pliki**.</span><span class="sxs-lookup"><span data-stu-id="afa3d-170">Click **View files**.</span></span>

       ![łącze "Wyświetl pliki" Hello](./media/storsimple-data-manager-change-default-blob-path/view-files.png)

    <span data-ttu-id="afa3d-172">b.</span><span class="sxs-lookup"><span data-stu-id="afa3d-172">b.</span></span> <span data-ttu-id="afa3d-173">Kliknij pozycję **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="afa3d-173">Click **Add**.</span></span>
    
    <span data-ttu-id="afa3d-174">c.</span><span class="sxs-lookup"><span data-stu-id="afa3d-174">c.</span></span> <span data-ttu-id="afa3d-175">Typ **project.json**, a następnie naciśnij klawisz Enter.</span><span class="sxs-lookup"><span data-stu-id="afa3d-175">Type **project.json**, and then press Enter.</span></span>
    
    <span data-ttu-id="afa3d-176">d.</span><span class="sxs-lookup"><span data-stu-id="afa3d-176">d.</span></span> <span data-ttu-id="afa3d-177">W hello **project.json** plików, Wklej hello następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="afa3d-177">In hello **project.json** file, paste hello following code:</span></span>

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

    <span data-ttu-id="afa3d-178">e.</span><span class="sxs-lookup"><span data-stu-id="afa3d-178">e.</span></span> <span data-ttu-id="afa3d-179">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="afa3d-179">Click **Save**.</span></span>

<span data-ttu-id="afa3d-180">Utworzono funkcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="afa3d-180">You have created an Azure function.</span></span> <span data-ttu-id="afa3d-181">Ta funkcja jest wywoływane zawsze, gdy nowy obiekt blob jest generowany przez zadanie transformacji danych hello.</span><span class="sxs-lookup"><span data-stu-id="afa3d-181">This function is triggered each time a new blob is generated by hello data-transformation job.</span></span>

## <a name="next-steps"></a><span data-ttu-id="afa3d-182">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="afa3d-182">Next steps</span></span>

[<span data-ttu-id="afa3d-183">Użyj interfejsu użytkownika Menedżera danych StorSimple tootransform danych</span><span class="sxs-lookup"><span data-stu-id="afa3d-183">Use StorSimple Data Manager UI tootransform your data</span></span>](storsimple-data-manager-ui.md)
