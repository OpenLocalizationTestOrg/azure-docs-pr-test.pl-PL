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
# <a name="load-balance-containers-in-a-kubernetes-cluster-in-azure-container-service"></a><span data-ttu-id="d5ce9-104">Kontenery równoważenia obciążenia w klastrze Kubernetes usługi kontenera platformy Azure</span><span class="sxs-lookup"><span data-stu-id="d5ce9-104">Load balance containers in a Kubernetes cluster in Azure Container Service</span></span> 
<span data-ttu-id="d5ce9-105">W tym artykule przedstawiono równoważenia obciążenia w klastrze Kubernetes usługi kontenera platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="d5ce9-105">This article introduces load balancing in a Kubernetes cluster in Azure Container Service.</span></span> <span data-ttu-id="d5ce9-106">Równoważenie obciążenia sieciowego zapewnia zewnętrznie dostępny adres IP dla usługi i dystrybuuje ruch sieciowy między stanowiskami uruchomionych w maszynach wirtualnych agenta.</span><span class="sxs-lookup"><span data-stu-id="d5ce9-106">Load balancing provides an externally accessible IP address for the service and distributes network traffic among the pods running in agent VMs.</span></span>

<span data-ttu-id="d5ce9-107">Usługa Kubernetes można skonfigurować do używania [modułu równoważenia obciążenia Azure](../../load-balancer/load-balancer-overview.md) do zarządzania zewnętrznego ruchu sieciowego (TCP).</span><span class="sxs-lookup"><span data-stu-id="d5ce9-107">You can set up a Kubernetes service to use [Azure Load Balancer](../../load-balancer/load-balancer-overview.md) to manage external network (TCP) traffic.</span></span> <span data-ttu-id="d5ce9-108">Dodatkowa konfiguracja obciążenia routing ruchu HTTP lub HTTPS lub bardziej zaawansowanych scenariuszy i równoważenie są możliwe.</span><span class="sxs-lookup"><span data-stu-id="d5ce9-108">With additional configuration, load balancing and routing of HTTP or HTTPS traffic or more advanced scenarios are possible.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d5ce9-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="d5ce9-109">Prerequisites</span></span>
* <span data-ttu-id="d5ce9-110">[Wdrażanie klastra Kubernetes](container-service-kubernetes-walkthrough.md) usługi kontenera platformy Azure</span><span class="sxs-lookup"><span data-stu-id="d5ce9-110">[Deploy a Kubernetes cluster](container-service-kubernetes-walkthrough.md) in Azure Container Service</span></span>
* <span data-ttu-id="d5ce9-111">[Połączenia klienckie](../container-service-connect.md) do klastra</span><span class="sxs-lookup"><span data-stu-id="d5ce9-111">[Connect your client](../container-service-connect.md) to your cluster</span></span>

## <a name="azure-load-balancer"></a><span data-ttu-id="d5ce9-112">Moduł równoważenia obciążenia Azure</span><span class="sxs-lookup"><span data-stu-id="d5ce9-112">Azure load balancer</span></span>

<span data-ttu-id="d5ce9-113">Domyślnie klaster Kubernetes wdrożony w usłudze kontenera platformy Azure obejmuje usługi równoważenia obciążenia Azure internetowy agenta maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="d5ce9-113">By default, a Kubernetes cluster deployed in Azure Container Service includes an Internet-facing Azure load balancer for the agent VMs.</span></span> <span data-ttu-id="d5ce9-114">(Zasób równoważenia obciążenia oddzielne jest skonfigurowany do wzorca maszyn wirtualnych). Moduł równoważenia obciążenia Azure jest usługą równoważenia obciążenia warstwy 4.</span><span class="sxs-lookup"><span data-stu-id="d5ce9-114">(A separate load balancer resource is configured for the master VMs.) Azure load balancer is a Layer 4 load balancer.</span></span> <span data-ttu-id="d5ce9-115">Obecnie usługi równoważenia obciążenia obsługuje tylko ruch TCP w Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="d5ce9-115">Currently, the load balancer only supports TCP traffic in Kubernetes.</span></span>

