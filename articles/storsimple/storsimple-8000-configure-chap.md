---
title: "aaaConfigure protokołu CHAP dla urządzenia z serii StorSimple 8000 | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak tooconfigure hello protokół uwierzytelniania typu Challenge Handshake (CHAP) na urządzeniu StorSimple."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: TBD
ms.date: 07/03/2017
ms.author: alkohli
ms.openlocfilehash: 3351184b0317da7e3deae398bc0d63c3e5bd930f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-chap-for-your-storsimple-device"></a><span data-ttu-id="12c90-103">Konfigurowanie protokołu CHAP dla urządzenia StorSimple</span><span class="sxs-lookup"><span data-stu-id="12c90-103">Configure CHAP for your StorSimple device</span></span>

<span data-ttu-id="12c90-104">W tym samouczku wyjaśniono, jak tooconfigure protokołu CHAP dla urządzenia StorSimple.</span><span class="sxs-lookup"><span data-stu-id="12c90-104">This tutorial explains how tooconfigure CHAP for your StorSimple device.</span></span> <span data-ttu-id="12c90-105">Procedura Hello szczegółowo opisane w tym artykule dotyczy urządzeń z serii 8000 tooStorSimple.</span><span class="sxs-lookup"><span data-stu-id="12c90-105">hello procedure detailed in this article applies tooStorSimple 8000 series devices.</span></span>

<span data-ttu-id="12c90-106">Protokół uwierzytelniania typu Challenge Handshake oznacza protokołu CHAP.</span><span class="sxs-lookup"><span data-stu-id="12c90-106">CHAP stands for Challenge Handshake Authentication Protocol.</span></span> <span data-ttu-id="12c90-107">Jest schemat uwierzytelniania używany przez serwery toovalidate hello tożsamości klientów zdalnych.</span><span class="sxs-lookup"><span data-stu-id="12c90-107">It is an authentication scheme used by servers toovalidate hello identity of remote clients.</span></span> <span data-ttu-id="12c90-108">Weryfikacja Hello jest oparta na wspólne hasło lub klucz tajny.</span><span class="sxs-lookup"><span data-stu-id="12c90-108">hello verification is based on a shared password or secret.</span></span> <span data-ttu-id="12c90-109">Protokół CHAP, może być jedną z metod (jednokierunkowe) lub wzajemne (dwukierunkowe).</span><span class="sxs-lookup"><span data-stu-id="12c90-109">CHAP can be one way (unidirectional) or mutual (bidirectional).</span></span> <span data-ttu-id="12c90-110">Jednym ze sposobów jest CHAP podczas hello docelowy uwierzytelniania inicjatora.</span><span class="sxs-lookup"><span data-stu-id="12c90-110">One way CHAP is when hello target authenticates an initiator.</span></span> <span data-ttu-id="12c90-111">W wzajemnego lub wstecznego protokołu CHAP, docelowy hello umożliwiają uwierzytelnienie inicjatora hello a następnie inicjatora hello hello docelowej.</span><span class="sxs-lookup"><span data-stu-id="12c90-111">In mutual or reverse CHAP, hello target authenticates hello initiator and then hello initiator authenticates hello target.</span></span> <span data-ttu-id="12c90-112">Inicjator może być realizowane bez uwierzytelnienia docelowego.</span><span class="sxs-lookup"><span data-stu-id="12c90-112">Initiator authentication can be implemented without target authentication.</span></span> <span data-ttu-id="12c90-113">Jednak docelowym może być realizowane tylko wtedy, gdy uwierzytelnianie inicjatora również jest zaimplementowana.</span><span class="sxs-lookup"><span data-stu-id="12c90-113">However, target authentication can be implemented only if initiator authentication is also implemented.</span></span>

<span data-ttu-id="12c90-114">Najlepszym rozwiązaniem zaleca się użycie zabezpieczeń iSCSI tooenhance protokołu CHAP.</span><span class="sxs-lookup"><span data-stu-id="12c90-114">As a best practice, we recommend that you use CHAP tooenhance iSCSI security.</span></span>

