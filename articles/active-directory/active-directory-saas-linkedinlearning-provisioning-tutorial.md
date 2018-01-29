---
title: "Samouczek: Konfigurowanie LinkedIn Learning dla użytkownika automatycznego inicjowania obsługi administracyjnej z usługą Azure Active Directory | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak skonfigurować usługi Azure Active Directory, aby automatycznie zapewnianie i usuwanie kont użytkowników do uczenia LinkedIn."
services: active-directory
documentationcenter: 
author: asmalser-msft
writer: asmalser-msft
manager: mtillman
ms.assetid: d4ca2365-6729-48f7-bb7f-c0f5ffe740a3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/15/2017
ms.author: asmalser-msft
ms.openlocfilehash: 9b07417fbb094cdc285e00be3c48f9af0a38601d
ms.sourcegitcommit: e266df9f97d04acfc4a843770fadfd8edf4fa2b7
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/11/2017
---
# <a name="tutorial-configuring-linkedin-learning-for-automatic-user-provisioning"></a>Samouczek: Konfigurowanie Learning LinkedIn do inicjowania obsługi użytkowników


Celem tego samouczka jest opisano czynności, które należy wykonać w LinkedIn Learning i Azure AD, aby automatycznie zapewnianie i usuwanie kont użytkowników z usługi Azure AD do uczenia LinkedIn. 

## <a name="prerequisites"></a>Wymagania wstępne

Scenariusz opisany w tym samouczku założono, że już następujące elementy:

*   Dzierżawy usługi Azure Active Directory
*   Dzierżawy LinkedIn Learning 
*   Konto administratora w uczeniu LinkedIn dostęp do Centrum konta LinkedIn

> [!NOTE]
> Azure Active Directory integruje się z za pomocą uczenia LinkedIn [SCIM](http://www.simplecloud.info/) protokołu.

## <a name="assigning-users-to-linkedin-learning"></a>Przypisywanie użytkowników do uczenia LinkedIn

Usługi Azure Active Directory używa pojęcie o nazwie "przypisania" w celu określenia, którzy użytkownicy powinien otrzymać dostęp do wybranej aplikacji. W kontekście użytkownika automatyczne Inicjowanie obsługi konta tylko użytkownicy i grupy, które "przypisano" do aplikacji w usłudze Azure AD będą synchronizowane. 

Przed Skonfiguruj i włącz usługę inicjowania obsługi administracyjnej, należy zdecydować, jakie użytkownicy i/lub grup w usłudze Azure AD reprezentują użytkowników, którzy potrzebują dostępu do uczenia LinkedIn. Po decyzję, można przypisać tych użytkowników do uczenia LinkedIn, postępując zgodnie z instrukcjami poniżej:

[Przypisanie użytkownika lub grupę do aplikacji w przedsiębiorstwie](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-to-linkedin-learning"></a>Ważne porady dotyczące przypisywania użytkowników do uczenia LinkedIn

*   Zalecane jest pojedynczego użytkownika usługi Azure AD można przypisać do uczenia LinkedIn do testowania konfiguracji inicjowania obsługi administracyjnej. Później można przypisać dodatkowych użytkowników i/lub grup.

*   Przypisanie użytkownika do uczenia LinkedIn, należy wybrać **użytkownika** roli w oknie dialogowym przypisania. Rola "Domyślnego dostępu" nie działa w przypadku inicjowania obsługi administracyjnej.


## <a name="configuring-user-provisioning-to-linkedin-learning"></a>Konfigurowanie inicjowania obsługi administracyjnej LinkedIn Learning użytkownika

Ta sekcja przeprowadzi Cię przez usługę Azure AD nawiązywania połączenia z kontem użytkownika SCIM LinkedIn Learning inicjowania obsługi interfejsu API i konfigurowanie usługi inicjowania obsługi administracyjnej do tworzenia, aktualizacji i wyłączyć przypisane kont użytkowników w oparciu o użytkowników i grup Learning LinkedIn przypisania w usłudze Azure AD.

> [!TIP]
> Można też włączyć na języku SAML logowania jednokrotnego do uczenia LinkedIn, postępując zgodnie z instrukcjami zawarte w [portalu Azure](https://portal.azure.com). Logowanie jednokrotne można skonfigurować niezależnie od automatycznego inicjowania obsługi administracyjnej, że te dwie funkcje uzupełniają.


### <a name="to-configure-automatic-user-account-provisioning-to-linkedin-learning-in-azure-ad"></a>Aby skonfigurować użytkownika automatyczne Inicjowanie obsługi konta do uczenia LinkedIn w usłudze Azure AD:


Pierwszym krokiem jest można pobrać tokenu dostępu LinkedIn. Jeśli jesteś administratorem przedsiębiorstwa może samodzielnie inicjować tokenu dostępu. W Centrum konta, przejdź do **ustawienia &gt; ustawienia globalne** , a następnie otwórz **Instalator SCIM** panelu.

> [!NOTE]
> Jeśli uzyskujesz dostęp do Centrum konta bezpośrednio, a nie za pośrednictwem łącza, można osiągnąć go, wykonując następujące kroki.

1)  Zaloguj się do konta Center.

2)  Wybierz **Admin &gt; ustawienia administratora** .

3)  Kliknij przycisk **zaawansowane integracji** na lewym pasku bocznym. Użytkownik jest kierowany do Centrum konta.

