---
title: "pliki aaaPersist w powłoce chmury Azure (wersja zapoznawcza) | Dokumentacja firmy Microsoft"
description: "Wskazówki dotyczące jak powłoki chmury Azure będzie się powtarzał plików."
services: 
documentationcenter: 
author: jluk
manager: timlt
tags: azure-resource-manager
ms.assetid: 
ms.service: azure
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: juluk
ms.openlocfilehash: b230453d5551c545553d63559741950206e4f1b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="persist-files-in-azure-cloud-shell"></a><span data-ttu-id="df8e8-103">Utrwalanie plików w powłoce chmury Azure</span><span class="sxs-lookup"><span data-stu-id="df8e8-103">Persist files in Azure Cloud Shell</span></span>
<span data-ttu-id="df8e8-104">Powłoka chmury wykorzystuje pliki toopersist magazynu plików Azure między sesjami.</span><span class="sxs-lookup"><span data-stu-id="df8e8-104">Cloud Shell takes advantage of Azure File storage toopersist files across sessions.</span></span>

## <a name="set-up-a-clouddrive-file-share"></a><span data-ttu-id="df8e8-105">Konfigurowanie `clouddrive` udziału plików</span><span class="sxs-lookup"><span data-stu-id="df8e8-105">Set up a `clouddrive` file share</span></span>
<span data-ttu-id="df8e8-106">Na początkowej start powłoki chmury monituje tooassociate nowy lub istniejący plik udostępniać pliki toopersist między sesjami.</span><span class="sxs-lookup"><span data-stu-id="df8e8-106">On initial start, Cloud Shell prompts you tooassociate a new or existing file share toopersist files across sessions.</span></span>

### <a name="create-new-storage"></a><span data-ttu-id="df8e8-107">Tworzenie nowego magazynu</span><span class="sxs-lookup"><span data-stu-id="df8e8-107">Create new storage</span></span>

<span data-ttu-id="df8e8-108">Gdy używasz podstawowych ustawień i wybierz tylko subskrypcję, powłoki chmury tworzy trzy zasoby w Twoim imieniu w regionie hello obsługiwane, która jest najbliższym tooyou:</span><span class="sxs-lookup"><span data-stu-id="df8e8-108">When you use basic settings and select only a subscription, Cloud Shell creates three resources on your behalf in hello supported region that's nearest tooyou:</span></span>
* <span data-ttu-id="df8e8-109">Grupa zasobów:`cloud-shell-storage-<region>`</span><span class="sxs-lookup"><span data-stu-id="df8e8-109">Resource group: `cloud-shell-storage-<region>`</span></span>
* <span data-ttu-id="df8e8-110">Konto magazynu:`cs<uniqueGuid>`</span><span class="sxs-lookup"><span data-stu-id="df8e8-110">Storage account: `cs<uniqueGuid>`</span></span>
* <span data-ttu-id="df8e8-111">Udziału plików:`cs-<user>-<domain>-com-<uniqueGuid>`</span><span class="sxs-lookup"><span data-stu-id="df8e8-111">File share: `cs-<user>-<domain>-com-<uniqueGuid>`</span></span>

![Witaj ustawień subskrypcji](media/basic-storage.png)

<span data-ttu-id="df8e8-113">Instaluje Hello udziału plików jako `clouddrive` w Twojej `$Home` katalogu.</span><span class="sxs-lookup"><span data-stu-id="df8e8-113">hello file share mounts as `clouddrive` in your `$Home` directory.</span></span> <span data-ttu-id="df8e8-114">Witaj udział plików jest również używane toostore obrazu 5 GB, która jest tworzona automatycznie dla użytkownika i aktualizuje i będzie się powtarzał Twojej `$Home` katalogu.</span><span class="sxs-lookup"><span data-stu-id="df8e8-114">hello file share is also used toostore a 5-GB image that's created for you and that automatically updates and persists your `$Home` directory.</span></span> <span data-ttu-id="df8e8-115">To działanie jednorazowe i udziału plików hello automatycznie instaluje się w kolejnych sesjach.</span><span class="sxs-lookup"><span data-stu-id="df8e8-115">This is a one-time action, and hello file share mounts automatically in subsequent sessions.</span></span>

### <a name="use-existing-resources"></a><span data-ttu-id="df8e8-116">Korzystać z istniejących zasobów</span><span class="sxs-lookup"><span data-stu-id="df8e8-116">Use existing resources</span></span>

