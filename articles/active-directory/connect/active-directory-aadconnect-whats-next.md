---
title: "Azure AD Connect: Następne kroki i w jaki sposób toomanage Azure AD Connect | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooextend hello domyślnej konfiguracji i zadania operacyjne programu Azure AD Connect."
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
ms.openlocfilehash: 4404aaff24d54d76b83baca3b331a6a250ba4c03
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="next-steps-and-how-toomanage-azure-ad-connect"></a><span data-ttu-id="abb1a-103">Następne kroki i w jaki sposób toomanage Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="abb1a-103">Next steps and how toomanage Azure AD Connect</span></span>
<span data-ttu-id="abb1a-104">Użyj procedur operacyjnych hello w programie toomeet Połącz usługi Azure Active Directory (Azure AD) toocustomize tego artykułu, wymagań i potrzeb organizacji.</span><span class="sxs-lookup"><span data-stu-id="abb1a-104">Use hello operational procedures in this article toocustomize Azure Active Directory (Azure AD) Connect toomeet your organization's needs and requirements.</span></span>  

## <a name="add-additional-sync-admins"></a><span data-ttu-id="abb1a-105">Dodaj administratorów dodatkowe synchronizacji</span><span class="sxs-lookup"><span data-stu-id="abb1a-105">Add additional sync admins</span></span>
<span data-ttu-id="abb1a-106">Domyślnie tylko użytkownik hello, który hello instalacji i Administratorzy lokalni są aparatu synchronizacji hello zainstalowany toomanage stanie.</span><span class="sxs-lookup"><span data-stu-id="abb1a-106">By default, only hello user who did hello installation and local admins are able toomanage hello installed sync engine.</span></span> <span data-ttu-id="abb1a-107">Dla tooaccess stanie toobe dodatkowe osoby i zarządzać aparatem synchronizacji hello, Znajdź hello grupy o nazwie ADSyncAdmins na serwerze lokalnym hello je i Dodaj toothis grupy.</span><span class="sxs-lookup"><span data-stu-id="abb1a-107">For additional people toobe able tooaccess and manage hello sync engine, locate hello group named ADSyncAdmins on hello local server and add them toothis group.</span></span>

## <a name="assign-licenses-tooazure-ad-premium-and-enterprise-mobility-suite-users"></a><span data-ttu-id="abb1a-108">Przypisywanie licencji tooAzure użytkowników AD — wersja Premium i Enterprise Mobility Suite</span><span class="sxs-lookup"><span data-stu-id="abb1a-108">Assign licenses tooAzure AD Premium and Enterprise Mobility Suite users</span></span>
<span data-ttu-id="abb1a-109">Teraz, gdy użytkownicy zostały zsynchronizowane toohello chmury, należy tooassign je licencji, można rozpocząć korzystanie z aplikacji w chmurze takich jak Office 365.</span><span class="sxs-lookup"><span data-stu-id="abb1a-109">Now that your users have been synchronized toohello cloud, you need tooassign them a license so they can get going with cloud apps such as Office 365.</span></span>

### <a name="tooassign-an-azure-ad-premium-or-enterprise-mobility-suite-license"></a><span data-ttu-id="abb1a-110">tooassign Azure AD Premium lub Enterprise Mobility Suite licencji</span><span class="sxs-lookup"><span data-stu-id="abb1a-110">tooassign an Azure AD Premium or Enterprise Mobility Suite License</span></span>

1. <span data-ttu-id="abb1a-111">Zaloguj się toohello portalu Azure jako administrator.</span><span class="sxs-lookup"><span data-stu-id="abb1a-111">Sign in toohello Azure portal as an admin.</span></span>
2. <span data-ttu-id="abb1a-112">Po lewej stronie powitania, wybierz **usługi Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="abb1a-112">On hello left, select **Active Directory**.</span></span>
3. <span data-ttu-id="abb1a-113">Na powitania **usługi Active Directory** kliknij dwukrotnie hello katalogu, który ma hello użytkownicy mają tooset w górę.</span><span class="sxs-lookup"><span data-stu-id="abb1a-113">On hello **Active Directory** page, double-click hello directory that has hello users you want tooset up.</span></span>
4. <span data-ttu-id="abb1a-114">U góry strony katalogu hello hello, wybierz **licencji**.</span><span class="sxs-lookup"><span data-stu-id="abb1a-114">At hello top of hello directory page, select **Licenses**.</span></span>
5. <span data-ttu-id="abb1a-115">Na powitania **licencji** wybierz pozycję **Active Directory Premium** lub **Enterprise Mobility Suite**, a następnie kliknij przycisk **przypisać**.</span><span class="sxs-lookup"><span data-stu-id="abb1a-115">On hello **Licenses** page, select **Active Directory Premium** or **Enterprise Mobility Suite**, and then click **Assign**.</span></span>
6. <span data-ttu-id="abb1a-116">Okno dialogowe hello wybierz opcję użytkownicy hello mają tooassign licencji, a następnie kliknij hello znacznik wyboru Ikona toosave hello zmiany.</span><span class="sxs-lookup"><span data-stu-id="abb1a-116">In hello dialog box, select hello users you want tooassign licenses to, and then click hello check mark icon toosave hello changes.</span></span>

