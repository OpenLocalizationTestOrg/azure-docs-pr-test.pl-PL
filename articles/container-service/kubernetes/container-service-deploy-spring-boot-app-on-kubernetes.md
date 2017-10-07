---
title: "aaaDeploy aplikacji rozruchu sieci Spring na Kubernetes usługi kontenera platformy Azure | Dokumentacja firmy Microsoft"
description: "Ten samouczek przeprowadzi Cię jednak hello kroki toodeploy aplikacja Spring rozruchu w klastrze Kubernetes w systemie Microsoft Azure."
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
ms.openlocfilehash: 2bf9df459f874a1f478f43cdd29992d86c370837
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-spring-boot-application-on-a-kubernetes-cluster-in-hello-azure-container-service"></a>Wdrażanie aplikacji rozruchu Spring w klastrze Kubernetes w hello usługi kontenera platformy Azure

Witaj  **[Spring Framework]**  popularnych struktura open source, który pomaga Java deweloperom tworzenie aplikacji interfejsu API, mobilne i sieci web. W tym samouczku używana przykładowej aplikacji utworzony za pomocą [rozruchu Spring], podejście oparte na Konwencji poświęcone Spring tooget szybko rozpocząć pracę.

**[Kubernetes]**  i  **[Docker]**  są rozwiązania open source, które ułatwiają deweloperom automatyzację wdrażania hello, skalowania i zarządzania swoje aplikacje uruchomione w kontenerach.

Ten samouczek przeprowadzi Cię, jeśli połączenie tych dwóch popularnych open source technologii toodevelop i wdrażanie rozruchu Spring tooMicrosoft aplikacji Azure. W szczególności, użyj  *[rozruchu Spring]*  przy projektowaniu aplikacji,  *[Kubernetes]*  wdrożenia kontenera i hello [Usługi kontenera platformy azure (ACS)] toohost aplikacji.

### <a name="prerequisites"></a>Wymagania wstępne

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

Witaj następujące kroki opisano tworzenie aplikacji sieci web Spring rozruchu i testowanie go lokalnie.

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

1. Witaj w klonowania [rozruchu Spring na wprowadzenie Docker] przykładowy projekt do katalogu hello.
   ```
   git clone https://github.com/spring-guides/gs-spring-boot-docker.git
   ```

1. Zmień katalog projektu toohello ukończone.
   ```
   cd gs-spring-boot-docker
   cd complete
   ```

1. Użyj Maven toobuild i wykonywania hello przykładowej aplikacji.
   ```
   mvn package spring-boot:run
   ```

1. Test aplikacji sieci web hello przechodząc toohttp://localhost:8080 lub następujący hello `curl` polecenia:
   ```
   curl http://localhost:8080
   ```

1. Powinien zostać wyświetlony komunikat wyświetlany po hello: **Hello Docker World**

   ![Przejdź do przykładowej aplikacji lokalnie][SB01]

## <a name="create-an-azure-container-registry-using-hello-azure-cli"></a>Tworzenie przy użyciu interfejsu wiersza polecenia Azure hello rejestru kontenera platformy Azure

1. Otwórz wiersz polecenia.

1. Zaloguj się tooyour konto platformy Azure:
   ```azurecli
   az login
   ```

1. Utwórz grupę zasobów dla hello Azure zasoby używane w tym samouczku.
   ```azurecli
   az group create --name=wingtiptoys-kubernetes --location=eastus
   ```

1. Utwórz rejestru prywatnej kontenera platformy Azure w grupie zasobów hello. Samouczek Hello wypycha hello przykładową aplikację jako rejestru toothis Docker obrazu w kolejnych krokach. Zastąp `wingtiptoysregistry` o unikatowej nazwie dla rejestru.
   ```azurecli
   az acr create --admin-enabled --resource-group wingtiptoys-kubernetes--location eastus \
    --name wingtiptoysregistry --sku Basic
   ```

## <a name="push-your-app-toohello-container-registry"></a>Wypychanie rejestru kontenera toohello aplikacji

1. Przejdź do katalogu konfiguracji toohello instalacji Maven (~/.m2/ domyślne lub C:\Users\username\.m2) i otwórz hello *settings.xml* plik w edytorze tekstów.

1. Pobrać hasło hello rejestru kontenera z hello wiersza polecenia platformy Azure.
   ```azurecli
   az acr credential show --name wingtiptoysregistry --query passwords[0]
   ```

   ```json
   {
  "name": "password",
  "value": "AbCdEfGhIjKlMnOpQrStUvWxYz"
   }
   ```

