---
title: "Usługa Marathon specyficzna dla aplikacji lub użytkownika | Microsoft Docs"
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
ms.openlocfilehash: b265763fb5dad240edd710cd8d0fb1079e3a7b51
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="create-an-application-or-user-specific-marathon-service"></a><span data-ttu-id="2c4c4-104">Tworzenie usługi Marathon specyficznej dla aplikacji lub użytkownika</span><span class="sxs-lookup"><span data-stu-id="2c4c4-104">Create an application or user-specific Marathon service</span></span>
<span data-ttu-id="2c4c4-105">Usługa kontenera platformy Azure oferuje zestaw serwerów głównych, na których wstępnie konfigurujemy usługi Apache Mesos i Marathon.</span><span class="sxs-lookup"><span data-stu-id="2c4c4-105">Azure Container Service provides a set of master servers on which we preconfigure Apache Mesos and Marathon.</span></span> <span data-ttu-id="2c4c4-106">Mogą one być używane do organizowania aplikacji w klastrze, ale stosowanie w tym celu serwerów głównych nie jest zalecane.</span><span class="sxs-lookup"><span data-stu-id="2c4c4-106">These can be used to orchestrate your applications on the cluster, but it's best not to use the master servers for this purpose.</span></span> <span data-ttu-id="2c4c4-107">Na przykład dostosowywanie konfiguracji usługi Marathon wymaga logowania do serwerów głównych i wprowadzania zmian. Oznacza to, że należy używać unikatowych serwerów głównych, które są nieco inne niż standardowe i wymagają niezależnej obsługi oraz zarządzania.</span><span class="sxs-lookup"><span data-stu-id="2c4c4-107">For example, tweaking the configuration of Marathon requires logging into the master servers themselves and making changes--this encourages unique master servers that are a little different from the standard and need to be cared for and managed independently.</span></span> <span data-ttu-id="2c4c4-108">Ponadto konfiguracja wymagana przez jeden zespół może nie być konfiguracją optymalną dla innego zespołu.</span><span class="sxs-lookup"><span data-stu-id="2c4c4-108">Additionally, the configuration required by one team might not be the optimal configuration for another team.</span></span>

<span data-ttu-id="2c4c4-109">W tym artykule wyjaśnimy, jak dodać usługę Marathon specyficzną dla aplikacji lub użytkownika.</span><span class="sxs-lookup"><span data-stu-id="2c4c4-109">In this article, we'll explain how to add an application or user-specific Marathon service.</span></span>

<span data-ttu-id="2c4c4-110">Ponieważ usługa ta będzie należeć do pojedynczego użytkownika lub zespołu, będzie można w dowolny sposób skonfigurować jej działanie.</span><span class="sxs-lookup"><span data-stu-id="2c4c4-110">Because this service will belong to a single user or team, they are free to configure it in any way that they desire.</span></span> <span data-ttu-id="2c4c4-111">Ponadto usługa Azure Container Service zapewni ciągłość działania usługi.</span><span class="sxs-lookup"><span data-stu-id="2c4c4-111">Also, Azure Container Service will ensure that the service continues to run.</span></span> <span data-ttu-id="2c4c4-112">Jeśli wystąpi awaria usługi, usługa Azure Container Service uruchomi ją ponownie.</span><span class="sxs-lookup"><span data-stu-id="2c4c4-112">If the service fails, Azure Container Service will restart it for you.</span></span> <span data-ttu-id="2c4c4-113">W większości przypadków taki przestój będzie niezauważalny.</span><span class="sxs-lookup"><span data-stu-id="2c4c4-113">Most of the time you won't even notice it had downtime.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2c4c4-114">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="2c4c4-114">Prerequisites</span></span>
<span data-ttu-id="2c4c4-115">[Wdróż wystąpienie usługi Azure Container Service](container-service-deployment.md) z typem aranżacji DCOS i [upewnij się, że klient może połączyć się z klastrem](../container-service-connect.md).</span><span class="sxs-lookup"><span data-stu-id="2c4c4-115">[Deploy an instance of Azure Container Service](container-service-deployment.md) with orchestrator type DC/OS and  [ensure that your client can connect to your cluster](../container-service-connect.md).</span></span> <span data-ttu-id="2c4c4-116">Ponadto wykonaj poniższe kroki.</span><span class="sxs-lookup"><span data-stu-id="2c4c4-116">Also, do the following steps.</span></span>

