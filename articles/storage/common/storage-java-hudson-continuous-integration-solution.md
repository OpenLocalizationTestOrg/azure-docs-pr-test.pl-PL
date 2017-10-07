---
title: "aaaHow toouse Hudson z magazynem obiektów Blob | Dokumentacja firmy Microsoft"
description: "Opisuje sposób toouse Hudson z magazynu obiektów Blob platformy Azure jako repozytorium artefaktów kompilacji."
services: storage
documentationcenter: java
author: seguler
manager: jahogg
editor: tysonn
ms.assetid: 119becdd-72c4-4ade-a439-070233c1e1ac
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 02/28/2017
ms.author: seguler
ms.openlocfilehash: 196b5d014b0318c5972a052f7822b568cfcc23df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-storage-with-a-hudson-continuous-integration-solution"></a>Korzystanie z usługi Azure Storage z rozwiązaniem ciągłej integracji Hudson
## <a name="overview"></a>Omówienie
Witaj następujące informacje pokazuje, jak toouse magazynu obiektów Blob jako repozytorium artefaktów kompilacji utworzone przez rozwiązanie Hudson ciągłej integracji (CI) lub jako źródło do pobrania plików toobe używane w procesie kompilacji. Jest jednego ze scenariuszy hello, w którym użytkownik może to być przydatne, gdy jest kodowania w środowisku elastyczne programowanie (przy użyciu języka Java lub innych języków), kompilacje działają na podstawie ciągłej integracji i potrzebujesz repozytorium artefaktów z kompilacji, tak, aby było to możliwe , na przykład udostępniać je z innymi elementami członkowskimi organizacji klienta, lub Obsługa archiwum.  Inny scenariusz jest, gdy sam zadania kompilacji wymaga innych plików, na przykład zależności toodownload jako część hello Konstruuj wprowadzania.

W tym samouczku używana będzie hello Azure Storage wtyczki dla Hudson CI udostępnione przez firmę Microsoft.

## <a name="introduction-toohudson"></a>Wprowadzenie tooHudson
Umożliwia Hudson ciągłej integracji projektu oprogramowania przez deweloperów tooeasily zintegrować ich zmiany kodu i mieć kompilacje utworzonych automatycznie i często, zwiększając wydajność hello hello deweloperów. Kompilacje są określonej wersji, a artefaktów kompilacji może być przekazane toovarious repozytoriów. W tym artykule opisano sposób toouse magazynu obiektów Blob platformy Azure jako repozytorium hello hello kompilacji artefaktów. Przedstawiono w nim również sposób toodownload zależności z magazynu obiektów Blob platformy Azure.

