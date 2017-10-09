---
title: "aaaOptimize Azure dostarczania zawartości dla danego scenariusza"
description: "Jak toooptimize dostarczania zawartości dla konkretnych scenariuszy"
services: cdn
documentationcenter: 
author: smcevoy
manager: erikre
editor: 
ms.assetid: 
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: v-semcev
ms.openlocfilehash: 922a92fdbf7e6e21f2b5ae9a2fb4ac32735fc15a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-azure-content-delivery-for-your-scenario"></a>Optymalizacja Azure dostarczania zawartości dla danego scenariusza

Dostarczanie zawartości tooa dużych globalnej grupy odbiorców jest krytyczne tooensure hello zoptymalizowanych pod kątem dostarczania zawartości. Hello Azure Content Delivery Network zoptymalizować hello dostarczania zależy hello typu zawartości, do których masz. Zawartość może być witryna sieci Web, strumień na żywo, wideo lub dużego pliku do pobrania. Po utworzeniu punktu końcowego (CDN) sieci dostarczania zawartości, określ scenariusza w hello **zoptymalizowane pod kątem** opcji. Wybór określa, które optymalizacji jest stosowane toohello zawartości z punktu końcowego CDN hello.

Opcje optymalizacji są zaprojektowane toouse zachowania sprawdzonych tooimprove dostarczania zawartości wydajności i odciążanie lepsze pochodzenia. Wybrane opcje scenariusz wpłynąć na wydajność, modyfikując konfiguracje dla częściowej pamięci podręcznej, obiekt segmentu i zasady ponawiania awarii pochodzenia hello. 

Ten artykuł zawiera omówienie różnych funkcji optymalizacji i kiedy należy używać. Aby uzyskać więcej informacji o funkcjach i ograniczenia zobacz artykuły odpowiednich hello na poszczególnych typach poszczególnych optymalizacji.

> [!NOTE]
> Twoje **zoptymalizowane pod kątem** opcje mogą różnić w zależności od dostawcy hello wybrania. Dostawcy sieci CDN zastosować rozszerzenia na różne sposoby, w zależności od scenariusza hello. 

## <a name="provider-options"></a>Opcje dostawcy

obsługuje Hello Azure Content Delivery Network from Akamai:

* Dostarczanie ogólne sieci web 

* Ogólne przesyłania strumieniowego multimediów

* Przesyłanie strumieniowe multimediów wideo na żądanie

* Pobieranie dużych plików

* Akceleracja dynamiczne witryny 

Hello Azure Content Delivery Network from Verizon obsługuje tylko dostarczania ogólne sieci web. Może służyć do wideo na żądanie i pobierania plików o dużym. Nie masz tooselect optymalizacji typu.

Zdecydowanie zaleca się przetestowanie wydajności różnice między optymalne dostawcy hello tooselect różnych dostawców dla firmy.

## <a name="select-and-configure-optimization-types"></a>Wybierz i skonfiguruj typy optymalizacji

toocreate nowy punkt końcowy, wybierz typ optymalizacji, który najlepiej spełnia wymagania hello scenariusza i typu zawartości, którą chcesz hello toodeliver punktu końcowego. **Ogólne web dostarczania** hello domyślny wybór. Można aktualizować hello opcji optymalizacji dla dowolnego istniejącego punktu końcowego Akamai w dowolnym momencie. Ta zmiana nie przerywać dostarczanie z hello CDN. 

1. Wybierz punkt końcowy w profilu Akamai standardowa.

    ![Punkt końcowy zaznaczenia ](./media/cdn-optimization-overview/01_Akamai.png)

2. W obszarze **ustawienia**, wybierz pozycję **optymalizacji**. Następnie wybierz typ z hello **zoptymalizowane pod kątem** listy rozwijanej.

    ![Wybór optymalizacji i typ](./media/cdn-optimization-overview/02_Select.png)

## <a name="optimization-for-specific-scenarios"></a>Optymalizacja dla konkretnych scenariuszy

Aby zoptymalizować hello punktu końcowego CDN dla jednego z następujących scenariuszy hello. 

### <a name="general-web-delivery"></a>Dostarczanie ogólne sieci web

Najbardziej typowych opcji optymalizacji hello jest dostarczana ogólne sieci web. Jest on przeznaczony dla optymalizacji zawartości ogólne sieci web, takich jak aplikacje sieci web i stron sieci Web. Tego rodzaju optymalizacji mogą służyć do pliku i pobierane pliki wideo.

Typowy witryny sieci Web zawiera zawartość statycznych i dynamicznych. Zawartość statyczna zawiera obrazy, biblioteki języka JavaScript i arkusze stylów, które mogą być buforowane i dostarczyć toodifferent użytkowników. Zawartość dynamiczna jest spersonalizowane dla poszczególnych użytkowników, takie jak wiadomości, które są dostosowane tooa profilu użytkownika. Zawartość dynamiczna nie jest pamięci podręcznej, ponieważ istnieje unikatowy tooeach użytkownika, takie jak zawartość koszyka zakupów. Dostarczanie ogólne sieci web można zoptymalizować całej witryny sieci Web. 

