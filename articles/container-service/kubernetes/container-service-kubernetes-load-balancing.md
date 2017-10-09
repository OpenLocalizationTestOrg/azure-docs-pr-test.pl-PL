---
title: aaaLoad saldo kontenery Kubernetes na platformie Azure | Dokumentacja firmy Microsoft
description: "Połącz zewnętrznie i zrównoważenia obciążenia w wielu kontenerów Kubernetes klastra usługi kontenera platformy Azure."
services: container-service
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Kubernetes kontenerów, Micro-services, Azure"
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/17/2017
ms.author: danlep
ms.custom: mvc
ms.openlocfilehash: 8073c8d3a015a53a532c326749571cb2582e1bac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="load-balance-containers-in-a-kubernetes-cluster-in-azure-container-service"></a>Kontenery równoważenia obciążenia w klastrze Kubernetes usługi kontenera platformy Azure 
W tym artykule przedstawiono równoważenia obciążenia w klastrze Kubernetes usługi kontenera platformy Azure. Równoważenie obciążenia sieciowego zapewnia zewnętrznie dostępny adres IP dla usługi hello i dystrybuuje ruch sieciowy między stanowiskami hello uruchomionych w maszynach wirtualnych agenta.

Możesz skonfigurować toouse usługi Kubernetes [modułu równoważenia obciążenia Azure](../../load-balancer/load-balancer-overview.md) toomanage zewnętrznego ruchu sieciowego (TCP). Dodatkowa konfiguracja obciążenia routing ruchu HTTP lub HTTPS lub bardziej zaawansowanych scenariuszy i równoważenie są możliwe.

## <a name="prerequisites"></a>Wymagania wstępne
* [Wdrażanie klastra Kubernetes](container-service-kubernetes-walkthrough.md) usługi kontenera platformy Azure
* [Połączenia klienckie](../container-service-connect.md) tooyour klastra

## <a name="azure-load-balancer"></a>Moduł równoważenia obciążenia Azure

Domyślnie klaster Kubernetes wdrożony w usłudze kontenera platformy Azure obejmuje usługę równoważenia obciążenia Azure internetowy agenta hello maszyn wirtualnych. (Zasób równoważenia obciążenia oddzielne jest skonfigurowany do wzorca hello maszyn wirtualnych). Moduł równoważenia obciążenia Azure jest usługą równoważenia obciążenia warstwy 4. Obecnie hello modułu równoważenia obciążenia obsługuje tylko ruch TCP w Kubernetes.

Podczas tworzenia usługi Kubernetes, można automatycznie skonfigurować hello Azure usługi równoważenia obciążenia używanej tooallow dostępu toohello. tooconfigure hello moduł równoważenia obciążenia usługi hello zestaw `type` zbyt`LoadBalancer`. Moduł równoważenia obciążenia Hello tworzy toomap reguły publiczny adres IP i numer portu przychodzącego usługi ruchu toohello prywatnych adresów IP i numerów portów stanowiskami hello w agencie maszyny wirtualne (i odwrotnie dla ruchu odpowiedzi). 

 Poniżej przedstawiono dwa przykłady przedstawiający sposób tooset hello usługi Kubernetes `type` zbyt`LoadBalancer`. (Po próbie przykłady hello, usunięcie wdrożeń hello nie jest już potrzebne.)

### <a name="example-use-hello-kubectl-expose-command"></a>Przykład: Użyj hello `kubectl expose` polecenia 
Witaj [wskazówki Kubernetes](container-service-kubernetes-walkthrough.md) zawiera przykładowy sposób tooexpose usługi za pomocą hello `kubectl expose` polecenia i jego `--type=LoadBalancer` flagi. Poniżej przedstawiono kroki hello:

1. Uruchom nowe wdrożenie kontenera. Na przykład Witaj, po uruchomieniu polecenia nowe wdrożenie o nazwie `mynginx`. Wdrażanie Hello obejmuje trzy kontenery na podstawie obrazu Docker hello hello Nginx przez serwer sieci web.

    ```console
    kubectl run mynginx --replicas=3 --image nginx
    ```
