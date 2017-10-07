---
title: aaaHow tooconfigure pojedynczego logowania jednokrotnego tooan aplikacji serwera Proxy aplikacji | Dokumentacja firmy Microsoft
description: "Jak szybko możesz skonfigurować tooyour rejestracji jednokrotnej aplikacji serwera proxy aplikacji"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: e1289203177c77b3a8bcc9058c5c0b8ae50f243e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-single-sign-on-tooan-application-proxy-application"></a>Jak tooconfigure pojedynczy tooan logowania aplikacja serwera Proxy aplikacji

Logowanie jednokrotne (SSO) umożliwia tooaccess Twojego użytkowników aplikacji bez uwierzytelniania wiele razy. Umożliwia hello toooccur pojedynczego uwierzytelniania w chmurze hello, w usłudze Azure Active Directory oraz umożliwia usługi hello lub łącznika tooimpersonate hello użytkownika toocomplete wszelkie problemy dodatkowego uwierzytelniania z aplikacji hello.

## <a name="how-tooconfigure-single-sign-on"></a>Jak tooconfigure jednokrotnego
tooconfigure logowania jednokrotnego, najpierw upewnij się, że aplikacja jest skonfigurowana do uwierzytelniania wstępnego za pomocą usługi Azure Active Directory. toodo, przejdź zbyt**usługi Azure Active Directory**  - &gt; **aplikacje dla przedsiębiorstw**  - &gt; **wszystkie aplikacje**  - &gt; Aplikacji  **- &gt; serwera Proxy aplikacji**. Na tej stronie, zobacz "Wstępne uwierzytelnianie" hello pole i upewnij się, że ustawiono zbyt "Azure Active Directory. 

Aby uzyskać więcej informacji na temat metod uwierzytelniania wstępnego hello, zobacz krok 4 hello [dokumentu publikowania aplikacji](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal).

   ![Metoda uwierzytelniania wstępnego w portalu Azure](./media/application-proxy-config-sso-how-to/app-proxy.png)

## <a name="configuring-single-sign-on-modes-for-application-proxy-applications"></a>Konfigurowanie trybów rejestracji jednokrotnej dla aplikacji serwera Proxy aplikacji
Następnie skonfigurować hello określonego typu rejestracji jednokrotnej. Witaj logowania jednokrotnego metody są klasyfikowane oparte na korzysta z jakiego rodzaju uwierzytelniania hello wewnętrznej bazy danych aplikacji. Aplikacje serwera Proxy aplikacji obsługuje trzy rodzaje rejestracji:

-   **Na podstawie hasła logowania jednokrotnego**: opartego na hasłach logowania może służyć do dowolnej aplikacji, która korzysta z pola Nazwa użytkownika i hasło na toosign. Kroki konfiguracji można znaleźć w naszych [dokumentacji konfiguracji logowania jednokrotnego hasła](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-whats-new-azure-portal#bring-your-own-password-sso-applications).

-   **Zintegrowane uwierzytelnianie systemu Windows**: w przypadku aplikacji przy użyciu zintegrowanego uwierzytelniania systemu Windows (IWA) rejestracji jednokrotnej jest włączona za pośrednictwem protokołu Kerberos ograniczonego delegowania (KCD). To zapewnia łączniki serwera Proxy aplikacji uprawnienia użytkowników usługi Active Directory tooimpersonate i toosend i odbierać tokeny w ich imieniu. Szczegółowe informacje na temat konfigurowania KCD znajdują się w hello [rejestracji jednokrotnej z dokumentacją KCD](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-sso-using-kcd).

-   **Na podstawie nagłówka logowania jednokrotnego**: na podstawie nagłówka logowania jest włączona za pośrednictwem powiązania i wymagać dodatkowej konfiguracji. Aby uzyskać szczegółowe informacje o partnerstwie hello i instrukcje krok po kroku dotyczące konfigurowania aplikacji tooan rejestracji jednokrotnej, która używa nagłówki uwierzytelniania, zobacz hello [PingAccess dokumentacji usługi Azure AD](https://docs.microsoft.com/azure/active-directory/application-proxy-ping-access).

Każdą z tych opcji można znaleźć, przechodząc aplikacji tooyour "Aplikacje przedsiębiorstwa" i otwarcia hello **rejestracji jednokrotnej** strony w menu po lewej stronie powitania. należy pamiętać, że jeśli aplikacja została utworzona w hello starego portalu, mogą nie być widoczne wszystkie te opcje.

Na tej stronie zostanie również wyświetlony jedną dodatkową opcję logowania jednokrotnego: połączonego logowania jednokrotnego. To jest również obsługiwana przez serwer Proxy aplikacji. Należy jednak zwrócić uwagę, że ta opcja nie dodaje aplikacji toohello rejestracji jednokrotnej. Inaczej mówiąc, że aplikacja hello może już istnieć rejestracji jednokrotnej implementowane za pomocą innej usługi, takie jak Active Directory Federation Services. 

Ta opcja umożliwia toocreate administratora aplikacji tooan łącza, który użytkownicy trafić najpierw na podczas uzyskiwania dostępu do aplikacji hello. Na przykład jeśli istnieje, że aplikacja, która jest skonfigurowana tooauthenticate użytkowników przy użyciu Active Directory Federation Services 2.0, administrator może użyć hello "połączonego logowania jednokrotnego" opcja toocreate tooit łącza na powitania panelu dostępu.

## <a name="next-steps"></a>Następne kroki
[Podaj aplikacji tooyour rejestracji jednokrotnej z serwerem Proxy aplikacji](active-directory-application-proxy-sso-using-kcd.md)
