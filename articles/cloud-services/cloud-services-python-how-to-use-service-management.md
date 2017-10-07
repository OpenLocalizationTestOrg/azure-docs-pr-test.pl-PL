---
title: "Zarządzanie usługami hello toouse aaaHow interfejsu API (Python) — Przewodnik po funkcji"
description: "Dowiedz się, jak tooprogrammatically wykonywać typowe zadania zarządzania usługi w języku Python."
services: cloud-services
documentationcenter: python
author: lmazuel
manager: wpickett
editor: 
ms.assetid: 61538ec0-1536-4a7e-ae89-95967fe35d73
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 05/30/2017
ms.author: lmazuel
ms.openlocfilehash: b59622203470e1586484cec4033515edb39ca4d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-management-from-python"></a>Jak toouse zarządzania usługami w języku Python
Ten przewodnik przedstawia, jak tooprogrammatically wykonywać typowe zadania zarządzania usługi w języku Python. Witaj **ServiceManagementService** klasy w hello [zestaw Azure SDK for Python](https://github.com/Azure/azure-sdk-for-python) obsługuje dostęp programistyczny toomuch hello usług związanych z zarządzaniem funkcji, które są dostępne w hello [Klasycznego portalu azure] [ management-portal] (takich jak **tworzenie, aktualizowanie i usuwanie usługi w chmurze, wdrożeń, dane usługi zarządzania i maszyn wirtualnych**). Ta funkcja może być przydatne do tworzenia aplikacji, które muszą dostęp programistyczny tooservice zarządzania.

## <a name="WhatIs"></a>Co to jest usługa zarządzania
Witaj interfejs API zarządzania usługami zapewnia dostęp programistyczny toomuch hello funkcji zarządzania usługi dostępne za pośrednictwem hello [klasycznego portalu Azure][management-portal]. Witaj zestaw Azure SDK for Python umożliwia toomanage usługi w chmurze i kont magazynu.

toouse hello interfejs API zarządzania usługami, należy za[tworzenia konta platformy Azure](https://azure.microsoft.com/pricing/free-trial/).

## <a name="Concepts"></a>Pojęcia
Hello zestaw Azure SDK for Python opakowuje hello [interfejs API zarządzania usługami Azure][svc-mgmt-rest-api], która jest interfejs API REST. Wszystkie operacje interfejsu API są realizowane poprzez protokół SSL z wzajemnym uwierzytelnieniem certyfikatami X.509 v3. Usługa zarządzania Hello mogą być używane z wewnątrz w usłudze działającej na platformie Azure lub bezpośrednio za pośrednictwem hello Internetu z poziomu dowolnej aplikacji, który można wysłać żądania HTTPS i odbierania odpowiedzi protokołu HTTPS.

## <a name="Installation"></a>Instalacji
Wszystkie funkcje hello opisane w tym artykule są dostępne w hello `azure-servicemanagement-legacy` pakiet, który można zainstalować przy użyciu narzędzia pip. Aby uzyskać więcej informacji na temat instalacji (na przykład w przypadku nowych tooPython), zobacz ten artykuł: [instalowanie Python i hello Azure SDK](../python-how-to-install.md)

## <a name="Connect"></a>Porady: łączenie tooservice zarządzania
Zarządzanie usługami toohello tooconnect punktu końcowego, należy identyfikator subskrypcji platformy Azure i prawidłowy certyfikat zarządzania. Możesz uzyskać identyfikator subskrypcji za pośrednictwem hello [klasycznego portalu Azure][management-portal].

> [!NOTE]
> Jest teraz możliwe toouse certyfikaty utworzone za pomocą biblioteki OpenSSL uruchomionej w systemie Windows.  Wymaga to Python 2.7.4 lub nowszym. Zaleca się użytkowników toouse biblioteki OpenSSL zamiast PFX, ponieważ obsługę PFX certyfikatów prawdopodobnie zostaną usunięte w przyszłości hello.
>
>

### <a name="management-certificates-on-windowsmaclinux-openssl"></a>Certyfikaty zarządzania na systemem Windows lub Mac/Linux (OpenSSL)
Można użyć [OpenSSL](http://www.openssl.org/) toocreate certyfikat zarządzania.  Faktycznie wymagane dwa certyfikaty toocreate, jeden dla serwera hello ( `.cer` plików) i jeden dla powitania klienta ( `.pem` pliku). Witaj toocreate `.pem` plików, należy wykonać:

    openssl req -x509 -nodes -days 365 -newkey rsa:1024 -keyout mycert.pem -out mycert.pem

Witaj toocreate `.cer` certyfikatów, należy wykonać:

    openssl x509 -inform pem -in mycert.pem -outform der -out mycert.cer

Aby uzyskać więcej informacji o certyfikatach Azure, zobacz [Omówienie certyfikatów dla usług w chmurze Azure](cloud-services-certs-create.md). Pełny opis parametrów biblioteki OpenSSL, zobacz dokumentację hello w [http://www.openssl.org/docs/apps/openssl.html](http://www.openssl.org/docs/apps/openssl.html).

Po utworzeniu tych plików należy tooupload hello `.cer` pliku tooAzure za pomocą akcji "Przekaż" hello karty "Ustawienia" hello hello [klasycznego portalu Azure][management-portal], i wymagają toomake należy wziąć pod uwagę w którym zapisano hello `.pem` pliku.

Po uzyskaniu identyfikator subskrypcji utworzony certyfikat i przekazać hello `.cer` tooAzure plików, można połączyć punkt końcowy zarządzania platformy Azure toohello przekazując hello identyfikator subskrypcji i toohello ścieżka hello `.pem` pliku zbyt**ServiceManagementService**:

    from azure import *
    from azure.servicemanagement import *

    subscription_id = '<your_subscription_id>'
    certificate_path = '<path_to_.pem_certificate>'

    sms = ServiceManagementService(subscription_id, certificate_path)

W hello poprzedzających przykład `sms` jest **ServiceManagementService** obiektu. Witaj **ServiceManagementService** klasy jest toomanage klasy podstawowej używane hello usług platformy Azure.

### <a name="management-certificates-on-windows-makecert"></a>Certyfikaty zarządzania w systemie Windows (MakeCert)
Można utworzyć certyfikat zarządzania z podpisem własnym na przy użyciu maszyny `makecert.exe`.  Otwórz **wiersz polecenia programu Visual Studio** jako **administratora** i użyj hello następujące polecenie, zastępując *AzureCertificate* o nazwie certyfikatu hello chcesz toouse.

    makecert -sky exchange -r -n "CN=AzureCertificate" -pe -a sha1 -len 2048 -ss My "AzureCertificate.cer"

polecenie Hello tworzy hello `.cer` pliku i instaluje je w hello **osobistych** magazynu certyfikatów. Aby uzyskać więcej informacji, zobacz [Omówienie certyfikatów dla usług w chmurze Azure](cloud-services-certs-create.md).

Po utworzeniu certyfikatu hello należy tooupload hello `.cer` pliku tooAzure za pomocą akcji "Przekaż" hello karty "Ustawienia" hello hello [klasycznego portalu Azure][management-portal].

Po uzyskaniu identyfikator subskrypcji utworzony certyfikat i przekazać hello `.cer` tooAzure plików, można połączyć punkt końcowy zarządzania platformy Azure toohello przekazując hello identyfikator subskrypcji i lokalizacji hello hello certyfikatu w Twojej **Osobistych** magazyn certyfikatów za**ServiceManagementService** (ponownie, Zastąp *AzureCertificate* o nazwie hello certyfikatu):

    from azure import *
    from azure.servicemanagement import *

    subscription_id = '<your_subscription_id>'
    certificate_path = 'CURRENT_USER\\my\\AzureCertificate'

    sms = ServiceManagementService(subscription_id, certificate_path)

W hello poprzedzających przykład `sms` jest **ServiceManagementService** obiektu. Witaj **ServiceManagementService** klasy jest toomanage klasy podstawowej używane hello usług platformy Azure.

## <a name="ListAvailableLocations"></a>Jak: wyświetlić listę dostępnych lokalizacji
toolist hello lokalizacje, które są dostępne do obsługi usługi, użyj hello **listy\_lokalizacje** metody:

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    result = sms.list_locations()
    for location in result:
        print(location.name)

Podczas tworzenia usługi w chmurze lub Usługa magazynu należy tooprovide prawidłową lokalizację. Witaj **listy\_lokalizacje** metoda zawsze zwraca aktualną listę hello aktualnie dostępnych lokalizacji. Opracowywania tego tekstu hello dostępne lokalizacje to:

* Europa Zachodnia
* Europa Północna
* Azja Południowo-Wschodnia
* Azja Wschodnia
* Środkowe stany USA
* Środkowo-północne stany USA
* Południowo-środkowe stany USA
* Zachodnie stany USA
* Wschodnie stany USA
* Japonia Wschodnia
* Japonia Zachodnia
* Brazylia Południowa
* Australia Wschodnia
* Australia Południowo-Wschodnia

## <a name="CreateCloudService"></a>Porady: Tworzenie usługi w chmurze
Podczas tworzenia aplikacji i uruchom go na platformie Azure, hello kod i konfiguracja łącznie są nazywane Azure [usługi w chmurze] [ cloud service] (nazywane *usługi hostowanej* w wcześniej Zwalnia Azure). Hello **utworzyć\_hostowanej\_usługi** metoda pozwala toocreate nową usługę hostowaną przez podanie nazwy usługi hostowanej (który musi być unikatowa na platformie Azure), etykiety (automatycznie zakodowanego toobase64) Opis i lokalizację.

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    name = 'myhostedservice'
    label = 'myhostedservice'
    desc = 'my hosted service'
    location = 'West US'

    sms.create_hosted_service(name, label, desc, location)

Możesz wyświetlić listę wszystkich usług hostowanych hello subskrypcji z hello **listy\_hostowane\_usług** metody:

    result = sms.list_hosted_services()

    for hosted_service in result:
        print('Service name: ' + hosted_service.service_name)
        print('Management URL: ' + hosted_service.url)
        print('Location: ' + hosted_service.hosted_service_properties.location)
        print('')

Jeśli chcesz tooget informacji na temat określonej usługi hostowanej, możesz to zrobić przez przekazanie toohello nazwę usługi hostowanej hello **uzyskać\_hostowane\_usługi\_właściwości** — metoda:

    hosted_service = sms.get_hosted_service_properties('myhostedservice')

    print('Service name: ' + hosted_service.service_name)
    print('Management URL: ' + hosted_service.url)
    print('Location: ' + hosted_service.hosted_service_properties.location)

Po utworzeniu usługi w chmurze, można wdrożyć usługę toohello kodu przy hello **utworzyć\_wdrożenia** metody.

## <a name="DeleteCloudService"></a>Porady: usuwanie usługi w chmurze
Usługi w chmurze można usunąć przez przekazanie toohello nazwa usługi hello **usunąć\_hostowanej\_usługi** — metoda:

    sms.delete_hosted_service('myhostedservice')

Przed usunięciem usługi muszą zostać usunięte wszystkie wdrożenia hello usługi. (Zobacz [porady: usuwanie wdrożenia](#DeleteDeployment) Aby uzyskać więcej informacji.)

## <a name="DeleteDeployment"></a>Porady: usuwanie wdrożenia
toodelete wdrożenia, użyj hello **usunąć\_wdrożenia** metody. Witaj poniższy przykład przedstawia sposób toodelete wdrożenia o nazwie `v1`.

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    sms.delete_deployment('myhostedservice', 'v1')

## <a name="CreateStorageService"></a>Porady: Tworzenie usługi magazynu
A [usługi magazynu](../storage/common/storage-create-storage-account.md) zapewnia dostęp tooAzure [obiekty BLOB](../storage/blobs/storage-python-how-to-use-blob-storage.md), [tabel](../cosmos-db/table-storage-how-to-use-python.md), i [kolejek](../storage/queues/storage-python-how-to-use-queue-storage.md). toocreate usługi magazynu, należy nazwę usługi hello (od 3 do 24 małych liter i unikatowa na platformie Azure), opis etykiety (w górę too100 znaków, automatycznie zakodowanego toobase64) i lokalizację. Witaj poniższy przykład pokazuje, jak toocreate magazynu usługi, określając lokalizację.

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    name = 'mystorageaccount'
    label = 'mystorageaccount'
    location = 'West US'
    desc = 'My storage account description.'

    result = sms.create_storage_account(name, desc, label, location=location)

    operation_result = sms.get_operation_status(result.request_id)
    print('Operation status: ' + operation_result.status)

Należy zwrócić uwagę w hello poprzedzających przykładzie stan hello hello **utworzyć\_magazynu\_konta** operacji mogą być pobierane przez przekazanie hello wynik zwracany przez **utworzyć\_magazynu \_konta** toohello **uzyskać\_operacji\_stan** metody.  

Można wyświetlić listę kont magazynu oraz ich właściwości z hello **listy\_magazynu\_kont** metody:

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    result = sms.list_storage_accounts()
    for account in result:
        print('Service name: ' + account.service_name)
        print('Location: ' + account.storage_service_properties.location)
        print('')

## <a name="DeleteStorageService"></a>Porady: usuwanie usługi magazynu
Usługa Magazyn można usunąć przez przekazanie toohello nazwa usługi magazynu hello **usunąć\_magazynu\_konta** metody. Usunięcie usługi magazynu powoduje usunięcie wszystkich danych przechowywanych w usłudze hello (obiekty BLOB, tabel i kolejek).

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    sms.delete_storage_account('mystorageaccount')

## <a name="ListOperatingSystems"></a>Jak: wyświetlić listę dostępnych systemów operacyjnych
systemy operacyjne hello toolist, które są dostępne do obsługi usługi, użyj hello **listy\_działających\_systemów** metody:

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    result = sms.list_operating_systems()

    for os in result:
        print('OS: ' + os.label)
        print('Family: ' + os.family_label)
        print('Active: ' + str(os.is_active))

Alternatywnie można użyć hello **listy\_operacyjnego\_systemu\_rodzin** metodę, która grup systemów operacyjnych hello rodziny:

    result = sms.list_operating_system_families()

    for family in result:
        print('Family: ' + family.label)
        for os in family.operating_systems:
            if os.is_active:
                print('OS: ' + os.label)
                print('Version: ' + os.version)
        print('')

## <a name="CreateVMImage"></a>Porady: Tworzenie obrazu systemu operacyjnego
tooadd systemu operacyjnego obrazu toohello repozytorium obrazów, użyj hello **dodać\_os\_obrazu** metody:

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    name = 'mycentos'
    label = 'mycentos'
    os = 'Linux' # Linux or Windows
    media_link = 'url_to_storage_blob_for_source_image_vhd'

    result = sms.add_os_image(label, media_link, name, os)

    operation_result = sms.get_operation_status(result.request_id)
    print('Operation status: ' + operation_result.status)

obrazy systemu operacyjnego hello toolist, które są dostępne, użyj hello **listy\_os\_obrazów** metody. Zawiera wszystkie obrazy platformy i obrazów użytkowników:

    result = sms.list_os_images()

    for image in result:
        print('Name: ' + image.name)
        print('Label: ' + image.label)
        print('OS: ' + image.os)
        print('Category: ' + image.category)
        print('Description: ' + image.description)
        print('Location: ' + image.location)
        print('Media link: ' + image.media_link)
        print('')

## <a name="DeleteVMImage"></a>Porady: usuwanie obrazu systemu operacyjnego
toodelete obrazu użytkownika, użyj hello **usunąć\_os\_obrazu** metody:

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    result = sms.delete_os_image('mycentos')

    operation_result = sms.get_operation_status(result.request_id)
    print('Operation status: ' + operation_result.status)

## <a name="CreateVM"></a>Porady: tworzenie maszyny wirtualnej
toocreate maszyny wirtualnej, należy najpierw toocreate [usługi w chmurze](#CreateCloudService).  Następnie utwórz hello wdrożenia maszyny wirtualnej przy użyciu hello **utworzyć\_wirtualnego\_maszyny\_wdrożenia** — metoda:

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    name = 'myvm'
    location = 'West US'

    #Set hello location
    sms.create_hosted_service(service_name=name,
        label=name,
        location=location)

    # Name of an os image as returned by list_os_images
    image_name = 'OpenLogic__OpenLogic-CentOS-62-20120531-en-us-30GB.vhd'

    # Destination storage account container/blob where hello VM disk
    # will be created
    media_link = 'url_to_target_storage_blob_for_vm_hd'

    # Linux VM configuration, you can use WindowsConfigurationSet
    # for a Windows VM instead
    linux_config = LinuxConfigurationSet('myhostname', 'myuser', 'mypassword', True)

    os_hd = OSVirtualHardDisk(image_name, media_link)

    sms.create_virtual_machine_deployment(service_name=name,
        deployment_name=name,
        deployment_slot='production',
        label=name,
        role_name=name,
        system_config=linux_config,
        os_virtual_hard_disk=os_hd,
        role_size='Small')

## <a name="DeleteVM"></a>Porady: usuwanie maszyny wirtualnej
toodelete maszyny wirtualnej, należy najpierw usunąć hello wdrożenia przy użyciu hello **usunąć\_wdrożenia** metody:

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    sms.delete_deployment(service_name='myvm',
        deployment_name='myvm')

następnie można usunąć usługi w chmurze Hello przy użyciu hello **usunąć\_hostowanej\_usługi** metody:

    sms.delete_hosted_service(service_name='myvm')

## <a name="how-to-create-a-virtual-machine-from-a-captured-virtual-machine-image"></a>Porady: Tworzenie maszyny wirtualnej z obrazu przechwyconych maszyny wirtualnej
toocapture obrazu maszyny Wirtualnej, należy najpierw wywołać hello **przechwytywania\_wirtualna\_obrazu** metody:

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    # replace hello below three parameters with actual values
    hosted_service_name = 'hs1'
    deployment_name = 'dep1'
    vm_name = 'vm1'

    image_name = vm_name + 'image'
    image = CaptureRoleAsVMImage    ('Specialized',
        image_name,
        image_name + 'label',
        image_name + 'description',
        'english',
        'mygroup')

    result = sms.capture_vm_image(
            hosted_service_name,
            deployment_name,
            vm_name,
            image
        )

Następnie toomake się, że pomyślnie zostały przechwycony obraz powitania, użyj hello **listy\_wirtualna\_obrazów** interfejsu api i upewnij się, że obraz jest wyświetlana w wynikach hello:

    images = sms.list_vm_images()

toofinally utworzyć hello maszyny wirtualnej za pomocą przechwycony obraz powitania, użyj hello **utworzyć\_wirtualnego\_maszyny\_wdrożenia** jak wcześniej, ale tym razem przekazywanie hello vm_image_name zamiast niego

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    name = 'myvm'
    location = 'West US'

    #Set hello location
    sms.create_hosted_service(service_name=name,
        label=name,
        location=location)

    sms.create_virtual_machine_deployment(service_name=name,
        deployment_name=name,
        deployment_slot='production',
        label=name,
        role_name=name,
        system_config=linux_config,
        os_virtual_hard_disk=None,
        role_size='Small',
        vm_image_name = image_name)

więcej informacji o toolearn, toocapture maszyny wirtualnej systemu Linux, zobacz temat [jak tooCapture maszyny wirtualnej systemu Linux.](../virtual-machines/linux/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)

więcej informacji o toolearn, toocapture maszyny wirtualnej systemu Windows, zobacz temat [jak tooCapture maszyny wirtualnej systemu Windows.](../virtual-machines/windows/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

## <a name="What's Next"> </a>Następne kroki
Teraz, kiedy znasz już podstawy hello zarządzania usługami, można uzyskać dostępu do hello [kompletne API dokumentacji dla hello Azure Python SDK](http://azure-sdk-for-python.readthedocs.org/) i wykonać złożone zadania łatwo toomanage aplikacji python.

Aby uzyskać więcej informacji, zobacz hello [Centrum deweloperów języka Python](/develop/python/).

[What is Service Management]: #WhatIs
[Concepts]: #Concepts
[How to: Connect tooservice management]: #Connect
[How to: List available locations]: #ListAvailableLocations
[How to: Create a cloud service]: #CreateCloudService
[How to: Delete a cloud service]: #DeleteCloudService
[How to: Create a deployment]: #CreateDeployment
[How to: Update a deployment]: #UpdateDeployment
[How to: Move deployments between staging and production]: #MoveDeployments
[How to: Delete a deployment]: #DeleteDeployment
[How to: Create a storage service]: #CreateStorageService
[How to: Delete a storage service]: #DeleteStorageService
[How to: List available operating systems]: #ListOperatingSystems
[How to: Create an operating system image]: #CreateVMImage
[How to: Delete an operating system image]: #DeleteVMImage
[How to: Create a virtual machine]: #CreateVM
[How to: Delete a virtual machine]: #DeleteVM
[Next Steps]: #NextSteps
[management-portal]: https://manage.windowsazure.com/
[svc-mgmt-rest-api]: http://msdn.microsoft.com/library/windowsazure/ee460799.aspx


[cloud service]:/services/cloud-services/
