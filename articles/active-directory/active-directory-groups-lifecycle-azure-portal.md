---
title: "aaaPreview usługi Office 365 grupuje ważności w usłudze Azure Active Directory | Dokumentacja firmy Microsoft"
description: "Jak tooset się wygaśnięcia dla usługi Office 365 grup w usłudze Azure Active Directory (wersja zapoznawcza)"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: curtand
ms.reviewer: kairaz.contractor
ms.custom: it-pro
ms.openlocfilehash: a8c99961cff3aad3f4d8b0cc1b2eb8e8a4c9ba95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-office-365-groups-expiration-preview"></a>Skonfiguruj wygaśnięcia grup usługi Office 365 (wersja zapoznawcza)

Możesz teraz zarządzać hello cyklem życia grup usługi Office 365, ustawiając wygaśnięcia w wybranych grupach usługi Office 365. Po ustawieniu tej wygaśnięcia właścicieli tych grup są zadawane toorenew ich grup, jeśli nadal potrzebujesz hello grup. Wszystkie grupy usługi Office 365, która nie zostanie odnowiony zostaną usunięte. W ciągu 30 dni można przywrócić żadnej grupy usługi Office 365, który został usunięty przez właścicieli grupy hello lub hello administratora.  


> [!NOTE]
> Można ustawić wygaśnięcie tylko grup usługi Office 365.
>
> Ustawianie ważności dla grup usługi Office 365 wymaga przypisania licencji usługi Azure AD Premium do
>   - Witaj, administrator konfiguruje ustawienia wygaśnięcia hello hello dzierżawcy
>   - Wszyscy członkowie grupy hello wybrana dla tego ustawienia

## <a name="set-office-365-groups-expiration"></a>Ustawienia okresu ważności grup usługi Office 365

1. Otwórz hello [Centrum administracyjnego usługi Azure AD](https://aad.portal.azure.com) przy użyciu konta, które jest administratorem globalnym w dzierżawie usługi Azure AD.

2. Otwórz usługę Azure AD, wybierz **użytkowników i grup**.

3. Wybierz **ustawienia grupy** , a następnie wybierz **wygaśnięcia** ustawienia wygaśnięcia hello tooopen.
  
  ![Blok wygaśnięcia](./media/active-directory-groups-lifecycle-azure-portal/expiration-settings.png)

4. Na powitania **wygaśnięcia** bloku, można wykonywać następujące czynności:

  * Ustaw okres istnienia grupy hello w dniach. Można wybrać jedną z hello ustawienia wartości lub wartości niestandardowych (powinien być 31 dni lub więcej). 
  * Określ adres e-mail, w którym mają być wysyłane powiadomienia hello odnowienia i wygaśnięcia po grupie nie ma ono właściciela. 
  * Wybierz grupy, które usługi Office 365 wygaśnie. Można włączyć wygaśnięcia dla **wszystkie** grup usługi Office 365, możesz wybrać spośród grup hello usługi Office 365 lub wybrać **Brak** wyłączyć wygaśnięcia dla wszystkich grup.
  * Zapisz ustawienia, gdy wszystko będzie gotowe, wybierając **zapisać**.

Aby uzyskać instrukcje dotyczące sposobu toodownload i zainstaluj hello wygaśnięcia tooconfigure modułu PowerShell firmy Microsoft dla grup usługi Office 365 za pomocą programu PowerShell, zobacz [Azure V2 PowerShell moduł usługi Active Directory - publicznej wersji zapoznawczej 2.0.0.137](https://www.powershellgallery.com/packages/AzureADPreview/2.0.0.137).

Powiadomienia e-mail, taką jak są wysyłane właścicieli grupy usługi Office 365 toohello 30 dni, 15 dni i 1 dzień przed tooexpiration hello grupy.

![Powiadomienia e-mail o wygaśnięciu](./media/active-directory-groups-lifecycle-azure-portal/expiration-notification.png)

Właściciel grupy Hello można wybrać **grupy odnawiania** toorenew hello grupy usługi Office 365 lub wybrać **Przejdź toogroup** członków hello toosee i inne szczegółowe informacje o hello grupy.

Po wygaśnięciu grupy jeden dzień po dacie wygaśnięcia hello jest usunąć hello grupy. Powiadomienie e-mail, taką jak są wysyłane właścicieli grupy usługi Office 365 toohello informująca o wygaśnięciu hello i kolejne usunięcie ich z grupy usługi Office 365.

![Powiadomienie e-mail usunięcia grupy](./media/active-directory-groups-lifecycle-azure-portal/deletion-notification.png)

Witaj grupy można przywrócić, wybierając **grupy przywracania** lub za pomocą poleceń cmdlet programu PowerShell, zgodnie z opisem w [przywracanie usuniętych usługi Office 365 grupy w usłudze Azure Active Directory] (https://docs.microsoft.com/azure/active-directory/ Active-Directory-groups-Restore-Azure-Portal).
    
Jeśli grupa hello, które są przywracane zawiera dokumentów, witryn programu SharePoint lub inne obiekty trwałe, może upłynąć too24 godziny toofully przywracania hello grupy i jego zawartość.

> [!NOTE]
> * Podczas wdrażania ustawień wygasania hello, może być niektórych grup, które są starsze niż hello okna wygaśnięcia. Te grupy nie są można natychmiast usunąć, ale są too30 dni do wygaśnięcia. Hello pierwszy odnawiania powiadomienia e-mail jest wysyłane w ciągu dnia. Na przykład, A grupa została utworzona 400 dni temu i hello wygaśnięcia interwał jest ustawiany too180 dni. Podczas stosowania ustawień wygasania, A grupy ma 30 dni przed usunięciem, chyba że właściciela hello odnawia go.
> * Gdy dynamiczna grupa jest usuwane i przywrócić, jest to traktowane jako nową grupę i ponownie wypełnione zgodnie z reguły toohello. Ten proces może potrwać too24 godzin.

## <a name="next-steps"></a>Następne kroki
Te artykuły zawierają dodatkowe informacje o grup usługi Azure AD.

* [Zobacz istniejących grup](active-directory-groups-view-azure-portal.md)
* [Zarządzanie ustawieniami grupy](active-directory-groups-settings-azure-portal.md)
* [Elementy członkowskie grupy zarządzania](active-directory-groups-members-azure-portal.md)
* [Zarządzanie członkostwami grup](active-directory-groups-membership-azure-portal.md)
* [Dynamiczne reguły dla użytkowników w grupie zarządzania](active-directory-groups-dynamic-membership-azure-portal.md)
