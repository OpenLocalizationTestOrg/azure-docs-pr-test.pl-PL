---
title: Witaj toouse aaaHow Maven wtyczki dla aplikacji sieci Web Azure toodeploy w aplikacji Spring rozruchu w tooAzure rejestru kontenera Azure App Service
description: "Ten samouczek przeprowadzi Cię jednak hello kroki toodeploy aplikacja Spring rozruchu w tooAzure tooAzure rejestru kontenera Azure App Service przy użyciu wtyczki Maven."
services: 
documentationcenter: java
author: rmcmurray
manager: cfowler
editor: 
ms.assetid: 
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 08/07/2017
ms.author: robmcm;kevinzha
ms.openlocfilehash: 55b95e310c9ee186a6d77d941c5a620c2e259d8a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-maven-plugin-for-azure-web-apps-toodeploy-a-spring-boot-app-in-azure-container-registry-tooazure-app-service"></a>Jak toouse hello Maven wtyczki dla aplikacji sieci Web Azure toodeploy w aplikacji Spring rozruchu w tooAzure rejestru kontenera Azure App Service

Witaj  **[Spring Framework]**  popularnych struktura open source, który pomaga Java deweloperom tworzenie aplikacji interfejsu API, mobilne i sieci web. W tym samouczku używana przykładowej aplikacji utworzony za pomocą [rozruchu Spring], podejście oparte na Konwencji poświęcone Spring tooget szybko rozpocząć pracę.

W tym artykule przedstawiono sposób toodeploy próbki tooAzure aplikacji rozruchu Spring kontenera rejestru, a następnie użyć hello Maven wtyczki dla toodeploy Azure Web Apps tooAzure Twojej aplikacji usługi aplikacji.

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
* A [Docker] klienta.

> [!NOTE]
>
> Ze względu na wymagania dotyczące wirtualizacji toohello tego samouczka nie można wykonać hello opisanych w tym artykule na maszynie wirtualnej; należy użyć komputera fizycznego z włączonymi funkcjami wirtualizacji.
>

## <a name="clone-hello-sample-spring-boot-on-docker-web-app"></a>Klonowanie hello przykładu rozruchu Spring Docker aplikacji sieci web

W tej sekcji sklonować konteneryzowanych aplikacji rozruchu Spring i przetestować go lokalnie.

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

1. Witaj w klonowania [rozruchu Spring na wprowadzenie Docker] przykładowy projekt do katalogu hello utworzony; na przykład:
   ```shell
   git clone -b private-registry https://github.com/Microsoft/gs-spring-boot-docker
   ```

1. Zmień katalog projektu toohello ukończone; na przykład:
   ```shell
   cd gs-spring-boot-docker/complete
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

1. Powinien zostać wyświetlony komunikat wyświetlany po hello: **Hello Docker World**

   ![Przejdź do przykładowej aplikacji lokalnie][SB01]

## <a name="create-an-azure-service-principal"></a>Tworzenie nazwy głównej usługi platformy Azure

W tej sekcji utworzysz Azure nazwy głównej usługi, która hello używa wtyczki Maven, wdrażając tooAzure Twojego kontenera.

1. Otwórz wiersz polecenia.

1. Zaloguj się do konta platformy Azure przy użyciu hello wiersza polecenia platformy Azure:
   ```azurecli
   az login
   ```
   Wykonaj hello instrukcje toocomplete hello procesu logowania.

1. Tworzenie nazwy głównej usługi platformy Azure:
   ```azurecli
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
   > Po skonfigurowaniu hello Maven wtyczki toodeploy Twojego tooAzure kontenera Użyj wartości hello z odpowiedź w formacie JSON. Hello `aaaaaaaa`, `uuuuuuuu`, `pppppppp`, i `tttttttt` są symbole zastępcze, które są używane w tej toomake przykład go łatwiejsze toomap tych wartości tootheir odpowiednich elementów podczas konfigurowania programu Maven `settings.xml` w hello obok pliku sekcja.
   >
   >

## <a name="create-an-azure-container-registry-using-hello-azure-cli"></a>Tworzenie przy użyciu interfejsu wiersza polecenia Azure hello rejestru kontenera platformy Azure

1. Otwórz wiersz polecenia.

1. Zaloguj się tooyour konto platformy Azure:
   ```azurecli
   az login
   ```

1. Utwórz grupę zasobów dla hello zasobów platformy Azure, które będą używane w tym artykule:
   ```azurecli
   az group create --name=wingtiptoysresources --location=westus
   ```
   Zastąp `wingtiptoysresources` w tym przykładzie z unikatową nazwę grupy zasobów.

