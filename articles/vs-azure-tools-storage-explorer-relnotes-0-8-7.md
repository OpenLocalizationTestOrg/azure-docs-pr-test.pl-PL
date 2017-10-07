---
title: "aaaMicrosoft Eksploratora usługi Storage Azure 0.8.7 (wersja zapoznawcza) | Dokumentacja firmy Microsoft"
description: "Informacje o wersji dla Eksploratora usługi Microsoft Azure Storage 0.8.7 (wersja zapoznawcza)"
services: storage
documentationcenter: na
author: cawa
manager: paulyuk
editor: 
ms.assetid: 
ms.service: storage
ms.devlang: multiple
ms.topic: release-notes
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/18/2017
ms.author: cawa
ms.openlocfilehash: 9fdd491a3ea838e20f9d4f82c176cfb02fbe306b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-azure-storage-explorer-087-preview"></a>Eksplorator usługi Storage platformy Microsoft Azure 0.8.7 (wersja zapoznawcza)
## <a name="overview"></a>Omówienie
Ten artykuł zawiera informacje o wersji hello Eksploratora usługi Storage Azure 0.8.7 wersji zapoznawczej.

[Eksploratora usługi Microsoft Azure Storage (wersja zapoznawcza)](./vs-azure-tools-storage-manage-with-storage-explorer.md) jest aplikacją autonomiczną, która umożliwia tooeasily pracy z danymi usługi Azure Storage w systemie Windows, macOS i Linux.

