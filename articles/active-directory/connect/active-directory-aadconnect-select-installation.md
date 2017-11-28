---
title: 'Azure AD Connect: Wybierz typ instalacji | Dokumentacja firmy Microsoft'
description: "W tym temacie przedstawiono sposób Wybieranie typu instalacji do użycia programu Azure AD Connect"
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
ms.openlocfilehash: a5697686bd1f41d581554b27ce78897963e38c74
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="select-which-installation-type-to-use-for-azure-ad-connect"></a><span data-ttu-id="c7aeb-103">Wybierz typ instalacji, które można użyć programu Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="c7aeb-103">Select which installation type to use for Azure AD Connect</span></span>
<span data-ttu-id="c7aeb-104">Azure AD Connect ma dwa typy instalacji nowej instalacji: Express i niestandardowych.</span><span class="sxs-lookup"><span data-stu-id="c7aeb-104">Azure AD Connect has two installation types for new installation: Express and customized.</span></span> <span data-ttu-id="c7aeb-105">Ten temat ułatwia podjęcie decyzji, którą opcję do użycia podczas instalacji.</span><span class="sxs-lookup"><span data-stu-id="c7aeb-105">This topic helps you to decide which option to use during installation.</span></span>

## <a name="express"></a><span data-ttu-id="c7aeb-106">Express</span><span class="sxs-lookup"><span data-stu-id="c7aeb-106">Express</span></span>
<span data-ttu-id="c7aeb-107">Express jest najbardziej typowych opcji i jest używany przez wszystkie nowe instalacje około 90%.</span><span class="sxs-lookup"><span data-stu-id="c7aeb-107">Express is the most common option and is used by about 90% of all new installations.</span></span> <span data-ttu-id="c7aeb-108">Została zaprojektowana w celu zapewnienia odpowiedniej konfiguracji najbardziej typowych scenariuszy.</span><span class="sxs-lookup"><span data-stu-id="c7aeb-108">It was designed to provide a configuration that works for the most common customer scenarios.</span></span>

<span data-ttu-id="c7aeb-109">Zakłada się:</span><span class="sxs-lookup"><span data-stu-id="c7aeb-109">It assumes:</span></span>

- <span data-ttu-id="c7aeb-110">Masz pojedynczego Active Directory lasu lokalnego.</span><span class="sxs-lookup"><span data-stu-id="c7aeb-110">You have a single Active Directory forest on-premises.</span></span>
- <span data-ttu-id="c7aeb-111">Masz konto administratora przedsiębiorstwa, używanej do instalacji.</span><span class="sxs-lookup"><span data-stu-id="c7aeb-111">You have an enterprise administrator account you can use for the installation.</span></span>
- <span data-ttu-id="c7aeb-112">Masz mniej niż 100 000 obiektów w usłudze Active Directory lokalnymi.</span><span class="sxs-lookup"><span data-stu-id="c7aeb-112">You have less than 100,000 objects in your on-premises Active Directory.</span></span>

<span data-ttu-id="c7aeb-113">Pobierz:</span><span class="sxs-lookup"><span data-stu-id="c7aeb-113">You get:</span></span>

- <span data-ttu-id="c7aeb-114">[Synchronizacja haseł](active-directory-aadconnectsync-implement-password-synchronization.md) z lokalnego do usługi Azure AD dla logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="c7aeb-114">[Password synchronization](active-directory-aadconnectsync-implement-password-synchronization.md) from on-premises to Azure AD for single sign-on.</span></span>
- <span data-ttu-id="c7aeb-115">Konfiguracja, która synchronizuje [użytkowników, grup, kontaktów i komputerach z systemem Windows 10](active-directory-aadconnectsync-understanding-default-configuration.md).</span><span class="sxs-lookup"><span data-stu-id="c7aeb-115">A configuration that synchronizes [users, groups, contacts, and Windows 10 computers](active-directory-aadconnectsync-understanding-default-configuration.md).</span></span>
- <span data-ttu-id="c7aeb-116">Synchronizacja wszystkich kwalifikujących się obiekty w wszystkie domeny i wszystkich jednostkach organizacyjnych.</span><span class="sxs-lookup"><span data-stu-id="c7aeb-116">Synchronization of all eligible objects in all domains and all OUs.</span></span>
- <span data-ttu-id="c7aeb-117">[Automatyczne uaktualnianie](active-directory-aadconnect-feature-automatic-upgrade.md) jest włączona, upewnij się, że należy zawsze używać najnowszej dostępnej wersji.</span><span class="sxs-lookup"><span data-stu-id="c7aeb-117">[Automatic upgrade](active-directory-aadconnect-feature-automatic-upgrade.md) is enabled to make sure you always use the latest available version.</span></span>

<span data-ttu-id="c7aeb-118">Opcje, których można nadal używać Express:</span><span class="sxs-lookup"><span data-stu-id="c7aeb-118">Options where you can still use Express:</span></span>

