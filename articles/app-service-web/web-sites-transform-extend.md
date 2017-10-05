---
title: "Zaawansowana konfiguracja i rozszerzenia aplikacji sieci web usługi aplikacji Azure"
description: "Użyj deklaracji Transformation(XDT) dokument XML, aby przekształcić plik ApplicationHost.config w aplikacji sieci web w usłudze Azure App Service i dodać prywatnych rozszerzeń w celu zezwolenia na akcje niestandardowe administracji."
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
ms.openlocfilehash: 314d3a954e712b829e7cf5eb37b23b31670f976b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="azure-app-service-web-app-advanced-config-and-extensions"></a>Zaawansowana konfiguracja i rozszerzenia aplikacji sieci web usługi aplikacji Azure
Za pomocą [transformacji dokumentów XML](http://msdn.microsoft.com/library/dd465326.aspx) deklaracje (XDT) można przekształcać [ApplicationHost.config](http://www.iis.net/learn/get-started/planning-your-iis-architecture/introduction-to-applicationhostconfig) plik w aplikacji sieci web w usłudze Azure App Service. Deklaracje XDT umożliwia również dodać prywatnych rozszerzeń w celu zezwolenia na akcje administracyjnej aplikacji sieci web niestandardowego. Ten artykuł zawiera rozszerzenia aplikacji sieci web PHP Manager próbki, który umożliwia zarządzanie ustawień PHP za pomocą interfejsu sieci web.

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a id="transform"></a>Konfiguracja zaawansowana przy użyciu pliku ApplicationHost.config
Usługi aplikacji platformy zapewnia elastyczność i kontrola konfiguracji aplikacji sieci web. Chociaż standardowego pliku konfiguracji ApplicationHost.config usług IIS nie jest dostępne do bezpośredniej edycji w usłudze App Service, platformy obsługuje deklaratywne model przekształcenia ApplicationHost.config oparte na transformacji dokumentów XML (XDT).

Aby korzystać z tej funkcji przekształcenia, Utwórz plik ApplicationHost.xdt z XDT zawartości i umieścić w obszarze katalogu głównego witryny (d:\home\site) w [konsoli Kudu](https://github.com/projectkudu/kudu/wiki/Kudu-console). Może być konieczne ponowne uruchomienie aplikacji sieci Web, aby zmiany zaczęły obowiązywać.

W poniższym przykładzie applicationHost.xdt pokazano, jak dodać nową zmienną środowiskową niestandardowej aplikacji sieci web, która używa PHP 5.4.

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

Plik dziennika z stanu przekształcania aplikacji i szczegółów jest dostępna z katalogu głównego FTP, w obszarze LogFiles\Transform.

Aby uzyskać dodatkowe przykłady, zobacz [https://github.com/projectkudu/kudu/wiki/Xdt-transform-samples](https://github.com/projectkudu/kudu/wiki/Xdt-transform-samples).

**Uwaga**<br />
Elementy na liście modułów w obszarze `system.webServer` nie można usunąć ani zmienić kolejności, ale możliwe jest dodawanie do listy.

## <a id="extend"></a>Rozszerzenie aplikacji sieci web
### <a id="overview"></a>Omówienie rozszerzeń aplikacji sieci web prywatnych
Usługi aplikacji obsługuje rozszerzenia aplikacji sieci web jako punkt rozszerzeń dla czynności administracyjnych. W rzeczywistości niektóre usługi aplikacji — funkcje platformy są zaimplementowane jako wstępnie zainstalowane rozszerzenia. Gdy nie można zmodyfikować rozszerzenia platformy wstępnie zainstalowane, można tworzyć i konfigurować prywatne rozszerzenia aplikacji sieci web. Ta funkcja opiera się również w deklaracjach XDT. Kluczowe kroki tworzenia rozszerzenia aplikacji sieci web prywatne są następujące:

1. Rozszerzenie aplikacji sieci Web **zawartości**: tworzenie dowolnej aplikacji sieci web obsługiwane przez usługę App Service
2. Rozszerzenie aplikacji sieci Web **deklaracji**: Utwórz plik ApplicationHost.xdt
3. Rozszerzenie aplikacji sieci Web **wdrożenia**: umieścić w folderze SiteExtensions w zawartości`root`

Łączy wewnętrznych aplikacji sieci web powinny wskazywać ścieżkę względem ścieżki aplikacji określone w pliku ApplicationHost.xdt. Każda zmiana pliku ApplicationHost.xdt wymaga ponownego uruchomienia aplikacji sieci web.

**Uwaga**: dodatkowe informacje dla tych elementów klucza są dostępne pod adresem [https://github.com/projectkudu/kudu/wiki/Azure-Site-Extensions](https://github.com/projectkudu/kudu/wiki/Azure-Site-Extensions).

Szczegółowy przykład znajduje się w celu zilustrowania kroki tworzenia i włączania rozszerzenia aplikacji sieci web prywatnych. Można pobrać kodu źródłowego, na przykład PHP Manager, który jest zgodny z [https://github.com/projectkudu/PHPManager](https://github.com/projectkudu/PHPManager).

### <a id="SiteSample"></a>Przykład rozszerzenia aplikacji sieci Web: PHP Manager
PHP Manager to rozszerzenie aplikacji sieci web, który umożliwia aplikacji administratorom łatwe wyświetlanie i konfigurowanie ustawień PHP, przy użyciu interfejsu sieci web zamiast bezpośrednio modyfikować pliki .ini PHP sieci web. Wspólne pliki konfiguracji dla programu PHP obejmują pliku php.ini, znajduje się w obszarze Program Files i. plik user.ini znajdujący się w katalogu głównym aplikacji sieci web. Ponieważ plik php.ini nie jest edytowalny bezpośrednio z usługi aplikacji platformy, rozszerzenie PHP Manager używa. user.ini pliku w celu zastosowania zmian ustawień.

#### <a id="PHPwebapp"></a>Aplikacja sieci web PHP Manager
Poniżej przedstawiono strony głównej wdrożenia PHP Manager:

![TransformSitePHPUI][TransformSitePHPUI]

Jak widać, rozszerzenia aplikacji sieci web jest tak samo jak aplikacji sieci web regularnych, ale z plikiem ApplicationHost.xdt dodatkowe umieszczony w folderze głównym aplikacji sieci web (więcej informacji o pliku ApplicationHost.xdt są dostępne w następnej sekcji tego artykułu).

Rozszerzenia PHP Manager został utworzony przy użyciu szablonu programu Visual Studio ASP.NET MVC 4 sieci Web aplikacji. Następujący widok w Eksploratorze rozwiązań pokazuje strukturę rozszerzenia PHP Manager.

![TransformSiteSolEx][TransformSiteSolEx]

Tylko specjalne logiki umożliwiającej we/wy pliku jest wskaż, gdzie znajduje się w katalogu wwwroot aplikacji sieci web. Jak pokazano w poniższym przykładzie kodu, zmiennej środowiskowej "HOME" oznacza ścieżkę katalogu głównego aplikacji sieci web, a ścieżka wwwroot można utworzyć przez dodanie "site\wwwroot":

```csharp
/// <summary>
/// Gives the location of the .user.ini file, even if one doesn't exist yet
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


Po ścieżce katalogu, umożliwia zwykły plik operacji We/Wy odczytu i zapisu do plików.

Jeden punkt ostrożność z rozszerzeń aplikacji sieci web odniesieniu do obsługi łączy wewnętrznych.  Jeśli masz łącza w plikach HTML, które zapewniają ścieżki bezwzględne łącza wewnętrzne w aplikacji sieci web, musisz zapewnić, że te łącza jest dołączany na początku nazwą rozszerzenia jako katalogu głównym. Jest to niezbędne, ponieważ główny dla rozszerzenia jest teraz "/`[your-extension-name]`/" zamiast są tylko "/", dlatego dowolny wewnętrzny łącza należy zaktualizować odpowiednio. Na przykład załóżmy, że kod zawiera łącze do następującego:

`"<a href="/Home/Settings">PHP Settings</a>"`

Gdy łącze jest częścią rozszerzenia aplikacji sieci web, link musi być w następującym formacie:

`"<a href="/[your-site-name]/Home/Settings">Settings</a>"`

To wymaganie można obejść przez albo przy użyciu tylko ścieżek względnych w aplikacji sieci web lub w przypadku aplikacji ASP.NET przy użyciu `@Html.ActionLink` metodę, która tworzy linki odpowiednie dla Ciebie.

#### <a id="XDT"></a>Plik applicationHost.xdt
Kod rozszerzenia aplikacji sieci web przechodzi w obszarze %HOME%\SiteExtensions\[your Nazwa rozszerzenia]. Zadzwonimy to katalog główny rozszerzenia.  

Aby zarejestrować rozszerzenie aplikacji sieci web przy użyciu pliku applicationHost.config, należy umieścić plik o nazwie ApplicationHost.xdt w folderze głównym rozszerzenia. Zawartość pliku ApplicationHost.xdt powinna być następująca:

```xml
<?xml version="1.0"?>
<configuration xmlns:xdt="http://schemas.microsoft.com/XML-Document-Transform">
  <system.applicationHost>
    <sites>
      <site name="%XDT_SCMSITENAME%" xdt:Locator="Match(name)">
        <!-- NOTE: Add your extension name in the application paths below -->
        <application path="/[your-extension-name]" xdt:Locator="Match(path)" xdt:Transform="Remove" />
        <application path="/[your-extension-name]" applicationPool="%XDT_APPPOOLNAME%" xdt:Transform="Insert">
          <virtualDirectory path="/" physicalPath="%XDT_EXTENSIONPATH%" />
        </application>
      </site>
    </sites>
  </system.applicationHost>
</configuration>
```

Nazwa wybranego jako nazwę rozszerzenia powinien mieć taką samą nazwę jak folder główny rozszerzenia.

Skutkuje to dodanie nowej ścieżki aplikacji do `system.applicationHost` listę witryn w witrynie SCM. Lokacja SCM jest punkt końcowy administracji w lokacji z poświadczeniami dostępu określone. Ma adres URL `https://[your-site-name].scm.azurewebsites.net`.  

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
      <!-- Note the custom changes that go here -->
      <application path="/[your-extension-name]" applicationPool="[your-website]">
        <virtualDirectory path="/" physicalPath="C:\DWASFiles\Sites\[your-website]\VirtualDirectory0\SiteExtensions\[your-extension-name]" />
      </application>
    </site>
  </sites>
  ... 
</system.applicationHost>
```

### <a id="deploy"></a>Wdrażanie rozszerzenia aplikacji sieci Web
Aby zainstalować rozszerzenia aplikacji sieci web, umożliwia FTP skopiuj wszystkie pliki aplikacji sieci web w taki sposób, aby `\SiteExtensions\[your-extension-name]` folderu, na którym chcesz zainstalować rozszerzenia aplikacji sieci web.  Pamiętaj skopiować plik ApplicationHost.xdt do tej lokalizacji również. Ponownie uruchom aplikację sieci web, aby włączyć rozszerzenie.

Można wyświetlić rozszerzenie aplikacji sieci web na:

`https://[your-site-name].scm.azurewebsites.net/[your-extension-name]`

Należy pamiętać, że adres URL wygląda podobnie jak adres URL dla aplikacji sieci web, z wyjątkiem tego, który używa protokołu HTTPS i zawiera ".scm".

Istnieje możliwość wyłączyć wszystkie prywatne rozszerzenia (nie wstępnie zainstalowane) dla aplikacji sieci web podczas projektowania i badania przez dodawanie ustawień aplikacji z kluczem `WEBSITE_PRIVATE_EXTENSIONS` i wartości `0`.

> [!NOTE]
> Jeśli chcesz zacząć korzystać z usługi Azure App Service przed utworzeniem konta platformy Azure, przejdź do artykułu [Try App Service](https://azure.microsoft.com/try/app-service/) (Wypróbuj usługę App Service), w którym wyjaśniono, jak od razu utworzyć początkową aplikację sieci Web o krótkim okresie istnienia w usłudze App Service. Bez kart kredytowych i bez zobowiązań.
> 
> 

## <a name="whats-changed"></a>Co zostało zmienione
* Przewodnik dotyczący przejścia od usługi Witryny sieci Web do usługi App Service można znaleźć w temacie [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714) (Usługa Azure App Service i jej wpływ na istniejące usługi platformy Azure).

<!-- IMAGES -->
[TransformSitePHPUI]: ./media/web-sites-transform-extend/TransformSitePHPUI.png
[TransformSiteSolEx]: ./media/web-sites-transform-extend/TransformSiteSolEx.png

