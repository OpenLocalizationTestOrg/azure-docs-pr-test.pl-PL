---
title: "Ustawienia grupy aaaConfigure za pomocą poleceń cmdlet usługi Azure Active Directory | Dokumentacja firmy Microsoft"
description: "Jak zarządzać hello ustawienia grup za pomocą poleceń cmdlet usługi Azure Active Directory"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 9f2090e6-3af4-4f07-bbb2-1d18dae89b73
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: curtand
ms.reviewer: kairaz.contractor
ms.custom: it-pro;
ms.openlocfilehash: 46db49d9dec3eaa41c97ca74c57854189eddc16d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-cmdlets-for-configuring-group-settings"></a>Polecenia cmdlet usługi Azure Active Directory służące do konfigurowania ustawień grupy

> [!IMPORTANT]
> Ta zawartość dotyczy tylko tooOffice 365 grupy. Aby uzyskać więcej informacji na temat grup zabezpieczeń toocreate użytkowników tooallow, ustaw `Set-MSOLCompanySettings -UsersPermissionToCreateGroupsEnabled $True` zgodnie z opisem w [Set-MSOLCompanySettings](https://docs.microsoft.com/en-us/powershell/module/msonline/set-msolcompanysettings?view=azureadps-1.0). 

Ustawienia grup usługi Office 365 są skonfigurowane przy użyciu obiektu ustawień i obiektu SettingsTemplate. Początkowo nie widać żadnych ustawień obiektów w danym katalogu, ponieważ katalog jest skonfigurowany z ustawieniami domyślnymi hello. toochange hello domyślne ustawienia, należy utworzyć nowy obiekt ustawień używany szablon ustawienia. Ustawienia szablonów są definiowane przez firmę Microsoft. Istnieje kilka szablonów różne ustawienia. Ustawienia grupy tooconfigure usługi Office 365 dla katalogu, użyj szablonu hello o nazwie "Group.Unified". Ustawienia grupy tooconfigure usługi Office 365 na pojedynczej grupy, użyj szablonu hello o nazwie "Group.Unified.Guest". Ten szablon jest używany toomanage gościa dostęp tooan usługi Office 365 grupy. 

polecenia cmdlet Hello są częścią modułu hello Azure Active Directory programu PowerShell w wersji 2. Instrukcje jak toodownload i modułu hello instalacji na komputerze, zobacz artykuł hello [Azure Active Directory programu PowerShell w wersji 2](https://docs.microsoft.com/powershell/azuread/). Można zainstalować wersji w wersji 2 hello hello modułu na podstawie [galerii programu PowerShell hello](https://www.powershellgallery.com/packages/AzureAD/).

## <a name="retrieve-a-specific-settings-value"></a>Pobierz wartość określonych ustawień
Jeśli znasz nazwę hello hello ustawienie tooretrieve, można użyć hello poniżej polecenia cmdlet tooretrieve hello bieżące ustawienia wartości. W tym przykładzie mamy pobierania hello wartość ustawienia o nazwie "UsageGuidelinesUrl." Możesz zapoznać się, że więcej informacji na temat ustawień katalogu i nazw bardziej szczegółowo w dół w tym artykule.

```powershell
(Get-AzureADDirectorySetting).Values | Where-Object -Property Name -Value UsageGuidelinesUrl -EQ
```

## <a name="create-settings-at-hello-directory-level"></a>Utwórz ustawienia na poziomie katalogu hello
Te kroki tworzenia ustawień na poziomie katalogu stosować tooall usługi Office 365 (grup Unified) w katalogu hello.

1. W hello DirectorySettings poleceń cmdlet należy określić identyfikator hello hello SettingsTemplate ma toouse. Jeśli nie znasz tego Identyfikatora, to polecenie cmdlet zwraca hello listę wszystkich szablonów ustawienia:
  
  ```
  PS C:> Get-AzureADDirectorySettingTemplate
  ```
  To wywołanie polecenia cmdlet zwraca wszystkie szablony, które są dostępne:
  
  ```
  Id                                   DisplayName         Description
  --                                   -----------         -----------
  62375ab9-6b52-47ed-826b-58e47e0e304b Group.Unified       ...
  08d542b9-071f-4e16-94b0-74abb372e3d9 Group.Unified.Guest Settings for a specific Unified Group
  16933506-8a8d-4f0d-ad58-e1db05a5b929 Company.BuiltIn     Setting templates define hello different settings that can be used for hello associ...
  4bc7f740-180e-4586-adb6-38b2e9024e6b Application...
  898f1161-d651-43d1-805c-3b0b388a9fc2 Custom Policy       Settings ...
  5cf42378-d67d-4f36-ba46-e8b86229381d Password Rule       Settings ...
  ```
2. tooadd URL wskazówek dotyczących użycia, należy najpierw tooget hello SettingsTemplate obiektu, który definiuje wartość adresu URL wskazówek dotyczących użycia hello; oznacza to, że hello Group.Unified szablonu:
  
  ```
  $Template = Get-AzureADDirectorySettingTemplate -Id 62375ab9-6b52-47ed-826b-58e47e0e304b
  ```
3. Następnie należy utworzyć nowy obiekt ustawień na podstawie tego szablonu:
  
  ```
  $Setting = $template.CreateDirectorySetting()
  ```  
4. Następnie zaktualizuj wartość wskazówek dotyczących użycia hello:
  
  ```
  $setting["UsageGuidelinesUrl"] = "<https://guideline.com>"
  ```  
5. Na koniec Zastosuj ustawienia hello:
  
  ```
  New-AzureADDirectorySetting -DirectorySetting $setting
  ```

Po pomyślnym zakończeniu hello polecenie cmdlet zwraca identyfikator hello hello nowy obiekt ustawień:
  ```
  Id                                   DisplayName TemplateId                           Values
  --                                   ----------- ----------                           ------
  c391b57d-5783-4c53-9236-cefb5c6ef323             62375ab9-6b52-47ed-826b-58e47e0e304b {class SettingValue {...
  ```
Poniżej przedstawiono ustawienia hello zdefiniowane w hello Group.Unified SettingsTemplate.

| **Ustawienie** | **Opis** |
| --- | --- |
|  <ul><li>EnableGroupCreation<li>Typ: wartość logiczna<li>Domyślnie: True |Hello flagę wskazującą, czy w katalogu hello dozwolona jest utworzenie grupy Unified. |
|  <ul><li>GroupCreationAllowedGroupId<li>Typ: ciąg<li>Wartość domyślna: "" |Identyfikator GUID hello grupy zabezpieczeń, dla których hello elementy członkowskie są dozwolone grupy Unified toocreate nawet wtedy, gdy EnableGroupCreation == false. |
|  <ul><li>UsageGuidelinesUrl<li>Typ: ciąg<li>Wartość domyślna: "" |Toohello łącze wskazówki dotyczące użycia grupy. |
|  <ul><li>ClassificationDescriptions<li>Typ: ciąg<li>Wartość domyślna: "" | Rozdzielana przecinkami lista Opisy klasyfikacji. |
|  <ul><li>DefaultClassification<li>Typ: ciąg<li>Wartość domyślna: "" | Klasyfikacja Hello, który jest używany jako hello domyślnej klasyfikacji dla grupy, jeśli nie podano żadnej toobe.|
|  <ul><li>PrefixSuffixNamingRequirement<li>Typ: ciąg<li>Wartość domyślna: "" |Nie zaimplementowano jeszcze
|  <ul><li>AllowGuestsToBeGroupOwner<li>Typ: wartość logiczna<li>Domyślnie: False | Wartość logiczna wskazująca, czy użytkownika gościa może być właścicielem grupy. |
|  <ul><li>AllowGuestsToAccessGroups<li>Typ: wartość logiczna<li>Domyślnie: True | Wartość logiczna wskazująca, czy użytkownika gościa może mieć właściwość content grupy tooUnified dostępu. |
|  <ul><li>GuestUsageGuidelinesUrl<li>Typ: ciąg<li>Wartość domyślna: "" | adres url Hello wskazówki dotyczące użycia łącza toohello gościa. |
|  <ul><li>AllowToAddGuests<li>Typ: wartość logiczna<li>Domyślnie: True | Wartość logiczna wskazująca, czy jest dozwolone tooadd gości toothis katalogu.|
|  <ul><li>ClassificationList<li>Typ: ciąg<li>Wartość domyślna: "" |Rozdzielana przecinkami lista wartości prawidłowe klasyfikacji, które mogą być zastosowane tooUnified grup. |
|  <ul><li>EnableGroupCreation<li>Typ: wartość logiczna<li>Domyślnie: True | Wartość logiczna wskazująca, czy użytkownicy niebędący administratorami można tworzyć nowe grupy Unified. |


## <a name="read-settings-at-hello-directory-level"></a>Odczytaj ustawienia na poziomie katalogu hello
Następujące kroki odczytać ustawień na poziomie katalogu, które mają zastosowanie grupy Office tooall w katalogu hello.

1. Przeczytaj wszystkich istniejących ustawień katalogu:
  ```
  Get-AzureADDirectorySetting -All $True
  ```
  To polecenie cmdlet zwraca listę wszystkich ustawień katalogu:
  ```
  Id                                   DisplayName   TemplateId                           Values
  --                                   -----------   ----------                           ------
  c391b57d-5783-4c53-9236-cefb5c6ef323 Group.Unified 62375ab9-6b52-47ed-826b-58e47e0e304b {class SettingValue {...
  ```

2. Odczytywanie wszystkich ustawień dla określonej grupy:
  ```
  Get-AzureADObjectSetting -TargetObjectId ab6a3887-776a-4db7-9da4-ea2b0d63c504 -TargetType Groups
  ```

3. Przeczytaj wszystkie wartości obiektu ustawienia określonego katalogu, za pomocą ustawienia identyfikatora GUID ustawień katalogu:
  ```
  (Get-AzureADDirectorySetting -Id c391b57d-5783-4c53-9236-cefb5c6ef323).values
  ```
  To polecenie cmdlet zwraca hello nazwy i wartości w tym obiekcie ustawienia dla tej określonej grupie:
  ```
  Name                          Value
  ----                          -----
  ClassificationDescriptions
  DefaultClassification
  PrefixSuffixNamingRequirement
  AllowGuestsToBeGroupOwner     False 
  AllowGuestsToAccessGroups     True
  GuestUsageGuidelinesUrl
  GroupCreationAllowedGroupId
  AllowToAddGuests              True
  UsageGuidelinesUrl            <https://guideline.com>
  ClassificationList
  EnableGroupCreation           True
  ```

## <a name="update-settings-for-a-specific-group"></a>Ustawienia aktualizacji dla określonej grupy

1. Wyszukaj hello ustawienia szablonu o nazwie "Groups.Unified.Guest"
  ```
  Get-AzureADDirectorySettingTemplate
  
  Id                                   DisplayName            Description
  --                                   -----------            -----------
  62375ab9-6b52-47ed-826b-58e47e0e304b Group.Unified          ...
  08d542b9-071f-4e16-94b0-74abb372e3d9 Group.Unified.Guest    Settings for a specific Unified Group
  4bc7f740-180e-4586-adb6-38b2e9024e6b Application            ...
  898f1161-d651-43d1-805c-3b0b388a9fc2 Custom Policy Settings ...
  5cf42378-d67d-4f36-ba46-e8b86229381d Password Rule Settings ...
  ```
2. Pobierz obiekt szablonu hello hello Groups.Unified.Guest szablonu:
  ```
  $Template = Get-AzureADDirectorySettingTemplate -Id 08d542b9-071f-4e16-94b0-74abb372e3d9
  ```
3. Utwórz nowy obiekt ustawień z szablonu hello:
  ```
  $Setting = $Template.CreateDirectorySetting()
  ```

4. Ustaw wartość toohello wymagane ustawienia hello:
  ```
  $Setting["AllowToAddGuests"]=$False
  ```
5. Tworzenie nowego ustawienia hello hello wymaganej grupy w katalogu hello:
  ```
  New-AzureADObjectSetting -TargetType Groups -TargetObjectId ab6a3887-776a-4db7-9da4-ea2b0d63c504 -DirectorySetting $Setting
  
  Id                                   DisplayName TemplateId                           Values
  --                                   ----------- ----------                           ------
  25651479-a26e-4181-afce-ce24111b2cb5             08d542b9-071f-4e16-94b0-74abb372e3d9 {class SettingValue {...
  ```

## <a name="update-settings-at-hello-directory-level"></a>Zaktualizuj ustawienia na poziomie katalogu hello

Te kroki zaktualizować ustawienia na poziomie katalogu, które tooall Unified grup w katalogu hello. Tych przykładów założono, że istnieje już obiekt ustawień w katalogu.

1. Znajdź istniejący obiekt ustawień hello:
  ```
  Get-AzureADDirectorySetting | Where-object -Property Displayname -Value "Group.Unified" -EQ
  
  Id                                   DisplayName   TemplateId                           Values
  --                                   -----------   ----------                           ------
  c391b57d-5783-4c53-9236-cefb5c6ef323 Group.Unified 62375ab9-6b52-47ed-826b-58e47e0e304b {class SettingValue {...
  
  $setting = Get-AzureADDirectorySetting –Id c391b57d-5783-4c53-9236-cefb5c6ef323
  ```
2. Zaktualizuj wartość hello:
  
  ```
  $Setting["AllowToAddGuests"] = "false"
  ```
3. Zaktualizuj ustawienie hello:
  
  ```
  Set-AzureADDirectorySetting -Id c391b57d-5783-4c53-9236-cefb5c6ef323 -DirectorySetting $Setting
  ```

## <a name="remove-settings-at-hello-directory-level"></a>Usuń ustawienia na poziomie katalogu hello
Ten krok powoduje usunięcie ustawień na poziomie katalogu, które mają zastosowanie grupy Office tooall w katalogu hello.
  ```
  Remove-AzureADDirectorySetting –Id c391b57d-5783-4c53-9236-cefb5c6ef323c
  ```

## <a name="cmdlet-syntax-reference"></a>Odwołania do składni polecenia cmdlet
Więcej dokumentacji programu PowerShell usługi Azure Active Directory można znaleźć [polecenia cmdlet usługi Azure Active Directory](/powershell/azure/install-adv2?view=azureadps-2.0).

## <a name="additional-reading"></a>Dodatkowe materiały

* [Zarządzanie tooresources dostępu za pomocą grup usługi Azure Active Directory](active-directory-manage-groups.md)
* [Integrowanie tożsamości lokalnych z usługą Azure Active Directory](active-directory-aadconnect.md)
