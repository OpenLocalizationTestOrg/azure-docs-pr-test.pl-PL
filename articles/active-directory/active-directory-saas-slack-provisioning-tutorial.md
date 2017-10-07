---
title: "Samouczek: Konfigurowanie zapas czasu dla użytkownika automatycznego inicjowania obsługi administracyjnej z usługą Azure Active Directory | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak konta tooSlack tooconfigure usługi Azure Active Directory tooautomatically udostępniania i usuwanie użytkowników."
services: active-directory
documentationcenter: 
author: asmalser-msft
writer: asmalser-msft
manager: sakula
ms.assetid: d4ca2365-6729-48f7-bb7f-c0f5ffe740a3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: asmalser-msft
ms.reviewer: asmalser
ms.openlocfilehash: d0a565bbe0bd7e229b9dd99b1ebbaf67d93a2206
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-slack-for-automatic-user-provisioning"></a>Samouczek: Konfigurowanie zapas czasu dla użytkownika automatycznego inicjowania obsługi administracyjnej.


Witaj celem tego samouczka jest tooshow hello czynności, które należy tooperform zapas czasu i Azure AD tooautomatically udostępniania i usuwanie kont użytkowników z usługi Azure AD tooSlack. 

## <a name="prerequisites"></a>Wymagania wstępne

Scenariusz Hello opisane w tym samouczku założono, że już hello następujące elementy:

*   Dzierżawy usługi Azure Active Active directory
*   Zapas czasu dzierżawy z hello [Plus planu](https://aadsyncfabric.slack.com/pricing) lub lepiej jest włączone 
*   Konto użytkownika w zapas czasu z uprawnieniami administratora zespołu 

Uwaga: hello Azure AD inicjowania obsługi administracyjnej integracji opiera się na powitania [API SCIM zapas czasu](https://api.slack.com/scim) czyli zespoły tooSlack dostępne na powitania Plus planu lub większą.

## <a name="assigning-users-tooslack"></a>Przypisywanie użytkowników tooSlack

Azure Active Directory korzysta z koncepcji o nazwie "przypisania" toodetermine użytkowników, którzy mają otrzymywać aplikacje tooselected dostępu. W kontekście hello Inicjowanie obsługi konta użytkowników tylko hello użytkowników i grup, które zostały "przypisane" tooan aplikacji w usłudze Azure AD będą synchronizowane. 

Przed Skonfiguruj i Włącz hello inicjowania obsługi usługi, konieczne będzie toodecide jakie użytkowników i/lub grup w usłudze Azure AD reprezentują hello użytkowników, którzy muszą uzyskiwać dostęp do aplikacji Slack tooyour. Po decyzję, wykonując instrukcje hello w tym miejscu można przypisać tych użytkowników tooyour Slack aplikacji:

[Przypisywanie użytkownikowi lub grupie aplikacji przedsiębiorstwa tooan](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-tooslack"></a>Ważne porady dotyczące przypisywania tooSlack użytkowników

*   Zalecane jest pojedynczego użytkownika usługi Azure AD można przypisać hello tootest tooSlack inicjowania obsługi konfiguracji. Później można przypisać dodatkowych użytkowników i/lub grup.

*   Podczas przypisywania tooSlack użytkownika, należy wybrać hello **użytkownika** lub rola "Grupy" w oknie dialogowym przydział hello. Rola "Domyślnego dostępu" Hello nie działa w przypadku inicjowania obsługi administracyjnej.


## <a name="configuring-user-provisioning-tooslack"></a>Konfigurowanie inicjowania obsługi administracyjnej tooSlack użytkownika 

Ta sekcja przeprowadzi Cię przez łączenie inicjowania obsługi interfejsu API konta użytkownika tooSlack programu Azure AD i konfigurowanie hello inicjowania obsługi administracyjnej toocreate usługi, zaktualizuj i wyłączenie konta użytkowników przypisane w zapas czasu, w oparciu o przypisania użytkowników i grup w usłudze Azure AD.

**Porada:** można też tooenabled na języku SAML rejestracji jednokrotnej dla zapas czasu, zgodnie z instrukcjami hello (Azure portal) [https://portal.azure.com]. Logowanie jednokrotne można skonfigurować niezależnie od automatycznego inicjowania obsługi administracyjnej, chociaż te dwie funkcje uzupełniania siebie nawzajem.


### <a name="tooconfigure-automatic-user-account-provisioning-tooslack-in-azure-ad"></a>konto użytkownika automatyczne tooconfigure udostępniania tooSlack w usłudze Azure AD:


1)  W hello [portalu Azure](https://portal.azure.com), Przeglądaj toohello **usługi Azure Active Directory > aplikacje przedsiębiorstwa > wszystkie aplikacje** sekcji.

2) Zapas czasu został już skonfigurowany dla logowania jednokrotnego, wyszukaj wystąpienie usługi przy użyciu pola wyszukiwania hello zapas czasu. W przeciwnym razie wybierz **Dodaj** i wyszukaj **Slack** w galerii aplikacji hello. Wybierz zapas czasu z wyników wyszukiwania hello i dodać go tooyour listy aplikacji.

3)  Wybierz wystąpienia programu zapas czasu, a następnie wybierz hello **inicjowania obsługi administracyjnej** kartę.

4)  Zestaw hello **inicjowania obsługi trybu** za**automatyczne**.

![Zapas czasu obsługi](./media/active-directory-saas-slack-provisioning-tutorial/Slack1.PNG)

5)  W obszarze hello **poświadczeń administratora** kliknij **autoryzacji**. Spowoduje to otwarcie okna dialogowego Slack autoryzacji w nowym oknie przeglądarki. 

