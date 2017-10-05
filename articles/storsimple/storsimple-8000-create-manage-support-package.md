---
title: "Utwórz pakiet obsługi serii StorSimple 8000 | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tworzyć, odszyfrowywania i edytować pakiet obsługi dla danego urządzenia z serii StorSimple 8000."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/05/2017
ms.author: alkohli
ms.openlocfilehash: 92abbb96b2117e10800de61b5c405a784453265b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-manage-a-support-package-for-storsimple-8000-series"></a><span data-ttu-id="b226d-103">Tworzenie i zarządzanie nimi pakiet obsługi serii StorSimple 8000</span><span class="sxs-lookup"><span data-stu-id="b226d-103">Create and manage a support package for StorSimple 8000 series</span></span>

## <a name="overview"></a><span data-ttu-id="b226d-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="b226d-104">Overview</span></span>

<span data-ttu-id="b226d-105">Pakiet obsługi StorSimple jest mechanizm łatwy w użyciu, która gromadzi wszystkie dzienniki odpowiednich pomagające Microsoft Support żadnych problemów urządzenia StorSimple.</span><span class="sxs-lookup"><span data-stu-id="b226d-105">A StorSimple support package is an easy-to-use mechanism that collects all relevant logs to assist Microsoft Support with troubleshooting any StorSimple device issues.</span></span> <span data-ttu-id="b226d-106">Dzienniki zbierane są zaszyfrowane i skompresowane.</span><span class="sxs-lookup"><span data-stu-id="b226d-106">The collected logs are encrypted and compressed.</span></span>

