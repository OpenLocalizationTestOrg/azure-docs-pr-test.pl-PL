---
title: "aaaUse usługi Office 365 dzierżawcy z subskrypcją platformy Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooan katalogu (dzierżawcy) tooadd usługi Office 365 subskrypcji platformy Azure."
services: 
documentationcenter: 
author: JiangChen79
manager: jlian
editor: 
tags: billing,top-support-issue
ms.assetid: cc9c57c6-7bfd-4dea-9027-c75ef3737589
ms.service: billing
ms.workload: na
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: cjiang
ms.openlocfilehash: e560370417bd074a7e37ceb7c60da45dbbbcf775
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="associate-an-office-365-tenant-tooan-azure-subscription"></a>Skojarz tooan dzierżawy usługi Office 365 subskrypcji platformy Azure
Połącz oddzielne subskrypcji platformy Azure i usługi Office 365, umożliwiając dostęp do dzierżawy usługi Office 365 hello z subskrypcją platformy Azure. toolink subskrypcji, zaloguj się tooAzure z hello konta administratora usługi Azure, dodanie katalogu i Dodaj dzierżawy usługi Azure Active Directory toohello konta organizacyjne hello usługi Office 365.

Jeśli chcesz subskrypcji usługi Office 365 dla użytkowników w wystąpieniu usługi Azure Active Directory lub mieć konto usługi Office 365, ale nie jest konto platformy Azure, zobacz [tworzenia konta platformy Azure z kontem usługi Office 365](billing-use-existing-office-365-account-azure-subscription.md). 

