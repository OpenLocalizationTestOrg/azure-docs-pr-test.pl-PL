---
title: "Rozwiązywanie problemów z wystąpień kontenera platformy Azure"
description: "Dowiedz się, jak rozwiązać problemy z wystąpień kontenera platformy Azure"
services: container-instances
documentationcenter: 
author: seanmck
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 
ms.service: container-instances
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/03/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: 86fa4b7dca7c362f95c0243a33f03d1f2dd3ab42
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="troubleshoot-deployment-issues-with-azure-container-instances"></a><span data-ttu-id="91962-103">Rozwiązywanie problemów dotyczących wdrożenia z wystąpień kontenera platformy Azure</span><span class="sxs-lookup"><span data-stu-id="91962-103">Troubleshoot deployment issues with Azure Container Instances</span></span>

<span data-ttu-id="91962-104">W tym artykule przedstawiono sposób rozwiązywania problemów w przypadku wdrażania kontenerów do wystąpień kontenera platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="91962-104">This article shows how to troubleshoot issues when deploying containers to Azure Container Instances.</span></span> <span data-ttu-id="91962-105">Omówiono także niektóre typowe problemy, które może napotkać.</span><span class="sxs-lookup"><span data-stu-id="91962-105">It also describes some of the common issues you may run into.</span></span>

## <a name="getting-diagnostic-events"></a><span data-ttu-id="91962-106">Pobieranie zdarzeń diagnostycznych</span><span class="sxs-lookup"><span data-stu-id="91962-106">Getting diagnostic events</span></span>

