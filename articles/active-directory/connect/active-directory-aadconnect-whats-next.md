---
title: "Azure AD Connect: Kolejne kroki i sposobu zarządzania Azure AD Connect | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak rozszerzyć domyślnej konfiguracji i zadania operacyjne programu Azure AD Connect."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: curtand
ms.assetid: c18bee36-aebf-4281-b8fc-3fe14116f1a5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: beace24fa00c85a5038a3c39ae8f76af5fd12111
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="next-steps-and-how-to-manage-azure-ad-connect"></a><span data-ttu-id="57538-103">Kolejne kroki i sposobu zarządzania Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="57538-103">Next steps and how to manage Azure AD Connect</span></span>
<span data-ttu-id="57538-104">Należy użyć procedury działania w tym artykule, aby dostosować Połącz usługi Azure Active Directory (Azure AD) do zaspokojenia potrzeb i wymagań Twojej organizacji.</span><span class="sxs-lookup"><span data-stu-id="57538-104">Use the operational procedures in this article to customize Azure Active Directory (Azure AD) Connect to meet your organization's needs and requirements.</span></span>  

## <a name="add-additional-sync-admins"></a><span data-ttu-id="57538-105">Dodaj administratorów dodatkowe synchronizacji</span><span class="sxs-lookup"><span data-stu-id="57538-105">Add additional sync admins</span></span>
<span data-ttu-id="57538-106">Domyślnie tylko użytkownik, który został instalacji i Administratorzy lokalni mogą zarządzać aparatem synchronizacji zainstalowane.</span><span class="sxs-lookup"><span data-stu-id="57538-106">By default, only the user who did the installation and local admins are able to manage the installed sync engine.</span></span> <span data-ttu-id="57538-107">Dodatkowe użytkownicy powinni mieć możliwość dostępu i zarządzanie aparatu synchronizacji zlokalizuj grupę o nazwie ADSyncAdmins na serwerze lokalnym i dodaj je do tej grupy.</span><span class="sxs-lookup"><span data-stu-id="57538-107">For additional people to be able to access and manage the sync engine, locate the group named ADSyncAdmins on the local server and add them to this group.</span></span>

## <a name="assign-licenses-to-azure-ad-premium-and-enterprise-mobility-suite-users"></a><span data-ttu-id="57538-108">Przypisywanie licencji do użytkowników usługi Azure AD Premium i Enterprise Mobility Suite</span><span class="sxs-lookup"><span data-stu-id="57538-108">Assign licenses to Azure AD Premium and Enterprise Mobility Suite users</span></span>
<span data-ttu-id="57538-109">Teraz, gdy użytkownicy zostały zsynchronizowane w chmurze, należy przypisać im licencję, można rozpocząć korzystanie z aplikacji w chmurze takich jak Office 365.</span><span class="sxs-lookup"><span data-stu-id="57538-109">Now that your users have been synchronized to the cloud, you need to assign them a license so they can get going with cloud apps such as Office 365.</span></span>

### <a name="to-assign-an-azure-ad-premium-or-enterprise-mobility-suite-license"></a><span data-ttu-id="57538-110">Aby przypisać Azure AD Premium lub Enterprise Mobility Suite licencji</span><span class="sxs-lookup"><span data-stu-id="57538-110">To assign an Azure AD Premium or Enterprise Mobility Suite License</span></span>

1. <span data-ttu-id="57538-111">Zaloguj się do portalu Azure jako administrator.</span><span class="sxs-lookup"><span data-stu-id="57538-111">Sign in to the Azure portal as an admin.</span></span>
2. <span data-ttu-id="57538-112">W obszarze po lewej stronie wybierz pozycję **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="57538-112">On the left, select **Active Directory**.</span></span>
3. <span data-ttu-id="57538-113">Na **usługi Active Directory** kliknij dwukrotnie katalog, który ma użytkowników chcesz skonfigurować.</span><span class="sxs-lookup"><span data-stu-id="57538-113">On the **Active Directory** page, double-click the directory that has the users you want to set up.</span></span>
4. <span data-ttu-id="57538-114">W górnej części strony katalogu wybierz pozycję **Licencje**.</span><span class="sxs-lookup"><span data-stu-id="57538-114">At the top of the directory page, select **Licenses**.</span></span>
5. <span data-ttu-id="57538-115">Na **licencji** wybierz pozycję **Active Directory Premium** lub **Enterprise Mobility Suite**, a następnie kliknij przycisk **przypisać**.</span><span class="sxs-lookup"><span data-stu-id="57538-115">On the **Licenses** page, select **Active Directory Premium** or **Enterprise Mobility Suite**, and then click **Assign**.</span></span>
6. <span data-ttu-id="57538-116">W oknie dialogowym wybierz użytkowników, do których chcesz przypisać licencje, a następnie kliknij ikonę znacznika wyboru, aby zapisać zmiany.</span><span class="sxs-lookup"><span data-stu-id="57538-116">In the dialog box, select the users you want to assign licenses to, and then click the check mark icon to save the changes.</span></span>

