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
# <a name="upload-a-custom-java-web-app-tooazure"></a>Przekazywanie niestandardowych tooAzure aplikacji sieci web Java
W tym temacie wyjaśniono, jak tooupload niestandardowych Java sieci web aplikacji zbyt[usłudze Azure App Service] aplikacji sieci Web. Zawiera informacje dotyczące tooany Java witryny sieci Web lub aplikacji sieci web, a także kilka przykładów dotyczących konkretnych aplikacji.

Należy pamiętać, że Azure umożliwia tworzenie aplikacji sieci web Java za pomocą portalu Azure hello konfiguracji interfejsu użytkownika i hello Azure Marketplace, zgodnie z opisem w [tworzenie aplikacji sieci web Java w usłudze Azure App Service](web-sites-java-get-started.md). Ten samouczek jest przeznaczony dla scenariuszy, w których nie ma interfejs użytkownika konfiguracji portalu Azure hello toouse lub hello Azure Marketplace.  

## <a name="configuration-guidelines"></a>Wskazówki dotyczące konfigurowania
Hello poniżej opisano ustawienia hello oczekiwano niestandardowej aplikacji sieci web Java na platformie Azure.

* port HTTP Hello używany przez proces Java hello jest przypisywane dynamicznie.  proces Hello musi używać portu powitania od zmiennej środowiskowej hello `HTTP_PLATFORM_PORT`.
* Wszystkie nasłuchiwać portów innych niż jeden odbiornik HTTP hello powinny być wyłączone.  W Tomcat, która zawiera hello zamykania, HTTPS i AJP portów.
* kontener Hello musi toobe skonfigurowany tylko ruchu IPv4.
* Witaj **uruchamiania** polecenia dla aplikacji hello musi toobe w konfiguracji hello.
* Aplikacje, które wymagają katalogi z uprawnienie zapisu muszą toobe znajduje się w aplikacji sieci web platformy Azure hello zawartości katalogu, który jest **D:\home**.  zmiennej środowiskowej Hello `HOME` odwołuje się tooD:\home.  

W pliku web.config hello można ustawić zmienne środowiskowe zgodnie z potrzebami.

## <a name="webconfig-httpplatform-configuration"></a>plik Web.config httpPlatform konfiguracji
Witaj następujące informacje w tym artykule opisano hello **httpPlatform** format w pliku web.config.

**argumenty** (domyślne = ""). Toohello argumenty pliku wykonywalnego lub skryptu określony w hello **processPath** ustawienie.

Przykłady (przedstawiono **processPath** uwzględnione):

    processPath="%HOME%\site\wwwroot\bin\tomcat\bin\catalina.bat"
    arguments="start"

    processPath="%JAVA_HOME\bin\java.exe"
    arguments="-Djava.net.preferIPv4Stack=true -Djetty.port=%HTTP\_PLATFORM\_PORT% -Djetty.base=&quot;%HOME%\site\wwwroot\bin\jetty-distribution-9.1.0.v20131115&quot; -jar &quot;%HOME%\site\wwwroot\bin\jetty-distribution-9.1.0.v20131115\start.jar&quot;"


**processPath** -toohello ścieżki pliku wykonywalnego lub skrypt, który uruchomi proces nasłuchiwanie żądań HTTP.

Przykłady:

    processPath="%JAVA_HOME%\bin\java.exe"

    processPath="%HOME%\site\wwwroot\bin\tomcat\bin\startup.bat"

    processPath="%HOME%\site\wwwroot\bin\tomcat\bin\catalina.bat"

**rapidFailsPerMinute** (domyślne = 10.) Liczba określone w procesie hello **processPath** jest dozwolona toocrash na minutę. Po przekroczeniu tego limitu **HttpPlatformHandler** spowoduje zatrzymanie uruchamiania procesu hello hello pozostałej części hello minutę.

**requestTimeout** (domyślne = "00: 02:00".) Czas trwania, dla którego **HttpPlatformHandler** będzie oczekiwał na odpowiedź z procesu hello nasłuchiwanie `%HTTP_PLATFORM_PORT%`.

**startupRetryCount** (domyślne = 10.) Ile razy **HttpPlatformHandler** spróbuje procesu hello toolaunch określone w **processPath**. Zobacz **startupTimeLimit** więcej szczegółów.

