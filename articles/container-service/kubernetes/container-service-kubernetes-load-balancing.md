---
title: "Równoważenie obciążenia kontenery Kubernetes na platformie Azure | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: ab46bb204f14424e394ced499ffbc0ef1cada15b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="load-balance-containers-in-a-kubernetes-cluster-in-azure-container-service"></a>Kontenery równoważenia obciążenia w klastrze Kubernetes usługi kontenera platformy Azure 
W tym artykule przedstawiono równoważenia obciążenia w klastrze Kubernetes usługi kontenera platformy Azure. Równoważenie obciążenia sieciowego zapewnia zewnętrznie dostępny adres IP dla usługi i dystrybuuje ruch sieciowy między stanowiskami uruchomionych w maszynach wirtualnych agenta.

Usługa Kubernetes można skonfigurować do używania [modułu równoważenia obciążenia Azure](../../load-balancer/load-balancer-overview.md) do zarządzania zewnętrznego ruchu sieciowego (TCP). Dodatkowa konfiguracja obciążenia routing ruchu HTTP lub HTTPS lub bardziej zaawansowanych scenariuszy i równoważenie są możliwe.

## <a name="prerequisites"></a>Wymagania wstępne
* [Wdrażanie klastra Kubernetes](container-service-kubernetes-walkthrough.md) usługi kontenera platformy Azure
* [Połączenia klienckie](../container-service-connect.md) do klastra

## <a name="azure-load-balancer"></a>Moduł równoważenia obciążenia Azure

Domyślnie klaster Kubernetes wdrożony w usłudze kontenera platformy Azure obejmuje usługi równoważenia obciążenia Azure internetowy agenta maszyn wirtualnych. (Zasób równoważenia obciążenia oddzielne jest skonfigurowany do wzorca maszyn wirtualnych). Moduł równoważenia obciążenia Azure jest usługą równoważenia obciążenia warstwy 4. Obecnie usługi równoważenia obciążenia obsługuje tylko ruch TCP w Kubernetes.

Podczas tworzenia usługi Kubernetes, można automatycznie skonfigurować usługę równoważenia obciążenia Azure, aby zezwolić na dostęp do usługi. Aby skonfigurować usługę równoważenia obciążenia, ustaw usługę `type` do `LoadBalancer`. Moduł równoważenia obciążenia tworzy regułę do mapowania na publiczny adres IP i numer portu przychodzącego ruchu usługi prywatnych adresów IP i numerów portów stanowiskami w agencie maszyny wirtualne (i odwrotnie dla ruchu odpowiedzi). 

 Poniżej przedstawiono dwa przykłady przedstawiająca sposób ustawić usługę Kubernetes `type` do `LoadBalancer`. (Po wypróbowaniu w przykładach, usunięcie wdrożenia nie jest już potrzebne.)

### <a name="example-use-the-kubectl-expose-command"></a>Przykład: Użyj `kubectl expose` polecenia 
[Wskazówki Kubernetes](container-service-kubernetes-walkthrough.md) zawiera przykładowy sposób do udostępnienia usługi z `kubectl expose` polecenia i jego `--type=LoadBalancer` flagi. Poniżej przedstawiono kroki:

1. Uruchom nowe wdrożenie kontenera. Na przykład następujące polecenie uruchamia nowe wdrożenie o nazwie `mynginx`. Wdrożenie składa się z trzech kontenerów na podstawie obrazu Docker Nginx serwera sieci web.

    ```console
    kubectl run mynginx --replicas=3 --image nginx
    ```
2. Sprawdź, czy z kontenerów. Na przykład, jeśli zapytanie dla kontenerów z `kubectl get pods`, zobacz dane wyjściowe podobne do następujących:

    ![Pobierz kontenery Nginx](./media/container-service-kubernetes-load-balancing/nginx-get-pods.png)

