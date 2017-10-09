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
# <a name="programmatically-create-a-stream-analytics-job-monitor"></a>Programowe tworzenie monitor zadania usługi analiza strumienia

W tym artykule przedstawiono sposób monitorowania tooenable zadania usługi analiza strumienia. Zadania usługi analiza strumienia, które są tworzone za pomocą interfejsów API REST, zestawu SDK platformy Azure lub programu PowerShell monitorowania, domyślnie nie jest konieczne. Można ręcznie włączyć ją w hello portalu Azure, przechodząc na stronę Monitor toohello zadania i klikając hello Włącz przycisk lub można zautomatyzować ten proces, wykonując kroki hello w tym artykule. Hello danych monitorowania zostaną wyświetlone w obszarze metryki hello hello portalu Azure dla zadania usługi analiza strumienia.

## <a name="prerequisites"></a>Wymagania wstępne

Przed rozpoczęciem tego procesu, musi mieć następujące hello:

* Visual Studio 2017 lub 2015
* [Azure .NET SDK](https://azure.microsoft.com/downloads/) pobrane i zainstalowane
* Istniejące zadanie usługi analiza strumienia musi toohave włączone monitorowanie

## <a name="create-a-project"></a>Tworzenie projektu

1. Utwórz aplikację konsolową programu Visual Studio C# .NET.
2. W konsoli Menedżera pakietów hello hello uruchom następujące polecenia pakietów NuGet hello tooinstall. Witaj najpierw jedna jest hello zestawu .NET SDK usługi Azure Stream Analytics zarządzania. Witaj drugim jest hello Azure SDK Monitor, który będzie używany tooenable monitorowania. Witaj ostatnio jedna jest powitania klienta usługi Azure Active Directory, który będzie używany do uwierzytelniania.
   
   ```
   Install-Package Microsoft.Azure.Management.StreamAnalytics
   Install-Package Microsoft.Azure.Insights -Pre
   Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
   ```
3. Dodaj hello następującego pliku App.config toohello sekcji appSettings.
   
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
   Zastąp wartości *SubscriptionId* i *ActiveDirectoryTenantId* identyfikatorami z usługi Azure subskrypcji i dzierżawcy. Te wartości można uzyskać, uruchamiając następujące polecenia cmdlet programu PowerShell hello:
   
   ```
   Get-AzureAccount
   ```
4. Dodaj następujące hello przy użyciu instrukcji toohello pliku źródłowego (Program.cs) w projekcie hello.
   
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
5. Dodaj metodę pomocnika uwierzytelniania.
   
     ciąg statycznego publicznego GetAuthorizationHeader()
   
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
     }

## <a name="create-management-clients"></a>Utwórz zarządzania klientami

Witaj następujący kod skonfiguruje hello niezbędne zmiennych i zarządzania klientami.

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

## <a name="enable-monitoring-for-an-existing-stream-analytics-job"></a>Aby włączyć monitorowanie dla istniejącego zadania usługi analiza strumienia

Witaj poniższy kod umożliwia monitorowanie **istniejących** zadania usługi analiza strumienia. Pierwsza część kodu hello Hello wykonuje żądanie GET względem hello Stream Analytics usługi tooretrieve informacji na temat określonego zadania usługi analiza strumienia hello. Używa hello *identyfikator* właściwości (pobierane z żądania GET hello) jako parametru metody Put w hello hello drugiej połowie hello kod, który wysyła żądanie PUT toohello Insights usługi monitorowania tooenable hello analiza strumienia zadanie.

>[!WARNING]
>Jeśli uprzednio włączono monitorowania dla różnych zadania Stream Analytics, za pośrednictwem hello portalu Azure lub programistycznie za pośrednictwem hello poniższego kodu, **firma Microsoft zaleca, aby podać hello używane podczas tej samej nazwy konta magazynu możesz wcześniej włączony, monitorowania.**
> 
> Konto magazynu Hello jest utworzone zadanie usługi analiza strumienia w nie specjalnie zadania toohello sam region toohello połączone.
> 
> Wszystkie usługi analiza strumienia zadania (i innych zasobów platformy Azure), w tym samym regionie udostępnić ten toostore konta magazynu danych monitorowania. Jeśli podasz innego konta magazynu może spowodować niezamierzone skutki uboczne w hello monitorowania inne zadania usługi analiza strumienia lub innych zasobów platformy Azure.
> 
> Nazwa konta magazynu Hello użycie tooreplace `<YOUR STORAGE ACCOUNT NAME>` powitania po kod powinien być konto magazynu, który znajduje się w hello tej samej subskrypcji co zadanie Stream Analytics hello włączasz monitorowania.
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



## <a name="get-support"></a>Uzyskiwanie pomocy technicznej

Aby uzyskać dodatkową pomoc, spróbuj naszych [forum usługi Azure Stream Analytics](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).

## <a name="next-steps"></a>Następne kroki

* [Wprowadzenie tooAzure analiza strumienia](stream-analytics-introduction.md)
* [Get started using Azure Stream Analytics (Rozpoczynanie pracy z usługą Azure Stream Analytics)](stream-analytics-real-time-fraud-detection.md)
* [Scale Azure Stream Analytics jobs (Skalowanie zadań usługi Azure Stream Analytics)](stream-analytics-scale-jobs.md)
* [Azure Stream Analytics Query Language Reference (Dokumentacja dotycząca języka zapytań usługi Azure Stream Analytics)](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Azure Stream Analytics Management REST API Reference (Dokumentacja interfejsu API REST zarządzania usługą Azure Stream Analytics)](https://msdn.microsoft.com/library/azure/dn835031.aspx)

