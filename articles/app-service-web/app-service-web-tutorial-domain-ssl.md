---
title: "Dodaj niestandardową domenę i protokołu SSL dla aplikacji sieci web platformy Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak przygotować aplikacji sieci Azure web, aby przejść przez dodanie znakowaniu firmy produkcji. Mapa niestandardowa nazwa domeny (domena niestandardowych) do aplikacji sieci web i zabezpiecz ją przy użyciu niestandardowego certyfikatu SSL."
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
ms.openlocfilehash: c9d00f678b6257a8aafb35acd2d5a2292703a2dc
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="add-custom-domain-and-ssl-to-an-azure-web-app"></a>Dodaj niestandardową domenę i protokołu SSL dla aplikacji sieci web platformy Azure

Ten samouczek pokazuje, jak szybko zamapować niestandardowej nazwy domeny do aplikacji sieci web platformy Azure i zabezpiecz ją przy użyciu niestandardowego certyfikatu SSL. 

## <a name="before-you-begin"></a>Przed rozpoczęciem

Przed uruchomieniem tego przykładu należy zainstalować [Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) lokalnie.

Należy również dostęp administracyjny do strony Konfiguracja DNS dla dostawcy odpowiedniej domeny. Na przykład, aby dodać `www.contoso.com`, musisz mieć możliwość konfigurowania wpisów DNS dla `contoso.com`.

Ponadto należy się prawidłowe. Plik PFX _i_ jego hasło dla certyfikatu SSL, aby przekazać i ich powiązania. Należy skonfigurować ten certyfikat protokołu SSL do zabezpieczania nazwy domeny niestandardowej, która ma. W powyższym przykładzie, należy zabezpieczyć certyfikat SSL `www.contoso.com`. 

## <a name="step-1---create-an-azure-web-app"></a>Krok 1 — Tworzenie aplikacji sieci web platformy Azure

### <a name="log-in-to-azure"></a>Zaloguj się do platformy Azure.

