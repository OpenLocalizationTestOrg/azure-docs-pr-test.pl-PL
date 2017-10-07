---
title: "aaaAzure wystąpienia metadane usługi dla systemu Windows | Dokumentacja firmy Microsoft"
description: "Interfejs rESTful tooget informacje o obliczeniowych, sieci i zdarzeń planowanych konserwacji systemu Windows maszyny Wirtualnej."
services: virtual-machines-windows
documentationcenter: 
author: harijay
manager: timlt
editor: 
tags: azure-resource-manager
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 08/11/2017
ms.author: harijay
ms.openlocfilehash: a33c26b5e9ed650be639598cdb6895fc19ccb605
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-instance-metadata-service-for-windows-vms"></a><span data-ttu-id="f2085-103">Usługa Azure wystąpienie metadanych dla maszyn wirtualnych systemu Windows</span><span class="sxs-lookup"><span data-stu-id="f2085-103">Azure Instance Metadata service for Windows VMs</span></span>


<span data-ttu-id="f2085-104">Hello Azure wystąpienie metadanych usługi dostarcza informacji o uruchomionych wystąpień maszyn wirtualnych, które można toomanage używane i skonfigurować maszyny wirtualne.</span><span class="sxs-lookup"><span data-stu-id="f2085-104">hello Azure Instance Metadata Service provides information about running virtual machine instances that can be used toomanage and configure your virtual machines.</span></span>
<span data-ttu-id="f2085-105">Dotyczy to również informacje, takie jak jednostka SKU, konfiguracji sieci i zdarzeń planowanych konserwacji.</span><span class="sxs-lookup"><span data-stu-id="f2085-105">This includes information such as SKU, network configuration, and upcoming maintenance events.</span></span> <span data-ttu-id="f2085-106">Aby uzyskać więcej informacji na jakie rodzaje informacji jest dostępnych w temacie [kategorie metadanych](#instance-metadata-data-categories).</span><span class="sxs-lookup"><span data-stu-id="f2085-106">For more information on what type of information is available, see [metadata categories](#instance-metadata-data-categories).</span></span>

<span data-ttu-id="f2085-107">Usługa metadanych wystąpienia platformy Azure jest punkt końcowy REST tooall dostępne maszyny wirtualne IaaS utworzony za pośrednictwem hello [usługi Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/).</span><span class="sxs-lookup"><span data-stu-id="f2085-107">Azure's Instance Metadata Service is a REST Endpoint accessible tooall IaaS VMs created via hello [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/).</span></span> <span data-ttu-id="f2085-108">punkt końcowy Hello jest dostępny w dobrze znanego adresu IP bez obsługi routingu (`169.254.169.254`) który jest możliwy tylko z wewnątrz hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="f2085-108">hello endpoint is available at a well-known non-routable IP address (`169.254.169.254`) that can be accessed only from within hello VM.</span></span>



> [!IMPORTANT]
> <span data-ttu-id="f2085-109">Ta usługa jest **ogólnie dostępna** w globalnej regiony platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="f2085-109">This service is  **generally available** in Global Azure Regions.</span></span> <span data-ttu-id="f2085-110">Znajduje się w publicznej wersji zapoznawczej dla instytucji rządowych, Chin i chmury Azure niemiecki.</span><span class="sxs-lookup"><span data-stu-id="f2085-110">It is in Public preview for Government, China, and German Azure Cloud.</span></span> <span data-ttu-id="f2085-111">Regularnie odbiera aktualizacje tooexpose nowe informacje o wystąpieniu maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="f2085-111">It regularly receives updates tooexpose new information about virtual machine instances.</span></span> <span data-ttu-id="f2085-112">Ta strona odzwierciedla hello aktualne [kategorii danych](#instance-metadata-data-categories) dostępne.</span><span class="sxs-lookup"><span data-stu-id="f2085-112">This page reflects hello up-to-date [data categories](#instance-metadata-data-categories) available.</span></span>



## <a name="service-availability"></a><span data-ttu-id="f2085-113">Dostępność usługi</span><span class="sxs-lookup"><span data-stu-id="f2085-113">Service Availability</span></span>
<span data-ttu-id="f2085-114">Usługa Hello jest dostępna we wszystkich regionach globalne Azure ogólnie dostępna.</span><span class="sxs-lookup"><span data-stu-id="f2085-114">hello service is available in all generally available Global Azure regions.</span></span> <span data-ttu-id="f2085-115">Usługa Hello znajduje się w publicznej wersji zapoznawczej w regionach dla instytucji rządowych, Chiny lub Niemcy hello.</span><span class="sxs-lookup"><span data-stu-id="f2085-115">hello service is in public preview  in hello Government, China, or Germany regions.</span></span>

<span data-ttu-id="f2085-116">Regiony</span><span class="sxs-lookup"><span data-stu-id="f2085-116">Regions</span></span>                                        | <span data-ttu-id="f2085-117">Dostępność?</span><span class="sxs-lookup"><span data-stu-id="f2085-117">Availability?</span></span>
-----------------------------------------------|-----------------------------------------------
[<span data-ttu-id="f2085-118">Wszystkie ogólnie dostępna globalne regiony platformy Azure</span><span class="sxs-lookup"><span data-stu-id="f2085-118">All Generally Available Global Azure Regions</span></span>](https://azure.microsoft.com/regions/)     | <span data-ttu-id="f2085-119">Ogólnie dostępna</span><span class="sxs-lookup"><span data-stu-id="f2085-119">Generally Available</span></span> 
[<span data-ttu-id="f2085-120">Azure dla instytucji rządowych</span><span class="sxs-lookup"><span data-stu-id="f2085-120">Azure Government</span></span>](https://azure.microsoft.com/overview/clouds/government/)              | <span data-ttu-id="f2085-121">W wersji zapoznawczej</span><span class="sxs-lookup"><span data-stu-id="f2085-121">In Preview</span></span> 
[<span data-ttu-id="f2085-122">Chin Azure</span><span class="sxs-lookup"><span data-stu-id="f2085-122">Azure China</span></span>](https://www.azure.cn/)                                                           | <span data-ttu-id="f2085-123">W wersji zapoznawczej</span><span class="sxs-lookup"><span data-stu-id="f2085-123">In Preview</span></span>
[<span data-ttu-id="f2085-124">Niemcy Azure</span><span class="sxs-lookup"><span data-stu-id="f2085-124">Azure Germany</span></span>](https://azure.microsoft.com/overview/clouds/germany/)                    | <span data-ttu-id="f2085-125">W wersji zapoznawczej</span><span class="sxs-lookup"><span data-stu-id="f2085-125">In Preview</span></span>

<span data-ttu-id="f2085-126">Ta tabela jest aktualizowany, gdy usługa hello staje się dostępna w innych chmur Azure.</span><span class="sxs-lookup"><span data-stu-id="f2085-126">This table is updated when hello service becomes available in other Azure clouds.</span></span>

<span data-ttu-id="f2085-127">tootry limit hello wystąpienia usługi metadanych, utwórz maszynę Wirtualną z [usługi Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/) lub hello [portalu Azure](http://portal.azure.com) w hello powyżej regiony i wykonaj hello przykłady poniżej.</span><span class="sxs-lookup"><span data-stu-id="f2085-127">tootry out hello Instance Metadata Service, create a VM from [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/) or hello [Azure portal](http://portal.azure.com) in hello above regions and follow hello examples below.</span></span>

## <a name="usage"></a><span data-ttu-id="f2085-128">Sposób użycia</span><span class="sxs-lookup"><span data-stu-id="f2085-128">Usage</span></span>

### <a name="versioning"></a><span data-ttu-id="f2085-129">Przechowywanie wersji</span><span class="sxs-lookup"><span data-stu-id="f2085-129">Versioning</span></span>
<span data-ttu-id="f2085-130">Witaj wystąpienia usługi metadanych jest kontrolą wersji.</span><span class="sxs-lookup"><span data-stu-id="f2085-130">hello Instance Metadata Service is versioned.</span></span> <span data-ttu-id="f2085-131">Wersje są obowiązkowe i hello bieżąca wersja to `2017-04-02`.</span><span class="sxs-lookup"><span data-stu-id="f2085-131">Versions are mandatory and hello current version is `2017-04-02`.</span></span>

> [!NOTE] 
> <span data-ttu-id="f2085-132">Poprzednie wersje Podgląd zdarzeń zaplanowane {najnowszych} obsługiwana jako wersja interfejsu api hello.</span><span class="sxs-lookup"><span data-stu-id="f2085-132">Previous preview releases of scheduled events supported {latest} as hello api-version.</span></span> <span data-ttu-id="f2085-133">Ten format jest już obsługiwane i zostaną wycofane w przyszłości hello.</span><span class="sxs-lookup"><span data-stu-id="f2085-133">This format is no longer supported and will be deprecated in hello future.</span></span>

<span data-ttu-id="f2085-134">Przy wdrażaniu nowsze wersje, starsze wersje nadal będą dostępne dla zgodności czy skrypty są zależne formatów określonych danych.</span><span class="sxs-lookup"><span data-stu-id="f2085-134">As we add newer versions, older versions can still be accessed for compatibility if your scripts have dependencies on specific data formats.</span></span> <span data-ttu-id="f2085-135">Jednak należy pamiętać, że bieżący version(2017-03-01) podglądu tego hello mogą nie być dostępne po usługi hello jest ogólnie dostępna.</span><span class="sxs-lookup"><span data-stu-id="f2085-135">However, note that hello current preview version(2017-03-01) may not be available once hello service is generally available.</span></span>

### <a name="using-headers"></a><span data-ttu-id="f2085-136">Korzystanie z nagłówków</span><span class="sxs-lookup"><span data-stu-id="f2085-136">Using headers</span></span>
<span data-ttu-id="f2085-137">Zapytania hello wystąpienia usługi metadanych, należy określić nagłówek hello `Metadata: true` tooensure hello żądania nie został przypadkowo przekierowany.</span><span class="sxs-lookup"><span data-stu-id="f2085-137">When you query hello Instance Metadata Service, you must provide hello header `Metadata: true` tooensure hello request was not unintentionally redirected.</span></span>

### <a name="retrieving-metadata"></a><span data-ttu-id="f2085-138">Pobieranie metadanych</span><span class="sxs-lookup"><span data-stu-id="f2085-138">Retrieving metadata</span></span>

<span data-ttu-id="f2085-139">Wystąpienie metadanych jest dostępna do uruchamiania maszyny wirtualne utworzone/zarządzane przy użyciu [usługi Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/).</span><span class="sxs-lookup"><span data-stu-id="f2085-139">Instance metadata is available for running VMs created/managed using [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/).</span></span> <span data-ttu-id="f2085-140">Dostęp do wszystkich kategorii danych dla wystąpienia maszyny wirtualnej przy użyciu hello następujące żądania:</span><span class="sxs-lookup"><span data-stu-id="f2085-140">Access all data categories for a virtual machine instance using hello following request:</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance?api-version=2017-04-02"
```

> [!NOTE] 
> <span data-ttu-id="f2085-141">Wszystkie wystąpienia zapytania metadanych jest rozróżniana wielkość liter.</span><span class="sxs-lookup"><span data-stu-id="f2085-141">All instance metadata queries are case-sensitive.</span></span>

### <a name="data-output"></a><span data-ttu-id="f2085-142">Dane wyjściowe</span><span class="sxs-lookup"><span data-stu-id="f2085-142">Data output</span></span>
<span data-ttu-id="f2085-143">Domyślnie program hello wystąpienia usługi metadanych zwraca dane w formacie JSON (`Content-Type: application/json`).</span><span class="sxs-lookup"><span data-stu-id="f2085-143">By default, hello Instance Metadata Service returns data in JSON format (`Content-Type: application/json`).</span></span> <span data-ttu-id="f2085-144">Jednak różnych interfejsów API może zwracać dane w różnych formatach, jeśli jest to wymagane.</span><span class="sxs-lookup"><span data-stu-id="f2085-144">However, different APIs can return data in different formats if requested.</span></span>
<span data-ttu-id="f2085-145">Witaj poniższej tabeli jest odwołaniem innych formatów danych, który może obsługiwać interfejsy API.</span><span class="sxs-lookup"><span data-stu-id="f2085-145">hello following table is a reference of other data formats APIs may support.</span></span>

<span data-ttu-id="f2085-146">Interfejs API</span><span class="sxs-lookup"><span data-stu-id="f2085-146">API</span></span> | <span data-ttu-id="f2085-147">Domyślny Format danych</span><span class="sxs-lookup"><span data-stu-id="f2085-147">Default Data Format</span></span> | <span data-ttu-id="f2085-148">W innych formatach</span><span class="sxs-lookup"><span data-stu-id="f2085-148">Other Formats</span></span>
--------|---------------------|--------------
<span data-ttu-id="f2085-149">/instance</span><span class="sxs-lookup"><span data-stu-id="f2085-149">/instance</span></span> | <span data-ttu-id="f2085-150">JSON</span><span class="sxs-lookup"><span data-stu-id="f2085-150">json</span></span> | <span data-ttu-id="f2085-151">Tekst</span><span class="sxs-lookup"><span data-stu-id="f2085-151">text</span></span>
<span data-ttu-id="f2085-152">/scheduledevents</span><span class="sxs-lookup"><span data-stu-id="f2085-152">/scheduledevents</span></span> | <span data-ttu-id="f2085-153">JSON</span><span class="sxs-lookup"><span data-stu-id="f2085-153">json</span></span> | <span data-ttu-id="f2085-154">Brak</span><span class="sxs-lookup"><span data-stu-id="f2085-154">none</span></span>

<span data-ttu-id="f2085-155">tooaccess format odpowiedzi z systemem innym niż domyślny, określ żądany format hello jako parametr querystring w żądaniu hello.</span><span class="sxs-lookup"><span data-stu-id="f2085-155">tooaccess a non-default response format, specify hello requested format as a querystring parameter in hello request.</span></span> <span data-ttu-id="f2085-156">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="f2085-156">For example:</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance?api-version=2017-04-02&format=text"
```

### <a name="security"></a><span data-ttu-id="f2085-157">Bezpieczeństwo</span><span class="sxs-lookup"><span data-stu-id="f2085-157">Security</span></span>
<span data-ttu-id="f2085-158">punkt końcowy usługi metadanych wystąpienia Hello jest dostępny tylko w obrębie hello uruchomione wystąpienie maszyny wirtualnej bez obsługi routingu adresu IP.</span><span class="sxs-lookup"><span data-stu-id="f2085-158">hello Instance Metadata Service endpoint is accessible only from within hello running virtual machine instance on a non-routable IP address.</span></span> <span data-ttu-id="f2085-159">Ponadto wszelkie żądania z `X-Forwarded-For` nagłówek został odrzucony przez usługę hello.</span><span class="sxs-lookup"><span data-stu-id="f2085-159">In addition, any request with a `X-Forwarded-For` header is rejected by hello service.</span></span>
<span data-ttu-id="f2085-160">Wymagamy toocontain żądań `Metadata: true` tooensure nagłówek, który hello rzeczywistego żądania bezpośrednio był zamierzony i nie jest częścią niezamierzonych przekierowania.</span><span class="sxs-lookup"><span data-stu-id="f2085-160">We also require requests toocontain a `Metadata: true` header tooensure that hello actual request was directly intended and not a part of unintentional redirection.</span></span> 

### <a name="error"></a><span data-ttu-id="f2085-161">Błąd</span><span class="sxs-lookup"><span data-stu-id="f2085-161">Error</span></span>
<span data-ttu-id="f2085-162">Jeśli istnieje element danych nie można odnaleźć lub źle sformułowane żądanie, hello wystąpienia usługi metadanych zwraca standardowe komunikaty o błędach HTTP.</span><span class="sxs-lookup"><span data-stu-id="f2085-162">If there is a data element not found or a malformed request, hello Instance Metadata Service returns standard HTTP errors.</span></span> <span data-ttu-id="f2085-163">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="f2085-163">For example:</span></span>

<span data-ttu-id="f2085-164">Kod stanu HTTP</span><span class="sxs-lookup"><span data-stu-id="f2085-164">HTTP Status Code</span></span> | <span data-ttu-id="f2085-165">Przyczyna</span><span class="sxs-lookup"><span data-stu-id="f2085-165">Reason</span></span>
----------------|-------
<span data-ttu-id="f2085-166">200 OK</span><span class="sxs-lookup"><span data-stu-id="f2085-166">200 OK</span></span> |
<span data-ttu-id="f2085-167">400 Niewłaściwe żądanie</span><span class="sxs-lookup"><span data-stu-id="f2085-167">400 Bad Request</span></span> | <span data-ttu-id="f2085-168">Brak `Metadata: true` nagłówka</span><span class="sxs-lookup"><span data-stu-id="f2085-168">Missing `Metadata: true` header</span></span>
<span data-ttu-id="f2085-169">404 — Nie odnaleziono</span><span class="sxs-lookup"><span data-stu-id="f2085-169">404 Not Found</span></span> | <span data-ttu-id="f2085-170">Witaj does't żądany element istnieje</span><span class="sxs-lookup"><span data-stu-id="f2085-170">hello requested element does't exist</span></span> 
<span data-ttu-id="f2085-171">405 — metoda nie jest dozwolone</span><span class="sxs-lookup"><span data-stu-id="f2085-171">405 Method Not Allowed</span></span> | <span data-ttu-id="f2085-172">Tylko `GET` i `POST` żądania są obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="f2085-172">Only `GET` and `POST` requests are supported</span></span>
<span data-ttu-id="f2085-173">429 zbyt wiele żądań</span><span class="sxs-lookup"><span data-stu-id="f2085-173">429 Too Many Requests</span></span> | <span data-ttu-id="f2085-174">Interfejs API Hello obecnie obsługuje maksymalnie 5 zapytania na sekundę</span><span class="sxs-lookup"><span data-stu-id="f2085-174">hello API currently supports a maximum of 5 queries per second</span></span>
<span data-ttu-id="f2085-175">Błąd usługi 500</span><span class="sxs-lookup"><span data-stu-id="f2085-175">500 Service Error</span></span>     | <span data-ttu-id="f2085-176">Spróbuj ponownie za jakiś czas</span><span class="sxs-lookup"><span data-stu-id="f2085-176">Retry after some time</span></span>

### <a name="examples"></a><span data-ttu-id="f2085-177">Przykłady</span><span class="sxs-lookup"><span data-stu-id="f2085-177">Examples</span></span>

> [!NOTE] 
> <span data-ttu-id="f2085-178">Wszystkie odpowiedzi interfejsu API są ciągami formatu JSON.</span><span class="sxs-lookup"><span data-stu-id="f2085-178">All API responses are JSON strings.</span></span> <span data-ttu-id="f2085-179">Wszystkie odpowiedzi na przykład następujące są drukowane pretty dla czytelności.</span><span class="sxs-lookup"><span data-stu-id="f2085-179">All following example responses  are pretty-printed for readability.</span></span>

#### <a name="retrieving-network-information"></a><span data-ttu-id="f2085-180">Trwa pobieranie informacji o sieci</span><span class="sxs-lookup"><span data-stu-id="f2085-180">Retrieving network information</span></span>

<span data-ttu-id="f2085-181">**Żądanie**</span><span class="sxs-lookup"><span data-stu-id="f2085-181">**Request**</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/network?api-version=2017-04-02"
```

<span data-ttu-id="f2085-182">**Odpowiedź**</span><span class="sxs-lookup"><span data-stu-id="f2085-182">**Response**</span></span>

> [!NOTE] 
> <span data-ttu-id="f2085-183">odpowiedź Hello jest ciągu JSON.</span><span class="sxs-lookup"><span data-stu-id="f2085-183">hello response is a JSON string.</span></span> <span data-ttu-id="f2085-184">powitania po przykład odpowiedzi jest drukowany pretty dla czytelności.</span><span class="sxs-lookup"><span data-stu-id="f2085-184">hello following example response is pretty-printed for readability.</span></span>

```
{
  "interface": [
    {
      "ipv4": {
        "ipAddress": [
          {
            "privateIpAddress": "10.1.0.4",
            "publicIpAddress": "X.X.X.X"
          }
        ],
        "subnet": [
          {
            "address": "10.1.0.0",
            "prefix": "24"
          }
        ]
      },
      "ipv6": {
        "ipAddress": []
      },
      "macAddress": "000D3AF806EC"
    }
  ]
}

```

#### <a name="retrieving-public-ip-address"></a><span data-ttu-id="f2085-185">Trwa pobieranie publicznego adresu IP</span><span class="sxs-lookup"><span data-stu-id="f2085-185">Retrieving public IP address</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/network/interface/0/ipv4/ipAddress/0/publicIpAddress?api-version=2017-04-02&format=text"
```

#### <a name="retrieving-all-metadata-for-an-instance"></a><span data-ttu-id="f2085-186">Pobieranie wszystkich metadanych dla wystąpienia</span><span class="sxs-lookup"><span data-stu-id="f2085-186">Retrieving all metadata for an instance</span></span>

<span data-ttu-id="f2085-187">**Żądanie**</span><span class="sxs-lookup"><span data-stu-id="f2085-187">**Request**</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance?api-version=2017-04-02"
```

<span data-ttu-id="f2085-188">**Odpowiedź**</span><span class="sxs-lookup"><span data-stu-id="f2085-188">**Response**</span></span>

> [!NOTE] 
> <span data-ttu-id="f2085-189">odpowiedź Hello jest ciągu JSON.</span><span class="sxs-lookup"><span data-stu-id="f2085-189">hello response is a JSON string.</span></span> <span data-ttu-id="f2085-190">powitania po przykład odpowiedzi jest drukowany pretty dla czytelności.</span><span class="sxs-lookup"><span data-stu-id="f2085-190">hello following example response is pretty-printed for readability.</span></span>

```
{
  "compute": {
    "location": "westcentralus",
    "name": "IMDSSample",
    "offer": "UbuntuServer",
    "osType": "Linux",
    "platformFaultDomain": "0",
    "platformUpdateDomain": "0",
    "publisher": "Canonical",
    "sku": "16.04.0-LTS",
    "version": "16.04.201610200",
    "vmId": "5d33a910-a7a0-4443-9f01-6a807801b29b",
    "vmSize": "Standard_A1"
  },
  "network": {
    "interface": [
      {
        "ipv4": {
          "ipAddress": [
            {
              "privateIpAddress": "10.1.0.4",
              "publicIpAddress": "X.X.X.X"
            }
          ],
          "subnet": [
            {
              "address": "10.1.0.0",
              "prefix": "24"
            }
          ]
        },
        "ipv6": {
          "ipAddress": []
        },
        "macAddress": "000D3AF806EC"
      }
    ]
  }
}
```

#### <a name="retrieving-metadata-in-windows-virtual-machine"></a><span data-ttu-id="f2085-191">Pobieranie metadanych maszyny wirtualnej systemu Windows</span><span class="sxs-lookup"><span data-stu-id="f2085-191">Retrieving metadata in Windows virtual machine</span></span>

<span data-ttu-id="f2085-192">**Żądanie**</span><span class="sxs-lookup"><span data-stu-id="f2085-192">**Request**</span></span>

<span data-ttu-id="f2085-193">W systemie Windows można pobrać wystąpienia metadanych za pośrednictwem hello programu PowerShell narzędzia `curl`:</span><span class="sxs-lookup"><span data-stu-id="f2085-193">Instance metadata can be retrieved in Windows via hello PowerShell utility `curl`:</span></span> 

```
curl -H @{'Metadata'='true'} http://169.254.169.254/metadata/instance?api-version=2017-04-02 | select -ExpandProperty Content
```

<span data-ttu-id="f2085-194">Lub za pośrednictwem hello `Invoke-RestMethod` polecenia cmdlet:</span><span class="sxs-lookup"><span data-stu-id="f2085-194">Or through hello `Invoke-RestMethod` cmdlet:</span></span>
    
```
Invoke-RestMethod -Headers @{"Metadata"="true"} -URI http://169.254.169.254/metadata/instance?api-version=2017-04-02 -Method get 
```

<span data-ttu-id="f2085-195">**Odpowiedź**</span><span class="sxs-lookup"><span data-stu-id="f2085-195">**Response**</span></span>

> [!NOTE] 
> <span data-ttu-id="f2085-196">odpowiedź Hello jest ciągu JSON.</span><span class="sxs-lookup"><span data-stu-id="f2085-196">hello response is a JSON string.</span></span> <span data-ttu-id="f2085-197">powitania po przykład odpowiedzi jest drukowany pretty dla czytelności.</span><span class="sxs-lookup"><span data-stu-id="f2085-197">hello following example response  is pretty-printed for readability.</span></span>

```
{
  "compute": {
    "location": "westus",
    "name": "SQLTest",
    "offer": "SQL2016SP1-WS2016",
    "osType": "Windows",
    "platformFaultDomain": "0",
    "platformUpdateDomain": "0",
    "publisher": "MicrosoftSQLServer",
    "sku": "Enterprise",
    "version": "13.0.400110",
    "vmId": "453945c8-3923-4366-b2d3-ea4c80e9b70e",
    "vmSize": "Standard_DS2"
  },
  "network": {
    "interface": [
      {
        "ipv4": {
          "ipAddress": [
            {
              "privateIpAddress": "10.0.1.4",
              "publicIpAddress": "X.X.X.X"
            }
          ],
          "subnet": [
            {
              "address": "10.0.1.0",
              "prefix": "24"
            }
          ]
        },
        "ipv6": {
          "ipAddress": [
            
          ]
        },
        "macAddress": "002248020E1E"
      }
    ]
  }
}
```

## <a name="instance-metadata-data-categories"></a><span data-ttu-id="f2085-198">Kategorie danych metadanych wystąpienia</span><span class="sxs-lookup"><span data-stu-id="f2085-198">Instance metadata data categories</span></span>
<span data-ttu-id="f2085-199">Witaj następujące kategorie danych są dostępne za pośrednictwem hello wystąpienia usługi metadanych:</span><span class="sxs-lookup"><span data-stu-id="f2085-199">hello following data categories are available through hello Instance Metadata Service:</span></span>

<span data-ttu-id="f2085-200">Dane</span><span class="sxs-lookup"><span data-stu-id="f2085-200">Data</span></span> | <span data-ttu-id="f2085-201">Opis</span><span class="sxs-lookup"><span data-stu-id="f2085-201">Description</span></span>
-----|------------
<span data-ttu-id="f2085-202">location</span><span class="sxs-lookup"><span data-stu-id="f2085-202">location</span></span> | <span data-ttu-id="f2085-203">Witaj regionu Azure wirtualna jest uruchomiona</span><span class="sxs-lookup"><span data-stu-id="f2085-203">Azure Region hello VM is running in</span></span>
<span data-ttu-id="f2085-204">name</span><span class="sxs-lookup"><span data-stu-id="f2085-204">name</span></span> | <span data-ttu-id="f2085-205">Nazwa hello maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="f2085-205">Name of hello VM</span></span> 
<span data-ttu-id="f2085-206">Oferta</span><span class="sxs-lookup"><span data-stu-id="f2085-206">offer</span></span> | <span data-ttu-id="f2085-207">Zapewniają informacje o hello obrazu maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="f2085-207">Offer information for hello VM image.</span></span> <span data-ttu-id="f2085-208">Ta wartość ma tylko obrazy wdrożone z galerii Azure obrazu.</span><span class="sxs-lookup"><span data-stu-id="f2085-208">This value is only present for images deployed from Azure image gallery.</span></span>
<span data-ttu-id="f2085-209">Wydawcy</span><span class="sxs-lookup"><span data-stu-id="f2085-209">publisher</span></span> | <span data-ttu-id="f2085-210">Wydawca hello obrazu maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="f2085-210">Publisher of hello VM image</span></span>
<span data-ttu-id="f2085-211">Jednostka SKU</span><span class="sxs-lookup"><span data-stu-id="f2085-211">sku</span></span> | <span data-ttu-id="f2085-212">Określonej jednostki SKU dla obrazu maszyny Wirtualnej hello</span><span class="sxs-lookup"><span data-stu-id="f2085-212">Specific SKU for hello VM image</span></span>  
<span data-ttu-id="f2085-213">Wersja</span><span class="sxs-lookup"><span data-stu-id="f2085-213">version</span></span> | <span data-ttu-id="f2085-214">Wersja obrazu maszyny Wirtualnej hello</span><span class="sxs-lookup"><span data-stu-id="f2085-214">Version of hello VM image</span></span> 
<span data-ttu-id="f2085-215">osType</span><span class="sxs-lookup"><span data-stu-id="f2085-215">osType</span></span> | <span data-ttu-id="f2085-216">Linux lub Windows</span><span class="sxs-lookup"><span data-stu-id="f2085-216">Linux or Windows</span></span> 
<span data-ttu-id="f2085-217">platformUpdateDomain</span><span class="sxs-lookup"><span data-stu-id="f2085-217">platformUpdateDomain</span></span> |  <span data-ttu-id="f2085-218">[Domeny aktualizacji](manage-availability.md) hello wirtualna jest uruchomiona w</span><span class="sxs-lookup"><span data-stu-id="f2085-218">[Update domain](manage-availability.md) hello VM is running in</span></span>
<span data-ttu-id="f2085-219">platformFaultDomain</span><span class="sxs-lookup"><span data-stu-id="f2085-219">platformFaultDomain</span></span> | <span data-ttu-id="f2085-220">[Domena błędów](manage-availability.md) hello wirtualna jest uruchomiona w</span><span class="sxs-lookup"><span data-stu-id="f2085-220">[Fault domain](manage-availability.md) hello VM is running in</span></span>
<span data-ttu-id="f2085-221">vmId</span><span class="sxs-lookup"><span data-stu-id="f2085-221">vmId</span></span> | <span data-ttu-id="f2085-222">[Unikatowy identyfikator](https://azure.microsoft.com/blog/accessing-and-using-azure-vm-unique-id/) dla hello maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="f2085-222">[Unique identifier](https://azure.microsoft.com/blog/accessing-and-using-azure-vm-unique-id/) for hello VM</span></span>
<span data-ttu-id="f2085-223">vmSize</span><span class="sxs-lookup"><span data-stu-id="f2085-223">vmSize</span></span> | [<span data-ttu-id="f2085-224">Rozmiar maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="f2085-224">VM size</span></span>](sizes.md)
<span data-ttu-id="f2085-225">IPv4/elementu privateIpAddress</span><span class="sxs-lookup"><span data-stu-id="f2085-225">ipv4/privateIpAddress</span></span> | <span data-ttu-id="f2085-226">Lokalny adres IPv4 hello maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="f2085-226">Local IPv4 address of hello VM</span></span> 
<span data-ttu-id="f2085-227">IPv4/publicznego adresu IP</span><span class="sxs-lookup"><span data-stu-id="f2085-227">ipv4/publicIpAddress</span></span> | <span data-ttu-id="f2085-228">Publiczny adres IPv4 hello maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="f2085-228">Public IPv4 address of hello VM</span></span>
<span data-ttu-id="f2085-229">podsieć lub adres.</span><span class="sxs-lookup"><span data-stu-id="f2085-229">subnet/address</span></span> | <span data-ttu-id="f2085-230">Adres podsieci hello maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="f2085-230">Subnet address of hello VM</span></span>
<span data-ttu-id="f2085-231">prefiks podsieci /</span><span class="sxs-lookup"><span data-stu-id="f2085-231">subnet/prefix</span></span> | <span data-ttu-id="f2085-232">Prefiks podsieci, przykład 24</span><span class="sxs-lookup"><span data-stu-id="f2085-232">Subnet prefix, example 24</span></span>
<span data-ttu-id="f2085-233">adres IPv6/IP</span><span class="sxs-lookup"><span data-stu-id="f2085-233">ipv6/ipAddress</span></span> | <span data-ttu-id="f2085-234">Lokalny adres IPv6 hello maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="f2085-234">Local IPv6 address of hello VM</span></span>
<span data-ttu-id="f2085-235">MacAddress</span><span class="sxs-lookup"><span data-stu-id="f2085-235">macAddress</span></span> | <span data-ttu-id="f2085-236">Adres mac dla maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="f2085-236">VM mac address</span></span> 
<span data-ttu-id="f2085-237">scheduledevents</span><span class="sxs-lookup"><span data-stu-id="f2085-237">scheduledevents</span></span> | <span data-ttu-id="f2085-238">Obecnie w publicznej wersji zapoznawczej zobacz [scheduledevents](scheduled-events.md)</span><span class="sxs-lookup"><span data-stu-id="f2085-238">Currently in Public Preview See [scheduledevents](scheduled-events.md)</span></span>

## <a name="example-scenarios-for-usage"></a><span data-ttu-id="f2085-239">Przykładowe scenariusze użycia</span><span class="sxs-lookup"><span data-stu-id="f2085-239">Example scenarios for usage</span></span>  

### <a name="tracking-vm-running-on-azure"></a><span data-ttu-id="f2085-240">Śledzenie maszyn wirtualnych działających na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="f2085-240">Tracking VM running on Azure</span></span>

<span data-ttu-id="f2085-241">Jako dostawcę usług mogą wymagać tootrack hello liczbę maszyn wirtualnych z oprogramowaniem lub agentami, którzy muszą tootrack unikatowość hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="f2085-241">As a service provider, you may require tootrack hello number of VMs running your software or have agents that need tootrack uniqueness of hello VM.</span></span> <span data-ttu-id="f2085-242">toobe stanie tooget Unikatowy identyfikator dla maszyny Wirtualnej, użyj hello `vmId` pola wystąpienia metadanych usługi.</span><span class="sxs-lookup"><span data-stu-id="f2085-242">toobe able tooget a unique ID for a VM, use hello `vmId` field from Instance Metadata Service.</span></span>

<span data-ttu-id="f2085-243">**Żądanie**</span><span class="sxs-lookup"><span data-stu-id="f2085-243">**Request**</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/compute/vmId?api-version=2017-04-02&format=text"
```

<span data-ttu-id="f2085-244">**Odpowiedź**</span><span class="sxs-lookup"><span data-stu-id="f2085-244">**Response**</span></span>

```
5c08b38e-4d57-4c23-ac45-aca61037f084
```

### <a name="placement-of-containers-data-partitions-based-faultupdate-domain"></a><span data-ttu-id="f2085-245">Umieszczania kontenery, partycje danych na podstawie domen błędów lub zaktualizowania</span><span class="sxs-lookup"><span data-stu-id="f2085-245">Placement of containers, data-partitions based fault/update domain</span></span> 

<span data-ttu-id="f2085-246">Dla niektórych scenariuszy, umieszczania repliki danych różnych znaczenie ma.</span><span class="sxs-lookup"><span data-stu-id="f2085-246">For certain scenarios, placement of different data replicas is of prime importance.</span></span> <span data-ttu-id="f2085-247">Na przykład [umieszczania repliki systemu plików HDFS](https://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/HdfsDesign.html#Replica_Placement:_The_First_Baby_Steps) lub położenia kontenera za pomocą [orchestrator](https://kubernetes.io/docs/user-guide/node-selection/) może wymagać tooknow hello `platformFaultDomain` i `platformUpdateDomain` hello maszyna wirtualna jest uruchomiona na.</span><span class="sxs-lookup"><span data-stu-id="f2085-247">For example, [HDFS replica placement](https://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/HdfsDesign.html#Replica_Placement:_The_First_Baby_Steps) or container placement via an [orchestrator](https://kubernetes.io/docs/user-guide/node-selection/) may you require tooknow hello `platformFaultDomain` and `platformUpdateDomain` hello VM is running on.</span></span>
<span data-ttu-id="f2085-248">Umożliwia wysyłanie zapytań tych danych bezpośrednio za pomocą hello wystąpienie metadanych usługi.</span><span class="sxs-lookup"><span data-stu-id="f2085-248">You can query this data directly via hello Instance Metadata Service.</span></span>

<span data-ttu-id="f2085-249">**Żądanie**</span><span class="sxs-lookup"><span data-stu-id="f2085-249">**Request**</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/compute/platformFaultDomain?api-version=2017-04-02&format=text" 
```

<span data-ttu-id="f2085-250">**Odpowiedź**</span><span class="sxs-lookup"><span data-stu-id="f2085-250">**Response**</span></span>

```
0
```

### <a name="getting-more-information-about-hello-vm-during-support-case"></a><span data-ttu-id="f2085-251">Więcej informacji na temat hello maszyny Wirtualnej podczas do sprawę pomocy technicznej</span><span class="sxs-lookup"><span data-stu-id="f2085-251">Getting more information about hello VM during support case</span></span> 

<span data-ttu-id="f2085-252">Jako dostawcę usług mogą wystąpić pomocy technicznej miejsce chcesz tooknow więcej informacji na temat hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="f2085-252">As a service provider, you may get a support call where you would like tooknow more information about hello VM.</span></span> <span data-ttu-id="f2085-253">Pytania powitania klienta tooshare hello obliczeń metadane zapewniają podstawowe informacje dotyczące hello pomocy technicznej professional tooknow o rodzaju hello maszyny wirtualnej na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="f2085-253">Asking hello customer tooshare hello compute metadata can provide basic information for hello support professional tooknow about hello kind of VM on Azure.</span></span> 

<span data-ttu-id="f2085-254">**Żądanie**</span><span class="sxs-lookup"><span data-stu-id="f2085-254">**Request**</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/compute?api-version=2017-04-02"
```

<span data-ttu-id="f2085-255">**Odpowiedź**</span><span class="sxs-lookup"><span data-stu-id="f2085-255">**Response**</span></span>

> [!NOTE] 
> <span data-ttu-id="f2085-256">odpowiedź Hello jest ciągu JSON.</span><span class="sxs-lookup"><span data-stu-id="f2085-256">hello response is a JSON string.</span></span> <span data-ttu-id="f2085-257">powitania po przykład odpowiedzi jest drukowany pretty dla czytelności.</span><span class="sxs-lookup"><span data-stu-id="f2085-257">hello following example response is pretty-printed for readability.</span></span>

```
{
  "compute": {
    "location": "CentralUS",
    "name": "IMDSCanary",
    "offer": "RHEL",
    "osType": "Linux",
    "platformFaultDomain": "0",
    "platformUpdateDomain": "0",
    "publisher": "RedHat",
    "sku": "7.2",
    "version": "7.2.20161026",
    "vmId": "5c08b38e-4d57-4c23-ac45-aca61037f084",
    "vmSize": "Standard_DS2"
  }
}
```

### <a name="examples-of-calling-metadata-service-using-different-languages-inside-hello-vm"></a><span data-ttu-id="f2085-258">Przykłady wywoływania usługi metadanych przy użyciu różnych języków wewnątrz hello maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="f2085-258">Examples of calling metadata service using different languages inside hello VM</span></span> 

<span data-ttu-id="f2085-259">Język</span><span class="sxs-lookup"><span data-stu-id="f2085-259">Language</span></span> | <span data-ttu-id="f2085-260">Przykład</span><span class="sxs-lookup"><span data-stu-id="f2085-260">Example</span></span> 
---------|----------------
<span data-ttu-id="f2085-261">Ruby</span><span class="sxs-lookup"><span data-stu-id="f2085-261">Ruby</span></span>     | <span data-ttu-id="f2085-262">https://github.com/Microsoft/azureimds/blob/Master/IMDSSample.RB</span><span class="sxs-lookup"><span data-stu-id="f2085-262">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.rb</span></span>
<span data-ttu-id="f2085-263">Przejdź do sieci Lan</span><span class="sxs-lookup"><span data-stu-id="f2085-263">Go Lan</span></span>   | <span data-ttu-id="f2085-264">https://github.com/Microsoft/azureimds/blob/Master/imdssample.go</span><span class="sxs-lookup"><span data-stu-id="f2085-264">https://github.com/Microsoft/azureimds/blob/master/imdssample.go</span></span>            
<span data-ttu-id="f2085-265">python</span><span class="sxs-lookup"><span data-stu-id="f2085-265">python</span></span>   | <span data-ttu-id="f2085-266">https://github.com/Microsoft/azureimds/blob/Master/IMDSSample.PY</span><span class="sxs-lookup"><span data-stu-id="f2085-266">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.py</span></span>
<span data-ttu-id="f2085-267">C++</span><span class="sxs-lookup"><span data-stu-id="f2085-267">C++</span></span>      | <span data-ttu-id="f2085-268">https://github.com/Microsoft/azureimds/blob/Master/IMDSSample-Windows.cpp</span><span class="sxs-lookup"><span data-stu-id="f2085-268">https://github.com/Microsoft/azureimds/blob/master/IMDSSample-windows.cpp</span></span>
<span data-ttu-id="f2085-269">C#</span><span class="sxs-lookup"><span data-stu-id="f2085-269">C#</span></span>       | <span data-ttu-id="f2085-270">https://github.com/Microsoft/azureimds/blob/Master/IMDSSample.CS</span><span class="sxs-lookup"><span data-stu-id="f2085-270">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.cs</span></span>
<span data-ttu-id="f2085-271">Javascript</span><span class="sxs-lookup"><span data-stu-id="f2085-271">Javascript</span></span> | <span data-ttu-id="f2085-272">https://github.com/Microsoft/azureimds/blob/Master/IMDSSample.js</span><span class="sxs-lookup"><span data-stu-id="f2085-272">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.js</span></span>
<span data-ttu-id="f2085-273">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f2085-273">Powershell</span></span> | <span data-ttu-id="f2085-274">https://github.com/Microsoft/azureimds/blob/Master/IMDSSample.ps1</span><span class="sxs-lookup"><span data-stu-id="f2085-274">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.ps1</span></span>
<span data-ttu-id="f2085-275">Bash</span><span class="sxs-lookup"><span data-stu-id="f2085-275">Bash</span></span>       | <span data-ttu-id="f2085-276">https://github.com/Microsoft/azureimds/blob/Master/IMDSSample.sh</span><span class="sxs-lookup"><span data-stu-id="f2085-276">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.sh</span></span>
    

## <a name="faq"></a><span data-ttu-id="f2085-277">Często zadawane pytania</span><span class="sxs-lookup"><span data-stu-id="f2085-277">FAQ</span></span>
1. <span data-ttu-id="f2085-278">Pojawia się błąd hello `400 Bad Request, Required metadata header not specified`.</span><span class="sxs-lookup"><span data-stu-id="f2085-278">I am getting hello error `400 Bad Request, Required metadata header not specified`.</span></span> <span data-ttu-id="f2085-279">Co to znaczy?</span><span class="sxs-lookup"><span data-stu-id="f2085-279">What does this mean?</span></span>
   * <span data-ttu-id="f2085-280">Hello usługi metadanych wystąpienia wymaga nagłówka hello `Metadata: true` toobe przekazano hello żądania.</span><span class="sxs-lookup"><span data-stu-id="f2085-280">hello Instance Metadata Service requires hello header `Metadata: true` toobe passed in hello request.</span></span> <span data-ttu-id="f2085-281">Przekazywanie tego nagłówka w wywołaniu REST hello umożliwia dostęp toohello wystąpienie metadanych usługi.</span><span class="sxs-lookup"><span data-stu-id="f2085-281">Passing this header in hello REST call allows access toohello Instance Metadata Service.</span></span> 
2. <span data-ttu-id="f2085-282">Dlaczego nie występują obliczeniowe informacji Moje maszyny wirtualnej?</span><span class="sxs-lookup"><span data-stu-id="f2085-282">Why am I not getting compute information for my VM?</span></span>
   * <span data-ttu-id="f2085-283">Obecnie hello wystąpienie metadanych usługi obsługuje tylko wystąpienia utworzone za pomocą Menedżera zasobów Azure.</span><span class="sxs-lookup"><span data-stu-id="f2085-283">Currently hello Instance Metadata Service only supports instances created with Azure Resource Manager.</span></span> <span data-ttu-id="f2085-284">W przyszłości hello może dodać obsługę maszyn wirtualnych usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="f2085-284">In hello future, we may add support for Cloud Service VMs.</span></span>
3. <span data-ttu-id="f2085-285">Napisany wcześniej utworzony Moje maszyny wirtualnej za pomocą usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="f2085-285">I created my Virtual Machine through Azure Resource Manager a while back.</span></span> <span data-ttu-id="f2085-286">Dlaczego mam nie zawiera compute metadane?</span><span class="sxs-lookup"><span data-stu-id="f2085-286">Why am I not see compute metadata information?</span></span>
   * <span data-ttu-id="f2085-287">Wszystkie maszyny wirtualne utworzone po wrz 2016, można dodać [Tag](../../azure-resource-manager/resource-group-using-tags.md) toostart oglądanie obliczeń metadanych.</span><span class="sxs-lookup"><span data-stu-id="f2085-287">For any VMs created after Sep 2016, add a [Tag](../../azure-resource-manager/resource-group-using-tags.md) toostart seeing compute metadata.</span></span> <span data-ttu-id="f2085-288">Dla starszych maszyn wirtualnych (utworzone przed 2016 wrz) Dodaj/Usuń rozszerzenia lub danych dysków toohello wirtualna toorefresh metadanych.</span><span class="sxs-lookup"><span data-stu-id="f2085-288">For older VMs (created before Sep 2016), add/remove extensions or data disks toohello VM toorefresh metadata.</span></span>
4. <span data-ttu-id="f2085-289">Dlaczego otrzymuję błąd hello `500 Internal Server Error`?</span><span class="sxs-lookup"><span data-stu-id="f2085-289">Why am I getting hello error `500 Internal Server Error`?</span></span>
   * <span data-ttu-id="f2085-290">Ponów żądanie w oparciu wykładniczego wycofywania systemu.</span><span class="sxs-lookup"><span data-stu-id="f2085-290">Please retry your request based on exponential back off system.</span></span> <span data-ttu-id="f2085-291">Jeśli hello problem będzie się powtarzał skontaktuj się z pomocą techniczną platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="f2085-291">If hello issue persists contact  Azure support.</span></span>
5. <span data-ttu-id="f2085-292">Gdzie udostępniać dodatkowe pytania/komentarze?</span><span class="sxs-lookup"><span data-stu-id="f2085-292">Where do I share additional questions/comments?</span></span>
   * <span data-ttu-id="f2085-293">Wyślij komentarze dotyczące http://feedback.azure.com.</span><span class="sxs-lookup"><span data-stu-id="f2085-293">Send your comments on http://feedback.azure.com.</span></span>
7. <span data-ttu-id="f2085-294">Czy to pomoże dla wystąpienia ustawić skali maszyny wirtualnej?</span><span class="sxs-lookup"><span data-stu-id="f2085-294">Would this work for Virtual Machine Scale Set Instance?</span></span>
   * <span data-ttu-id="f2085-295">Tak, usługa metadanych jest dostępna dla wystąpień ustawić skali.</span><span class="sxs-lookup"><span data-stu-id="f2085-295">Yes Metadata service is available for Scale Set Instances.</span></span> 
6. <span data-ttu-id="f2085-296">Jak uzyskać pomoc techniczną dla usługi hello?</span><span class="sxs-lookup"><span data-stu-id="f2085-296">How do I get support for hello service?</span></span>
   * <span data-ttu-id="f2085-297">tooget obsługę usługi hello Utwórz problem pomocy technicznej w portalu Azure, aby hello maszyny Wirtualnej, jeśli nie jesteś odpowiedzi metadanych stanie tooget mimo ponownych prób długa</span><span class="sxs-lookup"><span data-stu-id="f2085-297">tooget support for hello service, create a support issue in Azure portal for hello VM where you are not able tooget metadata response after long retries</span></span> 

   ![Obsługa metadanych wystąpienia](./media/instance-metadata-service/InstanceMetadata-support.png)
    
## <a name="next-steps"></a><span data-ttu-id="f2085-299">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f2085-299">Next steps</span></span>

- <span data-ttu-id="f2085-300">Dowiedz się więcej o hello [zaplanowane zdarzenia](scheduled-events.md) interfejsu API **w publicznej wersji zapoznawczej** podał hello metadanych wystąpienia usługi.</span><span class="sxs-lookup"><span data-stu-id="f2085-300">Learn more about hello [Scheduled Events](scheduled-events.md) API **in public preview** provided by hello Instance Metadata service.</span></span>
