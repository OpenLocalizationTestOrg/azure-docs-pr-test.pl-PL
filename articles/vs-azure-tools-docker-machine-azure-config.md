---
title: "obsługuje aaaCreate Docker na platformie Azure z maszyną Docker | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano Użyj hostów docker toocreate maszyny Docker na platformie Azure."
services: azure-container-service
documentationcenter: na
author: mlearned
manager: douge
editor: 
ms.assetid: 7a3ff6e1-fa93-4a62-b524-ab182d2fea08
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 06/08/2016
ms.author: mlearned
ms.openlocfilehash: fbf67e8189bbf33f874c4a9b619a931f28ccee12
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-docker-hosts-in-azure-with-docker-machine"></a>Tworzenie hostów platformy Docker na platformie Azure przy użyciu maszyny platformy Docker
Uruchomiona [Docker](https://www.docker.com/) kontenery wymaga hosta maszyny Wirtualnej uruchomionej hello docker demon.
W tym temacie opisano sposób toouse hello [docker maszyny](https://docs.docker.com/machine/) polecenia toocreate nowych maszyn wirtualnych systemu Linux, skonfigurowano hello demona Docker, działające na platformie Azure. 

**Uwaga:** 

* *W tym artykule zależy od 0.9.0-rc2 wersją maszyny docker lub większa*
* *Kontenery systemu Windows, które będą obsługiwane za pośrednictwem docker maszyny w hello Najbliższa przyszłość*

## <a name="create-vms-with-docker-machine"></a>Tworzenie maszyn wirtualnych z maszyną Docker
Tworzenie docker hosta maszyn wirtualnych na platformie Azure z hello `docker-machine create` polecenia przy użyciu hello `azure` sterownika. 

Hello Azure sterownik wymaga Twojego identyfikatora subskrypcji. Można użyć hello [interfejsu wiersza polecenia Azure](cli-install-nodejs.md) lub hello [Azure Portal](https://portal.azure.com) tooretrieve subskrypcji platformy Azure. 

**Przy użyciu hello portalu Azure**

* Wybierz **subskrypcje** z hello nawigacji po lewej stronie strony i skopiuj hello identyfikator subskrypcji.

**Przy użyciu hello wiersza polecenia platformy Azure**

* Typ ```azure account list``` i identyfikator subskrypcji hello kopiowania.

Typ `docker-machine create --driver azure` toosee hello opcje i ich wartości domyślne.
Możesz również sprawdzić hello [dokumentacji sterownika Azure Docker](https://docs.docker.com/machine/drivers/azure/) Aby uzyskać więcej informacji. 

Witaj poniższy przykład, opiera się na powitania [wartości domyślne](https://github.com/docker/machine/blob/master/drivers/azure/azure.go#L22), ale opcjonalnie ustawiona te wartości: 

* usługi Azure dns dla nazwy hello skojarzone z hello publicznego adresu IP i certyfikaty generowane. Jest to nazwa DNS hello maszyny wirtualnej. Hello maszyny Wirtualnej może, a następnie bezpiecznie Zatrzymaj, zwolnij hello dynamicznego adresu IP i podaj tooreconnect możliwości powitania po hello wirtualna uruchamia się ponownie z nowego adresu IP. Prefiks nazwy Hello musi być unikatowa w danym regionie UNIQUE_DNSNAME_PREFIX.westus.cloudapp.azure.com.
* Otwórz port 80 na powitania wirtualna wychodzący dostęp do Internetu
* rozmiar hello wirtualna tooutilize szybsze magazyn w warstwie premium
* Magazyn w warstwie Premium przeznaczony dla hello dysku maszyny wirtualnej

```
docker-machine create -d azure --azure-subscription-id <Your AZURE_SUBSCRIPTION_ID> --azure-dns <Your UNIQUE_DNSNAME_PREFIX> --azure-open-port 80 --azure-size Standard_DS1_v2 --azure-storage-type "Premium_LRS" mydockerhost 
```

## <a name="choose-a-docker-host-with-docker-machine"></a>Wybierz hosta z maszyną docker docker
Po utworzeniu wpisu docker maszyny dla hosta, możesz ustawić hello domyślnego hosta podczas uruchamiania polecenia docker.

## <a name="using-powershell"></a>Korzystanie z programu PowerShell
```powershell
docker-machine env MyDockerHost | Invoke-Expression 
```

## <a name="using-bash"></a>Przy użyciu Bash
```bash
eval $(docker-machine env MyDockerHost)
```

Teraz możesz uruchamiać polecenia docker na określonym hoście hello

```
docker ps
docker info
```

## <a name="run-a-container"></a>Uruchom kontenera
Z hosta skonfigurowane teraz możesz uruchomić tootest serwera sieci web proste czy host został skonfigurowany prawidłowo.
W tym miejscu wyświetlonym możemy użyć obrazu standardowe nginx, określ, czy powinien nasłuchiwać na porcie 80 i że hello hosta maszyny Wirtualnej zostanie ponownie uruchomiony, kontener hello spowoduje ponowne uruchomienie również (`--restart=always`). 

```bash
docker run -d -p 80:80 --restart=always nginx
```

dane wyjściowe Hello powinien wyglądać jak poniżej hello:

```
Unable toofind image 'nginx:latest' locally
latest: Pulling from library/nginx
efd26ecc9548: Pull complete
a3ed95caeb02: Pull complete
83f52fbfa5f8: Pull complete
fa664caa1402: Pull complete
Digest: sha256:12127e07a75bda1022fbd4ea231f5527a1899aad4679e3940482db3b57383b1d
Status: Downloaded newer image for nginx:latest
25942c35d86fe43c688d0c03ad478f14cc9c16913b0e1c2971cb32eb4d0ab721
```

## <a name="test-hello-container"></a>Kontener testu hello
Sprawdź uruchomionych kontenerów przy użyciu `docker ps`:

```bash
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                         NAMES
d5b78f27b335        nginx               "nginx -g 'daemon off"   5 minutes ago       Up 5 minutes        0.0.0.0:80->80/tcp, 443/tcp   goofy_mahavira
```

I hello toosee systemem kontenera, typu `docker-machine ip <VM name>` toofind hello IP address tooenter w przeglądarce hello:

```
PS C:\> docker-machine ip MyDockerHost
191.237.46.90
```

![Kontener ngnix uruchomione](./media/vs-azure-tools-docker-machine-azure-config/nginxsuccess.png)

## <a name="summary"></a>Podsumowanie
Docker komputera z można łatwo udostępnić hostów docker na platformie Azure dla operacji sprawdzania poprawności programu docker poszczególnych hosta.
W środowisku produkcyjnym hosting kontenerów, zobacz hello [usługi kontenera platformy Azure](http://aka.ms/AzureContainerService)

toodevelop .NET Core aplikacji za pomocą programu Visual Studio, zobacz [Docker Tools for Visual Studio](http://aka.ms/DockerToolsForVS)

