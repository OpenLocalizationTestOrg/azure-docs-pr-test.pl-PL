---
title: "aaaConfigure protokołu CHAP dla urządzenia z serii StorSimple 8000 | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak tooconfigure hello protokół uwierzytelniania typu Challenge Handshake (CHAP) na urządzeniu StorSimple."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 467044d7-7885-4382-90bd-3148dbbd341f
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: 272ef2c184f56ad262e55410357494c72e45cf83
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-chap-for-your-storsimple-device"></a><span data-ttu-id="f3482-103">Konfigurowanie protokołu CHAP dla urządzenia StorSimple</span><span class="sxs-lookup"><span data-stu-id="f3482-103">Configure CHAP for your StorSimple device</span></span>
<span data-ttu-id="f3482-104">W tym samouczku wyjaśniono, jak tooconfigure protokołu CHAP dla urządzenia StorSimple.</span><span class="sxs-lookup"><span data-stu-id="f3482-104">This tutorial explains how tooconfigure CHAP for your StorSimple device.</span></span> <span data-ttu-id="f3482-105">procedury Hello szczegółowo opisane w tym artykule dotyczą serii 8000 tooStorSimple, a także urządzenia StorSimple 1200.</span><span class="sxs-lookup"><span data-stu-id="f3482-105">hello procedure detailed in this article applies tooStorSimple 8000 series as well as StorSimple 1200 devices.</span></span>

<span data-ttu-id="f3482-106">Protokół uwierzytelniania typu Challenge Handshake oznacza protokołu CHAP.</span><span class="sxs-lookup"><span data-stu-id="f3482-106">CHAP stands for Challenge Handshake Authentication Protocol.</span></span> <span data-ttu-id="f3482-107">Jest schemat uwierzytelniania używany przez serwery toovalidate hello tożsamości klientów zdalnych.</span><span class="sxs-lookup"><span data-stu-id="f3482-107">It is an authentication scheme used by servers toovalidate hello identity of remote clients.</span></span> <span data-ttu-id="f3482-108">Weryfikacja Hello jest oparta na wspólne hasło lub klucz tajny.</span><span class="sxs-lookup"><span data-stu-id="f3482-108">hello verification is based on a shared password or secret.</span></span> <span data-ttu-id="f3482-109">Protokół CHAP, może być jednokierunkowe (jednokierunkowe) lub wzajemne (dwukierunkowe).</span><span class="sxs-lookup"><span data-stu-id="f3482-109">CHAP can be one-way (unidirectional) or mutual (bidirectional).</span></span> <span data-ttu-id="f3482-110">Jednokierunkowe CHAP jest w przypadku docelowej hello uwierzytelnia inicjatora.</span><span class="sxs-lookup"><span data-stu-id="f3482-110">One-way CHAP is when hello target authenticates an initiator.</span></span> <span data-ttu-id="f3482-111">Wzajemne lub wstecznego protokołu CHAP, na powitania drugiej strony, wymaga, aby docelowy hello uwierzytelniania inicjatora hello i następnie inicjatora hello uwierzytelniania hello docelowej.</span><span class="sxs-lookup"><span data-stu-id="f3482-111">Mutual or reverse CHAP, on hello other hand, requires that hello target authenticate hello initiator and then hello initiator authenticate hello target.</span></span> <span data-ttu-id="f3482-112">Inicjator może być realizowane bez uwierzytelnienia docelowego.</span><span class="sxs-lookup"><span data-stu-id="f3482-112">Initiator authentication can be implemented without target authentication.</span></span> <span data-ttu-id="f3482-113">Jednak docelowym może być realizowane tylko wtedy, gdy uwierzytelnianie inicjatora również jest zaimplementowana.</span><span class="sxs-lookup"><span data-stu-id="f3482-113">However, target authentication can be implemented only if initiator authentication is also implemented.</span></span> 

