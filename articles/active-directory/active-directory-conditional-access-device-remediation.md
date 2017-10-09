---
title: "aaaYou nie można pobrać istnieje w tym miejscu na powitania portalu Azure na urządzeniu z systemem Windows | Dokumentacja firmy Microsoft"
description: "Dowiedz się, gdy nie można w tym miejscu, w którymś z get i co można sprawdzić tooavoid uruchomione w tym oknie dialogowym."
services: active-directory
keywords: "dostęp warunkowy oparty na urządzeniach, rejestracja urządzenia, włączanie rejestracji urządzenia, rejestracja urządzenia i MDM"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 8ad0156c-0812-4855-8563-6fbff6194174
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/05/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: eda2aa10fbff5b3e515723219f61c1cb6f634e29
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="you-cant-get-there-from-here-on-a-windows-device"></a><span data-ttu-id="1f501-104">Nie można dostać się tam z tego miejsca na urządzeniu z systemem Windows</span><span class="sxs-lookup"><span data-stu-id="1f501-104">You can't get there from here on a Windows device</span></span>

<span data-ttu-id="1f501-105">Na przykład podczas próby uzyskania dostępu do intranetu usługi SharePoint Online w organizacji możesz zostać wyświetlona strona z informacją o tym, że *nie można dostać się tam z tego miejsca*.</span><span class="sxs-lookup"><span data-stu-id="1f501-105">During an attempt to, for example, access your organization's SharePoint Online intranet you might run into a page that states that *you can't get there from here*.</span></span> <span data-ttu-id="1f501-106">Widzisz tę stronę, ponieważ administrator skonfigurował zasady dostępu warunkowego, uniemożliwiający organizacji tooyour dostępu do zasobów w niektórych warunkach.</span><span class="sxs-lookup"><span data-stu-id="1f501-106">You are seeing this page, because your administrator has configured a conditional access policy that prevents access tooyour organization's resources under certain conditions.</span></span> <span data-ttu-id="1f501-107">Gdy może być konieczne toocontact pracy działu pomocy technicznej lub tooget Twojego administratora, można rozwiązać ten problem, istnieje kilka rzeczy, które można wypróbować samodzielnie, najpierw.</span><span class="sxs-lookup"><span data-stu-id="1f501-107">While it might be necessary toocontact helpdesk or your administrator tooget this problem solved, there are a few things you can try out yourself, first.</span></span>

<span data-ttu-id="1f501-108">Jeśli używasz **Windows** urządzenia, należy sprawdzić następujące hello:</span><span class="sxs-lookup"><span data-stu-id="1f501-108">If you are using a **Windows** device, you should check hello following:</span></span>

- <span data-ttu-id="1f501-109">Czy używasz obsługiwanej przeglądarki?</span><span class="sxs-lookup"><span data-stu-id="1f501-109">Are you using a supported browser?</span></span>

- <span data-ttu-id="1f501-110">Czy używasz obsługiwanej wersji systemu Windows na urządzeniu?</span><span class="sxs-lookup"><span data-stu-id="1f501-110">Are you running a supported version of Windows on your device?</span></span>

- <span data-ttu-id="1f501-111">Czy urządzenie jest zgodne?</span><span class="sxs-lookup"><span data-stu-id="1f501-111">Is your device compliant?</span></span>






## <a name="supported-browser"></a><span data-ttu-id="1f501-112">Obsługiwana przeglądarka</span><span class="sxs-lookup"><span data-stu-id="1f501-112">Supported browser</span></span>

<span data-ttu-id="1f501-113">Jeśli administrator skonfigurował zasady dostępu warunkowego, dostęp do zasobów organizacji można uzyskiwać tylko za pomocą obsługiwanej przeglądarki.</span><span class="sxs-lookup"><span data-stu-id="1f501-113">If your administrator has configured a conditional access policy, you can only access your organization's resources by using a supported browser.</span></span> <span data-ttu-id="1f501-114">Na urządzeniu z systemem Windows są obsługiwane tylko przeglądarki **Internet Explorer** i **Edge**.</span><span class="sxs-lookup"><span data-stu-id="1f501-114">On a Windows device, only **Internet Explorer** and **Edge** are supported.</span></span>

