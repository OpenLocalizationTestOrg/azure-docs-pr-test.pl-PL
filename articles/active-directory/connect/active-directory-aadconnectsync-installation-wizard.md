---
title: "Ponowne uruchomienie Kreatora instalacji modułu hello Azure AD Connect | Dokumentacja firmy Microsoft"
description: "Wyjaśniono, jak Kreator instalacji hello działa powitania po raz drugi uruchomienia."
keywords: "Kreator instalacji Hello Azure AD Connect umożliwia skonfigurowanie hello ustawienia konserwacji po raz drugi uruchomienia"
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: d800214e-e591-4297-b9b5-d0b1581cc36a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 83cc74aca471ef9b4f65f7f3582e3e48d3d81cfe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-running-hello-installation-wizard-a-second-time"></a><span data-ttu-id="4237b-104">Synchronizacja programu Azure AD Connect: uruchamiania Kreatora instalacji powitania po raz drugi</span><span class="sxs-lookup"><span data-stu-id="4237b-104">Azure AD Connect sync: Running hello installation wizard a second time</span></span>
<span data-ttu-id="4237b-105">Witaj Uruchom Kreatora instalacji hello Azure AD Connect, po raz pierwszy przeprowadzi Cię on przez jak tooconfigure instalacji.</span><span class="sxs-lookup"><span data-stu-id="4237b-105">hello first time you run hello Azure AD Connect installation wizard, it walks you through how tooconfigure your installation.</span></span> <span data-ttu-id="4237b-106">Jeśli ponownie uruchom Kreatora instalacji hello oferuje opcje konserwacji.</span><span class="sxs-lookup"><span data-stu-id="4237b-106">If you run hello installation wizard again, it offers options for maintenance.</span></span>

<span data-ttu-id="4237b-107">Kreator instalacji hello znajduje się w menu start hello o nazwie **Azure AD Connect**.</span><span class="sxs-lookup"><span data-stu-id="4237b-107">You can find hello installation wizard in hello start menu named **Azure AD Connect**.</span></span>

![Start menu](./media/active-directory-aadconnectsync-installation-wizard/startmenu.png)

<span data-ttu-id="4237b-109">Po uruchomieniu Kreatora instalacji hello pojawić się Strona z następującymi opcjami:</span><span class="sxs-lookup"><span data-stu-id="4237b-109">When you start hello installation wizard, you see a page with these options:</span></span>

![Strona z listą dodatkowe zadania](./media/active-directory-aadconnectsync-installation-wizard/additionaltasks.png)

