---
title: "Cennik usługi Azure IoT Hub aaaUnderstand | Dokumentacja firmy Microsoft"
description: "Przewodnik dewelopera po — informacje o jak pomiaru i cenach współpracuje z tym Centrum IoT poszło przykłady."
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 1ac90923-1edf-4134-bbd4-77fee9b68d24
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/12/2016
ms.author: elioda
ms.openlocfilehash: e294c0b7f483e042ca3f63e93c14e0c2d773ae7f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-iot-hub-pricing-information"></a>Informacje o cenach Centrum IoT Azure

[Centrum IoT Azure cennik] [ lnk-pricing] hello ogólne informacje na różne jednostki SKU i cenach dla Centrum IoT. Ten artykuł zawiera więcej informacji na temat sposobu różne funkcje Centrum IoT są mierzone jako powitalne wiadomości przez Centrum IoT.

## <a name="charges-per-operation"></a>Opłaty na operację

| Operacja | Informacje o rozliczeniach | 
| --------- | ------------------- |
| Operacje rejestru tożsamości <br/> (Tworzenie, pobieranie, listy, aktualizowanie i usuwanie) | Nie zostanie obciążona. |
| Komunikaty z urządzenia do chmury | Pomyślnie wysłane wiadomości są naliczane w fragmentów 4 KB na ruch przychodzący do Centrum IoT, na przykład się, że komunikat 6KB rozliczany 2 wiadomości. |
| Komunikaty chmury do urządzenia | Pomyślnie wysłane wiadomości są pobierane w fragmentów 4 KB, na przykład wiadomości 6 KB rozliczany 2 wiadomości. |
| Przekazywania plików | TooAzure transfer plików magazynu nie są naliczane przez Centrum IoT. Komunikaty rozpoczęcia i zakończenia transferu plików są naliczane, ponieważ messaged mierzonego w przyrostach 4 KB. Na przykład przesyłania pliku 10 MB jest pobierana dwa komunikaty w toohello dodanie usługi Azure Storage kosztów. |
| Metody bezpośrednie | Metoda pomyślnego żądania są naliczane w fragmentów 4 KB, odpowiedzi z treściami niepustym są naliczane 4 KB jako dodatkowe komunikaty. Żądania toodisconnected urządzeń są naliczane jako komunikaty w fragmentów 4 KB. Na przykład metodę o treści 6 KB, który daje w odpowiedzi nie jednostki z urządzenia hello jest rozliczany jako dwa komunikaty; metody z treścią 6 KB powstały w odpowiedzi 1 KB z urządzenia hello jest rozliczany jako dwa komunikaty żądania hello plus kolejną wiadomość hello odpowiedź. |
| Liczba odczytów bliźniaczej reprezentacji urządzenia | Dwie urządzenia odczytuje z hello urządzenia i z powrotem rozwiązania hello zakończenia są naliczane jako komunikaty w fragmentów 512-bajtowego. Na przykład odczytywania dwie 6 KB urządzenia jest rozliczany jako 12 wiadomości. |
| Aktualizacje dwie urządzeń (znaczniki i właściwości) | Aktualizacje dwie urządzenia z hello urządzenie i hello są naliczane jako komunikaty w fragmentów 512-bajtowego. Na przykład odczytywania dwie 6 KB urządzenia jest rozliczany jako 12 wiadomości. |
| Urządzenie dwie zapytań | Zapytania są naliczane jako komunikaty, w zależności od wielkości wynik hello w fragmentów 512-bajtowego. |
| Operacje zadań <br/> (tworzenie, aktualizowanie, wyświetlanie, usuwanie) | Nie zostanie obciążona. |
| Operacje na urządzenie zadania | Operacje zadania (na przykład aktualizacji dwie urządzenia i metody) są naliczane normalnego. Na przykład zadanie wynikiem wywołania metody 1000 1 KB żądań i odpowiedzi pusty treści jest pobierana 1000 komunikatów. |

> [!NOTE]
> Wszystkich rozmiarów są obliczane, biorąc pod uwagę rozmiar ładunku hello w bajtach (protokół ramek zostanie zignorowana). W przypadku wiadomości (które mają właściwości, oraz i treść) rozmiar hello jest obliczana w sposób niezależny od protokołu, zgodnie z opisem w hello [Centrum IoT wiadomości przewodnik dewelopera][lnk-message-size].

## <a name="example-1"></a>Przykład #1

Urządzenie wysyła jeden komunikat urządzenia do chmury 1 KB na minutę tooIoT koncentratora, który jest odczytywany przez usługi Azure Stream Analytics. zaplecza rozwiązania Hello wywołuje metodę (z 512-bajtowych ładunku) na urządzeniu hello tootrigger co 10 minut określonej akcji. urządzenie Hello odpowiada metoda toohello z wynikiem 200 bajtów.

urządzenie Hello zużywa komunikat 1 * 1440 wiadomości na dzień dla wiadomości powitania od urządzenia do chmury i 2 żądania i odpowiedzi = 60 minut * 24 godzin * 6 razy na godzinę * 24 godziny = 288 komunikatów dla metod hello, łącznie z 1728 wiadomości na dzień.

## <a name="example-2"></a>Przykład #2

Urządzenie wysyła jeden komunikat urządzenia do chmury 100 KB co godzinę. Aktualizuje również dwie jego urządzenia z 1 KB ładunków co 4 godziny. rozwiązania Hello kończyć raz dziennie, dwie urządzenia 14 KB hello odczyty i aktualizuje go z konfiguracjami toochange ładunków 512-bajtowego.

urządzenie Hello zużywa 25 wiadomości (100KB / 4KB) * 24 godziny dla wiadomości urządzenia do chmury, a także komunikat 1 * 6 razy dziennie aktualizacje dwie urządzenia, dla wszystkich 156 wiadomości na dzień.
Witaj zaplecza rozwiązania wykorzystuje dwie urządzenia hello tooread 28 wiadomości (14KB/0,5 KB), a także tooupdate 1 wiadomość go dla wszystkich wiadomości 29.

Całkowita liczba urządzenia hello zaplecza rozwiązania hello zajmować 185 wiadomości na dzień.


[lnk-pricing]: https://azure.microsoft.com/pricing/details/iot-hub
[lnk-message-size]: iot-hub-devguide-messages-construct.md
