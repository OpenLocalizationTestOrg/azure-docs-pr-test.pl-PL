Aplikacje .NET mogą używać hello **programie StackExchange.Redis** pamięci podręcznej klienta, które można skonfigurować w programie Visual Studio przy użyciu pakietu NuGet, który upraszcza konfigurację hello aplikacje w pamięci podręcznej klienta. 

> [!NOTE]
> Aby uzyskać więcej informacji, zobacz hello [programie StackExchange.Redis](http://github.com/StackExchange/StackExchange.Redis) github strony i hello [programie StackExchange.Redis pamięci podręcznej klienta dokumentacji](http://github.com/StackExchange/StackExchange.Redis#documentation).
> 
> 

tooconfigure aplikacji klienckiej w programie Visual Studio przy użyciu hello pakietu NuGet w programie StackExchange.Redis, kliknij prawym przyciskiem myszy projekt hello w **Eksploratora rozwiązań** i wybierz polecenie **Zarządzaj pakietami NuGet**. 

![Zarządzanie pakietami NuGet](media/redis-cache-configure-stackexchange-redis-nuget/redis-cache-manage-nuget-menu.png)

Typ **programie StackExchange.Redis** lub **StackExchange.Redis.StrongName** w polu tekstowym wyszukiwania hello, wybierz hello żądanej wersji z hello wyników, a następnie kliknij przycisk **zainstalować**.

> [!NOTE]
> Jeśli wolisz toouse o silnych nazwach wersji hello **programie StackExchange.Redis** biblioteki klienta, wybierz **StackExchange.Redis.StrongName**; w przeciwnym razie wybierz **programie StackExchange.Redis**.
> 
> 

![Pakiet NuGet StackExchange.Redis](media/redis-cache-configure-stackexchange-redis-nuget/redis-cache-stackexchange-redis.png)

Witaj NuGet pakietu pliki do pobrania i dodaje hello jest wymagany odwołania do zestawów z tooaccess aplikacja klienta pamięci podręcznej Redis Azure z hello programie StackExchange.Redis pamięci podręcznej klienta.

> [!NOTE]
> Jeśli wcześniej skonfigurowano toouse Twojego projektu programie StackExchange.Redis, możesz sprawdzić dostępność aktualizacji pakietu toohello z hello **Menedżera pakietów NuGet**. toocheck dla i zainstaluj zaktualizowane wersje hello pakietu NuGet w programie StackExchange.Redis, kliknij przycisk **aktualizacje** w hello hello **Menedżera pakietów NuGet** okna. Jeśli toohello aktualizacji pakietu NuGet w programie StackExchange.Redis jest dostępny, należy zaktualizować wersja hello zaktualizowane toouse projektu.
> 
> 

Można także zainstalować pakiet NuGet w programie StackExchange.Redis hello, klikając **Menedżera pakietów NuGet**, **Konsola Menedżera pakietów** z hello **narzędzia** menu i hello uruchomione następujące polecenie z hello **Konsola Menedżera pakietów** okna.
    
```
Install-Package StackExchange.Redis
```
