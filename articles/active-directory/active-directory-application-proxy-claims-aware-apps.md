---
title: "aplikacje świadome aaaClaims - serwera Proxy aplikacji usługi Azure AD | Dokumentacja firmy Microsoft"
description: "Jak toopublish lokalnej aplikacji ASP.NET, które akceptują oświadczenia usług AD FS dla bezpieczny dostęp zdalny przez użytkowników."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
editor: harshja
ms.assetid: 91e6211b-fe6a-42c6-bdb3-1fff0312db15
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: kgremban
ms.openlocfilehash: 7be633225de700226c7c94815eb91b3de2b61cb5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="working-with-claims-aware-apps-in-application-proxy"></a>Praca z aplikacji obsługujących oświadczenia w serwer Proxy aplikacji
[Aplikacje obsługujące oświadczenia](https://msdn.microsoft.com/library/windows/desktop/bb736227.aspx) wykonania przekierowania toohello zabezpieczeń usługi tokenów (STS). Hello STS żądania poświadczeń użytkownika hello zamian token i następnie przekierowuje hello użytkownika toohello aplikacji. Istnieje kilka sposobów tooenable serwera Proxy aplikacji toowork z tych przekierowania. Użyj tego artykułu tooconfigure wdrożenia dla aplikacji obsługujących oświadczenia. 

## <a name="prerequisites"></a>Wymagania wstępne
Upewnij się, że ten hello STS hello aplikacji obsługującej oświadczenia przekierowuje toois dostępne spoza sieci lokalnej. Można udostępnić hello STS ujawnienie go za pośrednictwem serwera proxy lub zezwalając poza połączenia. 

## <a name="publish-your-application"></a>Publikowanie aplikacji

1. Publikowanie aplikacji zgodnie z instrukcjami toohello opisanego w [publikowania aplikacji za pomocą serwera Proxy aplikacji](application-proxy-publish-azure-portal.md).
2. Przejdź do strony aplikacji hello portalu i wybierz pozycję toohello **logowanie jednokrotne**.
3. Jeśli została wybrana opcja **usługi Azure Active Directory** jako sieci **metoda uwierzytelniania wstępnego**, wybierz pozycję **usługi Azure AD rejestracji jednokrotnej wyłączone** jako sieci **wewnętrzne Metoda uwierzytelniania**. Jeśli została wybrana opcja **Passthrough** jako sieci **metoda uwierzytelniania wstępnego**, nie potrzebujesz cokolwiek toochange.

## <a name="configure-adfs"></a>Konfigurowanie usług AD FS

Usługi AD FS można skonfigurować dla aplikacji obsługujących oświadczenia w jeden z dwóch sposobów. Hello jest najpierw przy użyciu domen niestandardowych. Hello jest drugi z protokołu WS-Federation. 

### <a name="option-1-custom-domains"></a>Opcja 1: Domen niestandardowych

Jeśli wszystkie hello wewnętrzne adresy URL dla aplikacji są w pełni kwalifikowanej nazwy domen (FQDN), a następnie można skonfigurować [domen niestandardowych](active-directory-application-proxy-custom-domains.md) dla aplikacji. Użyj hello domen niestandardowych toocreate zewnętrznych adresów URL, które są takie same jak hello wewnętrzne adresy URL hello. W przypadku sieci zewnętrzne adresy URL zgodne z wewnętrznych adresów URL, przekierowań STS hello pracować, czy użytkownicy są lokalnego lub zdalnego. 

### <a name="option-2-ws-federation"></a>Opcja 2: WS-Federation

1. Otwórz przystawkę Zarządzanie usługi AD FS.
2. Przejdź za**zaufania jednostek uzależnionych**, kliknij prawym przyciskiem myszy w aplikacji hello są publikowanie za pomocą serwera Proxy aplikacji i wybierz **właściwości**.  

   ![Zaufania jednostek uzależnionych kliknij prawym przyciskiem myszy nazwę aplikacji — zrzut ekranu](./media/active-directory-application-proxy-claims-aware-apps/appproxyrelyingpartytrust.png)  

3. Na powitania **punkty końcowe** , w obszarze **typ punktu końcowego**, wybierz pozycję **WS-Federation**.
4. W obszarze **URL zaufanych**, wprowadź adres URL hello wprowadzony w powitania serwera Proxy aplikacji w obszarze **zewnętrzny adres URL** i kliknij przycisk **OK**.  

   ![Dodawanie punktu końcowego — ustaw wartość adres URL z zaufanych — zrzut ekranu](./media/active-directory-application-proxy-claims-aware-apps/appproxyendpointtrustedurl.png)  

## <a name="next-steps"></a>Następne kroki
* [Włącz jednokrotnego](application-proxy-sso-overview.md) dla aplikacji, które nie są obsługujących oświadczenia
* [Włącz toointeract aplikacji natywnej klienta z serwera proxy aplikacji](active-directory-application-proxy-native-client.md)


