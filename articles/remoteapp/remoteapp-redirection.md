---
title: "Przekierowanie aaaUsing w usłudze Azure RemoteApp | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooconfigure i używanie przekierowania w usłudze RemoteApp"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 2c8c867f-4907-4f2e-9ccd-2eb82bb5b837
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: d5739a75cf606bd971268da67b2c5ff0fe5fe19b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="using-redirection-in-azure-remoteapp"></a><span data-ttu-id="caf93-103">Przy użyciu przekierowania w usłudze Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="caf93-103">Using redirection in Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="caf93-104">Usługa Azure RemoteApp nie będzie obsługiwana od 31 sierpnia 2017 r.</span><span class="sxs-lookup"><span data-stu-id="caf93-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="caf93-105">Witaj odczytu [anonsu](https://go.microsoft.com/fwlink/?linkid=821148) szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="caf93-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="caf93-106">Przekierowywanie urządzeń pozwala użytkownikom interakcję z aplikacji zdalnych przy użyciu komputera lokalnego hello urządzeń dołączonych tootheir, telefon lub tablet.</span><span class="sxs-lookup"><span data-stu-id="caf93-106">Device redirection lets your users interact with remote apps using hello devices attached tootheir local computer, phone, or tablet.</span></span> <span data-ttu-id="caf93-107">Na przykład jeśli podano Skype za pośrednictwem usługi Azure RemoteApp, użytkownika musi aparatu hello zainstalowane na ich toowork komputera za pomocą programu Skype.</span><span class="sxs-lookup"><span data-stu-id="caf93-107">For example, if you have provided Skype through Azure RemoteApp, your user needs hello camera installed on their PC toowork with Skype.</span></span> <span data-ttu-id="caf93-108">Dotyczy to również drukarki, głośniki monitorów i urządzenia peryferyjne podłączone zakresu USB.</span><span class="sxs-lookup"><span data-stu-id="caf93-108">This is also true for printers, speakers, monitors, and a range of USB-connected peripherals.</span></span>

<span data-ttu-id="caf93-109">Połączenia programów RemoteApp wykorzystuje hello protokołu RDP (Remote Desktop) i funkcja RemoteFX tooprovide przekierowania.</span><span class="sxs-lookup"><span data-stu-id="caf93-109">RemoteApp leverages hello Remote Desktop Protocol (RDP) and RemoteFX tooprovide redirection.</span></span>

## <a name="what-redirection-is-enabled-by-default"></a><span data-ttu-id="caf93-110">Jakie przekierowania jest domyślnie włączone?</span><span class="sxs-lookup"><span data-stu-id="caf93-110">What redirection is enabled by default?</span></span>
<span data-ttu-id="caf93-111">Korzystając z programów RemoteApp, po przekierowań hello są domyślnie włączone.</span><span class="sxs-lookup"><span data-stu-id="caf93-111">When you use RemoteApp, hello following redirections are enabled by default.</span></span> <span data-ttu-id="caf93-112">informacje Hello w nawiasach Pokaż hello ustawienie RDP.</span><span class="sxs-lookup"><span data-stu-id="caf93-112">hello information in parentheses show hello RDP setting.</span></span>

