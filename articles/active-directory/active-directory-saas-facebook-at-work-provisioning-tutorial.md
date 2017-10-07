---
title: "Samouczek: Skonfiguruj miejsca pracy przez Facebook dla Inicjowanie obsługi użytkowników | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak konta tooautomatically udostępniania i usuwanie użytkowników z usługi Azure AD tooWorkplace przez usługi Facebook."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 6341e67e-8ce6-42dc-a4ea-7295904a53ef
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 33d294dbc8f441b29138408b3c9ca41f2141f8af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configure-workplace-by-facebook-for-user-provisioning"></a>Samouczek: Skonfiguruj miejsca pracy przez Facebook dla Inicjowanie obsługi użytkowników

Ten samouczek przedstawia hello tooautomatically niezbędne kroki zapewnianie i usuwanie kont użytkowników z usługi Azure Active Directory (Azure AD) tooWorkplace przez usługi Facebook.

## <a name="prerequisites"></a>Wymagania wstępne

tooconfigure integracji usługi Azure AD z miejsca pracy przez usługi Facebook, potrzebne są następujące hello:

- Subskrypcję usługi Azure AD
- Dołączanie w serwisie Facebook rejestracji jednokrotnej (SSO) włączone subskrypcji

kroki hello tootest w tym samouczku, wykonaj te zalecenia:

- Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.
- Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać [miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).

## <a name="assign-users-tooworkplace-by-facebook"></a>Przypisywanie użytkowników tooWorkplace przez usługi Facebook

Pojęcie o nazwie "przypisania" toodetermine użytkowników, którzy mają otrzymywać aplikacje tooselected dostępu korzysta z usługi Azure AD. W kontekście hello Inicjowanie obsługi konta użytkowników tylko hello użytkowników i grup, które zostały przypisane tooan aplikacji w usłudze Azure AD są synchronizowane.

Aby zdecydować, skonfiguruj i Włącz hello inicjowania obsługi usługi, jakie użytkowników i grup w usłudze Azure AD reprezentują hello użytkowników, którzy wymagają dostępu tooyour miejsca pracy przez aplikację usługi Facebook. Następnie można przypisać te tooyour użytkowników miejsca pracy przez aplikację usługi Facebook, postępując hello instrukcjami [przypisanie użytkownika lub grupy aplikacji przedsiębiorstwa tooan](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal).

>[!IMPORTANT]
>*   Hello testu inicjowania obsługi konfiguracji przypisując pojedynczy tooWorkplace użytkownika usługi Azure AD przez usługi Facebook. Przypisz później dodatkowych użytkowników i grup.
>*   Po przypisaniu tooWorkplace użytkownika przez usługi Facebook, musisz wybrać poprawnej roli użytkownika. Hello roli domyślnego dostępu nie działa w przypadku inicjowania obsługi administracyjnej.

## <a name="enable-automated-user-provisioning"></a>Włącz inicjowanie obsługi użytkowników automatycznych

Ta sekcja przeprowadzi Cię przez łączenie konta użytkownika usługi Azure AD toohello inicjowania obsługi interfejsu API z miejsca pracy przez usługi Facebook. Dowiesz się również, jak tooconfigure hello inicjowania obsługi usługi toocreate, zaktualizować, a następnie wyłącz konta użytkowników przypisane w pracy przez usługi Facebook. To jest ustalane na podstawie użytkownika i przypisanie do grupy w usłudze Azure AD.

