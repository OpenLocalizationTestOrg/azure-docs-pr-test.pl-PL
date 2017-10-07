---
title: aaaAzure Active Directory powiadomienia o raportach
description: "Jak toouse hello powiadomienia raportowania usługi Azure Active Directory dla podejrzanych znak dodatków."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: ae6d4b0e-5931-4cb3-98bf-9be91b381c92
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/15/2017
ms.author: dhanyahk;markvi
ms.custom: oldportal
ms.reviewer: dhanyahk
ms.openlocfilehash: 3843c45eaf9d68e671943bfdbc7ab68933f38fbb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-reporting-notifications"></a>Powiadomienia o raportach usługi Azure Active Directory
## <a name="what-reports-generate-email-notifications"></a>Jakie raporty generowanie powiadomień e-mail
W tej chwili tylko hello nieregularne znak w wyzwalaczy raport aktywności wiadomości e-mail z powiadomieniami.

## <a name="what-is-an-irregular-sign-in"></a>Co to jest "nieregularne logowania"?
Nieregularne logowania są tymi, które zostały zidentyfikowane przez naszych algorytmów, na podstawie hello warunku "niemożliwa podróż", w połączeniu z nietypowych lokalizacji logowania i urządzenia uczenia maszynowego. Może to oznaczać, że haker zostały próby toosign za pomocą tego konta.

## <a name="who-receives-hello-email-notifications"></a>Kto otrzymuje powiadomienia e-mail hello?
Witaj poczty e-mail są wysyłane tooall administratorów globalnych, który został przypisany do licencji usługi Active Directory — wersja Premium. tooensure on jest przeprowadzane, możemy wysyłać go również toohello Administratorzy alternatywny adres E-mail. Administratorzy powinna zawierać aad-alerts-noreply@mail.windowsazure.com na liście bezpiecznych, nie zostaną pominięte hello poczty e-mail.

## <a name="how-often-are-these-emails-sent"></a>Jak często są te wiadomości e-mail wysyłanych?
Hello wiadomość e-mail jest wysyłana, gdy 10 nowych nieregularne logowania działań występują w hello ostatnich 30 dni lub ponieważ hello ostatnią wiadomość e-mail została wysłana, ta wartość jest mniejsza.

## <a name="how-do-i-access-hello-report-mentioned-in-hello-email"></a>Jak uzyskać dostępu do raportu hello wspomnianego hello poczty e-mail?
Po kliknięciu łącza hello będzie przekierowany toohello strony raportu w hello klasycznego portalu Azure. W kolejności tooaccess hello raport, należy toobe zarówno:

* Administrator lub współadministratora subskrypcji platformy Azure
* Administrator globalny w katalogu hello i przypisaniu licencji usługi Active Directory — wersja Premium. Aby uzyskać więcej informacji, zobacz [Wersje usługi Azure Active Directory](active-directory-editions.md).

## <a name="can-i-turn-off-these-emails"></a>Można wyłączyć te wiadomości e-mail?
Tak, tooturn wyłączyć powiadomienia dotyczące logowania tooanomalous w hello klasycznego portalu Azure, kliknij przycisk **Konfiguruj**, a następnie wybierz **wyłączone** w obszarze hello **powiadomienia**sekcji.

## <a name="whats-next"></a>Co dalej
* Zastanawiasz się, jak zabezpieczeń, inspekcji i raporty dotyczące działań są dostępne? Zapoznaj się z [zabezpieczeń platformy Azure AD, inspekcji i raporty dotyczące działań](active-directory-view-access-usage-reports.md)
* [Wprowadzenie do usługi Azure Active Directory — wersja Premium](active-directory-get-started-premium.md)
* [Dodawanie znakowania firmowego tooyour logowania i panelu dostępu do stron](active-directory-add-company-branding.md)