<span data-ttu-id="df8e8-117">Przy użyciu zaawansowanych opcji hello, można skojarzyć istniejących zasobów.</span><span class="sxs-lookup"><span data-stu-id="df8e8-117">By using hello advanced option, you can associate existing resources.</span></span> <span data-ttu-id="df8e8-118">Po wyświetleniu monitu Instalatora magazynu hello zaznacz **Pokaż zaawansowane ustawienia** tooview dodatkowe opcje.</span><span class="sxs-lookup"><span data-stu-id="df8e8-118">When hello storage setup prompt appears, select **Show advanced settings** tooview additional options.</span></span> <span data-ttu-id="df8e8-119">Istniejących udziałów plików odbierania toopersist obrazu użytkownika 5 GB z `$Home` katalogu.</span><span class="sxs-lookup"><span data-stu-id="df8e8-119">Existing file shares receive a 5-GB user image toopersist your `$Home` directory.</span></span> <span data-ttu-id="df8e8-120">menu rozwijane Hello są filtrowane w Twoim regionie powłoki w chmurze i kont lokalnych nadmiarowe & geograficznie nadmiarowego magazynu.</span><span class="sxs-lookup"><span data-stu-id="df8e8-120">hello drop-down menus are filtered for your Cloud Shell region and for local-redundant & geo-redundant storage accounts.</span></span>

![Witaj ustawienie grupy zasobów](media/advanced-storage.png)

### <a name="restrict-resource-creation-with-an-azure-resource-policy"></a><span data-ttu-id="df8e8-122">Ogranicz tworzenie zasobów przy użyciu zasad zasobów platformy Azure</span><span class="sxs-lookup"><span data-stu-id="df8e8-122">Restrict resource creation with an Azure resource policy</span></span>
<span data-ttu-id="df8e8-123">Konta magazynu, utworzone w chmurze powłoki są oznaczane `ms-resource-usage:azure-cloud-shell`.</span><span class="sxs-lookup"><span data-stu-id="df8e8-123">Storage accounts that you create in Cloud Shell are tagged with `ms-resource-usage:azure-cloud-shell`.</span></span> <span data-ttu-id="df8e8-124">Toodisallow użytkownikom tworzenie kont magazynu w chmurze powłoki, utworzyć [zasad zasobów platformy Azure dla tagów](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-policy-tags) wyzwolenia przy tym konkretnym elementem tag.</span><span class="sxs-lookup"><span data-stu-id="df8e8-124">If you want toodisallow users from creating storage accounts in Cloud Shell, create an [Azure resource policy for tags](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-policy-tags) that are triggered by this specific tag.</span></span>

## <a name="how-cloud-shell-works"></a><span data-ttu-id="df8e8-125">Jak działa powłoki chmury</span><span class="sxs-lookup"><span data-stu-id="df8e8-125">How Cloud Shell works</span></span>
<span data-ttu-id="df8e8-126">Powłoka w chmurze będzie się powtarzał plików za pomocą obu hello następujące metody:</span><span class="sxs-lookup"><span data-stu-id="df8e8-126">Cloud Shell persists files through both of hello following methods:</span></span>
* <span data-ttu-id="df8e8-127">Tworzenie obrazu dysku z Twojej `$Home` toopersist katalogu wszystkich zawartości w katalogu hello.</span><span class="sxs-lookup"><span data-stu-id="df8e8-127">Creating a disk image of your `$Home` directory toopersist all contents within hello directory.</span></span> <span data-ttu-id="df8e8-128">obraz dysku Hello jest zapisywany w udziale określony plik jako `acc_<User>.img` w `fileshare.storage.windows.net/fileshare/.cloudconsole/acc_<User>.img`, i automatycznie synchronizuje zmiany.</span><span class="sxs-lookup"><span data-stu-id="df8e8-128">hello disk image is saved in your specified file share as `acc_<User>.img` at `fileshare.storage.windows.net/fileshare/.cloudconsole/acc_<User>.img`, and it automatically syncs changes.</span></span>

* <span data-ttu-id="df8e8-129">Instalowanie udziału plików określony jako `clouddrive` w Twojej `$Home` katalogu do interakcji z udziału plików bezpośrednio.</span><span class="sxs-lookup"><span data-stu-id="df8e8-129">Mounting your specified file share as `clouddrive` in your `$Home` directory for direct file share interaction.</span></span> <span data-ttu-id="df8e8-130">`/Home/<User>/clouddrive`jest mapowany za`fileshare.storage.windows.net/fileshare`.</span><span class="sxs-lookup"><span data-stu-id="df8e8-130">`/Home/<User>/clouddrive` is mapped too`fileshare.storage.windows.net/fileshare`.</span></span>
 
