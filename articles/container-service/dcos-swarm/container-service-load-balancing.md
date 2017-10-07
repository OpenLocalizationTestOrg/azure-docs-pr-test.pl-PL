---
title: kontenery saldo aaaLoad w klastrze Azure DC/OS | Dokumentacja firmy Microsoft
description: "Zrównoważenia obciążenia w wielu kontenerów w klastrze usługi kontenera platformy Azure DC/OS."
services: container-service
documentationcenter: 
author: rgardler
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Kontenery, mikrousługi, DC/OS, Azure"
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/02/2017
ms.author: rogardle
ms.custom: mvc
ms.openlocfilehash: 2249cb06880cdb7e9a3aa94c0750c6a27316d349
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="load-balance-containers-in-an-azure-container-service-dcos-cluster"></a>Kontenery Równoważenie obciążenia klastra usługi kontenera platformy Azure DC/OS
W tym artykule firma Microsoft Poznaj jak toocreate wewnętrznego modułu równoważenia obciążenia w DC/OS zarządzane przy użyciu platformy Marathon-LB usługi kontenera platformy Azure. Ta konfiguracja umożliwia tooscale możesz aplikacji w poziomie. Można też tootake zaletą hello agenta publicznego i prywatnego klastrów przez umieszczenie z usługi równoważenia obciążenia w klastrze publicznego hello i kontenerów aplikacji w klastrze prywatnej hello. W tym samouczku zostały wykonane następujące czynności:

> [!div class="checklist"]
> * Konfigurowanie równoważenia obciążenia platformy Marathon
> * Wdrażanie aplikacji przy użyciu usługi równoważenia obciążenia hello
> * Konfigurowanie i modułu równoważenia obciążenia Azure

Należy ACS DC/OS hello toocomplete klastra kroków w tym samouczku. W razie potrzeby [w tym przykładzie skrypt](./../kubernetes/scripts/container-service-cli-deploy-dcos.md) można utworzyć.

Ten samouczek wymaga hello Azure CLI w wersji 2.0.4 lub nowszej. Uruchom `az --version` toofind hello wersji. Jeśli potrzebujesz tooupgrade, zobacz [zainstalować Azure CLI 2.0]( /cli/azure/install-azure-cli). 

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

## <a name="load-balancing-overview"></a>Równoważenie obciążenia — omówienie

Istnieją dwie warstwy równoważenia obciążenia w klastrze usługi kontenera platformy Azure DC/OS: 

**Moduł równoważenia obciążenia Azure** udostępnia publicznych punktów wejścia (hello dostęp do tych, że użytkownicy końcowi). Warstwa Azure LB jest udostępniany automatycznie przez usługi kontenera platformy Azure i jest domyślnie skonfigurowany tooexpose portu 80 i 443 8080.

**Witaj Marathon moduł równoważenia obciążenia (warstwa marathon-lb)** tras ruchu przychodzącego żądania toocontainer wystąpień, które usługi te żądania. Skalowania hello kontenerów świadczących naszej usługi sieci web, hello warstwa marathon-lb jest dynamicznie dostosowuje. Ten moduł równoważenia obciążenia nie jest dostępny domyślnie w usłudze kontenera, ale jest łatwe tooinstall.

## <a name="configure-marathon-load-balancer"></a>Konfigurowanie równoważenia obciążenia platformy Marathon

Moduł równoważenia obciążenia platformy Marathon dynamicznie ponownie konfiguruje oparty na powitania kontenerów, które zostały wdrożone. Istnieje również odporne toohello utratę kontenera lub agenta — jeśli dzieje się tak, Apache Mesos uruchomieniu hello kontener w innym miejscu i dostosowuje warstwa marathon-lb.

Hello uruchom następujące polecenie modułu równoważenia obciążenia platformy marathon hello tooinstall w klastrze hello agenta publicznego.

```azurecli-interactive
dcos package install marathon-lb
```

