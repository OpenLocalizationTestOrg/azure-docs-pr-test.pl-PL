---
title: "aaaManage Azure DC/OS klastra przy użyciu interfejsu użytkownika platformy Marathon | Dokumentacja firmy Microsoft"
description: "Wdrażanie usługi klastra usługi kontenera platformy Azure tooan kontenerów przy użyciu hello interfejsu użytkownika sieci web Marathon."
services: container-service
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Docker, kontenery, mikrousługi, Mesos, Azure"
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/04/2017
ms.author: danlep
ms.custom: mvc
ms.openlocfilehash: a90180e1b4763e6d2ddfa699ed4b7269f209f728
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-an-azure-container-service-dcos-cluster-through-hello-marathon-web-ui"></a><span data-ttu-id="f6583-104">Zarządzanie klastrem usługi kontenera platformy Azure DC/OS za pośrednictwem sieci web Marathon hello interfejsu użytkownika</span><span class="sxs-lookup"><span data-stu-id="f6583-104">Manage an Azure Container Service DC/OS cluster through hello Marathon web UI</span></span>
<span data-ttu-id="f6583-105">DC/OS udostępnia środowisko wdrażania i skalowania obciążeń klastrowanych, zapewniając jednocześnie abstrakcyjność sprzętu źródłowego hello.</span><span class="sxs-lookup"><span data-stu-id="f6583-105">DC/OS provides an environment for deploying and scaling clustered workloads, while abstracting hello underlying hardware.</span></span> <span data-ttu-id="f6583-106">Ponad systemem DC/OS istnieje platforma, która zarządza planowaniem i wykonywaniem obciążeń obliczeniowych.</span><span class="sxs-lookup"><span data-stu-id="f6583-106">On top of DC/OS, there is a framework that manages scheduling and executing compute workloads.</span></span>

<span data-ttu-id="f6583-107">Platformy są dostępne dla wielu popularnych zadań, w tym dokumencie opisano sposób uruchamiania tooget wdrażanie kontenerów przy użyciu platformy Marathon.</span><span class="sxs-lookup"><span data-stu-id="f6583-107">While frameworks are available for many popular workloads, this document describes how tooget started deploying containers with Marathon.</span></span> 


## <a name="prerequisites"></a><span data-ttu-id="f6583-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="f6583-108">Prerequisites</span></span>
<span data-ttu-id="f6583-109">Przed przystąpieniem do pracy nad tymi przykładami będziesz potrzebować klastra DC/OS skonfigurowanego w usłudze kontenera platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="f6583-109">Before working through these examples, you need a DC/OS cluster that is configured in Azure Container Service.</span></span> <span data-ttu-id="f6583-110">Należy również toohave łączności zdalnej toothis klastra.</span><span class="sxs-lookup"><span data-stu-id="f6583-110">You also need toohave remote connectivity toothis cluster.</span></span> <span data-ttu-id="f6583-111">Aby uzyskać więcej informacji na temat tych elementów zobacz następujące artykuły hello:</span><span class="sxs-lookup"><span data-stu-id="f6583-111">For more information on these items, see hello following articles:</span></span>

* [<span data-ttu-id="f6583-112">Wdrażanie klastra usługi Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="f6583-112">Deploy an Azure Container Service cluster</span></span>](container-service-deployment.md)
* [<span data-ttu-id="f6583-113">Połącz tooan klastra usługi kontenera platformy Azure</span><span class="sxs-lookup"><span data-stu-id="f6583-113">Connect tooan Azure Container Service cluster</span></span>](../container-service-connect.md)

> [!NOTE]
> <span data-ttu-id="f6583-114">W tym artykule przyjęto założenie, że tunelowanie korzysta klastra DC/OS toohello za pośrednictwem lokalnego portu 80.</span><span class="sxs-lookup"><span data-stu-id="f6583-114">This article assumes you are tunneling toohello DC/OS cluster through your local port 80.</span></span>
>

