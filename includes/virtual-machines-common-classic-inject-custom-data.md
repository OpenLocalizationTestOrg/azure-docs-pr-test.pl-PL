


<span data-ttu-id="3d9d0-101">W tym temacie opisano sposób:</span><span class="sxs-lookup"><span data-stu-id="3d9d0-101">This topic describes how to:</span></span>

* <span data-ttu-id="3d9d0-102">Wstaw danych do maszyny wirtualnej platformy Azure (VM), gdy jest inicjowana.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-102">Inject data into an Azure virtual machine (VM) when it is being provisioned.</span></span>
* <span data-ttu-id="3d9d0-103">Pobrać do systemów Windows i Linux.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-103">Retrieve it for both Windows and Linux.</span></span>
* <span data-ttu-id="3d9d0-104">Użyj specjalnego narzędzi dostępnych w niektórych systemach toodetect i automatycznie obsługiwać danych niestandardowych.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-104">Use special tools available on some systems toodetect and handle custom data automatically.</span></span>

> [!NOTE]
> <span data-ttu-id="3d9d0-105">W tym artykule opisano sposób niestandardowe dane mogą zostać dodane przy użyciu maszyny Wirtualnej utworzonej z hello interfejs API zarządzania usługami Azure.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-105">This article describes how custom data can be injected by using a VM created with hello Azure Service Management API.</span></span> <span data-ttu-id="3d9d0-106">toosee toouse hello Azure API Management zasobów, zobacz temat [hello przykładowy szablon](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-customdata).</span><span class="sxs-lookup"><span data-stu-id="3d9d0-106">toosee how toouse hello Azure Resource Management API, see [hello example template](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-customdata).</span></span>
> 
> 

