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
# <a name="get-started-with-azure-data-lake-store-using-net-sdk"></a>Rozpoczynanie pracy z usługą Azure Data Lake Store z użyciem zestawu SDK .NET
> [!div class="op_single_selector"]
> * [Portal](data-lake-store-get-started-portal.md)
> * [PowerShell](data-lake-store-get-started-powershell.md)
> * [Zestaw SDK platformy .NET](data-lake-store-get-started-net-sdk.md)
> * [Zestaw SDK Java](data-lake-store-get-started-java-sdk.md)
> * [Interfejs API REST](data-lake-store-get-started-rest-api.md)
> * [Interfejs wiersza polecenia platformy Azure 2.0](data-lake-store-get-started-cli-2.0.md)
> * [Node.js](data-lake-store-manage-use-nodejs.md)
> * [Python](data-lake-store-get-started-python.md)
>
>

Dowiedz się, jak toouse hello [zestawu SDK usługi Azure Data Lake Store .NET](https://docs.microsoft.com/dotnet/api/overview/azure/data-lake-store?view=azure-dotnet) tooperform podstawowe operacje, takie jak tworzenie folderów, przekazywanie i pobieranie plików danych itp. Aby uzyskać więcej informacji o usłudze Data Lake, zobacz temat [Usługa Azure Data Lake Store](data-lake-store-overview.md).

## <a name="prerequisites"></a>Wymagania wstępne
* **Program Visual Studio w wersji 2013, 2015 lub 2017**. Poniższe instrukcje Hello Użyj Visual Studio 2015 Update 2.

* **Subskrypcja platformy Azure**. Zobacz temat [Uzyskiwanie bezpłatnej wersji próbnej platformy Azure](https://azure.microsoft.com/pricing/free-trial/).

* **Konto usługi Azure Data Lake Store**. Aby uzyskać instrukcje dotyczące toocreate konta, zobacz [wprowadzenie do usługi Azure Data Lake Store](data-lake-store-get-started-portal.md)

* **Utworzenie aplikacji usługi Azure Active Directory**. Używasz hello Azure AD aplikacji tooauthenticate hello usługi Data Lake Store aplikacji z usługą Azure AD. Istnieją różne podejścia tooauthenticate z usługą Azure AD, które są **uwierzytelniania użytkowników końcowych** lub **do usługi uwierzytelniania**. Aby uzyskać instrukcje i więcej informacji na temat tooauthenticate, zobacz [uwierzytelniania użytkowników końcowych](data-lake-store-end-user-authenticate-using-active-directory.md) lub [do usługi uwierzytelniania](data-lake-store-authenticate-using-active-directory.md).

## <a name="create-a-net-application"></a>Tworzenie aplikacji .NET
1. Otwórz program Visual Studio i utwórz aplikację konsolową.
2. Z hello **pliku** menu, kliknij przycisk **nowy**, a następnie kliknij przycisk **projektu**.
3. Z **nowy projekt**, wpisz lub wybierz hello następujące wartości:

   | Właściwość | Wartość |
   | --- | --- |
   | Kategoria |Szablony/Visual C#/Windows |
   | Szablon |Aplikacja konsolowa |
   | Nazwa |CreateADLApplication |
4. Kliknij przycisk **OK** toocreate hello projektu.
5. Dodaj projekt tooyour pakiety Nuget hello.

   1. Kliknij prawym przyciskiem myszy nazwę projektu hello w Eksploratorze rozwiązań hello, a następnie kliknij przycisk **Zarządzaj pakietami NuGet**.
   2. W hello **Menedżera pakietów Nuget** karcie, upewnij się, że **źródła pakietu** ustawiono zbyt**nuget.org** i **Uwzględnij wersję wstępną** pole wyboru jest zaznaczone.
   3. Wyszukaj i zainstaluj następujące pakiety NuGet hello:

      * `Microsoft.Azure.Management.DataLake.Store` — w tym samouczku jest używana wersja v2.1.3-preview.
      * `Microsoft.Rest.ClientRuntime.Azure.Authentication` — w tym samouczku jest używana wersja v2.2.12.

        ![Dodawanie źródła pakietów Nuget](./media/data-lake-store-get-started-net-sdk/data-lake-store-install-nuget-package.png "Tworzenie nowego konta usługi Azure Data Lake")
   4. Zamknij hello **Menedżera pakietów Nuget**.
6. Otwórz **Program.cs**, usuń istniejący kod hello, a następnie dołącz hello następujące instrukcje tooadd odwołania toonamespaces.

        using System;
        using System.IO;
        using System.Security.Cryptography.X509Certificates; // Required only if you are using an Azure AD application created with certificates
        using System.Threading;

        using Microsoft.Azure.Management.DataLake.Store;
        using Microsoft.Azure.Management.DataLake.Store.Models;
        using Microsoft.IdentityModel.Clients.ActiveDirectory;
        using Microsoft.Rest.Azure.Authentication;

7. Zadeklaruj zmienne hello, jak pokazano poniżej i podaj hello wartości nazwy usługi Data Lake Store i hello Nazwa grupy zasobów, która już istnieje. Ponadto upewnij się, że hello lokalna ścieżka i nazwa pliku podana tutaj musi istnieć na komputerze hello. Dodaj następujące fragment kodu po deklaracjach przestrzeni nazw hello hello.

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

W pozostałej części artykułu hello hello widać, jak toouse hello dostępne operacji tooperform metod .NET, takich jak uwierzytelnianie, przekazywanie plików itp.

## <a name="authentication"></a>Authentication

### <a name="if-you-are-using-end-user-authentication-recommended-for-this-tutorial"></a>Jeśli używasz uwierzytelniania użytkowników końcowych (zalecane w przypadku tego samouczka)

Za pomocą to istniejących tooauthenticate natywnych aplikacji usługi Azure AD aplikacji **interaktywnie**, która oznacza, że będzie monitowany tooenter poświadczenia platformy Azure.

Łatwość użycia, aby uzyskać poniższy fragment hello są używane wartości domyślne dla Identyfikatora klienta oraz identyfikatora URI, który będzie działać z dowolnej subskrypcji platformy Azure przekierowania. toohelp szybciej wykonania kroków tego samouczka, zaleca się posłuż się tą metodą. Poniższy fragment hello wystarczy podać wartość powitania dla swojego identyfikatora dzierżawcy. Możesz pobrać go za pomocą instrukcji hello na [tworzenie aplikacji usługi Active Directory](data-lake-store-end-user-authenticate-using-active-directory.md).

    // User login via interactive popup
    // Use hello client ID of an existing AAD Web application.
    SynchronizationContext.SetSynchronizationContext(new SynchronizationContext());
    var tenant_id = "<AAD_tenant_id>"; // Replace this string with hello user's Azure Active Directory tenant ID
    var nativeClientApp_clientId = "1950a258-227b-4e31-a9cf-717495945fc2";
    var activeDirectoryClientSettings = ActiveDirectoryClientSettings.UsePromptOnly(nativeClientApp_clientId, new Uri("urn:ietf:wg:oauth:2.0:oob"));
    var creds = UserTokenProvider.LoginWithPromptAsync(tenant_id, activeDirectoryClientSettings).Result;

Kilka rzeczy tooknow o ta Wstawka kodu powyżej:

* toohelp szybciej ukończenia samouczka hello, ta Wstawka kodu używa usługi Azure AD identyfikator domeny i klienta, który jest dostępny domyślnie dla wszystkich subskrypcji platformy Azure. Dzięki temu można **użyć tego fragmentu w aplikacji w niezmienionej formie**.
* Jednak jeśli chcesz toouse domenę usługi Azure AD i identyfikator klienta aplikacji, należy utworzyć aplikację native usługi Azure AD, a następnie użyj hello Azure AD dzierżawy ID, identyfikator klienta i identyfikator URI przekierowania dla aplikacji hello została utworzona. Instrukcje można znaleźć w temacie [Create an Active Directory Application for end-user authentication with Data Lake Store](data-lake-store-end-user-authenticate-using-active-directory.md) (Tworzenie aplikacji usługi Active Directory na potrzeby uwierzytelniania użytkownika końcowego przy użyciu usługi Data Lake Store).

### <a name="if-you-are-using-service-to-service-authentication-with-client-secret"></a>Jeśli używasz uwierzytelniania między usługami z kluczem tajnym klienta
Witaj następujący fragment kodu mogą być używane tooauthenticate aplikacji **nieinteraktywnie**, przy użyciu klucza tajnego klienta hello / klucz dla aplikacji / usługi podmiot zabezpieczeń. Użyj tej metody wraz z istniejącą aplikacją sieci Web usługi Azure AD. Aby uzyskać instrukcje dotyczące sposobu aplikacji sieci web toocreate hello Azure AD i jak tooretrieve hello identyfikator klienta i klucz tajny klienta wymagane we fragmencie hello poniżej, zobacz [tworzenie aplikacji usługi Active Directory do usługi uwierzytelniania z danymi Lake — magazyn](data-lake-store-authenticate-using-active-directory.md).

    // Service principal / appplication authentication with client secret / key
    // Use hello client ID of an existing AAD "Web App" application.
    SynchronizationContext.SetSynchronizationContext(new SynchronizationContext());

    var domain = "<AAD-directory-domain>";
    var webApp_clientId = "<AAD-application-clientid>";
    var clientSecret = "<AAD-application-client-secret>";
    var clientCredential = new ClientCredential(webApp_clientId, clientSecret);
    var creds = await ApplicationTokenProvider.LoginSilentAsync(domain, clientCredential);

### <a name="if-you-are-using-service-to-service-authentication-with-certificate"></a>Jeśli używasz uwierzytelniania między usługami z certyfikatem

Jak trzecia opcja hello następujący fragment kodu może być używane tooauthenticate aplikacji **nieinteraktywnie**, dla aplikacji usługi Azure Active Directory przy użyciu certyfikatu hello / service principal. Użyj tej metody wraz z istniejącą [aplikacją usługi Azure AD z certyfikatami](../azure-resource-manager/resource-group-authenticate-service-principal.md).

    // Service principal / application authentication with certificate
    // Use hello client ID and certificate of an existing AAD "Web App" application.
    SynchronizationContext.SetSynchronizationContext(new SynchronizationContext());

    var domain = "<AAD-directory-domain>";
    var webApp_clientId = "<AAD-application-clientid>";
    var clientCert = <AAD-application-client-certificate>
    var clientAssertionCertificate = new ClientAssertionCertificate(webApp_clientId, clientCert);
    var creds = await ApplicationTokenProvider.LoginSilentWithCertificateAsync(domain, clientAssertionCertificate);

## <a name="create-client-objects"></a>Tworzenie obiektów klienta
Hello następujący fragment kodu tworzy konto usługi Data Lake Store hello i systemie plików obiektów klienta, które są używane tooissue żądań toohello usługi.

    // Create client objects and set hello subscription ID
    _adlsClient = new DataLakeStoreAccountManagementClient(creds) { SubscriptionId = _subId };
    _adlsFileSystemClient = new DataLakeStoreFileSystemManagementClient(creds);

## <a name="list-all-data-lake-store-accounts-within-a-subscription"></a>Wyświetlanie listy wszystkich kont usługi Data Lake Store w ramach subskrypcji
Witaj następujący fragment kodu zawiera listę wszystkich kont usługi Data Lake Store w ramach danej subskrypcji Azure.

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

## <a name="create-a-directory"></a>Tworzenie katalogu
powitania po fragment kodu przedstawia `CreateDirectory` metody, której można toocreate katalogu w ramach konta usługi Data Lake Store.

    // Create a directory
    public static async Task CreateDirectory(string path)
    {
        await _adlsFileSystemClient.FileSystem.MkdirsAsync(_adlsAccountName, path);
    }

## <a name="upload-a-file"></a>Przekazywanie pliku
powitania po fragment kodu przedstawia `UploadFile` metody, których można używać tooupload pliki tooa konta usługi Data Lake Store.

    // Upload a file
    public static void UploadFile(string srcFilePath, string destFilePath, bool force = true)
    {
        _adlsFileSystemClient.FileSystem.UploadFile(_adlsAccountName, srcFilePath, destFilePath, overwrite:force);
    }

Witaj zestaw SDK obsługuje cyklicznego przekazywanie i pobieranie między ścieżkę do pliku lokalnego i ścieżka pliku usługi Data Lake Store.    

## <a name="get-file-or-directory-info"></a>Uzyskiwanie informacji o pliku lub katalogu
powitania po fragment kodu przedstawia `GetItemInfo` metody, której można tooretrieve informacji o pliku lub katalogu dostępnym w usłudze Data Lake Store.

    // Get file or directory info
    public static async Task<FileStatusProperties> GetItemInfo(string path)
    {
        return await _adlsFileSystemClient.FileSystem.GetFileStatusAsync(_adlsAccountName, path).FileStatus;
    }

## <a name="list-file-or-directories"></a>Wyświetlanie listy plików lub katalogów
powitania po fragment kodu przedstawia `ListItem` metodę, której można użyć toolist hello plików i katalogów w ramach konta usługi Data Lake Store.

    // List files and directories
    public static List<FileStatusProperties> ListItems(string directoryPath)
    {
        return _adlsFileSystemClient.FileSystem.ListFileStatus(_adlsAccountName, directoryPath).FileStatuses.FileStatus.ToList();
    }

## <a name="concatenate-files"></a>Łączenie plików
powitania po fragment kodu przedstawia `ConcatenateFiles` metody, aby używać tooconcatenate plików.

    // Concatenate files
    public static Task ConcatenateFiles(string[] srcFilePaths, string destFilePath)
    {
        await _adlsFileSystemClient.FileSystem.ConcatAsync(_adlsAccountName, destFilePath, srcFilePaths);
    }

## <a name="append-tooa-file"></a>Dołącz plik tooa
powitania po fragment kodu przedstawia `AppendToFile` używanej metody Dołącz plik tooa danych przechowywanych w konto usługi Data Lake Store.

    // Append toofile
    public static async Task AppendToFile(string path, string content)
    {
        using (var stream = new MemoryStream(Encoding.UTF8.GetBytes(content)))
        {
            await _adlsFileSystemClient.FileSystem.AppendAsync(_adlsAccountName, path, stream);
        }
    }

## <a name="download-a-file"></a>Pobieranie pliku
powitania po fragment kodu przedstawia `DownloadFile` metoda użycie toodownload plik z konta usługi Data Lake Store.

    // Download file
    public static void DownloadFile(string srcFilePath, string destFilePath)
    {
         _adlsFileSystemClient.FileSystem.DownloadFile(_adlsAccountName, srcFilePath, destFilePath);
    }

## <a name="next-steps"></a>Następne kroki
* [Zabezpieczanie danych w usłudze Data Lake Store](data-lake-store-secure-data.md)
* [Korzystanie z usługi Azure Data Lake Analytics z usługą Data Lake Store](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [Korzystanie z usługi Azure HDInsight z usługą Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md)
* [Dokumentacja zestawu SDK .NET usługi Data Lake Store](https://docs.microsoft.com/dotnet/api/?view=azuremgmtdatalakestore-2.1.0-preview&term=DataLake.Store)
* [Dokumentacja interfejsu REST usługi Data Lake Store](https://msdn.microsoft.com/library/mt693424.aspx)
