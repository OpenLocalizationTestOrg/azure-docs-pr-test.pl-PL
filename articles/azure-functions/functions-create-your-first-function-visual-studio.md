---
title: "Tworzenie pierwszej funkcji na platformie Azure przy użyciu programu Visual Studio | Microsoft Docs"
description: "Tworzenie prostej funkcji wyzwalanej przez protokół HTTP i publikowanie jej na platformie Azure przy użyciu narzędzi usługi Azure Functions dla programu Visual Studio."
services: functions
documentationcenter: na
author: rachelappel
manager: erikre
editor: 
tags: 
keywords: "azure functions, funkcje, przetwarzanie zdarzeń, obliczenia, architektura bez serwera"
ms.assetid: 82db1177-2295-4e39-bd42-763f6082e796
ms.service: functions
ms.devlang: multiple
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 07/05/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 04370558725d76ffe83d8aaf5d16c88fd2803ba9
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="create-your-first-function-using-visual-studio"></a><span data-ttu-id="f29fa-104">Tworzenie pierwszej funkcji przy użyciu programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f29fa-104">Create your first function using Visual Studio</span></span>

<span data-ttu-id="f29fa-105">Usługa Azure Functions umożliwia wykonywanie kodu w środowisku bezserwerowym bez konieczności uprzedniego tworzenia maszyny wirtualnej lub publikowania aplikacji sieci Web.</span><span class="sxs-lookup"><span data-stu-id="f29fa-105">Azure Functions lets you execute your code in a serverless environment without having to first create a VM or publish a web application.</span></span>

<span data-ttu-id="f29fa-106">W tym temacie możesz dowiedzieć się, jak za pomocą narzędzi Visual Studio 2017 dla usługi Azure Functions tworzenie i testowanie lokalnie funkcję "hello world".</span><span class="sxs-lookup"><span data-stu-id="f29fa-106">In this topic, you learn how to use the Visual Studio 2017 tools for Azure Functions to create and test a "hello world" function locally.</span></span> <span data-ttu-id="f29fa-107">Kod funkcji zostanie następnie opublikowany na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="f29fa-107">You will then publish the function code to Azure.</span></span> <span data-ttu-id="f29fa-108">Te narzędzia są dostępne jako część obciążenia projektowania na platformie Azure w programie Visual Studio 2017 w wersji 15.3 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="f29fa-108">These tools are available as part of the Azure development workload in Visual Studio 2017 version 15.3, or a later version.</span></span>

![Kod usługi Azure Functions w projekcie programu Visual Studio](./media/functions-create-your-first-function-visual-studio/functions-vstools-intro.png)

## <a name="prerequisites"></a><span data-ttu-id="f29fa-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="f29fa-110">Prerequisites</span></span>

<span data-ttu-id="f29fa-111">Do ukończenia tego samouczka niezbędne jest zainstalowanie następujących składników:</span><span class="sxs-lookup"><span data-stu-id="f29fa-111">To complete this tutorial, install:</span></span>

* <span data-ttu-id="f29fa-112">[Program Visual Studio 2017 w wersji 15.3](https://www.visualstudio.com/vs/preview/) zawierający obciążenie **Programowanie na platformie Azure**.</span><span class="sxs-lookup"><span data-stu-id="f29fa-112">[Visual Studio 2017 version 15.3](https://www.visualstudio.com/vs/preview/), including the **Azure development** workload.</span></span>

    ![Instalowanie programu Visual Studio 2017 z obciążeniem Programowanie na platformie Azure](./media/functions-create-your-first-function-visual-studio/functions-vs-workloads.png)
    
    >[!NOTE]  
    <span data-ttu-id="f29fa-114">Po instalacji lub uaktualnienia do programu Visual Studio 2017 wersji 15 ustęp 3, może być również konieczne ręcznie zaktualizować narzędzi Visual Studio 2017 dla usługi Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="f29fa-114">After you install or upgrade to Visual Studio 2017 version 15.3, you might also need to manually update the Visual Studio 2017 tools for Azure Functions.</span></span> <span data-ttu-id="f29fa-115">Można aktualizować narzędzi z **narzędzia** menu w obszarze **rozszerzenia i aktualizacje...**   >  **Aktualizacje** > **programu Visual Studio Marketplace** > **sieci Web i usługę Azure Functions zadania narzędzia** > **aktualizacji**.</span><span class="sxs-lookup"><span data-stu-id="f29fa-115">You can update the tools from the **Tools** menu under **Extensions and Updates...** > **Updates** > **Visual Studio Marketplace** > **Azure Functions and Web Jobs Tools** > **Update**.</span></span> 

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)] 