## <a name="verify-the-scheduled-synchronization-task"></a><span data-ttu-id="57538-117">Sprawdź zadanie zaplanowanej synchronizacji</span><span class="sxs-lookup"><span data-stu-id="57538-117">Verify the scheduled synchronization task</span></span>
<span data-ttu-id="57538-118">Aby sprawdzić stan synchronizacji, użyj portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="57538-118">Use the Azure portal to check the status of a synchronization.</span></span>

### <a name="to-verify-the-scheduled-synchronization-task"></a><span data-ttu-id="57538-119">Można zweryfikować zadania zaplanowanej synchronizacji</span><span class="sxs-lookup"><span data-stu-id="57538-119">To verify the scheduled synchronization task</span></span>
1. <span data-ttu-id="57538-120">Zaloguj się do portalu Azure jako administrator.</span><span class="sxs-lookup"><span data-stu-id="57538-120">Sign in to the Azure portal as an admin.</span></span>
2. <span data-ttu-id="57538-121">W obszarze po lewej stronie wybierz pozycję **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="57538-121">On the left, select **Active Directory**.</span></span>
3. <span data-ttu-id="57538-122">Na **usługi Active Directory** kliknij dwukrotnie katalog, który ma użytkowników chcesz skonfigurować.</span><span class="sxs-lookup"><span data-stu-id="57538-122">On the **Active Directory** page, double-click the directory that has the users you want to set up.</span></span>
4. <span data-ttu-id="57538-123">W górnej części strony katalogu, wybierz **integracji katalogów**.</span><span class="sxs-lookup"><span data-stu-id="57538-123">At the top of the directory page, select **Directory Integration**.</span></span>
5. <span data-ttu-id="57538-124">W obszarze **Integracja z lokalną usługą active directory**, należy pamiętać, czas ostatniej synchronizacji.</span><span class="sxs-lookup"><span data-stu-id="57538-124">Under **integration with local active directory**, note the last sync time.</span></span>

<span data-ttu-id="57538-125"><center>![Czas synchronizacji katalogu](./media/active-directory-aadconnect-whats-next/verify.png)</center></span><span class="sxs-lookup"><span data-stu-id="57538-125"><center>![Directory sync time](./media/active-directory-aadconnect-whats-next/verify.png)</center></span></span>

## <a name="start-a-scheduled-synchronization-task"></a><span data-ttu-id="57538-126">Uruchom zadanie synchronizacji według harmonogramu</span><span class="sxs-lookup"><span data-stu-id="57538-126">Start a scheduled synchronization task</span></span>
<span data-ttu-id="57538-127">Jeśli chcesz uruchomić zadanie synchronizacji, można to zrobić, uruchamiając ponownie za pomocą Kreatora programu Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="57538-127">If you need to run a synchronization task, you can do this by running through the Azure AD Connect wizard again.</span></span>  <span data-ttu-id="57538-128">Musisz podać swoje poświadczenia usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="57538-128">You need to provide your Azure AD credentials.</span></span>  <span data-ttu-id="57538-129">W kreatorze Wybierz **Dostosuj opcje synchronizacji** zadań, a następnie kliknij przycisk **dalej** można przenieść za pomocą kreatora.</span><span class="sxs-lookup"><span data-stu-id="57538-129">In the wizard, select the **Customize synchronization options** task, and click **Next** to move through the wizard.</span></span> <span data-ttu-id="57538-130">Na koniec, upewnij się, że **Uruchom proces synchronizacji, gdy tylko Konfiguracja początkowa zostanie ukończona** zaznaczone pole.</span><span class="sxs-lookup"><span data-stu-id="57538-130">At the end, ensure that the **Start the synchronization process as soon as the initial configuration completes** box is selected.</span></span>

<span data-ttu-id="57538-131"><center>![Uruchom synchronizację](./media/active-directory-aadconnect-whats-next/startsynch.png)</center></span><span class="sxs-lookup"><span data-stu-id="57538-131"><center>![Start synchronization](./media/active-directory-aadconnect-whats-next/startsynch.png)</center></span></span>

