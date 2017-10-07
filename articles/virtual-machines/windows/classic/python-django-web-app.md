---
title: Aplikacja sieci web aaaDjango na maszynie Wirtualnej Azure z systemem Windows Server | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak toohost Django witryny sieci Web opartej na platformie Azure przy użyciu systemu Windows Server 2012 R2 Datacenter Maszynę wirtualną z hello klasycznego modelu wdrażania."
services: virtual-machines-windows
documentationcenter: python
author: huguesv
manager: wpickett
editor: 
tags: azure-service-management
ms.assetid: e36484d1-afbf-47f5-b755-5e65397dc1c3
ms.service: virtual-machines-windows
ms.workload: web
ms.tgt_pltfrm: vm-windows
ms.devlang: python
ms.topic: article
ms.date: 05/31/2017
ms.author: huvalo
ms.openlocfilehash: 55847e3c6d6769965be29077e8d4eeebad914637
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="django-hello-world-web-app-on-a-windows-server-vm"></a>Aplikacja sieci web Django Hello World na maszynie Wirtualnej systemu Windows Server

> [!IMPORTANT] 
> Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [usługi Azure Resource Manager i hello klasycznego modelu wdrażania](../../../resource-manager-deployment-model.md). W tym artykule opisano hello klasycznego modelu wdrażania. Zaleca się, że większości nowych wdrożeń Użyj modelu Resource Manager hello.

W tym samouczku przedstawiono sposób toohost witryny sieci Web na podstawie Django w systemie Windows Server w maszynach wirtualnych platformy Azure. W samouczku hello przyjęto założenie, nie już pewne doświadczenie w systemie Azure. Po zakończeniu samouczka hello może mieć aplikacji opartej na Django w górę i w chmurze hello.

Instrukcje:

* Konfigurowanie maszyny wirtualnej platformy Azure toohost Django. Mimo że w tym samouczku opisano sposób toodo dla **systemu Windows Server**, możesz zrobić hello takie same dla maszyny Wirtualnej systemu Linux hostowanych w systemie Azure.
* Utwórz nową aplikację Django w systemie Windows.

Witaj samouczek pokazuje, jak aplikacja sieci web toobuild podstawowe Hello World. Aplikacja Hello jest hostowana na maszynie wirtualnej platformy Azure.

powitania po zrzut ekranu przedstawia aplikacji hello zakończone:

![Okno przeglądarki Wyświetla hello hello world strony na platformie Azure][1]

[!INCLUDE [create-account-and-vms-note](../../../../includes/create-account-and-vms-note.md)]

## <a name="create-and-set-up-an-azure-virtual-machine-toohost-django"></a>Tworzenie i konfigurowanie maszyny wirtualnej platformy Azure toohost Django

1. toocreate maszyny wirtualnej platformy Azure z hello dystrybucji systemu Windows Server 2012 R2 Datacenter, zobacz [Utwórz maszynę wirtualną z systemem Windows w portalu Azure hello](tutorial.md).
2. Ustaw ruch na porcie 80 Azure toodirect z hello web tooport 80 na maszynie wirtualnej hello:
   
   1. W hello portalu Azure przejdź do pulpitu nawigacyjnego toohello i wybierz nowo utworzony maszyny wirtualnej.
   2. Kliknij kolejno opcje **Punkty końcowe** i **Dodaj**.

     ![Dodawanie punktu końcowego](./media/python-django-web-app/django-helloworld-add-endpoint-new-portal.png)

   3. Na powitania **dodać punkt końcowy** strony, dla **nazwa**, wprowadź **HTTP**. Ustaw hello publicznych i prywatnych portów TCP za**80**.

     ![Wprowadź nazwę i Ustaw porty publiczny i prywatny](./media/python-django-web-app/django-helloworld-add-endpoint-set-ports-new-portal.png)

   4. Kliknij przycisk **OK**.
     