4)  Kliknij przycisk **+ Dodaj nową konfigurację SCIM** i postępuj zgodnie z procedurą, wypełniając każdego pola.

> Autoassign licencji nie jest włączona, oznacza, że tylko dane użytkownika jest synchronizowany.

![LinkedIn szkoleniowe dotyczące inicjowania obsługi administracyjnej](./media/active-directory-saas-linkedinlearning-provisioning-tutorial/linkedin_1.PNG)

> Po włączeniu autolicense przypisania musisz Zanotuj wystąpienia aplikacji i typu licencji. Przypisano licencje na pierwszym dostarczanych, najpierw służyć podstawę, dopóki wszystkie licencje są pobierane.

![LinkedIn szkoleniowe dotyczące inicjowania obsługi administracyjnej](./media/active-directory-saas-linkedinlearning-provisioning-tutorial/linkedin_2.PNG)

5)  Kliknij przycisk **Generuj token**. Powinien zostać wyświetlony ekran tokenu dostępu w obszarze **token dostępu** pola.

6)  Zapisz tokenu dostępu do Schowka lub komputera przed opuszczeniem strony.

7) Następnie zaloguj się do [portalu Azure](https://portal.azure.com), a następnie przejdź do **usługi Azure Active Directory > aplikacje przedsiębiorstwa > wszystkie aplikacje** sekcji.

8) LinkedIn Learning został już skonfigurowany dla logowania jednokrotnego, wyszukaj wystąpieniem Learning LinkedIn przy użyciu pola wyszukiwania. W przeciwnym razie wybierz **Dodaj** i wyszukaj **LinkedIn Learning** w galerii aplikacji. Wybierz LinkedIn Learning z wyników wyszukiwania i dodaj go do listy aplikacji.

9)  Wybierz wystąpienie usługi uczenie LinkedIn, a następnie wybierz **inicjowania obsługi administracyjnej** kartę.

10) Ustaw **tryb obsługi administracyjnej** do **automatyczne**.

![LinkedIn szkoleniowe dotyczące inicjowania obsługi administracyjnej](./media/active-directory-saas-linkedinlearning-provisioning-tutorial/linkedin_3.PNG)

11)  Wypełnij następujące pola w obszarze **poświadczeń administratora** :

* W **adres URL dzierżawy** wprowadź https://api.linkedin.com.

* W **klucz tajny tokenu** wprowadź token dostępu wygenerowany w kroku 1 i kliknij przycisk **Testuj połączenie** .

* Powiadomienie o Powodzenie powinna zostać wyświetlona po stronie upperright portalu usługi.

12) Wprowadź adres e-mail osoby lub grupy, który powinien zostać wyświetlony inicjowania obsługi administracyjnej powiadomienia o błędach w **wiadomość E-mail z powiadomieniem** pola, a następnie zaznacz pole wyboru poniżej.

13) Kliknij pozycję **Zapisz**. 

14) W **mapowań atrybutów** Przejrzyj atrybuty użytkowników i grup, które będą synchronizowane z usługi Azure AD do uczenia LinkedIn. Należy pamiętać, że atrybuty wybrany jako **pasujące** właściwości, które będą używane do dopasowania kont użytkowników i grup w uczeniu LinkedIn dla operacji update. Wybierz przycisk Zapisz, aby zatwierdzić zmiany.

![LinkedIn szkoleniowe dotyczące inicjowania obsługi administracyjnej](./media/active-directory-saas-linkedinlearning-provisioning-tutorial/linkedin_4.PNG)

15) Aby włączyć usługi Azure AD usługi szkoleniowe LinkedIn inicjowania obsługi administracyjnej, zmień **stan inicjowania obsługi administracyjnej** do **na** w **ustawienia** sekcji

16) Kliknij pozycję **Zapisz**. 

Spowoduje to uruchomienie synchronizacji początkowej użytkowników i/lub grupy przypisane do uczenia LinkedIn w sekcji Użytkownicy i grupy. Należy pamiętać, że synchronizacji początkowej będzie trwać dłużej wykonać niż kolejne synchronizacje, występujące co około 20 minut, tak długo, jak usługa jest uruchomiona. Można użyć **szczegóły synchronizacji** sekcji, aby monitorować postęp i skorzystaj z linków do inicjowania obsługi administracyjnej raporty działania, które opisują wszystkie akcje wykonywane przez usługę inicjowania obsługi administracyjnej w aplikacji LinkedIn Learning.


## <a name="additional-resources"></a>Dodatkowe zasoby

* [Zarządzanie aprowizacja konta użytkowników dla aplikacji przedsiębiorstwa](active-directory-enterprise-apps-manage-provisioning.md)
* [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md)
