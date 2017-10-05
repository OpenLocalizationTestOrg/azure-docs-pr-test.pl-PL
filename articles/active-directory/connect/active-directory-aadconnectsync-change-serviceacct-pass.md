---
title: "Synchronizacja programu Azure AD Connect: Zmiana konta usługi Azure AD Connect synchronizacji | Dokumentacja firmy Microsoft"
description: "Dokument ten temat opisuje oraz klucz szyfrowania został on porzucony po zmianie hasła."
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
ms.openlocfilehash: bf6234d0810f870909957ee1c1e33c225a4922b9
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="changing-the-azure-ad-connect-sync-service-account-password"></a><span data-ttu-id="463d3-104">Zmiana hasła konta usługi synchronizacji Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="463d3-104">Changing the Azure AD Connect sync service account password</span></span>
<span data-ttu-id="463d3-105">Jeśli zmienisz hasło konta usługi synchronizacji Azure AD Connect, usługi synchronizacji nie będzie możliwe start poprawnie dopiero po klucz szyfrowania porzucone i ponownie zainicjować hasło konta usługi synchronizacji Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="463d3-105">If you change the  Azure AD Connect sync service account password, the Synchronization Service will not be able start correctly until you have abandoned the encryption key and reinitialized the Azure AD Connect sync service account password.</span></span> 

<span data-ttu-id="463d3-106">Azure AD Connect, jako część usługi synchronizacji przechowuje klucz szyfrowania hasła kont usługi AD DS i Azure AD.</span><span class="sxs-lookup"><span data-stu-id="463d3-106">Azure AD Connect, as part of the Synchronization Services uses an encryption key to store the passwords of the AD DS and Azure AD service accounts.</span></span>  <span data-ttu-id="463d3-107">Konta te są szyfrowane przed są przechowywane w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="463d3-107">These accounts are encrypted before they are stored in the database.</span></span> 

