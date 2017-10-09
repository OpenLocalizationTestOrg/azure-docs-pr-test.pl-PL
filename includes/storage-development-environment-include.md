## <a name="set-up-your-development-environment"></a>Konfigurowanie środowiska projektowego
Następnie skonfiguruj środowiska deweloperskiego w Visual Studio, wszystko jest gotowe tootry przykłady kodu hello w tym przewodniku.

### <a name="create-a-windows-console-application-project"></a>Utwórz projekt aplikacji konsoli dla systemu Windows
W programie Visual Studio utwórz nową aplikację konsoli dla systemu Windows. Hello następujące kroki pokazują, jak toocreate aplikacji konsoli w programie Visual Studio 2017, jednak hello kroki są podobne w innych wersjach programu Visual Studio.

1. Wybierz kolejno pozycje **Plik** > **Nowy** > **Projekt**
2. Wybierz kolejno pozycje **Zainstalowane** > **Szablony** > **Visual C#** > **Klasyczny pulpit systemu Windows**
3. Wybierz pozycję **Aplikacja konsoli (.NET Framework)**
4. Wprowadź nazwę aplikacji w hello **Name:** pola
5. Kliknij przycisk **OK**

![Okno dialogowe tworzenia projektu w programie Visual Studio](./media/storage-development-environment-include/storage-development-environment-include-1.png)

Wszystkie przykłady kodu, w tym samouczku można dodać toohello `Main()` metody Aplikacja konsoli `Program.cs` pliku.

Można użyć hello biblioteki klienta magazynu Azure w dowolnego typu aplikacji .NET, w tym chmury Azure usługi lub aplikacji sieci web oraz aplikacje komputerów stacjonarnych i przenośnych. W tym przewodniku dla uproszczenia przedstawiono aplikację konsolową.

### <a name="use-nuget-tooinstall-hello-required-packages"></a>Korzystanie z pakietów hello wymagane tooinstall NuGet
Istnieją dwa pakiety tooreference toocomplete Twojego projektu musi w tym samouczku:

* [Biblioteka klienta usługi Microsoft Azure Storage dla platformy .NET](https://www.nuget.org/packages/WindowsAzure.Storage/): ten pakiet zapewnia dostęp programistyczny toodata zasobów na koncie magazynu.
* [Biblioteka programu Microsoft Azure Configuration Manager dla środowiska .NET](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/): ten pakiet zawiera klasę do analizowania parametrów połączenia w pliku konfiguracji, niezależnie od tego, gdzie została uruchomiona aplikacja.

Możesz użyć NuGet tooobtain oba pakiety. Wykonaj następujące kroki:

1. Kliknij projekt prawym przyciskiem myszy w **Eksploratorze rozwiązań** i wybierz polecenie **Zarządzaj pakietami NuGet**.
2. Wyszukaj w trybie online "Windowsazure.Storage", a następnie kliknij przycisk **zainstalować** tooinstall hello biblioteki klienta usługi Storage oraz jej zależności.
3. Wyszukaj w trybie online "WindowsAzure.ConfigurationManager", a następnie kliknij przycisk **zainstalować** tooinstall hello Azure Configuration Manager.

> [!NOTE]
> Pakiet biblioteki klienta usługi Storage Hello znajduje się również w hello [zestawu Azure SDK dla platformy .NET](https://azure.microsoft.com/downloads/). Firma Microsoft zaleca jednak również zainstalować hello biblioteki klienta usługi Storage z posiadanie najnowszej wersji biblioteki klienta hello hello tooensure NuGet.
> 
> zależności ODataLib Hello w hello biblioteki klienta usługi Storage dla platformy .NET są rozwiązywane przez pakiety ODataLib hello jest dostępne na NuGet, a nie z usługi danych WCF. Hello biblioteki ODataLib można pobrać bezpośrednio lub odwołuje się projekt kodu za pośrednictwem pakietu NuGet. Witaj określone pakiety ODataLib używane przez hello biblioteki klienta usługi Storage są [OData](http://nuget.org/packages/Microsoft.Data.OData/), [Edm](http://nuget.org/packages/Microsoft.Data.Edm/), i [przestrzennym](http://nuget.org/packages/System.Spatial/). Te biblioteki są używane przez klasy magazynu tabel Azure hello, są one wymaganymi zależnościami do programowania za pomocą hello biblioteki klienta usługi Storage.
> 
> 

### <a name="determine-your-target-environment"></a>Określanie środowiska docelowego
Masz dwie opcje środowiska uruchamiania hello przykłady w tym przewodniku:

* Można uruchomić kod dla konta usługi Azure Storage w chmurze hello. 
* Można uruchomić kod dla emulatora magazynu Azure hello. emulator magazynu Hello jest lokalnym środowiskiem, które emuluje konto usługi Azure Storage w chmurze hello. Witaj emulator jest bezpłatną opcją do testowania i debugowania kodu, gdy aplikacja jest w fazie projektowania. Witaj emulator używa dobrze znanego konta i klucz. Aby uzyskać więcej informacji, zobacz [hello Użyj emulatora magazynu Azure do programowania i testowania](../articles/storage/common/storage-use-emulator.md)

Jeśli ma być przeznaczona dla konta magazynu w chmurze hello, skopiuj hello podstawowy klucz dostępu dla konta magazynu z hello portalu Azure. Aby uzyskać więcej informacji, zobacz temat [View and copy storage access keys](../articles/storage/common/storage-create-storage-account.md#view-and-copy-storage-access-keys) (Wyświetlanie i kopiowanie kluczy dostępu kopiowania).

> [!NOTE]
> Możesz zastosować tooavoid emulatora magazynu hello ponoszenia kosztów związanych z usługą Azure Storage. Jednak jeśli tootarget konto usługi Azure storage w chmurze hello, koszty związane z wykonaniem tego samouczka będą nieznaczny.
> 
> 

### <a name="configure-your-storage-connection-string"></a>Konfigurowanie parametrów połączenia magazynu
Hello biblioteki klienta magazynu Azure dla platformy .NET obsługuje korzystanie z punktów końcowych tooconfigure magazynu połączenia ciągu i poświadczeń do uzyskiwania dostępu do usług magazynu. Witaj najlepsze sposób toomaintain parametry połączenia magazynu jest w pliku konfiguracji. 

Aby uzyskać więcej informacji dotyczących parametrów połączenia, zobacz [skonfigurować tooAzure parametry połączenia magazynu](../articles/storage/common/storage-configure-connection-string.md).

> [!NOTE]
> Klucz konta magazynu jest podobny toohello hasła głównego konta magazynu. Zawsze należy uważać tooprotect klucz konta magazynu. Unikaj dystrybucję tooother użytkowników, kodować je lub zapisać go w pliku tekstowego, który jest dostępny tooothers. Wygeneruj ponownie klucz za pośrednictwem hello portalu Azure, jeśli uważasz, że mogą zostać naruszone.
> 
> 

tooconfigure Twojego parametry połączenia, otwórz hello `app.config` plików w Eksploratorze rozwiązań w programie Visual Studio. Dodaj zawartość hello hello `<appSettings>` widocznego poniżej. Zastąp `account-name` hello nazwą konta magazynu i `account-key` kluczem dostępu do konta:

```xml
<configuration>
    <startup> 
        <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.5.2" />
    </startup>
    <appSettings>
        <add key="StorageConnectionString" value="DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key" />
    </appSettings>
</configuration>
```

Na przykład ustawienie konfiguracji może wyglądać mniej więcej tak:

```xml
<add key="StorageConnectionString" value="DefaultEndpointsProtocol=https;AccountName=storagesample;AccountKey=GMuzNHjlB3S9itqZJHHCnRkrokLkcSyW7yK9BRbGp0ENePunLPwBgpxV1Z/pVo9zpem/2xSHXkMqTHHLcx8XRA==" />
```

emulator magazynu hello tootarget, można użyć skrótu klawiaturowego, który mapuje toohello dobrze znaną nazwę konta i klucz. W takim przypadku ustawienie parametrów połączenia wygląda następująco:

```xml
<add key="StorageConnectionString" value="UseDevelopmentStorage=true;" />
```

