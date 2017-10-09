---
title: aaaManage Azure Swarm klaster z interfejsu API Docker | Dokumentacja firmy Microsoft
description: "Wdrażanie kontenerów tooa Docker Swarm klastra usługi kontenera platformy Azure"
services: container-service
documentationcenter: 
author: rgardler
manager: madhana
editor: 
tags: acs, azure-container-service
keywords: "Docker, kontenery, mikrousługi, Mesos, Azure"
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 09/13/2016
ms.author: rogardle
ms.custom: mvc
ms.openlocfilehash: bb9b07c82a7b48caeb2e351455797cbf2a6e7480
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="container-management-with-docker-swarm"></a>Zarządzanie kontenerami przy użyciu rozwiązania Docker Swarm
Rozwiązanie Docker Swarm oferuje środowisko wdrażania konteneryzowanych obciążeń w puli zestawów hostów Docker. Rozwiązanie docker Swarm używa hello natywnego interfejsu API Docker. Witaj przepływ pracy zarządzania kontenerami w rozwiązaniu Docker Swarm jest niemal identyczny toowhat, który będzie hostem jeden kontener. Ten dokument zawiera proste przykłady wdrażania konteneryzowanych obciążeń w wystąpieniu usługi kontenera platformy Azure w rozwiązaniu Docker Swarm. Szczegółową dokumentację dotyczącą rozwiązania Docker Swarm można znaleźć na stronie [Docker Swarm w witrynie Docker.com](https://docs.docker.com/swarm/).

[!INCLUDE [container-service-swarm-mode-note](../../../includes/container-service-swarm-mode-note.md)]

Wymagania wstępne dotyczące ćwiczeń toohello w tym dokumencie:

[Utworzenie klastra Swarm usługi Azure Container Service](container-service-deployment.md)

[Połącz z klastrem Swarm hello usługi kontenera platformy Azure](../container-service-connect.md)

## <a name="deploy-a-new-container"></a>Wdrażanie nowego kontenera
toocreate nowy kontener w hello Docker Swarm, użyj hello `docker run` polecenia (sprawdzeniu otwartych wzorców toohello tunelu SSH, zgodnie z harmonogramem powyższe wymagania wstępne hello). W tym przykładzie kontener jest tworzony z hello `yeasy/simple-web` obrazu:

```bash
user@ubuntu:~$ docker run -d -p 80:80 yeasy/simple-web

4298d397b9ab6f37e2d1978ef3c8c1537c938e98a8bf096ff00def2eab04bf72
```

Po utworzeniu kontenera hello, za pomocą `docker ps` tooreturn informacji na temat hello kontenera. Zauważ, znajduje się agent Swarm hello obsługujący hello kontenera:

```bash
user@ubuntu:~$ docker ps

CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                 NAMES
4298d397b9ab        yeasy/simple-web    "/bin/sh -c 'python i"   31 seconds ago      Up 9 seconds        10.0.0.5:80->80/tcp   swarm-agent-34A73819-1/happy_allen
```  

Można teraz uzyskać dostępu do aplikacji hello, która działa w tym kontenerze, za pośrednictwem hello publicznej nazwy DNS modułu równoważenia obciążenia agenta Swarm hello. Te informacje można znaleźć w portalu Azure hello:  

![Rzeczywiste wyniki dotyczące odwiedzin](./media/container-service-docker-swarm/real-visit.jpg)  

Domyślnie hello modułu równoważenia obciążenia ma porty 80, 8080 i 443 open. Jeśli chcesz, aby tooconnect na innym porcie należy tooopen ten port na powitania modułu równoważenia obciążenia Azure dla hello puli agenta.

## <a name="deploy-multiple-containers"></a>Wdrażanie wielu kontenerów
Uruchomiono wiele kontenerów, wykonując "Uruchom docker" wielokrotnie, program hello `docker ps` toosee polecenia, obsługującego kontenery hello są uruchomione na. W poniższym przykładzie hello trzy kontenery zostały rozmieszczone równomiernie w obrębie trzech agentów Swarm hello:  

```bash
user@ubuntu:~$ docker ps

CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                 NAMES
11be062ff602        yeasy/simple-web    "/bin/sh -c 'python i"   11 seconds ago      Up 10 seconds       10.0.0.6:83->80/tcp   swarm-agent-34A73819-2/clever_banach
1ff421554c50        yeasy/simple-web    "/bin/sh -c 'python i"   49 seconds ago      Up 48 seconds       10.0.0.4:82->80/tcp   swarm-agent-34A73819-0/stupefied_ride
4298d397b9ab        yeasy/simple-web    "/bin/sh -c 'python i"   2 minutes ago       Up 2 minutes        10.0.0.5:80->80/tcp   swarm-agent-34A73819-1/happy_allen
```  

## <a name="deploy-containers-by-using-docker-compose"></a>Wdrażanie kontenerów przy użyciu rozwiązania Docker Compose
Można użyć rozwiązania Docker Compose tooautomate hello wdrażania i konfigurowania wielu kontenerów. toodo tak, upewnij się, że utworzono tunel Secure Shell (SSH) i ustawiono zmienną DOCKER_HOST tego hello (patrz wymagania wstępne hello powyżej).

Utwórz plik docker-compose.yml w systemie lokalnym. toodo, użyj tego [próbki](https://raw.githubusercontent.com/rgardler/AzureDevTestDeploy/master/docker-compose.yml).

```bash
web:
  image: adtd/web:0.1
  ports:
    - "80:80"
  links:
    - rest:rest-demo-azure.marathon.mesos
rest:
  image: adtd/rest:0.1
  ports:
    - "8080:8080"

```

Uruchom `docker-compose up -d` toostart hello kontenera wdrożenia:

```bash
user@ubuntu:~/compose$ docker-compose up -d
Pulling rest (adtd/rest:0.1)...
swarm-agent-3B7093B8-0: Pulling adtd/rest:0.1... : downloaded
swarm-agent-3B7093B8-2: Pulling adtd/rest:0.1... : downloaded
swarm-agent-3B7093B8-3: Pulling adtd/rest:0.1... : downloaded
Creating compose_rest_1
Pulling web (adtd/web:0.1)...
swarm-agent-3B7093B8-3: Pulling adtd/web:0.1... : downloaded
swarm-agent-3B7093B8-0: Pulling adtd/web:0.1... : downloaded
swarm-agent-3B7093B8-2: Pulling adtd/web:0.1... : downloaded
Creating compose_web_1
```

Na koniec zostanie zwrócona lista uruchomionych kontenerów hello. Ta lista odzwierciedla hello kontenerów, które zostały wdrożone przy użyciu rozwiązania Docker Compose:

```bash
user@ubuntu:~/compose$ docker ps
CONTAINER ID        IMAGE               COMMAND                CREATED             STATUS              PORTS                     NAMES
caf185d221b7        adtd/web:0.1        "apache2-foreground"   2 minutes ago       Up About a minute   10.0.0.4:80->80/tcp       swarm-agent-3B7093B8-0/compose_web_1
040efc0ea937        adtd/rest:0.1       "catalina.sh run"      3 minutes ago       Up 2 minutes        10.0.0.4:8080->8080/tcp   swarm-agent-3B7093B8-0/compose_rest_1
```

Oczywiście można użyć `docker-compose ps` tooexamine tylko hello kontenerów zdefiniowanych w Twojej `compose.yml` pliku.

## <a name="next-steps"></a>Następne kroki
[Dowiedz się więcej na temat rozwiązania Docker Swarm](https://docs.docker.com/swarm/)

