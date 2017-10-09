---
title: "przepustowość sieci trybu RemoteApp aaaAzure — ogólne wytyczne | Dokumentacja firmy Microsoft"
description: "Zrozumienie wskazówki przepustowości sieci podstawowej dla kolekcji usługi Azure RemoteApp i aplikacji."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 529bf318-ae37-4c14-a11c-43fa703d68a3
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: d3407eea71e2e8ac524787ee680cfd870c800864
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-remoteapp-network-bandwidth---general-guidelines-if-you-cant-test-your-own"></a>Azure RemoteApp przepustowość sieci — ogólne wytyczne (Jeśli użytkownik nie może przetestować własnych)
> [!IMPORTANT]
> Usługa Azure RemoteApp nie będzie obsługiwana od 31 sierpnia 2017 r. Witaj odczytu [anonsu](https://go.microsoft.com/fwlink/?linkid=821148) szczegółowe informacje.
> 
> 

Jeśli nie masz hello czas lub możliwości hello toorun [testy przepustowości sieci](remoteapp-bandwidthtests.md) usługi Azure RemoteApp, poniżej przedstawiono kilka wskazówek dość ogólny, które mogą ułatwić oszacowanie przepustowość sieci dla poszczególnych użytkowników.

Jeśli masz kombinację tych scenariuszy, nie zaleca się niczego najwyżej (do) 10 MB/s jako hello minimalnej przepustowości dla nowoczesnych aplikacji podłączonej do Internetu w środowisku zdalnym. (Mimo że zgodnie z opisem, nie gwarantuje to lepiej niż średni użytkowników.)

## <a name="complex-powerpoint-simple-powerpoint"></a>PowerPoint złożonych, prosty programu PowerPoint
Usługa Azure RemoteApp jest najlepiej w sieci LAN 100 MB. W hello 10 MB/s profilu sieci, gdy zakłócenia powyżej 120 ms jest większa niż % 5, hello użytkownika zostanie wyświetlony średni środowisko. Na 1 MB/s hello różnych jest glaring — na przykład w ramach pokazu slajdów, hello użytkownika może nie być wyświetlana animowane przejścia na wszystkich ponieważ ramki są pomijane.

## <a name="internet-explorer-mixed-pdf-pdf-text"></a>Mieszany programu Internet Explorer, PDF, PDF, tekst
Profil sieci usługi 10 MB/s jest Zamknij tooLAN w większości aspektów. 1 MB/s zapewni OK środowisko, mimo że może być niektórych zakłócenia, gdy użytkownik przewinie, gdy istnieją obrazy na ekranie powitania.

## <a name="flash-video-youtube"></a>Flash wideo (YouTube)
100 MB/s LAN zapewnia hello najlepsze doświadczenia, gdy 10 MB/s jest dopuszczalne (znaczenie firma Microsoft nadąża z szybkość klatek hello, ale zwiększa zakłóceń). 1 MB/s zakłócenia jest bardzo wysoka i zauważalne.

## <a name="word-typing-word-remote-input"></a>Wpisz (Word zdalnego danych wejściowych) w programie Word
Jest to scenariusz użycia niskiej przepustowości. 256 KB/s udostępniamy tak dobrze doświadczenia jako sieci LAN.

## <a name="learn-more"></a>Dowiedz się więcej
* [Szacowanie użycia przepustowości sieci usługi Azure RemoteApp](remoteapp-bandwidth.md)
* [Usługa Azure RemoteApp — jak przepustowości sieci i jakości środowisko pracy ze sobą?](remoteapp-bandwidthexperience.md)
* [Usługa Azure RemoteApp — tseting użycie przepustowości sieci z niektórych typowych scenariuszy](remoteapp-bandwidthtests.md)

