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
# <a name="django-hello-world-web-app-on-a-linux-vm"></a>Aplikacja sieci web Django Hello World na maszynie Wirtualnej systemu Linux
> [!div class="op_single_selector"]
> * [Windows](../windows/classic/python-django-web-app.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
> * [System Mac/Linux](../windows/classic/python-django-web-app.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
> 
> 

<br>

W tym samouczku przedstawiono sposób hosta witryny sieci Web na podstawie Django w systemie Linux w maszynach wirtualnych platformy Azure. W samouczku przyjęto założenie, nie już pewne doświadczenie w systemie Azure. Po zakończeniu samouczka może mieć aplikacji opartej na Django w górę i w chmurze.

Instrukcje:

* Skonfiguruj maszynę wirtualną platformy Azure do hosta Django. Mimo że w tym samouczku wyjaśniono, jak to zrobić w **Linux**, wykonaj te same dla maszyny Wirtualnej systemu Windows Server hostowana na platformie Azure. 
* Utwórz nową aplikację Django w systemie Linux.

Samouczek przedstawia sposób tworzenia podstawowej aplikacji sieci web Hello World. Aplikacja znajduje się w maszynie wirtualnej platformy Azure.

Poniższy zrzut ekranu przedstawia gotową aplikację:

![Oknie przeglądarki zostanie wyświetlona strona Hello World na platformie Azure](./media/python-django-web-app/mac-linux-django-helloworld-browser.png)

[!INCLUDE [create-account-and-vms-note](../../../includes/create-account-and-vms-note.md)]

## <a name="create-and-set-up-an-azure-virtual-machine-to-host-django"></a>Tworzenie i konfigurowanie maszyny wirtualnej platformy Azure na hoście Django

1. Aby utworzyć maszynę wirtualną platformy Azure z rozkładem Ubuntu Server 14.04 LTS, zobacz [Utwórz maszynę wirtualną systemu Linux w portalu Azure](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Możesz również wybrać uwierzytelnianie hasła zamiast za pomocą klucza publicznego SSH.
2. Aby edytować grupy zabezpieczeń sieci, aby zezwolić na ruch przychodzący HTTP na porcie 80, zobacz [tworzenia grup zabezpieczeń sieci w portalu Azure](../../virtual-network/virtual-networks-create-nsg-arm-pportal.md).
3. (Opcjonalnie) Domyślnie nowej maszyny wirtualnej nie ma w pełni kwalifikowaną nazwą domeny (FQDN).  Aby utworzyć Maszynę wirtualną z wykorzystaniem nazwy FQDN, zobacz [utworzenia nazwy FQDN w portalu Azure dla maszyny Wirtualnej systemu Windows](../windows/portal-create-fqdn.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Ten krok nie jest wymagane wykonanie kroków tego samouczka.

## <a id="setup"></a>Konfigurowanie środowiska programowania
> [!NOTE]
> Jeśli musisz zainstalować Python lub chcesz użyć bibliotek klienckich, zobacz [Przewodnik instalacji języka Python](../../python-how-to-install.md).

Maszyny Wirtualnej systemu Ubuntu Linux ma Python 2.7 preinstalowany, ale go nie dołączono Apache lub Django. Wykonaj poniższe kroki, aby nawiązać połączenie z maszyną Wirtualną i zainstaluj Apache i Django:

1. Otwórz nowe okno terminala.
2. Aby połączyć maszyny Wirtualnej Azure, wprowadź następujące polecenie. Jeśli nie utworzono nazwy FQDN, możesz połączyć za pomocą publicznego adresu IP, który jest wyświetlany w podsumowaniu w portalu Azure maszyny wirtualnej.
   
       $ ssh yourusername@yourVmUrl
3. Aby zainstalować Django, wpisz następujące polecenia:
   
       $ sudo apt-get install python-setuptools python-pip
       $ sudo pip install django
4. Aby zainstalować Apache z mod wsgi, wprowadź następujące polecenie:
   
       $ sudo apt-get install apache2 libapache2-mod-wsgi

## <a name="create-a-new-django-app"></a>Utwórz nową aplikację Django
1. Aby uzyskać dostępu do maszyny Wirtualnej przy użyciu protokołu SSH, Otwórz okno terminalu, którego użyto w poprzedniej sekcji.
2. Aby utworzyć nowy projekt Django, wprowadź następujące polecenia:
   
       $ cd /var/www
       $ sudo django-admin.py startproject helloworld
   
   `django-admin.py` Skryptu wygenerowanie podstawowej struktury witryn skonstruowanych na podstawie Django:
   
   * `helloworld/manage.py`pomaga rozpocząć hosting i Zatrzymaj hosting witryny sieci Web na podstawie Django.
   * `helloworld/helloworld/settings.py`zawiera ustawienia Django dla aplikacji.
   * `helloworld/helloworld/urls.py`nie ma kodu mapowania między każdego adresu URL i jego widoku.
3. W katalogu /var/www/helloworld/helloworld Utwórz nowy plik o nazwie views.py. Ten plik zawiera widok, który renderuje stronę "hello world". W edytorze kodu wprowadź następujące polecenia:
   
       from django.http import HttpResponse
       def home(request):
           html = "<html><body>Hello World!</body></html>"
           return HttpResponse(html)
4. Zastąp zawartość pliku urls.py za pomocą następujących poleceń:
   
       from django.conf.urls import patterns, url
       urlpatterns = patterns('',
           url(r'^$', 'helloworld.views.home', name='home'),
       )

## <a name="set-up-apache"></a>Konfigurowanie Apache
1. W folderze /etc/apache2/sites-available/helloworld.conf Utwórz plik konfiguracji Apache hosta wirtualnego. Ustaw wartość na następujące wartości. Zastąp *yourVmName* rzeczywistą nazwą komputera używasz (na przykład *pyubuntu*).
   
       <VirtualHost *:80>
       ServerName yourVmName
       </VirtualHost>
       WSGIScriptAlias / /var/www/helloworld/helloworld/wsgi.py
       WSGIPythonPath /var/www/helloworld
2. Aby aktywować lokacji, użyj następującego polecenia:
   
       $ sudo a2ensite helloworld
3. Aby ponownie uruchomić Apache, użyj następującego polecenia:
   
       $ sudo service apache2 reload
4. Ładowanie strony sieci Web w przeglądarce:
   
   ![Oknie przeglądarki zostanie wyświetlona strona world hello na platformie Azure](./media/python-django-web-app/mac-linux-django-helloworld-browser.png)

## <a name="shut-down-your-azure-virtual-machine"></a>Zamknij maszynę wirtualną z platformy Azure
Po zakończeniu korzystania z tego samouczka, firma Microsoft zaleca zamknięcie lub Usuń maszynę Wirtualną platformy Azure utworzoną w ramach tego samouczka. Spowoduje to zwolnienie zasobów dla innych samouczków, a można uniknąć naliczania opłat użycia platformy Azure.