1. Dodaj z rejestru kontenera Azure id i hasła tooa nowe `<server>` kolekcji w hello *settings.xml* pliku.
Witaj `id` i `username` są nazwa hello hello rejestru. Użyj hello `password` wartość z zakresu od poprzedniego polecenia hello (bez cudzysłowów).

   ```xml
   <servers>
      <server>
         <id>wingtiptoysregistry</id>
         <username>wingtiptoysregistry</username>
         <password>AbCdEfGhIjKlMnOpQrStUvWxYz</password>
      </server>
   </servers>
   ```

1. Przejdź do katalogu projektu toohello ukończone aplikacji Spring rozruchu (na przykład "*C:\SpringBoot\gs-spring-boot-docker\complete*"lub"*/users/robert/SpringBoot/gs-spring-boot-docker / pełne*") i otwórz hello *pom.xml* plik w edytorze tekstów.

1. Aktualizacja hello `<properties>` kolekcji w hello *pom.xml* pliku z wartością serwera logowania hello rejestru kontenera platformy Azure.

   ```xml
   <properties>
      <docker.image.prefix>wingtiptoysregistry.azurecr.io</docker.image.prefix>
      <java.version>1.8</java.version>
   </properties>
   ```

1. Aktualizacja hello `<plugins>` kolekcji w hello *pom.xml* pliku, który hello `<plugin>` zawiera powitania serwera adres i rejestru nazwę logowania dla rejestr kontenera platformy Azure.

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

1. Przejdź do katalogu projektu toohello ukończone aplikacji Spring rozruchu i uruchom następujące polecenie toobuild hello Docker kontenera i wypychania hello obrazu toohello rejestru hello:

   ```
   mvn package docker:build -DpushImage
   ```

> [!NOTE]
>
>  Użytkownik może zostać wyświetlony komunikat o błędzie jest podobny tooone hello następującego przypadku Maven wypchnięcia tooAzure obrazu hello:
>
> * `[ERROR] Failed tooexecute goal com.spotify:docker-maven-plugin:0.4.11:build (default-cli) on project gs-spring-boot-docker: Exception caught: no basic auth credentials`
>
> * `[ERROR] Failed tooexecute goal com.spotify:docker-maven-plugin:0.4.11:build (default-cli) on project gs-spring-boot-docker: Exception caught: Incomplete Docker registry authorization credentials. Please provide all of username, password, and email or none.`
>
> Jeśli ten błąd wystąpi, zaloguj się za tooAzure z wiersza polecenia Docker hello.
>
> `docker login -u wingtiptoysregistry -p "AbCdEfGhIjKlMnOpQrStUvWxYz" wingtiptoysregistry.azurecr.io`
>
> Następnie Wypchnij z kontenera:
>
> `docker push wingtiptoysregistry.azurecr.io/gs-spring-boot-docker`

## <a name="create-a-kubernetes-cluster-on-acs-using-hello-azure-cli"></a>Tworzenie klastra Kubernetes na ACS za pomocą hello wiersza polecenia platformy Azure

1. Utwórz klaster Kubernetes usługi kontenera platformy Azure. Witaj poniższe polecenie tworzy *kubernetes* klastra w hello *wingtiptoys kubernetes* zasobów grupy z *wingtiptoys containerservice* jako klaster hello Nazwa i *wingtiptoys kubernetes* jako prefiks DNS hello:
   ```azurecli
   az acs create --orchestrator-type=kubernetes --resource-group=wingtiptoys-kubernetes \ 
    --name=wingtiptoys-containerservice --dns-prefix=wingtiptoys-kubernetes
   ```
   Polecenie to może chwilę potrwać toocomplete.

1. Zainstaluj `kubectl` przy użyciu hello wiersza polecenia platformy Azure. Użytkownicy systemu Linux mogą mieć tooprefix, to polecenie z `sudo` ponieważ wdraża hello Kubernetes CLI zbyt`/usr/local/bin`.
   ```azurecli
   az acs kubernetes install-cli
   ```

1. Pobierz informacje o konfiguracji klastra hello tak klastra można zarządzać za pomocą interfejsu sieci web Kubernetes hello i `kubectl`. 
   ```azurecli
   az acs kubernetes get-credentials --resource-group=wingtiptoys-kubernetes  \ 
    --name=wingtiptoys-containerservice
   ```

## <a name="deploy-hello-image-tooyour-kubernetes-cluster"></a>Wdrażanie klastra Kubernetes tooyour obraz powitania