6) W nowym oknie hello Zaloguj się do zapas czasu przy użyciu konta administratora zespołu. w hello wynikowy autoryzacji oknie dialogowym Wybierz hello Slack zespół, który ma tooenable Inicjowanie obsługi, a następnie wybierz **autoryzacji**. Inicjowanie obsługi konfiguracji hello toocomplete portalu Azure po zakończeniu, zwróć toohello.

![Okno dialogowe autoryzacji](./media/active-directory-saas-slack-provisioning-tutorial/Slack3.PNG)

7) W portalu Azure hello, kliknij przycisk **Testuj połączenie** tooensure usługi Azure AD można połączyć aplikację Slack tooyour. Jeśli hello połączenia nie powiedzie się, upewnij się, że Slack konto ma uprawnienia administratora zespołu i spróbuj hello "Autoryzuj" krok ponownie.

8) Wprowadź adres e-mail hello osoby lub grupy, które powinny być przesyłane powiadomienia błąd inicjowania obsługi administracyjnej w hello **wiadomość E-mail z powiadomieniem** pola i zaznacz pole wyboru hello poniżej.

9) Kliknij pozycję **Zapisz**. 

10) W obszarze hello sekcji mapowania, wybierz **tooSlack synchronizacji Azure Active Directory użytkowników**.

11) W hello **mapowań atrybutów** Przejrzyj hello atrybutów użytkowników, które są synchronizowane z usługą Azure AD tooSlack. Należy pamiętać, że wybrany jako atrybuty hello **pasujące** właściwości będzie używane toomatch hello kontom zapas czasu dla operacji update. Wybierz toocommit przycisk Zapisz hello wszelkie zmiany.

12) tooenable hello inicjowania obsługi usługi Azure AD dla zapas czasu, zmień hello **stan inicjowania obsługi administracyjnej** za**na** w hello **ustawienia** sekcji

13) Kliknij pozycję **Zapisz**. 

Spowoduje to uruchomienie synchronizacji początkowej hello użytkowników i/lub grupy przypisane tooSlack w hello użytkowników i grup sekcji. Należy pamiętać, że synchronizacji początkowej hello potrwa tooperform dłużej niż kolejne synchronizacje, które występują co 10 minut, tak długo, jak działa usługa hello. Można użyć hello **szczegóły synchronizacji** sekcji postępu toomonitor i wykonaj łącza tooprovisioning działania raporty, które opisują wszystkie akcje wykonywane przez hello świadczenie usługi na Slack aplikacji.

## <a name="optional-configuring-group-object-provisioning-tooslack"></a>[Opcjonalnie] Konfigurowanie inicjowania obsługi administracyjnej tooSlack obiektu grupy 

Opcjonalnie można włączyć hello udostępnianie obiektów grupy z tooSlack usługi Azure AD. To jest inny niż "przypisanie grupy użytkowników", w tym obiekcie rzeczywiste grupy hello dodatkowo tooits elementy członkowskie będą replikowane z tooSlack usługi Azure AD. Na przykład jeśli istnieje grupa o nazwie "My" w usłudze Azure AD, wewnątrz zapas czasu zostanie utworzona grupa identitical o nazwie "My".

### <a name="tooenable-provisioning-of-group-objects"></a>obiekty grupy tooenable inicjowania obsługi administracyjnej:

1) W obszarze hello sekcji mapowania, wybierz **tooSlack synchronizacji Azure Active Directory grup**.

2) W bloku atrybutu mapowania hello ustawić tooYes włączone.

3) W hello **mapowań atrybutów** Przejrzyj hello grupy atrybutów, które są synchronizowane z usługą Azure AD tooSlack. Należy pamiętać, że wybrany jako atrybuty hello **pasujące** właściwości zostaną grup hello toomatch używanych w zapas czasu dla operacji update. 

4) Kliknij pozycję **Zapisz**.

Ten wynik w dowolnej grupy tooSlack przypisane obiekty w hello **użytkowników i grup** sekcji pełni synchronizowane z usługą Azure AD tooSlack. Można użyć hello **szczegóły synchronizacji** sekcji postępu toomonitor i wykonaj łącza tooprovisioning działania raporty, które opisują wszystkie akcje wykonywane przez hello świadczenie usługi na Slack aplikacji.


## <a name="additional-resources"></a>Dodatkowe zasoby

* [Zarządzanie aprowizacja konta użytkowników dla aplikacji przedsiębiorstwa](active-directory-enterprise-apps-manage-provisioning.md)
* [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md)
