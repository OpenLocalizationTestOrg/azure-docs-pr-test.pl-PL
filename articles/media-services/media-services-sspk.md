---
title: "aaaLicensing Microsoft® Smooth Streaming klienta Eksportowanie zestawu"
description: "Więcej informacji na temat sposobu toolicensing hello Microsoft® Smooth Streaming klienta Eksportowanie zestawu."
services: media-services
documentationcenter: 
author: xpouyat
manager: cfowler
editor: 
ms.assetid: e3b488e7-8428-4c10-a072-eb3af46c82ad
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: xpouyat
ms.openlocfilehash: 56c3dccda73dd02207bb4dbe8109ba6fda917a6b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="licensing-microsoft-smooth-streaming-client-porting-kit"></a>Licencjonowania Microsoft® Smooth Streaming Client Eksportowanie zestawu
## <a name="overview"></a>Omówienie
Microsoft Smooth Streaming klienta Eksportowanie zestawu (**SSPK** skrócie) jest Smooth Streaming implementacji klienta, który jest zoptymalizowany toohelp osadzonych producentów, kabel i operatorów komórkowych, zawartości usługodawcy, słuchawki producenci, niezależnym dostawcom oprogramowania (ISV) i rozwiązania dostawców toocreate produktów i usług do przesyłania strumieniowego z adaptacyjną przesyłania strumieniowego zawartości w formacie Smooth Streaming. SSPK jest platforma i urządzenie niezależnie od implementacji klienta Smooth Streaming, które mogą być przenoszone hello Licencjobiorcy tooany urządzeń i platform. 

Przedstawionym poniżej jest Architektura wysokiego poziomu, a pole IIS Smooth Streaming Eksportowanie zestawu jest obsługiwane przez firmę Microsoft implementacją Smooth Streaming Client hello zawiera całą logikę core hello do odtwarzania zawartości Smooth Streaming. Jest to następnie przenoszone przez partnerów dla określonego urządzenia lub platformy zaimplementowanie odpowiednich interfejsów. 

![SSPK](./media/media-services-sspk/sspk-arch.png)

## <a name="description"></a>Opis
SSPK jest licencjonowana na warunkach, które oferuje doskonałą biznesu. Licencja SSPK zapewnia branży hello:

* Smooth Streaming Eksportowanie zestawu źródła w języku C++ 
  * implementuje funkcje Smooth Streaming Client
  * dodaje format analizowania heurystyki buforowanie logiki itp.
* Aplikacja odtwarzacza interfejsów API 
  * interfejsy programowania do interakcji z aplikacją media player
* Interfejs (PAL) warstwy abstrakcji platformy 
  * interfejsy programowania do interakcji z systemem operacyjnym hello (wątki, sockets)
* Interfejs (HAL) warstwy abstrakcji sprzętu 
  * interfejsy do interakcji z urządzenia, A / V dekodery (dekodowania, renderowania)
