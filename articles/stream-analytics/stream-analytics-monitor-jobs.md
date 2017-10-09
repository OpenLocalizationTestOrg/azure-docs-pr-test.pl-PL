---
title: monitor aaaProgrammatically zadania Stream Analytics | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak tooprogrammatically monitorować zadania Stream Analytics utworzone za pośrednictwem interfejsów API REST, zestawu SDK platformy Azure lub programu PowerShell."
keywords: .NET monitor, zadanie monitora, monitorowanie aplikacji
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 2ec02cc9-4ca5-4a25-ae60-c44be9ad4835
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 04/20/2017
ms.author: jeffstok
ms.openlocfilehash: 44a9c29c2161ee81ea76ece4646a8691bf5d5b48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="programmatically-create-a-stream-analytics-job-monitor"></a><span data-ttu-id="f9590-104">Programowe tworzenie monitor zadania usługi analiza strumienia</span><span class="sxs-lookup"><span data-stu-id="f9590-104">Programmatically create a Stream Analytics job monitor</span></span>

<span data-ttu-id="f9590-105">W tym artykule przedstawiono sposób monitorowania tooenable zadania usługi analiza strumienia.</span><span class="sxs-lookup"><span data-stu-id="f9590-105">This article demonstrates how tooenable monitoring for a Stream Analytics job.</span></span> <span data-ttu-id="f9590-106">Zadania usługi analiza strumienia, które są tworzone za pomocą interfejsów API REST, zestawu SDK platformy Azure lub programu PowerShell monitorowania, domyślnie nie jest konieczne.</span><span class="sxs-lookup"><span data-stu-id="f9590-106">Stream Analytics jobs that are created via REST APIs, Azure SDK, or PowerShell do not have monitoring enabled by default.</span></span> <span data-ttu-id="f9590-107">Można ręcznie włączyć ją w hello portalu Azure, przechodząc na stronę Monitor toohello zadania i klikając hello Włącz przycisk lub można zautomatyzować ten proces, wykonując kroki hello w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="f9590-107">You can manually enable it in hello Azure portal by going toohello job’s Monitor page and clicking hello Enable button or you can automate this process by following hello steps in this article.</span></span> <span data-ttu-id="f9590-108">Hello danych monitorowania zostaną wyświetlone w obszarze metryki hello hello portalu Azure dla zadania usługi analiza strumienia.</span><span class="sxs-lookup"><span data-stu-id="f9590-108">hello monitoring data will show up in hello Metrics area of hello Azure portal for your Stream Analytics job.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f9590-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="f9590-109">Prerequisites</span></span>

<span data-ttu-id="f9590-110">Przed rozpoczęciem tego procesu, musi mieć następujące hello:</span><span class="sxs-lookup"><span data-stu-id="f9590-110">Before you begin this process, you must have hello following:</span></span>

