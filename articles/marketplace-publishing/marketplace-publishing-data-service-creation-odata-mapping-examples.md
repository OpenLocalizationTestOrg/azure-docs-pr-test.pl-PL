---
title: "toocreating aaaGuide usługi danych dla hello Marketplace | Dokumentacja firmy Microsoft"
description: "Szczegółowe instrukcje sposobu toocreate, certyfikować i wdrożyć usługę Data zakupu na hello Azure Marketplace."
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
ms.openlocfilehash: 8917a43959834d15f70866297f98d24bb83e217f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="examples-of-mapping-an-existing-web-service-tooodata-through-csdls"></a><span data-ttu-id="c070d-103">Przykładowe mapowanie istniejące sieci web tooOData usługi za pośrednictwem CSDLs</span><span class="sxs-lookup"><span data-stu-id="c070d-103">Examples of mapping an existing web service tooOData through CSDLs</span></span>
> [!IMPORTANT]
> <span data-ttu-id="c070d-104">**W tym momencie firma Microsoft nie są już dołączania żadnych nowych wydawców danych usługi. Nowe dataservices nie zostanie zatwierdzenia dla listy.**</span><span class="sxs-lookup"><span data-stu-id="c070d-104">**At this time we are no longer onboarding any new Data Service publishers. New dataservices will not get approved for listing.**</span></span> <span data-ttu-id="c070d-105">Jeśli masz aplikacji biznesowej SaaS chcesz toopublish na AppSource więcej informacji można znaleźć [tutaj](https://appsource.microsoft.com/partners).</span><span class="sxs-lookup"><span data-stu-id="c070d-105">If you have a SaaS business application you would like toopublish on AppSource you can find more information [here](https://appsource.microsoft.com/partners).</span></span> <span data-ttu-id="c070d-106">Jeśli masz aplikacje IaaS lub dewelopera usługi będzie jak toopublish w witrynie Azure Marketplace więcej informacji można znaleźć [tutaj](https://azure.microsoft.com/marketplace/programs/certified/).</span><span class="sxs-lookup"><span data-stu-id="c070d-106">If you have an IaaS applications or developer service you would like toopublish on Azure Marketplace you can find more information [here](https://azure.microsoft.com/marketplace/programs/certified/).</span></span>
> 
> 

## <a name="example-functionimport-for-raw-data-returned-using-post"></a><span data-ttu-id="c070d-107">Przykład: FunctionImport "Raw" danych zwracane przy użyciu "POST"</span><span class="sxs-lookup"><span data-stu-id="c070d-107">Example: FunctionImport for "Raw" data returned using "POST"</span></span>
<span data-ttu-id="c070d-108">Użyj POST nieprzetworzone dane toocreate nowy podrzędny i zwróć URL(location) zdefiniowane przez jego serwer lub tooupdate część hello na powitania serwera podrzędnego adresu URL.</span><span class="sxs-lookup"><span data-stu-id="c070d-108">Use POST Raw data toocreate a new subordinate and return its server defined URL(location) or tooupdate part of hello subordinate at hello server defined URL.</span></span>  <span data-ttu-id="c070d-109">Gdzie podrzędny hello jest typu stream, tzn. bez struktury, np.</span><span class="sxs-lookup"><span data-stu-id="c070d-109">Where hello subordinate is a stream, i.e. unstructured, ex.</span></span> <span data-ttu-id="c070d-110">plik tekstowy.</span><span class="sxs-lookup"><span data-stu-id="c070d-110">a text file.</span></span>  <span data-ttu-id="c070d-111">Uważaj POST w nie idempotentności bez lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="c070d-111">Beware POST in not idempotent without a location.</span></span>

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

## <a name="example-functionimport-using-delete"></a><span data-ttu-id="c070d-112">Przykład: FunctionImport przy użyciu "DELETE"</span><span class="sxs-lookup"><span data-stu-id="c070d-112">Example: FunctionImport using "DELETE"</span></span>
<span data-ttu-id="c070d-113">Użyj tooremove usunięcia określonego identyfikatora URI.</span><span class="sxs-lookup"><span data-stu-id="c070d-113">Use DELETE tooremove a specified URI.</span></span>

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

## <a name="example-functionimport-using-post"></a><span data-ttu-id="c070d-114">Przykład: FunctionImport przy użyciu "POST"</span><span class="sxs-lookup"><span data-stu-id="c070d-114">Example: FunctionImport using "POST"</span></span>
<span data-ttu-id="c070d-115">Użyj POST nieprzetworzone dane toocreate nowy podrzędny i zwróć URL(location) zdefiniowane przez jego serwer lub tooupdate część hello na powitania serwera podrzędnego adresu URL.</span><span class="sxs-lookup"><span data-stu-id="c070d-115">Use POST Raw data toocreate a new subordinate and return its server defined URL(location) or tooupdate part of hello subordinate at hello server defined URL.</span></span>  <span data-ttu-id="c070d-116">Gdy podrzędny hello jest strukturą.</span><span class="sxs-lookup"><span data-stu-id="c070d-116">Where hello subordinate is a structure.</span></span> <span data-ttu-id="c070d-117">Uważaj POST nie jest idempotentności bez lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="c070d-117">Beware POST is not idempotent without a location.</span></span>

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

## <a name="example-functionimport-using-put"></a><span data-ttu-id="c070d-118">Przykład: FunctionImport przy użyciu "PUT"</span><span class="sxs-lookup"><span data-stu-id="c070d-118">Example: FunctionImport using "PUT"</span></span>
<span data-ttu-id="c070d-119">Użyj PUT toocreate nowy podrzędny lub adres URL zdefiniowany tooupdate hello całego podrzędny na serwerze.</span><span class="sxs-lookup"><span data-stu-id="c070d-119">Use PUT toocreate a new subordinate or tooupdate hello entire subordinate at a server defined URL.</span></span>  <span data-ttu-id="c070d-120">W przypadku, gdy podrzędny hello jest strukturą, PUT jest idempotentności tak wielu wystąpień spowoduje hello sam stan, tj</span><span class="sxs-lookup"><span data-stu-id="c070d-120">Where hello subordinate is a structure, PUT is idempotent so multiple occurrences will result in hello same state, i.e</span></span> <span data-ttu-id="c070d-121">x = 5.</span><span class="sxs-lookup"><span data-stu-id="c070d-121">x=5.</span></span>  <span data-ttu-id="c070d-122">Put powinien być używany z hello całej zawartości z hello określonych zasobów.</span><span class="sxs-lookup"><span data-stu-id="c070d-122">Put should be used with hello full content of hello specified resource.</span></span>

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


## <a name="example-functionimport-for-raw-data-returned-using-put"></a><span data-ttu-id="c070d-123">Przykład: FunctionImport "Raw" danych zwracane przy użyciu "PUT"</span><span class="sxs-lookup"><span data-stu-id="c070d-123">Example: FunctionImport for "Raw" data returned using "PUT"</span></span>
<span data-ttu-id="c070d-124">Użyj PUT nieprzetworzone dane toocreate nowy podrzędny lub podrzędny całego hello tooupdate pod adresem URL zdefiniowanego serwera.</span><span class="sxs-lookup"><span data-stu-id="c070d-124">Use PUT Raw data toocreate a new subordinate or tooupdate hello entire subordinate at a server defined URL.</span></span>  <span data-ttu-id="c070d-125">Gdzie podrzędny hello jest typu stream, tzn. bez struktury, np.</span><span class="sxs-lookup"><span data-stu-id="c070d-125">Where hello subordinate is a stream, i.e. unstructured, ex.</span></span> <span data-ttu-id="c070d-126">plik tekstowy.</span><span class="sxs-lookup"><span data-stu-id="c070d-126">a text file.</span></span>  <span data-ttu-id="c070d-127">PUT jest idempotentności tak wielu wystąpień spowoduje hello sam stan, tj</span><span class="sxs-lookup"><span data-stu-id="c070d-127">PUT is idempotent so multiple occurrences will result in hello same state, i.e</span></span> <span data-ttu-id="c070d-128">x = 5.</span><span class="sxs-lookup"><span data-stu-id="c070d-128">x=5.</span></span>  <span data-ttu-id="c070d-129">Put powinien być używany z hello całej zawartości z hello określonych zasobów.</span><span class="sxs-lookup"><span data-stu-id="c070d-129">Put should be used with hello full content of hello specified resource.</span></span>

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


## <a name="example-functionimport-for-raw-data-returned-using-get"></a><span data-ttu-id="c070d-130">Przykład: FunctionImport "Raw" danych zwracane przy użyciu "GET"</span><span class="sxs-lookup"><span data-stu-id="c070d-130">Example: FunctionImport for "Raw" data returned using "GET"</span></span>
<span data-ttu-id="c070d-131">Za pomocą UZYSKAĆ nieprzetworzone dane tooreturn podrzędny, która nie ma określonej struktury, tj. tekst.</span><span class="sxs-lookup"><span data-stu-id="c070d-131">Use GET Raw data tooreturn a subordinate that is unstructured, i.e. text.</span></span>

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

## <a name="example-functionimport-for-paging-through-returned-data"></a><span data-ttu-id="c070d-132">Przykład: FunctionImport "Stronicowanie" za pośrednictwem zwrócone dane</span><span class="sxs-lookup"><span data-stu-id="c070d-132">Example: FunctionImport for "Paging" through returned data</span></span>
<span data-ttu-id="c070d-133">Implementowanie stronicowania RESTful za pośrednictwem danych za pomocą GET.</span><span class="sxs-lookup"><span data-stu-id="c070d-133">Use implement RESTful paging through your data with GET.</span></span>  <span data-ttu-id="c070d-134">Domyślne stronicowania ustawiono too100 wiersza na stronie danych.</span><span class="sxs-lookup"><span data-stu-id="c070d-134">Default paging is set too100 row per page of data.</span></span>

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

## <a name="see-also"></a><span data-ttu-id="c070d-135">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="c070d-135">See Also</span></span>
* <span data-ttu-id="c070d-136">Jeśli interesuje Cię w uzgodnieniu hello ogólny proces mapowania OData i cel, przeczytaj ten artykuł [danych usługi OData mapowania](marketplace-publishing-data-service-creation-odata-mapping.md) tooreview definicje, struktur i instrukcje.</span><span class="sxs-lookup"><span data-stu-id="c070d-136">If you are interested in understanding hello overall OData mapping process and purpose, read this article [Data Service OData Mapping](marketplace-publishing-data-service-creation-odata-mapping.md) tooreview definitions, structures, and instructions.</span></span>
* <span data-ttu-id="c070d-137">Jeśli interesuje Cię learning oraz opis hello określonych węzłów i ich parametry, przeczytaj ten artykuł [węzły mapowanie danych usługi OData](marketplace-publishing-data-service-creation-odata-mapping-nodes.md) definicje i wyjaśnienia, przykłady i kontekstu przypadków użycia.</span><span class="sxs-lookup"><span data-stu-id="c070d-137">If you are interested in learning and understanding hello specific nodes and their parameters, read this article [Data Service OData Mapping Nodes](marketplace-publishing-data-service-creation-odata-mapping-nodes.md) for definitions and explanations, examples, and use case context.</span></span>
* <span data-ttu-id="c070d-138">toohello tooreturn określonej ścieżki do publikowania toohello danych usługi Azure Marketplace, przeczytaj ten artykuł [Podręcznik publikowania danych usługi](marketplace-publishing-data-service-creation.md).</span><span class="sxs-lookup"><span data-stu-id="c070d-138">tooreturn toohello prescribed path for publishing a Data Service toohello Azure Marketplace, read this article [Data Service Publishing Guide](marketplace-publishing-data-service-creation.md).</span></span>

