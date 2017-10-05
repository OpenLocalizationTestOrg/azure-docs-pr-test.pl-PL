---
title: "Monitor klastra Azure DC/OS - operacje zarządzania | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 9b8f96b34b53982c469273a3df9751ceb7930d60
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="monitor-an-azure-container-service-dcos-cluster-with-operations-management-suite"></a><span data-ttu-id="6ead7-103">Monitor klastra usługi kontenera platformy Azure DC/OS w usłudze Operations Management Suite</span><span class="sxs-lookup"><span data-stu-id="6ead7-103">Monitor an Azure Container Service DC/OS cluster with Operations Management Suite</span></span>

<span data-ttu-id="6ead7-104">Pakiet Microsoft Operations Management Suite (OMS) to oparte na chmurze rozwiązanie firmy Microsoft do zarządzania systemami IT, które ułatwia zarządzanie infrastrukturą lokalną i chmurową oraz jej ochronę.</span><span class="sxs-lookup"><span data-stu-id="6ead7-104">Microsoft Operations Management Suite (OMS) is Microsoft's cloud-based IT management solution that helps you manage and protect your on-premises and cloud infrastructure.</span></span> <span data-ttu-id="6ead7-105">Kontener rozwiązanie to rozwiązanie w OMS analizy dzienników, które ułatwia przeglądanie spisu kontenera, wydajności i dzienniki w jednej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="6ead7-105">Container Solution is a solution in OMS Log Analytics, which helps you view the container inventory, performance, and logs in a single location.</span></span> <span data-ttu-id="6ead7-106">Można inspekcji, rozwiązywanie problemów z kontenerów, wyświetlając dzienniki w centralnej lokalizacji oraz znaleźć zakłócenia, wykorzystywanie nadmiarowe kontenera na hoście.</span><span class="sxs-lookup"><span data-stu-id="6ead7-106">You can audit, troubleshoot containers by viewing the logs in centralized location, and find noisy consuming excess container on a host.</span></span>

![](media/container-service-monitoring-oms/image1.png)

<span data-ttu-id="6ead7-107">Aby uzyskać więcej informacji o rozwiązaniu kontenera, zapoznaj się [analizy dzienników rozwiązania kontenera](../../log-analytics/log-analytics-containers.md).</span><span class="sxs-lookup"><span data-stu-id="6ead7-107">For more information about Container Solution, please refer to the [Container Solution Log Analytics](../../log-analytics/log-analytics-containers.md).</span></span>

## <a name="setting-up-oms-from-the-dcos-universe"></a><span data-ttu-id="6ead7-108">Konfigurowanie OMS z universe DC/OS</span><span class="sxs-lookup"><span data-stu-id="6ead7-108">Setting up OMS from the DC/OS universe</span></span>


<span data-ttu-id="6ead7-109">W tym artykule założono, że skonfigurowano DC/OS i wdrożeniu aplikacji kontenera sieci web proste w klastrze.</span><span class="sxs-lookup"><span data-stu-id="6ead7-109">This article assumes that you have set up an DC/OS and have deployed simple web container applications on the cluster.</span></span>

