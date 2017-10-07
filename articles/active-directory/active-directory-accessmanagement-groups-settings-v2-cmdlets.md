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
# <a name="azure-active-directory-version-2-cmdlets-for-group-management"></a>Usługi Active Directory w wersji 2 poleceń cmdlet systemu Azure dla grupy zarządzania
> [!div class="op_single_selector"]
> * [Witryna Azure Portal](active-directory-groups-create-azure-portal.md)
> * [Klasyczna witryna Azure Portal](active-directory-accessmanagement-manage-groups.md)
> * [PowerShell](active-directory-accessmanagement-groups-settings-v2-cmdlets.md)
>
>

Ten artykuł zawiera przykłady toouse PowerShell toomanage grup w usłudze Azure Active Directory (Azure AD).  On również informuje tooget konfiguracji z hello modułu Azure AD PowerShell. Najpierw należy [Pobierz modułu Azure AD PowerShell hello](https://www.powershellgallery.com/packages/AzureAD/).

## <a name="installing-hello-azure-ad-powershell-module"></a>Instalowanie modułu programu PowerShell usługi Azure AD hello
Moduł Azure AD PowerShell hello tooinstall, hello Użyj następującego polecenia:

    PS C:\Windows\system32> install-module azuread

tooverify, który hello moduł został zainstalowany, użyj następującego polecenia hello:

    PS C:\Windows\system32> get-module azuread

    ModuleType Version      Name                                ExportedCommands
    ---------- ---------    ----                                ----------------
    Binary     2.0.0.115    azuread                      {Add-AzureADAdministrati...}

Teraz możesz rozpocząć używać hello poleceń cmdlet w hello module. Pełny opis poleceń cmdlet hello w module hello Azure AD, można znaleźć w dokumentacji online odwołanie toohello [Azure Active Directory programu PowerShell w wersji 2](/powershell/azure/install-adv2?view=azureadps-2.0).

## <a name="connecting-toohello-directory"></a>Łączenie toohello katalogu
Aby umożliwić zarządzanie grupami za pomocą poleceń cmdlet programu PowerShell usługi Azure AD, należy połączyć ma toomanage katalogu toohello sesji programu PowerShell. Witaj Użyj następującego polecenia:

    PS C:\Windows\system32> Connect-AzureAD

Witaj polecenie cmdlet wyświetli monit dla hello poświadczeń można mają toouse tooaccess katalogu. W tym przykładzie używamy karen@drumkit.onmicrosoft.com tooaccess hello pokaz katalogu. Witaj polecenie cmdlet zwraca sesji hello tooshow potwierdzenie został pomyślnie połączony tooyour katalogu:

    Account                       Environment Tenant
    -------                       ----------- ------
    Karen@drumkit.onmicrosoft.com AzureCloud  85b5ff1e-0402-400c-9e3c-0f…

Teraz możesz rozpocząć używać hello AzureAD poleceń cmdlet toomanage grupy w katalogu.

## <a name="retrieving-groups"></a>Pobieranie grupy
tooretrieve istniejących grup z katalogu, których można używać hello polecenia cmdlet Get-AzureADGroups. tooretrieve wszystkich grup w katalogu hello, użyj hello cmdlet bez parametrów:

    PS C:\Windows\system32> get-azureadgroup

polecenia cmdlet Hello zwraca wszystkie grupy hello połączonego katalogu.

Można użyć tooretrieve parametru - objectID hello określonej grupy, dla którego należy określić objectID hello grupy:

    PS C:\Windows\system32> get-azureadgroup -ObjectId e29bae11-4ac0-450c-bc37-6dae8f3da61b

polecenie cmdlet Hello zwraca teraz hello grupy, których objectID zgodna z wartością hello parametru hello, wprowadzony:

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

Można wyszukiwać określone grupy przy użyciu hello — parametr filtru. Ten parametr przyjmuje klauzuli filtru ODATA i zwraca wszystkie grupy, które odpowiada hello filtru, tak jak hello poniższy przykład:

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
> Hello poleceń cmdlet programu AzureAD PowerShell implementuje hello standardowego zapytania OData. Aby uzyskać więcej informacji, zobacz **$filter** w [opcje zapytania systemu OData przy użyciu punktu końcowego OData hello](https://msdn.microsoft.com/library/gg309461.aspx#BKMK_filter).

## <a name="creating-groups"></a>Tworzenie grup
toocreate nową grupę w katalogu, polecenia cmdlet służącego do hello AzureADGroup nowy. To polecenie cmdlet tworzy nową grupę zabezpieczeń o nazwie "Marketing":

    PS C:\Windows\system32> New-AzureADGroup -Description "Marketing" -DisplayName "Marketing" -MailEnabled $false -SecurityEnabled $true -MailNickName "Marketing"

## <a name="updating-groups"></a>Aktualizowanie grupy
tooupdate istniejącej grupy, użyj polecenia cmdlet hello AzureADGroup zestawu. W tym przykładzie Zmieniamy hello Właściwość DisplayName hello grupy "Administratorzy usługi Intune". Po pierwsze firma Microsoft jest znajdowanie grupy hello przy użyciu polecenia cmdlet Get-AzureADGroup hello i Filtruj, używając atrybutu DisplayName hello:

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

Następnie Zmieniamy hello opis toohello nowej wartości właściwości "Administratorzy usługi Intune urządzenie":

    PS C:\Windows\system32> Set-AzureADGroup -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df -Description "Intune Device Administrators"

Teraz ponownie znalezienie hello grupy, widzimy właściwości Description hello jest zaktualizowane tooreflect hello nowej wartości:

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

## <a name="deleting-groups"></a>Usuwanie grup
grupy toodelete z katalogu, użyj polecenia cmdlet Remove-AzureADGroup hello w następujący sposób:

    PS C:\Windows\system32> Remove-AzureADGroup -ObjectId b11ca53e-07cc-455d-9a89-1fe3ab24566b

## <a name="managing-members-of-groups"></a>Zarządzanie członkami grup
Tooadd nowe elementy członkowskie tooa grupy, należy użyć polecenia cmdlet hello AzureADGroupMember Dodaj. To polecenie dodaje członek grupy Administratorzy usługi Intune toohello wykorzystane przez nas w poprzednim przykładzie hello:

    PS C:\Windows\system32> Add-AzureADGroupMember -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df -RefObjectId 72cd4bbd-2594-40a2-935c-016f3cfeeeea

Witaj - ObjectId parametr jest hello ObjectID z toowhich grupy hello chcemy tooadd członka, a hello - RefObjectId jest hello ObjectID użytkownika hello chcemy tooadd jako członek grupy toohello.

tooget hello istniejących członków grupy, użyj polecenia cmdlet Get-AzureADGroupMember hello, jak w poniższym przykładzie:

    PS C:\Windows\system32> Get-AzureADGroupMember -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df

    DeletionTimeStamp ObjectId                             ObjectType
    ----------------- --------                             ----------
                          72cd4bbd-2594-40a2-935c-016f3cfeeeea User
                          8120cc36-64b4-4080-a9e8-23aa98e8b34f User

element członkowski hello tooremove dodaliśmy wcześniej toohello grupy, użyj hello AzureADGroupMember Usuń polecenia cmdlet, jak to pokazano poniżej:

    PS C:\Windows\system32> Remove-AzureADGroupMember -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df -MemberId 72cd4bbd-2594-40a2-935c-016f3cfeeeea

tooverify hello grupy uległ użytkownika, użyj polecenia cmdlet Select AzureADGroupIdsUserIsMemberOf hello. To polecenie cmdlet przyjmuje jako parametry hello ObjectId hello użytkownika, dla których toocheck hello członkostwa w grupach oraz listę grup, dla których toocheck hello członkostwa. Witaj listę grup muszą być w formie hello złożone zmiennej typu "Microsoft.Open.AzureAD.Model.GroupIdsForMembershipCheck", dlatego firma Microsoft najpierw utworzyć zmienną z danym typem:

    PS C:\Windows\system32> $g = new-object Microsoft.Open.AzureAD.Model.GroupIdsForMembershipCheck

Następnie możemy podać wartości toocheck identyfikatory GroupID hello w atrybucie hello identyfikatory "GroupID" tej zmiennej złożone:

    PS C:\Windows\system32> $g.GroupIds = "b11ca53e-07cc-455d-9a89-1fe3ab24566b", "31f1ff6c-d48c-4f8a-b2e1-abca7fd399df"

Teraz Jeśli chcemy toocheck hello członkostwa w grupach użytkownika z 72cd4bbd-2594-40a2-935c-016f3cfeeeea ObjectID względem grupy hello w $g powinniśmy skorzystać:

    PS C:\Windows\system32> Select-AzureADGroupIdsUserIsMemberOf -ObjectId 72cd4bbd-2594-40a2-935c-016f3cfeeeea -GroupIdsForMembershipCheck $g

    OdataMetadata                                                                                                 Value
    -------------                                                                                                  -----
    https://graph.windows.net/85b5ff1e-0402-400c-9e3c-0f9e965325d1/$metadata#Collection(Edm.String)             {31f1ff6c-d48c-4f8a-b2e1-abca7fd399df}


wartość Hello, zwracana jest lista grup, których członkiem jest ten użytkownik. Można także zastosować dla tej metody toocheck kontakty, grupy lub podmiotów zabezpieczeń usługi członkostwa dla danej listy grup, za pomocą AzureADGroupIdsContactIsMemberOf Select, wybierz AzureADGroupIdsGroupIsMemberOf lub Wybierz AzureADGroupIdsServicePrincipalIsMemberOf

## <a name="managing-owners-of-groups"></a>Zarządzanie właścicielami grupy
Grupa tooadd właścicieli tooa, polecenia cmdlet służącego do hello AzureADGroupOwner Dodaj:

    PS C:\Windows\system32> Add-AzureADGroupOwner -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df -RefObjectId 72cd4bbd-2594-40a2-935c-016f3cfeeeea

Witaj - ObjectId parametr jest hello ObjectID z toowhich grupy hello chcemy tooadd właściciela i hello - RefObjectId jest hello ObjectID użytkownika hello chcemy tooadd jako właściciel grupy hello.

tooretrieve hello właścicieli grupy, użyj polecenia cmdlet Get-AzureADGroupOwner hello:

    PS C:\Windows\system32> Get-AzureADGroupOwner -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df

polecenia cmdlet Hello zwraca listę hello właścicieli dla określonej grupy hello:

    DeletionTimeStamp ObjectId                             ObjectType
    ----------------- --------                             ----------
                          e831b3fd-77c9-49c7-9fca-de43e109ef67 User

Jeśli chcesz tooremove właściciela z grupy, użyj polecenia cmdlet Remove-AzureADGroupOwner hello:

    PS C:\Windows\system32> remove-AzureADGroupOwner -ObjectId 31f1ff6c-d48c-4f8a-b2e1-abca7fd399df -OwnerId e831b3fd-77c9-49c7-9fca-de43e109ef67

## <a name="reserved-aliases"></a>Aliasy zastrzeżone 
Po utworzeniu grupy niektóre punkty końcowe umożliwiają hello użytkownika końcowego toospecify toobe mailNickname lub alias, używana jako część adresu e-mail hello hello grupy. Grupy z powitania po aliasów e-mail wysoko uprzywilejowane można tworzyć tylko przez administratora globalnego usługi Azure AD. 
  
* nadużyć 
* Administrator 
* Administrator 
* hostmaster 
* majordomo 
* Postmaster 
* główny 
* Zabezpieczenia 
* Zabezpieczeń 
* admin protokołu SSL 
* webmaster 

## <a name="next-steps"></a>Następne kroki
Więcej dokumentacji programu PowerShell usługi Azure Active Directory można znaleźć [polecenia cmdlet usługi Azure Active Directory](/powershell/azure/install-adv2?view=azureadps-2.0).

* [Zarządzanie tooresources dostępu za pomocą grup usługi Azure Active Directory](active-directory-manage-groups.md)
* [Integrowanie tożsamości lokalnych z usługą Azure Active Directory](active-directory-aadconnect.md)
