---
title: "aaaTroubleshoot problemów z magazynu plików Azure w systemie Windows | Dokumentacja firmy Microsoft"
description: "Rozwiązywanie problemów magazyn plików Azure w systemie Windows"
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
ms.date: 06/28/2017
ms.author: genli
ms.openlocfilehash: ba0315d1add76a27fec93a9aee3aa99ccb7fa164
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-file-storage-problems-in-windows"></a><span data-ttu-id="1302e-103">Rozwiązywanie problemów magazyn plików Azure w systemie Windows</span><span class="sxs-lookup"><span data-stu-id="1302e-103">Troubleshoot Azure File storage problems in Windows</span></span>

<span data-ttu-id="1302e-104">W tym artykule wymieniono typowe problemy, które są powiązane tooMicrosoft magazyn plików Azure podczas nawiązywania połączenia przez klientów systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="1302e-104">This article lists common problems that are related tooMicrosoft Azure File storage when you connect from Windows clients.</span></span> <span data-ttu-id="1302e-105">Zapewnia także możliwe przyczyny i rozwiązania tych problemów.</span><span class="sxs-lookup"><span data-stu-id="1302e-105">It also provides possible causes and resolutions for these problems.</span></span> <span data-ttu-id="1302e-106">Ponadto toohello Rozwiązywanie problemów z kroków w tym artykule, można również użyć [AzFileDiagnostics](https://gallery.technet.microsoft.com/Troubleshooting-tool-for-a9fa1fe5) aby upewnić się, że Windows hello środowiska klienta ma poprawne warunki wstępne.</span><span class="sxs-lookup"><span data-stu-id="1302e-106">In addition toohello troubleshooting steps in this article, you can also use [AzFileDiagnostics](https://gallery.technet.microsoft.com/Troubleshooting-tool-for-a9fa1fe5) to ensure that hello Windows client environment has correct prerequisites.</span></span> <span data-ttu-id="1302e-107">AzFileDiagnostics automatyzuje wykrywania większość objawy hello wymienionych w tym artykule i pomaga skonfigurować optymalną wydajność tooget środowiska.</span><span class="sxs-lookup"><span data-stu-id="1302e-107">AzFileDiagnostics automates detection of most of hello symptoms mentioned in this article and helps set up your environment tooget optimal performance.</span></span> <span data-ttu-id="1302e-108">Informacje te można również znaleźć w hello [Rozwiązywanie problemów z udziałów plików Azure](https://support.microsoft.com/help/4022301/troubleshooter-for-azure-files-shares) zapewnia tooassist czynności możesz problemów udziałów plików Azure łączenie/mapowanie/instalowanie.</span><span class="sxs-lookup"><span data-stu-id="1302e-108">You can also find this information in hello [Azure Files shares Troubleshooter](https://support.microsoft.com/help/4022301/troubleshooter-for-azure-files-shares) that provides steps tooassist you with problems connecting/mapping/mounting Azure Files shares.</span></span>


<a id="error53-67-87"></a>
## <a name="error-53-error-67-or-error-87-when-you-mount-or-unmount-an-azure-file-share"></a><span data-ttu-id="1302e-109">Błąd 53, 67 błąd lub 87 błąd podczas instalowania lub odinstalowania udziału plików na platformę Azure</span><span class="sxs-lookup"><span data-stu-id="1302e-109">Error 53, Error 67, or Error 87 when you mount or unmount an Azure file share</span></span>

<span data-ttu-id="1302e-110">Podczas próby toomount udostępniania plików z lokalnymi lub z różnych centrach danych, zostanie zgłoszony hello następujące błędy:</span><span class="sxs-lookup"><span data-stu-id="1302e-110">When you try toomount a file share from on-premises or from a different datacenter, you might receive hello following errors:</span></span>

- <span data-ttu-id="1302e-111">Wystąpił błąd systemowy 53.</span><span class="sxs-lookup"><span data-stu-id="1302e-111">System error 53 has occurred.</span></span> <span data-ttu-id="1302e-112">Nie można odnaleźć ścieżki sieciowej Hello.</span><span class="sxs-lookup"><span data-stu-id="1302e-112">hello network path was not found.</span></span>
- <span data-ttu-id="1302e-113">Wystąpił błąd systemowy 67.</span><span class="sxs-lookup"><span data-stu-id="1302e-113">System error 67 has occurred.</span></span> <span data-ttu-id="1302e-114">Nie można odnaleźć nazwy sieci Hello.</span><span class="sxs-lookup"><span data-stu-id="1302e-114">hello network name cannot be found.</span></span>
- <span data-ttu-id="1302e-115">Wystąpił błąd systemowy 87.</span><span class="sxs-lookup"><span data-stu-id="1302e-115">System error 87 has occurred.</span></span> <span data-ttu-id="1302e-116">Parametr Hello jest nieprawidłowy.</span><span class="sxs-lookup"><span data-stu-id="1302e-116">hello parameter is incorrect.</span></span>

### <a name="cause-1-unencrypted-communication-channel"></a><span data-ttu-id="1302e-117">Przyczyny 1: Kanał komunikacyjny niezaszyfrowane</span><span class="sxs-lookup"><span data-stu-id="1302e-117">Cause 1: Unencrypted communication channel</span></span>

<span data-ttu-id="1302e-118">Ze względów bezpieczeństwa połączeń tooAzure udziały plików są zablokowane, jeśli nie jest szyfrowany kanał komunikacyjny hello i hello próba połączenia nie jest podejmowana z hello tym samym centrum danych, w którym znajdują się hello udziały plików platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="1302e-118">For security reasons, connections tooAzure file shares are blocked if hello communication channel isn’t encrypted and if hello connection attempt isn't made from hello same datacenter where hello Azure file shares reside.</span></span> <span data-ttu-id="1302e-119">Szyfrowanie kanału komunikacji znajduje się tylko wtedy, gdy użytkownik hello kliencki system operacyjny obsługuje szyfrowanie protokołu SMB.</span><span class="sxs-lookup"><span data-stu-id="1302e-119">Communication channel encryption is provided only if hello user’s client OS supports SMB encryption.</span></span>

<span data-ttu-id="1302e-120">Windows 8, Windows Server 2012 i nowsze wersje każdego systemu negocjowania żądania zawierające SMB 3.0, który obsługuje szyfrowanie.</span><span class="sxs-lookup"><span data-stu-id="1302e-120">Windows 8, Windows Server 2012, and later versions of each system negotiate requests that include SMB 3.0, which supports encryption.</span></span>

### <a name="solution-for-cause-1"></a><span data-ttu-id="1302e-121">Rozwiązanie dla przyczyny 1</span><span class="sxs-lookup"><span data-stu-id="1302e-121">Solution for cause 1</span></span>

<span data-ttu-id="1302e-122">Połączenie z klienta, który wykonuje jedną z następujących hello:</span><span class="sxs-lookup"><span data-stu-id="1302e-122">Connect from a client that does one of hello following:</span></span>

- <span data-ttu-id="1302e-123">Spełnia wymagania hello systemu Windows 8 i Windows Server 2012 lub nowszy</span><span class="sxs-lookup"><span data-stu-id="1302e-123">Meets hello requirements of Windows 8 and Windows Server 2012 or later versions</span></span>
- <span data-ttu-id="1302e-124">Nawiązuje połączenie z maszyną wirtualną w hello sam centrum danych, zgodnie z kontem magazynu platformy Azure, służący do udziału plików na platformę Azure hello hello</span><span class="sxs-lookup"><span data-stu-id="1302e-124">Connects from a virtual machine in hello same datacenter as hello Azure storage account that is used for hello Azure file share</span></span>

### <a name="cause-2-port-445-is-blocked"></a><span data-ttu-id="1302e-125">Przyczyny 2: Port 445 jest zablokowany.</span><span class="sxs-lookup"><span data-stu-id="1302e-125">Cause 2: Port 445 is blocked</span></span>

<span data-ttu-id="1302e-126">Błąd systemowy 53 lub błąd systemu 67 może wystąpić, jeśli port 445 komunikacji wychodzącej tooan plików Azure magazynu centrum danych jest zablokowana.</span><span class="sxs-lookup"><span data-stu-id="1302e-126">System error 53 or system error 67 can occur if port 445 outbound communication tooan Azure File storage datacenter is blocked.</span></span> <span data-ttu-id="1302e-127">Podsumowanie hello toosee usługodawców Zezwalaj lub nie zezwalaj na dostęp z portu 445, przejdź zbyt[TechNet](http://social.technet.microsoft.com/wiki/contents/articles/32346.azure-summary-of-isps-that-allow-disallow-access-from-port-445.aspx).</span><span class="sxs-lookup"><span data-stu-id="1302e-127">toosee hello summary of ISPs that allow or disallow access from port 445, go too[TechNet](http://social.technet.microsoft.com/wiki/contents/articles/32346.azure-summary-of-isps-that-allow-disallow-access-from-port-445.aspx).</span></span>

<span data-ttu-id="1302e-128">toounderstand czy jest to powód wiadomości powitania "Błąd systemu 53" hello, może użyć Portqry tooquery hello TCP:445 endpoint.</span><span class="sxs-lookup"><span data-stu-id="1302e-128">toounderstand whether this is hello reason behind hello "System error 53" message, you can use Portqry tooquery hello TCP:445 endpoint.</span></span> <span data-ttu-id="1302e-129">Jeśli punkt końcowy TCP:445 hello jest wyświetlany jako filtrowane hello TCP port jest zablokowany.</span><span class="sxs-lookup"><span data-stu-id="1302e-129">If hello TCP:445 endpoint is displayed as filtered, hello TCP port is blocked.</span></span> <span data-ttu-id="1302e-130">Poniżej przedstawiono przykładowe zapytanie:</span><span class="sxs-lookup"><span data-stu-id="1302e-130">Here is an example query:</span></span>

  `g:\DataDump\Tools\Portqry>PortQry.exe -n [storage account name].file.core.windows.net -p TCP -e 445`

<span data-ttu-id="1302e-131">Jeśli TCP port 445 jest zablokowany przez regułę wzdłuż ścieżki sieciowej hello, zostanie wyświetlony hello następujące dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="1302e-131">If TCP port 445 is blocked by a rule along hello network path, you will see hello following output:</span></span>

  `TCP port 445 (microsoft-ds service): FILTERED`

<span data-ttu-id="1302e-132">Aby uzyskać więcej informacji o tym, jak toouse Portqry, zobacz [opis narzędzia wiersza polecenia Portqry.exe hello](https://support.microsoft.com/help/310099).</span><span class="sxs-lookup"><span data-stu-id="1302e-132">For more information about how toouse Portqry, see [Description of hello Portqry.exe command-line utility](https://support.microsoft.com/help/310099).</span></span>

### <a name="solution-for-cause-2"></a><span data-ttu-id="1302e-133">Rozwiązanie dla przyczyny 2</span><span class="sxs-lookup"><span data-stu-id="1302e-133">Solution for cause 2</span></span>

<span data-ttu-id="1302e-134">Praca z port 445 wychodzących tooopen dział IT za[zakresów adresów IP Azure](https://www.microsoft.com/download/details.aspx?id=41653).</span><span class="sxs-lookup"><span data-stu-id="1302e-134">Work with your IT department tooopen port 445 outbound too[Azure IP ranges](https://www.microsoft.com/download/details.aspx?id=41653).</span></span>

### <a name="cause-3-ntlmv1-is-enabled"></a><span data-ttu-id="1302e-135">Przyczyny 3: NTLMv1 jest włączona.</span><span class="sxs-lookup"><span data-stu-id="1302e-135">Cause 3: NTLMv1 is enabled</span></span>

<span data-ttu-id="1302e-136">Błąd systemowy 53 lub błąd systemu: 87 może wystąpić, jeśli włączono komunikację NTLMv1 na powitania klienta.</span><span class="sxs-lookup"><span data-stu-id="1302e-136">System error 53 or system error 87 can occur if NTLMv1 communication is enabled on hello client.</span></span> <span data-ttu-id="1302e-137">Magazyn plików Azure obsługuje tylko z uwierzytelniania NTLMv2.</span><span class="sxs-lookup"><span data-stu-id="1302e-137">Azure File storage supports only NTLMv2 authentication.</span></span> <span data-ttu-id="1302e-138">Mających włączone NTLMv1 tworzy mniej bezpiecznych klienta.</span><span class="sxs-lookup"><span data-stu-id="1302e-138">Having NTLMv1 enabled creates a less-secure client.</span></span> <span data-ttu-id="1302e-139">W związku z tym komunikacja jest zablokowana dla usługi Magazyn plików Azure.</span><span class="sxs-lookup"><span data-stu-id="1302e-139">Therefore, communication is blocked for Azure File storage.</span></span> 

<span data-ttu-id="1302e-140">toodetermine czy jest to hello Przyczyna błędu hello, sprawdź, czy ten powitania po podklucz rejestru jest ustawiona wartość tooa 3:</span><span class="sxs-lookup"><span data-stu-id="1302e-140">toodetermine whether this is hello cause of hello error, verify that hello following registry subkey is set tooa value of 3:</span></span>

<span data-ttu-id="1302e-141">**Kluczu HKLM\SYSTEM\CurrentControlSet\Control\Lsa > LmCompatibilityLevel**</span><span class="sxs-lookup"><span data-stu-id="1302e-141">**HKLM\SYSTEM\CurrentControlSet\Control\Lsa > LmCompatibilityLevel**</span></span>

<span data-ttu-id="1302e-142">Aby uzyskać więcej informacji, zobacz hello [LmCompatibilityLevel](https://technet.microsoft.com/library/cc960646.aspx) temacie w witrynie TechNet.</span><span class="sxs-lookup"><span data-stu-id="1302e-142">For more information, see hello [LmCompatibilityLevel](https://technet.microsoft.com/library/cc960646.aspx) topic on TechNet.</span></span>

### <a name="solution-for-cause-3"></a><span data-ttu-id="1302e-143">Rozwiązanie dla przyczyny 3</span><span class="sxs-lookup"><span data-stu-id="1302e-143">Solution for cause 3</span></span>

<span data-ttu-id="1302e-144">Przywróć hello **LmCompatibilityLevel** wartość toohello domyślna wartość 3 w powitania po podklucz rejestru:</span><span class="sxs-lookup"><span data-stu-id="1302e-144">Revert hello **LmCompatibilityLevel** value toohello default value of 3 in hello following registry subkey:</span></span>

  <span data-ttu-id="1302e-145">**Kluczu HKLM\SYSTEM\CurrentControlSet\Control\Lsa**</span><span class="sxs-lookup"><span data-stu-id="1302e-145">**HKLM\SYSTEM\CurrentControlSet\Control\Lsa**</span></span>

<a id="error1816"></a>
## <a name="error-1816-not-enough-quota-is-available-tooprocess-this-command-when-you-copy-tooan-azure-file-share"></a><span data-ttu-id="1302e-146">Błąd 1816 "za mało zasobów jest dostępne tooprocess to polecenie" przy kopiowaniu tooan udziału plików na platformę Azure</span><span class="sxs-lookup"><span data-stu-id="1302e-146">Error 1816 “Not enough quota is available tooprocess this command” when you copy tooan Azure file share</span></span>

### <a name="cause"></a><span data-ttu-id="1302e-147">Przyczyna</span><span class="sxs-lookup"><span data-stu-id="1302e-147">Cause</span></span>

<span data-ttu-id="1302e-148">Błąd 1816 odbywa się po osiągnięciu hello górny limit współbieżnych otwartych dojść, które są dozwolone dla pliku na komputerze hello, którym jest zainstalowany hello udziału plików.</span><span class="sxs-lookup"><span data-stu-id="1302e-148">Error 1816 happens when you reach hello upper limit of concurrent open handles that are allowed for a file on hello computer where hello file share is being mounted.</span></span>

### <a name="solution"></a><span data-ttu-id="1302e-149">Rozwiązanie</span><span class="sxs-lookup"><span data-stu-id="1302e-149">Solution</span></span>

<span data-ttu-id="1302e-150">Ograniczenia hello liczby równoczesnych otwartych dojść zamykając niektóre dojść, a następnie spróbuj ponownie.</span><span class="sxs-lookup"><span data-stu-id="1302e-150">Reduce hello number of concurrent open handles by closing some handles, and then retry.</span></span> <span data-ttu-id="1302e-151">Aby uzyskać więcej informacji, zobacz [Lista kontrolna wydajności i skalowalności magazynu Microsoft Azure](storage-performance-checklist.md).</span><span class="sxs-lookup"><span data-stu-id="1302e-151">For more information, see [Microsoft Azure Storage performance and scalability checklist](storage-performance-checklist.md).</span></span>

<a id="slowfilecopying"></a>
## <a name="slow-file-copying-tooand-from-azure-file-storage-in-windows"></a><span data-ttu-id="1302e-152">Powolne pliku kopiowanie tooand z usługi Magazyn plików Azure w systemie Windows</span><span class="sxs-lookup"><span data-stu-id="1302e-152">Slow file copying tooand from Azure File storage in Windows</span></span>

<span data-ttu-id="1302e-153">Niska wydajność napotkać podczas próby tootransfer pliki toohello usługa plików Azure.</span><span class="sxs-lookup"><span data-stu-id="1302e-153">You might see slow performance when you try tootransfer files toohello Azure File service.</span></span>

- <span data-ttu-id="1302e-154">Jeśli użytkownik nie ma określonego minimalny wymagany rozmiar operacji We/Wy, zalecane jest użycie 1 MB, ponieważ hello rozmiaru we/wy, aby zapewnić optymalną wydajność.</span><span class="sxs-lookup"><span data-stu-id="1302e-154">If you don’t have a specific minimum I/O size requirement, we recommend that you use 1 MB as hello I/O size for optimal performance.</span></span>
-   <span data-ttu-id="1302e-155">Jeśli znasz zapisuje hello rozmiaru końcowego, pliku, który powiększa się z, a oprogramowanie nie ma problemów ze zgodnością, gdy hello niezapisanych tail hello pliku zawiera zera, a następnie ustaw hello rozmiar pliku z wyprzedzeniem zamiast wprowadzania każdego zapisu rozszerzanie zapisu.</span><span class="sxs-lookup"><span data-stu-id="1302e-155">If you know hello final size of a file that you are extending with writes, and your software doesn’t have compatibility problems when hello unwritten tail on hello file contains zeros, then set hello file size in advance instead of making every write an extending write.</span></span>
-   <span data-ttu-id="1302e-156">Użyj metody copy prawo hello:</span><span class="sxs-lookup"><span data-stu-id="1302e-156">Use hello right copy method:</span></span>
    -   <span data-ttu-id="1302e-157">Użyj [AzCopy](storage-use-azcopy.md#file-copy) żadnych transferu między dwoma udziałami plików.</span><span class="sxs-lookup"><span data-stu-id="1302e-157">Use [AzCopy](storage-use-azcopy.md#file-copy) for any transfer between two file shares.</span></span>
    -   <span data-ttu-id="1302e-158">Użyj [Robocopy](https://blogs.msdn.microsoft.com/granth/2009/12/07/multi-threaded-robocopy-for-faster-copies/) między udziałami plików na komputerze lokalnym.</span><span class="sxs-lookup"><span data-stu-id="1302e-158">Use [Robocopy](https://blogs.msdn.microsoft.com/granth/2009/12/07/multi-threaded-robocopy-for-faster-copies/) between file shares on an on-premises computer.</span></span>

### <a name="considerations-for-windows-81-or-windows-server-2012-r2"></a><span data-ttu-id="1302e-159">Zagadnienia dotyczące Windows 8.1 lub Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="1302e-159">Considerations for Windows 8.1 or Windows Server 2012 R2</span></span>

<span data-ttu-id="1302e-160">Dla klientów z systemem Windows 8.1 lub Windows Server 2012 R2, upewnij się, że hello [KB3114025](https://support.microsoft.com/help/3114025) poprawka jest zainstalowana.</span><span class="sxs-lookup"><span data-stu-id="1302e-160">For clients that are running Windows 8.1 or Windows Server 2012 R2, make sure that hello [KB3114025](https://support.microsoft.com/help/3114025) hotfix is installed.</span></span> <span data-ttu-id="1302e-161">Ta poprawka poprawia wydajność hello Utwórz i zamknąć dojścia.</span><span class="sxs-lookup"><span data-stu-id="1302e-161">This hotfix improves hello performance of create and close handles.</span></span>

<span data-ttu-id="1302e-162">Można uruchomić następującego skryptu toocheck, czy zainstalowano poprawkę hello hello:</span><span class="sxs-lookup"><span data-stu-id="1302e-162">You can run hello following script toocheck whether hello hotfix has been installed:</span></span>

`reg query HKLM\SYSTEM\CurrentControlSet\Services\LanmanWorkstation\Parameters\Policies`

<span data-ttu-id="1302e-163">Jeśli zainstalowano poprawkę hello następujące dane wyjściowe są wyświetlane:</span><span class="sxs-lookup"><span data-stu-id="1302e-163">If hotfix is installed, hello following output is displayed:</span></span>

`HKEY_Local_MACHINE\SYSTEM\CurrentControlSet\Services\LanmanWorkstation\Parameters\Policies {96c345ef-3cac-477b-8fcd-bea1a564241c} REG_DWORD 0x1`

> [!Note]
> <span data-ttu-id="1302e-164">Obrazy systemu Windows Server 2012 R2 w portalu Azure Marketplace mają poprawki KB3114025 instalowane domyślnie począwszy od grudnia 2015 r.</span><span class="sxs-lookup"><span data-stu-id="1302e-164">Windows Server 2012 R2 images in Azure Marketplace have hotfix KB3114025 installed by default, starting in December 2015.</span></span>

<a id="shareismissing"></a>
## <a name="no-folder-with-a-drive-letter-in-my-computer"></a><span data-ttu-id="1302e-165">Nie folderu z literą dysku w **Mój komputer**</span><span class="sxs-lookup"><span data-stu-id="1302e-165">No folder with a drive letter in **My Computer**</span></span>

<span data-ttu-id="1302e-166">Jeśli mapujesz udziału plików na platformę Azure jako administrator przy użyciu polecenie net use udziału hello pojawia się toobe Brak.</span><span class="sxs-lookup"><span data-stu-id="1302e-166">If you map an Azure file share as an administrator by using net use, hello share appears toobe missing.</span></span>

### <a name="cause"></a><span data-ttu-id="1302e-167">Przyczyna</span><span class="sxs-lookup"><span data-stu-id="1302e-167">Cause</span></span>

<span data-ttu-id="1302e-168">Domyślnie Eksploratorze plików systemu Windows nie działa jako administrator.</span><span class="sxs-lookup"><span data-stu-id="1302e-168">By default, Windows File Explorer does not run as an administrator.</span></span> <span data-ttu-id="1302e-169">Jeśli uruchomisz polecenie net use z wiersza polecenia z uprawnieniami administracyjnymi, mapowania dysku sieciowego hello jako administrator.</span><span class="sxs-lookup"><span data-stu-id="1302e-169">If you run net use from an administrative command prompt, you map hello network drive as an administrator.</span></span> <span data-ttu-id="1302e-170">Ponieważ zamapowanych dysków są skoncentrowane na użytkowniku, hello konta użytkownika, który jest zalogowany nie są wyświetlane hello dysków, jeśli są one zainstalowane przy użyciu konta innego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="1302e-170">Because mapped drives are user-centric, hello user account that is logged in does not display hello drives if they are mounted under a different user account.</span></span>

### <a name="solution"></a><span data-ttu-id="1302e-171">Rozwiązanie</span><span class="sxs-lookup"><span data-stu-id="1302e-171">Solution</span></span>
<span data-ttu-id="1302e-172">Instalowanie udziału hello z wiersza polecenia bez uprawnień administratora.</span><span class="sxs-lookup"><span data-stu-id="1302e-172">Mount hello share from a non-administrator command line.</span></span> <span data-ttu-id="1302e-173">Alternatywnie, można wykonać [w tym temacie w witrynie TechNet](https://technet.microsoft.com/library/ee844140.aspx) tooconfigure hello **EnableLinkedConnections** wartości rejestru.</span><span class="sxs-lookup"><span data-stu-id="1302e-173">Alternatively, you can follow [this TechNet topic](https://technet.microsoft.com/library/ee844140.aspx) tooconfigure hello **EnableLinkedConnections** registry value.</span></span>

<a id="netuse"></a>
## <a name="net-use-command-fails-if-hello-storage-account-contains-a-forward-slash"></a><span data-ttu-id="1302e-174">Polecenie net use zakończy się niepowodzeniem, jeśli konto magazynu hello zawiera ukośnik</span><span class="sxs-lookup"><span data-stu-id="1302e-174">Net use command fails if hello storage account contains a forward slash</span></span>

### <a name="cause"></a><span data-ttu-id="1302e-175">Przyczyna</span><span class="sxs-lookup"><span data-stu-id="1302e-175">Cause</span></span>

<span data-ttu-id="1302e-176">polecenie net use Hello ukośnika (/) są interpretowane jako opcji wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="1302e-176">hello net use command interprets a forward slash (/) as a command-line option.</span></span> <span data-ttu-id="1302e-177">Nazwa konta użytkownika rozpoczyna się od ukośnika, mapowanie dysku hello kończy się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="1302e-177">If your user account name starts with a forward slash, hello drive mapping fails.</span></span>

### <a name="solution"></a><span data-ttu-id="1302e-178">Rozwiązanie</span><span class="sxs-lookup"><span data-stu-id="1302e-178">Solution</span></span>

<span data-ttu-id="1302e-179">Możesz użyć dowolnej z hello następujące kroki toowork wokół hello problemu:</span><span class="sxs-lookup"><span data-stu-id="1302e-179">You can use either of hello following steps toowork around hello problem:</span></span>

- <span data-ttu-id="1302e-180">Uruchom następujące polecenia programu PowerShell hello:</span><span class="sxs-lookup"><span data-stu-id="1302e-180">Run hello following PowerShell command:</span></span>

  `New-SmbMapping -LocalPath y: -RemotePath \\server\share -UserName accountName -Password "password can contain / and \ etc" `

  <span data-ttu-id="1302e-181">Z pliku wsadowego możesz uruchomić polecenie hello w ten sposób:</span><span class="sxs-lookup"><span data-stu-id="1302e-181">From a batch file, you can run hello command this way:</span></span>

  `Echo new-smbMapping ... | powershell -command –`

- <span data-ttu-id="1302e-182">Wprowadzone znaki cudzysłowu wokół hello toowork klucza tego problemu —, chyba że hello pierwszego znaku ukośnika hello.</span><span class="sxs-lookup"><span data-stu-id="1302e-182">Put double quotation marks around hello key toowork around this problem--unless hello forward slash is hello first character.</span></span> <span data-ttu-id="1302e-183">Jeśli tak jest, użyj trybie interakcyjnym hello i wprowadź swoje hasło oddzielnie lub ponownie wygenerować tooget Twoje klucze klucz, który nie zaczyna się od ukośnika.</span><span class="sxs-lookup"><span data-stu-id="1302e-183">If it is, either use hello interactive mode and enter your password separately or regenerate your keys tooget a key that doesn't start with a forward slash.</span></span>

<a id="cannotaccess"></a>
## <a name="application-or-service-cannot-access-a-mounted-azure-file-storage-drive"></a><span data-ttu-id="1302e-184">Aplikacja lub usługa nie może uzyskać dostępu zainstalowany dysk magazynu plików Azure</span><span class="sxs-lookup"><span data-stu-id="1302e-184">Application or service cannot access a mounted Azure File storage drive</span></span>

### <a name="cause"></a><span data-ttu-id="1302e-185">Przyczyna</span><span class="sxs-lookup"><span data-stu-id="1302e-185">Cause</span></span>

<span data-ttu-id="1302e-186">Dyski są zainstalowane dla poszczególnych użytkowników.</span><span class="sxs-lookup"><span data-stu-id="1302e-186">Drives are mounted per user.</span></span> <span data-ttu-id="1302e-187">Jeśli aplikacji lub usługi jest uruchomiony w ramach innego konta użytkownika niż hello, który zainstalowany dysk hello, aplikacja hello nie będą widzieć hello dysku.</span><span class="sxs-lookup"><span data-stu-id="1302e-187">If your application or service is running under a different user account than hello one that mounted hello drive, hello application will not see hello drive.</span></span>

### <a name="solution"></a><span data-ttu-id="1302e-188">Rozwiązanie</span><span class="sxs-lookup"><span data-stu-id="1302e-188">Solution</span></span>

<span data-ttu-id="1302e-189">Użyj jednej z następujących rozwiązań hello:</span><span class="sxs-lookup"><span data-stu-id="1302e-189">Use one of hello following solutions:</span></span>

-   <span data-ttu-id="1302e-190">Dysk hello zainstalować z hello tego samego konta użytkownika, który zawiera aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="1302e-190">Mount hello drive from hello same user account that contains hello application.</span></span> <span data-ttu-id="1302e-191">Można użyć narzędzia, takiego jak narzędzia PsExec.</span><span class="sxs-lookup"><span data-stu-id="1302e-191">You can use a tool such as PsExec.</span></span>
- <span data-ttu-id="1302e-192">Przekazywanie hello parametry nazwę i hasło użytkownika z polecenia net use hello nazwy konta magazynu hello i klucz.</span><span class="sxs-lookup"><span data-stu-id="1302e-192">Pass hello storage account name and key in hello user name and password parameters of hello net use command.</span></span>

<span data-ttu-id="1302e-193">Po wykonaniu tych instrukcji, może zostać wyświetlony następujący komunikat o błędzie, uruchamiając polecenie net use dla konta usługi systemu i sieci hello hello: "Wystąpił błąd systemowy 1312.</span><span class="sxs-lookup"><span data-stu-id="1302e-193">After you follow these instructions, you might receive hello following error message when you run net use for hello system/network service account: "System error 1312 has occurred.</span></span> <span data-ttu-id="1302e-194">Określona sesja logowania nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="1302e-194">A specified logon session does not exist.</span></span> <span data-ttu-id="1302e-195">Go może została już zakończona."</span><span class="sxs-lookup"><span data-stu-id="1302e-195">It may already have been terminated."</span></span> <span data-ttu-id="1302e-196">W takim przypadku należy sprawdzić tej nazwie użytkownika hello przekazywany toonet Użyj zawiera informacje o domenie (na przykład: "[nazwa konta magazynu]. file.core.windows .net").</span><span class="sxs-lookup"><span data-stu-id="1302e-196">If this occurs, make sure that hello username that is passed toonet use includes domain information (for example: "[storage account name].file.core.windows.net").</span></span>

<a id="doesnotsupportencryption"></a>
## <a name="error-you-are-copying-a-file-tooa-destination-that-does-not-support-encryption"></a><span data-ttu-id="1302e-197">Błąd "Kopiujesz plik docelowy tooa, który nie obsługuje szyfrowania"</span><span class="sxs-lookup"><span data-stu-id="1302e-197">Error "You are copying a file tooa destination that does not support encryption"</span></span>

<span data-ttu-id="1302e-198">Po skopiowaniu pliku za pośrednictwem sieci hello plik hello jest odszyfrowany na komputerze źródłowym hello, przekazywane w postaci zwykłego tekstu, a następnie ponownie szyfrowane w miejscu docelowym hello.</span><span class="sxs-lookup"><span data-stu-id="1302e-198">When a file is copied over hello network, hello file is decrypted on hello source computer, transmitted in plaintext, and re-encrypted at hello destination.</span></span> <span data-ttu-id="1302e-199">Jednak zostanie wyświetlony następujący błąd, jeśli próbujesz toocopy zaszyfrowanego pliku hello: "Kopiujesz hello plik tooa docelowy nie obsługuje szyfrowania."</span><span class="sxs-lookup"><span data-stu-id="1302e-199">However, you might see hello following error when you're trying toocopy an encrypted file: "You are copying hello file tooa destination that does not support encryption."</span></span>

### <a name="cause"></a><span data-ttu-id="1302e-200">Przyczyna</span><span class="sxs-lookup"><span data-stu-id="1302e-200">Cause</span></span>
<span data-ttu-id="1302e-201">Ten problem może wystąpić, jeśli używasz systemu szyfrowania plików (EFS).</span><span class="sxs-lookup"><span data-stu-id="1302e-201">This problem can occur if you are using Encrypting File System (EFS).</span></span> <span data-ttu-id="1302e-202">Pliki zaszyfrowane przez funkcję BitLocker można tooAzure skopiowanego pliku magazynu.</span><span class="sxs-lookup"><span data-stu-id="1302e-202">BitLocker-encrypted files can be copied tooAzure File storage.</span></span> <span data-ttu-id="1302e-203">Magazyn plików Azure nie obsługuje jednak systemu szyfrowania plików NTFS.</span><span class="sxs-lookup"><span data-stu-id="1302e-203">However, Azure File storage does not support NTFS EFS.</span></span>

### <a name="workaround"></a><span data-ttu-id="1302e-204">Obejście problemu</span><span class="sxs-lookup"><span data-stu-id="1302e-204">Workaround</span></span>
<span data-ttu-id="1302e-205">toocopy pliku za pośrednictwem sieci hello, musisz najpierw musisz go odszyfrować.</span><span class="sxs-lookup"><span data-stu-id="1302e-205">toocopy a file over hello network, you must first decrypt it.</span></span> <span data-ttu-id="1302e-206">Użyj jednej z następujących metod hello:</span><span class="sxs-lookup"><span data-stu-id="1302e-206">Use one of hello following methods:</span></span>

- <span data-ttu-id="1302e-207">Użyj hello **skopiuj /d** polecenia.</span><span class="sxs-lookup"><span data-stu-id="1302e-207">Use hello **copy /d** command.</span></span> <span data-ttu-id="1302e-208">Umożliwia hello zaszyfrowane pliki toobe zapisane jako odszyfrowane pliki w miejscu docelowym hello.</span><span class="sxs-lookup"><span data-stu-id="1302e-208">It allows hello encrypted files toobe saved as decrypted files at hello destination.</span></span>
- <span data-ttu-id="1302e-209">Ustaw powitania po klucz rejestru:</span><span class="sxs-lookup"><span data-stu-id="1302e-209">Set hello following registry key:</span></span>
  - <span data-ttu-id="1302e-210">Ścieżka = HKLM\Software\Policies\Microsoft\Windows\System</span><span class="sxs-lookup"><span data-stu-id="1302e-210">Path = HKLM\Software\Policies\Microsoft\Windows\System</span></span>
  - <span data-ttu-id="1302e-211">Typ wartości = DWORD</span><span class="sxs-lookup"><span data-stu-id="1302e-211">Value type = DWORD</span></span>
  - <span data-ttu-id="1302e-212">Nazwa = CopyFileAllowDecryptedRemoteDestination</span><span class="sxs-lookup"><span data-stu-id="1302e-212">Name = CopyFileAllowDecryptedRemoteDestination</span></span>
  - <span data-ttu-id="1302e-213">Wartość = 1</span><span class="sxs-lookup"><span data-stu-id="1302e-213">Value = 1</span></span>

<span data-ttu-id="1302e-214">Należy pamiętać, że tego klucza rejestru hello ustawienie ma wpływ na wszystkie operacje kopii wykonywanych toonetwork udziałów.</span><span class="sxs-lookup"><span data-stu-id="1302e-214">Be aware that setting hello registry key affects all copy operations that are made toonetwork shares.</span></span>

## <a name="need-help-contact-support"></a><span data-ttu-id="1302e-215">Potrzebujesz pomocy?</span><span class="sxs-lookup"><span data-stu-id="1302e-215">Need help?</span></span> <span data-ttu-id="1302e-216">Skontaktuj się z pomocą techniczną.</span><span class="sxs-lookup"><span data-stu-id="1302e-216">Contact support.</span></span>
<span data-ttu-id="1302e-217">Jeśli nadal potrzebujesz pomocy, [się z pomocą techniczną](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget szybkie rozwiązanie problemu.</span><span class="sxs-lookup"><span data-stu-id="1302e-217">If you still need help, [contact support](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget your problem resolved quickly.</span></span>
