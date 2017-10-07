---
title: "aaaCreate pierwszej funkcji platformy Azure przy użyciu programu Visual Studio | Dokumentacja firmy Microsoft"
description: "Tworzenie i publikowanie proste tooAzure funkcja wyzwalana HTTP przy użyciu narzędzi funkcji Azure dla programu Visual Studio."
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
ms.openlocfilehash: 851e5b98dcc2da00334620896a0ea31f566589f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-function-using-visual-studio"></a><span data-ttu-id="7c0ad-104">Tworzenie pierwszej funkcji przy użyciu programu Visual Studio</span><span class="sxs-lookup"><span data-stu-id="7c0ad-104">Create your first function using Visual Studio</span></span>

<span data-ttu-id="7c0ad-105">Środowisko Azure Functions umożliwia wykonywanie kodu w środowisku bez serwera bez konieczności toofirst tworzenie maszyny Wirtualnej lub opublikować aplikację sieci web.</span><span class="sxs-lookup"><span data-stu-id="7c0ad-105">Azure Functions lets you execute your code in a serverless environment without having toofirst create a VM or publish a web application.</span></span>

<span data-ttu-id="7c0ad-106">W tym temacie dowiesz się, jak toouse hello 2017 usługi Visual Studio tools dla usługi Azure Functions toocreate i przetestować funkcję "hello world", który jest lokalnie.</span><span class="sxs-lookup"><span data-stu-id="7c0ad-106">In this topic, you learn how toouse hello Visual Studio 2017 tools for Azure Functions toocreate and test a "hello world" function locally.</span></span> <span data-ttu-id="7c0ad-107">Następnie będzie publikować tooAzure kodu funkcji hello.</span><span class="sxs-lookup"><span data-stu-id="7c0ad-107">You will then publish hello function code tooAzure.</span></span> <span data-ttu-id="7c0ad-108">Te narzędzia są dostępne jako część hello obciążenia Azure Programowanie w Visual Studio 2017 wersji 15 ustęp 3 lub nowszym.</span><span class="sxs-lookup"><span data-stu-id="7c0ad-108">These tools are available as part of hello Azure development workload in Visual Studio 2017 version 15.3, or a later version.</span></span>

![Kod usługi Azure Functions w projekcie programu Visual Studio](./media/functions-create-your-first-function-visual-studio/functions-vstools-intro.png)

## <a name="prerequisites"></a><span data-ttu-id="7c0ad-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="7c0ad-110">Prerequisites</span></span>

<span data-ttu-id="7c0ad-111">toocomplete tego samouczka, instalacji:</span><span class="sxs-lookup"><span data-stu-id="7c0ad-111">toocomplete this tutorial, install:</span></span>

* <span data-ttu-id="7c0ad-112">[Visual Studio 2017 wersji 15 ustęp 3](https://www.visualstudio.com/vs/preview/), łącznie z hello **Azure programowanie** obciążenia.</span><span class="sxs-lookup"><span data-stu-id="7c0ad-112">[Visual Studio 2017 version 15.3](https://www.visualstudio.com/vs/preview/), including hello **Azure development** workload.</span></span>

    ![Instalowanie programu Visual Studio 2017 przy użyciu hello Azure programowanie obciążenia](./media/functions-create-your-first-function-visual-studio/functions-vs-workloads.png)
    
    >[!NOTE]  
    <span data-ttu-id="7c0ad-114">Po instalacji lub uaktualnienia tooVisual Studio 2017 wersji 15 ustęp 3, może być również konieczne toomanually aktualizacji hello 2017 usługi Visual Studio tools dla usługi Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="7c0ad-114">After you install or upgrade tooVisual Studio 2017 version 15.3, you might also need toomanually update hello Visual Studio 2017 tools for Azure Functions.</span></span> <span data-ttu-id="7c0ad-115">Można aktualizować hello narzędzi z hello **narzędzia** menu w obszarze **rozszerzenia i aktualizacje...**   >  **Aktualizacje** > **programu Visual Studio Marketplace** > **sieci Web i usługę Azure Functions zadania narzędzia**  >  **Aktualizacji**.</span><span class="sxs-lookup"><span data-stu-id="7c0ad-115">You can update hello tools from hello **Tools** menu under **Extensions and Updates...** > **Updates** > **Visual Studio Marketplace** > **Azure Functions and Web Jobs Tools** > **Update**.</span></span> 

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)] 

