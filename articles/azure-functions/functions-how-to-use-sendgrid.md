---
title: "Sposób użycia funkcji Azure SendGrid | Dokumentacja firmy Microsoft"
description: "Przedstawia sposób użycia SendGrid w funkcji platformy Azure"
services: functions
documentationcenter: na
author: rachelappel
manager: erikre
ms.service: functions
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 01/31/2017
ms.author: rachelap
ms.openlocfilehash: 05c9f4e4a4351219da68af8b702c25f21d7d4d02
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-sendgrid-in-azure-functions"></a><span data-ttu-id="c33d8-103">Jak używać SendGrid w funkcji platformy Azure</span><span class="sxs-lookup"><span data-stu-id="c33d8-103">How to use SendGrid in Azure Functions</span></span>

## <a name="sendgrid-overview"></a><span data-ttu-id="c33d8-104">Omówienie SendGrid</span><span class="sxs-lookup"><span data-stu-id="c33d8-104">SendGrid Overview</span></span>

<span data-ttu-id="c33d8-105">Azure Functions obsługuje SendGrid output powiązania, aby umożliwić funkcji do wysyłania wiadomości e-mail przy użyciu kilku wierszy kodu i konta SendGrid.</span><span class="sxs-lookup"><span data-stu-id="c33d8-105">Azure Functions supports SendGrid output bindings to enable your functions to send email messages with a few lines of code and a SendGrid account.</span></span>

