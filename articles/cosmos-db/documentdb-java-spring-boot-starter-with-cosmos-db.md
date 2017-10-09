---
title: "Witaj toouse aaaHow Spring początkowego rozruchu z interfejsu API Azure rozwiązania Cosmos bazy danych usługi DocumentDB"
description: "Dowiedz się, jak tooconfigure aplikacji utworzone z hello Spring inicjatora rozruchu z hello interfejsu API Azure rozwiązania Cosmos bazy danych usługi DocumentDB."
services: cosmos-db
documentationcenter: java
author: rmcmurray
manager: cfowler
editor: 
keywords: "Rozwiązania Cosmos Spring, Spring początkowego rozruchu, bazy danych"
ms.assetid: 
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: article
ms.date: 08/08/2017
ms.author: robmcm;yungez;kevinzha
ms.openlocfilehash: a2c6de678f850676cb2887e224e5c12950db0e53
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-spring-boot-starter-with-azure-cosmos-db-documentdb-api"></a><span data-ttu-id="cbc15-104">Jak toouse hello Spring początkowego rozruchu z interfejsu API Azure rozwiązania Cosmos bazy danych usługi DocumentDB</span><span class="sxs-lookup"><span data-stu-id="cbc15-104">How toouse hello Spring Boot Starter with Azure Cosmos DB DocumentDB API</span></span>

## <a name="overview"></a><span data-ttu-id="cbc15-105">Omówienie</span><span class="sxs-lookup"><span data-stu-id="cbc15-105">Overview</span></span>

<span data-ttu-id="cbc15-106">Witaj  **[Spring Framework]**  to rozwiązanie open source, które pomaga deweloperom języka Java, tworzenie aplikacji na poziomie przedsiębiorstwa.</span><span class="sxs-lookup"><span data-stu-id="cbc15-106">hello **[Spring Framework]** is an open-source solution that helps Java developers create enterprise-level applications.</span></span> <span data-ttu-id="cbc15-107">Jednego z projektów innych popularnych hello, które jest wbudowane znajdujący się na platformie jest [rozruchu Spring], zapewniające uproszczone podejście do tworzenia aplikacji Java autonomicznych.</span><span class="sxs-lookup"><span data-stu-id="cbc15-107">One of hello more-popular projects that is built on top of that platform is [Spring Boot], which provides a simplified approach for creating stand-alone Java applications.</span></span> <span data-ttu-id="cbc15-108">Deweloperzy toohelp rozpocząć pracę z rozruchem Spring, kilka pakietów rozruchu Spring próbki są dostępne pod adresem <https://github.com/spring-guides/>.</span><span class="sxs-lookup"><span data-stu-id="cbc15-108">toohelp developers get started with Spring Boot, several sample Spring Boot packages are available at <https://github.com/spring-guides/>.</span></span> <span data-ttu-id="cbc15-109">Ponadto toochoosing z hello Lista podstawowa rozruchu Spring projektów, hello  **[Spring Initializr]**  ułatwia deweloperom szybkie wprowadzenie do tworzenia niestandardowych aplikacji rozruchu sprężyny.</span><span class="sxs-lookup"><span data-stu-id="cbc15-109">In addition toochoosing from hello list of basic Spring Boot projects, hello **[Spring Initializr]** helps developers get started with creating custom Spring Boot applications.</span></span>

<span data-ttu-id="cbc15-110">Azure DB rozwiązania Cosmos jest usługą globalnie rozproszone bazy danych, która umożliwia deweloperom stosowanie toowork z danymi przy użyciu różnych standardowych interfejsów API, takich jak usługi DocumentDB, bazy danych MongoDB, wykres i tabela interfejsów API.</span><span class="sxs-lookup"><span data-stu-id="cbc15-110">Azure Cosmos DB is a globally-distributed database service that allows developers toowork with data using a variety of standard APIs, such as DocumentDB, MongoDB, Graph, and Table APIs.</span></span> <span data-ttu-id="cbc15-111">Początkowy rozruchu Spring firmy Microsoft umożliwia deweloperom toouse rozruchu Spring aplikacji, które łatwo zintegrować z bazy danych rozwiązania Cosmos Azure za pomocą interfejsów API usługi DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="cbc15-111">Microsoft's Spring Boot Starter enables developers toouse Spring Boot applications that easily integrate with Azure Cosmos DB by using DocumentDB APIs.</span></span>

