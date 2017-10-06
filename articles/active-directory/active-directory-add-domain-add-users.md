---
title: "Domena niestandardowa tooa użytkowników aaaAssign w usłudze Azure Active Directory | Dokumentacja firmy Microsoft"
description: "Jak toopopulate domeny niestandardowej w usłudze Azure Active Directory z kontami użytkowników."
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
ms.openlocfilehash: 23c338a361a90fddf42d4df90db94c9774305886
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="assign-users-tooa-custom-domain"></a>Przypisywanie użytkowników tooa niestandardową domenę
Po dodaniu tooAzure Twojego niestandardową domenę usługi Active Directory, należy dodać hello kont użytkowników dla tej domeny, dzięki czemu będzie można ich uwierzytelnianie.

> [!IMPORTANT]
> Firma Microsoft zaleca się, że zarządzania usługi Azure AD przy użyciu hello [Centrum administracyjnego usługi Azure AD](https://aad.portal.azure.com) w hello portalu Azure zamiast hello klasycznego portalu Azure, do którego odwołuje się w tym artykule. Aby uzyskać jak toomanage Twojego nazw domen w Centrum administracyjnym hello Azure AD, zobacz [Zarządzanie niestandardowych nazw domen w usłudze Azure Active Directory](active-directory-domains-manage-azure-portal.md).

## <a name="users-synced-from-a-on-premises-directory"></a>Użytkownicy synchronizowane z katalogu lokalnego
Jeśli już ustawiono połączenia między lokalnymi usługi Active Directory i Azure Active Directory, synchronizacji można wypełnić hello kont. Aby uzyskać więcej informacji na temat toosynchronize usługi Azure Active Directory z lokalnej usługi Active Directory, zobacz temat [integrowanie tożsamości lokalnych z usługą Azure Active Directory](active-directory-aadconnect.md).

## <a name="users-added-and-managed-in-hello-cloud"></a>Użytkownicy dodawane i zarządzane w chmurze hello
toochange hello domeny do istniejącego konta użytkownika:

1. Otwórz hello klasycznego portalu Azure przy użyciu konta, które jest administratorem globalnym lub administratorem użytkownika.
2. Otwórz katalog.
3. Wybierz hello **użytkowników** kartę.
4. Wybierz hello użytkownika z listy hello.
5. Zmiana domeny hello hello użytkownika, a następnie wybierz **zapisać**.

Można to także zrobić przy użyciu [Microsoft PowerShell](https://msdn.microsoft.com/library/azure/e1ef403f-3347-4409-8f46-d72dafa116e0#BKMK_ManageDomains) lub hello [interfejsu API programu Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/domains-operations).

## <a name="select-a-custom-domain-when-creating-a-new-user"></a>Wybierz domenę niestandardową, podczas tworzenia nowego użytkownika
1. Otwórz hello klasycznego portalu Azure przy użyciu konta, które jest administratorem globalnym lub administratorem użytkownika.
2. Otwórz katalog.
3. Wybierz hello **użytkowników** kartę.
4. Na pasku poleceń hello, wybierz **Dodaj**.
5. Po dodaniu hello nazwy użytkownika z listy domeny hello należy wybrać hello domeny niestandardowej.
6. Wybierz pozycję **Zapisz**.

## <a name="next-steps"></a>Następne kroki
* [Przy użyciu domeny niestandardowej nazwy toosimplify hello logowania użytkowników](active-directory-add-domain.md)
* [Zarządzanie niestandardowymi nazwami domen](active-directory-add-manage-domain-names.md)
* [Zapoznanie z koncepcjami związanymi z zarządzaniem domenami w usłudze Azure AD](active-directory-add-domain-concepts.md)