## <a name="create-an-azure-functions-project-in-visual-studio"></a><span data-ttu-id="f29fa-116">Tworzenie projektu usługi Azure Functions w programie Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f29fa-116">Create an Azure Functions project in Visual Studio</span></span>

[!INCLUDE [Create a project using the Azure Functions template](../../includes/functions-vstools-create.md)]

<span data-ttu-id="f29fa-117">Po utworzeniu projektu można utworzyć pierwszą funkcję.</span><span class="sxs-lookup"><span data-stu-id="f29fa-117">Now that you have created the project, you can create your first function.</span></span>

## <a name="create-the-function"></a><span data-ttu-id="f29fa-118">Tworzenie funkcji</span><span class="sxs-lookup"><span data-stu-id="f29fa-118">Create the function</span></span>

1. <span data-ttu-id="f29fa-119">W **Eksploratorze rozwiązań** kliknij prawym przyciskiem myszy węzeł projektu i wybierz polecenie **Dodaj** > **Nowy element**.</span><span class="sxs-lookup"><span data-stu-id="f29fa-119">In **Solution Explorer**, right-click on your project node and select **Add** > **New Item**.</span></span> <span data-ttu-id="f29fa-120">Wybierz pozycję **Funkcja platformy Azure** i kliknij pozycję **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="f29fa-120">Select **Azure Function** and click **Add**.</span></span>

2. <span data-ttu-id="f29fa-121">Wybierz pozycję **HttpTrigger**, wpisz **nazwę funkcji**, wybierz opcję **Anonimowe** w polu **Prawa dostępu** i kliknij pozycję **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="f29fa-121">Select **HttpTrigger**, type a **Function Name**, select **Anonymous** for **Access Rights**, and click **Create**.</span></span> <span data-ttu-id="f29fa-122">Do utworzonej funkcji można uzyskać dostęp przez żądanie HTTP z dowolnego klienta.</span><span class="sxs-lookup"><span data-stu-id="f29fa-122">The function created is accessed by an HTTP request from any client.</span></span> 

    ![Tworzenie nowej funkcji platformy Azure](./media/functions-create-your-first-function-visual-studio/functions-vstools-add-new-function-2.png)

    <span data-ttu-id="f29fa-124">Plik kodu zostanie dodany do projektu, który zawiera klasę implementującą kodu funkcji.</span><span class="sxs-lookup"><span data-stu-id="f29fa-124">A code file is added to your project that contains a class that implements your function code.</span></span> <span data-ttu-id="f29fa-125">Ten kod opiera się na szablonie, który odbiera wartość nazwy i tłumiące echo go.</span><span class="sxs-lookup"><span data-stu-id="f29fa-125">This code is based on a template, which receives a name value and echos it back.</span></span> <span data-ttu-id="f29fa-126">**FunctionName** atrybut ustawia nazwę funkcji.</span><span class="sxs-lookup"><span data-stu-id="f29fa-126">The **FunctionName** attribute sets the name of your function.</span></span> <span data-ttu-id="f29fa-127">**HttpTrigger** atrybut wskazuje komunikat, który wyzwala funkcji.</span><span class="sxs-lookup"><span data-stu-id="f29fa-127">The **HttpTrigger** attribute indicates the message that triggers the function.</span></span> 

    ![Plik kodu — funkcja](./media/functions-create-your-first-function-visual-studio/functions-code-page.png)

<span data-ttu-id="f29fa-129">Po utworzeniu funkcji wyzwalanej przez protokół HTTP można ją przetestować na komputerze lokalnym.</span><span class="sxs-lookup"><span data-stu-id="f29fa-129">Now that you have created an HTTP-triggered function, you can test it on your local computer.</span></span>

## <a name="test-the-function-locally"></a><span data-ttu-id="f29fa-130">Lokalne testowanie funkcji</span><span class="sxs-lookup"><span data-stu-id="f29fa-130">Test the function locally</span></span>

