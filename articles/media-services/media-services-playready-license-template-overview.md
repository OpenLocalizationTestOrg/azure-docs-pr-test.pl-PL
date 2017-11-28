---
title: "Omówienie szablon licencji PlayReady usług aaaMedia"
description: "Ten temat zawiera omówienie szablon licencji PlayReady, który używany licencje PlayReady tooconfigure."
author: juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: fddce5d0-1278-478f-ae05-9b985c748731
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: juliako
ms.openlocfilehash: 5a5ba930c56f70038db204681486ebc4308199fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="media-services-playready-license-template-overview"></a><span data-ttu-id="93c71-103">Omówienie szablon licencji PlayReady usługi multimediów</span><span class="sxs-lookup"><span data-stu-id="93c71-103">Media Services PlayReady license template overview</span></span>
<span data-ttu-id="93c71-104">Usługa Azure Media Services udostępnia teraz usługę dostarczania licencji PlayReady firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="93c71-104">Azure Media Services now provides a service for delivering Microsoft PlayReady licenses.</span></span> <span data-ttu-id="93c71-105">Gdy hello player użytkownika końcowego (na przykład Silverlight) próbuje tooplay PlayReady z zawartości chronionej, żądanie wysłane toohello licencji dostarczania usługi tooobtain licencji.</span><span class="sxs-lookup"><span data-stu-id="93c71-105">When hello end user player (for example, Silverlight) tries tooplay your PlayReady protected content, a request is sent toohello license delivery service tooobtain a license.</span></span> <span data-ttu-id="93c71-106">Jeśli usługa licencji hello zatwierdza Żądanie hello, wystawia licencję hello, która jest wysłane toohello klienta i mogą być używane toodecrypt i play hello określonej zawartości.</span><span class="sxs-lookup"><span data-stu-id="93c71-106">If hello license service approves hello request, it issues hello license which is sent toohello client and can be used toodecrypt and play hello specified content.</span></span>

<span data-ttu-id="93c71-107">Media Services dostarcza również interfejsy API, które umożliwiają skonfigurowanie licencji PlayReady.</span><span class="sxs-lookup"><span data-stu-id="93c71-107">Media Services also provides APIs that let you configure your PlayReady licenses.</span></span> <span data-ttu-id="93c71-108">Licencje zawierają hello prawa i ograniczenia, które mają dla hello tooenforce środowiska uruchomieniowego PlayReady DRM, gdy użytkownik próbuje tooplayback chronionej zawartości.</span><span class="sxs-lookup"><span data-stu-id="93c71-108">Licenses contain hello rights and restrictions that you want for hello PlayReady DRM runtime tooenforce when a user is trying tooplayback protected content.</span></span>
<span data-ttu-id="93c71-109">Poniżej przedstawiono niektóre ograniczenia licencji PlayReady, które można określić:</span><span class="sxs-lookup"><span data-stu-id="93c71-109">Below are some examples of PlayReady license restrictions that you can specify:</span></span>

