---
title: "Zarządzanie klastrem Azure DC/OS z interfejsu API REST platformy Marathon | Dokumentacja firmy Microsoft"
description: "Wdrażanie kontenerów do klastra usługi kontenera platformy Azure DC/OS przy użyciu interfejsu API REST platformy Marathon."
services: container-service
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Docker, kontenery, mikrousługi, Mesos, Azure"
ms.assetid: c7175446-4507-4a33-a7a2-63583e5996e3
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/04/2017
ms.author: danlep
ms.custom: mvc
ms.openlocfilehash: 65f8e0170fa7b89162e811a1d5dd58775fd20d7b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="dcos-container-management-through-the-marathon-rest-api"></a><span data-ttu-id="bcc29-104">Zarządzanie kontenerem DC/OS przy użyciu interfejsu API REST platformy Marathon</span><span class="sxs-lookup"><span data-stu-id="bcc29-104">DC/OS container management through the Marathon REST API</span></span>
<span data-ttu-id="bcc29-105">Platforma DC/OS dostarcza środowisko wdrażania i skalowania obciążeń klastrowanych, zapewniając jednocześnie abstrakcyjność sprzętu bazowego.</span><span class="sxs-lookup"><span data-stu-id="bcc29-105">DC/OS provides an environment for deploying and scaling clustered workloads, while abstracting the underlying hardware.</span></span> <span data-ttu-id="bcc29-106">Ponad systemem DC/OS istnieje platforma, która zarządza planowaniem i wykonywaniem obciążeń obliczeniowych.</span><span class="sxs-lookup"><span data-stu-id="bcc29-106">On top of DC/OS, there is a framework that manages scheduling and executing compute workloads.</span></span> <span data-ttu-id="bcc29-107">Platformy są dostępne dla wielu popularnych zadań, ten dokument stanowi wprowadzenie tworzenie i skalować wdrożenia kontenerów przy użyciu interfejsu API REST platformy Marathon.</span><span class="sxs-lookup"><span data-stu-id="bcc29-107">Although frameworks are available for many popular workloads, this document gets you started creating and scaling container deployments by using the Marathon REST API.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="bcc29-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="bcc29-108">Prerequisites</span></span>

<span data-ttu-id="bcc29-109">Przed przystąpieniem do pracy nad tymi przykładami będziesz potrzebować klastra DC/OS skonfigurowanego w usłudze kontenera platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="bcc29-109">Before working through these examples, you need a DC/OS cluster that is configured in Azure Container Service.</span></span> <span data-ttu-id="bcc29-110">Potrzebna będzie także zdalna łączność z tym klastrem.</span><span class="sxs-lookup"><span data-stu-id="bcc29-110">You also need to have remote connectivity to this cluster.</span></span> <span data-ttu-id="bcc29-111">Aby uzyskać więcej informacji na temat tych elementów, zobacz następujące artykuły:</span><span class="sxs-lookup"><span data-stu-id="bcc29-111">For more information on these items, see the following articles:</span></span>

* [<span data-ttu-id="bcc29-112">Wdrażanie klastra usługi Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="bcc29-112">Deploying an Azure Container Service cluster</span></span>](container-service-deployment.md)
* [<span data-ttu-id="bcc29-113">Łączenie z klastrem usługi Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="bcc29-113">Connecting to an Azure Container Service cluster</span></span>](../container-service-connect.md)

## <a name="access-the-dcos-apis"></a><span data-ttu-id="bcc29-114">Dostęp do interfejsów API platformy DC/OS</span><span class="sxs-lookup"><span data-stu-id="bcc29-114">Access the DC/OS APIs</span></span>
<span data-ttu-id="bcc29-115">Po nawiązaniu połączeniu z klastrem usługi kontenera platformy Azure masz dostęp do platformy DC/OS i powiązanych interfejsów API REST pod adresem http://localhost:local-port.</span><span class="sxs-lookup"><span data-stu-id="bcc29-115">After you are connected to the Azure Container Service cluster, you can access the DC/OS and related REST APIs through http://localhost:local-port.</span></span> <span data-ttu-id="bcc29-116">W przykładach przedstawionych w tym dokumencie założono, że tunelowanie korzysta z portu 80.</span><span class="sxs-lookup"><span data-stu-id="bcc29-116">The examples in this document assume that you are tunneling on port 80.</span></span> <span data-ttu-id="bcc29-117">Na przykład punkty końcowe platformy Marathon można połączyć się z na identyfikatory URI rozpoczynające się od `http://localhost/marathon/v2/`.</span><span class="sxs-lookup"><span data-stu-id="bcc29-117">For example, the Marathon endpoints can be reached at URIs beginning with `http://localhost/marathon/v2/`.</span></span> 

