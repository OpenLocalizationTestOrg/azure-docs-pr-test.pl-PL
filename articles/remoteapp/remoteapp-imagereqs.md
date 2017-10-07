---
title: "wymagania dotyczące obrazu usługi RemoteApp aaaAzure | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat wymagań hello tworzenia toobe obrazy używane z usługą Azure RemoteApp"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 7cbb90f4-6dc9-462c-a429-088cdb57414e
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: 4e35203eb93a866d4e0bd591d42b34746c7ffa4d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="requirements-for-azure-remoteapp-images"></a><span data-ttu-id="3748a-103">Wymagania dotyczące usługi Azure RemoteApp obrazów</span><span class="sxs-lookup"><span data-stu-id="3748a-103">Requirements for Azure RemoteApp images</span></span>
> [!IMPORTANT]
> <span data-ttu-id="3748a-104">Usługa Azure RemoteApp nie będzie obsługiwana od 31 sierpnia 2017 r.</span><span class="sxs-lookup"><span data-stu-id="3748a-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="3748a-105">Witaj odczytu [anonsu](https://go.microsoft.com/fwlink/?linkid=821148) szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="3748a-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="3748a-106">Usługa Azure RemoteApp używa toohost obrazu systemu Windows Server 2012 R2, wszystkie programy hello mają tooshare z użytkownikami.</span><span class="sxs-lookup"><span data-stu-id="3748a-106">Azure RemoteApp uses a Windows Server 2012 R2 image toohost all hello programs that you want tooshare with your users.</span></span> <span data-ttu-id="3748a-107">toocreate niestandardowego obrazu, można uruchomić z istniejącego obrazu lub [Utwórz nową](remoteapp-create-custom-image.md).</span><span class="sxs-lookup"><span data-stu-id="3748a-107">toocreate a custom image, you can start with an existing image or [create a new one](remoteapp-create-custom-image.md).</span></span>

> [!TIP]
> <span data-ttu-id="3748a-108">Czy wiesz, że Twoje daje subskrypcji usługi Azure RemoteApp dostęp tooa obrazu systemu Windows Server 2012 R2 w hello galerii maszyny Wirtualnej platformy Azure, których można używać toocreate obrazu szablonu?</span><span class="sxs-lookup"><span data-stu-id="3748a-108">Did you know that your Azure RemoteApp subscription gives you access tooa Windows Server 2012 R2 image in hello Azure VM gallery that you can use toocreate your own template image?</span></span> <span data-ttu-id="3748a-109">[Go wyewidencjonować](remoteapp-image-on-azurevm.md).</span><span class="sxs-lookup"><span data-stu-id="3748a-109">[Check it out](remoteapp-image-on-azurevm.md).</span></span>  
> 
> 

<span data-ttu-id="3748a-110">Witaj wymagania dotyczące obrazu hello, które mogą być przekazywane do użycia z usługą Azure RemoteApp są:</span><span class="sxs-lookup"><span data-stu-id="3748a-110">hello requirements for hello image that can be uploaded for use with Azure RemoteApp are:</span></span>

