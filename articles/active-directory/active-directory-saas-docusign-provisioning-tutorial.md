---
title: 'Samouczek: Integracji Azure Active Directory z DocuSign | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i DocuSign."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 294cd6b8-74d7-44bc-92bc-020ccd13ff12
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: jeedes
ms.openlocfilehash: 8562a8f9e05fb72d3331507b7da5c6afee38f9b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-docusign-for-user-provisioning"></a>Samouczek: Konfigurowanie DocuSign Inicjowanie obsługi użytkowników

Celem Hello tego samouczka jest tooshow hello czynności, które należy tooperform w DocuSign i Azure AD tooautomatically udostępniania i usuwanie kont użytkowników z usługi Azure AD tooDocuSign.

## <a name="prerequisites"></a>Wymagania wstępne

Scenariusz Hello opisane w tym samouczku założono, że już hello następujące elementy:

*   Dzierżawy usługi Azure Active directory.
*   DocuSign logowanie jednokrotne włączone subskrypcji.
*   Konto użytkownika w DocuSign z uprawnieniami administratora zespołu.

## <a name="assigning-users-toodocusign"></a>Przypisywanie użytkowników tooDocuSign

Azure Active Directory korzysta z koncepcji o nazwie "przypisania" toodetermine użytkowników, którzy mają otrzymywać aplikacje tooselected dostępu. W kontekście hello Inicjowanie obsługi konta użytkowników tylko hello użytkowników i grup, które zostały "przypisane" tooan aplikacji w usłudze Azure AD są synchronizowane.

Przed Skonfiguruj i Włącz hello usługi inicjowania obsługi administracyjnej, należy toodecide jakie użytkowników i/lub grup w usłudze Azure AD reprezentują hello użytkowników, którzy muszą uzyskiwać dostęp do aplikacji DocuSign tooyour. Po decyzję, wykonując instrukcje hello w tym miejscu można przypisać tych użytkowników tooyour DocuSign aplikacji:

[Przypisywanie użytkownikowi lub grupie aplikacji przedsiębiorstwa tooan](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-toodocusign"></a>Ważne porady dotyczące przypisywania tooDocuSign użytkowników

*   Zalecane jest jeden użytkownik usługi Azure AD jest przypisany hello tootest tooDocuSign inicjowania obsługi konfiguracji. Później można przypisać dodatkowych użytkowników i/lub grup.

*   Podczas przypisywania tooDocuSign użytkownika, należy wybrać poprawnej roli użytkownika. Rola "Domyślnego dostępu" Hello nie działa w przypadku inicjowania obsługi administracyjnej.

## <a name="enable-user-provisioning"></a>Włącz inicjowanie obsługi użytkowników

Ta sekcja przeprowadzi Cię przez łączenie inicjowania obsługi interfejsu API konta użytkownika tooDocuSign programu Azure AD i konfigurowanie hello inicjowania obsługi usługi toocreate, zaktualizować, a następnie wyłącz konta użytkowników przypisane w DocuSign w oparciu o przypisania użytkowników i grup w usłudze Azure AD.

> [!Tip]
> Można też tooenabled na języku SAML logowania jednokrotnego dla DocuSign hello instrukcje podane w następujących [portalu Azure](https://portal.azure.com). Logowanie jednokrotne można skonfigurować niezależnie od automatycznego inicjowania obsługi administracyjnej, chociaż te dwie funkcje uzupełniania siebie nawzajem.

### <a name="tooconfigure-user-account-provisioning"></a>Przypisywanie konta użytkowników tooconfigure:

Celem Hello w tej sekcji jest toooutline jak tooDocuSign kont tooenable użytkownika usługi Active Directory Inicjowanie obsługi użytkowników.

1. W hello [portalu Azure](https://portal.azure.com), Przeglądaj toohello **usługi Azure Active Directory > aplikacje przedsiębiorstwa > wszystkie aplikacje** sekcji.

2. DocuSign został już skonfigurowany dla logowania jednokrotnego, wyszukaj wystąpieniem DocuSign za pomocą hello pola wyszukiwania. W przeciwnym razie wybierz **Dodaj** i wyszukaj **DocuSign** w galerii aplikacji hello. Wybierz DocuSign z wyników wyszukiwania hello i dodać go tooyour listy aplikacji.

3. Wybierz wystąpienia programu DocuSign, a następnie wybierz hello **inicjowania obsługi administracyjnej** kartę.

4. Zestaw hello **inicjowania obsługi trybu** za**automatyczne**. 

    ![Inicjowanie obsługi administracyjnej](./media/active-directory-saas-docusign-provisioning-tutorial/provisioning.png)

5. W obszarze hello **poświadczeń administratora** sekcji, podaj hello następujące ustawienia konfiguracji:
   
    a. W hello **nazwa użytkownika administratora** tekstowym, wpisz nazwę, która ma hello konta DocuSign **administratorem** profil DocuSign.com przypisane.
   
    b. W hello **hasło administratora** tekstowym, wpisz hello hasło dla tego konta.

6. W portalu Azure hello, kliknij przycisk **Testuj połączenie** tooensure usługi Azure AD można połączyć tooyour DocuSign aplikację.

7. W hello **wiadomość E-mail z powiadomieniem** wprowadź hello adres e-mail osoby lub grupy, który powinien otrzymywać powiadomienia błąd inicjowania obsługi administracyjnej i zaznacz pole wyboru hello.

8. Kliknij przycisk **zapisać.**

9. W obszarze hello sekcji mapowania, wybierz **tooDocuSign synchronizacji Azure Active Directory użytkowników.**

10. W hello **mapowań atrybutów** Przejrzyj hello atrybutów użytkowników, które są synchronizowane z usługą Azure AD tooDocuSign. Witaj atrybuty wybrany jako **pasujące** właściwości są używane toomatch hello kontom DocuSign dla operacji update. Wybierz toocommit przycisk Zapisz hello wszelkie zmiany.

11. tooenable hello inicjowania obsługi usługi Azure AD dla DocuSign, zmień hello **stan inicjowania obsługi administracyjnej** za**na** w sekcji Ustawienia hello

12. Kliknij przycisk **zapisać.**

Rozpoczyna się hello wstępnej synchronizacji użytkowników i/lub grupy przypisane tooDocuSign w hello użytkowników i grup sekcji. Witaj początkowej synchronizacji ma tooperform dłużej niż kolejne synchronizacje, które występują co około 20 minut, tak długo, jak działa usługa hello. Można użyć hello **szczegóły synchronizacji** sekcji postępu toomonitor i wykonaj łącza tooprovisioning działania raporty, które opisują wszystkie działania wykonywane przez hello usługi w aplikacji DocuSign inicjowania obsługi administracyjnej.

Można teraz utworzyć konta testowego. Poczekaj na górę minut too20 tooverify, który hello konto zostało zsynchronizowane tooDocuSign.

## <a name="additional-resources"></a>Dodatkowe zasoby

* [Zarządzanie aprowizacja konta użytkowników dla aplikacji przedsiębiorstwa](active-directory-saas-tutorial-list.md)
* [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md)
* [Konfigurowanie rejestracji jednokrotnej](active-directory-saas-docusign-tutorial.md)