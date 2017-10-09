---
title: "Azure AD Connect: Jeśli już masz usługi Azure AD | Dokumentacja firmy Microsoft"
description: "W tym temacie opisano sposób łączenia podczas toouse masz istniejącej dzierżawy usługi Azure AD."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: f7b166e9e85c1f03330e8e0074d4afa4036738c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-when-you-have-an-existent-tenant"></a>Azure AD Connect: Jeśli masz dzierżawę istniejących
Większość hello tematy dotyczące sposobu toouse Azure AD Connect przyjęto założenie, możesz zaczynać nowej usługi Azure AD dzierżawy i czy ma żadnych użytkowników lub istnieją inne obiekty. Ale jeśli została uruchomiona z dzierżawy usługi Azure AD wypełnić go użytkowników i innych obiektów, a teraz ma toouse Connect, a następnie w tym temacie jest dla Ciebie.

## <a name="hello-basics"></a>podstawy Hello
Obiekt w usłudze Azure AD albo jest zarządzany w hello chmury (Azure AD) lub lokalnie. Dla jednego pojedynczego obiektu nie może zarządzać niektóre atrybuty lokalnymi i niektórych innych atrybutów w usłudze Azure AD. Każdy obiekt ma flagę wskazującą, w którym obiekt hello jest obsługiwany.

W chmurze hello można zarządzać niektórych użytkowników lokalnych i inne. Typowy scenariusz dla tej konfiguracji jest organizacji z różnych kont pracowników i pracowników sprzedaży. Witaj kont pracowników ma lokalnego konta AD, ale pracownicy sprzedaży hello nie, użytkownicy mają konta w usłudze Azure AD. Czy zarządzanie niektórych użytkowników lokalnych, a niektóre w usłudze Azure AD.

Jeśli rozpoczęto toomanage użytkowników w usłudze Azure AD, które są również w lokalnej usłudze AD i później mają toouse Connect, a następnie istnieją pewne dodatkowe problemy potrzebne tooconsider.

