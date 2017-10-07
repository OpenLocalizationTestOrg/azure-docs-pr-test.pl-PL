---
title: "Schemat wejściowych metadanych usługi Media Services aaaAzure | Dokumentacja firmy Microsoft"
description: "Witaj temat zawiera omówienie usługi Azure Media Services wejściowych metadanych schematu."
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: d72848e2-4b65-4c84-94bc-e2a90a6e7f47
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: juliako
ms.openlocfilehash: 9b72c6ff317aa98451ea75548465dc6023b44a55
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="input-metadata"></a>Dane wejściowe metadanych
Zadania kodowania jest skojarzony z zasób wejściowy (lub zasoby) na którym chcesz tooperform niektóre zadania kodowania.  Po zakończeniu zadania jest generowany zawartości wyjściowej.  zawartości wyjściowej Hello zawiera wideo, audio, miniatur manifestu, zawartości wyjściowej hello itp. zawiera także plik o metadane dotyczące zasobu wejściowego hello. Witaj nazwę pliku XML metadanych hello ma hello następującego formatu: &lt;asset_id&gt;_metadata.xml (na przykład 41114ad3-eb5e - 4c d 57 8 92-5354e2b7d4a4_metadata.xml), gdzie &lt;asset_id&gt; jest hello IDśrodkaTrwałego wartość hello zasobów wejściowych.  

Jeśli chcesz tooexamine hello metadanych plików, można utworzyć **SAS** lokalizator i pobierania hello komputera lokalnego tooyour pliku. Przykład można znaleźć na temat toocreate lokalizatora SAS i pobranie pliku [przy użyciu rozszerzeń zestawu SDK .NET usługi Media hello](media-services-dotnet-get-started.md).  

W tym temacie omówiono hello elementów i typy hello schematu XML na które metada wejściowych hello (&lt;asset_id&gt;_metadata.xml) opiera się.  Informacje o hello zawierający metadane dotyczące zawartości wyjściowej hello, zobacz [metadanych dane wyjściowe](media-services-output-metadata-schema.md).  