## <a name="create-an-azure-functions-project-in-visual-studio"></a><span data-ttu-id="7c0ad-116">Tworzenie projektu usługi Azure Functions w programie Visual Studio</span><span class="sxs-lookup"><span data-stu-id="7c0ad-116">Create an Azure Functions project in Visual Studio</span></span>

[!INCLUDE [Create a project using hello Azure Functions template](../../includes/functions-vstools-create.md)]

<span data-ttu-id="7c0ad-117">Teraz, po utworzeniu projektu hello, można utworzyć swoją pierwszą funkcję.</span><span class="sxs-lookup"><span data-stu-id="7c0ad-117">Now that you have created hello project, you can create your first function.</span></span>

## <a name="create-hello-function"></a><span data-ttu-id="7c0ad-118">Utwórz hello — funkcja</span><span class="sxs-lookup"><span data-stu-id="7c0ad-118">Create hello function</span></span>

1. <span data-ttu-id="7c0ad-119">W **Eksploratorze rozwiązań** kliknij prawym przyciskiem myszy węzeł projektu i wybierz polecenie **Dodaj** > **Nowy element**.</span><span class="sxs-lookup"><span data-stu-id="7c0ad-119">In **Solution Explorer**, right-click on your project node and select **Add** > **New Item**.</span></span> <span data-ttu-id="7c0ad-120">Wybierz pozycję **Funkcja platformy Azure** i kliknij pozycję **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="7c0ad-120">Select **Azure Function** and click **Add**.</span></span>

2. <span data-ttu-id="7c0ad-121">Wybierz pozycję **HttpTrigger**, wpisz **nazwę funkcji**, wybierz opcję **Anonimowe** w polu **Prawa dostępu** i kliknij pozycję **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="7c0ad-121">Select **HttpTrigger**, type a **Function Name**, select **Anonymous** for **Access Rights**, and click **Create**.</span></span> <span data-ttu-id="7c0ad-122">Funkcja Hello tworzone jest dostępny przez żądania HTTP za pomocą dowolnego klienta.</span><span class="sxs-lookup"><span data-stu-id="7c0ad-122">hello function created is accessed by an HTTP request from any client.</span></span> 

    ![Tworzenie nowej funkcji platformy Azure](./media/functions-create-your-first-function-visual-studio/functions-vstools-add-new-function-2.png)

    <span data-ttu-id="7c0ad-124">Projekt tooyour, który zawiera klasę implementującą kodu funkcji zostanie dodany plik kodu.</span><span class="sxs-lookup"><span data-stu-id="7c0ad-124">A code file is added tooyour project that contains a class that implements your function code.</span></span> <span data-ttu-id="7c0ad-125">Ten kod opiera się na szablonie, który odbiera wartość nazwy i tłumiące echo go.</span><span class="sxs-lookup"><span data-stu-id="7c0ad-125">This code is based on a template, which receives a name value and echos it back.</span></span> <span data-ttu-id="7c0ad-126">Witaj **FunctionName** atrybut ustawia hello nazwę funkcji.</span><span class="sxs-lookup"><span data-stu-id="7c0ad-126">hello **FunctionName** attribute sets hello name of your function.</span></span> <span data-ttu-id="7c0ad-127">Witaj **HttpTrigger** atrybut wskazuje wiadomość hello wyzwala hello funkcji.</span><span class="sxs-lookup"><span data-stu-id="7c0ad-127">hello **HttpTrigger** attribute indicates hello message that triggers hello function.</span></span> 

    ![Plik kodu — funkcja](./media/functions-create-your-first-function-visual-studio/functions-code-page.png)

<span data-ttu-id="7c0ad-129">Po utworzeniu funkcji wyzwalanej przez protokół HTTP można ją przetestować na komputerze lokalnym.</span><span class="sxs-lookup"><span data-stu-id="7c0ad-129">Now that you have created an HTTP-triggered function, you can test it on your local computer.</span></span>

## <a name="test-hello-function-locally"></a><span data-ttu-id="7c0ad-130">Testowanie funkcji hello lokalnie</span><span class="sxs-lookup"><span data-stu-id="7c0ad-130">Test hello function locally</span></span>

