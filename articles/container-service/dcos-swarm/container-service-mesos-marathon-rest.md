---
title: aaaManage Azure DC/OS klaster z interfejsu API REST platformy Marathon | Dokumentacja firmy Microsoft
description: "Wdrażanie klastra usługi kontenera platformy Azure DC/OS tooan kontenerów przy użyciu hello interfejsu API REST platformy Marathon."
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
ms.openlocfilehash: d926b9b90f5d4eda85a015d9ea0d96fea2c4b566
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="dcos-container-management-through-hello-marathon-rest-api"></a><span data-ttu-id="98383-104">Zarządzanie kontenerem DC/OS przy użyciu hello interfejsu API REST platformy Marathon</span><span class="sxs-lookup"><span data-stu-id="98383-104">DC/OS container management through hello Marathon REST API</span></span>
<span data-ttu-id="98383-105">DC/OS udostępnia środowisko wdrażania i skalowania obciążeń klastrowanych, zapewniając jednocześnie abstrakcyjność sprzętu źródłowego hello.</span><span class="sxs-lookup"><span data-stu-id="98383-105">DC/OS provides an environment for deploying and scaling clustered workloads, while abstracting hello underlying hardware.</span></span> <span data-ttu-id="98383-106">Ponad systemem DC/OS istnieje platforma, która zarządza planowaniem i wykonywaniem obciążeń obliczeniowych.</span><span class="sxs-lookup"><span data-stu-id="98383-106">On top of DC/OS, there is a framework that manages scheduling and executing compute workloads.</span></span> <span data-ttu-id="98383-107">Platformy są dostępne dla wielu popularnych zadań, ten dokument stanowi wprowadzenie tworzenia i skalowania wdrożenia kontenerów przy użyciu hello interfejsu API REST platformy Marathon.</span><span class="sxs-lookup"><span data-stu-id="98383-107">Although frameworks are available for many popular workloads, this document gets you started creating and scaling container deployments by using hello Marathon REST API.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="98383-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="98383-108">Prerequisites</span></span>

<span data-ttu-id="98383-109">Przed przystąpieniem do pracy nad tymi przykładami będziesz potrzebować klastra DC/OS skonfigurowanego w usłudze kontenera platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="98383-109">Before working through these examples, you need a DC/OS cluster that is configured in Azure Container Service.</span></span> <span data-ttu-id="98383-110">Należy również toohave łączności zdalnej toothis klastra.</span><span class="sxs-lookup"><span data-stu-id="98383-110">You also need toohave remote connectivity toothis cluster.</span></span> <span data-ttu-id="98383-111">Aby uzyskać więcej informacji na temat tych elementów zobacz następujące artykuły hello:</span><span class="sxs-lookup"><span data-stu-id="98383-111">For more information on these items, see hello following articles:</span></span>

* [<span data-ttu-id="98383-112">Wdrażanie klastra usługi Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="98383-112">Deploying an Azure Container Service cluster</span></span>](container-service-deployment.md)
* [<span data-ttu-id="98383-113">Łączenie tooan klastra usługi kontenera platformy Azure</span><span class="sxs-lookup"><span data-stu-id="98383-113">Connecting tooan Azure Container Service cluster</span></span>](../container-service-connect.md)

## <a name="access-hello-dcos-apis"></a><span data-ttu-id="98383-114">Witaj dostępu do interfejsów API DC/OS</span><span class="sxs-lookup"><span data-stu-id="98383-114">Access hello DC/OS APIs</span></span>
<span data-ttu-id="98383-115">Po są połączone toohello klastra usługi kontenera platformy Azure, możesz uzyskać dostęp do hello DC/OS i powiązanych interfejsów API REST, za pośrednictwem portu http://localhost:local.</span><span class="sxs-lookup"><span data-stu-id="98383-115">After you are connected toohello Azure Container Service cluster, you can access hello DC/OS and related REST APIs through http://localhost:local-port.</span></span> <span data-ttu-id="98383-116">Przykłady Hello w tym dokumencie założono, że tunelowanie korzysta na porcie 80.</span><span class="sxs-lookup"><span data-stu-id="98383-116">hello examples in this document assume that you are tunneling on port 80.</span></span> <span data-ttu-id="98383-117">Na przykład punkty końcowe platformy Marathon hello jest osiągalna na identyfikatory URI rozpoczynające się od `http://localhost/marathon/v2/`.</span><span class="sxs-lookup"><span data-stu-id="98383-117">For example, hello Marathon endpoints can be reached at URIs beginning with `http://localhost/marathon/v2/`.</span></span> 

