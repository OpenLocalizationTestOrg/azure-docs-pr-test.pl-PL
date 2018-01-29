---
title: "Korzystanie z programu Storage Explorer (wersja zapoznawcza) za pośrednictwem usługi Azure File Storage | Microsoft Docs"
description: "Dowiedz się, jak korzystać z programu Storage Explorer (wersja zapoznawcza) w celu pracy z udziałami plików i plikami."
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
ms.openlocfilehash: 964691758254531cb92a5b1cbe055ef61d25dba8
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/11/2017
---
# <a name="using-storage-explorer-preview-with-azure-file-storage"></a>Korzystanie z programu Storage Explorer (wersja zapoznawcza) za pośrednictwem usługi Azure File Storage

Azure File Storage to usługa, która umożliwia korzystanie z udziałów plików w chmurze przy użyciu standardowego protokołu bloku komunikatów serwera (SMB, Server Message Block). Obsługiwane są wersje 2.1 i 3.0 protokołu SMB. W usłudze Magazyn plików Azure można migrować starsze aplikacje korzystające z udziałów plików na platformę Azure szybko i bez kosztownych modyfikacji oprogramowania. Usługa File Storage może być używana do udostępniania danych publicznie lub do przechowywania danych aplikacji prywatnie. Ten artykuł zawiera informacje dotyczące sposobu korzystania z programu Storage Explorer (wersja zapoznawcza) w celu pracy z udziałami plików i plikami.

## <a name="prerequisites"></a>Wymagania wstępne

Do wykonania kroków opisanych w tym artykule konieczne jest wykonanie kroków znajdujących się w następujących artykułach:

- [Pobieranie i instalowanie Eksploratora usługi Storage (wersja zapoznawcza)](http://www.storageexplorer.com/)

- [Łączenie się z usługą lub kontem magazynu platformy Azure](https://docs.microsoft.com//azure/vs-azure-tools-storage-manage-with-storage-explorer#connect-to-a-storage-account-or-service)

## <a name="create-a-file-share"></a>Tworzenie udziału plików

Wszystkie pliki muszą znajdować się w udziale plików, który jest po prostu logiczną grupą plików. Konto może zawierać nieograniczoną liczbę udziałów plików, a każdy udział może obejmować nieograniczoną liczbę plików.

Poniższe kroki ilustrują tworzenie udziału plików w programie Storage Explorer (wersja zapoznawcza).

1. Otwórz Eksploratora usługi Storage (wersja zapoznawcza).

2. W okienku po lewej stronie rozwiń konto magazynu, w którym chcesz utworzyć udział plików

3. Kliknij prawym przyciskiem myszy pozycję **Udziały plików**, a następnie z menu kontekstowego wybierz pozycję **Utwórz udział plików**.

    ![Tworzenie udziału plików](media/vs-azure-tools-storage-explorer-files/image1.png)

4. Poniżej folderu **Udziały plików** zostanie wyświetlone pole tekstowe. Wprowadź nazwę udziału plików. Lista reguł i ograniczeń dotyczących nazewnictwa udziałów plików znajduje się w sekcji [Reguły nazewnictwa udziałów](https://docs.microsoft.com//azure/storage/storage-dotnet-how-to-use-blobs#create-a-container).

    ![Nazywanie udziału](media/vs-azure-tools-storage-explorer-files/image2.png)

5. Naciśnij klawisz **Enter** po zakończeniu tworzenia udziału plików lub klawisz **Esc**, aby anulować. Po pomyślnym utworzeniu udział plików zostanie wyświetlony w folderze **Udziały plików** dla wybranego konta magazynu.

    ![Nowy udział](media/vs-azure-tools-storage-explorer-files/image3.png)

## <a name="view-a-file-shares-contents"></a>Wyświetlanie zawartości udziału plików

Udziały plików zawierają pliki i foldery (które mogą również zawierać pliki).

Poniższe kroki ilustrują wyświetlanie zawartości udziału plików w programie Storage Explorer (wersja zapoznawcza):

1. Otwórz Eksploratora usługi Storage (wersja zapoznawcza).

2. W okienku po lewej stronie rozwiń konto magazynu zawierające udział plików, który chcesz wyświetlić.

3. Rozwiń pozycję **Udziały plików** konta magazynu.

4. Kliknij prawym przyciskiem myszy udział plików, który chcesz wyświetlić, a następnie z menu kontekstowego wybierz pozycję **Otwórz**. Możesz także kliknąć dwukrotnie udział plików, który chcesz wyświetlić.

    ![Otwieranie udziału](media/vs-azure-tools-storage-explorer-files/image4.png)

5. W okienku głównym zostanie wyświetlona zawartość udziału plików.
    
    ![Zawartość udziału](media/vs-azure-tools-storage-explorer-files/image5.png)

## <a name="delete-a-file-share"></a>Usuwanie udziału plików

Udziały plików można łatwo tworzyć i usuwać. Informacje na temat sposobu usuwania pojedynczych plików zawiera sekcja [Managing files in a file share](https://docs.microsoft.com//azure/vs-azure-tools-storage-explorer-blobs#managing-blobs-in-a-blob-container) (Zarządzanie plikami w udziale plików).

Poniższe kroki ilustrują usuwanie udziału plików w programie Storage Explorer (wersja zapoznawcza):

1. Otwórz Eksploratora usługi Storage (wersja zapoznawcza).

2. W okienku po lewej stronie rozwiń konto magazynu zawierające udział plików, który chcesz wyświetlić.

3. Rozwiń pozycję **Udziały plików** konta magazynu.

4. Kliknij prawym przyciskiem myszy udział plików, który chcesz usunąć, a następnie z menu kontekstowego wybierz pozycję **Usuń**. Możesz również nacisnąć klawisz **Delete**, aby usunąć aktualnie wybrany udział plików.

    ![Usuwanie](media/vs-azure-tools-storage-explorer-files/image6.png)

5. Wybierz pozycję **Tak** w oknie dialogowym potwierdzenia.
    
    ![Okno dialogowe potwierdzenia](media/vs-azure-tools-storage-explorer-files/image7.png)

## <a name="copy-a-file-share"></a>Kopiowanie udziału plików

Program Storage Explorer (wersja zapoznawcza) umożliwia kopiowanie udziału pliku do schowka, a następnie wklejanie go do innego konta magazynu. Informacje na temat sposobu kopiowania pojedynczych plików zawiera sekcja [Managing files in a file share](https://docs.microsoft.com//azure/vs-azure-tools-storage-explorer-blobs#managing-blobs-in-a-blob-container) (Zarządzanie plikami w udziale plików).

Poniższe kroki ilustrują kopiowanie udziału plików z jednego konta magazynu do innego.

1. Otwórz Eksploratora usługi Storage (wersja zapoznawcza).

2. W okienku po lewej stronie rozwiń konto magazynu zawierające udział plików, który chcesz skopiować.

3. Rozwiń pozycję **Udziały plików** konta magazynu.

4. Kliknij prawym przyciskiem myszy udział plików, który chcesz skopiować, a następnie z menu kontekstowego wybierz pozycję **Kopiuj udział plików**.

    ![Kopiowanie udziału plików](media/vs-azure-tools-storage-explorer-files/image8.png)

5. Kliknij prawym przyciskiem myszy żądane „docelowe” konto magazynu, do którego chcesz wkleić udział plików, a następnie z menu kontekstowego wybierz pozycję **Wklej udział plików**.

    ![Wklejanie udziału plików](media/vs-azure-tools-storage-explorer-files/image9.png)

## <a name="get-the-sas-for-a-file-share"></a>Uzyskiwanie sygnatury dostępu współdzielonego dla udziału plików

[Sygnatura dostępu współdzielonego (SAS, shared access signature)](https://docs.microsoft.com//azure/storage/storage-dotnet-shared-access-signature-part-1) zapewnia delegowany dostęp do zasobów w ramach konta magazynu. Oznacza to, że możliwe jest przyznanie klientowi ograniczonych uprawnień do obiektów w ramach konta magazynu na określony czas i z określonym zestawem uprawnień bez konieczności udostępniania kluczy dostępu do konta.

Poniższe kroki ilustrują tworzenie sygnatury dostępu współdzielonego dla udziału plików:

1. Otwórz Eksploratora usługi Storage (wersja zapoznawcza).

2. W okienku po lewej stronie rozwiń konto magazynu zawierające udział plików, dla którego ma zostać uzyskana sygnatura dostępu współdzielonego.

3. Rozwiń pozycję **Udziały plików** konta magazynu.

4. Kliknij prawym przyciskiem myszy żądany udział plików, a następnie z menu kontekstowego wybierz pozycję **Uzyskaj sygnaturę dostępu współdzielonego**.

    ![Uzyskiwanie sygnatury dostępu współdzielonego](media/vs-azure-tools-storage-explorer-files/image10.png)

5. W oknie dialogowym **Sygnatura dostępu współdzielonego** określ zasady, daty rozpoczęcia i wygaśnięcia, strefę czasową oraz poziomy dostępu dla zasobu.

    ![Okno dialogowe sygnatury dostępu współdzielonego](media/vs-azure-tools-storage-explorer-files/image11.png)

6. Po zakończeniu określania opcji sygnatury dostępu współdzielonego wybierz pozycję **Utwórz**.

7. Zostanie wyświetlone drugie okno dialogowe **Sygnatura dostępu współdzielonego** zawierające listę udziałów plików wraz z adresami URL i ciągami zapytań umożliwiającymi dostęp do zasobu magazynu. Wybierz pozycję **Kopiuj** obok adres URL, który chcesz skopiować do schowka.
    
    ![Drugie okno dialogowe Sygnatura dostępu współdzielonego](media/vs-azure-tools-storage-explorer-files/image12.png)

8. Po zakończeniu wybierz pozycję **Zamknij**.

## <a name="manage-access-policies-for-a-file-share"></a>Zarządzanie zasadami dostępu dla udziału plików

Poniższe kroki ilustrują zarządzanie (dodawanie i usuwanie) zasadami dostępu dla udziału plików. Zasady dostępu są używane do tworzenia adresów URL sygnatur dostępu współdzielonego, za pomocą których użytkownicy mogą uzyskiwać dostęp do zasobów pliku magazynu przez zdefiniowany okres.

1. Otwórz Eksploratora usługi Storage (wersja zapoznawcza).

2. W okienku po lewej stronie rozwiń konto magazynu zawierające udział plików, którego zasadami dostępu chcesz zarządzać.

3. Rozwiń pozycję **Udziały plików** konta magazynu.

4. Wybierz żądany udział plików, a następnie z menu kontekstowego wybierz pozycję **Zarządzaj zasadami dostępu**.

    ![Menu kontekstowe Zarządzanie zasadami dostępu](media/vs-azure-tools-storage-explorer-files/image13.png)

5. W oknie dialogowym **Zasady dostępu** zostanie wyświetlona lista wszystkich zasad dostępu, które zostały już utworzone dla wybranego udziału plików.
    
    ![Zasady dostępu](media/vs-azure-tools-storage-explorer-files/image14.png)

6. Wykonaj następujące kroki w zależności od zadania zarządzania zasadami dostępu:
    
    - **Dodawanie nowych zasad dostępu** — wybierz pozycję **Dodaj**. Po wygenerowaniu w oknie dialogowym **Zasady dostępu** będą wyświetlane nowo dodane zasady dostępu (przy użyciu ustawień domyślnych).

    - **Edytowanie zasad dostępu** — wykonaj wszystkie żądane operacje edycji, a następnie wybierz pozycję **Zapisz**.

    - **Usuwanie zasad dostępu** — wybierz pozycję **Usuń** obok zasad dostępu, które chcesz usunąć.

7. Utwórz nowy adres URL sygnatury dostępu współdzielonego za pomocą utworzonych wcześniej zasad dostępu:
    
    ![Pobieranie sygnatury dostępu współdzielonego](media/vs-azure-tools-storage-explorer-files/image15.png)
    
    ![Nazwa i właściwości sygnatury dostępu współdzielonego](media/vs-azure-tools-storage-explorer-files/image16.png)

## <a name="managing-files-in-a-file-share"></a>Zarządzanie plikami w udziale plików

Po utworzeniu udziału plików można do niego przekazać plik, pobrać plik na komputer lokalny, otworzyć plik na komputerze lokalnym i wykonać wiele innych operacji.

Poniższe kroki ilustrują zarządzanie plikami (i folderami) w udziale plików.

1.  Otwórz Eksploratora usługi Storage (wersja zapoznawcza).

2.  W okienku po lewej stronie rozwiń konto magazynu zawierające udział plików, którym chcesz zarządzać.

3.  Rozwiń pozycję **Udziały plików** konta magazynu.

4.  Dwukrotnie kliknij udział plików, który chcesz wyświetlić.

5.  W okienku głównym zostanie wyświetlona zawartość udziału plików.

    ![Zawartość udziału](media/vs-azure-tools-storage-explorer-files/image17.png)

6.  W okienku głównym zostanie wyświetlona zawartość udziału plików.

7.  Wykonaj następujące kroki w zależności od zadania, które chcesz wykonać:

    - **Przekazywanie plików do udziału plików**

        a.  Na pasku narzędzi okienka głównego wybierz pozycję **Przekaż**, a następnie z menu rozwijanego wybierz pozycję **Przekaż pliki**.

        ![Przekazywanie plików](media/vs-azure-tools-storage-explorer-files/image18.png)
        
        b. W oknie dialogowym **Przekazywanie plików** wybierz przycisk wielokropka (**...**) po prawej stronie pola tekstowego **Pliki**, aby wybrać pliki do przekazania.

        ![Dodawanie plików](media/vs-azure-tools-storage-explorer-files/image19.png)

        c. Wybierz pozycję **Przekaż**.

    - **Przekazywanie folderu do udziału plików**
        
        a. Na pasku narzędzi okienka głównego wybierz pozycję **Przekaż**, a następnie z menu rozwijanego wybierz pozycję **Przekaż folder**.

        ![Menu Przekaż folder](media/vs-azure-tools-storage-explorer-files/image20.png)

        b. W oknie dialogowym **Przekazywanie folderu** wybierz przycisk wielokropka (**...**) po prawej stronie pola tekstowego **Folder**, aby wybrać folder, którego zawartość chcesz przekazać.

        c. Opcjonalnie określ folder docelowy, do którego zawartość wybranego folderu zostanie przekazana. Jeśli folder docelowy nie istnieje, zostanie on utworzony.

        d. Wybierz pozycję **Przekaż**.

    - **Pobieranie pliku na komputer lokalny**
        
        a. Wybierz plik, który chcesz pobrać.
        
        b. Na pasku narzędzi okienka głównego wybierz pozycję **Pobierz**.
        
        c. W oknie dialogowym **Określanie lokalizacji, w której zapisać pobrany plik** określ lokalizację, w której ma zostać zapisany pobrany plik, oraz nazwę tego pliku.

        d. Wybierz pozycję **Zapisz**.

    - **Otwieranie pliku na komputerze lokalnym**
        
        a.  Wybierz plik, który chcesz otworzyć.
        
        b.  Na pasku narzędzi okienka głównego wybierz pozycję **Otwórz**.
        
        c.  Plik zostanie pobrany i otwarty przy użyciu aplikacji skojarzonej z typem pliku źródłowego.

    - **Kopiowanie pliku do Schowka**

        a. Wybierz plik, który chcesz skopiować.

        b. Na pasku narzędzi okienka głównego wybierz pozycję **Kopiuj**.

        c. W lewym okienku przejdź do innego udziału plików i kliknij go dwukrotnie, aby wyświetlić go w okienku głównym.

        d. Na pasku narzędzi okienka głównego wybierz pozycję **Wklej**, aby utworzyć kopię pliku.

    - **Usuwanie pliku**

        a. Wybierz plik, który chcesz usunąć.

        b. Na pasku narzędzi okienka głównego wybierz pozycję **Usuń**.

        c. Wybierz pozycję **Tak** w oknie dialogowym potwierdzenia.

## <a name="next-steps"></a>Następne kroki

- Zobacz [najnowsze informacje o wersji i filmy wideo dotyczące programu Storage Explorer (wersja zapoznawcza)](http://www.storageexplorer.com/).

- Dowiedz się, jak [tworzyć aplikacje przy użyciu obiektów Blob, tabel, kolejek i plików platformy Azure](https://azure.microsoft.com/documentation/services/storage/).
