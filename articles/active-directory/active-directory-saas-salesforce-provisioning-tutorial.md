---
title: "Samouczek: Integracji Azure Active Directory z usług Salesforce | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Salesforce."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 49384b8b-3836-4eb1-b438-1c46bb9baf6f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: a916be8dbf0b4c6173cda873936a53cd1f3ff12b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-salesforce-for-automatic-user-provisioning"></a>Samouczek: Konfigurowanie usług Salesforce użytkownika automatycznego inicjowania obsługi administracyjnej.

Celem Hello tego samouczka jest wymagane tooperform kroki hello tooshow w Salesforce i Azure AD tooautomatically udostępniania i usuwanie kont użytkowników z usługi Azure AD tooSalesforce.

## <a name="prerequisites"></a>Wymagania wstępne

Scenariusz Hello opisane w tym samouczku założono, że już hello następujące elementy:

*   Dzierżawy usługi Azure Active directory.
*   Musi mieć prawidłową dzierżawy dla usługi Salesforce w pracy lub Salesforce dla instytucji edukacyjnych. Można użyć bezpłatnego konta wersji próbnej dla każdej usługi.
*   Konto użytkownika w usłudze Salesforce z uprawnieniami administratora zespołu.

## <a name="assigning-users-toosalesforce"></a>Przypisywanie użytkowników tooSalesforce

Azure Active Directory korzysta z koncepcji o nazwie "przypisania" toodetermine użytkowników, którzy mają otrzymywać aplikacje tooselected dostępu. W kontekście hello Inicjowanie obsługi konta użytkowników tylko hello użytkowników i grup, które zostały "przypisane" tooan aplikacji w usłudze Azure AD jest zsynchronizowany.

Przed Skonfiguruj i Włącz hello usługi inicjowania obsługi administracyjnej, należy toodecide jakie użytkowników i/lub grup w usłudze Azure AD reprezentują hello użytkowników, którzy muszą uzyskiwać dostęp do aplikacji Salesforce tooyour. Po decyzję, wykonując następujące instrukcje hello tutaj można przypisać aplikacji Salesforce tooyour tych użytkowników:

[Przypisywanie użytkownikowi lub grupie aplikacji przedsiębiorstwa tooan](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-toosalesforce"></a>Ważne porady dotyczące przypisywania tooSalesforce użytkowników

*   Zalecane jest jeden użytkownik usługi Azure AD jest przypisany hello tootest tooSalesforce inicjowania obsługi konfiguracji. Później można przypisać dodatkowych użytkowników i/lub grup.

*  Podczas przypisywania tooSalesforce użytkownika, należy wybrać poprawnej roli użytkownika. Rola "Domyślnego dostępu" Hello nie działa w przypadku inicjowania obsługi administracyjnej

    > [!NOTE]
    > Ta aplikacja importuje role niestandardowe z Salesforce jako część procesu, który powitania klienta może być tooselect, przypisując użytkownikom udostępniania hello

## <a name="enable-automated-user-provisioning"></a>Włącz automatyczne Inicjowanie obsługi użytkowników

Ta sekcja przeprowadzi Cię przez łączenie inicjowania obsługi interfejsu API konta użytkownika tooSalesforce programu Azure AD i konfigurowanie hello inicjowania obsługi usługi toocreate, zaktualizować, a następnie wyłącz konta użytkowników przypisane w usłudze Salesforce w oparciu o przypisania użytkowników i grup w usłudze Azure AD .

>[!Tip]
>Można też tooenabled na języku SAML logowania jednokrotnego dla usług Salesforce, po hello instrukcje podane w [portalu Azure](https://portal.azure.com). Logowanie jednokrotne można skonfigurować niezależnie od automatycznego inicjowania obsługi administracyjnej, chociaż te dwie funkcje uzupełniania siebie nawzajem.

### <a name="tooconfigure-automatic-user-account-provisioning"></a>tooconfigure użytkownika automatyczne Inicjowanie obsługi konta:

Celem Hello w tej sekcji jest toooutline jak tooSalesforce kont tooenable użytkownika usługi Active Directory Inicjowanie obsługi użytkowników.

1. W hello [portalu Azure](https://portal.azure.com), Przeglądaj toohello **usługi Azure Active Directory > aplikacje przedsiębiorstwa > wszystkie aplikacje** sekcji.

2. Jeśli usługa Salesforce została już skonfigurowana dla logowania jednokrotnego, wyszukiwanie dla swojego wystąpienia usługi Salesforce za pomocą pola wyszukiwania hello. W przeciwnym razie wybierz **Dodaj** i wyszukaj **Salesforce** w galerii aplikacji hello. Wybierz usługi Salesforce z wyników wyszukiwania hello i dodać tooyour listę aplikacji.

3. Wybierz wystąpienie usługi Salesforce, a następnie wybierz hello **inicjowania obsługi administracyjnej** kartę.

4. Zestaw hello **inicjowania obsługi trybu** za**automatyczne**. 
![Inicjowanie obsługi administracyjnej](./media/active-directory-saas-salesforce-provisioning-tutorial/provisioning.png)

5. W obszarze hello **poświadczeń administratora** sekcji, podaj hello następujące ustawienia konfiguracji:
   
    a. W hello **nazwa użytkownika administratora** tekstowym, wpisz nazwę, która ma hello konta usług Salesforce **administratorem** profilu w witrynie Salesforce.com przypisane.
   
    b. W hello **hasło administratora** tekstowym, wpisz hello hasło dla tego konta.

6. tooget Twojego tokenu zabezpieczającego usług Salesforce, otwórz nową kartę i zaloguj się do hello sam konto administratora usług Salesforce. Na powitania prawym górnym rogu strony hello, kliknij swoją nazwę, a następnie kliknij przycisk **Moje ustawienia**.

     ![Włącz inicjowanie obsługi użytkowników](./media/active-directory-saas-salesforce-provisioning-tutorial/sf-my-settings.png "Włącz inicjowanie obsługi użytkowników")
7. W okienku nawigacji po lewej stronie powitania kliknij **osobistych** tooexpand hello powiązanych sekcji, a następnie kliknij przycisk **zresetować moje tokenu zabezpieczeń**.
  
    ![Włącz inicjowanie obsługi użytkowników](./media/active-directory-saas-salesforce-provisioning-tutorial/sf-personal-reset.png "Włącz inicjowanie obsługi użytkowników")
8. Na powitania **zresetować moje tokenu zabezpieczeń** kliknij przycisk **zresetować tokenu zabezpieczeń** przycisku.

    ![Włącz inicjowanie obsługi użytkowników](./media/active-directory-saas-salesforce-provisioning-tutorial/sf-reset-token.png "Włącz inicjowanie obsługi użytkowników")
9. Sprawdź skrzynki odbiorczej poczty e-mail hello skojarzone z tym kontem administratora. Poszukaj wiadomości e-mail z witryny Salesforce.com zawierający hello nowy token zabezpieczający.
10. Skopiuj hello tokenu, przejdź do pozycji tooyour okno usługi Azure AD i wklej go do hello **gniazda tokenu** pola.

11. W portalu Azure hello, kliknij przycisk **Testuj połączenie** tooensure usługi Azure AD można połączyć aplikacji Salesforce tooyour.

12. W hello **wiadomość E-mail z powiadomieniem** wprowadź hello adres e-mail osoby lub grupy, który powinien otrzymywać powiadomienia błąd inicjowania obsługi administracyjnej i zaznacz pole wyboru hello poniżej.

13. Kliknij przycisk **zapisać.**  
    
14.  W obszarze hello sekcji mapowania, wybierz **tooSalesforce synchronizacji Azure Active Directory użytkowników.**

15. W hello **mapowań atrybutów** Przejrzyj hello atrybutów użytkowników, które są synchronizowane z usługą Azure AD tooSalesforce. Należy pamiętać, że wybrany jako atrybuty hello **pasujące** właściwości są używane toomatch hello konta w usłudze Salesforce operacje aktualizacji. Wybierz toocommit przycisk Zapisz hello wszelkie zmiany.

16. tooenable hello inicjowania obsługi usługi Azure AD dla usług Salesforce, zmień hello **stan inicjowania obsługi administracyjnej** za**na** w sekcji Ustawienia hello

17. Kliknij przycisk **zapisać.**

Spowoduje to uruchomienie synchronizacji początkowej hello użytkowników i/lub grupy przypisane tooSalesforce w hello użytkowników i grup sekcji. Należy pamiętać, że tooperform dłużej niż kolejne synchronizacje, które występują co około 20 minut, tak długo, jak działa usługa hello przyjmuje hello synchronizacji początkowej. Można użyć hello **szczegóły synchronizacji** sekcji postępu toomonitor i wykonaj łącza tooprovisioning działania raporty, które opisują wszystkie działania wykonywane przez hello świadczenie usługi w aplikacji Salesforce.

Można teraz utworzyć konta testowego. Poczekaj na górę minut too20 tooverify, który hello konto zostało zsynchronizowane tooSalesforce.

## <a name="additional-resources"></a>Dodatkowe zasoby

* [Zarządzanie aprowizacja konta użytkowników dla aplikacji przedsiębiorstwa](active-directory-saas-tutorial-list.md)
* [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md)
* [Konfigurowanie rejestracji jednokrotnej](active-directory-saas-salesforce-tutorial.md)