> [!NOTE]
> Można znaleźć hello [kodu schematu](media-services-input-metadata-schema.md#code) [przykład XML](media-services-input-metadata-schema.md#xml) na powitania na końcu tego tematu.  
> 
> 

## <a name="AssetFiles"></a>Element AssetFiles (element główny)
Zawiera kolekcję [elementu AssetFile](media-services-input-metadata-schema.md#AssetFile)s hello zadania kodowania.  

Zobacz przykład XML na końcu tego tematu hello: [przykład XML](media-services-input-metadata-schema.md#xml).  

| Nazwa | Opis |
| --- | --- |
| **AssetFile**<br /><br /> minOccurs = maxOccurs "1" = "unbounded" |Element podrzędny pojedynczego. Aby uzyskać więcej informacji, zobacz [AssetFile elementu](media-services-input-metadata-schema.md#AssetFile). |

## <a name="AssetFile"></a>AssetFile element
 Zawiera atrybuty i elementy, które opisują pliku zasobów.  

 Zobacz przykład XML na końcu tego tematu hello: [przykład XML](media-services-input-metadata-schema.md#xml).  

### <a name="attributes"></a>Atrybuty
| Nazwa | Typ | Opis |
| --- | --- | --- |
| **Nazwa**<br /><br /> Wymagane |**xs:String** |Nazwa pliku zasobów. |
| **Rozmiar**<br /><br /> Wymagane |**xs:Long** |Rozmiar pliku zasobów hello w bajtach. |
| **Czas trwania**<br /><br /> Wymagane |**DURATION** |Czas trwania wstecz odtwarzania zawartości. Przykład: Czas trwania = "PT25M37.757S". |
| **NumberOfStreams**<br /><br /> Wymagane |**xs:int** |Liczba strumieni w pliku trwałego hello. |
| **FormatNames**<br /><br /> Wymagane |**xs:String** |Format nazwy. |
| **FormatVerboseNames**<br /><br /> Wymagane |**xs:String** |Pełne nazwy formatu. |
| **Czas rozpoczęcia** |**DURATION** |Godzina rozpoczęcia zawartości. Przykład: Wartość StartTime = "PT2.669S". |
| **OverallBitRate** |**xs:int** |Średnia szybkość transmisji bitów pliku zasobów hello w KB/s. |

> [!NOTE]
> Witaj następujące 4 elementy podrzędne muszą być umieszczone w sekwencji.  
> 
> 

### <a name="child-elements"></a>Elementy podrzędne
| Nazwa | Typ | Opis |
| --- | --- | --- |
| **Programy**<br /><br /> minOccurs = "0" | |Kolekcja wszystkich [element programy](media-services-input-metadata-schema.md#Programs) gdy plik zasobów hello jest w formacie MPEG-TS. |
| **VideoTracks**<br /><br /> minOccurs = "0" | |Każdy plik zasobów fizycznych może zawierać zero lub więcej ścieżek wideo przeplatana do formatu odpowiedniego kontenera. Ten element zawiera zbiór wszystkich [elementu VideoTracks](media-services-input-metadata-schema.md#VideoTracks) będących częścią hello pliku zasobów. |
| **AudioTracks**<br /><br /> minOccurs = "0" | |Każdy plik zasobów fizycznych może zawierać zero lub więcej ścieżek audio przeplatana do formatu odpowiedniego kontenera. Ten element zawiera zbiór wszystkich [elementu AudioTracks](media-services-input-metadata-schema.md#AudioTracks) będących częścią hello pliku zasobów. |
| **Metadane**<br /><br /> minOccurs = maxOccurs "0" = "unbounded" |[MetadataType](media-services-input-metadata-schema.md#MetadataType) |Reprezentowane jako ciągi key\value metadanych pliku zasobów. Na przykład:<br /><br /> **&lt;Metadane klucz = wartość "język" = "eng" /&gt;** |

## <a name="TrackType"></a>TrackType
Zobacz przykład XML na końcu tego tematu hello: [przykład XML](media-services-input-metadata-schema.md#xml).  

### <a name="attributes"></a>Atrybuty
| Nazwa | Typ | Opis |
| --- | --- | --- |
| **Identyfikator**<br /><br /> Wymagane |**xs:int** |Liczony od zera indeks tej ścieżki audio i wideo.<br /><br /> Nie jest tym hello TrackID w pliku MP4. |
| **Koder-dekoder** |**xs:String** |Parametry kodera-dekodera wideo Śledź. |
| **CodecLongName** |**xs:String** |Śledź audio i wideo koder-dekoder długa nazwa. |
| **Podstawy czasu**<br /><br /> Wymagane |**xs:String** |Podstawa czasu. Przykład: Podstawy czasu = "1/48000" |
| **NumberOfFrames** |**xs:int** |Liczba ramek (istnieje dla ścieżki wideo). |
| **Czas rozpoczęcia** |**DURATION** |Godzina rozpoczęcia śledzenia. Przykład: Wartość StartTime = "PT2.669S" |
| **Czas trwania** |**DURATION** |Śledzenie czasu trwania. Przykład: Czas trwania = "PTSampleFormat M37.757S". |

> [!NOTE]
> powitania po 2 elementy podrzędne muszą być umieszczone w sekwencji.  
> 
> 

### <a name="child-elements"></a>Elementy podrzędne
| Nazwa | Typ | Opis |
| --- | --- | --- |
| **Dyspozycji**<br /><br /> minOccurs = maxOccurs "0" = "1" |[StreamDispositionType](media-services-input-metadata-schema.md#StreamDispositionType) |Zawiera informacje o prezentacji (na przykład czy określonej ścieżki audio jest dla osób niedowidzących). |
| **Metadane**<br /><br /> minOccurs = maxOccurs "0" = "unbounded" |[MetadataType](media-services-input-metadata-schema.md#MetadataType) |Ciągi ogólnego klucza i wartości, które mogą być używane toohold różne informacje. Na przykład klucz = "język", a wartość = "eng". |

## <a name="AudioTrackType"></a>AudioTrackType (dziedziczy TrackType)
 **AudioTrackType** jest typem złożonym globalny, który dziedziczy z [TrackType](media-services-input-metadata-schema.md#TrackType).  

 Typ Hello reprezentuje określonej ścieżki audio w pliku trwałego hello.  

 Zobacz przykład XML na końcu tego tematu hello: [przykład XML](media-services-input-metadata-schema.md#xml).  

### <a name="attributes"></a>Atrybuty
| Nazwa | Typ | Opis |
| --- | --- | --- |
| **SampleFormat** |**xs:String** |Przykładowy format. |
| **ChannelLayout** |**xs:String** |Układ kanału. |
| **Kanały**<br /><br /> Wymagane |**xs:int** |Liczba (0 lub więcej) audio kanałów. |
| **SamplingRate**<br /><br /> Wymagane |**xs:int** |Częstotliwość próbkowania audio w próbek na sekundę lub Hz. |
| **Szybkość transmisji bitów** |**xs:int** |Średnia audio szybkość transmisji bitów w bitów na sekundę, obliczoną z hello pliku zasobów. Tylko hello podstawowe strumienia ładunku jest liczony i koszty pakietów hello jest niedostępna w tej liczby. |
| **BitsPerSample** |**xs:int** |Wpisz bitów na próbkę hello wFormatTag formatu. |

## <a name="VideoTrackType"></a>VideoTrackType (dziedziczy TrackType)
**VideoTrackType** jest typem złożonym globalny, który dziedziczy z [TrackType](media-services-input-metadata-schema.md#TrackType).  

Typ Hello reprezentuje określonej ścieżki wideo w pliku trwałego hello.  

Zobacz przykład XML na końcu tego tematu hello: [przykład XML](media-services-input-metadata-schema.md#xml).  

### <a name="attributes"></a>Atrybuty
| Nazwa | Typ | Opis |
| --- | --- | --- |
| **FourCC**<br /><br /> Wymagane |**xs:String** |Kodera-dekodera wideo FourCC kodu. |
| **Profil** |**xs:String** |Ścieżka wideo profil. |
| **Poziom** |**xs:String** |Poziom śledzenia wideo. |
| **PixelFormat** |**xs:String** |Ścieżka wideo format piksela. |
| **Szerokość**<br /><br /> Wymagane |**xs:int** |Zakodowany szerokości wideo w pikselach. |
| **Wysokość**<br /><br /> Wymagane |**xs:int** |Zakodowany wideo wysokość w pikselach. |
| **DisplayAspectRatioNumerator**<br /><br /> Wymagane |**xs:Double** |Licznik współczynnik proporcji wideo. |
| **DisplayAspectRatioDenominator**<br /><br /> Wymagane |**xs:Double** |Denominator współczynnik proporcji wideo. |
| **DisplayAspectRatioDenominator**<br /><br /> Wymagane |**xs:Double** |Przykładowe wideo licznik współczynnik proporcji. |
| **SampleAspectRatioNumerator** |**xs:Double** |Przykładowe wideo licznik współczynnik proporcji. |
| **SampleAspectRatioNumerator** |**xs:Double** |Denominator współczynnik proporcji próbki wideo. |
| **Szybkość klatek**<br /><br /> Wymagane |**xs:decimal** |Mierzy szybkość odtwarzania wideo w formacie .3f. |
| **Szybkość transmisji bitów** |**xs:int** |Średnia wideo szybkość transmisji bitów w kilobitów na sekundę, obliczoną z hello pliku zasobów. Tylko hello podstawowe strumienia ładunku jest liczony i koszty pakietów hello nie jest dołączony. |
| **MaxGOPBitrate** |**xs:int** |Maksymalna liczba GOP średnia szybkość transmisji bitów dla tej ścieżki wideo, w kilobitów na sekundę. |
| **HasBFrames** |**xs:int** |Ścieżka wideo liczbę ramek B. |

## <a name="MetadataType"></a>MetadataType
**MetadataType** jest typem złożonym globalne informacje metadanych z pliku zasobów jako ciągi klucza i wartości. Na przykład klucz = "język", a wartość = "eng".  

Zobacz przykład XML na końcu tego tematu hello: [przykład XML](media-services-input-metadata-schema.md#xml).  

### <a name="attributes"></a>Atrybuty
| Nazwa | Typ | Opis |
| --- | --- | --- |
| **klucz**<br /><br /> Wymagane |**xs:String** |klucz Hello hello pary klucz wartość. |
| **wartość**<br /><br /> Wymagane |**xs:String** |wartość Hello hello pary klucza/wartości. |

## <a name="ProgramType"></a>ProgramType
**ProgramType** jest typem złożonym globalnego zawiera opis programu.  

### <a name="attributes"></a>Atrybuty
| Nazwa | Typ | Opis |
| --- | --- | --- |
| **ProgramId**<br /><br /> Wymagane |**xs:int** |Identyfikator programu |
| **NumberOfPrograms**<br /><br /> Wymagane |**xs:int** |Liczba programów. |
| **PmtPid**<br /><br /> Wymagane |**xs:int** |Program mapy tabele (PMTs) zawierają informacje o programach.  Aby uzyskać więcej informacji, zobacz [rata](http://en.wikipedia.org/wiki/MPEG_transport_stream#PMT). |
| **PcrPid**<br /><br /> Wymagane |**xs:int** |Używany przez dekodera. Aby uzyskać więcej informacji, zobacz [PCR](http://en.wikipedia.org/wiki/MPEG_transport_stream#PCR) |
| **StartPTS** |**xs: długa** |Sygnatura czasowa rozpoczęcia prezentacji. |
| **EndPTS** |**xs: długa** |Końcowa sygnatura czasowa prezentacji. |

## <a name="StreamDispositionType"></a>StreamDispositionType
**StreamDispositionType** jest typem złożonym globalne opisuje hello strumienia.  

Zobacz przykład XML na końcu tego tematu hello: [przykład XML](media-services-input-metadata-schema.md#xml).  

### <a name="attributes"></a>Atrybuty
| Nazwa | Typ | Opis |
| --- | --- | --- |
| **Domyślne**<br /><br /> Wymagane |**xs:int** |Ustawienie tego atrybutu tooindicate too1, to hello domyślne prezentacji. |
| **Dub**<br /><br /> Wymagane |**xs:int** |Ustaw ten atrybut too1 tooindicate jest hello dubbingu prezentacji. |
| **Oryginał**<br /><br /> Wymagane |**xs:int** |Ustaw ten atrybut tooindicate too1, jest to hello oryginalnej prezentacji. |
| **Komentarz**<br /><br /> Wymagane |**xs:int** |Ustaw ten atrybut too1 tooindicate Śledź zawiera komentarz. |
| **Tekst**<br /><br /> Wymagane |**xs:int** |Ustaw ten atrybut too1 tooindicate Śledź zawiera tekst. |
| **Karaoke**<br /><br /> Wymagane |**xs:int** |Ustaw tooindicate too1 ten atrybut reprezentuje hello Śledź karaoke (muzyką w tle, nie vocals). |
| **Wymuszone**<br /><br /> Wymagane |**xs:int** |Ustawienie tego atrybutu tooindicate too1, to hello wymuszone prezentacji. |
| **HearingImpaired**<br /><br /> Wymagane |**xs:int** |Ustaw tooindicate too1 ten atrybut, którego hello niesłyszący tej ścieżki. |
| **VisualImpaired**<br /><br /> Wymagane |**xs:int** |Ustaw ten atrybut tooindicate too1, Śledź ten jest przeznaczony dla osób niedowidzących hello. |
| **CleanEffects**<br /><br /> Wymagane |**xs:int** |Ustaw tooindicate too1 tego atrybutu, ta ścieżka ma efekty czyste. |
| **AttachedPic**<br /><br /> Wymagane |**xs:int** |Ustawienie tego atrybutu tooindicate too1, ta ścieżka ma obrazów. |

## <a name="Programs"></a>Element programy
Element otoki zawierający wiele **Program** elementów.  

### <a name="child-elements"></a>Elementy podrzędne
| Nazwa | Typ | Opis |
| --- | --- | --- |
| **Program**<br /><br /> minOccurs = maxOccurs "0" = "unbounded" |[ProgramType](media-services-input-metadata-schema.md#ProgramType) |Dla plików zasobów, które są w formacie MPEG-TS zawiera informacje dotyczące programów w pliku trwałego hello. |

## <a name="VideoTracks"></a>VideoTracks element
 Element otoki zawierający wiele **VideoTrack** elementów.  

 Zobacz przykład XML na końcu tego tematu hello: [przykład XML](media-services-input-metadata-schema.md#xml).  

### <a name="child-elements"></a>Elementy podrzędne
| Nazwa | Typ | Opis |
| --- | --- | --- |
| **VideoTrack**<br /><br /> minOccurs = maxOccurs "0" = "unbounded" |[VideoTrackType (dziedziczy TrackType)](media-services-input-metadata-schema.md#VideoTrackType) |Zawiera informacje dotyczące ścieżki wideo w pliku trwałego hello. |

## <a name="AudioTracks"></a>AudioTracks element
 Element otoki zawierający wiele **AudioTrack** elementów.  

 Zobacz przykład XML na końcu tego tematu hello: [przykład XML](media-services-input-metadata-schema.md#xml).  

### <a name="elements"></a>Elementy
| Nazwa | Typ | Opis |
| --- | --- | --- |
| **AudioTrack**<br /><br /> minOccurs = maxOccurs "0" = "unbounded" |[AudioTrackType (dziedziczy TrackType)](media-services-input-metadata-schema.md#AudioTrackType) |Zawiera informacje dotyczące ścieżki audio w pliku trwałego hello. |

## <a name="code"></a>Kod schematu
    <?xml version="1.0" encoding="utf-8"?>  
    <xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:msdata="urn:schemas-microsoft-com:xml-msdata" version="1.0"  
               xmlns="http://schemas.microsoft.com/windowsazure/mediaservices/2014/07/mediaencoder/inputmetadata"  
               targetNamespace="http://schemas.microsoft.com/windowsazure/mediaservices/2014/07/mediaencoder/inputmetadata"  
               elementFormDefault="qualified">  

      <xs:complexType name="MetadataType">  
        <xs:attribute name="key"   type="xs:string" use="required"/>  
        <xs:attribute name="value" type="xs:string" use="required"/>  
      </xs:complexType>  

      <xs:complexType name="ProgramType">  
        <xs:attribute name="ProgramId" type="xs:int" use="required">  
          <xs:annotation>  
            <xs:documentation>Program Id</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="NumberOfPrograms" type="xs:int" use="required">  
          <xs:annotation>  
            <xs:documentation>Number of programs</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="PmtPid" type="xs:int" use="required">  
          <xs:annotation>  
            <xs:documentation>pmt pid</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="PcrPid" type="xs:int" use="required">  
          <xs:annotation>  
            <xs:documentation>pcr pid</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="StartPTS" type="xs:long">  
          <xs:annotation>  
            <xs:documentation>start pts</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="EndPTS" type="xs:long">  
          <xs:annotation>  
            <xs:documentation>end pts</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
      </xs:complexType>  

      <xs:complexType name="StreamDispositionType">  
        <xs:attribute name="Default"          type="xs:int" use="required" />  
        <xs:attribute name="Dub"              type="xs:int" use="required" />  
        <xs:attribute name="Original"         type="xs:int" use="required" />  
        <xs:attribute name="Comment"          type="xs:int" use="required" />  
        <xs:attribute name="Lyrics"           type="xs:int" use="required" />  
        <xs:attribute name="Karaoke"          type="xs:int" use="required" />  
        <xs:attribute name="Forced"           type="xs:int" use="required" />  
        <xs:attribute name="HearingImpaired"  type="xs:int" use="required" />  
        <xs:attribute name="VisualImpaired"   type="xs:int" use="required" />  
        <xs:attribute name="CleanEffects"     type="xs:int" use="required" />  
        <xs:attribute name="AttachedPic"      type="xs:int" use="required" />  
      </xs:complexType>  

      <xs:complexType name="TrackType" abstract="true">  
        <xs:sequence>  
          <xs:element name="Disposition" type="StreamDispositionType" minOccurs="0" maxOccurs="1"/>  
          <xs:element name="Metadata" type="MetadataType" minOccurs="0" maxOccurs="unbounded"/>  
        </xs:sequence>  
        <xs:attribute name="Id" use="required">  
          <xs:annotation>  
            <xs:documentation>zero-based index of this video track. Note: this is not necessarily hello TrackID as used in an MP4 file</xs:documentation>  
          </xs:annotation>  
          <xs:simpleType>  
            <xs:restriction base="xs:int">  
              <xs:minInclusive value="0"/>  
            </xs:restriction>  
          </xs:simpleType>  
        </xs:attribute>  
        <xs:attribute name="Codec" type="xs:string">  
          <xs:annotation>  
            <xs:documentation>video track codec string</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="CodecLongName" type="xs:string">  
          <xs:annotation>  
            <xs:documentation>video track codec long name</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="TimeBase"  type="xs:string" use="required">  
          <xs:annotation>  
            <xs:documentation>Time base. Example: TimeBase="1/48000"</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="NumberOfFrames">  
          <xs:annotation>  
            <xs:documentation>number of frames</xs:documentation>  
          </xs:annotation>  
          <xs:simpleType>  
            <xs:restriction base="xs:int">  
              <xs:minInclusive value="0"/>  
            </xs:restriction>  
          </xs:simpleType>  
        </xs:attribute>  
        <xs:attribute name="StartTime" type="xs:duration">  
          <xs:annotation>  
            <xs:documentation>Track start time. Example: StartTime="PT2.669S"</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
        <xs:attribute name="Duration" type="xs:duration">  
          <xs:annotation>  
            <xs:documentation>Track duration. Example: Duration="PT25M37.757S"</xs:documentation>  
          </xs:annotation>  
        </xs:attribute>  
      </xs:complexType>  

      <xs:complexType name="VideoTrackType">  
        <xs:annotation>  
          <xs:documentation>A specific video track in hello parent AssetFile</xs:documentation>  
        </xs:annotation>  
        <xs:complexContent>  
          <xs:extension base="TrackType">  
            <xs:attribute name="FourCC" type="xs:string" use="required">  
              <xs:annotation>  
                <xs:documentation>video codec FourCC code</xs:documentation>  
              </xs:annotation>  
            </xs:attribute>  
            <xs:attribute name="Profile" type="xs:string">  
              <xs:annotation>  
                <xs:documentation>profile</xs:documentation>  
              </xs:annotation>  
            </xs:attribute>  
            <xs:attribute name="Level" type="xs:string">  
              <xs:annotation>  
                <xs:documentation>level</xs:documentation>  
              </xs:annotation>  
            </xs:attribute>  
            <xs:attribute name="PixelFormat" type="xs:string">  
              <xs:annotation>  
                <xs:documentation>Video track's pixel format</xs:documentation>  
              </xs:annotation>  
            </xs:attribute>  
            <xs:attribute name="Width" use="required">  
              <xs:annotation>  
                <xs:documentation>encoded video width in pixels</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:int">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="Height" use="required">  
              <xs:annotation>  
                <xs:documentation>encoded video height in pixels</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:int">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="DisplayAspectRatioNumerator" use="required">  
              <xs:annotation>  
                <xs:documentation>video display aspect ratio numerator</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:double">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="DisplayAspectRatioDenominator" use="required">  
              <xs:annotation>  
                <xs:documentation>video display aspect ratio denominator</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:double">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="SampleAspectRatioNumerator">  
              <xs:annotation>  
                <xs:documentation>video sample aspect ratio numerator</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:double">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="SampleAspectRatioDenominator">  
              <xs:annotation>  
                <xs:documentation>video sample aspect ratio denominator</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:double">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="FrameRate" use="required">  
              <xs:annotation>  
                <xs:documentation>measured video frame rate in .3f format</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:decimal">  
                  <xs:minInclusive value="0"/>  
                  <xs:fractionDigits value="3"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="Bitrate">  
              <xs:annotation>  
                <xs:documentation>average video bit rate in kilobits per second, as calculated from hello AssetFile. Counts only hello elementary stream payload, and does not include hello packaging overhead</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:int">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="MaxGOPBitrate">  
              <xs:annotation>  
                <xs:documentation>Max GOP average bitrate for this video track, in kilobits per second</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:int">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="HasBFrames" type="xs:int">  
              <xs:annotation>  
                <xs:documentation>video track number of B frames</xs:documentation>  
              </xs:annotation>  
            </xs:attribute>  
          </xs:extension>  
        </xs:complexContent>  
      </xs:complexType>  

      <xs:complexType name="AudioTrackType">  
        <xs:annotation>  
          <xs:documentation>a specific audio track in hello parent AssetFile</xs:documentation>  
        </xs:annotation>  
        <xs:complexContent>  
          <xs:extension base="TrackType">  
            <xs:attribute name="SampleFormat"  type="xs:string">  
              <xs:annotation>  
                <xs:documentation>sample format</xs:documentation>  
              </xs:annotation>  
            </xs:attribute>  
            <xs:attribute name="ChannelLayout"  type="xs:string">  
              <xs:annotation>  
                <xs:documentation>channel layout</xs:documentation>  
              </xs:annotation>  
            </xs:attribute>  
            <xs:attribute name="Channels" use="required">  
              <xs:annotation>  
                <xs:documentation>number of audio channels</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:int">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="SamplingRate" use="required">  
              <xs:annotation>  
                <xs:documentation>audio sampling rate in samples/sec or Hz</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:int">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="Bitrate">  
              <xs:annotation>  
                <xs:documentation>average audio bit rate in bits per second, as calculated from hello AssetFile. Counts only hello elementary stream payload, and does not include hello packaging overhead</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:int">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
            <xs:attribute name="BitsPerSample">  
              <xs:annotation>  
                <xs:documentation>Bits per sample for hello wFormatTag format type</xs:documentation>  
              </xs:annotation>  
              <xs:simpleType>  
                <xs:restriction base="xs:int">  
                  <xs:minInclusive value="0"/>  
                </xs:restriction>  
              </xs:simpleType>  
            </xs:attribute>  
          </xs:extension>  
        </xs:complexContent>  
      </xs:complexType>  

      <xs:element name="AssetFiles">  
        <xs:annotation>  
          <xs:documentation>Collection of AssetFile entries for hello encoding job</xs:documentation>  
        </xs:annotation>  
        <xs:complexType>  
          <xs:sequence>  
            <xs:element name="AssetFile" minOccurs="1" maxOccurs="unbounded">  
              <xs:annotation>  
                <xs:documentation>asset file</xs:documentation>  
              </xs:annotation>  
              <xs:complexType>  
                <xs:sequence>  
                  <xs:element name="Programs" minOccurs="0">  
                    <xs:annotation>  
                      <xs:documentation>This is hello collection of all programs when file is MPEG-TS</xs:documentation>  
                    </xs:annotation>  
                    <xs:complexType>  
                      <xs:sequence>  
                        <xs:element name="Program" type="ProgramType" minOccurs="0" maxOccurs="unbounded" />  
                      </xs:sequence>  
                    </xs:complexType>  
                  </xs:element>  
                  <xs:element name="VideoTracks" minOccurs="0">  
                    <xs:annotation>  
                      <xs:documentation>Each physical AssetFile can contain in it zero or more video tracks interleaved into an appropriate container format. This is hello collection of all those video tracks</xs:documentation>  
                    </xs:annotation>  
                    <xs:complexType>  
                      <xs:sequence>  
                        <xs:element name="VideoTrack" type="VideoTrackType" minOccurs="0" maxOccurs="unbounded" />  
                      </xs:sequence>  
                    </xs:complexType>  
                  </xs:element>  
                  <xs:element name="AudioTracks" minOccurs="0">  
                    <xs:annotation>  
                      <xs:documentation>each physical AssetFile can contain in it zero or more audio tracks interleaved into an appropriate container format. This is hello collection of all those audio tracks</xs:documentation>  
                    </xs:annotation>  
                    <xs:complexType>  
                      <xs:sequence>  
                        <xs:element name="AudioTrack" type="AudioTrackType" minOccurs="0" maxOccurs="unbounded" />  
                      </xs:sequence>  
                    </xs:complexType>  
                  </xs:element>  
                  <xs:element name="Metadata" type="MetadataType" minOccurs="0" maxOccurs="unbounded" />  
                </xs:sequence>  
                <xs:attribute name="Name" type="xs:string" use="required">  
                  <xs:annotation>  
                    <xs:documentation>hello media asset file name</xs:documentation>  
                  </xs:annotation>  
                </xs:attribute>  
                <xs:attribute name="Size" use="required">  
                  <xs:annotation>  
                    <xs:documentation>size of file in bytes</xs:documentation>  
                  </xs:annotation>  
                  <xs:simpleType>  
                    <xs:restriction base="xs:long">  
                      <xs:minInclusive value="0"/>  
                    </xs:restriction>  
                  </xs:simpleType>  
                </xs:attribute>  
                <xs:attribute name="Duration" type="xs:duration" use="required">  
                  <xs:annotation>  
                    <xs:documentation>content play back duration. Example: Duration="PT25M37.757S"</xs:documentation>  
                  </xs:annotation>  
                </xs:attribute>  
                <xs:attribute name="NumberOfStreams" type="xs:int" use="required">  
                  <xs:annotation>  
                    <xs:documentation>number of streams in asset file</xs:documentation>  
                  </xs:annotation>  
                </xs:attribute>  
                <xs:attribute name="FormatNames" type="xs:string" use="required">  
                  <xs:annotation>  
                    <xs:documentation>format names</xs:documentation>  
                  </xs:annotation>  
                </xs:attribute>  
                <xs:attribute name="FormatVerboseName" type="xs:string" use="required">  
                  <xs:annotation>  
                    <xs:documentation>format verbose names</xs:documentation>  
                  </xs:annotation>  
                </xs:attribute>  
                <xs:attribute name="StartTime" type="xs:duration">  
                  <xs:annotation>  
                    <xs:documentation>content start time. Example: StartTime="PT2.669S"</xs:documentation>  
                  </xs:annotation>  
                </xs:attribute>  
                <xs:attribute name="OverallBitRate">  
                  <xs:annotation>  
                    <xs:documentation>average bitrate of hello asset file in kbps</xs:documentation>  
                  </xs:annotation>  
                  <xs:simpleType>  
                    <xs:restriction base="xs:int">  
                      <xs:minInclusive value="0"/>  
                    </xs:restriction>  
                  </xs:simpleType>  
                </xs:attribute>  
              </xs:complexType>  
            </xs:element>  
          </xs:sequence>  
        </xs:complexType>  
      </xs:element>  
    </xs:schema>  


## <a name="xml"></a>Przykład pliku XML
Hello poniżej znajduje się przykład pliku metadanych hello danych wejściowych.  

    <?xml version="1.0" encoding="utf-8"?>  
    <AssetFiles xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns="http://schemas.microsoft.com/windowsazure/mediaservices/2014/07/mediaencoder/inputmetadata">  
      <AssetFile Name="bear.mp4" Size="1973733" Duration="PT12.678S" NumberOfStreams="2" FormatNames="mov,mp4,m4a,3gp,3g2,mj2" FormatVerboseName="QuickTime / MOV" StartTime="PT0S" OverallBitRate="1245">  
        <VideoTracks>  
          <VideoTrack Id="1" Codec="h264" CodecLongName="H.264 / AVC / MPEG-4 AVC / MPEG-4 part 10" TimeBase="1/29970" NumberOfFrames="375" StartTime="PT0.034S" Duration="PT12.645S" FourCC="avc1" Profile="High" Level="4.1" PixelFormat="yuv420p" Width="512" Height="384" DisplayAspectRatioNumerator="4" DisplayAspectRatioDenominator="3" SampleAspectRatioNumerator="1" SampleAspectRatioDenominator="1" FrameRate="29.656" Bitrate="1043" HasBFrames="1">  
            <Disposition Default="1" Dub="0" Original="0" Comment="0" Lyrics="0" Karaoke="0" Forced="0" HearingImpaired="0" VisualImpaired="0" CleanEffects="0" AttachedPic="0" />  
            <Metadata key="creation_time" value="2010-03-10 16:11:56" />  
            <Metadata key="language" value="eng" />  
            <Metadata key="handler_name" value="Mainconcept MP4 Video Media Handler" />  
          </VideoTrack>  
        </VideoTracks>  
        <AudioTracks>  
          <AudioTrack Id="0" Codec="aac" CodecLongName="AAC (Advanced Audio Coding)" TimeBase="1/44100" NumberOfFrames="546" StartTime="PT0S" Duration="PT12.678S" SampleFormat="fltp" ChannelLayout="stereo" Channels="2" SamplingRate="44100" Bitrate="156" BitsPerSample="0">  
            <Disposition Default="1" Dub="0" Original="0" Comment="0" Lyrics="0" Karaoke="0" Forced="0" HearingImpaired="0" VisualImpaired="0" CleanEffects="0" AttachedPic="0" />  
            <Metadata key="creation_time" value="2010-03-10 16:11:56" />  
            <Metadata key="language" value="eng" />  
            <Metadata key="handler_name" value="Mainconcept MP4 Sound Media Handler" />  
          </AudioTrack>  
        </AudioTracks>  
        <Metadata key="major_brand" value="mp42" />  
        <Metadata key="minor_version" value="0" />  
        <Metadata key="compatible_brands" value="mp42mp41" />  
        <Metadata key="creation_time" value="2010-03-10 16:11:53" />  
        <Metadata key="comment" value="Courtesy of National Geographic.  Used by Permission." />  
      </AssetFile>  
    </AssetFiles>  

## <a name="next-steps"></a>Następne kroki
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Przekazywanie opinii
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