* <span data-ttu-id="caf93-113">Odtwarzanie dźwięków na komputerze lokalnym hello (**Odtwarzaj na tym komputerze**).</span><span class="sxs-lookup"><span data-stu-id="caf93-113">Play sounds on hello local computer (**Play on this computer**).</span></span> <span data-ttu-id="caf93-114">(audiomode:i:0)</span><span class="sxs-lookup"><span data-stu-id="caf93-114">(audiomode:i:0)</span></span>
* <span data-ttu-id="caf93-115">Przechwyć audio z komputera lokalnego hello i komputer zdalny toohello wysyłania (**Graj z tego komputera**).</span><span class="sxs-lookup"><span data-stu-id="caf93-115">Capture audio from hello local computer and send toohello remote computer (**Record from this computer**).</span></span> <span data-ttu-id="caf93-116">(audiocapturemode:i:1)</span><span class="sxs-lookup"><span data-stu-id="caf93-116">(audiocapturemode:i:1)</span></span>
* <span data-ttu-id="caf93-117">Drukowanie toolocal drukarki (redirectprinters:i:1)</span><span class="sxs-lookup"><span data-stu-id="caf93-117">Print toolocal printers (redirectprinters:i:1)</span></span>
* <span data-ttu-id="caf93-118">Porty COM (redirectcomports:i:1)</span><span class="sxs-lookup"><span data-stu-id="caf93-118">COM ports (redirectcomports:i:1)</span></span>
* <span data-ttu-id="caf93-119">Karta inteligentna urządzenia (redirectsmartcards:i:1)</span><span class="sxs-lookup"><span data-stu-id="caf93-119">Smart card device (redirectsmartcards:i:1)</span></span>
* <span data-ttu-id="caf93-120">Schowek (toocopy możliwości i Wklej) (redirectclipboard:i:1)</span><span class="sxs-lookup"><span data-stu-id="caf93-120">Clipboard (ability toocopy and paste) (redirectclipboard:i:1)</span></span>
* <span data-ttu-id="caf93-121">Wyczyść typ czcionki Wygładzanie (Zezwalaj na wygładzanie czcionek: i:1)</span><span class="sxs-lookup"><span data-stu-id="caf93-121">Clear type font smoothing (allow font smoothing:i:1)</span></span>
* <span data-ttu-id="caf93-122">Przekieruj urządzeń wszystkich obsługiwanych Plug and Play.</span><span class="sxs-lookup"><span data-stu-id="caf93-122">Redirect all supported Plug and Play devices.</span></span> <span data-ttu-id="caf93-123">(devicestoredirect:s: *)</span><span class="sxs-lookup"><span data-stu-id="caf93-123">(devicestoredirect:s:*)</span></span>

## <a name="what-other-redirection-is-available"></a><span data-ttu-id="caf93-124">Jakie inne przekierowania jest dostępny?</span><span class="sxs-lookup"><span data-stu-id="caf93-124">What other redirection is available?</span></span>
<span data-ttu-id="caf93-125">Dwie opcje przekierowania są domyślnie wyłączone:</span><span class="sxs-lookup"><span data-stu-id="caf93-125">Two redirection options are disabled by default:</span></span>

* <span data-ttu-id="caf93-126">Przekierowywanie dysków (mapowanie dysku): zamapowanych dysków w sesji zdalnej hello stają się dyski twarde komputera lokalnego.</span><span class="sxs-lookup"><span data-stu-id="caf93-126">Drive redirection (drive mapping): Your local computer's drives become mapped drives in hello remote session.</span></span> <span data-ttu-id="caf93-127">Dzięki temu możesz zapisać lub otwarte pliki z dysków lokalnych podczas pracy w sesji zdalnej hello.</span><span class="sxs-lookup"><span data-stu-id="caf93-127">This lets you save or open files from your local drives while you work in hello remote session.</span></span>
* <span data-ttu-id="caf93-128">Przekierowywaniem USB: można użyć komputera lokalnego tooyour podłączonego urządzenia USB hello hello sesji zdalnej.</span><span class="sxs-lookup"><span data-stu-id="caf93-128">USB redirection: You can use hello USB devices attached tooyour local computer within hello remote session.</span></span>

