---
title: 'Samouczek: Integracji Azure Active Directory z polem | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i pola."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1c959595-6e57-4954-9c0d-67ba03ee212b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: e92baabb174642c22c99e2a30bc9c71845b3b75f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-box-for-automatic-user-provisioning"></a>Samouczek: Konfigurowanie pole dla użytkownika automatycznego inicjowania obsługi administracyjnej.

Celem Hello tego samouczka jest tooshow hello czynności, które należy tooperform w polu i Azure AD tooautomatically udostępniania i usuwanie kont użytkowników z tooBox usługi Azure AD.

## <a name="prerequisites"></a>Wymagania wstępne

Scenariusz Hello opisane w tym samouczku założono, że już hello następujące elementy:

*   Dzierżawy usługi Azure Active directory.
*   Pole jednokrotnego włączone subskrypcji.
*   Konto użytkownika, w polu z uprawnieniami administratora zespołu.

## <a name="assigning-users-toobox"></a>Przypisywanie użytkowników tooBox 

Azure Active Directory korzysta z koncepcji o nazwie "przypisania" toodetermine użytkowników, którzy mają otrzymywać aplikacje tooselected dostępu. W kontekście hello Inicjowanie obsługi konta użytkowników tylko hello użytkowników i grup, które zostały "przypisane" tooan aplikacji w usłudze Azure AD jest zsynchronizowany.

Przed Skonfiguruj i Włącz hello usługi inicjowania obsługi administracyjnej, należy toodecide jakie użytkowników i/lub grup w usłudze Azure AD reprezentują hello użytkowników, którzy muszą uzyskiwać dostęp do aplikacji Box tooyour. Po decyzję, wykonując następujące instrukcje hello można przypisać aplikacji Box tooyour tych użytkowników:

[Przypisywanie użytkownikowi lub grupie aplikacji przedsiębiorstwa tooan](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

## <a name="assign-users-and-groups"></a>Przypisywanie użytkowników i grup
Witaj **pole > Użytkownicy i grupy** kartę w portalu Azure hello umożliwia toospecify, którzy użytkownicy i grupy może być przyznany dostęp tooBox. Przypisanie użytkownika lub grupy powoduje powitania po toooccur rzeczy:

* Usługi Azure AD pozwala tooBox tooauthenticate użytkownika (za pomocą przypisania bezpośredniego lub członkostwa w grupie) hello przypisane. Jeśli użytkownik nie jest przypisany, usługi Azure AD nie zezwolić na ich toosign tooBox i zwraca błąd na stronie logowania w usłudze Azure AD hello.
* Kafelek aplikacji pole jest dodany użytkownik toohello [uruchamiający aplikację](active-directory-appssoaccess-whatis.md#deploying-azure-ad-integrated-applications-to-users).
* Jeśli włączono automatyczne udostępnianie następnie hello przypisanych użytkowników i grupy są dodawane toohello udostępniania kolejki toobe udostępniany automatycznie.
  
  * Jeśli tylko obiekty użytkownika zostały skonfigurowane toobe zainicjowano obsługę administracyjną, następnie wszystkie bezpośrednio przypisanych użytkowników są umieszczane w kolejce inicjowania obsługi administracyjnej hello i wszystkich użytkowników, którzy należą do żadnych przypisanych grup są umieszczane w hello udostępniania kolejki. 
  * Jeśli obiekty grupy zostały skonfigurowane toobe zainicjowano obsługę administracyjną, wszystkich obiektów grupy przypisanej są tooBox elastycznie i wszystkich użytkowników, którzy należą do tych grup. Witaj członkostwa grup i użytkowników są zachowywane podczas zapisywania tooBox.

Można użyć hello **atrybuty > logowanie jednokrotne** karcie tooconfigure, których atrybutów użytkownika (lub oświadczenia), są prezentowane tooBox podczas uwierzytelniania na podstawie SAML i hello **atrybuty > inicjowania obsługi administracyjnej** Karta tooconfigure jak przepływ atrybutów użytkowników i grup z usługi Azure AD tooBox podczas inicjowania obsługi operacji.

### <a name="important-tips-for-assigning-users-toobox"></a>Ważne porady dotyczące przypisywania tooBox użytkowników 

*   Zalecane jest pojedynczy usługi Azure AD hello tootest tooBox przypisane przez użytkownika inicjowania obsługi konfiguracji. Później można przypisać dodatkowych użytkowników i/lub grup.

*   Podczas przypisywania toobox użytkownika, należy wybrać poprawnej roli użytkownika. Rola "Domyślnego dostępu" Hello nie działa w przypadku inicjowania obsługi administracyjnej.

## <a name="enable-automated-user-provisioning"></a>Włącz automatyczne Inicjowanie obsługi użytkowników

Ta sekcja przeprowadzi łączenie inicjowania obsługi interfejsu API konta użytkownika tooBox programu Azure AD i konfigurowanie hello inicjowania obsługi usługi toocreate, zaktualizować, a następnie wyłącz konta użytkowników przypisane w oparciu o przypisania użytkowników i grup w usłudze Azure AD.

Jeśli włączono automatyczne udostępnianie następnie hello przypisanych użytkowników i grupy są dodawane toohello udostępniania kolejki toobe udostępniany automatycznie.
    
 * Jeśli tylko obiekty użytkownika są skonfigurowane toobe udostępniane, a następnie bezpośrednio przypisanych użytkowników są umieszczane w kolejce inicjowania obsługi administracyjnej hello i wszystkich użytkowników, którzy należą do żadnych przypisanych grup są umieszczane w hello udostępniania kolejki. 
    
 * Jeśli obiekty grupy zostały skonfigurowane toobe zainicjowano obsługę administracyjną, wszystkich obiektów grupy przypisanej są tooBox elastycznie i wszystkich użytkowników, którzy należą do tych grup. Witaj członkostwa grup i użytkowników są zachowywane podczas zapisywania tooBox.

> [!TIP] 
> Można też tooenabled na języku SAML rejestracji jednokrotnej dla pola hello instrukcje podane w następujących [portalu Azure](https://portal.azure.com). Logowanie jednokrotne można skonfigurować niezależnie od automatycznego inicjowania obsługi administracyjnej, chociaż te dwie funkcje uzupełniania siebie nawzajem.

### <a name="tooconfigure-automatic-user-account-provisioning"></a>tooconfigure użytkownika automatyczne Inicjowanie obsługi konta:

Celem Hello w tej sekcji jest toooutline jak tooBox kont tooenable Inicjowanie obsługi administracyjnej użytkownika usługi Active Directory.

1. W hello [portalu Azure](https://portal.azure.com), Przeglądaj toohello **usługi Azure Active Directory > aplikacje przedsiębiorstwa > wszystkie aplikacje** sekcji.

2. Jeśli pole został już skonfigurowany dla logowania jednokrotnego, wyszukiwanie wystąpienia pola przy użyciu pola wyszukiwania hello. W przeciwnym razie wybierz **Dodaj** i wyszukaj **pole** w galerii aplikacji hello. Zaznacz pole z hello wyniki wyszukiwania i dodaj go tooyour listy aplikacji.

3. Wybierz wystąpienia pola, a następnie wybierz hello **inicjowania obsługi administracyjnej** kartę.

4. Zestaw hello **inicjowania obsługi trybu** za**automatyczne**. 

    ![Inicjowanie obsługi administracyjnej](./media/active-directory-saas-box-userprovisioning-tutorial/provisioning.png)

5. W obszarze hello **poświadczeń administratora** kliknij **autoryzacji** tooopen okno dialogowe logowania pola w nowym oknie przeglądarki.

6. Na powitania **logowania toogrant dostępu tooBox** hello wymagane poświadczenia, a następnie kliknij przycisk **autoryzacji**. 
   
    ![Włącz inicjowanie obsługi użytkowników](./media/active-directory-saas-box-userprovisioning-tutorial/IC769546.png "Włącz inicjowanie obsługi użytkowników")

7. Kliknij przycisk **Udziel dostępu tooBox** tooauthorize tej operacji i tooreturn toohello portalu Azure. 
   
    ![Włącz inicjowanie obsługi użytkowników](./media/active-directory-saas-box-userprovisioning-tutorial/IC769549.png "Włącz inicjowanie obsługi użytkowników")

8. W portalu Azure hello, kliknij przycisk **Testuj połączenie** tooensure usługi Azure AD można połączyć tooyour okno aplikacji. Jeśli hello połączenia nie powiedzie się, upewnij się, Twoje konto pole ma uprawnienia administratora zespołu i spróbuj hello **"Autoryzuj"** krok ponownie.

9. Wprowadź adres e-mail hello osoby lub grupy, które powinny być przesyłane powiadomienia błąd inicjowania obsługi administracyjnej w hello **wiadomość E-mail z powiadomieniem** pola, a następnie zaznacz pole wyboru hello.

10. Kliknij przycisk **zapisać.**

11. W obszarze hello sekcji mapowania, wybierz **tooBox synchronizacji Azure Active Directory użytkowników.**

12. W hello **mapowań atrybutów** Przejrzyj hello atrybutów użytkowników, które są synchronizowane z usługą Azure AD tooBox. Witaj atrybuty wybrany jako **pasujące** właściwości są używane toomatch hello konta w polu operacje aktualizacji. Wybierz toocommit przycisk Zapisz hello wszelkie zmiany.

13. tooenable hello inicjowania obsługi usługi Azure AD dla pola, zmień hello **stan inicjowania obsługi administracyjnej** za**na** w sekcji Ustawienia hello

14. Kliknij przycisk **zapisać.**

Zaczynającym się hello wstępnej synchronizacji użytkowników i/lub grupy przypisane tooBox w hello użytkowników i grup sekcji. Witaj początkowej synchronizacji ma tooperform dłużej niż kolejne synchronizacje, które występują co około 20 minut, tak długo, jak działa usługa hello. Można użyć hello **szczegóły synchronizacji** sekcji postępu toomonitor i wykonaj łącza tooprovisioning działania raporty, które opisują wszystkie akcje wykonywane przez hello świadczenie usługi w polu aplikacji.

Można teraz utworzyć konta testowego. Poczekaj na górę minut too20 tooverify, który hello konto zostało zsynchronizowane toobox.

W tej dzierżawie pole zsynchronizowanych użytkowników są wyświetlane w obszarze **użytkowników zarządzanych** w hello **konsoli administracyjnej**.

![Stan integracji](./media/active-directory-saas-box-userprovisioning-tutorial/IC769556.png "stan integracji")


## <a name="additional-resources"></a>Dodatkowe zasoby

* [Zarządzanie aprowizacja konta użytkowników dla aplikacji przedsiębiorstwa](active-directory-saas-tutorial-list.md)
* [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md)
* [Konfigurowanie rejestracji jednokrotnej](active-directory-saas-box-tutorial.md)