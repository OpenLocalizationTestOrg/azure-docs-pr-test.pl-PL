---
title: "aaaDisable logowania użytkowników dla aplikacji przedsiębiorstwa w usłudze Azure Active Directory | Dokumentacja firmy Microsoft"
description: "Jak toodisable aplikacji przedsiębiorstwa, aby użytkownicy nie mogą zalogować tooit w usłudze Azure Active Directory"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: a27562f9-18dc-42e8-9fee-5419566f8fd7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.openlocfilehash: 4c560b59359d433b0852a7606cc2cc0204866234
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="disable-user-sign-ins-for-an-enterprise-app-in-azure-active-directory"></a>Wyłącz logowania użytkowników dla aplikacji przedsiębiorstwa w usłudze Azure Active Directory
Jest łatwy toodisable aplikacji dla przedsiębiorstw, dzięki czemu użytkownicy nie mogą zalogować tooit w usłudze Azure Active Directory (Azure AD). Musi mieć hello odpowiednie uprawnienia toomanage hello przedsiębiorstwa aplikacji, a musi być administratorem globalnym katalogu hello.

## <a name="how-do-i-disable-user-sign-ins"></a>Jak wyłączyć logowania użytkowników?
1. Zaloguj się toohello [portalu Azure](https://portal.azure.com) przy użyciu konta, które jest administratorem globalnym katalogu hello.
2. Wybierz **więcej usług**, wprowadź **usługi Azure Active Directory** w hello pola tekstowego, a następnie wybierz **Enter**.
3. Na powitania **usługi Azure Active Directory** -  ***directoryname*** bloku (to znaczy bloku hello Azure AD dla katalogu hello są używane do zarządzania), wybierz **aplikacjedlaprzedsiębiorstw**.

    ![Otwieranie aplikacji przedsiębiorstwa](./media/active-directory-coreapps-disable-app-azure-portal/open-enterprise-apps.png)
4. Na powitania **aplikacje dla przedsiębiorstw** bloku, wybierz opcję **wszystkie aplikacje**. Zostanie wyświetlona lista aplikacji hello, którymi można zarządzać.
5. Na powitania **aplikacje przedsiębiorstwa — wszystkie aplikacje** bloku, wybierz aplikację.
6. Na powitania ***appname*** bloku (to znaczy hello bloku o nazwie hello hello wybranej aplikacji w tytule hello) wybierz **właściwości**.

    ![Wybieranie hello wszystkie polecenia aplikacji](./media/active-directory-coreapps-disable-app-azure-portal/select-app.png)
7. Na powitania ***appname*** - **właściwości** bloku, wybierz opcję **nr** dla **dostępny dla użytkowników w toosign?**.
8. Wybierz hello **zapisać** polecenia.

## <a name="next-steps"></a>Następne kroki
* [Zobacz wszystkie moje grupy](active-directory-groups-view-azure-portal.md)
* [Przypisywanie użytkownikowi lub grupie aplikacji przedsiębiorstwa tooan](active-directory-coreapps-assign-user-azure-portal.md)
* [Usuń przypisanie użytkownika lub grupy z aplikacjami](active-directory-coreapps-remove-assignment-azure-portal.md)
* [Zmiana nazwy hello lub logo aplikacji przedsiębiorstwa](active-directory-coreapps-change-app-logo-user-azure-portal.md)
