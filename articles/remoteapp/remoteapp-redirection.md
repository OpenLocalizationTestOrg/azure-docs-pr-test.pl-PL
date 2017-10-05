---
title: "Przy użyciu przekierowania w usłudze Azure RemoteApp | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak konfigurowanie i używanie przekierowania w usłudze RemoteApp"
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
ms.openlocfilehash: b5a65d129225fde46e3b090bc3cd9427989005ee
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="using-redirection-in-azure-remoteapp"></a><span data-ttu-id="27023-103">Przy użyciu przekierowania w usłudze Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="27023-103">Using redirection in Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="27023-104">Usługa Azure RemoteApp nie będzie obsługiwana od 31 sierpnia 2017 r.</span><span class="sxs-lookup"><span data-stu-id="27023-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="27023-105">Szczegółowe informacje zawiera [powiadomienie](https://go.microsoft.com/fwlink/?linkid=821148).</span><span class="sxs-lookup"><span data-stu-id="27023-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="27023-106">Przekierowywanie urządzeń pozwala użytkownikom interakcję z aplikacji zdalnych przy użyciu urządzenia podłączone do ich komputera lokalnego, telefon lub tablet.</span><span class="sxs-lookup"><span data-stu-id="27023-106">Device redirection lets your users interact with remote apps using the devices attached to their local computer, phone, or tablet.</span></span> <span data-ttu-id="27023-107">Na przykład jeśli podano Skype za pośrednictwem usługi Azure RemoteApp, użytkownika musi aparatu zainstalowana na danym komputerze do pracy za pomocą programu Skype.</span><span class="sxs-lookup"><span data-stu-id="27023-107">For example, if you have provided Skype through Azure RemoteApp, your user needs the camera installed on their PC to work with Skype.</span></span> <span data-ttu-id="27023-108">Dotyczy to również drukarki, głośniki monitorów i urządzenia peryferyjne podłączone zakresu USB.</span><span class="sxs-lookup"><span data-stu-id="27023-108">This is also true for printers, speakers, monitors, and a range of USB-connected peripherals.</span></span>

<span data-ttu-id="27023-109">Połączenia programów RemoteApp korzysta z protokołu RDP (Remote Desktop) i funkcja RemoteFX do przekierowywania.</span><span class="sxs-lookup"><span data-stu-id="27023-109">RemoteApp leverages the Remote Desktop Protocol (RDP) and RemoteFX to provide redirection.</span></span>

## <a name="what-redirection-is-enabled-by-default"></a><span data-ttu-id="27023-110">Jakie przekierowania jest domyślnie włączone?</span><span class="sxs-lookup"><span data-stu-id="27023-110">What redirection is enabled by default?</span></span>
<span data-ttu-id="27023-111">Gdy używasz usługi RemoteApp są domyślnie włączone następujące przekierowań.</span><span class="sxs-lookup"><span data-stu-id="27023-111">When you use RemoteApp, the following redirections are enabled by default.</span></span> <span data-ttu-id="27023-112">Informacje zawarte w nawiasach Pokaż ustawienia protokołu RDP.</span><span class="sxs-lookup"><span data-stu-id="27023-112">The information in parentheses show the RDP setting.</span></span>

