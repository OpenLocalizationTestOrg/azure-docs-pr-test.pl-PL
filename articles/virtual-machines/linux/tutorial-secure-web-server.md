---
title: "aaaSecure certyfikaty serwera sieci web przy użyciu protokołu SSL na platformie Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak certyfikaty serwera sieci web NGINX hello toosecure przy użyciu protokołu SSL na maszynie Wirtualnej systemu Linux na platformie Azure"
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
ms.date: 07/17/2017
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: d3a62d77ac05c9aa2a44356b7c8e44cb485b81aa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="secure-a-web-server-with-ssl-certificates-on-a-linux-virtual-machine-in-azure"></a>Zabezpieczenia serwera sieci web z certyfikatów SSL na maszynie wirtualnej systemu Linux na platformie Azure
serwery sieci web toosecure, certyfikat później SSL (Secure Sockets) mogą być używane tooencrypt ruchu w sieci web. Te certyfikaty SSL mogą być przechowywane w usłudze Azure Key Vault i umożliwia bezpieczne wdrażanie certyfikatów tooLinux o maszynach wirtualnych (VM) na platformie Azure. Ten samouczek zawiera informacje na temat wykonywania następujących czynności:

> [!div class="checklist"]
> * Tworzenie usługi Azure Key Vault
> * Generowanie lub Przekaż certyfikat toohello magazyn kluczy
> * Utwórz maszynę Wirtualną i zainstaluj serwer sieci web NGINX hello
> * Wstaw hello certyfikatu do hello maszyny Wirtualnej i skonfigurować NGINX wraz z powiązaniem SSL

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Jeśli wybierz tooinstall i użyj interfejsu wiersza polecenia hello lokalnie, w tym samouczku wymaga działają hello Azure CLI w wersji 2.0.4 lub nowszej. Uruchom `az --version` toofind hello wersji. Jeśli potrzebujesz tooinstall lub uaktualniania, zobacz [zainstalować Azure CLI 2.0]( /cli/azure/install-azure-cli).  


## <a name="overview"></a>Omówienie
Usługa Azure Key Vault zabezpiecza kluczy kryptograficznych i kluczy tajnych takich certyfikatów lub hasła. Magazyn kluczy pozwala uprościć proces zarządzania hello certyfikatu i umożliwia toomaintain kontrolę nad kluczami, które uzyskują dostęp do tych certyfikatów. Można utworzyć certyfikatu z podpisem własnym wewnątrz usługi Key Vault, lub Przekaż istniejących, zaufanego certyfikatu, który już następującą.

Zamiast przy użyciu niestandardowego obrazu maszyny Wirtualnej, który zawiera certyfikaty rozszerzania w, wstrzyknąć certyfikatów do uruchomionej maszyny Wirtualnej. Ten proces zapewnia, że certyfikaty aktualną hello są zainstalowane na serwerze sieci web podczas wdrażania. Jeśli możesz odnowić lub zastąpić certyfikat, nie masz również toocreate nowego niestandardowego obrazu maszyny Wirtualnej. Hello najnowsze certyfikaty są automatycznie dodane podczas tworzenia dodatkowych maszyn wirtualnych. W trakcie całego procesu hello certyfikaty hello nigdy nie pozostaw hello platformy Azure lub są widoczne w skrypcie, Historia wiersza polecenia lub szablonu.


