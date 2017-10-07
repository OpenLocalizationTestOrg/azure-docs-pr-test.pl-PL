---
title: "aaaUse hello zestawu .NET SDK toodevelop aplikacji w usłudze Azure Data Lake Store | Dokumentacja firmy Microsoft"
description: "Użyj zestawu SDK usługi Azure Data Lake Store .NET toocreate konto usługi Data Lake Store i wykonywać podstawowe operacje w hello usługi Data Lake Store"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: ea57d5a9-2929-4473-9d30-08227912aba7
ms.service: data-lake-store
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/09/2017
ms.author: nitinme
ms.openlocfilehash: cb3a1dfb2f6379f728069d66b0ee77ce0f838fe7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-store-using-net-sdk"></a><span data-ttu-id="98dd0-103">Rozpoczynanie pracy z usługą Azure Data Lake Store z użyciem zestawu SDK .NET</span><span class="sxs-lookup"><span data-stu-id="98dd0-103">Get started with Azure Data Lake Store using .NET SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="98dd0-104">Portal</span><span class="sxs-lookup"><span data-stu-id="98dd0-104">Portal</span></span>](data-lake-store-get-started-portal.md)
> * [<span data-ttu-id="98dd0-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="98dd0-105">PowerShell</span></span>](data-lake-store-get-started-powershell.md)
> * [<span data-ttu-id="98dd0-106">Zestaw SDK platformy .NET</span><span class="sxs-lookup"><span data-stu-id="98dd0-106">.NET SDK</span></span>](data-lake-store-get-started-net-sdk.md)
> * [<span data-ttu-id="98dd0-107">Zestaw SDK Java</span><span class="sxs-lookup"><span data-stu-id="98dd0-107">Java SDK</span></span>](data-lake-store-get-started-java-sdk.md)
> * [<span data-ttu-id="98dd0-108">Interfejs API REST</span><span class="sxs-lookup"><span data-stu-id="98dd0-108">REST API</span></span>](data-lake-store-get-started-rest-api.md)
> * [<span data-ttu-id="98dd0-109">Interfejs wiersza polecenia platformy Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="98dd0-109">Azure CLI 2.0</span></span>](data-lake-store-get-started-cli-2.0.md)
> * [<span data-ttu-id="98dd0-110">Node.js</span><span class="sxs-lookup"><span data-stu-id="98dd0-110">Node.js</span></span>](data-lake-store-manage-use-nodejs.md)
> * [<span data-ttu-id="98dd0-111">Python</span><span class="sxs-lookup"><span data-stu-id="98dd0-111">Python</span></span>](data-lake-store-get-started-python.md)
>
>

<span data-ttu-id="98dd0-112">Dowiedz się, jak toouse hello [zestawu SDK usługi Azure Data Lake Store .NET](https://docs.microsoft.com/dotnet/api/overview/azure/data-lake-store?view=azure-dotnet) tooperform podstawowe operacje, takie jak tworzenie folderów, przekazywanie i pobieranie plików danych itp. Aby uzyskać więcej informacji o usłudze Data Lake, zobacz temat [Usługa Azure Data Lake Store](data-lake-store-overview.md).</span><span class="sxs-lookup"><span data-stu-id="98dd0-112">Learn how toouse hello [Azure Data Lake Store .NET SDK](https://docs.microsoft.com/dotnet/api/overview/azure/data-lake-store?view=azure-dotnet) tooperform basic operations such as create folders, upload and download data files, etc. For more information about Data Lake, see [Azure Data Lake Store](data-lake-store-overview.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="98dd0-113">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="98dd0-113">Prerequisites</span></span>
* <span data-ttu-id="98dd0-114">**Program Visual Studio w wersji 2013, 2015 lub 2017**.</span><span class="sxs-lookup"><span data-stu-id="98dd0-114">**Visual Studio 2013, 2015, or 2017**.</span></span> <span data-ttu-id="98dd0-115">Poniższe instrukcje Hello Użyj Visual Studio 2015 Update 2.</span><span class="sxs-lookup"><span data-stu-id="98dd0-115">hello instructions below use Visual Studio 2015 Update 2.</span></span>

* <span data-ttu-id="98dd0-116">**Subskrypcja platformy Azure**.</span><span class="sxs-lookup"><span data-stu-id="98dd0-116">**An Azure subscription**.</span></span> <span data-ttu-id="98dd0-117">Zobacz temat [Uzyskiwanie bezpłatnej wersji próbnej platformy Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="98dd0-117">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="98dd0-118">**Konto usługi Azure Data Lake Store**.</span><span class="sxs-lookup"><span data-stu-id="98dd0-118">**Azure Data Lake Store account**.</span></span> <span data-ttu-id="98dd0-119">Aby uzyskać instrukcje dotyczące toocreate konta, zobacz [wprowadzenie do usługi Azure Data Lake Store](data-lake-store-get-started-portal.md)</span><span class="sxs-lookup"><span data-stu-id="98dd0-119">For instructions on how toocreate an account, see [Get started with Azure Data Lake Store](data-lake-store-get-started-portal.md)</span></span>

* <span data-ttu-id="98dd0-120">**Utworzenie aplikacji usługi Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="98dd0-120">**Create an Azure Active Directory Application**.</span></span> <span data-ttu-id="98dd0-121">Używasz hello Azure AD aplikacji tooauthenticate hello usługi Data Lake Store aplikacji z usługą Azure AD.</span><span class="sxs-lookup"><span data-stu-id="98dd0-121">You use hello Azure AD application tooauthenticate hello Data Lake Store application with Azure AD.</span></span> <span data-ttu-id="98dd0-122">Istnieją różne podejścia tooauthenticate z usługą Azure AD, które są **uwierzytelniania użytkowników końcowych** lub **do usługi uwierzytelniania**.</span><span class="sxs-lookup"><span data-stu-id="98dd0-122">There are different approaches tooauthenticate with Azure AD, which are **end-user authentication** or **service-to-service authentication**.</span></span> <span data-ttu-id="98dd0-123">Aby uzyskać instrukcje i więcej informacji na temat tooauthenticate, zobacz [uwierzytelniania użytkowników końcowych](data-lake-store-end-user-authenticate-using-active-directory.md) lub [do usługi uwierzytelniania](data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="98dd0-123">For instructions and more information on how tooauthenticate, see [End-user authentication](data-lake-store-end-user-authenticate-using-active-directory.md) or [Service-to-service authentication](data-lake-store-authenticate-using-active-directory.md).</span></span>

## <a name="create-a-net-application"></a><span data-ttu-id="98dd0-124">Tworzenie aplikacji .NET</span><span class="sxs-lookup"><span data-stu-id="98dd0-124">Create a .NET application</span></span>
1. <span data-ttu-id="98dd0-125">Otwórz program Visual Studio i utwórz aplikację konsolową.</span><span class="sxs-lookup"><span data-stu-id="98dd0-125">Open Visual Studio and create a console application.</span></span>
2. <span data-ttu-id="98dd0-126">Z hello **pliku** menu, kliknij przycisk **nowy**, a następnie kliknij przycisk **projektu**.</span><span class="sxs-lookup"><span data-stu-id="98dd0-126">From hello **File** menu, click **New**, and then click **Project**.</span></span>
3. <span data-ttu-id="98dd0-127">Z **nowy projekt**, wpisz lub wybierz hello następujące wartości:</span><span class="sxs-lookup"><span data-stu-id="98dd0-127">From **New Project**, type or select hello following values:</span></span>

   | <span data-ttu-id="98dd0-128">Właściwość</span><span class="sxs-lookup"><span data-stu-id="98dd0-128">Property</span></span> | <span data-ttu-id="98dd0-129">Wartość</span><span class="sxs-lookup"><span data-stu-id="98dd0-129">Value</span></span> |
   | --- | --- |
   | <span data-ttu-id="98dd0-130">Kategoria</span><span class="sxs-lookup"><span data-stu-id="98dd0-130">Category</span></span> |<span data-ttu-id="98dd0-131">Szablony/Visual C#/Windows</span><span class="sxs-lookup"><span data-stu-id="98dd0-131">Templates/Visual C#/Windows</span></span> |
   | <span data-ttu-id="98dd0-132">Szablon</span><span class="sxs-lookup"><span data-stu-id="98dd0-132">Template</span></span> |<span data-ttu-id="98dd0-133">Aplikacja konsolowa</span><span class="sxs-lookup"><span data-stu-id="98dd0-133">Console Application</span></span> |
   | <span data-ttu-id="98dd0-134">Nazwa</span><span class="sxs-lookup"><span data-stu-id="98dd0-134">Name</span></span> |<span data-ttu-id="98dd0-135">CreateADLApplication</span><span class="sxs-lookup"><span data-stu-id="98dd0-135">CreateADLApplication</span></span> |
4. <span data-ttu-id="98dd0-136">Kliknij przycisk **OK** toocreate hello projektu.</span><span class="sxs-lookup"><span data-stu-id="98dd0-136">Click **OK** toocreate hello project.</span></span>
5. <span data-ttu-id="98dd0-137">Dodaj projekt tooyour pakiety Nuget hello.</span><span class="sxs-lookup"><span data-stu-id="98dd0-137">Add hello Nuget packages tooyour project.</span></span>

   1. <span data-ttu-id="98dd0-138">Kliknij prawym przyciskiem myszy nazwę projektu hello w Eksploratorze rozwiązań hello, a następnie kliknij przycisk **Zarządzaj pakietami NuGet**.</span><span class="sxs-lookup"><span data-stu-id="98dd0-138">Right-click hello project name in hello Solution Explorer and click **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="98dd0-139">W hello **Menedżera pakietów Nuget** karcie, upewnij się, że **źródła pakietu** ustawiono zbyt**nuget.org** i **Uwzględnij wersję wstępną** pole wyboru jest zaznaczone.</span><span class="sxs-lookup"><span data-stu-id="98dd0-139">In hello **Nuget Package Manager** tab, make sure that **Package source** is set too**nuget.org** and that **Include prerelease** check box is selected.</span></span>
   3. <span data-ttu-id="98dd0-140">Wyszukaj i zainstaluj następujące pakiety NuGet hello:</span><span class="sxs-lookup"><span data-stu-id="98dd0-140">Search for and install hello following NuGet packages:</span></span>

      * <span data-ttu-id="98dd0-141">`Microsoft.Azure.Management.DataLake.Store` — w tym samouczku jest używana wersja v2.1.3-preview.</span><span class="sxs-lookup"><span data-stu-id="98dd0-141">`Microsoft.Azure.Management.DataLake.Store` - This tutorial uses v2.1.3-preview.</span></span>
      * <span data-ttu-id="98dd0-142">`Microsoft.Rest.ClientRuntime.Azure.Authentication` — w tym samouczku jest używana wersja v2.2.12.</span><span class="sxs-lookup"><span data-stu-id="98dd0-142">`Microsoft.Rest.ClientRuntime.Azure.Authentication` - This tutorial uses v2.2.12.</span></span>

        <span data-ttu-id="98dd0-143">![Dodawanie źródła pakietów Nuget](./media/data-lake-store-get-started-net-sdk/data-lake-store-install-nuget-package.png "Tworzenie nowego konta usługi Azure Data Lake")</span><span class="sxs-lookup"><span data-stu-id="98dd0-143">![Add a Nuget source](./media/data-lake-store-get-started-net-sdk/data-lake-store-install-nuget-package.png "Create a new Azure Data Lake account")</span></span>
   4. <span data-ttu-id="98dd0-144">Zamknij hello **Menedżera pakietów Nuget**.</span><span class="sxs-lookup"><span data-stu-id="98dd0-144">Close hello **Nuget Package Manager**.</span></span>
6. <span data-ttu-id="98dd0-145">Otwórz **Program.cs**, usuń istniejący kod hello, a następnie dołącz hello następujące instrukcje tooadd odwołania toonamespaces.</span><span class="sxs-lookup"><span data-stu-id="98dd0-145">Open **Program.cs**, delete hello existing code, and then include hello following statements tooadd references toonamespaces.</span></span>

        using System;
        using System.IO;
        using System.Security.Cryptography.X509Certificates; // Required only if you are using an Azure AD application created with certificates
        using System.Threading;

        using Microsoft.Azure.Management.DataLake.Store;
        using Microsoft.Azure.Management.DataLake.Store.Models;
        using Microsoft.IdentityModel.Clients.ActiveDirectory;
        using Microsoft.Rest.Azure.Authentication;

7. <span data-ttu-id="98dd0-146">Zadeklaruj zmienne hello, jak pokazano poniżej i podaj hello wartości nazwy usługi Data Lake Store i hello Nazwa grupy zasobów, która już istnieje.</span><span class="sxs-lookup"><span data-stu-id="98dd0-146">Declare hello variables as shown below, and provide hello values for Data Lake Store name and hello resource group name that already exist.</span></span> <span data-ttu-id="98dd0-147">Ponadto upewnij się, że hello lokalna ścieżka i nazwa pliku podana tutaj musi istnieć na komputerze hello.</span><span class="sxs-lookup"><span data-stu-id="98dd0-147">Also, make sure hello local path and file name you provide here must exist on hello computer.</span></span> <span data-ttu-id="98dd0-148">Dodaj następujące fragment kodu po deklaracjach przestrzeni nazw hello hello.</span><span class="sxs-lookup"><span data-stu-id="98dd0-148">Add hello following code snippet after hello namespace declarations.</span></span>

        namespace SdkSample
        {
            class Program
            {
                private static DataLakeStoreAccountManagementClient _adlsClient;
                private static DataLakeStoreFileSystemManagementClient _adlsFileSystemClient;

                private static string _adlsAccountName;
                private static string _resourceGroupName;
                private static string _location;
                private static string _subId;

                private static void Main(string[] args)
                {
                    _adlsAccountName = "<DATA-LAKE-STORE-NAME>"; // TODO: Replace this value with hello name of your existing Data Lake Store account.
                    _resourceGroupName = "<RESOURCE-GROUP-NAME>"; // TODO: Replace this value with hello name of hello resource group containing your Data Lake Store account.
                    _location = "East US 2";
                    _subId = "<SUBSCRIPTION-ID>";

                    string localFolderPath = @"C:\local_path\"; // TODO: Make sure this exists and can be overwritten.
                    string localFilePath = Path.Combine(localFolderPath, "file.txt"); // TODO: Make sure this exists and can be overwritten.
                    string remoteFolderPath = "/data_lake_path/";
                    string remoteFilePath = Path.Combine(remoteFolderPath, "file.txt");
                }
            }
        }

<span data-ttu-id="98dd0-149">W pozostałej części artykułu hello hello widać, jak toouse hello dostępne operacji tooperform metod .NET, takich jak uwierzytelnianie, przekazywanie plików itp.</span><span class="sxs-lookup"><span data-stu-id="98dd0-149">In hello remaining sections of hello article, you can see how toouse hello available .NET methods tooperform operations such as authentication, file upload, etc.</span></span>

## <a name="authentication"></a><span data-ttu-id="98dd0-150">Authentication</span><span class="sxs-lookup"><span data-stu-id="98dd0-150">Authentication</span></span>

### <a name="if-you-are-using-end-user-authentication-recommended-for-this-tutorial"></a><span data-ttu-id="98dd0-151">Jeśli używasz uwierzytelniania użytkowników końcowych (zalecane w przypadku tego samouczka)</span><span class="sxs-lookup"><span data-stu-id="98dd0-151">If you are using end-user authentication (recommended for this tutorial)</span></span>

<span data-ttu-id="98dd0-152">Za pomocą to istniejących tooauthenticate natywnych aplikacji usługi Azure AD aplikacji **interaktywnie**, która oznacza, że będzie monitowany tooenter poświadczenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="98dd0-152">Use this with an existing Azure AD native application tooauthenticate your application **interactively**, which means you will be prompted tooenter your Azure credentials.</span></span>

<span data-ttu-id="98dd0-153">Łatwość użycia, aby uzyskać poniższy fragment hello są używane wartości domyślne dla Identyfikatora klienta oraz identyfikatora URI, który będzie działać z dowolnej subskrypcji platformy Azure przekierowania.</span><span class="sxs-lookup"><span data-stu-id="98dd0-153">For ease of use, hello snippet below uses default values for client ID and redirect URI that will work with any Azure subscription.</span></span> <span data-ttu-id="98dd0-154">toohelp szybciej wykonania kroków tego samouczka, zaleca się posłuż się tą metodą.</span><span class="sxs-lookup"><span data-stu-id="98dd0-154">toohelp you complete this tutorial faster, we recommend you use this approach.</span></span> <span data-ttu-id="98dd0-155">Poniższy fragment hello wystarczy podać wartość powitania dla swojego identyfikatora dzierżawcy.</span><span class="sxs-lookup"><span data-stu-id="98dd0-155">In hello snippet below, just provide hello value for your tenant ID.</span></span> <span data-ttu-id="98dd0-156">Możesz pobrać go za pomocą instrukcji hello na [tworzenie aplikacji usługi Active Directory](data-lake-store-end-user-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="98dd0-156">You can retrieve it using hello instructions provided at [Create an Active Directory Application](data-lake-store-end-user-authenticate-using-active-directory.md).</span></span>

    // User login via interactive popup
    // Use hello client ID of an existing AAD Web application.
    SynchronizationContext.SetSynchronizationContext(new SynchronizationContext());
    var tenant_id = "<AAD_tenant_id>"; // Replace this string with hello user's Azure Active Directory tenant ID
    var nativeClientApp_clientId = "1950a258-227b-4e31-a9cf-717495945fc2";
    var activeDirectoryClientSettings = ActiveDirectoryClientSettings.UsePromptOnly(nativeClientApp_clientId, new Uri("urn:ietf:wg:oauth:2.0:oob"));
    var creds = UserTokenProvider.LoginWithPromptAsync(tenant_id, activeDirectoryClientSettings).Result;

<span data-ttu-id="98dd0-157">Kilka rzeczy tooknow o ta Wstawka kodu powyżej:</span><span class="sxs-lookup"><span data-stu-id="98dd0-157">A couple of things tooknow about this snippet above:</span></span>

* <span data-ttu-id="98dd0-158">toohelp szybciej ukończenia samouczka hello, ta Wstawka kodu używa usługi Azure AD identyfikator domeny i klienta, który jest dostępny domyślnie dla wszystkich subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="98dd0-158">toohelp you complete hello tutorial faster, this snippet uses an an Azure AD domain and client ID that is available by default for all Azure subscriptions.</span></span> <span data-ttu-id="98dd0-159">Dzięki temu można **użyć tego fragmentu w aplikacji w niezmienionej formie**.</span><span class="sxs-lookup"><span data-stu-id="98dd0-159">So, you can **use this snippet as-is in your application**.</span></span>
* <span data-ttu-id="98dd0-160">Jednak jeśli chcesz toouse domenę usługi Azure AD i identyfikator klienta aplikacji, należy utworzyć aplikację native usługi Azure AD, a następnie użyj hello Azure AD dzierżawy ID, identyfikator klienta i identyfikator URI przekierowania dla aplikacji hello została utworzona.</span><span class="sxs-lookup"><span data-stu-id="98dd0-160">However, if you do want toouse your own Azure AD domain and application client ID, you must create an Azure AD native application and then use hello Azure AD tenant ID, client ID, and redirect URI for hello application you created.</span></span> <span data-ttu-id="98dd0-161">Instrukcje można znaleźć w temacie [Create an Active Directory Application for end-user authentication with Data Lake Store](data-lake-store-end-user-authenticate-using-active-directory.md) (Tworzenie aplikacji usługi Active Directory na potrzeby uwierzytelniania użytkownika końcowego przy użyciu usługi Data Lake Store).</span><span class="sxs-lookup"><span data-stu-id="98dd0-161">See [Create an Active Directory Application for end-user authentication with Data Lake Store](data-lake-store-end-user-authenticate-using-active-directory.md) for instructions.</span></span>

### <a name="if-you-are-using-service-to-service-authentication-with-client-secret"></a><span data-ttu-id="98dd0-162">Jeśli używasz uwierzytelniania między usługami z kluczem tajnym klienta</span><span class="sxs-lookup"><span data-stu-id="98dd0-162">If you are using service-to-service authentication with client secret</span></span>
<span data-ttu-id="98dd0-163">Witaj następujący fragment kodu mogą być używane tooauthenticate aplikacji **nieinteraktywnie**, przy użyciu klucza tajnego klienta hello / klucz dla aplikacji / usługi podmiot zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="98dd0-163">hello following snippet can be used tooauthenticate your application **non-interactively**, using hello client secret / key for an application / service principal.</span></span> <span data-ttu-id="98dd0-164">Użyj tej metody wraz z istniejącą aplikacją sieci Web usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="98dd0-164">Use this with an existing Azure AD "Web App" Application.</span></span> <span data-ttu-id="98dd0-165">Aby uzyskać instrukcje dotyczące sposobu aplikacji sieci web toocreate hello Azure AD i jak tooretrieve hello identyfikator klienta i klucz tajny klienta wymagane we fragmencie hello poniżej, zobacz [tworzenie aplikacji usługi Active Directory do usługi uwierzytelniania z danymi Lake — magazyn](data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="98dd0-165">For instructions on how toocreate hello Azure AD web application and how tooretrieve hello client ID and client secret required in hello snippet below, see [Create an Active Directory Application for service-to-service authentication with Data Lake Store](data-lake-store-authenticate-using-active-directory.md).</span></span>

    // Service principal / appplication authentication with client secret / key
    // Use hello client ID of an existing AAD "Web App" application.
    SynchronizationContext.SetSynchronizationContext(new SynchronizationContext());

    var domain = "<AAD-directory-domain>";
    var webApp_clientId = "<AAD-application-clientid>";
    var clientSecret = "<AAD-application-client-secret>";
    var clientCredential = new ClientCredential(webApp_clientId, clientSecret);
    var creds = await ApplicationTokenProvider.LoginSilentAsync(domain, clientCredential);

### <a name="if-you-are-using-service-to-service-authentication-with-certificate"></a><span data-ttu-id="98dd0-166">Jeśli używasz uwierzytelniania między usługami z certyfikatem</span><span class="sxs-lookup"><span data-stu-id="98dd0-166">If you are using service-to-service authentication with certificate</span></span>

<span data-ttu-id="98dd0-167">Jak trzecia opcja hello następujący fragment kodu może być używane tooauthenticate aplikacji **nieinteraktywnie**, dla aplikacji usługi Azure Active Directory przy użyciu certyfikatu hello / service principal.</span><span class="sxs-lookup"><span data-stu-id="98dd0-167">As a third option, hello following snippet can be used tooauthenticate your application **non-interactively**, using hello certificate for an Azure Active Directory application / service principal.</span></span> <span data-ttu-id="98dd0-168">Użyj tej metody wraz z istniejącą [aplikacją usługi Azure AD z certyfikatami](../azure-resource-manager/resource-group-authenticate-service-principal.md).</span><span class="sxs-lookup"><span data-stu-id="98dd0-168">Use this with an existing [Azure AD Application with certificates](../azure-resource-manager/resource-group-authenticate-service-principal.md).</span></span>

    // Service principal / application authentication with certificate
    // Use hello client ID and certificate of an existing AAD "Web App" application.
    SynchronizationContext.SetSynchronizationContext(new SynchronizationContext());

    var domain = "<AAD-directory-domain>";
    var webApp_clientId = "<AAD-application-clientid>";
    var clientCert = <AAD-application-client-certificate>
    var clientAssertionCertificate = new ClientAssertionCertificate(webApp_clientId, clientCert);
    var creds = await ApplicationTokenProvider.LoginSilentWithCertificateAsync(domain, clientAssertionCertificate);

## <a name="create-client-objects"></a><span data-ttu-id="98dd0-169">Tworzenie obiektów klienta</span><span class="sxs-lookup"><span data-stu-id="98dd0-169">Create client objects</span></span>
<span data-ttu-id="98dd0-170">Hello następujący fragment kodu tworzy konto usługi Data Lake Store hello i systemie plików obiektów klienta, które są używane tooissue żądań toohello usługi.</span><span class="sxs-lookup"><span data-stu-id="98dd0-170">hello following snippet creates hello Data Lake Store account and filesystem client objects, which are used tooissue requests toohello service.</span></span>

    // Create client objects and set hello subscription ID
    _adlsClient = new DataLakeStoreAccountManagementClient(creds) { SubscriptionId = _subId };
    _adlsFileSystemClient = new DataLakeStoreFileSystemManagementClient(creds);

## <a name="list-all-data-lake-store-accounts-within-a-subscription"></a><span data-ttu-id="98dd0-171">Wyświetlanie listy wszystkich kont usługi Data Lake Store w ramach subskrypcji</span><span class="sxs-lookup"><span data-stu-id="98dd0-171">List all Data Lake Store accounts within a subscription</span></span>
<span data-ttu-id="98dd0-172">Witaj następujący fragment kodu zawiera listę wszystkich kont usługi Data Lake Store w ramach danej subskrypcji Azure.</span><span class="sxs-lookup"><span data-stu-id="98dd0-172">hello following snippet lists all Data Lake Store accounts within a given Azure subscription.</span></span>

    // List all ADLS accounts within hello subscription
    public static async Task<List<DataLakeStoreAccount>> ListAdlStoreAccounts()
    {
        var response = await _adlsClient.Account.ListAsync();
        var accounts = new List<DataLakeStoreAccount>(response);

        while (response.NextPageLink != null)
        {
            response = _adlsClient.Account.ListNext(response.NextPageLink);
            accounts.AddRange(response);
        }

        return accounts;
    }

## <a name="create-a-directory"></a><span data-ttu-id="98dd0-173">Tworzenie katalogu</span><span class="sxs-lookup"><span data-stu-id="98dd0-173">Create a directory</span></span>
<span data-ttu-id="98dd0-174">powitania po fragment kodu przedstawia `CreateDirectory` metody, której można toocreate katalogu w ramach konta usługi Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="98dd0-174">hello following snippet shows a `CreateDirectory` method that you can use toocreate a directory within a Data Lake Store account.</span></span>

    // Create a directory
    public static async Task CreateDirectory(string path)
    {
        await _adlsFileSystemClient.FileSystem.MkdirsAsync(_adlsAccountName, path);
    }

## <a name="upload-a-file"></a><span data-ttu-id="98dd0-175">Przekazywanie pliku</span><span class="sxs-lookup"><span data-stu-id="98dd0-175">Upload a file</span></span>
<span data-ttu-id="98dd0-176">powitania po fragment kodu przedstawia `UploadFile` metody, których można używać tooupload pliki tooa konta usługi Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="98dd0-176">hello following snippet shows an `UploadFile` method that you can use tooupload files tooa Data Lake Store account.</span></span>

    // Upload a file
    public static void UploadFile(string srcFilePath, string destFilePath, bool force = true)
    {
        _adlsFileSystemClient.FileSystem.UploadFile(_adlsAccountName, srcFilePath, destFilePath, overwrite:force);
    }

<span data-ttu-id="98dd0-177">Witaj zestaw SDK obsługuje cyklicznego przekazywanie i pobieranie między ścieżkę do pliku lokalnego i ścieżka pliku usługi Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="98dd0-177">hello SDK supports recursive upload and download between a local file path and a Data Lake Store file path.</span></span>    

## <a name="get-file-or-directory-info"></a><span data-ttu-id="98dd0-178">Uzyskiwanie informacji o pliku lub katalogu</span><span class="sxs-lookup"><span data-stu-id="98dd0-178">Get file or directory info</span></span>
<span data-ttu-id="98dd0-179">powitania po fragment kodu przedstawia `GetItemInfo` metody, której można tooretrieve informacji o pliku lub katalogu dostępnym w usłudze Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="98dd0-179">hello following snippet shows a `GetItemInfo` method that you can use tooretrieve information about a file or directory available in Data Lake Store.</span></span>

    // Get file or directory info
    public static async Task<FileStatusProperties> GetItemInfo(string path)
    {
        return await _adlsFileSystemClient.FileSystem.GetFileStatusAsync(_adlsAccountName, path).FileStatus;
    }

## <a name="list-file-or-directories"></a><span data-ttu-id="98dd0-180">Wyświetlanie listy plików lub katalogów</span><span class="sxs-lookup"><span data-stu-id="98dd0-180">List file or directories</span></span>
<span data-ttu-id="98dd0-181">powitania po fragment kodu przedstawia `ListItem` metodę, której można użyć toolist hello plików i katalogów w ramach konta usługi Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="98dd0-181">hello following snippet shows a `ListItem` method that can use toolist hello file and directories in a Data Lake Store account.</span></span>

    // List files and directories
    public static List<FileStatusProperties> ListItems(string directoryPath)
    {
        return _adlsFileSystemClient.FileSystem.ListFileStatus(_adlsAccountName, directoryPath).FileStatuses.FileStatus.ToList();
    }

## <a name="concatenate-files"></a><span data-ttu-id="98dd0-182">Łączenie plików</span><span class="sxs-lookup"><span data-stu-id="98dd0-182">Concatenate files</span></span>
<span data-ttu-id="98dd0-183">powitania po fragment kodu przedstawia `ConcatenateFiles` metody, aby używać tooconcatenate plików.</span><span class="sxs-lookup"><span data-stu-id="98dd0-183">hello following snippet shows a `ConcatenateFiles` method that you use tooconcatenate files.</span></span>

    // Concatenate files
    public static Task ConcatenateFiles(string[] srcFilePaths, string destFilePath)
    {
        await _adlsFileSystemClient.FileSystem.ConcatAsync(_adlsAccountName, destFilePath, srcFilePaths);
    }

## <a name="append-tooa-file"></a><span data-ttu-id="98dd0-184">Dołącz plik tooa</span><span class="sxs-lookup"><span data-stu-id="98dd0-184">Append tooa file</span></span>
<span data-ttu-id="98dd0-185">powitania po fragment kodu przedstawia `AppendToFile` używanej metody Dołącz plik tooa danych przechowywanych w konto usługi Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="98dd0-185">hello following snippet shows a `AppendToFile` method that you use append data tooa file already stored in a Data Lake Store account.</span></span>

    // Append toofile
    public static async Task AppendToFile(string path, string content)
    {
        using (var stream = new MemoryStream(Encoding.UTF8.GetBytes(content)))
        {
            await _adlsFileSystemClient.FileSystem.AppendAsync(_adlsAccountName, path, stream);
        }
    }

## <a name="download-a-file"></a><span data-ttu-id="98dd0-186">Pobieranie pliku</span><span class="sxs-lookup"><span data-stu-id="98dd0-186">Download a file</span></span>
<span data-ttu-id="98dd0-187">powitania po fragment kodu przedstawia `DownloadFile` metoda użycie toodownload plik z konta usługi Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="98dd0-187">hello following snippet shows a `DownloadFile` method that you use toodownload a file from a Data Lake Store account.</span></span>

    // Download file
    public static void DownloadFile(string srcFilePath, string destFilePath)
    {
         _adlsFileSystemClient.FileSystem.DownloadFile(_adlsAccountName, srcFilePath, destFilePath);
    }

## <a name="next-steps"></a><span data-ttu-id="98dd0-188">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="98dd0-188">Next steps</span></span>
* [<span data-ttu-id="98dd0-189">Zabezpieczanie danych w usłudze Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="98dd0-189">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="98dd0-190">Korzystanie z usługi Azure Data Lake Analytics z usługą Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="98dd0-190">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="98dd0-191">Korzystanie z usługi Azure HDInsight z usługą Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="98dd0-191">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
* [<span data-ttu-id="98dd0-192">Dokumentacja zestawu SDK .NET usługi Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="98dd0-192">Data Lake Store .NET SDK Reference</span></span>](https://docs.microsoft.com/dotnet/api/?view=azuremgmtdatalakestore-2.1.0-preview&term=DataLake.Store)
* [<span data-ttu-id="98dd0-193">Dokumentacja interfejsu REST usługi Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="98dd0-193">Data Lake Store REST Reference</span></span>](https://msdn.microsoft.com/library/mt693424.aspx)
