---
title: "Synchronizacja programu Azure AD Connect: Zmiana konta usługi synchronizacji połączyć hello Azure AD | Dokumentacja firmy Microsoft"
description: "W tym dokumencie tematu opisano hello klucza szyfrowania i jak tooabandon po hello hasło jest zmienione."
services: active-directory
keywords: "Konto usługi synchronizacji programu Azure AD, hasło"
documentationcenter: 
author: cychua
manager: femila
editor: 
ms.assetid: 76b19162-8b16-4960-9e22-bd64e6675ecc
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 11948ac4662f722e4f684ef6c9b9ccdc6387e60f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="changing-hello-azure-ad-connect-sync-service-account-password"></a><span data-ttu-id="ab4ff-104">Zmiana hasła konta usługi synchronizacji Azure AD Connect hello</span><span class="sxs-lookup"><span data-stu-id="ab4ff-104">Changing hello Azure AD Connect sync service account password</span></span>
<span data-ttu-id="ab4ff-105">Jeśli zmienisz hasło konta usługi synchronizacji Azure AD Connect hello hello usługi synchronizacji nie będą mogli start poprawnie dopiero po porzucone hello klucza szyfrowania i ponownie zainicjować hasło konta usługi synchronizacji Azure AD Connect hello.</span><span class="sxs-lookup"><span data-stu-id="ab4ff-105">If you change hello  Azure AD Connect sync service account password, hello Synchronization Service will not be able start correctly until you have abandoned hello encryption key and reinitialized hello Azure AD Connect sync service account password.</span></span> 

<span data-ttu-id="ab4ff-106">Azure AD Connect, jako część usługi synchronizacji hello używa szyfrowania klucza toostore hello hasła hello usług AD DS i konta usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ab4ff-106">Azure AD Connect, as part of hello Synchronization Services uses an encryption key toostore hello passwords of hello AD DS and Azure AD service accounts.</span></span>  <span data-ttu-id="ab4ff-107">Konta te są szyfrowane przed są przechowywane w bazie danych hello.</span><span class="sxs-lookup"><span data-stu-id="ab4ff-107">These accounts are encrypted before they are stored in hello database.</span></span> 

