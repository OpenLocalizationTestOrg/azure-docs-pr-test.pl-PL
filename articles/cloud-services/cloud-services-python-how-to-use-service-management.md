---
title: "Sposób użycia interfejsu API (Python) — Przewodnik po funkcji zarządzania usługami"
description: "Dowiedz się, jak programowo wykonywać typowe zadania zarządzania dla usługi w języku Python."
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
ms.openlocfilehash: 13249ba9a4b317a3154776b411ce0bb1f316b3bb
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-service-management-from-python"></a><span data-ttu-id="86440-103">Jak używać usługi zarządzania w języku Python</span><span class="sxs-lookup"><span data-stu-id="86440-103">How to use Service Management from Python</span></span>
<span data-ttu-id="86440-104">Ten przewodnik przedstawia, jak programowo wykonywać typowe zadania zarządzania dla usługi w języku Python.</span><span class="sxs-lookup"><span data-stu-id="86440-104">This guide shows you how to programmatically perform common service management tasks from Python.</span></span> <span data-ttu-id="86440-105">**ServiceManagementService** klasy w [zestaw Azure SDK for Python](https://github.com/Azure/azure-sdk-for-python) obsługuje dostęp programistyczny umożliwiający wiele usług związanych z zarządzaniem funkcji dostępnych w [klasycznego portalu Azure] [ management-portal] (takich jak **tworzenie, aktualizowanie i usuwanie usługi w chmurze, wdrożeń, dane usługi zarządzania i maszyn wirtualnych**).</span><span class="sxs-lookup"><span data-stu-id="86440-105">The **ServiceManagementService** class in the [Azure SDK for Python](https://github.com/Azure/azure-sdk-for-python) supports programmatic access to much of the service management-related functionality that is available in the [Azure classic portal][management-portal] (such as **creating, updating, and deleting cloud services, deployments, data management services, and virtual machines**).</span></span> <span data-ttu-id="86440-106">Ta funkcja może być przydatne do tworzenia aplikacji, które muszą dostęp programistyczny umożliwiający zarządzanie usługą.</span><span class="sxs-lookup"><span data-stu-id="86440-106">This functionality can be useful in building applications that need programmatic access to service management.</span></span>

## <span data-ttu-id="86440-107"><a name="WhatIs"></a>Co to jest usługa zarządzania</span><span class="sxs-lookup"><span data-stu-id="86440-107"><a name="WhatIs"> </a>What is Service Management</span></span>
<span data-ttu-id="86440-108">Interfejs API zarządzania usługami zapewnia dostęp programistyczny umożliwiający wiele funkcji zarządzania usługi dostępne za pośrednictwem [klasycznego portalu Azure][management-portal].</span><span class="sxs-lookup"><span data-stu-id="86440-108">The Service Management API provides programmatic access to much of the service management functionality available through the [Azure classic portal][management-portal].</span></span> <span data-ttu-id="86440-109">Zestaw Azure SDK for Python umożliwia zarządzanie usługi w chmurze i kont magazynu.</span><span class="sxs-lookup"><span data-stu-id="86440-109">The Azure SDK for Python allows you to manage your cloud services and storage accounts.</span></span>

<span data-ttu-id="86440-110">Aby użyć interfejs API zarządzania usługami, musisz [tworzenia konta platformy Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="86440-110">To use the Service Management API, you need to [create an Azure account](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <span data-ttu-id="86440-111"><a name="Concepts"></a>Pojęcia</span><span class="sxs-lookup"><span data-stu-id="86440-111"><a name="Concepts"> </a>Concepts</span></span>
<span data-ttu-id="86440-112">Zestaw Azure SDK for Python opakowuje [interfejs API zarządzania usługami Azure][svc-mgmt-rest-api], która jest interfejs API REST.</span><span class="sxs-lookup"><span data-stu-id="86440-112">The Azure SDK for Python wraps the [Azure Service Management API][svc-mgmt-rest-api], which is a REST API.</span></span> <span data-ttu-id="86440-113">Wszystkie operacje interfejsu API są realizowane poprzez protokół SSL z wzajemnym uwierzytelnieniem certyfikatami X.509 v3.</span><span class="sxs-lookup"><span data-stu-id="86440-113">All API operations are performed over SSL and mutually authenticated using X.509 v3 certificates.</span></span> <span data-ttu-id="86440-114">Dostęp do usługi zarządzania można uzyskać poprzez usługę uruchomioną w systemie Azure lub bezpośrednio przez Internet z dowolnej aplikacji, która potrafi przesłać żądanie HTTPS i odbierać odpowiedzi HTTPS.</span><span class="sxs-lookup"><span data-stu-id="86440-114">The management service may be accessed from within a service running in Azure, or directly over the Internet from any application that can send an HTTPS request and receive an HTTPS response.</span></span>

## <span data-ttu-id="86440-115"><a name="Installation"></a>Instalacji</span><span class="sxs-lookup"><span data-stu-id="86440-115"><a name="Installation"> </a>Installation</span></span>
<span data-ttu-id="86440-116">Wszystkie funkcje opisane w tym artykule są dostępne w `azure-servicemanagement-legacy` pakiet, który można zainstalować przy użyciu narzędzia pip.</span><span class="sxs-lookup"><span data-stu-id="86440-116">All the features described in this article are available in the `azure-servicemanagement-legacy` package, which you can install using pip.</span></span> <span data-ttu-id="86440-117">Aby uzyskać więcej informacji na temat instalacji (na przykład jeśli jesteś nowym użytkownikiem Python), zobacz ten artykuł: [instalowanie Python i zestawu Azure SDK](../python-how-to-install.md)</span><span class="sxs-lookup"><span data-stu-id="86440-117">For more information about installation (for example, if you are new to Python), see this article: [Installing Python and the Azure SDK](../python-how-to-install.md)</span></span>

## <span data-ttu-id="86440-118"><a name="Connect"></a>Jak: nawiązać połączenia z usługi zarządzania</span><span class="sxs-lookup"><span data-stu-id="86440-118"><a name="Connect"> </a>How to: Connect to service management</span></span>
<span data-ttu-id="86440-119">Aby połączyć się z punktem końcowym usługi zarządzania, należy identyfikator subskrypcji platformy Azure i prawidłowy certyfikat zarządzania.</span><span class="sxs-lookup"><span data-stu-id="86440-119">To connect to the Service Management endpoint, you need your Azure subscription ID and a valid management certificate.</span></span> <span data-ttu-id="86440-120">Możesz uzyskać identyfikator subskrypcji za pośrednictwem [klasycznego portalu Azure][management-portal].</span><span class="sxs-lookup"><span data-stu-id="86440-120">You can obtain your subscription ID through the [Azure classic portal][management-portal].</span></span>

> [!NOTE]
> <span data-ttu-id="86440-121">Obecnie istnieje możliwość używania certyfikatów utworzone za pomocą biblioteki OpenSSL uruchomionej w systemie Windows.</span><span class="sxs-lookup"><span data-stu-id="86440-121">It is now possible to use certificates created with OpenSSL when running on Windows.</span></span>  <span data-ttu-id="86440-122">Wymaga to Python 2.7.4 lub nowszym.</span><span class="sxs-lookup"><span data-stu-id="86440-122">It requires Python 2.7.4 or later.</span></span> <span data-ttu-id="86440-123">Firma Microsoft zaleca użytkownikom używanie biblioteki OpenSSL zamiast PFX, ponieważ obsługa PFX certyfikatów prawdopodobnie zostaną usunięte w przyszłości.</span><span class="sxs-lookup"><span data-stu-id="86440-123">We recommend users to use OpenSSL instead of .pfx, since support for .pfx certificates will likely be removed in the future.</span></span>
>
>

### <a name="management-certificates-on-windowsmaclinux-openssl"></a><span data-ttu-id="86440-124">Certyfikaty zarządzania na systemem Windows lub Mac/Linux (OpenSSL)</span><span class="sxs-lookup"><span data-stu-id="86440-124">Management certificates on Windows/Mac/Linux (OpenSSL)</span></span>
<span data-ttu-id="86440-125">Można użyć [OpenSSL](http://www.openssl.org/) można utworzyć certyfikat zarządzania.</span><span class="sxs-lookup"><span data-stu-id="86440-125">You can use [OpenSSL](http://www.openssl.org/) to create your management certificate.</span></span>  <span data-ttu-id="86440-126">Rzeczywiście, należy utworzyć dwa certyfikaty, jeden dla serwera ( `.cer` plików) i jeden dla klienta ( `.pem` pliku).</span><span class="sxs-lookup"><span data-stu-id="86440-126">You actually need to create two certificates, one for the server (a `.cer` file) and one for the client (a `.pem` file).</span></span> <span data-ttu-id="86440-127">Aby utworzyć `.pem` plików, należy wykonać:</span><span class="sxs-lookup"><span data-stu-id="86440-127">To create the `.pem` file, execute:</span></span>

    openssl req -x509 -nodes -days 365 -newkey rsa:1024 -keyout mycert.pem -out mycert.pem

<span data-ttu-id="86440-128">Aby utworzyć `.cer` certyfikatów, należy wykonać:</span><span class="sxs-lookup"><span data-stu-id="86440-128">To create the `.cer` certificate, execute:</span></span>

    openssl x509 -inform pem -in mycert.pem -outform der -out mycert.cer

<span data-ttu-id="86440-129">Aby uzyskać więcej informacji o certyfikatach Azure, zobacz [Omówienie certyfikatów dla usług w chmurze Azure](cloud-services-certs-create.md).</span><span class="sxs-lookup"><span data-stu-id="86440-129">For more information about Azure certificates, see [Certificates Overview for Azure Cloud Services](cloud-services-certs-create.md).</span></span> <span data-ttu-id="86440-130">Pełny opis parametrów biblioteki OpenSSL, zobacz dokumentację w [http://www.openssl.org/docs/apps/openssl.html](http://www.openssl.org/docs/apps/openssl.html).</span><span class="sxs-lookup"><span data-stu-id="86440-130">For a complete description of OpenSSL parameters, see the documentation at [http://www.openssl.org/docs/apps/openssl.html](http://www.openssl.org/docs/apps/openssl.html).</span></span>

<span data-ttu-id="86440-131">Po utworzeniu tych plików, należy przekazać `.cer` plików na platformie Azure przy użyciu akcji "Przekazywanie" kartę "Ustawienia" [klasycznego portalu Azure][management-portal], i zwróć uwagę na którym zapisano `.pem` pliku.</span><span class="sxs-lookup"><span data-stu-id="86440-131">After you have created these files, you need to upload the `.cer` file to Azure via the "Upload" action of the "Settings" tab of the [Azure classic portal][management-portal], and you need to make note of where you saved the `.pem` file.</span></span>

<span data-ttu-id="86440-132">Po uzyskaniu identyfikator subskrypcji utworzony certyfikat i przekazać `.cer` plików na platformie Azure, można połączyć z punktem końcowym zarządzania platformy Azure przy przekazywanie identyfikator subskrypcji i ścieżkę do `.pem` pliku **ServiceManagementService**:</span><span class="sxs-lookup"><span data-stu-id="86440-132">After you have obtained your subscription ID, created a certificate, and uploaded the `.cer` file to Azure, you can connect to the Azure management endpoint by passing the subscription id and the path to the `.pem` file to **ServiceManagementService**:</span></span>

    from azure import *
    from azure.servicemanagement import *

    subscription_id = '<your_subscription_id>'
    certificate_path = '<path_to_.pem_certificate>'

    sms = ServiceManagementService(subscription_id, certificate_path)

<span data-ttu-id="86440-133">W powyższym przykładzie `sms` jest **ServiceManagementService** obiektu.</span><span class="sxs-lookup"><span data-stu-id="86440-133">In the preceding example, `sms` is a **ServiceManagementService** object.</span></span> <span data-ttu-id="86440-134">**ServiceManagementService** klasa jest klasą podstawowy używany do zarządzania usługami Azure.</span><span class="sxs-lookup"><span data-stu-id="86440-134">The **ServiceManagementService** class is the primary class used to manage Azure services.</span></span>

### <a name="management-certificates-on-windows-makecert"></a><span data-ttu-id="86440-135">Certyfikaty zarządzania w systemie Windows (MakeCert)</span><span class="sxs-lookup"><span data-stu-id="86440-135">Management certificates on Windows (MakeCert)</span></span>
<span data-ttu-id="86440-136">Można utworzyć certyfikat zarządzania z podpisem własnym na przy użyciu maszyny `makecert.exe`.</span><span class="sxs-lookup"><span data-stu-id="86440-136">You can create a self-signed management certificate on your machine using `makecert.exe`.</span></span>  <span data-ttu-id="86440-137">Otwórz **wiersz polecenia programu Visual Studio** jako **administratora** i należy użyć następującego polecenia, zastępując *AzureCertificate* o nazwie certyfikat, chcesz użyć.</span><span class="sxs-lookup"><span data-stu-id="86440-137">Open a **Visual Studio command prompt** as an **administrator** and use the following command, replacing *AzureCertificate* with the certificate name you would like to use.</span></span>

    makecert -sky exchange -r -n "CN=AzureCertificate" -pe -a sha1 -len 2048 -ss My "AzureCertificate.cer"

<span data-ttu-id="86440-138">Polecenie tworzy `.cer` pliku i instaluje je w **osobistych** magazynu certyfikatów.</span><span class="sxs-lookup"><span data-stu-id="86440-138">The command creates the `.cer` file, and installs it in the **Personal** certificate store.</span></span> <span data-ttu-id="86440-139">Aby uzyskać więcej informacji, zobacz [Omówienie certyfikatów dla usług w chmurze Azure](cloud-services-certs-create.md).</span><span class="sxs-lookup"><span data-stu-id="86440-139">For more information, see [Certificates Overview for Azure Cloud Services](cloud-services-certs-create.md).</span></span>

<span data-ttu-id="86440-140">Po utworzeniu certyfikatu należy przekazać `.cer` plików na platformie Azure przy użyciu akcji "Przekazywanie" kartę "Ustawienia" [klasycznego portalu Azure][management-portal].</span><span class="sxs-lookup"><span data-stu-id="86440-140">After you have created the certificate, you need to upload the `.cer` file to Azure via the "Upload" action of the "Settings" tab of the [Azure classic portal][management-portal].</span></span>

<span data-ttu-id="86440-141">Po uzyskaniu identyfikator subskrypcji utworzony certyfikat i przekazać `.cer` plików na platformie Azure, można połączyć z punktem końcowym zarządzania platformy Azure przy przekazywanie identyfikator subskrypcji i lokalizacji certyfikatu w Twojej **osobistych** magazyn certyfikatów **ServiceManagementService** (ponownie, Zastąp *AzureCertificate* o nazwie certyfikatu):</span><span class="sxs-lookup"><span data-stu-id="86440-141">After you have obtained your subscription ID, created a certificate, and uploaded the `.cer` file to Azure, you can connect to the Azure management endpoint by passing the subscription id and the location of the certificate in your **Personal** certificate store to **ServiceManagementService** (again, replace *AzureCertificate* with the name of your certificate):</span></span>

    from azure import *
    from azure.servicemanagement import *

    subscription_id = '<your_subscription_id>'
    certificate_path = 'CURRENT_USER\\my\\AzureCertificate'

    sms = ServiceManagementService(subscription_id, certificate_path)

<span data-ttu-id="86440-142">W powyższym przykładzie `sms` jest **ServiceManagementService** obiektu.</span><span class="sxs-lookup"><span data-stu-id="86440-142">In the preceding example, `sms` is a **ServiceManagementService** object.</span></span> <span data-ttu-id="86440-143">**ServiceManagementService** klasa jest klasą podstawowy używany do zarządzania usługami Azure.</span><span class="sxs-lookup"><span data-stu-id="86440-143">The **ServiceManagementService** class is the primary class used to manage Azure services.</span></span>

## <span data-ttu-id="86440-144"><a name="ListAvailableLocations"></a>Jak: wyświetlić listę dostępnych lokalizacji</span><span class="sxs-lookup"><span data-stu-id="86440-144"><a name="ListAvailableLocations"> </a>How to: List available locations</span></span>
<span data-ttu-id="86440-145">Aby wyświetlić lokalizacje, które są dostępne dla usług hostingu, użyj **listy\_lokalizacje** metody:</span><span class="sxs-lookup"><span data-stu-id="86440-145">To list the locations that are available for hosting services, use the **list\_locations** method:</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    result = sms.list_locations()
    for location in result:
        print(location.name)

<span data-ttu-id="86440-146">Podczas tworzenia usługi w chmurze lub Usługa magazynu, musisz podać prawidłową lokalizację.</span><span class="sxs-lookup"><span data-stu-id="86440-146">When you create a cloud service or storage service you need to provide a valid location.</span></span> <span data-ttu-id="86440-147">**Listy\_lokalizacje** metoda zawsze zwraca aktualną listę dostępnych lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="86440-147">The **list\_locations** method always returns an up-to-date list of the currently available locations.</span></span> <span data-ttu-id="86440-148">Opracowywania tego tekstu, są dostępne lokalizacje:</span><span class="sxs-lookup"><span data-stu-id="86440-148">As of this writing, the available locations are:</span></span>

* <span data-ttu-id="86440-149">Europa Zachodnia</span><span class="sxs-lookup"><span data-stu-id="86440-149">West Europe</span></span>
* <span data-ttu-id="86440-150">Europa Północna</span><span class="sxs-lookup"><span data-stu-id="86440-150">North Europe</span></span>
* <span data-ttu-id="86440-151">Azja Południowo-Wschodnia</span><span class="sxs-lookup"><span data-stu-id="86440-151">Southeast Asia</span></span>
* <span data-ttu-id="86440-152">Azja Wschodnia</span><span class="sxs-lookup"><span data-stu-id="86440-152">East Asia</span></span>
* <span data-ttu-id="86440-153">Środkowe stany USA</span><span class="sxs-lookup"><span data-stu-id="86440-153">Central US</span></span>
* <span data-ttu-id="86440-154">Środkowo-północne stany USA</span><span class="sxs-lookup"><span data-stu-id="86440-154">North Central US</span></span>
* <span data-ttu-id="86440-155">Południowo-środkowe stany USA</span><span class="sxs-lookup"><span data-stu-id="86440-155">South Central US</span></span>
* <span data-ttu-id="86440-156">Zachodnie stany USA</span><span class="sxs-lookup"><span data-stu-id="86440-156">West US</span></span>
* <span data-ttu-id="86440-157">Wschodnie stany USA</span><span class="sxs-lookup"><span data-stu-id="86440-157">East US</span></span>
* <span data-ttu-id="86440-158">Japonia Wschodnia</span><span class="sxs-lookup"><span data-stu-id="86440-158">Japan East</span></span>
* <span data-ttu-id="86440-159">Japonia Zachodnia</span><span class="sxs-lookup"><span data-stu-id="86440-159">Japan West</span></span>
* <span data-ttu-id="86440-160">Brazylia Południowa</span><span class="sxs-lookup"><span data-stu-id="86440-160">Brazil South</span></span>
* <span data-ttu-id="86440-161">Australia Wschodnia</span><span class="sxs-lookup"><span data-stu-id="86440-161">Australia East</span></span>
* <span data-ttu-id="86440-162">Australia Południowo-Wschodnia</span><span class="sxs-lookup"><span data-stu-id="86440-162">Australia Southeast</span></span>

## <span data-ttu-id="86440-163"><a name="CreateCloudService"></a>Porady: Tworzenie usługi w chmurze</span><span class="sxs-lookup"><span data-stu-id="86440-163"><a name="CreateCloudService"> </a>How to: Create a cloud service</span></span>
<span data-ttu-id="86440-164">Podczas tworzenia aplikacji i uruchom go na platformie Azure, kod i konfiguracja łącznie są nazywane Azure [usługi w chmurze] [ cloud service] (nazywane *usługi hostowanej* we wcześniejszych wersjach platformy Azure).</span><span class="sxs-lookup"><span data-stu-id="86440-164">When you create an application and run it in Azure, the code and configuration together are called an Azure [cloud service][cloud service] (known as a *hosted service* in earlier Azure releases).</span></span> <span data-ttu-id="86440-165">**Utworzyć\_hostowane\_usługi** metoda pozwala utworzyć nową usługę hostowaną, podając nazwę usługi hostowanej (który musi być unikatowa na platformie Azure), etykiety (automatycznie zakodowane w formacie base64), opis oraz lokalizację.</span><span class="sxs-lookup"><span data-stu-id="86440-165">The **create\_hosted\_service** method allows you to create a new hosted service by providing a hosted service name (which must be unique in Azure), a label (automatically encoded to base64), a description, and a location.</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    name = 'myhostedservice'
    label = 'myhostedservice'
    desc = 'my hosted service'
    location = 'West US'

    sms.create_hosted_service(name, label, desc, location)

<span data-ttu-id="86440-166">Można wyświetlić listę wszystkich usług hostowanych dla Twojej subskrypcji z **listy\_hostowanej\_usług** metody:</span><span class="sxs-lookup"><span data-stu-id="86440-166">You can list all the hosted services for your subscription with the **list\_hosted\_services** method:</span></span>

    result = sms.list_hosted_services()

    for hosted_service in result:
        print('Service name: ' + hosted_service.service_name)
        print('Management URL: ' + hosted_service.url)
        print('Location: ' + hosted_service.hosted_service_properties.location)
        print('')

<span data-ttu-id="86440-167">Jeśli chcesz uzyskać informacje o określonej usługi hostowanej, możesz to zrobić przez przekazanie nazwa usługi hostowanej **uzyskać\_hostowanej\_usługi\_właściwości** metody:</span><span class="sxs-lookup"><span data-stu-id="86440-167">If you want to get information about a particular hosted service, you can do so by passing the hosted service name to the **get\_hosted\_service\_properties** method:</span></span>

    hosted_service = sms.get_hosted_service_properties('myhostedservice')

    print('Service name: ' + hosted_service.service_name)
    print('Management URL: ' + hosted_service.url)
    print('Location: ' + hosted_service.hosted_service_properties.location)

<span data-ttu-id="86440-168">Po utworzeniu usługi w chmurze, można wdrożyć kodu do usługi z **utworzyć\_wdrożenia** metody.</span><span class="sxs-lookup"><span data-stu-id="86440-168">After you have created a cloud service, you can deploy your code to the service with the **create\_deployment** method.</span></span>

## <span data-ttu-id="86440-169"><a name="DeleteCloudService"></a>Porady: usuwanie usługi w chmurze</span><span class="sxs-lookup"><span data-stu-id="86440-169"><a name="DeleteCloudService"> </a>How to: Delete a cloud service</span></span>
<span data-ttu-id="86440-170">Można usunąć usługi w chmurze, przekazując nazwy usługi na **usunąć\_hostowane\_usługi** metody:</span><span class="sxs-lookup"><span data-stu-id="86440-170">You can delete a cloud service by passing the service name to the **delete\_hosted\_service** method:</span></span>

    sms.delete_hosted_service('myhostedservice')

<span data-ttu-id="86440-171">Przed usunięciem usługi należy najpierw usunąć wszystkie wdrożenia dla usługi.</span><span class="sxs-lookup"><span data-stu-id="86440-171">Before you can delete a service, all deployments for the service must first be deleted.</span></span> <span data-ttu-id="86440-172">(Zobacz [porady: usuwanie wdrożenia](#DeleteDeployment) Aby uzyskać więcej informacji.)</span><span class="sxs-lookup"><span data-stu-id="86440-172">(See [How to: Delete a deployment](#DeleteDeployment) for details.)</span></span>

## <span data-ttu-id="86440-173"><a name="DeleteDeployment"></a>Porady: usuwanie wdrożenia</span><span class="sxs-lookup"><span data-stu-id="86440-173"><a name="DeleteDeployment"> </a>How to: Delete a deployment</span></span>
<span data-ttu-id="86440-174">Aby usunąć wdrożenia, użyj **usunąć\_wdrożenia** metody.</span><span class="sxs-lookup"><span data-stu-id="86440-174">To delete a deployment, use the **delete\_deployment** method.</span></span> <span data-ttu-id="86440-175">Poniższy przykład pokazuje, jak usunąć wdrożenie o nazwie `v1`.</span><span class="sxs-lookup"><span data-stu-id="86440-175">The following example shows how to delete a deployment named `v1`.</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    sms.delete_deployment('myhostedservice', 'v1')

## <span data-ttu-id="86440-176"><a name="CreateStorageService"></a>Porady: Tworzenie usługi magazynu</span><span class="sxs-lookup"><span data-stu-id="86440-176"><a name="CreateStorageService"> </a>How to: Create a storage service</span></span>
<span data-ttu-id="86440-177">A [usługi magazynu](../storage/common/storage-create-storage-account.md) zapewnia dostęp do usługi Azure [obiekty BLOB](../storage/blobs/storage-python-how-to-use-blob-storage.md), [tabel](../cosmos-db/table-storage-how-to-use-python.md), i [kolejek](../storage/queues/storage-python-how-to-use-queue-storage.md).</span><span class="sxs-lookup"><span data-stu-id="86440-177">A [storage service](../storage/common/storage-create-storage-account.md) gives you access to Azure [Blobs](../storage/blobs/storage-python-how-to-use-blob-storage.md), [Tables](../cosmos-db/table-storage-how-to-use-python.md), and [Queues](../storage/queues/storage-python-how-to-use-queue-storage.md).</span></span> <span data-ttu-id="86440-178">Aby utworzyć usługę magazynu, należy nazwę usługi (od 3 do 24 małych liter i unikatowa na platformie Azure), opis, etykiety (maksymalnie 100 znaków, automatycznie zakodowane w formacie base64) i lokalizację.</span><span class="sxs-lookup"><span data-stu-id="86440-178">To create a storage service, you need a name for the service (between 3 and 24 lowercase characters and unique within Azure), a description, a label (up to 100 characters, automatically encoded to base64), and a location.</span></span> <span data-ttu-id="86440-179">Poniższy przykład przedstawia sposób tworzenia usługi magazynu, określając lokalizację.</span><span class="sxs-lookup"><span data-stu-id="86440-179">The following example shows how to create a storage service by specifying a location.</span></span>

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

<span data-ttu-id="86440-180">Uwaga w poprzednim przykładzie który stan **utworzyć\_magazynu\_konta** operacji mogą być pobierane przez przekazanie wynik zwracany przez **utworzyć\_magazynu\_konta** do **uzyskać\_operacji\_stan** — metoda.</span><span class="sxs-lookup"><span data-stu-id="86440-180">Note in the preceding example that the status of the **create\_storage\_account** operation can be retrieved by passing the result returned by **create\_storage\_account** to the **get\_operation\_status** method.</span></span>  

<span data-ttu-id="86440-181">Można wyświetlić listę kont magazynu oraz ich właściwości z **listy\_magazynu\_kont** metody:</span><span class="sxs-lookup"><span data-stu-id="86440-181">You can list your storage accounts and their properties with the **list\_storage\_accounts** method:</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    result = sms.list_storage_accounts()
    for account in result:
        print('Service name: ' + account.service_name)
        print('Location: ' + account.storage_service_properties.location)
        print('')

## <span data-ttu-id="86440-182"><a name="DeleteStorageService"></a>Porady: usuwanie usługi magazynu</span><span class="sxs-lookup"><span data-stu-id="86440-182"><a name="DeleteStorageService"> </a>How to: Delete a storage service</span></span>
<span data-ttu-id="86440-183">Usługa magazynu można usunąć, przekazując nazwy usługi magazynu do **usunąć\_magazynu\_konta** metody.</span><span class="sxs-lookup"><span data-stu-id="86440-183">You can delete a storage service by passing the storage service name to the **delete\_storage\_account** method.</span></span> <span data-ttu-id="86440-184">Usunięcie usługi magazynu powoduje usunięcie wszystkich danych przechowywanych w usłudze (obiekty BLOB, tabel i kolejek).</span><span class="sxs-lookup"><span data-stu-id="86440-184">Deleting a storage service deletes all data stored in the service (blobs, tables, and queues).</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    sms.delete_storage_account('mystorageaccount')

## <span data-ttu-id="86440-185"><a name="ListOperatingSystems"></a>Jak: wyświetlić listę dostępnych systemów operacyjnych</span><span class="sxs-lookup"><span data-stu-id="86440-185"><a name="ListOperatingSystems"> </a>How to: List available operating systems</span></span>
<span data-ttu-id="86440-186">Aby wyświetlić listę systemów operacyjnych, które są dostępne dla usług hostingu, użyj **listy\_operacyjnego\_systemów** metody:</span><span class="sxs-lookup"><span data-stu-id="86440-186">To list the operating systems that are available for hosting services, use the **list\_operating\_systems** method:</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    result = sms.list_operating_systems()

    for os in result:
        print('OS: ' + os.label)
        print('Family: ' + os.family_label)
        print('Active: ' + str(os.is_active))

<span data-ttu-id="86440-187">Alternatywnie można użyć **listy\_operacyjnego\_systemu\_rodzin** metodę, która grupuje rodziny systemów operacyjnych:</span><span class="sxs-lookup"><span data-stu-id="86440-187">Alternatively, you can use the **list\_operating\_system\_families** method, which groups the operating systems by family:</span></span>

    result = sms.list_operating_system_families()

    for family in result:
        print('Family: ' + family.label)
        for os in family.operating_systems:
            if os.is_active:
                print('OS: ' + os.label)
                print('Version: ' + os.version)
        print('')

## <span data-ttu-id="86440-188"><a name="CreateVMImage"></a>Porady: Tworzenie obrazu systemu operacyjnego</span><span class="sxs-lookup"><span data-stu-id="86440-188"><a name="CreateVMImage"> </a>How to: Create an operating system image</span></span>
<span data-ttu-id="86440-189">Aby dodać obraz systemu operacyjnego do repozytorium obrazów, użyj **dodać\_os\_obrazu** metody:</span><span class="sxs-lookup"><span data-stu-id="86440-189">To add an operating system image to the image repository, use the **add\_os\_image** method:</span></span>

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

<span data-ttu-id="86440-190">Aby wyświetlić listę dostępnych obrazów systemu operacyjnego, należy użyć **listy\_os\_obrazów** metody.</span><span class="sxs-lookup"><span data-stu-id="86440-190">To list the operating system images that are available, use the **list\_os\_images** method.</span></span> <span data-ttu-id="86440-191">Zawiera wszystkie obrazy platformy i obrazów użytkowników:</span><span class="sxs-lookup"><span data-stu-id="86440-191">It includes all platform images and user images:</span></span>

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

## <span data-ttu-id="86440-192"><a name="DeleteVMImage"></a>Porady: usuwanie obrazu systemu operacyjnego</span><span class="sxs-lookup"><span data-stu-id="86440-192"><a name="DeleteVMImage"> </a>How to: Delete an operating system image</span></span>
<span data-ttu-id="86440-193">Aby usunąć obrazu użytkownika, użyj **usunąć\_systemu operacyjnego\_obrazu** metody:</span><span class="sxs-lookup"><span data-stu-id="86440-193">To delete a user image, use the **delete\_os\_image** method:</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    result = sms.delete_os_image('mycentos')

    operation_result = sms.get_operation_status(result.request_id)
    print('Operation status: ' + operation_result.status)

## <span data-ttu-id="86440-194"><a name="CreateVM"></a>Porady: tworzenie maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="86440-194"><a name="CreateVM"> </a>How to: Create a virtual machine</span></span>
<span data-ttu-id="86440-195">Aby utworzyć maszynę wirtualną, należy najpierw utworzyć [usługi w chmurze](#CreateCloudService).</span><span class="sxs-lookup"><span data-stu-id="86440-195">To create a virtual machine, you first need to create a [cloud service](#CreateCloudService).</span></span>  <span data-ttu-id="86440-196">Następnie utworzyć przy użyciu wdrożenia maszyny wirtualnej **utworzyć\_wirtualnego\_maszyny\_wdrożenia** metody:</span><span class="sxs-lookup"><span data-stu-id="86440-196">Then create the virtual machine deployment using the **create\_virtual\_machine\_deployment** method:</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    name = 'myvm'
    location = 'West US'

    #Set the location
    sms.create_hosted_service(service_name=name,
        label=name,
        location=location)

    # Name of an os image as returned by list_os_images
    image_name = 'OpenLogic__OpenLogic-CentOS-62-20120531-en-us-30GB.vhd'

    # Destination storage account container/blob where the VM disk
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

## <span data-ttu-id="86440-197"><a name="DeleteVM"></a>Porady: usuwanie maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="86440-197"><a name="DeleteVM"> </a>How to: Delete a virtual machine</span></span>
<span data-ttu-id="86440-198">Aby usunąć maszynę wirtualną, należy najpierw usunąć wdrożenia przy użyciu **usunąć\_wdrożenia** metody:</span><span class="sxs-lookup"><span data-stu-id="86440-198">To delete a virtual machine, you first delete the deployment using the **delete\_deployment** method:</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    sms.delete_deployment(service_name='myvm',
        deployment_name='myvm')

<span data-ttu-id="86440-199">Następnie można usunąć usługi w chmurze przy użyciu **usunąć\_hostowane\_usługi** metody:</span><span class="sxs-lookup"><span data-stu-id="86440-199">The cloud service can then be deleted using the **delete\_hosted\_service** method:</span></span>

    sms.delete_hosted_service(service_name='myvm')

## <a name="how-to-create-a-virtual-machine-from-a-captured-virtual-machine-image"></a><span data-ttu-id="86440-200">Porady: Tworzenie maszyny wirtualnej z obrazu przechwyconych maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="86440-200">How To: Create a Virtual Machine from a Captured Virtual Machine Image</span></span>
<span data-ttu-id="86440-201">Aby przechwycić obraz maszyny Wirtualnej, należy najpierw wywołać **przechwytywania\_wirtualna\_obrazu** metody:</span><span class="sxs-lookup"><span data-stu-id="86440-201">To capture a VM image, you first call the **capture\_vm\_image** method:</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    # replace the below three parameters with actual values
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

<span data-ttu-id="86440-202">Następnie, aby upewnić się, że pomyślnie przechwyceniu obrazu, należy użyć **listy\_wirtualna\_obrazów** interfejsu api i upewnij się, że obraz jest wyświetlana w wynikach:</span><span class="sxs-lookup"><span data-stu-id="86440-202">Next, to make sure that you have successfully captured the image, use the **list\_vm\_images** api, and make sure your image is displayed in the results:</span></span>

    images = sms.list_vm_images()

<span data-ttu-id="86440-203">Aby na koniec utwórz maszynę wirtualną przy użyciu przechwyconego obrazu, należy użyć **utworzyć\_wirtualnego\_maszyny\_wdrożenia** jak wcześniej, ale tym razem przekazywanie vm_image_name zamiast tego</span><span class="sxs-lookup"><span data-stu-id="86440-203">To finally create the virtual machine using the captured image, use the **create\_virtual\_machine\_deployment** method as before, but this time pass in the vm_image_name instead</span></span>

    from azure import *
    from azure.servicemanagement import *

    sms = ServiceManagementService(subscription_id, certificate_path)

    name = 'myvm'
    location = 'West US'

    #Set the location
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

<span data-ttu-id="86440-204">Aby dowiedzieć się więcej o sposobie przechwytywania maszyny wirtualnej systemu Linux, zobacz [Przechwytywanie maszyny wirtualnej systemu Linux.](../virtual-machines/linux/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="86440-204">To learn more about how to capture a Linux Virtual Machine, see [How to Capture a Linux Virtual Machine.](../virtual-machines/linux/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)</span></span>

<span data-ttu-id="86440-205">Aby dowiedzieć się więcej o sposobie przechwytywania maszyny wirtualnej systemu Windows, temacie [jak przechwycić maszynę wirtualną systemu Windows.](../virtual-machines/windows/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="86440-205">To learn more about how to capture a Windows Virtual Machine, see [How to Capture a Windows Virtual Machine.](../virtual-machines/windows/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)</span></span>

## <span data-ttu-id="86440-206"><a name="What's Next"> </a>Następne kroki</span><span class="sxs-lookup"><span data-stu-id="86440-206"><a name="What's Next"> </a>Next Steps</span></span>
<span data-ttu-id="86440-207">Teraz, kiedy znasz już podstawy usługi zarządzania, należy uzyskać dostęp [kompletne API dokumentacji dla zestawu Azure SDK Python](http://azure-sdk-for-python.readthedocs.org/) i wykonać złożone zadania łatwe do zarządzania aplikacją python.</span><span class="sxs-lookup"><span data-stu-id="86440-207">Now that you've learned the basics of service management, you can access the [Complete API reference documentation for the Azure Python SDK](http://azure-sdk-for-python.readthedocs.org/) and perform complex tasks easily to manage your python application.</span></span>

<span data-ttu-id="86440-208">Więcej informacji możesz znaleźć w [Centrum deweloperów języka Python](/develop/python/).</span><span class="sxs-lookup"><span data-stu-id="86440-208">For more information, see the [Python Developer Center](/develop/python/).</span></span>

[What is Service Management]: #WhatIs
[Concepts]: #Concepts
[How to: Connect to service management]: #Connect
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
