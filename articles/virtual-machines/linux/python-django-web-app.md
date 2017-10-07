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
# <a name="django-hello-world-web-app-on-a-linux-vm"></a>Aplikacja sieci web Django Hello World na maszynie Wirtualnej systemu Linux
> [!div class="op_single_selector"]
> * [Windows](../windows/classic/python-django-web-app.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
> * [System Mac/Linux](../windows/classic/python-django-web-app.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
> 
> 

<br>

W tym samouczku przedstawiono sposób toohost witryny sieci Web na podstawie Django w systemie Linux w maszynach wirtualnych platformy Azure. W samouczku hello przyjęto założenie, nie już pewne doświadczenie w systemie Azure. Po zakończeniu samouczka hello może mieć aplikacji opartej na Django w górę i w chmurze hello.

Instrukcje:

* Konfigurowanie maszyny wirtualnej platformy Azure toohost Django. Mimo że w tym samouczku wyjaśniono, jak toodo to dla **Linux**, możesz zrobić hello takie same dla maszyny Wirtualnej systemu Windows Server hostowana na platformie Azure. 
* Utwórz nową aplikację Django w systemie Linux.

Witaj samouczek pokazuje, jak aplikacja sieci web toobuild podstawowe Hello World. Aplikacja Hello jest hostowana na maszynie wirtualnej platformy Azure.

powitania po zrzut ekranu przedstawia aplikacji hello zakończone:

![Oknie przeglądarki zostanie wyświetlona strona Hello World hello na platformie Azure](./media/python-django-web-app/mac-linux-django-helloworld-browser.png)

[!INCLUDE [create-account-and-vms-note](../../../includes/create-account-and-vms-note.md)]

## <a name="create-and-set-up-an-azure-virtual-machine-toohost-django"></a>Tworzenie i konfigurowanie maszyny wirtualnej platformy Azure toohost Django

1. Zobacz toocreate maszyny wirtualnej platformy Azure z hello dystrybucji Ubuntu Server 14.04 LTS [Utwórz maszynę wirtualną systemu Linux w portalu Azure hello](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Możesz również wybrać uwierzytelnianie hasła zamiast za pomocą klucza publicznego SSH.
2. Zobacz tooedit hello sieci zabezpieczeń grupy tooallow przychodzące HTTP ruchu tooport 80, [tworzenia grup zabezpieczeń sieci w portalu Azure hello](../../virtual-network/virtual-networks-create-nsg-arm-pportal.md).
3. (Opcjonalnie) Domyślnie nowej maszyny wirtualnej nie ma w pełni kwalifikowaną nazwą domeny (FQDN).  Zobacz toocreate maszynę Wirtualną za pomocą nazwy FQDN, [utworzenia nazwy FQDN w hello portalu Azure dla maszyny Wirtualnej systemu Windows](../windows/portal-create-fqdn.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Ten krok nie jest wymagane wykonanie kroków tego samouczka.

## <a id="setup"></a>Konfigurowanie środowiska deweloperskiego hello
> [!NOTE]
> Jeśli konieczne tooinstall Python lub toouse powitania klienta biblioteki, zobacz hello [Przewodnik instalacji języka Python](../../python-how-to-install.md).

Witaj maszyny Wirtualnej systemu Ubuntu Linux ma Python 2.7 preinstalowany, ale go nie dołączono Apache lub Django. Ukończ hello następujące kroki tooconnect tooyour maszyny Wirtualnej, a następnie zainstaluj Apache i Django:

1. Otwórz nowe okno terminala.
2. toohello tooconnect maszyny Wirtualnej platformy Azure, wprowadź następujące polecenie hello. Jeśli nie utworzono nazwy FQDN, można połączyć się przy użyciu hello publiczny adres IP wyświetlany w maszynie wirtualnej hello podsumowania w hello portalu Azure.
   
       $ ssh yourusername@yourVmUrl
3. tooinstall Django, wprowadź hello następującego polecenia:
   
       $ sudo apt-get install python-setuptools python-pip
       $ sudo pip install django
4. tooinstall Apache z mod wsgi, wprowadź następujące polecenie hello:
   
       $ sudo apt-get install apache2 libapache2-mod-wsgi

## <a name="create-a-new-django-app"></a>Utwórz nową aplikację Django
1. sieci maszyny Wirtualnej, hello Otwórz okno terminala użyte w powyższej sekcji hello tooaccess SSH toouse.
2. toocreate nowy projekt Django, wprowadź hello następującego polecenia:
   
       $ cd /var/www
       $ sudo django-admin.py startproject helloworld
   
   Witaj `django-admin.py` skryptu wygenerowanie podstawowej struktury witryn skonstruowanych na podstawie Django:
   
   * `helloworld/manage.py`pomaga rozpocząć hosting i Zatrzymaj hosting witryny sieci Web na podstawie Django.
   * `helloworld/helloworld/settings.py`zawiera ustawienia Django dla aplikacji.
   * `helloworld/helloworld/urls.py`nie ma kodu mapowania hello między każdego adresu URL i jego widoku.
3. W katalogu /var/www/helloworld/helloworld hello Utwórz nowy plik o nazwie views.py. Ten plik zawiera widok hello, który renderuje stronę "hello world" hello. W edytorze kodu wprowadź hello następującego polecenia:
   
       from django.http import HttpResponse
       def home(request):
           html = "<html><body>Hello World!</body></html>"
           return HttpResponse(html)
4. Zastąp zawartość pliku urls.py hello hello hello następującego polecenia:
   
       from django.conf.urls import patterns, url
       urlpatterns = patterns('',
           url(r'^$', 'helloworld.views.home', name='home'),
       )

## <a name="set-up-apache"></a>Konfigurowanie Apache
1. W folderze /etc/apache2/sites-available/helloworld.conf hello należy utworzyć plik konfiguracji Apache hosta wirtualnego. Ustaw następujące wartości toohello zawartość hello. Zastąp *yourVmName* z rzeczywistą nazwą hello maszyny hello używasz (na przykład *pyubuntu*).
   
       <VirtualHost *:80>
       ServerName yourVmName
       </VirtualHost>
       WSGIScriptAlias / /var/www/helloworld/helloworld/wsgi.py
       WSGIPythonPath /var/www/helloworld
2. Witryna tooactivate hello hello Użyj następującego polecenia:
   
       $ sudo a2ensite helloworld
3. toorestart Apache, hello Użyj następującego polecenia:
   
       $ sudo service apache2 reload
4. Ładowanie hello strony sieci Web w przeglądarce:
   
   ![Okno przeglądarki Wyświetla hello hello world strony na platformie Azure](./media/python-django-web-app/mac-linux-django-helloworld-browser.png)

## <a name="shut-down-your-azure-virtual-machine"></a>Zamknij maszynę wirtualną z platformy Azure
Po zakończeniu korzystania z tego samouczka, firma Microsoft zaleca zamknięcie lub usunąć hello utworzone w samouczku hello maszyny Wirtualnej platformy Azure. Spowoduje to zwolnienie zasobów dla innych samouczków, a można uniknąć naliczania opłat użycia platformy Azure.

