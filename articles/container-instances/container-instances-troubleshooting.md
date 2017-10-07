---
title: "aaaTroubleshooting wystąpień kontenera platformy Azure"
description: "Dowiedz się, jak tootroubleshoot problemy związane z wystąpień kontenera platformy Azure"
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
ms.openlocfilehash: dfec636a0a174c74a6f2e9d9c4da6e871f8d2fda
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-deployment-issues-with-azure-container-instances"></a><span data-ttu-id="bf416-103">Rozwiązywanie problemów dotyczących wdrożenia z wystąpień kontenera platformy Azure</span><span class="sxs-lookup"><span data-stu-id="bf416-103">Troubleshoot deployment issues with Azure Container Instances</span></span>

<span data-ttu-id="bf416-104">W tym artykule opisano, jak tootroubleshoot problemy podczas wdrażania tooAzure kontenery wystąpień kontenera.</span><span class="sxs-lookup"><span data-stu-id="bf416-104">This article shows how tootroubleshoot issues when deploying containers tooAzure Container Instances.</span></span> <span data-ttu-id="bf416-105">Omówiono także niektóre hello typowych problemów, które może napotkać.</span><span class="sxs-lookup"><span data-stu-id="bf416-105">It also describes some of hello common issues you may run into.</span></span>

## <a name="getting-diagnostic-events"></a><span data-ttu-id="bf416-106">Pobieranie zdarzeń diagnostycznych</span><span class="sxs-lookup"><span data-stu-id="bf416-106">Getting diagnostic events</span></span>

