---
title: "aaaCreate na maszynie Wirtualnej platformy Azure na podstawie obrazu usługi Azure RemoteApp | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate obrazu usługi Azure RemoteApp, zaczynając od maszyny wirtualnej platformy Azure."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: d41583ef-6cd8-4115-8dcb-b2cd5b3d301a
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 2d432bcb15be68a2946d91b5f36f41d980726338
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-azure-remoteapp-image-based-on-an-azure-virtual-machine"></a><span data-ttu-id="ea398-103">Tworzenie obrazu usługi Azure RemoteApp oparte na maszynie wirtualnej platformy Azure</span><span class="sxs-lookup"><span data-stu-id="ea398-103">Create a Azure RemoteApp image based on an Azure virtual machine</span></span>
> [!IMPORTANT]
> <span data-ttu-id="ea398-104">Usługa Azure RemoteApp nie będzie obsługiwana od 31 sierpnia 2017 r.</span><span class="sxs-lookup"><span data-stu-id="ea398-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="ea398-105">Witaj odczytu [anonsu](https://go.microsoft.com/fwlink/?linkid=821148) szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="ea398-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="ea398-106">Z maszyny wirtualnej platformy Azure, można tworzyć obrazy usługi Azure RemoteApp, (przechowujących aplikacji hello udostępnianych w kolekcji).</span><span class="sxs-lookup"><span data-stu-id="ea398-106">You can create Azure RemoteApp images (which hold hello apps you share in your collection) from an Azure virtual machine.</span></span> <span data-ttu-id="ea398-107">Możesz również wybrać toouse dodaliśmy toohello galerii obrazu maszyny Wirtualnej platformy Azure, które spełnia wszystkie wymagania dotyczące obrazu usługi Azure RemoteApp hello obrazu maszyny wirtualnej — można tego obrazu maszyny Wirtualnej jako punkt początkowy dla własnego maszyny Wirtualnej, jeśli chcesz.</span><span class="sxs-lookup"><span data-stu-id="ea398-107">You could also choose toouse a virtual machine image we added toohello Azure VM image gallery that meets all hello Azure RemoteApp image requirements - you can use that VM image as a starting point for your own VM, if you want.</span></span> <span data-ttu-id="ea398-108">Po prostu wyszukaj hello obrazu "Systemu Windows serwera hosta sesji pulpitu zdalnego" w bibliotece hello.</span><span class="sxs-lookup"><span data-stu-id="ea398-108">Just look for hello "Windows Server Remote Desktop Session Host" image in hello library.</span></span>

<span data-ttu-id="ea398-109">Istnieją dwa toocreate kroki własny obraz oparty na maszynie Wirtualnej platformy Azure — Tworzenie obrazu hello, a następnie przekaż z hello Azure VM biblioteki tooAzure programów RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="ea398-109">There are two steps toocreate your own image based on an Azure VM - create hello image and then upload it from hello Azure VM library tooAzure RemoteApp.</span></span>

## <a name="create-a-custom-image-based-on-an-azure-vm"></a><span data-ttu-id="ea398-110">Utworzyć obraz niestandardowy oparty na maszynie Wirtualnej platformy Azure</span><span class="sxs-lookup"><span data-stu-id="ea398-110">Create a custom image based on an Azure VM</span></span>
<span data-ttu-id="ea398-111">Użyj tych kroków toocreate obraz oparty na maszynie Wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="ea398-111">Use these steps toocreate an image based on an Azure VM.</span></span>

