---
title: "aaaPython aplikacji sieci web przy użyciu platformy Django na maszynie Wirtualnej platformy Azure systemu Linux | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toohost na podstawie Django sieci web aplikacji na platformie Azure przy użyciu maszyny Wirtualnej systemu Linux."
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
ms.openlocfilehash: 520c47e19e8ffb4bb866f70772d506ddf76e242c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="django-hello-world-web-app-on-a-linux-vm"></a><span data-ttu-id="7de73-103">Aplikacja sieci web Django Hello World na maszynie Wirtualnej systemu Linux</span><span class="sxs-lookup"><span data-stu-id="7de73-103">Django Hello World web app on a Linux VM</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="7de73-104">Windows</span><span class="sxs-lookup"><span data-stu-id="7de73-104">Windows</span></span>](../windows/classic/python-django-web-app.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
> * [<span data-ttu-id="7de73-105">System Mac/Linux</span><span class="sxs-lookup"><span data-stu-id="7de73-105">Mac/Linux</span></span>](../windows/classic/python-django-web-app.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
> 
> 

<br>

<span data-ttu-id="7de73-106">W tym samouczku przedstawiono sposób toohost witryny sieci Web na podstawie Django w systemie Linux w maszynach wirtualnych platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="7de73-106">This tutorial shows you how toohost a Django-based website in Linux in Azure Virtual Machines.</span></span> <span data-ttu-id="7de73-107">W samouczku hello przyjęto założenie, nie już pewne doświadczenie w systemie Azure.</span><span class="sxs-lookup"><span data-stu-id="7de73-107">In hello tutorial, we assume no prior experience with Azure.</span></span> <span data-ttu-id="7de73-108">Po zakończeniu samouczka hello może mieć aplikacji opartej na Django w górę i w chmurze hello.</span><span class="sxs-lookup"><span data-stu-id="7de73-108">When you finish hello tutorial, you can have a Django-based application up and running in hello cloud.</span></span>

<span data-ttu-id="7de73-109">Instrukcje:</span><span class="sxs-lookup"><span data-stu-id="7de73-109">Learn how to:</span></span>

* <span data-ttu-id="7de73-110">Konfigurowanie maszyny wirtualnej platformy Azure toohost Django.</span><span class="sxs-lookup"><span data-stu-id="7de73-110">Set up an Azure virtual machine toohost Django.</span></span> <span data-ttu-id="7de73-111">Mimo że w tym samouczku wyjaśniono, jak toodo to dla **Linux**, możesz zrobić hello takie same dla maszyny Wirtualnej systemu Windows Server hostowana na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="7de73-111">Although this tutorial explains how toodo this for **Linux**, you can do hello same for a Windows Server VM hosted in Azure.</span></span> 
* <span data-ttu-id="7de73-112">Utwórz nową aplikację Django w systemie Linux.</span><span class="sxs-lookup"><span data-stu-id="7de73-112">Create a new Django application in Linux.</span></span>

<span data-ttu-id="7de73-113">Witaj samouczek pokazuje, jak aplikacja sieci web toobuild podstawowe Hello World.</span><span class="sxs-lookup"><span data-stu-id="7de73-113">hello tutorial shows you how toobuild a basic Hello World web application.</span></span> <span data-ttu-id="7de73-114">Aplikacja Hello jest hostowana na maszynie wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="7de73-114">hello application is hosted in an Azure virtual machine.</span></span>

<span data-ttu-id="7de73-115">powitania po zrzut ekranu przedstawia aplikacji hello zakończone:</span><span class="sxs-lookup"><span data-stu-id="7de73-115">hello following screenshot shows hello completed application:</span></span>

![Oknie przeglądarki zostanie wyświetlona strona Hello World hello na platformie Azure](./media/python-django-web-app/mac-linux-django-helloworld-browser.png)

[!INCLUDE [create-account-and-vms-note](../../../includes/create-account-and-vms-note.md)]

## <a name="create-and-set-up-an-azure-virtual-machine-toohost-django"></a><span data-ttu-id="7de73-117">Tworzenie i konfigurowanie maszyny wirtualnej platformy Azure toohost Django</span><span class="sxs-lookup"><span data-stu-id="7de73-117">Create and set up an Azure virtual machine toohost Django</span></span>

1. <span data-ttu-id="7de73-118">Zobacz toocreate maszyny wirtualnej platformy Azure z hello dystrybucji Ubuntu Server 14.04 LTS [Utwórz maszynę wirtualną systemu Linux w portalu Azure hello](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="7de73-118">toocreate an Azure virtual machine with hello Ubuntu Server 14.04 LTS distribution, see [Create a Linux virtual machine in hello Azure portal](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="7de73-119">Możesz również wybrać uwierzytelnianie hasła zamiast za pomocą klucza publicznego SSH.</span><span class="sxs-lookup"><span data-stu-id="7de73-119">You also can choose password authentication instead of using an SSH public key.</span></span>
2. <span data-ttu-id="7de73-120">Zobacz tooedit hello sieci zabezpieczeń grupy tooallow przychodzące HTTP ruchu tooport 80, [tworzenia grup zabezpieczeń sieci w portalu Azure hello](../../virtual-network/virtual-networks-create-nsg-arm-pportal.md).</span><span class="sxs-lookup"><span data-stu-id="7de73-120">tooedit hello network security group tooallow incoming HTTP traffic tooport 80, see [Create network security groups in hello Azure portal](../../virtual-network/virtual-networks-create-nsg-arm-pportal.md).</span></span>
3. <span data-ttu-id="7de73-121">(Opcjonalnie) Domyślnie nowej maszyny wirtualnej nie ma w pełni kwalifikowaną nazwą domeny (FQDN).</span><span class="sxs-lookup"><span data-stu-id="7de73-121">(Optional) By default, your new virtual machine doesn't have a fully qualified domain name (FQDN).</span></span>  <span data-ttu-id="7de73-122">Zobacz toocreate maszynę Wirtualną za pomocą nazwy FQDN, [utworzenia nazwy FQDN w hello portalu Azure dla maszyny Wirtualnej systemu Windows](../windows/portal-create-fqdn.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="7de73-122">toocreate a VM with an FQDN, see [Create an FQDN in hello Azure portal for a Windows VM](../windows/portal-create-fqdn.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="7de73-123">Ten krok nie jest wymagane wykonanie kroków tego samouczka.</span><span class="sxs-lookup"><span data-stu-id="7de73-123">This step is not required for completing this tutorial.</span></span>

## <span data-ttu-id="7de73-124"><a id="setup"></a>Konfigurowanie środowiska deweloperskiego hello</span><span class="sxs-lookup"><span data-stu-id="7de73-124"><a id="setup"> </a>Set up hello development environment</span></span>
> [!NOTE]
> <span data-ttu-id="7de73-125">Jeśli konieczne tooinstall Python lub toouse powitania klienta biblioteki, zobacz hello [Przewodnik instalacji języka Python](../../python-how-to-install.md).</span><span class="sxs-lookup"><span data-stu-id="7de73-125">If you need tooinstall Python or want toouse hello client libraries, see hello [Python installation guide](../../python-how-to-install.md).</span></span>

<span data-ttu-id="7de73-126">Witaj maszyny Wirtualnej systemu Ubuntu Linux ma Python 2.7 preinstalowany, ale go nie dołączono Apache lub Django.</span><span class="sxs-lookup"><span data-stu-id="7de73-126">hello Ubuntu Linux VM has Python 2.7 preinstalled, but it doesn't come with Apache or Django.</span></span> <span data-ttu-id="7de73-127">Ukończ hello następujące kroki tooconnect tooyour maszyny Wirtualnej, a następnie zainstaluj Apache i Django:</span><span class="sxs-lookup"><span data-stu-id="7de73-127">Complete hello following steps tooconnect tooyour VM and install Apache and Django:</span></span>

1. <span data-ttu-id="7de73-128">Otwórz nowe okno terminala.</span><span class="sxs-lookup"><span data-stu-id="7de73-128">Open a new Terminal window.</span></span>
2. <span data-ttu-id="7de73-129">toohello tooconnect maszyny Wirtualnej platformy Azure, wprowadź następujące polecenie hello.</span><span class="sxs-lookup"><span data-stu-id="7de73-129">tooconnect toohello Azure VM, enter hello following command.</span></span> <span data-ttu-id="7de73-130">Jeśli nie utworzono nazwy FQDN, można połączyć się przy użyciu hello publiczny adres IP wyświetlany w maszynie wirtualnej hello podsumowania w hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="7de73-130">If you didn't create an FQDN, you can connect by using hello public IP address that's displayed in hello virtual machine summary in hello Azure portal.</span></span>
   
       $ ssh yourusername@yourVmUrl
3. <span data-ttu-id="7de73-131">tooinstall Django, wprowadź hello następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="7de73-131">tooinstall Django, enter hello following commands:</span></span>
   
       $ sudo apt-get install python-setuptools python-pip
       $ sudo pip install django
4. <span data-ttu-id="7de73-132">tooinstall Apache z mod wsgi, wprowadź następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="7de73-132">tooinstall Apache with mod-wsgi, enter hello following command:</span></span>
   
       $ sudo apt-get install apache2 libapache2-mod-wsgi

## <a name="create-a-new-django-app"></a><span data-ttu-id="7de73-133">Utwórz nową aplikację Django</span><span class="sxs-lookup"><span data-stu-id="7de73-133">Create a new Django app</span></span>
1. <span data-ttu-id="7de73-134">sieci maszyny Wirtualnej, hello Otwórz okno terminala użyte w powyższej sekcji hello tooaccess SSH toouse.</span><span class="sxs-lookup"><span data-stu-id="7de73-134">toouse SSH tooaccess your VM, open hello Terminal window you used in hello preceding section.</span></span>
2. <span data-ttu-id="7de73-135">toocreate nowy projekt Django, wprowadź hello następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="7de73-135">toocreate a new Django project, enter hello following commands:</span></span>
   
       $ cd /var/www
       $ sudo django-admin.py startproject helloworld
   
   <span data-ttu-id="7de73-136">Witaj `django-admin.py` skryptu wygenerowanie podstawowej struktury witryn skonstruowanych na podstawie Django:</span><span class="sxs-lookup"><span data-stu-id="7de73-136">hello `django-admin.py` script generates a basic structure for Django-based websites:</span></span>
   
   * <span data-ttu-id="7de73-137">`helloworld/manage.py`pomaga rozpocząć hosting i Zatrzymaj hosting witryny sieci Web na podstawie Django.</span><span class="sxs-lookup"><span data-stu-id="7de73-137">`helloworld/manage.py` helps you start hosting and stop hosting your Django-based website.</span></span>
   * <span data-ttu-id="7de73-138">`helloworld/helloworld/settings.py`zawiera ustawienia Django dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="7de73-138">`helloworld/helloworld/settings.py` has Django settings for your application.</span></span>
   * <span data-ttu-id="7de73-139">`helloworld/helloworld/urls.py`nie ma kodu mapowania hello między każdego adresu URL i jego widoku.</span><span class="sxs-lookup"><span data-stu-id="7de73-139">`helloworld/helloworld/urls.py` has hello mapping code between each URL and its view.</span></span>
3. <span data-ttu-id="7de73-140">W katalogu /var/www/helloworld/helloworld hello Utwórz nowy plik o nazwie views.py.</span><span class="sxs-lookup"><span data-stu-id="7de73-140">In hello /var/www/helloworld/helloworld directory, create a new file named views.py.</span></span> <span data-ttu-id="7de73-141">Ten plik zawiera widok hello, który renderuje stronę "hello world" hello.</span><span class="sxs-lookup"><span data-stu-id="7de73-141">This file has hello view that renders hello "hello world" page.</span></span> <span data-ttu-id="7de73-142">W edytorze kodu wprowadź hello następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="7de73-142">In your code editor, enter hello following commands:</span></span>
   
       from django.http import HttpResponse
       def home(request):
           html = "<html><body>Hello World!</body></html>"
           return HttpResponse(html)
4. <span data-ttu-id="7de73-143">Zastąp zawartość pliku urls.py hello hello hello następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="7de73-143">Replace hello contents of hello urls.py file with hello following commands:</span></span>
   
       from django.conf.urls import patterns, url
       urlpatterns = patterns('',
           url(r'^$', 'helloworld.views.home', name='home'),
       )

## <a name="set-up-apache"></a><span data-ttu-id="7de73-144">Konfigurowanie Apache</span><span class="sxs-lookup"><span data-stu-id="7de73-144">Set up Apache</span></span>
1. <span data-ttu-id="7de73-145">W folderze /etc/apache2/sites-available/helloworld.conf hello należy utworzyć plik konfiguracji Apache hosta wirtualnego.</span><span class="sxs-lookup"><span data-stu-id="7de73-145">In hello /etc/apache2/sites-available/helloworld.conf folder, create an Apache virtual host configuration file.</span></span> <span data-ttu-id="7de73-146">Ustaw następujące wartości toohello zawartość hello.</span><span class="sxs-lookup"><span data-stu-id="7de73-146">Set hello contents toohello following values.</span></span> <span data-ttu-id="7de73-147">Zastąp *yourVmName* z rzeczywistą nazwą hello maszyny hello używasz (na przykład *pyubuntu*).</span><span class="sxs-lookup"><span data-stu-id="7de73-147">Replace *yourVmName* with hello actual name of hello machine you are using (for example, *pyubuntu*).</span></span>
   
       <VirtualHost *:80>
       ServerName yourVmName
       </VirtualHost>
       WSGIScriptAlias / /var/www/helloworld/helloworld/wsgi.py
       WSGIPythonPath /var/www/helloworld
2. <span data-ttu-id="7de73-148">Witryna tooactivate hello hello Użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="7de73-148">tooactivate hello site, use hello following command:</span></span>
   
       $ sudo a2ensite helloworld
3. <span data-ttu-id="7de73-149">toorestart Apache, hello Użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="7de73-149">toorestart Apache, use hello following command:</span></span>
   
       $ sudo service apache2 reload
4. <span data-ttu-id="7de73-150">Ładowanie hello strony sieci Web w przeglądarce:</span><span class="sxs-lookup"><span data-stu-id="7de73-150">Load hello webpage in your browser:</span></span>
   
   ![Okno przeglądarki Wyświetla hello hello world strony na platformie Azure](./media/python-django-web-app/mac-linux-django-helloworld-browser.png)

## <a name="shut-down-your-azure-virtual-machine"></a><span data-ttu-id="7de73-152">Zamknij maszynę wirtualną z platformy Azure</span><span class="sxs-lookup"><span data-stu-id="7de73-152">Shut down your Azure virtual machine</span></span>
<span data-ttu-id="7de73-153">Po zakończeniu korzystania z tego samouczka, firma Microsoft zaleca zamknięcie lub usunąć hello utworzone w samouczku hello maszyny Wirtualnej platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="7de73-153">When you're done with this tutorial, we recommend that you shut down or remove hello Azure VM you created for hello tutorial.</span></span> <span data-ttu-id="7de73-154">Spowoduje to zwolnienie zasobów dla innych samouczków, a można uniknąć naliczania opłat użycia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="7de73-154">This frees up resources for other tutorials, and you can avoid incurring Azure usage charges.</span></span>

