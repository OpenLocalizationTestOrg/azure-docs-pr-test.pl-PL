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
# <a name="azure-app-service-web-app-advanced-config-and-extensions"></a><span data-ttu-id="5e17c-103">Zaawansowana konfiguracja i rozszerzenia aplikacji sieci web usługi aplikacji Azure</span><span class="sxs-lookup"><span data-stu-id="5e17c-103">Azure App Service web app advanced config and extensions</span></span>
<span data-ttu-id="5e17c-104">Za pomocą [transformacji dokumentów XML](http://msdn.microsoft.com/library/dd465326.aspx) deklaracje (XDT) można przekształcać [ApplicationHost.config](http://www.iis.net/learn/get-started/planning-your-iis-architecture/introduction-to-applicationhostconfig) plik w aplikacji sieci web w usłudze Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="5e17c-104">By using [XML Document Transformation](http://msdn.microsoft.com/library/dd465326.aspx) (XDT) declarations, you can transform the [ApplicationHost.config](http://www.iis.net/learn/get-started/planning-your-iis-architecture/introduction-to-applicationhostconfig) file in your web app in Azure App Service.</span></span> <span data-ttu-id="5e17c-105">Deklaracje XDT umożliwia również dodać prywatnych rozszerzeń w celu zezwolenia na akcje administracyjnej aplikacji sieci web niestandardowego.</span><span class="sxs-lookup"><span data-stu-id="5e17c-105">You can also use XDT declarations to add private extensions to enable custom web app administration actions.</span></span> <span data-ttu-id="5e17c-106">Ten artykuł zawiera rozszerzenia aplikacji sieci web PHP Manager próbki, który umożliwia zarządzanie ustawień PHP za pomocą interfejsu sieci web.</span><span class="sxs-lookup"><span data-stu-id="5e17c-106">This article includes a sample PHP Manager web app extension that enables management of PHP settings through a web interface.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <span data-ttu-id="5e17c-107"><a id="transform"></a>Konfiguracja zaawansowana przy użyciu pliku ApplicationHost.config</span><span class="sxs-lookup"><span data-stu-id="5e17c-107"><a id="transform"></a>Advanced configuration through ApplicationHost.config</span></span>
<span data-ttu-id="5e17c-108">Usługi aplikacji platformy zapewnia elastyczność i kontrola konfiguracji aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="5e17c-108">The App Service platform provides flexibility and control for web app configuration.</span></span> <span data-ttu-id="5e17c-109">Chociaż standardowego pliku konfiguracji ApplicationHost.config usług IIS nie jest dostępne do bezpośredniej edycji w usłudze App Service, platformy obsługuje deklaratywne model przekształcenia ApplicationHost.config oparte na transformacji dokumentów XML (XDT).</span><span class="sxs-lookup"><span data-stu-id="5e17c-109">Although the standard IIS ApplicationHost.config configuration file is not available for direct editing in App Service, the platform supports a declarative ApplicationHost.config transform model based on XML Document Transformation (XDT).</span></span>

<span data-ttu-id="5e17c-110">Aby korzystać z tej funkcji przekształcenia, Utwórz plik ApplicationHost.xdt z XDT zawartości i umieścić w obszarze katalogu głównego witryny (d:\home\site) w [konsoli Kudu](https://github.com/projectkudu/kudu/wiki/Kudu-console).</span><span class="sxs-lookup"><span data-stu-id="5e17c-110">To leverage this transform functionality, you create an ApplicationHost.xdt file with XDT content and place under the site root (d:\home\site) in the [Kudu Console](https://github.com/projectkudu/kudu/wiki/Kudu-console).</span></span> <span data-ttu-id="5e17c-111">Może być konieczne ponowne uruchomienie aplikacji sieci Web, aby zmiany zaczęły obowiązywać.</span><span class="sxs-lookup"><span data-stu-id="5e17c-111">You may need to restart the Web App for changes to take effect.</span></span>

<span data-ttu-id="5e17c-112">W poniższym przykładzie applicationHost.xdt pokazano, jak dodać nową zmienną środowiskową niestandardowej aplikacji sieci web, która używa PHP 5.4.</span><span class="sxs-lookup"><span data-stu-id="5e17c-112">The following applicationHost.xdt sample shows how to add a new custom environment variable to a web app that uses PHP 5.4.</span></span>

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

<span data-ttu-id="5e17c-113">Plik dziennika z stanu przekształcania aplikacji i szczegółów jest dostępna z katalogu głównego FTP, w obszarze LogFiles\Transform.</span><span class="sxs-lookup"><span data-stu-id="5e17c-113">A log file with transform status and details is available from the FTP root under LogFiles\Transform.</span></span>

<span data-ttu-id="5e17c-114">Aby uzyskać dodatkowe przykłady, zobacz [https://github.com/projectkudu/kudu/wiki/Xdt-transform-samples](https://github.com/projectkudu/kudu/wiki/Xdt-transform-samples).</span><span class="sxs-lookup"><span data-stu-id="5e17c-114">For additional samples, see [https://github.com/projectkudu/kudu/wiki/Xdt-transform-samples](https://github.com/projectkudu/kudu/wiki/Xdt-transform-samples).</span></span>

<span data-ttu-id="5e17c-115">**Uwaga**</span><span class="sxs-lookup"><span data-stu-id="5e17c-115">**Note**</span></span><br />
<span data-ttu-id="5e17c-116">Elementy na liście modułów w obszarze `system.webServer` nie można usunąć ani zmienić kolejności, ale możliwe jest dodawanie do listy.</span><span class="sxs-lookup"><span data-stu-id="5e17c-116">Elements from the list of modules under `system.webServer` cannot be removed or reordered, but additions to the list are possible.</span></span>

## <span data-ttu-id="5e17c-117"><a id="extend"></a>Rozszerzenie aplikacji sieci web</span><span class="sxs-lookup"><span data-stu-id="5e17c-117"><a id="extend"></a> Extend your web app</span></span>
### <span data-ttu-id="5e17c-118"><a id="overview"></a>Omówienie rozszerzeń aplikacji sieci web prywatnych</span><span class="sxs-lookup"><span data-stu-id="5e17c-118"><a id="overview"></a> Overview of private web app extensions</span></span>
<span data-ttu-id="5e17c-119">Usługi aplikacji obsługuje rozszerzenia aplikacji sieci web jako punkt rozszerzeń dla czynności administracyjnych.</span><span class="sxs-lookup"><span data-stu-id="5e17c-119">App Service supports web app extensions as an extensibility point for administrative actions.</span></span> <span data-ttu-id="5e17c-120">W rzeczywistości niektóre usługi aplikacji — funkcje platformy są zaimplementowane jako wstępnie zainstalowane rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="5e17c-120">In fact, some App Service platform features are implemented as pre-installed extensions.</span></span> <span data-ttu-id="5e17c-121">Gdy nie można zmodyfikować rozszerzenia platformy wstępnie zainstalowane, można tworzyć i konfigurować prywatne rozszerzenia aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="5e17c-121">While the pre-installed platform extensions cannot be modified, you can create and configure private extensions for your own web app.</span></span> <span data-ttu-id="5e17c-122">Ta funkcja opiera się również w deklaracjach XDT.</span><span class="sxs-lookup"><span data-stu-id="5e17c-122">This functionality also relies on XDT declarations.</span></span> <span data-ttu-id="5e17c-123">Kluczowe kroki tworzenia rozszerzenia aplikacji sieci web prywatne są następujące:</span><span class="sxs-lookup"><span data-stu-id="5e17c-123">The key steps for creating a private web app extension are the following:</span></span>

1. <span data-ttu-id="5e17c-124">Rozszerzenie aplikacji sieci Web **zawartości**: tworzenie dowolnej aplikacji sieci web obsługiwane przez usługę App Service</span><span class="sxs-lookup"><span data-stu-id="5e17c-124">Web app extension **content**: create any web application supported by App Service</span></span>
2. <span data-ttu-id="5e17c-125">Rozszerzenie aplikacji sieci Web **deklaracji**: Utwórz plik ApplicationHost.xdt</span><span class="sxs-lookup"><span data-stu-id="5e17c-125">Web app extension **declaration**: create an ApplicationHost.xdt file</span></span>
3. <span data-ttu-id="5e17c-126">Rozszerzenie aplikacji sieci Web **wdrożenia**: umieścić w folderze SiteExtensions w zawartości`root`</span><span class="sxs-lookup"><span data-stu-id="5e17c-126">Web app extension **deployment**: place content in the SiteExtensions folder under `root`</span></span>

<span data-ttu-id="5e17c-127">Łączy wewnętrznych aplikacji sieci web powinny wskazywać ścieżkę względem ścieżki aplikacji określone w pliku ApplicationHost.xdt.</span><span class="sxs-lookup"><span data-stu-id="5e17c-127">Internal links for the web app should point to a path relative to the application path specified in the ApplicationHost.xdt file.</span></span> <span data-ttu-id="5e17c-128">Każda zmiana pliku ApplicationHost.xdt wymaga ponownego uruchomienia aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="5e17c-128">Any change to the ApplicationHost.xdt file requires a web app recycle.</span></span>

<span data-ttu-id="5e17c-129">**Uwaga**: dodatkowe informacje dla tych elementów klucza są dostępne pod adresem [https://github.com/projectkudu/kudu/wiki/Azure-Site-Extensions](https://github.com/projectkudu/kudu/wiki/Azure-Site-Extensions).</span><span class="sxs-lookup"><span data-stu-id="5e17c-129">**Note**: Additional information for these key elements is available at [https://github.com/projectkudu/kudu/wiki/Azure-Site-Extensions](https://github.com/projectkudu/kudu/wiki/Azure-Site-Extensions).</span></span>

<span data-ttu-id="5e17c-130">Szczegółowy przykład znajduje się w celu zilustrowania kroki tworzenia i włączania rozszerzenia aplikacji sieci web prywatnych.</span><span class="sxs-lookup"><span data-stu-id="5e17c-130">A detailed example is included to illustrate the steps for creating and enabling a private web app extension.</span></span> <span data-ttu-id="5e17c-131">Można pobrać kodu źródłowego, na przykład PHP Manager, który jest zgodny z [https://github.com/projectkudu/PHPManager](https://github.com/projectkudu/PHPManager).</span><span class="sxs-lookup"><span data-stu-id="5e17c-131">The source code for the PHP Manager example that follows can be downloaded from [https://github.com/projectkudu/PHPManager](https://github.com/projectkudu/PHPManager).</span></span>

### <span data-ttu-id="5e17c-132"><a id="SiteSample"></a>Przykład rozszerzenia aplikacji sieci Web: PHP Manager</span><span class="sxs-lookup"><span data-stu-id="5e17c-132"><a id="SiteSample"></a> Web app extension example: PHP Manager</span></span>
<span data-ttu-id="5e17c-133">PHP Manager to rozszerzenie aplikacji sieci web, który umożliwia aplikacji administratorom łatwe wyświetlanie i konfigurowanie ustawień PHP, przy użyciu interfejsu sieci web zamiast bezpośrednio modyfikować pliki .ini PHP sieci web.</span><span class="sxs-lookup"><span data-stu-id="5e17c-133">PHP Manager is a web app extension that allows web app administrators to easily view and configure their PHP settings using a web interface instead of having to modify PHP .ini files directly.</span></span> <span data-ttu-id="5e17c-134">Wspólne pliki konfiguracji dla programu PHP obejmują pliku php.ini, znajduje się w obszarze Program Files i. plik user.ini znajdujący się w katalogu głównym aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="5e17c-134">Common configuration files for PHP include the php.ini file located under Program Files and the .user.ini file located in the root folder of your web app.</span></span> <span data-ttu-id="5e17c-135">Ponieważ plik php.ini nie jest edytowalny bezpośrednio z usługi aplikacji platformy, rozszerzenie PHP Manager używa. user.ini pliku w celu zastosowania zmian ustawień.</span><span class="sxs-lookup"><span data-stu-id="5e17c-135">Since the php.ini file is not directly editable on the App Service platform, the PHP Manager extension uses the .user.ini file to apply setting changes.</span></span>

#### <span data-ttu-id="5e17c-136"><a id="PHPwebapp"></a>Aplikacja sieci web PHP Manager</span><span class="sxs-lookup"><span data-stu-id="5e17c-136"><a id="PHPwebapp"></a> The PHP Manager web application</span></span>
<span data-ttu-id="5e17c-137">Poniżej przedstawiono strony głównej wdrożenia PHP Manager:</span><span class="sxs-lookup"><span data-stu-id="5e17c-137">The following is the home page of the PHP Manager deployment:</span></span>

![TransformSitePHPUI][TransformSitePHPUI]

<span data-ttu-id="5e17c-139">Jak widać, rozszerzenia aplikacji sieci web jest tak samo jak aplikacji sieci web regularnych, ale z plikiem ApplicationHost.xdt dodatkowe umieszczony w folderze głównym aplikacji sieci web (więcej informacji o pliku ApplicationHost.xdt są dostępne w następnej sekcji tego artykułu).</span><span class="sxs-lookup"><span data-stu-id="5e17c-139">As you can see, a web app extension is just like a regular web application, but with an additional ApplicationHost.xdt file placed in the root folder of the web app (more details about the ApplicationHost.xdt file are available in the next section of this article).</span></span>

<span data-ttu-id="5e17c-140">Rozszerzenia PHP Manager został utworzony przy użyciu szablonu programu Visual Studio ASP.NET MVC 4 sieci Web aplikacji.</span><span class="sxs-lookup"><span data-stu-id="5e17c-140">The PHP Manager extension was created using the Visual Studio ASP.NET MVC 4 Web Application template.</span></span> <span data-ttu-id="5e17c-141">Następujący widok w Eksploratorze rozwiązań pokazuje strukturę rozszerzenia PHP Manager.</span><span class="sxs-lookup"><span data-stu-id="5e17c-141">The following view from Solution Explorer shows the structure of the PHP Manager extension.</span></span>

![TransformSiteSolEx][TransformSiteSolEx]

<span data-ttu-id="5e17c-143">Tylko specjalne logiki umożliwiającej we/wy pliku jest wskaż, gdzie znajduje się w katalogu wwwroot aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="5e17c-143">The only special logic needed for file I/O is to indicate where the wwwroot directory of the web app is located.</span></span> <span data-ttu-id="5e17c-144">Jak pokazano w poniższym przykładzie kodu, zmiennej środowiskowej "HOME" oznacza ścieżkę katalogu głównego aplikacji sieci web, a ścieżka wwwroot można utworzyć przez dodanie "site\wwwroot":</span><span class="sxs-lookup"><span data-stu-id="5e17c-144">As the following code example shows, the environment variable "HOME" indicates the web app's root path, and the wwwroot path can be constructed by appending "site\wwwroot":</span></span>

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


<span data-ttu-id="5e17c-145">Po ścieżce katalogu, umożliwia zwykły plik operacji We/Wy odczytu i zapisu do plików.</span><span class="sxs-lookup"><span data-stu-id="5e17c-145">After you have the directory path, you can use regular file I/O operations to read and write to files.</span></span>

<span data-ttu-id="5e17c-146">Jeden punkt ostrożność z rozszerzeń aplikacji sieci web odniesieniu do obsługi łączy wewnętrznych.</span><span class="sxs-lookup"><span data-stu-id="5e17c-146">One point of caution with web app extensions regards the handling of internal links.</span></span>  <span data-ttu-id="5e17c-147">Jeśli masz łącza w plikach HTML, które zapewniają ścieżki bezwzględne łącza wewnętrzne w aplikacji sieci web, musisz zapewnić, że te łącza jest dołączany na początku nazwą rozszerzenia jako katalogu głównym.</span><span class="sxs-lookup"><span data-stu-id="5e17c-147">If you have any links in your HTML files that give absolute paths to internal links on your web app, you must ensure those links are prepended with your extension name as your root.</span></span> <span data-ttu-id="5e17c-148">Jest to niezbędne, ponieważ główny dla rozszerzenia jest teraz "/`[your-extension-name]`/" zamiast są tylko "/", dlatego dowolny wewnętrzny łącza należy zaktualizować odpowiednio.</span><span class="sxs-lookup"><span data-stu-id="5e17c-148">This is needed because the root for your extension is now "/`[your-extension-name]`/" rather than being just "/", so any internal links must be updated accordingly.</span></span> <span data-ttu-id="5e17c-149">Na przykład załóżmy, że kod zawiera łącze do następującego:</span><span class="sxs-lookup"><span data-stu-id="5e17c-149">For example, suppose your code includes a link to the following:</span></span>

`"<a href="/Home/Settings">PHP Settings</a>"`

<span data-ttu-id="5e17c-150">Gdy łącze jest częścią rozszerzenia aplikacji sieci web, link musi być w następującym formacie:</span><span class="sxs-lookup"><span data-stu-id="5e17c-150">When the link is part of a web app extension, the link must be in the following form:</span></span>

`"<a href="/[your-site-name]/Home/Settings">Settings</a>"`

<span data-ttu-id="5e17c-151">To wymaganie można obejść przez albo przy użyciu tylko ścieżek względnych w aplikacji sieci web lub w przypadku aplikacji ASP.NET przy użyciu `@Html.ActionLink` metodę, która tworzy linki odpowiednie dla Ciebie.</span><span class="sxs-lookup"><span data-stu-id="5e17c-151">You can work around this requirement by either using only relative paths within your web application, or in the case of ASP.NET applications, by using the `@Html.ActionLink` method which creates the appropriate links for you.</span></span>

#### <span data-ttu-id="5e17c-152"><a id="XDT"></a>Plik applicationHost.xdt</span><span class="sxs-lookup"><span data-stu-id="5e17c-152"><a id="XDT"></a> The applicationHost.xdt file</span></span>
<span data-ttu-id="5e17c-153">Kod rozszerzenia aplikacji sieci web przechodzi w obszarze %HOME%\SiteExtensions\[your Nazwa rozszerzenia].</span><span class="sxs-lookup"><span data-stu-id="5e17c-153">The code for your web app extension goes under %HOME%\SiteExtensions\[your-extension-name].</span></span> <span data-ttu-id="5e17c-154">Zadzwonimy to katalog główny rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="5e17c-154">We'll call this the extension root.</span></span>  

<span data-ttu-id="5e17c-155">Aby zarejestrować rozszerzenie aplikacji sieci web przy użyciu pliku applicationHost.config, należy umieścić plik o nazwie ApplicationHost.xdt w folderze głównym rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="5e17c-155">To register your web app extension with the applicationHost.config file, you need to place a file called ApplicationHost.xdt in the extension root.</span></span> <span data-ttu-id="5e17c-156">Zawartość pliku ApplicationHost.xdt powinna być następująca:</span><span class="sxs-lookup"><span data-stu-id="5e17c-156">The content of the ApplicationHost.xdt file should be as follows:</span></span>

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

<span data-ttu-id="5e17c-157">Nazwa wybranego jako nazwę rozszerzenia powinien mieć taką samą nazwę jak folder główny rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="5e17c-157">The name you select as your extension name should have the same name as your extension root folder.</span></span>

<span data-ttu-id="5e17c-158">Skutkuje to dodanie nowej ścieżki aplikacji do `system.applicationHost` listę witryn w witrynie SCM.</span><span class="sxs-lookup"><span data-stu-id="5e17c-158">This has the effect of adding a new application path to the `system.applicationHost` sites list under the SCM site.</span></span> <span data-ttu-id="5e17c-159">Lokacja SCM jest punkt końcowy administracji w lokacji z poświadczeniami dostępu określone.</span><span class="sxs-lookup"><span data-stu-id="5e17c-159">The SCM site is a site administration end point with specific access credentials.</span></span> <span data-ttu-id="5e17c-160">Ma adres URL `https://[your-site-name].scm.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="5e17c-160">It has the URL `https://[your-site-name].scm.azurewebsites.net`.</span></span>  

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

### <span data-ttu-id="5e17c-161"><a id="deploy"></a>Wdrażanie rozszerzenia aplikacji sieci Web</span><span class="sxs-lookup"><span data-stu-id="5e17c-161"><a id="deploy"></a> Web app extension deployment</span></span>
<span data-ttu-id="5e17c-162">Aby zainstalować rozszerzenia aplikacji sieci web, umożliwia FTP skopiuj wszystkie pliki aplikacji sieci web w taki sposób, aby `\SiteExtensions\[your-extension-name]` folderu, na którym chcesz zainstalować rozszerzenia aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="5e17c-162">To install your web app extension, you can use FTP to copy all the files of your web application to the `\SiteExtensions\[your-extension-name]` folder of the web app on which you want to install the extension.</span></span>  <span data-ttu-id="5e17c-163">Pamiętaj skopiować plik ApplicationHost.xdt do tej lokalizacji również.</span><span class="sxs-lookup"><span data-stu-id="5e17c-163">Be sure to copy the ApplicationHost.xdt file to this location as well.</span></span> <span data-ttu-id="5e17c-164">Ponownie uruchom aplikację sieci web, aby włączyć rozszerzenie.</span><span class="sxs-lookup"><span data-stu-id="5e17c-164">Restart your web app to enable the extension.</span></span>

<span data-ttu-id="5e17c-165">Można wyświetlić rozszerzenie aplikacji sieci web na:</span><span class="sxs-lookup"><span data-stu-id="5e17c-165">You should be able to see your web app extension at:</span></span>

`https://[your-site-name].scm.azurewebsites.net/[your-extension-name]`

<span data-ttu-id="5e17c-166">Należy pamiętać, że adres URL wygląda podobnie jak adres URL dla aplikacji sieci web, z wyjątkiem tego, który używa protokołu HTTPS i zawiera ".scm".</span><span class="sxs-lookup"><span data-stu-id="5e17c-166">Note that the URL looks just like the URL for your web app, except that it uses HTTPS and contains ".scm".</span></span>

<span data-ttu-id="5e17c-167">Istnieje możliwość wyłączyć wszystkie prywatne rozszerzenia (nie wstępnie zainstalowane) dla aplikacji sieci web podczas projektowania i badania przez dodawanie ustawień aplikacji z kluczem `WEBSITE_PRIVATE_EXTENSIONS` i wartości `0`.</span><span class="sxs-lookup"><span data-stu-id="5e17c-167">It is possible to disable all private (not pre-installed) extensions for your web app during development and investigations by adding an app settings with the key `WEBSITE_PRIVATE_EXTENSIONS` and a value of `0`.</span></span>

> [!NOTE]
> <span data-ttu-id="5e17c-168">Jeśli chcesz zacząć korzystać z usługi Azure App Service przed utworzeniem konta platformy Azure, przejdź do artykułu [Try App Service](https://azure.microsoft.com/try/app-service/) (Wypróbuj usługę App Service), w którym wyjaśniono, jak od razu utworzyć początkową aplikację sieci Web o krótkim okresie istnienia w usłudze App Service.</span><span class="sxs-lookup"><span data-stu-id="5e17c-168">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="5e17c-169">Bez kart kredytowych i bez zobowiązań.</span><span class="sxs-lookup"><span data-stu-id="5e17c-169">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="whats-changed"></a><span data-ttu-id="5e17c-170">Co zostało zmienione</span><span class="sxs-lookup"><span data-stu-id="5e17c-170">What's changed</span></span>
* <span data-ttu-id="5e17c-171">Przewodnik dotyczący przejścia od usługi Witryny sieci Web do usługi App Service można znaleźć w temacie [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714) (Usługa Azure App Service i jej wpływ na istniejące usługi platformy Azure).</span><span class="sxs-lookup"><span data-stu-id="5e17c-171">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!-- IMAGES -->
[TransformSitePHPUI]: ./media/web-sites-transform-extend/TransformSitePHPUI.png
[TransformSiteSolEx]: ./media/web-sites-transform-extend/TransformSiteSolEx.png

