## <a name="azure-dns"></a><span data-ttu-id="88884-101">System DNS platformy Azure</span><span class="sxs-lookup"><span data-stu-id="88884-101">Azure DNS</span></span>
<span data-ttu-id="88884-102">Usługa DNS platformy Azure to Usługa hostingu domen DNS, rozpoznawania nazw przy użyciu infrastruktury Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="88884-102">Azure DNS is a hosting service for DNS domains, providing name resolution using Microsoft Azure infrastructure.</span></span>

| <span data-ttu-id="88884-103">Właściwość</span><span class="sxs-lookup"><span data-stu-id="88884-103">Property</span></span> | <span data-ttu-id="88884-104">Opis</span><span class="sxs-lookup"><span data-stu-id="88884-104">Description</span></span> | <span data-ttu-id="88884-105">Przykładowa wartość</span><span class="sxs-lookup"><span data-stu-id="88884-105">Sample Value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="88884-106">**DNSzones**</span><span class="sxs-lookup"><span data-stu-id="88884-106">**DNSzones**</span></span> |<span data-ttu-id="88884-107">Rekordy DNS domeny strefy informacji toohost z określonej domeny</span><span class="sxs-lookup"><span data-stu-id="88884-107">Domain zone information toohost DNS records of a particular domain</span></span> |<span data-ttu-id="88884-108">/ subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com "</span><span class="sxs-lookup"><span data-stu-id="88884-108">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com"</span></span> |

### <a name="dns-record-sets"></a><span data-ttu-id="88884-109">Zestawy rekordów DNS</span><span class="sxs-lookup"><span data-stu-id="88884-109">DNS record sets</span></span>
<span data-ttu-id="88884-110">Strefy DNS mieć obiektu podrzędnego o nazwie zestaw rekordów.</span><span class="sxs-lookup"><span data-stu-id="88884-110">DNS zones have a child object named record set.</span></span> <span data-ttu-id="88884-111">Zestawy rekordów jest kolekcją rekordów hosta przez typ strefy DNS.</span><span class="sxs-lookup"><span data-stu-id="88884-111">Record sets are a collection of host records by type for a DNS zone.</span></span> <span data-ttu-id="88884-112">Typy rekordów są A, AAAA, CNAME, MX, NS, SOA, SRV i TXT.</span><span class="sxs-lookup"><span data-stu-id="88884-112">Record types are A, AAAA, CNAME, MX, NS, SOA,SRV and TXT.</span></span>

| <span data-ttu-id="88884-113">Właściwość</span><span class="sxs-lookup"><span data-stu-id="88884-113">Property</span></span> | <span data-ttu-id="88884-114">Opis</span><span class="sxs-lookup"><span data-stu-id="88884-114">Description</span></span> | <span data-ttu-id="88884-115">Wartość przykładowa</span><span class="sxs-lookup"><span data-stu-id="88884-115">Sample value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="88884-116">A</span><span class="sxs-lookup"><span data-stu-id="88884-116">A</span></span> |<span data-ttu-id="88884-117">Typ rekordu IPv4</span><span class="sxs-lookup"><span data-stu-id="88884-117">IPv4 record type</span></span> |<span data-ttu-id="88884-118">/Subscriptions/{GUID}/.../Providers/Microsoft.Network/dnszones/contoso.com/A/www</span><span class="sxs-lookup"><span data-stu-id="88884-118">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/A/www</span></span> |
| <span data-ttu-id="88884-119">AAAA</span><span class="sxs-lookup"><span data-stu-id="88884-119">AAAA</span></span> |<span data-ttu-id="88884-120">Typ rekordu IPv6</span><span class="sxs-lookup"><span data-stu-id="88884-120">IPv6 record type</span></span> |<span data-ttu-id="88884-121">/Subscriptions/{GUID}/.../Providers/Microsoft.Network/dnszones/contoso.com/AAAA/hostrecord</span><span class="sxs-lookup"><span data-stu-id="88884-121">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/AAAA/hostrecord</span></span> |
| <span data-ttu-id="88884-122">CNAME</span><span class="sxs-lookup"><span data-stu-id="88884-122">CNAME</span></span> |<span data-ttu-id="88884-123">Nazwa kanoniczna typu rekordu <sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="88884-123">canonical name record type <sup>1</sup></span></span> |<span data-ttu-id="88884-124">/Subscriptions/{GUID}/.../Providers/Microsoft.Network/dnszones/contoso.com/CNAME/www</span><span class="sxs-lookup"><span data-stu-id="88884-124">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/CNAME/www</span></span> |
| <span data-ttu-id="88884-125">MX</span><span class="sxs-lookup"><span data-stu-id="88884-125">MX</span></span> |<span data-ttu-id="88884-126">Typ rekordu poczty</span><span class="sxs-lookup"><span data-stu-id="88884-126">mail record type</span></span> |<span data-ttu-id="88884-127">/Subscriptions/{GUID}/.../Providers/Microsoft.Network/dnszones/contoso.com/MX/mail</span><span class="sxs-lookup"><span data-stu-id="88884-127">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/MX/mail</span></span> |
| <span data-ttu-id="88884-128">NS</span><span class="sxs-lookup"><span data-stu-id="88884-128">NS</span></span> |<span data-ttu-id="88884-129">Typ rekordu nazwy serwera</span><span class="sxs-lookup"><span data-stu-id="88884-129">name server record type</span></span> |<span data-ttu-id="88884-130">/Subscriptions/{GUID}/.../Providers/Microsoft.Network/dnszones/contoso.com/NS/</span><span class="sxs-lookup"><span data-stu-id="88884-130">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/NS/</span></span> |
| <span data-ttu-id="88884-131">SOA</span><span class="sxs-lookup"><span data-stu-id="88884-131">SOA</span></span> |<span data-ttu-id="88884-132">Początek typ rekordu urząd <sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="88884-132">Start of Authority record type <sup>2</sup></span></span> |<span data-ttu-id="88884-133">/Subscriptions/{GUID}/.../Providers/Microsoft.Network/dnszones/contoso.com/SOA</span><span class="sxs-lookup"><span data-stu-id="88884-133">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/SOA</span></span> |
| <span data-ttu-id="88884-134">SRV</span><span class="sxs-lookup"><span data-stu-id="88884-134">SRV</span></span> |<span data-ttu-id="88884-135">Typ rekordu usługi</span><span class="sxs-lookup"><span data-stu-id="88884-135">service record type</span></span> |<span data-ttu-id="88884-136">/Subscriptions/{GUID}/.../Providers/Microsoft.Network/dnszones/contoso.com/SRV</span><span class="sxs-lookup"><span data-stu-id="88884-136">/subscriptions/{guid}/.../providers/Microsoft.Network/dnszones/contoso.com/SRV</span></span> |

