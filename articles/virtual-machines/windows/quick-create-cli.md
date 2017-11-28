---
title: "Szybki Start - aaaAzure utworzyć CLI maszyny Wirtualnej z systemem Windows | Dokumentacja firmy Microsoft"
description: Dowiesz toocreate maszyn wirtualnych systemu Windows z hello wiersza polecenia platformy Azure.
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/11/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 029bdecec219b12b80b958ceeedda214f1b13149
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-windows-virtual-machine-with-hello-azure-cli"></a><span data-ttu-id="23bec-103">Utwórz maszynę wirtualną systemu Windows z hello wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="23bec-103">Create a Windows virtual machine with hello Azure CLI</span></span>

<span data-ttu-id="23bec-104">Hello wiersza polecenia platformy Azure jest używana toocreate i zarządzania zasobami Azure z wiersza polecenia hello lub w skryptach.</span><span class="sxs-lookup"><span data-stu-id="23bec-104">hello Azure CLI is used toocreate and manage Azure resources from hello command line or in scripts.</span></span> <span data-ttu-id="23bec-105">Szczegóły tego przewodnika przy użyciu hello Azure CLI toodeploy maszyny wirtualnej z systemem Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="23bec-105">This guide details using hello Azure CLI toodeploy a virtual machine running Windows Server 2016.</span></span> <span data-ttu-id="23bec-106">Po zakończeniu wdrażania nawiązanie połączenia toohello serwera i zainstaluj usługi IIS.</span><span class="sxs-lookup"><span data-stu-id="23bec-106">Once deployment is complete, we connect toohello server and install IIS.</span></span>

