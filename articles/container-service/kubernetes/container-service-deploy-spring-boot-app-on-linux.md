---
title: "aaaDeploy aplikacji sieci Web Spring rozruchu w systemie Linux w usłudze kontenera platformy Azure | Dokumentacja firmy Microsoft"
description: Ten samouczek przedstawia jednak hello kroki toodeploy aplikacja rozruchu Spring jako aplikacji sieci web systemu Linux w systemie Microsoft Azure.
services: container-service
documentationcenter: java
author: rmcmurray
manager: cfowler
editor: 
ms.assetid: 
ms.service: container-service
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 08/04/2017
ms.author: asirveda;robmcm
ms.custom: mvc
ms.openlocfilehash: 2c44be1c7f66a38f48239001f0be9e90c7e6edef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-spring-boot-application-on-linux-in-hello-azure-container-service"></a>Wdrażanie aplikacji Spring rozruchu w systemie Linux w hello usługi kontenera platformy Azure

Witaj ** [Spring Framework] ** to rozwiązanie open source, które pomaga deweloperom języka Java, tworzenie aplikacji na poziomie przedsiębiorstwa. Jednego z projektów innych popularnych hello, które jest wbudowane znajdujący się na platformie jest [rozruchu Spring], zapewniające uproszczone podejście do tworzenia aplikacji Java autonomicznych.

**[Docker] ** jest rozwiązania open source, które pomaga deweloperom automatyzację wdrażania hello, skalowania i zarządzania ich aplikacji, które są uruchomione w kontenerach.

Ten samouczek przeprowadzi Cię przez kolejne przy użyciu Docker toodevelop i wdrażanie rozruchu Spring aplikacji tooa hoście z systemem Linux w hello [usługi kontenera platformy Azure (ACS)].

## <a name="prerequisites"></a>Wymagania wstępne

Kolejność toocomplete hello kroki w tym samouczku potrzebne hello toohave następujące wymagania wstępne:

* Subskrypcja platformy Azure; Jeśli nie masz jeszcze subskrypcji platformy Azure, możesz przeprowadzić aktywację Twojej [korzyści dla subskrybentów MSDN] lub zarejestrować się w celu [bezpłatne konto platformy Azure].
* Witaj [Azure interfejsu wiersza polecenia (CLI)].
* Aktualne [Java Developer Kit (JDK)].
* Apache na [Maven] (w wersji 3) Narzędzie kompilacji.
* A [Git] klienta.
* A [Docker] klienta.

> [!NOTE]
>
> Ze względu na wymagania dotyczące wirtualizacji toohello tego samouczka nie można wykonać hello opisanych w tym artykule na maszynie wirtualnej; należy użyć komputera fizycznego z włączonymi funkcjami wirtualizacji.
>

## <a name="create-hello-spring-boot-on-docker-getting-started-web-app"></a>Utwórz hello Spring rozruchowego na wprowadzenie Docker aplikacji sieci web

Witaj kolejnych krokach objaśniono sposób hello kroki, które są wymagane toocreate prostą aplikację sieci web Spring rozruchu i przetestować go lokalnie.

1. Otwórz wiersz polecenia i utworzyć toohold lokalnego katalogu aplikacji i zmień katalog toothat; na przykład:
   ```
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   --lub--
   ```
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. Witaj w klonowania [rozruchu Spring na wprowadzenie Docker] przykładowy projekt do katalogu hello utworzony; na przykład:
   ```
   git clone https://github.com/spring-guides/gs-spring-boot-docker.git
   ```

1. Zmień katalog projektu toohello ukończone; na przykład:
   ```
   cd gs-spring-boot-docker/complete
   ```

1. Kompiluj plik JAR hello za pomocą programu Maven; na przykład:
   ```
   mvn package
   ```

1. Po utworzeniu aplikacji sieci web hello zmienić katalogu toohello `target` katalog w którym plik JAR hello znajduje się uruchomić aplikacji sieci web hello; na przykład:
   ```
   cd target
   java -jar gs-spring-boot-docker-0.1.0.jar
   ```

1. Testowanie aplikacji sieci web hello przechodząc tooit lokalnie za pomocą przeglądarki sieci web. Na przykład jeśli masz curl dostępny i skonfigurowany toorun serwera Tomcat hello na porcie 80:
   ```
   curl http://localhost
   ```