## <a name="create-an-azure-key-vault"></a>Tworzenie usługi Azure Key Vault
Przed utworzeniem magazyn kluczy i certyfikatów, Utwórz nową grupę zasobów o [Tworzenie grupy az](/cli/azure/group#create). Witaj poniższy przykład tworzy grupę zasobów o nazwie *myResourceGroupSecureWeb* w hello *eastus* lokalizacji:

```azurecli-interactive 
az group create --name myResourceGroupSecureWeb --location eastus
```

Następnie należy utworzyć magazyn kluczy o [az keyvault utworzyć](/cli/azure/keyvault#create) i włącz ją do użycia podczas wdrażania maszyny Wirtualnej. Każdy magazyn kluczy wymaga unikatowej nazwy i powinna być małe litery. Zastąp  *<mykeyvault>*  w hello poniższy przykład z własną unikatową nazwę usługi Key Vault:

```azurecli-interactive 
keyvault_name=<mykeyvault>
az keyvault create \
    --resource-group myResourceGroupSecureWeb \
    --name $keyvault_name \
    --enabled-for-deployment
```

## <a name="generate-a-certificate-and-store-in-key-vault"></a>Wygeneruj certyfikat i przechowywania w magazynie kluczy
W środowisku produkcyjnym, należy zaimportować prawidłowy certyfikat podpisane przez zaufanego dostawcę z [importu certyfikatów keyvault az](/cli/azure/certificate#import). W tym samouczku hello poniższym przykładzie pokazano, jak można wygenerować certyfikatu z podpisem własnym z [utworzenia certyfikatu keyvault az](/cli/azure/certificate#create) używającą hello domyślne zasady certyfikatu:

```azurecli-interactive 
az keyvault certificate create \
    --vault-name $keyvault_name \
    --name mycert \
    --policy "$(az keyvault certificate get-default-policy)"
```

### <a name="prepare-a-certificate-for-use-with-a-vm"></a>Przygotowanie certyfikat do użycia z maszyny Wirtualnej
certyfikat hello toouse podczas hello maszyny Wirtualnej utworzyć procesu, uzyskać identyfikator hello certyfikatu z [az keyvault wersje klucza tajnego listy-](/cli/azure/keyvault/secret#list-versions). Konwertuj hello certyfikatu z [az wirtualna format klucz tajny](/cli/azure/vm#format-secret). Poniższy przykład Hello przypisuje hello dane wyjściowe tych poleceń toovariables dla łatwość użycia w hello następne kroki:

```azurecli-interactive 
secret=$(az keyvault secret list-versions \
          --vault-name $keyvault_name \
          --name mycert \
          --query "[?attributes.enabled].id" --output tsv)
vm_secret=$(az vm format-secret --secret "$secret")
```

### <a name="create-a-cloud-init-config-toosecure-nginx"></a>Tworzenie chmury init config toosecure NGINX
[Init chmury](https://cloudinit.readthedocs.io) jest toocustomize podejścia powszechnie używaną Maszynę wirtualną systemu Linux rozruchu dla powitania po raz pierwszy. Można użyć pakietów tooinstall init chmury i zapisywać pliki, lub użytkowników tooconfigure i zabezpieczeń. Jak init chmury jest uruchamiany podczas hello początkowego procesu rozruchu, nie istnieją żadne dodatkowe czynności lub wymagane tooapply agentów konfiguracji.

Podczas tworzenia maszyny Wirtualnej, certyfikaty i klucze są przechowywane w hello chronione */var/lib/agentawaagent/* katalogu. Dodawanie tooautomate hello toohello certyfikatów maszyny Wirtualnej i konfigurowanie serwera sieci web hello, użyj init chmury. W tym przykładzie mamy Instalowanie i konfigurowanie serwera sieci web NGINX hello. Można użyć hello sam przetwarzania tooinstall i skonfigurować Apache. 

Utwórz plik o nazwie *chmurze init-web-server.txt* i Wklej hello następującej konfiguracji:

```yaml
#cloud-config
package_upgrade: true
packages:
  - nginx
write_files:
  - owner: www-data:www-data
  - path: /etc/nginx/sites-available/default
    content: |
      server {
        listen 443 ssl;
        ssl_certificate /etc/nginx/ssl/mycert.cert;
        ssl_certificate_key /etc/nginx/ssl/mycert.prv;
      }
runcmd:
  - secretsname=$(find /var/lib/waagent/ -name "*.prv" | cut -c -57)
  - mkdir /etc/nginx/ssl
  - cp $secretsname.crt /etc/nginx/ssl/mycert.cert
  - cp $secretsname.prv /etc/nginx/ssl/mycert.prv
  - service nginx restart
```

### <a name="create-a-secure-vm"></a>Tworzenie bezpiecznej maszyny Wirtualnej
Teraz Utwórz maszynę Wirtualną z [tworzenia maszyny wirtualnej az](/cli/azure/vm#create). dane certyfikatu Hello jest wprowadzona z usługi Key Vault z hello `--secrets` parametru. Przekaż w konfiguracji chmury init hello z hello `--custom-data` parametru:

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroupSecureWeb \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init-web-server.txt \
    --secrets "$vm_secret"
```

Trwa kilka minut, aż hello toobe maszyny Wirtualnej utworzone, tooinstall pakietów hello i toostart aplikacji hello. Po utworzeniu hello maszyny Wirtualnej, zwróć uwagę na powitania `publicIpAddress` wyświetlanych przez hello wiersza polecenia platformy Azure. Ten adres jest używany tooaccess witryny w przeglądarce sieci web.

tooallow secure tooreach ruchu w sieci web z maszyną Wirtualną, otwórz port 443 z hello Internet z [port Otwórz az maszyny wirtualnej](/cli/azure/vm#open-port):

```azurecli-interactive 
az vm open-port \
    --resource-group myResourceGroupSecureWeb \
    --name myVM \
    --port 443
```


### <a name="test-hello-secure-web-app"></a>Przetestuj aplikację sieci web bezpiecznego hello
Teraz możesz otworzyć przeglądarkę sieci web i wprowadź *https://<publicIpAddress>*  na pasku adresu hello. Podaj własny publicznego adresu IP z hello maszyny Wirtualnej utworzyć procesu. Jeśli używasz certyfikatu z podpisem własnym, zaakceptuj ostrzeżenie o zabezpieczeniach hello:

![Zaakceptuj ostrzeżenie o zabezpieczeniach przeglądarki sieci web](./media/tutorial-secure-web-server/browser-warning.png)

Następnie wyświetleniem zabezpieczonej witrynie NGINX jak hello poniższy przykład:

![Uruchamianie zabezpieczoną witryną NGINX widoku](./media/tutorial-secure-web-server/secured-nginx.png)


## <a name="next-steps"></a>Następne kroki

W tym samouczku NGINX serwera sieci web jest zabezpieczony za pomocą certyfikatu SSL, przechowywane w usłudze Azure Key Vault. W tym samouczku omówiono:

> [!div class="checklist"]
> * Tworzenie usługi Azure Key Vault
> * Generowanie lub Przekaż certyfikat toohello magazyn kluczy
> * Utwórz maszynę Wirtualną i zainstaluj serwer sieci web NGINX hello
> * Wstaw hello certyfikatu do hello maszyny Wirtualnej i skonfigurować NGINX wraz z powiązaniem SSL

Postępuj zgodnie z tym toosee łącze wstępnie skompilowany przykłady skryptów maszyny wirtualnej.

> [!div class="nextstepaction"]
> [Przykłady skryptów maszyny wirtualnej systemu Windows](./cli-samples.md)