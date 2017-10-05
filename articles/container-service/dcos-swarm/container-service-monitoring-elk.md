---
title: "Monitorowanie klastra Azure DC/OS - stosu ŁOSI | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: fcfa277cdd0f3cebc0fbbb23e771fb23ffbe2ca6
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="monitor-an-azure-container-service-cluster-with-elk"></a><span data-ttu-id="8bdbf-104">Monitor klastra usługi kontenera platformy Azure z ŁOSI</span><span class="sxs-lookup"><span data-stu-id="8bdbf-104">Monitor an Azure Container Service cluster with ELK</span></span>
<span data-ttu-id="8bdbf-105">W tym artykule przedstawiony sposób wdrażania stosu ŁOSI (Elasticsearch, Logstash, Kibana) w klastrze DC/OS usługi kontenera platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="8bdbf-105">In this article, we demonstrate how to deploy the ELK (Elasticsearch, Logstash, Kibana) stack on a DC/OS cluster in Azure Container Service.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="8bdbf-106">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="8bdbf-106">Prerequisites</span></span>
<span data-ttu-id="8bdbf-107">[Wdrażanie](container-service-deployment.md) i [połączyć](../container-service-connect.md) klastra DC/OS konfigurowane za pomocą usługi kontenera platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="8bdbf-107">[Deploy](container-service-deployment.md) and [connect](../container-service-connect.md) a DC/OS cluster configured by Azure Container Service.</span></span> <span data-ttu-id="8bdbf-108">Eksplorowanie usługi Pulpit nawigacyjny DC/OS i Marathon [tutaj](container-service-mesos-marathon-ui.md).</span><span class="sxs-lookup"><span data-stu-id="8bdbf-108">Explore the DC/OS dashboard and Marathon services [here](container-service-mesos-marathon-ui.md).</span></span> <span data-ttu-id="8bdbf-109">Zainstaluj również [modułu równoważenia obciążenia platformy Marathon](container-service-load-balancing.md).</span><span class="sxs-lookup"><span data-stu-id="8bdbf-109">Also install the [Marathon Load Balancer](container-service-load-balancing.md).</span></span>


## <a name="elk-elasticsearch-logstash-kibana"></a><span data-ttu-id="8bdbf-110">ŁOSI (Elasticsearch, Logstash, Kibana)</span><span class="sxs-lookup"><span data-stu-id="8bdbf-110">ELK (Elasticsearch, Logstash, Kibana)</span></span>
<span data-ttu-id="8bdbf-111">Stos ŁOSI jest kombinacją Elasticsearch, Logstash i Kibana, która zapewnia kompleksowe stosu, który może służyć do monitorowania i analizować dzienniki w klastrze.</span><span class="sxs-lookup"><span data-stu-id="8bdbf-111">ELK stack is a combination of Elasticsearch, Logstash, and Kibana that provides an end to end stack that can be used to monitor and analyze logs in your cluster.</span></span>