## <a name="explore-hello-dcos-ui"></a><span data-ttu-id="f6583-115">Eksploruj hello interfejsu użytkownika DC/OS</span><span class="sxs-lookup"><span data-stu-id="f6583-115">Explore hello DC/OS UI</span></span>
<span data-ttu-id="f6583-116">Z tunel Secure Shell (SSH) [ustanowić](../container-service-connect.md), Przeglądaj toohttp://localhost/.</span><span class="sxs-lookup"><span data-stu-id="f6583-116">With a Secure Shell (SSH) tunnel [established](../container-service-connect.md), browse toohttp://localhost/.</span></span> <span data-ttu-id="f6583-117">Ładuje hello interfejsu użytkownika sieci web platformy DC/OS i zawiera informacje o klastrze hello, takich jak używanych zasobów, aktywnych agentów i uruchomione usługi.</span><span class="sxs-lookup"><span data-stu-id="f6583-117">This loads hello DC/OS web UI and shows information about hello cluster, such as used resources, active agents, and running services.</span></span>

![Interfejs użytkownika platformy DC/OS](./media/container-service-mesos-marathon-ui/dcos2.png)

## <a name="explore-hello-marathon-ui"></a><span data-ttu-id="f6583-119">Eksploruj hello interfejs użytkownika platformy Marathon</span><span class="sxs-lookup"><span data-stu-id="f6583-119">Explore hello Marathon UI</span></span>
<span data-ttu-id="f6583-120">Witaj toosee interfejs użytkownika platformy Marathon, przejdź toohttp://localhost/marathon.</span><span class="sxs-lookup"><span data-stu-id="f6583-120">toosee hello Marathon UI, browse toohttp://localhost/marathon.</span></span> <span data-ttu-id="f6583-121">Na tym ekranie można uruchomić w klastrze usługi kontenera platformy Azure DC/OS hello nowy kontener lub inną aplikację.</span><span class="sxs-lookup"><span data-stu-id="f6583-121">From this screen, you can start a new container or another application on hello Azure Container Service DC/OS cluster.</span></span> <span data-ttu-id="f6583-122">Możesz również sprawdzić informacje dotyczące działających kontenerów i aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f6583-122">You can also see information about running containers and applications.</span></span>  

![Interfejs użytkownika platformy Marathon](./media/container-service-mesos-marathon-ui/dcos3.png)

## <a name="deploy-a-docker-formatted-container"></a><span data-ttu-id="f6583-124">Wdrażanie kontenera w formacie programu Docker</span><span class="sxs-lookup"><span data-stu-id="f6583-124">Deploy a Docker-formatted container</span></span>
<span data-ttu-id="f6583-125">toodeploy nowy kontener przy użyciu platformy Marathon, kliknij przycisk **tworzenie aplikacji**, a następnie wprowadź następujące informacje na kartach formularza hello hello:</span><span class="sxs-lookup"><span data-stu-id="f6583-125">toodeploy a new container by using Marathon, click **Create Application**, and enter hello following information into hello form tabs:</span></span>

| <span data-ttu-id="f6583-126">Pole</span><span class="sxs-lookup"><span data-stu-id="f6583-126">Field</span></span> | <span data-ttu-id="f6583-127">Wartość</span><span class="sxs-lookup"><span data-stu-id="f6583-127">Value</span></span> |
| --- | --- |
| <span data-ttu-id="f6583-128">ID</span><span class="sxs-lookup"><span data-stu-id="f6583-128">ID</span></span> |<span data-ttu-id="f6583-129">nginx</span><span class="sxs-lookup"><span data-stu-id="f6583-129">nginx</span></span> |
| <span data-ttu-id="f6583-130">Memory (Pamięć)</span><span class="sxs-lookup"><span data-stu-id="f6583-130">Memory</span></span> | <span data-ttu-id="f6583-131">32</span><span class="sxs-lookup"><span data-stu-id="f6583-131">32</span></span> |
| <span data-ttu-id="f6583-132">Image (Obraz)</span><span class="sxs-lookup"><span data-stu-id="f6583-132">Image</span></span> |<span data-ttu-id="f6583-133">nginx</span><span class="sxs-lookup"><span data-stu-id="f6583-133">nginx</span></span> |
| <span data-ttu-id="f6583-134">Network (Sieć)</span><span class="sxs-lookup"><span data-stu-id="f6583-134">Network</span></span> |<span data-ttu-id="f6583-135">Bridged (Pomostowa)</span><span class="sxs-lookup"><span data-stu-id="f6583-135">Bridged</span></span> |
| <span data-ttu-id="f6583-136">Host Port (Port hosta)</span><span class="sxs-lookup"><span data-stu-id="f6583-136">Host Port</span></span> |<span data-ttu-id="f6583-137">80</span><span class="sxs-lookup"><span data-stu-id="f6583-137">80</span></span> |
| <span data-ttu-id="f6583-138">Protocol (Protokół)</span><span class="sxs-lookup"><span data-stu-id="f6583-138">Protocol</span></span> |<span data-ttu-id="f6583-139">TCP</span><span class="sxs-lookup"><span data-stu-id="f6583-139">TCP</span></span> |

