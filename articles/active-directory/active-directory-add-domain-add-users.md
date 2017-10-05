---
title: "Przypisywanie użytkowników do domeny niestandardowej w usłudze Azure Active Directory | Dokumentacja firmy Microsoft"
description: "Sposób wypełniania domeny niestandardowej w usłudze Azure Active Directory z kontami użytkowników."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 717b5a7c-7bc3-4ab1-98b5-4740b53338fe
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: curtand
ms.custom: oldportal;it-pro;
robots: NOINDEX
ms.openlocfilehash: 39cb54a6637088c35c6aef864a804c24803f48ba
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="assign-users-to-a-custom-domain"></a>Przypisywanie użytkowników do domeny niestandardowej
Po dodaniu domeny niestandardowej do usługi Azure Active Directory, należy dodać konta użytkowników dla tej domeny, dzięki czemu będzie można ich uwierzytelnianie.

> [!IMPORTANT]
> Firma Microsoft zaleca zarządzanie usługą Azure AD przy użyciu [centrum administracyjnego usługi Azure AD](https://aad.portal.azure.com) w witrynie Azure Portal zamiast korzystania z klasycznej witryny Azure Portal przywołanej w niniejszym artykule. Jak zarządzać nazwy domeny w Centrum administracyjnym usługi Azure AD, zobacz [Zarządzanie niestandardowych nazw domen w usłudze Azure Active Directory](active-directory-domains-manage-azure-portal.md).

## <a name="users-synced-from-a-on-premises-directory"></a>Użytkownicy synchronizowane z katalogu lokalnego
Jeśli już ustawiono połączenia między lokalnymi usługi Active Directory i Azure Active Directory, synchronizacji można wypełnić kont. Aby uzyskać więcej informacji na temat sposobu synchronizacji usługi Azure Active Directory z lokalnej usługi Active Directory, zobacz [integrowanie tożsamości lokalnych z usługą Azure Active Directory](active-directory-aadconnect.md).

## <a name="users-added-and-managed-in-the-cloud"></a>Użytkownicy dodawane i zarządzane w chmurze
Aby zmienić domenę do istniejącego konta użytkownika:

1. Otwórz klasyczny portal Azure przy użyciu konta, które jest administratorem globalnym lub administratorem użytkownika.
2. Otwórz katalog.
3. Wybierz kartę **Użytkownicy**.
4. Wybierz użytkownika z listy.
5. Zmiana domeny użytkownika, a następnie wybierz **zapisać**.

Można to także zrobić przy użyciu [Microsoft PowerShell](https://msdn.microsoft.com/library/azure/e1ef403f-3347-4409-8f46-d72dafa116e0#BKMK_ManageDomains) lub [interfejsu API programu Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/domains-operations).

## <a name="select-a-custom-domain-when-creating-a-new-user"></a>Wybierz domenę niestandardową, podczas tworzenia nowego użytkownika
1. Otwórz klasyczny portal Azure przy użyciu konta, które jest administratorem globalnym lub administratorem użytkownika.
2. Otwórz katalog.
3. Wybierz kartę **Użytkownicy**.
4. Na pasku poleceń Wybierz **Dodaj**.
5. Po dodaniu nazwy użytkownika, wybierz domenę niestandardową z listy domen.
6. Wybierz pozycję **Zapisz**.

## <a name="next-steps"></a>Następne kroki
* [Aby uprościć proces logowania użytkowników przy użyciu niestandardowych nazw domen](active-directory-add-domain.md)
* [Zarządzanie niestandardowymi nazwami domen](active-directory-add-manage-domain-names.md)
* [Zapoznanie z koncepcjami związanymi z zarządzaniem domenami w usłudze Azure AD](active-directory-add-domain-concepts.md)