<span data-ttu-id="57538-132">Aby uzyskać więcej informacji o synchronizacji Azure AD Connect harmonogramu, zobacz [Azure AD Connect harmonogramu](active-directory-aadconnectsync-feature-scheduler.md).</span><span class="sxs-lookup"><span data-stu-id="57538-132">For more information on the Azure AD Connect sync Scheduler, see [Azure AD Connect Scheduler](active-directory-aadconnectsync-feature-scheduler.md).</span></span>

## <a name="additional-tasks-available-in-azure-ad-connect"></a><span data-ttu-id="57538-133">Dodatkowe zadania dostępne w programie Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="57538-133">Additional tasks available in Azure AD Connect</span></span>
<span data-ttu-id="57538-134">Po początkowej instalacji programu Azure AD Connect można zawsze uruchomić Kreator ponownie z start Azure AD Connect skrótów strony lub pulpitu.</span><span class="sxs-lookup"><span data-stu-id="57538-134">After your initial installation of Azure AD Connect, you can always start the wizard again from the Azure AD Connect start page or desktop shortcut.</span></span>  <span data-ttu-id="57538-135">Można zauważyć, że ponownie przejść przez kreatora zawiera niektóre nowe opcje w formie dodatkowe zadania.</span><span class="sxs-lookup"><span data-stu-id="57538-135">You will notice that going through the wizard again provides some new options in the form of additional tasks.</span></span>  

<span data-ttu-id="57538-136">Poniższa tabela zawiera podsumowanie tych zadań i krótki opis każdego zadania.</span><span class="sxs-lookup"><span data-stu-id="57538-136">The following table provides a summary of these tasks and a brief description of each task.</span></span>

![Lista dodatkowych zadań](./media/active-directory-aadconnect-whats-next/addtasks.png)

| <span data-ttu-id="57538-138">Dodatkowe zadania</span><span class="sxs-lookup"><span data-stu-id="57538-138">Additional task</span></span> | <span data-ttu-id="57538-139">Opis</span><span class="sxs-lookup"><span data-stu-id="57538-139">Description</span></span> |
| --- | --- |
| <span data-ttu-id="57538-140">**Wyświetl wybrany scenariusz**</span><span class="sxs-lookup"><span data-stu-id="57538-140">**View the selected scenario**</span></span> |<span data-ttu-id="57538-141">Umożliwia wyświetlenie bieżącego rozwiązania Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="57538-141">View your current Azure AD Connect solution.</span></span>  <span data-ttu-id="57538-142">Obejmuje to ustawienia ogólne synchronizacji katalogów i ustawień synchronizacji.</span><span class="sxs-lookup"><span data-stu-id="57538-142">This includes general settings, synchronized directories, and sync settings.</span></span> |
| <span data-ttu-id="57538-143">**Dostosuj opcje synchronizacji**</span><span class="sxs-lookup"><span data-stu-id="57538-143">**Customize synchronization options**</span></span> |<span data-ttu-id="57538-144">Zmiany bieżącej konfiguracji, takie jak dodanie dodatkowych lasów usługi Active Directory do konfiguracji lub włączenie opcji synchronizacji, takich jak użytkownika, grupy, urządzenia lub zapisywania zwrotnego haseł.</span><span class="sxs-lookup"><span data-stu-id="57538-144">Change the current configuration like adding additional Active Directory forests to the configuration, or enabling sync options such as user, group, device, or password write-back.</span></span> |
| <span data-ttu-id="57538-145">**Włącz tryb przejściowy**</span><span class="sxs-lookup"><span data-stu-id="57538-145">**Enable Staging Mode**</span></span> |<span data-ttu-id="57538-146">Etap informacje, które nie są natychmiast zsynchronizowane i nie są eksportowane do usługi Azure AD lub lokalnej usługi Active Directory.</span><span class="sxs-lookup"><span data-stu-id="57538-146">Stage information that is not immediately synchronized and is not exported to Azure AD or on-premises Active Directory.</span></span>  <span data-ttu-id="57538-147">Ta funkcja umożliwia podgląd synchronizacje przed ich wystąpieniem.</span><span class="sxs-lookup"><span data-stu-id="57538-147">With this feature, you can preview the synchronizations before they occur.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="57538-148">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="57538-148">Next steps</span></span>
<span data-ttu-id="57538-149">Dowiedz się więcej o [integrowanie tożsamości lokalnych z usługą Azure Active Directory](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="57538-149">Learn more about [integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>