<span data-ttu-id="4237b-111">Po zainstalowaniu usług AD FS z programem Azure AD Connect, masz jeszcze więcej opcji.</span><span class="sxs-lookup"><span data-stu-id="4237b-111">If you have installed ADFS with Azure AD Connect, you have even more options.</span></span> <span data-ttu-id="4237b-112">Witaj dodatkowe opcje masz dla usług AD FS są udokumentowane w artykule [zarządzania usług AD FS](active-directory-aadconnect-federation-management.md#manage-ad-fs).</span><span class="sxs-lookup"><span data-stu-id="4237b-112">hello additional options you have for ADFS are documented in [ADFS management](active-directory-aadconnect-federation-management.md#manage-ad-fs).</span></span>

<span data-ttu-id="4237b-113">Wybierz jedno z zadań hello i kliknij przycisk **dalej** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="4237b-113">Select one of hello tasks and click **Next** toocontinue.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4237b-114">Chociaż hello Kreatora instalacji, Otwórz, wszystkie operacje w aparacie synchronizacji hello są wstrzymane.</span><span class="sxs-lookup"><span data-stu-id="4237b-114">While you have hello installation wizard open, all operations in hello sync engine are suspended.</span></span> <span data-ttu-id="4237b-115">Upewnij się, że zamknąć kreatora instalacji hello zaraz po zakończeniu zmiany w konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="4237b-115">Make sure you close hello installation wizard as soon as you have completed your configuration changes.</span></span>
>
>

## <a name="view-current-configuration"></a><span data-ttu-id="4237b-116">Wyświetl bieżącą konfigurację</span><span class="sxs-lookup"><span data-stu-id="4237b-116">View current configuration</span></span>
<span data-ttu-id="4237b-117">Ta opcja umożliwia szybki przegląd aktualnie skonfigurowanych opcji.</span><span class="sxs-lookup"><span data-stu-id="4237b-117">This option gives you a quick view of your currently configured options.</span></span>

![Strona z listą wszystkich opcji i ich stan](./media/active-directory-aadconnectsync-installation-wizard/viewconfig.png)

<span data-ttu-id="4237b-119">Kliknij przycisk **Wstecz** toogo Wstecz.</span><span class="sxs-lookup"><span data-stu-id="4237b-119">Click **Previous** toogo back.</span></span> <span data-ttu-id="4237b-120">W przypadku wybrania **zakończenia**, zamknąć kreatora instalacji hello.</span><span class="sxs-lookup"><span data-stu-id="4237b-120">If you select **Exit**, you close hello installation wizard.</span></span>

## <a name="customize-synchronization-options"></a><span data-ttu-id="4237b-121">Dostosuj opcje synchronizacji</span><span class="sxs-lookup"><span data-stu-id="4237b-121">Customize synchronization options</span></span>
<span data-ttu-id="4237b-122">Ta opcja jest używana toomake zmiany toohello synchronizacji konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="4237b-122">This option is used toomake changes toohello sync configuration.</span></span> <span data-ttu-id="4237b-123">Zostanie wyświetlony podzbiór opcje ze ścieżki instalacji niestandardowej konfiguracji hello.</span><span class="sxs-lookup"><span data-stu-id="4237b-123">You see a subset of options from hello custom configuration installation path.</span></span> <span data-ttu-id="4237b-124">Ta opcja jest widoczna, nawet jeśli początkowo użyć instalacji ekspresowej.</span><span class="sxs-lookup"><span data-stu-id="4237b-124">You see this option even if you used express installation initially.</span></span>

* <span data-ttu-id="4237b-125">[Dodaj więcej katalogów](active-directory-aadconnect-get-started-custom.md#connect-your-directories).</span><span class="sxs-lookup"><span data-stu-id="4237b-125">[Add more directories](active-directory-aadconnect-get-started-custom.md#connect-your-directories).</span></span> <span data-ttu-id="4237b-126">Aby usunięcie katalogu, zobacz [usunąć łącznik](active-directory-aadconnectsync-service-manager-ui-connectors.md#delete).</span><span class="sxs-lookup"><span data-stu-id="4237b-126">For removing a directory, see [Delete a Connector](active-directory-aadconnectsync-service-manager-ui-connectors.md#delete).</span></span>
* <span data-ttu-id="4237b-127">[Zmień domenę i jednostkę Organizacyjną filtrowania](active-directory-aadconnect-get-started-custom.md#domain-and-ou-filtering).</span><span class="sxs-lookup"><span data-stu-id="4237b-127">[Change Domain and OU filtering](active-directory-aadconnect-get-started-custom.md#domain-and-ou-filtering).</span></span>
* <span data-ttu-id="4237b-128">Usuń grupę filtrowania.</span><span class="sxs-lookup"><span data-stu-id="4237b-128">Remove Group filtering.</span></span>
* <span data-ttu-id="4237b-129">[Zmień funkcje opcjonalne](active-directory-aadconnect-get-started-custom.md#optional-features).</span><span class="sxs-lookup"><span data-stu-id="4237b-129">[Change optional features](active-directory-aadconnect-get-started-custom.md#optional-features).</span></span>

<span data-ttu-id="4237b-130">Witaj innych opcji hello początkowej instalacji nie można zmienić i nie są dostępne.</span><span class="sxs-lookup"><span data-stu-id="4237b-130">hello other options from hello initial installation cannot be changed and are not available.</span></span> <span data-ttu-id="4237b-131">Dostępne są następujące opcje:</span><span class="sxs-lookup"><span data-stu-id="4237b-131">These options are:</span></span>

* <span data-ttu-id="4237b-132">Zmień hello toouse atrybut userPrincipalName i sourceAnchor.</span><span class="sxs-lookup"><span data-stu-id="4237b-132">Change hello attribute toouse for userPrincipalName and sourceAnchor.</span></span>
* <span data-ttu-id="4237b-133">Zmień hello dołączenie metody dla obiektów z innego lasu.</span><span class="sxs-lookup"><span data-stu-id="4237b-133">Change hello joining method for objects from different forest.</span></span>
* <span data-ttu-id="4237b-134">Włącz filtrowanie na podstawie grupy.</span><span class="sxs-lookup"><span data-stu-id="4237b-134">Enable group-based filtering.</span></span>

## <a name="refresh-directory-schema"></a><span data-ttu-id="4237b-135">Odśwież schemat katalogu</span><span class="sxs-lookup"><span data-stu-id="4237b-135">Refresh directory schema</span></span>
<span data-ttu-id="4237b-136">Ta opcja jest używana, jeśli schemat hello zostały zmienione w jednym z lokalnymi lasami usługi AD DS.</span><span class="sxs-lookup"><span data-stu-id="4237b-136">This option is used if you have changed hello schema in one of your on-premises AD DS forests.</span></span> <span data-ttu-id="4237b-137">Na przykład może być zainstalowany program Exchange lub uaktualnić schematu tooa systemu Windows Server 2012 z obiektami urządzenia.</span><span class="sxs-lookup"><span data-stu-id="4237b-137">For example, you might have installed Exchange or upgraded tooa Windows Server 2012 schema with device objects.</span></span> <span data-ttu-id="4237b-138">W takim przypadku należy tooinstruct Azure AD Connect tooread hello schematu ponownie z usług AD DS i zaktualizować pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="4237b-138">In this case, you need tooinstruct Azure AD Connect tooread hello schema again from AD DS and update its cache.</span></span> <span data-ttu-id="4237b-139">Ta akcja generuje również hello reguły synchronizacji.</span><span class="sxs-lookup"><span data-stu-id="4237b-139">This action also regenerates hello Sync Rules.</span></span> <span data-ttu-id="4237b-140">Jeśli dodasz hello schematu programu Exchange, na przykład hello reguły synchronizacji programu Exchange są dodawane toohello konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="4237b-140">If you add hello Exchange schema, as an example, hello Sync Rules for Exchange are added toohello configuration.</span></span>

<span data-ttu-id="4237b-141">Po wybraniu tej opcji są wyświetlane wszystkie katalogi hello w konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="4237b-141">When you select this option, all hello directories in your configuration are listed.</span></span> <span data-ttu-id="4237b-142">Możesz zachować hello domyślne ustawienie i Odśwież wszystkich lasach lub usuń zaznaczenie niektórych z nich.</span><span class="sxs-lookup"><span data-stu-id="4237b-142">You can keep hello default setting and refresh all forests or unselect some of them.</span></span>

![Strona z listą wszystkich katalogów w środowisku hello](./media/active-directory-aadconnectsync-installation-wizard/refreshschema.png)

## <a name="configure-staging-mode"></a><span data-ttu-id="4237b-144">Konfigurowanie trybu przejściowego</span><span class="sxs-lookup"><span data-stu-id="4237b-144">Configure staging mode</span></span>
<span data-ttu-id="4237b-145">Ta opcja pozwala tooenable i Wyłącz tryb przejściowy na powitania serwera.</span><span class="sxs-lookup"><span data-stu-id="4237b-145">This option allows you tooenable and disable staging mode on hello server.</span></span> <span data-ttu-id="4237b-146">Więcej informacji o tymczasowych trybu i sposobie ich użycia można znaleźć w [operacji](active-directory-aadconnectsync-operations.md#staging-mode).</span><span class="sxs-lookup"><span data-stu-id="4237b-146">More information about staging mode and how it is used can be found in [Operations](active-directory-aadconnectsync-operations.md#staging-mode).</span></span>

<span data-ttu-id="4237b-147">Opcja Hello pokazuje, czy przemieszczania jest obecnie włączona lub wyłączona:</span><span class="sxs-lookup"><span data-stu-id="4237b-147">hello option shows if staging is currently enabled or disabled:</span></span>  
![Opcja, która również jest wyświetlany bieżący stan trybu przejściowego hello](./media/active-directory-aadconnectsync-installation-wizard/stagingmodecurrentstate.png)

<span data-ttu-id="4237b-149">toochange hello stanu, wybranie tej opcji i hello zaznacz lub usuń zaznaczenie pola wyboru.</span><span class="sxs-lookup"><span data-stu-id="4237b-149">toochange hello state, select this option and select or unselect hello checkbox.</span></span>  
![Opcja, która również jest wyświetlany bieżący stan trybu przejściowego hello](./media/active-directory-aadconnectsync-installation-wizard/stagingmodeenable.png)

## <a name="change-user-sign-in"></a><span data-ttu-id="4237b-151">Zmień logowanie użytkowników</span><span class="sxs-lookup"><span data-stu-id="4237b-151">Change user sign-in</span></span>
<span data-ttu-id="4237b-152">Ta opcja umożliwia toochange toofederation synchronizacji haseł lub hello odwrotnie.</span><span class="sxs-lookup"><span data-stu-id="4237b-152">This option allows you toochange from password sync toofederation or hello other way around.</span></span> <span data-ttu-id="4237b-153">Nie można zmienić za**nieskonfigurowane**.</span><span class="sxs-lookup"><span data-stu-id="4237b-153">You cannot change too**do not configure**.</span></span>

<span data-ttu-id="4237b-154">Aby uzyskać więcej informacji na temat tej opcji, zobacz [logowania użytkownika](active-directory-aadconnect-user-signin.md#changing-the-user-sign-in-method).</span><span class="sxs-lookup"><span data-stu-id="4237b-154">For more information on this option, see [user sign-in](active-directory-aadconnect-user-signin.md#changing-the-user-sign-in-method).</span></span>

## <a name="next-steps"></a><span data-ttu-id="4237b-155">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="4237b-155">Next steps</span></span>
* <span data-ttu-id="4237b-156">Dowiedz się więcej o hello model konfiguracji używane przez synchronizacja programu Azure AD Connect w [Aprowizacją deklaratywną opis](active-directory-aadconnectsync-understanding-declarative-provisioning.md).</span><span class="sxs-lookup"><span data-stu-id="4237b-156">Learn more about hello configuration model used by Azure AD Connect sync in [Understanding Declarative Provisioning](active-directory-aadconnectsync-understanding-declarative-provisioning.md).</span></span>

<span data-ttu-id="4237b-157">**Tematy poglądowe**</span><span class="sxs-lookup"><span data-stu-id="4237b-157">**Overview topics**</span></span>

* [<span data-ttu-id="4237b-158">Synchronizacja programu Azure AD Connect: zrozumienie i dostosowywanie synchronizacji</span><span class="sxs-lookup"><span data-stu-id="4237b-158">Azure AD Connect sync: Understand and customize synchronization</span></span>](active-directory-aadconnectsync-whatis.md)
* [<span data-ttu-id="4237b-159">Integrowanie tożsamości lokalnych z usługą Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4237b-159">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
