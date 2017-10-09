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
# <a name="load-balance-containers-in-a-kubernetes-cluster-in-azure-container-service"></a><span data-ttu-id="350d1-104">Kontenery równoważenia obciążenia w klastrze Kubernetes usługi kontenera platformy Azure</span><span class="sxs-lookup"><span data-stu-id="350d1-104">Load balance containers in a Kubernetes cluster in Azure Container Service</span></span> 
<span data-ttu-id="350d1-105">W tym artykule przedstawiono równoważenia obciążenia w klastrze Kubernetes usługi kontenera platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="350d1-105">This article introduces load balancing in a Kubernetes cluster in Azure Container Service.</span></span> <span data-ttu-id="350d1-106">Równoważenie obciążenia sieciowego zapewnia zewnętrznie dostępny adres IP dla usługi hello i dystrybuuje ruch sieciowy między stanowiskami hello uruchomionych w maszynach wirtualnych agenta.</span><span class="sxs-lookup"><span data-stu-id="350d1-106">Load balancing provides an externally accessible IP address for hello service and distributes network traffic among hello pods running in agent VMs.</span></span>

<span data-ttu-id="350d1-107">Możesz skonfigurować toouse usługi Kubernetes [modułu równoważenia obciążenia Azure](../../load-balancer/load-balancer-overview.md) toomanage zewnętrznego ruchu sieciowego (TCP).</span><span class="sxs-lookup"><span data-stu-id="350d1-107">You can set up a Kubernetes service toouse [Azure Load Balancer](../../load-balancer/load-balancer-overview.md) toomanage external network (TCP) traffic.</span></span> <span data-ttu-id="350d1-108">Dodatkowa konfiguracja obciążenia routing ruchu HTTP lub HTTPS lub bardziej zaawansowanych scenariuszy i równoważenie są możliwe.</span><span class="sxs-lookup"><span data-stu-id="350d1-108">With additional configuration, load balancing and routing of HTTP or HTTPS traffic or more advanced scenarios are possible.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="350d1-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="350d1-109">Prerequisites</span></span>
* <span data-ttu-id="350d1-110">[Wdrażanie klastra Kubernetes](container-service-kubernetes-walkthrough.md) usługi kontenera platformy Azure</span><span class="sxs-lookup"><span data-stu-id="350d1-110">[Deploy a Kubernetes cluster](container-service-kubernetes-walkthrough.md) in Azure Container Service</span></span>
* <span data-ttu-id="350d1-111">[Połączenia klienckie](../container-service-connect.md) tooyour klastra</span><span class="sxs-lookup"><span data-stu-id="350d1-111">[Connect your client](../container-service-connect.md) tooyour cluster</span></span>

## <a name="azure-load-balancer"></a><span data-ttu-id="350d1-112">Moduł równoważenia obciążenia Azure</span><span class="sxs-lookup"><span data-stu-id="350d1-112">Azure load balancer</span></span>

<span data-ttu-id="350d1-113">Domyślnie klaster Kubernetes wdrożony w usłudze kontenera platformy Azure obejmuje usługę równoważenia obciążenia Azure internetowy agenta hello maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="350d1-113">By default, a Kubernetes cluster deployed in Azure Container Service includes an Internet-facing Azure load balancer for hello agent VMs.</span></span> <span data-ttu-id="350d1-114">(Zasób równoważenia obciążenia oddzielne jest skonfigurowany do wzorca hello maszyn wirtualnych). Moduł równoważenia obciążenia Azure jest usługą równoważenia obciążenia warstwy 4.</span><span class="sxs-lookup"><span data-stu-id="350d1-114">(A separate load balancer resource is configured for hello master VMs.) Azure load balancer is a Layer 4 load balancer.</span></span> <span data-ttu-id="350d1-115">Obecnie hello modułu równoważenia obciążenia obsługuje tylko ruch TCP w Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="350d1-115">Currently, hello load balancer only supports TCP traffic in Kubernetes.</span></span>

