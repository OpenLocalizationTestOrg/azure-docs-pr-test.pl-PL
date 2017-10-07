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
# <a name="azure-active-directory-cmdlets-for-configuring-group-settings"></a><span data-ttu-id="77e37-103">Polecenia cmdlet usługi Azure Active Directory służące do konfigurowania ustawień grupy</span><span class="sxs-lookup"><span data-stu-id="77e37-103">Azure Active Directory cmdlets for configuring group settings</span></span>

> [!IMPORTANT]
> <span data-ttu-id="77e37-104">Ta zawartość dotyczy tylko tooOffice 365 grupy.</span><span class="sxs-lookup"><span data-stu-id="77e37-104">This content applies only tooOffice 365 groups.</span></span> <span data-ttu-id="77e37-105">Aby uzyskać więcej informacji na temat grup zabezpieczeń toocreate użytkowników tooallow, ustaw `Set-MSOLCompanySettings -UsersPermissionToCreateGroupsEnabled $True` zgodnie z opisem w [Set-MSOLCompanySettings](https://docs.microsoft.com/en-us/powershell/module/msonline/set-msolcompanysettings?view=azureadps-1.0).</span><span class="sxs-lookup"><span data-stu-id="77e37-105">For more information on how tooallow users toocreate Security groups, set `Set-MSOLCompanySettings -UsersPermissionToCreateGroupsEnabled $True` as described in [Set-MSOLCompanySettings](https://docs.microsoft.com/en-us/powershell/module/msonline/set-msolcompanysettings?view=azureadps-1.0).</span></span> 

<span data-ttu-id="77e37-106">Ustawienia grup usługi Office 365 są skonfigurowane przy użyciu obiektu ustawień i obiektu SettingsTemplate.</span><span class="sxs-lookup"><span data-stu-id="77e37-106">Office 365 Groups settings are configured using a Settings object and a SettingsTemplate object.</span></span> <span data-ttu-id="77e37-107">Początkowo nie widać żadnych ustawień obiektów w danym katalogu, ponieważ katalog jest skonfigurowany z ustawieniami domyślnymi hello.</span><span class="sxs-lookup"><span data-stu-id="77e37-107">Initially, you don't see any Settings objects in your directory, because your directory is configured with hello default settings.</span></span> <span data-ttu-id="77e37-108">toochange hello domyślne ustawienia, należy utworzyć nowy obiekt ustawień używany szablon ustawienia.</span><span class="sxs-lookup"><span data-stu-id="77e37-108">toochange hello default settings, you must create a new settings object using a settings template.</span></span> <span data-ttu-id="77e37-109">Ustawienia szablonów są definiowane przez firmę Microsoft.</span><span class="sxs-lookup"><span data-stu-id="77e37-109">Settings templates are defined by Microsoft.</span></span> <span data-ttu-id="77e37-110">Istnieje kilka szablonów różne ustawienia.</span><span class="sxs-lookup"><span data-stu-id="77e37-110">There are several different settings templates.</span></span> <span data-ttu-id="77e37-111">Ustawienia grupy tooconfigure usługi Office 365 dla katalogu, użyj szablonu hello o nazwie "Group.Unified".</span><span class="sxs-lookup"><span data-stu-id="77e37-111">tooconfigure Office 365 group settings for your directory, you use hello template named "Group.Unified".</span></span> <span data-ttu-id="77e37-112">Ustawienia grupy tooconfigure usługi Office 365 na pojedynczej grupy, użyj szablonu hello o nazwie "Group.Unified.Guest".</span><span class="sxs-lookup"><span data-stu-id="77e37-112">tooconfigure Office 365 group settings on a single group, use hello template named "Group.Unified.Guest".</span></span> <span data-ttu-id="77e37-113">Ten szablon jest używany toomanage gościa dostęp tooan usługi Office 365 grupy.</span><span class="sxs-lookup"><span data-stu-id="77e37-113">This template is used toomanage guest access tooan Office 365 group.</span></span> 

<span data-ttu-id="77e37-114">polecenia cmdlet Hello są częścią modułu hello Azure Active Directory programu PowerShell w wersji 2.</span><span class="sxs-lookup"><span data-stu-id="77e37-114">hello cmdlets are part of hello Azure Active Directory PowerShell V2 module.</span></span> <span data-ttu-id="77e37-115">Instrukcje jak toodownload i modułu hello instalacji na komputerze, zobacz artykuł hello [Azure Active Directory programu PowerShell w wersji 2](https://docs.microsoft.com/powershell/azuread/).</span><span class="sxs-lookup"><span data-stu-id="77e37-115">For instructions how toodownload and install hello module on your computer, see hello article [Azure Active Directory PowerShell Version 2](https://docs.microsoft.com/powershell/azuread/).</span></span> <span data-ttu-id="77e37-116">Można zainstalować wersji w wersji 2 hello hello modułu na podstawie [galerii programu PowerShell hello](https://www.powershellgallery.com/packages/AzureAD/).</span><span class="sxs-lookup"><span data-stu-id="77e37-116">You can install hello version 2 release of hello module from [hello PowerShell gallery](https://www.powershellgallery.com/packages/AzureAD/).</span></span>

## <a name="retrieve-a-specific-settings-value"></a><span data-ttu-id="77e37-117">Pobierz wartość określonych ustawień</span><span class="sxs-lookup"><span data-stu-id="77e37-117">Retrieve a specific settings value</span></span>
<span data-ttu-id="77e37-118">Jeśli znasz nazwę hello hello ustawienie tooretrieve, można użyć hello poniżej polecenia cmdlet tooretrieve hello bieżące ustawienia wartości.</span><span class="sxs-lookup"><span data-stu-id="77e37-118">If you know hello name of hello setting you want tooretrieve, you can use hello below cmdlet tooretrieve hello current settings value.</span></span> <span data-ttu-id="77e37-119">W tym przykładzie mamy pobierania hello wartość ustawienia o nazwie "UsageGuidelinesUrl."</span><span class="sxs-lookup"><span data-stu-id="77e37-119">In this example, we're retrieving hello value for a setting named "UsageGuidelinesUrl."</span></span> <span data-ttu-id="77e37-120">Możesz zapoznać się, że więcej informacji na temat ustawień katalogu i nazw bardziej szczegółowo w dół w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="77e37-120">You can read more about directory settings and their names further down in this article.</span></span>

```powershell
(Get-AzureADDirectorySetting).Values | Where-Object -Property Name -Value UsageGuidelinesUrl -EQ
```

## <a name="create-settings-at-hello-directory-level"></a><span data-ttu-id="77e37-121">Utwórz ustawienia na poziomie katalogu hello</span><span class="sxs-lookup"><span data-stu-id="77e37-121">Create settings at hello directory level</span></span>
<span data-ttu-id="77e37-122">Te kroki tworzenia ustawień na poziomie katalogu stosować tooall usługi Office 365 (grup Unified) w katalogu hello.</span><span class="sxs-lookup"><span data-stu-id="77e37-122">These steps create settings at directory level, which apply tooall Office 365 groups (Unified groups) in hello directory.</span></span>

1. <span data-ttu-id="77e37-123">W hello DirectorySettings poleceń cmdlet należy określić identyfikator hello hello SettingsTemplate ma toouse.</span><span class="sxs-lookup"><span data-stu-id="77e37-123">In hello DirectorySettings cmdlets, you must specify hello ID of hello SettingsTemplate you want toouse.</span></span> <span data-ttu-id="77e37-124">Jeśli nie znasz tego Identyfikatora, to polecenie cmdlet zwraca hello listę wszystkich szablonów ustawienia:</span><span class="sxs-lookup"><span data-stu-id="77e37-124">If you do not know this ID, this cmdlet returns hello list of all settings templates:</span></span>
  
  ```
  PS C:> Get-AzureADDirectorySettingTemplate
  ```
  <span data-ttu-id="77e37-125">To wywołanie polecenia cmdlet zwraca wszystkie szablony, które są dostępne:</span><span class="sxs-lookup"><span data-stu-id="77e37-125">This cmdlet call returns all templates that are available:</span></span>
  
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
2. <span data-ttu-id="77e37-126">tooadd URL wskazówek dotyczących użycia, należy najpierw tooget hello SettingsTemplate obiektu, który definiuje wartość adresu URL wskazówek dotyczących użycia hello; oznacza to, że hello Group.Unified szablonu:</span><span class="sxs-lookup"><span data-stu-id="77e37-126">tooadd a usage guideline URL, first you need tooget hello SettingsTemplate object that defines hello usage guideline URL value; that is, hello Group.Unified template:</span></span>
  
  ```
  $Template = Get-AzureADDirectorySettingTemplate -Id 62375ab9-6b52-47ed-826b-58e47e0e304b
  ```
3. <span data-ttu-id="77e37-127">Następnie należy utworzyć nowy obiekt ustawień na podstawie tego szablonu:</span><span class="sxs-lookup"><span data-stu-id="77e37-127">Next, create a new settings object based on that template:</span></span>
  
  ```
  $Setting = $template.CreateDirectorySetting()
  ```  
4. <span data-ttu-id="77e37-128">Następnie zaktualizuj wartość wskazówek dotyczących użycia hello:</span><span class="sxs-lookup"><span data-stu-id="77e37-128">Then update hello usage guideline value:</span></span>
  
  ```
  $setting["UsageGuidelinesUrl"] = "<https://guideline.com>"
  ```  
5. <span data-ttu-id="77e37-129">Na koniec Zastosuj ustawienia hello:</span><span class="sxs-lookup"><span data-stu-id="77e37-129">Finally, apply hello settings:</span></span>
  
  ```
  New-AzureADDirectorySetting -DirectorySetting $setting
  ```

<span data-ttu-id="77e37-130">Po pomyślnym zakończeniu hello polecenie cmdlet zwraca identyfikator hello hello nowy obiekt ustawień:</span><span class="sxs-lookup"><span data-stu-id="77e37-130">Upon successful completion, hello cmdlet returns hello ID of hello new settings object:</span></span>
  ```
  Id                                   DisplayName TemplateId                           Values
  --                                   ----------- ----------                           ------
  c391b57d-5783-4c53-9236-cefb5c6ef323             62375ab9-6b52-47ed-826b-58e47e0e304b {class SettingValue {...
  ```
<span data-ttu-id="77e37-131">Poniżej przedstawiono ustawienia hello zdefiniowane w hello Group.Unified SettingsTemplate.</span><span class="sxs-lookup"><span data-stu-id="77e37-131">Here are hello settings defined in hello Group.Unified SettingsTemplate.</span></span>

| <span data-ttu-id="77e37-132">**Ustawienie**</span><span class="sxs-lookup"><span data-stu-id="77e37-132">**Setting**</span></span> | <span data-ttu-id="77e37-133">**Opis**</span><span class="sxs-lookup"><span data-stu-id="77e37-133">**Description**</span></span> |
| --- | --- |
|  <ul><li><span data-ttu-id="77e37-134">EnableGroupCreation</span><span class="sxs-lookup"><span data-stu-id="77e37-134">EnableGroupCreation</span></span><li><span data-ttu-id="77e37-135">Typ: wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="77e37-135">Type: Boolean</span></span><li><span data-ttu-id="77e37-136">Domyślnie: True</span><span class="sxs-lookup"><span data-stu-id="77e37-136">Default: True</span></span> |<span data-ttu-id="77e37-137">Hello flagę wskazującą, czy w katalogu hello dozwolona jest utworzenie grupy Unified.</span><span class="sxs-lookup"><span data-stu-id="77e37-137">hello flag indicating whether Unified Group creation is allowed in hello directory.</span></span> |
|  <ul><li><span data-ttu-id="77e37-138">GroupCreationAllowedGroupId</span><span class="sxs-lookup"><span data-stu-id="77e37-138">GroupCreationAllowedGroupId</span></span><li><span data-ttu-id="77e37-139">Typ: ciąg</span><span class="sxs-lookup"><span data-stu-id="77e37-139">Type: String</span></span><li><span data-ttu-id="77e37-140">Wartość domyślna: ""</span><span class="sxs-lookup"><span data-stu-id="77e37-140">Default: “”</span></span> |<span data-ttu-id="77e37-141">Identyfikator GUID hello grupy zabezpieczeń, dla których hello elementy członkowskie są dozwolone grupy Unified toocreate nawet wtedy, gdy EnableGroupCreation == false.</span><span class="sxs-lookup"><span data-stu-id="77e37-141">GUID of hello security group for which hello members are allowed toocreate Unified Groups even when EnableGroupCreation == false.</span></span> |
|  <ul><li><span data-ttu-id="77e37-142">UsageGuidelinesUrl</span><span class="sxs-lookup"><span data-stu-id="77e37-142">UsageGuidelinesUrl</span></span><li><span data-ttu-id="77e37-143">Typ: ciąg</span><span class="sxs-lookup"><span data-stu-id="77e37-143">Type: String</span></span><li><span data-ttu-id="77e37-144">Wartość domyślna: ""</span><span class="sxs-lookup"><span data-stu-id="77e37-144">Default: “”</span></span> |<span data-ttu-id="77e37-145">Toohello łącze wskazówki dotyczące użycia grupy.</span><span class="sxs-lookup"><span data-stu-id="77e37-145">A link toohello Group Usage Guidelines.</span></span> |
|  <ul><li><span data-ttu-id="77e37-146">ClassificationDescriptions</span><span class="sxs-lookup"><span data-stu-id="77e37-146">ClassificationDescriptions</span></span><li><span data-ttu-id="77e37-147">Typ: ciąg</span><span class="sxs-lookup"><span data-stu-id="77e37-147">Type: String</span></span><li><span data-ttu-id="77e37-148">Wartość domyślna: ""</span><span class="sxs-lookup"><span data-stu-id="77e37-148">Default: “”</span></span> | <span data-ttu-id="77e37-149">Rozdzielana przecinkami lista Opisy klasyfikacji.</span><span class="sxs-lookup"><span data-stu-id="77e37-149">A comma-delimited list of classification descriptions.</span></span> |
|  <ul><li><span data-ttu-id="77e37-150">DefaultClassification</span><span class="sxs-lookup"><span data-stu-id="77e37-150">DefaultClassification</span></span><li><span data-ttu-id="77e37-151">Typ: ciąg</span><span class="sxs-lookup"><span data-stu-id="77e37-151">Type: String</span></span><li><span data-ttu-id="77e37-152">Wartość domyślna: ""</span><span class="sxs-lookup"><span data-stu-id="77e37-152">Default: “”</span></span> | <span data-ttu-id="77e37-153">Klasyfikacja Hello, który jest używany jako hello domyślnej klasyfikacji dla grupy, jeśli nie podano żadnej toobe.</span><span class="sxs-lookup"><span data-stu-id="77e37-153">hello classification that is toobe used as hello default classification for a group if none was specified.</span></span>|
|  <ul><li><span data-ttu-id="77e37-154">PrefixSuffixNamingRequirement</span><span class="sxs-lookup"><span data-stu-id="77e37-154">PrefixSuffixNamingRequirement</span></span><li><span data-ttu-id="77e37-155">Typ: ciąg</span><span class="sxs-lookup"><span data-stu-id="77e37-155">Type: String</span></span><li><span data-ttu-id="77e37-156">Wartość domyślna: ""</span><span class="sxs-lookup"><span data-stu-id="77e37-156">Default: “”</span></span> |<span data-ttu-id="77e37-157">Nie zaimplementowano jeszcze</span><span class="sxs-lookup"><span data-stu-id="77e37-157">Not implemented yet</span></span>
|  <ul><li><span data-ttu-id="77e37-158">AllowGuestsToBeGroupOwner</span><span class="sxs-lookup"><span data-stu-id="77e37-158">AllowGuestsToBeGroupOwner</span></span><li><span data-ttu-id="77e37-159">Typ: wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="77e37-159">Type: Boolean</span></span><li><span data-ttu-id="77e37-160">Domyślnie: False</span><span class="sxs-lookup"><span data-stu-id="77e37-160">Default: False</span></span> | <span data-ttu-id="77e37-161">Wartość logiczna wskazująca, czy użytkownika gościa może być właścicielem grupy.</span><span class="sxs-lookup"><span data-stu-id="77e37-161">Boolean indicating whether or not a guest user can be an owner of groups.</span></span> |
|  <ul><li><span data-ttu-id="77e37-162">AllowGuestsToAccessGroups</span><span class="sxs-lookup"><span data-stu-id="77e37-162">AllowGuestsToAccessGroups</span></span><li><span data-ttu-id="77e37-163">Typ: wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="77e37-163">Type: Boolean</span></span><li><span data-ttu-id="77e37-164">Domyślnie: True</span><span class="sxs-lookup"><span data-stu-id="77e37-164">Default: True</span></span> | <span data-ttu-id="77e37-165">Wartość logiczna wskazująca, czy użytkownika gościa może mieć właściwość content grupy tooUnified dostępu.</span><span class="sxs-lookup"><span data-stu-id="77e37-165">Boolean indicating whether or not a guest user can have access tooUnified groups' content.</span></span> |
|  <ul><li><span data-ttu-id="77e37-166">GuestUsageGuidelinesUrl</span><span class="sxs-lookup"><span data-stu-id="77e37-166">GuestUsageGuidelinesUrl</span></span><li><span data-ttu-id="77e37-167">Typ: ciąg</span><span class="sxs-lookup"><span data-stu-id="77e37-167">Type: String</span></span><li><span data-ttu-id="77e37-168">Wartość domyślna: ""</span><span class="sxs-lookup"><span data-stu-id="77e37-168">Default: “”</span></span> | <span data-ttu-id="77e37-169">adres url Hello wskazówki dotyczące użycia łącza toohello gościa.</span><span class="sxs-lookup"><span data-stu-id="77e37-169">hello url of a link toohello guest usage guidelines.</span></span> |
|  <ul><li><span data-ttu-id="77e37-170">AllowToAddGuests</span><span class="sxs-lookup"><span data-stu-id="77e37-170">AllowToAddGuests</span></span><li><span data-ttu-id="77e37-171">Typ: wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="77e37-171">Type: Boolean</span></span><li><span data-ttu-id="77e37-172">Domyślnie: True</span><span class="sxs-lookup"><span data-stu-id="77e37-172">Default: True</span></span> | <span data-ttu-id="77e37-173">Wartość logiczna wskazująca, czy jest dozwolone tooadd gości toothis katalogu.</span><span class="sxs-lookup"><span data-stu-id="77e37-173">A boolean indicating whether or not is allowed tooadd guests toothis directory.</span></span>|
|  <ul><li><span data-ttu-id="77e37-174">ClassificationList</span><span class="sxs-lookup"><span data-stu-id="77e37-174">ClassificationList</span></span><li><span data-ttu-id="77e37-175">Typ: ciąg</span><span class="sxs-lookup"><span data-stu-id="77e37-175">Type: String</span></span><li><span data-ttu-id="77e37-176">Wartość domyślna: ""</span><span class="sxs-lookup"><span data-stu-id="77e37-176">Default: “”</span></span> |<span data-ttu-id="77e37-177">Rozdzielana przecinkami lista wartości prawidłowe klasyfikacji, które mogą być zastosowane tooUnified grup.</span><span class="sxs-lookup"><span data-stu-id="77e37-177">A comma-delimited list of valid classification values that can be applied tooUnified Groups.</span></span> |
|  <ul><li><span data-ttu-id="77e37-178">EnableGroupCreation</span><span class="sxs-lookup"><span data-stu-id="77e37-178">EnableGroupCreation</span></span><li><span data-ttu-id="77e37-179">Typ: wartość logiczna</span><span class="sxs-lookup"><span data-stu-id="77e37-179">Type: Boolean</span></span><li><span data-ttu-id="77e37-180">Domyślnie: True</span><span class="sxs-lookup"><span data-stu-id="77e37-180">Default: True</span></span> | <span data-ttu-id="77e37-181">Wartość logiczna wskazująca, czy użytkownicy niebędący administratorami można tworzyć nowe grupy Unified.</span><span class="sxs-lookup"><span data-stu-id="77e37-181">A boolean indicating whether or not non-admin users can create new Unified groups.</span></span> |


## <a name="read-settings-at-hello-directory-level"></a><span data-ttu-id="77e37-182">Odczytaj ustawienia na poziomie katalogu hello</span><span class="sxs-lookup"><span data-stu-id="77e37-182">Read settings at hello directory level</span></span>
<span data-ttu-id="77e37-183">Następujące kroki odczytać ustawień na poziomie katalogu, które mają zastosowanie grupy Office tooall w katalogu hello.</span><span class="sxs-lookup"><span data-stu-id="77e37-183">These steps read settings at directory level, which apply tooall Office groups in hello directory.</span></span>

1. <span data-ttu-id="77e37-184">Przeczytaj wszystkich istniejących ustawień katalogu:</span><span class="sxs-lookup"><span data-stu-id="77e37-184">Read all existing directory settings:</span></span>
  ```
  Get-AzureADDirectorySetting -All $True
  ```
  <span data-ttu-id="77e37-185">To polecenie cmdlet zwraca listę wszystkich ustawień katalogu:</span><span class="sxs-lookup"><span data-stu-id="77e37-185">This cmdlet returns a list of all directory settings:</span></span>
  ```
  Id                                   DisplayName   TemplateId                           Values
  --                                   -----------   ----------                           ------
  c391b57d-5783-4c53-9236-cefb5c6ef323 Group.Unified 62375ab9-6b52-47ed-826b-58e47e0e304b {class SettingValue {...
  ```

2. <span data-ttu-id="77e37-186">Odczytywanie wszystkich ustawień dla określonej grupy:</span><span class="sxs-lookup"><span data-stu-id="77e37-186">Read all settings for a specific group:</span></span>
  ```
  Get-AzureADObjectSetting -TargetObjectId ab6a3887-776a-4db7-9da4-ea2b0d63c504 -TargetType Groups
  ```

3. <span data-ttu-id="77e37-187">Przeczytaj wszystkie wartości obiektu ustawienia określonego katalogu, za pomocą ustawienia identyfikatora GUID ustawień katalogu:</span><span class="sxs-lookup"><span data-stu-id="77e37-187">Read all directory settings values of a specific directory settings object, using Settings Id GUID:</span></span>
  ```
  (Get-AzureADDirectorySetting -Id c391b57d-5783-4c53-9236-cefb5c6ef323).values
  ```
  <span data-ttu-id="77e37-188">To polecenie cmdlet zwraca hello nazwy i wartości w tym obiekcie ustawienia dla tej określonej grupie:</span><span class="sxs-lookup"><span data-stu-id="77e37-188">This cmdlet returns hello names and values in this settings object for this specific group:</span></span>
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

## <a name="update-settings-for-a-specific-group"></a><span data-ttu-id="77e37-189">Ustawienia aktualizacji dla określonej grupy</span><span class="sxs-lookup"><span data-stu-id="77e37-189">Update settings for a specific group</span></span>

1. <span data-ttu-id="77e37-190">Wyszukaj hello ustawienia szablonu o nazwie "Groups.Unified.Guest"</span><span class="sxs-lookup"><span data-stu-id="77e37-190">Search for hello settings template named "Groups.Unified.Guest"</span></span>
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
2. <span data-ttu-id="77e37-191">Pobierz obiekt szablonu hello hello Groups.Unified.Guest szablonu:</span><span class="sxs-lookup"><span data-stu-id="77e37-191">Retrieve hello template object for hello Groups.Unified.Guest template:</span></span>
  ```
  $Template = Get-AzureADDirectorySettingTemplate -Id 08d542b9-071f-4e16-94b0-74abb372e3d9
  ```
3. <span data-ttu-id="77e37-192">Utwórz nowy obiekt ustawień z szablonu hello:</span><span class="sxs-lookup"><span data-stu-id="77e37-192">Create a new settings object from hello template:</span></span>
  ```
  $Setting = $Template.CreateDirectorySetting()
  ```

4. <span data-ttu-id="77e37-193">Ustaw wartość toohello wymagane ustawienia hello:</span><span class="sxs-lookup"><span data-stu-id="77e37-193">Set hello setting toohello required value:</span></span>
  ```
  $Setting["AllowToAddGuests"]=$False
  ```
5. <span data-ttu-id="77e37-194">Tworzenie nowego ustawienia hello hello wymaganej grupy w katalogu hello:</span><span class="sxs-lookup"><span data-stu-id="77e37-194">Create hello new setting for hello required group in hello directory:</span></span>
  ```
  New-AzureADObjectSetting -TargetType Groups -TargetObjectId ab6a3887-776a-4db7-9da4-ea2b0d63c504 -DirectorySetting $Setting
  
  Id                                   DisplayName TemplateId                           Values
  --                                   ----------- ----------                           ------
  25651479-a26e-4181-afce-ce24111b2cb5             08d542b9-071f-4e16-94b0-74abb372e3d9 {class SettingValue {...
  ```

## <a name="update-settings-at-hello-directory-level"></a><span data-ttu-id="77e37-195">Zaktualizuj ustawienia na poziomie katalogu hello</span><span class="sxs-lookup"><span data-stu-id="77e37-195">Update settings at hello directory level</span></span>

<span data-ttu-id="77e37-196">Te kroki zaktualizować ustawienia na poziomie katalogu, które tooall Unified grup w katalogu hello.</span><span class="sxs-lookup"><span data-stu-id="77e37-196">These steps update settings at directory level, which apply tooall Unified groups in hello directory.</span></span> <span data-ttu-id="77e37-197">Tych przykładów założono, że istnieje już obiekt ustawień w katalogu.</span><span class="sxs-lookup"><span data-stu-id="77e37-197">These examples assume there is already a Settings object in your directory.</span></span>

1. <span data-ttu-id="77e37-198">Znajdź istniejący obiekt ustawień hello:</span><span class="sxs-lookup"><span data-stu-id="77e37-198">Find hello existing Settings object:</span></span>
  ```
  Get-AzureADDirectorySetting | Where-object -Property Displayname -Value "Group.Unified" -EQ
  
  Id                                   DisplayName   TemplateId                           Values
  --                                   -----------   ----------                           ------
  c391b57d-5783-4c53-9236-cefb5c6ef323 Group.Unified 62375ab9-6b52-47ed-826b-58e47e0e304b {class SettingValue {...
  
  $setting = Get-AzureADDirectorySetting –Id c391b57d-5783-4c53-9236-cefb5c6ef323
  ```
2. <span data-ttu-id="77e37-199">Zaktualizuj wartość hello:</span><span class="sxs-lookup"><span data-stu-id="77e37-199">Update hello value:</span></span>
  
  ```
  $Setting["AllowToAddGuests"] = "false"
  ```
3. <span data-ttu-id="77e37-200">Zaktualizuj ustawienie hello:</span><span class="sxs-lookup"><span data-stu-id="77e37-200">Update hello setting:</span></span>
  
  ```
  Set-AzureADDirectorySetting -Id c391b57d-5783-4c53-9236-cefb5c6ef323 -DirectorySetting $Setting
  ```

## <a name="remove-settings-at-hello-directory-level"></a><span data-ttu-id="77e37-201">Usuń ustawienia na poziomie katalogu hello</span><span class="sxs-lookup"><span data-stu-id="77e37-201">Remove settings at hello directory level</span></span>
<span data-ttu-id="77e37-202">Ten krok powoduje usunięcie ustawień na poziomie katalogu, które mają zastosowanie grupy Office tooall w katalogu hello.</span><span class="sxs-lookup"><span data-stu-id="77e37-202">This step removes settings at directory level, which apply tooall Office groups in hello directory.</span></span>
  ```
  Remove-AzureADDirectorySetting –Id c391b57d-5783-4c53-9236-cefb5c6ef323c
  ```

## <a name="cmdlet-syntax-reference"></a><span data-ttu-id="77e37-203">Odwołania do składni polecenia cmdlet</span><span class="sxs-lookup"><span data-stu-id="77e37-203">Cmdlet syntax reference</span></span>
<span data-ttu-id="77e37-204">Więcej dokumentacji programu PowerShell usługi Azure Active Directory można znaleźć [polecenia cmdlet usługi Azure Active Directory](/powershell/azure/install-adv2?view=azureadps-2.0).</span><span class="sxs-lookup"><span data-stu-id="77e37-204">You can find more Azure Active Directory PowerShell documentation at [Azure Active Directory Cmdlets](/powershell/azure/install-adv2?view=azureadps-2.0).</span></span>

## <a name="additional-reading"></a><span data-ttu-id="77e37-205">Dodatkowe materiały</span><span class="sxs-lookup"><span data-stu-id="77e37-205">Additional reading</span></span>

* [<span data-ttu-id="77e37-206">Zarządzanie tooresources dostępu za pomocą grup usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="77e37-206">Managing access tooresources with Azure Active Directory groups</span></span>](active-directory-manage-groups.md)
* [<span data-ttu-id="77e37-207">Integrowanie tożsamości lokalnych z usługą Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="77e37-207">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