<span data-ttu-id="7c0ad-131">Podstawowe narzędzia usługi Azure Functions umożliwiają uruchamianie projektu usługi Azure Functions na lokalnym komputerze deweloperskim.</span><span class="sxs-lookup"><span data-stu-id="7c0ad-131">Azure Functions Core Tools lets you run Azure Functions project on your local development computer.</span></span> <span data-ttu-id="7c0ad-132">Jesteś zostanie wyświetlony monit o tooinstall, które te narzędzia hello podczas pierwszego uruchomienia funkcji w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7c0ad-132">You are prompted tooinstall these tools hello first time you start a function from Visual Studio.</span></span>  

1. <span data-ttu-id="7c0ad-133">tootest funkcji, naciśnij klawisz F5.</span><span class="sxs-lookup"><span data-stu-id="7c0ad-133">tootest your function, press F5.</span></span> <span data-ttu-id="7c0ad-134">Po wyświetleniu monitu Zaakceptuj Żądanie hello z toodownload programu Visual Studio i zainstalować narzędzia do podstawowych funkcji platformy Azure (CLI).</span><span class="sxs-lookup"><span data-stu-id="7c0ad-134">If prompted, accept hello request from Visual Studio toodownload and install Azure Functions Core (CLI) tools.</span></span>  <span data-ttu-id="7c0ad-135">Możesz także tooenable wyjątek zapory, aby narzędzia hello mogły obsługiwać żądania HTTP.</span><span class="sxs-lookup"><span data-stu-id="7c0ad-135">You may also need tooenable a firewall exception so that hello tools can handle HTTP requests.</span></span>

2. <span data-ttu-id="7c0ad-136">Adres URL hello kopiowania funkcji ze środowiska uruchomieniowego usługi Azure Functions hello wyjściowej.</span><span class="sxs-lookup"><span data-stu-id="7c0ad-136">Copy hello URL of your function from hello Azure Functions runtime output.</span></span>  

    ![Lokalne środowisko uruchomieniowe platformy Azure](./media/functions-create-your-first-function-visual-studio/functions-vstools-f5.png)

3. <span data-ttu-id="7c0ad-138">Wklej adres URL żądania HTTP hello hello do paska adresu przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="7c0ad-138">Paste hello URL for hello HTTP request into your browser's address bar.</span></span> <span data-ttu-id="7c0ad-139">Dołącz ciągu zapytania hello `&name=<yourname>` toothis adresu URL i wykonać hello żądania.</span><span class="sxs-lookup"><span data-stu-id="7c0ad-139">Append hello query string `&name=<yourname>` toothis URL and execute hello request.</span></span> <span data-ttu-id="7c0ad-140">Hello poniżej przedstawiono odpowiedzi hello w hello przeglądarki toohello lokalne żądania GET zwracane przez funkcję hello:</span><span class="sxs-lookup"><span data-stu-id="7c0ad-140">hello following shows hello response in hello browser toohello local GET request returned by hello function:</span></span> 

    ![Funkcja localhost odpowiedzi w przeglądarce hello](./media/functions-create-your-first-function-visual-studio/functions-test-local-browser.png)

4. <span data-ttu-id="7c0ad-142">toostop debugowanie, kliknij przycisk hello **zatrzymać** przycisk na powitania narzędzi Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7c0ad-142">toostop debugging, click hello **Stop** button on hello Visual Studio toolbar.</span></span>

<span data-ttu-id="7c0ad-143">Po sprawdzeniu, czy funkcja hello działa poprawnie na komputerze lokalnym, jest tooAzure projektu hello toopublish czasu.</span><span class="sxs-lookup"><span data-stu-id="7c0ad-143">After you have verified that hello function runs correctly on your local computer, it's time toopublish hello project tooAzure.</span></span>

## <a name="publish-hello-project-tooazure"></a><span data-ttu-id="7c0ad-144">Publikowanie hello tooAzure projektu</span><span class="sxs-lookup"><span data-stu-id="7c0ad-144">Publish hello project tooAzure</span></span>

<span data-ttu-id="7c0ad-145">Aby opublikować projekt, musisz mieć aplikację funkcji w swojej subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="7c0ad-145">You must have a function app in your Azure subscription before you can publish your project.</span></span> <span data-ttu-id="7c0ad-146">Aplikację funkcji możesz utworzyć bezpośrednio w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7c0ad-146">You can create a function app right from Visual Studio.</span></span>

[!INCLUDE [Publish hello project tooAzure](../../includes/functions-vstools-publish.md)]

