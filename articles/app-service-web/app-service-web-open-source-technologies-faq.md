---
title: "aplikacje sieci web technologii źródła aaaOpen często zadawane pytania dotyczące usługi Azure | Dokumentacja firmy Microsoft"
description: Uzyskaj odpowiedzi toofrequently zadawane pytania na temat technologii open source w funkcji Web Apps hello Azure App Service.
services: app-service\web
documentationcenter: 
author: genlin
manager: cshepard
editor: 
tags: top-support-issue
ms.assetid: 2fa5ee6b-51a6-4237-805f-518e6c57d11b
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 7/10/2017
ms.author: genli
ms.openlocfilehash: 35cff4f322859d25972747cf55aa7c4316381a51
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="open-source-technologies-faqs-for-web-apps-in-azure"></a>Technologie open source często zadawane pytania dotyczące aplikacji sieci Web na platformie Azure

Ten artykuł zawiera toofrequently odpowiedzi zadawane pytania (FAQ) dotyczące problemów z technologii open source hello [funkcja Web Apps usługi Azure App Service](https://azure.microsoft.com/services/app-service/web/).

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="my-cleardb-database-is-down-how-do-i-resolve-this"></a>Baza danych ClearDB jest wyłączony. Jak rozwiązać ten problem?

W przypadku problemów związanych z bazy danych, skontaktuj się z [Obsługa ClearDB](https://www.cleardb.com/developers/help/support). 

Aby uzyskać odpowiedzi na pytania toocommon o ClearDB, zobacz [ClearDB — często zadawane pytania](https://docs.microsoft.com/azure/store-cleardb-faq/).

## <a name="why-isnt-my-cleardb-database-listed-in-hello-portal"></a>Dlaczego mojej bazy danych ClearDB nie jest wymieniony w portalu hello?

Jeśli utworzysz bazę danych ClearDB w hello [portalu Azure](http://portal.azure.com/), hello bazy danych nie jest wyświetlane w hello [klasycznego portalu Azure](http://manage.windowsazure.com/). toowork obejścia tego problemu, może ręcznie połączyć aplikację sieci web toohello bazy danych.

Podobnie jeśli utworzysz bazę danych ClearDB w hello [klasycznego portalu Azure](http://manage.windowsazure.com/), nie zobaczysz bazy danych w hello [portalu Azure](http://portal.azure.com/). W takim przypadku obejście nie jest dostępna. 

Aby uzyskać więcej informacji, zobacz [często zadawane pytania dotyczące bazy danych ClearDB MySQL z usługi aplikacji Azure](https://docs.microsoft.com/azure/store-cleardb-faq/).

## <a name="why-wasnt-my-cleardb-database-migrated-during-my-subscription-migration"></a>Dlaczego nie migracji bazy danych ClearDB podczas migracji mojej subskrypcji?

Podczas przeprowadzania migracji zasobów w subskrypcjach, mają zastosowanie następujące ograniczenia. Baza danych ClearDB MySQL jest usługi innej firmy i nie są migrowane podczas migracji subskrypcji platformy Azure.

Jeśli nie zarządzasz hello migracji bazy danych MySQL, przed przeprowadzeniem migracji zasobów platformy Azure, bazy danych ClearDB MySQL mogą być niedostępne. tooavoid to najpierw ręcznie należy zmigrować bazę danych ClearDB, a następnie przeprowadzić migrację hello subskrypcji platformy Azure dla aplikacji sieci web.

Aby uzyskać więcej informacji, zobacz [często zadawane pytania dotyczące bazy danych ClearDB MySQL z usługi aplikacji Azure](https://docs.microsoft.com/azure/store-cleardb-faq/).

## <a name="how-do-i-turn-on-php-logging-tootroubleshoot-php-issues"></a>Jak włączyć rejestrowanie problemów PHP tootroubleshoot PHP

tooturn PHP rejestrowania:

1. Zaloguj się tooyour [Kudu witryny sieci Web](https://*yourwebsitename*.scm.azurewebsites.net).
2. W menu u góry hello, wybierz **konsoli debugowania** > **CMD**.
3. Wybierz hello **lokacji** folderu.
4. Wybierz hello **wwwroot** folderu.
5. Wybierz hello  **+**  ikonę, a następnie wybierz **nowy plik**.
6. Ustaw nazwę pliku hello zbyt**. user.ini**.
7. Wybierz ikonę ołówka hello obok zbyt**. user.ini**.
8. W pliku hello Dodaj ten kod:`log_errors=on`
9. Wybierz pozycję **Zapisz**.
10. Wybierz ikonę ołówka hello obok zbyt**wp config.php**.
11. Zmień toohello tekst hello następującego kodu:
   ```
   //Enable WP_DEBUG modedefine('WP_DEBUG', true);//Enable debug logging too/wp-content/debug.logdefine('WP_DEBUG_LOG', true);
   //Supress errors and warnings tooscreendefine('WP_DEBUG_DISPLAY', false);//Supress PHP errors tooscreenini_set('display_errors', 0);
   ```
12. Witaj portalu Azure, w menu aplikacji sieci web hello, ponownie uruchomić aplikacji sieci web.

Aby uzyskać więcej informacji, zobacz [dzienniki błędów włączyć WordPress](https://blogs.msdn.microsoft.com/azureossds/2015/10/09/logging-php-errors-in-wordpress-2/).

## <a name="how-do-i-log-python-application-errors-in-apps-that-are-hosted-in-app-service"></a>Jak rejestrować błędów aplikacji Python w aplikacjach, które znajdują się w usłudze App Service?

błędów aplikacji Python toocapture:

1. Witaj portalu Azure w aplikacji sieci web wybierz **ustawienia**.
2. Na powitania **ustawienia** wybierz opcję **ustawienia aplikacji**.
3. W obszarze **ustawień aplikacji**, wprowadź powitania po parę klucza i wartości:
    * Klucz: WSGI_LOG
    * Wartość: D:\home\site\wwwroot\logs.txt (wprowadź wybrana nazwa pliku)

Błędy w pliku logs.txt hello w folderze wwwroot hello powinna zostać wyświetlona.

## <a name="how-do-i-change-hello-version-of-hello-nodejs-application-that-is-hosted-in-app-service"></a>Jak zmienić wersję hello hello aplikacji Node.js, który znajduje się w usłudze App Service?

Wersja hello toochange hello aplikacji Node.js, można użyć jednego z hello następujące opcje:

*   W portalu Azure hello, użyj **ustawień aplikacji**.
    1. W hello portalu Azure Przejdź tooyour aplikacji sieci web.
    2. Na powitania **ustawienia** bloku, wybierz opcję **ustawienia aplikacji**.
    3. W **ustawień aplikacji**, mogą obejmować WEBSITE_NODE_DEFAULT_VERSION jako klucz hello i hello wersji środowiska node.js ma jako wartość hello.
    4. Przejdź tooyour [konsoli Kudu](https://*yourwebsitename*.scm.azurewebsites.net).
    5. toocheck hello wersji środowiska Node.js, wprowadź następujące polecenie hello:  
   ```
   node -v
   ```
*   Zmodyfikuj plik iisnode.yml udostępniany hello. Zmiana wersji środowiska Node.js hello w plik iisnode.yml udostępniany hello jedynie ustawia środowisko uruchomieniowe hello tego programu iisnode używa. Twoje cmd Kudu i inne nadal używać hello wersji środowiska Node.js, który jest ustawiony w **ustawień aplikacji** w hello portalu Azure.

    Plik iisnode.yml hello tooset ręcznie utworzyć plik iisnode.yml udostępniany w folderze głównym aplikacji. W pliku hello obejmują powitania po wierszu:
   ```
   nodeProcessCommandLine: "D:\Program Files (x86)\nodejs\5.9.1\node.exe"
   ```
   
*   Ustaw hello plik iisnode.yml udostępniany przy użyciu pliku package.json podczas wdrażania kontroli źródła.
    Witaj procesu wdrażania kontroli źródła Azure obejmuje hello następujące kroki:
    1. Przenosi toohello zawartości aplikacji sieci web platformy Azure.
    2. Tworzy domyślny skrypt wdrożenia, jeśli nie ma takiego (pliku deploy.cmd, .deployment pliki) w folderze głównym aplikacji hello w sieci web.
    3. Uruchamia skrypt wdrożenia, w którym tworzy plik iisnode.yml udostępniany Jeśli wspomina hello wersji środowiska Node.js w pliku package.json hello > aparatu`"engines": {"node": "5.9.1","npm": "3.7.3"}`
    4. Plik iisnode.yml udostępniany Hello ma powitania po wierszu kodu:
        ```
        nodeProcessCommandLine: "D:\Program Files (x86)\nodejs\5.9.1\node.exe"
        ```

## <a name="i-see-hello-message-error-establishing-a-database-connection-in-my-wordpress-app-thats-hosted-in-app-service-how-do-i-troubleshoot-this"></a>Wiadomości powitania "Błąd podczas nawiązywania połączenia z bazą danych" widoczne w mojej aplikacji WordPress, który znajduje się w usłudze App Service. Jak rozwiązać ten problem?

Jeśli widzisz ten błąd w aplikacji Azure WordPress, tooenable php_errors.log i debug.log pełną hello kroki szczegółowo w [dzienniki błędów włączyć WordPress](https://blogs.msdn.microsoft.com/azureossds/2015/10/09/logging-php-errors-in-wordpress-2/).

Po włączeniu hello dzienniki, występuje błąd hello, a następnie sprawdź toosee dzienniki hello, w przypadku korzystania z połączeń:
```
[09-Oct-2015 00:03:13 UTC] PHP Warning: mysqli_real_connect(): (HY000/1226): User ‘abcdefghijk79' has exceeded hello ‘max_user_connections’ resource (current value: 4) in D:\home\site\wwwroot\wp-includes\wp-db.php on line 1454
```

Jeśli zostanie wyświetlony ten błąd w plikach debug.log lub php_errors.log aplikacji przekracza hello liczbę połączeń. Jeśli przechowujesz na ClearDB Sprawdź hello liczbę połączeń, które są dostępne w Twojej [plan usługi](https://www.cleardb.com/pricing.view).

## <a name="how-do-i-debug-a-nodejs-app-thats-hosted-in-app-service"></a>Jak debugować aplikację Node.js, która jest hostowana w usłudze App Service?

1.  Przejdź tooyour [konsoli Kudu](https://*yourwebsitename*.scm.azurewebsites.net/DebugConsole).
2.  Folder Dzienniki aplikacji przejdź tooyour (D:\home\LogFiles\Application).
3.  W pliku logging_errors.txt hello Sprawdź, czy zawartość.

## <a name="how-do-i-install-native-python-modules-in-an-app-service-web-app-or-api-app"></a>Jak zainstalować natywnych modułów środowiska Python w aplikacji sieci web usługi aplikacji lub aplikacji interfejsu API?

Niektóre pakiety mogą nie zainstalować przy użyciu narzędzia pip na platformie Azure. Pakiet HELLO mogą nie być dostępne na powitania indeksu pakietów języka Python lub kompilatora mogą być wymagane (kompilator nie jest dostępna na komputerze hello, na którym działa aplikacja sieci web hello w usłudze App Service). Informacje dotyczące instalowania modułów macierzystych z usługi aplikacji — aplikacje sieci web i aplikacji API apps, zobacz [zainstalować modułów środowiska Python w usłudze App Service](https://blogs.msdn.microsoft.com/azureossds/2015/06/29/install-native-python-modules-on-azure-web-apps-api-apps/).

## <a name="how-do-i-deploy-a-django-app-tooapp-service-by-using-git-and-hello-new-version-of-python"></a>Jak wdrożyć tooApp aplikacji Django usługi przy użyciu usługi Git i hello nowej wersji języka Python?

Aby uzyskać informacje o instalowaniu Django, zobacz [wdrażanie tooApp aplikacji Django usługi](https://blogs.msdn.microsoft.com/azureossds/2016/08/25/deploying-django-app-to-azure-app-services-using-git-and-new-version-of-python/).

## <a name="where-are-hello-tomcat-log-files-located"></a>Gdzie znajdują się pliki dziennika Tomcat hello znajdujące się?

Dla portalu Azure Marketplace i wdrożeń niestandardowych:

* Lokalizacja folderu: D:\home\site\wwwroot\bin\apache-tomcat-8.0.33\logs
* Pliki odsetek:
    * catalina. *rrrr mm-dd*.log
    * Menedżer hosta. *rrrr mm-dd*.log
    * localhost. *rrrr mm-dd*.log
    * Menedżer. *rrrr mm-dd*.log
    * site_access_log. *rrrr mm-dd*.log


Dla portalu **ustawień aplikacji** wdrożenia:

* Lokalizacja folderu: D:\home\LogFiles
* Pliki odsetek:
    * catalina. *rrrr mm-dd*.log
    * Menedżer hosta. *rrrr mm-dd*.log
    * localhost. *rrrr mm-dd*.log
    * Menedżer. *rrrr mm-dd*.log
    * site_access_log. *rrrr mm-dd*.log

## <a name="how-do-i-troubleshoot-jdbc-driver-connection-errors"></a>Jak rozwiązywać problemy z błędami połączeń sterownik JDBC

Można napotkać następujące wiadomości w dziennikach Tomcat hello:

```
hello web application[ROOT] registered hello JDBC driver [com.mysql.jdbc.Driver] but failed toounregister it when hello web application was stopped. tooprevent a memory leak,hello JDBC Driver has been forcibly unregistered
```

Błąd hello tooresolve:

1. Usuń plik sqljdbc*.jar hello z folderu aplikacji/lib.
2. Jeśli używasz hello niestandardowych Tomcat lub Azure Marketplace Tomcat serwer sieci web, należy skopiować ten folder lib JAR pliku toohello Tomcat.
3. Jeśli włączasz Java z portalu Azure hello (wybierz **Java 1.8** > **serwera Tomcat**), plik jar sqljdbc.* hello kopiowania w folderze hello jest równoległe tooyour aplikacji. Następnie należy dodać hello następującego pliku web.config toohello ustawienie ścieżki klasy:

    ```
    <httpPlatform>
    <environmentVariables>
    <environmentVariablename ="JAVA_OPTS" value=" -Djava.net.preferIPv4Stack=true
    -Xms128M -classpath %CLASSPATH%;[Path toohello sqljdbc*.jarfile]" />
    </environmentVariables>
    </httpPlatform>
    ```

## <a name="why-do-i-see-errors-when-i-attempt-toocopy-live-log-files"></a>Dlaczego Zobacz błędy, gdy próbuję pliki dziennika na żywo toocopy?

Jeśli pliki dziennika na żywo toocopy dla aplikacji Java (na przykład Tomcat), można napotkać tego błędu FTP:

```
Error transferring file [filename] Copying files from remote side failed.
    
hello process cannot access hello file because it is being used by another process.
```

komunikat o błędzie Hello mogą się różnić w zależności od klienta hello FTP.

Wszystkie aplikacje Java mają to blokującego problem. Tylko Kudu obsługuje pobieranie tego pliku w uruchomionej aplikacji hello.

Zatrzymywanie aplikacji hello zezwala na dostęp FTP toothese plików.

Inne obejście jest toowrite zadania WebJob, który jest uruchamiany zgodnie z harmonogramem i kopii tych plików tooa innego katalogu. Aby uzyskać przykładowy projekt, zobacz hello [CopyLogsJob](https://github.com/kamilsykora/CopyLogsJob) projektu.

## <a name="where-do-i-find-hello-log-files-for-jetty"></a>Gdzie znaleźć hello plików dziennika dla Jetty?

Marketplace i wdrożeń niestandardowych hello plik dziennika znajduje się w folderze D:\home\site\wwwroot\bin\jetty-distribution-9.1.2.v20140210\logs hello. Należy pamiętać, że lokalizacja folderu hello zależy od wersji hello Jetty używasz. Na przykład ścieżka hello podane tu dla Jetty 9.1.2. Wyszukaj jetty_*YYYY_MM_DD*. stderrout.log.

W przypadku wdrożeń aplikacji ustawienia portalu plik dziennika hello jest D:\home\LogFiles. Wyszukaj jetty_*YYYY_MM_DD*. stderrout.log

## <a name="can-i-send-email-from-my-azure-web-app"></a>Z mojej aplikacji sieci web platformy Azure można wysłać wiadomości e-mail?

Usługa aplikacji nie ma funkcji wbudowanych poczty e-mail. Dla niektórych dobrej alternatyw do wysyłania wiadomości e-mail z aplikacji, zobacz ten [przepełnienie stosu dyskusji](http://stackoverflow.com/questions/17666161/sending-email-from-azure).

## <a name="why-does-my-wordpress-site-redirect-tooanother-url"></a>Dlaczego Moja witryna WordPress Przekierowywanie adresu URL tooanother?

Jeśli niedawno migracji tooAzure WordPress może przekierować toohello starego adresu URL domeny. Jest to spowodowane przez ustawienie w bazie danych MySQL hello.

WordPress Buddy + jest rozszerzeniem lokacji Azure, której można adresem URL przekierowania hello tooupdate bezpośrednio w bazie danych hello. Aby uzyskać więcej informacji o używaniu WordPress Buddy +, zobacz [WordPress narzędzia i MySQL migracji Buddy + z WordPress](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/).

Alternatywnie, jeśli wolisz toomanually adresu URL przekierowania hello usługi aktualizacji za pomocą zapytania SQL lub PHPMyAdmin, zobacz [WordPress: przekierowywanie adresu URL toowrong](https://blogs.msdn.microsoft.com/azureossds/2016/07/12/wordpress-redirecting-to-wrong-url/).

## <a name="how-do-i-change-my-wordpress-sign-in-password"></a>Jak zmienić hasło logowania WordPress?

Jeśli pamiętasz hasła logowania WordPress, możesz użyć WordPress Buddy + tooupdate go. hasło, hello install WordPress Buddy + Azure lokacji rozszerzenia, a następnie pełne hello kroki opisane w tooreset [WordPress narzędzia i MySQL migracji Buddy + z WordPress](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/).

## <a name="i-cant-sign-in-toowordpress-how-do-i-resolve-this"></a>Nie można zalogować tooWordPress. Jak rozwiązać ten problem?

Jeśli okaże się zablokowane WordPress po zainstalowaniu ostatnio wtyczkę, może być uszkodzony wtyczki. WordPress Buddy + jest rozszerzeniem lokacji Azure, które mogą pomóc Wyłącz wtyczki w WordPress. Aby uzyskać więcej informacji, zobacz [WordPress narzędzia i MySQL migracji Buddy + z WordPress](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/).

## <a name="how-do-i-migrate-my-wordpress-database"></a>Jak przeprowadzić migrację bazy danych WordPress?

Istnieje wiele opcji migrowania danych MySQL hello jest połączonych tooyour WordPress witryny sieci Web:

* Deweloperzy: Użyj hello [wiersza polecenia lub PHPMyAdmin](https://blogs.msdn.microsoft.com/azureossds/2016/03/02/migrating-data-between-mysql-databases-using-kudu-console-azure-app-service/)
* Innych niż deweloperów: Użyj [WordPress Buddy +](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/)

## <a name="how-do-i-help-make-wordpress-more-secure"></a>Sposób pomóc zabezpieczyć WordPress

toolearn o najlepsze rozwiązania dotyczące WordPress, zobacz [najlepszych rozwiązaniach dotyczących zabezpieczeń WordPress na platformie Azure](https://blogs.msdn.microsoft.com/azureossds/2016/12/26/best-practices-for-wordpress-security-on-azure/).

## <a name="i-am-trying-toouse-phpmyadmin-and-i-see-hello-message-access-denied-how-do-i-resolve-this"></a>Próbuję toouse PHPMyAdmin i pojawia się komunikat hello "Odmowa dostępu". Jak rozwiązać ten problem?

Ten problem może wystąpić, jeśli funkcja w aplikacji MySQL hello nie jest jeszcze uruchomiona w tym wystąpieniu usługi aplikacji. tooresolve hello problem, spróbuj tooaccess witryny sieci Web. Spowoduje to uruchomienie procesów hello wymagane, w tym procesie hello MySQL w aplikacji. na liście tooverify czy MySQL działa w aplikacji, w Eksploratorze procesu upewnij się, że mysqld.exe hello procesów.

Po upewnieniu się, że działa MySQL w aplikacji, spróbuj toouse PHPMyAdmin.

## <a name="i-get-an-http-403-error-when-i-try-tooimport-or-export-my-mysql-in-app-database-by-using-phpmyadmin-how-do-i-resolve-this"></a>Błąd HTTP 403 I spróbuj tooimport lub eksportu bazy danych MySQL w aplikacji przy użyciu PHPMyadmin. Jak rozwiązać ten problem?

Jeśli używasz starszej wersji przeglądarki Chrome, mogą występować znaną usterką. tooresolve hello problem uaktualnienia tooa nowszej wersji programu Chrome. Spróbuj również przy użyciu innej przeglądarki, takich jak program Internet Explorer lub Edge, gdzie hello problem nie występuje.