## <a name="injecting-custom-data-into-your-azure-virtual-machine"></a><span data-ttu-id="3d9d0-107">Wstrzykiwania niestandardowe dane do maszyny wirtualnej platformy Azure</span><span class="sxs-lookup"><span data-stu-id="3d9d0-107">Injecting custom data into your Azure virtual machine</span></span>
<span data-ttu-id="3d9d0-108">Ta funkcja jest obecnie obsługiwane tylko w hello [interfejsu wiersza polecenia platformy Azure](https://github.com/Azure/azure-xplat-cli).</span><span class="sxs-lookup"><span data-stu-id="3d9d0-108">This feature is currently supported only in hello [Azure Command-Line Interface](https://github.com/Azure/azure-xplat-cli).</span></span> <span data-ttu-id="3d9d0-109">W tym miejscu utworzymy `custom-data.txt` pliku, który zawiera danych, następnie wstrzyknąć który w toohello maszyny Wirtualnej podczas inicjowania obsługi.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-109">Here we create a `custom-data.txt` file that contains our data, then inject that in toohello VM during provisioning.</span></span> <span data-ttu-id="3d9d0-110">Mimo że można użyć opcji hello na powitania `azure vm create` polecenia hello poniżej pokazano, jednym z podejść bardzo podstawowe:</span><span class="sxs-lookup"><span data-stu-id="3d9d0-110">Although you may use any of hello options for hello `azure vm create` command, hello following demonstrates one very basic approach:</span></span>

```
    azure vm create <vmname> <vmimage> <username> <password> \  
    --location "West US" --ssh 22 \  
    --custom-data ./custom-data.txt  
```


## <a name="using-custom-data-in-hello-virtual-machine"></a><span data-ttu-id="3d9d0-111">W maszynie wirtualnej hello przy użyciu niestandardowych danych</span><span class="sxs-lookup"><span data-stu-id="3d9d0-111">Using custom data in hello virtual machine</span></span>
* <span data-ttu-id="3d9d0-112">Jeśli maszyna wirtualna Azure jest Maszynę wirtualną z systemem Windows, a następnie hello niestandardowych danych zostanie zapisany za`%SYSTEMDRIVE%\AzureData\CustomData.bin`.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-112">If your Azure VM is a Windows-based VM, then hello custom data file is saved too`%SYSTEMDRIVE%\AzureData\CustomData.bin`.</span></span> <span data-ttu-id="3d9d0-113">Mimo że był algorytmem Base64 tootransfer z toohello komputera lokalnego hello nowej maszyny Wirtualnej, jest automatycznie zdekodować i można otworzyć lub użyć natychmiast.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-113">Although it was base64-encoded tootransfer from hello local computer toohello new VM, it is automatically decoded and can be opened or used immediately.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="3d9d0-114">Jeśli plik hello istnieje, zostanie zastąpiony.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-114">If hello file exists, it is overwritten.</span></span> <span data-ttu-id="3d9d0-115">zabezpieczenia Hello katalogu hello są skonfigurowane za**systemu: Pełna kontrola** i **Administratorzy: Pełna kontrola**.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-115">hello security on hello directory is set too**System:Full Control** and **Administrators:Full Control**.</span></span>
  > 
  > 
* <span data-ttu-id="3d9d0-116">W przypadku maszyny Wirtualnej Azure opartych na systemie Linux maszyny Wirtualnej, a następnie plik danych niestandardowych hello będą znajdować się w jednej z następujących hello umieszcza w zależności od Twojego distro.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-116">If your Azure VM is a Linux-based VM, then hello custom data file will be located in one of hello following places depending on your distro.</span></span> <span data-ttu-id="3d9d0-117">Witaj dane mogą być algorytmem Base64, może więc być konieczny danych hello toodecode najpierw:</span><span class="sxs-lookup"><span data-stu-id="3d9d0-117">hello data may be base64-encoded, so you may need toodecode hello data first:</span></span>
  
  * `/var/lib/waagent/ovf-env.xml`
  * `/var/lib/waagent/CustomData`
  * `/var/lib/cloud/instance/user-data.txt` 

## <a name="cloud-init-on-azure"></a><span data-ttu-id="3d9d0-118">Inicjowania chmurze na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="3d9d0-118">Cloud-init on Azure</span></span>
<span data-ttu-id="3d9d0-119">W przypadku maszyny Wirtualnej Azure z obrazu Ubuntu lub CoreOS, można użyć toosend CustomData inicjowaniem toocloud konfiguracji chmury.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-119">If your Azure VM is from an Ubuntu or CoreOS image, then you can use CustomData toosend a cloud-config toocloud-init.</span></span> <span data-ttu-id="3d9d0-120">Lub jeśli plik danych niestandardowych jest skryptem, następnie init chmury można po prostu wykonywania.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-120">Or if your custom data file is a script, then cloud-init can simply execute it.</span></span>

### <a name="ubuntu-cloud-images"></a><span data-ttu-id="3d9d0-121">Obrazy Ubuntu chmury</span><span class="sxs-lookup"><span data-stu-id="3d9d0-121">Ubuntu Cloud Images</span></span>
<span data-ttu-id="3d9d0-122">W większości obrazów systemu Linux platformy Azure, możesz edytować "/ etc/waagent.conf" tooconfigure hello zasobów dysku i zamiany pliku.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-122">In most Azure Linux images, you would edit "/etc/waagent.conf" tooconfigure hello temporary resource disk and swap file.</span></span> <span data-ttu-id="3d9d0-123">Zobacz [Podręcznik użytkownika agenta systemu Linux Azure](../articles/virtual-machines/linux/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-123">See [Azure Linux Agent user guide](../articles/virtual-machines/linux/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for more information.</span></span>

<span data-ttu-id="3d9d0-124">Jednak na powitania Ubuntu chmury obrazów, należy użyć init chmury tooconfigure hello zasobu dysku (to znaczy hello "tymczasowych" dysk) i wymiany partycji.</span><span class="sxs-lookup"><span data-stu-id="3d9d0-124">However, on hello Ubuntu Cloud Images, you must use cloud-init tooconfigure hello resource disk (that is, hello "ephemeral" disk) and swap partition.</span></span> <span data-ttu-id="3d9d0-125">Zobacz następujące strony w witrynie wiki Ubuntu hello szczegółowe hello: [AzureSwapPartitions](https://wiki.ubuntu.com/AzureSwapPartitions).</span><span class="sxs-lookup"><span data-stu-id="3d9d0-125">See hello following page on hello Ubuntu wiki for more details: [AzureSwapPartitions](https://wiki.ubuntu.com/AzureSwapPartitions).</span></span>

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps-using-cloud-init"></a><span data-ttu-id="3d9d0-126">Następne kroki: przy użyciu inicjowania chmury</span><span class="sxs-lookup"><span data-stu-id="3d9d0-126">Next steps: Using cloud-init</span></span>
<span data-ttu-id="3d9d0-127">Aby uzyskać więcej informacji, zobacz hello [init chmury dokumentacji Ubuntu](https://help.ubuntu.com/community/CloudInit).</span><span class="sxs-lookup"><span data-stu-id="3d9d0-127">For further information, see hello [cloud-init documentation for Ubuntu](https://help.ubuntu.com/community/CloudInit).</span></span>

<!--Link references-->
[<span data-ttu-id="3d9d0-128">Dodaj dokumentacja interfejsu API REST zarządzania usługi roli</span><span class="sxs-lookup"><span data-stu-id="3d9d0-128">Add Role Service Management REST API Reference</span></span>](http://msdn.microsoft.com/library/azure/jj157186.aspx)

[<span data-ttu-id="3d9d0-129">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="3d9d0-129">Azure Command-line Interface</span></span>](https://github.com/Azure/azure-xplat-cli)