1. Powinien zostać wyświetlony komunikat wyświetlany po hello: **Hello Docker World!**

   ![Przejdź do przykładowej aplikacji lokalnie][SB01]

## <a name="create-an-azure-container-registry-toouse-as-a-private-docker-registry"></a>Utwórz toouse rejestru kontenera Azure jako prywatnych rejestru Docker

Witaj kolejnych krokach objaśniono sposób przy użyciu hello Azure toocreate portalu rejestru kontenera platformy Azure.

> [!NOTE]
>
> Toouse hello Azure CLI zamiast hello portalu Azure, należy wykonać kroki hello [tworzenie prywatnych rejestru kontenera Docker przy użyciu hello Azure CLI 2.0](../../container-registry/container-registry-get-started-azure-cli.md).
>

1. Przeglądaj toohello [portalu Azure] i zaloguj się.

   Po zalogowaniu się na koncie tooyour na powitania portalu Azure, można wykonać kroki hello w hello [tworzenie prywatnych rejestru kontenera Docker przy użyciu portalu Azure hello] artykułu, które są paraphrased w hello następujące kroki dla hello zapewnienia praktycznych.

1. Kliknij ikonę menu hello **+ nowy**, następnie kliknij przycisk **kontenery**, a następnie kliknij przycisk **rejestru kontenera Azure**.
   
   ![Tworzenie nowego rejestru kontenera platformy Azure][AR01]

1. Gdy zostanie wyświetlona strona informacji hello hello rejestru kontenera Azure szablonu, kliknij przycisk **Utwórz**. 

   ![Tworzenie nowego rejestru kontenera platformy Azure][AR02]

1. Gdy hello **Utwórz kontener rejestru** zostanie wyświetlona strona, wprowadź użytkownika **nazwa rejestru** i **grupy zasobów**, wybierz **włączyć** dla Witaj **administrator**, a następnie kliknij przycisk **Utwórz**.

   ![Konfigurowanie ustawień rejestru kontenera platformy Azure][AR03]

1. Po utworzeniu kontenera rejestru przejdź do klucza rejestru kontenera tooyour hello portalu Azure, a następnie kliknij **klucze dostępu**. Zwróć uwagę na powitania nazwę użytkownika i hasło hello następnych kroków.

   ![Klawisze dostępu rejestru kontenera platformy Azure][AR04]

## <a name="configure-maven-toouse-your-azure-container-registry-access-keys"></a>Skonfiguruj Maven toouse klucze dostępu do rejestru kontenera platformy Azure

1. Przejdź do katalogu konfiguracji toohello instalacji Maven i otwórz hello *settings.xml* plik w edytorze tekstów.

1. Dodaj ustawienia dostępu do rejestru kontenera Azure hello w poprzedniej sekcji tego samouczka toohello `<servers>` kolekcji w hello *settings.xml* pliku; na przykład:

   ```xml
   <servers>
      <server>
         <id>wingtiptoysregistry</id>
         <username>wingtiptoysregistry</username>
         <password>AbCdEfGhIjKlMnOpQrStUvWxYz</password>
      </server>
   </servers>
   ```

1. Przejdź do katalogu projektu ukończona toohello aplikacji Spring rozruchu, (na przykład: "*C:\SpringBoot\gs-spring-boot-docker\complete*"lub"*/users/robert/SpringBoot/gs-spring-boot-docker / pełne*") i otwórz hello *pom.xml* plik w edytorze tekstów.

1. Aktualizacja hello `<properties>` kolekcji w hello *pom.xml* pliku z wartością serwera logowania hello rejestru kontenera platformy Azure z poprzedniej sekcji hello tego samouczka; na przykład:

   ```xml
   <properties>
      <docker.image.prefix>wingtiptoysregistry.azurecr.io</docker.image.prefix>
      <java.version>1.8</java.version>
   </properties>
   ```

