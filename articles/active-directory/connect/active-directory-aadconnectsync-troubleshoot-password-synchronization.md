---
title: "Rozwiązywanie problemów z synchronizacją hasła z synchronizacji Azure AD Connect | Dokumentacja firmy Microsoft"
description: "Ten artykuł zawiera informacje dotyczące rozwiązywania problemów z synchronizacją hasła."
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 33fa6a8867764975a57b8727e7705529d1d7506a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="troubleshoot-password-synchronization-with-azure-ad-connect-sync"></a><span data-ttu-id="eb86c-103">Rozwiązywanie problemów z synchronizacją hasła z synchronizacji Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="eb86c-103">Troubleshoot password synchronization with Azure AD Connect sync</span></span>
<span data-ttu-id="eb86c-104">Ten temat zawiera procedurę rozwiązywania problemów z synchronizacją haseł.</span><span class="sxs-lookup"><span data-stu-id="eb86c-104">This topic provides steps for how to troubleshoot issues with password synchronization.</span></span> <span data-ttu-id="eb86c-105">Jeśli nie można zsynchronizować hasła, zgodnie z oczekiwaniami, można dla podzbioru użytkowników lub dla wszystkich użytkowników.</span><span class="sxs-lookup"><span data-stu-id="eb86c-105">If passwords are not synchronizing as expected, it can be either for a subset of users or for all users.</span></span> <span data-ttu-id="eb86c-106">Dla usługi Azure Active Directory (Azure AD) wdrożenia Uzyskuj dostęp do wersji 1.1.524.0 lub później, jest teraz diagnostycznych polecenia cmdlet, które służy do rozwiązywania problemów z synchronizacją hasła:</span><span class="sxs-lookup"><span data-stu-id="eb86c-106">For Azure Active Directory (Azure AD) Connect deployment with version 1.1.524.0 or later, there is now a diagnostic cmdlet that you can use to troubleshoot password synchronization issues:</span></span>

