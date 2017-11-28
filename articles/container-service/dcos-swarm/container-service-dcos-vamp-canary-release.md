---
title: Wersja aaaCanary z Vamp w klastrze Azure DC/OS | Dokumentacja firmy Microsoft
description: "Jak toouse Vamp toocanary wersji usług i zastosować filtrowanie w klastrze usługi kontenera platformy Azure DC/OS inteligentne ruchu"
services: container-service
author: gggina
manager: rasquill
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 04/17/2017
ms.author: rasquill
ms.custom: mvc
ms.openlocfilehash: e7b8658a161a7cddcf718e3e1c12a889a330d3d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="canary-release-microservices-with-vamp-on-an-azure-container-service-dcos-cluster"></a><span data-ttu-id="d4ef9-103">Mikrousług mozgi wersji z Vamp w klastrze usługi kontenera platformy Azure DC/OS</span><span class="sxs-lookup"><span data-stu-id="d4ef9-103">Canary release microservices with Vamp on an Azure Container Service DC/OS cluster</span></span>

<span data-ttu-id="d4ef9-104">W tym przewodniku skonfigurujemy Vamp na usługi kontenera platformy Azure z klastrem DC/OS.</span><span class="sxs-lookup"><span data-stu-id="d4ef9-104">In this walkthrough, we set up Vamp on Azure Container Service with a DC/OS cluster.</span></span> <span data-ttu-id="d4ef9-105">Możemy mozgi Zwolnij hello Vamp pokaz usługi "sava", a następnie Rozwiąż niezgodności hello usługi z przeglądarki Firefox, stosując filtrowanie ruchu inteligentne.</span><span class="sxs-lookup"><span data-stu-id="d4ef9-105">We canary release hello Vamp demo service "sava", and then resolve an incompatibility of hello service with Firefox by applying smart traffic filtering.</span></span> 

> [!TIP] 
> <span data-ttu-id="d4ef9-106">W tym przewodniku Vamp działa w klastrze DC/OS, ale umożliwia także Vamp z Kubernetes jako hello orchestrator.</span><span class="sxs-lookup"><span data-stu-id="d4ef9-106">In this walkthrough Vamp runs on a DC/OS cluster, but you can also use Vamp with Kubernetes as hello orchestrator.</span></span>
>

## <a name="about-canary-releases-and-vamp"></a><span data-ttu-id="d4ef9-107">Temat element canary zwalnia i Vamp</span><span class="sxs-lookup"><span data-stu-id="d4ef9-107">About canary releases and Vamp</span></span>