![Interfejs użytkownika New Application (Nowa aplikacja) — General (Ogólne)](./media/container-service-mesos-marathon-ui/dcos4.png)

![Interfejs użytkownika New Application (Nowa aplikacja) — Docker Container (Kontener Docker)](./media/container-service-mesos-marathon-ui/dcos5.png)

![Interfejs użytkownika New Application (Nowa aplikacja) — Ports and Service Discovery (Porty i odnajdowanie usług)](./media/container-service-mesos-marathon-ui/dcos6.png)

<span data-ttu-id="f6583-143">Jeśli chcesz toostatically mapy hello port kontenera tooa portu na agencie hello, należy toouse trybu JSON.</span><span class="sxs-lookup"><span data-stu-id="f6583-143">If you want toostatically map hello container port tooa port on hello agent, you need toouse JSON Mode.</span></span> <span data-ttu-id="f6583-144">toodo tak, Przełącz Kreatora nowej aplikacji hello zbyt**tryb JSON** za pomocą przełącznika hello.</span><span class="sxs-lookup"><span data-stu-id="f6583-144">toodo so, switch hello New Application wizard too**JSON Mode** by using hello toggle.</span></span> <span data-ttu-id="f6583-145">Następnie wprowadź następujące ustawienia w obszarze hello hello `portMappings` sekcji hello definicji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f6583-145">Then enter hello following setting under hello `portMappings` section of hello application definition.</span></span> <span data-ttu-id="f6583-146">W tym przykładzie wiąże hello kontenera tooport 80 agenta DC/OS hello port 80.</span><span class="sxs-lookup"><span data-stu-id="f6583-146">This example binds port 80 of hello container tooport 80 of hello DC/OS agent.</span></span> <span data-ttu-id="f6583-147">Po wprowadzeniu tej zmiany możesz wyłączyć tryb JSON w kreatorze.</span><span class="sxs-lookup"><span data-stu-id="f6583-147">You can switch this wizard out of JSON Mode after you make this change.</span></span>

```none
"hostPort": 80,
```

![Interfejs użytkownika New Application (Nowa aplikacja) — przykładowy port 80](./media/container-service-mesos-marathon-ui/dcos13.png)

<span data-ttu-id="f6583-149">Kontrole kondycji tooenable należy ustawić ścieżkę na powitania **sprawdza kondycji** kartę.</span><span class="sxs-lookup"><span data-stu-id="f6583-149">If you want tooenable health checks, set a path on hello **Health Checks** tab.</span></span>

![Interfejs użytkownika New Application (Nowa aplikacja) — kontrole kondycji](./media/container-service-mesos-marathon-ui/dcos_healthcheck.png)

<span data-ttu-id="f6583-151">Witaj klastra DC/OS jest wdrażany z zestawem agentów prywatnych i publicznych.</span><span class="sxs-lookup"><span data-stu-id="f6583-151">hello DC/OS cluster is deployed with set of private and public agents.</span></span> <span data-ttu-id="f6583-152">Witaj klastra toobe tooaccess stanie aplikacji hello Internet należy agenta publicznego tooa aplikacji hello toodeploy.</span><span class="sxs-lookup"><span data-stu-id="f6583-152">For hello cluster toobe able tooaccess applications from hello Internet, you need toodeploy hello applications tooa public agent.</span></span> <span data-ttu-id="f6583-153">toodo należy wybrać hello **opcjonalnie** kartę hello Kreatora nowej aplikacji, a następnie wprowadź **slave_public** dla hello **zaakceptowane role zasobów**.</span><span class="sxs-lookup"><span data-stu-id="f6583-153">toodo so, select hello **Optional** tab of hello New Application wizard and enter **slave_public** for hello **Accepted Resource Roles**.</span></span>

<span data-ttu-id="f6583-154">Następnie kliknij przycisk **Create Application** (Utwórz aplikację).</span><span class="sxs-lookup"><span data-stu-id="f6583-154">Then click **Create Application**.</span></span>

![Interfejs użytkownika New Application (Nowa aplikacja) — ustawienia agenta publicznego](./media/container-service-mesos-marathon-ui/dcos14.png)

