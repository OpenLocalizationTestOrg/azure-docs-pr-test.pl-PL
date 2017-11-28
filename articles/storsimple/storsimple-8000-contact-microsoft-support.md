---
title: Tworzenie biletu pomocy technicznej lub w przypadku serii StorSimple 8000 | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak rejestrować żądania pomocy technicznej i rozpocząć sesję pomocy technicznej na urządzeniu z serii StorSimple 8000."
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
ms.date: 07/25/2017
ms.author: alkohli;
ms.openlocfilehash: 4b5a14237ce79100f980b2186b2c3c887abaa296
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="contact-microsoft-support"></a><span data-ttu-id="f360a-103">Kontakt z pomocą techniczną firmy Microsoft</span><span class="sxs-lookup"><span data-stu-id="f360a-103">Contact Microsoft Support</span></span>

<span data-ttu-id="f360a-104">Menedżer urządzeń StorSimple oferuje możliwość **dziennika nowe żądanie pomocy technicznej** wewnątrz bloku podsumowania usługi.</span><span class="sxs-lookup"><span data-stu-id="f360a-104">The StorSimple Device Manager provides the capability to **log a new support request** within the service summary blade.</span></span> <span data-ttu-id="f360a-105">Jeśli wystąpią problemy z rozwiązania StorSimple można utworzyć żądania obsługi technicznej.</span><span class="sxs-lookup"><span data-stu-id="f360a-105">If you encounter any issues with your StorSimple solution, you can create a service request for technical support.</span></span> <span data-ttu-id="f360a-106">W ramach sesji online ze specjalistą pomocy technicznej może również należy rozpocząć sesję pomocy technicznej na urządzeniu StorSimple.</span><span class="sxs-lookup"><span data-stu-id="f360a-106">In an online session with your support engineer, you may also need to start a support session on your StorSimple device.</span></span> <span data-ttu-id="f360a-107">W tym artykule przedstawiono:</span><span class="sxs-lookup"><span data-stu-id="f360a-107">This article walks you through:</span></span>

* <span data-ttu-id="f360a-108">Jak utworzyć żądanie pomocy technicznej.</span><span class="sxs-lookup"><span data-stu-id="f360a-108">How to create a support request.</span></span>
* <span data-ttu-id="f360a-109">Jak zarządzać cykl żądania obsługi z w portalu.</span><span class="sxs-lookup"><span data-stu-id="f360a-109">How to manage a support request lifecycle from within the portal.</span></span>
* <span data-ttu-id="f360a-110">Jak rozpocząć sesję pomocy technicznej w interfejsie programu Windows PowerShell urządzenia StorSimple.</span><span class="sxs-lookup"><span data-stu-id="f360a-110">How to start a support session in the Windows PowerShell interface of your StorSimple device.</span></span>

