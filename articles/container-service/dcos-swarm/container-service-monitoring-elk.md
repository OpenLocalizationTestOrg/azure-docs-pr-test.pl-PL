---
title: "aaaMonitor klaster Azure DC/OS - stosu ŁOSI | Dokumentacja firmy Microsoft"
description: "Monitorowanie klastra DC/OS w klastrze usługi kontenera platformy Azure z ŁOSI (Elasticsearch Logstash i Kibana)."
services: container-service
documentationcenter: 
author: sauryadas
manager: madhana
editor: 
tags: acs, azure-container-service
keywords: "Kontenery, DC/OS, Azure, monitorowanie, łosi"
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/27/2017
ms.author: saudas
ms.custom: mvc
ms.openlocfilehash: 8d81c5342616ec14880d38803cdf95f5845a669b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-cluster-with-elk"></a><span data-ttu-id="a830b-104">Monitor klastra usługi kontenera platformy Azure z ŁOSI</span><span class="sxs-lookup"><span data-stu-id="a830b-104">Monitor an Azure Container Service cluster with ELK</span></span>
<span data-ttu-id="a830b-105">W tym artykule przedstawiony sposób stosu hello toodeploy ŁOSI (Elasticsearch, Logstash, Kibana) w klastrze DC/OS usługi kontenera platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="a830b-105">In this article, we demonstrate how toodeploy hello ELK (Elasticsearch, Logstash, Kibana) stack on a DC/OS cluster in Azure Container Service.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="a830b-106">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="a830b-106">Prerequisites</span></span>
<span data-ttu-id="a830b-107">[Wdrażanie](container-service-deployment.md) i [połączyć](../container-service-connect.md) klastra DC/OS konfigurowane za pomocą usługi kontenera platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="a830b-107">[Deploy](container-service-deployment.md) and [connect](../container-service-connect.md) a DC/OS cluster configured by Azure Container Service.</span></span> <span data-ttu-id="a830b-108">Eksploruj pulpitu nawigacyjnego DC/OS hello i usługi Marathon [tutaj](container-service-mesos-marathon-ui.md).</span><span class="sxs-lookup"><span data-stu-id="a830b-108">Explore hello DC/OS dashboard and Marathon services [here](container-service-mesos-marathon-ui.md).</span></span> <span data-ttu-id="a830b-109">Zainstaluj również hello [modułu równoważenia obciążenia platformy Marathon](container-service-load-balancing.md).</span><span class="sxs-lookup"><span data-stu-id="a830b-109">Also install hello [Marathon Load Balancer](container-service-load-balancing.md).</span></span>


## <a name="elk-elasticsearch-logstash-kibana"></a><span data-ttu-id="a830b-110">ŁOSI (Elasticsearch, Logstash, Kibana)</span><span class="sxs-lookup"><span data-stu-id="a830b-110">ELK (Elasticsearch, Logstash, Kibana)</span></span>
<span data-ttu-id="a830b-111">Stos ŁOSI jest kombinacją Elasticsearch, Logstash, i Kibana udostępniający stosu tooend zakończenia mogą być używane toomonitor i analizowanie dzienników w klastrze.</span><span class="sxs-lookup"><span data-stu-id="a830b-111">ELK stack is a combination of Elasticsearch, Logstash, and Kibana that provides an end tooend stack that can be used toomonitor and analyze logs in your cluster.</span></span>

