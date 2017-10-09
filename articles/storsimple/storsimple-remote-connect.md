---
title: "aaaConnect zdalnie tooyour urządzenia StorSimple | Dokumentacja firmy Microsoft"
description: "Wyjaśniono, jak tooconfigure Twojego urządzenia pod kątem zarządzania zdalnego i w jaki sposób tooWindows tooconnect programu PowerShell dla StorSimple za pośrednictwem protokołu HTTP lub HTTPS."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 923377aa-f451-4656-87de-5e95a34a6a2a
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 55ed8fcdd997901301e0adc164a302216cde0332
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-remotely-tooyour-storsimple-8000-series-device"></a><span data-ttu-id="ac611-103">Zdalne połączenia urządzenia z serii StorSimple 8000 tooyour</span><span class="sxs-lookup"><span data-stu-id="ac611-103">Connect remotely tooyour StorSimple 8000 series device</span></span>

## <a name="overview"></a><span data-ttu-id="ac611-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="ac611-104">Overview</span></span>
<span data-ttu-id="ac611-105">Można użyć urządzenia StorSimple tooyour tooconnect komunikacji zdalnej programu Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ac611-105">You can use Windows PowerShell remoting tooconnect tooyour StorSimple device.</span></span> <span data-ttu-id="ac611-106">Po podłączeniu w ten sposób, nie będą widzieć menu.</span><span class="sxs-lookup"><span data-stu-id="ac611-106">When you connect this way, you will not see a menu.</span></span> <span data-ttu-id="ac611-107">(Możesz zobaczyć menu tylko wtedy, gdy używasz konsoli szeregowej hello na powitania tooconnect urządzenia). Za pomocą komunikacji zdalnej programu Windows PowerShell należy połączyć tooa określonego obszaru działania.</span><span class="sxs-lookup"><span data-stu-id="ac611-107">(You see a menu only if you use hello serial console on hello device tooconnect.) With Windows PowerShell remoting, you connect tooa specific runspace.</span></span> <span data-ttu-id="ac611-108">Można również określić język wyświetlania hello.</span><span class="sxs-lookup"><span data-stu-id="ac611-108">You can also specify hello display language.</span></span> 

<span data-ttu-id="ac611-109">Aby uzyskać więcej informacji o używaniu toomanage komunikacji zdalnej programu Windows PowerShell urządzeniu Przejdź zbyt[Użyj środowiska Windows PowerShell dla StorSimple tooadminister urządzenia StorSimple](storsimple-windows-powershell-administration.md).</span><span class="sxs-lookup"><span data-stu-id="ac611-109">For more information about using Windows PowerShell remoting toomanage your device, go too[Use Windows PowerShell for StorSimple tooadminister your StorSimple device](storsimple-windows-powershell-administration.md).</span></span>

<span data-ttu-id="ac611-110">Ten samouczek wyjaśnia sposób tooconfigure Twojego urządzenia pod kątem zarządzania zdalnego, a następnie jak tooWindows tooconnect programu PowerShell dla StorSimple.</span><span class="sxs-lookup"><span data-stu-id="ac611-110">This tutorial explains how tooconfigure your device for remote management and then how tooconnect tooWindows PowerShell for StorSimple.</span></span> <span data-ttu-id="ac611-111">Można użyć protokołu HTTP lub HTTPS tooconnect za pośrednictwem komunikacji zdalnej programu Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ac611-111">You can use HTTP or HTTPS tooconnect via Windows PowerShell remoting.</span></span> <span data-ttu-id="ac611-112">Jednak podczas decydowania jak tooWindows tooconnect programu PowerShell dla StorSimple, należy wziąć pod uwagę następujące hello:</span><span class="sxs-lookup"><span data-stu-id="ac611-112">However, when you are deciding how tooconnect tooWindows PowerShell for StorSimple, consider hello following:</span></span> 

* <span data-ttu-id="ac611-113">Łączenie bezpośrednio toohello konsoli szeregowej urządzenia jest bezpieczne, ale nie jest łączącego konsoli szeregowej toohello za pośrednictwem przełączników sieciowych.</span><span class="sxs-lookup"><span data-stu-id="ac611-113">Connecting directly toohello device serial console is secure, but connecting toohello serial console over network switches is not.</span></span> <span data-ttu-id="ac611-114">Należy uważać na powitania ryzyko związane z zabezpieczeniami podczas łączenia z konsolą szeregową urządzenia toohello za pośrednictwem przełączników sieciowych.</span><span class="sxs-lookup"><span data-stu-id="ac611-114">Be cautious of hello security risk when connecting toohello device serial console over network switches.</span></span> 
* <span data-ttu-id="ac611-115">Łączących się za pośrednictwem sesji HTTP może oferować lepsze bezpieczeństwo niż łączących się za pośrednictwem konsoli szeregowej hello hello sieci.</span><span class="sxs-lookup"><span data-stu-id="ac611-115">Connecting through an HTTP session might offer more security than connecting through hello serial console over hello network.</span></span> <span data-ttu-id="ac611-116">Chociaż nie jest to najbezpieczniejsza metoda hello, jest dopuszczalne w zaufanych sieciach.</span><span class="sxs-lookup"><span data-stu-id="ac611-116">Although this is not hello most secure method, it is acceptable on trusted networks.</span></span> 
* <span data-ttu-id="ac611-117">Łączących się za pośrednictwem sesji protokołu HTTPS z certyfikatu z podpisem własnym jest hello najbardziej bezpieczne i hello zalecana opcja.</span><span class="sxs-lookup"><span data-stu-id="ac611-117">Connecting through an HTTPS session with a self-signed certificate is hello most secure and hello recommended option.</span></span>

