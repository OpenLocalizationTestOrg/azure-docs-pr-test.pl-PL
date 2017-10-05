---
title: "Zdalne nawiązywanie połączenia urządzenia StorSimple | Dokumentacja firmy Microsoft"
description: "Wyjaśniono, jak skonfigurować urządzenie do zdalnego zarządzania oraz sposób nawiązywania połączenia z programu Windows PowerShell dla urządzenia StorSimple za pośrednictwem protokołu HTTP lub HTTPS."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/07/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ff76884f020a0fb8a1b48bd371c419bd65e85fd3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="connect-remotely-to-your-storsimple-8000-series-device"></a><span data-ttu-id="975be-103">Zdalne nawiązywanie połączenia z urządzenia z serii StorSimple 8000</span><span class="sxs-lookup"><span data-stu-id="975be-103">Connect remotely to your StorSimple 8000 series device</span></span>

## <a name="overview"></a><span data-ttu-id="975be-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="975be-104">Overview</span></span>

<span data-ttu-id="975be-105">Możesz zdalnie nawiązać urządzenia za pomocą środowiska Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="975be-105">You can remotely connect to your device via Windows PowerShell.</span></span> <span data-ttu-id="975be-106">Po ustanowieniu połączenia w ten sposób nie ma menu.</span><span class="sxs-lookup"><span data-stu-id="975be-106">When you connect this way, you do not see a menu.</span></span> <span data-ttu-id="975be-107">(Możesz zobaczyć menu tylko wtedy, gdy używasz konsoli szeregowej urządzenia do łączenia). Przy użyciu komunikacji zdalnej programu Windows PowerShell należy nawiązać określonego obszaru działania.</span><span class="sxs-lookup"><span data-stu-id="975be-107">(You see a menu only if you use the serial console on the device to connect.) With Windows PowerShell remoting, you connect to a specific runspace.</span></span> <span data-ttu-id="975be-108">Można również określić język wyświetlania.</span><span class="sxs-lookup"><span data-stu-id="975be-108">You can also specify the display language.</span></span>

<span data-ttu-id="975be-109">Aby uzyskać więcej informacji o użyciu komunikacji zdalnej programu Windows PowerShell do zarządzania urządzeniem, przejdź do [Użyj środowiska Windows PowerShell dla urządzenia StorSimple do administrowania urządzeniem StorSimple](storsimple-8000-windows-powershell-administration.md).</span><span class="sxs-lookup"><span data-stu-id="975be-109">For more information about using Windows PowerShell remoting to manage your device, go to [Use Windows PowerShell for StorSimple to administer your StorSimple device](storsimple-8000-windows-powershell-administration.md).</span></span>

<span data-ttu-id="975be-110">W tym samouczku opisano, jak skonfigurować urządzenie do zdalnego zarządzania, a następnie sposób nawiązywania połączenia z programu Windows PowerShell dla urządzenia StorSimple.</span><span class="sxs-lookup"><span data-stu-id="975be-110">This tutorial explains how to configure your device for remote management and then how to connect to Windows PowerShell for StorSimple.</span></span> <span data-ttu-id="975be-111">Zdalne połączenia za pomocą środowiska Windows PowerShell można użyć protokołu HTTP lub HTTPS.</span><span class="sxs-lookup"><span data-stu-id="975be-111">You can use HTTP or HTTPS to remotely connect via Windows PowerShell.</span></span> <span data-ttu-id="975be-112">Jednakże wybierając sposób nawiązywania połączenia z programu Windows PowerShell dla urządzenia StorSimple, należy wziąć pod uwagę następujące informacje:</span><span class="sxs-lookup"><span data-stu-id="975be-112">However, when you are deciding how to connect to Windows PowerShell for StorSimple, consider the following information:</span></span>

* <span data-ttu-id="975be-113">Połączenie bezpośrednio z konsolą szeregową urządzenia jest bezpieczne, ale połączenie z konsolą szeregową za pośrednictwem przełączników sieciowych nie jest.</span><span class="sxs-lookup"><span data-stu-id="975be-113">Connecting directly to the device serial console is secure, but connecting to the serial console over network switches is not.</span></span> <span data-ttu-id="975be-114">Połączenie z konsolą szeregową urządzenia za pośrednictwem przełączników sieciowych, należy uważać na zagrożenie bezpieczeństwa.</span><span class="sxs-lookup"><span data-stu-id="975be-114">Be cautious of the security risk when connecting to the device serial console over network switches.</span></span>
* <span data-ttu-id="975be-115">Łączących się za pośrednictwem sesji HTTP może oferować lepsze bezpieczeństwo niż łączących się za pośrednictwem konsoli szeregowej za pośrednictwem sieci.</span><span class="sxs-lookup"><span data-stu-id="975be-115">Connecting through an HTTP session might offer more security than connecting through the serial console over the network.</span></span> <span data-ttu-id="975be-116">Chociaż nie jest najbezpieczniejszą metodą, jest dopuszczalne w zaufanych sieciach.</span><span class="sxs-lookup"><span data-stu-id="975be-116">Although this is not the most secure method, it is acceptable on trusted networks.</span></span>
* <span data-ttu-id="975be-117">Połączenie za pomocą sesji protokołu HTTPS z certyfikatu z podpisem własnym to najwyższy poziom bezpieczeństwa i zalecana opcja.</span><span class="sxs-lookup"><span data-stu-id="975be-117">Connecting through an HTTPS session with a self-signed certificate is the most secure and the recommended option.</span></span>

