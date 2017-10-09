
1. <span data-ttu-id="4ce23-101">Zaloguj się tooyour subskrypcji platformy Azure przy użyciu hello czynności opisane w [połączyć tooAzure z hello Azure CLI 1.0](../articles/xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="4ce23-101">Sign in tooyour Azure subscription using hello steps listed in [Connect tooAzure from hello Azure CLI 1.0](../articles/xplat-cli-connect.md).</span></span>

2. <span data-ttu-id="4ce23-102">Upewnij się, że są w trybie wdrożenia klasycznego hello w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="4ce23-102">Make sure you are in hello Classic deployment mode as follows:</span></span>

    ```azurecli
    azure config mode asm
    ```

3. <span data-ttu-id="4ce23-103">Sprawdzić hello obrazu systemu Linux, które mają tooload z hello dostępnych obrazów w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="4ce23-103">Find out hello Linux image that you want tooload from hello available images as follows:</span></span>

   ```azurecli   
    azure vm image list | grep "Linux"
    ```
   
    <span data-ttu-id="4ce23-104">W oknie wiersza polecenia systemu Windows użyj polecenia **find** zamiast grep.</span><span class="sxs-lookup"><span data-stu-id="4ce23-104">In a Windows command-prompt window, use **find** instead of grep.</span></span>
   
4. <span data-ttu-id="4ce23-105">Użyj `azure vm create` toocreate maszyny Wirtualnej z obrazu systemu Linux hello z poprzedniej liście hello.</span><span class="sxs-lookup"><span data-stu-id="4ce23-105">Use `azure vm create` toocreate a VM with hello Linux image from hello previous list.</span></span> <span data-ttu-id="4ce23-106">Ten krok powoduje utworzenie konta magazynu i usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="4ce23-106">This step creates a cloud service and storage account.</span></span> <span data-ttu-id="4ce23-107">Można także połączyć tej maszyny Wirtualnej tooan istniejącej usługi w chmurze z `-c` opcji.</span><span class="sxs-lookup"><span data-stu-id="4ce23-107">You could also connect this VM tooan existing cloud service with a `-c` option.</span></span> <span data-ttu-id="4ce23-108">Utwórz toolog punkt końcowy SSH w maszyny wirtualnej systemu Linux toohello z hello `-e` opcji.</span><span class="sxs-lookup"><span data-stu-id="4ce23-108">Create an SSH endpoint toolog in toohello Linux virtual machine with hello `-e` option.</span></span> <span data-ttu-id="4ce23-109">Witaj poniższy przykład tworzy Maszynę wirtualną o nazwie `myVM` przy użyciu hello `Ubuntu-14_04_4-LTS` obrazu w hello `West US` lokalizacji i dodaje nazwę użytkownika `ops`:</span><span class="sxs-lookup"><span data-stu-id="4ce23-109">hello following example creates a VM named `myVM` using hello `Ubuntu-14_04_4-LTS` image in hello `West US` location, and adds a user name `ops`:</span></span>
   
    ```azurecli
    azure vm create myVM \
        b39f27a8b8c64d52b05eac6a62ebad85__Ubuntu-14_04_4-LTS-amd64-server-20160516-en-us-30GB \
        -g ops -p P@ssw0rd! -z "Small" -e -l "West US"
    ```

    <span data-ttu-id="4ce23-110">Witaj danych wyjściowych jest toohello podobnie poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="4ce23-110">hello output is similar toohello following example:</span></span>

    ```azurecli
    info:    Executing command vm create
    + Looking up image b39f27a8b8c64d52b05eac6a62ebad85__Ubuntu-14_04_4-LTS-amd64-server-20160516-en-us-30GB
    + Looking up cloud service
    info:    cloud service myVM not found.
    + Creating cloud service
    + Retrieving storage accounts
    + Creating VM
    info:    vm create command OK
    ```
   
   > [!NOTE]
   > <span data-ttu-id="4ce23-111">Dla maszyny wirtualnej systemu Linux, należy podać hello `-e` opcji `vm create`.</span><span class="sxs-lookup"><span data-stu-id="4ce23-111">For a Linux virtual machine, you must provide hello `-e` option in `vm create`.</span></span> <span data-ttu-id="4ce23-112">Nie jest możliwe tooenable SSH po utworzeniu maszyny wirtualnej hello.</span><span class="sxs-lookup"><span data-stu-id="4ce23-112">It is not possible tooenable SSH after hello virtual machine has been created.</span></span> <span data-ttu-id="4ce23-113">Aby uzyskać więcej szczegółów na SSH, przeczytaj [jak tooUse SSH z systemem Linux na platformie Azure](../articles/virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="4ce23-113">For more details on SSH, read [How tooUse SSH with Linux on Azure](../articles/virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

5. <span data-ttu-id="4ce23-114">Atrybuty hello hello maszyny Wirtualnej można sprawdzić za pomocą hello `azure vm show` polecenia.</span><span class="sxs-lookup"><span data-stu-id="4ce23-114">You can verify hello attributes of hello VM by using hello `azure vm show` command.</span></span> <span data-ttu-id="4ce23-115">Witaj poniższy przykład zawiera informacje dotyczące hello maszyny Wirtualnej o nazwie `myVM`:</span><span class="sxs-lookup"><span data-stu-id="4ce23-115">hello following example lists information for hello VM named `myVM`:</span></span>

    ```azurecli   
    azure vm show myVM
    ```

6. <span data-ttu-id="4ce23-116">Uruchom maszyny Wirtualnej z hello `azure vm start` polecenia w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="4ce23-116">Start your VM with hello `azure vm start` command as follows:</span></span>

    ```azurecli
    azure vm start myVM
    ```

## <a name="next-steps"></a><span data-ttu-id="4ce23-117">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="4ce23-117">Next steps</span></span>
<span data-ttu-id="4ce23-118">Aby uzyskać więcej informacji na temat wszystkich tych poleceń maszyny wirtualnej Azure CLI w wersji 1.0, przeczytaj hello [hello Using Azure CLI 1.0 z hello wdrażania klasycznego interfejsu API](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="4ce23-118">For details on all these Azure CLI 1.0 virtual machine commands, read hello [Using hello Azure CLI 1.0 with hello Classic deployment API](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span></span>

