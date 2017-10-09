---
title: 'Samouczek: Integracji Azure Active Directory z Jive | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Jive."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 6fbfdbe7-d66c-4305-9fea-76d6a6a92830
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: b1c0d0bc2d79427c055f577fe5f9d30d10f1bbdd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-jive-for-user-provisioning"></a>Samouczek: Konfigurowanie Jive Inicjowanie obsługi użytkowników

Celem Hello tego samouczka jest tooshow hello czynności, które należy tooperform w Jive i Azure AD tooautomatically udostępniania i usuwanie kont użytkowników z usługi Azure AD tooJive.

## <a name="prerequisites"></a>Wymagania wstępne

Scenariusz Hello opisane w tym samouczku założono, że już hello następujące elementy:

*   Dzierżawy usługi Azure Active directory.
*   Jive jednokrotnego włączone subskrypcji.
*   Konto użytkownika w Jive z uprawnieniami administratora zespołu.

## <a name="assigning-users-toojive"></a>Przypisywanie użytkowników tooJive

Azure Active Directory korzysta z koncepcji o nazwie "przypisania" toodetermine użytkowników, którzy mają otrzymywać aplikacje tooselected dostępu. W kontekście hello Inicjowanie obsługi konta użytkowników tylko hello użytkowników i grup, które zostały "przypisane" tooan aplikacji w usłudze Azure AD jest zsynchronizowany.

Przed Skonfiguruj i Włącz hello usługi inicjowania obsługi administracyjnej, należy toodecide jakie użytkowników i/lub grup w usłudze Azure AD reprezentują hello użytkowników, którzy wymagają dostępu tooyour Jive aplikacji. Po decyzję, wykonując instrukcje hello w tym miejscu można przypisać tych użytkowników tooyour Jive aplikacji:

[Przypisywanie użytkownikowi lub grupie aplikacji przedsiębiorstwa tooan](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-toojive"></a>Ważne porady dotyczące przypisywania tooJive użytkowników

*   Zalecane jest pojedynczego użytkownika usługi Azure AD można przypisać hello tootest tooJive inicjowania obsługi konfiguracji. Później można przypisać dodatkowych użytkowników i/lub grup.

*   Podczas przypisywania tooJive użytkownika, należy wybrać poprawnej roli użytkownika. Rola "Domyślnego dostępu" Hello nie działa w przypadku inicjowania obsługi administracyjnej.

## <a name="enable-user-provisioning"></a>Włącz inicjowanie obsługi użytkowników

Ta sekcja przeprowadzi Cię przez łączenie inicjowania obsługi interfejsu API konta użytkownika tooJive programu Azure AD i konfigurowanie hello inicjowania obsługi usługi toocreate, zaktualizować, a następnie wyłącz konta użytkowników przypisane w Jive w oparciu o przypisania użytkowników i grup w usłudze Azure AD.

> [!TIP]
> Można też tooenabled na języku SAML rejestracji jednokrotnej dla Jive hello instrukcje podane w następujących [portalu Azure](https://portal.azure.com). Logowanie jednokrotne można skonfigurować niezależnie od automatycznego inicjowania obsługi administracyjnej, chociaż te dwie funkcje uzupełniania siebie nawzajem.

### <a name="tooconfigure-user-account-provisioning"></a>Przypisywanie konta użytkowników tooconfigure:

Celem Hello w tej sekcji jest toooutline jak tooJive kont tooenable użytkownika usługi Active Directory Inicjowanie obsługi użytkowników.
W ramach tej procedury jest wymagana tooprovide należy toorequest z Jive.com token zabezpieczeń użytkownika.

1. W hello [portalu Azure](https://portal.azure.com), Przeglądaj toohello **usługi Azure Active Directory > aplikacje przedsiębiorstwa > wszystkie aplikacje** sekcji.

2. Jive został już skonfigurowany dla logowania jednokrotnego, wyszukaj wystąpieniem Jive za pomocą hello pola wyszukiwania. W przeciwnym razie wybierz **Dodaj** i wyszukaj **Jive** w galerii aplikacji hello. Wybierz Jive z wyników wyszukiwania hello i dodać go tooyour listy aplikacji.

3. Wybierz wystąpienia programu Jive, a następnie wybierz hello **inicjowania obsługi administracyjnej** kartę.

4. Zestaw hello **inicjowania obsługi trybu** za**automatyczne**. 

    ![Inicjowanie obsługi administracyjnej](./media/active-directory-saas-jive-provisioning-tutorial/provisioning.png)

5. W obszarze hello **poświadczeń administratora** sekcji, podaj hello następujące ustawienia konfiguracji:
   
    a. W hello **nazwa użytkownika administratora Jive** tekstowym, wpisz nazwę, która ma hello konta Jive **administratorem** profil Jive.com przypisane.
   
    b. W hello **hasło administratora Jive** tekstowym, wpisz hello hasło dla tego konta.
   
    c. W hello **adres URL dzierżawy Jive** pole tekstowe, typ hello Jive — adres URL dzierżawy.
      
      > [!NOTE]
      > adres URL dzierżawy Jive Hello jest adres URL, który jest używany przez toolog Twojej organizacji w tooJive.  
      > Zwykle adres URL hello ma hello następującego formatu: **www.\< Organizacja\>. jive.com**.          

6. W portalu Azure hello, kliknij przycisk **Testuj połączenie** tooensure usługi Azure AD można połączyć tooyour Jive aplikację.

7. Wprowadź adres e-mail hello osoby lub grupy, które powinny być przesyłane powiadomienia błąd inicjowania obsługi administracyjnej w hello **wiadomość E-mail z powiadomieniem** pola i zaznacz pole wyboru hello poniżej.

8. Kliknij przycisk **zapisać.**

9. W obszarze hello sekcji mapowania, wybierz **tooJive synchronizacji Azure Active Directory użytkowników.**

10. W hello **mapowań atrybutów** Przejrzyj hello atrybutów użytkowników, które są synchronizowane z usługą Azure AD tooJive. Witaj atrybuty wybrany jako **pasujące** właściwości są używane toomatch hello kontom Jive dla operacji update. Wybierz toocommit przycisk Zapisz hello wszelkie zmiany.

11. tooenable hello inicjowania obsługi usługi Azure AD dla Jive, zmień hello **stan inicjowania obsługi administracyjnej** za**na** w sekcji Ustawienia hello

12. Kliknij przycisk **zapisać.**

Rozpoczyna się hello wstępnej synchronizacji użytkowników i/lub grupy przypisane tooJive w hello użytkowników i grup sekcji. Witaj początkowej synchronizacji ma tooperform dłużej niż kolejne synchronizacje, które występują co około 20 minut, tak długo, jak działa usługa hello. Można użyć hello **szczegóły synchronizacji** sekcji postępu toomonitor i wykonaj łącza tooprovisioning działania raporty, które opisują wszystkie działania wykonywane przez hello usługi w aplikacji Jive inicjowania obsługi administracyjnej.

Można teraz utworzyć konta testowego. Poczekaj na górę minut too20 tooverify, który hello konto zostało zsynchronizowane tooJive.

## <a name="additional-resources"></a>Dodatkowe zasoby

* [Zarządzanie aprowizacja konta użytkowników dla aplikacji przedsiębiorstwa](active-directory-saas-tutorial-list.md)
* [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md)
* [Konfigurowanie rejestracji jednokrotnej](active-directory-saas-jive-tutorial.md)