---
title: "Zarządzanie klastrem Azure DC/OS z interfejsu API REST platformy Marathon"
description: "Wdrażanie kontenerów do klastra usługi kontenera platformy Azure DC/OS przy użyciu interfejsu API REST platformy Marathon."
services: container-service
author: dlepow
manager: timlt
ms.service: container-service
ms.topic: article
ms.date: 04/04/2017
ms.author: danlep
ms.custom: mvc
ms.openlocfilehash: c9322756c30011305ebe6f4f2fd38554f275a1b3
ms.sourcegitcommit: 5d3e99478a5f26e92d1e7f3cec6b0ff5fbd7cedf
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/06/2017
---
# <a name="dcos-container-management-through-the-marathon-rest-api"></a>Zarządzanie kontenerem DC/OS przy użyciu interfejsu API REST platformy Marathon

Platforma DC/OS dostarcza środowisko wdrażania i skalowania obciążeń klastrowanych, zapewniając jednocześnie abstrakcyjność sprzętu bazowego. Ponad systemem DC/OS istnieje platforma, która zarządza planowaniem i wykonywaniem obciążeń obliczeniowych. Platformy są dostępne dla wielu popularnych zadań, ten dokument stanowi wprowadzenie tworzenie i skalować wdrożenia kontenerów przy użyciu interfejsu API REST platformy Marathon. 

## <a name="prerequisites"></a>Wymagania wstępne

Przed przystąpieniem do pracy nad tymi przykładami będziesz potrzebować klastra DC/OS skonfigurowanego w usłudze kontenera platformy Azure. Potrzebna będzie także zdalna łączność z tym klastrem. Aby uzyskać więcej informacji na temat tych elementów, zobacz następujące artykuły:

* [Wdrażanie klastra usługi Azure Container Service](container-service-deployment.md)
* [Łączenie z klastrem usługi Azure Container Service](../container-service-connect.md)

## <a name="access-the-dcos-apis"></a>Dostęp do interfejsów API platformy DC/OS
Po nawiązaniu połączeniu z klastrem usługi kontenera platformy Azure masz dostęp do platformy DC/OS i powiązanych interfejsów API REST pod adresem http://localhost:local-port. W przykładach przedstawionych w tym dokumencie założono, że tunelowanie korzysta z portu 80. Na przykład punkty końcowe platformy Marathon można połączyć się z na identyfikatory URI rozpoczynające się od `http://localhost/marathon/v2/`. 

