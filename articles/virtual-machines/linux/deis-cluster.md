---
title: "aaaDeploy Deis 3 węzłami klastra | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano sposób toocreate węzłem 3 Deis klastra na platformie Azure przy użyciu szablonu usługi Azure Resource Manager"
services: virtual-machines-linux
documentationcenter: 
author: HaishiBai
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 5eb67eb7-95d4-461d-8eac-44925224ba5f
ms.service: virtual-machines-linux
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 06/24/2015
ms.author: hbai
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a4c0fb8cbb849264e64b433540157c9afecd184e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-configure-a-3-node-deis-cluster-in-azure"></a><span data-ttu-id="02a42-103">Wdrażanie i konfigurowanie węzłem 3 Deis klastra w systemie Azure</span><span class="sxs-lookup"><span data-stu-id="02a42-103">Deploy and configure a 3-node Deis cluster in Azure</span></span>
<span data-ttu-id="02a42-104">W tym artykule przedstawiono inicjowania obsługi administracyjnej [Deis](http://deis.io/) klastra na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="02a42-104">This article walks you through provisioning a [Deis](http://deis.io/) cluster on Azure.</span></span> <span data-ttu-id="02a42-105">Obejmuje wszystkie kroki hello tworzenie hello toodeploying wymagane certyfikaty i skalowanie próbkę **Przejdź** aplikacji w klastrze nowo aprowizowanej hello.</span><span class="sxs-lookup"><span data-stu-id="02a42-105">It covers all hello steps from creating hello necessary certificates toodeploying and scaling a sample **Go** application on hello newly provisioned cluster.</span></span>

<span data-ttu-id="02a42-106">Witaj Poniższy diagram przedstawia hello architektury systemu hello wdrożone.</span><span class="sxs-lookup"><span data-stu-id="02a42-106">hello following diagram shows hello architecture of hello deployed system.</span></span> <span data-ttu-id="02a42-107">Zarządza administrator systemu przy użyciu klastra hello Deis narzędzi, takich jak **deis** i **deisctl**.</span><span class="sxs-lookup"><span data-stu-id="02a42-107">A system administrator manages hello cluster using Deis tools such as **deis** and **deisctl**.</span></span> <span data-ttu-id="02a42-108">Nawiązywane są połączenia za pośrednictwem usługi równoważenia obciążenia Azure, który przesyła dalej węzłów w klastrze hello tooone połączeń hello hello elementu członkowskiego.</span><span class="sxs-lookup"><span data-stu-id="02a42-108">Connections are established through an Azure load balancer, which forwards hello connections tooone of hello member nodes on hello cluster.</span></span> <span data-ttu-id="02a42-109">dostęp klientom Witaj wdrożone aplikacje za pomocą hello również równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="02a42-109">hello clients access deployed applications through hello load balancer as well.</span></span> <span data-ttu-id="02a42-110">W takim przypadku Usługa równoważenia obciążenia hello przekazuje tooa ruchu hello Deis routera sieci, które dodatkowo routs kontenery Docker toocorresponding ruchu hostowanych w klastrze hello.</span><span class="sxs-lookup"><span data-stu-id="02a42-110">In this case, hello load balancer forwards hello traffic tooa Deis router mesh, which further routs traffic toocorresponding Docker containers hosted on hello cluster.</span></span>

  ![Diagram architektury wdrożonej Desis klastra](./media/deis-cluster/architecture-overview.png)

<span data-ttu-id="02a42-112">W kolejności toorun za pośrednictwem hello następujące kroki potrzebne są:</span><span class="sxs-lookup"><span data-stu-id="02a42-112">In order toorun through hello following steps, you'll need:</span></span>

* <span data-ttu-id="02a42-113">Aktywna subskrypcja platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="02a42-113">An active Azure subscription.</span></span> <span data-ttu-id="02a42-114">Jeśli nie masz, możesz pobrać wolnego ślad [witryny azure.com](https://azure.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="02a42-114">If you don't have one, you can get a free trail on [azure.com](https://azure.microsoft.com/).</span></span>
* <span data-ttu-id="02a42-115">Służbowy lub grup zasobów platformy Azure toouse identyfikator służbowe.</span><span class="sxs-lookup"><span data-stu-id="02a42-115">A work or school id toouse Azure resource groups.</span></span> <span data-ttu-id="02a42-116">Jeśli masz konto osobiste i zaloguj się za pomocą identyfikatora Microsoft, należy za[utworzyć identyfikator pracy niż osobiste](../windows/create-aad-work-id.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="02a42-116">If you have a personal account and log in with a Microsoft id, you need too[create a work id from your personal one](../windows/create-aad-work-id.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="02a42-117">Albo — w zależności od systemu operacyjnego klienta — Witaj [programu Azure PowerShell](/powershell/azureps-cmdlets-docs) lub hello [Azure CLI for Mac, Linux i Windows](../../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="02a42-117">Either -- depending on your client operating system -- hello [Azure PowerShell](/powershell/azureps-cmdlets-docs) or hello [Azure CLI for Mac, Linux, and Windows](../../cli-install-nodejs.md).</span></span>
* <span data-ttu-id="02a42-118">[Biblioteki OpenSSL](https://www.openssl.org/).</span><span class="sxs-lookup"><span data-stu-id="02a42-118">[OpenSSL](https://www.openssl.org/).</span></span> <span data-ttu-id="02a42-119">Biblioteki OpenSSL jest używane toogenerate hello wymagane certyfikaty.</span><span class="sxs-lookup"><span data-stu-id="02a42-119">OpenSSL is used toogenerate hello necessary certificates.</span></span>
* <span data-ttu-id="02a42-120">Klient Git, takich jak [Git Bash](https://git-scm.com/).</span><span class="sxs-lookup"><span data-stu-id="02a42-120">A Git client such as [Git Bash](https://git-scm.com/).</span></span>
* <span data-ttu-id="02a42-121">tootest hello przykładowej aplikacji, należy również serwer DNS.</span><span class="sxs-lookup"><span data-stu-id="02a42-121">tootest hello sample application, you'll also need a DNS server.</span></span> <span data-ttu-id="02a42-122">Można użyć dowolnego serwerów DNS lub usługi, które obsługują rekordy A symboli wieloznacznych.</span><span class="sxs-lookup"><span data-stu-id="02a42-122">You can use any DNS servers or services that support wildcard A records.</span></span>
* <span data-ttu-id="02a42-123">Toorun komputera Deis narzędziami klienckimi.</span><span class="sxs-lookup"><span data-stu-id="02a42-123">A computer toorun Deis client tools.</span></span> <span data-ttu-id="02a42-124">Można użyć komputera lokalnego lub maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="02a42-124">You can use either a local machine or a virtual machine.</span></span> <span data-ttu-id="02a42-125">Te narzędzia można uruchomić na dowolnym dystrybucji systemu Linux, ale hello poniższe instrukcje korzystają z systemu Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="02a42-125">You can run these tools on almost any Linux distribution, but hello following instructions use Ubuntu.</span></span>

## <a name="provision-hello-cluster"></a><span data-ttu-id="02a42-126">Zainicjuj obsługę hello klastra</span><span class="sxs-lookup"><span data-stu-id="02a42-126">Provision hello cluster</span></span>
<span data-ttu-id="02a42-127">W tej sekcji użyjesz [usługi Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md) szablonu z repozytorium typu open source hello [azure — Szybki Start — szablony](https://github.com/Azure/azure-quickstart-templates).</span><span class="sxs-lookup"><span data-stu-id="02a42-127">In this section, you'll use an [Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md) template from hello open source repository [azure-quickstart-templates](https://github.com/Azure/azure-quickstart-templates).</span></span> <span data-ttu-id="02a42-128">Po pierwsze będą kopiowane dół hello szablonu.</span><span class="sxs-lookup"><span data-stu-id="02a42-128">First, you'll copy down hello template.</span></span> <span data-ttu-id="02a42-129">Następnie utworzysz nową parę kluczy SSH do uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="02a42-129">Then, you'll create a new SSH key pair for authentication.</span></span> <span data-ttu-id="02a42-130">A następnie należy skonfigurować nowy identyfikator dla klastra należy.</span><span class="sxs-lookup"><span data-stu-id="02a42-130">And then, you'll configure a new identifier for you cluster.</span></span> <span data-ttu-id="02a42-131">A na koniec użyjesz skrypt powłoki hello lub hello PowerShell skryptu tooprovision hello klastra.</span><span class="sxs-lookup"><span data-stu-id="02a42-131">And finally, you'll use either hello Shell script or hello PowerShell script tooprovision hello cluster.</span></span>

1. <span data-ttu-id="02a42-132">Klonowanie repozytorium hello: [https://github.com/Azure/azure-quickstart-templates](https://github.com/Azure/azure-quickstart-templates).</span><span class="sxs-lookup"><span data-stu-id="02a42-132">Clone hello repository: [https://github.com/Azure/azure-quickstart-templates](https://github.com/Azure/azure-quickstart-templates).</span></span>
   
        git clone https://github.com/Azure/azure-quickstart-templates
2. <span data-ttu-id="02a42-133">Folder szablonu przejdź toohello:</span><span class="sxs-lookup"><span data-stu-id="02a42-133">Go toohello template folder:</span></span>
   
        cd azure-quickstart-templates\deis-cluster-coreos
3. <span data-ttu-id="02a42-134">Utwórz nową parę kluczy SSH za pomocą ssh-keygen:</span><span class="sxs-lookup"><span data-stu-id="02a42-134">Create a new SSH key pair using ssh-keygen:</span></span>
   
        ssh-keygen -t rsa -b 4096 -c "[your_email@domain.com]"
4. <span data-ttu-id="02a42-135">Generowanie za pomocą hello powyżej klucza prywatnego certyfikatu:</span><span class="sxs-lookup"><span data-stu-id="02a42-135">Generate a certificate using hello above private key:</span></span>
   
        openssl req -x509 -days 365 -new -key [your private key file] -out [cert file toobe generated]
5. <span data-ttu-id="02a42-136">Przejdź za[https://discovery.etcd.io/new](https://discovery.etcd.io/new) toogenerate nowy token klastra, który wygląda coś, takich jak:</span><span class="sxs-lookup"><span data-stu-id="02a42-136">Go too[https://discovery.etcd.io/new](https://discovery.etcd.io/new) toogenerate a new cluster token, which looks something like:</span></span>
   
        https://discovery.etcd.io/6a28e078895c5ec737174db2419bb2f3
   <br />
   <span data-ttu-id="02a42-137">Każdy klaster CoreOS musi toohave unikatowy tokenu z tej bezpłatnej usługi.</span><span class="sxs-lookup"><span data-stu-id="02a42-137">Each CoreOS cluster needs toohave a unique token from this free service.</span></span> <span data-ttu-id="02a42-138">Zobacz [CoreOS dokumentacji](https://coreos.com/docs/cluster-management/setup/cluster-discovery/) więcej szczegółów.</span><span class="sxs-lookup"><span data-stu-id="02a42-138">Please see [CoreOS documentation](https://coreos.com/docs/cluster-management/setup/cluster-discovery/) for more details.</span></span>
6. <span data-ttu-id="02a42-139">Modyfikowanie hello **config.yaml chmury** pliku istniejących hello tooreplace **odnajdywania** tokenu z hello nowy token:</span><span class="sxs-lookup"><span data-stu-id="02a42-139">Modify hello **cloud-config.yaml** file tooreplace hello existing  **discovery** token with hello new token:</span></span>
   
        #cloud-config
        ---
        coreos:
          etcd:
            # generate a new token for each unique cluster from https://discovery.etcd.io/new
            # uncomment hello following line and replace it with your discovery URL
            discovery: https://discovery.etcd.io/3973057f670770a7628f917d58c2208a
        ...
7. <span data-ttu-id="02a42-140">Modyfikowanie hello **parameters.JSON następującym kodem azuredeploy** plik: hello Otwórz certyfikat został utworzony w kroku 4 w edytorze tekstów.</span><span class="sxs-lookup"><span data-stu-id="02a42-140">Modify hello **azuredeploy-parameters.json** file: Open hello certificate you created in step 4 in a text editor.</span></span> <span data-ttu-id="02a42-141">Skopiuj cały tekst między `----BEGIN CERTIFICATE-----` i `-----END CERTIFICATE-----` do hello **sshKeyData** parametr (należy tooremove wszystkie znaki nowego wiersza).</span><span class="sxs-lookup"><span data-stu-id="02a42-141">Copy all text between `----BEGIN CERTIFICATE-----` and `-----END CERTIFICATE-----` into hello **sshKeyData** parameter (you'll need tooremove all newline characters).</span></span>
8. <span data-ttu-id="02a42-142">Modyfikowanie hello **newStorageAccountName** parametru.</span><span class="sxs-lookup"><span data-stu-id="02a42-142">Modify hello **newStorageAccountName** parameter.</span></span> <span data-ttu-id="02a42-143">To konto magazynu hello dysków systemu operacyjnego maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="02a42-143">This is hello storage account for VM OS disks.</span></span> <span data-ttu-id="02a42-144">Ta nazwa konta została toobe globalnie unikatowe.</span><span class="sxs-lookup"><span data-stu-id="02a42-144">This account name has toobe globally unique.</span></span>
9. <span data-ttu-id="02a42-145">Modyfikowanie hello **publicDomainName** parametru.</span><span class="sxs-lookup"><span data-stu-id="02a42-145">Modify hello **publicDomainName** parameter.</span></span> <span data-ttu-id="02a42-146">Będzie to część nazwy DNS hello skojarzone z adresem IP publiczny moduł równoważenia obciążenia hello.</span><span class="sxs-lookup"><span data-stu-id="02a42-146">This will become part of hello DNS name associated with hello load balancer public IP.</span></span> <span data-ttu-id="02a42-147">Witaj FQDN końcowego ma hello format *[wartość tego parametru]*. *kolumny [region]* . cloudapp.azure.com. Na przykład jeśli określono nazwę hello jako deishbai32 i hello grupa zasobów jest wdrożony toohello regionu zachodnie stany USA, a następnie hello końcowego FQDN tooyour będzie usługa równoważenia obciążenia deishbai32.westus.cloudapp.azure.com.</span><span class="sxs-lookup"><span data-stu-id="02a42-147">hello final FQDN will have hello format of *[value of this parameter]*.*[region]*.cloudapp.azure.com. For example, if you specify hello name as deishbai32, and hello resource group is deployed toohello West US region, then hello final FQDN tooyour load balancer will be deishbai32.westus.cloudapp.azure.com.</span></span>
10. <span data-ttu-id="02a42-148">Zapisz plik parametru hello.</span><span class="sxs-lookup"><span data-stu-id="02a42-148">Save hello parameter file.</span></span> <span data-ttu-id="02a42-149">A następnie można udostępnić hello klastra przy użyciu programu Azure PowerShell:</span><span class="sxs-lookup"><span data-stu-id="02a42-149">And then you can provision hello cluster using Azure PowerShell:</span></span>
    
        .\deploy-deis.ps1 -ResourceGroupName [resource group name] -ResourceGroupLocation "West US" -TemplateFile
        .\azuredeploy.json -ParametersFile .\azuredeploy-parameters.json -CloudInitFile .\cloud-config.yaml
    
    <span data-ttu-id="02a42-150">lub interfejsu wiersza polecenia platformy Azure:</span><span class="sxs-lookup"><span data-stu-id="02a42-150">or Azure CLI:</span></span>
    
        ./deploy-deis.sh -n "[resource group name]" -l "West US" -f ./azuredeploy.json -e ./azuredeploy-parameters.json
        -c ./cloud-config.yaml  
11. <span data-ttu-id="02a42-151">Po zainicjowaniu obsługi hello grupy zasobów, można wyświetlić wszystkie zasoby hello w grupie hello na klasycznego portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="02a42-151">Once hello resource group is provisioned, you can see all hello resources in hello group on Azure classic portal.</span></span> <span data-ttu-id="02a42-152">Jak pokazano w hello następującego zrzutu ekranu, hello grupa zasobów zawiera sieć wirtualną z trzech maszyn wirtualnych, które są przyłączone do toohello tego samego zestawu dostępności.</span><span class="sxs-lookup"><span data-stu-id="02a42-152">As shown in hello following screenshot, hello resource group contains a virtual network with three VMs, which are joined toohello same availability set.</span></span> <span data-ttu-id="02a42-153">Grupa Hello zawiera również modułu równoważenia obciążenia, który ma skojarzone publicznego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="02a42-153">hello group also contains a load balancer, which has an associated public IP.</span></span>
    
    ![Grupa zasobów elastycznie Hello w klasycznym portalu Azure](./media/deis-cluster/resource-group.png)

## <a name="install-hello-client"></a><span data-ttu-id="02a42-155">Instalowanie powitania klienta</span><span class="sxs-lookup"><span data-stu-id="02a42-155">Install hello client</span></span>
<span data-ttu-id="02a42-156">Należy **deisctl** toocontrol Twojego Deis klastra.</span><span class="sxs-lookup"><span data-stu-id="02a42-156">You need **deisctl** toocontrol your Deis cluster.</span></span> <span data-ttu-id="02a42-157">Chociaż deisctl jest automatycznie zainstalowane we wszystkich węzłach klastra hello, jest dobrym rozwiązaniem deisctl toouse na osobnym komputerze administracyjnych.</span><span class="sxs-lookup"><span data-stu-id="02a42-157">Although deisctl is automatically installed in all hello cluster nodes, it's a good practice toouse deisctl on a separate administrative machine.</span></span> <span data-ttu-id="02a42-158">Ponadto ponieważ wszystkie węzły są skonfigurowane przy użyciu tylko prywatnych adresów IP, należy toouse tunelowanie SSH za pośrednictwem usługi równoważenia obciążenia hello, który ma publicznego adresu IP, tooconnect toohello węzła maszyny.</span><span class="sxs-lookup"><span data-stu-id="02a42-158">Furthermore, because all nodes are configured with only private IP addresses, you'll need toouse SSH tunneling through hello load balancer, which has a public IP, tooconnect toohello node machines.</span></span> <span data-ttu-id="02a42-159">Witaj poniżej przedstawiono kroki hello konfigurowania deisctl na oddzielnych Ubuntu fizyczne lub maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="02a42-159">hello following are hello steps of setting up deisctl on a separate Ubuntu physical or virtual machine.</span></span>

1. <span data-ttu-id="02a42-160">Deis deisctl:mkdir instalacji</span><span class="sxs-lookup"><span data-stu-id="02a42-160">Install deisctl:mkdir deis</span></span>
   
        cd deis
        curl -sSL http://deis.io/deisctl/install.sh | sh -s 1.6.1
        sudo ln -fs $PWD/deisctl /usr/local/bin/deisctl
2. <span data-ttu-id="02a42-161">Dodaj agenta toossh klucza prywatnego:</span><span class="sxs-lookup"><span data-stu-id="02a42-161">Add your private key toossh agent:</span></span>
   
        eval `ssh-agent -s`
        ssh-add [path toohello private key file, see step 1 in hello previous section]
3. <span data-ttu-id="02a42-162">Skonfiguruj deisctl:</span><span class="sxs-lookup"><span data-stu-id="02a42-162">Configure deisctl:</span></span>
   
        export DEISCTL_TUNNEL=[public ip of hello load balancer]:2223

<span data-ttu-id="02a42-163">Witaj szablon definiuje reguły NAT ruchu przychodzącego, które mapują 2223 tooinstance 1, 2224 tooinstance 2 i 2225 tooinstance 3.</span><span class="sxs-lookup"><span data-stu-id="02a42-163">hello template defines inbound NAT rules that map 2223 tooinstance 1, 2224 tooinstance 2, and 2225 tooinstance 3.</span></span> <span data-ttu-id="02a42-164">Za pomocą narzędzia deisctl hello zapewnia nadmiarowość.</span><span class="sxs-lookup"><span data-stu-id="02a42-164">This provides redundancy for using hello deisctl tool.</span></span> <span data-ttu-id="02a42-165">Można sprawdzić te reguły w klasycznym portalu Azure:</span><span class="sxs-lookup"><span data-stu-id="02a42-165">You can examine these rules on Azure classic portal:</span></span>

![Reguły NAT modułu równoważenia obciążenia hello](./media/deis-cluster/nat-rules.png)

> [!NOTE]
> <span data-ttu-id="02a42-167">Obecnie hello szablon obsługuje tylko klastry węzłów 3.</span><span class="sxs-lookup"><span data-stu-id="02a42-167">Currently hello template only supports 3-node clusters.</span></span> <span data-ttu-id="02a42-168">Jest to spowodowane ograniczenia w szablonie usługi Azure Resource Manager definicję reguły NAT, które nie obsługują pętli składni.</span><span class="sxs-lookup"><span data-stu-id="02a42-168">This is because of a limitation in Azure Resource Manager template NAT rule definition, which doesn’t support loop syntax.</span></span>
> 
> 

## <a name="install-and-start-hello-deis-platform"></a><span data-ttu-id="02a42-169">Zainstaluj i uruchom hello Deis platformy</span><span class="sxs-lookup"><span data-stu-id="02a42-169">Install and start hello Deis platform</span></span>
<span data-ttu-id="02a42-170">Teraz można używać deisctl tooinstall i rozpocząć hello Deis platformy:</span><span class="sxs-lookup"><span data-stu-id="02a42-170">Now you can use deisctl tooinstall and start hello Deis platform:</span></span>

    deisctl config platform set domain=[some domain]
    deisctl config platform set sshPrivateKey=[path toohello private key file]
    deisctl install platform
    deisctl start platform

> [!NOTE]
> <span data-ttu-id="02a42-171">Początkowy platformy hello zajmie trochę czasu (jak 10 minut).</span><span class="sxs-lookup"><span data-stu-id="02a42-171">Starting hello platform takes a while (as much as 10 minutes).</span></span> <span data-ttu-id="02a42-172">Szczególnie uruchamianie usługi konstruktora hello może zająć dużo czasu.</span><span class="sxs-lookup"><span data-stu-id="02a42-172">Especially, starting hello builder service can take a long time.</span></span> <span data-ttu-id="02a42-173">Czasami zajmuje kilka prób toosucceed: Jeśli operacja hello toohang, spróbuj wpisać `ctrl+c` toobreak wykonanie polecenia hello i spróbuj ponownie.</span><span class="sxs-lookup"><span data-stu-id="02a42-173">And sometimes it takes a few tries toosucceed: If hello operation seems toohang, try typing `ctrl+c` toobreak execution of hello command and retry.</span></span>
> 
> 

<span data-ttu-id="02a42-174">Można użyć `deisctl list` tooverify, jeśli wszystkie usługi są uruchomione:</span><span class="sxs-lookup"><span data-stu-id="02a42-174">You can use `deisctl list` tooverify if all services are running:</span></span>

    deisctl list
    UNIT                            MACHINE                 LOAD    ACTIVE          SUB
    deis-builder.service            ebe3005e.../10.0.0.6    loaded  active          running
    deis-controller.service         ebe3005e.../10.0.0.6    loaded  active          running
    deis-database.service           9c79bbdd.../10.0.0.5    loaded  active          running
    deis-logger.service             9c79bbdd.../10.0.0.5    loaded  active          running
    deis-logspout.service           8d658d5a.../10.0.0.4    loaded  active          running
    deis-logspout.service           9c79bbdd.../10.0.0.5    loaded  active          running
    deis-logspout.service           ebe3005e.../10.0.0.6    loaded  active          running
    deis-publisher.service          8d658d5a.../10.0.0.4    loaded  active          running
    deis-publisher.service          9c79bbdd.../10.0.0.5    loaded  active          running
    deis-publisher.service          ebe3005e.../10.0.0.6    loaded  active          running
    deis-registry@1.service         ebe3005e.../10.0.0.6    loaded  active          running
    deis-router@1.service           ebe3005e.../10.0.0.6    loaded  active          running
    deis-router@2.service           8d658d5a.../10.0.0.4    loaded  active          running
    deis-router@3.service           9c79bbdd.../10.0.0.5    loaded  active          running
    deis-store-daemon.service       8d658d5a.../10.0.0.4    loaded  active          running
    deis-store-daemon.service       9c79bbdd.../10.0.0.5    loaded  active          running
    deis-store-daemon.service       ebe3005e.../10.0.0.6    loaded  active          running
    deis-store-gateway@1.service    9c79bbdd.../10.0.0.5    loaded  active          running
    deis-store-metadata.service     8d658d5a.../10.0.0.4    loaded  active          running
    deis-store-metadata.service     9c79bbdd.../10.0.0.5    loaded  active          running
    deis-store-metadata.service     ebe3005e.../10.0.0.6    loaded  active          running
    deis-store-monitor.service      8d658d5a.../10.0.0.4    loaded  active          running
    deis-store-monitor.service      9c79bbdd.../10.0.0.5    loaded  active          running
    deis-store-monitor.service      ebe3005e.../10.0.0.6    loaded  active          running
    deis-store-volume.service       8d658d5a.../10.0.0.4    loaded  active          running
    deis-store-volume.service       9c79bbdd.../10.0.0.5    loaded  active          running
    deis-store-volume.service       ebe3005e.../10.0.0.6    loaded  active          running

<span data-ttu-id="02a42-175">Gratulacje!</span><span class="sxs-lookup"><span data-stu-id="02a42-175">Congratulations!</span></span> <span data-ttu-id="02a42-176">Teraz już wiem uruchomionej Deis clsuter na platformie Azure!</span><span class="sxs-lookup"><span data-stu-id="02a42-176">Now you've got a running Deis clsuter on Azure!</span></span> <span data-ttu-id="02a42-177">Następnie umożliwia wdrożenie przykładowego Przejdź aplikacji toosee hello klastra w akcji.</span><span class="sxs-lookup"><span data-stu-id="02a42-177">Next, let's deploy a sample Go application toosee hello cluster in action.</span></span>

## <a name="deploy-and-scale-a-hello-world-application"></a><span data-ttu-id="02a42-178">Wdrażanie i skalowanie aplikacji Hello World</span><span class="sxs-lookup"><span data-stu-id="02a42-178">Deploy and scale a Hello World application</span></span>
<span data-ttu-id="02a42-179">Witaj poniższej procedurze pokazano, jak toodeploy "Hello World" Przejdź klastra toohello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="02a42-179">hello following steps show how toodeploy a "Hello World" Go application toohello cluster.</span></span> <span data-ttu-id="02a42-180">kroki Hello są oparte na [Deis dokumentacji](http://docs.deis.io/en/latest/using_deis/using-dockerfiles/#using-dockerfiles).</span><span class="sxs-lookup"><span data-stu-id="02a42-180">hello steps are based on [Deis documentation](http://docs.deis.io/en/latest/using_deis/using-dockerfiles/#using-dockerfiles).</span></span>

1. <span data-ttu-id="02a42-181">Dla routingu toowork siatki hello prawidłowo, należy toohave rekord A symboli wieloznacznych dla domeny wskazuje toohello publicznego adresu IP usługi równoważenia obciążenia hello.</span><span class="sxs-lookup"><span data-stu-id="02a42-181">For hello routing mesh toowork properly, you’ll need toohave a wildcard A record for your domain pointing toohello public IP of hello load balancer.</span></span> <span data-ttu-id="02a42-182">Witaj Poniższy zrzut ekranu przedstawia hello A rekord rejestracji domen przykładowe na GoDaddy:</span><span class="sxs-lookup"><span data-stu-id="02a42-182">hello following screenshot shows hello A record for a sample domain registration on GoDaddy:</span></span>
   
    ![Rekord GoDaddy A](./media/deis-cluster/go-daddy.png)
   
   <p />
2. <span data-ttu-id="02a42-184">Deis instalacji:</span><span class="sxs-lookup"><span data-stu-id="02a42-184">Install deis:</span></span>
   
        mkdir deis
        cd deis
        curl -sSL http://deis.io/deis-cli/install.sh | sh
        ln -fs $PWD/deis /usr/local/bin/deis
3. <span data-ttu-id="02a42-185">Utwórz nowy klucz SSH, a następnie dodaj tooGitHub klucza publicznego hello (oczywiście można również wykorzystać istniejące klucze).</span><span class="sxs-lookup"><span data-stu-id="02a42-185">Create a new SSH key, and then add hello public key tooGitHub (of course, you can also reuse your existing keys).</span></span> <span data-ttu-id="02a42-186">toocreate nową parę kluczy SSH, należy użyć:</span><span class="sxs-lookup"><span data-stu-id="02a42-186">toocreate a new SSH key pair, use:</span></span>
   
        cd ~/.ssh
        ssh-keygen (press [Enter]s toouse default file names and empty passcode)
4. <span data-ttu-id="02a42-187">Dodaj id_rsa.pub lub klucza publicznego hello wybranych tooGitHub.</span><span class="sxs-lookup"><span data-stu-id="02a42-187">Add id_rsa.pub, or hello public key of your choice, tooGitHub.</span></span> <span data-ttu-id="02a42-188">Można to zrobić za pomocą hello dodać SSH klucza przycisku w ekranie konfiguracji klucze SSH:</span><span class="sxs-lookup"><span data-stu-id="02a42-188">You can do this by using hello Add SSH key button in your SSH keys configuration screen:</span></span>
   
   ![Klucz usługi GitHub](./media/deis-cluster/github-key.png)
   
   <p />
5. <span data-ttu-id="02a42-190">Zarejestruj nowego użytkownika:</span><span class="sxs-lookup"><span data-stu-id="02a42-190">Register a new user:</span></span>
   
        deis register http://deis.[your domain]
   <p />
6. <span data-ttu-id="02a42-191">Dodaj klucz SSH hello:</span><span class="sxs-lookup"><span data-stu-id="02a42-191">Add hello SSH key:</span></span>
   
        deis keys:add [path tooyour SSH public key]
   <p />      
7. <span data-ttu-id="02a42-192">Tworzenie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="02a42-192">Create an application.</span></span>
   
        git clone https://github.com/deis/helloworld.git
        cd helloworld
        deis create
        git push deis master
   <p /><span data-ttu-id="02a42-193">
8.Witaj git wypychania wyzwoli toobe obrazów Docker wbudowany i wdrożeniu, którego może potrwać kilka minut.</span><span class="sxs-lookup"><span data-stu-id="02a42-193">
8. hello git push will trigger Docker images toobe built and deployed, which will take a few minutes.</span></span> <span data-ttu-id="02a42-194">Moje doświadczeniu czasami kroku 10 (Pushing obrazu tooprivate repozytorium) mogą wykraczać.</span><span class="sxs-lookup"><span data-stu-id="02a42-194">From my experience, occasionally, Step 10 (Pushing image tooprivate repository) may hang.</span></span> <span data-ttu-id="02a42-195">W takim przypadku można zatrzymać procesu hello przy użyciu aplikacji hello Usuń "deis aplikacji: zniszczyć <application name> ` tooremove hello application and try again. You can use `deis apps:list" toofind limit hello nazwę aplikacji.</span><span class="sxs-lookup"><span data-stu-id="02a42-195">When this happens, you can stop hello process, remove hello application using `deis apps:destroy –a <application name>` tooremove hello application and try again. You can use `deis apps:list` toofind out hello name of your application.</span></span> <span data-ttu-id="02a42-196">Jeśli wszystko działa powinny być widoczne przypominać następujące hello na końcu hello dane wyjściowe poleceń:</span><span class="sxs-lookup"><span data-stu-id="02a42-196">If everything works out, you should see something like hello following at hello end of command outputs:</span></span>
   
        -----> Launching...
               done, lambda-underdog:v2 deployed tooDeis
               http://lambda-underdog.artitrack.com
               toolearn more, use `deis help` or visit http://deis.io
        toossh://git@deis.artitrack.com:2222/lambda-underdog.git
         * [new branch]      master -> master
   <p />
9. <span data-ttu-id="02a42-197">Sprawdź, czy aplikacja hello działa:</span><span class="sxs-lookup"><span data-stu-id="02a42-197">Verify if hello application is working:</span></span>
   
        curl -S http://[your application name].[your domain]
   <span data-ttu-id="02a42-198">Powinien zostać wyświetlony następujący ekran:</span><span class="sxs-lookup"><span data-stu-id="02a42-198">You should see:</span></span>
   
        Welcome tooDeis!
        See hello documentation at http://docs.deis.io/ for more information.
        (you can use geis apps:list tooget hello name of your application).
   <p />
10. <span data-ttu-id="02a42-199">Skala wystąpień too3 aplikacji hello:</span><span class="sxs-lookup"><span data-stu-id="02a42-199">Scale hello application too3 instances:</span></span>
    
        deis scale cmd=3
    <p />
11. <span data-ttu-id="02a42-200">Opcjonalnie można użyć deis szczegóły tooexamine informacje o aplikacji.</span><span class="sxs-lookup"><span data-stu-id="02a42-200">Optionally, you can use deis info tooexamine details of your application.</span></span> <span data-ttu-id="02a42-201">Witaj następujące dane wyjściowe są z mojej wdrożenia aplikacji:</span><span class="sxs-lookup"><span data-stu-id="02a42-201">hello following outputs are from my application deployment:</span></span>
    
        deis info
        === lambda-underdog Application
        {
          "updated": "2015-05-22T06:14:10UTC",
          "uuid": "10c74ee7-b7ff-4786-967a-7e65af7eabc3",
          "created": "2015-05-22T06:07:55UTC",
          "url": "lambda-underdog.artitrack.com",
          "owner": "haishi",
          "id": "lambda-underdog",
          "structure": {
            "cmd": 3
          }
        }
    
        === lambda-underdog Processes
        --- cmd:
        cmd.1 up (v2)
        cmd.2 up (v2)
        cmd.3 up (v2)
    
        === lambda-underdog Domains
        No domains

## <a name="next-steps"></a><span data-ttu-id="02a42-202">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="02a42-202">Next Steps</span></span>
<span data-ttu-id="02a42-203">W tym artykule udał za pośrednictwem wszystkich tooprovision kroki hello Deis nowy klaster na platformie Azure przy użyciu szablonu usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="02a42-203">This article walked you through all hello steps tooprovision a new Deis cluster on Azure using an Azure Resource Manager template.</span></span> <span data-ttu-id="02a42-204">Szablon Hello obsługuje nadmiarowości w narzędzi połączeń, a także równoważenie obciążenia dla wdrożonych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="02a42-204">hello template supports redundancy in tooling connections as well as load balancing for deployed applications.</span></span> <span data-ttu-id="02a42-205">Szablon Hello unika również na węzeł elementu członkowskiego, które zapisuje cenne zasoby publicznych adresów IP i zapewnia bardziej zabezpieczonym środowisku toohost aplikacji przy użyciu publicznych adresów IP.</span><span class="sxs-lookup"><span data-stu-id="02a42-205">hello template also avoids using public IPs on member nodes, which saves precious public IP resources and provides a more secured environment toohost applications.</span></span> <span data-ttu-id="02a42-206">toolearn więcej, zobacz następujące artykuły hello:</span><span class="sxs-lookup"><span data-stu-id="02a42-206">toolearn more, see hello following articles:</span></span>

<span data-ttu-id="02a42-207">[Omówienie usługi Azure Resource Manager][resource-group-overview]</span><span class="sxs-lookup"><span data-stu-id="02a42-207">[Azure Resource Manager Overview][resource-group-overview]</span></span>  
<span data-ttu-id="02a42-208">[Jak toouse hello wiersza polecenia platformy Azure][azure-command-line-tools]</span><span class="sxs-lookup"><span data-stu-id="02a42-208">[How toouse hello Azure CLI][azure-command-line-tools]</span></span>  
<span data-ttu-id="02a42-209">[Używanie programu Azure PowerShell z usługą Azure Resource Manager][powershell-azure-resource-manager]</span><span class="sxs-lookup"><span data-stu-id="02a42-209">[Using Azure PowerShell with Azure Resource Manager][powershell-azure-resource-manager]</span></span>  

[azure-command-line-tools]: ../../cli-install-nodejs.md
[resource-group-overview]: ../../azure-resource-manager/resource-group-overview.md
[powershell-azure-resource-manager]: ../../azure-resource-manager/powershell-azure-resource-manager.md