<span data-ttu-id="350d1-116">Podczas tworzenia usługi Kubernetes, można automatycznie skonfigurować hello Azure usługi równoważenia obciążenia używanej tooallow dostępu toohello.</span><span class="sxs-lookup"><span data-stu-id="350d1-116">When creating a Kubernetes service, you can automatically configure hello Azure load balancer tooallow access toohello service.</span></span> <span data-ttu-id="350d1-117">tooconfigure hello moduł równoważenia obciążenia usługi hello zestaw `type` zbyt`LoadBalancer`.</span><span class="sxs-lookup"><span data-stu-id="350d1-117">tooconfigure hello load balancer, set hello service `type` too`LoadBalancer`.</span></span> <span data-ttu-id="350d1-118">Moduł równoważenia obciążenia Hello tworzy toomap reguły publiczny adres IP i numer portu przychodzącego usługi ruchu toohello prywatnych adresów IP i numerów portów stanowiskami hello w agencie maszyny wirtualne (i odwrotnie dla ruchu odpowiedzi).</span><span class="sxs-lookup"><span data-stu-id="350d1-118">hello load balancer creates a rule toomap a public IP address and port number of incoming service traffic toohello private IP addresses and port numbers of hello pods in agent VMs (and vice versa for response traffic).</span></span> 

 <span data-ttu-id="350d1-119">Poniżej przedstawiono dwa przykłady przedstawiający sposób tooset hello usługi Kubernetes `type` zbyt`LoadBalancer`.</span><span class="sxs-lookup"><span data-stu-id="350d1-119">Following are two examples showing how tooset hello Kubernetes service `type` too`LoadBalancer`.</span></span> <span data-ttu-id="350d1-120">(Po próbie przykłady hello, usunięcie wdrożeń hello nie jest już potrzebne.)</span><span class="sxs-lookup"><span data-stu-id="350d1-120">(After trying hello examples, delete hello deployments if you no longer need them.)</span></span>

### <a name="example-use-hello-kubectl-expose-command"></a><span data-ttu-id="350d1-121">Przykład: Użyj hello `kubectl expose` polecenia</span><span class="sxs-lookup"><span data-stu-id="350d1-121">Example: Use hello `kubectl expose` command</span></span> 
<span data-ttu-id="350d1-122">Witaj [wskazówki Kubernetes](container-service-kubernetes-walkthrough.md) zawiera przykładowy sposób tooexpose usługi za pomocą hello `kubectl expose` polecenia i jego `--type=LoadBalancer` flagi.</span><span class="sxs-lookup"><span data-stu-id="350d1-122">hello [Kubernetes walkthrough](container-service-kubernetes-walkthrough.md) includes an example of how tooexpose a service with hello `kubectl expose` command and its `--type=LoadBalancer` flag.</span></span> <span data-ttu-id="350d1-123">Poniżej przedstawiono kroki hello:</span><span class="sxs-lookup"><span data-stu-id="350d1-123">Here are hello steps :</span></span>

1. <span data-ttu-id="350d1-124">Uruchom nowe wdrożenie kontenera.</span><span class="sxs-lookup"><span data-stu-id="350d1-124">Start a new container deployment.</span></span> <span data-ttu-id="350d1-125">Na przykład Witaj, po uruchomieniu polecenia nowe wdrożenie o nazwie `mynginx`.</span><span class="sxs-lookup"><span data-stu-id="350d1-125">For example, hello following command starts a new deployment called `mynginx`.</span></span> <span data-ttu-id="350d1-126">Wdrażanie Hello obejmuje trzy kontenery na podstawie obrazu Docker hello hello Nginx przez serwer sieci web.</span><span class="sxs-lookup"><span data-stu-id="350d1-126">hello deployment consists of three containers based on hello Docker image for hello Nginx web server.</span></span>

    ```console
    kubectl run mynginx --replicas=3 --image nginx
    ```
2. <span data-ttu-id="350d1-127">Sprawdź, czy kontenery hello są uruchomione.</span><span class="sxs-lookup"><span data-stu-id="350d1-127">Verify that hello containers are running.</span></span> <span data-ttu-id="350d1-128">Na przykład, jeśli zapytanie dla kontenerów hello z `kubectl get pods`, zobacz dane wyjściowe podobne toohello poniżej:</span><span class="sxs-lookup"><span data-stu-id="350d1-128">For example, if you query for hello containers with `kubectl get pods`, you see output similar toohello following:</span></span>

    ![Pobierz kontenery Nginx](./media/container-service-kubernetes-load-balancing/nginx-get-pods.png)

