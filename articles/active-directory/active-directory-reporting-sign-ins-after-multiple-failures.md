---
title: aaaSign ins po wielokrotnych niepowodzeniach
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
ms.openlocfilehash: 48d137dc3abf65287cb3b9ba8a6ff10340f6741f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="sign-ins-after-multiple-failures"></a>Logowania po wielokrotnych niepowodzeniach
Ten raport wskazuje użytkowników, którzy mają pomyślnie zalogował się po wiele kolejnych logowania nie powiodła się podczas prób. Możliwe przyczyny:

* Użytkownik miał zapomniane hasła</li><li>Użytkownik jest ofiarą hello odgadnięcie ataków siłowych hasła powiodło się

Ten raport zostanie w wynikach hello wiele kolejnych nieudanych prób logowania wprowadzone toohello wcześniejszego pomyślnego logowania i sygnatura czasowa skojarzona hello pierwszego pomyślnego logowania.

**Raport ustawienia**: hello minimalną liczbę kolejnych nieudanych logowania można skonfigurować w prób, które musi wystąpić, zanim mogą być wyświetlane w raporcie hello. Po wprowadzeniu zmian jest toothis ustawieniem dla niego toonote ważne, czy te zmiany nie zostaną zastosowane tooany istniejących nie powiodło się logowania, które aktualnie wyświetlane w raporcie istniejących. Jednak zostaną one zastosowane tooall przyszłych logowania. Raport o zmianach toothis może zawierać tylko przez administratorów licencjonowane.

![Logowania po wielokrotnych niepowodzeniach](./media/active-directory-reporting-sign-ins-after-multiple-failures/signInsAfterMultipleFailures.PNG)

