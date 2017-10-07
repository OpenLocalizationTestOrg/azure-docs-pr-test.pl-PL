---
title: aaaQuickstart - klastra Azure Kubernetes dla systemu Linux | Dokumentacja firmy Microsoft
description: "Dowiesz toocreate klastra Kubernetes dla systemu Linux kontenerów w usłudze kontenera platformy Azure z hello wiersza polecenia platformy Azure."
services: container-service
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: acs, azure-container-service, kubernetes
keywords: 
ms.assetid: 8da267e8-2aeb-4c24-9a7a-65bdca3a82d6
ms.service: container-service
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/21/2017
ms.author: nepeters
ms.custom: H1Hack27Feb2017, mvc
ms.openlocfilehash: 8b0d7a803148c1cbf329f4b76f2e99b4b7e14983
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-kubernetes-cluster-for-linux-containers"></a>Wdrażanie klastra Kubernetes dla kontenerów systemu Linux

W tym szybki start klastra Kubernetes jest wdrażane za pomocą hello wiersza polecenia platformy Azure. Następnie wdrożone i uruchomić w klastrze hello aplikacji kontenera wielu składające się z frontonu sieci web oraz wystąpienia pamięci podręcznej Redis. Po ukończeniu aplikacji hello jest dostępny za pośrednictwem hello internet. 

