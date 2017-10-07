---
title: domeny niestandardowej aaaAdd i SSL tooan Azure web app | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak tooprepare platformy Azure w sieci web toogo aplikacji w środowisku produkcyjnym, dodając znakowaniu firmy. Mapa aplikacji sieci web tooyour (domena niestandardowych) nazwa domeny niestandardowej hello i zabezpiecz ją przy użyciu niestandardowego certyfikatu SSL."
services: app-service\web
documentationcenter: nodejs
author: cephalin
manager: erikre
editor: 
ms.assetid: dc446e0e-0958-48ea-8d99-441d2b947a7c
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: tutorial
ms.date: 03/29/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 2679ed8b2dbbeba0b128c1a3ec01148f97c35342
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="add-custom-domain-and-ssl-tooan-azure-web-app"></a>Dodaj niestandardową domenę i protokołu SSL tooan aplikacji sieci web Azure

Ten samouczek pokazuje, jak tooquickly mapowania aplikacji sieci web Azure tooyour nazwy domeny niestandardowej i zabezpiecz ją przy użyciu niestandardowego certyfikatu SSL. 

## <a name="before-you-begin"></a>Przed rozpoczęciem

Przed uruchomieniem tego przykładu należy zainstalować hello [Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) lokalnie.

Należy również strony konfiguracji DNS toohello dostęp administracyjny do dostawcy odpowiedniej domeny. Na przykład tooadd `www.contoso.com`, należy wpisy DNS może tooconfigure toobe dla `contoso.com`.

Ponadto należy się prawidłowe. Plik PFX _i_ jego hasło dla certyfikatu SSL hello ma tooupload i ich powiązania. Ten certyfikat protokołu SSL należy toosecure skonfigurowanych hello domenę niestandardową nazwę. W hello powyżej przykładzie, należy zabezpieczyć certyfikat SSL `www.contoso.com`. 

## <a name="step-1---create-an-azure-web-app"></a>Krok 1 — Tworzenie aplikacji sieci web platformy Azure

### <a name="log-in-tooazure"></a>Zaloguj się za tooAzure