<span data-ttu-id="bf416-107">Dzienniki tooview w kodzie aplikacji w kontenerze, można użyć hello [dzienniki kontenera az](/cli/azure/container#logs) polecenia.</span><span class="sxs-lookup"><span data-stu-id="bf416-107">tooview logs from your application code within a container, you can use hello [az container logs](/cli/azure/container#logs) command.</span></span> <span data-ttu-id="bf416-108">Jednak jeśli Twoje kontenera nie pomyślnie wdrożone, informacje diagnostyczne hello tooreview dostarczonych przez dostawcę zasobów hello wystąpień kontenera platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="bf416-108">But if your container does not deploy successfully, you need tooreview hello diagnostic information provided by hello Azure Container Instances resource provider.</span></span> <span data-ttu-id="bf416-109">zdarzenia hello tooview Twojego kontenera, uruchom następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="bf416-109">tooview hello events for your container, run hello following command:</span></span>

```azurecli-interactive
az container show -n mycontainername -g myresourcegroup
```

<span data-ttu-id="bf416-110">dane wyjściowe Hello zawiera właściwości core hello z kontenera, wraz z wdrożenia zdarzenia:</span><span class="sxs-lookup"><span data-stu-id="bf416-110">hello output includes hello core properties of your container, along with deployment events:</span></span>

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

## <a name="common-deployment-issues"></a><span data-ttu-id="bf416-111">Typowe problemy z wdrażaniem</span><span class="sxs-lookup"><span data-stu-id="bf416-111">Common deployment issues</span></span>

<span data-ttu-id="bf416-112">Istnieje kilka typowych problemów z tego konta dla większości błędy we wdrożeniu.</span><span class="sxs-lookup"><span data-stu-id="bf416-112">There are a few common issues that account for most errors in deployment.</span></span>

### <a name="unable-toopull-image"></a><span data-ttu-id="bf416-113">Nie można toopull obrazu</span><span class="sxs-lookup"><span data-stu-id="bf416-113">Unable toopull image</span></span>

<span data-ttu-id="bf416-114">W przypadku wystąpień kontenera Azure toopull obrazu początkowo ponowną niektórych okres przed niepowodzeniem po pewnym czasie.</span><span class="sxs-lookup"><span data-stu-id="bf416-114">If Azure Container Instances is unable toopull your image initially, it retries for some period before eventually failing.</span></span> <span data-ttu-id="bf416-115">Jeśli nie można ściągnąć obraz powitania, są wyświetlane zdarzeń, takich jak następujące hello:</span><span class="sxs-lookup"><span data-stu-id="bf416-115">If hello image cannot be pulled, events like hello following are shown:</span></span>

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
    "message": "Failed: Failed toopull image \"microsoft/aci-hellowrld\": rpc error: code 2 desc Error: image microsoft/aci-hellowrld:latest not found",
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

<span data-ttu-id="bf416-116">tooresolve, usunąć kontener hello i ponów próbę wdrożenia, płatniczych szczególną uwagę prawidłowo wpisana nazwa obrazu hello.</span><span class="sxs-lookup"><span data-stu-id="bf416-116">tooresolve, delete hello container and retry your deployment, paying close attention that you have typed hello image name correctly.</span></span>

### <a name="container-continually-exits-and-restarts"></a><span data-ttu-id="bf416-117">Kontener stale kończy działanie i uruchamia ponownie</span><span class="sxs-lookup"><span data-stu-id="bf416-117">Container continually exits and restarts</span></span>

<span data-ttu-id="bf416-118">Obecnie wystąpień kontenera Azure obsługuje tylko długotrwałe usług.</span><span class="sxs-lookup"><span data-stu-id="bf416-118">Currently, Azure Container Instances only supports long-running services.</span></span> <span data-ttu-id="bf416-119">Jeśli Twoje kontenera uruchamia toocompletion i wyjściach, automatycznie uruchamia ponownie i zostanie ponownie uruchomione.</span><span class="sxs-lookup"><span data-stu-id="bf416-119">If your container runs toocompletion and exits, it automatically restarts and runs again.</span></span> <span data-ttu-id="bf416-120">W takim przypadku zdarzeń, takich jak następujące po są wyświetlane.</span><span class="sxs-lookup"><span data-stu-id="bf416-120">If this happens, events like those following are shown.</span></span> <span data-ttu-id="bf416-121">Należy pamiętać, kontenera hello uruchamia, a następnie szybko ponownego uruchomienia.</span><span class="sxs-lookup"><span data-stu-id="bf416-121">Note that hello container successfully starts, then quickly restarts.</span></span> <span data-ttu-id="bf416-122">Witaj API wystąpień kontenera obejmuje `retryCount` właściwość, która pokazuje, ile razy w określonym kontenerze została uruchomiona ponownie.</span><span class="sxs-lookup"><span data-stu-id="bf416-122">hello Container Instances API includes a `retryCount` property that shows how many times a particular container has restarted.</span></span>

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
> <span data-ttu-id="bf416-123">Większość obrazów kontener dla dystrybucje systemu Linux ustawić powłoki, takie jak bash, jako hello domyślne polecenie.</span><span class="sxs-lookup"><span data-stu-id="bf416-123">Most container images for Linux distributions set a shell, such as bash, as hello default command.</span></span> <span data-ttu-id="bf416-124">Ponieważ powłoki samodzielnie nie jest usługą długotrwałe, kontenery natychmiast zamknąć i dzielą się na pętli ponownego uruchomienia.</span><span class="sxs-lookup"><span data-stu-id="bf416-124">Since a shell on its own is not a long-running service, these containers immediately exit and fall into a restart loop.</span></span>

### <a name="container-takes-a-long-time-toostart"></a><span data-ttu-id="bf416-125">Kontener ma toostart długi czas</span><span class="sxs-lookup"><span data-stu-id="bf416-125">Container takes a long time toostart</span></span>

<span data-ttu-id="bf416-126">Jeśli Twoje kontenera toostart długo trwa, ale ostatecznie zakończy się pomyślnie, należy uruchomić analizując hello rozmiar obrazu kontenera.</span><span class="sxs-lookup"><span data-stu-id="bf416-126">If your container takes a long time toostart, but eventually succeeds, start by looking at hello size of your container image.</span></span> <span data-ttu-id="bf416-127">Ponieważ wystąpień kontenera platformy Azure pobiera kontener obrazu na żądanie, czas uruchamiania hello występują jest z nią bezpośrednio powiązane tooits rozmiar.</span><span class="sxs-lookup"><span data-stu-id="bf416-127">Because Azure Container Instances pulls your container image on demand, hello startup time you experience is directly related tooits size.</span></span>

<span data-ttu-id="bf416-128">Można wyświetlić hello rozmiar obrazu kontenera przy użyciu interfejsu wiersza polecenia Docker hello:</span><span class="sxs-lookup"><span data-stu-id="bf416-128">You can view hello size of your container image using hello Docker CLI:</span></span>

```bash
docker images
```

<span data-ttu-id="bf416-129">Dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="bf416-129">Output:</span></span>

```bash
REPOSITORY                             TAG                 IMAGE ID            CREATED             SIZE
microsoft/aci-helloworld               latest              7f78509b568e        13 days ago         68.1MB
```

<span data-ttu-id="bf416-130">rozmiary obrazów klucza tookeeping Hello małych jest zapewnienie, że ostatecznego obrazu nie zawiera żadnych czynności, które nie są wymagane w czasie wykonywania.</span><span class="sxs-lookup"><span data-stu-id="bf416-130">hello key tookeeping image sizes small is ensuring that your final image does not contain anything that is not required at runtime.</span></span> <span data-ttu-id="bf416-131">Jednym ze sposobów toodo jest [kompilacje wieloetapowym](https://docs.docker.com/engine/userguide/eng-image/multistage-build/).</span><span class="sxs-lookup"><span data-stu-id="bf416-131">One way toodo this is with [multi-stage builds](https://docs.docker.com/engine/userguide/eng-image/multistage-build/).</span></span> <span data-ttu-id="bf416-132">Kompilacje wieloetapowym był łatwy tooensure hello finalnego obrazu zawiera tylko artefakty hello potrzebne dla aplikacji, czy nie wszelkie dodatkowe hello zawartości, która nie jest wymagana podczas kompilacji.</span><span class="sxs-lookup"><span data-stu-id="bf416-132">Multi-stage builds make it easy tooensure that hello final image contains only hello artifacts you need for your application, and not any of hello extra content that was required at build time.</span></span>

<span data-ttu-id="bf416-133">Witaj innych sposób tooreduce hello wpływ ściągania obraz powitania w chwili uruchomienia z kontenera jest obraz kontenera hello toohost przy użyciu hello Azure kontenera rejestru w hello tym samym regionie, w którym ma być wystąpień kontenera Azure toouse.</span><span class="sxs-lookup"><span data-stu-id="bf416-133">hello other way tooreduce hello impact of hello image pull on your container's startup time is toohost hello container image using hello Azure Container Registry in hello same region where you intend toouse Azure Container Instances.</span></span> <span data-ttu-id="bf416-134">Skraca to ścieżki sieciowej hello hello tootravel potrzeb obrazu kontenera znacznie skrócić czas pobierania hello.</span><span class="sxs-lookup"><span data-stu-id="bf416-134">This shortens hello network path that hello container image needs tootravel, significantly shortening hello download time.</span></span>
