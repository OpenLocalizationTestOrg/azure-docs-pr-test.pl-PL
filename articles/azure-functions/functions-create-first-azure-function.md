---
title: Tworzenie pierwszej funkcji z poziomu witryny Azure Portal | Microsoft Docs
description: "Dowiedz się, jak utworzyć pierwszą funkcję platformy Azure do wykonywania bezserwerowego przy użyciu witryny Azure Portal."
services: functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
ms.assetid: 96cf87b9-8db6-41a8-863a-abb828e3d06d
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 08/07/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 3ec1f278f21d89782137625aff200f07f15fd9fb
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="create-your-first-function-in-the-azure-portal"></a><span data-ttu-id="e51d6-103">Tworzenie pierwszej funkcji w witrynie Azure Portal</span><span class="sxs-lookup"><span data-stu-id="e51d6-103">Create your first function in the Azure portal</span></span>

<span data-ttu-id="e51d6-104">Usługa Azure Functions umożliwia wykonywanie kodu w środowisku bezserwerowym bez konieczności uprzedniego tworzenia maszyny wirtualnej lub publikowania aplikacji sieci Web.</span><span class="sxs-lookup"><span data-stu-id="e51d6-104">Azure Functions lets you execute your code in a serverless environment without having to first create a VM or publish a web application.</span></span> <span data-ttu-id="e51d6-105">W tym temacie opisano tworzenie funkcji „hello world” w witrynie Azure Portal przy użyciu usługi Functions.</span><span class="sxs-lookup"><span data-stu-id="e51d6-105">In this topic, learn how to use Functions to create a "hello world" function in the Azure portal.</span></span>

![Tworzenie aplikacji funkcji w witrynie Azure Portal](./media/functions-create-first-azure-function/function-app-in-portal-editor.png)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="log-in-to-azure"></a><span data-ttu-id="e51d6-107">Zaloguj się do platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="e51d6-107">Log in to Azure</span></span>