> [!NOTE]
> <span data-ttu-id="df8e8-131">Wszystkie pliki w Twojej `$Home` katalogu, takiego jak kluczy SSH są zachowywane w obrazie dysku użytkownika, który jest przechowywany w udziale zainstalowanego pliku.</span><span class="sxs-lookup"><span data-stu-id="df8e8-131">All files in your `$Home` directory, such as SSH keys, are persisted in your user disk image, which is stored in your mounted file share.</span></span> <span data-ttu-id="df8e8-132">Zastosowanie najlepszych rozwiązań podczas utrwalania informacji w sieci `$Home` katalogu i udziału zainstalowanego pliku.</span><span class="sxs-lookup"><span data-stu-id="df8e8-132">Apply best practices when you persist information in your `$Home` directory and mounted file share.</span></span>

## <a name="use-hello-clouddrive-command"></a><span data-ttu-id="df8e8-133">Użyj hello `clouddrive` polecenia</span><span class="sxs-lookup"><span data-stu-id="df8e8-133">Use hello `clouddrive` command</span></span>
<span data-ttu-id="df8e8-134">Za pomocą powłoki w chmurze, można uruchomić polecenie o nazwie `clouddrive`, która umożliwia możesz toomanually aktualizacji hello udział pliku to jest tooCloud zainstalowanego powłoki.</span><span class="sxs-lookup"><span data-stu-id="df8e8-134">With Cloud Shell, you can run a command called `clouddrive`, which enables you toomanually update hello file share that's mounted tooCloud Shell.</span></span>
<span data-ttu-id="df8e8-135">![Uruchomienie polecenia "clouddrive" hello](media/clouddrive-h.png)</span><span class="sxs-lookup"><span data-stu-id="df8e8-135">![Running hello "clouddrive" command](media/clouddrive-h.png)</span></span>

## <a name="mount-a-new-clouddrive"></a><span data-ttu-id="df8e8-136">Zainstaluj nowy`clouddrive`</span><span class="sxs-lookup"><span data-stu-id="df8e8-136">Mount a new `clouddrive`</span></span>

### <a name="prerequisites-for-manual-mounting"></a><span data-ttu-id="df8e8-137">Wymagania wstępne dotyczące ręcznego instalowania</span><span class="sxs-lookup"><span data-stu-id="df8e8-137">Prerequisites for manual mounting</span></span>
<span data-ttu-id="df8e8-138">Można aktualizować hello udziału plików, który jest skojarzony z powłoki chmury przy użyciu hello `clouddrive mount` polecenia.</span><span class="sxs-lookup"><span data-stu-id="df8e8-138">You can update hello file share that's associated with Cloud Shell by using hello `clouddrive mount` command.</span></span>

<span data-ttu-id="df8e8-139">W przypadku instalowania istniejącego udziału pliku, muszą być hello kont magazynu:</span><span class="sxs-lookup"><span data-stu-id="df8e8-139">If you mount an existing file share, hello storage accounts must be:</span></span>
* <span data-ttu-id="df8e8-140">Magazyn lokalnie nadmiarowy lub udziałów plików magazynu geograficznie nadmiarowego toosupport.</span><span class="sxs-lookup"><span data-stu-id="df8e8-140">Locally-redundant storage or geo-redundant storage toosupport file shares.</span></span>
* <span data-ttu-id="df8e8-141">Znajduje się w danym regionie przypisane.</span><span class="sxs-lookup"><span data-stu-id="df8e8-141">Located in your assigned region.</span></span> <span data-ttu-id="df8e8-142">Podczas pracy dołączania hello region przypisane do Ciebie toois na liście Nazwa grupy zasobów hello `cloud-shell-storage-<region>`.</span><span class="sxs-lookup"><span data-stu-id="df8e8-142">When you are onboarding, hello region you are assigned toois listed in hello resource group name `cloud-shell-storage-<region>`.</span></span>

