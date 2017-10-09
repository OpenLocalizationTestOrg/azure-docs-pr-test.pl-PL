---
title: "aaaAzure RemoteApp — jak przepustowości sieci i jakości środowisko pracy ze sobą? | Microsoft Docs"
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
ms.openlocfilehash: 62b0caadf63359eceb63d27fae6ad289b682ff63
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-remoteapp---how-do-network-bandwidth-and-quality-of-experience-work-together"></a>Usługa Azure RemoteApp — jak przepustowości sieci i jakości środowisko pracy ze sobą?
> [!IMPORTANT]
> Usługa Azure RemoteApp nie będzie obsługiwana od 31 sierpnia 2017 r. Witaj odczytu [anonsu](https://go.microsoft.com/fwlink/?linkid=821148) szczegółowe informacje.
> 
> 

Kiedy przeglądasz hello [ogólne przepustowość sieci](remoteapp-bandwidth.md) wymagane usługi Azure RemoteApp, przechowywać w hello uwzględnić następujące czynniki — są to wszystkie części dynamiczny system, że wpływ hello ogólną użytkowników. 

* **Dostępna przepustowość sieci i warunków sieciowych bieżącego** — zestaw parametrów (utraty, czas oczekiwania, zakłócenia) na powitania sam sieci w danym momencie może wpłynąć na aplikacji hello przesyłania strumieniowego środowisko, co oznacza obniżona, ogólną użytkowników. Hello przepustowości w sieci jest funkcją przeciążenia, utraty losowego opóźnienia, ponieważ te parametry wpływ na powitania mechanizmu kontroli przeciążenia, które w formantach Włącz hello kolizji tooavoid szybkość transmisji.  Na przykład stratnej sieci lub sieci duże opóźnienie będzie interfejs użytkownika hello zły nawet w przypadku sieci z przepustowości 1000 MB. utrata Hello i opóźnienia różnić w zależności od hello liczbę użytkowników, którzy znajdują się na powitania tej samej sieci i co robią użytkownicy tych (na przykład obejrzeć filmy wideo, pobierania lub przekazywania duże pliki, drukowania).
* **Scenariusz użycia** — środowisko hello zależy od tego, jakie hello robią użytkownicy jako osoby i grupy na powitania sam sieci. Na przykład Odczyt jeden slajd wymaga tylko toobe jednej ramce, które są aktualizowane; Jeśli użytkownik hello skims i przewija hello zawartości dokumentu tekstowego, muszą większej liczby toobe ramki zaktualizowane na sekundę. Witaj ponownie komunikację i określonymi toohello serwera w tym scenariuszu zostanie ostatecznie korzystać z większej przepustowości sieci. Należy również rozważyć extreme przykład: wielu użytkowników są obejrzeć filmy wideo wysokiej rozdzielczości (na przykład rozdzielczość 4K), zawierający rozmów konferencyjnych HD, granie w gry wideo 3D lub działa w systemach CAD. Wszystkie te można wprowadzać nawet naprawdę dużej przepustowości sieci praktycznie bezużyteczny.
* **Rozdzielczość i hello liczbę ekranów ekranu** -większą przepustowość sieci jest wymagana toofull aktualizacji ekrany większy niż mniejszych ekranach. podstawową technologią Hello potrafi pretty kodowania i przesyłania tylko hello regiony ekranów powitalnych, które zostały zaktualizowane, ale okazjonalnie, cały ekran hello wymagane toobe aktualizacji. Gdy użytkownik hello ma wyższy rozdzielczość ekranu (na przykład rozdzielczość 4K), aktualizacja wymaga większe obciążenie przepustowości sieci niż ekranu z niższej rozdzielczości (na przykład 1024x768px). Ta sama logika ma zastosowanie, jeśli używasz więcej niż jednego ekranu dla przekierowania. Przepustowość musi tooincrease o numerze hello ekranów.
* **Przekierowanie do Schowka i urządzenia** — jest to problem nie bardzo oczywista, ale w wielu przypadkach Jeśli użytkownik zapisuje dużych fragment danych toohello Schowek, zajmuje nieco czasu dla tego tootransfer informacje z klienta usług pulpitu zdalnego hello toohello serwera. środowisko podrzędne Hello można wpływ na środowisko hello wysyłanie zawartości Schowka powitania od początku. Hello samo dotyczy przekierowywanie urządzeń — Jeśli skaner lub kamera internetowa generuje dużą ilość danych wymagającego toobe wysyłane toohello nadrzędnego serwera, drukarki musi tooreceive dużego dokumentu lub lokalnej pamięci masowej musi toobe dostępne tooan uruchomieniu aplikacji w hello toocopy chmury dużych plików, użytkownicy mogą zauważyć porzuconych ramki lub tymczasowo wideo "zablokowane" ponieważ hello dane potrzebne do przekierowywania hello zwiększa przepustowość sieci hello wymaga. 

Podczas oceny potrzeb przepustowości sieci, upewnij się, że tooconsider wszystkie te czynniki pracy jako system.

Teraz, przejdź wstecz toohello [artykułu przepustowości sieci głównego](remoteapp-bandwidth.md), albo przenieś tootesting Twojego [przepustowość sieci](remoteapp-bandwidthtests.md).

## <a name="learn-more"></a>Dowiedz się więcej
* [Szacowanie użycia przepustowości sieci usługi Azure RemoteApp](remoteapp-bandwidth.md)
* [Usługa Azure RemoteApp — użycie przepustowości sieci z niektórych typowych scenariuszy testowania](remoteapp-bandwidthtests.md)
* [Azure RemoteApp przepustowość sieci — ogólne wytyczne (Jeśli użytkownik nie może przetestować własnych)](remoteapp-bandwidthguidelines.md)

