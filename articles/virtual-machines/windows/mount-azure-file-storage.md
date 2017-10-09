---
title: "aaaMount usługi Azure file storage z maszyny Wirtualnej systemu Windows Azure | Dokumentacja firmy Microsoft"
description: "Przechowywanie plików w chmurze hello z usługą Magazyn plików Azure i instalowanie udziału plików w chmurze z maszyny wirtualnej platformy Azure (VM)."
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: 
ms.tgt_pltfrm: 
ms.devlang: 
ms.topic: article
ms.date: 06/15/2017
ms.author: cynthn
ms.openlocfilehash: 965f1c1b3f0d07fec6d86f9312a05e02e8ce7fe0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-file-shares-with-windows-vms"></a><span data-ttu-id="fd95f-103">Udziały plików platformy Azure za pomocą maszyn wirtualnych systemu Windows</span><span class="sxs-lookup"><span data-stu-id="fd95f-103">Use Azure file shares with Windows VMs</span></span> 

<span data-ttu-id="fd95f-104">Udziały plików platformy Azure można użyć jako sposobu toostore i dostęp do plików z maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="fd95f-104">You can use Azure file shares as a way toostore and access files from your VM.</span></span> <span data-ttu-id="fd95f-105">Na przykład można przechowywać skrypt lub plik konfiguracji aplikacji, które mają tooshare maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="fd95f-105">For example, you can store a script or an application configuration file that you want all your VMs tooshare.</span></span> <span data-ttu-id="fd95f-106">W tym temacie zostanie przedstawiony zostanie sposób udziału plików toocreate i instalacji platformy Azure i w jaki sposób tooupload i pobierania plików.</span><span class="sxs-lookup"><span data-stu-id="fd95f-106">In this topic, we show you how toocreate and mount an Azure file share, and how tooupload and download files.</span></span>

## <a name="connect-tooa-file-share-from-a-vm"></a><span data-ttu-id="fd95f-107">Połącz tooa udział plików z maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="fd95f-107">Connect tooa file share from a VM</span></span>