Więcej informacji na temat Hudson można znaleźć w folderze [spełnia Hudson](http://wiki.eclipse.org/Hudson-ci/Meet_Hudson).

## <a name="benefits-of-using-hello-blob-service"></a>Zalety używania usługi Blob hello
Przy użyciu hello obiektu Blob usługi toohost Twojego artefaktów kompilacji elastyczne programowanie zalety:

* Wysoka dostępność artefaktów kompilacji i/lub zależności do pobrania.
* Wydajność rozwiązania Hudson CI przekazuje użytkownika artefaktów kompilacji.
* Wydajność, gdy klienci i partnerzy pobrać artefaktów z kompilacji.
* Kontrolę nad zasad dostępu, wybór między anonimowego dostępu, dostęp sygnatury dostępu współdzielonego opartych na wygaśnięcia, prywatne, dostępu itd.

## <a name="prerequisites"></a>Wymagania wstępne
Można będzie konieczne hello następujących toouse hello usługi obiektów Blob wraz z rozwiązaniem Hudson CI:

* Rozwiązanie Hudson ciągłej integracji.
  
    Jeśli obecnie nie ma rozwiązania Hudson CI, możesz uruchomić rozwiązania Hudson CI przy użyciu hello następujące techniki:
  
  1. Na komputerze z obsługą języka Java pobierania hello WAR Hudson z <http://hudson-ci.org/>.
  2. W wierszu polecenia, który jest otwarty toohello folderu, który zawiera hello Hudson WAR Uruchom hello Hudson WAR. Na przykład, jeśli pobrano wersji 3.1.2:
     
      `java -jar hudson-3.1.2.war`

  3. W przeglądarce otwórz `http://localhost:8080/`. Spowoduje to otwarcie hello Hudson pulpitu nawigacyjnego.
  4. Przy pierwszym użyciu Hudson, ukończenie początkowej konfiguracji hello na `http://localhost:8080/`.
  5. Po zakończeniu początkowej konfiguracji hello anulować hello uruchomione wystąpienie hello Hudson WAR, uruchom ponownie hello Hudson WAR i otwórz ponownie hello Hudson pulpitu nawigacyjnego, `http://localhost:8080/`, które będzie używane tooinstall i skonfigurować hello wtyczki usługi Azure Storage.
     
      Podczas gdy typowe rozwiązania Hudson elementu konfiguracji należy skonfigurować toorun jako usługa, systemem hello Hudson war w wierszu polecenia hello będą wystarczające do celów tego samouczka.
* Konto platformy Azure. Można założyć konto platformy Azure w usłudze <http://www.azure.com>.
* Konto usługi Azure Storage. Jeśli nie masz już konto magazynu, możesz utworzyć jedną przy użyciu kroków hello na [Utwórz konto magazynu](../common/storage-create-storage-account.md#create-a-storage-account).
* Zaleca się, ale nie wymaga znajomości hello Hudson CI rozwiązania, jak hello następującą zawartość będzie używać tooshow prosty przykład Witaj kroki niezbędne w przypadku używania usługi Blob hello jako repozytorium dla Hudson CI tworzenie artefaktów.

## <a name="how-toouse-hello-blob-service-with-hudson-ci"></a>Jak toouse hello usługa Blob z Hudson elementu konfiguracji
Usługa Blob hello toouse z Hudson, będziesz potrzebować tooinstall hello wtyczki usługi Azure Storage, skonfiguruj toouse wtyczki hello konta magazynu, a następnie utworzyć akcję po kompilacji, która przekazuje konta magazynu tooyour artefaktów kompilacji. Te kroki opisano w hello następujące sekcje.

## <a name="how-tooinstall-hello-azure-storage-plugin"></a>Jak tooinstall hello wtyczki usługi Azure Storage
1. W ramach hello Hudson pulpitu nawigacyjnego, kliknij przycisk **Zarządzanie Hudson**.
2. Na powitania **Zarządzanie Hudson** kliknij przycisk **Zarządzanie wtyczkami**.
3. Kliknij przycisk hello **dostępne** kartę.
4. Kliknij przycisk **innych**.
5. W hello **Uploaders artefaktu** zaznacz **dodatek Microsoft Azure Storage**.
6. Kliknij pozycję **Zainstaluj**.
7. Po zakończeniu instalacji hello, uruchom ponownie Hudson.

## <a name="how-tooconfigure-hello-azure-storage-plugin-toouse-your-storage-account"></a>Jak tooconfigure hello toouse wtyczki usługi Azure Storage konta magazynu
1. W ramach hello Hudson pulpitu nawigacyjnego, kliknij przycisk **Zarządzanie Hudson**.
2. Na powitania **Zarządzanie Hudson** kliknij przycisk **skonfigurować System**.
3. W hello **konfiguracji konta magazynu Azure Microsoft** sekcji:
   
    a. Wprowadź nazwę konta magazynu, który można uzyskać z hello [Azure Portal](https://portal.azure.com).
   
    b. Wprowadź klucz konta magazynu również u: hello [Azure Portal](https://portal.azure.com).
   
    c. Użyj wartości domyślnej powitania dla **adres URL punktu końcowego usługi Blob** korzystania z chmury publicznej Azure hello. Jeśli używasz innej chmurze platformy Azure, użyj punktu końcowego hello jako hello określony w [Azure Portal](https://portal.azure.com) dla konta magazynu.
   
    d. Kliknij przycisk **sprawdzanie poprawności poświadczeń magazynu** toovalidate Twojego konta magazynu.
   
    e. [Opcjonalnie] Jeśli masz dodatkowe konta magazynu, które mają dokonano tooyour dostępne Hudson CI, kliknij przycisk **dodać więcej kont magazynu**.
   
    f. Kliknij przycisk **zapisać** toosave ustawień.

## <a name="how-toocreate-a-post-build-action-that-uploads-your-build-artifacts-tooyour-storage-account"></a>Jak toocreate akcję po kompilacji, która przekazuje konta magazynu tooyour artefaktów kompilacji
Do celów instrukcji najpierw potrzebujemy toocreate zadanie, które będzie utworzyć kilka plików, a następnie dodaj na koncie magazynu tooyour hello działania mające miejsce po kompilacji tooupload hello plików.

1. W ramach hello Hudson pulpitu nawigacyjnego, kliknij przycisk **nowe zadanie**.
2. Zadania hello nazwa **MyJob**, kliknij przycisk **kompilacji zadanie oprogramowania wolne stylu**, a następnie kliknij przycisk **OK**.
3. W hello **kompilacji** sekcji hello zadania konfiguracji, kliknij przycisk **kroku kompilacji Dodaj** i wybierz polecenie **wykonywanie wsadowe systemu Windows polecenie**.
4. W **polecenia**, użyj następującego polecenia hello:

    ```   
        md text
        cd text
        echo Hello Azure Storage from Hudson > hello.txt
        date /t > date.txt
        time /t >> date.txt
    ```

5. W hello **akcje postkompilacyjnego** sekcji hello zadania konfiguracji, kliknij przycisk **przekazać magazynu obiektów Blob Azure tooMicrosoft artefakty**.
6. Aby uzyskać **nazwy konta magazynu**, wybierz hello toouse konta magazynu.
7. Aby uzyskać **nazwa kontenera**, określ nazwę kontenera hello. (kontener hello zostanie utworzony, jeśli go jeszcze nie istnieje po przekazaniu są hello artefaktów kompilacji.) Można używać zmiennych środowiskowych, dlatego w tym przykładzie wprowadź **${JOB_NAME}** jako nazwa kontenera hello.
   
    **Porada**
   
    Poniżej hello **polecenia** sekcji, w którym wprowadzono skryptu dla **wykonywanie wsadowe systemu Windows polecenie** jest łącze zmiennych środowiskowych toohello rozpoznaje Hudson. Kliknij przycisk Połącz nazwy zmiennych środowiskowych hello toolearn wraz z opisami. Należy pamiętać, że środowisko zmiennych, które zawierają znaki specjalne, takie jak hello **BUILD_URL** zmiennej środowiskowej, nie są dozwolone jako nazwa kontenera lub wspólnej ścieżki wirtualnej.
8. Kliknij przycisk **Upublicznij domyślnie nowy kontener** w tym przykładzie. (Jeśli chcesz toouse Kontener prywatny należy toocreate dostępu tooallow sygnatury dostępu współdzielonego. Która wykracza poza zakres tego artykułu hello. Dowiedz się więcej na temat sygnatur dostępu współdzielonego w [za pomocą sygnatur dostępu do udostępnionych (SAS)](../storage-dotnet-shared-access-signature-part-1.md).)
9. [Opcjonalnie] Kliknij przycisk **czystą kontenera przed przekazaniem** Jeśli toobe kontenera hello wyczyszczone zawartości przed artefaktów kompilacji są przekazywane (Pozostaw zaznaczenie opcji, jeśli nie chcesz, aby zawartość hello tooclean kontenera hello).
10. Dla **tooupload listy artefakty**, wprowadź  **tekstu /*.txt**.
11. Dla **wspólnej ścieżki wirtualnej przekazane artefaktów**, wprowadź **${kompilacji\_identyfikator} / ${kompilacji\_numer}**.
12. Kliknij przycisk **zapisać** toosave ustawień.
13. W hello Hudson pulpitu nawigacyjnego, kliknij przycisk **kompilacji teraz** toorun **MyJob**. Sprawdź dane wyjściowe konsoli hello stanu. Komunikaty o stanie dla usługi Azure Storage są uwzględniane w danych wyjściowych konsoli hello uruchomienia działania mające miejsce po kompilacji hello tooupload artefaktów kompilacji.
14. Po pomyślnym ukończeniu zadania hello należy zbadać artefaktów kompilacji hello otwierając hello publicznego obiektu blob.
    
    a. Zaloguj się toohello [Azure Portal](https://portal.azure.com).
    
    b. Kliknij przycisk **magazynu**.
    
    c. Kliknij nazwę konta magazynu hello używanej Hudson.
    
    d. Kliknij przycisk **kontenery**.
    
    e. Kliknij przycisk hello kontener o nazwie **myjob**, wersja małe hello nazwy zadania hello przypisana podczas tworzenia hello Hudson zadania. Nazwa kontenera i nazwy obiektów blob są małe litery (a z uwzględnieniem wielkości liter) w usłudze Azure Storage. W ramach hello listę obiektów blob do kontenera hello o nazwie **myjob** powinna zostać wyświetlona **hello.txt** i **date.txt**. Kopiuj adres URL hello dowolny z tych elementów, a następnie otwórz go w przeglądarce. Zobaczysz hello pliku tekstowego, który został przekazany jako artefaktów kompilacji.

Można utworzyć tylko jedną akcję mające miejsce po kompilacji, która przekazuje tooAzure artefakty magazynu obiektów Blob na zadanie. Należy pamiętać, że magazyn obiektów Blob tooAzure tooupload artefakty hello jednego działania mające miejsce po kompilacji można określić różnych plików (w tym symboli wieloznacznych) i toofiles ścieżek w ciągu **tooupload listy artefakty** przy użyciu średnika jako separatora. Na przykład jeśli Twoje Hudson kompilacji tworzy pliki JAR i pliki TXT w swoim obszarze roboczym **kompilacji** folderu i chcesz tooupload zarówno tooAzure magazynu obiektów Blob, należy użyć następującego hello dla hello **tooupload listy artefakty** wartość: **kompilacji /\*JAR; kompilacji /\*.txt**. Umożliwia także składni podwójnego dwukropka toospecify toouse ścieżki, w ramach hello nazwa obiektu blob. Na przykład, jeśli chcesz, aby tooget słoików hello przekazany za pośrednictwem **plików binarnych** hello ścieżka obiektu blob i tooget pliki TXT hello przekazany za pośrednictwem **powiadomienia** w hello ścieżka obiektu blob, przy użyciu następujących hello hello  **Lista artefaktów tooupload** wartość: **kompilacji /\*. jar::binaries; kompilacji /\*. txt::notices**.

## <a name="how-toocreate-a-build-step-that-downloads-from-azure-blob-storage"></a>Jak toocreate kroku kompilacji który pliki do pobrania z magazynu obiektów Blob platformy Azure
Hello następujące kroki pokazują, jak krok elementów toodownload tooconfigure kompilacji z magazynu obiektów Blob platformy Azure. Powinien to być przydatne w przypadku elementów tooinclude w kompilacji, na przykład słoików znajdujących się w magazynie obiektów Blob Azure.

1. W hello **kompilacji** sekcji hello zadania konfiguracji, kliknij przycisk **kroku kompilacji Dodaj** i wybierz polecenie **pobrać z magazynu obiektów Blob Azure**.
2. Aby uzyskać **nazwy konta magazynu**, wybierz hello toouse konta magazynu.
3. Aby uzyskać **nazwa kontenera**, określ nazwę hello hello kontenera, który zawiera obiekty BLOB hello ma toodownload. Można używać zmiennych środowiskowych.
4. Aby uzyskać **nazwa obiektu Blob**, określ nazwę obiektu blob hello. Można używać zmiennych środowiskowych. Ponadto można użyć znak gwiazdki jako symbolu wieloznacznego po określeniu znakami hello hello nazwy obiektu blob. Na przykład **projektu\***  określić wszystkie obiekty BLOB, których nazwy rozpoczynają się od **projektu**.
5. [Opcjonalnie] Aby uzyskać **ścieżkę pobierania**, określ ścieżkę hello na powitania maszyny Hudson miejscu toodownload pliki z magazynu obiektów Blob platformy Azure. Można także zmiennych środowiskowych. (Jeśli nie zostanie określona wartość **ścieżkę pobierania**, hello pliki z magazynu obiektów Blob Azure będą pobrane toohello zadania obszaru roboczego.)

Jeśli masz dodatkowe elementy, które chcesz toodownload z magazynu obiektów Blob platformy Azure, można utworzyć kompilacji dodatkowe kroki.

Po uruchomieniu kompilacji, można sprawdzić hello kompilacji dane wyjściowe konsoli historii lub znajduje się w lokalizacji pobierania, toosee hello czy obiekty BLOB, które miały zostały pomyślnie pobrane.

## <a name="components-used-by-hello-blob-service"></a>Składniki używane przez hello usługi Blob
następujące Hello zawiera omówienie składników usługi hello obiektu Blob.

* **Konto magazynu**: wszystkie dostępu tooAzure magazynu odbywa się za pomocą konta magazynu. Jest to najwyższy poziom hello przestrzeń nazw hello dla uzyskiwania dostępu do obiektów blob. Konto może zawierać nieograniczoną liczbę kontenerów, tak długo, jak ich łączny rozmiar wynosi poniżej 100 TB.
* **Kontener**: kontener zawiera grupowanie zestawu obiektów blob. Wszystkie obiekty blob muszą być w kontenerze. Konto może zawierać nieograniczoną liczbę kontenerów. Kontener może przechowywać nieograniczoną liczbę obiektów blob.
* **Obiekt blob**: typ i rozmiar pliku. Istnieją dwa typy obiektów blob, które mogą być przechowywane w usłudze Azure Storage: blokowe i stronicowe obiekty BLOB. Większość plików są blokowych obiektów blob. Pojedynczy blokowy obiekt blob może być się rozmiar too200 GB. W tym samouczku korzysta z blokowych obiektów blob. Stronicowe obiekty BLOB innego typu obiektu blob, może być zapasowej TB too1 rozmiar i są bardziej wydajne, gdy zakresy bajtów w pliku są często modyfikowane. Aby uzyskać więcej informacji dotyczących obiektów blob, zobacz [opis blokowych obiektów blob, Dołącz obiektów blob i stronicowe obiekty BLOB](http://msdn.microsoft.com/library/azure/ee691964.aspx).
* **Format adresu URL**: obiekty BLOB mają hello następującego formatu adresu URL:
  
    `http://storageaccount.blob.core.windows.net/container_name/blob_name`
  
    (format hello powyżej dotyczy toohello chmury Azure publicznej. Jeśli używasz innej chmury Azure używać punktu końcowego hello w hello [Azure Portal](https://portal.azure.com) toodetermine punktu końcowego adresu URL.)
  
    W formacie hello powyżej `storageaccount` reprezentuje hello nazwy konta magazynu `container_name` reprezentuje hello nazwa Twojej kontenera i `blob_name` reprezentuje hello odpowiednio nazwę Twojej blob. W nazwie kontenera hello, może mieć wiele ścieżek rozdzielonych ukośnikiem,  **/** . Przykładowa nazwa kontenera Hello w tym samouczku został **MyJob**, i **${kompilacji\_identyfikator} / ${kompilacji\_numer}** została użyta dla hello wspólnej ścieżki wirtualnej, co powoduje hello obiektu blob o Adres URL hello następującej postaci:
  
    `http://example.blob.core.windows.net/myjob/2014-05-01_11-56-22/1/hello.txt`

## <a name="next-steps"></a>Następne kroki
* [Spełnia Hudson](http://wiki.eclipse.org/Hudson-ci/Meet_Hudson)
* [Magazyn Azure SDK dla języka Java](https://github.com/azure/azure-storage-java)
* [Odwołanie do zestawu SDK klienta usługi Azure Storage](http://dl.windowsazure.com/storage/javadoc/)
* [Interfejs API REST usług Azure Storage](https://msdn.microsoft.com/library/azure/dd179355.aspx)
* [Blog zespołu odpowiedzialnego za usługę Azure Storage](http://blogs.msdn.com/b/windowsazurestorage/)

Aby uzyskać więcej informacji, odwiedź stronę [Azure dla deweloperów języka Java](/java/azure).