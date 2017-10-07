---
title: "aaaEstimate wykorzystanie przepustowości sieci usługi Azure RemoteApp | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat hello wymagania dotyczące przepustowości sieci dla kolekcji usługi Azure RemoteApp i aplikacji."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 3127f4c7-f532-46c3-ba9b-649f647abec1
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 675ee82f26ddb46a3bb3e0ee95ed397e4064e45f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="estimate-azure-remoteapp-network-bandwidth-usage"></a>Szacowanie użycia przepustowości sieci usługi Azure RemoteApp
> [!IMPORTANT]
> Usługa Azure RemoteApp nie będzie obsługiwana od 31 sierpnia 2017 r. Witaj odczytu [anonsu](https://go.microsoft.com/fwlink/?linkid=821148) szczegółowe informacje.
> 
> 

Usługa Azure RemoteApp używa hello toocommunicate protokołu RDP (Remote Desktop) między aplikacjami działającymi w hello chmury Azure i użytkowników. Ten artykuł zawiera podstawowe wskazówki można użyć tooestimate użycie sieci, które potencjalnie ocenę użycia przepustowości sieci dla poszczególnych użytkowników usługi Azure RemoteApp.

Szacowanie przepustowości dla każdego użytkownika jest bardzo złożone i wymaga korzystania z wielu aplikacji jednocześnie w scenariuszach wielozadaniowości których aplikacje mogą mieć wpływ na siebie nawzajem wydajności z uwzględnieniem ich zapotrzebowanie na przepustowość sieci. Typ nawet powitania klienta pulpitu zdalnego (na przykład klient dla komputerów Mac i HTML5 klienta) może spowodować toodifferent przepustowości wyników. toohelp pracy za pośrednictwem tych komplikacji, firma Microsoft będzie podzielić scenariusze użycia hello kilka hello typowych kategorii tooreplicate rzeczywistych scenariuszy. (Jeśli hello rzeczywistych scenariuszy jest oczywiście różnych kategorii i różni się przez użytkownika.)

Przed rozszerzana dalsze — należy pamiętać, że przyjęto założenie, RDP zapewnia dobre tooexcellent środowisko dla większości scenariuszy użycia w sieciach z opóźnieniem poniżej 120 ms i przepustowości ponad 5 MB — jest oparta na toodynamically możliwości jego RDP dostosować za pomocą hello dostępnej sieci przepustowość i hello oszacować wymagania dotyczące przepustowości aplikacji. W tym artykule wykracza poza tymi toolook "Większość scenariuszy użycia" hello krawędzi, gdzie scenariusze rozpocząć toounwind i środowisko użytkownika rozpoczyna się toodegrade.

Teraz sprawdź następujące artykuły szczegółowe hello, w tym tooconsider czynników, zalecenia dotyczące planu bazowego i jakie firma Microsoft nie zostały uwzględnione w naszej szacuje hello.

* [Jak przepustowości sieci i jakości środowisko pracy razem?](remoteapp-bandwidthexperience.md)
* [Użycie przepustowości sieci z niektórych typowych scenariuszy testowania](remoteapp-bandwidthtests.md)
* [Szybkie wytyczne, jeśli nie masz hello tootest czas lub możliwości](remoteapp-bandwidthguidelines.md)

## <a name="what-are-we-not-including"></a>Jakie firma Microsoft nie zawierają?
Po przejrzeniu hello proponowane testy i Nasze zalecenia dotyczące ogólnej (i niewątpliwie ogólny), należy pamiętać, że istnieje kilka czynników, które firma Microsoft nie należy wziąć pod uwagę. Na przykład Witaj komplikacji środowisko użytkownik podał hello asymetrycznego rodzaj przekazywania i pobierania przepustowości. Hello asymetrycznego rodzaj większości sieci Wi-Fi wpłynie również hello wydajności i wrażenie środowisko użytkownika hello. W scenariuszach interakcyjne hello podrzędne ruchu może niższy niż od początku, hello, co może zwiększyć liczbę hello utracone ramki wideo lub audio i dlatego wpływ hello użytkownika z punktu widzenia użytkownika hello przesyłania strumieniowego środowisko priorytety. Można uruchamiać własne toosee eksperymenty co to jest dobrym przypadek użycia określonego i sieci.

Mimo że omówimy przekierowywania firma Microsoft nie uwzględniła wpływ przepustowości hello brany pod uwagę ruch sieciowy hello spowodowane przez podłączone urządzenia, takie jak magazyn, drukarek, skanerów, kamer internetowych i inne urządzenia USB. Zazwyczaj Hello wpływu tych urządzeń tymczasowo wzrósł hello wymagania dotyczące przepustowości i zniknie po zakończeniu zadania hello. Ale jeśli często, że żądanie przepustowości może być dość zauważalne.

Również nie omówiono sposób wielu użytkowników może wpłynąć na innych użytkowników w ramach hello tej samej sieci. Na przykład wielu użytkowników korzystających z 4K wideo w sieci 100 MB/s może mieć znaczący wpływ na innych użytkowników w tej samej sieci, w trakcie toodo hello tego samego zadania. Niestety pobiera przeszkodę progresywnie wpływ hello toodetermine toogive współbieżnego użycia wspólnych lub obejmujące wszystkie zalecenia o jak hello system przeprowadza w agregacji. To wszystko, co możemy powiedzieć hello podstawowych technologii protokołu spowoduje hello najlepsze wykorzystanie hello dostępnej przepustowości sieci, że mają swoje ograniczenia.