Witaj przykładowej aplikacji używane w tym dokumencie są zapisywane w języku Python. Hello pojęcia i szczegółowe tutaj kroki mogą być używane toodeploy każdy kontener obrazu w klastrze Kubernetes. Witaj kodu, plik Dockerfile i wstępnie utworzony projekt toothis powiązane pliki manifestu Kubernetes są dostępne na [GitHub](https://github.com/Azure-Samples/azure-voting-app-redis.git).

![Obraz przeglądania tooAzure głosu](media/container-service-kubernetes-walkthrough/azure-vote.png)

To szybki start założono podstawową wiedzę na temat pojęć Kubernetes, aby uzyskać szczegółowe informacje na temat Kubernetes Zobacz hello [dokumentacji Kubernetes]( https://kubernetes.io/docs/home/).

Jeśli nie masz subskrypcji platformy Azure, przed rozpoczęciem utwórz [bezpłatne konto](https://azure.microsoft.com/free/?WT.mc_id=A261C142F).

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Wybierz tooinstall, użyj interfejsu wiersza polecenia hello lokalnie tego przewodnika Szybki Start wymaga działają hello Azure CLI w wersji 2.0.4 lub nowszej. Uruchom `az --version` toofind hello wersji. Jeśli potrzebujesz tooinstall lub uaktualniania, zobacz [zainstalować Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="create-a-resource-group"></a>Tworzenie grupy zasobów

Utwórz grupę zasobów o hello [Tworzenie grupy az](/cli/azure/group#create) polecenia. Grupa zasobów platformy Azure to logiczna grupa przeznaczona do wdrażania zasobów platformy Azure i zarządzania nimi. 

Witaj poniższy przykład tworzy grupę zasobów o nazwie *myResourceGroup* w hello *westeurope* lokalizacji.

```azurecli-interactive 
az group create --name myResourceGroup --location westeurope
```

Dane wyjściowe:

```json
{
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup",
  "location": "westeurope",
  "managedBy": null,
  "name": "myResourceGroup",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "tags": null
}
```

## <a name="create-kubernetes-cluster"></a>Tworzenie klastra Kubernetes

Tworzenie klastra Kubernetes usługi kontenera platformy Azure z hello [az acs utworzyć](/cli/azure/acs#create) polecenia. Witaj poniższym przykładzie jest tworzony klaster o nazwie *myK8sCluster* z systemem Linux jednego głównego węzła i trzech węzłów agenta systemu Linux.

```azurecli-interactive 
az acs create --orchestrator-type kubernetes --resource-group myResourceGroup --name myK8sCluster --generate-ssh-keys 
```

Po kilku minutach polecenia hello kończy i zwraca informacje o formacie json o hello klastra. 

## <a name="connect-toohello-cluster"></a>Połącz toohello klastra

Użyj toomanage klastrze Kubernetes [kubectl](https://kubernetes.io/docs/user-guide/kubectl/), klient wiersza polecenia Kubernetes hello. 

Jeśli korzystasz z usługi Azure CloudShell, narzędzie kubectl jest już zainstalowane. Jeśli chcesz, aby tooinstall lokalnie, użytkownik może użyć hello [az kubernetes acs install-cli](/cli/azure/acs/kubernetes#install-cli) polecenia.

tooconfigure kubectl tooconnect tooyour Kubernetes klastra, uruchom hello [az kubernetes acs get poświadczenia](/cli/azure/acs/kubernetes#get-credentials) polecenia. Ten krok pobiera poświadczenia i konfiguruje hello toouse Kubernetes CLI je.

```azurecli-interactive 
az acs kubernetes get-credentials --resource-group=myResourceGroup --name=myK8sCluster
```

tooverify hello połączenia tooyour klastra, użyj hello [kubectl uzyskać](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) tooreturn polecenia listy hello węzłów klastra.

```azurecli-interactive
kubectl get nodes
```

Dane wyjściowe:

```bash
NAME                    STATUS                     AGE       VERSION
k8s-agent-14ad53a1-0    Ready                      10m       v1.6.6
k8s-agent-14ad53a1-1    Ready                      10m       v1.6.6
k8s-agent-14ad53a1-2    Ready                      10m       v1.6.6
k8s-master-14ad53a1-0   Ready,SchedulingDisabled   10m       v1.6.6
```

## <a name="run-hello-application"></a>Uruchamianie aplikacji hello

Plik manifestu Kubernetes definiuje żądanego stanu dla klastra hello, w tym, co powinna być uruchomiona kontener obrazów. Na przykład manifestu jest toocreate używane wszystkie obiekty, potrzebne toorun hello Azure głos aplikacji. 

Utwórz plik o nazwie `azure-vote.yml` i skopiuj do niego hello następujących yaml programu. Jeśli pracujesz w usłudze Azure Cloud Shell, ten plik można utworzyć przy użyciu serwera vi lub Nano tak jak podczas pracy w systemie wirtualnym lub fizycznym.

```yaml
apiVersion: apps/v1beta1
kind: Deployment
metadata:
  name: azure-vote-back
spec:
  replicas: 1
  template:
    metadata:
      labels:
        app: azure-vote-back
    spec:
      containers:
      - name: azure-vote-back
        image: redis
        ports:
        - containerPort: 6379
          name: redis
---
apiVersion: v1
kind: Service
metadata:
  name: azure-vote-back
spec:
  ports:
  - port: 6379
  selector:
    app: azure-vote-back
---
apiVersion: apps/v1beta1
kind: Deployment
metadata:
  name: azure-vote-front
spec:
  replicas: 1
  template:
    metadata:
      labels:
        app: azure-vote-front
    spec:
      containers:
      - name: azure-vote-front
        image: microsoft/azure-vote-front:redis-v1
        ports:
        - containerPort: 80
        env:
        - name: REDIS
          value: "azure-vote-back"
---
apiVersion: v1
kind: Service
metadata:
  name: azure-vote-front
spec:
  type: LoadBalancer
  ports:
  - port: 80
  selector:
    app: azure-vote-front
```

Użyj hello [kubectl utworzyć](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#create) polecenia aplikacji hello toorun.

```azurecli-interactive
kubectl create -f azure-vote.yml
```

Dane wyjściowe:

```bash
deployment "azure-vote-back" created
service "azure-vote-back" created
deployment "azure-vote-front" created
service "azure-vote-front" created
```

## <a name="test-hello-application"></a>Testowanie aplikacji hello

Jak aplikacja hello jest uruchamiana, [usługi Kubernetes](https://kubernetes.io/docs/concepts/services-networking/service/) jest tworzony, że ujawnia hello toohello fronton aplikacji internetowych. Ten proces może potrwać kilka minut toocomplete. 

postęp toomonitor, użyj hello [kubectl pobrać usługi](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) z hello `--watch` argumentu.

```azurecli-interactive
kubectl get service azure-vote-front --watch
```

Początkowo hello **IP zewnętrznego** dla hello *azure głos początku* usługi pojawia się jako *oczekujące*. Gdy adres IP zewnętrznego hello zmienił się z *oczekujące* tooan *adres IP*, użyj `CTRL-C` toostop hello kubectl czujki procesu. 
  
```bash
azure-vote-front   10.0.34.242   <pending>     80:30676/TCP   7s
azure-vote-front   10.0.34.242   52.179.23.131   80:30676/TCP   2m
```

Użytkownik może przeglądać toohello zewnętrznego adresu IP adres toosee hello Azure głos aplikacji.

![Obraz przeglądania tooAzure głosu](media/container-service-kubernetes-walkthrough/azure-vote.png)  

## <a name="delete-cluster"></a>Usuwanie klastra
Gdy hello klastra nie jest już potrzebne, można użyć hello [az grupę Usuń](/cli/azure/group#delete) polecenia grupy zasobów hello tooremove, usługi kontenera i wszystkich powiązanych zasobów.

```azurecli-interactive 
az group delete --name myResourceGroup --yes --no-wait
```

## <a name="get-hello-code"></a>Pobierz kod hello

W tym szybki start kontenera wstępnie utworzony obrazy zostały toocreate używane wdrożenia Kubernetes. Witaj związane z kodu aplikacji, plik Dockerfile, i plik manifestu Kubernetes są dostępne w serwisie GitHub.

[https://github.com/Azure-Samples/azure-voting-app-redis](https://github.com/Azure-Samples/azure-voting-app-redis.git)

## <a name="next-steps"></a>Następne kroki

W tym szybki start wdrożeniu klastra Kubernetes i wdrożone tooit wielu kontenera aplikacji. 

toolearn więcej informacji na temat usługi kontenera platformy Azure i krokach związanych z pełny toodeployment przykład kodu, nadal toohello Kubernetes klastra samouczka.

> [!div class="nextstepaction"]
> [Zarządzanie klastrem Kubernetes usługi ASC](./container-service-tutorial-kubernetes-prepare-app.md)
