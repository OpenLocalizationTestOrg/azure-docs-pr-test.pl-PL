---
title: "aaaConnectors w hello interfejsu użytkownika programu Azure AD Synchronization Service Manager | Dokumentacja firmy Microsoft"
description: "Zrozumienie hello kartę łączników w hello Menedżera usługi synchronizacji programu Azure AD Connect."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 60f1d979-8e6d-4460-aaab-747fffedfc1e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c0969630313178b1e299385b1289360c8f787cb5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="using-connectors-with-hello-azure-ad-connect-sync-service-manager"></a><span data-ttu-id="21111-103">Za pomocą łączników o hello Azure AD Connect synchronizacji programu Service Manager</span><span class="sxs-lookup"><span data-stu-id="21111-103">Using connectors with hello Azure AD Connect Sync Service Manager</span></span>

![Menedżera usługi synchronizacji](./media/active-directory-aadconnectsync-service-manager-ui/connectors.png)

<span data-ttu-id="21111-105">Karta łączniki Hello jest używany toomanage, wszystkie aparatu synchronizacji hello systemów jest połączona z.</span><span class="sxs-lookup"><span data-stu-id="21111-105">hello Connectors tab is used toomanage all systems hello sync engine is connected to.</span></span>

## <a name="connector-actions"></a><span data-ttu-id="21111-106">Akcje łącznika</span><span class="sxs-lookup"><span data-stu-id="21111-106">Connector actions</span></span>
| <span data-ttu-id="21111-107">Akcja</span><span class="sxs-lookup"><span data-stu-id="21111-107">Action</span></span> | <span data-ttu-id="21111-108">Komentarz</span><span class="sxs-lookup"><span data-stu-id="21111-108">Comment</span></span> |
| --- | --- |
| <span data-ttu-id="21111-109">Przycisk Utwórz</span><span class="sxs-lookup"><span data-stu-id="21111-109">Create</span></span> |<span data-ttu-id="21111-110">Nie używaj.</span><span class="sxs-lookup"><span data-stu-id="21111-110">Do not use.</span></span> <span data-ttu-id="21111-111">Połączenie tooadditional AD lasów, należy użyć Kreatora instalacji hello.</span><span class="sxs-lookup"><span data-stu-id="21111-111">For connecting tooadditional AD forests, use hello installation wizard.</span></span> |
| <span data-ttu-id="21111-112">Właściwości</span><span class="sxs-lookup"><span data-stu-id="21111-112">Properties</span></span> |<span data-ttu-id="21111-113">Używany do domeny i jednostki Organizacyjnej filtrowania.</span><span class="sxs-lookup"><span data-stu-id="21111-113">Used for domain and OU filtering.</span></span> |
| [<span data-ttu-id="21111-114">Usuwanie</span><span class="sxs-lookup"><span data-stu-id="21111-114">Delete</span></span>](#delete) |<span data-ttu-id="21111-115">Używane tooeither usunąć dane hello hello łącznika miejsca lub toodelete połączenia tooa lasu.</span><span class="sxs-lookup"><span data-stu-id="21111-115">Used tooeither delete hello data in hello connector space or toodelete connection tooa forest.</span></span> |
| [<span data-ttu-id="21111-116">Konfigurowanie profilów uruchamiania</span><span class="sxs-lookup"><span data-stu-id="21111-116">Configure Run Profiles</span></span>](#configure-run-profiles) |<span data-ttu-id="21111-117">Z wyjątkiem domeny filtrowania nic tooconfigure tutaj.</span><span class="sxs-lookup"><span data-stu-id="21111-117">Except for domain filtering, nothing tooconfigure here.</span></span> <span data-ttu-id="21111-118">Akcję tę można stosować profilów uruchamiania toosee już skonfigurowane.</span><span class="sxs-lookup"><span data-stu-id="21111-118">You can use this action toosee already configured run profiles.</span></span> |
| <span data-ttu-id="21111-119">Uruchom polecenie</span><span class="sxs-lookup"><span data-stu-id="21111-119">Run</span></span> |<span data-ttu-id="21111-120">Używane toostart jednorazowy Uruchom profilu.</span><span class="sxs-lookup"><span data-stu-id="21111-120">Used toostart a one-off run of a profile.</span></span> |
| <span data-ttu-id="21111-121">Stop</span><span class="sxs-lookup"><span data-stu-id="21111-121">Stop</span></span> |<span data-ttu-id="21111-122">Zatrzymuje łącznika aktualnie uruchomione profilu.</span><span class="sxs-lookup"><span data-stu-id="21111-122">Stops a Connector currently running a profile.</span></span> |
| <span data-ttu-id="21111-123">Łącznik eksportu</span><span class="sxs-lookup"><span data-stu-id="21111-123">Export Connector</span></span> |<span data-ttu-id="21111-124">Nie używaj.</span><span class="sxs-lookup"><span data-stu-id="21111-124">Do not use.</span></span> |
| <span data-ttu-id="21111-125">Importuj łącznika</span><span class="sxs-lookup"><span data-stu-id="21111-125">Import Connector</span></span> |<span data-ttu-id="21111-126">Nie używaj.</span><span class="sxs-lookup"><span data-stu-id="21111-126">Do not use.</span></span> |
| <span data-ttu-id="21111-127">Łącznik aktualizacji</span><span class="sxs-lookup"><span data-stu-id="21111-127">Update Connector</span></span> |<span data-ttu-id="21111-128">Nie używaj.</span><span class="sxs-lookup"><span data-stu-id="21111-128">Do not use.</span></span> |
| <span data-ttu-id="21111-129">Odśwież schemat</span><span class="sxs-lookup"><span data-stu-id="21111-129">Refresh Schema</span></span> |<span data-ttu-id="21111-130">Odświeża hello pamięci podręcznej schematu.</span><span class="sxs-lookup"><span data-stu-id="21111-130">Refreshes hello cached schema.</span></span> <span data-ttu-id="21111-131">Jest toouse preferowanych opcji powitania w Kreatorze instalacji hello zamiast tego należy również od który aktualizacje synchronizacji reguły.</span><span class="sxs-lookup"><span data-stu-id="21111-131">It is preferred toouse hello option in hello installation wizard instead, since that also updates sync rules.</span></span> |
| [<span data-ttu-id="21111-132">Obszar łączników wyszukiwania</span><span class="sxs-lookup"><span data-stu-id="21111-132">Search Connector Space</span></span>](#search-connector-space) |<span data-ttu-id="21111-133">Obiekty toofind używane i zbyt[wykonaj obiekt i jego danych za pośrednictwem systemu hello](#follow-an-object-and-its-data-through-the-system).</span><span class="sxs-lookup"><span data-stu-id="21111-133">Used toofind objects and too[Follow an object and its data through hello system](#follow-an-object-and-its-data-through-the-system).</span></span> |

### <a name="delete"></a><span data-ttu-id="21111-134">Usuwanie</span><span class="sxs-lookup"><span data-stu-id="21111-134">Delete</span></span>
<span data-ttu-id="21111-135">Akcja usuwania Hello jest używany dla dwóch różnych rzeczy.</span><span class="sxs-lookup"><span data-stu-id="21111-135">hello delete action is used for two different things.</span></span>  
![Menedżera usługi synchronizacji](./media/active-directory-aadconnectsync-service-manager-ui/connectordelete.png)

<span data-ttu-id="21111-137">Witaj opcja **usunąć tylko przestrzeni łącznika** powoduje usunięcie wszystkich danych, ale zachować hello konfiguracja.</span><span class="sxs-lookup"><span data-stu-id="21111-137">hello option **Delete connector space only** removes all data, but keep hello configuration.</span></span>

<span data-ttu-id="21111-138">Witaj opcja **usunąć Connector i łącznika miejsca** usuwa hello danych i konfiguracji hello.</span><span class="sxs-lookup"><span data-stu-id="21111-138">hello option **Delete Connector and connector space** removes hello data and hello configuration.</span></span> <span data-ttu-id="21111-139">Ta opcja jest używana, gdy tooconnect tooa lasu nie mają już.</span><span class="sxs-lookup"><span data-stu-id="21111-139">This option is used when you do not want tooconnect tooa forest anymore.</span></span>

<span data-ttu-id="21111-140">Obie te opcje synchronizować wszystkie obiekty i zaktualizować hello metaverse obiektów.</span><span class="sxs-lookup"><span data-stu-id="21111-140">Both options sync all objects and update hello metaverse objects.</span></span> <span data-ttu-id="21111-141">Ta akcja jest operacją wymagającą dużo czasu.</span><span class="sxs-lookup"><span data-stu-id="21111-141">This action is a long running operation.</span></span>

### <a name="configure-run-profiles"></a><span data-ttu-id="21111-142">Konfigurowanie profilów uruchamiania</span><span class="sxs-lookup"><span data-stu-id="21111-142">Configure Run Profiles</span></span>
<span data-ttu-id="21111-143">Ta opcja umożliwia hello toosee skonfigurowane dla łącznika profilów uruchamiania.</span><span class="sxs-lookup"><span data-stu-id="21111-143">This option allows you toosee hello run profiles configured for a Connector.</span></span>

![Menedżera usługi synchronizacji](./media/active-directory-aadconnectsync-service-manager-ui/configurerunprofiles.png)

### <a name="search-connector-space"></a><span data-ttu-id="21111-145">Obszar łączników wyszukiwania</span><span class="sxs-lookup"><span data-stu-id="21111-145">Search Connector Space</span></span>
<span data-ttu-id="21111-146">Akcja przestrzeni łącznika wyszukiwania Hello jest przydatne toofind obiektów i rozwiązywania problemów danych.</span><span class="sxs-lookup"><span data-stu-id="21111-146">hello search connector space action is useful toofind objects and troubleshoot data issues.</span></span>

![Menedżera usługi synchronizacji](./media/active-directory-aadconnectsync-service-manager-ui/cssearch.png)

<span data-ttu-id="21111-148">Najpierw wybrać **zakres**.</span><span class="sxs-lookup"><span data-stu-id="21111-148">Start by selecting a **scope**.</span></span> <span data-ttu-id="21111-149">Można wyszukiwać na podstawie danych (RDN, nazwa Wyróżniająca, zakotwiczenia, poddrzewa), lub stanu obiektu hello (wszystkie inne opcje).</span><span class="sxs-lookup"><span data-stu-id="21111-149">You can search based on data (RDN, DN, Anchor, Sub-Tree), or state of hello object (all other options).</span></span>  
<span data-ttu-id="21111-150">![Menedżera usługi synchronizacji](./media/active-directory-aadconnectsync-service-manager-ui/cssearchscope.png)</span><span class="sxs-lookup"><span data-stu-id="21111-150">![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/cssearchscope.png)</span></span>  
<span data-ttu-id="21111-151">Jeśli na przykład wykonać wyszukiwanie poddrzewa, możesz uzyskać wszystkie obiekty w jednej jednostce Organizacyjnej.</span><span class="sxs-lookup"><span data-stu-id="21111-151">If you for example do a Sub-Tree search, you get all objects in one OU.</span></span>  
<span data-ttu-id="21111-152">![Menedżera usługi synchronizacji](./media/active-directory-aadconnectsync-service-manager-ui/cssearchsubtree.png)</span><span class="sxs-lookup"><span data-stu-id="21111-152">![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/cssearchsubtree.png)</span></span>  
<span data-ttu-id="21111-153">W tym miejscu. Wybierz obiekt, wybierz **właściwości**, i [po nim](active-directory-aadconnectsync-troubleshoot-object-not-syncing.md) z hello źródła łącznika, za pośrednictwem hello metaverse i toohello docelowych łącznika miejsca.</span><span class="sxs-lookup"><span data-stu-id="21111-153">From this grid you can select an object, select **properties**, and [follow it](active-directory-aadconnectsync-troubleshoot-object-not-syncing.md) from hello source connector space, through hello metaverse, and toohello target connector space.</span></span>

### <a name="changing-hello-ad-ds-account-password"></a><span data-ttu-id="21111-154">Zmiana hasła konta hello AD DS</span><span class="sxs-lookup"><span data-stu-id="21111-154">Changing hello AD DS account password</span></span>
<span data-ttu-id="21111-155">Jeśli zmienisz hasło konta hello hello usługi synchronizacji nie będą już mogli tooimport/export zmiany tooon lokalnych AD.</span><span class="sxs-lookup"><span data-stu-id="21111-155">If you change hello account password, hello Synchronization Service will no longer be able tooimport/export changes tooon-premises AD.</span></span>   <span data-ttu-id="21111-156">Może pojawić się następujące hello:</span><span class="sxs-lookup"><span data-stu-id="21111-156">You may see hello following:</span></span>

- <span data-ttu-id="21111-157">krok importu/eksportu Hello na powitania łącznika AD zakończy się niepowodzeniem z powodu błędu "nie-start — poświadczenia".</span><span class="sxs-lookup"><span data-stu-id="21111-157">hello import/export step for hello AD connector fails with "no-start-credentials" error.</span></span>
- <span data-ttu-id="21111-158">W Podglądzie zdarzeń systemu Windows w dzienniku zdarzeń aplikacji hello zawiera błąd 6000 identyfikator zdarzenia i komunikat "hello zarządzania toorun agenta"contoso.com"nie powiodło się, ponieważ poświadczenia hello była nieprawidłowa."</span><span class="sxs-lookup"><span data-stu-id="21111-158">Under Windows Event Viewer, hello application event log contains an error with Event ID 6000 and message “hello management agent “contoso.com” failed toorun because hello credentials were invalid.”</span></span>

<span data-ttu-id="21111-159">tooresolve hello wystawiania, konto użytkownika hello usług AD DS aktualizacji przy użyciu następujących hello:</span><span class="sxs-lookup"><span data-stu-id="21111-159">tooresolve hello issue, update hello AD DS user account using hello following:</span></span>


1. <span data-ttu-id="21111-160">Uruchom hello Synchronization Service Manager (START → usługa synchronizacji).</span><span class="sxs-lookup"><span data-stu-id="21111-160">Start hello Synchronization Service Manager (START → Synchronization Service).</span></span>
</br><span data-ttu-id="21111-161">![Menedżera usługi synchronizacji](./media/active-directory-aadconnectsync-service-manager-ui/startmenu.png)</span><span class="sxs-lookup"><span data-stu-id="21111-161">![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/startmenu.png)</span></span>
2. <span data-ttu-id="21111-162">Przejdź toohello **łączniki** kartę.</span><span class="sxs-lookup"><span data-stu-id="21111-162">Go toohello **Connectors** tab.</span></span>
3. <span data-ttu-id="21111-163">Wybierz hello łączniku usługi AD, który jest skonfigurowany toouse hello konta usług AD DS.</span><span class="sxs-lookup"><span data-stu-id="21111-163">Select hello AD Connector which is configured toouse hello AD DS account.</span></span>
4. <span data-ttu-id="21111-164">W obszarze akcje, wybierz **właściwości**.</span><span class="sxs-lookup"><span data-stu-id="21111-164">Under Actions, select **Properties**.</span></span>
5. <span data-ttu-id="21111-165">W wyskakującym oknie dialogowym hello wybierz opcję Połącz tooActive katalogu lasu:</span><span class="sxs-lookup"><span data-stu-id="21111-165">In hello pop-up dialog, select Connect tooActive Directory Forest:</span></span>
6. <span data-ttu-id="21111-166">Nazwa lasu Hello wskazuje hello odpowiedniej lokalnej usługi AD.</span><span class="sxs-lookup"><span data-stu-id="21111-166">hello Forest name indicates hello corresponding on-prem AD.</span></span>
7. <span data-ttu-id="21111-167">Nazwa użytkownika Hello wskazuje hello AD DS konto używane do synchronizacji.</span><span class="sxs-lookup"><span data-stu-id="21111-167">hello User name indicates hello AD DS account used for synchronization.</span></span>
8. <span data-ttu-id="21111-168">Wprowadź nowe hasło hello hello AD DS konta w pole tekstowe hasła hello ![Azure AD Connect synchronizacji szyfrowania klucz narzędzia](media/active-directory-aadconnectsync-encryption-key/key6.png)</span><span class="sxs-lookup"><span data-stu-id="21111-168">Enter hello new password of hello AD DS account in hello Password textbox ![Azure AD Connect Sync Encryption Key Utility](media/active-directory-aadconnectsync-encryption-key/key6.png)</span></span>
9. <span data-ttu-id="21111-169">Kliknij przycisk OK toosave hello nowe hasło, a następnie ponownie uruchom hello usługi synchronizacji tooremove hello stare hasło z pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="21111-169">Click OK toosave hello new password and restart hello Synchronization Service tooremove hello old password from memory cache.</span></span>



## <a name="next-steps"></a><span data-ttu-id="21111-170">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="21111-170">Next steps</span></span>
<span data-ttu-id="21111-171">Dowiedz się więcej o hello [synchronizacja programu Azure AD Connect](active-directory-aadconnectsync-whatis.md) konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="21111-171">Learn more about hello [Azure AD Connect sync](active-directory-aadconnectsync-whatis.md) configuration.</span></span>

<span data-ttu-id="21111-172">Dowiedz się więcej na temat [integrowania tożsamości lokalnych z usługą Azure Active Directory](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="21111-172">Learn more about [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>
