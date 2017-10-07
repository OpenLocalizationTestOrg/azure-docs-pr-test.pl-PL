---
title: 'Samouczek: Integracji Azure Active Directory z Citrix GoToMeeting | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Citrix GoToMeeting."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 0f59fedb-2cf8-48d2-a5fb-222ed943ff78
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 3c6eed5309dfa384c292b0cf63f8aa58988add81
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-citrix-gotomeeting-for-automatic-user-provisioning"></a>Samouczek: Konfigurowanie Citrix GoToMeeting dla użytkownika automatycznego inicjowania obsługi administracyjnej.

Celem Hello tego samouczka jest tooshow hello czynności, które należy tooperform w Citrix GoToMeeting i Azure AD tooautomatically udostępniania i usuwanie kont użytkowników z usługi Azure AD tooCitrix GoToMeeting.

## <a name="prerequisites"></a>Wymagania wstępne

Scenariusz Hello opisane w tym samouczku założono, że już hello następujące elementy:

*   Dzierżawy usługi Azure Active directory.
*   Citrix GoToMeeting jednokrotnego włączone subskrypcji.
*   Konto użytkownika w Citrix GoToMeeting z uprawnieniami administratora zespołu.

## <a name="assigning-users-toocitrix-gotomeeting"></a>Przypisywanie użytkowników tooCitrix GoToMeeting

Azure Active Directory korzysta z koncepcji o nazwie "przypisania" toodetermine użytkowników, którzy mają otrzymywać aplikacje tooselected dostępu. W kontekście hello Inicjowanie obsługi konta użytkowników tylko hello użytkowników i grup, które zostały "przypisane" tooan aplikacji w usłudze Azure AD jest zsynchronizowany.

Przed Skonfiguruj i Włącz hello usługi inicjowania obsługi administracyjnej, należy toodecide jakie użytkowników i/lub grup w usłudze Azure AD reprezentują hello użytkowników, którzy muszą korzystać tooyour Citrix GoToMeeting aplikacji. Po decyzję, można przypisać tooyour tych użytkowników aplikacji Citrix GoToMeeting, wykonując instrukcje hello tutaj:

[Przypisywanie użytkownikowi lub grupie aplikacji przedsiębiorstwa tooan](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-toocitrix-gotomeeting"></a>Ważne porady dotyczące przypisywania użytkowników tooCitrix GoToMeeting

*   Zalecane jest jeden użytkownik usługi Azure AD jest przypisany hello tootest GoToMeeting tooCitrix inicjowania obsługi konfiguracji. Później można przypisać dodatkowych użytkowników i/lub grup.

*   Podczas przypisywania tooCitrix użytkownika GoToMeeting, musisz wybrać poprawnej roli użytkownika. Rola "Domyślnego dostępu" Hello nie działa w przypadku inicjowania obsługi administracyjnej.

## <a name="enable-automated-user-provisioning"></a>Włącz automatyczne Inicjowanie obsługi użytkowników

Ta sekcja przeprowadzi Cię przez łączenie inicjowania obsługi interfejsu API konta użytkownika GoToMeeting tooCitrix usługi Azure AD i konfigurowanie hello inicjowania obsługi usługi toocreate, zaktualizować, a następnie wyłącz przypisany użytkownik kont w Citrix GoToMeeting opartych na użytkowników i grup przypisania w usłudze Azure AD.

> [!TIP]
> Można też tooenabled na języku SAML logowania jednokrotnego dla Citrix GoToMeeting, hello instrukcje podane w następujących [portalu Azure](https://portal.azure.com). Logowanie jednokrotne można skonfigurować niezależnie od automatycznego inicjowania obsługi administracyjnej, chociaż te dwie funkcje uzupełniania siebie nawzajem.

### <a name="tooconfigure-automatic-user-account-provisioning"></a>tooconfigure użytkownika automatyczne Inicjowanie obsługi konta:

1. W hello [portalu Azure](https://portal.azure.com), Przeglądaj toohello **usługi Azure Active Directory > aplikacje przedsiębiorstwa > wszystkie aplikacje** sekcji.

2. Citrix GoToMeeting został już skonfigurowany dla logowania jednokrotnego, wyszukaj wystąpienie usługi przy użyciu pola wyszukiwania hello Citrix GoToMeeting. W przeciwnym razie wybierz **Dodaj** i wyszukaj **Citrix GoToMeeting** w galerii aplikacji hello. Wybierz Citrix GoToMeeting z wyników wyszukiwania hello i dodać go tooyour listę aplikacji.

3. Wybierz wystąpienia programu Citrix GoToMeeting, a następnie wybierz hello **inicjowania obsługi administracyjnej** kartę.

4. Zestaw hello **inicjowania obsługi administracyjnej** tryb zbyt**automatyczne**. 

    ![Inicjowanie obsługi administracyjnej](./media/active-directory-saas-citrixgotomeeting-provisioning-tutorial/provisioning.png)

5. W obszarze hello sekcji poświadczenia administratora wykonaj hello następujące kroki:
   
    a. W hello **nazwa użytkownika administratora GoToMeeting Citrix** tekstowym, wpisz nazwę użytkownika hello administratora.

    b. W hello **hasło administratora GoToMeeting Citrix** pole tekstowe, hasło administratora hello.

6. W portalu Azure hello, kliknij przycisk **Testuj połączenie** tooensure usługi Azure AD mogą się łączyć tooyour Citrix GoToMeeting aplikacji. Jeśli hello połączenia nie powiedzie się, upewnij się, Twoje konto Citrix GoToMeeting ma uprawnienia administratora zespołu i spróbuj hello **"Poświadczeń administratora"** krok ponownie.

7. Wprowadź adres e-mail hello osoby lub grupy, które powinny być przesyłane powiadomienia błąd inicjowania obsługi administracyjnej w hello **wiadomość E-mail z powiadomieniem** pola, a następnie zaznacz pole wyboru hello.

8. Kliknij przycisk **zapisać.**

9. W obszarze hello sekcji mapowania, wybierz **tooCitrix synchronizacji Azure Active Directory użytkowników GoToMeeting.**

10. W hello **mapowań atrybutów** Przejrzyj hello atrybutów użytkowników, które są synchronizowane z usługą Azure AD tooCitrix GoToMeeting. Witaj atrybuty wybrany jako **pasujące** właściwości są używane toomatch hello kontom Citrix GoToMeeting dla operacji update. Wybierz toocommit przycisk Zapisz hello wszelkie zmiany.

11. tooenable hello inicjowania obsługi usługi Azure AD dla Citrix GoToMeeting, zmień hello **stan inicjowania obsługi administracyjnej** za**na** w sekcji Ustawienia hello

12. Kliknij przycisk **zapisać.**

Rozpoczyna hello wstępnej synchronizacji użytkowników i/lub grupy przypisane tooCitrix GoToMeeting w sekcji hello użytkowników i grup. Witaj początkowej synchronizacji ma tooperform dłużej niż kolejne synchronizacje, które występują co około 20 minut, tak długo, jak działa usługa hello. Można użyć hello **szczegóły synchronizacji** sekcji postępu toomonitor i wykonaj łącza tooprovisioning działania raporty, które opisują wszystkie działania wykonywane przez hello świadczenie usługi w aplikacji Citrix GoToMeeting.

## <a name="additional-resources"></a>Dodatkowe zasoby

* [Zarządzanie aprowizacja konta użytkowników dla aplikacji przedsiębiorstwa](active-directory-saas-tutorial-list.md)
* [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md)
* [Konfigurowanie rejestracji jednokrotnej](active-directory-saas-citrix-gotomeeting-tutorial.md)


