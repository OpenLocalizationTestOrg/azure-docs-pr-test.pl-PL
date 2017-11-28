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
# <a name="azure-app-service-web-app-advanced-config-and-extensions"></a><span data-ttu-id="96ea8-103">Zaawansowana konfiguracja i rozszerzenia aplikacji sieci web usługi aplikacji Azure</span><span class="sxs-lookup"><span data-stu-id="96ea8-103">Azure App Service web app advanced config and extensions</span></span>
<span data-ttu-id="96ea8-104">Za pomocą [transformacji dokumentów XML](http://msdn.microsoft.com/library/dd465326.aspx) deklaracje (XDT) można przekształcać hello [ApplicationHost.config](http://www.iis.net/learn/get-started/planning-your-iis-architecture/introduction-to-applicationhostconfig) plik w aplikacji sieci web w usłudze Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="96ea8-104">By using [XML Document Transformation](http://msdn.microsoft.com/library/dd465326.aspx) (XDT) declarations, you can transform hello [ApplicationHost.config](http://www.iis.net/learn/get-started/planning-your-iis-architecture/introduction-to-applicationhostconfig) file in your web app in Azure App Service.</span></span> <span data-ttu-id="96ea8-105">Umożliwia także XDT deklaracje tooadd prywatnych rozszerzeń tooenable niestandardowe sieci web aplikacji administracji akcje.</span><span class="sxs-lookup"><span data-stu-id="96ea8-105">You can also use XDT declarations tooadd private extensions tooenable custom web app administration actions.</span></span> <span data-ttu-id="96ea8-106">Ten artykuł zawiera rozszerzenia aplikacji sieci web PHP Manager próbki, który umożliwia zarządzanie ustawień PHP za pomocą interfejsu sieci web.</span><span class="sxs-lookup"><span data-stu-id="96ea8-106">This article includes a sample PHP Manager web app extension that enables management of PHP settings through a web interface.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <span data-ttu-id="96ea8-107"><a id="transform"></a>Konfiguracja zaawansowana przy użyciu pliku ApplicationHost.config</span><span class="sxs-lookup"><span data-stu-id="96ea8-107"><a id="transform"></a>Advanced configuration through ApplicationHost.config</span></span>
<span data-ttu-id="96ea8-108">Hello platformie App Service zapewnia elastyczność i kontrola konfiguracji aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="96ea8-108">hello App Service platform provides flexibility and control for web app configuration.</span></span> <span data-ttu-id="96ea8-109">Chociaż hello standardowego pliku konfiguracji ApplicationHost.config usług IIS nie jest dostępne do bezpośredniej edycji w usłudze App Service, hello platformy obsługuje deklaratywne model przekształcenia ApplicationHost.config oparte na transformacji dokumentów XML (XDT).</span><span class="sxs-lookup"><span data-stu-id="96ea8-109">Although hello standard IIS ApplicationHost.config configuration file is not available for direct editing in App Service, hello platform supports a declarative ApplicationHost.config transform model based on XML Document Transformation (XDT).</span></span>

<span data-ttu-id="96ea8-110">tooleverage tę funkcję przekształcenia należy utworzyć plik ApplicationHost.xdt z XDT zawartości i objęcia hello katalogu głównego witryny (d:\home\site) w hello [konsoli Kudu](https://github.com/projectkudu/kudu/wiki/Kudu-console).</span><span class="sxs-lookup"><span data-stu-id="96ea8-110">tooleverage this transform functionality, you create an ApplicationHost.xdt file with XDT content and place under hello site root (d:\home\site) in hello [Kudu Console](https://github.com/projectkudu/kudu/wiki/Kudu-console).</span></span> <span data-ttu-id="96ea8-111">Witaj toorestart aplikacji sieci Web może być konieczne dla efektu tootake zmiany.</span><span class="sxs-lookup"><span data-stu-id="96ea8-111">You may need toorestart hello Web App for changes tootake effect.</span></span>

<span data-ttu-id="96ea8-112">następujące przykładowe applicationHost.xdt Hello pokazuje, jak tooadd nowej zmiennej tooa niestandardowego środowiska sieci web aplikacji, który używa PHP 5.4.</span><span class="sxs-lookup"><span data-stu-id="96ea8-112">hello following applicationHost.xdt sample shows how tooadd a new custom environment variable tooa web app that uses PHP 5.4.</span></span>

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

<span data-ttu-id="96ea8-113">Plik dziennika z stanu przekształcania aplikacji i szczegółów jest dostępny z głównego hello FTP w obszarze LogFiles\Transform.</span><span class="sxs-lookup"><span data-stu-id="96ea8-113">A log file with transform status and details is available from hello FTP root under LogFiles\Transform.</span></span>

<span data-ttu-id="96ea8-114">Aby uzyskać dodatkowe przykłady, zobacz [https://github.com/projectkudu/kudu/wiki/Xdt-transform-samples](https://github.com/projectkudu/kudu/wiki/Xdt-transform-samples).</span><span class="sxs-lookup"><span data-stu-id="96ea8-114">For additional samples, see [https://github.com/projectkudu/kudu/wiki/Xdt-transform-samples](https://github.com/projectkudu/kudu/wiki/Xdt-transform-samples).</span></span>

<span data-ttu-id="96ea8-115">**Uwaga**</span><span class="sxs-lookup"><span data-stu-id="96ea8-115">**Note**</span></span><br />
<span data-ttu-id="96ea8-116">Elementy z listy hello modułów w obszarze `system.webServer` nie można usunąć ani zmienić kolejności, ale dodatków toohello listy są możliwe.</span><span class="sxs-lookup"><span data-stu-id="96ea8-116">Elements from hello list of modules under `system.webServer` cannot be removed or reordered, but additions toohello list are possible.</span></span>

## <span data-ttu-id="96ea8-117"><a id="extend"></a>Rozszerzenie aplikacji sieci web</span><span class="sxs-lookup"><span data-stu-id="96ea8-117"><a id="extend"></a> Extend your web app</span></span>
### <span data-ttu-id="96ea8-118"><a id="overview"></a>Omówienie rozszerzeń aplikacji sieci web prywatnych</span><span class="sxs-lookup"><span data-stu-id="96ea8-118"><a id="overview"></a> Overview of private web app extensions</span></span>
<span data-ttu-id="96ea8-119">Usługi aplikacji obsługuje rozszerzenia aplikacji sieci web jako punkt rozszerzeń dla czynności administracyjnych.</span><span class="sxs-lookup"><span data-stu-id="96ea8-119">App Service supports web app extensions as an extensibility point for administrative actions.</span></span> <span data-ttu-id="96ea8-120">W rzeczywistości niektóre usługi aplikacji — funkcje platformy są zaimplementowane jako wstępnie zainstalowane rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="96ea8-120">In fact, some App Service platform features are implemented as pre-installed extensions.</span></span> <span data-ttu-id="96ea8-121">Gdy hello platformy wstępnie zainstalowane rozszerzenia nie może być modyfikowany, można tworzyć i konfigurować prywatne rozszerzenia aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="96ea8-121">While hello pre-installed platform extensions cannot be modified, you can create and configure private extensions for your own web app.</span></span> <span data-ttu-id="96ea8-122">Ta funkcja opiera się również w deklaracjach XDT.</span><span class="sxs-lookup"><span data-stu-id="96ea8-122">This functionality also relies on XDT declarations.</span></span> <span data-ttu-id="96ea8-123">Hello klucza kroki tworzenia rozszerzenia aplikacji sieci web prywatne są następujące hello:</span><span class="sxs-lookup"><span data-stu-id="96ea8-123">hello key steps for creating a private web app extension are hello following:</span></span>

1. <span data-ttu-id="96ea8-124">Rozszerzenie aplikacji sieci Web **zawartości**: tworzenie dowolnej aplikacji sieci web obsługiwane przez usługę App Service</span><span class="sxs-lookup"><span data-stu-id="96ea8-124">Web app extension **content**: create any web application supported by App Service</span></span>
2. <span data-ttu-id="96ea8-125">Rozszerzenie aplikacji sieci Web **deklaracji**: Utwórz plik ApplicationHost.xdt</span><span class="sxs-lookup"><span data-stu-id="96ea8-125">Web app extension **declaration**: create an ApplicationHost.xdt file</span></span>
3. <span data-ttu-id="96ea8-126">Rozszerzenie aplikacji sieci Web **wdrożenia**: zawartość należy umieścić w folderze SiteExtensions hello w obszarze`root`</span><span class="sxs-lookup"><span data-stu-id="96ea8-126">Web app extension **deployment**: place content in hello SiteExtensions folder under `root`</span></span>

<span data-ttu-id="96ea8-127">Łączy wewnętrznych dla aplikacji sieci web hello powinny wskazywać tooa ścieżki względnej toohello ścieżka aplikacji określone w pliku ApplicationHost.xdt hello.</span><span class="sxs-lookup"><span data-stu-id="96ea8-127">Internal links for hello web app should point tooa path relative toohello application path specified in hello ApplicationHost.xdt file.</span></span> <span data-ttu-id="96ea8-128">Dowolny plik ApplicationHost.xdt toohello zmiany wymaga ponownego uruchomienia aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="96ea8-128">Any change toohello ApplicationHost.xdt file requires a web app recycle.</span></span>

<span data-ttu-id="96ea8-129">**Uwaga**: dodatkowe informacje dla tych elementów klucza są dostępne pod adresem [https://github.com/projectkudu/kudu/wiki/Azure-Site-Extensions](https://github.com/projectkudu/kudu/wiki/Azure-Site-Extensions).</span><span class="sxs-lookup"><span data-stu-id="96ea8-129">**Note**: Additional information for these key elements is available at [https://github.com/projectkudu/kudu/wiki/Azure-Site-Extensions](https://github.com/projectkudu/kudu/wiki/Azure-Site-Extensions).</span></span>

<span data-ttu-id="96ea8-130">Szczegółowy przykład jest dołączony tooillustrate hello kroki tworzenia i włączania rozszerzenia aplikacji sieci web prywatnych.</span><span class="sxs-lookup"><span data-stu-id="96ea8-130">A detailed example is included tooillustrate hello steps for creating and enabling a private web app extension.</span></span> <span data-ttu-id="96ea8-131">Witaj kodu źródłowego, na przykład PHP Manager hello, sposób może zostać pobrany z [https://github.com/projectkudu/PHPManager](https://github.com/projectkudu/PHPManager).</span><span class="sxs-lookup"><span data-stu-id="96ea8-131">hello source code for hello PHP Manager example that follows can be downloaded from [https://github.com/projectkudu/PHPManager](https://github.com/projectkudu/PHPManager).</span></span>

### <span data-ttu-id="96ea8-132"><a id="SiteSample"></a>Przykład rozszerzenia aplikacji sieci Web: PHP Manager</span><span class="sxs-lookup"><span data-stu-id="96ea8-132"><a id="SiteSample"></a> Web app extension example: PHP Manager</span></span>
<span data-ttu-id="96ea8-133">PHP Manager to rozszerzenie aplikacji sieci web, która pozwala administratorom aplikacji sieci web widoku tooeasily i konfigurowanie ustawień PHP, zamiast plików .ini PHP toomodify bezpośrednio przy użyciu interfejsu sieci web.</span><span class="sxs-lookup"><span data-stu-id="96ea8-133">PHP Manager is a web app extension that allows web app administrators tooeasily view and configure their PHP settings using a web interface instead of having toomodify PHP .ini files directly.</span></span> <span data-ttu-id="96ea8-134">Wspólne pliki konfiguracji dla programów PHP i dołączyć plik php.ini hello znajduje się w obszarze plików i programów hello. plik user.ini znajdujący się w folderze głównym hello aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="96ea8-134">Common configuration files for PHP include hello php.ini file located under Program Files and hello .user.ini file located in hello root folder of your web app.</span></span> <span data-ttu-id="96ea8-135">Ponieważ plik php.ini hello nie jest edytowalny bezpośrednio na powitania usługi aplikacji platformy, hello rozszerzenia PHP Manager używa hello. user.ini tooapply plików, zmiany ustawień.</span><span class="sxs-lookup"><span data-stu-id="96ea8-135">Since hello php.ini file is not directly editable on hello App Service platform, hello PHP Manager extension uses hello .user.ini file tooapply setting changes.</span></span>

#### <span data-ttu-id="96ea8-136"><a id="PHPwebapp"></a>Witaj aplikacji sieci web PHP Manager</span><span class="sxs-lookup"><span data-stu-id="96ea8-136"><a id="PHPwebapp"></a> hello PHP Manager web application</span></span>
<span data-ttu-id="96ea8-137">strony głównej hello hello deployment PHP Manager jest następujący Hello:</span><span class="sxs-lookup"><span data-stu-id="96ea8-137">hello following is hello home page of hello PHP Manager deployment:</span></span>

![TransformSitePHPUI][TransformSitePHPUI]

<span data-ttu-id="96ea8-139">Jak widać, rozszerzenia aplikacji sieci web jest tak samo jak aplikacji sieci web regularnych, ale z plikiem ApplicationHost.xdt dodatkowe umieszczony w folderze głównym hello (więcej informacji o pliku ApplicationHost.xdt hello są dostępne w następnej sekcji hello tej aplikacji sieci web hello artykuł).</span><span class="sxs-lookup"><span data-stu-id="96ea8-139">As you can see, a web app extension is just like a regular web application, but with an additional ApplicationHost.xdt file placed in hello root folder of hello web app (more details about hello ApplicationHost.xdt file are available in hello next section of this article).</span></span>

<span data-ttu-id="96ea8-140">Witaj rozszerzenia PHP Manager został utworzony przy użyciu szablonu programu Visual Studio ASP.NET MVC 4 sieci Web aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="96ea8-140">hello PHP Manager extension was created using hello Visual Studio ASP.NET MVC 4 Web Application template.</span></span> <span data-ttu-id="96ea8-141">Witaj następujący widok w Eksploratorze rozwiązań pokazuje hello strukturę hello rozszerzenia PHP Manager.</span><span class="sxs-lookup"><span data-stu-id="96ea8-141">hello following view from Solution Explorer shows hello structure of hello PHP Manager extension.</span></span>

![TransformSiteSolEx][TransformSiteSolEx]

<span data-ttu-id="96ea8-143">Hello tylko specjalne potrzebne do We/Wy pliku jest tooindicate gdzie hello wwwroot hello aplikacji sieci web znajduje się katalog.</span><span class="sxs-lookup"><span data-stu-id="96ea8-143">hello only special logic needed for file I/O is tooindicate where hello wwwroot directory of hello web app is located.</span></span> <span data-ttu-id="96ea8-144">Witaj poniższy kod przedstawia przykład Witaj zmiennej środowiskowej "HOME" wskazuje hello ścieżki katalogu głównego aplikacji sieci web, a ścieżka wwwroot hello można utworzyć przez dodanie "site\wwwroot":</span><span class="sxs-lookup"><span data-stu-id="96ea8-144">As hello following code example shows, hello environment variable "HOME" indicates hello web app's root path, and hello wwwroot path can be constructed by appending "site\wwwroot":</span></span>

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


<span data-ttu-id="96ea8-145">Po umieszczeniu hello ścieżki katalogu, można użyć zwykły plik tooread operacji We/Wy i zapisać toofiles.</span><span class="sxs-lookup"><span data-stu-id="96ea8-145">After you have hello directory path, you can use regular file I/O operations tooread and write toofiles.</span></span>

<span data-ttu-id="96ea8-146">Jeden punkt ostrożność z rozszerzeń aplikacji sieci web traktuje hello obsługę łączy wewnętrznych.</span><span class="sxs-lookup"><span data-stu-id="96ea8-146">One point of caution with web app extensions regards hello handling of internal links.</span></span>  <span data-ttu-id="96ea8-147">Jeśli masz łącza w plikach HTML, które zapewniają ścieżki bezwzględne toointernal łącza w aplikacji sieci web, musisz zapewnić, że te łącza jest dołączany na początku nazwą rozszerzenia jako katalogu głównym.</span><span class="sxs-lookup"><span data-stu-id="96ea8-147">If you have any links in your HTML files that give absolute paths toointernal links on your web app, you must ensure those links are prepended with your extension name as your root.</span></span> <span data-ttu-id="96ea8-148">Jest to niezbędne, ponieważ główny powitania dla rozszerzenia jest teraz "/`[your-extension-name]`/" zamiast są tylko "/", dlatego dowolny wewnętrzny łącza należy zaktualizować odpowiednio.</span><span class="sxs-lookup"><span data-stu-id="96ea8-148">This is needed because hello root for your extension is now "/`[your-extension-name]`/" rather than being just "/", so any internal links must be updated accordingly.</span></span> <span data-ttu-id="96ea8-149">Na przykład załóżmy, że kod obejmuje następujące toohello łącza:</span><span class="sxs-lookup"><span data-stu-id="96ea8-149">For example, suppose your code includes a link toohello following:</span></span>

`"<a href="/Home/Settings">PHP Settings</a>"`

<span data-ttu-id="96ea8-150">Łącze hello jest częścią rozszerzenia aplikacji sieci web, hello link musi należeć hello następującej postaci:</span><span class="sxs-lookup"><span data-stu-id="96ea8-150">When hello link is part of a web app extension, hello link must be in hello following form:</span></span>

`"<a href="/[your-site-name]/Home/Settings">Settings</a>"`

<span data-ttu-id="96ea8-151">To wymaganie można obejść przez przy użyciu tylko ścieżek względnych w aplikacji sieci web, lub hello wielkość liter w aplikacji ASP.NET przy użyciu hello `@Html.ActionLink` metodę, która tworzy hello odpowiednie łącza.</span><span class="sxs-lookup"><span data-stu-id="96ea8-151">You can work around this requirement by either using only relative paths within your web application, or in hello case of ASP.NET applications, by using hello `@Html.ActionLink` method which creates hello appropriate links for you.</span></span>

#### <span data-ttu-id="96ea8-152"><a id="XDT"></a>Witaj applicationHost.xdt pliku</span><span class="sxs-lookup"><span data-stu-id="96ea8-152"><a id="XDT"></a> hello applicationHost.xdt file</span></span>
<span data-ttu-id="96ea8-153">Kod powitania dla rozszerzenia aplikacji sieci web przechodzi w obszarze %HOME%\SiteExtensions\[your Nazwa rozszerzenia].</span><span class="sxs-lookup"><span data-stu-id="96ea8-153">hello code for your web app extension goes under %HOME%\SiteExtensions\[your-extension-name].</span></span> <span data-ttu-id="96ea8-154">Zadzwonimy to katalog główny rozszerzenia hello.</span><span class="sxs-lookup"><span data-stu-id="96ea8-154">We'll call this hello extension root.</span></span>  

<span data-ttu-id="96ea8-155">tooregister Twojego rozszerzenia aplikacji sieci web z pliku applicationHost.config hello należy tooplace plik o nazwie ApplicationHost.xdt hello rozszerzenia głównego.</span><span class="sxs-lookup"><span data-stu-id="96ea8-155">tooregister your web app extension with hello applicationHost.config file, you need tooplace a file called ApplicationHost.xdt in hello extension root.</span></span> <span data-ttu-id="96ea8-156">zawartość Hello hello ApplicationHost.xdt pliku powinna być następująca:</span><span class="sxs-lookup"><span data-stu-id="96ea8-156">hello content of hello ApplicationHost.xdt file should be as follows:</span></span>

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

<span data-ttu-id="96ea8-157">Nazwa Hello wybrana jako nazwę rozszerzenia powinien mieć hello sama nazwa jak folder główny rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="96ea8-157">hello name you select as your extension name should have hello same name as your extension root folder.</span></span>

<span data-ttu-id="96ea8-158">To ustawienie działa hello dodawania nowych toohello ścieżka aplikacji `system.applicationHost` listę witryn w witrynie SCM hello.</span><span class="sxs-lookup"><span data-stu-id="96ea8-158">This has hello effect of adding a new application path toohello `system.applicationHost` sites list under hello SCM site.</span></span> <span data-ttu-id="96ea8-159">lokacja SCM Hello jest punkt końcowy administracji w lokacji z poświadczeniami dostępu określone.</span><span class="sxs-lookup"><span data-stu-id="96ea8-159">hello SCM site is a site administration end point with specific access credentials.</span></span> <span data-ttu-id="96ea8-160">Ma adres URL hello `https://[your-site-name].scm.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="96ea8-160">It has hello URL `https://[your-site-name].scm.azurewebsites.net`.</span></span>  

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

### <span data-ttu-id="96ea8-161"><a id="deploy"></a>Wdrażanie rozszerzenia aplikacji sieci Web</span><span class="sxs-lookup"><span data-stu-id="96ea8-161"><a id="deploy"></a> Web app extension deployment</span></span>
<span data-ttu-id="96ea8-162">tooinstall rozszerzenie aplikacji sieci web, można użyć FTP toocopy wszystkie pliki hello toohello aplikacji sieci web `\SiteExtensions\[your-extension-name]` folderu hello aplikacji sieci web, na którym ma zostać tooinstall hello rozszerzenia.</span><span class="sxs-lookup"><span data-stu-id="96ea8-162">tooinstall your web app extension, you can use FTP toocopy all hello files of your web application toohello `\SiteExtensions\[your-extension-name]` folder of hello web app on which you want tooinstall hello extension.</span></span>  <span data-ttu-id="96ea8-163">Należy się toocopy hello ApplicationHost.xdt toothis lokalizację pliku również.</span><span class="sxs-lookup"><span data-stu-id="96ea8-163">Be sure toocopy hello ApplicationHost.xdt file toothis location as well.</span></span> <span data-ttu-id="96ea8-164">Uruchom ponownie rozszerzenia hello tooenable aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="96ea8-164">Restart your web app tooenable hello extension.</span></span>

<span data-ttu-id="96ea8-165">Powinny być możliwe toosee rozszerzenie aplikacji sieci web na:</span><span class="sxs-lookup"><span data-stu-id="96ea8-165">You should be able toosee your web app extension at:</span></span>

`https://[your-site-name].scm.azurewebsites.net/[your-extension-name]`

<span data-ttu-id="96ea8-166">Należy pamiętać, że powitalne adres URL wygląda tak hello adres URL dla aplikacji sieci web, z wyjątkiem tego, który używa protokołu HTTPS i zawiera ".scm".</span><span class="sxs-lookup"><span data-stu-id="96ea8-166">Note that hello URL looks just like hello URL for your web app, except that it uses HTTPS and contains ".scm".</span></span>

<span data-ttu-id="96ea8-167">Jest możliwe toodisable wszystkie prywatne (nie preinstalowanym) rozszerzenia aplikacji sieci web podczas projektowania i badania przez dodawanie ustawień aplikacji z kluczem hello `WEBSITE_PRIVATE_EXTENSIONS` i wartości `0`.</span><span class="sxs-lookup"><span data-stu-id="96ea8-167">It is possible toodisable all private (not pre-installed) extensions for your web app during development and investigations by adding an app settings with hello key `WEBSITE_PRIVATE_EXTENSIONS` and a value of `0`.</span></span>

> [!NOTE]
> <span data-ttu-id="96ea8-168">Tooget wprowadzenie do usługi Azure App Service przed utworzeniem konta platformy Azure, przejdź zbyt[Wypróbuj usługę App Service](https://azure.microsoft.com/try/app-service/), gdzie możesz od razu utworzyć krótkotrwałą, początkową aplikację sieci web w usłudze App Service.</span><span class="sxs-lookup"><span data-stu-id="96ea8-168">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="96ea8-169">Bez kart kredytowych i bez zobowiązań.</span><span class="sxs-lookup"><span data-stu-id="96ea8-169">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="whats-changed"></a><span data-ttu-id="96ea8-170">Co zostało zmienione</span><span class="sxs-lookup"><span data-stu-id="96ea8-170">What's changed</span></span>
* <span data-ttu-id="96ea8-171">Toohello przewodnik zmiany z tooApp witryn sieci Web usługi dla: [usłudze Azure App Service i jej wpływ na istniejące usługi platformy Azure](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="96ea8-171">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!-- IMAGES -->
[TransformSitePHPUI]: ./media/web-sites-transform-extend/TransformSitePHPUI.png
[TransformSiteSolEx]: ./media/web-sites-transform-extend/TransformSiteSolEx.png

