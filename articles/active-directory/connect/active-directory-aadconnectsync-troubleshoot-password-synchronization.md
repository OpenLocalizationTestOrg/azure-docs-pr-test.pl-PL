---
title: "Synchronizacja haseł aaaTroubleshoot z synchronizacji Azure AD Connect | Dokumentacja firmy Microsoft"
description: "Ten artykuł zawiera informacje na temat problemów z synchronizacją hasła tootroubleshoot."
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
ms.openlocfilehash: 390eafec792cb39251627c14cb754f8bb30035b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-password-synchronization-with-azure-ad-connect-sync"></a><span data-ttu-id="22f63-103">Rozwiązywanie problemów z synchronizacją hasła z synchronizacji Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="22f63-103">Troubleshoot password synchronization with Azure AD Connect sync</span></span>
<span data-ttu-id="22f63-104">Ten temat zawiera kroki opisujące sposób tootroubleshoot problemy z synchronizacją haseł.</span><span class="sxs-lookup"><span data-stu-id="22f63-104">This topic provides steps for how tootroubleshoot issues with password synchronization.</span></span> <span data-ttu-id="22f63-105">Jeśli nie można zsynchronizować hasła, zgodnie z oczekiwaniami, można dla podzbioru użytkowników lub dla wszystkich użytkowników.</span><span class="sxs-lookup"><span data-stu-id="22f63-105">If passwords are not synchronizing as expected, it can be either for a subset of users or for all users.</span></span> <span data-ttu-id="22f63-106">Dla usługi Azure Active Directory (Azure AD) wdrożenia Uzyskuj dostęp do wersji 1.1.524.0 lub później, jest teraz diagnostycznych polecenia cmdlet można tootroubleshoot problemów z synchronizacją hasła:</span><span class="sxs-lookup"><span data-stu-id="22f63-106">For Azure Active Directory (Azure AD) Connect deployment with version 1.1.524.0 or later, there is now a diagnostic cmdlet that you can use tootroubleshoot password synchronization issues:</span></span>

