---
title: klaster aaaDeploy kontenera Docker na platformie Azure | Dokumentacja firmy Microsoft
description: "Wdrażanie rozwiązania Kubernetes, DC/OS lub Docker Swarm usługi kontenera platformy Azure przy użyciu portalu Azure hello lub szablonu usługi Resource Manager."
services: container-service
documentationcenter: 
author: rgardler
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: Docker, Containers, Micro-services, Mesos, Azure, dcos, swarm, kubernetes, azure container service, acs
ms.service: container-service
ms.devlang: na
ms.topic: quickstart
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/01/2017
ms.author: rogardle
ms.custom: H1Hack27Feb2017, mvc
ms.openlocfilehash: 26e3a7d0af9d71acd8b5c85fd667fcf7d84cef66
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-docker-container-hosting-solution-using-hello-azure-portal"></a><span data-ttu-id="ce8e5-104">Wdrażanie rozwiązania przy użyciu portalu Azure hello hostingu kontener Docker</span><span class="sxs-lookup"><span data-stu-id="ce8e5-104">Deploy a Docker container hosting solution using hello Azure portal</span></span>



<span data-ttu-id="ce8e5-105">Usługa kontenera platformy Azure zapewnia szybkie wdrażanie popularnych rozwiązań typu open source służących do aranżowania i klastrowania kontenerów.</span><span class="sxs-lookup"><span data-stu-id="ce8e5-105">Azure Container Service provides rapid deployment of popular open-source container clustering and orchestration solutions.</span></span> <span data-ttu-id="ce8e5-106">Ten dokument zawiera opis kroków wdrażania klastra usługi kontenera platformy Azure przy użyciu hello portalu Azure lub szablon szybkiego startu usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="ce8e5-106">This document walks you through deploying an Azure Container Service cluster by using hello Azure portal or an Azure Resource Manager quickstart template.</span></span> 

<span data-ttu-id="ce8e5-107">Można także wdrożyć klaster usługi kontenera platformy Azure przy użyciu hello [Azure CLI 2.0](container-service-create-acs-cluster-cli.md) lub hello interfejsów API usługi kontenera platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="ce8e5-107">You can also deploy an Azure Container Service cluster by using hello [Azure CLI 2.0](container-service-create-acs-cluster-cli.md) or hello Azure Container Service APIs.</span></span>

