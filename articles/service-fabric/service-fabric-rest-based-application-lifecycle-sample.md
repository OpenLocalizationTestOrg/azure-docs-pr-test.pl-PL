---
title: "przykład cyklu życia aplikacji opartej na aaaREST | Dokumentacja firmy Microsoft"
description: "Próbka usługi sieć szkieletowa usług Microsoft Azure, która zawiera cyklem życia aplikacji hello przy użyciu interfejsu REST sieci szkieletowej usług hello."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 0a374e53-ff23-4ee8-8cc6-259d41e118e7
ms.service: service-fabric
ms.devlang: rest-api
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/2/2016
ms.author: ryanwi
redirect_url: /rest/api/servicefabric/
ms.openlocfilehash: a6817edb932b3e9fc987dc7d90bcbb3c5eb91e64
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="rest-based-application-lifecycle-sample"></a><span data-ttu-id="088a5-103">Przykład cyklu życia aplikacji opartej na protokole REST</span><span class="sxs-lookup"><span data-stu-id="088a5-103">REST-based application lifecycle sample</span></span>
<span data-ttu-id="088a5-104">W tym przykładzie przedstawiono hello cyklem życia aplikacji sieci szkieletowej usług za pośrednictwem wywołania interfejsu API REST.</span><span class="sxs-lookup"><span data-stu-id="088a5-104">This sample demonstrates hello Service Fabric application lifecycle through REST API calls.</span></span> <span data-ttu-id="088a5-105">Aby uzyskać więcej informacji na cyklem życia aplikacji usługi sieć szkieletowa hello, zobacz [cyklem życia aplikacji usługi sieć szkieletowa](service-fabric-application-lifecycle.md).</span><span class="sxs-lookup"><span data-stu-id="088a5-105">For more information on hello Service Fabric application lifecycle, see [Service Fabric application lifecycle](service-fabric-application-lifecycle.md).</span></span>

<span data-ttu-id="088a5-106">W tym przykładzie są wykonywane następujące hello:</span><span class="sxs-lookup"><span data-stu-id="088a5-106">This sample performs hello following:</span></span>