<span data-ttu-id="b226d-107">Ten samouczek zawiera instrukcje krok po kroku, aby utworzyć i zarządzać pakietu obsługi dla danego urządzenia z serii StorSimple 8000.</span><span class="sxs-lookup"><span data-stu-id="b226d-107">This tutorial includes step-by-step instructions to create and manage the support package for your StorSimple 8000 series device.</span></span> <span data-ttu-id="b226d-108">Jeśli pracujesz z tablicą wirtualnego StorSimple, przejdź do [generowanie pakietu dziennika](storsimple-ova-web-ui-admin.md#generate-a-log-package).</span><span class="sxs-lookup"><span data-stu-id="b226d-108">If you are working with a StorSimple Virtual Array, go to [generate a log package](storsimple-ova-web-ui-admin.md#generate-a-log-package).</span></span>

## <a name="create-a-support-package"></a><span data-ttu-id="b226d-109">Utwórz pakiet pomocy technicznej</span><span class="sxs-lookup"><span data-stu-id="b226d-109">Create a support package</span></span>

<span data-ttu-id="b226d-110">W niektórych przypadkach należy ręcznie utworzyć pakiet pomocy technicznej za pośrednictwem programu Windows PowerShell dla urządzenia StorSimple.</span><span class="sxs-lookup"><span data-stu-id="b226d-110">In some cases, you'll need to manually create the support package through Windows PowerShell for StorSimple.</span></span> <span data-ttu-id="b226d-111">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="b226d-111">For example:</span></span>

* <span data-ttu-id="b226d-112">Jeśli musisz usunąć poufne informacje z plików dziennika przed udostępnianie Support firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="b226d-112">If you need to remove sensitive information from your log files prior to sharing with Microsoft Support.</span></span>
* <span data-ttu-id="b226d-113">Jeśli masz problemy przekazywanie pakietu z powodu problemów z łącznością.</span><span class="sxs-lookup"><span data-stu-id="b226d-113">If you are having difficulty uploading the package due to connectivity issues.</span></span>

<span data-ttu-id="b226d-114">Możesz udostępniać pakietu ręcznie wygenerowane pomocy technicznej firmy Microsoft Support za pośrednictwem poczty e-mail.</span><span class="sxs-lookup"><span data-stu-id="b226d-114">You can share your manually generated support package with Microsoft Support over email.</span></span> <span data-ttu-id="b226d-115">Wykonaj poniższe kroki, aby utworzyć pakiet obsługi w programie Windows PowerShell dla StorSimple.</span><span class="sxs-lookup"><span data-stu-id="b226d-115">Perform the following steps to create a support package in Windows PowerShell for StorSimple.</span></span>

#### <a name="to-create-a-support-package-in-windows-powershell-for-storsimple"></a><span data-ttu-id="b226d-116">Aby utworzyć pakiet pomocy technicznej w programie Windows PowerShell dla urządzenia StorSimple</span><span class="sxs-lookup"><span data-stu-id="b226d-116">To create a support package in Windows PowerShell for StorSimple</span></span>

1. <span data-ttu-id="b226d-117">Aby rozpocząć sesję programu Windows PowerShell jako administrator na komputerze zdalnym, który jest używany do nawiązania połączenia urządzenia StorSimple, wprowadź następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="b226d-117">To start a Windows PowerShell session as an administrator on the remote computer that's used to connect to your StorSimple device, enter the following command:</span></span>
   
    `Start PowerShell`
2. <span data-ttu-id="b226d-118">W sesji środowiska Windows PowerShell połączenie z konsolą SSAdmin urządzenia:</span><span class="sxs-lookup"><span data-stu-id="b226d-118">In the Windows PowerShell session, connect to the SSAdmin Console of your device:</span></span>
   
   1. <span data-ttu-id="b226d-119">W wierszu polecenia wpisz:</span><span class="sxs-lookup"><span data-stu-id="b226d-119">At the command prompt, enter:</span></span>
     
       `$MS = New-PSSession -ComputerName <IP address for DATA 0> -Credential SSAdmin -ConfigurationName "SSAdminConsole"`
   2. <span data-ttu-id="b226d-120">W otwartym oknie dialogowym Wprowadź hasło administratora urządzenia.</span><span class="sxs-lookup"><span data-stu-id="b226d-120">In the dialog box that opens, enter your device administrator password.</span></span> <span data-ttu-id="b226d-121">Domyślne hasło jest _Password1_.</span><span class="sxs-lookup"><span data-stu-id="b226d-121">The default password is _Password1_.</span></span>
     
      ![Okno dialogowe poświadczenie programu PowerShell](./media/storsimple-8000-create-manage-support-package/IC740962.png)
   3. <span data-ttu-id="b226d-123">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="b226d-123">Select **OK**.</span></span>
   4. <span data-ttu-id="b226d-124">W wierszu polecenia wpisz:</span><span class="sxs-lookup"><span data-stu-id="b226d-124">At the command prompt, enter:</span></span>
     
      `Enter-PSSession $MS`
3. <span data-ttu-id="b226d-125">W sesji, który zostanie otwarty wprowadź odpowiednie polecenie.</span><span class="sxs-lookup"><span data-stu-id="b226d-125">In the session that opens, enter the appropriate command.</span></span>
   
   * <span data-ttu-id="b226d-126">Udziały sieciowe, które są chronione hasłem wpisz:</span><span class="sxs-lookup"><span data-stu-id="b226d-126">For network shares that are password protected, enter:</span></span>
     
       `Export-HcsSupportPackage –PackageTag "MySupportPackage" –Credential "Username" -Force`
     
       <span data-ttu-id="b226d-127">Zostanie wyświetlony monit o podanie hasła, ścieżka do udostępnionego folderu sieciowego i hasło szyfrowania (ponieważ pakietu obsługi jest zaszyfrowany).</span><span class="sxs-lookup"><span data-stu-id="b226d-127">You'll be prompted for a password, a path to the network shared folder, and an encryption passphrase (because the support package is encrypted).</span></span> <span data-ttu-id="b226d-128">Pakiet obsługi jest tworzona w określonym folderze.</span><span class="sxs-lookup"><span data-stu-id="b226d-128">A support package is then created in the specified folder.</span></span>
   * <span data-ttu-id="b226d-129">W przypadku udziałów, które nie są chronione hasłem, nie trzeba `-Credential` parametru.</span><span class="sxs-lookup"><span data-stu-id="b226d-129">For shares that are not password protected, you do not need the `-Credential` parameter.</span></span> <span data-ttu-id="b226d-130">Wprowadź następujące informacje:</span><span class="sxs-lookup"><span data-stu-id="b226d-130">Enter the following:</span></span>
     
       `Export-HcsSupportPackage –PackageTag "MySupportPackage" -Force`
     
       <span data-ttu-id="b226d-131">Dla obu kontrolerów w udostępnionym folderze sieciowym określonym zostaje utworzony pakiet pomocy technicznej.</span><span class="sxs-lookup"><span data-stu-id="b226d-131">The support package is created for both controllers in the specified network shared folder.</span></span> <span data-ttu-id="b226d-132">Jest to plik zaszyfrowanych, skompresowanych, który można wysłać do firmy Microsoft Support do rozwiązywania problemów.</span><span class="sxs-lookup"><span data-stu-id="b226d-132">It's an encrypted, compressed file that can be sent to Microsoft Support for troubleshooting.</span></span> <span data-ttu-id="b226d-133">Aby uzyskać więcej informacji, zobacz [skontaktuj się z pomocą techniczną firmy Microsoft](storsimple-8000-contact-microsoft-support.md).</span><span class="sxs-lookup"><span data-stu-id="b226d-133">For more information, see [Contact Microsoft Support](storsimple-8000-contact-microsoft-support.md).</span></span>

### <a name="the-export-hcssupportpackage-cmdlet-parameters"></a><span data-ttu-id="b226d-134">Parametry polecenia cmdlet Export-HcsSupportPackage</span><span class="sxs-lookup"><span data-stu-id="b226d-134">The Export-HcsSupportPackage cmdlet parameters</span></span>

<span data-ttu-id="b226d-135">Można używać następujących parametrów, za pomocą polecenia cmdlet Export-HcsSupportPackage.</span><span class="sxs-lookup"><span data-stu-id="b226d-135">You can use the following parameters with the Export-HcsSupportPackage cmdlet.</span></span>

| <span data-ttu-id="b226d-136">Parametr</span><span class="sxs-lookup"><span data-stu-id="b226d-136">Parameter</span></span> | <span data-ttu-id="b226d-137">Wymagane opcjonalne</span><span class="sxs-lookup"><span data-stu-id="b226d-137">Required/Optional</span></span> | <span data-ttu-id="b226d-138">Opis</span><span class="sxs-lookup"><span data-stu-id="b226d-138">Description</span></span> |
| --- | --- | --- |
| `-Path` |<span data-ttu-id="b226d-139">Wymagane</span><span class="sxs-lookup"><span data-stu-id="b226d-139">Required</span></span> |<span data-ttu-id="b226d-140">Użyj, aby podać lokalizację folderu udostępnionego sieci, w której znajduje się pakiet pomocy technicznej.</span><span class="sxs-lookup"><span data-stu-id="b226d-140">Use to provide the location of the network shared folder in which the support package is placed.</span></span> |
| `-EncryptionPassphrase` |<span data-ttu-id="b226d-141">Wymagane</span><span class="sxs-lookup"><span data-stu-id="b226d-141">Required</span></span> |<span data-ttu-id="b226d-142">Użyj, aby podać hasło, aby zaszyfrować pakiet pomocy technicznej.</span><span class="sxs-lookup"><span data-stu-id="b226d-142">Use to provide a passphrase to help encrypt the support package.</span></span> |
| `-Credential` |<span data-ttu-id="b226d-143">Optional (Opcjonalność)</span><span class="sxs-lookup"><span data-stu-id="b226d-143">Optional</span></span> |<span data-ttu-id="b226d-144">Użyj, aby podać poświadczenia dostępu do udostępnionego folderu sieciowego.</span><span class="sxs-lookup"><span data-stu-id="b226d-144">Use to supply access credentials for the network shared folder.</span></span> |
| `-Force` |<span data-ttu-id="b226d-145">Optional (Opcjonalność)</span><span class="sxs-lookup"><span data-stu-id="b226d-145">Optional</span></span> |<span data-ttu-id="b226d-146">Użyj, aby pominąć krok potwierdzenie hasła szyfrowania.</span><span class="sxs-lookup"><span data-stu-id="b226d-146">Use to skip the encryption passphrase confirmation step.</span></span> |
| `-PackageTag` |<span data-ttu-id="b226d-147">Optional (Opcjonalność)</span><span class="sxs-lookup"><span data-stu-id="b226d-147">Optional</span></span> |<span data-ttu-id="b226d-148">Użyj, aby określić katalog w *ścieżki* w znajduje się pakiet pomocy technicznej.</span><span class="sxs-lookup"><span data-stu-id="b226d-148">Use to specify a directory under *Path* in which the support package is placed.</span></span> <span data-ttu-id="b226d-149">Wartość domyślna to [nazwa]-[bieżącą datę i time:yyyy-MM-dd-HH-mm-ss].</span><span class="sxs-lookup"><span data-stu-id="b226d-149">The default is [device name]-[current date and time:yyyy-MM-dd-HH-mm-ss].</span></span> |
| `-Scope` |<span data-ttu-id="b226d-150">Optional (Opcjonalność)</span><span class="sxs-lookup"><span data-stu-id="b226d-150">Optional</span></span> |<span data-ttu-id="b226d-151">Określ jako **klastra** (ustawienie domyślne), aby utworzyć pakiet pomocy technicznej dla obu kontrolerów.</span><span class="sxs-lookup"><span data-stu-id="b226d-151">Specify as **Cluster** (default) to create a support package for both controllers.</span></span> <span data-ttu-id="b226d-152">Jeśli chcesz utworzyć pakiet tylko dla bieżącego kontrolera, określ **kontrolera**.</span><span class="sxs-lookup"><span data-stu-id="b226d-152">If you want to create a package only for the current controller, specify **Controller**.</span></span> |

## <a name="edit-a-support-package"></a><span data-ttu-id="b226d-153">Edytuj pakiet pomocy technicznej</span><span class="sxs-lookup"><span data-stu-id="b226d-153">Edit a support package</span></span>

<span data-ttu-id="b226d-154">Po wygenerowaniu pakietu obsługi może być konieczne Edytuj pakiet, aby usunąć informacje poufne.</span><span class="sxs-lookup"><span data-stu-id="b226d-154">After you have generated a support package, you might need to edit the package to remove sensitive information.</span></span> <span data-ttu-id="b226d-155">Mogą to być nazwy woluminów, urządzenia adresów IP i nazwy kopii zapasowej z plików dziennika.</span><span class="sxs-lookup"><span data-stu-id="b226d-155">This can include volume names, device IP addresses, and backup names from the log files.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b226d-156">Można edytować tylko pakietu obsługi, który został wygenerowany za pomocą programu Windows PowerShell dla StorSimple.</span><span class="sxs-lookup"><span data-stu-id="b226d-156">You can only edit a support package that was generated through Windows PowerShell for StorSimple.</span></span> <span data-ttu-id="b226d-157">Nie można edytować pakiet utworzony w portalu Azure w usłudze Menedżer StorSimple urządzenia.</span><span class="sxs-lookup"><span data-stu-id="b226d-157">You can't edit a package created in the Azure portal with StorSimple Device Manager service.</span></span>

<span data-ttu-id="b226d-158">Aby edytować pakiet obsługi przed przekazaniem go w witrynie Microsoft Support, najpierw odszyfrować pakiet pomocy technicznej, Edytuj pliki i następnie ponownie go zaszyfrować.</span><span class="sxs-lookup"><span data-stu-id="b226d-158">To edit a support package before uploading it on the Microsoft Support site, first decrypt the support package, edit the files, and then re-encrypt it.</span></span> <span data-ttu-id="b226d-159">Wykonaj poniższe kroki.</span><span class="sxs-lookup"><span data-stu-id="b226d-159">Perform the following steps.</span></span>

#### <a name="to-edit-a-support-package-in-windows-powershell-for-storsimple"></a><span data-ttu-id="b226d-160">Aby edytować pakiet obsługi w programie Windows PowerShell dla urządzenia StorSimple</span><span class="sxs-lookup"><span data-stu-id="b226d-160">To edit a support package in Windows PowerShell for StorSimple</span></span>

1. <span data-ttu-id="b226d-161">Generowanie pakietu obsługi, jak opisano wcześniej, w [do utworzenia pakietu obsługi w programie Windows PowerShell dla urządzenia StorSimple](#to-create-a-support-package-in-windows-powershell-for-storsimple).</span><span class="sxs-lookup"><span data-stu-id="b226d-161">Generate a support package as described earlier, in [To create a support package in Windows PowerShell for StorSimple](#to-create-a-support-package-in-windows-powershell-for-storsimple).</span></span>
2. <span data-ttu-id="b226d-162">[Pobierz skrypt](http://gallery.technet.microsoft.com/scriptcenter/Script-to-decrypt-a-a8d1ed65) lokalnie na komputerze klienckim.</span><span class="sxs-lookup"><span data-stu-id="b226d-162">[Download the script](http://gallery.technet.microsoft.com/scriptcenter/Script-to-decrypt-a-a8d1ed65) locally on your client.</span></span>
3. <span data-ttu-id="b226d-163">Zaimportuj moduł programu Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b226d-163">Import the Windows PowerShell module.</span></span> <span data-ttu-id="b226d-164">Określ ścieżkę do folderu lokalnego, w której skrypt został pobrany.</span><span class="sxs-lookup"><span data-stu-id="b226d-164">Specify the path to the local folder in which you downloaded the script.</span></span> <span data-ttu-id="b226d-165">Aby zaimportować moduł, wpisz:</span><span class="sxs-lookup"><span data-stu-id="b226d-165">To import the module, enter:</span></span>
   
    `Import-module <Path to the folder that contains the Windows PowerShell script>`
4. <span data-ttu-id="b226d-166">Wszystkie pliki są *.aes* pliki skompresowane i szyfrowane.</span><span class="sxs-lookup"><span data-stu-id="b226d-166">All the files are *.aes* files that are compressed and encrypted.</span></span> <span data-ttu-id="b226d-167">Aby zdekompresować i odszyfrowuje pliki, wpisz:</span><span class="sxs-lookup"><span data-stu-id="b226d-167">To decompress and decrypt files, enter:</span></span>
   
    `Open-HcsSupportPackage <Path to the folder that contains support package files>`
   
    <span data-ttu-id="b226d-168">Należy pamiętać, że rzeczywisty plik rozszerzenia są teraz wyświetlane dla wszystkich plików.</span><span class="sxs-lookup"><span data-stu-id="b226d-168">Note that the actual file extensions are now displayed for all the files.</span></span>
   
    ![Edytuj pakiet, pomocy technicznej](./media/storsimple-8000-create-manage-support-package/IC750706.png)
5. <span data-ttu-id="b226d-170">Gdy zostanie wyświetlony monit o hasło szyfrowania, wprowadź hasło, które są używane podczas tworzenia pakietu obsługi.</span><span class="sxs-lookup"><span data-stu-id="b226d-170">When you're prompted for the encryption passphrase, enter the passphrase that you used when the support package was created.</span></span>
   
        cmdlet Open-HcsSupportPackage at command pipeline position 1
   
        Supply values for the following parameters:EncryptionPassphrase: ****
6. <span data-ttu-id="b226d-171">Przejdź do folderu, który zawiera pliki dziennika.</span><span class="sxs-lookup"><span data-stu-id="b226d-171">Browse to the folder that contains the log files.</span></span> <span data-ttu-id="b226d-172">Ponieważ pliki dziennika są teraz zdekompresować i odszyfrować, te będą mieć oryginalnego rozszerzenia pliku.</span><span class="sxs-lookup"><span data-stu-id="b226d-172">Because the log files are now decompressed and decrypted, these will have original file extensions.</span></span> <span data-ttu-id="b226d-173">Zmodyfikuj te pliki, aby usunąć wszelkie informacje specyficzne dla klienta, takich jak nazwy woluminu i adresy IP urządzeń i zapisać pliki.</span><span class="sxs-lookup"><span data-stu-id="b226d-173">Modify these files to remove any customer-specific information, such as volume names and device IP addresses, and save the files.</span></span>
7. <span data-ttu-id="b226d-174">Zamknij pliki, aby kompresować gzip i szyfrowanie AES 256.</span><span class="sxs-lookup"><span data-stu-id="b226d-174">Close the files to compress them with gzip and encrypt them with AES-256.</span></span> <span data-ttu-id="b226d-175">Jest to szybkości i zabezpieczeń w przesyłania pakietu pomocy technicznej za pośrednictwem sieci.</span><span class="sxs-lookup"><span data-stu-id="b226d-175">This is for speed and security in transferring the support package over a network.</span></span> <span data-ttu-id="b226d-176">Podczas kompresji i szyfrowania plików, wprowadź następujące informacje:</span><span class="sxs-lookup"><span data-stu-id="b226d-176">To compress and encrypt files, enter the following:</span></span>
   
    `Close-HcsSupportPackage <Path to the folder that contains support package files>`
   
    ![Edytuj pakiet, pomocy technicznej](./media/storsimple-8000-create-manage-support-package/IC750707.png)
8. <span data-ttu-id="b226d-178">Po wyświetleniu monitu podaj hasło szyfrowania dla pakietu obsługi zmodyfikowane.</span><span class="sxs-lookup"><span data-stu-id="b226d-178">When prompted, provide an encryption passphrase for the modified support package.</span></span>
   
        cmdlet Close-HcsSupportPackage at command pipeline position 1
        Supply values for the following parameters:EncryptionPassphrase: ****
9. <span data-ttu-id="b226d-179">Zapisz nowe hasło, dzięki czemu można udostępniać Microsoft Support na żądanie.</span><span class="sxs-lookup"><span data-stu-id="b226d-179">Write down the new passphrase, so that you can share it with Microsoft Support when requested.</span></span>

### <a name="example-editing-files-in-a-support-package-on-a-password-protected-share"></a><span data-ttu-id="b226d-180">Przykład: Edytowanie plików w pakiecie pomocy technicznej w udziale chronione hasłem</span><span class="sxs-lookup"><span data-stu-id="b226d-180">Example: Editing files in a support package on a password-protected share</span></span>

<span data-ttu-id="b226d-181">Poniższy przykład pokazuje, jak można odszyfrować, edytować i ponownie zaszyfrować pakiet obsługi.</span><span class="sxs-lookup"><span data-stu-id="b226d-181">The following example shows how to decrypt, edit, and re-encrypt a support package.</span></span>

        PS C:\WINDOWS\system32> Import-module C:\Users\Default\StorSimple\SupportPackage\HCSSupportPackageTools.psm1

        PS C:\WINDOWS\system32> Open-HcsSupportPackage \\hcsfs\Logs\TD48\TD48Logs\C0-A\etw

        cmdlet Open-HcsSupportPackage at command pipeline position 1

        Supply values for the following parameters:

        EncryptionPassphrase: ****

        PS C:\WINDOWS\system32> Close-HcsSupportPackage \\hcsfs\Logs\TD48\TD48Logs\C0-A\etw

        cmdlet Close-HcsSupportPackage at command pipeline position 1

        Supply values for the following parameters:

        EncryptionPassphrase: ****

        PS C:\WINDOWS\system32>

## <a name="next-steps"></a><span data-ttu-id="b226d-182">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b226d-182">Next steps</span></span>

* <span data-ttu-id="b226d-183">Dowiedz się więcej o [informacje zebrane w pakietu obsługi](https://support.microsoft.com/help/3193606/storsimple-support-packages-and-device-logs)</span><span class="sxs-lookup"><span data-stu-id="b226d-183">Learn about the [information collected in the Support package](https://support.microsoft.com/help/3193606/storsimple-support-packages-and-device-logs)</span></span>
* <span data-ttu-id="b226d-184">Dowiedz się, jak [użycie pakietów pomocy technicznej i dzienniki urządzenia do rozwiązywania problemów z wdrożeniem urządzenia](storsimple-troubleshoot-deployment.md#support-packages-and-device-logs-available-for-troubleshooting).</span><span class="sxs-lookup"><span data-stu-id="b226d-184">Learn how to [use support packages and device logs to troubleshoot your device deployment](storsimple-troubleshoot-deployment.md#support-packages-and-device-logs-available-for-troubleshooting).</span></span>
* <span data-ttu-id="b226d-185">Dowiedz się, jak [zarządzać urządzenia StorSimple przy użyciu usługi Menedżer StorSimple urządzenia](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="b226d-185">Learn how to [use the StorSimple Device Manager service to administer your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