<span data-ttu-id="f3482-114">Najlepszym rozwiązaniem zaleca się użycie zabezpieczeń iSCSI tooenhance protokołu CHAP.</span><span class="sxs-lookup"><span data-stu-id="f3482-114">As a best practice, we recommend that you use CHAP tooenhance iSCSI security.</span></span>

> [!NOTE]
> <span data-ttu-id="f3482-115">Należy pamiętać, że protokół IPSEC nie jest obecnie obsługiwane urządzenia StorSimple.</span><span class="sxs-lookup"><span data-stu-id="f3482-115">Keep in mind that IPSEC is not currently supported on StorSimple devices.</span></span>
> 
> 

<span data-ttu-id="f3482-116">można skonfigurować ustawienia protokołu CHAP Hello na urządzeniu StorSimple hello w hello następujące sposoby:</span><span class="sxs-lookup"><span data-stu-id="f3482-116">hello CHAP settings on hello StorSimple device can be configured in hello following ways:</span></span>

* <span data-ttu-id="f3482-117">Uwierzytelnianie jednokierunkowe lub jednokierunkowe</span><span class="sxs-lookup"><span data-stu-id="f3482-117">Unidirectional or one-way authentication</span></span>
* <span data-ttu-id="f3482-118">Dwukierunkowy lub uwierzytelniania wzajemnego lub wstecznego</span><span class="sxs-lookup"><span data-stu-id="f3482-118">Bidirectional or mutual or reverse authentication</span></span>

<span data-ttu-id="f3482-119">W każdym z tych przypadków portal hello hello urządzeń i oprogramowania inicjatora iSCSI serwera hello musi toobe skonfigurowany.</span><span class="sxs-lookup"><span data-stu-id="f3482-119">In each of these cases, hello portal for hello device and hello server iSCSI initiator software needs toobe configured.</span></span> <span data-ttu-id="f3482-120">Witaj szczegółowe informacje na temat tej konfiguracji zostały opisane w hello samouczka.</span><span class="sxs-lookup"><span data-stu-id="f3482-120">hello detailed steps for this configuration are described in hello following tutorial.</span></span>

## <a name="unidirectional-or-one-way-authentication"></a><span data-ttu-id="f3482-121">Uwierzytelnianie jednokierunkowe lub jednokierunkowe</span><span class="sxs-lookup"><span data-stu-id="f3482-121">Unidirectional or one-way authentication</span></span>
<span data-ttu-id="f3482-122">W jednokierunkowe uwierzytelniania docelowy hello uwierzytelnia hello inicjatora.</span><span class="sxs-lookup"><span data-stu-id="f3482-122">In unidirectional authentication, hello target authenticates hello initiator.</span></span> <span data-ttu-id="f3482-123">To uwierzytelnianie wymaga skonfigurowania ustawień inicjatora protokołu CHAP hello na powitania urządzenia StorSimple i hello oprogramowaniem iSCSI Initiator na hoście hello.</span><span class="sxs-lookup"><span data-stu-id="f3482-123">This authentication requires that you configure hello CHAP initiator settings on hello StorSimple device and hello iSCSI Initiator software on hello host.</span></span> <span data-ttu-id="f3482-124">Witaj szczegółowe procedury dotyczące urządzenia StorSimple i hosta systemu Windows są opisane w dalszej części.</span><span class="sxs-lookup"><span data-stu-id="f3482-124">hello detailed procedures for your StorSimple device and Windows host are described next.</span></span>

#### <a name="tooconfigure-your-device-for-one-way-authentication"></a><span data-ttu-id="f3482-125">tooconfigure Twojego urządzenia pod kątem uwierzytelniania jednokierunkowe</span><span class="sxs-lookup"><span data-stu-id="f3482-125">tooconfigure your device for one-way authentication</span></span>
1. <span data-ttu-id="f3482-126">W hello klasycznego portalu Azure na powitania **urządzeń** kliknij przycisk hello **Konfiguruj** kartę.</span><span class="sxs-lookup"><span data-stu-id="f3482-126">In hello Azure classic portal, on hello **Devices** page, click hello **Configure** tab.</span></span>
   
    ![Inicjatora protokołu CHAP](./media/storsimple-configure-chap/IC740943.png)
