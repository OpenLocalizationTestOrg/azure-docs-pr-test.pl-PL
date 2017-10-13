---
title: "Przypisywanie licencji na usługę Azure MFA | Microsoft Docs"
description: "Dowiedz się, jak przypisywać użytkownikom licencje na usługę Microsoft Azure Multi-Factor Authentication."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 514ef423-8ee6-4987-8a4e-80d5dc394cf9
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/13/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: it-pro
ROBOTS: NOINDEX
ms.openlocfilehash: 45522bf526c4aeab1d6ccc8891a55a0436ff9320
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="assigning-an-azure-mfa-azure-ad-premium-or-enterprise-mobility-license-to-users"></a>Przypisywanie użytkownikom licencji usługi Azure MFA, usługi Azure AD w wersji Premium lub pakietu Enterprise Mobility
Jeśli zakupiono licencję usługi Azure MFA, usługi Azure AD w wersji Premium lub pakietu Enterprise Mobility Suite, nie trzeba tworzyć dostawcy usługi Multi-Factor Authentication. Po przypisaniu licencji użytkownikom będzie można umożliwić im korzystanie z usługi MFA.

## <a name="to-assign-a-license"></a>Aby przypisać licencję
1. Zaloguj się do [klasycznego portalu Azure](https://manage.windowsazure.com) jako administrator.
2. W obszarze po lewej stronie wybierz pozycję **Active Directory**.
3. Na stronie usługi Active Directory kliknij dwukrotnie katalog zawierający użytkowników, których chcesz włączyć.
4. W górnej części strony katalogu wybierz pozycję **Licencje**.
   ![Przypisywanie licencji](./media/multi-factor-authentication-get-started-assign-licenses/assign1.png)
5. Na stronie Licencje wybierz pozycję **Azure Multi-Factor Authentication**, **Active Directory Premium** lub **Enterprise Mobility Suite**.  Jeśli masz tylko jedną licencję, powinna ona zostać wybrana automatycznie.
6. W dolnej części strony kliknij pozycję **Przypisz**.
   ![Przypisywanie licencji](./media/multi-factor-authentication-get-started-assign-licenses/assign3.png)
7. W wyświetlonym oknie kliknij obok użytkowników lub grup, którym chcesz przypisać licencje.  Zostanie wyświetlony zielony znacznik wyboru.
8. Kliknij ikonę znacznika wyboru, aby zapisać zmiany.
   ![Przypisywanie licencji](./media/multi-factor-authentication-get-started-assign-licenses/assign4.png)
9. Pojawi się komunikat z informacją o liczbie przypisanych licencji i liczbie ewentualnych niepowodzeń przypisań licencji.  Kliknij przycisk **OK**.
   ![Przypisywanie licencji](./media/multi-factor-authentication-get-started-assign-licenses/assign5.png)

## <a name="next-steps"></a>Następne kroki

- Aby uzyskać więcej informacji, zobacz [What is Microsoft Azure Active Directory licensing?](../active-directory/active-directory-licensing-what-is.md) (Co to jest licencjonowanie usługi Microsoft Azure Active Directory?)
