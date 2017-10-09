---
title: aaaUpload niestandardowych tooAzure aplikacji sieci web Java
description: Ten samouczek pokazuje, jak tooupload niestandardowych Java web tooAzure aplikacji App Service Web Apps.
services: app-service\web
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: eb2ccd83-e5c6-444e-a0fc-08fd5cc8326c
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 0cb4a682bb25d86ff08bfd03628c89795c58451e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="upload-a-custom-java-web-app-tooazure"></a><span data-ttu-id="e3f67-103">Przekazywanie niestandardowych tooAzure aplikacji sieci web Java</span><span class="sxs-lookup"><span data-stu-id="e3f67-103">Upload a custom Java web app tooAzure</span></span>
<span data-ttu-id="e3f67-104">W tym temacie wyjaśniono, jak tooupload niestandardowych Java sieci web aplikacji zbyt[usłudze Azure App Service] aplikacji sieci Web.</span><span class="sxs-lookup"><span data-stu-id="e3f67-104">This topic explains how tooupload a custom Java web app too[Azure App Service] Web Apps.</span></span> <span data-ttu-id="e3f67-105">Zawiera informacje dotyczące tooany Java witryny sieci Web lub aplikacji sieci web, a także kilka przykładów dotyczących konkretnych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e3f67-105">Included is information that applies tooany Java website or web app, and also some examples for specific applications.</span></span>

