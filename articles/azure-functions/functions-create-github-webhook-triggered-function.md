---
title: Tworzenie funkcji na platformie Azure wyzwalanej przez element webhook GitHub | Microsoft Docs
description: "Użyj usługi Azure Functions, aby utworzyć funkcję niewymagającą użycia serwera wywoływaną za pomocą elementu webhook GitHub."
services: functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
ms.assetid: 36ef34b8-3729-4940-86d2-cb8e176fcc06
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/31/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 038bb4cf0a9278416261c05ddaa0ee97d83b63c5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-function-triggered-by-a-github-webhook"></a><span data-ttu-id="37b17-103">Tworzenie funkcji wyzwalanej przez element webhook GitHub</span><span class="sxs-lookup"><span data-stu-id="37b17-103">Create a function triggered by a GitHub webhook</span></span>

<span data-ttu-id="37b17-104">Dowiedz się, jak utworzyć funkcję wyzwalaną przez żądanie elementu webhook protokołu HTTP z ładunkiem specyficznym dla usługi GitHub.</span><span class="sxs-lookup"><span data-stu-id="37b17-104">Learn how to create a function that is triggered by an HTTP webhook request with a GitHub-specific payload.</span></span>

![Funkcja wyzwalana przez element webhook GitHub w witrynie Azure Portal](./media/functions-create-github-webhook-triggered-function/function-app-in-portal-editor.png)

## <a name="prerequisites"></a><span data-ttu-id="37b17-106">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="37b17-106">Prerequisites</span></span>

