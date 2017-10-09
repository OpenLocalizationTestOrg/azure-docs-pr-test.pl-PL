---
title: aaaLog biletu pomocy technicznej dla serii StorSimple 8000 | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak żądania toocreate pomocy technicznej i rozpocząć sesję pomocy technicznej na urządzeniu StorSimple."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 2ebc20fe-f490-4749-8e43-c9fac86f1676
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/27/2017
ms.author: alkohli;anbacker
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: e1a3aa3c56e036c782c4fb502c477dc0feaa0ccd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="contact-microsoft-support-for-your-storsimple"></a><span data-ttu-id="2b981-103">Skontaktuj się z pomocą techniczną firmy Microsoft dla Twojego urządzenia StorSimple</span><span class="sxs-lookup"><span data-stu-id="2b981-103">Contact Microsoft Support for your StorSimple</span></span>
<span data-ttu-id="2b981-104">Jeśli wystąpią problemy z rozwiązania Microsoft Azure StorSimple można utworzyć żądania obsługi technicznej.</span><span class="sxs-lookup"><span data-stu-id="2b981-104">If you encounter any issues with your Microsoft Azure StorSimple solution, you can create a service request for technical support.</span></span> <span data-ttu-id="2b981-105">W ramach sesji online ze specjalistą pomocy technicznej możesz także toostart sesję pomocy technicznej na urządzeniu StorSimple.</span><span class="sxs-lookup"><span data-stu-id="2b981-105">In an online session with your support engineer, you may also need toostart a support session on your StorSimple device.</span></span> <span data-ttu-id="2b981-106">W tym artykule przedstawiono:</span><span class="sxs-lookup"><span data-stu-id="2b981-106">This article walks you through:</span></span>

* <span data-ttu-id="2b981-107">Jak toocreate obsługi żądania.</span><span class="sxs-lookup"><span data-stu-id="2b981-107">How toocreate a support request.</span></span>
* <span data-ttu-id="2b981-108">Jak toostart sesję pomocy technicznej w hello interfejsu programu Windows PowerShell urządzenia StorSimple.</span><span class="sxs-lookup"><span data-stu-id="2b981-108">How toostart a support session in hello Windows PowerShell interface of your StorSimple device.</span></span>

