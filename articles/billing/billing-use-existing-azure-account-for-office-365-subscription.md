---
title: "aaaSign dla usługi Office 365 z kontem platformy Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak subskrypcja toocreate usługi Office 365 przy użyciu konta platformy Azure"
services: 
documentationcenter: 
author: JiangChen79
manager: adpick
editor: 
tags: billing,top-support-issue
ms.assetid: 
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 08/03/2017
ms.author: cjiang
ms.openlocfilehash: d19e1c1edff0b9658b639e796a72bbf4e87b9c3d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="sign-up-for-an-office-365-subscription-with-your-azure-account"></a>Załóż subskrypcji usługi Office 365 z Twoim kontem platformy Azure
Jeśli jest to Twoja subskrypcja platformy Azure, można użyć toosign Twojego konta platformy Azure dla subskrypcji usługi Office 365. W przypadku części organizacji, która ma subskrypcji platformy Azure, można utworzyć subskrypcji usługi Office 365 dla użytkowników w istniejącej Azure usługi Active Directory (Azure AD). Zarejestruj się tooOffice 365 przy użyciu konta mającego uprawnienia administratora globalnego lub administratorem rozliczeń w dzierżawie usługi Azure Active Directory. Aby uzyskać więcej informacji, zobacz [Sprawdź uprawnienia Moje konto w usłudze Azure AD](#RoleInAzureAD) i [przypisywanie ról administratorów w usłudze Azure Active Directory](../active-directory/active-directory-assign-admin-roles.md).

Jeśli masz już konto usługi Office 365 oraz subskrypcji platformy Azure, możesz [skojarzyć tooan dzierżawy usługi Office 365 subskrypcji platformy Azure](billing-add-office-365-tenant-to-azure-subscription.md).

## <a name="get-an-office-365-subscription-by-using-your-azure-account"></a>Uzyskiwanie subskrypcji usługi Office 365 przy użyciu konta platformy Azure

1. Przejdź toohello [stronę produktu usługi Office 365](https://products.office.com/business)i wybierz plan.
2. Kliknij przycisk **Zaloguj** na powitania prawym górnym rogu strony hello.

    ![Zrzut ekranu przedstawiający stronę wersji próbnej usługi Office 365](./media/billing-use-existing-azure-account-office-365-subscription/12-office-365-trial-page.png)
3. Zaloguj się przy użyciu poświadczeń konta platformy Azure. Jeśli tworzysz subskrypcję dla swojej organizacji, należy użyć konta platformy Azure, który jest członkiem roli hello Administrator globalny lub administrator rozliczeń katalogu w dzierżawie usługi Azure Active Directory.

    ![Zrzut ekranu usługi Office 365, logowanie](./media/billing-use-existing-azure-account-office-365-subscription/13-office-365-sign-in.png)
4. Kliknij przycisk **Wypróbuj teraz**.

    ![Zrzut ekranu potwierdzenie zamówienia dla usługi Office 365.](./media/billing-use-existing-azure-account-office-365-subscription/14-office-365-confirm-your-order.png)
5. Na stronie Potwierdzenie dostarczenia kolejności powitania kliknij **Kontynuuj**.

    ![Zrzut ekranu przedstawiający przyjęcia zamówień hello usługi Office 365](./media/billing-use-existing-azure-account-office-365-subscription/15-office-365-order-receipt.png)

Teraz wszystko jest gotowe. Jeśli subskrypcja usługi Office 365 hello został utworzony dla Twojej organizacji, użyj powitania po toocheck kroki, które użytkownicy usługi Azure AD są dostępne w usłudze Office 365.

1. Otwórz Centrum administracyjne usługi Office 365 hello.
2. Rozwiń węzeł **użytkowników**, a następnie kliknij przycisk **aktywni użytkownicy**.

    ![Zrzut ekranu przedstawiający Centrum administratorów hello usługi Office 365](./media/billing-use-existing-azure-account-office-365-subscription/16-office-365-admin-center-users.png)

Po utworzeniu konta hello subskrypcji usługi Office 365 jest dodawany toohello tego samego wystąpienia usługi Azure Active Directory, należącego do Twojej subskrypcji platformy Azure. Aby uzyskać więcej informacji, zobacz [więcej informacji na temat subskrypcji platformy Azure i usługi Office 365](billing-use-existing-office-365-account-azure-subscription.md#more-about-subs) i [jak subskrypcje platformy Azure są kojarzone z usługi Azure Active Directory](../active-directory/active-directory-how-subscriptions-associated-directory.md).

## <a id="RoleInAzureAD"></a>Sprawdź uprawnienia Moje konto w usłudze Azure AD
1. Zaloguj się toohello [portalu Azure](https://portal.azure.com/).
2. Kliknij przycisk **więcej usług**, a następnie wyszukaj **usługi Active Directory**.

    ![Zrzut ekranu z usługi Active Directory w portalu Azure hello](./media/billing-use-existing-azure-account-office-365-subscription/billing-more-services-active-directory.png)
3. Kliknij przycisk **użytkowników i grup** > **wszyscy użytkownicy**.
4. Wybierz nazwę użytkownika hello. 

    ![Zrzut ekranu pokazujący hello użytkowników usługi Azure Active Directory](./media/billing-use-existing-azure-account-office-365-subscription/billing-users-groups.png)

5. Kliknij przycisk **roli katalogu**.
  
    ![Zrzut ekranu pokazujący hello Azure directory portalu roli](./media/billing-use-existing-azure-account-office-365-subscription/billing-user-directory-role.png)
6.  Rola Hello **administratora globalnego** lub **administratorem ograniczonym** > **administrator rozliczeń** jest wymagane toocreate subskrypcję usługi Office 365 dla użytkowników w usłudze istniejącej usługi Azure Active Directory.

    ![Zrzut ekranu pokazujący usługi Azure directory portalu rolę administratora rozliczeń](./media/billing-use-existing-azure-account-office-365-subscription/billing-directoryrole-limited.png)

## <a name="need-help-contact-support"></a>Potrzebujesz pomocy? Skontaktuj się z pomocą techniczną.
Jeśli nadal potrzebujesz pomocy, [się z pomocą techniczną](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget szybkie rozwiązanie problemu. 