<span data-ttu-id="e3f67-106">Należy pamiętać, że Azure umożliwia tworzenie aplikacji sieci web Java za pomocą portalu Azure hello konfiguracji interfejsu użytkownika i hello Azure Marketplace, zgodnie z opisem w [tworzenie aplikacji sieci web Java w usłudze Azure App Service](web-sites-java-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="e3f67-106">Note that Azure provides a means for creating Java web apps using hello Azure Portal's configuration UI, and hello Azure Marketplace, as documented at [Create a Java web app in Azure App Service](web-sites-java-get-started.md).</span></span> <span data-ttu-id="e3f67-107">Ten samouczek jest przeznaczony dla scenariuszy, w których nie ma interfejs użytkownika konfiguracji portalu Azure hello toouse lub hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="e3f67-107">This tutorial is for scenarios in which you do not want toouse hello Azure Portal configuration UI or hello Azure Marketplace.</span></span>  

## <a name="configuration-guidelines"></a><span data-ttu-id="e3f67-108">Wskazówki dotyczące konfigurowania</span><span class="sxs-lookup"><span data-stu-id="e3f67-108">Configuration guidelines</span></span>
<span data-ttu-id="e3f67-109">Hello poniżej opisano ustawienia hello oczekiwano niestandardowej aplikacji sieci web Java na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="e3f67-109">hello following describes hello settings expected for custom Java web apps on Azure.</span></span>

* <span data-ttu-id="e3f67-110">port HTTP Hello używany przez proces Java hello jest przypisywane dynamicznie.</span><span class="sxs-lookup"><span data-stu-id="e3f67-110">hello HTTP port used by hello Java process is dynamically assigned.</span></span>  <span data-ttu-id="e3f67-111">proces Hello musi używać portu powitania od zmiennej środowiskowej hello `HTTP_PLATFORM_PORT`.</span><span class="sxs-lookup"><span data-stu-id="e3f67-111">hello process must use hello port from hello environment variable `HTTP_PLATFORM_PORT`.</span></span>
* <span data-ttu-id="e3f67-112">Wszystkie nasłuchiwać portów innych niż jeden odbiornik HTTP hello powinny być wyłączone.</span><span class="sxs-lookup"><span data-stu-id="e3f67-112">All listen ports other than hello single HTTP listener should be disabled.</span></span>  <span data-ttu-id="e3f67-113">W Tomcat, która zawiera hello zamykania, HTTPS i AJP portów.</span><span class="sxs-lookup"><span data-stu-id="e3f67-113">In Tomcat, that includes hello shutdown, HTTPS, and AJP ports.</span></span>
* <span data-ttu-id="e3f67-114">kontener Hello musi toobe skonfigurowany tylko ruchu IPv4.</span><span class="sxs-lookup"><span data-stu-id="e3f67-114">hello container needs toobe configured for IPv4 traffic only.</span></span>
* <span data-ttu-id="e3f67-115">Witaj **uruchamiania** polecenia dla aplikacji hello musi toobe w konfiguracji hello.</span><span class="sxs-lookup"><span data-stu-id="e3f67-115">hello **startup** command for hello application needs toobe set in hello configuration.</span></span>
* <span data-ttu-id="e3f67-116">Aplikacje, które wymagają katalogi z uprawnienie zapisu muszą toobe znajduje się w aplikacji sieci web platformy Azure hello zawartości katalogu, który jest **D:\home**.</span><span class="sxs-lookup"><span data-stu-id="e3f67-116">Applications that require directories with write permission need toobe located in hello Azure web app's content directory,  which is **D:\home**.</span></span>  <span data-ttu-id="e3f67-117">zmiennej środowiskowej Hello `HOME` odwołuje się tooD:\home.</span><span class="sxs-lookup"><span data-stu-id="e3f67-117">hello environmental variable `HOME` refers tooD:\home.</span></span>  

<span data-ttu-id="e3f67-118">W pliku web.config hello można ustawić zmienne środowiskowe zgodnie z potrzebami.</span><span class="sxs-lookup"><span data-stu-id="e3f67-118">You can set environment variables as required in hello web.config file.</span></span>

## <a name="webconfig-httpplatform-configuration"></a><span data-ttu-id="e3f67-119">plik Web.config httpPlatform konfiguracji</span><span class="sxs-lookup"><span data-stu-id="e3f67-119">web.config httpPlatform configuration</span></span>
<span data-ttu-id="e3f67-120">Witaj następujące informacje w tym artykule opisano hello **httpPlatform** format w pliku web.config.</span><span class="sxs-lookup"><span data-stu-id="e3f67-120">hello following information describes hello **httpPlatform** format within web.config.</span></span>

<span data-ttu-id="e3f67-121">**argumenty** (domyślne = "").</span><span class="sxs-lookup"><span data-stu-id="e3f67-121">**arguments** (Default="").</span></span> <span data-ttu-id="e3f67-122">Toohello argumenty pliku wykonywalnego lub skryptu określony w hello **processPath** ustawienie.</span><span class="sxs-lookup"><span data-stu-id="e3f67-122">Arguments toohello executable or script specified in hello **processPath** setting.</span></span>

<span data-ttu-id="e3f67-123">Przykłady (przedstawiono **processPath** uwzględnione):</span><span class="sxs-lookup"><span data-stu-id="e3f67-123">Examples (shown with **processPath** included):</span></span>

    processPath="%HOME%\site\wwwroot\bin\tomcat\bin\catalina.bat"
    arguments="start"

    processPath="%JAVA_HOME\bin\java.exe"
    arguments="-Djava.net.preferIPv4Stack=true -Djetty.port=%HTTP\_PLATFORM\_PORT% -Djetty.base=&quot;%HOME%\site\wwwroot\bin\jetty-distribution-9.1.0.v20131115&quot; -jar &quot;%HOME%\site\wwwroot\bin\jetty-distribution-9.1.0.v20131115\start.jar&quot;"


<span data-ttu-id="e3f67-124">**processPath** -toohello ścieżki pliku wykonywalnego lub skrypt, który uruchomi proces nasłuchiwanie żądań HTTP.</span><span class="sxs-lookup"><span data-stu-id="e3f67-124">**processPath** - Path toohello executable or script that will launch a process listening for HTTP requests.</span></span>

<span data-ttu-id="e3f67-125">Przykłady:</span><span class="sxs-lookup"><span data-stu-id="e3f67-125">Examples:</span></span>

    processPath="%JAVA_HOME%\bin\java.exe"

    processPath="%HOME%\site\wwwroot\bin\tomcat\bin\startup.bat"

    processPath="%HOME%\site\wwwroot\bin\tomcat\bin\catalina.bat"

<span data-ttu-id="e3f67-126">**rapidFailsPerMinute** (domyślne = 10.) Liczba określone w procesie hello **processPath** jest dozwolona toocrash na minutę.</span><span class="sxs-lookup"><span data-stu-id="e3f67-126">**rapidFailsPerMinute** (Default=10.) Number of times hello process specified in **processPath** is allowed toocrash per minute.</span></span> <span data-ttu-id="e3f67-127">Po przekroczeniu tego limitu **HttpPlatformHandler** spowoduje zatrzymanie uruchamiania procesu hello hello pozostałej części hello minutę.</span><span class="sxs-lookup"><span data-stu-id="e3f67-127">If this limit is exceeded, **HttpPlatformHandler** will stop launching hello process for hello remainder of hello minute.</span></span>

<span data-ttu-id="e3f67-128">**requestTimeout** (domyślne = "00: 02:00".) Czas trwania, dla którego **HttpPlatformHandler** będzie oczekiwał na odpowiedź z procesu hello nasłuchiwanie `%HTTP_PLATFORM_PORT%`.</span><span class="sxs-lookup"><span data-stu-id="e3f67-128">**requestTimeout** (Default="00:02:00".) Duration for which **HttpPlatformHandler** will wait for a response from hello process listening on `%HTTP_PLATFORM_PORT%`.</span></span>

<span data-ttu-id="e3f67-129">**startupRetryCount** (domyślne = 10.) Ile razy **HttpPlatformHandler** spróbuje procesu hello toolaunch określone w **processPath**.</span><span class="sxs-lookup"><span data-stu-id="e3f67-129">**startupRetryCount** (Default=10.) Number of times **HttpPlatformHandler** will try toolaunch hello process specified in **processPath**.</span></span> <span data-ttu-id="e3f67-130">Zobacz **startupTimeLimit** więcej szczegółów.</span><span class="sxs-lookup"><span data-stu-id="e3f67-130">See **startupTimeLimit** for more details.</span></span>

<span data-ttu-id="e3f67-131">**startupTimeLimit** (domyślne = 10 sekund.) Czas trwania, dla którego **HttpPlatformHandler** będzie oczekiwał na powitania toostart skryptu lub pliku wykonywalnego procesu nasłuchuje na porcie hello.</span><span class="sxs-lookup"><span data-stu-id="e3f67-131">**startupTimeLimit** (Default=10 seconds.) Duration for which **HttpPlatformHandler** will wait for hello executable/script toostart a process listening on hello port.</span></span>  <span data-ttu-id="e3f67-132">Po przekroczeniu tego limitu czasu **HttpPlatformHandler** będzie kasowanie hello procesu i spróbuj toolaunch go ponownie **startupRetryCount** razy.</span><span class="sxs-lookup"><span data-stu-id="e3f67-132">If this time limit is exceeded, **HttpPlatformHandler** will kill hello process and try toolaunch it again **startupRetryCount** times.</span></span>

<span data-ttu-id="e3f67-133">**stdoutLogEnabled** (domyślne = "true".) Jeśli PRAWDA, **stdout** i **stderr** procesu hello określone w hello **processPath** zostanie przekierowany toohello pliku określonego w  **stdoutLogFile** (zobacz **stdoutLogFile** sekcji).</span><span class="sxs-lookup"><span data-stu-id="e3f67-133">**stdoutLogEnabled** (Default="true".) If true, **stdout** and **stderr** for hello process specified in hello **processPath** setting will be redirected toohello file specified in **stdoutLogFile** (see **stdoutLogFile** section).</span></span>

<span data-ttu-id="e3f67-134">**stdoutLogFile** (Default="d:\home\LogFiles\httpPlatformStdout.log".) Ścieżka bezwzględna do pliku, dla którego **stdout** i **stderr** z procesu hello określone w **processPath** będą rejestrowane.</span><span class="sxs-lookup"><span data-stu-id="e3f67-134">**stdoutLogFile** (Default="d:\home\LogFiles\httpPlatformStdout.log".) Absolute file path for which **stdout** and **stderr** from hello process specified in **processPath** will be logged.</span></span>

> [!NOTE]
> <span data-ttu-id="e3f67-135">`%HTTP_PLATFORM_PORT%`to specjalne symbol zastępczy wymagający toospecified w ramach **argumenty** lub w ramach hello **httpPlatform** **environmentVariables** listy.</span><span class="sxs-lookup"><span data-stu-id="e3f67-135">`%HTTP_PLATFORM_PORT%` is a special placeholder which needs toospecified either as part of **arguments** or as part of hello **httpPlatform** **environmentVariables** list.</span></span> <span data-ttu-id="e3f67-136">Ten zostanie zastąpiony przez port wytworzone przez **HttpPlatformHandler** tak, aby hello proces określony przez **processPath** może nasłuchiwać na tym porcie.</span><span class="sxs-lookup"><span data-stu-id="e3f67-136">This will be replaced by an internally generated port by **HttpPlatformHandler** so that hello process specified by **processPath** can listen on this port.</span></span>
> 
> 

## <a name="deployment"></a><span data-ttu-id="e3f67-137">Wdrożenie</span><span class="sxs-lookup"><span data-stu-id="e3f67-137">Deployment</span></span>
<span data-ttu-id="e3f67-138">Aplikacje sieci web Java na podstawie można wdrożyć prosty sposób przez większość hello sam oznacza używanych z aplikacjami sieci web Internet Information Services (IIS) na podstawie hello.</span><span class="sxs-lookup"><span data-stu-id="e3f67-138">Java based web apps can be deployed easily through most of hello same means that are used with hello Internet Information Services (IIS) based web applications.</span></span>  <span data-ttu-id="e3f67-139">FTP, Git i Kudu są wszystkie obsługiwane jako mechanizmy wdrażania, jak jest hello zintegrowane możliwości SCM dla aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="e3f67-139">FTP, Git and Kudu are all supported as deployment mechanisms, as is hello integrated SCM capability for web apps.</span></span> <span data-ttu-id="e3f67-140">WebDeploy działa jako protokół, jednak nie opracowanej Java w programie Visual Studio WebDeploy nie mieści się z przypadki użycia wdrożenia aplikacji sieci web Java.</span><span class="sxs-lookup"><span data-stu-id="e3f67-140">WebDeploy works as a protocol, however, as Java is not developed in Visual Studio, WebDeploy does not fit with Java web app deployment use cases.</span></span>

## <a name="application-configuration-examples"></a><span data-ttu-id="e3f67-141">Konfiguracja aplikacji przykłady</span><span class="sxs-lookup"><span data-stu-id="e3f67-141">Application configuration Examples</span></span>
<span data-ttu-id="e3f67-142">Dla aplikacji, plików web.config i hello hello Konfiguracja aplikacji jest dostępna jako przykłady tooshow jak tooenable aplikacji Java aplikacji sieci Web usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e3f67-142">For hello following applications, a web.config file and hello application configuration is provided as examples tooshow how tooenable your Java application on App Service Web Apps.</span></span>

### <a name="tomcat"></a><span data-ttu-id="e3f67-143">Tomcat</span><span class="sxs-lookup"><span data-stu-id="e3f67-143">Tomcat</span></span>
<span data-ttu-id="e3f67-144">Gdy istnieją dwie odmiany Tomcat dostarczanych z aplikacji usługi sieci Web aplikacji, nadal jest dość możliwe tooupload klienta określonych wystąpień.</span><span class="sxs-lookup"><span data-stu-id="e3f67-144">While there are two variations on Tomcat that are supplied with App Service Web Apps, it is still quite possible tooupload customer specific instances.</span></span> <span data-ttu-id="e3f67-145">Poniżej przedstawiono przykładowy instalacji Tomcat z innego języka Java maszyny wirtualnej (JVM).</span><span class="sxs-lookup"><span data-stu-id="e3f67-145">Below is an example of an install of Tomcat with a different Java Virtual Machine (JVM).</span></span>

    <?xml version="1.0" encoding="UTF-8"?>
    <configuration>
      <system.webServer>
        <handlers>
          <add name="httpPlatformHandler" path="*" verb="*" modules="httpPlatformHandler" resourceType="Unspecified" />
        </handlers>
        <httpPlatform processPath="%HOME%\site\wwwroot\bin\tomcat\bin\startup.bat" 
            arguments="">
          <environmentVariables>
            <environmentVariable name="CATALINA_OPTS" value="-Dport.http=%HTTP_PLATFORM_PORT%" />
            <environmentVariable name="CATALINA_HOME" value="%HOME%\site\wwwroot\bin\tomcat" />
            <environmentVariable name="JRE_HOME" value="%HOME%\site\wwwroot\bin\java" /> <!-- optional, if not specified, this will default too%programfiles%\Java -->
            <environmentVariable name="JAVA_OPTS" value="-Djava.net.preferIPv4Stack=true" />
          </environmentVariables>
        </httpPlatform>
      </system.webServer>
    </configuration>

<span data-ttu-id="e3f67-146">Na powitania po stronie serwera Tomcat istnieje kilka zmian konfiguracji, które wymagają toobe wprowadzone.</span><span class="sxs-lookup"><span data-stu-id="e3f67-146">On hello Tomcat side, there are a few configuration changes that need toobe made.</span></span> <span data-ttu-id="e3f67-147">Witaj server.xml musi tooset toobe edytować:</span><span class="sxs-lookup"><span data-stu-id="e3f67-147">hello server.xml needs toobe edited tooset:</span></span>

* <span data-ttu-id="e3f67-148">Zamknięcie portów = -1</span><span class="sxs-lookup"><span data-stu-id="e3f67-148">Shutdown port = -1</span></span>
* <span data-ttu-id="e3f67-149">Port HTTP łącznika = ${port.http}</span><span class="sxs-lookup"><span data-stu-id="e3f67-149">HTTP connector port = ${port.http}</span></span>
* <span data-ttu-id="e3f67-150">Adres HTTP łącznika = "127.0.0.1"</span><span class="sxs-lookup"><span data-stu-id="e3f67-150">HTTP connector address = "127.0.0.1"</span></span>
* <span data-ttu-id="e3f67-151">Komentarz HTTPS i AJP łączników</span><span class="sxs-lookup"><span data-stu-id="e3f67-151">Comment out HTTPS and AJP connectors</span></span>
* <span data-ttu-id="e3f67-152">Ustawienia IPv4 Hello można również ustawić, w którym można dodać pliku catalina.properties hello`java.net.preferIPv4Stack=true`</span><span class="sxs-lookup"><span data-stu-id="e3f67-152">hello IPv4 setting can also be set in hello catalina.properties file where you can add     `java.net.preferIPv4Stack=true`</span></span>

<span data-ttu-id="e3f67-153">Direct3d wywołania nie są obsługiwane w aplikacjach sieci Web usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e3f67-153">Direct3d calls are not supported on App Service Web Apps.</span></span> <span data-ttu-id="e3f67-154">toodisable, Dodaj powitania po opcji języka Java powinien aplikacji wywołań takie:`-Dsun.java2d.d3d=false`</span><span class="sxs-lookup"><span data-stu-id="e3f67-154">toodisable those, add hello following Java option should your application make such calls: `-Dsun.java2d.d3d=false`</span></span>

### <a name="jetty"></a><span data-ttu-id="e3f67-155">Jetty</span><span class="sxs-lookup"><span data-stu-id="e3f67-155">Jetty</span></span>
<span data-ttu-id="e3f67-156">Jak hello przypadku Tomcat, klienci mogą przekazać własnych wystąpieniach dla Jetty.</span><span class="sxs-lookup"><span data-stu-id="e3f67-156">As is hello case for Tomcat, customers can upload their own instances for Jetty.</span></span> <span data-ttu-id="e3f67-157">W przypadku hello uruchomionych hello pełnej instalacji programu Jetty hello konfiguracja będzie wyglądać następująco:</span><span class="sxs-lookup"><span data-stu-id="e3f67-157">In hello case of running hello full install of Jetty, hello configuration would look like this:</span></span>

    <?xml version="1.0" encoding="UTF-8"?>
    <configuration>
      <system.webServer>
        <handlers>
          <add name="httppPlatformHandler" path="*" verb="*" modules="httpPlatformHandler" resourceType="Unspecified" />
        </handlers>
        <httpPlatform processPath="%JAVA_HOME%\bin\java.exe" 
             arguments="-Djava.net.preferIPv4Stack=true -Djetty.port=%HTTP_PLATFORM_PORT% -Djetty.base=&quot;%HOME%\site\wwwroot\bin\jetty-distribution-9.1.0.v20131115&quot; -jar &quot;%HOME%\site\wwwroot\bin\jetty-distribution-9.1.0.v20131115\start.jar&quot;"
            startupTimeLimit="20"
          startupRetryCount="10"
          stdoutLogEnabled="true">
        </httpPlatform>
      </system.webServer>
    </configuration>

<span data-ttu-id="e3f67-158">Witaj Jetty należy toobe zmienione w hello start.ini tooset `java.net.preferIPv4Stack=true`.</span><span class="sxs-lookup"><span data-stu-id="e3f67-158">hello Jetty configuration needs toobe changed in hello start.ini tooset `java.net.preferIPv4Stack=true`.</span></span>

### <a name="springboot"></a><span data-ttu-id="e3f67-159">Springboot</span><span class="sxs-lookup"><span data-stu-id="e3f67-159">Springboot</span></span>
<span data-ttu-id="e3f67-160">W kolejności tooget Springboot aplikacja zostanie uruchomiona muszą tooupload plik JAR lub WAR i dodać hello następującego pliku web.config.</span><span class="sxs-lookup"><span data-stu-id="e3f67-160">In order tooget a Springboot application running you need tooupload your JAR or WAR file and add hello following web.config file.</span></span> <span data-ttu-id="e3f67-161">plik web.config Hello przechodzi w stan hello wwwroot folder.</span><span class="sxs-lookup"><span data-stu-id="e3f67-161">hello web.config file goes into hello wwwroot folder.</span></span> <span data-ttu-id="e3f67-162">W pliku web.config hello dostosować plik JAR tooyour toopoint argumenty hello, w hello następującego przykładowego pliku JAR hello znajduje się w folderze wwwroot hello również.</span><span class="sxs-lookup"><span data-stu-id="e3f67-162">In hello web.config adjust hello arguments toopoint tooyour JAR file, in hello following example hello JAR file is located in hello wwwroot folder as well.</span></span>  

    <?xml version="1.0" encoding="UTF-8"?>
    <configuration>
      <system.webServer>
        <handlers>
          <add name="httpPlatformHandler" path="*" verb="*" modules="httpPlatformHandler" resourceType="Unspecified" />
        </handlers>
        <httpPlatform processPath="%JAVA_HOME%\bin\java.exe"
            arguments="-Djava.net.preferIPv4Stack=true -Dserver.port=%HTTP_PLATFORM_PORT% -jar &quot;%HOME%\site\wwwroot\my-web-project.jar&quot;">
        </httpPlatform>
      </system.webServer>
    </configuration>


### <a name="hudson"></a><span data-ttu-id="e3f67-163">Hudson</span><span class="sxs-lookup"><span data-stu-id="e3f67-163">Hudson</span></span>
<span data-ttu-id="e3f67-164">Naszym teście używane hello Hudson 3.1.2 war i hello domyślnego Tomcat 7.0.50 wystąpienia, ale bez wykorzystania hello interfejsu użytkownika tooset rzeczy.</span><span class="sxs-lookup"><span data-stu-id="e3f67-164">Our test used hello Hudson 3.1.2 war and hello default Tomcat 7.0.50 instance but without using hello UI tooset things up.</span></span>  <span data-ttu-id="e3f67-165">Ponieważ Hudson jest narzędziem kompilacji oprogramowania, jest tooinstall zaleca go na dedykowanego wystąpienia, gdzie hello **AlwaysOn** flagę można ustawić na powitania aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="e3f67-165">Because Hudson is a software build tool, it is advised tooinstall it on dedicated instances where hello **AlwaysOn** flag can be set on hello web app.</span></span>

1. <span data-ttu-id="e3f67-166">W aplikacji sieci web katalogu głównego, tj., **d:\home\site\wwwroot**, Utwórz **webapps** katalogu (jeśli jeszcze nie istnieje) i umieścić Hudson.war w **d:\home\site\wwwroot\webapps**.</span><span class="sxs-lookup"><span data-stu-id="e3f67-166">In your web app’s root directory, i.e., **d:\home\site\wwwroot**, create a **webapps** directory (if not already present), and place Hudson.war in **d:\home\site\wwwroot\webapps**.</span></span>
2. <span data-ttu-id="e3f67-167">Pobierz apache maven 3.0.5 (zgodny z Hudson) i umieść go w **d:\home\site\wwwroot**.</span><span class="sxs-lookup"><span data-stu-id="e3f67-167">Download apache maven 3.0.5 (compatible with Hudson) and place it in **d:\home\site\wwwroot**.</span></span>
3. <span data-ttu-id="e3f67-168">Utwórz plik web.config w **d:\home\site\wwwroot** i hello Wklej zawartość w niej:</span><span class="sxs-lookup"><span data-stu-id="e3f67-168">Create web.config in **d:\home\site\wwwroot** and paste hello following contents in it:</span></span>
   
        <?xml version="1.0" encoding="UTF-8"?>
        <configuration>
          <system.webServer>
            <handlers>
              <add name="httppPlatformHandler" path="*" verb="*" 
        modules="httpPlatformHandler" resourceType="Unspecified" />
            </handlers>
            <httpPlatform processPath="%AZURE_TOMCAT7_HOME%\bin\startup.bat"
        startupTimeLimit="20"
        startupRetryCount="10">
        <environmentVariables>
          <environmentVariable name="HUDSON_HOME" 
        value="%HOME%\site\wwwroot\hudson_home" />
          <environmentVariable name="JAVA_OPTS" 
        value="-Djava.net.preferIPv4Stack=true -Duser.home=%HOME%/site/wwwroot/user_home -Dhudson.DNSMultiCast.disabled=true" />
        </environmentVariables>            
            </httpPlatform>
          </system.webServer>
        </configuration>
   
    <span data-ttu-id="e3f67-169">W tym momencie hello aplikacji sieci web można uruchomić ją ponownie tootake hello zmiany.</span><span class="sxs-lookup"><span data-stu-id="e3f67-169">At this point hello web app can be restarted tootake hello changes.</span></span>  <span data-ttu-id="e3f67-170">Połącz toohttp://yourwebapp/hudson toostart Hudson.</span><span class="sxs-lookup"><span data-stu-id="e3f67-170">Connect toohttp://yourwebapp/hudson toostart Hudson.</span></span>
4. <span data-ttu-id="e3f67-171">Po Hudson konfiguruje się, powinien zostać wyświetlony po ekranie powitania:</span><span class="sxs-lookup"><span data-stu-id="e3f67-171">After Hudson configures itself, you should see hello following screen:</span></span>
   
    ![Hudson](./media/web-sites-java-custom-upload/hudson1.png)
5. <span data-ttu-id="e3f67-173">Hello dostępu do strony konfiguracji Hudson: kliknij **Hudson zarządzanie**, a następnie kliknij przycisk **Konfiguruj System**.</span><span class="sxs-lookup"><span data-stu-id="e3f67-173">Access hello Hudson configuration page: Click **Manage Hudson**, and then click **Configure System**.</span></span>
6. <span data-ttu-id="e3f67-174">Skonfiguruj hello JDK, jak pokazano poniżej:</span><span class="sxs-lookup"><span data-stu-id="e3f67-174">Configure hello JDK as shown below:</span></span>
   
    ![Konfiguracja Hudson](./media/web-sites-java-custom-upload/hudson2.png)
7. <span data-ttu-id="e3f67-176">Skonfiguruj Maven, jak pokazano poniżej:</span><span class="sxs-lookup"><span data-stu-id="e3f67-176">Configure Maven as shown below:</span></span>
   
    ![Konfiguracja maven](./media/web-sites-java-custom-upload/maven.png)
8. <span data-ttu-id="e3f67-178">Zapisz ustawienia hello.</span><span class="sxs-lookup"><span data-stu-id="e3f67-178">Save hello settings.</span></span> <span data-ttu-id="e3f67-179">Hudson powinno być teraz skonfigurowana i gotowa do użycia.</span><span class="sxs-lookup"><span data-stu-id="e3f67-179">Hudson should now be configured and ready for use.</span></span>

<span data-ttu-id="e3f67-180">Aby uzyskać dodatkowe informacje na temat Hudson, zobacz [http://hudson-ci.org](http://hudson-ci.org).</span><span class="sxs-lookup"><span data-stu-id="e3f67-180">For additional information on Hudson, see [http://hudson-ci.org](http://hudson-ci.org).</span></span>

### <a name="liferay"></a><span data-ttu-id="e3f67-181">Liferay</span><span class="sxs-lookup"><span data-stu-id="e3f67-181">Liferay</span></span>
<span data-ttu-id="e3f67-182">Liferay jest obsługiwana w aplikacji sieci Web usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e3f67-182">Liferay is supported on App Service Web Apps.</span></span> <span data-ttu-id="e3f67-183">Ponieważ Liferay może wymagać znaczących pamięci, aplikacji sieci web hello musi toorun w średnich i dużych dedykowanych procesów roboczych, który zawiera za mało pamięci.</span><span class="sxs-lookup"><span data-stu-id="e3f67-183">Since Liferay can require significant memory, hello web app needs toorun on a medium or large dedicated worker, which can provide enough memory.</span></span> <span data-ttu-id="e3f67-184">Liferay również zajmuje kilka minut toostart.</span><span class="sxs-lookup"><span data-stu-id="e3f67-184">Liferay also takes several minutes toostart up.</span></span> <span data-ttu-id="e3f67-185">Z tego powodu zaleca się ustawienie aplikacji sieci web hello zbyt**zawsze na**.</span><span class="sxs-lookup"><span data-stu-id="e3f67-185">For that reason, it is recommended that you set hello web app too**Always On**.</span></span>  

<span data-ttu-id="e3f67-186">Przy użyciu Liferay 6.1.2, który Community Edition GA3 powiązane z Tomcat, hello następujące pliki zostały zmienione po pobraniu Liferay:</span><span class="sxs-lookup"><span data-stu-id="e3f67-186">Using Liferay 6.1.2 Community Edition GA3 bundled with Tomcat, hello following files were edited after downloading Liferay:</span></span>

<span data-ttu-id="e3f67-187">**Server.XML**</span><span class="sxs-lookup"><span data-stu-id="e3f67-187">**Server.xml**</span></span>

* <span data-ttu-id="e3f67-188">Zmień zamykania portu zbyt-1.</span><span class="sxs-lookup"><span data-stu-id="e3f67-188">Change Shutdown port too-1.</span></span>
* <span data-ttu-id="e3f67-189">Zmień zbyt łącznika HTTP`<Connector port="${port.http}" protocol="HTTP/1.1" connectionTimeout="600000" address="127.0.0.1" URIEncoding="UTF-8" />`</span><span class="sxs-lookup"><span data-stu-id="e3f67-189">Change HTTP connector too       `<Connector port="${port.http}" protocol="HTTP/1.1" connectionTimeout="600000" address="127.0.0.1" URIEncoding="UTF-8" />`</span></span>
* <span data-ttu-id="e3f67-190">Komentarz hello AJP łącznika.</span><span class="sxs-lookup"><span data-stu-id="e3f67-190">Comment out hello AJP connector.</span></span>

<span data-ttu-id="e3f67-191">W hello **liferay\tomcat-7.0.40\webapps\ROOT\WEB-INF\classes** folderu, Utwórz plik o nazwie **portal ext.properties**.</span><span class="sxs-lookup"><span data-stu-id="e3f67-191">In hello **liferay\tomcat-7.0.40\webapps\ROOT\WEB-INF\classes** folder, create a file named **portal-ext.properties**.</span></span> <span data-ttu-id="e3f67-192">Ten plik wymaga toocontain jednej linii, jak pokazano poniżej:</span><span class="sxs-lookup"><span data-stu-id="e3f67-192">This file needs toocontain one line, as shown here:</span></span>

    liferay.home=%HOME%/site/wwwroot/liferay

<span data-ttu-id="e3f67-193">Na powitania katalogu poziomu folderu tomcat 7.0.40 hello, Utwórz plik o nazwie **web.config** z hello następującej zawartości:</span><span class="sxs-lookup"><span data-stu-id="e3f67-193">At hello same directory level as hello tomcat-7.0.40 folder, create a file named **web.config** with hello following content:</span></span>

    <?xml version="1.0" encoding="UTF-8"?>
    <configuration>
      <system.webServer>
        <handlers>
    <add name="httpPlatformHandler" path="*" verb="*"
         modules="httpPlatformHandler" resourceType="Unspecified" />
        </handlers>
        <httpPlatform processPath="%HOME%\site\wwwroot\tomcat-7.0.40\bin\catalina.bat" 
                      arguments="run" 
                      startupTimeLimit="10" 
                      requestTimeout="00:10:00" 
                      stdoutLogEnabled="true">
          <environmentVariables>
      <environmentVariable name="CATALINA_OPTS" value="-Dport.http=%HTTP_PLATFORM_PORT%" />
      <environmentVariable name="CATALINA_HOME" value="%HOME%\site\wwwroot\tomcat-7.0.40" />
            <environmentVariable name="JRE_HOME" value="D:\Program Files\Java\jdk1.7.0_51" /> 
            <environmentVariable name="JAVA_OPTS" value="-Djava.net.preferIPv4Stack=true" />
          </environmentVariables>
        </httpPlatform>
      </system.webServer>
    </configuration>

<span data-ttu-id="e3f67-194">W obszarze hello **httpPlatform** bloku hello **requestTimeout** ustawiono zbyt "00: 10:00".</span><span class="sxs-lookup"><span data-stu-id="e3f67-194">Under hello **httpPlatform** block, hello **requestTimeout** is set too“00:10:00”.</span></span>  <span data-ttu-id="e3f67-195">Można zmniejszyć, ale następnie są prawdopodobnie toosee niektóre błędy przekroczenia limitu czasu podczas Liferay jest uruchamianie.</span><span class="sxs-lookup"><span data-stu-id="e3f67-195">It can be reduced but then you are likely toosee some timeout errors while Liferay is bootstrapping.</span></span>  <span data-ttu-id="e3f67-196">Jeśli ta wartość została zmieniona, następnie hello **connectionTimeout** w hello tomcat server.xml również powinien być modyfikowany.</span><span class="sxs-lookup"><span data-stu-id="e3f67-196">If this value is changed, then hello **connectionTimeout** in hello tomcat server.xml should also be modified.</span></span>  

<span data-ttu-id="e3f67-197">Warto zauważyć, że varariable environnment JRE_HOME hello jest określona w hello powyżej web.config toopoint toohello JDK 64-bitowych.</span><span class="sxs-lookup"><span data-stu-id="e3f67-197">It is worth noting that hello JRE_HOME environnment varariable is specified in hello above web.config toopoint toohello 64-bit JDK.</span></span> <span data-ttu-id="e3f67-198">Domyślnie Hello jest 32-bitowy, ale ponieważ Liferay może wymagać wysokiego poziomu pamięci, zaleca się toouse hello JDK 64-bitowych.</span><span class="sxs-lookup"><span data-stu-id="e3f67-198">hello default is 32-bit, but since Liferay may require high levels of memory, it is recommended toouse hello 64-bit JDK.</span></span>

<span data-ttu-id="e3f67-199">Po wprowadzeniu tych zmian, ponownie uruchom aplikację sieci web uruchomiona Liferay, następnie należy otworzyć http://yourwebapp.</span><span class="sxs-lookup"><span data-stu-id="e3f67-199">Once you make these changes, restart your web app running Liferay, Then, open http://yourwebapp.</span></span> <span data-ttu-id="e3f67-200">Hello Liferay portal jest dostępny z głównego aplikacji sieci web hello.</span><span class="sxs-lookup"><span data-stu-id="e3f67-200">hello Liferay portal is available from hello web app root.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="e3f67-201">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e3f67-201">Next steps</span></span>
<span data-ttu-id="e3f67-202">Aby uzyskać więcej informacji o Liferay, zobacz [http://www.liferay.com](http://www.liferay.com).</span><span class="sxs-lookup"><span data-stu-id="e3f67-202">For more information about Liferay, see [http://www.liferay.com](http://www.liferay.com).</span></span>

<span data-ttu-id="e3f67-203">Aby uzyskać więcej informacji na temat języka Java, odwiedź stronę [Azure dla deweloperów języka Java](/java/azure).</span><span class="sxs-lookup"><span data-stu-id="e3f67-203">For more information about Java, visit [Azure for Java developers](/java/azure).</span></span>

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- External Links -->
[usłudze Azure App Service]: http://go.microsoft.com/fwlink/?LinkId=529714
