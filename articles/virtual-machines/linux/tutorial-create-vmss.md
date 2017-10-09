---
title: aaaCreate zestawy skalowania maszyny wirtualnej dla systemu Linux na platformie Azure | Dokumentacja firmy Microsoft
description: "Tworzenie i wdrażanie aplikacji wysokiej dostępności na maszynach wirtualnych systemu Linux przy użyciu zestawu skali maszyny wirtualnej"
services: virtual-machine-scale-sets
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: 
ms.assetid: 
ms.service: virtual-machine-scale-sets
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: azurecli
ms.topic: article
ms.date: 08/11/2017
ms.author: iainfou
ms.openlocfilehash: 00dd81043f9be46ef2dc6dfe97eefdb20944ee13
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-scale-set-and-deploy-a-highly-available-app-on-linux"></a><span data-ttu-id="57c22-103">Tworzenie zestawu skali maszyny wirtualnej i wdrażanie aplikacji wysokiej dostępności w systemie Linux</span><span class="sxs-lookup"><span data-stu-id="57c22-103">Create a Virtual Machine Scale Set and deploy a highly available app on Linux</span></span>
<span data-ttu-id="57c22-104">Zestaw skali maszyny wirtualnej umożliwia toodeploy i zarządzać zestawem identyczne, automatyczne skalowanie maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="57c22-104">A virtual machine scale set allows you toodeploy and manage a set of identical, auto-scaling virtual machines.</span></span> <span data-ttu-id="57c22-105">Można ręcznie skalować hello liczbę maszyn wirtualnych w zestawie skalowania hello lub zdefiniuj tooautoscale reguły na podstawie użycia procesora CPU, pamięci żądanie lub ruchu sieciowego.</span><span class="sxs-lookup"><span data-stu-id="57c22-105">You can scale hello number of VMs in hello scale set manually, or define rules tooautoscale based on CPU usage, memory demand, or network traffic.</span></span> <span data-ttu-id="57c22-106">W tym samouczku możesz wdrożyć skali maszyny wirtualnej w usłudze Azure.</span><span class="sxs-lookup"><span data-stu-id="57c22-106">In this tutorial, you deploy a virtual machine scale set in Azure.</span></span> <span data-ttu-id="57c22-107">Omawiane kwestie:</span><span class="sxs-lookup"><span data-stu-id="57c22-107">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="57c22-108">Użyj toocreate init chmury tooscale aplikacji</span><span class="sxs-lookup"><span data-stu-id="57c22-108">Use cloud-init toocreate an app tooscale</span></span>
> * <span data-ttu-id="57c22-109">Utwórz zestaw skali maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="57c22-109">Create a virtual machine scale set</span></span>
> * <span data-ttu-id="57c22-110">Zwiększanie lub zmniejszanie hello liczbę wystąpień w zestawie skalowania</span><span class="sxs-lookup"><span data-stu-id="57c22-110">Increase or decrease hello number of instances in a scale set</span></span>
> * <span data-ttu-id="57c22-111">Wyświetl informacje o połączeniu dla wystąpień zestawu skali</span><span class="sxs-lookup"><span data-stu-id="57c22-111">View connection info for scale set instances</span></span>
> * <span data-ttu-id="57c22-112">Dysków danych w zestawie skalowania</span><span class="sxs-lookup"><span data-stu-id="57c22-112">Use data disks in a scale set</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="57c22-113">Jeśli wybierz tooinstall i użyj interfejsu wiersza polecenia hello lokalnie, w tym samouczku wymaga działają hello Azure CLI w wersji 2.0.4 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="57c22-113">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="57c22-114">Uruchom `az --version` toofind hello wersji.</span><span class="sxs-lookup"><span data-stu-id="57c22-114">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="57c22-115">Jeśli potrzebujesz tooinstall lub uaktualniania, zobacz [zainstalować Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="57c22-115">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="scale-set-overview"></a><span data-ttu-id="57c22-116">Omówienie zestawu skali</span><span class="sxs-lookup"><span data-stu-id="57c22-116">Scale Set overview</span></span>
<span data-ttu-id="57c22-117">Zestaw skali maszyny wirtualnej umożliwia toodeploy i zarządzać zestawem identyczne, automatyczne skalowanie maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="57c22-117">A virtual machine scale set allows you toodeploy and manage a set of identical, auto-scaling virtual machines.</span></span> <span data-ttu-id="57c22-118">Skali ustawia hello Użyj tego samego składniki jako poznanie w samouczku poprzedniej hello zbyt[tworzyć maszyny wirtualne o wysokiej dostępności](tutorial-availability-sets.md).</span><span class="sxs-lookup"><span data-stu-id="57c22-118">Scale sets use hello same components as you learned about in hello previous tutorial too[Create highly available VMs](tutorial-availability-sets.md).</span></span> <span data-ttu-id="57c22-119">Maszyny wirtualne w zestawie skalowania są tworzone w dostępności ustaw i rozpowszechniane w domenach awarii i aktualizacji logiki.</span><span class="sxs-lookup"><span data-stu-id="57c22-119">VMs in a scale set are created in an availability set and distributed across logic fault and update domains.</span></span>

<span data-ttu-id="57c22-120">Maszyny wirtualne są tworzone zgodnie z potrzebami w zestawie skalowania.</span><span class="sxs-lookup"><span data-stu-id="57c22-120">VMs are created as needed in a scale set.</span></span> <span data-ttu-id="57c22-121">Zdefiniuj toocontrol reguł skalowania automatycznego, kiedy maszyny wirtualne są dodawane lub usuwane z hello zestaw skali.</span><span class="sxs-lookup"><span data-stu-id="57c22-121">You define autoscale rules toocontrol how and when VMs are added or removed from hello scale set.</span></span> <span data-ttu-id="57c22-122">Te reguły może wyzwolić na podstawie metryk, takich jak obciążenie procesora CPU, pamięć lub ruchu sieciowego.</span><span class="sxs-lookup"><span data-stu-id="57c22-122">These rules can trigger based on metrics such as CPU load, memory usage, or network traffic.</span></span>

<span data-ttu-id="57c22-123">Obsługa się too1, 000 maszyn wirtualnych, gdy używasz obrazu platformy Azure zestawach skali.</span><span class="sxs-lookup"><span data-stu-id="57c22-123">Scale sets support up too1,000 VMs when you use an Azure platform image.</span></span> <span data-ttu-id="57c22-124">W przypadku obciążeń produkcyjnych, warto zapoznać się z zbyt[utworzyć niestandardowy obraz maszyny Wirtualnej](tutorial-custom-images.md).</span><span class="sxs-lookup"><span data-stu-id="57c22-124">For production workloads, you may wish too[Create a custom VM image](tutorial-custom-images.md).</span></span> <span data-ttu-id="57c22-125">Możesz utworzyć zapasowych maszyn wirtualnych too100 w skali ustawić przy użyciu obrazu niestandardowego.</span><span class="sxs-lookup"><span data-stu-id="57c22-125">You can create up too100 VMs in a scale set when using a custom image.</span></span>


## <a name="create-an-app-tooscale"></a><span data-ttu-id="57c22-126">Utwórz tooscale aplikacji</span><span class="sxs-lookup"><span data-stu-id="57c22-126">Create an app tooscale</span></span>
<span data-ttu-id="57c22-127">W środowisku produkcyjnym, możesz za[utworzyć niestandardowy obraz maszyny Wirtualnej](tutorial-custom-images.md) zawierającą aplikacji zainstalowane i skonfigurowane.</span><span class="sxs-lookup"><span data-stu-id="57c22-127">For production use, you may wish too[Create a custom VM image](tutorial-custom-images.md) that includes your application installed and configured.</span></span> <span data-ttu-id="57c22-128">W tym samouczku umożliwia dostosowywanie hello maszyn wirtualnych na pierwszym tooquickly rozruchu zobacz zestaw akcji skalowania.</span><span class="sxs-lookup"><span data-stu-id="57c22-128">For this tutorial, lets customize hello VMs on first boot tooquickly see a scale set in action.</span></span>

<span data-ttu-id="57c22-129">W poprzednich samouczka przedstawiono [jak toocustomize maszyny wirtualnej systemu Linux, po pierwszym uruchomieniu komputera](tutorial-automate-vm-deployment.md) z inicjowaniem chmury.</span><span class="sxs-lookup"><span data-stu-id="57c22-129">In a previous tutorial, you learned [How toocustomize a Linux virtual machine on first boot](tutorial-automate-vm-deployment.md) with cloud-init.</span></span> <span data-ttu-id="57c22-130">Można użyć tej samej chmurze inicjowania konfiguracji pliku tooinstall NGINX hello i uruchom prostej aplikacji Node.js "Hello World".</span><span class="sxs-lookup"><span data-stu-id="57c22-130">You can use hello same cloud-init configuration file tooinstall NGINX and run a simple 'Hello World' Node.js app.</span></span> 

<span data-ttu-id="57c22-131">W bieżącym powłoki, Utwórz plik o nazwie *init.txt chmury* i Wklej powitania po konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="57c22-131">In your current shell, create a file named *cloud-init.txt* and paste hello following configuration.</span></span> <span data-ttu-id="57c22-132">Na przykład utworzyć plik hello w hello powłoki chmury nie na komputerze lokalnym.</span><span class="sxs-lookup"><span data-stu-id="57c22-132">For example, create hello file in hello Cloud Shell not on your local machine.</span></span> <span data-ttu-id="57c22-133">Wprowadź `sensible-editor cloud-init.txt` toocreate hello pliku i wyświetlić listę dostępnych edytory.</span><span class="sxs-lookup"><span data-stu-id="57c22-133">Enter `sensible-editor cloud-init.txt` toocreate hello file and see a list of available editors.</span></span> <span data-ttu-id="57c22-134">Upewnij się, że plik całego init chmury hello został poprawnie skopiowany, szczególnie hello pierwszy wiersz:</span><span class="sxs-lookup"><span data-stu-id="57c22-134">Make sure that hello whole cloud-init file is copied correctly, especially hello first line:</span></span>

```yaml
#cloud-config
package_upgrade: true
packages:
  - nginx
  - nodejs
  - npm
write_files:
  - owner: www-data:www-data
  - path: /etc/nginx/sites-available/default
    content: |
      server {
        listen 80;
        location / {
          proxy_pass http://localhost:3000;
          proxy_http_version 1.1;
          proxy_set_header Upgrade $http_upgrade;
          proxy_set_header Connection keep-alive;
          proxy_set_header Host $host;
          proxy_cache_bypass $http_upgrade;
        }
      }
  - owner: azureuser:azureuser
  - path: /home/azureuser/myapp/index.js
    content: |
      var express = require('express')
      var app = express()
      var os = require('os');
      app.get('/', function (req, res) {
        res.send('Hello World from host ' + os.hostname() + '!')
      })
      app.listen(3000, function () {
        console.log('Hello world app listening on port 3000!')
      })
runcmd:
  - service nginx restart
  - cd "/home/azureuser/myapp"
  - npm init
  - npm install express -y
  - nodejs index.js
```


## <a name="create-a-scale-set"></a><span data-ttu-id="57c22-135">Utwórz zestaw skali</span><span class="sxs-lookup"><span data-stu-id="57c22-135">Create a scale set</span></span>
<span data-ttu-id="57c22-136">Przed utworzeniem zestaw skali, Utwórz grupę zasobów o [Tworzenie grupy az](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="57c22-136">Before you can create a scale set, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="57c22-137">Witaj poniższy przykład tworzy grupę zasobów o nazwie *myResourceGroupScaleSet* w hello *eastus* lokalizacji:</span><span class="sxs-lookup"><span data-stu-id="57c22-137">hello following example creates a resource group named *myResourceGroupScaleSet* in hello *eastus* location:</span></span>

```azurecli-interactive 
az group create --name myResourceGroupScaleSet --location eastus
```

<span data-ttu-id="57c22-138">Teraz Utwórz zestaw o skali maszyny wirtualnej [az vmss utworzyć](/cli/azure/vmss#create).</span><span class="sxs-lookup"><span data-stu-id="57c22-138">Now create a virtual machine scale set with [az vmss create](/cli/azure/vmss#create).</span></span> <span data-ttu-id="57c22-139">Witaj poniższy przykład tworzy zestaw o nazwie skalowania *myScaleSet*, używa hello init chmury pliku toocustomize hello maszyny Wirtualnej i generuje klucze SSH, jeśli nie istnieją:</span><span class="sxs-lookup"><span data-stu-id="57c22-139">hello following example creates a scale set named *myScaleSet*, uses hello cloud-init file toocustomize hello VM, and generates SSH keys if they do not exist:</span></span>

```azurecli-interactive 
az vmss create \
  --resource-group myResourceGroupScaleSet \
  --name myScaleSet \
  --image UbuntuLTS \
  --upgrade-policy-mode automatic \
  --custom-data cloud-init.txt \
  --admin-username azureuser \
  --generate-ssh-keys      
```

<span data-ttu-id="57c22-140">Go zajmuje kilka minut toocreate i skonfiguruje wszystkie zasoby zestaw skalowania hello maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="57c22-140">It takes a few minutes toocreate and configure all hello scale set resources and VMs.</span></span> <span data-ttu-id="57c22-141">Istnieją zadania w tle, które nadal toorun po hello Azure CLI zwraca toohello wiersza.</span><span class="sxs-lookup"><span data-stu-id="57c22-141">There are background tasks that continue toorun after hello Azure CLI returns you toohello prompt.</span></span> <span data-ttu-id="57c22-142">Może to być inny kilka minut, w celu uzyskania dostępu do aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="57c22-142">It may be another couple of minutes before you can access hello app.</span></span>


## <a name="allow-web-traffic"></a><span data-ttu-id="57c22-143">Zezwalaj na ruch w sieci web</span><span class="sxs-lookup"><span data-stu-id="57c22-143">Allow web traffic</span></span>
<span data-ttu-id="57c22-144">Moduł równoważenia obciążenia został utworzony automatycznie jako część zestawu skali maszyny wirtualnej hello.</span><span class="sxs-lookup"><span data-stu-id="57c22-144">A load balancer was created automatically as part of hello virtual machine scale set.</span></span> <span data-ttu-id="57c22-145">Moduł równoważenia obciążenia Hello dystrybuuje ruch zestawu zdefiniowanego maszyn wirtualnych przy użyciu reguły modułu równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="57c22-145">hello load balancer distributes traffic across a set of defined VMs using load balancer rules.</span></span> <span data-ttu-id="57c22-146">Dowiedz się więcej o pojęcia dotyczące usługi równoważenia obciążenia i konfiguracji w następnym samouczku hello [jak tooload złoty środek między maszynami wirtualnymi na platformie Azure](tutorial-load-balancer.md).</span><span class="sxs-lookup"><span data-stu-id="57c22-146">You can learn more about load balancer concepts and configuration in hello next tutorial, [How tooload balance virtual machines in Azure](tutorial-load-balancer.md).</span></span>

<span data-ttu-id="57c22-147">Aplikacja sieci web tooallow ruchu tooreach hello, tworzenia reguły za pomocą [utworzyć regułę równoważeniem obciążenia sieciowego az](/cli/azure/network/lb/rule#create).</span><span class="sxs-lookup"><span data-stu-id="57c22-147">tooallow traffic tooreach hello web app, create a rule with [az network lb rule create](/cli/azure/network/lb/rule#create).</span></span> <span data-ttu-id="57c22-148">Witaj poniższy przykład powoduje utworzenie reguły o nazwie *myLoadBalancerRuleWeb*:</span><span class="sxs-lookup"><span data-stu-id="57c22-148">hello following example creates a rule named *myLoadBalancerRuleWeb*:</span></span>

```azurecli-interactive 
az network lb rule create \
  --resource-group myResourceGroupScaleSet \
  --name myLoadBalancerRuleWeb \
  --lb-name myScaleSetLB \
  --backend-pool-name myScaleSetLBBEPool \
  --backend-port 80 \
  --frontend-ip-name loadBalancerFrontEnd \
  --frontend-port 80 \
  --protocol tcp
```

## <a name="test-your-app"></a><span data-ttu-id="57c22-149">Testowanie aplikacji</span><span class="sxs-lookup"><span data-stu-id="57c22-149">Test your app</span></span>
<span data-ttu-id="57c22-150">toosee aplikacji Node.js w sieci web hello uzyskać hello publicznego adresu IP z usługi równoważenia obciążenia z [az sieci ip publicznego Pokaż](/cli/azure/network/public-ip#show).</span><span class="sxs-lookup"><span data-stu-id="57c22-150">toosee your Node.js app on hello web, obtain hello public IP address of your load balancer with [az network public-ip show](/cli/azure/network/public-ip#show).</span></span> <span data-ttu-id="57c22-151">Witaj poniższy przykład uzyskuje hello adres IP dla *myScaleSetLBPublicIP* utworzone jako część zestawu skalowania hello:</span><span class="sxs-lookup"><span data-stu-id="57c22-151">hello following example obtains hello IP address for *myScaleSetLBPublicIP* created as part of hello scale set:</span></span>

```azurecli-interactive 
az network public-ip show \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSetLBPublicIP \
    --query [ipAddress] \
    --output tsv
```

<span data-ttu-id="57c22-152">Wprowadź hello publicznego adresu IP w przeglądarce sieci web tooa.</span><span class="sxs-lookup"><span data-stu-id="57c22-152">Enter hello public IP address in tooa web browser.</span></span> <span data-ttu-id="57c22-153">Aplikacja Hello jest wyświetlana, łącznie z nazwą hosta hello hello hello tej maszyny Wirtualnej obciążenia ruchu równoważenia dystrybuowane do:</span><span class="sxs-lookup"><span data-stu-id="57c22-153">hello app is displayed, including hello hostname of hello VM that hello load balancer distributed traffic to:</span></span>

![Uruchomionej aplikacji Node.js](./media/tutorial-create-vmss/running-nodejs-app.png)

<span data-ttu-id="57c22-155">zestaw w akcji skalowania hello toosee, możesz można życie odświeżania obciążenia hello toosee przeglądarki sieci web równoważenia rozpowszechniają wszystkich aplikacji uruchomionych maszyn wirtualnych hello ruchu.</span><span class="sxs-lookup"><span data-stu-id="57c22-155">toosee hello scale set in action, you can force-refresh your web browser toosee hello load balancer distribute traffic across all hello VMs running your app.</span></span>


## <a name="management-tasks"></a><span data-ttu-id="57c22-156">Zadania zarządzania</span><span class="sxs-lookup"><span data-stu-id="57c22-156">Management tasks</span></span>
<span data-ttu-id="57c22-157">W całym cyklu życia hello zestawu skali hello, może być konieczne toorun jednego lub więcej zadań zarządzania.</span><span class="sxs-lookup"><span data-stu-id="57c22-157">Throughout hello lifecycle of hello scale set, you may need toorun one or more management tasks.</span></span> <span data-ttu-id="57c22-158">Ponadto można toocreate skrypty, które automatyzacji różnych zadań cyklu życia.</span><span class="sxs-lookup"><span data-stu-id="57c22-158">Additionally, you may want toocreate scripts that automate various lifecycle-tasks.</span></span> <span data-ttu-id="57c22-159">Hello Azure CLI 2.0 zapewnia toodo szybko tych zadań.</span><span class="sxs-lookup"><span data-stu-id="57c22-159">hello Azure CLI 2.0 provides a quick way toodo those tasks.</span></span> <span data-ttu-id="57c22-160">Poniżej przedstawiono kilka typowych zadań.</span><span class="sxs-lookup"><span data-stu-id="57c22-160">Here are a few common tasks.</span></span>

### <a name="view-vms-in-a-scale-set"></a><span data-ttu-id="57c22-161">Maszyny wirtualne widoku w zestawie skalowania</span><span class="sxs-lookup"><span data-stu-id="57c22-161">View VMs in a scale set</span></span>
<span data-ttu-id="57c22-162">Ustaw listę maszyn wirtualnych uruchomionych w skali sieci tooview, użyj [wystąpienia listy az vmss](/cli/azure/vmss#list-instances) w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="57c22-162">tooview a list of VMs running in your scale set, use [az vmss list-instances](/cli/azure/vmss#list-instances) as follows:</span></span>

```azurecli-interactive 
az vmss list-instances \
  --resource-group myResourceGroupScaleSet \
  --name myScaleSet \
  --output table
```

<span data-ttu-id="57c22-163">Witaj danych wyjściowych jest toohello podobnie poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="57c22-163">hello output is similar toohello following example:</span></span>

```azurecli-interactive 
  InstanceId  LatestModelApplied    Location    Name          ProvisioningState    ResourceGroup            VmId
------------  --------------------  ----------  ------------  -------------------  -----------------------  ------------------------------------
           1  True                  eastus      myScaleSet_1  Succeeded            MYRESOURCEGROUPSCALESET  c72ddc34-6c41-4a53-b89e-dd24f27b30ab
           3  True                  eastus      myScaleSet_3  Succeeded            MYRESOURCEGROUPSCALESET  44266022-65c3-49c5-92dd-88ffa64f95da
```


### <a name="increase-or-decrease-vm-instances"></a><span data-ttu-id="57c22-164">Zwiększanie lub zmniejszanie wystąpień maszyn wirtualnych</span><span class="sxs-lookup"><span data-stu-id="57c22-164">Increase or decrease VM instances</span></span>
<span data-ttu-id="57c22-165">toosee hello liczbę wystąpień obecnie w skali ustawiono, użyj [Pokaż vmss az](/cli/azure/vmss#show) i wykonywać zapytania na *sku.capacity*:</span><span class="sxs-lookup"><span data-stu-id="57c22-165">toosee hello number of instances you currently have in a scale set, use [az vmss show](/cli/azure/vmss#show) and query on *sku.capacity*:</span></span>

```azurecli-interactive 
az vmss show \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet \
    --query [sku.capacity] \
    --output table
```

<span data-ttu-id="57c22-166">Możesz ręcznie zwiększyć lub zmniejszyć liczbę hello maszyn wirtualnych w skali hello ustawiony za pomocą [skali vmss az](/cli/azure/vmss#scale).</span><span class="sxs-lookup"><span data-stu-id="57c22-166">You can then manually increase or decrease hello number of virtual machines in hello scale set with [az vmss scale](/cli/azure/vmss#scale).</span></span> <span data-ttu-id="57c22-167">Witaj poniższy przykład przedstawia hello liczbę maszyn wirtualnych w sieci za zestaw skalowania*5*:</span><span class="sxs-lookup"><span data-stu-id="57c22-167">hello following example sets hello number of VMs in your scale set too*5*:</span></span>

```azurecli-interactive 
az vmss scale \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet \
    --new-capacity 5
```

<span data-ttu-id="57c22-168">Reguły automatycznego skalowania umożliwiają definiowanie konfiguracji tooscale w górę lub w dół hello liczbę maszyn wirtualnych w skali sieci toodemand odpowiedzi, takie jak ruch w sieci i użycie procesora CPU.</span><span class="sxs-lookup"><span data-stu-id="57c22-168">Autoscale rules let you define how tooscale up or down hello number of VMs in your scale set in response toodemand such as network traffic or CPU usage.</span></span> <span data-ttu-id="57c22-169">Obecnie te zasady nie można ustawić w 2.0 interfejsu wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="57c22-169">Currently, these rules cannot be set in Azure CLI 2.0.</span></span> <span data-ttu-id="57c22-170">Użyj hello [portalu Azure](https://portal.azure.com) tooconfigure automatycznego skalowania.</span><span class="sxs-lookup"><span data-stu-id="57c22-170">Use hello [Azure portal](https://portal.azure.com) tooconfigure autoscale.</span></span>

### <a name="get-connection-info"></a><span data-ttu-id="57c22-171">Pobierz informacje o połączeniu</span><span class="sxs-lookup"><span data-stu-id="57c22-171">Get connection info</span></span>
<span data-ttu-id="57c22-172">informacje o połączeniu tooobtain około hello w Twojej zestawy skalowania maszyn wirtualnych, użyj [az vmss listy--połączenia — informacje o wystąpieniu](/cli/azure/vmss#list-instance-connection-info).</span><span class="sxs-lookup"><span data-stu-id="57c22-172">tooobtain connection information about hello VMs in your scale sets, use [az vmss list-instance-connection-info](/cli/azure/vmss#list-instance-connection-info).</span></span> <span data-ttu-id="57c22-173">To polecenie wyświetla hello publicznego adresu IP i portu dla każdej maszyny Wirtualnej, która pozwala tooconnect przy użyciu protokołu SSH:</span><span class="sxs-lookup"><span data-stu-id="57c22-173">This command outputs hello public IP address and port for each VM that allows you tooconnect with SSH:</span></span>

```azurecli-interactive 
az vmss list-instance-connection-info \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet
```


## <a name="use-data-disks-with-scale-sets"></a><span data-ttu-id="57c22-174">Dyski danych za pomocą zestawów skali</span><span class="sxs-lookup"><span data-stu-id="57c22-174">Use data disks with scale sets</span></span>
<span data-ttu-id="57c22-175">Można tworzyć i dysków z danymi za pomocą zestawów skali.</span><span class="sxs-lookup"><span data-stu-id="57c22-175">You can create and use data disks with scale sets.</span></span> <span data-ttu-id="57c22-176">W poprzednich samouczek przedstawiono sposób zbyt[dysków Azure zarządzanie](tutorial-manage-disks.md) najlepszych rozwiązań i ulepszenia wydajności umożliwiające tworzenie aplikacji na dysków z danymi, a nie na dysku systemu operacyjnego hello tekst hello opisanych.</span><span class="sxs-lookup"><span data-stu-id="57c22-176">In a previous tutorial, you learned how too[Manage Azure disks](tutorial-manage-disks.md) that outlines hello best practices and performance improvements for building apps on data disks rather than hello OS disk.</span></span>

### <a name="create-scale-set-with-data-disks"></a><span data-ttu-id="57c22-177">Utwórz zestaw skali z dysków z danymi</span><span class="sxs-lookup"><span data-stu-id="57c22-177">Create scale set with data disks</span></span>
<span data-ttu-id="57c22-178">toocreate skali ustawić i dołączyć dysków z danymi, Dodaj hello `--data-disk-sizes-gb` toohello parametru [az vmss utworzyć](/cli/azure/vmss#create) polecenia.</span><span class="sxs-lookup"><span data-stu-id="57c22-178">toocreate a scale set and attach data disks, add hello `--data-disk-sizes-gb` parameter toohello [az vmss create](/cli/azure/vmss#create) command.</span></span> <span data-ttu-id="57c22-179">Witaj poniższy przykład tworzy zestaw o skali *50*wystąpienia tooeach dołączone dyski danych Gb:</span><span class="sxs-lookup"><span data-stu-id="57c22-179">hello following example creates a scale set with *50*Gb data disks attached tooeach instance:</span></span>

```azurecli-interactive 
az vmss create \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSetDisks \
    --image UbuntuLTS \
    --upgrade-policy-mode automatic \
    --custom-data cloud-init.txt \
    --admin-username azureuser \
    --generate-ssh-keys \
    --data-disk-sizes-gb 50
```

<span data-ttu-id="57c22-180">Usunięcie wystąpienia z zestawu skalowania żadnych dysków dołączonych danych są również usuwane.</span><span class="sxs-lookup"><span data-stu-id="57c22-180">When instances are removed from a scale set, any attached data disks are also removed.</span></span>

### <a name="add-data-disks"></a><span data-ttu-id="57c22-181">Dodawanie dysków z danymi</span><span class="sxs-lookup"><span data-stu-id="57c22-181">Add data disks</span></span>
<span data-ttu-id="57c22-182">Ustaw tooinstances dysku danych, w Twojej skali tooadd, użyj [dołączyć dysku vmss az](/cli/azure/vmss/disk#attach).</span><span class="sxs-lookup"><span data-stu-id="57c22-182">tooadd a data disk tooinstances in your scale set, use [az vmss disk attach](/cli/azure/vmss/disk#attach).</span></span> <span data-ttu-id="57c22-183">Witaj poniższy przykład umożliwia dodanie *50*wystąpienia tooeach dysku Gb:</span><span class="sxs-lookup"><span data-stu-id="57c22-183">hello following example adds a *50*Gb disk tooeach instance:</span></span>

```azurecli-interactive 
az vmss disk attach \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet \
    --size-gb 50 \
    --lun 2
```

### <a name="detach-data-disks"></a><span data-ttu-id="57c22-184">Odłączanie dysku z danymi</span><span class="sxs-lookup"><span data-stu-id="57c22-184">Detach data disks</span></span>
<span data-ttu-id="57c22-185">Ustaw tooinstances dysku danych, w Twojej skali tooremove, użyj [odłączyć dysku vmss az](/cli/azure/vmss/disk#detach).</span><span class="sxs-lookup"><span data-stu-id="57c22-185">tooremove a data disk tooinstances in your scale set, use [az vmss disk detach](/cli/azure/vmss/disk#detach).</span></span> <span data-ttu-id="57c22-186">Witaj poniższy przykład umożliwia usunięcie hello dysk z danymi o numerze LUN *2* z każde wystąpienie:</span><span class="sxs-lookup"><span data-stu-id="57c22-186">hello following example removes hello data disk at LUN *2* from each instance:</span></span>

```azurecli-interactive 
az vmss disk detach \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet \
    --lun 2
```


## <a name="next-steps"></a><span data-ttu-id="57c22-187">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="57c22-187">Next steps</span></span>
<span data-ttu-id="57c22-188">W tym samouczku utworzony zestaw skali maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="57c22-188">In this tutorial, you created a virtual machine scale set.</span></span> <span data-ttu-id="57c22-189">W tym samouczku omówiono:</span><span class="sxs-lookup"><span data-stu-id="57c22-189">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="57c22-190">Użyj toocreate init chmury tooscale aplikacji</span><span class="sxs-lookup"><span data-stu-id="57c22-190">Use cloud-init toocreate an app tooscale</span></span>
> * <span data-ttu-id="57c22-191">Utwórz zestaw skali maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="57c22-191">Create a virtual machine scale set</span></span>
> * <span data-ttu-id="57c22-192">Zwiększanie lub zmniejszanie hello liczbę wystąpień w zestawie skalowania</span><span class="sxs-lookup"><span data-stu-id="57c22-192">Increase or decrease hello number of instances in a scale set</span></span>
> * <span data-ttu-id="57c22-193">Wyświetl informacje o połączeniu dla wystąpień zestawu skali</span><span class="sxs-lookup"><span data-stu-id="57c22-193">View connection info for scale set instances</span></span>
> * <span data-ttu-id="57c22-194">Dysków danych w zestawie skalowania</span><span class="sxs-lookup"><span data-stu-id="57c22-194">Use data disks in a scale set</span></span>

<span data-ttu-id="57c22-195">Więcej informacji na temat pojęć dla maszyn wirtualnych równoważenia obciążenia poprawić toohello dalej toolearn samouczka.</span><span class="sxs-lookup"><span data-stu-id="57c22-195">Advance toohello next tutorial toolearn more about load balancing concepts for virtual machines.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="57c22-196">Równoważyć obciążenie maszyn wirtualnych</span><span class="sxs-lookup"><span data-stu-id="57c22-196">Load balance virtual machines</span></span>](tutorial-load-balancer.md)