* <span data-ttu-id="27023-113">Odtwarzanie dźwięków na komputerze lokalnym (**Odtwarzaj na tym komputerze**).</span><span class="sxs-lookup"><span data-stu-id="27023-113">Play sounds on the local computer (**Play on this computer**).</span></span> <span data-ttu-id="27023-114">(audiomode:i:0)</span><span class="sxs-lookup"><span data-stu-id="27023-114">(audiomode:i:0)</span></span>
* <span data-ttu-id="27023-115">Przechwyć audio z komputera lokalnego i wysłać do komputera zdalnego (**Graj z tego komputera**).</span><span class="sxs-lookup"><span data-stu-id="27023-115">Capture audio from the local computer and send to the remote computer (**Record from this computer**).</span></span> <span data-ttu-id="27023-116">(audiocapturemode:i:1)</span><span class="sxs-lookup"><span data-stu-id="27023-116">(audiocapturemode:i:1)</span></span>
* <span data-ttu-id="27023-117">Drukowanie do drukarek lokalnych (redirectprinters:i:1)</span><span class="sxs-lookup"><span data-stu-id="27023-117">Print to local printers (redirectprinters:i:1)</span></span>
* <span data-ttu-id="27023-118">Porty COM (redirectcomports:i:1)</span><span class="sxs-lookup"><span data-stu-id="27023-118">COM ports (redirectcomports:i:1)</span></span>
* <span data-ttu-id="27023-119">Karta inteligentna urządzenia (redirectsmartcards:i:1)</span><span class="sxs-lookup"><span data-stu-id="27023-119">Smart card device (redirectsmartcards:i:1)</span></span>
* <span data-ttu-id="27023-120">Schowek (możliwość kopiowania i wklejania) (redirectclipboard:i:1)</span><span class="sxs-lookup"><span data-stu-id="27023-120">Clipboard (ability to copy and paste) (redirectclipboard:i:1)</span></span>
* <span data-ttu-id="27023-121">Wyczyść typ czcionki Wygładzanie (Zezwalaj na wygładzanie czcionek: i:1)</span><span class="sxs-lookup"><span data-stu-id="27023-121">Clear type font smoothing (allow font smoothing:i:1)</span></span>
* <span data-ttu-id="27023-122">Przekieruj urządzeń wszystkich obsługiwanych Plug and Play.</span><span class="sxs-lookup"><span data-stu-id="27023-122">Redirect all supported Plug and Play devices.</span></span> <span data-ttu-id="27023-123">(devicestoredirect:s: *)</span><span class="sxs-lookup"><span data-stu-id="27023-123">(devicestoredirect:s:*)</span></span>

## <a name="what-other-redirection-is-available"></a><span data-ttu-id="27023-124">Jakie inne przekierowania jest dostępny?</span><span class="sxs-lookup"><span data-stu-id="27023-124">What other redirection is available?</span></span>
<span data-ttu-id="27023-125">Dwie opcje przekierowania są domyślnie wyłączone:</span><span class="sxs-lookup"><span data-stu-id="27023-125">Two redirection options are disabled by default:</span></span>

* <span data-ttu-id="27023-126">Przekierowywanie dysków (mapowanie dysku): zamapowanych dysków w sesji zdalnej stają się dyski twarde komputera lokalnego.</span><span class="sxs-lookup"><span data-stu-id="27023-126">Drive redirection (drive mapping): Your local computer's drives become mapped drives in the remote session.</span></span> <span data-ttu-id="27023-127">Dzięki temu możesz zapisać lub otwarte pliki z dysków lokalnych podczas pracy w sesji zdalnej.</span><span class="sxs-lookup"><span data-stu-id="27023-127">This lets you save or open files from your local drives while you work in the remote session.</span></span>
* <span data-ttu-id="27023-128">Przekierowywaniem USB: można używać urządzeń USB podłączone do komputera lokalnego w sesji zdalnej.</span><span class="sxs-lookup"><span data-stu-id="27023-128">USB redirection: You can use the USB devices attached to your local computer within the remote session.</span></span>

