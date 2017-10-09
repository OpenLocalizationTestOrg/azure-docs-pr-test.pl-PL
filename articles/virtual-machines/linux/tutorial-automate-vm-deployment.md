---
title: aaaCustomize maszyny Wirtualnej systemu Linux, po pierwszym uruchomieniu komputera na platformie Azure | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak inicjowaniem chmury toouse i Key Vault toocustomze maszyn wirtualnych systemu Linux powitania po raz pierwszy one rozruchu w systemie Azure"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 08/11/2017
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: 280189723ac0205226f9c0068bd605da13249ace
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocustomize-a-linux-virtual-machine-on-first-boot"></a>Jak toocustomize maszyny wirtualnej systemu Linux, po pierwszym uruchomieniu komputera
W poprzednich instrukcji możesz przedstawiono sposób maszyny wirtualnej tooa tooSSH (VM) i ręcznie zainstalować NGINX. wymagane jest zwykle toocreate maszyn wirtualnych w szybki i spójny sposób jakiegoś automatyzacji. Typowe toocustomize podejście maszyny Wirtualnej po pierwszym uruchomieniu komputera jest toouse [init chmury](https://cloudinit.readthedocs.io). Ten samouczek zawiera informacje na temat wykonywania następujących czynności:

> [!div class="checklist"]
> * Utwórz plik konfiguracji init chmury
> * Utwórz maszynę Wirtualną, która używa pliku init chmury
> * Wyświetlanie działającej aplikacji Node.js po powitalne zostanie utworzona maszyna wirtualna
> * Użyj usługi Key Vault toosecurely magazyn certyfikatów
> * Automatyzacja bezpiecznego wdrażania z NGINX z inicjowaniem chmury


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Jeśli wybierz tooinstall i użyj interfejsu wiersza polecenia hello lokalnie, w tym samouczku wymaga działają hello Azure CLI w wersji 2.0.4 lub nowszej. Uruchom `az --version` toofind hello wersji. Jeśli potrzebujesz tooinstall lub uaktualniania, zobacz [zainstalować Azure CLI 2.0]( /cli/azure/install-azure-cli).  



## <a name="cloud-init-overview"></a>Init chmury — omówienie
[Init chmury](https://cloudinit.readthedocs.io) jest toocustomize podejścia powszechnie używaną Maszynę wirtualną systemu Linux rozruchu dla powitania po raz pierwszy. Można użyć pakietów tooinstall init chmury i zapisywać pliki, lub użytkowników tooconfigure i zabezpieczeń. Jak init chmury jest uruchamiany podczas hello początkowego procesu rozruchu, nie istnieją żadne dodatkowe czynności lub wymagane tooapply agentów konfiguracji.

Init chmury działa także w dystrybucji. Na przykład nie używaj **instalacji stanie get** lub **yum zainstalować** tooinstall pakietu. Zamiast tego można zdefiniować listę tooinstall pakietów. Init chmury automatycznie używa narzędzia do zarządzania natywnego pakietu hello distro hello, którą wybierzesz.

Możemy pracy z naszych partnerów tooget chmury inicjowania uwzględnione i Praca w obrazach hello udostępniają one tooAzure. Witaj w poniższej tabeli przedstawiono hello bieżącej dostępności init chmury na obrazy platformy Azure:

| Alias | Wydawca | Oferta | SKU | Wersja |
|:--- |:--- |:--- |:--- |:--- |:--- |
| UbuntuLTS |Canonical |UbuntuServer |16.04 LTS |najnowsza |
| UbuntuLTS |Canonical |UbuntuServer |14.04.5-LTS |najnowsza |
| CoreOS |CoreOS |CoreOS |Stable |najnowsza |


## <a name="create-cloud-init-config-file"></a>Utwórz plik konfiguracji init chmury
inicjowaniem chmury toosee akcji, utwórz maszynę Wirtualną, która instaluje NGINX i uruchamia prostej aplikacji Node.js "Hello World". powitania po konfiguracji chmury init instaluje hello wymagane pakiety, utworzenie aplikacji Node.js, a następnie zainicjować i uruchomienie aplikacji hello.

W bieżącym powłoki, Utwórz plik o nazwie *init.txt chmury* i Wklej powitania po konfiguracji. Na przykład utworzyć plik hello w hello powłoki chmury nie na komputerze lokalnym. Można użyć dowolnego edytora, którego chcesz. Wprowadź `sensible-editor cloud-init.txt` toocreate hello pliku i wyświetlić listę dostępnych edytory. Upewnij się, że plik całego init chmury hello został poprawnie skopiowany, szczególnie hello pierwszy wiersz:

```yaml
#cloud-config
package_upgrade: true
packages:
  - nginx
  - nodejs
  - npm
write_files:
  - owner: www-data:www-data
  - path: /etc/nginx/sites-available/default
    content: |
      server {
        listen 80;
        location / {
          proxy_pass http://localhost:3000;
          proxy_http_version 1.1;
          proxy_set_header Upgrade $http_upgrade;
          proxy_set_header Connection keep-alive;
          proxy_set_header Host $host;
          proxy_cache_bypass $http_upgrade;
        }
      }
  - owner: azureuser:azureuser
  - path: /home/azureuser/myapp/index.js
    content: |
      var express = require('express')
      var app = express()
      var os = require('os');
      app.get('/', function (req, res) {
        res.send('Hello World from host ' + os.hostname() + '!')
      })
      app.listen(3000, function () {
        console.log('Hello world app listening on port 3000!')
      })
runcmd:
  - service nginx restart
  - cd "/home/azureuser/myapp"
  - npm init
  - npm install express -y
  - nodejs index.js
```

Aby uzyskać więcej informacji o opcjach konfiguracji chmury init, zobacz [przykłady konfiguracji chmury init](https://cloudinit.readthedocs.io/en/latest/topics/examples.html).

## <a name="create-virtual-machine"></a>Tworzenie maszyny wirtualnej
Przed utworzeniem maszyny Wirtualnej, Utwórz nową grupę zasobów o [Tworzenie grupy az](/cli/azure/group#create). Witaj poniższy przykład tworzy grupę zasobów o nazwie *myResourceGroupAutomate* w hello *eastus* lokalizacji:

```azurecli-interactive 
az group create --name myResourceGroupAutomate --location eastus
```

Teraz Utwórz maszynę Wirtualną z [tworzenia maszyny wirtualnej az](/cli/azure/vm#create). Użyj hello `--custom-data` toopass parametru w pliku config init chmury. Podaj hello pełną ścieżkę toohello *init.txt chmury* konfiguracji w przypadku zapisania pliku hello poza istnieje katalog roboczy. Witaj poniższy przykład tworzy Maszynę wirtualną o nazwie *myAutomatedVM*:

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroupAutomate \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init.txt
```

Trwa kilka minut, aż hello toobe maszyny Wirtualnej utworzone, tooinstall pakietów hello i toostart aplikacji hello. Istnieją zadania w tle, które nadal toorun po hello Azure CLI zwraca toohello wiersza. Może to być inny kilka minut, w celu uzyskania dostępu do aplikacji hello. Po utworzeniu hello maszyny Wirtualnej, zwróć uwagę na powitania `publicIpAddress` wyświetlanych przez hello wiersza polecenia platformy Azure. Ten adres jest aplikacja Node.js hello tooaccess używane za pośrednictwem przeglądarki sieci web.

tooallow web tooreach ruch maszyny Wirtualnej, otwórz port 80 z hello Internet z [port Otwórz az maszyny wirtualnej](/cli/azure/vm#open-port):

```azurecli-interactive 
az vm open-port --port 80 --resource-group myResourceGroupAutomate --name myVM
```

## <a name="test-web-app"></a>Przetestuj aplikację sieci web
Teraz możesz otworzyć przeglądarkę sieci web i wprowadź *http://<publicIpAddress>*  na pasku adresu hello. Podaj własny publicznego adresu IP z hello maszyny Wirtualnej utworzyć procesu. Aplikacja Node.js jest wyświetlana tak jak hello poniższy przykład:

![Wyświetl uruchomione NGINX lokacji](./media/tutorial-automate-vm-deployment/nginx.png)


## <a name="inject-certificates-from-key-vault"></a>Wstaw certyfikaty z magazynu kluczy
W tej sekcji opcjonalne przedstawiono, jak można bezpiecznie certyfikaty są przechowywane w usłudze Azure Key Vault i wstrzyknąć podczas hello wdrożenia maszyny Wirtualnej. Zamiast przy użyciu niestandardowego obrazu, który zawiera certyfikaty hello rozszerzania programu, ten proces zapewnia, że hello najbardziej aktualne certyfikaty są wstrzykiwane tooa maszyny Wirtualnej po pierwszym uruchomieniu komputera. W trakcie hello certyfikatu hello nigdy nie opuszcza hello platformy Azure lub jest widoczna w skryptu, Historia wiersza polecenia lub szablonu.

Usługa Azure Key Vault zabezpiecza kluczy kryptograficznych i kluczy tajnych, takich jak certyfikaty lub hasła. Key Vault ułatwia usprawnić proces zarządzania kluczami hello i umożliwia toomaintain kontrolę nad kluczami, które dostępu i szyfrowania danych. W tym scenariuszu przedstawiono niektóre toocreate pojęcia magazyn kluczy i użycia certyfikatu, jednak nie jest wyczerpujący Przegląd na temat toouse magazynu kluczy.

Hello następujące kroki pokazują, jak można:

- Tworzenie usługi Azure Key Vault
- Generowanie lub Przekaż certyfikat toohello magazyn kluczy
- Utwórz klucz tajny z tooinject certyfikatu hello w tooa maszyny Wirtualnej
- Utwórz maszynę Wirtualną i wstrzyknąć hello certyfikatu

### <a name="create-an-azure-key-vault"></a>Tworzenie usługi Azure Key Vault
Najpierw utwórz magazyn kluczy o [az keyvault utworzyć](/cli/azure/keyvault#create) i włącz ją do użycia podczas wdrażania maszyny Wirtualnej. Każdy magazyn kluczy wymaga unikatowej nazwy i powinna być małe litery. Zastąp *mykeyvault* w hello poniższy przykład z własną unikatową nazwę usługi Key Vault:

```azurecli-interactive 
keyvault_name=mykeyvault
az keyvault create \
    --resource-group myResourceGroupAutomate \
    --name $keyvault_name \
    --enabled-for-deployment
```

### <a name="generate-certificate-and-store-in-key-vault"></a>Generowanie certyfikatu i przechowywania w magazynie kluczy
W środowisku produkcyjnym, należy zaimportować prawidłowy certyfikat podpisane przez zaufanego dostawcę z [importu certyfikatów keyvault az](/cli/azure/keyvault/certificate#import). W tym samouczku hello poniższym przykładzie pokazano, jak można wygenerować certyfikatu z podpisem własnym z [utworzenia certyfikatu keyvault az](/cli/azure/keyvault/certificate#create) używającą hello domyślne zasady certyfikatu:

```azurecli-interactive 
az keyvault certificate create \
    --vault-name $keyvault_name \
    --name mycert \
    --policy "$(az keyvault certificate get-default-policy)"
```


### <a name="prepare-certificate-for-use-with-vm"></a>Przygotowywanie certyfikatów do użytku z maszyną Wirtualną.
certyfikat hello toouse podczas hello maszyny Wirtualnej utworzyć procesu, uzyskać identyfikator hello certyfikatu z [az keyvault wersje klucza tajnego listy-](/cli/azure/keyvault/secret#list-versions). Hello maszyna wirtualna wymaga certyfikatu hello tooinject format go podczas rozruchu, więc przekonwertować hello certyfikatu z [az wirtualna format klucz tajny](/cli/azure/vm#format-secret). Poniższy przykład Hello przypisuje hello dane wyjściowe tych poleceń toovariables dla łatwość użycia w hello następne kroki:

```azurecli-interactive 
secret=$(az keyvault secret list-versions \
          --vault-name $keyvault_name \
          --name mycert \
          --query "[?attributes.enabled].id" --output tsv)
vm_secret=$(az vm format-secret --secret "$secret")
```


### <a name="create-cloud-init-config-toosecure-nginx"></a>Tworzenie chmury init config toosecure NGINX
Podczas tworzenia maszyny Wirtualnej, certyfikaty i klucze są przechowywane w hello chronione */var/lib/agentawaagent/* katalogu. tooautomate Dodawanie hello certyfikatu toohello maszyny Wirtualnej i skonfigurowaniu NGINX, można użyć konfiguracji zaktualizowane init chmury z poprzedniego przykładu hello.

Utwórz plik o nazwie *chmurze init-secured.txt* i Wklej powitania po konfiguracji. Ponownie Jeśli używasz hello powłoki chmury, Utwórz plik konfiguracji init chmury hello, występują, a nie na komputerze lokalnym. Użyj `sensible-editor cloud-init-secured.txt` toocreate hello pliku i wyświetlić listę dostępnych edytory. Upewnij się, że plik całego init chmury hello został poprawnie skopiowany, szczególnie hello pierwszy wiersz:

```yaml
#cloud-config
package_upgrade: true
packages:
  - nginx
  - nodejs
  - npm
write_files:
  - owner: www-data:www-data
  - path: /etc/nginx/sites-available/default
    content: |
      server {
        listen 80;
        listen 443 ssl;
        ssl_certificate /etc/nginx/ssl/mycert.cert;
        ssl_certificate_key /etc/nginx/ssl/mycert.prv;
        location / {
          proxy_pass http://localhost:3000;
          proxy_http_version 1.1;
          proxy_set_header Upgrade $http_upgrade;
          proxy_set_header Connection keep-alive;
          proxy_set_header Host $host;
          proxy_cache_bypass $http_upgrade;
        }
      }
  - owner: azureuser:azureuser
  - path: /home/azureuser/myapp/index.js
    content: |
      var express = require('express')
      var app = express()
      var os = require('os');
      app.get('/', function (req, res) {
        res.send('Hello World from host ' + os.hostname() + '!')
      })
      app.listen(3000, function () {
        console.log('Hello world app listening on port 3000!')
      })
runcmd:
  - secretsname=$(find /var/lib/waagent/ -name "*.prv" | cut -c -57)
  - mkdir /etc/nginx/ssl
  - cp $secretsname.crt /etc/nginx/ssl/mycert.cert
  - cp $secretsname.prv /etc/nginx/ssl/mycert.prv
  - service nginx restart
  - cd "/home/azureuser/myapp"
  - npm init
  - npm install express -y
  - nodejs index.js
```

### <a name="create-secure-vm"></a>Tworzenie bezpiecznej maszyny Wirtualnej
Teraz Utwórz maszynę Wirtualną z [tworzenia maszyny wirtualnej az](/cli/azure/vm#create). dane certyfikatu Hello jest wprowadzona z usługi Key Vault z hello `--secrets` parametru. Jak w poprzednim przykładzie hello, należy także podać w konfiguracji chmury init hello z hello `--custom-data` parametru:

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroupAutomate \
    --name myVMSecured \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init-secured.txt \
    --secrets "$vm_secret"
```

Trwa kilka minut, aż hello toobe maszyny Wirtualnej utworzone, tooinstall pakietów hello i toostart aplikacji hello. Istnieją zadania w tle, które nadal toorun po hello Azure CLI zwraca toohello wiersza. Może to być inny kilka minut, w celu uzyskania dostępu do aplikacji hello. Po utworzeniu hello maszyny Wirtualnej, zwróć uwagę na powitania `publicIpAddress` wyświetlanych przez hello wiersza polecenia platformy Azure. Ten adres jest aplikacja Node.js hello tooaccess używane za pośrednictwem przeglądarki sieci web.

tooallow secure tooreach ruchu w sieci web z maszyną Wirtualną, otwórz port 443 z hello Internet z [port Otwórz az maszyny wirtualnej](/cli/azure/vm#open-port):

```azurecli-interactive 
az vm open-port \
    --resource-group myResourceGroupAutomate \
    --name myVMSecured \
    --port 443
```

### <a name="test-secure-web-app"></a>Przetestuj aplikację sieci web bezpiecznego
Teraz możesz otworzyć przeglądarkę sieci web i wprowadź *https://<publicIpAddress>*  na pasku adresu hello. Podaj własny publicznego adresu IP z hello maszyny Wirtualnej utworzyć procesu. Jeśli używasz certyfikatu z podpisem własnym, zaakceptuj ostrzeżenie o zabezpieczeniach hello:

![Zaakceptuj ostrzeżenie o zabezpieczeniach przeglądarki sieci web](./media/tutorial-automate-vm-deployment/browser-warning.png)

Zabezpieczonej witrynie NGINX i Node.js jak hello poniższy przykład następnie jest wyświetlana aplikacja:

![Uruchamianie zabezpieczoną witryną NGINX widoku](./media/tutorial-automate-vm-deployment/secured-nginx.png)


## <a name="next-steps"></a>Następne kroki
W tym samouczku należy skonfigurować po pierwszym uruchomieniu komputera z inicjowaniem chmury maszyn wirtualnych. W tym samouczku omówiono:

> [!div class="checklist"]
> * Utwórz plik konfiguracji init chmury
> * Utwórz maszynę Wirtualną, która używa pliku init chmury
> * Wyświetlanie działającej aplikacji Node.js po powitalne zostanie utworzona maszyna wirtualna
> * Użyj usługi Key Vault toosecurely magazyn certyfikatów
> * Automatyzacja bezpiecznego wdrażania z NGINX z inicjowaniem chmury

Jak przejść dalej toolearn samouczka toohello toocreate niestandardowych obrazów maszyn wirtualnych.

> [!div class="nextstepaction"]
> [Tworzenie niestandardowych obrazów maszyn wirtualnych](./tutorial-custom-images.md)