<span data-ttu-id="cbc15-112">W tym artykule przedstawiono tworzenie rozwiązania Cosmos bazy danych platformy Azure przy użyciu hello portalu Azure, a następnie za pomocą hello **Spring Initializr** toocreate aplikację java niestandardowe, a następnie dodaj hello początkowego rozruchu Spring funkcji tooyour niestandardowe dane toostore aplikacji i pobierania danych z bazy danych programu Azure rozwiązania Cosmos przy użyciu hello interfejsu API usługi DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="cbc15-112">This article demonstrates creating an Azure Cosmos DB using hello Azure portal, then using hello **Spring Initializr** toocreate a custom java application, and then add hello Spring Boot Starter functionality tooyour custom application toostore data in and retrieve data from your Azure Cosmos DB by using hello DocumentDB API.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cbc15-113">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="cbc15-113">Prerequisites</span></span>

<span data-ttu-id="cbc15-114">Witaj, następujące wymagania wstępne są wymagane w kolejności toofollow hello opisanych w tym artykule:</span><span class="sxs-lookup"><span data-stu-id="cbc15-114">hello following prerequisites are required in order toofollow hello steps in this article:</span></span>

* <span data-ttu-id="cbc15-115">Subskrypcja platformy Azure; Jeśli nie masz jeszcze subskrypcji platformy Azure, możesz przeprowadzić aktywację Twojej [korzyści dla subskrybentów MSDN] lub zarejestrować się w celu [bezpłatne konto platformy Azure].</span><span class="sxs-lookup"><span data-stu-id="cbc15-115">An Azure subscription; if you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits] or sign up for a [free Azure account].</span></span>

* <span data-ttu-id="cbc15-116">A [Java Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/), wersji 1,7 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="cbc15-116">A [Java Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/), version 1.7 or later.</span></span>

