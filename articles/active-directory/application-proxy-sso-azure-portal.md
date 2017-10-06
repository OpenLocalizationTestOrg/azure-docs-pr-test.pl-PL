---
title: "aaaSingle logowania jednokrotnego tooapps z serwera Proxy aplikacji usługi Azure AD | Dokumentacja firmy Microsoft"
description: "Włącz logowanie jednokrotne dla aplikacji opublikowanych lokalnymi przy użyciu aplikacji serwera Proxy Azure AD w hello portalu Azure."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: d94ac3f4-cd33-4c51-9d19-544a528637d4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 5ff288d36163b74215677d9e34c93c985ac33d54
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="password-vaulting-for-single-sign-on-with-application-proxy"></a>Hasło vaulting dla logowania jednokrotnego przy użyciu serwera Proxy aplikacji

Azure Active Directory serwera Proxy aplikacji pomaga zwiększyć wydajność przez publikowanie aplikacji lokalnych, dzięki czemu pracowników zdalnych można bezpiecznie uzyskiwać do nich dostęp, zbyt. W portalu Azure hello można skonfigurować pojedynczy logowania jednokrotnego (SSO) toothese aplikacji. Użytkownicy potrzebują tylko tooauthenticate z usługą Azure AD, a ich dostęp do aplikacji przedsiębiorstwa bez toosign ponownie.

Serwer Proxy aplikacji obsługuje kilka [pojedynczy logowania jednokrotnego tryby](application-proxy-sso-overview.md). Na podstawie hasła logowania jest przeznaczony dla aplikacji, które używają kombinacja nazwy użytkownika i hasła do uwierzytelnienia. Po skonfigurowaniu opartego na hasłach logowania jednokrotnego dla aplikacji, użytkownicy mają toosign w toohello lokalną aplikację tylko raz. Po wykonaniu tej usługi Azure Active Directory przechowuje informacje logowania hello i automatycznie udostępnia on toohello aplikacji podczas użytkowników dostępu zdalnego. 

Należy już zostały opublikowane i przetestować aplikację przy użyciu serwera Proxy aplikacji. Jeśli nie, wykonaj kroki hello w [publikowanie aplikacji przy użyciu serwera Proxy aplikacji usługi Azure AD](application-proxy-publish-azure-portal.md) następnie potem wróć tutaj. 

## <a name="set-up-password-vaulting-for-your-application"></a>Ustawianie hasła vaulting aplikacji

1. Zaloguj się toohello [portalu Azure](https://portal.azure.com) jako administrator.
2. Wybierz **usługi Azure Active Directory** > **aplikacje dla przedsiębiorstw** > **wszystkie aplikacje**.
3. Z listy hello wybierz hello aplikacji, które mają tooset się z logowania jednokrotnego.  
4. Wybierz **logowanie jednokrotne**.

   ![Wybierz rejestracji jednokrotnej](./media/application-proxy-sso-azure-portal/select-sso.png)

5. W trybie logowania jednokrotnego hello, wybierz opcję **opartego na hasłach logowania jednokrotnego**.
6. Witaj adres URL logowania wprowadź hello URL strony hello gdzie użytkownicy wprowadź ich toosign nazwy użytkownika i hasła w aplikacji tooyour poza siecią firmową hello. Może to być hello zewnętrzny adres URL, które utworzono podczas publikowania aplikacji hello za pośrednictwem serwera Proxy aplikacji. 

   ![Wybierz opartego na hasłach logowania jednokrotnego, a następnie wprowadź adres URL](./media/application-proxy-sso-azure-portal/password-sso.png)

7. Wybierz pozycję **Zapisz**.

<!-- Need toorepro?
7. hello page should tell you that a sign-in form was successfully detected at hello provided URL. If it doesn't, select **Configure [your app name] Password Single Sign-on Settings** and choose **Manually detect sign-in fields**. Follow hello instructions toopoint out where hello sign-in credentials go. 
-->

## <a name="test-your-app"></a>Testowanie aplikacji

Przejdź tooexternal adres URL skonfigurowany dla aplikacji tooyour dostępu zdalnego. Zaloguj się przy użyciu poświadczeń dla danej aplikacji (lub hello poświadczenia dla konta testowego skonfigurowanego przy użyciu dostępu). Po zalogowaniu pomyślnie należy aplikacji hello tooleave może być i wrócić bez konieczności ponownego wprowadzania poświadczeń. 

## <a name="next-steps"></a>Następne kroki

- Przeczytaj informacje o innych sposobów tooimplement [rejestracji jednokrotnej z serwerem Proxy aplikacji](application-proxy-sso-overview.md)
- Dowiedz się więcej o [zagadnienia dotyczące zabezpieczeń w celu uzyskania dostępu do aplikacji zdalnie z serwera Proxy aplikacji usługi Azure AD](application-proxy-security-considerations.md)