* <span data-ttu-id="f9590-111">Visual Studio 2017 lub 2015</span><span class="sxs-lookup"><span data-stu-id="f9590-111">Visual Studio 2017 or 2015</span></span>
* <span data-ttu-id="f9590-112">[Azure .NET SDK](https://azure.microsoft.com/downloads/) pobrane i zainstalowane</span><span class="sxs-lookup"><span data-stu-id="f9590-112">[Azure .NET SDK](https://azure.microsoft.com/downloads/) downloaded and installed</span></span>
* <span data-ttu-id="f9590-113">Istniejące zadanie usługi analiza strumienia musi toohave włączone monitorowanie</span><span class="sxs-lookup"><span data-stu-id="f9590-113">An existing Stream Analytics job that needs toohave monitoring enabled</span></span>

## <a name="create-a-project"></a><span data-ttu-id="f9590-114">Tworzenie projektu</span><span class="sxs-lookup"><span data-stu-id="f9590-114">Create a project</span></span>

1. <span data-ttu-id="f9590-115">Utwórz aplikację konsolową programu Visual Studio C# .NET.</span><span class="sxs-lookup"><span data-stu-id="f9590-115">Create a Visual Studio C# .NET console application.</span></span>
2. <span data-ttu-id="f9590-116">W konsoli Menedżera pakietów hello hello uruchom następujące polecenia pakietów NuGet hello tooinstall.</span><span class="sxs-lookup"><span data-stu-id="f9590-116">In hello Package Manager Console, run hello following commands tooinstall hello NuGet packages.</span></span> <span data-ttu-id="f9590-117">Witaj najpierw jedna jest hello zestawu .NET SDK usługi Azure Stream Analytics zarządzania.</span><span class="sxs-lookup"><span data-stu-id="f9590-117">hello first one is hello Azure Stream Analytics Management .NET SDK.</span></span> <span data-ttu-id="f9590-118">Witaj drugim jest hello Azure SDK Monitor, który będzie używany tooenable monitorowania.</span><span class="sxs-lookup"><span data-stu-id="f9590-118">hello second one is hello Azure Monitor SDK that will be used tooenable monitoring.</span></span> <span data-ttu-id="f9590-119">Witaj ostatnio jedna jest powitania klienta usługi Azure Active Directory, który będzie używany do uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="f9590-119">hello last one is hello Azure Active Directory client that will be used for authentication.</span></span>
   
   ```
   Install-Package Microsoft.Azure.Management.StreamAnalytics
   Install-Package Microsoft.Azure.Insights -Pre
   Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
   ```
3. <span data-ttu-id="f9590-120">Dodaj hello następującego pliku App.config toohello sekcji appSettings.</span><span class="sxs-lookup"><span data-stu-id="f9590-120">Add hello following appSettings section toohello App.config file.</span></span>
   
   ```
   <appSettings>
     <!--CSM Prod related values-->
     <add key="ResourceGroupName" value="RESOURCE GROUP NAME" />
     <add key="JobName" value="YOUR JOB NAME" />
     <add key="StorageAccountName" value="YOUR STORAGE ACCOUNT"/>
     <add key="ActiveDirectoryEndpoint" value="https://login.microsoftonline.com/" />
     <add key="ResourceManagerEndpoint" value="https://management.azure.com/" />
     <add key="WindowsManagementUri" value="https://management.core.windows.net/" />
     <add key="AsaClientId" value="1950a258-227b-4e31-a9cf-717495945fc2" />
     <add key="RedirectUri" value="urn:ietf:wg:oauth:2.0:oob" />
     <add key="SubscriptionId" value="YOUR AZURE SUBSCRIPTION ID" />
     <add key="ActiveDirectoryTenantId" value="YOUR TENANT ID" />
   </appSettings>
   ```
   <span data-ttu-id="f9590-121">Zastąp wartości *SubscriptionId* i *ActiveDirectoryTenantId* identyfikatorami z usługi Azure subskrypcji i dzierżawcy.</span><span class="sxs-lookup"><span data-stu-id="f9590-121">Replace values for *SubscriptionId* and *ActiveDirectoryTenantId* with your Azure subscription and tenant IDs.</span></span> <span data-ttu-id="f9590-122">Te wartości można uzyskać, uruchamiając następujące polecenia cmdlet programu PowerShell hello:</span><span class="sxs-lookup"><span data-stu-id="f9590-122">You can get these values by running hello following PowerShell cmdlet:</span></span>
   
   ```
   Get-AzureAccount
   ```
4. <span data-ttu-id="f9590-123">Dodaj następujące hello przy użyciu instrukcji toohello pliku źródłowego (Program.cs) w projekcie hello.</span><span class="sxs-lookup"><span data-stu-id="f9590-123">Add hello following using statements toohello source file (Program.cs) in hello project.</span></span>
   
   ```
     using System;
     using System.Configuration;
     using System.Threading;
     using Microsoft.Azure;
     using Microsoft.Azure.Management.Insights;
     using Microsoft.Azure.Management.Insights.Models;
     using Microsoft.Azure.Management.StreamAnalytics;
     using Microsoft.Azure.Management.StreamAnalytics.Models;
     using Microsoft.IdentityModel.Clients.ActiveDirectory;
   ```
5. <span data-ttu-id="f9590-124">Dodaj metodę pomocnika uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="f9590-124">Add an authentication helper method.</span></span>
   
     <span data-ttu-id="f9590-125">ciąg statycznego publicznego GetAuthorizationHeader()</span><span class="sxs-lookup"><span data-stu-id="f9590-125">public static string GetAuthorizationHeader()</span></span>
   
         {
             AuthenticationResult result = null;
             var thread = new Thread(() =>
             {
                 try
                 {
                     var context = new AuthenticationContext(
                         ConfigurationManager.AppSettings["ActiveDirectoryEndpoint"] +
                         ConfigurationManager.AppSettings["ActiveDirectoryTenantId"]);
   
                     result = context.AcquireToken(
                         resource: ConfigurationManager.AppSettings["WindowsManagementUri"],
                         clientId: ConfigurationManager.AppSettings["AsaClientId"],
                         redirectUri: new Uri(ConfigurationManager.AppSettings["RedirectUri"]),
                         promptBehavior: PromptBehavior.Always);
                 }
                 catch (Exception threadEx)
                 {
                     Console.WriteLine(threadEx.Message);
                 }
             });
   
             thread.SetApartmentState(ApartmentState.STA);
             thread.Name = "AcquireTokenThread";
             thread.Start();
             thread.Join();
   
             if (result != null)
             {
                 return result.AccessToken;
             }
   
             throw new InvalidOperationException("Failed tooacquire token");
     <span data-ttu-id="f9590-126">}</span><span class="sxs-lookup"><span data-stu-id="f9590-126">}</span></span>

