>[!NOTE]
> Możesz pozostawić komentarze na tej stronie opinii lub za pomocą [Azure opinii](https://feedback.azure.com/forums/216843-virtual-machines) #azerrormessage znacznika.

## <a name="error-response-format"></a>Format odpowiedzi błędu 
Maszyny wirtualne platformy Azure, użyj następującego formatu JSON dla odpowiedzi na błąd hello:

```json
{
  "status": "status code",
  "error": {
    "code":"Top level error code",
    "message":"Top level error message",
    "details":[
     {
      "code":"Inner evel error code",
      "message":"Inner level error message"
     }
    ]
   }
}
```

Odpowiedzi na błąd zawsze zawiera kod stanu i obiektu błędu. Każdy obiekt błąd zawsze zawiera kod błędu i komunikatu. Jeśli hello maszyny Wirtualnej jest tworzona przy użyciu szablonu, obiekt błędu hello zawiera także sekcji Szczegóły, która zawiera wewnętrzny poziom nawiasów kody błędów i komunikatów. Zazwyczaj hello większości wewnętrzny poziom nawiasów komunikat o błędzie jest hello awarii głównego.


## <a name="common-virtual-machine-management-errors"></a>Typowe błędy zarządzania maszyny wirtualnej

W tej sekcji przedstawiono hello typowe komunikaty o błędach, które można napotkać podczas zarządzania maszyn wirtualnych:

|  Kod błędu:  |  Komunikat o błędzie  |  
|  :------| :-------------|  
|  AcquireDiskLeaseFailed  |  Nie można tooacquire dzierżawy podczas tworzenia dysku "{0}" za pomocą obiektu blob z identyfikatorem URI {1}. Obiekt blob jest już używana.  |  
|  AllocationFailed  |  Alokacja nie powiodła się. Spróbuj zmniejszyć rozmiar maszyny Wirtualnej hello lub liczbę maszyn wirtualnych, spróbuj ponownie później lub wdrażanie tooa innego zestawu dostępności lub innej lokalizacji platformy Azure.  |  
|  AllocationFailed  |  Hello alokacji maszyny Wirtualnej nie powiodła z powodu wewnętrznego błędu tooan. Spróbuj ponownie później lub spróbuj przeprowadzić wdrożenie tooa innej lokalizacji.  |
|  ArtifactNotFound  |  Nie można odnaleźć Hello rozszerzenia maszyny Wirtualnej o wydawcy "{0}" i typie "{1}" w lokalizacji "{2}".  |
|  ArtifactNotFound  |  Rozszerzenie o wydawcy "{0}", wpisz "{1}" i nie można odnaleźć wersji programu obsługi typu "{2}" w repozytorium rozszerzeń hello.  |
|  ArtifactVersionNotFound  |  Nie znaleziono w repozytorium artefaktów hello spełniająca hello wersji żądanej wersji "{0}".  |
|  ArtifactVersionNotFound  |  Nie znaleziono w repozytorium artefaktów hello spełniająca hello wersji żądanej wersji "{0}" dla rozszerzenia maszyny Wirtualnej o wydawcy "{1}" i typie "{2}".  |
|  AttachDiskWhileBeingDetached  |  Nie można dołączyć danych tooVM dysku "{0}" "{1}", ponieważ dysk hello jest aktualnie odłączona. Poczekaj, aż hello dysk zostanie całkowicie odłączony, a następnie spróbuj ponownie.  |
|  Element BadRequest  |  Wyrównane "zestawów dostępności nie są jeszcze obsługiwane w tym regionie.  |
|  Element BadRequest  |  Dodawanie maszyny wirtualnej z dyskami zarządzanych, zarządzać toonon zestawu dostępności lub dodanie z toomanaged dysków obiektu blob na podstawie zestawu dostępności maszyny wirtualnej nie jest obsługiwana. Utwórz zbiór dostępności z właściwością "zarządzany" wartości w kolejności tooadd maszyny Wirtualnej z tooit dysków zarządzanych.  |
|  Element BadRequest  |  Dyski zarządzane nie są obsługiwane w tym regionie.  |
|  Element BadRequest  |  Wiele Vmextension na program obsługi nie jest obsługiwane w systemie operacyjnym typu "{0}". VMExtension "{1}" z programem obsługi "{2}" już dodany lub określony w danych wejściowych.  |
|  Element BadRequest  |  Operacja "{0}" nie jest obsługiwana dla zasobu "{1}" w przypadku dysków zarządzanych.  |
|  CertificateImproperlyFormatted  |  Witaj reprezentacja JSON klucza tajnego pobierane z {0} ma pole danych, która nie jest poprawnie sformatowanym plikiem PFX lub podane hasło hello nie dekoduje prawidłowo pliku PFX hello.  |
|  CertificateImproperlyFormatted  |  Witaj dane pobrane z {0} nie jest da się rozszeregować na formacie JSON.  |
|  Konflikt  |  Zmiana rozmiaru dysku jest dozwolona tylko w przypadku tworzenia maszyny Wirtualnej lub po deallocated hello maszyny Wirtualnej.  |
|  ConflictingUserInput  |  Nie można dołączyć dysku "{0}", ponieważ hello dysku jest już przypisany do maszyny Wirtualnej "{1}".  |
|  ConflictingUserInput  |  Źródłowe i docelowe grupy zasobów są hello tego samego.  |
|  ConflictingUserInput  |  Konta magazynu źródłowego i docelowego dla dysku {0} są różne.  |
|  ContainerAlreadyOnLease  |  Jest już dzierżawę na powitania kontenerze magazynu przechowującym obiekt blob hello o identyfikatorze URI {0}.  |
|  CrossSubscriptionMoveWithKeyVaultResources  |  Żądanie hello przeniesienia zasobów zawiera zasoby KeyVault przywoływane przez co najmniej jeden {0} s w żądaniu hello. Nie jest to obsługiwane obecnie między subskrypcjami przenoszenia. Sprawdź, czy szczegóły błędu hello w celu hello identyfikatorów zasobów KeyVault.  |
|  DiagnosticsOperationInternalError  |  Wystąpił błąd wewnętrzny podczas przetwarzania profilu diagnostyki maszyny wirtualnej {0}.  |
|  DiskBlobAlreadyInUseByAnotherDisk  |  {0} obiektu blob jest już używana przez inny dysk należący tooVM "{1}". Możesz zbadać metadane obiektu blob hello, aby uzyskać informacje na dysku hello.  |
|  DiskBlobNotFound  |  Blob toofind wirtualnego dysku twardego o identyfikatorze URI {0} dla dysku "{1}".  |
|  DiskBlobNotFound  |  Blob toofind wirtualnego dysku twardego o identyfikatorze URI {0}.  |
|  DiskEncryptionKeySecretMissingTags  |  klucz tajny {0} nie ma hello {1} tagów. Zaktualizuj wersję klucza tajnego hello, Dodaj hello wymagane tagi i spróbuj ponownie.  |
|  DiskEncryptionKeySecretUnwrapFailed  |  Dekodowanie wartości tajny {0} przy użyciu klucza {1} nie powiodło się.  |
|  DiskImageNotReady  |  {0} obrazu dysku jest w stanie {1}. Spróbuj ponownie, gdy obraz będzie gotowy.  |
|  DiskPreparationError  |  Wystąpił co najmniej jeden błąd podczas przygotowywania dysków maszyny Wirtualnej. Zobacz widok wystąpienia dysku, aby uzyskać szczegółowe informacje.  |
|  DiskProcessingError  |  Dysku przetwarzanie zostało zatrzymane, jako hello maszyna wirtualna ma inne dyski w przypadku dysków nie powiodło się.  |
|  ImageBlobNotFound  |  Blob toofind wirtualnego dysku twardego o identyfikatorze URI {0} dla dysku "{1}".  |
|  ImageBlobNotFound  |  Blob toofind wirtualnego dysku twardego o identyfikatorze URI {0}.  |
|  IncorrectDiskBlobType  |  Obiekty BLOB dysków może być tylko typu stronicowych obiektów blob. {0} obiektu blob dla dysku "{1}" ma typ blokowy obiekt blob.  |
|  IncorrectDiskBlobType  |  Obiekty BLOB dysków może być tylko typu stronicowych obiektów blob. {0} obiektu blob jest typu "{1}".  |
|  IncorrectImageBlobType  |  Obiekty BLOB dysków może być tylko typu stronicowych obiektów blob. {0} obiektu blob dla dysku "{1}" ma typ blokowy obiekt blob.  |
|  IncorrectImageBlobType  |  Obiekty BLOB dysków może być tylko typu stronicowych obiektów blob. {0} obiektu blob jest typu "{1}".  |
|  InternalOperationError  |  Nie można rozpoznać konto magazynu {0}. Sprawdź, czy został utworzony za pośrednictwem dostawcy zasobów magazynu hello hello sam lokalizacji co hello zasoby obliczeniowe.  |
|  InternalOperationError  |  zadania poszukiwania celu {0} nie powiodło się.  |
|  InternalOperationError  |  Wystąpił błąd podczas sprawdzania poprawności hello profilu sieciowego maszyny Wirtualnej "{0}".  |
|  InvalidAccountType  |  Witaj AccountType {0} jest nieprawidłowy.  |
|  InvalidParameter  |  Witaj wartość parametru {0} jest nieprawidłowa.  |
|  InvalidParameter  |  określone hasło administratora Hello jest niedozwolone.  |
|  InvalidParameter  |  "hello podane hasło musi zawierać od {0}-{1\} \ znaków i musi spełniać co najmniej {2} z następujących hello, wymagania dotyczące złożoności hasła: <ol><li> Zawiera wielką literę</li><li>Zawiera małą literę</li><li>Zawiera cyfrę</li><li>Zawiera znaki specjalne.</li></ol>  |
|  InvalidParameter  |  Określona nazwa użytkownika administratora Hello jest niedozwolone.  |
|  InvalidParameter  |  Nie można dołączyć istniejącego dysku systemu operacyjnego, jeśli hello maszyna wirtualna jest utworzona z obrazu użytkownika lub platformy.  |
|  InvalidParameter  |  Nazwa kontenera {0} jest nieprawidłowy. Nazwy kontenerów muszą być 3 do 63 znaków długości i mogą zawierać tylko małe znaki alfanumeryczne i łączniki. Łącznik musi być poprzedzone i następuje znak alfanumeryczny.  |
|  InvalidParameter  |  Nazwa kontenera {0} w {1} adres URL jest nieprawidłowy. Nazwy kontenerów muszą być 3 do 63 znaków długości i mogą zawierać tylko małe znaki alfanumeryczne i łączniki. Łącznik musi być poprzedzone i następuje znak alfanumeryczny.  |
|  InvalidParameter  |  Nazwa obiektu blob Hello w {0} adres URL zawiera ukośnika. Jest to obecnie nieobsługiwane w przypadku dysków.  |
|  InvalidParameter  |  Identyfikator URI Hello {0} nie wygląda prawidłowe toobe identyfikator URI obiektu blob.  |
|  InvalidParameter  |  Dysk o nazwie "{0}" już używa tej samej jednostki LUN hello: {1}.  |
|  InvalidParameter  |  Dysk o nazwie "{0}" już istnieje.  |
|  InvalidParameter  |  Nie można określić zastępuje obraz użytkownika dla dysku już zdefiniowanego w hello określony obraz odniesienia.  |
|  InvalidParameter  |  Dysk o nazwie "{0}" już używa hello tego samego {1} adres URL dysku VHD.  |
|  InvalidParameter  |  Witaj {0} określony błąd domeny liczba musi należeć hello zakresu {1} too\ {2\}.  |
|  InvalidParameter  |  Witaj licencji typu {0} jest nieprawidłowy. Prawidłowy typ licencji są: Windows_Client lub Windows_Server, z uwzględnieniem wielkości liter.  |
|  InvalidParameter  |  Nazwa hosta systemu Linux nie może przekraczać {0} znaków ani zawierać następujących znaków hello: {1}.  |
|  InvalidParameter  |  Ścieżka docelowa kluczy publicznych Ssh jest obecnie ograniczone tooits domyślna wartość {0} tooa z powodu znanego problemu w agenta inicjowania obsługi administracyjnej systemu Linux.  |
|  InvalidParameter  |  Dysk pod numerem LUN {0} już istnieje.  |
|  InvalidParameter  |  {0} subskrypcji hello żądania musi odpowiadać {1} subskrypcji hello zawarte w identyfikatorze dysku zarządzanego hello.  |
|  InvalidParameter  |  Niestandardowe dane w profilu OSProfile muszą korzystać z szyfrowania Base64, a liczba ich znaków nie może przekraczać {0}.  |
|  InvalidParameter  |  Nazwa obiektu blob w {0} adres URL musi mieć rozszerzenie "{1}".  |
|  InvalidParameter  |  {0} "nie jest prawidłowy prefiks nazwy przechwyconego obiektu blob dysku VHD. Prawidłowy prefiks zgodny z wyrażeniem regularnym "{1}".  |
|  InvalidParameter  |  Nie można dodać certyfikatów tooyour maszyny Wirtualnej, jeśli nie zainicjowano hello agenta maszyny Wirtualnej.  |
|  InvalidParameter  |  Dysk pod numerem LUN {0} już istnieje.  |
|  InvalidParameter  |  Toocreate hello maszyny Wirtualnej ponieważ hello żądany rozmiar {0} nie jest dostępny w klastrze hello, gdzie jest przydzielonego hello zestawu dostępności. są dostępne rozmiary Hello: {1}. Przeczytaj więcej VM na zmianę rozmiaru strategii w https://aka.ms/azure-resizevm.  |
|  InvalidParameter  |  Hello żądany rozmiar maszyny Wirtualnej {0} nie jest dostępny w regionie bieżącego hello. Witaj w hello bieżącego obszaru są dostępne: {1}. Dowiedz się więcej na powitania dostępne rozmiary maszyn wirtualnych w każdym regionie na https://aka.ms/azure-regions.  |
|  InvalidParameter  |  Hello żądany rozmiar maszyny Wirtualnej {0} nie jest dostępny w regionie bieżącego hello. Dowiedz się więcej na powitania dostępne rozmiary maszyn wirtualnych w każdym regionie na https://aka.ms/azure-regions.  |
|  InvalidParameter  |  Nazwa użytkownika administratora systemu Windows nie może być większa niż {0} znaków długie, kończyć się kropką (.) ani zawierać hello następujących znaków: {1}.  |
|  InvalidParameter  |  Nazwa komputera systemu Windows nie może być większa niż {0} znaków długie, być całkowicie numeryczna ani zawierać hello następujących znaków: {1}.  |
|  MissingMoveDependentResources  |  Żądanie hello przeniesienia zasobów nie zawiera wszystkich zasobów zależnych hello. Sprawdź szczegóły błędów dotyczących brakujących identyfikatorów zasobów.  |
|  MoveResourcesHaveInvalidState  |  Żądanie przeniesienia zasobów Hello zawiera maszyny wirtualne, które są skojarzone z kontami magazynu nieprawidłowy. Sprawdź, czy szczegółowe informacje dotyczące tych identyfikatorów zasobów i nazwy konta magazynu do którego istnieje odwołanie.  |
|  MoveResourcesHavePendingOperations  |  Żądanie hello przeniesienia zasobów zawiera zasoby, dla których operacja oczekuje. Sprawdź szczegóły identyfikatorów tych zasobów. Ponów operację po ukończyć powitalnych oczekujących operacji.  |
|  MoveResourcesNotFound  |  Witaj przenoszenia zasobów zawiera zasoby, których nie można znaleźć. Sprawdź szczegóły identyfikatorów tych zasobów.  |
|  NetworkingInternalOperationError  |  Nieznany błąd alokacji sieci.  |
|  NetworkingInternalOperationError  |  Nieznany błąd alokacji sieci  |
|  NetworkingInternalOperationError  |  Wystąpił błąd wewnętrzny podczas przetwarzania profilu sieciowego hello maszyny Wirtualnej.  |
|  notFound  |  Nie można odnaleźć {0} Hello zestawu dostępności.  |
|  notFound  |  Źródłowej maszyny wirtualnej "{0}" określony w żądaniu hello nie istnieje w tej lokalizacji platformy Azure.  |
|  notFound  |  Nie znaleziono dzierżawy o identyfikatorze {0}.  |
|  notFound  |  Nie można odnaleźć obrazu Hello {0}.  |
|  NotSupported  |  Typ licencji Hello to {0}, ale {1} obiektu blob obrazu hello nie pochodzi z lokalnymi.  |
|  OperationNotAllowed  |  Nie można usunąć zestawu dostępności {0}. Przed usunięciem zestawu danych o dostępności upewnij się, że nie zawiera żadnej maszyny Wirtualnej.  |
|  OperationNotAllowed  |  Zmiana dostępności jednostka SKU zestawu z too'Classic "Wyrównany" "nie jest dozwolone.  |
|  OperationNotAllowed  |  Nie można modyfikować rozszerzeń w hello maszyny Wirtualnej, kiedy hello maszyna wirtualna nie jest uruchomiona.  |
|  OperationNotAllowed  |  Witaj akcji przechwytywania jest obsługiwana tylko na maszynie wirtualnej z dyskami na podstawie obiektu blob. Użyj hello "Image" zasobu interfejsów API toocreate obrazów z zarządzanych maszyny wirtualnej.  |
|  OperationNotAllowed  |  Nie można utworzyć Hello zasobu {0} z obrazu {1}, dopóki obraz został utworzony pomyślnie.  |
|  OperationNotAllowed  |  TooencryptionSettings aktualizacji nie jest dozwolona, gdy maszyna wirtualna jest przydzielany, spróbuj ponownie po cofnięciu przydziału maszyny Wirtualnej  |
|  OperationNotAllowed  |  Dodawanie dysków zarządzanych w tooa maszyny Wirtualnej z dyskami na podstawie obiektu blob nie jest obsługiwane.  |
|  OperationNotAllowed  |  Maksymalna liczba dysków z danymi Hello dozwolone tooa toobe dołączona maszyna wirtualna ten rozmiar jest {0}.  |
|  OperationNotAllowed  |  Dodawanie obiektów blob na podstawie tooVM dysku z dyskami zarządzanych nie jest obsługiwane.  |
|  OperationNotAllowed  |  Operacja "{0}" nie jest dozwolona w obrazie "{1}" od powitalne obrazu jest oznaczona do usunięcia. Możesz tylko ponowić operację usuwania hello (lub poczekaj, aż bieżące toocomplete jeden).  |
|  OperationNotAllowed  |  Operacja "{0}" nie jest dozwolona na maszynie Wirtualnej "{1}", ponieważ powitalne uogólniona maszyna wirtualna.  |
|  OperationNotAllowed  |  Operacja "{0}" nie jest dozwolona jako kolekcja punktu przywracania "{1}" jest oznaczona do usunięcia.  |
|  OperationNotAllowed  |  Operacja "{0}" nie jest dozwolona na rozszerzenia maszyny Wirtualnej "{1}", ponieważ jest ona oznaczona do usunięcia. Możesz tylko ponowić operację usuwania hello (lub poczekaj, aż bieżące toocomplete jeden).  |
|  OperationNotAllowed  |  Operacja "{0}" nie jest dozwolona, ponieważ hello maszyn wirtualnych "{1}" jest inicjowana przy użyciu obrazu hello "{2}".  |
|  OperationNotAllowed  |  Operacja "{0}" nie jest dozwolona, ponieważ aktualnie używa hello obrazu "{2}" hello ScaleSet maszyny wirtualnej "{1}".  |
|  OperationNotAllowed  |  Operacja "{0}" nie jest dozwolona na maszynie Wirtualnej "{1}" od powitalne maszyna wirtualna została oznaczona do usunięcia. Możesz tylko ponowić operację usuwania hello (lub poczekaj, aż bieżące toocomplete jeden).  |
|  OperationNotAllowed  |  Operacja "{0}" nie jest dozwolona na maszyny Wirtualnej "{1}", ponieważ hello maszyny Wirtualnej jest deallocated lub oznaczone toobe alokację.  |
|  OperationNotAllowed  |  Operacja "{0}" nie jest dozwolona na maszynie Wirtualnej "{1}" od powitalne maszyna wirtualna jest uruchomiona. Sprawdź Wyłącz zasilanie jawnie w przypadku zamykania hello maszyny Wirtualnej z wewnątrz systemu operacyjnego gościa hello.  |
|  OperationNotAllowed  |  Operacja "{0}" nie jest dozwolona na maszynie Wirtualnej "{1}" od powitalne nie cofnięciu przydziału maszyny Wirtualnej.  |
|  OperationNotAllowed  |  Operacja "{0}" nie jest dozwolona na maszynie Wirtualnej "{1}", ponieważ maszyna wirtualna ma rozszerzenie "{2}" w stanie niepowodzenia.  |
|  OperationNotAllowed  |  Operacja "{0}" nie jest dozwolona na maszynie Wirtualnej "{1}", ponieważ inna operacja jest w toku.  |
|  OperationNotAllowed  |  Operacja Hello "{0}" wymaga hello maszyny wirtualnej "{1}" toobe Uogólniono.  |
|  OperationNotAllowed  |  Operacja Hello wymaga hello toobe maszyna wirtualna uruchomiona (lub ustawić toorun).  |
|  OperationNotAllowed  |  Dysk z rozmiar {0} GB, która jest mniejsza niż hello rozmiaru {1}GB odpowiedniego dysku w obrazie, jest niedozwolone.  |
|  OperationNotAllowed  |  Rozszerzenia zestawu skali maszyny Wirtualnej programu obsługi "{0}" można dodać tylko w czasie hello tworzenia zestawu skali maszyny Wirtualnej.  |
|  OperationNotAllowed  |  Rozszerzenia zestawu skali maszyny Wirtualnej programu obsługi "{0}" może być usunięta tylko w czasie hello usuwania zestawu skali maszyny Wirtualnej.  |
|  OperationNotAllowed  |  Maszyny Wirtualnej "{0}" jest już używa dysków zarządzanych.  |
|  OperationNotAllowed  |  Maszyna wirtualna "{0}" należy too'Classic "zestawu dostępności"{1}". Sprawdź dostępność aktualizacji hello ustawić toouse "wyrównany' SKU, a następnie spróbuj ponownie hello konwersji.  |
|  OperationNotAllowed  |  Utworzony na podstawie obrazu maszyny Wirtualnej nie może mieć obiektu blob na podstawie dysków. Wszystkie dyski są dyski toobe zarządzane.  |
|  OperationNotAllowed  |  Przechwytywanie nie można ukończyć operacji, ponieważ hello uogólniona maszyna wirtualna jest nie.  |
|  OperationNotAllowed  |  Operacje zarządzania na maszynie Wirtualnej "{0}" są niedozwolone, ponieważ dyski maszyny Wirtualnej zostanie przekonwertowana toomanaged dysków.  |
|  OperationNotAllowed  |  Wykonywana operacja zmienia stan zasilania maszyny wirtualnej too\ {0} {1\}. Przeprowadź {2} operację po pewnym czasie.  |
|  OperationNotAllowed  |  Nie można tooadd lub aktualizacji hello maszyny Wirtualnej. Hello żądany rozmiar maszyny Wirtualnej {0} może nie być dostępne w jednostce alokacji istniejącego hello. Przeczytaj więcej VM na zmianę rozmiaru strategii w https://aka.ms/azure-resizevm.  |
|  OperationNotAllowed  |  Tooresize hello maszyny Wirtualnej ponieważ hello żądany rozmiar {0} nie jest dostępny w klastrze hello, gdzie jest przydzielonego hello zestawu dostępności. są dostępne rozmiary Hello: {1}. Przeczytaj więcej VM na zmianę rozmiaru strategii w https://aka.ms/azure-resizevm.  |
|  OperationNotAllowed  |  Tooresize hello maszyny Wirtualnej ponieważ hello żądany rozmiar {0} nie jest dostępny w klastrze hello gdzie hello maszyna wirtualna jest aktualnie przydzielone. tooresize sieci VM too\ {1\} skontaktuj deallocate (jest to operacja zatrzymania w hello portalu Azure), a następnie spróbuj ponownie operacji zmiany rozmiaru hello. Przeczytaj więcej VM na zmianę rozmiaru strategii w https://aka.ms/azure-resizevm.  |
|  OSProvisioningClientError  |  Inicjowanie obsługi administracyjnej systemu operacyjnego nie powiodło się dla maszyny Wirtualnej "{0}", ponieważ system operacyjny gościa hello jest aktualnie aprowizowany.  |
|  OSProvisioningClientError  |  Inicjowania obsługi systemu operacyjnego dla maszyny Wirtualnej "{0}" nie powiodło się. Szczegóły błędu: {1} upewnij się, że obraz powitania został poprawnie przygotowany (uogólniony). <ul><li>Instrukcje dla systemu Windows: https://azure.microsoft.com/documentation/articles/virtual-machines-windows-upload-image/  </li></ul> |
|  OSProvisioningClientError  |  Generowanie klucza SSH hosta nie powiodło się. Szczegóły błędu: {0}. tooresolve ten problem, sprawdź, czy agenta systemu Linux jest poprawnie skonfigurowana. <ul><li>Możesz sprawdzić instrukcje hello: https://azure.microsoft.com/documentation/articles/virtual-machines-linux-agent-user-guide/ </li></ul> |
|  OSProvisioningClientError  |  Nazwa użytkownika określona dla hello maszyny Wirtualnej jest nieprawidłowa dla tej dystrybucji systemu Linux. Szczegóły błędu: {0}.  |
|  OSProvisioningInternalError  |  Inicjowanie obsługi administracyjnej systemu operacyjnego nie powiodła się dla maszyny Wirtualnej "{0}" ze względu na błąd wewnętrzny tooan.  |
|  OSProvisioningTimedOut  |  Inicjowania obsługi systemu operacyjnego dla maszyny Wirtualnej "{0}" nie zostało ukończone w hello wyznaczony czas. Witaj maszyna wirtualna może nadal pomyślnie zakończyć inicjowanie obsługi. Sprawdź później stan inicjowania obsługi administracyjnej.  |
|  OSProvisioningTimedOut  |  Inicjowania obsługi systemu operacyjnego dla maszyny Wirtualnej "{0}" nie zostało ukończone w hello wyznaczony czas. Witaj maszyna wirtualna może nadal pomyślnie zakończyć inicjowanie obsługi. Sprawdź później stan inicjowania obsługi administracyjnej. Sprawdź także, czy obraz powitania został poprawnie przygotowany (uogólniony).   <ul><li>Instrukcje dla systemu Windows: https://azure.microsoft.com/documentation/articles/virtual-machines-windows-upload-image/ </li><li> Instrukcje dla systemu Linux: https://azure.microsoft.com/documentation/articles/virtual-machines-linux-capture-image/</li></ul>  |
|  OSProvisioningTimedOut  |  Inicjowania obsługi systemu operacyjnego dla maszyny Wirtualnej "{0}" nie zostało ukończone w hello wyznaczony czas. Agent gościa maszyny Wirtualnej hello Wykryto jednak uruchomiona. Sugeruje to gościa hello systemu operacyjnego nie został poprawnie przygotowany toobe użyty jako obraz maszyny Wirtualnej (CreateOption = FromImage). tooresolve ten problem, albo użyj hello wirtualnego dysku twardego, ponieważ jest z CreateOption = Attach lub prawidłowo przygotowania go do użycia jako obraz:   <ul><li>Instrukcje dla systemu Windows: https://azure.microsoft.com/documentation/articles/virtual-machines-windows-upload-image/ </li><li> Instrukcje dla systemu Linux: https://azure.microsoft.com/documentation/articles/virtual-machines-linux-capture-image/</li></ul>  |
|  OverConstrainedAllocationRequest  |  Witaj wymaganego rozmiaru maszyny Wirtualnej nie jest obecnie dostępny w lokalizacji hello wybrane.  |
|  ResourceUpdateBlockedOnPlatformUpdate  |  Nie można zaktualizować zasobu w tej chwili ukończenia aktualizacji platformy tooongoing. Spróbuj ponownie później.  |
|  StorageAccountLimitation  |  Konto magazynu "{0}" nie obsługuje stronicowych obiektów blob, które są wymagane toocreate dysków.  |
|  StorageAccountLimitation  |  Konto magazynu „{0}” przekroczyło limit przydziału.  |
|  StorageAccountLocationMismatch  |  Nie można rozpoznać konto magazynu {0}. Sprawdź, czy został utworzony za pośrednictwem dostawcy zasobów magazynu hello hello sam lokalizacji co hello zasoby obliczeniowe.  |
|  StorageAccountNotFound  |  Nie można odnaleźć konta magazynu {0}. Upewnij się, konto magazynu nie zostanie usunięta i należy toohello tej samej lokalizacji platformy Azure jako hello maszyny Wirtualnej.  |
|  StorageAccountNotRecognized  |  Użyj konta magazynu zarządzanego przez dostawcę zasobów magazynu. Użycie {0} nie jest obsługiwane.  |
|  StorageAccountOperationInternalError  |  Podczas dostępu do konta magazynu {0} wystąpił błąd wewnętrzny.  |
|  StorageAccountSubscriptionMismatch  |  Konto magazynu {0} nie należy toosubscription {1}.  |
|  StorageAccountTooBusy  |  Konto magazynu "{0}" jest obecnie zbyt zajęty. Należy wziąć pod uwagę przy użyciu innego konta.  |
|  StorageAccountTypeNotSupported  |  {0} dysku używa {1}, który jest konto magazynu obiektów Blob. Spróbuj ponownie z konta magazynu ogólnego przeznaczenia.  |
|  StorageAccountTypeNotSupported  |  Konto magazynu {0} jest typu {1}. Funkcja diagnostyki rozruchu obsługuje typy kont magazynu {2}.  |
|  SubscriptionNotAuthorizedForImage  |  Witaj subskrypcja nie ma autoryzacji.  |
|  TargetDiskBlobAlreadyExists  |  Obiekt blob {0} już istnieje. Podaj toocreate identyfikator URI obiektu blob różnych nowego dysku danych puste "{1}".  |
|  TargetDiskBlobAlreadyExists  |  Przechwytywanie nie można kontynuować operacji, ponieważ docelowy obrazu obiektu blob {0} już istnieje, a hello flagi toooverwrite — obiekty BLOB dysków VHD nie jest ustawiona. Usunąć obiektu blob hello lub Ustaw flagę hello obiekty BLOB dysków VHD toooverwrite i spróbuj ponownie.  |
|  TargetDiskBlobAlreadyExists  |  Nie można kontynuować operacji przechwytywania, ponieważ obiekt blob obrazu docelowego {0} ma aktywną dzierżawę.   |
|  TargetDiskBlobAlreadyExists  |  Obiekt blob {0} już istnieje. Podaj inny identyfikator URI obiektu blob jako cel dysku "{1}".  |
|  TooManyVMRedeploymentRequests  |  Odebrano zbyt dużą liczbę żądań dla maszyny Wirtualnej "{0}" lub maszyn wirtualnych hello w hello tym samym zestawie dostępności co ta maszyna wirtualna. Spróbuj ponownie później.  |
|  VHDSizeInvalid  |  Witaj określona wartość rozmiaru dysku {0} dla dysku "{1}" z obiektu blob {2} jest nieprawidłowa. Rozmiar dysku musi należeć do zakresu od {3} i {4}.  |
|  VMAgentStatusCommunicationError  |  Maszyny Wirtualnej "{0}" nie zgłosiła stanu agenta maszyny Wirtualnej lub rozszerzenia. Sprawdź, czy hello maszyna wirtualna ma działającego agenta maszyny Wirtualnej i może nawiązywać połączenia wychodzące tooAzure magazynu.  |
|  VMArtifactRepositoryInternalError  |  Wystąpił błąd podczas komunikacji z repozytorium artefaktów hello tooretrieve szczegółów artefaktu maszyny Wirtualnej.  |
|  VMArtifactRepositoryInternalError  |  Wystąpił błąd wewnętrzny podczas pobierania danych artefaktu maszyny Wirtualnej hello z repozytorium artefaktów hello.  |
|  VMExtensionHandlerNonTransientError  |  Program obsługi "{0}" zgłosiła błąd dla rozszerzenia maszyny Wirtualnej "{1}" z kodem błędu terminala "{2}" i komunikatem o błędzie: "{3}"  |
|  VMExtensionManagementInternalError  |  Podczas przetwarzania rozszerzenia maszyny wirtualnej „{0}” wystąpił błąd wewnętrzny.  |
|  VMExtensionManagementInternalError  |  Wystąpiło wiele błędów podczas przygotowywania rozszerzeń maszyny Wirtualnej hello. Zobacz widok wystąpienia rozszerzenia maszyny Wirtualnej, aby uzyskać szczegółowe informacje.  |
|  VMExtensionProvisioningError  |  Maszyna wirtualna zgłosiła błąd podczas przetwarzania rozszerzenia "{0}". Komunikat o błędzie: "{1}".  |
|  VMExtensionProvisioningError  |  Wiele rozszerzeń maszyny Wirtualnej nie toobe inicjowana na powitania maszyny Wirtualnej. Zobacz widok wystąpienia rozszerzenia maszyny Wirtualnej hello szczegółowe informacje.  |
|  VMExtensionProvisioningTimeout  |  Inicjowanie obsługi rozszerzenia maszyny Wirtualnej "{0}" został przekroczony. Instalacja rozszerzenia może trwać zbyt długo lub nie można uzyskać stanu rozszerzenia.  |
|  VMMarketplaceInvalidInput  |  Tworzenie maszyny wirtualnej z obrazu niepochodzącego z witryny Marketplace nie wymagają informacji o planie, Usuń hello informacji o planie w żądaniu hello. Nazwa dysku systemu operacyjnego to {0}.  |
|  VMMarketplaceInvalidInput  |  informacje o zakupie Hello jest niezgodny. Nie można toodeploy z obrazu witryny Marketplace hello. Nazwa dysku systemu operacyjnego to {0}.  |
|  VMMarketplaceInvalidInput  |  Tworzenie maszyny wirtualnej z obrazu witryny Marketplace wymaga informacji o planie w żądaniu hello. Nazwa dysku systemu operacyjnego to {0}.  |
|  VMNotFound  |  Witaj maszyny Wirtualnej "{0}" nie można odnaleźć.  |
|  VMRedeploymentFailed  |  Ponownego wdrażania maszyny Wirtualnej "{0}" nie powiodła z powodu wewnętrznego błędu tooan. Spróbuj ponownie później.  |
|  VMRedeploymentTimedOut  |  Ponowne wdrożenie maszyny Wirtualnej "{0}" nie zostało zakończone w hello wyznaczony czas. Go może zakończyła się pomyślnie w pewnym czasie. W przeciwnym wypadku można ponowić żądanie hello.  |
|  VMStartTimedOut  |  Nie można uruchomić maszyny Wirtualnej "{0}" w hello wyznaczony czas. Witaj maszyna wirtualna nadal może uruchomić się pomyślnie. Sprawdź stan zasilania hello później.  |


## <a name="next-steps"></a>Następne kroki
Jeśli potrzebujesz więcej pomocy, skontaktuj się hello ekspertów platformy Azure na [hello fora MSDN Azure i przepełnienie stosu](https://azure.microsoft.com/support/forums/). Alternatywnie można pliku zdarzenia pomocy technicznej platformy Azure. Przejdź toohello [witrynę pomocy technicznej platformy Azure](https://azure.microsoft.com/support/options/) i wybierz **uzyskać obsługuje**.