3. Na pulpicie nawigacyjnym hello wybierz maszyny Wirtualnej. toouse protokołu RDP (Remote Desktop) tooremotely logowania toohello nowo tworzone maszyny wirtualnej Azure, kliknij przycisk **Connect**.  

> [!IMPORTANT] 
> Witaj, postępując zgodnie z instrukcjami założono, poprawnie podpisane toohello maszynie wirtualnej. One założono, że są wydawania polecenia hello maszyny wirtualnej, a nie na komputerze lokalnym.

## <a id="setup"></a>Instalacji języka Python, Django i WFastCGI
> [!NOTE]
> toodownload przy użyciu programu Internet Explorer, może być tooconfigure programu Internet Explorer **Konfiguracja zwiększonych zabezpieczeń** ustawienia. toodo tego, kliknij **Start** > **narzędzia administracyjne** > **Menedżera serwera** > **serweralokalnego**. Kliknij przycisk **Konfiguracja zwiększonych zabezpieczeń**, a następnie wybierz **poza**.

1. Zainstaluj najnowsze wersje Python 2.7 lub 3.4 Python z hello [python.org][python.org].
2. Zainstaluj pakiety wfastcgi i django hello przy użyciu narzędzia pip.
   
    Dla języka Python 2.7 użyj hello następujące polecenie:
   
        c:\python27\scripts\pip install wfastcgi
        c:\python27\scripts\pip install django
   
    Dla języka Python 3.4 Użyj hello następujące polecenie:
   
        c:\python34\scripts\pip install wfastcgi
        c:\python34\scripts\pip install django

## <a name="install-iis-with-fastcgi"></a>Instalowanie usług IIS przy użyciu FastCGI
* Zainstaluj usługi Internet Information Services (IIS) z obsługą FastCGI. Może to potrwać kilka minut tooexecute.
   
        start /wait %windir%\System32\PkgMgr.exe /iu:IIS-WebServerRole;IIS-WebServer;IIS-CommonHttpFeatures;IIS-StaticContent;IIS-DefaultDocument;IIS-DirectoryBrowsing;IIS-HttpErrors;IIS-HealthAndDiagnostics;IIS-HttpLogging;IIS-LoggingLibraries;IIS-RequestMonitor;IIS-Security;IIS-RequestFiltering;IIS-HttpCompressionStatic;IIS-WebServerManagementTools;IIS-ManagementConsole;WAS-WindowsActivationService;WAS-ProcessModel;WAS-NetFxEnvironment;WAS-ConfigurationAPI;IIS-CGI

## <a name="create-a-new-django-application"></a>Utwórz nową aplikację Django
1. W C:\inetpub\wwwroot toocreate nowy projekt Django, wprowadź następujące polecenie hello:
   
   Dla języka Python 2.7 użyj hello następujące polecenie:
   
       C:\Python27\Scripts\django-admin.exe startproject helloworld
   
   Dla języka Python 3.4 Użyj hello następujące polecenie:
   
       C:\Python34\Scripts\django-admin.exe startproject helloworld
   
   ![wynik Hello polecenia hello New-AzureService](./media/python-django-web-app/django-helloworld-cmd-new-azure-service.png)
2. Witaj `django-admin` polecenia wygenerowanie podstawowej struktury witryn skonstruowanych na podstawie Django:
   
   * `helloworld\manage.py`pomaga rozpocząć hosting i Zatrzymaj hosting witryny sieci Web na podstawie Django.
   * `helloworld\helloworld\settings.py`zawiera ustawienia Django dla aplikacji.
   * `helloworld\helloworld\urls.py`nie ma kodu mapowania hello między każdego adresu URL i jego widoku.
3. W katalogu C:\inetpub\wwwroot\helloworld\helloworld hello Utwórz nowy plik o nazwie views.py. Ten plik zawiera widok hello, który renderuje stronę "hello world" hello. W edytorze kodu wprowadź hello następującego polecenia:
   
       from django.http import HttpResponse
       def home(request):
           html = "<html><body>Hello World!</body></html>"
           return HttpResponse(html)
