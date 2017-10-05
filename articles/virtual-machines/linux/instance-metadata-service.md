---
title: "Usługa metadanych wystąpienia platformy Azure dla maszyn wirtualnych systemu Linux | Dokumentacja firmy Microsoft"
description: "Interfejs rESTful można pobrać informacji o Linux VM obliczeniowych, sieci i zdarzeń planowanych konserwacji."
services: virtual-machines-linux
documentationcenter: 
author: harijay
manager: timlt
editor: 
tags: azure-resource-manager
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 08/11/2017
ms.author: harijay
ms.openlocfilehash: a61acbe0532ece3a6a26ceb366c12c69db4c304c
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="azure-instance-metadata-service-for-linux-vms"></a><span data-ttu-id="d0a5b-103">Usługa Azure wystąpienie metadanych dla maszyn wirtualnych systemu Linux</span><span class="sxs-lookup"><span data-stu-id="d0a5b-103">Azure Instance Metadata service for Linux VMs</span></span>


<span data-ttu-id="d0a5b-104">Usługę Azure wystąpienie metadanych dostarcza informacji o uruchomionych wystąpień maszyn wirtualnych, które mogą służyć do zarządzania i skonfigurować maszyny wirtualne.</span><span class="sxs-lookup"><span data-stu-id="d0a5b-104">The Azure Instance Metadata Service provides information about running virtual machine instances that can be used to manage and configure your virtual machines.</span></span>
<span data-ttu-id="d0a5b-105">Dotyczy to również informacje, takie jak jednostka SKU, konfiguracji sieci i zdarzeń planowanych konserwacji.</span><span class="sxs-lookup"><span data-stu-id="d0a5b-105">This includes information such as SKU, network configuration, and upcoming maintenance events.</span></span> <span data-ttu-id="d0a5b-106">Aby uzyskać więcej informacji na jakie rodzaje informacji jest dostępnych w temacie [kategorie metadanych](#instance-metadata-data-categories).</span><span class="sxs-lookup"><span data-stu-id="d0a5b-106">For more information on what type of information is available, see [metadata categories](#instance-metadata-data-categories).</span></span>

<span data-ttu-id="d0a5b-107">Usługa metadanych wystąpienia platformy Azure jest punkt końcowy REST jest dostępny dla wszystkich maszyn wirtualnych IaaS utworzony za pośrednictwem [usługi Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/).</span><span class="sxs-lookup"><span data-stu-id="d0a5b-107">Azure's Instance Metadata Service is a REST Endpoint accessible to all IaaS VMs created via the [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/).</span></span> <span data-ttu-id="d0a5b-108">Punkt końcowy jest dostępny w dobrze znanego adresu IP bez obsługi routingu (`169.254.169.254`) który jest możliwy tylko z poziomu maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="d0a5b-108">The endpoint is available at a well-known non-routable IP address (`169.254.169.254`) that can be accessed only from within the VM.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d0a5b-109">Ta usługa jest **ogólnie dostępna** w globalnej regiony platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="d0a5b-109">This service is  **generally available** in Global Azure Regions.</span></span> <span data-ttu-id="d0a5b-110">Znajduje się w publicznej wersji zapoznawczej dla instytucji rządowych, Chin i chmury Azure niemiecki.</span><span class="sxs-lookup"><span data-stu-id="d0a5b-110">It is in Public preview for Government, China, and German Azure Cloud.</span></span> <span data-ttu-id="d0a5b-111">Regularnie odbiera aktualizacje, aby udostępnić nowe informacje o wystąpieniu maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="d0a5b-111">It regularly receives updates to expose new information about virtual machine instances.</span></span> <span data-ttu-id="d0a5b-112">Ta strona odzwierciedla aktualne [kategorii danych](#instance-metadata-data-categories) dostępne.</span><span class="sxs-lookup"><span data-stu-id="d0a5b-112">This page reflects the up-to-date [data categories](#instance-metadata-data-categories) available.</span></span>

## <a name="service-availability"></a><span data-ttu-id="d0a5b-113">Dostępność usług</span><span class="sxs-lookup"><span data-stu-id="d0a5b-113">Service availability</span></span>
<span data-ttu-id="d0a5b-114">Usługa jest dostępna we wszystkich regionach globalne Azure ogólnie dostępna.</span><span class="sxs-lookup"><span data-stu-id="d0a5b-114">The service is available in all generally available Global Azure regions.</span></span> <span data-ttu-id="d0a5b-115">Usługa jest w wersji zapoznawczej w regionach dla instytucji rządowych, Chiny lub Niemczech.</span><span class="sxs-lookup"><span data-stu-id="d0a5b-115">The service is in public preview  in the Government, China, or Germany regions.</span></span>

<span data-ttu-id="d0a5b-116">Regiony</span><span class="sxs-lookup"><span data-stu-id="d0a5b-116">Regions</span></span>                                        | <span data-ttu-id="d0a5b-117">Dostępność?</span><span class="sxs-lookup"><span data-stu-id="d0a5b-117">Availability?</span></span>
-----------------------------------------------|-----------------------------------------------
[<span data-ttu-id="d0a5b-118">Wszystkie ogólnie dostępna globalne regiony platformy Azure</span><span class="sxs-lookup"><span data-stu-id="d0a5b-118">All Generally Available Global Azure Regions</span></span>](https://azure.microsoft.com/regions/)     | <span data-ttu-id="d0a5b-119">Ogólnie dostępna</span><span class="sxs-lookup"><span data-stu-id="d0a5b-119">Generally Available</span></span> 
[<span data-ttu-id="d0a5b-120">Azure dla instytucji rządowych</span><span class="sxs-lookup"><span data-stu-id="d0a5b-120">Azure Government</span></span>](https://azure.microsoft.com/overview/clouds/government/)              | <span data-ttu-id="d0a5b-121">W wersji zapoznawczej</span><span class="sxs-lookup"><span data-stu-id="d0a5b-121">In Preview</span></span> 
[<span data-ttu-id="d0a5b-122">Chin Azure</span><span class="sxs-lookup"><span data-stu-id="d0a5b-122">Azure China</span></span>](https://www.azure.cn/)                                                           | <span data-ttu-id="d0a5b-123">W wersji zapoznawczej</span><span class="sxs-lookup"><span data-stu-id="d0a5b-123">In Preview</span></span>
[<span data-ttu-id="d0a5b-124">Niemcy Azure</span><span class="sxs-lookup"><span data-stu-id="d0a5b-124">Azure Germany</span></span>](https://azure.microsoft.com/overview/clouds/germany/)                    | <span data-ttu-id="d0a5b-125">W wersji zapoznawczej</span><span class="sxs-lookup"><span data-stu-id="d0a5b-125">In Preview</span></span>

<span data-ttu-id="d0a5b-126">Ta tabela jest aktualizowany, gdy usługa stanie się dostępny w innych chmur platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="d0a5b-126">This table is updated when the service becomes available in other Azure clouds.</span></span>

<span data-ttu-id="d0a5b-127">Wypróbowanie usługi metadanych wystąpienia, należy utworzyć Maszynę wirtualną z [usługi Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/) lub [portalu Azure](http://portal.azure.com) w regionach powyżej i postępuj zgodnie z poniższym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="d0a5b-127">To try out the Instance Metadata Service, create a VM from [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/) or the [Azure portal](http://portal.azure.com) in the above regions and follow the examples below.</span></span>

## <a name="usage"></a><span data-ttu-id="d0a5b-128">Sposób użycia</span><span class="sxs-lookup"><span data-stu-id="d0a5b-128">Usage</span></span>

### <a name="versioning"></a><span data-ttu-id="d0a5b-129">Przechowywanie wersji</span><span class="sxs-lookup"><span data-stu-id="d0a5b-129">Versioning</span></span>
<span data-ttu-id="d0a5b-130">Wystąpienie usługi metadanych jest kontrolą wersji.</span><span class="sxs-lookup"><span data-stu-id="d0a5b-130">The Instance Metadata Service is versioned.</span></span> <span data-ttu-id="d0a5b-131">Wersje są obowiązkowe i bieżąca wersja to `2017-04-02`.</span><span class="sxs-lookup"><span data-stu-id="d0a5b-131">Versions are mandatory and the current version is `2017-04-02`.</span></span>

> [!NOTE] 
> <span data-ttu-id="d0a5b-132">Poprzednie wersje Podgląd zdarzeń zaplanowane {najnowszych} obsługiwana jako wersja interfejsu api.</span><span class="sxs-lookup"><span data-stu-id="d0a5b-132">Previous preview releases of scheduled events supported {latest} as the api-version.</span></span> <span data-ttu-id="d0a5b-133">Ten format jest już obsługiwane i zostaną wycofane w przyszłości.</span><span class="sxs-lookup"><span data-stu-id="d0a5b-133">This format is no longer supported and will be deprecated in the future.</span></span>

<span data-ttu-id="d0a5b-134">Przy wdrażaniu nowsze wersje, starsze wersje nadal będą dostępne dla zgodności czy skrypty są zależne formatów określonych danych.</span><span class="sxs-lookup"><span data-stu-id="d0a5b-134">As we add newer versions, older versions can still be accessed for compatibility if your scripts have dependencies on specific data formats.</span></span> <span data-ttu-id="d0a5b-135">Jednak należy pamiętać, że bieżący version(2017-03-01) Podgląd mogą nie być dostępne po usługi jest ogólnie dostępna.</span><span class="sxs-lookup"><span data-stu-id="d0a5b-135">However, note that the current preview version(2017-03-01) may not be available once the service is generally available.</span></span>

### <a name="using-headers"></a><span data-ttu-id="d0a5b-136">Korzystanie z nagłówków</span><span class="sxs-lookup"><span data-stu-id="d0a5b-136">Using headers</span></span>
<span data-ttu-id="d0a5b-137">Kwerenda usługi metadanych wystąpienia, należy określić nagłówek `Metadata: true` aby upewnić się, żądanie nie zostało przekierowane przypadkowo.</span><span class="sxs-lookup"><span data-stu-id="d0a5b-137">When you query the Instance Metadata Service, you must provide the header `Metadata: true` to ensure the request was not unintentionally redirected.</span></span>

### <a name="retrieving-metadata"></a><span data-ttu-id="d0a5b-138">Pobieranie metadanych</span><span class="sxs-lookup"><span data-stu-id="d0a5b-138">Retrieving metadata</span></span>

<span data-ttu-id="d0a5b-139">Wystąpienie metadanych jest dostępna do uruchamiania maszyny wirtualne utworzone/zarządzane przy użyciu [usługi Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/).</span><span class="sxs-lookup"><span data-stu-id="d0a5b-139">Instance metadata is available for running VMs created/managed using [Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/).</span></span> <span data-ttu-id="d0a5b-140">Dostęp do wszystkich kategorii danych dla wystąpienia maszyny wirtualnej za pomocą następujących żądania:</span><span class="sxs-lookup"><span data-stu-id="d0a5b-140">Access all data categories for a virtual machine instance using the following request:</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance?api-version=2017-04-02"
```

> [!NOTE] 
> <span data-ttu-id="d0a5b-141">Wszystkie wystąpienia zapytania metadanych jest rozróżniana wielkość liter.</span><span class="sxs-lookup"><span data-stu-id="d0a5b-141">All instance metadata queries are case-sensitive.</span></span>

### <a name="data-output"></a><span data-ttu-id="d0a5b-142">Dane wyjściowe</span><span class="sxs-lookup"><span data-stu-id="d0a5b-142">Data output</span></span>
<span data-ttu-id="d0a5b-143">Domyślnie usługa metadanych wystąpienia zwraca dane w formacie JSON (`Content-Type: application/json`).</span><span class="sxs-lookup"><span data-stu-id="d0a5b-143">By default, the Instance Metadata Service returns data in JSON format (`Content-Type: application/json`).</span></span> <span data-ttu-id="d0a5b-144">Jednak różnych interfejsów API może zwracać dane w różnych formatach, jeśli jest to wymagane.</span><span class="sxs-lookup"><span data-stu-id="d0a5b-144">However, different APIs can return data in different formats if requested.</span></span>
<span data-ttu-id="d0a5b-145">Poniższa tabela jest odwołaniem innych formatów danych, który może obsługiwać interfejsy API.</span><span class="sxs-lookup"><span data-stu-id="d0a5b-145">The following table is a reference of other data formats APIs may support.</span></span>

<span data-ttu-id="d0a5b-146">Interfejs API</span><span class="sxs-lookup"><span data-stu-id="d0a5b-146">API</span></span> | <span data-ttu-id="d0a5b-147">Domyślny Format danych</span><span class="sxs-lookup"><span data-stu-id="d0a5b-147">Default Data Format</span></span> | <span data-ttu-id="d0a5b-148">W innych formatach</span><span class="sxs-lookup"><span data-stu-id="d0a5b-148">Other Formats</span></span>
--------|---------------------|--------------
<span data-ttu-id="d0a5b-149">/instance</span><span class="sxs-lookup"><span data-stu-id="d0a5b-149">/instance</span></span> | <span data-ttu-id="d0a5b-150">JSON</span><span class="sxs-lookup"><span data-stu-id="d0a5b-150">json</span></span> | <span data-ttu-id="d0a5b-151">Tekst</span><span class="sxs-lookup"><span data-stu-id="d0a5b-151">text</span></span>
<span data-ttu-id="d0a5b-152">/scheduledevents</span><span class="sxs-lookup"><span data-stu-id="d0a5b-152">/scheduledevents</span></span> | <span data-ttu-id="d0a5b-153">JSON</span><span class="sxs-lookup"><span data-stu-id="d0a5b-153">json</span></span> | <span data-ttu-id="d0a5b-154">Brak</span><span class="sxs-lookup"><span data-stu-id="d0a5b-154">none</span></span>

<span data-ttu-id="d0a5b-155">Aby uzyskać dostęp, format odpowiedzi z systemem innym niż domyślny, określ żądany format jako parametr querystring w żądaniu.</span><span class="sxs-lookup"><span data-stu-id="d0a5b-155">To access a non-default response format, specify the requested format as a querystring parameter in the request.</span></span> <span data-ttu-id="d0a5b-156">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="d0a5b-156">For example:</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance?api-version=2017-04-02&format=text"
```

### <a name="security"></a><span data-ttu-id="d0a5b-157">Bezpieczeństwo</span><span class="sxs-lookup"><span data-stu-id="d0a5b-157">Security</span></span>
<span data-ttu-id="d0a5b-158">Punkt końcowy usługi metadanych wystąpienia jest dostępny tylko w obrębie uruchomione wystąpienie maszyny wirtualnej bez obsługi routingu adresu IP.</span><span class="sxs-lookup"><span data-stu-id="d0a5b-158">The Instance Metadata Service endpoint is accessible only from within the running virtual machine instance on a non-routable IP address.</span></span> <span data-ttu-id="d0a5b-159">Ponadto wszelkie żądania z `X-Forwarded-For` nagłówek został odrzucony przez usługę.</span><span class="sxs-lookup"><span data-stu-id="d0a5b-159">In addition, any request with a `X-Forwarded-For` header is rejected by the service.</span></span>
<span data-ttu-id="d0a5b-160">Wymagamy żądania zawiera `Metadata: true` nagłówka, aby upewnić się, że rzeczywistego żądania bezpośrednio był zamierzony i nie jest częścią niezamierzonych przekierowania.</span><span class="sxs-lookup"><span data-stu-id="d0a5b-160">We also require requests to contain a `Metadata: true` header to ensure that the actual request was directly intended and not a part of unintentional redirection.</span></span> 

### <a name="error"></a><span data-ttu-id="d0a5b-161">Błąd</span><span class="sxs-lookup"><span data-stu-id="d0a5b-161">Error</span></span>
<span data-ttu-id="d0a5b-162">Jeśli istnieje element danych nie można odnaleźć lub źle sformułowane żądanie, wystąpienie usługi metadanych zwraca standardowe komunikaty o błędach HTTP.</span><span class="sxs-lookup"><span data-stu-id="d0a5b-162">If there is a data element not found or a malformed request, the Instance Metadata Service returns standard HTTP errors.</span></span> <span data-ttu-id="d0a5b-163">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="d0a5b-163">For example:</span></span>

<span data-ttu-id="d0a5b-164">Kod stanu HTTP</span><span class="sxs-lookup"><span data-stu-id="d0a5b-164">HTTP Status Code</span></span> | <span data-ttu-id="d0a5b-165">Przyczyna</span><span class="sxs-lookup"><span data-stu-id="d0a5b-165">Reason</span></span>
----------------|-------
<span data-ttu-id="d0a5b-166">200 OK</span><span class="sxs-lookup"><span data-stu-id="d0a5b-166">200 OK</span></span> |
<span data-ttu-id="d0a5b-167">400 Niewłaściwe żądanie</span><span class="sxs-lookup"><span data-stu-id="d0a5b-167">400 Bad Request</span></span> | <span data-ttu-id="d0a5b-168">Brak `Metadata: true` nagłówka</span><span class="sxs-lookup"><span data-stu-id="d0a5b-168">Missing `Metadata: true` header</span></span>
<span data-ttu-id="d0a5b-169">404 — Nie odnaleziono</span><span class="sxs-lookup"><span data-stu-id="d0a5b-169">404 Not Found</span></span> | <span data-ttu-id="d0a5b-170">Istnieje does't żądanego elementu</span><span class="sxs-lookup"><span data-stu-id="d0a5b-170">The requested element does't exist</span></span> 
<span data-ttu-id="d0a5b-171">405 — metoda nie jest dozwolone</span><span class="sxs-lookup"><span data-stu-id="d0a5b-171">405 Method Not Allowed</span></span> | <span data-ttu-id="d0a5b-172">Tylko `GET` i `POST` żądania są obsługiwane.</span><span class="sxs-lookup"><span data-stu-id="d0a5b-172">Only `GET` and `POST` requests are supported</span></span>
<span data-ttu-id="d0a5b-173">429 zbyt wiele żądań</span><span class="sxs-lookup"><span data-stu-id="d0a5b-173">429 Too Many Requests</span></span> | <span data-ttu-id="d0a5b-174">Interfejs API obsługuje obecnie maksymalnie 5 zapytania na sekundę</span><span class="sxs-lookup"><span data-stu-id="d0a5b-174">The API currently supports a maximum of 5 queries per second</span></span>
<span data-ttu-id="d0a5b-175">Błąd usługi 500</span><span class="sxs-lookup"><span data-stu-id="d0a5b-175">500 Service Error</span></span>     | <span data-ttu-id="d0a5b-176">Spróbuj ponownie za jakiś czas</span><span class="sxs-lookup"><span data-stu-id="d0a5b-176">Retry after some time</span></span>

### <a name="examples"></a><span data-ttu-id="d0a5b-177">Przykłady</span><span class="sxs-lookup"><span data-stu-id="d0a5b-177">Examples</span></span>

> [!NOTE] 
> <span data-ttu-id="d0a5b-178">Wszystkie odpowiedzi interfejsu API są ciągami formatu JSON.</span><span class="sxs-lookup"><span data-stu-id="d0a5b-178">All API responses are JSON strings.</span></span> <span data-ttu-id="d0a5b-179">Wszystkie odpowiedzi na przykład następujące są drukowane pretty dla czytelności.</span><span class="sxs-lookup"><span data-stu-id="d0a5b-179">All following example responses  are pretty-printed for readability.</span></span>

#### <a name="retrieving-network-information"></a><span data-ttu-id="d0a5b-180">Trwa pobieranie informacji o sieci</span><span class="sxs-lookup"><span data-stu-id="d0a5b-180">Retrieving network information</span></span>

<span data-ttu-id="d0a5b-181">**Żądanie**</span><span class="sxs-lookup"><span data-stu-id="d0a5b-181">**Request**</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/network?api-version=2017-04-02"
```

<span data-ttu-id="d0a5b-182">**Odpowiedź**</span><span class="sxs-lookup"><span data-stu-id="d0a5b-182">**Response**</span></span>

> [!NOTE] 
> <span data-ttu-id="d0a5b-183">Odpowiedź jest ciągu JSON.</span><span class="sxs-lookup"><span data-stu-id="d0a5b-183">The response is a JSON string.</span></span> <span data-ttu-id="d0a5b-184">Następujący przykład odpowiedzi jest drukowany pretty dla czytelności.</span><span class="sxs-lookup"><span data-stu-id="d0a5b-184">The following example response is pretty-printed for readability.</span></span>

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

#### <a name="retrieving-public-ip-address"></a><span data-ttu-id="d0a5b-185">Trwa pobieranie publicznego adresu IP</span><span class="sxs-lookup"><span data-stu-id="d0a5b-185">Retrieving public IP address</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/network/interface/0/ipv4/ipAddress/0/publicIpAddress?api-version=2017-04-02&format=text"
```

#### <a name="retrieving-all-metadata-for-an-instance"></a><span data-ttu-id="d0a5b-186">Pobieranie wszystkich metadanych dla wystąpienia</span><span class="sxs-lookup"><span data-stu-id="d0a5b-186">Retrieving all metadata for an instance</span></span>

<span data-ttu-id="d0a5b-187">**Żądanie**</span><span class="sxs-lookup"><span data-stu-id="d0a5b-187">**Request**</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance?api-version=2017-04-02"
```

<span data-ttu-id="d0a5b-188">**Odpowiedź**</span><span class="sxs-lookup"><span data-stu-id="d0a5b-188">**Response**</span></span>

> [!NOTE] 
> <span data-ttu-id="d0a5b-189">Odpowiedź jest ciągu JSON.</span><span class="sxs-lookup"><span data-stu-id="d0a5b-189">The response is a JSON string.</span></span> <span data-ttu-id="d0a5b-190">Następujący przykład odpowiedzi jest drukowany pretty dla czytelności.</span><span class="sxs-lookup"><span data-stu-id="d0a5b-190">The following example response is pretty-printed for readability.</span></span>

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

#### <a name="retrieving-metadata-in-windows-virtual-machine"></a><span data-ttu-id="d0a5b-191">Pobieranie metadanych maszyny wirtualnej w systemie Windows</span><span class="sxs-lookup"><span data-stu-id="d0a5b-191">Retrieving metadata in Windows Virtual Machine</span></span>

<span data-ttu-id="d0a5b-192">**Żądanie**</span><span class="sxs-lookup"><span data-stu-id="d0a5b-192">**Request**</span></span>

<span data-ttu-id="d0a5b-193">W systemie Windows można pobrać metadanych wystąpienia za pomocą programu PowerShell narzędzia `curl`:</span><span class="sxs-lookup"><span data-stu-id="d0a5b-193">Instance metadata can be retrieved in Windows via the PowerShell utility `curl`:</span></span> 

```
curl -H @{'Metadata'='true'} http://169.254.169.254/metadata/instance?api-version=2017-04-02 | select -ExpandProperty Content
```

<span data-ttu-id="d0a5b-194">Lub za pomocą `Invoke-RestMethod` polecenia cmdlet:</span><span class="sxs-lookup"><span data-stu-id="d0a5b-194">Or through the `Invoke-RestMethod` cmdlet:</span></span>
    
```
Invoke-RestMethod -Headers @{"Metadata"="true"} -URI http://169.254.169.254/metadata/instance?api-version=2017-04-02 -Method get 
```

<span data-ttu-id="d0a5b-195">**Odpowiedź**</span><span class="sxs-lookup"><span data-stu-id="d0a5b-195">**Response**</span></span>

> [!NOTE] 
> <span data-ttu-id="d0a5b-196">Odpowiedź jest ciągu JSON.</span><span class="sxs-lookup"><span data-stu-id="d0a5b-196">The response is a JSON string.</span></span> <span data-ttu-id="d0a5b-197">Następujący przykład odpowiedzi jest drukowany pretty dla czytelności.</span><span class="sxs-lookup"><span data-stu-id="d0a5b-197">The following example response  is pretty-printed for readability.</span></span>

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

## <a name="instance-metadata-data-categories"></a><span data-ttu-id="d0a5b-198">Kategorie danych metadanych wystąpienia</span><span class="sxs-lookup"><span data-stu-id="d0a5b-198">Instance metadata data categories</span></span>
<span data-ttu-id="d0a5b-199">Następujące kategorie danych są dostępne za pośrednictwem usługi metadanych wystąpienie:</span><span class="sxs-lookup"><span data-stu-id="d0a5b-199">The following data categories are available through the Instance Metadata Service:</span></span>

<span data-ttu-id="d0a5b-200">Dane</span><span class="sxs-lookup"><span data-stu-id="d0a5b-200">Data</span></span> | <span data-ttu-id="d0a5b-201">Opis</span><span class="sxs-lookup"><span data-stu-id="d0a5b-201">Description</span></span>
-----|------------
<span data-ttu-id="d0a5b-202">location</span><span class="sxs-lookup"><span data-stu-id="d0a5b-202">location</span></span> | <span data-ttu-id="d0a5b-203">Region platformy Azure, maszyna wirtualna jest uruchomiona</span><span class="sxs-lookup"><span data-stu-id="d0a5b-203">Azure Region the VM is running in</span></span>
<span data-ttu-id="d0a5b-204">name</span><span class="sxs-lookup"><span data-stu-id="d0a5b-204">name</span></span> | <span data-ttu-id="d0a5b-205">Nazwa maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="d0a5b-205">Name of the VM</span></span> 
<span data-ttu-id="d0a5b-206">Oferta</span><span class="sxs-lookup"><span data-stu-id="d0a5b-206">offer</span></span> | <span data-ttu-id="d0a5b-207">Oferują informacji o obrazie maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="d0a5b-207">Offer information for the VM image.</span></span> <span data-ttu-id="d0a5b-208">Ta wartość ma tylko obrazy wdrożone z galerii Azure obrazu.</span><span class="sxs-lookup"><span data-stu-id="d0a5b-208">This value is only present for images deployed from Azure image gallery.</span></span>
<span data-ttu-id="d0a5b-209">Wydawcy</span><span class="sxs-lookup"><span data-stu-id="d0a5b-209">publisher</span></span> | <span data-ttu-id="d0a5b-210">Wydawcy obrazu maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="d0a5b-210">Publisher of the VM image</span></span>
<span data-ttu-id="d0a5b-211">Jednostka SKU</span><span class="sxs-lookup"><span data-stu-id="d0a5b-211">sku</span></span> | <span data-ttu-id="d0a5b-212">Określonej jednostki SKU dla obrazu maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="d0a5b-212">Specific SKU for the VM image</span></span>  
<span data-ttu-id="d0a5b-213">Wersja</span><span class="sxs-lookup"><span data-stu-id="d0a5b-213">version</span></span> | <span data-ttu-id="d0a5b-214">Wersja obrazu maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="d0a5b-214">Version of the VM image</span></span> 
<span data-ttu-id="d0a5b-215">osType</span><span class="sxs-lookup"><span data-stu-id="d0a5b-215">osType</span></span> | <span data-ttu-id="d0a5b-216">Linux lub Windows</span><span class="sxs-lookup"><span data-stu-id="d0a5b-216">Linux or Windows</span></span> 
<span data-ttu-id="d0a5b-217">platformUpdateDomain</span><span class="sxs-lookup"><span data-stu-id="d0a5b-217">platformUpdateDomain</span></span> |  <span data-ttu-id="d0a5b-218">[Domeny aktualizacji](manage-availability.md) wirtualna jest uruchomiona</span><span class="sxs-lookup"><span data-stu-id="d0a5b-218">[Update domain](manage-availability.md) the VM is running in</span></span>
<span data-ttu-id="d0a5b-219">platformFaultDomain</span><span class="sxs-lookup"><span data-stu-id="d0a5b-219">platformFaultDomain</span></span> | <span data-ttu-id="d0a5b-220">[Domena błędów](manage-availability.md) wirtualna jest uruchomiona</span><span class="sxs-lookup"><span data-stu-id="d0a5b-220">[Fault domain](manage-availability.md) the VM is running in</span></span>
<span data-ttu-id="d0a5b-221">vmId</span><span class="sxs-lookup"><span data-stu-id="d0a5b-221">vmId</span></span> | <span data-ttu-id="d0a5b-222">[Unikatowy identyfikator](https://azure.microsoft.com/blog/accessing-and-using-azure-vm-unique-id/) dla maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="d0a5b-222">[Unique identifier](https://azure.microsoft.com/blog/accessing-and-using-azure-vm-unique-id/) for the VM</span></span>
<span data-ttu-id="d0a5b-223">vmSize</span><span class="sxs-lookup"><span data-stu-id="d0a5b-223">vmSize</span></span> | [<span data-ttu-id="d0a5b-224">Rozmiar maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="d0a5b-224">VM size</span></span>](sizes.md)
<span data-ttu-id="d0a5b-225">IPv4/elementu privateIpAddress</span><span class="sxs-lookup"><span data-stu-id="d0a5b-225">ipv4/privateIpAddress</span></span> | <span data-ttu-id="d0a5b-226">Lokalny adres IPv4 maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="d0a5b-226">Local IPv4 address of the VM</span></span> 
<span data-ttu-id="d0a5b-227">IPv4/publicznego adresu IP</span><span class="sxs-lookup"><span data-stu-id="d0a5b-227">ipv4/publicIpAddress</span></span> | <span data-ttu-id="d0a5b-228">Publiczny adres IPv4 maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="d0a5b-228">Public IPv4 address of the VM</span></span>
<span data-ttu-id="d0a5b-229">podsieć lub adres.</span><span class="sxs-lookup"><span data-stu-id="d0a5b-229">subnet/address</span></span> | <span data-ttu-id="d0a5b-230">Adres podsieci maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="d0a5b-230">Subnet address of the VM</span></span>
<span data-ttu-id="d0a5b-231">prefiks podsieci /</span><span class="sxs-lookup"><span data-stu-id="d0a5b-231">subnet/prefix</span></span> | <span data-ttu-id="d0a5b-232">Prefiks podsieci, przykład 24</span><span class="sxs-lookup"><span data-stu-id="d0a5b-232">Subnet prefix, example 24</span></span>
<span data-ttu-id="d0a5b-233">adres IPv6/IP</span><span class="sxs-lookup"><span data-stu-id="d0a5b-233">ipv6/ipAddress</span></span> | <span data-ttu-id="d0a5b-234">Lokalny adres IPv6 maszyny wirtualnej</span><span class="sxs-lookup"><span data-stu-id="d0a5b-234">Local IPv6 address of the VM</span></span>
<span data-ttu-id="d0a5b-235">MacAddress</span><span class="sxs-lookup"><span data-stu-id="d0a5b-235">macAddress</span></span> | <span data-ttu-id="d0a5b-236">Adres mac dla maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="d0a5b-236">VM mac address</span></span> 
<span data-ttu-id="d0a5b-237">scheduledevents</span><span class="sxs-lookup"><span data-stu-id="d0a5b-237">scheduledevents</span></span> | <span data-ttu-id="d0a5b-238">Obecnie w publicznej wersji zapoznawczej zobacz [scheduledevents](scheduled-events.md)</span><span class="sxs-lookup"><span data-stu-id="d0a5b-238">Currently in Public Preview See [scheduledevents](scheduled-events.md)</span></span>

## <a name="example-scenarios-for-usage"></a><span data-ttu-id="d0a5b-239">Przykładowe scenariusze użycia</span><span class="sxs-lookup"><span data-stu-id="d0a5b-239">Example scenarios for usage</span></span>  

### <a name="tracking-vm-running-on-azure"></a><span data-ttu-id="d0a5b-240">Śledzenie maszyn wirtualnych działających na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="d0a5b-240">Tracking VM running on Azure</span></span>

<span data-ttu-id="d0a5b-241">Jako dostawcę usług może wymagać śledzić liczbę maszyn wirtualnych z oprogramowaniem lub agentami, którzy muszą śledzić unikatowości maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="d0a5b-241">As a service provider, you may require to track the number of VMs running your software or have agents that need to track uniqueness of the VM.</span></span> <span data-ttu-id="d0a5b-242">Aby można było pobrać Unikatowy identyfikator dla maszyny Wirtualnej, użyj `vmId` pola wystąpienia metadanych usługi.</span><span class="sxs-lookup"><span data-stu-id="d0a5b-242">To be able to get a unique ID for a VM, use the `vmId` field from Instance Metadata Service.</span></span>

<span data-ttu-id="d0a5b-243">**Żądanie**</span><span class="sxs-lookup"><span data-stu-id="d0a5b-243">**Request**</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/compute/vmId?api-version=2017-04-02&format=text"
```

<span data-ttu-id="d0a5b-244">**Odpowiedź**</span><span class="sxs-lookup"><span data-stu-id="d0a5b-244">**Response**</span></span>

```
5c08b38e-4d57-4c23-ac45-aca61037f084
```

### <a name="placement-of-containers-data-partitions-based-faultupdate-domain"></a><span data-ttu-id="d0a5b-245">Umieszczania kontenery, partycje danych na podstawie domen błędów lub zaktualizowania</span><span class="sxs-lookup"><span data-stu-id="d0a5b-245">Placement of containers, data-partitions based fault/update domain</span></span> 

<span data-ttu-id="d0a5b-246">Dla niektórych scenariuszy, umieszczania repliki danych różnych znaczenie ma.</span><span class="sxs-lookup"><span data-stu-id="d0a5b-246">For certain scenarios, placement of different data replicas is of prime importance.</span></span> <span data-ttu-id="d0a5b-247">Na przykład [umieszczania repliki systemu plików HDFS](https://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/HdfsDesign.html#Replica_Placement:_The_First_Baby_Steps) lub położenia kontenera za pomocą [orchestrator](https://kubernetes.io/docs/user-guide/node-selection/) może wymagać wiedzieć `platformFaultDomain` i `platformUpdateDomain` maszyna wirtualna jest uruchomiona na.</span><span class="sxs-lookup"><span data-stu-id="d0a5b-247">For example, [HDFS replica placement](https://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/HdfsDesign.html#Replica_Placement:_The_First_Baby_Steps) or container placement via an [orchestrator](https://kubernetes.io/docs/user-guide/node-selection/) may you require to know the `platformFaultDomain` and `platformUpdateDomain` the VM is running on.</span></span>
<span data-ttu-id="d0a5b-248">Umożliwia wysyłanie zapytań tych danych bezpośrednio za pomocą wystąpienia usługi metadanych.</span><span class="sxs-lookup"><span data-stu-id="d0a5b-248">You can query this data directly via the Instance Metadata Service.</span></span>

<span data-ttu-id="d0a5b-249">**Żądanie**</span><span class="sxs-lookup"><span data-stu-id="d0a5b-249">**Request**</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/compute/platformFaultDomain?api-version=2017-04-02&format=text" 
```

<span data-ttu-id="d0a5b-250">**Odpowiedź**</span><span class="sxs-lookup"><span data-stu-id="d0a5b-250">**Response**</span></span>

```
0
```

### <a name="getting-more-information-about-the-vm-during-support-case"></a><span data-ttu-id="d0a5b-251">Więcej informacji na temat maszyny Wirtualnej podczas do sprawę pomocy technicznej</span><span class="sxs-lookup"><span data-stu-id="d0a5b-251">Getting more information about the VM during support case</span></span> 

<span data-ttu-id="d0a5b-252">Jako dostawcę usług mogą wystąpić pomocy technicznej gdzie chcesz dowiedzieć się więcej informacji na temat maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="d0a5b-252">As a service provider, you may get a support call where you would like to know more information about the VM.</span></span> <span data-ttu-id="d0a5b-253">Pytania klientów do udostępniania metadanych obliczeń zapewnia podstawowe informacje o pomocy technicznej wiedzieć o rodzaju maszyny Wirtualnej na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="d0a5b-253">Asking the customer to share the compute metadata can provide basic information for the support professional to know about the kind of VM on Azure.</span></span> 

<span data-ttu-id="d0a5b-254">**Żądanie**</span><span class="sxs-lookup"><span data-stu-id="d0a5b-254">**Request**</span></span>

```
curl -H Metadata:true "http://169.254.169.254/metadata/instance/compute?api-version=2017-04-02"
```

<span data-ttu-id="d0a5b-255">**Odpowiedź**</span><span class="sxs-lookup"><span data-stu-id="d0a5b-255">**Response**</span></span>

> [!NOTE] 
> <span data-ttu-id="d0a5b-256">Odpowiedź jest ciągu JSON.</span><span class="sxs-lookup"><span data-stu-id="d0a5b-256">The response is a JSON string.</span></span> <span data-ttu-id="d0a5b-257">Następujący przykład odpowiedzi jest drukowany pretty dla czytelności.</span><span class="sxs-lookup"><span data-stu-id="d0a5b-257">The following example response is pretty-printed for readability.</span></span>

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

### <a name="examples-of-calling-metadata-service-using-different-languages-inside-the-vm"></a><span data-ttu-id="d0a5b-258">Przykłady wywoływania usługi metadanych przy użyciu różnych języków, w ramach maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="d0a5b-258">Examples of calling metadata service using different languages inside the VM</span></span> 

<span data-ttu-id="d0a5b-259">Język</span><span class="sxs-lookup"><span data-stu-id="d0a5b-259">Language</span></span> | <span data-ttu-id="d0a5b-260">Przykład</span><span class="sxs-lookup"><span data-stu-id="d0a5b-260">Example</span></span> 
---------|----------------
<span data-ttu-id="d0a5b-261">Ruby</span><span class="sxs-lookup"><span data-stu-id="d0a5b-261">Ruby</span></span>     | <span data-ttu-id="d0a5b-262">https://github.com/Microsoft/azureimds/blob/Master/IMDSSample.RB</span><span class="sxs-lookup"><span data-stu-id="d0a5b-262">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.rb</span></span>
<span data-ttu-id="d0a5b-263">Przejdź do sieci Lan</span><span class="sxs-lookup"><span data-stu-id="d0a5b-263">Go Lan</span></span>   | <span data-ttu-id="d0a5b-264">https://github.com/Microsoft/azureimds/blob/Master/imdssample.go</span><span class="sxs-lookup"><span data-stu-id="d0a5b-264">https://github.com/Microsoft/azureimds/blob/master/imdssample.go</span></span>            
<span data-ttu-id="d0a5b-265">python</span><span class="sxs-lookup"><span data-stu-id="d0a5b-265">python</span></span>   | <span data-ttu-id="d0a5b-266">https://github.com/Microsoft/azureimds/blob/Master/IMDSSample.PY</span><span class="sxs-lookup"><span data-stu-id="d0a5b-266">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.py</span></span>
<span data-ttu-id="d0a5b-267">C++</span><span class="sxs-lookup"><span data-stu-id="d0a5b-267">C++</span></span>      | <span data-ttu-id="d0a5b-268">https://github.com/Microsoft/azureimds/blob/Master/IMDSSample-Windows.cpp</span><span class="sxs-lookup"><span data-stu-id="d0a5b-268">https://github.com/Microsoft/azureimds/blob/master/IMDSSample-windows.cpp</span></span>
<span data-ttu-id="d0a5b-269">C#</span><span class="sxs-lookup"><span data-stu-id="d0a5b-269">C#</span></span>       | <span data-ttu-id="d0a5b-270">https://github.com/Microsoft/azureimds/blob/Master/IMDSSample.CS</span><span class="sxs-lookup"><span data-stu-id="d0a5b-270">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.cs</span></span>
<span data-ttu-id="d0a5b-271">Javascript</span><span class="sxs-lookup"><span data-stu-id="d0a5b-271">Javascript</span></span> | <span data-ttu-id="d0a5b-272">https://github.com/Microsoft/azureimds/blob/Master/IMDSSample.js</span><span class="sxs-lookup"><span data-stu-id="d0a5b-272">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.js</span></span>
<span data-ttu-id="d0a5b-273">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d0a5b-273">Powershell</span></span> | <span data-ttu-id="d0a5b-274">https://github.com/Microsoft/azureimds/blob/Master/IMDSSample.ps1</span><span class="sxs-lookup"><span data-stu-id="d0a5b-274">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.ps1</span></span>
<span data-ttu-id="d0a5b-275">Bash</span><span class="sxs-lookup"><span data-stu-id="d0a5b-275">Bash</span></span>       | <span data-ttu-id="d0a5b-276">https://github.com/Microsoft/azureimds/blob/Master/IMDSSample.sh</span><span class="sxs-lookup"><span data-stu-id="d0a5b-276">https://github.com/Microsoft/azureimds/blob/master/IMDSSample.sh</span></span>
    

## <a name="faq"></a><span data-ttu-id="d0a5b-277">Często zadawane pytania</span><span class="sxs-lookup"><span data-stu-id="d0a5b-277">FAQ</span></span>
1. <span data-ttu-id="d0a5b-278">Pojawia się błąd `400 Bad Request, Required metadata header not specified`.</span><span class="sxs-lookup"><span data-stu-id="d0a5b-278">I am getting the error `400 Bad Request, Required metadata header not specified`.</span></span> <span data-ttu-id="d0a5b-279">Co to znaczy?</span><span class="sxs-lookup"><span data-stu-id="d0a5b-279">What does this mean?</span></span>
   * <span data-ttu-id="d0a5b-280">Wystąpienie usługi metadanych wymaga nagłówka `Metadata: true` , należy przesłać żądanie.</span><span class="sxs-lookup"><span data-stu-id="d0a5b-280">The Instance Metadata Service requires the header `Metadata: true` to be passed in the request.</span></span> <span data-ttu-id="d0a5b-281">Przekazywanie tego nagłówka w wywołaniu REST umożliwia dostęp do wystąpienia usługi metadanych.</span><span class="sxs-lookup"><span data-stu-id="d0a5b-281">Passing this header in the REST call allows access to the Instance Metadata Service.</span></span> 
2. <span data-ttu-id="d0a5b-282">Dlaczego nie występują obliczeniowe informacji Moje maszyny wirtualnej?</span><span class="sxs-lookup"><span data-stu-id="d0a5b-282">Why am I not getting compute information for my VM?</span></span>
   * <span data-ttu-id="d0a5b-283">Obecnie usługa metadanych wystąpienie obsługuje tylko wystąpienia utworzone za pomocą Menedżera zasobów Azure.</span><span class="sxs-lookup"><span data-stu-id="d0a5b-283">Currently the Instance Metadata Service only supports instances created with Azure Resource Manager.</span></span> <span data-ttu-id="d0a5b-284">Firma Microsoft może w przyszłości, Dodaj obsługę maszyn wirtualnych usługi w chmurze.</span><span class="sxs-lookup"><span data-stu-id="d0a5b-284">In the future, we may add support for Cloud Service VMs.</span></span>
3. <span data-ttu-id="d0a5b-285">Napisany wcześniej utworzony Moje maszyny wirtualnej za pomocą usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="d0a5b-285">I created my Virtual Machine through Azure Resource Manager a while back.</span></span> <span data-ttu-id="d0a5b-286">Dlaczego mam nie zawiera compute metadane?</span><span class="sxs-lookup"><span data-stu-id="d0a5b-286">Why am I not see compute metadata information?</span></span>
   * <span data-ttu-id="d0a5b-287">Wszystkie maszyny wirtualne utworzone po wrz 2016, można dodać [Tag](../../azure-resource-manager/resource-group-using-tags.md) aby zacząć wyświetlać obliczeniowe metadanych.</span><span class="sxs-lookup"><span data-stu-id="d0a5b-287">For any VMs created after Sep 2016, add a [Tag](../../azure-resource-manager/resource-group-using-tags.md) to start seeing compute metadata.</span></span> <span data-ttu-id="d0a5b-288">Dla starszych maszyn wirtualnych (utworzone przed 2016 wrz) Dodaj/Usuń rozszerzenia lub danych dysków do maszyny Wirtualnej, aby odświeżyć metadane.</span><span class="sxs-lookup"><span data-stu-id="d0a5b-288">For older VMs (created before Sep 2016), add/remove extensions or data disks to the VM to refresh metadata.</span></span>
4. <span data-ttu-id="d0a5b-289">Dlaczego otrzymuję błąd `500 Internal Server Error`?</span><span class="sxs-lookup"><span data-stu-id="d0a5b-289">Why am I getting the error `500 Internal Server Error`?</span></span>
   * <span data-ttu-id="d0a5b-290">Ponów żądanie w oparciu wykładniczego wycofywania systemu.</span><span class="sxs-lookup"><span data-stu-id="d0a5b-290">Please retry your request based on exponential back off system.</span></span> <span data-ttu-id="d0a5b-291">Jeśli problem będzie się powtarzał skontaktuj się z pomocą techniczną platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="d0a5b-291">If the issue persists contact  Azure support.</span></span>
5. <span data-ttu-id="d0a5b-292">Gdzie udostępniać dodatkowe pytania/komentarze?</span><span class="sxs-lookup"><span data-stu-id="d0a5b-292">Where do I share additional questions/comments?</span></span>
   * <span data-ttu-id="d0a5b-293">Wyślij komentarze dotyczące http://feedback.azure.com.</span><span class="sxs-lookup"><span data-stu-id="d0a5b-293">Send your comments on http://feedback.azure.com.</span></span>
7. <span data-ttu-id="d0a5b-294">Czy to pomoże dla wystąpienia ustawić skali maszyny wirtualnej?</span><span class="sxs-lookup"><span data-stu-id="d0a5b-294">Would this work for Virtual Machine Scale Set Instance?</span></span>
   * <span data-ttu-id="d0a5b-295">Tak, usługa metadanych jest dostępna dla wystąpień ustawić skali.</span><span class="sxs-lookup"><span data-stu-id="d0a5b-295">Yes Metadata service is available for Scale Set Instances.</span></span> 
6. <span data-ttu-id="d0a5b-296">Jak uzyskać pomoc techniczną dla usługi?</span><span class="sxs-lookup"><span data-stu-id="d0a5b-296">How do I get support for the service?</span></span>
   * <span data-ttu-id="d0a5b-297">Aby uzyskać pomoc techniczną dla usługi, utworzyć problem pomocy technicznej w portalu Azure dla maszyny Wirtualnej, gdy nie jest możliwe uzyskanie odpowiedzi metadanych mimo ponownych prób długa</span><span class="sxs-lookup"><span data-stu-id="d0a5b-297">To get support for the service, create a support issue in Azure portal for the VM where you are not able to get metadata response after long retries</span></span> 

   ![Obsługa metadanych wystąpienia](./media/instance-metadata-service/InstanceMetadata-support.png)
    
## <a name="next-steps"></a><span data-ttu-id="d0a5b-299">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d0a5b-299">Next steps</span></span>

- <span data-ttu-id="d0a5b-300">Dowiedz się więcej o [zaplanowane zdarzenia](scheduled-events.md) interfejsu API **w publicznej wersji zapoznawczej** udostępniony przez usługę wystąpienie metadanych.</span><span class="sxs-lookup"><span data-stu-id="d0a5b-300">Learn more about the [Scheduled Events](scheduled-events.md) API **in public preview** provided by the Instance Metadata service.</span></span>
