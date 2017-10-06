---
title: "aaaManaging niestandardowych nazw domen w usłudze Azure Active Directory | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 4719524c4e972f6c981db39f016729da13b37670
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="managing-custom-domain-names-in-your-azure-active-directory"></a>Zarządzanie niestandardowych nazw domen w usłudze Azure Active Directory
Nazwa domeny jest ważnym elementem hello identyfikator wiele zasobów katalogu: wchodzi w skład użytkownika nazwy lub adresu e-mail dla użytkownika, część adresu hello w grupie i może być częścią aplikacji hello identyfikator URI aplikacji. Zasób w usłudze Azure Active Directory (Azure AD) może zawierać nazwy domeny, który już jest weryfikowany jako należących do katalogu hello zawierającej hello zasobów. Tylko administrator globalny może wykonywać zadania zarządzania domeny w usłudze Azure AD.

## <a name="set-hello-primary-domain-name-for-your-azure-ad-directory"></a>Nazwa domeny głównej hello zestawu dla katalogu usługi Azure AD
Podczas tworzenia katalogu hello początkową nazwę domeny, takie jak "contoso.onmicrosoft.com", jest również hello podstawowej nazwy domeny. domena podstawowa Hello jest hello domyślna nazwa domeny dla nowego użytkownika, podczas tworzenia nowego użytkownika. Nazwa domeny głównej ustawienia usprawnia proces hello administratora toocreate nowych użytkowników w portalu hello. Nazwa domeny głównej hello toochange:

1. Zaloguj się toohello [portalu Azure](https://portal.azure.com) przy użyciu konta, które jest administratorem globalnym katalogu hello.
2. Wybierz **więcej usług**, wprowadź **usługi Azure Active Directory** w hello pola tekstowego, a następnie wybierz **Enter**.
   
   ![Otwieranie Zarządzanie użytkownikami](./media/active-directory-domains-add-azure-portal/user-management.png)
3. Na powitania ***nazwa katalogu*** bloku, wybierz opcję **nazwy domen**.
4. Na powitania  ***nazwa katalogu* -nazwy domen** bloku, nazwa domeny wybierz hello chcesz toomake hello podstawowej nazwy domeny.
5. Na powitania ***nazwy domeny*** bloku (to znaczy hello bloku, który otwiera mającą nazwę nowej domeny w tytule hello), wybierz hello **Ustaw jako podstawowy** polecenia. Potwierdź wybór po wyświetleniu monitu.
   
   ![Wprowadź nazwę domeny głównej](./media/active-directory-domains-manage-azure-portal/make-primary.png)

Można zmienić nazwę domeny głównej hello toobe Twojego katalogu zweryfikowanej domeny niestandardowej, która nie jest zintegrowany. Zmiana hello domeny głównej dla katalogu nie zmieni hello nazwy żadnych istniejących użytkowników.

## <a name="add-custom-domain-names-tooyour-azure-ad"></a>Dodaj tooyour nazwy domeny niestandardowej usługi Azure AD
Możesz dodać too900 domeny niestandardowej nazwy tooeach usługi Azure AD katalogu. Witaj procesu zbyt[Dodawanie dodatkowej niestandardowej nazwy domeny](add-custom-domain.md) jest hello takie same dla hello pierwszej niestandardowej nazwy domeny.

## <a name="add-subdomains-of-a-custom-domain"></a>Dodawanie poddomen domeny niestandardowej
Jeśli chcesz tooadd nazwy domen trzeciego poziomu, takie jak katalog tooyour "europe.contoso.com", należy najpierw dodać i sprawdzić, hello domeny drugiego poziomu, np. contoso.com. poddomeny Hello zostanie automatycznie zweryfikowane przez usługę Azure AD. toosee, który hello poddomeny dodanego została zweryfikowana, Odśwież hello strony w przeglądarce hello, który zawiera listę domen hello.

## <a name="what-toodo-if-you-change-hello-dns-registrar-for-your-custom-domain-name"></a>Jakie toodo hello DNS rejestratora po zmianie nazwy domeny niestandardowej
Jeśli zmienisz hello DNS rejestratora dla niestandardowej nazwy domeny, możesz kontynuować toouse nazwy domeny niestandardowej z usługą Azure AD, sam bez przerw i dodatkowe zadania konfiguracyjne. Jeśli korzystasz z niestandardowej nazwy domeny z usługą Office 365, Intune lub innych usług, które opierają się na niestandardowych nazw domen w usłudze Azure AD, zapoznaj się z toohello dokumentacją dla tych usług.

## <a name="delete-a-custom-domain-name"></a>Usuń niestandardową nazwę domeny
Czy organizacja już używa tej nazwy domeny, czy należy toouse tej nazwy domeny z inną usługą Azure AD, możesz usunąć niestandardową nazwę domeny z usługi Azure AD.

toodelete niestandardowej nazwy domeny, należy najpierw upewnić, że żaden zasób w katalogu zależeć hello nazwy domeny. Nie można usunąć nazwy domeny z katalogu, jeśli:

* Każdy użytkownik ma nazwę użytkownika, adres e-mail lub adres serwera proxy, który obejmuje nazwę domeny hello.
* Każda grupa ma adres e-mail lub adres serwera proxy, który obejmuje nazwę domeny hello.
* Aplikacje w usługi Azure AD ma identyfikator URI, który obejmuje nazwę domeny hello aplikacji.

Należy zmienić lub usunąć tych zasobów w katalogu usługi Azure AD, przed usunięciem hello niestandardowej nazwy domeny.

## <a name="use-powershell-or-graph-api-toomanage-domain-names"></a>Użyj nazwy domeny toomanage programu PowerShell lub interfejsu API programu Graph
Większość zadań zarządzania dla nazwy domeny w usłudze Azure Active Directory można również przeprowadzić przy użyciu PowerShell firmy Microsoft lub programowo przy użyciu interfejsu API Azure AD Graph.

* [Przy użyciu programu PowerShell toomanage domen w usłudze Azure AD](https://msdn.microsoft.com/library/azure/e1ef403f-3347-4409-8f46-d72dafa116e0#BKMK_ManageDomains)
* [Przy użyciu nazwy domeny toomanage interfejsu API programu Graph w usłudze Azure AD](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/domains-operations)

## <a name="next-steps"></a>Następne kroki
* [Dodawanie niestandardowych nazw domen](add-custom-domain.md)