<span data-ttu-id="d5ce9-116">Podczas tworzenia usługi Kubernetes, można automatycznie skonfigurować usługę równoważenia obciążenia Azure, aby zezwolić na dostęp do usługi.</span><span class="sxs-lookup"><span data-stu-id="d5ce9-116">When creating a Kubernetes service, you can automatically configure the Azure load balancer to allow access to the service.</span></span> <span data-ttu-id="d5ce9-117">Aby skonfigurować usługę równoważenia obciążenia, ustaw usługę `type` do `LoadBalancer`.</span><span class="sxs-lookup"><span data-stu-id="d5ce9-117">To configure the load balancer, set the service `type` to `LoadBalancer`.</span></span> <span data-ttu-id="d5ce9-118">Moduł równoważenia obciążenia tworzy regułę do mapowania na publiczny adres IP i numer portu przychodzącego ruchu usługi prywatnych adresów IP i numerów portów stanowiskami w agencie maszyny wirtualne (i odwrotnie dla ruchu odpowiedzi).</span><span class="sxs-lookup"><span data-stu-id="d5ce9-118">The load balancer creates a rule to map a public IP address and port number of incoming service traffic to the private IP addresses and port numbers of the pods in agent VMs (and vice versa for response traffic).</span></span> 

 <span data-ttu-id="d5ce9-119">Poniżej przedstawiono dwa przykłady przedstawiająca sposób ustawić usługę Kubernetes `type` do `LoadBalancer`.</span><span class="sxs-lookup"><span data-stu-id="d5ce9-119">Following are two examples showing how to set the Kubernetes service `type` to `LoadBalancer`.</span></span> <span data-ttu-id="d5ce9-120">(Po wypróbowaniu w przykładach, usunięcie wdrożenia nie jest już potrzebne.)</span><span class="sxs-lookup"><span data-stu-id="d5ce9-120">(After trying the examples, delete the deployments if you no longer need them.)</span></span>

### <a name="example-use-the-kubectl-expose-command"></a><span data-ttu-id="d5ce9-121">Przykład: Użyj `kubectl expose` polecenia</span><span class="sxs-lookup"><span data-stu-id="d5ce9-121">Example: Use the `kubectl expose` command</span></span> 
<span data-ttu-id="d5ce9-122">[Wskazówki Kubernetes](container-service-kubernetes-walkthrough.md) zawiera przykładowy sposób do udostępnienia usługi z `kubectl expose` polecenia i jego `--type=LoadBalancer` flagi.</span><span class="sxs-lookup"><span data-stu-id="d5ce9-122">The [Kubernetes walkthrough](container-service-kubernetes-walkthrough.md) includes an example of how to expose a service with the `kubectl expose` command and its `--type=LoadBalancer` flag.</span></span> <span data-ttu-id="d5ce9-123">Poniżej przedstawiono kroki:</span><span class="sxs-lookup"><span data-stu-id="d5ce9-123">Here are the steps :</span></span>

1. <span data-ttu-id="d5ce9-124">Uruchom nowe wdrożenie kontenera.</span><span class="sxs-lookup"><span data-stu-id="d5ce9-124">Start a new container deployment.</span></span> <span data-ttu-id="d5ce9-125">Na przykład następujące polecenie uruchamia nowe wdrożenie o nazwie `mynginx`.</span><span class="sxs-lookup"><span data-stu-id="d5ce9-125">For example, the following command starts a new deployment called `mynginx`.</span></span> <span data-ttu-id="d5ce9-126">Wdrożenie składa się z trzech kontenerów na podstawie obrazu Docker Nginx serwera sieci web.</span><span class="sxs-lookup"><span data-stu-id="d5ce9-126">The deployment consists of three containers based on the Docker image for the Nginx web server.</span></span>

    ```console
    kubectl run mynginx --replicas=3 --image nginx
    ```
2. <span data-ttu-id="d5ce9-127">Sprawdź, czy z kontenerów.</span><span class="sxs-lookup"><span data-stu-id="d5ce9-127">Verify that the containers are running.</span></span> <span data-ttu-id="d5ce9-128">Na przykład, jeśli zapytanie dla kontenerów z `kubectl get pods`, zobacz dane wyjściowe podobne do następujących:</span><span class="sxs-lookup"><span data-stu-id="d5ce9-128">For example, if you query for the containers with `kubectl get pods`, you see output similar to the following:</span></span>

    ![Pobierz kontenery Nginx](./media/container-service-kubernetes-load-balancing/nginx-get-pods.png)

