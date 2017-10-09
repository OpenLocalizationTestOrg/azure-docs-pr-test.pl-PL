---
title: "aaaInternet rzeczy najlepsze rozwiązania w zakresie zabezpieczeń | Dokumentacja firmy Microsoft"
description: "Witaj artykuł zawiera listę nadzorowaną dotyczącą programu Microsoft Internet rzeczy najlepsze rozwiązania i ogólne zalecenia."
services: security
documentationcenter: na
author: TomShinder
manager: StevenPo
editor: TomSh
ms.assetid: 2d5598c5-4c30-481d-b8f4-51ee024ea9a7
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/04/2017
ms.author: yurid
ms.openlocfilehash: 7ee31c912e8ac230ffa5efcd5b4c2b0b0713584f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="internet-of-things-security-best-practices"></a>Internet rzeczy najlepsze rozwiązania w zakresie zabezpieczeń
Zabezpieczanie infrastruktury Internetu rzeczy (IoT) hello jest krytyczne przedsiębiorstwa dla każdego związanego z rozwiązania IoT. Ze względu na powitania liczbę urządzeń i hello toocompromise miliony urządzenia IoT jest nieuproszczony i może mieć wpływ powszechnie związanych z Rozproszony charakter tych urządzeń, hello wpływ zdarzeń zabezpieczeń.

Z tego powodu podejście zabezpieczeń zabezpieczeń w zakresie zabezpieczeń IoT. Przenosi danych potrzeb toobe bezpiecznego w chmurze hello i jak w sieciach prywatnych i publicznych. Metody muszą toobe w miejscu toosecurely udostępniania hello urządzenia IoT samodzielnie. Każda warstwa z urządzenia, toonetwork, toocloud zaplecza musi silne zabezpieczenie gwarancji.

Najlepsze rozwiązania IoT mogą być podzielone na hello w następujący sposób:

* IoT producenta sprzętu lub integrator
* Deweloper rozwiązania IoT
* Narzędzie wdrażania rozwiązania IoT
* Operator rozwiązania IoT

Ten artykuł zawiera podsumowanie [Internet z innymi najlepszych rozwiązań dotyczących zabezpieczeń](../iot-suite/iot-security-best-practices.md). Bardziej szczegółowe informacje można znaleźć w artykule toothat.

## <a name="iot-hardware-manufacturer-or-integrator"></a>IoT producenta sprzętu lub integrator
Wykonaj hello najlepsze rozwiązania w zakresie poniżej IoT produkcji sprzętu lub integrator sprzętu:

* **Zakres wymagania sprzętowe toominimum**: projekt sprzętu hello powinna zawierać minimalne funkcje wymagane dla operacji hello sprzętu i nic więcej. 
* **Należy sprzętu manipulację dowód**: kompilacji w mechanizmów toodetect fizycznego manipulowania sprzętu, takich jak otwieranie hello urządzenia pokrycia, usunięcie części urządzenia hello itp. 
* **Tworzenie wokół bezpiecznych składników sprzętowych**: Jeśli [kst](https://en.wikipedia.org/wiki/Cost_of_goods_sold) zezwolić, tworzenia funkcji zabezpieczeń, takich jak bezpieczna i szyfrowana magazynowania i funkcji rozruchowego opartego na modułu TPM.
* **Zabezpieczyć uaktualnień**: uaktualnienie oprogramowania układowego okres istnienia hello urządzenia są nieuniknione.

## <a name="iot-solution-developer"></a>Deweloper rozwiązania IoT
Jeśli jesteś deweloperem rozwiązania IoT, wykonaj hello najlepsze rozwiązania w zakresie poniżej:

* **Postępuj zgodnie z metodologii rozwoju oprogramowania bezpiecznego**: tworzenie bezpiecznej oprogramowania wymaga podstaw pomyśleć o zabezpieczeń z hello incepcja projektu hello wszystkich hello sposób tooits implementacji, testowania i wdrażania.
* **Wybierz oprogramowanie typu open source z rozwagą**: oprogramowanie typu open source zapewnia tooquickly opracowywania rozwiązań.
* **Integracja z rozwagą**: istnieje wiele luk w zabezpieczeniach oprogramowania hello w granic hello bibliotek i interfejsów API. 

## <a name="iot-solution-deployer"></a>Narzędzie wdrażania rozwiązania IoT
W przypadku wdrażania rozwiązania IoT, wykonaj hello najlepsze rozwiązania w zakresie poniżej:

* **Wdrażanie sprzętu bezpiecznie**: IoT wdrożenia może wymagać toobe sprzęt wdrożony w lokalizacjach niezabezpieczone, taki jak publiczny spacji lub ustawień nienadzorowanych.
* **Bezpieczeństwa kluczy uwierzytelniania**: podczas wdrażania, każde urządzenie wymaga identyfikatory urządzeń i skojarzonych kluczy uwierzytelniania generowane przez usługę w chmurze hello. Zachowaj te klucze fizycznie bezpieczne nawet po wdrożeniu hello. Dowolny klawisz, którego bezpieczeństwo zostało naruszone mogą posłużyć toomasquerade złośliwe urządzenia jako istniejące urządzenie.

## <a name="iot-solution-operator"></a>Operator rozwiązania IoT
Jeśli jesteś operator rozwiązania IoT, wykonaj hello najlepsze rozwiązania w zakresie poniżej:

* **Zachowaj systemu toodate**: Upewnij się, systemów operacyjnych urządzeń i wszystkie sterowniki urządzeń są zaktualizowane toohello najnowszych wersji. 
* **Ochrona przed złośliwych działań**: pozwala na powitania systemu operacyjnego, umieść hello najnowszych funkcji oprogramowania antywirusowego i przed złośliwym oprogramowaniem w każdym systemie operacyjnym urządzenia. 
* **Inspekcji, często**: inspekcja IoT infrastruktury zabezpieczeń związanych z problemów jest kluczem wysyłanej toosecurity zdarzenia.
* **Fizycznie ochrona powitalnych IoT infrastruktury**: hello najgorszy zabezpieczeń ataków na infrastrukturę IoT jest uruchomiony przy użyciu toodevices fizyczny dostęp.
* **Ochrona poświadczeń w chmurze**: chmury uwierzytelniania poświadczenia używane do konfigurowania i obsługi wdrażania IoT są prawdopodobnie hello Najprostszym sposobem toogain dostępu i złamanie IoT. 

