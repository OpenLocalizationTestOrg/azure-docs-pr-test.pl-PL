---
title: "Przewodnik dotyczący tworzenia usługi danych dla witryny Marketplace | Dokumentacja firmy Microsoft"
description: "Szczegółowe instrukcje dotyczące sposobu tworzenia, certyfikować i wdrażania usługi danych dla kupić w witrynie Azure Marketplace."
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: 148f8638-ee80-4100-8d63-5afa4167ca1b
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/26/2016
ms.author: hascipio; avikova
ms.openlocfilehash: 2ab624941fc385f14b62bb5d743927f157955845
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="examples-of-mapping-an-existing-web-service-to-odata-through-csdls"></a><span data-ttu-id="3f4de-103">Przykładowe mapowanie istniejącej usługi sieci web OData za pomocą CSDLs</span><span class="sxs-lookup"><span data-stu-id="3f4de-103">Examples of mapping an existing web service to OData through CSDLs</span></span>
> [!IMPORTANT]
> <span data-ttu-id="3f4de-104">**W tym momencie firma Microsoft nie są już dołączania żadnych nowych wydawców danych usługi. Nowe dataservices nie zostanie zatwierdzenia dla listy.**</span><span class="sxs-lookup"><span data-stu-id="3f4de-104">**At this time we are no longer onboarding any new Data Service publishers. New dataservices will not get approved for listing.**</span></span> <span data-ttu-id="3f4de-105">Jeśli masz aplikacji biznesowych SaaS chcesz publikować w AppSource więcej informacji można znaleźć [tutaj](https://appsource.microsoft.com/partners).</span><span class="sxs-lookup"><span data-stu-id="3f4de-105">If you have a SaaS business application you would like to publish on AppSource you can find more information [here](https://appsource.microsoft.com/partners).</span></span> <span data-ttu-id="3f4de-106">Jeśli masz aplikacje IaaS lub więcej informacji można znaleźć usługi developer chcesz publikować w witrynie Azure Marketplace [tutaj](https://azure.microsoft.com/marketplace/programs/certified/).</span><span class="sxs-lookup"><span data-stu-id="3f4de-106">If you have an IaaS applications or developer service you would like to publish on Azure Marketplace you can find more information [here](https://azure.microsoft.com/marketplace/programs/certified/).</span></span>
> 
> 

## <a name="example-functionimport-for-raw-data-returned-using-post"></a><span data-ttu-id="3f4de-107">Przykład: FunctionImport "Raw" danych zwracane przy użyciu "POST"</span><span class="sxs-lookup"><span data-stu-id="3f4de-107">Example: FunctionImport for "Raw" data returned using "POST"</span></span>
<span data-ttu-id="3f4de-108">Użyj POST nieprzetworzone dane, aby utworzyć nowy podrzędny i zwraca jego serwerem zdefiniowane przez URL(location) lub zaktualizować część podrzędnym na serwerze adresu URL.</span><span class="sxs-lookup"><span data-stu-id="3f4de-108">Use POST Raw data to create a new subordinate and return its server defined URL(location) or to update part of the subordinate at the server defined URL.</span></span>  <span data-ttu-id="3f4de-109">Gdzie podrzędnym jest typu stream, tj.</span><span class="sxs-lookup"><span data-stu-id="3f4de-109">Where the subordinate is a stream, i.e.</span></span> <span data-ttu-id="3f4de-110">bez struktury, np.</span><span class="sxs-lookup"><span data-stu-id="3f4de-110">unstructured, ex.</span></span> <span data-ttu-id="3f4de-111">plik tekstowy.</span><span class="sxs-lookup"><span data-stu-id="3f4de-111">a text file.</span></span>  <span data-ttu-id="3f4de-112">Uważaj POST w nie idempotentności bez lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="3f4de-112">Beware POST in not idempotent without a location.</span></span>

        <!--  No EntitySet or EntityType nodes required for Raw output-->
        <FunctionImport Name="AddUsageEvent" ReturnType="Raw(text/plain)" d:EncodeParameterValues="true" d:AllowedHttpMethods="POST" d:BaseUri="http://services.organization.net/MyServicePath?name={name}&amp;AccountKey=22AC643">
        <d:Title d:Map="" />
        <d:Rights d:Map="" />
        <d:Description>Add usage event (data acquisition)</d:Description>
        <d:Headers>
        <d:Header d:Name="Content-Type" d:Value="application/xml;charset=UTF-8" />
        </d:Headers>
        <Parameter Name="name" Nullable="false" Mode="In" Type="String" d:Description="first name" d:SampleValues="John|Joe|Bill"  d:EncodeParameterValue="true" />
        <d:Namespaces>
        <d:Namespace d:Prefix="p" d:Uri="http://schemas.organization.net/2010/04/myNamespace " />
        <d:Namespace d:Prefix="p2" d:Uri=" http://schemas.organization.net/2010/04/myNamespace2 " />
        </d:Namespaces>
        </FunctionImport>

## <a name="example-functionimport-using-delete"></a><span data-ttu-id="3f4de-113">Przykład: FunctionImport przy użyciu "DELETE"</span><span class="sxs-lookup"><span data-stu-id="3f4de-113">Example: FunctionImport using "DELETE"</span></span>
<span data-ttu-id="3f4de-114">Usuń umożliwia usunięcie określonego identyfikatora URI.</span><span class="sxs-lookup"><span data-stu-id="3f4de-114">Use DELETE to remove a specified URI.</span></span>

        <EntitySet Name="DeleteUsageFileEntitySet" EntityType="MyOffer.DeleteUsageFileEntity" />
        <FunctionImport Name="DeleteUsageFile" EntitySet="DeleteUsageFileEntitySet" ReturnType="Collection(MyOffer.DeleteUsageFileEntity)"  d:AllowedHttpMethods="DELETE" d:EncodeParameterValues="true” d:BaseUri=”http://services.organization.net/MyServicePath?name={name}&amp;AccountKey=22AC643" >
        <d:Title d:Map="" />
        <d:Rights d:Map="" />
        <d:Description>Delete usage File</d:Description>
        <d:Headers>
        <d:Header d:Name="Content-Type" d:Value="application/xml;charset=UTF-8" />
        </d:Headers>
        <Parameter Name="name" Nullable="false" Mode="In" Type="String" d:Description="first name" d:SampleValues="John|Joe|Bill"  d:EncodeParameterValue="true" />
        <d:Namespaces>
        <d:Namespace d:Prefix="p" d:Uri="http://schemas.organization.net/2010/04/myNamespace " />
        <d:Namespace d:Prefix="p2" d:Uri=" http://schemas.organization.net/2010/04/myNamespace2 " />
        </d:Namespaces>
        </FunctionImport>
        <EntityType Name="DeleteUsageFileEntity" d:Map="//boolean">
        <Property Name="boolean" Type="String" Nullable="true" d:Map="./boolean" />
        </EntityType>

## <a name="example-functionimport-using-post"></a><span data-ttu-id="3f4de-115">Przykład: FunctionImport przy użyciu "POST"</span><span class="sxs-lookup"><span data-stu-id="3f4de-115">Example: FunctionImport using "POST"</span></span>
<span data-ttu-id="3f4de-116">Użyj POST nieprzetworzone dane, aby utworzyć nowy podrzędny i zwraca jego serwerem zdefiniowane przez URL(location) lub zaktualizować część podrzędnym na serwerze adresu URL.</span><span class="sxs-lookup"><span data-stu-id="3f4de-116">Use POST Raw data to create a new subordinate and return its server defined URL(location) or to update part of the subordinate at the server defined URL.</span></span>  <span data-ttu-id="3f4de-117">Gdzie podrzędnym jest strukturą.</span><span class="sxs-lookup"><span data-stu-id="3f4de-117">Where the subordinate is a structure.</span></span> <span data-ttu-id="3f4de-118">Uważaj POST nie jest idempotentności bez lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="3f4de-118">Beware POST is not idempotent without a location.</span></span>

        <EntitySet Name="CreateANewModelEntitySet2" EntityType=" MyOffer.CreateANewModelEntity2" />
        <FunctionImport Name="CreateModel" EntitySet="CreateANewModelEntitySet2" ReturnType="Collection(MyOffer.CreateANewModelEntity2)" d:EncodeParameterValues="true" d:AllowedHttpMethods="POST" d:BaseUri=”http://services.organization.net/MyServicePath?name={name}&amp;AccountKey=22AC643">
        <d:Title d:Map="" />
        <d:Rights d:Map="" />
        <d:Description>Create A New Model</d:Description>
        <d:Headers>
        <d:Header d:Name="Content-Type" d:Value="application/xml;charset=UTF-8" />
        </d:Headers>
        <Parameter name="name" Nullable="false" Mode="In" Type="String" d:Description="first name" d:SampleValues="John|Joe|Bill"  d:EncodeParameterValue="true" />
        <d:Namespaces>
        <d:Namespace d:Prefix="p" d:Uri="http://schemas.organization.net/2010/04/myNamespace " />
        <d:Namespace d:Prefix="p2" d:Uri=" http://schemas.organization.net/2010/04/myNamespace2 " />
        </d:Namespaces>
        </FunctionImport>

## <a name="example-functionimport-using-put"></a><span data-ttu-id="3f4de-119">Przykład: FunctionImport przy użyciu "PUT"</span><span class="sxs-lookup"><span data-stu-id="3f4de-119">Example: FunctionImport using "PUT"</span></span>
<span data-ttu-id="3f4de-120">Aby utworzyć nowy podrzędny lub zaktualizować cały podrzędnym pod adresem URL zdefiniowanego serwera, należy użyć PUT.</span><span class="sxs-lookup"><span data-stu-id="3f4de-120">Use PUT to create a new subordinate or to update the entire subordinate at a server defined URL.</span></span>  <span data-ttu-id="3f4de-121">W przypadku, gdy podrzędnym jest strukturą, PUT jest idempotentności tak wielu wystąpień spowodują samym stanie, tj</span><span class="sxs-lookup"><span data-stu-id="3f4de-121">Where the subordinate is a structure, PUT is idempotent so multiple occurrences will result in the same state, i.e</span></span> <span data-ttu-id="3f4de-122">x = 5.</span><span class="sxs-lookup"><span data-stu-id="3f4de-122">x=5.</span></span>  <span data-ttu-id="3f4de-123">Umieść powinien być używany z pełnej zawartości określonego zasobu.</span><span class="sxs-lookup"><span data-stu-id="3f4de-123">Put should be used with the full content of the specified resource.</span></span>

        <EntitySet Name="UpdateAnExistingModelEntitySet" EntityType="MyOffer.UpdateAnExistingModelEntity" />
        <FunctionImport Name="UpdateModel" EntitySet="UpdateAnExistingModelEntitySet" ReturnType="Collection(MyOffer.UpdateAnExistingModelEntity)" d:EncodeParameterValues="true" d:AllowedHttpMethods="PUT" d:BaseUri=”http://services.organization.net/MyServicePath?name={name}&amp;AccountKey=22AC643">
        <d:Title d:Map="" />
        <d:Rights d:Map="" />
        <d:Description>Update an Existing Model</d:Description>
        <d:Headers>
        <d:Header d:Name="Content-Type" d:Value="application/xml;charset=UTF-8" />
        </d:Headers>
        <Parameter Name="name" Nullable="false" Mode="In" Type="String" d:Description="first name" d:SampleValues="John|Joe|Bill"  d:EncodeParameterValue="true" />
        <d:Namespaces>
        <d:Namespace d:Prefix="p" d:Uri="http://schemas.organization.net/2010/04/myNamespace " />
        <d:Namespace d:Prefix="p2" d:Uri=" http://schemas.organization.net/2010/04/myNamespace2 " />
        </d:Namespaces>
        </FunctionImport>
        <EntityType Name="UpdateAnExistingModelEntity" d:Map="//string">
        <Property Name="string"     Type="String" Nullable="true" d:Map="./string" />
        </EntityType>


## <a name="example-functionimport-for-raw-data-returned-using-put"></a><span data-ttu-id="3f4de-124">Przykład: FunctionImport "Raw" danych zwracane przy użyciu "PUT"</span><span class="sxs-lookup"><span data-stu-id="3f4de-124">Example: FunctionImport for "Raw" data returned using "PUT"</span></span>
<span data-ttu-id="3f4de-125">Użyj PUT nieprzetworzone dane, aby utworzyć nowy podrzędny lub zaktualizować cały podrzędnym pod adresem URL zdefiniowanego serwera.</span><span class="sxs-lookup"><span data-stu-id="3f4de-125">Use PUT Raw data to create a new subordinate or to update the entire subordinate at a server defined URL.</span></span>  <span data-ttu-id="3f4de-126">Gdzie podrzędnym jest typu stream, tj.</span><span class="sxs-lookup"><span data-stu-id="3f4de-126">Where the subordinate is a stream, i.e.</span></span> <span data-ttu-id="3f4de-127">bez struktury, np.</span><span class="sxs-lookup"><span data-stu-id="3f4de-127">unstructured, ex.</span></span> <span data-ttu-id="3f4de-128">plik tekstowy.</span><span class="sxs-lookup"><span data-stu-id="3f4de-128">a text file.</span></span>  <span data-ttu-id="3f4de-129">PUT jest idempotentności tak wielu wystąpień spowodują samym stanie, tj</span><span class="sxs-lookup"><span data-stu-id="3f4de-129">PUT is idempotent so multiple occurrences will result in the same state, i.e</span></span> <span data-ttu-id="3f4de-130">x = 5.</span><span class="sxs-lookup"><span data-stu-id="3f4de-130">x=5.</span></span>  <span data-ttu-id="3f4de-131">Umieść powinien być używany z pełnej zawartości określonego zasobu.</span><span class="sxs-lookup"><span data-stu-id="3f4de-131">Put should be used with the full content of the specified resource.</span></span>

        <!--  No EntitySet or EntityType nodes required for Raw output-->
        <FunctionImport Name="CancelBuild” ReturnType="Raw(text/plain)" d:AllowedHttpMethods="PUT" d:EncodeParameterValues="true" d:BaseUri=” http://services.organization.net/MyServicePath?name={name}&amp;AccountKey=22AC643">
        <d:Title d:Map="" />
        <d:Rights d:Map="" />
        <d:Description>Cancel Build</d:Description>
        <d:Headers>
        <d:Header d:Name="Content-Type" d:Value="application/xml;charset=UTF-8" />
        </d:Headers>
        <Parameter Name="name" Nullable="false" Mode="In" Type="String" d:Description="first name" d:SampleValues="John|Joe|Bill"  d:EncodeParameterValue="true" />
        <d:Namespaces>
        <d:Namespace d:Prefix="p" d:Uri="http://schemas.organization.net/2010/04/myNamespace " />
        <d:Namespace d:Prefix="p2" d:Uri=" http://schemas.organization.net/2010/04/myNamespace2 " />
        </d:Namespaces>
        </FunctionImport>


## <a name="example-functionimport-for-raw-data-returned-using-get"></a><span data-ttu-id="3f4de-132">Przykład: FunctionImport "Raw" danych zwracane przy użyciu "GET"</span><span class="sxs-lookup"><span data-stu-id="3f4de-132">Example: FunctionImport for "Raw" data returned using "GET"</span></span>
<span data-ttu-id="3f4de-133">Użyj UZYSKAĆ pierwotnych danych do zwrócenia podrzędny, która nie ma określonej struktury, tj. tekst.</span><span class="sxs-lookup"><span data-stu-id="3f4de-133">Use GET Raw data to return a subordinate that is unstructured, i.e. text.</span></span>

        <!--  No EntitySet or EntityType nodes required for Raw output-->
        <FunctionImport Name="GetModelUsageFile" ReturnType="Raw(text/plain)" d:EncodeParameterValues="true" d:AllowedHttpMethods="GET" d:BaseUri="https://cmla.cloudapp.net/api2/model/builder/build?buildId={buildId}&amp;apiVersion={apiVersion}">
        <d:Title d:Map="" />
        <d:Rights d:Map="" />
        <d:Description>Download A Models Usage File</d:Description>
        <d:Headers>
        <d:Header d:Name="Accept" d:Value="application/xml,application/xhtml+xml,text/html;" />
        <d:Header d:Name="Content-Type" d:Value="application/xml;charset=UTF-8" />
        </d:Headers>
        <Parameter Name="name" Nullable="false" Mode="In" Type="String" d:Description="first name" d:SampleValues="John|Joe|Bill"  d:EncodeParameterValue="true" />
        <d:Namespaces>
        <d:Namespace d:Prefix="p" d:Uri="http://schemas.organization.net/2010/04/myNamespace " />
        <d:Namespace d:Prefix="p2" d:Uri=" http://schemas.organization.net/2010/04/myNamespace2 " />
        </d:Namespaces>
        </FunctionImport>

## <a name="example-functionimport-for-paging-through-returned-data"></a><span data-ttu-id="3f4de-134">Przykład: FunctionImport "Stronicowanie" za pośrednictwem zwrócone dane</span><span class="sxs-lookup"><span data-stu-id="3f4de-134">Example: FunctionImport for "Paging" through returned data</span></span>
<span data-ttu-id="3f4de-135">Implementowanie stronicowania RESTful za pośrednictwem danych za pomocą GET.</span><span class="sxs-lookup"><span data-stu-id="3f4de-135">Use implement RESTful paging through your data with GET.</span></span>  <span data-ttu-id="3f4de-136">Domyślne stronicowania wynosi 100 wierszy na stronie danych.</span><span class="sxs-lookup"><span data-stu-id="3f4de-136">Default paging is set to 100 row per page of data.</span></span>

        <EntitySet Name=”CropEntitySet" EntityType="MyOffer.CropEntity" />
        <FunctionImport    Name="GetCropReport" EntitySet="CropEntitySet” ReturnType="Collection(MyOffer.CropEntity)" d:EmitSelfLink="false" d:EncodeParameterValues="true" d:Paging="SkipTake" d:MaxPageSize="100" d:BaseUri="http://api.mydata.org/Crop? report={report}&amp;series={series}&amp;start={$skip}&amp;size=100">
        <Parameter Name="report" Type="Int32" Mode="In" Nullable="false" d:SampleValues="4"  d:enum="1|2|3|4|5|6|7|8|9|10|11|12|13|14|15|16|17|18|19"  />
        <Parameter Name="series"    Type="String"    Mode="In" Nullable="false" d:SampleValues="FARM" />
        <d:Headers>
        <d:Header d:Name="Content-Type" d:Value="text/xml;charset=UTF-8" />
        </d:Headers>
        <d:Namespaces>
        <d:Namespace d:Prefix="diffgr" d:Uri="urn:schemas-microsoft-com:xml-diffgram-v1" />
        </d:Namespaces>
        </FunctionImport>

## <a name="see-also"></a><span data-ttu-id="3f4de-137">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="3f4de-137">See Also</span></span>
* <span data-ttu-id="3f4de-138">Jeśli interesuje Cię zrozumieć ogólny proces mapowania OData i cel, przeczytaj ten artykuł [danych usługi OData mapowania](marketplace-publishing-data-service-creation-odata-mapping.md) Aby przejrzeć definicje, struktur i instrukcje.</span><span class="sxs-lookup"><span data-stu-id="3f4de-138">If you are interested in understanding the overall OData mapping process and purpose, read this article [Data Service OData Mapping](marketplace-publishing-data-service-creation-odata-mapping.md) to review definitions, structures, and instructions.</span></span>
* <span data-ttu-id="3f4de-139">Jeśli interesuje Cię uczenia i zrozumienie określonych węzłów i ich parametry, przeczytaj ten artykuł [węzły mapowanie danych usługi OData](marketplace-publishing-data-service-creation-odata-mapping-nodes.md) definicje i wyjaśnienia, przykłady i kontekstu przypadków użycia.</span><span class="sxs-lookup"><span data-stu-id="3f4de-139">If you are interested in learning and understanding the specific nodes and their parameters, read this article [Data Service OData Mapping Nodes](marketplace-publishing-data-service-creation-odata-mapping-nodes.md) for definitions and explanations, examples, and use case context.</span></span>
* <span data-ttu-id="3f4de-140">Aby powrócić do określonej ścieżki do publikowania danych usługi Azure Marketplace, przeczytaj ten artykuł [Podręcznik publikowania danych usługi](marketplace-publishing-data-service-creation.md).</span><span class="sxs-lookup"><span data-stu-id="3f4de-140">To return to the prescribed path for publishing a Data Service to the Azure Marketplace, read this article [Data Service Publishing Guide](marketplace-publishing-data-service-creation.md).</span></span>

