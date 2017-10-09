---
title: "Synchronizacja programu Azure AD Connect: zmiany hasła konta DS hello AD | Dokumentacja firmy Microsoft"
description: "W tym dokumencie temacie opisano, jak Azure AD Connect po hello hasło do konta usług AD DS hello tooupdate zostanie zmieniona."
services: active-directory
keywords: "Usługi AD DS konta, konto usługi Active Directory, hasło"
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
ms.openlocfilehash: 2707c9246446612f8d083ecde876b3b4fb2435ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="changing-hello-ad-ds-account-password"></a><span data-ttu-id="96f37-104">Zmiana hasła konta hello AD DS</span><span class="sxs-lookup"><span data-stu-id="96f37-104">Changing hello AD DS account password</span></span>
<span data-ttu-id="96f37-105">Witaj AD DS konto odnosi się toohello konto użytkownika używane przez toocommunicate Azure AD Connect z lokalną usługą Active Directory.</span><span class="sxs-lookup"><span data-stu-id="96f37-105">hello AD DS account refers toohello user account used by Azure AD Connect toocommunicate with on-premises Active Directory.</span></span> <span data-ttu-id="96f37-106">Jeśli zmienisz hasło hello hello konta usług AD DS, należy zaktualizować Azure AD Connect usługi synchronizacji z hello nowe hasło.</span><span class="sxs-lookup"><span data-stu-id="96f37-106">If you change hello password of hello AD DS account, you must update Azure AD Connect Synchronization Service with hello new password.</span></span> <span data-ttu-id="96f37-107">W przeciwnym razie powitalne synchronizacji nie będzie można poprawnie synchronizowane z hello lokalnej usługi Active Directory i wystąpi hello następujące błędy:</span><span class="sxs-lookup"><span data-stu-id="96f37-107">Otherwise, hello Synchronization can no longer synchronize correctly with hello on-premises Active Directory and you will encounter hello following errors:</span></span>

* <span data-ttu-id="96f37-108">W hello Menedżera usługi synchronizacji, importu lub eksportu operację z lokalnymi AD kończy się niepowodzeniem z **logowanie bez poświadczeń na początku** błędu.</span><span class="sxs-lookup"><span data-stu-id="96f37-108">In hello Synchronization Service Manager, any import or export operation with on-premises AD fails with **no-start-credentials** error.</span></span>

* <span data-ttu-id="96f37-109">W Podglądzie zdarzeń systemu Windows, w dzienniku zdarzeń aplikacji hello zawiera błąd **6000 identyfikator zdarzenia** i komunikat **"hello zarządzania agenta"contoso.com"nie powiodło się toorun ponieważ hello poświadczenia były nieprawidłowe"** .</span><span class="sxs-lookup"><span data-stu-id="96f37-109">Under Windows Event Viewer, hello application event log contains an error with **Event ID 6000** and message **'hello management agent "contoso.com" failed toorun because hello credentials were invalid'**.</span></span>


## <a name="how-tooupdate-hello-synchronization-service-with-new-password-for-ad-ds-account"></a><span data-ttu-id="96f37-110">Jak tooupdate hello usługi synchronizacji z nowe hasło dla konta usług AD DS</span><span class="sxs-lookup"><span data-stu-id="96f37-110">How tooupdate hello Synchronization Service with new password for AD DS account</span></span>
<span data-ttu-id="96f37-111">Witaj tooupdate usługi synchronizacji z hello nowe hasło:</span><span class="sxs-lookup"><span data-stu-id="96f37-111">tooupdate hello Synchronization Service with hello new password:</span></span>

1. <span data-ttu-id="96f37-112">Uruchom hello Synchronization Service Manager (START → usługa synchronizacji).</span><span class="sxs-lookup"><span data-stu-id="96f37-112">Start hello Synchronization Service Manager (START → Synchronization Service).</span></span>
</br><span data-ttu-id="96f37-113">![Menedżera usługi synchronizacji](./media/active-directory-aadconnectsync-service-manager-ui/startmenu.png)</span><span class="sxs-lookup"><span data-stu-id="96f37-113">![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/startmenu.png)</span></span>  

2. <span data-ttu-id="96f37-114">Przejdź toohello **łączniki** kartę.</span><span class="sxs-lookup"><span data-stu-id="96f37-114">Go toohello **Connectors** tab.</span></span>

3. <span data-ttu-id="96f37-115">Wybierz hello **łącznika AD** , który odpowiada toohello AD DS konto, dla którego jego hasło zostało zmienione.</span><span class="sxs-lookup"><span data-stu-id="96f37-115">Select hello **AD Connector** that corresponds toohello AD DS account for which its password was changed.</span></span>

4. <span data-ttu-id="96f37-116">W obszarze **akcje**, wybierz pozycję **właściwości**.</span><span class="sxs-lookup"><span data-stu-id="96f37-116">Under **Actions**, select **Properties**.</span></span>

5. <span data-ttu-id="96f37-117">W wyskakującym oknie dialogowym hello, wybierz **Connect lesie katalogu tooActive**:</span><span class="sxs-lookup"><span data-stu-id="96f37-117">In hello pop-up dialog, select **Connect tooActive Directory Forest**:</span></span>

6. <span data-ttu-id="96f37-118">Wprowadź nowe hasło hello konta hello usług AD DS w hello **hasło** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="96f37-118">Enter hello new password of hello AD DS account in hello **Password** textbox.</span></span>

7. <span data-ttu-id="96f37-119">Kliknij przycisk **OK** toosave hello nowe hasło i zamknij hello podręczne okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="96f37-119">Click **OK** toosave hello new password and close hello pop-up dialog.</span></span>

8. <span data-ttu-id="96f37-120">Ponowne uruchomienie hello Azure AD Connect usługi synchronizacji w obszarze Menedżer sterowania usługami systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="96f37-120">Restart hello Azure AD Connect Synchronization Service under Windows Service Control Manager.</span></span> <span data-ttu-id="96f37-121">Jest to tooensure który wszelkie odwołania toohello stare hasło jest usuwany z hello pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="96f37-121">This is tooensure that any reference toohello old password is removed from hello memory cache.</span></span>

## <a name="next-steps"></a><span data-ttu-id="96f37-122">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="96f37-122">Next steps</span></span>
<span data-ttu-id="96f37-123">**Tematy poglądowe**</span><span class="sxs-lookup"><span data-stu-id="96f37-123">**Overview topics**</span></span>

* [<span data-ttu-id="96f37-124">Synchronizacja programu Azure AD Connect: zrozumienie i dostosowywanie synchronizacji</span><span class="sxs-lookup"><span data-stu-id="96f37-124">Azure AD Connect sync: Understand and customize synchronization</span></span>](active-directory-aadconnectsync-whatis.md)

* [<span data-ttu-id="96f37-125">Integrowanie tożsamości lokalnych z usługą Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="96f37-125">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
