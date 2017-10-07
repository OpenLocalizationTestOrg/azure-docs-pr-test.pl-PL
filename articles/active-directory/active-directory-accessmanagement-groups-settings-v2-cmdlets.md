---
title: "Przykłady aaaPowerShell Zarządzanie grupami w usłudze Azure Active Directory | Dokumentacja firmy Microsoft"
description: "Ta strona zawiera toohelp przykłady PowerShell Zarządzanie grupami w usłudze Azure Active Directory"
keywords: "Azure AD, Azure Active Directory, programu PowerShell, grup, grupy zarządzania"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 7a5023dc-2727-4c25-8254-b531fc3244ac
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: curtand
ms.reviewer: rodejo
ms.openlocfilehash: ba049babc436e99a290f20899b3a87bcfa811d9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-version-2-cmdlets-for-group-management"></a><span data-ttu-id="bc8bc-104">Usługi Active Directory w wersji 2 poleceń cmdlet systemu Azure dla grupy zarządzania</span><span class="sxs-lookup"><span data-stu-id="bc8bc-104">Azure Active Directory version 2 cmdlets for group management</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="bc8bc-105">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="bc8bc-105">Azure portal</span></span>](active-directory-groups-create-azure-portal.md)
> * [<span data-ttu-id="bc8bc-106">Klasyczna witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="bc8bc-106">Azure classic portal</span></span>](active-directory-accessmanagement-manage-groups.md)
> * [<span data-ttu-id="bc8bc-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="bc8bc-107">PowerShell</span></span>](active-directory-accessmanagement-groups-settings-v2-cmdlets.md)
>
>

<span data-ttu-id="bc8bc-108">Ten artykuł zawiera przykłady toouse PowerShell toomanage grup w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="bc8bc-108">This article contains examples of how toouse PowerShell toomanage your groups in Azure Active Directory (Azure AD).</span></span>  <span data-ttu-id="bc8bc-109">On również informuje tooget konfiguracji z hello modułu Azure AD PowerShell.</span><span class="sxs-lookup"><span data-stu-id="bc8bc-109">It also tells you how tooget set up with hello Azure AD PowerShell module.</span></span> <span data-ttu-id="bc8bc-110">Najpierw należy [Pobierz modułu Azure AD PowerShell hello](https://www.powershellgallery.com/packages/AzureAD/).</span><span class="sxs-lookup"><span data-stu-id="bc8bc-110">First, you must [download hello Azure AD PowerShell module](https://www.powershellgallery.com/packages/AzureAD/).</span></span>

## <a name="installing-hello-azure-ad-powershell-module"></a><span data-ttu-id="bc8bc-111">Instalowanie modułu programu PowerShell usługi Azure AD hello</span><span class="sxs-lookup"><span data-stu-id="bc8bc-111">Installing hello Azure AD PowerShell module</span></span>
<span data-ttu-id="bc8bc-112">Moduł Azure AD PowerShell hello tooinstall, hello Użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="bc8bc-112">tooinstall hello Azure AD PowerShell module, use hello following commands:</span></span>

    PS C:\Windows\system32> install-module azuread

<span data-ttu-id="bc8bc-113">tooverify, który hello moduł został zainstalowany, użyj następującego polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="bc8bc-113">tooverify that hello module was installed, use hello following command:</span></span>

    PS C:\Windows\system32> get-module azuread

    ModuleType Version      Name                                ExportedCommands
    ---------- ---------    ----                                ----------------
    Binary     2.0.0.115    azuread                      {Add-AzureADAdministrati...}

<span data-ttu-id="bc8bc-114">Teraz możesz rozpocząć używać hello poleceń cmdlet w hello module.</span><span class="sxs-lookup"><span data-stu-id="bc8bc-114">Now you can start using hello cmdlets in hello module.</span></span> <span data-ttu-id="bc8bc-115">Pełny opis poleceń cmdlet hello w module hello Azure AD, można znaleźć w dokumentacji online odwołanie toohello [Azure Active Directory programu PowerShell w wersji 2](/powershell/azure/install-adv2?view=azureadps-2.0).</span><span class="sxs-lookup"><span data-stu-id="bc8bc-115">For a full description of hello cmdlets in hello Azure AD module, please refer toohello online reference documentation for [Azure Active Directory PowerShell Version 2](/powershell/azure/install-adv2?view=azureadps-2.0).</span></span>

## <a name="connecting-toohello-directory"></a><span data-ttu-id="bc8bc-116">Łączenie toohello katalogu</span><span class="sxs-lookup"><span data-stu-id="bc8bc-116">Connecting toohello directory</span></span>
<span data-ttu-id="bc8bc-117">Aby umożliwić zarządzanie grupami za pomocą poleceń cmdlet programu PowerShell usługi Azure AD, należy połączyć ma toomanage katalogu toohello sesji programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="bc8bc-117">Before you can start managing groups using Azure AD PowerShell cmdlets, you must connect your PowerShell session toohello directory you want toomanage.</span></span> <span data-ttu-id="bc8bc-118">Witaj Użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="bc8bc-118">Use hello following command:</span></span>

    PS C:\Windows\system32> Connect-AzureAD

<span data-ttu-id="bc8bc-119">Witaj polecenie cmdlet wyświetli monit dla hello poświadczeń można mają toouse tooaccess katalogu.</span><span class="sxs-lookup"><span data-stu-id="bc8bc-119">hello cmdlet prompts you for hello credentials you want toouse tooaccess your directory.</span></span> <span data-ttu-id="bc8bc-120">W tym przykładzie używamy karen@drumkit.onmicrosoft.com tooaccess hello pokaz katalogu.</span><span class="sxs-lookup"><span data-stu-id="bc8bc-120">In this example, we are using karen@drumkit.onmicrosoft.com tooaccess hello demonstration directory.</span></span> <span data-ttu-id="bc8bc-121">Witaj polecenie cmdlet zwraca sesji hello tooshow potwierdzenie został pomyślnie połączony tooyour katalogu:</span><span class="sxs-lookup"><span data-stu-id="bc8bc-121">hello cmdlet returns a confirmation tooshow hello session was connected successfully tooyour directory:</span></span>

    Account                       Environment Tenant
    -------                       ----------- ------
    Karen@drumkit.onmicrosoft.com AzureCloud  85b5ff1e-0402-400c-9e3c-0f…

<span data-ttu-id="bc8bc-122">Teraz możesz rozpocząć używać hello AzureAD poleceń cmdlet toomanage grupy w katalogu.</span><span class="sxs-lookup"><span data-stu-id="bc8bc-122">Now you can start using hello AzureAD cmdlets toomanage groups in your directory.</span></span>

## <a name="retrieving-groups"></a><span data-ttu-id="bc8bc-123">Pobieranie grupy</span><span class="sxs-lookup"><span data-stu-id="bc8bc-123">Retrieving groups</span></span>
<span data-ttu-id="bc8bc-124">tooretrieve istniejących grup z katalogu, których można używać hello polecenia cmdlet Get-AzureADGroups.</span><span class="sxs-lookup"><span data-stu-id="bc8bc-124">tooretrieve existing groups from your directory you can use hello Get-AzureADGroups cmdlet.</span></span> <span data-ttu-id="bc8bc-125">tooretrieve wszystkich grup w katalogu hello, użyj hello cmdlet bez parametrów:</span><span class="sxs-lookup"><span data-stu-id="bc8bc-125">tooretrieve all groups in hello directory, use hello cmdlet without parameters:</span></span>

    PS C:\Windows\system32> get-azureadgroup

<span data-ttu-id="bc8bc-126">polecenia cmdlet Hello zwraca wszystkie grupy hello połączonego katalogu.</span><span class="sxs-lookup"><span data-stu-id="bc8bc-126">hello cmdlet returns all groups in hello connected directory.</span></span>

<span data-ttu-id="bc8bc-127">Można użyć tooretrieve parametru - objectID hello określonej grupy, dla którego należy określić objectID hello grupy:</span><span class="sxs-lookup"><span data-stu-id="bc8bc-127">You can use hello -objectID parameter tooretrieve a specific group for which you specify hello group’s objectID:</span></span>

    PS C:\Windows\system32> get-azureadgroup -ObjectId e29bae11-4ac0-450c-bc37-6dae8f3da61b

<span data-ttu-id="bc8bc-128">polecenie cmdlet Hello zwraca teraz hello grupy, których objectID zgodna z wartością hello parametru hello, wprowadzony:</span><span class="sxs-lookup"><span data-stu-id="bc8bc-128">hello cmdlet now returns hello group whose objectID matches hello value of hello parameter you entered:</span></span>

    DeletionTimeStamp            :
    ObjectId                     : e29bae11-4ac0-450c-bc37-6dae8f3da61b
    ObjectType                   : Group
    Description                  :
    DirSyncEnabled               :
    DisplayName                  : Pacific NW Support
    LastDirSyncTime              :
    Mail                         :
    MailEnabled                  : False
    MailNickName                 : 9bb4139b-60a1-434a-8c0d-7c1f8eee2df9
    OnPremisesSecurityIdentifier :
    ProvisioningErrors           : {}
    ProxyAddresses               : {}
    SecurityEnabled              : True

<span data-ttu-id="bc8bc-129">Można wyszukiwać określone grupy przy użyciu hello — parametr filtru.</span><span class="sxs-lookup"><span data-stu-id="bc8bc-129">You can search for a specific group using hello -filter parameter.</span></span> <span data-ttu-id="bc8bc-130">Ten parametr przyjmuje klauzuli filtru ODATA i zwraca wszystkie grupy, które odpowiada hello filtru, tak jak hello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="bc8bc-130">This parameter takes an ODATA filter clause and returns all groups that match hello filter, as in hello following example:</span></span>

    PS C:\Windows\system32> Get-AzureADGroup -Filter "DisplayName eq 'Intune Administrators'"


    DeletionTimeStamp            :
    ObjectId                     : 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df
    ObjectType                   : Group
    Description                  : Intune Administrators
    DirSyncEnabled               :
    DisplayName                  : Intune Administrators
    LastDirSyncTime              :
    Mail                         :
    MailEnabled                  : False
    MailNickName                 : 4dd067a0-6515-4f23-968a-cc2ffc2eff5c
    OnPremisesSecurityIdentifier :
    ProvisioningErrors           : {}
    ProxyAddresses               : {}
    SecurityEnabled              : True

> [!NOTE] 
> <span data-ttu-id="bc8bc-131">Hello poleceń cmdlet programu AzureAD PowerShell implementuje hello standardowego zapytania OData.</span><span class="sxs-lookup"><span data-stu-id="bc8bc-131">hello AzureAD PowerShell cmdlets implement hello OData query standard.</span></span> <span data-ttu-id="bc8bc-132">Aby uzyskać więcej informacji, zobacz **$filter** w [opcje zapytania systemu OData przy użyciu punktu końcowego OData hello](https://msdn.microsoft.com/library/gg309461.aspx#BKMK_filter).</span><span class="sxs-lookup"><span data-stu-id="bc8bc-132">For more information, see **$filter** in [OData system query options using hello OData endpoint](https://msdn.microsoft.com/library/gg309461.aspx#BKMK_filter).</span></span>

## <a name="creating-groups"></a><span data-ttu-id="bc8bc-133">Tworzenie grup</span><span class="sxs-lookup"><span data-stu-id="bc8bc-133">Creating groups</span></span>
<span data-ttu-id="bc8bc-134">toocreate nową grupę w katalogu, polecenia cmdlet służącego do hello AzureADGroup nowy.</span><span class="sxs-lookup"><span data-stu-id="bc8bc-134">toocreate a new group in your directory, use hello New-AzureADGroup cmdlet.</span></span> <span data-ttu-id="bc8bc-135">To polecenie cmdlet tworzy nową grupę zabezpieczeń o nazwie "Marketing":</span><span class="sxs-lookup"><span data-stu-id="bc8bc-135">This cmdlet creates a new security group called “Marketing":</span></span>

    PS C:\Windows\system32> New-AzureADGroup -Description "Marketing" -DisplayName "Marketing" -MailEnabled $false -SecurityEnabled $true -MailNickName "Marketing"

## <a name="updating-groups"></a><span data-ttu-id="bc8bc-136">Aktualizowanie grupy</span><span class="sxs-lookup"><span data-stu-id="bc8bc-136">Updating groups</span></span>
<span data-ttu-id="bc8bc-137">tooupdate istniejącej grupy, użyj polecenia cmdlet hello AzureADGroup zestawu.</span><span class="sxs-lookup"><span data-stu-id="bc8bc-137">tooupdate an existing group, use hello Set-AzureADGroup cmdlet.</span></span> <span data-ttu-id="bc8bc-138">W tym przykładzie Zmieniamy hello Właściwość DisplayName hello grupy "Administratorzy usługi Intune".</span><span class="sxs-lookup"><span data-stu-id="bc8bc-138">In this example, we’re changing hello DisplayName property of hello group “Intune Administrators.”</span></span> <span data-ttu-id="bc8bc-139">Po pierwsze firma Microsoft jest znajdowanie grupy hello przy użyciu polecenia cmdlet Get-AzureADGroup hello i Filtruj, używając atrybutu DisplayName hello:</span><span class="sxs-lookup"><span data-stu-id="bc8bc-139">First, we’re finding hello group using hello Get-AzureADGroup cmdlet and filter using hello DisplayName attribute:</span></span>

    PS C:\Windows\system32> Get-AzureADGroup -Filter "DisplayName eq 'Intune Administrators'"


    DeletionTimeStamp            :
    ObjectId                     : 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df
    ObjectType                   : Group
    Description                  : Intune Administrators
    DirSyncEnabled               :
    DisplayName                  : Intune Administrators
    LastDirSyncTime              :
    Mail                         :
    MailEnabled                  : False
    MailNickName                 : 4dd067a0-6515-4f23-968a-cc2ffc2eff5c
    OnPremisesSecurityIdentifier :
    ProvisioningErrors           : {}
    ProxyAddresses               : {}
    SecurityEnabled              : True

<span data-ttu-id="bc8bc-140">Następnie Zmieniamy hello opis toohello nowej wartości właściwości "Administratorzy usługi Intune urządzenie":</span><span class="sxs-lookup"><span data-stu-id="bc8bc-140">Next, we’re changing hello Description property toohello new value “Intune Device Administrators”:</span></span>

    PS C:\Windows\system32> Set-AzureADGroup -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df -Description "Intune Device Administrators"

<span data-ttu-id="bc8bc-141">Teraz ponownie znalezienie hello grupy, widzimy właściwości Description hello jest zaktualizowane tooreflect hello nowej wartości:</span><span class="sxs-lookup"><span data-stu-id="bc8bc-141">Now if we find hello group again, we see hello Description property is updated tooreflect hello new value:</span></span>

    PS C:\Windows\system32> Get-AzureADGroup -Filter "DisplayName eq 'Intune Administrators'"


    DeletionTimeStamp            :
    ObjectId                     : 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df
    ObjectType                   : Group
    Description                  : Intune Device Administrators
    DirSyncEnabled               :
    DisplayName                  : Intune Administrators
    LastDirSyncTime              :
    Mail                         :
    MailEnabled                  : False
    MailNickName                 : 4dd067a0-6515-4f23-968a-cc2ffc2eff5c
    OnPremisesSecurityIdentifier :
    ProvisioningErrors           : {}
    ProxyAddresses               : {}
    SecurityEnabled              : True

## <a name="deleting-groups"></a><span data-ttu-id="bc8bc-142">Usuwanie grup</span><span class="sxs-lookup"><span data-stu-id="bc8bc-142">Deleting groups</span></span>
<span data-ttu-id="bc8bc-143">grupy toodelete z katalogu, użyj polecenia cmdlet Remove-AzureADGroup hello w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="bc8bc-143">toodelete groups from your directory, use hello Remove-AzureADGroup cmdlet as follows:</span></span>

    PS C:\Windows\system32> Remove-AzureADGroup -ObjectId b11ca53e-07cc-455d-9a89-1fe3ab24566b

## <a name="managing-members-of-groups"></a><span data-ttu-id="bc8bc-144">Zarządzanie członkami grup</span><span class="sxs-lookup"><span data-stu-id="bc8bc-144">Managing members of groups</span></span>
<span data-ttu-id="bc8bc-145">Tooadd nowe elementy członkowskie tooa grupy, należy użyć polecenia cmdlet hello AzureADGroupMember Dodaj.</span><span class="sxs-lookup"><span data-stu-id="bc8bc-145">If you need tooadd new members tooa group, use hello Add-AzureADGroupMember cmdlet.</span></span> <span data-ttu-id="bc8bc-146">To polecenie dodaje członek grupy Administratorzy usługi Intune toohello wykorzystane przez nas w poprzednim przykładzie hello:</span><span class="sxs-lookup"><span data-stu-id="bc8bc-146">This command adds a member toohello Intune Administrators group we used in hello previous example:</span></span>

    PS C:\Windows\system32> Add-AzureADGroupMember -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df -RefObjectId 72cd4bbd-2594-40a2-935c-016f3cfeeeea

<span data-ttu-id="bc8bc-147">Witaj - ObjectId parametr jest hello ObjectID z toowhich grupy hello chcemy tooadd członka, a hello - RefObjectId jest hello ObjectID użytkownika hello chcemy tooadd jako członek grupy toohello.</span><span class="sxs-lookup"><span data-stu-id="bc8bc-147">hello -ObjectId parameter is hello ObjectID of hello group toowhich we want tooadd a member, and hello -RefObjectId is hello ObjectID of hello user we want tooadd as a member toohello group.</span></span>

<span data-ttu-id="bc8bc-148">tooget hello istniejących członków grupy, użyj polecenia cmdlet Get-AzureADGroupMember hello, jak w poniższym przykładzie:</span><span class="sxs-lookup"><span data-stu-id="bc8bc-148">tooget hello existing members of a group, use hello Get-AzureADGroupMember cmdlet, as in this example:</span></span>

    PS C:\Windows\system32> Get-AzureADGroupMember -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df

    DeletionTimeStamp ObjectId                             ObjectType
    ----------------- --------                             ----------
                          72cd4bbd-2594-40a2-935c-016f3cfeeeea User
                          8120cc36-64b4-4080-a9e8-23aa98e8b34f User

<span data-ttu-id="bc8bc-149">element członkowski hello tooremove dodaliśmy wcześniej toohello grupy, użyj hello AzureADGroupMember Usuń polecenia cmdlet, jak to pokazano poniżej:</span><span class="sxs-lookup"><span data-stu-id="bc8bc-149">tooremove hello member we previously added toohello group, use hello Remove-AzureADGroupMember cmdlet, as is shown here:</span></span>

    PS C:\Windows\system32> Remove-AzureADGroupMember -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df -MemberId 72cd4bbd-2594-40a2-935c-016f3cfeeeea

<span data-ttu-id="bc8bc-150">tooverify hello grupy uległ użytkownika, użyj polecenia cmdlet Select AzureADGroupIdsUserIsMemberOf hello.</span><span class="sxs-lookup"><span data-stu-id="bc8bc-150">tooverify hello group membership(s) of a user, use hello Select-AzureADGroupIdsUserIsMemberOf cmdlet.</span></span> <span data-ttu-id="bc8bc-151">To polecenie cmdlet przyjmuje jako parametry hello ObjectId hello użytkownika, dla których toocheck hello członkostwa w grupach oraz listę grup, dla których toocheck hello członkostwa.</span><span class="sxs-lookup"><span data-stu-id="bc8bc-151">This cmdlet takes as its parameters hello ObjectId of hello user for which toocheck hello group memberships, and a list of groups for which toocheck hello memberships.</span></span> <span data-ttu-id="bc8bc-152">Witaj listę grup muszą być w formie hello złożone zmiennej typu "Microsoft.Open.AzureAD.Model.GroupIdsForMembershipCheck", dlatego firma Microsoft najpierw utworzyć zmienną z danym typem:</span><span class="sxs-lookup"><span data-stu-id="bc8bc-152">hello list of groups must be provided in hello form of a complex variable of type “Microsoft.Open.AzureAD.Model.GroupIdsForMembershipCheck”, so we first must create a variable with that type:</span></span>

    PS C:\Windows\system32> $g = new-object Microsoft.Open.AzureAD.Model.GroupIdsForMembershipCheck

<span data-ttu-id="bc8bc-153">Następnie możemy podać wartości toocheck identyfikatory GroupID hello w atrybucie hello identyfikatory "GroupID" tej zmiennej złożone:</span><span class="sxs-lookup"><span data-stu-id="bc8bc-153">Next, we provide values for hello groupIds toocheck in hello attribute “GroupIds” of this complex variable:</span></span>

    PS C:\Windows\system32> $g.GroupIds = "b11ca53e-07cc-455d-9a89-1fe3ab24566b", "31f1ff6c-d48c-4f8a-b2e1-abca7fd399df"

<span data-ttu-id="bc8bc-154">Teraz Jeśli chcemy toocheck hello członkostwa w grupach użytkownika z 72cd4bbd-2594-40a2-935c-016f3cfeeeea ObjectID względem grupy hello w $g powinniśmy skorzystać:</span><span class="sxs-lookup"><span data-stu-id="bc8bc-154">Now, if we want toocheck hello group memberships of a user with ObjectID 72cd4bbd-2594-40a2-935c-016f3cfeeeea against hello groups in $g, we should use:</span></span>

    PS C:\Windows\system32> Select-AzureADGroupIdsUserIsMemberOf -ObjectId 72cd4bbd-2594-40a2-935c-016f3cfeeeea -GroupIdsForMembershipCheck $g

    OdataMetadata                                                                                                 Value
    -------------                                                                                                  -----
    https://graph.windows.net/85b5ff1e-0402-400c-9e3c-0f9e965325d1/$metadata#Collection(Edm.String)             {31f1ff6c-d48c-4f8a-b2e1-abca7fd399df}


<span data-ttu-id="bc8bc-155">wartość Hello, zwracana jest lista grup, których członkiem jest ten użytkownik.</span><span class="sxs-lookup"><span data-stu-id="bc8bc-155">hello value returned is a list of groups of which this user is a member.</span></span> <span data-ttu-id="bc8bc-156">Można także zastosować dla tej metody toocheck kontakty, grupy lub podmiotów zabezpieczeń usługi członkostwa dla danej listy grup, za pomocą AzureADGroupIdsContactIsMemberOf Select, wybierz AzureADGroupIdsGroupIsMemberOf lub Wybierz AzureADGroupIdsServicePrincipalIsMemberOf</span><span class="sxs-lookup"><span data-stu-id="bc8bc-156">You can also apply this method toocheck Contacts, Groups or Service Principals membership for a given list of groups, using Select-AzureADGroupIdsContactIsMemberOf, Select-AzureADGroupIdsGroupIsMemberOf or Select-AzureADGroupIdsServicePrincipalIsMemberOf</span></span>

## <a name="managing-owners-of-groups"></a><span data-ttu-id="bc8bc-157">Zarządzanie właścicielami grupy</span><span class="sxs-lookup"><span data-stu-id="bc8bc-157">Managing owners of groups</span></span>
<span data-ttu-id="bc8bc-158">Grupa tooadd właścicieli tooa, polecenia cmdlet służącego do hello AzureADGroupOwner Dodaj:</span><span class="sxs-lookup"><span data-stu-id="bc8bc-158">tooadd owners tooa group, use hello Add-AzureADGroupOwner cmdlet:</span></span>

    PS C:\Windows\system32> Add-AzureADGroupOwner -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df -RefObjectId 72cd4bbd-2594-40a2-935c-016f3cfeeeea

<span data-ttu-id="bc8bc-159">Witaj - ObjectId parametr jest hello ObjectID z toowhich grupy hello chcemy tooadd właściciela i hello - RefObjectId jest hello ObjectID użytkownika hello chcemy tooadd jako właściciel grupy hello.</span><span class="sxs-lookup"><span data-stu-id="bc8bc-159">hello -ObjectId parameter is hello ObjectID of hello group toowhich we want tooadd an owner, and hello -RefObjectId is hello ObjectID of hello user we want tooadd as an owner of hello group.</span></span>

<span data-ttu-id="bc8bc-160">tooretrieve hello właścicieli grupy, użyj polecenia cmdlet Get-AzureADGroupOwner hello:</span><span class="sxs-lookup"><span data-stu-id="bc8bc-160">tooretrieve hello owners of a group, use hello Get-AzureADGroupOwner cmdlet:</span></span>

    PS C:\Windows\system32> Get-AzureADGroupOwner -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df

<span data-ttu-id="bc8bc-161">polecenia cmdlet Hello zwraca listę hello właścicieli dla określonej grupy hello:</span><span class="sxs-lookup"><span data-stu-id="bc8bc-161">hello cmdlet returns hello list of owners for hello specified group:</span></span>

    DeletionTimeStamp ObjectId                             ObjectType
    ----------------- --------                             ----------
                          e831b3fd-77c9-49c7-9fca-de43e109ef67 User

<span data-ttu-id="bc8bc-162">Jeśli chcesz tooremove właściciela z grupy, użyj polecenia cmdlet Remove-AzureADGroupOwner hello:</span><span class="sxs-lookup"><span data-stu-id="bc8bc-162">If you want tooremove an owner from a group, use hello Remove-AzureADGroupOwner cmdlet:</span></span>

    PS C:\Windows\system32> remove-AzureADGroupOwner -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df -OwnerId e831b3fd-77c9-49c7-9fca-de43e109ef67

## <a name="reserved-aliases"></a><span data-ttu-id="bc8bc-163">Aliasy zastrzeżone</span><span class="sxs-lookup"><span data-stu-id="bc8bc-163">Reserved aliases</span></span> 
<span data-ttu-id="bc8bc-164">Po utworzeniu grupy niektóre punkty końcowe umożliwiają hello użytkownika końcowego toospecify toobe mailNickname lub alias, używana jako część adresu e-mail hello hello grupy.</span><span class="sxs-lookup"><span data-stu-id="bc8bc-164">When a group is created, certain endpoints allow hello end user toospecify a mailNickname or alias toobe used as part of hello email address of hello group.</span></span> <span data-ttu-id="bc8bc-165">Grupy z powitania po aliasów e-mail wysoko uprzywilejowane można tworzyć tylko przez administratora globalnego usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bc8bc-165">Groups with hello following highly privileged email aliases can only be created by an Azure AD global administrator.</span></span> 
  
* <span data-ttu-id="bc8bc-166">nadużyć</span><span class="sxs-lookup"><span data-stu-id="bc8bc-166">abuse</span></span> 
* <span data-ttu-id="bc8bc-167">Administrator</span><span class="sxs-lookup"><span data-stu-id="bc8bc-167">admin</span></span> 
* <span data-ttu-id="bc8bc-168">Administrator</span><span class="sxs-lookup"><span data-stu-id="bc8bc-168">administrator</span></span> 
* <span data-ttu-id="bc8bc-169">hostmaster</span><span class="sxs-lookup"><span data-stu-id="bc8bc-169">hostmaster</span></span> 
* <span data-ttu-id="bc8bc-170">majordomo</span><span class="sxs-lookup"><span data-stu-id="bc8bc-170">majordomo</span></span> 
* <span data-ttu-id="bc8bc-171">Postmaster</span><span class="sxs-lookup"><span data-stu-id="bc8bc-171">postmaster</span></span> 
* <span data-ttu-id="bc8bc-172">główny</span><span class="sxs-lookup"><span data-stu-id="bc8bc-172">root</span></span> 
* <span data-ttu-id="bc8bc-173">Zabezpieczenia</span><span class="sxs-lookup"><span data-stu-id="bc8bc-173">secure</span></span> 
* <span data-ttu-id="bc8bc-174">Zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="bc8bc-174">security</span></span> 
* <span data-ttu-id="bc8bc-175">admin protokołu SSL</span><span class="sxs-lookup"><span data-stu-id="bc8bc-175">ssl-admin</span></span> 
* <span data-ttu-id="bc8bc-176">webmaster</span><span class="sxs-lookup"><span data-stu-id="bc8bc-176">webmaster</span></span> 

## <a name="next-steps"></a><span data-ttu-id="bc8bc-177">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="bc8bc-177">Next steps</span></span>
<span data-ttu-id="bc8bc-178">Więcej dokumentacji programu PowerShell usługi Azure Active Directory można znaleźć [polecenia cmdlet usługi Azure Active Directory](/powershell/azure/install-adv2?view=azureadps-2.0).</span><span class="sxs-lookup"><span data-stu-id="bc8bc-178">You can find more Azure Active Directory PowerShell documentation at [Azure Active Directory Cmdlets](/powershell/azure/install-adv2?view=azureadps-2.0).</span></span>

* [<span data-ttu-id="bc8bc-179">Zarządzanie tooresources dostępu za pomocą grup usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bc8bc-179">Managing access tooresources with Azure Active Directory groups</span></span>](active-directory-manage-groups.md)
* [<span data-ttu-id="bc8bc-180">Integrowanie tożsamości lokalnych z usługą Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bc8bc-180">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