## <a name="change-your-redirection-settings-in-remoteapp"></a><span data-ttu-id="27023-129">Zmień ustawienia przekierowywania w programie RemoteApp</span><span class="sxs-lookup"><span data-stu-id="27023-129">Change your redirection settings in RemoteApp</span></span>
<span data-ttu-id="27023-130">Ustawienia przekierowywania urządzeń dla kolekcji można zmienić za pomocą programu Microsoft Azure PowerShell przy użyciu zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="27023-130">You can change the device redirection settings for a collection by using the Microsoft Azure PowerShell with SDK.</span></span> <span data-ttu-id="27023-131">Po zainstalowaniu nowego środowiska PowerShell i zestawu SDK, najpierw go skonfigurować do zarządzania subskrypcją, zgodnie z opisem w [jak instalowanie i konfigurowanie programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="27023-131">After you install the new PowerShell and SDK, first configure it to manage your subscription as described in [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="27023-132">Można ustawić właściwości niestandardowe RDP używać polecenie podobne do następującego:</span><span class="sxs-lookup"><span data-stu-id="27023-132">Then use a command similar to the following to set the custom RDP properties:</span></span>

    Set-AzureRemoteAppCollection -CollectionName <collection name>  -CustomRdpProperty "drivestoredirect:s:*`nusbdevicestoredirect:s:*"

<span data-ttu-id="27023-133">(Należy pamiętać, że  *\`n*  jest używany jako separator poszczególnych właściwości.)</span><span class="sxs-lookup"><span data-stu-id="27023-133">(Note that *\`n* is used as a delimiter between individual properties.)</span></span>

<span data-ttu-id="27023-134">Aby uzyskać listę właściwości protokołu RDP, które niestandardowe są skonfigurowane, uruchom następujące polecenie cmdlet.</span><span class="sxs-lookup"><span data-stu-id="27023-134">To get a list of what custom RDP properties are configured, run the following cmdlet.</span></span> <span data-ttu-id="27023-135">Należy pamiętać, że tylko niestandardowe właściwości są wyświetlane jako wynik i nie domyślne właściwości:</span><span class="sxs-lookup"><span data-stu-id="27023-135">Note that only custom properties are shown as output results and not the default properties:</span></span>  

    Get-AzureRemoteAppCollection -CollectionName <collection name>

<span data-ttu-id="27023-136">Po ustawieniu właściwości niestandardowe należy określić wszystkie niestandardowe właściwości zawsze; w przeciwnym razie ustawienie umożliwia przywrócenie na wyłączone.</span><span class="sxs-lookup"><span data-stu-id="27023-136">When you set custom properties you must specify all custom properties each time; otherwise the setting reverts to disabled.</span></span>   

### <a name="common-examples"></a><span data-ttu-id="27023-137">Typowe przykłady</span><span class="sxs-lookup"><span data-stu-id="27023-137">Common examples</span></span>
<span data-ttu-id="27023-138">Aby włączyć przekierowywanie dysków, użyj następującego polecenia cmdlet:</span><span class="sxs-lookup"><span data-stu-id="27023-138">Use the following cmdlet to enable drive redirection:</span></span>  

    Set-AzureRemoteAppCollection -CollectionName <collection name>  -CustomRdpProperty "drivestoredirect:s:*"

<span data-ttu-id="27023-139">Użyj następującego polecenia cmdlet do włączenia USB i dysków przekierowania:</span><span class="sxs-lookup"><span data-stu-id="27023-139">Use this cmdlet to enable both USB and Drive redirection:</span></span>

    Set-AzureRemoteAppCollection -CollectionName <collection name>  -CustomRdpProperty "drivestoredirect:s:*`nusbdevicestoredirect:s:*"

<span data-ttu-id="27023-140">To polecenie cmdlet umożliwia wyłączenie funkcji udostępniania Schowka:</span><span class="sxs-lookup"><span data-stu-id="27023-140">Use this cmdlet to disable clipboard sharing:</span></span>  

    Set-AzureRemoteAppCollection -CollectionName <collection name>  -CustomRdpProperty "redirectclipboard:i:0"

> [!IMPORTANT]
> <span data-ttu-id="27023-141">Pamiętaj całkowicie Wyloguj wszystkich użytkowników w kolekcji (a nie tylko odłączać) przed przetestowaniem zmiany.</span><span class="sxs-lookup"><span data-stu-id="27023-141">Be sure to completely log off all users in the collection (and not just disconnect them) before you test the change.</span></span> <span data-ttu-id="27023-142">Aby upewnić się, użytkownicy są całkowicie wylogowani, przejdź do **sesji** w kolekcji w portalu Azure i wylogowania wszyscy użytkownicy, którzy są odłączone lub zalogowany.</span><span class="sxs-lookup"><span data-stu-id="27023-142">To ensure users are completely logged off, go to the **Sessions** tab in the collection in the Azure portal and log off any users who are disconnected or signed in.</span></span> <span data-ttu-id="27023-143">Czasami może potrwać kilka sekund na dyskach lokalnych można wyświetlić w Eksploratorze w ramach sesji.</span><span class="sxs-lookup"><span data-stu-id="27023-143">Sometimes it can take several seconds for the local drives to show in Explorer within the session.</span></span>
> 
> 

## <a name="change-usb-redirection-settings-on-your-windows-client"></a><span data-ttu-id="27023-144">Zmień ustawienia przekierowywania USB na kliencie systemu Windows</span><span class="sxs-lookup"><span data-stu-id="27023-144">Change USB redirection settings on your Windows client</span></span>
<span data-ttu-id="27023-145">Jeśli chcesz użyć przekierowywaniem USB na komputerze, który łączy się RemoteApp, istnieją 2 akcje, które muszą mieć miejsce.</span><span class="sxs-lookup"><span data-stu-id="27023-145">If you want to use USB redirection on a computer that connects to RemoteApp, there are 2 actions that need to happen.</span></span> <span data-ttu-id="27023-146">1 - administrator musi włączyć przekierowywanie USB na poziomie kolekcji przy użyciu programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="27023-146">1 - Your administrator needs to enable USB redirection at the collection level by using Azure PowerShell.</span></span> <span data-ttu-id="27023-147">2 — na każdym urządzeniu, na którym ma być używany z przekierowywaniem USB musisz włączyć zasady grupy, która pozwala.</span><span class="sxs-lookup"><span data-stu-id="27023-147">2 - On each device where you want to use USB redirection, you need to enable a group policy that permits it.</span></span> <span data-ttu-id="27023-148">Ten krok należy wykonać dla każdego użytkownika, który chce korzystać z przekierowywaniem USB.</span><span class="sxs-lookup"><span data-stu-id="27023-148">This step will need to be done for each user that wants to use USB redirection.</span></span>

> [!NOTE]
> <span data-ttu-id="27023-149">Przekierowywaniem USB z usługą Azure RemoteApp jest obsługiwana tylko dla komputerów z systemem Windows.</span><span class="sxs-lookup"><span data-stu-id="27023-149">USB redirection with Azure RemoteApp is only supported for Windows computers.</span></span>
> 
> 

### <a name="enable-usb-redirection-for-the-remoteapp-collection"></a><span data-ttu-id="27023-150">Włącz przekierowywaniem USB kolekcji usługi RemoteApp</span><span class="sxs-lookup"><span data-stu-id="27023-150">Enable USB redirection for the RemoteApp collection</span></span>
<span data-ttu-id="27023-151">Aby włączyć przekierowywaniem USB na poziomie kolekcji, użyj następującego polecenia cmdlet:</span><span class="sxs-lookup"><span data-stu-id="27023-151">Use the following cmdlet to enable USB redirection at the collection level:</span></span>

    Set-AzureRemoteAppCollection -CollectionName <collection_name> -CustomRdpProperty "nusbdevicestoredirect:s:*"

### <a name="enable-usb-redirection-for-the-client-computer"></a><span data-ttu-id="27023-152">Włącz przekierowywaniem USB do komputera klienckiego</span><span class="sxs-lookup"><span data-stu-id="27023-152">Enable USB redirection for the client computer</span></span>
<span data-ttu-id="27023-153">Aby skonfigurować ustawienia przekierowywania USB na komputerze:</span><span class="sxs-lookup"><span data-stu-id="27023-153">To configure USB redirection settings on your computer:</span></span>

1. <span data-ttu-id="27023-154">Otwórz Edytor lokalnych zasad grupy (GPEDIT. MSC).</span><span class="sxs-lookup"><span data-stu-id="27023-154">Open the Local Group Policy Editor (GPEDIT.MSC).</span></span> <span data-ttu-id="27023-155">(Uruchom gpedit.msc z wiersza polecenia).</span><span class="sxs-lookup"><span data-stu-id="27023-155">(Run gpedit.msc from a command prompt.)</span></span>
2. <span data-ttu-id="27023-156">Otwórz **komputera Konfiguracja komputera\Zasady\Szablony administracyjne\Składniki systemu Windows\Usługi usług pulpitu Podłączanie pulpitu Client\RemoteFX urządzenia przekierowywaniem USB**.</span><span class="sxs-lookup"><span data-stu-id="27023-156">Open **Computer Configuration\Policies\Administrative Templates\Windows Components\Remote Desktop Services\Remote Desktop Connection Client\RemoteFX USB Device Redirection**.</span></span>
3. <span data-ttu-id="27023-157">Kliknij dwukrotnie **Zezwalaj na RDP przekierowywanie inne obsługiwane urządzenia USB funkcji RemoteFX z tego komputera**.</span><span class="sxs-lookup"><span data-stu-id="27023-157">Double-click **Allow RDP redirection of other supported RemoteFX USB devices from this computer**.</span></span>
4. <span data-ttu-id="27023-158">Wybierz **włączone**, a następnie wybierz **administratorów i użytkowników w prawa dostępu przekierowania USB RemoteFX**.</span><span class="sxs-lookup"><span data-stu-id="27023-158">Select **Enabled**, and then select **Administrators and Users in the RemoteFX USB Redirection Access Rights**.</span></span>
5. <span data-ttu-id="27023-159">Otwórz wiersz polecenia z uprawnieniami administracyjnymi i uruchom następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="27023-159">Open a command prompt with administrative permissions, and run the following command:</span></span>
   
        gpupdate /force
6. <span data-ttu-id="27023-160">Uruchom ponownie komputer.</span><span class="sxs-lookup"><span data-stu-id="27023-160">Restart the computer.</span></span>

<span data-ttu-id="27023-161">Można także użyć narzędzia do zarządzania zasadami grupy do tworzenia i stosowania zasad przekierowania USB dla wszystkich komputerów w domenie:</span><span class="sxs-lookup"><span data-stu-id="27023-161">You can also use the Group Policy Management tool to create and apply the USB redirection policy for all computers in your domain:</span></span>

1. <span data-ttu-id="27023-162">Zaloguj się do kontrolera domeny jako administrator domeny.</span><span class="sxs-lookup"><span data-stu-id="27023-162">Log into the domain controller as the domain administrator.</span></span>
2. <span data-ttu-id="27023-163">Otwórz konsolę zarządzania zasadami grupy.</span><span class="sxs-lookup"><span data-stu-id="27023-163">Open the Group Policy Management Console.</span></span> <span data-ttu-id="27023-164">(Kliknij **Start > Narzędzia administracyjne > Zarządzanie zasadami grupy**.)</span><span class="sxs-lookup"><span data-stu-id="27023-164">(Click **Start > Administrative Tools > Group Policy Management**.)</span></span>
3. <span data-ttu-id="27023-165">Przejdź do domeny lub jednostki organizacyjnej, dla której chcesz utworzyć zasady.</span><span class="sxs-lookup"><span data-stu-id="27023-165">Navigate to the domain or organizational unit for which you want to create the policy.</span></span>
4. <span data-ttu-id="27023-166">Kliknij prawym przyciskiem myszy **domyślne zasady domeny**, a następnie kliknij przycisk **Edytuj**.</span><span class="sxs-lookup"><span data-stu-id="27023-166">Right-click **Default Domain Policy**, and then click **Edit**.</span></span>
5. <span data-ttu-id="27023-167">Otwórz **komputera Konfiguracja komputera\Zasady\Szablony administracyjne\Składniki systemu Windows\Usługi usług pulpitu Podłączanie pulpitu Client\RemoteFX urządzenia przekierowywaniem USB**.</span><span class="sxs-lookup"><span data-stu-id="27023-167">Open **Computer Configuration\Policies\Administrative Templates\Windows Components\Remote Desktop Services\Remote Desktop Connection Client\RemoteFX USB Device Redirection**.</span></span>
6. <span data-ttu-id="27023-168">Kliknij dwukrotnie **Zezwalaj na RDP przekierowywanie inne obsługiwane urządzenia USB funkcji RemoteFX z tego komputera**.</span><span class="sxs-lookup"><span data-stu-id="27023-168">Double-click **Allow RDP redirection of other supported RemoteFX USB devices from this computer**.</span></span>
7. <span data-ttu-id="27023-169">Wybierz **włączone**, a następnie wybierz **administratorów i użytkowników w prawa dostępu przekierowania USB RemoteFX**.</span><span class="sxs-lookup"><span data-stu-id="27023-169">Select **Enabled**, and then select **Administrators and Users in the RemoteFX USB Redirection Access Rights**.</span></span>
8. <span data-ttu-id="27023-170">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="27023-170">Click **OK**.</span></span>  