<span data-ttu-id="fd95f-108">W tej sekcji założono, że masz już udział, które mają tooconnect do plików.</span><span class="sxs-lookup"><span data-stu-id="fd95f-108">This section assumes you already have a file share that you want tooconnect to.</span></span> <span data-ttu-id="fd95f-109">Jeśli potrzebujesz toocreate jedną zobacz [utworzyć udział plików](#create-a-file-share) dalszej części tego tematu.</span><span class="sxs-lookup"><span data-stu-id="fd95f-109">If you need toocreate one, see [Create a file share](#create-a-file-share) later in this topic.</span></span>

1. <span data-ttu-id="fd95f-110">Zaloguj się toohello [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="fd95f-110">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="fd95f-111">W menu po lewej stronie powitania kliknij **kont magazynu**.</span><span class="sxs-lookup"><span data-stu-id="fd95f-111">On hello left menu, click **Storage accounts**.</span></span>
3. <span data-ttu-id="fd95f-112">Wybierz konto magazynu.</span><span class="sxs-lookup"><span data-stu-id="fd95f-112">Choose your storage account.</span></span>
4. <span data-ttu-id="fd95f-113">W hello **omówienie** w obszarze **usług**, wybierz pozycję **pliki**.</span><span class="sxs-lookup"><span data-stu-id="fd95f-113">In hello **Overview** page, under **Services**, select **Files**.</span></span>
5. <span data-ttu-id="fd95f-114">Wybierz udział plików.</span><span class="sxs-lookup"><span data-stu-id="fd95f-114">Select a file share.</span></span>
6. <span data-ttu-id="fd95f-115">Kliknij przycisk **Connect** tooopen strona zawierająca hello składni wiersza polecenia dla udziału plików hello instalowanie w systemie Windows lub Linux.</span><span class="sxs-lookup"><span data-stu-id="fd95f-115">Click **Connect** tooopen a page that shows hello command-line syntax for mounting hello file share from Windows or Linux.</span></span>
7. <span data-ttu-id="fd95f-116">Wyróżnij hello Składnia polecenia hello i wklej go w Notatniku lub w innym miejscu gdzie możesz łatwo do niego dostęp.</span><span class="sxs-lookup"><span data-stu-id="fd95f-116">Highlight hello syntax of hello command and paste it into Notepad or someplace else where you can easily access it.</span></span> 
8. <span data-ttu-id="fd95f-117">Edytuj hello składni tooremove hello wiodące ** > ** i Zastąp *[litera dysku]* z literą dysku hello (na przykład **/Y:**) miejsce chcesz udziału plików hello toomount.</span><span class="sxs-lookup"><span data-stu-id="fd95f-117">Edit hello syntax tooremove hello leading **> ** and replace *[drive letter]* with hello drive letter (for example, **Y:**) where you would like toomount hello file share.</span></span>
8. <span data-ttu-id="fd95f-118">Podłącz tooyour maszyny Wirtualnej, a następnie otwórz okno wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="fd95f-118">Connect tooyour VM and open a command prompt.</span></span>
9. <span data-ttu-id="fd95f-119">Wklej w hello edytować składni połączenia i trafień **Enter**.</span><span class="sxs-lookup"><span data-stu-id="fd95f-119">Paste in hello edited connection syntax and hit **Enter**.</span></span>
10. <span data-ttu-id="fd95f-120">Po utworzeniu połączenia hello otrzymasz wiadomość hello **hello polecenie zostało wykonane pomyślnie.**</span><span class="sxs-lookup"><span data-stu-id="fd95f-120">When hello connection has been created, you get hello message **hello command completed successfully.**</span></span>
11. <span data-ttu-id="fd95f-121">Sprawdź połączenie hello, wpisując w hello dysku litery tooswitch toothat stacji, a następnie wpisz **dir** toosee zawartość hello hello udziału plików.</span><span class="sxs-lookup"><span data-stu-id="fd95f-121">Check hello connection by typing in hello drive letter tooswitch toothat drive and then type **dir** toosee hello contents of hello file share.</span></span>



## <a name="create-a-file-share"></a><span data-ttu-id="fd95f-122">Tworzenie udziału plików</span><span class="sxs-lookup"><span data-stu-id="fd95f-122">Create a file share</span></span> 
1. <span data-ttu-id="fd95f-123">Zaloguj się toohello [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="fd95f-123">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="fd95f-124">W menu po lewej stronie powitania kliknij **kont magazynu**.</span><span class="sxs-lookup"><span data-stu-id="fd95f-124">On hello left menu, click **Storage accounts**.</span></span>
3. <span data-ttu-id="fd95f-125">Wybierz konto magazynu.</span><span class="sxs-lookup"><span data-stu-id="fd95f-125">Choose your storage account.</span></span>
4. <span data-ttu-id="fd95f-126">W hello **omówienie** w obszarze **usług**, wybierz pozycję **pliki**.</span><span class="sxs-lookup"><span data-stu-id="fd95f-126">In hello **Overview** page, under **Services**, select **Files**.</span></span>
5. <span data-ttu-id="fd95f-127">Na stronie usługi plików powitania kliknij **+ udział pliku** toocreate udostępnianie pierwszego pliku. \\</span><span class="sxs-lookup"><span data-stu-id="fd95f-127">In hello File Service page, click **+ File share** toocreate your first file share.\\</span></span>
6. <span data-ttu-id="fd95f-128">Wprowadź nazwę udziału plików hello.</span><span class="sxs-lookup"><span data-stu-id="fd95f-128">Fill in hello file share name.</span></span> <span data-ttu-id="fd95f-129">Nazwy udziałów plików można użyć, małe litery, cyfry i łączniki pojedynczego.</span><span class="sxs-lookup"><span data-stu-id="fd95f-129">File share names can use lowercase letters, numbers and single hyphens.</span></span> <span data-ttu-id="fd95f-130">Nazwa Hello nie może rozpoczynać się od łącznika i nie można używać wielu łączników obok siebie.</span><span class="sxs-lookup"><span data-stu-id="fd95f-130">hello name cannot start with a hyphen and you can't use multiple, consecutive hyphens.</span></span> 
7. <span data-ttu-id="fd95f-131">Wypełnij limit na rozmiar pliku hello można się too5120 GB.</span><span class="sxs-lookup"><span data-stu-id="fd95f-131">Fill in a limit on how large hello file can be, up too5120 GB.</span></span>
8. <span data-ttu-id="fd95f-132">Kliknij przycisk **OK** udziału plików hello toodeploy.</span><span class="sxs-lookup"><span data-stu-id="fd95f-132">Click **OK** toodeploy hello file share.</span></span>
   
## <a name="upload-files"></a><span data-ttu-id="fd95f-133">Przekazywanie plików</span><span class="sxs-lookup"><span data-stu-id="fd95f-133">Upload files</span></span>
1. <span data-ttu-id="fd95f-134">Zaloguj się toohello [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="fd95f-134">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="fd95f-135">W menu po lewej stronie powitania kliknij **kont magazynu**.</span><span class="sxs-lookup"><span data-stu-id="fd95f-135">On hello left menu, click **Storage accounts**.</span></span>
3. <span data-ttu-id="fd95f-136">Wybierz konto magazynu.</span><span class="sxs-lookup"><span data-stu-id="fd95f-136">Choose your storage account.</span></span>
4. <span data-ttu-id="fd95f-137">W hello **omówienie** w obszarze **usług**, wybierz pozycję **pliki**.</span><span class="sxs-lookup"><span data-stu-id="fd95f-137">In hello **Overview** page, under **Services**, select **Files**.</span></span>
5. <span data-ttu-id="fd95f-138">Wybierz udział plików.</span><span class="sxs-lookup"><span data-stu-id="fd95f-138">Select a file share.</span></span>
6. <span data-ttu-id="fd95f-139">Kliknij przycisk **przekazać** tooopen hello **przekazać pliki** strony.</span><span class="sxs-lookup"><span data-stu-id="fd95f-139">Click **Upload** tooopen hello **Upload files** page.</span></span>
7. <span data-ttu-id="fd95f-140">Polecenie toobrowse ikona folderu hello lokalnego systemu plików dla tooupload pliku.</span><span class="sxs-lookup"><span data-stu-id="fd95f-140">Click on hello folder icon toobrowse your local file system for a file tooupload.</span></span>   
8. <span data-ttu-id="fd95f-141">Kliknij przycisk **przekazać** udziału plików toohello tooupload hello pliku.</span><span class="sxs-lookup"><span data-stu-id="fd95f-141">Click **Upload** tooupload hello file toohello file share.</span></span>

## <a name="download-files"></a><span data-ttu-id="fd95f-142">Pobieranie plików</span><span class="sxs-lookup"><span data-stu-id="fd95f-142">Download files</span></span>
1. <span data-ttu-id="fd95f-143">Zaloguj się toohello [portalu Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="fd95f-143">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="fd95f-144">W menu po lewej stronie powitania kliknij **kont magazynu**.</span><span class="sxs-lookup"><span data-stu-id="fd95f-144">On hello left menu, click **Storage accounts**.</span></span>
3. <span data-ttu-id="fd95f-145">Wybierz konto magazynu.</span><span class="sxs-lookup"><span data-stu-id="fd95f-145">Choose your storage account.</span></span>
4. <span data-ttu-id="fd95f-146">W hello **omówienie** w obszarze **usług**, wybierz pozycję **pliki**.</span><span class="sxs-lookup"><span data-stu-id="fd95f-146">In hello **Overview** page, under **Services**, select **Files**.</span></span>
5. <span data-ttu-id="fd95f-147">Wybierz udział plików.</span><span class="sxs-lookup"><span data-stu-id="fd95f-147">Select a file share.</span></span>
6. <span data-ttu-id="fd95f-148">Kliknij prawym przyciskiem myszy na powitania plik i wybierz polecenie **Pobierz** toodownload on tooyour komputera lokalnego.</span><span class="sxs-lookup"><span data-stu-id="fd95f-148">Right-click on hello file and choose **Download** toodownload it tooyour local machine.</span></span>
   

## <a name="next-steps"></a><span data-ttu-id="fd95f-149">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="fd95f-149">Next steps</span></span>

<span data-ttu-id="fd95f-150">Można również tworzyć i Zarządzanie udziałami plików przy użyciu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="fd95f-150">You can also create and manage file shares using PowerShell.</span></span> <span data-ttu-id="fd95f-151">Aby uzyskać więcej informacji, zobacz [Rozpoczynanie pracy z magazynem plików Azure w systemie Windows](../../storage/files/storage-dotnet-how-to-use-files.md).</span><span class="sxs-lookup"><span data-stu-id="fd95f-151">For more information, see [Get started with Azure File storage on Windows](../../storage/files/storage-dotnet-how-to-use-files.md).</span></span>
