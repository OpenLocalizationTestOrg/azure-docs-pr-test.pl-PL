---
title: Tworzenie funkcji uruchamianej zgodnie z harmonogramem na platformie Azure | Microsoft Docs
description: "Dowiedz się, jak utworzyć na platformie Azure funkcję uruchamianą zgodnie z określonym harmonogramem."
services: functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
ms.assetid: ba50ee47-58e0-4972-b67b-828f2dc48701
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/31/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 03cc5e71e8eb20002cf58e713fc0fc92a9129874
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-function-in-azure-that-is-triggered-by-a-timer"></a><span data-ttu-id="a3378-103">Tworzenie funkcji wyzwalanej czasomierzem na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="a3378-103">Create a function in Azure that is triggered by a timer</span></span>

<span data-ttu-id="a3378-104">Dowiedz się, jak za pomocą usługi Azure Functions utworzyć funkcję uruchamianą zgodnie z określonym harmonogramem.</span><span class="sxs-lookup"><span data-stu-id="a3378-104">Learn how to use Azure Functions to create a function that runs based a schedule that you define.</span></span>

![Tworzenie aplikacji funkcji w witrynie Azure Portal](./media/functions-create-scheduled-function/function-app-in-portal-editor.png)

## <a name="prerequisites"></a><span data-ttu-id="a3378-106">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="a3378-106">Prerequisites</span></span>

<span data-ttu-id="a3378-107">W celu ukończenia tego samouczka:</span><span class="sxs-lookup"><span data-stu-id="a3378-107">To complete this tutorial:</span></span>

