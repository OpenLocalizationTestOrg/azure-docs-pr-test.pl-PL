---
title: "Projekt z usługą kontenera Azure i rejestru kontenera Azure aaaUse | Dokumentacja firmy Microsoft"
description: "Tworzenie klastra usługi ACS Kubernetes i toocreate rejestru kontenera Azure pierwszej aplikacji Azure z projektu."
services: container-service
documentationcenter: 
author: squillace
manager: gamonroy
editor: 
tags: draft, helm, acs, azure-container-service
keywords: Docker, Containers, microservices, Kubernetes, Draft, Azure
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/31/2017
ms.author: rasquill
ms.custom: mvc
ms.openlocfilehash: f5e21cda01e5e8452bf86a5c8fa458904d89f451
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-draft-with-azure-container-service-and-azure-container-registry-toobuild-and-deploy-an-application-tookubernetes"></a><span data-ttu-id="0d849-104">Projekt za pomocą toobuild usługi kontenera platformy Azure i rejestru kontenera Azure i wdrażanie aplikacji tooKubernetes</span><span class="sxs-lookup"><span data-stu-id="0d849-104">Use Draft with Azure Container Service and Azure Container Registry toobuild and deploy an application tooKubernetes</span></span>

<span data-ttu-id="0d849-105">[Projekt](https://aka.ms/draft) to nowe narzędzie open source, który umożliwia łatwe toodevelop aplikacji kontenera i wdrażanie ich klastry tooKubernetes bez wiedzy o te informacje o Docker i Kubernetes — lub nawet ich zainstalowanie.</span><span class="sxs-lookup"><span data-stu-id="0d849-105">[Draft](https://aka.ms/draft) is a new open-source tool that makes it easy toodevelop container-based applications and deploy them tooKubernetes clusters without knowing much about Docker and Kubernetes -- or even installing them.</span></span> <span data-ttu-id="0d849-106">Za pomocą takich narzędzi jak projekt umożliwiają możesz i zespół zespołami tworzenie aplikacji hello z Kubernetes, nie płatności tyle tooinfrastructure uwagi.</span><span class="sxs-lookup"><span data-stu-id="0d849-106">Using tools like Draft let you and your teams focus on building hello application with Kubernetes, not paying as much attention tooinfrastructure.</span></span>

<span data-ttu-id="0d849-107">Narzędzia Draft można użyć z dowolnym rejestrem obrazów Docker i dowolnym klastrem Kubernetes, w tym lokalnym.</span><span class="sxs-lookup"><span data-stu-id="0d849-107">You can use Draft with any Docker image registry and any Kubernetes cluster, including locally.</span></span> <span data-ttu-id="0d849-108">Ten samouczek pokazuje, jak toouse ACS z toocreate Kubernetes, ACR i usługi Azure DNS na żywo developer CI/CD potoku przy użyciu wersji roboczej.</span><span class="sxs-lookup"><span data-stu-id="0d849-108">This tutorial shows how toouse ACS with Kubernetes, ACR, and Azure DNS toocreate a live CI/CD developer pipeline using Draft.</span></span>


## <a name="create-an-azure-container-registry"></a><span data-ttu-id="0d849-109">Tworzenie rejestru Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="0d849-109">Create an Azure Container Registry</span></span>
<span data-ttu-id="0d849-110">Możesz z łatwością [tworzenie nowych rejestru kontenera Azure](../../container-registry/container-registry-get-started-azure-cli.md), ale hello obejmuje następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="0d849-110">You can easily [create a new Azure Container Registry](../../container-registry/container-registry-get-started-azure-cli.md), but hello steps are as follows:</span></span>

1. <span data-ttu-id="0d849-111">Utwórz toomanage grupy zasobów platformy Azure ACR rejestru i hello Kubernetes klastrem usługi ACS.</span><span class="sxs-lookup"><span data-stu-id="0d849-111">Create a Azure resource group toomanage your ACR registry and hello Kubernetes cluster in ACS.</span></span>
      ```azurecli
      az group create --name draft --location eastus
      ```

2. <span data-ttu-id="0d849-112">Utwórz rejestr obrazów ACR za pomocą polecenia [az acr create](/cli/azure/acr#create)</span><span class="sxs-lookup"><span data-stu-id="0d849-112">Create an ACR image registry using [az acr create](/cli/azure/acr#create)</span></span>
      ```azurecli
      az acr create -g draft -n draftacs --sku Basic --admin-enabled true -l eastus
      ```


## <a name="create-an-azure-container-service-with-kubernetes"></a><span data-ttu-id="0d849-113">Tworzenie usługi Azure Container Service za pomocą rozwiązania Kubernetes</span><span class="sxs-lookup"><span data-stu-id="0d849-113">Create an Azure Container Service with Kubernetes</span></span>

<span data-ttu-id="0d849-114">Teraz wszystko jest gotowe toouse [az acs utworzyć](/cli/azure/acs#create) toocreate ACS klastra przy użyciu Kubernetes jako hello `--orchestrator-type` wartość.</span><span class="sxs-lookup"><span data-stu-id="0d849-114">Now you're ready toouse [az acs create](/cli/azure/acs#create) toocreate an ACS cluster using Kubernetes as hello `--orchestrator-type` value.</span></span>
```azurecli
az acs create --resource-group draft --name draft-kube-acs --dns-prefix draft-cluster --orchestrator-type kubernetes
```

> [!NOTE]
> <span data-ttu-id="0d849-115">Ponieważ Kubernetes nie jest typem aranżacji domyślne hello, należy użyć hello `--orchestrator-type kubernetes` przełącznika.</span><span class="sxs-lookup"><span data-stu-id="0d849-115">Because Kubernetes is not hello default orchestrator type, be sure you use hello `--orchestrator-type kubernetes` switch.</span></span>

<span data-ttu-id="0d849-116">wyjściowy Hello zakończone powodzeniem wygląda podobne toohello poniżej.</span><span class="sxs-lookup"><span data-stu-id="0d849-116">hello output when successful looks similar toohello following.</span></span>

```json
waiting for AAD role toopropagate.done
{
  "id": "/subscriptions/<guid>/resourceGroups/draft/providers/Microsoft.Resources/deployments/azurecli14904.93snip09",
  "name": "azurecli1496227204.9323909",
  "properties": {
    "correlationId": "<guid>",
    "debugSetting": null,
    "dependencies": [],
    "mode": "Incremental",
    "outputs": null,
    "parameters": {
      "clientSecret": {
        "type": "SecureString"
      }
    },
    "parametersLink": null,
    "providers": [
      {
        "id": null,
        "namespace": "Microsoft.ContainerService",
        "registrationState": null,
        "resourceTypes": [
          {
            "aliases": null,
            "apiVersions": null,
            "locations": [
              "westus"
            ],
            "properties": null,
            "resourceType": "containerServices"
          }
        ]
      }
    ],
    "provisioningState": "Succeeded",
    "template": null,
    "templateLink": null,
    "timestamp": "2017-05-31T10:46:29.434095+00:00"
  },
  "resourceGroup": "draft"
}
```

<span data-ttu-id="0d849-117">Teraz, gdy masz klastra, można zaimportować hello poświadczeń przy użyciu hello [az kubernetes acs get poświadczenia](/cli/azure/acs/kubernetes#get-credentials) polecenia.</span><span class="sxs-lookup"><span data-stu-id="0d849-117">Now that you have a cluster, you can import hello credentials by using hello [az acs kubernetes get-credentials](/cli/azure/acs/kubernetes#get-credentials) command.</span></span> <span data-ttu-id="0d849-118">Teraz masz lokalnego pliku konfiguracji dla klastra należy jakie Helm i wersji roboczej tooget pracy.</span><span class="sxs-lookup"><span data-stu-id="0d849-118">Now you have a local configuration file for your cluster, which is what Helm and Draft need tooget their work done.</span></span>

## <a name="install-and-configure-draft"></a><span data-ttu-id="0d849-119">Instalowanie i konfigurowanie narzędzia Draft</span><span class="sxs-lookup"><span data-stu-id="0d849-119">Install and configure draft</span></span>
<span data-ttu-id="0d849-120">instrukcje instalacji Hello projekt znajdują się w hello [repozytorium projekt](https://github.com/Azure/draft/blob/master/docs/install.md).</span><span class="sxs-lookup"><span data-stu-id="0d849-120">hello installation instructions for Draft are in hello [Draft repository](https://github.com/Azure/draft/blob/master/docs/install.md).</span></span> <span data-ttu-id="0d849-121">Są stosunkowo proste, ale wymaga niektórych konfiguracji, ponieważ zależy on od [Helm](https://aka.ms/helm) toocreate i wdrażanie wykresu Helm do hello Kubernetes klastra.</span><span class="sxs-lookup"><span data-stu-id="0d849-121">They are relatively simple, but do require some configuration, as it depends on [Helm](https://aka.ms/helm) toocreate and deploy a Helm chart into hello Kubernetes cluster.</span></span>

1. <span data-ttu-id="0d849-122">[Pobierz i zainstaluj narzędzie Helm](https://aka.ms/helm#install).</span><span class="sxs-lookup"><span data-stu-id="0d849-122">[Download and install Helm](https://aka.ms/helm#install).</span></span>
2. <span data-ttu-id="0d849-123">Użyj toosearch Helm dla i zainstaluj `stable/traefik`i tooenable kontrolera wejściowych ruchu przychodzącego żądania kompilacji.</span><span class="sxs-lookup"><span data-stu-id="0d849-123">Use Helm toosearch for and install `stable/traefik`, and ingress controller tooenable inbound requests for your builds.</span></span>
    ```bash
    $ helm search traefik
    NAME            VERSION DESCRIPTION
    stable/traefik  1.3.0   A Traefik based Kubernetes ingress controller w...

    $ helm install stable/traefik --name ingress
    ```
    <span data-ttu-id="0d849-124">Teraz ustawić czujki na powitania `ingress` kontrolera toocapture hello zewnętrznych wartość IP po jej wdrożeniu.</span><span class="sxs-lookup"><span data-stu-id="0d849-124">Now set a watch on hello `ingress` controller toocapture hello external IP value when it is deployed.</span></span> <span data-ttu-id="0d849-125">Ten adres IP będzie hello jedną [mapowane domeny wdrożenia tooyour](#wire-up-deployment-domain) w następnej sekcji hello.</span><span class="sxs-lookup"><span data-stu-id="0d849-125">This IP address will be hello one [mapped tooyour deployment domain](#wire-up-deployment-domain) in hello next section.</span></span>

    ```bash
    kubectl get svc -w
    NAME                          CLUSTER-IP     EXTERNAL-IP     PORT(S)                      AGE
    ingress-traefik               10.0.248.104   13.64.108.240   80:31046/TCP,443:32556/TCP   1h
    kubernetes                    10.0.0.1       <none>          443/TCP                      7h
    ```

    <span data-ttu-id="0d849-126">W takim przypadku hello zewnętrznym adresem IP dla domeny wdrożenia hello jest `13.64.108.240`.</span><span class="sxs-lookup"><span data-stu-id="0d849-126">In this case, hello external IP for hello deployment domain is `13.64.108.240`.</span></span> <span data-ttu-id="0d849-127">Teraz możesz mapować IP toothat domeny.</span><span class="sxs-lookup"><span data-stu-id="0d849-127">Now you can map your domain toothat IP.</span></span>

## <a name="wire-up-deployment-domain"></a><span data-ttu-id="0d849-128">Podłączanie domeny wdrażania</span><span class="sxs-lookup"><span data-stu-id="0d849-128">Wire up deployment domain</span></span>

<span data-ttu-id="0d849-129">Narzędzie Draft tworzy wydanie dla każdego tworzonego planu Helm, czyli każdej aplikacji, nad którą pracujesz.</span><span class="sxs-lookup"><span data-stu-id="0d849-129">Draft creates a release for each Helm chart it creates -- each application you are working on.</span></span> <span data-ttu-id="0d849-130">Każda z nich zostanie wygenerowana nazwa, który jest używany przez projekt jako _poddomeny_ u góry głównego hello _domeny wdrożenia_ przez Ciebie harmonogramem.</span><span class="sxs-lookup"><span data-stu-id="0d849-130">Each one gets a generated name that is used by draft as a _subdomain_ on top of hello root _deployment domain_ that you control.</span></span> <span data-ttu-id="0d849-131">(W tym przykładzie używamy `squillace.io` jako hello wdrażania domen.) tooenable to zachowanie poddomeny, należy utworzyć rekord A dla `'*'` w wpisy DNS dla domeny wdrożenia, dzięki czemu każdy wygenerowany poddomeny jest routingiem toohello Kubernetes Kontroler wejściowych klastra.</span><span class="sxs-lookup"><span data-stu-id="0d849-131">(In this example, we use `squillace.io` as hello deployment domain.) tooenable this subdomain behavior, you must create an A record for `'*'` in your DNS entries for your deployment domain, so that each generated subdomain is routed toohello Kubernetes cluster's ingress controller.</span></span>

<span data-ttu-id="0d849-132">Dostawca domeny ma swoje własne serwery DNS tooassign sposób; zbyt[delegować tooAzure nameservers Twojego domeny DNS](../../dns/dns-delegate-domain-azure-dns.md), należy wykonać następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="0d849-132">Your own domain provider has their own way tooassign DNS servers; too[delegate your domain nameservers tooAzure DNS](../../dns/dns-delegate-domain-azure-dns.md), you take hello following steps:</span></span>

1. <span data-ttu-id="0d849-133">Utwórz grupę zasobów dla swojej strefy.</span><span class="sxs-lookup"><span data-stu-id="0d849-133">Create a resource group for your zone.</span></span>
    ```azurecli
    az group create --name squillace.io --location eastus
    {
      "id": "/subscriptions/<guid>/resourceGroups/squillace.io",
      "location": "eastus",
      "managedBy": null,
      "name": "zones",
      "properties": {
        "provisioningState": "Succeeded"
      },
      "tags": null
    }
    ```

2. <span data-ttu-id="0d849-134">Utwórz strefę DNS dla swojej domeny.</span><span class="sxs-lookup"><span data-stu-id="0d849-134">Create a DNS zone for your domain.</span></span>
<span data-ttu-id="0d849-135">Użyj hello [utworzyć strefę dns sieci az](/cli/azure/network/dns/zone#create) polecenia tooobtain hello nameservers toodelegate DNS kontrolować tooAzure DNS dla domeny.</span><span class="sxs-lookup"><span data-stu-id="0d849-135">Use hello [az network dns zone create](/cli/azure/network/dns/zone#create) command tooobtain hello nameservers toodelegate DNS control tooAzure DNS for your domain.</span></span>
    ```azurecli
    az network dns zone create --resource-group squillace.io --name squillace.io
    {
      "etag": "<guid>",
      "id": "/subscriptions/<guid>/resourceGroups/zones/providers/Microsoft.Network/dnszones/squillace.io",
      "location": "global",
      "maxNumberOfRecordSets": 5000,
      "name": "squillace.io",
      "nameServers": [
        "ns1-09.azure-dns.com.",
        "ns2-09.azure-dns.net.",
        "ns3-09.azure-dns.org.",
        "ns4-09.azure-dns.info."
      ],
      "numberOfRecordSets": 2,
      "resourceGroup": "squillace.io",
      "tags": {},
      "type": "Microsoft.Network/dnszones"
    }
    ```
3. <span data-ttu-id="0d849-136">Dodaj serwery DNS hello są podane toohello dostawcy domeny dla domeny wdrożenia, dzięki czemu możesz toouse usługi Azure DNS toorepoint domeny ma.</span><span class="sxs-lookup"><span data-stu-id="0d849-136">Add hello DNS servers you are given toohello domain provider for your deployment domain, which enables you toouse Azure DNS toorepoint your domain as you want.</span></span>
4. <span data-ttu-id="0d849-137">Utworzyć wpis zestaw rekordów A dla Twojego toohello mapowania domeny wdrożenia `ingress` IP z kroku 2 hello w poprzedniej sekcji.</span><span class="sxs-lookup"><span data-stu-id="0d849-137">Create an A record-set entry for your deployment domain mapping toohello `ingress` IP from step 2 of hello previous section.</span></span>
    ```azurecli
    az network dns record-set a add-record --ipv4-address 13.64.108.240 --record-set-name '*' -g squillace.io -z squillace.io
    ```
<span data-ttu-id="0d849-138">Witaj dane wyjściowe podobne:</span><span class="sxs-lookup"><span data-stu-id="0d849-138">hello output looks something like:</span></span>
    ```json
    {
      "arecords": [
        {
          "ipv4Address": "13.64.108.240"
        }
      ],
      "etag": "<guid>",
      "id": "/subscriptions/<guid>/resourceGroups/squillace.io/providers/Microsoft.Network/dnszones/squillace.io/A/*",
      "metadata": null,
      "name": "*",
      "resourceGroup": "squillace.io",
      "ttl": 3600,
      "type": "Microsoft.Network/dnszones/A"
    }
    ```

5. <span data-ttu-id="0d849-139">Skonfiguruj toouse projekt rejestru i utworzyć poddomeny dla każdego Helm wykresu, który tworzy.</span><span class="sxs-lookup"><span data-stu-id="0d849-139">Configure Draft toouse your registry and create subdomains for each Helm chart it creates.</span></span> <span data-ttu-id="0d849-140">tooconfigure projekt, potrzebne są:</span><span class="sxs-lookup"><span data-stu-id="0d849-140">tooconfigure Draft, you need:</span></span>
  - <span data-ttu-id="0d849-141">nazwa rejestru Azure Container Registry (w tym przykładzie: `draft`);</span><span class="sxs-lookup"><span data-stu-id="0d849-141">your Azure Container Registry name (in this example, `draft`)</span></span>
  - <span data-ttu-id="0d849-142">klucz rejestru lub hasło z polecenia `az acr credential show -n <registry name> --output tsv --query "passwords[0].value"`;</span><span class="sxs-lookup"><span data-stu-id="0d849-142">your registry key, or password, from `az acr credential show -n <registry name> --output tsv --query "passwords[0].value"`.</span></span>
  - <span data-ttu-id="0d849-143">Wdrażanie domeny głównej Hello, skonfigurowano toomap toohello Kubernetes wejściowych zewnętrzny adres IP (w tym miejscu `squillace.io`)</span><span class="sxs-lookup"><span data-stu-id="0d849-143">hello root deployment domain that you have configured toomap toohello Kubernetes ingress external IP address (here, `squillace.io`)</span></span>

  <span data-ttu-id="0d849-144">Wywołanie `draft init` i procesu konfiguracji hello wyświetla monit o podanie wartości hello powyżej.</span><span class="sxs-lookup"><span data-stu-id="0d849-144">Call `draft init` and hello configuration process prompts you for hello values above.</span></span> <span data-ttu-id="0d849-145">Witaj proces wygląda na to coś następujące hello hello po raz pierwszy, należy ją uruchomić.</span><span class="sxs-lookup"><span data-stu-id="0d849-145">hello process looks something like hello following hello first time you run it.</span></span>
 ```bash
    $ draft init
    Creating pack ruby...
    Creating pack node...
    Creating pack gradle...
    Creating pack maven...
    Creating pack php...
    Creating pack python...
    Creating pack dotnetcore...
    Creating pack golang...
    $DRAFT_HOME has been configured at /Users/ralphsquillace/.draft.

    In order tooinstall Draft, we need a bit more information...

    1. Enter your Docker registry URL (e.g. docker.io, quay.io, myregistry.azurecr.io): draft.azurecr.io
    2. Enter your username: draft
    3. Enter your password:
    4. Enter your org where Draft will push images [draft]: draft
    5. Enter your top-level domain for ingress (e.g. draft.example.com): squillace.io
    Draft has been installed into your Kubernetes Cluster.
    Happy Sailing!
    ```

<span data-ttu-id="0d849-146">Teraz wszystko jest gotowe toodeploy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="0d849-146">Now you're ready toodeploy an application.</span></span>


## <a name="build-and-deploy-an-application"></a><span data-ttu-id="0d849-147">Kompilowanie i wdrażanie aplikacji</span><span class="sxs-lookup"><span data-stu-id="0d849-147">Build and deploy an application</span></span>

<span data-ttu-id="0d849-148">W repozytorium projekt hello są [sześciu aplikacji prosty przykład](https://github.com/Azure/draft/tree/master/examples).</span><span class="sxs-lookup"><span data-stu-id="0d849-148">In hello Draft repo are [six simple example applications](https://github.com/Azure/draft/tree/master/examples).</span></span> <span data-ttu-id="0d849-149">Klonowanie repozytorium hello i Użyjmy hello [przykład Python](https://github.com/Azure/draft/tree/master/examples/python).</span><span class="sxs-lookup"><span data-stu-id="0d849-149">Clone hello repo and let's use hello [Python example](https://github.com/Azure/draft/tree/master/examples/python).</span></span> <span data-ttu-id="0d849-150">Zmiany w katalogu przykładów/Python hello i wpisz `draft create` toobuild hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="0d849-150">Change into hello examples/Python directory, and type `draft create` toobuild hello application.</span></span> <span data-ttu-id="0d849-151">Powinien on wyglądać hello poniższy przykład.</span><span class="sxs-lookup"><span data-stu-id="0d849-151">It should look like hello following example.</span></span>
```bash
$ draft create
--> Python app detected
--> Ready toosail
```

<span data-ttu-id="0d849-152">dane wyjściowe Hello zawiera plik Dockerfile i Helm wykresu.</span><span class="sxs-lookup"><span data-stu-id="0d849-152">hello output includes a Dockerfile and a Helm chart.</span></span> <span data-ttu-id="0d849-153">toobuild i wdrażania, wystarczy wpisać `draft up`.</span><span class="sxs-lookup"><span data-stu-id="0d849-153">toobuild and deploy, you just type `draft up`.</span></span> <span data-ttu-id="0d849-154">dane wyjściowe Hello jest rozbudowany, ale rozpoczyna się jak hello poniższy przykład.</span><span class="sxs-lookup"><span data-stu-id="0d849-154">hello output is extensive, but begins like hello following example.</span></span>
```bash
$ draft up
--> Building Dockerfile
Step 1 : FROM python:onbuild
onbuild: Pulling from library/python
10a267c67f42: Pulling fs layer
fb5937da9414: Pulling fs layer
9021b2326a1e: Pulling fs layer
dbed9b09434e: Pulling fs layer
ea8a37f15161: Pulling fs layer
<snip>
```

<span data-ttu-id="0d849-155">i kiedy kończy się pomyślnie coś podobnego toohello poniższy przykład.</span><span class="sxs-lookup"><span data-stu-id="0d849-155">and when successful ends with something similar toohello following example.</span></span>
```bash
ab68189731eb: Pushed
53c0ab0341bee12d01be3d3c192fbd63562af7f1: digest: sha256:bb0450ec37acf67ed461c1512ef21f58a500ff9326ce3ec623ce1e4427df9765 size: 2841
--> Deploying tooKubernetes
--> Status: DEPLOYED
--> Notes:

  http://gangly-bronco.squillace.io tooaccess your application

Watching local files for changes...
```

<span data-ttu-id="0d849-156">Niezależnie od jest nazwa wykresu, możesz teraz `curl http://gangly-bronco.squillace.io` tooreceive hello odpowiedzi, `Hello World!`.</span><span class="sxs-lookup"><span data-stu-id="0d849-156">Whatever your chart's name is, you can now `curl http://gangly-bronco.squillace.io` tooreceive hello reply, `Hello World!`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0d849-157">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="0d849-157">Next steps</span></span>

<span data-ttu-id="0d849-158">Teraz, gdy masz klaster usługi ACS Kubernetes można badać przy użyciu [rejestru kontenera Azure](../../container-registry/container-registry-intro.md) toocreate więcej i różnych wdrożenia tego scenariusza.</span><span class="sxs-lookup"><span data-stu-id="0d849-158">Now that you have an ACS Kubernetes cluster, you can investigate using [Azure Container Registry](../../container-registry/container-registry-intro.md) toocreate more and different deployments of this scenario.</span></span> <span data-ttu-id="0d849-159">Na przykład możesz utworzyć zestaw rekordów usługi DNS dla domeny draft._basedomain.toplevel_, który steruje działaniem na poziomie głębszej poddomeny dla specyficznych wdrożeń usługi ACS.</span><span class="sxs-lookup"><span data-stu-id="0d849-159">For example, you can create a draft._basedomain.toplevel_ domain DNS record-set that controls things off of a deeper subdomain for specific ACS deployments.</span></span>