* <span data-ttu-id="088a5-107">Witaj przepisy **WordCount 1.0.0** próbki z pakietu aplikacji WordCount hello w magazynie obraz powitania.</span><span class="sxs-lookup"><span data-stu-id="088a5-107">Provisions hello **WordCount 1.0.0** sample from hello WordCount application package in hello image store.</span></span>
* <span data-ttu-id="088a5-108">Wyświetla listę hello typy aplikacji, w tym WordCount 1.0.0.</span><span class="sxs-lookup"><span data-stu-id="088a5-108">Displays hello list of application types, which includes WordCount 1.0.0.</span></span>
* <span data-ttu-id="088a5-109">Tworzy aplikację WordCount hello jako **fabric: / WordCount**.</span><span class="sxs-lookup"><span data-stu-id="088a5-109">Creates hello WordCount application as **fabric:/WordCount**.</span></span>
* <span data-ttu-id="088a5-110">Wyświetla hello listę aplikacji, w tym sieci szkieletowej: / WordCount w wersji 1.0.0.</span><span class="sxs-lookup"><span data-stu-id="088a5-110">Displays hello list of applications, which includes fabric:/WordCount version 1.0.0.</span></span>
* <span data-ttu-id="088a5-111">Wersja hello 1.1.0 przepisy przykładu WordCount hello z hello **WordCountUpgrade** pakiet aplikacji hello obraz magazynu.</span><span class="sxs-lookup"><span data-stu-id="088a5-111">Provisions hello 1.1.0 version of hello WordCount sample from hello **WordCountUpgrade** application package in hello image store.</span></span>
* <span data-ttu-id="088a5-112">Wyświetla hello listę typów aplikacji, która obejmuje zarówno WordCount 1.0.0 i **WordCount 1.1.0**.</span><span class="sxs-lookup"><span data-stu-id="088a5-112">Displays hello list of application types, which includes both WordCount 1.0.0 and **WordCount 1.1.0**.</span></span>
* <span data-ttu-id="088a5-113">Uaktualnia tooversion aplikacji WordCount hello 1.1.0.</span><span class="sxs-lookup"><span data-stu-id="088a5-113">Upgrades hello WordCount application tooversion 1.1.0.</span></span>
* <span data-ttu-id="088a5-114">Wyświetla hello listę aplikacji, która obejmuje WordCount wersji 1.1.0, ale nie zawiera już WordCount w wersji 1.0.0.</span><span class="sxs-lookup"><span data-stu-id="088a5-114">Displays hello list of applications, which includes WordCount version 1.1.0, but no longer includes WordCount version 1.0.0.</span></span>
* <span data-ttu-id="088a5-115">Usuwa hello aplikacji WordCount.</span><span class="sxs-lookup"><span data-stu-id="088a5-115">Deletes hello WordCount application.</span></span>
* <span data-ttu-id="088a5-116">Wyświetla hello listę aplikacji, która nie zawiera już sieci szkieletowej: / WordCount.</span><span class="sxs-lookup"><span data-stu-id="088a5-116">Displays hello list of applications, which no longer includes fabric:/WordCount.</span></span>
* <span data-ttu-id="088a5-117">Wstrzymuje obsługę administracyjną wersji hello 1.1.0 hello przykładu WordCount.</span><span class="sxs-lookup"><span data-stu-id="088a5-117">Unprovisions hello 1.1.0 version of hello WordCount sample.</span></span>
* <span data-ttu-id="088a5-118">Wyświetla listę hello typy aplikacji, co obejmuje WordCount 1.0.0, ale nie zawiera już WordCount 1.1.0.</span><span class="sxs-lookup"><span data-stu-id="088a5-118">Displays hello list of application types, which includes WordCount 1.0.0, but no longer includes WordCount 1.1.0.</span></span>
* <span data-ttu-id="088a5-119">Wstrzymuje obsługę administracyjną wersji hello 1.0.0 hello przykładu WordCount.</span><span class="sxs-lookup"><span data-stu-id="088a5-119">Unprovisions hello 1.0.0 version of hello WordCount sample.</span></span>
* <span data-ttu-id="088a5-120">Wyświetla listę hello typy aplikacji, która nie zawiera już WordCount.</span><span class="sxs-lookup"><span data-stu-id="088a5-120">Displays hello list of application types, which no longer includes WordCount.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="088a5-121">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="088a5-121">Prerequisites</span></span>
<span data-ttu-id="088a5-122">W przykładzie użyto hello [przykład WordCount](http://aka.ms/servicefabricsamples) (znalezione w hello **wprowadzenie** — przykłady).</span><span class="sxs-lookup"><span data-stu-id="088a5-122">This sample uses hello [WordCount sample](http://aka.ms/servicefabricsamples) (found in hello **Getting Started** samples).</span></span> <span data-ttu-id="088a5-123">przykład WordCount Hello muszą zostać skompilowane na początku, a następnie dwa pakiety aplikacji musi być skopiowany toohello magazynu obrazów.</span><span class="sxs-lookup"><span data-stu-id="088a5-123">hello WordCount sample must be built first, and then two application packages must be copied toohello image store.</span></span>

| <span data-ttu-id="088a5-124">Folder</span><span class="sxs-lookup"><span data-stu-id="088a5-124">Folder</span></span> | <span data-ttu-id="088a5-125">Opis</span><span class="sxs-lookup"><span data-stu-id="088a5-125">Description</span></span> |
| --- | --- |
| <span data-ttu-id="088a5-126">WordCount</span><span class="sxs-lookup"><span data-stu-id="088a5-126">WordCount</span></span> |<span data-ttu-id="088a5-127">Witaj WordCount przykładowej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="088a5-127">hello WordCount sample application.</span></span> <span data-ttu-id="088a5-128">Witaj **ApplicationManifest.xml** plik zawiera **ApplicationTypeVersion = "1.0.0"**.</span><span class="sxs-lookup"><span data-stu-id="088a5-128">hello **ApplicationManifest.xml** file contains **ApplicationTypeVersion="1.0.0"**.</span></span> |
| <span data-ttu-id="088a5-129">WordCountUpgrade</span><span class="sxs-lookup"><span data-stu-id="088a5-129">WordCountUpgrade</span></span> |<span data-ttu-id="088a5-130">Witaj WordCount przykładowej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="088a5-130">hello WordCount sample application.</span></span> <span data-ttu-id="088a5-131">pliku ApplicationManifest.xml Hello musi zostać zmieniony zbyt**ApplicationTypeVersion = "1.1.0"** toooccur uaktualniania aplikacji hello tooallow.</span><span class="sxs-lookup"><span data-stu-id="088a5-131">hello ApplicationManifest.xml file must be changed too**ApplicationTypeVersion="1.1.0"** tooallow hello application upgrade toooccur.</span></span> |

<span data-ttu-id="088a5-132">toocreate hello pakietów aplikacji i skopiuj je toohello magazynu obrazów, wykonać hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="088a5-132">toocreate hello application packages and copy them toohello image store, take hello following steps:</span></span>

1. <span data-ttu-id="088a5-133">Kopiuj **C:\ServiceFabricSamples\Services\WordCount\WordCount\pkg\Debug** za**C:\Temp\WordCount**.</span><span class="sxs-lookup"><span data-stu-id="088a5-133">Copy **C:\ServiceFabricSamples\Services\WordCount\WordCount\pkg\Debug** too**C:\Temp\WordCount**.</span></span> <span data-ttu-id="088a5-134">Spowoduje to utworzenie pakietu aplikacji hello WordCount.</span><span class="sxs-lookup"><span data-stu-id="088a5-134">This creates hello WordCount application package.</span></span>
2. <span data-ttu-id="088a5-135">Skopiuj C:\Temp\WordCount zbyt**C:\Temp\WordCountUpgrade**.</span><span class="sxs-lookup"><span data-stu-id="088a5-135">Copy C:\Temp\WordCount too**C:\Temp\WordCountUpgrade**.</span></span> <span data-ttu-id="088a5-136">Spowoduje to utworzenie hello **aplikacji WordCountUpgrade** pakietu.</span><span class="sxs-lookup"><span data-stu-id="088a5-136">This creates hello **WordCountUpgrade application** package.</span></span>
3. <span data-ttu-id="088a5-137">Otwórz **C:\Temp\WordCountUpgrade\ApplicationManifest.xml** w edytorze tekstów.</span><span class="sxs-lookup"><span data-stu-id="088a5-137">Open **C:\Temp\WordCountUpgrade\ApplicationManifest.xml** in a text editor.</span></span>
4. <span data-ttu-id="088a5-138">W hello **ApplicationManifest** element, zmień hello **ApplicationTypeVersion** atrybutu zbyt**"1.1.0"**.</span><span class="sxs-lookup"><span data-stu-id="088a5-138">In hello **ApplicationManifest** element, change hello **ApplicationTypeVersion** attribute too**"1.1.0"**.</span></span>  <span data-ttu-id="088a5-139">Spowoduje to zaktualizowanie hello numer wersji aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="088a5-139">This updates hello version number of hello application.</span></span>
5. <span data-ttu-id="088a5-140">Zapisywanie pliku ApplicationManifest.xml hello zmienione.</span><span class="sxs-lookup"><span data-stu-id="088a5-140">Save hello changed ApplicationManifest.xml file.</span></span>
6. <span data-ttu-id="088a5-141">Uruchom magazynu obrazów toohello toocopy hello aplikacji hello następującego skryptu programu PowerShell jako administrator:</span><span class="sxs-lookup"><span data-stu-id="088a5-141">Run hello following PowerShell script as an administrator toocopy hello applications toohello image store:</span></span>

```powershell
# Deploy hello WordCount and upgrade applications
$applicationPathWordCount = "C:\Temp\WordCount"
$applicationPathUpgrade = "C:\Temp\WordCountUpgrade"

# LOCAL:
$imageStoreConnection = "file:C:\SfDevCluster\Data\ImageStoreShare"
$cluster = 'localhost:19000'

Connect-ServiceFabricCluster $cluster

Copy-ServiceFabricApplicationPackage -ApplicationPackagePath $applicationPathWordCount -ImageStoreConnectionString $imageStoreConnection
Copy-ServiceFabricApplicationPackage -ApplicationPackagePath $applicationPathUpgrade -ImageStoreConnectionString $imageStoreConnection
```

<span data-ttu-id="088a5-142">Po zakończeniu hello skrypt programu PowerShell, ta aplikacja jest gotowa toorun.</span><span class="sxs-lookup"><span data-stu-id="088a5-142">When hello PowerShell script finishes, this application is ready toorun.</span></span>

## <a name="example"></a><span data-ttu-id="088a5-143">Przykład</span><span class="sxs-lookup"><span data-stu-id="088a5-143">Example</span></span>
<span data-ttu-id="088a5-144">Witaj poniższy przykład pokazuje cyklem życia aplikacji usługi sieć szkieletowa hello.</span><span class="sxs-lookup"><span data-stu-id="088a5-144">hello following example demonstrates hello Service Fabric application lifecycle.</span></span>

```csharp
using System;
using System.Collections.Generic;
using System.Fabric;
using System.Fabric.Description;
using System.Fabric.Health;
using System.Fabric.Query;
using System.IO;
using System.Net;
using System.Text;
using System.Web.Script.Serialization;

namespace ServiceFabricRestCaller
{
    class Program
    {
        static void Main(string[] args)
        {
            Uri clusterUri = new Uri("http://localhost:19080");
            string buildPathApplication = "WordCount";
            string applicationVersionNumber = "1.0.0";
            string buildPathUpgrade = "WordCountUpgrade";
            string updateVersionNumber = "1.1.0";

            Console.WriteLine("\nProvision hello 1.0.0 WordCount application for hello first time.");
            ProvisionAnApplication(clusterUri, buildPathApplication);
            Console.WriteLine("\nPress Enter tooget hello list of application types: ");
            Console.ReadLine();


            Console.WriteLine("\nGet hello list of application types.");
            GetListOfApplicationTypes(clusterUri);
            Console.WriteLine("\nPress Enter toocreate hello fabric:/WordCount application: ");
            Console.ReadLine();


            Console.WriteLine("\nCreate hello fabric:/WordCount application.");
            CreateApplication(clusterUri);
            Console.WriteLine("\nPress Enter tooget hello list of applications: ");
            Console.ReadLine();


            Console.WriteLine("\nGet hello list of applications.");
            GetApplicationList(clusterUri);
            Console.WriteLine("\nPress Enter tooprovision hello 1.1.0 upgrade toohello WordCount application: ");
            Console.ReadLine();


            Console.WriteLine("\nProvision hello 1.1.0 upgrade toohello WordCount application.");
            ProvisionAnApplication(clusterUri, buildPathUpgrade);
            Console.WriteLine("\nPress Enter tooget hello list of application types: ");
            Console.ReadLine();


            Console.WriteLine("\nGet hello list of application types.");
            GetListOfApplicationTypes(clusterUri);
            Console.WriteLine("\nPress Enter tooupgrade hello fabric:/WordCount application: ");
            Console.ReadLine();


            Console.WriteLine("\nUpgrade hello fabric:/WordCount application.");
            UpgradeApplicationByApplicationType(clusterUri);
            Console.WriteLine("\nPress Enter tooget hello list of applications: ");
            Console.ReadLine();


            Console.WriteLine("\nGet hello list of applications.");
            GetApplicationList(clusterUri);
            Console.WriteLine("\nPress Enter toodelete hello fabric:/WordCount application: ");
            Console.ReadLine();


            Console.WriteLine("\nDelete hello fabric:/WordCount application.");
            DeleteApplication(clusterUri);
            Console.WriteLine("\nPress Enter tooget hello list of applications: ");
            Console.ReadLine();


            Console.WriteLine("\nGet hello list of applications.");
            GetApplicationList(clusterUri);
            Console.WriteLine("\nPress Enter toounprovision hello WordCount 1.1.0 application: ");
            Console.ReadLine();


            Console.WriteLine("\nUnprovision hello WordCount 1.1.0 application.");
            UnprovisionAnApplication(clusterUri, updateVersionNumber);
            Console.WriteLine("\nPress Enter tooget hello list of application types: ");
            Console.ReadLine();


            Console.WriteLine("\nGet hello list of application types.");
            GetListOfApplicationTypes(clusterUri);
            Console.WriteLine("\nPress Enter toounprovision hello WordCount 1.0.0 application: ");
            Console.ReadLine();


            Console.WriteLine("\nUnprovision hello WordCount 1.0.0 application.");
            UnprovisionAnApplication(clusterUri, applicationVersionNumber);
            Console.WriteLine("\nPress Enter tooget hello final list of application types: ");
            Console.ReadLine();


            Console.WriteLine("\nGet hello final list of application types.");
            GetListOfApplicationTypes(clusterUri);
            Console.WriteLine("\nPress Enter tooend this program: ");
            Console.ReadLine();
        }

        #region Classes

        /// <summary>
        /// Class similar tooApplicationType. Designed for use with JavaScriptSerializer.
        /// </summary>
        public class AppType
        {
            public string Name { get; set; }
            public string Version { get; set; }
            public List<ApplicationParameter> DefaultParameterList { get; set; }
        }

        /// <summary>
        /// Class designed for use with JavaScriptSerializer.
        /// </summary>
        public class ApplicationInfo
        {
            public string Id { get; set; }
            public string Name { get; set; }
            public string TypeName { get; set; }
            public string TypeVersion { get; set; }
            public ApplicationStatus Status { get; set; }
            public List<Parameter> Parameters { get; set; }
            public HealthState HealthState { get; set; }
        }

        /// <summary>
        /// Class similar tooParameter. Designed for use with JavaScriptSerializer.
        /// </summary>
        public class Parameter
        {
            public string Name { get; set; }
            public string Value { get; set; }
        }

        #endregion


        #region Get List of Application Types (REST API)

        /// <summary>
        /// Gets hello list of application types.
        /// </summary>
        /// <param name="clusterUri">hello URI tooaccess hello cluster.</param>
        /// <returns>Returns true if successful; otherwise false.</returns>
        public static bool GetListOfApplicationTypes(Uri clusterUri)
        {
            // String toocapture hello response stream.
            string responseString = string.Empty;

            // Create hello request and add URL parameters.
            Uri requestUri = new Uri(clusterUri, string.Format("/ApplicationTypes?api-version={0}",
            "1.0"));    // api-version

            HttpWebRequest request = (HttpWebRequest)WebRequest.Create(requestUri);
            request.Method = "GET";

            // Execute hello request and obtain hello response.
            try
            {
                using (HttpWebResponse response = (HttpWebResponse)request.GetResponse())
                {
                    using (StreamReader streamReader = new StreamReader(response.GetResponseStream(), true))
                    {
                        // Capture hello response string.
                        responseString = streamReader.ReadToEnd();
                    }
                }
            }
            catch (WebException e)
            {
                // If there is a web exception, display hello error message.
                Console.WriteLine("Error getting hello list of application types:");
                Console.WriteLine(e.Message);
                if (e.InnerException != null)
                    Console.WriteLine(e.InnerException.Message);
                return false;
            }
            catch (Exception e)
            {
                // If there is another kind of exception, throw it.
                throw (e);
            }

            // Deserialize hello response string.
            JavaScriptSerializer jss = new JavaScriptSerializer();
            List<AppType> applicationTypes = jss.Deserialize<List<AppType>>(responseString);

            // Display application type information for each application type.
            Console.WriteLine("Application types:");
            foreach (AppType applicationType in applicationTypes)
            {
                Console.WriteLine("  Application Type:");
                Console.WriteLine("    Name: " + applicationType.Name);
                Console.WriteLine("    Version: " + applicationType.Version);
                Console.WriteLine("    Default Parameter List:");

                foreach (var parameter in applicationType.DefaultParameterList)
                {
                    Console.WriteLine("      Name: " + parameter.Name);
                    Console.WriteLine("      Value: " + parameter.Value);
                }
            }

            return true;
        }

        #endregion


        #region Provision an Application (REST API)

        /// <summary>
        /// Provisions an application toohello image store.
        /// </summary>
        /// <param name="clusterUri">hello URI tooaccess hello cluster.</param>
        /// <param name="applicationTypeBuildPath">hello application type build path ("WordCount" or "WordCountUpgrade").</param>
        /// <returns>Returns true if successful; otherwise false.</returns>
        public static bool ProvisionAnApplication(Uri clusterUri, string applicationTypeBuildPath)
        {
            // Create hello request and add URL parameters.
            Uri requestUri = new Uri(clusterUri, string.Format("/ApplicationTypes/$/Provision?api-version={0}",
                "1.0"));    // api-version

            HttpWebRequest request = (HttpWebRequest)WebRequest.Create(requestUri);
            request.Method = "POST";
            request.ContentType = "application/json; charset=utf-8";

            // Create hello byte array that will become hello request body.
            string requestBody = "{\"ApplicationTypeBuildPath\":\"" + applicationTypeBuildPath + "\"}";
            byte[] requestBodyBytes = Encoding.UTF8.GetBytes(requestBody);
            request.ContentLength = requestBodyBytes.Length;

            // Stores hello response status code.
            HttpStatusCode statusCode;

            // Create hello request body.
            try
            {
                using (Stream requestStream = request.GetRequestStream())
                {
                    requestStream.Write(requestBodyBytes, 0, requestBodyBytes.Length);
                    requestStream.Close();

                    // Execute hello request and obtain hello response.
                    using (HttpWebResponse response = (HttpWebResponse)request.GetResponse())
                    {
                        statusCode = response.StatusCode;
                    }
                }
            }
            catch (WebException e)
            {
                // If there is a web exception, display hello error message.
                Console.WriteLine("Error provisioning hello application:");
                Console.WriteLine(e.Message);
                if (e.InnerException != null)
                    Console.WriteLine(e.InnerException.Message);
                return false;
            }
            catch (Exception e)
            {
                // If there is another kind of exception, throw it.
                throw (e);
            }

            Console.WriteLine("Provision an Application response status = " + statusCode.ToString());
            return true;
        }

        #endregion

        #region Unprovision an Application (REST API)

        /// <summary>
        /// Unprovisions an application.
        /// </summary>
        /// <param name="clusterUri">hello URI tooaccess hello cluster.</param>
        /// <returns>Returns true if successful; otherwise false.</returns>
        public static bool UnprovisionAnApplication(Uri clusterUri, string versionToUnprovision)
        {
            // Create hello request and add URL parameters.
            Uri requestUri = new Uri(clusterUri, string.Format("/ApplicationTypes/{0}/$/Unprovision?api-version={1}",
                "WordCount",     // Application Type Name
                "1.0"));            // api-version

            HttpWebRequest request = (HttpWebRequest)WebRequest.Create(requestUri);
            request.Method = "POST";
            request.ContentType = "application/json; charset=utf-8";

            // Stores hello response status code.
            HttpStatusCode statusCode;

            // Create hello byte array that will become hello request body.
            string requestBody = "{\"ApplicationTypeVersion\":\"" + versionToUnprovision + "\"}";
            byte[] requestBodyBytes = Encoding.UTF8.GetBytes(requestBody);
            request.ContentLength = requestBodyBytes.Length;

            // Create hello request body.
            try
            {
                using (Stream requestStream = request.GetRequestStream())
                {
                    requestStream.Write(requestBodyBytes, 0, requestBodyBytes.Length);
                    requestStream.Close();

                    // Execute hello request and obtain hello response.
                    using (HttpWebResponse response = (HttpWebResponse)request.GetResponse())
                    {
                        statusCode = response.StatusCode;
                    }
                }
            }
            catch (WebException e)
            {
                // If there is a web exception, display hello error message.
                Console.WriteLine("Error unprovisioning hello application:");
                Console.WriteLine(e.Message);
                if (e.InnerException != null)
                    Console.WriteLine(e.InnerException.Message);
                return false;
            }
            catch (Exception e)
            {
                // If there is another kind of exception, throw it.
                throw (e);
            }

            Console.WriteLine("Unprovision an Application response status = " + statusCode.ToString());
            return true;
        }

        #endregion

        #region Get Application List (REST API)

        /// <summary>
        /// Gets hello list of applications.
        /// </summary>
        /// <param name="clusterUri">hello URI tooaccess hello cluster.</param>
        /// <returns>Returns true if successful; otherwise false.</returns>
        public static bool GetApplicationList(Uri clusterUri)
        {
            // String toocapture hello response stream.
            string responseString = string.Empty;

            // Create hello request and add URL parameters.
            Uri requestUri = new Uri(clusterUri, string.Format("/Applications?api-version={0}",
                "1.0")); // api-version

            HttpWebRequest request = (HttpWebRequest)WebRequest.Create(requestUri);
            request.Method = "GET";

            // Execute hello request and obtain hello response.
            try
            {
                using (HttpWebResponse response = (HttpWebResponse)request.GetResponse())
                {
                    using (StreamReader streamReader = new StreamReader(response.GetResponseStream(), true))
                    {
                        // Capture hello response string.
                        responseString = streamReader.ReadToEnd();
                    }
                }
            }
            catch (WebException e)
            {
                // If there is a web exception, display hello error message.
                Console.WriteLine("Error getting hello application list:");
                Console.WriteLine(e.Message);
                if (e.InnerException != null)
                    Console.WriteLine(e.InnerException.Message);
                return false;
            }
            catch (Exception e)
            {
                // If there is another kind of exception, throw it.
                throw (e);
            }


            // Deserialize hello response string.
            JavaScriptSerializer jss = new JavaScriptSerializer();
            List<ApplicationInfo> applicationInfos = jss.Deserialize<List<ApplicationInfo>>(responseString);

            // Display some application information for each application.
            Console.WriteLine("Application List:");
            foreach (ApplicationInfo applicationInfo in applicationInfos)
            {
                Console.WriteLine("  Application:");
                Console.WriteLine("    Id: " + applicationInfo.Id);
                Console.WriteLine("    Name: " + applicationInfo.Name);
                Console.WriteLine("    TypeName: " + applicationInfo.TypeName);
                Console.WriteLine("    TypeVersion: " + applicationInfo.TypeVersion);
                Console.WriteLine("    Status: " + applicationInfo.Status);
                Console.WriteLine("    HealthState: " + applicationInfo.HealthState);

                Console.WriteLine("    Parameters:");

                foreach (Parameter parameter in applicationInfo.Parameters)
                {
                    Console.WriteLine("      Parameter:");
                    Console.WriteLine("        Name: " + parameter.Name);
                    Console.WriteLine("        Value: " + parameter.Value);
                }
            }

            return true;
        }

        #endregion

        #region Create Application (REST API)

        /// <summary>
        /// Creates an application.
        /// </summary>
        /// <param name="clusterUri">hello URI tooaccess hello cluster.</param>
        /// <returns>Returns true if successful; otherwise false.</returns>
        public static bool CreateApplication(Uri clusterUri)
        {
            // String toocapture hello response stream.
            string responseString = string.Empty;

            // Stores hello response status code.
            HttpStatusCode statusCode;

            // Create hello request and add URL parameters.
            Uri requestUri = new Uri(clusterUri, string.Format("/Applications/$/Create?api-version={0}",
                "1.0"));    // api-version

            HttpWebRequest request = (HttpWebRequest)WebRequest.Create(requestUri);
            request.ContentType = "text/json";
            request.Method = "POST";

            // Create hello byte array that will become hello request body.
            string requestBody = "{\"Name\":\"fabric:/WordCount\"," +
                                    "\"TypeName\":\"WordCount\"," +
                                    "\"TypeVersion\":\"1.0.0\"," +
                                    "\"ParameterList\":[]}";
            byte[] requestBodyBytes = Encoding.UTF8.GetBytes(requestBody);
            request.ContentLength = requestBodyBytes.Length;

            // Create hello request body.
            try
            {
                using (Stream requestStream = request.GetRequestStream())
                {
                    requestStream.Write(requestBodyBytes, 0, requestBodyBytes.Length);
                    requestStream.Close();

                    // Execute hello request and obtain hello response.
                    using (HttpWebResponse response = (HttpWebResponse)request.GetResponse())
                    {
                        statusCode = response.StatusCode;
                    }
                }
            }
            catch (WebException e)
            {
                // If there is a web exception, display hello error message.
                Console.WriteLine("Error creating application:");
                Console.WriteLine(e.Message);
                if (e.InnerException != null)
                    Console.WriteLine(e.InnerException.Message);
                return false;
            }
            catch (Exception e)
            {
                // If there is another kind of exception, throw it.
                throw (e);
            }

            Console.WriteLine("Create Application response status = " + statusCode.ToString());

            return true;
        }

        #endregion


        #region Delete Application (REST API)

        /// <summary>
        /// Deletes an application.
        /// </summary>
        /// <param name="clusterUri">hello URI tooaccess hello cluster.</param>
        /// <returns>Returns true if successful; otherwise false.</returns>
        public static bool DeleteApplication(Uri clusterUri)
        {
            // Create hello request and add URL parameters.
            Uri requestUri = new Uri(clusterUri,
                string.Format("/Applications/{0}/$/Delete?api-version={1}",
                "WordCount",    // Application Name
                "1.0"));        // api-version

            HttpWebRequest request = (HttpWebRequest)WebRequest.Create(requestUri);
            request.Method = "POST";
            request.ContentLength = 0;

            // Stores hello response status code.
            HttpStatusCode statusCode;

            // Execute hello request and obtain hello response.
            try
            {
                using (HttpWebResponse response = (HttpWebResponse)request.GetResponse())
                {
                    statusCode = response.StatusCode;
                }
            }
            catch (WebException e)
            {
                // If there is a web exception, display hello error message.
                Console.WriteLine("Error deleting application:");
                Console.WriteLine(e.Message);
                if (e.InnerException != null)
                    Console.WriteLine(e.InnerException.Message);
                return false;
            }
            catch (Exception e)
            {
                // If there is another kind of exception, throw it.
                throw (e);
            }

            Console.WriteLine("Delete Application response status = " + statusCode.ToString());

            return true;
        }

        #endregion

        #region Upgrade Application by Application Type (REST API)

        /// <summary>
        /// Upgrades an application by application type.
        /// </summary>
        /// <param name="clusterUri">hello URI tooaccess hello cluster.</param>
        /// <returns>Returns true if successful; otherwise false.</returns>
        public static bool UpgradeApplicationByApplicationType(Uri clusterUri)
        {
            // String toocapture hello response stream.
            string responseString = string.Empty;

            // Stores hello response status code.
            HttpStatusCode statusCode;

            // Create hello request and add URL parameters.
            Uri requestUri = new Uri(clusterUri, string.Format("/Applications/{0}/$/Upgrade?api-version={1}",
                "WordCount",     // Application Name
                "1.0"));                // api-version

            HttpWebRequest request = (HttpWebRequest)WebRequest.Create(requestUri);
            request.ContentType = "text/json";
            request.Method = "POST";


            // Create hello Health Policy.
            string requestBody = "{\"Name\":\"fabric:/WordCount\"," +
                                    "\"TargetApplicationTypeVersion\":\"1.1.0\"," +
                                    "\"Parameters\":[]," +
                                    "\"UpgradeKind\":1," +
                                    "\"RollingUpgradeMode\":1," +
                                    "\"UpgradeReplicaSetCheckTimeoutInSeconds\":5," +
                                    "\"ForceRestart\":true," +
                                    "\"MonitoringPolicy\":" +
                                    "{\"FailureAction\":1," +
                                    "\"HealthCheckWaitDurationInMilliseconds\":\"5000\"," +
                                    "\"HealthCheckStableDurationInMilliseconds\":\"10000\"," +
                                    "\"HealthCheckRetryTimeoutInMilliseconds\":\"20000\"," +
                                    "\"UpgradeTimeoutInMilliseconds\":\"60000\"," +
                                    "\"UpgradeDomainTimeoutInMilliseconds\":\"30000\"}}";

            // Create hello byte array that will become hello request body.
            byte[] requestBodyBytes = Encoding.UTF8.GetBytes(requestBody);
            request.ContentLength = requestBodyBytes.Length;

            // Create hello request body.
            try
            {
                using (Stream requestStream = request.GetRequestStream())
                {
                    requestStream.Write(requestBodyBytes, 0, requestBodyBytes.Length);
                    requestStream.Close();

                    // Execute hello request and obtain hello response.
                    using (HttpWebResponse response = (HttpWebResponse)request.GetResponse())
                    {
                        statusCode = response.StatusCode;
                    }
                }
            }
            catch (WebException e)
            {
                // If there is a web exception, display hello error message.
                Console.WriteLine("Error upgrading application:");
                Console.WriteLine(e.Message);
                if (e.InnerException != null)
                    Console.WriteLine(e.InnerException.Message);
                return false;
            }
            catch (Exception e)
            {
                // If there is another kind of exception, throw it.
                throw (e);
            }

            Console.WriteLine("Update Application response status = " + statusCode.ToString());

            return true;
        }

        #endregion
    }
}
```


<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="088a5-145">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="088a5-145">Next steps</span></span>
[<span data-ttu-id="088a5-146">Cykl życia aplikacji w sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="088a5-146">Service Fabric application lifecycle</span></span>](service-fabric-application-lifecycle.md)

