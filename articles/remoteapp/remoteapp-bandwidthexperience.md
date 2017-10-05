---
title: "Usługa Azure RemoteApp — jak przepustowości sieci i jakości środowisko pracy ze sobą? | Microsoft Docs"
description: "Informacje o wpływie jakość środowiska użytkownika przepustowości sieci w usłudze Azure RemoteApp."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 74ebc1fb-5187-4056-b08c-0e03b5ecaca6
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 74116902e973fba440b3c662fdf76202d052b4c8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-remoteapp---how-do-network-bandwidth-and-quality-of-experience-work-together"></a>Usługa Azure RemoteApp — jak przepustowości sieci i jakości środowisko pracy ze sobą?
> [!IMPORTANT]
> Usługa Azure RemoteApp nie będzie obsługiwana od 31 sierpnia 2017 r. Szczegółowe informacje zawiera [powiadomienie](https://go.microsoft.com/fwlink/?linkid=821148).
> 
> 

Kiedy przeglądasz [ogólne przepustowość sieci](remoteapp-bandwidth.md) wymagane usługi Azure RemoteApp, mieć na uwadze następujące czynniki — są to wszystkie część dynamicznego systemu, który ma wpływ na ogólną środowisko użytkownika. 

* **Dostępna przepustowość sieci i warunków sieciowych bieżącego** — zestaw parametrów (utraty, czas oczekiwania, zakłócenia) w tej samej sieci w danym momencie może wpłynąć na aplikacji przesyłania strumieniowego środowisko, co oznacza obniżona ogólną środowisko użytkownika. Przepustowość sieci jest funkcją przeciążenia, utraty losowego opóźnienia, ponieważ parametry te mają wpływ na mechanizmu kontroli przeciążenia, które z kolei formanty szybkość transmisji, aby uniknąć kolizji w.  Na przykład stratnej sieci lub sieci duże opóźnienie będzie interfejs użytkownika zły nawet w przypadku sieci z przepustowości 1000 MB. Utraty i opóźnienia różnić w zależności od liczby użytkowników znajdujących się w tej samej sieci i co robią użytkownicy tych (na przykład obejrzeć filmy wideo, pobierania lub przekazywania duże pliki, drukowania).
* **Scenariusz użycia** — środowisko zależy od tego, co użytkownicy wirtualni jako osoby i grupy w tej samej sieci. Na przykład Odczyt jeden slajd wymaga tylko jedną ramkę zaktualizowania; Jeśli użytkownik skims i przewija zawartości dokumentu tekstowego, potrzebna jest większa liczba klatek na sekundę aktualizacji. Komunikację i z powrotem do serwera w tym scenariuszu po pewnym czasie będzie korzystać z większej przepustowości sieci. Należy również rozważyć extreme przykład: wielu użytkowników są obejrzeć filmy wideo wysokiej rozdzielczości (na przykład rozdzielczość 4K), zawierający rozmów konferencyjnych HD, granie w gry wideo 3D lub działa w systemach CAD. Wszystkie te można wprowadzać nawet naprawdę dużej przepustowości sieci praktycznie bezużyteczny.
* **Ekranu rozdzielczość i liczbę ekranów** -większą przepustowość sieci jest wymagana do pełnej aktualizacji ekranów większy niż mniejszych ekranach. Podstawową technologią potrafi pretty kodowania i przesyłania tylko regiony ekrany, które zostały zaktualizowane, ale okazjonalnie, cały ekran musi zostać zaktualizowany. Gdy użytkownik ma wyższy rozdzielczość ekranu (na przykład rozdzielczość 4K), aktualizacja wymaga większe obciążenie przepustowości sieci niż ekranu z niższej rozdzielczości (na przykład 1024x768px). Ta sama logika ma zastosowanie, jeśli używasz więcej niż jednego ekranu dla przekierowania. Przepustowość należy zwiększyć liczbę ekranów.
* **Przekierowanie do Schowka i urządzenia** — jest to problem nie bardzo oczywista, ale w wielu przypadkach, jeśli użytkownik zapisuje dużych fragmentów danych do Schowka, zajmuje nieco czasu dla tych informacji do przesłania z klienta usług pulpitu zdalnego na serwer. Środowisko podrzędne można wpływ na środowisko przesyłania zawartości Schowka od początku. To samo dotyczy przekierowywania - skanera lub kamera internetowa generuje dużą ilość danych, który musi być wysyłane do serwera nadrzędnego, czy drukarka musi odbierać dużego dokumentu lub lokalnego magazynu musi być dostępna dla aplikacji w chmurze do skopiowania plików o dużym, użytkownicy mogą zauważyć porzuconych ramki lub tymczasowo wideo "zablokowane", ponieważ dane potrzebne do przekierowania urządzenia zwiększa przepustowość sieci musi. 

Podczas oceny potrzeb przepustowości sieci, upewnij się, że należy wziąć pod uwagę wszystkie te czynniki pracy jako system.

Teraz, przejdź wstecz do [artykułu przepustowości sieci głównego](remoteapp-bandwidth.md), lub przejść do testowania programu [przepustowość sieci](remoteapp-bandwidthtests.md).

## <a name="learn-more"></a>Dowiedz się więcej
* [Szacowanie użycia przepustowości sieci usługi Azure RemoteApp](remoteapp-bandwidth.md)
* [Usługa Azure RemoteApp — użycie przepustowości sieci z niektórych typowych scenariuszy testowania](remoteapp-bandwidthtests.md)
* [Azure RemoteApp przepustowość sieci — ogólne wytyczne (Jeśli użytkownik nie może przetestować własnych)](remoteapp-bandwidthguidelines.md)

