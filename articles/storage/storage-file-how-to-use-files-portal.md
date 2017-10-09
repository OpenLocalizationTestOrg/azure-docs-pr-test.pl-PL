---
title: "toomanage aaaHow magazyn plików Azure z hello portalu Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się toouse hello Azure toomanage portalu usługi Magazyn plików Azure."
services: storage
documentationcenter: 
author: RenaShahMSFT
manager: aungoo
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/27/2017
ms.author: renash
ms.openlocfilehash: 385b99ac1c3d97ca79059ae8229afb53f1e825cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-file-storage-from-hello-azure-portal"></a><span data-ttu-id="f718e-103">Jak magazyn plików Azure toouse z hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="f718e-103">How toouse Azure File storage from hello Azure Portal</span></span>
<span data-ttu-id="f718e-104">Witaj [portalu Azure](https://portal.azure.com) udostępnia interfejs użytkownika do zarządzania usługi Magazyn plików Azure.</span><span class="sxs-lookup"><span data-stu-id="f718e-104">hello [Azure portal](https://portal.azure.com) provides a user interface for managing Azure File storage.</span></span> <span data-ttu-id="f718e-105">Można wykonywać hello następujące akcje w przeglądarce sieci web:</span><span class="sxs-lookup"><span data-stu-id="f718e-105">You can perform hello following actions from your web browser:</span></span>

* <span data-ttu-id="f718e-106">Tworzenie udziału plików</span><span class="sxs-lookup"><span data-stu-id="f718e-106">Create a File Share</span></span>
* <span data-ttu-id="f718e-107">Przekazywanie i pobieranie plików tooand z udziału plików.</span><span class="sxs-lookup"><span data-stu-id="f718e-107">Upload and download files tooand from your file share.</span></span>
* <span data-ttu-id="f718e-108">Monitorowanie hello rzeczywistego użycia każdego udziału plików.</span><span class="sxs-lookup"><span data-stu-id="f718e-108">Monitor hello actual usage of each file share.</span></span>
* <span data-ttu-id="f718e-109">Dostosuj hello limitu przydziału rozmiaru udziału plików.</span><span class="sxs-lookup"><span data-stu-id="f718e-109">Adjust hello file share size quota.</span></span>
* <span data-ttu-id="f718e-110">Skopiuj hello instalacji poleceń toouse toomount udostępnić plik z klienta systemu Windows lub Linux.</span><span class="sxs-lookup"><span data-stu-id="f718e-110">Copy hello mount commands toouse toomount your file share from a Windows or Linux client.</span></span>

## <a name="create-file-share"></a><span data-ttu-id="f718e-111">Tworzenie udziału plików</span><span class="sxs-lookup"><span data-stu-id="f718e-111">Create file share</span></span>
1. <span data-ttu-id="f718e-112">Zaloguj się toohello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="f718e-112">Sign in toohello Azure portal.</span></span>
2. <span data-ttu-id="f718e-113">W menu nawigacji powitania kliknij **kont magazynu** lub **kont magazynu (klasyczne)**.</span><span class="sxs-lookup"><span data-stu-id="f718e-113">On hello navigation menu, click **Storage accounts** or **Storage accounts (classic)**.</span></span>
    
    ![Zrzut ekranu pokazujący sposób udział plików toocreate w portalu hello](media/storage-file-how-to-use-files-portal/use-files-portal-create-file-share1.png)

3. <span data-ttu-id="f718e-115">Wybierz konto magazynu.</span><span class="sxs-lookup"><span data-stu-id="f718e-115">Choose your storage account.</span></span>

    ![Zrzut ekranu pokazujący sposób udział plików toocreate w portalu hello](media/storage-file-how-to-use-files-portal/use-files-portal-create-file-share2.png)

4. <span data-ttu-id="f718e-117">Wybierz usługę „Pliki”.</span><span class="sxs-lookup"><span data-stu-id="f718e-117">Choose "Files" service.</span></span>

    ![Zrzut ekranu pokazujący sposób udział plików toocreate w portalu hello](media/storage-file-how-to-use-files-portal/use-files-portal-create-file-share3.png)

5. <span data-ttu-id="f718e-119">Kliknij pozycję "Udziały plików" i wykonaj toocreate łącze hello udostępnianie pierwszego pliku.</span><span class="sxs-lookup"><span data-stu-id="f718e-119">Click "File shares" and follow hello link toocreate your first file share.</span></span>

    ![Zrzut ekranu pokazujący sposób udział plików toocreate w portalu hello](media/storage-file-how-to-use-files-portal/use-files-portal-create-file-share4.png)

6. <span data-ttu-id="f718e-121">Wypełnij nazwę udziału plików hello i rozmiaru hello toocreate udziału (w górę too5120 GB) pliku hello pierwszego udziału plików.</span><span class="sxs-lookup"><span data-stu-id="f718e-121">Fill in hello file share name and hello size of hello file share (up too5120 GB) toocreate your first file share.</span></span> <span data-ttu-id="f718e-122">Po utworzeniu udziału plików hello, możesz go zainstalować z dowolnego systemu plików, który obsługuje protokół SMB 2.1 lub SMB 3.0.</span><span class="sxs-lookup"><span data-stu-id="f718e-122">Once hello file share has been created, you can mount it from any file system that supports SMB 2.1 or SMB 3.0.</span></span> <span data-ttu-id="f718e-123">Można kliknąć na **przydziału** na rozmiar udziału plików hello hello toochange pliku hello się too5120 GB.</span><span class="sxs-lookup"><span data-stu-id="f718e-123">You could click on **Quota** on hello file share toochange hello size of hello file up too5120 GB.</span></span> <span data-ttu-id="f718e-124">Zobacz zbyt[Kalkulator cen platformy Azure](https://azure.microsoft.com/pricing/calculator/) tooestimate hello magazynu koszt używania usługi Magazyn plików Azure.</span><span class="sxs-lookup"><span data-stu-id="f718e-124">Please refer too[Azure Pricing Calculator](https://azure.microsoft.com/pricing/calculator/) tooestimate hello storage cost of using Azure File storage.</span></span>

    ![Zrzut ekranu pokazujący sposób udział plików toocreate w portalu hello](media/storage-file-how-to-use-files-portal/use-files-portal-create-file-share5.png)

## <a name="upload-and-download-files"></a><span data-ttu-id="f718e-126">Przekazywanie i pobieranie plików</span><span class="sxs-lookup"><span data-stu-id="f718e-126">Upload and download files</span></span>
1. <span data-ttu-id="f718e-127">Wybierz utworzony udział plików.</span><span class="sxs-lookup"><span data-stu-id="f718e-127">Choose one file share your have already created.</span></span>

    ![Zrzut ekranu pokazujący sposób tooupload i pobieranie plików z hello portalu](media/storage-file-how-to-use-files-portal/use-files-portal-upload-file1.png)

2. <span data-ttu-id="f718e-129">Kliknij przycisk **przekazać** otworzyć Interfejs użytkownika hello przekazywania plików.</span><span class="sxs-lookup"><span data-stu-id="f718e-129">Click **Upload** to open hello user interface for files uploading.</span></span>

    ![Zrzut ekranu pokazujący sposób tooupload plików z portalu hello](media/storage-file-how-to-use-files-portal/use-files-portal-upload-file2.png)

## <a name="connect-toofile-share"></a><span data-ttu-id="f718e-131">Połącz toofile udziału</span><span class="sxs-lookup"><span data-stu-id="f718e-131">Connect toofile share</span></span>
-  <span data-ttu-id="f718e-132">Kliknij przycisk **Connect** uzyskać hello wiersza polecenia dla udziału plików hello instalowanie z systemu Windows i Linux.</span><span class="sxs-lookup"><span data-stu-id="f718e-132">Click **Connect** to get hello command line for mounting hello file share from Windows and Linux.</span></span> <span data-ttu-id="f718e-133">W przypadku użytkowników systemu Linux, można także skorzystać zbyt[jak toouse magazyn plików Azure z systemem Linux](storage-how-to-use-files-linux.md) instrukcje instalowania dla innych dystrybucje systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="f718e-133">For Linux users, you can also refer too[How toouse Azure File storage with Linux](storage-how-to-use-files-linux.md) for more mounting instructions for other Linux distributions.</span></span>

    ![Zrzut ekranu pokazujący sposób toomount hello udziału plików](media/storage-file-how-to-use-files-portal/use-files-portal-connect.png)
-  <span data-ttu-id="f718e-135">Możesz skopiować hello polecenia służący do instalowania plików udziału w systemie Windows lub Linux i uruchom go, musisz maszyna wirtualna platformy Azure lub lokalnie.</span><span class="sxs-lookup"><span data-stu-id="f718e-135">You can copy hello commands for mounting file share on Windows or Linux and run it from you Azure VM or on-premises machine.</span></span>

    ![Zrzut ekranu pokazujący hello polecenia instalacji systemu Windows i Linux](media/storage-file-how-to-use-files-portal/use-files-portal-show-mount-commands.png)

<span data-ttu-id="f718e-137">**Porada:**</span><span class="sxs-lookup"><span data-stu-id="f718e-137">**Tip:**</span></span>  
<span data-ttu-id="f718e-138">klucz dostępu do konta magazynu hello toofind potrzeby instalacji, kliknij **kluczy dostępu do wyświetlania dla tego konta magazynu** u dołu hello hello połączenia strony.</span><span class="sxs-lookup"><span data-stu-id="f718e-138">toofind hello storage account access key for mounting, click on **View access keys for this storage account** at hello bottom of hello connect page.</span></span>

## <a name="see-also"></a><span data-ttu-id="f718e-139">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="f718e-139">See also</span></span>
<span data-ttu-id="f718e-140">Poniższe linki umożliwiają uzyskanie dodatkowych informacji na temat usługi Magazyn plików Azure.</span><span class="sxs-lookup"><span data-stu-id="f718e-140">See these links for more information about Azure File storage.</span></span>

* [<span data-ttu-id="f718e-141">Często zadawane pytania</span><span class="sxs-lookup"><span data-stu-id="f718e-141">FAQ</span></span>](storage-files-faq.md)
* [<span data-ttu-id="f718e-142">Rozwiązywanie problemów</span><span class="sxs-lookup"><span data-stu-id="f718e-142">Troubleshooting</span></span>](storage-troubleshoot-file-connection-problems.md)