> [!NOTE]
> <span data-ttu-id="12c90-115">Należy pamiętać, że protokół IPSEC nie jest obecnie obsługiwane urządzenia StorSimple.</span><span class="sxs-lookup"><span data-stu-id="12c90-115">Keep in mind that IPSEC is not currently supported on StorSimple devices.</span></span>

<span data-ttu-id="12c90-116">można skonfigurować ustawienia protokołu CHAP Hello na urządzeniu StorSimple hello w hello następujące sposoby:</span><span class="sxs-lookup"><span data-stu-id="12c90-116">hello CHAP settings on hello StorSimple device can be configured in hello following ways:</span></span>

* <span data-ttu-id="12c90-117">Uwierzytelnianie jednokierunkowe lub jednokierunkowe</span><span class="sxs-lookup"><span data-stu-id="12c90-117">Unidirectional or one-way authentication</span></span>
* <span data-ttu-id="12c90-118">Dwukierunkowy lub uwierzytelniania wzajemnego lub wstecznego</span><span class="sxs-lookup"><span data-stu-id="12c90-118">Bidirectional or mutual or reverse authentication</span></span>

<span data-ttu-id="12c90-119">W każdym z tych przypadków portal hello hello urządzeń i oprogramowania inicjatora iSCSI serwera hello musi toobe skonfigurowany.</span><span class="sxs-lookup"><span data-stu-id="12c90-119">In each of these cases, hello portal for hello device and hello server iSCSI initiator software needs toobe configured.</span></span> <span data-ttu-id="12c90-120">Witaj szczegółowe informacje na temat tej konfiguracji zostały opisane w hello samouczka.</span><span class="sxs-lookup"><span data-stu-id="12c90-120">hello detailed steps for this configuration are described in hello following tutorial.</span></span>

## <a name="unidirectional-or-one-way-authentication"></a><span data-ttu-id="12c90-121">Uwierzytelnianie jednokierunkowe lub jednokierunkowe</span><span class="sxs-lookup"><span data-stu-id="12c90-121">Unidirectional or one-way authentication</span></span>

<span data-ttu-id="12c90-122">W jednokierunkowe uwierzytelniania docelowy hello uwierzytelnia hello inicjatora.</span><span class="sxs-lookup"><span data-stu-id="12c90-122">In unidirectional authentication, hello target authenticates hello initiator.</span></span> <span data-ttu-id="12c90-123">To uwierzytelnianie wymaga skonfigurowania ustawień inicjatora protokołu CHAP hello na powitania urządzenia StorSimple i hello oprogramowaniem iSCSI Initiator na hoście hello.</span><span class="sxs-lookup"><span data-stu-id="12c90-123">This authentication requires that you configure hello CHAP initiator settings on hello StorSimple device and hello iSCSI Initiator software on hello host.</span></span> <span data-ttu-id="12c90-124">Witaj szczegółowe procedury dotyczące urządzenia StorSimple i hosta systemu Windows są opisane w dalszej części.</span><span class="sxs-lookup"><span data-stu-id="12c90-124">hello detailed procedures for your StorSimple device and Windows host are described next.</span></span>

#### <a name="tooconfigure-your-device-for-one-way-authentication"></a><span data-ttu-id="12c90-125">tooconfigure Twojego urządzenia pod kątem uwierzytelniania jednokierunkowe</span><span class="sxs-lookup"><span data-stu-id="12c90-125">tooconfigure your device for one-way authentication</span></span>

1. <span data-ttu-id="12c90-126">W hello portalu Azure Przejdź tooyour usługi Menedżer urządzeń StorSimple.</span><span class="sxs-lookup"><span data-stu-id="12c90-126">In hello Azure portal, go tooyour StorSimple Device Manager service.</span></span> <span data-ttu-id="12c90-127">Kliknij przycisk **urządzeń** i wybierz i kliknij urządzenie ma tooconfigure protokołu CHAP dla.</span><span class="sxs-lookup"><span data-stu-id="12c90-127">Click **Devices** and select and click a device you wish tooconfigure CHAP for.</span></span> <span data-ttu-id="12c90-128">Przejdź za**ustawienia urządzenia > zabezpieczeń**.</span><span class="sxs-lookup"><span data-stu-id="12c90-128">Go too**Device settings > Security**.</span></span> <span data-ttu-id="12c90-129">W hello **ustawienia zabezpieczeń** bloku, kliknij przycisk **protokołu CHAP**.</span><span class="sxs-lookup"><span data-stu-id="12c90-129">In hello **Security settings** blade, click **CHAP**.</span></span>
   
    ![Inicjatora protokołu CHAP](./media/storsimple-8000-configure-chap/configure-chap5.png)