* <span data-ttu-id="eb86c-107">Jeśli masz problem, których hasła nie są zsynchronizowane, zapoznaj się [hasła nie są zsynchronizowane: Rozwiązywanie problemów przy użyciu polecenia cmdlet diagnostycznych](#no-passwords-are-synchronized-troubleshoot-by-using-the-diagnostic-cmdlet) sekcji.</span><span class="sxs-lookup"><span data-stu-id="eb86c-107">If you have an issue where no passwords are synchronized, refer to the [No passwords are synchronized: troubleshoot by using the diagnostic cmdlet](#no-passwords-are-synchronized-troubleshoot-by-using-the-diagnostic-cmdlet) section.</span></span>

* <span data-ttu-id="eb86c-108">Jeśli masz problem z pojedyncze obiekty, zapoznaj się [jeden obiekt nie synchronizuje haseł: Rozwiązywanie problemów przy użyciu polecenia cmdlet diagnostycznych](#one-object-is-not-synchronizing-passwords-troubleshoot-by-using-the-diagnostic-cmdlet) sekcji.</span><span class="sxs-lookup"><span data-stu-id="eb86c-108">If you have an issue with individual objects, refer to the [One object is not synchronizing passwords: troubleshoot by using the diagnostic cmdlet](#one-object-is-not-synchronizing-passwords-troubleshoot-by-using-the-diagnostic-cmdlet) section.</span></span>

<span data-ttu-id="eb86c-109">Dla wcześniejszych wersji programu Azure AD Connect wdrażania:</span><span class="sxs-lookup"><span data-stu-id="eb86c-109">For older versions of Azure AD Connect deployment:</span></span>

* <span data-ttu-id="eb86c-110">Jeśli masz problem, których hasła nie są zsynchronizowane, zapoznaj się [hasła nie są zsynchronizowane: Podręcznik rozwiązywania problemów z](#no-passwords-are-synchronized-manual-troubleshooting-steps) sekcji.</span><span class="sxs-lookup"><span data-stu-id="eb86c-110">If you have an issue where no passwords are synchronized, refer to the [No passwords are synchronized: manual troubleshooting steps](#no-passwords-are-synchronized-manual-troubleshooting-steps) section.</span></span>

* <span data-ttu-id="eb86c-111">Jeśli masz problem z pojedyncze obiekty, zapoznaj się [jeden obiekt nie synchronizuje haseł: Podręcznik rozwiązywania problemów z](#one-object-is-not-synchronizing-passwords-manual-troubleshooting-steps) sekcji.</span><span class="sxs-lookup"><span data-stu-id="eb86c-111">If you have an issue with individual objects, refer to the [One object is not synchronizing passwords: manual troubleshooting steps](#one-object-is-not-synchronizing-passwords-manual-troubleshooting-steps) section.</span></span>

## <a name="no-passwords-are-synchronized-troubleshoot-by-using-the-diagnostic-cmdlet"></a><span data-ttu-id="eb86c-112">Hasła nie są zsynchronizowane: Rozwiązywanie problemów przy użyciu polecenia cmdlet diagnostycznych</span><span class="sxs-lookup"><span data-stu-id="eb86c-112">No passwords are synchronized: troubleshoot by using the diagnostic cmdlet</span></span>
<span data-ttu-id="eb86c-113">Można użyć `Invoke-ADSyncDiagnostics` polecenia cmdlet, aby dowiedzieć się, dlaczego hasła nie są zsynchronizowane.</span><span class="sxs-lookup"><span data-stu-id="eb86c-113">You can use the `Invoke-ADSyncDiagnostics` cmdlet to figure out why no passwords are synchronized.</span></span>

> [!NOTE]
> <span data-ttu-id="eb86c-114">`Invoke-ADSyncDiagnostics` Polecenia cmdlet jest dostępna tylko dla wersji Azure AD Connect 1.1.524.0 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="eb86c-114">The `Invoke-ADSyncDiagnostics` cmdlet is available only for Azure AD Connect version 1.1.524.0 or later.</span></span>

### <a name="run-the-diagnostics-cmdlet"></a><span data-ttu-id="eb86c-115">Uruchom polecenie cmdlet diagnostyki</span><span class="sxs-lookup"><span data-stu-id="eb86c-115">Run the diagnostics cmdlet</span></span>
<span data-ttu-id="eb86c-116">Aby rozwiązać problemy, których hasła nie są zsynchronizowane:</span><span class="sxs-lookup"><span data-stu-id="eb86c-116">To troubleshoot issues where no passwords are synchronized:</span></span>

1. <span data-ttu-id="eb86c-117">Otwórz nową sesję programu Windows PowerShell na serwerze usługi Azure AD Connect z **Uruchom jako Administrator** opcji.</span><span class="sxs-lookup"><span data-stu-id="eb86c-117">Open a new Windows PowerShell session on your Azure AD Connect server with the **Run as Administrator** option.</span></span>

2. <span data-ttu-id="eb86c-118">Uruchom `Set-ExecutionPolicy RemoteSigned` lub `Set-ExecutionPolicy Unrestricted`.</span><span class="sxs-lookup"><span data-stu-id="eb86c-118">Run `Set-ExecutionPolicy RemoteSigned` or `Set-ExecutionPolicy Unrestricted`.</span></span>

3. <span data-ttu-id="eb86c-119">Uruchom polecenie `Import-Module ADSyncDiagnostics`.</span><span class="sxs-lookup"><span data-stu-id="eb86c-119">Run `Import-Module ADSyncDiagnostics`.</span></span>

4. <span data-ttu-id="eb86c-120">Uruchom polecenie `Invoke-ADSyncDiagnostics -PasswordSync`.</span><span class="sxs-lookup"><span data-stu-id="eb86c-120">Run `Invoke-ADSyncDiagnostics -PasswordSync`.</span></span>

### <a name="understand-the-results-of-the-cmdlet"></a><span data-ttu-id="eb86c-121">Zrozumienie wyniki polecenia cmdlet</span><span class="sxs-lookup"><span data-stu-id="eb86c-121">Understand the results of the cmdlet</span></span>
<span data-ttu-id="eb86c-122">Polecenia cmdlet diagnostycznych wykonuje następujące testy:</span><span class="sxs-lookup"><span data-stu-id="eb86c-122">The diagnostic cmdlet performs the following checks:</span></span>

* <span data-ttu-id="eb86c-123">Sprawdza, czy dla dzierżawy usługi Azure AD jest włączona funkcja synchronizacji hasła.</span><span class="sxs-lookup"><span data-stu-id="eb86c-123">Validates that the password synchronization feature is enabled for your Azure AD tenant.</span></span>

* <span data-ttu-id="eb86c-124">Sprawdza, czy serwer Azure AD Connect nie jest w trybie przejściowym.</span><span class="sxs-lookup"><span data-stu-id="eb86c-124">Validates that the Azure AD Connect server is not in staging mode.</span></span>

* <span data-ttu-id="eb86c-125">Dla każdego istniejącego lokalnego łącznika usługi Active Directory (która odnosi się do istniejącego lasu usługi Active Directory):</span><span class="sxs-lookup"><span data-stu-id="eb86c-125">For each existing on-premises Active Directory connector (which corresponds to an existing Active Directory forest):</span></span>

   * <span data-ttu-id="eb86c-126">Sprawdza, czy jest włączona funkcja synchronizacji hasła.</span><span class="sxs-lookup"><span data-stu-id="eb86c-126">Validates that the password synchronization feature is enabled.</span></span>
   
   * <span data-ttu-id="eb86c-127">Wyszukiwanie zdarzeń pulsu synchronizacji haseł w dziennikach zdarzeń aplikacji systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="eb86c-127">Searches for password synchronization heartbeat events in the Windows Application Event logs.</span></span>

   * <span data-ttu-id="eb86c-128">Dla każdej domeny usługi Active Directory, w obszarze łącznik lokalnej usługi Active Directory:</span><span class="sxs-lookup"><span data-stu-id="eb86c-128">For each Active Directory domain under the on-premises Active Directory connector:</span></span>

      * <span data-ttu-id="eb86c-129">Sprawdza, czy domena jest dostępny z serwera usługi Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="eb86c-129">Validates that the domain is reachable from the Azure AD Connect server.</span></span>

      * <span data-ttu-id="eb86c-130">Sprawdza, czy konta usług domenowych w usłudze Active Directory (AD DS), używane przez łącznik lokalnej usługi Active Directory ma prawidłową nazwę użytkownika, hasło i uprawnienia wymagane do synchronizacji haseł.</span><span class="sxs-lookup"><span data-stu-id="eb86c-130">Validates that the Active Directory Domain Services (AD DS) accounts used by the on-premises Active Directory connector has the correct username, password, and permissions required for password synchronization.</span></span>

<span data-ttu-id="eb86c-131">Na poniższym diagramie przedstawiono wyniki polecenia cmdlet dla topologii jednej domenie lokalnej usługi Active Directory:</span><span class="sxs-lookup"><span data-stu-id="eb86c-131">The following diagram illustrates the results of the cmdlet for a single-domain, on-premises Active Directory topology:</span></span>

![Dane wyjściowe diagnostyki dla synchronizacji haseł](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobalgeneral.png)

<span data-ttu-id="eb86c-133">Pozostałej części tej sekcji opisano określonych wyników zwróconych przez polecenie cmdlet i odpowiednie problemy.</span><span class="sxs-lookup"><span data-stu-id="eb86c-133">The rest of this section describes specific results that are returned by the cmdlet and corresponding issues.</span></span>

#### <a name="password-synchronization-feature-isnt-enabled"></a><span data-ttu-id="eb86c-134">Funkcja synchronizacji hasła nie jest włączona.</span><span class="sxs-lookup"><span data-stu-id="eb86c-134">Password synchronization feature isn't enabled</span></span>
<span data-ttu-id="eb86c-135">Jeśli nie włączono synchronizacji haseł za pomocą Kreatora programu Azure AD Connect, jest zwracany następujący błąd:</span><span class="sxs-lookup"><span data-stu-id="eb86c-135">If you haven't enabled password synchronization by using the Azure AD Connect wizard, the following error is returned:</span></span>

![Synchronizacja haseł nie jest włączona.](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobaldisabled.png)

#### <a name="azure-ad-connect-server-is-in-staging-mode"></a><span data-ttu-id="eb86c-137">Serwer systemu Azure AD Connect jest w trybie przejściowym</span><span class="sxs-lookup"><span data-stu-id="eb86c-137">Azure AD Connect server is in staging mode</span></span>
<span data-ttu-id="eb86c-138">Jeśli serwer usługi Azure AD Connect jest w trybie przejściowym, synchronizacja haseł jest tymczasowo wyłączona i zwrócony następujący błąd:</span><span class="sxs-lookup"><span data-stu-id="eb86c-138">If the Azure AD Connect server is in staging mode, password synchronization is temporarily disabled, and the following error is returned:</span></span>

![Serwer systemu Azure AD Connect jest w trybie przejściowym](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobalstaging.png)

#### <a name="no-password-synchronization-heartbeat-events"></a><span data-ttu-id="eb86c-140">Brak zdarzeń pulsu synchronizacji haseł</span><span class="sxs-lookup"><span data-stu-id="eb86c-140">No password synchronization heartbeat events</span></span>
<span data-ttu-id="eb86c-141">Każdy łącznik usługi Active Directory lokalnego ma własną kanału synchronizacji haseł.</span><span class="sxs-lookup"><span data-stu-id="eb86c-141">Each on-premises Active Directory connector has its own password synchronization channel.</span></span> <span data-ttu-id="eb86c-142">Po ustanowieniu kanału synchronizacji haseł i nie ma zmiany hasła mają być synchronizowane, co 30 minut w dzienniku zdarzeń aplikacji systemu Windows zostanie wygenerowane zdarzenie pulsu (identyfikator EventId 654).</span><span class="sxs-lookup"><span data-stu-id="eb86c-142">When the password synchronization channel is established and there aren't any password changes to be synchronized, a heartbeat event (EventId 654) is generated once every 30 minutes under the Windows Application Event Log.</span></span> <span data-ttu-id="eb86c-143">Dla każdego lokalnego łącznika usługi Active Directory polecenie cmdlet wyszukuje, poszukaj pokrewnych zdarzeń pulsu w ciągu ostatnich trzech godzin.</span><span class="sxs-lookup"><span data-stu-id="eb86c-143">For each on-premises Active Directory connector, the cmdlet searches for corresponding heartbeat events in the past three hours.</span></span> <span data-ttu-id="eb86c-144">Jeśli żadne zdarzenie pulsu zostanie znaleziony, jest zwracany następujący błąd:</span><span class="sxs-lookup"><span data-stu-id="eb86c-144">If no heartbeat event is found, the following error is returned:</span></span>

![Nie pulsu synchronizacji haseł Ci zdarzeń](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobalnoheartbeat.png)

#### <a name="ad-ds-account-does-not-have-correct-permissions"></a><span data-ttu-id="eb86c-146">Usługi AD DS konto nie ma odpowiednich uprawnień</span><span class="sxs-lookup"><span data-stu-id="eb86c-146">AD DS account does not have correct permissions</span></span>
<span data-ttu-id="eb86c-147">Jeśli konto usług AD DS, które jest używane przez łącznik lokalnej usługi Active Directory do synchronizacji skrótów haseł nie ma odpowiednich uprawnień, jest zwracany następujący błąd:</span><span class="sxs-lookup"><span data-stu-id="eb86c-147">If the AD DS account that's used by the on-premises Active Directory connector to synchronize password hashes does not have the appropriate permissions, the following error is returned:</span></span>

![Nieprawidłowe poświadczenia](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobalaccountincorrectpermission.png)

#### <a name="incorrect-ad-ds-account-username-or-password"></a><span data-ttu-id="eb86c-149">Nieprawidłowa nazwa użytkownika konta usług AD DS lub hasło</span><span class="sxs-lookup"><span data-stu-id="eb86c-149">Incorrect AD DS account username or password</span></span>
<span data-ttu-id="eb86c-150">Jeśli konto usług AD DS używany przez łącznik lokalnej usługi Active Directory do synchronizacji skrótów haseł ma nieprawidłową nazwą użytkownika lub hasło, jest zwracany następujący błąd:</span><span class="sxs-lookup"><span data-stu-id="eb86c-150">If the AD DS account used by the on-premises Active Directory connector to synchronize password hashes has an incorrect username or password, the following error is returned:</span></span>

![Nieprawidłowe poświadczenia](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobalaccountincorrectcredential.png)

## <a name="one-object-is-not-synchronizing-passwords-troubleshoot-by-using-the-diagnostic-cmdlet"></a><span data-ttu-id="eb86c-152">Jeden obiekt nie synchronizuje haseł: Rozwiązywanie problemów przy użyciu polecenia cmdlet diagnostycznych</span><span class="sxs-lookup"><span data-stu-id="eb86c-152">One object is not synchronizing passwords: troubleshoot by using the diagnostic cmdlet</span></span>
<span data-ttu-id="eb86c-153">Można użyć `Invoke-ADSyncDiagnostics` polecenia cmdlet, aby ustalić, dlaczego jeden obiekt nie synchronizuje haseł.</span><span class="sxs-lookup"><span data-stu-id="eb86c-153">You can use the `Invoke-ADSyncDiagnostics` cmdlet to determine why one object is not synchronizing passwords.</span></span>

> [!NOTE]
> <span data-ttu-id="eb86c-154">`Invoke-ADSyncDiagnostics` Polecenia cmdlet jest dostępna tylko dla wersji Azure AD Connect 1.1.524.0 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="eb86c-154">The `Invoke-ADSyncDiagnostics` cmdlet is available only for Azure AD Connect version 1.1.524.0 or later.</span></span>

### <a name="run-the-diagnostics-cmdlet"></a><span data-ttu-id="eb86c-155">Uruchom polecenie cmdlet diagnostyki</span><span class="sxs-lookup"><span data-stu-id="eb86c-155">Run the diagnostics cmdlet</span></span>
<span data-ttu-id="eb86c-156">Aby rozwiązać problemy, których hasła nie są zsynchronizowane:</span><span class="sxs-lookup"><span data-stu-id="eb86c-156">To troubleshoot issues where no passwords are synchronized:</span></span>

1. <span data-ttu-id="eb86c-157">Otwórz nową sesję programu Windows PowerShell na serwerze usługi Azure AD Connect z **Uruchom jako Administrator** opcji.</span><span class="sxs-lookup"><span data-stu-id="eb86c-157">Open a new Windows PowerShell session on your Azure AD Connect server with the **Run as Administrator** option.</span></span>

2. <span data-ttu-id="eb86c-158">Uruchom `Set-ExecutionPolicy RemoteSigned` lub `Set-ExecutionPolicy Unrestricted`.</span><span class="sxs-lookup"><span data-stu-id="eb86c-158">Run `Set-ExecutionPolicy RemoteSigned` or `Set-ExecutionPolicy Unrestricted`.</span></span>

3. <span data-ttu-id="eb86c-159">Uruchom polecenie `Import-Module ADSyncDiagnostics`.</span><span class="sxs-lookup"><span data-stu-id="eb86c-159">Run `Import-Module ADSyncDiagnostics`.</span></span>

4. <span data-ttu-id="eb86c-160">Uruchom następujące polecenie cmdlet:</span><span class="sxs-lookup"><span data-stu-id="eb86c-160">Run the following cmdlet:</span></span>
   ```
   Invoke-ADSyncDiagnostics -PasswordSync -ADConnectorName <Name-of-AD-Connector> -DistinguishedName <DistinguishedName-of-AD-object>
   ```
   <span data-ttu-id="eb86c-161">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="eb86c-161">For example:</span></span>
   ```
   Invoke-ADSyncDiagnostics -PasswordSync -ADConnectorName "contoso.com" -DistinguishedName "CN=TestUserCN=Users,DC=contoso,DC=com"
   ```

### <a name="understand-the-results-of-the-cmdlet"></a><span data-ttu-id="eb86c-162">Zrozumienie wyniki polecenia cmdlet</span><span class="sxs-lookup"><span data-stu-id="eb86c-162">Understand the results of the cmdlet</span></span>
<span data-ttu-id="eb86c-163">Polecenia cmdlet diagnostycznych wykonuje następujące testy:</span><span class="sxs-lookup"><span data-stu-id="eb86c-163">The diagnostic cmdlet performs the following checks:</span></span>

* <span data-ttu-id="eb86c-164">Sprawdza stan obiektu usługi Active Directory w przestrzeni łącznika usługi Active Directory, Metaverse i Azure AD przestrzeni łącznika.</span><span class="sxs-lookup"><span data-stu-id="eb86c-164">Examines the state of the Active Directory object in the Active Directory connector space, Metaverse, and Azure AD connector space.</span></span>

* <span data-ttu-id="eb86c-165">Sprawdza, czy są reguły synchronizacji z synchronizacją haseł włączone i zastosowane do obiektu usługi Active Directory.</span><span class="sxs-lookup"><span data-stu-id="eb86c-165">Validates that there are synchronization rules with password synchronization enabled and applied to the Active Directory object.</span></span>

* <span data-ttu-id="eb86c-166">Próbuje pobrać i wyświetlić wyniki ostatniej próby synchronizacji haseł dla obiekt.</span><span class="sxs-lookup"><span data-stu-id="eb86c-166">Attempts to retrieve and display the results of the last attempt to synchronize the password for the object.</span></span>

<span data-ttu-id="eb86c-167">Na poniższym diagramie przedstawiono wyniki polecenia cmdlet podczas rozwiązywania problemów z synchronizacji haseł dla pojedynczego obiektu:</span><span class="sxs-lookup"><span data-stu-id="eb86c-167">The following diagram illustrates the results of the cmdlet when troubleshooting password synchronization for a single object:</span></span>

![Dane wyjściowe diagnostyki dla synchronizacji haseł — pojedynczy obiekt](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phssingleobjectgeneral.png)

<span data-ttu-id="eb86c-169">Pozostałej części tej sekcji opisano określonych wyników zwróconych przez polecenie cmdlet i odpowiednie problemy.</span><span class="sxs-lookup"><span data-stu-id="eb86c-169">The rest of this section describes specific results returned by the cmdlet and corresponding issues.</span></span>

#### <a name="the-active-directory-object-isnt-exported-to-azure-ad"></a><span data-ttu-id="eb86c-170">Obiekt usługi Active Directory nie jest eksportowane do usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="eb86c-170">The Active Directory object isn't exported to Azure AD</span></span>
<span data-ttu-id="eb86c-171">Synchronizacja haseł dla tego konta usługi Active Directory lokalnego kończy się niepowodzeniem, ponieważ nie ma odpowiedniego obiektu w dzierżawie usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="eb86c-171">Password synchronization for this on-premises Active Directory account fails because there is no corresponding object in the Azure AD tenant.</span></span> <span data-ttu-id="eb86c-172">Zwrócono następujący błąd:</span><span class="sxs-lookup"><span data-stu-id="eb86c-172">The following error is returned:</span></span>

![Brak obiektu usługi Active Directory systemu Azure](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phssingleobjectnotexported.png)

#### <a name="user-has-a-temporary-password"></a><span data-ttu-id="eb86c-174">Użytkownik ma hasło tymczasowe</span><span class="sxs-lookup"><span data-stu-id="eb86c-174">User has a temporary password</span></span>
<span data-ttu-id="eb86c-175">Azure AD Connect nie obsługuje obecnie synchronizowanie tymczasowego hasła z usługą Azure AD.</span><span class="sxs-lookup"><span data-stu-id="eb86c-175">Currently, Azure AD Connect does not support synchronizing temporary passwords with Azure AD.</span></span> <span data-ttu-id="eb86c-176">Hasło jest traktowany jako tymczasowy Jeśli **zmienić hasło przy następnym logowaniu** opcja jest ustawiona na lokalnych użytkowników usługi Active Directory.</span><span class="sxs-lookup"><span data-stu-id="eb86c-176">A password is considered to be temporary if the **Change password at next logon** option is set on the on-premises Active Directory user.</span></span> <span data-ttu-id="eb86c-177">Zwrócono następujący błąd:</span><span class="sxs-lookup"><span data-stu-id="eb86c-177">The following error is returned:</span></span>

![Hasło tymczasowe nie są eksportowane.](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phssingleobjecttemporarypassword.png)

#### <a name="results-of-last-attempt-to-synchronize-password-arent-available"></a><span data-ttu-id="eb86c-179">Wyniki ostatniej próby synchronizacji haseł nie są dostępne</span><span class="sxs-lookup"><span data-stu-id="eb86c-179">Results of last attempt to synchronize password aren't available</span></span>
<span data-ttu-id="eb86c-180">Domyślnie program Azure AD Connect przechowuje liczbę prób synchronizacji haseł na siedem dni.</span><span class="sxs-lookup"><span data-stu-id="eb86c-180">By default, Azure AD Connect stores the results of password synchronization attempts for seven days.</span></span> <span data-ttu-id="eb86c-181">Jeśli nie są dostępne dla wybranego obiektu usługi Active Directory wyniki, zwracany jest następujące ostrzeżenie:</span><span class="sxs-lookup"><span data-stu-id="eb86c-181">If there are no results available for the selected Active Directory object, the following warning is returned:</span></span>

![Dane wyjściowe diagnostyki dla pojedynczego obiektu — nie historii synchronizacji haseł](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phssingleobjectnohistory.png)


## <a name="no-passwords-are-synchronized-manual-troubleshooting-steps"></a><span data-ttu-id="eb86c-183">Hasła nie są zsynchronizowane: ręczne kroki rozwiązywania problemów</span><span class="sxs-lookup"><span data-stu-id="eb86c-183">No passwords are synchronized: manual troubleshooting steps</span></span>
<span data-ttu-id="eb86c-184">Wykonaj następujące kroki, aby ustalić, dlaczego hasła nie są zsynchronizowane:</span><span class="sxs-lookup"><span data-stu-id="eb86c-184">Follow these steps to determine why no passwords are synchronized:</span></span>

1. <span data-ttu-id="eb86c-185">Jest to serwer Connect w [Tryb przejściowy](active-directory-aadconnectsync-operations.md#staging-mode)?</span><span class="sxs-lookup"><span data-stu-id="eb86c-185">Is the Connect server in [staging mode](active-directory-aadconnectsync-operations.md#staging-mode)?</span></span> <span data-ttu-id="eb86c-186">Serwer w trybie przejściowym nie synchronizować hasła.</span><span class="sxs-lookup"><span data-stu-id="eb86c-186">A server in staging mode does not synchronize any passwords.</span></span>

2. <span data-ttu-id="eb86c-187">Uruchom skrypt w [Pobierz stan ustawienia synchronizacji haseł](#get-the-status-of-password-sync-settings) sekcji.</span><span class="sxs-lookup"><span data-stu-id="eb86c-187">Run the script in the [Get the status of password sync settings](#get-the-status-of-password-sync-settings) section.</span></span> <span data-ttu-id="eb86c-188">Udostępnia przegląd konfiguracji synchronizacji haseł.</span><span class="sxs-lookup"><span data-stu-id="eb86c-188">It gives you an overview of the password sync configuration.</span></span>  

    ![Dane wyjściowe skryptu programu PowerShell z ustawień synchronizacji haseł](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/psverifyconfig.png)  

3. <span data-ttu-id="eb86c-190">Jeśli funkcja nie jest włączona w usłudze Azure AD lub stan kanału synchronizacji nie jest włączona, należy uruchomić Kreatora instalacji Connect.</span><span class="sxs-lookup"><span data-stu-id="eb86c-190">If the feature is not enabled in Azure AD or if the sync channel status is not enabled, run the Connect installation wizard.</span></span> <span data-ttu-id="eb86c-191">Wybierz **Dostosuj opcje synchronizacji**i usuń zaznaczenie pozycji synchronizacji haseł. Ta zmiana tymczasowo wyłącza funkcję.</span><span class="sxs-lookup"><span data-stu-id="eb86c-191">Select **Customize synchronization options**, and unselect password sync. This change temporarily disables the feature.</span></span> <span data-ttu-id="eb86c-192">Następnie uruchom ponownie kreatora i ponownie włączyć synchronizację haseł. Uruchom skrypt ponownie, aby sprawdzić, czy konfiguracja jest poprawna.</span><span class="sxs-lookup"><span data-stu-id="eb86c-192">Then run the wizard again and re-enable password sync. Run the script again to verify that the configuration is correct.</span></span>

4. <span data-ttu-id="eb86c-193">Poszukaj w dzienniku błędów.</span><span class="sxs-lookup"><span data-stu-id="eb86c-193">Look in the event log for errors.</span></span> <span data-ttu-id="eb86c-194">Poszukaj następujących zdarzeń, które wskazują problem:</span><span class="sxs-lookup"><span data-stu-id="eb86c-194">Look for the following events, which would indicate a problem:</span></span>
    * <span data-ttu-id="eb86c-195">Źródła: Identyfikator "Synchronizacji katalogów": 0, 611, 652, 655, jeśli te zdarzenia są widoczne masz problem z połączeniem.</span><span class="sxs-lookup"><span data-stu-id="eb86c-195">Source: "Directory synchronization" ID: 0, 611, 652, 655 If you see these events, you have a connectivity problem.</span></span> <span data-ttu-id="eb86c-196">Komunikat dziennika zdarzeń zawiera informacje lasu, gdzie występuje problem.</span><span class="sxs-lookup"><span data-stu-id="eb86c-196">The event log message contains forest information where you have a problem.</span></span> <span data-ttu-id="eb86c-197">Aby uzyskać więcej informacji, zobacz [problem z łącznością](#connectivity problem).</span><span class="sxs-lookup"><span data-stu-id="eb86c-197">For more information, see [Connectivity problem](#connectivity problem).</span></span>

5. <span data-ttu-id="eb86c-198">Jeśli widzisz Brak pulsu lub pracuje zaczynającego, uruchom [wyzwolenia pełnej synchronizacji haseł wszystkich](#trigger-a-full-sync-of-all-passwords).</span><span class="sxs-lookup"><span data-stu-id="eb86c-198">If you see no heartbeat or if nothing else worked, run [Trigger a full sync of all passwords](#trigger-a-full-sync-of-all-passwords).</span></span> <span data-ttu-id="eb86c-199">Uruchom skrypt tylko raz.</span><span class="sxs-lookup"><span data-stu-id="eb86c-199">Run the script only once.</span></span>

6. <span data-ttu-id="eb86c-200">Zobacz [Rozwiązywanie problemów z jednego obiektu, który nie jest synchronizowanie haseł](#one-object-is-not-synchronizing-passwords) sekcji.</span><span class="sxs-lookup"><span data-stu-id="eb86c-200">See the [Troubleshoot one object that is not synchronizing passwords](#one-object-is-not-synchronizing-passwords) section.</span></span>

### <a name="connectivity-problems"></a><span data-ttu-id="eb86c-201">Problemy z łącznością</span><span class="sxs-lookup"><span data-stu-id="eb86c-201">Connectivity problems</span></span>

<span data-ttu-id="eb86c-202">Czy masz połączenie z usługą Azure AD?</span><span class="sxs-lookup"><span data-stu-id="eb86c-202">Do you have connectivity with Azure AD?</span></span>

<span data-ttu-id="eb86c-203">Czy konto ma wymagane uprawnienia do odczytu skrótów haseł we wszystkich domenach?</span><span class="sxs-lookup"><span data-stu-id="eb86c-203">Does the account have required permissions to read the password hashes in all domains?</span></span> <span data-ttu-id="eb86c-204">Jeśli zainstalowano Połącz przy użyciu ustawień ekspresowych, uprawnienia powinny już być poprawne.</span><span class="sxs-lookup"><span data-stu-id="eb86c-204">If you installed Connect by using Express settings, the permissions should already be correct.</span></span> 

<span data-ttu-id="eb86c-205">Jeśli używasz niestandardowej instalacji, należy ręcznie ustawić uprawnienia w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="eb86c-205">If you used custom installation, set the permissions manually by doing the following:</span></span>
    
1. <span data-ttu-id="eb86c-206">Aby znaleźć konto używane przez łącznik usługi Active Directory, należy uruchomić **Menedżera usługi synchronizacji**.</span><span class="sxs-lookup"><span data-stu-id="eb86c-206">To find the account used by the Active Directory connector, start **Synchronization Service Manager**.</span></span> 
 
2. <span data-ttu-id="eb86c-207">Przejdź do **łączniki**, a następnie wyszukaj lokalnego lasu usługi Active Directory, rozwiązywania problemów.</span><span class="sxs-lookup"><span data-stu-id="eb86c-207">Go to **Connectors**, and then search for the on-premises Active Directory forest you are troubleshooting.</span></span> 
 
3. <span data-ttu-id="eb86c-208">Wybierz łącznik, a następnie kliknij przycisk **właściwości**.</span><span class="sxs-lookup"><span data-stu-id="eb86c-208">Select the connector, and then click **Properties**.</span></span> 
 
4. <span data-ttu-id="eb86c-209">Przejdź do **nawiązać połączenia z lasu usługi Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="eb86c-209">Go to **Connect to Active Directory Forest**.</span></span>  
    
    ![Konto używane przez łącznik usługi Active Directory](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/connectoraccount.png)  
    <span data-ttu-id="eb86c-211">Zanotuj nazwę użytkownika i domeny, w której znajduje się konto.</span><span class="sxs-lookup"><span data-stu-id="eb86c-211">Note the username and the domain where the account is located.</span></span>
    
5. <span data-ttu-id="eb86c-212">Uruchom **użytkownicy usługi Active Directory i komputery**, a następnie sprawdź, czy konto, aby odnaleźć wcześniej ma uprawnienia wykonaj ustawiony w katalogu głównym wszystkich domen w lesie:</span><span class="sxs-lookup"><span data-stu-id="eb86c-212">Start **Active Directory Users and Computers**, and then verify that the account you found earlier has the follow permissions set at the root of all domains in your forest:</span></span>
    * <span data-ttu-id="eb86c-213">Replikować zmiany katalogu</span><span class="sxs-lookup"><span data-stu-id="eb86c-213">Replicate Directory Changes</span></span>
    * <span data-ttu-id="eb86c-214">Replikowanie katalogu zmienia wszystkie</span><span class="sxs-lookup"><span data-stu-id="eb86c-214">Replicate Directory Changes All</span></span>

6. <span data-ttu-id="eb86c-215">Kontrolery domeny są osiągalne Azure AD Connect?</span><span class="sxs-lookup"><span data-stu-id="eb86c-215">Are the domain controllers reachable by Azure AD Connect?</span></span> <span data-ttu-id="eb86c-216">Jeśli serwer Connect nie może połączyć do wszystkich kontrolerów domeny, należy skonfigurować **tylko Użyj preferowanego kontrolera domeny**.</span><span class="sxs-lookup"><span data-stu-id="eb86c-216">If the Connect server cannot connect to all domain controllers, configure **Only use preferred domain controller**.</span></span>  
    
    ![Kontroler domeny jest używany przez łącznik usługi Active Directory](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/preferreddc.png)  
    
7. <span data-ttu-id="eb86c-218">Wróć do **Menedżera usługi synchronizacji** i **Konfigurowanie partycji katalogu**.</span><span class="sxs-lookup"><span data-stu-id="eb86c-218">Go back to **Synchronization Service Manager** and **Configure Directory Partition**.</span></span> 
 
8. <span data-ttu-id="eb86c-219">Wybierz domenę w **Wybieranie partycji katalogu**, wybierz pozycję **korzystają z kontrolerów domeny preferowanych** pole wyboru, a następnie kliknij przycisk **Konfiguruj**.</span><span class="sxs-lookup"><span data-stu-id="eb86c-219">Select your domain in **Select directory partitions**, select the **Only use preferred domain controllers** check box, and then click **Configure**.</span></span> 

9. <span data-ttu-id="eb86c-220">Na liście wprowadź kontrolerów domeny, które mają zostać użyte Connect do celów synchronizacji haseł. Tę samą listę służy do importowania i eksportowania również.</span><span class="sxs-lookup"><span data-stu-id="eb86c-220">In the list, enter the domain controllers that Connect should use for password sync. The same list is used for import and export as well.</span></span> <span data-ttu-id="eb86c-221">Wykonaj te kroki dla wszystkich domen.</span><span class="sxs-lookup"><span data-stu-id="eb86c-221">Do these steps for all your domains.</span></span>

10. <span data-ttu-id="eb86c-222">Jeśli skrypt pokazuje, że nie pulsu, uruchom skrypt [wyzwolenia pełnej synchronizacji haseł wszystkich](#trigger-a-full-sync-of-all-passwords).</span><span class="sxs-lookup"><span data-stu-id="eb86c-222">If the script shows that there is no heartbeat, run the script in [Trigger a full sync of all passwords](#trigger-a-full-sync-of-all-passwords).</span></span>

## <a name="one-object-is-not-synchronizing-passwords-manual-troubleshooting-steps"></a><span data-ttu-id="eb86c-223">Jeden obiekt nie synchronizuje haseł: ręczne kroki rozwiązywania problemów</span><span class="sxs-lookup"><span data-stu-id="eb86c-223">One object is not synchronizing passwords: manual troubleshooting steps</span></span>
<span data-ttu-id="eb86c-224">Umożliwia łatwe rozwiązywanie problemów z synchronizacją hasła, przeglądając stanu obiektu.</span><span class="sxs-lookup"><span data-stu-id="eb86c-224">You can easily troubleshoot password synchronization issues by reviewing the status of an object.</span></span>

1. <span data-ttu-id="eb86c-225">W **użytkownicy usługi Active Directory i komputery**, Wyszukaj użytkownika, a następnie sprawdź, czy **użytkownik musi zmienić hasło przy następnym logowaniu** pole wyboru jest wyczyszczone.</span><span class="sxs-lookup"><span data-stu-id="eb86c-225">In **Active Directory Users and Computers**, search for the user, and then verify that the **User must change password at next logon** check box is cleared.</span></span>  

    ![Active Directory produktywności hasła.](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/adprodpassword.png)  

    <span data-ttu-id="eb86c-227">Jeśli pole wyboru jest zaznaczone, należy poprosić użytkownika o zalogować się i zmienić hasło.</span><span class="sxs-lookup"><span data-stu-id="eb86c-227">If the check box is selected, ask the user to sign in and change the password.</span></span> <span data-ttu-id="eb86c-228">Tymczasowe hasła nie są zsynchronizowane z usługą Azure AD.</span><span class="sxs-lookup"><span data-stu-id="eb86c-228">Temporary passwords are not synchronized with Azure AD.</span></span>

2. <span data-ttu-id="eb86c-229">Jeśli hasło jest prawidłowe w usłudze Active Directory, należy wykonać użytkownika aparatu synchronizacji.</span><span class="sxs-lookup"><span data-stu-id="eb86c-229">If the password looks correct in Active Directory, follow the user in the sync engine.</span></span> <span data-ttu-id="eb86c-230">Przez użytkownika z lokalnej usługi Active Directory do usługi Azure AD, można sprawdzić, czy w obiekcie jest opisem błędu.</span><span class="sxs-lookup"><span data-stu-id="eb86c-230">By following the user from on-premises Active Directory to Azure AD, you can see whether there is a descriptive error on the object.</span></span>

    <span data-ttu-id="eb86c-231">a.</span><span class="sxs-lookup"><span data-stu-id="eb86c-231">a.</span></span> <span data-ttu-id="eb86c-232">Uruchom [Menedżera usługi synchronizacji](active-directory-aadconnectsync-service-manager-ui.md).</span><span class="sxs-lookup"><span data-stu-id="eb86c-232">Start the [Synchronization Service Manager](active-directory-aadconnectsync-service-manager-ui.md).</span></span>

    <span data-ttu-id="eb86c-233">b.</span><span class="sxs-lookup"><span data-stu-id="eb86c-233">b.</span></span> <span data-ttu-id="eb86c-234">Kliknij przycisk **łączniki**.</span><span class="sxs-lookup"><span data-stu-id="eb86c-234">Click **Connectors**.</span></span>

    <span data-ttu-id="eb86c-235">c.</span><span class="sxs-lookup"><span data-stu-id="eb86c-235">c.</span></span> <span data-ttu-id="eb86c-236">Wybierz **łącznika usługi Active Directory** gdzie znajduje się użytkownik.</span><span class="sxs-lookup"><span data-stu-id="eb86c-236">Select the **Active Directory Connector** where the user is located.</span></span>

    <span data-ttu-id="eb86c-237">d.</span><span class="sxs-lookup"><span data-stu-id="eb86c-237">d.</span></span> <span data-ttu-id="eb86c-238">Wybierz **wyszukiwania przestrzeni łącznika**.</span><span class="sxs-lookup"><span data-stu-id="eb86c-238">Select **Search Connector Space**.</span></span>

    <span data-ttu-id="eb86c-239">e.</span><span class="sxs-lookup"><span data-stu-id="eb86c-239">e.</span></span> <span data-ttu-id="eb86c-240">W **zakres** wybierz opcję **nazwa Wyróżniająca lub zakotwiczenia**, a następnie wprowadź pełną nazwę Wyświetlaną użytkownika, rozwiązywania problemów.</span><span class="sxs-lookup"><span data-stu-id="eb86c-240">In the **Scope** box, select **DN or Anchor**, and then enter the full DN of the user you are troubleshooting.</span></span>

    ![Wyszukaj użytkownika w przestrzeni łącznika o nazwie Wyróżniającej](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/searchcs.png)  

    <span data-ttu-id="eb86c-242">f.</span><span class="sxs-lookup"><span data-stu-id="eb86c-242">f.</span></span> <span data-ttu-id="eb86c-243">Użytkownik chce się dowiedzieć, a następnie kliknij przycisk Znajdź **właściwości** aby zobaczyć wszystkie atrybuty.</span><span class="sxs-lookup"><span data-stu-id="eb86c-243">Locate the user you are looking for, and then click **Properties** to see all the attributes.</span></span> <span data-ttu-id="eb86c-244">Jeśli użytkownik nie jest w wynikach wyszukiwania, upewnij się, Twoje [reguły filtrowania](active-directory-aadconnectsync-configure-filtering.md) i upewnij się, że uruchamiasz [Zastosuj i Sprawdź zmiany](active-directory-aadconnectsync-configure-filtering.md#apply-and-verify-changes) dla użytkownika, które mają być widoczne w Connect.</span><span class="sxs-lookup"><span data-stu-id="eb86c-244">If the user is not in the search result, verify your [filtering rules](active-directory-aadconnectsync-configure-filtering.md) and make sure that you run [Apply and verify changes](active-directory-aadconnectsync-configure-filtering.md#apply-and-verify-changes) for the user to appear in Connect.</span></span>

    <span data-ttu-id="eb86c-245">g.</span><span class="sxs-lookup"><span data-stu-id="eb86c-245">g.</span></span> <span data-ttu-id="eb86c-246">Aby wyświetlić szczegóły synchronizacji haseł obiektu w poprzednim tygodniu, kliknij przycisk **dziennika**.</span><span class="sxs-lookup"><span data-stu-id="eb86c-246">To see the password sync details of the object for the past week, click **Log**.</span></span>  

    ![Szczegóły dziennika obiektu](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/csobjectlog.png)  

    <span data-ttu-id="eb86c-248">Jeśli w dzienniku obiektu jest pusta, Azure AD Connect została nie można odczytać skrótów haseł z usługi Active Directory.</span><span class="sxs-lookup"><span data-stu-id="eb86c-248">If the object log is empty, Azure AD Connect has been unable to read the password hash from Active Directory.</span></span> <span data-ttu-id="eb86c-249">Kontynuuj rozwiązywanie problemów z [błędów połączenia](#connectivity-errors).</span><span class="sxs-lookup"><span data-stu-id="eb86c-249">Continue your troubleshooting with [Connectivity Errors](#connectivity-errors).</span></span> <span data-ttu-id="eb86c-250">Jeśli widzisz innych wartości niż **Powodzenie**, zgodnie z tabelą w [Dziennik synchronizacji haseł](#password-sync-log).</span><span class="sxs-lookup"><span data-stu-id="eb86c-250">If you see any other value than **success**, refer to the table in [Password sync log](#password-sync-log).</span></span>

    <span data-ttu-id="eb86c-251">h.</span><span class="sxs-lookup"><span data-stu-id="eb86c-251">h.</span></span> <span data-ttu-id="eb86c-252">Wybierz **TABLE/}[%{Column/}]")** karcie i upewnij się, że tej reguły synchronizacji co najmniej jeden w **PasswordSync** kolumna jest **True**.</span><span class="sxs-lookup"><span data-stu-id="eb86c-252">Select the **lineage** tab, and make sure that at least one sync rule in the **PasswordSync** column is **True**.</span></span> <span data-ttu-id="eb86c-253">W konfiguracji domyślnej nazwy reguły synchronizacji jest **w z usługi AD - AccountEnabled użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="eb86c-253">In the default configuration, the name of the sync rule is **In from AD - User AccountEnabled**.</span></span>  

    ![Elementy powiązane informacje o użytkowniku](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/cspasswordsync.png)  

    <span data-ttu-id="eb86c-255">i.</span><span class="sxs-lookup"><span data-stu-id="eb86c-255">i.</span></span> <span data-ttu-id="eb86c-256">Kliknij przycisk **właściwości obiektu Metaverse** Aby wyświetlić listę atrybutów użytkowników.</span><span class="sxs-lookup"><span data-stu-id="eb86c-256">Click **Metaverse Object Properties** to display a list of user attributes.</span></span>  

    ![Informacje magazynie metaverse](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/mvpasswordsync.png)  

    <span data-ttu-id="eb86c-258">Sprawdź, czy jest nie **cloudFiltered** atrybutu.</span><span class="sxs-lookup"><span data-stu-id="eb86c-258">Verify that there is no **cloudFiltered** attribute present.</span></span> <span data-ttu-id="eb86c-259">Upewnij się, że oczekiwanych wartości atrybutów domeny (domainFQDN i domainNetBios).</span><span class="sxs-lookup"><span data-stu-id="eb86c-259">Make sure that the domain attributes (domainFQDN and domainNetBios) have the expected values.</span></span>

    <span data-ttu-id="eb86c-260">j.</span><span class="sxs-lookup"><span data-stu-id="eb86c-260">j.</span></span> <span data-ttu-id="eb86c-261">Kliknij przycisk **łączniki** kartę. Upewnij się, że widoczny łączniki do lokalnej usługi Active Directory i Azure AD.</span><span class="sxs-lookup"><span data-stu-id="eb86c-261">Click the **Connectors** tab. Make sure that you see connectors to both on-premises Active Directory and Azure AD.</span></span>

    ![Informacje magazynie metaverse](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/mvconnectors.png)  

    <span data-ttu-id="eb86c-263">k.</span><span class="sxs-lookup"><span data-stu-id="eb86c-263">k.</span></span> <span data-ttu-id="eb86c-264">Wybierz wiersz, który reprezentuje usługi Azure AD, kliknij przycisk **właściwości**, a następnie kliknij przycisk **elementy powiązane** kartę. Obiekt miejsca łącznik powinien mieć Reguła ruchu wychodzącego **PasswordSync** kolumny ustawioną **True**.</span><span class="sxs-lookup"><span data-stu-id="eb86c-264">Select the row that represents Azure AD, click **Properties**, and then click the **Lineage** tab. The connector space object should have an outbound rule in the **PasswordSync** column set to **True**.</span></span> <span data-ttu-id="eb86c-265">W konfiguracji domyślnej nazwy reguły synchronizacji jest **Out do usługi AAD — użytkownik przyłączyć**.</span><span class="sxs-lookup"><span data-stu-id="eb86c-265">In the default configuration, the name of the sync rule is **Out to AAD - User Join**.</span></span>  

    ![Okno dialogowe właściwości obiektu obszaru łącznika](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/cspasswordsync2.png)  

### <a name="password-sync-log"></a><span data-ttu-id="eb86c-267">Dziennik synchronizacji haseł</span><span class="sxs-lookup"><span data-stu-id="eb86c-267">Password sync log</span></span>
<span data-ttu-id="eb86c-268">W kolumnie Stan może mieć następujące wartości:</span><span class="sxs-lookup"><span data-stu-id="eb86c-268">The status column can have the following values:</span></span>

| <span data-ttu-id="eb86c-269">Stan</span><span class="sxs-lookup"><span data-stu-id="eb86c-269">Status</span></span> | <span data-ttu-id="eb86c-270">Opis</span><span class="sxs-lookup"><span data-stu-id="eb86c-270">Description</span></span> |
| --- | --- |
| <span data-ttu-id="eb86c-271">Powodzenie</span><span class="sxs-lookup"><span data-stu-id="eb86c-271">Success</span></span> |<span data-ttu-id="eb86c-272">Hasło zostało pomyślnie zsynchronizowane.</span><span class="sxs-lookup"><span data-stu-id="eb86c-272">Password has been successfully synchronized.</span></span> |
| <span data-ttu-id="eb86c-273">FilteredByTarget</span><span class="sxs-lookup"><span data-stu-id="eb86c-273">FilteredByTarget</span></span> |<span data-ttu-id="eb86c-274">Ustawiono hasło **użytkownik musi zmienić hasło przy następnym logowaniu**.</span><span class="sxs-lookup"><span data-stu-id="eb86c-274">Password is set to **User must change password at next logon**.</span></span> <span data-ttu-id="eb86c-275">Hasło nie zostały zsynchronizowane.</span><span class="sxs-lookup"><span data-stu-id="eb86c-275">Password has not been synchronized.</span></span> |
| <span data-ttu-id="eb86c-276">NoTargetConnection</span><span class="sxs-lookup"><span data-stu-id="eb86c-276">NoTargetConnection</span></span> |<span data-ttu-id="eb86c-277">Brak obiektu metaverse lub przestrzeni łącznika usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="eb86c-277">No object in the metaverse or in the Azure AD connector space.</span></span> |
| <span data-ttu-id="eb86c-278">SourceConnectorNotPresent</span><span class="sxs-lookup"><span data-stu-id="eb86c-278">SourceConnectorNotPresent</span></span> |<span data-ttu-id="eb86c-279">Nie można odnaleźć obiektu w lokalnej przestrzeni łącznika usługi Active Directory.</span><span class="sxs-lookup"><span data-stu-id="eb86c-279">No object found in the on-premises Active Directory connector space.</span></span> |
| <span data-ttu-id="eb86c-280">TargetNotExportedToDirectory</span><span class="sxs-lookup"><span data-stu-id="eb86c-280">TargetNotExportedToDirectory</span></span> |<span data-ttu-id="eb86c-281">Obiekt do przestrzeni łącznika usługi Azure AD nie zostały wyeksportowane.</span><span class="sxs-lookup"><span data-stu-id="eb86c-281">The object in the Azure AD connector space has not yet been exported.</span></span> |
| <span data-ttu-id="eb86c-282">MigratedCheckDetailsForMoreInfo</span><span class="sxs-lookup"><span data-stu-id="eb86c-282">MigratedCheckDetailsForMoreInfo</span></span> |<span data-ttu-id="eb86c-283">Wpis dziennika został utworzony przed kompilacji 1.0.9125.0 i jest wyświetlany w stanie starszej wersji.</span><span class="sxs-lookup"><span data-stu-id="eb86c-283">Log entry was created before build 1.0.9125.0 and is shown in its legacy state.</span></span> |
| <span data-ttu-id="eb86c-284">Błąd</span><span class="sxs-lookup"><span data-stu-id="eb86c-284">Error</span></span> |<span data-ttu-id="eb86c-285">Usługa zwróciła nieznany błąd.</span><span class="sxs-lookup"><span data-stu-id="eb86c-285">Service returned an unknown error.</span></span> |
| <span data-ttu-id="eb86c-286">Nieznany</span><span class="sxs-lookup"><span data-stu-id="eb86c-286">Unknown</span></span> |<span data-ttu-id="eb86c-287">Wystąpił błąd podczas próby przetworzenia partii skrótów haseł.</span><span class="sxs-lookup"><span data-stu-id="eb86c-287">An error occurred while trying to process a batch of password hashes.</span></span>  |
| <span data-ttu-id="eb86c-288">MissingAttribute</span><span class="sxs-lookup"><span data-stu-id="eb86c-288">MissingAttribute</span></span> |<span data-ttu-id="eb86c-289">Określone atrybuty (na przykład protokołu Kerberos wyznaczania wartości skrótu) wymagane przez usługi domenowe Azure AD nie są dostępne.</span><span class="sxs-lookup"><span data-stu-id="eb86c-289">Specific attributes (for example, Kerberos hash) required by Azure AD Domain Services are not available.</span></span> |
| <span data-ttu-id="eb86c-290">RetryRequestedByTarget</span><span class="sxs-lookup"><span data-stu-id="eb86c-290">RetryRequestedByTarget</span></span> |<span data-ttu-id="eb86c-291">Określone atrybuty (na przykład protokołu Kerberos wyznaczania wartości skrótu) wymagane przez usługi domenowe Azure AD nie były wcześniej dostępne.</span><span class="sxs-lookup"><span data-stu-id="eb86c-291">Specific attributes (for example, Kerberos hash) required by Azure AD Domain Services were not available previously.</span></span> <span data-ttu-id="eb86c-292">Podejmowana jest próba, aby ponownie zsynchronizować skrót hasła użytkownika.</span><span class="sxs-lookup"><span data-stu-id="eb86c-292">An attempt to resynchronize the user's password hash is made.</span></span> |

## <a name="scripts-to-help-troubleshooting"></a><span data-ttu-id="eb86c-293">Skrypty pomocne podczas rozwiązywania problemów</span><span class="sxs-lookup"><span data-stu-id="eb86c-293">Scripts to help troubleshooting</span></span>

### <a name="get-the-status-of-password-sync-settings"></a><span data-ttu-id="eb86c-294">Pobierz stan ustawienia synchronizacji haseł</span><span class="sxs-lookup"><span data-stu-id="eb86c-294">Get the status of password sync settings</span></span>
```
Import-Module ADSync
$connectors = Get-ADSyncConnector
$aadConnectors = $connectors | Where-Object {$_.SubType -eq "Windows Azure Active Directory (Microsoft)"}
$adConnectors = $connectors | Where-Object {$_.ConnectorTypeName -eq "AD"}
if ($aadConnectors -ne $null -and $adConnectors -ne $null)
{
    if ($aadConnectors.Count -eq 1)
    {
        $features = Get-ADSyncAADCompanyFeature -ConnectorName $aadConnectors[0].Name
        Write-Host
        Write-Host "Password sync feature enabled in your Azure AD directory: "  $features.PasswordHashSync
        foreach ($adConnector in $adConnectors)
        {
            Write-Host
            Write-Host "Password sync channel status BEGIN ------------------------------------------------------- "
            Write-Host
            Get-ADSyncAADPasswordSyncConfiguration -SourceConnector $adConnector.Name
            Write-Host
            $pingEvents =
                Get-EventLog -LogName "Application" -Source "Directory Synchronization" -InstanceId 654  -After (Get-Date).AddHours(-3) |
                    Where-Object { $_.Message.ToUpperInvariant().Contains($adConnector.Identifier.ToString("D").ToUpperInvariant()) } |
                    Sort-Object { $_.Time } -Descending
            if ($pingEvents -ne $null)
            {
                Write-Host "Latest heart beat event (within last 3 hours). Time " $pingEvents[0].TimeWritten
            }
            else
            {
                Write-Warning "No ping event found within last 3 hours."
            }
            Write-Host
            Write-Host "Password sync channel status END ------------------------------------------------------- "
            Write-Host
        }
    }
    else
    {
        Write-Warning "More than one Azure AD Connectors found. Please update the script to use the appropriate Connector."
    }
}
Write-Host
if ($aadConnectors -eq $null)
{
    Write-Warning "No Azure AD Connector was found."
}
if ($adConnectors -eq $null)
{
    Write-Warning "No AD DS Connector was found."
}
Write-Host
```

#### <a name="trigger-a-full-sync-of-all-passwords"></a><span data-ttu-id="eb86c-295">Wyzwalacz pełnej synchronizacji haseł wszystkich</span><span class="sxs-lookup"><span data-stu-id="eb86c-295">Trigger a full sync of all passwords</span></span>
> [!NOTE]
> <span data-ttu-id="eb86c-296">Ten skrypt należy uruchomić tylko raz.</span><span class="sxs-lookup"><span data-stu-id="eb86c-296">Run this script only once.</span></span> <span data-ttu-id="eb86c-297">Jeśli trzeba je uruchomić więcej niż jeden raz, jest coś innego problemu.</span><span class="sxs-lookup"><span data-stu-id="eb86c-297">If you need to run it more than once, something else is the problem.</span></span> <span data-ttu-id="eb86c-298">Aby rozwiązać ten problem, skontaktuj się z pomocą techniczną firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="eb86c-298">To troubleshoot the problem, contact Microsoft support.</span></span>

<span data-ttu-id="eb86c-299">Pełna synchronizacja haseł wszystkich można wywołać za pomocą następującego skryptu:</span><span class="sxs-lookup"><span data-stu-id="eb86c-299">You can trigger a full sync of all passwords by using the following script:</span></span>

```
$adConnector = "<CASE SENSITIVE AD CONNECTOR NAME>"
$aadConnector = "<CASE SENSITIVE AAD CONNECTOR NAME>"
Import-Module adsync
$c = Get-ADSyncConnector -Name $adConnector
$p = New-Object Microsoft.IdentityManagement.PowerShell.ObjectModel.ConfigurationParameter "Microsoft.Synchronize.ForceFullPasswordSync", String, ConnectorGlobal, $null, $null, $null
$p.Value = 1
$c.GlobalParameters.Remove($p.Name)
$c.GlobalParameters.Add($p)
$c = Add-ADSyncConnector -Connector $c
Set-ADSyncAADPasswordSyncConfiguration -SourceConnector $adConnector -TargetConnector $aadConnector -Enable $false
Set-ADSyncAADPasswordSyncConfiguration -SourceConnector $adConnector -TargetConnector $aadConnector -Enable $true
```

## <a name="next-steps"></a><span data-ttu-id="eb86c-300">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="eb86c-300">Next steps</span></span>
* [<span data-ttu-id="eb86c-301">Implementowanie synchronizacji haseł z synchronizacji Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="eb86c-301">Implementing password synchronization with Azure AD Connect sync</span></span>](active-directory-aadconnectsync-implement-password-synchronization.md)
* [<span data-ttu-id="eb86c-302">Azure AD Connect Sync: Dostosowywanie opcji synchronizacji</span><span class="sxs-lookup"><span data-stu-id="eb86c-302">Azure AD Connect Sync: Customizing synchronization options</span></span>](active-directory-aadconnectsync-whatis.md)
* [<span data-ttu-id="eb86c-303">Integrowanie tożsamości lokalnych z usługą Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="eb86c-303">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
