---
title: Witaj toouse aaaHow Maven wtyczki dla aplikacji sieci Web Azure toodeploy tooAzure aplikacji Spring rozruchu
description: "Dowiedz się, jak toouse hello wtyczki Maven dla aplikacji sieci Web Azure toodeploy tooAzure aplikacji Spring rozruchu."
services: app-service\web
documentationcenter: java
author: rmcmurray
manager: cfowler
editor: 
ms.assetid: 
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: article
ms.date: 08/07/2017
ms.author: robmcm;kevinzha
ms.openlocfilehash: 376fe90fe20621e15d7c9856214937c78b66026a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-maven-plugin-for-azure-web-apps-toodeploy-a-spring-boot-app-tooazure"></a>Jak toouse hello wtyczki Maven dla aplikacji sieci Web Azure toodeploy tooAzure aplikacji Spring rozruchu

Witaj [Maven wtyczki dla aplikacji sieci Web Azure](https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin) dla [Apache Maven](http://maven.apache.org/) zapewnia bezproblemową integrację usługi Azure App Service w projekty Maven oraz usprawnia proces powitania dla aplikacji sieci web do deweloperzy toodeploy tooAzure usługi aplikacji.

W tym artykule przedstawiono przy użyciu hello Maven wtyczki dla aplikacji sieci Web Azure toodeploy próbki tooAzure aplikacji rozruchu Spring usługi aplikacji.

> [!NOTE]
>
> Witaj Maven wtyczki dla aplikacji sieci Web platformy Azure jest obecnie dostępna jako podgląd. Obecnie jest obsługiwana tylko publikacji FTP, chociaż hello przyszłości planowane dodatkowe funkcje.
>

## <a name="prerequisites"></a>Wymagania wstępne

Kolejność toocomplete hello kroki w tym samouczku potrzebne hello toohave następujące wymagania wstępne:

* Subskrypcja platformy Azure; Jeśli nie masz jeszcze subskrypcji platformy Azure, możesz przeprowadzić aktywację Twojej [korzyści dla subskrybentów MSDN] lub zarejestrować się w celu [bezpłatne konto platformy Azure].
* Witaj [Azure interfejsu wiersza polecenia (CLI)].
* Aktualne [Java Development Kit (JDK)], wersja 1.7 lub nowszej.
* Apache na [Maven] (w wersji 3) Narzędzie kompilacji.
* A [Git] klienta.

## <a name="clone-hello-sample-spring-boot-web-app"></a>Witaj klonowania Spring rozruchu przykładową aplikację sieci web

W tej sekcji sklonować ukończona aplikacja Spring rozruchu i przetestować go lokalnie.

1. Otwórz wiersz polecenia lub okno terminalu i utworzyć toohold lokalnego katalogu aplikacji Spring rozruchu i zmień katalog toothat; na przykład:
   ```shell
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   --lub--
   ```shell
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. Witaj w klonowania [Spring wprowadzenie rozruchu] przykładowy projekt do katalogu hello utworzony; na przykład:
   ```shell
   git clone https://github.com/microsoft/gs-spring-boot
   ```

1. Zmień katalog projektu toohello ukończone; na przykład:
   ```shell
   cd gs-spring-boot/complete
   ```

1. Kompiluj plik JAR hello za pomocą programu Maven; na przykład:
   ```shell
   mvn clean package
   ```

1. Podczas tworzenia aplikacji sieci web hello uruchomić aplikacji sieci web hello za pomocą programu Maven; na przykład:
   ```shell
   mvn spring-boot:run
   ```

1. Testowanie aplikacji sieci web hello przechodząc tooit lokalnie za pomocą przeglądarki sieci web. Na przykład można użyć hello następujące polecenie, jeśli masz curl dostępne:
   ```shell
   curl http://localhost:8080
   ```

1. Powinien zostać wyświetlony komunikat wyświetlany po hello: **pozdrowienia z Spring rozruchowe!**

## <a name="create-an-azure-service-principal"></a>Tworzenie nazwy głównej usługi platformy Azure

W tej sekcji utworzysz Azure nazwy głównej usługi, który używa wtyczki Maven Witaj, wdrażając tooAzure aplikacji sieci web.

1. Otwórz wiersz polecenia.

1. Zaloguj się do konta platformy Azure przy użyciu hello wiersza polecenia platformy Azure:
   ```shell
   az login
   ```
   Wykonaj hello instrukcje toocomplete hello procesu logowania.

1. Tworzenie nazwy głównej usługi platformy Azure:
   ```shell
   az ad sp create-for-rbac --name "uuuuuuuu" --password "pppppppp"
   ```
   Gdzie `uuuuuuuu` jest nazwą użytkownika hello i `pppppppp` jest hello hasło dla nazwy głównej usługi hello.

1. Azure odpowiada JSON podobny hello poniższy przykład:
   ```json
   {
      "appId": "aaaaaaaa-aaaa-aaaa-aaaa-aaaaaaaaaaaa",
      "displayName": "uuuuuuuu",
      "name": "http://uuuuuuuu",
      "password": "pppppppp",
      "tenant": "tttttttt-tttt-tttt-tttt-tttttttttttt"
   }
   ```

   > [!NOTE]
   >
   > Po skonfigurowaniu hello Maven wtyczki toodeploy tooAzure aplikacji sieci web, użyje hello wartości z tej odpowiedzi JSON. Hello `aaaaaaaa`, `uuuuuuuu`, `pppppppp`, i `tttttttt` są symbole zastępcze, które są używane w tej toomake przykład go łatwiejsze toomap tych wartości tootheir odpowiednich elementów podczas konfigurowania programu Maven `settings.xml` w hello obok pliku sekcja.
   >
   >

## <a name="configure-maven-toouse-your-azure-service-principal"></a>Skonfiguruj Maven toouse Twojej nazwy głównej usługi Azure

W tej sekcji można użyć wartości hello z uwierzytelniania hello tooconfigure główną usługi Azure używającej Maven, wdrażając tooAzure aplikacji sieci web.

1. Otwieranie programu Maven `settings.xml` plik w edytorze tekstów; ten plik może być w ścieżce, takie jak hello następujące przykłady:
   * `/etc/maven/settings.xml`
   * `%ProgramFiles%\apache-maven\3.5.0\conf\settings.xml`
   * `$HOME/.m2/settings.xml`

1. Dodaj ustawienia głównych usług Azure hello w poprzedniej sekcji tego samouczka toohello `<servers>` kolekcji w hello *settings.xml* pliku; na przykład:

   ```xml
   <servers>
      <server>
        <id>azure-auth</id>
         <configuration>
            <client>aaaaaaaa-aaaa-aaaa-aaaa-aaaaaaaaaaaa</client>
            <tenant>tttttttt-tttt-tttt-tttt-tttttttttttt</tenant>
            <key>pppppppp</key>
            <environment>AZURE</environment>
         </configuration>
      </server>
   </servers>
   ```
   Gdzie:
   Element | Opis
   ---|---|---
   `<id>` | Określa unikatową nazwę używający Maven toolook zapasową ustawień zabezpieczeń podczas wdrażania tooAzure aplikacji sieci web.
   `<client>` | Zawiera hello `appId` wartość z Twojej nazwy głównej usługi.
   `<tenant>` | Zawiera hello `tenant` wartość z Twojej nazwy głównej usługi.
   `<key>` | Zawiera hello `password` wartość z Twojej nazwy głównej usługi.
   `<environment>` | Definiuje hello docelowej chmury Azure środowisko, które jest `AZURE` w tym przykładzie. (Pełna lista środowisk jest dostępna w hello [Maven wtyczki dla aplikacji sieci Web Azure] dokumentacji)

1. Zapisz i zamknij hello *settings.xml* pliku.

## <a name="optional-customize-your-pomxml-before-deploying-your-web-app-tooazure"></a>OPCJONALNIE: Dostosowywanie programu pom.xml przed wdrożeniem tooAzure aplikacji sieci web

Otwórz hello `pom.xml` pliku aplikacji Spring rozruchu w edytorze tekstu, a następnie zlokalizuj hello `<plugin>` elementu `azure-webapp-maven-plugin`. Ten element powinien wyglądać hello poniższy przykład:

   ```xml
   <plugin>
      <groupId>com.microsoft.azure</groupId>
      <artifactId>azure-webapp-maven-plugin</artifactId>
      <version>0.1.3</version>
      <configuration>
         <authentication>
            <serverId>azure-auth</serverId>
         </authentication>
         <resourceGroup>maven-plugin</resourceGroup>
         <appName>maven-web-app-${maven.build.timestamp}</appName>
         <region>westus</region>
         <javaVersion>1.8</javaVersion>
         <deploymentType>ftp</deploymentType>
         <resources>
            <resource>
               <directory>${project.basedir}/target</directory>
               <targetPath>/</targetPath>
               <includes>
                  <include>*.jar</include>
               </includes>
            </resource>
            <resource>
               <directory>${project.basedir}</directory>
               <targetPath>/</targetPath>
               <includes>
                  <include>web.config</include>
               </includes>
            </resource>
         </resources>
      </configuration>
   </plugin>
   ```

Istnieje kilka wartości, które można modyfikować dla wtyczki Maven hello i szczegółowy opis każdego z tych elementów jest dostępna w hello [Maven wtyczki dla aplikacji sieci Web Azure] dokumentacji. Który trwa wspomniano, istnieje kilka wartości, które warto wyróżnianie w tym artykule:

Element | Opis
---|---|---
`<version>` | Określa wersję hello hello [Maven wtyczki dla aplikacji sieci Web Azure]. Należy sprawdzić wersji hello na liście hello [Maven centralnym repozytorium](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22) tooensure, którego używasz hello najnowszej wersji.
`<authentication>` | Określa hello informacje dotyczące uwierzytelniania dla platformy Azure, który w tym przykładzie zawiera `<serverId>` element, który zawiera `azure-auth`; Maven używa tej wartości toolook wartości podmiotu zabezpieczeń usługi Azure hello programu Maven *settings.xml* pliku, który został zdefiniowany w wcześniejszej części tego artykułu.
`<resourceGroup>` | Określa, docelowa grupa zasobów hello, który jest `maven-plugin` w tym przykładzie. Grupa zasobów Hello jest tworzona podczas wdrażania, jeśli jeszcze nie istnieje.
`<appName>` | Określa nazwę docelowej hello aplikacji sieci web. W tym przykładzie nazwa docelowego hello jest `maven-web-app-${maven.build.timestamp}`, gdzie hello `${maven.build.timestamp}` jest do niej dołączany sufiks w tej konflikt tooavoid przykład. (sygnatura czasowa hello jest opcjonalne; można określić dowolny unikatowy ciąg dla nazwy aplikacji hello).
`<region>` | Określa region docelowy hello, czyli w tym przykładzie `westus`. (Pełna lista jest w hello [Maven wtyczki dla aplikacji sieci Web Azure] dokumentacji.)
`<javaVersion>` | Określa wersję środowiska uruchomieniowego języka Java powitania dla aplikacji sieci web. (Pełna lista jest w hello [Maven wtyczki dla aplikacji sieci Web Azure] dokumentacji.)
`<deploymentType>` | Określa typ wdrożenia dla aplikacji sieci web. Obecnie tylko `ftp` jest obsługiwana, chociaż obsługuje inne typy wdrożenia jest programowanie.
`<resources>` | Określa zasobów i docelowy miejsc docelowych, które Maven używa podczas wdrażania tooAzure aplikacji sieci web. W tym przykładzie dwa `<resource>` elementy Określ, czy Maven wdroży hello plik JAR dla aplikacji sieci web i hello *web.config* pliku z hello rozruchu Spring projektu.

## <a name="build-and-deploy-your-web-app-tooazure"></a>Tworzenie i wdrażanie tooAzure aplikacji sieci web

Po skonfigurowaniu wszystkich ustawień hello w hello powyższej sekcji tego artykułu, są gotowe toodeploy tooAzure aplikacji sieci web. toodo tak, użycie hello następujące kroki:

1. Z wiersza polecenia hello lub okno terminalu, które były wcześniej używane odbudować plik JAR hello za pomocą programu Maven Jeśli wprowadzono żadnych zmian toohello *pom.xml* pliku; na przykład:
   ```shell
   mvn clean package
   ```

1. Wdrażanie tooAzure aplikacji sieci web przy użyciu narzędzia Maven; na przykład:
   ```shell
   mvn azure-webapp:deploy
   ```

Maven wdroży tooAzure aplikacji sieci web; Jeśli aplikacja sieci web hello jeszcze nie istnieje, zostanie utworzona.

Po wdrożeniu sieci web będą mogli toomanage go za pomocą hello [portalu Azure].

* Aplikacja sieci web zostaną wyświetlone w **usługi aplikacji**:

   ![Aplikacja sieci Web wyświetlane w portalu Azure usługi aplikacji][AP01]

* I hello adres URL dla aplikacji sieci web zostaną wyświetlone w hello **omówienie** dla aplikacji sieci web:

   ![Określanie hello adres URL aplikacji sieci web][AP02]

<!--
##  OPTIONAL: Configure hello embedded Tomcat server toorun on a different port

hello embedded Tomcat server in hello sample Spring Boot application is configured toorun on port 8080 by default. However, if you want toorun hello embedded Tomcat server toorun on a different port, such as port 80 for local testing, you can configure hello port by using hello following steps.

1. Go toohello *resources* directory (or create hello directory if it does not exist); for example:
   ```shell
   cd src/main/resources
   ```

1. Open hello *application.yml* file in a text editor if it exists, or create a new YAML file if it does not exist.

1. Modify hello **server** setting so that hello server runs on port 80; for example:
   ```yaml
   server:
      port: 80
   ```

1. Save and close hello *application.yml* file.
-->

## <a name="next-steps"></a>Następne kroki

Aby uzyskać więcej informacji na temat hello różne technologie omówione w tym artykule, zobacz hello następujące artykuły:

* [Maven wtyczki dla aplikacji sieci Web Azure]

* [Zaloguj się za tooAzure z hello wiersza polecenia platformy Azure](/azure/xplat-cli-connect)

* [Jak toouse hello wtyczki Maven dla aplikacji sieci Web Azure toodeploy konteneryzowanych tooAzure aplikacji Spring rozruchu](app-service-web-deploy-containerized-spring-boot-app-with-maven-plugin.md)

* [Tworzenie nazwy głównej usługi platformy Azure z 2.0 interfejsu wiersza polecenia platformy Azure](/cli/azure/create-an-azure-service-principal-azure-cli)

* [Informacje o ustawieniach maven](https://maven.apache.org/settings.html)

<!-- URL List -->

[Azure interfejsu wiersza polecenia (CLI)]: /cli/azure/overview
[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/
[portalu Azure]: https://portal.azure.com/
[bezpłatne konto platformy Azure]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[Maven]: http://maven.apache.org/
[korzyści dla subskrybentów MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring Boot]: http://projects.spring.io/spring-boot/
[Spring wprowadzenie rozruchu]: https://github.com/microsoft/gs-spring-boot
[Spring Framework]: https://spring.io/
[Maven wtyczki dla aplikacji sieci Web Azure]: https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin

<!-- IMG List -->

[AP01]: ./media/app-service-web-deploy-spring-boot-app-with-maven-plugin/AP01.png
[AP02]: ./media/app-service-web-deploy-spring-boot-app-with-maven-plugin/AP02.png
