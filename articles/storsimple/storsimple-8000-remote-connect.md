---
title: "aaaConnect zdalnie tooyour urządzenia StorSimple | Dokumentacja firmy Microsoft"
description: "Wyjaśniono, jak tooconfigure Twojego urządzenia pod kątem zarządzania zdalnego i w jaki sposób tooWindows tooconnect programu PowerShell dla StorSimple za pośrednictwem protokołu HTTP lub HTTPS."
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
ms.openlocfilehash: 38b6a6350891b9f6f8fdfc55880b2f47105d947c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-remotely-tooyour-storsimple-8000-series-device"></a><span data-ttu-id="6b6c1-103">Zdalne połączenia urządzenia z serii StorSimple 8000 tooyour</span><span class="sxs-lookup"><span data-stu-id="6b6c1-103">Connect remotely tooyour StorSimple 8000 series device</span></span>

## <a name="overview"></a><span data-ttu-id="6b6c1-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="6b6c1-104">Overview</span></span>

<span data-ttu-id="6b6c1-105">Można zdalnie połączyć urządzenie tooyour za pomocą środowiska Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6b6c1-105">You can remotely connect tooyour device via Windows PowerShell.</span></span> <span data-ttu-id="6b6c1-106">Po ustanowieniu połączenia w ten sposób nie ma menu.</span><span class="sxs-lookup"><span data-stu-id="6b6c1-106">When you connect this way, you do not see a menu.</span></span> <span data-ttu-id="6b6c1-107">(Możesz zobaczyć menu tylko wtedy, gdy używasz konsoli szeregowej hello na powitania tooconnect urządzenia). Za pomocą komunikacji zdalnej programu Windows PowerShell należy połączyć tooa określonego obszaru działania.</span><span class="sxs-lookup"><span data-stu-id="6b6c1-107">(You see a menu only if you use hello serial console on hello device tooconnect.) With Windows PowerShell remoting, you connect tooa specific runspace.</span></span> <span data-ttu-id="6b6c1-108">Można również określić język wyświetlania hello.</span><span class="sxs-lookup"><span data-stu-id="6b6c1-108">You can also specify hello display language.</span></span>

<span data-ttu-id="6b6c1-109">Aby uzyskać więcej informacji o używaniu toomanage komunikacji zdalnej programu Windows PowerShell urządzeniu Przejdź zbyt[Użyj środowiska Windows PowerShell dla StorSimple tooadminister urządzenia StorSimple](storsimple-8000-windows-powershell-administration.md).</span><span class="sxs-lookup"><span data-stu-id="6b6c1-109">For more information about using Windows PowerShell remoting toomanage your device, go too[Use Windows PowerShell for StorSimple tooadminister your StorSimple device](storsimple-8000-windows-powershell-administration.md).</span></span>

<span data-ttu-id="6b6c1-110">Ten samouczek wyjaśnia sposób tooconfigure Twojego urządzenia pod kątem zarządzania zdalnego, a następnie jak tooWindows tooconnect programu PowerShell dla StorSimple.</span><span class="sxs-lookup"><span data-stu-id="6b6c1-110">This tutorial explains how tooconfigure your device for remote management and then how tooconnect tooWindows PowerShell for StorSimple.</span></span> <span data-ttu-id="6b6c1-111">Korzystanie z protokołu HTTP lub HTTPS tooremotely połączenia za pomocą środowiska Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6b6c1-111">You can use HTTP or HTTPS tooremotely connect via Windows PowerShell.</span></span> <span data-ttu-id="6b6c1-112">Jednak podczas decydowania jak tooWindows tooconnect programu PowerShell dla StorSimple, należy wziąć pod uwagę hello następujących informacji:</span><span class="sxs-lookup"><span data-stu-id="6b6c1-112">However, when you are deciding how tooconnect tooWindows PowerShell for StorSimple, consider hello following information:</span></span>

* <span data-ttu-id="6b6c1-113">Łączenie bezpośrednio toohello konsoli szeregowej urządzenia jest bezpieczne, ale nie jest łączącego konsoli szeregowej toohello za pośrednictwem przełączników sieciowych.</span><span class="sxs-lookup"><span data-stu-id="6b6c1-113">Connecting directly toohello device serial console is secure, but connecting toohello serial console over network switches is not.</span></span> <span data-ttu-id="6b6c1-114">Należy uważać na powitania ryzyko związane z zabezpieczeniami podczas łączenia z konsolą szeregową urządzenia toohello za pośrednictwem przełączników sieciowych.</span><span class="sxs-lookup"><span data-stu-id="6b6c1-114">Be cautious of hello security risk when connecting toohello device serial console over network switches.</span></span>
* <span data-ttu-id="6b6c1-115">Łączących się za pośrednictwem sesji HTTP może oferować lepsze bezpieczeństwo niż łączących się za pośrednictwem konsoli szeregowej hello hello sieci.</span><span class="sxs-lookup"><span data-stu-id="6b6c1-115">Connecting through an HTTP session might offer more security than connecting through hello serial console over hello network.</span></span> <span data-ttu-id="6b6c1-116">Chociaż nie jest to najbezpieczniejsza metoda hello, jest dopuszczalne w zaufanych sieciach.</span><span class="sxs-lookup"><span data-stu-id="6b6c1-116">Although this is not hello most secure method, it is acceptable on trusted networks.</span></span>
* <span data-ttu-id="6b6c1-117">Łączących się za pośrednictwem sesji protokołu HTTPS z certyfikatu z podpisem własnym jest hello najbardziej bezpieczne i hello zalecana opcja.</span><span class="sxs-lookup"><span data-stu-id="6b6c1-117">Connecting through an HTTPS session with a self-signed certificate is hello most secure and hello recommended option.</span></span>