3. Aby skonfigurować usługę równoważenia obciążenia do akceptowania ruchu zewnętrznych do wdrożenia, uruchom `kubectl expose` z `--type=LoadBalancer`. Polecenie udostępnia serwer Nginx na porcie 80:

    ```console
    kubectl expose deployments mynginx --port=80 --type=LoadBalancer
    ```

4. Typ `kubectl get svc` aby zobaczyć stan usługi w klastrze. Gdy usługa równoważenia obciążenia konfiguruje regułę tak, `EXTERNAL-IP` usługi pojawia się jako `<pending>`. Po kilku minutach jest skonfigurowany jako zewnętrzny adres IP: 

    ![Konfigurowanie usługi równoważenia obciążenia Azure](./media/container-service-kubernetes-load-balancing/nginx-external-ip.png)

5. Upewnij się, że masz dostęp usługi przy użyciu zewnętrznego adresu IP. Na przykład otwórz przeglądarkę sieci web na adres IP podany. Przeglądarka pokazuje Nginx serwera sieci web działającego w jeden z kontenerów. Lub uruchom `curl` lub `wget` polecenia. Na przykład:

    ```
    curl 13.82.93.130
    ```

    Powinny pojawić się dane wyjściowe podobne do:

    ![Nginx dostępu z curl](./media/container-service-kubernetes-load-balancing/curl-output.png)

