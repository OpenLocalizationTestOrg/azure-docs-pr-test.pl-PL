---
title: "Strona aaaApplication nie są wyświetlane poprawnie dla aplikacji serwera Proxy aplikacji | Dokumentacja firmy Microsoft"
description: "Wskazówki dotyczące po stronie powitania nie jest prawidłowo wyświetlane w aplikacji serwer Proxy aplikacji jest zintegrowany z usługą Azure AD"
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
ms.openlocfilehash: f4abaa4e94c512868f2085affe59cac443784a56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="application-page-does-not-display-correctly-for-an-application-proxy-application"></a>Strona aplikacji nie są wyświetlane poprawnie dla aplikacji serwera Proxy aplikacji

W tym artykule pomocy tootroubleshoot problemy z aplikacjami serwera Proxy usługi Azure Active Directory aplikacji po przejściu toohello strony, ale coś na stronie powitania wygląda prawidłowe.

## <a name="overview"></a>Omówienie
Podczas publikowania aplikacji serwera Proxy aplikacji tylko strony w katalogu głównym są dostępne podczas uzyskiwania dostępu do aplikacji hello. Jeśli na stronie powitania nie jest wyświetlane prawidłowo, hello głównego wewnętrzny adres URL użyty dla aplikacji hello może brakować niektórych zasobów strony. tooresolve, upewnij się, że po opublikowaniu *wszystkie* hello zasobów na stronie powitania w ramach aplikacji.

Możesz sprawdzić to problemu hello otwierając tracker Twojej sieci (takie jak Fiddler lub F12 narzędzia w Internet Explorer/krawędzi), ładowanie strony hello i wyszukiwanie błędów 404. Wskazująca hello strony, które aktualnie nie można odnaleźć i może być konieczne toobe opublikowane.

Na przykład ten przypadek założono po opublikowaniu aplikacji kosztów przy użyciu wewnętrznego adresu URL z <http://myapps/expenses>, ale aplikacja hello korzysta z arkusza stylów hello <http://myapps/style.css>. W takim przypadku arkusza stylów hello nie jest opublikowana w aplikacji, więc ładowania aplikacji kosztów hello zgłosić błąd 404 podczas style.css tooload w trakcie. W tym przykładzie będzie można rozwiązać problemu hello, publikując aplikacji hello z wewnętrzny adres URL <http://myapp/> zamiast tego.

## <a name="problems-with-publishing-as-one-application"></a>Problemy z publikowaniem jako jedną aplikację

Jeśli nie jest możliwe toopublish wszystkie zasoby w hello tej samej aplikacji, należy toopublish wiele aplikacji i włączyć łącza między nimi.

toodo tak, zaleca się używanie hello [domen niestandardowych](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains) rozwiązania. Jednak to rozwiązanie wymaga własnej hello certyfikat dla domeny i aplikacji użyj w pełni kwalifikowanych nazw domen (FQDN). Inne opcje, zobacz hello [Rozwiązywanie problemów z dokumentacji uszkodzonych łączy](https://microsoft-my.sharepoint.com/personal/harshja_microsoft_com/_layouts/15/guestaccess.aspx?guestaccesstoken=IxuG3mFVbnPWI3Yn4Qi7wCNi8VIfHS5mwPt5quh8DMw%3d&docid=2_14558cd6ddea34c1c9887dc640feb5831&rev=1).

## <a name="next-steps"></a>Następne kroki
[Publikowanie aplikacji przy użyciu serwera Proxy aplikacji usługi Azure AD](application-proxy-publish-azure-portal.md)