## <a name="create-management-clients"></a><span data-ttu-id="f9590-127">Utwórz zarządzania klientami</span><span class="sxs-lookup"><span data-stu-id="f9590-127">Create management clients</span></span>

<span data-ttu-id="f9590-128">Witaj następujący kod skonfiguruje hello niezbędne zmiennych i zarządzania klientami.</span><span class="sxs-lookup"><span data-stu-id="f9590-128">hello following code will set up hello necessary variables and management clients.</span></span>

    string resourceGroupName = "<YOUR AZURE RESOURCE GROUP NAME>";
    string streamAnalyticsJobName = "<YOUR STREAM ANALYTICS JOB NAME>";

    // Get authentication token
    TokenCloudCredentials aadTokenCredentials =
        new TokenCloudCredentials(
            ConfigurationManager.AppSettings["SubscriptionId"],
            GetAuthorizationHeader());

    Uri resourceManagerUri = new
    Uri(ConfigurationManager.AppSettings["ResourceManagerEndpoint"]);

    // Create Stream Analytics and Insights management client
    StreamAnalyticsManagementClient streamAnalyticsClient = new
    StreamAnalyticsManagementClient(aadTokenCredentials, resourceManagerUri);
    InsightsManagementClient insightsClient = new
    InsightsManagementClient(aadTokenCredentials, resourceManagerUri);

## <a name="enable-monitoring-for-an-existing-stream-analytics-job"></a><span data-ttu-id="f9590-129">Aby włączyć monitorowanie dla istniejącego zadania usługi analiza strumienia</span><span class="sxs-lookup"><span data-stu-id="f9590-129">Enable monitoring for an existing Stream Analytics job</span></span>

<span data-ttu-id="f9590-130">Witaj poniższy kod umożliwia monitorowanie **istniejących** zadania usługi analiza strumienia.</span><span class="sxs-lookup"><span data-stu-id="f9590-130">hello following code enables monitoring for an **existing** Stream Analytics job.</span></span> <span data-ttu-id="f9590-131">Pierwsza część kodu hello Hello wykonuje żądanie GET względem hello Stream Analytics usługi tooretrieve informacji na temat określonego zadania usługi analiza strumienia hello.</span><span class="sxs-lookup"><span data-stu-id="f9590-131">hello first part of hello code performs a GET request against hello Stream Analytics service tooretrieve information about hello particular Stream Analytics job.</span></span> <span data-ttu-id="f9590-132">Używa hello *identyfikator* właściwości (pobierane z żądania GET hello) jako parametru metody Put w hello hello drugiej połowie hello kod, który wysyła żądanie PUT toohello Insights usługi monitorowania tooenable hello analiza strumienia zadanie.</span><span class="sxs-lookup"><span data-stu-id="f9590-132">It uses hello *Id* property (retrieved from hello GET request) as a parameter for hello Put method in hello second half of hello code, which sends a PUT request toohello Insights service tooenable monitoring for hello Stream Analytics job.</span></span>