<span data-ttu-id="d4ef9-108">[Zwalnianie mozgi](https://martinfowler.com/bliki/CanaryRelease.html) jest stosowane przez innowacyjnych organizacjami, takimi jak Netflix, Facebook i serwis Spotify strategii wdrażania inteligentne.</span><span class="sxs-lookup"><span data-stu-id="d4ef9-108">[Canary releasing](https://martinfowler.com/bliki/CanaryRelease.html) is a smart deployment strategy adopted by innovative organizations like Netflix, Facebook, and Spotify.</span></span> <span data-ttu-id="d4ef9-109">Jest to sens, ponieważ zmniejsza problemy, wprowadza bezpieczeństwa sieci i zwiększa innowacji podejście.</span><span class="sxs-lookup"><span data-stu-id="d4ef9-109">It’s an approach that makes sense, because it reduces issues, introduces safety-nets, and increases innovation.</span></span> <span data-ttu-id="d4ef9-110">Dlaczego nie wszystkie firmy przy użyciu go?</span><span class="sxs-lookup"><span data-stu-id="d4ef9-110">So why aren’t all companies using it?</span></span> <span data-ttu-id="d4ef9-111">Rozszerzanie tooinclude potoku CI/CD mozgi strategii dodaje złożoność i wymaga devops dużej wiedzy i doświadczenia.</span><span class="sxs-lookup"><span data-stu-id="d4ef9-111">Extending a CI/CD pipeline tooinclude canary strategies adds complexity, and requires extensive devops knowledge and experience.</span></span> <span data-ttu-id="d4ef9-112">To za mało tooblock mniejszych firmami i przedsiębiorstwami podobne przed ich nawet rozpocząć pracę.</span><span class="sxs-lookup"><span data-stu-id="d4ef9-112">That’s enough tooblock smaller companies and enterprises alike before they even get started.</span></span> 

<span data-ttu-id="d4ef9-113">[Vamp](http://vamp.io/) jest tooease systemu open source przeznaczona ten proces przejścia i przełączyć mozgi zwolnić harmonogramu kontenera tooyour preferowany funkcji.</span><span class="sxs-lookup"><span data-stu-id="d4ef9-113">[Vamp](http://vamp.io/) is an open-source system designed tooease this transition and bring canary releasing features tooyour preferred container scheduler.</span></span> <span data-ttu-id="d4ef9-114">Funkcje mozgi vamp firmy wykracza poza wdrożeniach opartych na procentach.</span><span class="sxs-lookup"><span data-stu-id="d4ef9-114">Vamp’s canary functionality goes beyond percentage-based rollouts.</span></span> <span data-ttu-id="d4ef9-115">Można filtrować ruch i podziału na szeroki zakres warunków, na przykład tootarget określonych użytkowników, zakresy adresów IP lub urządzeń.</span><span class="sxs-lookup"><span data-stu-id="d4ef9-115">Traffic can be filtered and split on a wide range of conditions, for example tootarget specific users, IP-ranges, or devices.</span></span> <span data-ttu-id="d4ef9-116">Vamp śledzi i analizuje metryki wydajności, co pozwala na automatyzację na podstawie danych rzeczywistych.</span><span class="sxs-lookup"><span data-stu-id="d4ef9-116">Vamp tracks and analyzes performance metrics, allowing for automation based on real-world data.</span></span> <span data-ttu-id="d4ef9-117">Konfigurowanie automatycznego wycofywania na błędy lub skalować wariantów pojedynczej usługi na podstawie obciążenia lub opóźnienia.</span><span class="sxs-lookup"><span data-stu-id="d4ef9-117">You can set up automatic rollback on errors, or scale individual service variants based on load or latency.</span></span>

## <a name="set-up-azure-container-service-with-dcos"></a><span data-ttu-id="d4ef9-118">Konfigurowanie usługi kontenera platformy Azure z DC/OS</span><span class="sxs-lookup"><span data-stu-id="d4ef9-118">Set up Azure Container Service with DC/OS</span></span>



1. <span data-ttu-id="d4ef9-119">[Wdrażanie klastra DC/OS](container-service-deployment.md) jeden z nich i dwaj agenci domyślny rozmiar.</span><span class="sxs-lookup"><span data-stu-id="d4ef9-119">[Deploy a DC/OS cluster](container-service-deployment.md) with one master and two agents of default size.</span></span> 

2. <span data-ttu-id="d4ef9-120">[Tworzenie tunelu SSH](../container-service-connect.md) klastra DC/OS toohello tooconnect.</span><span class="sxs-lookup"><span data-stu-id="d4ef9-120">[Create an SSH tunnel](../container-service-connect.md) tooconnect toohello DC/OS cluster.</span></span> <span data-ttu-id="d4ef9-121">W tym artykule przyjęto założenie, że tunelowania toohello klastra lokalnego portu 80.</span><span class="sxs-lookup"><span data-stu-id="d4ef9-121">This article assumes that you tunnel toohello cluster on local port 80.</span></span>


## <a name="set-up-vamp"></a><span data-ttu-id="d4ef9-122">Konfigurowanie Vamp</span><span class="sxs-lookup"><span data-stu-id="d4ef9-122">Set up Vamp</span></span>

<span data-ttu-id="d4ef9-123">Teraz, gdy masz uruchomiony klastra DC/OS Vamp można zainstalować z hello interfejsu użytkownika DC/OS (http://localhost:80).</span><span class="sxs-lookup"><span data-stu-id="d4ef9-123">Now that you have a running DC/OS cluster, you can install Vamp from hello DC/OS UI (http://localhost:80).</span></span> 

![Interfejs użytkownika platformy DC/OS](./media/container-service-dcos-vamp-canary-release/01_set_up_vamp.png)

<span data-ttu-id="d4ef9-125">Instalacja jest przeprowadzana w dwóch etapach:</span><span class="sxs-lookup"><span data-stu-id="d4ef9-125">Installation is done in two stages:</span></span>

1. <span data-ttu-id="d4ef9-126">**Wdrażanie Elasticsearch**.</span><span class="sxs-lookup"><span data-stu-id="d4ef9-126">**Deploy Elasticsearch**.</span></span>

2. <span data-ttu-id="d4ef9-127">Następnie **wdrażanie Vamp** instalując hello Vamp DC/OS universe pakietu.</span><span class="sxs-lookup"><span data-stu-id="d4ef9-127">Then **deploy Vamp** by installing hello Vamp DC/OS universe package.</span></span>

### <a name="deploy-elasticsearch"></a><span data-ttu-id="d4ef9-128">Wdrażanie Elasticsearch</span><span class="sxs-lookup"><span data-stu-id="d4ef9-128">Deploy Elasticsearch</span></span>

<span data-ttu-id="d4ef9-129">Vamp wymaga Elasticsearch zbierania metryk i agregacji.</span><span class="sxs-lookup"><span data-stu-id="d4ef9-129">Vamp requires Elasticsearch for metrics collection and aggregation.</span></span> <span data-ttu-id="d4ef9-130">Można użyć hello [obrazy usługi Docker magneticio](https://hub.docker.com/r/magneticio/elastic/) toodeploy zgodne stosu Vamp Elasticsearch.</span><span class="sxs-lookup"><span data-stu-id="d4ef9-130">You can use hello [magneticio Docker images](https://hub.docker.com/r/magneticio/elastic/) toodeploy a compatible Vamp Elasticsearch stack.</span></span>

1. <span data-ttu-id="d4ef9-131">W hello interfejsu użytkownika DC/OS, przejdź do pozycji zbyt**usług** i kliknij przycisk **wdrażanie usługi**.</span><span class="sxs-lookup"><span data-stu-id="d4ef9-131">In hello DC/OS UI, go too**Services** and click **Deploy Service**.</span></span>

2. <span data-ttu-id="d4ef9-132">Wybierz **tryb JSON** z hello **wdrożenia nowej usługi** wyskakujących.</span><span class="sxs-lookup"><span data-stu-id="d4ef9-132">Select **JSON mode** from hello **Deploy New Service** pop-up.</span></span>

  ![Wybierz tryb JSON](./media/container-service-dcos-vamp-canary-release/02_deploy_service_json_mode.png)

3. <span data-ttu-id="d4ef9-134">Wklej hello następującego formatu JSON.</span><span class="sxs-lookup"><span data-stu-id="d4ef9-134">Paste in hello following JSON.</span></span> <span data-ttu-id="d4ef9-135">Ta konfiguracja jest uruchamiany kontenera hello z 1 GB pamięci RAM i sprawdzenie kondycji podstawowe na porcie Elasticsearch hello.</span><span class="sxs-lookup"><span data-stu-id="d4ef9-135">This configuration runs hello container with 1 GB of RAM and a basic health check on hello Elasticsearch port.</span></span>
  
  ```JSON
  {
    "id": "elasticsearch",
    "instances": 1,
    "cpus": 0.2,
    "mem": 1024.0,
    "container": {
      "docker": {
        "image": "magneticio/elastic:2.2",
        "network": "HOST",
        "forcePullImage": true
      }
    },
    "healthChecks": [
      {
        "protocol": "TCP",
        "gracePeriodSeconds": 30,
        "intervalSeconds": 10,
        "timeoutSeconds": 5,
        "port": 9200,
        "maxConsecutiveFailures": 0
      }
    ]
  }
  ```
  

3. <span data-ttu-id="d4ef9-136">Kliknij przycisk **wdrażanie**.</span><span class="sxs-lookup"><span data-stu-id="d4ef9-136">Click **Deploy**.</span></span>

  <span data-ttu-id="d4ef9-137">DC/OS wdraża hello Elasticsearch kontenera.</span><span class="sxs-lookup"><span data-stu-id="d4ef9-137">DC/OS deploys hello Elasticsearch container.</span></span> <span data-ttu-id="d4ef9-138">Możesz śledzić postępy na powitania **usług** strony.</span><span class="sxs-lookup"><span data-stu-id="d4ef9-138">You can track progress on hello **Services** page.</span></span>  

  ![Wdrażanie e? Elasticsearch](./media/container-service-dcos-vamp-canary-release/03_deply_elasticsearch.png)

### <a name="deploy-vamp"></a><span data-ttu-id="d4ef9-140">Wdrażanie Vamp</span><span class="sxs-lookup"><span data-stu-id="d4ef9-140">Deploy Vamp</span></span>

<span data-ttu-id="d4ef9-141">Po Elasticsearch raporty jako **systemem**, można dodać hello Vamp Universe DC/OS pakietu.</span><span class="sxs-lookup"><span data-stu-id="d4ef9-141">Once Elasticsearch reports as **Running**, you can add hello Vamp DC/OS Universe package.</span></span> 

1. <span data-ttu-id="d4ef9-142">Przejdź za**Universe** i wyszukaj **vamp**.</span><span class="sxs-lookup"><span data-stu-id="d4ef9-142">Go too**Universe** and search for **vamp**.</span></span> 
  <span data-ttu-id="d4ef9-143">![Vamp na universe DC/OS](./media/container-service-dcos-vamp-canary-release/04_universe_deploy_vamp.png)</span><span class="sxs-lookup"><span data-stu-id="d4ef9-143">![Vamp on DC/OS universe](./media/container-service-dcos-vamp-canary-release/04_universe_deploy_vamp.png)</span></span>

2. <span data-ttu-id="d4ef9-144">Kliknij przycisk **zainstalować** toohello dalej vamp pakietu, a następnie wybierz pozycję **zaawansowane instalacji**.</span><span class="sxs-lookup"><span data-stu-id="d4ef9-144">Click **install** next toohello vamp package, and choose **Advanced Installation**.</span></span>

3. <span data-ttu-id="d4ef9-145">Przewiń w dół, a następnie wprowadź hello następującego adresu url elasticsearch: `http://elasticsearch.marathon.mesos:9200`.</span><span class="sxs-lookup"><span data-stu-id="d4ef9-145">Scroll down and enter hello following elasticsearch-url: `http://elasticsearch.marathon.mesos:9200`.</span></span> 

  ![Wprowadź adres URL Elasticsearch](./media/container-service-dcos-vamp-canary-release/05_universe_elasticsearch_url.png)

4. <span data-ttu-id="d4ef9-147">Kliknij przycisk **Przejrzyj i zainstaluj**, następnie kliknij przycisk **zainstalować** toostart hello wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="d4ef9-147">Click **Review and Install**, then click **Install** toostart hello deployment.</span></span>  

  <span data-ttu-id="d4ef9-148">DC/OS wdraża wszystkich wymaganych składników Vamp.</span><span class="sxs-lookup"><span data-stu-id="d4ef9-148">DC/OS deploys all required Vamp components.</span></span> <span data-ttu-id="d4ef9-149">Możesz śledzić postępy na powitania **usług** strony.</span><span class="sxs-lookup"><span data-stu-id="d4ef9-149">You can track progress on hello **Services** page.</span></span>
  
  ![Wdrażanie Vamp jako pakiet universe](./media/container-service-dcos-vamp-canary-release/06_deploy_vamp.png)
  
5. <span data-ttu-id="d4ef9-151">Po zakończeniu wdrażania, aby dostęp do hello Vamp interfejsu użytkownika:</span><span class="sxs-lookup"><span data-stu-id="d4ef9-151">Once deployment has completed, you can access hello Vamp UI:</span></span>

  ![Usługa vamp na DC/OS](./media/container-service-dcos-vamp-canary-release/07_deploy_vamp_complete.png)
  
  ![Vamp interfejsu użytkownika](./media/container-service-dcos-vamp-canary-release/08_vamp_ui.png)


## <a name="deploy-your-first-service"></a><span data-ttu-id="d4ef9-154">Wdrażanie w ramach pierwszej usługi</span><span class="sxs-lookup"><span data-stu-id="d4ef9-154">Deploy your first service</span></span>

<span data-ttu-id="d4ef9-155">Teraz tego Vamp jest uruchomiona, należy wdrożyć usługę z planu.</span><span class="sxs-lookup"><span data-stu-id="d4ef9-155">Now that Vamp is up and running, deploy a service from a blueprint.</span></span> 

<span data-ttu-id="d4ef9-156">W najprostszej postaci [planu Vamp](http://vamp.io/documentation/using-vamp/blueprints/) opisuje hello punktów końcowych (bramy), klastrami i toodeploy usług.</span><span class="sxs-lookup"><span data-stu-id="d4ef9-156">In its simplest form, a [Vamp blueprint](http://vamp.io/documentation/using-vamp/blueprints/) describes hello endpoints (gateways), clusters, and services toodeploy.</span></span> <span data-ttu-id="d4ef9-157">Vamp używa klastrów toogroup różnych wariantów hello same usługi na grupy logiczne mozgi zwalniania lub A / B testowania.</span><span class="sxs-lookup"><span data-stu-id="d4ef9-157">Vamp uses clusters toogroup different variants of hello same service into logical groups for canary releasing or A/B testing.</span></span>  

<span data-ttu-id="d4ef9-158">W tym scenariuszu przykładowej aplikacji wbudowanymi o nazwie [ **sava**](https://github.com/magneticio/sava), które jest w wersji 1.0.</span><span class="sxs-lookup"><span data-stu-id="d4ef9-158">This scenario uses a sample monolithic application called [**sava**](https://github.com/magneticio/sava), which is at version 1.0.</span></span> <span data-ttu-id="d4ef9-159">monolityczna Hello jest spakowany w kontenerze Docker, który znajduje się w Centrum Docker w obszarze magneticio/sava:1.0.0.</span><span class="sxs-lookup"><span data-stu-id="d4ef9-159">hello monolith is packaged in a Docker container, which is in Docker Hub under magneticio/sava:1.0.0.</span></span> <span data-ttu-id="d4ef9-160">Aplikacja Hello jest uruchamiana normalnie portu 8080, ale ma tooexpose 9050 go w porcie w takim przypadku.</span><span class="sxs-lookup"><span data-stu-id="d4ef9-160">hello app normally runs on port 8080, but you want tooexpose it under port 9050 in this case.</span></span> <span data-ttu-id="d4ef9-161">Wdrażanie aplikacji hello za pośrednictwem Vamp przy użyciu prostego planu.</span><span class="sxs-lookup"><span data-stu-id="d4ef9-161">Deploy hello app through Vamp using a simple blueprint.</span></span>

1. <span data-ttu-id="d4ef9-162">Przejdź za**wdrożeń**.</span><span class="sxs-lookup"><span data-stu-id="d4ef9-162">Go too**Deployments**.</span></span>

2. <span data-ttu-id="d4ef9-163">Kliknij pozycję **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="d4ef9-163">Click **Add**.</span></span>

3. <span data-ttu-id="d4ef9-164">Wklej w hello następującego planu yaml programu.</span><span class="sxs-lookup"><span data-stu-id="d4ef9-164">Paste in hello following blueprint YAML.</span></span> <span data-ttu-id="d4ef9-165">Ten plan zawiera jednego klastra z tylko jedną usługę variant, który możemy zmienić w późniejszym kroku:</span><span class="sxs-lookup"><span data-stu-id="d4ef9-165">This blueprint contains one cluster with only one service variant, which we change in a later step:</span></span>

  ```YAML
  name: sava                        # deployment name
  gateways:
    9050: sava_cluster/webport      # stable endpoint
  clusters:
    sava_cluster:               # cluster toocreate
     services:
        -
          breed:
            name: sava:1.0.0        # service variant name
            deployable: magneticio/sava:1.0.0
            ports:
              webport: 8080/http # cluster endpoint, used for canary releasing
  ```

4. <span data-ttu-id="d4ef9-166">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="d4ef9-166">Click **Save**.</span></span> <span data-ttu-id="d4ef9-167">Vamp inicjuje hello wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="d4ef9-167">Vamp initiates hello deployment.</span></span>

<span data-ttu-id="d4ef9-168">Witaj wdrożenia znajduje się na powitania **wdrożeń** strony.</span><span class="sxs-lookup"><span data-stu-id="d4ef9-168">hello deployment is listed on hello **Deployments** page.</span></span> <span data-ttu-id="d4ef9-169">Kliknij przycisk toomonitor wdrożenia hello jego stan.</span><span class="sxs-lookup"><span data-stu-id="d4ef9-169">Click hello deployment toomonitor its status.</span></span>

![Vamp interfejsu użytkownika — wdrażanie sava](./media/container-service-dcos-vamp-canary-release/09_sava100.png)

![Usługa sava w Vamp interfejsu użytkownika](./media/container-service-dcos-vamp-canary-release/09a_sava100.png)

<span data-ttu-id="d4ef9-172">Bramy są tworzone, które są wymienione na powitania **bram** strony:</span><span class="sxs-lookup"><span data-stu-id="d4ef9-172">Two gateways are created, which are listed on hello **Gateways** page:</span></span>

* <span data-ttu-id="d4ef9-173">Witaj tooaccess stabilna punktu końcowego, usługą (port 9050)</span><span class="sxs-lookup"><span data-stu-id="d4ef9-173">a stable endpoint tooaccess hello running service (port 9050)</span></span> 
* <span data-ttu-id="d4ef9-174">zarządzane Vamp wewnętrzny bramy (więcej informacji na temat tej bramy później).</span><span class="sxs-lookup"><span data-stu-id="d4ef9-174">a Vamp-managed internal gateway (more on this gateway later).</span></span> 

![Vamp interfejsu użytkownika — sava bram](./media/container-service-dcos-vamp-canary-release/10_vamp_sava_gateways.png)

<span data-ttu-id="d4ef9-176">teraz wdrożono Hello sava usługi, ale nie masz dostępu do jego zewnętrznie ponieważ hello modułu równoważenia obciążenia Azure nie może ustalić tooit ruchu tooforward jeszcze.</span><span class="sxs-lookup"><span data-stu-id="d4ef9-176">hello sava service has now deployed, but you can’t access it externally because hello Azure Load Balancer doesn’t know tooforward traffic tooit yet.</span></span> <span data-ttu-id="d4ef9-177">tooaccess hello usługi aktualizacji hello Azure konfiguracji sieci.</span><span class="sxs-lookup"><span data-stu-id="d4ef9-177">tooaccess hello service, update hello Azure networking configuration.</span></span>


## <a name="update-hello-azure-network-configuration"></a><span data-ttu-id="d4ef9-178">Zaktualizuj konfigurację sieci platformy Azure hello</span><span class="sxs-lookup"><span data-stu-id="d4ef9-178">Update hello Azure network configuration</span></span>

<span data-ttu-id="d4ef9-179">Usługa sava hello vamp wdrożonych na węzłach agenta DC/OS hello udostępnianie stabilna punktu końcowego w porcie 9050.</span><span class="sxs-lookup"><span data-stu-id="d4ef9-179">Vamp deployed hello sava service on hello DC/OS agent nodes, exposing a stable endpoint at port 9050.</span></span> <span data-ttu-id="d4ef9-180">Usługa hello tooaccess z poza hello klastra DC/OS, tworzy powitania po konfiguracji sieci Azure toohello zmiany we wdrożeniu klastra:</span><span class="sxs-lookup"><span data-stu-id="d4ef9-180">tooaccess hello service from outside hello DC/OS cluster, make hello following changes toohello Azure network configuration in your cluster deployment:</span></span> 

1. <span data-ttu-id="d4ef9-181">**Skonfiguruj hello modułu równoważenia obciążenia Azure** hello agentów (hello zasób o nazwie **dcos-agent-lb-xxxx**) z sondy kondycji i ruchu tooforward reguły portu 9050 toohello sava wystąpień.</span><span class="sxs-lookup"><span data-stu-id="d4ef9-181">**Configure hello Azure Load Balancer** for hello agents (hello resource named **dcos-agent-lb-xxxx**) with a health probe and a rule tooforward traffic on port 9050 toohello sava instances.</span></span> 

2. <span data-ttu-id="d4ef9-182">**Grupy zabezpieczeń sieci hello aktualizacji** dla agentów publicznych hello (hello zasób o nazwie **XXXX-agent publicznego nsg-XXXX**) tooallow ruch na porcie 9050.</span><span class="sxs-lookup"><span data-stu-id="d4ef9-182">**Update hello network security group** for hello public agents (hello resource named **XXXX-agent-public-nsg-XXXX**) tooallow traffic on port 9050.</span></span>

<span data-ttu-id="d4ef9-183">Aby uzyskać szczegółowy opis kroków toocomplete tych zadań za pomocą hello Azure portalu, zobacz [włączyć aplikacji usługi kontenera platformy Azure tooan dostępu publicznego](container-service-enable-public-access.md).</span><span class="sxs-lookup"><span data-stu-id="d4ef9-183">For detailed steps toocomplete these tasks using hello Azure portal, see [Enable public access tooan Azure Container Service application](container-service-enable-public-access.md).</span></span> <span data-ttu-id="d4ef9-184">Określ port 9050 dla wszystkich ustawień portu.</span><span class="sxs-lookup"><span data-stu-id="d4ef9-184">Specify port 9050 for all port settings.</span></span>


<span data-ttu-id="d4ef9-185">Po utworzeniu wszystko Przejdź toohello **omówienie** bloku hello modułu równoważenia obciążenia agenta DC/OS (hello zasób o nazwie **dcos-agent-lb-xxxx**).</span><span class="sxs-lookup"><span data-stu-id="d4ef9-185">Once everything has been created, go toohello **Overview** blade of hello DC/OS agent load balancer (hello resource named **dcos-agent-lb-xxxx**).</span></span> <span data-ttu-id="d4ef9-186">Znajdź hello **publicznego adresu IP**i użyj hello adres tooaccess sava w porcie 9050.</span><span class="sxs-lookup"><span data-stu-id="d4ef9-186">Find hello **Public IP address**, and use hello address tooaccess sava at port 9050.</span></span>

![Portal Azure — Pobierz publiczny adres IP](./media/container-service-dcos-vamp-canary-release/18_public_ip_address.png)

![sava](./media/container-service-dcos-vamp-canary-release/19_sava100.png)


## <a name="run-a-canary-release"></a><span data-ttu-id="d4ef9-189">Uruchom mozgi zlecenia</span><span class="sxs-lookup"><span data-stu-id="d4ef9-189">Run a canary release</span></span>

<span data-ttu-id="d4ef9-190">Załóżmy, że masz nową wersję tej aplikacji, które mają toocanary wydania do produkcji.</span><span class="sxs-lookup"><span data-stu-id="d4ef9-190">Suppose you have a new version of this application that you want toocanary release into production.</span></span> <span data-ttu-id="d4ef9-191">Została ona konteneryzowanych jako magneticio/sava:1.1.0 i są gotowe toogo.</span><span class="sxs-lookup"><span data-stu-id="d4ef9-191">You have it containerized as magneticio/sava:1.1.0 and are ready toogo.</span></span> <span data-ttu-id="d4ef9-192">Vamp umożliwia łatwe dodawanie nowych toohello usługi uruchamiania wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="d4ef9-192">Vamp lets you easily add new services toohello running deployment.</span></span> <span data-ttu-id="d4ef9-193">Te usługi "scalonych" są wdrożone równolegle z istniejącymi usługami hello w klastrze hello i przypisano wagę % 0.</span><span class="sxs-lookup"><span data-stu-id="d4ef9-193">These "merged" services are deployed alongside hello existing services in hello cluster, and assigned a weight of 0%.</span></span> <span data-ttu-id="d4ef9-194">Żaden ruch jest kierowany tooa nowo scalić usługi dostosować hello Dystrybucja ruchu.</span><span class="sxs-lookup"><span data-stu-id="d4ef9-194">No traffic is routed tooa newly merged service until you adjust hello traffic distribution.</span></span> <span data-ttu-id="d4ef9-195">suwak wagi Hello w hello Vamp interfejsu użytkownika umożliwia pełną kontrolę nad dystrybucji hello, umożliwiające przyrostowe dostosowań (wersja mozgi) lub błyskawicznych wycofywania.</span><span class="sxs-lookup"><span data-stu-id="d4ef9-195">hello weight slider in hello Vamp UI gives you complete control over hello distribution, allowing for incremental adjustments (canary release) or an instant rollback.</span></span>

### <a name="merge-a-new-service-variant"></a><span data-ttu-id="d4ef9-196">Scal nowy wariant usługi</span><span class="sxs-lookup"><span data-stu-id="d4ef9-196">Merge a new service variant</span></span>

<span data-ttu-id="d4ef9-197">toomerge hello nowej sava 1.1 usługi z hello systemem wdrażania:</span><span class="sxs-lookup"><span data-stu-id="d4ef9-197">toomerge hello new sava 1.1 service with hello running deployment:</span></span>

1. <span data-ttu-id="d4ef9-198">W hello Vamp interfejsu użytkownika, kliknij przycisk **plany**.</span><span class="sxs-lookup"><span data-stu-id="d4ef9-198">In hello Vamp UI, click **Blueprints**.</span></span>

2. <span data-ttu-id="d4ef9-199">Kliknij przycisk **Dodaj** i Wklej w hello następującego planu yaml programu: ten plan zawiera opis nowych toodeploy variant (sava: 1.1.0) usługi w istniejącym klastrze hello (sava_cluster).</span><span class="sxs-lookup"><span data-stu-id="d4ef9-199">Click **Add** and paste in hello following blueprint YAML: This blueprint describes a new service variant (sava:1.1.0) toodeploy within hello existing cluster (sava_cluster).</span></span>

  ```YAML
  name: sava:1.1.0      # blueprint name
  clusters:
    sava_cluster:       # cluster tooupdate
      services:
        -
          breed:
            name: sava:1.1.0    # service variant name
            deployable: magneticio/sava:1.1.0    
            ports:
              webport: 8080/http # cluster endpoint tooupdate
  ```
  
3. <span data-ttu-id="d4ef9-200">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="d4ef9-200">Click **Save**.</span></span> <span data-ttu-id="d4ef9-201">Plan Hello są przechowywane i wyświetlane na powitania **plany** strony.</span><span class="sxs-lookup"><span data-stu-id="d4ef9-201">hello blueprint is stored and listed on hello **Blueprints** page.</span></span>

4. <span data-ttu-id="d4ef9-202">Menu Akcja Otwórz hello na powitania sava: 1.1 planu, a następnie kliknij przycisk **scalić**.</span><span class="sxs-lookup"><span data-stu-id="d4ef9-202">Open hello action menu on hello sava:1.1 blueprint and click **Merge to**.</span></span>

  ![Vamp interfejsu użytkownika — plany](./media/container-service-dcos-vamp-canary-release/20_sava110_mergeto.png)

5. <span data-ttu-id="d4ef9-204">Wybierz hello **sava** wdrożenia i kliknij przycisk **scalania**.</span><span class="sxs-lookup"><span data-stu-id="d4ef9-204">Select hello **sava** deployment and click **Merge**.</span></span>

  ![Vamp interfejsu użytkownika — scalania toodeployment planu](./media/container-service-dcos-vamp-canary-release/21_sava110_merge.png)

<span data-ttu-id="d4ef9-206">Vamp wdraża hello nowy sava: 1.1.0 usługi wariant opisanego w plan hello obok sava: 1.0.0 w hello **sava_cluster** z hello uruchamiania wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="d4ef9-206">Vamp deploys hello new sava:1.1.0 service variant described in hello blueprint alongside sava:1.0.0 in hello **sava_cluster** of hello running deployment.</span></span> 

![Vamp interfejsu użytkownika — wdrażania sava aktualizacji](./media/container-service-dcos-vamp-canary-release/22_sava_cluster.png)

<span data-ttu-id="d4ef9-208">Witaj **sava/sava_cluster/webport** bramy (punktu końcowego klastra hello) zostaje również zaktualizowany, dodawanie toohello trasy nowo wdrożone sava: 1.1.0.</span><span class="sxs-lookup"><span data-stu-id="d4ef9-208">hello **sava/sava_cluster/webport** gateway (hello cluster endpoint) is also updated, adding a route toohello newly deployed sava:1.1.0.</span></span> <span data-ttu-id="d4ef9-209">W tym momencie nie ruch jest przekierowywany tutaj (hello **wagi** ustawiono too0%).</span><span class="sxs-lookup"><span data-stu-id="d4ef9-209">At this point, no traffic is routed here (hello **WEIGHT** is set too0%).</span></span>

![Vamp interfejsu użytkownika — klastra bramy](./media/container-service-dcos-vamp-canary-release/23_sava_cluster_webport.png)

### <a name="canary-release"></a><span data-ttu-id="d4ef9-211">Mozgi zlecenia</span><span class="sxs-lookup"><span data-stu-id="d4ef9-211">Canary release</span></span>

<span data-ttu-id="d4ef9-212">Obie wersje sava wdrożone w hello sam klastra, dostosować hello Dystrybucja ruchu między nimi za pomocą przenoszenia hello **wagi** suwaka.</span><span class="sxs-lookup"><span data-stu-id="d4ef9-212">With both versions of sava deployed in hello same cluster, adjust hello distribution of traffic between them by moving hello **WEIGHT** slider.</span></span>

1. <span data-ttu-id="d4ef9-213">Kliknij przycisk ![Vamp interfejsu użytkownika — Edytuj](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) dalej zbyt**wagi**.</span><span class="sxs-lookup"><span data-stu-id="d4ef9-213">Click ![Vamp UI - edit](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) next too**WEIGHT**.</span></span>

2. <span data-ttu-id="d4ef9-214">Ustaw hello wagi dystrybucji too50%/50% i kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="d4ef9-214">Set hello weight distribution too50%/50% and click **Save**.</span></span>

  ![Vamp interfejsu użytkownika — suwak wagi bramy](./media/container-service-dcos-vamp-canary-release/24_sava_cluster_webport_weight.png)

3. <span data-ttu-id="d4ef9-216">Przejdź wstecz tooyour przeglądarki i Odśwież stronę sava hello kilka razy.</span><span class="sxs-lookup"><span data-stu-id="d4ef9-216">Go back tooyour browser and refresh hello sava page a few more times.</span></span> <span data-ttu-id="d4ef9-217">Teraz aplikacja Hello sava przełącza między strony sava: 1.0 i strony sava: 1.1.</span><span class="sxs-lookup"><span data-stu-id="d4ef9-217">hello sava application now switches between a sava:1.0 page and a sava:1.1 page.</span></span>

  ![naprzemiennych sava1.0 i sava1.1 usługi](./media/container-service-dcos-vamp-canary-release/25_sava_100_101.png)


  > [!NOTE]
  > <span data-ttu-id="d4ef9-219">Tego wyrażenia warunkowe hello strony działa najlepiej z hello "Incognito" lub "Anonimowo" Tryb przeglądarki z powodu hello buforowanie zasoby statyczne.</span><span class="sxs-lookup"><span data-stu-id="d4ef9-219">This alternation of hello page works best with hello "Incognito" or “Anonymous” mode of your browser because of hello caching of static assets.</span></span>
  >

### <a name="filter-traffic"></a><span data-ttu-id="d4ef9-220">Filtrowanie ruchu</span><span class="sxs-lookup"><span data-stu-id="d4ef9-220">Filter traffic</span></span>

<span data-ttu-id="d4ef9-221">Po wdrożeniu Załóżmy, że wykrywane niezgodności w sava: 1.1.0, że powoduje problemy z wyświetlaniem w przeglądarki Firefox.</span><span class="sxs-lookup"><span data-stu-id="d4ef9-221">Suppose after deployment that you discovered an incompatibility in sava:1.1.0 that causes display problems in Firefox browsers.</span></span> <span data-ttu-id="d4ef9-222">Można ustawić ruch przychodzący toofilter Vamp i bezpośrednie, wszyscy użytkownicy Firefox kopii toohello znane stabilna sava: 1.0.0.</span><span class="sxs-lookup"><span data-stu-id="d4ef9-222">You can set Vamp toofilter incoming traffic and direct all Firefox users back toohello known stable sava:1.0.0.</span></span> <span data-ttu-id="d4ef9-223">Ten filtr natychmiast rozwiązuje hello przerw w działaniu Firefox użytkowników, gdy każdy inny nadal tooenjoy hello zalet hello zwiększona sava: 1.1.0.</span><span class="sxs-lookup"><span data-stu-id="d4ef9-223">This filter instantly resolves hello disruption for Firefox users, while everybody else continues tooenjoy hello benefits of hello improved sava:1.1.0.</span></span>

<span data-ttu-id="d4ef9-224">Vamp używa **warunki** toofilter ruch między trasy w bramy.</span><span class="sxs-lookup"><span data-stu-id="d4ef9-224">Vamp uses **conditions** toofilter traffic between routes in a gateway.</span></span> <span data-ttu-id="d4ef9-225">Ruch jest najpierw filtrowane i kierowane zgodnie z toohello warunki tooeach trasy.</span><span class="sxs-lookup"><span data-stu-id="d4ef9-225">Traffic is first filtered and directed according toohello conditions applied tooeach route.</span></span> <span data-ttu-id="d4ef9-226">Wszystkie pozostałe ruchu jest dystrybuowane zgodnie z ustawieniem wagi bramy toohello.</span><span class="sxs-lookup"><span data-stu-id="d4ef9-226">All remaining traffic is distributed according toohello gateway weight setting.</span></span>

<span data-ttu-id="d4ef9-227">Można utworzyć toofilter warunku wszyscy użytkownicy Firefox i kierowania ich toohello starego sava: 1.0.0:</span><span class="sxs-lookup"><span data-stu-id="d4ef9-227">You can create a condition toofilter all Firefox users and direct them toohello old sava:1.0.0:</span></span>

1. <span data-ttu-id="d4ef9-228">Na powitania sava/sava_cluster/webport **bram** kliknij przycisk ![Vamp interfejsu użytkownika — Edytuj](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) tooadd **WARUNKU** toohello sava/sava_cluster/sava:1.0.0/webport trasy.</span><span class="sxs-lookup"><span data-stu-id="d4ef9-228">On hello sava/sava_cluster/webport **Gateways** page, click ![Vamp UI - edit](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) tooadd a **CONDITION** toohello route sava/sava_cluster/sava:1.0.0/webport.</span></span> 

2. <span data-ttu-id="d4ef9-229">Wprowadź warunek hello **agenta użytkownika przeglądarki Firefox ==** i kliknij przycisk ![Vamp interfejsu użytkownika — Zapisz](./media/container-service-dcos-vamp-canary-release/vamp_ui_save.png).</span><span class="sxs-lookup"><span data-stu-id="d4ef9-229">Enter hello condition **user-agent == Firefox** and click ![Vamp UI - save](./media/container-service-dcos-vamp-canary-release/vamp_ui_save.png).</span></span>

  <span data-ttu-id="d4ef9-230">Vamp dodaje warunek hello siły domyślne % 0.</span><span class="sxs-lookup"><span data-stu-id="d4ef9-230">Vamp adds hello condition with a default strength of 0%.</span></span> <span data-ttu-id="d4ef9-231">filtrowanie ruchu toostart należy tooadjust hello warunku siły.</span><span class="sxs-lookup"><span data-stu-id="d4ef9-231">toostart filtering traffic, you need tooadjust hello condition strength.</span></span>

3. <span data-ttu-id="d4ef9-232">Kliknij przycisk ![Vamp interfejsu użytkownika — Edytuj](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) toochange hello **siły** stosowane toohello warunku.</span><span class="sxs-lookup"><span data-stu-id="d4ef9-232">Click ![Vamp UI - edit](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) toochange hello **STRENGTH** applied toohello condition.</span></span>
 
4. <span data-ttu-id="d4ef9-233">Zestaw hello **siły** too100% i kliknij przycisk ![Vamp interfejsu użytkownika — Zapisz](./media/container-service-dcos-vamp-canary-release/vamp_ui_save.png) toosave.</span><span class="sxs-lookup"><span data-stu-id="d4ef9-233">Set hello **STRENGTH** too100% and click ![Vamp UI - save](./media/container-service-dcos-vamp-canary-release/vamp_ui_save.png) toosave.</span></span>

  <span data-ttu-id="d4ef9-234">Vamp teraz wysyła cały ruch dopasowania hello toosava:1.0.0 warunku (wszyscy użytkownicy Firefox).</span><span class="sxs-lookup"><span data-stu-id="d4ef9-234">Vamp now sends all traffic matching hello condition (all Firefox users) toosava:1.0.0.</span></span>

  ![Vamp UI - zastosowanie toogateway warunku](./media/container-service-dcos-vamp-canary-release/26_apply_condition.png)

5. <span data-ttu-id="d4ef9-236">Na koniec należy dostosować hello bramy wagi toosend wszystkie pozostałe ruchu (wszyscy użytkownicy z systemem innym niż Firefox) toohello nowe sava: 1.1.0.</span><span class="sxs-lookup"><span data-stu-id="d4ef9-236">Finally, adjust hello gateway weight toosend all remaining traffic (all non-Firefox users) toohello new sava:1.1.0.</span></span> <span data-ttu-id="d4ef9-237">Kliknij przycisk ![Vamp interfejsu użytkownika — Edytuj](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) dalej zbyt**wagi** i ustawić dystrybucja wag hello, tak aby toohello bezpośrednie trasy sava/sava_cluster/sava:1.1.0/webport wynosi 100%.</span><span class="sxs-lookup"><span data-stu-id="d4ef9-237">Click ![Vamp UI - edit](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) next too**WEIGHT** and set hello weight distribution so 100% is directed toohello route sava/sava_cluster/sava:1.1.0/webport.</span></span>

  <span data-ttu-id="d4ef9-238">Cały ruch, które nie są filtrowane według warunku hello jest teraz ukierunkowanej toohello nowe sava: 1.1.0.</span><span class="sxs-lookup"><span data-stu-id="d4ef9-238">All traffic not filtered by hello condition is now directed toohello new sava:1.1.0.</span></span>

6. <span data-ttu-id="d4ef9-239">toosee hello filtru akcji, otwórz dwóch różnych przeglądarkach (jeden Firefox i inną przeglądarkę) i uzyskać dostępu do usługi sava hello z obu.</span><span class="sxs-lookup"><span data-stu-id="d4ef9-239">toosee hello filter in action, open two different browsers (one Firefox and one other browser) and access hello sava service from both.</span></span> <span data-ttu-id="d4ef9-240">Wszystkie żądania Firefox wysyłane toosava:1.0.0, podczas ukierunkowanych toosava:1.1.0 wszystkich innych przeglądarek.</span><span class="sxs-lookup"><span data-stu-id="d4ef9-240">All Firefox requests are sent toosava:1.0.0, while all other browsers are directed toosava:1.1.0.</span></span>

  ![Vamp interfejsu użytkownika — filtrowania ruchu](./media/container-service-dcos-vamp-canary-release/27_filter_traffic.png)

## <a name="summing-up"></a><span data-ttu-id="d4ef9-242">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="d4ef9-242">Summing up</span></span>

<span data-ttu-id="d4ef9-243">Ten artykuł został tooVamp szybkie wprowadzenie w klastrze DC/OS.</span><span class="sxs-lookup"><span data-stu-id="d4ef9-243">This article was a quick introduction tooVamp on a DC/OS cluster.</span></span> <span data-ttu-id="d4ef9-244">Po pierwsze otrzymano Vamp i systemem w sieci Azure kontenera DC/OS usługi klastra, wdrożyć usługi za pomocą planu Vamp i dostęp do niego w punkcie końcowym hello udostępniane (bramy).</span><span class="sxs-lookup"><span data-stu-id="d4ef9-244">For starters, you got Vamp up and running on your Azure Container Service DC/OS cluster, deployed a service with a Vamp blueprint, and accessed it at hello exposed endpoint (gateway).</span></span>

<span data-ttu-id="d4ef9-245">Możemy również dotknięciu na niektóre zaawansowane funkcje Vamp: scalanie nowej usługi variant toohello uruchamiania wdrożenia i wprowadzenie do przyrostowo, a następnie filtrowania ruchu tooresolve znane niezgodności.</span><span class="sxs-lookup"><span data-stu-id="d4ef9-245">We also touched on some powerful features of Vamp:  merging a new service variant toohello running deployment and introducing it incrementally, then filtering traffic tooresolve a known incompatibility.</span></span>


## <a name="next-steps"></a><span data-ttu-id="d4ef9-246">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d4ef9-246">Next steps</span></span>

* <span data-ttu-id="d4ef9-247">Więcej informacji o zarządzaniu Vamp akcji za pomocą hello [Vamp interfejsu API REST](http://vamp.io/documentation/api/api-reference/).</span><span class="sxs-lookup"><span data-stu-id="d4ef9-247">Learn about managing Vamp actions through hello [Vamp REST API](http://vamp.io/documentation/api/api-reference/).</span></span>

* <span data-ttu-id="d4ef9-248">Tworzenie skryptów automatyzacji Vamp w środowisku Node.js i uruchom je jako [Vamp przepływy pracy](http://vamp.io/documentation/tutorials/create-a-workflow/).</span><span class="sxs-lookup"><span data-stu-id="d4ef9-248">Build Vamp automation scripts in Node.js and run them as [Vamp workflows](http://vamp.io/documentation/tutorials/create-a-workflow/).</span></span>

* <span data-ttu-id="d4ef9-249">Zobacz dodatkowe [samouczki VAMP](http://vamp.io/documentation/tutorials/overview/).</span><span class="sxs-lookup"><span data-stu-id="d4ef9-249">See additional [VAMP tutorials](http://vamp.io/documentation/tutorials/overview/).</span></span>

