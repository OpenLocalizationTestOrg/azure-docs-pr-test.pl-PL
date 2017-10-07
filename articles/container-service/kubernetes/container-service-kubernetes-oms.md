---
title: "klaster Azure Kubernetes aaaMonitor - operacje zarządzania | Dokumentacja firmy Microsoft"
description: "Monitorowanie Kubernetes klastra usługi kontenera platformy Azure przy użyciu programu Microsoft Operations Management Suite"
services: container-service
documentationcenter: 
author: bburns
manager: timlt
editor: 
tags: acs, azure-container-service, kubernetes
keywords: 
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/09/2016
ms.author: bburns
ms.custom: mvc
ms.openlocfilehash: 7474ee1571134ffe43ff8e4041cf5a64f5635bb7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-cluster-with-microsoft-operations-management-suite-oms"></a>Monitor klastra usługi kontenera platformy Azure z Microsoft Operations Management Suite (OMS)

## <a name="prerequisites"></a>Wymagania wstępne
W tym przewodniku założono, że [utworzony klaster Kubernetes za pomocą usługi kontenera platformy Azure](container-service-kubernetes-walkthrough.md).

Założono również, że masz hello `az` interfejsu wiersza polecenia platformy Azure i `kubectl` narzędzia są zainstalowane.

Możesz przetestować, jeśli masz hello `az` zainstalowany, uruchamiając narzędzie:

```console
$ az --version
```

Jeśli nie masz hello `az` narzędzie zainstalowane, nie ma instrukcji [tutaj](https://github.com/azure/azure-cli#installation).  
Alternatywnie można użyć [powłoki chmury Azure](https://docs.microsoft.com/en-us/azure/cloud-shell/overview), mającego hello `az` interfejsu wiersza polecenia platformy Azure i `kubectl` narzędzia już zainstalowane automatycznie.  

Możesz przetestować, jeśli masz hello `kubectl` zainstalowany, uruchamiając narzędzie:

```console
$ kubectl version
```

Jeśli nie masz `kubectl` zainstalowany, możesz uruchomić:
```console
$ az acs kubernetes install-cli
```

tootest, jeśli masz zainstalowany w narzędziu do kubectl klucze kubernetes można uruchomić:
```console
$ kubectl get nodes
```

Jeśli hello powyżej polecenie błędy wychodzących, należy do własnych narzędzi kubectl tooinstall kubernetes klastra kluczy. Możesz to zrobić z hello następujące polecenie:
```console
RESOURCE_GROUP=my-resource-group
CLUSTER_NAME=my-acs-name
az acs kubernetes get-credentials --resource-group=$RESOURCE_GROUP --name=$CLUSTER_NAME
```

## <a name="monitoring-containers-with-operations-management-suite-oms"></a>Monitorowanie kontenerów w usłudze Operations Management Suite (OMS)

Microsoft Operations Management (OMS) jest firmy Microsoft w chmurze IT rozwiązania do zarządzania ułatwiające zarządzanie i ochrona lokalnej infrastruktury w chmurze. Kontener rozwiązanie to rozwiązanie w OMS Log Analytics, który pomaga w widoku hello kontenera magazynu, wydajności i dzienniki w jednej lokalizacji. Można inspekcji, rozwiązywanie problemów z kontenerów, wyświetlając hello dzienniki w centralnej lokalizacji oraz znaleźć zakłócenia, wykorzystywanie nadmiarowe kontenera na hoście.

![](media/container-service-monitoring-oms/image1.png)

Aby uzyskać więcej informacji o rozwiązaniu kontenera, zobacz toothe [analizy dzienników rozwiązania kontenera](../../log-analytics/log-analytics-containers.md).

## <a name="installing-oms-on-kubernetes"></a>Instalowanie pakietu OMS na Kubernetes

### <a name="obtain-your-workspace-id-and-key"></a>Uzyskaj identyfikator i klucz
Hello usługi toohello tootalk agent pakietu OMS musi on toobe skonfigurowany identyfikator obszaru roboczego i klucz obszaru roboczego. Klucz należy toocreate OMS i identyfikator obszaru roboczego hello tooget konta w <https://mms.microsoft.com>. Wykonaj hello kroki toocreate konta. Po zakończeniu tworzenia konta hello należy tooobtain Twój identyfikator i klucz, klikając **ustawienia**, następnie **połączonych źródeł**, a następnie **serwerów z systemem Linux**, jak pokazano poniżej.

 ![](media/container-service-monitoring-oms/image5.png)

### <a name="install-hello-oms-agent-using-a-daemonset"></a>Instalowanie agenta pakietu OMS hello za pomocą DaemonSet
DaemonSets są używane przez Kubernetes toorun pojedynczego wystąpienia na każdym hoście w klastrze hello kontenera.
Są one idealne w przypadku uruchamiania agenci monitorowania.

Oto hello [pliku yaml programu DaemonSet](https://github.com/Microsoft/OMS-docker/tree/master/Kubernetes). Zapisz plik o nazwie pliku tooa `oms-daemonset.yaml` i Zastąp symbol zastępczy wartości hello `WSID` i `KEY` z identyfikator i klucz w pliku hello.

Po dodaniu klucza toohello DaemonSet konfiguracji i identyfikator obszaru roboczego, na których można zainstalować agenta pakietu OMS hello w klastrze z hello `kubectl` narzędzia wiersza polecenia:

```console
$ kubectl create -f oms-daemonset.yaml
```

### <a name="installing-hello-oms-agent-using-a-kubernetes-secret"></a>Instalowanie agenta pakietu OMS hello przy użyciu klucza tajnego Kubernetes
tooprotect OMS identyfikator i klucz tajny Kubernetes można użyć jako część pliku DaemonSet yaml programu.

 - Skopiuj skrypt hello, pliku szablonu tajne i hello pliku DaemonSet yaml programu (z [repozytorium](https://github.com/Microsoft/OMS-docker/tree/master/Kubernetes)) i upewnij się, że są one na powitania tego samego katalogu. 
      - Generowanie skryptu - gen.sh klucz tajny klucz tajny
      - Szablon tajne — template.yaml klucz tajny
   - Plik yaml programu DaemonSet — omsagent — ds-secrets.yaml
 - Uruchom skrypt hello. skrypt Hello poprosi o hello OMS identyfikator i klucz podstawowy. Włóż który i hello skryptu zostanie utworzony plik tajny yaml programu, dlatego może być uruchomiony.   
   ```
   #> sudo bash ./secret-gen.sh 
   ```

   - Utwórz pod kluczy tajnych hello, uruchamiając następujące hello:``` kubectl create -f omsagentsecret.yaml ```
 
   - toocheck, uruchom następujące hello: 

   ``` 
   root@ubuntu16-13db:~# kubectl get secrets
   NAME                  TYPE                                  DATA      AGE
   default-token-gvl91   kubernetes.io/service-account-token   3         50d
   omsagent-secret       Opaque                                2         1d
   root@ubuntu16-13db:~# kubectl describe secrets omsagent-secret
   Name:           omsagent-secret
   Namespace:      default
   Labels:         <none>
   Annotations:    <none>

   Type:   Opaque

   Data
   ====
   WSID:   36 bytes
   KEY:    88 bytes 
   ```
 
  - Tworzenie sieci omsagent demon set, uruchamiając``` kubectl create -f omsagent-ds-secrets.yaml ```

### <a name="conclusion"></a>Podsumowanie
Gotowe. Po kilku minutach powinno być możliwe toosee dane przepływające tooyour OMS z pulpitu nawigacyjnego.
