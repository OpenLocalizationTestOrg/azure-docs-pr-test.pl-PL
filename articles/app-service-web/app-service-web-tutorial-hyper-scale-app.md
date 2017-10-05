---
title: Tworzenie aplikacji hiperskali na platformie Azure | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak używać różnych usług platformy Azure w celu zwiększenia wydajności aplikacji platformy ASP.NET na platformie Azure."
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
ms.openlocfilehash: eac9c5b0d8d0f7802d88e6f4f27d9d23c406e025
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="build-a-hyper-scale-web-app-in-azure"></a>Tworzenie aplikacji sieci web w hiperskali na platformie Azure

W tym samouczku przedstawiono sposób skalowanie aplikacji sieci web platformy ASP.NET na platformie Azure, aby zmaksymalizować żądania użytkownika.

Przed rozpoczęciem tego samouczka, upewnij się, że [wiersza polecenia platformy Azure jest instalowany](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) na tym komputerze. Ponadto należy [programu Visual Studio](https://www.visualstudio.com/vs/) na komputerze lokalnym, aby uruchomić przykładową aplikację.

## <a name="step-1---get-sample-application"></a>Krok 1 - Get przykładowej aplikacji
Ten krok służy do konfigurowania lokalnego projektu programu ASP.NET.

### <a name="clone-the-application-repository"></a>Klonuj repozytorium aplikacji

Otwórz wybrany terminal wiersza polecenia dowolnego i `CD` do katalogu roboczego. Następnie uruchom następujące polecenia, można sklonować przykładowej aplikacji. 

```powershell
git clone https://github.com/cephalin/HighScaleApp.git
```

### <a name="run-the-sample-application-in-visual-studio"></a>Uruchom przykładową aplikację w programie Visual Studio

Otwórz rozwiązanie w programie Visual Studio.

```powershell
cd HighScaleApp
.\HighScaleApp.sln
```

Typ `F5` do uruchomienia aplikacji.

Tej przykładowej aplikacji sieci web ASP.NET pochodzi z domyślnego szablonu i będzie się powtarzał użytkownika sesji i używa pamięci podręcznej danych wyjściowych. Spójrz na `HighScaleApp\Controllers\HomeController.cs`. `Index()` Metoda dodaje element danych do sesji.

```csharp
Session.Add("visited", "true"); 
```

I `About()` i `Contact()` ich dane wyjściowe pamięci podręcznej metody.

```csharp
[OutputCache(Duration = 60)]
```

## <a name="step-2---deploy-to-azure"></a>Krok 2 — wdrażanie na platformie Azure
W tym kroku możesz utworzyć aplikację sieci web platformy Azure i wdrażać przykładowej aplikacji ASP.NET do niego.

### <a name="create-a-resource-group"></a>Tworzenie grupy zasobów   
Użyj [Tworzenie grupy az](https://docs.microsoft.com/cli/azure/group#create) utworzyć [grupy zasobów](../azure-resource-manager/resource-group-overview.md) w regionie, Europa Zachodnia. Grupa zasobów to, gdzie umieścić wszystkie zasoby platformy Azure, które mają być zarządzane, takie jak zaplecza aplikacji sieci web i wszystkie bazy danych SQL.

```azurecli
az group create --location "West Europe" --name myResourceGroup
```

Aby sprawdzić, jakie możliwe wartości można użyć dla `---location`, użyj [appservice az listy lokalizacje](https://docs.microsoft.com/en-us/cli/azure/appservice#list-locations) polecenia.

### <a name="create-an-app-service-plan"></a>Tworzenie planu usługi App Service
Użyj [Tworzenie planu usług aplikacji az](https://docs.microsoft.com/en-us/cli/azure/appservice/plan#create) można utworzyć "B1" [planu usługi aplikacji](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md). 

```azurecli
az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --sku B1
```

Plan usługi aplikacji jest jednostki skalowania, która może zawierać dowolną liczbę aplikacji, które chcesz skalować w górę lub się ze sobą za pośrednictwem tej samej infrastruktury usługi aplikacji. Każdy plan jest również przypisany [warstwy cenowej](https://azure.microsoft.com/en-us/pricing/details/app-service/). Wyższych warstw obejmują lepsze sprzętu i więcej funkcji, takich jak więcej wystąpień skalowalnego w poziomie.

W tym samouczku B1 jest minimalna warstwę, która umożliwia skalowanie w poziomie do wystąpienia. Zawsze przejściem aplikację w górę lub w dół warstwy cenowej później, uruchamiając [aktualizacji planu usługi aplikacji az](https://docs.microsoft.com/cli/azure/appservice/plan#update). 

### <a name="create-a-web-app"></a>Tworzenie aplikacji sieci Web
Użyj [utworzyć az appservice web](https://docs.microsoft.com/en-us/cli/azure/appservice/web#create) do utworzenia aplikacji sieci web o unikatowej nazwie w `$appName`.

```azurecli
$appName = "<replace-with-a-unique-name>"
az appservice web create --name $appName --resource-group myResourceGroup --plan myAppServicePlan
```

### <a name="set-deployment-credentials"></a>Konfigurowanie poświadczeń wdrożenia
Użyj [az usługi aplikacji sieci web wdrożenia użytkownika zestaw](https://docs.microsoft.com/en-us/cli/azure/appservice/web/deployment/user#set) można ustawić poświadczenia wdrażania na poziomie konta usługi aplikacji.

```azurecli
az appservice web deployment user set --user-name <letters-numbers> --password <mininum-8-char-captital-lowercase-letters-numbers>
```

### <a name="configure-git-deployment"></a>Konfigurowanie wdrożenia Git
Użyj [kontroli źródła sieci web az appservice — config lokalnych git](https://docs.microsoft.com/en-us/cli/azure/appservice/web/source-control#config-local-git) do konfigurowania lokalnego wdrożenia usługi Git.

```azurecli
az appservice web source-control config-local-git --name $appName --resource-group myResourceGroup
```

To polecenie umożliwia wyjścia, który wygląda następująco:

```json
{
  "url": "https://user123@myuniqueappname.scm.azurewebsites.net/myuniqueappname.git"
}
```

Umożliwia skonfigurowanie programu Git zdalnego zwrócony adres URL. Polecenie używa w poprzednim przykładzie danych wyjściowych.

```powershell
git remote add azure https://user123@myuniqueappname.scm.azurewebsites.net/myuniqueappname.git
```

### <a name="deploy-the-sample-application"></a>Wdrażanie przykładowej aplikacji
Teraz można przystąpić do wdrażania aplikacji przykładowej. Uruchom polecenie `git push`.

```powershell
git push azure master
```

Po wyświetleniu monitu o hasło, należy użyć hasła określonej w momencie uruchomienia `az appservice web deployment user set`.

### <a name="browse-to-azure-web-app"></a>Przejdź do aplikacji sieci web Azure
Użyj [przeglądania sieci web appservice az](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse) Aby wyświetlić aplikację działającą na platformie Azure, uruchom następujące polecenie.

```azurecli
az appservice web browse --name $appName --resource-group myResourceGroup
```

## <a name="step-3---connect-to-redis"></a>Krok 3 — nawiązać połączenia z pamięci podręcznej Redis
W tym kroku możesz skonfigurować pamięć podręczna Redis Azure jako zewnętrznych, wspólnie przechowywane pamięci podręcznej do aplikacji sieci web platformy Azure. Może szybko korzystać z pamięci podręcznej Redis do buforowania danych wyjściowych strony. Ponadto, gdy użytkownik skalowanie aplikacji sieci web później, Redis pomaga utrwalić sesje użytkowników na wielu wystąpień niezawodnie.

### <a name="create-an-azure-redis-cache"></a>Tworzenie usługi Azure Redis Cache
Użyj [Tworzenie pamięci podręcznej redis az](https://docs.microsoft.com/en-us/cli/azure/redis#create) Tworzenie pamięci podręcznej Redis Azure i zapisać w formacie JSON dane wyjściowe. Użyj unikatowej nazwy w `$cacheName`.

```powershell
$cacheName = "<replace-with-a-unique-cache-name>"
$redis = (az redis create --name $cacheName --resource-group myResourceGroup --location "West Europe" --sku-capacity 0 --sku-family C --sku-name Basic | ConvertFrom-Json)
```

### <a name="configure-the-application-to-use-redis"></a>Konfigurowanie aplikacji do korzystania z pamięci podręcznej Redis
Format ciągu połączenia dla pamięci podręcznej.

```powershell
$connstring = "$($redis.hostname):$($redis.sslPort),password=$($redis.accessKeys.primaryKey),ssl=True,abortConnect=False"
$connstring 
```

Drugi wiersz powinien zapewnić wyjścia, który wygląda następująco:

```
mycachename.redis.cache.windows.net:6380,password=/rQP/TLz1mrEPpmh9b/gnfns/t9vBRXqXn3i1RwBjGA=,ssl=True,abortConnect=False
```

W programie Visual Studio, Utwórz plik konfiguracji sieci web w katalogu głównym projektu o nazwie `redis.config` i wklej następujący kod do niego. W `value`, użyj parametrów połączenia z danych wyjściowych programu PowerShell.

```xml
<appSettings>
  <add key="RedisConnection" value="your-azure-redis-cache-connection-string"/>
</appSettings>
```

Jeśli przyjrzymy się `.gitignore` plik w repozytorium Git, zobaczysz, że ten plik jest wyłączone z kontroli źródła. W ten sposób poufne informacje były bezpieczne. 

Otwórz `Web.config`. Powiadomienie `<appSettings file="redis.config">` element, który pobiera ustawienie utworzony w `redis.config`. 

Znajdź sekcję komentarze, która obejmuje `<sessionState>` i `<caching>`. Usuń znaczniki komentarza w tej sekcji.

![](./media/app-service-web-tutorial-hyper-scale-app/redisproviders.png)

Ten kod wyszukuje ciąg połączenia Redis zdefiniowanego w `RedisConnection`. 

Teraz aplikacja używa Redis do zarządzania sesjami i buforowania. Typ `F5` do uruchomienia aplikacji. Jeśli chcesz możesz pobrać klienta zarządzania Redis do wizualizacji danych, które są teraz zapisywane w pamięci podręcznej.

### <a name="configure-the-connection-string-in-azure"></a>Konfigurowanie parametrów połączenia na platformie Azure

Aby aplikacja działa na platformie Azure należy skonfigurować te same parametry połączenia Redis w aplikacji sieci web platformy Azure. Ponieważ `redis.config` nie są przechowywane w kontroli źródła, nie są wdrażane na platformie Azure, po uruchomieniu wdrożenia usługi Git.

Użyj [zaktualizować az usługi aplikacji sieci web config appsettings](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update) Aby dodać parametry połączenia o tej samej nazwie (`RedisConnection`).

AZ usługi aplikacji sieci web config appsettings zaktualizować — ustawienia "RedisConnection = $connstring"--name $appName — myResourceGroup grupy zasobów

Należy pamiętać, że `$connstring` zawiera ciąg sformatowany połączenia.

### <a name="redeploy-the-application-to-azure"></a>Należy ponownie wdrożyć aplikację na platformie Azure
Wypchnij zmiany na platformie Azure przy użyciu poleceń Git

```bash
git add .
git commit -m "now use Redis providers"
git push azure master
```

Po wyświetleniu monitu o hasło, należy użyć hasła określonej w momencie uruchomienia `az appservice web deployment user set`.

### <a name="browse-to-the-azure-web-app"></a>Przejdź do aplikacji sieci web platformy Azure
Użyj [przeglądania sieci web appservice az](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse) w celu wyświetlenia zmian na żywo na platformie Azure.

```azurecli
az appservice web browse --name $appName --resource-group myResourceGroup
```

## <a name="step-4---scale-to-multiple-instances"></a>Krok 4 — Skaluj do wielu wystąpień
Plan usługi aplikacji jest jednostką skalowania dla aplikacji sieci web platformy Azure. Do skalowania aplikacji sieci web, skalowanie planu usługi aplikacji.

Użyj [aktualizacji planu usługi aplikacji az](https://docs.microsoft.com/cli/azure/appservice/plan#update) do skalowania w poziomie plan usługi aplikacji do wystąpienia, który jest maksymalną liczbę dozwoloną przez warstwę cenową B1. Należy pamiętać, że B1 jest warstwę cenową wybraną podczas tworzenia planu usługi aplikacji wcześniej. 

```azurecli
az appservice plan update --name myAppServicePlan --resource-group myResourceGroup --number-of-workers 3 
```

## <a name="step-5---scale-geographically"></a>Krok 5 — skali geograficznie
Skalowanie geograficznie, możesz uruchomić aplikację w wielu regionach chmury Azure. Ten Instalator zrównoważenie obciążenia aplikacji dalsze oparte na lokalizacji geograficznej i zmniejsza czas odpowiedzi, umieszczając aplikację bliżej do przeglądarki klienta.

W tym kroku można skalować aplikacji sieci web ASP.NET w regionie drugi z [usługi Azure Traffic Manager](https://docs.microsoft.com/en-us/azure/traffic-manager/). Po zakończeniu tego kroku będziesz mieć aplikację sieci web uruchomione w Europie zachodnie (już utworzone) i aplikacji sieci web uruchomionych w Azji Południowo-Wschodnia (jeszcze nie utworzono). Obie aplikacje zostanie wyświetlona z tego samego adresu URL Menedżera ruchu.

### <a name="scale-up-the-europe-app-to-standard-tier"></a>Skalowanie w górę Europy aplikacji w warstwie Standard
W usłudze App Service Integracja z usługą Azure Traffic Manager wymaga warstwy cenowej standardowa. Użyj [aktualizacji planu usługi aplikacji az](https://docs.microsoft.com/cli/azure/appservice/plan#update) na skalowanie w górę aby S1 plan usługi aplikacji. 

```azurecli
az appservice plan update --name myAppServicePlan --resource-group myResourceGroup --sku S1
```
### <a name="create-a-traffic-manager-profile"></a>Tworzenie profilu usługi Traffic Manager 
Użyj [Tworzenie profilu Menedżera ruchu sieciowego az](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#create) do tworzenia profilu usługi Traffic Manager i dodać go do tej grupy zasobów. Użyj unikatowej nazwy DNS w $dnsName.

```azurecli
$dnsName = "<replace-with-unique-dns-name>"
az network traffic-manager profile create --name myTrafficManagerProfile --resource-group myResourceGroup --routing-method Performance --unique-dns-name $dnsName
```

> [!NOTE]
> `--routing-method Performance`Określa, że ten profil [kieruje ruchem użytkownika do najbliższego punktu końcowego](../traffic-manager/traffic-manager-routing-methods.md).

### <a name="get-the-resource-id-of-the-europe-app"></a>Pobierz identyfikator zasobu aplikacji Europy
Użyj [az usługi aplikacji sieci web Pokaż](https://docs.microsoft.com/en-us/cli/azure/appservice/web#show) można uzyskać Identyfikatora zasobów aplikacji sieci web.

```azurecli
$appId = az appservice web show --name $appName --resource-group myResourceGroup --query id --output tsv
```

### <a name="add-a-traffic-manager-endpoint-for-the-europe-app"></a>Dodawanie punktu końcowego Menedżera ruchu dla Europy aplikacji
Użyj [utworzyć punktu końcowego Menedżera ruchu sieciowego az](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create) Dodawanie punktu końcowego profilu Menedżera ruchu i użycie identyfikator zasobu aplikacji sieci web jako element docelowy.

```azurecli
az network traffic-manager endpoint create --name myWestEuropeEndpoint --profile-name myTrafficManagerProfile --resource-group myResourceGroup --type azureEndpoints --target-resource-id $appId
```

### <a name="get-the-traffic-manager-endpoint-url"></a>Pobierz adres URL punktu końcowego Menedżera ruchu
Profil Menedżera ruchu ma teraz punktu końcowego, który wskazuje istniejącą aplikację sieci web. Użyj [Pokaż profil Menedżera ruchu sieciowego az](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#show) można pobrać adresu URL. 

```azurecli
az network traffic-manager profile show --name myTrafficManagerProfile --resource-group myResourceGroup --query dnsConfig.fqdn --output tsv
```

Skopiuj dane wyjściowe w przeglądarce. Aplikacja sieci web powinno zostać wyświetlone ponownie.

### <a name="create-an-azure-redis-cache-in-asia"></a>Tworzenie pamięci podręcznej Azure Redis w Azji
Teraz Replikowanie aplikacji sieci web platformy Azure dla regionu Azja południowo-wschodnia. Aby rozpocząć, należy użyć [Tworzenie pamięci podręcznej redis az](https://docs.microsoft.com/en-us/cli/azure/redis#create) utworzyć drugi pamięć podręczna Redis Azure w Azji Południowo-Wschodnia. Ta pamięć podręczna musi być wspólnie przechowywane z aplikacją w Azji.

```powershell
$redis = (az redis create --name $cacheName-asia --resource-group myResourceGroup --location "Southeast Asia" --sku-capacity 0 --sku-family C --sku-name Basic | ConvertFrom-Json)
```

`--name $cacheName-asia`zawiera nazwę pamięci podręcznej Europa Zachodnia pamięci podręcznej z `-asia` sufiks.

### <a name="create-an-app-service-plan-in-asia"></a>Tworzenie planu usługi App Service w Azji
Użyj [Tworzenie planu usług aplikacji az](https://docs.microsoft.com/cli/azure/appservice/plan#create) można utworzyć planu usługi aplikacji — druga regionu Azja południowo-wschodnia, przy użyciu tej samej warstwie S1 jako plan Europa Zachodnia.

```azurecli
az appservice plan create --name myAppServicePlanAsia --resource-group myResourceGroup --location "Southeast Asia" --sku S1
```

### <a name="create-a-web-app-in-asia"></a>Tworzenie aplikacji sieci web w Azji
Użyj [utworzyć az appservice web](https://docs.microsoft.com/en-us/cli/azure/appservice/web#create) utworzyć drugi aplikację sieci web.

```azurecli
az appservice web create --name $appName-asia --resource-group myResourceGroup --plan myAppServicePlanAsia
```

`--name $appName-asia`zawiera nazwę aplikacji Europa Zachodnia aplikacji z `-asia` sufiks.

### <a name="configure-the-connection-string-for-redis"></a>Konfigurowanie parametrów połączenia dla pamięci podręcznej Redis
Użyj [zaktualizować az usługi aplikacji sieci web config appsettings](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update) można dodać do aplikacji sieci web, ciąg połączenia dla pamięci podręcznej Azja południowo-wschodnia.

AZ usługi aplikacji sieci web config appsettings zaktualizować — ustawienia "RedisConnection = $($redis.hostname): $($redis.sslPort), hasło = $($redis.accessKeys.primaryKey), ssl = True, abortConnect = False"--name $appName — Azja--myResourceGroup grupy zasobów

### <a name="configure-git-deployment-for-the-asia-app"></a>Konfiguruj wdrożenie Git dla aplikacji Azji.
Użyj [kontroli źródła sieci web az appservice — config lokalnych git](https://docs.microsoft.com/en-us/cli/azure/appservice/web/source-control#config-local-git) do skonfigurowania lokalnego wdrożenia Git dla drugiego aplikacji sieci web.

```azurecli
az appservice web source-control config-local-git --name $appName-asia --resource-group myResourceGroup
```

To polecenie umożliwia wyjścia, który wygląda następująco:

```json
{
  "url": "https://user123@myuniqueappname-asia.scm.azurewebsites.net/myuniqueappname.git"
}
```

Umożliwia skonfigurowanie zdalnego dla lokalnego repozytorium Git drugi zwrócony adres URL. Polecenie używa w poprzednim przykładzie danych wyjściowych.

```bash
git remote add azure-asia https://user123@myuniqueappname-asia.scm.azurewebsites.net/myuniqueappname.git
```

### <a name="deploy-your-sample-application"></a>Wdrażanie przykładowej aplikacji
Uruchom `git push` Aby wdrożyć aplikację przykładową, do drugiego zdalny narzędzia Git. 

```bash
git push azure-asia master
```

Po wyświetleniu monitu o hasło, należy użyć hasła określonej w momencie uruchomienia `az appservice web deployment user set`.

### <a name="browse-to-the-asia-app"></a>Przejdź do aplikacji Azja
Użyj [przeglądania sieci web appservice az](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse) Aby sprawdzić, czy aplikacja działa na platformie Azure.

```azurecli
az appservice web browse --name $appName-asia --resource-group myResourceGroup
```

### <a name="get-the-resource-id-of-the-asia-app"></a>Pobierz identyfikator zasobu aplikacji Azja
Użyj [az usługi aplikacji sieci web Pokaż](https://docs.microsoft.com/en-us/cli/azure/appservice/web#show) można uzyskać Identyfikatora zasobów aplikacji sieci web w Azji Południowo-Wschodnia.

```azurecli
$appIdAsia = az appservice web show --name $appName-asia --resource-group myResourceGroup --query id --output tsv
```

### <a name="add-a-traffic-manager-endpoint-for-the-asia-app"></a>Dodawanie punktu końcowego Menedżera ruchu, Azja aplikacji
Użyj [utworzyć punktu końcowego Menedżera ruchu sieciowego az](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create) można dodać drugiego punktu końcowego profilu Menedżera ruchu.

```azurecli
az network traffic-manager endpoint create --name myAsiaEndpoint --profile-name myTrafficManagerProfile --resource-group myResourceGroup --type azureEndpoints --target-resource-id $appIdAsia
```

### <a name="add-region-identifier-to-web-apps"></a>Dodaj identyfikator regionu do aplikacji sieci web
Użyj [zaktualizować az usługi aplikacji sieci web config appsettings](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update) można dodać zmienną środowiskową określonego regionu.

```azurecli
az appservice web config appsettings update --settings "Region=West Europe" --name $appName --resource-group myResourceGroup
az appservice web config appsettings update --settings "Region=Southeast Asia" --name $appName-asia --resource-group myResourceGroup
```

Kod aplikacji już używa tego ustawienia aplikacji. Spójrz na `HighScaleApp\Views\Home\Index.cshtml`.

### <a name="complete"></a>Zakończenie!

Teraz spróbuj uzyskać dostęp adres URL profilu Menedżera ruchu z przeglądarek w różnych regionach geograficznych. Przeglądarka klienta z Europy powinny być widoczne "Europa Zachodnia ASP.NET" i "Azja południowo-wschodnia ASP.NET." powinny być widoczne w przeglądarce klienta z Azja

## <a name="more-resources"></a>Więcej zasobów
