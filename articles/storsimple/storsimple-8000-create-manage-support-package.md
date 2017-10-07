---
title: "pakiet obsługi serii StorSimple 8000 aaaCreate | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate, odszyfrowywania i Edytuj pakiet obsługi dla danego urządzenia z serii StorSimple 8000."
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
ms.openlocfilehash: 857555b6ba31b1527f8f00d19818ebbec6005d0e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-a-support-package-for-storsimple-8000-series"></a><span data-ttu-id="1d0d8-103">Tworzenie i zarządzanie nimi pakiet obsługi serii StorSimple 8000</span><span class="sxs-lookup"><span data-stu-id="1d0d8-103">Create and manage a support package for StorSimple 8000 series</span></span>

## <a name="overview"></a><span data-ttu-id="1d0d8-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="1d0d8-104">Overview</span></span>

<span data-ttu-id="1d0d8-105">Pakiet obsługi StorSimple jest mechanizm łatwy w użyciu, która gromadzi wszystkie dzienniki odpowiednich tooassist Microsoft Support dotyczącą rozwiązywania problemów urządzenia StorSimple.</span><span class="sxs-lookup"><span data-stu-id="1d0d8-105">A StorSimple support package is an easy-to-use mechanism that collects all relevant logs tooassist Microsoft Support with troubleshooting any StorSimple device issues.</span></span> <span data-ttu-id="1d0d8-106">Witaj dzienniki zbierane są zaszyfrowane i skompresowane.</span><span class="sxs-lookup"><span data-stu-id="1d0d8-106">hello collected logs are encrypted and compressed.</span></span>

