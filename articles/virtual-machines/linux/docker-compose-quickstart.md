---
title: "aaaUse rozwiązania Docker Compose na maszynie Wirtualnej systemu Linux na platformie Azure | Dokumentacja firmy Microsoft"
description: Jak toouse Docker i tworzenia maszyn wirtualnych systemu Linux z hello wiersza polecenia platformy Azure
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 02ab8cf9-318d-4a28-9d0c-4a31dccc2a84
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: cf7254ad4813ccdc641fcacbb06ed1514a93cee5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-docker-and-compose-toodefine-and-run-a-multi-container-application-in-azure"></a>Pobierz wprowadzenie toodefine Docker i redagowanie i uruchomić aplikację usługi kontenera platformy Azure
Z [Redaguj](http://github.com/docker/compose), użyj toodefine plik prosty tekst aplikacja składająca się z wielu kontenerów Docker. Następnie pokrętła się na aplikację w jednym poleceniem, który jest toodeploy zdefiniowanych środowiska. Na przykład w tym artykule opisano sposób tooquickly konfigurowania bloga WordPress z wewnętrznej bazy danych MariaDB SQL bazy danych na maszynie Wirtualnej systemu Ubuntu. Umożliwia także tooset Redaguj się bardziej złożonych aplikacji.


## <a name="set-up-a-linux-vm-as-a-docker-host"></a>Skonfiguruj Maszynę wirtualną systemu Linux jako Docker host
Można użyć różnych procedur Azure i dostępnych obrazów lub szablony Menedżera zasobów w hello Azure Marketplace toocreate Maszynę wirtualną systemu Linux i skonfigurować jako hosta Docker. Na przykład, zobacz [przy użyciu środowiska hello rozszerzenia maszyny Wirtualnej platformy Docker toodeploy](dockerextension.md) tooquickly tworzenia maszyny Wirtualnej systemu Ubuntu z hello rozszerzenia maszyny Wirtualnej platformy Docker Azure za pomocą [szablon szybkiego startu](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu). 

Gdy używasz rozszerzenia maszyny Wirtualnej platformy Docker hello maszyny Wirtualnej jest automatycznie skonfigurowany jako Docker host i redagowanie jest już zainstalowana.


### <a name="create-docker-host-with-azure-cli-20"></a>Utwórz hosta Docker 2.0 interfejsu wiersza polecenia platformy Azure
Najnowsza wersja hello instalacji [Azure CLI 2.0](/cli/azure/install-az-cli2) i zaloguj się za pomocą konta Azure tooan [logowania az](/cli/azure/#login).

Najpierw utwórz grupę zasobów dla danego środowiska Docker [Tworzenie grupy az](/cli/azure/group#create). Witaj poniższy przykład tworzy grupę zasobów o nazwie *myResourceGroup* w hello *westus* lokalizacji:

```azurecli
az group create --name myResourceGroup --location westus
```

Następnie Wdróż maszynę Wirtualną za pomocą [Utwórz wdrożenie grupy az](/cli/azure/group/deployment#create) zawierająca rozszerzenia maszyny Wirtualnej Azure Docker hello [tego szablonu usługi Azure Resource Manager w witrynie GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu). Podać własne wartości *newStorageAccountName*, *adminUsername*, *adminPassword*, i *dnsNameForPublicIP*:

```azurecli
az group deployment create --resource-group myResourceGroup \
  --parameters '{"newStorageAccountName": {"value": "mystorageaccount"},
    "adminUsername": {"value": "azureuser"},
    "adminPassword": {"value": "P@ssw0rd!"},
    "dnsNameForPublicIP": {"value": "mypublicdns"}}' \
  --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/docker-simple-on-ubuntu/azuredeploy.json
```

Trwa kilka minut, aż hello toofinish wdrożenia. Po ukończeniu wdrażania hello [Przenieś krok toonext](#verify-that-compose-is-installed) tooyour tooSSH maszyny Wirtualnej. 

Opcjonalnie dodaj monit toohello zwracany kontroli tooinstead i hello umożliwiają wdrożenie nadal w tle hello hello `--no-wait` Flaga toohello poprzedzających polecenia. Dzięki temu tooperform pracować w hello CLI wdrożenia hello kontynuuje kilka minut. Można wyświetlić szczegółowe informacje o stanie hosta Docker hello z [az maszyny wirtualnej pokazu](/cli/azure/vm#show). Hello poniższy przykład umożliwia sprawdzenie stanu hello hello maszyny Wirtualnej o nazwie *myDockerVM* (hello domyślną nazwę szablonu hello — nie zmieniać tej nazwy) w grupie zasobów hello o nazwie *myResourceGroup*:

```azurecli
az vm show \
    --resource-group myResourceGroup \
    --name myDockerVM \
    --query [provisioningState] \
    --output tsv
```

Jeśli to polecenie zwraca *zakończyło się pomyślnie*, hello wdrożenia zostało ukończone i można toohello SSH maszyny Wirtualnej w powitania po kroku.


## <a name="verify-that-compose-is-installed"></a>Sprawdź, czy Redaguj jest zainstalowany
Po ukończeniu wdrażania hello SSH tooyour nowego Docker hosta przy użyciu nazwy DNS hello podane podczas wdrażania. Można użyć `az vm show -g myResourceGroup -n myDockerVM -d --query [fqdns] -o tsv` tooview szczegóły maszyny wirtualnej, łącznie z nazwą DNS hello.

```bash
ssh azureuser@mypublicdns.westus.cloudapp.azure.com
```

toocheck, które tworzą jest zainstalowany na powitania maszynę Wirtualną, uruchom następujące polecenie hello:

```bash
docker-compose --version
```

Zbyt wyświetlone dane wyjściowe podobne*rozwiązania docker compose 1.6.2, kompilacji 4d 72027*.

> [!TIP]
> Jeśli użyto innej metody toocreate hostów Docker i muszą tooinstall tworzą samodzielnie, zobacz hello [tworzą dokumentacji](https://github.com/docker/compose/blob/882dc673ce84b0b29cd59b6815cb93f74a6c4134/docs/install.md).


## <a name="create-a-docker-composeyml-configuration-file"></a>Utwórz plik docker-compose.yml konfiguracji
Następnie należy utworzyć `docker-compose.yml` pliku, który jest tylko plik konfiguracji tekstu, toodefine hello Docker kontenery toorun na powitania maszyny Wirtualnej. Plik Hello określa toorun obraz powitania w każdego kontenera (lub może być kompilacji z plik Dockerfile), zmienne środowiskowe niezbędne i zależności, porty i hello łącza między kontenerów. Aby uzyskać więcej informacji o składni pliku yml, zobacz [tworzą odwołanie do pliku](https://docs.docker.com/compose/compose-file/).

Utwórz hello *docker-compose.yml* plików w następujący sposób:

```bash
touch docker-compose.yml
```

Użyj Twojej tooadd Edytor tekstu pliku toohello niektórych danych. Witaj poniższym przykładzie użyto hello *vi* edytora:

```bash
vi docker-compose.yml
```

Witaj Wklej poniższy przykład w pliku tekstowym. Ta konfiguracja korzysta z obrazów z hello [rejestru DockerHub](https://registry.hub.docker.com/_/wordpress/) tooinstall WordPress (hello typu open source obsługi blogów i system zarządzania zawartością) i połączone wewnętrznej bazy danych MariaDB SQL bazy danych. Wprowadź własne *MYSQL_ROOT_PASSWORD* w następujący sposób:

```sh
wordpress:
  image: wordpress
  links:
    - db:mysql
  ports:
    - 80:80

db:
  image: mariadb
  environment:
    MYSQL_ROOT_PASSWORD: <your password>
```

## <a name="start-hello-containers-with-compose"></a>Kontenery hello zaczynać się Redaguj
W hello sam katalogu jako sieci *docker-compose.yml* pliku, uruchom następujące polecenie hello (w zależności od środowiska, może być konieczne toorun `docker-compose` przy użyciu `sudo`):

```bash
docker-compose up -d
```

To polecenie uruchamia kontenery Docker hello określone w *docker-compose.yml*. Trwa minutę lub dwie na toocomplete ten krok. Zostaną wyświetlone dane wyjściowe toohello podobnie poniższy przykład:

```bash
Creating wordpress_db_1...
Creating wordpress_wordpress_1...
...
```

> [!NOTE]
> Należy się hello toouse **-d** opcja uruchamiania, aby uruchomić w tle hello stale hello kontenerów.


tooverify, który kontenery hello są włączone, typ `docker-compose ps`. Powinien zostać wyświetlony wyglądać mniej więcej tak:

```bash
        Name                       Command               State         Ports
-----------------------------------------------------------------------------------
azureuser_db_1          docker-entrypoint.sh mysqld      Up      3306/tcp
azureuser_wordpress_1   docker-entrypoint.sh apach ...   Up      0.0.0.0:80->80/tcp
```

Teraz możesz połączyć tooWordPress bezpośrednio na powitania maszyny Wirtualnej na porcie 80. Otwórz przeglądarkę sieci web i wprowadź nazwę DNS hello maszyny wirtualnej (takie jak `http://mypublicdns.westus.cloudapp.azure.com`). Powinna zostać wyświetlona hello WordPress uruchomić ekranu, w którym można ukończyć powitalnych instalację i wprowadzenie do aplikacji hello.

![Ekran startowy WordPress][wordpress_start]

## <a name="next-steps"></a>Następne kroki
* Przejdź toohello [Podręcznik użytkownika rozszerzenia maszyny Wirtualnej platformy Docker](https://github.com/Azure/azure-docker-extension/blob/master/README.md) więcej opcji tooconfigure Docker i Redaguj w maszynie Wirtualnej platformy Docker. Na przykład jedną z opcji jest tooput hello Redaguj yml pliku (przekonwertowanego tooJSON) bezpośrednio w konfiguracji hello hello rozszerzenia maszyny Wirtualnej platformy Docker.
* Zapoznaj się z hello [tworzą wiersza polecenia](http://docs.docker.com/compose/reference/) i [Podręcznik użytkownika](http://docs.docker.com/compose/) więcej przykładów dotyczących tworzenia i wdrażania aplikacji usługi kontenera.
* Albo użyj szablonu usługi Azure Resource Manager, Twoje własne lub jeden przyczyniły się z hello [społeczności](https://azure.microsoft.com/documentation/templates/), skonfigurować toodeploy maszyny Wirtualnej platformy Azure, aplikacji i Docker Compose. Na przykład Witaj [wdrażanie bloga WordPress z rozwiązaniem Docker z](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-wordpress-mysql) szablon używa Docker i redagowanie tooquickly wdrażanie WordPress z wewnętrznej bazy danych MySQL na maszynie Wirtualnej systemu Ubuntu.
* Spróbuj integrowanie rozwiązania Docker Compose z klastrem Docker Swarm. Zobacz [przy użyciu tworzą z Swarm](https://docs.docker.com/compose/swarm/) dla scenariuszy.

<!--Image references-->

[wordpress_start]: media/docker-compose-quickstart/WordPress.png
