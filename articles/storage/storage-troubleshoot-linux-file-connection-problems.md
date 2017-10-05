---
title: "Rozwiązywanie problemów magazyn plików Azure w systemie Linux | Dokumentacja firmy Microsoft"
description: "Rozwiązywanie problemów magazyn plików Azure w systemie Linux"
services: storage
documentationcenter: 
author: genlin
manager: willchen
editor: na
tags: storage
ms.service: storage
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: genli
ms.openlocfilehash: 62cd62ec3a2900f06acacc0852a48b5e3ff1c8cd
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="troubleshoot-azure-file-storage-problems-in-linux"></a><span data-ttu-id="96936-103">Rozwiązywanie problemów magazyn plików Azure w systemie Linux</span><span class="sxs-lookup"><span data-stu-id="96936-103">Troubleshoot Azure File storage problems in Linux</span></span>

<span data-ttu-id="96936-104">W tym artykule wymieniono typowe problemy, które są związane z magazyn plików Microsoft Azure, podczas łączenia z klientów systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="96936-104">This article lists common problems that are related to Microsoft Azure File storage when you connect from Linux clients.</span></span> <span data-ttu-id="96936-105">Zapewnia także możliwe przyczyny i rozwiązania tych problemów.</span><span class="sxs-lookup"><span data-stu-id="96936-105">It also provides possible causes and resolutions for these problems.</span></span>

<a id="permissiondenied"></a>
## <a name="permission-denied-disk-quota-exceeded-when-you-try-to-open-a-file"></a><span data-ttu-id="96936-106">"Przekroczono przydział dysku [odmówiono uprawnienia]" podczas próby otwarcia pliku</span><span class="sxs-lookup"><span data-stu-id="96936-106">"[permission denied] Disk quota exceeded" when you try to open a file</span></span>

<span data-ttu-id="96936-107">W systemie Linux pojawi się komunikat o błędzie podobny do następującego:</span><span class="sxs-lookup"><span data-stu-id="96936-107">In Linux, you receive an error message that resembles the following:</span></span>

<span data-ttu-id="96936-108">**<filename>[odmówiono uprawnienia] Przekroczono przydział dysku**</span><span class="sxs-lookup"><span data-stu-id="96936-108">**<filename> [permission denied] Disk quota exceeded**</span></span>

### <a name="cause"></a><span data-ttu-id="96936-109">Przyczyna</span><span class="sxs-lookup"><span data-stu-id="96936-109">Cause</span></span>

<span data-ttu-id="96936-110">Osiągnięto górny limit współbieżnych otwartych dojść, które są dozwolone dla pliku.</span><span class="sxs-lookup"><span data-stu-id="96936-110">You have reached the upper limit of concurrent open handles that are allowed for a file.</span></span>

### <a name="solution"></a><span data-ttu-id="96936-111">Rozwiązanie</span><span class="sxs-lookup"><span data-stu-id="96936-111">Solution</span></span>

<span data-ttu-id="96936-112">Zmniejszyć liczbę jednoczesnych otwartych dojść zamykając niektóre dojść, a następnie spróbuj ponownie wykonać operację.</span><span class="sxs-lookup"><span data-stu-id="96936-112">Reduce the number of concurrent open handles by closing some handles, and then retry the operation.</span></span> <span data-ttu-id="96936-113">Aby uzyskać więcej informacji, zobacz [Lista kontrolna wydajności i skalowalności magazynu Microsoft Azure](storage-performance-checklist.md).</span><span class="sxs-lookup"><span data-stu-id="96936-113">For more information, see [Microsoft Azure Storage performance and scalability checklist](storage-performance-checklist.md).</span></span>

<a id="slowfilecopying"></a>
## <a name="slow-file-copying-to-and-from-azure-file-storage-in-linux"></a><span data-ttu-id="96936-114">Powolna kopiowanie plików do i z usługi Magazyn plików Azure w systemie Linux</span><span class="sxs-lookup"><span data-stu-id="96936-114">Slow file copying to and from Azure File storage in Linux</span></span>

