---
title: "aaaCreate pakietu obsługi StorSimple | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate, odszyfrowywania i Edytuj pakiet obsługi dla urządzenia StorSimple."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: eac76f5f-5db1-4c92-af8c-54053b91e66c
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: 209aeee50e823fd2ca96ababd1d0cf3ea9cdad53
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-a-storsimple-support-package"></a><span data-ttu-id="91c05-103">Tworzenie i zarządzanie nimi pakietu obsługi StorSimple</span><span class="sxs-lookup"><span data-stu-id="91c05-103">Create and manage a StorSimple support package</span></span>
## <a name="overview"></a><span data-ttu-id="91c05-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="91c05-104">Overview</span></span>
<span data-ttu-id="91c05-105">Pakiet obsługi StorSimple jest mechanizm łatwy w użyciu, która gromadzi wszystkie dzienniki odpowiednich tooassist Microsoft Support dotyczącą rozwiązywania problemów urządzenia StorSimple.</span><span class="sxs-lookup"><span data-stu-id="91c05-105">A StorSimple support package is an easy-to-use mechanism that collects all relevant logs tooassist Microsoft Support with troubleshooting any StorSimple device issues.</span></span> <span data-ttu-id="91c05-106">Witaj dzienniki zbierane są zaszyfrowane i skompresowane.</span><span class="sxs-lookup"><span data-stu-id="91c05-106">hello collected logs are encrypted and compressed.</span></span>

<span data-ttu-id="91c05-107">Ten samouczek zawiera instrukcje krok po kroku toocreate i zarządzaj nimi hello pakietu obsługi.</span><span class="sxs-lookup"><span data-stu-id="91c05-107">This tutorial includes step-by-step instructions toocreate and manage hello support package.</span></span>

## <a name="create-and-upload-a-support-package-in-hello-azure-classic-portal"></a><span data-ttu-id="91c05-108">Utworzyć i załadować pakiet obsługi w hello klasycznego portalu Azure</span><span class="sxs-lookup"><span data-stu-id="91c05-108">Create and upload a support package in hello Azure classic portal</span></span>
<span data-ttu-id="91c05-109">Możesz utworzyć i przekazać lokacji obsługi pakietu toohello Support firmy Microsoft za pośrednictwem hello **konserwacji** strony usługi hello w hello klasycznego portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="91c05-109">You can create and upload a support package toohello Microsoft Support site through hello **Maintenance** page of hello service in hello Azure classic portal.</span></span>

> [!NOTE]
> <span data-ttu-id="91c05-110">przekazywanie Hello wymaga klucza dostępu pomocy technicznej.</span><span class="sxs-lookup"><span data-stu-id="91c05-110">hello upload requires a support passkey.</span></span> <span data-ttu-id="91c05-111">Specjalistą pomocy technicznej powinien zapewnić tym tooyou w wiadomości e-mail.</span><span class="sxs-lookup"><span data-stu-id="91c05-111">Your support engineer should provide this tooyou in an email.</span></span>
> 
> 

<span data-ttu-id="91c05-112">Pakiet obsługi zaszyfrowane i skompresowane (plik .cab) jest utworzony i przekazane toohello witrynę pomocy technicznej.</span><span class="sxs-lookup"><span data-stu-id="91c05-112">An encrypted and compressed support package (.cab file) is created and uploaded toohello Support site.</span></span> <span data-ttu-id="91c05-113">Hello inżynier pomocy technicznej może następnie pobrać tego pakietu z hello witrynę pomocy technicznej, aby rozwiązać problem hello.</span><span class="sxs-lookup"><span data-stu-id="91c05-113">hello support engineer can then retrieve this package from hello Support site for troubleshooting hello issue.</span></span>

<span data-ttu-id="91c05-114">Wykonaj następujące kroki w hello klasycznego portalu toocreate pakietu obsługi hello.</span><span class="sxs-lookup"><span data-stu-id="91c05-114">Perform hello following steps in hello classic portal toocreate a support package.</span></span>

