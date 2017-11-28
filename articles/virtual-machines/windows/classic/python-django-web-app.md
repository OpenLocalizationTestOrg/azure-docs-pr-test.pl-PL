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
# <a name="django-hello-world-web-app-on-a-windows-server-vm"></a><span data-ttu-id="1d7e2-103">Aplikacja sieci web Django Hello World na maszynie Wirtualnej systemu Windows Server</span><span class="sxs-lookup"><span data-stu-id="1d7e2-103">Django Hello World web app on a Windows Server VM</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="1d7e2-104">Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [usługi Azure Resource Manager i hello klasycznego modelu wdrażania](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="1d7e2-104">Azure has two different deployment models for creating and working with resources: [Azure Resource Manager and hello classic deployment model](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="1d7e2-105">W tym artykule opisano hello klasycznego modelu wdrażania.</span><span class="sxs-lookup"><span data-stu-id="1d7e2-105">This article describes hello classic deployment model.</span></span> <span data-ttu-id="1d7e2-106">Zaleca się, że większości nowych wdrożeń Użyj modelu Resource Manager hello.</span><span class="sxs-lookup"><span data-stu-id="1d7e2-106">We recommend that most new deployments use hello Resource Manager model.</span></span>

<span data-ttu-id="1d7e2-107">W tym samouczku przedstawiono sposób toohost witryny sieci Web na podstawie Django w systemie Windows Server w maszynach wirtualnych platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="1d7e2-107">This tutorial shows you how toohost a Django-based website in Windows Server in Azure Virtual Machines.</span></span> <span data-ttu-id="1d7e2-108">W samouczku hello przyjęto założenie, nie już pewne doświadczenie w systemie Azure.</span><span class="sxs-lookup"><span data-stu-id="1d7e2-108">In hello tutorial, we assume no prior experience with Azure.</span></span> <span data-ttu-id="1d7e2-109">Po zakończeniu samouczka hello może mieć aplikacji opartej na Django w górę i w chmurze hello.</span><span class="sxs-lookup"><span data-stu-id="1d7e2-109">When you finish hello tutorial, you can have a Django-based application up and running in hello cloud.</span></span>

<span data-ttu-id="1d7e2-110">Instrukcje:</span><span class="sxs-lookup"><span data-stu-id="1d7e2-110">Learn how to:</span></span>

* <span data-ttu-id="1d7e2-111">Konfigurowanie maszyny wirtualnej platformy Azure toohost Django.</span><span class="sxs-lookup"><span data-stu-id="1d7e2-111">Set up an Azure virtual machine toohost Django.</span></span> <span data-ttu-id="1d7e2-112">Mimo że w tym samouczku opisano sposób toodo dla **systemu Windows Server**, możesz zrobić hello takie same dla maszyny Wirtualnej systemu Linux hostowanych w systemie Azure.</span><span class="sxs-lookup"><span data-stu-id="1d7e2-112">Although this tutorial explains how toodo this for **Windows Server**, you can do hello same for a Linux VM hosted in Azure.</span></span>
* <span data-ttu-id="1d7e2-113">Utwórz nową aplikację Django w systemie Windows.</span><span class="sxs-lookup"><span data-stu-id="1d7e2-113">Create a new Django application in Windows.</span></span>

<span data-ttu-id="1d7e2-114">Witaj samouczek pokazuje, jak aplikacja sieci web toobuild podstawowe Hello World.</span><span class="sxs-lookup"><span data-stu-id="1d7e2-114">hello tutorial shows you how toobuild a basic Hello World web application.</span></span> <span data-ttu-id="1d7e2-115">Aplikacja Hello jest hostowana na maszynie wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="1d7e2-115">hello application is hosted in an Azure virtual machine.</span></span>

<span data-ttu-id="1d7e2-116">powitania po zrzut ekranu przedstawia aplikacji hello zakończone:</span><span class="sxs-lookup"><span data-stu-id="1d7e2-116">hello following screenshot shows hello completed application:</span></span>

![Okno przeglądarki Wyświetla hello hello world strony na platformie Azure][1]

[!INCLUDE [create-account-and-vms-note](../../../../includes/create-account-and-vms-note.md)]

