---
title: 'Samouczek: Integracji Azure Active Directory z miejsca pracy przez Facebook | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i miejsca pracy przez usługi Facebook."
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
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 551ec353a5ec1da936373587688c299a6f4acca7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-workplace-by-facebook-for-user-provisioning"></a>Samouczek: Konfigurowanie miejsca pracy przez usługi Facebook na potrzeby Inicjowanie obsługi użytkowników

Celem Hello tego samouczka jest tooshow hello czynności, które należy tooperform w miejscu pracy przez Facebook i Azure AD tooautomatically udostępniania i usuwanie kont użytkowników z usługi Azure AD tooWorkplace przez usługi Facebook.

## <a name="prerequisites"></a>Wymagania wstępne

tooconfigure integracji usługi Azure AD z miejsca pracy przez usługi Facebook, należy hello następujące elementy:

- Subskrypcję usługi Azure AD
- Pracy przez Facebook jednokrotnego włączone subskrypcji

> [!NOTE]
> tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.

tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:

- Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.
- Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).

## <a name="assigning-users-tooworkplace-by-facebook"></a>Przypisywanie użytkowników tooWorkplace przez usługi Facebook

Azure Active Directory korzysta z koncepcji o nazwie "przypisania" toodetermine użytkowników, którzy mają otrzymywać aplikacje tooselected dostępu. W kontekście hello Inicjowanie obsługi konta użytkowników tylko hello użytkowników i grup, które zostały "przypisane" tooan aplikacji w usłudze Azure AD jest zsynchronizowany.

Przed Skonfiguruj i Włącz hello usługi inicjowania obsługi administracyjnej, należy toodecide jakie użytkowników i/lub grup w usłudze Azure AD reprezentują hello użytkowników, którzy wymagają dostępu tooyour miejsca pracy przez aplikację usługi Facebook. Po decyzję, można przypisać tych użytkowników tooyour miejsca pracy przez aplikację usługi Facebook, wykonując instrukcje hello tutaj:

[Przypisywanie użytkownikowi lub grupie aplikacji przedsiębiorstwa tooan](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal)

### <a name="important-tips-for-assigning-users-tooworkplace-by-facebook"></a>Ważne porady dotyczące przypisywania tooWorkplace użytkowników przez usługi Facebook

*   Zalecane jest pojedynczego użytkownika usługi Azure AD jest przypisywany tooWorkplace przez hello tootest Facebook inicjowania obsługi konfiguracji. Później można przypisać dodatkowych użytkowników i/lub grup.

*   Podczas przypisywania tooWorkplace użytkownika przez usługi Facebook, musisz wybrać poprawnej roli użytkownika. Rola "Domyślnego dostępu" Hello nie działa w przypadku inicjowania obsługi administracyjnej.

## <a name="enable-user-provisioning"></a>Włącz inicjowanie obsługi użytkowników

Ta sekcja przeprowadzi Cię przez łączenie z tooWorkplace usługi Azure AD przez konto użytkownika usługi Facebook na inicjowanie obsługi interfejsu API i konfigurowanie hello inicjowania obsługi usługi toocreate, zaktualizować, a następnie wyłącz konta użytkowników przypisane w pracy przez usługi Facebook na podstawie użytkownika i grupy przypisania w usłudze Azure AD.

