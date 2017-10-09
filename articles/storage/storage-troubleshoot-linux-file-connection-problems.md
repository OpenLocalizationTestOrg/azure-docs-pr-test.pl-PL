---
title: "aaaTroubleshoot problemów z magazynu plików Azure w systemie Linux | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 3dc537d714244451a5ff8e01f4a27f03873cf2fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-file-storage-problems-in-linux"></a><span data-ttu-id="62043-103">Rozwiązywanie problemów magazyn plików Azure w systemie Linux</span><span class="sxs-lookup"><span data-stu-id="62043-103">Troubleshoot Azure File storage problems in Linux</span></span>

<span data-ttu-id="62043-104">W tym artykule wymieniono typowe problemy, które są powiązane tooMicrosoft magazyn plików Azure po ustanowieniu połączenia od klientów systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="62043-104">This article lists common problems that are related tooMicrosoft Azure File storage when you connect from Linux clients.</span></span> <span data-ttu-id="62043-105">Zapewnia także możliwe przyczyny i rozwiązania tych problemów.</span><span class="sxs-lookup"><span data-stu-id="62043-105">It also provides possible causes and resolutions for these problems.</span></span>

<a id="permissiondenied"></a>
## <a name="permission-denied-disk-quota-exceeded-when-you-try-tooopen-a-file"></a><span data-ttu-id="62043-106">"Przekroczono przydział dysku [odmówiono uprawnienia]" podczas próby tooopen pliku</span><span class="sxs-lookup"><span data-stu-id="62043-106">"[permission denied] Disk quota exceeded" when you try tooopen a file</span></span>

<span data-ttu-id="62043-107">W systemie Linux pojawi się komunikat o błędzie podobny hello następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="62043-107">In Linux, you receive an error message that resembles hello following:</span></span>

<span data-ttu-id="62043-108">**<filename>[odmówiono uprawnienia] Przekroczono przydział dysku**</span><span class="sxs-lookup"><span data-stu-id="62043-108">**<filename> [permission denied] Disk quota exceeded**</span></span>

### <a name="cause"></a><span data-ttu-id="62043-109">Przyczyna</span><span class="sxs-lookup"><span data-stu-id="62043-109">Cause</span></span>

<span data-ttu-id="62043-110">Osiągnięto hello górny limit współbieżnych otwartych dojść, które są dozwolone dla pliku.</span><span class="sxs-lookup"><span data-stu-id="62043-110">You have reached hello upper limit of concurrent open handles that are allowed for a file.</span></span>

### <a name="solution"></a><span data-ttu-id="62043-111">Rozwiązanie</span><span class="sxs-lookup"><span data-stu-id="62043-111">Solution</span></span>

<span data-ttu-id="62043-112">Ograniczenia hello liczby równoczesnych otwartych dojść zamykając niektóre dojść, a następnie ponów operację hello.</span><span class="sxs-lookup"><span data-stu-id="62043-112">Reduce hello number of concurrent open handles by closing some handles, and then retry hello operation.</span></span> <span data-ttu-id="62043-113">Aby uzyskać więcej informacji, zobacz [Lista kontrolna wydajności i skalowalności magazynu Microsoft Azure](storage-performance-checklist.md).</span><span class="sxs-lookup"><span data-stu-id="62043-113">For more information, see [Microsoft Azure Storage performance and scalability checklist](storage-performance-checklist.md).</span></span>

<a id="slowfilecopying"></a>
## <a name="slow-file-copying-tooand-from-azure-file-storage-in-linux"></a><span data-ttu-id="62043-114">Powolne pliku kopiowanie tooand z usługi Magazyn plików Azure w systemie Linux</span><span class="sxs-lookup"><span data-stu-id="62043-114">Slow file copying tooand from Azure File storage in Linux</span></span>

