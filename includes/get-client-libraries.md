### <a name="install-via-composer"></a>Zainstaluj za pośrednictwem Composer
1. [Zainstaluj usługę Git][install-git]. Należy pamiętać, że w systemie Windows, musisz również dodać zmiennej środowiskowej PATH hello Git tooyour pliku wykonywalnego. 
2. Utwórz plik o nazwie **composer.json** w hello katalogu głównym projektu i dodać powitania po tooit kodu:
   
    ```json
    {
      "require": {
        "microsoft/windowsazure": "^0.4"
      }
    }
    ```
3. Pobierz  **[composer.phar] [ composer-phar]**  w katalogu głównym projektu.
4. Otwórz wiersz polecenia i wykonaj następujące polecenie w katalogu głównym projektu hello
   
    ```
    php composer.phar install
    ```

[php-sdk-github]: http://go.microsoft.com/fwlink/?LinkId=252719
[install-git]: http://git-scm.com/book/en/Getting-Started-Installing-Git
[download-SDK-PHP]: ../articles/php-download-sdk.md
[composer-phar]: http://getcomposer.org/composer.phar