1. Aktualizacja hello `<plugins>` kolekcji w hello *pom.xml* pliku, który hello `<plugin>` zawiera powitania serwera adres i rejestru nazwę logowania dla rejestr kontenera platformy Azure z poprzedniej sekcji hello tego samouczka. Na przykład:

   ```xml
   <plugin>
      <groupId>com.spotify</groupId>
      <artifactId>docker-maven-plugin</artifactId>
      <version>0.4.11</version>
      <configuration>
         <imageName>${docker.image.prefix}/${project.artifactId}</imageName>
         <dockerDirectory>src/main/docker</dockerDirectory>
         <resources>
            <resource>
               <targetPath>/</targetPath>
               <directory>${project.build.directory}</directory>
               <include>${project.build.finalName}.jar</include>
            </resource>
         </resources>
         <serverId>wingtiptoysregistry</serverId>
         <registryUrl>https://wingtiptoysregistry.azurecr.io</registryUrl>
      </configuration>
   </plugin>
   ```

1. Przejdź do katalogu projektu toohello ukończone aplikacji Spring rozruchu i uruchom następujące polecenie toorebuild hello aplikacji hello i push hello kontenera tooyour rejestru kontenera Azure:

   ```
   mvn package docker:build -DpushImage 
   ```

> [!NOTE]
>
> Gdy push Twojej tooAzure kontenera Docker może zostać wyświetlony komunikat o błędzie jest podobny tooone hello następujących, mimo że pomyślnie utworzono kontener programu Docker:
>
> * `[ERROR] Failed tooexecute goal com.spotify:docker-maven-plugin:0.4.11:build (default-cli) on project gs-spring-boot-docker: Exception caught: no basic auth credentials`
>
> * `[ERROR] Failed tooexecute goal com.spotify:docker-maven-plugin:0.4.11:build (default-cli) on project gs-spring-boot-docker: Exception caught: Incomplete Docker registry authorization credentials. Please provide all of username, password, and email or none.`
>
> W takiej sytuacji może być konieczne toosign w tooyour konto platformy Azure z wiersza polecenia Docker hello; na przykład:
>
> `docker login -u wingtiptoysregistry -p "AbCdEfGhIjKlMnOpQrStUvWxYz" wingtiptoysregistry.azurecr.io`
>
> Następnie możesz wypchnąć z kontenera z wiersza polecenia hello; na przykład:
>
> `docker push wingtiptoysregistry.azurecr.io/gs-spring-boot-docker`
>

## <a name="create-a-web-app-on-linux-on-azure-app-service-using-your-container-image"></a>Tworzenie aplikacji sieci web w systemie Linux w usłudze Azure App Service przy użyciu obrazu kontenera

1. Przeglądaj toohello [portalu Azure] i zaloguj się.

1. Kliknij ikonę menu hello **+ nowy**, następnie kliknij przycisk **sieci Web i mobilność**, a następnie kliknij przycisk **aplikacji sieci Web w systemie Linux**.
   
   ![Utwórz nową aplikację sieci web w portalu Azure hello][LX01]

1. Gdy hello **aplikacji sieci Web w systemie Linux** zostanie wyświetlona strona, wprowadź hello następujących informacji:

   a. Wprowadź unikatową nazwę hello **Nazwa aplikacji**, na przykład: "*wingtiptoyslinux*."

   b. Wybierz użytkownika **subskrypcji** z listy rozwijanej hello.

   c. Wybierz istniejące **grupy zasobów**, lub określ toocreate nazwę nowej grupy zasobów.

   d. Kliknij przycisk **kontenera konfiguracji** , a następnie wprowadź hello następujących informacji:

      * Wybierz **prywatnej rejestru**.

      * **Obraz i opcjonalnie tag**: Określ nazwę kontenera z wcześniej, na przykład: "*wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest*"

      * **Adres URL serwera**: Określ adres URL rejestru z wcześniej, na przykład: "*https://wingtiptoysregistry.azurecr.io*"

      * **Nazwa użytkownika logowania** i **hasło**: Określ poświadczenia logowania z użytkownika **klucze dostępu** używanego w poprzednich krokach.
   
   e. Po wprowadzeniu wszystkich hello powyżej informacji, kliknij przycisk **OK**.

   ![Konfiguruj ustawienia aplikacji sieci web][LX02]

1. Kliknij przycisk **Utwórz**.

