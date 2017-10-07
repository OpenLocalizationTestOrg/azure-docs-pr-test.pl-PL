---
title: "aaaDevelop funkcji platformy Azure przy użyciu programu Visual Studio | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak usługi Azure Functions toodevelop i testowania przy użyciu narzędzi funkcji Azure dla programu Visual Studio 2017 r."
services: functions
documentationcenter: .net
author: ggailey777
manager: erikre
editor: 
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: dotnet
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: glenga
ms.openlocfilehash: c9baf882bf58068cb9a8930bea337fe51b2a77ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-tools-for-visual-studio"></a><span data-ttu-id="5d59b-103">Środowisko Azure Functions Tools for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="5d59b-103">Azure Functions Tools for Visual Studio</span></span>  

<span data-ttu-id="5d59b-104">Narzędzi funkcji platformy Azure dla programu Visual Studio 2017 to rozszerzenie dla programu Visual Studio, który pozwala tworzyć, testować i wdrażać tooAzure funkcje C#.</span><span class="sxs-lookup"><span data-stu-id="5d59b-104">Azure Functions Tools for Visual Studio 2017 is an extension for Visual Studio that lets you develop, test, and deploy C# functions tooAzure.</span></span> <span data-ttu-id="5d59b-105">Jeśli jest to usprawnić pierwszej funkcji platformy Azure, możesz dowiedzieć się więcej, zobacz [tooAzure wprowadzenie funkcji](functions-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5d59b-105">If this is your first experience with Azure Functions, you can learn more at [An introduction tooAzure Functions](functions-overview.md).</span></span>

<span data-ttu-id="5d59b-106">Witaj narzędzi funkcji Azure udostępnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="5d59b-106">hello Azure Functions Tools provides hello following benefits:</span></span> 

* <span data-ttu-id="5d59b-107">Edytowania, tworzenia i uruchamiania funkcji na komputerze deweloperskim lokalnego.</span><span class="sxs-lookup"><span data-stu-id="5d59b-107">Edit, build, and run functions on your local development computer.</span></span> 
* <span data-ttu-id="5d59b-108">Publikowanie z usługi Azure Functions projektu bezpośrednio tooAzure.</span><span class="sxs-lookup"><span data-stu-id="5d59b-108">Publish your Azure Functions project directly tooAzure.</span></span> 
* <span data-ttu-id="5d59b-109">Użyj powiązania funkcji toodeclare atrybuty zadań Webjob bezpośrednio w hello kodu C# zamiast utrzymywania osobnych function.json dla powiązania definicje.</span><span class="sxs-lookup"><span data-stu-id="5d59b-109">Use WebJobs attributes toodeclare function bindings directly in hello C# code instead of maintaining a separate function.json for binding definitions.</span></span>
* <span data-ttu-id="5d59b-110">Tworzenie i wdrażanie wstępnie skompilowanym funkcje C#.</span><span class="sxs-lookup"><span data-stu-id="5d59b-110">Develop and deploy pre-compiled C# functions.</span></span> <span data-ttu-id="5d59b-111">Wstępnie skompilowane funkcje umożliwiać wydajności zimnego lepiej niż C# opartych na skryptach funkcji.</span><span class="sxs-lookup"><span data-stu-id="5d59b-111">Pre-complied functions provide a better cold-start performance than C# script-based functions.</span></span> 
* <span data-ttu-id="5d59b-112">Kod funkcji w języku C# przy jednoczesnym zachowaniu wszystkich zalet hello tworzenia Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5d59b-112">Code your functions in C# while having all of hello benefits of Visual Studio development.</span></span> 

<span data-ttu-id="5d59b-113">W tym temacie pokazano, jak toouse hello Azure funkcje narzędzi dla programu Visual Studio 2017 toodevelop funkcji w języku C#.</span><span class="sxs-lookup"><span data-stu-id="5d59b-113">This topic shows you how toouse hello Azure Functions Tools for Visual Studio 2017 toodevelop your functions in C#.</span></span> <span data-ttu-id="5d59b-114">Możesz także dowiedzieć się, jak toopublish tooAzure Twojego projektu jako zestaw .NET.</span><span class="sxs-lookup"><span data-stu-id="5d59b-114">You also learn how toopublish your project tooAzure as a .NET assembly.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5d59b-115">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="5d59b-115">Prerequisites</span></span>

