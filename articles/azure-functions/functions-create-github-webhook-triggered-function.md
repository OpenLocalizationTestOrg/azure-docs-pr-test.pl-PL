---
title: Funkcja w systemie Azure wyzwalane przez GitHub webhook aaaCreate | Dokumentacja firmy Microsoft
description: "Za pomocą usługi Azure Functions toocreate niekorzystającą funkcji, który jest wywoływany przez element webhook GitHub."
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
ms.openlocfilehash: 8ffcde82c9310d749159ed53eab113658e38a030
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-function-triggered-by-a-github-webhook"></a><span data-ttu-id="fd498-103">Tworzenie funkcji wyzwalanej przez element webhook GitHub</span><span class="sxs-lookup"><span data-stu-id="fd498-103">Create a function triggered by a GitHub webhook</span></span>

<span data-ttu-id="fd498-104">Dowiedz się, jak toocreate funkcję, która jest wyzwalana przez żądanie HTTP elementu webhook z ładunku specyficzne dla usługi GitHub.</span><span class="sxs-lookup"><span data-stu-id="fd498-104">Learn how toocreate a function that is triggered by an HTTP webhook request with a GitHub-specific payload.</span></span>

![Funkcja w portalu Azure hello wyzwolone element Github Webhook](./media/functions-create-github-webhook-triggered-function/function-app-in-portal-editor.png)

## <a name="prerequisites"></a><span data-ttu-id="fd498-106">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="fd498-106">Prerequisites</span></span>