<span data-ttu-id="f29fa-131">Podstawowe narzędzia usługi Azure Functions umożliwiają uruchamianie projektu usługi Azure Functions na lokalnym komputerze deweloperskim.</span><span class="sxs-lookup"><span data-stu-id="f29fa-131">Azure Functions Core Tools lets you run Azure Functions project on your local development computer.</span></span> <span data-ttu-id="f29fa-132">Monit o zainstalowanie tych narzędzi pojawia się przy pierwszym uruchomieniu funkcji w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f29fa-132">You are prompted to install these tools the first time you start a function from Visual Studio.</span></span>  

1. <span data-ttu-id="f29fa-133">Aby przetestować funkcję, naciśnij klawisz F5.</span><span class="sxs-lookup"><span data-stu-id="f29fa-133">To test your function, press F5.</span></span> <span data-ttu-id="f29fa-134">Po wyświetleniu monitu zaakceptuj żądanie programu Visual Studio dotyczące pobrania i zainstalowania podstawowych narzędzi usługi Azure Functions (CLI).</span><span class="sxs-lookup"><span data-stu-id="f29fa-134">If prompted, accept the request from Visual Studio to download and install Azure Functions Core (CLI) tools.</span></span>  <span data-ttu-id="f29fa-135">Może także być konieczne włączenie wyjątku zapory, aby umożliwić narzędziom obsługę żądań HTTP.</span><span class="sxs-lookup"><span data-stu-id="f29fa-135">You may also need to enable a firewall exception so that the tools can handle HTTP requests.</span></span>

2. <span data-ttu-id="f29fa-136">Skopiuj adres URL funkcji z danych wyjściowych środowiska uruchomieniowego usługi Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="f29fa-136">Copy the URL of your function from the Azure Functions runtime output.</span></span>  

    ![Lokalne środowisko uruchomieniowe platformy Azure](./media/functions-create-your-first-function-visual-studio/functions-vstools-f5.png)

3. <span data-ttu-id="f29fa-138">Wklej adres URL żądania HTTP w pasku adresu przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="f29fa-138">Paste the URL for the HTTP request into your browser's address bar.</span></span> <span data-ttu-id="f29fa-139">Dołącz ciąg zapytania `&name=<yourname>` do tego adresu URL i wykonaj żądanie.</span><span class="sxs-lookup"><span data-stu-id="f29fa-139">Append the query string `&name=<yourname>` to this URL and execute the request.</span></span> <span data-ttu-id="f29fa-140">Na poniższym obrazie przedstawiono wyświetloną w przeglądarce odpowiedź na lokalne żądanie GET zwróconą przez funkcję:</span><span class="sxs-lookup"><span data-stu-id="f29fa-140">The following shows the response in the browser to the local GET request returned by the function:</span></span> 

    ![Odpowiedź hosta localhost funkcji wyświetlona w przeglądarce](./media/functions-create-your-first-function-visual-studio/functions-test-local-browser.png)

4. <span data-ttu-id="f29fa-142">Aby zatrzymać debugowanie, kliknij przycisk **Zatrzymaj** na pasku narzędzi programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f29fa-142">To stop debugging, click the **Stop** button on the Visual Studio toolbar.</span></span>

<span data-ttu-id="f29fa-143">Gdy będziesz mieć pewność, że funkcja działa poprawnie na komputerze lokalnym, możesz opublikować projekt na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="f29fa-143">After you have verified that the function runs correctly on your local computer, it's time to publish the project to Azure.</span></span>

## <a name="publish-the-project-to-azure"></a><span data-ttu-id="f29fa-144">Publikowanie projektu na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="f29fa-144">Publish the project to Azure</span></span>

<span data-ttu-id="f29fa-145">Aby opublikować projekt, musisz mieć aplikację funkcji w swojej subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="f29fa-145">You must have a function app in your Azure subscription before you can publish your project.</span></span> <span data-ttu-id="f29fa-146">Aplikację funkcji możesz utworzyć bezpośrednio w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f29fa-146">You can create a function app right from Visual Studio.</span></span>

[!INCLUDE [Publish the project to Azure](../../includes/functions-vstools-publish.md)]

## <a name="test-your-function-in-azure"></a><span data-ttu-id="f29fa-147">Testowanie funkcji na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="f29fa-147">Test your function in Azure</span></span>

