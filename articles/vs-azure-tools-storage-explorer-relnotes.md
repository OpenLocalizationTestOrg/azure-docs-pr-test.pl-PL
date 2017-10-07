---
title: "informacje o wersji aaaMicrosoft Eksploratora usługi Azure Storage (wersja zapoznawcza) | Dokumentacja firmy Microsoft"
description: "Informacje o wersji dla Eksploratora usługi Microsoft Azure Storage (wersja zapoznawcza)"
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
ms.date: 07/31/2017
ms.author: cawa
ms.openlocfilehash: 44ff6dc8e2015f4eb71fa13098b832fbbf48ccac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-azure-storage-explorer-preview-release-notes"></a>Informacje o wersji Eksploratora usługi Microsoft Azure Storage (wersja zapoznawcza)

Ten artykuł zawiera Zwolnij hello uwagi 0.8.16 Eksploratora usługi Azure Storage (wersja zapoznawcza) wersji, a także informacje o wersji w poprzednich wersjach.

[Eksploratora usługi Microsoft Azure Storage (wersja zapoznawcza)](./vs-azure-tools-storage-manage-with-storage-explorer.md) jest aplikacją autonomiczną, która umożliwia tooeasily pracy z danymi usługi Azure Storage w systemie Windows, macOS i Linux.

## <a name="version-0816-preview"></a>Wersja 0.8.16 (wersja zapoznawcza)
8/21/2017

