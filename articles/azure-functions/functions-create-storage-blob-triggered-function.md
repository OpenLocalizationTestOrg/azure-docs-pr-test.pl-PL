---
title: "aaaCreate funkcji na platformie Azure wyzwalane przez magazynu obiektów Blob | Dokumentacja firmy Microsoft"
description: "Użyj usługi Azure Functions toocreate niekorzystającą funkcji, który jest wywoływany przez elementy dodane tooAzure magazynu obiektów Blob."
services: azure-functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
ms.assetid: d6bff41c-a624-40c1-bbc7-80590df29ded
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/31/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: acb7d29abb07a22da11d0e65d2ed54591f8e3f4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-function-triggered-by-azure-blob-storage"></a><span data-ttu-id="f0406-103">Tworzenie funkcji wyzwalanej przez magazyn obiektów Blob</span><span class="sxs-lookup"><span data-stu-id="f0406-103">Create a function triggered by Azure Blob storage</span></span>

<span data-ttu-id="f0406-104">Dowiedz się, jak toocreate funkcji wyzwalane, gdy pliki są przekazywane tooor zaktualizowane w magazynie obiektów Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="f0406-104">Learn how toocreate a function triggered when files are uploaded tooor updated in Azure Blob storage.</span></span>

![Przeglądanie wiadomości w dziennikach hello.](./media/functions-create-storage-blob-triggered-function/function-app-in-portal-editor.png)

## <a name="prerequisites"></a><span data-ttu-id="f0406-106">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="f0406-106">Prerequisites</span></span>

