---
title: aaaQuickstart - klastra Azure Kubernetes dla systemu Windows | Dokumentacja firmy Microsoft
description: "Dowiesz toocreate klastra Kubernetes kontenerów systemu Windows w usłudze kontenera platformy Azure z hello wiersza polecenia platformy Azure."
documentationcenter: 
author: dlepow
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
ms.date: 07/18/2017
ms.author: danlep
ms.custom: H1Hack27Feb2017, mvc
ms.openlocfilehash: 85fe65a46ae8c78797e8a8a097c2a37f06329335
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-kubernetes-cluster-for-windows-containers"></a>Wdrażanie klastra Kubernetes dla kontenerów systemu Windows

Hello wiersza polecenia platformy Azure jest używana toocreate i zarządzania zasobami Azure z wiersza polecenia hello lub w skryptach. Ta szczegółów przewodnik przy użyciu hello Azure CLI toodeploy [Kubernetes](https://kubernetes.io/docs/home/) klastra w [usługi kontenera platformy Azure](../container-service-intro.md). Po wdrożeniu klastra hello tooit należy połączyć z hello Kubernetes `kubectl` narzędzia wiersza polecenia, a wdrażanie Twojego pierwszego kontenera systemu Windows.

Jeśli nie masz subskrypcji platformy Azure, przed rozpoczęciem utwórz [bezpłatne konto](https://azure.microsoft.com/free/?WT.mc_id=A261C142F).

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Wybierz tooinstall, użyj interfejsu wiersza polecenia hello lokalnie tego przewodnika Szybki Start wymaga działają hello Azure CLI w wersji 2.0.4 lub nowszej. Uruchom `az --version` toofind hello wersji. Jeśli potrzebujesz tooinstall lub uaktualniania, zobacz [zainstalować Azure CLI 2.0]( /cli/azure/install-azure-cli). 

> [!NOTE]
> Obsługa kontenerów systemu Windows w rozwiązaniu Kubernetes w usłudze Azure Container Service jest dostępna w wersji zapoznawczej. 
>

## <a name="create-a-resource-group"></a>Tworzenie grupy zasobów

Utwórz grupę zasobów o hello [Tworzenie grupy az](/cli/azure/group#create) polecenia. Grupa zasobów platformy Azure to logiczna grupa przeznaczona do wdrażania zasobów platformy Azure i zarządzania nimi. 

Witaj poniższy przykład tworzy grupę zasobów o nazwie *myResourceGroup* w hello *eastus* lokalizacji.

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```

## <a name="create-kubernetes-cluster"></a>Tworzenie klastra Kubernetes
Tworzenie klastra Kubernetes usługi kontenera platformy Azure z hello [az acs utworzyć](/cli/azure/acs#create) polecenia. 

Witaj poniższym przykładzie jest tworzony klaster o nazwie *myK8sCluster* z systemem Linux jednego głównego węzła i dwa węzły agenta systemu Windows. W tym przykładzie tworzy SSH klucze wymagane tooconnect toohello Linux wzorca. W tym przykładzie użyto *azureuser* dla nazwy użytkownika administracyjnego i *myPassword12* jako hasło hello na węzłach Windows hello. Zaktualizować te wartości toosomething tooyour odpowiednie środowisko. 



```azurecli-interactive 
az acs create --orchestrator-type=kubernetes \
    --resource-group myResourceGroup \
    --name=myK8sCluster \
    --agent-count=2 \
    --generate-ssh-keys \
    --windows --admin-username azureuser \
    --admin-password myPassword12
```

Po kilku minutach polecenia hello kończy i pokazuje informacje dotyczące wdrożenia.

## <a name="install-kubectl"></a>Instalowanie narzędzia kubectl

tooconnect toohello Kubernetes klastra z komputera klienta, użyj [ `kubectl` ](https://kubernetes.io/docs/user-guide/kubectl/), klient wiersza polecenia Kubernetes hello. 

Jeśli korzystasz z usługi Azure CloudShell, narzędzie `kubectl` jest już zainstalowane. Jeśli chcesz, aby tooinstall lokalnie, użytkownik może użyć hello [az kubernetes acs install-cli](/cli/azure/acs/kubernetes#install-cli) polecenia.

Witaj następującego wiersza polecenia platformy Azure przykład instaluje `kubectl` tooyour systemu. W systemie Windows należy uruchomić to polecenie jako administrator.

```azurecli-interactive 
az acs kubernetes install-cli
```


## <a name="connect-with-kubectl"></a>Nawiązywanie połączenia przy użyciu narzędzia kubectl

tooconfigure `kubectl` tooconnect tooyour Kubernetes klastra, uruchom hello [az kubernetes acs get poświadczenia](/cli/azure/acs/kubernetes#get-credentials) polecenia. Witaj poniższy przykład pobiera hello konfigurację klastra dla klastra Kubernetes.

```azurecli-interactive 
az acs kubernetes get-credentials --resource-group=myResourceGroup --name=myK8sCluster
```

tooverify hello połączenia tooyour klaster z komputera, spróbuj uruchomić:

```azurecli-interactive
kubectl get nodes
```

`kubectl`Wyświetla listę węzłów hello wzorca i agenta.

```azurecli-interactive
NAME                    STATUS                     AGE       VERSION
k8s-agent-98dc3136-0    Ready                      5m        v1.5.3
k8s-agent-98dc3136-1    Ready                      5m        v1.5.3
k8s-master-98dc3136-0   Ready,SchedulingDisabled   5m        v1.5.3

```

## <a name="deploy-a-windows-iis-container"></a>Wdrażanie kontenera usług IIS systemu Windows

Kontener platformy Docker można uruchomić wewnątrz *zasobnika* rozwiązania Kubernetes zawierającego co najmniej jeden kontener. 

Ten prosty przykład używa toospecify pliku JSON kontenera usług Microsoft Internet Information Server (IIS), a następnie tworzy pod hello przy użyciu hello `kubctl apply` polecenia. 

Tworzenie pliku lokalnego o nazwie `iis.json` i hello kopiowania tekstu. Ten plik zawiera informacje toorun Kubernetes usług IIS w systemie Windows Server 2016 Nano Server przy użyciu obrazu publicznego kontenera z [Centrum Docker](https://hub.docker.com/r/nanoserver/iis/). kontener Hello korzysta z portu 80, ale początkowo jest dostępny tylko w ramach hello sieci klastra.

 ```JSON
 {
  "apiVersion": "v1",
  "kind": "Pod",
  "metadata": {
    "name": "iis",
    "labels": {
      "name": "iis"
    }
  },
  "spec": {
    "containers": [
      {
        "name": "iis",
        "image": "nanoserver/iis",
        "ports": [
          {
          "containerPort": 80
          }
        ]
      }
    ],
    "nodeSelector": {
     "beta.kubernetes.io/os": "windows"
     }
   }
 }
 ```

toostart hello pod, wpisz:
  
```azurecli-interactive
kubectl apply -f iis.json
```  

wdrożenie hello tootrack, wpisz:
  
```azurecli-interactive
kubectl get pods
```

Podczas wdrożenia hello pod jest stan hello `ContainerCreating`. Może upłynąć kilka minut, aż hello kontenera tooenter hello `Running` stanu.

```azurecli-interactive
NAME     READY        STATUS        RESTARTS    AGE
iis      1/1          Running       0           32s
```

## <a name="view-hello-iis-welcome-page"></a>Widok hello strona powitalna usług IIS

tooexpose hello pod toohello world z publicznym adresem IP hello wpisz następujące polecenie:

```azurecli-interactive
kubectl expose pods iis --port=80 --type=LoadBalancer
```

To polecenie Kubernetes tworzy usługę i [reguły modułu równoważenia obciążenia Azure](container-service-kubernetes-load-balancing.md) z publicznym adresem IP hello usługi. 

Uruchom następujące polecenie toosee hello stanu usługi hello hello.

```azurecli-interactive
kubectl get svc
```

Początkowo hello adres IP jest wyświetlany jako `pending`. Po kilku minutach hello zewnętrzny adres IP hello `iis` ustawiono pod:
  
```azurecli-interactive
NAME         CLUSTER-IP     EXTERNAL-IP     PORT(S)        AGE       
kubernetes   10.0.0.1       <none>          443/TCP        21h       
iis          10.0.111.25    13.64.158.233   80/TCP         22m
```

Można użyć przeglądarki sieci web na wybór toosee hello domyślne IIS strony powitalnej na powitania zewnętrzny adres IP:

![Obraz przeglądania tooIIS](./media/container-service-kubernetes-windows-walkthrough/kubernetes-iis.png)  


## <a name="delete-cluster"></a>Usuwanie klastra
Gdy hello klastra nie jest już potrzebne, można użyć hello [az grupę Usuń](/cli/azure/group#delete) polecenia grupy zasobów hello tooremove, usługi kontenera i wszystkich powiązanych zasobów.

```azurecli-interactive 
az group delete --name myResourceGroup
```


## <a name="next-steps"></a>Następne kroki

W tym przewodniku Szybki start wdrożono klaster Kubernetes, nawiązano połączenie z narzędziem `kubectl` i wdrożono zasobnik za pomocą kontenera usług IIS. toolearn więcej informacji na temat usługi kontenera platformy Azure, nadal toohello Kubernetes samouczka.

> [!div class="nextstepaction"]
> [Zarządzanie klastrem Kubernetes usługi ASC](container-service-tutorial-kubernetes-prepare-app.md)
