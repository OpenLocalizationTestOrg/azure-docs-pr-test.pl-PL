---
title: "aaaManage Azure Kubernetes klaster z interfejsu użytkownika sieci web | Dokumentacja firmy Microsoft"
description: "Przy użyciu hello Kubernetes interfejs użytkownika sieci web w usłudze kontenera platformy Azure"
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
ms.date: 02/21/2017
ms.author: bburns
ms.custom: mvc
ms.openlocfilehash: e24ea0b82c94d2fd4610e4442699ef756590e6bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-kubernetes-web-ui-with-azure-container-service"></a>Przy użyciu hello Kubernetes interfejs użytkownika sieci web z usługi kontenera platformy Azure

## <a name="prerequisites"></a>Wymagania wstępne
W tym przewodniku założono, że [utworzony klaster Kubernetes za pomocą usługi kontenera platformy Azure](container-service-kubernetes-walkthrough.md).


Założono również, że masz hello Azure CLI 2.0 i `kubectl` narzędzia są zainstalowane.

Możesz przetestować, jeśli masz hello `az` zainstalowany, uruchamiając narzędzie:

```console
$ az --version
```

Jeśli nie masz hello `az` narzędzie zainstalowane, nie ma instrukcji [tutaj](https://github.com/azure/azure-cli#installation).

Możesz przetestować, jeśli masz hello `kubectl` zainstalowany, uruchamiając narzędzie:

```console
$ kubectl version
```

Jeśli nie masz `kubectl` zainstalowany, możesz uruchomić:

```console
$ az acs kubernetes install-cli
```

## <a name="overview"></a>Omówienie

### <a name="connect-toohello-web-ui"></a>Połącz toohello interfejsu użytkownika sieci web
Hello interfejsu użytkownika sieci web Kubernetes można uruchomić, uruchamiając:

```console
$ az acs kubernetes browse -g [Resource Group] -n [Container service instance name]
```

To powinno spowodować otwarcie serwer proxy sieci web przeglądarce skonfigurowane tootalk tooa bezpieczne połączenie z komputera lokalnego toohello Kubernetes interfejsu użytkownika sieci web.

### <a name="create-and-expose-a-service"></a>Utworzyć i uwidocznić usługę
1. W hello Kubernetes interfejsu użytkownika sieci web, kliknij przycisk **Utwórz** przycisk w oknie prawym górnym hello.

    ![Kubernetes Tworzenie interfejsu użytkownika](./media/container-service-kubernetes-ui/create.png)

    Zostanie otwarte okno dialogowe której będzie można rozpocząć tworzenie aplikacji.

2. Nadaj nazwę hello `hello-nginx`. Użyj hello [ `nginx` kontenera z Docker](https://hub.docker.com/_/nginx/) i wdrażanie trzech replik tej usługi sieci web.

    ![Okno dialogowe Tworzenie Kubernetes Pod](./media/container-service-kubernetes-ui/nginx.png)

3. W obszarze **usługi**, wybierz pozycję **zewnętrznych** i wprowadź port 80.

    To ustawienie zrównoważenie obciążenia ruchu toohello trzy repliki.

    ![Okno dialogowe Tworzenie usługi Kubernetes](./media/container-service-kubernetes-ui/service.png)

4. Kliknij przycisk **Wdróż** toodeploy tych kontenerów i usług.

    ![Wdrażanie Kubernetes](./media/container-service-kubernetes-ui/deploy.png)

### <a name="view-your-containers"></a>Wyświetl kontenerów
Po kliknięciu **Wdróż**, hello interfejsu użytkownika przedstawiono usługi wdrażania:

![Stan Kubernetes](./media/container-service-kubernetes-ui/status.png)

Można wyświetlić hello stan każdego obiektu Kubernetes hello okrąg na powitania po lewej stronie interfejsu użytkownika, w obszarze **stanowiskami**. Jeśli jest częściowo koło obiektu hello nadal jest wdrażana. Gdy obiekt pełni zostanie wdrożona, Wyświetla zielony znacznik wyboru:

![Kubernetes wdrożony](./media/container-service-kubernetes-ui/deployed.png)

Gdy wszystko jest uruchomiona, kliknij jeden z szczegóły toosee stanowiskami o hello uruchomiona usługa sieci web.

![Stanowiskami Kubernetes](./media/container-service-kubernetes-ui/pods.png)

W hello **stanowiskami** widoku wyświetlane są informacje o kontenery hello hello pod, jak również zasoby Procesora i pamięci hello używane przez tych kontenerach:

![Kubernetes zasobów](./media/container-service-kubernetes-ui/resources.png)

Jeśli nie widzisz hello zasobów, może być konieczne toowait kilka minut dla hello toopropagate danych monitorowania.

Dzienniki hello toosee Twojego kontenera, kliknij przycisk **Sprawdź dzienniki**.

![Dzienniki Kubernetes](./media/container-service-kubernetes-ui/logs.png)

### <a name="viewing-your-service"></a>Wyświetlanie usługi
W dodatku toorunning kontenerów, hello Kubernetes interfejsu użytkownika została utworzona zewnętrzne `Service` który inicjuje opakowaniu toohello ruchu toobring usługi równoważenia obciążenia w klastrze.

W okienku nawigacji po lewej stronie powitania kliknij **usług** tooview wszystkie usługi (powinien istnieć tylko jeden).

![Kubernetes usług](./media/container-service-kubernetes-ui/service-deployed.png)

W tym widoku powinny pojawić się punkt końcowy zewnętrzne (adres IP), która została przydzielona tooyour usługi.
Kliknięcie tego adresu IP, powinna zostać wyświetlona z kontener Nginx uruchomiony za usługą równoważenia obciążenia.

![Widok nginx](./media/container-service-kubernetes-ui/nginx-page.png)

### <a name="resizing-your-service"></a>Zmiana rozmiaru usługi
W tooviewing Dodawanie obiektów w hello interfejsu użytkownika, możesz edytować i aktualizowanie obiektów interfejsu API Kubernetes hello.

Najpierw kliknij **wdrożeń** w hello pozostałych nawigacji w okienku toosee hello wdrożenia usługi.

Po przejściu do tego widoku, kliknij na powitania zestawu replik, a następnie kliknij **Edytuj** hello nawigacji w górnym pasku:

![Edytuj Kubernetes](./media/container-service-kubernetes-ui/edit.png)

Edytuj hello `spec.replicas` toobe pola `2`i kliknij przycisk **aktualizacji**.

Powoduje to hello liczby replikami toodrop tootwo usuwając jeden z stanowiskami.

 

