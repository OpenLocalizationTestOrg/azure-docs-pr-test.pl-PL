---
title: "grupy aaaRestore usunięto usługi Office 365 w usłudze Azure Active Directory | Dokumentacja firmy Microsoft"
description: "Jak toorestore usuniętej grupie, wyświetlanie dostępnych grup i permamnently usunąć grupę w usłudze Azure Active Directory"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: cc5f232a-1e77-45c2-b28b-1fcb4621725c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: curtand
ms.openlocfilehash: 4e6650d64aa19f0c909f1c511f48681de8032f63
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="restore-a-deleted-office-365-group-in-azure-active-directory"></a>Przywracanie usuniętej grupy usługi Office 365 w usłudze Azure Active Directory

Podczas usuwania grupy usługi Office 365 w hello Azure Active Directory (Azure AD), hello usunięta grupa jest zachowane, ale nie są widoczne przez 30 dni od daty usunięcia hello. Jest tak, aby grupa hello i jego zawartość można przywrócić w razie potrzeby. Ta funkcja jest ograniczone wyłącznie tooOffice 365 grup w usłudze Azure AD. Nie jest dostępna dla grup zabezpieczeń i grup dystrybucyjnych.

> [!NOTE] 
> Nie używaj `Remove-MsolGroup` ponieważ Przeczyszcza grupy hello trwałe. Zawsze używaj `Remove-AzureADMSGroup` grupy toodelete usługi Office 365. 

wymagane uprawnienia Hello toorestore grupa może zawierać żadnego z następujących hello:

Rola  | Uprawnienia 
--------- | ---------
Administrator firmy, pomocy partnera Tier2 i Administratorzy usługi InTune | Można przywrócić wszystkie usunięte grupy usługi Office 365 
Administrator konta użytkownika i Tier1 partnera pomocy technicznej | Można przywrócić wszystkie usuniętej grupy usługi Office 365, z wyjątkiem tych toohello przypisanej roli Administrator firmy 
Użytkownik | Można przywrócić wszystkie usuniętej grupy usługi Office 365, które są jego własnością 


## <a name="view-hello-deleted-office-365-groups-that-are-available-toorestore"></a>Widok hello usunięte grup usługi Office 365, które są dostępne toorestore
Hello następującego polecenia cmdlet mogą być używane tooview hello usunięte grup tooverify, który hello jedną lub te, które interesują Cię nie jeszcze zostały trwale usunięte. Te polecenia cmdlet są częścią hello [modułu Azure AD PowerShell](https://www.powershellgallery.com/packages/AzureAD/). Więcej informacji na temat tego modułu można znaleźć w hello [Azure Active Directory programu PowerShell w wersji 2](/powershell/azure/install-adv2?view=azureadps-2.0) artykułu.

1.  Uruchom następujące polecenia cmdlet toodisplay usunięte grup usługi Office 365 w dzierżawie, które są nadal dostępne toorestore hello.
  ```
  Get-AzureADMSDeletedGroup
  ```

2.  Jeśli znasz objectID hello określonej grupy (i pobrać go ze strony hello polecenie cmdlet w kroku 1), uruchom hello tooverify polecenia cmdlet, które hello określonej grupy usunięte po nie jeszcze trwale usunięto.
  ```
  Get-AzureADMSDeletedGroup –Id <objectId>
  ```



## <a name="how-toorestore-your-deleted-office-365-group"></a>Jak toorestore Twojego usuniętej grupy usługi Office 365
Po upewnieniu się, że grupa ta hello jest nadal dostępny toorestore hello przywracania usunął grupę z jednym hello następujące kroki. Jeśli grupa hello zawiera dokumenty, SP witryn lub inne obiekty trwałe, grupy i jego zawartość może potrwać nawet too24 godziny toofully przywracania.

1.  Uruchom hello następujące polecenia cmdlet toorestore hello grupy i jego zawartość.
  
  ```
  Restore-AzureADMSDeletedDirectoryObject –Id <objectId>
  ``` 

Alternatywnie hello następującego polecenia cmdlet można uruchomić toopermanently Usuń hello usunąć grupę.
  ```
  Remove-AzureADMSDeletedDirectoryObject –Id <objectId>
  ```

## <a name="how-do-you-know-this-worked"></a>Skąd wiadomo, to pracy?
tooverify zostały pomyślnie przywrócił grupy usługi Office 365, uruchom hello `Get-AzureADGroup –ObjectId <objectId>` polecenia cmdlet toodisplay informacji o grupie hello. Po przywróceniu hello jest ukończone żądania:
- grupy Hello pojawią się w pasku nawigacyjnym po lewej stronie powitania na serwerze Exchange
- Planowanie Hello hello grupy będą wyświetlane w planowania
- Witryny programu Sharepoint i wszystkie ich zawartość będzie dostępna
- Hello grupy jest możliwy za pomocą dowolnego hello punktów końcowych z programu Exchange i innych obciążeń usługi Office 365, które obsługują grup usługi Office 365


## <a name="next-steps"></a>Następne kroki
Te artykuły zawierają dodatkowe informacje o grupach usługi Azure Active Directory.

* [Zobacz istniejących grup](active-directory-groups-view-azure-portal.md)
* [Zarządzanie ustawieniami grupy](active-directory-groups-settings-azure-portal.md)
* [Elementy członkowskie grupy zarządzania](active-directory-groups-members-azure-portal.md)
* [Zarządzanie członkostwami grup](active-directory-groups-membership-azure-portal.md)
* [Dynamiczne reguły dla użytkowników w grupie zarządzania](active-directory-groups-dynamic-membership-azure-portal.md)