<span data-ttu-id="88884-137"><sup>1</sup> zezwala na tylko jedną wartość na zestawie rekordów.</span><span class="sxs-lookup"><span data-stu-id="88884-137"><sup>1</sup> only allows one value per record set.</span></span>

<span data-ttu-id="88884-138"><sup>2</sup> zezwala na tylko jeden typ rekordów SOA dla stref DNS.</span><span class="sxs-lookup"><span data-stu-id="88884-138"><sup>2</sup> only allows one record type SOA per DNS zone.</span></span> 

<span data-ttu-id="88884-139">Przykład strefy DNS w formacie Json:</span><span class="sxs-lookup"><span data-stu-id="88884-139">Sample of DNS zone in Json format:</span></span>

    {
      "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "newZoneName": {
          "type": "String",
          "metadata": {
              "description": "hello name of hello DNS zone toobe created."
          }
        },
        "newRecordName": {
          "type": "String",
          "defaultValue": "www",
          "metadata": {
              "description": "hello name of hello DNS record toobe created.  hello name is relative toohello zone, not hello FQDN."
          }
        }
      },
      "resources": 
      [
        {
          "type": "microsoft.network/dnszones",
          "name": "[parameters('newZoneName')]",
          "apiVersion": "2015-05-04-preview",
          "location": "global",
          "properties": {
          }
        },
        {
          "type": "microsoft.network/dnszones/a",
          "name": "[concat(parameters('newZoneName'), concat('/', parameters('newRecordName')))]",
          "apiVersion": "2015-05-04-preview",
          "location": "global",
          "properties": 
          {
            "TTL": 3600,
            "ARecords": 
            [
                {
                    "ipv4Address": "1.2.3.4"
                },
                {
                    "ipv4Address": "1.2.3.5"
                }
            ]
          },
          "dependsOn": [
            "[concat('Microsoft.Network/dnszones/', parameters('newZoneName'))]"
          ]
        }
          ]
    }

## <a name="additional-resources"></a><span data-ttu-id="88884-140">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="88884-140">Additional resources</span></span>
<span data-ttu-id="88884-141">Witaj odczytu [dokumentacja interfejsu API REST dla stref DNS ](https://msdn.microsoft.com/library/azure/mt130626.aspx) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="88884-141">Read hello [REST API documentation for DNS zones ](https://msdn.microsoft.com/library/azure/mt130626.aspx) for more information.</span></span>

<span data-ttu-id="88884-142">Witaj odczytu [dokumentacja interfejsu API REST dla zestawów rekordów DNS](https://msdn.microsoft.com/library/azure/mt130627.aspx) Aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="88884-142">Read hello [REST API documentation for DNS record sets](https://msdn.microsoft.com/library/azure/mt130627.aspx) for more information.</span></span>