<span data-ttu-id="5d59b-116">Narzędzia funkcji platformy Azure jest uwzględniona w hello Azure programowanie obciążenie [programu Visual Studio 2017 wersji 15 ustęp 3](https://www.visualstudio.com/vs/), lub jego nowsza wersja.</span><span class="sxs-lookup"><span data-stu-id="5d59b-116">Azure Functions Tools is included in hello Azure development workload of [Visual Studio 2017 version 15.3](https://www.visualstudio.com/vs/), or a later version.</span></span> <span data-ttu-id="5d59b-117">Upewnij się, że zawierają hello **Azure programowanie** obciążenia w instalacji programu Visual Studio 2017 wersji 15 ustęp 3:</span><span class="sxs-lookup"><span data-stu-id="5d59b-117">Make sure you include hello **Azure development** workload in your Visual Studio 2017 version 15.3 installation:</span></span>

![Instalowanie programu Visual Studio 2017 przy użyciu hello Azure programowanie obciążenia](./media/functions-create-your-first-function-visual-studio/functions-vs-workloads.png)

<span data-ttu-id="5d59b-119">toocreate i wdrażania funkcji, należy również:</span><span class="sxs-lookup"><span data-stu-id="5d59b-119">toocreate and deploy functions, you also need:</span></span>

* <span data-ttu-id="5d59b-120">Aktywna subskrypcja platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="5d59b-120">An active Azure subscription.</span></span> <span data-ttu-id="5d59b-121">Jeśli nie masz subskrypcji platformy Azure, [wolnego konta](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) są dostępne.</span><span class="sxs-lookup"><span data-stu-id="5d59b-121">If you don't have an Azure subscription, [free accounts](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) are available.</span></span>

* <span data-ttu-id="5d59b-122">Konto magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="5d59b-122">An Azure Storage account.</span></span> <span data-ttu-id="5d59b-123">toocreate konta magazynu, zobacz [Utwórz konto magazynu](../storage/common/storage-create-storage-account.md#create-a-storage-account).</span><span class="sxs-lookup"><span data-stu-id="5d59b-123">toocreate a storage account, see [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account).</span></span>  
## <a name="create-an-azure-functions-project"></a><span data-ttu-id="5d59b-124">Tworzenie projektu usługi Azure Functions</span><span class="sxs-lookup"><span data-stu-id="5d59b-124">Create an Azure Functions project</span></span> 

[!INCLUDE [Create a project using hello Azure Functions](../../includes/functions-vstools-create.md)]


## <a name="configure-hello-project-for-local-development"></a><span data-ttu-id="5d59b-125">Konfigurowanie hello projektu dla rozwoju lokalnych</span><span class="sxs-lookup"><span data-stu-id="5d59b-125">Configure hello project for local development</span></span>

<span data-ttu-id="5d59b-126">Podczas tworzenia nowego projektu przy użyciu szablonu usługi Azure Functions hello otrzymasz pusty C# projekt zawierający hello następujące pliki:</span><span class="sxs-lookup"><span data-stu-id="5d59b-126">When you create a new project using hello Azure Functions template, you get an empty C# project that contains hello following files:</span></span>

* <span data-ttu-id="5d59b-127">**Host.JSON**: umożliwia skonfigurowanie hello funkcji hosta.</span><span class="sxs-lookup"><span data-stu-id="5d59b-127">**host.json**: Lets you configure hello Functions host.</span></span> <span data-ttu-id="5d59b-128">Te ustawienia dotyczą zarówno podczas uruchamiania lokalnie i na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="5d59b-128">These settings apply both when running locally and in Azure.</span></span> <span data-ttu-id="5d59b-129">Aby uzyskać więcej informacji, zobacz [host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json) artykule.</span><span class="sxs-lookup"><span data-stu-id="5d59b-129">For more information, see [host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json) reference article.</span></span>
    
* <span data-ttu-id="5d59b-130">**Local.Settings.JSON**: przechowuje ustawienia używane podczas uruchamiania lokalnego funkcji.</span><span class="sxs-lookup"><span data-stu-id="5d59b-130">**local.settings.json**: Maintains settings used when running functions locally.</span></span> <span data-ttu-id="5d59b-131">Te ustawienia nie są używane przez platformę Azure, są one używane przez hello [Azure funkcje podstawowe narzędzia](functions-run-local.md).</span><span class="sxs-lookup"><span data-stu-id="5d59b-131">These settings are not used by Azure, they are used by hello [Azure Functions Core Tools](functions-run-local.md).</span></span> <span data-ttu-id="5d59b-132">Użyj tego ustawienia toospecify plików, takie jak tooother ciągów połączenia Azure usługi.</span><span class="sxs-lookup"><span data-stu-id="5d59b-132">Use this file toospecify settings, such as connection strings tooother Azure services.</span></span> <span data-ttu-id="5d59b-133">Dodaj nowy toohello klucza **wartości** tablicy dla każdego połączenia wymagany przez funkcje w projekcie.</span><span class="sxs-lookup"><span data-stu-id="5d59b-133">Add a new key toohello **Values** array for each connection required by functions in your project.</span></span> <span data-ttu-id="5d59b-134">Aby uzyskać więcej informacji, zobacz [pliku ustawień lokalnych](functions-run-local.md#local-settings-file) w hello Azure funkcje podstawowe narzędzia tematu.</span><span class="sxs-lookup"><span data-stu-id="5d59b-134">For more information, see [Local settings file](functions-run-local.md#local-settings-file) in hello Azure Functions Core Tools topic.</span></span>

<span data-ttu-id="5d59b-135">środowisko uruchomieniowe Functions Hello wewnętrznie używa konta usługi Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="5d59b-135">hello Functions runtime uses an Azure Storage account internally.</span></span> <span data-ttu-id="5d59b-136">W przypadku wyzwolenia wszystkich typów innych niż HTTP i elementów webhook, należy skonfigurować hello **Values.AzureWebJobsStorage** klucza tooa parametry połączenia w prawidłowe konto magazynu Azure.</span><span class="sxs-lookup"><span data-stu-id="5d59b-136">For all trigger types other than HTTP and webhooks, you must set hello **Values.AzureWebJobsStorage** key tooa valid Azure Storage account connection string.</span></span>

[!INCLUDE [Note toonot use local storage](../../includes/functions-local-settings-note.md)]

 <span data-ttu-id="5d59b-137">Parametry połączenia tooset hello magazynu konta:</span><span class="sxs-lookup"><span data-stu-id="5d59b-137">tooset hello storage account connection string:</span></span>

1. <span data-ttu-id="5d59b-138">W programie Visual Studio Otwórz **Eksplorator chmury**, rozwiń węzeł **konta magazynu** > **Twoje konto magazynu**, a następnie wybierz pozycję **właściwości**i kopiowania hello **parametry połączenia podstawowej** wartość.</span><span class="sxs-lookup"><span data-stu-id="5d59b-138">In Visual Studio, open **Cloud Explorer**, expand **Storage Account** > **Your Storage Account**, then select **Properties** and copy hello **Primary Connection String** value.</span></span>   

2. <span data-ttu-id="5d59b-139">W projekcie, otwórz plik projektu local.settings.json hello i ustaw wartość hello hello **AzureWebJobsStorage** klucza toohello parametry połączenia skopiowane.</span><span class="sxs-lookup"><span data-stu-id="5d59b-139">In your project, open hello local.settings.json project file and set hello value of hello **AzureWebJobsStorage** key toohello connection string you copied.</span></span>

3. <span data-ttu-id="5d59b-140">Powtórz hello poprzedniego kroku tooadd unikatowy kluczy toohello **wartości** tablicy dla innych połączeń wymagany przez funkcje.</span><span class="sxs-lookup"><span data-stu-id="5d59b-140">Repeat hello previous step tooadd unique keys toohello **Values** array for any other connections required by your functions.</span></span>  

## <a name="create-a-function"></a><span data-ttu-id="5d59b-141">Tworzenie funkcji</span><span class="sxs-lookup"><span data-stu-id="5d59b-141">Create a function</span></span>

<span data-ttu-id="5d59b-142">W przypadku funkcji wstępnie skompilowanym powiązania hello używane przez funkcję hello są definiowane przez stosowanie atrybutów w kodzie hello.</span><span class="sxs-lookup"><span data-stu-id="5d59b-142">In pre-compiled functions, hello bindings used by hello function are defined by applying attributes in hello code.</span></span> <span data-ttu-id="5d59b-143">Korzystając z toocreate narzędzi funkcji Azure hello funkcji z szablonów hello pod warunkiem, te atrybuty są stosowane dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="5d59b-143">When you use hello Azure Functions Tools toocreate your functions from hello provided templates, these attributes are applied for you.</span></span> 

1. <span data-ttu-id="5d59b-144">W **Eksploratorze rozwiązań** kliknij prawym przyciskiem myszy węzeł projektu i wybierz polecenie **Dodaj** > **Nowy element**.</span><span class="sxs-lookup"><span data-stu-id="5d59b-144">In **Solution Explorer**, right-click on your project node and select **Add** > **New Item**.</span></span> <span data-ttu-id="5d59b-145">Wybierz **funkcji platformy Azure**, wpisz **nazwa** hello klasy, a następnie kliknij przycisk **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="5d59b-145">Select **Azure Function**, type a **Name** for hello class, and click **Add**.</span></span>

2. <span data-ttu-id="5d59b-146">Wybierz wyzwalacz, ustaw hello powiązania właściwości, a następnie kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="5d59b-146">Choose your trigger, set hello binding properties, and click **Create**.</span></span> <span data-ttu-id="5d59b-147">Witaj poniższy przykład przedstawia ustawienia hello wyzwolenia tworzenia magazynu kolejek funkcji.</span><span class="sxs-lookup"><span data-stu-id="5d59b-147">hello following example shows hello settings when creating a Queue storage triggered function.</span></span> 

    ![](./media/functions-develop-vs/functions-vstools-create-queuetrigger.png)
    
    <span data-ttu-id="5d59b-148">Klucz ciąg połączenia o nazwie **QueueStorage** zostanie podany, która jest zdefiniowana w pliku local.settings.json hello.</span><span class="sxs-lookup"><span data-stu-id="5d59b-148">A connection string key named **QueueStorage** is supplied, which is defined in hello local.settings.json file.</span></span> 
 
3. <span data-ttu-id="5d59b-149">Sprawdź hello nowo dodanych klasy.</span><span class="sxs-lookup"><span data-stu-id="5d59b-149">Examine hello newly added class.</span></span> <span data-ttu-id="5d59b-150">Zobacz statycznego **Uruchom** — metoda, która ma atrybut hello **FunctionName** atrybutu.</span><span class="sxs-lookup"><span data-stu-id="5d59b-150">You see a static **Run** method, that is attributed with hello **FunctionName** attribute.</span></span> <span data-ttu-id="5d59b-151">Ten atrybut wskazuje, że metoda hello jest hello punkt wejścia dla funkcji hello.</span><span class="sxs-lookup"><span data-stu-id="5d59b-151">This attribute indicates that hello method is hello entry point for hello function.</span></span> 

    <span data-ttu-id="5d59b-152">Na przykład hello następujące klasy C# reprezentuje podstawowych funkcji magazynu wyzwalane kolejki:</span><span class="sxs-lookup"><span data-stu-id="5d59b-152">For example, hello following C# class represents a basic Queue storage triggered function:</span></span>

    ````csharp
    using System;
    using Microsoft.Azure.WebJobs;
    using Microsoft.Azure.WebJobs.Host;
    
    namespace FunctionApp1
    {
        public static class Function1
        {
            [FunctionName("QueueTriggerCSharp")]        
            public static void Run([QueueTrigger("myqueue-items", Connection = "QueueStorage")]string myQueueItem, TraceWriter log)
            {
                log.Info($"C# Queue trigger function processed: {myQueueItem}");
            }
        }
    } 
    ````
 
    <span data-ttu-id="5d59b-153">Atrybut specyficzne dla powiązania jest podany parametr wiązania zastosowane tooeach toohello metoda punktu wejścia.</span><span class="sxs-lookup"><span data-stu-id="5d59b-153">A binding-specific attribute is applied tooeach binding parameter supplied toohello entry point method.</span></span> <span data-ttu-id="5d59b-154">Atrybut Hello przyjmuje jako parametry, informacje o powiązaniu hello.</span><span class="sxs-lookup"><span data-stu-id="5d59b-154">hello attribute takes hello binding information as parameters.</span></span> <span data-ttu-id="5d59b-155">W poprzednim przykładzie hello hello pierwszy parametr ma **QueueTrigger** atrybut, wskazujący funkcję kolejki wyzwolone.</span><span class="sxs-lookup"><span data-stu-id="5d59b-155">In hello previous example, hello first parameter has a **QueueTrigger** attribute applied, indicating queue triggered function.</span></span> <span data-ttu-id="5d59b-156">Nazwa kolejki Hello i nazwa ustawienie parametrów połączenia są przekazywane jako parametry.</span><span class="sxs-lookup"><span data-stu-id="5d59b-156">hello queue name and connection string setting name are passed as parameters.</span></span>  

## <a name="testing-functions"></a><span data-ttu-id="5d59b-157">Testowanie funkcji</span><span class="sxs-lookup"><span data-stu-id="5d59b-157">Testing functions</span></span>

<span data-ttu-id="5d59b-158">Podstawowe narzędzia usługi Azure Functions umożliwiają uruchamianie projektu usługi Azure Functions na lokalnym komputerze deweloperskim.</span><span class="sxs-lookup"><span data-stu-id="5d59b-158">Azure Functions Core Tools lets you run Azure Functions project on your local development computer.</span></span> <span data-ttu-id="5d59b-159">Jesteś zostanie wyświetlony monit o tooinstall, które te narzędzia hello podczas pierwszego uruchomienia funkcji w programie Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5d59b-159">You are prompted tooinstall these tools hello first time you start a function from Visual Studio.</span></span>  

<span data-ttu-id="5d59b-160">tootest funkcji, naciśnij klawisz F5.</span><span class="sxs-lookup"><span data-stu-id="5d59b-160">tootest your function, press F5.</span></span> <span data-ttu-id="5d59b-161">Po wyświetleniu monitu Zaakceptuj Żądanie hello z toodownload programu Visual Studio i zainstalować narzędzia do podstawowych funkcji platformy Azure (CLI).</span><span class="sxs-lookup"><span data-stu-id="5d59b-161">If prompted, accept hello request from Visual Studio toodownload and install Azure Functions Core (CLI) tools.</span></span>  <span data-ttu-id="5d59b-162">Możesz także tooenable wyjątek zapory, aby narzędzia hello mogły obsługiwać żądania HTTP.</span><span class="sxs-lookup"><span data-stu-id="5d59b-162">You may also need tooenable a firewall exception so that hello tools can handle HTTP requests.</span></span>

<span data-ttu-id="5d59b-163">Z projektem hello uruchomiona można przetestować kodu jako może przetestować wdrożonej funkcji.</span><span class="sxs-lookup"><span data-stu-id="5d59b-163">With hello project running, you can test your code as you would test deployed function.</span></span> <span data-ttu-id="5d59b-164">Aby uzyskać więcej informacji, zobacz [strategii do testowania kodu w usługi Azure Functions](functions-test-a-function.md).</span><span class="sxs-lookup"><span data-stu-id="5d59b-164">For more information, see [Strategies for testing your code in Azure Functions](functions-test-a-function.md).</span></span> <span data-ttu-id="5d59b-165">Podczas uruchamiania w trybie debugowania, punkty przerwania są osiągane w programie Visual Studio, zgodnie z oczekiwaniami.</span><span class="sxs-lookup"><span data-stu-id="5d59b-165">When running in debug mode, breakpoints are hit in Visual Studio as expected.</span></span> 

<span data-ttu-id="5d59b-166">Przykład sposobu tootest kolejki wyzwalane funkcji, zobacz hello [samouczek Szybki Start — funkcja kolejki wyzwalane](functions-create-storage-queue-triggered-function.md#test-the-function).</span><span class="sxs-lookup"><span data-stu-id="5d59b-166">For an example of how tootest a queue triggered function, see hello [queue triggered function quickstart tutorial](functions-create-storage-queue-triggered-function.md#test-the-function).</span></span>  

<span data-ttu-id="5d59b-167">toolearn więcej informacji o użyciu hello Azure funkcje podstawowe narzędzia, zobacz [kodu i przetestuj usługę Azure functions lokalnie](functions-run-local.md).</span><span class="sxs-lookup"><span data-stu-id="5d59b-167">toolearn more about using hello Azure Functions Core Tools, see [Code and test Azure functions locally](functions-run-local.md).</span></span>

## <a name="publish-tooazure"></a><span data-ttu-id="5d59b-168">Publikowanie tooAzure</span><span class="sxs-lookup"><span data-stu-id="5d59b-168">Publish tooAzure</span></span>

[!INCLUDE [Publish hello project tooAzure](../../includes/functions-vstools-publish.md)]

>[!NOTE]  
><span data-ttu-id="5d59b-169">Wszystkie ustawienia dodanego w hello local.settings.json należy również dodać toohello funkcji aplikacji na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="5d59b-169">Any settings you added in hello local.settings.json must be also added toohello function app in Azure.</span></span> <span data-ttu-id="5d59b-170">Te ustawienia nie są automatycznie dodawane.</span><span class="sxs-lookup"><span data-stu-id="5d59b-170">These settings are not added automatically.</span></span> <span data-ttu-id="5d59b-171">Możesz dodać wymagane ustawienia tooyour funkcji aplikacji w jeden z następujących sposobów:</span><span class="sxs-lookup"><span data-stu-id="5d59b-171">You can add required settings tooyour function app in one of these ways:</span></span>
>
>* <span data-ttu-id="5d59b-172">[Przy użyciu hello portalu Azure](functions-how-to-use-azure-function-app-settings.md#settings).</span><span class="sxs-lookup"><span data-stu-id="5d59b-172">[Using hello Azure portal](functions-how-to-use-azure-function-app-settings.md#settings).</span></span>
>* <span data-ttu-id="5d59b-173">[Przy użyciu hello `--publish-local-settings` opcja publikowania w hello Azure funkcje podstawowe narzędzia](functions-run-local.md#publish).</span><span class="sxs-lookup"><span data-stu-id="5d59b-173">[Using hello `--publish-local-settings` publish option in hello Azure Functions Core Tools](functions-run-local.md#publish).</span></span>
>* <span data-ttu-id="5d59b-174">[Przy użyciu hello Azure CLI](/cli/azure/functionapp/config/appsettings#set).</span><span class="sxs-lookup"><span data-stu-id="5d59b-174">[Using hello Azure CLI](/cli/azure/functionapp/config/appsettings#set).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="5d59b-175">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="5d59b-175">Next steps</span></span>

<span data-ttu-id="5d59b-176">Uzyskać więcej informacji na temat narzędzia funkcji platformy Azure, zobacz typowe pytania części hello hello [2017 Visual Studio Tools dla usługi Azure Functions](https://blogs.msdn.microsoft.com/webdev/2017/05/10/azure-function-tools-for-visual-studio-2017/) wpis w blogu.</span><span class="sxs-lookup"><span data-stu-id="5d59b-176">For more information about Azure Functions Tools, see hello Common Questions section of hello [Visual Studio 2017 Tools for Azure Functions](https://blogs.msdn.microsoft.com/webdev/2017/05/10/azure-function-tools-for-visual-studio-2017/) blog post.</span></span>

<span data-ttu-id="5d59b-177">toolearn więcej informacji na temat hello Azure funkcje podstawowe narzędzia, zobacz [kodu i przetestuj usługę Azure functions lokalnie](functions-run-local.md).</span><span class="sxs-lookup"><span data-stu-id="5d59b-177">toolearn more about hello Azure Functions Core Tools, see [Code and test Azure functions locally](functions-run-local.md).</span></span>  
<span data-ttu-id="5d59b-178">toolearn więcej informacji na temat tworzenia funkcji jako biblioteki klas .NET, zobacz [.NET przy użyciu biblioteki klas z usługi Azure Functions](functions-dotnet-class-library.md).</span><span class="sxs-lookup"><span data-stu-id="5d59b-178">toolearn more about developing functions as .NET class libraries, see [Using .NET class libraries with Azure Functions](functions-dotnet-class-library.md).</span></span> <span data-ttu-id="5d59b-179">Ten temat zawiera również przykłady sposobu toodeclare atrybuty toouse hello różnego typu powiązania Azure Functions obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="5d59b-179">This topic also provides examples of how toouse attributes toodeclare hello various types of bindings supported by Azure Functions.</span></span>    