6. Aby sprawdzić konfigurację usługi równoważenia obciążenia Azure, przejdź do [portalu Azure](https://portal.azure.com).

7. Przeglądaj w poszukiwaniu grupy zasobów klastra usługi kontenera i wybierz usługę równoważenia obciążenia agenta maszyn wirtualnych. Jego nazwa powinna być taka sama jak usługi kontenera. (Nie należy wybierać usługi równoważenia obciążenia dla węzłów głównych jeden, którego nazwa zawiera **master-lb**.) 

    ![Moduł równoważenia obciążenia w grupie zasobów](./media/container-service-kubernetes-load-balancing/container-resource-group-portal.png)

8. Aby wyświetlić szczegóły konfiguracji usługi równoważenia obciążenia, kliknij przycisk **reguły równoważenia obciążenia** i nazwę reguły, które zostały skonfigurowane.

    ![Reguły modułu równoważenia obciążenia](./media/container-service-kubernetes-load-balancing/load-balancing-rules.png) 

### <a name="example-specify-type-loadbalancer-in-the-service-configuration-file"></a>Przykład: Określ `type: LoadBalancer` w pliku konfiguracji usługi

Jeśli wdrażania aplikacji kontenera Kubernetes z JSON lub yaml programu [pliku konfiguracji usługi](https://kubernetes.io/docs/user-guide/services/operations/#service-configuration-file), określić zewnętrznej usługi równoważenia obciążenia, dodając następujący wiersz w specyfikacji usług:

```YAML
 "type": "LoadBalancer"
``` 



Poniższe kroki Użyj Kubernetes [przykład księgi gości](https://github.com/kubernetes/kubernetes/tree/master/examples/guestbook). W tym przykładzie jest to aplikacja sieci web w wielowarstwowych oparte na obrazach Redis i PHP Docker. Można określić w pliku konfiguracji usługi równoważenia obciążenia Azure używane przez serwer PHP frontonu.

1. Pobierz plik `guestbook-all-in-one.yaml` z [GitHub](https://github.com/kubernetes/kubernetes/tree/master/examples/guestbook/all-in-one). 
2. Przeglądaj w poszukiwaniu `spec` dla `frontend` usługi.
3. Usuń komentarz z linii `type: LoadBalancer`.

    ![Moduł równoważenia obciążenia w konfiguracji usługi](./media/container-service-kubernetes-load-balancing/guestbook-frontend-loadbalance.png)

4. Zapisz plik i wdrażania aplikacji za pomocą następującego polecenia:

    ```
    kubectl create -f guestbook-all-in-one.yaml
    ```

5. Typ `kubectl get svc` aby zobaczyć stan usługi w klastrze. Gdy usługa równoważenia obciążenia konfiguruje regułę tak, `EXTERNAL-IP` z `frontend` usługi pojawia się jako `<pending>`. Po kilku minutach jest skonfigurowany jako zewnętrzny adres IP: 

    ![Konfigurowanie usługi równoważenia obciążenia Azure](./media/container-service-kubernetes-load-balancing/guestbook-external-ip.png)

6. Upewnij się, że masz dostęp usługi przy użyciu zewnętrznego adresu IP. Można na przykład otwórz przeglądarkę sieci web jako zewnętrzny adres IP usługi.

    ![Zewnętrznie księgi gości dostępu](./media/container-service-kubernetes-load-balancing/guestbook-web.png)

    Można dodać wpisów księgi gości.

7. Aby wyświetlić konfigurację usługi równoważenia obciążenia Azure, wyszukaj zasobu usługi równoważenia obciążenia dla klastra, w [portalu Azure](https://portal.azure.com). Zobacz kroki opisane w poprzednim przykładzie.

### <a name="considerations"></a>Zagadnienia do rozważenia

* Tworzenie reguły modułu równoważenia obciążenia wykonywany asynchronicznie, i informacje o elastycznie równoważenia są publikowane w usłudze `status.loadBalancer` pola.
* Każda usługa zostanie automatycznie przypisany własnego wirtualnego adresu IP w usłudze równoważenia obciążenia.
* Jeśli chcesz nawiązać połączenie z usługą równoważenia obciążenia za pomocą nazwy DNS, współpracować z dostawcą usług domeny do utworzenia nazwy DNS dla adresu IP reguły.

## <a name="http-or-https-traffic"></a>Ruch HTTP lub HTTPS

Aby ruch HTTP lub HTTPS do aplikacji sieci web kontenera równoważenia obciążenia i zarządzać certyfikatami dla transport layer security (TLS), można użyć Kubernetes [wejściowych](https://kubernetes.io/docs/user-guide/ingress/) zasobów. Transfer danych przychodzących jest kolekcją reguły zezwalające na połączenia przychodzące do uzyskania dostępu do usług klastra. Zasobu służąca do pracy Kubernetes klaster musi mieć [kontrolera wejściowych](https://kubernetes.io/docs/user-guide/ingress/#ingress-controllers) uruchomiona.

Usługa kontenera platformy Azure nie implementuje kontrolera wejściowych Kubernetes automatycznie. Dostępnych jest kilka implementacje kontrolera. Obecnie [kontrolera wejściowych Nginx](https://github.com/kubernetes/ingress/tree/master/examples/deployment/nginx) zaleca się, aby skonfigurować reguły wejściowych i zrównoważeniu ruchu HTTP i HTTPS. 

Aby uzyskać więcej informacji, zobacz [dokumentacji kontrolera wejściowych Nginx](https://github.com/kubernetes/ingress/tree/master/controllers/nginx/README.md).

> [!IMPORTANT]
> Korzystając z kontrolera wejściowych Nginx usługi kontenera platformy Azure, musi ujawniać wdrażanie kontrolera jako usługi za pomocą `type: LoadBalancer`. Spowoduje to skonfigurowanie usługi równoważenia obciążenia Azure można kierować ruchem do kontrolera. Aby uzyskać więcej informacji zobacz poprzedniej sekcji.


## <a name="next-steps"></a>Następne kroki

* Zobacz [dokumentacji Kubernetes usługi równoważenia obciążenia](https://kubernetes.io/docs/user-guide/load-balancer/)
* Dowiedz się więcej o [kontrolerów Kubernetes przychodzące i wejściowych](https://kubernetes.io/docs/user-guide/ingress/)
* Zobacz [Kubernetes przykłady](https://github.com/kubernetes/kubernetes/tree/master/examples)

