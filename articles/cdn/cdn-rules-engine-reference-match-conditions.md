---
title: "Aparat dopasowania warunki reguły aaaAzure CDN | Dokumentacja firmy Microsoft"
description: "Dokumentacja referencyjna dla usługi Azure CDN zasady warunków dopasowania aparatu i funkcje."
services: cdn
documentationcenter: 
author: Lichard
manager: akucer
editor: 
ms.assetid: 669ef140-a6dd-4b62-9b9d-3f375a14215e
ms.service: cdn
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: rli
ms.openlocfilehash: 5e79f8f0c75a646e13bf315c492b9f2a9defc396
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cdn-rules-engine-match-conditions"></a>Pasujące aparatu reguł usługi Azure CDN
Ten temat listy szczegółowe opisy hello dostępnych warunków dopasowania dla Azure Content Delivery Network (CDN) [aparatu reguł](cdn-rules-engine.md).

druga część Hello reguły to hello dopasowania warunku. Warunek dopasowania identyfikuje określone typy żądań, dla których będą wykonywane zestawem funkcji.

Na przykład może być używane toofilter żądań zawartości w określonej lokalizacji, żądania generowane z określonego adresu IP lub kraju lub informacje o nagłówku.

## <a name="always"></a>Zawsze

Witaj zawsze dopasowania warunek jest zaprojektowana tooapply domyślny zestaw funkcji tooall żądań.

## <a name="device"></a>Urządzenie