<span data-ttu-id="1f501-115">Można łatwo zidentyfikować, czy nie może uzyskać dostęp do zasobu powodu nieobsługiwanej przeglądarki tooan analizując sekcja szczegóły hello strony błędu hello:</span><span class="sxs-lookup"><span data-stu-id="1f501-115">You can easily identify whether you can't access a resource due tooan unsupported browser by looking at hello details section of hello error page:</span></span>

<span data-ttu-id="1f501-116">![Komunikat „Nie można dostać się tam z tego miejsca” dotyczący nieobsługiwanych przeglądarek](./media/active-directory-conditional-access-device-remediation/02.png "Scenariusz")</span><span class="sxs-lookup"><span data-stu-id="1f501-116">!["You can't get there from here" message for unsupported browsers](./media/active-directory-conditional-access-device-remediation/02.png "Scenario")</span></span>

<span data-ttu-id="1f501-117">Korygowanie tylko Hello jest toouse przeglądarki obsługującej hello aplikacji dla danej platformy urządzenia.</span><span class="sxs-lookup"><span data-stu-id="1f501-117">hello only remediation is toouse a browser that hello application supports for your device platform.</span></span> <span data-ttu-id="1f501-118">Pełna lista obsługiwanych przeglądarek jest dostępna na stronie [obsługiwanych przeglądarek](active-directory-conditional-access-supported-apps.md#supported-browsers-for-device-based-policies).</span><span class="sxs-lookup"><span data-stu-id="1f501-118">For a complete list of supported browsers, see [supported browsers](active-directory-conditional-access-supported-apps.md#supported-browsers-for-device-based-policies).</span></span>  


## <a name="supported-versions-of-windows"></a><span data-ttu-id="1f501-119">Obsługiwane wersje systemu Windows</span><span class="sxs-lookup"><span data-stu-id="1f501-119">Supported versions of Windows</span></span>

<span data-ttu-id="1f501-120">Hello muszą być spełnione następujące warunki dotyczące systemu operacyjnego Windows hello na urządzeniu:</span><span class="sxs-lookup"><span data-stu-id="1f501-120">hello following must be true about hello Windows operating system on your device:</span></span> 

- <span data-ttu-id="1f501-121">Jeśli używasz systemu operacyjnego z pulpitu systemu Windows na urządzeniu, musi toobe systemu Windows 7 lub nowszy.</span><span class="sxs-lookup"><span data-stu-id="1f501-121">If you are running a Windows desktop operating system on your device, it needs toobe Windows 7 or later.</span></span>
- <span data-ttu-id="1f501-122">Jeśli system operacyjny Windows server są uruchomione na urządzeniu, musi on toobe systemu Windows Server 2008 R2 lub nowszym.</span><span class="sxs-lookup"><span data-stu-id="1f501-122">If you are running a Windows server operating system on your device, it needs toobe Windows Server 2008 R2 or later.</span></span> 


## <a name="compliant-device"></a><span data-ttu-id="1f501-123">Zgodne urządzenie</span><span class="sxs-lookup"><span data-stu-id="1f501-123">Compliant device</span></span>

<span data-ttu-id="1f501-124">Administrator może skonfigurować zasady dostępu warunkowego, który umożliwia organizacji tooyour dostępu do zasobów tylko ze zgodnych urządzeń.</span><span class="sxs-lookup"><span data-stu-id="1f501-124">Your administrator might have configured a conditional access policy that allows access tooyour organization's resources only from compliant devices.</span></span> <span data-ttu-id="1f501-125">toobe zgodne urządzenie musi być albo tooyour dołączonego do lokalnej usługi Active Directory lub przyłączony tooyour usługi Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="1f501-125">toobe compliant, your device must be either joined tooyour on-premises Active Directory or joined tooyour Azure Active Directory.</span></span>

<span data-ttu-id="1f501-126">Można łatwo zidentyfikować, czy nie masz dostępu do zasobów powodu tooa urządzenia, które nie jest zgodne przez wyszukiwanie w sekcji szczegółów hello strony błędu hello:</span><span class="sxs-lookup"><span data-stu-id="1f501-126">You can easily identify whether you can't access a resource due tooa device that is not compliant by looking at hello details section of hello error page:</span></span>
 
<span data-ttu-id="1f501-127">![Komunikaty „Nie można dostać się tam z tego miejsca” dotyczące niezarejestrowanych urządzeń](./media/active-directory-conditional-access-device-remediation/01.png "Scenariusz")</span><span class="sxs-lookup"><span data-stu-id="1f501-127">!["You can't get there from here" messages for unregistered devices](./media/active-directory-conditional-access-device-remediation/01.png "Scenario")</span></span>


### <a name="is-your-device-joined-tooan-on-premises-active-directory"></a><span data-ttu-id="1f501-128">Jest tooan Twojego urządzenia przyłączone do lokalnej usługi Active Directory?</span><span class="sxs-lookup"><span data-stu-id="1f501-128">Is your device joined tooan on-premises Active Directory?</span></span>

<span data-ttu-id="1f501-129">**Jeśli Twoje urządzenie jest dołączane tooan lokalnej usługi Active Directory w organizacji:**</span><span class="sxs-lookup"><span data-stu-id="1f501-129">**If your device is joined tooan on-premises Active Directory in your organization:**</span></span>

1. <span data-ttu-id="1f501-130">Upewnij się, że logowania tooWindows przy użyciu swojego konta służbowego (konta usługi Active Directory).</span><span class="sxs-lookup"><span data-stu-id="1f501-130">Make sure that you sign in tooWindows by using your work account (your Active Directory account).</span></span>
2. <span data-ttu-id="1f501-131">Połącz tooyour sieci firmowej za pośrednictwem wirtualnej sieci prywatnej (VPN) lub funkcji DirectAccess.</span><span class="sxs-lookup"><span data-stu-id="1f501-131">Connect tooyour corporate network via a virtual private network (VPN) or DirectAccess.</span></span>
3. <span data-ttu-id="1f501-132">Po połączeniu, naciśnij klawisze logo systemu Windows hello + hello L toolock klucza sesji systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="1f501-132">After you are connected, press hello Windows logo key + hello L key toolock your Windows session.</span></span>
4. <span data-ttu-id="1f501-133">Odblokuj sesję systemu Windows, wprowadzając poświadczenia konta służbowego.</span><span class="sxs-lookup"><span data-stu-id="1f501-133">Unlock your Windows session by entering your work account credentials.</span></span>
5. <span data-ttu-id="1f501-134">Poczekaj chwilę, a następnie spróbuj ponownie w odpowiedzi na tooaccess hello aplikacji lub usługi.</span><span class="sxs-lookup"><span data-stu-id="1f501-134">Wait for a minute, and then try again tooaccess hello application or service.</span></span>
6. <span data-ttu-id="1f501-135">Jeśli widzisz hello sam kliknij hello **więcej szczegółów** połączyć, a następnie skontaktuj się z administratorem ze szczegółami hello.</span><span class="sxs-lookup"><span data-stu-id="1f501-135">If you see hello same page, click hello **More details** link, and then contact your administrator with hello details.</span></span>


### <a name="is-your-device-not-joined-tooan-on-premises-active-directory"></a><span data-ttu-id="1f501-136">Jest tooan Twojego urządzenia, które nie są przyłączone lokalnej usługi Active Directory?</span><span class="sxs-lookup"><span data-stu-id="1f501-136">Is your device not joined tooan on-premises Active Directory?</span></span>

<span data-ttu-id="1f501-137">Jeśli urządzenie nie jest dołączony tooan lokalnej usługi Active Directory i systemem Windows 10, dostępne są dwie opcje:</span><span class="sxs-lookup"><span data-stu-id="1f501-137">If your device is not joined tooan on-premises Active Directory and runs Windows 10, you have two options:</span></span>

* <span data-ttu-id="1f501-138">Uruchom funkcję Azure AD Join</span><span class="sxs-lookup"><span data-stu-id="1f501-138">Run Azure AD Join</span></span>
* <span data-ttu-id="1f501-139">Dodaj pracy lub szkołą tooWindows konta</span><span class="sxs-lookup"><span data-stu-id="1f501-139">Add your work or school account tooWindows</span></span>

<span data-ttu-id="1f501-140">Aby uzyskać informacje o różnicach między tymi dwoma opcjami, zobacz [Korzystanie z urządzeń z systemem Windows 10 w miejscu pracy](active-directory-azureadjoin-windows10-devices.md).</span><span class="sxs-lookup"><span data-stu-id="1f501-140">For information about how these options are different, see [Using Windows 10 devices in your workplace](active-directory-azureadjoin-windows10-devices.md).</span></span>  
<span data-ttu-id="1f501-141">Możliwe są następujące sytuacje:</span><span class="sxs-lookup"><span data-stu-id="1f501-141">If your device:</span></span>

- <span data-ttu-id="1f501-142">Należy tooyour organizacji, należy uruchomić Azure AD Join.</span><span class="sxs-lookup"><span data-stu-id="1f501-142">Belongs tooyour organization, you should run Azure AD Join.</span></span>
- <span data-ttu-id="1f501-143">Jest osobiste urządzenie lub z systemem Windows phone, należy dodać pracy lub szkołą tooWindows konta</span><span class="sxs-lookup"><span data-stu-id="1f501-143">Is a personal device or a Windows phone, you should add your work or school account tooWindows</span></span> 



#### <a name="azure-ad-join-on-windows-10"></a><span data-ttu-id="1f501-144">Funkcja Azure AD Join w systemie Windows 10</span><span class="sxs-lookup"><span data-stu-id="1f501-144">Azure AD Join on Windows 10</span></span>

<span data-ttu-id="1f501-145">Hello toojoin kroki tooAzure Twojego urządzenia AD są również powiązane hello wersji systemu Windows 10 są na nim uruchomione.</span><span class="sxs-lookup"><span data-stu-id="1f501-145">hello steps toojoin your device tooAzure AD are tied hello version of Windows 10 you are running on it.</span></span> <span data-ttu-id="1f501-146">toodetermine hello wersji systemu operacyjnego Windows 10, uruchom hello **winver** polecenia:</span><span class="sxs-lookup"><span data-stu-id="1f501-146">toodetermine hello version of your Windows 10 operating system, run hello **winver** command:</span></span> 

![Wersja systemu Windows](./media/active-directory-conditional-access-device-remediation/03.png )


<span data-ttu-id="1f501-148">**Rocznicowa aktualizacja systemu Windows 10 (wersja 1607):**</span><span class="sxs-lookup"><span data-stu-id="1f501-148">**Windows 10 Anniversary Update (Version 1607):**</span></span>

1. <span data-ttu-id="1f501-149">Otwórz hello **ustawienia** aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1f501-149">Open hello **Settings** app.</span></span>
2. <span data-ttu-id="1f501-150">Kliknij pozycję **Konta** > **Dostęp w pracy lub szkole**.</span><span class="sxs-lookup"><span data-stu-id="1f501-150">Click **Accounts** > **Access work or school**.</span></span>
3. <span data-ttu-id="1f501-151">Kliknij przycisk **Połącz**.</span><span class="sxs-lookup"><span data-stu-id="1f501-151">Click **Connect**.</span></span>
4. <span data-ttu-id="1f501-152">Kliknij przycisk **Dołącz to urządzenie tooAzure AD**.</span><span class="sxs-lookup"><span data-stu-id="1f501-152">Click **Join this device tooAzure AD**.</span></span>
5. <span data-ttu-id="1f501-153">Organizacja tooyour uwierzytelniania, zapewniają uwierzytelnianie wieloskładnikowe, jeśli zostanie wyświetlony monit, a następnie wykonaj kroki hello, które są wyświetlane.</span><span class="sxs-lookup"><span data-stu-id="1f501-153">Authenticate tooyour organization, provide multi-factor authentication if prompted, and then follow hello steps that are shown.</span></span>
6. <span data-ttu-id="1f501-154">Wyloguj się, a następnie zaloguj się przy użyciu swojego konta służbowego.</span><span class="sxs-lookup"><span data-stu-id="1f501-154">Sign out, and then sign in with your work account.</span></span>
7. <span data-ttu-id="1f501-155">Spróbuj ponownie tooaccess hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1f501-155">Try again tooaccess hello application.</span></span>

<span data-ttu-id="1f501-156">**Windows 10 — aktualizacja z listopada 2015 (wersja 1511):**</span><span class="sxs-lookup"><span data-stu-id="1f501-156">**Windows 10 November 2015 Update (Version 1511):**</span></span>

1. <span data-ttu-id="1f501-157">Otwórz hello **ustawienia** aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1f501-157">Open hello **Settings** app.</span></span>
2. <span data-ttu-id="1f501-158">Kliknij pozycję **System** > **Informacje**.</span><span class="sxs-lookup"><span data-stu-id="1f501-158">Click **System** > **About**.</span></span>
3. <span data-ttu-id="1f501-159">Kliknij pozycję **Przyłącz do usługi Azure AD**.</span><span class="sxs-lookup"><span data-stu-id="1f501-159">Click **Join Azure AD**.</span></span>
4. <span data-ttu-id="1f501-160">Organizacja tooyour uwierzytelniania, zapewniają uwierzytelnianie wieloskładnikowe, jeśli zostanie wyświetlony monit, a następnie wykonaj kroki hello, które są wyświetlane.</span><span class="sxs-lookup"><span data-stu-id="1f501-160">Authenticate tooyour organization, provide multi-factor authentication if prompted, and then follow hello steps that are shown.</span></span>
5. <span data-ttu-id="1f501-161">Wyloguj się, a następnie zaloguj się przy użyciu swojego konta służbowego (Twojego konta usługi Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1f501-161">Sign out, and then sign in with your work account (your Azure AD account).</span></span>
6. <span data-ttu-id="1f501-162">Spróbuj ponownie tooaccess hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1f501-162">Try again tooaccess hello application.</span></span>


#### <a name="workplace-join-on-windows-81"></a><span data-ttu-id="1f501-163">Przyłączanie w miejscu pracy w systemie Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="1f501-163">Workplace Join on Windows 8.1</span></span>

<span data-ttu-id="1f501-164">Jeśli urządzenie nie jest przyłączony do domeny i systemem Windows 8.1, toodo dołączanie do i zarejestrować się w programie Microsoft Intune, hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="1f501-164">If your device is not domain-joined and runs Windows 8.1, toodo a Workplace Join and enroll in Microsoft Intune, do hello following steps:</span></span>

1. <span data-ttu-id="1f501-165">Otwórz okno **Ustawienia komputera**.</span><span class="sxs-lookup"><span data-stu-id="1f501-165">Open **PC Settings**.</span></span>
2. <span data-ttu-id="1f501-166">Kliknij pozycję **Sieć** > **Miejsce pracy**.</span><span class="sxs-lookup"><span data-stu-id="1f501-166">Click **Network** > **Workplace**.</span></span>
3. <span data-ttu-id="1f501-167">Kliknij pozycję **Dołącz**.</span><span class="sxs-lookup"><span data-stu-id="1f501-167">Click **Join**.</span></span>
4. <span data-ttu-id="1f501-168">Organizacja tooyour uwierzytelniania, zapewniają uwierzytelnianie wieloskładnikowe, jeśli zostanie wyświetlony monit, a następnie wykonaj kroki hello, które są wyświetlane.</span><span class="sxs-lookup"><span data-stu-id="1f501-168">Authenticate tooyour organization, provide multi-factor authentication if prompted, and then follow hello steps that are shown.</span></span>
5. <span data-ttu-id="1f501-169">Kliknij pozycję **Włącz**.</span><span class="sxs-lookup"><span data-stu-id="1f501-169">Click **Turn on**.</span></span>
6. <span data-ttu-id="1f501-170">Spróbuj ponownie tooaccess hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1f501-170">Try again tooaccess hello application.</span></span>



#### <a name="add-your-work-or-school-account-toowindows"></a><span data-ttu-id="1f501-171">Dodaj pracy lub szkołą tooWindows konta</span><span class="sxs-lookup"><span data-stu-id="1f501-171">Add your work or school account tooWindows</span></span> 


<span data-ttu-id="1f501-172">**Rocznicowa aktualizacja systemu Windows 10 (wersja 1607):**</span><span class="sxs-lookup"><span data-stu-id="1f501-172">**Windows 10 Anniversary Update (Version 1607):**</span></span>

1. <span data-ttu-id="1f501-173">Otwórz hello **ustawienia** aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1f501-173">Open hello **Settings** app.</span></span>
2. <span data-ttu-id="1f501-174">Kliknij pozycję **Konta** > **Dostęp w pracy lub szkole**.</span><span class="sxs-lookup"><span data-stu-id="1f501-174">Click **Accounts** > **Access work or school**.</span></span>
3. <span data-ttu-id="1f501-175">Kliknij przycisk **Połącz**.</span><span class="sxs-lookup"><span data-stu-id="1f501-175">Click **Connect**.</span></span>
4. <span data-ttu-id="1f501-176">Organizacja tooyour uwierzytelniania, zapewniają uwierzytelnianie wieloskładnikowe, jeśli zostanie wyświetlony monit, a następnie wykonaj kroki hello, które są wyświetlane.</span><span class="sxs-lookup"><span data-stu-id="1f501-176">Authenticate tooyour organization, provide multi-factor authentication if prompted, and then follow hello steps that are shown.</span></span>
5. <span data-ttu-id="1f501-177">Spróbuj ponownie tooaccess hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1f501-177">Try again tooaccess hello application.</span></span>


<span data-ttu-id="1f501-178">**Windows 10 — aktualizacja z listopada 2015 (wersja 1511):**</span><span class="sxs-lookup"><span data-stu-id="1f501-178">**Windows 10 November 2015 Update (Version 1511):**</span></span>

1. <span data-ttu-id="1f501-179">Otwórz hello **ustawienia** aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1f501-179">Open hello **Settings** app.</span></span>
2. <span data-ttu-id="1f501-180">Kliknij pozycję **Konta** > **Twoje konta**.</span><span class="sxs-lookup"><span data-stu-id="1f501-180">Click **Accounts** > **Your accounts**.</span></span>
3. <span data-ttu-id="1f501-181">Kliknij pozycję **Dodaj konto służbowe**.</span><span class="sxs-lookup"><span data-stu-id="1f501-181">Click **Add work or school account**.</span></span>
4. <span data-ttu-id="1f501-182">Organizacja tooyour uwierzytelniania, zapewniają uwierzytelnianie wieloskładnikowe, jeśli zostanie wyświetlony monit, a następnie wykonaj kroki hello, które są wyświetlane.</span><span class="sxs-lookup"><span data-stu-id="1f501-182">Authenticate tooyour organization, provide multi-factor authentication if prompted, and then follow hello steps that are shown.</span></span>
5. <span data-ttu-id="1f501-183">Spróbuj ponownie tooaccess hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1f501-183">Try again tooaccess hello application.</span></span>





## <a name="next-steps"></a><span data-ttu-id="1f501-184">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="1f501-184">Next steps</span></span>
[<span data-ttu-id="1f501-185">Dostęp warunkowy do usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1f501-185">Azure Active Directory conditional access</span></span>](active-directory-conditional-access.md)

