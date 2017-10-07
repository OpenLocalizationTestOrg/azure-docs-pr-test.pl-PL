---
title: "aaaUnexpected aplikacji na liście aplikacji | Dokumentacja firmy Microsoft"
description: "Jak toosee wszystkich aplikacji w dzierżawie i zrozumieć, jak aplikacje pojawiają się na liście wszystkie aplikacje w aplikacjach dla przedsiębiorstw"
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
ms.openlocfilehash: 2f974046b655bc36a05f002c56511a8a988cd01c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="unexpected-application-in-my-applications-list"></a>Nieoczekiwany aplikacji na liście aplikacji

W tym artykule pomocy toounderstand jak aplikacje pojawiają się w sieci **wszystkie aplikacje** w obszarze **aplikacje dla przedsiębiorstw**. 

## <a name="how-toosee-all-applications-in-your-tenant"></a>Jak toosee wszystkich aplikacji w Twojej dzierżawie

toosee hello wszystkich aplikacji w dzierżawie, należy toouse hello **filtru** kontroli tooshow **wszystkie aplikacje** w obszarze hello **wszystkie aplikacje** listy. toodo, wykonaj hello czynności:

1.  Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego** lub **ko-administratora.**

2.  Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.

3.  Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.

4.  Kliknij przycisk **aplikacje dla przedsiębiorstw** z menu nawigacji po lewej stronie powitania w usłudze Azure Active Directory.

5.  Kliknij przycisk **wszystkie aplikacje** tooview listę wszystkich aplikacji.

6.  Kliknij przycisk hello Użyj hello **filtru** kontroli u góry hello hello **listę wszystkich aplikacji**.

7.  Na powitania **filtru** bloku, zestaw hello **Pokaż** opcję zbyt**wszystkie aplikacje.**

## <a name="why-does-a-specific-application-appear-in-my-all-applications-list"></a>Dlaczego określonej aplikacji jest wyświetlany na liście wszystkie aplikacje

Gdy filtrowane zbyt**wszystkie aplikacje**, hello **wszystkie aplikacje** **listy** przedstawiono każdy obiekt nazwy głównej usługi w dzierżawie. Obiekty nazwy głównej usługi mogą być wyświetlane na liście na różne sposoby:

1.  Po dodaniu dowolną aplikację z galerii aplikacji hello, w tym:

   1. **Azure AD galerii aplikacji** — aplikację, która została wstępnie zintegrowanych dla rejestracji jednokrotnej z usługą Azure AD.

   2. **Aplikacje serwera Proxy aplikacji** — aplikacji działających w środowisku lokalnym, które mają tooprovide bezpiecznego jednokrotnego tooexternally.

   3. **Niestandardowe opracowanych aplikacji** — aplikacji, który organizacja chce toodevelop na hello platformę tworzenia aplikacji w usłudze Azure AD, ale który nie istnieje jeszcze.

   4. **Aplikacje inne niż galerii** — Przenoszenie własnych aplikacji! Wszelkie link sieci web, które mają lub dowolnej aplikacji, która renderuje pole nazwy użytkownika i hasła, obsługuje protokoły SAML lub OpenID Connect lub obsługuje SCIM, który ma toointegrate dla rejestracji jednokrotnej z usługą Azure AD.

