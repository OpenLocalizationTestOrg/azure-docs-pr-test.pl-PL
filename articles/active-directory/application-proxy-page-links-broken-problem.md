---
title: "aaaLinks na stronie powitania nie działają dla aplikacji serwera Proxy aplikacji | Dokumentacja firmy Microsoft"
description: "Jak tootroubleshoot problemy związane z uszkodzonych łączy w przypadku aplikacji serwera Proxy aplikacji, który jest zintegrowany z usługą Azure AD"
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
ms.openlocfilehash: 77c1e22d27c7a6436d8e57e105037c2328180481
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="links-on-hello-page-dont-work-for-an-application-proxy-application"></a>Łącza na stronie powitania nie działają dla aplikacji serwera Proxy aplikacji

W tym artykule pomocy tootroubleshoot Dlaczego łącza dla aplikacji serwera Proxy usługi Azure Active Directory aplikacji nie działa prawidłowo.

## <a name="overview"></a>Omówienie 
Po opublikowaniu aplikacji serwera Proxy aplikacji, linki tylko hello czy pracy domyślnie w aplikacji hello są zawarte w hello toodestinations łącza opublikowane głównego adresu URL. Hello łączy w obrębie aplikacji hello nie działają, hello wewnętrzny adres URL dla aplikacji hello prawdopodobnie nie zawiera wszystkich hello miejsc docelowych łączy w obrębie aplikacji hello.

**Dlaczego to możliwe?** Po kliknięciu linku w aplikacji, serwer Proxy aplikacji prób tooresolve hello URL jako wewnętrzne URL w hello sam aplikację, lub jako adres URL dostępny zewnętrznie. Jeśli hello link wskazuje tooan wewnętrzny adres URL, który nie jest w hello same należy tooeither tych zasobników i nie powoduje błędu nie znaleziono aplikacji.

## <a name="ways-you-can-resolve-broken-links"></a>Sposoby, możesz rozwiązać przerwane łącza

Istnieją trzy sposoby tooresolve ten problem. Hello poniżej są wymienione w rosnącej złożoności.

1.  Upewnij się, że głównego, który zawiera wszystkie hello łącza do aplikacji hello jest hello wewnętrznego adresu URL. Dzięki temu wszystkie toobe łącza rozpoznać publikowanej zawartości w ramach hello sam aplikacji.

    Jeśli zmiany hello wewnętrznego adresu URL, ale nie mają hello toochange początkowej strony dla użytkowników, zmień hello adres URL strony głównej toohello wcześniej publikowane wewnętrznego adresu URL. Można to zrobić, przechodząc zbyt "Azure Active Directory" -&gt; rejestracji aplikacji -&gt; wybierz aplikacja hello —&gt; właściwości. Na tej karcie właściwości jest widoczny hello pole "adres URL strony głównej", który można dostosować toobe hello potrzeby strony docelowej.

2.  Jeśli aplikacje Użyj w pełni kwalifikowanych nazw domen (FQDN), użyj [domen niestandardowych](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains) toopublish aplikacji. Ta funkcja umożliwia hello tego samego adresu URL toobe używana zarówno wewnętrznie i zewnętrznie.

    Tej opcji zapewnia, że hello łącza do aplikacji są dostępne z zewnątrz za pośrednictwem serwera Proxy aplikacji, ponieważ hello łączy w obrębie adresu URL toointernal aplikacji hello również są rozpoznawane zewnętrznie. Należy pamiętać, że wszystkie linki nadal potrzebujesz toobelong tooa opublikowana aplikacja. Z tej opcji hello łącza muszą jednak toobelong toohello tej samej aplikacji i może należeć toomultiple aplikacji.

3.  Jeśli żadna z tych opcji jest to możliwe, przyłącz się podgląd hello nowa funkcja, która Wykonaj translację/poprawiania adresu URL. Po wybraniu tej opcji wewnętrzne adresy URL lub łącza, który istnieje w treści hello HTML w aplikacji można przetłumaczyć lub "mapowane", toohello opublikowane zewnętrzne adresy URL serwera Proxy aplikacji. Działa to tylko w przypadku łączy w hello HTML i CSS, a to pomaga czy łącze jest generowany przez JS. 

W związku z tym zdecydowanie zaleca się używanie hello [domen niestandardowych](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains) rozwiązanie, jeśli to możliwe. Jeśli mają toojoin hello podglądu, Wyślij wiadomość e-mail < aadapfeedback@microsoft.com > z hello applicationId(s).

## <a name="next-steps"></a>Następne kroki
[Praca z istniejącym lokalnych serwerów proxy](application-proxy-working-with-proxy-servers.md)