Mamy teraz będzie toouse hello Azure CLI 2.0 w zasobach hello toocreate okno terminalu potrzebne toohost naszej aplikacji Node.js na platformie Azure.  Zaloguj się za tooyour subskrypcji platformy Azure z hello [logowania az](/cli/azure/#login) poleceń i wykonaj hello wyświetlanymi instrukcjami. 

```azurecli 
az login 
``` 
   
### <a name="create-a-resource-group"></a>Tworzenie grupy zasobów   
Utwórz grupę zasobów o hello [Tworzenie grupy az](/cli/azure/group#create). Grupa zasobów platformy Azure to logiczny kontener przeznaczony do wdrażania zasobów platformy Azure, takich jak aplikacje sieci Web, bazy danych i konta magazynu, oraz zarządzania nimi. 

```azurecli
az group create --name myResourceGroup --location westeurope 
```

toosee jakie możliwe wartości można użyć dla `---location`, użyj hello `az appservice list-locations` polecenia wiersza polecenia platformy Azure.

## <a name="create-an-app-service-plan"></a>Tworzenie planu usługi App Service

Tworzenie planu usługi aplikacji z hello [Tworzenie planu usług aplikacji az](/cli/azure/appservice/plan#create) polecenia. 

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

Witaj poniższy przykład tworzy plan usługi aplikacji o nazwie `myAppServicePlan` przy użyciu hello **podstawowe** warstwy cenowej.

Tworzenie planu usług aplikacji az — nazwa myAppServicePlan — myResourceGroup grupy zasobów--sku B1

Po utworzeniu planu usługi aplikacji hello hello Azure CLI pokazuje informacje toohello podobnie poniższy przykład. 

```json 
{ 
    "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/serverfarms/myAppServicePlan", 
    "kind": "app", 
    "location": "West Europe", 
    "sku": { 
    "capacity": 1, 
    "family": "B", 
    "name": "B1", 
    "tier": "Basic" 
    }, 
    "status": "Ready", 
    "type": "Microsoft.Web/serverfarms" 
} 
``` 

## <a name="create-a-web-app"></a>Tworzenie aplikacji sieci Web

Teraz, utworzono plan usługi aplikacji, należy utworzyć aplikację sieci web w obrębie hello `myAppServicePlan` planu usługi aplikacji. Hello daje aplikacji sieci web użytkownik w przypadku hostingu toodeploy miejsca kodu, a także zawiera adres URL dla Ciebie tooview hello wdrożonych aplikacji. Użyj hello [utworzyć az appservice web](/cli/azure/appservice/web#create) aplikacji sieci web hello toocreate polecenia. 

W poleceniu hello poniżej, podstawić własną unikatowej nazwy aplikacji której występuje hello `<app_name>` symbolu zastępczego. Ta nazwa będzie służyć jako część hello hello domyślna nazwa domeny dla aplikacji sieci web hello, więc nazwa hello musi toobe unikatowy przez wszystkie aplikacje na platformie Azure. Później można mapować żadnych niestandardowych aplikacji sieci web toohello wpis DNS przed udostępnieniem jej tooyour użytkowników. 

```azurecli
az appservice web create --name <app_name> --resource-group myResourceGroup --plan myAppServicePlan 
```

Podczas tworzenia aplikacji sieci web hello hello Azure CLI pokazuje informacje toohello podobnie poniższy przykład. 

```json 
{ 
    "clientAffinityEnabled": true, 
    "defaultHostName": "<app_name>.azurewebsites.net", 
    "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/sites/<app_name>", 
    "isDefaultContainer": null, 
    "kind": "app", 
    "location": "West Europe", 
    "name": "<app_name>", 
    "repositorySiteName": "<app_name>", 
    "reserved": true, 
    "resourceGroup": "myResourceGroup", 
    "serverFarmId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/serverfarms/myAppServicePlan", 
    "state": "Running", 
    "type": "Microsoft.Web/sites", 
} 
```

Z danych wyjściowych JSON, hello `defaultHostName` wskazuje nazwę domeny domyślnej aplikacji sieci web. W przeglądarce Przejdź toothis adres.

```
http://<app_name>.azurewebsites.net 
``` 
 
![app-service-web-service-created](media/app-service-web-tutorial-domain-ssl/web-app-created.png)  

## <a name="step-2---configure-dns-mapping"></a>Krok 2 — Konfigurowanie mapowania DNS

W tym kroku, Dodaj mapowanie z domeny niestandardowej tooyour aplikacji sieci web domyślna nazwa domeny `<app_name>.azurewebsites.net`. Zazwyczaj jest wykonanie tego kroku w witryny sieci Web dostawcy domeny. Witryny sieci Web co rejestratora domen różni się nieznacznie, dlatego należy skonsultować się Twój dostawca dokumentacji. W tym miejscu są jednak pewne ogólne wytyczne. 

### <a name="navigate-tootoodns-management-page"></a>Przejdź do strony zarządzania tootooDNS

Po pierwsze Zaloguj rejestratora domen tooyour witryny sieci Web.  

Następnie odnaleźć hello strony Zarządzanie rekordami DNS. Wyszukaj łącza lub obszarów witryny hello etykietą **nazwy domeny**, **DNS**, lub **nazwy serwera zarządzania**. Często, można znaleźć łącza hello wyświetlanie informacji o koncie, a następnie sprawdzając takich jak łącze **mojej domeny**.

Po znalezieniu tej strony, poszukaj łącze umożliwiające dodawanie lub edytowanie rekordów DNS. Może to być **pliku strefy** lub **rekordy DNS** łącza, lub **konfiguracji zaawansowanej** łącza.

### <a name="create-a-cname-record"></a>Utwórz rekord CNAME

Dodaj rekord CNAME mapujący hello poddomeny odpowiednią nazwę tooyour aplikacji sieci web domyślna nazwa domeny (`<app_name>.azurewebsites.net`, gdzie `<app_name>` jest unikatowa nazwa aplikacji).

Dla hello `www.contoso.com` przykład utworzyć rekord CNAME, który mapuje hello `www` hostname zbyt`<app_name>.azurewebsites.net`.

## <a name="step-3---configure-hello-custom-domain-on-your-web-app"></a>Krok 3 — konfigurowanie domeny niestandardowej hello na aplikację sieci web

Po zakończeniu konfigurowania mapowania nazwy hosta hello w witryny sieci Web dostawcy domeny, możesz teraz gotowy tooconfigure hello niestandardową domenę aplikacji sieci web. Użyj hello [dodać az usługi aplikacji sieci web config hostname](/cli/azure/appservice/web/config/hostname#add) polecenia tooadd tej konfiguracji. 

W poleceniu hello poniżej, Zastąp `<app_name>` z unikatowej nazwy aplikacji, a < your_custom_domain > z hello pełną niestandardowej nazwy domeny (np. `www.contoso.com`). 

```azurecli
az appservice web config hostname add --webapp <app_name> --resource-group myResourceGroup --name <your_custom_domain>
```

domeny niestandardowej Hello jest teraz pełni zamapowanych tooyour aplikacji sieci web. W przeglądarce Przejdź toohello niestandardowej nazwy domeny. Na przykład:

```
http://www.contoso.com 
``` 

![app-service-web-service-created](media/app-service-web-tutorial-domain-ssl/web-app-custom-domain.png)  

## <a name="step-4---bind-a-custom-ssl-certificate-tooyour-web-app"></a>Krok 4 — wiązanie niestandardowej aplikacji sieci web tooyour certyfikat SSL

Masz teraz aplikacji sieci web platformy Azure, z nazwą domeny hello w hello na pasku adresu przeglądarki. Jednak w przypadku przejścia toohello `https://<your_custom_domain>` teraz otrzymujesz błąd certyfikatu. 

![app-service-web-service-created](media/app-service-web-tutorial-domain-ssl/web-app-cert-error.png)  

Ten błąd występuje, ponieważ aplikacja sieci web nie ma jeszcze powiązanie certyfikatu SSL, który jest zgodny z niestandardowej nazwy domeny. Jednak nie występuje błąd, jeśli użytkownik przejdzie zbyt`https://<app_name>.azurewebsites.net`. Jest to spowodowane aplikacji, a także wszystkie aplikacje w usłudze Azure App Service, są chronione za hello certyfikat protokołu SSL dla hello `*.azurewebsites.net` domeny symbolu wieloznacznego domyślnie. 

W kolejności tooaccess aplikacji sieci web przez niestandardową nazwę domeny, wymagany jest certyfikat SSL hello toobind dla aplikacji sieci web toohello domeny niestandardowej. Wykona go w tym kroku. 

### <a name="upload-hello-ssl-certificate"></a>Przekaż certyfikat SSL hello

Przekaż hello certyfikat SSL dla aplikacji sieci web tooyour domeny niestandardowej przy użyciu hello [az usługi aplikacji sieci web config ssl przekazywania](/cli/azure/appservice/web/config/ssl#upload) polecenia.

W poleceniu hello poniżej, Zastąp `<app_name>` z Twojej unikatowej nazwy aplikacji, `<path_to_ptx_file>` z hello tooyour ścieżki. Plik PFX i `<password>` z hasło do certyfikatu. 

```azurecli
az appservice web config ssl upload --name <app_name> --resource-group myResourceGroup --certificate-file <path_to_pfx_file> --certificate-password <password> 
```

Po przekazaniu certyfikatu hello hello Azure CLI pokazuje informacje toohello podobnie poniższy przykład:

```json
{
  "cerBlob": null,
  "expirationDate": "2018-03-29T14:12:57+00:00",
  "friendlyName": "",
  "hostNames": [
    "www.contoso.com"
  ],
  "hostingEnvironmentProfile": null,
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/cert
ificates/9FD1D2D06E2293673E2A8D1CA484A092BD016D00__West Europe_myResourceGroup",
  "issueDate": "2017-03-29T14:12:57+00:00",
  "issuer": "www.contoso.com",
  "keyVaultId": null,
  "keyVaultSecretName": null,
  "keyVaultSecretStatus": "Initialized",
  "kind": null,
  "location": "West Europe",
  "name": "9FD1D2D06E2293673E2A8D1CA484A092BD016D00__West Europe_myResourceGroup",
  "password": null,
 "pfxBlob": null,
  "publicKeyHash": null,
  "resourceGroup": "myResourceGroup",
  "selfLink": null,
  "serverFarmId": null,
  "siteName": null,
  "subjectName": "www.contoso.com",
  "tags": null,
  "thumbprint": "9FD1D2D06E2293673E2A8D1CA484A092BD016D00",
  "type": "Microsoft.Web/certificates",
  "valid": null
}
```

Z danych wyjściowych JSON, hello `thumbprint` przedstawia odcisku palca certyfikatu przekazane. Skopiuj wartości na potrzeby hello następnego kroku.

### <a name="bind-hello-uploaded-ssl-certificate-toohello-web-app"></a>Witaj BIND przekazać aplikacji sieci web toohello certyfikat SSL

Aplikacja sieci web ma teraz nazwę domeny niestandardowej hello i ma również certyfikat SSL, która zabezpiecza tej domeny niestandardowej. Witaj tylko element toodo po lewej stronie jest toobind hello przekazano certyfikat toohello aplikacja sieci web. Można to zrobić przy użyciu hello [powiązania ssl konfiguracji sieci web appservice az](/cli/azure/appservice/web/config/ssl#bind) polecenia.

W poleceniu hello poniżej, Zastąp `<app_name>` z Twojej unikatowej nazwy aplikacji i `<thumbprint-from-previous-output>` z hello odcisk palca certyfikatu, który można pobrać z hello poprzednie polecenie. 

powiązania ssl sieci web config az appservice--name < nazwa_aplikacji >--myResourceGroup grupy zasobów — odcisk palca certyfikatu < odcisk palca z — poprzednie output > SNI ssl — typ

Gdy certyfikat hello jest powiązane tooyour aplikacji sieci web, hello Azure CLI pokazuje informacje toohello podobnie poniższy przykład:

{"stanu dostępności": "Normal", "clientAffinityEnabled": ma wartość true, "clientCertEnabled": ma wartość FAŁSZ, "cloningInfo": null, "containerSize": 0, "dailyMemoryTimeQuota": 0, "defaultHostName": "< nazwa_aplikacji >. azurewebsites.net", "enabled": true "enabledHostNames": ["www.contoso.com", "< nazwa_aplikacji >. azurewebsites.net", "< nazwa_aplikacji >. scm.azurewebsites.net"], "gatewaySiteName": null, "hostNameSslStates": [{"hostType": "Standardowy", "name": "< nazwa_aplikacji >. azurewebsites.net", "sslState": "Wyłączone", "odcisk palca": null, "toUpdate": wartość null, "wirtualnego adresu IP": null}, {"hostType": "Repository", "name": "< nazwa_aplikacji >. scm.azurewebsites.net", "sslState": "Wyłączone" "odcisk palca": null, "toUpdate": null, "wirtualnego adresu IP": wartości null}, {"hostType": "Standardowy", "name": "www.contoso.com", "sslState": "SniEnabled", "odcisk palca": "9FD1D2D06E2293673E2A8D1CA484A092BD016D00", "toUpdate": null, "wirtualnego adresu IP": wartości null}], "nazwy hostów": ["www.contoso.com", "< nazwa_aplikacji >. azurewebsites.net"], "hostNamesDisabled": ma wartość FAŁSZ, "hostingEnvironmentProfile": null, "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/site s / < nazwa_aplikacji >", "isDefaultContainer": null "typu": "Aplikacja sieci Web", "lastModifiedTimeUtc": "2017-03-29T14:36:18.803333", "Lokalizacja": "Europa Zachodnia", "maxNumberOfWorkers": null, "Mikrousługi": "false", "Nazwa": "< nazwa_aplikacji >" "outboundIpAddresses": "13.94.143.57,13.94.136.57,40.68.199.146,13.94.138.55,13.94.140.1", "premiumAppDeployed": null, "repositorySiteName": "< nazwa_aplikacji >", "zastrzeżone": false "w grupie zasobów": "myResourceGroup", "scmSiteAlsoStopped": ma wartość FAŁSZ, "serverFarmId": "/ subskrypcji/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/dostawców/Microsof t.Web/serverfarms/myAppServicePlan", "siteConfig": null, "slotSwapStatus": null, "stan": "Uruchomiona", "suspendedTill": null "tagi": null, "targetSwapSlot": null, "trafficManagerHostNames": null, "type": "Microsoft.Web/sites", "usageState": "Normal"}

W przeglądarce Przejdź tooHTTPS punkt końcowy z niestandardowej nazwy domeny. Na przykład:

```
https://www.contoso.com 
``` 

![app-service-web-service-created](media/app-service-web-tutorial-domain-ssl/web-app-ssl-success.png)  

## <a name="more-resources"></a>Więcej zasobów

[Kupowanie i konfigurowanie niestandardowej nazwy domeny w usłudze Azure App Service](custom-dns-web-site-buydomains-web-app.md)
[kupowanie i konfigurowanie certyfikatu SSL usługi aplikacji Azure](web-sites-purchase-ssl-web-site.md)
