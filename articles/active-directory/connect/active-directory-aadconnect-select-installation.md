---
title: 'Azure AD Connect: Wybierz typ instalacji | Dokumentacja firmy Microsoft'
description: "W tym temacie przedstawiono sposób instalacji hello tooselect wpisz toouse programu Azure AD Connect"
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: a700e59eb05947ee1dbd9993141200c9340b2f1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="select-which-installation-type-toouse-for-azure-ad-connect"></a><span data-ttu-id="532df-103">Wybierz które toouse typu instalacji programu Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="532df-103">Select which installation type toouse for Azure AD Connect</span></span>
<span data-ttu-id="532df-104">Azure AD Connect ma dwa typy instalacji nowej instalacji: Express i niestandardowych.</span><span class="sxs-lookup"><span data-stu-id="532df-104">Azure AD Connect has two installation types for new installation: Express and customized.</span></span> <span data-ttu-id="532df-105">Ten temat ułatwia toodecide, która opcja toouse podczas instalacji.</span><span class="sxs-lookup"><span data-stu-id="532df-105">This topic helps you toodecide which option toouse during installation.</span></span>

## <a name="express"></a><span data-ttu-id="532df-106">Express</span><span class="sxs-lookup"><span data-stu-id="532df-106">Express</span></span>
<span data-ttu-id="532df-107">Express jest najbardziej typowych opcji hello i jest używany przez wszystkie nowe instalacje około 90%.</span><span class="sxs-lookup"><span data-stu-id="532df-107">Express is hello most common option and is used by about 90% of all new installations.</span></span> <span data-ttu-id="532df-108">Został zaprojektowany tooprovide konfigurację, która działa w przypadku najbardziej typowych scenariuszy hello.</span><span class="sxs-lookup"><span data-stu-id="532df-108">It was designed tooprovide a configuration that works for hello most common customer scenarios.</span></span>

<span data-ttu-id="532df-109">Zakłada się:</span><span class="sxs-lookup"><span data-stu-id="532df-109">It assumes:</span></span>

- <span data-ttu-id="532df-110">Masz pojedynczego Active Directory lasu lokalnego.</span><span class="sxs-lookup"><span data-stu-id="532df-110">You have a single Active Directory forest on-premises.</span></span>
- <span data-ttu-id="532df-111">Masz konto administratora przedsiębiorstwa, używanej do instalacji hello.</span><span class="sxs-lookup"><span data-stu-id="532df-111">You have an enterprise administrator account you can use for hello installation.</span></span>
- <span data-ttu-id="532df-112">Masz mniej niż 100 000 obiektów w usłudze Active Directory lokalnymi.</span><span class="sxs-lookup"><span data-stu-id="532df-112">You have less than 100,000 objects in your on-premises Active Directory.</span></span>

<span data-ttu-id="532df-113">Pobierz:</span><span class="sxs-lookup"><span data-stu-id="532df-113">You get:</span></span>

- <span data-ttu-id="532df-114">[Synchronizacja haseł](active-directory-aadconnectsync-implement-password-synchronization.md) z lokalnymi tooAzure AD dla logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="532df-114">[Password synchronization](active-directory-aadconnectsync-implement-password-synchronization.md) from on-premises tooAzure AD for single sign-on.</span></span>
- <span data-ttu-id="532df-115">Konfiguracja, która synchronizuje [użytkowników, grup, kontaktów i komputerach z systemem Windows 10](active-directory-aadconnectsync-understanding-default-configuration.md).</span><span class="sxs-lookup"><span data-stu-id="532df-115">A configuration that synchronizes [users, groups, contacts, and Windows 10 computers](active-directory-aadconnectsync-understanding-default-configuration.md).</span></span>
- <span data-ttu-id="532df-116">Synchronizacja wszystkich kwalifikujących się obiekty w wszystkie domeny i wszystkich jednostkach organizacyjnych.</span><span class="sxs-lookup"><span data-stu-id="532df-116">Synchronization of all eligible objects in all domains and all OUs.</span></span>
- <span data-ttu-id="532df-117">[Automatyczne uaktualnianie](active-directory-aadconnect-feature-automatic-upgrade.md) jest włączone toomake się, że zawsze używaj hello najnowszej dostępnej wersji.</span><span class="sxs-lookup"><span data-stu-id="532df-117">[Automatic upgrade](active-directory-aadconnect-feature-automatic-upgrade.md) is enabled toomake sure you always use hello latest available version.</span></span>

<span data-ttu-id="532df-118">Opcje, których można nadal używać Express:</span><span class="sxs-lookup"><span data-stu-id="532df-118">Options where you can still use Express:</span></span>

