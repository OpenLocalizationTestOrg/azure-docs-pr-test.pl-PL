---
title: "aaaSave wyszukiwania i zasobów danych numeru pin w usłudze Azure Data Catalog | Dokumentacja firmy Microsoft"
description: "Jak tooarticle wyróżnienia możliwości w wykazie danych Azure zapisywania źródła danych i zasobów danych do późniejszego użycia."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: 6bd00a81-820d-4b7c-91fa-ab09e575474c
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: 0ad0a31d4b84782fed9d80acc2734912eecd6d74
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="save-searches-and-pin-data-assets-in-azure-data-catalog"></a>Zapisz wyszukiwanie i zasobów danych numeru pin w wykazie danych Azure
## <a name="introduction"></a>Wprowadzenie
Azure Data Catalog oferuje możliwości dla odnajdywanie źródła danych. Można szybko wyszukiwania i filtrowania źródeł danych toolocate katalogu hello i zrozumieć ich przeznaczenie, dzięki czemu łatwiej toofind hello odpowiednich danych dla wykonywanego zadania hello.

Ale co zrobić, jeśli należy tooregularly pracować z hello same dane? I co zrobić, jeśli użytkownicy będą mieli regularnie współtworzenia toohello Twojej wiedzy tych samych źródeł danych w katalogu hello? W takich przypadkach o problem toorepeatedly hello same wyszukiwania może być mało wydajne. Jest to, gdzie zapisanego wyszukiwania i zasobów danych przypięte może pomóc.

## <a name="saved-searches"></a>Zapisane wyszukiwania
Zapisane wyszukiwanie w wykazie danych jest wielokrotnego użytku, definicji wyszukiwania dla poszczególnych użytkowników. Można zdefiniować wyszukiwania, w tym terminy wyszukiwania, znaczników i inne filtry i zapisz go. Można ponownie uruchomić hello zapisane wyszukiwania definicji tooreturn nowsze żadnych zasobów danych, które pasują do jej kryteriów wyszukiwania.

### <a name="create-a-saved-search"></a>Utwórz zapisanego wyszukiwania
zapisane wyszukiwanie toocreate hello następujące:
1. W portalu Azure Data Catalog hello w hello **bieżące wyszukiwanie** okna, kliknij przycisk **zapisać**. 

    ![Bieżące łącze Zapisz ustawienia wyszukiwania](./media/data-catalog-how-to-save-pin/01-save-option.png) 

2. Wprowadź kryteria wyszukiwania hello mają tooreuse, a następnie kliknij przycisk **zapisać**.

    ![Nazwa wyszukiwania zapisać bieżące ustawienia wyszukiwania](./media/data-catalog-how-to-save-pin/02-name.png)

3. Po wyświetleniu monitu wprowadź nazwę dla zapisanego wyszukiwania hello. Wybierz nazwę opisową i opisujący hello zasobów danych, które zostaną zwrócone przez wyszukiwanie hello.

### <a name="manage-saved-searches"></a>Zarządzanie zapisanych wyszukiwań
Po zapisaniu jednego lub więcej wyszukiwań **zapisane wyszukiwania** opcja jest wyświetlana poniżej hello **bieżące wyszukiwanie** pole. Po rozwinięciu listy hello są wyświetlane wszystkie zapisane wyszukiwania.

 ![Lista zapisanych wyszukiwań](./media/data-catalog-how-to-save-pin/03-list.png)

Wykonaj jedną z następujących hello:

* tooexecute wyszukiwanie, wybierz listy hello zapisanego kryterium wyszukiwania.

* tooview listę opcje zarządzania dla zapisanego kryterium wyszukiwania, kliknij przycisk hello dół strzałkę dalej toohello alias.

    ![Opcje zarządzania zapisanych wyszukiwań](./media/data-catalog-how-to-save-pin/04-managing.png)

* Wybierz nową nazwę dla hello zapisane wyszukiwania, tooenter **zmienić**. Definicja wyszukiwania Hello nie ulega zmianie.

* tooremove hello zapisane wyszukiwania z listy, wybierz opcję **usunąć**, a następnie Potwierdź usunięcie hello.

* toomark hello zapisane wyszukiwanie jako wyszukiwania domyślne, wybierz opcję **Zapisz jako domyślne**. Jeśli wyszukiwaniu "pusty" ze strony głównej hello Azure Data Catalog, wyszukiwanie domyślny jest wykonywana. Ponadto hello wyszukiwania, który jest oznaczony jako hello domyślne wyszukiwanie jest wyświetlany u góry hello hello **zapisane wyszukiwania** listy.

### <a name="organizational-saved-searches"></a>Organizacyjnej zapisanych wyszukiwań
Wszystkich użytkowników w organizacji można zapisać wyszukiwanie na własny użytek. Administratorzy katalogu danych można także zapisać wyszukiwanie wszystkich użytkowników w organizacji hello. Gdy Administratorzy, Zapisz wyszukiwanie, są one dostępne z **udziału w firmie hello** opcji. Wybranie tego hello udziałów opcja zapisanego wyszukiwania dla wszystkich użytkowników w organizacji hello.

 ![Organizacyjnej zapisanych wyszukiwań](./media/data-catalog-how-to-save-pin/08-organizational-saved-search.png)

## <a name="pinned-data-assets"></a>Zasoby danych przypięte
Z zapisane wyszukiwania można zapisać i ponownie użyć definicji wyszukiwania. Hello zasobów danych, które są zwracane przez hello wyszukiwania może zmieniać się w czasie, gdy zawartość hello hello zmiany katalogu. Po przypięciu zasobów danych, można zidentyfikować jawnie toomake zasoby danych specyficznych dla ich łatwiejsze tooaccess bez konieczności toouse wyszukiwania.

Przypinanie zasobu danych jest prosta. Lista tooyour przypięty tooadd hello danych zasobów, należy po prostu kliknij hello **numeru pin** ikony. Witaj ikona jest wyświetlana w hello rogu hello zasobów kafelka w widoku tile hello i hello lewej kolumny w widoku listy hello w portalu Azure Data Catalog hello.

![ikonę pinezki Hello zasobów danych](./media/data-catalog-how-to-save-pin/05-pinning.png)

Cofnięcie unieruchomienia zasobu danych jest równie proste. Po prostu kliknij hello **odpiąć** ikona tootoggle hello ustawienie hello wybranych zasobów.

![Ikona odpiąć zasobu danych Hello](./media/data-catalog-how-to-save-pin/06-unpinning.png)

## <a name="hello-my-assets-section"></a>Witaj sekcji Moje zasoby
Witaj Data Catalog zawiera strony głównej portalu **Moje zasoby** sekcja, która zawiera zasoby odsetek toohello bieżącego użytkownika. Ta sekcja zawiera oba zasoby przypięty i zapisane wyszukiwania.

![Witaj sekcji Moje zasoby na stronie głównej hello](./media/data-catalog-how-to-save-pin/07-my-assets.png)

## <a name="summary"></a>Podsumowanie
Wykaz danych Azure zapewnia możliwości stał się łatwiejsze toodiscover hello źródeł danych, które chcesz dodać, innych członków organizacji może poświęcać mniej czasu wyszukiwania danych i więcej czasu korzystania z niego. Zapisane wyszukiwania i przypięty dane, które zasoby kompilacji na tych podstawowych możliwości, aby użytkownicy mogą łatwo zidentyfikować źródeł danych, które działają w systemie wielokrotnie.