#### <a name="toocreate-a-support-package-in-hello-azure-classic-portal"></a><span data-ttu-id="91c05-115">toocreate pakiet pomocy technicznej w hello klasycznego portalu Azure</span><span class="sxs-lookup"><span data-stu-id="91c05-115">toocreate a support package in hello Azure classic portal</span></span>
1. <span data-ttu-id="91c05-116">Wybierz **urządzeń** > **konserwacji**.</span><span class="sxs-lookup"><span data-stu-id="91c05-116">Select **Devices** > **Maintenance**.</span></span>
2. <span data-ttu-id="91c05-117">W hello **pakietu obsługi** zaznacz **tworzenie i przekazywanie pakietu obsługi**.</span><span class="sxs-lookup"><span data-stu-id="91c05-117">In hello **Support package** section, select **Create and upload support package**.</span></span>
3. <span data-ttu-id="91c05-118">W hello **tworzenie i przekazywanie pakietu obsługi** okna dialogowego pozycję hello następujące:</span><span class="sxs-lookup"><span data-stu-id="91c05-118">In hello **Create and upload support package** dialog box, do hello following:</span></span>
   
    ![Utwórz pakiet pomocy technicznej](./media/storsimple-create-manage-support-package/IC740923.png)
   
   * <span data-ttu-id="91c05-120">W hello **klucz dostępu pomocy technicznej** tekst Wprowadź hello klucz dostępu.</span><span class="sxs-lookup"><span data-stu-id="91c05-120">In hello **Support Passkey** text box, enter hello passkey.</span></span> <span data-ttu-id="91c05-121">Specjalistą pomocy technicznej firmy Microsoft należy wysłać ten klucz dostępu tooyou w wiadomości e-mail.</span><span class="sxs-lookup"><span data-stu-id="91c05-121">Your Microsoft support engineer should send this passkey tooyou in email.</span></span>
   * <span data-ttu-id="91c05-122">Wybierz hello pole wyboru tooprovide zgody tooautomatically przekazywania hello pomocy technicznej pakietu toohello Microsoft Support lokację.</span><span class="sxs-lookup"><span data-stu-id="91c05-122">Select hello check box tooprovide consent tooautomatically upload hello support package toohello Microsoft Support site.</span></span>
   * <span data-ttu-id="91c05-123">Kliknij ikonę znacznika wyboru hello</span><span class="sxs-lookup"><span data-stu-id="91c05-123">Click hello check icon</span></span> ![Ikona znacznika wyboru](./media/storsimple-create-manage-support-package/IC740895.png)<span data-ttu-id="91c05-125">.</span><span class="sxs-lookup"><span data-stu-id="91c05-125">.</span></span>

## <a name="manually-create-a-support-package"></a><span data-ttu-id="91c05-126">Ręcznie Utwórz pakiet pomocy technicznej</span><span class="sxs-lookup"><span data-stu-id="91c05-126">Manually create a support package</span></span>
<span data-ttu-id="91c05-127">W niektórych przypadkach należy toomanually tworzenia pakietu obsługi hello za pomocą programu Windows PowerShell dla urządzenia StorSimple.</span><span class="sxs-lookup"><span data-stu-id="91c05-127">In some cases, you'll need toomanually create hello support package through Windows PowerShell for StorSimple.</span></span> <span data-ttu-id="91c05-128">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="91c05-128">For example:</span></span>

* <span data-ttu-id="91c05-129">Jeśli potrzebujesz tooremove poufnych informacji z dziennika plików poprzedniego toosharing z Microsoft Support.</span><span class="sxs-lookup"><span data-stu-id="91c05-129">If you need tooremove sensitive information from your log files prior toosharing with Microsoft Support.</span></span>
* <span data-ttu-id="91c05-130">Jeśli masz problemy przekazywanie pakietu hello powodu tooconnectivity problemów.</span><span class="sxs-lookup"><span data-stu-id="91c05-130">If you are having difficulty uploading hello package due tooconnectivity issues.</span></span>

