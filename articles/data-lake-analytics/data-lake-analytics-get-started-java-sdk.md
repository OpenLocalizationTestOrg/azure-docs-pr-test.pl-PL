---
title: aplikacje toodevelop zestawu Java SDK Data Lake Analytics aaaUse | Dokumentacja firmy Microsoft
description: "Korzystanie z zestawu Java SDK usługi Azure Data Lake Analytics toodevelop aplikacji"
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: saveenr
editor: cgronlun
ms.assetid: 07830b36-2fe3-4809-a846-129cf67b6a9e
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/05/2016
ms.author: edmaca
ms.openlocfilehash: 0d975812fe659ed34ee9befd37ee7c0bf50d3414
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-analytics-using-java-sdk"></a><span data-ttu-id="ce18c-103">Rozpoczynanie pracy z usługą Azure Data Lake Analytics przy użyciu zestawu SDK języka Java</span><span class="sxs-lookup"><span data-stu-id="ce18c-103">Get started with Azure Data Lake Analytics using Java SDK</span></span>
[!INCLUDE [get-started-selector](../../includes/data-lake-analytics-selector-get-started.md)]

<span data-ttu-id="ce18c-104">Dowiedz się, jak toouse hello toocreate zestawu Java SDK usługi Azure Data Lake Analytics konta usługi Azure Data Lake i wykonywać podstawowe operacje, takie jak tworzenie folderów, przekazywanie i pobieranie plików danych, usuwanie konta i pracy z zadaniami.</span><span class="sxs-lookup"><span data-stu-id="ce18c-104">Learn how toouse hello Azure Data Lake Analytics Java SDK toocreate an Azure Data Lake account and perform basic operations such as create folders, upload and download data files, delete your account, and work with jobs.</span></span> <span data-ttu-id="ce18c-105">Aby uzyskać więcej informacji o usłudze Data Lake, zobacz [Azure Data Lake Analytics](data-lake-analytics-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ce18c-105">For more information about Data Lake, see [Azure Data Lake Analytics](data-lake-analytics-overview.md).</span></span>

<span data-ttu-id="ce18c-106">W tym samouczku utworzysz aplikacji konsoli Java, która zawiera przykłady typowych zadań administracyjnych, a także tworzenie danych testowych i przesyłania zadania.</span><span class="sxs-lookup"><span data-stu-id="ce18c-106">In this tutorial, you will develop a Java console application which contains samples of common administrative tasks as well as creating test data and submitting a job.</span></span>  <span data-ttu-id="ce18c-107">toogo za pośrednictwem hello obsługiwane tego samouczka przy użyciu innych narzędzi, kliknij karty hello na powitania górnej części tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="ce18c-107">toogo through hello same tutorial using other supported tools, click hello tabs on hello top of this section.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ce18c-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="ce18c-108">Prerequisites</span></span>
* <span data-ttu-id="ce18c-109">Zestaw Java Development Kit (JDK) 8 (z użyciem języka Java w wersji 1.8).</span><span class="sxs-lookup"><span data-stu-id="ce18c-109">Java Development Kit (JDK) 8 (using Java version 1.8).</span></span>
* <span data-ttu-id="ce18c-110">IntelliJ lub inne odpowiednie środowisko programistyczne Java.</span><span class="sxs-lookup"><span data-stu-id="ce18c-110">IntelliJ or another suitable Java development environment.</span></span> <span data-ttu-id="ce18c-111">Jest to opcjonalne, ale zalecane.</span><span class="sxs-lookup"><span data-stu-id="ce18c-111">This is optional but recommended.</span></span> <span data-ttu-id="ce18c-112">Poniższe instrukcje Hello jest używane środowisko IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="ce18c-112">hello instructions below use IntelliJ.</span></span>
* <span data-ttu-id="ce18c-113">**Subskrypcja platformy Azure**.</span><span class="sxs-lookup"><span data-stu-id="ce18c-113">**An Azure subscription**.</span></span> <span data-ttu-id="ce18c-114">Zobacz temat [Uzyskiwanie bezpłatnej wersji próbnej platformy Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ce18c-114">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="ce18c-115">Tworzenie aplikacji usługi Azure Active Directory (AAD) i pobieranie jej **identyfikatora klienta**, **identyfikatora dzierżawy** i **klucza**.</span><span class="sxs-lookup"><span data-stu-id="ce18c-115">Create an Azure Active Directory (AAD) application and retrieve its **Client ID**, **Tenant ID**, and **Key**.</span></span> <span data-ttu-id="ce18c-116">Aby uzyskać więcej informacji dotyczących usługi AAD aplikacji i instrukcje na temat tooget Identyfikatora klienta, zobacz [aplikacji usługi Active Directory Utwórz i nazwę główną usługi za pomocą portalu](../azure-resource-manager/resource-group-create-service-principal-portal.md).</span><span class="sxs-lookup"><span data-stu-id="ce18c-116">For more information about AAD applications and instructions on how tooget a client ID, see [Create Active Directory application and service principal using portal](../azure-resource-manager/resource-group-create-service-principal-portal.md).</span></span> <span data-ttu-id="ce18c-117">Hello odpowiedzi identyfikatora URI i klucz będzie także dostępna z portalu powitania po utworzeniu aplikacji hello utworzone i generowania kluczy.</span><span class="sxs-lookup"><span data-stu-id="ce18c-117">hello Reply URI and Key will also be available from hello portal once you have hello application created and key generated.</span></span>

## <a name="how-do-i-authenticate-using-azure-active-directory"></a><span data-ttu-id="ce18c-118">W jaki sposób uwierzytelniać za pomocą usługi Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ce18c-118">How do I authenticate using Azure Active Directory?</span></span>
<span data-ttu-id="ce18c-119">Poniższy fragment kodu Hello zawiera kod **nieinterakcyjnym** uwierzytelniania, gdzie hello aplikacja udostępnia własne poświadczenia.</span><span class="sxs-lookup"><span data-stu-id="ce18c-119">hello code snippet below provides code for **non-interactive** authentication, where hello application provides its own credentials.</span></span>

<span data-ttu-id="ce18c-120">Konieczne będzie toogive zasobów toocreate uprawnienia aplikacji na platformie Azure dla tego samouczka toowork.</span><span class="sxs-lookup"><span data-stu-id="ce18c-120">You will need toogive your application permission toocreate resources in Azure for this tutorial toowork.</span></span> <span data-ttu-id="ce18c-121">Jest **zdecydowanie zalecane jest** tylko nadaj tej grupie zasobów nowe, nieużywane i puste tooa uprawnienia aplikacji współautora w Twojej subskrypcji platformy Azure na potrzeby tego samouczka hello.</span><span class="sxs-lookup"><span data-stu-id="ce18c-121">It is **highly recommended** that you only give this application Contributor permissions tooa new, unused, and empty resource group in your Azure subscription for hello purposes of this tutorial.</span></span>

## <a name="create-a-java-application"></a><span data-ttu-id="ce18c-122">Tworzenie aplikacji Java</span><span class="sxs-lookup"><span data-stu-id="ce18c-122">Create a Java application</span></span>
1. <span data-ttu-id="ce18c-123">Otwórz środowisko IntelliJ i Utwórz nowy projekt języka Java przy użyciu hello **wiersza polecenia aplikacji** szablonu.</span><span class="sxs-lookup"><span data-stu-id="ce18c-123">Open IntelliJ and create a new Java project using hello **Command Line App** template.</span></span>
2. <span data-ttu-id="ce18c-124">Kliknij prawym przyciskiem myszy na projekt hello na powitania po lewej stronie ekranu, a następnie kliknij przycisk **dodać obsługę Framework**.</span><span class="sxs-lookup"><span data-stu-id="ce18c-124">Right-click on hello project on hello left-hand side of your screen and click **Add Framework Support**.</span></span> <span data-ttu-id="ce18c-125">Wybierz pozycję **Maven** i kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="ce18c-125">Choose **Maven** and click **OK**.</span></span>
3. <span data-ttu-id="ce18c-126">Witaj Otwórz nowo utworzony **"pom.xml"** i dodaj następujące fragment tekstu między hello hello  **\</version >** znacznika i hello  **\< /project >** tagu:</span><span class="sxs-lookup"><span data-stu-id="ce18c-126">Open hello newly created **"pom.xml"** file and add hello following snippet of text between hello **\</version>** tag and hello **\</project>** tag:</span></span>

    >[!NOTE]
    ><span data-ttu-id="ce18c-127">Ten krok jest tymczasowy do momentu hello zestawu SDK usługi Azure Data Lake Analytics jest dostępna w programie Maven.</span><span class="sxs-lookup"><span data-stu-id="ce18c-127">This step is temporary until hello Azure Data Lake Analytics SDK is available in Maven.</span></span> <span data-ttu-id="ce18c-128">Ten artykuł zostanie zaktualizowany po hello zestawu SDK jest dostępny w programie Maven.</span><span class="sxs-lookup"><span data-stu-id="ce18c-128">This article will be updated once hello SDK is available in Maven.</span></span> <span data-ttu-id="ce18c-129">Wszystkie przyszłe aktualizacje toothis zestawu SDK będą dostępne za pośrednictwem programu Maven.</span><span class="sxs-lookup"><span data-stu-id="ce18c-129">All future updates toothis SDK will be availble through Maven.</span></span>
    >

        <repositories>
            <repository>
                <id>adx-snapshots</id>
                <name>Azure ADX Snapshots</name>
                <url>http://adxsnapshots.azurewebsites.net/</url>
                <layout>default</layout>
                <snapshots>
                    <enabled>true</enabled>
                </snapshots>
            </repository>
            <repository>
                <id>oss-snapshots</id>
                <name>Open Source Snapshots</name>
                <url>https://oss.sonatype.org/content/repositories/snapshots/</url>
                <layout>default</layout>
                <snapshots>
                    <enabled>true</enabled>
                    <updatePolicy>always</updatePolicy>
                </snapshots>
            </repository>
        </repositories>
        <dependencies>
            <dependency>
                <groupId>com.microsoft.azure</groupId>
                <artifactId>azure-client-authentication</artifactId>
                <version>1.0.0-20160513.000802-24</version>
            </dependency>
            <dependency>
                <groupId>com.microsoft.azure</groupId>
                <artifactId>azure-client-runtime</artifactId>
                <version>1.0.0-20160513.000812-28</version>
            </dependency>
            <dependency>
                <groupId>com.microsoft.rest</groupId>
                <artifactId>client-runtime</artifactId>
                <version>1.0.0-20160513.000825-29</version>
            </dependency>
            <dependency>
                <groupId>com.microsoft.azure</groupId>
                <artifactId>azure-mgmt-datalake-store</artifactId>
                <version>1.0.0-SNAPSHOT</version>
            </dependency>
            <dependency>
                <groupId>com.microsoft.azure</groupId>
                <artifactId>azure-mgmt-datalake-analytics</artifactId>
                <version>1.0.0-SNAPSHOT</version>
            </dependency>
        </dependencies>
4. <span data-ttu-id="ce18c-130">Przejdź za**pliku**, następnie **ustawienia**, następnie **kompilacji**, **wykonywania**, **wdrożenia**.</span><span class="sxs-lookup"><span data-stu-id="ce18c-130">Go too**File**, then **Settings**, then **Build**, **Execution**, **Deployment**.</span></span> <span data-ttu-id="ce18c-131">Wybierz **narzędzi do kompilacji**, **Maven**, **importowania**.</span><span class="sxs-lookup"><span data-stu-id="ce18c-131">Select **Build Tools**, **Maven**, **Importing**.</span></span> <span data-ttu-id="ce18c-132">Następnie sprawdź **Import Maven projektów automatycznie**.</span><span class="sxs-lookup"><span data-stu-id="ce18c-132">Then check **Import Maven projects automatically**.</span></span>
5. <span data-ttu-id="ce18c-133">Otwórz **Main.java** i Zastąp hello istniejący blok kodu z hello następującego kodu.</span><span class="sxs-lookup"><span data-stu-id="ce18c-133">Open **Main.java** and replace hello existing code block with hello following code.</span></span> <span data-ttu-id="ce18c-134">Ponadto podaj hello wartości parametrów wywoływanych we fragmencie kodu hello, takich jak **localFolderPath**, **_adlaAccountName**, **_adlsAccountName**, **_ resourceGroupName** i zastąp symbole zastępcze **identyfikator klienta**, **klucz TAJNY klienta**, **identyfikator DZIERŻAWCY**, i  **Identyfikator SUBSKRYPCJI**.</span><span class="sxs-lookup"><span data-stu-id="ce18c-134">Also, provide hello values for parameters called out in hello code snippet, such as **localFolderPath**, **_adlaAccountName**, **_adlsAccountName**, **_resourceGroupName** and replace placeholders for **CLIENT-ID**, **CLIENT-SECRET**, **TENANT-ID**, and **SUBSCRIPTION-ID**.</span></span>

    <span data-ttu-id="ce18c-135">Ten kod przechodzi hello proces tworzenia konta usługi Data Lake Store i usługi Data Lake Analytics, tworzenie plików w magazynie hello uruchamiania zadania, pobieranie stanu zadania pobierania danych wyjściowych zadania i usunięcia konta hello.</span><span class="sxs-lookup"><span data-stu-id="ce18c-135">This code goes through hello process of creating Data Lake Store and Data Lake Analytics accounts, creating files in hello store, running a job, getting job status, downloading job output, and finally deleting hello account.</span></span>

   > [!NOTE]
   > <span data-ttu-id="ce18c-136">Obecnie jest to znany problem z hello Azure Data Lake usługi.</span><span class="sxs-lookup"><span data-stu-id="ce18c-136">There is currently a known issue with hello Azure Data Lake Service.</span></span>  <span data-ttu-id="ce18c-137">Jeśli hello Przykładowa aplikacja zostanie przerwane lub napotka błąd, może być konieczne toomanually delete hello usługi Data Lake Store i usługi Data Lake Analytics kontom hello skrypt tworzy.</span><span class="sxs-lookup"><span data-stu-id="ce18c-137">If hello sample app is interrupted or encounters an error, you may need toomanually delete hello Data Lake Store & Data Lake Analytics accounts that hello script creates.</span></span>  <span data-ttu-id="ce18c-138">Jeśli nie masz doświadczenia w obsłudze hello portalu, hello [zarządzania usługi Azure Data Lake Analytics przy użyciu portalu Azure](data-lake-analytics-manage-use-portal.md) przewodnik ułatwiają rozpoczęcie pracy.</span><span class="sxs-lookup"><span data-stu-id="ce18c-138">If you're not familiar with hello Portal, hello [Manage Azure Data Lake Analytics using Azure Portal](data-lake-analytics-manage-use-portal.md) guide will get you started.</span></span>
   >
   >

        package com.company;

        import com.microsoft.azure.CloudException;
        import com.microsoft.azure.credentials.ApplicationTokenCredentials;
        import com.microsoft.azure.management.datalake.store.*;
        import com.microsoft.azure.management.datalake.store.models.*;
        import com.microsoft.azure.management.datalake.analytics.*;
        import com.microsoft.azure.management.datalake.analytics.models.*;
        import com.microsoft.rest.credentials.ServiceClientCredentials;
        import java.io.*;
        import java.nio.charset.Charset;
        import java.nio.file.Files;
        import java.nio.file.Paths;
        import java.util.ArrayList;
        import java.util.UUID;
        import java.util.List;

        public class Main {
            private static String _adlsAccountName;
            private static String _adlaAccountName;
            private static String _resourceGroupName;
            private static String _location;

            private static String _tenantId;
            private static String _subId;
            private static String _clientId;
            private static String _clientSecret;

            private static DataLakeStoreAccountManagementClient _adlsClient;
            private static DataLakeStoreFileSystemManagementClient _adlsFileSystemClient;
            private static DataLakeAnalyticsAccountManagementClient _adlaClient;
            private static DataLakeAnalyticsJobManagementClient _adlaJobClient;
            private static DataLakeAnalyticsCatalogManagementClient _adlaCatalogClient;

            public static void main(String[] args) throws Exception {
                _adlsAccountName = "<DATA-LAKE-STORE-NAME>";
                _adlaAccountName = "<DATA-LAKE-ANALYTICS-NAME>";
                _resourceGroupName = "<RESOURCE-GROUP-NAME>";
                _location = "East US 2";

                _tenantId = "<TENANT-ID>";
                _subId =  "<SUBSCRIPTION-ID>";
                _clientId = "<CLIENT-ID>";

                _clientSecret = "<CLIENT-SECRET>"; // TODO: For production scenarios, we recommend that you replace this line with a more secure way of acquiring hello application client secret, rather than hard-coding it in hello source code.

                String localFolderPath = "C:\\local_path\\"; // TODO: Change this tooany unused, new, empty folder on your local machine.

                // Authenticate
                ApplicationTokenCredentials creds = new ApplicationTokenCredentials(_clientId, _tenantId, _clientSecret, null);
                SetupClients(creds);

                // Create Data Lake Store and Analytics accounts
                WaitForNewline("Authenticated.", "Creating NEW accounts.");
                CreateAccounts();
                WaitForNewline("Accounts created.", "Displaying accounts.");

                // List Data Lake Store and Analytics accounts that this app can access
                System.out.println(String.format("All ADL Store accounts that this app can access in subscription %s:", _subId));
                List<DataLakeStoreAccount> adlsListResult = _adlsClient.getAccountOperations().list().getBody();
                for (DataLakeStoreAccount acct : adlsListResult) {
                    System.out.println(acct.getName());
                }
                System.out.println(String.format("All ADL Analytics accounts that this app can access in subscription %s:", _subId));
                List<DataLakeAnalyticsAccount> adlaListResult = _adlaClient.getAccountOperations().list().getBody();
                for (DataLakeAnalyticsAccount acct : adlaListResult) {
                    System.out.println(acct.getName());
                }
                WaitForNewline("Accounts displayed.", "Creating files.");

                // Create a file in Data Lake Store: input1.csv
                // TODO: these change order in hello next patch
                byte[] bytesContents = "123,abc".getBytes();
                _adlsFileSystemClient.getFileSystemOperations().create(_adlsAccountName, "/input1.csv", bytesContents, true);

                WaitForNewline("File created.", "Submitting a job.");

                // Submit a job tooData Lake Analytics
                UUID jobId = SubmitJobByScript("@input =  EXTRACT Data string FROM \"/input1.csv\" USING Extractors.Csv(); OUTPUT @input too@\"/output1.csv\" USING Outputters.Csv();", "testJob");
                WaitForNewline("Job submitted.", "Getting job status.");

                // Wait for job completion and output job status
                System.out.println(String.format("Job status: %s", GetJobStatus(jobId)));
                System.out.println("Waiting for job completion.");
                WaitForJob(jobId);
                System.out.println(String.format("Job status: %s", GetJobStatus(jobId)));
                WaitForNewline("Job completed.", "Downloading job output.");

                // Download job output from Data Lake Store
                DownloadFile("/output1.csv", localFolderPath + "output1.csv");
                WaitForNewline("Job output downloaded.", "Deleting file.");

                // Delete file from Data Lake Store
                DeleteFile("/output1.csv");
                WaitForNewline("File deleted.", "Deleting account.");

                // Delete account
                _adlsClient.getAccountOperations().delete(_resourceGroupName, _adlsAccountName);
                _adlaClient.getAccountOperations().delete(_resourceGroupName, _adlaAccountName);
                WaitForNewline("Account deleted.", "DONE.");
            }

            //Set up clients
            public static void SetupClients(ServiceClientCredentials creds)
            {
                _adlsClient = new DataLakeStoreAccountManagementClientImpl(creds);
                _adlsFileSystemClient = new DataLakeStoreFileSystemManagementClientImpl(creds);
                _adlaClient = new DataLakeAnalyticsAccountManagementClientImpl(creds);
                _adlaJobClient = new DataLakeAnalyticsJobManagementClientImpl(creds);
                _adlaCatalogClient = new DataLakeAnalyticsCatalogManagementClientImpl(creds);
                _adlsClient.setSubscriptionId(_subId);
                _adlaClient.setSubscriptionId(_subId);
            }

            // Helper function tooshow status and wait for user input
            public static void WaitForNewline(String reason, String nextAction)
            {
                if (nextAction == null)
                    nextAction = "";

                System.out.println(reason + "\r\nPress ENTER toocontinue...");
                try{System.in.read();}
                catch(Exception e){}

                if (!nextAction.isEmpty())
                {
                    System.out.println(nextAction);
                }
            }

            // Create Data Lake Store and Analytics accounts
            public static void CreateAccounts() throws InterruptedException, CloudException, IOException {
                // Create ADLS account
                DataLakeStoreAccount adlsParameters = new DataLakeStoreAccount();
                adlsParameters.setLocation(_location);

                _adlsClient.getAccountOperations().create(_resourceGroupName, _adlsAccountName, adlsParameters);

                // Create ADLA account
                DataLakeStoreAccountInfo adlsInfo = new DataLakeStoreAccountInfo();
                adlsInfo.setName(_adlsAccountName);

                DataLakeStoreAccountInfoProperties adlsInfoProperties = new DataLakeStoreAccountInfoProperties();
                adlsInfo.setProperties(adlsInfoProperties);

                List<DataLakeStoreAccountInfo> adlsInfoList = new ArrayList<DataLakeStoreAccountInfo>();
                adlsInfoList.add(adlsInfo);

                DataLakeAnalyticsAccountProperties adlaProperties = new DataLakeAnalyticsAccountProperties();
                adlaProperties.setDataLakeStoreAccounts(adlsInfoList);
                adlaProperties.setDefaultDataLakeStoreAccount(_adlsAccountName);

                DataLakeAnalyticsAccount adlaParameters = new DataLakeAnalyticsAccount();
                adlaParameters.setLocation(_location);
                adlaParameters.setName(_adlaAccountName);
                adlaParameters.setProperties(adlaProperties);

                    /* If this line generates an error message like "hello deep update for property 'DataLakeStoreAccounts' is not supported", please delete hello ADLS and ADLA accounts via hello portal and re-run your script. */

                _adlaClient.getAccountOperations().create(_resourceGroupName, _adlaAccountName, adlaParameters);
            }

            //todo: this changes in hello next version of hello API
            public static void CreateFile(String path, String contents, boolean force) throws IOException, CloudException {
                byte[] bytesContents = contents.getBytes();

                _adlsFileSystemClient.getFileSystemOperations().create(_adlsAccountName, path, bytesContents, force);
            }

            public static void DeleteFile(String filePath) throws IOException, CloudException {
                _adlsFileSystemClient.getFileSystemOperations().delete(filePath, _adlsAccountName);
            }

            // Download file
            public static void DownloadFile(String srcPath, String destPath) throws IOException, CloudException {
                InputStream stream = _adlsFileSystemClient.getFileSystemOperations().open(srcPath, _adlsAccountName).getBody();

                PrintWriter pWriter = new PrintWriter(destPath, Charset.defaultCharset().name());

                String fileContents = "";
                if (stream != null) {
                    Writer writer = new StringWriter();

                    char[] buffer = new char[1024];
                    try {
                        Reader reader = new BufferedReader(
                                new InputStreamReader(stream, "UTF-8"));
                        int n;
                        while ((n = reader.read(buffer)) != -1) {
                            writer.write(buffer, 0, n);
                        }
                    } finally {
                        stream.close();
                    }
                    fileContents =  writer.toString();
                }

                pWriter.println(fileContents);
                pWriter.close();
            }

            // Submit a U-SQL job by providing script contents.
            // Returns hello job ID
            public static UUID SubmitJobByScript(String script, String jobName) throws IOException, CloudException {
                UUID jobId = java.util.UUID.randomUUID();
                USqlJobProperties properties = new USqlJobProperties();
                properties.setScript(script);
                JobInformation parameters = new JobInformation();
                parameters.setName(jobName);
                parameters.setJobId(jobId);
                parameters.setType(JobType.USQL);
                parameters.setProperties(properties);

                JobInformation jobInfo = _adlaJobClient.getJobOperations().create(_adlaAccountName, jobId, parameters).getBody();

                return jobId;
            }

            // Wait for job completion
            public static JobResult WaitForJob(UUID jobId) throws IOException, CloudException {
                JobInformation jobInfo = _adlaJobClient.getJobOperations().get(_adlaAccountName, jobId).getBody();
                while (jobInfo.getState() != JobState.ENDED)
                {
                    jobInfo = _adlaJobClient.getJobOperations().get(_adlaAccountName,jobId).getBody();
                }
                return jobInfo.getResult();
            }

            // Get job status
            public static String GetJobStatus(UUID jobId) throws IOException, CloudException {
                JobInformation jobInfo = _adlaJobClient.getJobOperations().get(_adlaAccountName, jobId).getBody();
                return jobInfo.getState().toValue();
            }
        }

1. <span data-ttu-id="ce18c-139">Wykonaj hello toorun monity i aplikacji hello ukończone.</span><span class="sxs-lookup"><span data-stu-id="ce18c-139">Follow hello prompts toorun and complete hello application.</span></span>

## <a name="see-also"></a><span data-ttu-id="ce18c-140">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="ce18c-140">See also</span></span>
* <span data-ttu-id="ce18c-141">toosee hello sam samouczek przy użyciu innych narzędzi, kliknij przycisk hello selektor karty w górnej części hello hello strony.</span><span class="sxs-lookup"><span data-stu-id="ce18c-141">toosee hello same tutorial using other tools, click hello tab selectors on hello top of hello page.</span></span>
* <span data-ttu-id="ce18c-142">toosee bardziej złożonego zapytania, zobacz [witryny sieci Web analizowanie dzienników przy użyciu usługi Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).</span><span class="sxs-lookup"><span data-stu-id="ce18c-142">toosee a more complex query, see [Analyze Website logs using Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).</span></span>
* <span data-ttu-id="ce18c-143">tooget Rozpoczęto tworzenie aplikacji U-SQL, zobacz [skryptów U-SQL opracowanie przy użyciu narzędzi Data Lake Tools dla programu Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="ce18c-143">tooget started developing U-SQL applications, see [Develop U-SQL scripts using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span>
* <span data-ttu-id="ce18c-144">toolearn U-SQL, zobacz [wprowadzenie do języka Azure Data Lake Analytics U-SQL](data-lake-analytics-u-sql-get-started.md), i [dokumentację języka U-SQL](http://go.microsoft.com/fwlink/?LinkId=691348).</span><span class="sxs-lookup"><span data-stu-id="ce18c-144">toolearn U-SQL, see [Get started with Azure Data Lake Analytics U-SQL language](data-lake-analytics-u-sql-get-started.md), and [U-SQL language reference](http://go.microsoft.com/fwlink/?LinkId=691348).</span></span>
* <span data-ttu-id="ce18c-145">Informacje o zadaniach zarządzania znajdziesz w artykule [Zarządzanie usługą Azure Data Lake Analytics przy użyciu witryny Azure Portal](data-lake-analytics-manage-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="ce18c-145">For management tasks, see [Manage Azure Data Lake Analytics using Azure Portal](data-lake-analytics-manage-use-portal.md).</span></span>
* <span data-ttu-id="ce18c-146">Zobacz tooget Przegląd usługi Data Lake Analytics [Omówienie usługi Azure Data Lake Analytics](data-lake-analytics-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ce18c-146">tooget an overview of Data Lake Analytics, see [Azure Data Lake Analytics overview](data-lake-analytics-overview.md).</span></span>
