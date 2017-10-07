---
title: aaaManage Azure DC/OS klaster z interfejsu API REST platformy Marathon | Dokumentacja firmy Microsoft
description: "Wdrażanie klastra usługi kontenera platformy Azure DC/OS tooan kontenerów przy użyciu hello interfejsu API REST platformy Marathon."
services: container-service
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Docker, kontenery, mikrousługi, Mesos, Azure"
ms.assetid: c7175446-4507-4a33-a7a2-63583e5996e3
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/04/2017
ms.author: danlep
ms.custom: mvc
ms.openlocfilehash: d926b9b90f5d4eda85a015d9ea0d96fea2c4b566
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="dcos-container-management-through-hello-marathon-rest-api"></a>Zarządzanie kontenerem DC/OS przy użyciu hello interfejsu API REST platformy Marathon
DC/OS udostępnia środowisko wdrażania i skalowania obciążeń klastrowanych, zapewniając jednocześnie abstrakcyjność sprzętu źródłowego hello. Ponad systemem DC/OS istnieje platforma, która zarządza planowaniem i wykonywaniem obciążeń obliczeniowych. Platformy są dostępne dla wielu popularnych zadań, ten dokument stanowi wprowadzenie tworzenia i skalowania wdrożenia kontenerów przy użyciu hello interfejsu API REST platformy Marathon. 

## <a name="prerequisites"></a>Wymagania wstępne

Przed przystąpieniem do pracy nad tymi przykładami będziesz potrzebować klastra DC/OS skonfigurowanego w usłudze kontenera platformy Azure. Należy również toohave łączności zdalnej toothis klastra. Aby uzyskać więcej informacji na temat tych elementów zobacz następujące artykuły hello:

* [Wdrażanie klastra usługi Azure Container Service](container-service-deployment.md)
* [Łączenie tooan klastra usługi kontenera platformy Azure](../container-service-connect.md)

## <a name="access-hello-dcos-apis"></a>Witaj dostępu do interfejsów API DC/OS
Po są połączone toohello klastra usługi kontenera platformy Azure, możesz uzyskać dostęp do hello DC/OS i powiązanych interfejsów API REST, za pośrednictwem portu http://localhost:local. Przykłady Hello w tym dokumencie założono, że tunelowanie korzysta na porcie 80. Na przykład punkty końcowe platformy Marathon hello jest osiągalna na identyfikatory URI rozpoczynające się od `http://localhost/marathon/v2/`. 