<span data-ttu-id="23bec-107">Jeśli nie masz subskrypcji platformy Azure, przed rozpoczęciem utwórz [bezpłatne konto](https://azure.microsoft.com/free/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="23bec-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="23bec-108">Wybierz tooinstall, użyj interfejsu wiersza polecenia hello lokalnie tego przewodnika Szybki Start wymaga działają hello Azure CLI w wersji 2.0.4 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="23bec-108">If you choose tooinstall and use hello CLI locally, this quickstart requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="23bec-109">Uruchom `az --version` toofind hello wersji.</span><span class="sxs-lookup"><span data-stu-id="23bec-109">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="23bec-110">Jeśli potrzebujesz tooinstall lub uaktualniania, zobacz [zainstalować Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="23bec-110">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 


## <a name="create-a-resource-group"></a><span data-ttu-id="23bec-111">Tworzenie grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="23bec-111">Create a resource group</span></span>

<span data-ttu-id="23bec-112">Utwórz grupę zasobów za pomocą polecenia [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="23bec-112">Create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="23bec-113">Grupa zasobów platformy Azure to logiczny kontener przeznaczony do wdrażania zasobów platformy Azure i zarządzania nimi.</span><span class="sxs-lookup"><span data-stu-id="23bec-113">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="23bec-114">Witaj poniższy przykład tworzy grupę zasobów o nazwie *myResourceGroup* w hello *eastus* lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="23bec-114">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location.</span></span>

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```

## <a name="create-virtual-machine"></a><span data-ttu-id="23bec-115">Tworzenie maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="23bec-115">Create virtual machine</span></span>

<span data-ttu-id="23bec-116">Utwórz maszynę wirtualną za pomocą polecenia [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="23bec-116">Create a VM with [az vm create](/cli/azure/vm#create).</span></span> 

<span data-ttu-id="23bec-117">Witaj poniższy przykład tworzy Maszynę wirtualną o nazwie *myVM*.</span><span class="sxs-lookup"><span data-stu-id="23bec-117">hello following example creates a VM named *myVM*.</span></span> <span data-ttu-id="23bec-118">W tym przykładzie użyto *azureuser* dla nazwy użytkownika administracyjnego i *myPassword12* jako hello hasła.</span><span class="sxs-lookup"><span data-stu-id="23bec-118">This example uses *azureuser* for an administrative user name and *myPassword12* as hello password.</span></span> <span data-ttu-id="23bec-119">Zaktualizować te wartości toosomething tooyour odpowiednie środowisko.</span><span class="sxs-lookup"><span data-stu-id="23bec-119">Update these values toosomething appropriate tooyour environment.</span></span> <span data-ttu-id="23bec-120">Te wartości są wymagane podczas tworzenia połączenia z maszyną wirtualną hello.</span><span class="sxs-lookup"><span data-stu-id="23bec-120">These values are needed when creating a connection with hello virtual machine.</span></span>

```azurecli-interactive 
az vm create --resource-group myResourceGroup --name myVM --image win2016datacenter --admin-username azureuser --admin-password myPassword12
```

<span data-ttu-id="23bec-121">Podczas tworzenia maszyny Wirtualnej hello hello Azure CLI pokazuje informacje toohello podobnie poniższy przykład.</span><span class="sxs-lookup"><span data-stu-id="23bec-121">When hello VM has been created, hello Azure CLI shows information similar toohello following example.</span></span> <span data-ttu-id="23bec-122">Zwróć uwagę na powitania `publicIpAaddress`.</span><span class="sxs-lookup"><span data-stu-id="23bec-122">Take note of hello `publicIpAaddress`.</span></span> <span data-ttu-id="23bec-123">Ten adres jest używany tooaccess hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="23bec-123">This address is used tooaccess hello VM.</span></span>

```azurecli-interactive 
{
  "fqdns": "",
  "id": "/subscriptions/d5b9d4b7-6fc1-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM",
  "location": "eastus",
  "macAddress": "00-0D-3A-23-9A-49",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "52.174.34.95",
  "resourceGroup": "myResourceGroup"
}
```

## <a name="open-port-80-for-web-traffic"></a><span data-ttu-id="23bec-124">Otwieranie portu 80 na potrzeby ruchu w sieci Web</span><span class="sxs-lookup"><span data-stu-id="23bec-124">Open port 80 for web traffic</span></span> 

<span data-ttu-id="23bec-125">Domyślnie w tooWindows maszyn wirtualnych wdrożonych w usłudze Azure są dozwolone tylko na połączenia RDP.</span><span class="sxs-lookup"><span data-stu-id="23bec-125">By default only RDP connections are allowed in tooWindows virtual machines deployed in Azure.</span></span> <span data-ttu-id="23bec-126">Jeśli ta maszyna wirtualna będzie toobe serwer sieci Web, należy tooopen port 80 hello Internet.</span><span class="sxs-lookup"><span data-stu-id="23bec-126">If this VM is going toobe a webserver, you need tooopen port 80 from hello Internet.</span></span> <span data-ttu-id="23bec-127">Użyj hello [port Otwórz az maszyny wirtualnej](/cli/azure/vm#open-port) polecenia tooopen hello żądany port.</span><span class="sxs-lookup"><span data-stu-id="23bec-127">Use hello [az vm open-port](/cli/azure/vm#open-port) command tooopen hello desired port.</span></span>  
 
 ```azurecli-interactive  
az vm open-port --port 80 --resource-group myResourceGroup --name myVM
```


## <a name="connect-toovirtual-machine"></a><span data-ttu-id="23bec-128">Podłącz maszynę toovirtual</span><span class="sxs-lookup"><span data-stu-id="23bec-128">Connect toovirtual machine</span></span>

<span data-ttu-id="23bec-129">Użyj hello następujące polecenie toocreate sesję pulpitu zdalnego z maszyną wirtualną hello.</span><span class="sxs-lookup"><span data-stu-id="23bec-129">Use hello following command toocreate a remote desktop session with hello virtual machine.</span></span> <span data-ttu-id="23bec-130">Zamień adres IP hello hello publiczny adres IP maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="23bec-130">Replace hello IP address with hello public IP address of your virtual machine.</span></span> <span data-ttu-id="23bec-131">Po wyświetleniu monitu wprowadź poświadczenia hello używane podczas tworzenia maszyny wirtualnej hello.</span><span class="sxs-lookup"><span data-stu-id="23bec-131">When prompted, enter hello credentials used when creating hello virtual machine.</span></span>

```bash 
mstsc /v:<Public IP Address>
```

## <a name="install-iis-using-powershell"></a><span data-ttu-id="23bec-132">Instalowanie usług IIS przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="23bec-132">Install IIS using PowerShell</span></span>

<span data-ttu-id="23bec-133">Teraz, gdy użytkownik zalogował się toohello maszyny Wirtualnej platformy Azure, można użyć pojedynczy wiersz tooinstall PowerShell usług IIS i włączyć ruch internetowy tooallow reguły zapory lokalnej hello.</span><span class="sxs-lookup"><span data-stu-id="23bec-133">Now that you have logged in toohello Azure VM, you can use a single line of PowerShell tooinstall IIS and enable hello local firewall rule tooallow web traffic.</span></span> <span data-ttu-id="23bec-134">Otwórz wiersz programu PowerShell i uruchom następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="23bec-134">Open a PowerShell prompt and run hello following command:</span></span>

```powershell
Install-WindowsFeature -name Web-Server -IncludeManagementTools
```

## <a name="view-hello-iis-welcome-page"></a><span data-ttu-id="23bec-135">Widok hello strona powitalna usług IIS</span><span class="sxs-lookup"><span data-stu-id="23bec-135">View hello IIS welcome page</span></span>

<span data-ttu-id="23bec-136">Zainstalowane usługi IIS i portu 80 obecnie otwarte na maszynie Wirtualnej z hello Internet można użyć przeglądarki sieci web na wybór tooview hello domyślne IIS strony powitalnej.</span><span class="sxs-lookup"><span data-stu-id="23bec-136">With IIS installed and port 80 now open on your VM from hello Internet, you can use a web browser of your choice tooview hello default IIS welcome page.</span></span> <span data-ttu-id="23bec-137">Należy się toouse hello publicznego adresu IP, który opisane powyżej toovisit hello domyślnej strony.</span><span class="sxs-lookup"><span data-stu-id="23bec-137">Be sure toouse hello public IP address you documented above toovisit hello default page.</span></span> 

![Domyślna witryna usług IIS](./media/quick-create-powershell/default-iis-website.png) 

## <a name="clean-up-resources"></a><span data-ttu-id="23bec-139">Oczyszczanie zasobów</span><span class="sxs-lookup"><span data-stu-id="23bec-139">Clean up resources</span></span>

<span data-ttu-id="23bec-140">Gdy nie są już potrzebne, można użyć hello [usunięcie grupy az](/cli/azure/group#delete) polecenia grupy zasobów hello tooremove, maszyny Wirtualnej i wszystkich powiązanych zasobów.</span><span class="sxs-lookup"><span data-stu-id="23bec-140">When no longer needed, you can use hello [az group delete](/cli/azure/group#delete) command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="23bec-141">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="23bec-141">Next steps</span></span>

<span data-ttu-id="23bec-142">W tym przewodniku Szybki start została wdrożona prosta maszyna wirtualna i reguła sieciowej grupy zabezpieczeń oraz zainstalowano serwer sieci Web.</span><span class="sxs-lookup"><span data-stu-id="23bec-142">In this quick start, you’ve deployed a simple virtual machine, a network security group rule, and installed a web server.</span></span> <span data-ttu-id="23bec-143">toolearn więcej informacji o maszynach wirtualnych platformy Azure, nadal samouczek toohello dla maszyn wirtualnych systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="23bec-143">toolearn more about Azure virtual machines, continue toohello tutorial for Windows VMs.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="23bec-144">Samouczki dla maszyny wirtualnej platformy Azure z systemem Windows</span><span class="sxs-lookup"><span data-stu-id="23bec-144">Azure Windows virtual machine tutorials</span></span>](./tutorial-manage-vm.md)