<span data-ttu-id="91962-107">Aby wyświetlić dzienniki w kodzie aplikacji w kontenerze, można użyć [dzienniki kontenera az](/cli/azure/container#logs) polecenia.</span><span class="sxs-lookup"><span data-stu-id="91962-107">To view logs from your application code within a container, you can use the [az container logs](/cli/azure/container#logs) command.</span></span> <span data-ttu-id="91962-108">Jednak jeśli Twoje kontenera nie pomyślnie wdrożone, należy przejrzeć informacje diagnostyczne dostarczone przez dostawcę zasobów wystąpień kontenera platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="91962-108">But if your container does not deploy successfully, you need to review the diagnostic information provided by the Azure Container Instances resource provider.</span></span> <span data-ttu-id="91962-109">Aby wyświetlić zdarzenia z kontenera, uruchom następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="91962-109">To view the events for your container, run the following command:</span></span>

```azurecli-interactive
az container show -n mycontainername -g myresourcegroup
```

<span data-ttu-id="91962-110">Dane wyjściowe zawiera właściwości core z kontenera, wraz z wdrożenia zdarzenia:</span><span class="sxs-lookup"><span data-stu-id="91962-110">The output includes the core properties of your container, along with deployment events:</span></span>

```bash
{
  "containers": [
    {
      "command": null,
      "environmentVariables": [],
      "image": "microsoft/aci-helloworld",
      ...

      "events": [
      {
        "count": 1,
        "firstTimestamp": "2017-08-03T22:12:52+00:00",
        "lastTimestamp": "2017-08-03T22:12:52+00:00",
        "message": "Pulling: pulling image \"microsoft/aci-helloworld\"",
        "type": "Normal"
      },
      {
        "count": 1,
        "firstTimestamp": "2017-08-03T22:12:55+00:00",
        "lastTimestamp": "2017-08-03T22:12:55+00:00",
        "message": "Pulled: Successfully pulled image \"microsoft/aci-helloworld\"",
        "type": "Normal"
      },
      {
        "count": 1,
        "firstTimestamp": "2017-08-03T22:12:55+00:00",
        "lastTimestamp": "2017-08-03T22:12:55+00:00",
        "message": "Created: Created container with id 61602059d6c31529c27609ef4ec0c858b0a96150177fa045cf944d7cf8fbab69",
        "type": "Normal"
      },
      {
        "count": 1,
        "firstTimestamp": "2017-08-03T22:12:55+00:00",
        "lastTimestamp": "2017-08-03T22:12:55+00:00",
        "message": "Started: Started container with id 61602059d6c31529c27609ef4ec0c858b0a96150177fa045cf944d7cf8fbab69",
        "type": "Normal"
      }
    ],
    "name": "helloworld",
      "ports": [
        {
          "port": 80
        }
      ],
    ...
  ]
}
```

## <a name="common-deployment-issues"></a><span data-ttu-id="91962-111">Typowe problemy z wdrażaniem</span><span class="sxs-lookup"><span data-stu-id="91962-111">Common deployment issues</span></span>

<span data-ttu-id="91962-112">Istnieje kilka typowych problemów z tego konta dla większości błędy we wdrożeniu.</span><span class="sxs-lookup"><span data-stu-id="91962-112">There are a few common issues that account for most errors in deployment.</span></span>

### <a name="unable-to-pull-image"></a><span data-ttu-id="91962-113">Nie można ściągania obrazu</span><span class="sxs-lookup"><span data-stu-id="91962-113">Unable to pull image</span></span>

<span data-ttu-id="91962-114">W przypadku nie można ściągnąć obrazu początkowo wystąpień kontenera Azure ponowi próbę niektórych okres przed niepowodzeniem po pewnym czasie.</span><span class="sxs-lookup"><span data-stu-id="91962-114">If Azure Container Instances is unable to pull your image initially, it retries for some period before eventually failing.</span></span> <span data-ttu-id="91962-115">Jeśli obraz nie może być pobierane, wyświetlane są zdarzenia podobne do następujących:</span><span class="sxs-lookup"><span data-stu-id="91962-115">If the image cannot be pulled, events like the following are shown:</span></span>

```bash
"events": [
  {
    "count": 1,
    "firstTimestamp": "2017-08-03T22:19:31+00:00",
    "lastTimestamp": "2017-08-03T22:19:31+00:00",
    "message": "Pulling: pulling image \"microsoft/aci-hellowrld\"",
    "type": "Normal"
  },
  {
    "count": 1,
    "firstTimestamp": "2017-08-03T22:19:32+00:00",
    "lastTimestamp": "2017-08-03T22:19:32+00:00",
    "message": "Failed: Failed to pull image \"microsoft/aci-hellowrld\": rpc error: code 2 desc Error: image microsoft/aci-hellowrld:latest not found",
    "type": "Warning"
  },
  {
    "count": 1,
    "firstTimestamp": "2017-08-03T22:19:33+00:00",
    "lastTimestamp": "2017-08-03T22:19:33+00:00",
    "message": "BackOff: Back-off pulling image \"microsoft/aci-hellowrld\"",
    "type": "Normal"
  }
]
```

<span data-ttu-id="91962-116">Aby rozwiązać, usunięcie kontenera i ponów próbę wdrożenia, płatności zamknięcie uwagi prawidłowo wpisana nazwa obrazu.</span><span class="sxs-lookup"><span data-stu-id="91962-116">To resolve, delete the container and retry your deployment, paying close attention that you have typed the image name correctly.</span></span>

### <a name="container-continually-exits-and-restarts"></a><span data-ttu-id="91962-117">Kontener stale kończy działanie i uruchamia ponownie</span><span class="sxs-lookup"><span data-stu-id="91962-117">Container continually exits and restarts</span></span>

<span data-ttu-id="91962-118">Obecnie wystąpień kontenera Azure obsługuje tylko długotrwałe usług.</span><span class="sxs-lookup"><span data-stu-id="91962-118">Currently, Azure Container Instances only supports long-running services.</span></span> <span data-ttu-id="91962-119">Jeśli z kontenera uruchamia uzupełniania i wyjściach, automatycznie uruchamia ponownie i zostanie ponownie uruchomione.</span><span class="sxs-lookup"><span data-stu-id="91962-119">If your container runs to completion and exits, it automatically restarts and runs again.</span></span> <span data-ttu-id="91962-120">W takim przypadku zdarzeń, takich jak następujące po są wyświetlane.</span><span class="sxs-lookup"><span data-stu-id="91962-120">If this happens, events like those following are shown.</span></span> <span data-ttu-id="91962-121">Należy pamiętać, że kontener uruchamia, a następnie szybko ponownego uruchomienia.</span><span class="sxs-lookup"><span data-stu-id="91962-121">Note that the container successfully starts, then quickly restarts.</span></span> <span data-ttu-id="91962-122">Interfejs API wystąpień kontenera zawiera `retryCount` właściwość, która pokazuje, ile razy w określonym kontenerze została uruchomiona ponownie.</span><span class="sxs-lookup"><span data-stu-id="91962-122">The Container Instances API includes a `retryCount` property that shows how many times a particular container has restarted.</span></span>

```bash
"events": [
  {
    "count": 5,
    "firstTimestamp": "2017-08-03T22:21:55+00:00",
    "lastTimestamp": "2017-08-03T22:23:22+00:00",
    "message": "Pulling: pulling image \"alpine\"",
    "type": "Normal"
  },
  {
    "count": 5,
    "firstTimestamp": "2017-08-03T22:21:57+00:00",
    "lastTimestamp": "2017-08-03T22:23:23+00:00",
    "message": "Pulled: Successfully pulled image \"alpine\"",
    "type": "Normal"
  },
  {
    "count": 1,
    "firstTimestamp": "2017-08-03T22:21:57+00:00",
    "lastTimestamp": "2017-08-03T22:21:57+00:00",
    "message": "Created: Created container with id ad2bf9bc51761c5f935260b4bab53b164d52d9cbc045b16afcb26fb4d14d0a70",
    "type": "Normal"
  },
  {
    "count": 1,
    "firstTimestamp": "2017-08-03T22:21:57+00:00",
    "lastTimestamp": "2017-08-03T22:21:57+00:00",
    "message": "Started: Started container with id ad2bf9bc51761c5f935260b4bab53b164d52d9cbc045b16afcb26fb4d14d0a70",
    "type": "Normal"
  },
  {
    "count": 1,
    "firstTimestamp": "2017-08-03T22:21:58+00:00",
    "lastTimestamp": "2017-08-03T22:21:58+00:00",
    "message": "Created: Created container with id 7687b9bd15dc01731fa66fc45f6f0241495600602dd03841e559453245e7f70b",
    "type": "Normal"
  },
  {
    "count": 1,
    "firstTimestamp": "2017-08-03T22:21:58+00:00",
    "lastTimestamp": "2017-08-03T22:21:58+00:00",
    "message": "Started: Started container with id 7687b9bd15dc01731fa66fc45f6f0241495600602dd03841e559453245e7f70b",
    "type": "Normal"
  },
  {
    "count": 13,
    "firstTimestamp": "2017-08-03T22:21:59+00:00",
    "lastTimestamp": "2017-08-03T22:24:36+00:00",
    "message": "BackOff: Back-off restarting failed container",
    "type": "Warning"
  },
  {
    "count": 1,
    "firstTimestamp": "2017-08-03T22:22:13+00:00",
    "lastTimestamp": "2017-08-03T22:22:13+00:00",
    "message": "Created: Created container with id 72e347e891290e238135e4a6b3078748ca25a1275dbbff30d8d214f026d89220",
    "type": "Normal"
  },
  ...
```

> [!NOTE]
> <span data-ttu-id="91962-123">Większość obrazów kontener dla dystrybucje systemu Linux ustawić powłoki, takie jak bash, jako domyślne polecenie.</span><span class="sxs-lookup"><span data-stu-id="91962-123">Most container images for Linux distributions set a shell, such as bash, as the default command.</span></span> <span data-ttu-id="91962-124">Ponieważ powłoki samodzielnie nie jest usługą długotrwałe, kontenery natychmiast zamknąć i dzielą się na pętli ponownego uruchomienia.</span><span class="sxs-lookup"><span data-stu-id="91962-124">Since a shell on its own is not a long-running service, these containers immediately exit and fall into a restart loop.</span></span>

### <a name="container-takes-a-long-time-to-start"></a><span data-ttu-id="91962-125">Kontener zajmuje dużo czasu do uruchomienia</span><span class="sxs-lookup"><span data-stu-id="91962-125">Container takes a long time to start</span></span>

<span data-ttu-id="91962-126">Jeśli Twoje kontenera zajmuje dużo czasu można uruchomić, ale ostatecznie zakończy się powodzeniem, przyjrzeć rozmiar obrazu kontenera.</span><span class="sxs-lookup"><span data-stu-id="91962-126">If your container takes a long time to start, but eventually succeeds, start by looking at the size of your container image.</span></span> <span data-ttu-id="91962-127">Ponieważ wystąpień kontenera platformy Azure pobiera kontener obrazu na żądanie, czas uruchamiania, które występują jest bezpośrednio powiązana z jego rozmiaru.</span><span class="sxs-lookup"><span data-stu-id="91962-127">Because Azure Container Instances pulls your container image on demand, the startup time you experience is directly related to its size.</span></span>

<span data-ttu-id="91962-128">Rozmiar obrazu kontenera przy użyciu interfejsu wiersza polecenia Docker można wyświetlić:</span><span class="sxs-lookup"><span data-stu-id="91962-128">You can view the size of your container image using the Docker CLI:</span></span>

```bash
docker images
```

<span data-ttu-id="91962-129">Dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="91962-129">Output:</span></span>

```bash
REPOSITORY                             TAG                 IMAGE ID            CREATED             SIZE
microsoft/aci-helloworld               latest              7f78509b568e        13 days ago         68.1MB
```

<span data-ttu-id="91962-130">Klucz do przechowywania małych rozmiary obrazów jest zapewnienie, że ostatecznego obrazu nie zawiera żadnych czynności, które nie są wymagane w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="91962-130">The key to keeping image sizes small is ensuring that your final image does not contain anything that is not required at runtime.</span></span> <span data-ttu-id="91962-131">Jednym ze sposobów czy jest on [kompilacje wieloetapowym](https://docs.docker.com/engine/userguide/eng-image/multistage-build/).</span><span class="sxs-lookup"><span data-stu-id="91962-131">One way to do this is with [multi-stage builds](https://docs.docker.com/engine/userguide/eng-image/multistage-build/).</span></span> <span data-ttu-id="91962-132">Wieloetapowym kompilacje upewnij ułatwiają zapewnienie finalnego obrazu zawiera artefakty potrzebnych dla aplikacji i nie jakiekolwiek nadmiarowe zawartości, która nie jest wymagana podczas kompilacji.</span><span class="sxs-lookup"><span data-stu-id="91962-132">Multi-stage builds make it easy to ensure that the final image contains only the artifacts you need for your application, and not any of the extra content that was required at build time.</span></span>

<span data-ttu-id="91962-133">Inny sposób, aby zmniejszyć wpływ ściągania obrazu na czas uruchamiania programu kontenera jest hosta obrazu kontenera, w tym samym regionie, w którym zamierzasz używać wystąpień kontenera Azure za pomocą rejestru kontenera platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="91962-133">The other way to reduce the impact of the image pull on your container's startup time is to host the container image using the Azure Container Registry in the same region where you intend to use Azure Container Instances.</span></span> <span data-ttu-id="91962-134">Skraca lokalizacji sieciowej, która obraz kontenera musi podróży, znacznie skrócić czas pobierania.</span><span class="sxs-lookup"><span data-stu-id="91962-134">This shortens the network path that the container image needs to travel, significantly shortening the download time.</span></span>