W tym samouczku wdraża przy użyciu aplikacji hello `kubectl`, pozwoli Ci tooexplore hello wdrożenia za pośrednictwem interfejsu sieci web Kubernetes hello.

### <a name="deploy-with-hello-kubernetes-web-interface"></a>Rozmieszczanie za pomocą interfejsu sieci web Kubernetes hello

1. Otwórz wiersz polecenia.

1. Otwórz hello konfiguracji witryny sieci Web dla klastra Kubernetes w domyślnej przeglądarce:
   ```
   az acs kubernetes browse --resource-group=wingtiptoys-kubernetes --name=wingtiptoys-containerservice
   ```

1. Po otwarciu hello Kubernetes konfiguracji witryny sieci Web w przeglądarce, kliknij łącze hello zbyt**wdrażania konteneryzowanych aplikacji**:

   ![Kubernetes konfiguracji witryny sieci Web][KB01]

1. Gdy hello **wdrażania konteneryzowanych aplikacji** zostanie wyświetlona strona, określ hello następujące opcje:

   a. Wybierz **Określ szczegóły aplikacji poniżej**.

   b. Wprowadź nazwę aplikacji Spring rozruchu dla hello **Nazwa aplikacji**, na przykład: "*gs-spring — rozruchu — docker*".

   c. Wprowadź nazwy logowania serwera i kontener obrazu z wcześniej hello **obrazu kontenera**, na przykład: "*wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest*".

   d. Wybierz **zewnętrznych** dla hello **usługi**.

   e. Określ sieci zewnętrznych i wewnętrznych portów w hello **portu** i **docelowy port** pól tekstowych.

   ![Kubernetes konfiguracji witryny sieci Web][KB02]


1. Kliknij przycisk **Wdróż** toodeploy hello kontenera.

   ![Wdrażanie kontenera][KB05]

1. Po wdrożeniu aplikacji, zostanie wyświetlona aplikacji rozruchu Spring kategorii **usług**.

   ![Kubernetes usług][KB06]

1. Po kliknięciu łącza hello **zewnętrzne punkty końcowe**, zobaczysz rozruchu Spring aplikacji działających na platformie Azure.

   ![Kubernetes usług][KB07]

   ![Przejdź do przykładowej aplikacji na platformie Azure][SB02]


### <a name="deploy-with-kubectl"></a>Wdrażanie z kubectl

1. Otwórz wiersz polecenia.

1. Uruchom z kontenera hello Kubernetes klastra przy użyciu hello `kubectl run` polecenia. Nadaj nazwę usługi dla aplikacji na Kubernetes i hello pełnego obrazu. Na przykład:
   ```
   kubectl run gs-spring-boot-docker --image=wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest
   ```
   W tym poleceniu:

   * Nazwa kontenera Hello `gs-spring-boot-docker` określono natychmiast po hello `run` polecenia

   * Witaj `--image` parametr określa hello połączone nazwy logowania serwera i nazwa obrazu jako`wingtiptoysregistry.azurecr.io/gs-spring-boot-docker:latest`

1. Udostępnianie klastra Kubernetes zewnętrznie, używając hello `kubectl expose` polecenia. Określ nazwę usługi, hello publicznych TCP port używany tooaccess hello aplikacji i hello wewnętrzny docelowy port, którego nasłuchuje aplikacji. Na przykład:
   ```
   kubectl expose deployment gs-spring-boot-docker --type=LoadBalancer --port=80 --target-port=8080
   ```
   W tym poleceniu:

   * Nazwa kontenera Hello `gs-spring-boot-docker` określono natychmiast po hello `expose deployment` polecenia

   * Witaj `--type` parametr określa klastra hello używa modułu równoważenia obciążenia

   * Witaj `--port` parametr określa hello publicznych port TCP 80. Możesz uzyskać dostępu do aplikacji hello na tym porcie.

   * Witaj `--target-port` parametr określa hello wewnętrznego portu TCP 8080. Moduł równoważenia obciążenia Hello przekazuje żądania tooyour aplikacji na tym porcie.

1. Po wdrożeniu aplikacji hello klastra toohello zapytania hello zewnętrzny adres IP i otworzyć go w przeglądarce sieci web:

   ```
   kubectl get services -o jsonpath={.items[*].status.loadBalancer.ingress[0].ip} --namespace=${namespace}
   ```

   ![Przejdź do przykładowej aplikacji na platformie Azure][SB02]


## <a name="next-steps"></a>Następne kroki

