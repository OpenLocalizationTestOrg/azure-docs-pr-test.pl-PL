---
title: "Samouczek: Konfigurowanie LinkedIn Learning dla użytkownika automatycznego inicjowania obsługi administracyjnej z usługą Azure Active Directory | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooconfigure Azure użytkownika usługi Active Directory tooautomatically udostępniania i usuwanie kont tooLinkedIn Learning."
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
ms.date: 04/15/2017
ms.author: asmalser-msft
ms.openlocfilehash: e0503e09ab384723ffb73d6ef1df8be6abfc9294
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-linkedin-learning-for-automatic-user-provisioning"></a>Samouczek: Konfigurowanie Learning LinkedIn do inicjowania obsługi użytkowników


Witaj celem tego samouczka jest tooshow hello czynności, które należy tooperform w LinkedIn Learning i Azure AD tooautomatically udostępniania i usuwanie kont użytkowników z usługi Azure AD tooLinkedIn Learning. 

## <a name="prerequisites"></a>Wymagania wstępne

Scenariusz Hello opisane w tym samouczku założono, że już hello następujące elementy:

*   Dzierżawy usługi Azure Active Directory
*   Dzierżawy LinkedIn Learning 
*   Konto administratora w uczeniu LinkedIn z toohello dostępu LinkedIn Centrum konta

> [!NOTE]
> Usługa Azure Active Directory integruje się z Learning LinkedIn przy użyciu hello [SCIM](http://www.simplecloud.info/) protokołu.

## <a name="assigning-users-toolinkedin-learning"></a>Przypisywanie użytkowników tooLinkedIn nauki

Azure Active Directory korzysta z koncepcji o nazwie "przypisania" toodetermine użytkowników, którzy mają otrzymywać aplikacje tooselected dostępu. W kontekście hello Inicjowanie obsługi konta użytkowników tylko hello użytkowników i grup, które zostały "przypisane" tooan aplikacji w usłudze Azure AD będą synchronizowane. 

Przed Skonfiguruj i Włącz hello inicjowania obsługi usługi, konieczne będzie toodecide co użytkownicy i/lub grup w usłudze Azure AD reprezentują hello użytkowników, którzy wymagają dostępu tooLinkedIn Learning. Po decyzję, można przypisać te tooLinkedIn użytkowników uczenia, wykonując następujące instrukcje hello tutaj:

[Przypisywanie użytkownikowi lub grupie aplikacji przedsiębiorstwa tooan](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-toolinkedin-learning"></a>Ważne porady dotyczące przypisywania użytkowników tooLinkedIn nauki

*   Zalecane jest pojedynczego użytkownika usługi Azure AD można przypisać hello tootest Learning tooLinkedIn inicjowania obsługi konfiguracji. Później można przypisać dodatkowych użytkowników i/lub grup.

*   Podczas przypisywania tooLinkedIn użytkownika uczenia, musisz wybrać hello **użytkownika** roli w oknie dialogowym przydział hello. Rola "Domyślnego dostępu" Hello nie działa w przypadku inicjowania obsługi administracyjnej.


## <a name="configuring-user-provisioning-toolinkedin-learning"></a>Konfigurowanie użytkownika inicjowania obsługi administracyjnej tooLinkedIn nauki

Ta sekcja przeprowadzi Cię przez łączenie konta użytkownika SCIM Learning tooLinkedIn usługi Azure AD inicjowania obsługi interfejsu API i konfigurowanie hello inicjowania obsługi administracyjnej toocreate usługi, zaktualizuj i wyłączenie konta użytkowników przypisane w oparciu o użytkowników i grup Learning LinkedIn przypisania w usłudze Azure AD.

> [!TIP]
> Można też tooenabled na języku SAML logowania jednokrotnego do uczenia LinkedIn, po hello instrukcje podane w [portalu Azure](https://portal.azure.com). Logowanie jednokrotne można skonfigurować niezależnie od automatycznego inicjowania obsługi administracyjnej, że te dwie funkcje uzupełniają.


### <a name="tooconfigure-automatic-user-account-provisioning-toolinkedin-learning-in-azure-ad"></a>konto użytkownika automatyczne tooconfigure inicjowania obsługi administracyjnej tooLinkedIn uczenia w usłudze Azure AD:


pierwszym krokiem Hello jest tooretrieve LinkedIn tokenu dostępu. Jeśli jesteś administratorem przedsiębiorstwa może samodzielnie inicjować tokenu dostępu. W Centrum konta, przejdź zbyt**ustawienia &gt; ustawienia globalne** i otwórz hello **Instalator SCIM** panelu.

> [!NOTE]
> Jeśli uzyskujesz dostęp do Centrum konta hello bezpośrednio, a nie za pośrednictwem łącza, można osiągnąć za pomocą hello następujące kroki.

1)  Zaloguj się w Centrum tooAccount.

2)  Wybierz **Admin &gt; ustawienia administratora** .

3)  Kliknij przycisk **zaawansowane integracji** na lewym pasku bocznym hello. Jesteś toohello ukierunkowanej Centrum konta.

