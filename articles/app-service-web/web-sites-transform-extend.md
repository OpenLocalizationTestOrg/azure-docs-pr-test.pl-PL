---
title: "aaaAzure aplikacji sieci web usługi aplikacji Zaawansowana konfiguracja i rozszerzenia"
description: "Użyj Transformation(XDT) dokumentu XML deklaracje tootransform hello plik ApplicationHost.config w usłudze Azure App Service sieci web aplikacji i tooadd prywatnych rozszerzeń tooenable administracji niestandardowe czynności użytkownika."
author: cephalin
writer: cephalin
editor: mollybos
manager: erikre
services: app-service
documentationcenter: 
ms.assetid: b441a286-ef38-4abc-b102-cdb249baf5bc
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/25/2016
ms.author: cephalin
ms.openlocfilehash: 873347ac13113d1ac989cba29128382c81dcfcca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-web-app-advanced-config-and-extensions"></a>Zaawansowana konfiguracja i rozszerzenia aplikacji sieci web usługi aplikacji Azure
Za pomocą [transformacji dokumentów XML](http://msdn.microsoft.com/library/dd465326.aspx) deklaracje (XDT) można przekształcać hello [ApplicationHost.config](http://www.iis.net/learn/get-started/planning-your-iis-architecture/introduction-to-applicationhostconfig) plik w aplikacji sieci web w usłudze Azure App Service. Umożliwia także XDT deklaracje tooadd prywatnych rozszerzeń tooenable niestandardowe sieci web aplikacji administracji akcje. Ten artykuł zawiera rozszerzenia aplikacji sieci web PHP Manager próbki, który umożliwia zarządzanie ustawień PHP za pomocą interfejsu sieci web.

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a id="transform"></a>Konfiguracja zaawansowana przy użyciu pliku ApplicationHost.config
Hello platformie App Service zapewnia elastyczność i kontrola konfiguracji aplikacji sieci web. Chociaż hello standardowego pliku konfiguracji ApplicationHost.config usług IIS nie jest dostępne do bezpośredniej edycji w usłudze App Service, hello platformy obsługuje deklaratywne model przekształcenia ApplicationHost.config oparte na transformacji dokumentów XML (XDT).

tooleverage tę funkcję przekształcenia należy utworzyć plik ApplicationHost.xdt z XDT zawartości i objęcia hello katalogu głównego witryny (d:\home\site) w hello [konsoli Kudu](https://github.com/projectkudu/kudu/wiki/Kudu-console). Witaj toorestart aplikacji sieci Web może być konieczne dla efektu tootake zmiany.

następujące przykładowe applicationHost.xdt Hello pokazuje, jak tooadd nowej zmiennej tooa niestandardowego środowiska sieci web aplikacji, który używa PHP 5.4.

```xml
<?xml version="1.0"?>
<configuration xmlns:xdt="http://schemas.microsoft.com/XML-Document-Transform">
  <system.webServer>
    <fastCgi>
      <application>
        <environmentVariables>
          <environmentVariable name="CONFIGTEST" value="TEST" xdt:Transform="Insert" xdt:Locator="XPath(/configuration/system.webServer/fastCgi/application[contains(@fullPath,'5.4')]/environmentVariables)" />
        </environmentVariables>
      </application>
    </fastCgi>
  </system.webServer>
</configuration>
```

Plik dziennika z stanu przekształcania aplikacji i szczegółów jest dostępny z głównego hello FTP w obszarze LogFiles\Transform.

Aby uzyskać dodatkowe przykłady, zobacz [https://github.com/projectkudu/kudu/wiki/Xdt-transform-samples](https://github.com/projectkudu/kudu/wiki/Xdt-transform-samples).

**Uwaga**<br />
Elementy z listy hello modułów w obszarze `system.webServer` nie można usunąć ani zmienić kolejności, ale dodatków toohello listy są możliwe.

## <a id="extend"></a>Rozszerzenie aplikacji sieci web
### <a id="overview"></a>Omówienie rozszerzeń aplikacji sieci web prywatnych
Usługi aplikacji obsługuje rozszerzenia aplikacji sieci web jako punkt rozszerzeń dla czynności administracyjnych. W rzeczywistości niektóre usługi aplikacji — funkcje platformy są zaimplementowane jako wstępnie zainstalowane rozszerzenia. Gdy hello platformy wstępnie zainstalowane rozszerzenia nie może być modyfikowany, można tworzyć i konfigurować prywatne rozszerzenia aplikacji sieci web. Ta funkcja opiera się również w deklaracjach XDT. Hello klucza kroki tworzenia rozszerzenia aplikacji sieci web prywatne są następujące hello:

1. Rozszerzenie aplikacji sieci Web **zawartości**: tworzenie dowolnej aplikacji sieci web obsługiwane przez usługę App Service
2. Rozszerzenie aplikacji sieci Web **deklaracji**: Utwórz plik ApplicationHost.xdt
3. Rozszerzenie aplikacji sieci Web **wdrożenia**: zawartość należy umieścić w folderze SiteExtensions hello w obszarze`root`

Łączy wewnętrznych dla aplikacji sieci web hello powinny wskazywać tooa ścieżki względnej toohello ścieżka aplikacji określone w pliku ApplicationHost.xdt hello. Dowolny plik ApplicationHost.xdt toohello zmiany wymaga ponownego uruchomienia aplikacji sieci web.

**Uwaga**: dodatkowe informacje dla tych elementów klucza są dostępne pod adresem [https://github.com/projectkudu/kudu/wiki/Azure-Site-Extensions](https://github.com/projectkudu/kudu/wiki/Azure-Site-Extensions).

Szczegółowy przykład jest dołączony tooillustrate hello kroki tworzenia i włączania rozszerzenia aplikacji sieci web prywatnych. Witaj kodu źródłowego, na przykład PHP Manager hello, sposób może zostać pobrany z [https://github.com/projectkudu/PHPManager](https://github.com/projectkudu/PHPManager).

### <a id="SiteSample"></a>Przykład rozszerzenia aplikacji sieci Web: PHP Manager
PHP Manager to rozszerzenie aplikacji sieci web, która pozwala administratorom aplikacji sieci web widoku tooeasily i konfigurowanie ustawień PHP, zamiast plików .ini PHP toomodify bezpośrednio przy użyciu interfejsu sieci web. Wspólne pliki konfiguracji dla programów PHP i dołączyć plik php.ini hello znajduje się w obszarze plików i programów hello. plik user.ini znajdujący się w folderze głównym hello aplikacji sieci web. Ponieważ plik php.ini hello nie jest edytowalny bezpośrednio na powitania usługi aplikacji platformy, hello rozszerzenia PHP Manager używa hello. user.ini tooapply plików, zmiany ustawień.

#### <a id="PHPwebapp"></a>Witaj aplikacji sieci web PHP Manager
strony głównej hello hello deployment PHP Manager jest następujący Hello:

![TransformSitePHPUI][TransformSitePHPUI]

Jak widać, rozszerzenia aplikacji sieci web jest tak samo jak aplikacji sieci web regularnych, ale z plikiem ApplicationHost.xdt dodatkowe umieszczony w folderze głównym hello (więcej informacji o pliku ApplicationHost.xdt hello są dostępne w następnej sekcji hello tej aplikacji sieci web hello artykuł).

Witaj rozszerzenia PHP Manager został utworzony przy użyciu szablonu programu Visual Studio ASP.NET MVC 4 sieci Web aplikacji hello. Witaj następujący widok w Eksploratorze rozwiązań pokazuje hello strukturę hello rozszerzenia PHP Manager.

![TransformSiteSolEx][TransformSiteSolEx]

Hello tylko specjalne potrzebne do We/Wy pliku jest tooindicate gdzie hello wwwroot hello aplikacji sieci web znajduje się katalog. Witaj poniższy kod przedstawia przykład Witaj zmiennej środowiskowej "HOME" wskazuje hello ścieżki katalogu głównego aplikacji sieci web, a ścieżka wwwroot hello można utworzyć przez dodanie "site\wwwroot":

```csharp
/// <summary>
/// Gives hello location of hello .user.ini file, even if one doesn't exist yet
/// </summary>
private static string GetUserSettingsFilePath()
{
  var rootPath = Environment.GetEnvironmentVariable("HOME"); // For use on Azure Websites
  if (rootPath == null)
  {
    rootPath = System.IO.Path.GetTempPath(); // For testing purposes
  };
  var userSettingsFile = Path.Combine(rootPath, @"site\wwwroot\.user.ini");
  return userSettingsFile;
}
```


Po umieszczeniu hello ścieżki katalogu, można użyć zwykły plik tooread operacji We/Wy i zapisać toofiles.

Jeden punkt ostrożność z rozszerzeń aplikacji sieci web traktuje hello obsługę łączy wewnętrznych.  Jeśli masz łącza w plikach HTML, które zapewniają ścieżki bezwzględne toointernal łącza w aplikacji sieci web, musisz zapewnić, że te łącza jest dołączany na początku nazwą rozszerzenia jako katalogu głównym. Jest to niezbędne, ponieważ główny powitania dla rozszerzenia jest teraz "/`[your-extension-name]`/" zamiast są tylko "/", dlatego dowolny wewnętrzny łącza należy zaktualizować odpowiednio. Na przykład załóżmy, że kod obejmuje następujące toohello łącza:

`"<a href="/Home/Settings">PHP Settings</a>"`

Łącze hello jest częścią rozszerzenia aplikacji sieci web, hello link musi należeć hello następującej postaci:

`"<a href="/[your-site-name]/Home/Settings">Settings</a>"`

To wymaganie można obejść przez przy użyciu tylko ścieżek względnych w aplikacji sieci web, lub hello wielkość liter w aplikacji ASP.NET przy użyciu hello `@Html.ActionLink` metodę, która tworzy hello odpowiednie łącza.

#### <a id="XDT"></a>Witaj applicationHost.xdt pliku
Kod powitania dla rozszerzenia aplikacji sieci web przechodzi w obszarze %HOME%\SiteExtensions\[your Nazwa rozszerzenia]. Zadzwonimy to katalog główny rozszerzenia hello.  

tooregister Twojego rozszerzenia aplikacji sieci web z pliku applicationHost.config hello należy tooplace plik o nazwie ApplicationHost.xdt hello rozszerzenia głównego. zawartość Hello hello ApplicationHost.xdt pliku powinna być następująca:

```xml
<?xml version="1.0"?>
<configuration xmlns:xdt="http://schemas.microsoft.com/XML-Document-Transform">
  <system.applicationHost>
    <sites>
      <site name="%XDT_SCMSITENAME%" xdt:Locator="Match(name)">
        <!-- NOTE: Add your extension name in hello application paths below -->
        <application path="/[your-extension-name]" xdt:Locator="Match(path)" xdt:Transform="Remove" />
        <application path="/[your-extension-name]" applicationPool="%XDT_APPPOOLNAME%" xdt:Transform="Insert">
          <virtualDirectory path="/" physicalPath="%XDT_EXTENSIONPATH%" />
        </application>
      </site>
    </sites>
  </system.applicationHost>
</configuration>
```

Nazwa Hello wybrana jako nazwę rozszerzenia powinien mieć hello sama nazwa jak folder główny rozszerzenia.

To ustawienie działa hello dodawania nowych toohello ścieżka aplikacji `system.applicationHost` listę witryn w witrynie SCM hello. lokacja SCM Hello jest punkt końcowy administracji w lokacji z poświadczeniami dostępu określone. Ma adres URL hello `https://[your-site-name].scm.azurewebsites.net`.  

```xml
<system.applicationHost>
  ...       
  <sites>
    <site name="~1[your-website]" id="1716402716">
      <bindings>
        <binding protocol="http" bindingInformation="*:80: [your-website].scm.azurewebsites.net" />
        <binding protocol="https" bindingInformation="*:443: [your-website].scm.azurewebsites.net" />
      </bindings>
      <traceFailedRequestsLogging enabled="false" directory="C:\DWASFiles\Sites\[your-website]\VirtualDirectory0\LogFiles" />
      <detailedErrorLogging enabled="false" directory="C:\DWASFiles\Sites\[your-website]\VirtualDirectory0\LogFiles\DetailedErrors" />
      <logFile logSiteId="false" />
      <application path="/" applicationPool="[your-website]">
        <virtualDirectory path="/" physicalPath="D:\Program Files (x86)\SiteExtensions\Kudu\1.24.20926.5" />
      </application>
      <!-- Note hello custom changes that go here -->
      <application path="/[your-extension-name]" applicationPool="[your-website]">
        <virtualDirectory path="/" physicalPath="C:\DWASFiles\Sites\[your-website]\VirtualDirectory0\SiteExtensions\[your-extension-name]" />
      </application>
    </site>
  </sites>
  ... 
</system.applicationHost>
```

### <a id="deploy"></a>Wdrażanie rozszerzenia aplikacji sieci Web
tooinstall rozszerzenie aplikacji sieci web, można użyć FTP toocopy wszystkie pliki hello toohello aplikacji sieci web `\SiteExtensions\[your-extension-name]` folderu hello aplikacji sieci web, na którym ma zostać tooinstall hello rozszerzenia.  Należy się toocopy hello ApplicationHost.xdt toothis lokalizację pliku również. Uruchom ponownie rozszerzenia hello tooenable aplikacji sieci web.

Powinny być możliwe toosee rozszerzenie aplikacji sieci web na:

`https://[your-site-name].scm.azurewebsites.net/[your-extension-name]`

Należy pamiętać, że powitalne adres URL wygląda tak hello adres URL dla aplikacji sieci web, z wyjątkiem tego, który używa protokołu HTTPS i zawiera ".scm".

Jest możliwe toodisable wszystkie prywatne (nie preinstalowanym) rozszerzenia aplikacji sieci web podczas projektowania i badania przez dodawanie ustawień aplikacji z kluczem hello `WEBSITE_PRIVATE_EXTENSIONS` i wartości `0`.

> [!NOTE]
> Tooget wprowadzenie do usługi Azure App Service przed utworzeniem konta platformy Azure, przejdź zbyt[Wypróbuj usługę App Service](https://azure.microsoft.com/try/app-service/), gdzie możesz od razu utworzyć krótkotrwałą, początkową aplikację sieci web w usłudze App Service. Bez kart kredytowych i bez zobowiązań.
> 
> 

## <a name="whats-changed"></a>Co zostało zmienione
* Toohello przewodnik zmiany z tooApp witryn sieci Web usługi dla: [usłudze Azure App Service i jej wpływ na istniejące usługi platformy Azure](http://go.microsoft.com/fwlink/?LinkId=529714)

<!-- IMAGES -->
[TransformSitePHPUI]: ./media/web-sites-transform-extend/TransformSitePHPUI.png
[TransformSiteSolEx]: ./media/web-sites-transform-extend/TransformSiteSolEx.png