2. <span data-ttu-id="f3482-128">Przewiń w dół na tej stronie, a w hello **inicjatora protokołu CHAP** sekcji:</span><span class="sxs-lookup"><span data-stu-id="f3482-128">Scroll down on this page, and in hello **CHAP Initiator** section:</span></span>
   
   1. <span data-ttu-id="f3482-129">Podaj nazwę użytkownika dla użytkownika inicjatora protokołu CHAP.</span><span class="sxs-lookup"><span data-stu-id="f3482-129">Provide a user name for your CHAP initiator.</span></span>
   2. <span data-ttu-id="f3482-130">Podaj hasło dla użytkownika inicjatora protokołu CHAP.</span><span class="sxs-lookup"><span data-stu-id="f3482-130">Supply a password for your CHAP initiator.</span></span>
      
    > [!IMPORTANT]
    > <span data-ttu-id="f3482-131">Nazwa użytkownika protokołu CHAP Hello musi zawierać mniej niż 233 znaków.</span><span class="sxs-lookup"><span data-stu-id="f3482-131">hello CHAP user name must contain fewer than 233 characters.</span></span> <span data-ttu-id="f3482-132">Hasło protokołu CHAP Hello musi należeć do zakresu od 12 do 16 znaków.</span><span class="sxs-lookup"><span data-stu-id="f3482-132">hello CHAP password must be between 12 and 16 characters.</span></span> <span data-ttu-id="f3482-133">Wystąpił błąd uwierzytelniania na hoście Windows hello spowoduje dłużej nazwa użytkownika lub hasło.</span><span class="sxs-lookup"><span data-stu-id="f3482-133">A longer user name or password will result in an authentication failure on hello Windows host.</span></span>
   
   3. <span data-ttu-id="f3482-134">Potwierdź hasło hello.</span><span class="sxs-lookup"><span data-stu-id="f3482-134">Confirm hello password.</span></span>
3. <span data-ttu-id="f3482-135">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="f3482-135">Click **Save**.</span></span> <span data-ttu-id="f3482-136">Zostanie wyświetlony komunikat potwierdzenia.</span><span class="sxs-lookup"><span data-stu-id="f3482-136">A confirmation message will be displayed.</span></span> <span data-ttu-id="f3482-137">Kliknij przycisk **OK** toosave hello zmiany.</span><span class="sxs-lookup"><span data-stu-id="f3482-137">Click **OK** toosave hello changes.</span></span>

#### <a name="tooconfigure-one-way-authentication-on-hello-windows-host-server"></a><span data-ttu-id="f3482-138">tooconfigure jednokierunkowe uwierzytelniania w systemie Windows hello serwerze hosta</span><span class="sxs-lookup"><span data-stu-id="f3482-138">tooconfigure one-way authentication on hello Windows host server</span></span>
1. <span data-ttu-id="f3482-139">Na serwerze hosta z systemem Windows hello Uruchom inicjator iSCSI hello.</span><span class="sxs-lookup"><span data-stu-id="f3482-139">On hello Windows host server, start hello iSCSI Initiator.</span></span>
2. <span data-ttu-id="f3482-140">W hello **właściwości inicjatora iSCSI** okna, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="f3482-140">In hello **iSCSI Initiator Properties** window, perform hello following steps:</span></span>
   
   1. <span data-ttu-id="f3482-141">Kliknij przycisk hello **odnajdywania** kartę.</span><span class="sxs-lookup"><span data-stu-id="f3482-141">Click hello **Discovery** tab.</span></span>
      
       ![Właściwości inicjatora iSCSI](./media/storsimple-configure-chap/IC740944.png)
   2. <span data-ttu-id="f3482-143">Kliknij przycisk **odnajdź Portal**.</span><span class="sxs-lookup"><span data-stu-id="f3482-143">Click **Discover Portal**.</span></span>