>[!Tip]
>Można też tooenabled na języku SAML logowania jednokrotnego dla miejsca pracy przez Facebook, po hello instrukcje podane w [portalu Azure](https://portal.azure.com). Logowanie jednokrotne można skonfigurować niezależnie od automatycznego inicjowania obsługi administracyjnej, chociaż te dwie funkcje uzupełniania siebie nawzajem.

### <a name="tooconfigure-user-account-provisioning-tooworkplace-by-facebook-in-azure-ad"></a>konto użytkownika tooconfigure udostępniania tooWorkplace w serwisie Facebook w usłudze Azure AD:

Celem Hello w tej sekcji jest toooutline jak tooenable użytkownika usługi Active Directory Inicjowanie obsługi administracyjnej kont tooWorkplace przez usługi Facebook.

Azure obsługuje AD tooautomatically możliwości hello zsynchronizować hello szczegóły konta przypisane tooWorkplace użytkowników przez usługi Facebook. To automatyczną synchronizację umożliwia dołączanie przez dane hello tooget Facebook tooauthorize użytkowników, aby uzyskać dostęp, wymaga przed ich próby toosign w przypadku powitania po raz pierwszy. Również cofnąć udostępnia użytkowników z miejsca pracy przez usługi Facebook, gdy został odwołany dostępu w usłudze Azure AD.

1. W hello [portalu Azure](https://portal.azure.com), Przeglądaj toohello **usługi Azure Active Directory** > **aplikacje przedsiębiorstwa** > **wszystkie aplikacje** sekcji.

2. Jeśli skonfigurowano już miejsca pracy przez Facebook dla logowania jednokrotnego, wyszukiwania dla swojego wystąpienia w miejscu pracy przez usługi Facebook za pomocą pola wyszukiwania hello. W przeciwnym razie wybierz **Dodaj** i wyszukaj **miejsca pracy przez Facebook** w galerii aplikacji hello. Wybierz obszar roboczy w serwisie Facebook z wyników wyszukiwania hello i dodać go tooyour listę aplikacji.

3. Wybierz wystąpienia programu miejsca pracy przez usługi Facebook, a następnie wybierz hello **inicjowania obsługi administracyjnej** kartę.

4. Zestaw hello **inicjowania obsługi trybu** za**automatyczne**. 

    ![Inicjowanie obsługi administracyjnej](./media/active-directory-saas-workplacebyfacebook-provisioning-tutorial/provisioning.png)

5. W obszarze hello **poświadczeń administratora** sekcji i wprowadź klucz tajny tokenu hello hello adres URL dzierżawy z miejsca pracy przez administratora usługi Facebook.

6. W portalu Azure hello, kliknij przycisk **Testuj połączenie** tooensure usługi Azure AD mogą się łączyć tooyour miejsca pracy przez aplikację usługi Facebook. Jeśli hello połączenia nie powiedzie się, upewnij się, że miejsca pracy przez Facebook konto ma uprawnienia administratora zespołu.

7. Wprowadź adres e-mail hello osoby lub grupy, które powinny być przesyłane powiadomienia błąd inicjowania obsługi administracyjnej w hello **wiadomość E-mail z powiadomieniem** pola, a następnie zaznacz pole wyboru hello.

8. Kliknij przycisk **zapisać.**

9. W obszarze hello sekcji mapowania, wybierz **tooWorkplace synchronizacji Azure Active Directory użytkowników przez usługi Facebook.**

10. W hello **mapowań atrybutów** Przejrzyj hello atrybutów użytkowników, które są synchronizowane z usługą Azure AD tooWorkplace przez usługi Facebook. Witaj atrybuty wybrany jako **pasujące** właściwości są używane toomatch kont użytkowników hello w miejscu pracy przez Facebook dla operacji update. Wybierz toocommit przycisk Zapisz hello wszelkie zmiany.

11. tooenable hello inicjowania obsługi usługi Azure AD dla miejsca pracy przez Facebook, zmień hello **stan inicjowania obsługi administracyjnej** za**na** w hello **ustawienia** sekcji

12. Kliknij przycisk **zapisać.**

Aby uzyskać więcej informacji na temat tooconfigure automatycznego inicjowania obsługi administracyjnej, zobacz [https://developers.facebook.com/docs/facebook-at-work/provisioning/cloud-providers](https://developers.facebook.com/docs/facebook-at-work/provisioning/cloud-providers)

Można teraz utworzyć konta testowego. Poczekaj na górę minut too20 tooverify, który hello konto zostało zsynchronizowane tooWorkplace przez usługi Facebook.

## <a name="additional-resources"></a>Dodatkowe zasoby

* [Zarządzanie aprowizacja konta użytkowników dla aplikacji przedsiębiorstwa](active-directory-saas-tutorial-list.md)
* [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md)
* [Konfigurowanie rejestracji jednokrotnej](active-directory-saas-workplacebyfacebook-tutorial.md)