## <a name="change-your-redirection-settings-in-remoteapp"></a><span data-ttu-id="caf93-129">Zmień ustawienia przekierowywania w programie RemoteApp</span><span class="sxs-lookup"><span data-stu-id="caf93-129">Change your redirection settings in RemoteApp</span></span>
<span data-ttu-id="caf93-130">Ustawienia przekierowywania hello urządzeń dla kolekcji można zmienić za pomocą hello Microsoft Azure PowerShell przy użyciu zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="caf93-130">You can change hello device redirection settings for a collection by using hello Microsoft Azure PowerShell with SDK.</span></span> <span data-ttu-id="caf93-131">Po zainstalowaniu hello nowego środowiska PowerShell i zestawu SDK, najpierw go skonfigurować toomanage subskrypcji, jak opisano w [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="caf93-131">After you install hello new PowerShell and SDK, first configure it toomanage your subscription as described in [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="caf93-132">Następnie użyj polecenia toohello podobne, następujące właściwości niestandardowe RDP hello tooset:</span><span class="sxs-lookup"><span data-stu-id="caf93-132">Then use a command similar toohello following tooset hello custom RDP properties:</span></span>

    Set-AzureRemoteAppCollection -CollectionName <collection name>  -CustomRdpProperty "drivestoredirect:s:*`nusbdevicestoredirect:s:*"

<span data-ttu-id="caf93-133">(Należy pamiętać, że  *\`n*  jest używany jako separator poszczególnych właściwości.)</span><span class="sxs-lookup"><span data-stu-id="caf93-133">(Note that *\`n* is used as a delimiter between individual properties.)</span></span>

<span data-ttu-id="caf93-134">Lista właściwości protokołu RDP, które niestandardowe są skonfigurowane, uruchom następujące polecenie cmdlet hello tooget.</span><span class="sxs-lookup"><span data-stu-id="caf93-134">tooget a list of what custom RDP properties are configured, run hello following cmdlet.</span></span> <span data-ttu-id="caf93-135">Warto zauważyć, że tylko niestandardowe właściwości są wyświetlane jako wyniki dane wyjściowe nie hello właściwości domyślnych:</span><span class="sxs-lookup"><span data-stu-id="caf93-135">Note that only custom properties are shown as output results and not hello default properties:</span></span>  

    Get-AzureRemoteAppCollection -CollectionName <collection name>

<span data-ttu-id="caf93-136">Po ustawieniu właściwości niestandardowe należy określić wszystkie niestandardowe właściwości zawsze; w przeciwnym razie hello zostanie przywrócona ustawienia toodisabled.</span><span class="sxs-lookup"><span data-stu-id="caf93-136">When you set custom properties you must specify all custom properties each time; otherwise hello setting reverts toodisabled.</span></span>   

### <a name="common-examples"></a><span data-ttu-id="caf93-137">Typowe przykłady</span><span class="sxs-lookup"><span data-stu-id="caf93-137">Common examples</span></span>
<span data-ttu-id="caf93-138">Użyj następującego polecenia cmdlet tooenable dysku przekierowania hello:</span><span class="sxs-lookup"><span data-stu-id="caf93-138">Use hello following cmdlet tooenable drive redirection:</span></span>  

    Set-AzureRemoteAppCollection -CollectionName <collection name>  -CustomRdpProperty "drivestoredirect:s:*"

<span data-ttu-id="caf93-139">Użyj tego polecenia cmdlet tooenable przekierowania USB i dysków:</span><span class="sxs-lookup"><span data-stu-id="caf93-139">Use this cmdlet tooenable both USB and Drive redirection:</span></span>

    Set-AzureRemoteAppCollection -CollectionName <collection name>  -CustomRdpProperty "drivestoredirect:s:*`nusbdevicestoredirect:s:*"

<span data-ttu-id="caf93-140">Użyj tego polecenia cmdlet toodisable Schowka udostępniania:</span><span class="sxs-lookup"><span data-stu-id="caf93-140">Use this cmdlet toodisable clipboard sharing:</span></span>  

    Set-AzureRemoteAppCollection -CollectionName <collection name>  -CustomRdpProperty "redirectclipboard:i:0"

> [!IMPORTANT]
> <span data-ttu-id="caf93-141">Należy się toocompletely Wyloguj wszystkich użytkowników w kolekcji hello (i nie tylko odłączać) przed przetestowaniem hello zmiany.</span><span class="sxs-lookup"><span data-stu-id="caf93-141">Be sure toocompletely log off all users in hello collection (and not just disconnect them) before you test hello change.</span></span> <span data-ttu-id="caf93-142">Wyłącz Przejdź toohello całkowicie są zalogowani użytkownicy tooensure **sesji** w kolekcji hello w hello portalu Azure i wylogowania wszyscy użytkownicy, którzy są odłączone lub zalogowany.</span><span class="sxs-lookup"><span data-stu-id="caf93-142">tooensure users are completely logged off, go toohello **Sessions** tab in hello collection in hello Azure portal and log off any users who are disconnected or signed in.</span></span> <span data-ttu-id="caf93-143">Czasami może potrwać kilka sekund tooshow dyski lokalne powitania w Eksploratorze hello sesji.</span><span class="sxs-lookup"><span data-stu-id="caf93-143">Sometimes it can take several seconds for hello local drives tooshow in Explorer within hello session.</span></span>
> 
> 

## <a name="change-usb-redirection-settings-on-your-windows-client"></a><span data-ttu-id="caf93-144">Zmień ustawienia przekierowywania USB na kliencie systemu Windows</span><span class="sxs-lookup"><span data-stu-id="caf93-144">Change USB redirection settings on your Windows client</span></span>
<span data-ttu-id="caf93-145">Jeśli chcesz toouse przekierowywaniem USB na komputerze, który łączy tooRemoteApp istnieją 2 akcje, które wymagają toohappen.</span><span class="sxs-lookup"><span data-stu-id="caf93-145">If you want toouse USB redirection on a computer that connects tooRemoteApp, there are 2 actions that need toohappen.</span></span> <span data-ttu-id="caf93-146">1 - administrator musi tooenable przekierowywaniem USB na poziomie zbioru hello przy użyciu programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="caf93-146">1 - Your administrator needs tooenable USB redirection at hello collection level by using Azure PowerShell.</span></span> <span data-ttu-id="caf93-147">2 — na każdym urządzeniu, gdzie chcesz toouse przekierowywaniem USB należy tooenable zasad grupy, która pozwala.</span><span class="sxs-lookup"><span data-stu-id="caf93-147">2 - On each device where you want toouse USB redirection, you need tooenable a group policy that permits it.</span></span> <span data-ttu-id="caf93-148">Ten krok należy wykonać dla każdego użytkownika, który chce przekierowywaniem USB toouse toobe.</span><span class="sxs-lookup"><span data-stu-id="caf93-148">This step will need toobe done for each user that wants toouse USB redirection.</span></span>

> [!NOTE]
> <span data-ttu-id="caf93-149">Przekierowywaniem USB z usługą Azure RemoteApp jest obsługiwana tylko dla komputerów z systemem Windows.</span><span class="sxs-lookup"><span data-stu-id="caf93-149">USB redirection with Azure RemoteApp is only supported for Windows computers.</span></span>
> 
> 

### <a name="enable-usb-redirection-for-hello-remoteapp-collection"></a><span data-ttu-id="caf93-150">Włącz przekierowanie USB w celu hello kolekcji usługi RemoteApp</span><span class="sxs-lookup"><span data-stu-id="caf93-150">Enable USB redirection for hello RemoteApp collection</span></span>
<span data-ttu-id="caf93-151">Użyj następującego polecenia cmdlet przekierowywaniem USB tooenable na poziomie zbioru hello hello:</span><span class="sxs-lookup"><span data-stu-id="caf93-151">Use hello following cmdlet tooenable USB redirection at hello collection level:</span></span>

    Set-AzureRemoteAppCollection -CollectionName <collection_name> -CustomRdpProperty "nusbdevicestoredirect:s:*"

### <a name="enable-usb-redirection-for-hello-client-computer"></a><span data-ttu-id="caf93-152">Włącz przekierowywaniem USB do komputera klienckiego hello</span><span class="sxs-lookup"><span data-stu-id="caf93-152">Enable USB redirection for hello client computer</span></span>
<span data-ttu-id="caf93-153">ustawienia przekierowywania USB tooconfigure na komputerze:</span><span class="sxs-lookup"><span data-stu-id="caf93-153">tooconfigure USB redirection settings on your computer:</span></span>

1. <span data-ttu-id="caf93-154">Witaj Otwórz Edytor lokalnych zasad grupy (GPEDIT. MSC).</span><span class="sxs-lookup"><span data-stu-id="caf93-154">Open hello Local Group Policy Editor (GPEDIT.MSC).</span></span> <span data-ttu-id="caf93-155">(Uruchom gpedit.msc z wiersza polecenia).</span><span class="sxs-lookup"><span data-stu-id="caf93-155">(Run gpedit.msc from a command prompt.)</span></span>
2. <span data-ttu-id="caf93-156">Otwórz **komputera Konfiguracja komputera\Zasady\Szablony administracyjne\Składniki systemu Windows\Usługi usług pulpitu Podłączanie pulpitu Client\RemoteFX urządzenia przekierowywaniem USB**.</span><span class="sxs-lookup"><span data-stu-id="caf93-156">Open **Computer Configuration\Policies\Administrative Templates\Windows Components\Remote Desktop Services\Remote Desktop Connection Client\RemoteFX USB Device Redirection**.</span></span>
3. <span data-ttu-id="caf93-157">Kliknij dwukrotnie **Zezwalaj na RDP przekierowywanie inne obsługiwane urządzenia USB funkcji RemoteFX z tego komputera**.</span><span class="sxs-lookup"><span data-stu-id="caf93-157">Double-click **Allow RDP redirection of other supported RemoteFX USB devices from this computer**.</span></span>
4. <span data-ttu-id="caf93-158">Wybierz **włączone**, a następnie wybierz **administratorów i użytkowników w hello praw dostępu przekierowania USB RemoteFX**.</span><span class="sxs-lookup"><span data-stu-id="caf93-158">Select **Enabled**, and then select **Administrators and Users in hello RemoteFX USB Redirection Access Rights**.</span></span>
5. <span data-ttu-id="caf93-159">Otwórz wiersz polecenia z uprawnieniami administracyjnymi, a następnie uruchom następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="caf93-159">Open a command prompt with administrative permissions, and run hello following command:</span></span>
   
        gpupdate /force
6. <span data-ttu-id="caf93-160">Uruchom ponownie komputer hello.</span><span class="sxs-lookup"><span data-stu-id="caf93-160">Restart hello computer.</span></span>

<span data-ttu-id="caf93-161">Można również użyć toocreate narzędzia do zarządzania zasadami grupy hello i stosowanie zasad przekierowania USB powitania dla wszystkich komputerów w domenie:</span><span class="sxs-lookup"><span data-stu-id="caf93-161">You can also use hello Group Policy Management tool toocreate and apply hello USB redirection policy for all computers in your domain:</span></span>

1. <span data-ttu-id="caf93-162">Zaloguj się do kontrolera domeny hello jako administrator domeny hello.</span><span class="sxs-lookup"><span data-stu-id="caf93-162">Log into hello domain controller as hello domain administrator.</span></span>
2. <span data-ttu-id="caf93-163">Witaj Otwórz konsolę zarządzania zasadami grupy.</span><span class="sxs-lookup"><span data-stu-id="caf93-163">Open hello Group Policy Management Console.</span></span> <span data-ttu-id="caf93-164">(Kliknij **Start > Narzędzia administracyjne > Zarządzanie zasadami grupy**.)</span><span class="sxs-lookup"><span data-stu-id="caf93-164">(Click **Start > Administrative Tools > Group Policy Management**.)</span></span>
3. <span data-ttu-id="caf93-165">Przejdź toohello domenę lub jednostkę organizacyjną, dla której ma zostać toocreate hello zasad.</span><span class="sxs-lookup"><span data-stu-id="caf93-165">Navigate toohello domain or organizational unit for which you want toocreate hello policy.</span></span>
4. <span data-ttu-id="caf93-166">Kliknij prawym przyciskiem myszy **domyślne zasady domeny**, a następnie kliknij przycisk **Edytuj**.</span><span class="sxs-lookup"><span data-stu-id="caf93-166">Right-click **Default Domain Policy**, and then click **Edit**.</span></span>
5. <span data-ttu-id="caf93-167">Otwórz **komputera Konfiguracja komputera\Zasady\Szablony administracyjne\Składniki systemu Windows\Usługi usług pulpitu Podłączanie pulpitu Client\RemoteFX urządzenia przekierowywaniem USB**.</span><span class="sxs-lookup"><span data-stu-id="caf93-167">Open **Computer Configuration\Policies\Administrative Templates\Windows Components\Remote Desktop Services\Remote Desktop Connection Client\RemoteFX USB Device Redirection**.</span></span>
6. <span data-ttu-id="caf93-168">Kliknij dwukrotnie **Zezwalaj na RDP przekierowywanie inne obsługiwane urządzenia USB funkcji RemoteFX z tego komputera**.</span><span class="sxs-lookup"><span data-stu-id="caf93-168">Double-click **Allow RDP redirection of other supported RemoteFX USB devices from this computer**.</span></span>
7. <span data-ttu-id="caf93-169">Wybierz **włączone**, a następnie wybierz **administratorów i użytkowników w hello praw dostępu przekierowania USB RemoteFX**.</span><span class="sxs-lookup"><span data-stu-id="caf93-169">Select **Enabled**, and then select **Administrators and Users in hello RemoteFX USB Redirection Access Rights**.</span></span>
8. <span data-ttu-id="caf93-170">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="caf93-170">Click **OK**.</span></span>  