<span data-ttu-id="6b6c1-118">Możesz połączyć zdalnie toohello interfejsu programu Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6b6c1-118">You can connect remotely toohello Windows PowerShell interface.</span></span> <span data-ttu-id="6b6c1-119">Jednak urządzenia StorSimple tooyour dostępu zdalnego za pośrednictwem interfejsu programu Windows PowerShell hello nie jest włączona domyślnie.</span><span class="sxs-lookup"><span data-stu-id="6b6c1-119">However, remote access tooyour StorSimple device via hello Windows PowerShell interface is not enabled by default.</span></span> <span data-ttu-id="6b6c1-120">Należy najpierw włączyć zdalne zarządzanie na urządzeniu hello, a następnie na hello klienta, który jest używany tooaccess urządzenia.</span><span class="sxs-lookup"><span data-stu-id="6b6c1-120">You must enable remote management on hello device first, and then on hello client that is used tooaccess your device.</span></span>

<span data-ttu-id="6b6c1-121">Witaj opisane w tym artykule wykonano na komputerze hosta z systemem Windows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="6b6c1-121">hello steps described in this article were performed on a host system running Windows Server 2012 R2.</span></span>

## <a name="connect-through-http"></a><span data-ttu-id="6b6c1-122">Łączenie się za pośrednictwem protokołu HTTP</span><span class="sxs-lookup"><span data-stu-id="6b6c1-122">Connect through HTTP</span></span>

<span data-ttu-id="6b6c1-123">Łączenie tooWindows środowiska PowerShell dla urządzenia StorSimple za pośrednictwem sesji HTTP oferuje lepsze zabezpieczenia niż łączących się za pośrednictwem konsoli szeregowej hello urządzenia StorSimple.</span><span class="sxs-lookup"><span data-stu-id="6b6c1-123">Connecting tooWindows PowerShell for StorSimple through an HTTP session offers more security than connecting through hello serial console of your StorSimple device.</span></span> <span data-ttu-id="6b6c1-124">Chociaż nie jest to najbezpieczniejsza metoda hello, jest dopuszczalne w zaufanych sieciach.</span><span class="sxs-lookup"><span data-stu-id="6b6c1-124">Although this is not hello most secure method, it is acceptable on trusted networks.</span></span>

<span data-ttu-id="6b6c1-125">Możesz użyć albo hello Azure portalu lub hello konsoli szeregowej tooconfigure zdalnego zarządzania.</span><span class="sxs-lookup"><span data-stu-id="6b6c1-125">You can use either hello Azure portal or hello serial console tooconfigure remote management.</span></span> <span data-ttu-id="6b6c1-126">Wybierz jedną z procedur przedstawionych hello:</span><span class="sxs-lookup"><span data-stu-id="6b6c1-126">Select from hello following procedures:</span></span>

