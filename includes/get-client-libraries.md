### <a name="install-via-composer"></a><span data-ttu-id="8b233-101">Zainstaluj za pośrednictwem Composer</span><span class="sxs-lookup"><span data-stu-id="8b233-101">Install via Composer</span></span>
1. <span data-ttu-id="8b233-102">[Zainstaluj usługę Git][install-git].</span><span class="sxs-lookup"><span data-stu-id="8b233-102">[Install Git][install-git].</span></span> <span data-ttu-id="8b233-103">Należy pamiętać, że w systemie Windows, musisz również dodać zmiennej środowiskowej PATH hello Git tooyour pliku wykonywalnego.</span><span class="sxs-lookup"><span data-stu-id="8b233-103">Note that on Windows, you must also add hello Git executable tooyour PATH environment variable.</span></span> 
2. <span data-ttu-id="8b233-104">Utwórz plik o nazwie **composer.json** w hello katalogu głównym projektu i dodać powitania po tooit kodu:</span><span class="sxs-lookup"><span data-stu-id="8b233-104">Create a file named **composer.json** in hello root of your project and add hello following code tooit:</span></span>
   
    ```json
    {
      "require": {
        "microsoft/windowsazure": "^0.4"
      }
    }
    ```
3. <span data-ttu-id="8b233-105">Pobierz  **[composer.phar] [ composer-phar]**  w katalogu głównym projektu.</span><span class="sxs-lookup"><span data-stu-id="8b233-105">Download **[composer.phar][composer-phar]** in your project root.</span></span>
4. <span data-ttu-id="8b233-106">Otwórz wiersz polecenia i wykonaj następujące polecenie w katalogu głównym projektu hello</span><span class="sxs-lookup"><span data-stu-id="8b233-106">Open a command prompt and execute hello following command in your project root</span></span>
   
    ```
    php composer.phar install
    ```

[php-sdk-github]: http://go.microsoft.com/fwlink/?LinkId=252719
[install-git]: http://git-scm.com/book/en/Getting-Started-Installing-Git
[download-SDK-PHP]: ../articles/php-download-sdk.md
[composer-phar]: http://getcomposer.org/composer.phar