2. Sprawdź, czy kontenery hello są uruchomione. Na przykład, jeśli zapytanie dla kontenerów hello z `kubectl get pods`, zobacz dane wyjściowe podobne toohello poniżej:

    ![Pobierz kontenery Nginx](./media/container-service-kubernetes-load-balancing/nginx-get-pods.png)

3. tooconfigure hello obciążenia tooaccept ruch zewnętrzny toohello. wdrożenie modułu równoważenia, uruchom `kubectl expose` z `--type=LoadBalancer`. Witaj następujące polecenie przedstawia hello Nginx serwera na porcie 80:

    ```console
    kubectl expose deployments mynginx --port=80 --type=LoadBalancer
    ```

4. Typ `kubectl get svc` toosee hello stan działania usług hello hello klastra. Podczas równoważenia obciążenia hello konfiguruje reguły hello, hello `EXTERNAL-IP` z hello usługi pojawia się jako `<pending>`. Po kilku minutach skonfigurowano hello zewnętrzny adres IP: 

    ![Konfigurowanie usługi równoważenia obciążenia Azure](./media/container-service-kubernetes-load-balancing/nginx-external-ip.png)

5. Upewnij się, że masz dostęp usługi hello na powitania zewnętrzny adres IP. Na przykład otwórz adres IP toohello przeglądarki sieci web wyświetlane. Przeglądarka Hello zawiera serwer sieci web Nginx hello uruchomiony w jednym hello kontenerów. Lub uruchom hello `curl` lub `wget` polecenia. Na przykład:

    ```
    curl 13.82.93.130
    ```

    Powinny zostać wyświetlone dane wyjściowe podobne do poniższych:

    ![Nginx dostępu z curl](./media/container-service-kubernetes-load-balancing/curl-output.png)