### <a name="supported-storage-regions"></a><span data-ttu-id="df8e8-143">Regiony obsługiwanego magazynu</span><span class="sxs-lookup"><span data-stu-id="df8e8-143">Supported storage regions</span></span>
<span data-ttu-id="df8e8-144">Hello Azure pliki muszą znajdować się w hello sam regionu co hello powłoki chmury maszyny, która jest instalowanie, ich.</span><span class="sxs-lookup"><span data-stu-id="df8e8-144">hello Azure files must reside in hello same region as hello Cloud Shell machine that you're mounting them to.</span></span> <span data-ttu-id="df8e8-145">Klastry powłoki chmury istnieje obecnie w następujących regionach hello:</span><span class="sxs-lookup"><span data-stu-id="df8e8-145">Cloud Shell clusters currently exist in hello following regions:</span></span>
|<span data-ttu-id="df8e8-146">Obszar</span><span class="sxs-lookup"><span data-stu-id="df8e8-146">Area</span></span>|<span data-ttu-id="df8e8-147">Region</span><span class="sxs-lookup"><span data-stu-id="df8e8-147">Region</span></span>|
|---|---|
|<span data-ttu-id="df8e8-148">Ameryki</span><span class="sxs-lookup"><span data-stu-id="df8e8-148">Americas</span></span>|<span data-ttu-id="df8e8-149">Wschodnie stany USA, południowo środkowe stany USA, zachodnie stany USA</span><span class="sxs-lookup"><span data-stu-id="df8e8-149">East US, South Central US, West US</span></span>|
|<span data-ttu-id="df8e8-150">Europa</span><span class="sxs-lookup"><span data-stu-id="df8e8-150">Europe</span></span>|<span data-ttu-id="df8e8-151">Europa Północna, Europa Zachodnia</span><span class="sxs-lookup"><span data-stu-id="df8e8-151">North Europe, West Europe</span></span>|
|<span data-ttu-id="df8e8-152">Azja i Pacyfik</span><span class="sxs-lookup"><span data-stu-id="df8e8-152">Asia Pacific</span></span>|<span data-ttu-id="df8e8-153">Indie centralnej, południowo-Azja.</span><span class="sxs-lookup"><span data-stu-id="df8e8-153">India Central, Southeast Asia</span></span>|

### <a name="hello-clouddrive-mount-command"></a><span data-ttu-id="df8e8-154">Witaj `clouddrive mount` polecenia</span><span class="sxs-lookup"><span data-stu-id="df8e8-154">hello `clouddrive mount` command</span></span>

> [!NOTE]
> <span data-ttu-id="df8e8-155">Jeśli w przypadku instalowania nowego udziału plików, nowy obraz użytkownika jest tworzona dla Twojego `$Home` katalogu, ponieważ poprzedniego `$Home` obrazu jest przechowywany w hello poprzedniej udziału plików.</span><span class="sxs-lookup"><span data-stu-id="df8e8-155">If you're mounting a new file share, a new user image is created for your `$Home` directory, because your previous `$Home` image is kept in hello previous file share.</span></span>

<span data-ttu-id="df8e8-156">Uruchom hello `clouddrive mount` z hello następujące parametry:</span><span class="sxs-lookup"><span data-stu-id="df8e8-156">Run hello `clouddrive mount` command with hello following parameters:</span></span>

```
clouddrive mount -s mySubscription -g myRG -n storageAccountName -f fileShareName
```

<span data-ttu-id="df8e8-157">tooview więcej szczegółów, uruchom `clouddrive mount -h`, jak pokazano poniżej:</span><span class="sxs-lookup"><span data-stu-id="df8e8-157">tooview more details, run `clouddrive mount -h`, as shown here:</span></span>