## <a name="create-and-set-up-an-azure-virtual-machine-toohost-django"></a><span data-ttu-id="1d7e2-118">Tworzenie i konfigurowanie maszyny wirtualnej platformy Azure toohost Django</span><span class="sxs-lookup"><span data-stu-id="1d7e2-118">Create and set up an Azure virtual machine toohost Django</span></span>

1. <span data-ttu-id="1d7e2-119">toocreate maszyny wirtualnej platformy Azure z hello dystrybucji systemu Windows Server 2012 R2 Datacenter, zobacz [Utwórz maszynę wirtualną z systemem Windows w portalu Azure hello](tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="1d7e2-119">toocreate an Azure virtual machine with hello Windows Server 2012 R2 Datacenter distribution, see [Create a virtual machine running Windows in hello Azure portal](tutorial.md).</span></span>
2. <span data-ttu-id="1d7e2-120">Ustaw ruch na porcie 80 Azure toodirect z hello web tooport 80 na maszynie wirtualnej hello:</span><span class="sxs-lookup"><span data-stu-id="1d7e2-120">Set Azure toodirect port 80 traffic from hello web tooport 80 on hello virtual machine:</span></span>
   
   1. <span data-ttu-id="1d7e2-121">W hello portalu Azure przejdź do pulpitu nawigacyjnego toohello i wybierz nowo utworzony maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="1d7e2-121">In hello Azure portal, go toohello dashboard and select your newly created virtual machine.</span></span>
   2. <span data-ttu-id="1d7e2-122">Kliknij kolejno opcje **Punkty końcowe** i **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="1d7e2-122">Click **Endpoints**, and then click **Add**.</span></span>

     ![Dodawanie punktu końcowego](./media/python-django-web-app/django-helloworld-add-endpoint-new-portal.png)

   3. <span data-ttu-id="1d7e2-124">Na powitania **dodać punkt końcowy** strony, dla **nazwa**, wprowadź **HTTP**.</span><span class="sxs-lookup"><span data-stu-id="1d7e2-124">On hello **Add endpoint** page, for **Name**, enter **HTTP**.</span></span> <span data-ttu-id="1d7e2-125">Ustaw hello publicznych i prywatnych portów TCP za**80**.</span><span class="sxs-lookup"><span data-stu-id="1d7e2-125">Set hello public and private TCP ports too**80**.</span></span>

     ![Wprowadź nazwę i Ustaw porty publiczny i prywatny](./media/python-django-web-app/django-helloworld-add-endpoint-set-ports-new-portal.png)

   4. <span data-ttu-id="1d7e2-127">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="1d7e2-127">Click **OK**.</span></span>
     
3. <span data-ttu-id="1d7e2-128">Na pulpicie nawigacyjnym hello wybierz maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="1d7e2-128">In hello dashboard, select your VM.</span></span> <span data-ttu-id="1d7e2-129">toouse protokołu RDP (Remote Desktop) tooremotely logowania toohello nowo tworzone maszyny wirtualnej Azure, kliknij przycisk **Connect**.</span><span class="sxs-lookup"><span data-stu-id="1d7e2-129">toouse Remote Desktop Protocol (RDP) tooremotely sign in toohello newly created Azure virtual machine, click **Connect**.</span></span>  

> [!IMPORTANT] 
> <span data-ttu-id="1d7e2-130">Witaj, postępując zgodnie z instrukcjami założono, poprawnie podpisane toohello maszynie wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="1d7e2-130">hello following instructions assume that you signed in toohello virtual machine correctly.</span></span> <span data-ttu-id="1d7e2-131">One założono, że są wydawania polecenia hello maszyny wirtualnej, a nie na komputerze lokalnym.</span><span class="sxs-lookup"><span data-stu-id="1d7e2-131">They also assume that you are issuing commands in hello virtual machine and not on your local computer.</span></span>

## <span data-ttu-id="1d7e2-132"><a id="setup"></a>Instalacji języka Python, Django i WFastCGI</span><span class="sxs-lookup"><span data-stu-id="1d7e2-132"><a id="setup"> </a>Install Python, Django, and WFastCGI</span></span>
> [!NOTE]
> <span data-ttu-id="1d7e2-133">toodownload przy użyciu programu Internet Explorer, może być tooconfigure programu Internet Explorer **Konfiguracja zwiększonych zabezpieczeń** ustawienia.</span><span class="sxs-lookup"><span data-stu-id="1d7e2-133">toodownload by using Internet Explorer, you might have tooconfigure Internet Explorer **Enhanced Security Configuration** settings.</span></span> <span data-ttu-id="1d7e2-134">toodo tego, kliknij **Start** > **narzędzia administracyjne** > **Menedżera serwera** > **serweralokalnego**.</span><span class="sxs-lookup"><span data-stu-id="1d7e2-134">toodo this, click **Start** > **Administrative Tools** > **Server Manager** > **Local Server**.</span></span> <span data-ttu-id="1d7e2-135">Kliknij przycisk **Konfiguracja zwiększonych zabezpieczeń**, a następnie wybierz **poza**.</span><span class="sxs-lookup"><span data-stu-id="1d7e2-135">Click **IE Enhanced Security Configuration**, and then select **Off**.</span></span>

1. <span data-ttu-id="1d7e2-136">Zainstaluj najnowsze wersje Python 2.7 lub 3.4 Python z hello [python.org][python.org].</span><span class="sxs-lookup"><span data-stu-id="1d7e2-136">Install hello latest versions of Python 2.7 or Python 3.4 from [python.org][python.org].</span></span>
2. <span data-ttu-id="1d7e2-137">Zainstaluj pakiety wfastcgi i django hello przy użyciu narzędzia pip.</span><span class="sxs-lookup"><span data-stu-id="1d7e2-137">Install hello wfastcgi and django packages using pip.</span></span>
   
    <span data-ttu-id="1d7e2-138">Dla języka Python 2.7 użyj hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="1d7e2-138">For Python 2.7, use hello following command:</span></span>
   
        c:\python27\scripts\pip install wfastcgi
        c:\python27\scripts\pip install django
   
    <span data-ttu-id="1d7e2-139">Dla języka Python 3.4 Użyj hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="1d7e2-139">For Python 3.4, use hello following command:</span></span>
   
        c:\python34\scripts\pip install wfastcgi
        c:\python34\scripts\pip install django

## <a name="install-iis-with-fastcgi"></a><span data-ttu-id="1d7e2-140">Instalowanie usług IIS przy użyciu FastCGI</span><span class="sxs-lookup"><span data-stu-id="1d7e2-140">Install IIS with FastCGI</span></span>
* <span data-ttu-id="1d7e2-141">Zainstaluj usługi Internet Information Services (IIS) z obsługą FastCGI.</span><span class="sxs-lookup"><span data-stu-id="1d7e2-141">Install Internet Information Services (IIS) with FastCGI support.</span></span> <span data-ttu-id="1d7e2-142">Może to potrwać kilka minut tooexecute.</span><span class="sxs-lookup"><span data-stu-id="1d7e2-142">This might take several minutes tooexecute.</span></span>
   
        start /wait %windir%\System32\PkgMgr.exe /iu:IIS-WebServerRole;IIS-WebServer;IIS-CommonHttpFeatures;IIS-StaticContent;IIS-DefaultDocument;IIS-DirectoryBrowsing;IIS-HttpErrors;IIS-HealthAndDiagnostics;IIS-HttpLogging;IIS-LoggingLibraries;IIS-RequestMonitor;IIS-Security;IIS-RequestFiltering;IIS-HttpCompressionStatic;IIS-WebServerManagementTools;IIS-ManagementConsole;WAS-WindowsActivationService;WAS-ProcessModel;WAS-NetFxEnvironment;WAS-ConfigurationAPI;IIS-CGI

## <a name="create-a-new-django-application"></a><span data-ttu-id="1d7e2-143">Utwórz nową aplikację Django</span><span class="sxs-lookup"><span data-stu-id="1d7e2-143">Create a new Django application</span></span>
1. <span data-ttu-id="1d7e2-144">W C:\inetpub\wwwroot toocreate nowy projekt Django, wprowadź następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="1d7e2-144">In C:\inetpub\wwwroot, toocreate a new Django project, enter hello following command:</span></span>
   
   <span data-ttu-id="1d7e2-145">Dla języka Python 2.7 użyj hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="1d7e2-145">For Python 2.7, use hello following command:</span></span>
   
       C:\Python27\Scripts\django-admin.exe startproject helloworld
   
   <span data-ttu-id="1d7e2-146">Dla języka Python 3.4 Użyj hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="1d7e2-146">For Python 3.4, use hello following command:</span></span>
   
       C:\Python34\Scripts\django-admin.exe startproject helloworld
   
   ![wynik Hello polecenia hello New-AzureService](./media/python-django-web-app/django-helloworld-cmd-new-azure-service.png)
2. <span data-ttu-id="1d7e2-148">Witaj `django-admin` polecenia wygenerowanie podstawowej struktury witryn skonstruowanych na podstawie Django:</span><span class="sxs-lookup"><span data-stu-id="1d7e2-148">hello `django-admin` command generates a basic structure for Django-based websites:</span></span>
   
   * <span data-ttu-id="1d7e2-149">`helloworld\manage.py`pomaga rozpocząć hosting i Zatrzymaj hosting witryny sieci Web na podstawie Django.</span><span class="sxs-lookup"><span data-stu-id="1d7e2-149">`helloworld\manage.py` helps you start hosting and stop hosting your Django-based website.</span></span>
   * <span data-ttu-id="1d7e2-150">`helloworld\helloworld\settings.py`zawiera ustawienia Django dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1d7e2-150">`helloworld\helloworld\settings.py` has Django settings for your application.</span></span>
   * <span data-ttu-id="1d7e2-151">`helloworld\helloworld\urls.py`nie ma kodu mapowania hello między każdego adresu URL i jego widoku.</span><span class="sxs-lookup"><span data-stu-id="1d7e2-151">`helloworld\helloworld\urls.py` has hello mapping code between each URL and its view.</span></span>
3. <span data-ttu-id="1d7e2-152">W katalogu C:\inetpub\wwwroot\helloworld\helloworld hello Utwórz nowy plik o nazwie views.py.</span><span class="sxs-lookup"><span data-stu-id="1d7e2-152">In hello C:\inetpub\wwwroot\helloworld\helloworld directory, create a new file named views.py.</span></span> <span data-ttu-id="1d7e2-153">Ten plik zawiera widok hello, który renderuje stronę "hello world" hello.</span><span class="sxs-lookup"><span data-stu-id="1d7e2-153">This file has hello view that renders hello "hello world" page.</span></span> <span data-ttu-id="1d7e2-154">W edytorze kodu wprowadź hello następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="1d7e2-154">In your code editor, enter hello following commands:</span></span>
   
       from django.http import HttpResponse
       def home(request):
           html = "<html><body>Hello World!</body></html>"
           return HttpResponse(html)
4. <span data-ttu-id="1d7e2-155">Zastąp zawartość pliku urls.py hello hello hello następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="1d7e2-155">Replace hello contents of hello urls.py file with hello following commands:</span></span>
   
       from django.conf.urls import patterns, url
       urlpatterns = patterns('',
           url(r'^$', 'helloworld.views.home', name='home'),
       )

## <a name="set-up-iis"></a><span data-ttu-id="1d7e2-156">Konfigurowanie usług IIS</span><span class="sxs-lookup"><span data-stu-id="1d7e2-156">Set up IIS</span></span>
1. <span data-ttu-id="1d7e2-157">W pliku applicationhost.config globalne hello odblokować hello obsługi sekcji.</span><span class="sxs-lookup"><span data-stu-id="1d7e2-157">In hello global applicationhost.config file, unlock hello handlers section.</span></span>  <span data-ttu-id="1d7e2-158">Umożliwia to obsługę plików Python hello toouse Twojego pliku web.config.</span><span class="sxs-lookup"><span data-stu-id="1d7e2-158">This allows your web.config file toouse hello Python handler.</span></span> <span data-ttu-id="1d7e2-159">Dodaj to polecenie:</span><span class="sxs-lookup"><span data-stu-id="1d7e2-159">Add this command:</span></span>
   
        %windir%\system32\inetsrv\appcmd unlock config -section:system.webServer/handlers
2. <span data-ttu-id="1d7e2-160">Aktywacja WFastCGI.</span><span class="sxs-lookup"><span data-stu-id="1d7e2-160">Activate WFastCGI.</span></span> <span data-ttu-id="1d7e2-161">Spowoduje to dodanie pliku applicationhost.config globalne toohello aplikacji, który odwołuje się tooyour interpreter plik wykonywalny i hello wfastcgi.py skrypt w języku Python.</span><span class="sxs-lookup"><span data-stu-id="1d7e2-161">This adds an application toohello global applicationhost.config file, which refers tooyour Python interpreter executable and hello wfastcgi.py script.</span></span>
   
    <span data-ttu-id="1d7e2-162">W języku Python 2.7:</span><span class="sxs-lookup"><span data-stu-id="1d7e2-162">In Python 2.7:</span></span>
   
        C:\python27\scripts\wfastcgi-enable
   
    <span data-ttu-id="1d7e2-163">W języku Python 3.4:</span><span class="sxs-lookup"><span data-stu-id="1d7e2-163">In Python 3.4:</span></span>
   
        C:\python34\scripts\wfastcgi-enable
3. <span data-ttu-id="1d7e2-164">W C:\inetpub\wwwroot\helloworld Utwórz plik web.config.</span><span class="sxs-lookup"><span data-stu-id="1d7e2-164">In C:\inetpub\wwwroot\helloworld, create a web.config file.</span></span> <span data-ttu-id="1d7e2-165">Witaj wartość hello `scriptProcessor` atrybutu powinna być zgodna hello dane wyjściowe hello poprzedzających krok.</span><span class="sxs-lookup"><span data-stu-id="1d7e2-165">hello value of hello `scriptProcessor` attribute should match hello output from hello preceding step.</span></span> <span data-ttu-id="1d7e2-166">Aby uzyskać więcej informacji o ustawieniu wfastcgi hello, zobacz [pypi wfastcgi][wfastcgi].</span><span class="sxs-lookup"><span data-stu-id="1d7e2-166">For more information about hello wfastcgi setting, see [pypi wfastcgi][wfastcgi].</span></span>
   
   <span data-ttu-id="1d7e2-167">W języku Python 2.7:</span><span class="sxs-lookup"><span data-stu-id="1d7e2-167">In  Python 2.7:</span></span>
   
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
   
   <span data-ttu-id="1d7e2-168">W języku Python 3.4:</span><span class="sxs-lookup"><span data-stu-id="1d7e2-168">In  Python 3.4:</span></span>
   
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
4. <span data-ttu-id="1d7e2-169">Aktualizacja lokalizacji hello hello IIS domyślnej witryny sieci Web toopoint toohello Django projektu folderu:</span><span class="sxs-lookup"><span data-stu-id="1d7e2-169">Update hello location of hello IIS default website toopoint toohello Django project folder:</span></span>
   
        %windir%\system32\inetsrv\appcmd set vdir "Default Web Site/" -physicalPath:"C:\inetpub\wwwroot\helloworld"
5. <span data-ttu-id="1d7e2-170">Załaduj hello strony sieci Web w przeglądarce.</span><span class="sxs-lookup"><span data-stu-id="1d7e2-170">Load hello webpage in your browser.</span></span>

![Okno przeglądarki Wyświetla hello hello world strony na platformie Azure][1]

## <a name="shut-down-your-azure-virtual-machine"></a><span data-ttu-id="1d7e2-172">Zamknij maszynę wirtualną z platformy Azure</span><span class="sxs-lookup"><span data-stu-id="1d7e2-172">Shut down your Azure virtual machine</span></span>
<span data-ttu-id="1d7e2-173">Po zakończeniu korzystania z tego samouczka, firma Microsoft zaleca zamknięcie lub usunąć hello utworzone w samouczku hello maszyny Wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="1d7e2-173">When you're done with this tutorial, we recommend that you shut down or remove hello Azure VM you created for hello tutorial.</span></span> <span data-ttu-id="1d7e2-174">Spowoduje to zwolnienie zasobów dla innych samouczków, a można uniknąć naliczania opłat użycia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="1d7e2-174">This frees up resources for other tutorials, and you can avoid incurring Azure usage charges.</span></span>

[1]: ./media/python-django-web-app/django-helloworld-browser-azure.png

[port80]: ./media/python-django-web-app/django-helloworld-port80.png

[Web Platform Installer]: http://www.microsoft.com/web/downloads/platform.aspx
[python.org]: https://www.python.org/downloads/
[wfastcgi]: https://pypi.python.org/pypi/wfastcgi