6. toosee hello konfiguracji równoważenia obciążenia Azure hello, przejdź toohello [portalu Azure](https://portal.azure.com).

7. Przeglądaj w poszukiwaniu hello grupy zasobów klastra usługi kontenera, a następnie wybierz hello modułu równoważenia obciążenia dla agenta hello maszyn wirtualnych. Jego nazwa powinna hello w taki sam jak hello usługi kontenera. (Nie wybierz hello modułu równoważenia obciążenia dla węzłów głównych hello, hello jedną, którego nazwa zawiera **master-lb**.) 

    ![Moduł równoważenia obciążenia w grupie zasobów](./media/container-service-kubernetes-load-balancing/container-resource-group-portal.png)

8. Szczegóły hello toosee hello konfiguracji usługi równoważenia obciążenia, kliknij przycisk **reguły równoważenia obciążenia** i hello Nazwa reguły hello, który został skonfigurowany.

    ![Reguły modułu równoważenia obciążenia](./media/container-service-kubernetes-load-balancing/load-balancing-rules.png) 

### <a name="example-specify-type-loadbalancer-in-hello-service-configuration-file"></a>Przykład: Określ `type: LoadBalancer` w pliku konfiguracji usługi hello

Jeśli wdrażania aplikacji kontenera Kubernetes z JSON lub yaml programu [pliku konfiguracji usługi](https://kubernetes.io/docs/user-guide/services/operations/#service-configuration-file), określić zewnętrznej usługi równoważenia obciążenia, dodając powitania po Specyfikacja usługi toohello wiersza:

```YAML
 "type": "LoadBalancer"
``` 



Witaj następujące kroki Użyj hello Kubernetes [przykład księgi gości](https://github.com/kubernetes/kubernetes/tree/master/examples/guestbook). W tym przykładzie jest to aplikacja sieci web w wielowarstwowych oparte na obrazach Redis i PHP Docker. Można określić w pliku konfiguracji usługi hello tego serwera PHP frontonu hello używa modułu równoważenia obciążenia Azure hello.

1. Pobierz plik hello `guestbook-all-in-one.yaml` z [GitHub](https://github.com/kubernetes/kubernetes/tree/master/examples/guestbook/all-in-one). 
2. Przeglądaj w poszukiwaniu hello `spec` dla hello `frontend` usługi.
3. Usuń komentarz linii hello `type: LoadBalancer`.

    ![Moduł równoważenia obciążenia w konfiguracji usługi](./media/container-service-kubernetes-load-balancing/guestbook-frontend-loadbalance.png)

4. Zapisz plik hello i wdrażanie aplikacji hello, uruchamiając następujące polecenie hello:

    ```
    kubectl create -f guestbook-all-in-one.yaml
    ```

5. Typ `kubectl get svc` toosee hello stan działania usług hello hello klastra. Podczas równoważenia obciążenia hello konfiguruje reguły hello, hello `EXTERNAL-IP` z hello `frontend` usługi pojawia się jako `<pending>`. Po kilku minutach skonfigurowano hello zewnętrzny adres IP: 

    ![Konfigurowanie usługi równoważenia obciążenia Azure](./media/container-service-kubernetes-load-balancing/guestbook-external-ip.png)

6. Upewnij się, że masz dostęp usługi hello na powitania zewnętrzny adres IP. Na przykład można otworzyć przeglądarki toohello zewnętrzny adres IP sieci web hello usługi.

    ![Zewnętrznie księgi gości dostępu](./media/container-service-kubernetes-load-balancing/guestbook-web.png)

    Można dodać wpisów księgi gości.

7. toosee hello konfiguracji równoważenia obciążenia Azure hello, wyszukaj zasobu usługi równoważenia obciążenia hello hello klastra w hello [portalu Azure](https://portal.azure.com). Zobacz kroki hello w poprzednim przykładzie hello.

### <a name="considerations"></a>Zagadnienia do rozważenia

* Tworzenie reguły modułu równoważenia obciążenia hello wykonywany asynchronicznie, i informacje o równoważenia hello udostępniane są publikowane w usłudze hello `status.loadBalancer` pola.
* Każda usługa zostanie automatycznie przypisany własną wirtualnego adresu IP w usłudze równoważenia obciążenia hello.
* Jeśli chcesz modułu równoważenia obciążenia hello tooreach na podstawie nazwy DNS, współpracować z Twojej domeny usługi dostawcy toocreate nazwy DNS dla adresu IP hello reguły.

## <a name="http-or-https-traffic"></a>Ruch HTTP lub HTTPS

Saldo tooload HTTP lub HTTPS toocontainer ruch sieci web aplikacji i zarządzać certyfikatami dla transport layer security (TLS), możesz użyć hello Kubernetes [wejściowych](https://kubernetes.io/docs/user-guide/ingress/) zasobów. Transfer danych przychodzących jest zbiorem reguł zezwalających na połączenia przychodzące tooreach hello klastra usług. Dla toowork zasobów wejściowych, hello Kubernetes klaster musi mieć [kontrolera wejściowych](https://kubernetes.io/docs/user-guide/ingress/#ingress-controllers) uruchomiona.

Usługa kontenera platformy Azure nie implementuje kontrolera wejściowych Kubernetes automatycznie. Dostępnych jest kilka implementacje kontrolera. Obecnie hello [kontrolera wejściowych Nginx](https://github.com/kubernetes/ingress/tree/master/examples/deployment/nginx) zaleca się tooconfigure transfer danych przychodzących reguł i równoważenie obciążenia ruchu HTTP i HTTPS. 

Aby uzyskać więcej informacji, zobacz hello [dokumentacji kontrolera wejściowych Nginx](https://github.com/kubernetes/ingress/tree/master/controllers/nginx/README.md).

> [!IMPORTANT]
> Korzystając z hello wejściowych Nginx kontrolera usługi kontenera platformy Azure, musi ujawniać hello wdrażania kontrolera usługi za pomocą `type: LoadBalancer`. Spowoduje to skonfigurowanie hello Azure obciążenia równoważenia tooroute ruchu toohello kontrolera. Aby uzyskać więcej informacji zobacz hello w poprzedniej sekcji.


## <a name="next-steps"></a>Następne kroki

* Zobacz hello [dokumentacji Kubernetes usługi równoważenia obciążenia](https://kubernetes.io/docs/user-guide/load-balancer/)
* Dowiedz się więcej o [kontrolerów Kubernetes przychodzące i wejściowych](https://kubernetes.io/docs/user-guide/ingress/)
* Zobacz [Kubernetes przykłady](https://github.com/kubernetes/kubernetes/tree/master/examples)