<span data-ttu-id="c33d8-106">Aby użyć interfejsu API SendGrid w funkcji platformy Azure, musisz mieć [konta SendGrid](http://SendGrid.com).</span><span class="sxs-lookup"><span data-stu-id="c33d8-106">To use the SendGrid API in an Azure Function, you must have a [SendGrid account](http://SendGrid.com).</span></span> <span data-ttu-id="c33d8-107">Ponadto musi mieć klucz interfejsu API SendGrid.</span><span class="sxs-lookup"><span data-stu-id="c33d8-107">Additionally, you must have a SendGrid API Key.</span></span> <span data-ttu-id="c33d8-108">Zaloguj się do swojego konta SendGrid, a następnie kliknij przycisk **ustawienia** następnie **klucz interfejsu API** do wygenerowania klucza interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="c33d8-108">Log in to your SendGrid account and click **Settings** then **API Key** to generate an API key.</span></span> <span data-ttu-id="c33d8-109">Zachowanie dostęp do tego klucza, jak używasz w nadchodzących kroku.</span><span class="sxs-lookup"><span data-stu-id="c33d8-109">Keep this key available as you use it in an upcoming step.</span></span>

<span data-ttu-id="c33d8-110">Teraz można przystąpić do tworzenia aplikacji funkcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="c33d8-110">You are now ready to create an Azure Function app.</span></span>

## <a name="create-an-azure-function-app"></a><span data-ttu-id="c33d8-111">Tworzenie aplikacji funkcji platformy Azure</span><span class="sxs-lookup"><span data-stu-id="c33d8-111">Create an Azure Function app</span></span> 

<span data-ttu-id="c33d8-112">Aplikacje funkcji platformy Azure są kontenerami dla co najmniej jedną funkcję platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="c33d8-112">Azure Function Apps are containers for one or more Azure functions.</span></span> <span data-ttu-id="c33d8-113">Środowisko Azure functions to właśnie tę — funkcja.</span><span class="sxs-lookup"><span data-stu-id="c33d8-113">Azure functions are just that - a function.</span></span> <span data-ttu-id="c33d8-114">Każda funkcja Azure jest powiązany jeden wyzwalacz, który jest zdarzenie, które powoduje, że funkcja Uruchom.</span><span class="sxs-lookup"><span data-stu-id="c33d8-114">Each Azure function is tied to one trigger, which is an event that causes the function to run.</span></span>
<span data-ttu-id="c33d8-115">Każdej funkcji mogą zawierać dowolną liczbę danych wejściowych lub wyjściowych powiązania.</span><span class="sxs-lookup"><span data-stu-id="c33d8-115">Each function can contain any number of input or output bindings.</span></span> <span data-ttu-id="c33d8-116">Powiązania są usług używanych w funkcji.</span><span class="sxs-lookup"><span data-stu-id="c33d8-116">Bindings are services that you can use in a function.</span></span> <span data-ttu-id="c33d8-117">SendGrid jest powiązania wyjściowego, który służy do wysyłania wiadomości e-mail.</span><span class="sxs-lookup"><span data-stu-id="c33d8-117">SendGrid is an output binding you can use to send email.</span></span> 

1. <span data-ttu-id="c33d8-118">Zaloguj się do portalu Azure i [tworzenie aplikacji platformy Azure funkcja](https://docs.microsoft.com/azure/azure-functions/functions-create-first-azure-function) lub Otwórz istniejącą aplikację w funkcji.</span><span class="sxs-lookup"><span data-stu-id="c33d8-118">Log in to the Azure portal and [create an Azure Function App](https://docs.microsoft.com/azure/azure-functions/functions-create-first-azure-function) or open an existing Function app.</span></span> 
2. <span data-ttu-id="c33d8-119">Tworzenie funkcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="c33d8-119">Create an Azure function.</span></span> <span data-ttu-id="c33d8-120">Aby zachować prosty, wybierz ręczne wyzwalacza i C#.</span><span class="sxs-lookup"><span data-stu-id="c33d8-120">To keep it simple, choose a manual trigger and C#.</span></span> 

 ![Tworzenie funkcji platformy Azure](./media/functions-how-to-use-sendgrid/functions-new-function-manual-trigger-page.png)

## <a name="configure-sendgrid-for-use-in-an-azure-function-app"></a><span data-ttu-id="c33d8-122">Konfigurowanie SendGrid do użycia w aplikacji Azure — funkcja</span><span class="sxs-lookup"><span data-stu-id="c33d8-122">Configure SendGrid for use in an Azure Function app</span></span>

<span data-ttu-id="c33d8-123">Klucz interfejsu API SendGrid muszą być przechowywane jako ustawienie aplikacji w celu używania go w funkcji.</span><span class="sxs-lookup"><span data-stu-id="c33d8-123">You must store your SendGrid API Key as an app setting to use it in a function.</span></span> <span data-ttu-id="c33d8-124">W polu ApiKey nie jest rzeczywista klucza interfejsu API SendGrid, ale ustawienie aplikacji definiować reprezentujące rzeczywistego klucza interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="c33d8-124">The ApiKey field is not your actual SendGrid API key, but an app setting you define that represents your actual API key.</span></span> <span data-ttu-id="c33d8-125">Przechowywanie klucza w ten sposób jest zabezpieczeń, ponieważ jest oddzielony od dowolnego kodu lub pliki, które może być wyewidencjonowany do kontroli kodu źródłowego.</span><span class="sxs-lookup"><span data-stu-id="c33d8-125">Storing your key this way is for security, since it is separate from any code or files that might be checked into source code control.</span></span>

- <span data-ttu-id="c33d8-126">Utwórz **AppSettings** klucza w aplikacji funkcji **ustawienia aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="c33d8-126">Create an **AppSettings** key in your function app's **Application Settings**.</span></span>

 ![Tworzenie funkcji platformy Azure](./media/functions-how-to-use-sendgrid/functions-configure-sendgrid-api-key-app-settings.png)

## <a name="configure-sendgrid-output-bindings"></a><span data-ttu-id="c33d8-128">Skonfiguruj SendGrid powiązania danych wyjściowych</span><span class="sxs-lookup"><span data-stu-id="c33d8-128">Configure SendGrid output bindings</span></span>

<span data-ttu-id="c33d8-129">SendGrid jest dostępna jako platformy Azure funkcja powiązania wyjściowego.</span><span class="sxs-lookup"><span data-stu-id="c33d8-129">SendGrid is available as an Azure function output binding.</span></span> <span data-ttu-id="c33d8-130">Aby utworzyć SendGrid powiązania wyjściowego:</span><span class="sxs-lookup"><span data-stu-id="c33d8-130">To create a SendGrid output binding:</span></span>

1. <span data-ttu-id="c33d8-131">Przejdź do **integracji** kartę funkcji w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="c33d8-131">Go to the **Integrate** tab of the function in the Azure portal.</span></span>
2. <span data-ttu-id="c33d8-132">Kliknij przycisk **nowe dane wyjściowe** utworzyć SendGrid powiązania wyjściowego.</span><span class="sxs-lookup"><span data-stu-id="c33d8-132">Click **New Output** to create a SendGrid output binding.</span></span>
3. <span data-ttu-id="c33d8-133">Wypełnij **klucz interfejsu API** i **Nazwa parametru komunikatu** właściwości.</span><span class="sxs-lookup"><span data-stu-id="c33d8-133">Fill in the **API Key** and **Message parameter name** properties.</span></span> <span data-ttu-id="c33d8-134">Jeśli chcesz, możesz teraz wprowadzić inne właściwości lub ich zamiast tego kodu.</span><span class="sxs-lookup"><span data-stu-id="c33d8-134">If you want, you can enter the other properties now, or code them instead.</span></span> <span data-ttu-id="c33d8-135">Te ustawienia mogą być używane jako domyślne.</span><span class="sxs-lookup"><span data-stu-id="c33d8-135">These settings can be used as defaults.</span></span>

 ![Skonfiguruj SendGrid powiązania danych wyjściowych](./media/functions-how-to-use-sendgrid/functions-configure-sendgrid-output-bindings.png)

<span data-ttu-id="c33d8-137">Dodawanie powiązania funkcji tworzy plik o nazwie **function.json** w folderze z funkcji.</span><span class="sxs-lookup"><span data-stu-id="c33d8-137">Adding a binding to a function creates a file called **function.json** in your function's folder.</span></span> <span data-ttu-id="c33d8-138">Ten plik zawiera te same informacje, które widać w funkcji Azure **integracji** karcie, ale w formacie Json formatowania.</span><span class="sxs-lookup"><span data-stu-id="c33d8-138">This file contains all the same information that you see in the Azure function's **Integrate** tab, but in Json format.</span></span> <span data-ttu-id="c33d8-139">Ustawienie **ApiKey**, **komunikat**, i **z** pól utworzyć następujące wpisy w **function.json** pliku:</span><span class="sxs-lookup"><span data-stu-id="c33d8-139">Setting the **ApiKey**, **message**, and **from** fields create the following entries in the **function.json** file:</span></span> 

```json
{
  "bindings": [    
    {
      "type": "sendGrid",
      "name": "message",
      "apiKey": "SendGridKey",
      "direction": "out",
      "from": "azure@contoso.com"
    }
  ],
  "disabled": false
}
```

<span data-ttu-id="c33d8-140">Jeśli wolisz, użytkownik może modyfikować tego pliku samodzielnie bezpośrednio.</span><span class="sxs-lookup"><span data-stu-id="c33d8-140">If you prefer, you may modify this file yourself directly.</span></span>

<span data-ttu-id="c33d8-141">Teraz, gdy zostanie utworzony i skonfigurowany aplikacji funkcji i funkcji, można napisać kod, aby wysłać wiadomość e-mail.</span><span class="sxs-lookup"><span data-stu-id="c33d8-141">Now that you have created and configured the Function App and function, you can write the code to send an email.</span></span>

## <a name="write-code-that-creates-and-sends-email"></a><span data-ttu-id="c33d8-142">Pisanie kodu, który tworzy i wysyła wiadomości e-mail</span><span class="sxs-lookup"><span data-stu-id="c33d8-142">Write code that creates and sends email</span></span>

<span data-ttu-id="c33d8-143">Interfejs API SendGrid zawiera wszystkie polecenia, które należy utworzyć i wysłać wiadomość e-mail.</span><span class="sxs-lookup"><span data-stu-id="c33d8-143">The SendGrid API contains all the commands you need to create and send an email.</span></span>  

- <span data-ttu-id="c33d8-144">Zastąp kod w funkcji z następującym kodem:</span><span class="sxs-lookup"><span data-stu-id="c33d8-144">Replace the code in the function with the following code:</span></span>

```cs
#r "SendGrid"
using System;
using SendGrid.Helpers.Mail;

public static void Run(TraceWriter log, string input, out Mail message)
{
    message = new Mail
    {        
        Subject = "Azure news"          
    };

    var personalization = new Personalization();
    // change to email of recipient
    personalization.AddTo(new Email("MoreEmailPlease@contoso.com"));   

    Content content = new Content
    {
        Type = "text/plain",
        Value = input
    };
    message.AddContent(content);
    message.AddPersonalization(personalization);
}
```

<span data-ttu-id="c33d8-145">Zwróć uwagę, pierwszy wiersz zawiera ```#r``` dyrektywy, który odwołuje się do zestawu SendGrid.</span><span class="sxs-lookup"><span data-stu-id="c33d8-145">Notice the first line contains the ```#r``` directive that references the SendGrid assembly.</span></span> <span data-ttu-id="c33d8-146">Następnie można użyć ```using``` instrukcji, aby łatwo uzyskiwać dostęp do obiektów w tej przestrzeni nazw.</span><span class="sxs-lookup"><span data-stu-id="c33d8-146">After that, you can use a ```using``` statement to more easily access the objects in that namespace.</span></span> <span data-ttu-id="c33d8-147">W kodzie, tworzenie wystąpień ```Mail```, ```Personalization```, i ```Content``` obiektów z interfejsu API SendGrid tworzące wiadomości e-mail.</span><span class="sxs-lookup"><span data-stu-id="c33d8-147">In the code, create instances of ```Mail```, ```Personalization```, and ```Content``` objects from the SendGrid API that compose the email.</span></span> <span data-ttu-id="c33d8-148">Po powrocie komunikat SendGrid dostarcza ją.</span><span class="sxs-lookup"><span data-stu-id="c33d8-148">When you return the message, SendGrid delivers it.</span></span> 

<span data-ttu-id="c33d8-149">Sygnatura funkcji zawiera również dodatkowe parametru typu out ```Mail``` o nazwie ```message```.</span><span class="sxs-lookup"><span data-stu-id="c33d8-149">The function's signature also contains an extra out parameter of type ```Mail``` named ```message```.</span></span> <span data-ttu-id="c33d8-150">Zarówno wejściowa i wyjściowa express powiązań, same jako parametry funkcji w kodzie.</span><span class="sxs-lookup"><span data-stu-id="c33d8-150">Both input and output bindings express themselves as function parameters in code.</span></span> 

2. <span data-ttu-id="c33d8-151">Testowanie kodu, klikając **testu** i wprowadzania komunikatu do **treść żądania** pola, klikając **Uruchom** przycisku.</span><span class="sxs-lookup"><span data-stu-id="c33d8-151">Test your code by clicking **Test** and entering a message into the **Request body** field, then clicking the **Run** button.</span></span>

 ![Testowanie kodu](./media/functions-how-to-use-sendgrid/functions-develop-test-sendgrid.png)

3. <span data-ttu-id="c33d8-153">Sprawdź pocztę e-mail, aby sprawdzić, czy SendGrid wysyłane wiadomości e-mail.</span><span class="sxs-lookup"><span data-stu-id="c33d8-153">Check email to verify that SendGrid sent the email.</span></span> <span data-ttu-id="c33d8-154">Należy przejść do adresu w kodzie z kroku 1 i zawiera komunikat z **treść żądania**.</span><span class="sxs-lookup"><span data-stu-id="c33d8-154">It should go to the address in the code from step 1, and contain the message from the **Request body**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c33d8-155">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c33d8-155">Next steps</span></span>
<span data-ttu-id="c33d8-156">W tym artykule wykazało, jak używać usługi SendGrid do tworzenia i wysyłania wiadomości e-mail.</span><span class="sxs-lookup"><span data-stu-id="c33d8-156">This article has demonstrated how to use the SendGrid service to create and send email.</span></span> <span data-ttu-id="c33d8-157">Aby dowiedzieć się więcej na temat korzystania z usługi Azure Functions w aplikacjach, zobacz następujące tematy:</span><span class="sxs-lookup"><span data-stu-id="c33d8-157">To learn more about using Azure Functions in your apps, see the following topics:</span></span> 

- <span data-ttu-id="c33d8-158">[Najlepsze rozwiązania dotyczące usługi Azure Functions](functions-best-practices.md) wymieniono najważniejsze wskazówki podczas tworzenia usługi Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="c33d8-158">[Best practices for Azure Functions](functions-best-practices.md) Lists some best practices to use when creating Azure Functions.</span></span>

- <span data-ttu-id="c33d8-159">[Dokumentacja dla deweloperów usługi Azure funkcji](functions-reference.md) programisty dokumentacja dotycząca kodowania funkcji oraz definiowania wyzwalaczy i powiązań.</span><span class="sxs-lookup"><span data-stu-id="c33d8-159">[Azure Functions developer reference](functions-reference.md) Programmer reference for coding functions and defining triggers and bindings.</span></span>

- <span data-ttu-id="c33d8-160">[Testowanie usługi Azure Functions](functions-test-a-function.md) opis różnych narzędzi i technik testowania funkcji.</span><span class="sxs-lookup"><span data-stu-id="c33d8-160">[Testing Azure Functions](functions-test-a-function.md) Describes various tools and techniques for testing your functions.</span></span>