> [!NOTE]
> Jeśli używasz hello Azure Content Delivery Network from Akamai można toouse Optymalizacja Jeśli Twoje średni rozmiar pliku jest mniejsza niż 10 MB. Jeśli Twoje średni rozmiar pliku jest większy niż 10 MB, wybierz **pobierania plików o dużym** z hello **zoptymalizowane pod kątem** listy rozwijanej.

### <a name="general-media-streaming"></a>Ogólne przesyłania strumieniowego multimediów

Jeśli potrzebujesz punktu końcowego hello toouse transmisja strumieniowa na żywo i przesyłania strumieniowego wideo na żądanie, zaleca się ogólne multimediów strumieniowych optymalizacji.

Przesyłania strumieniowego multimediów jest czasowego, ponieważ pakiety przychodzące późno na powitania klienta może spowodować uszkodzenie wrażenia, takie jak częste buforowanie zawartości wideo. Multimediów strumieniowych optymalizacji zmniejsza opóźnienie hello dostarczania zawartości nośnika i zapewnia płynnego przesyłania strumieniowego dla użytkowników. 

Ten scenariusz jest typowy dla klientów usługi Azure media. Gdy używasz usługi Azure media services, możesz uzyskać jeden przesyłania strumieniowego punktu końcowego, który może służyć do przesyłania strumieniowego na żywo i na żądanie. W tym scenariuszu klienci nie muszą punktu końcowego tooanother tooswitch po zmianie z przesyłania strumieniowego na żywo tooon żądanie. Optymalizacja przesyłania strumieniowego multimediów ogólne obsługuje scenariusza tego typu.

Hello Azure Content Delivery Network from Verizon używa hello ogólne zawartości sieci web dostarczania optymalizacji typu toodeliver przesyłania strumieniowego multimediów.

toolearn więcej informacji na temat multimediów strumieniowych optymalizacji, zobacz [multimediów strumieniowych optymalizacji](cdn-media-streaming-optimization.md).

### <a name="video-on-demand-media-streaming"></a>Przesyłanie strumieniowe multimediów wideo na żądanie

Optymalizacja przesyłania strumieniowego multimediów wideo na żądanie poprawia przesyłania strumieniowego zawartości wideo na żądanie. Jeśli używasz punktu końcowego przesyłania strumieniowego wideo na żądanie można toouse tej opcji.

Hello Azure Content Delivery Network from Verizon używa hello ogólne zawartości sieci web dostarczania optymalizacji typu toodeliver przesyłania strumieniowego multimediów.

toolearn więcej informacji na temat multimediów strumieniowych optymalizacji, zobacz [multimediów strumieniowych optymalizacji](cdn-media-streaming-optimization.md).

> [!NOTE]
> Jeśli punkt końcowy hello służy głównie zawartości wideo na żądanie, użyj tego typu optymalizacji. Witaj główna różnica między tym optymalizacji i optymalizacji przesyłania strumieniowego multimediów ogólne hello jest limit ponownych prób połączenia hello. limit czasu Hello jest znacznie krótszy toowork ze scenariuszami transmisji strumieniowej na żywo.

### <a name="large-file-download"></a>Pobieranie dużych plików

Jeśli używasz hello Azure Content Delivery Network from Akamai, należy użyć plików toodeliver pobierania dużych plików większych niż 1,8 GB. Hello Azure Content Delivery Network from Verizon nie ma ograniczenia pliku pobrać rozmiar w jego optymalizację dostarczania ogólne sieci web.

Jeśli używasz hello Azure Content Delivery Network from Akamai pobierania dużych plików są zoptymalizowane pod kątem zawartości większych niż 10 MB. Jeśli Twoje średni rozmiar pliku jest mniejsza niż 10 MB, można toouse dostarczania ogólne sieci web. Jeśli Twoje rozmiary plików średni są stale większych niż 10 MB, może być efektywniejsze toocreate oddzielne punktu końcowego dla dużych plików. Aktualizacje oprogramowania układowego i oprogramowania są zwykle dużych plików.

Hello Azure Content Delivery Network from Verizon używa hello ogólne zawartości sieci web dostarczania optymalizacji typu toodeliver przesyłania strumieniowego multimediów.

toolearn więcej informacji na temat optymalizacji dużych plików, zobacz [optymalizacji plików o dużym](cdn-large-file-optimization.md).

### <a name="dynamic-site-acceleration"></a>Akceleracja dynamiczne witryny

 Akceleracja dynamiczne witryny jest dostępna z profilami zarówno Akamai i Verizon Content Delivery Network. Tego rodzaju optymalizacji obejmuje toouse dodatkowych opłat. Aby uzyskać więcej informacji zobacz hello cennik.

Akceleracja dynamiczne witryny obejmuje różne techniki, które korzystają hello opóźnienia i wydajności, zawartości dynamicznej. Techniki to m.in. optymalizacji trasy i sieci, optymalizacja protokołu TCP i inne. 

Możesz użyć tej optymalizacji tooaccelerate aplikacji sieci web, która zawiera wiele odpowiedzi, które nie są buforowalnej. Przykłady są wyniki wyszukiwania, transakcje wyewidencjonowania lub danych w czasie rzeczywistym. Można kontynuować toouse podstawowych CDN buforowania możliwości dla danych statycznych. 