## <a name="verify-hello-scheduled-synchronization-task"></a><span data-ttu-id="abb1a-117">Sprawdź hello zaplanowanej synchronizacji zadań</span><span class="sxs-lookup"><span data-stu-id="abb1a-117">Verify hello scheduled synchronization task</span></span>
<span data-ttu-id="abb1a-118">Użyj hello Azure toocheck portalu hello stan synchronizacji.</span><span class="sxs-lookup"><span data-stu-id="abb1a-118">Use hello Azure portal toocheck hello status of a synchronization.</span></span>

### <a name="tooverify-hello-scheduled-synchronization-task"></a><span data-ttu-id="abb1a-119">tooverify hello zaplanowanej synchronizacji zadań</span><span class="sxs-lookup"><span data-stu-id="abb1a-119">tooverify hello scheduled synchronization task</span></span>
1. <span data-ttu-id="abb1a-120">Zaloguj się toohello portalu Azure jako administrator.</span><span class="sxs-lookup"><span data-stu-id="abb1a-120">Sign in toohello Azure portal as an admin.</span></span>
2. <span data-ttu-id="abb1a-121">Po lewej stronie powitania, wybierz **usługi Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="abb1a-121">On hello left, select **Active Directory**.</span></span>
3. <span data-ttu-id="abb1a-122">Na powitania **usługi Active Directory** kliknij dwukrotnie hello katalogu, który ma hello użytkownicy mają tooset w górę.</span><span class="sxs-lookup"><span data-stu-id="abb1a-122">On hello **Active Directory** page, double-click hello directory that has hello users you want tooset up.</span></span>
4. <span data-ttu-id="abb1a-123">U góry strony katalogu hello hello, wybierz **integracji katalogów**.</span><span class="sxs-lookup"><span data-stu-id="abb1a-123">At hello top of hello directory page, select **Directory Integration**.</span></span>
5. <span data-ttu-id="abb1a-124">W obszarze **Integracja z lokalną usługą active directory**, Uwaga hello czas ostatniej synchronizacji.</span><span class="sxs-lookup"><span data-stu-id="abb1a-124">Under **integration with local active directory**, note hello last sync time.</span></span>

<span data-ttu-id="abb1a-125"><center>![Czas synchronizacji katalogu](./media/active-directory-aadconnect-whats-next/verify.png)</center></span><span class="sxs-lookup"><span data-stu-id="abb1a-125"><center>![Directory sync time](./media/active-directory-aadconnect-whats-next/verify.png)</center></span></span>

## <a name="start-a-scheduled-synchronization-task"></a><span data-ttu-id="abb1a-126">Uruchom zadanie synchronizacji według harmonogramu</span><span class="sxs-lookup"><span data-stu-id="abb1a-126">Start a scheduled synchronization task</span></span>
<span data-ttu-id="abb1a-127">Jeśli potrzebujesz toorun zadania synchronizacji, można w tym, uruchamiając ponownie kreatora hello Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="abb1a-127">If you need toorun a synchronization task, you can do this by running through hello Azure AD Connect wizard again.</span></span>  <span data-ttu-id="abb1a-128">Należy tooprovide poświadczeń usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="abb1a-128">You need tooprovide your Azure AD credentials.</span></span>  <span data-ttu-id="abb1a-129">W Kreatorze hello wybierz hello **Dostosuj opcje synchronizacji** zadań, a następnie kliknij przycisk **dalej** toomove za pomocą Kreatora hello.</span><span class="sxs-lookup"><span data-stu-id="abb1a-129">In hello wizard, select hello **Customize synchronization options** task, and click **Next** toomove through hello wizard.</span></span> <span data-ttu-id="abb1a-130">Na koniec hello, upewnij się, że hello **Uruchom proces synchronizacji hello zaraz po zakończeniu początkowej konfiguracji hello** zaznaczone pole.</span><span class="sxs-lookup"><span data-stu-id="abb1a-130">At hello end, ensure that hello **Start hello synchronization process as soon as hello initial configuration completes** box is selected.</span></span>

<span data-ttu-id="abb1a-131"><center>![Uruchom synchronizację](./media/active-directory-aadconnect-whats-next/startsynch.png)</center></span><span class="sxs-lookup"><span data-stu-id="abb1a-131"><center>![Start synchronization](./media/active-directory-aadconnect-whats-next/startsynch.png)</center></span></span>

