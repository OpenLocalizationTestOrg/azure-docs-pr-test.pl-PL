---
title: "tooAzure aaaDeploy App Service przy użyciu wtyczki Wpięć | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse Wpięć usługi aplikacji Azure wtyczki toodeploy Java web app tooAzure w Wpięć"
services: app-service\web
documentationcenter: 
author: mlearned
manager: douge
editor: 
ms.assetid: 
ms.service: multiple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 7/24/2017
ms.author: mlearned
ms.custom: Jenkins
ms.openlocfilehash: 080be7277555ce7d688dccdf38eef309e7a7b194
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-tooazure-app-service-with-jenkins-plugin"></a>Wdrażanie tooAzure aplikacji usługi z Wpięć wtyczki 
toodeploy tooAzure aplikacji sieci web Java można użyć wiersza polecenia platformy Azure w [potoku Wpięć](/azure/jenkins/execute-cli-jenkins-pipeline) można też korzystać z hello [wtyczki Wpięć usługi aplikacji Azure](https://plugins.jenkins.io/azure-app-service). Ten samouczek zawiera informacje na temat wykonywania następujących czynności:

> [!div class="checklist"]
> * Skonfiguruj tooAzure toodeploy Wpięć usługi aplikacji za pośrednictwem FTP 
> * Skonfiguruj tooAzure toodeploy Wpięć usługi aplikacji w systemie Linux przy użyciu rozwiązania Docker 

## <a name="create-and-configure-jenkins-instance"></a>Tworzenie i konfigurowanie Wpięć wystąpienia
Jeśli nie masz już wzorca Wpięć, rozpoczynać hello [szablon rozwiązania](install-jenkins-solution-template.md), w tym JDK8 oraz hello następujące wymagane wtyczek:

* [Dodatek klienta Git Wpięć](https://plugins.jenkins.io/git-client) v.2.4.6 
* [Dodatek docker Commons](https://plugins.jenkins.io/docker-commons) v.1.4.0
* [Poświadczenia Azure](https://plugins.jenkins.io/azure-credentials) v.1.2
* [Usługa aplikacji Azure](https://plugins.jenkins.io/azure-app-server) v.0.1

Możesz użyć hello usługi aplikacji wtyczki toodeploy aplikacji sieci Web we wszystkich językach (na przykład C#, PHP, Java i node.js itp.) obsługiwanych przez usługę Azure App Service. W tym samouczku używamy hello przykładowej aplikacji Java, [prostej aplikacji sieci Web Java na platformie Azure](https://github.com/azure-devops/javawebappsample). toofork hello repozytorium tooyour własne konto GitHub, kliknij przycisk hello **rozwidlenia** przycisk w prawym górnym rogu hello.  

Wymagane do tworzenia projektu języka Java hello są Java JDK i Maven. Sprawdź, czy zainstalować składniki hello w głównym Wpięć hello lub hello agenta maszyny Wirtualnej, jeśli używany jest jeden dla ciągłej integracji. 

tooinstall, zaloguj się przy użyciu protokołu SSH wystąpienia Wpięć toohello i uruchom następujące polecenia hello:

```bash
sudo apt-get install -y openjdk-7-jdk
sudo apt-get install -y maven
```

Podczas wdrażania usługi w systemie Linux tooApp, konieczne są również tooinstall Docker wzorca Wpięć hello lub agenta maszyny Wirtualnej hello używany dla kompilacji. Zobacz toothis artykułu tooinstall Docker: https://docs.docker.com/engine/installation/linux/ubuntu/.

## <a name="add-azure-service-principal-toojenkins-credential"></a>Dodaj poświadczenie tooJenkins główną usługi Azure

Podmiot zabezpieczeń usługi Azure jest wymagane toodeploy tooAzure. 

<ol>
<li>Użyj [interfejsu wiersza polecenia Azure](/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json) lub [portalu Azure](/azure/azure-resource-manager/resource-group-create-service-principal-portal) toocreate nazwy głównej usługi Azure</li>
<li>W ramach hello Wpięć pulpitu nawigacyjnego, kliknij przycisk **poświadczeń -> System ->**. Kliknij przycisk **credentials(unrestricted) globalne**.</li>
<li>Kliknij przycisk **dodać poświadczenia** tooadd nazwy głównej usługi Microsoft Azure wypełniając hello identyfikator subskrypcji, Identyfikatora klienta, klucz tajny klienta i końcowym tokenów OAuth 2.0. Podaj identyfikator **mySp**, do użycia w kolejnych krokach.</li>
</ol>

## <a name="azure-app-service-plugin"></a>Wtyczka usługi aplikacji Azure

Azure App Service wtyczki 1.0 obsługuje tooAzure ciągłego wdrażania aplikacji sieci Web za pomocą:

* Git i FTP.
* Docker dla aplikacji sieci Web w systemie Linux

## <a name="configure-jenkins-toodeploy-web-app-through-ftp-using-hello-jenkins-dashboard"></a>Skonfiguruj toodeploy Wpięć aplikacji sieci Web za pośrednictwem FTP przy użyciu pulpitu nawigacyjnego Wpięć hello

toodeploy tooAzure Twojego projektu aplikacji sieci Web, możesz przekazać Twojej artefaktów kompilacji (na przykład plik .war w języku Java) przy użyciu narzędzia Git i FTP.

Przed skonfigurowaniem zadania hello w Wpięć, należy plan usługi aplikacji Azure i aplikacji sieci Web dla uruchomionej aplikacji Java hello.


1. Tworzenie planu usługi aplikacji Azure z hello **wolne** przy użyciu hello warstwy cenowej [Tworzenie planu usług aplikacji az](/cli/azure/appservice/plan#create) polecenia interfejsu wiersza polecenia. planu usług aplikacji Hello definiuje hello toohost fizyczne zasoby używane aplikacje. Wszystkie aplikacje przypisane planu usług aplikacji tooan udostępniania tych zasobów, umożliwiając koszt toosave odnośnie do hostowania wielu aplikacji.
2. Utwórz aplikację sieci Web. Można albo użyj hello [portalu Azure](/azure/app-service-web/web-sites-configure) lub hello Użyj następującego polecenia Az interfejsu wiersza polecenia:
```azurecli-interactive 
az webapp create --name <myAppName> --resource-group <myResourceGroup> --plan <myAppServicePlan>
```

3. Upewnij się, że konfigurowanie hello konfigurację środowiska uruchomieniowego języka Java, która Twoja aplikacja powinna. Witaj następującego polecenia wiersza polecenia platformy Azure konfiguruje toorun aplikacji sieci web hello na ostatnie JDK 8 Java i [Apache Tomcat](http://tomcat.apache.org/) 8.0.
```azurecli-interactive
az webapp config set \
--name <myAppName> \
--resource-group <myResourceGroup> \
--java-version 1.8 \
--java-container Tomcat \
--java-container-version 8.0
```

### <a name="set-up-hello-jenkins-job"></a>Konfigurowanie hello Wpięć zadania


1. Utwórz nową **dowolne** projektu na pulpicie nawigacyjnym Wpięć
2. Skonfiguruj **zarządzania kodem źródłowym** toouse rozwidlenia lokalnego z [prostej aplikacji sieci Web Java na platformie Azure](https://github.com/azure-devops/javawebappsample) zapewniając hello **adres URL repozytorium**. Na przykład: http://github.com/&lt;yourID > / javawebappsample.
3. Dodaj projekt hello toobuild kroku kompilacji za pomocą programu Maven. W tym celu Dodawanie **wykonywania powłoki**. Na przykład potrzebujemy pliku dodatkowego kroku toorename hello *.war w tooROOT.war folderu docelowego.   
```bash
mvn clean package
mv target/*.war target/ROOT.war
```

4. Dodaj akcję po kompilacji, wybierając **publikowania aplikacji sieci Web platformy Azure**.
5. Podaj "mySp", podmiot zabezpieczeń usługi Azure hello przechowywane w poprzednim kroku.
6. W **Konfiguracja aplikacji** wybierz hello aplikacji sieci web i grupy zasobów w ramach subskrypcji. Dodatek Hello automatycznie wykrywa, czy Windows hello aplikacji sieci Web lub opartych na systemie Linux. W przypadku aplikacji sieci Web opartych na systemie Windows hello opcji "Publikowania plików" jest widoczne.
7. Wypełnij w plikach hello ma toodeploy (na przykład plik war pakiet Jeśli używasz programu Java.) Katalog źródłowy i katalog docelowy są opcjonalne. Parametry Hello Zezwalaj folder źródłowy i docelowy toospecify przekazywania plików. Aplikacja sieci web Java na platformie Azure jest uruchamiane na serwerze Tomcat. Dlatego możesz przekazać war się pakiet do folderu webapps. Na przykład ustawić **katalog źródłowy** zbyt "target" i "Używanie" podać **katalog docelowy**.
8. Jeśli chcesz toodeploy tooa miejsca niż produkcji, można również ustawić **miejsca** nazwy.
9. Zapisz hello projektu i skompiluj go. Aplikacja sieci web jest wdrożony tooAzure po zakończeniu kompilacji.

### <a name="deploy-web-app-through-ftp-using-jenkins-pipeline"></a>Wdrażanie aplikacji sieci Web za pośrednictwem FTP za pomocą potoku Wpięć

Wtyczka Hello jest gotowe do potoku. Może się odwoływać próbki tooa w repozytorium GitHub hello.

1. W witrynie GitHub interfejsu użytkownika sieci web, otwórz **Jenkinsfile_ftp_plugin** pliku. Kliknij przycisk tooedit ikonę ołówka hello tej grupy zasobów hello tooupdate pliku i nazwa aplikacji sieci web w wierszu 11 i 12.    
```java
def resourceGroup = '<myResourceGroup>'
def webAppName = '<myAppName>'
```

2. Zmień identyfikator poświadczeń 14 tooupdate wiersz w wystąpieniu Wpięć.    
```java
withCredentials([azureServicePrincipal('<mySp>')]) {
```

### <a name="create-a-jenkins-pipeline"></a>Tworzenie potoku Wpięć

1. Otwórz Wpięć w przeglądarce sieci web, kliknij pozycję **nowy element**.
2. Podaj nazwę zadania hello i wybierz **potoku**. Kliknij przycisk **OK**.
3. Kliknij przycisk hello **potoku** karcie dalej.
4. Dla **definicji**, wybierz pozycję **potoku skryptu z SCM**.
5. Aby uzyskać **SCM**, wybierz pozycję **Git**. Wprowadź hello GitHub adres URL dla Twojego repozytorium rozwidlonych: https:&lt;Twojego repozytorium rozwidlonych > .git
6. Aktualizacja **ścieżka skryptu** zbyt "Jenkinsfile_ftp_plugin"
7. Kliknij przycisk **zapisać** i hello wykonywania zadania.

## <a name="configure-jenkins-toodeploy-web-app-on-linux-through-docker"></a>Skonfiguruj toodeploy Wpięć aplikacji sieci Web w systemie Linux przy użyciu rozwiązania Docker

Oprócz Git/FTP aplikacji sieci Web w systemie Linux obsługuje wdrażanie przy użyciu rozwiązania Docker. toodeploy przy użyciu rozwiązania Docker, należy tooprovide plik Dockerfile, które pakiety aplikacji sieci web za pomocą usługi czasu wykonywania w obrazie docker. Następnie wtyczki hello tworzy obraz powitania, wypchnięcia jej tooa docker rejestru i wdraża aplikację sieci web tooyour obraz powitania.

Aplikacji w systemie Linux sieci Web obsługuje także tradycyjnych sposoby, takie jak usługi Git i FTP, ale tylko dla wbudowanych języków (.NET Core, Node.js, PHP i Ruby). W przypadku innych języków toopackage runtime kod i usługi aplikacji razem w obrazie docker a za pomocą docker toodeploy.

Przed skonfigurowaniem zadania hello w Wpięć, należy usługi aplikacji Azure w systemie Linux. Rejestru kontenera jest również wymagana toostore i zarządzaj nimi prywatnej obrazy usługi Docker kontenera. Można użyć DockerHub; w tym przykładzie jest używany rejestru kontenera platformy Azure.

* Możesz wykonać kroki hello [tutaj](/azure/app-service-web/app-service-linux-how-to-create-web-app) toocreate aplikacji sieci Web w systemie Linux 
* Rejestru kontenera platformy Azure jest zarządzany [Docker rejestru] usługi (https://docs.docker.com/registry/) na podstawie hello 2.0 rejestru Docker open source. Wykonaj kroki hello [tutaj] (/ azure/container-registry/container-registry-get-started-azure-cli) Aby uzyskać więcej pomocy na temat toodo tak. Można również użyć DockerHub.

### <a name="toodeploy-using-docker"></a>przy użyciu rozwiązania docker toodeploy:

1. Utwórz nowy projekt stylu Wpięć w pulpicie nawigacyjnym.
2. Skonfiguruj **zarządzania kodem źródłowym** toouse rozwidlenia lokalnego z [prostej aplikacji sieci Web Java na platformie Azure](https://github.com/azure-devops/javawebappsample) zapewniając hello **adres URL repozytorium**. Na przykład: http://github.com/&lt;yourid > / javawebappsample.
Dodaj projekt hello toobuild kroku kompilacji za pomocą programu Maven. To zrobić przez dodanie **wykonywania powłoki** i Dodaj powitania po wierszu **polecenia**:    
```bash
mvn clean package
```

3. Dodaj akcję po kompilacji, wybierając **publikowania aplikacji sieci Web platformy Azure**.
4. Podaj, **mySp**, podmiot zabezpieczeń usługi Azure hello przechowywane w poprzednim kroku jako poświadczeń usługi Azure.
5. W **Konfiguracja aplikacji** wybierz hello grupy zasobów i aplikacji sieci web systemu Linux w Twojej subskrypcji.
6. Wybierz publikowanie za pośrednictwem Docker.
7. Wypełnij **plik Dockerfile** ścieżki. Umożliwia zachowanie domyślne hello "/ plik Dockerfile" dla **URL rejestru Docker**, dostawy w formacie hello https://&lt;myRegistry >. azurecr.io, korzystając z rejestru kontenera platformy Azure. Pozostaw pole puste, jeśli używasz DockerHub.
8. Dla **poświadczenia rejestru**, Dodaj poświadczenie hello hello rejestru kontenera platformy Azure. Witaj identyfikator użytkownika i hasło można uzyskać, uruchamiając hello następującego polecenia wiersza polecenia platformy Azure. pierwsze polecenie Hello umożliwia hello konta administratora.    
```azurecli-interactive
az acr update -n <yourRegistry> --admin-enabled true
az acr credential show -n <yourRegistry>
```

9. Witaj nazwa obrazu docker i tagu w **zaawansowane** kartę są opcjonalne. Domyślnie nazwa obrazu są uzyskiwane z obrazu hello nazwę skonfigurowaną w tagu Azure hello portalu (w kontenerze Docker ustawienie.) są generowane na podstawie $BUILD_NUMBER. Upewnij się, określ nazwę obraz powitania w jednej wersji portalu Azure lub podać wartość **obrazu Docker** w **zaawansowane** kartę. Na przykład Podaj "&lt;yourRegistry >.azurecr.io/calculator" dla **obrazu Docker** i pozostawić **Tag obrazu Docker** puste.
10. Uwaga, wdrożenie zakończy się niepowodzeniem, korzystając z wbudowanego ustawienie obrazu Docker. Upewnij się, że zmiana docker config toouse niestandardowego obrazu w kontenerze Docker ustawienia w portalu Azure. Wbudowane obrazu użyj toodeploy podejście przekazywania plików.
11. Podejście podobne przekazywania toofile, można wybrać różne miejsca niż produkcji.
12. Zapisania i skompilowania projektu hello. Zobaczysz kontener obrazu spoczywa tooyour rejestru i wdrażania aplikacji sieci web.

### <a name="deploy-tooweb-app-on-linux-through-docker-using-jenkins-pipeline"></a>Wdrażanie aplikacji w systemie Linux przy użyciu rozwiązania Docker za pomocą potoku Wpięć tooWeb

1. W witrynie GitHub interfejsu użytkownika sieci web, otwórz **Jenkinsfile_container_plugin** pliku. Kliknij przycisk tooedit ikonę ołówka hello tej grupy zasobów hello tooupdate pliku i nazwa aplikacji sieci web w wierszu 11 i 12.    
```java
def resourceGroup = '<myResourceGroup>'
def webAppName = '<myAppName>'
```

2. Zmiana wiersza 13 tooyour kontenera rejestru serwera    
```java
def registryServer = '<registryURL>'
```    

3. Zmień identyfikator poświadczeń 16 tooupdate wiersz w wystąpieniu Wpięć    
```java
azureWebAppPublish azureCredentialsId: '<mySp>', publishType: 'docker', resourceGroup: resourceGroup, appName: webAppName, dockerImageName: imageName, dockerImageTag: imageTag, dockerRegistryEndpoint: [credentialsId: 'acr', url: "http://$registryServer"]
```    
### <a name="create-jenkins-pipeline"></a>Tworzenie potoku Wpięć    

1. Otwórz Wpięć w przeglądarce sieci web, kliknij pozycję **nowy element**.
2. Podaj nazwę zadania hello i wybierz **potoku**. Kliknij przycisk **OK**.
3. Kliknij przycisk hello **potoku** karcie dalej.
4. Dla **definicji**, wybierz pozycję **potoku skryptu z SCM**.
5. Aby uzyskać **SCM**, wybierz pozycję **Git**.
6. Wprowadź hello GitHub adres URL dla Twojego repozytorium rozwidlonych: https:&lt;Twojego repozytorium rozwidlonych > .git</li>
Zaktualizuj 7, **ścieżka skryptu** zbyt "Jenkinsfile_container_plugin"
8. Kliknij przycisk **zapisać** i hello wykonywania zadania.

## <a name="verify-your-web-app"></a>Sprawdź aplikację sieci web

1. plik WAR hello tooverify został wdrożony pomyślnie tooyour aplikacji sieci web. Otwórz przeglądarkę sieci web.
2. Przejdź toohttp: / /&lt;nazwa_aplikacji >.azurewebsites.net/api/calculator/ping zostanie wyświetlony:    
     Zapraszamy tooJava aplikacji sieci Web! Ta wartość jest aktualizowana!
   Sun cze 17 16:39:10 UTC 2017
3. Przejdź toohttp: / /&lt;nazwa_aplikacji >.azurewebsites.net/api/calculator/add?x=&lt;x > & y =&lt;y > (Zastąp &lt;x > i &lt;y > z dowolnej liczby) tooget hello sumę x i y        
    ![Kalkulator: Dodaj](./media/execute-cli-jenkins-pipeline/calculator-add.png)

### <a name="for-app-service-on-linux"></a>Usługi aplikacji w systemie Linux

* tooverify w wiersza polecenia platformy Azure, uruchom:

    ```
    az acr repository list -n <myRegistry> -o json
    ```

    Możesz uzyskać hello następujące wyniki:
    
    ```
    [
    "calculator"
    ]
    ```
    
    Przejdź toohttp: / /&lt;nazwa_aplikacji >.azurewebsites.net/api/calculator/ping. Zostanie wyświetlony komunikat hello: 
    
        Welcome tooJava Web App!!! This is updated!
        Sun Jul 09 16:39:10 UTC 2017

    Przejdź toohttp: / /&lt;nazwa_aplikacji >.azurewebsites.net/api/calculator/add?x=&lt;x > & y =&lt;y > (Zastąp &lt;x > i &lt;y > z dowolnej liczby) tooget hello sumę x i y
    
## <a name="next-steps"></a>Następne kroki

W tym samouczku używamy tooAzure toodeploy wtyczki hello w usłudze Azure App Service.

W tym samouczku omówiono:

> [!div class="checklist"]
> * Skonfiguruj toodeploy Wpięć usługi Azure App Service za pośrednictwem FTP 
> * Skonfiguruj tooAzure toodeploy Wpięć usługi aplikacji w systemie Linux przy użyciu rozwiązania Docker 
