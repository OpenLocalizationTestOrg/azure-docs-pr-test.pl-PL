---
title: "aaaCreate funkcję, która działa zgodnie z harmonogramem na platformie Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate funkcji na platformie Azure, który jest uruchamiany zgodnie z harmonogramem przez Ciebie."
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
ms.openlocfilehash: 793b06a65a154466dfd4c121bcc88082227cd597
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-function-in-azure-that-is-triggered-by-a-timer"></a><span data-ttu-id="47689-103">Tworzenie funkcji wyzwalanej czasomierzem na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="47689-103">Create a function in Azure that is triggered by a timer</span></span>

<span data-ttu-id="47689-104">Dowiedz się, jak toocreate usługi Azure Functions toouse funkcję, która działa na podstawie zdefiniowanego harmonogramu.</span><span class="sxs-lookup"><span data-stu-id="47689-104">Learn how toouse Azure Functions toocreate a function that runs based a schedule that you define.</span></span>

![Tworzenie aplikacji funkcji w hello portalu Azure](./media/functions-create-scheduled-function/function-app-in-portal-editor.png)

## <a name="prerequisites"></a><span data-ttu-id="47689-106">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="47689-106">Prerequisites</span></span>

<span data-ttu-id="47689-107">toocomplete tego samouczka:</span><span class="sxs-lookup"><span data-stu-id="47689-107">toocomplete this tutorial:</span></span>