<span data-ttu-id="98383-118">Aby uzyskać więcej informacji na temat hello różnych interfejsów API, zobacz hello dokumentację Mesosphere dotyczącą hello [interfejsu API platformy Marathon](https://mesosphere.github.io/marathon/docs/rest-api.html) i [Chronos interfejsu API](https://mesos.github.io/chronos/docs/api.html)oraz dokumentację Apache dotyczącą hello [Mesos API harmonogramu ](http://mesos.apache.org/documentation/latest/scheduler-http-api/).</span><span class="sxs-lookup"><span data-stu-id="98383-118">For more information on hello various APIs, see hello Mesosphere documentation for hello [Marathon API](https://mesosphere.github.io/marathon/docs/rest-api.html) and the [Chronos API](https://mesos.github.io/chronos/docs/api.html), and the Apache documentation for hello [Mesos Scheduler API](http://mesos.apache.org/documentation/latest/scheduler-http-api/).</span></span>

## <a name="gather-information-from-dcos-and-marathon"></a><span data-ttu-id="98383-119">Gromadzenie informacji z platform DC/OS i Marathon</span><span class="sxs-lookup"><span data-stu-id="98383-119">Gather information from DC/OS and Marathon</span></span>
<span data-ttu-id="98383-120">Przed wdrożeniem klastra DC/OS toohello kontenery Zbierz określone informacje o klastrze DC/OS hello, takich jak nazwy hello i stan agentów DC/OS hello.</span><span class="sxs-lookup"><span data-stu-id="98383-120">Before you deploy containers toohello DC/OS cluster, gather some information about hello DC/OS cluster, such as hello names and status of hello DC/OS agents.</span></span> <span data-ttu-id="98383-121">toodo zapytanie tak, hello `master/slaves` punkt końcowy hello interfejsu API REST platformy DC/OS.</span><span class="sxs-lookup"><span data-stu-id="98383-121">toodo so, query hello `master/slaves` endpoint of hello DC/OS REST API.</span></span> <span data-ttu-id="98383-122">Jeśli wszystko odbędzie się poprawnie, hello zapytanie zwraca listę agentów DC/OS i szereg właściwości każdego.</span><span class="sxs-lookup"><span data-stu-id="98383-122">If everything goes well, hello query returns a list of DC/OS agents and several properties for each.</span></span>

```bash
curl http://localhost/mesos/master/slaves
```

<span data-ttu-id="98383-123">Teraz, przy użyciu platformy Marathon hello `/apps` toocheck punktu końcowego dla bieżącego klastra DC/OS toohello wdrożeń aplikacji.</span><span class="sxs-lookup"><span data-stu-id="98383-123">Now, use hello Marathon `/apps` endpoint toocheck for current application deployments toohello DC/OS cluster.</span></span> <span data-ttu-id="98383-124">Jeśli jest to nowy klaster, pojawi się pusta tablica aplikacji.</span><span class="sxs-lookup"><span data-stu-id="98383-124">If this is a new cluster, you see an empty array for apps.</span></span>

```bash
curl localhost/marathon/v2/apps

{"apps":[]}
```

## <a name="deploy-a-docker-formatted-container"></a><span data-ttu-id="98383-125">Wdrażanie kontenera w formacie programu Docker</span><span class="sxs-lookup"><span data-stu-id="98383-125">Deploy a Docker-formatted container</span></span>
<span data-ttu-id="98383-126">Kontenery w formacie Docker za pośrednictwem interfejsu API REST platformy Marathon hello wdrażania przy użyciu pliku JSON, który opisuje hello zamierzone wdrożenie.</span><span class="sxs-lookup"><span data-stu-id="98383-126">You deploy Docker-formatted containers through hello Marathon REST API by using a JSON file that describes hello intended deployment.</span></span> <span data-ttu-id="98383-127">Witaj poniższego przykładu wdraża Nginx kontenera tooa prywatny agenta hello klastra.</span><span class="sxs-lookup"><span data-stu-id="98383-127">hello following sample deploys an Nginx container tooa private agent in hello cluster.</span></span> 

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

<span data-ttu-id="98383-128">toodeploy formacie programu Docker kontenerze, przechowywania pliku JSON hello w dostępnej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="98383-128">toodeploy a Docker-formatted container, store hello JSON file in an accessible location.</span></span> <span data-ttu-id="98383-129">Następnie toodeploy hello kontener, uruchom następujące polecenie hello.</span><span class="sxs-lookup"><span data-stu-id="98383-129">Next, toodeploy hello container, run hello following command.</span></span> <span data-ttu-id="98383-130">Określ nazwę pliku JSON hello hello (`marathon.json` w tym przykładzie).</span><span class="sxs-lookup"><span data-stu-id="98383-130">Specify hello name of hello JSON file (`marathon.json` in this example).</span></span>

```bash
curl -X POST http://localhost/marathon/v2/apps -d @marathon.json -H "Content-type: application/json"
```

<span data-ttu-id="98383-131">dane wyjściowe Hello są podobne toohello następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="98383-131">hello output is similar toohello following:</span></span>

```json
{"version":"2015-11-20T18:59:00.494Z","deploymentId":"b12f8a73-f56a-4eb1-9375-4ac026d6cdec"}
```

<span data-ttu-id="98383-132">Teraz po wykonaniu zapytania Marathon dla aplikacji, ta nowa aplikacja pojawi się w danych wyjściowych hello.</span><span class="sxs-lookup"><span data-stu-id="98383-132">Now, if you query Marathon for applications, this new application appears in hello output.</span></span>

```bash
curl localhost/marathon/v2/apps
```

## <a name="reach-hello-container"></a><span data-ttu-id="98383-133">Osiągnąć hello kontenera</span><span class="sxs-lookup"><span data-stu-id="98383-133">Reach hello container</span></span>

<span data-ttu-id="98383-134">Możesz zweryfikować tego hello Nginx jest uruchomione w kontenerze na jednym z agentów prywatnej hello w klastrze hello.</span><span class="sxs-lookup"><span data-stu-id="98383-134">You can verify that hello Nginx is running in a container on one of hello private agents in hello cluster.</span></span> <span data-ttu-id="98383-135">toofind hello hosta i portu, w którym jest uruchomiona kontenera hello, kwerendy Marathon hello uruchomionych zadań:</span><span class="sxs-lookup"><span data-stu-id="98383-135">toofind hello host and port where hello container is running, query Marathon for hello running tasks:</span></span> 

```bash
curl localhost/marathon/v2/tasks
```

<span data-ttu-id="98383-136">Znajdź wartość hello `host` w danych wyjściowych hello (adresów IP podobny zbyt`10.32.0.x`) i wartość hello `ports`.</span><span class="sxs-lookup"><span data-stu-id="98383-136">Find hello value of `host` in hello output (an IP address similar too`10.32.0.x`), and hello value of `ports`.</span></span>


<span data-ttu-id="98383-137">Teraz należy SSH terminali (nie połączeń tunelowych) toohello zarządzania połączeniami nazwy FQDN klastra hello.</span><span class="sxs-lookup"><span data-stu-id="98383-137">Now make an SSH terminal connection (not a tunneled connection) toohello management FQDN of hello cluster.</span></span> <span data-ttu-id="98383-138">Po nawiązaniu połączenia należy hello następujące żądania, zastępując wartości poprawne hello `host` i `ports`:</span><span class="sxs-lookup"><span data-stu-id="98383-138">Once connected, make hello following request, substituting hello correct values of `host` and `ports`:</span></span>

```bash
curl http://host:ports
```

<span data-ttu-id="98383-139">Hello dane wyjściowe server Nginx jest podobne toohello następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="98383-139">hello Nginx server output is similar toohello following:</span></span>

![Nginx z kontenera](./media/container-service-mesos-marathon-rest/nginx.png)




## <a name="scale-your-containers"></a><span data-ttu-id="98383-141">Skalowanie kontenerów</span><span class="sxs-lookup"><span data-stu-id="98383-141">Scale your containers</span></span>
<span data-ttu-id="98383-142">W przypadku wdrożeń aplikacji, można użyć tooscale interfejsu API platformy Marathon hello out lub skali.</span><span class="sxs-lookup"><span data-stu-id="98383-142">You can use hello Marathon API tooscale out or scale in application deployments.</span></span> <span data-ttu-id="98383-143">W poprzednim przykładzie hello wdrożono jedno wystąpienie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="98383-143">In hello previous example, you deployed one instance of an application.</span></span> <span data-ttu-id="98383-144">Przeprowadź skalowanie tę możliwość toothree wystąpienia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="98383-144">Let's scale this out toothree instances of an application.</span></span> <span data-ttu-id="98383-145">toodo tak, Utwórz plik JSON przy użyciu powitania po tekst JSON i zapisze go w dostępnej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="98383-145">toodo so, create a JSON file by using hello following JSON text, and store it in an accessible location.</span></span>

```json
{ "instances": 3 }
```

<span data-ttu-id="98383-146">Z połączeniem tunelowane Uruchom hello następujące polecenia tooscale limit aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="98383-146">From your tunneled connection, run hello following command tooscale out hello application.</span></span>

> [!NOTE]
> <span data-ttu-id="98383-147">Witaj identyfikatora URI jest http://localhost/marathon/v2/apps/ następuje identyfikator hello tooscale aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="98383-147">hello URI is http://localhost/marathon/v2/apps/ followed by hello ID of hello application tooscale.</span></span> <span data-ttu-id="98383-148">Jeśli używasz hello przykład Nginx, który znajduje się w tym miejscu, hello identyfikator URI będzie http://localhost/marathon/v2/apps/nginx.</span><span class="sxs-lookup"><span data-stu-id="98383-148">If you are using hello Nginx sample that is provided here, hello URI would be http://localhost/marathon/v2/apps/nginx.</span></span>
> 
> 

```bash
curl http://localhost/marathon/v2/apps/nginx -H "Content-type: application/json" -X PUT -d @scale.json
```

<span data-ttu-id="98383-149">Na koniec wykonaj zapytanie hello punktu końcowego platformy Marathon dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="98383-149">Finally, query hello Marathon endpoint for applications.</span></span> <span data-ttu-id="98383-150">Widoczne będą trzy kontenery Nginx.</span><span class="sxs-lookup"><span data-stu-id="98383-150">You see that there are now three Nginx containers.</span></span>

```bash
curl localhost/marathon/v2/apps
```

## <a name="equivalent-powershell-commands"></a><span data-ttu-id="98383-151">Równoważne polecenia programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="98383-151">Equivalent PowerShell commands</span></span>
<span data-ttu-id="98383-152">Te same akcje można wykonać za pomocą poleceń programu PowerShell w systemie Windows.</span><span class="sxs-lookup"><span data-stu-id="98383-152">You can perform these same actions by using PowerShell commands on a Windows system.</span></span>

<span data-ttu-id="98383-153">toogather informacje o klastrze DC/OS hello, takich jak nazwy i stan agenta, uruchom następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="98383-153">toogather information about hello DC/OS cluster, such as agent names and agent status, run hello following command:</span></span>

```powershell
Invoke-WebRequest -Uri http://localhost/mesos/master/slaves
```

<span data-ttu-id="98383-154">Kontenery w formacie Docker za pośrednictwem platformy Marathon wdrażania przy użyciu pliku JSON, który opisuje hello zamierzone wdrożenie.</span><span class="sxs-lookup"><span data-stu-id="98383-154">You deploy Docker-formatted containers through Marathon by using a JSON file that describes hello intended deployment.</span></span> <span data-ttu-id="98383-155">Witaj następującym przykładowym wdraża hello kontener Nginx, powiązania z portem 80 tooport agenta DC/OS hello 80 kontenera hello.</span><span class="sxs-lookup"><span data-stu-id="98383-155">hello following sample deploys hello Nginx container, binding port 80 of hello DC/OS agent tooport 80 of hello container.</span></span>

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

<span data-ttu-id="98383-156">toodeploy formacie programu Docker kontenerze, przechowywania pliku JSON hello w dostępnej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="98383-156">toodeploy a Docker-formatted container, store hello JSON file in an accessible location.</span></span> <span data-ttu-id="98383-157">Następnie toodeploy hello kontener, uruchom następujące polecenie hello.</span><span class="sxs-lookup"><span data-stu-id="98383-157">Next, toodeploy hello container, run hello following command.</span></span> <span data-ttu-id="98383-158">Określ plik JSON toohello ścieżka hello (`marathon.json` w tym przykładzie).</span><span class="sxs-lookup"><span data-stu-id="98383-158">Specify hello path toohello JSON file (`marathon.json` in this example).</span></span>

```powershell
Invoke-WebRequest -Method Post -Uri http://localhost/marathon/v2/apps -ContentType application/json -InFile 'c:\marathon.json'
```

<span data-ttu-id="98383-159">W przypadku wdrożeń aplikacji, można użyć tooscale interfejsu API platformy Marathon hello out lub skali.</span><span class="sxs-lookup"><span data-stu-id="98383-159">You can also use hello Marathon API tooscale out or scale in application deployments.</span></span> <span data-ttu-id="98383-160">W poprzednim przykładzie hello wdrożono jedno wystąpienie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="98383-160">In hello previous example, you deployed one instance of an application.</span></span> <span data-ttu-id="98383-161">Przeprowadź skalowanie tę możliwość toothree wystąpienia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="98383-161">Let's scale this out toothree instances of an application.</span></span> <span data-ttu-id="98383-162">toodo tak, Utwórz plik JSON przy użyciu powitania po tekst JSON i zapisze go w dostępnej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="98383-162">toodo so, create a JSON file by using hello following JSON text, and store it in an accessible location.</span></span>

```json
{ "instances": 3 }
```

<span data-ttu-id="98383-163">Witaj uruchom następujące polecenie tooscale limit aplikacji hello:</span><span class="sxs-lookup"><span data-stu-id="98383-163">Run hello following command tooscale out hello application:</span></span>

> [!NOTE]
> <span data-ttu-id="98383-164">Witaj identyfikatora URI jest http://localhost/marathon/v2/apps/ następuje identyfikator hello tooscale aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="98383-164">hello URI is http://localhost/marathon/v2/apps/ followed by hello ID of hello application tooscale.</span></span> <span data-ttu-id="98383-165">Jeśli używasz hello Nginx przykładu dostępnego w tym miejscu, hello identyfikator URI będzie http://localhost/marathon/v2/apps/nginx.</span><span class="sxs-lookup"><span data-stu-id="98383-165">If you are using hello Nginx sample provided here, hello URI would be http://localhost/marathon/v2/apps/nginx.</span></span>
> 
> 

```powershell
Invoke-WebRequest -Method Put -Uri http://localhost/marathon/v2/apps/nginx -ContentType application/json -InFile 'c:\scale.json'
```

## <a name="next-steps"></a><span data-ttu-id="98383-166">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="98383-166">Next steps</span></span>
* [<span data-ttu-id="98383-167">Więcej informacji na temat punktów końcowych HTTP platformy Mesos hello</span><span class="sxs-lookup"><span data-stu-id="98383-167">Read more about hello Mesos HTTP endpoints</span></span>](http://mesos.apache.org/documentation/latest/endpoints/)
* [<span data-ttu-id="98383-168">Więcej informacji na temat hello interfejsu API REST platformy Marathon</span><span class="sxs-lookup"><span data-stu-id="98383-168">Read more about hello Marathon REST API</span></span>](https://mesosphere.github.io/marathon/docs/rest-api.html)