+ <span data-ttu-id="f0406-107">Pobierz i zainstaluj hello [Eksploratora usługi Microsoft Azure Storage](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="f0406-107">Download and install hello [Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span></span>
+ <span data-ttu-id="f0406-108">Subskrypcja platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="f0406-108">An Azure subscription.</span></span> <span data-ttu-id="f0406-109">Jeśli nie masz subskrypcji, przed rozpoczęciem utwórz [bezpłatne konto](https://azure.microsoft.com/free/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="f0406-109">If you don't have one, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

## <a name="create-an-azure-function-app"></a><span data-ttu-id="f0406-110">Tworzenie aplikacji funkcji platformy Azure</span><span class="sxs-lookup"><span data-stu-id="f0406-110">Create an Azure Function app</span></span>

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

![Pomyślnie utworzona aplikacja funkcji.](./media/functions-create-first-azure-function/function-app-create-success.png)

<span data-ttu-id="f0406-112">Następnie należy utworzyć funkcji w hello nowej funkcji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f0406-112">Next, you create a function in hello new function app.</span></span>

<a name="create-function"></a>

## <a name="create-a-blob-storage-triggered-function"></a><span data-ttu-id="f0406-113">Tworzenie funkcji wyzwalanej przez magazyn obiektów Blob</span><span class="sxs-lookup"><span data-stu-id="f0406-113">Create a Blob storage triggered function</span></span>

1. <span data-ttu-id="f0406-114">Rozwiń węzeł funkcji aplikacji, a następnie kliknij przycisk hello  **+**  obok przycisku zbyt**funkcji**.</span><span class="sxs-lookup"><span data-stu-id="f0406-114">Expand your function app and click hello **+** button next too**Functions**.</span></span> <span data-ttu-id="f0406-115">Jeśli hello pierwszej funkcji w funkcji aplikacji, wybierz **Niestandardowa funkcja**.</span><span class="sxs-lookup"><span data-stu-id="f0406-115">If this is hello first function in your function app, select **Custom function**.</span></span> <span data-ttu-id="f0406-116">Spowoduje to wyświetlenie hello pełny zestaw szablonów funkcji.</span><span class="sxs-lookup"><span data-stu-id="f0406-116">This displays hello complete set of function templates.</span></span>

    ![Funkcje strony szybkiego startu w hello portalu Azure](./media/functions-create-storage-blob-triggered-function/add-first-function.png)

2. <span data-ttu-id="f0406-118">Wybierz hello **BlobTrigger** szablonu żądany język i użyj hello ustawień określonych w tabeli hello.</span><span class="sxs-lookup"><span data-stu-id="f0406-118">Select hello **BlobTrigger** template for your desired language, and use hello settings as specified in hello table.</span></span>

    ![Tworzenie funkcji wyzwalane magazynu obiektów Blob hello.](./media/functions-create-storage-blob-triggered-function/functions-create-blob-storage-trigger-portal.png)

    | <span data-ttu-id="f0406-120">Ustawienie</span><span class="sxs-lookup"><span data-stu-id="f0406-120">Setting</span></span> | <span data-ttu-id="f0406-121">Sugerowana wartość</span><span class="sxs-lookup"><span data-stu-id="f0406-121">Suggested value</span></span> | <span data-ttu-id="f0406-122">Opis</span><span class="sxs-lookup"><span data-stu-id="f0406-122">Description</span></span> |
    |---|---|---|
    | <span data-ttu-id="f0406-123">**Ścieżka**</span><span class="sxs-lookup"><span data-stu-id="f0406-123">**Path**</span></span>   | <span data-ttu-id="f0406-124">mycontainer/{nazwa}</span><span class="sxs-lookup"><span data-stu-id="f0406-124">mycontainer/{name}</span></span>    | <span data-ttu-id="f0406-125">Lokalizacja w monitorowanym magazynie obiektów Blob.</span><span class="sxs-lookup"><span data-stu-id="f0406-125">Location in Blob storage being monitored.</span></span> <span data-ttu-id="f0406-126">Nazwa pliku Hello hello obiektu blob jest przekazywany w powiązaniu hello jako hello _nazwa_ parametru.</span><span class="sxs-lookup"><span data-stu-id="f0406-126">hello file name of hello blob is passed in hello binding as hello _name_ parameter.</span></span>  |
    | <span data-ttu-id="f0406-127">**Połączenie konta magazynu**</span><span class="sxs-lookup"><span data-stu-id="f0406-127">**Storage account connection**</span></span> | <span data-ttu-id="f0406-128">AzureWebJobStorage</span><span class="sxs-lookup"><span data-stu-id="f0406-128">AzureWebJobStorage</span></span> | <span data-ttu-id="f0406-129">Użyj połączenia konta magazynu hello już używana przez aplikację funkcji lub Utwórz nową.</span><span class="sxs-lookup"><span data-stu-id="f0406-129">You can use hello storage account connection already being used by your function app, or create a new one.</span></span>  |
    | <span data-ttu-id="f0406-130">**Nazwa funkcji**</span><span class="sxs-lookup"><span data-stu-id="f0406-130">**Name your function**</span></span> | <span data-ttu-id="f0406-131">Unikatowa w obrębie aplikacji funkcji</span><span class="sxs-lookup"><span data-stu-id="f0406-131">Unique in your function app</span></span> | <span data-ttu-id="f0406-132">Nazwa funkcji wyzwalanej przez obiekt blob.</span><span class="sxs-lookup"><span data-stu-id="f0406-132">Name of this blob triggered function.</span></span> |

3. <span data-ttu-id="f0406-133">Kliknij przycisk **Utwórz** toocreate funkcji.</span><span class="sxs-lookup"><span data-stu-id="f0406-133">Click **Create** toocreate your function.</span></span>

<span data-ttu-id="f0406-134">Następnie połączyć konto magazynu Azure tooyour i utworzyć hello **mojkontener** kontenera.</span><span class="sxs-lookup"><span data-stu-id="f0406-134">Next, you connect tooyour Azure Storage account and create hello **mycontainer** container.</span></span>

## <a name="create-hello-container"></a><span data-ttu-id="f0406-135">Tworzenie kontenera hello</span><span class="sxs-lookup"><span data-stu-id="f0406-135">Create hello container</span></span>

1. <span data-ttu-id="f0406-136">W funkcji kliknij pozycję **Integracja**, rozwiń pozycję **Dokumentacja** i skopiuj wartości pól **Nazwa konta** oraz **Klucz konta**.</span><span class="sxs-lookup"><span data-stu-id="f0406-136">In your function, click **Integrate**, expand **Documentation**, and copy both **Account name** and **Account key**.</span></span> <span data-ttu-id="f0406-137">Używasz konta magazynu te poświadczenia tooconnect toohello.</span><span class="sxs-lookup"><span data-stu-id="f0406-137">You use these credentials tooconnect toohello storage account.</span></span> <span data-ttu-id="f0406-138">Jeśli nawiązano już połączenie konta magazynu, Pomiń toostep 4.</span><span class="sxs-lookup"><span data-stu-id="f0406-138">If you have already connected your storage account, skip toostep 4.</span></span>

    ![Uzyskaj konto magazynu hello poświadczeń dla połączenia.](./media/functions-create-storage-blob-triggered-function/functions-storage-account-connection.png)

1. <span data-ttu-id="f0406-140">Uruchom hello [Eksploratora usługi Microsoft Azure Storage](http://storageexplorer.com/) narzędzia, kliknij przycisk hello połączenia powitania po lewej stronie, wybierz **użyć nazwy konta magazynu i klucza**i kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="f0406-140">Run hello [Microsoft Azure Storage Explorer](http://storageexplorer.com/) tool, click hello connect icon on hello left, choose **Use a storage account name and key**, and click **Next**.</span></span>

    ![Uruchom narzędzie Eksploratora usługi Storage konta hello.](./media/functions-create-storage-blob-triggered-function/functions-storage-manager-connect-1.png)

1. <span data-ttu-id="f0406-142">Wprowadź hello **nazwa konta** i **klucz konta** z kroku 1, kliknij przycisk **dalej** , a następnie **Connect**.</span><span class="sxs-lookup"><span data-stu-id="f0406-142">Enter hello **Account name** and **Account key** from step 1, click **Next** and then **Connect**.</span></span> 

    ![Wprowadź poświadczenia magazynu hello i połącz.](./media/functions-create-storage-blob-triggered-function/functions-storage-manager-connect-2.png)

1. <span data-ttu-id="f0406-144">Rozwiń hello dołączony konta magazynu, kliknij prawym przyciskiem myszy **obiektu Blob kontenery**, kliknij przycisk **Tworzenie kontenera obiektów blob**, typu `mycontainer`, a następnie naciśnij klawisz enter.</span><span class="sxs-lookup"><span data-stu-id="f0406-144">Expand hello attached storage account, right-click **Blob containers**, click **Create blob container**, type `mycontainer`, and then press enter.</span></span>

    ![Tworzenie kolejki magazynu.](./media/functions-create-storage-blob-triggered-function/functions-storage-manager-create-blob-container.png)

<span data-ttu-id="f0406-146">Teraz, gdy masz kontenera obiektów blob można przetestować funkcji hello przekazując kontenera toohello plików.</span><span class="sxs-lookup"><span data-stu-id="f0406-146">Now that you have a blob container, you can test hello function by uploading a file toohello container.</span></span>

## <a name="test-hello-function"></a><span data-ttu-id="f0406-147">Funkcja hello testu</span><span class="sxs-lookup"><span data-stu-id="f0406-147">Test hello function</span></span>

1. <span data-ttu-id="f0406-148">W portalu Azure hello, funkcja tooyour przeglądania rozwiń hello **dzienniki** u dołu strony hello i upewnij się, że hello przesyłania strumieniowego tego dziennika nie jest wstrzymana.</span><span class="sxs-lookup"><span data-stu-id="f0406-148">Back in hello Azure portal, browse tooyour function expand hello **Logs** at hello bottom of hello page and make sure that log streaming isn't paused.</span></span>

1. <span data-ttu-id="f0406-149">W programie Storage Explorer rozwiń swoje konto magazynu i wybierz kolejno pozycje **Blob containers** (Kontenery obiektów Blob) oraz **mycontainer**.</span><span class="sxs-lookup"><span data-stu-id="f0406-149">In Storage Explorer, expand your storage account, **Blob containers**, and **mycontainer**.</span></span> <span data-ttu-id="f0406-150">Kliknij pozycję **Upload** (Przekaż), a następnie pozycję **Upload files...** (Przekaż pliki...).</span><span class="sxs-lookup"><span data-stu-id="f0406-150">Click **Upload** and then **Upload files...**.</span></span>

    ![Przekaż plik toohello kontenera obiektów blob.](./media/functions-create-storage-blob-triggered-function/functions-storage-manager-upload-file-blob.png)

1. <span data-ttu-id="f0406-152">W hello **przekazać pliki** okna dialogowego kliknij hello **pliki** pola.</span><span class="sxs-lookup"><span data-stu-id="f0406-152">In hello **Upload files** dialog box, click hello **Files** field.</span></span> <span data-ttu-id="f0406-153">Przeglądaj plik tooa na komputerze lokalnym, takich jak plik obrazu, zaznacz go i kliknij **Otwórz** , a następnie **przekazać**.</span><span class="sxs-lookup"><span data-stu-id="f0406-153">Browse tooa file on your local computer, such as an image file, select it and click **Open** and then **Upload**.</span></span>

1. <span data-ttu-id="f0406-154">Przejdź wstecz tooyour dzienniki funkcji i sprawdź, czy dany obiekt blob hello został odczytany.</span><span class="sxs-lookup"><span data-stu-id="f0406-154">Go back tooyour function logs and verify that hello blob has been read.</span></span>

   ![Przeglądanie wiadomości w dziennikach hello.](./media/functions-create-storage-blob-triggered-function/functions-blob-storage-trigger-view-logs.png)

    >[!NOTE]
    > <span data-ttu-id="f0406-156">Po uruchomieniu aplikacji funkcja hello domyślne użycie planu, może istnieć opóźnienie się tooseveral minut między hello obiektów blob są dodane lub zaktualizowane i hello funkcji inicjowane.</span><span class="sxs-lookup"><span data-stu-id="f0406-156">When your function app runs in hello default Consumption plan, there may be a delay of up tooseveral minutes between hello blob being added or updated and hello function being triggered.</span></span> <span data-ttu-id="f0406-157">Jeśli zależy Ci na małych opóźnieniach w funkcjach wyzwalanych przez obiekty Blob, rozważ uruchomienie aplikacji funkcji w planie usługi App Service.</span><span class="sxs-lookup"><span data-stu-id="f0406-157">If you need low latency in your blob triggered functions, consider running your function app in an App Service plan.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="f0406-158">Oczyszczanie zasobów</span><span class="sxs-lookup"><span data-stu-id="f0406-158">Clean up resources</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a><span data-ttu-id="f0406-159">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f0406-159">Next steps</span></span>

<span data-ttu-id="f0406-160">Utworzono funkcję, która jest uruchamiana po dodaniu tooor zaktualizowane obiektu blob w magazynie obiektów Blob.</span><span class="sxs-lookup"><span data-stu-id="f0406-160">You have created a function that runs when a blob is added tooor updated in Blob storage.</span></span> 

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

<span data-ttu-id="f0406-161">Aby uzyskać więcej informacji na temat wyzwalaczy magazynu obiektów Blob, zobacz [Powiązania magazynu obiektów Blob w usłudze Azure Functions](functions-bindings-storage-blob.md).</span><span class="sxs-lookup"><span data-stu-id="f0406-161">For more information about Blob storage triggers, see [Azure Functions Blob storage bindings](functions-bindings-storage-blob.md).</span></span>