1. Utwórz rejestru prywatnej kontenera platformy Azure w grupie zasobów hello aplikacji Spring rozruchu: 
   ```azurecli
   az acr create --admin-enabled --resource-group wingtiptoysresources --location westus --name wingtiptoysregistry --sku Basic
   ```
   Zastąp `wingtiptoysregistry` w tym przykładzie z unikatową nazwę rejestru kontenera.

1. Pobrać hasło hello rejestru kontenera:
   ```azurecli
   az acr credential show --name wingtiptoysregistry --query passwords[0]
   ```
   Azure będzie odpowiadać przy użyciu hasła; na przykład:
   ```json
   {
      "name": "password",
      "value": "xxxxxxxxxx"
   }
   ```

## <a name="add-your-azure-container-registry-and-azure-service-principal-tooyour-maven-settings"></a>Dodaj rejestru kontenera platformy Azure i ustawienia Maven tooyour główną usługi Azure

1. Otwieranie programu Maven `settings.xml` plik w edytorze tekstów; ten plik może być w ścieżce, takie jak hello następujące przykłady:
   * `/etc/maven/settings.xml`
   * `%ProgramFiles%\apache-maven\3.5.0\conf\settings.xml`
   * `$HOME/.m2/settings.xml`

1. Dodawanie ustawień dostępu do rejestru kontenera platformy Azure z poprzedniej sekcji tego artykułu toohello hello `<servers>` kolekcji w hello *settings.xml* pliku; na przykład:

   ```xml
   <servers>
      <server>
         <id>wingtiptoysregistry</id>
         <username>wingtiptoysregistry</username>
         <password>xxxxxxxxxx</password>
      </server>
   </servers>
   ```
   Gdzie:
   Element | Opis
   ---|---|---
   `<id>` | Zawiera nazwę hello rejestru prywatnej kontenera platformy Azure.
   `<username>` | Zawiera nazwę hello rejestru prywatnej kontenera platformy Azure.
   `<password>` | Zawiera hasło hello pobrany w poprzedniej sekcji hello tego artykułu.

1. Dodaj ustawienia podmiotu zabezpieczeń usługi Azure z wcześniejszej części tego artykułu toohello `<servers>` kolekcji w hello *settings.xml* pliku; na przykład:

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

## <a name="build-your-docker-container-image-and-push-it-tooyour-azure-container-registry"></a>Tworzenie obrazu kontenera programu Docker i wypchnąć go tooyour rejestru kontenera platformy Azure

1. Przejdź toohello ukończone katalogu projektu aplikacji Spring rozruchu, (np. "*C:\SpringBoot\gs-spring-boot-docker\complete*"lub"*/users/robert/SpringBoot/gs-spring-boot-docker/complete*") i otwórz hello *pom.xml* pliku z Edytor tekstu.

1. Aktualizacja hello `<properties>` kolekcji w hello *pom.xml* pliku z wartością serwera logowania hello rejestru kontenera platformy Azure z poprzedniej sekcji hello tego samouczka; na przykład:

   ```xml
   <properties>
      <azure.containerRegistry>wingtiptoysregistry</azure.containerRegistry>
      <docker.image.prefix>${azure.containerRegistry}.azurecr.io</docker.image.prefix>
      <java.version>1.8</java.version>
      <maven.build.timestamp.format>yyyyMMddHHmmssSSS</maven.build.timestamp.format>
   </properties>
   ```
   Gdzie:
   Element | Opis
   ---|---|---
   `<azure.containerRegistry>` | Określa nazwę hello rejestru prywatnej kontenera platformy Azure.
   `<docker.image.prefix>` | Określa adres URL rejestru prywatnej kontenera platformy Azure, w którym jest uzyskiwany w wyniku dołączania hello ". azurecr.io" toohello nazwa rejestru Kontener prywatny.

