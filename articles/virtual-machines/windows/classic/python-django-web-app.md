---
title: Aplikacja sieci web Django na maszynie Wirtualnej Azure z systemem Windows Server | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak hostowanie witryny sieci Web na podstawie Django na platformie Azure przy użyciu systemu Windows Server 2012 R2 Datacenter Maszynę wirtualną z klasycznym modelu wdrażania."
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
ms.openlocfilehash: 283a296fb39863c2801be1093cc4f56904786abd
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="django-hello-world-web-app-on-a-windows-server-vm"></a><span data-ttu-id="ffac8-103">Aplikacja sieci web Django Hello World na maszynie Wirtualnej systemu Windows Server</span><span class="sxs-lookup"><span data-stu-id="ffac8-103">Django Hello World web app on a Windows Server VM</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="ffac8-104">Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [usługi Azure Resource Manager i klasycznym modelu wdrażania](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="ffac8-104">Azure has two different deployment models for creating and working with resources: [Azure Resource Manager and the classic deployment model](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="ffac8-105">W tym artykule opisano klasycznym modelu wdrażania.</span><span class="sxs-lookup"><span data-stu-id="ffac8-105">This article describes the classic deployment model.</span></span> <span data-ttu-id="ffac8-106">Zaleca się, że większości nowych wdrożeń Użyj modelu Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="ffac8-106">We recommend that most new deployments use the Resource Manager model.</span></span>

<span data-ttu-id="ffac8-107">W tym samouczku przedstawiono sposób hosta witryny sieci Web na podstawie Django w systemie Windows Server w maszynach wirtualnych platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="ffac8-107">This tutorial shows you how to host a Django-based website in Windows Server in Azure Virtual Machines.</span></span> <span data-ttu-id="ffac8-108">W samouczku przyjęto założenie, nie już pewne doświadczenie w systemie Azure.</span><span class="sxs-lookup"><span data-stu-id="ffac8-108">In the tutorial, we assume no prior experience with Azure.</span></span> <span data-ttu-id="ffac8-109">Po zakończeniu samouczka może mieć aplikacji opartej na Django w górę i w chmurze.</span><span class="sxs-lookup"><span data-stu-id="ffac8-109">When you finish the tutorial, you can have a Django-based application up and running in the cloud.</span></span>

<span data-ttu-id="ffac8-110">Instrukcje:</span><span class="sxs-lookup"><span data-stu-id="ffac8-110">Learn how to:</span></span>

* <span data-ttu-id="ffac8-111">Skonfiguruj maszynę wirtualną platformy Azure do hosta Django.</span><span class="sxs-lookup"><span data-stu-id="ffac8-111">Set up an Azure virtual machine to host Django.</span></span> <span data-ttu-id="ffac8-112">Mimo że w tym samouczku wyjaśniono, jak to zrobić w **systemu Windows Server**, można wykonać takie same dla maszyny Wirtualnej systemu Linux hostowanych w systemie Azure.</span><span class="sxs-lookup"><span data-stu-id="ffac8-112">Although this tutorial explains how to do this for **Windows Server**, you can do the same for a Linux VM hosted in Azure.</span></span>
* <span data-ttu-id="ffac8-113">Utwórz nową aplikację Django w systemie Windows.</span><span class="sxs-lookup"><span data-stu-id="ffac8-113">Create a new Django application in Windows.</span></span>

<span data-ttu-id="ffac8-114">Samouczek przedstawia sposób tworzenia podstawowej aplikacji sieci web Hello World.</span><span class="sxs-lookup"><span data-stu-id="ffac8-114">The tutorial shows you how to build a basic Hello World web application.</span></span> <span data-ttu-id="ffac8-115">Aplikacja znajduje się w maszynie wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="ffac8-115">The application is hosted in an Azure virtual machine.</span></span>

<span data-ttu-id="ffac8-116">Poniższy zrzut ekranu przedstawia gotową aplikację:</span><span class="sxs-lookup"><span data-stu-id="ffac8-116">The following screenshot shows the completed application:</span></span>

![Oknie przeglądarki zostanie wyświetlona strona world hello na platformie Azure][1]

[!INCLUDE [create-account-and-vms-note](../../../../includes/create-account-and-vms-note.md)]

## <a name="create-and-set-up-an-azure-virtual-machine-to-host-django"></a><span data-ttu-id="ffac8-118">Tworzenie i konfigurowanie maszyny wirtualnej platformy Azure na hoście Django</span><span class="sxs-lookup"><span data-stu-id="ffac8-118">Create and set up an Azure virtual machine to host Django</span></span>

1. <span data-ttu-id="ffac8-119">Aby utworzyć maszynę wirtualną platformy Azure z rozkładem systemu Windows Server 2012 R2 Datacenter, zobacz [Utwórz maszynę wirtualną z systemem Windows w portalu Azure](tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="ffac8-119">To create an Azure virtual machine with the Windows Server 2012 R2 Datacenter distribution, see [Create a virtual machine running Windows in the Azure portal](tutorial.md).</span></span>
2. <span data-ttu-id="ffac8-120">Ustaw Azure, aby kierować port 80 ruch z sieci web do portu 80 w maszynie wirtualnej:</span><span class="sxs-lookup"><span data-stu-id="ffac8-120">Set Azure to direct port 80 traffic from the web to port 80 on the virtual machine:</span></span>
   
   1. <span data-ttu-id="ffac8-121">W portalu Azure przejdź do pulpitu nawigacyjnego, a następnie wybierz nowo utworzony maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="ffac8-121">In the Azure portal, go to the dashboard and select your newly created virtual machine.</span></span>
   2. <span data-ttu-id="ffac8-122">Kliknij kolejno opcje **Punkty końcowe** i **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="ffac8-122">Click **Endpoints**, and then click **Add**.</span></span>

     ![Dodawanie punktu końcowego](./media/python-django-web-app/django-helloworld-add-endpoint-new-portal.png)

   3. <span data-ttu-id="ffac8-124">Na **dodać punkt końcowy** strony, dla **nazwa**, wprowadź **HTTP**.</span><span class="sxs-lookup"><span data-stu-id="ffac8-124">On the **Add endpoint** page, for **Name**, enter **HTTP**.</span></span> <span data-ttu-id="ffac8-125">Ustaw portów TCP publiczne i prywatne **80**.</span><span class="sxs-lookup"><span data-stu-id="ffac8-125">Set the public and private TCP ports to **80**.</span></span>

     ![Wprowadź nazwę i Ustaw porty publiczny i prywatny](./media/python-django-web-app/django-helloworld-add-endpoint-set-ports-new-portal.png)

   4. <span data-ttu-id="ffac8-127">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="ffac8-127">Click **OK**.</span></span>
     
3. <span data-ttu-id="ffac8-128">Na pulpicie nawigacyjnym wybierz maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="ffac8-128">In the dashboard, select your VM.</span></span> <span data-ttu-id="ffac8-129">Aby zdalnie Zaloguj się do maszyny wirtualnej platformy Azure nowo utworzony za pomocą protokołu RDP (Remote Desktop), kliknij przycisk **Connect**.</span><span class="sxs-lookup"><span data-stu-id="ffac8-129">To use Remote Desktop Protocol (RDP) to remotely sign in to the newly created Azure virtual machine, click **Connect**.</span></span>  

> [!IMPORTANT] 
> <span data-ttu-id="ffac8-130">Poniższe instrukcje założono, że użytkownik zalogowany do maszyny wirtualnej prawidłowo.</span><span class="sxs-lookup"><span data-stu-id="ffac8-130">The following instructions assume that you signed in to the virtual machine correctly.</span></span> <span data-ttu-id="ffac8-131">One założono, że są wydawania polecenia na maszynie wirtualnej, a nie na komputerze lokalnym.</span><span class="sxs-lookup"><span data-stu-id="ffac8-131">They also assume that you are issuing commands in the virtual machine and not on your local computer.</span></span>

## <span data-ttu-id="ffac8-132"><a id="setup"></a>Instalacji języka Python, Django i WFastCGI</span><span class="sxs-lookup"><span data-stu-id="ffac8-132"><a id="setup"> </a>Install Python, Django, and WFastCGI</span></span>
> [!NOTE]
> <span data-ttu-id="ffac8-133">Aby pobrać za pomocą programu Internet Explorer, może być konieczne skonfigurowanie programu Internet Explorer **Konfiguracja zwiększonych zabezpieczeń** ustawienia.</span><span class="sxs-lookup"><span data-stu-id="ffac8-133">To download by using Internet Explorer, you might have to configure Internet Explorer **Enhanced Security Configuration** settings.</span></span> <span data-ttu-id="ffac8-134">Aby to zrobić, kliknij przycisk **Start** > **narzędzia administracyjne** > **Menedżera serwera** > **serweralokalnego**.</span><span class="sxs-lookup"><span data-stu-id="ffac8-134">To do this, click **Start** > **Administrative Tools** > **Server Manager** > **Local Server**.</span></span> <span data-ttu-id="ffac8-135">Kliknij przycisk **Konfiguracja zwiększonych zabezpieczeń**, a następnie wybierz **poza**.</span><span class="sxs-lookup"><span data-stu-id="ffac8-135">Click **IE Enhanced Security Configuration**, and then select **Off**.</span></span>

1. <span data-ttu-id="ffac8-136">Zainstaluj najnowsze wersje Python 2.7 lub 3.4 Python z [python.org][python.org].</span><span class="sxs-lookup"><span data-stu-id="ffac8-136">Install the latest versions of Python 2.7 or Python 3.4 from [python.org][python.org].</span></span>
2. <span data-ttu-id="ffac8-137">Instalowanie przy użyciu narzędzia pip pakiety wfastcgi i django.</span><span class="sxs-lookup"><span data-stu-id="ffac8-137">Install the wfastcgi and django packages using pip.</span></span>
   
    <span data-ttu-id="ffac8-138">Dla języka Python 2.7 użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="ffac8-138">For Python 2.7, use the following command:</span></span>
   
        c:\python27\scripts\pip install wfastcgi
        c:\python27\scripts\pip install django
   
    <span data-ttu-id="ffac8-139">Dla języka Python 3.4 Użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="ffac8-139">For Python 3.4, use the following command:</span></span>
   
        c:\python34\scripts\pip install wfastcgi
        c:\python34\scripts\pip install django

## <a name="install-iis-with-fastcgi"></a><span data-ttu-id="ffac8-140">Instalowanie usług IIS przy użyciu FastCGI</span><span class="sxs-lookup"><span data-stu-id="ffac8-140">Install IIS with FastCGI</span></span>
* <span data-ttu-id="ffac8-141">Zainstaluj usługi Internet Information Services (IIS) z obsługą FastCGI.</span><span class="sxs-lookup"><span data-stu-id="ffac8-141">Install Internet Information Services (IIS) with FastCGI support.</span></span> <span data-ttu-id="ffac8-142">Może to potrwać kilka minut do wykonania.</span><span class="sxs-lookup"><span data-stu-id="ffac8-142">This might take several minutes to execute.</span></span>
   
        start /wait %windir%\System32\PkgMgr.exe /iu:IIS-WebServerRole;IIS-WebServer;IIS-CommonHttpFeatures;IIS-StaticContent;IIS-DefaultDocument;IIS-DirectoryBrowsing;IIS-HttpErrors;IIS-HealthAndDiagnostics;IIS-HttpLogging;IIS-LoggingLibraries;IIS-RequestMonitor;IIS-Security;IIS-RequestFiltering;IIS-HttpCompressionStatic;IIS-WebServerManagementTools;IIS-ManagementConsole;WAS-WindowsActivationService;WAS-ProcessModel;WAS-NetFxEnvironment;WAS-ConfigurationAPI;IIS-CGI

## <a name="create-a-new-django-application"></a><span data-ttu-id="ffac8-143">Utwórz nową aplikację Django</span><span class="sxs-lookup"><span data-stu-id="ffac8-143">Create a new Django application</span></span>
1. <span data-ttu-id="ffac8-144">W C:\inetpub\wwwroot Aby utworzyć nowy projekt Django, wprowadź następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="ffac8-144">In C:\inetpub\wwwroot, to create a new Django project, enter the following command:</span></span>
   
   <span data-ttu-id="ffac8-145">Dla języka Python 2.7 użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="ffac8-145">For Python 2.7, use the following command:</span></span>
   
       C:\Python27\Scripts\django-admin.exe startproject helloworld
   
   <span data-ttu-id="ffac8-146">Dla języka Python 3.4 Użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="ffac8-146">For Python 3.4, use the following command:</span></span>
   
       C:\Python34\Scripts\django-admin.exe startproject helloworld
   
   ![Wynik polecenia New-AzureService](./media/python-django-web-app/django-helloworld-cmd-new-azure-service.png)
2. <span data-ttu-id="ffac8-148">`django-admin` Polecenia wygenerowanie podstawowej struktury witryn skonstruowanych na podstawie Django:</span><span class="sxs-lookup"><span data-stu-id="ffac8-148">The `django-admin` command generates a basic structure for Django-based websites:</span></span>
   
   * <span data-ttu-id="ffac8-149">`helloworld\manage.py`pomaga rozpocząć hosting i Zatrzymaj hosting witryny sieci Web na podstawie Django.</span><span class="sxs-lookup"><span data-stu-id="ffac8-149">`helloworld\manage.py` helps you start hosting and stop hosting your Django-based website.</span></span>
   * <span data-ttu-id="ffac8-150">`helloworld\helloworld\settings.py`zawiera ustawienia Django dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ffac8-150">`helloworld\helloworld\settings.py` has Django settings for your application.</span></span>
   * <span data-ttu-id="ffac8-151">`helloworld\helloworld\urls.py`nie ma kodu mapowania między każdego adresu URL i jego widoku.</span><span class="sxs-lookup"><span data-stu-id="ffac8-151">`helloworld\helloworld\urls.py` has the mapping code between each URL and its view.</span></span>
3. <span data-ttu-id="ffac8-152">W katalogu C:\inetpub\wwwroot\helloworld\helloworld Utwórz nowy plik o nazwie views.py.</span><span class="sxs-lookup"><span data-stu-id="ffac8-152">In the C:\inetpub\wwwroot\helloworld\helloworld directory, create a new file named views.py.</span></span> <span data-ttu-id="ffac8-153">Ten plik zawiera widok, który renderuje stronę "hello world".</span><span class="sxs-lookup"><span data-stu-id="ffac8-153">This file has the view that renders the "hello world" page.</span></span> <span data-ttu-id="ffac8-154">W edytorze kodu wprowadź następujące polecenia:</span><span class="sxs-lookup"><span data-stu-id="ffac8-154">In your code editor, enter the following commands:</span></span>
   
       from django.http import HttpResponse
       def home(request):
           html = "<html><body>Hello World!</body></html>"
           return HttpResponse(html)
4. <span data-ttu-id="ffac8-155">Zastąp zawartość pliku urls.py za pomocą następujących poleceń:</span><span class="sxs-lookup"><span data-stu-id="ffac8-155">Replace the contents of the urls.py file with the following commands:</span></span>
   
       from django.conf.urls import patterns, url
       urlpatterns = patterns('',
           url(r'^$', 'helloworld.views.home', name='home'),
       )

## <a name="set-up-iis"></a><span data-ttu-id="ffac8-156">Konfigurowanie usług IIS</span><span class="sxs-lookup"><span data-stu-id="ffac8-156">Set up IIS</span></span>
1. <span data-ttu-id="ffac8-157">W pliku applicationhost.config globalne Odblokuj sekcję programów obsługi.</span><span class="sxs-lookup"><span data-stu-id="ffac8-157">In the global applicationhost.config file, unlock the handlers section.</span></span>  <span data-ttu-id="ffac8-158">Dzięki temu pliku web.config, aby użyć obsługi języka Python.</span><span class="sxs-lookup"><span data-stu-id="ffac8-158">This allows your web.config file to use the Python handler.</span></span> <span data-ttu-id="ffac8-159">Dodaj to polecenie:</span><span class="sxs-lookup"><span data-stu-id="ffac8-159">Add this command:</span></span>
   
        %windir%\system32\inetsrv\appcmd unlock config -section:system.webServer/handlers
2. <span data-ttu-id="ffac8-160">Aktywacja WFastCGI.</span><span class="sxs-lookup"><span data-stu-id="ffac8-160">Activate WFastCGI.</span></span> <span data-ttu-id="ffac8-161">Spowoduje to dodanie aplikacji do pliku applicationhost.config globalny, który odwołuje się do pliku wykonywalnego interpretera Python i skrypt wfastcgi.py.</span><span class="sxs-lookup"><span data-stu-id="ffac8-161">This adds an application to the global applicationhost.config file, which refers to your Python interpreter executable and the wfastcgi.py script.</span></span>
   
    <span data-ttu-id="ffac8-162">W języku Python 2.7:</span><span class="sxs-lookup"><span data-stu-id="ffac8-162">In Python 2.7:</span></span>
   
        C:\python27\scripts\wfastcgi-enable
   
    <span data-ttu-id="ffac8-163">W języku Python 3.4:</span><span class="sxs-lookup"><span data-stu-id="ffac8-163">In Python 3.4:</span></span>
   
        C:\python34\scripts\wfastcgi-enable
3. <span data-ttu-id="ffac8-164">W C:\inetpub\wwwroot\helloworld Utwórz plik web.config.</span><span class="sxs-lookup"><span data-stu-id="ffac8-164">In C:\inetpub\wwwroot\helloworld, create a web.config file.</span></span> <span data-ttu-id="ffac8-165">Wartość `scriptProcessor` atrybutu powinna być zgodna dane wyjściowe z poprzedniego kroku.</span><span class="sxs-lookup"><span data-stu-id="ffac8-165">The value of the `scriptProcessor` attribute should match the output from the preceding step.</span></span> <span data-ttu-id="ffac8-166">Aby uzyskać więcej informacji o ustawieniu wfastcgi, zobacz [pypi wfastcgi][wfastcgi].</span><span class="sxs-lookup"><span data-stu-id="ffac8-166">For more information about the wfastcgi setting, see [pypi wfastcgi][wfastcgi].</span></span>
   
   <span data-ttu-id="ffac8-167">W języku Python 2.7:</span><span class="sxs-lookup"><span data-stu-id="ffac8-167">In  Python 2.7:</span></span>
   
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
   
   <span data-ttu-id="ffac8-168">W języku Python 3.4:</span><span class="sxs-lookup"><span data-stu-id="ffac8-168">In  Python 3.4:</span></span>
   
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
4. <span data-ttu-id="ffac8-169">Należy zaktualizować lokalizację usługi IIS domyślnej witryny sieci Web wskazują folder projektu Django:</span><span class="sxs-lookup"><span data-stu-id="ffac8-169">Update the location of the IIS default website to point to the Django project folder:</span></span>
   
        %windir%\system32\inetsrv\appcmd set vdir "Default Web Site/" -physicalPath:"C:\inetpub\wwwroot\helloworld"
5. <span data-ttu-id="ffac8-170">Ładowanie strony sieci Web w przeglądarce.</span><span class="sxs-lookup"><span data-stu-id="ffac8-170">Load the webpage in your browser.</span></span>

![Oknie przeglądarki zostanie wyświetlona strona world hello na platformie Azure][1]

## <a name="shut-down-your-azure-virtual-machine"></a><span data-ttu-id="ffac8-172">Zamknij maszynę wirtualną z platformy Azure</span><span class="sxs-lookup"><span data-stu-id="ffac8-172">Shut down your Azure virtual machine</span></span>
<span data-ttu-id="ffac8-173">Po zakończeniu korzystania z tego samouczka, firma Microsoft zaleca zamknięcie lub Usuń maszynę Wirtualną platformy Azure utworzoną w ramach tego samouczka.</span><span class="sxs-lookup"><span data-stu-id="ffac8-173">When you're done with this tutorial, we recommend that you shut down or remove the Azure VM you created for the tutorial.</span></span> <span data-ttu-id="ffac8-174">Spowoduje to zwolnienie zasobów dla innych samouczków, a można uniknąć naliczania opłat użycia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="ffac8-174">This frees up resources for other tutorials, and you can avoid incurring Azure usage charges.</span></span>

[1]: ./media/python-django-web-app/django-helloworld-browser-azure.png

[port80]: ./media/python-django-web-app/django-helloworld-port80.png

[Web Platform Installer]: http://www.microsoft.com/web/downloads/platform.aspx
[python.org]: https://www.python.org/downloads/
[wfastcgi]: https://pypi.python.org/pypi/wfastcgi