>[!Tip]
>Możesz również tooenabled na języku SAML logowania jednokrotnego dla miejsca pracy przez Facebook, przez następujące hello instrukcjami hello [portalu Azure](https://portal.azure.com). Chociaż te dwie funkcje uzupełniają logowania jednokrotnego można skonfigurować niezależnie od automatyczne udostępnianie.

### <a name="configure-user-account-provisioning-tooworkplace-by-facebook-in-azure-ad"></a>Skonfiguruj konto użytkownika w usłudze Azure AD inicjowania obsługi tooWorkplace przez usługi Facebook

Azure obsługuje AD tooautomatically możliwości hello zsynchronizować hello szczegóły konta przypisane tooWorkplace użytkowników przez usługi Facebook. To automatyczną synchronizację umożliwia dołączanie przez dane hello tooget Facebook tooauthorize użytkowników, aby uzyskać dostęp, wymaga przed ich próby toosign w przypadku powitania po raz pierwszy. Również cofnąć udostępnia użytkowników z miejsca pracy przez usługi Facebook, gdy został odwołany dostępu w usłudze Azure AD.

1. W hello [portalu Azure](https://portal.azure.com), wybierz pozycję **usługi Azure Active Directory** > **aplikacje przedsiębiorstwa** > **wszystkie aplikacje**.

2. Jeśli skonfigurowano już miejsca pracy przez Facebook dla logowania jednokrotnego, wyszukiwania dla swojego wystąpienia w miejscu pracy przez usługi Facebook, przy użyciu hello pola wyszukiwania. W przeciwnym razie wybierz **Dodaj** i wyszukaj **miejsca pracy przez Facebook** w galerii aplikacji hello. Wybierz **miejsca pracy przez Facebook** z hello wyniki wyszukiwania i dodać go tooyour listy aplikacji.

3. Wybierz wystąpienia programu miejsca pracy przez usługi Facebook, a następnie wybierz hello **inicjowania obsługi administracyjnej** kartę.

4. Ustaw **inicjowania obsługi trybu** za**automatyczne**. 

    ![Zrzut ekranu z miejsca pracy przez opcje inicjowania obsługi usługi Facebook](./media/active-directory-saas-facebook-at-work-provisioning-tutorial/provisioning.png)

5. W obszarze hello **poświadczeń administratora** wprowadź hello **klucz tajny tokenu** i hello **adres URL dzierżawy** z miejsca pracy przez administratora usługi Facebook.

6. Hello portalu Azure, wybierz **Testuj połączenie** tooensure usługi Azure AD mogą się łączyć tooyour miejsca pracy przez aplikację usługi Facebook. Witaj, połączenie nie powiedzie się, upewnij się, że miejsca pracy przez Facebook konto ma uprawnienia administratora zespołu.

7. Wprowadź adres e-mail hello osoby lub grupy, które powinny być przesyłane powiadomienia błąd inicjowania obsługi administracyjnej w hello **wiadomość E-mail z powiadomieniem** pola, a następnie zaznacz pole wyboru hello.

8. Wybierz pozycję **Zapisz**.

9. W obszarze hello sekcji mapowania, wybierz **tooWorkplace synchronizacji Azure Active Directory użytkowników przez Facebook**.

10. W hello **mapowań atrybutów** Przejrzyj hello atrybutów użytkowników, które są synchronizowane z usługą Azure AD tooWorkplace przez usługi Facebook. Witaj atrybuty wybrany jako **pasujące** właściwości są używane toomatch kont użytkowników hello w miejscu pracy przez Facebook dla operacji update. Wybierz wszystkie zmiany toocommit **zapisać**.

11. tooenable hello usługi inicjowania obsługi usługi Azure AD dla miejsca pracy przez Facebook, w hello **ustawienia** Zmień hello **stan inicjowania obsługi administracyjnej** za**na**.

12. Wybierz pozycję **Zapisz**.

Aby uzyskać więcej informacji na temat tooconfigure automatycznego inicjowania obsługi administracyjnej, zobacz [hello dokumentacji Facebook](https://developers.facebook.com/docs/facebook-at-work/provisioning/cloud-providers).

Można teraz utworzyć konta testowego. Poczekaj na górę minut too20 tooverify, który hello konto zostało zsynchronizowane tooWorkplace przez usługi Facebook.

## <a name="additional-resources"></a>Dodatkowe zasoby

* [Zarządzanie aprowizacja konta użytkowników dla aplikacji przedsiębiorstwa](active-directory-saas-tutorial-list.md)
* [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md)
* [Konfigurowanie rejestracji jednokrotnej](active-directory-saas-facebook-at-work-tutorial.md)