<span data-ttu-id="f6583-156">Do strony głównej platformy Marathon hello zobacz temat hello stan wdrożenia kontenera hello.</span><span class="sxs-lookup"><span data-stu-id="f6583-156">Back on hello Marathon main page, you can see hello deployment status for hello container.</span></span> <span data-ttu-id="f6583-157">Początkowo będzie widoczny stan **Deploying** (Wdrażanie).</span><span class="sxs-lookup"><span data-stu-id="f6583-157">Initially you see a status of **Deploying**.</span></span> <span data-ttu-id="f6583-158">Po pomyślnym wdrożeniu hello zmiany stanu zbyt**systemem**.</span><span class="sxs-lookup"><span data-stu-id="f6583-158">After a successful deployment, hello status changes too**Running**.</span></span>

![Strona główna interfejsu użytkownika platformy Marathon — stan wdrożenia kontenera](./media/container-service-mesos-marathon-ui/dcos7.png)

<span data-ttu-id="f6583-160">Przełącznik sieci web platformy DC/OS wstecz toohello interfejsu użytkownika (http://localhost/), zobacz, czy zadanie (w tym przypadku kontener w formacie programu Docker) jest uruchomiona w klastrze DC/OS hello.</span><span class="sxs-lookup"><span data-stu-id="f6583-160">When you switch back toohello DC/OS web UI (http://localhost/), you see that a task (in this case, a Docker-formatted container) is running on hello DC/OS cluster.</span></span>

![Interfejs użytkownika — zadanie uruchomione w klastrze hello sieci web platformy DC/OS](./media/container-service-mesos-marathon-ui/dcos8.png)

<span data-ttu-id="f6583-162">węzeł klastra hello toosee, który hello zadań jest uruchomiona na, kliknij przycisk hello **węzłów** kartę.</span><span class="sxs-lookup"><span data-stu-id="f6583-162">toosee hello cluster node that hello task is running on, click hello **Nodes** tab.</span></span>

![Interfejs użytkownika sieci Web platformy DC/OS — węzeł klastra zadania](./media/container-service-mesos-marathon-ui/dcos9.png)

## <a name="reach-hello-container"></a><span data-ttu-id="f6583-164">Osiągnąć hello kontenera</span><span class="sxs-lookup"><span data-stu-id="f6583-164">Reach hello container</span></span>

<span data-ttu-id="f6583-165">W tym przykładzie aplikacja hello jest uruchomiona w węźle agenta publicznego.</span><span class="sxs-lookup"><span data-stu-id="f6583-165">In this example, hello application is running on a public agent node.</span></span> <span data-ttu-id="f6583-166">Zostanie wyświetlona aplikacja hello z hello internet przechodząc agenta toohello nazwę FQDN klastra hello: `http://[DNSPREFIX]agents.[REGION].cloudapp.azure.com`, gdzie:</span><span class="sxs-lookup"><span data-stu-id="f6583-166">You reach hello application from hello internet by browsing toohello agent FQDN of hello cluster: `http://[DNSPREFIX]agents.[REGION].cloudapp.azure.com`, where:</span></span>

* <span data-ttu-id="f6583-167">**DNSPREFIX** jest hello prefiks DNS podany podczas wdrażania klastra hello.</span><span class="sxs-lookup"><span data-stu-id="f6583-167">**DNSPREFIX** is hello DNS prefix that you provided when you deployed hello cluster.</span></span>
* <span data-ttu-id="f6583-168">**REGION** jest hello regionu, w którym znajduje się w grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="f6583-168">**REGION** is hello region in which your resource group is located.</span></span>

    ![Nginx z Internetu](./media/container-service-mesos-marathon-ui/nginx.png)


## <a name="next-steps"></a><span data-ttu-id="f6583-170">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f6583-170">Next steps</span></span>
* [<span data-ttu-id="f6583-171">Praca z DC/OS i hello interfejsu API platformy Marathon</span><span class="sxs-lookup"><span data-stu-id="f6583-171">Work with DC/OS and hello Marathon API</span></span>](container-service-mesos-marathon-rest.md)

* <span data-ttu-id="f6583-172">Nowości dotyczące hello usługi kontenera platformy Azure z Mesos</span><span class="sxs-lookup"><span data-stu-id="f6583-172">Deep dive on hello Azure Container Service with Mesos</span></span>

    > [!VIDEO https://channel9.msdn.com/Events/Microsoft-Azure/AzureCon-2015/ACON203/player]
    > 
