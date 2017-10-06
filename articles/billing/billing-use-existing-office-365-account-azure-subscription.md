---
title: "aaaSign dla platformy Azure z kontem usługi Office 365 | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate subskrypcji platformy Azure przy użyciu konta usługi Office 365"
services: 
documentationcenter: 
author: JiangChen79
manager: adpick
editor: 
tags: billing,top-support-issue
ms.assetid: 129cdf7a-2165-483d-83e4-8f11f0fa7f8b
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 08/03/2017
ms.author: cjiang
ms.openlocfilehash: cc331bf7222b5b03e740cb40a214bc13ef585f54
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="sign-up-for-an-azure-subscription-with-your-office-365-account"></a>Załóż subskrypcji platformy Azure z Twoim kontem usługi Office 365
Jeśli masz subskrypcję usługi Office 365, korzystając z usługi Office 365 toocreate konta subskrypcji platformy Azure. Zaloguj się toohello [portalu Azure](https://portal.azure.com/) przy użyciu usługi Office 365, nazwę użytkownika i hasło. Jeśli chcesz tooset zapasowych maszyn wirtualnych lub innych usług platformy Azure, musi Załóż subskrypcji platformy Azure. Twoja subskrypcja platformy Azure można udostępniać innym użytkownikom i [korzystać z kontroli dostępu opartej na rolach toomanage dostępu tooyour subskrypcji platformy Azure i zasobów](https://docs.microsoft.com/azure/active-directory/role-based-access-control-configure)

Jeśli masz już konto usługi Office 365 oraz subskrypcji platformy Azure, zobacz [skojarzyć tooan dzierżawy usługi Office 365 subskrypcji platformy Azure](billing-add-office-365-tenant-to-azure-subscription.md).

## <a name="get-an-azure-subscription-using-your-office-365-account"></a>Uzyskiwanie subskrypcji platformy Azure przy użyciu konta usługi Office 365

Zaoszczędzić czas i uniknąć mnożenie konta po utworzeniu konta platformy Azure przy użyciu usługi Office 365, nazwę użytkownika i hasło. 

1. Zarejestruj się w [witryny Azure.com](https://account.azure.com/signup?offer=MS-AZR-0044p&appId=docs). 
2. Zaloguj się przy użyciu usługi Office 365, nazwę użytkownika i hasło. Witaj konto, którego używasz, nie wymaga uprawnień administratora toohave. Jeśli masz więcej niż jedno konto usługi Office 365, upewnij się, że używasz hello poświadczeń dla konta usługi Office 365 hello mają tooassociate z subskrypcją platformy Azure. 

   ![Zrzut ekranu pokazujący hello strony logowania.](./media/billing-use-existing-office-365-account-azure-subscription/billing-sign-in-with-office-365-account.png)

3. Wprowadź informacje wymagane hello i hello ukończenia procesu rejestracji. Niektóre informacje mogą być wymagane, jeśli masz już konto usługi Office 365.

    ![Zrzut ekranu pokazujący hello wypełnieniu formularza.](./media/billing-use-existing-office-365-account-azure-subscription/billing-azure-sign-up-fill-information.png)

- Jeśli potrzebujesz tooadd inne osoby w Twojej organizacji toohello subskrypcji platformy Azure, zobacz [wprowadzenie do zarządzania dostępem w portalu Azure hello](../active-directory/role-based-access-control-what-is.md). 

## <a id="more-about-subs">Więcej informacji na temat subskrypcji platformy Azure i usługi Office 365</a>
Office 365 i Azure używać użytkownicy toomanage usługi Azure AD hello i subskrypcji. Hello Azure directory przypomina kontenera, w którym można pogrupować użytkowników i subskrypcje. toouse hello tego samego konta dla subskrypcji platformy Azure i Office 365, toomake muszą się tego hello Azure subskrypcje są tworzone w hello sam katalogu jako subskrypcje hello usługi Office 365. Należy mieć na uwadze hello następujące punkty:

* Subskrypcja jest tworzony w katalogu
* Użytkownicy należą toodirectories
* Subskrypcja znajdzie się w katalogu hello hello użytkownika, który tworzy hello subskrypcji. Dzięki subskrypcji usługi Office 365 jest wiązana toohello tego samego konta jako subskrypcji platformy Azure.
* Subskrypcje platformy Azure są własnością poszczególnych użytkowników w katalogu hello
* Sam katalog hello należy do subskrypcji usługi Office 365. Użytkownicy z hello odpowiednie uprawnienia w katalogu hello mogą zarządzać te subskrypcje.

![Zrzut ekranu pokazujący relacji hello hello katalogu, użytkowników i subskrypcje.](./media/billing-use-existing-office-365-account-azure-subscription/19-background-information.png)

Aby uzyskać więcej informacji, zobacz [jak subskrypcje platformy Azure są kojarzone z usługi Azure Active Directory](../active-directory/active-directory-how-subscriptions-associated-directory.md).

## <a name="need-help-contact-support"></a>Potrzebujesz pomocy? Skontaktuj się z pomocą techniczną.
Jeśli nadal potrzebujesz pomocy, [się z pomocą techniczną](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget szybkie rozwiązanie problemu. 
