---
title: "Samouczek: Konfigurowanie usługi GitHub dla użytkownika automatycznego inicjowania obsługi administracyjnej z usługą Azure Active Directory | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak konta tooGitHub tooconfigure usługi Azure Active Directory tooautomatically udostępniania i usuwanie użytkowników."
services: active-directory
documentationcenter: 
author: asmalser-msft
writer: asmalser-msft
manager: stevenpo
ms.assetid: d4ca2365-6729-48f7-bb7f-c0f5ffe740a3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: asmalser-msft
ms.openlocfilehash: c1f0f7a42e4f8a94db3f409cd463e13bb1bc13bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-github-for-automatic-user-provisioning"></a>Samouczek: Konfigurowanie usługi GitHub dla użytkownika automatycznego inicjowania obsługi administracyjnej.


Celem Hello tego samouczka jest tooshow hello czynności, które należy tooperform w GitHub i Azure AD tooautomatically udostępniania i usuwanie kont użytkowników z usługi Azure AD tooGitHub. 

## <a name="prerequisites"></a>Wymagania wstępne

Scenariusz Hello opisane w tym samouczku założono, że już hello następujące elementy:

*   Dzierżawy usługi Azure Active directory
*   Dzierżawcy Github z hello [planu firm](https://help.github.com/articles/organization-billing-plans/#business-plan) lub lepiej jest włączone 
*   Konto użytkownika z uprawnieniami administratora w usłudze GitHub 

> [!NOTE]
> Hello Azure AD inicjowania obsługi administracyjnej integracji opiera się na powitania [GitHub SCIM API](https://developer.github.com/v3/scim/), które jest dostępne tooGithub zespoły w planie firm hello lub większą.

## <a name="assigning-users-toogithub"></a>Przypisywanie użytkowników tooGitHub

Azure Active Directory korzysta z koncepcji o nazwie "przypisania" toodetermine użytkowników, którzy mają otrzymywać aplikacje tooselected dostępu. W kontekście hello Inicjowanie obsługi konta użytkowników tylko hello użytkowników i grup, które zostały "przypisane" tooan aplikacji w usłudze Azure AD jest zsynchronizowany. 

Przed Skonfiguruj i Włącz hello usługi inicjowania obsługi administracyjnej, należy toodecide jakie użytkowników i/lub grup w usłudze Azure AD reprezentują hello użytkowników, którzy muszą uzyskiwać dostęp do aplikacji GitHub tooyour. Po decyzję, wykonując instrukcje hello w tym miejscu można przypisać tych użytkowników tooyour GitHub aplikacji:

[Przypisywanie użytkownikowi lub grupie aplikacji przedsiębiorstwa tooan](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-toogithub"></a>Ważne porady dotyczące przypisywania tooGitHub użytkowników

*   Zalecane jest jeden użytkownik usługi Azure AD jest przypisany hello tootest tooGitHub inicjowania obsługi konfiguracji. Później można przypisać dodatkowych użytkowników i/lub grup.

*   Podczas przypisywania tooGitHub użytkownika, należy wybrać albo hello **użytkownika** rola, lub inny prawidłowy specyficzne dla aplikacji (jeśli jest dostępny) w oknie dialogowym przydział hello. Witaj **domyślnego dostępu** roli nie działa w przypadku inicjowania obsługi administracyjnej, a użytkownicy są pomijane.


## <a name="configuring-user-provisioning-toogithub"></a>Konfigurowanie inicjowania obsługi administracyjnej tooGitHub użytkownika 

Ta sekcja przeprowadzi Cię przez łączenie inicjowania obsługi interfejsu API konta użytkownika tooGitHub programu Azure AD i konfigurowanie hello inicjowania obsługi usługi toocreate, zaktualizować, a następnie wyłącz konta użytkowników przypisane w usłudze GitHub, w oparciu o przypisania użytkowników i grup w usłudze Azure AD.

> [!TIP]
> Można też tooenabled na języku SAML logowania jednokrotnego dla GitHub hello instrukcje podane w następujących [portalu Azure](https://portal.azure.com). Logowanie jednokrotne można skonfigurować niezależnie od automatycznego inicjowania obsługi administracyjnej, chociaż te dwie funkcje uzupełniania siebie nawzajem.


### <a name="configure-automatic-user-account-provisioning-toogithub-in-azure-ad"></a>Skonfiguruj konto użytkownika automatycznego inicjowania obsługi administracyjnej tooGitHub w usłudze Azure AD


1. W hello [portalu Azure](https://portal.azure.com), Przeglądaj toohello **usługi Azure Active Directory > aplikacje przedsiębiorstwa > wszystkie aplikacje** sekcji.

2. Jeśli skonfigurowano już program GitHub dla logowania jednokrotnego, wyszukaj dla swojego wystąpienia usługi GitHub, za pomocą pola wyszukiwania hello. W przeciwnym razie wybierz **Dodaj** i wyszukaj **GitHub** w galerii aplikacji hello. Wybierz GitHub z wyników wyszukiwania hello i dodać go tooyour listę aplikacji.

3. Wybierz wystąpienie usługi GitHub, a następnie wybierz hello **inicjowania obsługi administracyjnej** kartę.

4. Zestaw hello **inicjowania obsługi trybu** za**automatyczne**.

    ![Inicjowanie obsługi usługi GitHub](./media/active-directory-saas-github-provisioning-tutorial/GitHub1.png)

5. W obszarze hello **poświadczeń administratora** kliknij **autoryzacji**. Ta operacja otwiera okno dialogowe autoryzacji GitHub w nowym oknie przeglądarki. 

6. W nowym oknie hello Zaloguj się do usługi GitHub przy użyciu konta administratora. W hello wynikowy okna dialogowego autoryzacji, wybierz zespół GitHub hello, inicjowanie obsługi tooenable, a następnie wybierz **autoryzacji**. Inicjowanie obsługi konfiguracji hello toocomplete portalu Azure po zakończeniu, zwróć toohello.

    ![Okno dialogowe autoryzacji](./media/active-directory-saas-github-provisioning-tutorial/GitHub2.png)

7. W portalu Azure hello, wprowadź **adres URL dzierżawy** i kliknij przycisk **Testuj połączenie** tooensure usługi Azure AD można połączyć tooyour GitHub aplikację. Jeśli hello połączenia nie powiedzie się, upewnij się, Twoje konto GitHub ma uprawnienia administratora i **adres URl dzierżawy** jest wprowadzona poprawnie, a następnie spróbuj hello "Autoryzuj" krok ponownie (może stanowić **adres URL dzierżawy** przez regułę: "https : //api.github.com/scim/v2/organizations/ + < Organizations_name > ", można znaleźć Twojej organizacji na koncie usługi GitHub: **ustawienia** > **organizacji**).

    ![Okno dialogowe autoryzacji](./media/active-directory-saas-github-provisioning-tutorial/GitHub3.png)

8. Wprowadź adres e-mail hello osoby lub grupy, które powinny być przesyłane powiadomienia błąd inicjowania obsługi administracyjnej w hello **wiadomość E-mail z powiadomieniem** pola i wyboru hello wyboru "Wyślij wiadomość e-mail z powiadomieniem, gdy wystąpi błąd."

9. Kliknij pozycję **Zapisz**. 

10. W obszarze hello sekcji mapowania, wybierz **tooGitHub synchronizacji Azure Active Directory użytkowników**.

11. W hello **mapowań atrybutów** Przejrzyj hello atrybutów użytkowników, które są synchronizowane z usługą Azure AD tooGitHub. Witaj atrybuty wybrany jako **pasujące** właściwości są używane toomatch hello konta w serwisie GitHub operacje aktualizacji. Wybierz toocommit przycisk Zapisz hello wszelkie zmiany.

12. tooenable hello inicjowania obsługi usługi Azure AD dla usługi GitHub, zmień hello **stan inicjowania obsługi administracyjnej** za**na** w hello **ustawienia** sekcji

13. Kliknij pozycję **Zapisz**. 

Ta operacja spowoduje uruchomienie synchronizacji początkowej hello użytkowników i/lub grupy przypisane tooGitHub w hello użytkowników i grup sekcji. Witaj początkowej synchronizacji ma tooperform dłużej niż kolejne synchronizacje, które występują co około 20 minut, tak długo, jak działa usługa hello. Można użyć hello **szczegóły synchronizacji** sekcji postępu toomonitor i wykonaj łącza tooprovisioning działania raporty, które opisują wszystkie działania wykonywane przez hello inicjowania obsługi usługi.

Aby uzyskać więcej informacji dotyczących sposobu inicjowania obsługi usługi Azure AD hello tooread logowania, zobacz [raportowania na użytkownika automatyczne Inicjowanie obsługi konta](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).


## <a name="additional-resources"></a>Dodatkowe zasoby

* [Zarządzanie aprowizacja konta użytkowników dla aplikacji przedsiębiorstwa](active-directory-enterprise-apps-manage-provisioning.md)
* [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md)

## <a name="next-steps"></a>Następne kroki

* [Dowiedz się, jak dzienniki tooreview i Uzyskaj raporty dotyczące inicjowania obsługi administracyjnej działania](active-directory-saas-provisioning-reporting.md)
