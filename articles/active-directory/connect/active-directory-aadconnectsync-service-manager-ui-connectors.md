---
title: "Łączniki w interfejsie użytkownika programu Azure AD Synchronization Service Manager | Dokumentacja firmy Microsoft"
description: "Dowiedz się na karcie łączniki Menedżera usługi synchronizacji programu Azure AD Connect."
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
ms.openlocfilehash: c0fae4b1755ca95466eeffb5ce61c1c7855d7381
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="using-connectors-with-the-azure-ad-connect-sync-service-manager"></a><span data-ttu-id="0fe18-103">Używanie łączników przy użyciu usługi Azure AD Connect synchronizacji Menedżera usług</span><span class="sxs-lookup"><span data-stu-id="0fe18-103">Using connectors with the Azure AD Connect Sync Service Manager</span></span>

![Menedżera usługi synchronizacji](./media/active-directory-aadconnectsync-service-manager-ui/connectors.png)

<span data-ttu-id="0fe18-105">Karta łączników jest używana do zarządzania wszystkimi systemami aparat synchronizacji jest połączona z.</span><span class="sxs-lookup"><span data-stu-id="0fe18-105">The Connectors tab is used to manage all systems the sync engine is connected to.</span></span>

## <a name="connector-actions"></a><span data-ttu-id="0fe18-106">Akcje łącznika</span><span class="sxs-lookup"><span data-stu-id="0fe18-106">Connector actions</span></span>
| <span data-ttu-id="0fe18-107">Akcja</span><span class="sxs-lookup"><span data-stu-id="0fe18-107">Action</span></span> | <span data-ttu-id="0fe18-108">Komentarz</span><span class="sxs-lookup"><span data-stu-id="0fe18-108">Comment</span></span> |
| --- | --- |
| <span data-ttu-id="0fe18-109">Przycisk Utwórz</span><span class="sxs-lookup"><span data-stu-id="0fe18-109">Create</span></span> |<span data-ttu-id="0fe18-110">Nie używaj.</span><span class="sxs-lookup"><span data-stu-id="0fe18-110">Do not use.</span></span> <span data-ttu-id="0fe18-111">Do połączenia dodatkowych lasów usługi AD, należy użyć Kreatora instalacji.</span><span class="sxs-lookup"><span data-stu-id="0fe18-111">For connecting to additional AD forests, use the installation wizard.</span></span> |
| <span data-ttu-id="0fe18-112">Właściwości</span><span class="sxs-lookup"><span data-stu-id="0fe18-112">Properties</span></span> |<span data-ttu-id="0fe18-113">Używany do domeny i jednostki Organizacyjnej filtrowania.</span><span class="sxs-lookup"><span data-stu-id="0fe18-113">Used for domain and OU filtering.</span></span> |
| [<span data-ttu-id="0fe18-114">Usuwanie</span><span class="sxs-lookup"><span data-stu-id="0fe18-114">Delete</span></span>](#delete) |<span data-ttu-id="0fe18-115">Używane do albo usunąć dane w przestrzeni łącznika lub usunąć połączenia do lasu.</span><span class="sxs-lookup"><span data-stu-id="0fe18-115">Used to either delete the data in the connector space or to delete connection to a forest.</span></span> |
| [<span data-ttu-id="0fe18-116">Konfigurowanie profilów uruchamiania</span><span class="sxs-lookup"><span data-stu-id="0fe18-116">Configure Run Profiles</span></span>](#configure-run-profiles) |<span data-ttu-id="0fe18-117">Z wyjątkiem domeny filtrowania, nic nie można skonfigurować w tym miejscu.</span><span class="sxs-lookup"><span data-stu-id="0fe18-117">Except for domain filtering, nothing to configure here.</span></span> <span data-ttu-id="0fe18-118">Ta akcja umożliwia Zobacz już skonfigurowane profile uruchamiania.</span><span class="sxs-lookup"><span data-stu-id="0fe18-118">You can use this action to see already configured run profiles.</span></span> |
| <span data-ttu-id="0fe18-119">Uruchom polecenie</span><span class="sxs-lookup"><span data-stu-id="0fe18-119">Run</span></span> |<span data-ttu-id="0fe18-120">Używane do uruchamiania jednorazowe Uruchom profilu.</span><span class="sxs-lookup"><span data-stu-id="0fe18-120">Used to start a one-off run of a profile.</span></span> |
| <span data-ttu-id="0fe18-121">Stop</span><span class="sxs-lookup"><span data-stu-id="0fe18-121">Stop</span></span> |<span data-ttu-id="0fe18-122">Zatrzymuje łącznika aktualnie uruchomione profilu.</span><span class="sxs-lookup"><span data-stu-id="0fe18-122">Stops a Connector currently running a profile.</span></span> |
| <span data-ttu-id="0fe18-123">Łącznik eksportu</span><span class="sxs-lookup"><span data-stu-id="0fe18-123">Export Connector</span></span> |<span data-ttu-id="0fe18-124">Nie używaj.</span><span class="sxs-lookup"><span data-stu-id="0fe18-124">Do not use.</span></span> |
| <span data-ttu-id="0fe18-125">Importuj łącznika</span><span class="sxs-lookup"><span data-stu-id="0fe18-125">Import Connector</span></span> |<span data-ttu-id="0fe18-126">Nie używaj.</span><span class="sxs-lookup"><span data-stu-id="0fe18-126">Do not use.</span></span> |
| <span data-ttu-id="0fe18-127">Łącznik aktualizacji</span><span class="sxs-lookup"><span data-stu-id="0fe18-127">Update Connector</span></span> |<span data-ttu-id="0fe18-128">Nie używaj.</span><span class="sxs-lookup"><span data-stu-id="0fe18-128">Do not use.</span></span> |
| <span data-ttu-id="0fe18-129">Odśwież schemat</span><span class="sxs-lookup"><span data-stu-id="0fe18-129">Refresh Schema</span></span> |<span data-ttu-id="0fe18-130">Odświeża pamięci podręcznej schematu.</span><span class="sxs-lookup"><span data-stu-id="0fe18-130">Refreshes the cached schema.</span></span> <span data-ttu-id="0fe18-131">Jest preferowany, aby zamiast tego należy użyć opcji w Kreatorze instalacji również od który aktualizacje synchronizacji reguły.</span><span class="sxs-lookup"><span data-stu-id="0fe18-131">It is preferred to use the option in the installation wizard instead, since that also updates sync rules.</span></span> |
| [<span data-ttu-id="0fe18-132">Obszar łączników wyszukiwania</span><span class="sxs-lookup"><span data-stu-id="0fe18-132">Search Connector Space</span></span>](#search-connector-space) |<span data-ttu-id="0fe18-133">Używana do znajdowania obiektów i [wykonaj obiekt i jego danych za pośrednictwem systemu](#follow-an-object-and-its-data-through-the-system).</span><span class="sxs-lookup"><span data-stu-id="0fe18-133">Used to find objects and to [Follow an object and its data through the system](#follow-an-object-and-its-data-through-the-system).</span></span> |

### <a name="delete"></a><span data-ttu-id="0fe18-134">Usuwanie</span><span class="sxs-lookup"><span data-stu-id="0fe18-134">Delete</span></span>
<span data-ttu-id="0fe18-135">Akcja usuwania, która jest używana do dwóch różnych rzeczy.</span><span class="sxs-lookup"><span data-stu-id="0fe18-135">The delete action is used for two different things.</span></span>  
![Menedżera usługi synchronizacji](./media/active-directory-aadconnectsync-service-manager-ui/connectordelete.png)

<span data-ttu-id="0fe18-137">Opcja **usunąć tylko przestrzeni łącznika** powoduje usunięcie wszystkich danych, ale zachować konfigurację.</span><span class="sxs-lookup"><span data-stu-id="0fe18-137">The option **Delete connector space only** removes all data, but keep the configuration.</span></span>

<span data-ttu-id="0fe18-138">Opcja **usunąć Connector i łącznika miejsca** powoduje usunięcie danych i konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="0fe18-138">The option **Delete Connector and connector space** removes the data and the configuration.</span></span> <span data-ttu-id="0fe18-139">Ta opcja jest używana, gdy użytkownik nie chce już połączenie z lasem.</span><span class="sxs-lookup"><span data-stu-id="0fe18-139">This option is used when you do not want to connect to a forest anymore.</span></span>

<span data-ttu-id="0fe18-140">Obie te opcje synchronizować wszystkie obiekty i zaktualizować obiektów metaverse.</span><span class="sxs-lookup"><span data-stu-id="0fe18-140">Both options sync all objects and update the metaverse objects.</span></span> <span data-ttu-id="0fe18-141">Ta akcja jest operacją wymagającą dużo czasu.</span><span class="sxs-lookup"><span data-stu-id="0fe18-141">This action is a long running operation.</span></span>

### <a name="configure-run-profiles"></a><span data-ttu-id="0fe18-142">Konfigurowanie profilów uruchamiania</span><span class="sxs-lookup"><span data-stu-id="0fe18-142">Configure Run Profiles</span></span>
<span data-ttu-id="0fe18-143">Ta opcja umożliwia Zobacz profile uruchamiania skonfigurowane dla łącznika.</span><span class="sxs-lookup"><span data-stu-id="0fe18-143">This option allows you to see the run profiles configured for a Connector.</span></span>

![Menedżera usługi synchronizacji](./media/active-directory-aadconnectsync-service-manager-ui/configurerunprofiles.png)

### <a name="search-connector-space"></a><span data-ttu-id="0fe18-145">Obszar łączników wyszukiwania</span><span class="sxs-lookup"><span data-stu-id="0fe18-145">Search Connector Space</span></span>
<span data-ttu-id="0fe18-146">Akcja wyszukiwania łącznika miejsca jest przydatne do znalezienia obiektów i rozwiązywania problemów danych.</span><span class="sxs-lookup"><span data-stu-id="0fe18-146">The search connector space action is useful to find objects and troubleshoot data issues.</span></span>

![Menedżera usługi synchronizacji](./media/active-directory-aadconnectsync-service-manager-ui/cssearch.png)

<span data-ttu-id="0fe18-148">Najpierw wybrać **zakres**.</span><span class="sxs-lookup"><span data-stu-id="0fe18-148">Start by selecting a **scope**.</span></span> <span data-ttu-id="0fe18-149">Można wyszukiwać na podstawie danych (RDN, nazwa Wyróżniająca, zakotwiczenia, poddrzewa), lub stanu obiektu (wszystkie inne opcje).</span><span class="sxs-lookup"><span data-stu-id="0fe18-149">You can search based on data (RDN, DN, Anchor, Sub-Tree), or state of the object (all other options).</span></span>  
<span data-ttu-id="0fe18-150">![Menedżera usługi synchronizacji](./media/active-directory-aadconnectsync-service-manager-ui/cssearchscope.png)</span><span class="sxs-lookup"><span data-stu-id="0fe18-150">![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/cssearchscope.png)</span></span>  
<span data-ttu-id="0fe18-151">Jeśli na przykład wykonać wyszukiwanie poddrzewa, możesz uzyskać wszystkie obiekty w jednej jednostce Organizacyjnej.</span><span class="sxs-lookup"><span data-stu-id="0fe18-151">If you for example do a Sub-Tree search, you get all objects in one OU.</span></span>  
<span data-ttu-id="0fe18-152">![Menedżera usługi synchronizacji](./media/active-directory-aadconnectsync-service-manager-ui/cssearchsubtree.png)</span><span class="sxs-lookup"><span data-stu-id="0fe18-152">![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/cssearchsubtree.png)</span></span>  
<span data-ttu-id="0fe18-153">W tym miejscu. Wybierz obiekt, wybierz **właściwości**, i [po nim](active-directory-aadconnectsync-troubleshoot-object-not-syncing.md) z obszaru łącznika źródło, za pomocą środowiska metaverse, a do docelowej przestrzeni łącznika.</span><span class="sxs-lookup"><span data-stu-id="0fe18-153">From this grid you can select an object, select **properties**, and [follow it](active-directory-aadconnectsync-troubleshoot-object-not-syncing.md) from the source connector space, through the metaverse, and to the target connector space.</span></span>

### <a name="changing-the-ad-ds-account-password"></a><span data-ttu-id="0fe18-154">Zmiana hasła do konta usług AD DS</span><span class="sxs-lookup"><span data-stu-id="0fe18-154">Changing the AD DS account password</span></span>
<span data-ttu-id="0fe18-155">Jeśli zmienisz hasło konta usługi synchronizacji nie będzie mógł importu/eksportu zmiany w lokalnej usługi AD.</span><span class="sxs-lookup"><span data-stu-id="0fe18-155">If you change the account password, the Synchronization Service will no longer be able to import/export changes to on-premises AD.</span></span>   <span data-ttu-id="0fe18-156">Użytkownik może wystąpić następujący błąd:</span><span class="sxs-lookup"><span data-stu-id="0fe18-156">You may see the following:</span></span>

- <span data-ttu-id="0fe18-157">Krok importu/eksportu dla łącznika usługi AD nie powiedzie się z powodu błędu "nie-start — poświadczenia".</span><span class="sxs-lookup"><span data-stu-id="0fe18-157">The import/export step for the AD connector fails with "no-start-credentials" error.</span></span>
- <span data-ttu-id="0fe18-158">W Podglądzie zdarzeń systemu Windows w dzienniku zdarzeń aplikacji zawiera błąd z 6000 identyfikator zdarzenia i komunikatem "agenta zarządzania"contoso.com"nie można uruchomić, ponieważ poświadczenia były nieprawidłowe."</span><span class="sxs-lookup"><span data-stu-id="0fe18-158">Under Windows Event Viewer, the application event log contains an error with Event ID 6000 and message “The management agent “contoso.com” failed to run because the credentials were invalid.”</span></span>

<span data-ttu-id="0fe18-159">Aby rozwiązać ten problem, zaktualizuj konto użytkownika usług AD DS za pomocą następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="0fe18-159">To resolve the issue, update the AD DS user account using the following:</span></span>


1. <span data-ttu-id="0fe18-160">Uruchom Menedżera usługi synchronizacji (usługa synchronizacji → START).</span><span class="sxs-lookup"><span data-stu-id="0fe18-160">Start the Synchronization Service Manager (START → Synchronization Service).</span></span>
</br><span data-ttu-id="0fe18-161">![Menedżera usługi synchronizacji](./media/active-directory-aadconnectsync-service-manager-ui/startmenu.png)</span><span class="sxs-lookup"><span data-stu-id="0fe18-161">![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/startmenu.png)</span></span>
2. <span data-ttu-id="0fe18-162">Przejdź do **łączniki** kartę.</span><span class="sxs-lookup"><span data-stu-id="0fe18-162">Go to the **Connectors** tab.</span></span>
3. <span data-ttu-id="0fe18-163">Wybierz łącznik AD, która jest skonfigurowana pod kątem używania konta usług AD DS.</span><span class="sxs-lookup"><span data-stu-id="0fe18-163">Select the AD Connector which is configured to use the AD DS account.</span></span>
4. <span data-ttu-id="0fe18-164">W obszarze akcje, wybierz **właściwości**.</span><span class="sxs-lookup"><span data-stu-id="0fe18-164">Under Actions, select **Properties**.</span></span>
5. <span data-ttu-id="0fe18-165">W oknie podręcznym wybierz opcję Połącz do lasu usługi Active Directory:</span><span class="sxs-lookup"><span data-stu-id="0fe18-165">In the pop-up dialog, select Connect to Active Directory Forest:</span></span>
6. <span data-ttu-id="0fe18-166">Nazwa lasu wskazuje odpowiedniej lokalnej usługi AD.</span><span class="sxs-lookup"><span data-stu-id="0fe18-166">The Forest name indicates the corresponding on-prem AD.</span></span>
7. <span data-ttu-id="0fe18-167">Nazwa użytkownika wskazuje, że konto usługi AD DS, używane do synchronizacji.</span><span class="sxs-lookup"><span data-stu-id="0fe18-167">The User name indicates the AD DS account used for synchronization.</span></span>
8. <span data-ttu-id="0fe18-168">Wprowadź nowe hasło do konta usług AD DS w pole tekstowe hasła ![Azure AD Connect synchronizacji szyfrowania klucz narzędzia](media/active-directory-aadconnectsync-encryption-key/key6.png)</span><span class="sxs-lookup"><span data-stu-id="0fe18-168">Enter the new password of the AD DS account in the Password textbox ![Azure AD Connect Sync Encryption Key Utility](media/active-directory-aadconnectsync-encryption-key/key6.png)</span></span>
9. <span data-ttu-id="0fe18-169">Kliknij przycisk OK, aby zapisać nowe hasło i uruchomić ponownie usługi synchronizacji, aby usunąć stare hasło z pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="0fe18-169">Click OK to save the new password and restart the Synchronization Service to remove the old password from memory cache.</span></span>



## <a name="next-steps"></a><span data-ttu-id="0fe18-170">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="0fe18-170">Next steps</span></span>
<span data-ttu-id="0fe18-171">Dowiedz się więcej o [synchronizacja programu Azure AD Connect](active-directory-aadconnectsync-whatis.md) konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="0fe18-171">Learn more about the [Azure AD Connect sync](active-directory-aadconnectsync-whatis.md) configuration.</span></span>

<span data-ttu-id="0fe18-172">Dowiedz się więcej na temat [integrowania tożsamości lokalnych z usługą Azure Active Directory](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="0fe18-172">Learn more about [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>
