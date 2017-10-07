---
title: "Samouczek usługi kontenera aaaAzure — wdrażanie klastra | Dokumentacja firmy Microsoft"
description: "Samouczek usługi kontenera platformy Azure — wdrażanie klastra"
services: container-service
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Docker, kontenery, mikrousługi, Kubernetes, DC/OS, Azure"
ms.assetid: 
ms.service: container-service
ms.devlang: azurecli
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/21/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: c4c8cc95c88d9c2077d0322f57e5d3159e2dd0ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-kubernetes-cluster-in-azure-container-service"></a>Wdrażanie klastra Kubernetes usługi kontenera platformy Azure

Kubernetes zapewnia platformę rozproszonej konteneryzowanych aplikacji. Z usługi kontenera platformy Azure inicjowania obsługi klastra produkcyjnego gotowe Kubernetes jest proste i szybkie. W tym samouczku, część 3 7, wdrożono klaster Kubernetes usługi kontenera platformy Azure. Ukończono kroki obejmują:

> [!div class="checklist"]
> * Wdrażanie klastra usług ACS Kubernetes
> * Instalacja hello Kubernetes interfejsu wiersza polecenia (kubectl)
> * Konfiguracja kubectl

W kolejnych samouczkach hello Azure głos aplikacja jest wdrożona toohello klastra, skalowania, zaktualizować, a Operations Management Suite jest skonfigurowany toomonitor hello Kubernetes klastra.

## <a name="before-you-begin"></a>Przed rozpoczęciem

W poprzednich samouczki obrazu kontenera został utworzony i przekazać tooan rejestru kontenera Azure wystąpienia. Jeśli nie zostało wykonane następujące kroki, a chcesz toofollow wzdłuż, zwróć zbyt[samouczek 1 — Tworzenie kontenera obrazów](./container-service-tutorial-kubernetes-prepare-app.md).

## <a name="create-kubernetes-cluster"></a>Tworzenie klastra Kubernetes

W hello [poprzedniego samouczek](./container-service-tutorial-kubernetes-prepare-acr.md), grupy zasobów o nazwie *myResourceGroup* został utworzony. Jeśli użytkownik nie zostało zrobione, Utwórz teraz tej grupy zasobów.

```azurecli-interactive
az group create --name myResourceGroup --location westeurope
```

Tworzenie klastra Kubernetes usługi kontenera platformy Azure z hello [az acs utworzyć](/cli/azure/acs#create) polecenia. 

Witaj poniższym przykładzie jest tworzony klaster o nazwie *myK8sCluster* z systemem Linux jednego głównego węzła i trzech węzłów agenta systemu Linux.

```azurecli-interactive 
az acs create --orchestrator-type=kubernetes --resource-group myResourceGroup --name=myK8SCluster --generate-ssh-keys 
```

Po kilku minutach hello polecenie zostanie wykonane, a w formacie json zwraca informacji o wdrażaniu hello ACS.

## <a name="install-hello-kubectl-cli"></a>Zainstaluj kubectl hello interfejsu wiersza polecenia

tooconnect toohello Kubernetes klastra z komputera klienta, użyj [kubectl](https://kubernetes.io/docs/user-guide/kubectl/), klient wiersza polecenia Kubernetes hello. 

Jeśli korzystasz z usługi Azure CloudShell, narzędzie `kubectl` jest już zainstalowane. Jeśli chcesz, aby tooinstall lokalnie, użyj hello [az kubernetes acs install-cli](/cli/azure/acs/kubernetes#install-cli) polecenia.

Jeśli uruchomiona w systemie Linux lub macOS, może być konieczne toorun z sudo. W systemie Windows upewnij się, że powłoki zostało uruchomione jako administrator.

```azurecli-interactive 
az acs kubernetes install-cli 
```

W systemie Windows, instalacja domyślna hello jest *c:\program files (x86)\kubectl.exe*. Tooadd może być konieczne tej ścieżki pliku toohello systemu Windows. 

## <a name="connect-with-kubectl"></a>Nawiązywanie połączenia przy użyciu narzędzia kubectl

tooconfigure `kubectl` tooconnect tooyour Kubernetes klastra, uruchom hello [az kubernetes acs get poświadczenia](/cli/azure/acs/kubernetes#get-credentials) polecenia.

```azurecli-interactive 
az acs kubernetes get-credentials --resource-group=myResourceGroup --name=myK8SCluster
```

tooverify hello połączenia tooyour klastra, uruchom hello [kubectl uzyskać węzłów](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) polecenia.

```azurecli-interactive
kubectl get nodes
```

Dane wyjściowe:

```bash
NAME                    STATUS                     AGE       VERSION
k8s-agent-98dc3136-0    Ready                      5m        v1.6.2
k8s-agent-98dc3136-1    Ready                      5m        v1.6.2
k8s-agent-98dc3136-2    Ready                      5m        v1.6.2
k8s-master-98dc3136-0   Ready,SchedulingDisabled   5m        v1.6.2
```

Po ukończeniu samouczka masz klastry ACS Kubernetes dla obciążeń. W kolejnych samouczkach aplikacji kontenera wielu jest wdrożone toothis klaster, skalowana w poziomie, aktualizacji i monitorowane.

## <a name="next-steps"></a>Następne kroki

W tym samouczku klastra Kubernetes usługi kontenera platformy Azure została wdrożona. Zakończono Hello następujące kroki:

> [!div class="checklist"]
> * Wdrożone klastra Kubernetes ACS
> * Zainstalowane hello Kubernetes interfejsu wiersza polecenia (kubectl)
> * Skonfigurowany kubectl

Przejdź dalej toolearn toohello dotyczące uruchamiania aplikacji w klastrze hello samouczka.

> [!div class="nextstepaction"]
> [Wdrażanie aplikacji w Kubernetes](./container-service-tutorial-kubernetes-deploy-application.md)