2. <span data-ttu-id="12c90-131">W hello **protokołu CHAP** bloku w hello **inicjatora protokołu CHAP** sekcji:</span><span class="sxs-lookup"><span data-stu-id="12c90-131">In hello **CHAP** blade, and in hello **CHAP Initiator** section:</span></span>
   
   1. <span data-ttu-id="12c90-132">Podaj nazwę użytkownika dla użytkownika inicjatora protokołu CHAP.</span><span class="sxs-lookup"><span data-stu-id="12c90-132">Provide a user name for your CHAP initiator.</span></span>
   2. <span data-ttu-id="12c90-133">Podaj hasło dla użytkownika inicjatora protokołu CHAP.</span><span class="sxs-lookup"><span data-stu-id="12c90-133">Supply a password for your CHAP initiator.</span></span>
      
    > [!IMPORTANT]
    > <span data-ttu-id="12c90-134">Nazwa użytkownika protokołu CHAP Hello musi zawierać mniej niż 233 znaków.</span><span class="sxs-lookup"><span data-stu-id="12c90-134">hello CHAP user name must contain fewer than 233 characters.</span></span> <span data-ttu-id="12c90-135">Hasło protokołu CHAP Hello musi należeć do zakresu od 12 do 16 znaków.</span><span class="sxs-lookup"><span data-stu-id="12c90-135">hello CHAP password must be between 12 and 16 characters.</span></span> <span data-ttu-id="12c90-136">Dłużej nazwa użytkownika lub hasło powoduje niepowodzenie uwierzytelniania na hoście Windows hello.</span><span class="sxs-lookup"><span data-stu-id="12c90-136">A longer user name or password results in an authentication failure on hello Windows host.</span></span>
   
   3. <span data-ttu-id="12c90-137">Potwierdź hasło hello.</span><span class="sxs-lookup"><span data-stu-id="12c90-137">Confirm hello password.</span></span>

       ![Inicjatora protokołu CHAP](./media/storsimple-8000-configure-chap/configure-chap6.png)
3. <span data-ttu-id="12c90-139">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="12c90-139">Click **Save**.</span></span> <span data-ttu-id="12c90-140">Zostanie wyświetlony komunikat potwierdzenia.</span><span class="sxs-lookup"><span data-stu-id="12c90-140">A confirmation message is displayed.</span></span> <span data-ttu-id="12c90-141">Kliknij przycisk **OK** toosave hello zmiany.</span><span class="sxs-lookup"><span data-stu-id="12c90-141">Click **OK** toosave hello changes.</span></span>

#### <a name="tooconfigure-one-way-authentication-on-hello-windows-host-server"></a><span data-ttu-id="12c90-142">tooconfigure jednokierunkowe uwierzytelniania w systemie Windows hello serwerze hosta</span><span class="sxs-lookup"><span data-stu-id="12c90-142">tooconfigure one-way authentication on hello Windows host server</span></span>
1. <span data-ttu-id="12c90-143">Na serwerze hosta z systemem Windows hello Uruchom inicjator iSCSI hello.</span><span class="sxs-lookup"><span data-stu-id="12c90-143">On hello Windows host server, start hello iSCSI Initiator.</span></span>
2. <span data-ttu-id="12c90-144">W hello **właściwości inicjatora iSCSI** okna, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="12c90-144">In hello **iSCSI Initiator Properties** window, perform hello following steps:</span></span>
   
   1. <span data-ttu-id="12c90-145">Kliknij przycisk hello **odnajdywania** kartę.</span><span class="sxs-lookup"><span data-stu-id="12c90-145">Click hello **Discovery** tab.</span></span>
      
       ![Właściwości inicjatora iSCSI](./media/storsimple-configure-chap/IC740944.png)
   2. <span data-ttu-id="12c90-147">Kliknij przycisk **odnajdź Portal**.</span><span class="sxs-lookup"><span data-stu-id="12c90-147">Click **Discover Portal**.</span></span>
