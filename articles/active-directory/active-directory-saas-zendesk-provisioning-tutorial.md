---
title: "Samouczek: Konfigurowanie usługi ZenDesk dla użytkownika automatycznego inicjowania obsługi administracyjnej z usługą Azure Active Directory | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak konta tooZenDesk tooconfigure usługi Azure Active Directory tooautomatically udostępniania i usuwanie użytkowników."
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
ms.openlocfilehash: 200e8790ec1755f5cf927274ceb38527dd993f3c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-zendesk-for-automatic-user-provisioning"></a>Samouczek: Konfigurowanie usługi ZenDesk dla użytkownika automatycznego inicjowania obsługi administracyjnej.


Celem Hello tego samouczka jest tooshow hello czynności, które należy tooperform w ZenDesk i Azure AD tooautomatically udostępniania i usuwanie kont użytkowników z usługi Azure AD tooZenDesk. 

## <a name="prerequisites"></a>Wymagania wstępne

Scenariusz Hello opisane w tym samouczku założono, że już hello następujące elementy:

*   Dzierżawy usługi Azure Active directory
*   Dzierżawcy ZenDesk z hello [Enterprise plan](https://www.zendesk.com/product/pricing/) lub lepiej jest włączone 
*   Konto użytkownika z uprawnieniami administratora w ZenDesk 

> [!NOTE]
> Witaj usługi Azure AD inicjowania obsługi administracyjnej integracji opiera się na powitania [interfejsu API REST usługi ZenDesk](https://developer.zendesk.com/rest_api/docs/core/introduction#the-api), co jest dostępne tooZenDesk zespoły w planie niezbędne hello lub większą.

## <a name="assigning-users-toozendesk"></a>Przypisywanie użytkowników tooZenDesk

Azure Active Directory korzysta z koncepcji o nazwie "przypisania" toodetermine użytkowników, którzy mają otrzymywać aplikacje tooselected dostępu. W kontekście hello Inicjowanie obsługi konta użytkowników tylko hello użytkowników i grup, które zostały "przypisane" tooan aplikacji w usłudze Azure AD są synchronizowane. 

Przed Skonfiguruj i Włącz hello usługi inicjowania obsługi administracyjnej, należy toodecide jakie użytkowników i/lub grup w usłudze Azure AD reprezentują hello użytkowników, którzy muszą uzyskiwać dostęp do aplikacji usługi ZenDesk tooyour. Po decyzję, wykonując instrukcje hello w tym miejscu można przypisać tych użytkowników tooyour ZenDesk aplikacji:

[Przypisywanie użytkownikowi lub grupie aplikacji przedsiębiorstwa tooan](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-toozendesk"></a>Ważne porady dotyczące przypisywania tooZenDesk użytkowników

*   Zalecane jest jeden użytkownik usługi Azure AD jest przypisany hello tootest tooZenDesk inicjowania obsługi konfiguracji. Później można przypisać dodatkowych użytkowników i/lub grup.

*   Podczas przypisywania tooZenDesk użytkownika, należy wybrać albo hello **użytkownika** rola, lub inny prawidłowy specyficzne dla aplikacji (jeśli jest dostępny) w oknie dialogowym przydział hello. Witaj **domyślnego dostępu** roli nie działa w przypadku inicjowania obsługi administracyjnej, a użytkownicy są pomijane.

> [!NOTE]
> Dodano funkcję hello świadczenie usługi odczytuje wszystkie role niestandardowe zdefiniowane w Zendesk i zaimportowanie ich do usługi Azure AD, w którym można je wybrać w oknie dialogowym Wybierz rolę hello. Role te będą widoczne w hello portalu Azure po włączeniu hello usługi inicjowania obsługi administracyjnej i jednego cyklu synchronizacji zostało ukończone.

## <a name="configuring-user-provisioning-toozendesk"></a>Konfigurowanie inicjowania obsługi administracyjnej tooZenDesk użytkownika 

Ta sekcja przeprowadzi Cię przez łączenie inicjowania obsługi interfejsu API konta użytkownika tooZenDesk programu Azure AD i konfigurowanie hello inicjowania obsługi usługi toocreate, zaktualizować, a następnie wyłącz konta użytkowników przypisane w ZenDesk w oparciu o przypisania użytkowników i grup w usłudze Azure AD.

> [!TIP] 
> Można też tooenabled na języku SAML logowania jednokrotnego dla ZenDesk hello instrukcje podane w następujących [portalu Azure](https://portal.azure.com). Logowanie jednokrotne można skonfigurować niezależnie od automatycznego inicjowania obsługi administracyjnej, chociaż te dwie funkcje uzupełniania siebie nawzajem.


### <a name="configure-automatic-user-account-provisioning-toozendesk-in-azure-ad"></a>Skonfiguruj konto użytkownika automatycznego inicjowania obsługi administracyjnej tooZenDesk w usłudze Azure AD


1. W hello [portalu Azure](https://portal.azure.com), Przeglądaj toohello **usługi Azure Active Directory > aplikacje przedsiębiorstwa > wszystkie aplikacje** sekcji.

2. Jeśli skonfigurowano już program ZenDesk dla logowania jednokrotnego, wyszukiwanie wystąpienia programu ZenDesk przy użyciu pola wyszukiwania hello. W przeciwnym razie wybierz **Dodaj** i wyszukaj **ZenDesk** w galerii aplikacji hello. Wybierz ZenDesk z wyników wyszukiwania hello i dodać go tooyour listę aplikacji.

3. Wybierz wystąpienia programu ZenDesk, a następnie wybierz hello **inicjowania obsługi administracyjnej** kartę.

4. Zestaw hello **inicjowania obsługi trybu** za**automatyczne**.

    ![Inicjowanie obsługi usługi ZenDesk](./media/active-directory-saas-zendesk-provisioning-tutorial/ZenDesk1.png)

5. W obszarze hello **poświadczeń administratora** hello wejściowych, sekcji **administratora & tokenkey & domeny** generowane przez konto użytkownika usługi ZenDesk (przy użyciu tego konta można znaleźć tokenu hello: **administratora**   >  **Interfejsu API** > **ustawienia**). 

    ![Inicjowanie obsługi usługi ZenDesk](./media/active-directory-saas-zendesk-provisioning-tutorial/ZenDesk2.png)

6. W portalu Azure hello, kliknij przycisk **Testuj połączenie** tooensure usługi Azure AD można połączyć tooyour ZenDesk aplikację. Jeśli hello połączenia nie powiedzie się, upewnij się, że Twoje konto usługi ZenDesk ma uprawnienia administratora i spróbuj ponownie wykonać krok 5.

7. Wprowadź adres e-mail hello osoby lub grupy, które powinny być przesyłane powiadomienia błąd inicjowania obsługi administracyjnej w hello **wiadomość E-mail z powiadomieniem** pola i wyboru hello wyboru "Wyślij wiadomość e-mail z powiadomieniem, gdy wystąpi błąd."

8. Kliknij pozycję **Zapisz**. 

9. W obszarze hello sekcji mapowania, wybierz **tooZenDesk synchronizacji Azure Active Directory użytkowników**.

10. W hello **mapowań atrybutów** Przejrzyj hello atrybutów użytkowników, które są synchronizowane z usługą Azure AD tooZenDesk. Witaj atrybuty wybrany jako **pasujące** właściwości są używane toomatch hello kontom ZenDesk dla operacji update. Wybierz toocommit przycisk Zapisz hello wszelkie zmiany.

11. tooenable hello inicjowania obsługi usługi Azure AD dla usługi ZenDesk, zmień hello **stan inicjowania obsługi administracyjnej** za**na** w hello **ustawienia** sekcji

12. Kliknij pozycję **Zapisz**. 

Ta operacja spowoduje uruchomienie synchronizacji początkowej hello użytkowników i/lub grupy przypisane tooZenDesk w hello użytkowników i grup sekcji. Witaj początkowej synchronizacji ma tooperform dłużej niż kolejne synchronizacje, które występują co około 20 minut, tak długo, jak działa usługa hello. Można użyć hello **szczegóły synchronizacji** sekcji postępu toomonitor i wykonaj łącza tooprovisioning działania raporty, które opisują wszystkie działania wykonywane przez hello inicjowania obsługi usługi.

Aby uzyskać więcej informacji dotyczących sposobu inicjowania obsługi usługi Azure AD hello tooread logowania, zobacz [raportowania na użytkownika automatyczne Inicjowanie obsługi konta](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).


## <a name="additional-resources"></a>Dodatkowe zasoby

* [Zarządzanie aprowizacja konta użytkowników dla aplikacji przedsiębiorstwa](active-directory-enterprise-apps-manage-provisioning.md)
* [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md)

## <a name="next-steps"></a>Następne kroki

* [Dowiedz się, jak dzienniki tooreview i Uzyskaj raporty dotyczące inicjowania obsługi administracyjnej działania](active-directory-saas-provisioning-reporting.md)
