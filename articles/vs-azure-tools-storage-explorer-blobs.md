---
title: "aaaManage zasobów magazynu obiektów Blob Azure przy użyciu Eksploratora usługi Storage (wersja zapoznawcza) | Dokumentacja firmy Microsoft"
description: "Zarządzanie kontenerów obiektów Blob platformy Azure i obiektów blob z Eksploratora usługi Storage (wersja zapoznawcza)"
services: storage
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 2f09e545-ec94-4d89-b96c-14783cc9d7a9
ms.service: storage
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/18/2016
ms.author: kraigb
ms.openlocfilehash: 503dd061b205875da127378ab48e8d465800fc09
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-blob-storage-resources-with-storage-explorer-preview"></a>Zarządzanie zasobami magazynu obiektów Blob Azure za pomocą Eksploratora usługi Storage (wersja zapoznawcza)
## <a name="overview"></a>Omówienie
[Magazyn obiektów Blob Azure](storage/blobs/storage-dotnet-how-to-use-blobs.md) to usługa do przechowywania dużych ilości danych bez struktury, takich jak dane tekstowe lub binarne, który można uzyskać z dowolnego miejsca w Witaj świecie za pośrednictwem protokołu HTTP lub HTTPS.
Możesz użyć danych tooexpose magazynu obiektów Blob publicznie toohello world lub toostore danych aplikacji prywatnie. W tym artykule dowiesz się, jak toouse toowork Eksploratora usługi Storage (wersja zapoznawcza) z obiektu blob kontenerów i obiektów blob.

## <a name="prerequisites"></a>Wymagania wstępne
toocomplete hello kroki opisane w tym artykule, będą potrzebne następujące hello:

* [Pobieranie i instalowanie Eksploratora usługi Storage (wersja zapoznawcza)](http://www.storageexplorer.com)
* [Połącz tooa kontem magazynu platformy Azure lub usługi](vs-azure-tools-storage-manage-with-storage-explorer.md#connect-to-a-storage-account-or-service)

## <a name="create-a-blob-container"></a>Tworzenie kontenera obiektów blob
Wszystkie obiekty BLOB muszą znajdować się w kontenerze obiektów blob to po prostu logiczne grupowanie obiektów blob. Konto może zawierać nieograniczoną liczbę kontenerów, a każdy kontener może przechowywać nieograniczoną liczbę obiektów blob.

Witaj poniższe kroki przedstawiają sposób toocreate kontener obiektów blob w ramach Eksploratora usługi Storage (wersja zapoznawcza).

1. Otwórz Eksploratora usługi Storage (wersja zapoznawcza).
2. W okienku po lewej stronie powitania rozwiń hello konta magazynu w ramach którego ma zostać kontenera obiektów blob hello toocreate.
3. Kliknij prawym przyciskiem myszy **kontenerów obiektów Blob**i z menu kontekstowego hello — wybierz pozycję **Tworzenie kontenera obiektów Blob**.

   ![Tworzenie menu kontekstowe kontenerów obiektów blob][0]
4. Pole tekstowe pojawi się poniżej hello **kontenerów obiektów Blob** folderu. Wprowadź nazwę hello kontenerze obiektu blob. Zobacz hello [reguły nazewnictwa kontenera](storage/blobs/storage-dotnet-how-to-use-blobs.md#create-a-container) sekcja zawiera listę reguł i ograniczenia dotyczące nazewnictwa kontenerów obiektów blob.

   ![Tworzenie pola tekstowego kontenerów obiektów Blob][1]
5. Naciśnij klawisz **Enter** po zakończeniu toocreate kontenera obiektów blob hello, lub **Esc** toocancel. Po pomyślnym utworzeniu kontenera obiektów blob hello będzie wyświetlana w obszarze hello **kontenerów obiektów Blob** folder hello wybranego konta magazynu.

   ![Utworzyć kontener obiektów blob][2]

## <a name="view-a-blob-containers-contents"></a>Wyświetlanie zawartości kontenera obiektów blob
Kontenerów obiektów blob zawiera obiekty BLOB i folderów (które może również zawierać obiektów blob).

Witaj poniższe kroki przedstawiają sposób zawartość hello tooview kontenera obiektów blob w ramach Eksploratora usługi Storage (wersja zapoznawcza):

1. Otwórz Eksploratora usługi Storage (wersja zapoznawcza).
2. W okienku po lewej stronie powitania rozwiń konto magazynu hello zawierające hello kontenera obiektów blob mają tooview.
3. Rozwiń konto magazynu hello **kontenerów obiektów Blob**.
4. Kontener obiektów blob powitania kliknij prawym przyciskiem myszy konieczność tooview i — wybierz z menu kontekstowego hello - **Otwórz Edytor kontenera obiektów Blob**.
   Możesz również kliknąć dwukrotnie hello kontenera obiektów blob mają tooview.

   ![Menu kontekstowe edytora kontenera obiektów blob Otwórz][19]
5. Witaj głównego okienku zostaną wyświetlone kontenera obiektów blob hello zawartość.

   ![Edytor kontenera obiektów blob][3]

## <a name="delete-a-blob-container"></a>Usunięcie kontenera obiektów blob
Kontenerów obiektów blob można łatwo tworzyć i usunięte zgodnie z potrzebami. (toosee jak toodelete poszczególne obiekty BLOB, można znaleźć w sekcji toohello [Zarządzanie obiekty BLOB w kontenerze obiektów blob](#managing-blobs-in-a-blob-container).)

Witaj poniższe kroki przedstawiają sposób toodelete kontener obiektów blob w ramach Eksploratora usługi Storage (wersja zapoznawcza):

1. Otwórz Eksploratora usługi Storage (wersja zapoznawcza).
2. W okienku po lewej stronie powitania rozwiń konto magazynu hello zawierające hello kontenera obiektów blob mają tooview.
3. Rozwiń konto magazynu hello **kontenerów obiektów Blob**.
4. Kontener obiektów blob powitania kliknij prawym przyciskiem myszy konieczność toodelete i — wybierz z menu kontekstowego hello - **usunąć**.
   Można również nacisnąć **usunąć** toodelete hello aktualnie zaznaczonego obiektu blob kontenera.

   ![Usuwanie menu kontekstowe kontenera obiektów blob][4]
5. Wybierz **tak** toohello okno dialogowe potwierdzenia.

   ![Usuwanie obiektów blob kontenera potwierdzenia][5]

## <a name="copy-a-blob-container"></a>Skopiuj kontenera obiektów blob
Eksplorator usługi Storage (wersja zapoznawcza) umożliwia toocopy Schowek toohello kontenera obiektów blob, a następnie wklej, który kontenera obiektów blob na innym koncie magazynu. (toosee jak toocopy poszczególne obiekty BLOB, można znaleźć w sekcji toohello [Zarządzanie obiekty BLOB w kontenerze obiektów blob](#managing-blobs-in-a-blob-container).)

Witaj następujące kroki pokazują, jak toocopy kontenera obiektów blob z jednego magazynu konta tooanother.

1. Otwórz Eksploratora usługi Storage (wersja zapoznawcza).
2. W okienku po lewej stronie powitania rozwiń konto magazynu hello zawierające hello kontenera obiektów blob mają toocopy.
3. Rozwiń konto magazynu hello **kontenerów obiektów Blob**.
4. Kontener obiektów blob powitania kliknij prawym przyciskiem myszy konieczność toocopy i — wybierz z menu kontekstowego hello - **kontenera obiektów Blob kopii**.

   ![Kopiowanie menu kontekstowe kontenera obiektów blob][6]
5. Kliknij prawym przyciskiem myszy konto magazynu Witaj "wartość", do którego chcesz kontenera obiektów blob hello toopaste, a - z menu kontekstowego hello — wybierz **kontenera obiektów Blob Wklej**.

   ![Menu kontekstowe kontenera obiektów blob wklejania][7]

## <a name="get-hello-sas-for-a-blob-container"></a>Pobierz hello SAS dla kontenera obiektów blob
A [sygnatury dostępu współdzielonego (SAS)](storage/common/storage-dotnet-shared-access-signature-part-1.md) zapewnia dostęp delegowany tooresources na koncie magazynu.
Oznacza to, że można udzielać się, że klient ograniczone uprawnienia tooobjects na koncie magazynu w określonym przedziale czasu i z określonym zestawem uprawnień, bez konieczności udostępniania kluczy dostępu konta.

Witaj poniższe kroki przedstawiają sposób toocreate sygnatury dostępu Współdzielonego dla kontenera obiektów blob:

1. Otwórz Eksploratora usługi Storage (wersja zapoznawcza).
2. W okienku po lewej stronie powitania rozwiń konto magazynu hello zawierające hello kontenera obiektów blob, dla którego chcesz tooget sygnatury dostępu Współdzielonego.
3. Rozwiń konto magazynu hello **kontenerów obiektów Blob**.
4. Kliknij prawym przyciskiem myszy kontener obiektów blob żądaną hello i — wybierz z menu kontekstowego hello - **Uzyskaj sygnaturę dostępu współdzielonego**.

   ![Uzyskiwanie sygnatury dostępu Współdzielonego menu kontekstowe][8]
5. W hello **sygnatura dostępu współdzielonego** okna dialogowego, określ hello zasad, daty rozpoczęcia i wygaśnięcia, strefy czasowej, a dla zasobu hello poziomy dostępu.

   ![Opcje SAS][9]
6. Po zakończeniu określenie opcji SAS hello wybierz **Utwórz**.
7. Drugi **sygnatura dostępu współdzielonego** okna dialogowego zostanie następnie wyświetlona, że listy hello kontenera obiektów blob oraz adres URL hello i QueryStrings można użyć tooaccess hello zasobów magazynu.
   Wybierz **kopiowania** dalej toohello adres URL ma toocopy toohello Schowka.

   ![Skopiuj adresy URL SAS][10]
8. Po zakończeniu wybierz pozycję **Zamknij**.

## <a name="manage-access-policies-for-a-blob-container"></a>Zarządzanie zasadami dostępu do kontenera obiektów blob
Witaj poniższe kroki przedstawiają sposób toomanage (Dodaj i Usuń) zasady dla kontenera obiektów blob dostępu:

1. Otwórz Eksploratora usługi Storage (wersja zapoznawcza).
2. W okienku po lewej stronie powitania rozwiń konto magazynu hello zawierające kontenera obiektów blob hello zasad dostępu, którego chcesz toomanage.
3. Rozwiń konto magazynu hello **kontenerów obiektów Blob**.
4. Wybierz kontener obiektów blob żądaną hello i — wybierz z menu kontekstowego hello - **Zarządzanie zasadami dostępu**.

   ![Menu kontekstowe Zarządzanie zasadami dostępu][11]
5. Witaj **zasady dostępu** okno dialogowe wyświetla wszystkie zasady dostępu dla kontenera obiektów blob wybranego hello już utworzone.

   ![Opcje zasad dostępu][12]        
6. Wykonaj następujące kroki w zależności od zadania zarządzania zasadami dostępu hello:

   * **Dodawanie nowych zasad dostępu** — wybierz pozycję **Dodaj**. Wygenerowany hello **zasady dostępu** hello nowo dodanych do wyświetlenia okna dialogowego dostęp zasad (przy użyciu ustawień domyślnych).
   * **Edytowanie zasad dostępu** — wprowadź żądane zmiany i wybierz **zapisać**.
   * **Usuń zasady dostępu** — wybierz tę opcję **Usuń** dalej toohello zasady dostępu mają tooremove.

## <a name="set-hello-public-access-level-for-a-blob-container"></a>Ustaw hello poziom dostępu publicznego kontenera obiektów blob
Domyślnie każdy kontener obiektów blob jest ustawiona zbyt "Brak dostępu publicznego".

Hello poniższe kroki przedstawiają sposób toospecify publiczny dostęp do poziomu kontenera obiektów blob.

1. Otwórz Eksploratora usługi Storage (wersja zapoznawcza).
2. W okienku po lewej stronie powitania rozwiń konto magazynu hello zawierające kontenera obiektów blob hello zasad dostępu, którego chcesz toomanage.
3. Rozwiń konto magazynu hello **kontenerów obiektów Blob**.
4. Wybierz kontener obiektów blob żądaną hello i — wybierz z menu kontekstowego hello - **Ustaw poziom dostępu publicznego**.

   ![Menu kontekstowe poziomu dostępu publicznego zestawu][13]
5. W hello **Ustaw poziom dostępu publicznego kontenera** okna dialogowego, określ hello żądany poziom dostępu.

   ![Ustaw opcje poziomu dostępu publicznego][14]
6. Wybierz przycisk **Zastosuj**.

## <a name="managing-blobs-in-a-blob-container"></a>Zarządzanie obiekty BLOB w kontenerze obiektów blob
Po utworzeniu kontenera obiektów blob można przekazać kontenera obiektów blob toothat obiektów blob, Pobierz komputera lokalnego tooyour obiektów blob, otwórz obiektu blob na komputerze lokalnym i wiele innych.

Witaj następujące kroki pokazują, jak toomanage hello obiektów blob (i foldery) w kontenerze obiektów blob.

1. Otwórz Eksploratora usługi Storage (wersja zapoznawcza).
2. W okienku po lewej stronie powitania rozwiń konto magazynu hello zawierające hello kontenera obiektów blob mają toomanage.
3. Rozwiń konto magazynu hello **kontenerów obiektów Blob**.
4. Kliknij dwukrotnie hello kontenera obiektów blob mają tooview.
5. Witaj głównego okienku zostaną wyświetlone kontenera obiektów blob hello zawartość.

   ![Widok kontenera obiektów blob][3]
6. Witaj głównego okienku zostaną wyświetlone kontenera obiektów blob hello zawartość.
7. Wykonaj następujące kroki w zależności od zadania hello mają tooperform:

   * **Przekaż kontenera obiektów blob tooa plików**

     1. W okienku głównym hello narzędzi, wybierz **przekazać**, a następnie **Przekaż** z menu rozwijanego hello.

        ![Przekazywanie plików menu][15]
     2. W hello **przekazać pliki** okno dialogowe, wybierz hello wielokropka (**...** ) przycisku po prawej stronie powitania hello **pliki** tooselect hello pliki mają tooupload polu tekstowym.

        ![Przekazywanie plików opcje][16]
     3. Określ typ hello **typu obiektu Blob**. Artykuł Hello [Rozpoczynanie pracy z magazynem obiektów Blob platformy Azure przy użyciu platformy .NET](storage/blobs/storage-dotnet-how-to-use-blobs.md#blob-service-concepts) wyjaśniono hello różnice między hello różnych typów obiektów blob.
     4. Opcjonalnie określ folder docelowy, do którego zostanie przekazany hello wybranych plików. Witaj, folder docelowy nie istnieje, zostanie utworzona.
     5. Wybierz pozycję **Przekaż**.
   * **Przekaż kontenera obiektów blob tooa folderu**

     1. Na pasku narzędzi w okienku głównym hello, wybierz **przekazać**, a następnie **przekazać folderu** z menu rozwijanego hello.

        ![Menu Przekaż folder][17]
     2. W hello **folder przekazywania** okno dialogowe, wybierz hello wielokropka (**...** ) przycisku po prawej stronie powitania hello **folderu** tekst pola tooselect hello folder zawartości, którego chcesz tooupload.

        ![Przekaż Opcje folderów][18]
     3. Określ typ hello **typu obiektu Blob**. Artykuł Hello [Rozpoczynanie pracy z magazynem obiektów Blob platformy Azure przy użyciu platformy .NET](storage/blobs/storage-dotnet-how-to-use-blobs.md#blob-service-concepts) wyjaśniono hello różnice między hello różnych typów obiektów blob.
     4. Opcjonalnie określ folder docelowy, w których hello zostanie przekazany zawartość wybranego folderu. Witaj, folder docelowy nie istnieje, zostanie utworzona.
     5. Wybierz pozycję **Przekaż**.
   * **Pobieranie obiektu blob tooyour komputera lokalnego**

     1. Wybierz hello obiektu blob mają toodownload.
     2. W okienku głównym hello narzędzi wybierz **Pobierz**.
     3. W hello **Określ, którego toosave hello pobrany obiekt blob** okna dialogowego, określ hello lokalizacji obiektu blob hello pobrane i hello nazwę mają toogive go.  
     4. Wybierz pozycję **Zapisz**.
   * **Otwórz obiektu blob na komputerze lokalnym**

     1. Wybierz hello obiektu blob mają tooopen.
     2. W okienku głównym hello narzędzi wybierz **Otwórz**.
     3. Obiekt blob Hello zostaną pobrane i otwarty aplikacji hello skojarzone z typem bazowym pliku hello blob.
   * **Kopiuj do Schowka toohello obiektów blob**

     1. Wybierz hello obiektu blob mają toocopy.
     2. W okienku głównym hello narzędzi wybierz **kopiowania**.
     3. W okienku po lewej stronie powitania, przejdź do kontenera obiektów blob tooanother i kliknij ją dwukrotnie tooview w okienku głównym hello.
     4. W okienku głównym hello narzędzi wybierz **Wklej** toocreate kopię hello obiektu blob.
   * **Usuwanie obiektu blob**

     1. Wybierz hello obiektu blob mają toodelete.
     2. W okienku głównym hello narzędzi wybierz **usunąć**.
     3. Wybierz **tak** toohello okno dialogowe potwierdzenia.

## <a name="next-steps"></a>Następne kroki
* Widok hello [najnowsze informacje o wersji Eksploratora usługi Storage (wersja zapoznawcza) i filmy wideo](http://www.storageexplorer.com).
* Dowiedz się, jak za[tworzenie aplikacji przy użyciu Azure blob, tabel, kolejek i plików](https://azure.microsoft.com/documentation/services/storage/).

[0]: ./media/vs-azure-tools-storage-explorer-blobs/blob-containers-create-context-menu.png
[1]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-create.png
[2]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-create-done.png
[3]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-editor.png
[4]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-delete-context-menu.png
[5]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-delete-confirmation.png
[6]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-copy-context-menu.png
[7]: ./media/vs-azure-tools-storage-explorer-blobs/blob-containers-paste-context-menu.png
[8]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-get-sas-context-menu.png
[9]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-get-sas-options.png
[10]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-get-sas-urls.png
[11]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-manage-access-policies-context-menu.png
[12]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-manage-access-policies-options.png
[13]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-set-public-access-level-context-menu.png
[14]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-set-public-access-level-options.png
[15]: ./media/vs-azure-tools-storage-explorer-blobs/blob-upload-files-menu.png
[16]: ./media/vs-azure-tools-storage-explorer-blobs/blob-upload-files-options.png
[17]: ./media/vs-azure-tools-storage-explorer-blobs/blob-upload-folder-menu.png
[18]: ./media/vs-azure-tools-storage-explorer-blobs/blob-upload-folder-options.png
[19]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-open-editor-context-menu.png
