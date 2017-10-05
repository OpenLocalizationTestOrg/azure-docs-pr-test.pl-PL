---
title: Korzystanie z zestawu Java SDK Data Lake Analytics w celu projektowania aplikacji | Dokumentacja firmy Microsoft
description: "Korzystanie z zestawu Java SDK usługi Azure Data Lake Analytics w celu projektowania aplikacji"
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
ms.openlocfilehash: 795d9ec0b0cac5d74673404f1d0d851393336df0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-data-lake-analytics-using-java-sdk"></a><span data-ttu-id="4eaa6-103">Rozpoczynanie pracy z usługą Azure Data Lake Analytics przy użyciu zestawu SDK języka Java</span><span class="sxs-lookup"><span data-stu-id="4eaa6-103">Get started with Azure Data Lake Analytics using Java SDK</span></span>
[!INCLUDE [get-started-selector](../../includes/data-lake-analytics-selector-get-started.md)]

<span data-ttu-id="4eaa6-104">Dowiedz się, jak utworzyć konto usługi Azure Data Lake i wykonywać podstawowe operacje, takie jak tworzenie folderów, przekazywanie i pobieranie plików danych, usuwanie konta i Praca z zadaniami przy użyciu zestawu SDK usługi Azure Data Lake Analytics Java.</span><span class="sxs-lookup"><span data-stu-id="4eaa6-104">Learn how to use the Azure Data Lake Analytics Java SDK to create an Azure Data Lake account and perform basic operations such as create folders, upload and download data files, delete your account, and work with jobs.</span></span> <span data-ttu-id="4eaa6-105">Aby uzyskać więcej informacji o usłudze Data Lake, zobacz [Azure Data Lake Analytics](data-lake-analytics-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4eaa6-105">For more information about Data Lake, see [Azure Data Lake Analytics](data-lake-analytics-overview.md).</span></span>

<span data-ttu-id="4eaa6-106">W tym samouczku utworzysz aplikacji konsoli Java, która zawiera przykłady typowych zadań administracyjnych, a także tworzenie danych testowych i przesyłania zadania.</span><span class="sxs-lookup"><span data-stu-id="4eaa6-106">In this tutorial, you will develop a Java console application which contains samples of common administrative tasks as well as creating test data and submitting a job.</span></span>  <span data-ttu-id="4eaa6-107">Aby wykonać kroki opisane w tym samouczku, korzystając z innych obsługiwanych narzędzi, kliknij odpowiednią kartę w górnej części tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="4eaa6-107">To go through the same tutorial using other supported tools, click the tabs on the top of this section.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4eaa6-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="4eaa6-108">Prerequisites</span></span>
* <span data-ttu-id="4eaa6-109">Zestaw Java Development Kit (JDK) 8 (z użyciem języka Java w wersji 1.8).</span><span class="sxs-lookup"><span data-stu-id="4eaa6-109">Java Development Kit (JDK) 8 (using Java version 1.8).</span></span>
* <span data-ttu-id="4eaa6-110">IntelliJ lub inne odpowiednie środowisko programistyczne Java.</span><span class="sxs-lookup"><span data-stu-id="4eaa6-110">IntelliJ or another suitable Java development environment.</span></span> <span data-ttu-id="4eaa6-111">Jest to opcjonalne, ale zalecane.</span><span class="sxs-lookup"><span data-stu-id="4eaa6-111">This is optional but recommended.</span></span> <span data-ttu-id="4eaa6-112">W poniższych instrukcjach jest używane środowisko IntelliJ.</span><span class="sxs-lookup"><span data-stu-id="4eaa6-112">The instructions below use IntelliJ.</span></span>
* <span data-ttu-id="4eaa6-113">**Subskrypcja platformy Azure**.</span><span class="sxs-lookup"><span data-stu-id="4eaa6-113">**An Azure subscription**.</span></span> <span data-ttu-id="4eaa6-114">Zobacz temat [Uzyskiwanie bezpłatnej wersji próbnej platformy Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4eaa6-114">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="4eaa6-115">Tworzenie aplikacji usługi Azure Active Directory (AAD) i pobieranie jej **identyfikatora klienta**, **identyfikatora dzierżawy** i **klucza**.</span><span class="sxs-lookup"><span data-stu-id="4eaa6-115">Create an Azure Active Directory (AAD) application and retrieve its **Client ID**, **Tenant ID**, and **Key**.</span></span> <span data-ttu-id="4eaa6-116">Aby uzyskać więcej informacji o aplikacjach usługi AAD i instrukcje na temat uzyskiwania identyfikatora klienta, zobacz [Create Active Directory application and service principal using portal](../azure-resource-manager/resource-group-create-service-principal-portal.md) (Tworzenie aplikacji i głównej nazwy usługi Active Directory przy użyciu portalu).</span><span class="sxs-lookup"><span data-stu-id="4eaa6-116">For more information about AAD applications and instructions on how to get a client ID, see [Create Active Directory application and service principal using portal](../azure-resource-manager/resource-group-create-service-principal-portal.md).</span></span> <span data-ttu-id="4eaa6-117">Identyfikator URI odpowiedzi i klucz będzie także dostępny z portalu po utworzeniu aplikacji i wygenerowaniu klucza.</span><span class="sxs-lookup"><span data-stu-id="4eaa6-117">The Reply URI and Key will also be available from the portal once you have the application created and key generated.</span></span>

## <a name="how-do-i-authenticate-using-azure-active-directory"></a><span data-ttu-id="4eaa6-118">W jaki sposób uwierzytelniać za pomocą usługi Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="4eaa6-118">How do I authenticate using Azure Active Directory?</span></span>
<span data-ttu-id="4eaa6-119">Poniższy fragment kodu zawiera kod uwierzytelniania **nieinteraktywnego**, w przypadku którego aplikacja udostępnia własne poświadczenia.</span><span class="sxs-lookup"><span data-stu-id="4eaa6-119">The code snippet below provides code for **non-interactive** authentication, where the application provides its own credentials.</span></span>

<span data-ttu-id="4eaa6-120">Przed wykonaniem kroków tego samouczka należy zezwolić aplikacji na tworzenie zasobów na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="4eaa6-120">You will need to give your application permission to create resources in Azure for this tutorial to work.</span></span> <span data-ttu-id="4eaa6-121">**Zdecydowanie zalecamy**, aby do celów związanych z tym samouczkiem nadać tej aplikacji uprawnienia współautora dotyczące nowej, nieużywanej i pustej grupy zasobów w subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="4eaa6-121">It is **highly recommended** that you only give this application Contributor permissions to a new, unused, and empty resource group in your Azure subscription for the purposes of this tutorial.</span></span>

## <a name="create-a-java-application"></a><span data-ttu-id="4eaa6-122">Tworzenie aplikacji Java</span><span class="sxs-lookup"><span data-stu-id="4eaa6-122">Create a Java application</span></span>
1. <span data-ttu-id="4eaa6-123">Otwórz środowisko IntelliJ i utwórz nowy projekt języka Java przy użyciu szablonu **Command Line App** (Aplikacja wiersza polecenia).</span><span class="sxs-lookup"><span data-stu-id="4eaa6-123">Open IntelliJ and create a new Java project using the **Command Line App** template.</span></span>
2. <span data-ttu-id="4eaa6-124">Kliknij prawym przyciskiem myszy projekt po lewej stronie ekranu, a następnie kliknij pozycję **Add Framework Support** (Dodaj obsługę struktury).</span><span class="sxs-lookup"><span data-stu-id="4eaa6-124">Right-click on the project on the left-hand side of your screen and click **Add Framework Support**.</span></span> <span data-ttu-id="4eaa6-125">Wybierz pozycję **Maven** i kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="4eaa6-125">Choose **Maven** and click **OK**.</span></span>
3. <span data-ttu-id="4eaa6-126">Otwórz nowo utworzony plik **„pom.xml”** i dodaj poniższy fragment tekstu między tagami **\</version >** i **\</project >**:</span><span class="sxs-lookup"><span data-stu-id="4eaa6-126">Open the newly created **"pom.xml"** file and add the following snippet of text between the **\</version>** tag and the **\</project>** tag:</span></span>

    >[!NOTE]
    ><span data-ttu-id="4eaa6-127">Ten krok jest tymczasowy do momentu zestawu SDK usługi Azure Data Lake Analytics jest dostępna w programie Maven.</span><span class="sxs-lookup"><span data-stu-id="4eaa6-127">This step is temporary until the Azure Data Lake Analytics SDK is available in Maven.</span></span> <span data-ttu-id="4eaa6-128">Ten artykuł zostanie zaktualizowany po udostępnieniu zestawu SDK w programie Maven.</span><span class="sxs-lookup"><span data-stu-id="4eaa6-128">This article will be updated once the SDK is available in Maven.</span></span> <span data-ttu-id="4eaa6-129">Wszystkie przyszłe aktualizacje tego zestawu SDK będą dostępne za pośrednictwem programu Maven.</span><span class="sxs-lookup"><span data-stu-id="4eaa6-129">All future updates to this SDK will be availble through Maven.</span></span>
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
4. <span data-ttu-id="4eaa6-130">Przejdź do **pliku**, następnie **ustawienia**, następnie **kompilacji**, **wykonywania**, **wdrożenia**.</span><span class="sxs-lookup"><span data-stu-id="4eaa6-130">Go to **File**, then **Settings**, then **Build**, **Execution**, **Deployment**.</span></span> <span data-ttu-id="4eaa6-131">Wybierz **narzędzi do kompilacji**, **Maven**, **importowania**.</span><span class="sxs-lookup"><span data-stu-id="4eaa6-131">Select **Build Tools**, **Maven**, **Importing**.</span></span> <span data-ttu-id="4eaa6-132">Następnie sprawdź **Import Maven projektów automatycznie**.</span><span class="sxs-lookup"><span data-stu-id="4eaa6-132">Then check **Import Maven projects automatically**.</span></span>
5. <span data-ttu-id="4eaa6-133">Otwórz **Main.java** i Zastąp istniejący blok kodu poniższym kodem.</span><span class="sxs-lookup"><span data-stu-id="4eaa6-133">Open **Main.java** and replace the existing code block with the following code.</span></span> <span data-ttu-id="4eaa6-134">Ponadto podaj wartości parametrów wywoływanych we fragmencie kodu, takie jak **localFolderPath**, **_adlaAccountName**, **_adlsAccountName**, **_ resourceGroupName** i zastąp symbole zastępcze **identyfikator klienta**, **klucz TAJNY klienta**, **identyfikator DZIERŻAWCY**, i  **Identyfikator SUBSKRYPCJI**.</span><span class="sxs-lookup"><span data-stu-id="4eaa6-134">Also, provide the values for parameters called out in the code snippet, such as **localFolderPath**, **_adlaAccountName**, **_adlsAccountName**, **_resourceGroupName** and replace placeholders for **CLIENT-ID**, **CLIENT-SECRET**, **TENANT-ID**, and **SUBSCRIPTION-ID**.</span></span>

    <span data-ttu-id="4eaa6-135">Ten kod przechodzi przez proces tworzenia konta usługi Data Lake Store i usługi Data Lake Analytics, tworzenie plików w magazynie uruchamiania zadania, pobieranie stanu zadania, pobieranie danych wyjściowych zadania i usunięcia konta.</span><span class="sxs-lookup"><span data-stu-id="4eaa6-135">This code goes through the process of creating Data Lake Store and Data Lake Analytics accounts, creating files in the store, running a job, getting job status, downloading job output, and finally deleting the account.</span></span>

   > [!NOTE]
   > <span data-ttu-id="4eaa6-136">Obecnie występuje znany problem z usługą Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="4eaa6-136">There is currently a known issue with the Azure Data Lake Service.</span></span>  <span data-ttu-id="4eaa6-137">Jeśli przykładowa aplikacja zostanie przerwana lub wystąpi błąd, może być konieczne ręczne usunięcie kont usług Data Lake Store i Data Lake Analytics utworzonych przez skrypt.</span><span class="sxs-lookup"><span data-stu-id="4eaa6-137">If the sample app is interrupted or encounters an error, you may need to manually delete the Data Lake Store & Data Lake Analytics accounts that the script creates.</span></span>  <span data-ttu-id="4eaa6-138">Jeśli nie znasz witryny Portal, zapoznaj się z przewodnikiem [Manage Azure Data Lake Analytics using Azure Portal](data-lake-analytics-manage-use-portal.md) (Zarządzanie usługą Azure Data Lake Analytics przy użyciu witryny Azure Portal).</span><span class="sxs-lookup"><span data-stu-id="4eaa6-138">If you're not familiar with the Portal, the [Manage Azure Data Lake Analytics using Azure Portal](data-lake-analytics-manage-use-portal.md) guide will get you started.</span></span>
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

                _clientSecret = "<CLIENT-SECRET>"; // TODO: For production scenarios, we recommend that you replace this line with a more secure way of acquiring the application client secret, rather than hard-coding it in the source code.

                String localFolderPath = "C:\\local_path\\"; // TODO: Change this to any unused, new, empty folder on your local machine.

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
                // TODO: these change order in the next patch
                byte[] bytesContents = "123,abc".getBytes();
                _adlsFileSystemClient.getFileSystemOperations().create(_adlsAccountName, "/input1.csv", bytesContents, true);

                WaitForNewline("File created.", "Submitting a job.");

                // Submit a job to Data Lake Analytics
                UUID jobId = SubmitJobByScript("@input =  EXTRACT Data string FROM \"/input1.csv\" USING Extractors.Csv(); OUTPUT @input TO @\"/output1.csv\" USING Outputters.Csv();", "testJob");
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

            // Helper function to show status and wait for user input
            public static void WaitForNewline(String reason, String nextAction)
            {
                if (nextAction == null)
                    nextAction = "";

                System.out.println(reason + "\r\nPress ENTER to continue...");
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

                    /* If this line generates an error message like "The deep update for property 'DataLakeStoreAccounts' is not supported", please delete the ADLS and ADLA accounts via the portal and re-run your script. */

                _adlaClient.getAccountOperations().create(_resourceGroupName, _adlaAccountName, adlaParameters);
            }

            //todo: this changes in the next version of the API
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
            // Returns the job ID
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

1. <span data-ttu-id="4eaa6-139">Postępuj zgodnie z monitami, aby uruchomić aplikację i ukończyć jej działanie.</span><span class="sxs-lookup"><span data-stu-id="4eaa6-139">Follow the prompts to run and complete the application.</span></span>

## <a name="see-also"></a><span data-ttu-id="4eaa6-140">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="4eaa6-140">See also</span></span>
* <span data-ttu-id="4eaa6-141">Aby wyświetlić ten samouczek przy użyciu innych narzędzi, kliknij odpowiedni selektor karty w górnej części strony.</span><span class="sxs-lookup"><span data-stu-id="4eaa6-141">To see the same tutorial using other tools, click the tab selectors on the top of the page.</span></span>
* <span data-ttu-id="4eaa6-142">Aby uzyskać informacje na temat bardziej złożonego zapytania, zobacz temat [Analizowanie dzienników witryn sieci Web przy użyciu usługi Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).</span><span class="sxs-lookup"><span data-stu-id="4eaa6-142">To see a more complex query, see [Analyze Website logs using Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).</span></span>
* <span data-ttu-id="4eaa6-143">Aby rozpocząć tworzenie aplikacji w języku U-SQL, zobacz artykuł [Tworzenie skryptów U-SQL przy użyciu narzędzi Data Lake Tools dla Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="4eaa6-143">To get started developing U-SQL applications, see [Develop U-SQL scripts using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span>
* <span data-ttu-id="4eaa6-144">Aby dowiedzieć się więcej o języku U-SQL, zobacz [Wprowadzenie do języka U-SQL w usłudze Azure Data Lake Analytics](data-lake-analytics-u-sql-get-started.md) i [Dokumentację języka SQL](http://go.microsoft.com/fwlink/?LinkId=691348).</span><span class="sxs-lookup"><span data-stu-id="4eaa6-144">To learn U-SQL, see [Get started with Azure Data Lake Analytics U-SQL language](data-lake-analytics-u-sql-get-started.md), and [U-SQL language reference](http://go.microsoft.com/fwlink/?LinkId=691348).</span></span>
* <span data-ttu-id="4eaa6-145">Informacje o zadaniach zarządzania znajdziesz w artykule [Zarządzanie usługą Azure Data Lake Analytics przy użyciu witryny Azure Portal](data-lake-analytics-manage-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="4eaa6-145">For management tasks, see [Manage Azure Data Lake Analytics using Azure Portal](data-lake-analytics-manage-use-portal.md).</span></span>
* <span data-ttu-id="4eaa6-146">Aby zapoznać się z omówieniem usługi Data Lake Analytics, zobacz [Omówienie usługi Azure Data Lake Analytics](data-lake-analytics-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4eaa6-146">To get an overview of Data Lake Analytics, see [Azure Data Lake Analytics overview](data-lake-analytics-overview.md).</span></span>
