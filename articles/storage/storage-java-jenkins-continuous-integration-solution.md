---
title: "aaaUsing usługi Azure Storage z Wpięć ciągłej integracji rozwiązania | Dokumentacja firmy Microsoft"
description: "W tym samouczku pokazują, jak toouse hello Azure usługa blob jako repozytorium dla kompilacji artefakty utworzone przez rozwiązanie Wpięć ciągłej integracji."
services: storage
documentationcenter: java
author: seguler
manager: jahogg
editor: tysonn
ms.assetid: f4e5ca75-f6cb-4f74-981b-2aa06bb8de45
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 02/28/2017
ms.author: seguler
ms.openlocfilehash: a8a8c6f3b03cf61d7ad98f0b38e9421dd0b47bfd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-storage-with-a-jenkins-continuous-integration-solution"></a>Korzystanie z usługi Azure Storage z rozwiązaniem ciągłej integracji Jenkins
## <a name="overview"></a>Omówienie
Witaj następujące informacje pokazuje, jak toouse magazynu obiektów Blob jako repozytorium artefaktów kompilacji utworzone przez rozwiązanie Wpięć ciągłej integracji (CI) lub jako źródło do pobrania plików toobe używane w procesie kompilacji. Jest jednego ze scenariuszy hello, w którym użytkownik może to być przydatne, gdy jest kodowania w środowisku elastyczne programowanie (przy użyciu języka Java lub innych języków), kompilacje działają na podstawie ciągłej integracji i potrzebujesz repozytorium artefaktów z kompilacji, tak, aby było to możliwe , na przykład udostępniać je z innymi elementami członkowskimi organizacji klienta, lub Obsługa archiwum. Inny scenariusz jest, gdy sam zadania kompilacji wymaga innych plików, na przykład zależności toodownload jako część hello Konstruuj wprowadzania.

W tym samouczku używana będzie hello wtyczki magazynu Azure dla Wpięć elementu CI udostępnione przez firmę Microsoft.

## <a name="overview-of-jenkins"></a>Omówienie Wpięć
Umożliwia Wpięć ciągłej integracji projektu oprogramowania przez deweloperów tooeasily zintegrować ich zmiany kodu i mieć kompilacje utworzonych automatycznie i często, zwiększając wydajność hello hello deweloperów. Kompilacje są określonej wersji, a artefaktów kompilacji może być przekazane toovarious repozytoriów. W tym temacie opisano sposób toouse Azure magazynu obiektów blob jako repozytorium hello hello artefaktów kompilacji. Pokazują również, jak magazynu obiektów blob toodownload zależności z platformy Azure.

