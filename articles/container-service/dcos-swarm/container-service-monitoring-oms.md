---
title: klaster Azure DC/OS aaaMonitor - Operations Management | Dokumentacja firmy Microsoft
description: "Monitorowanie klastra usługi kontenera platformy Azure DC/OS z programu Microsoft Operations Management Suite."
services: container-service
documentationcenter: 
author: keikhara
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure
ms.date: 11/17/2016
ms.author: keikhara
ms.custom: mvc
ms.openlocfilehash: 0ebfa3ba3cef8f0205b15731b0e91f5b304bc8fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-dcos-cluster-with-operations-management-suite"></a><span data-ttu-id="5d146-103">Monitor klastra usługi kontenera platformy Azure DC/OS w usłudze Operations Management Suite</span><span class="sxs-lookup"><span data-stu-id="5d146-103">Monitor an Azure Container Service DC/OS cluster with Operations Management Suite</span></span>

<span data-ttu-id="5d146-104">Pakiet Microsoft Operations Management Suite (OMS) to oparte na chmurze rozwiązanie firmy Microsoft do zarządzania systemami IT, które ułatwia zarządzanie infrastrukturą lokalną i chmurową oraz jej ochronę.</span><span class="sxs-lookup"><span data-stu-id="5d146-104">Microsoft Operations Management Suite (OMS) is Microsoft's cloud-based IT management solution that helps you manage and protect your on-premises and cloud infrastructure.</span></span> <span data-ttu-id="5d146-105">Kontener rozwiązanie to rozwiązanie w OMS Log Analytics, który pomaga w widoku hello kontenera magazynu, wydajności i dzienniki w jednej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="5d146-105">Container Solution is a solution in OMS Log Analytics, which helps you view hello container inventory, performance, and logs in a single location.</span></span> <span data-ttu-id="5d146-106">Można inspekcji, rozwiązywanie problemów z kontenerów, wyświetlając hello dzienniki w centralnej lokalizacji oraz znaleźć zakłócenia, wykorzystywanie nadmiarowe kontenera na hoście.</span><span class="sxs-lookup"><span data-stu-id="5d146-106">You can audit, troubleshoot containers by viewing hello logs in centralized location, and find noisy consuming excess container on a host.</span></span>

![](media/container-service-monitoring-oms/image1.png)

<span data-ttu-id="5d146-107">Aby uzyskać więcej informacji o rozwiązaniu kontenera, zobacz toothe [analizy dzienników rozwiązania kontenera](../../log-analytics/log-analytics-containers.md).</span><span class="sxs-lookup"><span data-stu-id="5d146-107">For more information about Container Solution, please refer toothe [Container Solution Log Analytics](../../log-analytics/log-analytics-containers.md).</span></span>

## <a name="setting-up-oms-from-hello-dcos-universe"></a><span data-ttu-id="5d146-108">Konfigurowanie OMS z hello DC/OS universe</span><span class="sxs-lookup"><span data-stu-id="5d146-108">Setting up OMS from hello DC/OS universe</span></span>


<span data-ttu-id="5d146-109">W tym artykule założono, że skonfigurowano DC/OS i wdrożeniu aplikacji kontenera sieci web prostego na powitania klastra.</span><span class="sxs-lookup"><span data-stu-id="5d146-109">This article assumes that you have set up an DC/OS and have deployed simple web container applications on hello cluster.</span></span>

