<span data-ttu-id="ee71b-101">Emulator magazynu obsługuje jednego stałego konta i klucz uwierzytelniania dobrze znanego uwierzytelniania klucza wspólnego.</span><span class="sxs-lookup"><span data-stu-id="ee71b-101">The storage emulator supports a single fixed account and a well-known authentication key for Shared Key authentication.</span></span> <span data-ttu-id="ee71b-102">Tego konta i klucz są dozwolone w emulatorze magazynu tylko poświadczenia klucza wspólnego.</span><span class="sxs-lookup"><span data-stu-id="ee71b-102">This account and key are the only Shared Key credentials permitted for use with the storage emulator.</span></span> <span data-ttu-id="ee71b-103">Są to:</span><span class="sxs-lookup"><span data-stu-id="ee71b-103">They are:</span></span>

```
Account name: devstoreaccount1
Account key: Eby8vdM02xNOcqFlqUwJPLlmEtlCDXJ1OUzFT50uSRZ6IFsuFq2UVErCz4I6tq/K1SZFPTOtr/KBHBeksoGMGw==
```

> [!NOTE]
> <span data-ttu-id="ee71b-104">Klucz uwierzytelniania obsługiwanych przez emulator magazynu jest przeznaczony tylko do celów testowych funkcje kodu uwierzytelniania klienta.</span><span class="sxs-lookup"><span data-stu-id="ee71b-104">The authentication key supported by the storage emulator is intended only for testing the functionality of your client authentication code.</span></span> <span data-ttu-id="ee71b-105">Nie ma żadnych celów zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="ee71b-105">It does not serve any security purpose.</span></span> <span data-ttu-id="ee71b-106">Nie można użyć konta magazynu w środowisku produkcyjnym i klucz w emulatorze magazynu.</span><span class="sxs-lookup"><span data-stu-id="ee71b-106">You cannot use your production storage account and key with the storage emulator.</span></span> <span data-ttu-id="ee71b-107">Nie należy używać konta programowanie z danymi produkcyjnymi.</span><span class="sxs-lookup"><span data-stu-id="ee71b-107">You should not use the development account with production data.</span></span>
> 
> <span data-ttu-id="ee71b-108">Emulator magazynu obsługuje tylko połączenia za pośrednictwem protokołu HTTP.</span><span class="sxs-lookup"><span data-stu-id="ee71b-108">The storage emulator supports connection via HTTP only.</span></span> <span data-ttu-id="ee71b-109">Jednak HTTPS to protokół zalecany do uzyskiwania dostępu do zasobów w sieci produkcyjnej kontem magazynu platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="ee71b-109">However, HTTPS is the recommended protocol for accessing resources in a production Azure storage account.</span></span>
> 

#### <a name="connect-to-the-emulator-account-using-a-shortcut"></a><span data-ttu-id="ee71b-110">Połącz się kontem emulatora przy użyciu skrótu</span><span class="sxs-lookup"><span data-stu-id="ee71b-110">Connect to the emulator account using a shortcut</span></span>
<span data-ttu-id="ee71b-111">Najprostszym sposobem nawiązać emulator magazynu z poziomu aplikacji jest skonfigurowanie parametrów połączenia w pliku konfiguracji aplikacji, która odwołuje się skrót `UseDevelopmentStorage=true`.</span><span class="sxs-lookup"><span data-stu-id="ee71b-111">The easiest way to connect to the storage emulator from your application is to configure a connection string in your application's configuration file that references the shortcut `UseDevelopmentStorage=true`.</span></span> <span data-ttu-id="ee71b-112">Oto przykład parametrów połączenia do emulatora magazynu w *app.config* pliku:</span><span class="sxs-lookup"><span data-stu-id="ee71b-112">Here's an example of a connection string to the storage emulator in an *app.config* file:</span></span> 

```xml
<appSettings>
  <add key="StorageConnectionString" value="UseDevelopmentStorage=true" />
</appSettings>
```

