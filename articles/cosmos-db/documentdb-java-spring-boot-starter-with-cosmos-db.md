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
# <a name="how-toouse-hello-spring-boot-starter-with-azure-cosmos-db-documentdb-api"></a>Jak toouse hello Spring początkowego rozruchu z interfejsu API Azure rozwiązania Cosmos bazy danych usługi DocumentDB

## <a name="overview"></a>Omówienie

Witaj  **[Spring Framework]**  to rozwiązanie open source, które pomaga deweloperom języka Java, tworzenie aplikacji na poziomie przedsiębiorstwa. Jednego z projektów innych popularnych hello, które jest wbudowane znajdujący się na platformie jest [rozruchu Spring], zapewniające uproszczone podejście do tworzenia aplikacji Java autonomicznych. Deweloperzy toohelp rozpocząć pracę z rozruchem Spring, kilka pakietów rozruchu Spring próbki są dostępne pod adresem <https://github.com/spring-guides/>. Ponadto toochoosing z hello Lista podstawowa rozruchu Spring projektów, hello  **[Spring Initializr]**  ułatwia deweloperom szybkie wprowadzenie do tworzenia niestandardowych aplikacji rozruchu sprężyny.

Azure DB rozwiązania Cosmos jest usługą globalnie rozproszone bazy danych, która umożliwia deweloperom stosowanie toowork z danymi przy użyciu różnych standardowych interfejsów API, takich jak usługi DocumentDB, bazy danych MongoDB, wykres i tabela interfejsów API. Początkowy rozruchu Spring firmy Microsoft umożliwia deweloperom toouse rozruchu Spring aplikacji, które łatwo zintegrować z bazy danych rozwiązania Cosmos Azure za pomocą interfejsów API usługi DocumentDB.

W tym artykule przedstawiono tworzenie rozwiązania Cosmos bazy danych platformy Azure przy użyciu hello portalu Azure, a następnie za pomocą hello **Spring Initializr** toocreate aplikację java niestandardowe, a następnie dodaj hello początkowego rozruchu Spring funkcji tooyour niestandardowe dane toostore aplikacji i pobierania danych z bazy danych programu Azure rozwiązania Cosmos przy użyciu hello interfejsu API usługi DocumentDB.

## <a name="prerequisites"></a>Wymagania wstępne

Witaj, następujące wymagania wstępne są wymagane w kolejności toofollow hello opisanych w tym artykule:

* Subskrypcja platformy Azure; Jeśli nie masz jeszcze subskrypcji platformy Azure, możesz przeprowadzić aktywację Twojej [korzyści dla subskrybentów MSDN] lub zarejestrować się w celu [bezpłatne konto platformy Azure].