* <span data-ttu-id="3748a-111">Niestandardowych aplikacji nie należy przechowywać dane lokalnie na powitania obrazu.</span><span class="sxs-lookup"><span data-stu-id="3748a-111">Custom applications don’t store data locally on hello image.</span></span> <span data-ttu-id="3748a-112">Te obrazy są bezstanowych i powinien zawierać wyłącznie aplikacje.</span><span class="sxs-lookup"><span data-stu-id="3748a-112">These images are stateless and should only contain applications.</span></span>
* <span data-ttu-id="3748a-113">Obraz powitania nie zawiera danych, które mogą zostać utracone.</span><span class="sxs-lookup"><span data-stu-id="3748a-113">hello image does not contain data that can be lost.</span></span>
* <span data-ttu-id="3748a-114">rozmiar obrazu Hello powinna być wielokrotnością liczby MB.</span><span class="sxs-lookup"><span data-stu-id="3748a-114">hello image size should be a multiple of MBs.</span></span> <span data-ttu-id="3748a-115">Jeśli spróbujesz tooupload obrazu, który nie jest wielokrotnością hello przekazywanie zakończy się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="3748a-115">If you try tooupload an image that is not an exact multiple, hello upload will fail.</span></span>
* <span data-ttu-id="3748a-116">Witaj, rozmiar obrazu musi być 127 GB lub mniej.</span><span class="sxs-lookup"><span data-stu-id="3748a-116">hello image size must be 127 GB or smaller.</span></span>
* <span data-ttu-id="3748a-117">Musi znajdować się na plik VHD (pliki VHDX nie są obecnie obsługiwane).</span><span class="sxs-lookup"><span data-stu-id="3748a-117">It must be on a VHD file (VHDX files are not currently supported).</span></span>
* <span data-ttu-id="3748a-118">Witaj wirtualnego dysku twardego nie może być maszyny wirtualnej generacji 2.</span><span class="sxs-lookup"><span data-stu-id="3748a-118">hello VHD must not be a generation 2 virtual machine.</span></span>
* <span data-ttu-id="3748a-119">Witaj wirtualnego dysku twardego może być stałym rozmiarze lub dynamicznie powiększających się.</span><span class="sxs-lookup"><span data-stu-id="3748a-119">hello VHD can be either fixed-size or dynamically expanding.</span></span> <span data-ttu-id="3748a-120">Dynamicznie powiększających się dysków VHD jest zalecane, ponieważ trwa tooAzure tooupload mniej czasu niż ustalony rozmiar pliku VHD.</span><span class="sxs-lookup"><span data-stu-id="3748a-120">A dynamically expanding VHD is recommended because it takes less time tooupload tooAzure than a fixed-size VHD file.</span></span>
* <span data-ttu-id="3748a-121">dysk Hello musi zostać zainicjowany przy użyciu stylu partycjonowania hello główny rekord rozruchowy (MBR).</span><span class="sxs-lookup"><span data-stu-id="3748a-121">hello disk must be initialized using hello Master Boot Record (MBR) partitioning style.</span></span> <span data-ttu-id="3748a-122">Witaj stylu partycji (GPT tabela) partycji GUID nie jest obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="3748a-122">hello GUID partition table (GPT) partition style is not supported.</span></span>
* <span data-ttu-id="3748a-123">Witaj dysku VHD musi zawierać jednej instalacji systemu Windows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="3748a-123">hello VHD must contain a single installation of Windows Server 2012 R2.</span></span> <span data-ttu-id="3748a-124">Nazwa może zawierać wiele woluminów, ale tylko jeden zawartych w instalacji systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="3748a-124">It can contain multiple volumes, but only one that contains an installation of Windows.</span></span>
* <span data-ttu-id="3748a-125">Witaj zdalnego pulpitu sesji hosta ról i funkcji Środowisko pulpitu hello musi być zainstalowany.</span><span class="sxs-lookup"><span data-stu-id="3748a-125">hello Remote Desktop Session Host (RDSH) role and hello Desktop Experience feature must be installed.</span></span>
* <span data-ttu-id="3748a-126">Witaj roli Broker połączeń usług pulpitu zdalnego musi *nie* można zainstalować.</span><span class="sxs-lookup"><span data-stu-id="3748a-126">hello Remote Desktop Connection Broker role must *not* be installed.</span></span>
* <span data-ttu-id="3748a-127">Witaj system szyfrowania plików (EFS) musi być wyłączona.</span><span class="sxs-lookup"><span data-stu-id="3748a-127">hello Encrypting File System (EFS) must be disabled.</span></span>
* <span data-ttu-id="3748a-128">Witaj obrazu musi być przetworzonej przez program Sysprep przy użyciu parametrów hello **/oobe / generalize/shutdown** (nie należy używać hello **/mode:vm** parametru).</span><span class="sxs-lookup"><span data-stu-id="3748a-128">hello image must be SYSPREPed using hello parameters **/oobe /generalize /shutdown** (DO NOT use hello **/mode:vm** parameter).</span></span>
* <span data-ttu-id="3748a-129">Przekazywanie dysk VHD z łańcucha migawek nie jest obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="3748a-129">Uploading your VHD from a snapshot chain is not supported.</span></span>

<span data-ttu-id="3748a-130">Zobacz [Tworzenie obrazu usługi Azure RemoteApp](remoteapp-imageoptions.md) Aby uzyskać więcej informacji na temat tworzenia obrazów na potrzeby usługi Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="3748a-130">See [Create an Azure RemoteApp image](remoteapp-imageoptions.md) for more information about creating images for Azure RemoteApp.</span></span>