**startupTimeLimit** (domyślne = 10 sekund.) Czas trwania, dla którego **HttpPlatformHandler** będzie oczekiwał na powitania toostart skryptu lub pliku wykonywalnego procesu nasłuchuje na porcie hello.  Po przekroczeniu tego limitu czasu **HttpPlatformHandler** będzie kasowanie hello procesu i spróbuj toolaunch go ponownie **startupRetryCount** razy.

**stdoutLogEnabled** (domyślne = "true".) Jeśli PRAWDA, **stdout** i **stderr** procesu hello określone w hello **processPath** zostanie przekierowany toohello pliku określonego w  **stdoutLogFile** (zobacz **stdoutLogFile** sekcji).

**stdoutLogFile** (Default="d:\home\LogFiles\httpPlatformStdout.log".) Ścieżka bezwzględna do pliku, dla którego **stdout** i **stderr** z procesu hello określone w **processPath** będą rejestrowane.

> [!NOTE]
> `%HTTP_PLATFORM_PORT%`to specjalne symbol zastępczy wymagający toospecified w ramach **argumenty** lub w ramach hello **httpPlatform** **environmentVariables** listy. Ten zostanie zastąpiony przez port wytworzone przez **HttpPlatformHandler** tak, aby hello proces określony przez **processPath** może nasłuchiwać na tym porcie.
> 
> 

## <a name="deployment"></a>Wdrożenie
Aplikacje sieci web Java na podstawie można wdrożyć prosty sposób przez większość hello sam oznacza używanych z aplikacjami sieci web Internet Information Services (IIS) na podstawie hello.  FTP, Git i Kudu są wszystkie obsługiwane jako mechanizmy wdrażania, jak jest hello zintegrowane możliwości SCM dla aplikacji sieci web. WebDeploy działa jako protokół, jednak nie opracowanej Java w programie Visual Studio WebDeploy nie mieści się z przypadki użycia wdrożenia aplikacji sieci web Java.

## <a name="application-configuration-examples"></a>Konfiguracja aplikacji przykłady
Dla aplikacji, plików web.config i hello hello Konfiguracja aplikacji jest dostępna jako przykłady tooshow jak tooenable aplikacji Java aplikacji sieci Web usługi aplikacji.

### <a name="tomcat"></a>Tomcat
Gdy istnieją dwie odmiany Tomcat dostarczanych z aplikacji usługi sieci Web aplikacji, nadal jest dość możliwe tooupload klienta określonych wystąpień. Poniżej przedstawiono przykładowy instalacji Tomcat z innego języka Java maszyny wirtualnej (JVM).

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

Na powitania po stronie serwera Tomcat istnieje kilka zmian konfiguracji, które wymagają toobe wprowadzone. Witaj server.xml musi tooset toobe edytować:

* Zamknięcie portów = -1
* Port HTTP łącznika = ${port.http}
* Adres HTTP łącznika = "127.0.0.1"
* Komentarz HTTPS i AJP łączników
* Ustawienia IPv4 Hello można również ustawić, w którym można dodać pliku catalina.properties hello`java.net.preferIPv4Stack=true`

Direct3d wywołania nie są obsługiwane w aplikacjach sieci Web usługi aplikacji. toodisable, Dodaj powitania po opcji języka Java powinien aplikacji wywołań takie:`-Dsun.java2d.d3d=false`

### <a name="jetty"></a>Jetty
Jak hello przypadku Tomcat, klienci mogą przekazać własnych wystąpieniach dla Jetty. W przypadku hello uruchomionych hello pełnej instalacji programu Jetty hello konfiguracja będzie wyglądać następująco:

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

Witaj Jetty należy toobe zmienione w hello start.ini tooset `java.net.preferIPv4Stack=true`.

### <a name="springboot"></a>Springboot
W kolejności tooget Springboot aplikacja zostanie uruchomiona muszą tooupload plik JAR lub WAR i dodać hello następującego pliku web.config. plik web.config Hello przechodzi w stan hello wwwroot folder. W pliku web.config hello dostosować plik JAR tooyour toopoint argumenty hello, w hello następującego przykładowego pliku JAR hello znajduje się w folderze wwwroot hello również.  

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


### <a name="hudson"></a>Hudson
Naszym teście używane hello Hudson 3.1.2 war i hello domyślnego Tomcat 7.0.50 wystąpienia, ale bez wykorzystania hello interfejsu użytkownika tooset rzeczy.  Ponieważ Hudson jest narzędziem kompilacji oprogramowania, jest tooinstall zaleca go na dedykowanego wystąpienia, gdzie hello **AlwaysOn** flagę można ustawić na powitania aplikacji sieci web.

