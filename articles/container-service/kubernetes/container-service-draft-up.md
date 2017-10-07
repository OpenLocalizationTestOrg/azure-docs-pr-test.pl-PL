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
# <a name="use-draft-with-azure-container-service-and-azure-container-registry-toobuild-and-deploy-an-application-tookubernetes"></a>Projekt za pomocą toobuild usługi kontenera platformy Azure i rejestru kontenera Azure i wdrażanie aplikacji tooKubernetes

[Projekt](https://aka.ms/draft) to nowe narzędzie open source, który umożliwia łatwe toodevelop aplikacji kontenera i wdrażanie ich klastry tooKubernetes bez wiedzy o te informacje o Docker i Kubernetes — lub nawet ich zainstalowanie. Za pomocą takich narzędzi jak projekt umożliwiają możesz i zespół zespołami tworzenie aplikacji hello z Kubernetes, nie płatności tyle tooinfrastructure uwagi.

Narzędzia Draft można użyć z dowolnym rejestrem obrazów Docker i dowolnym klastrem Kubernetes, w tym lokalnym. Ten samouczek pokazuje, jak toouse ACS z toocreate Kubernetes, ACR i usługi Azure DNS na żywo developer CI/CD potoku przy użyciu wersji roboczej.


## <a name="create-an-azure-container-registry"></a>Tworzenie rejestru Azure Container Registry
Możesz z łatwością [tworzenie nowych rejestru kontenera Azure](../../container-registry/container-registry-get-started-azure-cli.md), ale hello obejmuje następujące czynności:

1. Utwórz toomanage grupy zasobów platformy Azure ACR rejestru i hello Kubernetes klastrem usługi ACS.
      ```azurecli
      az group create --name draft --location eastus
      ```

2. Utwórz rejestr obrazów ACR za pomocą polecenia [az acr create](/cli/azure/acr#create)
      ```azurecli
      az acr create -g draft -n draftacs --sku Basic --admin-enabled true -l eastus
      ```


## <a name="create-an-azure-container-service-with-kubernetes"></a>Tworzenie usługi Azure Container Service za pomocą rozwiązania Kubernetes

Teraz wszystko jest gotowe toouse [az acs utworzyć](/cli/azure/acs#create) toocreate ACS klastra przy użyciu Kubernetes jako hello `--orchestrator-type` wartość.
```azurecli
az acs create --resource-group draft --name draft-kube-acs --dns-prefix draft-cluster --orchestrator-type kubernetes
```

> [!NOTE]
> Ponieważ Kubernetes nie jest typem aranżacji domyślne hello, należy użyć hello `--orchestrator-type kubernetes` przełącznika.

wyjściowy Hello zakończone powodzeniem wygląda podobne toohello poniżej.

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

Teraz, gdy masz klastra, można zaimportować hello poświadczeń przy użyciu hello [az kubernetes acs get poświadczenia](/cli/azure/acs/kubernetes#get-credentials) polecenia. Teraz masz lokalnego pliku konfiguracji dla klastra należy jakie Helm i wersji roboczej tooget pracy.

## <a name="install-and-configure-draft"></a>Instalowanie i konfigurowanie narzędzia Draft
instrukcje instalacji Hello projekt znajdują się w hello [repozytorium projekt](https://github.com/Azure/draft/blob/master/docs/install.md). Są stosunkowo proste, ale wymaga niektórych konfiguracji, ponieważ zależy on od [Helm](https://aka.ms/helm) toocreate i wdrażanie wykresu Helm do hello Kubernetes klastra.

1. [Pobierz i zainstaluj narzędzie Helm](https://aka.ms/helm#install).
2. Użyj toosearch Helm dla i zainstaluj `stable/traefik`i tooenable kontrolera wejściowych ruchu przychodzącego żądania kompilacji.
    ```bash
    $ helm search traefik
    NAME            VERSION DESCRIPTION
    stable/traefik  1.3.0   A Traefik based Kubernetes ingress controller w...

    $ helm install stable/traefik --name ingress
    ```
    Teraz ustawić czujki na powitania `ingress` kontrolera toocapture hello zewnętrznych wartość IP po jej wdrożeniu. Ten adres IP będzie hello jedną [mapowane domeny wdrożenia tooyour](#wire-up-deployment-domain) w następnej sekcji hello.

    ```bash
    kubectl get svc -w
    NAME                          CLUSTER-IP     EXTERNAL-IP     PORT(S)                      AGE
    ingress-traefik               10.0.248.104   13.64.108.240   80:31046/TCP,443:32556/TCP   1h
    kubernetes                    10.0.0.1       <none>          443/TCP                      7h
    ```

    W takim przypadku hello zewnętrznym adresem IP dla domeny wdrożenia hello jest `13.64.108.240`. Teraz możesz mapować IP toothat domeny.

## <a name="wire-up-deployment-domain"></a>Podłączanie domeny wdrażania

Narzędzie Draft tworzy wydanie dla każdego tworzonego planu Helm, czyli każdej aplikacji, nad którą pracujesz. Każda z nich zostanie wygenerowana nazwa, który jest używany przez projekt jako _poddomeny_ u góry głównego hello _domeny wdrożenia_ przez Ciebie harmonogramem. (W tym przykładzie używamy `squillace.io` jako hello wdrażania domen.) tooenable to zachowanie poddomeny, należy utworzyć rekord A dla `'*'` w wpisy DNS dla domeny wdrożenia, dzięki czemu każdy wygenerowany poddomeny jest routingiem toohello Kubernetes Kontroler wejściowych klastra.

Dostawca domeny ma swoje własne serwery DNS tooassign sposób; zbyt[delegować tooAzure nameservers Twojego domeny DNS](../../dns/dns-delegate-domain-azure-dns.md), należy wykonać następujące kroki hello:

1. Utwórz grupę zasobów dla swojej strefy.
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

2. Utwórz strefę DNS dla swojej domeny.
Użyj hello [utworzyć strefę dns sieci az](/cli/azure/network/dns/zone#create) polecenia tooobtain hello nameservers toodelegate DNS kontrolować tooAzure DNS dla domeny.
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
3. Dodaj serwery DNS hello są podane toohello dostawcy domeny dla domeny wdrożenia, dzięki czemu możesz toouse usługi Azure DNS toorepoint domeny ma.
4. Utworzyć wpis zestaw rekordów A dla Twojego toohello mapowania domeny wdrożenia `ingress` IP z kroku 2 hello w poprzedniej sekcji.
    ```azurecli
    az network dns record-set a add-record --ipv4-address 13.64.108.240 --record-set-name '*' -g squillace.io -z squillace.io
    ```
Witaj dane wyjściowe podobne:
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

5. Skonfiguruj toouse projekt rejestru i utworzyć poddomeny dla każdego Helm wykresu, który tworzy. tooconfigure projekt, potrzebne są:
  - nazwa rejestru Azure Container Registry (w tym przykładzie: `draft`);
  - klucz rejestru lub hasło z polecenia `az acr credential show -n <registry name> --output tsv --query "passwords[0].value"`;
  - Wdrażanie domeny głównej Hello, skonfigurowano toomap toohello Kubernetes wejściowych zewnętrzny adres IP (w tym miejscu `squillace.io`)

  Wywołanie `draft init` i procesu konfiguracji hello wyświetla monit o podanie wartości hello powyżej. Witaj proces wygląda na to coś następujące hello hello po raz pierwszy, należy ją uruchomić.
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

Teraz wszystko jest gotowe toodeploy aplikacji.


## <a name="build-and-deploy-an-application"></a>Kompilowanie i wdrażanie aplikacji

W repozytorium projekt hello są [sześciu aplikacji prosty przykład](https://github.com/Azure/draft/tree/master/examples). Klonowanie repozytorium hello i Użyjmy hello [przykład Python](https://github.com/Azure/draft/tree/master/examples/python). Zmiany w katalogu przykładów/Python hello i wpisz `draft create` toobuild hello aplikacji. Powinien on wyglądać hello poniższy przykład.
```bash
$ draft create
--> Python app detected
--> Ready toosail
```

dane wyjściowe Hello zawiera plik Dockerfile i Helm wykresu. toobuild i wdrażania, wystarczy wpisać `draft up`. dane wyjściowe Hello jest rozbudowany, ale rozpoczyna się jak hello poniższy przykład.
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

i kiedy kończy się pomyślnie coś podobnego toohello poniższy przykład.
```bash
ab68189731eb: Pushed
53c0ab0341bee12d01be3d3c192fbd63562af7f1: digest: sha256:bb0450ec37acf67ed461c1512ef21f58a500ff9326ce3ec623ce1e4427df9765 size: 2841
--> Deploying tooKubernetes
--> Status: DEPLOYED
--> Notes:

  http://gangly-bronco.squillace.io tooaccess your application

Watching local files for changes...
```

Niezależnie od jest nazwa wykresu, możesz teraz `curl http://gangly-bronco.squillace.io` tooreceive hello odpowiedzi, `Hello World!`.

## <a name="next-steps"></a>Następne kroki

Teraz, gdy masz klaster usługi ACS Kubernetes można badać przy użyciu [rejestru kontenera Azure](../../container-registry/container-registry-intro.md) toocreate więcej i różnych wdrożenia tego scenariusza. Na przykład możesz utworzyć zestaw rekordów usługi DNS dla domeny draft._basedomain.toplevel_, który steruje działaniem na poziomie głębszej poddomeny dla specyficznych wdrożeń usługi ACS.