<span data-ttu-id="ce8e5-108">Aby uzyskać ogólne informacje, zobacz [Wprowadzenie do usługi Azure Container Service](../container-service-intro.md).</span><span class="sxs-lookup"><span data-stu-id="ce8e5-108">For background, see [Azure Container Service introduction](../container-service-intro.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="ce8e5-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="ce8e5-109">Prerequisites</span></span>

* <span data-ttu-id="ce8e5-110">**Subskrypcja platformy Azure**: jeśli jej nie masz, możesz utworzyć konto [bezpłatnej wersji próbnej](http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=AA4C1C935).</span><span class="sxs-lookup"><span data-stu-id="ce8e5-110">**Azure subscription**: If you don't have one, sign up for a [free trial](http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=AA4C1C935).</span></span> <span data-ttu-id="ce8e5-111">W przypadku większego klastra warto rozważyć subskrypcję opartą na płatności zgodnie z rzeczywistym użyciem lub inne opcje zakupu.</span><span class="sxs-lookup"><span data-stu-id="ce8e5-111">For a larger cluster, consider a pay-as-you go subscription or other purchase options.</span></span>

    > [!NOTE]
    > <span data-ttu-id="ce8e5-112">Użycie subskrypcji platformy Azure i [przydziałami zasobów](../../azure-subscription-service-limits.md), takie jak limity przydziału rdzeni, można ograniczyć hello rozmiar klastra hello wdrażania.</span><span class="sxs-lookup"><span data-stu-id="ce8e5-112">Your Azure subscription usage and [resource quotas](../../azure-subscription-service-limits.md), such as cores quotas, can limit hello size of hello cluster you deploy.</span></span> <span data-ttu-id="ce8e5-113">toorequest zwiększenia limitu przydziału, otwórz [żądania obsługi online klienta](../../azure-supportability/how-to-create-azure-support-request.md) bez dodatkowych opłat.</span><span class="sxs-lookup"><span data-stu-id="ce8e5-113">toorequest a quota increase, open an [online customer support request](../../azure-supportability/how-to-create-azure-support-request.md) at no charge.</span></span>
    >

* <span data-ttu-id="ce8e5-114">**Klucz publiczny SSH RSA**: w przypadku wdrażania, za pośrednictwem portalu hello lub jednego z szablonów Szybki Start Azure hello, wymaga klucza publicznego hello tooprovide do uwierzytelniania względem usługi kontenera platformy Azure, maszyny wirtualne.</span><span class="sxs-lookup"><span data-stu-id="ce8e5-114">**SSH RSA public key**: When deploying through hello portal or one of hello Azure quickstart templates, you need tooprovide hello public key for authentication against Azure Container Service virtual machines.</span></span> <span data-ttu-id="ce8e5-115">toocreate kluczy RSA Secure Shell (SSH), zobacz hello [OS X i Linux](../../virtual-machines/linux/mac-create-ssh-keys.md) lub [Windows](../../virtual-machines/linux/ssh-from-windows.md) wskazówki.</span><span class="sxs-lookup"><span data-stu-id="ce8e5-115">toocreate Secure Shell (SSH) RSA keys, see hello [OS X and Linux](../../virtual-machines/linux/mac-create-ssh-keys.md) or [Windows](../../virtual-machines/linux/ssh-from-windows.md) guidance.</span></span> 

* <span data-ttu-id="ce8e5-116">**Identyfikator podmiotu zabezpieczeń klienta i klucz tajny usługi Service** (tylko Kubernetes): Aby uzyskać więcej informacji i wskazówek toocreate nazwy głównej usługi Azure Active Directory, zobacz [o hello nazwy głównej usługi dla klastra Kubernetes](../kubernetes/container-service-kubernetes-service-principal.md).</span><span class="sxs-lookup"><span data-stu-id="ce8e5-116">**Service principal client ID and secret** (Kubernetes only): For more information and guidance toocreate an Azure Active Directory service principal, see [About hello service principal for a Kubernetes cluster](../kubernetes/container-service-kubernetes-service-principal.md).</span></span>



## <a name="create-a-cluster-by-using-hello-azure-portal"></a><span data-ttu-id="ce8e5-117">Tworzenie klastra przy użyciu hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="ce8e5-117">Create a cluster by using hello Azure portal</span></span>
1. <span data-ttu-id="ce8e5-118">Wybierz zalogować się w portalu Azure, toohello **nowy**i wyszukiwania hello Azure Marketplace w celu **usługi kontenera platformy Azure**.</span><span class="sxs-lookup"><span data-stu-id="ce8e5-118">Sign in toohello Azure portal, select **New**, and search hello Azure Marketplace for **Azure Container Service**.</span></span>

    ![Usługa Azure Container Service w portalu Marketplace](./media/container-service-deployment/acs-portal1.png)  <br />

2. <span data-ttu-id="ce8e5-120">Kliknij pozycję **Azure Container Service**, a następnie kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="ce8e5-120">Click **Azure Container Service**, and click **Create**.</span></span>

3. <span data-ttu-id="ce8e5-121">Na powitania **podstawy** bloku, wprowadź hello następujących informacji:</span><span class="sxs-lookup"><span data-stu-id="ce8e5-121">On hello **Basics** blade, enter hello following information:</span></span>

    * <span data-ttu-id="ce8e5-122">**Orchestrator**: Wybierz jedno z toodeploy orchestrators kontenera hello na powitania klastra.</span><span class="sxs-lookup"><span data-stu-id="ce8e5-122">**Orchestrator**: Select one of hello container orchestrators toodeploy on hello cluster.</span></span>
        * <span data-ttu-id="ce8e5-123">**DC/OS**: wdraża klaster DC/OS.</span><span class="sxs-lookup"><span data-stu-id="ce8e5-123">**DC/OS**: Deploys a DC/OS cluster.</span></span>
        * <span data-ttu-id="ce8e5-124">**Swarm**: wdraża klaster Docker Swarm.</span><span class="sxs-lookup"><span data-stu-id="ce8e5-124">**Swarm**: Deploys a Docker Swarm cluster.</span></span>
        * <span data-ttu-id="ce8e5-125">**Kubernetes**: wdraża klaster Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="ce8e5-125">**Kubernetes**: Deploys a Kubernetes cluster.</span></span>
    * <span data-ttu-id="ce8e5-126">**Subskrypcja**: wybierz subskrypcję platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="ce8e5-126">**Subscription**: Select an Azure subscription.</span></span>
    * <span data-ttu-id="ce8e5-127">**Grupa zasobów**: Wprowadź nazwę nowej grupy zasobów hello hello wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="ce8e5-127">**Resource group**: Enter hello name of a new resource group for hello deployment.</span></span>
    * <span data-ttu-id="ce8e5-128">**Lokalizacja**: Wybierz region platformy Azure dla hello wdrożenia usługi kontenera platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="ce8e5-128">**Location**: Select an Azure region for hello Azure Container Service deployment.</span></span> <span data-ttu-id="ce8e5-129">Aby uzyskać informacje o dostępności, zobacz [Dostępność produktów według regionów](https://azure.microsoft.com/regions/services/).</span><span class="sxs-lookup"><span data-stu-id="ce8e5-129">For availability, check [Products available by region](https://azure.microsoft.com/regions/services/).</span></span>
    
    ![Ustawienia podstawowe](./media/container-service-deployment/acs-portal3.png)  <br />
    
    <span data-ttu-id="ce8e5-131">Kliknij przycisk **OK** gdy wszystko będzie gotowe tooproceed.</span><span class="sxs-lookup"><span data-stu-id="ce8e5-131">Click **OK** when you're ready tooproceed.</span></span>

4. <span data-ttu-id="ce8e5-132">Na powitania **wzorca konfiguracji** bloku, wprowadź hello następujące ustawienia dla węzła głównego Linux hello lub w węzłach klastra hello (niektóre ustawienia są określone tooeach orchestrator):</span><span class="sxs-lookup"><span data-stu-id="ce8e5-132">On hello **Master configuration** blade, enter hello following settings for hello Linux master node or nodes in hello cluster (some settings are specific tooeach orchestrator):</span></span>

    * <span data-ttu-id="ce8e5-133">**Nazwa DNS wzorca**: hello prefiks toocreate unikatową w pełni kwalifikowana nazwa domeny (FQDN) głównego hello.</span><span class="sxs-lookup"><span data-stu-id="ce8e5-133">**Master DNS name**: hello prefix used toocreate a unique fully qualified domain name (FQDN) for hello master.</span></span> <span data-ttu-id="ce8e5-134">Hello wzorca nazwy FQDN ma formę hello *prefiks*dotyczących zarządzania*lokalizacji*. cloudapp.azure.com.</span><span class="sxs-lookup"><span data-stu-id="ce8e5-134">hello master FQDN is of hello form *prefix*mgmt.*location*.cloudapp.azure.com.</span></span>
    * <span data-ttu-id="ce8e5-135">**Nazwa użytkownika**: hello nazwę użytkownika dla konta na poszczególnych maszyn wirtualnych systemu Linux hello hello klastra.</span><span class="sxs-lookup"><span data-stu-id="ce8e5-135">**User name**: hello user name for an account on each of hello Linux virtual machines in hello cluster.</span></span>
    * <span data-ttu-id="ce8e5-136">**Klucz publiczny SSH RSA**: Dodaj hello publicznego toobe klucza używany do uwierzytelniania względem maszyn wirtualnych systemu Linux hello.</span><span class="sxs-lookup"><span data-stu-id="ce8e5-136">**SSH RSA public key**: Add hello public key toobe used for authentication against hello Linux virtual machines.</span></span> <span data-ttu-id="ce8e5-137">Ważne jest, aby klucz ten nie zawierał podziałów wierszy i zawiera hello `ssh-rsa` prefiks.</span><span class="sxs-lookup"><span data-stu-id="ce8e5-137">It is important that this key contains no line breaks, and it includes hello `ssh-rsa` prefix.</span></span> <span data-ttu-id="ce8e5-138">Witaj `username@domain` przyrostek jest opcjonalna.</span><span class="sxs-lookup"><span data-stu-id="ce8e5-138">hello `username@domain` postfix is optional.</span></span> <span data-ttu-id="ce8e5-139">Witaj klucz powinien wyglądać jak poniżej hello: **AAAAB3Nz ssh-rsa... <>...... UcyupgH azureuser@linuxvm** .</span><span class="sxs-lookup"><span data-stu-id="ce8e5-139">hello key should look something like hello following: **ssh-rsa AAAAB3Nz...<...>...UcyupgH azureuser@linuxvm**.</span></span> 
    * <span data-ttu-id="ce8e5-140">**Nazwy głównej usługi**: w przypadku wybrania hello Kubernetes orchestrator Azure Active Directory wprowadź **usługi identyfikator podmiotu zabezpieczeń klienta** (nazywanych również hello appId) i **klucz tajny klienta główna usługi** (hasło).</span><span class="sxs-lookup"><span data-stu-id="ce8e5-140">**Service principal**: If you selected hello Kubernetes orchestrator, enter an Azure Active Directory **Service principal client ID** (also called hello appId) and **Service principal client secret** (password).</span></span> <span data-ttu-id="ce8e5-141">Aby uzyskać więcej informacji, zobacz [o hello nazwy głównej usługi dla klastra Kubernetes](../kubernetes/container-service-kubernetes-service-principal.md).</span><span class="sxs-lookup"><span data-stu-id="ce8e5-141">For more information, see [About hello service principal for a Kubernetes cluster](../kubernetes/container-service-kubernetes-service-principal.md).</span></span>
    * <span data-ttu-id="ce8e5-142">**Liczba wzorca**: hello liczba wzorców w klastrze hello.</span><span class="sxs-lookup"><span data-stu-id="ce8e5-142">**Master count**: hello number of masters in hello cluster.</span></span>
    * <span data-ttu-id="ce8e5-143">**Diagnostyki maszyny Wirtualnej**: w przypadku niektórych orchestrators można włączyć diagnostyki maszyny Wirtualnej na powitania wzorców.</span><span class="sxs-lookup"><span data-stu-id="ce8e5-143">**VM diagnostics**: For some orchestrators, you can enable VM diagnostics on hello masters.</span></span>

    ![Konfiguracja serwera głównego](./media/container-service-deployment/acs-portal4.png)  <br />

    <span data-ttu-id="ce8e5-145">Kliknij przycisk **OK** gdy wszystko będzie gotowe tooproceed.</span><span class="sxs-lookup"><span data-stu-id="ce8e5-145">Click **OK** when you're ready tooproceed.</span></span>

5. <span data-ttu-id="ce8e5-146">Na powitania **konfiguracji agenta** bloku, wprowadź hello następujących informacji:</span><span class="sxs-lookup"><span data-stu-id="ce8e5-146">On hello **Agent configuration** blade, enter hello following information:</span></span>

    * <span data-ttu-id="ce8e5-147">**Liczba agentów**: Docker Swarm i Kubernetes, ta wartość jest początkowa liczba agentów w zestawie skali agenta hello hello.</span><span class="sxs-lookup"><span data-stu-id="ce8e5-147">**Agent count**: For Docker Swarm and Kubernetes, this value is hello initial number of agents in hello agent scale set.</span></span> <span data-ttu-id="ce8e5-148">DC/OS jest hello początkowa liczba agentów w prywatnym zestawie skali.</span><span class="sxs-lookup"><span data-stu-id="ce8e5-148">For DC/OS, it is hello initial number of agents in a private scale set.</span></span> <span data-ttu-id="ce8e5-149">Ponadto w przypadku koordynatora DC/OS jest tworzony publiczny zestaw skalowania zawierający wstępnie określoną liczbę agentów.</span><span class="sxs-lookup"><span data-stu-id="ce8e5-149">Additionally, a public scale set is created for DC/OS, which contains a predetermined number of agents.</span></span> <span data-ttu-id="ce8e5-150">Witaj agentów w tym publicznym zestawie jest określana na podstawie hello liczba wzorców w klastrze hello: jeden agent publiczny dla jeden z nich i dwóch agentów publicznych dla trzech lub 5 serwerów głównych.</span><span class="sxs-lookup"><span data-stu-id="ce8e5-150">hello number of agents in this public scale set is determined by hello number of masters in hello cluster: one public agent for one master, and two public agents for three or five masters.</span></span>
    * <span data-ttu-id="ce8e5-151">**Rozmiar maszyny wirtualnej agenta**: hello rozmiar maszyn wirtualnych hello agenta.</span><span class="sxs-lookup"><span data-stu-id="ce8e5-151">**Agent virtual machine size**: hello size of hello agent virtual machines.</span></span>
    * <span data-ttu-id="ce8e5-152">**System operacyjny**: to ustawienie jest dostępne tylko wtedy, gdy wybrano hello Kubernetes orchestrator.</span><span class="sxs-lookup"><span data-stu-id="ce8e5-152">**Operating system**: This setting is currently available only if you selected hello Kubernetes orchestrator.</span></span> <span data-ttu-id="ce8e5-153">Wybierz opcję dystrybucji systemu Linux lub toorun systemu operacyjnego Windows Server, na powitania agentów.</span><span class="sxs-lookup"><span data-stu-id="ce8e5-153">Choose either a Linux distribution or a Windows Server operating system toorun on hello agents.</span></span> <span data-ttu-id="ce8e5-154">To ustawienie określa, czy w klastrze można uruchamiać aplikacje kontenera systemu Linux czy Windows.</span><span class="sxs-lookup"><span data-stu-id="ce8e5-154">This setting determines whether your cluster can run Linux or Windows container apps.</span></span> 

        > [!NOTE]
        > <span data-ttu-id="ce8e5-155">Obsługa kontenerów systemu Windows dla klastrów Kubernetes jest dostępna w wersji zapoznawczej.</span><span class="sxs-lookup"><span data-stu-id="ce8e5-155">Windows container support is in preview for Kubernetes clusters.</span></span> <span data-ttu-id="ce8e5-156">W przypadku klastrów DC/OS i Swarm tylko agenci systemu Linux są obecnie obsługiwani przez usługę Azure Container Service.</span><span class="sxs-lookup"><span data-stu-id="ce8e5-156">On DC/OS and Swarm clusters, only Linux agents are currently supported in Azure Container Service.</span></span>

    * <span data-ttu-id="ce8e5-157">**Poświadczenia agenta**: w przypadku wybrania systemu operacyjnego Windows hello, wprowadź administrator **nazwy użytkownika** i **hasło** dla agenta hello maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="ce8e5-157">**Agent credentials**: If you selected hello Windows operating system, enter an administrator **User name** and **Password** for hello agent VMs.</span></span> 

    ![Konfiguracja agenta](./media/container-service-deployment/acs-portal5.png)  <br />

    <span data-ttu-id="ce8e5-159">Kliknij przycisk **OK** gdy wszystko będzie gotowe tooproceed.</span><span class="sxs-lookup"><span data-stu-id="ce8e5-159">Click **OK** when you're ready tooproceed.</span></span>

6. <span data-ttu-id="ce8e5-160">Po zakończeniu weryfikacji usługi kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="ce8e5-160">After service validation finishes, click **OK**.</span></span>

    ![Walidacja](./media/container-service-deployment/acs-portal6.png)  <br />

7. <span data-ttu-id="ce8e5-162">Przejrzyj postanowienia hello.</span><span class="sxs-lookup"><span data-stu-id="ce8e5-162">Review hello terms.</span></span> <span data-ttu-id="ce8e5-163">proces wdrażania hello toostart, kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="ce8e5-163">toostart hello deployment process, click **Create**.</span></span>

    <span data-ttu-id="ce8e5-164">Został wybrany toopin hello wdrożenia toohello portalu Azure, można wyświetlić stan wdrożenia hello.</span><span class="sxs-lookup"><span data-stu-id="ce8e5-164">If you've elected toopin hello deployment toohello Azure portal, you can see hello deployment status.</span></span>

    ![Stan wdrożenia](./media/container-service-deployment/acs-portal8.png)  <br />

<span data-ttu-id="ce8e5-166">wdrożenie Hello zajmuje kilka minut toocomplete.</span><span class="sxs-lookup"><span data-stu-id="ce8e5-166">hello deployment takes several minutes toocomplete.</span></span> <span data-ttu-id="ce8e5-167">Następnie hello klastra usługi kontenera platformy Azure jest gotowy do użycia.</span><span class="sxs-lookup"><span data-stu-id="ce8e5-167">Then, hello Azure Container Service cluster is ready for use.</span></span>


## <a name="create-a-cluster-by-using-a-quickstart-template"></a><span data-ttu-id="ce8e5-168">Tworzenie klastra przy użyciu szablonu szybkiego startu</span><span class="sxs-lookup"><span data-stu-id="ce8e5-168">Create a cluster by using a quickstart template</span></span>
<span data-ttu-id="ce8e5-169">Szablony szybkiego startu usługi Azure są dostępne toodeploy klastra usługi kontenera platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="ce8e5-169">Azure quickstart templates are available toodeploy a cluster in Azure Container Service.</span></span> <span data-ttu-id="ce8e5-170">Witaj pod warunkiem, że szablony szybkiego startu może być zmodyfikowany tooinclude dodatkowe lub zaawansowanych konfiguracji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="ce8e5-170">hello provided quickstart templates can be modified tooinclude additional or advanced Azure configuration.</span></span> <span data-ttu-id="ce8e5-171">toocreate klastra usługi kontenera platformy Azure przy użyciu szablonu Azure szybkiego startu, potrzebujesz subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="ce8e5-171">toocreate an Azure Container Service cluster by using an Azure quickstart template, you need an Azure subscription.</span></span> <span data-ttu-id="ce8e5-172">Jeśli jej nie masz, utwórz konto [bezpłatnej wersji próbnej](http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=AA4C1C935).</span><span class="sxs-lookup"><span data-stu-id="ce8e5-172">If you don't have one, then sign up for a [free trial](http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=AA4C1C935).</span></span> 

<span data-ttu-id="ce8e5-173">Wykonaj te kroki toodeploy klastra przy użyciu szablonu i hello Azure CLI 2.0 (zobacz [instrukcje instalacji i](/cli/azure/install-az-cli2)).</span><span class="sxs-lookup"><span data-stu-id="ce8e5-173">Follow these steps toodeploy a cluster using a template and hello Azure CLI 2.0 (see [installation and setup instructions](/cli/azure/install-az-cli2)).</span></span>

> [!NOTE] 
> <span data-ttu-id="ce8e5-174">Jeśli w systemie Windows za pomocą podobne kroki toodeploy szablonu przy użyciu programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ce8e5-174">If you're on a Windows system, you can use similar steps toodeploy a template using Azure PowerShell.</span></span> <span data-ttu-id="ce8e5-175">Zobacz kroki w dalszej części tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="ce8e5-175">See steps later in this section.</span></span> <span data-ttu-id="ce8e5-176">Można także wdrożyć szablon przy użyciu hello [portal](../../azure-resource-manager/resource-group-template-deploy-portal.md) lub innych metod.</span><span class="sxs-lookup"><span data-stu-id="ce8e5-176">You can also deploy a template through hello [portal](../../azure-resource-manager/resource-group-template-deploy-portal.md) or other methods.</span></span>

1. <span data-ttu-id="ce8e5-177">toodeploy klastra DC/OS, Kubernetes lub Docker Swarm, wybierz jeden z szablonów Szybki Start dostępny hello z usługi GitHub.</span><span class="sxs-lookup"><span data-stu-id="ce8e5-177">toodeploy a DC/OS, Docker Swarm, or Kubernetes cluster, select one of hello available quickstart templates from GitHub.</span></span> <span data-ttu-id="ce8e5-178">Częściowa lista została przedstawiona poniżej.</span><span class="sxs-lookup"><span data-stu-id="ce8e5-178">A partial list follows.</span></span> <span data-ttu-id="ce8e5-179">są takie same, z wyjątkiem hello domyślnie wybraną aranżacją hello Hello DC/OS i Swarm szablonów.</span><span class="sxs-lookup"><span data-stu-id="ce8e5-179">hello DC/OS and Swarm templates are hello same, except for hello default orchestrator selection.</span></span>

    * [<span data-ttu-id="ce8e5-180">Szablon DC/OS</span><span class="sxs-lookup"><span data-stu-id="ce8e5-180">DC/OS template</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-dcos)
    * [<span data-ttu-id="ce8e5-181">Szablon Swarm</span><span class="sxs-lookup"><span data-stu-id="ce8e5-181">Swarm template</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-swarm)
    * [<span data-ttu-id="ce8e5-182">Szablon Kubernetes</span><span class="sxs-lookup"><span data-stu-id="ce8e5-182">Kubernetes template</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-kubernetes)

2. <span data-ttu-id="ce8e5-183">Zaloguj się za tooyour konto platformy Azure (`az login`) i upewnij się, że hello Azure CLI jest połączonych tooyour subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="ce8e5-183">Log in tooyour Azure account (`az login`), and make sure that hello Azure CLI is connected tooyour Azure subscription.</span></span> <span data-ttu-id="ce8e5-184">Hello domyślne subskrypcji można wyświetlić za pomocą następującego polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="ce8e5-184">You can see hello default subscription by using hello following command:</span></span>

    ```azurecli
    az account show
    ```
    
    <span data-ttu-id="ce8e5-185">Jeśli masz więcej niż jeden tooset subskrypcji i potrzeb subskrypcji różne domyślne uruchomić `az account set --subscription` i określić nazwę lub identyfikator subskrypcji hello.</span><span class="sxs-lookup"><span data-stu-id="ce8e5-185">If you have more than one subscription and need tooset a different default subscription, run `az account set --subscription` and specify hello subscription ID or name.</span></span>

3. <span data-ttu-id="ce8e5-186">Najlepszym rozwiązaniem Użyj nowej grupy zasobów hello wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="ce8e5-186">As a best practice, use a new resource group for hello deployment.</span></span> <span data-ttu-id="ce8e5-187">toocreate grupę zasobów, użyj hello `az group create` polecenia Podaj nazwę grupy zasobów i lokalizacji:</span><span class="sxs-lookup"><span data-stu-id="ce8e5-187">toocreate a resource group, use hello `az group create` command specify a resource group name and location:</span></span> 

    ```azurecli
    az group create --name "RESOURCE_GROUP" --location "LOCATION"
    ```

4. <span data-ttu-id="ce8e5-188">Utwórz szablonu JSON w pliku zawierającego hello wymagane parametry.</span><span class="sxs-lookup"><span data-stu-id="ce8e5-188">Create a JSON file containing hello required template parameters.</span></span> <span data-ttu-id="ce8e5-189">Plik parametrów hello pobierania o nazwie `azuredeploy.parameters.json` dołączony szablon usługi kontenera platformy Azure hello `azuredeploy.json` w witrynie GitHub.</span><span class="sxs-lookup"><span data-stu-id="ce8e5-189">Download hello parameters file named `azuredeploy.parameters.json` that accompanies hello Azure Container Service template `azuredeploy.json` in GitHub.</span></span> <span data-ttu-id="ce8e5-190">Wprowadź wymagane wartości parametrów dla klastra.</span><span class="sxs-lookup"><span data-stu-id="ce8e5-190">Enter required parameter values for your cluster.</span></span> 

    <span data-ttu-id="ce8e5-191">Na przykład toouse hello [szablon DC/OS](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-dcos), podaj wartości parametrów dla `dnsNamePrefix` i `sshRSAPublicKey`.</span><span class="sxs-lookup"><span data-stu-id="ce8e5-191">For example, toouse hello [DC/OS template](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-dcos), supply parameter values for `dnsNamePrefix` and `sshRSAPublicKey`.</span></span> <span data-ttu-id="ce8e5-192">Zobacz opis hello w `azuredeploy.json` i opcje dla innych parametrów.</span><span class="sxs-lookup"><span data-stu-id="ce8e5-192">See hello descriptions in `azuredeploy.json` and options for other parameters.</span></span>  
 

5. <span data-ttu-id="ce8e5-193">Tworzenie klastra usługi kontenera przez przekazanie pliku parametrów wdrożenia hello z hello następujące polecenie, gdzie:</span><span class="sxs-lookup"><span data-stu-id="ce8e5-193">Create a Container Service cluster by passing hello deployment parameters file with hello following command, where:</span></span>

    * <span data-ttu-id="ce8e5-194">**RESOURCE_GROUP** to nazwa grupy zasobów hello utworzony w poprzednim kroku hello hello.</span><span class="sxs-lookup"><span data-stu-id="ce8e5-194">**RESOURCE_GROUP** is hello name of hello resource group that you created in hello previous step.</span></span>
    * <span data-ttu-id="ce8e5-195">**DEPLOYMENT_NAME** (opcjonalnie) jest nazwą zapewniają toohello wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="ce8e5-195">**DEPLOYMENT_NAME** (optional) is a name you give toohello deployment.</span></span>
    * <span data-ttu-id="ce8e5-196">**TEMPLATE_URI** hello lokalizacja pliku wdrożenia hello `azuredeploy.json`.</span><span class="sxs-lookup"><span data-stu-id="ce8e5-196">**TEMPLATE_URI** is hello location of hello deployment file `azuredeploy.json`.</span></span> <span data-ttu-id="ce8e5-197">Ten identyfikator URI musi być hello plik Raw, nie toohello wskaźnika interfejsu użytkownika serwisu GitHub.</span><span class="sxs-lookup"><span data-stu-id="ce8e5-197">This URI must be hello Raw file, not a pointer toohello GitHub UI.</span></span> <span data-ttu-id="ce8e5-198">toofind tego identyfikatora URI, wybierz hello `azuredeploy.json` pliku w usłudze GitHub, a następnie kliknij przycisk hello **Raw** przycisku.</span><span class="sxs-lookup"><span data-stu-id="ce8e5-198">toofind this URI, select hello `azuredeploy.json` file in GitHub, and click hello **Raw** button.</span></span>  

    ```azurecli
    az group deployment create -g RESOURCE_GROUP -n DEPLOYMENT_NAME --template-uri TEMPLATE_URI --parameters @azuredeploy.parameters.json
    ```

    <span data-ttu-id="ce8e5-199">Można też podać parametry jako ciąg w formacie JSON hello w wierszu polecenia.</span><span class="sxs-lookup"><span data-stu-id="ce8e5-199">You can also provide parameters as a JSON-formatted string on hello command line.</span></span> <span data-ttu-id="ce8e5-200">Użyj polecenia podobne toohello następującego:</span><span class="sxs-lookup"><span data-stu-id="ce8e5-200">Use a command similar toohello following:</span></span>

    ```azurecli
    az group deployment create -g RESOURCE_GROUP -n DEPLOYMENT_NAME --template-uri TEMPLATE_URI --parameters "{ \"param1\": {\"value1\"} … }"
    ```

    > [!NOTE]
    > <span data-ttu-id="ce8e5-201">wdrożenie Hello zajmuje kilka minut toocomplete.</span><span class="sxs-lookup"><span data-stu-id="ce8e5-201">hello deployment takes several minutes toocomplete.</span></span>
    > 

### <a name="equivalent-powershell-commands"></a><span data-ttu-id="ce8e5-202">Równoważne polecenia programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="ce8e5-202">Equivalent PowerShell commands</span></span>
<span data-ttu-id="ce8e5-203">Szablon klastra usługi Azure Container Service można również wdrożyć przy użyciu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ce8e5-203">You can also deploy an Azure Container Service cluster template with PowerShell.</span></span> <span data-ttu-id="ce8e5-204">Ten dokument jest oparty na powitania w wersji 1.0 [modułu Azure PowerShell](https://azure.microsoft.com/blog/azps-1-0/).</span><span class="sxs-lookup"><span data-stu-id="ce8e5-204">This document is based on hello version 1.0 [Azure PowerShell module](https://azure.microsoft.com/blog/azps-1-0/).</span></span>

1. <span data-ttu-id="ce8e5-205">toodeploy klastra DC/OS, Kubernetes lub Docker Swarm, wybierz jeden z szablonów Szybki Start dostępny hello z usługi GitHub.</span><span class="sxs-lookup"><span data-stu-id="ce8e5-205">toodeploy a DC/OS, Docker Swarm, or Kubernetes cluster, select one of hello available quickstart templates from GitHub.</span></span> <span data-ttu-id="ce8e5-206">Częściowa lista została przedstawiona poniżej.</span><span class="sxs-lookup"><span data-stu-id="ce8e5-206">A partial list follows.</span></span> <span data-ttu-id="ce8e5-207">Należy pamiętać, że hello DC/OS i Swarm szablony są hello takie same, z wyjątkiem hello hello domyślnie wybraną aranżacją.</span><span class="sxs-lookup"><span data-stu-id="ce8e5-207">Note that hello DC/OS and Swarm templates are hello same, with hello exception of hello default orchestrator selection.</span></span>

    * [<span data-ttu-id="ce8e5-208">Szablon DC/OS</span><span class="sxs-lookup"><span data-stu-id="ce8e5-208">DC/OS template</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-dcos)
    * [<span data-ttu-id="ce8e5-209">Szablon Swarm</span><span class="sxs-lookup"><span data-stu-id="ce8e5-209">Swarm template</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-swarm)
    * [<span data-ttu-id="ce8e5-210">Szablon Kubernetes</span><span class="sxs-lookup"><span data-stu-id="ce8e5-210">Kubernetes template</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-kubernetes)

2. <span data-ttu-id="ce8e5-211">Przed utworzeniem klastra w ramach subskrypcji platformy Azure, sprawdź, czy w tooAzure została podpisana sesji programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ce8e5-211">Before creating a cluster in your Azure subscription, verify that your PowerShell session has been signed in tooAzure.</span></span> <span data-ttu-id="ce8e5-212">Można to zrobić z hello `Get-AzureRMSubscription` polecenia:</span><span class="sxs-lookup"><span data-stu-id="ce8e5-212">You can do this with hello `Get-AzureRMSubscription` command:</span></span>

    ```powershell
    Get-AzureRmSubscription
    ```

3. <span data-ttu-id="ce8e5-213">Jeśli potrzebujesz toosign w tooAzure, użyj hello `Login-AzureRMAccount` polecenia:</span><span class="sxs-lookup"><span data-stu-id="ce8e5-213">If you need toosign in tooAzure, use hello `Login-AzureRMAccount` command:</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

4. <span data-ttu-id="ce8e5-214">Najlepszym rozwiązaniem Użyj nowej grupy zasobów hello wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="ce8e5-214">As a best practice, use a new resource group for hello deployment.</span></span> <span data-ttu-id="ce8e5-215">toocreate grupę zasobów, użyj hello `New-AzureRmResourceGroup` polecenia, a następnie określ region nazwę i miejsce docelowe grupy zasobów:</span><span class="sxs-lookup"><span data-stu-id="ce8e5-215">toocreate a resource group, use hello `New-AzureRmResourceGroup` command, and specify a resource group name and destination region:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name GROUP_NAME -Location REGION
    ```

5. <span data-ttu-id="ce8e5-216">Po utworzeniu grupy zasobów, można utworzyć klaster z hello następujące polecenia.</span><span class="sxs-lookup"><span data-stu-id="ce8e5-216">After you create a resource group, you can create your cluster with hello following command.</span></span> <span data-ttu-id="ce8e5-217">Identyfikator URI hello Hello żądanego szablonu zostanie określony z hello `-TemplateUri` parametru.</span><span class="sxs-lookup"><span data-stu-id="ce8e5-217">hello URI of hello desired template is specified with hello `-TemplateUri` parameter.</span></span> <span data-ttu-id="ce8e5-218">Po uruchomieniu tego polecenia program PowerShell wyświetli monit o wprowadzenie wartości parametrów wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="ce8e5-218">When you run this command, PowerShell prompts you for deployment parameter values.</span></span>

    ```powershell
    New-AzureRmResourceGroupDeployment -Name DEPLOYMENT_NAME -ResourceGroupName RESOURCE_GROUP_NAME -TemplateUri TEMPLATE_URI
    ```

#### <a name="provide-template-parameters"></a><span data-ttu-id="ce8e5-219">Wprowadzanie parametrów szablonu</span><span class="sxs-lookup"><span data-stu-id="ce8e5-219">Provide template parameters</span></span>
<span data-ttu-id="ce8e5-220">Jeśli znasz programu PowerShell, wiesz, że do przechodzenia między hello dostępne parametry polecenia cmdlet, wpisując znak minus (-), a następnie naciskając klawisz TAB hello.</span><span class="sxs-lookup"><span data-stu-id="ce8e5-220">If you're familiar with PowerShell, you know that you can cycle through hello available parameters for a cmdlet by typing a minus sign (-) and then pressing hello TAB key.</span></span> <span data-ttu-id="ce8e5-221">Ta funkcja działa również w przypadku parametrów zdefiniowanych w szablonie.</span><span class="sxs-lookup"><span data-stu-id="ce8e5-221">This same functionality also works with parameters that you define in your template.</span></span> <span data-ttu-id="ce8e5-222">Jak wpisywania nazwy szablonu hello hello polecenia cmdlet pobiera szablon hello, analizuje parametry hello i dynamicznie dodaje hello szablonu parametrów toohello polecenia.</span><span class="sxs-lookup"><span data-stu-id="ce8e5-222">As soon as you type hello template name, hello cmdlet fetches hello template, parses hello parameters, and adds hello template parameters toohello command dynamically.</span></span> <span data-ttu-id="ce8e5-223">Dzięki temu wartości parametrów szablonu hello toospecify łatwe.</span><span class="sxs-lookup"><span data-stu-id="ce8e5-223">This makes it easy toospecify hello template parameter values.</span></span> <span data-ttu-id="ce8e5-224">A Jeśli zapomnisz wartości wymaganego parametru programu PowerShell wyświetla monit o podanie wartości hello.</span><span class="sxs-lookup"><span data-stu-id="ce8e5-224">And, if you forget a required parameter value, PowerShell prompts you for hello value.</span></span>

<span data-ttu-id="ce8e5-225">Oto pełne polecenie Witaj z uwzględnionymi parametrami.</span><span class="sxs-lookup"><span data-stu-id="ce8e5-225">Here is hello full command, with parameters included.</span></span> <span data-ttu-id="ce8e5-226">Należy podać własne wartości nazw hello hello zasobów.</span><span class="sxs-lookup"><span data-stu-id="ce8e5-226">Provide your own values for hello names of hello resources.</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName RESOURCE_GROUP_NAME-TemplateURI TEMPLATE_URI -adminuser value1 -adminpassword value2 ....
```

## <a name="next-steps"></a><span data-ttu-id="ce8e5-227">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="ce8e5-227">Next steps</span></span>
<span data-ttu-id="ce8e5-228">Teraz, gdy masz działający klaster, możesz zapoznać się z tymi dokumentami, aby uzyskać szczegółowe informacje na temat połączeń i zarządzania:</span><span class="sxs-lookup"><span data-stu-id="ce8e5-228">Now that you have a functioning cluster, see these documents for connection and management details:</span></span>

* [<span data-ttu-id="ce8e5-229">Połącz tooan klastra usługi kontenera platformy Azure</span><span class="sxs-lookup"><span data-stu-id="ce8e5-229">Connect tooan Azure Container Service cluster</span></span>](../container-service-connect.md)
* [<span data-ttu-id="ce8e5-230">Współpraca z usługą Azure Container Service i rozwiązaniem DC/OS</span><span class="sxs-lookup"><span data-stu-id="ce8e5-230">Work with Azure Container Service and DC/OS</span></span>](container-service-mesos-marathon-rest.md)
* [<span data-ttu-id="ce8e5-231">Współpraca z usługą Azure Container Service i rozwiązaniem Docker Swarm</span><span class="sxs-lookup"><span data-stu-id="ce8e5-231">Work with Azure Container Service and Docker Swarm</span></span>](container-service-docker-swarm.md)
* [<span data-ttu-id="ce8e5-232">Współpraca z usługą Azure Container Service i rozwiązaniem Kubernetes</span><span class="sxs-lookup"><span data-stu-id="ce8e5-232">Work with Azure Container Service and Kubernetes</span></span>](../kubernetes/container-service-kubernetes-walkthrough.md)