* A [Java Development Kit (JDK)](http://www.oracle.com/technetwork/java/javase/downloads/), wersji 1,7 lub nowszej.

* [Apache Maven](http://maven.apache.org/), w wersji 3.0 lub nowszej.

## <a name="create-an-azure-cosmos-db-by-using-hello-azure-portal"></a>Tworzenie bazy danych Azure rozwiązania Cosmos przy użyciu hello portalu Azure

1. Przeglądaj toohello Azure w portalu <https://portal.azure.com/> i kliknij przycisk **+ nowy**.

   ![Azure Portal][AZ01]

1. Kliknij przycisk **baz danych**, a następnie kliknij przycisk **bazy danych Azure rozwiązania Cosmos**.

   ![Azure Portal][AZ02]

1. Na powitania **bazy danych Azure rozwiązania Cosmos** wprowadź hello następujących informacji:

   * Wprowadź unikatową **identyfikator**, który będzie używany jako hello identyfikatora URI dla bazy danych. Na przykład: *wingtiptoysdata.documents.azure.com*.
   * Wybierz **SQL (DB dokumentu)** dla hello interfejsu API.
   * Wybierz hello **subskrypcji** ma toouse bazy danych.
   * Określ, czy toocreate nowy **grupy zasobów** bazy danych, lub wybierz istniejącą grupę zasobów.
   * Określ hello **lokalizacji** bazy danych.
   
   Po określeniu tych opcji, kliknij przycisk **Utwórz** toocreate bazy danych.

   ![Azure Portal][AZ03]

1. Podczas tworzenia bazy danych znajduje się w sieci Azure **pulpitu nawigacyjnego**, jak również zgodnie z hello **wszystkie zasoby** i **bazy danych Azure rozwiązania Cosmos** stron. Możesz kliknąć bazy danych na żadnym z tych lokalizacji tooopen hello właściwości strony dla pamięci podręcznej.

   ![Azure Portal][AZ04]

1. Gdy zostanie wyświetlona strona właściwości hello bazy danych, kliknij przycisk **klucze dostępu** i skopiuj klucze dostępu i identyfikator URI dla Twojej bazy danych; te wartości zostaną użyte w aplikacji rozruchu sprężyny.

   ![Azure Portal][AZ05]

## <a name="create-a-simple-spring-boot-application-with-hello-spring-initializr"></a>Utworzyć prostą aplikację Spring rozruchu z hello Spring Initializr

1. Przeglądaj zbyt<https://start.spring.io/>.

1. Określ, czy toogenerate **Maven** projektu z **Java**, wprowadź hello **grupy** i **artefaktu** nazwy aplikacji, i następnie kliknij przycisk hello zbyt**Generowanie projektu**.

   ![Opcje Initializr Basic Spring][SI01]

   > [!NOTE]
   >
   > Hello Spring Initializr używa hello **grupy** i **artefaktu** nazwy pakietu hello toocreate nazwy, na przykład: *com.example.wintiptoys*.
   >

1. Po wyświetleniu monitu, Pobierz hello ścieżka tooa projektu na komputerze lokalnym.

   ![Pobierz niestandardowy projekt Spring rozruchu][SI02]

1. Po wyodrębnieniu plików hello w systemie lokalnym, prosty aplikacji rozruchu Spring będzie gotowy do edycji.

   ![Pliki projektu rozruchu Spring niestandardowe][SI03]

## <a name="configure-your-spring-boot-app-toouse-hello-azure-spring-boot-starter"></a>Konfigurowanie programu rozruchowego Spring aplikacji toouse hello początkowego rozruchu Spring Azure

1. Zlokalizuj hello *pom.xml* pliku w katalogu hello aplikacji; na przykład:

   `C:\SpringBoot\wingtiptoys\pom.xml`

   — lub —

   `/users/example/home/wingtiptoys/pom.xml`

   ![Zlokalizuj plik pom.xml hello][PM01]

1. Otwórz hello *pom.xml* plik w edytorze tekstu, a następnie dodaj powitania po toolist wierszy z `<dependencies>`:

   ```xml
   <dependency>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-documentdb-spring-boot-starter</artifactId>
      <version>0.1.4</version>
   </dependency>
   ```

   ![Edytowanie pliku pom.xml hello][PM02]

1. Zapisz i zamknij hello *pom.xml* pliku.

## <a name="configure-your-spring-boot-app-toouse-your-azure-cosmos-db"></a>Konfigurowanie programu rozruchowego Spring toouse aplikacji bazy danych programu Azure rozwiązania Cosmos

1. Zlokalizuj hello *application.properties* pliku w hello *zasobów* katalogu aplikacji, np.:

   `C:\SpringBoot\wingtiptoys\src\main\resources\application.properties`

   — lub —

   `/users/example/home/wingtiptoys/src/main/resources/application.properties`

   ![Znajdź plik application.properties hello][RE01]

1. Otwórz hello *application.properties* plik w edytorze tekstów i Dodaj poniższe wiersze toohello plik hello i Zamień hello przykładowe wartości hello odpowiednie właściwości bazy danych:

   ```yaml
   # Specify hello DNS URI of your Azure Cosmos DB.
   azure.documentdb.uri=https://wingtiptoys.documents.azure.com:443/

   # Specify hello access key for your database.
   azure.documentdb.key=57686f6120447564652c20426f6220526f636b73==

   # Specify hello name of your database.
   azure.documentdb.database=wingtiptoysdata
   ```

   ![Edytowanie pliku application.properties hello][RE02]

1. Zapisz i zamknij hello *application.properties* pliku.

## <a name="add-sample-code-tooimplement-basic-database-functionality"></a>Dodawanie funkcji podstawowych bazy danych tooimplement kod przykładowy

W tej sekcji utworzysz dwie klasy Java do przechowywania danych użytkownika, a następnie zmodyfikować Twojej aplikacji głównej klasy toocreate wystąpienia klasy użytkownika hello i zapisać go tooyour bazy danych.

### <a name="define-a-basic-class-for-storing-user-data"></a>Definiowanie podstawowe klasy do przechowywania danych użytkownika

1. Utwórz nowy plik o nazwie *User.java* hello — w tym samym katalogu co plik głównej aplikacji Java.

1. Otwórz hello *User.java* plik w edytorze tekstów i dodaj następujące hello linii toodefine pliku toohello klasy rodzajowe użytkownika, która przechowuje i pobrać wartości w bazie danych:

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

1. Zapisz i zamknij hello *User.java* pliku.

### <a name="define-a-data-repository-interface"></a>Zdefiniuj interfejs repozytorium danych

1. Utwórz nowy plik o nazwie *UserRepository.java* hello — w tym samym katalogu co plik głównej aplikacji Java.

1. Otwórz hello *UserRepository.java* plik w edytorze tekstów i dodaj następujące hello linii toodefine pliku toohello repozytorium interfejs, który rozszerza interfejs repozytorium usługi DocumentDB domyślny hello:

   ```java
   package com.example.wingtiptoys;

   import com.microsoft.azure.spring.data.documentdb.repository.DocumentDbRepository;
   import org.springframework.stereotype.Repository;

   @Repository
   public interface UserRepository extends DocumentDbRepository<User, String> {}   
   ```

1. Zapisz i zamknij hello *UserRepository.java* pliku.

### <a name="modify-hello-main-application-class"></a>Modyfikowanie klasy głównym aplikacji hello

1. Zlokalizuj plik Java głównej aplikacji hello w katalogu pakietów hello aplikacji; na przykład:

   `C:\SpringBoot\wingtiptoys\src\main\java\com\example\wingtiptoys\WingtiptoysApplication.java`

   — lub —

   `/users/example/home/wingtiptoys/src/main/java/com/example/wingtiptoys/WingtiptoysApplication.java`

   ![Zlokalizuj plik Java aplikacji hello][JV01]

1. Otwórz plik Java głównej aplikacji hello w edytorze tekstów, a następnie dodaj poniższe wiersze toohello plik hello:

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

1. Zapisz i zamknij plik Java głównej aplikacji hello.

## <a name="build-and-test-your-app"></a>Tworzenie i testowanie aplikacji

1. Otwórz wiersz polecenia i zmień folder katalogu toohello gdy Twoje *pom.xml* znajduje się plik, na przykład:

   `cd C:\SpringBoot\wingtiptoys`

   — lub —

   `cd /users/example/home/wingtiptoys`

1. Tworzenie aplikacji Spring rozruchu z Maven i uruchamianie na przykład:

   ```shell
   mvn package
   java -jar target/wingtiptoys-0.0.1-SNAPSHOT.jar
   ```

1. Aplikacja wyświetli komunikaty środowiska uruchomieniowego i powinna zostać wyświetlona wiadomość hello `User: testFirstName testLastName` wyświetlane tooindicate, że wartości zostały pomyślnie przechowywane i pobierane z bazy danych.

   ![Pomyślne dane wyjściowe aplikacji hello][JV02]

1. OPCJONALNIE: Można hello Azure tooview portalu hello zawartość Twojego rozwiązania Cosmos bazy danych Azure na stronie właściwości hello bazy danych, klikając **Eksploratora dokumentów**i wybierając element i z hello wyświetlana lista tooview hello zawartość.

   ![Przy użyciu tooview Eksploratora dokumentów hello danych][JV03]

## <a name="next-steps"></a>Następne kroki

Aby uzyskać więcej informacji na temat korzystania z bazy danych Azure rozwiązania Cosmos i Java zobacz następujące artykuły hello:

* [Dokumentacja rozwiązania Cosmos Azure DB].

* [Azure DB rozwiązania Cosmos: Tworzenie aplikacji interfejsu API usługi DocumentDB z językiem Java i hello portalu Azure][Build a DocumentDB API app with Java]

Aby uzyskać więcej informacji o używaniu aplikacji rozruchu Spring na platformie Azure zobacz następujące artykuły hello:

* [Spring rozruchu DocumenDB początkowy dla platformy Azure](https://github.com/Microsoft/azure-spring-boot-starters/tree/master/azure-documentdb-spring-boot-starter-sample)

* [Wdrażanie aplikacji rozruchu Spring toohello usłudze Azure App Service](../app-service/app-service-deploy-spring-boot-web-app-on-azure.md)

* [Działającej aplikacja rozruchu Spring w klastrze Kubernetes w hello usługi kontenera platformy Azure](../container-service/container-service-deploy-spring-boot-app-on-kubernetes.md)

Aby uzyskać więcej informacji o korzystaniu z językiem Java Azure, zobacz hello [Azure Java Developer Center] i hello [Java Tools for Visual Studio Team Services].

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