<span data-ttu-id="975be-118">Możesz połączyć zdalnie do interfejsu programu Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="975be-118">You can connect remotely to the Windows PowerShell interface.</span></span> <span data-ttu-id="975be-119">Jednak dostępu zdalnego do urządzenia StorSimple za pośrednictwem interfejsu programu Windows PowerShell nie jest włączona domyślnie.</span><span class="sxs-lookup"><span data-stu-id="975be-119">However, remote access to your StorSimple device via the Windows PowerShell interface is not enabled by default.</span></span> <span data-ttu-id="975be-120">Należy najpierw włączyć zdalne zarządzanie na urządzeniu, a następnie na kliencie umożliwiające dostęp do urządzenia.</span><span class="sxs-lookup"><span data-stu-id="975be-120">You must enable remote management on the device first, and then on the client that is used to access your device.</span></span>

<span data-ttu-id="975be-121">Kroki opisane w tym artykule wykonano na komputerze hosta z systemem Windows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="975be-121">The steps described in this article were performed on a host system running Windows Server 2012 R2.</span></span>

## <a name="connect-through-http"></a><span data-ttu-id="975be-122">Łączenie się za pośrednictwem protokołu HTTP</span><span class="sxs-lookup"><span data-stu-id="975be-122">Connect through HTTP</span></span>

<span data-ttu-id="975be-123">Łączenie z programu Windows PowerShell dla urządzenia StorSimple za pośrednictwem sesji HTTP oferuje lepsze zabezpieczenia niż łączących się za pośrednictwem konsoli szeregowej urządzenia StorSimple.</span><span class="sxs-lookup"><span data-stu-id="975be-123">Connecting to Windows PowerShell for StorSimple through an HTTP session offers more security than connecting through the serial console of your StorSimple device.</span></span> <span data-ttu-id="975be-124">Chociaż nie jest najbezpieczniejszą metodą, jest dopuszczalne w zaufanych sieciach.</span><span class="sxs-lookup"><span data-stu-id="975be-124">Although this is not the most secure method, it is acceptable on trusted networks.</span></span>

<span data-ttu-id="975be-125">Aby skonfigurować zdalne zarządzanie, można użyć portalu Azure lub konsoli szeregowej.</span><span class="sxs-lookup"><span data-stu-id="975be-125">You can use either the Azure portal or the serial console to configure remote management.</span></span> <span data-ttu-id="975be-126">Wybierz jedną z następujących procedur:</span><span class="sxs-lookup"><span data-stu-id="975be-126">Select from the following procedures:</span></span>