3. <span data-ttu-id="350d1-130">tooconfigure hello obciążenia tooaccept ruch zewnętrzny toohello. wdrożenie modułu równoważenia, uruchom `kubectl expose` z `--type=LoadBalancer`.</span><span class="sxs-lookup"><span data-stu-id="350d1-130">tooconfigure hello load balancer tooaccept external traffic toohello deployment, run `kubectl expose` with `--type=LoadBalancer`.</span></span> <span data-ttu-id="350d1-131">Witaj następujące polecenie przedstawia hello Nginx serwera na porcie 80:</span><span class="sxs-lookup"><span data-stu-id="350d1-131">hello following command exposes hello Nginx server on port 80:</span></span>

    ```console
    kubectl expose deployments mynginx --port=80 --type=LoadBalancer
    ```

4. <span data-ttu-id="350d1-132">Typ `kubectl get svc` toosee hello stan działania usług hello hello klastra.</span><span class="sxs-lookup"><span data-stu-id="350d1-132">Type `kubectl get svc` toosee hello state of hello services in hello cluster.</span></span> <span data-ttu-id="350d1-133">Podczas równoważenia obciążenia hello konfiguruje reguły hello, hello `EXTERNAL-IP` z hello usługi pojawia się jako `<pending>`.</span><span class="sxs-lookup"><span data-stu-id="350d1-133">While hello load balancer configures hello rule, hello `EXTERNAL-IP` of hello service appears as `<pending>`.</span></span> <span data-ttu-id="350d1-134">Po kilku minutach skonfigurowano hello zewnętrzny adres IP:</span><span class="sxs-lookup"><span data-stu-id="350d1-134">After a few minutes, hello external IP address is configured:</span></span> 

    ![Konfigurowanie usługi równoważenia obciążenia Azure](./media/container-service-kubernetes-load-balancing/nginx-external-ip.png)

5. <span data-ttu-id="350d1-136">Upewnij się, że masz dostęp usługi hello na powitania zewnętrzny adres IP.</span><span class="sxs-lookup"><span data-stu-id="350d1-136">Verify that you can access hello service at hello external IP address.</span></span> <span data-ttu-id="350d1-137">Na przykład otwórz adres IP toohello przeglądarki sieci web wyświetlane.</span><span class="sxs-lookup"><span data-stu-id="350d1-137">For example, open a web browser toohello IP address shown.</span></span> <span data-ttu-id="350d1-138">Przeglądarka Hello zawiera serwer sieci web Nginx hello uruchomiony w jednym hello kontenerów.</span><span class="sxs-lookup"><span data-stu-id="350d1-138">hello browser shows hello Nginx web server running in one of hello containers.</span></span> <span data-ttu-id="350d1-139">Lub uruchom hello `curl` lub `wget` polecenia.</span><span class="sxs-lookup"><span data-stu-id="350d1-139">Or, run hello `curl` or `wget` command.</span></span> <span data-ttu-id="350d1-140">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="350d1-140">For example:</span></span>

    ```
    curl 13.82.93.130
    ```

    <span data-ttu-id="350d1-141">Powinny zostać wyświetlone dane wyjściowe podobne do poniższych:</span><span class="sxs-lookup"><span data-stu-id="350d1-141">You should see output similar to:</span></span>

    ![Nginx dostępu z curl](./media/container-service-kubernetes-load-balancing/curl-output.png)

