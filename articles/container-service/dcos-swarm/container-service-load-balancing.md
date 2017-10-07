---
title: kontenery saldo aaaLoad w klastrze Azure DC/OS | Dokumentacja firmy Microsoft
description: "Zrównoważenia obciążenia w wielu kontenerów w klastrze usługi kontenera platformy Azure DC/OS."
services: container-service
documentationcenter: 
author: rgardler
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Kontenery, mikrousługi, DC/OS, Azure"
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/02/2017
ms.author: rogardle
ms.custom: mvc
ms.openlocfilehash: 2249cb06880cdb7e9a3aa94c0750c6a27316d349
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="load-balance-containers-in-an-azure-container-service-dcos-cluster"></a><span data-ttu-id="6282c-104">Kontenery Równoważenie obciążenia klastra usługi kontenera platformy Azure DC/OS</span><span class="sxs-lookup"><span data-stu-id="6282c-104">Load balance containers in an Azure Container Service DC/OS cluster</span></span>
<span data-ttu-id="6282c-105">W tym artykule firma Microsoft Poznaj jak toocreate wewnętrznego modułu równoważenia obciążenia w DC/OS zarządzane przy użyciu platformy Marathon-LB usługi kontenera platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="6282c-105">In this article, we explore how toocreate an internal load balancer in a DC/OS managed Azure Container Service using Marathon-LB.</span></span> <span data-ttu-id="6282c-106">Ta konfiguracja umożliwia tooscale możesz aplikacji w poziomie.</span><span class="sxs-lookup"><span data-stu-id="6282c-106">This configuration enables you tooscale your applications horizontally.</span></span> <span data-ttu-id="6282c-107">Można też tootake zaletą hello agenta publicznego i prywatnego klastrów przez umieszczenie z usługi równoważenia obciążenia w klastrze publicznego hello i kontenerów aplikacji w klastrze prywatnej hello.</span><span class="sxs-lookup"><span data-stu-id="6282c-107">It also allows you tootake advantage of hello public and private agent clusters by placing your load balancers on hello public cluster and your application containers on hello private cluster.</span></span> <span data-ttu-id="6282c-108">W tym samouczku zostały wykonane następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="6282c-108">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="6282c-109">Konfigurowanie równoważenia obciążenia platformy Marathon</span><span class="sxs-lookup"><span data-stu-id="6282c-109">Configure a Marathon Load Balancer</span></span>
> * <span data-ttu-id="6282c-110">Wdrażanie aplikacji przy użyciu usługi równoważenia obciążenia hello</span><span class="sxs-lookup"><span data-stu-id="6282c-110">Deploy an application using hello load balancer</span></span>
> * <span data-ttu-id="6282c-111">Konfigurowanie i modułu równoważenia obciążenia Azure</span><span class="sxs-lookup"><span data-stu-id="6282c-111">Configure and Azure load balancer</span></span>

<span data-ttu-id="6282c-112">Należy ACS DC/OS hello toocomplete klastra kroków w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="6282c-112">You need an ACS DC/OS cluster toocomplete hello steps in this tutorial.</span></span> <span data-ttu-id="6282c-113">W razie potrzeby [w tym przykładzie skrypt](./../kubernetes/scripts/container-service-cli-deploy-dcos.md) można utworzyć.</span><span class="sxs-lookup"><span data-stu-id="6282c-113">If needed, [this script sample](./../kubernetes/scripts/container-service-cli-deploy-dcos.md) can create one for you.</span></span>

