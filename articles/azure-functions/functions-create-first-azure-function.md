---
title: aaaCreate pierwszej funkcji z hello portalu Azure | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak toocreate platformy Azure pierwsze działać przez wykonanie niekorzystającą hello portalu Azure."
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
ms.openlocfilehash: 84283d7d4bc6015061946af4589f9a70ae61f36b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-function-in-hello-azure-portal"></a><span data-ttu-id="032cf-103">Tworzenie pierwszej funkcji w hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="032cf-103">Create your first function in hello Azure portal</span></span>

<span data-ttu-id="032cf-104">Środowisko Azure Functions umożliwia wykonywanie kodu w środowisku bez serwera bez konieczności toofirst tworzenie maszyny Wirtualnej lub opublikować aplikację sieci web.</span><span class="sxs-lookup"><span data-stu-id="032cf-104">Azure Functions lets you execute your code in a serverless environment without having toofirst create a VM or publish a web application.</span></span> <span data-ttu-id="032cf-105">W tym temacie Dowiedz się, jak toouse funkcjonuje toocreate funkcję "hello world" hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="032cf-105">In this topic, learn how toouse Functions toocreate a "hello world" function in hello Azure portal.</span></span>

![Tworzenie aplikacji funkcji w hello portalu Azure](./media/functions-create-first-azure-function/function-app-in-portal-editor.png)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="log-in-tooazure"></a><span data-ttu-id="032cf-107">Zaloguj się za tooAzure</span><span class="sxs-lookup"><span data-stu-id="032cf-107">Log in tooAzure</span></span>

