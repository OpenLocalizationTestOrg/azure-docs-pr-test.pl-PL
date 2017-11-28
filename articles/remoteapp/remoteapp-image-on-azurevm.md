---
title: "Tworzenie obrazu usługi Azure RemoteApp opartego na maszynie Wirtualnej platformy Azure | Dokumentacja firmy Microsoft"
description: "Informacje o sposobie tworzenia obrazu usługi Azure RemoteApp, zaczynając od maszyny wirtualnej platformy Azure."
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
ms.openlocfilehash: ee64b86835af8e6237cddcd8acc779fc6dac8214
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-azure-remoteapp-image-based-on-an-azure-virtual-machine"></a><span data-ttu-id="8f422-103">Tworzenie obrazu usługi Azure RemoteApp oparte na maszynie wirtualnej platformy Azure</span><span class="sxs-lookup"><span data-stu-id="8f422-103">Create a Azure RemoteApp image based on an Azure virtual machine</span></span>
> [!IMPORTANT]
> <span data-ttu-id="8f422-104">Usługa Azure RemoteApp nie będzie obsługiwana od 31 sierpnia 2017 r.</span><span class="sxs-lookup"><span data-stu-id="8f422-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="8f422-105">Szczegółowe informacje zawiera [powiadomienie](https://go.microsoft.com/fwlink/?linkid=821148).</span><span class="sxs-lookup"><span data-stu-id="8f422-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="8f422-106">Z maszyny wirtualnej platformy Azure, można tworzyć obrazy usługi Azure RemoteApp, (które przechowywania aplikacji, którą można udostępniać w kolekcji).</span><span class="sxs-lookup"><span data-stu-id="8f422-106">You can create Azure RemoteApp images (which hold the apps you share in your collection) from an Azure virtual machine.</span></span> <span data-ttu-id="8f422-107">Można również użyć obrazu maszyny wirtualnej, dodane do galerii obrazu maszyny Wirtualnej platformy Azure, które spełnia wszystkie wymagania obrazu usługi Azure RemoteApp — można tego obrazu maszyny Wirtualnej jako punkt początkowy dla własnego maszyny Wirtualnej, jeśli chcesz.</span><span class="sxs-lookup"><span data-stu-id="8f422-107">You could also choose to use a virtual machine image we added to the Azure VM image gallery that meets all the Azure RemoteApp image requirements - you can use that VM image as a starting point for your own VM, if you want.</span></span> <span data-ttu-id="8f422-108">Po prostu wyszukaj obraz "Systemu Windows serwera hosta sesji pulpitu zdalnego" w bibliotece.</span><span class="sxs-lookup"><span data-stu-id="8f422-108">Just look for the "Windows Server Remote Desktop Session Host" image in the library.</span></span>

<span data-ttu-id="8f422-109">Istnieją dwa kroki, aby utworzyć własny obraz oparty na maszynie Wirtualnej platformy Azure — Tworzenie obrazu i przekaż go w bibliotece maszyny Wirtualnej platformy Azure do usługi Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="8f422-109">There are two steps to create your own image based on an Azure VM - create the image and then upload it from the Azure VM library to Azure RemoteApp.</span></span>

## <a name="create-a-custom-image-based-on-an-azure-vm"></a><span data-ttu-id="8f422-110">Utworzyć obraz niestandardowy oparty na maszynie Wirtualnej platformy Azure</span><span class="sxs-lookup"><span data-stu-id="8f422-110">Create a custom image based on an Azure VM</span></span>
<span data-ttu-id="8f422-111">Wykonaj te kroki, aby utworzyć obraz oparty na maszynie Wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="8f422-111">Use these steps to create an image based on an Azure VM.</span></span>

