<span data-ttu-id="fd3b1-101">emulator magazynu Hello obsługuje jednego stałego konta i klucz uwierzytelniania dobrze znanego uwierzytelniania klucza wspólnego.</span><span class="sxs-lookup"><span data-stu-id="fd3b1-101">hello storage emulator supports a single fixed account and a well-known authentication key for Shared Key authentication.</span></span> <span data-ttu-id="fd3b1-102">Tego konta i klucz są hello dozwolone emulatorze magazynu hello tylko poświadczenia klucza wspólnego.</span><span class="sxs-lookup"><span data-stu-id="fd3b1-102">This account and key are hello only Shared Key credentials permitted for use with hello storage emulator.</span></span> <span data-ttu-id="fd3b1-103">Są to:</span><span class="sxs-lookup"><span data-stu-id="fd3b1-103">They are:</span></span>

```
Account name: devstoreaccount1
Account key: Eby8vdM02xNOcqFlqUwJPLlmEtlCDXJ1OUzFT50uSRZ6IFsuFq2UVErCz4I6tq/K1SZFPTOtr/KBHBeksoGMGw==
```

> [!NOTE]
> <span data-ttu-id="fd3b1-104">klucz uwierzytelniania Hello obsługiwane przez emulator magazynu hello jest przeznaczona tylko dla testowania funkcji hello kodu uwierzytelniania klienta.</span><span class="sxs-lookup"><span data-stu-id="fd3b1-104">hello authentication key supported by hello storage emulator is intended only for testing hello functionality of your client authentication code.</span></span> <span data-ttu-id="fd3b1-105">Nie ma żadnych celów zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="fd3b1-105">It does not serve any security purpose.</span></span> <span data-ttu-id="fd3b1-106">Nie można używać konta magazynu w środowisku produkcyjnym i klucz hello emulatora magazynu.</span><span class="sxs-lookup"><span data-stu-id="fd3b1-106">You cannot use your production storage account and key with hello storage emulator.</span></span> <span data-ttu-id="fd3b1-107">Nie należy używać konta programowanie hello z danymi produkcyjnymi.</span><span class="sxs-lookup"><span data-stu-id="fd3b1-107">You should not use hello development account with production data.</span></span>
> 
> <span data-ttu-id="fd3b1-108">emulator magazynu Hello obsługuje tylko połączenia za pośrednictwem protokołu HTTP.</span><span class="sxs-lookup"><span data-stu-id="fd3b1-108">hello storage emulator supports connection via HTTP only.</span></span> <span data-ttu-id="fd3b1-109">Jednak HTTPS jest hello zalecane protokół do dostępu do zasobów w sieci produkcyjnej kontem magazynu platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="fd3b1-109">However, HTTPS is hello recommended protocol for accessing resources in a production Azure storage account.</span></span>
> 

#### <a name="connect-toohello-emulator-account-using-a-shortcut"></a><span data-ttu-id="fd3b1-110">Połącz toohello emulatora konta przy użyciu skrótu</span><span class="sxs-lookup"><span data-stu-id="fd3b1-110">Connect toohello emulator account using a shortcut</span></span>
<span data-ttu-id="fd3b1-111">Hello Najprostszym sposobem tooconnect toohello emulatora magazynu z poziomu aplikacji jest tooconfigure parametry połączenia w pliku konfiguracji aplikacji, który odwołuje się skrót hello `UseDevelopmentStorage=true`.</span><span class="sxs-lookup"><span data-stu-id="fd3b1-111">hello easiest way tooconnect toohello storage emulator from your application is tooconfigure a connection string in your application's configuration file that references hello shortcut `UseDevelopmentStorage=true`.</span></span> <span data-ttu-id="fd3b1-112">Oto przykład emulatora magazynu połączenia ciąg toohello w *app.config* pliku:</span><span class="sxs-lookup"><span data-stu-id="fd3b1-112">Here's an example of a connection string toohello storage emulator in an *app.config* file:</span></span> 

```xml
<appSettings>
  <add key="StorageConnectionString" value="UseDevelopmentStorage=true" />
</appSettings>
```

