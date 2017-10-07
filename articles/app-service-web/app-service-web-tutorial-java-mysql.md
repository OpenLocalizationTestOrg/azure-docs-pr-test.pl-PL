---
title: aaaBuild aplikacji sieci web Java i MySQL na platformie Azure
description: "Dowiedz się, jak tooget aplikacji Java łączące usługi baza danych MySQL na platformie Azure toohello pracy usługi aplikacji Azure."
services: app-service\web
documentationcenter: Java
author: bbenz
manager: jeffsand
editor: jasonwhowell
ms.assetid: 
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: tutorial
ms.date: 05/22/2017
ms.author: bbenz
ms.custom: mvc
ms.openlocfilehash: 0820ee9c2b7bf8fcaa22287c27a7ab848a1c4927
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-java-and-mysql-web-app-in-azure"></a>Tworzenie aplikacji sieci web Java i MySQL na platformie Azure

Ten samouczek pokazuje, jak toocreate Java sieci web aplikacji na platformie Azure i podłącz go tooa baza danych MySQL. Po zakończeniu, konieczne będzie [Spring rozruchu](https://projects.spring.io/spring-boot/) przechowywania danych w aplikacji [bazy danych Azure dla programu MySQL](https://docs.microsoft.com/azure/mysql/overview) systemem [aplikacji sieci Web usługi aplikacji Azure](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview).

![Aplikacja Java w usługi aplikacji Azure](./media/app-service-web-tutorial-java-mysql/appservice-web-app.png)

Ten samouczek zawiera informacje na temat wykonywania następujących czynności:

> [!div class="checklist"]
> * Utwórz bazę danych MySQL na platformie Azure
> * Połącz toohello aplikację przykładową bazę danych
> * Wdrażanie tooAzure aplikacji hello
> * Aktualizowanie i wdrożenie aplikacji hello
> * Strumieniowe przesyłanie dzienników diagnostycznych z platformy Azure
> * Monitorowanie aplikacji hello w hello portalu Azure


## <a name="prerequisites"></a>Wymagania wstępne

1. [Pobierz i zainstaluj oprogramowanie Git](https://git-scm.com/)
1. [Pobierz i zainstaluj hello Java 7 JDK lub nowszy](http://www.oracle.com/technetwork/java/javase/downloads/index.html)
1. [Pobierz, zainstaluj i uruchom MySQL](https://dev.mysql.com/doc/refman/5.7/en/installing.html) 

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

Jeśli wybierz tooinstall i użyj interfejsu wiersza polecenia hello lokalnie, w tym temacie wymaga, że uruchamiasz hello Azure CLI w wersji 2.0 lub nowszej. Uruchom `az --version` toofind hello wersji. Jeśli potrzebujesz tooinstall lub uaktualniania, zobacz [zainstalować Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="prepare-local-mysql"></a>Przygotowywanie lokalnej MySQL 

W tym kroku utworzysz bazę danych w lokalnym serwerze MySQL do użycia w przypadku testowania aplikacji hello lokalnie na komputerze.

### <a name="connect-toomysql-server"></a>Połącz serwer tooMySQL

W oknie terminalu Połącz tooyour lokalny serwer MySQL. Wszystkie polecenia hello toorun to okno terminalu można użyć w tym samouczku.

```bash
mysql -u root -p
```

Jeśli zostanie wyświetlony monit o podanie hasła, wprowadź hasło hello hello `root` konta. Jeśli nie pamiętasz hasła do konta głównego, zobacz [MySQL: jak tooReset hello hasła użytkownika Root](https://dev.mysql.com/doc/refman/5.7/en/resetting-permissions.html).

Jeśli polecenie zostanie wykonane pomyślnie, na serwerze MySQL już jest uruchomiona. Jeśli nie, upewnij się, że serwera lokalnego MySQL została uruchomiona z następujących hello [MySQL poinstalacyjne czynności](https://dev.mysql.com/doc/refman/5.7/en/postinstallation.html).

### <a name="create-a-database"></a>Tworzenie bazy danych 

W hello `mysql` należy utworzyć bazę danych i tabeli dla hello elementów do wykonania.

```sql
CREATE DATABASE tododb;
```

Zakończyć połączenie z serwerem, wpisując `quit`.

```sql
quit
```

## <a name="create-and-run-hello-sample-app"></a>Tworzenie i uruchamianie hello przykładowej aplikacji 

W tym kroku sklonować przykładowej aplikacji rozruchu Spring, skonfiguruj ją toouse hello lokalnej bazy danych MySQL i uruchom go na komputerze. 

### <a name="clone-hello-sample"></a>Przykład Witaj klonowania

Hello okno terminalu Przejdź tooa pracy katalogu i klonowania repozytorium przykładowej hello. 

```bash
git clone https://github.com/azure-samples/mysql-spring-boot-todo
```

### <a name="configure-hello-app-toouse-hello-mysql-database"></a>Skonfiguruj bazę danych MySQL hello hello aplikacji toouse

Aktualizacja hello `spring.datasource.password` i wartość w *spring-boot-mysql-todo/src/main/resources/application.properties* z hello tego samego hasła głównego używany tooopen hello MySQL wiersz:

```
spring.datasource.password=mysqlpass
```

### <a name="build-and-run-hello-sample"></a>Tworzenie i uruchamianie przykładowych hello

Tworzenie i uruchamianie przykładowych hello przy użyciu otoki Maven hello zawarte w repozytorium hello:

```bash
cd spring-boot-mysql-todo
mvnw package spring-boot:run
```

Otwórz toosee toohttp://localhost:8080 Twojego przeglądarki w przykładowym hello w akcji. Podczas dodawania listy toohello zadań, użyj hello SQL następujące polecenia w hello MySQL monitu tooview hello danych przechowywanych w MySQL.

```SQL
use testdb;
select * from todo_item;
```

Zatrzymywanie aplikacji hello za pomocą `Ctrl` + `C` w hello terminala. 

## <a name="create-an-azure-mysql-database"></a>Utwórz bazę danych MySQL na platformie Azure

W tym kroku utworzysz [bazy danych Azure dla programu MySQL](../mysql/quickstart-create-mysql-server-database-using-azure-cli.md) wystąpienia przy użyciu hello [interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/install-azure-cli). Należy skonfigurować hello przykładowej aplikacji toouse tej bazy danych później w samouczku hello.

Użyj hello Azure CLI 2.0 w zasobach hello toocreate okno terminalu potrzebne toohost aplikacji Java w usługi aplikacji Azure. Zaloguj się za tooyour subskrypcji platformy Azure z hello [logowania az](/cli/azure/#login) poleceń i wykonaj hello wyświetlanymi instrukcjami. 

```azurecli-interactive 
az login 
```   

### <a name="create-a-resource-group"></a>Tworzenie grupy zasobów

Utwórz [grupy zasobów](../azure-resource-manager/resource-group-overview.md) z hello [Tworzenie grupy az](/cli/azure/group#create) polecenia. Grupy zasobów platformy Azure jest kontenerem logicznym, w której wdrożone i zarządzane zasoby pokrewne, takie jak aplikacje sieci web, baz danych i konta magazynu. 

Witaj poniższy przykład tworzy grupę zasobów w regionie Europa Północna, Europa hello:

```azurecli-interactive
az group create --name myResourceGroup --location "North Europe"
```    

toosee hello możliwe wartości można użyć dla `--location`, użyj hello [appservice az listy lokalizacje](/cli/azure/appservice#list-locations) polecenia.

### <a name="create-a-mysql-server"></a>Utwórz serwer MySQL

Utwórz serwer bazy danych Azure dla programu MySQL (wersja zapoznawcza) z hello [utworzenie przez serwer mysql az](/cli/azure/mysql/server#create) polecenia.    
Podstawić własną unikatową nazwę serwera MySQL, której występuje hello `<mysql_server_name>` symbolu zastępczego. Ta nazwa jest częścią nazwy hosta serwera MySQL, `<mysql_server_name>.mysql.database.azure.com`, dlatego toobe potrzebuje globalnie unikatowe. Zamienić `<admin_user>` i `<admin_password>` z własne wartości.

```azurecli-interactive
az mysql server create --name <mysql_server_name> \ 
    --resource-group myResourceGroup \ 
    --location "North Europe" \
    --admin-user <admin_user> \ 
    --admin-password <admin_password>
```

Po utworzeniu serwer MySQL hello hello Azure CLI pokazuje informacje toohello podobnie poniższy przykład:

```json
{
  "administratorLogin": "admin_user",
  "administratorLoginPassword": null,
  "fullyQualifiedDomainName": "mysql_server_name.mysql.database.azure.com",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.DBforMySQL/servers/mysql_server_name",
  "location": "northeurope",
  "name": "mysql_server_name",
  "resourceGroup": "mysqlJavaResourceGroup",
  ...
  < Output has been truncated for readability >
}
```

### <a name="configure-server-firewall"></a>Konfigurowanie zapory serwera

Tworzenie reguły zapory klienta MySQL serwera tooallow połączeń przy użyciu hello [az mysql reguły zapory serwera — Utwórz](/cli/azure/mysql/server/firewall-rule#create) polecenia. 

```azurecli-interactive
az mysql server firewall-rule create \
    --name allIPs \
    --server <mysql_server_name>  \ 
    --resource-group myResourceGroup \ 
    --start-ip-address 0.0.0.0 \ 
    --end-ip-address 255.255.255.255
```

> [!NOTE]
> Bazy danych platformy Azure dla programu MySQL (wersja zapoznawcza) nie obsługuje obecnie automatycznie połączenia z usługami Azure. Adresy IP na platformie Azure są przypisywane dynamicznie, jest lepsze tooenable wszystkie adresy IP dla teraz. Jak usługa hello kontynuuje jej podgląd, lepiej metody zabezpieczania bazy danych zostanie włączona.

## <a name="configure-hello-azure-mysql-database"></a>Skonfiguruj bazę danych MySQL na platformie Azure hello

W hello okno terminalu na komputerze nawiąż połączenie toohello serwer MySQL na platformie Azure. Użyj wartości hello wcześniej określona dla `<admin_user>` i `<mysql_server_name>`.

```bash
mysql -u <admin_user>@<mysql_server_name> -h <mysql_server_name>.mysql.database.azure.com -P 3306 -p
```

### <a name="create-a-database"></a>Tworzenie bazy danych 

W hello `mysql` należy utworzyć bazę danych i tabeli dla hello elementów do wykonania.

```sql
CREATE DATABASE tododb;
```

### <a name="create-a-user-with-permissions"></a>Utwórz użytkownika z uprawnieniami

Tworzenie użytkownika bazy danych i nadaj mu wszystkie uprawnienia w hello `tododb` bazy danych. Zastąp symbole zastępcze hello `<Javaapp_user>` i `<Javaapp_password>` z własnych unikatowej nazwy aplikacji.

```sql
CREATE USER '<Javaapp_user>' IDENTIFIED BY '<Javaapp_password>'; 
GRANT ALL PRIVILEGES ON tododb.* too'<Javaapp_user>';
```

Zakończyć połączenie z serwerem, wpisując `quit`.

```sql
quit
```

## <a name="deploy-hello-sample-tooazure-app-service"></a>Wdrażanie hello próbki tooAzure usługi aplikacji

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

### <a name="configure-hello-app-toouse-hello-azure-sql-database"></a>Konfigurowanie bazy danych Azure SQL hello toouse aplikacji hello

Przed uruchomieniem hello Przykładowa aplikacja, ustawienia aplikacji na powitania sieci web aplikacji toouse hello Azure baza danych MySQL utworzonej w usłudze Azure. Te właściwości są uwidocznione toohello aplikacji sieci web jako zmienne środowiskowe i Zastąp wartości hello application.properties hello wewnątrz aplikacji sieci web spakowanych hello. 

Ustawienia aplikacji przy użyciu [appsettings konfiguracji aplikacji sieci Web az](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings) w hello interfejsu wiersza polecenia:

```azurecli-interactive
az webapp config appsettings set \
    --settings SPRING_DATASOURCE_URL="jdbc:mysql://<mysql_server_name>.mysql.database.azure.com:3306/tododb?verifyServerCertificate=true&useSSL=true&requireSSL=false" \
    --resource-group myResourceGroup \
    --name <app_name>
```

```azurecli-interactive
az webapp config appsettings set \
    --settings SPRING_DATASOURCE_USERNAME=Javaapp_user@mysql_server_name  \
    --resource-group myResourceGroup \ 
    --name <app_name>
```

```azurecli-interactive
az webapp config appsettings set \
    --settings SPRING_DATASOURCE_URL=Javaapp_password \
    --resource-group myResourceGroup \ 
    --name <app_name>
```

### <a name="get-ftp-deployment-credentials"></a>Uzyskiwanie poświadczeń wdrożenia FTP 
Można wdrożyć z appservice tooAzure aplikacji na różne sposoby, w tym FTP, lokalne Git GitHub, Visual Studio Team Services i BitBucket. W tym przykładzie FTP toodeploy hello. Plik WAR utworzony wcześniej na tooAzure Twojego komputera lokalnego usługi aplikacji.

toodetermine co toopass wzdłuż w ftp polecenia toohello aplikacji sieci Web, Użyj poświadczeń [az usługi aplikacji sieci web wdrożenia listy publikowania — profile](https://docs.microsoft.com/cli/azure/appservice/web/deployment#list-publishing-profiles) polecenia: 

```azurecli-interactive
az webapp deployment list-publishing-profiles \ 
    --name <app_name> \ 
    --resource-group myResourceGroup \
    --query "[?publishMethod=='FTP'].{URL:publishUrl, Username:userName,Password:userPWD}" \ 
    --output json
```

```JSON
[
  {
    "Password": "aBcDeFgHiJkLmNoPqRsTuVwXyZ",
    "URL": "ftp://waws-prod-blu-069.ftp.azurewebsites.windows.net/site/wwwroot",
    "Username": "app_name\\$app_name"
  }
]
```

### <a name="upload-hello-app-using-ftp"></a>Przekaż aplikację hello za pomocą protokołu FTP

Użyj ulubionego hello toodeploy narzędzia FTP. Toohello pliku WAR */site/wwwroot/webapps* folderu na pobrane z hello adres serwera hello `URL` w hello poprzednie polecenie. Usuń istniejący katalog domyślny (ROOT) aplikacji hello i Zastąp istniejące ROOT.war z hello hello. Wbudowane hello wcześniej w samouczku hello pliku WAR.

```bash
ftp waws-prod-blu-069.ftp.azurewebsites.windows.net
Connected toowaws-prod-blu-069.drip.azurewebsites.windows.net.
220 Microsoft FTP Service
Name (waws-prod-blu-069.ftp.azurewebsites.windows.net:raisa): app_name\$app_name
331 Password required
Password:
cd /site/wwwroot/webapps
mdelete -i ROOT/*
rmdir ROOT/
put target/TodoDemo-0.0.1-SNAPSHOT.war ROOT.war
```

### <a name="test-hello-web-app"></a>Przetestuj aplikację sieci web hello

Przeglądaj zbyt`http://<app_name>.azurewebsites.net/` i dodaj kilka zadań toohello listy. 

![Aplikacja Java w usługi aplikacji Azure](./media/app-service-web-tutorial-java-mysql/appservice-web-app.png)

**Gratulacje!** Używasz aplikacji Java opartych na danych w usłudze Azure App Service.

## <a name="update-hello-app-and-redeploy"></a>Aktualizacja aplikacji hello i utwórz je ponownie

Zaktualizuj tooinclude aplikacji hello dodatkowe kolumny na liście todo powitania dla elementu hello dzień został utworzony. Spring rozruchu obsługuje aktualizacji schematu bazy danych hello automatycznie jako zmianami modelu danych hello bez zmiany istniejącego rekordy bazy danych.

1. W systemie lokalnym otwarcie *src/main/java/com/example/fabrikam/TodoItem.java* i dodaj następujące hello importuje toohello klasy:   

    ```java
    import java.text.SimpleDateFormat;
    import java.util.Calendar;
    ```

2. Dodaj `String` właściwości `timeCreated` za*src/main/java/com/example/fabrikam/TodoItem.java*, inicjowanie go z sygnaturą czasową podczas tworzenia obiektu. Dodaj metody pobierające/ustawiające hello nowe `timeCreated` właściwości podczas edytowania tego pliku.

    ```java
    private String name;
    private boolean complete;
    private String timeCreated;
    ...

    public TodoItem(String category, String name) {
       this.category = category;
       this.name = name;
       this.complete = false;
       this.timeCreated = new SimpleDateFormat("MMMM dd, YYYY").format(Calendar.getInstance().getTime());
    }
    ...
    public void setTimeCreated(String timeCreated) {
       this.timeCreated = timeCreated;
    }

    public String getTimeCreated() {
        return timeCreated;
    }
    ```

3. Aktualizacja *src/main/java/com/example/fabrikam/TodoDemoController.java* o wiersz w hello `updateTodo` sygnatury czasowej hello tooset metody:

    ```java
    item.setComplete(requestItem.isComplete());
    item.setId(requestItem.getId());
    item.setTimeCreated(requestItem.getTimeCreated());
    repository.save(item);
    ```

4. Dodaj obsługę nowego pola hello hello Thymeleaf szablonu. Aktualizacja *src/main/resources/templates/index.html* z użyciem nowego nagłówka tabeli sygnatury czasowej hello i nową wartość hello toodisplay pola sygnatury czasowej hello w każdym wierszu danych tabeli.

    ```html
    <th>Name</th>
    <th>Category</th>
    <th>Time Created</th>
    <th>Complete</th>
    ...
    <td th:text="${item.category}">item_category</td><input type="hidden" th:field="*{todoList[__${i.index}__].category}"/>
    <td th:text="${item.timeCreated}">item_time_created</td><input type="hidden" th:field="*{todoList[__${i.index}__].timeCreated}"/>
    <td><input type="checkbox" th:checked="${item.complete} == true" th:field="*{todoList[__${i.index}__].complete}"/></td>
    ```

5. Odbuduj aplikacji hello:

    ```bash
    mvnw clean package 
    ```

6. Zaktualizowano hello FTP. WAR jako przed, usunięcie istniejących hello */wwwroot/webapps/katalogu głównego witryny* katalogu i *ROOT.war*, a następnie przekazać zaktualizowany hello. Plik WAR jako ROOT.war. 

Podczas odświeżania aplikacji hello **tworzony** kolumny jest teraz widoczne. Po dodaniu nowego zadania aplikacji hello zostanie automatycznie wypełnić hello sygnatury czasowej. Istniejących zadań pozostają bez zmian i korzystanie z aplikacji hello, mimo że hello podstawowy model danych został zmieniony. 

![Zaktualizowane o nową kolumnę aplikacji Java](./media/app-service-web-tutorial-java-mysql/appservice-updates-java.png)
      
## <a name="stream-diagnostic-logs"></a>Dzienniki diagnostyczne strumienia 

Podczas wykonywania aplikacji Java w usłudze Azure App Service można uzyskać konsoli hello dzienniki przetwarzana potokowo bezpośrednio tooyour terminala. W ten sposób można uzyskać hello tego samego komunikaty diagnostyczne toohelp Debugowanie błędów aplikacji.

Dziennik toostart przesyłania strumieniowego, użyj hello [końcowego fragmentu dziennika aplikacji sieci Web az](/cli/azure/appservice/web/log#tail) polecenia.

```azurecli-interactive 
az webapp log tail \
    --name <app_name> \
    --resource-group myResourceGroup 
``` 

## <a name="manage-your-azure-web-app"></a>Zarządzanie aplikacji sieci web platformy Azure

Przejdź aplikacji sieci web hello toosee portalu Azure toohello, który został utworzony.

toodo, zaloguj się za[https://portal.azure.com](https://portal.azure.com).

W menu po lewej stronie powitania kliknij **usługi aplikacji**, następnie kliknij nazwę hello aplikacji sieci web platformy Azure.

![Aplikacja sieci web tooAzure nawigacji w portalu](./media/app-service-web-tutorial-java-mysql/access-portal.png)

Domyślnie bloku aplikacji sieci web zawiera hello **omówienie** strony. Ta strona udostępnia widok sposobu działania aplikacji. W tym miejscu mogą też wykonywać zadania zarządzania, takie jak zatrzymanie, start, ponowne uruchomienie i usuwania. Hello karty po lewej stronie powitania bloku hello zawierają hello innej konfiguracji stron, które można otworzyć.

![Blok usługi App Service w witrynie Azure Portal](./media/app-service-web-tutorial-java-mysql/web-app-blade.png)

Te karty w bloku hello zawierają hello wiele aplikacji sieci web tooyour można dodać funkcje. powitania po liście oferuje kilka możliwości hello:
* Mapowanie niestandardowej nazwy DNS
* Tworzenie powiązania niestandardowego certyfikatu SSL
* Konfigurowanie ciągłego wdrażania
* Skalowanie w górę i w dół
* Dodawanie uwierzytelniania użytkownika

## <a name="clean-up-resources"></a>Oczyszczanie zasobów

Jeśli nie potrzebujesz tych zasobów innym samouczek (zobacz [następne kroki](#next)), można je usunąć, uruchamiając następujące polecenie hello: 
  
```azurecli-interactive
az group delete --name myResourceGroup 
``` 

<a name="next"></a>

## <a name="next-steps"></a>Następne kroki

> [!div class="checklist"]
> * Utwórz bazę danych MySQL na platformie Azure
> * Połącz próbki toohello aplikacji Java MySQL
> * Wdrażanie tooAzure aplikacji hello
> * Aktualizowanie i wdrożenie aplikacji hello
> * Strumieniowe przesyłanie dzienników diagnostycznych z platformy Azure
> * Zarządzanie aplikacją hello w hello portalu Azure

Przejść dalej toolearn samouczka toohello jak toomap DNS niestandardowej nazwy toohello aplikacji.

> [!div class="nextstepaction"] 
> [Mapowanie istniejących niestandardowe DNS nazwy tooAzure aplikacji sieci Web](app-service-web-tutorial-custom-domain.md)