<span data-ttu-id="91c05-131">Możesz udostępniać pakietu ręcznie wygenerowane pomocy technicznej firmy Microsoft Support za pośrednictwem poczty e-mail.</span><span class="sxs-lookup"><span data-stu-id="91c05-131">You can share your manually generated support package with Microsoft Support over email.</span></span> <span data-ttu-id="91c05-132">Wykonaj następujące kroki toocreate pakiet obsługi w programie Windows PowerShell dla urządzenia StorSimple hello.</span><span class="sxs-lookup"><span data-stu-id="91c05-132">Perform hello following steps toocreate a support package in Windows PowerShell for StorSimple.</span></span>

#### <a name="toocreate-a-support-package-in-windows-powershell-for-storsimple"></a><span data-ttu-id="91c05-133">toocreate pakiet obsługi w programie Windows PowerShell dla urządzenia StorSimple</span><span class="sxs-lookup"><span data-stu-id="91c05-133">toocreate a support package in Windows PowerShell for StorSimple</span></span>
1. <span data-ttu-id="91c05-134">toostart sesję programu Windows PowerShell jako administrator na komputerze zdalnym hello, który został użyty tooconnect tooyour urządzenia StorSimple, wprowadź hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="91c05-134">toostart a Windows PowerShell session as an administrator on hello remote computer that's used tooconnect tooyour StorSimple device, enter hello following command:</span></span>
   
    `Start PowerShell`
2. <span data-ttu-id="91c05-135">W sesji środowiska Windows PowerShell hello Podłącz toohello konsoli SSAdmin urządzenia:</span><span class="sxs-lookup"><span data-stu-id="91c05-135">In hello Windows PowerShell session, connect toohello SSAdmin Console of your device:</span></span>
   
   * <span data-ttu-id="91c05-136">Witaj wiersza polecenia wpisz:</span><span class="sxs-lookup"><span data-stu-id="91c05-136">At hello command prompt, enter:</span></span>
     
       `$MS = New-PSSession -ComputerName <IP address for DATA 0> -Credential SSAdmin -ConfigurationName "SSAdminConsole"`
   * <span data-ttu-id="91c05-137">Okno dialogowe hello otwiera wprowadź hasło administratora urządzenia.</span><span class="sxs-lookup"><span data-stu-id="91c05-137">In hello dialog box that opens, enter your device administrator password.</span></span> <span data-ttu-id="91c05-138">Witaj domyślne hasło jest:</span><span class="sxs-lookup"><span data-stu-id="91c05-138">hello default password is:</span></span>
     
      `Password1`
     
      ![Okno dialogowe poświadczenie programu PowerShell](./media/storsimple-create-manage-support-package/IC740962.png)
   * <span data-ttu-id="91c05-140">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="91c05-140">Select **OK**.</span></span>
   * <span data-ttu-id="91c05-141">Witaj wiersza polecenia wpisz:</span><span class="sxs-lookup"><span data-stu-id="91c05-141">At hello command prompt, enter:</span></span>
     
      `Enter-PSSession $MS`