## <a name="before-you-begin"></a>Przed rozpoczęciem
* Musi mieć hello poświadczenia administratora usługi subskrypcji platformy Azure hello. Konta administratora współpracującego nie można wykonać niektóre kroki hello w tym artykule. toochange administratorem usługi, zobacz [jak tooadd lub zmień role administratora platformy Azure](billing-add-change-azure-subscription-administrator.md#change-service-administrator-for-a-subscription).
* Musi mieć poświadczenia administratora globalnego dzierżawy usługi Office 365 hello hello.
* adres e-mail administratora usługi hello Hello nie może występować w hello dzierżawy usługi Office 365.
* adres e-mail administratora usługi hello Hello musi niezgodne z administratorami globalnymi dzierżawy hello usługi Office 365.
* Jeśli używany jest adres e-mail konta Microsoft i konta organizacyjnego, tymczasowo zmienić administratora usługi hello toouse Twojej subskrypcji platformy Azure innego konta Microsoft. Możesz utworzyć konto Microsoft na powitania [strony Rejestracja konta Microsoft](https://signup.live.com/).

## <a name="link-office-365-tenant-tooazure-subscription"></a>Łączenie subskrypcji tooAzure dzierżawy usługi Office 365
toohello dzierżawy usługi Office 365 hello tooassociate subskrypcji platformy Azure, wykonaj następujące kroki:

### <a name="step-1-add-office-365-tenant-tooyour-azure-subscription"></a>Krok 1: Dodaj tooyour dzierżawy usługi Office 365 subskrypcji platformy Azure

1. Zaloguj się toohello [klasycznego portalu Azure](https://manage.windowsazure.com/) przy użyciu poświadczeń administratora usługi hello.

    ![Zrzut ekranu Azure logowanie](./media/billing-add-office-365-tenant-to-azure-subscription/s313_azure-sign-in-service-admin.png)

2. Wybierz w okienku po lewej stronie powitania **usługi ACTIVE DIRECTORY**. Niepowołanymi dzierżawy hello usługi Office 365. Jeśli zostanie wyświetlony, Pomiń zbyt[krok 2: Zmień katalog hello skojarzone z hello subskrypcji platformy Azure](#Step2).
   
   ![Wpis zrzut ekranu z usługi Active Directory](./media/billing-add-office-365-tenant-to-azure-subscription/s35-classic-portal-active-directory-entry.png)

3. Wybierz **nowy** > **katalogu** > **tworzenie NIESTANDARDOWYCH**.
   
    ![Utwórz niestandardowy zrzut ekranu z usługą Azure Active Directory](./media/billing-add-office-365-tenant-to-azure-subscription/s37-aad-custom-create.png)
   
4. Na powitania **Dodaj katalog** w obszarze **katalogu**, wybierz pozycję **Użyj istniejącego katalogu**. Następnie wybierz **jestem toobe gotowa, teraz wylogować**i wybierz **Complete** ![ukończyć ikona](./media/billing-add-office-365-tenant-to-azure-subscription/s38_complete-icon.png).
   
    ![Zrzut ekranu przedstawiający "Użyj istniejącego katalogu"](./media/billing-add-office-365-tenant-to-azure-subscription/s39_add-directory-use-existing.png)
   
5. Po zarejestrowaniu zalogować się przy użyciu poświadczeń administratora globalnego hello dzierżawy usługi Office 365.
   
    ![Logowanie administratora globalnego zrzut ekranu usługi Office 365](./media/billing-add-office-365-tenant-to-azure-subscription/s310_sign-in-global-admin-office-365.png)
   
6. Wybierz **kontynuować**.
   
    ![Zrzut ekranu przedstawiający weryfikacji](./media/billing-add-office-365-tenant-to-azure-subscription/s311_use-contoso-directory-azure-verify.png)
   
7. Wybierz **Wyloguj się teraz**.
   
    ![Zrzut ekranu przedstawiający wylogowania](./media/billing-add-office-365-tenant-to-azure-subscription/s312_use-contoso-directory-azure-confirm-and-sign-out.png)
   
8. Zaloguj się toohello [klasycznego portalu Azure](https://manage.windowsazure.com/) przy użyciu poświadczeń administratora usługi hello.
   
    ![Zrzut ekranu Azure logowanie](./media/billing-add-office-365-tenant-to-azure-subscription/s313_azure-sign-in-service-admin.png)
   
9. Dzierżawy usługi Office 365 na pulpicie nawigacyjnym hello powinna zostać wyświetlona.
   
    ![Zrzut ekranu przedstawiający pulpit nawigacyjny](./media/billing-add-office-365-tenant-to-azure-subscription/s314_office-365-tenant-appear-in-azure.png)

### <a name="Step2"></a>Krok 2: Zmień katalog hello skojarzony z hello subskrypcji platformy Azure
   
1. Wybierz **ustawienia**.
   
    ![Zrzut ekranu Azure ikona klasycznych ustawień portalu](./media/billing-add-office-365-tenant-to-azure-subscription/s315_azure-classic-portal-settings-icon.png)
   
2. Wybierz subskrypcję platformy Azure, a następnie wybierz **Edytuj katalog**.

    ![Zrzut ekranu Azure subskrypcji edycji katalogu](./media/billing-add-office-365-tenant-to-azure-subscription/s316_azure-subscription-edit-directory.png)
   
3. Wybierz **dalej** ![dalej](./media/billing-add-office-365-tenant-to-azure-subscription/s317_next-icon.png).
   
    ![Zrzut ekranu przedstawiający "Zmiany hello skojarzone katalogu"](./media/billing-add-office-365-tenant-to-azure-subscription/s318_azure-change-associated-directory.png)
   
4. Przejrzyj kont hello, których to dotyczy. W przypadku wszystkich administratorów wspólnej i [kontroli dostępu opartej na rolach (RBAC)](../active-directory/role-based-access-control-configure.md) użytkownicy z dostępem przypisane w hello istniejących grup zasobów zostaną usunięte. Ostrzeżenie Hello, które otrzymujesz wymienia tylko usunięcie hello współadministratorów.
      
    ![Zrzut ekranu pokazujący hello kont administratora współpracującego toobe usunięte.](./media/billing-add-office-365-tenant-to-azure-subscription/s322_azure-confirm-directory-mapping.png)
   
    ![Zrzut ekranu przedstawia przykład toobe konta użytkownika usunięte.](./media/billing-add-office-365-tenant-to-azure-subscription/s325_assigned-users-removed-resource-groups.png)
   
5. Wybierz **Complete** ![ukończyć ikona](./media/billing-add-office-365-tenant-to-azure-subscription/s38_complete-icon.png).

### <a name="step-3-add-your-office-365-organizational-accounts-as-co-administrators-toohello-azure-active-directory-tenant"></a>Krok 3: Dodawanie konta organizacyjnego usługi Office 365 jako dzierżawy usługi Azure Active Directory toohello współadministratorów
   
1. Wybierz hello **ADMINISTRATORZY** , a następnie wybierz **dodać**.
   
    ![Karta Administratorzy ustawienia portalu klasycznego zrzut ekranu Azure](./media/billing-add-office-365-tenant-to-azure-subscription/s319_azure-classic-portal-settings-administrators.png)
   
2. Wprowadź konto organizacyjne dzierżawy usługi Office 365, wybierz hello subskrypcji platformy Azure, a następnie wybierz **Complete** ![ukończyć ikona](./media/billing-add-office-365-tenant-to-azure-subscription/s38_complete-icon.png).
   
    ![Zrzut ekranu Azure Dodaj współadministratorem — okno dialogowe](./media/billing-add-office-365-tenant-to-azure-subscription/s320_azure-add-co-administrator.png)
   
3. Przejdź wstecz toohello **ADMINISTRATORZY** kartę. Witaj konta organizacyjnego wyświetlany jako współadministrator powinna zostać wyświetlona.
   
    ![Zrzut ekranu przedstawiający kartę Administratorzy](./media/billing-add-office-365-tenant-to-azure-subscription/s321_azure-co-administrator-added.png)
4.  Test tooAzure dostępu z kontem administratora współpracującego hello.
   
    a. Wyloguj hello klasycznego portalu Azure.
   
    b. Otwórz hello [portalu Azure](https://portal.azure.com/).
   
    c. Wprowadź poświadczenia administratora współpracującego hello hello, a następnie wybierz **Zaloguj**.
   
    ![Zrzut ekranu Azure strony logowania](./media/billing-add-office-365-tenant-to-azure-subscription/s324_azure-sign-in-with-co-admin.png)

## <a name="need-help-contact-support"></a>Potrzebujesz pomocy? Skontaktuj się z pomocą techniczną.
Jeśli nadal potrzebujesz pomocy, [się z pomocą techniczną](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget szybkie rozwiązanie problemu.


