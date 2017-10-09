---
title: "Aplikacja rozszerzenia — usługa Azure AD B2C | Dokumentacja firmy Microsoft"
description: Przywracanie hello w b2c aplikacji rozszerzenia
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: f0392e32-0771-473c-a799-81438ca2bcff
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/17/2017
ms.author: parja
ms.openlocfilehash: b36410c18314bd893dc669b49814fdcd77fae054
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-extensions-app"></a>Usługa Azure AD B2C: Rozszerzeń aplikacji

Podczas tworzenia katalogu usługi Azure AD B2C aplikacja o nazwie `b2c-extensions-app. Do not modify. Used by AADB2C for storing user data.` jest tworzony automatycznie wewnątrz hello nowego katalogu. Tej aplikacji, hello określonego tooas **b2c rozszerzeń aplikacji**, jest widoczny w *rejestracji aplikacji*. Jest on używany przez hello Azure AD B2C usługi toostore informacje o użytkownikach i atrybuty niestandardowe. Usunięcie aplikacji hello Azure AD B2C nie będzie działać prawidłowo, i będzie mieć wpływ na środowisko produkcyjne.

> [!IMPORTANT]
> Nie należy usuwać hello w b2c aplikacji rozszerzenia, chyba że planujesz tooimmediately delete dzierżawy. Jeśli aplikacja hello pozostaje usunięte przez dłużej niż 30 dni, informacje o użytkowniku zostaną trwale utracone.

## <a name="verifying-that-hello-extensions-app-is-present"></a>Weryfikowanie, aplikacja rozszerzenia hello jest obecny

występuje tooverify, który hello b2c rozszerzeń aplikacji:

1. W dzierżawie usługi Azure AD B2C, kliknij **więcej usług** w menu nawigacji po lewej stronie powitania.
1. Wyszukaj i Otwórz **rejestracji aplikacji**.
1. Wyszukaj aplikację, która rozpoczyna się od **b2c rozszerzeń aplikacji**

## <a name="recover-hello-extensions-app"></a>Odzyskaj hello rozszerzeń aplikacji

Jeśli przypadkowo usunięte hello w b2c aplikacji rozszerzeń, masz toorecover 30 dni go. Możesz przywrócić aplikacji hello przy użyciu interfejsu API programu Graph hello:

1. Przeglądaj zbyt[https://graphexplorer.azurewebsites.net/](https://graphexplorer.azurewebsites.net/).
1. Zaloguj się w witrynie toohello jako administratora globalnego dla katalogu usługi Azure AD B2C hello interesujące aplikacja hello usunięte toorestore dla.
1. Wystawiać HTTP GET dla adresu URL hello `https://graph.windows.net/{tenantName}.onmicrosoft.com/deletedApplications` z interfejsu api-version = 1.6. Upewnij się, że tooreplace `{tenantName}` nazwą Twojej dzierżawy. Ta operacja spowoduje wyświetlenie listy wszystkich aplikacji hello, które zostały usunięte w ramach hello w ciągu ostatnich 30 dni.
1. Znajdź aplikacji hello liście hello gdzie hello nazwa rozpoczyna się od "ruch aplikacji b2c rozszerzenia" i skopiuj jej `objectid` wartości właściwości.
1. Wystawiać POST protokołu HTTP dla adresu URL hello `https://graph.windows.net/myorganization/deletedApplications/{OBJECTID}/restore`. Zastąp hello `{OBJECTID}` część adresu URL hello z hello `objectid` hello w poprzednim kroku. 

Powinny teraz być zbyt[aplikacja hello przywrócić](#verifying-that-the-extensions-app-is-present) w hello portalu Azure.

> [!NOTE]
> Aplikację można przywrócić tylko, jeśli został on usunięty w hello ostatnich 30 dni. Jeśli został on więcej niż 30 dni, dane zostaną trwale utracone. Aby uzyskać pomoc pliku biletu pomocy technicznej.