3. <span data-ttu-id="91c05-142">W sesji hello, który zostanie otwarty wprowadź odpowiednie polecenie hello.</span><span class="sxs-lookup"><span data-stu-id="91c05-142">In hello session that opens, enter hello appropriate command.</span></span>
   
   * <span data-ttu-id="91c05-143">Udziały sieciowe, które są chronione hasłem wpisz:</span><span class="sxs-lookup"><span data-stu-id="91c05-143">For network shares that are password protected, enter:</span></span>
     
       `Export-HcsSupportPackage –PackageTag "MySupportPackage" –Credential "Username" -Force`
     
       <span data-ttu-id="91c05-144">Zostanie wyświetlony monit o hasło, ścieżka folderu udostępnionego toohello sieci oraz hasło szyfrowania (ponieważ pakietu obsługi hello jest zaszyfrowany).</span><span class="sxs-lookup"><span data-stu-id="91c05-144">You'll be prompted for a password, a path toohello network shared folder, and an encryption passphrase (because hello support package is encrypted).</span></span> <span data-ttu-id="91c05-145">W określonym folderze hello zostanie utworzona pakiet obsługi.</span><span class="sxs-lookup"><span data-stu-id="91c05-145">A support package is then created in hello specified folder.</span></span>
   * <span data-ttu-id="91c05-146">W przypadku udziałów, które nie są chronione hasłem, nie trzeba hello `-Credential` parametru.</span><span class="sxs-lookup"><span data-stu-id="91c05-146">For shares that are not password protected, you do not need hello `-Credential` parameter.</span></span> <span data-ttu-id="91c05-147">Wprowadź poniżej hello:</span><span class="sxs-lookup"><span data-stu-id="91c05-147">Enter hello following:</span></span>
     
       `Export-HcsSupportPackage –PackageTag "MySupportPackage" -Force`
     
       <span data-ttu-id="91c05-148">Pakiet pomocy technicznej Hello został utworzony dla obu kontrolerów w folderze udostępnionym hello określonej sieci.</span><span class="sxs-lookup"><span data-stu-id="91c05-148">hello support package is created for both controllers in hello specified network shared folder.</span></span> <span data-ttu-id="91c05-149">Jest to plik zaszyfrowanych, skompresowanych, który można wysłać tooMicrosoft pomocy technicznej do rozwiązywania problemów.</span><span class="sxs-lookup"><span data-stu-id="91c05-149">It's an encrypted, compressed file that can be sent tooMicrosoft Support for troubleshooting.</span></span> <span data-ttu-id="91c05-150">Aby uzyskać więcej informacji, zobacz [skontaktuj się z pomocą techniczną firmy Microsoft](storsimple-contact-microsoft-support.md).</span><span class="sxs-lookup"><span data-stu-id="91c05-150">For more information, see [Contact Microsoft Support](storsimple-contact-microsoft-support.md).</span></span>

### <a name="hello-export-hcssupportpackage-cmdlet-parameters"></a><span data-ttu-id="91c05-151">Parametry polecenia cmdlet Hello HcsSupportPackage eksportu</span><span class="sxs-lookup"><span data-stu-id="91c05-151">hello Export-HcsSupportPackage cmdlet parameters</span></span>
<span data-ttu-id="91c05-152">Można użyć następujących parametrów polecenia cmdlet hello HcsSupportPackage eksportu hello.</span><span class="sxs-lookup"><span data-stu-id="91c05-152">You can use hello following parameters with hello Export-HcsSupportPackage cmdlet.</span></span>