4)  Kliknij przycisk **+ Dodaj nową konfigurację SCIM** i wykonaj procedurę hello wypełniając każdego pola.

> Autoassign licencji nie jest włączona, oznacza, że tylko dane użytkownika jest synchronizowany.

![LinkedIn szkoleniowe dotyczące inicjowania obsługi administracyjnej](./media/active-directory-saas-linkedinlearning-provisioning-tutorial/linkedin_1.PNG)

> Po włączeniu przypisania autolicense należy toonote wystąpienia aplikacji i typu licencji. Przypisano licencje na pierwszym dostarczanych, najpierw służyć podstawę, dopóki wszystkie licencje hello są pobierane.

![LinkedIn szkoleniowe dotyczące inicjowania obsługi administracyjnej](./media/active-directory-saas-linkedinlearning-provisioning-tutorial/linkedin_2.PNG)

5)  Kliknij przycisk **Generuj token**. Powinien zostać wyświetlony ekran tokenu dostępu w obszarze hello **token dostępu** pola.

6)  Zapisz Schowka tooyour tokenu dostępu lub komputerze z przed opuszczeniem hello strony.

7) Następnie zaloguj się toohello [portalu Azure](https://portal.azure.com)i Przeglądaj toohello **usługi Azure Active Directory > aplikacje przedsiębiorstwa > wszystkie aplikacje** sekcji.

8) LinkedIn Learning został już skonfigurowany dla logowania jednokrotnego, wyszukaj wystąpienie usługi przy użyciu pola wyszukiwania hello Learning LinkedIn. W przeciwnym razie wybierz **Dodaj** i wyszukaj **LinkedIn Learning** w galerii aplikacji hello. Wybierz LinkedIn Learning z wyników wyszukiwania hello i dodać tooyour listy aplikacji.

9)  Wybierz wystąpienie usługi uczenie LinkedIn, a następnie wybierz hello **inicjowania obsługi administracyjnej** kartę.

10) Zestaw hello **inicjowania obsługi trybu** za**automatyczne**.

![LinkedIn szkoleniowe dotyczące inicjowania obsługi administracyjnej](./media/active-directory-saas-linkedinlearning-provisioning-tutorial/linkedin_3.PNG)

11)  Wypełnij następujące pola w obszarze hello **poświadczeń administratora** :

* W hello **adres URL dzierżawy** wprowadź https://api.linkedin.com.

* W hello **klucz tajny tokenu** wprowadź token dostępu hello wygenerowany w kroku 1 i kliknij przycisk **Testuj połączenie** .

* Powiadomienie Powodzenie powinna zostać wyświetlona po stronie upperright hello portalu usługi.

12) Wprowadź adres e-mail hello osoby lub grupy, które powinny być przesyłane powiadomienia błąd inicjowania obsługi administracyjnej w hello **wiadomość E-mail z powiadomieniem** pola i zaznacz pole wyboru hello poniżej.

13) Kliknij pozycję **Zapisz**. 

14) W hello **mapowań atrybutów** Przejrzyj atrybuty użytkowników i grup hello, które są synchronizowane z usługą Azure AD tooLinkedIn Learning. Należy pamiętać, że wybrany jako atrybuty hello **pasujące** właściwości będzie używana toomatch hello kont i grup użytkowników w uczeniu LinkedIn dla operacji aktualizacji. Wybierz toocommit przycisk Zapisz hello wszelkie zmiany.

![LinkedIn szkoleniowe dotyczące inicjowania obsługi administracyjnej](./media/active-directory-saas-linkedinlearning-provisioning-tutorial/linkedin_4.PNG)

15) tooenable hello inicjowania obsługi usługi Azure AD LinkedIn szkoleniowe, zmień hello **stan inicjowania obsługi administracyjnej** za**na** w hello **ustawienia** sekcji

16) Kliknij pozycję **Zapisz**. 

Spowoduje to uruchomienie synchronizacji początkowej hello żadnych użytkowników i/lub grupy przypisane tooLinkedIn uczenia się w sekcji hello użytkowników i grup. Należy pamiętać, że synchronizacji początkowej hello potrwa tooperform dłużej niż kolejne synchronizacje, które występują co około 20 minut, tak długo, jak działa usługa hello. Można użyć hello **szczegóły synchronizacji** sekcji postępu toomonitor i wykonaj łącza tooprovisioning działania raporty, które opisują wszystkie akcje wykonywane przez hello świadczenie usługi w aplikacji LinkedIn Learning.


## <a name="additional-resources"></a>Dodatkowe zasoby

* [Zarządzanie aprowizacja konta użytkowników dla aplikacji przedsiębiorstwa](active-directory-enterprise-apps-manage-provisioning.md)
* [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md)
