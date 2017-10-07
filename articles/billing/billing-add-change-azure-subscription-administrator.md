---
title: "aaaAdd lub zmień role subskrypcji Azure admin | Dokumentacja firmy Microsoft"
description: "Opisuje sposób tooadd lub zmień Współadministratorem Azure, Administrator usługi i konto administratora"
services: 
documentationcenter: 
author: genlin
manager: jlian
editor: 
tags: billing
ms.assetid: 13a72d76-e043-4212-bcac-a35f4a27ee26
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: genli
ms.openlocfilehash: 14eaecf2dbfd7152775ac3552bf3a7ae3db596b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="add-or-change-azure-administrator-roles-that-manage-hello-subscription-or-services"></a>Dodać lub zmienić role administratora platformy Azure, zarządzających hello subskrypcji lub usługi
Możesz zmienić hello Azure administratora, który zarządza subskrypcji platformy Azure ani nie zarządza nimi hello Azure usług używanych w ramach subskrypcji. tooview Azure informacji dotyczących rozliczeń i Zarządzaj subskrypcjami, musisz zalogować się toohello [Centrum konta](https://account.windowsazure.com/Home/Index) jako hello administratora konta. 

## <a name="add-an-admin-for-a-subscription"></a>Dodawanie administratora dla subskrypcji
Możesz dodać administratora platformy Azure w portalu Azure hello lub hello klasycznego portalu Azure.

**Witryna Azure Portal**

tooadd ktoś administratora dla subskrypcji w portalu Azure hello wyrazi hello właściciela roli. Rola właściciela Hello może zarządzać tylko hello zasobów w subskrypcji hello, któremu przypisano. Nie ma subskrypcji tooother uprawnień dostępu. Witaj właścicieli dodać za pomocą hello [portalu Azure](https://portal.azure.com) nie może zarządzać zasobem w hello [klasycznego portalu Azure](https://manage.windowsazure.com).

1. Zaloguj się toohello [portalu Azure](https://portal.azure.com).
2. W menu Centrum hello wybierz **subskrypcji** > *hello subskrypcji, które mają hello admin tooaccess*.

    ![Zrzut ekranu pokazujący wybranej subskrypcji](./media/billing-add-change-azure-subscription-administrator/newselectsub.png)

3. W bloku subskrypcji hello, wybierz **(IAM) kontroli dostępu**.
4. Wybierz **dodać** > **roli** > **właściciela**. Wpisz adres e-mail hello użytkownika hello tooadd właściciel hello wybierz użytkownika, a następnie wybrać **zapisać**.

    ![Zrzut ekranu pokazujący hello rolę właściciela](./media/billing-add-change-azure-subscription-administrator/add-role.png)

5. Jeśli ma być tooadd hello właściciela konta administratora współpracującego w hello **(IAM) kontroli dostępu** strony, kliknij prawym przyciskiem myszy hello użytkownika, a następnie wybierz **Dodaj jako współadministrator**. Ta funkcja jest teraz dostępna w [portalu Azure w wersji zapoznawczej](https://preview.portal.azure.com/). 

     ![Zrzut ekranu, który dodaje współadministratorem](./media/billing-add-change-azure-subscription-administrator/add-coadmin.png)

    >[!TIP]
    >Konieczne będzie tooadd hello "Właściciela" użytkownika jako administratora współpracującego Jeśli użytkownik hello musi toomanage hello usług platformy Azure w [klasycznego portalu Azure](https://manage.windowsazure.com/).

    uprawnienia administratora współpracującego hello tooremove, kliknij prawym przyciskiem myszy użytkownika "administrator wspólnej" hello, a następnie wybierz **usunąć administratora współpracującego**.

    ![Zrzut ekranu, która usuwa współadministratorem](./media/billing-add-change-azure-subscription-administrator/remove-coadmin.png)


**Klasyczna witryna Azure Portal**

1. Zaloguj się toohello [klasycznego portalu Azure](https://manage.windowsazure.com/).
2. Wybierz w okienku nawigacji hello **ustawienia**> **Administratorzy**> **Dodaj**. </br>

    ![Zrzut ekranu pokazujący sposób tooget toohello Dodawanie przycisku](./media/billing-add-change-azure-subscription-administrator/addcoadmin.png)
3. Wpisz adres e-mail osoby hello ma tooadd jako administratora współpracującego i hello następnie wybierz subskrypcję, która ma hello tooaccess współadministratorem hello.</br>

    ![Zrzut ekranu pokazujący wybranej subskrypcji ](./media/billing-add-change-azure-subscription-administrator/addcoadmin2.png)</br>

Witaj następującego adresu e-mail mogą być dodawane jako Współadministrator:

* **Account Microsoft** (dawniej identyfikator Windows Live ID) </br>
  Można użyć toosign Account Microsoft w tooall konsumentów produktów firmy Microsoft i usługami w chmurze, takich jak Outlook (usługi Hotmail), Skype (MSN), OneDrive, Windows Phone i Xbox LIVE.
* **Konta organizacyjnego**</br>
  Konta organizacyjnego jest kontem, która jest tworzona w usłudze Azure Active Directory. Ten format jest adres konta organizacyjnego Hello:

    Użytkownik @&lt;domenę&gt;. onmicrosoft.com

## <a name="change-service-administrator-for-a-subscription"></a>Zmienić administratora usługi dla subskrypcji
Tylko Administrator konta hello można zmienić hello administratora usługi dla subskrypcji.

1. Zaloguj się za[Centrum konta platformy Azure](https://account.windowsazure.com/subscriptions) przy użyciu hello administratora konta.
2. Wybierz subskrypcję hello ma toochange.
3. Na powitania po prawej stronie, wybierz **edytować subskrypcji** szczegóły. </br>

    ![editsub](./media/billing-add-change-azure-subscription-administrator/editsub.png)
4. W hello **administratora usługi** wprowadź adres e-mail hello hello nowego administratora usługi. </br>

    ![changeSA](./media/billing-add-change-azure-subscription-administrator/changeSA.png)

## <a name="change-hello-account-administrator"></a>Zmień hello konta administratora
własność tootransfer hello konta tooanother konto platformy Azure, zobacz [transfer własności subskrypcji platformy Azure](billing-subscription-transfer.md).

Zdecydowanie zaleca się nie możesz usunąć lub zmienić adresu e-mail administratora konta hello. Może pojawić się nieoczekiwane i niepożądane zachowanie w przypadku hello konto platformy Azure. Może nie być tooAzure stanie logowania przy użyciu tego konta, zmienić konta toohello lub zarządzanie zasobami za pomocą tego konta. 

## <a name="check-hello-account-administrator-of-hello-subscription"></a>Sprawdź hello administratora konta subskrypcji hello
Jeśli nie masz pewności będącego hello administratora konta subskrypcji, użyj hello następujące kroki toofind wychodzących.

  1. Zaloguj się toohello [portalu Azure](https://portal.azure.com).
  2. W menu Centrum hello wybierz **subskrypcji**.
  3. Wybierz subskrypcję hello chcesz toocheck, a następnie sprawdź w obszarze **ustawienia**.
  4. Wybierz **właściwości**. Witaj administratora konta subskrypcji hello jest wyświetlany w hello **administrator konta** pole.  

## <a name="types-of-azure-admin-accounts"></a>Typy kont administratora platformy Azure
 Konto administratora, Administrator usługi i współadministrator są hello trzy rodzaje ról administratorów w Microsoft Azure. Witaj poniższej tabeli opisano hello różnica między tych trzech ról administracyjnych.

| Rola administratora | Limit | Opis |
| --- | --- | --- |
| Konto administratora (AA) |1 na konto platformy Azure |To osoby hello utworzył konto na lub zakupiono subskrypcji platformy Azure i hello autoryzowanych tooaccess [Centrum konta](https://account.windowsazure.com/Home/Index) i wykonywać różne zadania zarządzania. Te obejmują jest możliwe toocreate subskrypcji, anulowanie subskrypcji, zmienić hello rozliczeń dla subskrypcji i zmienić hello administratora usługi. |
| Administrator usługi (SA) |1 na subskrypcji platformy Azure |Ta rola jest toomanage autoryzowanych usług w hello [portalu Azure](https://portal.azure.com). Domyślnie na nową subskrypcję hello konto administratora jest również hello administratora usługi. |
| Współadministrator (CA) w hello [klasycznego portalu Azure](https://manage.windowsazure.com) |200 na subskrypcję |Ta rola ma hello same poziomy dostępu jako hello administratora usługi, ale nie można zmienić skojarzenia hello katalogów tooAzure subskrypcji. |

Azure opartej na roli Active Directory kontroli dostępu (RBAC) umożliwia użytkownikom toobe dodane toomultiple ról. Aby uzyskać więcej informacji, zobacz [kontroli dostępu opartej na roli Azure Active Directory](../active-directory/role-based-access-control-configure.md).

## <a name="limitations-and-restrictions-for-admin-accounts"></a>Ograniczenia dla konta administratora
* Każda subskrypcja jest skojarzona z katalogu usługi Azure AD (znanej także jako hello katalog domyślny). toofind hello subskrypcji hello katalog domyślny jest skojarzony z Przejdź toohello [klasycznego portalu Azure](https://manage.windowsazure.com/), wybierz pozycję **ustawienia** > **subskrypcje**. Sprawdź hello subskrypcji identyfikator toofind hello katalog domyślny.
* Jeśli logujesz się przy użyciu Account firmy Microsoft, można tylko dodać inne Accounts Microsoft lub użytkowników w ramach hello katalog domyślny jako Współadministrator.
* Jeśli logujesz się za pomocą konta organizacyjnego, można dodać inne konta organizacyjne w organizacji jako Współadministrator. Na przykład abby@contoso.com można dodać bob@contoso.com administratorem usługi ani Współadministratorem, ale nie można dodać john@notcontoso.com chyba że john@notcontoso.com jest w domyślnym katalogiem. Użytkownicy zalogowany za pomocą konta organizacyjne, mogą nadal użytkowników Account Microsoft tooadd administratorem usługi ani Współadministratorem.
* Teraz, aby była możliwa toosign w tooAzure za pomocą konta organizacyjnego, Oto hello tooService zmiany administratora i wymagania dotyczące konta administratora współpracującego:

  | Zaloguj się — metoda | Dodaj Account Microsoft lub użytkowników w ramach katalog domyślny jako urzędu certyfikacji lub SA? | Dodaj konto organizacyjne w hello tej samej organizacji jako urzędu certyfikacji lub SA? | Dodaj konto organizacyjne w innej organizacji jako urzędu certyfikacji lub SA? |
  | --- | --- | --- | --- |
  |  Konto Microsoft |Tak |Nie |Nie |
  |  Konto organizacji |Tak |Tak |Nie |

## <a name="learn-more-about-resource-access-control-and-active-directory"></a>Dowiedz się więcej na temat kontroli dostępu do zasobów i usługi Active Directory
* Zobacz toolearn więcej informacji na temat sposobu jest kontrolowany dostęp do zasobów na platformie Microsoft Azure [opis dostęp do zasobów na platformie Azure](../active-directory/active-directory-understanding-resource-access.md).
* Aby uzyskać więcej informacji o usłudze Azure Active Directory, zobacz [jak subskrypcje platformy Azure są kojarzone z usługi Azure Active Directory](../active-directory/active-directory-how-subscriptions-associated-directory.md) i [przypisywanie ról administratorów w usłudze Azure Active Directory](../active-directory/active-directory-assign-admin-roles.md).

## <a name="need-help-contact-support"></a>Potrzebujesz pomocy? Skontaktuj się z pomocą techniczną.
Jeśli nadal potrzebujesz pomocy, [się z pomocą techniczną](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget szybkie rozwiązanie problemu.