6. <span data-ttu-id="350d1-143">toosee hello konfiguracji równoważenia obciążenia Azure hello, przejdź toohello [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="350d1-143">toosee hello configuration of hello Azure load balancer, go toohello [Azure portal](https://portal.azure.com).</span></span>

7. <span data-ttu-id="350d1-144">Przeglądaj w poszukiwaniu hello grupy zasobów klastra usługi kontenera, a następnie wybierz hello modułu równoważenia obciążenia dla agenta hello maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="350d1-144">Browse for hello resource group for your container service cluster, and select hello load balancer for hello agent VMs.</span></span> <span data-ttu-id="350d1-145">Jego nazwa powinna hello w taki sam jak hello usługi kontenera.</span><span class="sxs-lookup"><span data-stu-id="350d1-145">Its name should be hello same as hello container service.</span></span> <span data-ttu-id="350d1-146">(Nie wybierz hello modułu równoważenia obciążenia dla węzłów głównych hello, hello jedną, którego nazwa zawiera **master-lb**.)</span><span class="sxs-lookup"><span data-stu-id="350d1-146">(Don't choose hello load balancer for hello master nodes, hello one whose name includes **master-lb**.)</span></span> 

    ![Moduł równoważenia obciążenia w grupie zasobów](./media/container-service-kubernetes-load-balancing/container-resource-group-portal.png)

8. <span data-ttu-id="350d1-148">Szczegóły hello toosee hello konfiguracji usługi równoważenia obciążenia, kliknij przycisk **reguły równoważenia obciążenia** i hello Nazwa reguły hello, który został skonfigurowany.</span><span class="sxs-lookup"><span data-stu-id="350d1-148">toosee hello details of hello load balancer configuration, click **Load balancing rules** and hello name of hello rule that was configured.</span></span>

    ![Reguły modułu równoważenia obciążenia](./media/container-service-kubernetes-load-balancing/load-balancing-rules.png) 

### <a name="example-specify-type-loadbalancer-in-hello-service-configuration-file"></a><span data-ttu-id="350d1-150">Przykład: Określ `type: LoadBalancer` w pliku konfiguracji usługi hello</span><span class="sxs-lookup"><span data-stu-id="350d1-150">Example: Specify `type: LoadBalancer` in hello service configuration file</span></span>

<span data-ttu-id="350d1-151">Jeśli wdrażania aplikacji kontenera Kubernetes z JSON lub yaml programu [pliku konfiguracji usługi](https://kubernetes.io/docs/user-guide/services/operations/#service-configuration-file), określić zewnętrznej usługi równoważenia obciążenia, dodając powitania po Specyfikacja usługi toohello wiersza:</span><span class="sxs-lookup"><span data-stu-id="350d1-151">If you deploy a Kubernetes container app from a YAML or JSON [service configuration file](https://kubernetes.io/docs/user-guide/services/operations/#service-configuration-file), specify an external load balancer by adding hello following line toohello service specification:</span></span>

```YAML
 "type": "LoadBalancer"
``` 



<span data-ttu-id="350d1-152">Witaj następujące kroki Użyj hello Kubernetes [przykład księgi gości](https://github.com/kubernetes/kubernetes/tree/master/examples/guestbook).</span><span class="sxs-lookup"><span data-stu-id="350d1-152">hello following steps use hello Kubernetes [Guestbook example](https://github.com/kubernetes/kubernetes/tree/master/examples/guestbook).</span></span> <span data-ttu-id="350d1-153">W tym przykładzie jest to aplikacja sieci web w wielowarstwowych oparte na obrazach Redis i PHP Docker.</span><span class="sxs-lookup"><span data-stu-id="350d1-153">This example is a multi-tier web app based on  Redis and PHP Docker images.</span></span> <span data-ttu-id="350d1-154">Można określić w pliku konfiguracji usługi hello tego serwera PHP frontonu hello używa modułu równoważenia obciążenia Azure hello.</span><span class="sxs-lookup"><span data-stu-id="350d1-154">You can specify in hello service configuration file that hello frontend PHP server uses hello Azure load balancer.</span></span>

1. <span data-ttu-id="350d1-155">Pobierz plik hello `guestbook-all-in-one.yaml` z [GitHub](https://github.com/kubernetes/kubernetes/tree/master/examples/guestbook/all-in-one).</span><span class="sxs-lookup"><span data-stu-id="350d1-155">Download hello file `guestbook-all-in-one.yaml` from [GitHub](https://github.com/kubernetes/kubernetes/tree/master/examples/guestbook/all-in-one).</span></span> 
2. <span data-ttu-id="350d1-156">Przeglądaj w poszukiwaniu hello `spec` dla hello `frontend` usługi.</span><span class="sxs-lookup"><span data-stu-id="350d1-156">Browse for hello `spec` for hello `frontend` service.</span></span>
3. <span data-ttu-id="350d1-157">Usuń komentarz linii hello `type: LoadBalancer`.</span><span class="sxs-lookup"><span data-stu-id="350d1-157">Uncomment hello line `type: LoadBalancer`.</span></span>

    ![Moduł równoważenia obciążenia w konfiguracji usługi](./media/container-service-kubernetes-load-balancing/guestbook-frontend-loadbalance.png)

4. <span data-ttu-id="350d1-159">Zapisz plik hello i wdrażanie aplikacji hello, uruchamiając następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="350d1-159">Save hello file, and deploy hello app by running hello following command:</span></span>

    ```
    kubectl create -f guestbook-all-in-one.yaml
    ```

5. <span data-ttu-id="350d1-160">Typ `kubectl get svc` toosee hello stan działania usług hello hello klastra.</span><span class="sxs-lookup"><span data-stu-id="350d1-160">Type `kubectl get svc` toosee hello state of hello services in hello cluster.</span></span> <span data-ttu-id="350d1-161">Podczas równoważenia obciążenia hello konfiguruje reguły hello, hello `EXTERNAL-IP` z hello `frontend` usługi pojawia się jako `<pending>`.</span><span class="sxs-lookup"><span data-stu-id="350d1-161">While hello load balancer configures hello rule, hello `EXTERNAL-IP` of hello `frontend` service appears as `<pending>`.</span></span> <span data-ttu-id="350d1-162">Po kilku minutach skonfigurowano hello zewnętrzny adres IP:</span><span class="sxs-lookup"><span data-stu-id="350d1-162">After a few minutes, hello external IP address is configured:</span></span> 

    ![Konfigurowanie usługi równoważenia obciążenia Azure](./media/container-service-kubernetes-load-balancing/guestbook-external-ip.png)

6. <span data-ttu-id="350d1-164">Upewnij się, że masz dostęp usługi hello na powitania zewnętrzny adres IP.</span><span class="sxs-lookup"><span data-stu-id="350d1-164">Verify that you can access hello service at hello external IP address.</span></span> <span data-ttu-id="350d1-165">Na przykład można otworzyć przeglądarki toohello zewnętrzny adres IP sieci web hello usługi.</span><span class="sxs-lookup"><span data-stu-id="350d1-165">For example, you can open a web browser toohello external IP address of hello service.</span></span>

    ![Zewnętrznie księgi gości dostępu](./media/container-service-kubernetes-load-balancing/guestbook-web.png)

    <span data-ttu-id="350d1-167">Można dodać wpisów księgi gości.</span><span class="sxs-lookup"><span data-stu-id="350d1-167">You can add guestbook entries.</span></span>

7. <span data-ttu-id="350d1-168">toosee hello konfiguracji równoważenia obciążenia Azure hello, wyszukaj zasobu usługi równoważenia obciążenia hello hello klastra w hello [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="350d1-168">toosee hello configuration of hello Azure load balancer, browse for hello load balancer resource for hello cluster in hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="350d1-169">Zobacz kroki hello w poprzednim przykładzie hello.</span><span class="sxs-lookup"><span data-stu-id="350d1-169">See hello steps in hello previous example.</span></span>

### <a name="considerations"></a><span data-ttu-id="350d1-170">Zagadnienia do rozważenia</span><span class="sxs-lookup"><span data-stu-id="350d1-170">Considerations</span></span>

* <span data-ttu-id="350d1-171">Tworzenie reguły modułu równoważenia obciążenia hello wykonywany asynchronicznie, i informacje o równoważenia hello udostępniane są publikowane w usłudze hello `status.loadBalancer` pola.</span><span class="sxs-lookup"><span data-stu-id="350d1-171">Creation of hello load balancer rule happens asynchronously, and information about hello provisioned balancer is published in hello service’s `status.loadBalancer` field.</span></span>
* <span data-ttu-id="350d1-172">Każda usługa zostanie automatycznie przypisany własną wirtualnego adresu IP w usłudze równoważenia obciążenia hello.</span><span class="sxs-lookup"><span data-stu-id="350d1-172">Every service is automatically assigned its own virtual IP address in hello load balancer.</span></span>
* <span data-ttu-id="350d1-173">Jeśli chcesz modułu równoważenia obciążenia hello tooreach na podstawie nazwy DNS, współpracować z Twojej domeny usługi dostawcy toocreate nazwy DNS dla adresu IP hello reguły.</span><span class="sxs-lookup"><span data-stu-id="350d1-173">If you want tooreach hello load balancer by a DNS name, work with your domain service provider toocreate a DNS name for hello rule's IP address.</span></span>

## <a name="http-or-https-traffic"></a><span data-ttu-id="350d1-174">Ruch HTTP lub HTTPS</span><span class="sxs-lookup"><span data-stu-id="350d1-174">HTTP or HTTPS traffic</span></span>

<span data-ttu-id="350d1-175">Saldo tooload HTTP lub HTTPS toocontainer ruch sieci web aplikacji i zarządzać certyfikatami dla transport layer security (TLS), możesz użyć hello Kubernetes [wejściowych](https://kubernetes.io/docs/user-guide/ingress/) zasobów.</span><span class="sxs-lookup"><span data-stu-id="350d1-175">tooload balance HTTP or HTTPS traffic toocontainer web apps and manage certificates for transport layer security (TLS), you can use hello Kubernetes [Ingress](https://kubernetes.io/docs/user-guide/ingress/) resource.</span></span> <span data-ttu-id="350d1-176">Transfer danych przychodzących jest zbiorem reguł zezwalających na połączenia przychodzące tooreach hello klastra usług.</span><span class="sxs-lookup"><span data-stu-id="350d1-176">An Ingress is a collection of rules that allow inbound connections tooreach hello cluster services.</span></span> <span data-ttu-id="350d1-177">Dla toowork zasobów wejściowych, hello Kubernetes klaster musi mieć [kontrolera wejściowych](https://kubernetes.io/docs/user-guide/ingress/#ingress-controllers) uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="350d1-177">For an Ingress resource toowork, hello Kubernetes cluster must have an [Ingress controller](https://kubernetes.io/docs/user-guide/ingress/#ingress-controllers) running.</span></span>

<span data-ttu-id="350d1-178">Usługa kontenera platformy Azure nie implementuje kontrolera wejściowych Kubernetes automatycznie.</span><span class="sxs-lookup"><span data-stu-id="350d1-178">Azure Container Service does not implement a Kubernetes Ingress controller automatically.</span></span> <span data-ttu-id="350d1-179">Dostępnych jest kilka implementacje kontrolera.</span><span class="sxs-lookup"><span data-stu-id="350d1-179">Several controller implementations are available.</span></span> <span data-ttu-id="350d1-180">Obecnie hello [kontrolera wejściowych Nginx](https://github.com/kubernetes/ingress/tree/master/examples/deployment/nginx) zaleca się tooconfigure transfer danych przychodzących reguł i równoważenie obciążenia ruchu HTTP i HTTPS.</span><span class="sxs-lookup"><span data-stu-id="350d1-180">Currently, hello [Nginx Ingress controller](https://github.com/kubernetes/ingress/tree/master/examples/deployment/nginx) is recommended tooconfigure Ingress rules and load balance HTTP and HTTPS traffic.</span></span> 

<span data-ttu-id="350d1-181">Aby uzyskać więcej informacji, zobacz hello [dokumentacji kontrolera wejściowych Nginx](https://github.com/kubernetes/ingress/tree/master/controllers/nginx/README.md).</span><span class="sxs-lookup"><span data-stu-id="350d1-181">For more information, see hello [Nginx Ingress controller documentation](https://github.com/kubernetes/ingress/tree/master/controllers/nginx/README.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="350d1-182">Korzystając z hello wejściowych Nginx kontrolera usługi kontenera platformy Azure, musi ujawniać hello wdrażania kontrolera usługi za pomocą `type: LoadBalancer`.</span><span class="sxs-lookup"><span data-stu-id="350d1-182">When using hello Nginx Ingress controller in Azure Container Service, you must expose hello controller deployment as a service with `type: LoadBalancer`.</span></span> <span data-ttu-id="350d1-183">Spowoduje to skonfigurowanie hello Azure obciążenia równoważenia tooroute ruchu toohello kontrolera.</span><span class="sxs-lookup"><span data-stu-id="350d1-183">This configures hello Azure load balancer tooroute traffic toohello controller.</span></span> <span data-ttu-id="350d1-184">Aby uzyskać więcej informacji zobacz hello w poprzedniej sekcji.</span><span class="sxs-lookup"><span data-stu-id="350d1-184">For more information, see hello previous section.</span></span>


## <a name="next-steps"></a><span data-ttu-id="350d1-185">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="350d1-185">Next steps</span></span>

* <span data-ttu-id="350d1-186">Zobacz hello [dokumentacji Kubernetes usługi równoważenia obciążenia](https://kubernetes.io/docs/user-guide/load-balancer/)</span><span class="sxs-lookup"><span data-stu-id="350d1-186">See hello [Kubernetes LoadBalancer documentation](https://kubernetes.io/docs/user-guide/load-balancer/)</span></span>
* <span data-ttu-id="350d1-187">Dowiedz się więcej o [kontrolerów Kubernetes przychodzące i wejściowych](https://kubernetes.io/docs/user-guide/ingress/)</span><span class="sxs-lookup"><span data-stu-id="350d1-187">Learn more about [Kubernetes Ingress and Ingress controllers](https://kubernetes.io/docs/user-guide/ingress/)</span></span>
* <span data-ttu-id="350d1-188">Zobacz [Kubernetes przykłady](https://github.com/kubernetes/kubernetes/tree/master/examples)</span><span class="sxs-lookup"><span data-stu-id="350d1-188">See [Kubernetes examples](https://github.com/kubernetes/kubernetes/tree/master/examples)</span></span>

