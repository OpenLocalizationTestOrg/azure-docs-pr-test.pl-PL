---
title: "aaaFind się, kiedy określony użytkownik będą mogli tooaccess aplikacji | Dokumentacja firmy Microsoft"
description: "Jak toofind się, gdy użytkownik niezwykle ważne być tooaccess stanie aplikacji została skonfigurowana dla Inicjowanie obsługi użytkowników z usługą Azure AD"
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
ms.openlocfilehash: bb9520499dcc8bbbe6fae05c5238c8852815ea0a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="find-out-when-a-specific-user-will-be-able-tooaccess-an-application"></a>Ustalić, kiedy określony użytkownik będzie możliwe tooaccess aplikacji
Używając użytkownika automatycznego inicjowania obsługi administracyjnej za pomocą aplikacji, usługi Azure AD automatycznie udostępniania i aktualizowanie kont użytkowników w aplikacji na podstawie takich elementów, jak [przypisania użytkowników i grup](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) w odstępach zaplanowanego czasu, zazwyczaj co 10 minut.

## <a name="how-long-does-it-take"></a>Jak długo trwa?

Hello czas potrzebny toobe danego użytkownika, udostępnione zależy od głównie czy już wystąpił początkową synchronizację "pełnej".

Witaj pierwsza synchronizacja między usługą Azure AD i aplikacji może potrwać od godziny tooseveral 20 minut, w zależności od wielkości hello katalogu hello Azure AD i hello liczbę użytkowników w zakresie obsługi. 

Kolejne synchronizacje po początkowej synchronizacji hello przebiegać szybciej (np. w ciągu 10 minut), jak znaki wodne, przedstawiające stan hello obu systemów po początkowej synchronizacji hello, poprawa wydajności kolejne synchronizacje magazyny hello inicjowania obsługi usługi.

## <a name="how-toocheck-hello-status-of-a-user"></a>Jak toocheck hello stanu użytkownika

Stan inicjowania obsługi administracyjnej hello toosee dla wybranego użytkownika, należy skontaktować się hello dzienniki inspekcji w usłudze Azure AD.

Hello inicjowania obsługi dzienników inspekcji można uzyskać w portalu Azure w hello hello **usługi Azure Active Directory &gt; aplikacje przedsiębiorstwa &gt; \[Nazwa aplikacji\] &gt; dzienniki inspekcji**kartę. Filtr hello dzienniki na powitania **Inicjowanie obsługi konta** tooonly kategorii Zobacz hello inicjowania obsługi zdarzeń dla danej aplikacji. Można wyszukiwać użytkowników na podstawie hello "dopasowania Identyfikatora" skonfigurowanego dla nich w hello atrybutu mapowania. 

Na przykład, jeśli skonfigurowano hello "główna nazwa użytkownika" lub "adres e-mail" jako hello dopasowanie atrybutu na stronie powitania usługi Azure AD, a użytkownik hello udostępniania nie ma wartość "audrey@contoso.com", następnie dzienniki inspekcji hello wyszukiwania dla"audrey@contoso.com", a następnie przejrzyj zwracane wpisy.

Witaj udostępniania inspekcji rejestruje rekord hello wszystkie operacje wykonywane przez hello inicjowania obsługi usługi, w tym:

* Podczas badania usługi Azure AD dla przypisanych użytkowników, które znajdują się w zakresie alokacji
* Wykonywanie zapytania hello docelowej aplikacji hello istnienia tych użytkowników
* Porównanie obiektów użytkownika hello między hello systemu
* Dodawanie, aktualizowanie lub wyłączanie hello konta użytkownika w systemie docelowym hello na podstawie porównania hello

## <a name="next-steps"></a>Następne kroki
[Automatyzowanie Inicjowanie obsługi użytkowników i anulowania zastrzeżenia tooSaaS aplikacji za pomocą usługi Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-saas-app-provisioning)''