<span data-ttu-id="6282c-114">Ten samouczek wymaga hello Azure CLI w wersji 2.0.4 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="6282c-114">This tutorial requires hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="6282c-115">Uruchom `az --version` toofind hello wersji.</span><span class="sxs-lookup"><span data-stu-id="6282c-115">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="6282c-116">Jeśli potrzebujesz tooupgrade, zobacz [zainstalować Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="6282c-116">If you need tooupgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

## <a name="load-balancing-overview"></a><span data-ttu-id="6282c-117">Równoważenie obciążenia — omówienie</span><span class="sxs-lookup"><span data-stu-id="6282c-117">Load balancing overview</span></span>

<span data-ttu-id="6282c-118">Istnieją dwie warstwy równoważenia obciążenia w klastrze usługi kontenera platformy Azure DC/OS:</span><span class="sxs-lookup"><span data-stu-id="6282c-118">There are two load-balancing layers in an Azure Container Service DC/OS cluster:</span></span> 

<span data-ttu-id="6282c-119">**Moduł równoważenia obciążenia Azure** udostępnia publicznych punktów wejścia (hello dostęp do tych, że użytkownicy końcowi).</span><span class="sxs-lookup"><span data-stu-id="6282c-119">**Azure Load Balancer** provides public entry points (hello ones that end users access).</span></span> <span data-ttu-id="6282c-120">Warstwa Azure LB jest udostępniany automatycznie przez usługi kontenera platformy Azure i jest domyślnie skonfigurowany tooexpose portu 80 i 443 8080.</span><span class="sxs-lookup"><span data-stu-id="6282c-120">An Azure LB is provided automatically by Azure Container Service and is, by default, configured tooexpose port 80, 443 and 8080.</span></span>

<span data-ttu-id="6282c-121">**Witaj Marathon moduł równoważenia obciążenia (warstwa marathon-lb)** tras ruchu przychodzącego żądania toocontainer wystąpień, które usługi te żądania.</span><span class="sxs-lookup"><span data-stu-id="6282c-121">**hello Marathon Load Balancer (marathon-lb)** routes inbound requests toocontainer instances that service these requests.</span></span> <span data-ttu-id="6282c-122">Skalowania hello kontenerów świadczących naszej usługi sieci web, hello warstwa marathon-lb jest dynamicznie dostosowuje.</span><span class="sxs-lookup"><span data-stu-id="6282c-122">As we scale hello containers providing our web service, hello marathon-lb dynamically adapts.</span></span> <span data-ttu-id="6282c-123">Ten moduł równoważenia obciążenia nie jest dostępny domyślnie w usłudze kontenera, ale jest łatwe tooinstall.</span><span class="sxs-lookup"><span data-stu-id="6282c-123">This load balancer is not provided by default in your Container Service, but it is easy tooinstall.</span></span>

## <a name="configure-marathon-load-balancer"></a><span data-ttu-id="6282c-124">Konfigurowanie równoważenia obciążenia platformy Marathon</span><span class="sxs-lookup"><span data-stu-id="6282c-124">Configure Marathon Load Balancer</span></span>

<span data-ttu-id="6282c-125">Moduł równoważenia obciążenia platformy Marathon dynamicznie ponownie konfiguruje oparty na powitania kontenerów, które zostały wdrożone.</span><span class="sxs-lookup"><span data-stu-id="6282c-125">Marathon Load Balancer dynamically reconfigures itself based on hello containers that you've deployed.</span></span> <span data-ttu-id="6282c-126">Istnieje również odporne toohello utratę kontenera lub agenta — jeśli dzieje się tak, Apache Mesos uruchomieniu hello kontener w innym miejscu i dostosowuje warstwa marathon-lb.</span><span class="sxs-lookup"><span data-stu-id="6282c-126">It's also resilient toohello loss of a container or an agent - if this occurs, Apache Mesos restarts hello container elsewhere and marathon-lb adapts.</span></span>

<span data-ttu-id="6282c-127">Hello uruchom następujące polecenie modułu równoważenia obciążenia platformy marathon hello tooinstall w klastrze hello agenta publicznego.</span><span class="sxs-lookup"><span data-stu-id="6282c-127">Run hello following command tooinstall hello marathon load balancer on hello public agent's cluster.</span></span>

```azurecli-interactive
dcos package install marathon-lb
```

## <a name="deploy-load-balanced-application"></a><span data-ttu-id="6282c-128">Wdrożenie aplikacji o zrównoważonym obciążeniu</span><span class="sxs-lookup"><span data-stu-id="6282c-128">Deploy load balanced application</span></span>

<span data-ttu-id="6282c-129">Teraz, gdy mamy hello pakiet marathon-lb, możemy wdrożyć kontenera aplikacji czy Życzymy saldo tooload.</span><span class="sxs-lookup"><span data-stu-id="6282c-129">Now that we have hello marathon-lb package, we can deploy an application container that we wish tooload balance.</span></span> 

<span data-ttu-id="6282c-130">Najpierw pobierz hello FQDN agentów hello publicznie udostępnione.</span><span class="sxs-lookup"><span data-stu-id="6282c-130">First, get hello FQDN of hello publicly exposed agents.</span></span>

```azurecli-interactive
az acs list --resource-group myResourceGroup --query "[0].agentPoolProfiles[0].fqdn" --output tsv
```

<span data-ttu-id="6282c-131">Następnie utwórz plik o nazwie *hello web.json* i kopia w powitania po zawartości.</span><span class="sxs-lookup"><span data-stu-id="6282c-131">Next, create a file named *hello-web.json* and copy in hello following contents.</span></span> <span data-ttu-id="6282c-132">Witaj `HAPROXY_0_VHOST` etykiety musi toobe zaktualizowane hello FQDN hello agentów DC/OS.</span><span class="sxs-lookup"><span data-stu-id="6282c-132">hello `HAPROXY_0_VHOST` label needs toobe updated with hello FQDN of hello DC/OS agents.</span></span> 

```json
{
  "id": "web",
  "container": {
    "type": "DOCKER",
    "docker": {
      "image": "yeasy/simple-web",
      "network": "BRIDGE",
      "portMappings": [
        { "hostPort": 0, "containerPort": 80, "servicePort": 10000 }
      ],
      "forcePullImage":true
    }
  },
  "instances": 3,
  "cpus": 0.1,
  "mem": 65,
  "healthChecks": [{
      "protocol": "HTTP",
      "path": "/",
      "portIndex": 0,
      "timeoutSeconds": 10,
      "gracePeriodSeconds": 10,
      "intervalSeconds": 2,
      "maxConsecutiveFailures": 10
  }],
  "labels":{
    "HAPROXY_GROUP":"external",
    "HAPROXY_0_VHOST":"YOUR FQDN",
    "HAPROXY_0_MODE":"http"
  }
}
```

<span data-ttu-id="6282c-133">Za pomocą aplikacji hello toorun interfejsu wiersza polecenia DC/OS hello.</span><span class="sxs-lookup"><span data-stu-id="6282c-133">Use hello DC/OS CLI toorun hello application.</span></span> <span data-ttu-id="6282c-134">Domyślnie Marathon wdraża hello hello awaryjności toohello prywatnej klastra.</span><span class="sxs-lookup"><span data-stu-id="6282c-134">By default Marathon deploys hello hello applicaton toohello private cluster.</span></span> <span data-ttu-id="6282c-135">Oznacza to, że hello powyżej wdrożenia jest dostępny tylko przez moduł równoważenia obciążenia, który jest zwykle hello żądanego zachowania.</span><span class="sxs-lookup"><span data-stu-id="6282c-135">This means that hello above deployment is only accessible via your load balancer, which is usually hello desired behavior.</span></span>

```azurecli-interactive
dcos marathon app add hello-web.json
```

<span data-ttu-id="6282c-136">Po wdrożeniu aplikacji hello Przeglądaj toohello FQDN hello agenta klastra tooview ze zrównoważonym obciążeniem aplikacji.</span><span class="sxs-lookup"><span data-stu-id="6282c-136">Once hello application has been deployed, browse toohello FQDN of hello agent cluster tooview load balanced application.</span></span>

![Obraz aplikacji ze zrównoważonym obciążeniem](./media/container-service-load-balancing/lb-app.png)

## <a name="configure-azure-load-balancer"></a><span data-ttu-id="6282c-138">Konfigurowanie usługi równoważenia obciążenia Azure</span><span class="sxs-lookup"><span data-stu-id="6282c-138">Configure Azure Load Balancer</span></span>

<span data-ttu-id="6282c-139">Domyślnie moduł Azure Load Balancer udostępnia porty 80, 8080 i 443.</span><span class="sxs-lookup"><span data-stu-id="6282c-139">By default, Azure Load Balancer exposes ports 80, 8080, and 443.</span></span> <span data-ttu-id="6282c-140">Jeśli używasz jednego z tych trzech portów (tak jak w hello powyżej przykładzie), a następnie nic nie należy toodo.</span><span class="sxs-lookup"><span data-stu-id="6282c-140">If you're using one of these three ports (as we do in hello above example), then there is nothing you need toodo.</span></span> <span data-ttu-id="6282c-141">Powinno być możliwe toohit FQDN modułu równoważenia obciążenia agenta i każdym odświeżeniu, będzie naciśniesz jeden z trzech serwerów sieci web w działaniu okrężnym.</span><span class="sxs-lookup"><span data-stu-id="6282c-141">You should be able toohit your agent load balancer's FQDN, and each time you refresh, you'll hit one of your three web servers in a round-robin fashion.</span></span> 

<span data-ttu-id="6282c-142">Jeśli używasz innego portu, należy reguła tooadd okrężnego oraz sondę modułu równoważenia obciążenia hello hello portu, który został użyty.</span><span class="sxs-lookup"><span data-stu-id="6282c-142">If you use a different port, you need tooadd a round-robin rule and a probe on hello load balancer for hello port that you used.</span></span> <span data-ttu-id="6282c-143">Można to zrobić z hello [interfejsu wiersza polecenia Azure](../../azure-resource-manager/xplat-cli-azure-resource-manager.md), za pomocą polecenia hello `azure network lb rule create` i `azure network lb probe create`.</span><span class="sxs-lookup"><span data-stu-id="6282c-143">You can do this from hello [Azure CLI](../../azure-resource-manager/xplat-cli-azure-resource-manager.md), with hello commands `azure network lb rule create` and `azure network lb probe create`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6282c-144">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="6282c-144">Next steps</span></span>

<span data-ttu-id="6282c-145">W tym samouczku poznanie równoważenia obciążenia w ACS z parametry hello Marathon i obciążenia Azure równoważenia tym hello następujące akcje:</span><span class="sxs-lookup"><span data-stu-id="6282c-145">In this tutorial, you learned about load balancing in ACS with both hello Marathon and Azure load balancers including hello following actions:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="6282c-146">Konfigurowanie równoważenia obciążenia platformy Marathon</span><span class="sxs-lookup"><span data-stu-id="6282c-146">Configure a Marathon Load Balancer</span></span>
> * <span data-ttu-id="6282c-147">Wdrażanie aplikacji przy użyciu usługi równoważenia obciążenia hello</span><span class="sxs-lookup"><span data-stu-id="6282c-147">Deploy an application using hello load balancer</span></span>
> * <span data-ttu-id="6282c-148">Konfigurowanie i modułu równoważenia obciążenia Azure</span><span class="sxs-lookup"><span data-stu-id="6282c-148">Configure and Azure load balancer</span></span>

<span data-ttu-id="6282c-149">Przejdź dalej toolearn samouczka toohello Integrowanie usługi Azure storage z DC/OS na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="6282c-149">Advance toohello next tutorial toolearn about integrating Azure storage with DC/OS in Azure.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="6282c-150">Azure instalacji udziału plików w klastrze DC/OS</span><span class="sxs-lookup"><span data-stu-id="6282c-150">Mount Azure File Share in DC/OS cluster</span></span>](container-service-dcos-fileshare.md)