Aby uzyskać więcej informacji na temat Spring rozruch przy użyciu na platformie Azure zobacz następujące artykuły hello:

* [Wdrażanie aplikacji rozruchu Spring toohello usłudze Azure App Service](../../app-service/app-service-deploy-spring-boot-web-app-on-azure.md)
* [Wdrażanie aplikacji Spring rozruchu w systemie Linux w hello usługi kontenera platformy Azure](container-service-deploy-spring-boot-app-on-linux.md)

Aby uzyskać więcej informacji o korzystaniu z językiem Java Azure, zobacz hello [Azure Java Developer Center] i hello [Java Tools for Visual Studio Team Services].

Aby uzyskać więcej informacji na temat hello Spring rozruchu na Docker przykładowy projekt, zobacz [rozruchu Spring na wprowadzenie Docker].

Witaj następującego łącza znajdują się dodatkowe informacje o tworzeniu aplikacji Spring rozruchu:

* Aby uzyskać więcej informacji dotyczących tworzenia prostej aplikacji Spring rozruchu Zobacz hello Spring Initializr na https://start.spring.io/.

Witaj poniższe linki udostępniają dodatkowe informacje dotyczące korzystania z usługi Azure Kubernetes:

* [Rozpoczynanie pracy z klastrem Kubernetes w usłudze kontenera](https://docs.microsoft.com/azure/container-service/container-service-kubernetes-walkthrough)
* [Przy użyciu hello Kubernetes interfejs użytkownika sieci web z usługi kontenera platformy Azure](https://docs.microsoft.com/azure/container-service/container-service-kubernetes-ui)

Więcej informacji na temat przy użyciu interfejsu wiersza polecenia Kubernetes jest dostępna w hello **kubectl** Podręcznik użytkownika w <https://kubernetes.io/docs/user-guide/kubectl/>.

Witaj Kubernetes witryny sieci Web ma kilka artykuł, w którym omówiono w nim przy użyciu obrazów w rejestrach prywatnych:

* [Konfigurowanie usługi konta dla stanowiskami]
* [Przestrzenie nazw]
* [Ściąganie obrazu z rejestru prywatnych]

Aby uzyskać dodatkowe przykłady sposobu toouse Docker niestandardowe obrazy z platformy Azure, zobacz [dla aplikacji sieci Web platformy Azure w systemie Linux przy użyciu niestandardowego obrazu Docker].

<!-- URL List -->

[Azure interfejsu wiersza polecenia (CLI)]: /cli/azure/overview
[Usługi kontenera platformy azure (ACS)]: https://azure.microsoft.com/services/container-service/
[Azure Java Developer Center]: https://azure.microsoft.com/develop/java/
[Azure portal]: https://portal.azure.com/
[Create a private Docker container registry using hello Azure portal]: /azure/container-registry/container-registry-get-started-portal
[dla aplikacji sieci Web platformy Azure w systemie Linux przy użyciu niestandardowego obrazu Docker]: /azure/app-service-web/app-service-linux-using-custom-docker-image
[Docker]: https://www.docker.com/
[bezpłatne konto platformy Azure]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Java Tools for Visual Studio Team Services]: https://java.visualstudio.com/
[Kubernetes]: https://kubernetes.io/
[Kubernetes Command-Line Interface (kubectl)]: https://kubernetes.io/docs/user-guide/kubectl-overview/
[Maven]: http://maven.apache.org/
[korzyści dla subskrybentów MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[rozruchu Spring]: http://projects.spring.io/spring-boot/
[rozruchu Spring na wprowadzenie Docker]: https://github.com/spring-guides/gs-spring-boot-docker
[Spring Framework]: https://spring.io/
[Konfigurowanie usługi konta dla stanowiskami]: https://kubernetes.io/docs/tasks/configure-pod-container/configure-service-account/
[Przestrzenie nazw]: https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/
[Ściąganie obrazu z rejestru prywatnych]: https://kubernetes.io/docs/tasks/configure-pod-container/pull-image-private-registry/

<!-- IMG List -->

[SB01]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/SB01.png
[SB02]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/SB02.png

[AR01]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/AR01.png
[AR02]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/AR02.png
[AR03]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/AR03.png
[AR04]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/AR04.png

[KB01]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/KB01.png
[KB02]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/KB02.png
[KB03]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/KB03.png
[KB04]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/KB04.png
[KB05]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/KB05.png
[KB06]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/KB06.png
[KB07]: ./media/container-service-deploy-spring-boot-app-on-kubernetes/KB07.png
