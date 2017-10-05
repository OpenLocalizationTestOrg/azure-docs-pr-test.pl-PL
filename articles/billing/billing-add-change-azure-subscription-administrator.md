---
title: "Dodawanie lub zmienianie ról subskrypcji Azure administratora | Dokumentacja firmy Microsoft"
description: "Opisuje, jak dodać lub zmienić administratora współpracującego Azure, Administrator usługi i konto administratora"
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
ms.openlocfilehash: da5995535d42ed52772cb09e0f4da51bbf878748
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="add-or-change-azure-administrator-roles-that-manage-the-subscription-or-services"></a>Dodać lub zmienić role administratora platformy Azure, zarządzających subskrypcji lub usług
Możesz zmienić administratora platformy Azure, który zarządza subskrypcji platformy Azure ani nie zarządza nimi usług Azure używane w ramach subskrypcji. Aby wyświetlić Azure informacji dotyczących rozliczeń i Zarządzaj subskrypcjami, należy zalogować się do [Centrum konta](https://account.windowsazure.com/Home/Index) jako administratora konta. 

## <a name="add-an-admin-for-a-subscription"></a>Dodawanie administratora dla subskrypcji
Możesz dodać administratora platformy Azure w portalu Azure lub w klasycznym portalu Azure.

**Witryna Azure Portal**

Aby dodać osobę administratora dla subskrypcji w portalu Azure, możesz przydzielić im rolę właściciela. Rola właściciela może zarządzać tylko zasobów w subskrypcji, który zostanie przypisany. Nie ma uprawnień dostępu do innych subskrypcji. Właściciele dodać za pomocą [portalu Azure](https://portal.azure.com) nie może zarządzać zasobem w [klasycznego portalu Azure](https://manage.windowsazure.com).

1. Zaloguj się w witrynie [Azure Portal](https://portal.azure.com).
2. W menu Centrum wybierz **subskrypcji** > *subskrypcji, która ma administratora, aby uzyskać dostęp do*.

    ![Zrzut ekranu pokazujący wybranej subskrypcji](./media/billing-add-change-azure-subscription-administrator/newselectsub.png)

3. W bloku subskrypcji, wybierz **(IAM) kontroli dostępu**.
4. Wybierz **dodać** > **roli** > **właściciela**. Wpisz adres e-mail użytkownika, aby dodać jako właściciela, wybierz użytkownika, a następnie wybierz **zapisać**.

    ![Zrzut ekranu pokazujący rolę właściciela wybrane](./media/billing-add-change-azure-subscription-administrator/add-role.png)

5. Jeśli chcesz dodać konto właściciela jako administratora współpracującego w **(IAM) kontroli dostępu** strony, kliknij prawym przyciskiem myszy użytkownika, a następnie wybierz **Dodaj jako współadministrator**. Ta funkcja jest teraz dostępna w [portalu Azure w wersji zapoznawczej](https://preview.portal.azure.com/). 

     ![Zrzut ekranu, który dodaje współadministratorem](./media/billing-add-change-azure-subscription-administrator/add-coadmin.png)

    >[!TIP]
    >Musisz dodać użytkownika "Właściciela" jako współadministrator, jeśli użytkownik chce zarządzać usług platformy Azure w [klasycznego portalu Azure](https://manage.windowsazure.com/).

    Aby usunąć uprawnienia administratora współpracującego, kliknij prawym przyciskiem myszy użytkownika "współadministratorem", a następnie wybierz **usunąć administratora współpracującego**.

    ![Zrzut ekranu, która usuwa współadministratorem](./media/billing-add-change-azure-subscription-administrator/remove-coadmin.png)


**Klasyczna witryna Azure Portal**

1. Zaloguj się do [klasycznej witryny Azure Portal](https://manage.windowsazure.com/).
2. W okienku nawigacji wybierz **ustawienia**> **Administratorzy**> **Dodaj**. </br>

    ![Zrzut ekranu pokazujący sposób uzyskać dostęp do przycisku Dodaj](./media/billing-add-change-azure-subscription-administrator/addcoadmin.png)
3. Wpisz adres e-mail osoby, którą chcesz dodać jako współadministrator, a następnie wybierz subskrypcję, która ma współadministrator do uzyskania dostępu.</br>

    ![Zrzut ekranu pokazujący wybranej subskrypcji ](./media/billing-add-change-azure-subscription-administrator/addcoadmin2.png)</br>

Adres e-mail mogą być dodawane jako Współadministrator:

* **Account Microsoft** (dawniej identyfikator Windows Live ID) </br>
  Zaloguj się do wszystkich produktów firmy Microsoft konsumentów i usługami w chmurze, takich jak Outlook (usługi Hotmail), Skype (MSN), OneDrive, Windows Phone i Xbox LIVE, można użyć Account firmy Microsoft.
* **Konta organizacyjnego**</br>
  Konta organizacyjnego jest kontem, która jest tworzona w usłudze Azure Active Directory. Ten format jest adres konta organizacyjnego:

    Użytkownik @&lt;domenę&gt;. onmicrosoft.com

## <a name="change-service-administrator-for-a-subscription"></a>Zmienić administratora usługi dla subskrypcji
Tylko Administrator konta może zmienić administratora usługi dla subskrypcji.

1. Zaloguj się do [Centrum konta platformy Azure](https://account.windowsazure.com/subscriptions) przy użyciu konta administratora.
2. Wybierz subskrypcję, którą chcesz zmienić.
3. Po prawej stronie wybierz **edytować subskrypcji** szczegóły. </br>

    ![editsub](./media/billing-add-change-azure-subscription-administrator/editsub.png)
4. W **administratora usługi** wprowadź adres e-mail nowego administratora usługi. </br>

    ![changeSA](./media/billing-add-change-azure-subscription-administrator/changeSA.png)

## <a name="change-the-account-administrator"></a>Zmiana konta administratora
Aby przetransferować własność konta platformy Azure na inne konto, zobacz [transfer własności subskrypcji platformy Azure](billing-subscription-transfer.md).

Zdecydowanie zaleca się nie możesz usunąć lub zmienić adresu e-mail administratora konta. Może pojawić się nieoczekiwane i niepożądane zachowanie w przypadku konta platformy Azure. Może nie być w stanie zalogować się do platformy Azure przy użyciu tego konta, wprowadzać zmiany na koncie lub zarządzanie zasobami za pomocą tego konta. 

## <a name="check-the-account-administrator-of-the-subscription"></a>Sprawdzenie administratora konta subskrypcji
Jeśli nie masz pewności, który jest administratorem konta subskrypcji, aby dowiedzieć się, należy użyć następujące kroki.

  1. Zaloguj się w witrynie [Azure Portal](https://portal.azure.com).
  2. W menu Centrum wybierz **subskrypcji**.
  3. Wybierz subskrypcję, którą chcesz sprawdzić, a następnie sprawdź w obszarze **ustawienia**.
  4. Wybierz **właściwości**. Administratora konta subskrypcji jest wyświetlany w **administrator konta** pole.  

## <a name="types-of-azure-admin-accounts"></a>Typy kont administratora platformy Azure
 Konto administratora, Administrator usługi i współadministrator są trzy rodzaje ról administratorów w Microsoft Azure. W poniższej tabeli opisano różnice między tych trzech ról administracyjnych.

| Rola administratora | Limit | Opis |
| --- | --- | --- |
| Konto administratora (AA) |1 na konto platformy Azure |To jest osobą, która utworzył konto na lub zakupiono subskrypcji platformy Azure i uprawnień dostępu [Centrum konta](https://account.windowsazure.com/Home/Index) i wykonywać różne zadania zarządzania. Obejmują one, można tworzyć subskrypcje, anulowanie subskrypcji, zmienić rozliczeń dla subskrypcji oraz zmienić administratora usługi. |
| Administrator usługi (SA) |1 na subskrypcji platformy Azure |Ta rola jest autoryzowany do zarządzania usługami w [portalu Azure](https://portal.azure.com). Domyślnie na nową subskrypcję konto administratora jest również administratorem usługi. |
| Współadministrator (CA) w [klasycznego portalu Azure](https://manage.windowsazure.com) |200 na subskrypcję |Ta rola ma takie same uprawnienia dostępu jak administrator usługi, ale nie może zmieniać skojarzenia subskrypcji do katalogów platformy Azure. |

Azure opartej na roli Active Directory kontroli dostępu (RBAC) umożliwia użytkownikom można dodać do wielu ról. Aby uzyskać więcej informacji, zobacz [kontroli dostępu opartej na roli Azure Active Directory](../active-directory/role-based-access-control-configure.md).

## <a name="limitations-and-restrictions-for-admin-accounts"></a>Ograniczenia dla konta administratora
* Każda subskrypcja jest skojarzona z katalogu usługi Azure AD (znanej także jako domyślny katalog). Aby znaleźć katalog domyślny jest skojarzony z subskrypcją, przejdź do [klasycznego portalu Azure](https://manage.windowsazure.com/), wybierz pozycję **ustawienia** > **subskrypcje**. Sprawdź identyfikator subskrypcji można znaleźć katalogu domyślne.
* Jeśli logujesz się przy użyciu Account firmy Microsoft, innych Accounts Microsoft lub użytkowników w katalogu domyślne można tylko dodać jako Współadministrator.
* Jeśli logujesz się za pomocą konta organizacyjnego, można dodać inne konta organizacyjne w organizacji jako Współadministrator. Na przykład abby@contoso.com można dodać bob@contoso.com administratorem usługi ani Współadministratorem, ale nie można dodać john@notcontoso.com chyba że john@notcontoso.com jest w domyślnym katalogiem. Użytkownicy zalogowany za pomocą konta organizacyjne można kontynuować dodawanie użytkowników Account Microsoft administratorem usługi ani Współadministratorem.
* Teraz istnieje możliwość logowanie do platformy Azure za pomocą konta organizacyjnego, w tym miejscu jest zmiany administratora usługi i współadministrator wymagania dotyczące konta:

  | Zaloguj się — metoda | Dodaj Account Microsoft lub użytkowników w ramach katalog domyślny jako urzędu certyfikacji lub SA? | Dodaj konto organizacyjne w tej samej organizacji jako urzędu certyfikacji lub SA? | Dodaj konto organizacyjne w innej organizacji jako urzędu certyfikacji lub SA? |
  | --- | --- | --- | --- |
  |  Konto Microsoft |Tak |Nie |Nie |
  |  Konto organizacji |Tak |Tak |Nie |

## <a name="learn-more-about-resource-access-control-and-active-directory"></a>Dowiedz się więcej na temat kontroli dostępu do zasobów i usługi Active Directory
* Aby dowiedzieć się więcej na temat sposobu jest kontrolowany dostęp do zasobów w systemie Microsoft Azure, zobacz [opis dostęp do zasobów na platformie Azure](../active-directory/active-directory-understanding-resource-access.md).
* Aby uzyskać więcej informacji o usłudze Azure Active Directory, zobacz [jak subskrypcje platformy Azure są kojarzone z usługi Azure Active Directory](../active-directory/active-directory-how-subscriptions-associated-directory.md) i [przypisywanie ról administratorów w usłudze Azure Active Directory](../active-directory/active-directory-assign-admin-roles.md).

## <a name="need-help-contact-support"></a>Potrzebujesz pomocy? Skontaktuj się z pomocą techniczną.
Jeśli nadal potrzebujesz pomocy, [się z pomocą techniczną](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) uzyskać szybkie rozwiązanie problemu.