[!INCLUDE [install the DC/OS CLI](../../../includes/container-service-install-dcos-cli-include.md)]

## <a name="create-an-application-or-user-specific-marathon-service"></a><span data-ttu-id="2c4c4-117">Tworzenie usługi Marathon specyficznej dla aplikacji lub użytkownika</span><span class="sxs-lookup"><span data-stu-id="2c4c4-117">Create an application or user-specific Marathon service</span></span>
<span data-ttu-id="2c4c4-118">Rozpocznij od utworzenia pliku konfiguracji JSON definiującego nazwę usługi aplikacji, którą chcesz utworzyć.</span><span class="sxs-lookup"><span data-stu-id="2c4c4-118">Begin by creating a JSON configuration file that defines the name of the application service that you want to create.</span></span> <span data-ttu-id="2c4c4-119">W tym miejscu użyjemy ciągu `marathon-alice` jako nazwy szablonu.</span><span class="sxs-lookup"><span data-stu-id="2c4c4-119">Here we use `marathon-alice` as the framework name.</span></span> <span data-ttu-id="2c4c4-120">Zapisz plik z nazwą typu `marathon-alice.json`:</span><span class="sxs-lookup"><span data-stu-id="2c4c4-120">Save the file as something like `marathon-alice.json`:</span></span>

```json
{"marathon": {"framework-name": "marathon-alice" }}
```

<span data-ttu-id="2c4c4-121">Następnie użyj interfejsu wiersza polecenia DC/OS, aby zainstalować wystąpienie usługi Marathon z opcjami ustawionymi w pliku konfiguracji:</span><span class="sxs-lookup"><span data-stu-id="2c4c4-121">Next, use the DC/OS CLI to install the Marathon instance with the options that are set in your configuration file:</span></span>

```bash
dcos package install --options=marathon-alice.json marathon
```

<span data-ttu-id="2c4c4-122">Usługa `marathon-alice` powinna teraz zostać wyświetlona jako działająca na karcie usług interfejsu użytkownika DC/OS.</span><span class="sxs-lookup"><span data-stu-id="2c4c4-122">You should now see your `marathon-alice` service running in the Services tab of your DC/OS UI.</span></span> <span data-ttu-id="2c4c4-123">Jeśli chcesz bezpośrednio uzyskiwać dostęp do interfejsu użytkownika, zostanie użyta wartość `http://<hostname>/service/marathon-alice/`.</span><span class="sxs-lookup"><span data-stu-id="2c4c4-123">The UI will be `http://<hostname>/service/marathon-alice/` if you want to access it directly.</span></span>

## <a name="set-the-dcos-cli-to-access-the-service"></a><span data-ttu-id="2c4c4-124">Ustawianie interfejsu wiersza polecenia DC/OS w celu uzyskiwania dostępu do usługi</span><span class="sxs-lookup"><span data-stu-id="2c4c4-124">Set the DC/OS CLI to access the service</span></span>
<span data-ttu-id="2c4c4-125">Opcjonalnie możesz skonfigurować interfejs wiersza polecenia DC/OS do uzyskiwania dostępu do nowej usługi, ustawiając właściwość `marathon.url`, aby wskazywała wystąpienie `marathon-alice` w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="2c4c4-125">You can optionally configure your DC/OS CLI to access this new service by setting the `marathon.url` property to point to the `marathon-alice` instance as follows:</span></span>

```bash
dcos config set marathon.url http://<hostname>/service/marathon-alice/
```

<span data-ttu-id="2c4c4-126">Możesz sprawdzić, z jakim wystąpieniem usługi Marathon działa interfejs wiersza polecenia, używając polecenia `dcos config show`.</span><span class="sxs-lookup"><span data-stu-id="2c4c4-126">You can verify which instance of Marathon that your CLI is working against with the `dcos config show` command.</span></span> <span data-ttu-id="2c4c4-127">Możesz wrócić do korzystania z głównej usługi Marathon przy użyciu polecenia `dcos config unset marathon.url`.</span><span class="sxs-lookup"><span data-stu-id="2c4c4-127">You can revert to using your master Marathon service with the command `dcos config unset marathon.url`.</span></span>

