---
title: "Python sieci web app przy użyciu platformy Django na maszynie Wirtualnej platformy Azure systemu Linux | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak host aplikacji sieci web na podstawie Django w platformie Azure przy użyciu maszyny Wirtualnej systemu Linux."
services: virtual-machines-linux
documentationcenter: python
author: huguesv
manager: wpickett
editor: 
tags: azure-resource-manager
ms.assetid: 00ad4c2c-4316-4f9a-913f-f7f49b158db7
ms.service: virtual-machines-linux
ms.workload: web
ms.tgt_pltfrm: vm-linux
ms.devlang: python
ms.topic: article
ms.date: 05/31/2017
ms.author: huvalo
ms.openlocfilehash: 6e2ab8c7da7496d0e2b567a4bdc9341adcf01552
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="django-hello-world-web-app-on-a-linux-vm"></a><span data-ttu-id="a9741-103">Aplikacja sieci web Django Hello World na maszynie Wirtualnej systemu Linux</span><span class="sxs-lookup"><span data-stu-id="a9741-103">Django Hello World web app on a Linux VM</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a9741-104">Windows</span><span class="sxs-lookup"><span data-stu-id="a9741-104">Windows</span></span>](../windows/classic/python-django-web-app.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
> * [<span data-ttu-id="a9741-105">System Mac/Linux</span><span class="sxs-lookup"><span data-stu-id="a9741-105">Mac/Linux</span></span>](../windows/classic/python-django-web-app.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
> 
> 

<br>

<span data-ttu-id="a9741-106">W tym samouczku przedstawiono sposób hosta witryny sieci Web na podstawie Django w systemie Linux w maszynach wirtualnych platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="a9741-106">This tutorial shows you how to host a Django-based website in Linux in Azure Virtual Machines.</span></span> <span data-ttu-id="a9741-107">W samouczku przyjęto założenie, nie już pewne doświadczenie w systemie Azure.</span><span class="sxs-lookup"><span data-stu-id="a9741-107">In the tutorial, we assume no prior experience with Azure.</span></span> <span data-ttu-id="a9741-108">Po zakończeniu samouczka może mieć aplikacji opartej na Django w górę i w chmurze.</span><span class="sxs-lookup"><span data-stu-id="a9741-108">When you finish the tutorial, you can have a Django-based application up and running in the cloud.</span></span>

<span data-ttu-id="a9741-109">Instrukcje:</span><span class="sxs-lookup"><span data-stu-id="a9741-109">Learn how to:</span></span>

* <span data-ttu-id="a9741-110">Skonfiguruj maszynę wirtualną platformy Azure do hosta Django.</span><span class="sxs-lookup"><span data-stu-id="a9741-110">Set up an Azure virtual machine to host Django.</span></span> <span data-ttu-id="a9741-111">Mimo że w tym samouczku wyjaśniono, jak to zrobić w **Linux**, wykonaj te same dla maszyny Wirtualnej systemu Windows Server hostowana na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="a9741-111">Although this tutorial explains how to do this for **Linux**, you can do the same for a Windows Server VM hosted in Azure.</span></span> 
* <span data-ttu-id="a9741-112">Utwórz nową aplikację Django w systemie Linux.</span><span class="sxs-lookup"><span data-stu-id="a9741-112">Create a new Django application in Linux.</span></span>

<span data-ttu-id="a9741-113">Samouczek przedstawia sposób tworzenia podstawowej aplikacji sieci web Hello World.</span><span class="sxs-lookup"><span data-stu-id="a9741-113">The tutorial shows you how to build a basic Hello World web application.</span></span> <span data-ttu-id="a9741-114">Aplikacja znajduje się w maszynie wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="a9741-114">The application is hosted in an Azure virtual machine.</span></span>

<span data-ttu-id="a9741-115">Poniższy zrzut ekranu przedstawia gotową aplikację:</span><span class="sxs-lookup"><span data-stu-id="a9741-115">The following screenshot shows the completed application:</span></span>

![Oknie przeglądarki zostanie wyświetlona strona Hello World na platformie Azure](./media/python-django-web-app/mac-linux-django-helloworld-browser.png)

[!INCLUDE [create-account-and-vms-note](../../../includes/create-account-and-vms-note.md)]

## <a name="create-and-set-up-an-azure-virtual-machine-to-host-django"></a><span data-ttu-id="a9741-117">Tworzenie i konfigurowanie maszyny wirtualnej platformy Azure na hoście Django</span><span class="sxs-lookup"><span data-stu-id="a9741-117">Create and set up an Azure virtual machine to host Django</span></span>

1. <span data-ttu-id="a9741-118">Aby utworzyć maszynę wirtualną platformy Azure z rozkładem Ubuntu Server 14.04 LTS, zobacz [Utwórz maszynę wirtualną systemu Linux w portalu Azure](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a9741-118">To create an Azure virtual machine with the Ubuntu Server 14.04 LTS distribution, see [Create a Linux virtual machine in the Azure portal](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="a9741-119">Możesz również wybrać uwierzytelnianie hasła zamiast za pomocą klucza publicznego SSH.</span><span class="sxs-lookup"><span data-stu-id="a9741-119">You also can choose password authentication instead of using an SSH public key.</span></span>
2. <span data-ttu-id="a9741-120">Aby edytować grupy zabezpieczeń sieci, aby zezwolić na ruch przychodzący HTTP na porcie 80, zobacz [tworzenia grup zabezpieczeń sieci w portalu Azure](../../virtual-network/virtual-networks-create-nsg-arm-pportal.md).</span><span class="sxs-lookup"><span data-stu-id="a9741-120">To edit the network security group to allow incoming HTTP traffic to port 80, see [Create network security groups in the Azure portal](../../virtual-network/virtual-networks-create-nsg-arm-pportal.md).</span></span>
3. <span data-ttu-id="a9741-121">(Opcjonalnie) Domyślnie nowej maszyny wirtualnej nie ma w pełni kwalifikowaną nazwą domeny (FQDN).</span><span class="sxs-lookup"><span data-stu-id="a9741-121">(Optional) By default, your new virtual machine doesn't have a fully qualified domain name (FQDN).</span></span>  <span data-ttu-id="a9741-122">Aby utworzyć Maszynę wirtualną z wykorzystaniem nazwy FQDN, zobacz [utworzenia nazwy FQDN w portalu Azure dla maszyny Wirtualnej systemu Windows](../windows/portal-create-fqdn.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a9741-122">To create a VM with an FQDN, see [Create an FQDN in the Azure portal for a Windows VM](../windows/portal-create-fqdn.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="a9741-123">Ten krok nie jest wymagane wykonanie kroków tego samouczka.</span><span class="sxs-lookup"><span data-stu-id="a9741-123">This step is not required for completing this tutorial.</span></span>

## <span data-ttu-id="a9741-124"><a id="setup"></a>Konfigurowanie środowiska programowania</span><span class="sxs-lookup"><span data-stu-id="a9741-124"><a id="setup"> </a>Set up the development environment</span></span>
> [!NOTE]
> <span data-ttu-id="a9741-125">Jeśli musisz zainstalować Python lub chcesz użyć bibliotek klienckich, zobacz [Przewodnik instalacji języka Python](../../python-how-to-install.md).</span><span class="sxs-lookup"><span data-stu-id="a9741-125">If you need to install Python or want to use the client libraries, see the [Python installation guide](../../python-how-to-install.md).</span></span>

<span data-ttu-id="a9741-126">Maszyny Wirtualnej systemu Ubuntu Linux ma Python 2.7 preinstalowany, ale go nie dołączono Apache lub Django.</span><span class="sxs-lookup"><span data-stu-id="a9741-126">The Ubuntu Linux VM has Python 2.7 preinstalled, but it doesn't come with Apache or Django.</span></span> <span data-ttu-id="a9741-127">Wykonaj poniższe kroki, aby nawiązać połączenie z maszyną Wirtualną i zainstaluj Apache i Django:</span><span class="sxs-lookup"><span data-stu-id="a9741-127">Complete the following steps to connect to your VM and install Apache and Django:</span></span>

1. <span data-ttu-id="a9741-128">Otwórz nowe okno terminala.</span><span class="sxs-lookup"><span data-stu-id="a9741-128">Open a new Terminal window.</span></span>
2. <span data-ttu-id="a9741-129">Aby połączyć maszyny Wirtualnej Azure, wprowadź następujące polecenie.</span><span class="sxs-lookup"><span data-stu-id="a9741-129">To connect to the Azure VM, enter the following command.</span></span> <span data-ttu-id="a9741-130">Jeśli nie utworzono nazwy FQDN, możesz połączyć za pomocą publicznego adresu IP, który jest wyświetlany w podsumowaniu w portalu Azure maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="a9741-130">If you didn't create an FQDN, you can connect by using the public IP address that's displayed in the virtual machine summary in the Azure portal.</span></span>
   
       $ ssh yourusername@yourVmUrl
3. <span data-ttu-id="a9741-131">Aby zainstalować Django, wpisz następujące polecenia:</span><span class="sxs-lookup"><span data-stu-id="a9741-131">To install Django, enter the following commands:</span></span>
   
       $ sudo apt-get install python-setuptools python-pip
       $ sudo pip install django
4. <span data-ttu-id="a9741-132">Aby zainstalować Apache z mod wsgi, wprowadź następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="a9741-132">To install Apache with mod-wsgi, enter the following command:</span></span>
   
       $ sudo apt-get install apache2 libapache2-mod-wsgi

## <a name="create-a-new-django-app"></a><span data-ttu-id="a9741-133">Utwórz nową aplikację Django</span><span class="sxs-lookup"><span data-stu-id="a9741-133">Create a new Django app</span></span>
1. <span data-ttu-id="a9741-134">Aby uzyskać dostępu do maszyny Wirtualnej przy użyciu protokołu SSH, Otwórz okno terminalu, którego użyto w poprzedniej sekcji.</span><span class="sxs-lookup"><span data-stu-id="a9741-134">To use SSH to access your VM, open the Terminal window you used in the preceding section.</span></span>
2. <span data-ttu-id="a9741-135">Aby utworzyć nowy projekt Django, wprowadź następujące polecenia:</span><span class="sxs-lookup"><span data-stu-id="a9741-135">To create a new Django project, enter the following commands:</span></span>
   
       $ cd /var/www
       $ sudo django-admin.py startproject helloworld
   
   <span data-ttu-id="a9741-136">`django-admin.py` Skryptu wygenerowanie podstawowej struktury witryn skonstruowanych na podstawie Django:</span><span class="sxs-lookup"><span data-stu-id="a9741-136">The `django-admin.py` script generates a basic structure for Django-based websites:</span></span>
   
   * <span data-ttu-id="a9741-137">`helloworld/manage.py`pomaga rozpocząć hosting i Zatrzymaj hosting witryny sieci Web na podstawie Django.</span><span class="sxs-lookup"><span data-stu-id="a9741-137">`helloworld/manage.py` helps you start hosting and stop hosting your Django-based website.</span></span>
   * <span data-ttu-id="a9741-138">`helloworld/helloworld/settings.py`zawiera ustawienia Django dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a9741-138">`helloworld/helloworld/settings.py` has Django settings for your application.</span></span>
   * <span data-ttu-id="a9741-139">`helloworld/helloworld/urls.py`nie ma kodu mapowania między każdego adresu URL i jego widoku.</span><span class="sxs-lookup"><span data-stu-id="a9741-139">`helloworld/helloworld/urls.py` has the mapping code between each URL and its view.</span></span>
3. <span data-ttu-id="a9741-140">W katalogu /var/www/helloworld/helloworld Utwórz nowy plik o nazwie views.py.</span><span class="sxs-lookup"><span data-stu-id="a9741-140">In the /var/www/helloworld/helloworld directory, create a new file named views.py.</span></span> <span data-ttu-id="a9741-141">Ten plik zawiera widok, który renderuje stronę "hello world".</span><span class="sxs-lookup"><span data-stu-id="a9741-141">This file has the view that renders the "hello world" page.</span></span> <span data-ttu-id="a9741-142">W edytorze kodu wprowadź następujące polecenia:</span><span class="sxs-lookup"><span data-stu-id="a9741-142">In your code editor, enter the following commands:</span></span>
   
       from django.http import HttpResponse
       def home(request):
           html = "<html><body>Hello World!</body></html>"
           return HttpResponse(html)
4. <span data-ttu-id="a9741-143">Zastąp zawartość pliku urls.py za pomocą następujących poleceń:</span><span class="sxs-lookup"><span data-stu-id="a9741-143">Replace the contents of the urls.py file with the following commands:</span></span>
   
       from django.conf.urls import patterns, url
       urlpatterns = patterns('',
           url(r'^$', 'helloworld.views.home', name='home'),
       )

## <a name="set-up-apache"></a><span data-ttu-id="a9741-144">Konfigurowanie Apache</span><span class="sxs-lookup"><span data-stu-id="a9741-144">Set up Apache</span></span>
1. <span data-ttu-id="a9741-145">W folderze /etc/apache2/sites-available/helloworld.conf Utwórz plik konfiguracji Apache hosta wirtualnego.</span><span class="sxs-lookup"><span data-stu-id="a9741-145">In the /etc/apache2/sites-available/helloworld.conf folder, create an Apache virtual host configuration file.</span></span> <span data-ttu-id="a9741-146">Ustaw wartość na następujące wartości.</span><span class="sxs-lookup"><span data-stu-id="a9741-146">Set the contents to the following values.</span></span> <span data-ttu-id="a9741-147">Zastąp *yourVmName* rzeczywistą nazwą komputera używasz (na przykład *pyubuntu*).</span><span class="sxs-lookup"><span data-stu-id="a9741-147">Replace *yourVmName* with the actual name of the machine you are using (for example, *pyubuntu*).</span></span>
   
       <VirtualHost *:80>
       ServerName yourVmName
       </VirtualHost>
       WSGIScriptAlias / /var/www/helloworld/helloworld/wsgi.py
       WSGIPythonPath /var/www/helloworld
2. <span data-ttu-id="a9741-148">Aby aktywować lokacji, użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="a9741-148">To activate the site, use the following command:</span></span>
   
       $ sudo a2ensite helloworld
3. <span data-ttu-id="a9741-149">Aby ponownie uruchomić Apache, użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="a9741-149">To restart Apache, use the following command:</span></span>
   
       $ sudo service apache2 reload
4. <span data-ttu-id="a9741-150">Ładowanie strony sieci Web w przeglądarce:</span><span class="sxs-lookup"><span data-stu-id="a9741-150">Load the webpage in your browser:</span></span>
   
   ![Oknie przeglądarki zostanie wyświetlona strona world hello na platformie Azure](./media/python-django-web-app/mac-linux-django-helloworld-browser.png)

## <a name="shut-down-your-azure-virtual-machine"></a><span data-ttu-id="a9741-152">Zamknij maszynę wirtualną z platformy Azure</span><span class="sxs-lookup"><span data-stu-id="a9741-152">Shut down your Azure virtual machine</span></span>
<span data-ttu-id="a9741-153">Po zakończeniu korzystania z tego samouczka, firma Microsoft zaleca zamknięcie lub Usuń maszynę Wirtualną platformy Azure utworzoną w ramach tego samouczka.</span><span class="sxs-lookup"><span data-stu-id="a9741-153">When you're done with this tutorial, we recommend that you shut down or remove the Azure VM you created for the tutorial.</span></span> <span data-ttu-id="a9741-154">Spowoduje to zwolnienie zasobów dla innych samouczków, a można uniknąć naliczania opłat użycia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="a9741-154">This frees up resources for other tutorials, and you can avoid incurring Azure usage charges.</span></span>