Aby uzyskać więcej informacji na temat hello różnych interfejsów API, zobacz hello dokumentację Mesosphere dotyczącą hello [interfejsu API platformy Marathon](https://mesosphere.github.io/marathon/docs/rest-api.html) i [Chronos interfejsu API](https://mesos.github.io/chronos/docs/api.html)oraz dokumentację Apache dotyczącą hello [Mesos API harmonogramu ](http://mesos.apache.org/documentation/latest/scheduler-http-api/).

## <a name="gather-information-from-dcos-and-marathon"></a>Gromadzenie informacji z platform DC/OS i Marathon
Przed wdrożeniem klastra DC/OS toohello kontenery Zbierz określone informacje o klastrze DC/OS hello, takich jak nazwy hello i stan agentów DC/OS hello. toodo zapytanie tak, hello `master/slaves` punkt końcowy hello interfejsu API REST platformy DC/OS. Jeśli wszystko odbędzie się poprawnie, hello zapytanie zwraca listę agentów DC/OS i szereg właściwości każdego.

```bash
curl http://localhost/mesos/master/slaves
```

Teraz, przy użyciu platformy Marathon hello `/apps` toocheck punktu końcowego dla bieżącego klastra DC/OS toohello wdrożeń aplikacji. Jeśli jest to nowy klaster, pojawi się pusta tablica aplikacji.

```bash
curl localhost/marathon/v2/apps

{"apps":[]}
```

## <a name="deploy-a-docker-formatted-container"></a>Wdrażanie kontenera w formacie programu Docker
Kontenery w formacie Docker za pośrednictwem interfejsu API REST platformy Marathon hello wdrażania przy użyciu pliku JSON, który opisuje hello zamierzone wdrożenie. Witaj poniższego przykładu wdraża Nginx kontenera tooa prywatny agenta hello klastra. 

```json
{
  "id": "nginx",
  "cpus": 0.1,
  "mem": 32.0,
  "instances": 1,
  "container": {
    "type": "DOCKER",
    "docker": {
      "image": "nginx",
      "network": "BRIDGE",
      "portMappings": [
        { "containerPort": 80, "servicePort": 9000, "protocol": "tcp" }
      ]
    }
  }
}
```

toodeploy formacie programu Docker kontenerze, przechowywania pliku JSON hello w dostępnej lokalizacji. Następnie toodeploy hello kontener, uruchom następujące polecenie hello. Określ nazwę pliku JSON hello hello (`marathon.json` w tym przykładzie).

```bash
curl -X POST http://localhost/marathon/v2/apps -d @marathon.json -H "Content-type: application/json"
```

dane wyjściowe Hello są podobne toohello następujące czynności:

```json
{"version":"2015-11-20T18:59:00.494Z","deploymentId":"b12f8a73-f56a-4eb1-9375-4ac026d6cdec"}
```

Teraz po wykonaniu zapytania Marathon dla aplikacji, ta nowa aplikacja pojawi się w danych wyjściowych hello.

```bash
curl localhost/marathon/v2/apps
```

## <a name="reach-hello-container"></a>Osiągnąć hello kontenera

Możesz zweryfikować tego hello Nginx jest uruchomione w kontenerze na jednym z agentów prywatnej hello w klastrze hello. toofind hello hosta i portu, w którym jest uruchomiona kontenera hello, kwerendy Marathon hello uruchomionych zadań: 

```bash
curl localhost/marathon/v2/tasks
```

Znajdź wartość hello `host` w danych wyjściowych hello (adresów IP podobny zbyt`10.32.0.x`) i wartość hello `ports`.


Teraz należy SSH terminali (nie połączeń tunelowych) toohello zarządzania połączeniami nazwy FQDN klastra hello. Po nawiązaniu połączenia należy hello następujące żądania, zastępując wartości poprawne hello `host` i `ports`:

```bash
curl http://host:ports
```

Hello dane wyjściowe server Nginx jest podobne toohello następujące czynności:

![Nginx z kontenera](./media/container-service-mesos-marathon-rest/nginx.png)




## <a name="scale-your-containers"></a>Skalowanie kontenerów
W przypadku wdrożeń aplikacji, można użyć tooscale interfejsu API platformy Marathon hello out lub skali. W poprzednim przykładzie hello wdrożono jedno wystąpienie aplikacji. Przeprowadź skalowanie tę możliwość toothree wystąpienia aplikacji. toodo tak, Utwórz plik JSON przy użyciu powitania po tekst JSON i zapisze go w dostępnej lokalizacji.

```json
{ "instances": 3 }
```

Z połączeniem tunelowane Uruchom hello następujące polecenia tooscale limit aplikacji hello.

> [!NOTE]
> Witaj identyfikatora URI jest http://localhost/marathon/v2/apps/ następuje identyfikator hello tooscale aplikacji hello. Jeśli używasz hello przykład Nginx, który znajduje się w tym miejscu, hello identyfikator URI będzie http://localhost/marathon/v2/apps/nginx.
> 
> 

```bash
curl http://localhost/marathon/v2/apps/nginx -H "Content-type: application/json" -X PUT -d @scale.json
```

Na koniec wykonaj zapytanie hello punktu końcowego platformy Marathon dla aplikacji. Widoczne będą trzy kontenery Nginx.

```bash
curl localhost/marathon/v2/apps
```

## <a name="equivalent-powershell-commands"></a>Równoważne polecenia programu PowerShell
Te same akcje można wykonać za pomocą poleceń programu PowerShell w systemie Windows.

toogather informacje o klastrze DC/OS hello, takich jak nazwy i stan agenta, uruchom następujące polecenie hello:

```powershell
Invoke-WebRequest -Uri http://localhost/mesos/master/slaves
```

Kontenery w formacie Docker za pośrednictwem platformy Marathon wdrażania przy użyciu pliku JSON, który opisuje hello zamierzone wdrożenie. Witaj następującym przykładowym wdraża hello kontener Nginx, powiązania z portem 80 tooport agenta DC/OS hello 80 kontenera hello.

```json
{
  "id": "nginx",
  "cpus": 0.1,
  "mem": 32.0,
  "instances": 1,
  "container": {
    "type": "DOCKER",
    "docker": {
      "image": "nginx",
      "network": "BRIDGE",
      "portMappings": [
        { "containerPort": 80, "servicePort": 9000, "protocol": "tcp" }
      ]
    }
  }
}
```

toodeploy formacie programu Docker kontenerze, przechowywania pliku JSON hello w dostępnej lokalizacji. Następnie toodeploy hello kontener, uruchom następujące polecenie hello. Określ plik JSON toohello ścieżka hello (`marathon.json` w tym przykładzie).

```powershell
Invoke-WebRequest -Method Post -Uri http://localhost/marathon/v2/apps -ContentType application/json -InFile 'c:\marathon.json'
```

W przypadku wdrożeń aplikacji, można użyć tooscale interfejsu API platformy Marathon hello out lub skali. W poprzednim przykładzie hello wdrożono jedno wystąpienie aplikacji. Przeprowadź skalowanie tę możliwość toothree wystąpienia aplikacji. toodo tak, Utwórz plik JSON przy użyciu powitania po tekst JSON i zapisze go w dostępnej lokalizacji.

```json
{ "instances": 3 }
```

Witaj uruchom następujące polecenie tooscale limit aplikacji hello:

> [!NOTE]
> Witaj identyfikatora URI jest http://localhost/marathon/v2/apps/ następuje identyfikator hello tooscale aplikacji hello. Jeśli używasz hello Nginx przykładu dostępnego w tym miejscu, hello identyfikator URI będzie http://localhost/marathon/v2/apps/nginx.
> 
> 

```powershell
Invoke-WebRequest -Method Put -Uri http://localhost/marathon/v2/apps/nginx -ContentType application/json -InFile 'c:\scale.json'
```

## <a name="next-steps"></a>Następne kroki
* [Więcej informacji na temat punktów końcowych HTTP platformy Mesos hello](http://mesos.apache.org/documentation/latest/endpoints/)
* [Więcej informacji na temat hello interfejsu API REST platformy Marathon](https://mesosphere.github.io/marathon/docs/rest-api.html)