## <a name="configure-the-elk-stack-on-a-dcos-cluster"></a><span data-ttu-id="8bdbf-112">Skonfigurować stosu ŁOSI w klastrze DC/OS</span><span class="sxs-lookup"><span data-stu-id="8bdbf-112">Configure the ELK stack on a DC/OS cluster</span></span>
<span data-ttu-id="8bdbf-113">Dostęp za pośrednictwem interfejsu użytkownika DC/OS [http://localhost:80 /](http://localhost:80/) raz w Interfejsie użytkownika DC/OS przejdź do **Universe**.</span><span class="sxs-lookup"><span data-stu-id="8bdbf-113">Access your DC/OS UI via [http://localhost:80/](http://localhost:80/) Once in the DC/OS UI navigate to **Universe**.</span></span> <span data-ttu-id="8bdbf-114">Wyszukiwanie i instalowanie Elasticsearch, Logstash i Kibana z Universe DC/OS i w tej kolejności.</span><span class="sxs-lookup"><span data-stu-id="8bdbf-114">Search and install Elasticsearch, Logstash, and Kibana from the DC/OS Universe and in that specific order.</span></span> <span data-ttu-id="8bdbf-115">Więcej informacji o konfiguracji z **instalacji zaawansowanym** łącza.</span><span class="sxs-lookup"><span data-stu-id="8bdbf-115">You can learn more about configuration if you go to the **Advanced Installation** link.</span></span>

![ELK1](./media/container-service-monitoring-elk/elk1.PNG) ![ELK2](./media/container-service-monitoring-elk/elk2.PNG) ![ELK3](./media/container-service-monitoring-elk/elk3.PNG) 

<span data-ttu-id="8bdbf-119">Po ŁOSI kontenery i czy do pracy, musisz włączyć Kibana przy użyciu platformy Marathon-LB.</span><span class="sxs-lookup"><span data-stu-id="8bdbf-119">Once the ELK containers and are up and running, you need to enable Kibana to be accessed through Marathon-LB.</span></span> <span data-ttu-id="8bdbf-120">Przejdź do **usług** > **kibana**i kliknij przycisk **Edytuj** jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="8bdbf-120">Navigate to **Services** > **kibana**, and click **Edit** as shown below.</span></span>

![ELK4](./media/container-service-monitoring-elk/elk4.PNG)


<span data-ttu-id="8bdbf-122">Przełącz, aby **tryb JSON** i przewiń w dół do sekcji etykiety.</span><span class="sxs-lookup"><span data-stu-id="8bdbf-122">Toggle to **JSON mode** and scroll down to the labels section.</span></span>
<span data-ttu-id="8bdbf-123">Konieczne jest dodanie `"HAPROXY_GROUP": "external"` wpis tutaj jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="8bdbf-123">You need to add a `"HAPROXY_GROUP": "external"` entry here as shown below.</span></span>
<span data-ttu-id="8bdbf-124">Po kliknięciu **wdrażać zmiany**, ponownym uruchomieniu kontenera.</span><span class="sxs-lookup"><span data-stu-id="8bdbf-124">Once you click **Deploy changes**, your container restarts.</span></span>

![ELK5](./media/container-service-monitoring-elk/elk5.PNG)


<span data-ttu-id="8bdbf-126">Aby sprawdzić, czy Kibana jest zarejestrowany jako usługa na pulpicie nawigacyjnym HAPROXY, należy otworzyć port 9090 w klastrze agenta, ponieważ HAPROXY działa na porcie 9090.</span><span class="sxs-lookup"><span data-stu-id="8bdbf-126">If you want to verify that Kibana is registered as a service in the HAPROXY dashboard, you need to open port 9090 on the agent cluster as HAPROXY runs on port 9090.</span></span>
<span data-ttu-id="8bdbf-127">Domyślnie, możemy otworzyć porty 80, 8080 i 443 w klastrze DC/OS agenta.</span><span class="sxs-lookup"><span data-stu-id="8bdbf-127">By default, we open ports 80, 8080, and 443 in the DC/OS agent cluster.</span></span>
<span data-ttu-id="8bdbf-128">Podano instrukcje dotyczące otwierania portu i podaj publiczny oceny [tutaj](container-service-enable-public-access.md).</span><span class="sxs-lookup"><span data-stu-id="8bdbf-128">Instructions to open a port and provide public assess are provided [here](container-service-enable-public-access.md).</span></span>

<span data-ttu-id="8bdbf-129">Aby uzyskać dostęp do pulpitu nawigacyjnego HAPROXY, otwórz interfejsu administracyjnego warstwa Marathon-LB w: `http://$PUBLIC_NODE_IP_ADDRESS:9090/haproxy?stats`.</span><span class="sxs-lookup"><span data-stu-id="8bdbf-129">To access the HAPROXY dashboard, open the Marathon-LB admin interface at: `http://$PUBLIC_NODE_IP_ADDRESS:9090/haproxy?stats`.</span></span>
<span data-ttu-id="8bdbf-130">Po przejściu do adresu URL, powinien zostać wyświetlony pulpit nawigacyjny HAPROXY w sposób przedstawiony poniżej i powinna być widoczna dla Kibana wpisu usługi.</span><span class="sxs-lookup"><span data-stu-id="8bdbf-130">Once you navigate to the URL, you should see the HAPROXY dashboard as shown below and you should see a service entry for Kibana.</span></span>

![ELK6](./media/container-service-monitoring-elk/elk6.PNG)


<span data-ttu-id="8bdbf-132">Do uzyskiwania dostępu Kibana pulpitu nawigacyjnego, który jest wdrażana na porcie 5601, należy otworzyć port 5601.</span><span class="sxs-lookup"><span data-stu-id="8bdbf-132">To access the Kibana dashboard, which is deployed on port 5601, you need to open port 5601.</span></span> <span data-ttu-id="8bdbf-133">Postępuj zgodnie z instrukcjami [tutaj](container-service-enable-public-access.md).</span><span class="sxs-lookup"><span data-stu-id="8bdbf-133">Follow instructions [here](container-service-enable-public-access.md).</span></span> <span data-ttu-id="8bdbf-134">Następnie otwórz pulpit nawigacyjny Kibana w: `http://localhost:5601`.</span><span class="sxs-lookup"><span data-stu-id="8bdbf-134">Then open the Kibana dashboard at: `http://localhost:5601`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8bdbf-135">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="8bdbf-135">Next steps</span></span>

* <span data-ttu-id="8bdbf-136">Dla dziennika systemu i aplikacji przekazywania i ustawień, zobacz [zarządzanie dziennikiem w DC/OS z ŁOSI](https://docs.mesosphere.com/1.8/administration/logging/elk/).</span><span class="sxs-lookup"><span data-stu-id="8bdbf-136">For system and application log forwarding and setup, see [Log Management in DC/OS with ELK](https://docs.mesosphere.com/1.8/administration/logging/elk/).</span></span>

* <span data-ttu-id="8bdbf-137">Aby filtrować dzienników, zobacz [filtrowania dzienniki z ŁOSI](https://docs.mesosphere.com/1.8/administration/logging/filter-elk/).</span><span class="sxs-lookup"><span data-stu-id="8bdbf-137">To filter logs, see [Filtering Logs with ELK](https://docs.mesosphere.com/1.8/administration/logging/filter-elk/).</span></span> 

 