- <span data-ttu-id="532df-119">Jeśli nie chcesz toosynchronize wszystkich jednostkach organizacyjnych, można nadal używać Express i na ostatniej stronie powitania, usuń zaznaczenie **Uruchom proces synchronizacji hello...** *.</span><span class="sxs-lookup"><span data-stu-id="532df-119">If you do not want toosynchronize all OUs, you can still use Express and on hello last page, unselect **Start hello synchronization process...***.</span></span> <span data-ttu-id="532df-120">A następnie ponownie uruchom Kreatora instalacji hello i zmienić jednostek organizacyjnych hello w [opcje konfiguracji](active-directory-aadconnectsync-installation-wizard.md#customize-synchronization-options) i Włącz synchronizację według harmonogramu.</span><span class="sxs-lookup"><span data-stu-id="532df-120">Then run hello installation wizard again and change hello OUs in [configuration options](active-directory-aadconnectsync-installation-wizard.md#customize-synchronization-options) and enable scheduled sync.</span></span>
- <span data-ttu-id="532df-121">Ma tooenable hello funkcji w usłudze Azure AD Premium, takie jak zapisywanie zwrotne haseł.</span><span class="sxs-lookup"><span data-stu-id="532df-121">You want tooenable one of hello features in Azure AD Premium, such as Password writeback.</span></span> <span data-ttu-id="532df-122">Najpierw należy przeprowadzić express tooget hello początkowej instalacja została zakończona.</span><span class="sxs-lookup"><span data-stu-id="532df-122">First go through express tooget hello initial installation completed.</span></span> <span data-ttu-id="532df-123">A następnie ponownie uruchom Kreatora instalacji hello i zmienić hello [opcje konfiguracji](active-directory-aadconnectsync-installation-wizard.md#customize-synchronization-options).</span><span class="sxs-lookup"><span data-stu-id="532df-123">Then run hello installation wizard again and change hello [configuration options](active-directory-aadconnectsync-installation-wizard.md#customize-synchronization-options).</span></span>

## <a name="custom"></a><span data-ttu-id="532df-124">Niestandardowy</span><span class="sxs-lookup"><span data-stu-id="532df-124">Custom</span></span>
<span data-ttu-id="532df-125">Ścieżka dostosowane Hello umożliwia wiele więcej opcji niż express.</span><span class="sxs-lookup"><span data-stu-id="532df-125">hello customized path allows many more options than express.</span></span> <span data-ttu-id="532df-126">Stosuje we wszystkich przypadkach, gdy hello konfiguracji opisanych w poprzedniej sekcji Express nie jest reprezentatywna dla Twojej organizacji.</span><span class="sxs-lookup"><span data-stu-id="532df-126">It should be used in all cases where hello configuration described in previous section for express is not representative for your organization.</span></span>

<span data-ttu-id="532df-127">Zastosowania:</span><span class="sxs-lookup"><span data-stu-id="532df-127">Use when:</span></span>

- <span data-ttu-id="532df-128">Nie masz konta administratora przedsiębiorstwa tooan dostępu w usłudze Active Directory.</span><span class="sxs-lookup"><span data-stu-id="532df-128">You do not have access tooan enterprise admin account in Active Directory.</span></span>
- <span data-ttu-id="532df-129">Masz więcej niż jednym lesie lub planujesz toosynchronize więcej niż jednym lesie w przyszłości hello.</span><span class="sxs-lookup"><span data-stu-id="532df-129">You have more than one forest or you plan toosynchronize more than one forest in hello future.</span></span>
- <span data-ttu-id="532df-130">Masz domen w lesie nieosiągalny z serwera Connect hello.</span><span class="sxs-lookup"><span data-stu-id="532df-130">You have domains in your forest not reachable from hello Connect server.</span></span>
- <span data-ttu-id="532df-131">Planujesz toouse Federacji lub przekazywanego uwierzytelniania dla logowania użytkownika.</span><span class="sxs-lookup"><span data-stu-id="532df-131">You plan toouse federation or pass-through authentication for user sign-in.</span></span>
- <span data-ttu-id="532df-132">Masz więcej niż 100 000 obiektów i muszą toouse pełnego serwera SQL.</span><span class="sxs-lookup"><span data-stu-id="532df-132">You have more than 100,000 objects and need toouse a full SQL Server.</span></span>
- <span data-ttu-id="532df-133">Planujesz filtrowanie na podstawie grupy toouse i nie tylko domeny lub filtrowanie na podstawie jednostki Organizacyjnej.</span><span class="sxs-lookup"><span data-stu-id="532df-133">You plan toouse group-based filtering and not only domain or OU-based filtering.</span></span>

## <a name="upgrade-from-dirsync"></a><span data-ttu-id="532df-134">Uaktualnianie przy użyciu narzędzia DirSync</span><span class="sxs-lookup"><span data-stu-id="532df-134">Upgrade from DirSync</span></span>
<span data-ttu-id="532df-135">Jeśli obecnie używasz narzędzia DirSync, a następnie wykonaj kroki hello [uaktualnienia narzędzia DirSync](active-directory-aadconnect-dirsync-upgrade-get-started.md) tooupgrade istniejącej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="532df-135">If you are currently using DirSync, then follow hello steps in [Upgrade from DirSync](active-directory-aadconnect-dirsync-upgrade-get-started.md) tooupgrade your existing configuration.</span></span> <span data-ttu-id="532df-136">Istnieją dwa różne opcje uaktualniania:</span><span class="sxs-lookup"><span data-stu-id="532df-136">There are two different upgrade options:</span></span>

- <span data-ttu-id="532df-137">Tooinstall uaktualnienia w miejscu na połączenie hello sam serwer.</span><span class="sxs-lookup"><span data-stu-id="532df-137">In-place upgrade tooinstall Connect on hello same server.</span></span>
- <span data-ttu-id="532df-138">Równoległe wdrożenia tooinstall Connect na nowym serwerze, gdy serwer DirSync hello jest nadal działa.</span><span class="sxs-lookup"><span data-stu-id="532df-138">Parallel deployment tooinstall Connect on a new server while hello existing DirSync server is still operational.</span></span>

## <a name="upgrade-from-azure-ad-sync"></a><span data-ttu-id="532df-139">Uaktualnianie programu Azure AD Sync</span><span class="sxs-lookup"><span data-stu-id="532df-139">Upgrade from Azure AD Sync</span></span>
<span data-ttu-id="532df-140">Jeśli aktualnie używasz usługi Azure AD Sync, a następnie wykonać hello [te same czynności](active-directory-aadconnect-upgrade-previous-version.md) jako po uaktualnieniu z jednego połączenia wersji tooa nowszej.</span><span class="sxs-lookup"><span data-stu-id="532df-140">If you are currently using Azure AD Sync, then you can follow hello [same steps](active-directory-aadconnect-upgrade-previous-version.md) as when you upgrade from one Connect version tooa newer.</span></span> <span data-ttu-id="532df-141">Istnieją dwa różne opcje uaktualniania:</span><span class="sxs-lookup"><span data-stu-id="532df-141">There are two different upgrade options:</span></span>

- <span data-ttu-id="532df-142">Tooinstall uaktualnienia w miejscu na połączenie hello sam serwer.</span><span class="sxs-lookup"><span data-stu-id="532df-142">In-place upgrade tooinstall Connect on hello same server.</span></span>
- <span data-ttu-id="532df-143">Zasięg migracji tooinstall Connect na nowym serwerze podczas istniejącego serwera Azure AD Sync hello jest nadal działa.</span><span class="sxs-lookup"><span data-stu-id="532df-143">Swing-migration tooinstall Connect on a new server while hello existing Azure AD Sync server is still operational.</span></span>

## <a name="migrate-from-fim2010-or-mim2016"></a><span data-ttu-id="532df-144">Migrowanie z usługi FIM2010 lub MIM2016</span><span class="sxs-lookup"><span data-stu-id="532df-144">Migrate from FIM2010 or MIM2016</span></span>
<span data-ttu-id="532df-145">Jeśli używasz obecnie programu Forefront Identity Manager 2010 lub Microsoft Identity Manager 2016 z hello łącznika usługi Azure AD, jedyną opcją jest migracji.</span><span class="sxs-lookup"><span data-stu-id="532df-145">If you are currently using Forefront Identity Manager 2010 or Microsoft Identity Manager 2016 with hello Azure AD Connector, then your only option is a migration.</span></span> <span data-ttu-id="532df-146">Wykonaj kroki hello opisanego w [migracji zasięg](active-directory-aadconnect-upgrade-previous-version.md#swing-migration).</span><span class="sxs-lookup"><span data-stu-id="532df-146">Follow hello steps described in [swing-migration](active-directory-aadconnect-upgrade-previous-version.md#swing-migration).</span></span> <span data-ttu-id="532df-147">W krokach hello Zastąp FIM2010/MIM2016 wszelkie uwagi Azure AD Sync.</span><span class="sxs-lookup"><span data-stu-id="532df-147">In hello steps, replace any mention of Azure AD Sync with FIM2010/MIM2016.</span></span>

## <a name="next-steps"></a><span data-ttu-id="532df-148">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="532df-148">Next steps</span></span>
<span data-ttu-id="532df-149">W zależności od opcji hello wybrano toouse, użyj hello tabelę z zawartości toohello toofind po lewej stronie artykułu z hello szczegółowe kroki.</span><span class="sxs-lookup"><span data-stu-id="532df-149">Depending on hello option you have selected toouse, use hello table of content toohello left toofind your article with hello detailed steps.</span></span>
