---
title: "aplikacje aaaProvisioning z filtrami zakresów | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak zakres toouse filtry tooprevent obiektów w aplikacji, które obsługują Inicjowanie obsługi użytkowników automatycznych z faktycznie obsługiwana administracyjnie, jeśli obiekt nie spełniają wymagań biznesowych."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: bcfbda74-e4d4-4859-83bc-06b104df3918
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: markvi
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f0299390dc3fdb70aa9d271e835069a08827d635
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="attribute-based-application-provisioning-with-scoping-filters"></a>Udostępniania aplikacji na podstawie atrybutów z filtrami zakresów
Celem Hello w tej sekcji jest tooexplain sposób określania zakresu toouse filtry toodefine atrybut reguły określające, którzy użytkownicy są udostępniane toohello aplikacji.

## <a name="clauses-and-scope-groups"></a>Klauzule i zakres grupy
![Filtr zakresów][1] 

Filtry zakresu są zdefiniowane przez jedną lub więcej **zakres grupy**, każdy z która zawiera jedną lub więcej **klauzule**. klauzule hello toosee dla określonego zakresu grupy, rozwiń ją, klikając hello Strzałka toohello po lewej stronie powitania grupy nazwy.

A **klauzuli** Określa, które użytkownicy mogą toopass za pośrednictwem hello zakresu filtru wyniku obliczenia atrybutów każdego użytkownika. Na przykład może zajść jedną klauzulę, który wymaga, aby użytkownika 'state' atrybutów równy Nowym Jorku, więc tylko użytkownicy z nowego Jorku są udostępnione do aplikacji hello.

![Nazwa grupy ustalania zakresu][2] 

Każdy **grupy zakresu** rozpoczynają się od jednego obowiązkowe **klauzuli**, jak pokazano na powitania zrzucie ekranu pokazano powyżej. Klauzulę po prostu z informacją, że użytkownik hello należy przypisać toohello aplikacji przed jej jest oceniana przez filtry zakresu. Klauzulę nie można usunąć lub zmodyfikować.

Naciskając przycisk odpowiednie hello można dodać nowe klauzule lub nowych grup zakresu. Można nadać każdej grupy zakresu nazwę, edytując jej **Nazwa grupy zakresu** właściwości.

## <a name="how-scoping-filters-are-evaluated"></a>Jak są analizowane filtry zakresu
Podczas inicjowania obsługi, firma Microsoft testuje co przypisany użytkownik względem z zakresu toodetermine filtrów, jeśli użytkownik wymaga dostępu toohello aplikacji. Można potraktować każdej klauzuli jako test, który musi zostać przekazane, tooavoid użytkownika hello pobierania odfiltrowane. 

Jeśli masz wiele zdefiniowanych grup zakresu, każdy użytkownik musi przejść pomyślnie co najmniej jeden z nich tooaccess aplikacji hello. W każdej grupie zakresu jednak hello użytkownik musi mieć co toopass klauzuli tej grupy określonego zakresu. 

Innymi słowy, można traktować zakres grupy jako połączone funkcją logiczną lub można traktować klauzule hello w nich jako i połączone funkcją logiczną. Rozważmy na przykład hello zakresu filtru poniżej:

![Nazwa grupy ustalania zakresu][3]  

Zgodnie z toothis zakresu filtru, użytkownicy muszą spełniać następujące hello kryteria, toobe obsługi administracyjnej:

1. Musi mieć przypisaną toohello aplikacji.
2. Muszą one działać działu inżynierii hello
3. Muszą one być pracy w sieci San Francisco lub Kanady.

## <a name="related-articles"></a>Pokrewne artykuły
* [Indeks artykułów dotyczących zarządzania aplikacjami w usłudze Azure Active Directory](active-directory-apps-index.md)
* [Automatyzowanie Inicjowanie obsługi użytkowników i anulowania zastrzeżenia tooSaaS aplikacji](active-directory-saas-app-provisioning.md)
* [Dostosowywanie mapowań atrybutów do inicjowania obsługi użytkowników](active-directory-saas-customizing-attribute-mappings.md)
* [Tworzenie wyrażeń na potrzeby mapowań atrybutów](active-directory-saas-writing-expressions-for-attribute-mappings.md)
* [Powiadomienia aprowizacji kont](active-directory-saas-account-provisioning-notifications.md)
* [Przy użyciu SCIM tooenable automatyczne Inicjowanie obsługi użytkowników i grup z usługi Azure Active Directory tooapplications](active-directory-scim-provisioning.md)
* [Lista samouczków dotyczących tooIntegrate aplikacji SaaS](active-directory-saas-tutorial-list.md)

<!--Image references-->
[1]: ./media/active-directory-saas-scoping-filters/ic782811.png
[2]: ./media/active-directory-saas-scoping-filters/ic782812.png
[3]: ./media/active-directory-saas-scoping-filters/ic782813.png