Aby uzyskać więcej informacji o różnych interfejsach API, zobacz dokumentację Mesosphere dotyczącą [interfejsu API platformy Marathon](https://mesosphere.github.io/marathon/docs/rest-api.html) i [interfejsu API programu Chronos](https://mesos.github.io/chronos/docs/api.html) oraz dokumentację Apache dotyczącą [interfejsu API aplikacji Mesos Scheduler](http://mesos.apache.org/documentation/latest/scheduler-http-api/).

## <a name="gather-information-from-dcos-and-marathon"></a>Gromadzenie informacji z platform DC/OS i Marathon
Przed wdrożeniem kontenerów do klastra DC/OS Zbierz określone informacje o klastrze DC/OS, takie jak nazwy i stan agentów DC/OS. W tym celu wykonaj zapytanie w punkcie końcowym `master/slaves` interfejsu API REST platformy DC/OS. Jeśli operacja zostanie wykonana pomyślnie, zapytanie zwróci listę agentów DC/OS i szereg właściwości każdego z nich.

```bash
curl http://localhost/mesos/master/slaves
```

Teraz użyj punktu końcowego `/apps` platformy Marathon, aby sprawdzić bieżące wdrożenia aplikacji w klastrze DC/OS. Jeśli jest to nowy klaster, pojawi się pusta tablica aplikacji.

```bash
curl localhost/marathon/v2/apps

{"apps":[]}
```

## <a name="deploy-a-docker-formatted-container"></a>Wdrażanie kontenera w formacie programu Docker
Kontenery w formacie Docker za pośrednictwem interfejsu API REST platformy Marathon można wdrożyć przy użyciu pliku JSON, który opisuje zamierzone wdrożenie. Poniższy przykład wdraża kontener Nginx prywatny agenta w klastrze. 

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

Do wdrożenia kontenera formacie programu Docker, przechowuj plik JSON w dostępnej lokalizacji. Następnie w celu wdrożenia kontenera uruchom następujące polecenie. Określ nazwę pliku JSON (`marathon.json` w tym przykładzie).

```bash
curl -X POST http://localhost/marathon/v2/apps -d @marathon.json -H "Content-type: application/json"
```

Dane wyjściowe będą podobne do następujących:

```json
{"version":"2015-11-20T18:59:00.494Z","deploymentId":"b12f8a73-f56a-4eb1-9375-4ac026d6cdec"}
```

Teraz po wykonaniu zapytania dotyczącego aplikacji na platformie Marathon nowa aplikacja pojawi się w danych wyjściowych.

```bash
curl localhost/marathon/v2/apps
```

## <a name="reach-the-container"></a>Osiągnąć kontenera

Aby sprawdzić, czy Nginx działa w kontenerze w jednej z prywatnych agentów w klastrze. Aby znaleźć hosta i portu, na którym jest uruchomiona kontenera, zapytanie Marathon uruchomione zadania: 

```bash
curl localhost/marathon/v2/tasks
```

Znajdź wartość `host` w danych wyjściowych (podobnie jak adres IP `10.32.0.x`), a wartością `ports`.


Teraz należy terminali połączenia SSH (nie połączeń tunelowych) do zarządzania nazwy FQDN klastra. Po nawiązaniu połączenia, wprowadź następujące żądania, zastępując poprawne wartości `host` i `ports`:

```bash
curl http://host:ports
```

Dane wyjściowe server Nginx jest podobny do następującego:

![Nginx z kontenera](./media/container-service-mesos-marathon-rest/nginx.png)




## <a name="scale-your-containers"></a>Skalowanie kontenerów
Interfejsu API platformy Marathon umożliwia skalowanie w poziomie oraz skalowanie w przypadku wdrożeń aplikacji. W poprzednim przykładzie wdrożono jedno wystąpienie aplikacji. Wykonamy teraz skalowanie w poziomie, aby uzyskać trzy wystąpienia aplikacji. W tym celu utwórz plik JSON zawierający następujący tekst JSON i zapisz go w dostępnej lokalizacji.

```json
{ "instances": 3 }
```

Z tunelowane połączenie uruchom następujące polecenie, aby skalować aplikację w poziomie.

> [!NOTE]
> Identyfikator URI będzie mieć postać http://localhost/marathon/v2/apps/ z dołączonym identyfikatorem aplikacji do skalowania. W przypadku użycia przedstawionej tutaj przykładowej aplikacji Nginx identyfikator URI będzie mieć postać http://localhost/marathon/v2/apps/nginx.
> 
> 

```bash
curl http://localhost/marathon/v2/apps/nginx -H "Content-type: application/json" -X PUT -d @scale.json
```

Na koniec wykonaj zapytanie dotyczące aplikacji w punkcie końcowym platformy Marathon. Widoczne będą trzy kontenery Nginx.

```bash
curl localhost/marathon/v2/apps
```

## <a name="equivalent-powershell-commands"></a>Równoważne polecenia programu PowerShell
Te same akcje można wykonać za pomocą poleceń programu PowerShell w systemie Windows.

Aby zebrać informacje dotyczące klastra DC/OS, takie jak nazwy i stan agenta, uruchom następujące polecenie:

```powershell
Invoke-WebRequest -Uri http://localhost/mesos/master/slaves
```

Kontenery w formacie programu Docker można wdrażać za pośrednictwem platformy Marathon przy użyciu pliku JSON, który opisuje zamierzone wdrożenie. W poniższym przykładzie wdrożono kontener Nginx, który powiąże port 80 agenta DC/OS z portem 80 kontenera.

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

Do wdrożenia kontenera formacie programu Docker, przechowuj plik JSON w dostępnej lokalizacji. Następnie w celu wdrożenia kontenera uruchom następujące polecenie. Określ ścieżkę do pliku JSON (`marathon.json` w tym przykładzie).

```powershell
Invoke-WebRequest -Method Post -Uri http://localhost/marathon/v2/apps -ContentType application/json -InFile 'c:\marathon.json'
```

Interfejs API platformy Marathon umożliwia także skalowanie w poziomie oraz skalowanie na zewnątrz wdrożeń aplikacji. W poprzednim przykładzie wdrożono jedno wystąpienie aplikacji. Wykonamy teraz skalowanie w poziomie, aby uzyskać trzy wystąpienia aplikacji. W tym celu utwórz plik JSON zawierający następujący tekst JSON i zapisz go w dostępnej lokalizacji.

```json
{ "instances": 3 }
```

Uruchom następujące polecenie, aby skalować aplikację w poziomie:

> [!NOTE]
> Identyfikator URI będzie mieć postać http://localhost/marathon/v2/apps/ z dołączonym identyfikatorem aplikacji do skalowania. W przypadku użycia przedstawionej tutaj przykładowej aplikacji Nginx, identyfikator URI będzie mieć postać http://localhost/marathon/v2/apps/nginx.
> 
> 

```powershell
Invoke-WebRequest -Method Put -Uri http://localhost/marathon/v2/apps/nginx -ContentType application/json -InFile 'c:\scale.json'
```

## <a name="next-steps"></a>Następne kroki
* [Więcej informacji na temat punktów końcowych HTTP platformy Mesos](http://mesos.apache.org/documentation/latest/endpoints/)
* [Więcej informacji na temat interfejsu API REST platformy Marathon](https://mesosphere.github.io/marathon/docs/rest-api.html)