* [<span data-ttu-id="6b6c1-127">Użyj hello Azure tooenable portalu zdalnego zarządzania za pośrednictwem protokołu HTTP</span><span class="sxs-lookup"><span data-stu-id="6b6c1-127">Use hello Azure portal tooenable remote management over HTTP</span></span>](#use-the-azure-classic-portal-to-enable-remote-management-over-http)
* [<span data-ttu-id="6b6c1-128">Użyj konsoli szeregowej hello tooenable zdalnego zarządzania za pośrednictwem protokołu HTTP</span><span class="sxs-lookup"><span data-stu-id="6b6c1-128">Use hello serial console tooenable remote management over HTTP</span></span>](#use-the-serial-console-to-enable-remote-management-over-http)

<span data-ttu-id="6b6c1-129">Po włączeniu zdalnego zarządzania za pomocą hello następujące procedury tooprepare powitania klienta dla połączenia zdalnego.</span><span class="sxs-lookup"><span data-stu-id="6b6c1-129">After you enable remote management, use hello following procedure tooprepare hello client for a remote connection.</span></span>

* [<span data-ttu-id="6b6c1-130">Przygotuj powitania klienta dla połączenia zdalnego</span><span class="sxs-lookup"><span data-stu-id="6b6c1-130">Prepare hello client for remote connection</span></span>](#prepare-the-client-for-remote-connection)

### <a name="use-hello-azure-portal-tooenable-remote-management-over-http"></a><span data-ttu-id="6b6c1-131">Użyj hello Azure tooenable portalu zdalnego zarządzania za pośrednictwem protokołu HTTP</span><span class="sxs-lookup"><span data-stu-id="6b6c1-131">Use hello Azure portal tooenable remote management over HTTP</span></span>

<span data-ttu-id="6b6c1-132">Wykonaj hello, wykonaj następujące kroki w hello Azure tooenable portalu zdalnego zarządzania za pośrednictwem protokołu HTTP.</span><span class="sxs-lookup"><span data-stu-id="6b6c1-132">Perform hello following steps in hello Azure portal tooenable remote management over HTTP.</span></span>

#### <a name="tooenable-remote-management-through-hello-azure-portal"></a><span data-ttu-id="6b6c1-133">tooenable zarządzanie zdalne za pomocą hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="6b6c1-133">tooenable remote management through hello Azure portal</span></span>

1. <span data-ttu-id="6b6c1-134">Przejdź tooyour usługi Menedżer urządzeń StorSimple.</span><span class="sxs-lookup"><span data-stu-id="6b6c1-134">Go tooyour StorSimple Device Manager service.</span></span> <span data-ttu-id="6b6c1-135">Wybierz **urządzeń** , a następnie wybierz i kliknij przycisk hello urządzenie tooconfigure do zdalnego zarządzania.</span><span class="sxs-lookup"><span data-stu-id="6b6c1-135">Select **Devices** and then select and click hello device you want tooconfigure for remote management.</span></span> <span data-ttu-id="6b6c1-136">Przejdź za**ustawienia urządzenia > zabezpieczeń**.</span><span class="sxs-lookup"><span data-stu-id="6b6c1-136">Go too**Device settings > Security**.</span></span>
2. <span data-ttu-id="6b6c1-137">W hello **ustawienia zabezpieczeń** bloku, kliknij przycisk **zdalnego zarządzania**.</span><span class="sxs-lookup"><span data-stu-id="6b6c1-137">In hello **Security settings** blade, click **Remote Management**.</span></span>
3. <span data-ttu-id="6b6c1-138">W hello **zdalnego zarządzania** ustawić bloku **włączyć zdalne zarządzanie** za**tak**.</span><span class="sxs-lookup"><span data-stu-id="6b6c1-138">In hello **Remote management** blade, set **Enable Remote Management** too**Yes**.</span></span>
4. <span data-ttu-id="6b6c1-139">Teraz możesz tooconnect przy użyciu protokołu HTTP.</span><span class="sxs-lookup"><span data-stu-id="6b6c1-139">You can now choose tooconnect using HTTP.</span></span> <span data-ttu-id="6b6c1-140">(domyślnie hello jest tooconnect za pośrednictwem protokołu HTTPS). Upewnij się, że wybrano HTTP.</span><span class="sxs-lookup"><span data-stu-id="6b6c1-140">(hello default is tooconnect over HTTPS.) Make sure that HTTP is selected.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="6b6c1-141">Łączenie za pośrednictwem protokołu HTTP jest dopuszczalne tylko w sieciach zaufanych.</span><span class="sxs-lookup"><span data-stu-id="6b6c1-141">Connecting over HTTP is acceptable only on trusted networks.</span></span>
   
5. <span data-ttu-id="6b6c1-142">Kliknij przycisk **zapisać** i po wyświetleniu monitu o potwierdzenie, wybierz **tak**.</span><span class="sxs-lookup"><span data-stu-id="6b6c1-142">Click **Save** and when prompted for confirmation, select **Yes**.</span></span>

### <a name="use-hello-serial-console-tooenable-remote-management-over-http"></a><span data-ttu-id="6b6c1-143">Użyj konsoli szeregowej hello tooenable zdalnego zarządzania za pośrednictwem protokołu HTTP</span><span class="sxs-lookup"><span data-stu-id="6b6c1-143">Use hello serial console tooenable remote management over HTTP</span></span>
<span data-ttu-id="6b6c1-144">Wykonaj następujące kroki na powitania urządzenia konsoli szeregowej tooenable zdalne zarządzanie hello.</span><span class="sxs-lookup"><span data-stu-id="6b6c1-144">Perform hello following steps on hello device serial console tooenable remote management.</span></span>

#### <a name="tooenable-remote-management-through-hello-device-serial-console"></a><span data-ttu-id="6b6c1-145">tooenable zdalnego zarządzania za pośrednictwem konsoli szeregowej urządzenia hello</span><span class="sxs-lookup"><span data-stu-id="6b6c1-145">tooenable remote management through hello device serial console</span></span>
1. <span data-ttu-id="6b6c1-146">Menu konsoli szeregowej hello wybierz opcję 1.</span><span class="sxs-lookup"><span data-stu-id="6b6c1-146">On hello serial console menu, select option 1.</span></span> <span data-ttu-id="6b6c1-147">Aby uzyskać więcej informacji o używaniu konsoli szeregowej hello na urządzeniu hello Przejdź zbyt[łączenie tooWindows środowiska PowerShell dla urządzenia StorSimple za pośrednictwem konsoli szeregowej urządzenia](storsimple-8000-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="6b6c1-147">For more information about using hello serial console on hello device, go too[Connect tooWindows PowerShell for StorSimple via device serial console](storsimple-8000-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console).</span></span>
2. <span data-ttu-id="6b6c1-148">Witaj, wpisz w wierszu:`Enable-HcsRemoteManagement –AllowHttp`</span><span class="sxs-lookup"><span data-stu-id="6b6c1-148">At hello prompt, type: `Enable-HcsRemoteManagement –AllowHttp`</span></span>
3. <span data-ttu-id="6b6c1-149">Użytkownik jest powiadamiany o hello luk w zabezpieczeniach systemu przy użyciu protokołu HTTP tooconnect toohello urządzenia.</span><span class="sxs-lookup"><span data-stu-id="6b6c1-149">You are notified about hello security vulnerabilities of using HTTP tooconnect toohello device.</span></span> <span data-ttu-id="6b6c1-150">Po wyświetleniu monitu Potwierdź, wpisując **Y**.</span><span class="sxs-lookup"><span data-stu-id="6b6c1-150">When prompted, confirm by typing **Y**.</span></span>
4. <span data-ttu-id="6b6c1-151">Sprawdź, czy HTTP jest włączona, wpisując:`Get-HcsSystem`</span><span class="sxs-lookup"><span data-stu-id="6b6c1-151">Verify that HTTP is enabled by typing: `Get-HcsSystem`</span></span>
5. <span data-ttu-id="6b6c1-152">Sprawdź, że hello **RemoteManagementMode** pola pokazuje **HttpsAndHttpEnabled**.hello następującej ilustracji przedstawiono te ustawienia programu PuTTY.</span><span class="sxs-lookup"><span data-stu-id="6b6c1-152">Verify that hello **RemoteManagementMode** field shows **HttpsAndHttpEnabled**.hello following illustration shows these settings in PuTTY.</span></span>
   
     ![Serial HTTPS i HTTP włączone](./media/storsimple-remote-connect/HCS_SerialHttpsAndHttpEnabled.png)

### <a name="prepare-hello-client-for-remote-connection"></a><span data-ttu-id="6b6c1-154">Przygotuj powitania klienta dla połączenia zdalnego</span><span class="sxs-lookup"><span data-stu-id="6b6c1-154">Prepare hello client for remote connection</span></span>
<span data-ttu-id="6b6c1-155">Wykonaj następujące kroki na powitania klienta tooenable zdalne zarządzanie hello.</span><span class="sxs-lookup"><span data-stu-id="6b6c1-155">Perform hello following steps on hello client tooenable remote management.</span></span>

#### <a name="tooprepare-hello-client-for-remote-connection"></a><span data-ttu-id="6b6c1-156">tooprepare powitania klienta dla połączenia zdalnego</span><span class="sxs-lookup"><span data-stu-id="6b6c1-156">tooprepare hello client for remote connection</span></span>
1. <span data-ttu-id="6b6c1-157">Uruchom sesję programu Windows PowerShell jako administrator.</span><span class="sxs-lookup"><span data-stu-id="6b6c1-157">Start a Windows PowerShell session as an administrator.</span></span>
2. <span data-ttu-id="6b6c1-158">Wpisz hello następującego adresu IP hello tooadd polecenia listy zaufanych hostów hello StorSimple urządzenia toohello klienta:</span><span class="sxs-lookup"><span data-stu-id="6b6c1-158">Type hello following command tooadd hello IP address of hello StorSimple device toohello client’s trusted hosts list:</span></span>
   
     `Set-Item wsman:\localhost\Client\TrustedHosts <device_ip> -Concatenate -Force`
   
     <span data-ttu-id="6b6c1-159">Zastąp <*device_ip*> o adresie IP hello urządzenia; na przykład:</span><span class="sxs-lookup"><span data-stu-id="6b6c1-159">Replace <*device_ip*> with hello IP address of your device; for example:</span></span> 
   
     `Set-Item wsman:\localhost\Client\TrustedHosts 10.126.173.90 -Concatenate -Force`
3. <span data-ttu-id="6b6c1-160">Następujące polecenie toosave hello urządzenia poświadczeń w zmiennej hello typu:</span><span class="sxs-lookup"><span data-stu-id="6b6c1-160">Type hello following command toosave hello device credentials in a variable:</span></span> 
   
    ```
    $cred = Get-Credential
    ```
    
4. <span data-ttu-id="6b6c1-161">W hello pojawi się okno dialogowe:</span><span class="sxs-lookup"><span data-stu-id="6b6c1-161">In hello dialog box that appears:</span></span>
   
   1. <span data-ttu-id="6b6c1-162">Wpisz nazwę użytkownika hello w następującym formacie: *device_ip\SSAdmin*.</span><span class="sxs-lookup"><span data-stu-id="6b6c1-162">Type hello user name in this format: *device_ip\SSAdmin*.</span></span>
   2. <span data-ttu-id="6b6c1-163">Wpisz hasło administratora urządzenia hello, która została ustawiona, gdy urządzenie hello został skonfigurowany z kreatorem hello.</span><span class="sxs-lookup"><span data-stu-id="6b6c1-163">Type hello device administrator password that was set when hello device was configured with hello setup wizard.</span></span> <span data-ttu-id="6b6c1-164">Witaj domyślne hasło jest *Password1*.</span><span class="sxs-lookup"><span data-stu-id="6b6c1-164">hello default password is *Password1*.</span></span>
5. <span data-ttu-id="6b6c1-165">Uruchom sesję programu Windows PowerShell na urządzeniu hello, wpisując polecenie:</span><span class="sxs-lookup"><span data-stu-id="6b6c1-165">Start a Windows PowerShell session on hello device by typing this command:</span></span>
   
     `Enter-PSSession -Credential $cred -ConfigurationName SSAdminConsole -ComputerName <device_ip>`
   
   > [!NOTE]
   > <span data-ttu-id="6b6c1-166">toocreate sesję programu Windows PowerShell do użytku z urządzenia wirtualnego StorSimple hello, Dołącz hello `–Port` parametru i określ port publiczny hello skonfigurowanego w komunikację zdalną dla urządzenia wirtualnego StorSimple.</span><span class="sxs-lookup"><span data-stu-id="6b6c1-166">toocreate a Windows PowerShell session for use with hello StorSimple virtual device, append hello `–Port` parameter and specify hello public port that you configured in Remoting for StorSimple Virtual Appliance.</span></span>
   
   
<span data-ttu-id="6b6c1-167">W tym momencie powinien mieć active środowiska Windows PowerShell sesji toohello urządzeniu zdalnym.</span><span class="sxs-lookup"><span data-stu-id="6b6c1-167">At this point, you should have an active remote Windows PowerShell session toohello device.</span></span>
   
![Usługi zdalne środowiska PowerShell przy użyciu protokołu HTTP](./media/storsimple-remote-connect/HCS_PSRemotingUsingHTTP.png)

## <a name="connect-through-https"></a><span data-ttu-id="6b6c1-169">Łączenie się za pośrednictwem protokołu HTTPS</span><span class="sxs-lookup"><span data-stu-id="6b6c1-169">Connect through HTTPS</span></span>

<span data-ttu-id="6b6c1-170">Łączenie tooWindows środowiska PowerShell dla urządzenia StorSimple za pomocą sesji protokołu HTTPS jest hello najbardziej bezpieczne i zalecana metoda tooyour zdalnie łączącego się urządzenia Microsoft Azure StorSimple.</span><span class="sxs-lookup"><span data-stu-id="6b6c1-170">Connecting tooWindows PowerShell for StorSimple through an HTTPS session is hello most secure and recommended method of remotely connecting tooyour Microsoft Azure StorSimple device.</span></span> <span data-ttu-id="6b6c1-171">Hello następujące procedury wyjaśniają, jak tooset się hello serial konsoli i komputerów klienckich, dzięki czemu może używać protokołu HTTPS tooconnect tooWindows programu PowerShell dla urządzenia StorSimple.</span><span class="sxs-lookup"><span data-stu-id="6b6c1-171">hello following procedures explain how tooset up hello serial console and client computers so that you can use HTTPS tooconnect tooWindows PowerShell for StorSimple.</span></span>

<span data-ttu-id="6b6c1-172">Możesz użyć albo hello Azure portalu lub hello konsoli szeregowej tooconfigure zdalnego zarządzania.</span><span class="sxs-lookup"><span data-stu-id="6b6c1-172">You can use either hello Azure portal or hello serial console tooconfigure remote management.</span></span> <span data-ttu-id="6b6c1-173">Wybierz jedną z procedur przedstawionych hello:</span><span class="sxs-lookup"><span data-stu-id="6b6c1-173">Select from hello following procedures:</span></span>

* [<span data-ttu-id="6b6c1-174">Użyj hello Azure tooenable portalu zdalnego zarządzania za pośrednictwem protokołu HTTPS</span><span class="sxs-lookup"><span data-stu-id="6b6c1-174">Use hello Azure portal tooenable remote management over HTTPS</span></span>](#use-the-azure-classic-portal-to-enable-remote-management-over-https)
* [<span data-ttu-id="6b6c1-175">Użyj konsoli szeregowej hello tooenable zdalnego zarządzania za pośrednictwem protokołu HTTPS</span><span class="sxs-lookup"><span data-stu-id="6b6c1-175">Use hello serial console tooenable remote management over HTTPS</span></span>](#use-the-serial-console-to-enable-remote-management-over-https)

<span data-ttu-id="6b6c1-176">Po włączeniu zdalnego zarządzania przy użyciu hello następujące procedury tooprepare hello hosta do zdalnego zarządzania, a następnie podłącz urządzenie toohello z hostem zdalnym hello.</span><span class="sxs-lookup"><span data-stu-id="6b6c1-176">After you enable remote management, use hello following procedures tooprepare hello host for a remote management and connect toohello device from hello remote host.</span></span>

* [<span data-ttu-id="6b6c1-177">Przygotowanie hello hosta do zarządzania zdalnego</span><span class="sxs-lookup"><span data-stu-id="6b6c1-177">Prepare hello host for remote management</span></span>](#prepare-the-host-for-remote-management)
* [<span data-ttu-id="6b6c1-178">Podłącz urządzenie toohello z hostem zdalnym hello</span><span class="sxs-lookup"><span data-stu-id="6b6c1-178">Connect toohello device from hello remote host</span></span>](#connect-to-the-device-from-the-remote-host)

### <a name="use-hello-azure-portal-tooenable-remote-management-over-https"></a><span data-ttu-id="6b6c1-179">Użyj hello Azure tooenable portalu zdalnego zarządzania za pośrednictwem protokołu HTTPS</span><span class="sxs-lookup"><span data-stu-id="6b6c1-179">Use hello Azure portal tooenable remote management over HTTPS</span></span>

<span data-ttu-id="6b6c1-180">Wykonaj hello, wykonaj następujące kroki w hello Azure tooenable portalu zdalnego zarządzania za pośrednictwem protokołu HTTPS.</span><span class="sxs-lookup"><span data-stu-id="6b6c1-180">Perform hello following steps in hello Azure portal tooenable remote management over HTTPS.</span></span>

#### <a name="tooenable-remote-management-over-https-from-hello-azure-portal"></a><span data-ttu-id="6b6c1-181">tooenable zdalne zarządzanie przy użyciu protokołu HTTPS z hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="6b6c1-181">tooenable remote management over HTTPS from hello Azure portal</span></span>

1. <span data-ttu-id="6b6c1-182">Przejdź tooyour usługi Menedżer urządzeń StorSimple.</span><span class="sxs-lookup"><span data-stu-id="6b6c1-182">Go tooyour StorSimple Device Manager service.</span></span> <span data-ttu-id="6b6c1-183">Wybierz **urządzeń** , a następnie wybierz i kliknij przycisk hello urządzenie tooconfigure do zdalnego zarządzania.</span><span class="sxs-lookup"><span data-stu-id="6b6c1-183">Select **Devices** and then select and click hello device you want tooconfigure for remote management.</span></span> <span data-ttu-id="6b6c1-184">Przejdź za**ustawienia urządzenia > zabezpieczeń**.</span><span class="sxs-lookup"><span data-stu-id="6b6c1-184">Go too**Device settings > Security**.</span></span>
2. <span data-ttu-id="6b6c1-185">W hello **ustawienia zabezpieczeń** bloku, kliknij przycisk **zdalnego zarządzania**.</span><span class="sxs-lookup"><span data-stu-id="6b6c1-185">In hello **Security settings** blade, click **Remote Management**.</span></span>
3. <span data-ttu-id="6b6c1-186">Ustaw **włączyć zdalne zarządzanie** za**tak**.</span><span class="sxs-lookup"><span data-stu-id="6b6c1-186">Set **Enable Remote Management** too**Yes**.</span></span>
4. <span data-ttu-id="6b6c1-187">Teraz możesz tooconnect przy użyciu protokołu HTTPS.</span><span class="sxs-lookup"><span data-stu-id="6b6c1-187">You can now choose tooconnect using HTTPS.</span></span> <span data-ttu-id="6b6c1-188">(domyślnie hello jest tooconnect za pośrednictwem protokołu HTTPS). Upewnij się, że wybrany jest protokół HTTPS.</span><span class="sxs-lookup"><span data-stu-id="6b6c1-188">(hello default is tooconnect over HTTPS.) Make sure that HTTPS is selected.</span></span>
5. <span data-ttu-id="6b6c1-189">Kliknij przycisk..., a następnie kliknij przycisk **Pobierz certyfikat zdalnego zarządzania**.</span><span class="sxs-lookup"><span data-stu-id="6b6c1-189">Click ... and then click **Download Remote Management Certificate**.</span></span> <span data-ttu-id="6b6c1-190">Określ toosave lokalizację tego pliku.</span><span class="sxs-lookup"><span data-stu-id="6b6c1-190">Specify a location toosave this file.</span></span> <span data-ttu-id="6b6c1-191">Należy tooinstall ten certyfikat na komputerze klienta lub hosta hello użyje tooconnect toohello urządzenia.</span><span class="sxs-lookup"><span data-stu-id="6b6c1-191">You need tooinstall this certificate on hello client or host computer that you will use tooconnect toohello device.</span></span>
6. <span data-ttu-id="6b6c1-192">Kliknij przycisk **zapisać** , a następnie kliknij przycisk **tak** po wyświetleniu monitu o potwierdzenie.</span><span class="sxs-lookup"><span data-stu-id="6b6c1-192">Click **Save** and then click **Yes** when prompted for confirmation.</span></span>

### <a name="use-hello-serial-console-tooenable-remote-management-over-https"></a><span data-ttu-id="6b6c1-193">Użyj konsoli szeregowej hello tooenable zdalnego zarządzania za pośrednictwem protokołu HTTPS</span><span class="sxs-lookup"><span data-stu-id="6b6c1-193">Use hello serial console tooenable remote management over HTTPS</span></span>

<span data-ttu-id="6b6c1-194">Wykonaj następujące kroki na powitania urządzenia konsoli szeregowej tooenable zdalne zarządzanie hello.</span><span class="sxs-lookup"><span data-stu-id="6b6c1-194">Perform hello following steps on hello device serial console tooenable remote management.</span></span>

#### <a name="tooenable-remote-management-through-hello-device-serial-console"></a><span data-ttu-id="6b6c1-195">tooenable zdalnego zarządzania za pośrednictwem konsoli szeregowej urządzenia hello</span><span class="sxs-lookup"><span data-stu-id="6b6c1-195">tooenable remote management through hello device serial console</span></span>
1. <span data-ttu-id="6b6c1-196">Menu konsoli szeregowej hello wybierz opcję 1.</span><span class="sxs-lookup"><span data-stu-id="6b6c1-196">On hello serial console menu, select option 1.</span></span> <span data-ttu-id="6b6c1-197">Aby uzyskać więcej informacji o używaniu konsoli szeregowej hello na urządzeniu hello Przejdź zbyt[łączenie tooWindows środowiska PowerShell dla urządzenia StorSimple za pośrednictwem konsoli szeregowej urządzenia](storsimple-8000-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="6b6c1-197">For more information about using hello serial console on hello device, go too[Connect tooWindows PowerShell for StorSimple via device serial console](storsimple-8000-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console).</span></span>
2. <span data-ttu-id="6b6c1-198">Witaj, wpisz w wierszu:</span><span class="sxs-lookup"><span data-stu-id="6b6c1-198">At hello prompt, type:</span></span>
   
     `Enable-HcsRemoteManagement`
   
    <span data-ttu-id="6b6c1-199">To należy włączyć protokół HTTPS na urządzeniu.</span><span class="sxs-lookup"><span data-stu-id="6b6c1-199">This should enable HTTPS on your device.</span></span>
3. <span data-ttu-id="6b6c1-200">Sprawdź, czy został włączony protokół HTTPS, wpisując:</span><span class="sxs-lookup"><span data-stu-id="6b6c1-200">Verify that HTTPS has been enabled by typing:</span></span> 
   
     `Get-HcsSystem`
   
    <span data-ttu-id="6b6c1-201">Upewnij się, że hello **RemoteManagementMode** pola pokazuje **HttpsEnabled**.hello następującej ilustracji przedstawiono te ustawienia programu PuTTY.</span><span class="sxs-lookup"><span data-stu-id="6b6c1-201">Make sure that hello **RemoteManagementMode** field shows **HttpsEnabled**.hello following illustration shows these settings in PuTTY.</span></span>
   
     ![Serial obsługujące protokół HTTPS.](./media/storsimple-remote-connect/HCS_SerialHttpsEnabled.png)
4. <span data-ttu-id="6b6c1-203">Z danych wyjściowych hello `Get-HcsSystem`, skopiuj numer seryjny hello hello urządzenia i zapisz go do późniejszego użycia.</span><span class="sxs-lookup"><span data-stu-id="6b6c1-203">From hello output of `Get-HcsSystem`, copy hello serial number of hello device and save it for later use.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="6b6c1-204">numer seryjny Hello mapuje toohello Nazwa CN certyfikatu hello.</span><span class="sxs-lookup"><span data-stu-id="6b6c1-204">hello serial number maps toohello CN name in hello certificate.</span></span>
   
5. <span data-ttu-id="6b6c1-205">Uzyskaj certyfikat zdalnego zarządzania, wpisując:</span><span class="sxs-lookup"><span data-stu-id="6b6c1-205">Obtain a remote management certificate by typing:</span></span> 
   
     `Get-HcsRemoteManagementCert`
   
    <span data-ttu-id="6b6c1-206">Pojawi się następujący certyfikat z podobnych toohello.</span><span class="sxs-lookup"><span data-stu-id="6b6c1-206">A certificate similar toohello following will appear.</span></span>
   
    ![Pobierz certyfikat zdalnego zarządzania](./media/storsimple-remote-connect/HCS_GetRemoteManagementCertificate.png)
6. <span data-ttu-id="6b6c1-208">Kopiowanie informacji hello w certyfikacie hello z **---BEGIN CERTIFICATE---** za**---END CERTIFICATE---** do edytora tekstu, takiego jak Notatnik, a następnie zapisz go jako plik cer.</span><span class="sxs-lookup"><span data-stu-id="6b6c1-208">Copy hello information in hello certificate from **-----BEGIN CERTIFICATE-----** too**-----END CERTIFICATE-----** into a text editor such as Notepad, and save it as a .cer file.</span></span> <span data-ttu-id="6b6c1-209">(Zostanie skopiowany hosta zdalnego tooyour plików, podczas przygotowywania hosta hello.)</span><span class="sxs-lookup"><span data-stu-id="6b6c1-209">(You will copy this file tooyour remote host when you prepare hello host.)</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="6b6c1-210">toogenerate nowego świadectwa, użyj hello `Set-HcsRemoteManagementCert` polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="6b6c1-210">toogenerate a new certificate, use hello `Set-HcsRemoteManagementCert` cmdlet.</span></span>
   
### <a name="prepare-hello-host-for-remote-management"></a><span data-ttu-id="6b6c1-211">Przygotowanie hello hosta do zarządzania zdalnego</span><span class="sxs-lookup"><span data-stu-id="6b6c1-211">Prepare hello host for remote management</span></span>

<span data-ttu-id="6b6c1-212">komputer hosta hello tooprepare połączenie zdalnego za pomocą sesji protokołu HTTPS, należy wykonać hello zgodnie z procedurami:</span><span class="sxs-lookup"><span data-stu-id="6b6c1-212">tooprepare hello host computer for a remote connection that uses an HTTPS session, perform hello following procedures:</span></span>

* <span data-ttu-id="6b6c1-213">[Importowanie pliku .cer hello w magazynie głównym hello powitania klienta lub hosta zdalnego](#to-import-the-certificate-on-the-remote-host).</span><span class="sxs-lookup"><span data-stu-id="6b6c1-213">[Import hello .cer file into hello root store of hello client or remote host](#to-import-the-certificate-on-the-remote-host).</span></span>
* <span data-ttu-id="6b6c1-214">[Dodawanie pliku hosts toohello numerów seryjnych urządzeń hello na zdalnym hoście](#to-add-device-serial-numbers-to-the-remote-host).</span><span class="sxs-lookup"><span data-stu-id="6b6c1-214">[Add hello device serial numbers toohello hosts file on your remote host](#to-add-device-serial-numbers-to-the-remote-host).</span></span>

<span data-ttu-id="6b6c1-215">Poniżej opisano każdego hello powyższej procedury.</span><span class="sxs-lookup"><span data-stu-id="6b6c1-215">Each of hello preceding procedures, is described below.</span></span>

#### <a name="tooimport-hello-certificate-on-hello-remote-host"></a><span data-ttu-id="6b6c1-216">tooimport hello certyfikat na zdalnym hoście hello</span><span class="sxs-lookup"><span data-stu-id="6b6c1-216">tooimport hello certificate on hello remote host</span></span>
1. <span data-ttu-id="6b6c1-217">Kliknij prawym przyciskiem myszy plik cer hello i wybierz **instalacji certyfikatu**.</span><span class="sxs-lookup"><span data-stu-id="6b6c1-217">Right-click hello .cer file and select **Install certificate**.</span></span> <span data-ttu-id="6b6c1-218">Spowoduje to uruchomienie Kreatora importu certyfikatów hello.</span><span class="sxs-lookup"><span data-stu-id="6b6c1-218">This starts hello Certificate Import Wizard.</span></span>
   
    ![Kreator importu certyfikatów 1](./media/storsimple-remote-connect/HCS_CertificateImportWizard1.png)
2. <span data-ttu-id="6b6c1-220">Dla **lokalizacji magazynu**, wybierz pozycję **komputera lokalnego**, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="6b6c1-220">For **Store location**, select **Local Machine**, and then click **Next**.</span></span>
3. <span data-ttu-id="6b6c1-221">Wybierz **Umieść wszystkie certyfikaty w powitania po magazynu**, a następnie kliknij przycisk **Przeglądaj**.</span><span class="sxs-lookup"><span data-stu-id="6b6c1-221">Select **Place all certificates in hello following store**, and then click **Browse**.</span></span> <span data-ttu-id="6b6c1-222">Przejdź w magazynie głównym toohello dostęp do zdalnego hosta, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="6b6c1-222">Navigate toohello root store of your remote host, and then click **Next**.</span></span>
   
    ![Kreator importu certyfikatów 2](./media/storsimple-remote-connect/HCS_CertificateImportWizard2.png)
4. <span data-ttu-id="6b6c1-224">Kliknij przycisk **Zakończ**.</span><span class="sxs-lookup"><span data-stu-id="6b6c1-224">Click **Finish**.</span></span> <span data-ttu-id="6b6c1-225">Zostanie wyświetlony komunikat informujący o tym, że hello importowanie zakończyło się pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="6b6c1-225">A message that tells you that hello import was successful appears.</span></span>
   
    ![Kreator importu certyfikatów 3](./media/storsimple-remote-connect/HCS_CertificateImportWizard3.png)

#### <a name="tooadd-device-serial-numbers-toohello-remote-host"></a><span data-ttu-id="6b6c1-227">host zdalny numery seryjne toohello tooadd urządzenia</span><span class="sxs-lookup"><span data-stu-id="6b6c1-227">tooadd device serial numbers toohello remote host</span></span>
1. <span data-ttu-id="6b6c1-228">Uruchom program Notatnik jako administrator, a następnie otwórz plik hosts hello znajdujący się w \Windows\System32\Drivers\etc.</span><span class="sxs-lookup"><span data-stu-id="6b6c1-228">Start Notepad as an administrator, and then open hello hosts file located at \Windows\System32\Drivers\etc.</span></span>
2. <span data-ttu-id="6b6c1-229">Dodaj następujące trzy pliku hosts tooyour wpisy hello: **adres IP interfejsu dane 0**, **adresu IP stałym kontrolera 0**, i **adres IP stałym kontrolera 1**.</span><span class="sxs-lookup"><span data-stu-id="6b6c1-229">Add hello following three entries tooyour hosts file: **DATA 0 IP address**, **Controller 0 Fixed IP address**, and **Controller 1 Fixed IP address**.</span></span>
3. <span data-ttu-id="6b6c1-230">Wprowadź numer seryjny urządzenia hello, który został wcześniej zapisany.</span><span class="sxs-lookup"><span data-stu-id="6b6c1-230">Enter hello device serial number that you saved earlier.</span></span> <span data-ttu-id="6b6c1-231">Ten adres IP toohello mapy, pokazane na powitania po obrazu.</span><span class="sxs-lookup"><span data-stu-id="6b6c1-231">Map this toohello IP address as shown in hello following image.</span></span> <span data-ttu-id="6b6c1-232">Dla kontrolera 0 i kontrolera 1, dołącz **Controller0** i **kontroler1** na końcu hello hello numeru seryjnego (nazwa Pospolita).</span><span class="sxs-lookup"><span data-stu-id="6b6c1-232">For Controller 0 and Controller 1, append **Controller0** and **Controller1** at hello end of hello serial number (CN name).</span></span>
   
    ![Dodawanie pliku toohosts nazwa Pospolita](./media/storsimple-remote-connect/HCS_AddingCNNameToHostsFile.png)
4. <span data-ttu-id="6b6c1-234">Plik hosts hello Zapisz.</span><span class="sxs-lookup"><span data-stu-id="6b6c1-234">Save hello hosts file.</span></span>

### <a name="connect-toohello-device-from-hello-remote-host"></a><span data-ttu-id="6b6c1-235">Podłącz urządzenie toohello z hostem zdalnym hello</span><span class="sxs-lookup"><span data-stu-id="6b6c1-235">Connect toohello device from hello remote host</span></span>

<span data-ttu-id="6b6c1-236">Użyj programu Windows PowerShell i protokołu SSL tooenter jako SSAdmin sesję na swoim urządzeniu, z hosta zdalnego lub klienta.</span><span class="sxs-lookup"><span data-stu-id="6b6c1-236">Use Windows PowerShell and SSL tooenter an SSAdmin session on your device from a remote host or client.</span></span> <span data-ttu-id="6b6c1-237">Sesja SSAdmin Hello mapuje toooption 1 w hello [konsoli szeregowej](storsimple-8000-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console) menu urządzenia.</span><span class="sxs-lookup"><span data-stu-id="6b6c1-237">hello SSAdmin session maps toooption 1 in hello [serial console](storsimple-8000-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console) menu of your device.</span></span>

<span data-ttu-id="6b6c1-238">Wykonaj następujące procedury na komputerze hello, z którego mają połączenia zdalnego programu Windows PowerShell hello toomake hello.</span><span class="sxs-lookup"><span data-stu-id="6b6c1-238">Perform hello following procedure on hello computer from which you want toomake hello remote Windows PowerShell connection.</span></span>

#### <a name="tooenter-an-ssadmin-session-on-hello-device-by-using-windows-powershell-and-ssl"></a><span data-ttu-id="6b6c1-239">tooenter jako SSAdmin sesji na urządzeniu hello za pomocą środowiska Windows PowerShell i SSL</span><span class="sxs-lookup"><span data-stu-id="6b6c1-239">tooenter an SSAdmin session on hello device by using Windows PowerShell and SSL</span></span>
1. <span data-ttu-id="6b6c1-240">Uruchom sesję programu Windows PowerShell jako administrator.</span><span class="sxs-lookup"><span data-stu-id="6b6c1-240">Start a Windows PowerShell session as an administrator.</span></span>
2. <span data-ttu-id="6b6c1-241">Dodaj hello urządzenia IP address toohello klienta zaufanych hostów, wpisując:</span><span class="sxs-lookup"><span data-stu-id="6b6c1-241">Add hello device IP address toohello client’s trusted hosts by typing:</span></span>
   
     `Set-Item wsman:\localhost\Client\TrustedHosts <device_ip> -Concatenate -Force`
   
    <span data-ttu-id="6b6c1-242">Gdzie <*device_ip*> hello adres IP urządzenia, na przykład:</span><span class="sxs-lookup"><span data-stu-id="6b6c1-242">Where <*device_ip*> is hello IP address of your device; for example:</span></span> 
   
     `Set-Item wsman:\localhost\Client\TrustedHosts 10.126.173.90 -Concatenate -Force`
3. <span data-ttu-id="6b6c1-243">toocreate nowe poświadczenie, wpisz:</span><span class="sxs-lookup"><span data-stu-id="6b6c1-243">toocreate a new credential, type:</span></span>
   
     `$cred = New-Object pscredential @("<IP of target device>\SSAdmin", (ConvertTo-SecureString -Force -AsPlainText "<Device Administrator Password>"))`
   
    <span data-ttu-id="6b6c1-244">Gdzie <*IP urządzenie docelowe*> jest adresem IP hello dane 0 dla urządzenia; na przykład **10.126.173.90** pokazane na powitania poprzedzających obrazu pliku hosts hello.</span><span class="sxs-lookup"><span data-stu-id="6b6c1-244">Where <*IP of target device*> is hello IP address of DATA 0 for your device; for example, **10.126.173.90** as shown in hello preceding image of hello hosts file.</span></span> <span data-ttu-id="6b6c1-245">Ponadto podaj hello hasło administratora urządzenia.</span><span class="sxs-lookup"><span data-stu-id="6b6c1-245">Also, supply hello administrator password for your device.</span></span>
4. <span data-ttu-id="6b6c1-246">Utwórz sesję, wpisując:</span><span class="sxs-lookup"><span data-stu-id="6b6c1-246">Create a session by typing:</span></span>
   
     `$session = New-PSSession -UseSSL -ComputerName <Serial number of target device> -Credential $cred -ConfigurationName "SSAdminConsole"`
   
    <span data-ttu-id="6b6c1-247">Dla parametru - ComputerName hello w poleceniu cmdlet hello, podaj hello <*numer seryjny urządzenia docelowego*>.</span><span class="sxs-lookup"><span data-stu-id="6b6c1-247">For hello -ComputerName parameter in hello cmdlet, provide hello <*serial number of target device*>.</span></span> <span data-ttu-id="6b6c1-248">Ten numer seryjny został zamapowany toohello adres IP interfejsu dane 0 w pliku hosts hello na zdalnym hoście; na przykład **SHX0991003G44MT** pokazane na powitania po obrazu.</span><span class="sxs-lookup"><span data-stu-id="6b6c1-248">This serial number was mapped toohello IP address of DATA 0 in hello hosts file on your remote host; for example, **SHX0991003G44MT** as shown in hello following image.</span></span>
5. <span data-ttu-id="6b6c1-249">Wpisz:</span><span class="sxs-lookup"><span data-stu-id="6b6c1-249">Type:</span></span>
   
     `Enter-PSSession $session`
6. <span data-ttu-id="6b6c1-250">Należy toowait za kilka minut, a następnie będzie tooyour podłączonego urządzenia za pośrednictwem protokołu HTTPS przy użyciu protokołu SSL.</span><span class="sxs-lookup"><span data-stu-id="6b6c1-250">You will need toowait a few minutes, and then you will be connected tooyour device via HTTPS over SSL.</span></span> <span data-ttu-id="6b6c1-251">Zostanie wyświetlony komunikat, który wskazuje, że jesteś tooyour podłączonego urządzenia.</span><span class="sxs-lookup"><span data-stu-id="6b6c1-251">You see a message that indicates you are connected tooyour device.</span></span>
   
    ![Usługi zdalne środowiska PowerShell przy użyciu protokołu HTTPS i SSL](./media/storsimple-remote-connect/HCS_PSRemotingUsingHTTPSAndSSL.png)

## <a name="next-steps"></a><span data-ttu-id="6b6c1-253">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="6b6c1-253">Next steps</span></span>

* <span data-ttu-id="6b6c1-254">Dowiedz się więcej o [przy użyciu programu Windows PowerShell tooadminister urządzenia StorSimple](storsimple-8000-windows-powershell-administration.md).</span><span class="sxs-lookup"><span data-stu-id="6b6c1-254">Learn more about [using Windows PowerShell tooadminister your StorSimple device](storsimple-8000-windows-powershell-administration.md).</span></span>
* <span data-ttu-id="6b6c1-255">Dowiedz się więcej o [tooadminister usługi Menedżer StorSimple urządzenia przy użyciu hello urządzenia StorSimple](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="6b6c1-255">Learn more about [using hello StorSimple Device Manager service tooadminister your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