1. Sprawdź, czy `<plugin>` hello Docker wtyczki w Twojej *pom.xml* plik zawiera prawidłowe właściwości hello powitania serwera adres i rejestru nazwy logowania z poprzedniego kroku hello w tym samouczku. Na przykład:

   ```xml
   <plugin>
      <groupId>com.spotify</groupId>
      <artifactId>docker-maven-plugin</artifactId>
      <version>0.4.11</version>
      <configuration>
         <imageName>${docker.image.prefix}/${project.artifactId}</imageName>
         <registryUrl>https://${docker.image.prefix}</registryUrl>
         <serverId>${azure.containerRegistry}</serverId>
         <dockerDirectory>src/main/docker</dockerDirectory>
         <resources>
            <resource>
               <targetPath>/</targetPath>
               <directory>${project.build.directory}</directory>
               <include>${project.build.finalName}.jar</include>
            </resource>
         </resources>
      </configuration>
   </plugin>
   ```
   Gdzie:
   Element | Opis
   ---|---|---
   `<serverId>` | Określa właściwość hello, która zawiera nazwę rejestru prywatnej kontenera platformy Azure.
   `<registryUrl>` | Określa właściwość hello, który zawiera adres URL hello rejestru prywatnej kontenera platformy Azure.

1. Przejdź do katalogu projektu toohello ukończone aplikacji Spring rozruchu i uruchom następujące polecenie toorebuild hello aplikacji hello push hello kontenera tooyour rejestru kontenera platformy Azure:

   ```
   mvn package docker:build -DpushImage 
   ```

1. OPCJONALNIE: Przeglądaj toohello [portalu Azure] i sprawdź, czy jest obraz kontenera Docker o nazwie **gs-spring — rozruchu — docker** w rejestrze kontenera.

   ![Sprawdź kontenera w portalu Azure][CR01]

