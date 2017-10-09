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
# <a name="create-a-function-triggered-by-azure-queue-storage"></a><span data-ttu-id="1535c-103">Tworzenie funkcji wyzwalanej przez usługę Azure Queue Storage</span><span class="sxs-lookup"><span data-stu-id="1535c-103">Create a function triggered by Azure Queue storage</span></span>

<span data-ttu-id="1535c-104">Dowiedz się, jak toocreate funkcji wyzwalane, gdy wiadomości są przesyłane tooan kolejki magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="1535c-104">Learn how toocreate a function triggered when messages are submitted tooan Azure Storage queue.</span></span>

![Przeglądanie wiadomości w dziennikach hello.](./media/functions-create-storage-queue-triggered-function/function-app-in-portal-editor.png)

## <a name="prerequisites"></a><span data-ttu-id="1535c-106">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="1535c-106">Prerequisites</span></span>

- <span data-ttu-id="1535c-107">Pobierz i zainstaluj hello [Eksploratora usługi Microsoft Azure Storage](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="1535c-107">Download and install hello [Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span></span>

- <span data-ttu-id="1535c-108">Subskrypcja platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="1535c-108">An Azure subscription.</span></span> <span data-ttu-id="1535c-109">Jeśli nie masz subskrypcji, przed rozpoczęciem utwórz [bezpłatne konto](https://azure.microsoft.com/free/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="1535c-109">If you don't have one, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

## <a name="create-an-azure-function-app"></a><span data-ttu-id="1535c-110">Tworzenie aplikacji funkcji platformy Azure</span><span class="sxs-lookup"><span data-stu-id="1535c-110">Create an Azure Function app</span></span>

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

![Pomyślnie utworzona aplikacja funkcji.](./media/functions-create-first-azure-function/function-app-create-success.png)

<span data-ttu-id="1535c-112">Następnie należy utworzyć funkcji w hello nowej funkcji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1535c-112">Next, you create a function in hello new function app.</span></span>

<a name="create-function"></a>

## <a name="create-a-queue-triggered-function"></a><span data-ttu-id="1535c-113">Tworzenie funkcji wyzwalanej przez kolejkę</span><span class="sxs-lookup"><span data-stu-id="1535c-113">Create a Queue triggered function</span></span>

1. <span data-ttu-id="1535c-114">Rozwiń węzeł funkcji aplikacji, a następnie kliknij przycisk hello  **+**  obok przycisku zbyt**funkcji**.</span><span class="sxs-lookup"><span data-stu-id="1535c-114">Expand your function app and click hello **+** button next too**Functions**.</span></span> <span data-ttu-id="1535c-115">Jeśli hello pierwszej funkcji w funkcji aplikacji, wybierz **Niestandardowa funkcja**.</span><span class="sxs-lookup"><span data-stu-id="1535c-115">If this is hello first function in your function app, select **Custom function**.</span></span> <span data-ttu-id="1535c-116">Spowoduje to wyświetlenie hello pełny zestaw szablonów funkcji.</span><span class="sxs-lookup"><span data-stu-id="1535c-116">This displays hello complete set of function templates.</span></span>

    ![Funkcje strony szybkiego startu w hello portalu Azure](./media/functions-create-storage-queue-triggered-function/add-first-function.png)

2. <span data-ttu-id="1535c-118">Wybierz hello **QueueTrigger** szablonu żądany język i użyj hello ustawień określonych w tabeli hello.</span><span class="sxs-lookup"><span data-stu-id="1535c-118">Select hello **QueueTrigger** template for your desired language, and  use hello settings as specified in hello table.</span></span>

    ![Tworzenie funkcji wyzwalane kolejki magazynu hello.](./media/functions-create-storage-queue-triggered-function/functions-create-queue-storage-trigger-portal.png)
    
    | <span data-ttu-id="1535c-120">Ustawienie</span><span class="sxs-lookup"><span data-stu-id="1535c-120">Setting</span></span> | <span data-ttu-id="1535c-121">Sugerowana wartość</span><span class="sxs-lookup"><span data-stu-id="1535c-121">Suggested value</span></span> | <span data-ttu-id="1535c-122">Opis</span><span class="sxs-lookup"><span data-stu-id="1535c-122">Description</span></span> |
    |---|---|---|
    | <span data-ttu-id="1535c-123">**Nazwa kolejki**</span><span class="sxs-lookup"><span data-stu-id="1535c-123">**Queue name**</span></span>   | <span data-ttu-id="1535c-124">myqueue-items</span><span class="sxs-lookup"><span data-stu-id="1535c-124">myqueue-items</span></span>    | <span data-ttu-id="1535c-125">Nazwa hello kolejki tooconnect tooin Twojego konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="1535c-125">Name of hello queue tooconnect tooin your Storage account.</span></span> |
    | <span data-ttu-id="1535c-126">**Połączenie konta magazynu**</span><span class="sxs-lookup"><span data-stu-id="1535c-126">**Storage account connection**</span></span> | <span data-ttu-id="1535c-127">AzureWebJobStorage</span><span class="sxs-lookup"><span data-stu-id="1535c-127">AzureWebJobStorage</span></span> | <span data-ttu-id="1535c-128">Użyj połączenia konta magazynu hello już używana przez aplikację funkcji lub Utwórz nową.</span><span class="sxs-lookup"><span data-stu-id="1535c-128">You can use hello storage account connection already being used by your function app, or create a new one.</span></span>  |
    | <span data-ttu-id="1535c-129">**Nazwa funkcji**</span><span class="sxs-lookup"><span data-stu-id="1535c-129">**Name your function**</span></span> | <span data-ttu-id="1535c-130">Unikatowa w obrębie aplikacji funkcji</span><span class="sxs-lookup"><span data-stu-id="1535c-130">Unique in your function app</span></span> | <span data-ttu-id="1535c-131">Nazwa funkcji wyzwalanej przez kolejkę.</span><span class="sxs-lookup"><span data-stu-id="1535c-131">Name of this queue triggered function.</span></span> |

3. <span data-ttu-id="1535c-132">Kliknij przycisk **Utwórz** toocreate funkcji.</span><span class="sxs-lookup"><span data-stu-id="1535c-132">Click **Create** toocreate your function.</span></span>

<span data-ttu-id="1535c-133">Następnie połączyć konto magazynu Azure tooyour i utworzyć hello **elementów Moja_kolejka** kolejki magazynu.</span><span class="sxs-lookup"><span data-stu-id="1535c-133">Next, you connect tooyour Azure Storage account and create hello **myqueue-items** storage queue.</span></span>

## <a name="create-hello-queue"></a><span data-ttu-id="1535c-134">Utwórz kolejkę hello</span><span class="sxs-lookup"><span data-stu-id="1535c-134">Create hello queue</span></span>

1. <span data-ttu-id="1535c-135">W funkcji kliknij pozycję **Integracja**, rozwiń pozycję **Dokumentacja** i skopiuj wartości pól **Nazwa konta** oraz **Klucz konta**.</span><span class="sxs-lookup"><span data-stu-id="1535c-135">In your function, click **Integrate**, expand **Documentation**, and copy both **Account name** and **Account key**.</span></span> <span data-ttu-id="1535c-136">Używasz konta magazynu te poświadczenia tooconnect toohello.</span><span class="sxs-lookup"><span data-stu-id="1535c-136">You use these credentials tooconnect toohello storage account.</span></span> <span data-ttu-id="1535c-137">Jeśli nawiązano już połączenie konta magazynu, Pomiń toostep 4.</span><span class="sxs-lookup"><span data-stu-id="1535c-137">If you have already connected your storage account, skip toostep 4.</span></span>

    ![Uzyskaj konto magazynu hello poświadczeń dla połączenia.](./media/functions-create-storage-queue-triggered-function/functions-storage-account-connection.png)<span data-ttu-id="1535c-139">v</span><span class="sxs-lookup"><span data-stu-id="1535c-139">v</span></span>

1. <span data-ttu-id="1535c-140">Uruchom hello [Eksploratora usługi Microsoft Azure Storage](http://storageexplorer.com/) narzędzia, kliknij przycisk hello połączenia powitania po lewej stronie, wybierz **użyć nazwy konta magazynu i klucza**i kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="1535c-140">Run hello [Microsoft Azure Storage Explorer](http://storageexplorer.com/) tool, click hello connect icon on hello left, choose **Use a storage account name and key**, and click **Next**.</span></span>

    ![Uruchom narzędzie Eksploratora usługi Storage konta hello.](./media/functions-create-storage-queue-triggered-function/functions-storage-manager-connect-1.png)

1. <span data-ttu-id="1535c-142">Wprowadź hello **nazwa konta** i **klucz konta** z kroku 1, kliknij przycisk **dalej** , a następnie **Connect**.</span><span class="sxs-lookup"><span data-stu-id="1535c-142">Enter hello **Account name** and **Account key** from step 1, click **Next** and then **Connect**.</span></span>

    ![Wprowadź poświadczenia magazynu hello i połącz.](./media/functions-create-storage-queue-triggered-function/functions-storage-manager-connect-2.png)

1. <span data-ttu-id="1535c-144">Rozwiń hello dołączony konta magazynu, kliknij prawym przyciskiem myszy **kolejek**, kliknij przycisk **Tworzenie kolejki**, typ `myqueue-items`, a następnie naciśnij klawisz enter.</span><span class="sxs-lookup"><span data-stu-id="1535c-144">Expand hello attached storage account, right-click **Queues**, click **Create queue**, type `myqueue-items`, and then press enter.</span></span>

    ![Tworzenie kolejki magazynu.](./media/functions-create-storage-queue-triggered-function/functions-storage-manager-create-queue.png)

<span data-ttu-id="1535c-146">Teraz, gdy masz kolejki magazynu można przetestować funkcji hello przez dodanie toohello kolejki komunikatów.</span><span class="sxs-lookup"><span data-stu-id="1535c-146">Now that you have a storage queue, you can test hello function by adding a message toohello queue.</span></span>

## <a name="test-hello-function"></a><span data-ttu-id="1535c-147">Funkcja hello testu</span><span class="sxs-lookup"><span data-stu-id="1535c-147">Test hello function</span></span>

1. <span data-ttu-id="1535c-148">W portalu Azure hello, funkcja tooyour przeglądania rozwiń hello **dzienniki** u dołu strony hello i upewnij się, że hello przesyłania strumieniowego tego dziennika nie jest wstrzymana.</span><span class="sxs-lookup"><span data-stu-id="1535c-148">Back in hello Azure portal, browse tooyour function expand hello **Logs** at hello bottom of hello page and make sure that log streaming isn't paused.</span></span>

1. <span data-ttu-id="1535c-149">W programie Storage Explorer rozwiń swoje konto magazynu, wybierz kolejno pozycje **Queues** (Kolejki) i **myqueue-items**, a następnie kliknij pozycję **Add message** (Dodaj komunikat).</span><span class="sxs-lookup"><span data-stu-id="1535c-149">In Storage Explorer, expand your storage account, **Queues**, and **myqueue-items**, then click **Add message**.</span></span>

    ![Dodaj toohello kolejki komunikatów.](./media/functions-create-storage-queue-triggered-function/functions-storage-manager-add-message.png)

1. <span data-ttu-id="1535c-151">Wpisz komunikat „Hello World!”</span><span class="sxs-lookup"><span data-stu-id="1535c-151">Type your "Hello World!"</span></span> <span data-ttu-id="1535c-152">w polu **Message text** (Tekst komunikatu) i kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="1535c-152">message in **Message text** and click **OK**.</span></span>

1. <span data-ttu-id="1535c-153">Zaczekaj kilka sekund, a następnie wróć tooyour dzienniki funkcji i sprawdź, czy tej nowej wiadomości powitania został odczytany z kolejki hello.</span><span class="sxs-lookup"><span data-stu-id="1535c-153">Wait for a few seconds, then go back tooyour function logs and verify that hello new message has been read from hello queue.</span></span>

    ![Przeglądanie wiadomości w dziennikach hello.](./media/functions-create-storage-queue-triggered-function/functions-queue-storage-trigger-view-logs.png)

1. <span data-ttu-id="1535c-155">W Eksploratorze magazynu kliknij **Odśwież** i sprawdź, że wiadomość hello został przetworzony i nie jest już w kolejce hello.</span><span class="sxs-lookup"><span data-stu-id="1535c-155">Back in Storage Explorer, click **Refresh** and verify that hello message has been processed and is no longer in hello queue.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="1535c-156">Oczyszczanie zasobów</span><span class="sxs-lookup"><span data-stu-id="1535c-156">Clean up resources</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a><span data-ttu-id="1535c-157">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="1535c-157">Next steps</span></span>

<span data-ttu-id="1535c-158">Utworzono funkcję, która jest uruchamiana, gdy wiadomość zostanie dodany tooa magazynu kolejki.</span><span class="sxs-lookup"><span data-stu-id="1535c-158">You have created a function that runs when a message is added tooa storage queue.</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

<span data-ttu-id="1535c-159">Aby uzyskać więcej informacji na temat wyzwalaczy usługi Queue Storage, zobacz [Powiązania usługi Queue Storage w usłudze Azure Functions](functions-bindings-storage-queue.md).</span><span class="sxs-lookup"><span data-stu-id="1535c-159">For more information about Queue storage triggers, see [Azure Functions Storage queue bindings](functions-bindings-storage-queue.md).</span></span>