## <a name="deploy-load-balanced-application"></a>Wdrożenie aplikacji o zrównoważonym obciążeniu

Teraz, gdy mamy hello pakiet marathon-lb, możemy wdrożyć kontenera aplikacji czy Życzymy saldo tooload. 

Najpierw pobierz hello FQDN agentów hello publicznie udostępnione.

```azurecli-interactive
az acs list --resource-group myResourceGroup --query "[0].agentPoolProfiles[0].fqdn" --output tsv
```

Następnie utwórz plik o nazwie *hello web.json* i kopia w powitania po zawartości. Witaj `HAPROXY_0_VHOST` etykiety musi toobe zaktualizowane hello FQDN hello agentów DC/OS. 

```json
{
  "id": "web",
  "container": {
    "type": "DOCKER",
    "docker": {
      "image": "yeasy/simple-web",
      "network": "BRIDGE",
      "portMappings": [
        { "hostPort": 0, "containerPort": 80, "servicePort": 10000 }
      ],
      "forcePullImage":true
    }
  },
  "instances": 3,
  "cpus": 0.1,
  "mem": 65,
  "healthChecks": [{
      "protocol": "HTTP",
      "path": "/",
      "portIndex": 0,
      "timeoutSeconds": 10,
      "gracePeriodSeconds": 10,
      "intervalSeconds": 2,
      "maxConsecutiveFailures": 10
  }],
  "labels":{
    "HAPROXY_GROUP":"external",
    "HAPROXY_0_VHOST":"YOUR FQDN",
    "HAPROXY_0_MODE":"http"
  }
}
```

Za pomocą aplikacji hello toorun interfejsu wiersza polecenia DC/OS hello. Domyślnie Marathon wdraża hello hello awaryjności toohello prywatnej klastra. Oznacza to, że hello powyżej wdrożenia jest dostępny tylko przez moduł równoważenia obciążenia, który jest zwykle hello żądanego zachowania.

```azurecli-interactive
dcos marathon app add hello-web.json
```

Po wdrożeniu aplikacji hello Przeglądaj toohello FQDN hello agenta klastra tooview ze zrównoważonym obciążeniem aplikacji.

![Obraz aplikacji ze zrównoważonym obciążeniem](./media/container-service-load-balancing/lb-app.png)

## <a name="configure-azure-load-balancer"></a>Konfigurowanie usługi równoważenia obciążenia Azure

Domyślnie moduł Azure Load Balancer udostępnia porty 80, 8080 i 443. Jeśli używasz jednego z tych trzech portów (tak jak w hello powyżej przykładzie), a następnie nic nie należy toodo. Powinno być możliwe toohit FQDN modułu równoważenia obciążenia agenta i każdym odświeżeniu, będzie naciśniesz jeden z trzech serwerów sieci web w działaniu okrężnym. 

Jeśli używasz innego portu, należy reguła tooadd okrężnego oraz sondę modułu równoważenia obciążenia hello hello portu, który został użyty. Można to zrobić z hello [interfejsu wiersza polecenia Azure](../../azure-resource-manager/xplat-cli-azure-resource-manager.md), za pomocą polecenia hello `azure network lb rule create` i `azure network lb probe create`.

## <a name="next-steps"></a>Następne kroki

W tym samouczku poznanie równoważenia obciążenia w ACS z parametry hello Marathon i obciążenia Azure równoważenia tym hello następujące akcje:

> [!div class="checklist"]
> * Konfigurowanie równoważenia obciążenia platformy Marathon
> * Wdrażanie aplikacji przy użyciu usługi równoważenia obciążenia hello
> * Konfigurowanie i modułu równoważenia obciążenia Azure

Przejdź dalej toolearn samouczka toohello Integrowanie usługi Azure storage z DC/OS na platformie Azure.

> [!div class="nextstepaction"]
> [Azure instalacji udziału plików w klastrze DC/OS](container-service-dcos-fileshare.md)