## <a name="create-a-resource-group"></a><span data-ttu-id="009c3-101">Tworzenie grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="009c3-101">Create a resource group</span></span>

<span data-ttu-id="009c3-102">Utwórz grupę zasobów o hello [Tworzenie grupy az](/cli/azure/group#create) polecenia.</span><span class="sxs-lookup"><span data-stu-id="009c3-102">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="009c3-103">Grupa zasobów platformy Azure to logiczny kontener przeznaczony do wdrażania zasobów platformy Azure i zarządzania nimi.</span><span class="sxs-lookup"><span data-stu-id="009c3-103">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="009c3-104">Witaj poniższy przykład tworzy grupę zasobów o nazwie *myResourceGroup* w hello *eastus* lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="009c3-104">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location.</span></span>

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```

## <a name="create-a-virtual-machine"></a><span data-ttu-id="009c3-105">Tworzenie maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="009c3-105">Create a virtual machine</span></span>

<span data-ttu-id="009c3-106">Utwórz maszynę Wirtualną z hello [tworzenia maszyny wirtualnej az](/cli/azure/vm#create) polecenia.</span><span class="sxs-lookup"><span data-stu-id="009c3-106">Create a VM with hello [az vm create](/cli/azure/vm#create) command.</span></span> 

<span data-ttu-id="009c3-107">Witaj poniższy przykład tworzy Maszynę wirtualną o nazwie *myVM* i tworzy kluczy SSH, jeśli nie już istnieją w domyślnej lokalizacji klucza.</span><span class="sxs-lookup"><span data-stu-id="009c3-107">hello following example creates a VM named *myVM* and creates SSH keys if they do not already exist in a default key location.</span></span> <span data-ttu-id="009c3-108">toouse określonego zestawu kluczy, należy użyć hello `--ssh-key-value` opcji.</span><span class="sxs-lookup"><span data-stu-id="009c3-108">toouse a specific set of keys, use hello `--ssh-key-value` option.</span></span>  

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys
```

<span data-ttu-id="009c3-109">Podczas tworzenia maszyny Wirtualnej hello hello Azure CLI pokazuje informacje toohello podobnie poniższy przykład.</span><span class="sxs-lookup"><span data-stu-id="009c3-109">When hello VM has been created, hello Azure CLI shows information similar toohello following example.</span></span> <span data-ttu-id="009c3-110">Zwróć uwagę na powitania `publicIpAddress`.</span><span class="sxs-lookup"><span data-stu-id="009c3-110">Take note of hello `publicIpAddress`.</span></span> <span data-ttu-id="009c3-111">Ten adres jest używany tooaccess hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="009c3-111">This address is used tooaccess hello VM.</span></span>

```azurecli-interactive 
{
  "fqdns": "",
  "id": "/subscriptions/<subscription ID>/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM",
  "location": "eastus",
  "macAddress": "00-0D-3A-23-9A-49",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "40.68.254.142",
  "resourceGroup": "myResourceGroup"
}
```



## <a name="open-port-80-for-web-traffic"></a><span data-ttu-id="009c3-112">Otwieranie portu 80 na potrzeby ruchu w sieci Web</span><span class="sxs-lookup"><span data-stu-id="009c3-112">Open port 80 for web traffic</span></span> 

<span data-ttu-id="009c3-113">Domyślnie tylko połączeń SSH mają dostęp do maszyn wirtualnych systemu Linux wdrożonych na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="009c3-113">By default, only SSH connections are allowed into Linux VMs deployed in Azure.</span></span> <span data-ttu-id="009c3-114">Ponieważ ta maszyna wirtualna będzie toobe serwera sieci web, wystarczy tooopen port 80 hello internet.</span><span class="sxs-lookup"><span data-stu-id="009c3-114">Because this VM is going toobe a web server, you need tooopen port 80 from hello internet.</span></span> <span data-ttu-id="009c3-115">Użyj hello [port Otwórz az maszyny wirtualnej](/cli/azure/vm#open-port) polecenia tooopen hello żądany port.</span><span class="sxs-lookup"><span data-stu-id="009c3-115">Use hello [az vm open-port](/cli/azure/vm#open-port) command tooopen hello desired port.</span></span>  
 
```azurecli-interactive 
az vm open-port --port 80 --resource-group myResourceGroup --name myVM
```
## <a name="ssh-into-your-vm"></a><span data-ttu-id="009c3-116">Łączenie z maszyną wirtualną za pośrednictwem protokołu SSH</span><span class="sxs-lookup"><span data-stu-id="009c3-116">SSH into your VM</span></span>


<span data-ttu-id="009c3-117">Jeśli nie znasz już hello publicznego adresu IP maszyny Wirtualnej, uruchom hello [az sieci ip publicznego listy](/cli/azure/network/public-ip#list) polecenia:</span><span class="sxs-lookup"><span data-stu-id="009c3-117">If you don't already know hello public IP address of your VM, run hello [az network public-ip list](/cli/azure/network/public-ip#list) command:</span></span>


```azurecli-interactive
az network public-ip list --resource-group myResourceGroup --query [].ipAddress
```

<span data-ttu-id="009c3-118">Użyj hello następujące polecenie toocreate jako sesji SSH z maszyną wirtualną hello.</span><span class="sxs-lookup"><span data-stu-id="009c3-118">Use hello following command toocreate an SSH session with hello virtual machine.</span></span> <span data-ttu-id="009c3-119">Zastąp hello poprawne publiczny adres IP maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="009c3-119">Substitute hello correct public IP address of your virtual machine.</span></span> <span data-ttu-id="009c3-120">W tym przykładzie adres IP hello jest *40.68.254.142*.</span><span class="sxs-lookup"><span data-stu-id="009c3-120">In this example, hello IP address is *40.68.254.142*.</span></span>

```bash
ssh azureuser@40.68.254.142
```

