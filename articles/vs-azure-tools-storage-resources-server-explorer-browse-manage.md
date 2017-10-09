---
title: "aaaBrowsing i zarządzanie zasobami magazynu za pomocą Eksploratora serwera | Dokumentacja firmy Microsoft"
description: "Przeglądanie i zarządzanie zasobami magazynu za pomocą Eksploratora serwera"
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 658dc064-4a4e-414b-ae5a-a977a34c930d
ms.service: storage
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 8/24/2017
ms.author: kraigb
ms.openlocfilehash: f5b456b812f2ad8103c50538d532a57397bcccbb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="browsing-and-managing-storage-resources-with-server-explorer"></a>Przeglądanie i zarządzanie zasobami magazynu za pomocą Eksploratora serwera
[!INCLUDE [storage-try-azure-tools](../includes/storage-try-azure-tools.md)]

## <a name="overview"></a>Omówienie
Jeśli po zainstalowaniu hello Azure Tools dla programu Microsoft Visual Studio można wyświetlić obiektów blob, kolejki i danych z tabeli z kont magazynu dla platformy Azure. węzeł magazyn Azure Hello w Eksploratorze serwera zawiera dane konta emulatora magazynu lokalnego i innymi kontami magazynu Azure.

Wybierz tooview Eksploratora serwera w programie Visual Studio na pasku menu hello **widoku**, **Eksploratora serwera**. węzeł magazynu Hello są wyświetlane wszystkie hello kont magazynu, które istnieją w ramach każdej subskrypcji/certyfikatu Azure podłączenia do. Jeśli nie ma konta magazynu, można dodać go, wykonując instrukcje hello [dalszej części tego tematu](#add-storage-accounts-by-using-server-explorer).

Od wersji 2.7 zestawu SDK platformy Azure, możesz również użyć nowego tooview Eksplorator chmury hello i zarządzania zasobami platformy Azure. Zobacz [zarządzania zasobami Azure za pomocą Eksploratora chmury](vs-azure-tools-resources-managing-with-cloud-explorer.md) Aby uzyskać więcej informacji.

## <a name="view-and-manage-storage-resources-in-visual-studio"></a>Wyświetlanie i zarządzanie zasobami magazynu w programie Visual Studio
W Eksploratorze serwera automatycznie pokazuje listę tabel, kolejek i obiektów blob na koncie emulatora magazynu. Konto emulatora magazynu Hello znajduje się w Eksploratorze serwera w węźle magazyn hello jako hello **programowanie** węzła.

zasoby toosee hello emulatora konta magazynu, rozwiń węzeł hello **programowanie** węzła. Jeśli emulator magazynu hello nie została uruchomiona po rozwinięciu hello **programowanie** węzła, zostanie ona automatycznie rozpoczęta. Może to zająć kilka sekund. Podczas uruchamiania hello emulatora magazynu, możesz kontynuować toowork w innych obszarach programu Visual Studio.

tooview zasobów na koncie magazynu, rozwiń węzeł konta magazynu hello w Eksploratorze serwera. wyświetlane są następujące węzły podrzędne Hello:

* Obiekty blob
* Kolejki
* Tabele

## <a name="work-with-blob-resources"></a>Praca z zasobami obiektów Blob
węzeł obiekty BLOB Hello zostanie wyświetlona lista kontenery hello wybrane konto magazynu. Kontenerów obiektów blob zawierają pliki obiektu blob, a te obiekty BLOB można organizować w folderach i podfolderach. Zobacz [jak toouse magazynu obiektów Blob z .NET](storage/blobs/storage-dotnet-how-to-use-blobs.md) Aby uzyskać więcej informacji.

### <a name="toocreate-a-blob-container"></a>toocreate kontenera obiektów blob
1. Hello Otwórz menu skrótów hello **obiekty BLOB** węzeł, a następnie wybierz pozycję **Tworzenie kontenera obiektów Blob**.
2. W hello **Tworzenie kontenera obiektów Blob** okna dialogowego wprowadź nazwę hello hello nowego kontenera.  
3. Naciśnij klawisz **ENTER** na klawiaturze lub można kliknij lub naciśnij polecenie poza kontenera obiektów blob hello toosave hello nazwę pola.
   
   > [!NOTE]
   > Nazwa kontenera obiektów blob Hello musi rozpoczynać się od liczby (0 – 9) lub małą literę (a-z).
   > 
   > 

### <a name="toodelete-a-blob-container"></a>toodelete kontenera obiektów blob
* Menu skrótów Otwórz hello hello kontenera obiektów blob mają tooremove, a następnie wybierz pozycję **usunąć**.

### <a name="toodisplay-a-list-of-hello-items-contained-in-a-blob-container"></a>toodisplay listy hello elementów zawartych w kontenerze obiektów blob
* Otwórz menu skrótów hello nazwa kontenera obiektów blob hello na liście, a następnie wybierz pozycję **Otwórz**.
  
    Podczas wyświetlania zawartości hello kontenera obiektów blob, zostanie wyświetlony na karcie znany jako widok kontenera obiektów blob hello.
  
    ![VST_SE_BlobDesigner](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC749016.png)
  
    Można wykonywać następujące operacje na obiektach blob za pomocą przycisków hello w hello prawym górnym rogu widoku kontenera obiektów blob hello hello:
  
  * Wprowadź wartość filtru i zastosować je
  * Odśwież listę hello obiektów blob w kontenerze hello
  * Przekazywanie pliku
  * Usuwanie obiektu blob
    
    > [!NOTE]
    > Usunięcie pliku z kontenera obiektów blob nie powoduje usunięcia hello pliku źródłowego. powoduje tylko usunięcie go z hello kontenera obiektów blob.
    > 
    > 
  * Otwórz obiektu blob
  * Zapisz na komputerze lokalnym toohello obiektów blob

### <a name="toocreate-a-folder-or-subfolder-in-a-blob-container"></a>toocreate folder lub podfolder w kontenerze obiektów blob
1. Wybierz kontener obiektów blob hello w Eksploratorze chmury. W oknie kontenera hello, wybierz hello **przekazania obiektu Blob** przycisku.
   
    ![Przekazywanie pliku do folderu obiektów blob](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC766037.png)
2. W hello **Przekaż nowy plik** oknie dialogowym Wybierz hello **Przeglądaj** przycisk toospecify hello plików mają tooupload, a następnie wprowadź nazwę folderu w hello **Folder (opcjonalnie)** pole .
   
    Możesz dodać podfoldery w folderach kontenera, wykonując hello same procedury. Jeśli nie określisz nazwy folderu hello plik zostanie przekazany toohello najwyższego poziomu hello kontenera obiektów blob. Plik Hello pojawia się w określonym folderze hello w kontenerze hello.
   
    ![Folder dodany tooa kontenera obiektów blob](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC766038.png)
3. Kliknij dwukrotnie hello folder, lub naciśnij klawisz ENTER toosee hello zawartość folderu hello. Podczas pracy w folderze hello kontenera, można przejść wstecz toohello głównego hello kontenera, wybierając hello **Otwórz katalog nadrzędny** (Strzałka w górę) przycisku.

### <a name="toodelete-a-container-folder"></a>toodelete folderu kontenera
* Usuń wszystkie pliki hello w folderze hello
  
  > [!NOTE]
  > Ponieważ foldery w kontenerów obiektów blob to foldery wirtualne, nie można utworzyć pusty folder ani nie można usunąć toodelete folderu jego zawartość pliku. Masz toodelete hello całą zawartość hello toodelete folderu.
  > 
  > 

### <a name="toofilter-blobs-in-a-container"></a>obiekty BLOB toofilter w kontenerze
Można filtrować obiektów blob hello, które są wyświetlane, określając Wspólny prefiks.

Na przykład, jeśli wprowadzony prefiks hello `hello` w polu tekstowym filtru Witaj, a następnie wybierz pozycję hello **Execute** (**!**) przycisk, są wyświetlane tylko obiekty BLOB, które zaczynają się od "hello".

![VST_SE_FilterBlobs](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC519076.png)

> [!NOTE]
> pole filtru Hello jest rozróżniana wielkość liter i nie obsługuje filtrowania z symbolami wieloznacznymi. Obiekty BLOB można filtrować tylko według prefiksu. Prefiks Hello może zawierać ogranicznika, jeśli używasz blob tooorganize ogranicznik w hierarchii wirtualnego. Na przykład filtrowanie hello prefiks HelloFabric / zwraca wszystkie obiekty BLOB, począwszy od tego ciągu.
> 
> 

### <a name="toodownload-blob-data"></a>toodownload danych obiektów blob
* W **Eksplorator chmury**, otwórz menu skrótów powitania dla co najmniej jednego obiektu blob, a następnie wybierz pozycję **Otwórz**, lub wybierz hello nazwa obiektu blob, a następnie wybierz hello **Otwórz** , lub kliknij dwukrotnie Nazwa obiektu blob Hello.
  
    postęp Hello pobieranie obiektu blob jest wyświetlana w hello **dziennika aktywności platformy Azure** okna.
  
    Otwiera Hello obiektów blob w hello domyślny edytor dla tego typu pliku. Jeśli system operacyjny hello rozpoznaje typ pliku hello, hello zostanie otwarty w aplikacji zainstalowanej lokalnie; w przeciwnym razie zostanie wyświetlony monit toochoose aplikacji, która jest odpowiednia dla typu pliku hello hello obiektu blob. Plik lokalne powitania, który jest tworzony podczas pobierania obiektu blob jest oznaczony jako tylko do odczytu.
  
    Dane obiektu blob jest buforowane lokalnie i porównywany hello obiektu blob godzina ostatniej modyfikacji w hello usługi Blob. Jeśli obiekt blob hello został zaktualizowany od czasu ostatniego pobrania, zostanie pobrane ponownie; w przeciwnym razie hello blob zostaną załadowane z hello dysku lokalnym. Domyślnie obiektu blob jest tooa pobranego katalogu tymczasowego. toodownload obiekty BLOB tooa określonego katalogu, hello Otwórz menu skrótów hello wybrane nazwy obiektu blob i wybierz polecenie **Zapisz jako**. Po zapisaniu obiektu blob w ten sposób hello pliku obiektu blob nie jest otwarty i hello lokalnego pliku jest tworzony z atrybutami odczytu i zapisu.

### <a name="tooupload-blobs"></a>obiekty BLOB tooupload
* Wybierz hello **przekazania obiektu Blob** przycisku, gdy kontener hello jest otwarty w celu wyświetlenia w widoku kontenera obiektów blob hello.
  
    Możesz wybrać jedną lub więcej plików tooupload i przekazać plików dowolnego typu. Witaj **dziennika aktywności platformy Azure** pokazuje hello postęp hello przekazywania. Aby uzyskać więcej informacji o tym, jak toowork za pomocą danych obiektów blob, zobacz [jak toouse hello usługi magazynu obiektów Blob Azure w programie .NET](http://go.microsoft.com/fwlink/p/?LinkId=267911).

### <a name="tooview-logs-transferred-tooblobs"></a>tooview dzienniki transferu tooblobs
* Jeśli używasz diagnostyki Azure toolog danych z aplikacji platformy Azure i konto magazynu tooyour Dzienniki zostały przeniesione, zobaczysz kontenerów, które zostały utworzone przez usługę Azure dla tych dzienników. Wyświetlanie dzienników w Eksploratorze serwera jest łatwy sposób problemy tooidentify z aplikacją, zwłaszcza, jeśli został wdrożony tooAzure. Aby uzyskać więcej informacji na temat diagnostyki Azure, zobacz [zbierania danych rejestrowania za pomocą diagnostyki Azure](https://msdn.microsoft.com/library/azure/gg433048.aspx).

### <a name="tooget-hello-url-for-a-blob"></a>adres URL hello tooget dla obiektu blob
* Otwórz menu skrótów hello blob, a następnie wybierz pozycję **URL kopii**.

### <a name="tooedit-a-blob"></a>tooedit obiektu blob
* Wybierz hello obiektów blob, a następnie wybierz pozycję hello **Otwórz Blob** przycisku.
  
    Plik Hello jest pobrany tooa tymczasowej lokalizacji i otworzyć hello komputera lokalnego. Należy ponownie przekazać hello blob po wprowadzeniu zmian.

## <a name="work-with-queue-resources"></a>Praca z kolejki zasobów
Magazyn kolejek usługi znajdują się w koncie magazynu platformy Azure i można ich używać tooallow Twojego chmury usługi ról toocommunicate ze sobą oraz z innymi usługami przez mechanizm przekazywania komunikat. Dostępne kolejki hello programowo za pośrednictwem usługi w chmurze, jak i za pośrednictwem usługi sieci web dla klientów zewnętrznych. Kolejki hello można także przejść bezpośrednio, za pomocą Eksploratora serwera w programie Visual Studio.

Podczas opracowywania usługi w chmurze, która używa kolejek może mają toouse Visual Studio toocreate kolejek i pracować z nimi interaktywnie podczas tworzenia i testowania kodu.

W Eksploratorze serwera można wyświetlać kolejki hello na koncie magazynu, tworzenie i usuwanie kolejek, otwórz tooview kolejki jego wiadomości i Dodaj kolejka tooa wiadomości. Podczas otwierania kolejki w celu wyświetlenia można wyświetlić poszczególne wiadomości powitania i mogą wykonywać następujące akcje w kolejce hello za pomocą przycisków hello w hello lewego górnego narożnika hello:

* Odśwież widok hello hello kolejki
* Dodaj toohello kolejki komunikatów
* Usuwania z kolejki znajdujące się najwyżej wiadomość hello
* Wyczyść hello całego kolejki

powitania po obraz pokazuje kolejki, która zawiera dwa komunikaty.

![Wyświetlanie kolejki](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC651470.png)

Aby uzyskać więcej informacji na temat magazynu usług kolejek, zobacz [porady: użycie hello kolejki magazynu usługi](http://go.microsoft.com/fwlink/?LinkID=264702). Informacji o usłudze sieci web hello magazynu usług kolejek, zobacz [pojęcia dotyczące usługi kolejki](http://go.microsoft.com/fwlink/?LinkId=264788). Aby dowiedzieć się jak toosend wiadomości tooa magazynu usługi kolejki przy użyciu programu Visual Studio, zobacz [tooa wysyłania wiadomości kolejki usług magazynu](https://msdn.microsoft.com/library/azure/jj649344.aspx).

> [!NOTE]
> Magazyn kolejek usługi różni się od kolejek usługi service bus. Aby uzyskać więcej informacji na temat kolejek usługi service bus Zobacz kolejek usługi Service Bus, tematy i subskrypcje.
> 
> 

## <a name="work-with-table-resources"></a>Praca z tabeli zasobów
Usługa Azure Table storage Hello przechowywania dużych ilości danych strukturalnych. Usługa Hello jest magazynem danych NoSQL, który przyjmuje uwierzytelnione wywołania z wewnątrz lub na zewnątrz hello chmury Azure. Tabele Azure idealnie nadają się do przechowywania strukturalnych danych nierelacyjnych.

### <a name="toocreate-a-table"></a>toocreate tabeli
1. W Eksploratorze chmury, wybierz hello **tabel** węzła magazynu hello konta, a następnie wybierz pozycję **Create Table**.
2. W hello **Create Table** okna dialogowego wprowadź nazwę tabeli hello.

### <a name="tooview-table-data"></a>dane tabeli tooview
1. W Eksploratorze chmury Otwórz hello **Azure** węzeł, a następnie otwórz hello **magazynu** węzła.
2. Otwórz hello węzeł konta magazynu interesuje, a następnie otwórz hello **tabel** toosee węzła listy tabel dla konta magazynu hello.
3. Otwórz menu skrótów powitania dla tabeli, a następnie wybierz pozycję **widok tabeli**.
   
    ![Tabeli platformy Azure, w Eksploratorze rozwiązań](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC744165.png)

Tabela Hello jest zorganizowana według jednostek (wyświetlane w wierszach) i właściwości (wyświetlane kolumny). Na przykład hello następującej ilustracji przedstawiono jednostek na liście hello **projektanta tabel**:

### <a name="tooedit-table-data"></a>dane tabeli tooedit
1. W hello **projektanta tabel**, otwórz menu skrótów hello jednostki (pojedynczy wiersz) lub właściwości (jedną komórkę), a następnie wybierz pozycję **Edytuj**.
   
    ![Dodaj lub Edytuj jednostkę tabeli](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC656238.png)
   
    Jednostki w jednej tabeli nie są wymagane toohave hello sam zestaw właściwości (kolumny). Utrzymaj hello uwadze następujące ograniczenia na wyświetlanie i edytowanie danych tabeli.
   
   * Nie można wyświetlić lub edytować dane binarne (byte[]) typu, ale można ją zapisać w tabeli.
   * Nie można edytować hello **PartitionKey** lub **RowKey** wartości, ponieważ Magazyn tabel na platformie Azure nie obsługuje tej operacji.
   * Nie można utworzyć właściwość o nazwie sygnatury czasowej, usługi magazynu Azure używają właściwość o tej nazwie.
   * Jeśli wprowadzisz wartość daty i godziny, należy wykonać formacie, który jest odpowiedni toohello ustawienia regionalne i językowe na komputerze (na przykład MM/DD/RRRR GG [AM | PM] dla Stanów Zjednoczonych W języku angielskim).

### <a name="tooadd-entities"></a>tooadd jednostek
1. W hello **projektanta tabel**, wybierz hello **Dodaj jednostki** przycisku.
   
    ![Dodawanie jednostki](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC655336.png)
2. W hello **Dodaj jednostki** okna dialogowego wprowadź wartości hello hello **PartitionKey** i **RowKey** właściwości.
   
    ![Dodaj jednostki — okno dialogowe](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC655335.png)
   
    Wprowadź wartości hello ostrożnie, ponieważ nie można ich zmienić po zamknięciu hello — okno dialogowe, chyba że w przypadku usunięcia jednostki hello i dodaj go ponownie.

### <a name="toofilter-entities"></a>toofilter jednostek
Można dostosować hello zestaw jednostek, które są wyświetlane w tabeli, jeśli używasz hello konstruktora zapytań.

1. Konstruktor kwerend hello tooopen, otwórz tabelę do wyświetlenia.
2. Przycisk hello konstruktora zapytań w widoku tabeli hello paska narzędzi.
   
    Witaj **konstruktora zapytań** zostanie wyświetlone okno dialogowe. Witaj Poniższa ilustracja przedstawia kwerendę, która jest tworzona w hello konstruktora zapytań.
   
    ![Konstruktor kwerend](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC652231.png)
3. Po zakończeniu tworzenia zapytania hello, zamknij okno dialogowe hello. tekst Hello formularzu hello zapytania zostanie wyświetlony w polu tekstowym jako filtr usługi danych WCF.
4. Witaj toorun kwerendy, wybierz ikonę zielonym trójkątem hello.
   
    Można także filtrować dane jednostki, która jest wyświetlana w hello **projektanta tabel** Jeśli wprowadź ciąg filtru usługi danych WCF bezpośrednio w polu filtru hello. Tego rodzaju ciągu jest podobne tooa klauzuli SQL WHERE, ale są przesyłane toohello serwera w żądaniu HTTP. Informacje, jak tooconstruct filtru ciągów, zobacz [konstruowania filtru ciągów hello projektanta tabel](https://msdn.microsoft.com/library/azure/ff683669.aspx).
   
    Witaj poniższej ilustracji przedstawiono przykład ciągu prawidłowym filtrem:
   
    ![VST_SE_TableFilter](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC655337.png)

### <a name="refresh-storage-data"></a>Odświeżanie magazynu danych
Gdy Eksploratora serwera łączy tooor pobiera dane z konta magazynu, może potrwać minutę tooa toocomplete operacji hello. Jeśli nie można się połączyć, operacja hello może upłynął limit czasu. Gdy dane są pobierane, możesz kontynuować toowork w innych częściach programu Visual Studio. toocancel hello operacja trwa zbyt długo, wybierz hello **Zatrzymaj odświeżanie** przycisk na powitania narzędzi Eksploratora serwera.

#### <a name="toorefresh-blob-container-data"></a>dane w kontenerze obiektów blob toorefresh
* Wybierz hello **obiekty BLOB** węźle poniżej **magazynu** i wybierz polecenie hello **Odśwież** przycisk na powitania narzędzi Eksploratora serwera.
* listy hello toorefresh obiektów blob, który jest wyświetlany, wybierz hello **Execute** przycisku.

#### <a name="toorefresh-table-data"></a>dane tabeli toorefresh
* Wybierz hello **tabel** węźle poniżej **magazynu** i wybierz polecenie hello **Odśwież** przycisku.
* listy hello toorefresh jednostek wyświetlanych w hello **projektanta tabel**, wybierz hello **Execute** przycisk na powitania **projektanta tabel**.

#### <a name="toorefresh-queue-data"></a>toorefresh kolejki danych
* Wybierz hello **kolejek** węzła, a następnie wybierz pozycję hello **Odśwież** przycisku.

#### <a name="toorefresh-all-items-in-a-storage-account"></a>toorefresh wszystkie elementy na koncie magazynu
* Wybierz nazwę konta hello, a następnie wybierz hello **Odśwież** przycisk na powitania narzędzi Eksploratora serwera.

### <a name="add-storage-accounts-by-using-server-explorer"></a>Dodawanie konta magazynu za pomocą Eksploratora serwera
Istnieją dwa sposoby tooadd kont magazynu za pomocą Eksploratora serwera. Można utworzyć nowe konto magazynu w ramach subskrypcji platformy Azure, lub można dołączyć istniejącego konta magazynu.

#### <a name="toocreate-a-new-storage-account-by-using-server-explorer"></a>toocreate nowe konto magazynu przy użyciu Eksploratora serwera
1. W Eksploratorze serwera Otwórz menu skrótów hello hello węzła magazynu, a następnie wybierz Utwórz konto magazynu.
   
    ![Utwórz nowe konto magazynu Azure](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC744166.png)
2. Wybierz lub wprowadź następujące informacje dotyczące hello nowe konto magazynu w hello hello **Utwórz konto magazynu** okno dialogowe.
   
   * Witaj ma konto magazynu hello tooadd toowhich subskrypcji platformy Azure.
   * Nazwa Hello ma toouse hello nowe konto magazynu.
   * Witaj region lub grupę koligacji, (na przykład zachodnie stany USA lub Azja Wschodnia).
   * Witaj typ replikacji ma toouse dla konta magazynu hello, takich jak geograficznie nadmiarowy.
3. Wybierz pozycję **Utwórz**.
   
    Witaj nowe konto magazynu jest wyświetlana w hello **magazynu** listy w Eksploratorze rozwiązań.

#### <a name="tooattach-an-existing-storage-account-by-using-server-explorer"></a>tooattach istniejącego konta magazynu za pomocą Eksploratora serwera
1. W Eksploratorze serwera Otwórz menu skrótów hello hello węzła magazynu Azure, a następnie wybierz **Dołącz zewnętrzną usługę Storage**.
   
    ![Dodawanie istniejącego konta magazynu](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC766039.png)
2. Wybierz lub wprowadź następujące informacje dotyczące hello nowe konto magazynu w hello hello **Utwórz konto magazynu** okno dialogowe.
   
   * Nazwa Hello hello istniejące konto magazynu, które chcesz tooattach. Można wprowadzić nazwę lub wybierz ją z listy hello.
   * klucz Hello hello wybranego konta magazynu. Ta wartość jest zazwyczaj dostarczany po wybraniu konta magazynu. Klucz konta magazynu hello tooremember programu Visual Studio, zaznacz pole klucza hello Zapamiętaj konta.
   * Witaj protokołu toouse tooconnect toohello konta magazynu, takich jak HTTP, HTTPS lub niestandardowe punktu końcowego. Zobacz [jak parametry połączenia z tooConfigure](https://msdn.microsoft.com/library/azure/ee758697.aspx) uzyskać więcej informacji o niestandardowe punkty końcowe.

### <a name="tooview-hello-secondary-endpoints"></a>dodatkowej punkty końcowe tooview hello
* Jeśli utworzono konto magazynu przy użyciu hello **dostęp do odczytu z magazynu geograficznie nadmiarowego** opcji replikacji można wyświetlić jego dodatkowej punkty końcowe. Otwórz menu skrótów hello hello nazwy konta, a następnie wybierz pozycję **właściwości**.
  
    ![Punkty końcowe dodatkowej pamięci masowej](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC766040.png)

### <a name="tooremove-a-storage-account-from-server-explorer"></a>tooremove konto magazynu z poziomu Eksploratora serwera
* W Eksploratorze serwera Otwórz menu skrótów hello hello nazwy konta, a następnie wybierz **usunąć**. Usunięcie konta magazynu, zostaną również usunięte wszystkie zapisane informacje klucza dla tego konta.
  
  > [!NOTE]
  > Jeśli usuniesz konto magazynu z poziomu Eksploratora serwera nie wpływa na koncie magazynu lub dane, które zawiera; po prostu usuwa odwołanie hello z Eksploratora serwera. toopermanently usuwania konta magazynu, należy użyć hello [klasycznego portalu Azure](http://go.microsoft.com/fwlink/?LinkID=213885).
  > 
  > 

## <a name="next-steps"></a>Następne kroki
toolearn więcej na temat korzystania z usług magazynu Azure, zobacz [dostęp do usług magazynu Azure hello](https://msdn.microsoft.com/library/azure/ee405490.aspx).