3. <span data-ttu-id="f3482-144">W hello **odnajdowanie portalu obiektu docelowego** okno dialogowe:</span><span class="sxs-lookup"><span data-stu-id="f3482-144">In hello **Discover Target Portal** dialog box:</span></span>
   
   1. <span data-ttu-id="f3482-145">Określ adres IP hello urządzenia.</span><span class="sxs-lookup"><span data-stu-id="f3482-145">Specify hello IP address of your device.</span></span>
   2. <span data-ttu-id="f3482-146">Kliknij przycisk **zaawansowane**.</span><span class="sxs-lookup"><span data-stu-id="f3482-146">Click **Advanced**.</span></span>
      
       ![Odnajdowanie portalu obiektu docelowego](./media/storsimple-configure-chap/IC740945.png)
4. <span data-ttu-id="f3482-148">W hello **Zaawansowane ustawienia** okno dialogowe:</span><span class="sxs-lookup"><span data-stu-id="f3482-148">In hello **Advanced Settings** dialog box:</span></span>
   
   1. <span data-ttu-id="f3482-149">Wybierz hello **Włącz protokół CHAP logowania** pole wyboru.</span><span class="sxs-lookup"><span data-stu-id="f3482-149">Select hello **Enable CHAP log on** check box.</span></span>
   2. <span data-ttu-id="f3482-150">W hello **nazwa** pole, podaj nazwę użytkownika hello, określona dla hello inicjatora protokołu CHAP w portalu klasycznym hello.</span><span class="sxs-lookup"><span data-stu-id="f3482-150">In hello **Name** field, supply hello user name that you specified for hello CHAP Initiator in hello classic portal.</span></span>
   3. <span data-ttu-id="f3482-151">W hello **klucz tajny obiektu docelowego** pole, podaj hasło hello określony dla hello inicjatora protokołu CHAP w portalu klasycznym hello.</span><span class="sxs-lookup"><span data-stu-id="f3482-151">In hello **Target secret** field, supply hello password that you specified for hello CHAP Initiator in hello classic portal.</span></span>
   4. <span data-ttu-id="f3482-152">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="f3482-152">Click **OK**.</span></span>
      
       ![Zaawansowane ustawienia ogólne](./media/storsimple-configure-chap/IC740946.png)
5. <span data-ttu-id="f3482-154">Na powitania **celów** kartę hello **właściwości inicjatora iSCSI** okna, stan urządzenia hello powinny się wyświetlać jako **połączony**.</span><span class="sxs-lookup"><span data-stu-id="f3482-154">On hello **Targets** tab of hello **iSCSI Initiator Properties** window, hello device status should appear as **Connected**.</span></span> <span data-ttu-id="f3482-155">Jeśli używasz urządzenia StorSimple 1200 następnie każdy wolumin zostanie zainstalowany jako obiektu docelowego iSCSI w sposób przedstawiony poniżej.</span><span class="sxs-lookup"><span data-stu-id="f3482-155">If you are using a StorSimple 1200 device, then each volume will be mounted as an iSCSI target as shown below.</span></span> <span data-ttu-id="f3482-156">W związku z tym kroki 3 i 4 należy powtórzyć dla każdego woluminu toobe.</span><span class="sxs-lookup"><span data-stu-id="f3482-156">Hence, steps  3-4 will need toobe repeated for each volume.</span></span>
   
    ![Woluminów zainstalowanych jako osobne cele](./media/storsimple-configure-chap/chap4.png)
   
   > [!IMPORTANT]
   > <span data-ttu-id="f3482-158">Jeśli zmienisz nazwę iSCSI hello hello nową nazwę będzie służyć do nowej sesji iSCSI.</span><span class="sxs-lookup"><span data-stu-id="f3482-158">If you change hello iSCSI name, hello new name will be used for new iSCSI sessions.</span></span> <span data-ttu-id="f3482-159">Nowe ustawienia nie są ponownie używane istniejące sesje aż do wylogowywania i logowania.</span><span class="sxs-lookup"><span data-stu-id="f3482-159">New settings are not used for existing sessions until you log off and log on again.</span></span>
   > 
   > 

