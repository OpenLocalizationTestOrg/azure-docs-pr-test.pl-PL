---
title: "aaaApplication lub usługi Marathon specyficzne dla użytkownika | Dokumentacja firmy Microsoft"
description: "Tworzenie usługi Marathon specyficznej dla aplikacji lub użytkownika"
services: container-service
documentationcenter: 
author: rgardler
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Kontenery, Marathon, mikrousługi, DC/OS, Azure"
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/12/2016
ms.author: rogardle
ms.custom: mvc
ms.openlocfilehash: 1e6f69ed64e113a3a059788a71ddb57b6d3ad8da
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-or-user-specific-marathon-service"></a><span data-ttu-id="393cc-104">Tworzenie usługi Marathon specyficznej dla aplikacji lub użytkownika</span><span class="sxs-lookup"><span data-stu-id="393cc-104">Create an application or user-specific Marathon service</span></span>
<span data-ttu-id="393cc-105">Usługa kontenera platformy Azure oferuje zestaw serwerów głównych, na których wstępnie konfigurujemy usługi Apache Mesos i Marathon.</span><span class="sxs-lookup"><span data-stu-id="393cc-105">Azure Container Service provides a set of master servers on which we preconfigure Apache Mesos and Marathon.</span></span> <span data-ttu-id="393cc-106">Mogą to być tooorchestrate używanych aplikacji na powitania klastra, ale najlepiej nie toouse hello serwerów głównych, w tym celu.</span><span class="sxs-lookup"><span data-stu-id="393cc-106">These can be used tooorchestrate your applications on hello cluster, but it's best not toouse hello master servers for this purpose.</span></span> <span data-ttu-id="393cc-107">Na przykład Dostosowywanie konfiguracji hello usługi Marathon wymaga logowania do serwerów głównych hello się i wprowadzania zmian — to unikatowych serwerów głównych, które są nieco inne niż standardowe hello i toobe należy zapewnić opiekę i zarządzanie nimi niezależnie od siebie.</span><span class="sxs-lookup"><span data-stu-id="393cc-107">For example, tweaking hello configuration of Marathon requires logging into hello master servers themselves and making changes--this encourages unique master servers that are a little different from hello standard and need toobe cared for and managed independently.</span></span> <span data-ttu-id="393cc-108">Ponadto Konfiguracja hello wymagana przez jeden zespół może nie być hello konfiguracją optymalną dla innego zespołu.</span><span class="sxs-lookup"><span data-stu-id="393cc-108">Additionally, hello configuration required by one team might not be hello optimal configuration for another team.</span></span>

<span data-ttu-id="393cc-109">W tym artykule wyjaśniamy sposób tooadd usługi Marathon dla aplikacji lub specyficzne dla użytkownika.</span><span class="sxs-lookup"><span data-stu-id="393cc-109">In this article, we'll explain how tooadd an application or user-specific Marathon service.</span></span>

<span data-ttu-id="393cc-110">Ponieważ usługa ta będzie należeć tooa jednego użytkownika lub zespołu, są one wolnego tooconfigure w dowolny sposób, że chcą mieć.</span><span class="sxs-lookup"><span data-stu-id="393cc-110">Because this service will belong tooa single user or team, they are free tooconfigure it in any way that they desire.</span></span> <span data-ttu-id="393cc-111">Usługi kontenera platformy Azure będzie upewnij się również, że usługa hello nadal toorun.</span><span class="sxs-lookup"><span data-stu-id="393cc-111">Also, Azure Container Service will ensure that hello service continues toorun.</span></span> <span data-ttu-id="393cc-112">W przypadku niepowodzenia usługi hello będzie Uruchom usługi kontenera platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="393cc-112">If hello service fails, Azure Container Service will restart it for you.</span></span> <span data-ttu-id="393cc-113">W większości przypadków hello nie nawet widać, że miała przestoju.</span><span class="sxs-lookup"><span data-stu-id="393cc-113">Most of hello time you won't even notice it had downtime.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="393cc-114">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="393cc-114">Prerequisites</span></span>
<span data-ttu-id="393cc-115">[Wdróż wystąpienie usługi kontenera platformy Azure](container-service-deployment.md) z programem orchestrator wpisz DC/OS i [upewnij się, że klient połączenie klastra tooyour](../container-service-connect.md).</span><span class="sxs-lookup"><span data-stu-id="393cc-115">[Deploy an instance of Azure Container Service](container-service-deployment.md) with orchestrator type DC/OS and  [ensure that your client can connect tooyour cluster](../container-service-connect.md).</span></span> <span data-ttu-id="393cc-116">Ponadto hello następujące kroki.</span><span class="sxs-lookup"><span data-stu-id="393cc-116">Also, do hello following steps.</span></span>