3. <span data-ttu-id="d5ce9-130">Aby skonfigurować usługę równoważenia obciążenia do akceptowania ruchu zewnętrznych do wdrożenia, uruchom `kubectl expose` z `--type=LoadBalancer`.</span><span class="sxs-lookup"><span data-stu-id="d5ce9-130">To configure the load balancer to accept external traffic to the deployment, run `kubectl expose` with `--type=LoadBalancer`.</span></span> <span data-ttu-id="d5ce9-131">Polecenie udostępnia serwer Nginx na porcie 80:</span><span class="sxs-lookup"><span data-stu-id="d5ce9-131">The following command exposes the Nginx server on port 80:</span></span>

    ```console
    kubectl expose deployments mynginx --port=80 --type=LoadBalancer
    ```

4. <span data-ttu-id="d5ce9-132">Typ `kubectl get svc` aby zobaczyć stan usługi w klastrze.</span><span class="sxs-lookup"><span data-stu-id="d5ce9-132">Type `kubectl get svc` to see the state of the services in the cluster.</span></span> <span data-ttu-id="d5ce9-133">Gdy usługa równoważenia obciążenia konfiguruje regułę tak, `EXTERNAL-IP` usługi pojawia się jako `<pending>`.</span><span class="sxs-lookup"><span data-stu-id="d5ce9-133">While the load balancer configures the rule, the `EXTERNAL-IP` of the service appears as `<pending>`.</span></span> <span data-ttu-id="d5ce9-134">Po kilku minutach jest skonfigurowany jako zewnętrzny adres IP:</span><span class="sxs-lookup"><span data-stu-id="d5ce9-134">After a few minutes, the external IP address is configured:</span></span> 

    ![Konfigurowanie usługi równoważenia obciążenia Azure](./media/container-service-kubernetes-load-balancing/nginx-external-ip.png)

5. <span data-ttu-id="d5ce9-136">Upewnij się, że masz dostęp usługi przy użyciu zewnętrznego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="d5ce9-136">Verify that you can access the service at the external IP address.</span></span> <span data-ttu-id="d5ce9-137">Na przykład otwórz przeglądarkę sieci web na adres IP podany.</span><span class="sxs-lookup"><span data-stu-id="d5ce9-137">For example, open a web browser to the IP address shown.</span></span> <span data-ttu-id="d5ce9-138">Przeglądarka pokazuje Nginx serwera sieci web działającego w jeden z kontenerów.</span><span class="sxs-lookup"><span data-stu-id="d5ce9-138">The browser shows the Nginx web server running in one of the containers.</span></span> <span data-ttu-id="d5ce9-139">Lub uruchom `curl` lub `wget` polecenia.</span><span class="sxs-lookup"><span data-stu-id="d5ce9-139">Or, run the `curl` or `wget` command.</span></span> <span data-ttu-id="d5ce9-140">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="d5ce9-140">For example:</span></span>

    ```
    curl 13.82.93.130
    ```

    <span data-ttu-id="d5ce9-141">Powinny pojawić się dane wyjściowe podobne do:</span><span class="sxs-lookup"><span data-stu-id="d5ce9-141">You should see output similar to:</span></span>

    ![Nginx dostępu z curl](./media/container-service-kubernetes-load-balancing/curl-output.png)

