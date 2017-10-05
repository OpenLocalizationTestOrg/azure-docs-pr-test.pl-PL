---
title: "Utwórz zestawy skalowania maszyny wirtualnej dla systemu Linux na platformie Azure | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 2b8d519e11f70eda164bd8f6e131a3989f242ab0
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-virtual-machine-scale-set-and-deploy-a-highly-available-app-on-linux"></a><span data-ttu-id="e675f-103">Tworzenie zestawu skali maszyny wirtualnej i wdrażanie aplikacji wysokiej dostępności w systemie Linux</span><span class="sxs-lookup"><span data-stu-id="e675f-103">Create a Virtual Machine Scale Set and deploy a highly available app on Linux</span></span>
<span data-ttu-id="e675f-104">Zestaw skali maszyny wirtualnej umożliwia wdrażanie i zarządzanie nimi zestaw identyczne, automatyczne skalowanie maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="e675f-104">A virtual machine scale set allows you to deploy and manage a set of identical, auto-scaling virtual machines.</span></span> <span data-ttu-id="e675f-105">Można ręcznie skalować liczbę maszyn wirtualnych w zestawie skalowania lub definiowania reguł do skalowania automatycznego na podstawie użycia procesora CPU, pamięci żądanie lub ruchu sieciowego.</span><span class="sxs-lookup"><span data-stu-id="e675f-105">You can scale the number of VMs in the scale set manually, or define rules to autoscale based on CPU usage, memory demand, or network traffic.</span></span> <span data-ttu-id="e675f-106">W tym samouczku możesz wdrożyć skali maszyny wirtualnej w usłudze Azure.</span><span class="sxs-lookup"><span data-stu-id="e675f-106">In this tutorial, you deploy a virtual machine scale set in Azure.</span></span> <span data-ttu-id="e675f-107">Omawiane kwestie:</span><span class="sxs-lookup"><span data-stu-id="e675f-107">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="e675f-108">Umożliwia tworzenie aplikacji do skalowania init chmury</span><span class="sxs-lookup"><span data-stu-id="e675f-108">Use cloud-init to create an app to scale</span></span>
> * <span data-ttu-id="e675f-109">Utwórz zestaw skali maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="e675f-109">Create a virtual machine scale set</span></span>
> * <span data-ttu-id="e675f-110">Zwiększ lub Zmniejsz liczbę wystąpień w zestawie skalowania</span><span class="sxs-lookup"><span data-stu-id="e675f-110">Increase or decrease the number of instances in a scale set</span></span>
> * <span data-ttu-id="e675f-111">Wyświetl informacje o połączeniu dla wystąpień zestawu skali</span><span class="sxs-lookup"><span data-stu-id="e675f-111">View connection info for scale set instances</span></span>
> * <span data-ttu-id="e675f-112">Dysków danych w zestawie skalowania</span><span class="sxs-lookup"><span data-stu-id="e675f-112">Use data disks in a scale set</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="e675f-113">Jeśli wybierzesz do zainstalowania i używania interfejsu wiersza polecenia lokalnie, w tym samouczku wymaga używasz interfejsu wiersza polecenia Azure w wersji 2.0.4 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="e675f-113">If you choose to install and use the CLI locally, this tutorial requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="e675f-114">Uruchom polecenie `az --version`, aby dowiedzieć się, jaka wersja jest używana.</span><span class="sxs-lookup"><span data-stu-id="e675f-114">Run `az --version` to find the version.</span></span> <span data-ttu-id="e675f-115">Jeśli konieczna będzie instalacja lub uaktualnienie, zobacz [Instalowanie interfejsu wiersza polecenia platformy Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="e675f-115">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="scale-set-overview"></a><span data-ttu-id="e675f-116">Omówienie zestawu skali</span><span class="sxs-lookup"><span data-stu-id="e675f-116">Scale Set overview</span></span>
<span data-ttu-id="e675f-117">Zestaw skali maszyny wirtualnej umożliwia wdrażanie i zarządzanie nimi zestaw identyczne, automatyczne skalowanie maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="e675f-117">A virtual machine scale set allows you to deploy and manage a set of identical, auto-scaling virtual machines.</span></span> <span data-ttu-id="e675f-118">Zestawy skalowania, użyj tego samego składników jako poznanie w poprzednim w samouczku [tworzyć maszyny wirtualne o wysokiej dostępności](tutorial-availability-sets.md).</span><span class="sxs-lookup"><span data-stu-id="e675f-118">Scale sets use the same components as you learned about in the previous tutorial to [Create highly available VMs](tutorial-availability-sets.md).</span></span> <span data-ttu-id="e675f-119">Maszyny wirtualne w zestawie skalowania są tworzone w dostępności ustaw i rozpowszechniane w domenach awarii i aktualizacji logiki.</span><span class="sxs-lookup"><span data-stu-id="e675f-119">VMs in a scale set are created in an availability set and distributed across logic fault and update domains.</span></span>

<span data-ttu-id="e675f-120">Maszyny wirtualne są tworzone zgodnie z potrzebami w zestawie skalowania.</span><span class="sxs-lookup"><span data-stu-id="e675f-120">VMs are created as needed in a scale set.</span></span> <span data-ttu-id="e675f-121">Należy zdefiniować regułę automatycznego skalowania do kontrolowania sposobu i czasu maszyny wirtualne są dodawane lub usuwane z zestawu skalowania.</span><span class="sxs-lookup"><span data-stu-id="e675f-121">You define autoscale rules to control how and when VMs are added or removed from the scale set.</span></span> <span data-ttu-id="e675f-122">Te reguły może wyzwolić na podstawie metryk, takich jak obciążenie procesora CPU, pamięć lub ruchu sieciowego.</span><span class="sxs-lookup"><span data-stu-id="e675f-122">These rules can trigger based on metrics such as CPU load, memory usage, or network traffic.</span></span>

<span data-ttu-id="e675f-123">Skala ustawia obsługi maksymalnie 1000 maszyn wirtualnych, korzystając z obrazu platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="e675f-123">Scale sets support up to 1,000 VMs when you use an Azure platform image.</span></span> <span data-ttu-id="e675f-124">W przypadku obciążeń produkcyjnych warto [utworzyć niestandardowy obraz maszyny Wirtualnej](tutorial-custom-images.md).</span><span class="sxs-lookup"><span data-stu-id="e675f-124">For production workloads, you may wish to [Create a custom VM image](tutorial-custom-images.md).</span></span> <span data-ttu-id="e675f-125">Możesz utworzyć maksymalnie 100 maszyn wirtualnych w skali ustawić przy użyciu obrazu niestandardowego.</span><span class="sxs-lookup"><span data-stu-id="e675f-125">You can create up to 100 VMs in a scale set when using a custom image.</span></span>


## <a name="create-an-app-to-scale"></a><span data-ttu-id="e675f-126">Utwórz aplikację do skalowania</span><span class="sxs-lookup"><span data-stu-id="e675f-126">Create an app to scale</span></span>
<span data-ttu-id="e675f-127">W środowisku produkcyjnym, warto [utworzyć niestandardowy obraz maszyny Wirtualnej](tutorial-custom-images.md) zawierającą aplikacji zainstalowane i skonfigurowane.</span><span class="sxs-lookup"><span data-stu-id="e675f-127">For production use, you may wish to [Create a custom VM image](tutorial-custom-images.md) that includes your application installed and configured.</span></span> <span data-ttu-id="e675f-128">W tym samouczku umożliwia dostosowywanie maszyn wirtualnych po pierwszym uruchomieniu komputera, aby szybko wyświetlić zestaw akcji skalowania.</span><span class="sxs-lookup"><span data-stu-id="e675f-128">For this tutorial, lets customize the VMs on first boot to quickly see a scale set in action.</span></span>

<span data-ttu-id="e675f-129">W poprzednich samouczka przedstawiono [sposobu dostosowywania maszyny wirtualnej systemu Linux, po pierwszym uruchomieniu komputera](tutorial-automate-vm-deployment.md) z inicjowaniem chmury.</span><span class="sxs-lookup"><span data-stu-id="e675f-129">In a previous tutorial, you learned [How to customize a Linux virtual machine on first boot](tutorial-automate-vm-deployment.md) with cloud-init.</span></span> <span data-ttu-id="e675f-130">Można użyć tego samego pliku konfiguracji chmury init NGINX zainstalować i uruchomić prostej aplikacji Node.js "Hello World".</span><span class="sxs-lookup"><span data-stu-id="e675f-130">You can use the same cloud-init configuration file to install NGINX and run a simple 'Hello World' Node.js app.</span></span> 

<span data-ttu-id="e675f-131">W bieżącym powłoki, Utwórz plik o nazwie *init.txt chmury* i wklej następującą konfigurację.</span><span class="sxs-lookup"><span data-stu-id="e675f-131">In your current shell, create a file named *cloud-init.txt* and paste the following configuration.</span></span> <span data-ttu-id="e675f-132">Na przykład utworzyć plik, w powłoce chmury nie na komputerze lokalnym.</span><span class="sxs-lookup"><span data-stu-id="e675f-132">For example, create the file in the Cloud Shell not on your local machine.</span></span> <span data-ttu-id="e675f-133">Wprowadź `sensible-editor cloud-init.txt` do tworzenia pliku i wyświetlić listę dostępnych edytory.</span><span class="sxs-lookup"><span data-stu-id="e675f-133">Enter `sensible-editor cloud-init.txt` to create the file and see a list of available editors.</span></span> <span data-ttu-id="e675f-134">Upewnij się, że poprawnie skopiować pliku całego init chmury szczególnie pierwszy wiersz:</span><span class="sxs-lookup"><span data-stu-id="e675f-134">Make sure that the whole cloud-init file is copied correctly, especially the first line:</span></span>

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


## <a name="create-a-scale-set"></a><span data-ttu-id="e675f-135">Utwórz zestaw skali</span><span class="sxs-lookup"><span data-stu-id="e675f-135">Create a scale set</span></span>
<span data-ttu-id="e675f-136">Przed utworzeniem zestaw skali, Utwórz grupę zasobów o [Tworzenie grupy az](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="e675f-136">Before you can create a scale set, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="e675f-137">Poniższy przykład tworzy grupę zasobów o nazwie *myResourceGroupScaleSet* w *eastus* lokalizacji:</span><span class="sxs-lookup"><span data-stu-id="e675f-137">The following example creates a resource group named *myResourceGroupScaleSet* in the *eastus* location:</span></span>

```azurecli-interactive 
az group create --name myResourceGroupScaleSet --location eastus
```

<span data-ttu-id="e675f-138">Teraz Utwórz zestaw o skali maszyny wirtualnej [az vmss utworzyć](/cli/azure/vmss#create).</span><span class="sxs-lookup"><span data-stu-id="e675f-138">Now create a virtual machine scale set with [az vmss create](/cli/azure/vmss#create).</span></span> <span data-ttu-id="e675f-139">Poniższy przykład tworzy zestaw o nazwie skalowania *myScaleSet*, używa pliku init chmury do dostosowywania maszyny Wirtualnej i generuje klucze SSH, jeśli nie istnieją:</span><span class="sxs-lookup"><span data-stu-id="e675f-139">The following example creates a scale set named *myScaleSet*, uses the cloud-init file to customize the VM, and generates SSH keys if they do not exist:</span></span>

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

<span data-ttu-id="e675f-140">Trwa kilka minut, aby utworzyć i skonfigurować zasoby zestaw skali i maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="e675f-140">It takes a few minutes to create and configure all the scale set resources and VMs.</span></span> <span data-ttu-id="e675f-141">Istnieją zadania w tle, które nadal działać po interfejsu wiersza polecenia Azure powrót do wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="e675f-141">There are background tasks that continue to run after the Azure CLI returns you to the prompt.</span></span> <span data-ttu-id="e675f-142">Może to być inny kilka minut, w celu uzyskania dostępu do aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e675f-142">It may be another couple of minutes before you can access the app.</span></span>


## <a name="allow-web-traffic"></a><span data-ttu-id="e675f-143">Zezwalaj na ruch w sieci web</span><span class="sxs-lookup"><span data-stu-id="e675f-143">Allow web traffic</span></span>
<span data-ttu-id="e675f-144">Moduł równoważenia obciążenia został utworzony automatycznie jako część zestawu skali maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="e675f-144">A load balancer was created automatically as part of the virtual machine scale set.</span></span> <span data-ttu-id="e675f-145">Moduł równoważenia obciążenia dystrybuuje ruch zestawu zdefiniowanego maszyn wirtualnych przy użyciu reguły modułu równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="e675f-145">The load balancer distributes traffic across a set of defined VMs using load balancer rules.</span></span> <span data-ttu-id="e675f-146">Dowiedz się więcej o pojęcia dotyczące usługi równoważenia obciążenia i konfiguracji w następnym samouczku [jak równoważyć obciążenie maszyn wirtualnych na platformie Azure](tutorial-load-balancer.md).</span><span class="sxs-lookup"><span data-stu-id="e675f-146">You can learn more about load balancer concepts and configuration in the next tutorial, [How to load balance virtual machines in Azure](tutorial-load-balancer.md).</span></span>

<span data-ttu-id="e675f-147">Aby zezwolić na ruch do aplikacji sieci web, należy utworzyć regułę z [utworzyć regułę równoważeniem obciążenia sieciowego az](/cli/azure/network/lb/rule#create).</span><span class="sxs-lookup"><span data-stu-id="e675f-147">To allow traffic to reach the web app, create a rule with [az network lb rule create](/cli/azure/network/lb/rule#create).</span></span> <span data-ttu-id="e675f-148">Poniższy przykład tworzy reguły o nazwie *myLoadBalancerRuleWeb*:</span><span class="sxs-lookup"><span data-stu-id="e675f-148">The following example creates a rule named *myLoadBalancerRuleWeb*:</span></span>

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

## <a name="test-your-app"></a><span data-ttu-id="e675f-149">Testowanie aplikacji</span><span class="sxs-lookup"><span data-stu-id="e675f-149">Test your app</span></span>
<span data-ttu-id="e675f-150">Aby wyświetlić aplikację Node.js w sieci web, należy uzyskać publicznego adresu IP z usługi równoważenia obciążenia z [az sieci ip publicznego Pokaż](/cli/azure/network/public-ip#show).</span><span class="sxs-lookup"><span data-stu-id="e675f-150">To see your Node.js app on the web, obtain the public IP address of your load balancer with [az network public-ip show](/cli/azure/network/public-ip#show).</span></span> <span data-ttu-id="e675f-151">Poniższy przykład uzyskuje adres IP dla *myScaleSetLBPublicIP* utworzona w ramach zestawu skali:</span><span class="sxs-lookup"><span data-stu-id="e675f-151">The following example obtains the IP address for *myScaleSetLBPublicIP* created as part of the scale set:</span></span>

```azurecli-interactive 
az network public-ip show \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSetLBPublicIP \
    --query [ipAddress] \
    --output tsv
```

<span data-ttu-id="e675f-152">Wprowadź publicznego adresu IP w przeglądarce sieci web.</span><span class="sxs-lookup"><span data-stu-id="e675f-152">Enter the public IP address in to a web browser.</span></span> <span data-ttu-id="e675f-153">Aplikacja jest wyświetlana, łącznie z nazwą hosta maszyny Wirtualnej, ruch do dystrybucji modułu równoważenia obciążenia:</span><span class="sxs-lookup"><span data-stu-id="e675f-153">The app is displayed, including the hostname of the VM that the load balancer distributed traffic to:</span></span>

![Uruchomionej aplikacji Node.js](./media/tutorial-create-vmss/running-nodejs-app.png)

<span data-ttu-id="e675f-155">Aby wyświetlić zestaw akcji skalowania, możesz można życie odświeżania przeglądarki sieci web, aby zobaczyć Dystrybuuj ruch na wszystkich maszynach wirtualnych z tą aplikacją usługi równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="e675f-155">To see the scale set in action, you can force-refresh your web browser to see the load balancer distribute traffic across all the VMs running your app.</span></span>


## <a name="management-tasks"></a><span data-ttu-id="e675f-156">Zadania zarządzania</span><span class="sxs-lookup"><span data-stu-id="e675f-156">Management tasks</span></span>
<span data-ttu-id="e675f-157">W całym cyklu życia zestawu skalowania konieczne może być Uruchom jedno lub więcej zadań zarządzania.</span><span class="sxs-lookup"><span data-stu-id="e675f-157">Throughout the lifecycle of the scale set, you may need to run one or more management tasks.</span></span> <span data-ttu-id="e675f-158">Ponadto można tworzenia skryptów automatyzujących różnych zadań cyklu życia.</span><span class="sxs-lookup"><span data-stu-id="e675f-158">Additionally, you may want to create scripts that automate various lifecycle-tasks.</span></span> <span data-ttu-id="e675f-159">Azure CLI 2.0 umożliwia szybkie do wykonywania tych zadań.</span><span class="sxs-lookup"><span data-stu-id="e675f-159">The Azure CLI 2.0 provides a quick way to do those tasks.</span></span> <span data-ttu-id="e675f-160">Poniżej przedstawiono kilka typowych zadań.</span><span class="sxs-lookup"><span data-stu-id="e675f-160">Here are a few common tasks.</span></span>

### <a name="view-vms-in-a-scale-set"></a><span data-ttu-id="e675f-161">Maszyny wirtualne widoku w zestawie skalowania</span><span class="sxs-lookup"><span data-stu-id="e675f-161">View VMs in a scale set</span></span>
<span data-ttu-id="e675f-162">Aby wyświetlić listę uruchomionych w zestawie skalowania maszyn wirtualnych, użyj [wystąpienia listy az vmss](/cli/azure/vmss#list-instances) w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="e675f-162">To view a list of VMs running in your scale set, use [az vmss list-instances](/cli/azure/vmss#list-instances) as follows:</span></span>

```azurecli-interactive 
az vmss list-instances \
  --resource-group myResourceGroupScaleSet \
  --name myScaleSet \
  --output table
```

<span data-ttu-id="e675f-163">Dane wyjściowe są podobne do poniższego przykładu:</span><span class="sxs-lookup"><span data-stu-id="e675f-163">The output is similar to the following example:</span></span>

```azurecli-interactive 
  InstanceId  LatestModelApplied    Location    Name          ProvisioningState    ResourceGroup            VmId
------------  --------------------  ----------  ------------  -------------------  -----------------------  ------------------------------------
           1  True                  eastus      myScaleSet_1  Succeeded            MYRESOURCEGROUPSCALESET  c72ddc34-6c41-4a53-b89e-dd24f27b30ab
           3  True                  eastus      myScaleSet_3  Succeeded            MYRESOURCEGROUPSCALESET  44266022-65c3-49c5-92dd-88ffa64f95da
```


### <a name="increase-or-decrease-vm-instances"></a><span data-ttu-id="e675f-164">Zwiększanie lub zmniejszanie wystąpień maszyn wirtualnych</span><span class="sxs-lookup"><span data-stu-id="e675f-164">Increase or decrease VM instances</span></span>
<span data-ttu-id="e675f-165">Aby wyświetlić liczbę wystąpień aktualnie zainstalowana w zestawie skalowania, użyj [Pokaż vmss az](/cli/azure/vmss#show) i wykonywać zapytania na *sku.capacity*:</span><span class="sxs-lookup"><span data-stu-id="e675f-165">To see the number of instances you currently have in a scale set, use [az vmss show](/cli/azure/vmss#show) and query on *sku.capacity*:</span></span>

```azurecli-interactive 
az vmss show \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet \
    --query [sku.capacity] \
    --output table
```

<span data-ttu-id="e675f-166">Możesz ręcznie zwiększyć lub zmniejszyć liczbę maszyn wirtualnych w skali ustawiony za pomocą [skali vmss az](/cli/azure/vmss#scale).</span><span class="sxs-lookup"><span data-stu-id="e675f-166">You can then manually increase or decrease the number of virtual machines in the scale set with [az vmss scale](/cli/azure/vmss#scale).</span></span> <span data-ttu-id="e675f-167">Poniższy przykład ustawia liczbę maszyn wirtualnych w skali, z ustawioną *5*:</span><span class="sxs-lookup"><span data-stu-id="e675f-167">The following example sets the number of VMs in your scale set to *5*:</span></span>

```azurecli-interactive 
az vmss scale \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet \
    --new-capacity 5
```

<span data-ttu-id="e675f-168">Reguły automatycznego skalowania umożliwiają definiowanie sposobu skalowania w górę lub w dół liczbę maszyn wirtualnych w Twojej skali w odpowiedzi na żądanie, takie jak ruch w sieci i użycie procesora CPU.</span><span class="sxs-lookup"><span data-stu-id="e675f-168">Autoscale rules let you define how to scale up or down the number of VMs in your scale set in response to demand such as network traffic or CPU usage.</span></span> <span data-ttu-id="e675f-169">Obecnie te zasady nie można ustawić w 2.0 interfejsu wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="e675f-169">Currently, these rules cannot be set in Azure CLI 2.0.</span></span> <span data-ttu-id="e675f-170">Użyj [portalu Azure](https://portal.azure.com) skonfigurowanie automatycznego skalowania.</span><span class="sxs-lookup"><span data-stu-id="e675f-170">Use the [Azure portal](https://portal.azure.com) to configure autoscale.</span></span>

### <a name="get-connection-info"></a><span data-ttu-id="e675f-171">Pobierz informacje o połączeniu</span><span class="sxs-lookup"><span data-stu-id="e675f-171">Get connection info</span></span>
<span data-ttu-id="e675f-172">Aby uzyskać informacje o połączeniu o w Twojej zestawy skalowania maszyn wirtualnych, użyj [az vmss listy--połączenia — informacje o wystąpieniu](/cli/azure/vmss#list-instance-connection-info).</span><span class="sxs-lookup"><span data-stu-id="e675f-172">To obtain connection information about the VMs in your scale sets, use [az vmss list-instance-connection-info](/cli/azure/vmss#list-instance-connection-info).</span></span> <span data-ttu-id="e675f-173">To polecenie wyświetla publicznego adresu IP i portu dla każdej maszyny Wirtualnej, która umożliwia nawiązanie połączenia przy użyciu protokołu SSH:</span><span class="sxs-lookup"><span data-stu-id="e675f-173">This command outputs the public IP address and port for each VM that allows you to connect with SSH:</span></span>

```azurecli-interactive 
az vmss list-instance-connection-info \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet
```


## <a name="use-data-disks-with-scale-sets"></a><span data-ttu-id="e675f-174">Dyski danych za pomocą zestawów skali</span><span class="sxs-lookup"><span data-stu-id="e675f-174">Use data disks with scale sets</span></span>
<span data-ttu-id="e675f-175">Można tworzyć i dysków z danymi za pomocą zestawów skali.</span><span class="sxs-lookup"><span data-stu-id="e675f-175">You can create and use data disks with scale sets.</span></span> <span data-ttu-id="e675f-176">W poprzednich samouczka przedstawiono sposób [dysków Azure zarządzanie](tutorial-manage-disks.md) który przedstawiono najlepsze rozwiązania i ulepszenia wydajności umożliwiające tworzenie aplikacji dla dysków z danymi, a nie na dysku systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="e675f-176">In a previous tutorial, you learned how to [Manage Azure disks](tutorial-manage-disks.md) that outlines the best practices and performance improvements for building apps on data disks rather than the OS disk.</span></span>

### <a name="create-scale-set-with-data-disks"></a><span data-ttu-id="e675f-177">Utwórz zestaw skali z dysków z danymi</span><span class="sxs-lookup"><span data-stu-id="e675f-177">Create scale set with data disks</span></span>
<span data-ttu-id="e675f-178">Aby utworzyć zestaw skali i dołączyć dysk danych, należy dodać `--data-disk-sizes-gb` parametr [az vmss utworzyć](/cli/azure/vmss#create) polecenia.</span><span class="sxs-lookup"><span data-stu-id="e675f-178">To create a scale set and attach data disks, add the `--data-disk-sizes-gb` parameter to the [az vmss create](/cli/azure/vmss#create) command.</span></span> <span data-ttu-id="e675f-179">Poniższy przykład tworzy zestaw o skali *50*do niej dołączone dyski danych Gb na każde wystąpienie:</span><span class="sxs-lookup"><span data-stu-id="e675f-179">The following example creates a scale set with *50*Gb data disks attached to each instance:</span></span>

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

<span data-ttu-id="e675f-180">Usunięcie wystąpienia z zestawu skalowania żadnych dysków dołączonych danych są również usuwane.</span><span class="sxs-lookup"><span data-stu-id="e675f-180">When instances are removed from a scale set, any attached data disks are also removed.</span></span>

### <a name="add-data-disks"></a><span data-ttu-id="e675f-181">Dodawanie dysków z danymi</span><span class="sxs-lookup"><span data-stu-id="e675f-181">Add data disks</span></span>
<span data-ttu-id="e675f-182">Aby dodać dysk z danymi do wystąpień w zestawie skali, użyj [dołączyć dysku vmss az](/cli/azure/vmss/disk#attach).</span><span class="sxs-lookup"><span data-stu-id="e675f-182">To add a data disk to instances in your scale set, use [az vmss disk attach](/cli/azure/vmss/disk#attach).</span></span> <span data-ttu-id="e675f-183">W poniższym przykładzie dodano *50*dysk Gb na każde wystąpienie:</span><span class="sxs-lookup"><span data-stu-id="e675f-183">The following example adds a *50*Gb disk to each instance:</span></span>

```azurecli-interactive 
az vmss disk attach \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet \
    --size-gb 50 \
    --lun 2
```

### <a name="detach-data-disks"></a><span data-ttu-id="e675f-184">Odłączanie dysku z danymi</span><span class="sxs-lookup"><span data-stu-id="e675f-184">Detach data disks</span></span>
<span data-ttu-id="e675f-185">Aby usunąć dysk z danymi do wystąpień w zestawie skali, użyj [odłączyć dysku vmss az](/cli/azure/vmss/disk#detach).</span><span class="sxs-lookup"><span data-stu-id="e675f-185">To remove a data disk to instances in your scale set, use [az vmss disk detach](/cli/azure/vmss/disk#detach).</span></span> <span data-ttu-id="e675f-186">Poniższy przykład umożliwia usunięcie dysk z danymi o numerze LUN *2* z każde wystąpienie:</span><span class="sxs-lookup"><span data-stu-id="e675f-186">The following example removes the data disk at LUN *2* from each instance:</span></span>

```azurecli-interactive 
az vmss disk detach \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet \
    --lun 2
```


## <a name="next-steps"></a><span data-ttu-id="e675f-187">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e675f-187">Next steps</span></span>
<span data-ttu-id="e675f-188">W tym samouczku utworzony zestaw skali maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="e675f-188">In this tutorial, you created a virtual machine scale set.</span></span> <span data-ttu-id="e675f-189">Możesz przedstawiono sposób do:</span><span class="sxs-lookup"><span data-stu-id="e675f-189">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="e675f-190">Umożliwia tworzenie aplikacji do skalowania init chmury</span><span class="sxs-lookup"><span data-stu-id="e675f-190">Use cloud-init to create an app to scale</span></span>
> * <span data-ttu-id="e675f-191">Utwórz zestaw skali maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="e675f-191">Create a virtual machine scale set</span></span>
> * <span data-ttu-id="e675f-192">Zwiększ lub Zmniejsz liczbę wystąpień w zestawie skalowania</span><span class="sxs-lookup"><span data-stu-id="e675f-192">Increase or decrease the number of instances in a scale set</span></span>
> * <span data-ttu-id="e675f-193">Wyświetl informacje o połączeniu dla wystąpień zestawu skali</span><span class="sxs-lookup"><span data-stu-id="e675f-193">View connection info for scale set instances</span></span>
> * <span data-ttu-id="e675f-194">Dysków danych w zestawie skalowania</span><span class="sxs-lookup"><span data-stu-id="e675f-194">Use data disks in a scale set</span></span>

<span data-ttu-id="e675f-195">Przejdź do następnego samouczek, aby dowiedzieć się więcej na temat pojęć dla maszyn wirtualnych równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="e675f-195">Advance to the next tutorial to learn more about load balancing concepts for virtual machines.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="e675f-196">Równoważyć obciążenie maszyn wirtualnych</span><span class="sxs-lookup"><span data-stu-id="e675f-196">Load balance virtual machines</span></span>](tutorial-load-balancer.md)