+ <span data-ttu-id="37b17-107">Konto w usłudze GitHub z przynajmniej jednym projektem.</span><span class="sxs-lookup"><span data-stu-id="37b17-107">A GitHub account with at least one project.</span></span>
+ <span data-ttu-id="37b17-108">Subskrypcja platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="37b17-108">An Azure subscription.</span></span> <span data-ttu-id="37b17-109">Jeśli nie masz subskrypcji, przed rozpoczęciem utwórz [bezpłatne konto](https://azure.microsoft.com/free/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="37b17-109">If you don't have one, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

## <a name="create-an-azure-function-app"></a><span data-ttu-id="37b17-110">Tworzenie aplikacji funkcji platformy Azure</span><span class="sxs-lookup"><span data-stu-id="37b17-110">Create an Azure Function app</span></span>

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

![Pomyślnie utworzona aplikacja funkcji.](./media/functions-create-first-azure-function/function-app-create-success.png)

<span data-ttu-id="37b17-112">Następnie należy utworzyć funkcję w nowej aplikacji funkcji.</span><span class="sxs-lookup"><span data-stu-id="37b17-112">Next, you create a function in the new function app.</span></span>

<a name="create-function"></a>

## <a name="create-a-github-webhook-triggered-function"></a><span data-ttu-id="37b17-113">Tworzenie funkcji wyzwalanej przez element webhook GitHub</span><span class="sxs-lookup"><span data-stu-id="37b17-113">Create a GitHub webhook triggered function</span></span>

1. <span data-ttu-id="37b17-114">Rozwiń aplikację funkcji i kliknij przycisk **+** obok pozycji **Funkcje**.</span><span class="sxs-lookup"><span data-stu-id="37b17-114">Expand your function app and click the **+** button next to **Functions**.</span></span> <span data-ttu-id="37b17-115">Jeśli jest to pierwsza funkcja w aplikacji funkcji, wybierz pozycję **Funkcja niestandardowa**.</span><span class="sxs-lookup"><span data-stu-id="37b17-115">If this is the first function in your function app, select **Custom function**.</span></span> <span data-ttu-id="37b17-116">Spowoduje to wyświetlenie pełnego zestawu szablonów funkcji.</span><span class="sxs-lookup"><span data-stu-id="37b17-116">This displays the complete set of function templates.</span></span>

    ![Strona szybkiego rozpoczynania pracy z usługą Functions w witrynie Azure Portal](./media/functions-create-github-webhook-triggered-function/add-first-function.png)

2. <span data-ttu-id="37b17-118">Wybierz **GitHub WebHook** szablon odpowiedni język.</span><span class="sxs-lookup"><span data-stu-id="37b17-118">Select the **GitHub WebHook** template for your desired language.</span></span> <span data-ttu-id="37b17-119">**Nadaj nazwę funkcji**, a następnie wybierz pozycję **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="37b17-119">**Name your function**, then select **Create**.</span></span>

     ![Tworzenie funkcji wyzwalanej przez element webhook GitHub w witrynie Azure portal](./media/functions-create-github-webhook-triggered-function/functions-create-github-webhook-trigger.png) 

3. <span data-ttu-id="37b17-121">W nowej funkcji kliknij pozycję **</> Pobierz adres URL funkcji**, po czym skopiuj i zapisz wartości.</span><span class="sxs-lookup"><span data-stu-id="37b17-121">In your new function, click **</> Get function URL**, then copy and save the values.</span></span> <span data-ttu-id="37b17-122">Powtórz te czynności po kliknięciu pozycji **</> Pobierz wpis tajny usługi GitHub**.</span><span class="sxs-lookup"><span data-stu-id="37b17-122">Do the same thing for **</> Get GitHub secret**.</span></span> <span data-ttu-id="37b17-123">Wartości te będą potrzebne podczas konfigurowania elementu webhook w usłudze GitHub.</span><span class="sxs-lookup"><span data-stu-id="37b17-123">You use these values to configure the webhook in GitHub.</span></span>

    ![Sprawdzanie kodu funkcji](./media/functions-create-github-webhook-triggered-function/functions-copy-function-url-github-secret.png)

<span data-ttu-id="37b17-125">W następnym kroku zostanie utworzony element webhook w repozytorium GitHub.</span><span class="sxs-lookup"><span data-stu-id="37b17-125">Next, you create a webhook in your GitHub repository.</span></span>

## <a name="configure-the-webhook"></a><span data-ttu-id="37b17-126">Konfigurowanie elementu webhook</span><span class="sxs-lookup"><span data-stu-id="37b17-126">Configure the webhook</span></span>

1. <span data-ttu-id="37b17-127">W usłudze GitHub przejdź do repozytorium, którego jesteś właścicielem.</span><span class="sxs-lookup"><span data-stu-id="37b17-127">In GitHub, navigate to a repository that you own.</span></span> <span data-ttu-id="37b17-128">Możesz też użyć dowolnego rozwidlonego repozytorium.</span><span class="sxs-lookup"><span data-stu-id="37b17-128">You can also use any repository that you have forked.</span></span> <span data-ttu-id="37b17-129">Jeśli konieczne będzie rozwidlenie repozytorium, skorzystaj z informacji pod adresem <https://github.com/Azure-Samples/functions-quickstart>.</span><span class="sxs-lookup"><span data-stu-id="37b17-129">If you need to fork a repository, use <https://github.com/Azure-Samples/functions-quickstart>.</span></span>

1. <span data-ttu-id="37b17-130">Kliknij kolejno pozycje **Ustawienia**, **Elementy webhook** i **Dodaj element webhook**.</span><span class="sxs-lookup"><span data-stu-id="37b17-130">Click **Settings**, then click **Webhooks**, and  **Add webhook**.</span></span>

    ![Dodawanie elementu webhook GitHub](./media/functions-create-github-webhook-triggered-function/functions-create-new-github-webhook-2.png)

1. <span data-ttu-id="37b17-132">Użyj ustawień określonych w tabeli i kliknij pozycję **Dodaj element webhook**.</span><span class="sxs-lookup"><span data-stu-id="37b17-132">Use settings as specified in the table, then click **Add webhook**.</span></span>

    ![Ustawianie adresu URL i wpisu tajnego elementu webhook](./media/functions-create-github-webhook-triggered-function/functions-create-new-github-webhook-3.png)

| <span data-ttu-id="37b17-134">Ustawienie</span><span class="sxs-lookup"><span data-stu-id="37b17-134">Setting</span></span> | <span data-ttu-id="37b17-135">Sugerowana wartość</span><span class="sxs-lookup"><span data-stu-id="37b17-135">Suggested value</span></span> | <span data-ttu-id="37b17-136">Opis</span><span class="sxs-lookup"><span data-stu-id="37b17-136">Description</span></span> |
|---|---|---|
| <span data-ttu-id="37b17-137">**Adres URL ładunku**</span><span class="sxs-lookup"><span data-stu-id="37b17-137">**Payload URL**</span></span> | <span data-ttu-id="37b17-138">Skopiowana wartość</span><span class="sxs-lookup"><span data-stu-id="37b17-138">Copied value</span></span> | <span data-ttu-id="37b17-139">Użyj wartości zwróconej po kliknięciu pozycji **</> Pobierz adres URL funkcji**.</span><span class="sxs-lookup"><span data-stu-id="37b17-139">Use the value returned by  **</> Get function URL**.</span></span> |
| <span data-ttu-id="37b17-140">**Wpis tajny**</span><span class="sxs-lookup"><span data-stu-id="37b17-140">**Secret**</span></span>   | <span data-ttu-id="37b17-141">Skopiowana wartość</span><span class="sxs-lookup"><span data-stu-id="37b17-141">Copied value</span></span> | <span data-ttu-id="37b17-142">Użyj wartości zwróconej po kliknięciu pozycji **</> Pobierz wpis tajny usługi GitHub**.</span><span class="sxs-lookup"><span data-stu-id="37b17-142">Use the value returned by  **</> Get GitHub secret**.</span></span> |
| <span data-ttu-id="37b17-143">**Typ zawartości**</span><span class="sxs-lookup"><span data-stu-id="37b17-143">**Content type**</span></span> | <span data-ttu-id="37b17-144">application/json</span><span class="sxs-lookup"><span data-stu-id="37b17-144">application/json</span></span> | <span data-ttu-id="37b17-145">Funkcja oczekuje ładunku JSON.</span><span class="sxs-lookup"><span data-stu-id="37b17-145">The function expects a JSON payload.</span></span> |
| <span data-ttu-id="37b17-146">Wyzwalacze zdarzeń</span><span class="sxs-lookup"><span data-stu-id="37b17-146">Event triggers</span></span> | <span data-ttu-id="37b17-147">Pozwól mi wybrać pojedyncze zdarzenia</span><span class="sxs-lookup"><span data-stu-id="37b17-147">Let me select individual events</span></span> | <span data-ttu-id="37b17-148">Wyzwalacz ma być uruchamiany tylko w przypadku zdarzeń z komentarzami dotyczącymi problemów.</span><span class="sxs-lookup"><span data-stu-id="37b17-148">We only want to trigger on issue comment events.</span></span>  |
| | <span data-ttu-id="37b17-149">Komentarz dotyczący problemu</span><span class="sxs-lookup"><span data-stu-id="37b17-149">Issue comment</span></span> |  |

<span data-ttu-id="37b17-150">Element webhook został skonfigurowany do wyzwolenia funkcji po dodaniu nowego komentarza dotyczącego problemu.</span><span class="sxs-lookup"><span data-stu-id="37b17-150">Now, the webhook is configured to trigger your function when a new issue comment is added.</span></span>

## <a name="test-the-function"></a><span data-ttu-id="37b17-151">Testowanie funkcji</span><span class="sxs-lookup"><span data-stu-id="37b17-151">Test the function</span></span>

1. <span data-ttu-id="37b17-152">W swoim repozytorium GitHub otwórz kartę **Problemy** w nowym oknie przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="37b17-152">In your GitHub repository, open the **Issues** tab in a new browser window.</span></span>

1. <span data-ttu-id="37b17-153">W nowym oknie kliknij pozycję **Nowy problem**, wpisz tytuł, a następnie kliknij pozycję **Prześlij nowy problem**.</span><span class="sxs-lookup"><span data-stu-id="37b17-153">In the new window, click **New Issue**, type a title, and then click **Submit new issue**.</span></span>

1. <span data-ttu-id="37b17-154">W obszarze problemu wpisz komentarz i kliknij pozycję **Komentarz**.</span><span class="sxs-lookup"><span data-stu-id="37b17-154">In the issue, type a comment and click **Comment**.</span></span>

    ![Dodawanie komentarza dotyczącego problemu w usłudze GitHub.](./media/functions-create-github-webhook-triggered-function/functions-github-webhook-add-comment.png)

1. <span data-ttu-id="37b17-156">Wróć do portalu i wyświetl dzienniki.</span><span class="sxs-lookup"><span data-stu-id="37b17-156">Go back to the portal and view the logs.</span></span> <span data-ttu-id="37b17-157">Powinien zostać wyświetlony wpis śledzenia z nowym tekstem komentarza.</span><span class="sxs-lookup"><span data-stu-id="37b17-157">You should see a trace entry with the new comment text.</span></span>

     ![Wyświetlanie tekstu komentarza w dziennikach.](./media/functions-create-github-webhook-triggered-function/function-app-view-logs.png)

## <a name="clean-up-resources"></a><span data-ttu-id="37b17-159">Oczyszczanie zasobów</span><span class="sxs-lookup"><span data-stu-id="37b17-159">Clean up resources</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a><span data-ttu-id="37b17-160">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="37b17-160">Next steps</span></span>

<span data-ttu-id="37b17-161">Utworzono funkcję, która jest uruchamiana w momencie otrzymania żądania od elementu webhook GitHub.</span><span class="sxs-lookup"><span data-stu-id="37b17-161">You have created a function that runs when a request is received from a GitHub webhook.</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

<span data-ttu-id="37b17-162">Aby uzyskać więcej informacji na temat wyzwalaczy elementów webhook, zobacz temat [Powiązania protokołu HTTP i elementów webhook w usłudze Azure Functions](functions-bindings-http-webhook.md).</span><span class="sxs-lookup"><span data-stu-id="37b17-162">For more information about webhook triggers, see [Azure Functions HTTP and webhook bindings](functions-bindings-http-webhook.md).</span></span>