## <a name="customize-your-pomxml-then-build-and-deploy-your-container-tooazure"></a>Dostosowywanie programu pom.xml, a następnie Skompiluj i wdróż tooAzure Twojego kontenera

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
         <resourceGroup>wingtiptoysresources</resourceGroup>
         <appName>maven-linux-app-${maven.build.timestamp}</appName>
         <region>westus</region>
         <containerSettings>
            <imageName>${docker.image.prefix}/${project.artifactId}</imageName>
            <registryUrl>https://${docker.image.prefix}</registryUrl>
            <serverId>${azure.containerRegistry}</serverId>
         </containerSettings>
         <appSettings>
            <property>
               <name>PORT</name>
               <value>8080</value>
            </property>
         </appSettings>
      </configuration>
   </plugin>
   ```

Istnieje kilka wartości, które można modyfikować dla wtyczki Maven hello i szczegółowy opis każdego z tych elementów jest dostępna w hello [Maven wtyczki dla aplikacji sieci Web Azure] dokumentacji. Który trwa wspomniano, istnieje kilka wartości, które warto wyróżnianie w tym artykule:

Element | Opis
---|---|---
`<version>` | Określa wersję hello hello [Maven wtyczki dla aplikacji sieci Web Azure]. Należy sprawdzić wersji hello na liście hello [Maven centralnym repozytorium](http://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-webapp-maven-plugin%22) tooensure, którego używasz hello najnowszej wersji.
`<authentication>` | Określa hello informacje dotyczące uwierzytelniania dla platformy Azure, który w tym przykładzie zawiera `<serverId>` element, który zawiera `azure-auth`; Maven używa tej wartości toolook wartości podmiotu zabezpieczeń usługi Azure hello programu Maven *settings.xml* pliku, który został zdefiniowany w wcześniejszej części tego artykułu.
`<resourceGroup>` | Określa, docelowa grupa zasobów hello, który jest `wingtiptoysresources` w tym przykładzie. Grupa zasobów Hello zostanie utworzony podczas wdrażania, jeśli jeszcze nie istnieje.
`<appName>` | Określa nazwę docelowej hello aplikacji sieci web. W tym przykładzie nazwa docelowego hello jest `maven-linux-app-${maven.build.timestamp}`, gdzie hello `${maven.build.timestamp}` jest do niej dołączany sufiks w tej konflikt tooavoid przykład. (sygnatura czasowa hello jest opcjonalne; można określić dowolny unikatowy ciąg dla nazwy aplikacji hello).
`<region>` | Określa region docelowy hello, czyli w tym przykładzie `westus`. (Pełna lista jest w hello [Maven wtyczki dla aplikacji sieci Web Azure] dokumentacji.)
`<containerSettings>` | Określa właściwości hello, które zawierają hello nazwy i adresu URL z kontenera.
`<appSettings>` | Określa unikatowy ustawienia Maven toouse, wdrażając tooAzure aplikacji sieci web. W tym przykładzie `<property>` element zawiera pary nazwa/wartość elementów podrzędnych, określających hello portu dla aplikacji.

> [!NOTE]
>
> numer portu Hello ustawienia toochange hello w tym przykładzie jest konieczne tylko w przypadku, gdy zmieniasz hello portów z domyślnej hello.
>

1. Z wiersza polecenia hello lub okno terminalu, które były wcześniej używane odbudować plik JAR hello za pomocą programu Maven Jeśli wprowadzono żadnych zmian toohello *pom.xml* pliku; na przykład:
   ```shell
   mvn clean package
   ```

1. Wdrażanie tooAzure aplikacji sieci web przy użyciu narzędzia Maven; na przykład:
   ```shell
   mvn azure-webapp:deploy
   ```

Maven wdroży tooAzure aplikacji sieci web; Jeśli aplikacja sieci web hello jeszcze nie istnieje, zostanie utworzona.

> [!NOTE]
>
> Jeśli region hello, określany w hello `<region>` elementu z *pom.xml* plik nie ma wystarczającej liczby serwerów, które są dostępne po uruchomieniu wdrożenia, można napotkać błąd toohello podobnie poniższy przykład:
>
> ```
> [INFO] Start deploying tooWeb App maven-linux-app-20170804...
> [INFO] ------------------------------------------------------------------------
> [INFO] BUILD FAILURE
> [INFO] ------------------------------------------------------------------------
> [INFO] Total time: 31.059 s
> [INFO] Finished at: 2017-08-04T12:15:47-07:00
> [INFO] Final Memory: 51M/279M
> [INFO] ------------------------------------------------------------------------
> [ERROR] Failed tooexecute goal com.microsoft.azure:azure-webapp-maven-plugin:0.1.3:deploy (default-cli) on project gs-spring-boot-docker: null: MojoExecutionException: CloudException: OnError while emitting onNext value: retrofit2.Response.class
> ```
>
> W takim przypadku można określić innego regionu i uruchom ponownie hello toodeploy polecenie narzędzia Maven aplikacji.
>
>

Po wdrożeniu sieci web będą mogli toomanage go za pomocą hello [portalu Azure].

* Aplikacja sieci web zostaną wyświetlone w **usługi aplikacji**:

   ![Aplikacja sieci Web wyświetlane w portalu Azure usługi aplikacji][AP01]

* I hello adres URL dla aplikacji sieci web zostaną wyświetlone w hello **omówienie** dla aplikacji sieci web:

   ![Określanie hello adres URL aplikacji sieci web][AP02]

## <a name="next-steps"></a>Następne kroki

Aby uzyskać więcej informacji na temat hello różne technologie omówione w tym artykule, zobacz hello następujące artykuły:

* [Maven wtyczki dla aplikacji sieci Web Azure]

* [Zaloguj się za tooAzure z hello wiersza polecenia platformy Azure](/azure/xplat-cli-connect)

* [Tworzenie nazwy głównej usługi platformy Azure z 2.0 interfejsu wiersza polecenia platformy Azure](/cli/azure/create-an-azure-service-principal-azure-cli)

* [Informacje o ustawieniach maven](https://maven.apache.org/settings.html)

* [Dodatek docker przypadku Maven]

<!-- URL List -->

[Azure interfejsu wiersza polecenia (CLI)]: /cli/azure/overview
[Azure Container Service (ACS)]: https://azure.microsoft.com/services/container-service/
[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/
[portalu Azure]: https://portal.azure.com/
[Maven wtyczki dla aplikacji sieci Web Azure]: https://github.com/Microsoft/azure-maven-plugins/tree/master/azure-webapp-maven-plugin
[Create a private Docker container registry using hello Azure portal]: /azure/container-registry/container-registry-get-started-portal
[Using a custom Docker image for Azure Web App on Linux]: /azure/app-service-web/app-service-linux-using-custom-docker-image
[Docker]: https://www.docker.com/
[Dodatek docker przypadku Maven]: https://github.com/spotify/docker-maven-plugin
[bezpłatne konto platformy Azure]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[Maven]: http://maven.apache.org/
[korzyści dla subskrybentów MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[rozruchu Spring]: http://projects.spring.io/spring-boot/
[rozruchu Spring na wprowadzenie Docker]: https://github.com/spring-guides/gs-spring-boot-docker
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[SB01]: ./media/app-service-web-deploy-spring-boot-app-from-container-registry-using-maven-plugin/SB01.png
[CR01]: ./media/app-service-web-deploy-spring-boot-app-from-container-registry-using-maven-plugin/CR01.png
[AP01]: ./media/app-service-web-deploy-spring-boot-app-from-container-registry-using-maven-plugin/AP01.png
[AP02]: ./media/app-service-web-deploy-spring-boot-app-from-container-registry-using-maven-plugin/AP02.png
