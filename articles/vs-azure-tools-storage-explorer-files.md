---
title: "aaaUsing Eksploratora usługi Storage (wersja zapoznawcza) z usługą Magazyn plików Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak Dowiedz się, jak toouse toowork Eksploratora usługi Storage (wersja zapoznawcza) z plików, udziały i pliki."
services: storage
documentationcenter: na
author: cawaMS
manager: paulyuk
editor: 
ms.assetid: 
ms.service: storage
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/09/2017
ms.author: cawa
ms.openlocfilehash: 98eb3cde711ae3dbfdb6ffaec23ae24f822370e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="using-storage-explorer-preview-with-azure-file-storage"></a>Korzystanie z programu Storage Explorer (wersja zapoznawcza) za pośrednictwem usługi Azure File Storage

Plik Azure magazynu znajduje się, że usługa, która umożliwia pliku udziałów w chmurze hello przy użyciu hello standardowego protokołu bloku komunikatów serwera (SMB). Obsługiwane są wersje 2.1 i 3.0 protokołu SMB. Magazyn plików Azure można migrować starsze aplikacje korzystające z tooAzure udziały plików szybko i bez kosztownych modyfikacji oprogramowania. Możesz użyć pliku magazynu tooexpose danych publicznie toohello world lub toostore danych aplikacji prywatnie. W tym artykule dowiesz się, jak toouse toowork Eksploratora usługi Storage (wersja zapoznawcza) z plików, udziały i pliki.

## <a name="prerequisites"></a>Wymagania wstępne

toocomplete hello kroki opisane w tym artykule, będą potrzebne następujące hello:

- [Pobieranie i instalowanie Eksploratora usługi Storage (wersja zapoznawcza)](http://www.storageexplorer.com/)

- [Połącz tooa kontem magazynu platformy Azure lub usługi](https://docs.microsoft.com//azure/vs-azure-tools-storage-manage-with-storage-explorer#connect-to-a-storage-account-or-service)

## <a name="create-a-file-share"></a>Tworzenie udziału plików

Wszystkie pliki muszą znajdować się w udziale plików, który jest po prostu logiczną grupą plików. Konto może zawierać nieograniczoną liczbę udziałów plików, a każdy udział może obejmować nieograniczoną liczbę plików.

Witaj następujące kroki pokazują, jak toocreate, udostępniania plików, w ramach Eksploratora usługi Storage (wersja zapoznawcza).

1. Otwórz Eksploratora usługi Storage (wersja zapoznawcza).

2. W okienku po lewej stronie hello rozwiń hello konta magazynu w ramach którego ma zostać hello toocreate udziału plików

3. Kliknij prawym przyciskiem myszy **udziałów plików**i z menu kontekstowego hello — wybierz pozycję **Utwórz udział plików**.

    ![Tworzenie udziału plików](media/vs-azure-tools-storage-explorer-files/image1.png)

4. Pole tekstowe pojawi się poniżej hello **udziałów plików** folderu. Wprowadź nazwę hello udziału plików. Zobacz hello [udostępnianie reguły nazewnictwa](https://docs.microsoft.com//azure/storage/storage-dotnet-how-to-use-blobs#create-a-container) sekcja zawiera listę reguł i ograniczenia dotyczące nazewnictwa udziałów plików.

    ![Nazewnictwo hello udziału](media/vs-azure-tools-storage-explorer-files/image2.png)

5. Naciśnij klawisz **Enter** podczas done toocreate hello udziału plików lub **Esc** toocancel. Po pomyślnie utworzono udział plików hello, będzie on wyświetlany w obszarze hello **udziałów plików** folder hello wybranego konta magazynu.

    ![Witaj nowego udziału.](media/vs-azure-tools-storage-explorer-files/image3.png)

## <a name="view-a-file-shares-contents"></a>Wyświetlanie zawartości udziału plików

Udziały plików zawierają pliki i foldery (które mogą również zawierać pliki).

Hello następujące kroki ilustrują sposób udostępnienia tooview hello zawartości pliku w Eksploratora usługi Storage (wersja zapoznawcza): +

1. Otwórz Eksploratora usługi Storage (wersja zapoznawcza).

2. W okienku po lewej stronie powitania rozwiń konto magazynu hello zawierające hello udziału plików mają tooview.

3. Rozwiń konto magazynu hello **udziałów plików**.

4. Udział plików kliknij prawym przyciskiem myszy hello konieczność tooview i — wybierz z menu kontekstowego hello - **Otwórz**. Można także kliknąć dwukrotnie hello udziału plików mają tooview.

    ![Otwieranie udziału](media/vs-azure-tools-storage-explorer-files/image4.png)

5. Witaj głównego okienku zostaną wyświetlone udziału plików hello zawartość.
    
    ![Witaj udziału zawartości](media/vs-azure-tools-storage-explorer-files/image5.png)

## <a name="delete-a-file-share"></a>Usuwanie udziału plików

Udziały plików można łatwo tworzyć i usuwać. (toosee jak toodelete poszczególnych plików, można znaleźć w sekcji toohello [zarządzania plikami w udziale plików](https://docs.microsoft.com//azure/vs-azure-tools-storage-explorer-blobs#managing-blobs-in-a-blob-container).)

następujące kroki Hello ilustrują sposób toodelete, udostępniania plików, w ramach Eksploratora usługi Storage (wersja zapoznawcza):

1. Otwórz Eksploratora usługi Storage (wersja zapoznawcza).

2. W okienku po lewej stronie powitania rozwiń konto magazynu hello zawierające hello udziału plików mają tooview.

3. Rozwiń konto magazynu hello **udziałów plików**.

4. Udział plików kliknij prawym przyciskiem myszy hello konieczność toodelete i — wybierz z menu kontekstowego hello - **usunąć**. Można również nacisnąć **usunąć** toodelete hello aktualnie wybranego pliku udziału.

    ![Usuwanie](media/vs-azure-tools-storage-explorer-files/image6.png)

5. Wybierz **tak** toohello okno dialogowe potwierdzenia.
    
    ![Okno dialogowe potwierdzenia](media/vs-azure-tools-storage-explorer-files/image7.png)

## <a name="copy-a-file-share"></a>Kopiowanie udziału plików

Eksplorator usługi Storage (wersja zapoznawcza) umożliwia toocopy Schowek toohello udziału pliku, a następnie wklej tego udziału pliku do innego konta magazynu. (toosee jak toocopy poszczególnych plików, można znaleźć w sekcji toohello [zarządzania plikami w udziale plików](https://docs.microsoft.com//azure/vs-azure-tools-storage-explorer-blobs#managing-blobs-in-a-blob-container).)

Witaj następujące kroki pokazują, jak udostępnić toocopy plik z jednym tooanother konta magazynu.

1. Otwórz Eksploratora usługi Storage (wersja zapoznawcza).

2. W okienku po lewej stronie powitania rozwiń konto magazynu hello zawierające hello udziału plików mają toocopy.

3. Rozwiń konto magazynu hello **udziałów plików**.

4. Udział plików kliknij prawym przyciskiem myszy hello konieczność toocopy i — wybierz z menu kontekstowego hello - **udział plików kopii**.

    ![Kopiowanie udziału plików](media/vs-azure-tools-storage-explorer-files/image8.png)

5. Kliknij prawym przyciskiem myszy konto magazynu Witaj "wartość", do którego chcesz udziału plików hello toopaste, a — wybierz z menu kontekstowego hello - **udział plików Wklej**.

    ![Wklejanie udziału plików](media/vs-azure-tools-storage-explorer-files/image9.png)

## <a name="get-hello-sas-for-a-file-share"></a>Pobierz hello sygnatury dostępu Współdzielonego dla udziału plików

A [sygnatury dostępu współdzielonego (SAS)](https://docs.microsoft.com//azure/storage/storage-dotnet-shared-access-signature-part-1) zapewnia dostęp delegowany tooresources na koncie magazynu. Oznacza to, że można udzielać się, że klient ograniczone uprawnienia tooobjects na koncie magazynu w określonym przedziale czasu i z określonym zestawem uprawnień, bez konieczności tooshare klucze dostępu do Twojego konta.

Witaj poniższe kroki przedstawiają sposób toocreate sygnatury dostępu Współdzielonego dla pliku udziału: +

1. Otwórz Eksploratora usługi Storage (wersja zapoznawcza).

2. W okienku po lewej stronie powitania rozwiń konto magazynu hello zawierające hello udziału plików, dla którego chcesz tooget sygnatury dostępu Współdzielonego.

3. Rozwiń konto magazynu hello **udziałów plików**.

4. Kliknij prawym przyciskiem myszy hello udziału żądanego pliku i z menu kontekstowego hello — wybierz pozycję **Uzyskaj sygnaturę dostępu współdzielonego**.

    ![Uzyskiwanie sygnatury dostępu współdzielonego](media/vs-azure-tools-storage-explorer-files/image10.png)

5. W hello **sygnatura dostępu współdzielonego** okna dialogowego, określ hello zasad, daty rozpoczęcia i wygaśnięcia, strefy czasowej, a dla zasobu hello poziomy dostępu.

    ![Okno dialogowe sygnatury dostępu współdzielonego](media/vs-azure-tools-storage-explorer-files/image11.png)

6. Po zakończeniu określenie opcji SAS hello wybierz **Utwórz**.

7. Drugi **sygnatura dostępu współdzielonego** okna dialogowego zostanie następnie wyświetlona, że listy hello udziału plików wraz z adresu URL hello i QueryStrings można użyć tooaccess hello zasobów magazynu. Wybierz **kopiowania** dalej toohello adres URL ma toocopy toohello Schowka.
    
    ![Drugie okno dialogowe Sygnatura dostępu współdzielonego](media/vs-azure-tools-storage-explorer-files/image12.png)

8. Po zakończeniu wybierz pozycję **Zamknij**.

## <a name="manage-access-policies-for-a-file-share"></a>Zarządzanie zasadami dostępu dla udziału plików

Witaj poniższe kroki przedstawiają sposób toomanage (Dodaj i Usuń) zasady dla udziału plików dostępu: +. Zasady dostępu Hello jest używane do tworzenia adresów URL SAS za pośrednictwem której osoby mogą używać hello tooaccess zasobu magazynu plików w zdefiniowanym okresie.

1. Otwórz Eksploratora usługi Storage (wersja zapoznawcza).

2. W okienku po lewej stronie powitania rozwiń konto magazynu hello zawierające udziału plików hello zasad dostępu, którego chcesz toomanage.

3. Rozwiń konto magazynu hello **udziałów plików**.

4. Wybierz udział żądanego pliku hello i — wybierz z menu kontekstowego hello - **Zarządzanie zasadami dostępu**.

    ![Menu kontekstowe Zarządzanie zasadami dostępu](media/vs-azure-tools-storage-explorer-files/image13.png)

5. Witaj **zasady dostępu** okno dialogowe wyświetla wszystkie zasady dostępu dla udziału plików wybranych hello już utworzony.
    
    ![Zasady dostępu](media/vs-azure-tools-storage-explorer-files/image14.png)

6. Wykonaj następujące kroki w zależności od zadania zarządzania zasadami dostępu hello:
    
    - **Dodawanie nowych zasad dostępu** — wybierz pozycję **Dodaj**. Wygenerowany hello **zasady dostępu** hello nowo dodanych do wyświetlenia okna dialogowego dostęp zasad (przy użyciu ustawień domyślnych).

    - **Edytowanie zasad dostępu** — wykonaj wszystkie żądane operacje edycji, a następnie wybierz pozycję **Zapisz**.

    - **Usuń zasady dostępu** — wybierz tę opcję **Usuń** dalej toohello zasady dostępu mają tooremove.

7. Utwórz nowy adres URL sygnatury dostępu Współdzielonego przy użyciu hello utworzoną wcześniej zasad dostępu:
    
    ![Pobieranie sygnatury dostępu współdzielonego](media/vs-azure-tools-storage-explorer-files/image15.png)
    
    ![Nazwa i właściwości sygnatury dostępu współdzielonego](media/vs-azure-tools-storage-explorer-files/image16.png)

## <a name="managing-files-in-a-file-share"></a>Zarządzanie plikami w udziale plików

Po utworzeniu udziału plików można przekazać pliku toothat udziału plików, Pobierz plik tooyour komputera lokalnego, otwórz plik na komputerze lokalnym i wiele innych.

Witaj poniższe kroki przedstawiają jak udostępnić toomanage hello plików (i foldery) w pliku.

1.  Otwórz Eksploratora usługi Storage (wersja zapoznawcza).

2.  W okienku po lewej stronie powitania rozwiń konto magazynu hello zawierające hello udziału plików mają toomanage.

3.  Rozwiń konto magazynu hello **udziałów plików**.

4.  Kliknij dwukrotnie hello udziału plików mają tooview.

5.  Witaj głównego okienku zostaną wyświetlone udziału plików hello zawartość.

    ![Witaj udziału zawartości](media/vs-azure-tools-storage-explorer-files/image17.png)

6.  Witaj głównego okienku zostaną wyświetlone udziału plików hello zawartość.

7.  Wykonaj następujące kroki w zależności od zadania hello mają tooperform:

    - **Przekaż udziału plików tooa plików**

        a.  W okienku głównym hello narzędzi, wybierz **przekazać**, a następnie **Przekaż** z menu rozwijanego hello.

        ![Przekazywanie plików](media/vs-azure-tools-storage-explorer-files/image18.png)
        
        b. W hello **przekazać pliki** okno dialogowe, wybierz hello wielokropka (**...** ) przycisku po prawej stronie powitania hello **pliki** tooselect hello pliki mają tooupload polu tekstowym.

        ![Dodawanie plików](media/vs-azure-tools-storage-explorer-files/image19.png)

        c. Wybierz pozycję **Przekaż**.

    - **Przekaż udziału plików tooa folderu**
        
        a. Na pasku narzędzi w okienku głównym hello, wybierz **przekazać**, a następnie **przekazać folderu** z menu rozwijanego hello.

        ![Menu Przekaż folder](media/vs-azure-tools-storage-explorer-files/image20.png)

        b. W hello **folder przekazywania** okno dialogowe, wybierz hello wielokropka (**...** ) przycisku po prawej stronie powitania hello **folderu** tekst pola tooselect hello folder zawartości, którego chcesz tooupload.

        c. Opcjonalnie określ folder docelowy, w których hello zostanie przekazany zawartość wybranego folderu. Witaj, folder docelowy nie istnieje, zostanie utworzona.

        d. Wybierz pozycję **Przekaż**.

    - **Pobierz plik tooyour komputera lokalnego**
        
        a. Wybierz plik hello mają toodownload.
        
        b. W okienku głównym hello narzędzi wybierz **Pobierz**.
        
        c. W hello **Określ, gdzie toosave hello pobrany plik** okna dialogowego, określ hello lokalizację pliku hello pobrane i hello nazwę mają toogive go.

        d. Wybierz pozycję **Zapisz**.

    - **Otwieranie pliku na komputerze lokalnym**
        
        a.  Wybierz plik hello mają tooopen.
        
        b.  W okienku głównym hello narzędzi wybierz **Otwórz**.
        
        c.  Plik Hello zostaną pobrane i otworzyć przy użyciu aplikacji hello skojarzonej z hello podstawowy typ pliku.

    - **Skopiuj plik toohello Schowka**

        a. Wybierz plik hello mają toocopy.

        b. W okienku głównym hello narzędzi wybierz **kopiowania**.

        c. W okienku po lewej stronie powitania, przejdź do udziału plików tooanother i kliknij ją dwukrotnie tooview w okienku głównym hello.

        d. W okienku głównym hello narzędzi wybierz **Wklej** toocreate kopię pliku hello.

    - **Usuwanie pliku**

        a. Wybierz plik hello mają toodelete.

        b. W okienku głównym hello narzędzi wybierz **usunąć**.

        c. Wybierz **tak** toohello okno dialogowe potwierdzenia.

## <a name="next-steps"></a>Następne kroki

- Widok hello [najnowsze informacje o wersji Eksploratora usługi Storage (wersja zapoznawcza) i filmy wideo](http://www.storageexplorer.com/).

- Dowiedz się, jak za[tworzenie aplikacji przy użyciu Azure blob, tabel, kolejek i plików](https://azure.microsoft.com/documentation/services/storage/).