#### <a name="connect-to-the-emulator-account-using-the-well-known-account-name-and-key"></a><span data-ttu-id="ee71b-113">Połącz się kontem emulatora, korzystając z dobrze znaną nazwę konta i klucza</span><span class="sxs-lookup"><span data-stu-id="ee71b-113">Connect to the emulator account using the well-known account name and key</span></span>
<span data-ttu-id="ee71b-114">Aby utworzyć parametry połączenia, które odwołuje się do emulatora nazwę konta i klucz, należy określić punkty końcowe dla każdej usługi, które mają być używane z emulatora w parametrach połączenia.</span><span class="sxs-lookup"><span data-stu-id="ee71b-114">To create a connection string that references the emulator account name and key, you must specify the endpoints for each of the services you wish to use from the emulator in the connection string.</span></span> <span data-ttu-id="ee71b-115">Jest to konieczne, tak aby parametry połączenia będzie odwoływać się do emulatora punktów końcowych, które są inne niż konto magazynu w środowisku produkcyjnym.</span><span class="sxs-lookup"><span data-stu-id="ee71b-115">This is necessary so that the connection string will reference the emulator endpoints, which are different than those for a production storage account.</span></span> <span data-ttu-id="ee71b-116">Na przykład wartość parametrów połączenia będzie wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="ee71b-116">For example, the value of your connection string will look like this:</span></span>

```
DefaultEndpointsProtocol=http;AccountName=devstoreaccount1;
AccountKey=Eby8vdM02xNOcqFlqUwJPLlmEtlCDXJ1OUzFT50uSRZ6IFsuFq2UVErCz4I6tq/K1SZFPTOtr/KBHBeksoGMGw==;
BlobEndpoint=http://127.0.0.1:10000/devstoreaccount1;
TableEndpoint=http://127.0.0.1:10002/devstoreaccount1;
QueueEndpoint=http://127.0.0.1:10001/devstoreaccount1;
```

<span data-ttu-id="ee71b-117">Ta wartość jest taka sama jak pokazano powyżej, skrót `UseDevelopmentStorage=true`.</span><span class="sxs-lookup"><span data-stu-id="ee71b-117">This value is identical to the shortcut shown above, `UseDevelopmentStorage=true`.</span></span>

#### <a name="specify-an-http-proxy"></a><span data-ttu-id="ee71b-118">Określ serwer proxy HTTP</span><span class="sxs-lookup"><span data-stu-id="ee71b-118">Specify an HTTP proxy</span></span>
<span data-ttu-id="ee71b-119">Można również określić serwer proxy HTTP do użycia podczas testowania usługi przed emulatora magazynu.</span><span class="sxs-lookup"><span data-stu-id="ee71b-119">You can also specify an HTTP proxy to use when you're testing your service against the storage emulator.</span></span> <span data-ttu-id="ee71b-120">Może to być przydatne do obserwacji żądań i odpowiedzi HTTP podczas debugowania kodu operacji względem usługi magazynu.</span><span class="sxs-lookup"><span data-stu-id="ee71b-120">This can be useful for observing HTTP requests and responses while you're debugging operations against the storage services.</span></span> <span data-ttu-id="ee71b-121">Aby określić serwer proxy, Dodaj `DevelopmentStorageProxyUri` opcji w parametrach połączenia, a następnie ustaw dla niego wartość identyfikatora URI serwera proxy.</span><span class="sxs-lookup"><span data-stu-id="ee71b-121">To specify a proxy, add the `DevelopmentStorageProxyUri` option to the connection string, and set its value to the proxy URI.</span></span> <span data-ttu-id="ee71b-122">Na przykład poniżej przedstawiono parametry połączenia, które wskazuje emulator magazynu i konfiguruje serwer proxy HTTP:</span><span class="sxs-lookup"><span data-stu-id="ee71b-122">For example, here is a connection string that points to the storage emulator and configures an HTTP proxy:</span></span>

```
UseDevelopmentStorage=true;DevelopmentStorageProxyUri=http://myProxyUri
```