Więcej informacji na temat Wpięć można znaleźć w folderze [spełnia Wpięć](https://wiki.jenkins-ci.org/display/JENKINS/Meet+Jenkins).

## <a name="benefits-of-using-hello-blob-service"></a>Zalety używania usługi Blob hello
Przy użyciu hello obiektu Blob usługi toohost Twojego artefaktów kompilacji elastyczne programowanie zalety:

* Wysoka dostępność artefaktów kompilacji i/lub zależności do pobrania.
* Wydajność rozwiązania CI Wpięć przekazuje użytkownika artefaktów kompilacji.
* Wydajność, gdy klienci i partnerzy pobrać artefaktów z kompilacji.
* Kontrolę nad zasad dostępu, wybór między anonimowego dostępu, dostęp sygnatury dostępu współdzielonego opartych na wygaśnięcia, prywatne, dostępu itd.

## <a name="prerequisites"></a>Wymagania wstępne
Można będzie muszą hello następujących toouse hello usługa Blob wraz z rozwiązaniem Wpięć CI:

* Rozwiązanie Wpięć ciągłej integracji.
  
    Jeśli obecnie nie ma rozwiązania CI Wpięć, możesz uruchomić rozwiązania CI Wpięć przy użyciu hello następujące techniki:
  
  1. Na komputerze z obsługą języka Java, Pobierz jenkins.war z <http://jenkins-ci.org>.
  2. W wierszu polecenia, który jest otwarty toohello folderu, który zawiera jenkins.war Uruchom polecenie:
     
      `java -jar jenkins.war`

  3. W przeglądarce otwórz `http://localhost:8080/`. Spowoduje to otwarcie pulpitu nawigacyjnego Wpięć hello, którego można będzie użyć tooinstall i skonfigurować hello wtyczki usługi Azure Storage.
     
      Podczas gdy typowe rozwiązania Wpięć elementu konfiguracji należy skonfigurować toorun jako usługa, systemem war Wpięć hello w wierszu polecenia hello będą wystarczające do celów tego samouczka.
* Konto platformy Azure. Można założyć konto platformy Azure w usłudze <http://www.azure.com>.
* Konto usługi Azure Storage. Jeśli nie masz już konto magazynu, możesz utworzyć jedną przy użyciu kroków hello na [Utwórz konto magazynu](storage-create-storage-account.md#create-a-storage-account).
* Zaleca się, ale nie wymaga znajomości hello CI Wpięć rozwiązania, jak hello następującą zawartość będzie używać tooshow prosty przykład Witaj kroki niezbędne w przypadku używania usługi Blob hello jako repozytorium dla Wpięć elementu CI tworzenie artefaktów.

## <a name="how-toouse-hello-blob-service-with-jenkins-ci"></a>Jak toouse hello usługa Blob z Wpięć elementu konfiguracji
Usługa Blob hello toouse z Wpięć, będziesz potrzebować tooinstall hello wtyczki usługi Azure Storage, skonfiguruj toouse wtyczki hello konta magazynu, a następnie utworzyć akcję po kompilacji, która przekazuje konta magazynu tooyour artefaktów kompilacji. Te kroki opisano w hello następujące sekcje.

## <a name="how-tooinstall-hello-azure-storage-plugin"></a>Jak tooinstall hello wtyczki usługi Azure Storage
1. W ramach hello Wpięć pulpitu nawigacyjnego, kliknij przycisk **Zarządzanie Wpięć**.
2. W hello **Zarządzanie Wpięć** kliknij przycisk **Zarządzanie wtyczkami**.
3. Kliknij przycisk hello **dostępne** kartę.
4. W hello **Uploaders artefaktu** sekcji wyboru **dodatek Microsoft Azure Storage**.
5. Kliknij opcję **zainstalować bez ponownego uruchomienia** lub **teraz pobrać i zainstalować po ponownym uruchomieniu**.
6. Uruchom ponownie Wpięć.

## <a name="how-tooconfigure-hello-azure-storage-plugin-toouse-your-storage-account"></a>Jak tooconfigure hello toouse wtyczki usługi Azure Storage konta magazynu
1. W ramach hello Wpięć pulpitu nawigacyjnego, kliknij przycisk **Zarządzanie Wpięć**.
2. W hello **Zarządzanie Wpięć** kliknij przycisk **skonfigurować System**.
3. W hello **konfiguracji konta magazynu Azure Microsoft** sekcji:
   1. Wprowadź nazwę konta magazynu, który można uzyskać z hello [Azure Portal](https://portal.azure.com).
   2. Wprowadź klucz konta magazynu również u: hello [Azure Portal](https://portal.azure.com).
   3. Użyj wartości domyślnej powitania dla **adres URL punktu końcowego usługi Blob** korzystania z chmury publicznej Azure hello. Jeśli używasz innej chmurze platformy Azure, użyj punktu końcowego hello jako hello określony w [Azure Portal](https://portal.azure.com) dla konta magazynu. 
   4. Kliknij przycisk **sprawdzanie poprawności poświadczeń magazynu** toovalidate Twojego konta magazynu. 
   5. [Opcjonalnie] Jeśli masz dodatkowe konta magazynu, które mają dokonano tooyour dostępne CI Wpięć, kliknij przycisk **dodać więcej kont magazynu**.
   6. Kliknij przycisk **zapisać** toosave ustawień.

## <a name="how-toocreate-a-post-build-action-that-uploads-your-build-artifacts-tooyour-storage-account"></a>Jak toocreate akcję po kompilacji, która przekazuje konta magazynu tooyour artefaktów kompilacji
Do celów instrukcji najpierw potrzebujemy toocreate zadanie, które będzie utworzyć kilka plików, a następnie dodaj na koncie magazynu tooyour hello działania mające miejsce po kompilacji tooupload hello plików.

1. W ramach hello Wpięć pulpitu nawigacyjnego, kliknij przycisk **nowy element**.
2. Zadania hello nazwa **MyJob**, kliknij przycisk **kompilowania projektu oprogramowania wolne stylu**, a następnie kliknij przycisk **OK**.
3. W hello **kompilacji** sekcji hello zadania konfiguracji, kliknij przycisk **kroku kompilacji Dodaj** i wybierz polecenie **wykonywanie wsadowe systemu Windows polecenie**.
4. W **polecenia**, użyj następującego polecenia hello:

    ```   
    md text
    cd text
    echo Hello Azure Storage from Jenkins > hello.txt
    date /t > date.txt
    time /t >> date.txt
    ```

5. W hello **działania mające miejsce po kompilacji** sekcji hello zadania konfiguracji, kliknij przycisk **dodać akcję postkompilacyjnego** i wybierz polecenie **przekazać magazynu obiektów Blob tooAzure artefakty**.
6. Aby uzyskać **nazwy konta magazynu**, wybierz hello toouse konta magazynu.
7. Aby uzyskać **nazwa kontenera**, określ nazwę kontenera hello. (kontener hello zostanie utworzony, jeśli go jeszcze nie istnieje po przekazaniu są hello artefaktów kompilacji.) Można używać zmiennych środowiskowych, dlatego w tym przykładzie wprowadź **${JOB_NAME}** jako nazwa kontenera hello.
   
    **Porada**
   
    Poniżej hello **polecenia** sekcji, w którym wprowadzono skryptu **wykonywanie wsadowe systemu Windows polecenia** jest łącze zmiennych środowiskowych toohello rozpoznaje Wpięć. Kliknij przycisk Połącz nazwy zmiennych środowiskowych hello toolearn wraz z opisami. Należy pamiętać, że środowisko zmiennych, które zawierają znaki specjalne, takie jak hello **BUILD_URL** zmiennej środowiskowej, nie są dozwolone jako nazwa kontenera lub wspólnej ścieżki wirtualnej.
8. Kliknij przycisk **Upublicznij domyślnie nowy kontener** w tym przykładzie. (Jeśli chcesz toouse Kontener prywatny należy toocreate dostępu tooallow sygnatury dostępu współdzielonego. Która wykracza poza zakres hello tego tematu. Dowiedz się więcej na temat sygnatur dostępu współdzielonego w [za pomocą sygnatur dostępu do udostępnionych (SAS)](storage-dotnet-shared-access-signature-part-1.md).)
9. [Opcjonalnie] Kliknij przycisk **czystą kontenera przed przekazaniem** Jeśli toobe kontenera hello wyczyszczone zawartości przed artefaktów kompilacji są przekazywane (Pozostaw zaznaczenie opcji, jeśli nie chcesz, aby zawartość hello tooclean kontenera hello).
10. Dla **tooupload listy artefakty**, wprowadź  **tekstu /*.txt**.
11. Dla **wspólnej ścieżki wirtualnej przekazane artefaktów**dla celów tego samouczka, wprowadź **${kompilacji\_identyfikator} / ${kompilacji\_numer}**.
12. Kliknij przycisk **zapisać** toosave ustawień.
13. Na pulpicie nawigacyjnym Wpięć hello, kliknij przycisk **kompilacji teraz** toorun **MyJob**. Sprawdź dane wyjściowe konsoli hello stanu. Komunikaty o stanie dla magazynu Azure będą uwzględniane w danych wyjściowych konsoli hello uruchomienia działania mające miejsce po kompilacji hello tooupload artefaktów kompilacji.
14. Po pomyślnym ukończeniu zadania hello należy zbadać artefaktów kompilacji hello otwierając hello publicznego obiektu blob.
    1. Toohello logowania [Azure Portal](https://portal.azure.com).
    2. Kliknij przycisk **magazynu**.
    3. Kliknij nazwę konta magazynu hello używanej Wpięć.
    4. Kliknij przycisk **kontenery**.
    5. Kliknij przycisk hello kontener o nazwie **myjob**, małe litery wersji hello nazwy zadania hello przypisana podczas tworzenia zadania Wpięć hello. Nazwa kontenera i nazwy obiektów blob są małe litery (a z uwzględnieniem wielkości liter) w magazynie Azure. W ramach hello listę obiektów blob do kontenera hello o nazwie **myjob** powinna zostać wyświetlona **hello.txt** i **date.txt**. Kopiuj adres URL hello dowolny z tych elementów, a następnie otwórz go w przeglądarce. Zobaczysz hello pliku tekstowego, który został przekazany jako artefaktów kompilacji.

Można utworzyć tylko jedną akcję mające miejsce po kompilacji, która przekazuje magazynu obiektów blob tooAzure artefaktów na zadanie. Należy pamiętać, że magazyn obiektów blob tooAzure tooupload artefakty hello jednego działania mające miejsce po kompilacji można określić różnych plików (w tym symboli wieloznacznych) i toofiles ścieżek w ciągu **tooupload listy artefakty** przy użyciu średnika jako separatora. Na przykład jeśli kompilacji z Wpięć tworzy pliki JAR i pliki TXT w swoim obszarze roboczym **kompilacji** folderu i chcesz tooupload zarówno tooAzure magazynu obiektów blob, należy użyć następującego hello dla hello **tooupload listy artefakty** wartość: **kompilacji /\*JAR; kompilacji /\*.txt**. Umożliwia także składni podwójnego dwukropka toospecify toouse ścieżki, w ramach hello nazwa obiektu blob. Na przykład, jeśli chcesz, aby tooget słoików hello przekazany za pośrednictwem **plików binarnych** hello ścieżka obiektu blob i tooget pliki TXT hello przekazany za pośrednictwem **powiadomienia** w hello ścieżka obiektu blob, przy użyciu następujących hello hello  **Lista artefaktów tooupload** wartość: **kompilacji /\*. jar::binaries; kompilacji /\*. txt::notices**.

## <a name="how-toocreate-a-build-step-that-downloads-from-azure-blob-storage"></a>Jak toocreate kroku kompilacji który pliki do pobrania z magazynu obiektów blob platformy Azure
Witaj następujące kroki pokazują, jak tooconfigure kompilacji krok toodownload elementy z magazynu obiektów blob platformy Azure. Powinien to być przydatne, jeśli chcesz tooinclude elementów w kompilacji, na przykład słoików zachowujących na platformie Azure magazynu obiektów blob.

1. W hello **kompilacji** sekcji hello zadania konfiguracji, kliknij przycisk **kroku kompilacji Dodaj** i wybierz polecenie **pobrać z magazynu obiektów Blob Azure**.
2. Aby uzyskać **nazwy konta magazynu**, wybierz hello toouse konta magazynu.
3. Aby uzyskać **nazwa kontenera**, określ nazwę hello hello kontenera, który zawiera obiekty BLOB hello ma toodownload. Można używać zmiennych środowiskowych.
4. Aby uzyskać **nazwa obiektu Blob**, określ nazwę obiektu blob hello. Można używać zmiennych środowiskowych. Ponadto można użyć znak gwiazdki jako symbolu wieloznacznego po określeniu znakami hello hello nazwy obiektu blob. Na przykład **projektu\***  określić wszystkie obiekty BLOB, których nazwy rozpoczynają się od **projektu**.
5. [Opcjonalnie] Aby uzyskać **ścieżkę pobierania**, określ ścieżkę hello na maszynie Wpięć hello miejscu toodownload pliki z magazynu obiektów blob platformy Azure. Można także zmiennych środowiskowych. (Jeśli nie zostanie określona wartość **ścieżkę pobierania**, hello pliki z magazynu obiektów blob Azure będą pobrane toohello zadania obszaru roboczego.)

Jeśli masz dodatkowe elementy, które chcesz toodownload z magazynu obiektów blob platformy Azure, można utworzyć kompilacji dodatkowe kroki.

Po uruchomieniu kompilacji, można sprawdzić hello kompilacji dane wyjściowe konsoli historii lub znajduje się w lokalizacji pobierania, toosee hello czy obiekty BLOB, które miały zostały pomyślnie pobrane.  

## <a name="components-used-by-hello-blob-service"></a>Składniki używane przez hello usługi Blob
następujące Hello zawiera omówienie składników usługi hello obiektu Blob.

* **Konto magazynu**: wszystkie dostępu tooAzure magazynu odbywa się za pomocą konta magazynu. Jest to najwyższy poziom hello przestrzeń nazw hello dla uzyskiwania dostępu do obiektów blob. Konto może zawierać nieograniczoną liczbę kontenerów, tak długo, jak ich łączny rozmiar wynosi poniżej 100TB.
* **Kontener**: kontener zawiera grupowanie zestawu obiektów blob. Wszystkie obiekty blob muszą być w kontenerze. Konto może zawierać nieograniczoną liczbę kontenerów. Kontener może przechowywać nieograniczoną liczbę obiektów blob.
* **Obiekt blob**: typ i rozmiar pliku. Istnieją dwa typy obiektów blob, które mogą być przechowywane w usłudze Azure Storage: blokowe i stronicowe obiekty BLOB. Większość plików są blokowych obiektów blob. Pojedynczy blokowy obiekt blob może być zapasowej too200GB rozmiar. W tym samouczku korzysta z blokowych obiektów blob. Stronicowe obiekty BLOB innego typu obiektu blob, może być zapasowej too1TB rozmiary i są bardziej wydajne, gdy zakresy bajtów w pliku są często modyfikowane. Aby uzyskać więcej informacji dotyczących obiektów blob, zobacz [opis blokowych obiektów blob, Dołącz obiektów blob i stronicowe obiekty BLOB](http://msdn.microsoft.com/library/azure/ee691964.aspx).
* **Format adresu URL**: obiekty BLOB mają hello następującego formatu adresu URL:
  
    `http://storageaccount.blob.core.windows.net/container_name/blob_name`
  
    (format hello powyżej dotyczy toohello chmury Azure publicznej. Jeśli używasz innej chmury Azure używać punktu końcowego hello w hello [Azure Portal](https://portal.azure.com) toodetermine punktu końcowego adresu URL.)
  
    W formacie hello powyżej `storageaccount` reprezentuje hello nazwy konta magazynu `container_name` reprezentuje hello nazwa Twojej kontenera i `blob_name` reprezentuje hello odpowiednio nazwę Twojej blob. W nazwie kontenera hello, może mieć wiele ścieżek rozdzielonych ukośnikiem,  **/** . Przykładowa nazwa kontenera Hello w tym samouczku został **MyJob**, i **${kompilacji\_identyfikator} / ${kompilacji\_numer}** została użyta dla hello wspólnej ścieżki wirtualnej, co powoduje hello obiektu blob o Adres URL hello następującej postaci:
  
    `http://example.blob.core.windows.net/myjob/2014-04-14_23-57-00/1/hello.txt`

## <a name="next-steps"></a>Następne kroki
* [Spełnia Wpięć](https://wiki.jenkins-ci.org/display/JENKINS/Meet+Jenkins)
* [Magazyn Azure SDK dla języka Java](https://github.com/azure/azure-storage-java)
* [Odwołanie do zestawu SDK klienta usługi Azure Storage](http://dl.windowsazure.com/storage/javadoc/)
* [Interfejs API REST usług Azure Storage](https://msdn.microsoft.com/library/azure/dd179355.aspx)
* [Blog zespołu odpowiedzialnego za usługę Azure Storage](http://blogs.msdn.com/b/windowsazurestorage/)

Aby uzyskać więcej informacji, zobacz też hello [Centrum deweloperów języka Java](https://azure.microsoft.com/develop/java/).