4. Zastąp zawartość pliku urls.py hello hello hello następującego polecenia:
   
       from django.conf.urls import patterns, url
       urlpatterns = patterns('',
           url(r'^$', 'helloworld.views.home', name='home'),
       )

## <a name="set-up-iis"></a>Konfigurowanie usług IIS
1. W pliku applicationhost.config globalne hello odblokować hello obsługi sekcji.  Umożliwia to obsługę plików Python hello toouse Twojego pliku web.config. Dodaj to polecenie:
   
        %windir%\system32\inetsrv\appcmd unlock config -section:system.webServer/handlers
2. Aktywacja WFastCGI. Spowoduje to dodanie pliku applicationhost.config globalne toohello aplikacji, który odwołuje się tooyour interpreter plik wykonywalny i hello wfastcgi.py skrypt w języku Python.
   
    W języku Python 2.7:
   
        C:\python27\scripts\wfastcgi-enable
   
    W języku Python 3.4:
   
        C:\python34\scripts\wfastcgi-enable
3. W C:\inetpub\wwwroot\helloworld Utwórz plik web.config. Witaj wartość hello `scriptProcessor` atrybutu powinna być zgodna hello dane wyjściowe hello poprzedzających krok. Aby uzyskać więcej informacji o ustawieniu wfastcgi hello, zobacz [pypi wfastcgi][wfastcgi].
   
   W języku Python 2.7:
   
        <configuration>
          <appSettings>
            <add key="WSGI_HANDLER" value="django.core.handlers.wsgi.WSGIHandler()" />
            <add key="PYTHONPATH" value="C:\inetpub\wwwroot\helloworld" />
            <add key="DJANGO_SETTINGS_MODULE" value="helloworld.settings" />
          </appSettings>
          <system.webServer>
            <handlers>
                <add name="Python FastCGI" path="*" verb="*" modules="FastCgiModule" scriptProcessor="C:\Python27\python.exe|C:\Python27\Lib\site-packages\wfastcgi.pyc" resourceType="Unspecified" />
            </handlers>
          </system.webServer>
        </configuration>
   
   W języku Python 3.4:
   
        <configuration>
          <appSettings>
            <add key="WSGI_HANDLER" value="django.core.handlers.wsgi.WSGIHandler()" />
            <add key="PYTHONPATH" value="C:\inetpub\wwwroot\helloworld" />
            <add key="DJANGO_SETTINGS_MODULE" value="helloworld.settings" />
          </appSettings>
          <system.webServer>
            <handlers>
                <add name="Python FastCGI" path="*" verb="*" modules="FastCgiModule" scriptProcessor="C:\Python34\python.exe|C:\Python34\Lib\site-packages\wfastcgi.py" resourceType="Unspecified" />
            </handlers>
          </system.webServer>
        </configuration>
4. Aktualizacja lokalizacji hello hello IIS domyślnej witryny sieci Web toopoint toohello Django projektu folderu:
   
        %windir%\system32\inetsrv\appcmd set vdir "Default Web Site/" -physicalPath:"C:\inetpub\wwwroot\helloworld"
5. Załaduj hello strony sieci Web w przeglądarce.

![Okno przeglądarki Wyświetla hello hello world strony na platformie Azure][1]

## <a name="shut-down-your-azure-virtual-machine"></a>Zamknij maszynę wirtualną z platformy Azure
Po zakończeniu korzystania z tego samouczka, firma Microsoft zaleca zamknięcie lub usunąć hello utworzone w samouczku hello maszyny Wirtualnej platformy Azure. Spowoduje to zwolnienie zasobów dla innych samouczków, a można uniknąć naliczania opłat użycia platformy Azure.

[1]: ./media/python-django-web-app/django-helloworld-browser-azure.png

[port80]: ./media/python-django-web-app/django-helloworld-port80.png

[Web Platform Installer]: http://www.microsoft.com/web/downloads/platform.aspx
[python.org]: https://www.python.org/downloads/
[wfastcgi]: https://pypi.python.org/pypi/wfastcgi