<span data-ttu-id="463d3-108">Klucz szyfrowania używany jest zabezpieczone przy użyciu [ochrony danych systemu Windows (DPAPI)](https://msdn.microsoft.com/library/ms995355.aspx).</span><span class="sxs-lookup"><span data-stu-id="463d3-108">The encryption key used is secured using [Windows Data Protection (DPAPI)](https://msdn.microsoft.com/library/ms995355.aspx).</span></span> <span data-ttu-id="463d3-109">DPAPI chroni szyfrowania klucza przy użyciu **hasło konta usługi synchronizacji programu Azure AD Connect**.</span><span class="sxs-lookup"><span data-stu-id="463d3-109">DPAPI protects the encryption key using the **password of the Azure AD Connect sync service account**.</span></span> 

<span data-ttu-id="463d3-110">Jeśli musisz zmienić hasło konta usługi można użyć procedury [porzucanie klucz szyfrowania synchronizacji Azure AD Connect](#abandoning-the-azure-ad-connect-sync-encryption-key) w tym celu.</span><span class="sxs-lookup"><span data-stu-id="463d3-110">If you need to change the service account password you can use the procedures in [Abandoning the Azure AD Connect Sync encryption key](#abandoning-the-azure-ad-connect-sync-encryption-key) to accomplish this.</span></span>  <span data-ttu-id="463d3-111">Te procedury należy również Jeśli musisz porzucić klucz szyfrowania dla dowolnej przyczyny.</span><span class="sxs-lookup"><span data-stu-id="463d3-111">These procedures should also be used if you need to abandon the encryption key for any reason.</span></span>

##<a name="issues-that-arise-from-changing-the-password"></a><span data-ttu-id="463d3-112">Problemy, które wynikają z zmiany hasła</span><span class="sxs-lookup"><span data-stu-id="463d3-112">Issues that arise from changing the password</span></span>
<span data-ttu-id="463d3-113">Istnieją dwie czynności, które należy wykonać, gdy zmieniasz hasło konta usługi.</span><span class="sxs-lookup"><span data-stu-id="463d3-113">There are two things that need to be done when you change the service account password.</span></span>

<span data-ttu-id="463d3-114">Najpierw należy zmienić hasło w obszarze Menedżer sterowania usługami systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="463d3-114">First, you need to change the password under the Windows Service Control Manager.</span></span>  <span data-ttu-id="463d3-115">Dopóki ten problem zostanie rozwiązany, zostaną wyświetlone następujące błędy:</span><span class="sxs-lookup"><span data-stu-id="463d3-115">Until this issue is resolved you will see following errors:</span></span>


- <span data-ttu-id="463d3-116">Jeśli użytkownik próbuje uruchomić usługę synchronizacji w Menedżera sterowania usługami systemu Windows, zostanie wyświetlony błąd "**systemu Windows nie można uruchomić usługi Microsoft Azure AD Sync na komputerze lokalnym**".</span><span class="sxs-lookup"><span data-stu-id="463d3-116">If you try to start the Synchronization Service in Windows Service Control Manager, you receive the error "**Windows could not start the Microsoft Azure AD Sync service on Local Computer**".</span></span> <span data-ttu-id="463d3-117">**Błąd 1069: Usługa nie została uruchomiona z powodu niepowodzenia logowania.** "</span><span class="sxs-lookup"><span data-stu-id="463d3-117">**Error 1069: The service did not start due to a logon failure.**"</span></span>
- <span data-ttu-id="463d3-118">W Podglądzie zdarzeń systemu Windows, w dzienniku zdarzeń systemowych zawiera błąd **7038 identyfikator zdarzenia** i komunikatem "**usługi ADSync nie może zalogować się zgodnie z aktualnie skonfigurowanym hasłem z powodu następującego błędu: użytkownik Nazwa lub hasło jest niepoprawne.** "</span><span class="sxs-lookup"><span data-stu-id="463d3-118">Under Windows Event Viewer, the system event log contains an error with **Event ID 7038** and message “**The ADSync service was unable to log on as with the currently configured password due to the following error: The user name or password is incorrect.**"</span></span>

<span data-ttu-id="463d3-119">Drugie określonych warunkach, jeśli hasło zostanie zaktualizowane, usługa synchronizacji można już pobierać klucz szyfrowania za pośrednictwem DPAPI.</span><span class="sxs-lookup"><span data-stu-id="463d3-119">Second, under specific conditions, if the password is updated, the Synchronization Service can no longer retrieve the encryption key via DPAPI.</span></span> <span data-ttu-id="463d3-120">Bez klucza szyfrowania usługi synchronizacji nie można odszyfrować hasła wymagane do synchronizacji z lokalnej usługi AD i Azure AD.</span><span class="sxs-lookup"><span data-stu-id="463d3-120">Without the encryption key, the Synchronization Service cannot decrypt the passwords required to synchronize to/from on-premises AD and Azure AD.</span></span>
<span data-ttu-id="463d3-121">Zostaną wyświetlone błędy takie jak:</span><span class="sxs-lookup"><span data-stu-id="463d3-121">You will see errors such as:</span></span>

- <span data-ttu-id="463d3-122">W obszarze Menedżer sterowania usługami systemu Windows, jeśli użytkownik próbuje uruchomić usługę synchronizacji i nie może pobrać klucza szyfrowania go zakończy się niepowodzeniem z powodu błędu "** systemu Windows nie można uruchomić programu Microsoft Azure AD Sync na komputerze lokalnym.</span><span class="sxs-lookup"><span data-stu-id="463d3-122">Under Windows Service Control Manager, if you try to start the Synchronization Service and it cannot retrieve the encryption key, it fails with error “**Windows could not start the Microsoft Azure AD Sync on Local Computer.</span></span> <span data-ttu-id="463d3-123">Aby uzyskać więcej informacji przejrzyj dziennik zdarzeń systemu.</span><span class="sxs-lookup"><span data-stu-id="463d3-123">For more information, review the System Event log.</span></span> <span data-ttu-id="463d3-124">Jeśli jest to usługa firmy Microsoft, skontaktuj się z dostawcą usługi i zapoznaj się kod błędu usługi **-21451857952 ***. "</span><span class="sxs-lookup"><span data-stu-id="463d3-124">If this is a non-Microsoft service, contact the service vendor, and refer to service-specific error code **-21451857952****.”</span></span>
- <span data-ttu-id="463d3-125">W Podglądzie zdarzeń systemu Windows, w dzienniku zdarzeń aplikacji zawiera błąd **6028 identyfikator zdarzenia** i komunikat o błędzie *"**nie można uzyskać dostępu do klucza szyfrowania serwera.* *"*</span><span class="sxs-lookup"><span data-stu-id="463d3-125">Under Windows Event Viewer, the application event log contains an error with **Event ID 6028** and error message *“**The server encryption key cannot be accessed.**”*</span></span>

<span data-ttu-id="463d3-126">Aby upewnić się, że nie będą odbierać te błędy, wykonaj procedury przedstawione w [porzucanie klucz szyfrowania synchronizacji Azure AD Connect](#abandoning-the-azure-ad-connect-sync-encryption-key) po zmianie hasła.</span><span class="sxs-lookup"><span data-stu-id="463d3-126">To ensure that you do not receive these errors, follow the procedures in [Abandoning the Azure AD Connect Sync encryption key](#abandoning-the-azure-ad-connect-sync-encryption-key) when changing the password.</span></span>
 
## <a name="abandoning-the-azure-ad-connect-sync-encryption-key"></a><span data-ttu-id="463d3-127">Porzucanie klucz szyfrowania synchronizacji Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="463d3-127">Abandoning the Azure AD Connect Sync encryption key</span></span>
>[!IMPORTANT]
><span data-ttu-id="463d3-128">Poniższe procedury dotyczą tylko usługi Azure AD Connect kompilacji 1.1.443.0 lub starszy.</span><span class="sxs-lookup"><span data-stu-id="463d3-128">The following procedures only apply to Azure AD Connect build 1.1.443.0 or older.</span></span>

<span data-ttu-id="463d3-129">Użyj następujących procedur, aby porzucić klucz szyfrowania.</span><span class="sxs-lookup"><span data-stu-id="463d3-129">Use the following procedures to abandon the encryption key.</span></span>

### <a name="what-to-do-if-you-need-to-abandon-the-encryption-key"></a><span data-ttu-id="463d3-130">Co zrobić, jeśli musisz porzucić klucz szyfrowania</span><span class="sxs-lookup"><span data-stu-id="463d3-130">What to do if you need to abandon the encryption key</span></span>

<span data-ttu-id="463d3-131">Jeśli musisz porzucić klucz szyfrowania, w tym celu należy użyć poniższych procedur.</span><span class="sxs-lookup"><span data-stu-id="463d3-131">If you need to abandon the encryption key, use the following procedures to accomplish this.</span></span>

1. [<span data-ttu-id="463d3-132">Porzuć istniejący klucz szyfrowania</span><span class="sxs-lookup"><span data-stu-id="463d3-132">Abandon the existing encryption key</span></span>](#abandon-the-existing-encryption-key)

2. [<span data-ttu-id="463d3-133">Podaj hasło do konta usług AD DS</span><span class="sxs-lookup"><span data-stu-id="463d3-133">Provide the password of the AD DS account</span></span>](#provide-the-password-of-the-ad-ds-account)

3. [<span data-ttu-id="463d3-134">Zainicjuj ponownie hasło do konta synchronizacji usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="463d3-134">Reinitialize the password of the Azure AD sync account</span></span>](#reinitialize-the-password-of-the-azure-ad-sync-account)

4. [<span data-ttu-id="463d3-135">Uruchom usługę synchronizacji</span><span class="sxs-lookup"><span data-stu-id="463d3-135">Start the Synchronization Service</span></span>](#start-the-synchronization-service)

#### <a name="abandon-the-existing-encryption-key"></a><span data-ttu-id="463d3-136">Porzuć istniejący klucz szyfrowania</span><span class="sxs-lookup"><span data-stu-id="463d3-136">Abandon the existing encryption key</span></span>
<span data-ttu-id="463d3-137">Porzuć istniejący klucz szyfrowania, można utworzyć tego nowego klucza szyfrowania:</span><span class="sxs-lookup"><span data-stu-id="463d3-137">Abandon the existing encryption key so that new encryption key can be created:</span></span>

1. <span data-ttu-id="463d3-138">Zaloguj się do usługi Azure AD Connect serwera jako administrator.</span><span class="sxs-lookup"><span data-stu-id="463d3-138">Log in to your Azure AD Connect Server as administrator.</span></span>

2. <span data-ttu-id="463d3-139">Rozpocznij nową sesję programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="463d3-139">Start a new PowerShell session.</span></span>

3. <span data-ttu-id="463d3-140">Przejdź do folderu:`$env:Program Files\Microsoft Azure AD Sync\bin\`</span><span class="sxs-lookup"><span data-stu-id="463d3-140">Navigate to folder: `$env:Program Files\Microsoft Azure AD Sync\bin\`</span></span>

4. <span data-ttu-id="463d3-141">Uruchom polecenie:`./miiskmu.exe /a`</span><span class="sxs-lookup"><span data-stu-id="463d3-141">Run the command: `./miiskmu.exe /a`</span></span>

![Narzędzie klucza szyfrowania synchronizacji programu Azure AD Connect](media/active-directory-aadconnectsync-encryption-key/key5.png)

#### <a name="provide-the-password-of-the-ad-ds-account"></a><span data-ttu-id="463d3-143">Podaj hasło do konta usług AD DS</span><span class="sxs-lookup"><span data-stu-id="463d3-143">Provide the password of the AD DS account</span></span>
<span data-ttu-id="463d3-144">Jak istniejące hasła przechowywane w bazie danych nie można odszyfrować, musisz podać usługi synchronizacji z hasłem konta usług AD DS.</span><span class="sxs-lookup"><span data-stu-id="463d3-144">As the existing passwords stored inside the database can no longer be decrypted, you need to provide the Synchronization Service with the password of the AD DS account.</span></span> <span data-ttu-id="463d3-145">Usługa synchronizacji szyfruje hasła przy użyciu nowego klucza szyfrowania:</span><span class="sxs-lookup"><span data-stu-id="463d3-145">The Synchronization Service encrypts the passwords using the new encryption key:</span></span>

1. <span data-ttu-id="463d3-146">Uruchom Menedżera usługi synchronizacji (usługa synchronizacji → START).</span><span class="sxs-lookup"><span data-stu-id="463d3-146">Start the Synchronization Service Manager (START → Synchronization Service).</span></span>
</br><span data-ttu-id="463d3-147">![Menedżera usługi synchronizacji](./media/active-directory-aadconnectsync-service-manager-ui/startmenu.png)</span><span class="sxs-lookup"><span data-stu-id="463d3-147">![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/startmenu.png)</span></span>  
2. <span data-ttu-id="463d3-148">Przejdź do **łączniki** kartę.</span><span class="sxs-lookup"><span data-stu-id="463d3-148">Go to the **Connectors** tab.</span></span>
3. <span data-ttu-id="463d3-149">Wybierz **łącznika AD** odpowiadający lokalnej usługi AD.</span><span class="sxs-lookup"><span data-stu-id="463d3-149">Select the **AD Connector** that corresponds to your on-premises AD.</span></span> <span data-ttu-id="463d3-150">Jeśli masz więcej niż jeden łącznik AD, powtórz następujące kroki dla każdego z nich.</span><span class="sxs-lookup"><span data-stu-id="463d3-150">If you have more than one AD connector, repeat the following steps for each of them.</span></span>
4. <span data-ttu-id="463d3-151">W obszarze **akcje**, wybierz pozycję **właściwości**.</span><span class="sxs-lookup"><span data-stu-id="463d3-151">Under **Actions**, select **Properties**.</span></span>
5. <span data-ttu-id="463d3-152">W oknie podręcznym wybierz **Połącz z lasu usługi Active Directory**:</span><span class="sxs-lookup"><span data-stu-id="463d3-152">In the pop-up dialog, select **Connect to Active Directory Forest**:</span></span>
6. <span data-ttu-id="463d3-153">Wprowadź hasło do konta usług AD DS w **hasło** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="463d3-153">Enter the password of the AD DS account in the **Password** textbox.</span></span> <span data-ttu-id="463d3-154">Jeśli nie znasz swojego hasła, należy ustawić go do żadnej znanej wartości, przed wykonaniem tej czynności.</span><span class="sxs-lookup"><span data-stu-id="463d3-154">If you do not know its password, you must set it to a known value before performing this step.</span></span>
7. <span data-ttu-id="463d3-155">Kliknij przycisk **OK** Aby zapisać nowe hasło i zamknąć okno podręczne.</span><span class="sxs-lookup"><span data-stu-id="463d3-155">Click **OK** to save the new password and close the pop-up dialog.</span></span>
<span data-ttu-id="463d3-156">![Narzędzie klucza szyfrowania synchronizacji programu Azure AD Connect](media/active-directory-aadconnectsync-encryption-key/key6.png)</span><span class="sxs-lookup"><span data-stu-id="463d3-156">![Azure AD Connect Sync Encryption Key Utility](media/active-directory-aadconnectsync-encryption-key/key6.png)</span></span>

#### <a name="reinitialize-the-password-of-the-azure-ad-sync-account"></a><span data-ttu-id="463d3-157">Zainicjuj ponownie hasło do konta synchronizacji usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="463d3-157">Reinitialize the password of the Azure AD sync account</span></span>
<span data-ttu-id="463d3-158">Nie można bezpośrednio Podaj hasło konta usługi Azure AD do usługi synchronizacji.</span><span class="sxs-lookup"><span data-stu-id="463d3-158">You cannot directly provide the password of the Azure AD service account to the Synchronization Service.</span></span> <span data-ttu-id="463d3-159">Zamiast tego należy użyć polecenia cmdlet **ADSyncAADServiceAccount Dodaj** może ponownie zainicjować konta usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="463d3-159">Instead, you need to use the cmdlet **Add-ADSyncAADServiceAccount** to reinitialize the Azure AD service account.</span></span> <span data-ttu-id="463d3-160">Polecenia cmdlet resetuje hasło do konta i udostępnia usługi synchronizacji:</span><span class="sxs-lookup"><span data-stu-id="463d3-160">The cmdlet resets the account password and makes it available to the Synchronization Service:</span></span>

1. <span data-ttu-id="463d3-161">Rozpocznij nową sesję programu PowerShell na serwerze programu Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="463d3-161">Start a new PowerShell session on the Azure AD Connect server.</span></span>
2. <span data-ttu-id="463d3-162">Uruchom polecenie cmdlet `Add-ADSyncAADServiceAccount`.</span><span class="sxs-lookup"><span data-stu-id="463d3-162">Run cmdlet `Add-ADSyncAADServiceAccount`.</span></span>
3. <span data-ttu-id="463d3-163">W wyskakującym oknie dialogowym podaj poświadczenia administratora globalnego usługi Azure AD dla dzierżawy usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="463d3-163">In the pop-up dialog, provide the Azure AD Global admin credentials for your Azure AD tenant.</span></span>
<span data-ttu-id="463d3-164">![Narzędzie klucza szyfrowania synchronizacji programu Azure AD Connect](media/active-directory-aadconnectsync-encryption-key/key7.png)</span><span class="sxs-lookup"><span data-stu-id="463d3-164">![Azure AD Connect Sync Encryption Key Utility](media/active-directory-aadconnectsync-encryption-key/key7.png)</span></span>
4. <span data-ttu-id="463d3-165">Jeśli ten zakończy się powodzeniem, zostanie wyświetlony wiersz polecenia programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="463d3-165">If it is successful, you will see the PowerShell command prompt.</span></span>

#### <a name="start-the-synchronization-service"></a><span data-ttu-id="463d3-166">Uruchom usługę synchronizacji</span><span class="sxs-lookup"><span data-stu-id="463d3-166">Start the Synchronization Service</span></span>
<span data-ttu-id="463d3-167">Usługa synchronizacji uzyskuje dostęp do klucza szyfrowania i hasła, które są niezbędne, aby uruchomić usługę w Menedżerze sterowania usługami systemu Windows:</span><span class="sxs-lookup"><span data-stu-id="463d3-167">Now that the Synchronization Service has access to the encryption key and all the passwords it needs, you can restart the service in the Windows Service Control Manager:</span></span>


1. <span data-ttu-id="463d3-168">Przejdź do systemu Windows Menedżera sterowania usługami (usługi → START).</span><span class="sxs-lookup"><span data-stu-id="463d3-168">Go to Windows Service Control Manager (START → Services).</span></span>
2. <span data-ttu-id="463d3-169">Wybierz **Microsoft Azure AD Sync** i kliknij przycisk Uruchom ponownie.</span><span class="sxs-lookup"><span data-stu-id="463d3-169">Select **Microsoft Azure AD Sync** and click Restart.</span></span>

## <a name="next-steps"></a><span data-ttu-id="463d3-170">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="463d3-170">Next steps</span></span>
<span data-ttu-id="463d3-171">**Tematy poglądowe**</span><span class="sxs-lookup"><span data-stu-id="463d3-171">**Overview topics**</span></span>

* [<span data-ttu-id="463d3-172">Synchronizacja programu Azure AD Connect: zrozumienie i dostosowywanie synchronizacji</span><span class="sxs-lookup"><span data-stu-id="463d3-172">Azure AD Connect sync: Understand and customize synchronization</span></span>](active-directory-aadconnectsync-whatis.md)

* [<span data-ttu-id="463d3-173">Integrowanie tożsamości lokalnych z usługą Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="463d3-173">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