<span data-ttu-id="2b981-109">Przejrzyj hello [StorSimple 8000 serii Obsługa SLA oraz informacje](https://msdn.microsoft.com/library/mt433077.aspx) przed utworzeniem żądania pomocy technicznej.</span><span class="sxs-lookup"><span data-stu-id="2b981-109">Review hello [StorSimple 8000 Series Support SLAs and information](https://msdn.microsoft.com/library/mt433077.aspx) before you create a Support request.</span></span>

## <a name="create-a-support-request"></a><span data-ttu-id="2b981-110">Utwórz żądanie obsługi</span><span class="sxs-lookup"><span data-stu-id="2b981-110">Create a support request</span></span>
<span data-ttu-id="2b981-111">Wykonaj hello następujące kroki toocreate żądania pomocy technicznej:</span><span class="sxs-lookup"><span data-stu-id="2b981-111">Perform hello following steps toocreate a support request:</span></span>

#### <a name="toocreate-a-support-request"></a><span data-ttu-id="2b981-112">toocreate żądania obsługi</span><span class="sxs-lookup"><span data-stu-id="2b981-112">toocreate a support request</span></span>
1. <span data-ttu-id="2b981-113">W hello [klasycznego portalu Azure](https://manage.windowsazure.com/), w hello prawym górnym rogu kliknij nazwę konta, a następnie kliknij przycisk **skontaktuj się z pomocą techniczną firmy Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="2b981-113">In hello [Azure classic portal](https://manage.windowsazure.com/), in hello upper right corner, click your account name and then click **Contact Microsoft Support**.</span></span>
   
    ![MS skontaktuj się z pomocą techniczną przez ManagementPortal](./media/storsimple-contact-microsoft-support/Ibiza1.png)
2. <span data-ttu-id="2b981-115">Będzie przekierowany toohello nowego portalu Azure (portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="2b981-115">You will be redirected toohello new Azure portal (portal.azure.com).</span></span> <span data-ttu-id="2b981-116">Kliknij przycisk hello **nowy obsługuje żądania** kafelka.</span><span class="sxs-lookup"><span data-stu-id="2b981-116">Click hello **New support request** tile.</span></span>
   
    ![MS skontaktuj się z pomocą techniczną przez nowego portalu](./media/storsimple-contact-microsoft-support/Ibiza2.png)
   
    <span data-ttu-id="2b981-118">Po prawej stronie powitania ekranie powitania, hello **nowy obsługuje żądania** pojawi się okienko.</span><span class="sxs-lookup"><span data-stu-id="2b981-118">On hello right side of hello screen, hello **New support request** pane appears.</span></span> 
   
    ![Nowe okienko żądania obsługi](./media/storsimple-contact-microsoft-support/Ibiza3a.png)
3. <span data-ttu-id="2b981-120">W hello **podstawy** okno dialogowe, pełną hello następujące:</span><span class="sxs-lookup"><span data-stu-id="2b981-120">In hello **Basics** dialog box, complete hello following:</span></span>                                
   
   1. <span data-ttu-id="2b981-121">Z hello **wydawania typu** listy rozwijanej wybierz **techniczne**.</span><span class="sxs-lookup"><span data-stu-id="2b981-121">From hello **Issue type** drop-down list , select **Technical**.</span></span>
   2. <span data-ttu-id="2b981-122">Wybierz **subskrypcji** z listy rozwijanej hello.</span><span class="sxs-lookup"><span data-stu-id="2b981-122">Select a **Subscription** from hello drop-down list.</span></span>
   3. <span data-ttu-id="2b981-123">Z hello **usługi** listy rozwijanej wybierz **StorSimple**.</span><span class="sxs-lookup"><span data-stu-id="2b981-123">From hello **Service** drop-down list, select **StorSimple**.</span></span> 
   4. <span data-ttu-id="2b981-124">Wybierz **plan pomocy technicznej** z listy rozwijanej hello.</span><span class="sxs-lookup"><span data-stu-id="2b981-124">Select a **Support plan** from hello drop-down list.</span></span> <span data-ttu-id="2b981-125">Należy tooenable plan płatnej pomocy technicznej, pomocy technicznej.</span><span class="sxs-lookup"><span data-stu-id="2b981-125">You need a paid support plan tooenable Technical Support.</span></span>
4. <span data-ttu-id="2b981-126">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="2b981-126">Click **Next**.</span></span> <span data-ttu-id="2b981-127">Witaj **Problem** zostanie wyświetlone okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="2b981-127">hello **Problem** dialog box appears.</span></span>
   
    ![Nowe okienko żądania obsługi](./media/storsimple-contact-microsoft-support/Ibiza5a.png) 
5. <span data-ttu-id="2b981-129">W hello **Problem** okno dialogowe, pełną hello następujące:</span><span class="sxs-lookup"><span data-stu-id="2b981-129">In hello **Problem** dialog box, complete hello following:</span></span>
   
   1. <span data-ttu-id="2b981-130">Wybierz **ważność** poziomu z listy rozwijanej hello.</span><span class="sxs-lookup"><span data-stu-id="2b981-130">Select a **Severity** level from hello drop-down list.</span></span>
   2. <span data-ttu-id="2b981-131">Wybierz **typ problemu** z listy rozwijanej hello.</span><span class="sxs-lookup"><span data-stu-id="2b981-131">Select a **Problem type** from hello drop-down list.</span></span>
   3. <span data-ttu-id="2b981-132">Wybierz **kategorii** z listy rozwijanej hello.</span><span class="sxs-lookup"><span data-stu-id="2b981-132">Select a **Category** from hello drop-down list.</span></span> 
   4. <span data-ttu-id="2b981-133">W hello **szczegóły** polu Zwięźle opisz swój problem.</span><span class="sxs-lookup"><span data-stu-id="2b981-133">In hello **Details** box, briefly describe your issue.</span></span>
   5. <span data-ttu-id="2b981-134">W hello **okresie** należy wskazać hello datę, godzinę i strefę czasową, która odpowiada toohello ostatniego wystąpienia problemu.</span><span class="sxs-lookup"><span data-stu-id="2b981-134">In hello **Time frame** box, indicate hello date, time, and time zone that corresponds toohello most recent occurrence of your issue.</span></span>
   6. <span data-ttu-id="2b981-135">W obszarze **przekazywania pliku**, kliknij przycisk hello folderu ikona toobrowse tooyour pomocy technicznej pakietu.</span><span class="sxs-lookup"><span data-stu-id="2b981-135">Under **File upload**, click hello folder icon toobrowse tooyour support package.</span></span>
   7. <span data-ttu-id="2b981-136">Wybierz hello **udostępnianie informacji diagnostycznych** pole wyboru.</span><span class="sxs-lookup"><span data-stu-id="2b981-136">Select hello **Share diagnostic information** check box.</span></span>
6. <span data-ttu-id="2b981-137">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="2b981-137">Click **Next**.</span></span> <span data-ttu-id="2b981-138">Witaj **informacje kontaktowe** zostanie wyświetlone okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="2b981-138">hello **Contact information** dialog box appears.</span></span>
   
    ![Nowe okienko żądania obsługi](./media/storsimple-contact-microsoft-support/Ibiza6a.png) 
7. <span data-ttu-id="2b981-140">Wprowadź swoje informacje kontaktowe i wybierz metodę kontaktu (telefonu lub poczty e-mail).</span><span class="sxs-lookup"><span data-stu-id="2b981-140">Enter your contact information and select a contact method (phone or email).</span></span> 
8. <span data-ttu-id="2b981-141">Wybierz hello **Zapisz zmiany dotyczące kontaktu dla przyszłych żądań obsługi** pole wyboru.</span><span class="sxs-lookup"><span data-stu-id="2b981-141">Select hello **Save contact changes for future support requests** check box.</span></span>
9. <span data-ttu-id="2b981-142">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="2b981-142">Click **Create**.</span></span>

<span data-ttu-id="2b981-143">Gdy prześlesz żądanie z pracownikiem pomocy technicznej skontaktuje się z Tobą jak najszybciej tooproceed w żądaniu.</span><span class="sxs-lookup"><span data-stu-id="2b981-143">After you have submitted your request, a Support engineer will contact you as soon as possible tooproceed with your request.</span></span>

## <a name="start-a-support-session-in-windows-powershell-for-storsimple"></a><span data-ttu-id="2b981-144">Rozpocznij sesję pomocy technicznej w programie Windows PowerShell dla urządzenia StorSimple</span><span class="sxs-lookup"><span data-stu-id="2b981-144">Start a support session in Windows PowerShell for StorSimple</span></span>
<span data-ttu-id="2b981-145">tootroubleshoot wszelkie problemy, które mogą wystąpić z urządzeniem StorSimple hello, konieczne będzie tooengage z zespołem Microsoft Support hello.</span><span class="sxs-lookup"><span data-stu-id="2b981-145">tootroubleshoot any issues that you might experience with hello StorSimple device, you will need tooengage with hello Microsoft Support team.</span></span> <span data-ttu-id="2b981-146">Microsoft Support może być konieczne toouse toolog sesji pomocy technicznej, na urządzeniu tooyour.</span><span class="sxs-lookup"><span data-stu-id="2b981-146">Microsoft Support may need toouse a support session toolog on tooyour device.</span></span> 

<span data-ttu-id="2b981-147">Wykonaj następujące hello kroki toostart sesję pomocy technicznej:</span><span class="sxs-lookup"><span data-stu-id="2b981-147">Perform hello following steps toostart a support session:</span></span>

#### <a name="toostart-a-support-session"></a><span data-ttu-id="2b981-148">toostart sesję pomocy technicznej</span><span class="sxs-lookup"><span data-stu-id="2b981-148">toostart a support session</span></span>
1. <span data-ttu-id="2b981-149">Urządzenie hello dostępu bezpośrednio za pomocą konsoli szeregowej hello lub za pośrednictwem sesji telnet z komputera zdalnego.</span><span class="sxs-lookup"><span data-stu-id="2b981-149">Access hello device directly by using hello serial console or through a telnet session from a remote computer.</span></span> <span data-ttu-id="2b981-150">toodo, wykonaj kroki hello w [konsolą szeregową urządzenia przy użyciu programu PuTTY tooconnect toohello](storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="2b981-150">toodo this, follow hello steps in [Use PuTTY tooconnect toohello device serial console](storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span></span>
2. <span data-ttu-id="2b981-151">W sesji hello, który zostanie otwarty, naciśnij klawisz hello **Enter** tooget klucza wiersza polecenia.</span><span class="sxs-lookup"><span data-stu-id="2b981-151">In hello session that opens, press hello **Enter** key tooget a command prompt.</span></span>
3. <span data-ttu-id="2b981-152">W menu konsoli szeregowej hello, wybierz opcję 1, **Zaloguj się przy użyciu pełnego dostępu**.</span><span class="sxs-lookup"><span data-stu-id="2b981-152">In hello serial console menu, select option 1, **Log in with full access**.</span></span>
4. <span data-ttu-id="2b981-153">W wierszu hello wpisz hello następującego hasła:</span><span class="sxs-lookup"><span data-stu-id="2b981-153">At hello prompt, type hello following password:</span></span> 
   
    `Password1`
5. <span data-ttu-id="2b981-154">W wierszu hello wpisz hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="2b981-154">At hello prompt, type hello following command:</span></span>
   
    `Enable-HcsSupportAccess`
6. <span data-ttu-id="2b981-155">Tooyou zostanie wyświetlone zaszyfrowanego ciągu.</span><span class="sxs-lookup"><span data-stu-id="2b981-155">An encrypted string will be presented tooyou.</span></span> <span data-ttu-id="2b981-156">Skopiuj ten ciąg do edytora tekstu, takiego jak Notatnik.</span><span class="sxs-lookup"><span data-stu-id="2b981-156">Copy this string into a text editor such as Notepad.</span></span>
7. <span data-ttu-id="2b981-157">Zapisz ten ciąg i wysyłać je w tooMicrosoft wiadomości e-mail pomocy technicznej.</span><span class="sxs-lookup"><span data-stu-id="2b981-157">Save this string and send it in an email message tooMicrosoft Support.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="2b981-158">Dostęp do pomocy technicznej można wyłączyć, uruchamiając `Disable-HcsSupportAccess`.</span><span class="sxs-lookup"><span data-stu-id="2b981-158">You can disable support access by running `Disable-HcsSupportAccess`.</span></span> <span data-ttu-id="2b981-159">urządzenia StorSimple Hello będzie również próbują uzyskać dostęp do pomocy technicznej toodisable, 8 godzin po hello sesji zostało zainicjowane.</span><span class="sxs-lookup"><span data-stu-id="2b981-159">hello StorSimple device will also attempt toodisable support access 8 hours after hello session was initiated.</span></span> <span data-ttu-id="2b981-160">Jest najlepszym toochange praktyki urządzenia StorSimple poświadczenia po zainicjowaniu sesji pomocy technicznej.</span><span class="sxs-lookup"><span data-stu-id="2b981-160">It is a best practice toochange your StorSimple device credentials after initiating a support session.</span></span>
> 
> 

