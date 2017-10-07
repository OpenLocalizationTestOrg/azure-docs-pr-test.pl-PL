---
title: "Witaj aaaExecute wiersza polecenia platformy Azure z Wpięć | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse toodeploy interfejsu wiersza polecenia Azure Java web tooAzure aplikacji w potoku Wpięć"
services: app-service\web
documentationcenter: 
author: mlearned
manager: douge
editor: 
ms.assetid: 
ms.service: jenkins
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 6/7/2017
ms.author: mlearned
ms.custom: Jenkins
ms.openlocfilehash: 4bd1e12e6de1f010453ff51c835f84e7361962f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-tooazure-app-service-with-jenkins-and-hello-azure-cli"></a>Wdrażanie aplikacji usługi z Wpięć tooAzure i hello wiersza polecenia platformy Azure
toodeploy tooAzure aplikacji sieci web Java można użyć wiersza polecenia platformy Azure w [potoku Wpięć](https://jenkins.io/doc/book/pipeline/). W tym samouczku, możesz utworzyć potok CI/CD na maszynie Wirtualnej platformy Azure w tym jak:

> [!div class="checklist"]
> * Tworzenie maszyny Wirtualnej z Wpięć
> * Skonfiguruj Wpięć
> * Tworzenie aplikacji sieci web na platformie Azure
> * Przygotowanie repozytorium GitHub
> * Tworzenie potoku Wpięć
> * Należy uruchomić potoku hello i sprawdzić hello aplikacji sieci web

Ten samouczek wymaga hello Azure CLI w wersji 2.0.4 lub nowszej. Wersja hello toofind, uruchom `az --version`. Jeśli potrzebujesz tooupgrade, zobacz [zainstalować Azure CLI 2.0]( /cli/azure/install-azure-cli).

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

## <a name="create-and-configure-jenkins-instance"></a>Tworzenie i konfigurowanie Wpięć wystąpienia
Jeśli nie masz już wzorca Wpięć, rozpoczynać hello [szablon rozwiązania](install-jenkins-solution-template.md), która obejmuje hello wymagane [poświadczenia Azure](https://plugins.jenkins.io/azure-credentials) wtyczki domyślnie. 

wtyczki poświadczenia Azure Hello umożliwia toostore poświadczenia główne usługi Microsoft Azure z Wpięć. W wersji 1.2 Dodaliśmy obsługę hello dlatego tego potoku Wpięć można pobrać hello Azure poświadczenia. 

Upewnij się, że w wersji 1.2 lub nowszej:
* W ramach hello Wpięć pulpitu nawigacyjnego, kliknij przycisk **Menedżera wtyczki -> Zarządzaj Wpięć ->** i wyszukaj **poświadczenia Azure**. 
* Zaktualizuj hello wtyczki, jeśli wersja hello jest starsza niż 1.2.

Java JDK i Maven są również wymagane w hello Wpięć wzorca. tooinstall, zaloguj się przy użyciu protokołu SSH wzorca tooJenkins i uruchom następujące polecenia hello:
```bash
sudo apt-get install -y openjdk-7-jdk
sudo apt-get install -y maven
```

## <a name="add-azure-service-principal-toojenkins-credential"></a>Dodaj poświadczenie tooJenkins główną usługi Azure

Poświadczenie Azure jest wymagane tooexecute wiersza polecenia platformy Azure.

* W ramach hello Wpięć pulpitu nawigacyjnego, kliknij przycisk **poświadczeń -> System ->**. Kliknij przycisk **credentials(unrestricted) globalne**.
* Kliknij przycisk **dodać poświadczenia** tooadd [nazwy głównej usługi Microsoft Azure](https://docs.microsoft.com/en-us/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json) wypełniając hello identyfikator subskrypcji, Identyfikatora klienta, klucz tajny klienta i końcowym tokenów OAuth 2.0. Podaj identyfikator do użycia w kolejnym kroku.

![Dodawanie poświadczeń](./media/execute-cli-jenkins-pipeline/add-credentials.png)

## <a name="create-an-azure-app-service-for-deploying-hello-java-web-app"></a>Tworzenie usługi aplikacji Azure do wdrażania aplikacji sieci web Java hello

Tworzenie planu usługi aplikacji Azure z hello **wolne** przy użyciu hello warstwy cenowej [Tworzenie planu usług aplikacji az](/cli/azure/appservice/plan#create) polecenia interfejsu wiersza polecenia. planu usług aplikacji Hello definiuje hello toohost fizyczne zasoby używane aplikacje. Wszystkie aplikacje przypisane planu usług aplikacji tooan udostępniania tych zasobów, umożliwiając koszt toosave odnośnie do hostowania wielu aplikacji. 

```azurecli-interactive
az appservice plan create \
    --name myAppServicePlan \ 
    --resource-group myResourceGroup \
    --sku FREE
```

Jeśli hello plan jest gotowy, powitalne interfejsu wiersza polecenia Azure zawiera podobne dane wyjściowe toohello poniższy przykład:

```json
{ 
  "adminSiteName": null,
  "appServicePlanName": "myAppServicePlan",
  "geoRegion": "North Europe",
  "hostingEnvironmentProfile": null,
  "id": "/subscriptions/0000-0000/resourceGroups/myResourceGroup/providers/Microsoft.Web/serverfarms/myAppServicePlan",
  "kind": "app",
  "location": "North Europe",
  "maximumNumberOfWorkers": 1,
  "name": "myAppServicePlan",
  ...
  < Output has been truncated for readability >
} 
``` 

### <a name="create-an-azure-web-app"></a>Tworzenie aplikacji sieci Web platformy Azure

 Użyj hello [tworzenie aplikacji sieci Web az](/cli/azure/appservice/web#create) toocreate polecenia interfejsu wiersza polecenia definicję aplikacji sieci web w hello `myAppServicePlan` planu usługi aplikacji. definicję aplikacji sieci web Hello zapewnia tooaccess adres URL aplikacji przy użyciu i konfiguruje kilka opcji toodeploy Twojego tooAzure kodu. 

```azurecli-interactive
az webapp create \
    --name <app_name> \ 
    --resource-group myResourceGroup \
    --plan myAppServicePlan
```

SUBSTITUTE hello `<app_name>` symbol zastępczy własne unikatowej nazwy aplikacji. Ta nazwa jest część hello domyślna nazwa domeny dla aplikacji sieci web hello, więc nazwa hello musi toobe unikatowy przez wszystkie aplikacje w usłudze Azure. Przed udostępnieniem jej tooyour użytkowników, możesz mapować aplikacji sieci web toohello wpis nazwy domeny niestandardowej.

Podczas definiowania aplikacji sieci web hello jest gotowy, hello Azure CLI pokazuje informacje toohello podobnie poniższy przykład: 

```json 
{
  "availabilityState": "Normal",
  "clientAffinityEnabled": true,
  "clientCertEnabled": false,
  "cloningInfo": null,
  "containerSize": 0,
  "dailyMemoryTimeQuota": 0,
  "defaultHostName": "<app_name>.azurewebsites.net",
  "enabled": true,
   ...
  < Output has been truncated for readability >
}
```

### <a name="configure-java"></a>Konfigurowanie języka Java 

Skonfigurować hello Java runtime wymagające aplikacji z hello [aktualizacja konfiguracji sieci web appservice az](/cli/azure/appservice/web/config#update) polecenia.

Witaj następujące polecenie konfiguruje toorun aplikacji sieci web hello na ostatnie JDK 8 Java i [Apache Tomcat](http://tomcat.apache.org/) 8.0.

```azurecli-interactive
az webapp config set \ 
    --name <app_name> \
    --resource-group myResourceGroup \ 
    --java-version 1.8 \ 
    --java-container Tomcat \
    --java-container-version 8.0
```

## <a name="prepare-a-github-repository"></a>Przygotowanie repozytorium GitHub
Otwórz hello [prostej aplikacji sieci Web Java na platformie Azure](https://github.com/azure-devops/javawebappsample) repozytorium. toofork hello repozytorium tooyour własne konto GitHub, kliknij przycisk hello **rozwidlenia** przycisk w prawym górnym rogu hello.

* W witrynie GitHub interfejsu użytkownika sieci web, otwórz **Jenkinsfile** pliku. Kliknij przycisk tooedit ikonę ołówka hello tej grupy zasobów hello tooupdate pliku i nazwa aplikacji sieci web w wierszu 20 i 21.

```java
def resourceGroup = '<myResourceGroup>'
def webAppName = '<app_name>'
```

* Zmień identyfikator poświadczeń 23 tooupdate wiersz w wystąpieniu Wpięć

```java
withCredentials([azureServicePrincipal('<mySrvPrincipal>')]) {
```

## <a name="create-jenkins-pipeline"></a>Tworzenie potoku Wpięć
Otwórz Wpięć w przeglądarce sieci web, kliknij pozycję **nowy element**. 

* Podaj nazwę zadania hello i wybierz **potoku**. Kliknij przycisk **OK**.
* Kliknij przycisk hello **potoku** karcie dalej. 
* Dla **definicji**, wybierz pozycję **potoku skryptu z SCM**.
* Aby uzyskać **SCM**, wybierz pozycję **Git**.
* Wprowadź hello GitHub adres URL dla Twojego repozytorium rozwidlonych: https:\<Twojego repozytorium rozwidlonych\>.git
* Kliknij przycisk **Zapisz**

## <a name="test-your-pipeline"></a>Testowanie potoku sieci
* Przejdź toohello potok został utworzony, kliknij przycisk **kompilacji teraz**
* Kompilacja ma być pomyślnie wykonane w ciągu kilku sekund i można go toohello kompilacji i kliknij przycisk **dane wyjściowe konsoli** toosee hello szczegóły

## <a name="verify-your-web-app"></a>Sprawdź aplikację sieci web
plik WAR hello tooverify został wdrożony pomyślnie tooyour aplikacji sieci web. Otwórz przeglądarkę sieci web:

* Przejdź toohttp: / /&lt;nazwa_aplikacji >.azurewebsites.net/api/calculator/ping  
Zobacz:

        Welcome tooJava Web App!!! This is updated!
        Sun Jun 17 16:39:10 UTC 2017

* Przejdź toohttp: / /&lt;nazwa_aplikacji >.azurewebsites.net/api/calculator/add?x=&lt;x > & y =&lt;y > (Zastąp &lt;x > i &lt;y > z dowolnej liczby) tooget hello sumę x i y

![Kalkulator: Dodaj](./media/execute-cli-jenkins-pipeline/calculator-add.png)

## <a name="deploy-tooazure-web-app-on-linux"></a>Wdrażanie tooAzure aplikacji sieci Web w systemie Linux
Teraz, gdy wiesz, jak toouse wiersza polecenia platformy Azure w sieci Wpięć potoku, można zmodyfikować hello skryptu toodeploy tooan aplikacji sieci Web platformy Azure w systemie Linux.

Aplikacji w systemie Linux sieci Web obsługuje wdrożenia hello toodo inny sposób, który jest toouse Docker. toodeploy, należy tooprovide plik Dockerfile, które pakiety aplikacji sieci web za pomocą usługi czasu wykonywania w obrazie Docker. Dodatek Hello następnie utworzyć obraz powitania, wypchnąć go tooa Docker rejestru i wdrażanie aplikacji sieci web tooyour obraz powitania.

* Wykonaj kroki hello [tutaj](/azure/app-service-web/app-service-linux-how-to-create-web-app) toocreate jako aplikacji sieci Web Azure z systemem Linux.
* Zainstaluj Docker na wystąpienie Wpięć, wykonując instrukcje hello na tym [artykułu](https://docs.docker.com/engine/installation/linux/ubuntu/).
* Tworzenie rejestru kontenera w hello portalu Azure za pomocą kroków hello [tutaj](/azure/container-registry/container-registry-get-started-azure-cli).
* W hello sam [prostej aplikacji sieci Web Java na platformie Azure](https://github.com/azure-devops/javawebappsample) repozytorium rozwidlone, Edytuj hello **Jenkinsfile2** pliku:
    * Wiersz 18-21, odpowiednio zaktualizować toohello nazwy grupy zasobów, aplikacji sieci web i ACR. 
        ```
        def webAppResourceGroup = '<myResourceGroup>'
        def webAppName = '<app_name>'
        def acrName = '<myRegistry>'
        ```

    * Wiersz 24, aktualizacja \<azsrvprincipal\> tooyour identyfikator poświadczeń
        ```
        withCredentials([azureServicePrincipal('<mySrvPrincipal>')]) {
        ```

* Utwórz nowy potok Wpięć tak samo jak w przypadku wdrażania aplikacji sieci web tooAzure w systemie Windows, ten czas, użyj **Jenkinsfile2** zamiast tego.
* Uruchom nowe zadanie.
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
W tym samouczku należy skonfigurować Wpięć potok, który umożliwia wyewidencjonowanie hello kodu źródłowego w repozytorium GitHub. Uruchamia Maven toobuild plik war, a następnie używa tooAzure toodeploy interfejsu wiersza polecenia Azure App Service. W tym samouczku omówiono:

> [!div class="checklist"]
> * Tworzenie maszyny Wirtualnej z Wpięć
> * Skonfiguruj Wpięć
> * Tworzenie aplikacji sieci web na platformie Azure
> * Przygotowanie repozytorium GitHub
> * Tworzenie potoku Wpięć
> * Należy uruchomić potoku hello i sprawdzić hello aplikacji sieci web