#### <a name="connect-toohello-emulator-account-using-hello-well-known-account-name-and-key"></a><span data-ttu-id="fd3b1-113">Połącz toohello emulatora konta przy użyciu hello dobrze znaną nazwę konta i klucz</span><span class="sxs-lookup"><span data-stu-id="fd3b1-113">Connect toohello emulator account using hello well-known account name and key</span></span>
<span data-ttu-id="fd3b1-114">toocreate ciąg połączenia, czy odwołania hello emulatora nazwę konta i klucza, należy określić hello punktów końcowych dla każdego z hello możesz usług ma toouse z emulatora hello w parametrach połączenia hello.</span><span class="sxs-lookup"><span data-stu-id="fd3b1-114">toocreate a connection string that references hello emulator account name and key, you must specify hello endpoints for each of hello services you wish toouse from hello emulator in hello connection string.</span></span> <span data-ttu-id="fd3b1-115">Jest to konieczne, tak aby parametry połączenia hello będzie odwoływać się do punktów końcowych emulatora hello, które są inne niż konto magazynu w środowisku produkcyjnym.</span><span class="sxs-lookup"><span data-stu-id="fd3b1-115">This is necessary so that hello connection string will reference hello emulator endpoints, which are different than those for a production storage account.</span></span> <span data-ttu-id="fd3b1-116">Na przykład hello wartość parametrów połączenia będzie wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="fd3b1-116">For example, hello value of your connection string will look like this:</span></span>

```
DefaultEndpointsProtocol=http;AccountName=devstoreaccount1;
AccountKey=Eby8vdM02xNOcqFlqUwJPLlmEtlCDXJ1OUzFT50uSRZ6IFsuFq2UVErCz4I6tq/K1SZFPTOtr/KBHBeksoGMGw==;
BlobEndpoint=http://127.0.0.1:10000/devstoreaccount1;
TableEndpoint=http://127.0.0.1:10002/devstoreaccount1;
QueueEndpoint=http://127.0.0.1:10001/devstoreaccount1;
```

<span data-ttu-id="fd3b1-117">Ta wartość jest skrót identyczne toohello przedstawionych powyżej, `UseDevelopmentStorage=true`.</span><span class="sxs-lookup"><span data-stu-id="fd3b1-117">This value is identical toohello shortcut shown above, `UseDevelopmentStorage=true`.</span></span>

#### <a name="specify-an-http-proxy"></a><span data-ttu-id="fd3b1-118">Określ serwer proxy HTTP</span><span class="sxs-lookup"><span data-stu-id="fd3b1-118">Specify an HTTP proxy</span></span>
<span data-ttu-id="fd3b1-119">Podczas testowania usługi przed hello emulatora magazynu, można również określić toouse serwera proxy HTTP.</span><span class="sxs-lookup"><span data-stu-id="fd3b1-119">You can also specify an HTTP proxy toouse when you're testing your service against hello storage emulator.</span></span> <span data-ttu-id="fd3b1-120">Może to być przydatne do obserwacji żądań i odpowiedzi HTTP podczas debugujesz operacji względem hello usług magazynu.</span><span class="sxs-lookup"><span data-stu-id="fd3b1-120">This can be useful for observing HTTP requests and responses while you're debugging operations against hello storage services.</span></span> <span data-ttu-id="fd3b1-121">toospecify serwer proxy, Dodaj hello `DevelopmentStorageProxyUri` opcję toohello ciąg połączenia i ustaw jej wartość toohello identyfikatora URI serwera proxy.</span><span class="sxs-lookup"><span data-stu-id="fd3b1-121">toospecify a proxy, add hello `DevelopmentStorageProxyUri` option toohello connection string, and set its value toohello proxy URI.</span></span> <span data-ttu-id="fd3b1-122">Na przykład poniżej przedstawiono parametry połączenia, które wskazuje toohello emulatora magazynu i konfiguruje serwer proxy HTTP:</span><span class="sxs-lookup"><span data-stu-id="fd3b1-122">For example, here is a connection string that points toohello storage emulator and configures an HTTP proxy:</span></span>

```
UseDevelopmentStorage=true;DevelopmentStorageProxyUri=http://myProxyUri
```

