---
title: "Magazyn plików Azure instalacji z maszyny Wirtualnej systemu Windows Azure | Dokumentacja firmy Microsoft"
description: "Przechowywanie plików w chmurze za pomocą usługi Azure file storage i instalowanie udziału plików w chmurze z maszyny wirtualnej platformy Azure (VM)."
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
ms.openlocfilehash: 6ffb2d2da1e2439df6f5da543411e3c2c68d3435
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="use-azure-file-shares-with-windows-vms"></a><span data-ttu-id="b1636-103">Udziały plików platformy Azure za pomocą maszyn wirtualnych systemu Windows</span><span class="sxs-lookup"><span data-stu-id="b1636-103">Use Azure file shares with Windows VMs</span></span> 

<span data-ttu-id="b1636-104">Korzystać z udziałów plików na platformę Azure, jako sposób przechowywania i uzyskać dostęp do plików z maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="b1636-104">You can use Azure file shares as a way to store and access files from your VM.</span></span> <span data-ttu-id="b1636-105">Na przykład można przechowywać skryptu lub pliku konfiguracji aplikacji, które wszystkich maszyn wirtualnych do udziału.</span><span class="sxs-lookup"><span data-stu-id="b1636-105">For example, you can store a script or an application configuration file that you want all your VMs to share.</span></span> <span data-ttu-id="b1636-106">W tym temacie zostanie przedstawiony zostanie sposób tworzenia i instalowanie udziału plików na platformę Azure oraz sposób przekazywania i pobierania plików.</span><span class="sxs-lookup"><span data-stu-id="b1636-106">In this topic, we show you how to create and mount an Azure file share, and how to upload and download files.</span></span>

## <a name="connect-to-a-file-share-from-a-vm"></a><span data-ttu-id="b1636-107">Połączenia z udziałem plików z maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="b1636-107">Connect to a file share from a VM</span></span>