<span data-ttu-id="bcc29-118">Aby uzyskać więcej informacji o różnych interfejsach API, zobacz dokumentację Mesosphere dotyczącą [interfejsu API platformy Marathon](https://mesosphere.github.io/marathon/docs/rest-api.html) i [interfejsu API programu Chronos](https://mesos.github.io/chronos/docs/api.html) oraz dokumentację Apache dotyczącą [interfejsu API aplikacji Mesos Scheduler](http://mesos.apache.org/documentation/latest/scheduler-http-api/).</span><span class="sxs-lookup"><span data-stu-id="bcc29-118">For more information on the various APIs, see the Mesosphere documentation for the [Marathon API](https://mesosphere.github.io/marathon/docs/rest-api.html) and the [Chronos API](https://mesos.github.io/chronos/docs/api.html), and the Apache documentation for the [Mesos Scheduler API](http://mesos.apache.org/documentation/latest/scheduler-http-api/).</span></span>

## <a name="gather-information-from-dcos-and-marathon"></a><span data-ttu-id="bcc29-119">Gromadzenie informacji z platform DC/OS i Marathon</span><span class="sxs-lookup"><span data-stu-id="bcc29-119">Gather information from DC/OS and Marathon</span></span>
<span data-ttu-id="bcc29-120">Przed wdrożeniem kontenerów do klastra DC/OS Zbierz określone informacje o klastrze DC/OS, takie jak nazwy i stan agentów DC/OS.</span><span class="sxs-lookup"><span data-stu-id="bcc29-120">Before you deploy containers to the DC/OS cluster, gather some information about the DC/OS cluster, such as the names and status of the DC/OS agents.</span></span> <span data-ttu-id="bcc29-121">W tym celu wykonaj zapytanie w punkcie końcowym `master/slaves` interfejsu API REST platformy DC/OS.</span><span class="sxs-lookup"><span data-stu-id="bcc29-121">To do so, query the `master/slaves` endpoint of the DC/OS REST API.</span></span> <span data-ttu-id="bcc29-122">Jeśli operacja zostanie wykonana pomyślnie, zapytanie zwróci listę agentów DC/OS i szereg właściwości każdego z nich.</span><span class="sxs-lookup"><span data-stu-id="bcc29-122">If everything goes well, the query returns a list of DC/OS agents and several properties for each.</span></span>

```bash
curl http://localhost/mesos/master/slaves
```

<span data-ttu-id="bcc29-123">Teraz użyj punktu końcowego `/apps` platformy Marathon, aby sprawdzić bieżące wdrożenia aplikacji w klastrze DC/OS.</span><span class="sxs-lookup"><span data-stu-id="bcc29-123">Now, use the Marathon `/apps` endpoint to check for current application deployments to the DC/OS cluster.</span></span> <span data-ttu-id="bcc29-124">Jeśli jest to nowy klaster, pojawi się pusta tablica aplikacji.</span><span class="sxs-lookup"><span data-stu-id="bcc29-124">If this is a new cluster, you see an empty array for apps.</span></span>

```bash
curl localhost/marathon/v2/apps

{"apps":[]}
```

## <a name="deploy-a-docker-formatted-container"></a><span data-ttu-id="bcc29-125">Wdrażanie kontenera w formacie programu Docker</span><span class="sxs-lookup"><span data-stu-id="bcc29-125">Deploy a Docker-formatted container</span></span>
<span data-ttu-id="bcc29-126">Kontenery w formacie Docker za pośrednictwem interfejsu API REST platformy Marathon można wdrożyć przy użyciu pliku JSON, który opisuje zamierzone wdrożenie.</span><span class="sxs-lookup"><span data-stu-id="bcc29-126">You deploy Docker-formatted containers through the Marathon REST API by using a JSON file that describes the intended deployment.</span></span> <span data-ttu-id="bcc29-127">Poniższy przykład wdraża kontener Nginx prywatny agenta w klastrze.</span><span class="sxs-lookup"><span data-stu-id="bcc29-127">The following sample deploys an Nginx container to a private agent in the cluster.</span></span> 

```json
{
  "id": "nginx",
  "cpus": 0.1,
  "mem": 32.0,
  "instances": 1,
  "container": {
    "type": "DOCKER",
    "docker": {
      "image": "nginx",
      "network": "BRIDGE",
      "portMappings": [
        { "containerPort": 80, "servicePort": 9000, "protocol": "tcp" }
      ]
    }
  }
}
```

<span data-ttu-id="bcc29-128">Do wdrożenia kontenera formacie programu Docker, przechowuj plik JSON w dostępnej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="bcc29-128">To deploy a Docker-formatted container, store the JSON file in an accessible location.</span></span> <span data-ttu-id="bcc29-129">Następnie w celu wdrożenia kontenera uruchom następujące polecenie.</span><span class="sxs-lookup"><span data-stu-id="bcc29-129">Next, to deploy the container, run the following command.</span></span> <span data-ttu-id="bcc29-130">Określ nazwę pliku JSON (`marathon.json` w tym przykładzie).</span><span class="sxs-lookup"><span data-stu-id="bcc29-130">Specify the name of the JSON file (`marathon.json` in this example).</span></span>

```bash
curl -X POST http://localhost/marathon/v2/apps -d @marathon.json -H "Content-type: application/json"
```

<span data-ttu-id="bcc29-131">Dane wyjściowe będą podobne do następujących:</span><span class="sxs-lookup"><span data-stu-id="bcc29-131">The output is similar to the following:</span></span>

```json
{"version":"2015-11-20T18:59:00.494Z","deploymentId":"b12f8a73-f56a-4eb1-9375-4ac026d6cdec"}
```

<span data-ttu-id="bcc29-132">Teraz po wykonaniu zapytania dotyczącego aplikacji na platformie Marathon nowa aplikacja pojawi się w danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="bcc29-132">Now, if you query Marathon for applications, this new application appears in the output.</span></span>

```bash
curl localhost/marathon/v2/apps
```

## <a name="reach-the-container"></a><span data-ttu-id="bcc29-133">Osiągnąć kontenera</span><span class="sxs-lookup"><span data-stu-id="bcc29-133">Reach the container</span></span>

<span data-ttu-id="bcc29-134">Aby sprawdzić, czy Nginx działa w kontenerze w jednej z prywatnych agentów w klastrze.</span><span class="sxs-lookup"><span data-stu-id="bcc29-134">You can verify that the Nginx is running in a container on one of the private agents in the cluster.</span></span> <span data-ttu-id="bcc29-135">Aby znaleźć hosta i portu, na którym jest uruchomiona kontenera, zapytanie Marathon uruchomione zadania:</span><span class="sxs-lookup"><span data-stu-id="bcc29-135">To find the host and port where the container is running, query Marathon for the running tasks:</span></span> 

```bash
curl localhost/marathon/v2/tasks
```

<span data-ttu-id="bcc29-136">Znajdź wartość `host` w danych wyjściowych (podobnie jak adres IP `10.32.0.x`), a wartością `ports`.</span><span class="sxs-lookup"><span data-stu-id="bcc29-136">Find the value of `host` in the output (an IP address similar to `10.32.0.x`), and the value of `ports`.</span></span>


<span data-ttu-id="bcc29-137">Teraz należy terminali połączenia SSH (nie połączeń tunelowych) do zarządzania nazwy FQDN klastra.</span><span class="sxs-lookup"><span data-stu-id="bcc29-137">Now make an SSH terminal connection (not a tunneled connection) to the management FQDN of the cluster.</span></span> <span data-ttu-id="bcc29-138">Po nawiązaniu połączenia, wprowadź następujące żądania, zastępując poprawne wartości `host` i `ports`:</span><span class="sxs-lookup"><span data-stu-id="bcc29-138">Once connected, make the following request, substituting the correct values of `host` and `ports`:</span></span>

```bash
curl http://host:ports
```

<span data-ttu-id="bcc29-139">Dane wyjściowe server Nginx jest podobny do następującego:</span><span class="sxs-lookup"><span data-stu-id="bcc29-139">The Nginx server output is similar to the following:</span></span>

![Nginx z kontenera](./media/container-service-mesos-marathon-rest/nginx.png)




## <a name="scale-your-containers"></a><span data-ttu-id="bcc29-141">Skalowanie kontenerów</span><span class="sxs-lookup"><span data-stu-id="bcc29-141">Scale your containers</span></span>
<span data-ttu-id="bcc29-142">Interfejsu API platformy Marathon umożliwia skalowanie w poziomie oraz skalowanie w przypadku wdrożeń aplikacji.</span><span class="sxs-lookup"><span data-stu-id="bcc29-142">You can use the Marathon API to scale out or scale in application deployments.</span></span> <span data-ttu-id="bcc29-143">W poprzednim przykładzie wdrożono jedno wystąpienie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="bcc29-143">In the previous example, you deployed one instance of an application.</span></span> <span data-ttu-id="bcc29-144">Wykonamy teraz skalowanie w poziomie, aby uzyskać trzy wystąpienia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="bcc29-144">Let's scale this out to three instances of an application.</span></span> <span data-ttu-id="bcc29-145">W tym celu utwórz plik JSON zawierający następujący tekst JSON i zapisz go w dostępnej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="bcc29-145">To do so, create a JSON file by using the following JSON text, and store it in an accessible location.</span></span>

```json
{ "instances": 3 }
```

<span data-ttu-id="bcc29-146">Z tunelowane połączenie uruchom następujące polecenie, aby skalować aplikację w poziomie.</span><span class="sxs-lookup"><span data-stu-id="bcc29-146">From your tunneled connection, run the following command to scale out the application.</span></span>

> [!NOTE]
> <span data-ttu-id="bcc29-147">Identyfikator URI będzie mieć postać http://localhost/marathon/v2/apps/ z dołączonym identyfikatorem aplikacji do skalowania.</span><span class="sxs-lookup"><span data-stu-id="bcc29-147">The URI is http://localhost/marathon/v2/apps/ followed by the ID of the application to scale.</span></span> <span data-ttu-id="bcc29-148">W przypadku użycia przedstawionej tutaj przykładowej aplikacji Nginx identyfikator URI będzie mieć postać http://localhost/marathon/v2/apps/nginx.</span><span class="sxs-lookup"><span data-stu-id="bcc29-148">If you are using the Nginx sample that is provided here, the URI would be http://localhost/marathon/v2/apps/nginx.</span></span>
> 
> 

```bash
curl http://localhost/marathon/v2/apps/nginx -H "Content-type: application/json" -X PUT -d @scale.json
```

<span data-ttu-id="bcc29-149">Na koniec wykonaj zapytanie dotyczące aplikacji w punkcie końcowym platformy Marathon.</span><span class="sxs-lookup"><span data-stu-id="bcc29-149">Finally, query the Marathon endpoint for applications.</span></span> <span data-ttu-id="bcc29-150">Widoczne będą trzy kontenery Nginx.</span><span class="sxs-lookup"><span data-stu-id="bcc29-150">You see that there are now three Nginx containers.</span></span>

```bash
curl localhost/marathon/v2/apps
```

## <a name="equivalent-powershell-commands"></a><span data-ttu-id="bcc29-151">Równoważne polecenia programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="bcc29-151">Equivalent PowerShell commands</span></span>
<span data-ttu-id="bcc29-152">Te same akcje można wykonać za pomocą poleceń programu PowerShell w systemie Windows.</span><span class="sxs-lookup"><span data-stu-id="bcc29-152">You can perform these same actions by using PowerShell commands on a Windows system.</span></span>

<span data-ttu-id="bcc29-153">Aby zebrać informacje dotyczące klastra DC/OS, takie jak nazwy i stan agenta, uruchom następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="bcc29-153">To gather information about the DC/OS cluster, such as agent names and agent status, run the following command:</span></span>

```powershell
Invoke-WebRequest -Uri http://localhost/mesos/master/slaves
```

<span data-ttu-id="bcc29-154">Kontenery w formacie programu Docker można wdrażać za pośrednictwem platformy Marathon przy użyciu pliku JSON, który opisuje zamierzone wdrożenie.</span><span class="sxs-lookup"><span data-stu-id="bcc29-154">You deploy Docker-formatted containers through Marathon by using a JSON file that describes the intended deployment.</span></span> <span data-ttu-id="bcc29-155">W poniższym przykładzie wdrożono kontener Nginx, który powiąże port 80 agenta DC/OS z portem 80 kontenera.</span><span class="sxs-lookup"><span data-stu-id="bcc29-155">The following sample deploys the Nginx container, binding port 80 of the DC/OS agent to port 80 of the container.</span></span>

```json
{
  "id": "nginx",
  "cpus": 0.1,
  "mem": 32.0,
  "instances": 1,
  "container": {
    "type": "DOCKER",
    "docker": {
      "image": "nginx",
      "network": "BRIDGE",
      "portMappings": [
        { "containerPort": 80, "servicePort": 9000, "protocol": "tcp" }
      ]
    }
  }
}
```

<span data-ttu-id="bcc29-156">Do wdrożenia kontenera formacie programu Docker, przechowuj plik JSON w dostępnej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="bcc29-156">To deploy a Docker-formatted container, store the JSON file in an accessible location.</span></span> <span data-ttu-id="bcc29-157">Następnie w celu wdrożenia kontenera uruchom następujące polecenie.</span><span class="sxs-lookup"><span data-stu-id="bcc29-157">Next, to deploy the container, run the following command.</span></span> <span data-ttu-id="bcc29-158">Określ ścieżkę do pliku JSON (`marathon.json` w tym przykładzie).</span><span class="sxs-lookup"><span data-stu-id="bcc29-158">Specify the path to the JSON file (`marathon.json` in this example).</span></span>

```powershell
Invoke-WebRequest -Method Post -Uri http://localhost/marathon/v2/apps -ContentType application/json -InFile 'c:\marathon.json'
```

<span data-ttu-id="bcc29-159">Interfejs API platformy Marathon umożliwia także skalowanie w poziomie oraz skalowanie na zewnątrz wdrożeń aplikacji.</span><span class="sxs-lookup"><span data-stu-id="bcc29-159">You can also use the Marathon API to scale out or scale in application deployments.</span></span> <span data-ttu-id="bcc29-160">W poprzednim przykładzie wdrożono jedno wystąpienie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="bcc29-160">In the previous example, you deployed one instance of an application.</span></span> <span data-ttu-id="bcc29-161">Wykonamy teraz skalowanie w poziomie, aby uzyskać trzy wystąpienia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="bcc29-161">Let's scale this out to three instances of an application.</span></span> <span data-ttu-id="bcc29-162">W tym celu utwórz plik JSON zawierający następujący tekst JSON i zapisz go w dostępnej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="bcc29-162">To do so, create a JSON file by using the following JSON text, and store it in an accessible location.</span></span>

```json
{ "instances": 3 }
```

<span data-ttu-id="bcc29-163">Uruchom następujące polecenie, aby skalować aplikację w poziomie:</span><span class="sxs-lookup"><span data-stu-id="bcc29-163">Run the following command to scale out the application:</span></span>

> [!NOTE]
> <span data-ttu-id="bcc29-164">Identyfikator URI będzie mieć postać http://localhost/marathon/v2/apps/ z dołączonym identyfikatorem aplikacji do skalowania.</span><span class="sxs-lookup"><span data-stu-id="bcc29-164">The URI is http://localhost/marathon/v2/apps/ followed by the ID of the application to scale.</span></span> <span data-ttu-id="bcc29-165">W przypadku użycia przedstawionej tutaj przykładowej aplikacji Nginx, identyfikator URI będzie mieć postać http://localhost/marathon/v2/apps/nginx.</span><span class="sxs-lookup"><span data-stu-id="bcc29-165">If you are using the Nginx sample provided here, the URI would be http://localhost/marathon/v2/apps/nginx.</span></span>
> 
> 

```powershell
Invoke-WebRequest -Method Put -Uri http://localhost/marathon/v2/apps/nginx -ContentType application/json -InFile 'c:\scale.json'
```

## <a name="next-steps"></a><span data-ttu-id="bcc29-166">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="bcc29-166">Next steps</span></span>
* [<span data-ttu-id="bcc29-167">Więcej informacji na temat punktów końcowych HTTP platformy Mesos</span><span class="sxs-lookup"><span data-stu-id="bcc29-167">Read more about the Mesos HTTP endpoints</span></span>](http://mesos.apache.org/documentation/latest/endpoints/)
* [<span data-ttu-id="bcc29-168">Więcej informacji na temat interfejsu API REST platformy Marathon</span><span class="sxs-lookup"><span data-stu-id="bcc29-168">Read more about the Marathon REST API</span></span>](https://mesosphere.github.io/marathon/docs/rest-api.html)

