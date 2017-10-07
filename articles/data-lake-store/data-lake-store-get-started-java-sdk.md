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
# <a name="get-started-with-azure-data-lake-store-using-java"></a>Rozpoczynanie pracy z usługą Azure Data Lake Store przy użyciu języka Java
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

Dowiedz się, jak toouse hello zestawu Java SDK usługi Azure Data Lake Store tooperform podstawowe operacje takie jak tworzenie folderów, przekazywanie i pobieranie plików danych itp. Aby uzyskać więcej informacji o usłudze Data Lake, zobacz temat [Usługa Azure Data Lake Store](data-lake-store-overview.md).

Dokumentacja interfejsu API zestawu SDK Java powitania dla usługi Azure Data Lake Store można uzyskać dostęp [dokumentacja interfejsu API usługi Azure Data Lake magazynu Java](https://azure.github.io/azure-data-lake-store-java/javadoc/).

## <a name="prerequisites"></a>Wymagania wstępne
* Zestaw Java Development Kit (JDK 7 lub nowszy, korzystający z języka Java w wersji 1.7 lub nowszej)
* Konto usługi Azure Data Lake Store. Postępuj zgodnie z instrukcjami hello w [wprowadzenie do usługi Azure Data Lake Store za pomocą portalu Azure hello](data-lake-store-get-started-portal.md).
* [Maven](https://maven.apache.org/install.html). Ten samouczek używa programu Maven na potrzeby zależności między kompilacją i projektem. Chociaż możliwe toobuild bez użycia systemu kompilacji, takich jak Maven i Gradle, Utwórz te systemy jest znacznie łatwiejsze zależności toomanage.
* (Opcjonalnie) Wtyczka [IntelliJ IDEA](https://www.jetbrains.com/idea/download/) lub [Eclipse](https://www.eclipse.org/downloads/) przypominająca środowisko IDE lub podobna.

## <a name="how-do-i-authenticate-using-azure-active-directory"></a>W jaki sposób uwierzytelniać za pomocą usługi Azure Active Directory?
W tym samouczku używamy usługi Azure AD aplikacji klienta tajny tooretrieve tokenu usługi Azure Active Directory (authentication service-to-service). Używamy tej operacji katalogu i toocreate tokenu pliku operacji tooperform obiektu klienta usługi Data Lake Store. Aby uzyskać instrukcje dotyczące sposobu tooauthenticate przy użyciu usługi Azure Data Lake Store hello klucz tajny klienta wykonujemy hello następujące ogólne kroki:

1. Utworzenie aplikacji sieci Web Azure AD
2. Pobieranie Identyfikatora klienta hello, klucz tajny klienta i punktu końcowego tokena dla hello aplikacji sieci web usługi Azure AD.
3. Konfigurowanie dostępu dla aplikacji sieci web usługi Azure AD hello na powitania usługi Data Lake Store plik/folder, który ma tooaccess z hello tworzonej aplikacji w języku Java.

Aby uzyskać instrukcje dotyczące tooperform tych kroków, zobacz temat [tworzenie aplikacji usługi Active Directory](data-lake-store-authenticate-using-active-directory.md).

Usługa Azure Active Directory zapewnia innych opcji oraz tooretrieve tokenu. Można wybrać z liczbą toosuit mechanizmów uwierzytelniania inny scenariusz, na przykład aplikacji działających w przeglądarce, aplikacji rozproszonych jako aplikacji pulpitu lub aplikacji serwera, uruchamiane lokalnie lub w wirtualnej platformy Azure maszyny. Można również wybrać różne rodzaje poświadczeń, takie jak hasła, certyfikaty, uwierzytelnianie 2-etapowe itd. Ponadto usługa Azure Active Directory umożliwia toosynchronize lokalnych użytkowników usługi Active Directory z chmurą hello. Aby uzyskać szczegółowe informacje, zobacz [Scenariusze uwierzytelniania dla usługi Azure Active Directory](../active-directory/active-directory-authentication-scenarios.md). 

## <a name="create-a-java-application"></a>Tworzenie aplikacji Java
Witaj kod przykładowy [w serwisie GitHub](https://azure.microsoft.com/documentation/samples/data-lake-store-java-upload-download-get-started/) przeprowadzi Cię przez proces tworzenia plików w magazynie hello, łączenia plików, pobierania pliku i usuń niektóre pliki w magazynie hello hello. Ta sekcja hello artykułu opisano hello głównych części kodu hello.

1. Utwórz projekt Maven za pomocą [mvn archetype](https://maven.apache.org/guides/getting-started/maven-in-five-minutes.html) z hello wiersza polecenia lub przy użyciu środowiska IDE. Aby uzyskać instrukcje dotyczące sposobu toocreate Java projektu przy użyciu IntelliJ, zobacz [tutaj](https://www.jetbrains.com/help/idea/2016.1/creating-and-running-your-first-java-application.html). Aby uzyskać instrukcje dotyczące toocreate projektu za pomocą programu Eclipse, zobacz [tutaj](http://help.eclipse.org/mars/index.jsp?topic=%2Forg.eclipse.jdt.doc.user%2FgettingStarted%2Fqs-3.htm). 
2. Dodaj następujące zależności tooyour Maven hello **pom.xml** pliku. Dodaj następujące fragment tekstu między hello hello  **\</version >** znacznika i hello  **\</project >** tagu:
   
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
   
    zależność pierwszy Hello jest hello toouse zestawu SDK Data Lake Store (`azure-data-lake-store-sdk`) z hello maven repozytorium. Witaj drugi zależności (`slf4j-nop`) jest toospecify które toouse framework rejestrowania dla tej aplikacji. Witaj zestawu SDK Data Lake Store używa [slf4j](http://www.slf4j.org/) fasad rejestrowania, który pozwala wybrać wiele platform popularnych rejestrowania, takich jak log4j, Java, rejestrowanie, logback, itp., lub bez rejestrowania. W tym przykładzie zostanie wyłączony rejestrowania, dlatego używamy hello **slf4j nop** powiązania. toouse inne opcje logowania w aplikacji, zobacz [tutaj](http://www.slf4j.org/manual.html#projectDep).

### <a name="add-hello-application-code"></a>Dodaj kod aplikacji hello
Istnieją trzy główne części toohello kodu.

1. Uzyskać hello tokenu usługi Azure Active Directory
2. Użyj tokenu toocreate powitania klienta usługi Data Lake Store.
3. Użyj operacji tooperform klienta usługi Data Lake Store hello.

#### <a name="step-1-obtain-an-azure-active-directory-token"></a>Krok 1. Uzyskaj token usługi Azure Active Directory
Witaj zestawu SDK Data Lake Store zapewnia wygodne metody, które umożliwiają zarządzanie tokeny zabezpieczające hello potrzebne toohello tootalk konta usługi Data Lake Store. Jednak hello zestawu SDK nie wprowadzić, że można używać tylko tych metod. Można użyć innych środków do uzyskania tokenu również, jak przy użyciu hello [zestawu SDK usługi Azure Active Directory](https://github.com/AzureAD/azure-activedirectory-library-for-java), lub niestandardowy kod.

toouse hello token tooobtain zestawu SDK Data Lake Store hello Active Directory w sieci Web aplikacji został utworzony wcześniej, użyj jednej z podklasy hello `AccessTokenProvider` (hello poniższym przykładzie użyto `ClientCredsTokenProvider`). Witaj dostawcy tokenu pamięć podręczną hello poświadczenia tooobtain hello token używany w pamięci i hello token odnawia automatycznie, jeśli chodzi o tooexpire. Jest możliwe toocreate własne podklasy `AccessTokenProvider` tokeny są uzyskiwane przez kod klienta, ale teraz umożliwia po prostu użyj hello podać jedną w hello zestawu SDK.

Zastąp **wypełniania-tutaj** hello rzeczywiste wartości dla hello aplikacji sieci Web Azure Active Directory.

    private static String clientId = "FILL-IN-HERE";
    private static String authTokenEndpoint = "FILL-IN-HERE";
    private static String clientKey = "FILL-IN-HERE";

    AccessTokenProvider provider = new ClientCredsTokenProvider(authTokenEndpoint, clientId, clientKey);

#### <a name="step-2-create-an-azure-data-lake-store-client-adlstoreclient-object"></a>Krok 2. Utwórz obiekt klienta usługi Azure Data Lake Store (ADLStoreClient)
Tworzenie [ADLStoreClient](https://azure.github.io/azure-data-lake-store-java/javadoc/) obiekt wymaga toospecify hello usługi Data Lake Store konta nazwy i hello dostawcy tokenów wygenerowanych w ostatnim kroku hello. Należy pamiętać, że hello konta Data Lake Store, że nazwa musi toobe w pełni kwalifikowaną nazwą domeny. Na przykład zastąp ciąg **FILL-IN-HERE** (Wypełnij tutaj) czymś w rodzaju **mydatalakestore.azuredatalakestore.net**.

    private static String accountFQDN = "FILL-IN-HERE";  // full account FQDN, not just hello account name
    ADLStoreClient client = ADLStoreClient.createClient(accountFQDN, provider);

### <a name="step-3-use-hello-adlstoreclient-tooperform-file-and-directory-operations"></a>Krok 3: Użyj hello ADLStoreClient tooperform plików i katalogów operacji
Poniższy kod Hello zawiera przykładowe fragmenty niektórych typowych operacji. Można przyjrzeć się hello pełne [dokumentacja interfejsu API zestawu SDK Java Data Lake magazynu](https://azure.github.io/azure-data-lake-store-java/javadoc/) z hello **ADLStoreClient** obiekt toosee innych operacji.

Pamiętaj, że pliki są odczytywane i zapisywane za pomocą standardowych strumieni Java. Oznacza to, że można dowolną hello Java strumienie na powitania Data Lake — magazyn strumieni toobenefit ze standardowych funkcji języka Java (np. drukowania strumieni sformatowane wyniki ani żadnych strumieni kompresji i szyfrowania hello dodatkowe funkcje na warstwy "TOP, itp.).

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

#### <a name="step-4-build-and-run-hello-application"></a>Krok 4: Tworzenie i uruchamianie aplikacji hello
1. toorun od w IDE zlokalizuj i naciśnij klawisz hello **Uruchom** przycisku. toorun z Maven, użyj [exec: exec](http://www.mojohaus.org/exec-maven-plugin/exec-mojo.html).
2. tooproduce jar autonomiczny, który można uruchomić z jar hello kompilacji wiersza polecenia wszystkie zależności uwzględnione, przy użyciu hello [Maven zestawu wtyczki](http://maven.apache.org/plugins/maven-assembly-plugin/usage.html). Witaj pom.xml w hello [przykładowy kod źródłowy w serwisie github](https://github.com/Azure-Samples/data-lake-store-java-upload-download-get-started/blob/master/pom.xml) zawiera przykładowy sposób toodo to.

## <a name="next-steps"></a>Następne kroki
* [Przeglądaj JavaDoc hello zestawu Java SDK](https://azure.github.io/azure-data-lake-store-java/javadoc/)
* [Zabezpieczanie danych w usłudze Data Lake Store](data-lake-store-secure-data.md)
* [Korzystanie z usługi Azure Data Lake Analytics z usługą Data Lake Store](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [Korzystanie z usługi Azure HDInsight z usługą Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md)