> [!NOTE]
>
> Azure automatycznie przypisze Internet żądań tooembedded Tomcat serwera, który działa na standardowe porty hello 80 lub 8080. Jednak z osadzonych toorun serwer Tomcat jest skonfigurowany na port niestandardowy, należy najpierw tooadd aplikacji sieci web tooyour zmiennej środowiska, który definiuje hello port serwera Tomcat osadzonych. toodo tak, użycie hello następujące kroki:
>
> 1. Przeglądaj toohello [portalu Azure] i zaloguj się.
> 
> 2. Kliknij ikonę hello **usługi aplikacji**. (Zobacz poniższy obraz powitania element #1).
>
> 3. Wybierz aplikację sieci web z listy hello. (Element #2 na poniższym obrazie hello.)
>
> 4. Kliknij przycisk **ustawienia aplikacji**. (Element #3 na poniższym obrazie hello.)
>
> 5. W hello **ustawień aplikacji** Dodaj nową zmienną środowiskową o nazwie **portu** i wprowadź numer portu niestandardowego hello wartości. (Element #4 hello obraz poniżej.)
>
> 6. Kliknij pozycję **Zapisz**. (Element #5 na poniższym obrazie hello.)
>
> ![Zapisywanie niestandardowy numer portu w hello portalu Azure][LX03]
>

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

Aby uzyskać więcej informacji o używaniu aplikacji rozruchu Spring na platformie Azure zobacz następujące artykuły hello:

* [Wdrażanie aplikacji rozruchu Spring toohello usłudze Azure App Service](../../app-service/app-service-deploy-spring-boot-web-app-on-azure.md)
* [Wdrażanie aplikacji rozruchu Spring w klastrze Kubernetes w hello usługi kontenera platformy Azure](container-service-deploy-spring-boot-app-on-kubernetes.md)

Aby uzyskać więcej informacji o korzystaniu z językiem Java Azure, zobacz hello [Azure Java Developer Center] i hello [Java Tools for Visual Studio Team Services].

Aby uzyskać dalsze informacje na temat hello Spring rozruchowego na Docker przykładowy projekt, zobacz [rozruchu Spring na wprowadzenie Docker].

Aby uzyskać pomoc dotyczącą Rozpoczynanie pracy z aplikacjami Spring rozruchu, zobacz hello **Spring Initializr** na https://start.spring.io/.

Aby uzyskać więcej informacji na temat rozpoczynania pracy z tworzenia prostej aplikacji Spring rozruchu Zobacz hello Spring Initializr na https://start.spring.io/.

Aby uzyskać dodatkowe przykłady sposobu toouse Docker niestandardowe obrazy z platformy Azure, zobacz [dla aplikacji sieci Web platformy Azure w systemie Linux przy użyciu niestandardowego obrazu Docker].

<!-- URL List -->

[Azure interfejsu wiersza polecenia (CLI)]: /cli/azure/overview
[Usługa kontenera platformy Azure (ACS)]: https://azure.microsoft.com/services/container-service/
[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/
[Witryna Azure Portal]: https://portal.azure.com/
[Utwórz prywatne rejestru kontenera Docker przy użyciu hello portalu Azure]: /azure/container-registry/container-registry-get-started-portal
[Przy użyciu niestandardowego obrazu Docker dla aplikacji sieci Web platformy Azure w systemie Linux]: /azure/app-service-web/app-service-linux-using-custom-docker-image
[Docker]: https://www.docker.com/
[bezpłatne konto platformy Azure]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Narzędzia języka Java dla programu Visual Studio Team Services]: https://java.visualstudio.com/
[Maven]: http://maven.apache.org/
[Korzyści dla subskrybentów MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Spring rozruchu]: http://projects.spring.io/spring-boot/
[Spring rozruchowego na wprowadzenie Docker]: https://github.com/spring-guides/gs-spring-boot-docker
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[SB01]: ./media/container-service-deploy-spring-boot-app-on-linux/SB01.png
[SB02]: ./media/container-service-deploy-spring-boot-app-on-linux/SB02.png

[AR01]: ./media/container-service-deploy-spring-boot-app-on-linux/AR01.png
[AR02]: ./media/container-service-deploy-spring-boot-app-on-linux/AR02.png
[AR03]: ./media/container-service-deploy-spring-boot-app-on-linux/AR03.png
[AR04]: ./media/container-service-deploy-spring-boot-app-on-linux/AR04.png

[LX01]: ./media/container-service-deploy-spring-boot-app-on-linux/LX01.png
[LX02]: ./media/container-service-deploy-spring-boot-app-on-linux/LX02.png
[LX03]: ./media/container-service-deploy-spring-boot-app-on-linux/LX03.png
