---
title: "toouse aaaHow SendGrid w usługi Azure Functions | Dokumentacja firmy Microsoft"
description: "Pokazuje sposób toouse SendGrid w funkcji platformy Azure"
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
ms.openlocfilehash: a0ffdae04e5924c773d2d26427626fc1f570f7ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-sendgrid-in-azure-functions"></a><span data-ttu-id="5452b-103">Jak toouse SendGrid w funkcji platformy Azure</span><span class="sxs-lookup"><span data-stu-id="5452b-103">How toouse SendGrid in Azure Functions</span></span>

## <a name="sendgrid-overview"></a><span data-ttu-id="5452b-104">Omówienie SendGrid</span><span class="sxs-lookup"><span data-stu-id="5452b-104">SendGrid Overview</span></span>

<span data-ttu-id="5452b-105">Azure Functions obsługuje SendGrid output tooenable powiązania wiadomości e-mail toosend funkcji przy użyciu kilku wierszy kodu i konta SendGrid.</span><span class="sxs-lookup"><span data-stu-id="5452b-105">Azure Functions supports SendGrid output bindings tooenable your functions toosend email messages with a few lines of code and a SendGrid account.</span></span>

<span data-ttu-id="5452b-106">toouse API SendGrid hello w funkcji platformy Azure, musi mieć [konta SendGrid](http://SendGrid.com).</span><span class="sxs-lookup"><span data-stu-id="5452b-106">toouse hello SendGrid API in an Azure Function, you must have a [SendGrid account](http://SendGrid.com).</span></span> <span data-ttu-id="5452b-107">Ponadto musi mieć klucz interfejsu API SendGrid.</span><span class="sxs-lookup"><span data-stu-id="5452b-107">Additionally, you must have a SendGrid API Key.</span></span> <span data-ttu-id="5452b-108">Zaloguj się za tooyour SendGrid konta i kliknij przycisk **ustawienia** następnie **klucz interfejsu API** klucza toogenerate interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="5452b-108">Log in tooyour SendGrid account and click **Settings** then **API Key** toogenerate an API key.</span></span> <span data-ttu-id="5452b-109">Zachowanie dostęp do tego klucza, jak używasz w nadchodzących kroku.</span><span class="sxs-lookup"><span data-stu-id="5452b-109">Keep this key available as you use it in an upcoming step.</span></span>

<span data-ttu-id="5452b-110">Wszystko jest teraz gotowy toocreate aplikacji funkcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="5452b-110">You are now ready toocreate an Azure Function app.</span></span>

## <a name="create-an-azure-function-app"></a><span data-ttu-id="5452b-111">Tworzenie aplikacji funkcji platformy Azure</span><span class="sxs-lookup"><span data-stu-id="5452b-111">Create an Azure Function app</span></span> 

<span data-ttu-id="5452b-112">Aplikacje funkcji platformy Azure są kontenerami dla co najmniej jedną funkcję platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="5452b-112">Azure Function Apps are containers for one or more Azure functions.</span></span> <span data-ttu-id="5452b-113">Środowisko Azure functions to właśnie tę — funkcja.</span><span class="sxs-lookup"><span data-stu-id="5452b-113">Azure functions are just that - a function.</span></span> <span data-ttu-id="5452b-114">Każdej funkcji platformy Azure jest wiązana tooone wyzwalacza jest zdarzenie, które powoduje, że toorun funkcja hello.</span><span class="sxs-lookup"><span data-stu-id="5452b-114">Each Azure function is tied tooone trigger, which is an event that causes hello function toorun.</span></span>
<span data-ttu-id="5452b-115">Każdej funkcji mogą zawierać dowolną liczbę danych wejściowych lub wyjściowych powiązania.</span><span class="sxs-lookup"><span data-stu-id="5452b-115">Each function can contain any number of input or output bindings.</span></span> <span data-ttu-id="5452b-116">Powiązania są usług używanych w funkcji.</span><span class="sxs-lookup"><span data-stu-id="5452b-116">Bindings are services that you can use in a function.</span></span> <span data-ttu-id="5452b-117">SendGrid jest wyjścia powiązanie, możesz użyć toosend wiadomości e-mail.</span><span class="sxs-lookup"><span data-stu-id="5452b-117">SendGrid is an output binding you can use toosend email.</span></span> 

1. <span data-ttu-id="5452b-118">Zaloguj się za toohello portalu Azure i [tworzenie aplikacji platformy Azure funkcja](https://docs.microsoft.com/azure/azure-functions/functions-create-first-azure-function) lub Otwórz istniejącą aplikację w funkcji.</span><span class="sxs-lookup"><span data-stu-id="5452b-118">Log in toohello Azure portal and [create an Azure Function App](https://docs.microsoft.com/azure/azure-functions/functions-create-first-azure-function) or open an existing Function app.</span></span> 
2. <span data-ttu-id="5452b-119">Tworzenie funkcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="5452b-119">Create an Azure function.</span></span> <span data-ttu-id="5452b-120">tookeep prostotę, wybierz ręczne wyzwalacza i C#.</span><span class="sxs-lookup"><span data-stu-id="5452b-120">tookeep it simple, choose a manual trigger and C#.</span></span> 

 ![Tworzenie funkcji platformy Azure](./media/functions-how-to-use-sendgrid/functions-new-function-manual-trigger-page.png)

## <a name="configure-sendgrid-for-use-in-an-azure-function-app"></a><span data-ttu-id="5452b-122">Konfigurowanie SendGrid do użycia w aplikacji Azure — funkcja</span><span class="sxs-lookup"><span data-stu-id="5452b-122">Configure SendGrid for use in an Azure Function app</span></span>

<span data-ttu-id="5452b-123">Klucz interfejsu API SendGrid musi być przechowywany jako toouse ustawienie aplikacji w funkcji.</span><span class="sxs-lookup"><span data-stu-id="5452b-123">You must store your SendGrid API Key as an app setting toouse it in a function.</span></span> <span data-ttu-id="5452b-124">Hello ApiKey nie jest rzeczywista klucza interfejsu API SendGrid, ale ustawienie aplikacji definiować reprezentujące rzeczywistego klucza interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="5452b-124">hello ApiKey field is not your actual SendGrid API key, but an app setting you define that represents your actual API key.</span></span> <span data-ttu-id="5452b-125">Przechowywanie klucza w ten sposób jest zabezpieczeń, ponieważ jest oddzielony od dowolnego kodu lub pliki, które może być wyewidencjonowany do kontroli kodu źródłowego.</span><span class="sxs-lookup"><span data-stu-id="5452b-125">Storing your key this way is for security, since it is separate from any code or files that might be checked into source code control.</span></span>

- <span data-ttu-id="5452b-126">Utwórz **AppSettings** klucza w aplikacji funkcji **ustawienia aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="5452b-126">Create an **AppSettings** key in your function app's **Application Settings**.</span></span>

 ![Tworzenie funkcji platformy Azure](./media/functions-how-to-use-sendgrid/functions-configure-sendgrid-api-key-app-settings.png)

## <a name="configure-sendgrid-output-bindings"></a><span data-ttu-id="5452b-128">Skonfiguruj SendGrid powiązania danych wyjściowych</span><span class="sxs-lookup"><span data-stu-id="5452b-128">Configure SendGrid output bindings</span></span>

<span data-ttu-id="5452b-129">SendGrid jest dostępna jako platformy Azure funkcja powiązania wyjściowego.</span><span class="sxs-lookup"><span data-stu-id="5452b-129">SendGrid is available as an Azure function output binding.</span></span> <span data-ttu-id="5452b-130">toocreate SendGrid powiązania wyjściowego:</span><span class="sxs-lookup"><span data-stu-id="5452b-130">toocreate a SendGrid output binding:</span></span>

1. <span data-ttu-id="5452b-131">Przejdź toohello **integracji** kartę funkcji hello w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="5452b-131">Go toohello **Integrate** tab of hello function in hello Azure portal.</span></span>
2. <span data-ttu-id="5452b-132">Kliknij przycisk **nowe dane wyjściowe** toocreate SendGrid powiązania wyjściowego.</span><span class="sxs-lookup"><span data-stu-id="5452b-132">Click **New Output** toocreate a SendGrid output binding.</span></span>
3. <span data-ttu-id="5452b-133">Wypełnij hello **klucz interfejsu API** i **Nazwa parametru komunikatu** właściwości.</span><span class="sxs-lookup"><span data-stu-id="5452b-133">Fill in hello **API Key** and **Message parameter name** properties.</span></span> <span data-ttu-id="5452b-134">Jeśli chcesz, możesz wprowadzić teraz hello inne właściwości lub ich zamiast tego kodu.</span><span class="sxs-lookup"><span data-stu-id="5452b-134">If you want, you can enter hello other properties now, or code them instead.</span></span> <span data-ttu-id="5452b-135">Te ustawienia mogą być używane jako domyślne.</span><span class="sxs-lookup"><span data-stu-id="5452b-135">These settings can be used as defaults.</span></span>

 ![Skonfiguruj SendGrid powiązania danych wyjściowych](./media/functions-how-to-use-sendgrid/functions-configure-sendgrid-output-bindings.png)

<span data-ttu-id="5452b-137">Dodawanie funkcji tooa powiązania tworzy plik o nazwie **function.json** w folderze z funkcji.</span><span class="sxs-lookup"><span data-stu-id="5452b-137">Adding a binding tooa function creates a file called **function.json** in your function's folder.</span></span> <span data-ttu-id="5452b-138">Ten plik zawiera wszystkie hello tych samych informacji, zobacz w hello Azure funkcja **integracji** karcie, ale w formacie Json formatowania.</span><span class="sxs-lookup"><span data-stu-id="5452b-138">This file contains all hello same information that you see in hello Azure function's **Integrate** tab, but in Json format.</span></span> <span data-ttu-id="5452b-139">Ustawienie hello **ApiKey**, **komunikat**, i **z** pola utworzenie hello następujące wpisy w hello **function.json** pliku:</span><span class="sxs-lookup"><span data-stu-id="5452b-139">Setting hello **ApiKey**, **message**, and **from** fields create hello following entries in hello **function.json** file:</span></span> 

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

<span data-ttu-id="5452b-140">Jeśli wolisz, użytkownik może modyfikować tego pliku samodzielnie bezpośrednio.</span><span class="sxs-lookup"><span data-stu-id="5452b-140">If you prefer, you may modify this file yourself directly.</span></span>

<span data-ttu-id="5452b-141">Teraz, gdy zostanie utworzony i skonfigurowany hello aplikacji funkcji i funkcji, można napisać hello kodu toosend wiadomości e-mail.</span><span class="sxs-lookup"><span data-stu-id="5452b-141">Now that you have created and configured hello Function App and function, you can write hello code toosend an email.</span></span>

## <a name="write-code-that-creates-and-sends-email"></a><span data-ttu-id="5452b-142">Pisanie kodu, który tworzy i wysyła wiadomości e-mail</span><span class="sxs-lookup"><span data-stu-id="5452b-142">Write code that creates and sends email</span></span>

<span data-ttu-id="5452b-143">Witaj SendGrid API zawiera wszystkie hello polecenia należy toocreate i wysłać wiadomość e-mail.</span><span class="sxs-lookup"><span data-stu-id="5452b-143">hello SendGrid API contains all hello commands you need toocreate and send an email.</span></span>  

- <span data-ttu-id="5452b-144">Zastąp kod hello w funkcji hello hello następującego kodu:</span><span class="sxs-lookup"><span data-stu-id="5452b-144">Replace hello code in hello function with hello following code:</span></span>

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
    // change tooemail of recipient
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

<span data-ttu-id="5452b-145">Powiadomienie hello pierwszy wiersz zawiera hello ```#r``` dyrektywy, który odwołuje się do zestawu SendGrid hello.</span><span class="sxs-lookup"><span data-stu-id="5452b-145">Notice hello first line contains hello ```#r``` directive that references hello SendGrid assembly.</span></span> <span data-ttu-id="5452b-146">Następnie można użyć ```using``` toomore instrukcji łatwo uzyskiwać dostęp do obiektów hello w tej przestrzeni nazw.</span><span class="sxs-lookup"><span data-stu-id="5452b-146">After that, you can use a ```using``` statement toomore easily access hello objects in that namespace.</span></span> <span data-ttu-id="5452b-147">W kodzie hello tworzenia wystąpień ```Mail```, ```Personalization```, i ```Content``` obiektów z hello SendGrid interfejsu API, tworzące hello poczty e-mail.</span><span class="sxs-lookup"><span data-stu-id="5452b-147">In hello code, create instances of ```Mail```, ```Personalization```, and ```Content``` objects from hello SendGrid API that compose hello email.</span></span> <span data-ttu-id="5452b-148">Po powrocie wiadomość hello SendGrid dostarcza ją.</span><span class="sxs-lookup"><span data-stu-id="5452b-148">When you return hello message, SendGrid delivers it.</span></span> 

<span data-ttu-id="5452b-149">Witaj sygnatura funkcji zawiera również dodatkową parametru typu out ```Mail``` o nazwie ```message```.</span><span class="sxs-lookup"><span data-stu-id="5452b-149">hello function's signature also contains an extra out parameter of type ```Mail``` named ```message```.</span></span> <span data-ttu-id="5452b-150">Zarówno wejściowa i wyjściowa express powiązań, same jako parametry funkcji w kodzie.</span><span class="sxs-lookup"><span data-stu-id="5452b-150">Both input and output bindings express themselves as function parameters in code.</span></span> 

2. <span data-ttu-id="5452b-151">Testowanie kodu, klikając **testu** i wprowadzić komunikat w hello **treść żądania** pola, a następnie klikając hello **Uruchom** przycisku.</span><span class="sxs-lookup"><span data-stu-id="5452b-151">Test your code by clicking **Test** and entering a message into hello **Request body** field, then clicking hello **Run** button.</span></span>

 ![Testowanie kodu](./media/functions-how-to-use-sendgrid/functions-develop-test-sendgrid.png)

3. <span data-ttu-id="5452b-153">Sprawdź, czy SendGrid wysyłane wiadomości e-mail hello tooverify wiadomości e-mail.</span><span class="sxs-lookup"><span data-stu-id="5452b-153">Check email tooverify that SendGrid sent hello email.</span></span> <span data-ttu-id="5452b-154">Należy go toohello adresu w kodzie hello z kroku 1 i zawierać wiadomości powitania od hello **treść żądania**.</span><span class="sxs-lookup"><span data-stu-id="5452b-154">It should go toohello address in hello code from step 1, and contain hello message from hello **Request body**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5452b-155">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="5452b-155">Next steps</span></span>
<span data-ttu-id="5452b-156">W tym artykule wykazała, jak toouse hello SendGrid usługa toocreate i wysyłania wiadomości e-mail.</span><span class="sxs-lookup"><span data-stu-id="5452b-156">This article has demonstrated how toouse hello SendGrid service toocreate and send email.</span></span> <span data-ttu-id="5452b-157">toolearn więcej informacji na temat przy użyciu usługi Azure Functions w aplikacjach, zobacz następujące tematy hello:</span><span class="sxs-lookup"><span data-stu-id="5452b-157">toolearn more about using Azure Functions in your apps, see hello following topics:</span></span> 

- <span data-ttu-id="5452b-158">[Najlepsze rozwiązania dotyczące usługi Azure Functions](functions-best-practices.md) wymieniono niektóre najlepszych praktyk toouse podczas tworzenia usługi Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="5452b-158">[Best practices for Azure Functions](functions-best-practices.md) Lists some best practices toouse when creating Azure Functions.</span></span>

- <span data-ttu-id="5452b-159">[Dokumentacja dla deweloperów usługi Azure funkcji](functions-reference.md) programisty dokumentacja dotycząca kodowania funkcji oraz definiowania wyzwalaczy i powiązań.</span><span class="sxs-lookup"><span data-stu-id="5452b-159">[Azure Functions developer reference](functions-reference.md) Programmer reference for coding functions and defining triggers and bindings.</span></span>

- <span data-ttu-id="5452b-160">[Testowanie usługi Azure Functions](functions-test-a-function.md) opis różnych narzędzi i technik testowania funkcji.</span><span class="sxs-lookup"><span data-stu-id="5452b-160">[Testing Azure Functions](functions-test-a-function.md) Describes various tools and techniques for testing your functions.</span></span>