Witaj urządzenia dopasowania warunek identyfikuje żądań wysyłanych z urządzenia przenośnego na podstawie jego właściwości.  Wykrywanie urządzenia przenośnego odbywa się za pośrednictwem [WURFL](http://wurfl.sourceforge.net/).  Poniżej przedstawiono możliwości WURFL oraz ich zmienne aparatu reguł CDN.

> [!NOTE] 
> Poniższe zmienne Hello są obsługiwane w hello **modyfikowania nagłówka żądania klienta** i **zmodyfikować nagłówek odpowiedzi klienta** funkcji.

Możliwości | Zmienna | Opis | Przykładowe wartości
-----------|----------|-------------|----------------
Nazwa marki | % {wurfl_cap_brand_name} | Ciąg, który wskazuje nazwę marki hello hello urządzenia. | Samsung
System operacyjny urządzenia | % {wurfl_cap_device_os} | Ciąg, który wskazuje hello system operacyjny zainstalowany na urządzeniu hello. | DLA SYSTEMU IOS
Wersja systemu operacyjnego urządzenia | % {wurfl_cap_device_os_version} | Ciąg, który wskazuje hello numer wersji systemu operacyjnego zainstalowanego na urządzeniu hello hello. | 1.0.1
Podwójna orientacji | % {wurfl_cap_dual_orientation} | Wartość logiczna, która wskazuje, czy urządzenie hello obsługuje dwa orientacji. | Wartość true
HTML preferowane DTD | % {wurfl_cap_html_preferred_dtd} | Ciąg, który wskazuje definicja typu dokumentu preferowanych hello urządzeń przenośnych (DTD) dla zawartości HTML. | Brak<br/>xhtml_basic<br/>HTML5
Obraz ze Śródwierszowaniem | % {wurfl_cap_image_inlining} | Wartość logiczna, która wskazuje, czy urządzenie hello obsługuje Base64 zakodowany obrazów. | wartość false
Jest systemu Android | % {wurfl_vcap_is_android} | Wartość logiczna, która wskazuje, czy urządzenie hello używa hello system operacyjny Android. | Wartość true
IOS | % {wurfl_vcap_is_ios} | Wartość logiczna wskazująca, czy urządzenie hello korzysta z systemem iOS. | wartość false
Jest inteligentne TV | % {wurfl_cap_is_smarttv} | Wartość logiczna wskazująca, czy urządzenie hello jest inteligentne TV. | wartość false
Jest Smartphone | % {wurfl_vcap_is_smartphone} | Wartość logiczna wskazująca, czy urządzenie hello jest smartfona. | Wartość true
Jest typu Tablet | % {wurfl_cap_is_tablet} | Wartość logiczna wskazująca, czy urządzenie hello jest komputerze typu tablet. Jest to opis niezależny od systemu operacyjnego. | Wartość true
To urządzenie sieci bezprzewodowej | % {wurfl_cap_is_wireless_device} | Wartość logiczna wskazująca, czy urządzenie hello jest uznawane za urządzeniem sieci bezprzewodowej. | Wartość true
Nazwa Marketing | % {wurfl_cap_marketing_name} | Ciąg, który wskazuje nazwę marketing hello urządzenia. | Perłowej blackBerry 8100
Przeglądarkę dla telefonów | % {wurfl_cap_mobile_browser} | Ciąg, który wskazuje przeglądarki hello używane toorequest zawartości z hello urządzenia. | Chrome
Wersja przenośnego przeglądarki | % {wurfl_cap_mobile_browser_version} | Ciąg wskazujący wersję hello przeglądarki hello używane toorequest zawartości z hello urządzenia. | 31
Nazwa modelu | % {wurfl_cap_model_name} | Ciąg, który wskazuje nazwę modelu hello urządzenia. | S3
Pobierania progresywnego | % {wurfl_cap_progressive_download} | Wartość logiczna, która wskazuje, czy urządzenie hello obsługuje hello odtwarzania audio i wideo, gdy nadal są pobierane. | Wartość true
Data wydania | % {wurfl_cap_release_date} | Ciąg, który wskazuje hello rok i miesiąc, na które hello urządzenie było dodać toohello WURFL w bazie danych.<br/><br/>Format:`yyyy_mm` | 2013_december
Wysokość rozwiązania | % {wurfl_cap_resolution_height} | Liczba całkowita, która wskazuje urządzenie hello wysokość w pikselach. | 768
Szerokość rozwiązania | % {wurfl_cap_resolution_width} | Liczba całkowita, która wskazuje urządzenie hello szerokość w pikselach. | 1024


## <a name="location"></a>Lokalizacja

Spełniają te warunki są zaprojektowane tooidentify żądania na podstawie lokalizacji hello żądającego.

Nazwa | Przeznaczenie
-----|--------
JAKO liczba | Identyfikuje żądań pochodzących z określoną siecią.
Kraj | Identyfikuje żądań pochodzących z określonych hello krajach.


## <a name="origin"></a>Origin

Spełniają te warunki są zaprojektowane tooidentify żądań magazynu punktu tooCDN lub serwera pochodzenia klienta.

Nazwa | Przeznaczenie
-----|--------
Źródła usługi CDN | Identyfikuje żądania dotyczące zawartości przechowywanej w sieci CDN w warstwie magazynu.
Pochodzenie klienta | Identyfikuje żądania dotyczące zawartości przechowywanej na serwerze źródłowym określonego klienta.


## <a name="request"></a>Żądanie

Spełniają te warunki są zaprojektowane tooidentify żądania na podstawie ich właściwości.

Nazwa | Przeznaczenie
-----|--------
Adres IP klienta | Identyfikuje żądań pochodzących z określonego adresu IP.
Parametr pliku cookie | Kontrole hello pliki cookie skojarzone z każdym żądaniem dla hello określona wartość.
Wyrażenie regularne parametru pliku cookie | Sprawdza, czy hello pliki cookie skojarzone z każdym żądaniem dla hello określone wyrażenie regularne.
Krawędź Cname | Identyfikuje żądań, które wskazują tooa określonej krawędzi CNAME.
Odwoływanie domeny | Identyfikuje żądań, które zostały przekazane z hello określony hostname(s).
Literał nagłówka żądania | Identyfikuje żądań, które zawierają hello określony nagłówek set tooa określonej wartości.
Wyrażenie regularne nagłówka żądania | Identyfikuje żądań, które zawierają hello określony nagłówek Ustaw tooa wartość odpowiadającą hello określone wyrażenie regularne.
Symbol wieloznaczny nagłówka żądania | Identyfikuje żądań, które zawierają hello określony nagłówek wartość tooa odpowiadający hello określony wzorzec.
Request — metoda | Identyfikuje żądań ich metodą HTTP.
Schemat żądania | Identyfikuje żądań przez ich protokołu HTTP.

## <a name="url"></a>ADRES URL

Są zgodne z warunkami określonymi żądań zaprojektowanego tooidentify oparte na ich adresy URL.

Nazwa | Przeznaczenie
-----|--------
Adres URL ścieżki katalogu | Identyfikuje żądania za pomocą ich ścieżek względnych.
Rozszerzenie ścieżki adresu URL | Identyfikuje żądania za pomocą ich rozszerzenia nazwy pliku.
Nazwa pliku ścieżki adresu URL | Identyfikuje żądań według ich nazwy pliku.
Literał ścieżki adresu URL | Porównuje żądania do ścieżki względnej toohello określona wartość.
Wyrażenie regularne ścieżki adresu URL | Porównuje żądania do ścieżki względnej toohello określony wyrażenia regularnego.
Symbol wieloznaczny ścieżki adresu URL | Porównuje określony wzorzec toohello względna ścieżka żądania.
Adres URL zapytania literału | Porównuje żądanie obiektu toohello ciągu zapytania określona wartość.
Adres URL parametru zapytania | Identyfikuje żądań, które zawierają hello określonego zapytania parametr ciągu ustawić wartość tooa, która jest zgodna z określonym wzorcem.
Adres URL zapytania Regex | Identyfikuje żądań, które zawierają hello określonego zapytania parametr ciągu ustawić wartość tooa, który odpowiada określonemu wyrażeniu regularnemu.
Adres URL zapytania z symboli wieloznacznych | Porównuje hello określonej wartości z ciągu zapytania żądania hello.


## <a name="next-steps"></a>Następne kroki
* [Omówienie usługi Azure CDN](cdn-overview.md)
* [Odwołanie do aparatu reguł](cdn-rules-engine-reference.md)
* [Wyrażenia warunkowe aparatu reguł](cdn-rules-engine-reference-conditional-expressions.md)
* [Funkcje aparatu reguł](cdn-rules-engine-reference-features.md)
* [Zastępowanie domyślnego zachowania HTTP przy użyciu aparatu reguł hello](cdn-rules-engine.md)