<span data-ttu-id="b1636-108">W tej sekcji założono, że masz już udział plików, który chcesz nawiązać połączenie.</span><span class="sxs-lookup"><span data-stu-id="b1636-108">This section assumes you already have a file share that you want to connect to.</span></span> <span data-ttu-id="b1636-109">Jeśli potrzebujesz go utworzyć, zobacz [utworzyć udział plików](#create-a-file-share) dalszej części tego tematu.</span><span class="sxs-lookup"><span data-stu-id="b1636-109">If you need to create one, see [Create a file share](#create-a-file-share) later in this topic.</span></span>

1. <span data-ttu-id="b1636-110">Zaloguj się w witrynie [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b1636-110">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="b1636-111">W menu po lewej stronie kliknij **kont magazynu**.</span><span class="sxs-lookup"><span data-stu-id="b1636-111">On the left menu, click **Storage accounts**.</span></span>
3. <span data-ttu-id="b1636-112">Wybierz konto magazynu.</span><span class="sxs-lookup"><span data-stu-id="b1636-112">Choose your storage account.</span></span>
4. <span data-ttu-id="b1636-113">W **omówienie** w obszarze **usług**, wybierz pozycję **pliki**.</span><span class="sxs-lookup"><span data-stu-id="b1636-113">In the **Overview** page, under **Services**, select **Files**.</span></span>
5. <span data-ttu-id="b1636-114">Wybierz udział plików.</span><span class="sxs-lookup"><span data-stu-id="b1636-114">Select a file share.</span></span>
6. <span data-ttu-id="b1636-115">Kliknij przycisk **Connect** aby otworzyć stronę przedstawiono składnię wiersza polecenia instalowanie udziału plików z systemem Windows lub Linux.</span><span class="sxs-lookup"><span data-stu-id="b1636-115">Click **Connect** to open a page that shows the command-line syntax for mounting the file share from Windows or Linux.</span></span>
7. <span data-ttu-id="b1636-116">Wyróżnij składnię polecenia i wklej go w Notatniku lub w innym miejscu gdzie możesz łatwo do niego dostęp.</span><span class="sxs-lookup"><span data-stu-id="b1636-116">Highlight the syntax of the command and paste it into Notepad or someplace else where you can easily access it.</span></span> 
8. <span data-ttu-id="b1636-117">Edytuj składni, aby usunąć wiodące ** > ** i Zastąp *[litera dysku]* z literą dysku (na przykład **/Y:**) gdzie chcesz zainstalować udział plików.</span><span class="sxs-lookup"><span data-stu-id="b1636-117">Edit the syntax to remove the leading **> ** and replace *[drive letter]* with the drive letter (for example, **Y:**) where you would like to mount the file share.</span></span>
8. <span data-ttu-id="b1636-118">Połącz się z maszyną Wirtualną i otwórz wiersz polecenia.</span><span class="sxs-lookup"><span data-stu-id="b1636-118">Connect to your VM and open a command prompt.</span></span>
9. <span data-ttu-id="b1636-119">Wklej w składni edytowanych połączenia i trafień **Enter**.</span><span class="sxs-lookup"><span data-stu-id="b1636-119">Paste in the edited connection syntax and hit **Enter**.</span></span>
10. <span data-ttu-id="b1636-120">Po utworzeniu połączenia jest wyświetlany komunikat **polecenie zostało wykonane pomyślnie.**</span><span class="sxs-lookup"><span data-stu-id="b1636-120">When the connection has been created, you get the message **The command completed successfully.**</span></span>
11. <span data-ttu-id="b1636-121">Sprawdzanie połączenia, wpisując w literę dysku, aby przełączyć się do tego dysku, a następnie wpisz **dir** Aby wyświetlić zawartość udziału plików.</span><span class="sxs-lookup"><span data-stu-id="b1636-121">Check the connection by typing in the drive letter to switch to that drive and then type **dir** to see the contents of the file share.</span></span>



## <a name="create-a-file-share"></a><span data-ttu-id="b1636-122">Tworzenie udziału plików</span><span class="sxs-lookup"><span data-stu-id="b1636-122">Create a file share</span></span> 
1. <span data-ttu-id="b1636-123">Zaloguj się w witrynie [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b1636-123">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="b1636-124">W menu po lewej stronie kliknij **kont magazynu**.</span><span class="sxs-lookup"><span data-stu-id="b1636-124">On the left menu, click **Storage accounts**.</span></span>
3. <span data-ttu-id="b1636-125">Wybierz konto magazynu.</span><span class="sxs-lookup"><span data-stu-id="b1636-125">Choose your storage account.</span></span>
4. <span data-ttu-id="b1636-126">W **omówienie** w obszarze **usług**, wybierz pozycję **pliki**.</span><span class="sxs-lookup"><span data-stu-id="b1636-126">In the **Overview** page, under **Services**, select **Files**.</span></span>
5. <span data-ttu-id="b1636-127">Na stronie usługi plików, kliknij przycisk **+ udział pliku** do utworzenia pierwszego udziału plików. \\</span><span class="sxs-lookup"><span data-stu-id="b1636-127">In the File Service page, click **+ File share** to create your first file share.\\</span></span>
6. <span data-ttu-id="b1636-128">Wprowadź nazwę udziału plików.</span><span class="sxs-lookup"><span data-stu-id="b1636-128">Fill in the file share name.</span></span> <span data-ttu-id="b1636-129">Nazwy udziałów plików można użyć, małe litery, cyfry i łączniki pojedynczego.</span><span class="sxs-lookup"><span data-stu-id="b1636-129">File share names can use lowercase letters, numbers and single hyphens.</span></span> <span data-ttu-id="b1636-130">Nazwa nie może rozpoczynać się od łącznika i nie można używać wielu łączników obok siebie.</span><span class="sxs-lookup"><span data-stu-id="b1636-130">The name cannot start with a hyphen and you can't use multiple, consecutive hyphens.</span></span> 
7. <span data-ttu-id="b1636-131">Wprowadź limit na rozmiar, jaki może to być plik, do 5120 GB.</span><span class="sxs-lookup"><span data-stu-id="b1636-131">Fill in a limit on how large the file can be, up to 5120 GB.</span></span>
8. <span data-ttu-id="b1636-132">Kliknij przycisk **OK** wdrażania udziału plików.</span><span class="sxs-lookup"><span data-stu-id="b1636-132">Click **OK** to deploy the file share.</span></span>
   
## <a name="upload-files"></a><span data-ttu-id="b1636-133">Przekazywanie plików</span><span class="sxs-lookup"><span data-stu-id="b1636-133">Upload files</span></span>
1. <span data-ttu-id="b1636-134">Zaloguj się w witrynie [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b1636-134">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="b1636-135">W menu po lewej stronie kliknij **kont magazynu**.</span><span class="sxs-lookup"><span data-stu-id="b1636-135">On the left menu, click **Storage accounts**.</span></span>
3. <span data-ttu-id="b1636-136">Wybierz konto magazynu.</span><span class="sxs-lookup"><span data-stu-id="b1636-136">Choose your storage account.</span></span>
4. <span data-ttu-id="b1636-137">W **omówienie** w obszarze **usług**, wybierz pozycję **pliki**.</span><span class="sxs-lookup"><span data-stu-id="b1636-137">In the **Overview** page, under **Services**, select **Files**.</span></span>
5. <span data-ttu-id="b1636-138">Wybierz udział plików.</span><span class="sxs-lookup"><span data-stu-id="b1636-138">Select a file share.</span></span>
6. <span data-ttu-id="b1636-139">Kliknij przycisk **przekazać** otworzyć **przekazać pliki** strony.</span><span class="sxs-lookup"><span data-stu-id="b1636-139">Click **Upload** to open the **Upload files** page.</span></span>
7. <span data-ttu-id="b1636-140">Kliknij ikonę do przeglądania lokalnego systemu plików dla pliku do przekazania.</span><span class="sxs-lookup"><span data-stu-id="b1636-140">Click on the folder icon to browse your local file system for a file to upload.</span></span>   
8. <span data-ttu-id="b1636-141">Kliknij przycisk **przekazać** można przekazać pliku do udziału plików.</span><span class="sxs-lookup"><span data-stu-id="b1636-141">Click **Upload** to upload the file to the file share.</span></span>

## <a name="download-files"></a><span data-ttu-id="b1636-142">Pobieranie plików</span><span class="sxs-lookup"><span data-stu-id="b1636-142">Download files</span></span>
1. <span data-ttu-id="b1636-143">Zaloguj się w witrynie [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b1636-143">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="b1636-144">W menu po lewej stronie kliknij **kont magazynu**.</span><span class="sxs-lookup"><span data-stu-id="b1636-144">On the left menu, click **Storage accounts**.</span></span>
3. <span data-ttu-id="b1636-145">Wybierz konto magazynu.</span><span class="sxs-lookup"><span data-stu-id="b1636-145">Choose your storage account.</span></span>
4. <span data-ttu-id="b1636-146">W **omówienie** w obszarze **usług**, wybierz pozycję **pliki**.</span><span class="sxs-lookup"><span data-stu-id="b1636-146">In the **Overview** page, under **Services**, select **Files**.</span></span>
5. <span data-ttu-id="b1636-147">Wybierz udział plików.</span><span class="sxs-lookup"><span data-stu-id="b1636-147">Select a file share.</span></span>
6. <span data-ttu-id="b1636-148">Kliknij prawym przyciskiem myszy plik i wybierz polecenie **Pobierz** można pobrać go na komputerze lokalnym.</span><span class="sxs-lookup"><span data-stu-id="b1636-148">Right-click on the file and choose **Download** to download it to your local machine.</span></span>
   

## <a name="next-steps"></a><span data-ttu-id="b1636-149">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b1636-149">Next steps</span></span>

<span data-ttu-id="b1636-150">Można również tworzyć i Zarządzanie udziałami plików przy użyciu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b1636-150">You can also create and manage file shares using PowerShell.</span></span> <span data-ttu-id="b1636-151">Aby uzyskać więcej informacji, zobacz [Rozpoczynanie pracy z magazynem plików Azure w systemie Windows](../../storage/files/storage-dotnet-how-to-use-files.md).</span><span class="sxs-lookup"><span data-stu-id="b1636-151">For more information, see [Get started with Azure File storage on Windows](../../storage/files/storage-dotnet-how-to-use-files.md).</span></span>
