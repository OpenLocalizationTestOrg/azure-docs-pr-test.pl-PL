---
title: Logowania z wielu lokalizacji geograficznych
description: "Raport, który wskazuje użytkowników, którego dwa logowania wydawały się następować z różnych regionów, a czas między logowaniami dodatki uniemożliwia użytkownikowi ma przemieścić między tymi lokalizacjami."
services: active-directory
documentationcenter: 
author: SSalahAhmed
manager: gchander
editor: 
ms.assetid: 79259c8a-2388-4747-b41e-c07434ea9a02
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/04/2016
ms.author: saah;kenhoff
ms.openlocfilehash: 1de57f64692ade442f9ef8d1e3b587ffee35d7cf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="sign-ins-from-multiple-geographies"></a>Logowania z wielu lokalizacji geograficznych
Ten raport zawiera pomyślnego logowania z użytkownikiem, gdzie dwa logowania wydawały się następować z różnych regionów, a czas między sesje logowania uniemożliwia użytkownik zdążył przemieścić się między tymi lokalizacjami. Możliwe przyczyny:

* Użytkownik udostępnia komuś swoje hasło z innymi użytkownikami
* Użytkownik korzysta z pulpitu zdalnego w celu uruchomienia przeglądarki sieci web dla logowania
* Haker zalogował się na konto użytkownika z innego kraju
* Użytkownik korzysta z sieci VPN lub serwer proxy
* Użytkownik jest zalogowany przy użyciu wielu urządzeń w tym samym czasie, takie jak pulpit i na telefon komórkowy i adres IP telefonu komórkowego jest rzadko używana.

Wyniki z tego raportu zostanie wyświetlona pomyślnego logowania zdarzenia, oraz czas między sesje logowania, regionów, w którym sesje logowania wydawały się następować z i podróży szacowany czas między tymi lokalizacjami. Podczas podróży, wyświetlane jest tylko szacowana i może różnić się od czasu rzeczywistego podróży między lokacjami.

![Logowania z wielu lokalizacji geograficznych](./media/active-directory-reporting-sign-ins-from-multiple-geographies/signInsFromMultipleGeographies.PNG)