### <a name="download-azure-storage-explorer-0816-preview"></a>Pobierz Eksploratora usługi Azure Storage 0.8.16 (wersja zapoznawcza)
- [Eksplorator usługi Azure Storage 0.8.16 (wersja zapoznawcza) dla systemu Windows](https://go.microsoft.com/fwlink/?LinkId=708343)
- [Eksplorator usługi Azure Storage 0.8.16 (wersja zapoznawcza) dla komputerów Mac](https://go.microsoft.com/fwlink/?LinkId=708342)
- [Eksplorator usługi Azure Storage 0.8.16 (wersja zapoznawcza) dla systemu Linux](https://go.microsoft.com/fwlink/?LinkId=722418)

### <a name="new"></a>Nowy
* Po otwarciu obiektu blob Eksploratora usługi Storage spowoduje wyświetlenie monitu tooupload hello pobrany plik po wykryciu zmiany
* Rozszerzony stos Azure logowania
* Hello lepszą wydajność przekazywania/pobieranie wiele małych plików na powitania sam czas


### <a name="fixes"></a>Poprawki
* Dla niektórych typów obiektów blob wybierając zbyt "replace" podczas przekazywania konflikt czasami spowoduje przekazywania hello uruchamiany ponownie. 
* W wersji 0.8.15 przekazywania czasami spowoduje zatrzymania 99%.
* Podczas przekazywania plików tooa udziału plików, jeśli została wybrana opcja directory tooa tooupload, która jeszcze nie istnieje, przekazania nie powiedzie się.
* Eksploratora usługi Storage został niepoprawnie generowania sygnatury czasowe dla sygnatur dostępu współdzielonego i tabeli zapytania.


Znane problemy
* Przy użyciu nazwy i parametry połączenia klucza aktualnie nie działa. Zostanie on rozwiązany w następnej wersji hello. Do tego czasu można dołączyć z nazwy i klucza.
* Jeśli spróbujesz tooopen pliku o nieprawidłowej nazwie pliku systemu Windows hello pobierania spowoduje błąd: nie odnaleziono pliku.
* Po dla zadania, klikając przycisk "Anuluj", może upłynąć trochę czasu zanim toocancel tego zadania. Jest to ograniczenie hello biblioteki węzła magazynu Azure.
* Po zakończeniu przekazywania obiektów blob, karta hello, który zainicjował przekazywania hello jest odświeżany. Zmiana z poprzednich zachowanie, a także spowoduje toobe wycofać głównego toohello kontenera hello, które znajdują się w.
* Jeśli wybierzesz hello niewłaściwy kod PIN/certyfikatu karty inteligentnej, a następnie konieczne będzie toorestart w kolejności toohave Eksploratora usługi Storage zapomnij tej decyzji.
* panel ustawień konta Hello mogą być wyświetlane, należy tooreenter poświadczenia toofilter subskrypcji.
* Zmiana nazwy obiektów blob (indywidualnie lub wewnątrz kontenera obiektów blob zmienionej nazwie) nie zostaną zachowane migawki. Wszystkie inne właściwości i metadanych dla obiektów blob, plików i jednostek są zachowywane podczas zmiany nazwy.
* Mimo że stosu Azure aktualnie nie obsługuje udziałów plików, węzła udziałów plików jest nadal wyświetlana na koncie dołączone magazynu Azure stosu.
* Dla użytkowników na Ubuntu 14.04, konieczne będzie tooensure GCC działa toodate — można to zrobić, uruchamiając hello następujące polecenia, a następnie ponownym uruchomieniu komputera:

    ```
    sudo add-apt-repository ppa:ubuntu-toolchain-r/test
    sudo apt-get update
    sudo apt-get upgrade
    sudo apt-get dist-upgrade
    ```

* Dla użytkowników Ubuntu 17.04 konieczne będzie tooinstall GConf — można to zrobić systemem hello następujące polecenia, a następnie ponownym uruchomieniu komputera:

    ```
    sudo apt-get install libgconf-2-4
    ```

## <a name="version-0814-preview"></a>Wersja 0.8.14 (wersja zapoznawcza)
06/22/2017

### <a name="download-azure-storage-explorer-0814-preview"></a>Pobierz Eksploratora usługi Azure Storage 0.8.14 (wersja zapoznawcza)
* [Pobierz Eksploratora usługi Azure Storage 0.8.14 (wersja zapoznawcza) dla systemu Windows](https://go.microsoft.com/fwlink/?LinkId=809306)
* [Pobierz Eksploratora usługi Azure Storage 0.8.14 (wersja zapoznawcza) dla komputerów Mac](https://go.microsoft.com/fwlink/?LinkId=809307)
* [Pobierz Eksploratora usługi Azure Storage 0.8.14 (wersja zapoznawcza) dla systemu Linux](https://go.microsoft.com/fwlink/?LinkId=809308)

### <a name="new"></a>Nowy

* Zaktualizowano too1.7.2 wersji elektronów w kolejności tootake zaletą kilka aktualizacji krytycznych
* Teraz szybko dostępne hello online przewodnik rozwiązywania problemów z menu Pomoc hello
* Rozwiązywanie problemów z Eksploratora usługi Storage [przewodnik][2]
* [Instrukcje] [ 3] łączyć się z subskrypcji Azure stosu tooan

### <a name="known-issues"></a>Znane problemy

* Przyciski na powitania usuwania folderu — okno dialogowe potwierdzenia nie zarejestrować kliknięć myszą hello w systemie Linux. Obejście jest klawisz Enter hello toouse
* Jeśli wybierzesz hello niewłaściwy kod PIN/certyfikatu karty inteligentnej, a następnie konieczne będzie toorestart w kolejności toohave Eksploratora usługi Storage zapomnij hello decyzji
* Mając więcej niż 3 grup obiektów blob lub przekazywania na powitania sam plików czasu może powodować błędy
* panel ustawień konta Hello mogą być wyświetlane, należy tooreenter poświadczenia w kolejności toofilter subskrypcji
* Zmiana nazwy obiektów blob (indywidualnie lub wewnątrz kontenera obiektów blob zmienionej nazwie) nie zostaną zachowane migawki. Wszystkie inne właściwości i metadanych dla obiektów blob, plików i jednostek są zachowywane podczas zmiany nazwy.
* Mimo że stosu Azure aktualnie nie obsługuje udziałów plików, węzła udziałów plików jest nadal wyświetlana na koncie dołączone magazynu Azure stosu. 
* Ubuntu 14.04 instalacji potrzeb wersji gcc zaktualizowane lub uaktualnione — tooupgrade kroki są poniżej:

    ```
    sudo add-apt-repository ppa:ubuntu-toolchain-r/test
    sudo apt-get update
    sudo apt-get upgrade
    sudo apt-get dist-upgrade
    ```




## <a name="previous-releases"></a>Poprzednie wersje

* [Wersja 0.8.13](#version-0813)
* [Wersja 0.8.12 / 0.8.11 / 0.8.10](#version-0812--0811--0810)
* [Wersja 0.8.9 / 0.8.8](#version-089--088)
* [Wersja 0.8.7](#version-087)
* [Wersja 0.8.6](#version-086)
* [Wersja 0.8.5](#version-085)
* [Wersja 0.8.4](#version-084)
* [Wersja 0.8.3](#version-083)
* [Wersja 0.8.2](#version-082)
* [Wersja 0.8.0](#version-080)
* [Wersja 0.7.20160509.0](#version-07201605090)
* [Wersja 0.7.20160325.0](#version-07201603250)
* [Wersja 0.7.20160129.1](#version-07201601291)
* [Wersja 0.7.20160105.0](#version-07201601050)
* [Wersja 0.7.20151116.0](#version-07201511160)


### <a name="version-0813"></a>Wersja 0.8.13
05/12/2017

#### <a name="new"></a>Nowy

* Rozwiązywanie problemów z Eksploratora usługi Storage [przewodnik][2]
* [Instrukcje] [ 3] łączyć się z subskrypcji Azure stosu tooan

#### <a name="fixes"></a>Poprawki

* Stała: Przekazywanie pliku wypróbowana wysokiej spowodować błąd braku pamięci
* Stały: Można teraz zalogować się przy użyciu kodu PIN/za pomocą kart inteligentnych
* Stałe: Otwórz w portalu teraz współpracuje z Chińskiej wersji platformy Azure, platformy Azure w Niemczech Azure instytucji rządowych Stanów Zjednoczonych i stosu Azure
* Stała: Podczas przekazywania kontenera obiektów blob tooa folderu, błąd "Niedozwolonej operacji" czasami wystąpiłyby
* Stałej: Zaznacz wszystko zostało wyłączone podczas zarządzania migawki
* Stały: hello metadane obiektu blob podstawowej hello może spowodować zastąpienie po wyświetleniu właściwości hello jego migawek.

#### <a name="known-issues"></a>Znane problemy

* Jeśli wybierzesz hello niewłaściwy kod PIN/certyfikatu karty inteligentnej, a następnie konieczne będzie toorestart w kolejności toohave Eksploratora usługi Storage zapomnij hello decyzji
* Gdy jest powiększony przychodzący lub wychodzący, poziom powiększenia hello na chwilę może zresetować toohello domyślny poziom
* Mając więcej niż 3 grup obiektów blob lub przekazywania na powitania sam plików czasu może powodować błędy
* panel ustawień konta Hello mogą być wyświetlane, należy tooreenter poświadczenia w kolejności toofilter subskrypcji
* Zmiana nazwy obiektów blob (indywidualnie lub wewnątrz kontenera obiektów blob zmienionej nazwie) nie zostaną zachowane migawki. Wszystkie inne właściwości i metadanych dla obiektów blob, plików i jednostek są zachowywane podczas zmiany nazwy.
* Mimo że stosu Azure aktualnie nie obsługuje udziałów plików, węzła udziałów plików jest nadal wyświetlana na koncie dołączone magazynu Azure stosu. 
* Ubuntu 14.04 instalacji potrzeb wersji gcc zaktualizowane lub uaktualnione — tooupgrade kroki są poniżej:

    ```
    sudo add-apt-repository ppa:ubuntu-toolchain-r/test
    sudo apt-get update
    sudo apt-get upgrade
    sudo apt-get dist-upgrade
    ```


### <a name="version-0812--0811--0810"></a>Wersja 0.8.12 / 0.8.11 / 0.8.10
04/07/2017

#### <a name="new"></a>Nowy

* Eksplorator usługi Storage teraz zostanie automatycznie zamknięte podczas instalacji aktualizacji z hello powiadomienie o aktualizacji
* Szybki dostęp w miejscu udostępnia udoskonalone środowisko do pracy z często używanych zasobów
* W edytorze kontenera obiektów Blob hello możesz teraz przeglądać maszyny wirtualnej, które dzierżawionych obiektu blob należy do
* Teraz można zwinąć powitania po lewej stronie panelu
* Odnajdywanie teraz działa na powitania sam czas pobrania
* Statystyk użycia w hello kontenera obiektów Blob, udziału plików, a tabela edytory toosee hello rozmiar zasobu lub zaznaczenia
* Możesz teraz tooAzure logowania w usłudze Active Directory (AAD) na podstawie konta Azure stosu. 
* Można teraz archiwum przekazywania plików ponad 32 MB tooPremium magazynu kont
* Udoskonalona obsługa ułatwień dostępu
* Można teraz dodawać zaufanych Base-64 zakodowane certyfikatów X.509 SSL przez przejście tooEdit -&gt; certyfikaty SSL -&gt; importu certyfikatów

#### <a name="fixes"></a>Poprawki

* Stały: po odświeżeniu poświadczenia konta, widok drzewa hello czy czasami nie automatycznie odświeżenia
* Stała: Generowanie sygnatury dostępu Współdzielonego dla kolejki emulatora i tabele dadzą w wyniku nieprawidłowy adres URL
* Stały: konta premium magazynu teraz można rozszerzyć, gdy włączone jest serwer proxy
* Stała: hello przycisk Zastosuj na powitania konta, które strony zarządzania nie będzie działać, jeśli masz 1 lub 0 konta zaznaczone
* Stały: przekazywanie obiektów blob, które wymagają rozwiązania konfliktu może zakończyć się niepowodzeniem — stała 0.8.11 
* Stałe: wysyłanie opinii został przerwany w 0.8.11 — stała 0.8.12 

#### <a name="known-issues"></a>Znane problemy

* Po uaktualnieniu too0.8.10, konieczne będzie toorefresh wszystkie swoje poświadczenia.
* Gdy jest powiększony przychodzący lub wychodzący, poziom powiększenia hello na chwilę może zresetować toohello domyślny poziom.
* Więcej niż 3 grup obiektów blob lub przekazywania na powitania sam plików czasu może spowodować błędy.
* panel ustawień konta Hello mogą być wyświetlane, należy tooreenter poświadczenia w kolejności toofilter subskrypcji.
* Zmiana nazwy obiektów blob (indywidualnie lub wewnątrz kontenera obiektów blob zmienionej nazwie) nie zostaną zachowane migawki. Wszystkie inne właściwości i metadanych dla obiektów blob, plików i jednostek są zachowywane podczas zmiany nazwy.
* Mimo że stosu Azure aktualnie nie obsługuje udziałów plików, węzła udziałów plików jest nadal wyświetlana na koncie dołączone magazynu Azure stosu. 
* Ubuntu 14.04 instalacji potrzeb wersji gcc zaktualizowane lub uaktualnione — tooupgrade kroki są poniżej:

    ```
    sudo add-apt-repository ppa:ubuntu-toolchain-r/test
    sudo apt-get update
    sudo apt-get upgrade
    sudo apt-get dist-upgrade
    ```


### <a name="version-089--088"></a>Wersja 0.8.9 / 0.8.8
02/23/2017

<iframe width="560" height="315" src="https://www.youtube.com/embed/R6gonK3cYAc?ecver=1" frameborder="0" allowfullscreen></iframe>

<iframe width="560" height="315" src="https://www.youtube.com/embed/SrRPCm94mfE?ecver=1" frameborder="0" allowfullscreen></iframe>


#### <a name="new"></a>Nowy

* Eksplorator usługi Storage 0.8.9 będzie automatycznie pobierał hello najnowszej wersji aktualizacji.
* Poprawka: przy użyciu portalu sieci generowane tooattach identyfikatora URI połączenia SAS, konto magazynu może spowodować błąd.
* Teraz można tworzyć, zarządzanie i wspierania migawki obiektu blob.
* Można teraz zalogować konta tooAzure Chin, platformy Azure w Niemczech i Azure instytucji rządowych Stanów Zjednoczonych.
* Można teraz zmienić poziom powiększenia hello. Użyj opcji hello w tooZoom menu Widok hello Pomniejsz i zresetować powiększenie.
* Znaki Unicode są teraz obsługiwane w metadanych użytkownika do obiektów blob i plików.
* Zwiększona dostępność.
* informacje o wersji Hello następnej wersji mogą być wyświetlane z hello powiadomienie o aktualizacji. Można również wyświetlić hello bieżącej wersji hello menu Pomoc.

#### <a name="fixes"></a>Poprawki

* Stały: numer wersji hello jest teraz prawidłowo wyświetlany w Panelu sterowania w systemie Windows
* Stałe: wyszukiwania nie jest już ograniczona too50, 000 węzłów
* Stały: udział plików tooa przekazywania wykonana nieskończona Jeśli hello katalog docelowy już nie istnieje
* Stały: lepszą stabilność dla długich przekazywania i pobierania

#### <a name="known-issues"></a>Znane problemy

* Gdy jest powiększony przychodzący lub wychodzący, poziom powiększenia hello na chwilę może zresetować toohello domyślny poziom.
* Szybki dostęp działa tylko z elementami subskrypcji. Zasobów lokalnych lub zasobów dołączonych za pomocą klucza lub tokenu sygnatury dostępu Współdzielonego nie są obsługiwane w tej wersji.
* Może potrwać kilka sekund toonavigate toohello zasobu docelowego, w zależności od liczby zasobów, należy mieć szybki dostęp.
* Więcej niż 3 grup obiektów blob lub przekazywania na powitania sam plików czasu może spowodować błędy.

12/16/2016
### <a name="version-087"></a>Wersja 0.8.7

<iframe width="560" height="315" src="https://www.youtube.com/embed/Me4Y4jxoer8?ecver=1" frameborder="0" allowfullscreen></iframe>

#### <a name="new"></a>Nowy

* Można wybrać sposób tooresolve konfliktów na początku hello aktualizacji, Pobierz lub skopiuj sesji w oknie działania hello
* Umieść kursor nad kartę toosee hello pełną ścieżkę hello zasobu magazynu
* Po kliknięciu na karcie synchronizacji z lokalizacji, w okienku nawigacji po lewej stronie powitania

#### <a name="fixes"></a>Poprawki

* Stały: Eksploratora usługi Storage jest teraz zaufanych aplikacji dla komputerów Mac
* Stały: Ubuntu 14.04 jest ponownie obsługiwane
* Stały: Czasami hello Dodaj konto, które miga interfejsu użytkownika podczas ładowania subskrypcji
* Stały: Czasami nie wszystkie zasoby magazynu zostały wymienione w okienku nawigacji po lewej stronie powitania
* Stały: hello w okienku akcji czasami wyświetlane akcje pusty
* Stały: rozmiar okna hello z hello ostatniego zamknięcia sesji są teraz przechowywane
* Stałe: Można otworzyć wiele kart dla hello tego samego zasobu za pomocą menu kontekstowe hello

#### <a name="known-issues"></a>Znane problemy

* Szybki dostęp działa tylko z elementami subskrypcji. Zasobów lokalnych lub dołączonych za pomocą klucza lub tokenu sygnatury dostępu Współdzielonego zasobów nie są obsługiwane w tej wersji
* Szybki dostęp może potrwać kilka sekund toonavigate toohello zasobu docelowego, w zależności od liczby zasobów, masz
* Mając więcej niż 3 grup obiektów blob lub przekazywania na powitania sam plików czasu może powodować błędy
* Dojść wyszukiwania wyszukiwanie w węzłach około 50 000 — po to, może to mieć wpływ na wydajność lub może spowodować nieobsługiwany wyjątek
* Dla hello pierwsze logowanie przy użyciu Eksploratora usługi Storage hello na macOS, może pojawić się wiele wyświetla monit podanie łańcucha kluczy tooaccess uprawnień użytkownika. Zalecamy użycie wybierz zawsze Zezwalaj tak hello wiersza nie będą widoczne ponownie

11/18/2016
### <a name="version-086"></a>Wersja 0.8.6

#### <a name="new"></a>Nowy

* Można teraz numer pin najczęściej używane usług toohello szybki dostęp do ułatwienia nawigacji
* Teraz możesz otworzyć wiele edytorów na różnych kartach. Jednym kliknięciem tooopen kartę tymczasowego; Kliknij dwukrotnie pozycję tooopen kartę trwałych. Możesz również kliknąć na toomake tymczasowego kartę hello go stałe kartę
* Wprowadziliśmy zauważalna zmiana wydajności i stabilności ulepszenia przekazywania i pobierania, zwłaszcza w przypadku dużych plików na maszynach fast
* Teraz można tworzyć foldery "wirtualne" pusta w kontenerów obiektów blob
* Ma ponownie wprowadzono ukierunkowane wyszukiwanie z naszego nowego wyszukiwania podciągu rozszerzonego, teraz są dwie opcje wyszukiwania: 
    * Globalne wyszukiwanie - w hello tekstowym wyszukiwania wpisz wyszukiwany termin
    * Wyszukiwania zakresowego - kliknij hello Lupa ikona następnego tooa węzła, a następnie dodaj końcu toohello terminu wyszukiwania ścieżki hello, lub kliknij prawym przyciskiem myszy i wybierz pozycję "Wyszukiwania z tutaj"
* Dodano różne kompozycje: jasny (ustawienie domyślne), ciemny, wysoki kontrast czarne i wysoki kontrast biały. Przejdź tooEdit -&gt; toochange motywów preferencje motywów
* Można zmodyfikować właściwości obiektów Blob i plików
* Firma Microsoft obsługuje teraz zakodowanego (base64) i niekodowany kolejki komunikatów
* W systemie Linux, 64-bitowego systemu operacyjnego jest teraz wymagane. W tej wersji obsługiwany jest tylko 64-bitowych Ubuntu 16.04.1 LTS
* Zaktualizowaliśmy naszych logo!

#### <a name="fixes"></a>Poprawki

* Stała: Ekranu zamrożenia problemów
* Stały: Zwiększonych zabezpieczeń
* Stałe: Może być czasami zduplikowane dołączonego konta
* Stały: Obiektów blob z niezdefiniowanego typu zawartości można wygenerować wyjątek
* Stały: Hello otwierania panelu zapytania na pusta tabela nie było możliwe
* Stały: Zmienia się usterki podczas wyszukiwania.
* Stały: Zwiększenie hello liczby zasobów, załadowane z 50 too100 po kliknięciu przycisku "Obciążenia więcej"
* Stałe: Przy pierwszym uruchomieniu, jeśli konto jest podpisana, możemy teraz wybrać wszystkie subskrypcje dla tego konta domyślnie 

#### <a name="known-issues"></a>Znane problemy

* Ta wersja hello Eksploratora magazynu nie działa w Ubuntu 14.04
* tooopen wielu kartach powitania kliknij tego samego zasobu nie stale czy hello tego samego zasobu. Kliknij na inny zasób i następnie wrócić do poprzedniej strony i kliknij przycisk na powitania oryginalnego tooopen zasobów go ponownie w innej karty 
* Szybki dostęp działa tylko z elementami subskrypcji. Zasobów lokalnych lub dołączonych za pomocą klucza lub tokenu sygnatury dostępu Współdzielonego zasobów nie są obsługiwane w tej wersji
* Szybki dostęp może potrwać kilka sekund toonavigate toohello zasobu docelowego, w zależności od liczby zasobów, masz
* Mając więcej niż 3 grup obiektów blob lub przekazywania na powitania sam plików czasu może powodować błędy
* Dojść wyszukiwania wyszukiwanie w węzłach około 50 000 — po to, może to mieć wpływ na wydajność lub może spowodować nieobsługiwany wyjątek

10/03/2016
### <a name="version-085"></a>Wersja 0.8.5

#### <a name="new"></a>Nowy

* Można teraz Użyj generowanych przez Portal SAS kluczy tooattach tooStorage kont i zasobów

#### <a name="fixes"></a>Poprawki

* Stała: wyścigu podczas wyszukiwania czasami spowodował toobecome węzłów z systemem innym niż rozwijania
* Stałych: "Użyj protokołu HTTP" nie działa, gdy połączenie tooStorage kont z nazwą konta i klucz
* Stały: Klucze SAS (wygenerowany specjalnie portalu te) zwracają błąd "ukośnikiem na końcu"
* Stały: Importowanie tabeli problemów
    * Czasami klucz partycji i klucz wiersza zostały cofnięte
    * Nie można tooread "null" kluczy partycji

#### <a name="known-issues"></a>Znane problemy

* Dojść wyszukiwania wyszukiwanie w węzłach około 50 000 -, wydajność może mieć wpływ na
* Stos Azure aktualnie nie obsługuje plików, więc tooexpand plików w trakcie wyświetli błąd

09/12/2016
### <a name="version-084"></a>Wersja 0.8.4

<iframe width="560" height="315" src="https://www.youtube.com/embed/cr5tOGyGrIQ?ecver=1" frameborder="0" allowfullscreen></iframe>

#### <a name="new"></a>Nowy

* Generowanie linki bezpośrednie toostorage kont, kontenerów, kolejek, tabel, lub udziały plików do udostępniania i łatwo uzyskiwać dostęp do zasobów tooyour - systemu Windows i obsługi systemu Mac OS
* Wyszukaj kontenerów obiektów blob, tabel, kolejek, udziałów plików lub kont magazynu w polu wyszukiwania hello
* Teraz można pogrupować klauzul konstruktora zapytań hello tabeli
* Zmień nazwę i kopiowania/wklejania kontenerów obiektów blob, udziałów plików, tabel, obiektów blob, obiektów blob folderów, plików i katalogów z wewnątrz dołączone sygnatury dostępu Współdzielonego konta i kontenerów
* Zmiana nazwy i kopiowania obiektu blob kontenery i udziały plików teraz zachować właściwości i metadane

#### <a name="fixes"></a>Poprawki

* Stały: nie można edytować jednostek tabeli, gdy właściwości boolean lub binarne

#### <a name="known-issues"></a>Znane problemy

* Dojść wyszukiwania wyszukiwanie w węzłach około 50 000 -, wydajność może mieć wpływ na

08/03/2016
### <a name="version-083"></a>Wersja 0.8.3

<iframe width="560" height="315" src="https://www.youtube.com/embed/HeGW-jkSd9Y?ecver=1" frameborder="0" allowfullscreen></iframe>

#### <a name="new"></a>Nowy

* Zmień nazwę kontenerów, tabel, udziałów plików
* Udoskonalone środowisko konstruktora zapytań
* Możliwości toosave i ładowanie zapytań
* Bezpośrednie łącza toostorage kont lub kontenery, kolejek, tabel lub udziały do udostępniania i łatwe uzyskiwanie dostępu do zasobów plików (tylko Windows - macOS obsługuje wkrótce!)
* Możliwość toomanage i skonfigurować zasady CORS

#### <a name="fixes"></a>Poprawki

* Stały: Accounts Microsoft wymagają ponowne uwierzytelnianie co 8 – 12 godzin

#### <a name="known-issues"></a>Znane problemy

* Czasami hello interfejsu użytkownika mogą sprawiać wrażenie — maksymalizacja okna hello pomaga rozwiązać ten problem
* System macOS instalacji może wymagać podniesionego poziomu uprawnień
* Panel ustawień konta mogą być wyświetlane, należy tooreenter poświadczenia w kolejności toofilter subskrypcji
* Zmiana nazwy udziałów plików, kontenerów obiektów blob i tabele nie zachowuje metadane lub innych właściwości w kontenerze hello, takie jak przydziału udziału plików, poziom dostępu publicznego lub zasady dostępu
* Zmiana nazwy obiektów blob (indywidualnie lub wewnątrz kontenera obiektów blob zmienionej nazwie) nie zostaną zachowane migawki. Wszystkie inne właściwości i metadanych dla obiektów blob, plików i jednostek są zachowywane podczas zmiany nazwy
* Kopiowanie lub zmiana nazwy zasobów nie działa w ramach konta dołączone sygnatury dostępu Współdzielonego

07/07/2016
### <a name="version-082"></a>Wersja 0.8.2

<iframe width="560" height="315" src="https://www.youtube.com/embed/nYgKbRUNYZA?ecver=1" frameborder="0" allowfullscreen></iframe>

#### <a name="new"></a>Nowy

* Konta magazynu są pogrupowane według subskrypcji; Programowanie magazynu i zasobów dołączonych za pomocą klucza lub SAS są wyświetlane w węźle (lokalny i załączone)
* Wyloguj z konta w panelu "Ustawienia konta Azure"
* Konfigurowanie tooenable ustawienia serwera proxy i zarządzanie nimi logowania
* Tworzenie i przerwać dzierżawy obiektów blob
* Kontenery Otwórz obiektów blob, kolejek, tabel i pliki z jednym kliknięciem

#### <a name="fixes"></a>Poprawki

* Stała: dodaje z bibliotekami .NET lub Java wiadomości w kolejce są nie prawidłowo zdekodować z formatu base64
* Stały: $metrics tabele nie są wyświetlane w przypadku kont magazynu obiektów Blob
* Stały: węzeł tabele nie działa dla lokalnej pamięci masowej (Programowanie)

#### <a name="known-issues"></a>Znane problemy

* System macOS instalacji może wymagać podniesionego poziomu uprawnień

06/15/2016
### <a name="version-080"></a>Wersja 0.8.0

<iframe width="560" height="315" src="https://www.youtube.com/embed/ycfQhKztSIY?ecver=1" frameborder="0" allowfullscreen></iframe>

<iframe width="560" height="315" src="https://www.youtube.com/embed/k4_kOUCZ0WA?ecver=1" frameborder="0" allowfullscreen></iframe>

<iframe width="560" height="315" src="https://www.youtube.com/embed/3zEXJcGdl_k?ecver=1" frameborder="0" allowfullscreen></iframe>

#### <a name="new"></a>Nowy

* Obsługa udziału plików: wyświetlanie, przekazywanie, pobieranie, kopiowania plików i katalogów, identyfikatory URI SAS (Tworzenie i łączenie)
* Udoskonalona obsługa łączenie tooStorage identyfikatorów URI SAS lub klucze konta
* Eksportowanie tabeli wyników zapytania
* Zmienianie kolejności kolumn w tabeli i dostosowywania
* Wyświetlanie $logs kontenerów obiektów blob i tabelach $metrics dla konta magazynu o metryki włączone
* Ulepszone eksportowania i importowania zachowanie, zawiera teraz typ wartości właściwości

#### <a name="fixes"></a>Poprawki

* Stały: przekazanie lub pobranie dużych obiektów blob może spowodować niekompletne przekazywania/pobieranie
* Stały: Edycja, dodanie lub zaimportowanie jednostki z wartością liczbową ciągu ("1") spowoduje to przekonwertowanie go toodouble
* Stały: Tooexpand hello tabeli w węźle hello lokalne Środowisko deweloperskie

#### <a name="known-issues"></a>Znane problemy

* $metrics tabele nie są widoczne dla kont magazynu obiektów Blob
* Wiadomości w kolejce dodać programistycznie mogą nie być wyświetlane prawidłowo, jeśli wiadomości powitania są zakodowane przy użyciu kodowania Base64

05/17/2016
### <a name="version-07201605090"></a>Wersja 0.7.20160509.0

#### <a name="new"></a>Nowy

* Awarie lepszą obsługę błędów dla aplikacji

#### <a name="fixes"></a>Poprawki

* Usunięte usterki gdzie komunikaty paska informacyjnego czasami nie są wyświetlane podczas logowania były wymagane

#### <a name="known-issues"></a>Znane problemy

* Tabele: Dodawanie, edytowanie, lub importowanie jednostki, która ma właściwość z wartością ambiguously liczbowego, takie jak "1" lub "1.0" i hello toosend prób użytkownika jako `Edm.String`, wartość hello będzie Wróć za pośrednictwem powitania klienta interfejsu API jako Edm.Double

03/31/2016

### <a name="version-07201603250"></a>Wersja 0.7.20160325.0

<iframe width="560" height="315" src="https://www.youtube.com/embed/imbgBRHX65A?ecver=1" frameborder="0" allowfullscreen></iframe>

<iframe width="560" height="315" src="https://www.youtube.com/embed/ceX-P8XZ-s8?ecver=1" frameborder="0" allowfullscreen></iframe>


#### <a name="new"></a>Nowy

* Tabela wsparcia: przeglądanie, wyszukiwanie, eksportu, importowania i operacji CRUD dla jednostek
* Kolejka pomocy technicznej: przeglądanie, dodawanie dequeueing wiadomości
* Generowanie identyfikatorów URI sygnatury dostępu Współdzielonego dla konta magazynu
* Łączenie kont tooStorage identyfikatory URI sygnatury dostępu Współdzielonego
* Powiadomienia o aktualizacji dla przyszłych aktualizacji tooStorage Explorer
* Zaktualizowano wygląd i działanie

#### <a name="fixes"></a>Poprawki

* Ulepszenia wydajności i niezawodności

### <a name="known-issues-amp-mitigations"></a>Znane problemy &amp; środki zaradcze

* Pobieranie plików dużych obiektów blob nie działa prawidłowo — zaleca się używanie AzCopy, podczas gdy ten problem można rozwiązać 
* Poświadczenia konta nie zostaną pobrane ani hello folder macierzysty nie można odnaleźć lub nie można zapisać w pamięci podręcznej
* Jeśli firma Microsoft Dodawanie, edytowanie lub importowanie jednostki, która ma właściwość z wartością ambiguously liczbowego, takie jak "1" lub "1.0" i hello użytkownik spróbuje toosend go jako `Edm.String`, wartość hello będzie Wróć za pośrednictwem powitania klienta interfejsu API jako Edm.Double
* Podczas importowania plików CSV z rekordami wielowierszowe, dane hello może pobrać kostki lub zaszyfrowane

02/03/2016

### <a name="version-07201601291"></a>Wersja 0.7.20160129.1

#### <a name="fixes"></a>Poprawki

* Poprawia ogólną wydajność podczas przekazywanie, pobieranie i kopiowania obiektów blob

01/14/2016

### <a name="version-07201601050"></a>Wersja 0.7.20160105.0

#### <a name="new"></a>Nowy

* Obsługa systemu Linux (parzystość funkcji tooOSX)
* Dodaj kontenerów obiektów blob z kluczem dostępu sygnatur dostępu Współdzielonego
* Dodawanie konta magazynu dla Chin Azure
* Dodawanie konta magazynu z niestandardowe punkty końcowe
* Otwieranie i wyświetlanie hello zawartość tekstu i obrazów obiektów blob
* Wyświetlanie i edytowanie właściwości obiektów blob i metadanych

#### <a name="fixes"></a>Poprawki

* Stała: przekazywanie i pobieranie dużą liczbę obiektów blob (500 +) może wywoływać toohave aplikacji hello biały ekran 
* Stałym: podczas ustawiania poziomu dostępu publicznego kontenera obiektów blob, hello nową wartość nie jest aktualizowana dopiero po ustawieniu ponownie hello skupić się na powitania kontenera. Ponadto okno hello zawsze domyślnie konfiguruje zbyt "dostępu do żadnego elementu publicznego public" i nie hello rzeczywiste bieżącą wartość.
* Obsługa lepszej ogólnej klawiatury/ułatwień dostępu i interfejsu użytkownika
* Obszar nawigacji historii zawijany, gdy jest długa z białą przestrzenią
* Okno dialogowe SAS obsługuje sprawdzania poprawności danych wejściowych
* Magazyn lokalny nadal toobe dostępne, nawet jeśli wygasły poświadczenia użytkownika
* Usunięcie kontenera obiektów blob otwarty Eksplorator obiektów blob hello hello prawej strony jest zamknięty.

#### <a name="known-issues"></a>Znane problemy

* Wymagania instalacji Linux wersji gcc zaktualizowane lub uaktualnione — tooupgrade kroki są poniżej: 
    * `sudo add-apt-repository ppa:ubuntu-toolchain-r/test`
    * `sudo apt-get update`
    * `sudo apt-get upgrade`
    * `sudo apt-get dist-upgrade`

11/18/2015
### <a name="version-07201511160"></a>Wersja 0.7.20151116.0

#### <a name="new"></a>Nowy

* System macOS i wersji systemu Windows
* Zaloguj się tooview kont magazynu — użyć konta organizacji, Account firmy Microsoft, 2FA itp.
* Lokalne działania projektowe magazynu (użyć emulatora magazynu systemu Windows)
* Usługa Azure Resource Manager i Model Klasyczny zasobów pomocy technicznej
* Tworzenie i usuwanie obiektów blob, kolejek i tabel
* Wyszukiwanie określonych obiektów blob, kolejek i tabel
* Przejrzyj zawartość hello kontenerów obiektów blob
* Wyświetlanie i przeglądanie katalogów
* Przekazywanie, pobieranie i usuwanie obiektów blob i folderów
* Wyświetlanie i edytowanie właściwości obiektów blob i metadanych
* Generuj klucze SAS
* Zarządzanie i utworzyć przechowywane zasad dostępu (SAP)
* Wyszukaj obiekty BLOB według prefiksu
* Przeciągnij n Porzuć tooupload plików lub pobrać

#### <a name="known-issues"></a>Znane problemy

* Podczas ustawiania poziomu dostępu publicznego kontenera obiektów blob, dopóki nie zostanie ponownie ustawiony fokus hello w kontenerze hello hello nowa wartość nie jest aktualizowany
* Po otwarciu hello okna dialogowego tooset hello dostępu publicznego poziom zawsze widoczny "Brak dostępu publicznego" hello domyślnej i nie hello bieżąca wartość rzeczywista
* Nie można zmienić nazwy pobrany obiektów blob
* Wpisy dziennika aktywności będą czasami "zatrzymywane" w toku stanu, gdy wystąpi błąd i nie zostanie wyświetlony błąd hello
* Czasami awarii lub włącza całkowicie biały podczas próby tooupload lub pobrać dużą liczbę obiektów blob
* Czasami anulowanie operacji kopiowania nie działa
* Podczas tworzenia kontenera (tabeli-obiekt blob/kolejki), jeśli wejściowy nieprawidłową nazwę i kontynuować toocreate drugiego, w ramach typu innego kontenera nie można ustawić fokusu na nowy typ hello
* Nie można utworzyć nowego folderu, lub zmień nazwę folderu




[2]: https://support.microsoft.com/en-us/help/4021389/storage-explorer-troubleshooting-guide
[3]: vs-azure-tools-storage-manage-with-storage-explorer.md