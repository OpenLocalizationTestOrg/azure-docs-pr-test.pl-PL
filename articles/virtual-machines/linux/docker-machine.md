---
title: "obsługuje aaaUse maszyny Docker toocreate systemu Linux na platformie Azure | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak obsługuje toouse maszyny Docker toocreate Docker na platformie Azure."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
ms.assetid: 164b47de-6b17-4e29-8b7d-4996fa65bea4
ms.service: virtual-machines-linux
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 06/19/2017
ms.author: iainfou
ms.openlocfilehash: 905c645add51c78305aac85a7013441b3a73972f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-docker-machine-toocreate-hosts-in-azure"></a>Jak obsługuje toouse toocreate maszyny Docker na platformie Azure
Ten sposób artykuł szczegóły toouse [Docker maszyny](https://docs.docker.com/machine/) toocreate hostów na platformie Azure. Witaj `docker-machine` polecenie tworzy maszynę wirtualną systemu Linux (VM) na platformie Azure, a następnie instaluje Docker. Następnie można zarządzać hostach Docker w Azure przy użyciu hello tych samych narzędzi lokalnych i przepływów pracy.

## <a name="create-vms-with-docker-machine"></a>Tworzenie maszyn wirtualnych z maszyną Docker
Najpierw uzyskać identyfikator subskrypcji platformy Azure z [Pokaż konto az](/cli/azure/account#show) w następujący sposób:

```azurecli
sub=$(az account show --query "id" -o tsv)
```

Tworzenie maszyn wirtualnych z hostów Docker na platformie Azure z `docker-machine create` , określając *azure* jako hello sterownika. Aby uzyskać więcej informacji, zobacz hello [dokumentacji Docker Azure sterownika](https://docs.docker.com/machine/drivers/azure/)

Witaj poniższy przykład tworzy Maszynę wirtualną o nazwie *myVM*, tworzy konto użytkownika o nazwie *azureuser*i powoduje otwarcie portu *80* hello hosta maszyny Wirtualnej. Wykonaj wszystkie monity toolog w tooyour konto platformy Azure i udzielić toocreate uprawnienia maszyny Docker zasobów i zarządzanie nimi.

```bash
docker-machine create -d azure \
    --azure-subscription-id $sub \
    --azure-ssh-user azureuser \
    --azure-open-port 80 \
    myvm
```

Witaj dane wyjściowe wyglądają toohello podobnie poniższy przykład:

```bash
Creating CA: /Users/user/.docker/machine/certs/ca.pem
Creating client certificate: /Users/user/.docker/machine/certs/cert.pem
Running pre-create checks...
(myvmdocker) Completed machine pre-create checks.
Creating machine...
(myvmdocker) Querying existing resource group.  name="docker-machine"
(myvmdocker) Creating resource group.  name="docker-machine" location="westus"
(myvmdocker) Configuring availability set.  name="docker-machine"
(myvmdocker) Configuring network security group.  name="myvmdocker-firewall" location="westus"
(myvmdocker) Querying if virtual network already exists.  rg="docker-machine" location="westus" name="docker-machine-vnet"
(myvmdocker) Creating virtual network.  name="docker-machine-vnet" rg="docker-machine" location="westus"
(myvmdocker) Configuring subnet.  name="docker-machine" vnet="docker-machine-vnet" cidr="192.168.0.0/16"
(myvmdocker) Creating public IP address.  name="myvmdocker-ip" static=false
(myvmdocker) Creating network interface.  name="myvmdocker-nic"
(myvmdocker) Creating storage account.  sku=Standard_LRS name="vhdski0hvfazyd8mn991cg50" location="westus"
(myvmdocker) Creating virtual machine.  location="westus" size="Standard_A2" username="azureuser" osImage="canonical:UbuntuServer:16.04.0-LTS:latest" name="myvmdocker"
Waiting for machine toobe running, this may take a few minutes...
Detecting operating system of created instance...
Waiting for SSH toobe available...
Detecting hello provisioner...
Provisioning with ubuntu(systemd)...
Installing Docker...
Copying certs toohello local machine directory...
Copying certs toohello remote machine...
Setting Docker configuration on hello remote daemon...
Checking connection tooDocker...
Docker is up and running!
toosee how tooconnect your Docker Client toohello Docker Engine running on this virtual machine, run: docker-machine env myvmdocker
```

## <a name="configure-your-docker-shell"></a>Skonfiguruj powłoki Docker
tooconnect tooyour Docker hosta na platformie Azure, zdefiniować hello odpowiednie ustawienia połączeń. Jak wspomniano w końcu hello hello dane wyjściowe, wyświetlić hello informacje o połączeniu dla hosta Docker w następujący sposób: 

```bash
docker-machine env myvmdocker
```

Witaj danych wyjściowych jest toohello podobnie poniższy przykład:

```bash
export DOCKER_TLS_VERIFY="1"
export DOCKER_HOST="tcp://40.68.254.142:2376"
export DOCKER_CERT_PATH="/Users/user/.docker/machine/machines/machine"
export DOCKER_MACHINE_NAME="machine"
# Run this command tooconfigure your shell:
# eval $(docker-machine env myvmdocker)
```

Ustawienia połączenia hello toodefine można albo wykonywania hello sugerowana Konfiguracja polecenia (`eval $(docker-machine env myvmdocker)`), lub ręcznie ustawić zmienne środowiskowe hello. 

## <a name="run-a-container"></a>Uruchom kontenera
toosee kontenera akcji, umożliwia uruchamianie podstawowy serwer sieci Web NGINX. Tworzenie kontenera z `docker run` i ujawnia port 80 dla ruchu w sieci web w następujący sposób:

```bash
docker run -d -p 80:80 --restart=always nginx
```

Witaj danych wyjściowych jest toohello podobnie poniższy przykład:

```bash
Unable toofind image 'nginx:latest' locally
latest: Pulling from library/nginx
ff3d52d8f55f: Pull complete
226f4ec56ba3: Pull complete
53d7dd52b97d: Pull complete
Digest: sha256:41ad9967ea448d7c2b203c699b429abe1ed5af331cd92533900c6d77490e0268
Status: Downloaded newer image for nginx:latest
675e6056cb81167fe38ab98bf397164b01b998346d24e567f9eb7a7e94fba14a
```

Widok uruchomionych kontenerów z `docker ps`. Witaj następujące przykładowe dane wyjściowe wyglądają kontener NGINX hello uruchomiony z portu 80 udostępniane:

```bash
CONTAINER ID    IMAGE    COMMAND                   CREATED          STATUS          PORTS                          NAMES
d5b78f27b335    nginx    "nginx -g 'daemon off"    5 minutes ago    Up 5 minutes    0.0.0.0:80->80/tcp, 443/tcp    festive_mirzakhani
```

## <a name="test-hello-container"></a>Kontener testu hello
Uzyskaj hello publiczny adres IP hosta Docker w następujący sposób:


```bash
docker-machine ip myvmdocker
```

kontener hello toosee akcji, otwórz przeglądarkę sieci web i wprowadź hello publicznego adresu IP w danych wyjściowych hello hello poprzedzających polecenia:

![Kontener ngnix uruchomione](./media/docker-machine/nginx.png)

## <a name="next-steps"></a>Następne kroki
Można również utworzyć hostów z hello [rozszerzenia maszyny Wirtualnej platformy Docker](dockerextension.md). Przykłady przy użyciu rozwiązania Docker Compose można znaleźć [wprowadzenie Docker i redagowanie na platformie Azure](docker-compose-quickstart.md).
