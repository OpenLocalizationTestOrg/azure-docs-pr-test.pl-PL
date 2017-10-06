---
title: 'Samouczek: Integracji Azure Active Directory z piaskownicy Salesforce | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i usług Salesforce piaskownicy."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: bab73fda-6754-411d-9288-f73ecdaa486d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: jeedes
ms.openlocfilehash: 06ff50050845383a602b0edd6fca953ddd37cebd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-salesforce-sandbox-for-automatic-user-provisioning"></a>Samouczek: Konfigurowanie piaskownicy Salesforce użytkownika automatycznego inicjowania obsługi administracyjnej.

Celem Hello tego samouczka jest tooshow hello czynności, które należy tooperform w piaskownicy Salesforce i Azure AD tooautomatically udostępniania i usuwanie kont użytkowników z usługi Azure AD tooSalesforce piaskownicy.

## <a name="prerequisites"></a>Wymagania wstępne

Scenariusz Hello opisane w tym samouczku założono, że już hello następujące elementy:

*   Dzierżawy usługi Azure Active directory.
*   Musi mieć prawidłową dzierżawy piaskownicy Salesforce pracy lub Salesforce piaskownicy dla instytucji edukacyjnych. Można użyć bezpłatnego konta wersji próbnej dla każdej usługi.
*   Konto użytkownika w piaskownicy usługi Salesforce z uprawnieniami administratora zespołu.

## <a name="assigning-users-toosalesforce-sandbox"></a>Przypisywanie użytkowników tooSalesforce piaskownicy

Azure Active Directory korzysta z koncepcji o nazwie "przypisania" toodetermine użytkowników, którzy mają otrzymywać aplikacje tooselected dostępu. W kontekście hello Inicjowanie obsługi konta użytkowników tylko hello użytkowników i grup, które zostały "przypisane" tooan aplikacji w usłudze Azure AD są synchronizowane.

Przed Skonfiguruj i Włącz hello usługi inicjowania obsługi administracyjnej, należy toodecide jakie użytkowników i/lub grup w usłudze Azure AD reprezentują hello użytkowników, którzy wymagają dostępu tooyour aplikacji Salesforce piaskownicy. Po decyzję, wykonując instrukcje hello w tym miejscu można przypisać te tooyour użytkowników aplikacji Salesforce piaskownicy:

[Przypisywanie użytkownikowi lub grupie aplikacji przedsiębiorstwa tooan](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-toosalesforce-sandbox"></a>Ważne porady dotyczące przypisywania użytkowników tooSalesforce piaskownicy

* Zalecane jest jeden użytkownik usługi Azure AD jest przypisany hello tootest piaskownicy tooSalesforce inicjowania obsługi konfiguracji. Później można przypisać dodatkowych użytkowników i/lub grup.

* Podczas przypisywania tooSalesforce użytkownika piaskownicy, musisz wybrać poprawnej roli użytkownika. Rola "Domyślnego dostępu" Hello nie działa w przypadku inicjowania obsługi administracyjnej.

> [!NOTE]
> Ta aplikacja importuje role niestandardowe w piaskownicy Salesforce jako część procesu, który powitania klienta może być tooselect, przypisując użytkownikom udostępniania hello.

## <a name="enable-automated-user-provisioning"></a>Włącz automatyczne Inicjowanie obsługi użytkowników

Ta sekcja przeprowadzi Cię przez łączenie inicjowania obsługi interfejsu API konta użytkownika piaskownicy tooSalesforce usługi Azure AD i konfigurowanie hello inicjowania obsługi usługi toocreate, zaktualizować, a następnie wyłącz przypisany użytkownik, który kont w piaskownicy Salesforce na podstawie użytkownika i grupy przypisania w usłudze Azure AD.

>[!Tip]
>Można też tooenabled na języku SAML logowania jednokrotnego dla piaskownicy Salesforce, po hello instrukcje podane w [portalu Azure](https://portal.azure.com). Logowanie jednokrotne można skonfigurować niezależnie od automatycznego inicjowania obsługi administracyjnej, chociaż te dwie funkcje uzupełniania siebie nawzajem.

### <a name="tooconfigure-automatic-user-account-provisioning"></a>tooconfigure użytkownika automatyczne Inicjowanie obsługi konta:

Celem Hello w tej sekcji jest toooutline jak tooenable użytkownika usługi Active Directory Inicjowanie obsługi użytkowników kont tooSalesforce piaskownicy.

1. W hello [portalu Azure](https://portal.azure.com), Przeglądaj toohello **usługi Azure Active Directory > aplikacje przedsiębiorstwa > wszystkie aplikacje** sekcji.

2. Salesforce piaskownicy został już skonfigurowany dla logowania jednokrotnego, wyszukaj wystąpieniem piaskownicy Salesforce za pomocą hello pola wyszukiwania. W przeciwnym razie wybierz **Dodaj** i wyszukaj **piaskownicy Salesforce** w galerii aplikacji hello. Wybierz piaskownicy usługi Salesforce z wyników wyszukiwania hello i dodać tooyour listy aplikacji.

3. Wybierz wystąpienie usługi Salesforce piaskownicy, a następnie wybierz hello **inicjowania obsługi administracyjnej** kartę.

4. Zestaw hello **inicjowania obsługi trybu** za**automatyczne**. 
    ![Inicjowanie obsługi administracyjnej](./media/active-directory-saas-salesforce-sandbox-provisioning-tutorial/provisioning.png)

5. W obszarze hello **poświadczeń administratora** sekcji, podaj hello następujące ustawienia konfiguracji:
   
    a. W hello **nazwa użytkownika administratora** tekstowym, wpisz nazwę, która ma hello konta piaskownicy Salesforce **administratorem** profilu w witrynie Salesforce.com przypisane.
   
    b. W hello **hasło administratora** tekstowym, wpisz hello hasło dla tego konta.

6. tooget Twojego tokenu zabezpieczającego usług Salesforce piaskownicy, otwórz nową kartę i zaloguj się hello samo konto administratora usług Salesforce piaskownicy. Na powitania prawym górnym rogu strony hello, kliknij swoją nazwę, a następnie kliknij przycisk **Moje ustawienia**.

     ![Włącz inicjowanie obsługi użytkowników](./media/active-directory-saas-salesforce-sandbox-provisioning-tutorial/sf-my-settings.png "Włącz inicjowanie obsługi użytkowników")
7. W okienku nawigacji po lewej stronie powitania kliknij **osobistych** tooexpand hello powiązanych sekcji, a następnie kliknij przycisk **zresetować moje tokenu zabezpieczeń**.
  
    ![Włącz inicjowanie obsługi użytkowników](./media/active-directory-saas-salesforce-sandbox-provisioning-tutorial/sf-personal-reset.png "Włącz inicjowanie obsługi użytkowników")
8. Na powitania **zresetować moje tokenu zabezpieczeń** kliknij przycisk hello **zresetować tokenu zabezpieczeń** przycisku.

    ![Włącz inicjowanie obsługi użytkowników](./media/active-directory-saas-salesforce-sandbox-provisioning-tutorial/sf-reset-token.png "Włącz inicjowanie obsługi użytkowników")
9. Sprawdź skrzynki odbiorczej poczty e-mail hello skojarzone z tym kontem administratora. Poszukaj wiadomości e-mail z Salesforce Sandbox.com, zawierający hello nowy token zabezpieczający.
10. Skopiuj hello tokenu, przejdź do pozycji tooyour okno usługi Azure AD i wklej go do hello **gniazda tokenu** pola.

11. W portalu Azure hello, kliknij przycisk **Testuj połączenie** tooensure usługi Azure AD mogą się łączyć tooyour aplikacji Salesforce piaskownicy.

12. W hello **wiadomość E-mail z powiadomieniem** wprowadź hello adres e-mail osoby lub grupy, który powinien otrzymywać powiadomienia błąd inicjowania obsługi administracyjnej i zaznacz pole wyboru hello.

13. Kliknij przycisk **zapisać.**  
    
14.  W obszarze hello sekcji mapowania, wybierz **tooSalesforce synchronizacji Azure Active Directory użytkowników piaskownicy.**

15. W hello **mapowań atrybutów** Przejrzyj hello atrybutów użytkowników, które są synchronizowane z usługą Azure AD tooSalesforce piaskownicy. Witaj atrybuty wybrany jako **pasujące** właściwości są używane toomatch kont użytkowników hello w piaskownicy Salesforce dla operacji update. Wybierz toocommit przycisk Zapisz hello wszelkie zmiany.

16. tooenable hello inicjowania obsługi usługi Azure AD dla piaskownicy Salesforce, zmień hello **stan inicjowania obsługi administracyjnej** za**na** w sekcji Ustawienia hello

17. Kliknij przycisk **zapisać.**


Rozpoczyna hello wstępnej synchronizacji użytkowników i/lub grupy przypisane tooSalesforce piaskownicy w sekcji hello użytkowników i grup. Witaj początkowej synchronizacji ma tooperform dłużej niż kolejne synchronizacje, które występują co około 20 minut, tak długo, jak działa usługa hello. Można użyć hello **szczegóły synchronizacji** sekcji postępu toomonitor i wykonaj łącza tooprovisioning działania raporty, które opisują wszystkie działania wykonywane przez hello świadczenie usługi w aplikacji Salesforce piaskownicy.

Można teraz utworzyć konta testowego. Poczekaj na górę minut too20 tooverify, który hello konto zostało zsynchronizowane toosalesforce.

## <a name="additional-resources"></a>Dodatkowe zasoby

* [Zarządzanie aprowizacja konta użytkowników dla aplikacji przedsiębiorstwa](active-directory-saas-tutorial-list.md)
* [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md)
* [Konfigurowanie rejestracji jednokrotnej](active-directory-saas-salesforcesandbox-tutorial.md)