* <span data-ttu-id="22f63-107">Jeśli masz problem, których hasła nie są zsynchronizowane, zapoznaj się z pomocą techniczną firmy toohello [hasła nie są zsynchronizowane: Rozwiązywanie problemów przy użyciu polecenia cmdlet diagnostycznych hello](#no-passwords-are-synchronized-troubleshoot-by-using-the-diagnostic-cmdlet) sekcji.</span><span class="sxs-lookup"><span data-stu-id="22f63-107">If you have an issue where no passwords are synchronized, refer toohello [No passwords are synchronized: troubleshoot by using hello diagnostic cmdlet](#no-passwords-are-synchronized-troubleshoot-by-using-the-diagnostic-cmdlet) section.</span></span>

* <span data-ttu-id="22f63-108">Jeśli masz problem z pojedyncze obiekty, zapoznaj się z pomocą techniczną firmy toohello [jeden obiekt nie synchronizuje haseł: Rozwiązywanie problemów przy użyciu polecenia cmdlet diagnostycznych hello](#one-object-is-not-synchronizing-passwords-troubleshoot-by-using-the-diagnostic-cmdlet) sekcji.</span><span class="sxs-lookup"><span data-stu-id="22f63-108">If you have an issue with individual objects, refer toohello [One object is not synchronizing passwords: troubleshoot by using hello diagnostic cmdlet](#one-object-is-not-synchronizing-passwords-troubleshoot-by-using-the-diagnostic-cmdlet) section.</span></span>

<span data-ttu-id="22f63-109">Dla wcześniejszych wersji programu Azure AD Connect wdrażania:</span><span class="sxs-lookup"><span data-stu-id="22f63-109">For older versions of Azure AD Connect deployment:</span></span>

* <span data-ttu-id="22f63-110">Jeśli masz problem, których hasła nie są zsynchronizowane, zapoznaj się z pomocą techniczną firmy toohello [hasła nie są zsynchronizowane: Podręcznik rozwiązywania problemów z](#no-passwords-are-synchronized-manual-troubleshooting-steps) sekcji.</span><span class="sxs-lookup"><span data-stu-id="22f63-110">If you have an issue where no passwords are synchronized, refer toohello [No passwords are synchronized: manual troubleshooting steps](#no-passwords-are-synchronized-manual-troubleshooting-steps) section.</span></span>

* <span data-ttu-id="22f63-111">Jeśli masz problem z pojedyncze obiekty, zapoznaj się z pomocą techniczną firmy toohello [jeden obiekt nie synchronizuje haseł: Podręcznik rozwiązywania problemów z](#one-object-is-not-synchronizing-passwords-manual-troubleshooting-steps) sekcji.</span><span class="sxs-lookup"><span data-stu-id="22f63-111">If you have an issue with individual objects, refer toohello [One object is not synchronizing passwords: manual troubleshooting steps](#one-object-is-not-synchronizing-passwords-manual-troubleshooting-steps) section.</span></span>

## <a name="no-passwords-are-synchronized-troubleshoot-by-using-hello-diagnostic-cmdlet"></a><span data-ttu-id="22f63-112">Hasła nie są zsynchronizowane: Rozwiązywanie problemów przy użyciu polecenia cmdlet diagnostycznych hello</span><span class="sxs-lookup"><span data-stu-id="22f63-112">No passwords are synchronized: troubleshoot by using hello diagnostic cmdlet</span></span>
<span data-ttu-id="22f63-113">Można użyć hello `Invoke-ADSyncDiagnostics` toofigure polecenia cmdlet się, dlaczego hasła nie są zsynchronizowane.</span><span class="sxs-lookup"><span data-stu-id="22f63-113">You can use hello `Invoke-ADSyncDiagnostics` cmdlet toofigure out why no passwords are synchronized.</span></span>

> [!NOTE]
> <span data-ttu-id="22f63-114">Witaj `Invoke-ADSyncDiagnostics` polecenia cmdlet jest dostępna tylko dla wersji Azure AD Connect 1.1.524.0 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="22f63-114">hello `Invoke-ADSyncDiagnostics` cmdlet is available only for Azure AD Connect version 1.1.524.0 or later.</span></span>

### <a name="run-hello-diagnostics-cmdlet"></a><span data-ttu-id="22f63-115">Uruchom polecenie cmdlet diagnostyki hello</span><span class="sxs-lookup"><span data-stu-id="22f63-115">Run hello diagnostics cmdlet</span></span>
<span data-ttu-id="22f63-116">tootroubleshoot problemy, których hasła nie są zsynchronizowane:</span><span class="sxs-lookup"><span data-stu-id="22f63-116">tootroubleshoot issues where no passwords are synchronized:</span></span>

1. <span data-ttu-id="22f63-117">Otwórz sesję programu Windows PowerShell na serwerze programu Azure AD Connect z hello **Uruchom jako Administrator** opcji.</span><span class="sxs-lookup"><span data-stu-id="22f63-117">Open a new Windows PowerShell session on your Azure AD Connect server with hello **Run as Administrator** option.</span></span>

2. <span data-ttu-id="22f63-118">Uruchom `Set-ExecutionPolicy RemoteSigned` lub `Set-ExecutionPolicy Unrestricted`.</span><span class="sxs-lookup"><span data-stu-id="22f63-118">Run `Set-ExecutionPolicy RemoteSigned` or `Set-ExecutionPolicy Unrestricted`.</span></span>

3. <span data-ttu-id="22f63-119">Uruchom polecenie `Import-Module ADSyncDiagnostics`.</span><span class="sxs-lookup"><span data-stu-id="22f63-119">Run `Import-Module ADSyncDiagnostics`.</span></span>

4. <span data-ttu-id="22f63-120">Uruchom polecenie `Invoke-ADSyncDiagnostics -PasswordSync`.</span><span class="sxs-lookup"><span data-stu-id="22f63-120">Run `Invoke-ADSyncDiagnostics -PasswordSync`.</span></span>

### <a name="understand-hello-results-of-hello-cmdlet"></a><span data-ttu-id="22f63-121">Zrozumienie hello wyniki polecenia cmdlet hello</span><span class="sxs-lookup"><span data-stu-id="22f63-121">Understand hello results of hello cmdlet</span></span>
<span data-ttu-id="22f63-122">polecenia cmdlet diagnostycznych Hello wykonuje powitania po kontroli:</span><span class="sxs-lookup"><span data-stu-id="22f63-122">hello diagnostic cmdlet performs hello following checks:</span></span>

* <span data-ttu-id="22f63-123">Sprawdza poprawność tego hello funkcji synchronizacji haseł jest włączona dla Twojej dzierżawy usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="22f63-123">Validates that hello password synchronization feature is enabled for your Azure AD tenant.</span></span>

* <span data-ttu-id="22f63-124">Sprawdza poprawność tego hello Azure AD Connect, serwer nie jest w trybie przejściowym.</span><span class="sxs-lookup"><span data-stu-id="22f63-124">Validates that hello Azure AD Connect server is not in staging mode.</span></span>

* <span data-ttu-id="22f63-125">Dla każdego istniejącego lokalnego łącznika usługi Active Directory, (co odpowiada tooan istniejącego lasu usługi Active Directory):</span><span class="sxs-lookup"><span data-stu-id="22f63-125">For each existing on-premises Active Directory connector (which corresponds tooan existing Active Directory forest):</span></span>

   * <span data-ttu-id="22f63-126">Sprawdza poprawność tego hello jest włączona funkcja synchronizacji hasła.</span><span class="sxs-lookup"><span data-stu-id="22f63-126">Validates that hello password synchronization feature is enabled.</span></span>
   
   * <span data-ttu-id="22f63-127">Wyszukuje zdarzeń pulsu synchronizacji haseł w hello dzienniki zdarzeń aplikacji systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="22f63-127">Searches for password synchronization heartbeat events in hello Windows Application Event logs.</span></span>

   * <span data-ttu-id="22f63-128">Dla każdej domeny usługi Active Directory, w obszarze łącznika usługi Active Directory lokalne powitania:</span><span class="sxs-lookup"><span data-stu-id="22f63-128">For each Active Directory domain under hello on-premises Active Directory connector:</span></span>

      * <span data-ttu-id="22f63-129">Sprawdza poprawność tego hello domena jest osiągalna z hello Azure AD Connect serwera.</span><span class="sxs-lookup"><span data-stu-id="22f63-129">Validates that hello domain is reachable from hello Azure AD Connect server.</span></span>

      * <span data-ttu-id="22f63-130">Sprawdza, czy konta usług domenowych w usłudze Active Directory (AD DS) hello używane przez łącznik usługi Active Directory lokalne powitania ma hello prawidłową nazwę użytkownika, hasło i uprawnienia wymagane do synchronizacji haseł.</span><span class="sxs-lookup"><span data-stu-id="22f63-130">Validates that hello Active Directory Domain Services (AD DS) accounts used by hello on-premises Active Directory connector has hello correct username, password, and permissions required for password synchronization.</span></span>

<span data-ttu-id="22f63-131">powitania po diagram ilustruje hello wyniki polecenia cmdlet hello Topologia jednej domenie lokalnej usługi Active Directory:</span><span class="sxs-lookup"><span data-stu-id="22f63-131">hello following diagram illustrates hello results of hello cmdlet for a single-domain, on-premises Active Directory topology:</span></span>

![Dane wyjściowe diagnostyki dla synchronizacji haseł](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobalgeneral.png)

<span data-ttu-id="22f63-133">Witaj pozostałej części tej sekcji opisano określone wyniki, które są zwracane przez polecenie cmdlet hello i odpowiednie problemy.</span><span class="sxs-lookup"><span data-stu-id="22f63-133">hello rest of this section describes specific results that are returned by hello cmdlet and corresponding issues.</span></span>

#### <a name="password-synchronization-feature-isnt-enabled"></a><span data-ttu-id="22f63-134">Funkcja synchronizacji hasła nie jest włączona.</span><span class="sxs-lookup"><span data-stu-id="22f63-134">Password synchronization feature isn't enabled</span></span>
<span data-ttu-id="22f63-135">Jeśli nie włączono synchronizacji haseł za pomocą kreatora Połącz hello Azure AD, jest zwracany hello następujący błąd:</span><span class="sxs-lookup"><span data-stu-id="22f63-135">If you haven't enabled password synchronization by using hello Azure AD Connect wizard, hello following error is returned:</span></span>

![Synchronizacja haseł nie jest włączona.](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobaldisabled.png)

#### <a name="azure-ad-connect-server-is-in-staging-mode"></a><span data-ttu-id="22f63-137">Serwer systemu Azure AD Connect jest w trybie przejściowym</span><span class="sxs-lookup"><span data-stu-id="22f63-137">Azure AD Connect server is in staging mode</span></span>
<span data-ttu-id="22f63-138">Jeśli hello Azure AD Connect serwer działa w trybie przejściowym, synchronizacja haseł jest tymczasowo wyłączona i hello następujące zostanie zwrócony błąd:</span><span class="sxs-lookup"><span data-stu-id="22f63-138">If hello Azure AD Connect server is in staging mode, password synchronization is temporarily disabled, and hello following error is returned:</span></span>

![Serwer systemu Azure AD Connect jest w trybie przejściowym](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobalstaging.png)

#### <a name="no-password-synchronization-heartbeat-events"></a><span data-ttu-id="22f63-140">Brak zdarzeń pulsu synchronizacji haseł</span><span class="sxs-lookup"><span data-stu-id="22f63-140">No password synchronization heartbeat events</span></span>
<span data-ttu-id="22f63-141">Każdy łącznik usługi Active Directory lokalnego ma własną kanału synchronizacji haseł.</span><span class="sxs-lookup"><span data-stu-id="22f63-141">Each on-premises Active Directory connector has its own password synchronization channel.</span></span> <span data-ttu-id="22f63-142">Po nawiązaniu kanału synchronizacji haseł hello i nie ma żadnych toobe zmiany hasła zsynchronizowane, co 30 minut w dzienniku zdarzeń aplikacji systemu Windows hello zostanie wygenerowane zdarzenie pulsu (identyfikator EventId 654).</span><span class="sxs-lookup"><span data-stu-id="22f63-142">When hello password synchronization channel is established and there aren't any password changes toobe synchronized, a heartbeat event (EventId 654) is generated once every 30 minutes under hello Windows Application Event Log.</span></span> <span data-ttu-id="22f63-143">Przez każdy łącznik usługi Active Directory lokalne powitania polecenie cmdlet wyszukuje, poszukaj pokrewnych zdarzeń pulsu w hello ostatnich trzech godzin.</span><span class="sxs-lookup"><span data-stu-id="22f63-143">For each on-premises Active Directory connector, hello cmdlet searches for corresponding heartbeat events in hello past three hours.</span></span> <span data-ttu-id="22f63-144">Jeśli żadne zdarzenie pulsu zostanie znaleziony, hello następujące zostanie zwrócony błąd:</span><span class="sxs-lookup"><span data-stu-id="22f63-144">If no heartbeat event is found, hello following error is returned:</span></span>

![Nie pulsu synchronizacji haseł Ci zdarzeń](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobalnoheartbeat.png)

#### <a name="ad-ds-account-does-not-have-correct-permissions"></a><span data-ttu-id="22f63-146">Usługi AD DS konto nie ma odpowiednich uprawnień</span><span class="sxs-lookup"><span data-stu-id="22f63-146">AD DS account does not have correct permissions</span></span>
<span data-ttu-id="22f63-147">Jeśli konto hello usług AD DS, które jest używane przez hello lokalnego skrótów haseł toosynchronize łącznika usługi Active Directory nie ma odpowiednich uprawnień hello hello następujące zostanie zwrócony błąd:</span><span class="sxs-lookup"><span data-stu-id="22f63-147">If hello AD DS account that's used by hello on-premises Active Directory connector toosynchronize password hashes does not have hello appropriate permissions, hello following error is returned:</span></span>

![Nieprawidłowe poświadczenia](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobalaccountincorrectpermission.png)

#### <a name="incorrect-ad-ds-account-username-or-password"></a><span data-ttu-id="22f63-149">Nieprawidłowa nazwa użytkownika konta usług AD DS lub hasło</span><span class="sxs-lookup"><span data-stu-id="22f63-149">Incorrect AD DS account username or password</span></span>
<span data-ttu-id="22f63-150">Jeśli hello konta usług AD DS używany przez hello skrótów haseł toosynchronize lokalnej usługi Active Directory łącznika ma nieprawidłową nazwą użytkownika lub hasło, hello następujące zostanie zwrócony błąd:</span><span class="sxs-lookup"><span data-stu-id="22f63-150">If hello AD DS account used by hello on-premises Active Directory connector toosynchronize password hashes has an incorrect username or password, hello following error is returned:</span></span>

![Nieprawidłowe poświadczenia](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobalaccountincorrectcredential.png)

## <a name="one-object-is-not-synchronizing-passwords-troubleshoot-by-using-hello-diagnostic-cmdlet"></a><span data-ttu-id="22f63-152">Jeden obiekt nie synchronizuje haseł: Rozwiązywanie problemów przy użyciu polecenia cmdlet diagnostycznych hello</span><span class="sxs-lookup"><span data-stu-id="22f63-152">One object is not synchronizing passwords: troubleshoot by using hello diagnostic cmdlet</span></span>
<span data-ttu-id="22f63-153">Można użyć hello `Invoke-ADSyncDiagnostics` toodetermine polecenia cmdlet, dlaczego jeden obiekt nie synchronizuje haseł.</span><span class="sxs-lookup"><span data-stu-id="22f63-153">You can use hello `Invoke-ADSyncDiagnostics` cmdlet toodetermine why one object is not synchronizing passwords.</span></span>

> [!NOTE]
> <span data-ttu-id="22f63-154">Witaj `Invoke-ADSyncDiagnostics` polecenia cmdlet jest dostępna tylko dla wersji Azure AD Connect 1.1.524.0 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="22f63-154">hello `Invoke-ADSyncDiagnostics` cmdlet is available only for Azure AD Connect version 1.1.524.0 or later.</span></span>

### <a name="run-hello-diagnostics-cmdlet"></a><span data-ttu-id="22f63-155">Uruchom polecenie cmdlet diagnostyki hello</span><span class="sxs-lookup"><span data-stu-id="22f63-155">Run hello diagnostics cmdlet</span></span>
<span data-ttu-id="22f63-156">tootroubleshoot problemy, których hasła nie są zsynchronizowane:</span><span class="sxs-lookup"><span data-stu-id="22f63-156">tootroubleshoot issues where no passwords are synchronized:</span></span>

1. <span data-ttu-id="22f63-157">Otwórz sesję programu Windows PowerShell na serwerze programu Azure AD Connect z hello **Uruchom jako Administrator** opcji.</span><span class="sxs-lookup"><span data-stu-id="22f63-157">Open a new Windows PowerShell session on your Azure AD Connect server with hello **Run as Administrator** option.</span></span>

2. <span data-ttu-id="22f63-158">Uruchom `Set-ExecutionPolicy RemoteSigned` lub `Set-ExecutionPolicy Unrestricted`.</span><span class="sxs-lookup"><span data-stu-id="22f63-158">Run `Set-ExecutionPolicy RemoteSigned` or `Set-ExecutionPolicy Unrestricted`.</span></span>

3. <span data-ttu-id="22f63-159">Uruchom polecenie `Import-Module ADSyncDiagnostics`.</span><span class="sxs-lookup"><span data-stu-id="22f63-159">Run `Import-Module ADSyncDiagnostics`.</span></span>

4. <span data-ttu-id="22f63-160">Uruchom następujące polecenia cmdlet hello:</span><span class="sxs-lookup"><span data-stu-id="22f63-160">Run hello following cmdlet:</span></span>
   ```
   Invoke-ADSyncDiagnostics -PasswordSync -ADConnectorName <Name-of-AD-Connector> -DistinguishedName <DistinguishedName-of-AD-object>
   ```
   <span data-ttu-id="22f63-161">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="22f63-161">For example:</span></span>
   ```
   Invoke-ADSyncDiagnostics -PasswordSync -ADConnectorName "contoso.com" -DistinguishedName "CN=TestUserCN=Users,DC=contoso,DC=com"
   ```

### <a name="understand-hello-results-of-hello-cmdlet"></a><span data-ttu-id="22f63-162">Zrozumienie hello wyniki polecenia cmdlet hello</span><span class="sxs-lookup"><span data-stu-id="22f63-162">Understand hello results of hello cmdlet</span></span>
<span data-ttu-id="22f63-163">polecenia cmdlet diagnostycznych Hello wykonuje powitania po kontroli:</span><span class="sxs-lookup"><span data-stu-id="22f63-163">hello diagnostic cmdlet performs hello following checks:</span></span>

* <span data-ttu-id="22f63-164">Sprawdza stan hello hello obiektu usługi Active Directory w przestrzeni łącznika usługi Active Directory hello Metaverse i Azure AD przestrzeni łącznika.</span><span class="sxs-lookup"><span data-stu-id="22f63-164">Examines hello state of hello Active Directory object in hello Active Directory connector space, Metaverse, and Azure AD connector space.</span></span>

* <span data-ttu-id="22f63-165">Sprawdza, czy są reguły synchronizacji z synchronizacją haseł włączone i stosowane toohello obiektu usługi Active Directory.</span><span class="sxs-lookup"><span data-stu-id="22f63-165">Validates that there are synchronization rules with password synchronization enabled and applied toohello Active Directory object.</span></span>

* <span data-ttu-id="22f63-166">Próbuje tooretrieve i wyświetlania wyników hello hello ostatniej próby toosynchronize hello hasła dla obiekt hello.</span><span class="sxs-lookup"><span data-stu-id="22f63-166">Attempts tooretrieve and display hello results of hello last attempt toosynchronize hello password for hello object.</span></span>

<span data-ttu-id="22f63-167">powitania po diagram ilustruje hello wyniki polecenia cmdlet hello podczas rozwiązywania problemów z synchronizacji haseł dla pojedynczego obiektu:</span><span class="sxs-lookup"><span data-stu-id="22f63-167">hello following diagram illustrates hello results of hello cmdlet when troubleshooting password synchronization for a single object:</span></span>

![Dane wyjściowe diagnostyki dla synchronizacji haseł — pojedynczy obiekt](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phssingleobjectgeneral.png)

<span data-ttu-id="22f63-169">Witaj pozostałej części tej sekcji opisano określonych wyników zwróconych przez polecenie cmdlet hello i odpowiednie problemy.</span><span class="sxs-lookup"><span data-stu-id="22f63-169">hello rest of this section describes specific results returned by hello cmdlet and corresponding issues.</span></span>

#### <a name="hello-active-directory-object-isnt-exported-tooazure-ad"></a><span data-ttu-id="22f63-170">Hello obiektu usługi Active Directory nie jest eksportowany tooAzure AD</span><span class="sxs-lookup"><span data-stu-id="22f63-170">hello Active Directory object isn't exported tooAzure AD</span></span>
<span data-ttu-id="22f63-171">Synchronizacja haseł dla tego konta usługi Active Directory lokalnymi nie powiedzie się, ponieważ nie ma odpowiedniego obiektu w hello dzierżawy usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="22f63-171">Password synchronization for this on-premises Active Directory account fails because there is no corresponding object in hello Azure AD tenant.</span></span> <span data-ttu-id="22f63-172">Zwrócono Hello następujący błąd:</span><span class="sxs-lookup"><span data-stu-id="22f63-172">hello following error is returned:</span></span>

![Brak obiektu usługi Active Directory systemu Azure](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phssingleobjectnotexported.png)

#### <a name="user-has-a-temporary-password"></a><span data-ttu-id="22f63-174">Użytkownik ma hasło tymczasowe</span><span class="sxs-lookup"><span data-stu-id="22f63-174">User has a temporary password</span></span>
<span data-ttu-id="22f63-175">Azure AD Connect nie obsługuje obecnie synchronizowanie tymczasowego hasła z usługą Azure AD.</span><span class="sxs-lookup"><span data-stu-id="22f63-175">Currently, Azure AD Connect does not support synchronizing temporary passwords with Azure AD.</span></span> <span data-ttu-id="22f63-176">Hasło jest uznawany za toobe tymczasowego Jeśli hello **zmienić hasło przy następnym logowaniu** opcja jest ustawiona na powitania lokalnej usługi Active Directory użytkownika.</span><span class="sxs-lookup"><span data-stu-id="22f63-176">A password is considered toobe temporary if hello **Change password at next logon** option is set on hello on-premises Active Directory user.</span></span> <span data-ttu-id="22f63-177">Zwrócono Hello następujący błąd:</span><span class="sxs-lookup"><span data-stu-id="22f63-177">hello following error is returned:</span></span>

![Hasło tymczasowe nie są eksportowane.](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phssingleobjecttemporarypassword.png)

#### <a name="results-of-last-attempt-toosynchronize-password-arent-available"></a><span data-ttu-id="22f63-179">Wyniki ostatniej próby toosynchronize hasła nie są dostępne</span><span class="sxs-lookup"><span data-stu-id="22f63-179">Results of last attempt toosynchronize password aren't available</span></span>
<span data-ttu-id="22f63-180">Domyślnie program Azure AD Connect przechowuje wyniki hello prób synchronizacji haseł na siedem dni.</span><span class="sxs-lookup"><span data-stu-id="22f63-180">By default, Azure AD Connect stores hello results of password synchronization attempts for seven days.</span></span> <span data-ttu-id="22f63-181">Jeśli nie są dostępne dla obiekt usługi Active Directory hello wybrane wyniki, zwracany jest hello następujące ostrzeżenie:</span><span class="sxs-lookup"><span data-stu-id="22f63-181">If there are no results available for hello selected Active Directory object, hello following warning is returned:</span></span>

![Dane wyjściowe diagnostyki dla pojedynczego obiektu — nie historii synchronizacji haseł](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phssingleobjectnohistory.png)


## <a name="no-passwords-are-synchronized-manual-troubleshooting-steps"></a><span data-ttu-id="22f63-183">Hasła nie są zsynchronizowane: ręczne kroki rozwiązywania problemów</span><span class="sxs-lookup"><span data-stu-id="22f63-183">No passwords are synchronized: manual troubleshooting steps</span></span>
<span data-ttu-id="22f63-184">Wykonaj te kroki toodetermine, dlaczego hasła nie są zsynchronizowane:</span><span class="sxs-lookup"><span data-stu-id="22f63-184">Follow these steps toodetermine why no passwords are synchronized:</span></span>

1. <span data-ttu-id="22f63-185">Jest serwerem Connect hello w [Tryb przejściowy](active-directory-aadconnectsync-operations.md#staging-mode)?</span><span class="sxs-lookup"><span data-stu-id="22f63-185">Is hello Connect server in [staging mode](active-directory-aadconnectsync-operations.md#staging-mode)?</span></span> <span data-ttu-id="22f63-186">Serwer w trybie przejściowym nie synchronizować hasła.</span><span class="sxs-lookup"><span data-stu-id="22f63-186">A server in staging mode does not synchronize any passwords.</span></span>

2. <span data-ttu-id="22f63-187">Uruchom skrypt hello w hello [Pobierz stan hello ustawień synchronizacji hasła](#get-the-status-of-password-sync-settings) sekcji.</span><span class="sxs-lookup"><span data-stu-id="22f63-187">Run hello script in hello [Get hello status of password sync settings](#get-the-status-of-password-sync-settings) section.</span></span> <span data-ttu-id="22f63-188">Udostępnia przegląd konfiguracji synchronizacji haseł hello.</span><span class="sxs-lookup"><span data-stu-id="22f63-188">It gives you an overview of hello password sync configuration.</span></span>  

    ![Dane wyjściowe skryptu programu PowerShell z ustawień synchronizacji haseł](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/psverifyconfig.png)  

3. <span data-ttu-id="22f63-190">Nie włączono funkcji hello w usłudze Azure AD lub stan kanału synchronizacji hello nie jest włączona, uruchom Kreatora instalacji Connect hello.</span><span class="sxs-lookup"><span data-stu-id="22f63-190">If hello feature is not enabled in Azure AD or if hello sync channel status is not enabled, run hello Connect installation wizard.</span></span> <span data-ttu-id="22f63-191">Wybierz **Dostosuj opcje synchronizacji**i usuń zaznaczenie pozycji synchronizacji haseł. Ta zmiana tymczasowo wyłącza funkcję hello.</span><span class="sxs-lookup"><span data-stu-id="22f63-191">Select **Customize synchronization options**, and unselect password sync. This change temporarily disables hello feature.</span></span> <span data-ttu-id="22f63-192">Następnie uruchom ponownie kreatora hello i ponowne włączenie synchronizacji haseł. Uruchom skrypt hello ponownie tooverify, który hello konfiguracji są poprawne.</span><span class="sxs-lookup"><span data-stu-id="22f63-192">Then run hello wizard again and re-enable password sync. Run hello script again tooverify that hello configuration is correct.</span></span>

4. <span data-ttu-id="22f63-193">Poszukaj w dzienniku zdarzeń hello błędów.</span><span class="sxs-lookup"><span data-stu-id="22f63-193">Look in hello event log for errors.</span></span> <span data-ttu-id="22f63-194">Wyszukaj hello następujące zdarzenia, które wskazują problem:</span><span class="sxs-lookup"><span data-stu-id="22f63-194">Look for hello following events, which would indicate a problem:</span></span>
    * <span data-ttu-id="22f63-195">Źródła: Identyfikator "Synchronizacji katalogów": 0, 611, 652, 655, jeśli te zdarzenia są widoczne masz problem z połączeniem.</span><span class="sxs-lookup"><span data-stu-id="22f63-195">Source: "Directory synchronization" ID: 0, 611, 652, 655 If you see these events, you have a connectivity problem.</span></span> <span data-ttu-id="22f63-196">Hello komunikatu dziennika zdarzeń zawiera informacje lasu, gdzie występuje problem.</span><span class="sxs-lookup"><span data-stu-id="22f63-196">hello event log message contains forest information where you have a problem.</span></span> <span data-ttu-id="22f63-197">Aby uzyskać więcej informacji, zobacz [problem z łącznością](#connectivity problem).</span><span class="sxs-lookup"><span data-stu-id="22f63-197">For more information, see [Connectivity problem](#connectivity problem).</span></span>

5. <span data-ttu-id="22f63-198">Jeśli widzisz Brak pulsu lub pracuje zaczynającego, uruchom [wyzwolenia pełnej synchronizacji haseł wszystkich](#trigger-a-full-sync-of-all-passwords).</span><span class="sxs-lookup"><span data-stu-id="22f63-198">If you see no heartbeat or if nothing else worked, run [Trigger a full sync of all passwords](#trigger-a-full-sync-of-all-passwords).</span></span> <span data-ttu-id="22f63-199">Uruchom skrypt hello tylko raz.</span><span class="sxs-lookup"><span data-stu-id="22f63-199">Run hello script only once.</span></span>

6. <span data-ttu-id="22f63-200">Zobacz hello [Rozwiązywanie problemów z jednego obiektu, który nie jest synchronizowanie haseł](#one-object-is-not-synchronizing-passwords) sekcji.</span><span class="sxs-lookup"><span data-stu-id="22f63-200">See hello [Troubleshoot one object that is not synchronizing passwords](#one-object-is-not-synchronizing-passwords) section.</span></span>

### <a name="connectivity-problems"></a><span data-ttu-id="22f63-201">Problemy z łącznością</span><span class="sxs-lookup"><span data-stu-id="22f63-201">Connectivity problems</span></span>

<span data-ttu-id="22f63-202">Czy masz połączenie z usługą Azure AD?</span><span class="sxs-lookup"><span data-stu-id="22f63-202">Do you have connectivity with Azure AD?</span></span>

<span data-ttu-id="22f63-203">Konto hello wymaganych wartości skrótów haseł hello tooread uprawnienia we wszystkich domenach?</span><span class="sxs-lookup"><span data-stu-id="22f63-203">Does hello account have required permissions tooread hello password hashes in all domains?</span></span> <span data-ttu-id="22f63-204">Jeśli zainstalowano Połącz przy użyciu ustawień ekspresowych hello uprawnień powinna już być poprawne.</span><span class="sxs-lookup"><span data-stu-id="22f63-204">If you installed Connect by using Express settings, hello permissions should already be correct.</span></span> 

<span data-ttu-id="22f63-205">Jeśli używasz niestandardowej instalacji, należy ręcznie ustawić uprawnienia hello hello następujący:</span><span class="sxs-lookup"><span data-stu-id="22f63-205">If you used custom installation, set hello permissions manually by doing hello following:</span></span>
    
1. <span data-ttu-id="22f63-206">toofind hello konto używane przez łącznik usługi Active Directory hello, start **Menedżera usługi synchronizacji**.</span><span class="sxs-lookup"><span data-stu-id="22f63-206">toofind hello account used by hello Active Directory connector, start **Synchronization Service Manager**.</span></span> 
 
2. <span data-ttu-id="22f63-207">Przejdź za**łączniki**, a następnie wyszukaj lasu usługi Active Directory lokalne powitania rozwiązywania problemów.</span><span class="sxs-lookup"><span data-stu-id="22f63-207">Go too**Connectors**, and then search for hello on-premises Active Directory forest you are troubleshooting.</span></span> 
 
3. <span data-ttu-id="22f63-208">Wybierz łącznik hello, a następnie kliknij przycisk **właściwości**.</span><span class="sxs-lookup"><span data-stu-id="22f63-208">Select hello connector, and then click **Properties**.</span></span> 
 
4. <span data-ttu-id="22f63-209">Przejdź za**Connect lesie katalogu tooActive**.</span><span class="sxs-lookup"><span data-stu-id="22f63-209">Go too**Connect tooActive Directory Forest**.</span></span>  
    
    ![Konto używane przez łącznik usługi Active Directory](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/connectoraccount.png)  
    <span data-ttu-id="22f63-211">Należy pamiętać, hello nazwę użytkownika i domenę hello, w której znajduje się konto hello.</span><span class="sxs-lookup"><span data-stu-id="22f63-211">Note hello username and hello domain where hello account is located.</span></span>
    
5. <span data-ttu-id="22f63-212">Uruchom **użytkownicy usługi Active Directory i komputery**, a następnie sprawdź, czy konto hello znalezionych w wcześniej ma uprawnienia wykonaj hello ustawione w głównym hello wszystkich domen w lesie:</span><span class="sxs-lookup"><span data-stu-id="22f63-212">Start **Active Directory Users and Computers**, and then verify that hello account you found earlier has hello follow permissions set at hello root of all domains in your forest:</span></span>
    * <span data-ttu-id="22f63-213">Replikować zmiany katalogu</span><span class="sxs-lookup"><span data-stu-id="22f63-213">Replicate Directory Changes</span></span>
    * <span data-ttu-id="22f63-214">Replikowanie katalogu zmienia wszystkie</span><span class="sxs-lookup"><span data-stu-id="22f63-214">Replicate Directory Changes All</span></span>

6. <span data-ttu-id="22f63-215">Czy hello kontrolerów domeny jest dostępny przy użyciu programu Azure AD Connect?</span><span class="sxs-lookup"><span data-stu-id="22f63-215">Are hello domain controllers reachable by Azure AD Connect?</span></span> <span data-ttu-id="22f63-216">Jeśli hello Połącz serwer nie może połączyć tooall kontrolerów domeny, należy skonfigurować **tylko Użyj preferowanego kontrolera domeny**.</span><span class="sxs-lookup"><span data-stu-id="22f63-216">If hello Connect server cannot connect tooall domain controllers, configure **Only use preferred domain controller**.</span></span>  
    
    ![Kontroler domeny jest używany przez łącznik usługi Active Directory](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/preferreddc.png)  
    
7. <span data-ttu-id="22f63-218">Wróć za**Menedżera usługi synchronizacji** i **Konfigurowanie partycji katalogu**.</span><span class="sxs-lookup"><span data-stu-id="22f63-218">Go back too**Synchronization Service Manager** and **Configure Directory Partition**.</span></span> 
 
8. <span data-ttu-id="22f63-219">Wybierz domenę w **Wybieranie partycji katalogu**, wybierz pozycję hello **korzystają z kontrolerów domeny preferowanych** pole wyboru, a następnie kliknij przycisk **Konfiguruj**.</span><span class="sxs-lookup"><span data-stu-id="22f63-219">Select your domain in **Select directory partitions**, select hello **Only use preferred domain controllers** check box, and then click **Configure**.</span></span> 

9. <span data-ttu-id="22f63-220">Na liście hello wprowadź hello kontrolerów domeny, które Connect należy używać do synchronizacji haseł. Witaj, importowania i eksportowania również jest używana w tej samej listy.</span><span class="sxs-lookup"><span data-stu-id="22f63-220">In hello list, enter hello domain controllers that Connect should use for password sync. hello same list is used for import and export as well.</span></span> <span data-ttu-id="22f63-221">Wykonaj te kroki dla wszystkich domen.</span><span class="sxs-lookup"><span data-stu-id="22f63-221">Do these steps for all your domains.</span></span>

10. <span data-ttu-id="22f63-222">Jeśli skrypt hello pokazuje, że jest brak pulsu, uruchom skrypt hello w [wyzwolenia pełnej synchronizacji haseł wszystkich](#trigger-a-full-sync-of-all-passwords).</span><span class="sxs-lookup"><span data-stu-id="22f63-222">If hello script shows that there is no heartbeat, run hello script in [Trigger a full sync of all passwords](#trigger-a-full-sync-of-all-passwords).</span></span>

## <a name="one-object-is-not-synchronizing-passwords-manual-troubleshooting-steps"></a><span data-ttu-id="22f63-223">Jeden obiekt nie synchronizuje haseł: ręczne kroki rozwiązywania problemów</span><span class="sxs-lookup"><span data-stu-id="22f63-223">One object is not synchronizing passwords: manual troubleshooting steps</span></span>
<span data-ttu-id="22f63-224">Umożliwia łatwe rozwiązywanie problemów z synchronizacją hasła, przeglądając hello stanu obiektu.</span><span class="sxs-lookup"><span data-stu-id="22f63-224">You can easily troubleshoot password synchronization issues by reviewing hello status of an object.</span></span>

1. <span data-ttu-id="22f63-225">W **użytkownicy usługi Active Directory i komputery**, wyszukaj hello użytkownika, a następnie sprawdź tego hello **użytkownik musi zmienić hasło przy następnym logowaniu** pole wyboru jest wyczyszczone.</span><span class="sxs-lookup"><span data-stu-id="22f63-225">In **Active Directory Users and Computers**, search for hello user, and then verify that hello **User must change password at next logon** check box is cleared.</span></span>  

    ![Active Directory produktywności hasła.](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/adprodpassword.png)  

    <span data-ttu-id="22f63-227">Jeśli zaznaczono pole wyboru hello, poproś hello toosign użytkownika w i Zmień hasło hello.</span><span class="sxs-lookup"><span data-stu-id="22f63-227">If hello check box is selected, ask hello user toosign in and change hello password.</span></span> <span data-ttu-id="22f63-228">Tymczasowe hasła nie są zsynchronizowane z usługą Azure AD.</span><span class="sxs-lookup"><span data-stu-id="22f63-228">Temporary passwords are not synchronized with Azure AD.</span></span>

2. <span data-ttu-id="22f63-229">Jeśli hasło hello wygląda poprawnie w usłudze Active Directory, wykonaj użytkownika hello hello aparatu synchronizacji.</span><span class="sxs-lookup"><span data-stu-id="22f63-229">If hello password looks correct in Active Directory, follow hello user in hello sync engine.</span></span> <span data-ttu-id="22f63-230">Przez następujący użytkownik hello z lokalnej usługi Active Directory tooAzure AD widać, czy w obiekcie hello jest opisem błędu.</span><span class="sxs-lookup"><span data-stu-id="22f63-230">By following hello user from on-premises Active Directory tooAzure AD, you can see whether there is a descriptive error on hello object.</span></span>

    <span data-ttu-id="22f63-231">a.</span><span class="sxs-lookup"><span data-stu-id="22f63-231">a.</span></span> <span data-ttu-id="22f63-232">Uruchom hello [Menedżera usługi synchronizacji](active-directory-aadconnectsync-service-manager-ui.md).</span><span class="sxs-lookup"><span data-stu-id="22f63-232">Start hello [Synchronization Service Manager](active-directory-aadconnectsync-service-manager-ui.md).</span></span>

    <span data-ttu-id="22f63-233">b.</span><span class="sxs-lookup"><span data-stu-id="22f63-233">b.</span></span> <span data-ttu-id="22f63-234">Kliknij przycisk **łączniki**.</span><span class="sxs-lookup"><span data-stu-id="22f63-234">Click **Connectors**.</span></span>

    <span data-ttu-id="22f63-235">c.</span><span class="sxs-lookup"><span data-stu-id="22f63-235">c.</span></span> <span data-ttu-id="22f63-236">Wybierz hello **łącznika usługi Active Directory** którym znajduje się hello użytkownika.</span><span class="sxs-lookup"><span data-stu-id="22f63-236">Select hello **Active Directory Connector** where hello user is located.</span></span>

    <span data-ttu-id="22f63-237">d.</span><span class="sxs-lookup"><span data-stu-id="22f63-237">d.</span></span> <span data-ttu-id="22f63-238">Wybierz **wyszukiwania przestrzeni łącznika**.</span><span class="sxs-lookup"><span data-stu-id="22f63-238">Select **Search Connector Space**.</span></span>

    <span data-ttu-id="22f63-239">e.</span><span class="sxs-lookup"><span data-stu-id="22f63-239">e.</span></span> <span data-ttu-id="22f63-240">W hello **zakres** wybierz opcję **nazwa Wyróżniająca lub zakotwiczenia**, a następnie wprowadź hello Pełna nazwa Wyróżniająca użytkownika hello rozwiązywania problemów.</span><span class="sxs-lookup"><span data-stu-id="22f63-240">In hello **Scope** box, select **DN or Anchor**, and then enter hello full DN of hello user you are troubleshooting.</span></span>

    ![Wyszukaj użytkownika w przestrzeni łącznika o nazwie Wyróżniającej](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/searchcs.png)  

    <span data-ttu-id="22f63-242">f.</span><span class="sxs-lookup"><span data-stu-id="22f63-242">f.</span></span> <span data-ttu-id="22f63-243">Znajdź użytkownika hello szukasz, a następnie kliknij przycisk **właściwości** toosee hello wszystkie atrybuty.</span><span class="sxs-lookup"><span data-stu-id="22f63-243">Locate hello user you are looking for, and then click **Properties** toosee all hello attributes.</span></span> <span data-ttu-id="22f63-244">Sprawdź, czy hello użytkownika nie jest w wyniku wyszukiwania hello, Twoje [reguły filtrowania](active-directory-aadconnectsync-configure-filtering.md) i upewnij się, że uruchamiasz [Zastosuj i Sprawdź zmiany](active-directory-aadconnectsync-configure-filtering.md#apply-and-verify-changes) dla tooappear użytkownika hello w Connect.</span><span class="sxs-lookup"><span data-stu-id="22f63-244">If hello user is not in hello search result, verify your [filtering rules](active-directory-aadconnectsync-configure-filtering.md) and make sure that you run [Apply and verify changes](active-directory-aadconnectsync-configure-filtering.md#apply-and-verify-changes) for hello user tooappear in Connect.</span></span>

    <span data-ttu-id="22f63-245">g.</span><span class="sxs-lookup"><span data-stu-id="22f63-245">g.</span></span> <span data-ttu-id="22f63-246">Kliknij zeszłym tygodniu toosee hello hasła synchronizacji Szczegóły obiektu hello hello **dziennika**.</span><span class="sxs-lookup"><span data-stu-id="22f63-246">toosee hello password sync details of hello object for hello past week, click **Log**.</span></span>  

    ![Szczegóły dziennika obiektu](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/csobjectlog.png)  

    <span data-ttu-id="22f63-248">Jeśli dziennik obiektu hello jest pusta, Azure AD Connect została skrót hasła hello tooread z usługi Active Directory.</span><span class="sxs-lookup"><span data-stu-id="22f63-248">If hello object log is empty, Azure AD Connect has been unable tooread hello password hash from Active Directory.</span></span> <span data-ttu-id="22f63-249">Kontynuuj rozwiązywanie problemów z [błędów połączenia](#connectivity-errors).</span><span class="sxs-lookup"><span data-stu-id="22f63-249">Continue your troubleshooting with [Connectivity Errors](#connectivity-errors).</span></span> <span data-ttu-id="22f63-250">Jeśli widzisz innych wartości niż **Powodzenie**, można znaleźć tabeli toohello [Dziennik synchronizacji haseł](#password-sync-log).</span><span class="sxs-lookup"><span data-stu-id="22f63-250">If you see any other value than **success**, refer toohello table in [Password sync log](#password-sync-log).</span></span>

    <span data-ttu-id="22f63-251">h.</span><span class="sxs-lookup"><span data-stu-id="22f63-251">h.</span></span> <span data-ttu-id="22f63-252">Wybierz hello **elementy powiązane** karcie i upewnij się, reguły synchronizacji co najmniej jeden w hello **PasswordSync** kolumna jest **True**.</span><span class="sxs-lookup"><span data-stu-id="22f63-252">Select hello **lineage** tab, and make sure that at least one sync rule in hello **PasswordSync** column is **True**.</span></span> <span data-ttu-id="22f63-253">W konfiguracji domyślnej hello jest hello Nazwa reguły synchronizacji hello **w z usługi AD - AccountEnabled użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="22f63-253">In hello default configuration, hello name of hello sync rule is **In from AD - User AccountEnabled**.</span></span>  

    ![Elementy powiązane informacje o użytkowniku](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/cspasswordsync.png)  

    <span data-ttu-id="22f63-255">i.</span><span class="sxs-lookup"><span data-stu-id="22f63-255">i.</span></span> <span data-ttu-id="22f63-256">Kliknij przycisk **właściwości obiektu Metaverse** toodisplay listę atrybutów użytkowników.</span><span class="sxs-lookup"><span data-stu-id="22f63-256">Click **Metaverse Object Properties** toodisplay a list of user attributes.</span></span>  

    ![Informacje magazynie metaverse](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/mvpasswordsync.png)  

    <span data-ttu-id="22f63-258">Sprawdź, czy jest nie **cloudFiltered** atrybutu.</span><span class="sxs-lookup"><span data-stu-id="22f63-258">Verify that there is no **cloudFiltered** attribute present.</span></span> <span data-ttu-id="22f63-259">Upewnij się, że atrybuty domeny hello (domainFQDN i domainNetBios) jest hello oczekiwanych wartości.</span><span class="sxs-lookup"><span data-stu-id="22f63-259">Make sure that hello domain attributes (domainFQDN and domainNetBios) have hello expected values.</span></span>

    <span data-ttu-id="22f63-260">j.</span><span class="sxs-lookup"><span data-stu-id="22f63-260">j.</span></span> <span data-ttu-id="22f63-261">Kliknij przycisk hello **łączniki** kartę. Upewnij się, że widoczny tooboth łączniki lokalnej usługi Active Directory i Azure AD.</span><span class="sxs-lookup"><span data-stu-id="22f63-261">Click hello **Connectors** tab. Make sure that you see connectors tooboth on-premises Active Directory and Azure AD.</span></span>

    ![Informacje magazynie metaverse](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/mvconnectors.png)  

    <span data-ttu-id="22f63-263">k.</span><span class="sxs-lookup"><span data-stu-id="22f63-263">k.</span></span> <span data-ttu-id="22f63-264">Wybierz hello wiersza, który reprezentuje usługi Azure AD, kliknij przycisk **właściwości**, a następnie kliknij przycisk hello **elementy powiązane** kartę hello łącznika miejsca obiektu powinien mieć Reguła ruchu wychodzącego w hello **PasswordSync** zbyt zestawu kolumn**True**.</span><span class="sxs-lookup"><span data-stu-id="22f63-264">Select hello row that represents Azure AD, click **Properties**, and then click hello **Lineage** tab. hello connector space object should have an outbound rule in hello **PasswordSync** column set too**True**.</span></span> <span data-ttu-id="22f63-265">W konfiguracji domyślnej hello jest hello Nazwa reguły synchronizacji hello **się tooAAD — użytkownik przyłączyć**.</span><span class="sxs-lookup"><span data-stu-id="22f63-265">In hello default configuration, hello name of hello sync rule is **Out tooAAD - User Join**.</span></span>  

    ![Okno dialogowe właściwości obiektu obszaru łącznika](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/cspasswordsync2.png)  

### <a name="password-sync-log"></a><span data-ttu-id="22f63-267">Dziennik synchronizacji haseł</span><span class="sxs-lookup"><span data-stu-id="22f63-267">Password sync log</span></span>
<span data-ttu-id="22f63-268">Witaj w kolumnie Stan może mieć hello następujące wartości:</span><span class="sxs-lookup"><span data-stu-id="22f63-268">hello status column can have hello following values:</span></span>

| <span data-ttu-id="22f63-269">Stan</span><span class="sxs-lookup"><span data-stu-id="22f63-269">Status</span></span> | <span data-ttu-id="22f63-270">Opis</span><span class="sxs-lookup"><span data-stu-id="22f63-270">Description</span></span> |
| --- | --- |
| <span data-ttu-id="22f63-271">Powodzenie</span><span class="sxs-lookup"><span data-stu-id="22f63-271">Success</span></span> |<span data-ttu-id="22f63-272">Hasło zostało pomyślnie zsynchronizowane.</span><span class="sxs-lookup"><span data-stu-id="22f63-272">Password has been successfully synchronized.</span></span> |
| <span data-ttu-id="22f63-273">FilteredByTarget</span><span class="sxs-lookup"><span data-stu-id="22f63-273">FilteredByTarget</span></span> |<span data-ttu-id="22f63-274">Hasło jest ustawiane za**użytkownik musi zmienić hasło przy następnym logowaniu**.</span><span class="sxs-lookup"><span data-stu-id="22f63-274">Password is set too**User must change password at next logon**.</span></span> <span data-ttu-id="22f63-275">Hasło nie zostały zsynchronizowane.</span><span class="sxs-lookup"><span data-stu-id="22f63-275">Password has not been synchronized.</span></span> |
| <span data-ttu-id="22f63-276">NoTargetConnection</span><span class="sxs-lookup"><span data-stu-id="22f63-276">NoTargetConnection</span></span> |<span data-ttu-id="22f63-277">Brak obiektu hello metaverse lub przestrzeni łącznika hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="22f63-277">No object in hello metaverse or in hello Azure AD connector space.</span></span> |
| <span data-ttu-id="22f63-278">SourceConnectorNotPresent</span><span class="sxs-lookup"><span data-stu-id="22f63-278">SourceConnectorNotPresent</span></span> |<span data-ttu-id="22f63-279">Nie znaleziono w przestrzeni łącznika usługi Active Directory lokalne powitania obiektu.</span><span class="sxs-lookup"><span data-stu-id="22f63-279">No object found in hello on-premises Active Directory connector space.</span></span> |
| <span data-ttu-id="22f63-280">TargetNotExportedToDirectory</span><span class="sxs-lookup"><span data-stu-id="22f63-280">TargetNotExportedToDirectory</span></span> |<span data-ttu-id="22f63-281">Obiekt Hello w hello przestrzeni łącznika usługi Azure AD nie zostały wyeksportowane.</span><span class="sxs-lookup"><span data-stu-id="22f63-281">hello object in hello Azure AD connector space has not yet been exported.</span></span> |
| <span data-ttu-id="22f63-282">MigratedCheckDetailsForMoreInfo</span><span class="sxs-lookup"><span data-stu-id="22f63-282">MigratedCheckDetailsForMoreInfo</span></span> |<span data-ttu-id="22f63-283">Wpis dziennika został utworzony przed kompilacji 1.0.9125.0 i jest wyświetlany w stanie starszej wersji.</span><span class="sxs-lookup"><span data-stu-id="22f63-283">Log entry was created before build 1.0.9125.0 and is shown in its legacy state.</span></span> |
| <span data-ttu-id="22f63-284">Błąd</span><span class="sxs-lookup"><span data-stu-id="22f63-284">Error</span></span> |<span data-ttu-id="22f63-285">Usługa zwróciła nieznany błąd.</span><span class="sxs-lookup"><span data-stu-id="22f63-285">Service returned an unknown error.</span></span> |
| <span data-ttu-id="22f63-286">Nieznany</span><span class="sxs-lookup"><span data-stu-id="22f63-286">Unknown</span></span> |<span data-ttu-id="22f63-287">Wystąpił błąd podczas próby tooprocess partii skrótów haseł.</span><span class="sxs-lookup"><span data-stu-id="22f63-287">An error occurred while trying tooprocess a batch of password hashes.</span></span>  |
| <span data-ttu-id="22f63-288">MissingAttribute</span><span class="sxs-lookup"><span data-stu-id="22f63-288">MissingAttribute</span></span> |<span data-ttu-id="22f63-289">Określone atrybuty (na przykład protokołu Kerberos wyznaczania wartości skrótu) wymagane przez usługi domenowe Azure AD nie są dostępne.</span><span class="sxs-lookup"><span data-stu-id="22f63-289">Specific attributes (for example, Kerberos hash) required by Azure AD Domain Services are not available.</span></span> |
| <span data-ttu-id="22f63-290">RetryRequestedByTarget</span><span class="sxs-lookup"><span data-stu-id="22f63-290">RetryRequestedByTarget</span></span> |<span data-ttu-id="22f63-291">Określone atrybuty (na przykład protokołu Kerberos wyznaczania wartości skrótu) wymagane przez usługi domenowe Azure AD nie były wcześniej dostępne.</span><span class="sxs-lookup"><span data-stu-id="22f63-291">Specific attributes (for example, Kerberos hash) required by Azure AD Domain Services were not available previously.</span></span> <span data-ttu-id="22f63-292">Następuje próba tooresynchronize hello skrót hasła użytkownika.</span><span class="sxs-lookup"><span data-stu-id="22f63-292">An attempt tooresynchronize hello user's password hash is made.</span></span> |

## <a name="scripts-toohelp-troubleshooting"></a><span data-ttu-id="22f63-293">Rozwiązywanie problemów z toohelp skryptów</span><span class="sxs-lookup"><span data-stu-id="22f63-293">Scripts toohelp troubleshooting</span></span>

### <a name="get-hello-status-of-password-sync-settings"></a><span data-ttu-id="22f63-294">Pobierz stan hello ustawień synchronizacji haseł</span><span class="sxs-lookup"><span data-stu-id="22f63-294">Get hello status of password sync settings</span></span>
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
        Write-Warning "More than one Azure AD Connectors found. Please update hello script toouse hello appropriate Connector."
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

#### <a name="trigger-a-full-sync-of-all-passwords"></a><span data-ttu-id="22f63-295">Wyzwalacz pełnej synchronizacji haseł wszystkich</span><span class="sxs-lookup"><span data-stu-id="22f63-295">Trigger a full sync of all passwords</span></span>
> [!NOTE]
> <span data-ttu-id="22f63-296">Ten skrypt należy uruchomić tylko raz.</span><span class="sxs-lookup"><span data-stu-id="22f63-296">Run this script only once.</span></span> <span data-ttu-id="22f63-297">Jeśli potrzebujesz toorun on więcej niż raz, czegoś innego jest hello problem.</span><span class="sxs-lookup"><span data-stu-id="22f63-297">If you need toorun it more than once, something else is hello problem.</span></span> <span data-ttu-id="22f63-298">tootroubleshoot hello problem, skontaktuj się z pomocą techniczną firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="22f63-298">tootroubleshoot hello problem, contact Microsoft support.</span></span>

<span data-ttu-id="22f63-299">Możesz wyzwolić pełną synchronizację wszystkie hasła przy użyciu hello następującego skryptu:</span><span class="sxs-lookup"><span data-stu-id="22f63-299">You can trigger a full sync of all passwords by using hello following script:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="22f63-300">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="22f63-300">Next steps</span></span>
* [<span data-ttu-id="22f63-301">Implementowanie synchronizacji haseł z synchronizacji Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="22f63-301">Implementing password synchronization with Azure AD Connect sync</span></span>](active-directory-aadconnectsync-implement-password-synchronization.md)
* [<span data-ttu-id="22f63-302">Azure AD Connect Sync: Dostosowywanie opcji synchronizacji</span><span class="sxs-lookup"><span data-stu-id="22f63-302">Azure AD Connect Sync: Customizing synchronization options</span></span>](active-directory-aadconnectsync-whatis.md)
* [<span data-ttu-id="22f63-303">Integrowanie tożsamości lokalnych z usługą Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="22f63-303">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
