---
title: Tworzenie funkcji na platformie Azure wyzwalanej przez komunikaty kolejki | Microsoft Docs
description: "Utwórz za pomocą usługi Azure Functions funkcję niewymagającą użycia serwera wywoływaną za pomocą komunikatów przesyłanych do kolejki usługi Azure Storage."
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
ms.openlocfilehash: 92a03154bf5a8945e2de9606afd138803c76fafe
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-function-triggered-by-azure-queue-storage"></a><span data-ttu-id="3fd05-103">Tworzenie funkcji wyzwalanej przez usługę Azure Queue Storage</span><span class="sxs-lookup"><span data-stu-id="3fd05-103">Create a function triggered by Azure Queue storage</span></span>

<span data-ttu-id="3fd05-104">Dowiedz się, jak utworzyć funkcję wyzwalaną w momencie przesłania komunikatów do kolejki usługi Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="3fd05-104">Learn how to create a function triggered when messages are submitted to an Azure Storage queue.</span></span>

![Wyświetlanie komunikatu w dziennikach.](./media/functions-create-storage-queue-triggered-function/function-app-in-portal-editor.png)

## <a name="prerequisites"></a><span data-ttu-id="3fd05-106">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="3fd05-106">Prerequisites</span></span>

- <span data-ttu-id="3fd05-107">Pobrać i zainstalować program [Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="3fd05-107">Download and install the [Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span></span>

- <span data-ttu-id="3fd05-108">Subskrypcja platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="3fd05-108">An Azure subscription.</span></span> <span data-ttu-id="3fd05-109">Jeśli nie masz subskrypcji, przed rozpoczęciem utwórz [bezpłatne konto](https://azure.microsoft.com/free/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="3fd05-109">If you don't have one, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

## <a name="create-an-azure-function-app"></a><span data-ttu-id="3fd05-110">Tworzenie aplikacji funkcji platformy Azure</span><span class="sxs-lookup"><span data-stu-id="3fd05-110">Create an Azure Function app</span></span>

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

![Pomyślnie utworzona aplikacja funkcji.](./media/functions-create-first-azure-function/function-app-create-success.png)

<span data-ttu-id="3fd05-112">Następnie należy utworzyć funkcję w nowej aplikacji funkcji.</span><span class="sxs-lookup"><span data-stu-id="3fd05-112">Next, you create a function in the new function app.</span></span>

<a name="create-function"></a>

## <a name="create-a-queue-triggered-function"></a><span data-ttu-id="3fd05-113">Tworzenie funkcji wyzwalanej przez kolejkę</span><span class="sxs-lookup"><span data-stu-id="3fd05-113">Create a Queue triggered function</span></span>

1. <span data-ttu-id="3fd05-114">Rozwiń aplikację funkcji i kliknij przycisk **+** obok pozycji **Funkcje**.</span><span class="sxs-lookup"><span data-stu-id="3fd05-114">Expand your function app and click the **+** button next to **Functions**.</span></span> <span data-ttu-id="3fd05-115">Jeśli jest to pierwsza funkcja w aplikacji funkcji, wybierz pozycję **Funkcja niestandardowa**.</span><span class="sxs-lookup"><span data-stu-id="3fd05-115">If this is the first function in your function app, select **Custom function**.</span></span> <span data-ttu-id="3fd05-116">Spowoduje to wyświetlenie pełnego zestawu szablonów funkcji.</span><span class="sxs-lookup"><span data-stu-id="3fd05-116">This displays the complete set of function templates.</span></span>

    ![Strona szybkiego rozpoczynania pracy z usługą Functions w witrynie Azure Portal](./media/functions-create-storage-queue-triggered-function/add-first-function.png)

2. <span data-ttu-id="3fd05-118">Wybierz szablon **QueueTrigger** dla żądanego języka i użyj ustawień określonych w tabeli.</span><span class="sxs-lookup"><span data-stu-id="3fd05-118">Select the **QueueTrigger** template for your desired language, and  use the settings as specified in the table.</span></span>

    ![Tworzenie funkcji wyzwalanej przez kolejkę magazynu.](./media/functions-create-storage-queue-triggered-function/functions-create-queue-storage-trigger-portal.png)
    
    | <span data-ttu-id="3fd05-120">Ustawienie</span><span class="sxs-lookup"><span data-stu-id="3fd05-120">Setting</span></span> | <span data-ttu-id="3fd05-121">Sugerowana wartość</span><span class="sxs-lookup"><span data-stu-id="3fd05-121">Suggested value</span></span> | <span data-ttu-id="3fd05-122">Opis</span><span class="sxs-lookup"><span data-stu-id="3fd05-122">Description</span></span> |
    |---|---|---|
    | <span data-ttu-id="3fd05-123">**Nazwa kolejki**</span><span class="sxs-lookup"><span data-stu-id="3fd05-123">**Queue name**</span></span>   | <span data-ttu-id="3fd05-124">myqueue-items</span><span class="sxs-lookup"><span data-stu-id="3fd05-124">myqueue-items</span></span>    | <span data-ttu-id="3fd05-125">Nazwa kolejki, z którą zostanie nawiązane połączenie na koncie magazynu.</span><span class="sxs-lookup"><span data-stu-id="3fd05-125">Name of the queue to connect to in your Storage account.</span></span> |
    | <span data-ttu-id="3fd05-126">**Połączenie konta magazynu**</span><span class="sxs-lookup"><span data-stu-id="3fd05-126">**Storage account connection**</span></span> | <span data-ttu-id="3fd05-127">AzureWebJobStorage</span><span class="sxs-lookup"><span data-stu-id="3fd05-127">AzureWebJobStorage</span></span> | <span data-ttu-id="3fd05-128">Możesz skorzystać z połączenia konta magazynu już używanego przez aplikację funkcji lub utworzyć nowe.</span><span class="sxs-lookup"><span data-stu-id="3fd05-128">You can use the storage account connection already being used by your function app, or create a new one.</span></span>  |
    | <span data-ttu-id="3fd05-129">**Nazwa funkcji**</span><span class="sxs-lookup"><span data-stu-id="3fd05-129">**Name your function**</span></span> | <span data-ttu-id="3fd05-130">Unikatowa w obrębie aplikacji funkcji</span><span class="sxs-lookup"><span data-stu-id="3fd05-130">Unique in your function app</span></span> | <span data-ttu-id="3fd05-131">Nazwa funkcji wyzwalanej przez kolejkę.</span><span class="sxs-lookup"><span data-stu-id="3fd05-131">Name of this queue triggered function.</span></span> |

3. <span data-ttu-id="3fd05-132">Kliknij przycisk **Utwórz**, aby utworzyć funkcję.</span><span class="sxs-lookup"><span data-stu-id="3fd05-132">Click **Create** to create your function.</span></span>

<span data-ttu-id="3fd05-133">Następnie nawiąż połączenie z kontem usługi Azure Storage i utwórz kolejkę magazynu **myqueue-items**.</span><span class="sxs-lookup"><span data-stu-id="3fd05-133">Next, you connect to your Azure Storage account and create the **myqueue-items** storage queue.</span></span>

## <a name="create-the-queue"></a><span data-ttu-id="3fd05-134">Tworzenie kolejki</span><span class="sxs-lookup"><span data-stu-id="3fd05-134">Create the queue</span></span>

1. <span data-ttu-id="3fd05-135">W funkcji kliknij pozycję **Integracja**, rozwiń pozycję **Dokumentacja** i skopiuj wartości pól **Nazwa konta** oraz **Klucz konta**.</span><span class="sxs-lookup"><span data-stu-id="3fd05-135">In your function, click **Integrate**, expand **Documentation**, and copy both **Account name** and **Account key**.</span></span> <span data-ttu-id="3fd05-136">Te poświadczenia służą do nawiązywania połączenia z kontem magazynu.</span><span class="sxs-lookup"><span data-stu-id="3fd05-136">You use these credentials to connect to the storage account.</span></span> <span data-ttu-id="3fd05-137">Jeśli już nawiązano połączenie z kontem magazynu, przejdź do kroku 4.</span><span class="sxs-lookup"><span data-stu-id="3fd05-137">If you have already connected your storage account, skip to step 4.</span></span>

    ![Uzyskiwanie poświadczeń połączenia konta magazynu.](./media/functions-create-storage-queue-triggered-function/functions-storage-account-connection.png)<span data-ttu-id="3fd05-139">v</span><span class="sxs-lookup"><span data-stu-id="3fd05-139">v</span></span>

1. <span data-ttu-id="3fd05-140">Uruchom narzędzie [Microsoft Azure Storage Explorer](http://storageexplorer.com/), kliknij ikonę połączenia po lewej stronie, wybierz pozycję **Użyj klucza i nazwy konta magazynu** i kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="3fd05-140">Run the [Microsoft Azure Storage Explorer](http://storageexplorer.com/) tool, click the connect icon on the left, choose **Use a storage account name and key**, and click **Next**.</span></span>

    ![Uruchamianie narzędzia Storage Account Explorer.](./media/functions-create-storage-queue-triggered-function/functions-storage-manager-connect-1.png)

1. <span data-ttu-id="3fd05-142">Wprowadź wartości **Nazwa konta** i **Klucz konta** z kroku 1, kliknij przycisk **Dalej**, a następnie przycisk **Połącz**.</span><span class="sxs-lookup"><span data-stu-id="3fd05-142">Enter the **Account name** and **Account key** from step 1, click **Next** and then **Connect**.</span></span>

    ![Wprowadzanie poświadczeń magazynu i nawiązywanie połączenia.](./media/functions-create-storage-queue-triggered-function/functions-storage-manager-connect-2.png)

1. <span data-ttu-id="3fd05-144">Rozwiń dołączone konto magazynu, kliknij prawym przyciskiem myszy pozycję **Queues** (Kolejki), kliknij polecenie **Create queue** (Utwórz kolejkę), wpisz nazwę `myqueue-items`, a następnie naciśnij klawisz Enter.</span><span class="sxs-lookup"><span data-stu-id="3fd05-144">Expand the attached storage account, right-click **Queues**, click **Create queue**, type `myqueue-items`, and then press enter.</span></span>

    ![Tworzenie kolejki magazynu.](./media/functions-create-storage-queue-triggered-function/functions-storage-manager-create-queue.png)

<span data-ttu-id="3fd05-146">Teraz, gdy masz już kolejkę magazynu, możesz przetestować funkcję, dodając komunikat do kolejki.</span><span class="sxs-lookup"><span data-stu-id="3fd05-146">Now that you have a storage queue, you can test the function by adding a message to the queue.</span></span>

## <a name="test-the-function"></a><span data-ttu-id="3fd05-147">Testowanie funkcji</span><span class="sxs-lookup"><span data-stu-id="3fd05-147">Test the function</span></span>

1. <span data-ttu-id="3fd05-148">Wróć do witryny Azure Portal, przejdź do swoich funkcji, rozwiń pozycję **Dzienniki** w dolnej części strony i upewnij się, że strumieniowe przesyłanie dzienników nie jest wstrzymane.</span><span class="sxs-lookup"><span data-stu-id="3fd05-148">Back in the Azure portal, browse to your function expand the **Logs** at the bottom of the page and make sure that log streaming isn't paused.</span></span>

1. <span data-ttu-id="3fd05-149">W programie Storage Explorer rozwiń swoje konto magazynu, wybierz kolejno pozycje **Queues** (Kolejki) i **myqueue-items**, a następnie kliknij pozycję **Add message** (Dodaj komunikat).</span><span class="sxs-lookup"><span data-stu-id="3fd05-149">In Storage Explorer, expand your storage account, **Queues**, and **myqueue-items**, then click **Add message**.</span></span>

    ![Dodawanie komunikatu do kolejki.](./media/functions-create-storage-queue-triggered-function/functions-storage-manager-add-message.png)

1. <span data-ttu-id="3fd05-151">Wpisz komunikat „Hello World!”</span><span class="sxs-lookup"><span data-stu-id="3fd05-151">Type your "Hello World!"</span></span> <span data-ttu-id="3fd05-152">w polu **Message text** (Tekst komunikatu) i kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="3fd05-152">message in **Message text** and click **OK**.</span></span>

1. <span data-ttu-id="3fd05-153">Poczekaj kilka sekund, a następnie wróć do dzienników funkcji i sprawdź, czy nowy komunikat został odczytany z kolejki.</span><span class="sxs-lookup"><span data-stu-id="3fd05-153">Wait for a few seconds, then go back to your function logs and verify that the new message has been read from the queue.</span></span>

    ![Wyświetlanie komunikatu w dziennikach.](./media/functions-create-storage-queue-triggered-function/functions-queue-storage-trigger-view-logs.png)

1. <span data-ttu-id="3fd05-155">Wróć do programu Storage Explorer, kliknij pozycję **Refresh** (Odśwież) i sprawdź, czy komunikat został przetworzony i nie ma go już w kolejce.</span><span class="sxs-lookup"><span data-stu-id="3fd05-155">Back in Storage Explorer, click **Refresh** and verify that the message has been processed and is no longer in the queue.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="3fd05-156">Oczyszczanie zasobów</span><span class="sxs-lookup"><span data-stu-id="3fd05-156">Clean up resources</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a><span data-ttu-id="3fd05-157">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="3fd05-157">Next steps</span></span>

<span data-ttu-id="3fd05-158">Utworzono funkcję, która jest uruchamiana w momencie dodania komunikatu do kolejki magazynu.</span><span class="sxs-lookup"><span data-stu-id="3fd05-158">You have created a function that runs when a message is added to a storage queue.</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

<span data-ttu-id="3fd05-159">Aby uzyskać więcej informacji na temat wyzwalaczy usługi Queue Storage, zobacz [Powiązania usługi Queue Storage w usłudze Azure Functions](functions-bindings-storage-queue.md).</span><span class="sxs-lookup"><span data-stu-id="3fd05-159">For more information about Queue storage triggers, see [Azure Functions Storage queue bindings](functions-bindings-storage-queue.md).</span></span>