---
title: "Jak przeprowadzić przegląd dostępu | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak przeprowadzić przegląd aplikacji Azure Privileged Identity Management."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 49ee2feb-7d2e-4acf-82c1-40ff23062862
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/06/2017
ms.author: billmath
ms.custom: pim
ms.openlocfilehash: a98ed60221eeba1d9c92df846aeae2deafb8ae60
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-perform-an-access-review-in-azure-ad-privileged-identity-management"></a>Jak przeprowadzić przegląd dostępu w usłudze Azure AD Privileged Identity Management
Azure Active Directory (AD) Privileged Identity Management upraszcza, jak zarządzać uprzywilejowanego dostępu do zasobów w usłudze Azure AD i innych usług online firmy Microsoft, takich jak usługi Office 365 lub Microsoft Intune w przedsiębiorstwach.  

Jeśli użytkownik został przypisany do roli administratora, administrator ról uprzywilejowanych w organizacji może poprosić o regularnie potwierdzić nadal potrzebujesz tej roli dla zadania. Może spowodować, że wiadomość e-mail zawierającą łącze lub można przejść bezpośrednio do [portalu Azure](https://portal.azure.com). Wykonaj kroki opisane w tym artykule, aby wykonać własnym przeglądu przypisane role.

Jeśli administrator ról uprzywilejowanych zainteresowana przeglądami dostępu, Dowiedz się więcej na [jak rozpocząć Przegląd dostępu](active-directory-privileged-identity-management-how-to-start-security-review.md).

## <a name="add-the-privileged-identity-management-application"></a>Dodawanie aplikacji Privileged Identity Management
Możesz użyć aplikacji Azure AD Privileged Identity zarządzania (PIM) w [portalu Azure](https://portal.azure.com/) przeprowadzić zapoznania się z nimi.  Jeśli nie masz aplikacji usługi Azure AD Privileged Identity Management w portalu sieci, wykonaj następujące kroki, aby rozpocząć.

1. Zaloguj się w witrynie [Azure Portal](https://portal.azure.com/).
2. Wybierz swoją nazwę użytkownika w prawym górnym rogu portalu Azure i wybierz katalog, w której będzie można działać.
3. Wybierz polecenie **Więcej usług** i użyj pola tekstowego filtru, aby wyszukać **Azure AD Privileged Identity Management**.
4. Zaznacz opcję **Przypnij do pulpitu nawigacyjnego**, a następnie kliknij pozycję **Utwórz**. Zostanie otwarta aplikacja Privileged Identity Management.

## <a name="approve-or-deny-access"></a>Zatwierdzenia lub odmowy dostępu
Podczas zatwierdzania lub odmówić dostępu należy jest po prostu informuje recenzenta czy możesz nadal używać tej roli lub nie. Wybierz **Zatwierdź** aby pozostać w tej roli, lub **Odmów** Jeśli nie musisz już dostępu. Stan użytkownika nie zostaną zmienione od razu, dopóki recenzenta stosuje wyniki.
Wykonaj te czynności, aby go przejrzeć dostępu:

1. W aplikacji PIM zaznacz **przeglądu uprzywilejowany dostęp**. Jeśli masz wszelkie oczekujące dostępu przeglądy pojawią się one w bloku przeglądami dostępu usługi Azure AD.
2. Wybierz przeglądu, które chcesz wykonać.
3. Jeśli nie utworzono przeglądu, wyświetlane jako jedynym użytkownikiem w przeglądzie. Zaznacz pole wyboru obok swojej nazwy.
4. Wybierz **zatwierdzić** lub **odmowy**. Może być konieczne uwzględnienie Przyczyna decyzji w **przyczyny** pola tekstowego.  
5. Zamknij **ról Przegląd usługi Azure AD** bloku.

<!--Every topic should have next steps and links to the next logical set of content to keep the customer engaged-->
## <a name="next-steps"></a>Następne kroki
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-configure/PIM_EnablePim.png
