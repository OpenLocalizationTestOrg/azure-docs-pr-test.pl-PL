---
title: "Samouczek: Konfigurowanie Samanage dla użytkownika automatycznego inicjowania obsługi administracyjnej z usługą Azure Active Directory | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak konta tooSamanage tooconfigure usługi Azure Active Directory tooautomatically udostępniania i usuwanie użytkowników."
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
ms.openlocfilehash: 6cb36d2cc6ce33da4f8ebba65d138bfd4f2aca9b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-samanage-for-automatic-user-provisioning"></a>Samouczek: Konfigurowanie Samanage dla użytkownika automatycznego inicjowania obsługi administracyjnej.


Celem Hello tego samouczka jest tooshow hello czynności, które należy tooperform w Samanage i Azure AD tooautomatically udostępniania i usuwanie kont użytkowników z usługi Azure AD tooSamanage. 

## <a name="prerequisites"></a>Wymagania wstępne

Scenariusz Hello opisane w tym samouczku założono, że już hello następujące elementy:

*   Dzierżawy usługi Azure Active directory
*   Dzierżawcy Samanage z hello [Professional planu](https://www.samanage.com/pricing/) lub lepiej jest włączone 
*   Konto użytkownika z uprawnieniami administratora w Samanage 

> [!NOTE]
> Hello Azure AD inicjowania obsługi administracyjnej integracji opiera się na powitania [interfejsu API REST Samanage](https://www.samanage.com/api/), zespoły tooSamanage dostępne na powitania Professional planowanie lub większą.

## <a name="assigning-users-toosamanage"></a>Przypisywanie użytkowników tooSamanage

Azure Active Directory korzysta z koncepcji o nazwie "przypisania" toodetermine użytkowników, którzy mają otrzymywać aplikacje tooselected dostępu. W kontekście hello Inicjowanie obsługi konta użytkowników tylko hello użytkowników i grup, które zostały "przypisane" tooan aplikacji w usłudze Azure AD jest zsynchronizowany. 

Przed Skonfiguruj i Włącz hello usługi inicjowania obsługi administracyjnej, należy toodecide jakie użytkowników i/lub grup w usłudze Azure AD reprezentują hello użytkowników, którzy muszą uzyskiwać dostęp do aplikacji Samanage tooyour. Po decyzję, wykonując instrukcje hello w tym miejscu można przypisać tych użytkowników tooyour Samanage aplikacji:

[Przypisywanie użytkownikowi lub grupie aplikacji przedsiębiorstwa tooan](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-toosamanage"></a>Ważne porady dotyczące przypisywania tooSamanage użytkowników

*   Zalecane jest jeden użytkownik usługi Azure AD jest przypisany hello tootest tooSamanage inicjowania obsługi konfiguracji. Później można przypisać dodatkowych użytkowników i/lub grup.

*   Podczas przypisywania tooSamanage użytkownika, należy wybrać albo hello **użytkownika** rola, lub inny prawidłowy specyficzne dla aplikacji (jeśli jest dostępny) w oknie dialogowym przydział hello. Witaj **domyślnego dostępu** roli nie działa w przypadku inicjowania obsługi administracyjnej, a użytkownicy są pomijane.

> [!NOTE]
> Dodano funkcję hello świadczenie usługi odczytuje wszystkie role niestandardowe zdefiniowane w Samanage i zaimportowanie ich do usługi Azure AD, w którym można je wybrać w oknie dialogowym Wybierz rolę hello. Role te będą widoczne w hello portalu Azure po włączeniu hello usługi inicjowania obsługi administracyjnej i jednego cyklu synchronizacji zostało ukończone.

## <a name="configuring-user-provisioning-toosamanage"></a>Konfigurowanie inicjowania obsługi administracyjnej tooSamanage użytkownika 

Ta sekcja przeprowadzi Cię przez łączenie inicjowania obsługi interfejsu API konta użytkownika tooSamanage programu Azure AD i konfigurowanie hello inicjowania obsługi usługi toocreate, zaktualizować, a następnie wyłącz konta użytkowników przypisane w Samanage w oparciu o przypisania użytkowników i grup w usłudze Azure AD.

> [!TIP]
> Można też tooenabled na języku SAML logowania jednokrotnego dla Samanage hello instrukcje podane w następujących [portalu Azure](https://portal.azure.com). Logowanie jednokrotne można skonfigurować niezależnie od automatycznego inicjowania obsługi administracyjnej, chociaż te dwie funkcje uzupełniania siebie nawzajem.


### <a name="configure-automatic-user-account-provisioning-toosamanage-in-azure-ad"></a>Skonfiguruj konto użytkownika automatycznego inicjowania obsługi administracyjnej tooSamanage w usłudze Azure AD:


1. W hello [portalu Azure](https://portal.azure.com), Przeglądaj toohello **usługi Azure Active Directory > aplikacje przedsiębiorstwa > wszystkie aplikacje** sekcji.

2. Samanage został już skonfigurowany dla logowania jednokrotnego, wyszukaj wystąpieniem Samanage za pomocą hello pola wyszukiwania. W przeciwnym razie wybierz **Dodaj** i wyszukaj **Samanage** w galerii aplikacji hello. Wybierz Samanage z wyników wyszukiwania hello i dodać go tooyour listy aplikacji.

3. Wybierz wystąpienia programu Samanage, a następnie wybierz hello **inicjowania obsługi administracyjnej** kartę.

4. Zestaw hello **inicjowania obsługi trybu** za**automatyczne**.

    ![Samanage inicjowania obsługi administracyjnej.](./media/active-directory-saas-samanage-provisioning-tutorial/Samanage1.png)

5. W obszarze hello **poświadczeń administratora** hello wejściowych, sekcji **nazwa użytkownika i hasło administratora** Twojego Samanage konta. 

6. W portalu Azure hello, kliknij przycisk **Testuj połączenie** tooensure usługi Azure AD można połączyć tooyour Samanage aplikację. Jeśli hello połączenia nie powiedzie się, upewnij się, że Twoje konto Samanage ma uprawnienia administratora i spróbuj ponownie wykonać krok 5.

7. Wprowadź adres e-mail hello osoby lub grupy, które powinny być przesyłane powiadomienia błąd inicjowania obsługi administracyjnej w hello **wiadomość E-mail z powiadomieniem** pola i wyboru hello wyboru "Wyślij wiadomość e-mail z powiadomieniem, gdy wystąpi błąd."

8. Kliknij pozycję **Zapisz**. 

9. W obszarze hello sekcji mapowania, wybierz **tooSamanage synchronizacji Azure Active Directory użytkowników**.

10. W hello **mapowań atrybutów** Przejrzyj hello atrybutów użytkowników, które są synchronizowane z usługą Azure AD tooSamanage. Witaj atrybuty wybrany jako **pasujące** właściwości są używane toomatch hello kontom Samanage dla operacji update. Wybierz toocommit przycisk Zapisz hello wszelkie zmiany.

11. tooenable hello inicjowania obsługi usługi Azure AD dla Samanage, zmień hello **stan inicjowania obsługi administracyjnej** za**na** w hello **ustawienia** sekcji

12. Kliknij pozycję **Zapisz**. 

Ta operacja spowoduje uruchomienie synchronizacji początkowej hello użytkowników i/lub grupy przypisane tooSamanage w hello użytkowników i grup sekcji. Witaj początkowej synchronizacji ma tooperform dłużej niż kolejne synchronizacje, które występują co około 20 minut, tak długo, jak działa usługa hello. Można użyć hello **szczegóły synchronizacji** sekcji postępu toomonitor i wykonaj łącza tooprovisioning działania raporty, które opisują wszystkie działania wykonywane przez hello inicjowania obsługi usługi.

Aby uzyskać więcej informacji dotyczących sposobu inicjowania obsługi usługi Azure AD hello tooread logowania, zobacz [raportowania na użytkownika automatyczne Inicjowanie obsługi konta](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).


## <a name="additional-resources"></a>Dodatkowe zasoby

* [Zarządzanie aprowizacja konta użytkowników dla aplikacji przedsiębiorstwa](active-directory-enterprise-apps-manage-provisioning.md)
* [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md)

## <a name="next-steps"></a>Następne kroki

* [Dowiedz się, jak dzienniki tooreview i Uzyskaj raporty dotyczące inicjowania obsługi administracyjnej działania](active-directory-saas-provisioning-reporting.md)