<span data-ttu-id="ac611-118">Możesz połączyć zdalnie toohello interfejsu programu Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ac611-118">You can connect remotely toohello Windows PowerShell interface.</span></span> <span data-ttu-id="ac611-119">Jednak urządzenia StorSimple tooyour dostępu zdalnego za pośrednictwem interfejsu programu Windows PowerShell hello nie jest włączona domyślnie.</span><span class="sxs-lookup"><span data-stu-id="ac611-119">However, remote access tooyour StorSimple device via hello Windows PowerShell interface is not enabled by default.</span></span> <span data-ttu-id="ac611-120">Najpierw należy tooenable zdalne zarządzanie na urządzeniu hello, a następnie na hello klienta, który jest używany tooaccess urządzenia.</span><span class="sxs-lookup"><span data-stu-id="ac611-120">You need tooenable remote management on hello device first, and then on hello client that is used tooaccess your device.</span></span>

<span data-ttu-id="ac611-121">Witaj opisane w tym artykule wykonano na komputerze hosta z systemem Windows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="ac611-121">hello steps described in this article were performed on a host system running Windows Server 2012 R2.</span></span>

## <a name="connect-through-http"></a><span data-ttu-id="ac611-122">Łączenie się za pośrednictwem protokołu HTTP</span><span class="sxs-lookup"><span data-stu-id="ac611-122">Connect through HTTP</span></span>
<span data-ttu-id="ac611-123">Łączenie tooWindows środowiska PowerShell dla urządzenia StorSimple za pośrednictwem sesji HTTP oferuje lepsze zabezpieczenia niż łączących się za pośrednictwem konsoli szeregowej hello urządzenia StorSimple.</span><span class="sxs-lookup"><span data-stu-id="ac611-123">Connecting tooWindows PowerShell for StorSimple through an HTTP session offers more security than connecting through hello serial console of your StorSimple device.</span></span> <span data-ttu-id="ac611-124">Chociaż nie jest to najbezpieczniejsza metoda hello, jest dopuszczalne w zaufanych sieciach.</span><span class="sxs-lookup"><span data-stu-id="ac611-124">Although this is not hello most secure method, it is acceptable on trusted networks.</span></span>

<span data-ttu-id="ac611-125">Można użyć hello klasycznego portalu Azure lub hello konsoli szeregowej tooconfigure zdalnego zarządzania.</span><span class="sxs-lookup"><span data-stu-id="ac611-125">You can use either hello Azure classic portal or hello serial console tooconfigure remote management.</span></span> <span data-ttu-id="ac611-126">Wybierz jedną z procedur przedstawionych hello:</span><span class="sxs-lookup"><span data-stu-id="ac611-126">Select from hello following procedures:</span></span>