<span data-ttu-id="f360a-111">Przegląd [StorSimple 8000 serii Obsługa SLA oraz informacje](https://msdn.microsoft.com/library/mt433077.aspx) przed utworzeniem żądania pomocy technicznej.</span><span class="sxs-lookup"><span data-stu-id="f360a-111">Review the [StorSimple 8000 Series Support SLAs and information](https://msdn.microsoft.com/library/mt433077.aspx) before you create a Support request.</span></span>

## <a name="create-a-support-request"></a><span data-ttu-id="f360a-112">Utwórz żądanie obsługi</span><span class="sxs-lookup"><span data-stu-id="f360a-112">Create a support request</span></span>

<span data-ttu-id="f360a-113">W zależności od Twojego [plan pomocy technicznej](https://azure.microsoft.com/support/plans/), można tworzyć bilety pomocy technicznej problemu, na urządzeniu StorSimple bezpośrednio z bloku podsumowania usługi Menedżer StorSimple urządzenia.</span><span class="sxs-lookup"><span data-stu-id="f360a-113">Depending upon your [support plan](https://azure.microsoft.com/support/plans/), you can create support tickets for an issue on your StorSimple device directly from the StorSimple Device Manager service summary blade.</span></span> <span data-ttu-id="f360a-114">Wykonaj poniższe kroki, aby utworzyć żądanie pomocy technicznej:</span><span class="sxs-lookup"><span data-stu-id="f360a-114">Perform the following steps to create a support request:</span></span>

#### <a name="to-create-a-support-request"></a><span data-ttu-id="f360a-115">Aby utworzyć żądanie obsługi</span><span class="sxs-lookup"><span data-stu-id="f360a-115">To create a support request</span></span>

1. <span data-ttu-id="f360a-116">Przejdź do usługi Menedżer urządzeń StorSimple.</span><span class="sxs-lookup"><span data-stu-id="f360a-116">Go to your StorSimple Device Manager service.</span></span> <span data-ttu-id="f360a-117">W bloku Podsumowanie ustawień usługi, przejdź do **pomocy technicznej i rozwiązywania problemów** sekcji, a następnie kliknij przycisk **nowy obsługuje żądania**.</span><span class="sxs-lookup"><span data-stu-id="f360a-117">In the service summary blade settings, go to **SUPPORT + TROUBLESHOOTING** section and then click **New support request**.</span></span>
     
    ![MS skontaktuj się z pomocą techniczną przez nowego portalu](./media/storsimple-8000-contact-microsoft-support/contactsupport1.png)
   
2. <span data-ttu-id="f360a-119">W **nowy obsługuje żądania** bloku, wybierz opcję **podstawy**.</span><span class="sxs-lookup"><span data-stu-id="f360a-119">In the **New support request** blade, select **Basics**.</span></span> <span data-ttu-id="f360a-120">W **podstawy** blok, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="f360a-120">In the **Basics** blade, do the following steps:</span></span>
   1. <span data-ttu-id="f360a-121">Z **wydawania typu** listy rozwijanej wybierz **techniczne**.</span><span class="sxs-lookup"><span data-stu-id="f360a-121">From the **Issue type** drop-down list , select **Technical**.</span></span>
   2. <span data-ttu-id="f360a-122">Bieżący **subskrypcji**, **usługi** typu i **zasobów** (usługa Menedżera urządzeń StorSimple) są automatycznie wybrana.</span><span class="sxs-lookup"><span data-stu-id="f360a-122">The current **Subscription**, **Service** type, and the **Resource** (StorSimple Device Manager service) are automatically chosen.</span></span> 
   3. <span data-ttu-id="f360a-123">Wybierz **plan pomocy technicznej** z listy rozwijanej, jeśli masz wiele planów skojarzonych z Twoją subskrypcją.</span><span class="sxs-lookup"><span data-stu-id="f360a-123">Select a **Support plan** from the drop-down list if you have multiple plans associated with your subscription.</span></span> <span data-ttu-id="f360a-124">Należy plan płatnej pomocy technicznej, aby włączyć pomocy technicznej.</span><span class="sxs-lookup"><span data-stu-id="f360a-124">You need a paid support plan to enable Technical Support.</span></span>
   4. <span data-ttu-id="f360a-125">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="f360a-125">Click **Next**.</span></span>

       ![MS skontaktuj się z pomocą techniczną przez nowego portalu](./media/storsimple-8000-contact-microsoft-support/contactsupport2.png)

3. <span data-ttu-id="f360a-127">W **nowy obsługuje żądania** bloku, wybierz opcję **krok 2 Problem**.</span><span class="sxs-lookup"><span data-stu-id="f360a-127">In the **New support request** blade, select **Step 2 Problem**.</span></span> <span data-ttu-id="f360a-128">W **Problem** blok, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="f360a-128">In the **Problem** blade, do the following steps:</span></span>
    
    1. <span data-ttu-id="f360a-129">Wybierz **ważność**.</span><span class="sxs-lookup"><span data-stu-id="f360a-129">Choose the **Severity**.</span></span>
    2. <span data-ttu-id="f360a-130">Określ, czy problem jest związana z urządzenia lub usługi Menedżer StorSimple urządzenia.</span><span class="sxs-lookup"><span data-stu-id="f360a-130">Specify if the issue is related to the appliance or the StorSimple Device Manager service.</span></span>
    3. <span data-ttu-id="f360a-131">Wybierz **kategorii** w tym problemie i podaj więcej **szczegóły** o problemie.</span><span class="sxs-lookup"><span data-stu-id="f360a-131">Choose a **Category** for this issue and provide more **Details** about the issue.</span></span>
    4. <span data-ttu-id="f360a-132">Podaj datę i godzinę dla problemu.</span><span class="sxs-lookup"><span data-stu-id="f360a-132">Provide the start date and time for the problem.</span></span>
    5. <span data-ttu-id="f360a-133">W **przekazywania pliku**, kliknij ikonę folderu, aby przejść do pakietu programu obsługi.</span><span class="sxs-lookup"><span data-stu-id="f360a-133">In the **File upload**, click the folder icon to browse to your support package.</span></span>
    6. <span data-ttu-id="f360a-134">Sprawdź **udostępnianie informacji diagnostycznych**.</span><span class="sxs-lookup"><span data-stu-id="f360a-134">Check **Share diagnostic information**.</span></span>
    7. <span data-ttu-id="f360a-135">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="f360a-135">Click **Next**.</span></span>

       ![MS skontaktuj się z pomocą techniczną przez nowego portalu](./media/storsimple-8000-contact-microsoft-support/contactsupport3.png) 

4. <span data-ttu-id="f360a-137">W **nowy obsługuje żądania** bloku, kliknij przycisk **informacji skontaktuj się z kroku 3**.</span><span class="sxs-lookup"><span data-stu-id="f360a-137">In the **New support request** blade, click **Step 3 Contact information**.</span></span> <span data-ttu-id="f360a-138">W **informacje kontaktowe** blok, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="f360a-138">In the **Contact information** blade, do the following steps:</span></span>

    1. <span data-ttu-id="f360a-139">W **opcje kontaktu**, podaj preferowaną metodę kontaktu (telefonu lub poczty e-mail) i języka.</span><span class="sxs-lookup"><span data-stu-id="f360a-139">In the **Contact options**, provide your preferred contact method (phone or email) and the language.</span></span> <span data-ttu-id="f360a-140">Czas odpowiedzi jest automatycznie wybierany w oparciu o plan subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="f360a-140">The response time is automatically selected based on your subscription plan.</span></span>
    2. <span data-ttu-id="f360a-141">Informacje kontaktowe podać nazwę, poczty e-mail, opcjonalne kontaktu, kraju.</span><span class="sxs-lookup"><span data-stu-id="f360a-141">In the Contact information, provide your name, email, optional contact, country.</span></span> <span data-ttu-id="f360a-142">Wybierz **Zapisz zmiany dotyczące kontaktu dla przyszłych żądań obsługi** pole wyboru.</span><span class="sxs-lookup"><span data-stu-id="f360a-142">Select the **Save contact changes for future support requests** check box.</span></span>
    3. <span data-ttu-id="f360a-143">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="f360a-143">Click **Create**.</span></span>
   
        ![MS skontaktuj się z pomocą techniczną przez nowego portalu](./media/storsimple-8000-contact-microsoft-support/contactsupport5.png)   

    <span data-ttu-id="f360a-145">Microsoft Support użyje tych informacji do dotrzeć do Ciebie, aby uzyskać więcej informacji, diagnozowanie i rozwiązywanie.</span><span class="sxs-lookup"><span data-stu-id="f360a-145">Microsoft Support will use this information to reach out to you for further information, diagnosis, and resolution.</span></span>
<span data-ttu-id="f360a-146">Gdy prześlesz żądanie z pracownikiem pomocy technicznej skontaktuje się z Tobą tak szybko, jak to możliwe, aby przejść do żądania.</span><span class="sxs-lookup"><span data-stu-id="f360a-146">After you have submitted your request, a Support engineer will contact you as soon as possible to proceed with your request.</span></span>

## <a name="manage-a-support-request"></a><span data-ttu-id="f360a-147">Zarządzanie żądania obsługi</span><span class="sxs-lookup"><span data-stu-id="f360a-147">Manage a support request</span></span>

<span data-ttu-id="f360a-148">Po utworzeniu biletu pomocy technicznej możesz zarządzać jego cyklem życia z poziomu portalu.</span><span class="sxs-lookup"><span data-stu-id="f360a-148">After creating a support ticket, you can manage the lifecycle of the ticket from within the portal.</span></span>

#### <a name="to-manage-your-support-requests"></a><span data-ttu-id="f360a-149">Do zarządzania własnych żądań pomocy technicznej</span><span class="sxs-lookup"><span data-stu-id="f360a-149">To manage your support requests</span></span>

1. <span data-ttu-id="f360a-150">Aby przejść do strony pomocy i obsługi technicznej, przejdź do **Przeglądaj > Pomoc i obsługa techniczna**.</span><span class="sxs-lookup"><span data-stu-id="f360a-150">To get to the help and support page, navigate to **Browse > Help + support**.</span></span>

    ![Zarządzanie żądaniami obsługi](./media/storsimple-8000-contact-microsoft-support/managesupport1.png)

2. <span data-ttu-id="f360a-152">Tabelaryczny spis wszystkich żądań pomocy technicznej jest wyświetlany w **Pomoc i obsługa techniczna** bloku.</span><span class="sxs-lookup"><span data-stu-id="f360a-152">A tabular listing of All the support requests is displayed in the **Help + support** blade.</span></span>

    ![Zarządzanie żądaniami obsługi](./media/storsimple-8000-contact-microsoft-support/managesupport2.png)

3. <span data-ttu-id="f360a-154">Wybierz, a następnie kliknij przycisk żądania pomocy technicznej.</span><span class="sxs-lookup"><span data-stu-id="f360a-154">Select and click a support request.</span></span> <span data-ttu-id="f360a-155">Można wyświetlić stan i szczegóły dla tego żądania.</span><span class="sxs-lookup"><span data-stu-id="f360a-155">You can view the status and the details for this request.</span></span> <span data-ttu-id="f360a-156">Kliknij przycisk **+ nowy komunikat** aby kolejnych czynności związanych z tym żądaniem.</span><span class="sxs-lookup"><span data-stu-id="f360a-156">Click **+ New message** if you want to follow up on this request.</span></span>

    ![Zarządzanie żądaniami obsługi](./media/storsimple-8000-contact-microsoft-support/managesupport3.png)

## <a name="start-a-support-session-in-windows-powershell-for-storsimple"></a><span data-ttu-id="f360a-158">Rozpocznij sesję pomocy technicznej w programie Windows PowerShell dla urządzenia StorSimple</span><span class="sxs-lookup"><span data-stu-id="f360a-158">Start a support session in Windows PowerShell for StorSimple</span></span>

<span data-ttu-id="f360a-159">Aby rozwiązać problemy, które mogą pojawić się z urządzeniem StorSimple, konieczne będzie współpracować z zespołu Support firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="f360a-159">To troubleshoot any issues that you might experience with the StorSimple device, you will need to engage with the Microsoft Support team.</span></span> <span data-ttu-id="f360a-160">Microsoft Support konieczne może być zastosowanie sesji pomocy technicznej do logowania się do urządzenia.</span><span class="sxs-lookup"><span data-stu-id="f360a-160">Microsoft Support may need to use a support session to log on to your device.</span></span>

<span data-ttu-id="f360a-161">Wykonaj poniższe kroki, aby rozpocząć sesję pomocy technicznej:</span><span class="sxs-lookup"><span data-stu-id="f360a-161">Perform the following steps to start a support session:</span></span>

#### <a name="to-start-a-support-session"></a><span data-ttu-id="f360a-162">Aby rozpocząć sesję pomocy technicznej</span><span class="sxs-lookup"><span data-stu-id="f360a-162">To start a support session</span></span>

1. <span data-ttu-id="f360a-163">Dostęp do urządzenia, za pomocą konsoli szeregowej lub za pośrednictwem sesji telnet z komputera zdalnego.</span><span class="sxs-lookup"><span data-stu-id="f360a-163">Access the device directly by using the serial console or through a telnet session from a remote computer.</span></span> <span data-ttu-id="f360a-164">Aby to zrobić, wykonaj kroki opisane w [przy użyciu programu PuTTY można nawiązać połączenia z konsolą szeregową urządzenia](storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="f360a-164">To do this, follow the steps in [Use PuTTY to connect to the device serial console](storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span></span>
2. <span data-ttu-id="f360a-165">W sesji, który zostanie otwarty, naciśnij klawisz **Enter** klawisz, aby wyświetlić wiersz polecenia.</span><span class="sxs-lookup"><span data-stu-id="f360a-165">In the session that opens, press the **Enter** key to get a command prompt.</span></span>
3. <span data-ttu-id="f360a-166">W menu konsoli szeregowej wybierz opcję 1, **Zaloguj się przy użyciu pełnego dostępu**.</span><span class="sxs-lookup"><span data-stu-id="f360a-166">In the serial console menu, select option 1, **Log in with full access**.</span></span>
4. <span data-ttu-id="f360a-167">W wierszu polecenia wpisz następujące hasło:</span><span class="sxs-lookup"><span data-stu-id="f360a-167">At the prompt, type the following password:</span></span>
   
    `Password1`
5. <span data-ttu-id="f360a-168">W wierszu polecenia wpisz następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="f360a-168">At the prompt, type the following command:</span></span>
   
    `Enable-HcsSupportAccess`
6. <span data-ttu-id="f360a-169">Do użytkownika zostanie wyświetlone zaszyfrowanego ciągu.</span><span class="sxs-lookup"><span data-stu-id="f360a-169">An encrypted string will be presented to you.</span></span> <span data-ttu-id="f360a-170">Skopiuj ten ciąg do edytora tekstu, takiego jak Notatnik.</span><span class="sxs-lookup"><span data-stu-id="f360a-170">Copy this string into a text editor such as Notepad.</span></span>
7. <span data-ttu-id="f360a-171">Zapisz ten ciąg i wysłać go w wiadomości e-mail do firmy Microsoft Support.</span><span class="sxs-lookup"><span data-stu-id="f360a-171">Save this string and send it in an email message to Microsoft Support.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f360a-172">Dostęp do pomocy technicznej można wyłączyć, uruchamiając `Disable-HcsSupportAccess`.</span><span class="sxs-lookup"><span data-stu-id="f360a-172">You can disable support access by running `Disable-HcsSupportAccess`.</span></span> <span data-ttu-id="f360a-173">Urządzenia StorSimple spróbuje również wyłączyć dostęp do pomocy technicznej 8 godzin po sesji zostało zainicjowane.</span><span class="sxs-lookup"><span data-stu-id="f360a-173">The StorSimple device will also attempt to disable support access 8 hours after the session was initiated.</span></span> <span data-ttu-id="f360a-174">Jest najlepszym rozwiązaniem jest zmiana poświadczeń urządzenia StorSimple po zainicjowaniu sesji pomocy technicznej.</span><span class="sxs-lookup"><span data-stu-id="f360a-174">It is a best practice to change your StorSimple device credentials after initiating a support session.</span></span>


## <a name="next-steps"></a><span data-ttu-id="f360a-175">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f360a-175">Next steps</span></span>

<span data-ttu-id="f360a-176">Dowiedz się, jak [zdiagnozować i rozwiązać problemy związane z serii StorSimple 8000 urządzenia](storsimple-troubleshoot-deployment.md)</span><span class="sxs-lookup"><span data-stu-id="f360a-176">Learn how to [diagnose and solve problems related to your StorSimple 8000 series device](storsimple-troubleshoot-deployment.md)</span></span>