2.  Gdy skorzystania lub zalogowaniu się do 3<sup>usług pulpitu zdalnego</sup> aplikacji zintegrowany z usługą Azure Active Directory. Przykładem tego jest [Smartsheet](https://app.smartsheet.com/b/home) lub [DocuSign](https://www.docusign.net/member/MemberLogin.aspx).

3.  Gdy skorzystania lub dodanie tooa licencji użytkownika lub grupy tooa pierwszej strony aplikacji, takich jak [Microsoft Office 365](http://products.office.com/).

4.  Po dodaniu nowej rejestracji aplikacji przez tworzenie aplikacji utworzonych niestandardowych za pomocą hello [rejestru aplikacji](https://docs.microsoft.com/azure/active-directory/active-directory-app-registration).

5.  Po dodaniu nowej rejestracji aplikacji przez tworzenie aplikacji utworzonych niestandardowych za pomocą hello [portalu rejestracji aplikacji w wersji 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-app-registration#visit-the-microsoft-app-registration-portal).

6.  Po dodaniu aplikacji tworzony jest przy użyciu programu Visual Studio [metod uwierzytelniania ASP.net](http://www.asp.net/visual-studio/overview/2013/creating-web-projects-in-visual-studio#orgauthoptions) lub [usług połączonych](http://blogs.msdn.com/b/visualstudio/archive/2014/11/19/connecting-to-cloud-services.aspx).

7.  Podczas tworzenia obiektu główną usługi za pomocą hello [modułu Azure AD PowerShell](/powershell/azure/install-adv2?view=azureadps-2.0).

8.  Gdy zostanie [zgody tooan aplikacji](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) jako dane toouse administratorem w dzierżawie.

9.  Gdy [użytkownik zgadza aplikacji tooan](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent) toouse danych w dzierżawie.

10. Po włączeniu pewnych usług, które przechowują dane w dzierżawie. Przykładem jest resetowania hasła, która ma formę jako toostore główna usługi resetowania hasła zasad bezpieczne.

Przeczytaj więcej szczegółów, w jaki aplikacje są dodawane katalogu tooyour tooget [jak i dlaczego aplikacje są dodawane tooAzure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-how-applications-are-added).

## <a name="i-want-tooremove-a-specific-users-or-groups-assignment-tooan-application"></a>Chcę tooremove określonego użytkownika lub grupy aplikacji tooan przypisania

tooremove użytkownika lub grupę przypisania tooan aplikację, wykonaj kroki hello na liście hello [Usuń przypisanie użytkownika lub grupy z aplikacji przedsiębiorstwa w usłudze Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-remove-assignment-azure-portal) artykułu.

## <a name="i-want-toodisable-all-access-tooan-application-for-every-user"></a>Chcę toodisable wszystkich aplikacji tooan dostępu dla każdego użytkownika

toodisable wszystkie użytkownika logowania tooan aplikacji, wykonaj kroki hello na liście hello [wyłączyć logowania użytkowników dla aplikacji przedsiębiorstwa w usłudze Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-disable-app-azure-portal) artykułu.

## <a name="i-want-toodelete-an-application-entirely"></a>Chcę całkowicie toodelete aplikacji

zbyt**usunąć aplikację**, postępuj zgodnie z poniższymi instrukcjami hello:

1.  Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego** lub **ko-administratora.**

2.  Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.

3.  Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.

4.  Kliknij przycisk **aplikacje dla przedsiębiorstw** z menu nawigacji po lewej stronie powitania w usłudze Azure Active Directory.

5.  Kliknij przycisk **wszystkie aplikacje** tooview listę wszystkich aplikacji.

  * Jeśli nie ma aplikacji hello mają być wyświetlane tutaj, użyj hello **filtru** kontroli u góry hello hello **listę wszystkich aplikacji** i zestaw hello **Pokaż** opcję zbyt **Wszystkie aplikacje.**

6.  Wybierz aplikację hello ma toodelete.

7.  Po załadowaniu aplikacji hello, kliknij przycisk **usunąć** ikony z aplikacji top hello **omówienie** bloku.

## <a name="i-want-toodisable-all-future-user-consent-operations-tooany-application"></a>Chcę toodisable wszystkie przyszłe użytkownika zgody operacji tooany aplikacji

Wyłączanie zgody użytkownika dla użytkowników końcowych z aplikacji tooany zgodę zapobiec całego katalogu. Administratorzy mogą nadal oznacza zgodę na behalves użytkownika. zgoda toolearn więcej informacji na temat aplikacji, oraz dlaczego może lub nie możesz toodo tego odczytu [zgody administratora i użytkownika opis](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent).

zbyt**Wyłącz wszystkie operacje zgody użytkownika w przyszłości w katalogu cały**, postępuj zgodnie z poniższymi instrukcjami hello:

1.  Otwórz hello [ **Azure Portal** ](https://portal.azure.com/) i zaloguj się jako **administratora globalnego.**

2.  Otwórz hello **rozszerzenia usług Azure Active Directory** klikając **więcej usług** u dołu menu nawigacji głównego po lewej stronie powitania hello.

3.  Wpisz w **"Azure Active Directory**" w polu wyszukiwania filtr hello a wybierz hello **usługi Azure Active Directory** elementu.

4.  Kliknij przycisk **użytkowników i grup** w menu nawigacji hello.

5.  Kliknij przycisk **ustawienia użytkownika**.

6.  Wyłącz wszystkie operacje zgody użytkownika w przyszłości przez ustawienie hello **użytkownicy mogą zezwolić aplikacji tooaccess swoje dane** Przełącz zbyt**nr** i kliknij przycisk hello **zapisać** przycisku.

## <a name="next-steps"></a>Następne kroki
[Zarządzanie aplikacjami przy użyciu usługi Azure Active Directory](active-directory-enable-sso-scenario.md)
