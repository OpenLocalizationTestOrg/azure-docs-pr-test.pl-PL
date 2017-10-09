---
title: "aaaManage zasobów danych w usłudze Azure Data Catalog | Dokumentacja firmy Microsoft"
description: "Artykuł Hello prezentuje sposób widoczność toocontrol i własności zasobów danych zarejestrowane w wykazie danych Azure."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: 623f5ed4-8da7-48f5-943a-448d0b7cba69
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: 48a634b92d7da19c32c9e551f295eec257f54f1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-data-assets-in-azure-data-catalog"></a>Zarządzać zasobami danych w wykazie danych Azure
## <a name="introduction"></a>Wprowadzenie
Azure Data Catalog jest przeznaczona dla źródła danych odnajdywania, dzięki czemu można łatwo odnaleźć i zrozumieć hello źródeł danych muszą tooperform analizy i podejmować decyzje. Te możliwości odnajdywania należy hello największy wpływ, gdy inni użytkownicy można odnaleźć i zrozumieć hello szerokiej gamy dostępnych źródeł danych. Z tych elementów na uwadze hello domyślne zachowanie usługi Data Catalog jest dla wszystkich zarejestrowanych danych źródeł toobe widoczne tooand wykrywalny przez wszystkich użytkowników wykazu.

Wykaz danych nie zapewnia dostępu toohello samych danych. Dostęp do danych jest kontrolowany przez właściciela hello hello źródła danych. Data Catalog można odnajdywania źródeł danych i wyświetlić metadane hello źródeł toohello powiązane, które są zarejestrowane w wykazie hello.

Może się zdarzyć, jednak gdzie źródeł danych tylko powinna być widoczna toospecific użytkowników lub toomembers określonych grup. W takich sytuacjach użytkownicy mogą przejąć na własność zasobów danych zarejestrowanych w wykazie hello i następnie ustawić widoczność hello hello zasobów, których są właścicielami.

> [!NOTE]
> Hello funkcji opisanych w tym artykule jest dostępna tylko w hello Standard Edition usługi Azure Data Catalog. Witaj bezpłatna wersja nie udostępnia możliwości własności i ograniczanie widoczności zasobów danych.
>
>

## <a name="manage-ownership-of-data-assets"></a>Zarządzanie własności zasobów danych
Domyślnie nieposiadanej są zasobów danych, które są zarejestrowane w wykazie danych. Każdy użytkownik posiadający uprawnienia tooaccess hello katalogu mogą odnaleźć i Adnotuj tych zasobów. Użytkownicy mogą przejąć na własność zasobów danych go i następnie ograniczyć widoczność hello zasoby hello, w których są właścicielami.

Gdy zasobu danych w katalogu danych jest właścicielem, tylko użytkownicy, którzy są autoryzowane przez właścicieli hello mogą odnaleźć hello zasobów i wyświetlić jej metadane i tylko właściciele hello można usunąć zasobów hello z katalogu hello.

> [!NOTE]
> Własność w wykazie danych ma wpływ na powitania metadane są przechowywane w katalogu hello. Własność nie przyznaje wszystkie uprawnienia na powitania źródła danych.
>
>

### <a name="take-ownership"></a>Przejmowanie na własność
Użytkownicy mogą przejąć prawo własności zasobów danych, wybierając hello **Przejmij na własność** opcji w portalu wykazu danych hello. Żadne specjalne uprawnienia są wymagane tootake własności zasobów danych go. Każdy użytkownik może przejąć na własność zasobów danych go.

### <a name="add-owners-and-co-owners"></a>Dodaj właścicieli i współwłaścicieli
Jeśli ma już właściciela zasobów danych, innych użytkowników nie wystarczy przejąć na własność. Muszą zostać dodane jako współwłaściciele przez istniejące właściciela. Wszelkie właściciela można dodać dodatkowych użytkowników lub grup zabezpieczeń jako współwłaściciele.

> [!NOTE]
> Jego jest najlepszym toohave praktyki co najmniej dwóch osób jako właściciele dla żadnego należące do zasobów danych.
>
>

### <a name="remove-owners"></a>Usuń właścicieli
Podobnie jak wszelkie właściciel zasobu może dodawać współwłaścicieli, wszelkie właściciel zasobu można usunąć wszelkie współwłaściciel.

Właściciel zasobu, która usuwa go lub siebie jako właściciela nie może dłużej zarządzać hello zasobów. Jeśli właściciel zasobu hello usuwa go lub siebie jako właściciela, nie ma żadnych wspólnej właścicieli zasobów hello przywraca tooan bez właściciela stanu.

## <a name="control-visibility"></a>Widoczność formantu
Właścicieli zasobu danych można ustawić widoczność hello hello zasobów danych, których są właścicielami. widoczność toorestrict jako domyślny hello, w przypadku, gdy wszystkie usługi Data Catalog użytkownicy mogą odnajdować i widoku hello zasobów danych, właściciel zasobu hello przełączać hello ustawienie widoczności z **wszyscy** zbyt**właściciele i następujący użytkownicy** we właściwościach hello hello trwałego. Następnie można dodać właścicieli, konkretnych użytkowników i grup zabezpieczeń.

> [!NOTE]
> Jeśli to możliwe, należy przydzielić uprawnienia własności i widoczność zasobów grup toosecurity i nie tooindividual użytkowników.
>
>

## <a name="catalog-administrators"></a>Administratorzy katalogu
Administratorzy katalogu danych są niejawnie współwłaściciele wszystkich zasobów w katalogu hello. Właściciele zawartości nie można usunąć widoczność administratorów, a administratorzy mogą zarządzać własności i widoczności dla wszystkich zasobów danych w katalogu hello.

## <a name="summary"></a>Podsumowanie
Hello Data Catalog crowdsourcing toometadata i dane zasobów odnajdowania modelu pozwala wszystkich toocontribute użytkownicy wykazu i odnajdywanie. Witaj Standard Edition usługi Data Catalog jest przeznaczona dla własności i zarządzania widoczność hello toolimit oraz korzystanie z zasobów określonych danych.