## <a name="test-your-function-in-azure"></a><span data-ttu-id="7c0ad-147">Testowanie funkcji na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="7c0ad-147">Test your function in Azure</span></span>

1. <span data-ttu-id="7c0ad-148">Skopiuj hello podstawowy adres URL aplikacji funkcji hello ze strony profilu publikowania hello.</span><span class="sxs-lookup"><span data-stu-id="7c0ad-148">Copy hello base URL of hello function app from hello Publish profile page.</span></span> <span data-ttu-id="7c0ad-149">Zastąp hello `localhost:port` część adresu URL hello używane podczas testowania funkcji hello lokalnie z hello nowego podstawowego adresu URL.</span><span class="sxs-lookup"><span data-stu-id="7c0ad-149">Replace hello `localhost:port` portion of hello URL you used when testing hello function locally with hello new base URL.</span></span> <span data-ttu-id="7c0ad-150">Jak wcześniej, upewnij się, że ciąg zapytania hello tooappend `&name=<yourname>` toothis adresu URL i wykonać hello żądania.</span><span class="sxs-lookup"><span data-stu-id="7c0ad-150">As before, make sure tooappend hello query string `&name=<yourname>` toothis URL and execute hello request.</span></span>

    <span data-ttu-id="7c0ad-151">adres URL Hello, która wywołuje HTTP wyzwalane funkcja wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="7c0ad-151">hello URL that calls your HTTP triggered function looks like this:</span></span>

        http://<functionappname>.azurewebsites.net/api/<functionname>?name=<yourname> 

2. <span data-ttu-id="7c0ad-152">Wklej nowy adres URL dla żądania hello HTTP w pasku adresu przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="7c0ad-152">Paste this new URL for hello HTTP request into your browser's address bar.</span></span> <span data-ttu-id="7c0ad-153">Hello poniżej przedstawiono odpowiedzi hello w hello przeglądarki toohello zdalnego żądania GET zwracane przez funkcję hello:</span><span class="sxs-lookup"><span data-stu-id="7c0ad-153">hello following shows hello response in hello browser toohello remote GET request returned by hello function:</span></span> 

    ![Funkcja odpowiedzi w przeglądarce hello](./media/functions-create-your-first-function-visual-studio/functions-test-remote-browser.png)
 
## <a name="next-steps"></a><span data-ttu-id="7c0ad-155">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="7c0ad-155">Next steps</span></span>

<span data-ttu-id="7c0ad-156">Użyto aplikacji funkcji toocreate C# dla programu Visual Studio przy użyciu prostych funkcji HTTP wyzwolone.</span><span class="sxs-lookup"><span data-stu-id="7c0ad-156">You have used Visual Studio toocreate a C# function app with a simple HTTP triggered function.</span></span> 

+ <span data-ttu-id="7c0ad-157">toolearn jak tooconfigure toosupport Twojego projektu inne rodzaje wyzwalaczy i powiązań, zobacz hello [Konfiguruj hello projektu dla rozwoju lokalnych](functions-develop-vs.md#configure-the-project-for-local-development) sekcji [narzędzi funkcji Azure dla programu Visual Studio](functions-develop-vs.md).</span><span class="sxs-lookup"><span data-stu-id="7c0ad-157">toolearn how tooconfigure your project toosupport other types of triggers and bindings, see hello [Configure hello project for local development](functions-develop-vs.md#configure-the-project-for-local-development) section in [Azure Functions Tools for Visual Studio](functions-develop-vs.md).</span></span>
+ <span data-ttu-id="7c0ad-158">toolearn więcej informacji na temat lokalnych testowanie i debugowanie przy użyciu hello Azure funkcje podstawowe narzędzia, zobacz [kodu oraz testów usługi Azure Functions lokalnie](functions-run-local.md).</span><span class="sxs-lookup"><span data-stu-id="7c0ad-158">toolearn more about local testing and debugging using hello Azure Functions Core Tools, see [Code and test Azure Functions locally](functions-run-local.md).</span></span> 
+ <span data-ttu-id="7c0ad-159">toolearn więcej informacji na temat tworzenia funkcji jako biblioteki klas .NET, zobacz [.NET przy użyciu biblioteki klas z usługi Azure Functions](functions-dotnet-class-library.md).</span><span class="sxs-lookup"><span data-stu-id="7c0ad-159">toolearn more about developing functions as .NET class libraries, see [Using .NET class libraries with Azure Functions](functions-dotnet-class-library.md).</span></span> 

