---
title: kontenery aaaDeploy z Helm w Azure Kubernetes | Dokumentacja firmy Microsoft
description: "Użyj hello Helm pakowania narzędzia toodeploy kontenery w klastrze Kubernetes usługi kontenera platformy Azure"
services: container-service
documentationcenter: 
author: sauryadas
manager: madhana
editor: 
tags: acs, azure-container-service
keywords: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/10/2017
ms.author: saudas
ms.custom: mvc
ms.openlocfilehash: c7bd780afe00084ebe4e3a14873e1e340a29d144
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-helm-toodeploy-containers-on-a-kubernetes-cluster"></a>Używanie kontenerów toodeploy Helm w klastrze Kubernetes 

[Helm](https://github.com/kubernetes/helm/) jest narzędziem open source tworzenia pakietów, które pomaga zainstalować i zarządzanie cyklem życia hello Kubernetes aplikacji. Podobne tooLinux pakietu menedżerów takich jak Apt get i Yum Helm jest używane toomanage Kubernetes wykresy, które są pakiety zasobów Kubernetes wstępnie skonfigurowane. W tym artykule opisano sposób toowork z Helm w klastrze Kubernetes wdrożenia usługi kontenera platformy Azure.

Helm ma dwa składniki: 
* Witaj **Helm CLI** uruchomioną na komputerze lokalnie lub w chmurze powitania klienta  

* **Sterownicy** jest serwer, który działa w klastrze Kubernetes hello i zarządza hello cyklem życia aplikacji Kubernetes 
 
## <a name="prerequisites"></a>Wymagania wstępne

* [Tworzenie klastra Kubernetes](container-service-kubernetes-walkthrough.md) usługi kontenera platformy Azure

* [Instalowanie i konfigurowanie `kubectl` ](../container-service-connect.md) na komputerze lokalnym

* [Zainstaluj Helm](https://github.com/kubernetes/helm/blob/master/docs/install.md) na komputerze lokalnym

## <a name="helm-basics"></a>Podstawy Helm 

tooview informacji na temat hello Kubernetes klastra są sterownicy Instalowanie i wdrażanie aplikacji, wpisz następujące polecenie hello:

```bash
kubectl cluster-info 
```
![kubectl klastra — informacje](./media/container-service-kubernetes-helm/clusterinfo.png)
 
Po zainstalowaniu Helm zainstalować sterownicy w klastrze Kubernetes, wpisując następujące polecenie hello:

```bash
helm init --upgrade
```
Po pomyślnym ukończeniu, pojawić się dane wyjściowe podobne do następujących hello:

![Sterownicy instalacji](./media/container-service-kubernetes-helm/tiller-install.png)
 
 
 
 
tooview wszystkich hello Helm wykresów dostępne w repozytorium hello hello wpisz następujące polecenie:

```bash 
helm search 
```

Zostaną wyświetlone dane wyjściowe podobne do następujących hello:

![Helm wyszukiwania](./media/container-service-kubernetes-helm/helm-search.png)
 
tooupdate hello wykresy tooget hello najnowsze wersje, wpisz:

```bash 
helm repo update 
```
## <a name="deploy-an-nginx-ingress-controller-chart"></a>Wdrażanie Nginx wejściowych kontrolera wykresu 
 
toodeploy Nginx wejściowych kontrolera wykresu wpisz jedno polecenie:

```bash
helm install stable/nginx-ingress 
```
![Wdrażanie kontrolera wejściowych](./media/container-service-kubernetes-helm/nginx-ingress.png)

W przypadku wpisania `kubectl get svc` tooview wszystkich usług, które są uruchomione w klastrze hello, zostanie wyświetlony adres IP jest przypisania toohello wejściowych kontrolera. (Podczas przypisywania hello jest w toku, zobacz `<pending>`. Może potrwać kilka minut toocomplete.) 

Po przypisaniu adres IP hello Przejdź wartość toohello hello zewnętrznego adresu IP adres toosee hello Nginx zaplecza uruchomiony. 
 
![Transfer danych przychodzących adresów IP](./media/container-service-kubernetes-helm/ingress-ip-address.png)


toosee listę wykresy zainstalowanych w klastrze, wpisz:

```bash
helm list 
```

Polecenie hello można skrócić zbyt`helm ls`.
 
 
 
 
## <a name="deploy-a-mariadb-chart-and-client"></a>Wdrażanie wykresu MariaDB i klienta

Teraz można wdrożyć wykresu MariaDB i bazy danych MariaDB klienta tooconnect toohello.

Wykres toodeploy hello MariaDB, hello wpisz następujące polecenie:

```bash
helm install --name v1 stable/mariadb
```

gdzie `--name` jest znacznika używany w wersjach.

> [!TIP]
> W przypadku niepowodzenia wdrożenia hello Uruchom `helm repo update` i spróbuj ponownie.
>
 
 
tooview wszystkich schematów hello wdrożone w klastrze, wpisz:

```bash 
helm list
```
 
tooview wszystkich wdrożeń uruchomiona w klastrze, wpisz:

```bash
kubectl get deployments 
``` 
 
 
Na koniec toorun pod tooaccess powitania klienta, wpisz:

```bash
kubectl run v1-mariadb-client --rm --tty -i --image bitnami/mariadb --command -- bash  
``` 
 
 
tooconnect toohello klienta, hello wpisz następujące polecenie, zastępując `v1-mariadb` o nazwie hello wdrożenia:

```bash
sudo mysql –h v1-mariadb
```
 
 
Można teraz używać standardowych poleceń toocreate baz danych, tabelach itp. Na przykład `Create DATABASE testdb1;` tworzy pustą bazę danych. 
 
 
 
## <a name="next-steps"></a>Następne kroki

* Aby uzyskać więcej informacji o zarządzaniu Kubernetes wykresy, zobacz hello [Helm dokumentacji](https://github.com/kubernetes/helm/blob/master/docs/index.md). 