<span data-ttu-id="032cf-108">Zaloguj się za toohello [portalu Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="032cf-108">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>

## <a name="create-a-function-app"></a><span data-ttu-id="032cf-109">Tworzenie aplikacji funkcji</span><span class="sxs-lookup"><span data-stu-id="032cf-109">Create a function app</span></span>

<span data-ttu-id="032cf-110">Funkcja aplikacji toohost hello wykonywanie funkcji są wymagane.</span><span class="sxs-lookup"><span data-stu-id="032cf-110">You must have a function app toohost hello execution of your functions.</span></span> <span data-ttu-id="032cf-111">Aplikacja funkcji umożliwia grupowanie funkcji jako jednostki logicznej, co ułatwia wdrażanie i udostępnianie zasobów oraz zarządzanie nimi.</span><span class="sxs-lookup"><span data-stu-id="032cf-111">A function app lets you group functions as a logic unit for easier management, deployment, and sharing of resources.</span></span> 

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

<span data-ttu-id="032cf-112">Następnie należy utworzyć funkcji w hello nowej funkcji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="032cf-112">Next, you create a function in hello new function app.</span></span>

## <span data-ttu-id="032cf-113"><a name="create-function"></a>Tworzenie funkcji wyzwalanej przez protokół HTTP</span><span class="sxs-lookup"><span data-stu-id="032cf-113"><a name="create-function"></a>Create an HTTP triggered function</span></span>

1. <span data-ttu-id="032cf-114">Rozwiń węzeł nowej aplikacji funkcji, a następnie kliknij przycisk hello  **+**  obok przycisku zbyt**funkcji**.</span><span class="sxs-lookup"><span data-stu-id="032cf-114">Expand your new function app, then click hello **+** button next too**Functions**.</span></span>

2.  <span data-ttu-id="032cf-115">W hello **szybkie rozpoczęcie pracy** wybierz pozycję **element WebHook i interfejs API**, **wybierz język** Twojego funkcji, a następnie kliknij przycisk **tworzenia tej funkcji** .</span><span class="sxs-lookup"><span data-stu-id="032cf-115">In hello **Get started quickly** page, select **WebHook + API**, **Choose a language** for your function, and click **Create this function**.</span></span> 
   
    ![Funkcji szybkiego startu w hello portalu Azure.](./media/functions-create-first-azure-function/function-app-quickstart-node-webhook.png)

<span data-ttu-id="032cf-117">Funkcja jest tworzony w wybrany język przy użyciu szablonu hello funkcji HTTP wyzwolone.</span><span class="sxs-lookup"><span data-stu-id="032cf-117">A function is created in your chosen language using hello template for an HTTP triggered function.</span></span> <span data-ttu-id="032cf-118">Możesz uruchomić hello nową funkcję, wysyłając żądania HTTP.</span><span class="sxs-lookup"><span data-stu-id="032cf-118">You can run hello new function by sending an HTTP request.</span></span>

## <a name="test-hello-function"></a><span data-ttu-id="032cf-119">Funkcja hello testu</span><span class="sxs-lookup"><span data-stu-id="032cf-119">Test hello function</span></span>

1. <span data-ttu-id="032cf-120">W nowej funkcji kliknij przycisk **</> Pobierz adres URL funkcji**, wybierz pozycję **domyślne (klawisz funkcji)**, a następnie kliknij przycisk **Kopiuj**.</span><span class="sxs-lookup"><span data-stu-id="032cf-120">In your new function, click **</> Get function URL**, select **default (Function key)**, and then click **Copy**.</span></span> 

    ![Skopiuj adres URL funkcji hello z hello portalu Azure](./media/functions-create-first-azure-function/function-app-develop-tab-testing.png)

2. <span data-ttu-id="032cf-122">Wklej adres URL funkcji hello w pasku adresu przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="032cf-122">Paste hello function URL into your browser's address bar.</span></span> <span data-ttu-id="032cf-123">Dołącz ciągu zapytania hello `&name=<yourname>` toothis hello adresu URL i naciśnij klawisz `Enter` klucza na żądanie hello tooexecute klawiatury.</span><span class="sxs-lookup"><span data-stu-id="032cf-123">Append hello query string `&name=<yourname>` toothis URL and press hello `Enter` key on your keyboard tooexecute hello request.</span></span> <span data-ttu-id="032cf-124">Witaj poniżej znajduje się przykład hello odpowiedź zwrócona przez funkcję hello w przeglądarce Edge hello:</span><span class="sxs-lookup"><span data-stu-id="032cf-124">hello following is an example of hello response returned by hello function in hello Edge browser:</span></span>

    ![Funkcja odpowiedzi w przeglądarce hello.](./media/functions-create-first-azure-function/function-app-browser-testing.png)

    <span data-ttu-id="032cf-126">adres URL zawiera klucz, który jest wymagany, domyślnie tooaccess żądania Hello funkcji za pośrednictwem protokołu HTTP.</span><span class="sxs-lookup"><span data-stu-id="032cf-126">hello request URL includes a key that is required, by default, tooaccess your function over HTTP.</span></span>   

3. <span data-ttu-id="032cf-127">Po uruchomieniu funkcji informacje śledzenia są zapisywane toohello dzienniki.</span><span class="sxs-lookup"><span data-stu-id="032cf-127">When your function runs, trace information is written toohello logs.</span></span> <span data-ttu-id="032cf-128">wyniki śledzenia hello toosee hello poprzednie wykonanie powróć tooyour funkcji w portalu hello i kliknij przycisk hello Strzałka u dołu hello tooexpand ekranie powitania w górę **dzienniki**.</span><span class="sxs-lookup"><span data-stu-id="032cf-128">toosee hello trace output from hello previous execution, return tooyour function in hello portal and click hello up arrow at hello bottom of hello screen tooexpand **Logs**.</span></span> 

   ![Funkcje logowania podglądu hello portalu Azure.](./media/functions-create-first-azure-function/function-view-logs.png)

## <a name="clean-up-resources"></a><span data-ttu-id="032cf-130">Oczyszczanie zasobów</span><span class="sxs-lookup"><span data-stu-id="032cf-130">Clean up resources</span></span>

[!INCLUDE [Clean up resources](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a><span data-ttu-id="032cf-131">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="032cf-131">Next steps</span></span>

<span data-ttu-id="032cf-132">Utworzono aplikację funkcji z prostą funkcją wyzwalaną przez protokół HTTP.</span><span class="sxs-lookup"><span data-stu-id="032cf-132">You have created a function app with a simple HTTP triggered function.</span></span>  

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

<span data-ttu-id="032cf-133">Aby uzyskać więcej informacji, zobacz [Powiązania protokołu HTTP i elementów webhook w usłudze Azure Functions](functions-bindings-http-webhook.md).</span><span class="sxs-lookup"><span data-stu-id="032cf-133">For more information, see [Azure Functions HTTP and webhook bindings](functions-bindings-http-webhook.md).</span></span>