1. <span data-ttu-id="ea398-112">Utwórz maszynę wirtualną platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="ea398-112">Create an Azure virtual machine.</span></span> <span data-ttu-id="ea398-113">Można użyć hello "Systemu Windows serwera hosta sesji pulpitu zdalnego" lub "Windows Server zdalnego pulpitu sesji hosta z Microsoft Office 365 ProPlus" obraz powitania z galerii obrazu maszyny wirtualnej platformy Azure hello.</span><span class="sxs-lookup"><span data-stu-id="ea398-113">You can use hello "Windows Server Remote Desktop Session Host" or hello "Windows Server Remote Desktop Session Host with Microsoft Office 365 ProPlus" image from hello Azure virtual machine image gallery.</span></span> <span data-ttu-id="ea398-114">Ten obraz spełnia wszystkie wymagania obrazu szablonu usługi Azure RemoteApp hello.</span><span class="sxs-lookup"><span data-stu-id="ea398-114">This image meets all hello Azure RemoteApp template image requirements.</span></span>
   
    <span data-ttu-id="ea398-115">Aby uzyskać więcej informacji, zobacz [tworzenia maszyny Wirtualnej z systemem Windows](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ea398-115">For details, see [Create a VM running Windows](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
2. <span data-ttu-id="ea398-116">Połącz toohello maszyny Wirtualnej i instalowanie i konfigurowanie aplikacji hello, które mają tooshare za pośrednictwem usługi RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="ea398-116">Connect toohello VM and install and configure hello apps that you want tooshare through RemoteApp.</span></span> <span data-ttu-id="ea398-117">Upewnij się, że tooperform żadnych dodatkowych konfiguracji systemu Windows wymagane przez aplikacje.</span><span class="sxs-lookup"><span data-stu-id="ea398-117">Make sure tooperform any additional Windows configurations required by your apps.</span></span>
   
    <span data-ttu-id="ea398-118">Aby uzyskać więcej informacji, zobacz [jak tooLog na tooa maszyny wirtualnej z systemu Windows Server](../virtual-machines/windows/classic/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ea398-118">For details, see [How tooLog on tooa Virtual Machine Running Windows Server](../virtual-machines/windows/classic/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>
3. <span data-ttu-id="ea398-119">Jeśli używasz jednego z obrazów hosta sesji usług pulpitu zdalnego serwera Windows hello jest skrypt dołączone weryfikacji, który zapewni, że maszyna wirtualna spełnia RemoteApp hello pre-reqs.</span><span class="sxs-lookup"><span data-stu-id="ea398-119">If you are using one of hello Windows Server Remote Desktop Session Host images, there is an included validation script that will ensure your VM meets hello RemoteApp pre-reqs.</span></span> <span data-ttu-id="ea398-120">toorun skrypt, kliknij dwukrotnie **ValidateRemoteAppImage** hello pulpitu.</span><span class="sxs-lookup"><span data-stu-id="ea398-120">toorun script, double-click **ValidateRemoteAppImage** on hello desktop.</span></span> <span data-ttu-id="ea398-121">Upewnij się, że wszystkie błędy zgłoszone przez skrypt hello zostały usunięte przed kontynuowaniem toohello następnego kroku.</span><span class="sxs-lookup"><span data-stu-id="ea398-121">Ensure that all errors reported by hello script are fixed before proceeding toohello next step.</span></span>
4. <span data-ttu-id="ea398-122">Narzędzie SYSPREP Uogólnij i Przechwyć obraz powitania.</span><span class="sxs-lookup"><span data-stu-id="ea398-122">SYSPREP generalize and capture hello image.</span></span> <span data-ttu-id="ea398-123">Zobacz [jak tooCapture tooUse maszyny wirtualnej systemu Windows, jako szablon](../virtual-machines/windows/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) instrukcje.</span><span class="sxs-lookup"><span data-stu-id="ea398-123">See [How tooCapture a Windows Virtual Machine tooUse as a Template](../virtual-machines/windows/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) for instructions.</span></span>

## <a name="import-hello-image-into-hello-azure-remoteapp-image-library"></a><span data-ttu-id="ea398-124">Importowanie obraz powitania Biblioteka obrazów hello Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="ea398-124">Import hello image into hello Azure RemoteApp image library</span></span>
<span data-ttu-id="ea398-125">Użyj tych kroków tooimport hello nowy obraz do usługi Azure RemoteApp:</span><span class="sxs-lookup"><span data-stu-id="ea398-125">Use these steps tooimport hello new image into Azure RemoteApp:</span></span>

1. <span data-ttu-id="ea398-126">W hello **obrazy szablonów** karty:</span><span class="sxs-lookup"><span data-stu-id="ea398-126">In hello **Template Images** tab:</span></span>
   
   * <span data-ttu-id="ea398-127">Jeśli nie masz żadnych istniejących obrazów, kliknij przycisk **przekazać lub zaimportować obrazu szablonu**.</span><span class="sxs-lookup"><span data-stu-id="ea398-127">If you have no existing images, click **Upload or Import a Template Image**.</span></span>
   * <span data-ttu-id="ea398-128">Jeśli masz już co najmniej jeden obraz, kliknij przycisk  **+**  tooadd nowy obraz.</span><span class="sxs-lookup"><span data-stu-id="ea398-128">If you have at least one image already, click **+** tooadd a new image.</span></span>
2. <span data-ttu-id="ea398-129">Wybierz **Import obrazów z maszyn wirtualnych** biblioteki, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="ea398-129">Select **Import an image from your Virtual Machines** library, and then click **Next**.</span></span>
3. <span data-ttu-id="ea398-130">Na następnej stronie powitania wybierz z listy hello niestandardowego obrazu i upewnij się, że zostały wykonane kroki hello podczas tworzenia obrazu.</span><span class="sxs-lookup"><span data-stu-id="ea398-130">On hello next page, select your custom image from hello list and confirm that you followed hello steps listed when you created your image.</span></span> <span data-ttu-id="ea398-131">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="ea398-131">Click **Next**.</span></span>
4. <span data-ttu-id="ea398-132">Wprowadź nazwę dla nowego obrazu usługi RemoteApp hello i wybierz lokalizację, hello, a następnie kliknij proces importowania hello hello znacznikiem wyboru toostart.</span><span class="sxs-lookup"><span data-stu-id="ea398-132">Enter a name for hello new RemoteApp image and pick hello location, then click hello checkmark toostart hello import process.</span></span>

> [!NOTE]
> <span data-ttu-id="ea398-133">Obrazy można importować z dowolnej lokalizacji platformy Azure obsługiwane przez maszyny wirtualne Azure tooany lokalizacji platformy Azure obsługiwane przez usługę Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="ea398-133">You can import images from any Azure location supported by Azure Virtual Machines tooany Azure location supported by Azure RemoteApp.</span></span> <span data-ttu-id="ea398-134">W zależności od lokalizacji hello hello importowania może potrwać too25 minut.</span><span class="sxs-lookup"><span data-stu-id="ea398-134">Depending on hello locations hello import can take up too25 minutes.</span></span>
> 
> 

<span data-ttu-id="ea398-135">Teraz możesz są gotowe toocreate nowej kolekcji, albo [chmury](remoteapp-create-cloud-deployment.md) kolekcji lub [hybrydowego](remoteapp-create-hybrid-deployment.md), w zależności od potrzeb.</span><span class="sxs-lookup"><span data-stu-id="ea398-135">Now you are ready toocreate your new collection, either a [cloud](remoteapp-create-cloud-deployment.md) collection or [hybrid](remoteapp-create-hybrid-deployment.md), depending on your needs.</span></span>

