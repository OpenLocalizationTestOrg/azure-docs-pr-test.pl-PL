## <a name="configure-your-application-tooaccess-azure-storage"></a>Konfigurowanie sieci tooaccess aplikacji usługi Azure Storage
Istnieją dwa sposoby tooauthenticate Twojego tooaccess aplikacji usług magazynu:

* Klucz udostępniony: Użyj udostępnionych klucza tylko do celów testowych
* Udostępnionych podpis dostępu (SAS): Użyj sygnatury dostępu Współdzielonego dla aplikacji produkcyjnych

### <a name="shared-key"></a>Klucz wspólny
Uwierzytelniania klucza współużytkowanego oznacza, że aplikacja będzie korzystać z nazwy konta i konta usługi Magazyn kluczy tooaccess. Dla celów hello szybko przedstawiający sposób toouse tej biblioteki, użyjemy uwierzytelniania klucz udostępniony w tym wprowadzenie.

> [!WARNING] 
> **Klucz wstępny uwierzytelniania należy używać tylko do celów testowych!** Nazwa konta i klucz konta usługi, dzięki czemu toohello dostęp Pełna odczytu/zapisu skojarzone konto magazynu, rozproszonej tooevery osoby, która pobiera aplikacji. Jest to **nie** jest dobrą rozwiązaniem, ponieważ istnieje ryzyko, że po klucz szkodzi niezaufani klienci.
> 
> 

Podczas korzystania z uwierzytelniania klucza wspólnego, utworzysz [ciąg połączenia](../articles/storage/common/storage-configure-connection-string.md). Parametry połączenia Hello obejmuje:  

* Witaj **DefaultEndpointsProtocol** — możesz wybrać HTTP lub HTTPS. Jednak przy użyciu protokołu HTTPS zaleca się.
* Witaj **nazwa konta** — Witaj nazwa konta magazynu
* Witaj **klucz konta** — na powitania [portalu Azure](https://portal.azure.com), przejdź tooyour konta magazynu i kliknij hello **klucze** toofind ikona te informacje.
* (Opcjonalnie) **EndpointSuffix** — służy do usług magazynu w regionach z innym punktem końcowym sufiksów, na przykład chińskiej wersji platformy Azure lub zarządzania Azure.

Oto przykład parametrów połączenia przy użyciu klucza wspólnego uwierzytelniania:

`"DefaultEndpointsProtocol=https;AccountName=your_account_name_here;AccountKey=your_account_key_here"`

### <a name="shared-access-signatures-sas"></a>Sygnatury dostępu współdzielonego (SAS)
Dla aplikacji mobilnej hello zalecana metoda uwierzytelniania żądania przez klienta na powitania usługi Azure Storage jest użycie udostępnionych podpis dostępu (SAS). Sygnatury dostępu Współdzielonego pozwala toogrant zasobu tooa dostępu klienta w określonym przedziale czasu, z określonym zestawem uprawnień.
Jako właściciel konta magazynu hello musisz toogenerate sygnatury dostępu Współdzielonego tooconsume Twojego klientów mobilnych. toogenerate hello SAS, prawdopodobnie należy toowrite oddzielne usługa, która generuje hello SAS toobe rozproszonych tooyour klientów. Do celów testowych, można użyć hello [Eksploratora usługi Microsoft Azure Storage](http://storageexplorer.com) lub hello [Azure Portal](https://portal.azure.com) toogenerate sygnatury dostępu Współdzielonego. Podczas tworzenia hello sygnatury dostępu Współdzielonego, można określić hello interwał czasu, przez które hello SAS jest prawidłowa, a uprawnienia hello hello SAS przyznaje toohello klienta.

Witaj poniższy przykład pokazuje, jak toouse hello toogenerate Eksploratora usługi Microsoft Azure Storage sygnatury dostępu Współdzielonego.

1. Jeśli nie jest jeszcze, [hello instalowanie Eksploratora usługi Microsoft Azure Storage](http://storageexplorer.com)
2. Połącz tooyour subskrypcji.
3. Kliknij konto magazynu, a następnie kliknij na karcie Akcje"hello" w lewym dolnym rogu okna hello. Kliknij przycisk "Uzyskaj sygnaturę dostępu współdzielonego" toogenerate "Parametry połączenia" dla sieci SAS.
4. Oto przykład parametrów połączenia SAS że przyznaje uprawnienia odczytu i zapisu hello usługi, poziomie obiektu usługi blob hello hello konta magazynu i kontenera.
   
   `"SharedAccessSignature=sv=2015-04-05&ss=b&srt=sco&sp=rw&se=2016-07-21T18%3A00%3A00Z&sig=3ABdLOJZosCp0o491T%2BqZGKIhafF1nlM3MzESDDD3Gg%3D;BlobEndpoint=https://youraccount.blob.core.windows.net"`

Jak widać, korzystając z sygnatury dostępu Współdzielonego, że nie udostępnianie klucz konta w aplikacji. Dowiedz się więcej o sygnatury dostępu Współdzielonego i najlepsze rozwiązania dotyczące przy użyciu sygnatury dostępu Współdzielonego przez wyewidencjonowanie [sygnatury dostępu współdzielonego: opis hello SAS model](../articles/storage/common/storage-dotnet-shared-access-signature-part-1.md).