3. <span data-ttu-id="12c90-148">W hello **odnajdowanie portalu obiektu docelowego** okno dialogowe:</span><span class="sxs-lookup"><span data-stu-id="12c90-148">In hello **Discover Target Portal** dialog box:</span></span>
   
   1. <span data-ttu-id="12c90-149">Określ adres IP hello urządzenia.</span><span class="sxs-lookup"><span data-stu-id="12c90-149">Specify hello IP address of your device.</span></span>
   2. <span data-ttu-id="12c90-150">Kliknij przycisk **zaawansowane**.</span><span class="sxs-lookup"><span data-stu-id="12c90-150">Click **Advanced**.</span></span>
      
       ![Odnajdowanie portalu obiektu docelowego](./media/storsimple-configure-chap/IC740945.png)
4. <span data-ttu-id="12c90-152">W hello **Zaawansowane ustawienia** okno dialogowe:</span><span class="sxs-lookup"><span data-stu-id="12c90-152">In hello **Advanced Settings** dialog box:</span></span>
   
   1. <span data-ttu-id="12c90-153">Wybierz hello **Włącz protokół CHAP logowania** pole wyboru.</span><span class="sxs-lookup"><span data-stu-id="12c90-153">Select hello **Enable CHAP log on** check box.</span></span>
   2. <span data-ttu-id="12c90-154">W hello **nazwa** pole, podaj nazwę użytkownika hello, określona dla hello inicjatora protokołu CHAP w portalu klasycznym hello.</span><span class="sxs-lookup"><span data-stu-id="12c90-154">In hello **Name** field, supply hello user name that you specified for hello CHAP Initiator in hello classic portal.</span></span>
   3. <span data-ttu-id="12c90-155">W hello **klucz tajny obiektu docelowego** pole, podaj hasło hello określony dla hello inicjatora protokołu CHAP w portalu klasycznym hello.</span><span class="sxs-lookup"><span data-stu-id="12c90-155">In hello **Target secret** field, supply hello password that you specified for hello CHAP Initiator in hello classic portal.</span></span>
   4. <span data-ttu-id="12c90-156">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="12c90-156">Click **OK**.</span></span>
      
       ![Zaawansowane ustawienia ogólne](./media/storsimple-configure-chap/IC740946.png)
5. <span data-ttu-id="12c90-158">Na powitania **celów** kartę hello **właściwości inicjatora iSCSI** okna, stan urządzenia hello powinny się wyświetlać jako **połączony**.</span><span class="sxs-lookup"><span data-stu-id="12c90-158">On hello **Targets** tab of hello **iSCSI Initiator Properties** window, hello device status should appear as **Connected**.</span></span> <span data-ttu-id="12c90-159">Jeśli używasz urządzenia StorSimple 1200 każdy wolumin jest zainstalowany jako obiektu docelowego iSCSI.</span><span class="sxs-lookup"><span data-stu-id="12c90-159">If you are using a StorSimple 1200 device, then each volume is mounted as an iSCSI target.</span></span> <span data-ttu-id="12c90-160">W związku z tym kroki 3 i 4 należy powtórzyć dla każdego woluminu toobe.</span><span class="sxs-lookup"><span data-stu-id="12c90-160">Hence, steps 3-4 will need toobe repeated for each volume.</span></span>
   
    ![Woluminów zainstalowanych jako osobne cele](./media/storsimple-configure-chap/chap4.png)
   
   > [!IMPORTANT]
   > <span data-ttu-id="12c90-162">Jeśli zmienisz nazwę iSCSI hello hello Nowa nazwa służy do nowej sesji iSCSI.</span><span class="sxs-lookup"><span data-stu-id="12c90-162">If you change hello iSCSI name, hello new name is used for new iSCSI sessions.</span></span> <span data-ttu-id="12c90-163">Nowe ustawienia nie są ponownie używane istniejące sesje aż do wylogowywania i logowania.</span><span class="sxs-lookup"><span data-stu-id="12c90-163">New settings are not used for existing sessions until you log off and log on again.</span></span>