1. <span data-ttu-id="8f422-112">Utwórz maszynę wirtualną platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="8f422-112">Create an Azure virtual machine.</span></span> <span data-ttu-id="8f422-113">Można użyć "systemu Windows serwera hosta sesji pulpitu zdalnego" lub "Windows Server zdalnego pulpitu sesji hosta z Microsoft Office 365 ProPlus" obrazu z galerii obrazu maszyny wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="8f422-113">You can use the "Windows Server Remote Desktop Session Host" or the "Windows Server Remote Desktop Session Host with Microsoft Office 365 ProPlus" image from the Azure virtual machine image gallery.</span></span> <span data-ttu-id="8f422-114">Ten obraz spełnia wszystkie usługi Azure RemoteApp szablonu obrazu wymagania.</span><span class="sxs-lookup"><span data-stu-id="8f422-114">This image meets all the Azure RemoteApp template image requirements.</span></span>
   
    <span data-ttu-id="8f422-115">Aby uzyskać więcej informacji, zobacz [tworzenia maszyny Wirtualnej z systemem Windows](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="8f422-115">For details, see [Create a VM running Windows](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
2. <span data-ttu-id="8f422-116">Połączenie z maszyną Wirtualną i zainstaluj i skonfiguruj aplikacje, które ma zostać udostępniona za pośrednictwem usługi RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="8f422-116">Connect to the VM and install and configure the apps that you want to share through RemoteApp.</span></span> <span data-ttu-id="8f422-117">Upewnij się, że wykonywać żadnych dodatkowych konfiguracji systemu Windows wymagane przez aplikacje.</span><span class="sxs-lookup"><span data-stu-id="8f422-117">Make sure to perform any additional Windows configurations required by your apps.</span></span>
   
    <span data-ttu-id="8f422-118">Aby uzyskać więcej informacji, zobacz [jak Zaloguj się do maszyny wirtualnej systemem Windows Server](../virtual-machines/windows/classic/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="8f422-118">For details, see [How to Log on to a Virtual Machine Running Windows Server](../virtual-machines/windows/classic/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>
3. <span data-ttu-id="8f422-119">Jeśli używasz jednego z obrazów hosta sesji usług pulpitu zdalnego serwera systemu Windows jest dołączony weryfikacji skrypt, który zapewni, że maszyna wirtualna spełnia RemoteApp pre-reqs.</span><span class="sxs-lookup"><span data-stu-id="8f422-119">If you are using one of the Windows Server Remote Desktop Session Host images, there is an included validation script that will ensure your VM meets the RemoteApp pre-reqs.</span></span> <span data-ttu-id="8f422-120">Aby uruchomić skrypt, kliknij dwukrotnie **ValidateRemoteAppImage** na pulpicie.</span><span class="sxs-lookup"><span data-stu-id="8f422-120">To run script, double-click **ValidateRemoteAppImage** on the desktop.</span></span> <span data-ttu-id="8f422-121">Upewnij się, że wszystkie błędy zgłoszone przez skrypt zostały usunięte przed przejściem do następnego kroku.</span><span class="sxs-lookup"><span data-stu-id="8f422-121">Ensure that all errors reported by the script are fixed before proceeding to the next step.</span></span>
4. <span data-ttu-id="8f422-122">Programu SYSPREP Uogólnij i Przechwyć obraz.</span><span class="sxs-lookup"><span data-stu-id="8f422-122">SYSPREP generalize and capture the image.</span></span> <span data-ttu-id="8f422-123">Zobacz [jak przechwycić maszynę wirtualną systemu Windows do użycia jako szablon](../virtual-machines/windows/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) instrukcje.</span><span class="sxs-lookup"><span data-stu-id="8f422-123">See [How to Capture a Windows Virtual Machine to Use as a Template](../virtual-machines/windows/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) for instructions.</span></span>

## <a name="import-the-image-into-the-azure-remoteapp-image-library"></a><span data-ttu-id="8f422-124">Zaimportować go do usługi Azure RemoteApp Biblioteka obrazów</span><span class="sxs-lookup"><span data-stu-id="8f422-124">Import the image into the Azure RemoteApp image library</span></span>
<span data-ttu-id="8f422-125">Aby zaimportować nowy obraz do usługi Azure RemoteApp, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="8f422-125">Use these steps to import the new image into Azure RemoteApp:</span></span>

1. <span data-ttu-id="8f422-126">W **obrazy szablonów** karty:</span><span class="sxs-lookup"><span data-stu-id="8f422-126">In the **Template Images** tab:</span></span>
   
   * <span data-ttu-id="8f422-127">Jeśli nie masz żadnych istniejących obrazów, kliknij przycisk **przekazać lub zaimportować obrazu szablonu**.</span><span class="sxs-lookup"><span data-stu-id="8f422-127">If you have no existing images, click **Upload or Import a Template Image**.</span></span>
   * <span data-ttu-id="8f422-128">Jeśli masz już co najmniej jeden obraz, kliknij przycisk  **+**  Aby dodać nowy obraz.</span><span class="sxs-lookup"><span data-stu-id="8f422-128">If you have at least one image already, click **+** to add a new image.</span></span>
2. <span data-ttu-id="8f422-129">Wybierz **Import obrazów z maszyn wirtualnych** biblioteki, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="8f422-129">Select **Import an image from your Virtual Machines** library, and then click **Next**.</span></span>
3. <span data-ttu-id="8f422-130">Na następnej stronie wybierz niestandardowy obraz z listy i upewnij się, że zostały wykonane kroki podczas tworzenia obrazu.</span><span class="sxs-lookup"><span data-stu-id="8f422-130">On the next page, select your custom image from the list and confirm that you followed the steps listed when you created your image.</span></span> <span data-ttu-id="8f422-131">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="8f422-131">Click **Next**.</span></span>
4. <span data-ttu-id="8f422-132">Wprowadź nazwę dla nowego obrazu usługi RemoteApp i wybierz lokalizację, a następnie kliknij znacznik wyboru, aby rozpocząć proces importowania.</span><span class="sxs-lookup"><span data-stu-id="8f422-132">Enter a name for the new RemoteApp image and pick the location, then click the checkmark to start the import process.</span></span>

> [!NOTE]
> <span data-ttu-id="8f422-133">Obrazy można importować z dowolnej lokalizacji platformy Azure obsługiwane przez maszyny wirtualne Azure do dowolnej lokalizacji platformy Azure obsługiwane przez usługę Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="8f422-133">You can import images from any Azure location supported by Azure Virtual Machines to any Azure location supported by Azure RemoteApp.</span></span> <span data-ttu-id="8f422-134">W zależności od lokalizacji importowania może potrwać maksymalnie 25 minut.</span><span class="sxs-lookup"><span data-stu-id="8f422-134">Depending on the locations the import can take up to 25 minutes.</span></span>
> 
> 

<span data-ttu-id="8f422-135">Teraz można przystąpić do tworzenia nowej kolekcji, albo [chmury](remoteapp-create-cloud-deployment.md) kolekcji lub [hybrydowego](remoteapp-create-hybrid-deployment.md), w zależności od potrzeb.</span><span class="sxs-lookup"><span data-stu-id="8f422-135">Now you are ready to create your new collection, either a [cloud](remoteapp-create-cloud-deployment.md) collection or [hybrid](remoteapp-create-hybrid-deployment.md), depending on your needs.</span></span>