## <a name="azure-storage-explorer-087-preview"></a>Eksplorator usługi Azure Storage 0.8.7 (wersja zapoznawcza)
### <a name="download-azure-storage-explorer-087-preview"></a>Pobierz Eksploratora usługi Azure Storage 0.8.7 (wersja zapoznawcza)
- [Podgląd Explorer 0.8.7 magazynu Azure dla systemu Windows](https://go.microsoft.com/fwlink/?LinkId=708343)
- [Podgląd Explorer 0.8.7 magazynu Azure dla komputerów Mac](https://go.microsoft.com/fwlink/?LinkId=708342)
- [Podgląd Explorer 0.8.7 magazynu Azure dla systemu Linux](https://go.microsoft.com/fwlink/?LinkId=722418)

### <a name="new-updates"></a>Nowe aktualizacje
* Można wybrać sposób pobrać tooresolve konfliktów na początku hello aktualizacji lub skopiuj sesji hello **działania** okna.
* Aktywuj kartę toosee hello pełną ścieżką hello zasobów magazynu.
* Gdy użytkownik kliknie kartę synchronizuje się z jego lokalizacji w okienku nawigacji po lewej stronie powitania.

### <a name="fixes"></a>Poprawki
* Stały: Zaufanych aplikacji na macOS "Eksploratora usługi Storage jest teraz".
* Stały: Ubuntu 14.04 jest ponownie obsługiwane.
* Stały: Czasami hello dodać interfejsu użytkownika konta miga podczas ładowania subskrypcji.
* Stały: Czasami nie wszystkie zasoby magazynu zostały wymienione w okienku nawigacji po lewej stronie powitania.
* Stały: hello w okienku akcji czasami wyświetlane akcje puste.
* Stały: hello rozmiar okna z hello ostatniego zamknięcia sesji jest teraz przechowywane.
* Stałe: Można otworzyć wiele kart dla hello tego samego zasobu za pomocą menu kontekstowe hello.

### <a name="known-issues"></a>Znane problemy
* Szybki dostęp działa tylko w przypadku elementów na podstawie subskrypcji. Zasobów lokalnych lub zasobów dołączonych za pomocą klucza lub tokenu sygnatury dostępu Współdzielonego nie są obsługiwane w tej wersji.
* Może potrwać kilka sekund toonavigate toohello zasobu docelowego, w zależności od liczby zasobów, należy mieć szybki dostęp.
* Więcej niż trzech grup obiektów blob lub przekazywania na powitania sam plików czasu może spowodować błędy.
* Dojść wyszukiwania wyszukiwanie w węzłach około 50 000 — po to, wydajność może mieć wpływ na lub może spowodować nieobsługiwanych wyjątków.
* Dla hello pierwsze logowanie przy użyciu Eksploratora usługi Storage hello na macOS, może pojawić się wiele wyświetla monit podanie łańcucha hello tooaccess uprawnień użytkownika. Sugerujemy wybrania **zawsze Zezwalaj** tak hello wiersza nie wyświetlaj ponownie

## <a name="previous-releases"></a>Poprzednie wersje
### <a name="features"></a>Funkcje
#### <a name="main-features"></a>Główne funkcje
* System macOS, Linux oraz wersje systemu Windows
* Zaloguj się tooview pogrupowane według subskrypcji kont magazynu:
    * Użyj konta organizacji, Account firmy Microsoft, 2FA itp.
    * Konfigurowanie i zarządzanie nimi ustawienia serwera proxy
    * Usuwanie kont przy wylogowaniu
* Połącz przy użyciu konta tooStorage:
    * Nazwa konta i klucz
    * Niestandardowe punkty końcowe (w tym chińskiej wersji platformy Azure)
    * Identyfikator URI sygnatury dostępu Współdzielonego dla konta magazynu
* Obsługa usługi Azure Resource Manager i klasycznym magazynu
* Generuj klucze sygnatury dostępu Współdzielonego dla obiektów blob, kontenerów obiektów blob, kolejek, tabel lub udziały plików
* Połącz tooblob kontenerów, kolejek, tabel lub udziały plików z kluczem dostępu sygnatur dostępu Współdzielonego
* Zarządzanie zasadami dostępu przechowywane dla kontenerów obiektów blob, kolejek, tabel lub udziały plików
* Magazyn lokalny rozwój emulatorze magazynu (tylko system Windows)
* Tworzenie i usuwanie kontenerów obiektów blob, kolejek i tabel
* Widok $logs kontenerów obiektów blob i tabelach $metrics
* Wyszukaj określonych obiektów blob, kolejek, tabel lub udziały plików
* Linki bezpośrednie toostorage kont lub kontenery, kolejek, tabel lub plików udziałów do udostępniania i łatwe uzyskiwanie dostępu do zasobów
* Zmień nazwę kontenerów obiektów blob, tabel, udziałów plików
* Możliwość toomanage i skonfigurować zasady CORS
* Łatwo skopiować klucza podstawowego i pomocniczego dla kont magazynu
* Kontrole MD5 przekazywanie i pobieranie integralność danych i spójności
* Wyszukaj kontenerów obiektów blob, tabel, kolejek, udziałów plików lub kont magazynu w polu wyszukiwania hello
* Można teraz numer pin najczęściej używane usług toohello szybki dostęp do ułatwienia nawigacji
* Teraz możesz otworzyć wiele edytorów na różnych kartach. Jednym kliknięciem tooopen kartę tymczasowego; Kliknij dwukrotnie tooopen kartę trwałych. Możesz również kliknąć toomake tymczasowego kartę hello go stałe kartę
* Zauważalne ulepszenia wydajności i stabilności wysyłanie i pobieranie danych, szczególnie w przypadku dużych plików na maszynach fast
* Firma Microsoft ponownym są wprowadzeniem, hello rozszerzone ukierunkowane wyszukiwanie i dodany hello koncepcji zakresu. Wprowadź hello ścieżki tooa węzła za pośrednictwem ikony hover hello, kliknij prawym przyciskiem myszy -> "Wyszukiwania z tutaj", lub ręcznie tooscope tego węzła. Po zakresu, można dodać wyszukaj termin toohello koniec hello ścieżki toodeep wyszukiwania od tego węzła
* Dodano różne kompozycje: jasny (ustawienie domyślne), ciemny, wysoki kontrast czarne i wysoki kontrast biały.
* Przejdź tooEdit -> toochange motywów preferencje motywów
* W systemie Linux, 64-bitowego systemu operacyjnego jest teraz wymagane
* Zaktualizowaliśmy naszych logo!
#### <a name="blobs"></a>Obiekty blob
* Wyświetl obiekty BLOB i przeglądanie katalogów
* Przekazywanie, pobieranie, usuwanie i kopiowania obiektów blob i folderów
* Otwieranie i wyświetlanie hello zawartość tekstu i obrazów obiektów blob
* Wyświetlanie i edytowanie właściwości obiektów blob i metadanych
* Wyszukaj obiekty BLOB według prefiksu
* Tworzenie i przerwać dzierżaw obiekty BLOB i kontenerów obiektów blob
* Przeciągnij n porzucić tooupload plików
* Zmień nazwę obiekty BLOB i folderów
* Teraz można tworzyć foldery "wirtualne" pusta w kontenerów obiektów blob
* Można zmodyfikować właściwości hello obiektów Blob i plików
#### <a name="tables"></a>Tabele
* Wyświetl i zapytanie jednostki z ODATA lub użyj konstruktora zapytań toocreate złożonych zapytań
* Dodawanie, edytowanie i usuwanie jednostek
* Importowanie i eksportowanie spisu treści w formacie CSV (w tym eksportowanie wyników zapytania)
* Dostosowywanie kolejności kolumn
* Możliwość toosave zapytań
#### <a name="queues"></a>Kolejki
* Wyświetlanie podglądu 32 ostatnich wiadomości
* Dodawania, usuwania z kolejki, wyświetlanie komunikatów
* Czyszczenie kolejki
* Firma Microsoft możliwe go możesz toodecide czy tooencode/dekodowania wiadomości w kolejce
#### <a name="file-shares"></a>Udziały plików
* Wyświetlanie plików i przeglądanie katalogów
* Przekazywanie, pobieranie, usuwanie i kopiowanie plików oraz katalogów
* Wyświetl właściwości pliku
* Zmień nazwę plików i katalogów

### <a name="bug-fixes"></a>Poprawki błędów
* Stała: Ekranu zamrożenia problemów
* Stały: Zwiększonych zabezpieczeń

### <a name="known-issues"></a>Znane problemy
* Wyszukiwanie dojść wyszukiwania w węzłach około 50 000 -, wydajność może być wpływ na system macOS instalacji może wymagać podniesionego poziomu uprawnień
* Panel ustawień konta mogą być wyświetlane, należy tooreenter poświadczenia toofilter subskrypcji
* Zmiana nazwy obiektów blob (indywidualnie lub wewnątrz kontenera obiektów blob zmienionej nazwie) nie zostaną zachowane migawki. Wszystkie inne właściwości i metadanych dla obiektów blob, plików i jednostek są zachowywane podczas zmiany nazwy
* Stos Azure aktualnie nie obsługuje pliki, więc w trakcie tooexpand hello **pliki** węzła powoduje wystąpienie błędu
* Linux 14.04 instalacji wymaga wersji gcc zaktualizowane lub uaktualnione. Witaj poniższe kroki przedstawiają sposób tooupgrade:

```
sudo add-apt-repository ppa:ubuntu-toolchain-r/test
sudo apt-get update
sudo apt-get upgrade
sudo apt-get dist-upgrade
```

### <a name="previous-versions"></a>Poprzednie wersje
#### <a name="october-2016-release-version-085"></a>Października 2016 wersji (wersja 0.8.5)
* [Pobierz dla systemu Windows](https://go.microsoft.com/fwlink/?LinkId=809306)
* [Pobierz dla komputerów Mac](https://go.microsoft.com/fwlink/?LinkId=809307)
* [Do pobrania dla systemu Linux](https://go.microsoft.com/fwlink/?LinkId=809308)