[!INCLUDE [install hello DC/OS CLI](../../../includes/container-service-install-dcos-cli-include.md)]

## <a name="create-an-application-or-user-specific-marathon-service"></a><span data-ttu-id="393cc-117">Tworzenie usługi Marathon specyficznej dla aplikacji lub użytkownika</span><span class="sxs-lookup"><span data-stu-id="393cc-117">Create an application or user-specific Marathon service</span></span>
<span data-ttu-id="393cc-118">Rozpocznij od utworzenia pliku konfiguracji JSON, który definiuje nazwę hello hello usługi aplikacji, które mają toocreate.</span><span class="sxs-lookup"><span data-stu-id="393cc-118">Begin by creating a JSON configuration file that defines hello name of hello application service that you want toocreate.</span></span> <span data-ttu-id="393cc-119">W tym miejscu użyjemy `marathon-alice` jako nazwa struktury hello.</span><span class="sxs-lookup"><span data-stu-id="393cc-119">Here we use `marathon-alice` as hello framework name.</span></span> <span data-ttu-id="393cc-120">Zapisz plik hello jako przypominać `marathon-alice.json`:</span><span class="sxs-lookup"><span data-stu-id="393cc-120">Save hello file as something like `marathon-alice.json`:</span></span>

```json
{"marathon": {"framework-name": "marathon-alice" }}
```

<span data-ttu-id="393cc-121">Następnie użyj wystąpienie hello tooinstall hello interfejsu wiersza polecenia DC/OS usługi Marathon z opcjami hello, które są ustawione w pliku konfiguracji:</span><span class="sxs-lookup"><span data-stu-id="393cc-121">Next, use hello DC/OS CLI tooinstall hello Marathon instance with hello options that are set in your configuration file:</span></span>

```bash
dcos package install --options=marathon-alice.json marathon
```

<span data-ttu-id="393cc-122">Powinien zostać wyświetlony z `marathon-alice` usługa jest uruchomiona hello karcie usług interfejsu użytkownika DC/OS.</span><span class="sxs-lookup"><span data-stu-id="393cc-122">You should now see your `marathon-alice` service running in hello Services tab of your DC/OS UI.</span></span> <span data-ttu-id="393cc-123">Witaj interfejs użytkownika zostanie `http://<hostname>/service/marathon-alice/` Jeśli chcesz tooaccess go bezpośrednio.</span><span class="sxs-lookup"><span data-stu-id="393cc-123">hello UI will be `http://<hostname>/service/marathon-alice/` if you want tooaccess it directly.</span></span>

## <a name="set-hello-dcos-cli-tooaccess-hello-service"></a><span data-ttu-id="393cc-124">Ustaw tooaccess interfejsu wiersza polecenia DC/OS hello hello usługę</span><span class="sxs-lookup"><span data-stu-id="393cc-124">Set hello DC/OS CLI tooaccess hello service</span></span>
<span data-ttu-id="393cc-125">Opcjonalnie można skonfigurować sieci tooaccess interfejsu wiersza polecenia DC/OS nowej usługi przez ustawienie hello `marathon.url` toohello toopoint właściwości `marathon-alice` wystąpienia w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="393cc-125">You can optionally configure your DC/OS CLI tooaccess this new service by setting hello `marathon.url` property toopoint toohello `marathon-alice` instance as follows:</span></span>

```bash
dcos config set marathon.url http://<hostname>/service/marathon-alice/
```

<span data-ttu-id="393cc-126">Możesz sprawdzić, którego wystąpienia usługi Marathon, czy interfejs wiersza polecenia działa z hello przed `dcos config show` polecenia.</span><span class="sxs-lookup"><span data-stu-id="393cc-126">You can verify which instance of Marathon that your CLI is working against with hello `dcos config show` command.</span></span> <span data-ttu-id="393cc-127">Możesz przywrócić toousing głównej usługi Marathon przy użyciu polecenia hello `dcos config unset marathon.url`.</span><span class="sxs-lookup"><span data-stu-id="393cc-127">You can revert toousing your master Marathon service with hello command `dcos config unset marathon.url`.</span></span>

