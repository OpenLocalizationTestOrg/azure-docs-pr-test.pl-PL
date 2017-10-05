---
title: "Następne kroki dla zarządzania dostępem przy użyciu grup | Dokumentacja firmy Microsoft"
description: "Jak zaawansowane — do obiektu dla Zarządzanie grupami zabezpieczeń i zarządzanie dostępem do zasobów przy użyciu tych grup."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 44350a3c-8ea1-4da1-aaac-7fc53933dd21
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: curtand
ms.custom: oldportal;it-pro;
ms.openlocfilehash: 82fbeb379e90add09f7c569111053f6e9b1bc9c5
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="managing-owners-for-a-group"></a>Zarządzanie właścicielami grupy
Gdy właściciel zasobu ma przypisany dostęp do tego zasobu do grupy usługi Azure AD, członkostwo w grupie jest zarządzana przez właściciela grupy. Właściciel zasobu przekazuje skutecznie uprawnienie do przypisywania użytkowników do zasobów do właściciela grupy.

> [!IMPORTANT]
> Firma Microsoft zaleca zarządzanie usługą Azure AD przy użyciu [centrum administracyjnego usługi Azure AD](https://aad.portal.azure.com) w witrynie Azure Portal zamiast korzystania z klasycznej witryny Azure Portal przywołanej w niniejszym artykule. 

## <a name="assigning-group-ownership"></a>Przypisywanie własności grup
**Aby dodać właściciela grupy**

1. W [klasycznego portalu Azure](https://manage.windowsazure.com), wybierz pozycję **usługi Active Directory**, a następnie otwórz katalogu organizacji.
2. Wybierz **grup** karcie, a następnie otwórz grupę, którą chcesz dodać właścicieli.
3. Wybierz **Dodaj właścicieli**.
4. Na **Dodaj właścicieli** wybierz użytkownika, który chcesz dodać jako właściciela tej grupy i upewnij się, że ta nazwa jest dodawana do **wybrane** okienka.

**Aby usunąć właściciela grupy**

1. W [klasycznego portalu Azure](https://manage.windowsazure.com), wybierz pozycję **usługi Active Directory**, a następnie otwórz katalogu organizacji.
2. Wybierz **grup** karcie, a następnie otwórz grupę, którą chcesz usunąć właściciela.
3. Wybierz **właścicieli** kartę.
4. Wybierz właściciela, który chcesz usunąć z tej grupy, a następnie wybierz **Usuń**.

## <a name="additional-information"></a>Dodatkowe informacje
Te artykuły zawierają dodatkowe informacje o usłudze Azure Active Directory.

* [Zarządzanie dostępem do zasobów za pomocą grup usługi Azure Active Directory](active-directory-manage-groups.md)
* [Polecenia cmdlet usługi Azure Active Directory służące do konfigurowania ustawień grupy](active-directory-accessmanagement-groups-settings-cmdlets.md)
* [Indeks artykułów dotyczących zarządzania aplikacjami w usłudze Azure Active Directory](active-directory-apps-index.md)
* [Co to jest usługa Azure Active Directory?](active-directory-whatis.md)
* [Integrowanie tożsamości lokalnych z usługą Azure Active Directory](active-directory-aadconnect.md)