1. W aplikacji sieci web katalogu głównego, tj., **d:\home\site\wwwroot**, Utwórz **webapps** katalogu (jeśli jeszcze nie istnieje) i umieścić Hudson.war w **d:\home\site\wwwroot\webapps**.
2. Pobierz apache maven 3.0.5 (zgodny z Hudson) i umieść go w **d:\home\site\wwwroot**.
3. Utwórz plik web.config w **d:\home\site\wwwroot** i hello Wklej zawartość w niej:
   
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
   
    W tym momencie hello aplikacji sieci web można uruchomić ją ponownie tootake hello zmiany.  Połącz toohttp://yourwebapp/hudson toostart Hudson.
4. Po Hudson konfiguruje się, powinien zostać wyświetlony po ekranie powitania:
   
    ![Hudson](./media/web-sites-java-custom-upload/hudson1.png)
5. Hello dostępu do strony konfiguracji Hudson: kliknij **Hudson zarządzanie**, a następnie kliknij przycisk **Konfiguruj System**.
6. Skonfiguruj hello JDK, jak pokazano poniżej:
   
    ![Konfiguracja Hudson](./media/web-sites-java-custom-upload/hudson2.png)
7. Skonfiguruj Maven, jak pokazano poniżej:
   
    ![Konfiguracja maven](./media/web-sites-java-custom-upload/maven.png)
8. Zapisz ustawienia hello. Hudson powinno być teraz skonfigurowana i gotowa do użycia.

Aby uzyskać dodatkowe informacje na temat Hudson, zobacz [http://hudson-ci.org](http://hudson-ci.org).

### <a name="liferay"></a>Liferay
Liferay jest obsługiwana w aplikacji sieci Web usługi aplikacji. Ponieważ Liferay może wymagać znaczących pamięci, aplikacji sieci web hello musi toorun w średnich i dużych dedykowanych procesów roboczych, który zawiera za mało pamięci. Liferay również zajmuje kilka minut toostart. Z tego powodu zaleca się ustawienie aplikacji sieci web hello zbyt**zawsze na**.  

Przy użyciu Liferay 6.1.2, który Community Edition GA3 powiązane z Tomcat, hello następujące pliki zostały zmienione po pobraniu Liferay:

**Server.XML**

* Zmień zamykania portu zbyt-1.
* Zmień zbyt łącznika HTTP`<Connector port="${port.http}" protocol="HTTP/1.1" connectionTimeout="600000" address="127.0.0.1" URIEncoding="UTF-8" />`
* Komentarz hello AJP łącznika.

W hello **liferay\tomcat-7.0.40\webapps\ROOT\WEB-INF\classes** folderu, Utwórz plik o nazwie **portal ext.properties**. Ten plik wymaga toocontain jednej linii, jak pokazano poniżej:

    liferay.home=%HOME%/site/wwwroot/liferay

Na powitania katalogu poziomu folderu tomcat 7.0.40 hello, Utwórz plik o nazwie **web.config** z hello następującej zawartości:

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

W obszarze hello **httpPlatform** bloku hello **requestTimeout** ustawiono zbyt "00: 10:00".  Można zmniejszyć, ale następnie są prawdopodobnie toosee niektóre błędy przekroczenia limitu czasu podczas Liferay jest uruchamianie.  Jeśli ta wartość została zmieniona, następnie hello **connectionTimeout** w hello tomcat server.xml również powinien być modyfikowany.  

Warto zauważyć, że varariable environnment JRE_HOME hello jest określona w hello powyżej web.config toopoint toohello JDK 64-bitowych. Domyślnie Hello jest 32-bitowy, ale ponieważ Liferay może wymagać wysokiego poziomu pamięci, zaleca się toouse hello JDK 64-bitowych.

Po wprowadzeniu tych zmian, ponownie uruchom aplikację sieci web uruchomiona Liferay, następnie należy otworzyć http://yourwebapp. Hello Liferay portal jest dostępny z głównego aplikacji sieci web hello. 

## <a name="next-steps"></a>Następne kroki
Aby uzyskać więcej informacji o Liferay, zobacz [http://www.liferay.com](http://www.liferay.com).

Aby uzyskać więcej informacji na temat języka Java, odwiedź stronę [Azure dla deweloperów języka Java](/java/azure).

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- External Links -->
[usłudze Azure App Service]: http://go.microsoft.com/fwlink/?LinkId=529714
