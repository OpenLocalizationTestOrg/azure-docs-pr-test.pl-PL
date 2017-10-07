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
# <a name="troubleshoot-deployment-issues-with-azure-container-instances"></a>Rozwiązywanie problemów dotyczących wdrożenia z wystąpień kontenera platformy Azure

W tym artykule opisano, jak tootroubleshoot problemy podczas wdrażania tooAzure kontenery wystąpień kontenera. Omówiono także niektóre hello typowych problemów, które może napotkać.

## <a name="getting-diagnostic-events"></a>Pobieranie zdarzeń diagnostycznych

Dzienniki tooview w kodzie aplikacji w kontenerze, można użyć hello [dzienniki kontenera az](/cli/azure/container#logs) polecenia. Jednak jeśli Twoje kontenera nie pomyślnie wdrożone, informacje diagnostyczne hello tooreview dostarczonych przez dostawcę zasobów hello wystąpień kontenera platformy Azure. zdarzenia hello tooview Twojego kontenera, uruchom następujące polecenie hello:

```azurecli-interactive
az container show -n mycontainername -g myresourcegroup
```

dane wyjściowe Hello zawiera właściwości core hello z kontenera, wraz z wdrożenia zdarzenia:

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

## <a name="common-deployment-issues"></a>Typowe problemy z wdrażaniem

Istnieje kilka typowych problemów z tego konta dla większości błędy we wdrożeniu.

### <a name="unable-toopull-image"></a>Nie można toopull obrazu

W przypadku wystąpień kontenera Azure toopull obrazu początkowo ponowną niektórych okres przed niepowodzeniem po pewnym czasie. Jeśli nie można ściągnąć obraz powitania, są wyświetlane zdarzeń, takich jak następujące hello:

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

tooresolve, usunąć kontener hello i ponów próbę wdrożenia, płatniczych szczególną uwagę prawidłowo wpisana nazwa obrazu hello.

### <a name="container-continually-exits-and-restarts"></a>Kontener stale kończy działanie i uruchamia ponownie

Obecnie wystąpień kontenera Azure obsługuje tylko długotrwałe usług. Jeśli Twoje kontenera uruchamia toocompletion i wyjściach, automatycznie uruchamia ponownie i zostanie ponownie uruchomione. W takim przypadku zdarzeń, takich jak następujące po są wyświetlane. Należy pamiętać, kontenera hello uruchamia, a następnie szybko ponownego uruchomienia. Witaj API wystąpień kontenera obejmuje `retryCount` właściwość, która pokazuje, ile razy w określonym kontenerze została uruchomiona ponownie.

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
> Większość obrazów kontener dla dystrybucje systemu Linux ustawić powłoki, takie jak bash, jako hello domyślne polecenie. Ponieważ powłoki samodzielnie nie jest usługą długotrwałe, kontenery natychmiast zamknąć i dzielą się na pętli ponownego uruchomienia.

### <a name="container-takes-a-long-time-toostart"></a>Kontener ma toostart długi czas

Jeśli Twoje kontenera toostart długo trwa, ale ostatecznie zakończy się pomyślnie, należy uruchomić analizując hello rozmiar obrazu kontenera. Ponieważ wystąpień kontenera platformy Azure pobiera kontener obrazu na żądanie, czas uruchamiania hello występują jest z nią bezpośrednio powiązane tooits rozmiar.

Można wyświetlić hello rozmiar obrazu kontenera przy użyciu interfejsu wiersza polecenia Docker hello:

```bash
docker images
```

Dane wyjściowe:

```bash
REPOSITORY                             TAG                 IMAGE ID            CREATED             SIZE
microsoft/aci-helloworld               latest              7f78509b568e        13 days ago         68.1MB
```

rozmiary obrazów klucza tookeeping Hello małych jest zapewnienie, że ostatecznego obrazu nie zawiera żadnych czynności, które nie są wymagane w czasie wykonywania. Jednym ze sposobów toodo jest [kompilacje wieloetapowym](https://docs.docker.com/engine/userguide/eng-image/multistage-build/). Kompilacje wieloetapowym był łatwy tooensure hello finalnego obrazu zawiera tylko artefakty hello potrzebne dla aplikacji, czy nie wszelkie dodatkowe hello zawartości, która nie jest wymagana podczas kompilacji.

Witaj innych sposób tooreduce hello wpływ ściągania obraz powitania w chwili uruchomienia z kontenera jest obraz kontenera hello toohost przy użyciu hello Azure kontenera rejestru w hello tym samym regionie, w którym ma być wystąpień kontenera Azure toouse. Skraca to ścieżki sieciowej hello hello tootravel potrzeb obrazu kontenera znacznie skrócić czas pobierania hello.
