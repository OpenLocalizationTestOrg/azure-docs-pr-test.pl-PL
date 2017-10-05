---
title: Logowania po wielokrotnych niepowodzeniach
description: "Raport, który wskazuje użytkowników, którzy mają pomyślnie zalogował się po wiele kolejnych logowania nie powiodła się podczas prób."
services: active-directory
documentationcenter: 
author: SSalahAhmed
manager: femila
editor: 
ms.assetid: e4ec1a39-9c20-418f-8a75-6497d0117176
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/04/2016
ms.author: saah;kenhoff
ms.openlocfilehash: e55e0145adbdb1f41a8b8753d5555f20e96bf161
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="sign-ins-after-multiple-failures"></a>Logowania po wielokrotnych niepowodzeniach
Ten raport wskazuje użytkowników, którzy mają pomyślnie zalogował się po wiele kolejnych logowania nie powiodła się podczas prób. Możliwe przyczyny:

* Użytkownik miał zapomniane hasła</li><li>Użytkownik jest ofiarą odgadnięcie ukierunkowany hasła pomyślne wymusić ataków

Wyniki z tego raportu Pokaż liczbę kolejnych nieudanych prób logowania utworzone przed pomyślnym logowaniem i sygnaturę czasową skojarzone z pierwszego pomyślnego logowania.

**Raport ustawienia**: można skonfigurować minimalną liczbę kolejnych logowania nie powiodło się podczas prób, które musi wystąpić, zanim mogą być wyświetlane w raporcie. Możesz zmienić to ustawienie jest należy pamiętać, że te zmiany nie zostaną zastosowane do istniejącego logowania zakończonych niepowodzeniem ins który aktualnie wyświetlane w istniejącego raportu. Jednak zostaną one zastosowane do wszystkich przyszłych logowania. Zmiany w tym raporcie może zawierać tylko przez administratorów licencjonowane.

![Logowania po wielokrotnych niepowodzeniach](./media/active-directory-reporting-sign-ins-after-multiple-failures/signInsAfterMultipleFailures.PNG)

