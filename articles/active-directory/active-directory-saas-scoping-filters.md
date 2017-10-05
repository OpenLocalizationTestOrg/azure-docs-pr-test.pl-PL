---
title: "Inicjowanie obsługi aplikacji z filtrami zakresów | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak używać filtrów zakresu, aby zapobiec obiektów w aplikacji, które obsługują Inicjowanie obsługi użytkowników automatycznych z faktycznie obsługiwana administracyjnie, jeśli obiekt nie spełniają wymagań biznesowych."
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
ms.openlocfilehash: 109635052e2ded33831b050eb12d50745944091b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="attribute-based-application-provisioning-with-scoping-filters"></a>Udostępniania aplikacji na podstawie atrybutów z filtrami zakresów
Celem tej sekcji jest wyjaśnienie, jak używać filtrów zakresu do definiowania reguł na podstawie atrybutów, które określają, użytkowników, którzy są udostępnione do aplikacji.

## <a name="clauses-and-scope-groups"></a>Klauzule i zakres grupy
![Filtr zakresów][1] 

Filtry zakresu są zdefiniowane przez jedną lub więcej **zakres grupy**, każdy z która zawiera jedną lub więcej **klauzule**. Aby wyświetlić klauzule dla określonego zakresu grupy, rozwiń węzeł, klikając strzałkę w lewo nazwę grupy.

A **klauzuli** określa użytkowników, którzy mogą przekazywać zakresu filtru wyniku obliczenia atrybutów każdego użytkownika. Na przykład może być jedną klauzulę, która wymaga atrybutu 'state' użytkownika równa Nowym Jorku, dzięki udostępnieniu tylko użytkownicy z nowego Jorku do aplikacji.

![Nazwa grupy ustalania zakresu][2] 

Każdy **grupy zakresu** rozpoczynają się od jednego obowiązkowe **klauzuli**, jak pokazano na zrzucie ekranu powyżej. Po prostu klauzulę stwierdza, że użytkownik należy przypisać do aplikacji przed jej jest oceniana przez filtry zakresu. Klauzulę nie można usunąć lub zmodyfikować.

Naciskając odpowiedni przycisk, można dodać nowe klauzule lub nowych grup zakresu. Można nadać każdej grupy zakresu nazwę, edytując jej **Nazwa grupy zakresu** właściwości.

## <a name="how-scoping-filters-are-evaluated"></a>Jak są analizowane filtry zakresu
Podczas inicjowania obsługi, firma Microsoft testuje co przypisany użytkownik względem filtry zakresu, aby ustalić, czy ten użytkownik wymaga dostępu do aplikacji. Można potraktować każdej klauzuli jako testu, które muszą być przekazywane w kolejności dla użytkownika uniknąć pobierania odfiltrowane. 

Jeśli masz wiele zdefiniowanych grup zakresu, każdy użytkownik musi przejść pomyślnie co najmniej jeden z nich, aby uzyskać dostęp do aplikacji. Jednak w poszczególnych grupach zakresu, użytkownik musi mieć co klauzuli do przekazania tej grupy określonego zakresu. 

Innymi słowy, można traktować zakres grupy jako połączone funkcją logiczną lub uważasz klauzul w nich jako i połączone funkcją logiczną. Rozważmy na przykład Filtr zakresu poniżej:

![Nazwa grupy ustalania zakresu][3]  

Zgodnie z tego zakresu filtru użytkownicy muszą spełniać następujące kryteria, można zainicjować obsługi administracyjnej:

1. Należy do nich przypisać do aplikacji.
2. Muszą one pracować z działu inżynierii
3. Muszą one być pracy w sieci San Francisco lub Kanady.

## <a name="related-articles"></a>Pokrewne artykuły
* [Indeks artykułów dotyczących zarządzania aplikacjami w usłudze Azure Active Directory](active-directory-apps-index.md)
* [Automatyzowanie użytkownika alokowania i anulowania alokowania do aplikacji SaaS](active-directory-saas-app-provisioning.md)
* [Dostosowywanie mapowań atrybutów do inicjowania obsługi użytkowników](active-directory-saas-customizing-attribute-mappings.md)
* [Tworzenie wyrażeń na potrzeby mapowań atrybutów](active-directory-saas-writing-expressions-for-attribute-mappings.md)
* [Powiadomienia aprowizacji kont](active-directory-saas-account-provisioning-notifications.md)
* [Włączanie automatycznej aprowizacji użytkowników i grup z usługi Azure Active Directory do aplikacji przy użyciu SCIM](active-directory-scim-provisioning.md)
* [Lista samouczków dotyczących sposobów integracji aplikacji SaaS](active-directory-saas-tutorial-list.md)

<!--Image references-->
[1]: ./media/active-directory-saas-scoping-filters/ic782811.png
[2]: ./media/active-directory-saas-scoping-filters/ic782812.png
[3]: ./media/active-directory-saas-scoping-filters/ic782813.png
