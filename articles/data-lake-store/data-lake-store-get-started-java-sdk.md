---
title: "aaaUse hello zestawu Java SDK toodevelop aplikacji w usłudze Azure Data Lake Store | Dokumentacja firmy Microsoft"
description: "Użyj zestawu Java SDK usługi Azure Data Lake Store toocreate konto usługi Data Lake Store i wykonywać podstawowe operacje w hello usługi Data Lake Store"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: d10e09db-5232-4e84-bb50-52efc2c21887
ms.service: data-lake-store
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/28/2017
ms.author: nitinme
ms.openlocfilehash: d3bcee449c2a2a4bd2f7b241af46ecc010b6b62e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-store-using-java"></a><span data-ttu-id="6772b-103">Rozpoczynanie pracy z usługą Azure Data Lake Store przy użyciu języka Java</span><span class="sxs-lookup"><span data-stu-id="6772b-103">Get started with Azure Data Lake Store using Java</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="6772b-104">Portal</span><span class="sxs-lookup"><span data-stu-id="6772b-104">Portal</span></span>](data-lake-store-get-started-portal.md)
> * [<span data-ttu-id="6772b-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="6772b-105">PowerShell</span></span>](data-lake-store-get-started-powershell.md)
> * [<span data-ttu-id="6772b-106">Zestaw SDK platformy .NET</span><span class="sxs-lookup"><span data-stu-id="6772b-106">.NET SDK</span></span>](data-lake-store-get-started-net-sdk.md)
> * [<span data-ttu-id="6772b-107">Zestaw SDK Java</span><span class="sxs-lookup"><span data-stu-id="6772b-107">Java SDK</span></span>](data-lake-store-get-started-java-sdk.md)
> * [<span data-ttu-id="6772b-108">Interfejs API REST</span><span class="sxs-lookup"><span data-stu-id="6772b-108">REST API</span></span>](data-lake-store-get-started-rest-api.md)
> * [<span data-ttu-id="6772b-109">Interfejs wiersza polecenia platformy Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="6772b-109">Azure CLI 2.0</span></span>](data-lake-store-get-started-cli-2.0.md)
> * [<span data-ttu-id="6772b-110">Node.js</span><span class="sxs-lookup"><span data-stu-id="6772b-110">Node.js</span></span>](data-lake-store-manage-use-nodejs.md)
> * [<span data-ttu-id="6772b-111">Python</span><span class="sxs-lookup"><span data-stu-id="6772b-111">Python</span></span>](data-lake-store-get-started-python.md)
>
> 

<span data-ttu-id="6772b-112">Dowiedz się, jak toouse hello zestawu Java SDK usługi Azure Data Lake Store tooperform podstawowe operacje takie jak tworzenie folderów, przekazywanie i pobieranie plików danych itp. Aby uzyskać więcej informacji o usłudze Data Lake, zobacz temat [Usługa Azure Data Lake Store](data-lake-store-overview.md).</span><span class="sxs-lookup"><span data-stu-id="6772b-112">Learn how toouse hello Azure Data Lake Store Java SDK tooperform basic operations such as create folders, upload and download data files, etc. For more information about Data Lake, see [Azure Data Lake Store](data-lake-store-overview.md).</span></span>

<span data-ttu-id="6772b-113">Dokumentacja interfejsu API zestawu SDK Java powitania dla usługi Azure Data Lake Store można uzyskać dostęp [dokumentacja interfejsu API usługi Azure Data Lake magazynu Java](https://azure.github.io/azure-data-lake-store-java/javadoc/).</span><span class="sxs-lookup"><span data-stu-id="6772b-113">You can access hello Java SDK API docs for Azure Data Lake Store at [Azure Data Lake Store Java API docs](https://azure.github.io/azure-data-lake-store-java/javadoc/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6772b-114">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="6772b-114">Prerequisites</span></span>
* <span data-ttu-id="6772b-115">Zestaw Java Development Kit (JDK 7 lub nowszy, korzystający z języka Java w wersji 1.7 lub nowszej)</span><span class="sxs-lookup"><span data-stu-id="6772b-115">Java Development Kit (JDK 7 or higher, using Java version 1.7 or higher)</span></span>
* <span data-ttu-id="6772b-116">Konto usługi Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="6772b-116">Azure Data Lake Store account.</span></span> <span data-ttu-id="6772b-117">Postępuj zgodnie z instrukcjami hello w [wprowadzenie do usługi Azure Data Lake Store za pomocą portalu Azure hello](data-lake-store-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="6772b-117">Follow hello instructions at [Get started with Azure Data Lake Store using hello Azure Portal](data-lake-store-get-started-portal.md).</span></span>
* <span data-ttu-id="6772b-118">[Maven](https://maven.apache.org/install.html).</span><span class="sxs-lookup"><span data-stu-id="6772b-118">[Maven](https://maven.apache.org/install.html).</span></span> <span data-ttu-id="6772b-119">Ten samouczek używa programu Maven na potrzeby zależności między kompilacją i projektem.</span><span class="sxs-lookup"><span data-stu-id="6772b-119">This tutorial uses Maven for build and project dependencies.</span></span> <span data-ttu-id="6772b-120">Chociaż możliwe toobuild bez użycia systemu kompilacji, takich jak Maven i Gradle, Utwórz te systemy jest znacznie łatwiejsze zależności toomanage.</span><span class="sxs-lookup"><span data-stu-id="6772b-120">Although it is possible toobuild without using a build system like Maven or Gradle, these systems make is much easier toomanage dependencies.</span></span>
* <span data-ttu-id="6772b-121">(Opcjonalnie) Wtyczka [IntelliJ IDEA](https://www.jetbrains.com/idea/download/) lub [Eclipse](https://www.eclipse.org/downloads/) przypominająca środowisko IDE lub podobna.</span><span class="sxs-lookup"><span data-stu-id="6772b-121">(Optional) And IDE like [IntelliJ IDEA](https://www.jetbrains.com/idea/download/) or [Eclipse](https://www.eclipse.org/downloads/) or similar.</span></span>

## <a name="how-do-i-authenticate-using-azure-active-directory"></a><span data-ttu-id="6772b-122">W jaki sposób uwierzytelniać za pomocą usługi Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="6772b-122">How do I authenticate using Azure Active Directory?</span></span>
<span data-ttu-id="6772b-123">W tym samouczku używamy usługi Azure AD aplikacji klienta tajny tooretrieve tokenu usługi Azure Active Directory (authentication service-to-service).</span><span class="sxs-lookup"><span data-stu-id="6772b-123">In this tutorial we use a Azure AD application client secret tooretrieve an Azure Active Directory token (service-to-service authentication).</span></span> <span data-ttu-id="6772b-124">Używamy tej operacji katalogu i toocreate tokenu pliku operacji tooperform obiektu klienta usługi Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="6772b-124">We use this token toocreate an Data Lake Store client object tooperform operations file and directory operations.</span></span> <span data-ttu-id="6772b-125">Aby uzyskać instrukcje dotyczące sposobu tooauthenticate przy użyciu usługi Azure Data Lake Store hello klucz tajny klienta wykonujemy hello następujące ogólne kroki:</span><span class="sxs-lookup"><span data-stu-id="6772b-125">For instructions on how tooauthenticate with Azure Data Lake Store using hello client secret, we perform hello following high-level steps:</span></span>

1. <span data-ttu-id="6772b-126">Utworzenie aplikacji sieci Web Azure AD</span><span class="sxs-lookup"><span data-stu-id="6772b-126">Create an Azure AD web application</span></span>
2. <span data-ttu-id="6772b-127">Pobieranie Identyfikatora klienta hello, klucz tajny klienta i punktu końcowego tokena dla hello aplikacji sieci web usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6772b-127">Retrieve hello client ID, client secret, and token endpoint for hello Azure AD web application.</span></span>
3. <span data-ttu-id="6772b-128">Konfigurowanie dostępu dla aplikacji sieci web usługi Azure AD hello na powitania usługi Data Lake Store plik/folder, który ma tooaccess z hello tworzonej aplikacji w języku Java.</span><span class="sxs-lookup"><span data-stu-id="6772b-128">Configure access for hello Azure AD web application on hello Data Lake Store file/folder that you want tooaccess from hello Java application you are creating.</span></span>

<span data-ttu-id="6772b-129">Aby uzyskać instrukcje dotyczące tooperform tych kroków, zobacz temat [tworzenie aplikacji usługi Active Directory](data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="6772b-129">For instructions on how tooperform these steps, see [Create an Active Directory application](data-lake-store-authenticate-using-active-directory.md).</span></span>

<span data-ttu-id="6772b-130">Usługa Azure Active Directory zapewnia innych opcji oraz tooretrieve tokenu.</span><span class="sxs-lookup"><span data-stu-id="6772b-130">Azure Active Directory provides other options as well tooretrieve a token.</span></span> <span data-ttu-id="6772b-131">Można wybrać z liczbą toosuit mechanizmów uwierzytelniania inny scenariusz, na przykład aplikacji działających w przeglądarce, aplikacji rozproszonych jako aplikacji pulpitu lub aplikacji serwera, uruchamiane lokalnie lub w wirtualnej platformy Azure maszyny.</span><span class="sxs-lookup"><span data-stu-id="6772b-131">You can pick from a number of different authentication mechanisms toosuit your scenario, for example, an application running in a browser, an application distributed as a desktop application, or a server application running on-premises or in an Azure virtual machine.</span></span> <span data-ttu-id="6772b-132">Można również wybrać różne rodzaje poświadczeń, takie jak hasła, certyfikaty, uwierzytelnianie 2-etapowe itd. Ponadto usługa Azure Active Directory umożliwia toosynchronize lokalnych użytkowników usługi Active Directory z chmurą hello.</span><span class="sxs-lookup"><span data-stu-id="6772b-132">You can also pick from different types of credentials like passwords, certificates, 2-factor authentication, etc. In addition, Azure Active Directory allows you toosynchronize your on-premises Active Directory users with hello cloud.</span></span> <span data-ttu-id="6772b-133">Aby uzyskać szczegółowe informacje, zobacz [Scenariusze uwierzytelniania dla usługi Azure Active Directory](../active-directory/active-directory-authentication-scenarios.md).</span><span class="sxs-lookup"><span data-stu-id="6772b-133">For details, see [Authentication Scenarios for Azure Active Directory](../active-directory/active-directory-authentication-scenarios.md).</span></span> 

## <a name="create-a-java-application"></a><span data-ttu-id="6772b-134">Tworzenie aplikacji Java</span><span class="sxs-lookup"><span data-stu-id="6772b-134">Create a Java application</span></span>
<span data-ttu-id="6772b-135">Witaj kod przykładowy [w serwisie GitHub](https://azure.microsoft.com/documentation/samples/data-lake-store-java-upload-download-get-started/) przeprowadzi Cię przez proces tworzenia plików w magazynie hello, łączenia plików, pobierania pliku i usuń niektóre pliki w magazynie hello hello.</span><span class="sxs-lookup"><span data-stu-id="6772b-135">hello code sample available [on GitHub](https://azure.microsoft.com/documentation/samples/data-lake-store-java-upload-download-get-started/) walks you through hello process of creating files in hello store, concatenating files, downloading a file, and deleting some files in hello store.</span></span> <span data-ttu-id="6772b-136">Ta sekcja hello artykułu opisano hello głównych części kodu hello.</span><span class="sxs-lookup"><span data-stu-id="6772b-136">This section of hello article walk you through hello main parts of hello code.</span></span>

1. <span data-ttu-id="6772b-137">Utwórz projekt Maven za pomocą [mvn archetype](https://maven.apache.org/guides/getting-started/maven-in-five-minutes.html) z hello wiersza polecenia lub przy użyciu środowiska IDE.</span><span class="sxs-lookup"><span data-stu-id="6772b-137">Create a Maven project using [mvn archetype](https://maven.apache.org/guides/getting-started/maven-in-five-minutes.html) from hello command-line or using an IDE.</span></span> <span data-ttu-id="6772b-138">Aby uzyskać instrukcje dotyczące sposobu toocreate Java projektu przy użyciu IntelliJ, zobacz [tutaj](https://www.jetbrains.com/help/idea/2016.1/creating-and-running-your-first-java-application.html).</span><span class="sxs-lookup"><span data-stu-id="6772b-138">For instructions on how toocreate a Java project using IntelliJ, see [here](https://www.jetbrains.com/help/idea/2016.1/creating-and-running-your-first-java-application.html).</span></span> <span data-ttu-id="6772b-139">Aby uzyskać instrukcje dotyczące toocreate projektu za pomocą programu Eclipse, zobacz [tutaj](http://help.eclipse.org/mars/index.jsp?topic=%2Forg.eclipse.jdt.doc.user%2FgettingStarted%2Fqs-3.htm).</span><span class="sxs-lookup"><span data-stu-id="6772b-139">For instructions on how toocreate a project using Eclipse, see [here](http://help.eclipse.org/mars/index.jsp?topic=%2Forg.eclipse.jdt.doc.user%2FgettingStarted%2Fqs-3.htm).</span></span> 
2. <span data-ttu-id="6772b-140">Dodaj następujące zależności tooyour Maven hello **pom.xml** pliku.</span><span class="sxs-lookup"><span data-stu-id="6772b-140">Add hello following dependencies tooyour Maven **pom.xml** file.</span></span> <span data-ttu-id="6772b-141">Dodaj następujące fragment tekstu między hello hello  **\</version >** znacznika i hello  **\</project >** tagu:</span><span class="sxs-lookup"><span data-stu-id="6772b-141">Add hello following snippet of text between hello **\</version>** tag and hello **\</project>** tag:</span></span>
   
        <dependencies>
          <dependency>
            <groupId>com.microsoft.azure</groupId>
            <artifactId>azure-data-lake-store-sdk</artifactId>
            <version>2.1.5</version>
          </dependency>
          <dependency>
            <groupId>org.slf4j</groupId>
            <artifactId>slf4j-nop</artifactId>
            <version>1.7.21</version>
          </dependency>
        </dependencies>
   
    <span data-ttu-id="6772b-142">zależność pierwszy Hello jest hello toouse zestawu SDK Data Lake Store (`azure-data-lake-store-sdk`) z hello maven repozytorium.</span><span class="sxs-lookup"><span data-stu-id="6772b-142">hello first dependency is toouse hello Data Lake Store SDK (`azure-data-lake-store-sdk`) from hello maven repository.</span></span> <span data-ttu-id="6772b-143">Witaj drugi zależności (`slf4j-nop`) jest toospecify które toouse framework rejestrowania dla tej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="6772b-143">hello second dependency (`slf4j-nop`) is toospecify which logging framework toouse for this application.</span></span> <span data-ttu-id="6772b-144">Witaj zestawu SDK Data Lake Store używa [slf4j](http://www.slf4j.org/) fasad rejestrowania, który pozwala wybrać wiele platform popularnych rejestrowania, takich jak log4j, Java, rejestrowanie, logback, itp., lub bez rejestrowania.</span><span class="sxs-lookup"><span data-stu-id="6772b-144">hello Data Lake Store SDK uses [slf4j](http://www.slf4j.org/) logging façade, which lets you choose from a number of popular logging frameworks, like log4j, Java logging, logback, etc., or no logging.</span></span> <span data-ttu-id="6772b-145">W tym przykładzie zostanie wyłączony rejestrowania, dlatego używamy hello **slf4j nop** powiązania.</span><span class="sxs-lookup"><span data-stu-id="6772b-145">For this example, we will disable logging, hence we use hello **slf4j-nop** binding.</span></span> <span data-ttu-id="6772b-146">toouse inne opcje logowania w aplikacji, zobacz [tutaj](http://www.slf4j.org/manual.html#projectDep).</span><span class="sxs-lookup"><span data-stu-id="6772b-146">toouse other logging options in your app, see [here](http://www.slf4j.org/manual.html#projectDep).</span></span>

### <a name="add-hello-application-code"></a><span data-ttu-id="6772b-147">Dodaj kod aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="6772b-147">Add hello application code</span></span>
<span data-ttu-id="6772b-148">Istnieją trzy główne części toohello kodu.</span><span class="sxs-lookup"><span data-stu-id="6772b-148">There are three main parts toohello code.</span></span>

1. <span data-ttu-id="6772b-149">Uzyskać hello tokenu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6772b-149">Obtain hello Azure Active Directory token</span></span>
2. <span data-ttu-id="6772b-150">Użyj tokenu toocreate powitania klienta usługi Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="6772b-150">Use hello token toocreate a Data Lake Store client.</span></span>
3. <span data-ttu-id="6772b-151">Użyj operacji tooperform klienta usługi Data Lake Store hello.</span><span class="sxs-lookup"><span data-stu-id="6772b-151">Use hello Data Lake Store client tooperform operations.</span></span>

#### <a name="step-1-obtain-an-azure-active-directory-token"></a><span data-ttu-id="6772b-152">Krok 1. Uzyskaj token usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6772b-152">Step 1: Obtain an Azure Active Directory token.</span></span>
<span data-ttu-id="6772b-153">Witaj zestawu SDK Data Lake Store zapewnia wygodne metody, które umożliwiają zarządzanie tokeny zabezpieczające hello potrzebne toohello tootalk konta usługi Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="6772b-153">hello Data Lake Store SDK provides convenient methods that let you manage hello security tokens needed tootalk toohello Data Lake Store account.</span></span> <span data-ttu-id="6772b-154">Jednak hello zestawu SDK nie wprowadzić, że można używać tylko tych metod.</span><span class="sxs-lookup"><span data-stu-id="6772b-154">However, hello SDK does not mandate that only these methods be used.</span></span> <span data-ttu-id="6772b-155">Można użyć innych środków do uzyskania tokenu również, jak przy użyciu hello [zestawu SDK usługi Azure Active Directory](https://github.com/AzureAD/azure-activedirectory-library-for-java), lub niestandardowy kod.</span><span class="sxs-lookup"><span data-stu-id="6772b-155">You can use any other means of obtaining token as well, like using hello [Azure Active Directory SDK](https://github.com/AzureAD/azure-activedirectory-library-for-java), or your own custom code.</span></span>

<span data-ttu-id="6772b-156">toouse hello token tooobtain zestawu SDK Data Lake Store hello Active Directory w sieci Web aplikacji został utworzony wcześniej, użyj jednej z podklasy hello `AccessTokenProvider` (hello poniższym przykładzie użyto `ClientCredsTokenProvider`).</span><span class="sxs-lookup"><span data-stu-id="6772b-156">toouse hello Data Lake Store SDK tooobtain token for hello Active Directory Web application you created earlier, use one of hello subclasses of `AccessTokenProvider` (hello example below uses `ClientCredsTokenProvider`).</span></span> <span data-ttu-id="6772b-157">Witaj dostawcy tokenu pamięć podręczną hello poświadczenia tooobtain hello token używany w pamięci i hello token odnawia automatycznie, jeśli chodzi o tooexpire.</span><span class="sxs-lookup"><span data-stu-id="6772b-157">hello token provider caches hello creds used tooobtain hello token in memory, and automatically renews hello token if it is about tooexpire.</span></span> <span data-ttu-id="6772b-158">Jest możliwe toocreate własne podklasy `AccessTokenProvider` tokeny są uzyskiwane przez kod klienta, ale teraz umożliwia po prostu użyj hello podać jedną w hello zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="6772b-158">It is possible toocreate your own subclasses of `AccessTokenProvider` so tokens are obtained by your customer code, but for now let's just use hello one provided in hello SDK.</span></span>

<span data-ttu-id="6772b-159">Zastąp **wypełniania-tutaj** hello rzeczywiste wartości dla hello aplikacji sieci Web Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="6772b-159">Replace **FILL-IN-HERE** with hello actual values for hello Azure Active Directory Web application.</span></span>

    private static String clientId = "FILL-IN-HERE";
    private static String authTokenEndpoint = "FILL-IN-HERE";
    private static String clientKey = "FILL-IN-HERE";

    AccessTokenProvider provider = new ClientCredsTokenProvider(authTokenEndpoint, clientId, clientKey);

#### <a name="step-2-create-an-azure-data-lake-store-client-adlstoreclient-object"></a><span data-ttu-id="6772b-160">Krok 2. Utwórz obiekt klienta usługi Azure Data Lake Store (ADLStoreClient)</span><span class="sxs-lookup"><span data-stu-id="6772b-160">Step 2: Create an Azure Data Lake Store client (ADLStoreClient) object</span></span>
<span data-ttu-id="6772b-161">Tworzenie [ADLStoreClient](https://azure.github.io/azure-data-lake-store-java/javadoc/) obiekt wymaga toospecify hello usługi Data Lake Store konta nazwy i hello dostawcy tokenów wygenerowanych w ostatnim kroku hello.</span><span class="sxs-lookup"><span data-stu-id="6772b-161">Creating an [ADLStoreClient](https://azure.github.io/azure-data-lake-store-java/javadoc/) object requires you toospecify hello Data Lake Store account name and hello token provider you generated in hello last step.</span></span> <span data-ttu-id="6772b-162">Należy pamiętać, że hello konta Data Lake Store, że nazwa musi toobe w pełni kwalifikowaną nazwą domeny.</span><span class="sxs-lookup"><span data-stu-id="6772b-162">Note that hello Data Lake Store account name needs toobe a fully qualified domain name.</span></span> <span data-ttu-id="6772b-163">Na przykład zastąp ciąg **FILL-IN-HERE** (Wypełnij tutaj) czymś w rodzaju **mydatalakestore.azuredatalakestore.net**.</span><span class="sxs-lookup"><span data-stu-id="6772b-163">For example, replace **FILL-IN-HERE** with something like **mydatalakestore.azuredatalakestore.net**.</span></span>

    private static String accountFQDN = "FILL-IN-HERE";  // full account FQDN, not just hello account name
    ADLStoreClient client = ADLStoreClient.createClient(accountFQDN, provider);

### <a name="step-3-use-hello-adlstoreclient-tooperform-file-and-directory-operations"></a><span data-ttu-id="6772b-164">Krok 3: Użyj hello ADLStoreClient tooperform plików i katalogów operacji</span><span class="sxs-lookup"><span data-stu-id="6772b-164">Step 3: Use hello ADLStoreClient tooperform file and directory operations</span></span>
<span data-ttu-id="6772b-165">Poniższy kod Hello zawiera przykładowe fragmenty niektórych typowych operacji.</span><span class="sxs-lookup"><span data-stu-id="6772b-165">hello code below contains example snippets of some common operations.</span></span> <span data-ttu-id="6772b-166">Można przyjrzeć się hello pełne [dokumentacja interfejsu API zestawu SDK Java Data Lake magazynu](https://azure.github.io/azure-data-lake-store-java/javadoc/) z hello **ADLStoreClient** obiekt toosee innych operacji.</span><span class="sxs-lookup"><span data-stu-id="6772b-166">You can look at hello full [Data Lake Store Java SDK API docs](https://azure.github.io/azure-data-lake-store-java/javadoc/) of hello **ADLStoreClient** object toosee other operations.</span></span>

<span data-ttu-id="6772b-167">Pamiętaj, że pliki są odczytywane i zapisywane za pomocą standardowych strumieni Java.</span><span class="sxs-lookup"><span data-stu-id="6772b-167">Note that files are read from and written into using standard Java streams.</span></span> <span data-ttu-id="6772b-168">Oznacza to, że można dowolną hello Java strumienie na powitania Data Lake — magazyn strumieni toobenefit ze standardowych funkcji języka Java (np. drukowania strumieni sformatowane wyniki ani żadnych strumieni kompresji i szyfrowania hello dodatkowe funkcje na warstwy "TOP, itp.).</span><span class="sxs-lookup"><span data-stu-id="6772b-168">This means that you can layer any of hello Java streams on top of hello Data Lake Store streams toobenefit from standard Java functionality (e.g., Print streams for formatted output, or any of hello compression or encryption streams for additional functionality on top, etc.).</span></span>

     // create file and write some content
     String filename = "/a/b/c.txt";
     OutputStream stream = client.createFile(filename, IfExists.OVERWRITE  );
     PrintStream out = new PrintStream(stream);
     for (int i = 1; i <= 10; i++) {
         out.println("This is line #" + i);
         out.format("This is hello same line (%d), but using formatted output. %n", i);
     }
     out.close();
    
    // set file permission
    client.setPermission(filename, "744");

    // append toofile
    stream = client.getAppendStream(filename);
    stream.write(getSampleContent());
    stream.close();

    // Read File
    InputStream in = client.getReadStream(filename);
    byte[] b = new byte[64000];
    while (in.read(b) != -1) {
        System.out.write(b);
    }
    in.close();

    // concatenate hello two files into one
    List<String> fileList = Arrays.asList("/a/b/c.txt", "/a/b/d.txt");
    client.concatenateFiles("/a/b/f.txt", fileList);

    //rename hello file
    client.rename("/a/b/f.txt", "/a/b/g.txt");

    // list directory contents
    List<DirectoryEntry> list = client.enumerateDirectory("/a/b", 2000);
    System.out.println("Directory listing for directory /a/b:");
    for (DirectoryEntry entry : list) {
        printDirectoryInfo(entry);
    }

    // delete directory along with all hello subdirectories and files in it
    client.deleteRecursive("/a");

#### <a name="step-4-build-and-run-hello-application"></a><span data-ttu-id="6772b-169">Krok 4: Tworzenie i uruchamianie aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="6772b-169">Step 4: Build and run hello application</span></span>
1. <span data-ttu-id="6772b-170">toorun od w IDE zlokalizuj i naciśnij klawisz hello **Uruchom** przycisku.</span><span class="sxs-lookup"><span data-stu-id="6772b-170">toorun from within an IDE, locate and press hello **Run** button.</span></span> <span data-ttu-id="6772b-171">toorun z Maven, użyj [exec: exec](http://www.mojohaus.org/exec-maven-plugin/exec-mojo.html).</span><span class="sxs-lookup"><span data-stu-id="6772b-171">toorun from Maven, use [exec:exec](http://www.mojohaus.org/exec-maven-plugin/exec-mojo.html).</span></span>
2. <span data-ttu-id="6772b-172">tooproduce jar autonomiczny, który można uruchomić z jar hello kompilacji wiersza polecenia wszystkie zależności uwzględnione, przy użyciu hello [Maven zestawu wtyczki](http://maven.apache.org/plugins/maven-assembly-plugin/usage.html).</span><span class="sxs-lookup"><span data-stu-id="6772b-172">tooproduce a standalone jar that you can run from command-line build hello jar with all dependencies included, using hello [Maven assembly plugin](http://maven.apache.org/plugins/maven-assembly-plugin/usage.html).</span></span> <span data-ttu-id="6772b-173">Witaj pom.xml w hello [przykładowy kod źródłowy w serwisie github](https://github.com/Azure-Samples/data-lake-store-java-upload-download-get-started/blob/master/pom.xml) zawiera przykładowy sposób toodo to.</span><span class="sxs-lookup"><span data-stu-id="6772b-173">hello pom.xml in hello [example source code on github](https://github.com/Azure-Samples/data-lake-store-java-upload-download-get-started/blob/master/pom.xml) has an example of how toodo this.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6772b-174">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="6772b-174">Next steps</span></span>
* [<span data-ttu-id="6772b-175">Przeglądaj JavaDoc hello zestawu Java SDK</span><span class="sxs-lookup"><span data-stu-id="6772b-175">Explore JavaDoc for hello Java SDK</span></span>](https://azure.github.io/azure-data-lake-store-java/javadoc/)
* [<span data-ttu-id="6772b-176">Zabezpieczanie danych w usłudze Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="6772b-176">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="6772b-177">Korzystanie z usługi Azure Data Lake Analytics z usługą Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="6772b-177">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="6772b-178">Korzystanie z usługi Azure HDInsight z usługą Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="6772b-178">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)