* <span data-ttu-id="93c71-110">DateTime Hello, z których hello licencja jest nieprawidłowa.</span><span class="sxs-lookup"><span data-stu-id="93c71-110">hello DateTime from which hello license is valid.</span></span>
* <span data-ttu-id="93c71-111">wartość daty i godziny wygaśnięcia licencji hello Hello.</span><span class="sxs-lookup"><span data-stu-id="93c71-111">hello DateTime value when hello license expires.</span></span> 
* <span data-ttu-id="93c71-112">Dla hello toobe licencji zapisywane w magazynu trwałego na powitania klienta.</span><span class="sxs-lookup"><span data-stu-id="93c71-112">For hello license toobe saved in persistent storage on hello client.</span></span> <span data-ttu-id="93c71-113">Trwałe licencje są tooallow zwykle używanych w trybie offline odtwarzanie hello zawartości.</span><span class="sxs-lookup"><span data-stu-id="93c71-113">Persistent licenses are typically used tooallow offline playback of hello content.</span></span>
* <span data-ttu-id="93c71-114">Witaj minimalny poziom zabezpieczeń czy gracz musi mieć tooplay zawartości.</span><span class="sxs-lookup"><span data-stu-id="93c71-114">hello minimum security level that a player must have tooplay your content.</span></span> 
* <span data-ttu-id="93c71-115">Witaj output poziom ochrony dla formantów danych wyjściowych hello audio\video zawartości.</span><span class="sxs-lookup"><span data-stu-id="93c71-115">hello output protection level for hello output controls for audio\video content.</span></span> 
* <span data-ttu-id="93c71-116">Aby uzyskać więcej informacji, zobacz (3.5) hello w sekcji Formanty danych wyjściowych hello [reguły zgodności PlayReady](https://www.microsoft.com/playready/licensing/compliance/) dokumentu.</span><span class="sxs-lookup"><span data-stu-id="93c71-116">For more information, see hello Output Controls section (3.5) in hello [PlayReady Compliance Rules](https://www.microsoft.com/playready/licensing/compliance/) document.</span></span>

> [!NOTE]
> <span data-ttu-id="93c71-117">Obecnie można skonfigurować tylko hello PlayRight licencji PlayReady hello (to prawo jest wymagane).</span><span class="sxs-lookup"><span data-stu-id="93c71-117">Currently, you can only configure hello PlayRight of hello PlayReady license (this right is required).</span></span> <span data-ttu-id="93c71-118">Witaj PlayRight daje powitania klienta hello możliwości tooplayback hello zawartości.</span><span class="sxs-lookup"><span data-stu-id="93c71-118">hello PlayRight gives hello client hello ability tooplayback hello content.</span></span> <span data-ttu-id="93c71-119">Hello PlayRight umożliwia również konfigurowanie tooplayback określonych ograniczeń.</span><span class="sxs-lookup"><span data-stu-id="93c71-119">hello PlayRight also allows configuring restrictions specific tooplayback.</span></span> <span data-ttu-id="93c71-120">Aby uzyskać więcej informacji, zobacz [PlayReadyPlayRight](media-services-playready-license-template-overview.md#PlayReadyPlayRight).</span><span class="sxs-lookup"><span data-stu-id="93c71-120">For more information, see [PlayReadyPlayRight](media-services-playready-license-template-overview.md#PlayReadyPlayRight).</span></span>
> 
> 

<span data-ttu-id="93c71-121">licencje PlayReady tooconfigure za pomocą usługi Media Services, należy skonfigurować szablon licencji Media Services PlayReady hello.</span><span class="sxs-lookup"><span data-stu-id="93c71-121">tooconfigure PlayReady licenses using Media Services, you must configure hello Media Services PlayReady license template.</span></span> <span data-ttu-id="93c71-122">Witaj szablon jest zdefiniowany w pliku XML.</span><span class="sxs-lookup"><span data-stu-id="93c71-122">hello template is defined in XML.</span></span>

<span data-ttu-id="93c71-123">Witaj poniższy przykład przedstawia szablon najprostszym (i najbardziej typowych) hello, który konfiguruje podstawowe licencji przesyłania strumieniowego.</span><span class="sxs-lookup"><span data-stu-id="93c71-123">hello following example shows hello simplest (and most common) template that configures a basic streaming license.</span></span> <span data-ttu-id="93c71-124">Ta licencja klienci będą mogli tooplayback Twojego PlayReady chronionej zawartości.</span><span class="sxs-lookup"><span data-stu-id="93c71-124">With this license, your clients would be able tooplayback your PlayReady protected content.</span></span>

    <?xml version="1.0" encoding="utf-8"?>
    <PlayReadyLicenseResponseTemplate xmlns:i="http://www.w3.org/2001/XMLSchema-instance" 
                                      xmlns="http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/PlayReadyTemplate/v1">
      <LicenseTemplates>
        <PlayReadyLicenseTemplate>
          <ContentKey i:type="ContentEncryptionKeyFromHeader" />
          <PlayRight />
        </PlayReadyLicenseTemplate>
      </LicenseTemplates>
    </PlayReadyLicenseResponseTemplate>

<span data-ttu-id="93c71-125">Witaj XML zgodne schematu XML rozszerzeń toohello PlayReady licencji szablonu zdefiniowany w szablonie licencji PlayReady hello sekcji schematu XML.</span><span class="sxs-lookup"><span data-stu-id="93c71-125">hello XML conforms toohello PlayReady license template XML schema defined in hello PlayReady license template XML schema section.</span></span>

<span data-ttu-id="93c71-126">Usługa Media Services również definiuje zestaw klas .NET, które mogą być używane tooserialized i zdeserializowany tooand z hello XML.</span><span class="sxs-lookup"><span data-stu-id="93c71-126">Media Services also defines a set of .NET classes that could be used tooserialized and deserialized tooand from hello XML.</span></span> <span data-ttu-id="93c71-127">Aby uzyskać opis klasy głównym, zobacz [klasy Media Services na platformie .NET](media-services-playready-license-template-overview.md#classes).</span><span class="sxs-lookup"><span data-stu-id="93c71-127">For description of main classes, see [Media Services .NET classes](media-services-playready-license-template-overview.md#classes).</span></span> <span data-ttu-id="93c71-128">które są używane tooconfigure licencji szablonów.</span><span class="sxs-lookup"><span data-stu-id="93c71-128">that are used tooconfigure license templates.</span></span>

<span data-ttu-id="93c71-129">Na przykład na trasie, w którym będzie używał programu .NET klasy szablon licencji PlayReady hello tooconfigure, zobacz [za pomocą szyfrowania dynamicznego PlayReady i usługi dostarczania licencji](media-services-protect-with-drm.md).</span><span class="sxs-lookup"><span data-stu-id="93c71-129">For an end-to-end example that uses .NET classes tooconfigure hello PlayReady license template, see [Using PlayReady Dynamic Encryption and License Delivery Service](media-services-protect-with-drm.md).</span></span>

## <span data-ttu-id="93c71-130"><a id="classes"></a>Klasy Media Services na platformie .NET, które są używane tooconfigure licencji szablonów</span><span class="sxs-lookup"><span data-stu-id="93c71-130"><a id="classes"></a>Media Services .NET classes that are used tooconfigure license templates</span></span>
<span data-ttu-id="93c71-131">Witaj poniżej przedstawiono główne klasy .NET hello są szablony licencji PlayReady usług Media tooconfigure używane.</span><span class="sxs-lookup"><span data-stu-id="93c71-131">hello following are hello main .NET classes are used tooconfigure Media Services PlayReady license templates.</span></span> <span data-ttu-id="93c71-132">Te klasy mapy toohello typów zdefiniowanych w [schematu XML szablonu licencji PlayReady](media-services-playready-license-template-overview.md#schema).</span><span class="sxs-lookup"><span data-stu-id="93c71-132">These classes map toohello types defined in [PlayReady license template XML schema](media-services-playready-license-template-overview.md#schema).</span></span>

<span data-ttu-id="93c71-133">Witaj [MediaServicesLicenseTemplateSerializer](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.mediaserviceslicensetemplateserializer.aspx) klasa jest używana tooserialize i deserializacji tooand z szablon licencji Media Services hello XML.</span><span class="sxs-lookup"><span data-stu-id="93c71-133">hello [MediaServicesLicenseTemplateSerializer](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.mediaserviceslicensetemplateserializer.aspx) class is used tooserialize and deserialize tooand from hello Media Services license template XML.</span></span>

### <a name="playreadylicenseresponsetemplate"></a><span data-ttu-id="93c71-134">PlayReadyLicenseResponseTemplate</span><span class="sxs-lookup"><span data-stu-id="93c71-134">PlayReadyLicenseResponseTemplate</span></span>
<span data-ttu-id="93c71-135">[PlayReadyLicenseResponseTemplate](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.playreadylicenseresponsetemplate.aspx) — ta klasa reprezentuje hello szablonu dla użytkownika końcowego wstecz toohello wysłanych odpowiedzi hello.</span><span class="sxs-lookup"><span data-stu-id="93c71-135">[PlayReadyLicenseResponseTemplate](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.playreadylicenseresponsetemplate.aspx) - This class represents hello template for hello response sent back toohello end user.</span></span> <span data-ttu-id="93c71-136">Zawiera on pole niestandardowe dane ciągu między powitania serwera licencji i aplikacji hello (może być przydatne w przypadku aplikacji niestandardowej logiki), a także listę co najmniej jeden szablon licencji.</span><span class="sxs-lookup"><span data-stu-id="93c71-136">It contains a field for a custom data string between hello license server and hello application (may be useful for custom app logic) as well as a list of one or more license templates.</span></span>

<span data-ttu-id="93c71-137">To jest klasa "najwyższego poziomu" hello hello szablonu hierarchii.</span><span class="sxs-lookup"><span data-stu-id="93c71-137">This is hello “top level” class in hello template hierarchy.</span></span> <span data-ttu-id="93c71-138">Co oznacza, że szablon odpowiedzi hello zawiera listę szablonów licencji i hello licencji szablony obejmują (bezpośrednio lub pośrednio) hello wszystkie inne klasy, które tworzą toobe danych szablonu hello serializacji.</span><span class="sxs-lookup"><span data-stu-id="93c71-138">Meaning that hello response template includes a list of license templates and hello license templates include (directly or indirectly) all of hello other classes that make up hello template data toobe serialized.</span></span>

### <a name="playreadylicensetemplate"></a><span data-ttu-id="93c71-139">PlayReadyLicenseTemplate</span><span class="sxs-lookup"><span data-stu-id="93c71-139">PlayReadyLicenseTemplate</span></span>
<span data-ttu-id="93c71-140">[PlayReadyLicenseTemplate](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.playreadylicensetemplate.aspx) — klasa hello reprezentuje szablon licencji do tworzenia toobe licencji PlayReady zwrócił toohello użytkowników końcowych.</span><span class="sxs-lookup"><span data-stu-id="93c71-140">[PlayReadyLicenseTemplate](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.playreadylicensetemplate.aspx) - hello class represents a license template for creating PlayReady licenses toobe returned toohello end users.</span></span> <span data-ttu-id="93c71-141">Zawiera dane hello na powitania klucz zawartości w hello licencji i toobe żadnych uprawnień lub ograniczeń wymuszane przez hello środowiska uruchomieniowego PlayReady DRM używając hello klucz zawartości.</span><span class="sxs-lookup"><span data-stu-id="93c71-141">It contains hello data on hello content key in hello license and any rights or restrictions toobe enforced by hello PlayReady DRM runtime when using hello content key.</span></span>

### <span data-ttu-id="93c71-142"><a id="PlayReadyPlayRight"></a>PlayReadyPlayRight</span><span class="sxs-lookup"><span data-stu-id="93c71-142"><a id="PlayReadyPlayRight"></a>PlayReadyPlayRight</span></span>
<span data-ttu-id="93c71-143">[PlayReadyPlayRight](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.playreadyplayright.aspx) — ta klasa reprezentuje hello PlayRight licencji PlayReady.</span><span class="sxs-lookup"><span data-stu-id="93c71-143">[PlayReadyPlayRight](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.playreadyplayright.aspx) - This class represents hello PlayRight of a PlayReady license.</span></span> <span data-ttu-id="93c71-144">Domyślnie przyzna hello użytkownika hello możliwości tooplayback hello toohello zawartości podmiotu zero lub więcej ograniczeń skonfigurowane w hello licencji i na powitania PlayRight sam (dla określonych zasad dotyczących odtwarzania).</span><span class="sxs-lookup"><span data-stu-id="93c71-144">It grants hello user hello ability tooplayback hello content subject toohello zero or more restrictions configured in hello license and on hello PlayRight itself (for playback specific policy).</span></span> <span data-ttu-id="93c71-145">Większość zasad hello na powitania PlayRight ma toodo z danych wyjściowych ograniczeń, które kontrolowanie hello typów danych wyjściowych, które można odtwarzać zawartość hello za pośrednictwem i ograniczeń, które można umieścić w miejscu korzystając z danym danych wyjściowych.</span><span class="sxs-lookup"><span data-stu-id="93c71-145">Much of hello policy on hello PlayRight has toodo with output restrictions which control hello types of outputs that hello content can be played over and any restrictions that must be put in place when using a given output.</span></span> <span data-ttu-id="93c71-146">Na przykład jeśli hello DigitalVideoOnlyContentRestriction jest włączona, następnie hello środowiska uruchomieniowego DRM zezwala tylko hello toobe wideo wyświetlane na cyfrowe dane wyjściowe (analogowy wyjść wideo nie będą mogły toopass hello zawartości).</span><span class="sxs-lookup"><span data-stu-id="93c71-146">For example, if hello DigitalVideoOnlyContentRestriction is enabled, then hello DRM runtime will only allow hello video toobe displayed over digital outputs (analog video outputs won’t be allowed toopass hello content).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="93c71-147">Tego rodzaju ograniczenia mogą być bardzo zaawansowane, ale również może mieć wpływ na powitania klienta środowiska.</span><span class="sxs-lookup"><span data-stu-id="93c71-147">These types of restrictions can be very powerful but can also affect hello consumer experience.</span></span> <span data-ttu-id="93c71-148">Jeśli hello ochrony dane wyjściowe są skonfigurowane zbyt restrykcyjne, hello zawartości może być odtworzona w niektórych klientów.</span><span class="sxs-lookup"><span data-stu-id="93c71-148">If hello output protections are configured too restrictive, hello content might be unplayable on some clients.</span></span> <span data-ttu-id="93c71-149">Aby uzyskać więcej informacji, zobacz hello [reguły zgodności PlayReady](https://www.microsoft.com/playready/licensing/compliance/) dokumentu.</span><span class="sxs-lookup"><span data-stu-id="93c71-149">For more information, see hello [PlayReady Compliance Rules](https://www.microsoft.com/playready/licensing/compliance/) document.</span></span>
> 
> 

<span data-ttu-id="93c71-150">Przykład jakie ochrony poziomy obsługuje Silverlight, zobacz: [Silverlight obsługę ochrony danych wyjściowych](http://go.microsoft.com/fwlink/?LinkId=617318).</span><span class="sxs-lookup"><span data-stu-id="93c71-150">For an example of what protection levels Silverlight supports, see: [Silverlight support for output protections](http://go.microsoft.com/fwlink/?LinkId=617318).</span></span>

## <span data-ttu-id="93c71-151"><a id="schema"></a>Schemat XML szablonu licencji PlayReady</span><span class="sxs-lookup"><span data-stu-id="93c71-151"><a id="schema"></a>PlayReady license template XML schema</span></span>
    <?xml version="1.0" encoding="utf-8"?>
    <xs:schema xmlns:tns="http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/PlayReadyTemplate/v1" xmlns:ser="http://schemas.microsoft.com/2003/10/Serialization/" elementFormDefault="qualified" targetNamespace="http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/PlayReadyTemplate/v1" xmlns:xs="http://www.w3.org/2001/XMLSchema">
      <xs:import namespace="http://schemas.microsoft.com/2003/10/Serialization/" />
      <xs:complexType name="AgcAndColorStripeRestriction">
        <xs:sequence>
          <xs:element minOccurs="0" name="ConfigurationData" type="xs:unsignedByte" />
        </xs:sequence>
      </xs:complexType>
      <xs:element name="AgcAndColorStripeRestriction" nillable="true" type="tns:AgcAndColorStripeRestriction" />
      <xs:simpleType name="ContentType">
        <xs:restriction base="xs:string">
          <xs:enumeration value="Unspecified" />
          <xs:enumeration value="UltravioletDownload" />
          <xs:enumeration value="UltravioletStreaming" />
        </xs:restriction>
      </xs:simpleType>
      <xs:element name="ContentType" nillable="true" type="tns:ContentType" />
      <xs:complexType name="ExplicitAnalogTelevisionRestriction">
        <xs:sequence>
          <xs:element minOccurs="0" name="BestEffort" type="xs:boolean" />
          <xs:element minOccurs="0" name="ConfigurationData" type="xs:unsignedByte" />
        </xs:sequence>
      </xs:complexType>
      <xs:element name="ExplicitAnalogTelevisionRestriction" nillable="true" type="tns:ExplicitAnalogTelevisionRestriction" />
      <xs:complexType name="PlayReadyContentKey">
        <xs:sequence />
      </xs:complexType>
      <xs:element name="PlayReadyContentKey" nillable="true" type="tns:PlayReadyContentKey" />
      <xs:complexType name="ContentEncryptionKeyFromHeader">
        <xs:complexContent mixed="false">
          <xs:extension base="tns:PlayReadyContentKey">
            <xs:sequence />
          </xs:extension>
        </xs:complexContent>
      </xs:complexType>
      <xs:element name="ContentEncryptionKeyFromHeader" nillable="true" type="tns:ContentEncryptionKeyFromHeader" />
      <xs:complexType name="ContentEncryptionKeyFromKeyIdentifier">
        <xs:complexContent mixed="false">
          <xs:extension base="tns:PlayReadyContentKey">
            <xs:sequence>
              <xs:element minOccurs="0" name="KeyIdentifier" type="ser:guid" />
            </xs:sequence>
          </xs:extension>
        </xs:complexContent>
      </xs:complexType>
      <xs:element name="ContentEncryptionKeyFromKeyIdentifier" nillable="true" type="tns:ContentEncryptionKeyFromKeyIdentifier" />
      <xs:complexType name="PlayReadyLicenseResponseTemplate">
        <xs:sequence>
          <xs:element name="LicenseTemplates" nillable="true" type="tns:ArrayOfPlayReadyLicenseTemplate" />
          <xs:element minOccurs="0" name="ResponseCustomData" nillable="true" type="xs:string">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
        </xs:sequence>
      </xs:complexType>
      <xs:element name="PlayReadyLicenseResponseTemplate" nillable="true" type="tns:PlayReadyLicenseResponseTemplate" />
      <xs:complexType name="ArrayOfPlayReadyLicenseTemplate">
        <xs:sequence>
          <xs:element minOccurs="0" maxOccurs="unbounded" name="PlayReadyLicenseTemplate" nillable="true" type="tns:PlayReadyLicenseTemplate" />
        </xs:sequence>
      </xs:complexType>
      <xs:element name="ArrayOfPlayReadyLicenseTemplate" nillable="true" type="tns:ArrayOfPlayReadyLicenseTemplate" />
      <xs:complexType name="PlayReadyLicenseTemplate">
        <xs:sequence>
          <xs:element minOccurs="0" name="AllowTestDevices" type="xs:boolean" />
          <xs:element minOccurs="0" name="BeginDate" nillable="true" type="xs:dateTime">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element name="ContentKey" nillable="true" type="tns:PlayReadyContentKey" />
          <xs:element minOccurs="0" name="ContentType" type="tns:ContentType">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="ExpirationDate" nillable="true" type="xs:dateTime">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="GracePeriod" nillable="true" type="ser:duration">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="LicenseType" type="tns:PlayReadyLicenseType" />
          <xs:element minOccurs="0" name="PlayRight" nillable="true" type="tns:PlayReadyPlayRight" />
        </xs:sequence>
      </xs:complexType>
      <xs:element name="PlayReadyLicenseTemplate" nillable="true" type="tns:PlayReadyLicenseTemplate" />
      <xs:simpleType name="PlayReadyLicenseType">
        <xs:restriction base="xs:string">
          <xs:enumeration value="Nonpersistent" />
          <xs:enumeration value="Persistent" />
        </xs:restriction>
      </xs:simpleType>
      <xs:element name="PlayReadyLicenseType" nillable="true" type="tns:PlayReadyLicenseType" />
      <xs:complexType name="PlayReadyPlayRight">
        <xs:sequence>
          <xs:element minOccurs="0" name="AgcAndColorStripeRestriction" nillable="true" type="tns:AgcAndColorStripeRestriction">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="AllowPassingVideoContentToUnknownOutput" type="tns:UnknownOutputPassingOption">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="AnalogVideoOpl" nillable="true" type="xs:int">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="CompressedDigitalAudioOpl" nillable="true" type="xs:int">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="CompressedDigitalVideoOpl" nillable="true" type="xs:int">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="DigitalVideoOnlyContentRestriction" type="xs:boolean">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="ExplicitAnalogTelevisionOutputRestriction" nillable="true" type="tns:ExplicitAnalogTelevisionRestriction">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="FirstPlayExpiration" nillable="true" type="ser:duration">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="ImageConstraintForAnalogComponentVideoRestriction" type="xs:boolean">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="ImageConstraintForAnalogComputerMonitorRestriction" type="xs:boolean">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="ScmsRestriction" nillable="true" type="tns:ScmsRestriction">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="UncompressedDigitalAudioOpl" nillable="true" type="xs:int">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="UncompressedDigitalVideoOpl" nillable="true" type="xs:int">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
        </xs:sequence>
      </xs:complexType>
      <xs:element name="PlayReadyPlayRight" nillable="true" type="tns:PlayReadyPlayRight" />
      <xs:simpleType name="UnknownOutputPassingOption">
        <xs:restriction base="xs:string">
          <xs:enumeration value="NotAllowed" />
          <xs:enumeration value="Allowed" />
          <xs:enumeration value="AllowedWithVideoConstriction" />
        </xs:restriction>
      </xs:simpleType>
      <xs:element name="UnknownOutputPassingOption" nillable="true" type="tns:UnknownOutputPassingOption" />
      <xs:complexType name="ScmsRestriction">
        <xs:sequence>
          <xs:element minOccurs="0" name="ConfigurationData" type="xs:unsignedByte" />
        </xs:sequence>
      </xs:complexType>
      <xs:element name="ScmsRestriction" nillable="true" type="tns:ScmsRestriction" />
    </xs:schema>



## <a name="media-services-learning-paths"></a><span data-ttu-id="93c71-152">Ścieżki szkoleniowe dotyczące usługi Media Services</span><span class="sxs-lookup"><span data-stu-id="93c71-152">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="93c71-153">Przekazywanie opinii</span><span class="sxs-lookup"><span data-stu-id="93c71-153">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

