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
# <a name="how-toouse-service-management-from-python"></a><span data-ttu-id="02a96-103">Jak toouse zarządzania usługami w języku Python</span><span class="sxs-lookup"><span data-stu-id="02a96-103">How toouse Service Management from Python</span></span>
<span data-ttu-id="02a96-104">Ten przewodnik przedstawia, jak tooprogrammatically wykonywać typowe zadania zarządzania usługi w języku Python.</span><span class="sxs-lookup"><span data-stu-id="02a96-104">This guide shows you how tooprogrammatically perform common service management tasks from Python.</span></span> <span data-ttu-id="02a96-105">Witaj **ServiceManagementService** klasy w hello [zestaw Azure SDK for Python](https://github.com/Azure/azure-sdk-for-python) obsługuje dostęp programistyczny toomuch hello usług związanych z zarządzaniem funkcji, które są dostępne w hello [Klasycznego portalu azure] [ management-portal] (takich jak **tworzenie, aktualizowanie i usuwanie usługi w chmurze, wdrożeń, dane usługi zarządzania i maszyn wirtualnych**).</span><span class="sxs-lookup"><span data-stu-id="02a96-105">hello **ServiceManagementService** class in hello [Azure SDK for Python](https://github.com/Azure/azure-sdk-for-python) supports programmatic access toomuch of hello service management-related functionality that is available in hello [Azure classic portal][management-portal] (such as **creating, updating, and deleting cloud services, deployments, data management services, and virtual machines**).</span></span> <span data-ttu-id="02a96-106">Ta funkcja może być przydatne do tworzenia aplikacji, które muszą dostęp programistyczny tooservice zarządzania.</span><span class="sxs-lookup"><span data-stu-id="02a96-106">This functionality can be useful in building applications that need programmatic access tooservice management.</span></span>

## <span data-ttu-id="02a96-107"><a name="WhatIs"></a>Co to jest usługa zarządzania</span><span class="sxs-lookup"><span data-stu-id="02a96-107"><a name="WhatIs"> </a>What is Service Management</span></span>
<span data-ttu-id="02a96-108">Witaj interfejs API zarządzania usługami zapewnia dostęp programistyczny toomuch hello funkcji zarządzania usługi dostępne za pośrednictwem hello [klasycznego portalu Azure][management-portal].</span><span class="sxs-lookup"><span data-stu-id="02a96-108">hello Service Management API provides programmatic access toomuch of hello service management functionality available through hello [Azure classic portal][management-portal].</span></span> <span data-ttu-id="02a96-109">Witaj zestaw Azure SDK for Python umożliwia toomanage usługi w chmurze i kont magazynu.</span><span class="sxs-lookup"><span data-stu-id="02a96-109">hello Azure SDK for Python allows you toomanage your cloud services and storage accounts.</span></span>

<span data-ttu-id="02a96-110">toouse hello interfejs API zarządzania usługami, należy za[tworzenia konta platformy Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="02a96-110">toouse hello Service Management API, you need too[create an Azure account](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <span data-ttu-id="02a96-111"><a name="Concepts"></a>Pojęcia</span><span class="sxs-lookup"><span data-stu-id="02a96-111"><a name="Concepts"> </a>Concepts</span></span>
<span data-ttu-id="02a96-112">Hello zestaw Azure SDK for Python opakowuje hello [interfejs API zarządzania usługami Azure][svc-mgmt-rest-api], która jest interfejs API REST.</span><span class="sxs-lookup"><span data-stu-id="02a96-112">hello Azure SDK for Python wraps hello [Azure Service Management API][svc-mgmt-rest-api], which is a REST API.</span></span> <span data-ttu-id="02a96-113">Wszystkie operacje interfejsu API są realizowane poprzez protokół SSL z wzajemnym uwierzytelnieniem certyfikatami X.509 v3.</span><span class="sxs-lookup"><span data-stu-id="02a96-113">All API operations are performed over SSL and mutually authenticated using X.509 v3 certificates.</span></span> <span data-ttu-id="02a96-114">Usługa zarządzania Hello mogą być używane z wewnątrz w usłudze działającej na platformie Azure lub bezpośrednio za pośrednictwem hello Internetu z poziomu dowolnej aplikacji, który można wysłać żądania HTTPS i odbierania odpowiedzi protokołu HTTPS.</span><span class="sxs-lookup"><span data-stu-id="02a96-114">hello management service may be accessed from within a service running in Azure, or directly over hello Internet from any application that can send an HTTPS request and receive an HTTPS response.</span></span>

## <span data-ttu-id="02a96-115"><a name="Installation"></a>Instalacji</span><span class="sxs-lookup"><span data-stu-id="02a96-115"><a name="Installation"> </a>Installation</span></span>
<span data-ttu-id="02a96-116">Wszystkie funkcje hello opisane w tym artykule są dostępne w hello `azure-servicemanagement-legacy` pakiet, który można zainstalować przy użyciu narzędzia pip.</span><span class="sxs-lookup"><span data-stu-id="02a96-116">All hello features described in this article are available in hello `azure-servicemanagement-legacy` package, which you can install using pip.</span></span> <span data-ttu-id="02a96-117">Aby uzyskać więcej informacji na temat instalacji (na przykład w przypadku nowych tooPython), zobacz ten artykuł: [instalowanie Python i hello Azure SDK](../python-how-to-install.md)</span><span class="sxs-lookup"><span data-stu-id="02a96-117">For more information about installation (for example, if you are new tooPython), see this article: [Installing Python and hello Azure SDK](../python-how-to-install.md)</span></span>

## <span data-ttu-id="02a96-118"><a name="Connect"></a>Porady: łączenie tooservice zarządzania</span><span class="sxs-lookup"><span data-stu-id="02a96-118"><a name="Connect"> </a>How to: Connect tooservice management</span></span>
<span data-ttu-id="02a96-119">Zarządzanie usługami toohello tooconnect punktu końcowego, należy identyfikator subskrypcji platformy Azure i prawidłowy certyfikat zarządzania.</span><span class="sxs-lookup"><span data-stu-id="02a96-119">tooconnect toohello Service Management endpoint, you need your Azure subscription ID and a valid management certificate.</span></span> <span data-ttu-id="02a96-120">Możesz uzyskać identyfikator subskrypcji za pośrednictwem hello [klasycznego portalu Azure][management-portal].</span><span class="sxs-lookup"><span data-stu-id="02a96-120">You can obtain your subscription ID through hello [Azure classic portal][management-portal].</span></span>

> [!NOTE]
> <span data-ttu-id="02a96-121">Jest teraz możliwe toouse certyfikaty utworzone za pomocą biblioteki OpenSSL uruchomionej w systemie Windows.</span><span class="sxs-lookup"><span data-stu-id="02a96-121">It is now possible toouse certificates created with OpenSSL when running on Windows.</span></span>  <span data-ttu-id="02a96-122">Wymaga to Python 2.7.4 lub nowszym.</span><span class="sxs-lookup"><span data-stu-id="02a96-122">It requires Python 2.7.4 or later.</span></span> <span data-ttu-id="02a96-123">Zaleca się użytkowników toouse biblioteki OpenSSL zamiast PFX, ponieważ obsługę PFX certyfikatów prawdopodobnie zostaną usunięte w przyszłości hello.</span><span class="sxs-lookup"><span data-stu-id="02a96-123">We recommend users toouse OpenSSL instead of .pfx, since support for .pfx certificates will likely be removed in hello future.</span></span>
>
>

### <a name="management-certificates-on-windowsmaclinux-openssl"></a><span data-ttu-id="02a96-124">Certyfikaty zarządzania na systemem Windows lub Mac/Linux (OpenSSL)</span><span class="sxs-lookup"><span data-stu-id="02a96-124">Management certificates on Windows/Mac/Linux (OpenSSL)</span></span>
<span data-ttu-id="02a96-125">Można użyć [OpenSSL](http://www.openssl.org/) toocreate certyfikat zarządzania.</span><span class="sxs-lookup"><span data-stu-id="02a96-125">You can use [OpenSSL](http://www.openssl.org/) toocreate your management certificate.</span></span>  <span data-ttu-id="02a96-126">Faktycznie wymagane dwa certyfikaty toocreate, jeden dla serwera hello ( `.cer` plików) i jeden dla powitania klienta ( `.pem` pliku).</span><span class="sxs-lookup"><span data-stu-id="02a96-126">You actually need toocreate two certificates, one for hello server (a `.cer` file) and one for hello client (a `.pem` file).</span></span> <span data-ttu-id="02a96-127">Witaj toocreate `.pem` plików, należy wykonać:</span><span class="sxs-lookup"><span data-stu-id="02a96-127">toocreate hello `.pem` file, execute:</span></span>

    openssl req -x509 -nodes -days 365 -newkey rsa:1024 -keyout mycert.pem -out mycert.pem

<span data-ttu-id="02a96-128">Witaj toocreate `.cer` certyfikatów, należy wykonać:</span><span class="sxs-lookup"><span data-stu-id="02a96-128">toocreate hello `.cer` certificate, execute:</span></span>

    openssl x509 -inform pem -in mycert.pem -outform der -out mycert.cer

<span data-ttu-id="02a96-129">Aby uzyskać więcej informacji o certyfikatach Azure, zobacz [Omówienie certyfikatów dla usług w chmurze Azure](cloud-services-certs-create.md).</span><span class="sxs-lookup"><span data-stu-id="02a96-129">For more information about Azure certificates, see [Certificates Overview for Azure Cloud Services](cloud-services-certs-create.md).</span></span> <span data-ttu-id="02a96-130">Pełny opis parametrów biblioteki OpenSSL, zobacz dokumentację hello w [http://www.openssl.org/docs/apps/openssl.html](http://www.openssl.org/docs/apps/openssl.html).</span><span class="sxs-lookup"><span data-stu-id="02a96-130">For a complete description of OpenSSL parameters, see hello documentation at [http://www.openssl.org/docs/apps/openssl.html](http://www.openssl.org/docs/apps/openssl.html).</span></span>

<span data-ttu-id="02a96-131">Po utworzeniu tych plików należy tooupload hello `.cer` pliku tooAzure za pomocą akcji "Przekaż" hello karty "Ustawienia" hello hello [klasycznego portalu Azure][management-portal], i wymagają toomake należy wziąć pod uwagę w którym zapisano hello `.pem` pliku.</span><span class="sxs-lookup"><span data-stu-id="02a96-131">After you have created these files, you need tooupload hello `.cer` file tooAzure via hello "Upload" action of hello "Settings" tab of hello [Azure classic portal][management-portal], and you need toomake note of where you saved hello `.pem` file.</span></span>

<span data-ttu-id="02a96-132">Po uzyskaniu identyfikator subskrypcji utworzony certyfikat i przekazać hello `.cer` tooAzure plików, można połączyć punkt końcowy zarządzania platformy Azure toohello przekazując hello identyfikator subskrypcji i toohello ścieżka hello `.pem` pliku zbyt**ServiceManagementService**:</span><span class="sxs-lookup"><span data-stu-id="02a96-132">After you have obtained your subscription ID, created a certificate, and uploaded hello `.cer` file tooAzure, you can connect toohello Azure management endpoint by passing hello subscription id and hello path toohello `.pem` file too**ServiceManagementService**:</span></span>

    from azure import *
    from azure.servicemanagement import *

    subscription_id = '<your_subscription_id>'
    certificate_path = '<path_to_.pem_certificate>'

    sms = ServiceManagementService(subscription_id, certificate_path)

<span data-ttu-id="02a96-133">W hello poprzedzających przykład `sms` jest **ServiceManagementService** obiektu.</span><span class="sxs-lookup"><span data-stu-id="02a96-133">In hello preceding example, `sms` is a **ServiceManagementService** object.</span></span> <span data-ttu-id="02a96-134">Witaj **ServiceManagementService** klasy jest toomanage klasy podstawowej używane hello usług platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="02a96-134">hello **ServiceManagementService** class is hello primary class used toomanage Azure services.</span></span>

### <a name="management-certificates-on-windows-makecert"></a><span data-ttu-id="02a96-135">Certyfikaty zarządzania w systemie Windows (MakeCert)</span><span class="sxs-lookup"><span data-stu-id="02a96-135">Management certificates on Windows (MakeCert)</span></span>
<span data-ttu-id="02a96-136">Można utworzyć certyfikat zarządzania z podpisem własnym na przy użyciu maszyny `makecert.exe`.</span><span class="sxs-lookup"><span data-stu-id="02a96-136">You can create a self-signed management certificate on your machine using `makecert.exe`.</span></span>  <span data-ttu-id="02a96-137">Otwórz **wiersz polecenia programu Visual Studio** jako **administratora** i użyj hello następujące polecenie, zastępując *AzureCertificate* o nazwie certyfikatu hello chcesz toouse.</span><span class="sxs-lookup"><span data-stu-id="02a96-137">Open a **Visual Studio command prompt** as an **administrator** and use hello following command, replacing *AzureCertificate* with hello certificate name you would like toouse.</span></span>

    makecert -sky exchange -r -n "CN=AzureCertificate" -pe -a sha1 -len 2048 -ss My "AzureCertificate.cer"

<span data-ttu-id="02a96-138">polecenie Hello tworzy hello `.cer` pliku i instaluje je w hello **osobistych** magazynu certyfikatów.</span><span class="sxs-lookup"><span data-stu-id="02a96-138">hello command creates hello `.cer` file, and installs it in hello **Personal** certificate store.</span></span> <span data-ttu-id="02a96-139">Aby uzyskać więcej informacji, zobacz [Omówienie certyfikatów dla usług w chmurze Azure](cloud-services-certs-create.md).</span><span class="sxs-lookup"><span data-stu-id="02a96-139">For more information, see [Certificates Overview for Azure Cloud Services](cloud-services-certs-create.md).</span></span>

<span data-ttu-id="02a96-140">Po utworzeniu certyfikatu hello należy tooupload hello `.cer` pliku tooAzure za pomocą akcji "Przekaż" hello karty "Ustawienia" hello hello [klasycznego portalu Azure][management-portal].</span><span class="sxs-lookup"><span data-stu-id="02a96-140">After you have created hello certificate, you need tooupload hello `.cer` file tooAzure via hello "Upload" action of hello "Settings" tab of hello [Azure classic portal][management-portal].</span></span>

<span data-ttu-id="02a96-141">Po uzyskaniu identyfikator subskrypcji utworzony certyfikat i przekazać hello `.cer` tooAzure plików, można połączyć punkt końcowy zarządzania platformy Azure toohello przekazując hello identyfikator subskrypcji i lokalizacji hello hello certyfikatu w Twojej **Osobistych** magazyn certyfikatów za**ServiceManagementService** (ponownie, Zastąp *AzureCertificate* o nazwie hello certyfikatu):</span><span class="sxs-lookup"><span data-stu-id="02a96-141">After you have obtained your subscription ID, created a certificate, and uploaded hello `.cer` file tooAzure, you can connect toohello Azure management endpoint by passing hello subscription id and hello location of hello certificate in your **Personal** certificate store too**ServiceManagementService** (again, replace *AzureCertificate* with hello name of your certificate):</span></span>

    from azure import *
    from azure.servicemanagement import *

    subscription_id = '<your_subscription_id>'
    certificate_path = 'CURRENT_USER\\my\\AzureCertificate'

    sms = ServiceManagementService(subscription_id, certificate_path)

<span data-ttu-id="02a96-142">W hello poprzedzających przykład `sms` jest **ServiceManagementService** obiektu.</span><span class="sxs-lookup"><span data-stu-id="02a96-142">In hello preceding example, `sms` is a **ServiceManagementService** object.</span></span> <span data-ttu-id="02a96-143">Witaj **ServiceManagementService** klasy jest toomanage klasy podstawowej używane hello usług platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="02a96-143">hello **ServiceManagementService** class is hello primary class used toomanage Azure services.</span></span>

## <span data-ttu-id="02a96-144"><a name="ListAvailableLocations"></a>Jak: wyświetlić listę dostępnych lokalizacji</span><span class="sxs-lookup"><span data-stu-id="02a96-144"><a name="ListAvailableLocations"> </a>How to: List available locations</span></span>
<span data-ttu-id="02a96-145">toolist hello lokalizacje, które są dostępne do obsługi usługi, użyj hello **listy\_lokalizacje** metody:</span><span class="sxs-lookup"><span data-stu-id="02a96-145">toolist hello locations that are available for hosting services, use hello **list\_locations** method:</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    result = sms.list_locations()
    for location in result:
        print(location.name)

<span data-ttu-id="02a96-146">Podczas tworzenia usługi w chmurze lub Usługa magazynu należy tooprovide prawidłową lokalizację.</span><span class="sxs-lookup"><span data-stu-id="02a96-146">When you create a cloud service or storage service you need tooprovide a valid location.</span></span> <span data-ttu-id="02a96-147">Witaj **listy\_lokalizacje** metoda zawsze zwraca aktualną listę hello aktualnie dostępnych lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="02a96-147">hello **list\_locations** method always returns an up-to-date list of hello currently available locations.</span></span> <span data-ttu-id="02a96-148">Opracowywania tego tekstu hello dostępne lokalizacje to:</span><span class="sxs-lookup"><span data-stu-id="02a96-148">As of this writing, hello available locations are:</span></span>

* <span data-ttu-id="02a96-149">Europa Zachodnia</span><span class="sxs-lookup"><span data-stu-id="02a96-149">West Europe</span></span>
* <span data-ttu-id="02a96-150">Europa Północna</span><span class="sxs-lookup"><span data-stu-id="02a96-150">North Europe</span></span>
* <span data-ttu-id="02a96-151">Azja Południowo-Wschodnia</span><span class="sxs-lookup"><span data-stu-id="02a96-151">Southeast Asia</span></span>
* <span data-ttu-id="02a96-152">Azja Wschodnia</span><span class="sxs-lookup"><span data-stu-id="02a96-152">East Asia</span></span>
* <span data-ttu-id="02a96-153">Środkowe stany USA</span><span class="sxs-lookup"><span data-stu-id="02a96-153">Central US</span></span>
* <span data-ttu-id="02a96-154">Środkowo-północne stany USA</span><span class="sxs-lookup"><span data-stu-id="02a96-154">North Central US</span></span>
* <span data-ttu-id="02a96-155">Południowo-środkowe stany USA</span><span class="sxs-lookup"><span data-stu-id="02a96-155">South Central US</span></span>
* <span data-ttu-id="02a96-156">Zachodnie stany USA</span><span class="sxs-lookup"><span data-stu-id="02a96-156">West US</span></span>
* <span data-ttu-id="02a96-157">Wschodnie stany USA</span><span class="sxs-lookup"><span data-stu-id="02a96-157">East US</span></span>
* <span data-ttu-id="02a96-158">Japonia Wschodnia</span><span class="sxs-lookup"><span data-stu-id="02a96-158">Japan East</span></span>
* <span data-ttu-id="02a96-159">Japonia Zachodnia</span><span class="sxs-lookup"><span data-stu-id="02a96-159">Japan West</span></span>
* <span data-ttu-id="02a96-160">Brazylia Południowa</span><span class="sxs-lookup"><span data-stu-id="02a96-160">Brazil South</span></span>
* <span data-ttu-id="02a96-161">Australia Wschodnia</span><span class="sxs-lookup"><span data-stu-id="02a96-161">Australia East</span></span>
* <span data-ttu-id="02a96-162">Australia Południowo-Wschodnia</span><span class="sxs-lookup"><span data-stu-id="02a96-162">Australia Southeast</span></span>

## <span data-ttu-id="02a96-163"><a name="CreateCloudService"></a>Porady: Tworzenie usługi w chmurze</span><span class="sxs-lookup"><span data-stu-id="02a96-163"><a name="CreateCloudService"> </a>How to: Create a cloud service</span></span>
<span data-ttu-id="02a96-164">Podczas tworzenia aplikacji i uruchom go na platformie Azure, hello kod i konfiguracja łącznie są nazywane Azure [usługi w chmurze] [ cloud service] (nazywane *usługi hostowanej* w wcześniej Zwalnia Azure).</span><span class="sxs-lookup"><span data-stu-id="02a96-164">When you create an application and run it in Azure, hello code and configuration together are called an Azure [cloud service][cloud service] (known as a *hosted service* in earlier Azure releases).</span></span> <span data-ttu-id="02a96-165">Hello **utworzyć\_hostowanej\_usługi** metoda pozwala toocreate nową usługę hostowaną przez podanie nazwy usługi hostowanej (który musi być unikatowa na platformie Azure), etykiety (automatycznie zakodowanego toobase64) Opis i lokalizację.</span><span class="sxs-lookup"><span data-stu-id="02a96-165">hello **create\_hosted\_service** method allows you toocreate a new hosted service by providing a hosted service name (which must be unique in Azure), a label (automatically encoded toobase64), a description, and a location.</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    name = 'myhostedservice'
    label = 'myhostedservice'
    desc = 'my hosted service'
    location = 'West US'

    sms.create_hosted_service(name, label, desc, location)

<span data-ttu-id="02a96-166">Możesz wyświetlić listę wszystkich usług hostowanych hello subskrypcji z hello **listy\_hostowane\_usług** metody:</span><span class="sxs-lookup"><span data-stu-id="02a96-166">You can list all hello hosted services for your subscription with hello **list\_hosted\_services** method:</span></span>

    result = sms.list_hosted_services()

    for hosted_service in result:
        print('Service name: ' + hosted_service.service_name)
        print('Management URL: ' + hosted_service.url)
        print('Location: ' + hosted_service.hosted_service_properties.location)
        print('')

<span data-ttu-id="02a96-167">Jeśli chcesz tooget informacji na temat określonej usługi hostowanej, możesz to zrobić przez przekazanie toohello nazwę usługi hostowanej hello **uzyskać\_hostowane\_usługi\_właściwości** — metoda:</span><span class="sxs-lookup"><span data-stu-id="02a96-167">If you want tooget information about a particular hosted service, you can do so by passing hello hosted service name toohello **get\_hosted\_service\_properties** method:</span></span>

    hosted_service = sms.get_hosted_service_properties('myhostedservice')

    print('Service name: ' + hosted_service.service_name)
    print('Management URL: ' + hosted_service.url)
    print('Location: ' + hosted_service.hosted_service_properties.location)

<span data-ttu-id="02a96-168">Po utworzeniu usługi w chmurze, można wdrożyć usługę toohello kodu przy hello **utworzyć\_wdrożenia** metody.</span><span class="sxs-lookup"><span data-stu-id="02a96-168">After you have created a cloud service, you can deploy your code toohello service with hello **create\_deployment** method.</span></span>

## <span data-ttu-id="02a96-169"><a name="DeleteCloudService"></a>Porady: usuwanie usługi w chmurze</span><span class="sxs-lookup"><span data-stu-id="02a96-169"><a name="DeleteCloudService"> </a>How to: Delete a cloud service</span></span>
<span data-ttu-id="02a96-170">Usługi w chmurze można usunąć przez przekazanie toohello nazwa usługi hello **usunąć\_hostowanej\_usługi** — metoda:</span><span class="sxs-lookup"><span data-stu-id="02a96-170">You can delete a cloud service by passing hello service name toohello **delete\_hosted\_service** method:</span></span>

    sms.delete_hosted_service('myhostedservice')

<span data-ttu-id="02a96-171">Przed usunięciem usługi muszą zostać usunięte wszystkie wdrożenia hello usługi.</span><span class="sxs-lookup"><span data-stu-id="02a96-171">Before you can delete a service, all deployments for hello service must first be deleted.</span></span> <span data-ttu-id="02a96-172">(Zobacz [porady: usuwanie wdrożenia](#DeleteDeployment) Aby uzyskać więcej informacji.)</span><span class="sxs-lookup"><span data-stu-id="02a96-172">(See [How to: Delete a deployment](#DeleteDeployment) for details.)</span></span>

## <span data-ttu-id="02a96-173"><a name="DeleteDeployment"></a>Porady: usuwanie wdrożenia</span><span class="sxs-lookup"><span data-stu-id="02a96-173"><a name="DeleteDeployment"> </a>How to: Delete a deployment</span></span>
<span data-ttu-id="02a96-174">toodelete wdrożenia, użyj hello **usunąć\_wdrożenia** metody.</span><span class="sxs-lookup"><span data-stu-id="02a96-174">toodelete a deployment, use hello **delete\_deployment** method.</span></span> <span data-ttu-id="02a96-175">Witaj poniższy przykład przedstawia sposób toodelete wdrożenia o nazwie `v1`.</span><span class="sxs-lookup"><span data-stu-id="02a96-175">hello following example shows how toodelete a deployment named `v1`.</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    sms.delete_deployment('myhostedservice', 'v1')

## <span data-ttu-id="02a96-176"><a name="CreateStorageService"></a>Porady: Tworzenie usługi magazynu</span><span class="sxs-lookup"><span data-stu-id="02a96-176"><a name="CreateStorageService"> </a>How to: Create a storage service</span></span>
<span data-ttu-id="02a96-177">A [usługi magazynu](../storage/common/storage-create-storage-account.md) zapewnia dostęp tooAzure [obiekty BLOB](../storage/blobs/storage-python-how-to-use-blob-storage.md), [tabel](../cosmos-db/table-storage-how-to-use-python.md), i [kolejek](../storage/queues/storage-python-how-to-use-queue-storage.md).</span><span class="sxs-lookup"><span data-stu-id="02a96-177">A [storage service](../storage/common/storage-create-storage-account.md) gives you access tooAzure [Blobs](../storage/blobs/storage-python-how-to-use-blob-storage.md), [Tables](../cosmos-db/table-storage-how-to-use-python.md), and [Queues](../storage/queues/storage-python-how-to-use-queue-storage.md).</span></span> <span data-ttu-id="02a96-178">toocreate usługi magazynu, należy nazwę usługi hello (od 3 do 24 małych liter i unikatowa na platformie Azure), opis etykiety (w górę too100 znaków, automatycznie zakodowanego toobase64) i lokalizację.</span><span class="sxs-lookup"><span data-stu-id="02a96-178">toocreate a storage service, you need a name for hello service (between 3 and 24 lowercase characters and unique within Azure), a description, a label (up too100 characters, automatically encoded toobase64), and a location.</span></span> <span data-ttu-id="02a96-179">Witaj poniższy przykład pokazuje, jak toocreate magazynu usługi, określając lokalizację.</span><span class="sxs-lookup"><span data-stu-id="02a96-179">hello following example shows how toocreate a storage service by specifying a location.</span></span>

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

<span data-ttu-id="02a96-180">Należy zwrócić uwagę w hello poprzedzających przykładzie stan hello hello **utworzyć\_magazynu\_konta** operacji mogą być pobierane przez przekazanie hello wynik zwracany przez **utworzyć\_magazynu \_konta** toohello **uzyskać\_operacji\_stan** metody.</span><span class="sxs-lookup"><span data-stu-id="02a96-180">Note in hello preceding example that hello status of hello **create\_storage\_account** operation can be retrieved by passing hello result returned by **create\_storage\_account** toohello **get\_operation\_status** method.</span></span>  

<span data-ttu-id="02a96-181">Można wyświetlić listę kont magazynu oraz ich właściwości z hello **listy\_magazynu\_kont** metody:</span><span class="sxs-lookup"><span data-stu-id="02a96-181">You can list your storage accounts and their properties with hello **list\_storage\_accounts** method:</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    result = sms.list_storage_accounts()
    for account in result:
        print('Service name: ' + account.service_name)
        print('Location: ' + account.storage_service_properties.location)
        print('')

## <span data-ttu-id="02a96-182"><a name="DeleteStorageService"></a>Porady: usuwanie usługi magazynu</span><span class="sxs-lookup"><span data-stu-id="02a96-182"><a name="DeleteStorageService"> </a>How to: Delete a storage service</span></span>
<span data-ttu-id="02a96-183">Usługa Magazyn można usunąć przez przekazanie toohello nazwa usługi magazynu hello **usunąć\_magazynu\_konta** metody.</span><span class="sxs-lookup"><span data-stu-id="02a96-183">You can delete a storage service by passing hello storage service name toohello **delete\_storage\_account** method.</span></span> <span data-ttu-id="02a96-184">Usunięcie usługi magazynu powoduje usunięcie wszystkich danych przechowywanych w usłudze hello (obiekty BLOB, tabel i kolejek).</span><span class="sxs-lookup"><span data-stu-id="02a96-184">Deleting a storage service deletes all data stored in hello service (blobs, tables, and queues).</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    sms.delete_storage_account('mystorageaccount')

## <span data-ttu-id="02a96-185"><a name="ListOperatingSystems"></a>Jak: wyświetlić listę dostępnych systemów operacyjnych</span><span class="sxs-lookup"><span data-stu-id="02a96-185"><a name="ListOperatingSystems"> </a>How to: List available operating systems</span></span>
<span data-ttu-id="02a96-186">systemy operacyjne hello toolist, które są dostępne do obsługi usługi, użyj hello **listy\_działających\_systemów** metody:</span><span class="sxs-lookup"><span data-stu-id="02a96-186">toolist hello operating systems that are available for hosting services, use hello **list\_operating\_systems** method:</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    result = sms.list_operating_systems()

    for os in result:
        print('OS: ' + os.label)
        print('Family: ' + os.family_label)
        print('Active: ' + str(os.is_active))

<span data-ttu-id="02a96-187">Alternatywnie można użyć hello **listy\_operacyjnego\_systemu\_rodzin** metodę, która grup systemów operacyjnych hello rodziny:</span><span class="sxs-lookup"><span data-stu-id="02a96-187">Alternatively, you can use hello **list\_operating\_system\_families** method, which groups hello operating systems by family:</span></span>

    result = sms.list_operating_system_families()

    for family in result:
        print('Family: ' + family.label)
        for os in family.operating_systems:
            if os.is_active:
                print('OS: ' + os.label)
                print('Version: ' + os.version)
        print('')

## <span data-ttu-id="02a96-188"><a name="CreateVMImage"></a>Porady: Tworzenie obrazu systemu operacyjnego</span><span class="sxs-lookup"><span data-stu-id="02a96-188"><a name="CreateVMImage"> </a>How to: Create an operating system image</span></span>
<span data-ttu-id="02a96-189">tooadd systemu operacyjnego obrazu toohello repozytorium obrazów, użyj hello **dodać\_os\_obrazu** metody:</span><span class="sxs-lookup"><span data-stu-id="02a96-189">tooadd an operating system image toohello image repository, use hello **add\_os\_image** method:</span></span>

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

<span data-ttu-id="02a96-190">obrazy systemu operacyjnego hello toolist, które są dostępne, użyj hello **listy\_os\_obrazów** metody.</span><span class="sxs-lookup"><span data-stu-id="02a96-190">toolist hello operating system images that are available, use hello **list\_os\_images** method.</span></span> <span data-ttu-id="02a96-191">Zawiera wszystkie obrazy platformy i obrazów użytkowników:</span><span class="sxs-lookup"><span data-stu-id="02a96-191">It includes all platform images and user images:</span></span>

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

## <span data-ttu-id="02a96-192"><a name="DeleteVMImage"></a>Porady: usuwanie obrazu systemu operacyjnego</span><span class="sxs-lookup"><span data-stu-id="02a96-192"><a name="DeleteVMImage"> </a>How to: Delete an operating system image</span></span>
<span data-ttu-id="02a96-193">toodelete obrazu użytkownika, użyj hello **usunąć\_os\_obrazu** metody:</span><span class="sxs-lookup"><span data-stu-id="02a96-193">toodelete a user image, use hello **delete\_os\_image** method:</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    result = sms.delete_os_image('mycentos')

    operation_result = sms.get_operation_status(result.request_id)
    print('Operation status: ' + operation_result.status)

## <span data-ttu-id="02a96-194"><a name="CreateVM"></a>Porady: tworzenie maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="02a96-194"><a name="CreateVM"> </a>How to: Create a virtual machine</span></span>
<span data-ttu-id="02a96-195">toocreate maszyny wirtualnej, należy najpierw toocreate [usługi w chmurze](#CreateCloudService).</span><span class="sxs-lookup"><span data-stu-id="02a96-195">toocreate a virtual machine, you first need toocreate a [cloud service](#CreateCloudService).</span></span>  <span data-ttu-id="02a96-196">Następnie utwórz hello wdrożenia maszyny wirtualnej przy użyciu hello **utworzyć\_wirtualnego\_maszyny\_wdrożenia** — metoda:</span><span class="sxs-lookup"><span data-stu-id="02a96-196">Then create hello virtual machine deployment using hello **create\_virtual\_machine\_deployment** method:</span></span>

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

## <span data-ttu-id="02a96-197"><a name="DeleteVM"></a>Porady: usuwanie maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="02a96-197"><a name="DeleteVM"> </a>How to: Delete a virtual machine</span></span>
<span data-ttu-id="02a96-198">toodelete maszyny wirtualnej, należy najpierw usunąć hello wdrożenia przy użyciu hello **usunąć\_wdrożenia** metody:</span><span class="sxs-lookup"><span data-stu-id="02a96-198">toodelete a virtual machine, you first delete hello deployment using hello **delete\_deployment** method:</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    sms.delete_deployment(service_name='myvm',
        deployment_name='myvm')

<span data-ttu-id="02a96-199">następnie można usunąć usługi w chmurze Hello przy użyciu hello **usunąć\_hostowanej\_usługi** metody:</span><span class="sxs-lookup"><span data-stu-id="02a96-199">hello cloud service can then be deleted using hello **delete\_hosted\_service** method:</span></span>

    sms.delete_hosted_service(service_name='myvm')

## <a name="how-to-create-a-virtual-machine-from-a-captured-virtual-machine-image"></a><span data-ttu-id="02a96-200">Porady: Tworzenie maszyny wirtualnej z obrazu przechwyconych maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="02a96-200">How To: Create a Virtual Machine from a Captured Virtual Machine Image</span></span>
<span data-ttu-id="02a96-201">toocapture obrazu maszyny Wirtualnej, należy najpierw wywołać hello **przechwytywania\_wirtualna\_obrazu** metody:</span><span class="sxs-lookup"><span data-stu-id="02a96-201">toocapture a VM image, you first call hello **capture\_vm\_image** method:</span></span>

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

<span data-ttu-id="02a96-202">Następnie toomake się, że pomyślnie zostały przechwycony obraz powitania, użyj hello **listy\_wirtualna\_obrazów** interfejsu api i upewnij się, że obraz jest wyświetlana w wynikach hello:</span><span class="sxs-lookup"><span data-stu-id="02a96-202">Next, toomake sure that you have successfully captured hello image, use hello **list\_vm\_images** api, and make sure your image is displayed in hello results:</span></span>

    images = sms.list_vm_images()

<span data-ttu-id="02a96-203">toofinally utworzyć hello maszyny wirtualnej za pomocą przechwycony obraz powitania, użyj hello **utworzyć\_wirtualnego\_maszyny\_wdrożenia** jak wcześniej, ale tym razem przekazywanie hello vm_image_name zamiast niego</span><span class="sxs-lookup"><span data-stu-id="02a96-203">toofinally create hello virtual machine using hello captured image, use hello **create\_virtual\_machine\_deployment** method as before, but this time pass in hello vm_image_name instead</span></span>

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

<span data-ttu-id="02a96-204">więcej informacji o toolearn, toocapture maszyny wirtualnej systemu Linux, zobacz temat [jak tooCapture maszyny wirtualnej systemu Linux.](../virtual-machines/linux/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="02a96-204">toolearn more about how toocapture a Linux Virtual Machine, see [How tooCapture a Linux Virtual Machine.](../virtual-machines/linux/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)</span></span>

<span data-ttu-id="02a96-205">więcej informacji o toolearn, toocapture maszyny wirtualnej systemu Windows, zobacz temat [jak tooCapture maszyny wirtualnej systemu Windows.](../virtual-machines/windows/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="02a96-205">toolearn more about how toocapture a Windows Virtual Machine, see [How tooCapture a Windows Virtual Machine.](../virtual-machines/windows/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span></span>

## <span data-ttu-id="02a96-206"><a name="What's Next"> </a>Następne kroki</span><span class="sxs-lookup"><span data-stu-id="02a96-206"><a name="What's Next"> </a>Next Steps</span></span>
<span data-ttu-id="02a96-207">Teraz, kiedy znasz już podstawy hello zarządzania usługami, można uzyskać dostępu do hello [kompletne API dokumentacji dla hello Azure Python SDK](http://azure-sdk-for-python.readthedocs.org/) i wykonać złożone zadania łatwo toomanage aplikacji python.</span><span class="sxs-lookup"><span data-stu-id="02a96-207">Now that you've learned hello basics of service management, you can access hello [Complete API reference documentation for hello Azure Python SDK](http://azure-sdk-for-python.readthedocs.org/) and perform complex tasks easily toomanage your python application.</span></span>

<span data-ttu-id="02a96-208">Aby uzyskać więcej informacji, zobacz hello [Centrum deweloperów języka Python](/develop/python/).</span><span class="sxs-lookup"><span data-stu-id="02a96-208">For more information, see hello [Python Developer Center](/develop/python/).</span></span>

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