6. <span data-ttu-id="d5ce9-143">Aby sprawdzić konfigurację usługi równoważenia obciążenia Azure, przejdź do [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d5ce9-143">To see the configuration of the Azure load balancer, go to the [Azure portal](https://portal.azure.com).</span></span>

7. <span data-ttu-id="d5ce9-144">Przeglądaj w poszukiwaniu grupy zasobów klastra usługi kontenera i wybierz usługę równoważenia obciążenia agenta maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="d5ce9-144">Browse for the resource group for your container service cluster, and select the load balancer for the agent VMs.</span></span> <span data-ttu-id="d5ce9-145">Jego nazwa powinna być taka sama jak usługi kontenera.</span><span class="sxs-lookup"><span data-stu-id="d5ce9-145">Its name should be the same as the container service.</span></span> <span data-ttu-id="d5ce9-146">(Nie należy wybierać usługi równoważenia obciążenia dla węzłów głównych jeden, którego nazwa zawiera **master-lb**.)</span><span class="sxs-lookup"><span data-stu-id="d5ce9-146">(Don't choose the load balancer for the master nodes, the one whose name includes **master-lb**.)</span></span> 

    ![Moduł równoważenia obciążenia w grupie zasobów](./media/container-service-kubernetes-load-balancing/container-resource-group-portal.png)

8. <span data-ttu-id="d5ce9-148">Aby wyświetlić szczegóły konfiguracji usługi równoważenia obciążenia, kliknij przycisk **reguły równoważenia obciążenia** i nazwę reguły, które zostały skonfigurowane.</span><span class="sxs-lookup"><span data-stu-id="d5ce9-148">To see the details of the load balancer configuration, click **Load balancing rules** and the name of the rule that was configured.</span></span>

    ![Reguły modułu równoważenia obciążenia](./media/container-service-kubernetes-load-balancing/load-balancing-rules.png) 

### <a name="example-specify-type-loadbalancer-in-the-service-configuration-file"></a><span data-ttu-id="d5ce9-150">Przykład: Określ `type: LoadBalancer` w pliku konfiguracji usługi</span><span class="sxs-lookup"><span data-stu-id="d5ce9-150">Example: Specify `type: LoadBalancer` in the service configuration file</span></span>

<span data-ttu-id="d5ce9-151">Jeśli wdrażania aplikacji kontenera Kubernetes z JSON lub yaml programu [pliku konfiguracji usługi](https://kubernetes.io/docs/user-guide/services/operations/#service-configuration-file), określić zewnętrznej usługi równoważenia obciążenia, dodając następujący wiersz w specyfikacji usług:</span><span class="sxs-lookup"><span data-stu-id="d5ce9-151">If you deploy a Kubernetes container app from a YAML or JSON [service configuration file](https://kubernetes.io/docs/user-guide/services/operations/#service-configuration-file), specify an external load balancer by adding the following line to the service specification:</span></span>

```YAML
 "type": "LoadBalancer"
``` 



<span data-ttu-id="d5ce9-152">Poniższe kroki Użyj Kubernetes [przykład księgi gości](https://github.com/kubernetes/kubernetes/tree/master/examples/guestbook).</span><span class="sxs-lookup"><span data-stu-id="d5ce9-152">The following steps use the Kubernetes [Guestbook example](https://github.com/kubernetes/kubernetes/tree/master/examples/guestbook).</span></span> <span data-ttu-id="d5ce9-153">W tym przykładzie jest to aplikacja sieci web w wielowarstwowych oparte na obrazach Redis i PHP Docker.</span><span class="sxs-lookup"><span data-stu-id="d5ce9-153">This example is a multi-tier web app based on  Redis and PHP Docker images.</span></span> <span data-ttu-id="d5ce9-154">Można określić w pliku konfiguracji usługi równoważenia obciążenia Azure używane przez serwer PHP frontonu.</span><span class="sxs-lookup"><span data-stu-id="d5ce9-154">You can specify in the service configuration file that the frontend PHP server uses the Azure load balancer.</span></span>

1. <span data-ttu-id="d5ce9-155">Pobierz plik `guestbook-all-in-one.yaml` z [GitHub](https://github.com/kubernetes/kubernetes/tree/master/examples/guestbook/all-in-one).</span><span class="sxs-lookup"><span data-stu-id="d5ce9-155">Download the file `guestbook-all-in-one.yaml` from [GitHub](https://github.com/kubernetes/kubernetes/tree/master/examples/guestbook/all-in-one).</span></span> 
2. <span data-ttu-id="d5ce9-156">Przeglądaj w poszukiwaniu `spec` dla `frontend` usługi.</span><span class="sxs-lookup"><span data-stu-id="d5ce9-156">Browse for the `spec` for the `frontend` service.</span></span>
3. <span data-ttu-id="d5ce9-157">Usuń komentarz z linii `type: LoadBalancer`.</span><span class="sxs-lookup"><span data-stu-id="d5ce9-157">Uncomment the line `type: LoadBalancer`.</span></span>

    ![Moduł równoważenia obciążenia w konfiguracji usługi](./media/container-service-kubernetes-load-balancing/guestbook-frontend-loadbalance.png)

4. <span data-ttu-id="d5ce9-159">Zapisz plik i wdrażania aplikacji za pomocą następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="d5ce9-159">Save the file, and deploy the app by running the following command:</span></span>

    ```
    kubectl create -f guestbook-all-in-one.yaml
    ```

5. <span data-ttu-id="d5ce9-160">Typ `kubectl get svc` aby zobaczyć stan usługi w klastrze.</span><span class="sxs-lookup"><span data-stu-id="d5ce9-160">Type `kubectl get svc` to see the state of the services in the cluster.</span></span> <span data-ttu-id="d5ce9-161">Gdy usługa równoważenia obciążenia konfiguruje regułę tak, `EXTERNAL-IP` z `frontend` usługi pojawia się jako `<pending>`.</span><span class="sxs-lookup"><span data-stu-id="d5ce9-161">While the load balancer configures the rule, the `EXTERNAL-IP` of the `frontend` service appears as `<pending>`.</span></span> <span data-ttu-id="d5ce9-162">Po kilku minutach jest skonfigurowany jako zewnętrzny adres IP:</span><span class="sxs-lookup"><span data-stu-id="d5ce9-162">After a few minutes, the external IP address is configured:</span></span> 

    ![Konfigurowanie usługi równoważenia obciążenia Azure](./media/container-service-kubernetes-load-balancing/guestbook-external-ip.png)

6. <span data-ttu-id="d5ce9-164">Upewnij się, że masz dostęp usługi przy użyciu zewnętrznego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="d5ce9-164">Verify that you can access the service at the external IP address.</span></span> <span data-ttu-id="d5ce9-165">Można na przykład otwórz przeglądarkę sieci web jako zewnętrzny adres IP usługi.</span><span class="sxs-lookup"><span data-stu-id="d5ce9-165">For example, you can open a web browser to the external IP address of the service.</span></span>

    ![Zewnętrznie księgi gości dostępu](./media/container-service-kubernetes-load-balancing/guestbook-web.png)

    <span data-ttu-id="d5ce9-167">Można dodać wpisów księgi gości.</span><span class="sxs-lookup"><span data-stu-id="d5ce9-167">You can add guestbook entries.</span></span>

7. <span data-ttu-id="d5ce9-168">Aby wyświetlić konfigurację usługi równoważenia obciążenia Azure, wyszukaj zasobu usługi równoważenia obciążenia dla klastra, w [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d5ce9-168">To see the configuration of the Azure load balancer, browse for the load balancer resource for the cluster in the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="d5ce9-169">Zobacz kroki opisane w poprzednim przykładzie.</span><span class="sxs-lookup"><span data-stu-id="d5ce9-169">See the steps in the previous example.</span></span>

### <a name="considerations"></a><span data-ttu-id="d5ce9-170">Zagadnienia do rozważenia</span><span class="sxs-lookup"><span data-stu-id="d5ce9-170">Considerations</span></span>

* <span data-ttu-id="d5ce9-171">Tworzenie reguły modułu równoważenia obciążenia wykonywany asynchronicznie, i informacje o elastycznie równoważenia są publikowane w usłudze `status.loadBalancer` pola.</span><span class="sxs-lookup"><span data-stu-id="d5ce9-171">Creation of the load balancer rule happens asynchronously, and information about the provisioned balancer is published in the service’s `status.loadBalancer` field.</span></span>
* <span data-ttu-id="d5ce9-172">Każda usługa zostanie automatycznie przypisany własnego wirtualnego adresu IP w usłudze równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="d5ce9-172">Every service is automatically assigned its own virtual IP address in the load balancer.</span></span>
* <span data-ttu-id="d5ce9-173">Jeśli chcesz nawiązać połączenie z usługą równoważenia obciążenia za pomocą nazwy DNS, współpracować z dostawcą usług domeny do utworzenia nazwy DNS dla adresu IP reguły.</span><span class="sxs-lookup"><span data-stu-id="d5ce9-173">If you want to reach the load balancer by a DNS name, work with your domain service provider to create a DNS name for the rule's IP address.</span></span>

## <a name="http-or-https-traffic"></a><span data-ttu-id="d5ce9-174">Ruch HTTP lub HTTPS</span><span class="sxs-lookup"><span data-stu-id="d5ce9-174">HTTP or HTTPS traffic</span></span>

<span data-ttu-id="d5ce9-175">Aby ruch HTTP lub HTTPS do aplikacji sieci web kontenera równoważenia obciążenia i zarządzać certyfikatami dla transport layer security (TLS), można użyć Kubernetes [wejściowych](https://kubernetes.io/docs/user-guide/ingress/) zasobów.</span><span class="sxs-lookup"><span data-stu-id="d5ce9-175">To load balance HTTP or HTTPS traffic to container web apps and manage certificates for transport layer security (TLS), you can use the Kubernetes [Ingress](https://kubernetes.io/docs/user-guide/ingress/) resource.</span></span> <span data-ttu-id="d5ce9-176">Transfer danych przychodzących jest kolekcją reguły zezwalające na połączenia przychodzące do uzyskania dostępu do usług klastra.</span><span class="sxs-lookup"><span data-stu-id="d5ce9-176">An Ingress is a collection of rules that allow inbound connections to reach the cluster services.</span></span> <span data-ttu-id="d5ce9-177">Zasobu służąca do pracy Kubernetes klaster musi mieć [kontrolera wejściowych](https://kubernetes.io/docs/user-guide/ingress/#ingress-controllers) uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="d5ce9-177">For an Ingress resource to work, the Kubernetes cluster must have an [Ingress controller](https://kubernetes.io/docs/user-guide/ingress/#ingress-controllers) running.</span></span>

<span data-ttu-id="d5ce9-178">Usługa kontenera platformy Azure nie implementuje kontrolera wejściowych Kubernetes automatycznie.</span><span class="sxs-lookup"><span data-stu-id="d5ce9-178">Azure Container Service does not implement a Kubernetes Ingress controller automatically.</span></span> <span data-ttu-id="d5ce9-179">Dostępnych jest kilka implementacje kontrolera.</span><span class="sxs-lookup"><span data-stu-id="d5ce9-179">Several controller implementations are available.</span></span> <span data-ttu-id="d5ce9-180">Obecnie [kontrolera wejściowych Nginx](https://github.com/kubernetes/ingress/tree/master/examples/deployment/nginx) zaleca się, aby skonfigurować reguły wejściowych i zrównoważeniu ruchu HTTP i HTTPS.</span><span class="sxs-lookup"><span data-stu-id="d5ce9-180">Currently, the [Nginx Ingress controller](https://github.com/kubernetes/ingress/tree/master/examples/deployment/nginx) is recommended to configure Ingress rules and load balance HTTP and HTTPS traffic.</span></span> 

<span data-ttu-id="d5ce9-181">Aby uzyskać więcej informacji, zobacz [dokumentacji kontrolera wejściowych Nginx](https://github.com/kubernetes/ingress/tree/master/controllers/nginx/README.md).</span><span class="sxs-lookup"><span data-stu-id="d5ce9-181">For more information, see the [Nginx Ingress controller documentation](https://github.com/kubernetes/ingress/tree/master/controllers/nginx/README.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d5ce9-182">Korzystając z kontrolera wejściowych Nginx usługi kontenera platformy Azure, musi ujawniać wdrażanie kontrolera jako usługi za pomocą `type: LoadBalancer`.</span><span class="sxs-lookup"><span data-stu-id="d5ce9-182">When using the Nginx Ingress controller in Azure Container Service, you must expose the controller deployment as a service with `type: LoadBalancer`.</span></span> <span data-ttu-id="d5ce9-183">Spowoduje to skonfigurowanie usługi równoważenia obciążenia Azure można kierować ruchem do kontrolera.</span><span class="sxs-lookup"><span data-stu-id="d5ce9-183">This configures the Azure load balancer to route traffic to the controller.</span></span> <span data-ttu-id="d5ce9-184">Aby uzyskać więcej informacji zobacz poprzedniej sekcji.</span><span class="sxs-lookup"><span data-stu-id="d5ce9-184">For more information, see the previous section.</span></span>


## <a name="next-steps"></a><span data-ttu-id="d5ce9-185">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d5ce9-185">Next steps</span></span>

* <span data-ttu-id="d5ce9-186">Zobacz [dokumentacji Kubernetes usługi równoważenia obciążenia](https://kubernetes.io/docs/user-guide/load-balancer/)</span><span class="sxs-lookup"><span data-stu-id="d5ce9-186">See the [Kubernetes LoadBalancer documentation](https://kubernetes.io/docs/user-guide/load-balancer/)</span></span>
* <span data-ttu-id="d5ce9-187">Dowiedz się więcej o [kontrolerów Kubernetes przychodzące i wejściowych](https://kubernetes.io/docs/user-guide/ingress/)</span><span class="sxs-lookup"><span data-stu-id="d5ce9-187">Learn more about [Kubernetes Ingress and Ingress controllers](https://kubernetes.io/docs/user-guide/ingress/)</span></span>
* <span data-ttu-id="d5ce9-188">Zobacz [Kubernetes przykłady](https://github.com/kubernetes/kubernetes/tree/master/examples)</span><span class="sxs-lookup"><span data-stu-id="d5ce9-188">See [Kubernetes examples](https://github.com/kubernetes/kubernetes/tree/master/examples)</span></span>

