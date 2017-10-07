---
title: aaaBuild hiperskali aplikacji na platformie Azure | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak toomaximize różnych usług Azure toouse hello wydajności aplikacji platformy ASP.NET na platformie Azure."
services: app-service\web
documentationcenter: dotnet
author: cephalin
manager: erikre
editor: 
ms.assetid: a4d49ac7-0f97-4997-84c5-cdb9c4465757
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 03/23/2017
ms.author: cephalin
ms.openlocfilehash: 7952647b49a82c286c6a737eb41a7f23a13fd75e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-hyper-scale-web-app-in-azure"></a>Tworzenie aplikacji sieci web w hiperskali na platformie Azure

Ten samouczek pokazuje, jak żądania tooscale limit aplikacji sieci web platformy ASP.NET w Azure toomaximize użytkownika.

Przed rozpoczęciem tego samouczka, upewnij się, że [hello wiersza polecenia platformy Azure jest instalowany](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) na tym komputerze. Ponadto należy [programu Visual Studio](https://www.visualstudio.com/vs/) na komputerze lokalnym toorun hello przykładowej aplikacji.

## <a name="step-1---get-sample-application"></a>Krok 1 - Get przykładowej aplikacji
Ten krok służy do konfigurowania projektu programu ASP.NET lokalne powitania.

### <a name="clone-hello-application-repository"></a>Repozytorium aplikacji hello w klonowania

Witaj Otwórz terminal wiersza polecenia dowolnego i `CD` tooa katalog roboczy. Następnie hello uruchom następujące polecenia tooclone hello przykładowej aplikacji. 

```powershell
git clone https://github.com/cephalin/HighScaleApp.git
```

### <a name="run-hello-sample-application-in-visual-studio"></a>Uruchom hello przykładowej aplikacji w programie Visual Studio

Otwórz rozwiązanie hello w programie Visual Studio.

```powershell
cd HighScaleApp
.\HighScaleApp.sln
```

Typ `F5` toorun hello aplikacji.

Tej przykładowej aplikacji sieci web ASP.NET pochodzi z hello domyślny szablon i będzie się powtarzał użytkownika sesji i używa hello wyjściowej pamięci podręcznej. Spójrz na `HighScaleApp\Controllers\HomeController.cs`. Witaj `Index()` metoda dodaje część danych toohello sesji.

```csharp
Session.Add("visited", "true"); 
```

I hello `About()` i `Contact()` ich dane wyjściowe pamięci podręcznej metody.

```csharp
[OutputCache(Duration = 60)]
```

## <a name="step-2---deploy-tooazure"></a>Krok 2 — wdrażanie tooAzure
W tym kroku możesz utworzyć aplikację sieci web platformy Azure i wdrażać tooit aplikacji ASP.NET z przykładowych.

### <a name="create-a-resource-group"></a>Tworzenie grupy zasobów   
Użyj [Tworzenie grupy az](https://docs.microsoft.com/cli/azure/group#create) toocreate [grupy zasobów](../azure-resource-manager/resource-group-overview.md) w regionie Europy Zachodniej hello. Grupa zasobów to, gdzie możesz umieścić wszystkie hello zasobów platformy Azure, które mają toomanage ze sobą, takie jak zaplecza hello aplikacji sieci web i wszystkie bazy danych SQL.

```azurecli
az group create --location "West Europe" --name myResourceGroup
```

toosee jakie możliwe wartości można użyć dla `---location`, użyj hello [appservice az listy lokalizacje](https://docs.microsoft.com/en-us/cli/azure/appservice#list-locations) polecenia.

### <a name="create-an-app-service-plan"></a>Tworzenie planu usługi App Service
Użyj [Tworzenie planu usług aplikacji az](https://docs.microsoft.com/en-us/cli/azure/appservice/plan#create) toocreate "B1" [planu usługi aplikacji](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md). 

```azurecli
az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --sku B1
```

Plan usługi aplikacji jest jednostki skalowania, która może zawierać dowolną liczbę aplikacje mają tooscale w górę, lub limit razem w hello sam infrastruktury usługi aplikacji. Każdy plan jest również przypisany [warstwy cenowej](https://azure.microsoft.com/en-us/pricing/details/app-service/). Wyższych warstw obejmują lepsze sprzętu i więcej funkcji, takich jak więcej wystąpień skalowalnego w poziomie.

W tym samouczku B1 jest hello minimalna warstwy, która umożliwia skalowanie w poziomie toothree wystąpień. Aplikację można zawsze przeniesienie w górę lub w dół hello warstwy cenowej później, uruchamiając [aktualizacji planu usługi aplikacji az](https://docs.microsoft.com/cli/azure/appservice/plan#update). 

### <a name="create-a-web-app"></a>Tworzenie aplikacji sieci Web
Użyj [utworzyć az appservice web](https://docs.microsoft.com/en-us/cli/azure/appservice/web#create) toocreate aplikacji sieci web o unikatowej nazwie w `$appName`.

```azurecli
$appName = "<replace-with-a-unique-name>"
az appservice web create --name $appName --resource-group myResourceGroup --plan myAppServicePlan
```

### <a name="set-deployment-credentials"></a>Konfigurowanie poświadczeń wdrożenia
Użyj [az usługi aplikacji sieci web wdrożenia użytkownika zestaw](https://docs.microsoft.com/en-us/cli/azure/appservice/web/deployment/user#set) tooset wdrożenia poziomie konta poświadczeń dla usługi aplikacji.

```azurecli
az appservice web deployment user set --user-name <letters-numbers> --password <mininum-8-char-captital-lowercase-letters-numbers>
```

### <a name="configure-git-deployment"></a>Konfigurowanie wdrożenia Git
Użyj [kontroli źródła sieci web az appservice — config lokalnych git](https://docs.microsoft.com/en-us/cli/azure/appservice/web/source-control#config-local-git) tooconfigure lokalnego wdrożenia usługi Git.

```azurecli
az appservice web source-control config-local-git --name $appName --resource-group myResourceGroup
```

To polecenie umożliwia skorzystanie z danych wyjściowych, która wygląda hello:

```json
{
  "url": "https://user123@myuniqueappname.scm.azurewebsites.net/myuniqueappname.git"
}
```

Użyj hello zwrócił tooconfigure adresu URL programu Git zdalnego. Witaj następujące polecenie używa hello poprzedzających przykład danych wyjściowych.

```powershell
git remote add azure https://user123@myuniqueappname.scm.azurewebsites.net/myuniqueappname.git
```

### <a name="deploy-hello-sample-application"></a>Wdrażanie hello przykładowej aplikacji
Użytkownik jest teraz gotowy toodeploy przykładowej aplikacji. Uruchom polecenie `git push`.

```powershell
git push azure master
```

Po wyświetleniu monitu o hasło, należy użyć hasła hello, określona w momencie uruchomienia `az appservice web deployment user set`.

### <a name="browse-tooazure-web-app"></a>Przeglądaj tooAzure aplikacji sieci web
Użyj [przeglądania sieci web appservice az](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse) toosee aplikację działającą na platformie Azure, uruchom to polecenie.

```azurecli
az appservice web browse --name $appName --resource-group myResourceGroup
```

## <a name="step-3---connect-tooredis"></a>Krok 3 — Połącz tooRedis
W tym kroku można skonfigurować pamięć podręczna Redis Azure jako aplikacja sieci web platformy Azure tooyour zewnętrznych, wspólnie przechowywane pamięci podręcznej. Redis toocache można szybko wykorzystywać dane wyjściowe strony. Ponadto, gdy użytkownik skalowanie aplikacji sieci web później, Redis pomaga utrwalić sesje użytkowników na wielu wystąpień niezawodnie.

### <a name="create-an-azure-redis-cache"></a>Tworzenie usługi Azure Redis Cache
Użyj [Tworzenie pamięci podręcznej redis az](https://docs.microsoft.com/en-us/cli/azure/redis#create) pamięci podręcznej Redis Azure toocreate i Zapisz hello dane wyjściowe JSON. Użyj unikatowej nazwy w `$cacheName`.

```powershell
$cacheName = "<replace-with-a-unique-cache-name>"
$redis = (az redis create --name $cacheName --resource-group myResourceGroup --location "West Europe" --sku-capacity 0 --sku-family C --sku-name Basic | ConvertFrom-Json)
```

### <a name="configure-hello-application-toouse-redis"></a>Skonfiguruj toouse aplikacji hello Redis
Format hello parametry połączenia dla pamięci podręcznej.

```powershell
$connstring = "$($redis.hostname):$($redis.sslPort),password=$($redis.accessKeys.primaryKey),ssl=True,abortConnect=False"
$connstring 
```

drugi wiersz Hello powinien zapewnić wyjścia, który wygląda następująco:

```
mycachename.redis.cache.windows.net:6380,password=/rQP/TLz1mrEPpmh9b/gnfns/t9vBRXqXn3i1RwBjGA=,ssl=True,abortConnect=False
```

W programie Visual Studio, Utwórz plik konfiguracji sieci web w katalogu głównym projektu o nazwie `redis.config` i Wklej hello następującego kodu do niego. W `value`, użyj parametrów połączenia hello z hello dane wyjściowe programu PowerShell.

```xml
<appSettings>
  <add key="RedisConnection" value="your-azure-redis-cache-connection-string"/>
</appSettings>
```

Jeśli przyjrzymy się hello `.gitignore` plik w repozytorium Git, zobaczysz, że ten plik jest wyłączone z kontroli źródła. W ten sposób poufne informacje były bezpieczne. 

Otwórz `Web.config`. Powiadomienie hello `<appSettings file="redis.config">` element, który pobiera ustawienie hello utworzony w `redis.config`. 

Znajdź hello oznaczone jako sekcja zawierająca `<sessionState>` i `<caching>`. Usuń znaczniki komentarza w tej sekcji.

![](./media/app-service-web-tutorial-hyper-scale-app/redisproviders.png)

Ten kod wyszukuje ciąg połączenia Redis hello zdefiniowanego w `RedisConnection`. 

Teraz aplikacja korzysta z pamięci podręcznej Redis toomanage sesji i buforowania. Typ `F5` toorun hello aplikacji. Jeśli chcesz możesz pobrać Redis zarządzania klienta toovisualize hello danych zapisywanych teraz toohello pamięci podręcznej.

### <a name="configure-hello-connection-string-in-azure"></a>Konfigurowanie parametrów połączenia hello na platformie Azure

Dla twojej aplikacji toowork na platformie Azure, trzeba tooconfigure hello tych samych parametrach połączenia Redis w aplikacji sieci web platformy Azure. Ponieważ `redis.config` nie są przechowywane w kontroli źródła, nie jest wdrożony tooAzure po uruchomieniu wdrożenia usługi Git.

Użyj [zaktualizować az usługi aplikacji sieci web config appsettings](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update) tooadd hello parametrów połączenia z hello sama nazwa (`RedisConnection`).

AZ usługi aplikacji sieci web config appsettings zaktualizować — ustawienia "RedisConnection = $connstring"--name $appName — myResourceGroup grupy zasobów

Należy pamiętać, że `$connstring` zawiera hello sformatowany ciąg połączenia.

### <a name="redeploy-hello-application-tooazure"></a>Należy ponownie wdrożyć tooAzure aplikacji hello
Użyj toopush polecenia Git tooAzure Twoje zmiany

```bash
git add .
git commit -m "now use Redis providers"
git push azure master
```

Po wyświetleniu monitu o hasło, należy użyć hasła hello, określona w momencie uruchomienia `az appservice web deployment user set`.

### <a name="browse-toohello-azure-web-app"></a>Przeglądaj toohello aplikacji sieci web Azure
Użyj [przeglądania sieci web appservice az](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse) toosee hello zmiany wprowadzone w systemie Azure.

```azurecli
az appservice web browse --name $appName --resource-group myResourceGroup
```

## <a name="step-4---scale-toomultiple-instances"></a>Krok 4 — wystąpień toomultiple skali
plan usługi aplikacji Hello jest hello jednostką skalowania dla aplikacji sieci web platformy Azure. tooscale limit aplikacji sieci web, można skalować hello planu usługi aplikacji.

Użyj [aktualizacji planu usługi aplikacji az](https://docs.microsoft.com/cli/azure/appservice/plan#update) tooscale limit hello wystąpieniach toothree planu usługi aplikacji, która jest hello maksymalnej liczby dozwolonej przez hello B1 warstwy cenowej. Należy pamiętać, że B1 jest hello utworzenia hello wcześniej planu usługi aplikacji — warstwa wybraną warstwę cenową. 

```azurecli
az appservice plan update --name myAppServicePlan --resource-group myResourceGroup --number-of-workers 3 
```

## <a name="step-5---scale-geographically"></a>Krok 5 — skali geograficznie
Skalowanie geograficznie, możesz uruchomić aplikację w wielu regionach hello chmury Azure. Ten Instalator zrównoważenie obciążenia aplikacji dalsze oparte na lokalizacji geograficznej i zmniejsza czas odpowiedzi hello przez umieszczenie przeglądarek tooclient bliżej aplikacji.

W tym kroku skalować ASP.NET web app tooa drugi regionu z [usługi Azure Traffic Manager](https://docs.microsoft.com/en-us/azure/traffic-manager/). Na końcu hello hello krok będziesz mieć aplikację sieci web uruchomione w Europie zachodnie (już utworzone) i aplikacji sieci web uruchomionych w Azji Południowo-Wschodnia (jeszcze nie utworzono). Obie aplikacje zostanie obsłużona z hello sam adres URL Menedżera ruchu.

### <a name="scale-up-hello-europe-app-toostandard-tier"></a>Skalowanie w górę hello Europy aplikacji tooStandard warstwy
W usłudze App Service Integracja z usługą Azure Traffic Manager wymaga warstwy cenowej standardowa hello. Użyj [aktualizacji planu usługi aplikacji az](https://docs.microsoft.com/cli/azure/appservice/plan#update) tooscale się z tooS1 planu usługi aplikacji. 

```azurecli
az appservice plan update --name myAppServicePlan --resource-group myResourceGroup --sku S1
```
### <a name="create-a-traffic-manager-profile"></a>Tworzenie profilu usługi Traffic Manager 
Użyj [Tworzenie profilu Menedżera ruchu sieciowego az](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#create) toocreate Traffic Manager profilu i dodaj go tooyour grupy zasobów. Użyj unikatowej nazwy DNS w $dnsName.

```azurecli
$dnsName = "<replace-with-unique-dns-name>"
az network traffic-manager profile create --name myTrafficManagerProfile --resource-group myResourceGroup --routing-method Performance --unique-dns-name $dnsName
```

> [!NOTE]
> `--routing-method Performance`Określa, że ten profil [kieruje użytkownika ruchu toohello najbliższy punkt końcowy](../traffic-manager/traffic-manager-routing-methods.md).

### <a name="get-hello-resource-id-of-hello-europe-app"></a>Pobierz identyfikator zasobu hello hello Europy aplikacji
Użyj [az usługi aplikacji sieci web Pokaż](https://docs.microsoft.com/en-us/cli/azure/appservice/web#show) tooget hello identyfikator zasobu aplikacji sieci web.

```azurecli
$appId = az appservice web show --name $appName --resource-group myResourceGroup --query id --output tsv
```

### <a name="add-a-traffic-manager-endpoint-for-hello-europe-app"></a>Dodawanie punktu końcowego Menedżera ruchu hello Europy aplikacji
Użyj [utworzyć punktu końcowego Menedżera ruchu sieciowego az](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create) tooadd tooyour punktu końcowego profilu Menedżera ruchu i użycia hello identyfikator zasobu aplikacji sieci web jako hello docelowej.

```azurecli
az network traffic-manager endpoint create --name myWestEuropeEndpoint --profile-name myTrafficManagerProfile --resource-group myResourceGroup --type azureEndpoints --target-resource-id $appId
```

### <a name="get-hello-traffic-manager-endpoint-url"></a>Pobierz adres URL punktu końcowego Menedżera ruchu hello
Profil Menedżera ruchu ma punkt końcowy tego istniejącej aplikacji sieci web punktów tooyour. Użyj [Pokaż profil Menedżera ruchu sieciowego az](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#show) tooget adresu URL. 

```azurecli
az network traffic-manager profile show --name myTrafficManagerProfile --resource-group myResourceGroup --query dnsConfig.fqdn --output tsv
```

Kopiuj dane wyjściowe hello w przeglądarce. Aplikacja sieci web powinno zostać wyświetlone ponownie.

### <a name="create-an-azure-redis-cache-in-asia"></a>Tworzenie pamięci podręcznej Azure Redis w Azji
Teraz możesz replikować regionu Azja południowo-wschodnia toohello aplikacji sieci web platformy Azure. toostart, użyj [Tworzenie pamięci podręcznej redis az](https://docs.microsoft.com/en-us/cli/azure/redis#create) toocreate drugi pamięć podręczna Redis Azure w Azji Południowo-Wschodnia. Ta pamięć podręczna musi toobe kolokowane z aplikacją w Azji.

```powershell
$redis = (az redis create --name $cacheName-asia --resource-group myResourceGroup --location "Southeast Asia" --sku-capacity 0 --sku-family C --sku-name Basic | ConvertFrom-Json)
```

`--name $cacheName-asia`zapewnia hello nazwę hello pamięci podręcznej hello pamięci podręcznej Europa Zachodnia, z hello `-asia` sufiks.

### <a name="create-an-app-service-plan-in-asia"></a>Tworzenie planu usługi App Service w Azji
Użyj [Tworzenie planu usług aplikacji az](https://docs.microsoft.com/cli/azure/appservice/plan#create) toocreate drugi usługi aplikacji plan hello regionu Azja południowo-wschodnia, przy użyciu hello S1 tej samej warstwie jako hello plan Europa Zachodnia.

```azurecli
az appservice plan create --name myAppServicePlanAsia --resource-group myResourceGroup --location "Southeast Asia" --sku S1
```

### <a name="create-a-web-app-in-asia"></a>Tworzenie aplikacji sieci web w Azji
Użyj [utworzyć az appservice web](https://docs.microsoft.com/en-us/cli/azure/appservice/web#create) toocreate drugi aplikacji sieci web.

```azurecli
az appservice web create --name $appName-asia --resource-group myResourceGroup --plan myAppServicePlanAsia
```

`--name $appName-asia`zapewnia hello nazwa hello aplikacji hello aplikacji Europa Zachodnia, z hello `-asia` sufiks.

### <a name="configure-hello-connection-string-for-redis"></a>Konfigurowanie parametrów połączenia powitania dla pamięci podręcznej Redis
Użyj [zaktualizować az usługi aplikacji sieci web config appsettings](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update) tooadd toohello sieci web aplikacji hello ciąg połączenia dla hello Azja południowo-wschodnia pamięci podręcznej.

AZ usługi aplikacji sieci web config appsettings zaktualizować — ustawienia "RedisConnection = $($redis.hostname): $($redis.sslPort), hasło = $($redis.accessKeys.primaryKey), ssl = True, abortConnect = False"--name $appName — Azja--myResourceGroup grupy zasobów

### <a name="configure-git-deployment-for-hello-asia-app"></a>Konfiguruj wdrożenie Git dla aplikacji Azja hello.
Użyj [kontroli źródła sieci web az appservice — config lokalnych git](https://docs.microsoft.com/en-us/cli/azure/appservice/web/source-control#config-local-git) tooconfigure lokalnego wdrożenia Git dla aplikacji sieci web drugi hello.

```azurecli
az appservice web source-control config-local-git --name $appName-asia --resource-group myResourceGroup
```

To polecenie umożliwia skorzystanie z danych wyjściowych, która wygląda hello:

```json
{
  "url": "https://user123@myuniqueappname-asia.scm.azurewebsites.net/myuniqueappname.git"
}
```

Użyj hello zwrócił tooconfigure adres URL drugi Git dla lokalnego repozytorium zdalnego. Witaj następujące polecenie używa hello poprzedzających przykład danych wyjściowych.

```bash
git remote add azure-asia https://user123@myuniqueappname-asia.scm.azurewebsites.net/myuniqueappname.git
```

### <a name="deploy-your-sample-application"></a>Wdrażanie przykładowej aplikacji
Uruchom `git push` toodeploy Twojego drugi zdalnego Git przykładowej aplikacji toohello. 

```bash
git push azure-asia master
```

Po wyświetleniu monitu o hasło, należy użyć hasła hello, określona w momencie uruchomienia `az appservice web deployment user set`.

### <a name="browse-toohello-asia-app"></a>Przeglądaj toohello Azja aplikacji
Użyj [przeglądania sieci web appservice az](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse) tooverify, że aplikacja działa na żywo na platformie Azure.

```azurecli
az appservice web browse --name $appName-asia --resource-group myResourceGroup
```

### <a name="get-hello-resource-id-of-hello-asia-app"></a>Pobierz identyfikator zasobu hello hello Azja aplikacji
Użyj [az usługi aplikacji sieci web Pokaż](https://docs.microsoft.com/en-us/cli/azure/appservice/web#show) tooget hello identyfikator zasobu aplikacji sieci web w Azji Południowo-Wschodnia.

```azurecli
$appIdAsia = az appservice web show --name $appName-asia --resource-group myResourceGroup --query id --output tsv
```

### <a name="add-a-traffic-manager-endpoint-for-hello-asia-app"></a>Dodawanie punktu końcowego Menedżera ruchu hello Azja aplikacji
Użyj [utworzyć punktu końcowego Menedżera ruchu sieciowego az](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create) tooadd drugi toohello punktu końcowego profilu Menedżera ruchu.

```azurecli
az network traffic-manager endpoint create --name myAsiaEndpoint --profile-name myTrafficManagerProfile --resource-group myResourceGroup --type azureEndpoints --target-resource-id $appIdAsia
```

### <a name="add-region-identifier-tooweb-apps"></a>Dodawanie aplikacji tooweb identyfikator regionu
Użyj [zaktualizować az usługi aplikacji sieci web config appsettings](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update) tooadd zmienną środowiskową określonego regionu.

```azurecli
az appservice web config appsettings update --settings "Region=West Europe" --name $appName --resource-group myResourceGroup
az appservice web config appsettings update --settings "Region=Southeast Asia" --name $appName-asia --resource-group myResourceGroup
```

Kod aplikacji już używa tego ustawienia aplikacji. Spójrz na `HighScaleApp\Views\Home\Index.cshtml`.

### <a name="complete"></a>Zakończenie!

Teraz spróbuj tooaccess hello adres URL profilu Menedżera ruchu z przeglądarek w różnych regionach geograficznych. Przeglądarka klienta z Europy powinny być widoczne "Europa Zachodnia ASP.NET" i "Azja południowo-wschodnia ASP.NET." powinny być widoczne w przeglądarce klienta z Azja

## <a name="more-resources"></a>Więcej zasobów