+ <span data-ttu-id="47689-108">Jeśli nie masz subskrypcji platformy Azure, przed rozpoczęciem utwórz [bezpłatne konto](https://azure.microsoft.com/free/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="47689-108">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [functions-portal-favorite-function-apps](../../includes/functions-portal-favorite-function-apps.md)]

## <a name="create-an-azure-function-app"></a><span data-ttu-id="47689-109">Tworzenie aplikacji funkcji platformy Azure</span><span class="sxs-lookup"><span data-stu-id="47689-109">Create an Azure Function app</span></span>

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

![Pomyślnie utworzona aplikacja funkcji.](./media/functions-create-first-azure-function/function-app-create-success.png)

<span data-ttu-id="47689-111">Następnie należy utworzyć funkcji w hello nowej funkcji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="47689-111">Next, you create a function in hello new function app.</span></span>

<a name="create-function"></a>

## <a name="create-a-timer-triggered-function"></a><span data-ttu-id="47689-112">Tworzenie funkcji wyzwalanej czasomierzem</span><span class="sxs-lookup"><span data-stu-id="47689-112">Create a timer triggered function</span></span>

1. <span data-ttu-id="47689-113">Rozwiń węzeł funkcji aplikacji, a następnie kliknij przycisk hello  **+**  obok przycisku zbyt**funkcji**.</span><span class="sxs-lookup"><span data-stu-id="47689-113">Expand your function app and click hello **+** button next too**Functions**.</span></span> <span data-ttu-id="47689-114">Jeśli hello pierwszej funkcji w funkcji aplikacji, wybierz **Niestandardowa funkcja**.</span><span class="sxs-lookup"><span data-stu-id="47689-114">If this is hello first function in your function app, select **Custom function**.</span></span> <span data-ttu-id="47689-115">Spowoduje to wyświetlenie hello pełny zestaw szablonów funkcji.</span><span class="sxs-lookup"><span data-stu-id="47689-115">This displays hello complete set of function templates.</span></span>

    ![Funkcje strony szybkiego startu w hello portalu Azure](./media/functions-create-scheduled-function/add-first-function.png)

2. <span data-ttu-id="47689-117">Wybierz hello **TimerTrigger** szablon odpowiedni język.</span><span class="sxs-lookup"><span data-stu-id="47689-117">Select hello **TimerTrigger** template for your desired language.</span></span> <span data-ttu-id="47689-118">Następnie należy użyć ustawień hello określoną w tabeli hello:</span><span class="sxs-lookup"><span data-stu-id="47689-118">Then use hello settings as specified in hello table:</span></span>

    ![Utwórz funkcję czasomierza wyzwalane w hello portalu Azure.](./media/functions-create-scheduled-function/functions-create-timer-trigger.png)

    | <span data-ttu-id="47689-120">Ustawienie</span><span class="sxs-lookup"><span data-stu-id="47689-120">Setting</span></span> | <span data-ttu-id="47689-121">Sugerowana wartość</span><span class="sxs-lookup"><span data-stu-id="47689-121">Suggested value</span></span> | <span data-ttu-id="47689-122">Opis</span><span class="sxs-lookup"><span data-stu-id="47689-122">Description</span></span> |
    |---|---|---|
    | <span data-ttu-id="47689-123">**Nazwa funkcji**</span><span class="sxs-lookup"><span data-stu-id="47689-123">**Name your function**</span></span> | <span data-ttu-id="47689-124">TimerTriggerCSharp1</span><span class="sxs-lookup"><span data-stu-id="47689-124">TimerTriggerCSharp1</span></span> | <span data-ttu-id="47689-125">Definiuje nazwę hello funkcji czasomierza wyzwolone.</span><span class="sxs-lookup"><span data-stu-id="47689-125">Defines hello name of your timer triggered function.</span></span> |
    | <span data-ttu-id="47689-126">**[Harmonogram](http://en.wikipedia.org/wiki/Cron#CRON_expression)**</span><span class="sxs-lookup"><span data-stu-id="47689-126">**[Schedule](http://en.wikipedia.org/wiki/Cron#CRON_expression)**</span></span> | <span data-ttu-id="47689-127">0 \*/1 \* \* \* \*</span><span class="sxs-lookup"><span data-stu-id="47689-127">0 \*/1 \* \* \* \*</span></span> | <span data-ttu-id="47689-128">Pole sześć [wyrażenie CRON](http://en.wikipedia.org/wiki/Cron#CRON_expression) która planuje toorun Twojego funkcja co minutę.</span><span class="sxs-lookup"><span data-stu-id="47689-128">A six field [CRON expression](http://en.wikipedia.org/wiki/Cron#CRON_expression) that schedules your function toorun every minute.</span></span> |

2. <span data-ttu-id="47689-129">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="47689-129">Click **Create**.</span></span> <span data-ttu-id="47689-130">Zostanie utworzona funkcja w wybranym języku uruchamiana co minutę.</span><span class="sxs-lookup"><span data-stu-id="47689-130">A function is created in your chosen language that runs every minute.</span></span>

3. <span data-ttu-id="47689-131">Wyświetlanie informacji o śledzeniu zapisane dzienniki toohello Sprawdź wykonywania.</span><span class="sxs-lookup"><span data-stu-id="47689-131">Verify execution by viewing trace information written toohello logs.</span></span>

    ![Funkcje logowania podglądu hello portalu Azure.](./media/functions-create-scheduled-function/functions-timer-trigger-view-logs2.png)

<span data-ttu-id="47689-133">Teraz można zmienić harmonogramu hello funkcji wykonywania rzadziej, takich jak co godzinę.</span><span class="sxs-lookup"><span data-stu-id="47689-133">Now, you can change hello function's schedule so that it runs less often, such as once every hour.</span></span> 

## <a name="update-hello-timer-schedule"></a><span data-ttu-id="47689-134">Harmonogram czasomierza hello aktualizacji</span><span class="sxs-lookup"><span data-stu-id="47689-134">Update hello timer schedule</span></span>

1. <span data-ttu-id="47689-135">Rozwiń swoją funkcję i kliknij pozycję **Integracja**.</span><span class="sxs-lookup"><span data-stu-id="47689-135">Expand your function and click **Integrate**.</span></span> <span data-ttu-id="47689-136">Jest to, którym zdefiniować dane wejściowe i wyjściowe powiązań dla funkcji i również ustawić harmonogram hello.</span><span class="sxs-lookup"><span data-stu-id="47689-136">This is where you define input and output bindings for your function and also set hello schedule.</span></span> 

2. <span data-ttu-id="47689-137">W polu **Harmonogram** wprowadź nową wartość `0 0 */1 * * *`, a następnie kliknij przycisk **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="47689-137">Enter a new **Schedule** value of `0 0 */1 * * *`, and then click **Save**.</span></span>  

![Funkcje zaktualizować harmonogramu czasomierza w hello portalu Azure.](./media/functions-create-scheduled-function/functions-timer-trigger-change-schedule.png)

<span data-ttu-id="47689-139">Funkcja będzie teraz uruchamiana raz na godzinę.</span><span class="sxs-lookup"><span data-stu-id="47689-139">You now have a function that runs once every hour.</span></span> 

## <a name="clean-up-resources"></a><span data-ttu-id="47689-140">Oczyszczanie zasobów</span><span class="sxs-lookup"><span data-stu-id="47689-140">Clean up resources</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a><span data-ttu-id="47689-141">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="47689-141">Next steps</span></span>

<span data-ttu-id="47689-142">Utworzono funkcję uruchamianą zgodnie z harmonogramem.</span><span class="sxs-lookup"><span data-stu-id="47689-142">You have created a function that runs based on a schedule.</span></span>

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

<span data-ttu-id="47689-143">Aby uzyskać więcej informacji na temat wyzwalaczy czasomierza, zobacz [Planowanie wykonywania kodu za pomocą usługi Azure Functions](functions-bindings-timer.md).</span><span class="sxs-lookup"><span data-stu-id="47689-143">For more information timer triggers, see [Schedule code execution with Azure Functions](functions-bindings-timer.md).</span></span>