<span data-ttu-id="abb1a-132">Aby uzyskać więcej informacji na powitania usługi Azure AD Connect synchronizacji harmonogramu, zobacz [Azure AD Connect harmonogramu](active-directory-aadconnectsync-feature-scheduler.md).</span><span class="sxs-lookup"><span data-stu-id="abb1a-132">For more information on hello Azure AD Connect sync Scheduler, see [Azure AD Connect Scheduler](active-directory-aadconnectsync-feature-scheduler.md).</span></span>

## <a name="additional-tasks-available-in-azure-ad-connect"></a><span data-ttu-id="abb1a-133">Dodatkowe zadania dostępne w programie Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="abb1a-133">Additional tasks available in Azure AD Connect</span></span>
<span data-ttu-id="abb1a-134">Po początkowej instalacji programu Azure AD Connect można zawsze uruchomić Kreator hello ponownie z hello Azure AD Connect start strony lub pulpitu skrótów.</span><span class="sxs-lookup"><span data-stu-id="abb1a-134">After your initial installation of Azure AD Connect, you can always start hello wizard again from hello Azure AD Connect start page or desktop shortcut.</span></span>  <span data-ttu-id="abb1a-135">Można zauważyć, że ponownie przejść za pomocą Kreatora hello zawiera niektóre nowe opcje w formie hello dodatkowe zadania.</span><span class="sxs-lookup"><span data-stu-id="abb1a-135">You will notice that going through hello wizard again provides some new options in hello form of additional tasks.</span></span>  

<span data-ttu-id="abb1a-136">Witaj Poniższa tabela zawiera podsumowanie tych zadań i krótki opis każdego zadania.</span><span class="sxs-lookup"><span data-stu-id="abb1a-136">hello following table provides a summary of these tasks and a brief description of each task.</span></span>

![Lista dodatkowych zadań](./media/active-directory-aadconnect-whats-next/addtasks.png)

| <span data-ttu-id="abb1a-138">Dodatkowe zadania</span><span class="sxs-lookup"><span data-stu-id="abb1a-138">Additional task</span></span> | <span data-ttu-id="abb1a-139">Opis</span><span class="sxs-lookup"><span data-stu-id="abb1a-139">Description</span></span> |
| --- | --- |
| <span data-ttu-id="abb1a-140">**Wybrany scenariusz hello widoku**</span><span class="sxs-lookup"><span data-stu-id="abb1a-140">**View hello selected scenario**</span></span> |<span data-ttu-id="abb1a-141">Umożliwia wyświetlenie bieżącego rozwiązania Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="abb1a-141">View your current Azure AD Connect solution.</span></span>  <span data-ttu-id="abb1a-142">Obejmuje to ustawienia ogólne synchronizacji katalogów i ustawień synchronizacji.</span><span class="sxs-lookup"><span data-stu-id="abb1a-142">This includes general settings, synchronized directories, and sync settings.</span></span> |
| <span data-ttu-id="abb1a-143">**Dostosuj opcje synchronizacji**</span><span class="sxs-lookup"><span data-stu-id="abb1a-143">**Customize synchronization options**</span></span> |<span data-ttu-id="abb1a-144">Zmień hello bieżącej konfiguracji, takie jak dodanie dodatkowej konfiguracji toohello lasy usługi Active Directory lub włączanie opcji synchronizacji, takie jak użytkownika, grupy, urządzenia lub zapisywania zwrotnego haseł.</span><span class="sxs-lookup"><span data-stu-id="abb1a-144">Change hello current configuration like adding additional Active Directory forests toohello configuration, or enabling sync options such as user, group, device, or password write-back.</span></span> |
| <span data-ttu-id="abb1a-145">**Włącz tryb przejściowy**</span><span class="sxs-lookup"><span data-stu-id="abb1a-145">**Enable Staging Mode**</span></span> |<span data-ttu-id="abb1a-146">Etap informacje, które nie są natychmiast zsynchronizowane i nie jest eksportowane tooAzure AD lub lokalnej usługi Active Directory.</span><span class="sxs-lookup"><span data-stu-id="abb1a-146">Stage information that is not immediately synchronized and is not exported tooAzure AD or on-premises Active Directory.</span></span>  <span data-ttu-id="abb1a-147">Ta funkcja umożliwia podgląd synchronizacje hello przed ich wystąpieniem.</span><span class="sxs-lookup"><span data-stu-id="abb1a-147">With this feature, you can preview hello synchronizations before they occur.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="abb1a-148">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="abb1a-148">Next steps</span></span>
<span data-ttu-id="abb1a-149">Dowiedz się więcej o [integrowanie tożsamości lokalnych z usługą Azure Active Directory](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="abb1a-149">Learn more about [integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>