| <span data-ttu-id="91c05-153">Parametr</span><span class="sxs-lookup"><span data-stu-id="91c05-153">Parameter</span></span> | <span data-ttu-id="91c05-154">Wymagane opcjonalne</span><span class="sxs-lookup"><span data-stu-id="91c05-154">Required/Optional</span></span> | <span data-ttu-id="91c05-155">Opis</span><span class="sxs-lookup"><span data-stu-id="91c05-155">Description</span></span> |
| --- | --- | --- |
| `-Path` |<span data-ttu-id="91c05-156">Wymagane</span><span class="sxs-lookup"><span data-stu-id="91c05-156">Required</span></span> |<span data-ttu-id="91c05-157">Użyj lokalizacji hello tooprovide sieciowy folder udostępniony hello, w których hello znajduje się pakiet pomocy technicznej.</span><span class="sxs-lookup"><span data-stu-id="91c05-157">Use tooprovide hello location of hello network shared folder in which hello support package is placed.</span></span> |
| `-EncryptionPassphrase` |<span data-ttu-id="91c05-158">Wymagane</span><span class="sxs-lookup"><span data-stu-id="91c05-158">Required</span></span> |<span data-ttu-id="91c05-159">Użyj tooprovide toohelp hasło szyfrowania hello pakietu obsługi.</span><span class="sxs-lookup"><span data-stu-id="91c05-159">Use tooprovide a passphrase toohelp encrypt hello support package.</span></span> |
| `-Credential` |<span data-ttu-id="91c05-160">Optional (Opcjonalność)</span><span class="sxs-lookup"><span data-stu-id="91c05-160">Optional</span></span> |<span data-ttu-id="91c05-161">Użyj poświadczeń dostępu toosupply dla hello udostępnionego folderu sieciowego.</span><span class="sxs-lookup"><span data-stu-id="91c05-161">Use toosupply access credentials for hello network shared folder.</span></span> |
| `-Force` |<span data-ttu-id="91c05-162">Optional (Opcjonalność)</span><span class="sxs-lookup"><span data-stu-id="91c05-162">Optional</span></span> |<span data-ttu-id="91c05-163">Użyj tooskip hello szyfrowania hasła potwierdzenie kroku.</span><span class="sxs-lookup"><span data-stu-id="91c05-163">Use tooskip hello encryption passphrase confirmation step.</span></span> |
| `-PackageTag` |<span data-ttu-id="91c05-164">Optional (Opcjonalność)</span><span class="sxs-lookup"><span data-stu-id="91c05-164">Optional</span></span> |<span data-ttu-id="91c05-165">Użyj toospecify w katalogu *ścieżki* w obsłudze hello, który znajduje się pakiet.</span><span class="sxs-lookup"><span data-stu-id="91c05-165">Use toospecify a directory under *Path* in which hello support package is placed.</span></span> <span data-ttu-id="91c05-166">Domyślna Hello to [nazwa]-[bieżącą datę i time:yyyy-MM-dd-HH-mm-ss].</span><span class="sxs-lookup"><span data-stu-id="91c05-166">hello default is [device name]-[current date and time:yyyy-MM-dd-HH-mm-ss].</span></span> |
| `-Scope` |<span data-ttu-id="91c05-167">Optional (Opcjonalność)</span><span class="sxs-lookup"><span data-stu-id="91c05-167">Optional</span></span> |<span data-ttu-id="91c05-168">Określ jako **klastra** toocreate (ustawienie domyślne) pakiet obsługi dla obu kontrolerów.</span><span class="sxs-lookup"><span data-stu-id="91c05-168">Specify as **Cluster** (default) toocreate a support package for both controllers.</span></span> <span data-ttu-id="91c05-169">Jeśli tylko dla bieżącego kontrolera hello toocreate pakietu, określić **kontrolera**.</span><span class="sxs-lookup"><span data-stu-id="91c05-169">If you want toocreate a package only for hello current controller, specify **Controller**.</span></span> |

## <a name="edit-a-support-package"></a><span data-ttu-id="91c05-170">Edytuj pakiet pomocy technicznej</span><span class="sxs-lookup"><span data-stu-id="91c05-170">Edit a support package</span></span>
<span data-ttu-id="91c05-171">Po wygenerowaniu pakietu obsługi może być konieczne tooedit hello pakietu tooremove poufne informacje.</span><span class="sxs-lookup"><span data-stu-id="91c05-171">After you have generated a support package, you might need tooedit hello package tooremove sensitive information.</span></span> <span data-ttu-id="91c05-172">Mogą to być nazwy woluminów, urządzenia adresów IP i nazwy kopii zapasowej z plików dziennika hello.</span><span class="sxs-lookup"><span data-stu-id="91c05-172">This can include volume names, device IP addresses, and backup names from hello log files.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="91c05-173">Można edytować tylko pakietu obsługi, który został wygenerowany za pomocą programu Windows PowerShell dla StorSimple.</span><span class="sxs-lookup"><span data-stu-id="91c05-173">You can only edit a support package that was generated through Windows PowerShell for StorSimple.</span></span> <span data-ttu-id="91c05-174">Nie można edytować pakiet utworzony w hello klasycznego portalu Azure w usłudze Menedżer StorSimple.</span><span class="sxs-lookup"><span data-stu-id="91c05-174">You can't edit a package created in hello Azure classic portal with StorSimple Manager service.</span></span>
> 
> 

<span data-ttu-id="91c05-175">tooedit pakiet obsługi przed przekazaniem go w witrynie Microsoft Support hello najpierw odszyfrować pakietu obsługi hello, Edytuj pliki hello i następnie ponownie go zaszyfrować.</span><span class="sxs-lookup"><span data-stu-id="91c05-175">tooedit a support package before uploading it on hello Microsoft Support site, first decrypt hello support package, edit hello files, and then re-encrypt it.</span></span> <span data-ttu-id="91c05-176">Wykonaj następujące kroki hello.</span><span class="sxs-lookup"><span data-stu-id="91c05-176">Perform hello following steps.</span></span>