* Interfejs zarządzania (prawami cyfrowymi DRM) prawami cyfrowymi 
  * interfejsy programowania obsługi DRM za pośrednictwem hello warstwę abstrakcji DRM (DAL)
  * Microsoft PlayReady eksportowanie Kit jest dostarczany oddzielnie, ale integruje się za pośrednictwem tego interfejsu. Więcej szczegółów dotyczących licencji firmy Microsoft PlayReady Device, kliknij przycisk [tutaj](http://www.microsoft.com/playready/licensing/device_technology.mspx#pddipdl).
* Przykłady implementacji 
  * Przykładowe zastosowanie PAL dla systemu Linux
  * Przykładowe zastosowanie HAL dla GStreamer

## <a name="licensing-options"></a>Opcje licencjonowania
Microsoft Smooth Streaming klienta eksportowanie Kit jest dokonane toolicensees dostępne w dwóch umów licencyjnych distinct: jeden dla rozwoju Smooth produktów przejściowej klienta przesyłania strumieniowego i drugi dla dystrybucji Smooth Streaming klienta produktów końcowych tooend użytkowników.

* Mikroukładem producentów, niezależnie od oprogramowania i integratorów systemów. platforma dostawcy (ISV), którzy potrzebują Eksportowanie kodu źródłowego zestaw toodevelop produktów przejściowej Microsoft Smooth Streaming klienta Eksportowanie zestawu **licencji produktu przejściowej** powinien być wykonywany.
* Dla producentów lub niezależnym dostawcom oprogramowania wymagających praw dystrybucji dla użytkowników tooend Smooth Streaming klienta produktów końcowych, hello Microsoft Smooth Streaming klienta Eksportowanie zestawu **końcowej licencji produktu** mają zostać wykonane.

### <a name="microsoft-smooth-streaming-client-porting-kit-interim-product-license"></a>Microsoft Smooth Streaming Client Eksportowanie zestawu przejściowej licencji produktu
W ramach tej licencji firmy Microsoft oferuje Smooth Streaming klienta Eksportowanie zestawu hello toodevelop prawa własności intelektualnej niezbędne i dystrybuować Smooth produktów przejściowej klienta przesyłania strumieniowego tooother Smooth Streaming klienta Eksportowanie zestawu urządzeń licencjobiorców który Dystrybuuj Smooth Streaming klienta produktów końcowych.

#### <a name="fee-structure"></a>Opłata — struktura
Opłata jednorazowej licencji USA $ 50 000 zapewnia dostęp toohello Smooth Streaming klienta Eksportowanie zestawu. 

### <a name="microsoft-smooth-streaming-client-porting-kit-final-product-license"></a>Microsoft Smooth Streaming Client Eksportowanie zestawu końcowa licencji produktu
W ramach tej licencji firma Microsoft oferuje wszystkie niezbędne tooreceive prawa własności intelektualnej Smooth produktów przejściowej klienta przesyłania strumieniowego z innych licencjobiorców Smooth Streaming klienta Eksportowanie zestawu i toodistribute znakowaniem firmowym Smooth Streaming klienta końcowego Użytkownicy tooend produktów.

#### <a name="fee-structure"></a>Opłata — struktura
Witaj Smooth Streaming klienta produktu końcowego jest oferowanych w ramach jako model licencjonowanych w ramach:

* wysłane 0.10 $ dla wdrożenia urządzenia
* Licencjonowani Hello jest ograniczone do 50 000 $ każdego roku
* Nie licencjonowanych w pierwszych 10 000 urządzeń implementacji każdego roku 

## <a name="licensing-procedure-and-sspk-access"></a>Procedurę licencjonowania i SSPK dostępu
Wyślij wiadomość e-mail [ sspkinfo@microsoft.com ](mailto:sspkinfo@microsoft.com) dla wszystkich licencjonowania zapytania.

Witaj [portal dystrybucji SSPK](https://microsoft.sharepoint.com/teams/SSPKDOWNLOAD/) jest dostępny tooregistered licencjobiorców przejściowej.

Licencjobiorców przejściowej i końcowe SSPK mogą przesyłać pytania techniczne zbyt[smoothpk@microsoft.com](mailto:smoothpk@microsoft.com).

## <a name="microsoft-smooth-streaming-client-interim-product-agreement-licensees"></a>Microsoft Smooth Streaming licencjobiorców umowy tymczasowe produktu klienta
* Adroit rozwiązań biznesowych, Inc
* Zaawansowane cyfrowy emisji SA
* AirTies Kablosuz Iletism Sanayive Dis Ticaret A.S.
* Albis technologii Ltd.
* Alticast Corporation
* Cyfrowy Amazon usług, Inc.
* Technologia Arion, Inc.
* Oprogramowanie Multimedia AVC Company, Ltd.
* Cavium, Inc.
* EchoStar Corporation zakupu
* Enseo, Inc.
* Fluendo SA
* BroadInfoCom HANDAN Company, Ltd.
* Infomir GMBH
* Irdeto USA Inc.
* iWEDIA SA 
* Liberty globalne BV usług
* MediaTek Inc.
* MStar Co, Ltd.
* Nintendo Company, Ltd.
* OpenTV, Inc.
* Ograniczone cyfrowy szafran
* Elektrycznego Changhong prowincji Syczuan Co., Ltd.
* SoftAtHome
* Sony Corporation
* Tatung technologii Inc.
* Electronics Technoly (Huizhou) TCL Company, Ltd.
* TOP zwycięstwa inwestycji, Ltd.
* Pisz Vestel Elektronik Sanayi Ticaret A.S.
* VisualOn, Inc.
* ZTE Corporation

## <a name="microsoft-smooth-streaming-client-final-product-agreement-licensees"></a>Microsoft Smooth Streaming licencjobiorców umowy produktu końcowego klienta
* Zaawansowane cyfrowy emisji SA
* AirTies Kablosuz Iletism Sanayive Dis Ticaret A.S.
* Albis technologii Ltd.
* Cyfrowy Amazon usług, Inc.
* Technologia AmTRAN Company, Ltd.
* Arcadyan technologii Corporation
* Technologia Arion, Inc.
* ATMACA ELEKTRONİK SIECI SAN. PISZ TİC. A.Ş
* Brytyjskie niebo emisji ograniczone
* Technologia CastPal, Inc., Shenzhen
* Compal Electronics, Inc.
* Dongguan cyfrowy AV technologii Corp., Ltd.
* EchoStar Corporation zakupu
* Enseo, Inc.
* Ograniczone filmów Filmflex
* Fluendo SA
* Ograniczone innowacje Gibson
* Haier informacji Applicantion S.R.L
* BroadInfoCom HANDAN Company, Ltd.
* Międzynarodowe Hisense Company, Ltd. 
* Homecast Co., Ltd.
* HON Hai dokładności branży Company, Ltd.
* Infomir GMBH
* Kaonmedia Company, Ltd.
* KDDI Corporation
* Nintendo Company, Ltd.
* Kolor pomarańczowy SA
* Ograniczone cyfrowy szafran
* Połączenie szerokopasmowe Sagemcom SAS
* Shenzhen Coship Electronics CO., Ltd.
* Elektrycznego Jiuzhou Shenzhen Co., Ltd.
* Shenzhen Skyworth cyfrowy technologii Co., Ltd.
* Elektrycznego Changhong prowincji Syczuan Company, Ltd.
* Skardin przemysłowej Corp.
* Niebo Deutschland Fernsehen GmbH & Co. KG
* SmarDTV SA
* SoftAtHome
* Sony Corporation
* Ograniczone TCL zamorskich Marketing (urządzeniach oddalonych od brzegu komercyjnej Makau SAR)
* Technicolor dostarczanie technologii, SAS
* Tongfang Ltd. globalne
* TOP zwycięstwa inwestycji, Ltd.
* Toshiba Lifestyle produktów i usług firma
* S.r.o. /Slovakia/ uniwersalnej Corporation nośnika
* VIZIO, Inc.
* Wistron Corporation
* ZTE Corporation


## <a name="media-services-learning-paths"></a>Ścieżki szkoleniowe dotyczące usługi Media Services
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Przekazywanie opinii
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