1. <span data-ttu-id="f29fa-148">Skopiuj podstawowy adres URL aplikacji funkcji ze strony profilu publikowania.</span><span class="sxs-lookup"><span data-stu-id="f29fa-148">Copy the base URL of the function app from the Publish profile page.</span></span> <span data-ttu-id="f29fa-149">Część `localhost:port` adresu URL używaną podczas lokalnego testowania funkcji zastąp nowym podstawowym adresem URL.</span><span class="sxs-lookup"><span data-stu-id="f29fa-149">Replace the `localhost:port` portion of the URL you used when testing the function locally with the new base URL.</span></span> <span data-ttu-id="f29fa-150">Tak jak poprzednio dołącz ciąg zapytania `&name=<yourname>` do tego adresu URL i wykonaj żądanie.</span><span class="sxs-lookup"><span data-stu-id="f29fa-150">As before, make sure to append the query string `&name=<yourname>` to this URL and execute the request.</span></span>

    <span data-ttu-id="f29fa-151">Adres URL, który wywołuje funkcję wyzwalaną przez protokół HTTP, wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="f29fa-151">The URL that calls your HTTP triggered function looks like this:</span></span>

        http://<functionappname>.azurewebsites.net/api/<functionname>?name=<yourname> 

2. <span data-ttu-id="f29fa-152">Wklej nowy adres URL żądania HTTP na pasku adresu przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="f29fa-152">Paste this new URL for the HTTP request into your browser's address bar.</span></span> <span data-ttu-id="f29fa-153">Na poniższym obrazie przedstawiono wyświetloną w przeglądarce odpowiedź na zdalne żądanie GET zwróconą przez funkcję:</span><span class="sxs-lookup"><span data-stu-id="f29fa-153">The following shows the response in the browser to the remote GET request returned by the function:</span></span> 

    ![Odpowiedź funkcji wyświetlona w przeglądarce](./media/functions-create-your-first-function-visual-studio/functions-test-remote-browser.png)
 
## <a name="next-steps"></a><span data-ttu-id="f29fa-155">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f29fa-155">Next steps</span></span>

<span data-ttu-id="f29fa-156">W programie Visual Studio utworzono aplikację funkcji C# z prostą funkcją wyzwalaną przez protokół HTTP.</span><span class="sxs-lookup"><span data-stu-id="f29fa-156">You have used Visual Studio to create a C# function app with a simple HTTP triggered function.</span></span> 

+ <span data-ttu-id="f29fa-157">Aby dowiedzieć się, jak skonfigurować projekt w celu obsługi innych typów wyzwalaczy i powiązań, zobacz sekcję [Configure the project for local development (Konfigurowanie projektu na potrzeby lokalnego projektowania)](functions-develop-vs.md#configure-the-project-for-local-development) w temacie [Azure Functions Tools for Visual Studio (Narzędzia usługi Azure Functions dla programu Visual Studio)](functions-develop-vs.md).</span><span class="sxs-lookup"><span data-stu-id="f29fa-157">To learn how to configure your project to support other types of triggers and bindings, see the [Configure the project for local development](functions-develop-vs.md#configure-the-project-for-local-development) section in [Azure Functions Tools for Visual Studio](functions-develop-vs.md).</span></span>
+ <span data-ttu-id="f29fa-158">Aby dowiedzieć się więcej na temat lokalnego testowania i debugowania przy użyciu podstawowych narzędzi usługi Azure Functions, zobacz [Code and test Azure Functions locally (Kodowanie i lokalne testowanie usługi Azure Functions)](functions-run-local.md).</span><span class="sxs-lookup"><span data-stu-id="f29fa-158">To learn more about local testing and debugging using the Azure Functions Core Tools, see [Code and test Azure Functions locally](functions-run-local.md).</span></span> 
+ <span data-ttu-id="f29fa-159">Aby dowiedzieć się więcej o projektowaniu funkcji jako bibliotek klasy .NET, zobacz [Korzystanie z bibliotek klasy .NET w usłudze Azure Functions](functions-dotnet-class-library.md).</span><span class="sxs-lookup"><span data-stu-id="f29fa-159">To learn more about developing functions as .NET class libraries, see [Using .NET class libraries with Azure Functions](functions-dotnet-class-library.md).</span></span> 