![Uruchomione hello "clouddrive mount'command](media/mount-h.png)

## <a name="unmount-clouddrive"></a><span data-ttu-id="df8e8-159">Odinstaluj`clouddrive`</span><span class="sxs-lookup"><span data-stu-id="df8e8-159">Unmount `clouddrive`</span></span>
<span data-ttu-id="df8e8-160">Można odinstalować udziału plików, to jest zainstalowany tooCloud powłoki w dowolnym momencie.</span><span class="sxs-lookup"><span data-stu-id="df8e8-160">You can unmount a file share that's mounted tooCloud Shell at any time.</span></span> <span data-ttu-id="df8e8-161">Po odinstalowane udziału plików będzie toomount zostanie wyświetlony monit o nowe tooyour wcześniejsze udziału pliku następnej sesji.</span><span class="sxs-lookup"><span data-stu-id="df8e8-161">Once your file share is unmounted, you will be prompted toomount a new file share prior tooyour next session.</span></span>

<span data-ttu-id="df8e8-162">tooremove pliku udziału z chmury powłoki:</span><span class="sxs-lookup"><span data-stu-id="df8e8-162">tooremove a file share from Cloud Shell:</span></span>
1. <span data-ttu-id="df8e8-163">Uruchom polecenie `clouddrive unmount`.</span><span class="sxs-lookup"><span data-stu-id="df8e8-163">Run `clouddrive unmount`.</span></span>
2. <span data-ttu-id="df8e8-164">Potwierdzić oraz potwierdzić monity hello.</span><span class="sxs-lookup"><span data-stu-id="df8e8-164">Acknowledge and confirm hello prompts.</span></span>

<span data-ttu-id="df8e8-165">Udziału plików będzie tooexist, o ile nie można usunąć ręcznie.</span><span class="sxs-lookup"><span data-stu-id="df8e8-165">Your file share will continue tooexist unless you delete it manually.</span></span> <span data-ttu-id="df8e8-166">Chmura powłoki wyszuka już ten udział plików w kolejnych sesjach.</span><span class="sxs-lookup"><span data-stu-id="df8e8-166">Cloud Shell will no longer search for this file share on subsequent sessions.</span></span>

<span data-ttu-id="df8e8-167">tooview więcej szczegółów, uruchom `clouddrive unmount -h`, jak pokazano poniżej:</span><span class="sxs-lookup"><span data-stu-id="df8e8-167">tooview more details, run `clouddrive unmount -h`, as shown here:</span></span>

![Uruchomione hello "clouddrive unmount'command](media/unmount-h.png)

> [!WARNING]
> <span data-ttu-id="df8e8-169">Uruchomienie tego polecenia nie usunie żadnych zasobów.</span><span class="sxs-lookup"><span data-stu-id="df8e8-169">Running this command will not delete any resources.</span></span> <span data-ttu-id="df8e8-170">Ręczne usunięcie grupy zasobów, konta magazynu lub udziału plików, który jest mapowany tooCloud powłoki spowoduje trwałe usunięcie z `$Home` katalogu obrazu i innych plików w udziale plików.</span><span class="sxs-lookup"><span data-stu-id="df8e8-170">Manually deleting a resource group, storage account, or file share that is mapped tooCloud Shell will permanently delete your `$Home` directory image and any other files in your file share.</span></span> <span data-ttu-id="df8e8-171">Nie można cofnąć tej akcji.</span><span class="sxs-lookup"><span data-stu-id="df8e8-171">This action cannot be undone.</span></span>

## <a name="list-clouddrive-file-shares"></a><span data-ttu-id="df8e8-172">Lista `clouddrive` udziałów plików</span><span class="sxs-lookup"><span data-stu-id="df8e8-172">List `clouddrive` file shares</span></span>
<span data-ttu-id="df8e8-173">udziału plików, który jest zainstalowany jako toodiscover `clouddrive`, uruchom następujące hello `df` polecenia.</span><span class="sxs-lookup"><span data-stu-id="df8e8-173">toodiscover which file share is mounted as `clouddrive`, run hello following `df` command.</span></span> 

<span data-ttu-id="df8e8-174">tooclouddrive ścieżka pliku Hello pokazuje Twojej nazwy konta magazynu i udziału pliku w adresie URL hello.</span><span class="sxs-lookup"><span data-stu-id="df8e8-174">hello file path tooclouddrive shows your storage account name and file share in hello URL.</span></span> <span data-ttu-id="df8e8-175">Na przykład: `//storageaccountname.file.core.windows.net/filesharename`</span><span class="sxs-lookup"><span data-stu-id="df8e8-175">For example, `//storageaccountname.file.core.windows.net/filesharename`</span></span>

```
justin@Azure:~$ df
Filesystem                                               1K-blocks     Used Available Use% Mounted on
overlay                                                   30428648 15585636  14826628  52% /
tmpfs                                                       986704        0    986704   0% /dev
tmpfs                                                       986704        0    986704   0% /sys/fs/cgroup
/dev/sda1                                                 30428648 15585636  14826628  52% /etc/hosts
shm                                                          65536        0     65536   0% /dev/shm
//mystoragename.file.core.windows.net/fileshareName        6291456  5242944   1048512  84% /usr/justin/clouddrive
/dev/loop0                                                 5160576   601652   4296780  13% /home/justin
```

## <a name="transfer-local-files-toocloud-shell"></a><span data-ttu-id="df8e8-176">Transfer plików lokalnych tooCloud powłoki</span><span class="sxs-lookup"><span data-stu-id="df8e8-176">Transfer local files tooCloud Shell</span></span>
<span data-ttu-id="df8e8-177">Witaj `clouddrive` katalogu synchronizacje z hello bloku magazynu z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="df8e8-177">hello `clouddrive` directory syncs with hello Azure portal storage blade.</span></span> <span data-ttu-id="df8e8-178">Użyj tego bloku tootransfer lokalne pliki tooor z udziału plików.</span><span class="sxs-lookup"><span data-stu-id="df8e8-178">Use this blade tootransfer local files tooor from your file share.</span></span> <span data-ttu-id="df8e8-179">Aktualizowanie plików z poziomu powłoki chmury jest widoczny w hello magazyn plików graficznego interfejsu użytkownika podczas odświeżania bloku hello.</span><span class="sxs-lookup"><span data-stu-id="df8e8-179">Updating files from within Cloud Shell is reflected in hello file storage GUI when you refresh hello blade.</span></span>

### <a name="download-files"></a><span data-ttu-id="df8e8-180">Pobieranie plików</span><span class="sxs-lookup"><span data-stu-id="df8e8-180">Download files</span></span>

![Lista plików lokalnych](media/download.png)
1. <span data-ttu-id="df8e8-182">W hello portalu Azure Przejdź toohello udziału zainstalowanego pliku.</span><span class="sxs-lookup"><span data-stu-id="df8e8-182">In hello Azure portal, go toohello mounted file share.</span></span>
2. <span data-ttu-id="df8e8-183">Wybierz plik docelowy hello.</span><span class="sxs-lookup"><span data-stu-id="df8e8-183">Select hello target file.</span></span>
3. <span data-ttu-id="df8e8-184">Wybierz hello **Pobierz** przycisku.</span><span class="sxs-lookup"><span data-stu-id="df8e8-184">Select hello **Download** button.</span></span>

### <a name="upload-files"></a><span data-ttu-id="df8e8-185">Przekazywanie plików</span><span class="sxs-lookup"><span data-stu-id="df8e8-185">Upload files</span></span>

![Przekazane toobe plików lokalnych](media/upload.png)
1. <span data-ttu-id="df8e8-187">Przejdź tooyour zainstalowanego udziału plików.</span><span class="sxs-lookup"><span data-stu-id="df8e8-187">Go tooyour mounted file share.</span></span>
2. <span data-ttu-id="df8e8-188">Wybierz hello **przekazać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="df8e8-188">Select hello **Upload** button.</span></span>
3. <span data-ttu-id="df8e8-189">Wybierz plik hello lub pliki, które mają tooupload.</span><span class="sxs-lookup"><span data-stu-id="df8e8-189">Select hello file or files that you want tooupload.</span></span>
4. <span data-ttu-id="df8e8-190">Upewnij się, Przekaż hello.</span><span class="sxs-lookup"><span data-stu-id="df8e8-190">Confirm hello upload.</span></span>

<span data-ttu-id="df8e8-191">Powinien zostać wyświetlony hello pliki, które są dostępne w Twojej `clouddrive` katalogu w chmurze powłoki.</span><span class="sxs-lookup"><span data-stu-id="df8e8-191">You should now see hello files that are accessible in your `clouddrive` directory in Cloud Shell.</span></span>

## <a name="next-steps"></a><span data-ttu-id="df8e8-192">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="df8e8-192">Next steps</span></span>
[<span data-ttu-id="df8e8-193">Szybki Start powłoki chmury</span><span class="sxs-lookup"><span data-stu-id="df8e8-193">Cloud Shell Quickstart</span></span>](quickstart.md) <br><span data-ttu-id="df8e8-194">
[Więcej informacji na temat usługi Magazyn plików Azure](https://docs.microsoft.com/azure/storage/storage-introduction#file-storage)</span><span class="sxs-lookup"><span data-stu-id="df8e8-194">
[Learn about Azure File storage](https://docs.microsoft.com/azure/storage/storage-introduction#file-storage)</span></span> <br><span data-ttu-id="df8e8-195">
[Więcej informacji na temat tagów magazynu](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-using-tags)</span><span class="sxs-lookup"><span data-stu-id="df8e8-195">
[Learn about storage tags](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-using-tags)</span></span> <br>