#### <a name="tooedit-a-support-package-in-windows-powershell-for-storsimple"></a><span data-ttu-id="91c05-177">tooedit pakiet obsługi w programie Windows PowerShell dla urządzenia StorSimple</span><span class="sxs-lookup"><span data-stu-id="91c05-177">tooedit a support package in Windows PowerShell for StorSimple</span></span>
1. <span data-ttu-id="91c05-178">Generowanie pakietu obsługi, jak opisano wcześniej, w [toocreate pakiet obsługi w programie Windows PowerShell dla urządzenia StorSimple](#to-create-a-support-package-in-windows-powershell-for-storsimple).</span><span class="sxs-lookup"><span data-stu-id="91c05-178">Generate a support package as described earlier, in [toocreate a support package in Windows PowerShell for StorSimple](#to-create-a-support-package-in-windows-powershell-for-storsimple).</span></span>
2. <span data-ttu-id="91c05-179">[Pobierz skrypt hello](http://gallery.technet.microsoft.com/scriptcenter/Script-to-decrypt-a-a8d1ed65) lokalnie na komputerze klienckim.</span><span class="sxs-lookup"><span data-stu-id="91c05-179">[Download hello script](http://gallery.technet.microsoft.com/scriptcenter/Script-to-decrypt-a-a8d1ed65) locally on your client.</span></span>
3. <span data-ttu-id="91c05-180">Zaimportuj moduł programu Windows PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="91c05-180">Import hello Windows PowerShell module.</span></span> <span data-ttu-id="91c05-181">Określ hello ścieżki toohello folder lokalny którego zostały pobrane hello skryptu.</span><span class="sxs-lookup"><span data-stu-id="91c05-181">Specify hello path toohello local folder in which you downloaded hello script.</span></span> <span data-ttu-id="91c05-182">Moduł hello tooimport, wprowadź:</span><span class="sxs-lookup"><span data-stu-id="91c05-182">tooimport hello module, enter:</span></span>
   
    `Import-module <Path toohello folder that contains hello Windows PowerShell script>`
4. <span data-ttu-id="91c05-183">Wszystkie pliki hello są *.aes* pliki skompresowane i szyfrowane.</span><span class="sxs-lookup"><span data-stu-id="91c05-183">All hello files are *.aes* files that are compressed and encrypted.</span></span> <span data-ttu-id="91c05-184">toodecompress i odszyfrowywania plików, wpisz:</span><span class="sxs-lookup"><span data-stu-id="91c05-184">toodecompress and decrypt files, enter:</span></span>
   
    `Open-HcsSupportPackage <Path toohello folder that contains support package files>`
   
    <span data-ttu-id="91c05-185">Należy pamiętać, że rozszerzenia rzeczywisty plik hello są teraz wyświetlane dla wszystkich plików hello.</span><span class="sxs-lookup"><span data-stu-id="91c05-185">Note that hello actual file extensions are now displayed for all hello files.</span></span>
   
    ![Edytuj pakiet, pomocy technicznej](./media/storsimple-create-manage-support-package/IC750706.png)
5. <span data-ttu-id="91c05-187">Gdy zostanie wyświetlony monit o hasło szyfrowania hello, wprowadź hasło hello, który został użyty podczas tworzenia pakietu obsługi hello.</span><span class="sxs-lookup"><span data-stu-id="91c05-187">When you're prompted for hello encryption passphrase, enter hello passphrase that you used when hello support package was created.</span></span>
   
        cmdlet Open-HcsSupportPackage at command pipeline position 1
   
        Supply values for hello following parameters:EncryptionPassphrase: ****
6. <span data-ttu-id="91c05-188">Przeglądaj toohello folderu, który zawiera pliki dziennika hello.</span><span class="sxs-lookup"><span data-stu-id="91c05-188">Browse toohello folder that contains hello log files.</span></span> <span data-ttu-id="91c05-189">Ponieważ teraz zdekompresować i odszyfrować hello plików dziennika, te będą mieć oryginalnego rozszerzenia pliku.</span><span class="sxs-lookup"><span data-stu-id="91c05-189">Because hello log files are now decompressed and decrypted, these will have original file extensions.</span></span> <span data-ttu-id="91c05-190">Zmodyfikuj te pliki tooremove wszelkie informacje specyficzne dla klienta, takich jak nazwy woluminu i adresy IP urządzeń i Zapisz hello plików.</span><span class="sxs-lookup"><span data-stu-id="91c05-190">Modify these files tooremove any customer-specific information, such as volume names and device IP addresses, and save hello files.</span></span>
7. <span data-ttu-id="91c05-191">Zamknij hello pliki toocompress z gzip i szyfrowanie AES 256.</span><span class="sxs-lookup"><span data-stu-id="91c05-191">Close hello files toocompress them with gzip and encrypt them with AES-256.</span></span> <span data-ttu-id="91c05-192">Jest to szybkości i zabezpieczeń w przesyłania pakietu obsługi hello za pośrednictwem sieci.</span><span class="sxs-lookup"><span data-stu-id="91c05-192">This is for speed and security in transferring hello support package over a network.</span></span> <span data-ttu-id="91c05-193">toocompress i szyfrowania plików, wprowadź następujące hello:</span><span class="sxs-lookup"><span data-stu-id="91c05-193">toocompress and encrypt files, enter hello following:</span></span>
   
    `Close-HcsSupportPackage <Path toohello folder that contains support package files>`
   
    ![Edytuj pakiet, pomocy technicznej](./media/storsimple-create-manage-support-package/IC750707.png)
8. <span data-ttu-id="91c05-195">Po wyświetleniu monitu podaj hasło szyfrowania dla pakietu obsługi zmodyfikowane hello.</span><span class="sxs-lookup"><span data-stu-id="91c05-195">When prompted, provide an encryption passphrase for hello modified support package.</span></span>
   
        cmdlet Close-HcsSupportPackage at command pipeline position 1
        Supply values for hello following parameters:EncryptionPassphrase: ****
9. <span data-ttu-id="91c05-196">Zapisz hello nowe hasło, dzięki czemu można udostępniać Microsoft Support na żądanie.</span><span class="sxs-lookup"><span data-stu-id="91c05-196">Write down hello new passphrase, so that you can share it with Microsoft Support when requested.</span></span>

### <a name="example-editing-files-in-a-support-package-on-a-password-protected-share"></a><span data-ttu-id="91c05-197">Przykład: Edytowanie plików w pakiecie pomocy technicznej w udziale chronione hasłem</span><span class="sxs-lookup"><span data-stu-id="91c05-197">Example: Editing files in a support package on a password-protected share</span></span>
<span data-ttu-id="91c05-198">Witaj poniższy przykład pokazuje, jak toodecrypt, edytować i ponownie zaszyfrować pakiet obsługi.</span><span class="sxs-lookup"><span data-stu-id="91c05-198">hello following example shows how toodecrypt, edit, and re-encrypt a support package.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="91c05-199">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="91c05-199">Next steps</span></span>
* <span data-ttu-id="91c05-200">Dowiedz się, jak za[używana obsługa pakietów oraz urządzenia w dziennikach tootroubleshoot wdrożenia urządzenia](storsimple-troubleshoot-deployment.md#support-packages-and-device-logs-available-for-troubleshooting).</span><span class="sxs-lookup"><span data-stu-id="91c05-200">Learn how too[use support packages and device logs tootroubleshoot your device deployment](storsimple-troubleshoot-deployment.md#support-packages-and-device-logs-available-for-troubleshooting).</span></span>
* <span data-ttu-id="91c05-201">Dowiedz się, jak za[Użyj hello tooadminister usługi Menedżer StorSimple, urządzenia StorSimple](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="91c05-201">Learn how too[use hello StorSimple Manager service tooadminister your StorSimple device](storsimple-manager-service-administration.md).</span></span>