<span data-ttu-id="ab4ff-108">Witaj klucz szyfrowania używany jest zabezpieczone przy użyciu [ochrony danych systemu Windows (DPAPI)](https://msdn.microsoft.com/library/ms995355.aspx).</span><span class="sxs-lookup"><span data-stu-id="ab4ff-108">hello encryption key used is secured using [Windows Data Protection (DPAPI)](https://msdn.microsoft.com/library/ms995355.aspx).</span></span> <span data-ttu-id="ab4ff-109">DPAPI chroni hello klucza szyfrowania za pomocą hello **hasło konta usługi synchronizacji programu hello Azure AD Connect**.</span><span class="sxs-lookup"><span data-stu-id="ab4ff-109">DPAPI protects hello encryption key using hello **password of hello Azure AD Connect sync service account**.</span></span> 

<span data-ttu-id="ab4ff-110">Jeśli potrzebujesz hasło konta usługi hello toochange można użyć procedury hello [klucza szyfrowania programu Abandoning hello Azure AD Connect synchronizacji](#abandoning-the-azure-ad-connect-sync-encryption-key) tooaccomplish to.</span><span class="sxs-lookup"><span data-stu-id="ab4ff-110">If you need toochange hello service account password you can use hello procedures in [Abandoning hello Azure AD Connect Sync encryption key](#abandoning-the-azure-ad-connect-sync-encryption-key) tooaccomplish this.</span></span>  <span data-ttu-id="ab4ff-111">Te procedury należy również Jeśli potrzebujesz klucza szyfrowania hello tooabandon różnych przyczyn.</span><span class="sxs-lookup"><span data-stu-id="ab4ff-111">These procedures should also be used if you need tooabandon hello encryption key for any reason.</span></span>

##<a name="issues-that-arise-from-changing-hello-password"></a><span data-ttu-id="ab4ff-112">Problemy, które wynikają z zmiany hasła hello</span><span class="sxs-lookup"><span data-stu-id="ab4ff-112">Issues that arise from changing hello password</span></span>
<span data-ttu-id="ab4ff-113">Istnieją dwie czynności wymagające toobe wykonane po zmianie hello hasło do konta usługi.</span><span class="sxs-lookup"><span data-stu-id="ab4ff-113">There are two things that need toobe done when you change hello service account password.</span></span>

<span data-ttu-id="ab4ff-114">Najpierw należy toochange hello hasło w obszarze hello Menedżera sterowania usługami systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="ab4ff-114">First, you need toochange hello password under hello Windows Service Control Manager.</span></span>  <span data-ttu-id="ab4ff-115">Dopóki ten problem zostanie rozwiązany, zostaną wyświetlone następujące błędy:</span><span class="sxs-lookup"><span data-stu-id="ab4ff-115">Until this issue is resolved you will see following errors:</span></span>


- <span data-ttu-id="ab4ff-116">Jeśli spróbujesz hello toostart usługi synchronizacji w Menedżera sterowania usługami systemu Windows o błędzie hello "**systemu Windows nie można uruchomić usługi Microsoft Azure AD Sync hello na komputerze lokalnym**".</span><span class="sxs-lookup"><span data-stu-id="ab4ff-116">If you try toostart hello Synchronization Service in Windows Service Control Manager, you receive hello error "**Windows could not start hello Microsoft Azure AD Sync service on Local Computer**".</span></span> <span data-ttu-id="ab4ff-117">**Błąd 1069: hello usługa nie została uruchomiona ze względu na błąd logowania tooa.** "</span><span class="sxs-lookup"><span data-stu-id="ab4ff-117">**Error 1069: hello service did not start due tooa logon failure.**"</span></span>
- <span data-ttu-id="ab4ff-118">W Podglądzie zdarzeń systemu Windows, w dzienniku zdarzeń systemowych hello zawiera błąd **7038 identyfikator zdarzenia** i wiadomości "**hello usługi ADSync nie są toolog tak jak w przypadku hello obecnie skonfigurowane hasło powodu toohello następujących błędów: Witaj, nazwa użytkownika lub hasło jest niepoprawne.** "</span><span class="sxs-lookup"><span data-stu-id="ab4ff-118">Under Windows Event Viewer, hello system event log contains an error with **Event ID 7038** and message “**hello ADSync service was unable toolog on as with hello currently configured password due toohello following error: hello user name or password is incorrect.**"</span></span>

<span data-ttu-id="ab4ff-119">Po drugie określonych warunkach, jeśli hasło hello jest aktualizowany, hello usługi synchronizacji można już pobierać hello klucz szyfrowania za pośrednictwem DPAPI.</span><span class="sxs-lookup"><span data-stu-id="ab4ff-119">Second, under specific conditions, if hello password is updated, hello Synchronization Service can no longer retrieve hello encryption key via DPAPI.</span></span> <span data-ttu-id="ab4ff-120">Bez klucza szyfrowania hello powitalne Usługa synchronizacji nie można odszyfrować toosynchronize hello hasła wymagane do i z lokalnej usługi AD i Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ab4ff-120">Without hello encryption key, hello Synchronization Service cannot decrypt hello passwords required toosynchronize to/from on-premises AD and Azure AD.</span></span>
<span data-ttu-id="ab4ff-121">Zostaną wyświetlone błędy takie jak:</span><span class="sxs-lookup"><span data-stu-id="ab4ff-121">You will see errors such as:</span></span>

- <span data-ttu-id="ab4ff-122">W obszarze Menedżer sterowania usługami systemu Windows Jeśli spróbuj hello toostart usługi synchronizacji i nie może pobrać klucza szyfrowania hello go zakończy się niepowodzeniem z powodu błędu "** Windows hello Microsoft Azure AD Sync nie można uruchomić na komputerze lokalnym.</span><span class="sxs-lookup"><span data-stu-id="ab4ff-122">Under Windows Service Control Manager, if you try toostart hello Synchronization Service and it cannot retrieve hello encryption key, it fails with error “**Windows could not start hello Microsoft Azure AD Sync on Local Computer.</span></span> <span data-ttu-id="ab4ff-123">Aby uzyskać więcej informacji przejrzyj dziennik zdarzeń systemowych hello.</span><span class="sxs-lookup"><span data-stu-id="ab4ff-123">For more information, review hello System Event log.</span></span> <span data-ttu-id="ab4ff-124">Jeśli jest to usługa firmy Microsoft, skontaktuj się z dostawcą usługi hello i odwołuje się kod błędu tooservice **-21451857952 ***. "</span><span class="sxs-lookup"><span data-stu-id="ab4ff-124">If this is a non-Microsoft service, contact hello service vendor, and refer tooservice-specific error code **-21451857952****.”</span></span>
- <span data-ttu-id="ab4ff-125">W Podglądzie zdarzeń systemu Windows, w dzienniku zdarzeń aplikacji hello zawiera błąd **6028 identyfikator zdarzenia** i komunikat o błędzie *"**nie można uzyskać dostępu do klucza szyfrowania serwera hello.* *"*</span><span class="sxs-lookup"><span data-stu-id="ab4ff-125">Under Windows Event Viewer, hello application event log contains an error with **Event ID 6028** and error message *“**hello server encryption key cannot be accessed.**”*</span></span>

<span data-ttu-id="ab4ff-126">tooensure nie otrzymasz tych błędów, postępuj zgodnie z procedurami hello w [klucza szyfrowania programu Abandoning hello Azure AD Connect synchronizacji](#abandoning-the-azure-ad-connect-sync-encryption-key) podczas zmiany hasła hello.</span><span class="sxs-lookup"><span data-stu-id="ab4ff-126">tooensure that you do not receive these errors, follow hello procedures in [Abandoning hello Azure AD Connect Sync encryption key](#abandoning-the-azure-ad-connect-sync-encryption-key) when changing hello password.</span></span>
 
## <a name="abandoning-hello-azure-ad-connect-sync-encryption-key"></a><span data-ttu-id="ab4ff-127">Porzucanie klucza szyfrowania hello synchronizacji Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="ab4ff-127">Abandoning hello Azure AD Connect Sync encryption key</span></span>
>[!IMPORTANT]
><span data-ttu-id="ab4ff-128">Witaj następujące procedury mają zastosowanie tylko tooAzure AD Connect kompilacji 1.1.443.0 lub starszy.</span><span class="sxs-lookup"><span data-stu-id="ab4ff-128">hello following procedures only apply tooAzure AD Connect build 1.1.443.0 or older.</span></span>

<span data-ttu-id="ab4ff-129">Użyj powitania po klucz szyfrowania hello tooabandon procedury.</span><span class="sxs-lookup"><span data-stu-id="ab4ff-129">Use hello following procedures tooabandon hello encryption key.</span></span>

### <a name="what-toodo-if-you-need-tooabandon-hello-encryption-key"></a><span data-ttu-id="ab4ff-130">Jakie toodo, aby uzyskać klucz szyfrowania hello tooabandon</span><span class="sxs-lookup"><span data-stu-id="ab4ff-130">What toodo if you need tooabandon hello encryption key</span></span>

<span data-ttu-id="ab4ff-131">Klucz szyfrowania hello tooabandon, należy użyć powitania po tooaccomplish procedury.</span><span class="sxs-lookup"><span data-stu-id="ab4ff-131">If you need tooabandon hello encryption key, use hello following procedures tooaccomplish this.</span></span>

1. [<span data-ttu-id="ab4ff-132">Porzuć hello istniejącego klucza szyfrowania</span><span class="sxs-lookup"><span data-stu-id="ab4ff-132">Abandon hello existing encryption key</span></span>](#abandon-the-existing-encryption-key)

2. [<span data-ttu-id="ab4ff-133">Podaj hasło hello hello konta usług AD DS</span><span class="sxs-lookup"><span data-stu-id="ab4ff-133">Provide hello password of hello AD DS account</span></span>](#provide-the-password-of-the-ad-ds-account)

3. [<span data-ttu-id="ab4ff-134">Zainicjuj ponownie hasło hello hello konta synchronizacji usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="ab4ff-134">Reinitialize hello password of hello Azure AD sync account</span></span>](#reinitialize-the-password-of-the-azure-ad-sync-account)

4. [<span data-ttu-id="ab4ff-135">Uruchom hello usługi synchronizacji</span><span class="sxs-lookup"><span data-stu-id="ab4ff-135">Start hello Synchronization Service</span></span>](#start-the-synchronization-service)

#### <a name="abandon-hello-existing-encryption-key"></a><span data-ttu-id="ab4ff-136">Porzuć hello istniejącego klucza szyfrowania</span><span class="sxs-lookup"><span data-stu-id="ab4ff-136">Abandon hello existing encryption key</span></span>
<span data-ttu-id="ab4ff-137">Porzuć hello istniejącego klucza szyfrowania, więc można utworzyć tego nowego klucza szyfrowania:</span><span class="sxs-lookup"><span data-stu-id="ab4ff-137">Abandon hello existing encryption key so that new encryption key can be created:</span></span>

1. <span data-ttu-id="ab4ff-138">Zaloguj się za tooyour Azure AD Connect serwera jako administrator.</span><span class="sxs-lookup"><span data-stu-id="ab4ff-138">Log in tooyour Azure AD Connect Server as administrator.</span></span>

2. <span data-ttu-id="ab4ff-139">Rozpocznij nową sesję programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ab4ff-139">Start a new PowerShell session.</span></span>

3. <span data-ttu-id="ab4ff-140">Przejdź toofolder:`$env:Program Files\Microsoft Azure AD Sync\bin\`</span><span class="sxs-lookup"><span data-stu-id="ab4ff-140">Navigate toofolder: `$env:Program Files\Microsoft Azure AD Sync\bin\`</span></span>

4. <span data-ttu-id="ab4ff-141">Uruchom polecenie hello:`./miiskmu.exe /a`</span><span class="sxs-lookup"><span data-stu-id="ab4ff-141">Run hello command: `./miiskmu.exe /a`</span></span>

![Narzędzie klucza szyfrowania synchronizacji programu Azure AD Connect](media/active-directory-aadconnectsync-encryption-key/key5.png)

#### <a name="provide-hello-password-of-hello-ad-ds-account"></a><span data-ttu-id="ab4ff-143">Podaj hasło hello hello konta usług AD DS</span><span class="sxs-lookup"><span data-stu-id="ab4ff-143">Provide hello password of hello AD DS account</span></span>
<span data-ttu-id="ab4ff-144">Jak już istniejące hasła hello przechowywany w bazie danych hello mogły być odszyfrowane, należy tooprovide hello usługi synchronizacji z hello hasło konta hello usług AD DS.</span><span class="sxs-lookup"><span data-stu-id="ab4ff-144">As hello existing passwords stored inside hello database can no longer be decrypted, you need tooprovide hello Synchronization Service with hello password of hello AD DS account.</span></span> <span data-ttu-id="ab4ff-145">Witaj usługi synchronizacji szyfruje hello hasła przy użyciu nowego klucza szyfrowania hello:</span><span class="sxs-lookup"><span data-stu-id="ab4ff-145">hello Synchronization Service encrypts hello passwords using hello new encryption key:</span></span>

1. <span data-ttu-id="ab4ff-146">Uruchom hello Synchronization Service Manager (START → usługa synchronizacji).</span><span class="sxs-lookup"><span data-stu-id="ab4ff-146">Start hello Synchronization Service Manager (START → Synchronization Service).</span></span>
</br><span data-ttu-id="ab4ff-147">![Menedżera usługi synchronizacji](./media/active-directory-aadconnectsync-service-manager-ui/startmenu.png)</span><span class="sxs-lookup"><span data-stu-id="ab4ff-147">![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/startmenu.png)</span></span>  
2. <span data-ttu-id="ab4ff-148">Przejdź toohello **łączniki** kartę.</span><span class="sxs-lookup"><span data-stu-id="ab4ff-148">Go toohello **Connectors** tab.</span></span>
3. <span data-ttu-id="ab4ff-149">Wybierz hello **łącznika AD** , który odpowiada tooyour lokalnej usłudze AD.</span><span class="sxs-lookup"><span data-stu-id="ab4ff-149">Select hello **AD Connector** that corresponds tooyour on-premises AD.</span></span> <span data-ttu-id="ab4ff-150">Jeśli masz więcej niż jeden łącznik AD, powtórz hello następujące kroki dla każdego z nich.</span><span class="sxs-lookup"><span data-stu-id="ab4ff-150">If you have more than one AD connector, repeat hello following steps for each of them.</span></span>
4. <span data-ttu-id="ab4ff-151">W obszarze **akcje**, wybierz pozycję **właściwości**.</span><span class="sxs-lookup"><span data-stu-id="ab4ff-151">Under **Actions**, select **Properties**.</span></span>
5. <span data-ttu-id="ab4ff-152">W wyskakującym oknie dialogowym hello, wybierz **Connect lesie katalogu tooActive**:</span><span class="sxs-lookup"><span data-stu-id="ab4ff-152">In hello pop-up dialog, select **Connect tooActive Directory Forest**:</span></span>
6. <span data-ttu-id="ab4ff-153">Wprowadź hasło hello konta hello usług AD DS w hello **hasło** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="ab4ff-153">Enter hello password of hello AD DS account in hello **Password** textbox.</span></span> <span data-ttu-id="ab4ff-154">Jeśli nie znasz swojego hasła, należy ustawić tooa znane wartości przed wykonaniem tej czynności.</span><span class="sxs-lookup"><span data-stu-id="ab4ff-154">If you do not know its password, you must set it tooa known value before performing this step.</span></span>
7. <span data-ttu-id="ab4ff-155">Kliknij przycisk **OK** toosave hello nowe hasło i zamknij hello podręczne okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="ab4ff-155">Click **OK** toosave hello new password and close hello pop-up dialog.</span></span>
<span data-ttu-id="ab4ff-156">![Narzędzie klucza szyfrowania synchronizacji programu Azure AD Connect](media/active-directory-aadconnectsync-encryption-key/key6.png)</span><span class="sxs-lookup"><span data-stu-id="ab4ff-156">![Azure AD Connect Sync Encryption Key Utility](media/active-directory-aadconnectsync-encryption-key/key6.png)</span></span>

#### <a name="reinitialize-hello-password-of-hello-azure-ad-sync-account"></a><span data-ttu-id="ab4ff-157">Zainicjuj ponownie hasło hello hello konta synchronizacji usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="ab4ff-157">Reinitialize hello password of hello Azure AD sync account</span></span>
<span data-ttu-id="ab4ff-158">Nie można bezpośrednio podać hasło hello hello Azure AD service konta toohello usługi synchronizacji.</span><span class="sxs-lookup"><span data-stu-id="ab4ff-158">You cannot directly provide hello password of hello Azure AD service account toohello Synchronization Service.</span></span> <span data-ttu-id="ab4ff-159">Zamiast tego należy polecenia cmdlet hello toouse **ADSyncAADServiceAccount Dodaj** hello tooreinitialize konta usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ab4ff-159">Instead, you need toouse hello cmdlet **Add-ADSyncAADServiceAccount** tooreinitialize hello Azure AD service account.</span></span> <span data-ttu-id="ab4ff-160">polecenia cmdlet Hello resetuje hasło konta hello i ułatwia toohello dostępne usługi synchronizacji:</span><span class="sxs-lookup"><span data-stu-id="ab4ff-160">hello cmdlet resets hello account password and makes it available toohello Synchronization Service:</span></span>

1. <span data-ttu-id="ab4ff-161">Rozpocznij nową sesję programu PowerShell na powitania serwera Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="ab4ff-161">Start a new PowerShell session on hello Azure AD Connect server.</span></span>
2. <span data-ttu-id="ab4ff-162">Uruchom polecenie cmdlet `Add-ADSyncAADServiceAccount`.</span><span class="sxs-lookup"><span data-stu-id="ab4ff-162">Run cmdlet `Add-ADSyncAADServiceAccount`.</span></span>
3. <span data-ttu-id="ab4ff-163">W wyskakującym oknie dialogowym hello Podaj poświadczenia administratora globalnego hello Azure AD dla dzierżawy usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ab4ff-163">In hello pop-up dialog, provide hello Azure AD Global admin credentials for your Azure AD tenant.</span></span>
<span data-ttu-id="ab4ff-164">![Narzędzie klucza szyfrowania synchronizacji programu Azure AD Connect](media/active-directory-aadconnectsync-encryption-key/key7.png)</span><span class="sxs-lookup"><span data-stu-id="ab4ff-164">![Azure AD Connect Sync Encryption Key Utility](media/active-directory-aadconnectsync-encryption-key/key7.png)</span></span>
4. <span data-ttu-id="ab4ff-165">Jeśli ten zakończy się powodzeniem, zostanie wyświetlony wiersz polecenia programu PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="ab4ff-165">If it is successful, you will see hello PowerShell command prompt.</span></span>

#### <a name="start-hello-synchronization-service"></a><span data-ttu-id="ab4ff-166">Uruchom hello usługi synchronizacji</span><span class="sxs-lookup"><span data-stu-id="ab4ff-166">Start hello Synchronization Service</span></span>
<span data-ttu-id="ab4ff-167">Klucz szyfrowania toohello dostępu ma hello usługi synchronizacji i wszystkie hello haseł musi, można ponownie uruchomić usługę hello w hello Menedżera sterowania usługami systemu Windows:</span><span class="sxs-lookup"><span data-stu-id="ab4ff-167">Now that hello Synchronization Service has access toohello encryption key and all hello passwords it needs, you can restart hello service in hello Windows Service Control Manager:</span></span>


1. <span data-ttu-id="ab4ff-168">Przejdź tooWindows Menedżera sterowania usługami (usługi → START).</span><span class="sxs-lookup"><span data-stu-id="ab4ff-168">Go tooWindows Service Control Manager (START → Services).</span></span>
2. <span data-ttu-id="ab4ff-169">Wybierz **Microsoft Azure AD Sync** i kliknij przycisk Uruchom ponownie.</span><span class="sxs-lookup"><span data-stu-id="ab4ff-169">Select **Microsoft Azure AD Sync** and click Restart.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ab4ff-170">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="ab4ff-170">Next steps</span></span>
<span data-ttu-id="ab4ff-171">**Tematy poglądowe**</span><span class="sxs-lookup"><span data-stu-id="ab4ff-171">**Overview topics**</span></span>

* [<span data-ttu-id="ab4ff-172">Synchronizacja programu Azure AD Connect: zrozumienie i dostosowywanie synchronizacji</span><span class="sxs-lookup"><span data-stu-id="ab4ff-172">Azure AD Connect sync: Understand and customize synchronization</span></span>](active-directory-aadconnectsync-whatis.md)

* [<span data-ttu-id="ab4ff-173">Integrowanie tożsamości lokalnych z usługą Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ab4ff-173">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