>[!WARNING]
><span data-ttu-id="f9590-133">Jeśli uprzednio włączono monitorowania dla różnych zadania Stream Analytics, za pośrednictwem hello portalu Azure lub programistycznie za pośrednictwem hello poniższego kodu, **firma Microsoft zaleca, aby podać hello używane podczas tej samej nazwy konta magazynu możesz wcześniej włączony, monitorowania.**</span><span class="sxs-lookup"><span data-stu-id="f9590-133">If you have previously enabled monitoring for a different Stream Analytics job, either through hello Azure portal or programmatically via hello below code, **we recommend that you provide hello same storage account name that you used when you previously enabled monitoring.**</span></span>
> 
> <span data-ttu-id="f9590-134">Konto magazynu Hello jest utworzone zadanie usługi analiza strumienia w nie specjalnie zadania toohello sam region toohello połączone.</span><span class="sxs-lookup"><span data-stu-id="f9590-134">hello storage account is linked toohello region that you created your Stream Analytics job in, not specifically toohello job itself.</span></span>
> 
> <span data-ttu-id="f9590-135">Wszystkie usługi analiza strumienia zadania (i innych zasobów platformy Azure), w tym samym regionie udostępnić ten toostore konta magazynu danych monitorowania.</span><span class="sxs-lookup"><span data-stu-id="f9590-135">All Stream Analytics jobs (and all other Azure resources) in that same region share this storage account toostore monitoring data.</span></span> <span data-ttu-id="f9590-136">Jeśli podasz innego konta magazynu może spowodować niezamierzone skutki uboczne w hello monitorowania inne zadania usługi analiza strumienia lub innych zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="f9590-136">If you provide a different storage account, it might cause unintended side effects in hello monitoring of your other Stream Analytics jobs or other Azure resources.</span></span>
> 
> <span data-ttu-id="f9590-137">Nazwa konta magazynu Hello użycie tooreplace `<YOUR STORAGE ACCOUNT NAME>` powitania po kod powinien być konto magazynu, który znajduje się w hello tej samej subskrypcji co zadanie Stream Analytics hello włączasz monitorowania.</span><span class="sxs-lookup"><span data-stu-id="f9590-137">hello storage account name that you use tooreplace `<YOUR STORAGE ACCOUNT NAME>` in hello following code should be a storage account that is in hello same subscription as hello Stream Analytics job that you are enabling monitoring for.</span></span>
> 
> 

    // Get an existing Stream Analytics job
    JobGetParameters jobGetParameters = new JobGetParameters()
    {
        PropertiesToExpand = "inputs,transformation,outputs"
    };
    JobGetResponse jobGetResponse = streamAnalyticsClient.StreamingJobs.Get(resourceGroupName, streamAnalyticsJobName, jobGetParameters);

    // Enable monitoring
    ServiceDiagnosticSettingsPutParameters insightPutParameters = new ServiceDiagnosticSettingsPutParameters()
    {
            Properties = new ServiceDiagnosticSettings()
            {
                StorageAccountName = "<YOUR STORAGE ACCOUNT NAME>"
            }
    };
    insightsClient.ServiceDiagnosticSettingsOperations.Put(jobGetResponse.Job.Id, insightPutParameters);



## <a name="get-support"></a><span data-ttu-id="f9590-138">Uzyskiwanie pomocy technicznej</span><span class="sxs-lookup"><span data-stu-id="f9590-138">Get support</span></span>

<span data-ttu-id="f9590-139">Aby uzyskać dodatkową pomoc, spróbuj naszych [forum usługi Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="f9590-139">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="f9590-140">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f9590-140">Next steps</span></span>

* [<span data-ttu-id="f9590-141">Wprowadzenie tooAzure analiza strumienia</span><span class="sxs-lookup"><span data-stu-id="f9590-141">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="f9590-142">Get started using Azure Stream Analytics (Rozpoczynanie pracy z usługą Azure Stream Analytics)</span><span class="sxs-lookup"><span data-stu-id="f9590-142">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="f9590-143">Scale Azure Stream Analytics jobs (Skalowanie zadań usługi Azure Stream Analytics)</span><span class="sxs-lookup"><span data-stu-id="f9590-143">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="f9590-144">Azure Stream Analytics Query Language Reference (Dokumentacja dotycząca języka zapytań usługi Azure Stream Analytics)</span><span class="sxs-lookup"><span data-stu-id="f9590-144">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="f9590-145">Azure Stream Analytics Management REST API Reference (Dokumentacja interfejsu API REST zarządzania usługą Azure Stream Analytics)</span><span class="sxs-lookup"><span data-stu-id="f9590-145">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

