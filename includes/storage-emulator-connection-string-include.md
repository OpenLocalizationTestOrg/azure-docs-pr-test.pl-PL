emulator magazynu Hello obsługuje jednego stałego konta i klucz uwierzytelniania dobrze znanego uwierzytelniania klucza wspólnego. Tego konta i klucz są hello dozwolone emulatorze magazynu hello tylko poświadczenia klucza wspólnego. Są to:

```
Account name: devstoreaccount1
Account key: Eby8vdM02xNOcqFlqUwJPLlmEtlCDXJ1OUzFT50uSRZ6IFsuFq2UVErCz4I6tq/K1SZFPTOtr/KBHBeksoGMGw==
```

> [!NOTE]
> klucz uwierzytelniania Hello obsługiwane przez emulator magazynu hello jest przeznaczona tylko dla testowania funkcji hello kodu uwierzytelniania klienta. Nie ma żadnych celów zabezpieczeń. Nie można używać konta magazynu w środowisku produkcyjnym i klucz hello emulatora magazynu. Nie należy używać konta programowanie hello z danymi produkcyjnymi.
> 
> emulator magazynu Hello obsługuje tylko połączenia za pośrednictwem protokołu HTTP. Jednak HTTPS jest hello zalecane protokół do dostępu do zasobów w sieci produkcyjnej kontem magazynu platformy Azure.
> 

#### <a name="connect-toohello-emulator-account-using-a-shortcut"></a>Połącz toohello emulatora konta przy użyciu skrótu
Hello Najprostszym sposobem tooconnect toohello emulatora magazynu z poziomu aplikacji jest tooconfigure parametry połączenia w pliku konfiguracji aplikacji, który odwołuje się skrót hello `UseDevelopmentStorage=true`. Oto przykład emulatora magazynu połączenia ciąg toohello w *app.config* pliku: 

```xml
<appSettings>
  <add key="StorageConnectionString" value="UseDevelopmentStorage=true" />
</appSettings>
```

#### <a name="connect-toohello-emulator-account-using-hello-well-known-account-name-and-key"></a>Połącz toohello emulatora konta przy użyciu hello dobrze znaną nazwę konta i klucz
toocreate ciąg połączenia, czy odwołania hello emulatora nazwę konta i klucza, należy określić hello punktów końcowych dla każdego z hello możesz usług ma toouse z emulatora hello w parametrach połączenia hello. Jest to konieczne, tak aby parametry połączenia hello będzie odwoływać się do punktów końcowych emulatora hello, które są inne niż konto magazynu w środowisku produkcyjnym. Na przykład hello wartość parametrów połączenia będzie wyglądać następująco:

```
DefaultEndpointsProtocol=http;AccountName=devstoreaccount1;
AccountKey=Eby8vdM02xNOcqFlqUwJPLlmEtlCDXJ1OUzFT50uSRZ6IFsuFq2UVErCz4I6tq/K1SZFPTOtr/KBHBeksoGMGw==;
BlobEndpoint=http://127.0.0.1:10000/devstoreaccount1;
TableEndpoint=http://127.0.0.1:10002/devstoreaccount1;
QueueEndpoint=http://127.0.0.1:10001/devstoreaccount1;
```

Ta wartość jest skrót identyczne toohello przedstawionych powyżej, `UseDevelopmentStorage=true`.

#### <a name="specify-an-http-proxy"></a>Określ serwer proxy HTTP
Podczas testowania usługi przed hello emulatora magazynu, można również określić toouse serwera proxy HTTP. Może to być przydatne do obserwacji żądań i odpowiedzi HTTP podczas debugujesz operacji względem hello usług magazynu. toospecify serwer proxy, Dodaj hello `DevelopmentStorageProxyUri` opcję toohello ciąg połączenia i ustaw jej wartość toohello identyfikatora URI serwera proxy. Na przykład poniżej przedstawiono parametry połączenia, które wskazuje toohello emulatora magazynu i konfiguruje serwer proxy HTTP:

```
UseDevelopmentStorage=true;DevelopmentStorageProxyUri=http://myProxyUri
```

