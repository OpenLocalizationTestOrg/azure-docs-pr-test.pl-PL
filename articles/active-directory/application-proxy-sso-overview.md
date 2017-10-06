---
title: "aaaManage rejestracji Jednokrotnej dla serwera Proxy aplikacji usługi Azure AD | Dokumentacja firmy Microsoft"
description: Poznaj podstawy hello rejestracji jednokrotnej z serwerem Proxy aplikacji
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/23/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: a278751a5cb1bf98c970a4e5d2eb3edc3b784096
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-does-azure-ad-application-proxy-provide-single-sign-on"></a>W jaki sposób serwera Proxy aplikacji usługi Azure AD zapewnia rejestrację jednokrotną

Logowanie jednokrotne jest kluczowym elementem serwera Proxy aplikacji usługi Azure AD.  Ponieważ użytkownicy mają tylko toosign w tooAzure usługi Active Directory w chmurze hello zapewnia hello najlepsze środowisko użytkownika. Po uwierzytelniają tooAzure usługi Active Directory łącznika serwera Proxy aplikacji hello obsługuje hello uwierzytelniania toohello lokalnej aplikacji. nie wiadomo, Hello zaplecza aplikacji hello różnica między użytkownika zdalnego logowania za pośrednictwem serwera Proxy aplikacji i normalnie korzystać na urządzeniu przyłączonym do domeny. 

toouse usługi Azure Active Directory dla aplikacji tooyour rejestracji jednokrotnej należy tooselect **usługi Azure Active Directory** jako metody uwierzytelniania wstępnego hello. W przypadku wybrania **Passthrough** , a następnie użytkownicy nie uwierzytelniania na wszystkich tooAzure usługi Active Directory, ale są ukierunkowanej toohello prostej aplikacji. To ustawienie można skonfigurować przy najpierw opublikować aplikację, lub przejdź tooyour aplikacji hello portalu Azure i edytować ustawienia serwera Proxy aplikacji hello. 

toosee jednej opcji logowania jednokrotnego, wykonaj następujące kroki:

1. Zaloguj się toohello [portalu Azure](https://portal.azure.com).
2. Przejdź za**usługi Azure Active Directory** > **aplikacje dla przedsiębiorstw** > **wszystkie aplikacje**.
3. Wybierz hello aplikacji, których rejestracji jednokrotnej opcje mają toomanage.
4. Wybierz **logowanie jednokrotne**.

   ![Menu rozwijane logowania jednokrotnego](./media/application-proxy-sso-overview/single-sign-on-mode.png)

menu rozwijane Hello zawiera pięć opcji dla aplikacji tooyour rejestracji jednokrotnej:

* Azure AD rejestracji jednokrotnej wyłączone
* Na podstawie hasła logowania jednokrotnego
* Połączonego logowania jednokrotnego
* Zintegrowane uwierzytelnianie systemu Windows
* Na podstawie nagłówka logowania jednokrotnego

## <a name="azure-ad-single-sign-on-disabled"></a>Azure AD rejestracji jednokrotnej wyłączone

Jeśli nie chcesz toouse integracji Azure Active Directory dla aplikacji tooyour rejestracji jednokrotnej, wybierz **usługi Azure AD rejestracji jednokrotnej wyłączone**. W przypadku wybrania tej opcji użytkownicy mogą uwierzytelniać dwa razy. Najpierw uwierzytelnić tooAzure usługi Active Directory i następnie zaloguj się toohello samej aplikacji. 

Ta opcja jest dobrym rozwiązaniem, jeśli aplikacji lokalnej nie wymaga tooauthenticate użytkowników, ale ma tooadd usługi Azure Active Directory jako warstwę zabezpieczeń dla dostępu zdalnego. 

## <a name="password-based-sign-on"></a>Na podstawie hasła logowania jednokrotnego

Toouse usługi Azure Active Directory jako magazynu haseł dla lokalnych aplikacji, wybierz opcję **opartego na hasłach logowania jednokrotnego**. Ta opcja jest dobrym rozwiązaniem, jeśli aplikacja jest uwierzytelniany w usłudze kombi nazwy użytkownika i hasła zamiast tokenów dostępu lub nagłówków. Z opartego na hasłach logowania jednokrotnego użytkownicy potrzebują toosign w toohello aplikacji hello po raz pierwszy ich do niego dostęp. Po wykonaniu tej usługi Azure Active Directory udostępnia hello nazwy użytkownika i hasła w imieniu użytkownika hello. 

Aby uzyskać informacji o ustawieniach opartego na hasłach logowania, zobacz [hasło vaulting dla rejestracji jednokrotnej z serwerem Proxy aplikacji](application-proxy-sso-azure-portal.md).

## <a name="linked-sign-on"></a>Połączonego logowania jednokrotnego

Jeśli masz już jedno rozwiązanie logowania jednokrotnego dla tożsamości użytkownika lokalnego, wybierz **połączonego logowania jednokrotnego**. Ta opcja umożliwia tooleverage usługi Azure Active Directory w istniejących rozwiązaniach logowania jednokrotnego, ale nadal daje użytkownikom aplikacji toohello dostępu zdalnego. 

Informacje o połączonego logowania jednokrotnego (wcześniej znany jako istniejących logowania jednokrotnego), zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md#how-does-single-sign-on-with-azure-active-directory-work).

## <a name="integrated-windows-authentication"></a>Zintegrowane uwierzytelnianie systemu Windows

Użycie aplikacji lokalnej zintegrowanego Authentication(IWA) systemu Windows lub mają toouse, delegowanie ograniczone protokołu Kerberos (KCD) dla logowania jednokrotnego, wybierz opcję **zintegrowane uwierzytelnianie systemu Windows**. Po wybraniu tej opcji użytkownicy potrzebują tylko tooAzure tooauthenticate usługi Active Directory, a następnie łącznika serwera Proxy aplikacji hello personifikuje hello użytkownika tooget token protokołu Kerberos i zalogować się w aplikacji toohello. 

Aby uzyskać informacje o konfigurowaniu zintegrowane uwierzytelnianie systemu Windows, zobacz [ograniczone delegowanie protokołu Kerberos do logowania jednokrotnego przy użyciu serwera Proxy aplikacji](active-directory-application-proxy-sso-using-kcd.md).

## <a name="header-based-sign-on"></a>Na podstawie nagłówka logowania jednokrotnego 

Użycie aplikacji nagłówki uwierzytelniania, wybierz **na podstawie nagłówka logowania jednokrotnego**. Po wybraniu tej opcji użytkownicy potrzebują tylko tooauthentication hello Azure Active Directory. Partnerzy firmy Microsoft z usługą uwierzytelniania innej firmy o nazwie PingAccess, który translacji na format nagłówka aplikacji hello token dostępu usługi Azure Active Directory hello. 

Informacje dotyczące konfigurowania uwierzytelniania na podstawie nagłówka, zobacz [nagłówka uwierzytelniania dla logowania jednokrotnego przy użyciu serwera Proxy aplikacji](application-proxy-ping-access.md).

## <a name="next-steps"></a>Następne kroki

- [Hasło vaulting dla logowania jednokrotnego przy użyciu serwera Proxy aplikacji](application-proxy-sso-azure-portal.md)
- [Ograniczone delegowanie protokołu Kerberos do logowania jednokrotnego przy użyciu serwera Proxy aplikacji](active-directory-application-proxy-sso-using-kcd.md)
- [Nagłówek uwierzytelniania dla logowania jednokrotnego przy użyciu serwera Proxy aplikacji](application-proxy-ping-access.md) 