* <span data-ttu-id="cbc15-117">[Apache Maven](http://maven.apache.org/), w wersji 3.0 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="cbc15-117">[Apache Maven](http://maven.apache.org/), version 3.0 or later.</span></span>

## <a name="create-an-azure-cosmos-db-by-using-hello-azure-portal"></a><span data-ttu-id="cbc15-118">Tworzenie bazy danych Azure rozwiązania Cosmos przy użyciu hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="cbc15-118">Create an Azure Cosmos DB by using hello Azure portal</span></span>

1. <span data-ttu-id="cbc15-119">Przeglądaj toohello Azure w portalu <https://portal.azure.com/> i kliknij przycisk **+ nowy**.</span><span class="sxs-lookup"><span data-stu-id="cbc15-119">Browse toohello Azure portal at <https://portal.azure.com/> and click **+New**.</span></span>

   ![Azure Portal][AZ01]

1. <span data-ttu-id="cbc15-121">Kliknij przycisk **baz danych**, a następnie kliknij przycisk **bazy danych Azure rozwiązania Cosmos**.</span><span class="sxs-lookup"><span data-stu-id="cbc15-121">Click **Databases**, and then click **Azure Cosmos DB**.</span></span>

   ![Azure Portal][AZ02]

1. <span data-ttu-id="cbc15-123">Na powitania **bazy danych Azure rozwiązania Cosmos** wprowadź hello następujących informacji:</span><span class="sxs-lookup"><span data-stu-id="cbc15-123">On hello **Azure Cosmos DB** page, enter hello following information:</span></span>

   * <span data-ttu-id="cbc15-124">Wprowadź unikatową **identyfikator**, który będzie używany jako hello identyfikatora URI dla bazy danych.</span><span class="sxs-lookup"><span data-stu-id="cbc15-124">Enter a unique **ID**, which you will use as hello URI for your database.</span></span> <span data-ttu-id="cbc15-125">Na przykład: *wingtiptoysdata.documents.azure.com*.</span><span class="sxs-lookup"><span data-stu-id="cbc15-125">For example: *wingtiptoysdata.documents.azure.com*.</span></span>
   * <span data-ttu-id="cbc15-126">Wybierz **SQL (DB dokumentu)** dla hello interfejsu API.</span><span class="sxs-lookup"><span data-stu-id="cbc15-126">Choose **SQL (Document DB)** for hello API.</span></span>
   * <span data-ttu-id="cbc15-127">Wybierz hello **subskrypcji** ma toouse bazy danych.</span><span class="sxs-lookup"><span data-stu-id="cbc15-127">Choose hello **Subscription** you want toouse for your database.</span></span>
   * <span data-ttu-id="cbc15-128">Określ, czy toocreate nowy **grupy zasobów** bazy danych, lub wybierz istniejącą grupę zasobów.</span><span class="sxs-lookup"><span data-stu-id="cbc15-128">Specify whether toocreate a new **Resource group** for your database, or choose an existing resource group.</span></span>
   * <span data-ttu-id="cbc15-129">Określ hello **lokalizacji** bazy danych.</span><span class="sxs-lookup"><span data-stu-id="cbc15-129">Specify hello **Location** for your database.</span></span>
   
   <span data-ttu-id="cbc15-130">Po określeniu tych opcji, kliknij przycisk **Utwórz** toocreate bazy danych.</span><span class="sxs-lookup"><span data-stu-id="cbc15-130">When you have specified these options, click **Create** toocreate your database.</span></span>

   ![Azure Portal][AZ03]

1. <span data-ttu-id="cbc15-132">Podczas tworzenia bazy danych znajduje się w sieci Azure **pulpitu nawigacyjnego**, jak również zgodnie z hello **wszystkie zasoby** i **bazy danych Azure rozwiązania Cosmos** stron.</span><span class="sxs-lookup"><span data-stu-id="cbc15-132">When your database has been created, it is listed on your Azure **Dashboard**, as well as under hello **All Resources** and **Azure Cosmos DB** pages.</span></span> <span data-ttu-id="cbc15-133">Możesz kliknąć bazy danych na żadnym z tych lokalizacji tooopen hello właściwości strony dla pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="cbc15-133">You can click on your database on any of those locations tooopen hello properties page for your cache.</span></span>

   ![Azure Portal][AZ04]

1. <span data-ttu-id="cbc15-135">Gdy zostanie wyświetlona strona właściwości hello bazy danych, kliknij przycisk **klucze dostępu** i skopiuj klucze dostępu i identyfikator URI dla Twojej bazy danych; te wartości zostaną użyte w aplikacji rozruchu sprężyny.</span><span class="sxs-lookup"><span data-stu-id="cbc15-135">When hello properties page for your database is displayed, click **Access keys** and copy your URI and access keys for your database; you will use these values in your Spring Boot application.</span></span>

   ![Azure Portal][AZ05]

## <a name="create-a-simple-spring-boot-application-with-hello-spring-initializr"></a><span data-ttu-id="cbc15-137">Utworzyć prostą aplikację Spring rozruchu z hello Spring Initializr</span><span class="sxs-lookup"><span data-stu-id="cbc15-137">Create a simple Spring Boot application with hello Spring Initializr</span></span>

1. <span data-ttu-id="cbc15-138">Przeglądaj zbyt<https://start.spring.io/>.</span><span class="sxs-lookup"><span data-stu-id="cbc15-138">Browse too<https://start.spring.io/>.</span></span>

1. <span data-ttu-id="cbc15-139">Określ, czy toogenerate **Maven** projektu z **Java**, wprowadź hello **grupy** i **artefaktu** nazwy aplikacji, i następnie kliknij przycisk hello zbyt**Generowanie projektu**.</span><span class="sxs-lookup"><span data-stu-id="cbc15-139">Specify that you want toogenerate a **Maven** project with **Java**, enter hello **Group** and **Artifact** names for your application, and then click hello button too**Generate Project**.</span></span>

   ![Opcje Initializr Basic Spring][SI01]

   > [!NOTE]
   >
   > <span data-ttu-id="cbc15-141">Hello Spring Initializr używa hello **grupy** i **artefaktu** nazwy pakietu hello toocreate nazwy, na przykład: *com.example.wintiptoys*.</span><span class="sxs-lookup"><span data-stu-id="cbc15-141">hello Spring Initializr uses hello **Group** and **Artifact** names toocreate hello package name; for example: *com.example.wintiptoys*.</span></span>
   >

1. <span data-ttu-id="cbc15-142">Po wyświetleniu monitu, Pobierz hello ścieżka tooa projektu na komputerze lokalnym.</span><span class="sxs-lookup"><span data-stu-id="cbc15-142">When prompted, download hello project tooa path on your local computer.</span></span>

   ![Pobierz niestandardowy projekt Spring rozruchu][SI02]

1. <span data-ttu-id="cbc15-144">Po wyodrębnieniu plików hello w systemie lokalnym, prosty aplikacji rozruchu Spring będzie gotowy do edycji.</span><span class="sxs-lookup"><span data-stu-id="cbc15-144">After you have extracted hello files on your local system, your simple Spring Boot application will be ready for editing.</span></span>

   ![Pliki projektu rozruchu Spring niestandardowe][SI03]

## <a name="configure-your-spring-boot-app-toouse-hello-azure-spring-boot-starter"></a><span data-ttu-id="cbc15-146">Konfigurowanie programu rozruchowego Spring aplikacji toouse hello początkowego rozruchu Spring Azure</span><span class="sxs-lookup"><span data-stu-id="cbc15-146">Configure your Spring Boot app toouse hello Azure Spring Boot Starter</span></span>

1. <span data-ttu-id="cbc15-147">Zlokalizuj hello *pom.xml* pliku w katalogu hello aplikacji; na przykład:</span><span class="sxs-lookup"><span data-stu-id="cbc15-147">Locate hello *pom.xml* file in hello directory of your app; for example:</span></span>

   `C:\SpringBoot\wingtiptoys\pom.xml`

   <span data-ttu-id="cbc15-148">— lub —</span><span class="sxs-lookup"><span data-stu-id="cbc15-148">-or-</span></span>

   `/users/example/home/wingtiptoys/pom.xml`

   ![Zlokalizuj plik pom.xml hello][PM01]

1. <span data-ttu-id="cbc15-150">Otwórz hello *pom.xml* plik w edytorze tekstu, a następnie dodaj powitania po toolist wierszy z `<dependencies>`:</span><span class="sxs-lookup"><span data-stu-id="cbc15-150">Open hello *pom.xml* file in a text editor, and add hello following lines toolist of `<dependencies>`:</span></span>

   ```xml
   <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-documentdb-spring-boot-starter</artifactId>
      <version>0.1.4</version>
   </dependency>
   ```

   ![Edytowanie pliku pom.xml hello][PM02]

1. <span data-ttu-id="cbc15-152">Zapisz i zamknij hello *pom.xml* pliku.</span><span class="sxs-lookup"><span data-stu-id="cbc15-152">Save and close hello *pom.xml* file.</span></span>

## <a name="configure-your-spring-boot-app-toouse-your-azure-cosmos-db"></a><span data-ttu-id="cbc15-153">Konfigurowanie programu rozruchowego Spring toouse aplikacji bazy danych programu Azure rozwiązania Cosmos</span><span class="sxs-lookup"><span data-stu-id="cbc15-153">Configure your Spring Boot app toouse your Azure Cosmos DB</span></span>

1. <span data-ttu-id="cbc15-154">Zlokalizuj hello *application.properties* pliku w hello *zasobów* katalogu aplikacji, np.:</span><span class="sxs-lookup"><span data-stu-id="cbc15-154">Locate hello *application.properties* file in hello *resources* directory of your app; for example:</span></span>

   `C:\SpringBoot\wingtiptoys\src\main\resources\application.properties`

   <span data-ttu-id="cbc15-155">— lub —</span><span class="sxs-lookup"><span data-stu-id="cbc15-155">-or-</span></span>

   `/users/example/home/wingtiptoys/src/main/resources/application.properties`

   ![Znajdź plik application.properties hello][RE01]

1. <span data-ttu-id="cbc15-157">Otwórz hello *application.properties* plik w edytorze tekstów i Dodaj poniższe wiersze toohello plik hello i Zamień hello przykładowe wartości hello odpowiednie właściwości bazy danych:</span><span class="sxs-lookup"><span data-stu-id="cbc15-157">Open hello *application.properties* file in a text editor, and add hello following lines toohello file, and replace hello sample values with hello appropriate properties for your database:</span></span>

   ```yaml
   # Specify hello DNS URI of your Azure Cosmos DB.
   azure.documentdb.uri=https://wingtiptoys.documents.azure.com:443/

   # Specify hello access key for your database.
   azure.documentdb.key=57686f6120447564652c20426f6220526f636b73==

   # Specify hello name of your database.
   azure.documentdb.database=wingtiptoysdata
   ```

   ![Edytowanie pliku application.properties hello][RE02]

1. <span data-ttu-id="cbc15-159">Zapisz i zamknij hello *application.properties* pliku.</span><span class="sxs-lookup"><span data-stu-id="cbc15-159">Save and close hello *application.properties* file.</span></span>

## <a name="add-sample-code-tooimplement-basic-database-functionality"></a><span data-ttu-id="cbc15-160">Dodawanie funkcji podstawowych bazy danych tooimplement kod przykładowy</span><span class="sxs-lookup"><span data-stu-id="cbc15-160">Add sample code tooimplement basic database functionality</span></span>

<span data-ttu-id="cbc15-161">W tej sekcji utworzysz dwie klasy Java do przechowywania danych użytkownika, a następnie zmodyfikować Twojej aplikacji głównej klasy toocreate wystąpienia klasy użytkownika hello i zapisać go tooyour bazy danych.</span><span class="sxs-lookup"><span data-stu-id="cbc15-161">In this section you create two Java classes for storing user data, and then you modify your main application class toocreate an instance of hello user class and save it tooyour database.</span></span>

### <a name="define-a-basic-class-for-storing-user-data"></a><span data-ttu-id="cbc15-162">Definiowanie podstawowe klasy do przechowywania danych użytkownika</span><span class="sxs-lookup"><span data-stu-id="cbc15-162">Define a basic class for storing user data</span></span>

1. <span data-ttu-id="cbc15-163">Utwórz nowy plik o nazwie *User.java* hello — w tym samym katalogu co plik głównej aplikacji Java.</span><span class="sxs-lookup"><span data-stu-id="cbc15-163">Create a new file named *User.java* in hello same directory as your main application Java file.</span></span>

1. <span data-ttu-id="cbc15-164">Otwórz hello *User.java* plik w edytorze tekstów i dodaj następujące hello linii toodefine pliku toohello klasy rodzajowe użytkownika, która przechowuje i pobrać wartości w bazie danych:</span><span class="sxs-lookup"><span data-stu-id="cbc15-164">Open hello *User.java* file in a text editor, and add hello following lines toohello file toodefine a generic user class that stores and retrieve values in your database:</span></span>

   ```java
   package com.example.wingtiptoys;

   public class User {
      private String id;
      private String firstName;
      private String lastName;
 
      public User(String id, String firstName, String lastName) {
         this.id = id;
         this.firstName = firstName;
         this.lastName = lastName;
      }
   
      public String getId() {
         return this.id;
      }

      public void setId(String id) {
         this.id = id;
      }

      public String getFirstName() {
         return firstName;
      }

      public void setFirstName(String firstName) {
         this.firstName = firstName;
      }

      public String getLastName() {
         return lastName;
      }

      public void setLastName(String lastName) {
         this.lastName = lastName;
      }

      @Override
      public String toString() {
         return String.format("User: %s %s", firstName, lastName);
      }
   }
   ```

1. <span data-ttu-id="cbc15-165">Zapisz i zamknij hello *User.java* pliku.</span><span class="sxs-lookup"><span data-stu-id="cbc15-165">Save and close hello *User.java* file.</span></span>

### <a name="define-a-data-repository-interface"></a><span data-ttu-id="cbc15-166">Zdefiniuj interfejs repozytorium danych</span><span class="sxs-lookup"><span data-stu-id="cbc15-166">Define a data repository interface</span></span>

1. <span data-ttu-id="cbc15-167">Utwórz nowy plik o nazwie *UserRepository.java* hello — w tym samym katalogu co plik głównej aplikacji Java.</span><span class="sxs-lookup"><span data-stu-id="cbc15-167">Create a new file named *UserRepository.java* in hello same directory as your main application Java file.</span></span>

1. <span data-ttu-id="cbc15-168">Otwórz hello *UserRepository.java* plik w edytorze tekstów i dodaj następujące hello linii toodefine pliku toohello repozytorium interfejs, który rozszerza interfejs repozytorium usługi DocumentDB domyślny hello:</span><span class="sxs-lookup"><span data-stu-id="cbc15-168">Open hello *UserRepository.java* file in a text editor, and add hello following lines toohello file toodefine a user repository interface that extends hello default DocumentDB repository interface:</span></span>

   ```java
   package com.example.wingtiptoys;

   import com.microsoft.azure.spring.data.documentdb.repository.DocumentDbRepository;
   import org.springframework.stereotype.Repository;

   @Repository
   public interface UserRepository extends DocumentDbRepository<User, String> {}   
   ```

1. <span data-ttu-id="cbc15-169">Zapisz i zamknij hello *UserRepository.java* pliku.</span><span class="sxs-lookup"><span data-stu-id="cbc15-169">Save and close hello *UserRepository.java* file.</span></span>

### <a name="modify-hello-main-application-class"></a><span data-ttu-id="cbc15-170">Modyfikowanie klasy głównym aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="cbc15-170">Modify hello main application class</span></span>

1. <span data-ttu-id="cbc15-171">Zlokalizuj plik Java głównej aplikacji hello w katalogu pakietów hello aplikacji; na przykład:</span><span class="sxs-lookup"><span data-stu-id="cbc15-171">Locate hello main application Java file in hello package directory of your app; for example:</span></span>

   `C:\SpringBoot\wingtiptoys\src\main\java\com\example\wingtiptoys\WingtiptoysApplication.java`

   <span data-ttu-id="cbc15-172">— lub —</span><span class="sxs-lookup"><span data-stu-id="cbc15-172">-or-</span></span>

   `/users/example/home/wingtiptoys/src/main/java/com/example/wingtiptoys/WingtiptoysApplication.java`

   ![Zlokalizuj plik Java aplikacji hello][JV01]

1. <span data-ttu-id="cbc15-174">Otwórz plik Java głównej aplikacji hello w edytorze tekstów, a następnie dodaj poniższe wiersze toohello plik hello:</span><span class="sxs-lookup"><span data-stu-id="cbc15-174">Open hello main application Java file in a text editor, and add hello following lines toohello file:</span></span>

   ```java
   package com.example.wingtiptoys;

   import org.springframework.boot.SpringApplication;
   import org.springframework.boot.autoconfigure.SpringBootApplication;
   import org.springframework.beans.factory.annotation.Autowired;
   import org.springframework.boot.CommandLineRunner;

   @SpringBootApplication
   public class WingtiptoysApplication implements CommandLineRunner {

      @Autowired
      private UserRepository repository;
    
      public static void main(String[] args) {
         SpringApplication.run(WingtiptoysApplication.class, args);
      }

      public void run(String... var1) throws Exception {
         final User testUser = new User("testId", "testFirstName", "testLastName");

         repository.deleteAll();
         repository.save(testUser);

         final User result = repository.findOne(testUser.getId());

         System.out.printf("\n\n%s\n\n",result.toString());
      }
   }
   ```

1. <span data-ttu-id="cbc15-175">Zapisz i zamknij plik Java głównej aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="cbc15-175">Save and close hello main application Java file.</span></span>

## <a name="build-and-test-your-app"></a><span data-ttu-id="cbc15-176">Tworzenie i testowanie aplikacji</span><span class="sxs-lookup"><span data-stu-id="cbc15-176">Build and test your app</span></span>

1. <span data-ttu-id="cbc15-177">Otwórz wiersz polecenia i zmień folder katalogu toohello gdy Twoje *pom.xml* znajduje się plik, na przykład:</span><span class="sxs-lookup"><span data-stu-id="cbc15-177">Open a command prompt and change directory toohello folder where your *pom.xml* file is located; for example:</span></span>

   `cd C:\SpringBoot\wingtiptoys`

   <span data-ttu-id="cbc15-178">— lub —</span><span class="sxs-lookup"><span data-stu-id="cbc15-178">-or-</span></span>

   `cd /users/example/home/wingtiptoys`

1. <span data-ttu-id="cbc15-179">Tworzenie aplikacji Spring rozruchu z Maven i uruchamianie na przykład:</span><span class="sxs-lookup"><span data-stu-id="cbc15-179">Build your Spring Boot application with Maven and run it; for example:</span></span>

   ```shell
   mvn package
   java -jar target/wingtiptoys-0.0.1-SNAPSHOT.jar
   ```

1. <span data-ttu-id="cbc15-180">Aplikacja wyświetli komunikaty środowiska uruchomieniowego i powinna zostać wyświetlona wiadomość hello `User: testFirstName testLastName` wyświetlane tooindicate, że wartości zostały pomyślnie przechowywane i pobierane z bazy danych.</span><span class="sxs-lookup"><span data-stu-id="cbc15-180">Your application will display several runtime messages, and you should see hello message `User: testFirstName testLastName` displayed tooindicate that values have been successfully stored and retrieved from your database.</span></span>

   ![Pomyślne dane wyjściowe aplikacji hello][JV02]

1. <span data-ttu-id="cbc15-182">OPCJONALNIE: Można hello Azure tooview portalu hello zawartość Twojego rozwiązania Cosmos bazy danych Azure na stronie właściwości hello bazy danych, klikając **Eksploratora dokumentów**i wybierając element i z hello wyświetlana lista tooview hello zawartość.</span><span class="sxs-lookup"><span data-stu-id="cbc15-182">OPTIONAL: You can use hello Azure portal tooview hello contents of your Azure Cosmos DB from hello properties page for your database by clicking  **Document Explorer**, and then selecting and item from hello displayed list tooview hello contents.</span></span>

   ![Przy użyciu tooview Eksploratora dokumentów hello danych][JV03]

## <a name="next-steps"></a><span data-ttu-id="cbc15-184">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="cbc15-184">Next steps</span></span>

<span data-ttu-id="cbc15-185">Aby uzyskać więcej informacji na temat korzystania z bazy danych Azure rozwiązania Cosmos i Java zobacz następujące artykuły hello:</span><span class="sxs-lookup"><span data-stu-id="cbc15-185">For more information about using Azure Cosmos DB and Java, see hello following articles:</span></span>

* <span data-ttu-id="cbc15-186">[Dokumentacja rozwiązania Cosmos Azure DB].</span><span class="sxs-lookup"><span data-stu-id="cbc15-186">[Azure Cosmos DB Documentation].</span></span>

* <span data-ttu-id="cbc15-187">[Azure DB rozwiązania Cosmos: Tworzenie aplikacji interfejsu API usługi DocumentDB z językiem Java i hello portalu Azure][Build a DocumentDB API app with Java]</span><span class="sxs-lookup"><span data-stu-id="cbc15-187">[Azure Cosmos DB: Build a DocumentDB API app with Java and hello Azure portal][Build a DocumentDB API app with Java]</span></span>

<span data-ttu-id="cbc15-188">Aby uzyskać więcej informacji o używaniu aplikacji rozruchu Spring na platformie Azure zobacz następujące artykuły hello:</span><span class="sxs-lookup"><span data-stu-id="cbc15-188">For more information about using Spring Boot applications on Azure, see hello following articles:</span></span>

* [<span data-ttu-id="cbc15-189">Spring rozruchu DocumenDB początkowy dla platformy Azure</span><span class="sxs-lookup"><span data-stu-id="cbc15-189">Spring Boot DocumenDB Starter for Azure</span></span>](https://github.com/Microsoft/azure-spring-boot-starters/tree/master/azure-documentdb-spring-boot-starter-sample)

* [<span data-ttu-id="cbc15-190">Wdrażanie aplikacji rozruchu Spring toohello usłudze Azure App Service</span><span class="sxs-lookup"><span data-stu-id="cbc15-190">Deploy a Spring Boot Application toohello Azure App Service</span></span>](../app-service/app-service-deploy-spring-boot-web-app-on-azure.md)

* [<span data-ttu-id="cbc15-191">Działającej aplikacja rozruchu Spring w klastrze Kubernetes w hello usługi kontenera platformy Azure</span><span class="sxs-lookup"><span data-stu-id="cbc15-191">Running a Spring Boot Application on a Kubernetes Cluster in hello Azure Container Service</span></span>](../container-service/container-service-deploy-spring-boot-app-on-kubernetes.md)

<span data-ttu-id="cbc15-192">Aby uzyskać więcej informacji o korzystaniu z językiem Java Azure, zobacz hello [Azure Java Developer Center] i hello [Java Tools for Visual Studio Team Services].</span><span class="sxs-lookup"><span data-stu-id="cbc15-192">For more information about using Azure with Java, see hello [Azure Java Developer Center] and hello [Java Tools for Visual Studio Team Services].</span></span>

<!-- URL List -->

[Dokumentacja rozwiązania Cosmos Azure DB]: /azure/cosmos-db/
[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/
[Build a DocumentDB API app with Java]: https://docs.microsoft.com/azure/cosmos-db/create-documentdb-java
[bezpłatne konto platformy Azure]: https://azure.microsoft.com/pricing/free-trial/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[korzyści dla subskrybentów MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[rozruchu Spring]: http://projects.spring.io/spring-boot/
[Spring Initializr]: https://start.spring.io/
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[AZ01]: ./media/documentdb-java-spring-boot-starter-with-cosmos-db/AZ01.png
[AZ02]: ./media/documentdb-java-spring-boot-starter-with-cosmos-db/AZ02.png
[AZ03]: ./media/documentdb-java-spring-boot-starter-with-cosmos-db/AZ03.png
[AZ04]: ./media/documentdb-java-spring-boot-starter-with-cosmos-db/AZ04.png
[AZ05]: ./media/documentdb-java-spring-boot-starter-with-cosmos-db/AZ05.png

[SI01]: ./media/documentdb-java-spring-boot-starter-with-cosmos-db/SI01.png
[SI02]: ./media/documentdb-java-spring-boot-starter-with-cosmos-db/SI02.png
[SI03]: ./media/documentdb-java-spring-boot-starter-with-cosmos-db/SI03.png

[RE01]: ./media/documentdb-java-spring-boot-starter-with-cosmos-db/RE01.png
[RE02]: ./media/documentdb-java-spring-boot-starter-with-cosmos-db/RE02.png

[PM01]: ./media/documentdb-java-spring-boot-starter-with-cosmos-db/PM01.png
[PM02]: ./media/documentdb-java-spring-boot-starter-with-cosmos-db/PM02.png

[JV01]: ./media/documentdb-java-spring-boot-starter-with-cosmos-db/JV01.png
[JV02]: ./media/documentdb-java-spring-boot-starter-with-cosmos-db/JV02.png
[JV03]: ./media/documentdb-java-spring-boot-starter-with-cosmos-db/JV03.png
