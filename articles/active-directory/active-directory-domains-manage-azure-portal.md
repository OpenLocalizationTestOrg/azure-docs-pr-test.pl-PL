---
title: "Zarządzanie niestandardowych nazw domen w usłudze Azure Active Directory | Dokumentacja firmy Microsoft"
description: "Pojęcia dotyczące zarządzania i kwestie dotyczące zarządzania nazwę domeny w usłudze Azure Active Directory"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 5063cd0a-dba2-4ba9-aa65-b8117490d73a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: curtand;jeffsta
ms.openlocfilehash: 402c1be07b8ee885ee5341128fb3f419611b924d
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="managing-custom-domain-names-in-your-azure-active-directory"></a>Zarządzanie niestandardowych nazw domen w usłudze Azure Active Directory
Nazwa domeny jest ważnym elementem identyfikator wiele zasobów katalogu: wchodzi w skład użytkownika nazwy lub adresu e-mail dla użytkownika, część adresu w grupie i może być częścią aplikacji identyfikator URI aplikacji. Zasób w usłudze Azure Active Directory (Azure AD) może zawierać nazwy domeny, który już jest weryfikowany jako należących do katalogu, który zawiera zasób. Tylko administrator globalny może wykonywać zadania zarządzania domeny w usłudze Azure AD.

## <a name="set-the-primary-domain-name-for-your-azure-ad-directory"></a>Ustaw nazwę domeny głównej dla katalogu usługi Azure AD
Podczas tworzenia katalogu z początkowej nazwy domeny, takie jak "contoso.onmicrosoft.com", jest również nazwa domeny głównej. Podczas tworzenia nowego użytkownika, domena podstawowa jest domyślna nazwa domeny dla nowego użytkownika. Nazwa domeny głównej ustawienia usprawnia proces dla administratora utworzyć nowych użytkowników w portalu. Aby zmienić nazwę domeny głównej:

1. Zaloguj się do [portalu Azure](https://portal.azure.com) przy użyciu konta, które jest administratorem globalnym katalogu.
2. Wybierz **więcej usług**, wprowadź **usługi Azure Active Directory** w polu tekstowym, a następnie wybierz **Enter**.
   
   ![Otwieranie Zarządzanie użytkownikami](./media/active-directory-domains-add-azure-portal/user-management.png)
3. Na ***nazwa katalogu*** bloku, wybierz opcję **nazwy domen**.
4. Na  ***nazwa katalogu* -nazwy domen** bloku, wybierz nazwę domeny, które chcesz wprowadzić nazwę domeny głównej.
5. Na ***nazwy domeny*** bloku (to znaczy bloku otwartym mającą nazwę nowej domeny w tytule), wybierz **Ustaw jako podstawowy** polecenia. Potwierdź wybór po wyświetleniu monitu.
   
   ![Wprowadź nazwę domeny głównej](./media/active-directory-domains-manage-azure-portal/make-primary.png)

Można zmienić nazwę domeny głównej dla katalogu jako zweryfikowanej domeny niestandardowej, która nie jest zintegrowany. Zmiana domeny podstawowej dla katalogu nie spowoduje zmiany nazwy użytkownika dla wszystkich istniejących użytkowników.

## <a name="add-custom-domain-names-to-your-azure-ad"></a>Dodawanie niestandardowych nazw domen do usługi Azure AD
Maksymalnie 900 nazw domen niestandardowych można dodać do każdego katalogu usługi Azure AD. Proces [Dodawanie dodatkowej niestandardowej nazwy domeny](add-custom-domain.md) jest taki sam dla pierwszej nazwy domeny niestandardowej.

## <a name="add-subdomains-of-a-custom-domain"></a>Dodawanie poddomen domeny niestandardowej
Jeśli chcesz dodać nazwy domen trzeciego poziomu, takie jak "europe.contoso.com" do katalogu, należy najpierw dodać i zweryfikować domeny drugiego poziomu, np. contoso.com. Poddomeny zostanie automatycznie zweryfikowane przez usługę Azure AD. Aby wyświetlić zweryfikowaniu poddomeny, który właśnie został dodany, Odśwież stronę w przeglądarce, która zawiera listę domen.

## <a name="what-to-do-if-you-change-the-dns-registrar-for-your-custom-domain-name"></a>Co robić w przypadku zmiany nazwy domeny niestandardowej rejestratora DNS.
Jeśli zmienisz rejestratora DNS dla nazwy domeny niestandardowej, można korzystać z nazwy domeny niestandardowej z usługą Azure AD, sam bez przerw i dodatkowe zadania konfiguracyjne. Jeśli korzystasz z niestandardowej nazwy domeny z usługą Office 365, Intune lub innych usług, które opierają się na niestandardowych nazw domen w usłudze Azure AD, można znaleźć w dokumentacji tych usług.

## <a name="delete-a-custom-domain-name"></a>Usuń niestandardową nazwę domeny
Czy organizacja już używa tej nazwy domeny, czy należy użyć tej nazwy domeny z inną usługą Azure AD, możesz usunąć niestandardową nazwę domeny z usługi Azure AD.

Aby usunąć niestandardową nazwę domeny, musi najpierw upewnić, że żaden zasób w katalogu zależą od nazwy domeny. Nie można usunąć nazwy domeny z katalogu, jeśli:

* Każdy użytkownik ma nazwę użytkownika, adres e-mail lub adres serwera proxy, która zawiera nazwę domeny.
* Każda grupa ma adres e-mail lub adres serwera proxy, która zawiera nazwę domeny.
* Aplikacje w usługi Azure AD ma identyfikator URI, który obejmuje nazwę domeny aplikacji.

Należy zmienić lub usunąć tych zasobów w katalogu usługi Azure AD, przed usunięciem nazwy domeny niestandardowej.

## <a name="use-powershell-or-graph-api-to-manage-domain-names"></a>Użyj programu PowerShell lub interfejsu API programu Graph, zarządzanie nazwami domen
Większość zadań zarządzania dla nazwy domeny w usłudze Azure Active Directory można również przeprowadzić przy użyciu PowerShell firmy Microsoft lub programowo przy użyciu interfejsu API Azure AD Graph.

* [Zarządzanie nazwami domen w usłudze Azure AD przy użyciu programu PowerShell](https://msdn.microsoft.com/library/azure/e1ef403f-3347-4409-8f46-d72dafa116e0#BKMK_ManageDomains)
* [Zarządzanie nazwami domen w usłudze Azure AD przy użyciu interfejsu API programu Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/domains-operations)

## <a name="next-steps"></a>Następne kroki
* [Dodawanie niestandardowych nazw domen](add-custom-domain.md)

