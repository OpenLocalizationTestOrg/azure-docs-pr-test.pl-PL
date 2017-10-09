## <a name="overview"></a><span data-ttu-id="fa7be-101">Omówienie</span><span class="sxs-lookup"><span data-stu-id="fa7be-101">Overview</span></span>
<span data-ttu-id="fa7be-102">Podczas tworzenia nowej maszyny wirtualnej (VM) w grupie zasobów przez wdrożenie obrazu z [portalu Azure Marketplace](https://azure.microsoft.com/marketplace/), dysk systemu operacyjnego domyślny hello wynosi 127 GB.</span><span class="sxs-lookup"><span data-stu-id="fa7be-102">When you create a new virtual machine (VM) in a Resource Group by deploying an image from [Azure Marketplace](https://azure.microsoft.com/marketplace/), hello default OS drive is 127 GB.</span></span> <span data-ttu-id="fa7be-103">Mimo że jest możliwe tooadd danych dysków toohello maszyny Wirtualnej (jak wiele zależności hello SKU wybrano), a ponadto jest zalecane tooinstall aplikacji i obciążeń intensywnie korzystających z procesora CPU na tych dyskach uzupełnienie, często klienci muszą hello tooexpand systemu operacyjnego dysk toosupport niektórych scenariuszy, takich jak następujące:</span><span class="sxs-lookup"><span data-stu-id="fa7be-103">Even though it’s possible tooadd data disks toohello VM (how many depending upon hello SKU you’ve chosen) and moreover it’s recommended tooinstall applications and CPU intensive workloads on these addendum disks, oftentimes customers need tooexpand hello OS drive toosupport certain scenarios such as following:</span></span>

1. <span data-ttu-id="fa7be-104">Obsługa starszych aplikacji, które instalują składniki na dysku systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="fa7be-104">Support legacy applications that install components on OS drive.</span></span>
2. <span data-ttu-id="fa7be-105">Migrowanie fizycznego komputera lub maszyny wirtualnej ze środowiska lokalnego z większym dyskiem systemu operacyjnego.</span><span class="sxs-lookup"><span data-stu-id="fa7be-105">Migrate a physical PC or virtual machine from on-premises with a larger OS drive.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fa7be-106">Platforma Azure oferuje dwa różne modele wdrażania związane z tworzeniem zasobów i pracą z nimi: model wdrażania przy użyciu usługi Resource Manager i model klasyczny.</span><span class="sxs-lookup"><span data-stu-id="fa7be-106">Azure has two different deployment models for creating and working with resources: Resource Manager and Classic.</span></span> <span data-ttu-id="fa7be-107">W tym artykule omówiono przy użyciu hello modelu Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="fa7be-107">This article covers using hello Resource Manager model.</span></span> <span data-ttu-id="fa7be-108">Firma Microsoft zaleca, aby większości nowych wdrożeń korzystać hello modelu Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="fa7be-108">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>
> 
> 

## <a name="resize-hello-os-drive"></a><span data-ttu-id="fa7be-109">Zmień rozmiar dysku systemu operacyjnego hello</span><span class="sxs-lookup"><span data-stu-id="fa7be-109">Resize hello OS drive</span></span>
<span data-ttu-id="fa7be-110">W tym artykule możemy wykonywać zadania hello zmiany rozmiaru dysku hello systemu operacyjnego za pomocą modułów Menedżera zasobów systemu [programu Azure Powershell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="fa7be-110">In this article we’ll accomplish hello task of resizing hello OS drive using resource manager modules of [Azure Powershell](/powershell/azureps-cmdlets-docs).</span></span> <span data-ttu-id="fa7be-111">Otwórz okno programu Powershell lub programu Powershell ISE, na których w trybie administratora, a następnie wykonaj poniższe kroki hello:</span><span class="sxs-lookup"><span data-stu-id="fa7be-111">Open your Powershell ISE or Powershell window in administrative mode and follow hello steps below:</span></span>

1. <span data-ttu-id="fa7be-112">Logowanie tooyour Microsoft Azure konta w trybie zarządzania zasobów i wybrać subskrypcję w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="fa7be-112">Sign-in tooyour Microsoft Azure account in resource management mode and select your subscription as follows:</span></span>
   
   ```Powershell
   Login-AzureRmAccount
   Select-AzureRmSubscription –SubscriptionName 'my-subscription-name'
   ```
2. <span data-ttu-id="fa7be-113">Ustaw nazwę swojej grupy zasobów i nazwę maszyny wirtualnej w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="fa7be-113">Set your resource group name and VM name as follows:</span></span>
   
   ```Powershell
   $rgName = 'my-resource-group-name'
   $vmName = 'my-vm-name'
   ```
3. <span data-ttu-id="fa7be-114">Uzyskaj odwołanie tooyour maszyny Wirtualnej w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="fa7be-114">Obtain a reference tooyour VM as follows:</span></span>
   
   ```Powershell
   $vm = Get-AzureRmVM -ResourceGroupName $rgName -Name $vmName
   ```
4. <span data-ttu-id="fa7be-115">Zatrzymaj hello maszyny Wirtualnej przed zmianą rozmiaru dysku hello w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="fa7be-115">Stop hello VM before resizing hello disk as follows:</span></span>
   
    ```Powershell
    Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName
    ```
5. <span data-ttu-id="fa7be-116">I w tym miejscu możemy oczekiwania do momentu hello!</span><span class="sxs-lookup"><span data-stu-id="fa7be-116">And here comes hello moment we’ve been waiting for!</span></span> <span data-ttu-id="fa7be-117">Ustaw rozmiar hello wartości toohello żądanego dysku hello systemu operacyjnego i zaktualizować hello maszyny Wirtualnej w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="fa7be-117">Set hello size of hello OS disk toohello desired value and update hello VM as follows:</span></span>
   
   ```Powershell
   $vm.StorageProfile.OSDisk.DiskSizeGB = 1023
   Update-AzureRmVM -ResourceGroupName $rgName -VM $vm
   ```
   
   > [!WARNING]
   > <span data-ttu-id="fa7be-118">nowy rozmiar Hello powinna być większa niż rozmiar dysku istniejących hello.</span><span class="sxs-lookup"><span data-stu-id="fa7be-118">hello new size should be greater than hello existing disk size.</span></span> <span data-ttu-id="fa7be-119">Witaj maksymalna dozwolona jest 1023 GB.</span><span class="sxs-lookup"><span data-stu-id="fa7be-119">hello maximum allowed is 1023 GB.</span></span>
   > 
   > 
6. <span data-ttu-id="fa7be-120">Trwa aktualizowanie hello maszyny Wirtualnej może potrwać kilka sekund.</span><span class="sxs-lookup"><span data-stu-id="fa7be-120">Updating hello VM may take a few seconds.</span></span> <span data-ttu-id="fa7be-121">Po zakończeniu działania polecenia hello wykonywania, uruchom ponownie hello maszyny Wirtualnej w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="fa7be-121">Once hello command finishes executing, restart hello VM as follows:</span></span>
   
   ```Powershell
   Start-AzureRmVM -ResourceGroupName $rgName -Name $vmName
   ```

<span data-ttu-id="fa7be-122">To wszystko!</span><span class="sxs-lookup"><span data-stu-id="fa7be-122">And that’s it!</span></span> <span data-ttu-id="fa7be-123">Teraz RDP do hello maszynę Wirtualną, otwórz Zarządzanie komputerem (lub przystawki Zarządzanie dyskami) i rozwiń przy użyciu hello nowo przydzielone miejsce na dysku hello.</span><span class="sxs-lookup"><span data-stu-id="fa7be-123">Now RDP into hello VM, open Computer Management (or Disk Management) and expand hello drive using hello newly allocated space.</span></span>

## <a name="summary"></a><span data-ttu-id="fa7be-124">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="fa7be-124">Summary</span></span>
<span data-ttu-id="fa7be-125">W tym artykule użyliśmy usługi Azure Resource Manager moduły programu Powershell tooexpand hello dysku systemu operacyjnego maszyny wirtualne IaaS.</span><span class="sxs-lookup"><span data-stu-id="fa7be-125">In this article, we used Azure Resource Manager modules of Powershell tooexpand hello OS drive of an IaaS virtual machine.</span></span> <span data-ttu-id="fa7be-126">Przedstawionym poniżej jest hello wykonania skryptu użytkownikowi:</span><span class="sxs-lookup"><span data-stu-id="fa7be-126">Reproduced below is hello complete script for your reference:</span></span>

```Powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionName 'my-subscription-name'
$rgName = 'my-resource-group-name'
$vmName = 'my-vm-name'
$vm = Get-AzureRmVM -ResourceGroupName $rgName -Name $vmName
Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName
$vm.StorageProfile.OSDisk.DiskSizeGB = 1023
Update-AzureRmVM -ResourceGroupName $rgName -VM $vm
Start-AzureRmVM -ResourceGroupName $rgName -Name $vmName
```

## <a name="next-steps"></a><span data-ttu-id="fa7be-127">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="fa7be-127">Next Steps</span></span>
<span data-ttu-id="fa7be-128">Chociaż w tym artykule, firma Microsoft skupia się głównie na rozszerzania dysku systemu operacyjnego hello hello maszyny Wirtualnej, hello rozwinięte skrypt może także służyć do rozszerzania hello danych dysków dołączonych toohello maszyny Wirtualnej, zmieniając pojedynczy wiersz kodu.</span><span class="sxs-lookup"><span data-stu-id="fa7be-128">Though in this article, we focused primarily on expanding hello OS disk of hello VM, hello developed script may also be used for expanding hello data disks attached toohello VM by changing a single line of code.</span></span> <span data-ttu-id="fa7be-129">Na przykład tooexpand hello pierwsze dane na dysku toohello dołączona maszyna wirtualna, Zastąp hello ```OSDisk``` obiektu ```StorageProfile``` z ```DataDisks``` tablicy i użyć indeksu liczbowego tooobtain dysku odwołanie toofirst dołączonych danych, jak pokazano poniżej:</span><span class="sxs-lookup"><span data-stu-id="fa7be-129">For example, tooexpand hello first data disk attached toohello VM, replace hello ```OSDisk``` object of ```StorageProfile``` with ```DataDisks``` array and use a numeric index tooobtain a reference toofirst attached data disk, as shown below:</span></span>

```Powershell
$vm.StorageProfile.DataDisks[0].DiskSizeGB = 1023
```
<span data-ttu-id="fa7be-130">Podobnie można odwoływać się inne toohello dołączonych dysków maszyny Wirtualnej przy użyciu indeksu, jak pokazano powyżej danych lub hello ```Name``` właściwością hello na dysku, jak przedstawiono poniżej:</span><span class="sxs-lookup"><span data-stu-id="fa7be-130">Similarly you may reference other data disks attached toohello VM, either by using an index as shown above or hello ```Name``` property of hello disk as illustrated below:</span></span>

```Powershell
($vm.StorageProfile.DataDisks | Where {$_.Name -eq 'my-second-data-disk'})[0].DiskSizeGB = 1023
```

<span data-ttu-id="fa7be-131">Jeśli toofind się jak tooattach dyski tooan maszyny Wirtualnej Azure Resource Manager, należy to sprawdzić [artykułu](../articles/virtual-machines/windows/attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="fa7be-131">If you want toofind out how tooattach disks tooan Azure Resource Manager VM, check this [article](../articles/virtual-machines/windows/attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