- <span data-ttu-id="c7aeb-119">Jeśli nie chcesz synchronizować wszystkich jednostkach organizacyjnych, można nadal używać Express i na ostatniej stronie, usuń zaznaczenie **Uruchom proces synchronizacji...** *.</span><span class="sxs-lookup"><span data-stu-id="c7aeb-119">If you do not want to synchronize all OUs, you can still use Express and on the last page, unselect **Start the synchronization process...***.</span></span> <span data-ttu-id="c7aeb-120">A następnie ponownie uruchom Kreatora instalacji i zmienić jednostki organizacyjne w [opcje konfiguracji](active-directory-aadconnectsync-installation-wizard.md#customize-synchronization-options) i Włącz synchronizację według harmonogramu.</span><span class="sxs-lookup"><span data-stu-id="c7aeb-120">Then run the installation wizard again and change the OUs in [configuration options](active-directory-aadconnectsync-installation-wizard.md#customize-synchronization-options) and enable scheduled sync.</span></span>
- <span data-ttu-id="c7aeb-121">Chcesz włączyć funkcji w usłudze Azure AD Premium, takie jak zapisywanie zwrotne haseł.</span><span class="sxs-lookup"><span data-stu-id="c7aeb-121">You want to enable one of the features in Azure AD Premium, such as Password writeback.</span></span> <span data-ttu-id="c7aeb-122">Najpierw należy przeprowadzić express można pobrać ukończeniem instalacji początkowej.</span><span class="sxs-lookup"><span data-stu-id="c7aeb-122">First go through express to get the initial installation completed.</span></span> <span data-ttu-id="c7aeb-123">A następnie ponownie uruchom Kreatora instalacji i zmienić [opcje konfiguracji](active-directory-aadconnectsync-installation-wizard.md#customize-synchronization-options).</span><span class="sxs-lookup"><span data-stu-id="c7aeb-123">Then run the installation wizard again and change the [configuration options](active-directory-aadconnectsync-installation-wizard.md#customize-synchronization-options).</span></span>

## <a name="custom"></a><span data-ttu-id="c7aeb-124">Niestandardowy</span><span class="sxs-lookup"><span data-stu-id="c7aeb-124">Custom</span></span>
<span data-ttu-id="c7aeb-125">Ścieżka dostosowane umożliwia wiele więcej opcji niż express.</span><span class="sxs-lookup"><span data-stu-id="c7aeb-125">The customized path allows many more options than express.</span></span> <span data-ttu-id="c7aeb-126">Stosuje we wszystkich przypadkach, gdy konfiguracji opisanych w poprzedniej sekcji Express nie jest reprezentatywna dla Twojej organizacji.</span><span class="sxs-lookup"><span data-stu-id="c7aeb-126">It should be used in all cases where the configuration described in previous section for express is not representative for your organization.</span></span>

<span data-ttu-id="c7aeb-127">Zastosowania:</span><span class="sxs-lookup"><span data-stu-id="c7aeb-127">Use when:</span></span>

- <span data-ttu-id="c7aeb-128">Nie masz dostępu do konta administratora przedsiębiorstwa w usłudze Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c7aeb-128">You do not have access to an enterprise admin account in Active Directory.</span></span>
- <span data-ttu-id="c7aeb-129">Masz więcej niż jednym lesie lub planowane jest synchronizowanie więcej niż jednym lesie w przyszłości.</span><span class="sxs-lookup"><span data-stu-id="c7aeb-129">You have more than one forest or you plan to synchronize more than one forest in the future.</span></span>
- <span data-ttu-id="c7aeb-130">Masz domen w lesie nie jest dostępny z serwera, Połącz.</span><span class="sxs-lookup"><span data-stu-id="c7aeb-130">You have domains in your forest not reachable from the Connect server.</span></span>
- <span data-ttu-id="c7aeb-131">Zamierzasz używać federacyjnego lub przekazywanego uwierzytelniania dla logowania użytkownika.</span><span class="sxs-lookup"><span data-stu-id="c7aeb-131">You plan to use federation or pass-through authentication for user sign-in.</span></span>
- <span data-ttu-id="c7aeb-132">Możesz mieć więcej niż 100 000 obiektów i muszą korzystać pełnego serwera SQL.</span><span class="sxs-lookup"><span data-stu-id="c7aeb-132">You have more than 100,000 objects and need to use a full SQL Server.</span></span>
- <span data-ttu-id="c7aeb-133">Zamierzasz używać filtrowanie na podstawie grupy, a nie tylko domeny lub filtrowanie na podstawie jednostki Organizacyjnej.</span><span class="sxs-lookup"><span data-stu-id="c7aeb-133">You plan to use group-based filtering and not only domain or OU-based filtering.</span></span>

## <a name="upgrade-from-dirsync"></a><span data-ttu-id="c7aeb-134">Uaktualnianie przy użyciu narzędzia DirSync</span><span class="sxs-lookup"><span data-stu-id="c7aeb-134">Upgrade from DirSync</span></span>
<span data-ttu-id="c7aeb-135">Jeśli obecnie używasz narzędzia DirSync, należy wykonać czynności opisane w [uaktualnienia narzędzia DirSync](active-directory-aadconnect-dirsync-upgrade-get-started.md) do uaktualnienia istniejącej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="c7aeb-135">If you are currently using DirSync, then follow the steps in [Upgrade from DirSync](active-directory-aadconnect-dirsync-upgrade-get-started.md) to upgrade your existing configuration.</span></span> <span data-ttu-id="c7aeb-136">Istnieją dwa różne opcje uaktualniania:</span><span class="sxs-lookup"><span data-stu-id="c7aeb-136">There are two different upgrade options:</span></span>

- <span data-ttu-id="c7aeb-137">Uaktualnienie w miejscu do zainstalowania na tym samym serwerze Connect.</span><span class="sxs-lookup"><span data-stu-id="c7aeb-137">In-place upgrade to install Connect on the same server.</span></span>
- <span data-ttu-id="c7aeb-138">Wdrożenie równoległe do instalacji Connect na nowym serwerze, gdy nadal działa istniejącego serwera narzędzia DirSync.</span><span class="sxs-lookup"><span data-stu-id="c7aeb-138">Parallel deployment to install Connect on a new server while the existing DirSync server is still operational.</span></span>

## <a name="upgrade-from-azure-ad-sync"></a><span data-ttu-id="c7aeb-139">Uaktualnianie programu Azure AD Sync</span><span class="sxs-lookup"><span data-stu-id="c7aeb-139">Upgrade from Azure AD Sync</span></span>
<span data-ttu-id="c7aeb-140">Jeśli aktualnie używasz usługi Azure AD Sync, a następnie można wykonać [te same czynności](active-directory-aadconnect-upgrade-previous-version.md) jako podczas uaktualniania z jednej wersji programu Connect do nowszej.</span><span class="sxs-lookup"><span data-stu-id="c7aeb-140">If you are currently using Azure AD Sync, then you can follow the [same steps](active-directory-aadconnect-upgrade-previous-version.md) as when you upgrade from one Connect version to a newer.</span></span> <span data-ttu-id="c7aeb-141">Istnieją dwa różne opcje uaktualniania:</span><span class="sxs-lookup"><span data-stu-id="c7aeb-141">There are two different upgrade options:</span></span>

- <span data-ttu-id="c7aeb-142">Uaktualnienie w miejscu do zainstalowania na tym samym serwerze Connect.</span><span class="sxs-lookup"><span data-stu-id="c7aeb-142">In-place upgrade to install Connect on the same server.</span></span>
- <span data-ttu-id="c7aeb-143">Zasięg migration, aby zainstalować Connect na nowym serwerze, gdy istniejący serwer synchronizacji usługi Azure AD jest nadal działa.</span><span class="sxs-lookup"><span data-stu-id="c7aeb-143">Swing-migration to install Connect on a new server while the existing Azure AD Sync server is still operational.</span></span>

## <a name="migrate-from-fim2010-or-mim2016"></a><span data-ttu-id="c7aeb-144">Migrowanie z usługi FIM2010 lub MIM2016</span><span class="sxs-lookup"><span data-stu-id="c7aeb-144">Migrate from FIM2010 or MIM2016</span></span>
<span data-ttu-id="c7aeb-145">Jeśli używasz obecnie programu Forefront Identity Manager 2010 lub Microsoft Identity Manager 2016 z łącznika usługi Azure AD, jedyną opcją jest migracji.</span><span class="sxs-lookup"><span data-stu-id="c7aeb-145">If you are currently using Forefront Identity Manager 2010 or Microsoft Identity Manager 2016 with the Azure AD Connector, then your only option is a migration.</span></span> <span data-ttu-id="c7aeb-146">Wykonaj kroki opisane w [migracji zasięg](active-directory-aadconnect-upgrade-previous-version.md#swing-migration).</span><span class="sxs-lookup"><span data-stu-id="c7aeb-146">Follow the steps described in [swing-migration](active-directory-aadconnect-upgrade-previous-version.md#swing-migration).</span></span> <span data-ttu-id="c7aeb-147">W krokach Zastąp FIM2010/MIM2016 wszelkie uwagi Azure AD Sync.</span><span class="sxs-lookup"><span data-stu-id="c7aeb-147">In the steps, replace any mention of Azure AD Sync with FIM2010/MIM2016.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c7aeb-148">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c7aeb-148">Next steps</span></span>
<span data-ttu-id="c7aeb-149">W zależności od opcji wybranych do użycia umożliwia odnalezienie artykułu z szczegółowy opis kroków spis treści z lewej strony.</span><span class="sxs-lookup"><span data-stu-id="c7aeb-149">Depending on the option you have selected to use, use the table of content to the left to find your article with the detailed steps.</span></span>