-   <span data-ttu-id="62043-115">Jeśli użytkownik nie ma określonego minimalny wymagany rozmiar operacji We/Wy, zalecane jest użycie 1 MB, ponieważ hello rozmiaru we/wy, aby zapewnić optymalną wydajność.</span><span class="sxs-lookup"><span data-stu-id="62043-115">If you don’t have a specific minimum I/O size requirement, we recommend that you use 1 MB as hello I/O size for optimal performance.</span></span>
-   <span data-ttu-id="62043-116">Jeśli znasz hello rozmiaru końcowego, pliku, który powiększa się przy użyciu operacji zapisu, a oprogramowania nie występują problemy ze zgodnością, podczas niezapisanych tail hello pliku zawiera zera, ustaw rozmiar pliku hello wcześniej zamiast wprowadzania każdego zapisu rozszerzanie zapis.</span><span class="sxs-lookup"><span data-stu-id="62043-116">If you know hello final size of a file that you are extending by using writes, and your software doesn’t experience compatibility problems when an unwritten tail on hello file contains zeros, then set hello file size in advance instead of making every write an extending write.</span></span>
-   <span data-ttu-id="62043-117">Użyj metody copy prawo hello:</span><span class="sxs-lookup"><span data-stu-id="62043-117">Use hello right copy method:</span></span>
    -   <span data-ttu-id="62043-118">Użyj [AzCopy](storage-use-azcopy.md#file-copy) żadnych transferu między dwoma udziałami plików.</span><span class="sxs-lookup"><span data-stu-id="62043-118">Use [AzCopy](storage-use-azcopy.md#file-copy) for any transfer between two file shares.</span></span>
    -   <span data-ttu-id="62043-119">Użyj [Robocopy](https://blogs.msdn.microsoft.com/granth/2009/12/07/multi-threaded-robocopy-for-faster-copies/) między udziałami plików na komputerze lokalnym.</span><span class="sxs-lookup"><span data-stu-id="62043-119">Use [Robocopy](https://blogs.msdn.microsoft.com/granth/2009/12/07/multi-threaded-robocopy-for-faster-copies/) between file shares on an on-premises computer.</span></span>

<a id="error112"></a>
## <a name="mount-error112-host-is-down-because-of-a-reconnection-time-out"></a><span data-ttu-id="62043-120">"Instalowanie error(112): Host nie działa" z powodu limitu ponowne nawiązanie połączenia</span><span class="sxs-lookup"><span data-stu-id="62043-120">"Mount error(112): Host is down" because of a reconnection time-out</span></span>

<span data-ttu-id="62043-121">Błąd instalacji "112" występuje na powitania klienta systemu Linux, gdy długo powitania klienta.</span><span class="sxs-lookup"><span data-stu-id="62043-121">A "112" mount error occurs on hello Linux client when hello client has been idle for a long time.</span></span> <span data-ttu-id="62043-122">Po dłuższy czas bezczynności rozłączy powitania klienta i limit czasu połączenia hello.</span><span class="sxs-lookup"><span data-stu-id="62043-122">After extended idle time, hello client disconnects and hello connection times out.</span></span>  

### <a name="cause"></a><span data-ttu-id="62043-123">Przyczyna</span><span class="sxs-lookup"><span data-stu-id="62043-123">Cause</span></span>

<span data-ttu-id="62043-124">Witaj połączenia może być bezczynne dla hello z następujących powodów:</span><span class="sxs-lookup"><span data-stu-id="62043-124">hello connection can be idle for hello following reasons:</span></span>

-   <span data-ttu-id="62043-125">Błędy komunikacji sieci, które uniemożliwiają ponowne ustanowienie serwer toohello połączenia TCP, gdy jest używana opcja instalacji "ciąg soft" domyślne hello</span><span class="sxs-lookup"><span data-stu-id="62043-125">Network communication failures that prevent re-establishing a TCP connection toohello server when hello default “soft” mount option is used</span></span>
-   <span data-ttu-id="62043-126">Najnowsze poprawki ponowne nawiązanie połączenia, które nie są obecne w starszych jądra</span><span class="sxs-lookup"><span data-stu-id="62043-126">Recent reconnection fixes that are not present in older kernels</span></span>

### <a name="solution"></a><span data-ttu-id="62043-127">Rozwiązanie</span><span class="sxs-lookup"><span data-stu-id="62043-127">Solution</span></span>

<span data-ttu-id="62043-128">To ponowne nawiązanie połączenia jądra systemu Linux hello teraz problemu jako część hello następujące zmiany:</span><span class="sxs-lookup"><span data-stu-id="62043-128">This reconnection problem in hello Linux kernel is now fixed as part of hello following changes:</span></span>

- [<span data-ttu-id="62043-129">Poprawka ponownie toonot odroczenie sesji protokołu smb3 ponownie gdy ponownego połączenia gniazda</span><span class="sxs-lookup"><span data-stu-id="62043-129">Fix reconnect toonot defer smb3 session reconnect long after socket reconnect</span></span>](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/fs/cifs?id=4fcd1813e6404dd4420c7d12fb483f9320f0bf93)
-   [<span data-ttu-id="62043-130">Wywołanie usługi echo natychmiast po ponownego połączenia gniazda</span><span class="sxs-lookup"><span data-stu-id="62043-130">Call echo service immediately after socket reconnect</span></span>](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/?id=b8c600120fc87d53642476f48c8055b38d6e14c7)
-   [<span data-ttu-id="62043-131">CIFS: Naprawić uszkodzenie pamięci możliwe podczas ponownego nawiązania połączenia</span><span class="sxs-lookup"><span data-stu-id="62043-131">CIFS: Fix a possible memory corruption during reconnect</span></span>](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/commit/?id=53e0e11efe9289535b060a51d4cf37c25e0d0f2b)
-   [<span data-ttu-id="62043-132">CIFS: Usuń możliwe podwójne blokowanie obiektu mutex podczas ponownego nawiązania połączenia (dla jądra v4.9 i nowsze)</span><span class="sxs-lookup"><span data-stu-id="62043-132">CIFS: Fix a possible double locking of mutex during reconnect (for kernel v4.9 and later)</span></span>](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/commit/?id=96a988ffeb90dba33a71c3826086fe67c897a183)

<span data-ttu-id="62043-133">Jednak te zmiany nie mogą być przenoszone, jeszcze tooall hello dystrybucje systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="62043-133">However, these changes might not be ported yet tooall hello Linux distributions.</span></span> <span data-ttu-id="62043-134">Ta poprawka i inne poprawki ponowne nawiązanie połączenia są wprowadzane w powitania po popularnych jądra systemu Linux: 4.4.40, 4.8.16 i 4.9.1.</span><span class="sxs-lookup"><span data-stu-id="62043-134">This fix and other reconnection fixes are made in hello following popular Linux kernels: 4.4.40, 4.8.16, and 4.9.1.</span></span> <span data-ttu-id="62043-135">Ta poprawka można uzyskać przez uaktualnienie tooone te wersje zalecane jądra.</span><span class="sxs-lookup"><span data-stu-id="62043-135">You can get this fix by upgrading tooone of these recommended kernel versions.</span></span>

### <a name="workaround"></a><span data-ttu-id="62043-136">Obejście problemu</span><span class="sxs-lookup"><span data-stu-id="62043-136">Workaround</span></span>

<span data-ttu-id="62043-137">Ten problem można obejść, określając instalacji twardej.</span><span class="sxs-lookup"><span data-stu-id="62043-137">You can work around this problem by specifying a hard mount.</span></span> <span data-ttu-id="62043-138">Wymusza powitania klienta toowait, dopóki nie zostanie nawiązane połączenie lub do momentu jawnie zostało przerwane i może być używane tooprevent błędy z powodu limitów czasu sieci.</span><span class="sxs-lookup"><span data-stu-id="62043-138">This forces hello client toowait until a connection is established or until it’s explicitly interrupted and can be used tooprevent errors because of network time-outs.</span></span> <span data-ttu-id="62043-139">To rozwiązanie może jednak spowodować nieograniczonego oczekiwania.</span><span class="sxs-lookup"><span data-stu-id="62043-139">However, this workaround might cause indefinite waits.</span></span> <span data-ttu-id="62043-140">Należy przygotować toostop połączeń w razie potrzeby.</span><span class="sxs-lookup"><span data-stu-id="62043-140">Be prepared toostop connections as necessary.</span></span>

<span data-ttu-id="62043-141">Jeśli nie można uaktualnić toohello najnowsze wersje jądra, można obejść ten problem, przechowując pliku w udziale plików na platformę Azure hello zapisu tooevery 30 sekund lub mniej.</span><span class="sxs-lookup"><span data-stu-id="62043-141">If you cannot upgrade toohello latest kernel versions, you can work around this problem by keeping a file in hello Azure file share that you write tooevery 30 seconds or less.</span></span> <span data-ttu-id="62043-142">Musi to być operacji zapisu, takie jak ponowne zapisywanie hello utworzone lub Data modyfikacji pliku hello.</span><span class="sxs-lookup"><span data-stu-id="62043-142">This must be a write operation, such as rewriting hello created or modified date on hello file.</span></span> <span data-ttu-id="62043-143">W przeciwnym razie może uzyskiwać wyniki z pamięci podręcznej, a operacja nie może wyzwolić hello ponowne nawiązanie połączenia.</span><span class="sxs-lookup"><span data-stu-id="62043-143">Otherwise, you might get cached results, and your operation might not trigger hello reconnection.</span></span>

<a id="error115"></a>
## <a name="mount-error115-operation-now-in-progress-when-you-mount-azure-file-storage-by-using-smb-30"></a><span data-ttu-id="62043-144">"Instalowanie error(115): operacja w toku" podczas instalowania usługi Magazyn plików Azure przy użyciu protokołu SMB 3.0</span><span class="sxs-lookup"><span data-stu-id="62043-144">"Mount error(115): Operation now in progress" when you mount Azure File storage by using SMB 3.0</span></span>

### <a name="cause"></a><span data-ttu-id="62043-145">Przyczyna</span><span class="sxs-lookup"><span data-stu-id="62043-145">Cause</span></span>

<span data-ttu-id="62043-146">Niektóre dystrybucje systemu Linux nie jest jeszcze obsługiwany funkcji szyfrowania protokołu SMB 3.0 i użytkowników może zostać wyświetlony komunikat o błędzie "115", jeśli próbują toomount usługi Magazyn plików Azure przy użyciu protokołu SMB 3.0 ze względu na Brak funkcji.</span><span class="sxs-lookup"><span data-stu-id="62043-146">Some Linux distributions do not yet support encryption features in SMB 3.0 and users might receive a "115" error message if they try toomount Azure File storage by using SMB 3.0 because of a missing feature.</span></span>

### <a name="solution"></a><span data-ttu-id="62043-147">Rozwiązanie</span><span class="sxs-lookup"><span data-stu-id="62043-147">Solution</span></span>

<span data-ttu-id="62043-148">Funkcja szyfrowania protokołu SMB 3.0 dla systemu Linux została wprowadzona w 4.11 jądra.</span><span class="sxs-lookup"><span data-stu-id="62043-148">Encryption feature for SMB 3.0 for Linux was introduced in 4.11 kernel.</span></span> <span data-ttu-id="62043-149">Ta funkcja umożliwia instalowanie udziału plików platformy Azure z lokalnej lub w innym regionie Azure.</span><span class="sxs-lookup"><span data-stu-id="62043-149">This feature enables mounting of Azure File share from on-premises or a different Azure region.</span></span> <span data-ttu-id="62043-150">W czasie hello publikowania ta funkcja została backported tooUbuntu 17.04 i Ubuntu 16.10.</span><span class="sxs-lookup"><span data-stu-id="62043-150">At hello time of publishing, this functionality has been backported tooUbuntu 17.04 and Ubuntu 16.10.</span></span> <span data-ttu-id="62043-151">Jeśli klienta SMB systemu Linux nie obsługuje szyfrowania, należy zainstalować magazyn plików Azure przy użyciu protokołu SMB 2.1 z maszyny Wirtualnej systemu Linux platformy Azure, który znajduje się w hello tym samym centrum danych, ponieważ hello konta magazynu plików.</span><span class="sxs-lookup"><span data-stu-id="62043-151">If your Linux SMB client does not support encryption, mount Azure File storage by using SMB 2.1 from an Azure Linux VM that's in hello same datacenter as hello File storage account.</span></span>

<a id="slowperformance"></a>
## <a name="slow-performance-on-an-azure-file-share-mounted-on-a-linux-vm"></a><span data-ttu-id="62043-152">Niska wydajność w udziale plików na platformę Azure zainstalowane na maszynie Wirtualnej systemu Linux</span><span class="sxs-lookup"><span data-stu-id="62043-152">Slow performance on an Azure file share mounted on a Linux VM</span></span>

### <a name="cause"></a><span data-ttu-id="62043-153">Przyczyna</span><span class="sxs-lookup"><span data-stu-id="62043-153">Cause</span></span>

<span data-ttu-id="62043-154">Jedną z możliwych przyczyn niską wydajność jest wyłączone buforowanie.</span><span class="sxs-lookup"><span data-stu-id="62043-154">One possible cause of slow performance is disabled caching.</span></span>

### <a name="solution"></a><span data-ttu-id="62043-155">Rozwiązanie</span><span class="sxs-lookup"><span data-stu-id="62043-155">Solution</span></span>

<span data-ttu-id="62043-156">toocheck czy buforowanie jest wyłączone, wyszukaj hello **pamięci podręcznej =** wpisu.</span><span class="sxs-lookup"><span data-stu-id="62043-156">toocheck whether caching is disabled, look for hello **cache=** entry.</span></span> 

<span data-ttu-id="62043-157">**Pamięć podręczna = Brak** wskazuje, że buforowanie jest wyłączone.</span><span class="sxs-lookup"><span data-stu-id="62043-157">**Cache=none** indicates that caching is disabled.</span></span>  <span data-ttu-id="62043-158">Zainstalowanie hello udziału za pomocą polecenia instalacji domyślnej hello lub dodając jawnie hello **pamięci podręcznej = strict** tooensure polecenia instalacji toohello opcja, która domyślny tryb buforowania buforowania lub "strict" jest włączona.</span><span class="sxs-lookup"><span data-stu-id="62043-158">Remount hello share by using hello default mount command or by explicitly adding hello **cache=strict** option toohello mount command tooensure that default caching or "strict" caching mode is enabled.</span></span>

<span data-ttu-id="62043-159">W niektórych scenariuszach hello **serverino** opcji instalacji może spowodować hello **ls** stat toorun polecenie dla każdego wpisu w katalogu.</span><span class="sxs-lookup"><span data-stu-id="62043-159">In some scenarios, hello **serverino** mount option can cause hello **ls** command toorun stat against every directory entry.</span></span> <span data-ttu-id="62043-160">Ten problem powoduje spadek wydajności podczas jest wyświetlania katalogu duży.</span><span class="sxs-lookup"><span data-stu-id="62043-160">This behavior results in performance degradation when you're listing a big directory.</span></span> <span data-ttu-id="62043-161">Opcje instalacji hello można sprawdzić Twojej **/etc/fstab** wpis:</span><span class="sxs-lookup"><span data-stu-id="62043-161">You can check hello mount options in your **/etc/fstab** entry:</span></span>

`//azureuser.file.core.windows.net/cifs /cifs cifs vers=3.0,serverino,username=xxx,password=xxx,dir_mode=0777,file_mode=0777`

<span data-ttu-id="62043-162">Możesz również sprawdzić, czy prawidłowe opcje hello są używane przez uruchomienie hello **instalacji sudo | grep cifs** polecenia i sprawdzanie danych wyjściowych, takich jak hello następujące przykładowe dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="62043-162">You can also check whether hello correct options are being used by running hello  **sudo mount | grep cifs** command and checking its output, such as hello following example output:</span></span>

`//mabiccacifs.file.core.windows.net/cifs on /cifs type cifs (rw,relatime,vers=3.0,sec=ntlmssp,cache=strict,username=xxx,domain=X,uid=0,noforceuid,gid=0,noforcegid,addr=192.168.10.1,file_mode=0777, dir_mode=0777,persistenthandles,nounix,serverino,mapposix,rsize=1048576,wsize=1048576,actimeo=1)`

<span data-ttu-id="62043-163">Jeśli hello **pamięci podręcznej = strict** lub **serverino** opcja jest nie istnieje, odinstaluj i ponownie zainstalować magazyn plików Azure, uruchamiając polecenie instalacji hello z hello [dokumentacji](storage-how-to-use-files-linux.md).</span><span class="sxs-lookup"><span data-stu-id="62043-163">If hello **cache=strict** or **serverino** option is not present, unmount and mount Azure File storage again by running hello mount command from hello [documentation](storage-how-to-use-files-linux.md).</span></span> <span data-ttu-id="62043-164">Następnie, sprawdź ponownie tego hello **/etc/fstab** wpis ma hello wybraniu odpowiednich opcji.</span><span class="sxs-lookup"><span data-stu-id="62043-164">Then, recheck that hello **/etc/fstab** entry has hello correct options.</span></span>

<a id="timestampslost"></a>
## <a name="time-stamps-were-lost-in-copying-files-from-windows-toolinux"></a><span data-ttu-id="62043-165">Sygnatury czasowe zostały utracone podczas kopiowania plików z tooLinux systemu Windows</span><span class="sxs-lookup"><span data-stu-id="62043-165">Time stamps were lost in copying files from Windows tooLinux</span></span>

<span data-ttu-id="62043-166">Na platformach systemu Linux/Unix hello **cp -p** polecenie kończy się niepowodzeniem, jeśli plik 1 i 2 plików należą do firmy przez różnych użytkowników.</span><span class="sxs-lookup"><span data-stu-id="62043-166">On Linux/Unix platforms, hello **cp -p** command fails if file 1 and file 2 are owned by different users.</span></span>

### <a name="cause"></a><span data-ttu-id="62043-167">Przyczyna</span><span class="sxs-lookup"><span data-stu-id="62043-167">Cause</span></span>

<span data-ttu-id="62043-168">Witaj flagi force **f** w COPYFILE powoduje wykonywania **cp -p -f** w systemie Unix.</span><span class="sxs-lookup"><span data-stu-id="62043-168">hello force flag **f** in COPYFILE results in executing **cp -p -f** on Unix.</span></span> <span data-ttu-id="62043-169">To polecenie nie powiedzie się także sygnaturę czasową hello toopreserve hello pliku, który nie jesteś właścicielem.</span><span class="sxs-lookup"><span data-stu-id="62043-169">This command also fails toopreserve hello time stamp of hello file that you don't own.</span></span>

### <a name="workaround"></a><span data-ttu-id="62043-170">Obejście problemu</span><span class="sxs-lookup"><span data-stu-id="62043-170">Workaround</span></span>

<span data-ttu-id="62043-171">Użyj hello magazynu konta użytkownika do kopiowania plików hello:</span><span class="sxs-lookup"><span data-stu-id="62043-171">Use hello storage account user for copying hello files:</span></span>

- `Useadd : [storage account name]`
- `Passwd [storage account name]`
- `Su [storage account name]`
- `Cp -p filename.txt /share`

## <a name="need-help-contact-support"></a><span data-ttu-id="62043-172">Potrzebujesz pomocy?</span><span class="sxs-lookup"><span data-stu-id="62043-172">Need help?</span></span> <span data-ttu-id="62043-173">Skontaktuj się z pomocą techniczną.</span><span class="sxs-lookup"><span data-stu-id="62043-173">Contact support.</span></span>

<span data-ttu-id="62043-174">Jeśli nadal potrzebujesz pomocy, [się z pomocą techniczną](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget szybkie rozwiązanie problemu.</span><span class="sxs-lookup"><span data-stu-id="62043-174">If you still need help, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget your problem resolved quickly.</span></span>
