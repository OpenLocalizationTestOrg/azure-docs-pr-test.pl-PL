---
title: "Sprawdzaj dostęp za pomocą usługi Azure AD dostęp przeglądami | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak i sprawdzaj dostęp przy użyciu przeglądami dostępu do usługi Azure Active Directory."
services: active-directory
author: markwahl-msft
manager: mtillman
editor: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/19/2017
ms.author: billmath
ms.openlocfilehash: 98658a2b9fdd0ede98b3f6c10a19af527a8677cc
ms.sourcegitcommit: e266df9f97d04acfc4a843770fadfd8edf4fa2b7
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/11/2017
---
# <a name="review-access-with-azure-ad-access-reviews"></a>Przejrzyj dostępu z usługą Azure AD dostęp do przeglądu

Azure Active Directory (Azure AD) upraszcza przedsiębiorstw zarządzanie dostępem do aplikacji i członkami grup w usłudze Azure AD i innych usług Microsoft Online Services przy użyciu funkcji o nazwie dostęp monitoruje. Prawdopodobnie odebrał wiadomość e-mail od firmy Microsoft z prośbą o Przejrzyj dostępu dla członków grupy lub użytkownicy z dostępem do aplikacji. 

## <a name="open-an-access-review"></a>Otwórz przegląd dostępu

Aby wyświetlić przeglądy oczekujące dostępu, wybierz łącze w wiadomości e-mail. Jeśli nie masz wiadomość e-mail, możesz znaleźć przeglądy dostępu, wykonaj następujące czynności:

1. Zaloguj się na [panel dostępu usługi Azure AD](https://myapps.microsoft.com).

2. Wybierz symbol użytkownika w prawym górnym rogu strony, która wyświetla nazwę i domyślny organizacji. Jeśli jest wymieniona więcej niż jednej z organizacji, wybierz żądany Przegląd dostępu organizacji.

3. Jeśli Kafelek z etykietą **dostępu przeglądami** znajduje się w prawej części strony, wybierz go. Jeśli Kafelek nie jest widoczny, nie ma żadnych przeglądami dostępu do wykonania dla tej organizacji, a w tej chwili nie jest potrzebne nie działanie.

## <a name="fill-out-an-access-review"></a>Wypełnianie Przegląd dostępu

Po wybraniu Przegląd dostępu z listy widać nazwy użytkowników, którzy wymagają przejrzenia. Może pojawić tylko jedną nazwę — własne — Jeśli żądanie zostało Aby przejrzeć swoje własne dostępu.

Dla każdego wiersza na liście można zdecydować, czy do zatwierdzenia lub odmowy dostępu. Wybierz wiersz i zdecyduj, czy chcesz zaakceptować lub odrzucić. (Jeśli nie znasz użytkownika, można wskazać, że zbyt.)

Osoba dokonująca przeglądu może wymagać, aby podać uzasadnienie zatwierdzanie nieprzerwanego dostępu lub członkostwa w grupie.

## <a name="next-steps"></a>Następne kroki

Użytkownikowi odmówiono dostępu nie są natychmiast usuwane. Można usunąć, po zakończeniu działania przeglądu, lub kiedy administrator przestaje przeglądu. Jeśli chcesz zmienić odpowiedź, a użytkownik wcześniej odmowy zatwierdzenia lub odmowy zatwierdzone wcześniej użytkownika, zaznacz wiersz, zresetuj odpowiedzi, a następnie wybierz nową odpowiedź. Aby wykonać ten krok, dopiero po zakończeniu Przegląd dostępu.