### <a name="pre-requisite"></a><span data-ttu-id="5d146-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="5d146-110">Pre-requisite</span></span>
- <span data-ttu-id="5d146-111">[Subskrypcja usługi Microsoft Azure](https://azure.microsoft.com/free/) — można uzyskać tę bezpłatnie.</span><span class="sxs-lookup"><span data-stu-id="5d146-111">[Microsoft Azure Subscription](https://azure.microsoft.com/free/) - You can get this for free.</span></span>  
- <span data-ttu-id="5d146-112">Instalator obszar roboczy Microsoft OMS — zobacz "Krok 3" poniżej</span><span class="sxs-lookup"><span data-stu-id="5d146-112">Microsoft OMS Workspace Setup - see "Step 3" below</span></span>
- <span data-ttu-id="5d146-113">[Interfejs wiersza polecenia DC/OS](https://dcos.io/docs/1.8/usage/cli/install/) zainstalowane.</span><span class="sxs-lookup"><span data-stu-id="5d146-113">[DC/OS CLI](https://dcos.io/docs/1.8/usage/cli/install/) installed.</span></span>

1. <span data-ttu-id="5d146-114">Na pulpicie nawigacyjnym DC/OS hello kliknij Universe i wyszukaj "OMS", jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="5d146-114">In hello DC/OS dashboard, click on Universe and search for ‘OMS’ as shown below.</span></span>

![](media/container-service-monitoring-oms/image2.png)

2. <span data-ttu-id="5d146-115">Kliknij pozycję **Zainstaluj**.</span><span class="sxs-lookup"><span data-stu-id="5d146-115">Click **Install**.</span></span> <span data-ttu-id="5d146-116">Zobaczysz punktu obecności się z informacjami o wersji OMS hello i **zainstaluj pakiet** lub **instalacji zaawansowanym** przycisku.</span><span class="sxs-lookup"><span data-stu-id="5d146-116">You will see a pop up with hello OMS version information and an **Install Package** or **Advanced Installation** button.</span></span> <span data-ttu-id="5d146-117">Po kliknięciu **zaawansowane instalacji**, który poprowadzi Cię toohello **OMS określonej konfiguracji właściwości** strony.</span><span class="sxs-lookup"><span data-stu-id="5d146-117">When you click **Advanced Installation**, which leads you toohello **OMS specific configuration properties** page.</span></span>

![](media/container-service-monitoring-oms/image3.png)

![](media/container-service-monitoring-oms/image4.png)

3. <span data-ttu-id="5d146-118">W tym miejscu, konieczne będzie podanie tooenter hello `wsid` (hello identyfikator obszaru roboczego OMS) i `wskey` (hello OMS klucz podstawowy dla hello identyfikator obszaru roboczego).</span><span class="sxs-lookup"><span data-stu-id="5d146-118">Here, you will be asked tooenter hello `wsid` (hello OMS workspace ID) and `wskey` (hello OMS primary key for hello workspace id).</span></span> <span data-ttu-id="5d146-119">tooget zarówno `wsid` i `wskey` toocreate potrzebne jest konto OMS na <https://mms.microsoft.com>. Wykonaj hello kroki toocreate konta.</span><span class="sxs-lookup"><span data-stu-id="5d146-119">tooget both `wsid` and `wskey` you need toocreate an OMS account at <https://mms.microsoft.com>. Please follow hello steps toocreate an account.</span></span> <span data-ttu-id="5d146-120">Po zakończeniu tworzenia konta hello należy tooobtain Twojego `wsid` i `wskey` klikając **ustawienia**, następnie **połączonych źródeł**, a następnie **serwerów z systemem Linux** , jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="5d146-120">Once you are done creating hello account, you need tooobtain your `wsid` and `wskey` by clicking **Settings**, then **Connected Sources**, and then **Linux Servers**, as shown below.</span></span>

 ![](media/container-service-monitoring-oms/image5.png)

4. <span data-ttu-id="5d146-121">Wybierz hello numer możesz OMS wystąpienia i kliknij przycisk "Przejrzyj i zainstaluj" hello.</span><span class="sxs-lookup"><span data-stu-id="5d146-121">Select hello number you OMS instances that you want and click hello ‘Review and Install’ button.</span></span> <span data-ttu-id="5d146-122">Zazwyczaj można toohave hello liczby OMS wystąpień równy toohello maszyny Wirtualnej w klastrze agenta.</span><span class="sxs-lookup"><span data-stu-id="5d146-122">Typically, you will want toohave hello number of OMS instances equal toohello number of VM’s you have in your agent cluster.</span></span> <span data-ttu-id="5d146-123">Agent pakietu OMS dla systemu Linux jest instaluje poszczególnych kontenerów na każdej maszynie Wirtualnej, że chce toocollect informacje dotyczące monitorowania i rejestrowania informacji.</span><span class="sxs-lookup"><span data-stu-id="5d146-123">OMS Agent for Linux is installs as individual containers on each VM that it wants toocollect information for monitoring and logging information.</span></span>

## <a name="setting-up-a-simple-oms-dashboard"></a><span data-ttu-id="5d146-124">Skonfigurowanie prostego pulpit nawigacyjny OMS</span><span class="sxs-lookup"><span data-stu-id="5d146-124">Setting up a simple OMS dashboard</span></span>

<span data-ttu-id="5d146-125">Po zainstalowaniu hello Agent pakietu OMS dla systemu Linux na maszynach wirtualnych hello, następnym krokiem jest tooset się hello OMS z pulpitu nawigacyjnego.</span><span class="sxs-lookup"><span data-stu-id="5d146-125">Once you have installed hello OMS Agent for Linux on hello VMs, next step is tooset up hello OMS dashboard.</span></span> <span data-ttu-id="5d146-126">Istnieją dwa sposoby toodo to: portalu OMS lub portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="5d146-126">There are two ways toodo this: OMS Portal or Azure Portal.</span></span>

### <a name="oms-portal"></a><span data-ttu-id="5d146-127">Portalu OMS</span><span class="sxs-lookup"><span data-stu-id="5d146-127">OMS Portal</span></span> 

<span data-ttu-id="5d146-128">Zaloguj się w portalu OMS toohello (<https://mms.microsoft.com>) i przejdź toohello **galerii rozwiązań**.</span><span class="sxs-lookup"><span data-stu-id="5d146-128">Log in toohello OMS portal (<https://mms.microsoft.com>) and go toohello **Solution Gallery**.</span></span>

![](media/container-service-monitoring-oms/image6.png)

<span data-ttu-id="5d146-129">Po przejściu do hello **galerii rozwiązań**, wybierz pozycję **kontenery**.</span><span class="sxs-lookup"><span data-stu-id="5d146-129">Once you are in hello **Solution Gallery**, select **Containers**.</span></span>

![](media/container-service-monitoring-oms/image7.png)

<span data-ttu-id="5d146-130">Po wybraniu hello rozwiązania kontenera, zobaczysz hello kafelka na stronie pulpitu nawigacyjnego przeglądu OMS hello.</span><span class="sxs-lookup"><span data-stu-id="5d146-130">Once you’ve selected hello Container Solution, you will see hello tile on hello OMS Overview Dashboard page.</span></span> <span data-ttu-id="5d146-131">Po dane w kontenerze hello pozyskanych jest indeksowana, zostanie wyświetlona kafelka hello wypełnione informacjami na kafelkach widoku rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="5d146-131">Once hello ingested container data is indexed, you will see hello tile populated with information on the solution view tiles.</span></span>

![](media/container-service-monitoring-oms/image8.png)

### <a name="azure-portal"></a><span data-ttu-id="5d146-132">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="5d146-132">Azure Portal</span></span> 

<span data-ttu-id="5d146-133">Portal tooAzure logowania w <https://portal.microsoft.com/>.</span><span class="sxs-lookup"><span data-stu-id="5d146-133">Login tooAzure portal at <https://portal.microsoft.com/>.</span></span> <span data-ttu-id="5d146-134">Przejdź do **Marketplace**, wybierz pozycję **monitorowanie i zarządzanie** i kliknij przycisk **Zobacz wszystkie**.</span><span class="sxs-lookup"><span data-stu-id="5d146-134">Go to **Marketplace**, select **Monitoring + management** and click **See All**.</span></span> <span data-ttu-id="5d146-135">Następnie wpisz `containers` wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="5d146-135">Then Type `containers` in search.</span></span> <span data-ttu-id="5d146-136">Zostanie wyświetlone "kontenery" w wynikach wyszukiwania hello.</span><span class="sxs-lookup"><span data-stu-id="5d146-136">You will see "containers" in hello search results.</span></span> <span data-ttu-id="5d146-137">Wybierz **kontenery** i kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="5d146-137">Select **Containers** and click **Create**.</span></span>

![](media/container-service-monitoring-oms/image9.png)

<span data-ttu-id="5d146-138">Po kliknięciu **Utwórz**, jego wyświetli monit dla obszaru roboczego.</span><span class="sxs-lookup"><span data-stu-id="5d146-138">Once you click **Create**, it will ask you for your workspace.</span></span> <span data-ttu-id="5d146-139">Wybierz obszar roboczy lub jeśli nie istnieje, Utwórz nowy obszar roboczy.</span><span class="sxs-lookup"><span data-stu-id="5d146-139">Select your workspace or if you do not have one, create a new workspace.</span></span>

![](media/container-service-monitoring-oms/image10.PNG)

<span data-ttu-id="5d146-140">Po wybraniu obszaru roboczego kliknij **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="5d146-140">Once you’ve selected your workspace, click **Create**.</span></span>

![](media/container-service-monitoring-oms/image11.png)

<span data-ttu-id="5d146-141">Aby uzyskać więcej informacji na temat hello OMS kontenera rozwiązania, zobacz toothe [analizy dzienników rozwiązania kontenera](../../log-analytics/log-analytics-containers.md).</span><span class="sxs-lookup"><span data-stu-id="5d146-141">For more information about hello OMS Container Solution, please refer toothe [Container Solution Log Analytics](../../log-analytics/log-analytics-containers.md).</span></span>

### <a name="how-tooscale-oms-agent-with-acs-dcos"></a><span data-ttu-id="5d146-142">Jak tooscale Agent pakietu OMS z ACS DC/OS</span><span class="sxs-lookup"><span data-stu-id="5d146-142">How tooscale OMS Agent with ACS DC/OS</span></span> 

<span data-ttu-id="5d146-143">W przypadku należy toohave zainstalowany agent pakietu OMS jest zbyt mała liczba rzeczywista węzłów hello lub skalowaniu VMSS, dodając więcej maszyny Wirtualnej, możesz to zrobić przez skalowanie hello `msoms` usługi.</span><span class="sxs-lookup"><span data-stu-id="5d146-143">In case you need toohave installed OMS agent short of hello actual node count or you are scaling up VMSS by adding more VM, you can do so by scaling hello `msoms` service.</span></span>

<span data-ttu-id="5d146-144">Można go tooMarathon lub hello na karcie usług interfejsu użytkownika DC/OS i skalowanie w górę liczba węzłów.</span><span class="sxs-lookup"><span data-stu-id="5d146-144">You can either go tooMarathon or hello DC/OS UI Services tab and scale up your node count.</span></span>

![](media/container-service-monitoring-oms/image12.PNG)

<span data-ttu-id="5d146-145">To spowoduje wdrożenie tooother węzły, które nie zostały jeszcze wdrożone hello agent pakietu OMS.</span><span class="sxs-lookup"><span data-stu-id="5d146-145">This will deploy tooother nodes which have not yet deployed hello OMS agent.</span></span>

## <a name="uninstall-ms-oms"></a><span data-ttu-id="5d146-146">Odinstaluj MS OMS</span><span class="sxs-lookup"><span data-stu-id="5d146-146">Uninstall MS OMS</span></span>

<span data-ttu-id="5d146-147">toouninstall MS OMS wprowadź hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="5d146-147">toouninstall MS OMS enter hello following command:</span></span>

```bash
$ dcos package uninstall msoms
```

## <a name="let-us-know"></a><span data-ttu-id="5d146-148">Daj nam znać!</span><span class="sxs-lookup"><span data-stu-id="5d146-148">Let us know!!!</span></span>
<span data-ttu-id="5d146-149">Co to działa?</span><span class="sxs-lookup"><span data-stu-id="5d146-149">What works?</span></span> <span data-ttu-id="5d146-150">Czego brakuje?</span><span class="sxs-lookup"><span data-stu-id="5d146-150">What is missing?</span></span> <span data-ttu-id="5d146-151">Co potrzebujesz dla tego toobe przydatne dla Ciebie?</span><span class="sxs-lookup"><span data-stu-id="5d146-151">What else do you need for this toobe useful for you?</span></span> <span data-ttu-id="5d146-152">Daj nam znać w <a href="mailto:OMSContainers@microsoft.com">OMSContainers</a>.</span><span class="sxs-lookup"><span data-stu-id="5d146-152">Let us know at <a href="mailto:OMSContainers@microsoft.com">OMSContainers</a>.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5d146-153">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="5d146-153">Next steps</span></span>

 <span data-ttu-id="5d146-154">Teraz, po skonfigurowaniu OMS toomonitor kontenerów,[Zobacz Pulpit nawigacyjny kontenera](../../log-analytics/log-analytics-containers.md).</span><span class="sxs-lookup"><span data-stu-id="5d146-154">Now that you have set up OMS toomonitor your containers,[see your container dashboard](../../log-analytics/log-analytics-containers.md).</span></span>