<span data-ttu-id="12c90-164">Aby uzyskać więcej informacji o konfigurowaniu protokołu CHAP na serwerze hosta z systemem Windows hello Przejdź zbyt[uwagi dodatkowe](#additional-considerations).</span><span class="sxs-lookup"><span data-stu-id="12c90-164">For more information about configuring CHAP on hello Windows host server, go too[Additional considerations](#additional-considerations).</span></span>

## <a name="bidirectional-or-mutual-authentication"></a><span data-ttu-id="12c90-165">Dwukierunkowy lub wzajemnego uwierzytelniania</span><span class="sxs-lookup"><span data-stu-id="12c90-165">Bidirectional or mutual authentication</span></span>

<span data-ttu-id="12c90-166">W uwierzytelnianiu dwukierunkowego docelowy hello umożliwiają uwierzytelnienie inicjatora hello a następnie inicjatora hello hello docelowej.</span><span class="sxs-lookup"><span data-stu-id="12c90-166">In bidirectional authentication, hello target authenticates hello initiator and then hello initiator authenticates hello target.</span></span> <span data-ttu-id="12c90-167">Ta procedura wymaga ustawień inicjatora protokołu CHAP tooconfigure hello hello użytkownika, będą CHAP ustawień na urządzeniach hello i oprogramowaniem iSCSI Initiator na hoście hello.</span><span class="sxs-lookup"><span data-stu-id="12c90-167">This procedure requires hello user tooconfigure hello CHAP initiator settings, reverse CHAP settings on hello device, and iSCSI Initiator software on hello host.</span></span> <span data-ttu-id="12c90-168">Witaj poniższe procedury opisują hello kroki tooconfigure wzajemnego uwierzytelniania na powitania urządzeniu i na hoście Windows hello.</span><span class="sxs-lookup"><span data-stu-id="12c90-168">hello following procedures describe hello steps tooconfigure mutual authentication on hello device and on hello Windows host.</span></span>

#### <a name="tooconfigure-your-device-for-mutual-authentication"></a><span data-ttu-id="12c90-169">tooconfigure Twojego urządzenia pod kątem wzajemnego uwierzytelniania</span><span class="sxs-lookup"><span data-stu-id="12c90-169">tooconfigure your device for mutual authentication</span></span>

1. <span data-ttu-id="12c90-170">W hello portalu Azure Przejdź tooyour usługi Menedżer urządzeń StorSimple.</span><span class="sxs-lookup"><span data-stu-id="12c90-170">In hello Azure portal, go tooyour StorSimple Device Manager service.</span></span> <span data-ttu-id="12c90-171">Kliknij przycisk **urządzeń** i wybierz i kliknij urządzenie ma tooconfigure protokołu CHAP dla.</span><span class="sxs-lookup"><span data-stu-id="12c90-171">Click **Devices** and select and click a device you wish tooconfigure CHAP for.</span></span> <span data-ttu-id="12c90-172">Przejdź za**ustawienia urządzenia > zabezpieczeń**.</span><span class="sxs-lookup"><span data-stu-id="12c90-172">Go too**Device settings > Security**.</span></span> <span data-ttu-id="12c90-173">W hello **ustawienia zabezpieczeń** bloku, kliknij przycisk **protokołu CHAP**.</span><span class="sxs-lookup"><span data-stu-id="12c90-173">In hello **Security settings** blade, click **CHAP**.</span></span>
   
    ![Obiektu docelowego protokołu CHAP](./media/storsimple-8000-configure-chap/configure-chap5.png)
2. <span data-ttu-id="12c90-175">Przewiń w dół na tej stronie, a w hello **docelowego protokołu CHAP** sekcji:</span><span class="sxs-lookup"><span data-stu-id="12c90-175">Scroll down on this page, and in hello **CHAP Target** section:</span></span>
   
   1. <span data-ttu-id="12c90-176">Podaj **nazwy użytkownika** dla danego urządzenia.</span><span class="sxs-lookup"><span data-stu-id="12c90-176">Provide a **Reverse CHAP user name** for your device.</span></span>
   2. <span data-ttu-id="12c90-177">Podaj **wstecznego protokołu CHAP hasła** dla danego urządzenia.</span><span class="sxs-lookup"><span data-stu-id="12c90-177">Supply a **Reverse CHAP password** for your device.</span></span>
   3. <span data-ttu-id="12c90-178">Potwierdź hasło hello.</span><span class="sxs-lookup"><span data-stu-id="12c90-178">Confirm hello password.</span></span>
3. <span data-ttu-id="12c90-179">W hello **inicjatora protokołu CHAP** sekcji:</span><span class="sxs-lookup"><span data-stu-id="12c90-179">In hello **CHAP Initiator** section:</span></span>
   
   1. <span data-ttu-id="12c90-180">Podaj **nazwy użytkownika** dla danego urządzenia.</span><span class="sxs-lookup"><span data-stu-id="12c90-180">Provide a **user name** for your device.</span></span>
   2. <span data-ttu-id="12c90-181">Podaj **hasło** dla danego urządzenia.</span><span class="sxs-lookup"><span data-stu-id="12c90-181">Provide a **password** for your device.</span></span>
   3. <span data-ttu-id="12c90-182">Potwierdź hasło hello.</span><span class="sxs-lookup"><span data-stu-id="12c90-182">Confirm hello password.</span></span>

       ![Inicjatora protokołu CHAP](./media/storsimple-8000-configure-chap/configure-chap11.png)
4. <span data-ttu-id="12c90-184">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="12c90-184">Click **Save**.</span></span> <span data-ttu-id="12c90-185">Zostanie wyświetlony komunikat potwierdzenia.</span><span class="sxs-lookup"><span data-stu-id="12c90-185">A confirmation message is displayed.</span></span> <span data-ttu-id="12c90-186">Kliknij przycisk **OK** toosave hello zmiany.</span><span class="sxs-lookup"><span data-stu-id="12c90-186">Click **OK** toosave hello changes.</span></span>

#### <a name="tooconfigure-bidirectional-authentication-on-hello-windows-host-server"></a><span data-ttu-id="12c90-187">tooconfigure dwukierunkowego uwierzytelniania w systemie Windows hello serwerze hosta</span><span class="sxs-lookup"><span data-stu-id="12c90-187">tooconfigure bidirectional authentication on hello Windows host server</span></span>

1. <span data-ttu-id="12c90-188">Na serwerze hosta z systemem Windows hello Uruchom inicjator iSCSI hello.</span><span class="sxs-lookup"><span data-stu-id="12c90-188">On hello Windows host server, start hello iSCSI Initiator.</span></span>
2. <span data-ttu-id="12c90-189">W hello **właściwości inicjatora iSCSI** okna, kliknij przycisk hello **konfiguracji** kartę.</span><span class="sxs-lookup"><span data-stu-id="12c90-189">In hello **iSCSI Initiator Properties** window, click hello **Configuration** tab.</span></span>
3. <span data-ttu-id="12c90-190">Kliknij przycisk **protokołu CHAP**.</span><span class="sxs-lookup"><span data-stu-id="12c90-190">Click **CHAP**.</span></span>
4. <span data-ttu-id="12c90-191">W hello **wzajemnego protokołu CHAP klucz tajny inicjatora iSCSI** okno dialogowe:</span><span class="sxs-lookup"><span data-stu-id="12c90-191">In hello **iSCSI Initiator Mutual CHAP Secret** dialog box:</span></span>
   
   1. <span data-ttu-id="12c90-192">Typ hello **wstecznego protokołu CHAP hasła** skonfigurowanego w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="12c90-192">Type hello **Reverse CHAP Password** that you configured in hello Azure portal.</span></span>
   2. <span data-ttu-id="12c90-193">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="12c90-193">Click **OK**.</span></span>
      
       ![wzajemne tajny protokołu CHAP inicjatora iSCSI](./media/storsimple-configure-chap/IC740949.png)
5. <span data-ttu-id="12c90-195">Kliknij przycisk hello **cele** kartę.</span><span class="sxs-lookup"><span data-stu-id="12c90-195">Click hello **Targets** tab.</span></span>
6. <span data-ttu-id="12c90-196">Kliknij przycisk hello **Connect** przycisku.</span><span class="sxs-lookup"><span data-stu-id="12c90-196">Click hello **Connect** button.</span></span> 
7. <span data-ttu-id="12c90-197">W hello **połączyć tooTarget** okno dialogowe, kliknij przycisk **zaawansowane**.</span><span class="sxs-lookup"><span data-stu-id="12c90-197">In hello **Connect tooTarget** dialog box, click **Advanced**.</span></span>
8. <span data-ttu-id="12c90-198">W hello **właściwości zaawansowane** okno dialogowe:</span><span class="sxs-lookup"><span data-stu-id="12c90-198">In hello **Advanced Properties** dialog box:</span></span>
   
   1. <span data-ttu-id="12c90-199">Wybierz hello **Włącz protokół CHAP logowania** pole wyboru.</span><span class="sxs-lookup"><span data-stu-id="12c90-199">Select hello **Enable CHAP log on** check box.</span></span>
   2. <span data-ttu-id="12c90-200">W hello **nazwa** pole, podaj nazwę użytkownika hello, określona dla hello inicjatora protokołu CHAP w portalu klasycznym hello.</span><span class="sxs-lookup"><span data-stu-id="12c90-200">In hello **Name** field, supply hello user name that you specified for hello CHAP Initiator in hello classic portal.</span></span>
   3. <span data-ttu-id="12c90-201">W hello **klucz tajny obiektu docelowego** pole, podaj hasło hello określony dla hello inicjatora protokołu CHAP w portalu klasycznym hello.</span><span class="sxs-lookup"><span data-stu-id="12c90-201">In hello **Target secret** field, supply hello password that you specified for hello CHAP Initiator in hello classic portal.</span></span>
   4. <span data-ttu-id="12c90-202">Wybierz hello **wykonaj wzajemnego uwierzytelniania** pole wyboru.</span><span class="sxs-lookup"><span data-stu-id="12c90-202">Select hello **Perform mutual authentication** check box.</span></span>
      
       ![Ustawienia zaawansowane wzajemnego uwierzytelniania.](./media/storsimple-configure-chap/IC740950.png)
   5. <span data-ttu-id="12c90-204">Kliknij przycisk **OK** toocomplete hello CHAP konfiguracji</span><span class="sxs-lookup"><span data-stu-id="12c90-204">Click **OK** toocomplete hello CHAP configuration</span></span>

<span data-ttu-id="12c90-205">Aby uzyskać więcej informacji o konfigurowaniu protokołu CHAP na serwerze hosta z systemem Windows hello Przejdź zbyt[uwagi dodatkowe](#additional-considerations).</span><span class="sxs-lookup"><span data-stu-id="12c90-205">For more information about configuring CHAP on hello Windows host server, go too[Additional considerations](#additional-considerations).</span></span>

## <a name="additional-considerations"></a><span data-ttu-id="12c90-206">Dodatkowe zagadnienia</span><span class="sxs-lookup"><span data-stu-id="12c90-206">Additional considerations</span></span>

<span data-ttu-id="12c90-207">Witaj **szybkie połączenie** funkcja nie obsługuje połączeń, które mają włączony protokół CHAP.</span><span class="sxs-lookup"><span data-stu-id="12c90-207">hello **Quick Connect** feature does not support connections that have CHAP enabled.</span></span> <span data-ttu-id="12c90-208">Po włączeniu protokołu CHAP, upewnij się, że używasz hello **Connect** przycisku, który jest dostępny na powitania **cele** kartę tooconnect tooa docelowej.</span><span class="sxs-lookup"><span data-stu-id="12c90-208">When CHAP is enabled, make sure that you use hello **Connect** button that is available on hello **Targets** tab tooconnect tooa target.</span></span>

![Połącz tootarget](./media/storsimple-configure-chap/IC740947.png)

<span data-ttu-id="12c90-210">W hello **połączyć tooTarget** dialogowe hello przedstawioną, wybierz pozycję **Dodawanie połączenia tej toohello lista ulubionych elementów docelowych** pole wyboru.</span><span class="sxs-lookup"><span data-stu-id="12c90-210">In hello **Connect tooTarget** dialog box that is presented, select hello **Add this connection toohello list of Favorite Targets** check box.</span></span> <span data-ttu-id="12c90-211">Wybranie tej opcji gwarantuje, że przy każdym uruchomieniu komputera hello podejmowana jest próba toorestore hello połączenia toohello ulubionych obiektów docelowych iSCSI.</span><span class="sxs-lookup"><span data-stu-id="12c90-211">This selection ensures that every time hello computer restarts, an attempt is made toorestore hello connection toohello iSCSI favorite targets.</span></span>

## <a name="errors-during-configuration"></a><span data-ttu-id="12c90-212">Błędy podczas konfiguracji</span><span class="sxs-lookup"><span data-stu-id="12c90-212">Errors during configuration</span></span>

<span data-ttu-id="12c90-213">Jeśli konfiguracja protokołu CHAP jest niepoprawny, a następnie są prawdopodobnie toosee **niepowodzenie uwierzytelniania** komunikat o błędzie.</span><span class="sxs-lookup"><span data-stu-id="12c90-213">If your CHAP configuration is incorrect, then you are likely toosee an **Authentication failure** error message.</span></span>

## <a name="verification-of-chap-configuration"></a><span data-ttu-id="12c90-214">Weryfikacja konfiguracji protokołu CHAP</span><span class="sxs-lookup"><span data-stu-id="12c90-214">Verification of CHAP configuration</span></span>

<span data-ttu-id="12c90-215">Aby sprawdzić, czy, wykonując następujące kroki hello jest używany protokół CHAP.</span><span class="sxs-lookup"><span data-stu-id="12c90-215">You can verify that CHAP is being used by completing hello following steps.</span></span>

#### <a name="tooverify-your-chap-configuration"></a><span data-ttu-id="12c90-216">tooverify konfiguracji protokołu CHAP</span><span class="sxs-lookup"><span data-stu-id="12c90-216">tooverify your CHAP configuration</span></span>
1. <span data-ttu-id="12c90-217">Kliknij przycisk **Ulubione obiekty docelowe**.</span><span class="sxs-lookup"><span data-stu-id="12c90-217">Click **Favorite Targets**.</span></span>
2. <span data-ttu-id="12c90-218">Wybierz cel hello, dla której jest włączone uwierzytelnianie.</span><span class="sxs-lookup"><span data-stu-id="12c90-218">Select hello target for which you enabled authentication.</span></span>
3. <span data-ttu-id="12c90-219">Kliknij przycisk **szczegóły**.</span><span class="sxs-lookup"><span data-stu-id="12c90-219">Click **Details**.</span></span>
   
    ![Inicjator właściwości ulubionych obiektów docelowych iSCSI](./media/storsimple-configure-chap/IC740951.png)
4. <span data-ttu-id="12c90-221">W hello **ulubionych szczegóły docelowej** okno dialogowe, wpisu notatki hello w hello **uwierzytelniania** pola.</span><span class="sxs-lookup"><span data-stu-id="12c90-221">In hello **Favorite Target Details** dialog box, note hello entry in hello **Authentication** field.</span></span> <span data-ttu-id="12c90-222">Jeśli konfiguracja hello zakończyło się pomyślnie, powinien powiedzieć **protokołu CHAP**.</span><span class="sxs-lookup"><span data-stu-id="12c90-222">If hello configuration was successful, it should say **CHAP**.</span></span>
   
    ![Szczegóły ulubiony obiekt docelowy](./media/storsimple-configure-chap/IC740952.png)

## <a name="next-steps"></a><span data-ttu-id="12c90-224">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="12c90-224">Next steps</span></span>

* <span data-ttu-id="12c90-225">Dowiedz się więcej o [zabezpieczenia usługi StorSimple](storsimple-8000-security.md).</span><span class="sxs-lookup"><span data-stu-id="12c90-225">Learn more about [StorSimple security](storsimple-8000-security.md).</span></span>
* <span data-ttu-id="12c90-226">Dowiedz się więcej o [tooadminister usługi Menedżer StorSimple urządzenia przy użyciu hello urządzenia StorSimple](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="12c90-226">Learn more about [using hello StorSimple Device Manager service tooadminister your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