+ <span data-ttu-id="fd498-107">Konto w usłudze GitHub z przynajmniej jednym projektem.</span><span class="sxs-lookup"><span data-stu-id="fd498-107">A GitHub account with at least one project.</span></span>
+ <span data-ttu-id="fd498-108">Subskrypcja platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="fd498-108">An Azure subscription.</span></span> <span data-ttu-id="fd498-109">Jeśli nie masz subskrypcji, przed rozpoczęciem utwórz [bezpłatne konto](https://azure.microsoft.com/free/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="fd498-109">If you don't have one, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

## <a name="create-an-azure-function-app"></a><span data-ttu-id="fd498-110">Tworzenie aplikacji funkcji platformy Azure</span><span class="sxs-lookup"><span data-stu-id="fd498-110">Create an Azure Function app</span></span>

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

![Pomyślnie utworzona aplikacja funkcji.](./media/functions-create-first-azure-function/function-app-create-success.png)

<span data-ttu-id="fd498-112">Następnie należy utworzyć funkcji w hello nowej funkcji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="fd498-112">Next, you create a function in hello new function app.</span></span>

<a name="create-function"></a>

## <a name="create-a-github-webhook-triggered-function"></a><span data-ttu-id="fd498-113">Tworzenie funkcji wyzwalanej przez element webhook GitHub</span><span class="sxs-lookup"><span data-stu-id="fd498-113">Create a GitHub webhook triggered function</span></span>

1. <span data-ttu-id="fd498-114">Rozwiń węzeł funkcji aplikacji, a następnie kliknij przycisk hello  **+**  obok przycisku zbyt**funkcji**.</span><span class="sxs-lookup"><span data-stu-id="fd498-114">Expand your function app and click hello **+** button next too**Functions**.</span></span> <span data-ttu-id="fd498-115">Jeśli hello pierwszej funkcji w funkcji aplikacji, wybierz **Niestandardowa funkcja**.</span><span class="sxs-lookup"><span data-stu-id="fd498-115">If this is hello first function in your function app, select **Custom function**.</span></span> <span data-ttu-id="fd498-116">Spowoduje to wyświetlenie hello pełny zestaw szablonów funkcji.</span><span class="sxs-lookup"><span data-stu-id="fd498-116">This displays hello complete set of function templates.</span></span>

    ![Funkcje strony szybkiego startu w hello portalu Azure](./media/functions-create-github-webhook-triggered-function/add-first-function.png)

2. <span data-ttu-id="fd498-118">Wybierz hello **GitHub WebHook** szablon odpowiedni język.</span><span class="sxs-lookup"><span data-stu-id="fd498-118">Select hello **GitHub WebHook** template for your desired language.</span></span> <span data-ttu-id="fd498-119">**Nadaj nazwę funkcji**, a następnie wybierz pozycję **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="fd498-119">**Name your function**, then select **Create**.</span></span>

     ![Utwórz funkcję wyzwolone element webhook GitHub w hello portalu Azure](./media/functions-create-github-webhook-triggered-function/functions-create-github-webhook-trigger.png) 

3. <span data-ttu-id="fd498-121">W nowych funkcji, kliknij przycisk **adres URL funkcji <> / Get**, następnie skopiuj i Zapisz hello wartości.</span><span class="sxs-lookup"><span data-stu-id="fd498-121">In your new function, click **</> Get function URL**, then copy and save hello values.</span></span> <span data-ttu-id="fd498-122">Witaj samo dla **<> / GitHub pobrać klucza tajnego**.</span><span class="sxs-lookup"><span data-stu-id="fd498-122">Do hello same thing for **</> Get GitHub secret**.</span></span> <span data-ttu-id="fd498-123">Użyjesz tych wartości tooconfigure hello elementu webhook w witrynie GitHub.</span><span class="sxs-lookup"><span data-stu-id="fd498-123">You use these values tooconfigure hello webhook in GitHub.</span></span>

    ![Przegląd kodu funkcji hello](./media/functions-create-github-webhook-triggered-function/functions-copy-function-url-github-secret.png)

<span data-ttu-id="fd498-125">W następnym kroku zostanie utworzony element webhook w repozytorium GitHub.</span><span class="sxs-lookup"><span data-stu-id="fd498-125">Next, you create a webhook in your GitHub repository.</span></span>

## <a name="configure-hello-webhook"></a><span data-ttu-id="fd498-126">Skonfiguruj hello elementu webhook</span><span class="sxs-lookup"><span data-stu-id="fd498-126">Configure hello webhook</span></span>

1. <span data-ttu-id="fd498-127">W witrynie GitHub Przejdź repozytorium tooa, którego jesteś właścicielem.</span><span class="sxs-lookup"><span data-stu-id="fd498-127">In GitHub, navigate tooa repository that you own.</span></span> <span data-ttu-id="fd498-128">Możesz też użyć dowolnego rozwidlonego repozytorium.</span><span class="sxs-lookup"><span data-stu-id="fd498-128">You can also use any repository that you have forked.</span></span> <span data-ttu-id="fd498-129">Jeśli potrzebujesz toofork repozytorium, użyj <https://github.com/Azure-Samples/functions-quickstart>.</span><span class="sxs-lookup"><span data-stu-id="fd498-129">If you need toofork a repository, use <https://github.com/Azure-Samples/functions-quickstart>.</span></span>

1. <span data-ttu-id="fd498-130">Kliknij kolejno pozycje **Ustawienia**, **Elementy webhook** i **Dodaj element webhook**.</span><span class="sxs-lookup"><span data-stu-id="fd498-130">Click **Settings**, then click **Webhooks**, and  **Add webhook**.</span></span>

    ![Dodawanie elementu webhook GitHub](./media/functions-create-github-webhook-triggered-function/functions-create-new-github-webhook-2.png)

1. <span data-ttu-id="fd498-132">Użyj ustawień określonych w tabeli hello, a następnie kliknij przycisk **Dodawanie elementu webhook**.</span><span class="sxs-lookup"><span data-stu-id="fd498-132">Use settings as specified in hello table, then click **Add webhook**.</span></span>

    ![Adres URL elementu webhook hello zestawu i klucz tajny](./media/functions-create-github-webhook-triggered-function/functions-create-new-github-webhook-3.png)

| <span data-ttu-id="fd498-134">Ustawienie</span><span class="sxs-lookup"><span data-stu-id="fd498-134">Setting</span></span> | <span data-ttu-id="fd498-135">Sugerowana wartość</span><span class="sxs-lookup"><span data-stu-id="fd498-135">Suggested value</span></span> | <span data-ttu-id="fd498-136">Opis</span><span class="sxs-lookup"><span data-stu-id="fd498-136">Description</span></span> |
|---|---|---|
| <span data-ttu-id="fd498-137">**Adres URL ładunku**</span><span class="sxs-lookup"><span data-stu-id="fd498-137">**Payload URL**</span></span> | <span data-ttu-id="fd498-138">Skopiowana wartość</span><span class="sxs-lookup"><span data-stu-id="fd498-138">Copied value</span></span> | <span data-ttu-id="fd498-139">Użyj hello wartość zwrócona przez **adres URL funkcji <> / Get**.</span><span class="sxs-lookup"><span data-stu-id="fd498-139">Use hello value returned by  **</> Get function URL**.</span></span> |
| <span data-ttu-id="fd498-140">**Wpis tajny**</span><span class="sxs-lookup"><span data-stu-id="fd498-140">**Secret**</span></span>   | <span data-ttu-id="fd498-141">Skopiowana wartość</span><span class="sxs-lookup"><span data-stu-id="fd498-141">Copied value</span></span> | <span data-ttu-id="fd498-142">Użyj hello wartość zwrócona przez **<> / GitHub pobrać klucza tajnego**.</span><span class="sxs-lookup"><span data-stu-id="fd498-142">Use hello value returned by  **</> Get GitHub secret**.</span></span> |
| <span data-ttu-id="fd498-143">**Typ zawartości**</span><span class="sxs-lookup"><span data-stu-id="fd498-143">**Content type**</span></span> | <span data-ttu-id="fd498-144">application/json</span><span class="sxs-lookup"><span data-stu-id="fd498-144">application/json</span></span> | <span data-ttu-id="fd498-145">Funkcja Hello oczekuje ładunek JSON.</span><span class="sxs-lookup"><span data-stu-id="fd498-145">hello function expects a JSON payload.</span></span> |
| <span data-ttu-id="fd498-146">Wyzwalacze zdarzeń</span><span class="sxs-lookup"><span data-stu-id="fd498-146">Event triggers</span></span> | <span data-ttu-id="fd498-147">Pozwól mi wybrać pojedyncze zdarzenia</span><span class="sxs-lookup"><span data-stu-id="fd498-147">Let me select individual events</span></span> | <span data-ttu-id="fd498-148">Chcemy tylko tootrigger problem komentarz zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="fd498-148">We only want tootrigger on issue comment events.</span></span>  |
| | <span data-ttu-id="fd498-149">Komentarz dotyczący problemu</span><span class="sxs-lookup"><span data-stu-id="fd498-149">Issue comment</span></span> |  |

<span data-ttu-id="fd498-150">Teraz, hello elementu webhook jest skonfigurowany tootrigger funkcji w przypadku dodania nowego komentarza problem.</span><span class="sxs-lookup"><span data-stu-id="fd498-150">Now, hello webhook is configured tootrigger your function when a new issue comment is added.</span></span>

## <a name="test-hello-function"></a><span data-ttu-id="fd498-151">Funkcja hello testu</span><span class="sxs-lookup"><span data-stu-id="fd498-151">Test hello function</span></span>

1. <span data-ttu-id="fd498-152">W repozytorium GitHub Otwórz hello **problemów** kartę w nowym oknie przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="fd498-152">In your GitHub repository, open hello **Issues** tab in a new browser window.</span></span>

1. <span data-ttu-id="fd498-153">W nowym oknie powitania kliknij **nowy problem**wpisz tytuł, a następnie kliknij przycisk **przesłać nowy problem**.</span><span class="sxs-lookup"><span data-stu-id="fd498-153">In hello new window, click **New Issue**, type a title, and then click **Submit new issue**.</span></span>

1. <span data-ttu-id="fd498-154">W hello problem, wprowadź komentarz, a następnie kliknij przycisk **komentarz**.</span><span class="sxs-lookup"><span data-stu-id="fd498-154">In hello issue, type a comment and click **Comment**.</span></span>

    ![Dodawanie komentarza dotyczącego problemu w usłudze GitHub.](./media/functions-create-github-webhook-triggered-function/functions-github-webhook-add-comment.png)

1. <span data-ttu-id="fd498-156">Toohello portal wrócić do poprzedniej strony i sprawdź dzienniki hello.</span><span class="sxs-lookup"><span data-stu-id="fd498-156">Go back toohello portal and view hello logs.</span></span> <span data-ttu-id="fd498-157">Wpis śledzenia na nowy tekst komentarza hello powinna zostać wyświetlona.</span><span class="sxs-lookup"><span data-stu-id="fd498-157">You should see a trace entry with hello new comment text.</span></span>

     ![Wyświetl tekst komentarza hello w dziennikach hello.](./media/functions-create-github-webhook-triggered-function/function-app-view-logs.png)

## <a name="clean-up-resources"></a><span data-ttu-id="fd498-159">Oczyszczanie zasobów</span><span class="sxs-lookup"><span data-stu-id="fd498-159">Clean up resources</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a><span data-ttu-id="fd498-160">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="fd498-160">Next steps</span></span>

<span data-ttu-id="fd498-161">Utworzono funkcję, która jest uruchamiana w momencie otrzymania żądania od elementu webhook GitHub.</span><span class="sxs-lookup"><span data-stu-id="fd498-161">You have created a function that runs when a request is received from a GitHub webhook.</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

<span data-ttu-id="fd498-162">Aby uzyskać więcej informacji na temat wyzwalaczy elementów webhook, zobacz temat [Powiązania protokołu HTTP i elementów webhook w usłudze Azure Functions](functions-bindings-http-webhook.md).</span><span class="sxs-lookup"><span data-stu-id="fd498-162">For more information about webhook triggers, see [Azure Functions HTTP and webhook bindings](functions-bindings-http-webhook.md).</span></span>