* [<span data-ttu-id="975be-127">Użyj portalu Azure, aby włączyć zdalne zarządzanie za pośrednictwem protokołu HTTP</span><span class="sxs-lookup"><span data-stu-id="975be-127">Use the Azure portal to enable remote management over HTTP</span></span>](#use-the-azure-classic-portal-to-enable-remote-management-over-http)
* [<span data-ttu-id="975be-128">Użyj konsoli szeregowej, aby włączyć zdalne zarządzanie za pośrednictwem protokołu HTTP</span><span class="sxs-lookup"><span data-stu-id="975be-128">Use the serial console to enable remote management over HTTP</span></span>](#use-the-serial-console-to-enable-remote-management-over-http)

<span data-ttu-id="975be-129">Po włączeniu zdalnego zarządzania umożliwia przygotowanie klienta dla połączenia zdalnego poniższej procedury.</span><span class="sxs-lookup"><span data-stu-id="975be-129">After you enable remote management, use the following procedure to prepare the client for a remote connection.</span></span>

* [<span data-ttu-id="975be-130">Przygotuj klienta dla połączenia zdalnego</span><span class="sxs-lookup"><span data-stu-id="975be-130">Prepare the client for remote connection</span></span>](#prepare-the-client-for-remote-connection)

### <a name="use-the-azure-portal-to-enable-remote-management-over-http"></a><span data-ttu-id="975be-131">Użyj portalu Azure, aby włączyć zdalne zarządzanie za pośrednictwem protokołu HTTP</span><span class="sxs-lookup"><span data-stu-id="975be-131">Use the Azure portal to enable remote management over HTTP</span></span>

<span data-ttu-id="975be-132">Wykonaj poniższe kroki w portalu Azure, aby włączyć zdalne zarządzanie za pośrednictwem protokołu HTTP.</span><span class="sxs-lookup"><span data-stu-id="975be-132">Perform the following steps in the Azure portal to enable remote management over HTTP.</span></span>

#### <a name="to-enable-remote-management-through-the-azure-portal"></a><span data-ttu-id="975be-133">Aby włączyć zdalne zarządzanie za pomocą portalu Azure</span><span class="sxs-lookup"><span data-stu-id="975be-133">To enable remote management through the Azure portal</span></span>

1. <span data-ttu-id="975be-134">Przejdź do usługi Menedżer urządzeń StorSimple.</span><span class="sxs-lookup"><span data-stu-id="975be-134">Go to your StorSimple Device Manager service.</span></span> <span data-ttu-id="975be-135">Wybierz **urządzeń** , a następnie wybierz i kliknij przycisk urządzenia, które chcesz skonfigurować do zdalnego zarządzania.</span><span class="sxs-lookup"><span data-stu-id="975be-135">Select **Devices** and then select and click the device you want to configure for remote management.</span></span> <span data-ttu-id="975be-136">Przejdź do **ustawienia urządzenia > zabezpieczeń**.</span><span class="sxs-lookup"><span data-stu-id="975be-136">Go to **Device settings > Security**.</span></span>
2. <span data-ttu-id="975be-137">W **ustawienia zabezpieczeń** bloku, kliknij przycisk **zdalnego zarządzania**.</span><span class="sxs-lookup"><span data-stu-id="975be-137">In the **Security settings** blade, click **Remote Management**.</span></span>
3. <span data-ttu-id="975be-138">W **zdalnego zarządzania** ustawić bloku **włączyć zdalne zarządzanie** do **tak**.</span><span class="sxs-lookup"><span data-stu-id="975be-138">In the **Remote management** blade, set **Enable Remote Management** to **Yes**.</span></span>
4. <span data-ttu-id="975be-139">Teraz możesz wybrać opcję połączenia przy użyciu protokołu HTTP.</span><span class="sxs-lookup"><span data-stu-id="975be-139">You can now choose to connect using HTTP.</span></span> <span data-ttu-id="975be-140">(Wartość domyślna to łączenie za pośrednictwem protokołu HTTPS). Upewnij się, że wybrano HTTP.</span><span class="sxs-lookup"><span data-stu-id="975be-140">(The default is to connect over HTTPS.) Make sure that HTTP is selected.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="975be-141">Łączenie za pośrednictwem protokołu HTTP jest dopuszczalne tylko w sieciach zaufanych.</span><span class="sxs-lookup"><span data-stu-id="975be-141">Connecting over HTTP is acceptable only on trusted networks.</span></span>
   
5. <span data-ttu-id="975be-142">Kliknij przycisk **zapisać** i po wyświetleniu monitu o potwierdzenie, wybierz **tak**.</span><span class="sxs-lookup"><span data-stu-id="975be-142">Click **Save** and when prompted for confirmation, select **Yes**.</span></span>

### <a name="use-the-serial-console-to-enable-remote-management-over-http"></a><span data-ttu-id="975be-143">Użyj konsoli szeregowej, aby włączyć zdalne zarządzanie za pośrednictwem protokołu HTTP</span><span class="sxs-lookup"><span data-stu-id="975be-143">Use the serial console to enable remote management over HTTP</span></span>
<span data-ttu-id="975be-144">Wykonaj następujące czynności na konsoli szeregowej urządzenia, aby włączyć zdalne zarządzanie.</span><span class="sxs-lookup"><span data-stu-id="975be-144">Perform the following steps on the device serial console to enable remote management.</span></span>

#### <a name="to-enable-remote-management-through-the-device-serial-console"></a><span data-ttu-id="975be-145">Aby włączyć zdalne zarządzanie za pośrednictwem konsoli szeregowej urządzenia</span><span class="sxs-lookup"><span data-stu-id="975be-145">To enable remote management through the device serial console</span></span>
1. <span data-ttu-id="975be-146">W menu konsoli szeregowej wybierz opcję 1.</span><span class="sxs-lookup"><span data-stu-id="975be-146">On the serial console menu, select option 1.</span></span> <span data-ttu-id="975be-147">Aby uzyskać więcej informacji na temat używania konsoli szeregowej na urządzeniu, przejdź do [Połącz z programu Windows PowerShell dla StorSimple za pośrednictwem konsoli szeregowej urządzenia](storsimple-8000-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="975be-147">For more information about using the serial console on the device, go to [Connect to Windows PowerShell for StorSimple via device serial console](storsimple-8000-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console).</span></span>
2. <span data-ttu-id="975be-148">W wierszu polecenia wpisz:`Enable-HcsRemoteManagement –AllowHttp`</span><span class="sxs-lookup"><span data-stu-id="975be-148">At the prompt, type: `Enable-HcsRemoteManagement –AllowHttp`</span></span>
3. <span data-ttu-id="975be-149">Użytkownik jest powiadamiany o luk w zabezpieczeniach systemu przy użyciu protokołu HTTP do nawiązania połączenia z urządzeniem.</span><span class="sxs-lookup"><span data-stu-id="975be-149">You are notified about the security vulnerabilities of using HTTP to connect to the device.</span></span> <span data-ttu-id="975be-150">Po wyświetleniu monitu Potwierdź, wpisując **Y**.</span><span class="sxs-lookup"><span data-stu-id="975be-150">When prompted, confirm by typing **Y**.</span></span>
4. <span data-ttu-id="975be-151">Sprawdź, czy HTTP jest włączona, wpisując:`Get-HcsSystem`</span><span class="sxs-lookup"><span data-stu-id="975be-151">Verify that HTTP is enabled by typing: `Get-HcsSystem`</span></span>
5. <span data-ttu-id="975be-152">Sprawdź, czy **RemoteManagementMode** pola pokazuje **HttpsAndHttpEnabled**. Na poniższej ilustracji przedstawiono te ustawienia w PuTTY.</span><span class="sxs-lookup"><span data-stu-id="975be-152">Verify that the **RemoteManagementMode** field shows **HttpsAndHttpEnabled**.The following illustration shows these settings in PuTTY.</span></span>
   
     ![Serial HTTPS i HTTP włączone](./media/storsimple-remote-connect/HCS_SerialHttpsAndHttpEnabled.png)

### <a name="prepare-the-client-for-remote-connection"></a><span data-ttu-id="975be-154">Przygotuj klienta dla połączenia zdalnego</span><span class="sxs-lookup"><span data-stu-id="975be-154">Prepare the client for remote connection</span></span>
<span data-ttu-id="975be-155">Wykonaj następujące czynności na komputerze klienckim, aby włączyć zdalne zarządzanie.</span><span class="sxs-lookup"><span data-stu-id="975be-155">Perform the following steps on the client to enable remote management.</span></span>

#### <a name="to-prepare-the-client-for-remote-connection"></a><span data-ttu-id="975be-156">Aby przygotować klienta dla połączenia zdalnego</span><span class="sxs-lookup"><span data-stu-id="975be-156">To prepare the client for remote connection</span></span>
1. <span data-ttu-id="975be-157">Uruchom sesję programu Windows PowerShell jako administrator.</span><span class="sxs-lookup"><span data-stu-id="975be-157">Start a Windows PowerShell session as an administrator.</span></span>
2. <span data-ttu-id="975be-158">Wpisz następujące polecenie, aby dodać adres IP urządzenia StorSimple do listy zaufanych hostów klienta:</span><span class="sxs-lookup"><span data-stu-id="975be-158">Type the following command to add the IP address of the StorSimple device to the client’s trusted hosts list:</span></span>
   
     `Set-Item wsman:\localhost\Client\TrustedHosts <device_ip> -Concatenate -Force`
   
     <span data-ttu-id="975be-159">Zastąp <*device_ip*> przy użyciu adresu IP urządzenia; na przykład:</span><span class="sxs-lookup"><span data-stu-id="975be-159">Replace <*device_ip*> with the IP address of your device; for example:</span></span> 
   
     `Set-Item wsman:\localhost\Client\TrustedHosts 10.126.173.90 -Concatenate -Force`
3. <span data-ttu-id="975be-160">Wpisz następujące polecenie, aby zapisać poświadczenia urządzeń w zmiennej:</span><span class="sxs-lookup"><span data-stu-id="975be-160">Type the following command to save the device credentials in a variable:</span></span> 
   
    ```
    $cred = Get-Credential
    ```
    
4. <span data-ttu-id="975be-161">W wyświetlonym oknie dialogowym:</span><span class="sxs-lookup"><span data-stu-id="975be-161">In the dialog box that appears:</span></span>
   
   1. <span data-ttu-id="975be-162">Wpisz nazwę użytkownika w następującym formacie: *device_ip\SSAdmin*.</span><span class="sxs-lookup"><span data-stu-id="975be-162">Type the user name in this format: *device_ip\SSAdmin*.</span></span>
   2. <span data-ttu-id="975be-163">Wpisz hasło administratora urządzenia, która została ustawiona, gdy urządzenie zostało skonfigurowane przy użyciu Kreatora instalacji.</span><span class="sxs-lookup"><span data-stu-id="975be-163">Type the device administrator password that was set when the device was configured with the setup wizard.</span></span> <span data-ttu-id="975be-164">Domyślne hasło jest *Password1*.</span><span class="sxs-lookup"><span data-stu-id="975be-164">The default password is *Password1*.</span></span>
5. <span data-ttu-id="975be-165">Uruchom sesję programu Windows PowerShell na urządzeniu, wpisując polecenie:</span><span class="sxs-lookup"><span data-stu-id="975be-165">Start a Windows PowerShell session on the device by typing this command:</span></span>
   
     `Enter-PSSession -Credential $cred -ConfigurationName SSAdminConsole -ComputerName <device_ip>`
   
   > [!NOTE]
   > <span data-ttu-id="975be-166">Aby utworzyć sesję programu Windows PowerShell do użytku z urządzenia wirtualnego StorSimple, dołącz `–Port` parametru i określ port publiczny, skonfigurowanego w komunikację zdalną dla urządzenia wirtualnego StorSimple.</span><span class="sxs-lookup"><span data-stu-id="975be-166">To create a Windows PowerShell session for use with the StorSimple virtual device, append the `–Port` parameter and specify the public port that you configured in Remoting for StorSimple Virtual Appliance.</span></span>
   
   
<span data-ttu-id="975be-167">W tym momencie powinna mieć aktywnych sesji zdalnej programu Windows PowerShell do urządzenia.</span><span class="sxs-lookup"><span data-stu-id="975be-167">At this point, you should have an active remote Windows PowerShell session to the device.</span></span>
   
![Usługi zdalne środowiska PowerShell przy użyciu protokołu HTTP](./media/storsimple-remote-connect/HCS_PSRemotingUsingHTTP.png)

## <a name="connect-through-https"></a><span data-ttu-id="975be-169">Łączenie się za pośrednictwem protokołu HTTPS</span><span class="sxs-lookup"><span data-stu-id="975be-169">Connect through HTTPS</span></span>

<span data-ttu-id="975be-170">Łączenie z programu Windows PowerShell dla urządzenia StorSimple za pomocą sesji protokołu HTTPS jest najbardziej bezpieczna i zalecana metoda zdalne połączenie z urządzenia Microsoft Azure StorSimple.</span><span class="sxs-lookup"><span data-stu-id="975be-170">Connecting to Windows PowerShell for StorSimple through an HTTPS session is the most secure and recommended method of remotely connecting to your Microsoft Azure StorSimple device.</span></span> <span data-ttu-id="975be-171">Poniższe procedury dotyczą sposobu konfigurowania serial konsoli i komputerów klienckich, aby mogli używać protokołu HTTPS do łączenia z programu Windows PowerShell dla StorSimple.</span><span class="sxs-lookup"><span data-stu-id="975be-171">The following procedures explain how to set up the serial console and client computers so that you can use HTTPS to connect to Windows PowerShell for StorSimple.</span></span>

<span data-ttu-id="975be-172">Aby skonfigurować zdalne zarządzanie, można użyć portalu Azure lub konsoli szeregowej.</span><span class="sxs-lookup"><span data-stu-id="975be-172">You can use either the Azure portal or the serial console to configure remote management.</span></span> <span data-ttu-id="975be-173">Wybierz jedną z następujących procedur:</span><span class="sxs-lookup"><span data-stu-id="975be-173">Select from the following procedures:</span></span>

* [<span data-ttu-id="975be-174">Użyj portalu Azure, aby włączyć zdalne zarządzanie przy użyciu protokołu HTTPS</span><span class="sxs-lookup"><span data-stu-id="975be-174">Use the Azure portal to enable remote management over HTTPS</span></span>](#use-the-azure-classic-portal-to-enable-remote-management-over-https)
* [<span data-ttu-id="975be-175">Użyj konsoli szeregowej, aby włączyć zdalne zarządzanie przy użyciu protokołu HTTPS</span><span class="sxs-lookup"><span data-stu-id="975be-175">Use the serial console to enable remote management over HTTPS</span></span>](#use-the-serial-console-to-enable-remote-management-over-https)

<span data-ttu-id="975be-176">Po włączeniu zdalnego zarządzania umożliwia poniższych procedur Przygotuj hosta do zdalnego zarządzania i nawiąż połączenie z urządzeniem z hosta zdalnego.</span><span class="sxs-lookup"><span data-stu-id="975be-176">After you enable remote management, use the following procedures to prepare the host for a remote management and connect to the device from the remote host.</span></span>

* [<span data-ttu-id="975be-177">Przygotowanie hosta do zarządzania zdalnego</span><span class="sxs-lookup"><span data-stu-id="975be-177">Prepare the host for remote management</span></span>](#prepare-the-host-for-remote-management)
* [<span data-ttu-id="975be-178">Nawiąż połączenie z urządzeniem z hostem zdalnym</span><span class="sxs-lookup"><span data-stu-id="975be-178">Connect to the device from the remote host</span></span>](#connect-to-the-device-from-the-remote-host)

### <a name="use-the-azure-portal-to-enable-remote-management-over-https"></a><span data-ttu-id="975be-179">Użyj portalu Azure, aby włączyć zdalne zarządzanie przy użyciu protokołu HTTPS</span><span class="sxs-lookup"><span data-stu-id="975be-179">Use the Azure portal to enable remote management over HTTPS</span></span>

<span data-ttu-id="975be-180">Wykonaj poniższe kroki w portalu Azure, aby włączyć zdalne zarządzanie przy użyciu protokołu HTTPS.</span><span class="sxs-lookup"><span data-stu-id="975be-180">Perform the following steps in the Azure portal to enable remote management over HTTPS.</span></span>

#### <a name="to-enable-remote-management-over-https-from-the-azure-portal"></a><span data-ttu-id="975be-181">Aby włączyć zdalne zarządzanie przy użyciu protokołu HTTPS z portalu Azure</span><span class="sxs-lookup"><span data-stu-id="975be-181">To enable remote management over HTTPS from the Azure portal</span></span>

1. <span data-ttu-id="975be-182">Przejdź do usługi Menedżer urządzeń StorSimple.</span><span class="sxs-lookup"><span data-stu-id="975be-182">Go to your StorSimple Device Manager service.</span></span> <span data-ttu-id="975be-183">Wybierz **urządzeń** , a następnie wybierz i kliknij przycisk urządzenia, które chcesz skonfigurować do zdalnego zarządzania.</span><span class="sxs-lookup"><span data-stu-id="975be-183">Select **Devices** and then select and click the device you want to configure for remote management.</span></span> <span data-ttu-id="975be-184">Przejdź do **ustawienia urządzenia > zabezpieczeń**.</span><span class="sxs-lookup"><span data-stu-id="975be-184">Go to **Device settings > Security**.</span></span>
2. <span data-ttu-id="975be-185">W **ustawienia zabezpieczeń** bloku, kliknij przycisk **zdalnego zarządzania**.</span><span class="sxs-lookup"><span data-stu-id="975be-185">In the **Security settings** blade, click **Remote Management**.</span></span>
3. <span data-ttu-id="975be-186">Ustaw opcję **Włącz zdalne zarządzanie** na **Tak**.</span><span class="sxs-lookup"><span data-stu-id="975be-186">Set **Enable Remote Management** to **Yes**.</span></span>
4. <span data-ttu-id="975be-187">Można teraz nawiązać połączenia przy użyciu protokołu HTTPS.</span><span class="sxs-lookup"><span data-stu-id="975be-187">You can now choose to connect using HTTPS.</span></span> <span data-ttu-id="975be-188">(Wartość domyślna to łączenie za pośrednictwem protokołu HTTPS). Upewnij się, że wybrany jest protokół HTTPS.</span><span class="sxs-lookup"><span data-stu-id="975be-188">(The default is to connect over HTTPS.) Make sure that HTTPS is selected.</span></span>
5. <span data-ttu-id="975be-189">Kliknij przycisk..., a następnie kliknij przycisk **Pobierz certyfikat zdalnego zarządzania**.</span><span class="sxs-lookup"><span data-stu-id="975be-189">Click ... and then click **Download Remote Management Certificate**.</span></span> <span data-ttu-id="975be-190">Określ lokalizację do zapisania tego pliku.</span><span class="sxs-lookup"><span data-stu-id="975be-190">Specify a location to save this file.</span></span> <span data-ttu-id="975be-191">Należy zainstalować ten certyfikat na komputerze klienta lub hosta używaną do nawiązania połączenia z urządzeniem.</span><span class="sxs-lookup"><span data-stu-id="975be-191">You need to install this certificate on the client or host computer that you will use to connect to the device.</span></span>
6. <span data-ttu-id="975be-192">Kliknij przycisk **zapisać** , a następnie kliknij przycisk **tak** po wyświetleniu monitu o potwierdzenie.</span><span class="sxs-lookup"><span data-stu-id="975be-192">Click **Save** and then click **Yes** when prompted for confirmation.</span></span>

### <a name="use-the-serial-console-to-enable-remote-management-over-https"></a><span data-ttu-id="975be-193">Użyj konsoli szeregowej, aby włączyć zdalne zarządzanie przy użyciu protokołu HTTPS</span><span class="sxs-lookup"><span data-stu-id="975be-193">Use the serial console to enable remote management over HTTPS</span></span>

<span data-ttu-id="975be-194">Wykonaj następujące czynności na konsoli szeregowej urządzenia, aby włączyć zdalne zarządzanie.</span><span class="sxs-lookup"><span data-stu-id="975be-194">Perform the following steps on the device serial console to enable remote management.</span></span>

#### <a name="to-enable-remote-management-through-the-device-serial-console"></a><span data-ttu-id="975be-195">Aby włączyć zdalne zarządzanie za pośrednictwem konsoli szeregowej urządzenia</span><span class="sxs-lookup"><span data-stu-id="975be-195">To enable remote management through the device serial console</span></span>
1. <span data-ttu-id="975be-196">W menu konsoli szeregowej wybierz opcję 1.</span><span class="sxs-lookup"><span data-stu-id="975be-196">On the serial console menu, select option 1.</span></span> <span data-ttu-id="975be-197">Aby uzyskać więcej informacji na temat używania konsoli szeregowej na urządzeniu, przejdź do [Połącz z programu Windows PowerShell dla StorSimple za pośrednictwem konsoli szeregowej urządzenia](storsimple-8000-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="975be-197">For more information about using the serial console on the device, go to [Connect to Windows PowerShell for StorSimple via device serial console](storsimple-8000-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console).</span></span>
2. <span data-ttu-id="975be-198">W wierszu polecenia wpisz:</span><span class="sxs-lookup"><span data-stu-id="975be-198">At the prompt, type:</span></span>
   
     `Enable-HcsRemoteManagement`
   
    <span data-ttu-id="975be-199">To należy włączyć protokół HTTPS na urządzeniu.</span><span class="sxs-lookup"><span data-stu-id="975be-199">This should enable HTTPS on your device.</span></span>
3. <span data-ttu-id="975be-200">Sprawdź, czy został włączony protokół HTTPS, wpisując:</span><span class="sxs-lookup"><span data-stu-id="975be-200">Verify that HTTPS has been enabled by typing:</span></span> 
   
     `Get-HcsSystem`
   
    <span data-ttu-id="975be-201">Upewnij się, że **RemoteManagementMode** pola pokazuje **HttpsEnabled**. Na poniższej ilustracji przedstawiono te ustawienia w PuTTY.</span><span class="sxs-lookup"><span data-stu-id="975be-201">Make sure that the **RemoteManagementMode** field shows **HttpsEnabled**.The following illustration shows these settings in PuTTY.</span></span>
   
     ![Serial obsługujące protokół HTTPS.](./media/storsimple-remote-connect/HCS_SerialHttpsEnabled.png)
4. <span data-ttu-id="975be-203">Z danych wyjściowych `Get-HcsSystem`, skopiuj numer seryjny urządzenia i zapisz go na przyszłość.</span><span class="sxs-lookup"><span data-stu-id="975be-203">From the output of `Get-HcsSystem`, copy the serial number of the device and save it for later use.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="975be-204">Numer seryjny mapuje Nazwa CN certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="975be-204">The serial number maps to the CN name in the certificate.</span></span>
   
5. <span data-ttu-id="975be-205">Uzyskaj certyfikat zdalnego zarządzania, wpisując:</span><span class="sxs-lookup"><span data-stu-id="975be-205">Obtain a remote management certificate by typing:</span></span> 
   
     `Get-HcsRemoteManagementCert`
   
    <span data-ttu-id="975be-206">Zostanie wyświetlony certyfikat podobny do następującego.</span><span class="sxs-lookup"><span data-stu-id="975be-206">A certificate similar to the following will appear.</span></span>
   
    ![Pobierz certyfikat zdalnego zarządzania](./media/storsimple-remote-connect/HCS_GetRemoteManagementCertificate.png)
6. <span data-ttu-id="975be-208">Skopiuj dane w certyfikacie z **---BEGIN CERTIFICATE---** do **---END CERTIFICATE---** do edytora tekstu, takiego jak Notatnik, a następnie zapisz go jako plik cer.</span><span class="sxs-lookup"><span data-stu-id="975be-208">Copy the information in the certificate from **-----BEGIN CERTIFICATE-----** to **-----END CERTIFICATE-----** into a text editor such as Notepad, and save it as a .cer file.</span></span> <span data-ttu-id="975be-209">(Zostanie skopiowany ten plik do zdalnego hosta podczas przygotowywania hosta.)</span><span class="sxs-lookup"><span data-stu-id="975be-209">(You will copy this file to your remote host when you prepare the host.)</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="975be-210">Aby wygenerować nowy certyfikat, użyj `Set-HcsRemoteManagementCert` polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="975be-210">To generate a new certificate, use the `Set-HcsRemoteManagementCert` cmdlet.</span></span>
   
### <a name="prepare-the-host-for-remote-management"></a><span data-ttu-id="975be-211">Przygotowanie hosta do zarządzania zdalnego</span><span class="sxs-lookup"><span data-stu-id="975be-211">Prepare the host for remote management</span></span>

<span data-ttu-id="975be-212">Aby przygotować komputer-host dla połączenia zdalnego, które używa sesję protokołu HTTPS, należy wykonać następujące procedury:</span><span class="sxs-lookup"><span data-stu-id="975be-212">To prepare the host computer for a remote connection that uses an HTTPS session, perform the following procedures:</span></span>

* <span data-ttu-id="975be-213">[Importowanie pliku .cer w magazynie głównym klienta lub hosta zdalnego](#to-import-the-certificate-on-the-remote-host).</span><span class="sxs-lookup"><span data-stu-id="975be-213">[Import the .cer file into the root store of the client or remote host](#to-import-the-certificate-on-the-remote-host).</span></span>
* <span data-ttu-id="975be-214">[Dodaj numery seryjne w pliku hosts na zdalnym hoście](#to-add-device-serial-numbers-to-the-remote-host).</span><span class="sxs-lookup"><span data-stu-id="975be-214">[Add the device serial numbers to the hosts file on your remote host](#to-add-device-serial-numbers-to-the-remote-host).</span></span>

<span data-ttu-id="975be-215">Poniżej opisano każdy z powyższych procedurach.</span><span class="sxs-lookup"><span data-stu-id="975be-215">Each of the preceding procedures, is described below.</span></span>

#### <a name="to-import-the-certificate-on-the-remote-host"></a><span data-ttu-id="975be-216">Aby zaimportować certyfikat na zdalnym hoście</span><span class="sxs-lookup"><span data-stu-id="975be-216">To import the certificate on the remote host</span></span>
1. <span data-ttu-id="975be-217">Kliknij prawym przyciskiem myszy plik cer, a następnie wybierz **instalacji certyfikatu**.</span><span class="sxs-lookup"><span data-stu-id="975be-217">Right-click the .cer file and select **Install certificate**.</span></span> <span data-ttu-id="975be-218">Spowoduje to uruchomienie Kreatora importu certyfikatów.</span><span class="sxs-lookup"><span data-stu-id="975be-218">This starts the Certificate Import Wizard.</span></span>
   
    ![Kreator importu certyfikatów 1](./media/storsimple-remote-connect/HCS_CertificateImportWizard1.png)
2. <span data-ttu-id="975be-220">Dla **lokalizacji magazynu**, wybierz pozycję **komputera lokalnego**, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="975be-220">For **Store location**, select **Local Machine**, and then click **Next**.</span></span>
3. <span data-ttu-id="975be-221">Wybierz **Umieść wszystkie certyfikaty w następującym magazynie**, a następnie kliknij przycisk **Przeglądaj**.</span><span class="sxs-lookup"><span data-stu-id="975be-221">Select **Place all certificates in the following store**, and then click **Browse**.</span></span> <span data-ttu-id="975be-222">Przejdź do zdalnego hosta w magazynie głównym, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="975be-222">Navigate to the root store of your remote host, and then click **Next**.</span></span>
   
    ![Kreator importu certyfikatów 2](./media/storsimple-remote-connect/HCS_CertificateImportWizard2.png)
4. <span data-ttu-id="975be-224">Kliknij przycisk **Zakończ**.</span><span class="sxs-lookup"><span data-stu-id="975be-224">Click **Finish**.</span></span> <span data-ttu-id="975be-225">Zostanie wyświetlony komunikat informujący o tym, że importowanie zakończyło się pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="975be-225">A message that tells you that the import was successful appears.</span></span>
   
    ![Kreator importu certyfikatów 3](./media/storsimple-remote-connect/HCS_CertificateImportWizard3.png)

#### <a name="to-add-device-serial-numbers-to-the-remote-host"></a><span data-ttu-id="975be-227">Aby dodać numerów seryjnych urządzeń z hostem zdalnym</span><span class="sxs-lookup"><span data-stu-id="975be-227">To add device serial numbers to the remote host</span></span>
1. <span data-ttu-id="975be-228">Uruchom program Notatnik jako administrator, a następnie otwórz plik hostów zlokalizowany w \Windows\System32\Drivers\etc.</span><span class="sxs-lookup"><span data-stu-id="975be-228">Start Notepad as an administrator, and then open the hosts file located at \Windows\System32\Drivers\etc.</span></span>
2. <span data-ttu-id="975be-229">Dodaj następujące trzy wpisy do pliku hosts: **adres IP interfejsu dane 0**, **adresu IP stałym kontrolera 0**, i **adres IP stałym kontrolera 1**.</span><span class="sxs-lookup"><span data-stu-id="975be-229">Add the following three entries to your hosts file: **DATA 0 IP address**, **Controller 0 Fixed IP address**, and **Controller 1 Fixed IP address**.</span></span>
3. <span data-ttu-id="975be-230">Wprowadź numer seryjny urządzenia, który został wcześniej zapisany.</span><span class="sxs-lookup"><span data-stu-id="975be-230">Enter the device serial number that you saved earlier.</span></span> <span data-ttu-id="975be-231">Mapowanie to adres IP, jak pokazano na poniższej ilustracji.</span><span class="sxs-lookup"><span data-stu-id="975be-231">Map this to the IP address as shown in the following image.</span></span> <span data-ttu-id="975be-232">Dla kontrolera 0 i kontrolera 1, dołącz **Controller0** i **kontroler1** na końcu numeru seryjnego (nazwa Pospolita).</span><span class="sxs-lookup"><span data-stu-id="975be-232">For Controller 0 and Controller 1, append **Controller0** and **Controller1** at the end of the serial number (CN name).</span></span>
   
    ![Dodawanie pliku hosts nazwa Pospolita](./media/storsimple-remote-connect/HCS_AddingCNNameToHostsFile.png)
4. <span data-ttu-id="975be-234">Zapisz plik hosts.</span><span class="sxs-lookup"><span data-stu-id="975be-234">Save the hosts file.</span></span>

### <a name="connect-to-the-device-from-the-remote-host"></a><span data-ttu-id="975be-235">Nawiąż połączenie z urządzeniem z hostem zdalnym</span><span class="sxs-lookup"><span data-stu-id="975be-235">Connect to the device from the remote host</span></span>

<span data-ttu-id="975be-236">Użyj programu Windows PowerShell i protokołu SSL, aby wprowadzić sesji SSAdmin na urządzeniu z hosta zdalnego lub klienta.</span><span class="sxs-lookup"><span data-stu-id="975be-236">Use Windows PowerShell and SSL to enter an SSAdmin session on your device from a remote host or client.</span></span> <span data-ttu-id="975be-237">Mapuje opcja 1 w sesji SSAdmin [konsoli szeregowej](storsimple-8000-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console) menu urządzenia.</span><span class="sxs-lookup"><span data-stu-id="975be-237">The SSAdmin session maps to option 1 in the [serial console](storsimple-8000-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console) menu of your device.</span></span>

<span data-ttu-id="975be-238">Na komputerze, z którego mają być połączenia zdalnego programu Windows PowerShell, należy wykonać poniższą procedurę.</span><span class="sxs-lookup"><span data-stu-id="975be-238">Perform the following procedure on the computer from which you want to make the remote Windows PowerShell connection.</span></span>

#### <a name="to-enter-an-ssadmin-session-on-the-device-by-using-windows-powershell-and-ssl"></a><span data-ttu-id="975be-239">Aby wprowadzić sesji SSAdmin na urządzeniu za pomocą środowiska Windows PowerShell i SSL</span><span class="sxs-lookup"><span data-stu-id="975be-239">To enter an SSAdmin session on the device by using Windows PowerShell and SSL</span></span>
1. <span data-ttu-id="975be-240">Uruchom sesję programu Windows PowerShell jako administrator.</span><span class="sxs-lookup"><span data-stu-id="975be-240">Start a Windows PowerShell session as an administrator.</span></span>
2. <span data-ttu-id="975be-241">Dodaj adres IP urządzenia do klienta zaufanych hostów, wpisując:</span><span class="sxs-lookup"><span data-stu-id="975be-241">Add the device IP address to the client’s trusted hosts by typing:</span></span>
   
     `Set-Item wsman:\localhost\Client\TrustedHosts <device_ip> -Concatenate -Force`
   
    <span data-ttu-id="975be-242">Gdzie <*device_ip*> to adres IP urządzenia, na przykład:</span><span class="sxs-lookup"><span data-stu-id="975be-242">Where <*device_ip*> is the IP address of your device; for example:</span></span> 
   
     `Set-Item wsman:\localhost\Client\TrustedHosts 10.126.173.90 -Concatenate -Force`
3. <span data-ttu-id="975be-243">Aby utworzyć nowe poświadczenie, wpisz:</span><span class="sxs-lookup"><span data-stu-id="975be-243">To create a new credential, type:</span></span>
   
     `$cred = New-Object pscredential @("<IP of target device>\SSAdmin", (ConvertTo-SecureString -Force -AsPlainText "<Device Administrator Password>"))`
   
    <span data-ttu-id="975be-244">Gdzie <*IP urządzenie docelowe*> jest adresem IP dane 0 dla urządzenia; na przykład **10.126.173.90** opisane w poprzednim obraz w pliku hosts.</span><span class="sxs-lookup"><span data-stu-id="975be-244">Where <*IP of target device*> is the IP address of DATA 0 for your device; for example, **10.126.173.90** as shown in the preceding image of the hosts file.</span></span> <span data-ttu-id="975be-245">Ponadto należy podać hasło administratora urządzenia.</span><span class="sxs-lookup"><span data-stu-id="975be-245">Also, supply the administrator password for your device.</span></span>
4. <span data-ttu-id="975be-246">Utwórz sesję, wpisując:</span><span class="sxs-lookup"><span data-stu-id="975be-246">Create a session by typing:</span></span>
   
     `$session = New-PSSession -UseSSL -ComputerName <Serial number of target device> -Credential $cred -ConfigurationName "SSAdminConsole"`
   
    <span data-ttu-id="975be-247">Parametru - ComputerName w polecenia cmdlet, podaj <*numer seryjny urządzenia docelowego*>.</span><span class="sxs-lookup"><span data-stu-id="975be-247">For the -ComputerName parameter in the cmdlet, provide the <*serial number of target device*>.</span></span> <span data-ttu-id="975be-248">Ten numer seryjny został zamapowany na adres IP interfejsu dane 0 w pliku hosts na zdalnym hoście; na przykład **SHX0991003G44MT** jak pokazano na poniższej ilustracji.</span><span class="sxs-lookup"><span data-stu-id="975be-248">This serial number was mapped to the IP address of DATA 0 in the hosts file on your remote host; for example, **SHX0991003G44MT** as shown in the following image.</span></span>
5. <span data-ttu-id="975be-249">Wpisz:</span><span class="sxs-lookup"><span data-stu-id="975be-249">Type:</span></span>
   
     `Enter-PSSession $session`
6. <span data-ttu-id="975be-250">Należy odczekać kilka minut, a następnie nastąpi połączenie do urządzenia za pośrednictwem protokołu HTTPS przy użyciu protokołu SSL.</span><span class="sxs-lookup"><span data-stu-id="975be-250">You will need to wait a few minutes, and then you will be connected to your device via HTTPS over SSL.</span></span> <span data-ttu-id="975be-251">Zostanie wyświetlony komunikat, który wskazuje, że nawiązano połączenie z urządzeniem.</span><span class="sxs-lookup"><span data-stu-id="975be-251">You see a message that indicates you are connected to your device.</span></span>
   
    ![Usługi zdalne środowiska PowerShell przy użyciu protokołu HTTPS i SSL](./media/storsimple-remote-connect/HCS_PSRemotingUsingHTTPSAndSSL.png)

## <a name="next-steps"></a><span data-ttu-id="975be-253">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="975be-253">Next steps</span></span>

* <span data-ttu-id="975be-254">Dowiedz się więcej o [przy użyciu programu Windows PowerShell do administrowania urządzeniem StorSimple](storsimple-8000-windows-powershell-administration.md).</span><span class="sxs-lookup"><span data-stu-id="975be-254">Learn more about [using Windows PowerShell to administer your StorSimple device](storsimple-8000-windows-powershell-administration.md).</span></span>
* <span data-ttu-id="975be-255">Dowiedz się więcej o [przy użyciu usługi Menedżer StorSimple urządzenia do administrowania urządzeniem StorSimple](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="975be-255">Learn more about [using the StorSimple Device Manager service to administer your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