### <a name="pre-requisite"></a><span data-ttu-id="6ead7-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="6ead7-110">Pre-requisite</span></span>
- <span data-ttu-id="6ead7-111">[Subskrypcja usługi Microsoft Azure](https://azure.microsoft.com/free/) — można uzyskać tę bezpłatnie.</span><span class="sxs-lookup"><span data-stu-id="6ead7-111">[Microsoft Azure Subscription](https://azure.microsoft.com/free/) - You can get this for free.</span></span>  
- <span data-ttu-id="6ead7-112">Instalator obszar roboczy Microsoft OMS — zobacz "Krok 3" poniżej</span><span class="sxs-lookup"><span data-stu-id="6ead7-112">Microsoft OMS Workspace Setup - see "Step 3" below</span></span>
- <span data-ttu-id="6ead7-113">[Interfejs wiersza polecenia DC/OS](https://dcos.io/docs/1.8/usage/cli/install/) zainstalowane.</span><span class="sxs-lookup"><span data-stu-id="6ead7-113">[DC/OS CLI](https://dcos.io/docs/1.8/usage/cli/install/) installed.</span></span>

1. <span data-ttu-id="6ead7-114">Na pulpicie nawigacyjnym DC/OS kliknij Universe i wyszukaj "OMS", jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="6ead7-114">In the DC/OS dashboard, click on Universe and search for ‘OMS’ as shown below.</span></span>

![](media/container-service-monitoring-oms/image2.png)

2. <span data-ttu-id="6ead7-115">Kliknij pozycję **Zainstaluj**.</span><span class="sxs-lookup"><span data-stu-id="6ead7-115">Click **Install**.</span></span> <span data-ttu-id="6ead7-116">Zobaczysz punktu obecności się z informacjami o wersji OMS i **zainstaluj pakiet** lub **instalacji zaawansowanym** przycisku.</span><span class="sxs-lookup"><span data-stu-id="6ead7-116">You will see a pop up with the OMS version information and an **Install Package** or **Advanced Installation** button.</span></span> <span data-ttu-id="6ead7-117">Po kliknięciu **zaawansowane instalacji**, która prowadzi do **OMS określonej konfiguracji właściwości** strony.</span><span class="sxs-lookup"><span data-stu-id="6ead7-117">When you click **Advanced Installation**, which leads you to the **OMS specific configuration properties** page.</span></span>

![](media/container-service-monitoring-oms/image3.png)

![](media/container-service-monitoring-oms/image4.png)

3. <span data-ttu-id="6ead7-118">W tym miejscu, użytkownik zostanie poproszony o podanie `wsid` (identyfikator obszaru roboczego OMS) i `wskey` (OMS klucz podstawowy identyfikator obszaru roboczego).</span><span class="sxs-lookup"><span data-stu-id="6ead7-118">Here, you will be asked to enter the `wsid` (the OMS workspace ID) and `wskey` (the OMS primary key for the workspace id).</span></span> <span data-ttu-id="6ead7-119">Uzyskanie zarówno `wsid` i `wskey` musisz utworzyć konto OMS w <https://mms.microsoft.com>. Wykonaj kroki, aby utworzyć konto.</span><span class="sxs-lookup"><span data-stu-id="6ead7-119">To get both `wsid` and `wskey` you need to create an OMS account at <https://mms.microsoft.com>. Please follow the steps to create an account.</span></span> <span data-ttu-id="6ead7-120">Po zakończeniu tworzenia konta, musisz uzyskać Twoje `wsid` i `wskey` , klikając **ustawienia**, następnie **połączonych źródeł**, a następnie **serwerówzsystememLinux**, jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="6ead7-120">Once you are done creating the account, you need to obtain your `wsid` and `wskey` by clicking **Settings**, then **Connected Sources**, and then **Linux Servers**, as shown below.</span></span>

 ![](media/container-service-monitoring-oms/image5.png)

4. <span data-ttu-id="6ead7-121">Wybierz numer możesz OMS wystąpienia mają, a następnie kliknij przycisk "Przejrzyj i zainstaluj".</span><span class="sxs-lookup"><span data-stu-id="6ead7-121">Select the number you OMS instances that you want and click the ‘Review and Install’ button.</span></span> <span data-ttu-id="6ead7-122">Zwykle ma mieć liczbę wystąpień OMS równa liczbie maszyny Wirtualnej w klastrze agenta.</span><span class="sxs-lookup"><span data-stu-id="6ead7-122">Typically, you will want to have the number of OMS instances equal to the number of VM’s you have in your agent cluster.</span></span> <span data-ttu-id="6ead7-123">Agent pakietu OMS dla systemu Linux jest instaluje poszczególnych kontenerów na każdej maszynie Wirtualnej, które chcą zebrać informacje dotyczące monitorowania i rejestrowania informacji.</span><span class="sxs-lookup"><span data-stu-id="6ead7-123">OMS Agent for Linux is installs as individual containers on each VM that it wants to collect information for monitoring and logging information.</span></span>

## <a name="setting-up-a-simple-oms-dashboard"></a><span data-ttu-id="6ead7-124">Skonfigurowanie prostego pulpit nawigacyjny OMS</span><span class="sxs-lookup"><span data-stu-id="6ead7-124">Setting up a simple OMS dashboard</span></span>

<span data-ttu-id="6ead7-125">Po zainstalowaniu Agent pakietu OMS dla systemu Linux na maszynach wirtualnych, następnym krokiem jest ustanowienie OMS pulpitu nawigacyjnego.</span><span class="sxs-lookup"><span data-stu-id="6ead7-125">Once you have installed the OMS Agent for Linux on the VMs, next step is to set up the OMS dashboard.</span></span> <span data-ttu-id="6ead7-126">Istnieją dwa sposoby, w tym celu: portalu OMS lub portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="6ead7-126">There are two ways to do this: OMS Portal or Azure Portal.</span></span>

### <a name="oms-portal"></a><span data-ttu-id="6ead7-127">Portalu OMS</span><span class="sxs-lookup"><span data-stu-id="6ead7-127">OMS Portal</span></span> 

<span data-ttu-id="6ead7-128">Zaloguj się do portalu OMS (<https://mms.microsoft.com>) i przejdź do **galerii rozwiązań**.</span><span class="sxs-lookup"><span data-stu-id="6ead7-128">Log in to the OMS portal (<https://mms.microsoft.com>) and go to the **Solution Gallery**.</span></span>

![](media/container-service-monitoring-oms/image6.png)

<span data-ttu-id="6ead7-129">Po przejściu do **galerii rozwiązań**, wybierz pozycję **kontenery**.</span><span class="sxs-lookup"><span data-stu-id="6ead7-129">Once you are in the **Solution Gallery**, select **Containers**.</span></span>

![](media/container-service-monitoring-oms/image7.png)

<span data-ttu-id="6ead7-130">Po wybraniu rozwiązania kontenera, zobaczysz Kafelek na stronie pulpitu nawigacyjnego przeglądu OMS.</span><span class="sxs-lookup"><span data-stu-id="6ead7-130">Once you’ve selected the Container Solution, you will see the tile on the OMS Overview Dashboard page.</span></span> <span data-ttu-id="6ead7-131">Po danych pozyskiwane kontenera jest indeksowana, zostanie wyświetlona kafelka wypełnione informacjami na kafelkach widoku rozwiązania.</span><span class="sxs-lookup"><span data-stu-id="6ead7-131">Once the ingested container data is indexed, you will see the tile populated with information on the solution view tiles.</span></span>

![](media/container-service-monitoring-oms/image8.png)

### <a name="azure-portal"></a><span data-ttu-id="6ead7-132">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="6ead7-132">Azure Portal</span></span> 

<span data-ttu-id="6ead7-133">Zaloguj się do portalu Azure w <https://portal.microsoft.com/>.</span><span class="sxs-lookup"><span data-stu-id="6ead7-133">Login to Azure portal at <https://portal.microsoft.com/>.</span></span> <span data-ttu-id="6ead7-134">Przejdź do **Marketplace**, wybierz pozycję **monitorowanie i zarządzanie** i kliknij przycisk **Zobacz wszystkie**.</span><span class="sxs-lookup"><span data-stu-id="6ead7-134">Go to **Marketplace**, select **Monitoring + management** and click **See All**.</span></span> <span data-ttu-id="6ead7-135">Następnie wpisz `containers` wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="6ead7-135">Then Type `containers` in search.</span></span> <span data-ttu-id="6ead7-136">Zostanie wyświetlone "kontenery" w wynikach wyszukiwania.</span><span class="sxs-lookup"><span data-stu-id="6ead7-136">You will see "containers" in the search results.</span></span> <span data-ttu-id="6ead7-137">Wybierz **kontenery** i kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="6ead7-137">Select **Containers** and click **Create**.</span></span>

![](media/container-service-monitoring-oms/image9.png)

<span data-ttu-id="6ead7-138">Po kliknięciu **Utwórz**, jego wyświetli monit dla obszaru roboczego.</span><span class="sxs-lookup"><span data-stu-id="6ead7-138">Once you click **Create**, it will ask you for your workspace.</span></span> <span data-ttu-id="6ead7-139">Wybierz obszar roboczy lub jeśli nie istnieje, Utwórz nowy obszar roboczy.</span><span class="sxs-lookup"><span data-stu-id="6ead7-139">Select your workspace or if you do not have one, create a new workspace.</span></span>

![](media/container-service-monitoring-oms/image10.PNG)

<span data-ttu-id="6ead7-140">Po wybraniu obszaru roboczego kliknij **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="6ead7-140">Once you’ve selected your workspace, click **Create**.</span></span>

![](media/container-service-monitoring-oms/image11.png)

<span data-ttu-id="6ead7-141">Aby uzyskać więcej informacji o rozwiązaniu kontenera OMS, zapoznaj się [analizy dzienników rozwiązania kontenera](../../log-analytics/log-analytics-containers.md).</span><span class="sxs-lookup"><span data-stu-id="6ead7-141">For more information about the OMS Container Solution, please refer to the [Container Solution Log Analytics](../../log-analytics/log-analytics-containers.md).</span></span>

### <a name="how-to-scale-oms-agent-with-acs-dcos"></a><span data-ttu-id="6ead7-142">Jak skalować Agent pakietu OMS z ACS DC/OS</span><span class="sxs-lookup"><span data-stu-id="6ead7-142">How to scale OMS Agent with ACS DC/OS</span></span> 

<span data-ttu-id="6ead7-143">W przypadku, gdy potrzebne do zainstalowania agenta pakietu OMS jest zbyt mała liczba rzeczywista węzłów lub skalowaniu VMSS, dodając więcej maszyny Wirtualnej, możesz to zrobić przez skalowanie `msoms` usługi.</span><span class="sxs-lookup"><span data-stu-id="6ead7-143">In case you need to have installed OMS agent short of the actual node count or you are scaling up VMSS by adding more VM, you can do so by scaling the `msoms` service.</span></span>

<span data-ttu-id="6ead7-144">Można przejść do Marathon lub na karcie usług interfejsu użytkownika DC/OS i skalowanie w górę liczba węzłów.</span><span class="sxs-lookup"><span data-stu-id="6ead7-144">You can either go to Marathon or the DC/OS UI Services tab and scale up your node count.</span></span>

![](media/container-service-monitoring-oms/image12.PNG)

<span data-ttu-id="6ead7-145">To spowoduje wdrożenie do innych węzłów, które nie zostały jeszcze wdrożone agent pakietu OMS.</span><span class="sxs-lookup"><span data-stu-id="6ead7-145">This will deploy to other nodes which have not yet deployed the OMS agent.</span></span>

## <a name="uninstall-ms-oms"></a><span data-ttu-id="6ead7-146">Odinstaluj MS OMS</span><span class="sxs-lookup"><span data-stu-id="6ead7-146">Uninstall MS OMS</span></span>

<span data-ttu-id="6ead7-147">Aby odinstalować MS OMS, wprowadź następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="6ead7-147">To uninstall MS OMS enter the following command:</span></span>

```bash
$ dcos package uninstall msoms
```

## <a name="let-us-know"></a><span data-ttu-id="6ead7-148">Daj nam znać!</span><span class="sxs-lookup"><span data-stu-id="6ead7-148">Let us know!!!</span></span>
<span data-ttu-id="6ead7-149">Co to działa?</span><span class="sxs-lookup"><span data-stu-id="6ead7-149">What works?</span></span> <span data-ttu-id="6ead7-150">Czego brakuje?</span><span class="sxs-lookup"><span data-stu-id="6ead7-150">What is missing?</span></span> <span data-ttu-id="6ead7-151">Co należy to być przydatne dla Ciebie?</span><span class="sxs-lookup"><span data-stu-id="6ead7-151">What else do you need for this to be useful for you?</span></span> <span data-ttu-id="6ead7-152">Daj nam znać w <a href="mailto:OMSContainers@microsoft.com">OMSContainers</a>.</span><span class="sxs-lookup"><span data-stu-id="6ead7-152">Let us know at <a href="mailto:OMSContainers@microsoft.com">OMSContainers</a>.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6ead7-153">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="6ead7-153">Next steps</span></span>

 <span data-ttu-id="6ead7-154">Teraz, kiedy OMS zostały skonfigurowane do monitorowania kontenerów,[Zobacz Pulpit nawigacyjny kontenera](../../log-analytics/log-analytics-containers.md).</span><span class="sxs-lookup"><span data-stu-id="6ead7-154">Now that you have set up OMS to monitor your containers,[see your container dashboard](../../log-analytics/log-analytics-containers.md).</span></span>