Teraz użyjemy interfejsu wiersza polecenia platformy Azure 2.0 w oknie terminalu do utworzenia zasobów wymaganych do hostowania tej aplikacji w języku Node.js na platformie Azure.  Zaloguj się do subskrypcji platformy Azure za pomocą polecenia [az login](/cli/azure/#login) i postępuj zgodnie z instrukcjami wyświetlanymi na ekranie. 

```azurecli 
az login 
``` 
   
### <a name="create-a-resource-group"></a>Tworzenie grupy zasobów   
Utwórz grupę zasobów za pomocą polecenia [az group create](/cli/azure/group#create). Grupa zasobów platformy Azure to logiczny kontener przeznaczony do wdrażania zasobów platformy Azure, takich jak aplikacje sieci Web, bazy danych i konta magazynu, oraz zarządzania nimi. 

```azurecli
az group create --name myResourceGroup --location westeurope 
```

Aby sprawdzić, jakich wartości można użyć dla lokalizacji `---location`, użyj polecenia interfejsu wiersza polecenia platformy Azure `az appservice list-locations`.

## <a name="create-an-app-service-plan"></a>Tworzenie planu usługi App Service

Utwórz plan usługi App Service za pomocą polecenia [az appservice plan create](/cli/azure/appservice/plan#create). 

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

Poniższy przykład tworzy plan usługi aplikacji o nazwie `myAppServicePlan` przy użyciu **podstawowe** warstwy cenowej.

Tworzenie planu usług aplikacji az — nazwa myAppServicePlan — myResourceGroup grupy zasobów--sku B1

Po utworzeniu planu usługi aplikacji Azure CLI przedstawia informacje podobne do poniższego przykładu. 

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

Teraz, gdy został utworzony plan usługi App Service, utwórz aplikację sieci Web w ramach planu usługi App Service `myAppServicePlan`. Umożliwia aplikacji sieci web, możesz w przypadku hostingu miejsca, aby wdrożyć kod, a także zawiera adres URL do wyświetlania wdrożonej aplikacji. Użyj polecenia [az appservice web create](/cli/azure/appservice/web#create), aby utworzyć aplikację sieci Web. 

W poniższym poleceniu zastąp z własnej nazwy unikatowy aplikacji, w której występuje `<app_name>` symbolu zastępczego. Ta nazwa będzie służyć jako część domyślna nazwa domeny dla aplikacji sieci web, więc nazwa musi być unikatowy w obrębie wszystkich aplikacji w usłudze Azure. Później możesz zamapować dowolny niestandardowy wpis DNS na aplikację sieci Web, zanim udostępnisz ją użytkownikom. 

```azurecli
az appservice web create --name <app_name> --resource-group myResourceGroup --plan myAppServicePlan 
```

Po utworzeniu aplikacji sieci Web interfejs wiersza polecenia platformy Azure wyświetli informacje podobne do następujących. 

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

Z danych wyjściowych JSON `defaultHostName` wskazuje nazwę domeny domyślnej aplikacji sieci web. W przeglądarce przejdź do tego adresu.

```
http://<app_name>.azurewebsites.net 
``` 
 
![app-service-web-service-created](media/app-service-web-tutorial-domain-ssl/web-app-created.png)  

## <a name="step-2---configure-dns-mapping"></a>Krok 2 — Konfigurowanie mapowania DNS

W tym kroku należy dodać mapowanie z domeny niestandardowej nazwy domeny domyślnej aplikacji sieci web, `<app_name>.azurewebsites.net`. Zazwyczaj jest wykonanie tego kroku w witryny sieci Web dostawcy domeny. Witryny sieci Web co rejestratora domen różni się nieznacznie, dlatego należy skonsultować się Twój dostawca dokumentacji. W tym miejscu są jednak pewne ogólne wytyczne. 

### <a name="navigate-to-to-dns-management-page"></a>Przejdź do strony zarządzania DNS

Po pierwsze Zaloguj się do witryny sieci Web rejestratora domen.  

Następnie można znaleźć strony zarządzania rekordów DNS. Wyszukaj łącza lub obszarów witryny z etykietą **nazwy domeny**, **DNS**, lub **nazwy serwera zarządzania**. Często, można znaleźć link wyświetlanie informacji o koncie, a następnie sprawdzając takich jak łącze **mojej domeny**.

Po znalezieniu tej strony, poszukaj łącze umożliwiające dodawanie lub edytowanie rekordów DNS. Może to być **pliku strefy** lub **rekordy DNS** łącza, lub **konfiguracji zaawansowanej** łącza.

### <a name="create-a-cname-record"></a>Utwórz rekord CNAME

Dodaj rekord CNAME mapujący nazwa żądanego poddomeny do aplikacji sieci web domyślna nazwa domeny (`<app_name>.azurewebsites.net`, gdzie `<app_name>` jest unikatowa nazwa aplikacji).

Dla `www.contoso.com` przykład utworzyć rekord CNAME, który mapuje `www` nazwy hosta do `<app_name>.azurewebsites.net`.

## <a name="step-3---configure-the-custom-domain-on-your-web-app"></a>Krok 3 — konfigurowanie domeny niestandardowej w aplikacji sieci web

Po zakończeniu konfigurowania mapowania nazwy hosta w witryny sieci Web dostawcy domeny, możesz przystąpić do konfigurowania domeny niestandardowej w aplikacji sieci web. Użyj [dodać az usługi aplikacji sieci web config hostname](/cli/azure/appservice/web/config/hostname#add) polecenie, aby dodać tę konfigurację. 

W poniższym poleceniu zastąp `<app_name>` z unikatowej nazwy aplikacji, a < your_custom_domain > o nazwie FQDN domen niestandardowych (np. `www.contoso.com`). 

```azurecli
az appservice web config hostname add --webapp <app_name> --resource-group myResourceGroup --name <your_custom_domain>
```

Domena niestandardowa teraz pełni jest mapowana do aplikacji sieci web. W przeglądarce przejdź do nazwy domeny niestandardowej. Na przykład:

```
http://www.contoso.com 
``` 

![app-service-web-service-created](media/app-service-web-tutorial-domain-ssl/web-app-custom-domain.png)  

## <a name="step-4---bind-a-custom-ssl-certificate-to-your-web-app"></a>Krok 4 — wiązanie niestandardowe certyfikat SSL do aplikacji sieci web

Masz teraz aplikacji sieci web platformy Azure, wraz z nazwą domeny, w pasku adresu przeglądarki. Jednak jeśli przejdziesz do `https://<your_custom_domain>` teraz otrzymujesz błąd certyfikatu. 

![app-service-web-service-created](media/app-service-web-tutorial-domain-ssl/web-app-cert-error.png)  

Ten błąd występuje, ponieważ aplikacja sieci web nie ma jeszcze powiązanie certyfikatu SSL, który jest zgodny z niestandardowej nazwy domeny. Jednak nie występuje błąd, jeśli przejdziesz do `https://<app_name>.azurewebsites.net`. Jest to spowodowane aplikacji, a także wszystkie aplikacje w usłudze Azure App Service, jest zabezpieczony przy użyciu certyfikatu SSL dla `*.azurewebsites.net` domeny symbolu wieloznacznego domyślnie. 

Aby uzyskać dostęp do aplikacji sieci web przez niestandardową nazwę domeny, należy powiązać certyfikat protokołu SSL dla domeny niestandardowej aplikacji sieci web. Wykona go w tym kroku. 

### <a name="upload-the-ssl-certificate"></a>Przekaż certyfikat protokołu SSL

Przekaż certyfikat protokołu SSL dla domeny niestandardowej do aplikacji sieci web przy użyciu [az usługi aplikacji sieci web config ssl przekazywania](/cli/azure/appservice/web/config/ssl#upload) polecenia.

W poniższym poleceniu zastąp `<app_name>` z Twojej unikatowej nazwy aplikacji, `<path_to_ptx_file>` ze ścieżką do sieci. Plik PFX i `<password>` z hasło do certyfikatu. 

```azurecli
az appservice web config ssl upload --name <app_name> --resource-group myResourceGroup --certificate-file <path_to_pfx_file> --certificate-password <password> 
```

Po przekazaniu certyfikat interfejsu wiersza polecenia Azure zawiera informacje podobne do poniższego przykładu:

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

Z danych wyjściowych JSON `thumbprint` przedstawia odcisku palca certyfikatu przekazane. Skopiuj wartości na potrzeby kolejnego kroku.

### <a name="bind-the-uploaded-ssl-certificate-to-the-web-app"></a>Powiąż przekazany certyfikat SSL do aplikacji sieci web

Aplikacja sieci web ma teraz nazwę domeny niestandardowej, który ma i ma również certyfikat SSL, która zabezpiecza tej domeny niestandardowej. Tylko celu pozostało Aby powiązać certyfikat z przekazane do aplikacji sieci web. Można to zrobić przy użyciu [powiązania ssl konfiguracji sieci web appservice az](/cli/azure/appservice/web/config/ssl#bind) polecenia.

W poniższym poleceniu zastąp `<app_name>` z Twojej unikatowej nazwy aplikacji i `<thumbprint-from-previous-output>` o odcisk palca certyfikatu, który można pobrać z poprzednie polecenie. 

powiązania ssl sieci web config az appservice--name < nazwa_aplikacji >--myResourceGroup grupy zasobów — odcisk palca certyfikatu < odcisk palca z — poprzednie output > SNI ssl — typ

Gdy certyfikat jest powiązana z aplikacji sieci web, Azure CLI pokazuje informacje podobne do poniższego przykładu:

{"stanu dostępności": "Normal", "clientAffinityEnabled": ma wartość true, "clientCertEnabled": ma wartość FAŁSZ, "cloningInfo": null, "containerSize": 0, "dailyMemoryTimeQuota": 0, "defaultHostName": "< nazwa_aplikacji >. azurewebsites.net", "enabled": true "enabledHostNames": ["www.contoso.com", "< nazwa_aplikacji >. azurewebsites.net", "< nazwa_aplikacji >. scm.azurewebsites.net"], "gatewaySiteName": null, "hostNameSslStates": [{"hostType": "Standardowy", "name": "< nazwa_aplikacji >. azurewebsites.net", "sslState": "Wyłączone", "odcisk palca": null, "toUpdate": wartość null, "wirtualnego adresu IP": null}, {"hostType": "Repository", "name": "< nazwa_aplikacji >. scm.azurewebsites.net", "sslState": "Wyłączone" "odcisk palca": null, "toUpdate": null, "wirtualnego adresu IP": wartości null}, {"hostType": "Standardowy", "name": "www.contoso.com", "sslState": "SniEnabled", "odcisk palca": "9FD1D2D06E2293673E2A8D1CA484A092BD016D00", "toUpdate": null, "wirtualnego adresu IP": wartości null}], "nazwy hostów": ["www.contoso.com", "< nazwa_aplikacji >. azurewebsites.net"], "hostNamesDisabled": ma wartość FAŁSZ, "hostingEnvironmentProfile": null, "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/site s / < nazwa_aplikacji >", "isDefaultContainer": null "typu": "Aplikacja sieci Web", "lastModifiedTimeUtc": "2017-03-29T14:36:18.803333", "Lokalizacja": "Europa Zachodnia", "maxNumberOfWorkers": null, "Mikrousługi": "false", "Nazwa": "< nazwa_aplikacji >" "outboundIpAddresses": "13.94.143.57,13.94.136.57,40.68.199.146,13.94.138.55,13.94.140.1", "premiumAppDeployed": null, "repositorySiteName": "< nazwa_aplikacji >", "zastrzeżone": false "w grupie zasobów": "myResourceGroup", "scmSiteAlsoStopped": ma wartość FAŁSZ, "serverFarmId": "/ subskrypcji/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/dostawców/Microsof t.Web/serverfarms/myAppServicePlan", "siteConfig": null, "slotSwapStatus": null, "stan": "Uruchomiona", "suspendedTill": null "tagi": null, "targetSwapSlot": null, "trafficManagerHostNames": null, "type": "Microsoft.Web/sites", "usageState": "Normal"}

W przeglądarce przejdź do punktu końcowego protokołu HTTPS z niestandardowej nazwy domeny. Na przykład:

```
https://www.contoso.com 
``` 

![app-service-web-service-created](media/app-service-web-tutorial-domain-ssl/web-app-ssl-success.png)  

## <a name="more-resources"></a>Więcej zasobów

[Kupowanie i konfigurowanie niestandardowej nazwy domeny w usłudze Azure App Service](custom-dns-web-site-buydomains-web-app.md)
[kupowanie i konfigurowanie certyfikatu SSL usługi aplikacji Azure](web-sites-purchase-ssl-web-site.md)
