---
title: "aaaConfiguring Python z aplikacjami sieci Web usługi aplikacji Azure"
description: "W tym samouczku opisano opcje dotyczące tworzenia i konfigurowania podstawowego serwera sieci Web zgodnych aplikacji Python interfejs bramy (WSGI) w aplikacji sieci Web usługi aplikacji Azure."
services: app-service
documentationcenter: python
tags: python
author: huguesv
manager: erikre
editor: 
ms.assetid: fd00dc91-9935-4331-b955-4bd71e66d518
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 02/26/2016
ms.author: huvalo
ms.openlocfilehash: 00d49fb01491e9adb4b6fededfb95669a8dbd485
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-python-with-azure-app-service-web-apps"></a><span data-ttu-id="e84c9-103">Konfigurowanie języka Python z aplikacjami sieci Web usługi aplikacji Azure</span><span class="sxs-lookup"><span data-stu-id="e84c9-103">Configuring Python with Azure App Service Web Apps</span></span>
<span data-ttu-id="e84c9-104">W tym samouczku opisano opcje dotyczące tworzenia i konfigurowania podstawowej aplikacji Python zgodnych sieci Web serwera bramy interfejsu (WSGI) w [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="e84c9-104">This tutorial describes options for authoring and configuring a basic Web Server Gateway Interface (WSGI) compliant Python application on [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>

<span data-ttu-id="e84c9-105">Opisuje dodatkowe funkcje Git, takiego jak wdrożenie środowiska wirtualnego, a instalacja pakietu przy użyciu pliku requirements.txt.</span><span class="sxs-lookup"><span data-stu-id="e84c9-105">It describes additional features of Git deployment, such as virtual environment and package installation using requirements.txt.</span></span>

## <a name="bottle-django-or-flask"></a><span data-ttu-id="e84c9-106">Bottle, Django lub Flask?</span><span class="sxs-lookup"><span data-stu-id="e84c9-106">Bottle, Django or Flask?</span></span>
<span data-ttu-id="e84c9-107">Hello Azure Marketplace zawiera szablony dla struktur hello Bottle, Django i Flask.</span><span class="sxs-lookup"><span data-stu-id="e84c9-107">hello Azure Marketplace contains templates for hello Bottle, Django and Flask frameworks.</span></span> <span data-ttu-id="e84c9-108">Jeśli tworzysz pierwszej aplikacji sieci web w usłudze Azure App Service, lub nie masz doświadczenia z usługą Git, firma Microsoft zaleca wykonaj jedną z tych samouczki, które zawierają instrukcje krok po kroku działającą aplikację z galerii hello przy użyciu wdrożenia Git w systemie Windows lub Mac:</span><span class="sxs-lookup"><span data-stu-id="e84c9-108">If you are developing your first web app in Azure App Service, or you are not familiar with Git, we recommend that you follow one of these tutorials, which include step-by-step instructions for building a working application from hello gallery using Git deployment from Windows or Mac:</span></span>

* [<span data-ttu-id="e84c9-109">Tworzenie aplikacji sieci web w języku Bottle</span><span class="sxs-lookup"><span data-stu-id="e84c9-109">Creating web apps with Bottle</span></span>](web-sites-python-create-deploy-bottle-app.md)
* [<span data-ttu-id="e84c9-110">Tworzenie aplikacji sieci web przy użyciu platformy Django</span><span class="sxs-lookup"><span data-stu-id="e84c9-110">Creating web apps with Django</span></span>](web-sites-python-create-deploy-django-app.md)
* [<span data-ttu-id="e84c9-111">Tworzenie aplikacji sieci web za pomocą platformy Flask</span><span class="sxs-lookup"><span data-stu-id="e84c9-111">Creating web apps with Flask</span></span>](web-sites-python-create-deploy-flask-app.md)

## <a name="web-app-creation-on-azure-portal"></a><span data-ttu-id="e84c9-112">Tworzenie aplikacji sieci Web w portalu Azure</span><span class="sxs-lookup"><span data-stu-id="e84c9-112">Web app creation on Azure Portal</span></span>
<span data-ttu-id="e84c9-113">Ten samouczek zakłada istniejących Azure subskrypcji i dostęp toohello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="e84c9-113">This tutorial assumes an existing Azure subscription and access toohello Azure Portal.</span></span>

<span data-ttu-id="e84c9-114">Jeśli nie masz istniejącej aplikacji sieci web, możesz utworzyć jedną z hello [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e84c9-114">If you do not have an existing web app, you can create one from hello [Azure Portal](https://portal.azure.com).</span></span>  <span data-ttu-id="e84c9-115">Kliknij przycisk Nowy hello w lewym górnym rogu hello, a następnie kliknij przycisk **sieci Web i mobilność** > **aplikacji sieci Web**.</span><span class="sxs-lookup"><span data-stu-id="e84c9-115">Click hello NEW button in hello top left corner, then click **Web + Mobile** > **Web app**.</span></span>

## <a name="git-publishing"></a><span data-ttu-id="e84c9-116">Publikowanie w usłudze Git</span><span class="sxs-lookup"><span data-stu-id="e84c9-116">Git Publishing</span></span>
<span data-ttu-id="e84c9-117">Konfigurowanie publikowania Git dla aplikacji sieci web nowo utworzony wykonując instrukcje hello [tooAzure lokalnego wdrożenia Git usługi aplikacji](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="e84c9-117">Configure Git publishing for your newly created web app by following hello instructions at [Local Git Deployment tooAzure App Service](app-service-deploy-local-git.md).</span></span> <span data-ttu-id="e84c9-118">W tym samouczku używana Git toocreate, zarządzania i publikowania naszych Python tooAzure aplikacji sieci web usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e84c9-118">This tutorial uses Git toocreate, manage, and publish our Python web app tooAzure App Service.</span></span>

<span data-ttu-id="e84c9-119">Po skonfigurowaniu publikowania w usłudze Git repozytorium Git zostanie utworzona i skojarzona z aplikacją sieci web.</span><span class="sxs-lookup"><span data-stu-id="e84c9-119">Once Git publishing is set up, a Git repository will be created and associated with your web app.</span></span> <span data-ttu-id="e84c9-120">adres URL repozytorium Hello będą wyświetlane i można odtąd toopush używanych danych z chmury toohello środowisko rozwoju lokalnego hello.</span><span class="sxs-lookup"><span data-stu-id="e84c9-120">hello repository's URL will be displayed and can henceforth be used toopush data from hello local development environment toohello cloud.</span></span> <span data-ttu-id="e84c9-121">toopublish aplikacji za pomocą narzędzia Git, upewnij się, klient Git jest również instalowany i użyj hello instrukcje toopush Twojego tooAzure zawartości aplikacji usługi aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="e84c9-121">toopublish applications via Git, make sure a Git client is also installed and use hello instructions provided toopush your web app content tooAzure App Service.</span></span>

## <a name="application-overview"></a><span data-ttu-id="e84c9-122">Omówienie aplikacji</span><span class="sxs-lookup"><span data-stu-id="e84c9-122">Application Overview</span></span>
<span data-ttu-id="e84c9-123">W kolejnych sekcjach hello hello następujące pliki zostały utworzone.</span><span class="sxs-lookup"><span data-stu-id="e84c9-123">In hello next sections, hello following files are created.</span></span> <span data-ttu-id="e84c9-124">One powinna zostać umieszczona w głównym hello hello repozytorium Git.</span><span class="sxs-lookup"><span data-stu-id="e84c9-124">They should be placed in hello root of hello Git repository.</span></span>

    app.py
    requirements.txt
    runtime.txt
    web.config
    ptvs_virtualenv_proxy.py


## <a name="wsgi-handler"></a><span data-ttu-id="e84c9-125">Program obsługi WSGI</span><span class="sxs-lookup"><span data-stu-id="e84c9-125">WSGI Handler</span></span>
<span data-ttu-id="e84c9-126">WSGI jest standardem Python opisanego przez [3333 program ten](http://www.python.org/dev/peps/pep-3333/) Definiowanie interfejsu między serwerem sieci web hello i Python.</span><span class="sxs-lookup"><span data-stu-id="e84c9-126">WSGI is a Python standard described by [PEP 3333](http://www.python.org/dev/peps/pep-3333/) defining an interface between hello web server and Python.</span></span> <span data-ttu-id="e84c9-127">Zapewnia interfejs standardowych do pisania różnych aplikacji sieci web i struktur za pomocą języka Python.</span><span class="sxs-lookup"><span data-stu-id="e84c9-127">It provides a standardized interface for writing various web applications and frameworks using Python.</span></span> <span data-ttu-id="e84c9-128">Obecnie popularnych struktur sieci web języka Python posłużyć WSGI.</span><span class="sxs-lookup"><span data-stu-id="e84c9-128">Popular Python web frameworks today use WSGI.</span></span> <span data-ttu-id="e84c9-129">Umożliwia aplikacji sieci Web usługi aplikacji Azure obsługę tych platform; Ponadto użytkownicy zaawansowani można nawet tworzyć własne tak długo, jak niestandardowy program obsługi hello następuje hello WSGI specyfikacji wytyczne.</span><span class="sxs-lookup"><span data-stu-id="e84c9-129">Azure App Service Web Apps gives you support for any such frameworks; in addition, advanced users can even author their own as long as hello custom handler follows hello WSGI specification guidelines.</span></span>

<span data-ttu-id="e84c9-130">Oto przykład `app.py` definiuje niestandardowego programu obsługi:</span><span class="sxs-lookup"><span data-stu-id="e84c9-130">Here's an example of an `app.py` that defines a custom handler:</span></span>

    def wsgi_app(environ, start_response):
        status = '200 OK'
        response_headers = [('Content-type', 'text/plain')]
        start_response(status, response_headers)
        response_body = 'Hello World'
        yield response_body.encode()

    if __name__ == '__main__':
        from wsgiref.simple_server import make_server

        httpd = make_server('localhost', 5555, wsgi_app)
        httpd.serve_forever()

<span data-ttu-id="e84c9-131">Można uruchomić tej aplikacji lokalnie z `python app.py`, a następnie wyszukaj zbyt`http://localhost:5555` w przeglądarce sieci web.</span><span class="sxs-lookup"><span data-stu-id="e84c9-131">You can run this application locally with `python app.py`, then browse too`http://localhost:5555` in your web browser.</span></span>

## <a name="virtual-environment"></a><span data-ttu-id="e84c9-132">Środowisko wirtualne</span><span class="sxs-lookup"><span data-stu-id="e84c9-132">Virtual Environment</span></span>
<span data-ttu-id="e84c9-133">Chociaż hello przykładową aplikację powyżej nie wymaga żadnych pakiety zewnętrzne, jest prawdopodobne, że aplikacja będzie wymagać niektóre.</span><span class="sxs-lookup"><span data-stu-id="e84c9-133">Although hello example app above doesn't require any external packages, it is likely that your application will require some.</span></span>

<span data-ttu-id="e84c9-134">toohelp zarządzać zależności zewnętrznych pakietów, wdrażanie Azure Git obsługuje hello tworzenie środowisk wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="e84c9-134">toohelp manage external package dependencies, Azure Git deployment supports hello creation of virtual environments.</span></span>

<span data-ttu-id="e84c9-135">Wykrycie Azure pliku requirements.txt w głównym repozytorium hello hello, automatycznie tworzy środowiska wirtualnego o nazwie `env`.</span><span class="sxs-lookup"><span data-stu-id="e84c9-135">When Azure detects a requirements.txt in hello root of hello repository, it automatically creates a virtual environment named `env`.</span></span> <span data-ttu-id="e84c9-136">Jest to wykonywane tylko w pierwszym wdrożeniu hello, lub podczas każdego wdrożenia po hello zmieniono wybrane środowisko uruchomieniowe języka Python.</span><span class="sxs-lookup"><span data-stu-id="e84c9-136">This only occurs on hello first deployment, or during any deployment after hello selected Python runtime has changed.</span></span>

<span data-ttu-id="e84c9-137">Prawdopodobnie zechcesz toocreate środowiska wirtualnego lokalnie do tworzenia, ale nie dołączaj do repozytorium Git.</span><span class="sxs-lookup"><span data-stu-id="e84c9-137">You will probably want toocreate a virtual environment locally for development, but don't include it in your Git repository.</span></span>

## <a name="package-management"></a><span data-ttu-id="e84c9-138">Zarządzanie pakietami</span><span class="sxs-lookup"><span data-stu-id="e84c9-138">Package Management</span></span>
<span data-ttu-id="e84c9-139">W środowisku wirtualnym hello przy użyciu narzędzia pip, zostaną automatycznie zainstalowane pakiety wymienione w pliku requirements.txt.</span><span class="sxs-lookup"><span data-stu-id="e84c9-139">Packages listed in requirements.txt will be installed automatically in hello virtual environment using pip.</span></span> <span data-ttu-id="e84c9-140">Dzieje się to przy każdym wdrożeniu, ale narzędzie pip pomija instalację, jeśli pakiet jest już zainstalowana.</span><span class="sxs-lookup"><span data-stu-id="e84c9-140">This happens on every deployment, but pip will skip installation if a package is already installed.</span></span>

<span data-ttu-id="e84c9-141">Przykład `requirements.txt`:</span><span class="sxs-lookup"><span data-stu-id="e84c9-141">Example `requirements.txt`:</span></span>

    azure==0.8.4


## <a name="python-version"></a><span data-ttu-id="e84c9-142">Wersja języka Python</span><span class="sxs-lookup"><span data-stu-id="e84c9-142">Python Version</span></span>
[!INCLUDE [web-sites-python-customizing-runtime](../../includes/web-sites-python-customizing-runtime.md)]

<span data-ttu-id="e84c9-143">Przykład `runtime.txt`:</span><span class="sxs-lookup"><span data-stu-id="e84c9-143">Example `runtime.txt`:</span></span>

    python-2.7


## <a name="webconfig"></a><span data-ttu-id="e84c9-144">Web.config</span><span class="sxs-lookup"><span data-stu-id="e84c9-144">Web.config</span></span>
<span data-ttu-id="e84c9-145">Będziesz potrzebować toocreate toospecify pliku web.config sposób obsługi żądań powitania serwera.</span><span class="sxs-lookup"><span data-stu-id="e84c9-145">You'll need toocreate a web.config file toospecify how hello server should handle requests.</span></span>

<span data-ttu-id="e84c9-146">Należy pamiętać, że jeśli plik pliku web.x.y.config w repozytorium, jeśli odpowiada x.y hello wybrane środowisko uruchomieniowe języka Python, a następnie Azure automatycznie kopiuje hello odpowiedniego pliku jako pliku web.config.</span><span class="sxs-lookup"><span data-stu-id="e84c9-146">Note that if you have a web.x.y.config file in your repository, where x.y matches hello selected Python runtime, then Azure will automatically copy hello appropriate file as web.config.</span></span>

<span data-ttu-id="e84c9-147">Witaj poniższych przykładach plik web.config na podstawie skryptu serwera proxy środowiska wirtualnego, który jest opisany w następnej sekcji hello.</span><span class="sxs-lookup"><span data-stu-id="e84c9-147">hello following web.config examples rely on a virtual environment proxy script, which is described in hello next section.</span></span>  <span data-ttu-id="e84c9-148">Pracują z programem obsługi WSGI hello używane w przykładzie hello `app.py` powyżej.</span><span class="sxs-lookup"><span data-stu-id="e84c9-148">They work with hello WSGI handler used in hello example `app.py` above.</span></span>

<span data-ttu-id="e84c9-149">Przykład `web.config` dla języka Python 2.7:</span><span class="sxs-lookup"><span data-stu-id="e84c9-149">Example `web.config` for Python 2.7:</span></span>

    <?xml version="1.0"?>
    <configuration>
      <appSettings>
        <add key="WSGI_ALT_VIRTUALENV_HANDLER" value="app.wsgi_app" />
        <add key="WSGI_ALT_VIRTUALENV_ACTIVATE_THIS"
             value="D:\home\site\wwwroot\env\Scripts\activate_this.py" />
        <add key="WSGI_HANDLER"
             value="ptvs_virtualenv_proxy.get_virtualenv_handler()" />
        <add key="PYTHONPATH" value="D:\home\site\wwwroot" />
      </appSettings>
      <system.web>
        <compilation debug="true" targetFramework="4.0" />
      </system.web>
      <system.webServer>
        <modules runAllManagedModulesForAllRequests="true" />
        <handlers>
          <remove name="Python27_via_FastCGI" />
          <remove name="Python34_via_FastCGI" />
          <add name="Python FastCGI"
               path="handler.fcgi"
               verb="*"
               modules="FastCgiModule"
               scriptProcessor="D:\Python27\python.exe|D:\Python27\Scripts\wfastcgi.py"
               resourceType="Unspecified"
               requireAccess="Script" />
        </handlers>
        <rewrite>
          <rules>
            <rule name="Static Files" stopProcessing="true">
              <conditions>
                <add input="true" pattern="false" />
              </conditions>
            </rule>
            <rule name="Configure Python" stopProcessing="true">
              <match url="(.*)" ignoreCase="false" />
              <conditions>
                <add input="{REQUEST_URI}" pattern="^/static/.*" ignoreCase="true" negate="true" />
              </conditions>
              <action type="Rewrite"
                      url="handler.fcgi/{R:1}"
                      appendQueryString="true" />
            </rule>
          </rules>
        </rewrite>
      </system.webServer>
    </configuration>


<span data-ttu-id="e84c9-150">Przykład `web.config` dla języka Python 3.4:</span><span class="sxs-lookup"><span data-stu-id="e84c9-150">Example `web.config` for Python 3.4:</span></span>

    <?xml version="1.0"?>
    <configuration>
      <appSettings>
        <add key="WSGI_ALT_VIRTUALENV_HANDLER" value="app.wsgi_app" />
        <add key="WSGI_ALT_VIRTUALENV_ACTIVATE_THIS"
             value="D:\home\site\wwwroot\env\Scripts\python.exe" />
        <add key="WSGI_HANDLER"
             value="ptvs_virtualenv_proxy.get_venv_handler()" />
        <add key="PYTHONPATH" value="D:\home\site\wwwroot" />
      </appSettings>
      <system.web>
        <compilation debug="true" targetFramework="4.0" />
      </system.web>
      <system.webServer>
        <modules runAllManagedModulesForAllRequests="true" />
        <handlers>
          <remove name="Python27_via_FastCGI" />
          <remove name="Python34_via_FastCGI" />
          <add name="Python FastCGI"
               path="handler.fcgi"
               verb="*"
               modules="FastCgiModule"
               scriptProcessor="D:\Python34\python.exe|D:\Python34\Scripts\wfastcgi.py"
               resourceType="Unspecified"
               requireAccess="Script" />
        </handlers>
        <rewrite>
          <rules>
            <rule name="Static Files" stopProcessing="true">
              <conditions>
                <add input="true" pattern="false" />
              </conditions>
            </rule>
            <rule name="Configure Python" stopProcessing="true">
              <match url="(.*)" ignoreCase="false" />
              <conditions>
                <add input="{REQUEST_URI}" pattern="^/static/.*" ignoreCase="true" negate="true" />
              </conditions>
              <action type="Rewrite" url="handler.fcgi/{R:1}" appendQueryString="true" />
            </rule>
          </rules>
        </rewrite>
      </system.webServer>
    </configuration>


<span data-ttu-id="e84c9-151">Pliki statyczne będą obsługiwane przez serwer sieci web hello bezpośrednio, bez przechodzenia przez kod języka Python, aby poprawić wydajność.</span><span class="sxs-lookup"><span data-stu-id="e84c9-151">Static files will be handled by hello web server directly, without going through Python code, for improved performance.</span></span>

<span data-ttu-id="e84c9-152">Hello powyżej przykłady lokalizacji hello w adresie URL hello musi być zgodna hello lokalizacji plików statycznych hello na dysku.</span><span class="sxs-lookup"><span data-stu-id="e84c9-152">In hello above examples, hello location of hello static files on disk should match hello location in hello URL.</span></span> <span data-ttu-id="e84c9-153">Oznacza to, że żądanie `http://pythonapp.azurewebsites.net/static/site.css` posłuży hello pliku na dysku w `\static\site.css`.</span><span class="sxs-lookup"><span data-stu-id="e84c9-153">This means that a request for `http://pythonapp.azurewebsites.net/static/site.css` will serve hello file on disk at `\static\site.css`.</span></span>

<span data-ttu-id="e84c9-154">`WSGI_ALT_VIRTUALENV_HANDLER`Określa się tam hello WSGI obsługi.</span><span class="sxs-lookup"><span data-stu-id="e84c9-154">`WSGI_ALT_VIRTUALENV_HANDLER` is where you specify hello WSGI handler.</span></span> <span data-ttu-id="e84c9-155">W hello powyżej przykłady ma `app.wsgi_app` ponieważ obsługa hello ma funkcji o nazwie `wsgi_app` w `app.py` w folderze głównym hello.</span><span class="sxs-lookup"><span data-stu-id="e84c9-155">In hello above examples, it's `app.wsgi_app` because hello handler is a function named `wsgi_app` in `app.py` in hello root folder.</span></span>

<span data-ttu-id="e84c9-156">`PYTHONPATH`można dostosować, ale po zainstalowaniu wszystkich zależności w środowisku wirtualnym hello, określając je w pliku requirements.txt, nie ma potrzeby toochange go.</span><span class="sxs-lookup"><span data-stu-id="e84c9-156">`PYTHONPATH` can be customized, but if you install all your dependencies in hello virtual environment by specifying them in requirements.txt, you shouldn't need toochange it.</span></span>

## <a name="virtual-environment-proxy"></a><span data-ttu-id="e84c9-157">Serwer Proxy środowiska wirtualnego</span><span class="sxs-lookup"><span data-stu-id="e84c9-157">Virtual Environment Proxy</span></span>
<span data-ttu-id="e84c9-158">Hello następującego skryptu jest używany tooretrieve hello WSGI obsługi, aktywować hello wirtualnego błędów środowiska i dziennika.</span><span class="sxs-lookup"><span data-stu-id="e84c9-158">hello following script is used tooretrieve hello WSGI handler, activate hello virtual environment and log errors.</span></span> <span data-ttu-id="e84c9-159">Jest zaprojektowana toobe ogólnego i używany bez modyfikacji.</span><span class="sxs-lookup"><span data-stu-id="e84c9-159">It is designed toobe generic and used without modifications.</span></span>

<span data-ttu-id="e84c9-160">Zawartość `ptvs_virtualenv_proxy.py`:</span><span class="sxs-lookup"><span data-stu-id="e84c9-160">Contents of `ptvs_virtualenv_proxy.py`:</span></span>

     # ############################################################################
     #
     # Copyright (c) Microsoft Corporation. 
     #
     # This source code is subject tooterms and conditions of hello Apache License, Version 2.0. A 
     # copy of hello license can be found in hello License.html file at hello root of this distribution. If 
     # you cannot locate hello Apache License, Version 2.0, please send an email too
     # vspython@microsoft.com. By using this source code in any fashion, you are agreeing toobe bound 
     # by hello terms of hello Apache License, Version 2.0.
     #
     # You must not remove this notice, or any other, from this software.
     #
     # ###########################################################################

    import datetime
    import os
    import sys
    import traceback

    if sys.version_info[0] == 3:
        def to_str(value):
            return value.decode(sys.getfilesystemencoding())

        def execfile(path, global_dict):
            """Execute a file"""
            with open(path, 'r') as f:
                code = f.read()
            code = code.replace('\r\n', '\n') + '\n'
            exec(code, global_dict)
    else:
        def to_str(value):
            return value.encode(sys.getfilesystemencoding())

    def log(txt):
        """Logs fatal errors tooa log file if WSGI_LOG env var is defined"""
        log_file = os.environ.get('WSGI_LOG')
        if log_file:
            f = open(log_file, 'a+')
            try:
                f.write('%s: %s' % (datetime.datetime.now(), txt))
            finally:
                f.close()

    ptvsd_secret = os.getenv('WSGI_PTVSD_SECRET')
    if ptvsd_secret:
        log('Enabling ptvsd ...\n')
        try:
            import ptvsd
            try:
                ptvsd.enable_attach(ptvsd_secret)
                log('ptvsd enabled.\n')
            except: 
                log('ptvsd.enable_attach failed\n')
        except ImportError:
            log('error importing ptvsd.\n')

    def get_wsgi_handler(handler_name):
        if not handler_name:
            raise Exception('WSGI_ALT_VIRTUALENV_HANDLER env var must be set')

        if not isinstance(handler_name, str):
            handler_name = to_str(handler_name)

        module_name, _, callable_name = handler_name.rpartition('.')
        should_call = callable_name.endswith('()')
        callable_name = callable_name[:-2] if should_call else callable_name
        name_list = [(callable_name, should_call)]
        handler = None
        last_tb = ''

        while module_name:
            try:
                handler = __import__(module_name, fromlist=[name_list[0][0]])
                last_tb = ''
                for name, should_call in name_list:
                    handler = getattr(handler, name)
                    if should_call:
                        handler = handler()
                break
            except ImportError:
                module_name, _, callable_name = module_name.rpartition('.')
                should_call = callable_name.endswith('()')
                callable_name = callable_name[:-2] if should_call else callable_name
                name_list.insert(0, (callable_name, should_call))
                handler = None
                last_tb = ': ' + traceback.format_exc()

        if handler is None:
            raise ValueError('"%s" could not be imported%s' % (handler_name, last_tb))

        return handler

    activate_this = os.getenv('WSGI_ALT_VIRTUALENV_ACTIVATE_THIS')
    if not activate_this:
        raise Exception('WSGI_ALT_VIRTUALENV_ACTIVATE_THIS is not set')

    def get_virtualenv_handler():
        log('Activating virtualenv with %s\n' % activate_this)
        execfile(activate_this, dict(__file__=activate_this))

        log('Getting handler %s\n' % os.getenv('WSGI_ALT_VIRTUALENV_HANDLER'))
        handler = get_wsgi_handler(os.getenv('WSGI_ALT_VIRTUALENV_HANDLER'))
        log('Got handler: %r\n' % handler)
        return handler

    def get_venv_handler():
        log('Activating venv with executable at %s\n' % activate_this)
        import site
        sys.executable = activate_this
        old_sys_path, sys.path = sys.path, []

        site.main()

        sys.path.insert(0, '')
        for item in old_sys_path:
            if item not in sys.path:
                sys.path.append(item)

        log('Getting handler %s\n' % os.getenv('WSGI_ALT_VIRTUALENV_HANDLER'))
        handler = get_wsgi_handler(os.getenv('WSGI_ALT_VIRTUALENV_HANDLER'))
        log('Got handler: %r\n' % handler)
        return handler


## <a name="customize-git-deployment"></a><span data-ttu-id="e84c9-161">Dostosowywanie wdrożenia usługi Git</span><span class="sxs-lookup"><span data-stu-id="e84c9-161">Customize Git deployment</span></span>
[!INCLUDE [web-sites-python-customizing-runtime](../../includes/web-sites-python-customizing-deployment.md)]

## <a name="troubleshooting---package-installation"></a><span data-ttu-id="e84c9-162">Rozwiązywanie problemów — instalowanie pakietów</span><span class="sxs-lookup"><span data-stu-id="e84c9-162">Troubleshooting - Package Installation</span></span>
[!INCLUDE [web-sites-python-troubleshooting-package-installation](../../includes/web-sites-python-troubleshooting-package-installation.md)]

## <a name="troubleshooting---virtual-environment"></a><span data-ttu-id="e84c9-163">Rozwiązywanie problemów — środowisko wirtualne</span><span class="sxs-lookup"><span data-stu-id="e84c9-163">Troubleshooting - Virtual Environment</span></span>
[!INCLUDE [web-sites-python-troubleshooting-virtual-environment](../../includes/web-sites-python-troubleshooting-virtual-environment.md)]

## <a name="next-steps"></a><span data-ttu-id="e84c9-164">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e84c9-164">Next steps</span></span>
<span data-ttu-id="e84c9-165">Aby uzyskać więcej informacji, zobacz hello [Centrum deweloperów języka Python](/develop/python/).</span><span class="sxs-lookup"><span data-stu-id="e84c9-165">For more information, see hello [Python Developer Center](/develop/python/).</span></span>

> [!NOTE]
> <span data-ttu-id="e84c9-166">Tooget wprowadzenie do usługi Azure App Service przed utworzeniem konta platformy Azure, przejdź zbyt[Wypróbuj usługę App Service](https://azure.microsoft.com/try/app-service/), gdzie możesz od razu utworzyć krótkotrwałą, początkową aplikację sieci web w usłudze App Service.</span><span class="sxs-lookup"><span data-stu-id="e84c9-166">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="e84c9-167">Bez kart kredytowych i bez zobowiązań.</span><span class="sxs-lookup"><span data-stu-id="e84c9-167">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="whats-changed"></a><span data-ttu-id="e84c9-168">Co zostało zmienione</span><span class="sxs-lookup"><span data-stu-id="e84c9-168">What's changed</span></span>
* <span data-ttu-id="e84c9-169">Toohello przewodnik zmiany z tooApp witryn sieci Web usługi dla: [usłudze Azure App Service i jej wpływ na istniejące usługi platformy Azure](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="e84c9-169">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

