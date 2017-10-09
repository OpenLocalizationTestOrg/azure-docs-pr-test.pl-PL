<span data-ttu-id="0e32a-101">Aplikacje .NET mogą używać hello **programie StackExchange.Redis** pamięci podręcznej klienta, które można skonfigurować w programie Visual Studio przy użyciu pakietu NuGet, który upraszcza konfigurację hello aplikacje w pamięci podręcznej klienta.</span><span class="sxs-lookup"><span data-stu-id="0e32a-101">.NET applications can use hello **StackExchange.Redis** cache client, which can be configured in Visual Studio using a NuGet package that simplifies hello configuration of cache client applications.</span></span> 

> [!NOTE]
> <span data-ttu-id="0e32a-102">Aby uzyskać więcej informacji, zobacz hello [programie StackExchange.Redis](http://github.com/StackExchange/StackExchange.Redis) github strony i hello [programie StackExchange.Redis pamięci podręcznej klienta dokumentacji](http://github.com/StackExchange/StackExchange.Redis#documentation).</span><span class="sxs-lookup"><span data-stu-id="0e32a-102">For more information, see hello [StackExchange.Redis](http://github.com/StackExchange/StackExchange.Redis) github page and  hello [StackExchange.Redis cache client documentation](http://github.com/StackExchange/StackExchange.Redis#documentation).</span></span>
> 
> 

<span data-ttu-id="0e32a-103">tooconfigure aplikacji klienckiej w programie Visual Studio przy użyciu hello pakietu NuGet w programie StackExchange.Redis, kliknij prawym przyciskiem myszy projekt hello w **Eksploratora rozwiązań** i wybierz polecenie **Zarządzaj pakietami NuGet**.</span><span class="sxs-lookup"><span data-stu-id="0e32a-103">tooconfigure a client application in Visual Studio using hello StackExchange.Redis NuGet package, right-click hello project in **Solution Explorer** and choose **Manage NuGet Packages**.</span></span> 

![Zarządzanie pakietami NuGet](media/redis-cache-configure-stackexchange-redis-nuget/redis-cache-manage-nuget-menu.png)

<span data-ttu-id="0e32a-105">Typ **programie StackExchange.Redis** lub **StackExchange.Redis.StrongName** w polu tekstowym wyszukiwania hello, wybierz hello żądanej wersji z hello wyników, a następnie kliknij przycisk **zainstalować**.</span><span class="sxs-lookup"><span data-stu-id="0e32a-105">Type **StackExchange.Redis** or **StackExchange.Redis.StrongName** into hello search text box, select hello desired version from hello results, and click **Install**.</span></span>

> [!NOTE]
> <span data-ttu-id="0e32a-106">Jeśli wolisz toouse o silnych nazwach wersji hello **programie StackExchange.Redis** biblioteki klienta, wybierz **StackExchange.Redis.StrongName**; w przeciwnym razie wybierz **programie StackExchange.Redis**.</span><span class="sxs-lookup"><span data-stu-id="0e32a-106">If you prefer toouse a strong-named version of hello **StackExchange.Redis** client library, choose **StackExchange.Redis.StrongName**; otherwise choose **StackExchange.Redis**.</span></span>
> 
> 

![Pakiet NuGet StackExchange.Redis](media/redis-cache-configure-stackexchange-redis-nuget/redis-cache-stackexchange-redis.png)

<span data-ttu-id="0e32a-108">Witaj NuGet pakietu pliki do pobrania i dodaje hello jest wymagany odwołania do zestawów z tooaccess aplikacja klienta pamięci podręcznej Redis Azure z hello programie StackExchange.Redis pamięci podręcznej klienta.</span><span class="sxs-lookup"><span data-stu-id="0e32a-108">hello NuGet package downloads and adds hello required assembly references for your client application tooaccess Azure Redis Cache with hello StackExchange.Redis cache client.</span></span>

> [!NOTE]
> <span data-ttu-id="0e32a-109">Jeśli wcześniej skonfigurowano toouse Twojego projektu programie StackExchange.Redis, możesz sprawdzić dostępność aktualizacji pakietu toohello z hello **Menedżera pakietów NuGet**.</span><span class="sxs-lookup"><span data-stu-id="0e32a-109">If you have previously configured your project toouse StackExchange.Redis, you can check for updates toohello package from hello **NuGet Package Manager**.</span></span> <span data-ttu-id="0e32a-110">toocheck dla i zainstaluj zaktualizowane wersje hello pakietu NuGet w programie StackExchange.Redis, kliknij przycisk **aktualizacje** w hello hello **Menedżera pakietów NuGet** okna.</span><span class="sxs-lookup"><span data-stu-id="0e32a-110">toocheck for and install updated versions of hello StackExchange.Redis NuGet package, click **Updates** in hello hello **NuGet Package Manager** window.</span></span> <span data-ttu-id="0e32a-111">Jeśli toohello aktualizacji pakietu NuGet w programie StackExchange.Redis jest dostępny, należy zaktualizować wersja hello zaktualizowane toouse projektu.</span><span class="sxs-lookup"><span data-stu-id="0e32a-111">If an update toohello StackExchange.Redis NuGet package is available, you can update your project toouse hello updated version.</span></span>
> 
> 

<span data-ttu-id="0e32a-112">Można także zainstalować pakiet NuGet w programie StackExchange.Redis hello, klikając **Menedżera pakietów NuGet**, **Konsola Menedżera pakietów** z hello **narzędzia** menu i hello uruchomione następujące polecenie z hello **Konsola Menedżera pakietów** okna.</span><span class="sxs-lookup"><span data-stu-id="0e32a-112">You can also install hello StackExchange.Redis NuGet package by clicking **NuGet Package Manager**, **Package Manager Console** from hello **Tools** menu, and running hello following command from hello **Package Manager Console** window.</span></span>
    
```
Install-Package StackExchange.Redis
```