## <a name="sync-with-existing-users-in-azure-ad"></a>Synchronizacja istniejących użytkowników w usłudze Azure AD
Po zainstalowaniu usługi Azure AD Connect i rozpoczęciem tej synchronizacji, hello usługi Azure AD sync (w usłudze Azure AD) sprawdza co nowego obiektu i spróbuj toofind istniejących toomatch obiektu. Istnieją trzy atrybuty stosowane do tego procesu: **userPrincipalName**, **proxyAddresses**, i **sourceAnchor**/**nazwę immutableID** . Dopasowanie w **userPrincipalName** i **proxyAddresses** nosi nazwę **nietrwałego dopasowania**. Dopasowanie w **sourceAnchor** nosi nazwę **twardych dopasowania**. Dla hello **proxyAddresses** tylko hello wartość z atrybutu **SMTP:**, który będzie hello podstawowego adresu e-mail, zostanie użyta do oceny hello.

dopasowanie Hello tylko jest sprawdzany pod kątem nowych obiektów pochodzących z Connect. W przypadku zmiany istniejących obiektu tak ją jest zgodne z żadnym z tych atrybutów, następnie zostanie wyświetlony błąd zamiast tego.

Jeśli usługi Azure AD znajdzie obiektu, gdy wartości atrybutów hello są hello tego samego obiektu pochodzących z Connect i który znajduje się już w usłudze Azure AD, a następnie hello obiektu w usłudze Azure AD zostanie przejęty Connect. Witaj wcześniej obiektu zarządzanymi w chmurze z flagą zarządzać lokalnymi. Wszystkie atrybuty w usłudze Azure AD z wartością w lokalnym programie AD zostaną zastąpione wartość lokalne powitania. wyjątek Hello jest po atrybucie **NULL** wartości lokalnej. W takim przypadku wartość hello pozostaje usługi Azure AD, ale można nadal zmienić tylko lokalnymi toosomething else.

> [!WARNING]
> Ponieważ wszystkie atrybuty w usłudze Azure AD będą toobe zastąpione przez wartość lokalne powitania, upewnij się, że masz dobrej danych w sieci lokalnej. Na przykład jeśli tylko udało adres e-mail w usłudze Office 365, a nie przechowywane zaktualizowane w lokalnych usług AD DS, utracisz wszystkie wartości w usłudze Azure AD/usługi Office 365 nie znajduje się w usługach AD DS, a następnie.

> [!IMPORTANT]
> Jeśli użyciu synchronizacji haseł, które jest używane przez ustawień ekspresowych, a następnie hello hasła w usłudze Azure AD jest zastępowany hello hasła w lokalnej usługi AD. Jeśli użytkownicy są toomanage używane różne hasła, wówczas należy tooinform hello je, które powinny używać lokalnego hasła po zainstalowaniu Connect.

w procesie planowania należy rozważyć Hello w poprzedniej sekcji i ostrzeżenia. Jeśli wprowadzono wiele zmian w usłudze Azure AD nie zostaną uwzględnione w lokalnych usług AD DS, a następnie należy tooplan jak toopopulate usług AD DS z hello aktualizacji wartości przed synchronizacją obiektów z programem Azure AD Connect.

Jeśli dopasowane obiektów z soft-match, następnie hello **sourceAnchor** są dodawane toohello obiektu w usłudze Azure AD, dzięki czemu można następnie używać twardych dopasowania.

### <a name="hard-match-vs-soft-match"></a>Twarde dopasowania vs Soft-match
Nowa instalacja programu Connect należy nie ma różnic praktyczne między soft - i twardych dopasowania. Różnica Hello jest w sytuacji odzyskiwania po awarii. Jeśli zgubisz serwera z usługą Azure AD Connect, można ponownie zainstalować nowego wystąpienia bez utraty danych. Obiekt o sourceAnchor jest wysyłane tooConnect podczas początkowej instalacji. Hello dopasowania może następnie przyjąć przez klienta hello (Azure AD Connect), co jest znacznie szybsze niż to samo Witaj w usłudze Azure AD. Twarde dopasowanie jest oceniany zarówno połączenia, jak i przez usługę Azure AD. Elastyczne dopasowanie jest tylko obliczane przez usługę Azure AD.

### <a name="other-objects-than-users"></a>Innych obiektów niż użytkowników
Użytkownicy zwykle mają userPrincipalName jak proxyAddresses, dzięki łatwo hello dopasowania. Jednak inne obiekty, takie jak grupy zabezpieczeń nie są one. W takim przypadku może wyłącznie odpowiadać na dopasowanie twardych przy użyciu hello sourceAnchor. Hello sourceAnchor jest zawsze hello przekonwertować Base64 **objectGUID** lokalnego, dlatego należy zaktualizować wartość hello w usłudze Azure AD, gdy są potrzebne dwa obiekty toomatch. sourceAnchor Hello/nazwę immutableID mogą być aktualizowane tylko przy użyciu programu PowerShell, a nie za pośrednictwem hello portali.

## <a name="create-a-new-on-premises-active-directory-from-data-in-azure-ad"></a>Tworzenie nowej lokalnej usługi Active Directory na podstawie danych w usłudze Azure AD
Niektórzy klienci rozpoczynać się tylko na chmurze rozwiązanie z usługą Azure AD i nie mają lokalnego AD. Później mają tooconsume lokalnymi zasobami i mają toobuild lokalnej usługi AD w oparciu dane usługi Azure AD. Azure AD Connect nie może pomóc w tym scenariuszu. Nie tworzy użytkowników lokalnych i nie ma żadnych możliwości tooset hello hasło lokalne toohello sam jak w usłudze Azure AD.

Jeśli przyczyna tylko hello Dlaczego planujesz tooadd lokalnej usługi AD jest toosupport obiektów LOB (aplikacji biznesowych z), a następnie może być należy rozważyć toouse [usługi domenowe Azure AD](../../active-directory-domain-services/index.md) zamiast tego.

## <a name="next-steps"></a>Następne kroki
Dowiedz się więcej na temat [integrowania tożsamości lokalnych z usługą Azure Active Directory](active-directory-aadconnect.md).