<span data-ttu-id="e51d6-108">Zaloguj się do witryny [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="e51d6-108">Log in to the [Azure portal](https://portal.azure.com/).</span></span>

## <a name="create-a-function-app"></a><span data-ttu-id="e51d6-109">Tworzenie aplikacji funkcji</span><span class="sxs-lookup"><span data-stu-id="e51d6-109">Create a function app</span></span>

<span data-ttu-id="e51d6-110">Do obsługi wykonywania funkcji potrzebna jest aplikacja funkcji.</span><span class="sxs-lookup"><span data-stu-id="e51d6-110">You must have a function app to host the execution of your functions.</span></span> <span data-ttu-id="e51d6-111">Aplikacja funkcji umożliwia grupowanie funkcji jako jednostki logicznej, co ułatwia wdrażanie i udostępnianie zasobów oraz zarządzanie nimi.</span><span class="sxs-lookup"><span data-stu-id="e51d6-111">A function app lets you group functions as a logic unit for easier management, deployment, and sharing of resources.</span></span> 

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

<span data-ttu-id="e51d6-112">Następnie należy utworzyć funkcję w nowej aplikacji funkcji.</span><span class="sxs-lookup"><span data-stu-id="e51d6-112">Next, you create a function in the new function app.</span></span>

## <span data-ttu-id="e51d6-113"><a name="create-function"></a>Tworzenie funkcji wyzwalanej przez protokół HTTP</span><span class="sxs-lookup"><span data-stu-id="e51d6-113"><a name="create-function"></a>Create an HTTP triggered function</span></span>

1. <span data-ttu-id="e51d6-114">Rozwiń nową aplikację funkcji, a następnie kliknij przycisk **+** obok pozycji **Funkcje**.</span><span class="sxs-lookup"><span data-stu-id="e51d6-114">Expand your new function app, then click the **+** button next to **Functions**.</span></span>

2.  <span data-ttu-id="e51d6-115">Na stronie **Szybkie rozpoczynanie pracy** wybierz pozycję **Element webhook i interfejs API**, **wybierz język** funkcji i kliknij pozycję **Utwórz tę funkcję**.</span><span class="sxs-lookup"><span data-stu-id="e51d6-115">In the **Get started quickly** page, select **WebHook + API**, **Choose a language** for your function, and click **Create this function**.</span></span> 
   
    ![Szybkie rozpoczynanie pracy z usługą Functions w witrynie Azure Portal.](./media/functions-create-first-azure-function/function-app-quickstart-node-webhook.png)

<span data-ttu-id="e51d6-117">Funkcja zostanie utworzona w wybranym języku i przy użyciu szablonu funkcji wyzwalanej przez protokół HTTP.</span><span class="sxs-lookup"><span data-stu-id="e51d6-117">A function is created in your chosen language using the template for an HTTP triggered function.</span></span> <span data-ttu-id="e51d6-118">Możesz uruchomić nową funkcję, wysyłając żądanie HTTP.</span><span class="sxs-lookup"><span data-stu-id="e51d6-118">You can run the new function by sending an HTTP request.</span></span>

## <a name="test-the-function"></a><span data-ttu-id="e51d6-119">Testowanie funkcji</span><span class="sxs-lookup"><span data-stu-id="e51d6-119">Test the function</span></span>

1. <span data-ttu-id="e51d6-120">W nowej funkcji kliknij przycisk **</> Pobierz adres URL funkcji**, wybierz pozycję **domyślne (klawisz funkcji)**, a następnie kliknij przycisk **Kopiuj**.</span><span class="sxs-lookup"><span data-stu-id="e51d6-120">In your new function, click **</> Get function URL**, select **default (Function key)**, and then click **Copy**.</span></span> 

    ![Kopiowanie adresu URL funkcji z witryny Azure Portal](./media/functions-create-first-azure-function/function-app-develop-tab-testing.png)

2. <span data-ttu-id="e51d6-122">Wklej adres URL funkcji do paska adresu przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="e51d6-122">Paste the function URL into your browser's address bar.</span></span> <span data-ttu-id="e51d6-123">Dołącz ciąg zapytania `&name=<yourname>` do tego adresu URL i naciśnij klawisz `Enter` na klawiaturze, aby wykonać żądanie.</span><span class="sxs-lookup"><span data-stu-id="e51d6-123">Append the query string `&name=<yourname>` to this URL and press the `Enter` key on your keyboard to execute the request.</span></span> <span data-ttu-id="e51d6-124">Poniżej przedstawiono przykład odpowiedzi zwróconej przez funkcję w przeglądarce Edge:</span><span class="sxs-lookup"><span data-stu-id="e51d6-124">The following is an example of the response returned by the function in the Edge browser:</span></span>

    ![Odpowiedź funkcji wyświetlona w przeglądarce.](./media/functions-create-first-azure-function/function-app-browser-testing.png)

    <span data-ttu-id="e51d6-126">Adres URL żądania zawiera klucz, który domyślnie jest wymagany do uzyskania dostępu do funkcji za pośrednictwem protokołu HTTP.</span><span class="sxs-lookup"><span data-stu-id="e51d6-126">The request URL includes a key that is required, by default, to access your function over HTTP.</span></span>   

3. <span data-ttu-id="e51d6-127">Gdy funkcja działa, informacje o śledzeniu są zapisywane w dziennikach.</span><span class="sxs-lookup"><span data-stu-id="e51d6-127">When your function runs, trace information is written to the logs.</span></span> <span data-ttu-id="e51d6-128">Aby wyświetlić dane wyjściowe śledzenia z poprzedniego wykonania, wróć do funkcji w portalu i kliknij strzałkę w górę w dolnej części ekranu, aby rozwinąć pozycję **Dzienniki**.</span><span class="sxs-lookup"><span data-stu-id="e51d6-128">To see the trace output from the previous execution, return to your function in the portal and click the up arrow at the bottom of the screen to expand **Logs**.</span></span> 

   ![Podgląd dziennika usługi Functions w witrynie Azure Portal.](./media/functions-create-first-azure-function/function-view-logs.png)

## <a name="clean-up-resources"></a><span data-ttu-id="e51d6-130">Oczyszczanie zasobów</span><span class="sxs-lookup"><span data-stu-id="e51d6-130">Clean up resources</span></span>

[!INCLUDE [Clean up resources](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a><span data-ttu-id="e51d6-131">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e51d6-131">Next steps</span></span>

<span data-ttu-id="e51d6-132">Utworzono aplikację funkcji z prostą funkcją wyzwalaną przez protokół HTTP.</span><span class="sxs-lookup"><span data-stu-id="e51d6-132">You have created a function app with a simple HTTP triggered function.</span></span>  

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

<span data-ttu-id="e51d6-133">Aby uzyskać więcej informacji, zobacz [Powiązania protokołu HTTP i elementów webhook w usłudze Azure Functions](functions-bindings-http-webhook.md).</span><span class="sxs-lookup"><span data-stu-id="e51d6-133">For more information, see [Azure Functions HTTP and webhook bindings](functions-bindings-http-webhook.md).</span></span>