-   <span data-ttu-id="96936-115">Jeśli użytkownik nie ma określonego minimalny wymagany rozmiar operacji We/Wy, zalecane jest użycie 1 MB jako rozmiaru we/wy do uzyskania optymalnej wydajności.</span><span class="sxs-lookup"><span data-stu-id="96936-115">If you don’t have a specific minimum I/O size requirement, we recommend that you use 1 MB as the I/O size for optimal performance.</span></span>
-   <span data-ttu-id="96936-116">Jeśli znasz końcowego rozmiar pliku, który powiększa się przy użyciu operacji zapisu, a oprogramowania nie występują problemy ze zgodnością, podczas niezapisanych tail na plik zawiera zera, następnie ustaw rozmiar pliku z wyprzedzeniem zamiast wprowadzania każdego zapisu rozszerzanie zapisu.</span><span class="sxs-lookup"><span data-stu-id="96936-116">If you know the final size of a file that you are extending by using writes, and your software doesn’t experience compatibility problems when an unwritten tail on the file contains zeros, then set the file size in advance instead of making every write an extending write.</span></span>
-   <span data-ttu-id="96936-117">Użyj metody copy prawa:</span><span class="sxs-lookup"><span data-stu-id="96936-117">Use the right copy method:</span></span>
    -   <span data-ttu-id="96936-118">Użyj [AzCopy](storage-use-azcopy.md#file-copy) żadnych transferu między dwoma udziałami plików.</span><span class="sxs-lookup"><span data-stu-id="96936-118">Use [AzCopy](storage-use-azcopy.md#file-copy) for any transfer between two file shares.</span></span>
    -   <span data-ttu-id="96936-119">Użyj [Robocopy](https://blogs.msdn.microsoft.com/granth/2009/12/07/multi-threaded-robocopy-for-faster-copies/) między udziałami plików na komputerze lokalnym.</span><span class="sxs-lookup"><span data-stu-id="96936-119">Use [Robocopy](https://blogs.msdn.microsoft.com/granth/2009/12/07/multi-threaded-robocopy-for-faster-copies/) between file shares on an on-premises computer.</span></span>

<a id="error112"></a>
## <a name="mount-error112-host-is-down-because-of-a-reconnection-time-out"></a><span data-ttu-id="96936-120">"Instalowanie error(112): Host nie działa" z powodu limitu ponowne nawiązanie połączenia</span><span class="sxs-lookup"><span data-stu-id="96936-120">"Mount error(112): Host is down" because of a reconnection time-out</span></span>

<span data-ttu-id="96936-121">Błąd instalacji "112" występuje na komputerze klienckim systemu Linux, gdy klient był bezczynny przez długi czas.</span><span class="sxs-lookup"><span data-stu-id="96936-121">A "112" mount error occurs on the Linux client when the client has been idle for a long time.</span></span> <span data-ttu-id="96936-122">Po dłuższy czas bezczynności klient odłączy się i limit czasu połączenia.</span><span class="sxs-lookup"><span data-stu-id="96936-122">After extended idle time, the client disconnects and the connection times out.</span></span>  

### <a name="cause"></a><span data-ttu-id="96936-123">Przyczyna</span><span class="sxs-lookup"><span data-stu-id="96936-123">Cause</span></span>

<span data-ttu-id="96936-124">Połączenie może być bezczynne z następujących powodów:</span><span class="sxs-lookup"><span data-stu-id="96936-124">The connection can be idle for the following reasons:</span></span>

-   <span data-ttu-id="96936-125">Błędy komunikacji sieciowej uniemożliwiające ponowne ustanowienie połączenie TCP z serwerem, gdy jest używana opcja instalacji "ciąg soft" domyślne</span><span class="sxs-lookup"><span data-stu-id="96936-125">Network communication failures that prevent re-establishing a TCP connection to the server when the default “soft” mount option is used</span></span>
-   <span data-ttu-id="96936-126">Najnowsze poprawki ponowne nawiązanie połączenia, które nie są obecne w starszych jądra</span><span class="sxs-lookup"><span data-stu-id="96936-126">Recent reconnection fixes that are not present in older kernels</span></span>

### <a name="solution"></a><span data-ttu-id="96936-127">Rozwiązanie</span><span class="sxs-lookup"><span data-stu-id="96936-127">Solution</span></span>

<span data-ttu-id="96936-128">To ponowne nawiązanie połączenia jądra systemu Linux teraz problemu w ramach następujących zmian:</span><span class="sxs-lookup"><span data-stu-id="96936-128">This reconnection problem in the Linux kernel is now fixed as part of the following changes:</span></span>

- [<span data-ttu-id="96936-129">Poprawka nawiązywać nie mają być odroczone sesji protokołu smb3 ponownie gdy ponownego połączenia gniazda</span><span class="sxs-lookup"><span data-stu-id="96936-129">Fix reconnect to not defer smb3 session reconnect long after socket reconnect</span></span>](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/fs/cifs?id=4fcd1813e6404dd4420c7d12fb483f9320f0bf93)
-   [<span data-ttu-id="96936-130">Wywołanie usługi echo natychmiast po ponownego połączenia gniazda</span><span class="sxs-lookup"><span data-stu-id="96936-130">Call echo service immediately after socket reconnect</span></span>](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/?id=b8c600120fc87d53642476f48c8055b38d6e14c7)
-   [<span data-ttu-id="96936-131">CIFS: Naprawić uszkodzenie pamięci możliwe podczas ponownego nawiązania połączenia</span><span class="sxs-lookup"><span data-stu-id="96936-131">CIFS: Fix a possible memory corruption during reconnect</span></span>](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/commit/?id=53e0e11efe9289535b060a51d4cf37c25e0d0f2b)
-   [<span data-ttu-id="96936-132">CIFS: Usuń możliwe podwójne blokowanie obiektu mutex podczas ponownego nawiązania połączenia (dla jądra v4.9 i nowsze)</span><span class="sxs-lookup"><span data-stu-id="96936-132">CIFS: Fix a possible double locking of mutex during reconnect (for kernel v4.9 and later)</span></span>](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/commit/?id=96a988ffeb90dba33a71c3826086fe67c897a183)

<span data-ttu-id="96936-133">Jednak te zmiany mogą nie być przenoszone jeszcze do wszystkich dystrybucje systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="96936-133">However, these changes might not be ported yet to all the Linux distributions.</span></span> <span data-ttu-id="96936-134">Ta poprawka i inne poprawki ponowne nawiązanie połączenia są wprowadzane w następujących popularnych jądra systemu Linux: 4.4.40, 4.8.16 i 4.9.1.</span><span class="sxs-lookup"><span data-stu-id="96936-134">This fix and other reconnection fixes are made in the following popular Linux kernels: 4.4.40, 4.8.16, and 4.9.1.</span></span> <span data-ttu-id="96936-135">Ta poprawka można uzyskać przez uaktualnienie do wersji zalecane jądra.</span><span class="sxs-lookup"><span data-stu-id="96936-135">You can get this fix by upgrading to one of these recommended kernel versions.</span></span>

### <a name="workaround"></a><span data-ttu-id="96936-136">Obejście problemu</span><span class="sxs-lookup"><span data-stu-id="96936-136">Workaround</span></span>

<span data-ttu-id="96936-137">Ten problem można obejść, określając instalacji twardej.</span><span class="sxs-lookup"><span data-stu-id="96936-137">You can work around this problem by specifying a hard mount.</span></span> <span data-ttu-id="96936-138">Dzięki temu klient czekać do momentu jest nawiązywane połączenie lub go jawnie zostanie przerwane i pozwala uniknąć błędów z powodu limitów czasu w sieci.</span><span class="sxs-lookup"><span data-stu-id="96936-138">This forces the client to wait until a connection is established or until it’s explicitly interrupted and can be used to prevent errors because of network time-outs.</span></span> <span data-ttu-id="96936-139">To rozwiązanie może jednak spowodować nieograniczonego oczekiwania.</span><span class="sxs-lookup"><span data-stu-id="96936-139">However, this workaround might cause indefinite waits.</span></span> <span data-ttu-id="96936-140">Przygotuj się do zatrzymania połączenia w razie potrzeby.</span><span class="sxs-lookup"><span data-stu-id="96936-140">Be prepared to stop connections as necessary.</span></span>

<span data-ttu-id="96936-141">Jeśli nie można uaktualnić do najnowszej wersji jądra, można obejść ten problem, przechowując pliku w udziale plików na platformę Azure, który można zapisać co 30 sekund lub mniej.</span><span class="sxs-lookup"><span data-stu-id="96936-141">If you cannot upgrade to the latest kernel versions, you can work around this problem by keeping a file in the Azure file share that you write to every 30 seconds or less.</span></span> <span data-ttu-id="96936-142">Musi to być operacji zapisu, takie jak ponowne zapisywanie Data utworzone lub zmodyfikowane na plik.</span><span class="sxs-lookup"><span data-stu-id="96936-142">This must be a write operation, such as rewriting the created or modified date on the file.</span></span> <span data-ttu-id="96936-143">W przeciwnym razie może uzyskiwać wyniki z pamięci podręcznej, a operacja nie może wyzwolić ponowne połączenie.</span><span class="sxs-lookup"><span data-stu-id="96936-143">Otherwise, you might get cached results, and your operation might not trigger the reconnection.</span></span>

<a id="error115"></a>
## <a name="mount-error115-operation-now-in-progress-when-you-mount-azure-file-storage-by-using-smb-30"></a><span data-ttu-id="96936-144">"Instalowanie error(115): operacja w toku" podczas instalowania usługi Magazyn plików Azure przy użyciu protokołu SMB 3.0</span><span class="sxs-lookup"><span data-stu-id="96936-144">"Mount error(115): Operation now in progress" when you mount Azure File storage by using SMB 3.0</span></span>

### <a name="cause"></a><span data-ttu-id="96936-145">Przyczyna</span><span class="sxs-lookup"><span data-stu-id="96936-145">Cause</span></span>

<span data-ttu-id="96936-146">Niektóre dystrybucje systemu Linux nie jest jeszcze obsługiwany funkcji szyfrowania protokołu SMB 3.0 i użytkowników może zostać wyświetlony komunikat o błędzie "115", jeśli próby instalacji usługi Azure File storage przy użyciu protokołu SMB 3.0 ze względu na Brak funkcji.</span><span class="sxs-lookup"><span data-stu-id="96936-146">Some Linux distributions do not yet support encryption features in SMB 3.0 and users might receive a "115" error message if they try to mount Azure File storage by using SMB 3.0 because of a missing feature.</span></span>

### <a name="solution"></a><span data-ttu-id="96936-147">Rozwiązanie</span><span class="sxs-lookup"><span data-stu-id="96936-147">Solution</span></span>

<span data-ttu-id="96936-148">Funkcja szyfrowania protokołu SMB 3.0 dla systemu Linux została wprowadzona w 4.11 jądra.</span><span class="sxs-lookup"><span data-stu-id="96936-148">Encryption feature for SMB 3.0 for Linux was introduced in 4.11 kernel.</span></span> <span data-ttu-id="96936-149">Ta funkcja umożliwia instalowanie udziału plików platformy Azure z lokalnej lub w innym regionie Azure.</span><span class="sxs-lookup"><span data-stu-id="96936-149">This feature enables mounting of Azure File share from on-premises or a different Azure region.</span></span> <span data-ttu-id="96936-150">Podczas publikowania ta funkcja została backported Ubuntu 17.04 i Ubuntu 16.10.</span><span class="sxs-lookup"><span data-stu-id="96936-150">At the time of publishing, this functionality has been backported to Ubuntu 17.04 and Ubuntu 16.10.</span></span> <span data-ttu-id="96936-151">Jeśli klienta SMB systemu Linux nie obsługuje szyfrowania, należy zainstalować magazyn plików Azure przy użyciu protokołu SMB 2.1 z maszyny Wirtualnej systemu Linux platformy Azure, który znajduje się w tym samym centrum danych, co konto magazynu plików.</span><span class="sxs-lookup"><span data-stu-id="96936-151">If your Linux SMB client does not support encryption, mount Azure File storage by using SMB 2.1 from an Azure Linux VM that's in the same datacenter as the File storage account.</span></span>

<a id="slowperformance"></a>
## <a name="slow-performance-on-an-azure-file-share-mounted-on-a-linux-vm"></a><span data-ttu-id="96936-152">Niska wydajność w udziale plików na platformę Azure zainstalowane na maszynie Wirtualnej systemu Linux</span><span class="sxs-lookup"><span data-stu-id="96936-152">Slow performance on an Azure file share mounted on a Linux VM</span></span>

### <a name="cause"></a><span data-ttu-id="96936-153">Przyczyna</span><span class="sxs-lookup"><span data-stu-id="96936-153">Cause</span></span>

<span data-ttu-id="96936-154">Jedną z możliwych przyczyn niską wydajność jest wyłączone buforowanie.</span><span class="sxs-lookup"><span data-stu-id="96936-154">One possible cause of slow performance is disabled caching.</span></span>

### <a name="solution"></a><span data-ttu-id="96936-155">Rozwiązanie</span><span class="sxs-lookup"><span data-stu-id="96936-155">Solution</span></span>

<span data-ttu-id="96936-156">Aby sprawdzić, czy buforowanie jest wyłączone, należy wyszukać **pamięci podręcznej =** wpisu.</span><span class="sxs-lookup"><span data-stu-id="96936-156">To check whether caching is disabled, look for the **cache=** entry.</span></span> 

<span data-ttu-id="96936-157">**Pamięć podręczna = Brak** wskazuje, że buforowanie jest wyłączone.</span><span class="sxs-lookup"><span data-stu-id="96936-157">**Cache=none** indicates that caching is disabled.</span></span>  <span data-ttu-id="96936-158">Zainstaluj udziału za pomocą polecenia instalacji domyślnej lub jawnie dodając **pamięci podręcznej = strict** jest włączona opcja instalacji polecenie, aby zapewnić tym buforowanie domyślne lub "strict" tryb buforowania.</span><span class="sxs-lookup"><span data-stu-id="96936-158">Remount the share by using the default mount command or by explicitly adding the **cache=strict** option to the mount command to ensure that default caching or "strict" caching mode is enabled.</span></span>

<span data-ttu-id="96936-159">W niektórych scenariuszach **serverino** opcji instalacji może spowodować **ls** polecenie do uruchomienia stat dla każdego wpisu w katalogu.</span><span class="sxs-lookup"><span data-stu-id="96936-159">In some scenarios, the **serverino** mount option can cause the **ls** command to run stat against every directory entry.</span></span> <span data-ttu-id="96936-160">Ten problem powoduje spadek wydajności podczas jest wyświetlania katalogu duży.</span><span class="sxs-lookup"><span data-stu-id="96936-160">This behavior results in performance degradation when you're listing a big directory.</span></span> <span data-ttu-id="96936-161">Opcje instalacji można sprawdzić Twojej **/etc/fstab** wpis:</span><span class="sxs-lookup"><span data-stu-id="96936-161">You can check the mount options in your **/etc/fstab** entry:</span></span>

`//azureuser.file.core.windows.net/cifs /cifs cifs vers=3.0,serverino,username=xxx,password=xxx,dir_mode=0777,file_mode=0777`

<span data-ttu-id="96936-162">Możesz również sprawdzić, czy prawidłowe opcje są używane przez uruchomienie **instalacji sudo | grep cifs** polecenia i sprawdzanie danych wyjściowych, takie jak następujące przykładowe dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="96936-162">You can also check whether the correct options are being used by running the  **sudo mount | grep cifs** command and checking its output, such as the following example output:</span></span>

`//mabiccacifs.file.core.windows.net/cifs on /cifs type cifs (rw,relatime,vers=3.0,sec=ntlmssp,cache=strict,username=xxx,domain=X,uid=0,noforceuid,gid=0,noforcegid,addr=192.168.10.1,file_mode=0777, dir_mode=0777,persistenthandles,nounix,serverino,mapposix,rsize=1048576,wsize=1048576,actimeo=1)`

<span data-ttu-id="96936-163">Jeśli **pamięci podręcznej = strict** lub **serverino** opcja jest nie istnieje, odinstaluj i ponownie zainstalować magazyn plików Azure za pomocą polecenia instalacji z [dokumentacji](storage-how-to-use-files-linux.md).</span><span class="sxs-lookup"><span data-stu-id="96936-163">If the **cache=strict** or **serverino** option is not present, unmount and mount Azure File storage again by running the mount command from the [documentation](storage-how-to-use-files-linux.md).</span></span> <span data-ttu-id="96936-164">Następnie, która ponownie **/etc/fstab** wpis ma prawidłowe opcje.</span><span class="sxs-lookup"><span data-stu-id="96936-164">Then, recheck that the **/etc/fstab** entry has the correct options.</span></span>

<a id="timestampslost"></a>
## <a name="time-stamps-were-lost-in-copying-files-from-windows-to-linux"></a><span data-ttu-id="96936-165">Sygnatury czasowe zostały utracone podczas kopiowania plików z systemu Windows do systemu Linux</span><span class="sxs-lookup"><span data-stu-id="96936-165">Time stamps were lost in copying files from Windows to Linux</span></span>

<span data-ttu-id="96936-166">Na platformach systemu Linux/Unix **cp -p** polecenie kończy się niepowodzeniem, jeśli plik 1 i 2 plików należą do firmy przez różnych użytkowników.</span><span class="sxs-lookup"><span data-stu-id="96936-166">On Linux/Unix platforms, the **cp -p** command fails if file 1 and file 2 are owned by different users.</span></span>

### <a name="cause"></a><span data-ttu-id="96936-167">Przyczyna</span><span class="sxs-lookup"><span data-stu-id="96936-167">Cause</span></span>

<span data-ttu-id="96936-168">Flagi force **f** w COPYFILE powoduje wykonywania **cp -p -f** w systemie Unix.</span><span class="sxs-lookup"><span data-stu-id="96936-168">The force flag **f** in COPYFILE results in executing **cp -p -f** on Unix.</span></span> <span data-ttu-id="96936-169">To polecenie nie powiedzie się także zachować sygnatury czasowej pliku, który nie jesteś właścicielem.</span><span class="sxs-lookup"><span data-stu-id="96936-169">This command also fails to preserve the time stamp of the file that you don't own.</span></span>

### <a name="workaround"></a><span data-ttu-id="96936-170">Obejście problemu</span><span class="sxs-lookup"><span data-stu-id="96936-170">Workaround</span></span>

<span data-ttu-id="96936-171">Użyj użytkownika konta magazynu do kopiowania plików:</span><span class="sxs-lookup"><span data-stu-id="96936-171">Use the storage account user for copying the files:</span></span>

- `Useadd : [storage account name]`
- `Passwd [storage account name]`
- `Su [storage account name]`
- `Cp -p filename.txt /share`

## <a name="need-help-contact-support"></a><span data-ttu-id="96936-172">Potrzebujesz pomocy?</span><span class="sxs-lookup"><span data-stu-id="96936-172">Need help?</span></span> <span data-ttu-id="96936-173">Skontaktuj się z pomocą techniczną.</span><span class="sxs-lookup"><span data-stu-id="96936-173">Contact support.</span></span>

<span data-ttu-id="96936-174">Jeśli nadal potrzebujesz pomocy, [się z pomocą techniczną](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) uzyskać szybkie rozwiązanie problemu.</span><span class="sxs-lookup"><span data-stu-id="96936-174">If you still need help, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) to get your problem resolved quickly.</span></span>