## <a name="configure-hello-elk-stack-on-a-dcos-cluster"></a><span data-ttu-id="a830b-112">Skonfiguruj hello ŁOSI stosu w klastrze DC/OS</span><span class="sxs-lookup"><span data-stu-id="a830b-112">Configure hello ELK stack on a DC/OS cluster</span></span>
<span data-ttu-id="a830b-113">Dostęp za pośrednictwem interfejsu użytkownika DC/OS [http://localhost:80 /](http://localhost:80/) raz w hello interfejsu użytkownika DC/OS Przejdź zbyt**Universe**.</span><span class="sxs-lookup"><span data-stu-id="a830b-113">Access your DC/OS UI via [http://localhost:80/](http://localhost:80/) Once in hello DC/OS UI navigate too**Universe**.</span></span> <span data-ttu-id="a830b-114">Wyszukiwanie i instalowanie Elasticsearch, Logstash i Kibana z hello Universe DC/OS i w tej kolejności.</span><span class="sxs-lookup"><span data-stu-id="a830b-114">Search and install Elasticsearch, Logstash, and Kibana from hello DC/OS Universe and in that specific order.</span></span> <span data-ttu-id="a830b-115">Więcej informacji o konfiguracji przejście toohello **instalacji zaawansowanym** łącza.</span><span class="sxs-lookup"><span data-stu-id="a830b-115">You can learn more about configuration if you go toohello **Advanced Installation** link.</span></span>

![ELK1](./media/container-service-monitoring-elk/elk1.PNG) ![ELK2](./media/container-service-monitoring-elk/elk2.PNG) ![ELK3](./media/container-service-monitoring-elk/elk3.PNG) 

<span data-ttu-id="a830b-119">Raz hello ŁOSI kontenery i czy do pracy, należy uzyskać przy użyciu platformy Marathon-LB toobe Kibana tooenable.</span><span class="sxs-lookup"><span data-stu-id="a830b-119">Once hello ELK containers and are up and running, you need tooenable Kibana toobe accessed through Marathon-LB.</span></span> <span data-ttu-id="a830b-120">Przejdź za **usług** > **kibana**i kliknij przycisk **Edytuj** jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="a830b-120">Navigate too **Services** > **kibana**, and click **Edit** as shown below.</span></span>

![ELK4](./media/container-service-monitoring-elk/elk4.PNG)


<span data-ttu-id="a830b-122">Przełącz zbyt**tryb JSON** i przewiń w dół do sekcji etykiety toohello.</span><span class="sxs-lookup"><span data-stu-id="a830b-122">Toggle too**JSON mode** and scroll down toohello labels section.</span></span>
<span data-ttu-id="a830b-123">Należy tooadd `"HAPROXY_GROUP": "external"` wpis tutaj jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="a830b-123">You need tooadd a `"HAPROXY_GROUP": "external"` entry here as shown below.</span></span>
<span data-ttu-id="a830b-124">Po kliknięciu **wdrażać zmiany**, ponownym uruchomieniu kontenera.</span><span class="sxs-lookup"><span data-stu-id="a830b-124">Once you click **Deploy changes**, your container restarts.</span></span>

![ELK5](./media/container-service-monitoring-elk/elk5.PNG)


<span data-ttu-id="a830b-126">Jeśli chcesz, aby tooverify tego Kibana jest zarejestrowany jako usługa na pulpicie nawigacyjnym HAPROXY hello, należy tooopen portu 9090 w klastrze agenta hello jak HAPROXY działa na porcie 9090.</span><span class="sxs-lookup"><span data-stu-id="a830b-126">If you want tooverify that Kibana is registered as a service in hello HAPROXY dashboard, you need tooopen port 9090 on hello agent cluster as HAPROXY runs on port 9090.</span></span>
<span data-ttu-id="a830b-127">Domyślnie możemy otworzyć porty 80, 8080 i 443 w hello klastra agenta DC/OS.</span><span class="sxs-lookup"><span data-stu-id="a830b-127">By default, we open ports 80, 8080, and 443 in hello DC/OS agent cluster.</span></span>
<span data-ttu-id="a830b-128">Instrukcje tooopen portu i podaj oceny publicznego są udostępniane [tutaj](container-service-enable-public-access.md).</span><span class="sxs-lookup"><span data-stu-id="a830b-128">Instructions tooopen a port and provide public assess are provided [here](container-service-enable-public-access.md).</span></span>

<span data-ttu-id="a830b-129">tooaccess hello HAPROXY pulpitu nawigacyjnego, otwórz hello warstwa Marathon-LB interfejsu administracyjnego na: `http://$PUBLIC_NODE_IP_ADDRESS:9090/haproxy?stats`.</span><span class="sxs-lookup"><span data-stu-id="a830b-129">tooaccess hello HAPROXY dashboard, open hello Marathon-LB admin interface at: `http://$PUBLIC_NODE_IP_ADDRESS:9090/haproxy?stats`.</span></span>
<span data-ttu-id="a830b-130">Po przejściu toohello adres URL powinien zostać wyświetlony pulpit nawigacyjny HAPROXY hello w sposób przedstawiony poniżej i powinna być widoczna dla Kibana wpisu usługi.</span><span class="sxs-lookup"><span data-stu-id="a830b-130">Once you navigate toohello URL, you should see hello HAPROXY dashboard as shown below and you should see a service entry for Kibana.</span></span>

![ELK6](./media/container-service-monitoring-elk/elk6.PNG)


<span data-ttu-id="a830b-132">tooaccess hello Kibana dashboard, który jest wdrażana na porcie 5601, należy portu tooopen 5601.</span><span class="sxs-lookup"><span data-stu-id="a830b-132">tooaccess hello Kibana dashboard, which is deployed on port 5601, you need tooopen port 5601.</span></span> <span data-ttu-id="a830b-133">Postępuj zgodnie z instrukcjami [tutaj](container-service-enable-public-access.md).</span><span class="sxs-lookup"><span data-stu-id="a830b-133">Follow instructions [here](container-service-enable-public-access.md).</span></span> <span data-ttu-id="a830b-134">Następnie otwórz pulpit nawigacyjny Kibana hello w: `http://localhost:5601`.</span><span class="sxs-lookup"><span data-stu-id="a830b-134">Then open hello Kibana dashboard at: `http://localhost:5601`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a830b-135">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a830b-135">Next steps</span></span>

* <span data-ttu-id="a830b-136">Dla dziennika systemu i aplikacji przekazywania i ustawień, zobacz [zarządzanie dziennikiem w DC/OS z ŁOSI](https://docs.mesosphere.com/1.8/administration/logging/elk/).</span><span class="sxs-lookup"><span data-stu-id="a830b-136">For system and application log forwarding and setup, see [Log Management in DC/OS with ELK](https://docs.mesosphere.com/1.8/administration/logging/elk/).</span></span>

* <span data-ttu-id="a830b-137">Zobacz dzienniki toofilter [filtrowania dzienniki z ŁOSI](https://docs.mesosphere.com/1.8/administration/logging/filter-elk/).</span><span class="sxs-lookup"><span data-stu-id="a830b-137">toofilter logs, see [Filtering Logs with ELK](https://docs.mesosphere.com/1.8/administration/logging/filter-elk/).</span></span> 

 

