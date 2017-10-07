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
# <a name="media-services-playready-license-template-overview"></a>Omówienie szablon licencji PlayReady usługi multimediów
Usługa Azure Media Services udostępnia teraz usługę dostarczania licencji PlayReady firmy Microsoft. Gdy hello player użytkownika końcowego (na przykład Silverlight) próbuje tooplay PlayReady z zawartości chronionej, żądanie wysłane toohello licencji dostarczania usługi tooobtain licencji. Jeśli usługa licencji hello zatwierdza Żądanie hello, wystawia licencję hello, która jest wysłane toohello klienta i mogą być używane toodecrypt i play hello określonej zawartości.

Media Services dostarcza również interfejsy API, które umożliwiają skonfigurowanie licencji PlayReady. Licencje zawierają hello prawa i ograniczenia, które mają dla hello tooenforce środowiska uruchomieniowego PlayReady DRM, gdy użytkownik próbuje tooplayback chronionej zawartości.
Poniżej przedstawiono niektóre ograniczenia licencji PlayReady, które można określić:

* DateTime Hello, z których hello licencja jest nieprawidłowa.
* wartość daty i godziny wygaśnięcia licencji hello Hello. 
* Dla hello toobe licencji zapisywane w magazynu trwałego na powitania klienta. Trwałe licencje są tooallow zwykle używanych w trybie offline odtwarzanie hello zawartości.
* Witaj minimalny poziom zabezpieczeń czy gracz musi mieć tooplay zawartości. 
* Witaj output poziom ochrony dla formantów danych wyjściowych hello audio\video zawartości. 
* Aby uzyskać więcej informacji, zobacz (3.5) hello w sekcji Formanty danych wyjściowych hello [reguły zgodności PlayReady](https://www.microsoft.com/playready/licensing/compliance/) dokumentu.

> [!NOTE]
> Obecnie można skonfigurować tylko hello PlayRight licencji PlayReady hello (to prawo jest wymagane). Witaj PlayRight daje powitania klienta hello możliwości tooplayback hello zawartości. Hello PlayRight umożliwia również konfigurowanie tooplayback określonych ograniczeń. Aby uzyskać więcej informacji, zobacz [PlayReadyPlayRight](media-services-playready-license-template-overview.md#PlayReadyPlayRight).
> 
> 

licencje PlayReady tooconfigure za pomocą usługi Media Services, należy skonfigurować szablon licencji Media Services PlayReady hello. Witaj szablon jest zdefiniowany w pliku XML.

Witaj poniższy przykład przedstawia szablon najprostszym (i najbardziej typowych) hello, który konfiguruje podstawowe licencji przesyłania strumieniowego. Ta licencja klienci będą mogli tooplayback Twojego PlayReady chronionej zawartości.

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

Witaj XML zgodne schematu XML rozszerzeń toohello PlayReady licencji szablonu zdefiniowany w szablonie licencji PlayReady hello sekcji schematu XML.

Usługa Media Services również definiuje zestaw klas .NET, które mogą być używane tooserialized i zdeserializowany tooand z hello XML. Aby uzyskać opis klasy głównym, zobacz [klasy Media Services na platformie .NET](media-services-playready-license-template-overview.md#classes). które są używane tooconfigure licencji szablonów.

Na przykład na trasie, w którym będzie używał programu .NET klasy szablon licencji PlayReady hello tooconfigure, zobacz [za pomocą szyfrowania dynamicznego PlayReady i usługi dostarczania licencji](media-services-protect-with-drm.md).

## <a id="classes"></a>Klasy Media Services na platformie .NET, które są używane tooconfigure licencji szablonów
Witaj poniżej przedstawiono główne klasy .NET hello są szablony licencji PlayReady usług Media tooconfigure używane. Te klasy mapy toohello typów zdefiniowanych w [schematu XML szablonu licencji PlayReady](media-services-playready-license-template-overview.md#schema).

Witaj [MediaServicesLicenseTemplateSerializer](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.mediaserviceslicensetemplateserializer.aspx) klasa jest używana tooserialize i deserializacji tooand z szablon licencji Media Services hello XML.

### <a name="playreadylicenseresponsetemplate"></a>PlayReadyLicenseResponseTemplate
[PlayReadyLicenseResponseTemplate](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.playreadylicenseresponsetemplate.aspx) — ta klasa reprezentuje hello szablonu dla użytkownika końcowego wstecz toohello wysłanych odpowiedzi hello. Zawiera on pole niestandardowe dane ciągu między powitania serwera licencji i aplikacji hello (może być przydatne w przypadku aplikacji niestandardowej logiki), a także listę co najmniej jeden szablon licencji.

To jest klasa "najwyższego poziomu" hello hello szablonu hierarchii. Co oznacza, że szablon odpowiedzi hello zawiera listę szablonów licencji i hello licencji szablony obejmują (bezpośrednio lub pośrednio) hello wszystkie inne klasy, które tworzą toobe danych szablonu hello serializacji.

### <a name="playreadylicensetemplate"></a>PlayReadyLicenseTemplate
[PlayReadyLicenseTemplate](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.playreadylicensetemplate.aspx) — klasa hello reprezentuje szablon licencji do tworzenia toobe licencji PlayReady zwrócił toohello użytkowników końcowych. Zawiera dane hello na powitania klucz zawartości w hello licencji i toobe żadnych uprawnień lub ograniczeń wymuszane przez hello środowiska uruchomieniowego PlayReady DRM używając hello klucz zawartości.

### <a id="PlayReadyPlayRight"></a>PlayReadyPlayRight
[PlayReadyPlayRight](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.playreadyplayright.aspx) — ta klasa reprezentuje hello PlayRight licencji PlayReady. Domyślnie przyzna hello użytkownika hello możliwości tooplayback hello toohello zawartości podmiotu zero lub więcej ograniczeń skonfigurowane w hello licencji i na powitania PlayRight sam (dla określonych zasad dotyczących odtwarzania). Większość zasad hello na powitania PlayRight ma toodo z danych wyjściowych ograniczeń, które kontrolowanie hello typów danych wyjściowych, które można odtwarzać zawartość hello za pośrednictwem i ograniczeń, które można umieścić w miejscu korzystając z danym danych wyjściowych. Na przykład jeśli hello DigitalVideoOnlyContentRestriction jest włączona, następnie hello środowiska uruchomieniowego DRM zezwala tylko hello toobe wideo wyświetlane na cyfrowe dane wyjściowe (analogowy wyjść wideo nie będą mogły toopass hello zawartości).

> [!IMPORTANT]
> Tego rodzaju ograniczenia mogą być bardzo zaawansowane, ale również może mieć wpływ na powitania klienta środowiska. Jeśli hello ochrony dane wyjściowe są skonfigurowane zbyt restrykcyjne, hello zawartości może być odtworzona w niektórych klientów. Aby uzyskać więcej informacji, zobacz hello [reguły zgodności PlayReady](https://www.microsoft.com/playready/licensing/compliance/) dokumentu.
> 
> 

Przykład jakie ochrony poziomy obsługuje Silverlight, zobacz: [Silverlight obsługę ochrony danych wyjściowych](http://go.microsoft.com/fwlink/?LinkId=617318).

## <a id="schema"></a>Schemat XML szablonu licencji PlayReady
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



## <a name="media-services-learning-paths"></a>Ścieżki szkoleniowe dotyczące usługi Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Przekazywanie opinii
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

