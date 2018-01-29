---
title: 'Samouczek: Integracji Azure Active Directory z polem | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i pola."
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 1c959595-6e57-4954-9c0d-67ba03ee212b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 0f13fa47ef8eacd822f5744b9dde2bb1f0f2909f
ms.sourcegitcommit: e266df9f97d04acfc4a843770fadfd8edf4fa2b7
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/11/2017
---
# <a name="tutorial-configuring-box-for-automatic-user-provisioning"></a>Samouczek: Konfigurowanie pole dla użytkownika automatycznego inicjowania obsługi administracyjnej.

Celem tego samouczka jest do pokazania kroki, które należy wykonać w polu a usługą Azure AD można automatycznie udostępnić i usuwanie kont użytkowników z usługi Azure AD do pola.

## <a name="prerequisites"></a>Wymagania wstępne

Scenariusz opisany w tym samouczku założono, że już następujące elementy:

*   Dzierżawy usługi Azure Active directory.
*   Pole jednokrotnego włączone subskrypcji.
*   Konto użytkownika, w polu z uprawnieniami administratora zespołu.

## <a name="assigning-users-to-box"></a>Przypisywanie użytkowników do pola 

Usługi Azure Active Directory używa pojęcie o nazwie "przypisania" w celu określenia, którzy użytkownicy powinien otrzymać dostęp do wybranej aplikacji. W kontekście użytkownika automatyczne Inicjowanie obsługi konta tylko użytkownicy i grupy, które "przypisano" do aplikacji w usłudze Azure AD jest zsynchronizowany.

Przed Skonfiguruj i włącz usługę inicjowania obsługi administracyjnej, należy zdecydować, jaki użytkowników i/lub grup w usłudze Azure AD reprezentują użytkowników, którzy potrzebują dostępu do aplikacji pole. Po decyzję, postępując zgodnie z instrukcjami w tym miejscu można przypisać tych użytkowników do aplikacji pola:

[Przypisanie użytkownika lub grupę do aplikacji w przedsiębiorstwie](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

## <a name="assign-users-and-groups"></a>Przypisywanie użytkowników i grup
**Pole > Użytkownicy i grupy** kartę w portalu Azure umożliwia określenie, którzy użytkownicy i grupy może być przyznany dostęp do pola. Przypisanie użytkownika lub grupy powoduje, że występuje następujących czynności:

* Usługi Azure AD pozwala przypisany użytkownik (albo przez bezpośrednie przypisanie lub członkostwa w grupie) do uwierzytelniania do pola. Jeśli użytkownik nie jest przypisany, usługi Azure AD nie zezwala na je, aby zalogować się do pola i zwraca błąd na stronie logowania w usłudze Azure AD.
* Do użytkownika zostanie dodany Kafelek aplikacji dla pola [uruchamiający aplikację](active-directory-appssoaccess-whatis.md#deploying-azure-ad-integrated-applications-to-users).
* Jeśli włączono automatyczne udostępnianie przypisanych użytkowników i/lub grup są dodawane do inicjowania obsługi administracyjnej kolejki, aby automatycznie udostępniane.
  
  * Jeśli tylko obiekty użytkownika zostały skonfigurowane do obsługi administracyjnej, następnie wszystkie bezpośrednio przypisanych użytkowników są umieszczane w kolejce inicjowania obsługi administracyjnej i wszystkich użytkowników, którzy należą do żadnych przypisanych grup są umieszczane w kolejce inicjowania obsługi administracyjnej. 
  * Jeśli obiekty grupy zostały skonfigurowane do obsługi administracyjnej, wszystkich obiektów grupy przypisanej są udostępniane pól oraz wszystkich użytkowników, którzy należą do tych grup. Członkostwo grup i użytkowników są zachowywane podczas zapisywania do pola.

Można użyć **atrybuty > logowanie jednokrotne** kartę, aby skonfigurować, których atrybutów użytkownika (lub oświadczenia) są dostarczane do pola przy uwierzytelnianie SAML i **atrybuty > inicjowania obsługi administracyjnej** karty, aby Skonfiguruj sposób użytkowników i grup przepływ atrybutów z usługi Azure AD do pola podczas inicjowania obsługi operacji.

### <a name="important-tips-for-assigning-users-to-box"></a>Ważne porady dotyczące przypisywania użytkowników do pola 

*   Zalecane jest jeden przypisany do pola do testowania konfiguracji inicjowania obsługi administracyjnej użytkowników usługi Azure AD. Później można przypisać dodatkowych użytkowników i/lub grup.

*   Przypisanie użytkownika do pola, musisz wybrać poprawnej roli użytkownika. Rola "Domyślnego dostępu" nie działa w przypadku inicjowania obsługi administracyjnej.

## <a name="enable-automated-user-provisioning"></a>Włącz automatyczne Inicjowanie obsługi użytkowników

W tej sekcji prowadzi przez proces nawiązywania połączenia konta użytkownika pola inicjowania obsługi interfejsu API usługi Azure AD i konfigurowanie usługi inicjowania obsługi administracyjnej do tworzenia, aktualizacji i wyłączania konta użytkowników przypisane w oparciu o przypisania użytkowników i grup w usłudze Azure AD.

Jeśli włączono automatyczne udostępnianie przypisanych użytkowników i/lub grup są dodawane do inicjowania obsługi administracyjnej kolejki, aby automatycznie udostępniane.
    
 * Jeśli tylko obiekty użytkownika są skonfigurowane do obsługi administracyjnej, a następnie bezpośrednio przypisanych użytkowników są umieszczane w kolejce inicjowania obsługi administracyjnej i wszystkich użytkowników, którzy należą do żadnych przypisanych grup są umieszczane w kolejce inicjowania obsługi administracyjnej. 
    
 * Jeśli obiekty grupy zostały skonfigurowane do obsługi administracyjnej, wszystkich obiektów grupy przypisanej są udostępniane pól oraz wszystkich użytkowników, którzy należą do tych grup. Członkostwo grup i użytkowników są zachowywane podczas zapisywania do pola.

> [!TIP] 
> Można też włączyć na języku SAML rejestracji jednokrotnej dla pola, wykonując instrukcje podane w [portalu Azure](https://portal.azure.com). Logowanie jednokrotne można skonfigurować niezależnie od automatycznego inicjowania obsługi administracyjnej, chociaż te dwie funkcje uzupełniania siebie nawzajem.

### <a name="to-configure-automatic-user-account-provisioning"></a>Aby skonfigurować konto użytkownika automatycznego inicjowania obsługi administracyjnej:

Celem tej sekcji jest przedstawiają sposób włączania obsługi kont użytkowników usługi Active Directory do pola.

1. W [portalu Azure](https://portal.azure.com), przejdź do **usługi Azure Active Directory > aplikacje przedsiębiorstwa > wszystkie aplikacje** sekcji.

2. Jeśli pole został już skonfigurowany dla logowania jednokrotnego, wyszukiwanie wystąpienia pola przy użyciu pola wyszukiwania. W przeciwnym razie wybierz **Dodaj** i wyszukaj **pole** w galerii aplikacji. Zaznacz pole w wynikach wyszukiwania, a następnie dodaj go do listy aplikacji.

3. Wybierz wystąpienia pola, a następnie wybierz **inicjowania obsługi administracyjnej** kartę.

4. Ustaw **tryb obsługi administracyjnej** do **automatyczne**. 

    ![Inicjowanie obsługi administracyjnej](./media/active-directory-saas-box-userprovisioning-tutorial/provisioning.png)

5. W obszarze **poświadczeń administratora** kliknij **autoryzacji** aby otworzyć okno dialogowe logowania pola w nowym oknie przeglądarki.

6. Na **logowania w celu udzielenia dostępu do pola** , wprowadź wymagane poświadczenia, a następnie kliknij przycisk **autoryzacji**. 
   
    ![Włącz inicjowanie obsługi użytkowników](./media/active-directory-saas-box-userprovisioning-tutorial/IC769546.png "Włącz inicjowanie obsługi użytkowników")

7. Kliknij przycisk **udzielić dostępu do pola** autoryzować tę operację i powrócić do portalu Azure. 
   
    ![Włącz inicjowanie obsługi użytkowników](./media/active-directory-saas-box-userprovisioning-tutorial/IC769549.png "Włącz inicjowanie obsługi użytkowników")

8. W portalu Azure kliknij **Testuj połączenie** zapewniające usługi Azure AD mogą łączyć się z aplikacji pole. Jeśli połączenie nie powiedzie się, upewnij się, Twoje konto pole ma uprawnienia administratora zespołu i spróbuj **"Autoryzuj"** krok ponownie.

9. Wprowadź adres e-mail osoby lub grupy, który powinien zostać wyświetlony inicjowania obsługi administracyjnej powiadomienia o błędach w **wiadomość E-mail z powiadomieniem** pola, a następnie zaznacz pole wyboru.

10. Kliknij przycisk **zapisać.**

11. W sekcji mapowania wybierz **synchronizacji Azure użytkownicy usługi Active Directory do pola.**

12. W **mapowań atrybutów** Przejrzyj atrybuty użytkowników, które są synchronizowane z usługi Azure AD, do pola. Atrybuty wybrany jako **pasujące** właściwości są używane do dopasowania kont użytkowników w polu do operacji aktualizacji. Wybierz przycisk Zapisz, aby zatwierdzić zmiany.

13. Aby włączyć usługi Azure AD usługi Box inicjowania obsługi administracyjnej, zmień **stan inicjowania obsługi administracyjnej** do **na** w sekcji Ustawienia

14. Kliknij przycisk **zapisać.**

Zaczynającym się wstępnej synchronizacji użytkowników i/lub grupy przypisane do użytkowników i grup sekcji. Synchronizacji początkowej zajmuje więcej czasu wykonywania niż kolejne synchronizacje, występujące co około 20 minut, tak długo, jak usługa jest uruchomiona. Można użyć **szczegóły synchronizacji** sekcji, aby monitorować postęp i skorzystaj z linków do inicjowania obsługi administracyjnej raporty działania, które opisują wszystkie akcje wykonywane przez usługę inicjowania obsługi administracyjnej, w polu aplikacji.

Można teraz utworzyć konta testowego. Poczekaj, aż do 20 minut, aby sprawdzić, czy konto zostało zsynchronizowane do pola.

W tej dzierżawie pole zsynchronizowanych użytkowników są wyświetlane w obszarze **użytkowników zarządzanych** w **konsoli administracyjnej**.

![Stan integracji](./media/active-directory-saas-box-userprovisioning-tutorial/IC769556.png "stan integracji")


## <a name="additional-resources"></a>Dodatkowe zasoby

* [Zarządzanie aprowizacja konta użytkowników dla aplikacji przedsiębiorstwa](active-directory-saas-tutorial-list.md)
* [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md)
* [Konfigurowanie rejestracji jednokrotnej](active-directory-saas-box-tutorial.md)