* [<span data-ttu-id="ac611-127">Użyj hello Azure classic portal tooenable zdalnego zarządzania za pośrednictwem protokołu HTTP</span><span class="sxs-lookup"><span data-stu-id="ac611-127">Use hello Azure classic portal tooenable remote management over HTTP</span></span>](#use-the-azure-classic-portal-to-enable-remote-management-over-http)
* [<span data-ttu-id="ac611-128">Użyj konsoli szeregowej hello tooenable zdalnego zarządzania za pośrednictwem protokołu HTTP</span><span class="sxs-lookup"><span data-stu-id="ac611-128">Use hello serial console tooenable remote management over HTTP</span></span>](#use-the-serial-console-to-enable-remote-management-over-http)

<span data-ttu-id="ac611-129">Po włączeniu zdalnego zarządzania za pomocą hello następujące procedury tooprepare powitania klienta dla połączenia zdalnego.</span><span class="sxs-lookup"><span data-stu-id="ac611-129">After you enable remote management, use hello following procedure tooprepare hello client for a remote connection.</span></span>

* [<span data-ttu-id="ac611-130">Przygotuj powitania klienta dla połączenia zdalnego</span><span class="sxs-lookup"><span data-stu-id="ac611-130">Prepare hello client for remote connection</span></span>](#prepare-the-client-for-remote-connection)

### <a name="use-hello-azure-classic-portal-tooenable-remote-management-over-http"></a><span data-ttu-id="ac611-131">Użyj hello Azure classic portal tooenable zdalnego zarządzania za pośrednictwem protokołu HTTP</span><span class="sxs-lookup"><span data-stu-id="ac611-131">Use hello Azure classic portal tooenable remote management over HTTP</span></span>
<span data-ttu-id="ac611-132">Wykonaj hello, wykonaj następujące kroki w hello Azure classic portal tooenable zdalnego zarządzania za pośrednictwem protokołu HTTP.</span><span class="sxs-lookup"><span data-stu-id="ac611-132">Perform hello following steps in hello Azure classic portal tooenable remote management over HTTP.</span></span>

#### <a name="tooenable-remote-management-through-hello-azure-classic-portal"></a><span data-ttu-id="ac611-133">tooenable zarządzanie zdalne za pomocą hello klasycznego portalu Azure</span><span class="sxs-lookup"><span data-stu-id="ac611-133">tooenable remote management through hello Azure classic portal</span></span>
1. <span data-ttu-id="ac611-134">Dostęp **urządzeń** > **Konfiguruj** dla danego urządzenia.</span><span class="sxs-lookup"><span data-stu-id="ac611-134">Access **Devices** > **Configure** for your device.</span></span>
2. <span data-ttu-id="ac611-135">Przewiń w dół toohello **zdalnego zarządzania** sekcji.</span><span class="sxs-lookup"><span data-stu-id="ac611-135">Scroll down toohello **Remote Management** section.</span></span>
3. <span data-ttu-id="ac611-136">Ustaw **włączyć zdalne zarządzanie** za**tak**.</span><span class="sxs-lookup"><span data-stu-id="ac611-136">Set **Enable Remote Management** too**Yes**.</span></span>
4. <span data-ttu-id="ac611-137">Teraz możesz tooconnect przy użyciu protokołu HTTP.</span><span class="sxs-lookup"><span data-stu-id="ac611-137">You can now choose tooconnect using HTTP.</span></span> <span data-ttu-id="ac611-138">(domyślnie hello jest tooconnect za pośrednictwem protokołu HTTPS). Upewnij się, że wybrano HTTP.</span><span class="sxs-lookup"><span data-stu-id="ac611-138">(hello default is tooconnect over HTTPS.) Make sure that HTTP is selected.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="ac611-139">Łączenie za pośrednictwem protokołu HTTP jest dopuszczalne tylko w sieciach zaufanych.</span><span class="sxs-lookup"><span data-stu-id="ac611-139">Connecting over HTTP is acceptable only on trusted networks.</span></span>
   > 
   > 
5. <span data-ttu-id="ac611-140">Kliknij przycisk **zapisać** u dołu hello hello strony.</span><span class="sxs-lookup"><span data-stu-id="ac611-140">Click **Save** at hello bottom of hello page.</span></span>

### <a name="use-hello-serial-console-tooenable-remote-management-over-http"></a><span data-ttu-id="ac611-141">Użyj konsoli szeregowej hello tooenable zdalnego zarządzania za pośrednictwem protokołu HTTP</span><span class="sxs-lookup"><span data-stu-id="ac611-141">Use hello serial console tooenable remote management over HTTP</span></span>
<span data-ttu-id="ac611-142">Wykonaj następujące kroki na powitania urządzenia konsoli szeregowej tooenable zdalne zarządzanie hello.</span><span class="sxs-lookup"><span data-stu-id="ac611-142">Perform hello following steps on hello device serial console tooenable remote management.</span></span>

#### <a name="tooenable-remote-management-through-hello-device-serial-console"></a><span data-ttu-id="ac611-143">tooenable zdalnego zarządzania za pośrednictwem konsoli szeregowej urządzenia hello</span><span class="sxs-lookup"><span data-stu-id="ac611-143">tooenable remote management through hello device serial console</span></span>
1. <span data-ttu-id="ac611-144">Menu konsoli szeregowej hello wybierz opcję 1.</span><span class="sxs-lookup"><span data-stu-id="ac611-144">On hello serial console menu, select option 1.</span></span> <span data-ttu-id="ac611-145">Aby uzyskać więcej informacji o używaniu konsoli szeregowej hello na urządzeniu hello Przejdź zbyt[łączenie tooWindows środowiska PowerShell dla urządzenia StorSimple za pośrednictwem konsoli szeregowej urządzenia](storsimple-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="ac611-145">For more information about using hello serial console on hello device, go too[Connect tooWindows PowerShell for StorSimple via device serial console](storsimple-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console).</span></span>
2. <span data-ttu-id="ac611-146">Witaj, wpisz w wierszu:`Enable-HcsRemoteManagement –AllowHttp`</span><span class="sxs-lookup"><span data-stu-id="ac611-146">At hello prompt, type: `Enable-HcsRemoteManagement –AllowHttp`</span></span>
3. <span data-ttu-id="ac611-147">Użytkownik zostanie poinformowany o hello luk w zabezpieczeniach systemu przy użyciu protokołu HTTP tooconnect toohello urządzenia.</span><span class="sxs-lookup"><span data-stu-id="ac611-147">You will be notified about hello security vulnerabilities of using HTTP tooconnect toohello device.</span></span> <span data-ttu-id="ac611-148">Po wyświetleniu monitu Potwierdź, wpisując **Y**.</span><span class="sxs-lookup"><span data-stu-id="ac611-148">When prompted, confirm by typing **Y**.</span></span>
4. <span data-ttu-id="ac611-149">Sprawdź, czy HTTP jest włączona, wpisując:`Get-HcsSystem`</span><span class="sxs-lookup"><span data-stu-id="ac611-149">Verify that HTTP is enabled by typing: `Get-HcsSystem`</span></span>
5. <span data-ttu-id="ac611-150">Sprawdź, że hello **RemoteManagementMode** pola pokazuje **HttpsAndHttpEnabled**.hello następującej ilustracji przedstawiono te ustawienia programu PuTTY.</span><span class="sxs-lookup"><span data-stu-id="ac611-150">Verify that hello **RemoteManagementMode** field shows **HttpsAndHttpEnabled**.hello following illustration shows these settings in PuTTY.</span></span>
   
     ![Serial HTTPS i HTTP włączone](./media/storsimple-remote-connect/HCS_SerialHttpsAndHttpEnabled.png)

### <a name="prepare-hello-client-for-remote-connection"></a><span data-ttu-id="ac611-152">Przygotuj powitania klienta dla połączenia zdalnego</span><span class="sxs-lookup"><span data-stu-id="ac611-152">Prepare hello client for remote connection</span></span>
<span data-ttu-id="ac611-153">Wykonaj następujące kroki na powitania klienta tooenable zdalne zarządzanie hello.</span><span class="sxs-lookup"><span data-stu-id="ac611-153">Perform hello following steps on hello client tooenable remote management.</span></span>

#### <a name="tooprepare-hello-client-for-remote-connection"></a><span data-ttu-id="ac611-154">tooprepare powitania klienta dla połączenia zdalnego</span><span class="sxs-lookup"><span data-stu-id="ac611-154">tooprepare hello client for remote connection</span></span>
1. <span data-ttu-id="ac611-155">Uruchom sesję programu Windows PowerShell jako administrator.</span><span class="sxs-lookup"><span data-stu-id="ac611-155">Start a Windows PowerShell session as an administrator.</span></span>
2. <span data-ttu-id="ac611-156">Wpisz hello następującego adresu IP hello tooadd polecenia listy zaufanych hostów hello StorSimple urządzenia toohello klienta:</span><span class="sxs-lookup"><span data-stu-id="ac611-156">Type hello following command tooadd hello IP address of hello StorSimple device toohello client’s trusted hosts list:</span></span> 
   
     `Set-Item wsman:\localhost\Client\TrustedHosts <device_ip> -Concatenate -Force`
   
     <span data-ttu-id="ac611-157">Zastąp <*device_ip*> o adresie IP hello urządzenia; na przykład:</span><span class="sxs-lookup"><span data-stu-id="ac611-157">Replace <*device_ip*> with hello IP address of your device; for example:</span></span> 
   
     `Set-Item wsman:\localhost\Client\TrustedHosts 10.126.173.90 -Concatenate -Force`
3. <span data-ttu-id="ac611-158">Następujące polecenie toosave hello urządzenia poświadczeń w zmiennej hello typu:</span><span class="sxs-lookup"><span data-stu-id="ac611-158">Type hello following command toosave hello device credentials in a variable:</span></span> 
   
    ```
    $cred = Get-Credential
    ```
    
4. <span data-ttu-id="ac611-159">W hello pojawi się okno dialogowe:</span><span class="sxs-lookup"><span data-stu-id="ac611-159">In hello dialog box that appears:</span></span>
   
   1. <span data-ttu-id="ac611-160">Wpisz nazwę użytkownika hello w następującym formacie: *device_ip\SSAdmin*.</span><span class="sxs-lookup"><span data-stu-id="ac611-160">Type hello user name in this format: *device_ip\SSAdmin*.</span></span>
   2. <span data-ttu-id="ac611-161">Wpisz hasło administratora urządzenia hello, która została ustawiona, gdy urządzenie hello został skonfigurowany z kreatorem hello.</span><span class="sxs-lookup"><span data-stu-id="ac611-161">Type hello device administrator password that was set when hello device was configured with hello setup wizard.</span></span> <span data-ttu-id="ac611-162">Witaj domyślne hasło jest *Password1*.</span><span class="sxs-lookup"><span data-stu-id="ac611-162">hello default password is *Password1*.</span></span>
5. <span data-ttu-id="ac611-163">Uruchom sesję programu Windows PowerShell na urządzeniu hello, wpisując polecenie:</span><span class="sxs-lookup"><span data-stu-id="ac611-163">Start a Windows PowerShell session on hello device by typing this command:</span></span>
   
     `Enter-PSSession -Credential $cred -ConfigurationName SSAdminConsole -ComputerName <device_ip>`
   
   > [!NOTE]
   > <span data-ttu-id="ac611-164">toocreate sesję programu Windows PowerShell do użytku z urządzenia wirtualnego StorSimple hello, Dołącz hello `–Port` parametru i określ port publiczny hello skonfigurowanego w komunikację zdalną dla urządzenia wirtualnego StorSimple.</span><span class="sxs-lookup"><span data-stu-id="ac611-164">toocreate a Windows PowerShell session for use with hello StorSimple virtual device, append hello `–Port` parameter and specify hello public port that you configured in Remoting for StorSimple Virtual Appliance.</span></span>
   > 
   > 
   
     <span data-ttu-id="ac611-165">W tym momencie powinien mieć active środowiska Windows PowerShell sesji toohello urządzeniu zdalnym.</span><span class="sxs-lookup"><span data-stu-id="ac611-165">At this point, you should have an active remote Windows PowerShell session toohello device.</span></span>
   
    ![Usługi zdalne środowiska PowerShell przy użyciu protokołu HTTP](./media/storsimple-remote-connect/HCS_PSRemotingUsingHTTP.png)

## <a name="connect-through-https"></a><span data-ttu-id="ac611-167">Łączenie się za pośrednictwem protokołu HTTPS</span><span class="sxs-lookup"><span data-stu-id="ac611-167">Connect through HTTPS</span></span>
<span data-ttu-id="ac611-168">Łączenie tooWindows środowiska PowerShell dla urządzenia StorSimple za pomocą sesji protokołu HTTPS jest hello najbardziej bezpieczne i zalecana metoda tooyour zdalnie łączącego się urządzenia Microsoft Azure StorSimple.</span><span class="sxs-lookup"><span data-stu-id="ac611-168">Connecting tooWindows PowerShell for StorSimple through an HTTPS session is hello most secure and recommended method of remotely connecting tooyour Microsoft Azure StorSimple device.</span></span> <span data-ttu-id="ac611-169">Hello następujące procedury wyjaśniają, jak tooset się hello serial konsoli i komputerów klienckich, dzięki czemu może używać protokołu HTTPS tooconnect tooWindows programu PowerShell dla urządzenia StorSimple.</span><span class="sxs-lookup"><span data-stu-id="ac611-169">hello following procedures explain how tooset up hello serial console and client computers so that you can use HTTPS tooconnect tooWindows PowerShell for StorSimple.</span></span>

<span data-ttu-id="ac611-170">Można użyć hello klasycznego portalu Azure lub hello konsoli szeregowej tooconfigure zdalnego zarządzania.</span><span class="sxs-lookup"><span data-stu-id="ac611-170">You can use either hello Azure classic portal or hello serial console tooconfigure remote management.</span></span> <span data-ttu-id="ac611-171">Wybierz jedną z procedur przedstawionych hello:</span><span class="sxs-lookup"><span data-stu-id="ac611-171">Select from hello following procedures:</span></span>

* [<span data-ttu-id="ac611-172">Użyj hello Azure classic portal tooenable zdalnego zarządzania za pośrednictwem protokołu HTTPS</span><span class="sxs-lookup"><span data-stu-id="ac611-172">Use hello Azure classic portal tooenable remote management over HTTPS</span></span>](#use-the-azure-classic-portal-to-enable-remote-management-over-https)
* [<span data-ttu-id="ac611-173">Użyj konsoli szeregowej hello tooenable zdalnego zarządzania za pośrednictwem protokołu HTTPS</span><span class="sxs-lookup"><span data-stu-id="ac611-173">Use hello serial console tooenable remote management over HTTPS</span></span>](#use-the-serial-console-to-enable-remote-management-over-https)

<span data-ttu-id="ac611-174">Po włączeniu zdalnego zarządzania przy użyciu hello następujące procedury tooprepare hello hosta do zdalnego zarządzania, a następnie podłącz urządzenie toohello z hostem zdalnym hello.</span><span class="sxs-lookup"><span data-stu-id="ac611-174">After you enable remote management, use hello following procedures tooprepare hello host for a remote management and connect toohello device from hello remote host.</span></span>

* [<span data-ttu-id="ac611-175">Przygotowanie hello hosta do zarządzania zdalnego</span><span class="sxs-lookup"><span data-stu-id="ac611-175">Prepare hello host for remote management</span></span>](#prepare-the-host-for-remote-management)
* [<span data-ttu-id="ac611-176">Podłącz urządzenie toohello z hostem zdalnym hello</span><span class="sxs-lookup"><span data-stu-id="ac611-176">Connect toohello device from hello remote host</span></span>](#connect-to-the-device-from-the-remote-host)

### <a name="use-hello-azure-classic-portal-tooenable-remote-management-over-https"></a><span data-ttu-id="ac611-177">Użyj hello Azure classic portal tooenable zdalnego zarządzania za pośrednictwem protokołu HTTPS</span><span class="sxs-lookup"><span data-stu-id="ac611-177">Use hello Azure classic portal tooenable remote management over HTTPS</span></span>
<span data-ttu-id="ac611-178">Wykonaj hello, wykonaj następujące kroki w hello Azure classic portal tooenable zdalnego zarządzania za pośrednictwem protokołu HTTPS.</span><span class="sxs-lookup"><span data-stu-id="ac611-178">Perform hello following steps in hello Azure classic portal tooenable remote management over HTTPS.</span></span>

#### <a name="tooenable-remote-management-over-https-from-hello-azure-classic-portal"></a><span data-ttu-id="ac611-179">tooenable zdalne zarządzanie przy użyciu protokołu HTTPS z hello klasycznego portalu Azure</span><span class="sxs-lookup"><span data-stu-id="ac611-179">tooenable remote management over HTTPS from hello Azure classic portal</span></span>
1. <span data-ttu-id="ac611-180">Dostęp **urządzeń** > **Konfiguruj** dla danego urządzenia.</span><span class="sxs-lookup"><span data-stu-id="ac611-180">Access **Devices** > **Configure** for your device.</span></span>
2. <span data-ttu-id="ac611-181">Przewiń w dół toohello **zdalnego zarządzania** sekcji.</span><span class="sxs-lookup"><span data-stu-id="ac611-181">Scroll down toohello **Remote Management** section.</span></span>
3. <span data-ttu-id="ac611-182">Ustaw **włączyć zdalne zarządzanie** za**tak**.</span><span class="sxs-lookup"><span data-stu-id="ac611-182">Set **Enable Remote Management** too**Yes**.</span></span>
4. <span data-ttu-id="ac611-183">Teraz możesz tooconnect przy użyciu protokołu HTTPS.</span><span class="sxs-lookup"><span data-stu-id="ac611-183">You can now choose tooconnect using HTTPS.</span></span> <span data-ttu-id="ac611-184">(domyślnie hello jest tooconnect za pośrednictwem protokołu HTTPS). Upewnij się, że wybrany jest protokół HTTPS.</span><span class="sxs-lookup"><span data-stu-id="ac611-184">(hello default is tooconnect over HTTPS.) Make sure that HTTPS is selected.</span></span> 
5. <span data-ttu-id="ac611-185">Kliknij przycisk **Pobierz certyfikat zdalnego zarządzania**.</span><span class="sxs-lookup"><span data-stu-id="ac611-185">Click **Download Remote Management Certificate**.</span></span> <span data-ttu-id="ac611-186">Określ toosave lokalizację tego pliku.</span><span class="sxs-lookup"><span data-stu-id="ac611-186">Specify a location toosave this file.</span></span> <span data-ttu-id="ac611-187">Konieczne będzie tooinstall ten certyfikat na komputerze klienta lub hosta hello użyje tooconnect toohello urządzenia.</span><span class="sxs-lookup"><span data-stu-id="ac611-187">You will need tooinstall this certificate on hello client or host computer that you will use tooconnect toohello device.</span></span>
6. <span data-ttu-id="ac611-188">Kliknij przycisk **zapisać** u dołu hello hello strony.</span><span class="sxs-lookup"><span data-stu-id="ac611-188">Click **Save** at hello bottom of hello page.</span></span>

### <a name="use-hello-serial-console-tooenable-remote-management-over-https"></a><span data-ttu-id="ac611-189">Użyj konsoli szeregowej hello tooenable zdalnego zarządzania za pośrednictwem protokołu HTTPS</span><span class="sxs-lookup"><span data-stu-id="ac611-189">Use hello serial console tooenable remote management over HTTPS</span></span>
<span data-ttu-id="ac611-190">Wykonaj następujące kroki na powitania urządzenia konsoli szeregowej tooenable zdalne zarządzanie hello.</span><span class="sxs-lookup"><span data-stu-id="ac611-190">Perform hello following steps on hello device serial console tooenable remote management.</span></span>

#### <a name="tooenable-remote-management-through-hello-device-serial-console"></a><span data-ttu-id="ac611-191">tooenable zdalnego zarządzania za pośrednictwem konsoli szeregowej urządzenia hello</span><span class="sxs-lookup"><span data-stu-id="ac611-191">tooenable remote management through hello device serial console</span></span>
1. <span data-ttu-id="ac611-192">Menu konsoli szeregowej hello wybierz opcję 1.</span><span class="sxs-lookup"><span data-stu-id="ac611-192">On hello serial console menu, select option 1.</span></span> <span data-ttu-id="ac611-193">Aby uzyskać więcej informacji o używaniu konsoli szeregowej hello na urządzeniu hello Przejdź zbyt[łączenie tooWindows środowiska PowerShell dla urządzenia StorSimple za pośrednictwem konsoli szeregowej urządzenia](storsimple-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="ac611-193">For more information about using hello serial console on hello device, go too[Connect tooWindows PowerShell for StorSimple via device serial console](storsimple-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console).</span></span>
2. <span data-ttu-id="ac611-194">Witaj, wpisz w wierszu:</span><span class="sxs-lookup"><span data-stu-id="ac611-194">At hello prompt, type:</span></span> 
   
     `Enable-HcsRemoteManagement`
   
    <span data-ttu-id="ac611-195">To należy włączyć protokół HTTPS na urządzeniu.</span><span class="sxs-lookup"><span data-stu-id="ac611-195">This should enable HTTPS on your device.</span></span>
3. <span data-ttu-id="ac611-196">Sprawdź, czy został włączony protokół HTTPS, wpisując:</span><span class="sxs-lookup"><span data-stu-id="ac611-196">Verify that HTTPS has been enabled by typing:</span></span> 
   
     `Get-HcsSystem`
   
    <span data-ttu-id="ac611-197">Upewnij się, że hello **RemoteManagementMode** pola pokazuje **HttpsEnabled**.hello następującej ilustracji przedstawiono te ustawienia programu PuTTY.</span><span class="sxs-lookup"><span data-stu-id="ac611-197">Make sure that hello **RemoteManagementMode** field shows **HttpsEnabled**.hello following illustration shows these settings in PuTTY.</span></span>
   
     ![Serial obsługujące protokół HTTPS.](./media/storsimple-remote-connect/HCS_SerialHttpsEnabled.png)
4. <span data-ttu-id="ac611-199">Z danych wyjściowych hello `Get-HcsSystem`, skopiuj numer seryjny hello hello urządzenia i zapisz go do późniejszego użycia.</span><span class="sxs-lookup"><span data-stu-id="ac611-199">From hello output of `Get-HcsSystem`, copy hello serial number of hello device and save it for later use.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="ac611-200">numer seryjny Hello mapuje toohello Nazwa CN certyfikatu hello.</span><span class="sxs-lookup"><span data-stu-id="ac611-200">hello serial number maps toohello CN name in hello certificate.</span></span>
   > 
   > 
5. <span data-ttu-id="ac611-201">Uzyskaj certyfikat zdalnego zarządzania, wpisując:</span><span class="sxs-lookup"><span data-stu-id="ac611-201">Obtain a remote management certificate by typing:</span></span> 
   
     `Get-HcsRemoteManagementCert`
   
    <span data-ttu-id="ac611-202">Pojawi się następujący certyfikat z podobnych toohello.</span><span class="sxs-lookup"><span data-stu-id="ac611-202">A certificate similar toohello following will appear.</span></span>
   
    ![Pobierz certyfikat zdalnego zarządzania](./media/storsimple-remote-connect/HCS_GetRemoteManagementCertificate.png)
6. <span data-ttu-id="ac611-204">Kopiowanie informacji hello w certyfikacie hello z **---BEGIN CERTIFICATE---** za**---END CERTIFICATE---** do edytora tekstu, takiego jak Notatnik, a następnie zapisz go jako plik cer.</span><span class="sxs-lookup"><span data-stu-id="ac611-204">Copy hello information in hello certificate from **-----BEGIN CERTIFICATE-----** too**-----END CERTIFICATE-----** into a text editor such as Notepad, and save it as a .cer file.</span></span> <span data-ttu-id="ac611-205">(Zostanie skopiowany hosta zdalnego tooyour plików, podczas przygotowywania hosta hello.)</span><span class="sxs-lookup"><span data-stu-id="ac611-205">(You will copy this file tooyour remote host when you prepare hello host.)</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="ac611-206">toogenerate nowego świadectwa, użyj hello `Set-HcsRemoteManagementCert` polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="ac611-206">toogenerate a new certificate, use hello `Set-HcsRemoteManagementCert` cmdlet.</span></span>
   > 
   > 

### <a name="prepare-hello-host-for-remote-management"></a><span data-ttu-id="ac611-207">Przygotowanie hello hosta do zarządzania zdalnego</span><span class="sxs-lookup"><span data-stu-id="ac611-207">Prepare hello host for remote management</span></span>
<span data-ttu-id="ac611-208">komputer hosta hello tooprepare połączenie zdalnego za pomocą sesji protokołu HTTPS, należy wykonać hello zgodnie z procedurami:</span><span class="sxs-lookup"><span data-stu-id="ac611-208">tooprepare hello host computer for a remote connection that uses an HTTPS session, perform hello following procedures:</span></span>

* <span data-ttu-id="ac611-209">[Importowanie pliku .cer hello w magazynie głównym hello powitania klienta lub hosta zdalnego](#to-import-the-certificate-on-the-remote-host).</span><span class="sxs-lookup"><span data-stu-id="ac611-209">[Import hello .cer file into hello root store of hello client or remote host](#to-import-the-certificate-on-the-remote-host).</span></span>
* <span data-ttu-id="ac611-210">[Dodawanie pliku hosts toohello numerów seryjnych urządzeń hello na zdalnym hoście](#to-add-device-serial-numbers-to-the-remote-host).</span><span class="sxs-lookup"><span data-stu-id="ac611-210">[Add hello device serial numbers toohello hosts file on your remote host](#to-add-device-serial-numbers-to-the-remote-host).</span></span>

<span data-ttu-id="ac611-211">Poniżej opisano każdy z tych procedur.</span><span class="sxs-lookup"><span data-stu-id="ac611-211">Each of these procedures is described below.</span></span>

#### <a name="tooimport-hello-certificate-on-hello-remote-host"></a><span data-ttu-id="ac611-212">tooimport hello certyfikat na zdalnym hoście hello</span><span class="sxs-lookup"><span data-stu-id="ac611-212">tooimport hello certificate on hello remote host</span></span>
1. <span data-ttu-id="ac611-213">Kliknij prawym przyciskiem myszy plik cer hello i wybierz **instalacji certyfikatu**.</span><span class="sxs-lookup"><span data-stu-id="ac611-213">Right-click hello .cer file and select **Install certificate**.</span></span> <span data-ttu-id="ac611-214">Spowoduje to uruchomienie Kreatora importu certyfikatów hello.</span><span class="sxs-lookup"><span data-stu-id="ac611-214">This will start hello Certificate Import Wizard.</span></span>
   
    ![Kreator importu certyfikatów 1](./media/storsimple-remote-connect/HCS_CertificateImportWizard1.png)
2. <span data-ttu-id="ac611-216">Dla **lokalizacji magazynu**, wybierz pozycję **komputera lokalnego**, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="ac611-216">For **Store location**, select **Local Machine**, and then click **Next**.</span></span>
3. <span data-ttu-id="ac611-217">Wybierz **Umieść wszystkie certyfikaty w powitania po magazynu**, a następnie kliknij przycisk **Przeglądaj**.</span><span class="sxs-lookup"><span data-stu-id="ac611-217">Select **Place all certificates in hello following store**, and then click **Browse**.</span></span> <span data-ttu-id="ac611-218">Przejdź w magazynie głównym toohello dostęp do zdalnego hosta, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="ac611-218">Navigate toohello root store of your remote host, and then click **Next**.</span></span>
   
    ![Kreator importu certyfikatów 2](./media/storsimple-remote-connect/HCS_CertificateImportWizard2.png)
4. <span data-ttu-id="ac611-220">Kliknij przycisk **Zakończ**.</span><span class="sxs-lookup"><span data-stu-id="ac611-220">Click **Finish**.</span></span> <span data-ttu-id="ac611-221">Zostanie wyświetlony komunikat informujący o tym, że hello importowanie zakończyło się pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="ac611-221">A message that tells you that hello import was successful appears.</span></span>
   
    ![Kreator importu certyfikatów 3](./media/storsimple-remote-connect/HCS_CertificateImportWizard3.png)

#### <a name="tooadd-device-serial-numbers-toohello-remote-host"></a><span data-ttu-id="ac611-223">host zdalny numery seryjne toohello tooadd urządzenia</span><span class="sxs-lookup"><span data-stu-id="ac611-223">tooadd device serial numbers toohello remote host</span></span>
1. <span data-ttu-id="ac611-224">Uruchom program Notatnik jako administrator, a następnie otwórz plik hosts hello znajdujący się w \Windows\System32\Drivers\etc.</span><span class="sxs-lookup"><span data-stu-id="ac611-224">Start Notepad as an administrator, and then open hello hosts file located at \Windows\System32\Drivers\etc.</span></span>
2. <span data-ttu-id="ac611-225">Dodaj następujące trzy pliku hosts tooyour wpisy hello: **adres IP interfejsu dane 0**, **adresu IP stałym kontrolera 0**, i **adres IP stałym kontrolera 1**.</span><span class="sxs-lookup"><span data-stu-id="ac611-225">Add hello following three entries tooyour hosts file: **DATA 0 IP address**, **Controller 0 Fixed IP address**, and **Controller 1 Fixed IP address**.</span></span>
3. <span data-ttu-id="ac611-226">Wprowadź numer seryjny urządzenia hello, który został wcześniej zapisany.</span><span class="sxs-lookup"><span data-stu-id="ac611-226">Enter hello device serial number that you saved earlier.</span></span> <span data-ttu-id="ac611-227">Ten adres IP toohello mapy, pokazane na powitania po obrazu.</span><span class="sxs-lookup"><span data-stu-id="ac611-227">Map this toohello IP address as shown in hello following image.</span></span> <span data-ttu-id="ac611-228">Dla kontrolera 0 i kontrolera 1, dołącz **Controller0** i **kontroler1** na końcu hello hello numeru seryjnego (nazwa Pospolita).</span><span class="sxs-lookup"><span data-stu-id="ac611-228">For Controller 0 and Controller 1, append **Controller0** and **Controller1** at hello end of hello serial number (CN name).</span></span>
   
    ![Dodawanie pliku toohosts nazwa Pospolita](./media/storsimple-remote-connect/HCS_AddingCNNameToHostsFile.png)
4. <span data-ttu-id="ac611-230">Plik hosts hello Zapisz.</span><span class="sxs-lookup"><span data-stu-id="ac611-230">Save hello hosts file.</span></span>

### <a name="connect-toohello-device-from-hello-remote-host"></a><span data-ttu-id="ac611-231">Podłącz urządzenie toohello z hostem zdalnym hello</span><span class="sxs-lookup"><span data-stu-id="ac611-231">Connect toohello device from hello remote host</span></span>
<span data-ttu-id="ac611-232">Użyj programu Windows PowerShell i protokołu SSL tooenter jako SSAdmin sesję na swoim urządzeniu, z hosta zdalnego lub klienta.</span><span class="sxs-lookup"><span data-stu-id="ac611-232">Use Windows PowerShell and SSL tooenter an SSAdmin session on your device from a remote host or client.</span></span> <span data-ttu-id="ac611-233">Sesja SSAdmin Hello mapuje toooption 1 w hello [konsoli szeregowej](storsimple-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console) menu urządzenia.</span><span class="sxs-lookup"><span data-stu-id="ac611-233">hello SSAdmin session maps toooption 1 in hello [serial console](storsimple-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console) menu of your device.</span></span>

<span data-ttu-id="ac611-234">Wykonaj następujące procedury na komputerze hello, z którego mają połączenia zdalnego programu Windows PowerShell hello toomake hello.</span><span class="sxs-lookup"><span data-stu-id="ac611-234">Perform hello following procedure on hello computer from which you want toomake hello remote Windows PowerShell connection.</span></span>

#### <a name="tooenter-an-ssadmin-session-on-hello-device-by-using-windows-powershell-and-ssl"></a><span data-ttu-id="ac611-235">tooenter jako SSAdmin sesji na urządzeniu hello za pomocą środowiska Windows PowerShell i SSL</span><span class="sxs-lookup"><span data-stu-id="ac611-235">tooenter an SSAdmin session on hello device by using Windows PowerShell and SSL</span></span>
1. <span data-ttu-id="ac611-236">Uruchom sesję programu Windows PowerShell jako administrator.</span><span class="sxs-lookup"><span data-stu-id="ac611-236">Start a Windows PowerShell session as an administrator.</span></span>
2. <span data-ttu-id="ac611-237">Dodaj hello urządzenia IP address toohello klienta zaufanych hostów, wpisując:</span><span class="sxs-lookup"><span data-stu-id="ac611-237">Add hello device IP address toohello client’s trusted hosts by typing:</span></span>
   
     `Set-Item wsman:\localhost\Client\TrustedHosts <device_ip> -Concatenate -Force`
   
    <span data-ttu-id="ac611-238">Gdzie <*device_ip*> hello adres IP urządzenia, na przykład:</span><span class="sxs-lookup"><span data-stu-id="ac611-238">Where <*device_ip*> is hello IP address of your device; for example:</span></span> 
   
     `Set-Item wsman:\localhost\Client\TrustedHosts 10.126.173.90 -Concatenate -Force`
3. <span data-ttu-id="ac611-239">Należy utworzyć nowe poświadczenie, wpisując:</span><span class="sxs-lookup"><span data-stu-id="ac611-239">Create a new credential by typing:</span></span> 
   
     `$cred = New-Object pscredential @("<IP of target device>\SSAdmin", (ConvertTo-SecureString -Force -AsPlainText "<Device Administrator Password>"))`
   
    <span data-ttu-id="ac611-240">Gdzie <*IP urządzenie docelowe*> jest adresem IP hello dane 0 dla urządzenia; na przykład **10.126.173.90** pokazane na powitania poprzedzających obrazu pliku hosts hello.</span><span class="sxs-lookup"><span data-stu-id="ac611-240">Where <*IP of target device*> is hello IP address of DATA 0 for your device; for example, **10.126.173.90** as shown in hello preceding image of hello hosts file.</span></span> <span data-ttu-id="ac611-241">Ponadto podaj hello hasło administratora urządzenia.</span><span class="sxs-lookup"><span data-stu-id="ac611-241">Also, supply hello administrator password for your device.</span></span>
4. <span data-ttu-id="ac611-242">Utwórz sesję, wpisując:</span><span class="sxs-lookup"><span data-stu-id="ac611-242">Create a session by typing:</span></span>
   
     `$session = New-PSSession -UseSSL -ComputerName <Serial number of target device> -Credential $cred -ConfigurationName "SSAdminConsole"`
   
    <span data-ttu-id="ac611-243">Dla parametru - ComputerName hello w poleceniu cmdlet hello, podaj hello <*numer seryjny urządzenia docelowego*>.</span><span class="sxs-lookup"><span data-stu-id="ac611-243">For hello -ComputerName parameter in hello cmdlet, provide hello <*serial number of target device*>.</span></span> <span data-ttu-id="ac611-244">Ten numer seryjny został zamapowany toohello adres IP interfejsu dane 0 w pliku hosts hello na zdalnym hoście; na przykład **SHX0991003G44MT** pokazane na powitania po obrazu.</span><span class="sxs-lookup"><span data-stu-id="ac611-244">This serial number was mapped toohello IP address of DATA 0 in hello hosts file on your remote host; for example, **SHX0991003G44MT** as shown in hello following image.</span></span>
5. <span data-ttu-id="ac611-245">Wpisz:</span><span class="sxs-lookup"><span data-stu-id="ac611-245">Type:</span></span> 
   
     `Enter-PSSession $session`
6. <span data-ttu-id="ac611-246">Należy toowait za kilka minut, a następnie będzie tooyour podłączonego urządzenia za pośrednictwem protokołu HTTPS przy użyciu protokołu SSL.</span><span class="sxs-lookup"><span data-stu-id="ac611-246">You will need toowait a few minutes, and then you will be connected tooyour device via HTTPS over SSL.</span></span> <span data-ttu-id="ac611-247">Zostanie wyświetlony komunikat, który wskazuje, że jesteś tooyour podłączonych urządzeń.</span><span class="sxs-lookup"><span data-stu-id="ac611-247">You will see a message that indicates you are connected tooyour device.</span></span>
   
    ![Usługi zdalne środowiska PowerShell przy użyciu protokołu HTTPS i SSL](./media/storsimple-remote-connect/HCS_PSRemotingUsingHTTPSAndSSL.png)

## <a name="next-steps"></a><span data-ttu-id="ac611-249">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="ac611-249">Next steps</span></span>
* <span data-ttu-id="ac611-250">Dowiedz się więcej o [przy użyciu programu Windows PowerShell tooadminister urządzenia StorSimple](storsimple-windows-powershell-administration.md).</span><span class="sxs-lookup"><span data-stu-id="ac611-250">Learn more about [using Windows PowerShell tooadminister your StorSimple device](storsimple-windows-powershell-administration.md).</span></span>
* <span data-ttu-id="ac611-251">Dowiedz się więcej o [tooadminister usługi Menedżer StorSimple przy użyciu hello urządzenia StorSimple](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="ac611-251">Learn more about [using hello StorSimple Manager service tooadminister your StorSimple device](storsimple-manager-service-administration.md).</span></span>