+ <span data-ttu-id="a3378-108">Jeśli nie masz subskrypcji platformy Azure, przed rozpoczęciem utwórz [bezpłatne konto](https://azure.microsoft.com/free/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="a3378-108">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

## <a name="create-an-azure-function-app"></a><span data-ttu-id="a3378-109">Tworzenie aplikacji funkcji platformy Azure</span><span class="sxs-lookup"><span data-stu-id="a3378-109">Create an Azure Function app</span></span>

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

![Pomyślnie utworzona aplikacja funkcji.](./media/functions-create-first-azure-function/function-app-create-success.png)

<span data-ttu-id="a3378-111">Następnie należy utworzyć funkcję w nowej aplikacji funkcji.</span><span class="sxs-lookup"><span data-stu-id="a3378-111">Next, you create a function in the new function app.</span></span>

<a name="create-function"></a>

## <a name="create-a-timer-triggered-function"></a><span data-ttu-id="a3378-112">Tworzenie funkcji wyzwalanej czasomierzem</span><span class="sxs-lookup"><span data-stu-id="a3378-112">Create a timer triggered function</span></span>

1. <span data-ttu-id="a3378-113">Rozwiń aplikację funkcji i kliknij przycisk **+** obok pozycji **Funkcje**.</span><span class="sxs-lookup"><span data-stu-id="a3378-113">Expand your function app and click the **+** button next to **Functions**.</span></span> <span data-ttu-id="a3378-114">Jeśli jest to pierwsza funkcja w aplikacji funkcji, wybierz pozycję **Funkcja niestandardowa**.</span><span class="sxs-lookup"><span data-stu-id="a3378-114">If this is the first function in your function app, select **Custom function**.</span></span> <span data-ttu-id="a3378-115">Spowoduje to wyświetlenie pełnego zestawu szablonów funkcji.</span><span class="sxs-lookup"><span data-stu-id="a3378-115">This displays the complete set of function templates.</span></span>

    ![Strona szybkiego rozpoczynania pracy z usługą Functions w witrynie Azure Portal](./media/functions-create-scheduled-function/add-first-function.png)

2. <span data-ttu-id="a3378-117">Wybierz szablon **TimerTrigger** dla odpowiedniego języka.</span><span class="sxs-lookup"><span data-stu-id="a3378-117">Select the **TimerTrigger** template for your desired language.</span></span> <span data-ttu-id="a3378-118">Następnie użyj ustawień określonych w tabeli:</span><span class="sxs-lookup"><span data-stu-id="a3378-118">Then use the settings as specified in the table:</span></span>

    ![Utwórz funkcję wyzwalaną czasomierzem w witrynie Azure Portal.](./media/functions-create-scheduled-function/functions-create-timer-trigger.png)

    | <span data-ttu-id="a3378-120">Ustawienie</span><span class="sxs-lookup"><span data-stu-id="a3378-120">Setting</span></span> | <span data-ttu-id="a3378-121">Sugerowana wartość</span><span class="sxs-lookup"><span data-stu-id="a3378-121">Suggested value</span></span> | <span data-ttu-id="a3378-122">Opis</span><span class="sxs-lookup"><span data-stu-id="a3378-122">Description</span></span> |
    |---|---|---|
    | <span data-ttu-id="a3378-123">**Nazwa funkcji**</span><span class="sxs-lookup"><span data-stu-id="a3378-123">**Name your function**</span></span> | <span data-ttu-id="a3378-124">TimerTriggerCSharp1</span><span class="sxs-lookup"><span data-stu-id="a3378-124">TimerTriggerCSharp1</span></span> | <span data-ttu-id="a3378-125">Określa nazwę funkcji wyzwalanej czasomierzem.</span><span class="sxs-lookup"><span data-stu-id="a3378-125">Defines the name of your timer triggered function.</span></span> |
    | <span data-ttu-id="a3378-126">**[Harmonogram](http://en.wikipedia.org/wiki/Cron#CRON_expression)**</span><span class="sxs-lookup"><span data-stu-id="a3378-126">**[Schedule](http://en.wikipedia.org/wiki/Cron#CRON_expression)**</span></span> | <span data-ttu-id="a3378-127">0 \*/1 \* \* \* \*</span><span class="sxs-lookup"><span data-stu-id="a3378-127">0 \*/1 \* \* \* \*</span></span> | <span data-ttu-id="a3378-128">Składające się z 6 pól [wyrażenie CRON](http://en.wikipedia.org/wiki/Cron#CRON_expression) planujące uruchamianie funkcji co minutę.</span><span class="sxs-lookup"><span data-stu-id="a3378-128">A six field [CRON expression](http://en.wikipedia.org/wiki/Cron#CRON_expression) that schedules your function to run every minute.</span></span> |

2. <span data-ttu-id="a3378-129">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="a3378-129">Click **Create**.</span></span> <span data-ttu-id="a3378-130">Zostanie utworzona funkcja w wybranym języku uruchamiana co minutę.</span><span class="sxs-lookup"><span data-stu-id="a3378-130">A function is created in your chosen language that runs every minute.</span></span>

3. <span data-ttu-id="a3378-131">Zweryfikuj uruchomienie, wyświetlając informacje o śledzeniu zapisane w dziennikach.</span><span class="sxs-lookup"><span data-stu-id="a3378-131">Verify execution by viewing trace information written to the logs.</span></span>

    ![Podgląd dziennika usługi Functions w witrynie Azure Portal.](./media/functions-create-scheduled-function/functions-timer-trigger-view-logs2.png)

<span data-ttu-id="a3378-133">Teraz możesz zmienić harmonogram funkcji tak, aby była uruchamiana rzadziej, na przykład co godzinę.</span><span class="sxs-lookup"><span data-stu-id="a3378-133">Now, you can change the function's schedule so that it runs less often, such as once every hour.</span></span> 

## <a name="update-the-timer-schedule"></a><span data-ttu-id="a3378-134">Aktualizowanie harmonogramu czasomierza</span><span class="sxs-lookup"><span data-stu-id="a3378-134">Update the timer schedule</span></span>

1. <span data-ttu-id="a3378-135">Rozwiń swoją funkcję i kliknij pozycję **Integracja**.</span><span class="sxs-lookup"><span data-stu-id="a3378-135">Expand your function and click **Integrate**.</span></span> <span data-ttu-id="a3378-136">W tym miejscu określa się powiązania danych wejściowych i wyjściowych dla funkcji oraz ustawia harmonogram.</span><span class="sxs-lookup"><span data-stu-id="a3378-136">This is where you define input and output bindings for your function and also set the schedule.</span></span> 

2. <span data-ttu-id="a3378-137">W polu **Harmonogram** wprowadź nową wartość `0 0 */1 * * *`, a następnie kliknij przycisk **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="a3378-137">Enter a new **Schedule** value of `0 0 */1 * * *`, and then click **Save**.</span></span>  

![Harmonogram aktualizowania czasomierza usługi Functions w witrynie Azure Portal.](./media/functions-create-scheduled-function/functions-timer-trigger-change-schedule.png)

<span data-ttu-id="a3378-139">Funkcja będzie teraz uruchamiana raz na godzinę.</span><span class="sxs-lookup"><span data-stu-id="a3378-139">You now have a function that runs once every hour.</span></span> 

## <a name="clean-up-resources"></a><span data-ttu-id="a3378-140">Oczyszczanie zasobów</span><span class="sxs-lookup"><span data-stu-id="a3378-140">Clean up resources</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a><span data-ttu-id="a3378-141">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a3378-141">Next steps</span></span>

<span data-ttu-id="a3378-142">Utworzono funkcję uruchamianą zgodnie z harmonogramem.</span><span class="sxs-lookup"><span data-stu-id="a3378-142">You have created a function that runs based on a schedule.</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

<span data-ttu-id="a3378-143">Aby uzyskać więcej informacji na temat wyzwalaczy czasomierza, zobacz [Planowanie wykonywania kodu za pomocą usługi Azure Functions](functions-bindings-timer.md).</span><span class="sxs-lookup"><span data-stu-id="a3378-143">For more information timer triggers, see [Schedule code execution with Azure Functions](functions-bindings-timer.md).</span></span>