<span data-ttu-id="1d0d8-107">Ten samouczek zawiera instrukcje krok po kroku toocreate i zarządzaj nimi hello pakietu obsługi dla danego urządzenia z serii StorSimple 8000.</span><span class="sxs-lookup"><span data-stu-id="1d0d8-107">This tutorial includes step-by-step instructions toocreate and manage hello support package for your StorSimple 8000 series device.</span></span> <span data-ttu-id="1d0d8-108">Jeśli pracujesz z tablicą wirtualnego StorSimple, przejdź zbyt[generowanie pakietu dziennika](storsimple-ova-web-ui-admin.md#generate-a-log-package).</span><span class="sxs-lookup"><span data-stu-id="1d0d8-108">If you are working with a StorSimple Virtual Array, go too[generate a log package](storsimple-ova-web-ui-admin.md#generate-a-log-package).</span></span>

## <a name="create-a-support-package"></a><span data-ttu-id="1d0d8-109">Utwórz pakiet pomocy technicznej</span><span class="sxs-lookup"><span data-stu-id="1d0d8-109">Create a support package</span></span>

<span data-ttu-id="1d0d8-110">W niektórych przypadkach należy toomanually tworzenia pakietu obsługi hello za pomocą programu Windows PowerShell dla urządzenia StorSimple.</span><span class="sxs-lookup"><span data-stu-id="1d0d8-110">In some cases, you'll need toomanually create hello support package through Windows PowerShell for StorSimple.</span></span> <span data-ttu-id="1d0d8-111">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="1d0d8-111">For example:</span></span>

* <span data-ttu-id="1d0d8-112">Jeśli potrzebujesz tooremove poufnych informacji z dziennika plików poprzedniego toosharing z Microsoft Support.</span><span class="sxs-lookup"><span data-stu-id="1d0d8-112">If you need tooremove sensitive information from your log files prior toosharing with Microsoft Support.</span></span>
* <span data-ttu-id="1d0d8-113">Jeśli masz problemy przekazywanie pakietu hello powodu tooconnectivity problemów.</span><span class="sxs-lookup"><span data-stu-id="1d0d8-113">If you are having difficulty uploading hello package due tooconnectivity issues.</span></span>

<span data-ttu-id="1d0d8-114">Możesz udostępniać pakietu ręcznie wygenerowane pomocy technicznej firmy Microsoft Support za pośrednictwem poczty e-mail.</span><span class="sxs-lookup"><span data-stu-id="1d0d8-114">You can share your manually generated support package with Microsoft Support over email.</span></span> <span data-ttu-id="1d0d8-115">Wykonaj następujące kroki toocreate pakiet obsługi w programie Windows PowerShell dla urządzenia StorSimple hello.</span><span class="sxs-lookup"><span data-stu-id="1d0d8-115">Perform hello following steps toocreate a support package in Windows PowerShell for StorSimple.</span></span>

#### <a name="toocreate-a-support-package-in-windows-powershell-for-storsimple"></a><span data-ttu-id="1d0d8-116">toocreate pakiet obsługi w programie Windows PowerShell dla urządzenia StorSimple</span><span class="sxs-lookup"><span data-stu-id="1d0d8-116">toocreate a support package in Windows PowerShell for StorSimple</span></span>

1. <span data-ttu-id="1d0d8-117">toostart sesję programu Windows PowerShell jako administrator na komputerze zdalnym hello, który został użyty tooconnect tooyour urządzenia StorSimple, wprowadź hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="1d0d8-117">toostart a Windows PowerShell session as an administrator on hello remote computer that's used tooconnect tooyour StorSimple device, enter hello following command:</span></span>
   
    `Start PowerShell`
2. <span data-ttu-id="1d0d8-118">W sesji środowiska Windows PowerShell hello Podłącz toohello konsoli SSAdmin urządzenia:</span><span class="sxs-lookup"><span data-stu-id="1d0d8-118">In hello Windows PowerShell session, connect toohello SSAdmin Console of your device:</span></span>
   
   1. <span data-ttu-id="1d0d8-119">Witaj wiersza polecenia wpisz:</span><span class="sxs-lookup"><span data-stu-id="1d0d8-119">At hello command prompt, enter:</span></span>
     
       `$MS = New-PSSession -ComputerName <IP address for DATA 0> -Credential SSAdmin -ConfigurationName "SSAdminConsole"`
   2. <span data-ttu-id="1d0d8-120">Okno dialogowe hello otwiera wprowadź hasło administratora urządzenia.</span><span class="sxs-lookup"><span data-stu-id="1d0d8-120">In hello dialog box that opens, enter your device administrator password.</span></span> <span data-ttu-id="1d0d8-121">Witaj domyślne hasło jest _Password1_.</span><span class="sxs-lookup"><span data-stu-id="1d0d8-121">hello default password is _Password1_.</span></span>
     
      ![Okno dialogowe poświadczenie programu PowerShell](./media/storsimple-8000-create-manage-support-package/IC740962.png)
   3. <span data-ttu-id="1d0d8-123">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="1d0d8-123">Select **OK**.</span></span>
   4. <span data-ttu-id="1d0d8-124">Witaj wiersza polecenia wpisz:</span><span class="sxs-lookup"><span data-stu-id="1d0d8-124">At hello command prompt, enter:</span></span>
     
      `Enter-PSSession $MS`
3. <span data-ttu-id="1d0d8-125">W sesji hello, który zostanie otwarty wprowadź odpowiednie polecenie hello.</span><span class="sxs-lookup"><span data-stu-id="1d0d8-125">In hello session that opens, enter hello appropriate command.</span></span>
   
   * <span data-ttu-id="1d0d8-126">Udziały sieciowe, które są chronione hasłem wpisz:</span><span class="sxs-lookup"><span data-stu-id="1d0d8-126">For network shares that are password protected, enter:</span></span>
     
       `Export-HcsSupportPackage –PackageTag "MySupportPackage" –Credential "Username" -Force`
     
       <span data-ttu-id="1d0d8-127">Zostanie wyświetlony monit o hasło, ścieżka folderu udostępnionego toohello sieci oraz hasło szyfrowania (ponieważ pakietu obsługi hello jest zaszyfrowany).</span><span class="sxs-lookup"><span data-stu-id="1d0d8-127">You'll be prompted for a password, a path toohello network shared folder, and an encryption passphrase (because hello support package is encrypted).</span></span> <span data-ttu-id="1d0d8-128">W określonym folderze hello zostanie utworzona pakiet obsługi.</span><span class="sxs-lookup"><span data-stu-id="1d0d8-128">A support package is then created in hello specified folder.</span></span>
   * <span data-ttu-id="1d0d8-129">W przypadku udziałów, które nie są chronione hasłem, nie trzeba hello `-Credential` parametru.</span><span class="sxs-lookup"><span data-stu-id="1d0d8-129">For shares that are not password protected, you do not need hello `-Credential` parameter.</span></span> <span data-ttu-id="1d0d8-130">Wprowadź poniżej hello:</span><span class="sxs-lookup"><span data-stu-id="1d0d8-130">Enter hello following:</span></span>
     
       `Export-HcsSupportPackage –PackageTag "MySupportPackage" -Force`
     
       <span data-ttu-id="1d0d8-131">Pakiet pomocy technicznej Hello został utworzony dla obu kontrolerów w folderze udostępnionym hello określonej sieci.</span><span class="sxs-lookup"><span data-stu-id="1d0d8-131">hello support package is created for both controllers in hello specified network shared folder.</span></span> <span data-ttu-id="1d0d8-132">Jest to plik zaszyfrowanych, skompresowanych, który można wysłać tooMicrosoft pomocy technicznej do rozwiązywania problemów.</span><span class="sxs-lookup"><span data-stu-id="1d0d8-132">It's an encrypted, compressed file that can be sent tooMicrosoft Support for troubleshooting.</span></span> <span data-ttu-id="1d0d8-133">Aby uzyskać więcej informacji, zobacz [skontaktuj się z pomocą techniczną firmy Microsoft](storsimple-8000-contact-microsoft-support.md).</span><span class="sxs-lookup"><span data-stu-id="1d0d8-133">For more information, see [Contact Microsoft Support](storsimple-8000-contact-microsoft-support.md).</span></span>

### <a name="hello-export-hcssupportpackage-cmdlet-parameters"></a><span data-ttu-id="1d0d8-134">Parametry polecenia cmdlet Hello HcsSupportPackage eksportu</span><span class="sxs-lookup"><span data-stu-id="1d0d8-134">hello Export-HcsSupportPackage cmdlet parameters</span></span>

<span data-ttu-id="1d0d8-135">Można użyć następujących parametrów polecenia cmdlet hello HcsSupportPackage eksportu hello.</span><span class="sxs-lookup"><span data-stu-id="1d0d8-135">You can use hello following parameters with hello Export-HcsSupportPackage cmdlet.</span></span>

| <span data-ttu-id="1d0d8-136">Parametr</span><span class="sxs-lookup"><span data-stu-id="1d0d8-136">Parameter</span></span> | <span data-ttu-id="1d0d8-137">Wymagane opcjonalne</span><span class="sxs-lookup"><span data-stu-id="1d0d8-137">Required/Optional</span></span> | <span data-ttu-id="1d0d8-138">Opis</span><span class="sxs-lookup"><span data-stu-id="1d0d8-138">Description</span></span> |
| --- | --- | --- |
| `-Path` |<span data-ttu-id="1d0d8-139">Wymagane</span><span class="sxs-lookup"><span data-stu-id="1d0d8-139">Required</span></span> |<span data-ttu-id="1d0d8-140">Użyj lokalizacji hello tooprovide sieciowy folder udostępniony hello, w których hello znajduje się pakiet pomocy technicznej.</span><span class="sxs-lookup"><span data-stu-id="1d0d8-140">Use tooprovide hello location of hello network shared folder in which hello support package is placed.</span></span> |
| `-EncryptionPassphrase` |<span data-ttu-id="1d0d8-141">Wymagane</span><span class="sxs-lookup"><span data-stu-id="1d0d8-141">Required</span></span> |<span data-ttu-id="1d0d8-142">Użyj tooprovide toohelp hasło szyfrowania hello pakietu obsługi.</span><span class="sxs-lookup"><span data-stu-id="1d0d8-142">Use tooprovide a passphrase toohelp encrypt hello support package.</span></span> |
| `-Credential` |<span data-ttu-id="1d0d8-143">Optional (Opcjonalność)</span><span class="sxs-lookup"><span data-stu-id="1d0d8-143">Optional</span></span> |<span data-ttu-id="1d0d8-144">Użyj poświadczeń dostępu toosupply dla hello udostępnionego folderu sieciowego.</span><span class="sxs-lookup"><span data-stu-id="1d0d8-144">Use toosupply access credentials for hello network shared folder.</span></span> |
| `-Force` |<span data-ttu-id="1d0d8-145">Optional (Opcjonalność)</span><span class="sxs-lookup"><span data-stu-id="1d0d8-145">Optional</span></span> |<span data-ttu-id="1d0d8-146">Użyj tooskip hello szyfrowania hasła potwierdzenie kroku.</span><span class="sxs-lookup"><span data-stu-id="1d0d8-146">Use tooskip hello encryption passphrase confirmation step.</span></span> |
| `-PackageTag` |<span data-ttu-id="1d0d8-147">Optional (Opcjonalność)</span><span class="sxs-lookup"><span data-stu-id="1d0d8-147">Optional</span></span> |<span data-ttu-id="1d0d8-148">Użyj toospecify w katalogu *ścieżki* w obsłudze hello, który znajduje się pakiet.</span><span class="sxs-lookup"><span data-stu-id="1d0d8-148">Use toospecify a directory under *Path* in which hello support package is placed.</span></span> <span data-ttu-id="1d0d8-149">Domyślna Hello to [nazwa]-[bieżącą datę i time:yyyy-MM-dd-HH-mm-ss].</span><span class="sxs-lookup"><span data-stu-id="1d0d8-149">hello default is [device name]-[current date and time:yyyy-MM-dd-HH-mm-ss].</span></span> |
| `-Scope` |<span data-ttu-id="1d0d8-150">Optional (Opcjonalność)</span><span class="sxs-lookup"><span data-stu-id="1d0d8-150">Optional</span></span> |<span data-ttu-id="1d0d8-151">Określ jako **klastra** toocreate (ustawienie domyślne) pakiet obsługi dla obu kontrolerów.</span><span class="sxs-lookup"><span data-stu-id="1d0d8-151">Specify as **Cluster** (default) toocreate a support package for both controllers.</span></span> <span data-ttu-id="1d0d8-152">Jeśli tylko dla bieżącego kontrolera hello toocreate pakietu, określić **kontrolera**.</span><span class="sxs-lookup"><span data-stu-id="1d0d8-152">If you want toocreate a package only for hello current controller, specify **Controller**.</span></span> |

## <a name="edit-a-support-package"></a><span data-ttu-id="1d0d8-153">Edytuj pakiet pomocy technicznej</span><span class="sxs-lookup"><span data-stu-id="1d0d8-153">Edit a support package</span></span>

<span data-ttu-id="1d0d8-154">Po wygenerowaniu pakietu obsługi może być konieczne tooedit hello pakietu tooremove poufne informacje.</span><span class="sxs-lookup"><span data-stu-id="1d0d8-154">After you have generated a support package, you might need tooedit hello package tooremove sensitive information.</span></span> <span data-ttu-id="1d0d8-155">Mogą to być nazwy woluminów, urządzenia adresów IP i nazwy kopii zapasowej z plików dziennika hello.</span><span class="sxs-lookup"><span data-stu-id="1d0d8-155">This can include volume names, device IP addresses, and backup names from hello log files.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1d0d8-156">Można edytować tylko pakietu obsługi, który został wygenerowany za pomocą programu Windows PowerShell dla StorSimple.</span><span class="sxs-lookup"><span data-stu-id="1d0d8-156">You can only edit a support package that was generated through Windows PowerShell for StorSimple.</span></span> <span data-ttu-id="1d0d8-157">Nie można edytować pakiet utworzony w hello portalu Azure w usłudze Menedżer StorSimple urządzenia.</span><span class="sxs-lookup"><span data-stu-id="1d0d8-157">You can't edit a package created in hello Azure portal with StorSimple Device Manager service.</span></span>

<span data-ttu-id="1d0d8-158">tooedit pakiet obsługi przed przekazaniem go w witrynie Microsoft Support hello najpierw odszyfrować pakietu obsługi hello, Edytuj pliki hello i następnie ponownie go zaszyfrować.</span><span class="sxs-lookup"><span data-stu-id="1d0d8-158">tooedit a support package before uploading it on hello Microsoft Support site, first decrypt hello support package, edit hello files, and then re-encrypt it.</span></span> <span data-ttu-id="1d0d8-159">Wykonaj następujące kroki hello.</span><span class="sxs-lookup"><span data-stu-id="1d0d8-159">Perform hello following steps.</span></span>

#### <a name="tooedit-a-support-package-in-windows-powershell-for-storsimple"></a><span data-ttu-id="1d0d8-160">tooedit pakiet obsługi w programie Windows PowerShell dla urządzenia StorSimple</span><span class="sxs-lookup"><span data-stu-id="1d0d8-160">tooedit a support package in Windows PowerShell for StorSimple</span></span>

1. <span data-ttu-id="1d0d8-161">Generowanie pakietu obsługi, jak opisano wcześniej, w [toocreate pakiet obsługi w programie Windows PowerShell dla urządzenia StorSimple](#to-create-a-support-package-in-windows-powershell-for-storsimple).</span><span class="sxs-lookup"><span data-stu-id="1d0d8-161">Generate a support package as described earlier, in [toocreate a support package in Windows PowerShell for StorSimple](#to-create-a-support-package-in-windows-powershell-for-storsimple).</span></span>
2. <span data-ttu-id="1d0d8-162">[Pobierz skrypt hello](http://gallery.technet.microsoft.com/scriptcenter/Script-to-decrypt-a-a8d1ed65) lokalnie na komputerze klienckim.</span><span class="sxs-lookup"><span data-stu-id="1d0d8-162">[Download hello script](http://gallery.technet.microsoft.com/scriptcenter/Script-to-decrypt-a-a8d1ed65) locally on your client.</span></span>
3. <span data-ttu-id="1d0d8-163">Zaimportuj moduł programu Windows PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="1d0d8-163">Import hello Windows PowerShell module.</span></span> <span data-ttu-id="1d0d8-164">Określ hello ścieżki toohello folder lokalny którego zostały pobrane hello skryptu.</span><span class="sxs-lookup"><span data-stu-id="1d0d8-164">Specify hello path toohello local folder in which you downloaded hello script.</span></span> <span data-ttu-id="1d0d8-165">Moduł hello tooimport, wprowadź:</span><span class="sxs-lookup"><span data-stu-id="1d0d8-165">tooimport hello module, enter:</span></span>
   
    `Import-module <Path toohello folder that contains hello Windows PowerShell script>`
4. <span data-ttu-id="1d0d8-166">Wszystkie pliki hello są *.aes* pliki skompresowane i szyfrowane.</span><span class="sxs-lookup"><span data-stu-id="1d0d8-166">All hello files are *.aes* files that are compressed and encrypted.</span></span> <span data-ttu-id="1d0d8-167">toodecompress i odszyfrowywania plików, wpisz:</span><span class="sxs-lookup"><span data-stu-id="1d0d8-167">toodecompress and decrypt files, enter:</span></span>
   
    `Open-HcsSupportPackage <Path toohello folder that contains support package files>`
   
    <span data-ttu-id="1d0d8-168">Należy pamiętać, że rozszerzenia rzeczywisty plik hello są teraz wyświetlane dla wszystkich plików hello.</span><span class="sxs-lookup"><span data-stu-id="1d0d8-168">Note that hello actual file extensions are now displayed for all hello files.</span></span>
   
    ![Edytuj pakiet, pomocy technicznej](./media/storsimple-8000-create-manage-support-package/IC750706.png)
5. <span data-ttu-id="1d0d8-170">Gdy zostanie wyświetlony monit o hasło szyfrowania hello, wprowadź hasło hello, który został użyty podczas tworzenia pakietu obsługi hello.</span><span class="sxs-lookup"><span data-stu-id="1d0d8-170">When you're prompted for hello encryption passphrase, enter hello passphrase that you used when hello support package was created.</span></span>
   
        cmdlet Open-HcsSupportPackage at command pipeline position 1
   
        Supply values for hello following parameters:EncryptionPassphrase: ****
6. <span data-ttu-id="1d0d8-171">Przeglądaj toohello folderu, który zawiera pliki dziennika hello.</span><span class="sxs-lookup"><span data-stu-id="1d0d8-171">Browse toohello folder that contains hello log files.</span></span> <span data-ttu-id="1d0d8-172">Ponieważ teraz zdekompresować i odszyfrować hello plików dziennika, te będą mieć oryginalnego rozszerzenia pliku.</span><span class="sxs-lookup"><span data-stu-id="1d0d8-172">Because hello log files are now decompressed and decrypted, these will have original file extensions.</span></span> <span data-ttu-id="1d0d8-173">Zmodyfikuj te pliki tooremove wszelkie informacje specyficzne dla klienta, takich jak nazwy woluminu i adresy IP urządzeń i Zapisz hello plików.</span><span class="sxs-lookup"><span data-stu-id="1d0d8-173">Modify these files tooremove any customer-specific information, such as volume names and device IP addresses, and save hello files.</span></span>
7. <span data-ttu-id="1d0d8-174">Zamknij hello pliki toocompress z gzip i szyfrowanie AES 256.</span><span class="sxs-lookup"><span data-stu-id="1d0d8-174">Close hello files toocompress them with gzip and encrypt them with AES-256.</span></span> <span data-ttu-id="1d0d8-175">Jest to szybkości i zabezpieczeń w przesyłania pakietu obsługi hello za pośrednictwem sieci.</span><span class="sxs-lookup"><span data-stu-id="1d0d8-175">This is for speed and security in transferring hello support package over a network.</span></span> <span data-ttu-id="1d0d8-176">toocompress i szyfrowania plików, wprowadź następujące hello:</span><span class="sxs-lookup"><span data-stu-id="1d0d8-176">toocompress and encrypt files, enter hello following:</span></span>
   
    `Close-HcsSupportPackage <Path toohello folder that contains support package files>`
   
    ![Edytuj pakiet, pomocy technicznej](./media/storsimple-8000-create-manage-support-package/IC750707.png)
8. <span data-ttu-id="1d0d8-178">Po wyświetleniu monitu podaj hasło szyfrowania dla pakietu obsługi zmodyfikowane hello.</span><span class="sxs-lookup"><span data-stu-id="1d0d8-178">When prompted, provide an encryption passphrase for hello modified support package.</span></span>
   
        cmdlet Close-HcsSupportPackage at command pipeline position 1
        Supply values for hello following parameters:EncryptionPassphrase: ****
9. <span data-ttu-id="1d0d8-179">Zapisz hello nowe hasło, dzięki czemu można udostępniać Microsoft Support na żądanie.</span><span class="sxs-lookup"><span data-stu-id="1d0d8-179">Write down hello new passphrase, so that you can share it with Microsoft Support when requested.</span></span>

### <a name="example-editing-files-in-a-support-package-on-a-password-protected-share"></a><span data-ttu-id="1d0d8-180">Przykład: Edytowanie plików w pakiecie pomocy technicznej w udziale chronione hasłem</span><span class="sxs-lookup"><span data-stu-id="1d0d8-180">Example: Editing files in a support package on a password-protected share</span></span>

<span data-ttu-id="1d0d8-181">Witaj poniższy przykład pokazuje, jak toodecrypt, edytować i ponownie zaszyfrować pakiet obsługi.</span><span class="sxs-lookup"><span data-stu-id="1d0d8-181">hello following example shows how toodecrypt, edit, and re-encrypt a support package.</span></span>

        PS C:\WINDOWS\system32> Import-module C:\Users\Default\StorSimple\SupportPackage\HCSSupportPackageTools.psm1

        PS C:\WINDOWS\system32> Open-HcsSupportPackage \\hcsfs\Logs\TD48\TD48Logs\C0-A\etw

        cmdlet Open-HcsSupportPackage at command pipeline position 1

        Supply values for hello following parameters:

        EncryptionPassphrase: ****

        PS C:\WINDOWS\system32> Close-HcsSupportPackage \\hcsfs\Logs\TD48\TD48Logs\C0-A\etw

        cmdlet Close-HcsSupportPackage at command pipeline position 1

        Supply values for hello following parameters:

        EncryptionPassphrase: ****

        PS C:\WINDOWS\system32>

## <a name="next-steps"></a><span data-ttu-id="1d0d8-182">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="1d0d8-182">Next steps</span></span>

* <span data-ttu-id="1d0d8-183">Dowiedz się więcej o hello [informacje zebrane w hello pakietu obsługi](https://support.microsoft.com/help/3193606/storsimple-support-packages-and-device-logs)</span><span class="sxs-lookup"><span data-stu-id="1d0d8-183">Learn about hello [information collected in hello Support package](https://support.microsoft.com/help/3193606/storsimple-support-packages-and-device-logs)</span></span>
* <span data-ttu-id="1d0d8-184">Dowiedz się, jak za[używana obsługa pakietów oraz urządzenia w dziennikach tootroubleshoot wdrożenia urządzenia](storsimple-troubleshoot-deployment.md#support-packages-and-device-logs-available-for-troubleshooting).</span><span class="sxs-lookup"><span data-stu-id="1d0d8-184">Learn how too[use support packages and device logs tootroubleshoot your device deployment](storsimple-troubleshoot-deployment.md#support-packages-and-device-logs-available-for-troubleshooting).</span></span>
* <span data-ttu-id="1d0d8-185">Dowiedz się, jak za[Użyj hello tooadminister usługi Menedżera urządzeń StorSimple, urządzenia StorSimple](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="1d0d8-185">Learn how too[use hello StorSimple Device Manager service tooadminister your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