<span data-ttu-id="f3482-160">Aby uzyskać więcej informacji o konfigurowaniu protokołu CHAP na serwerze hosta z systemem Windows hello Przejdź zbyt[uwagi dodatkowe](#additional-considerations).</span><span class="sxs-lookup"><span data-stu-id="f3482-160">For more information about configuring CHAP on hello Windows host server, go too[Additional considerations](#additional-considerations).</span></span>

## <a name="bidirectional-or-mutual-authentication"></a><span data-ttu-id="f3482-161">Dwukierunkowy lub wzajemnego uwierzytelniania</span><span class="sxs-lookup"><span data-stu-id="f3482-161">Bidirectional or mutual authentication</span></span>
<span data-ttu-id="f3482-162">W uwierzytelnianiu dwukierunkowego docelowy hello umożliwiają uwierzytelnienie inicjatora hello a następnie inicjatora hello hello docelowej.</span><span class="sxs-lookup"><span data-stu-id="f3482-162">In bidirectional authentication, hello target authenticates hello initiator and then hello initiator authenticates hello target.</span></span> <span data-ttu-id="f3482-163">Wymaga to hello tooconfigure hello CHAP inicjatora ustawień, a także hello odwrócić ustawień protokołu CHAP na powitania urządzeniami i oprogramowaniem iSCSI Initiator na hoście hello.</span><span class="sxs-lookup"><span data-stu-id="f3482-163">This requires hello user tooconfigure hello CHAP initiator settings, as well as hello reverse CHAP settings on hello device and iSCSI Initiator software on hello host.</span></span> <span data-ttu-id="f3482-164">Witaj poniższe procedury opisują hello kroki tooconfigure wzajemnego uwierzytelniania na powitania urządzeniu i na hoście Windows hello.</span><span class="sxs-lookup"><span data-stu-id="f3482-164">hello following procedures describe hello steps tooconfigure mutual authentication on hello device and on hello Windows host.</span></span>

#### <a name="tooconfigure-your-device-for-mutual-authentication"></a><span data-ttu-id="f3482-165">tooconfigure Twojego urządzenia pod kątem wzajemnego uwierzytelniania</span><span class="sxs-lookup"><span data-stu-id="f3482-165">tooconfigure your device for mutual authentication</span></span>
1. <span data-ttu-id="f3482-166">W hello klasycznego portalu Azure na powitania **urządzeń** kliknij przycisk hello **Konfiguruj** kartę.</span><span class="sxs-lookup"><span data-stu-id="f3482-166">In hello Azure classic portal, on hello **Devices** page, click hello **Configure** tab.</span></span>
   
    ![Obiektu docelowego protokołu CHAP](./media/storsimple-configure-chap/IC740948.png)
2. <span data-ttu-id="f3482-168">Przewiń w dół na tej stronie, a w hello **docelowego protokołu CHAP** sekcji:</span><span class="sxs-lookup"><span data-stu-id="f3482-168">Scroll down on this page, and in hello **CHAP Target** section:</span></span>
   
   1. <span data-ttu-id="f3482-169">Podaj **nazwy użytkownika** dla danego urządzenia.</span><span class="sxs-lookup"><span data-stu-id="f3482-169">Provide a **Reverse CHAP user name** for your device.</span></span>
   2. <span data-ttu-id="f3482-170">Podaj **wstecznego protokołu CHAP hasła** dla danego urządzenia.</span><span class="sxs-lookup"><span data-stu-id="f3482-170">Supply a **Reverse CHAP password** for your device.</span></span>
   3. <span data-ttu-id="f3482-171">Potwierdź hasło hello.</span><span class="sxs-lookup"><span data-stu-id="f3482-171">Confirm hello password.</span></span>
3. <span data-ttu-id="f3482-172">W hello **inicjatora protokołu CHAP** sekcji:</span><span class="sxs-lookup"><span data-stu-id="f3482-172">In hello **CHAP Initiator** section:</span></span>
   
   1. <span data-ttu-id="f3482-173">Podaj **nazwy użytkownika** dla danego urządzenia.</span><span class="sxs-lookup"><span data-stu-id="f3482-173">Provide a **user name** for your device.</span></span>
   2. <span data-ttu-id="f3482-174">Podaj **hasło** dla danego urządzenia.</span><span class="sxs-lookup"><span data-stu-id="f3482-174">Provide a **password** for your device.</span></span>
   3. <span data-ttu-id="f3482-175">Potwierdź hasło hello.</span><span class="sxs-lookup"><span data-stu-id="f3482-175">Confirm hello password.</span></span>
4. <span data-ttu-id="f3482-176">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="f3482-176">Click **Save**.</span></span> <span data-ttu-id="f3482-177">Zostanie wyświetlony komunikat potwierdzenia.</span><span class="sxs-lookup"><span data-stu-id="f3482-177">A confirmation message will be displayed.</span></span> <span data-ttu-id="f3482-178">Kliknij przycisk **OK** toosave hello zmiany.</span><span class="sxs-lookup"><span data-stu-id="f3482-178">Click **OK** toosave hello changes.</span></span>

#### <a name="tooconfigure-bidirectional-authentication-on-hello-windows-host-server"></a><span data-ttu-id="f3482-179">tooconfigure dwukierunkowego uwierzytelniania w systemie Windows hello serwerze hosta</span><span class="sxs-lookup"><span data-stu-id="f3482-179">tooconfigure bidirectional authentication on hello Windows host server</span></span>
1. <span data-ttu-id="f3482-180">Na serwerze hosta z systemem Windows hello Uruchom inicjator iSCSI hello.</span><span class="sxs-lookup"><span data-stu-id="f3482-180">On hello Windows host server, start hello iSCSI Initiator.</span></span>
2. <span data-ttu-id="f3482-181">W hello **właściwości inicjatora iSCSI** okna, kliknij przycisk hello **konfiguracji** kartę.</span><span class="sxs-lookup"><span data-stu-id="f3482-181">In hello **iSCSI Initiator Properties** window, click hello **Configuration** tab.</span></span>
3. <span data-ttu-id="f3482-182">Kliknij przycisk **protokołu CHAP**.</span><span class="sxs-lookup"><span data-stu-id="f3482-182">Click **CHAP**.</span></span>
4. <span data-ttu-id="f3482-183">W hello **wzajemnego protokołu CHAP klucz tajny inicjatora iSCSI** okno dialogowe:</span><span class="sxs-lookup"><span data-stu-id="f3482-183">In hello **iSCSI Initiator Mutual CHAP Secret** dialog box:</span></span>
   
   1. <span data-ttu-id="f3482-184">Typ hello **wstecznego protokołu CHAP hasła** skonfigurowanego w hello klasycznego portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="f3482-184">Type hello **Reverse CHAP Password** that you configured in hello Azure classic portal.</span></span>
   2. <span data-ttu-id="f3482-185">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="f3482-185">Click **OK**.</span></span>
      
       ![wzajemne tajny protokołu CHAP inicjatora iSCSI](./media/storsimple-configure-chap/IC740949.png)
5. <span data-ttu-id="f3482-187">Kliknij przycisk hello **cele** kartę.</span><span class="sxs-lookup"><span data-stu-id="f3482-187">Click hello **Targets** tab.</span></span>
6. <span data-ttu-id="f3482-188">Kliknij przycisk hello **Connect** przycisku.</span><span class="sxs-lookup"><span data-stu-id="f3482-188">Click hello **Connect** button.</span></span> 
7. <span data-ttu-id="f3482-189">W hello **połączyć tooTarget** okno dialogowe, kliknij przycisk **zaawansowane**.</span><span class="sxs-lookup"><span data-stu-id="f3482-189">In hello **Connect tooTarget** dialog box, click **Advanced**.</span></span>
8. <span data-ttu-id="f3482-190">W hello **właściwości zaawansowane** okno dialogowe:</span><span class="sxs-lookup"><span data-stu-id="f3482-190">In hello **Advanced Properties** dialog box:</span></span>
   
   1. <span data-ttu-id="f3482-191">Wybierz hello **Włącz protokół CHAP logowania** pole wyboru.</span><span class="sxs-lookup"><span data-stu-id="f3482-191">Select hello **Enable CHAP log on** check box.</span></span>
   2. <span data-ttu-id="f3482-192">W hello **nazwa** pole, podaj nazwę użytkownika hello, określona dla hello inicjatora protokołu CHAP w portalu klasycznym hello.</span><span class="sxs-lookup"><span data-stu-id="f3482-192">In hello **Name** field, supply hello user name that you specified for hello CHAP Initiator in hello classic portal.</span></span>
   3. <span data-ttu-id="f3482-193">W hello **klucz tajny obiektu docelowego** pole, podaj hasło hello określony dla hello inicjatora protokołu CHAP w portalu klasycznym hello.</span><span class="sxs-lookup"><span data-stu-id="f3482-193">In hello **Target secret** field, supply hello password that you specified for hello CHAP Initiator in hello classic portal.</span></span>
   4. <span data-ttu-id="f3482-194">Wybierz hello **wykonaj wzajemnego uwierzytelniania** pole wyboru.</span><span class="sxs-lookup"><span data-stu-id="f3482-194">Select hello **Perform mutual authentication** check box.</span></span>
      
       ![Ustawienia zaawansowane wzajemnego uwierzytelniania.](./media/storsimple-configure-chap/IC740950.png)
   5. <span data-ttu-id="f3482-196">Kliknij przycisk **OK** toocomplete hello CHAP konfiguracji</span><span class="sxs-lookup"><span data-stu-id="f3482-196">Click **OK** toocomplete hello CHAP configuration</span></span>

<span data-ttu-id="f3482-197">Aby uzyskać więcej informacji o konfigurowaniu protokołu CHAP na serwerze hosta z systemem Windows hello Przejdź zbyt[uwagi dodatkowe](#additional-considerations).</span><span class="sxs-lookup"><span data-stu-id="f3482-197">For more information about configuring CHAP on hello Windows host server, go too[Additional considerations](#additional-considerations).</span></span>

## <a name="additional-considerations"></a><span data-ttu-id="f3482-198">Dodatkowe zagadnienia</span><span class="sxs-lookup"><span data-stu-id="f3482-198">Additional considerations</span></span>
<span data-ttu-id="f3482-199">Witaj **szybkie połączenie** funkcja nie obsługuje połączeń, które mają włączony protokół CHAP.</span><span class="sxs-lookup"><span data-stu-id="f3482-199">hello **Quick Connect** feature does not support connections that have CHAP enabled.</span></span> <span data-ttu-id="f3482-200">Po włączeniu protokołu CHAP, upewnij się, że używasz hello **Connect** przycisku, który jest dostępny na powitania **cele** kartę tooconnect tooa docelowej.</span><span class="sxs-lookup"><span data-stu-id="f3482-200">When CHAP is enabled, make sure that you use hello **Connect** button that is available on hello **Targets** tab tooconnect tooa target.</span></span>

![Połącz tootarget](./media/storsimple-configure-chap/IC740947.png)

<span data-ttu-id="f3482-202">W hello **połączyć tooTarget** dialogowe hello przedstawioną, wybierz pozycję **Dodawanie połączenia tej toohello lista ulubionych elementów docelowych** pole wyboru.</span><span class="sxs-lookup"><span data-stu-id="f3482-202">In hello **Connect tooTarget** dialog box that is presented, select hello **Add this connection toohello list of Favorite Targets** check box.</span></span> <span data-ttu-id="f3482-203">Dzięki temu, że przy każdym uruchomieniu komputera hello podejmowana jest próba toorestore hello połączenia toohello ulubionych obiektów docelowych iSCSI.</span><span class="sxs-lookup"><span data-stu-id="f3482-203">This ensures that every time hello computer restarts, an attempt is made toorestore hello connection toohello iSCSI favorite targets.</span></span>

## <a name="errors-during-configuration"></a><span data-ttu-id="f3482-204">Błędy podczas konfiguracji</span><span class="sxs-lookup"><span data-stu-id="f3482-204">Errors during configuration</span></span>
<span data-ttu-id="f3482-205">Jeśli konfiguracja protokołu CHAP jest niepoprawny, a następnie są prawdopodobnie toosee **niepowodzenie uwierzytelniania** komunikat o błędzie.</span><span class="sxs-lookup"><span data-stu-id="f3482-205">If your CHAP configuration is incorrect, then you are likely toosee an **Authentication failure** error message.</span></span>

## <a name="verification-of-chap-configuration"></a><span data-ttu-id="f3482-206">Weryfikacja konfiguracji protokołu CHAP</span><span class="sxs-lookup"><span data-stu-id="f3482-206">Verification of CHAP configuration</span></span>
<span data-ttu-id="f3482-207">Aby sprawdzić, czy, wykonując następujące kroki hello jest używany protokół CHAP.</span><span class="sxs-lookup"><span data-stu-id="f3482-207">You can verify that CHAP is being used by completing hello following steps.</span></span>

#### <a name="tooverify-your-chap-configuration"></a><span data-ttu-id="f3482-208">tooverify konfiguracji protokołu CHAP</span><span class="sxs-lookup"><span data-stu-id="f3482-208">tooverify your CHAP configuration</span></span>
1. <span data-ttu-id="f3482-209">Kliknij przycisk **Ulubione obiekty docelowe**.</span><span class="sxs-lookup"><span data-stu-id="f3482-209">Click **Favorite Targets**.</span></span>
2. <span data-ttu-id="f3482-210">Wybierz cel hello, dla której jest włączone uwierzytelnianie.</span><span class="sxs-lookup"><span data-stu-id="f3482-210">Select hello target for which you enabled authentication.</span></span>
3. <span data-ttu-id="f3482-211">Kliknij przycisk **szczegóły**.</span><span class="sxs-lookup"><span data-stu-id="f3482-211">Click **Details**.</span></span>
   
    ![Inicjator właściwości ulubionych obiektów docelowych iSCSI](./media/storsimple-configure-chap/IC740951.png)
4. <span data-ttu-id="f3482-213">W hello **ulubionych szczegóły docelowej** okno dialogowe, wpisu notatki hello w hello **uwierzytelniania** pola.</span><span class="sxs-lookup"><span data-stu-id="f3482-213">In hello **Favorite Target Details** dialog box, note hello entry in hello **Authentication** field.</span></span> <span data-ttu-id="f3482-214">Jeśli konfiguracja hello zakończyło się pomyślnie, powinien powiedzieć **protokołu CHAP**.</span><span class="sxs-lookup"><span data-stu-id="f3482-214">If hello configuration was successful, it should say **CHAP**.</span></span>
   
    ![Szczegóły ulubiony obiekt docelowy](./media/storsimple-configure-chap/IC740952.png)

## <a name="next-steps"></a><span data-ttu-id="f3482-216">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f3482-216">Next steps</span></span>
* <span data-ttu-id="f3482-217">Dowiedz się więcej o [zabezpieczenia usługi StorSimple](storsimple-security.md).</span><span class="sxs-lookup"><span data-stu-id="f3482-217">Learn more about [StorSimple security](storsimple-security.md).</span></span>
* <span data-ttu-id="f3482-218">Dowiedz się więcej o [tooadminister usługi Menedżer StorSimple przy użyciu hello urządzenia StorSimple](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="f3482-218">Learn more about [using hello StorSimple Manager service tooadminister your StorSimple device](storsimple-manager-service-administration.md).</span></span>

