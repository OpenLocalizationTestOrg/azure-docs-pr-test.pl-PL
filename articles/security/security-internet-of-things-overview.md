---
title: aaaSecure z Internetu rzeczy (IoT) na platformie Azure | Dokumentacja firmy Microsoft
description: " Azure Internetu rzeczy (IoT) usług oferuje szeroką gamę możliwości. Ten artykuł pomaga w zrozumieniu sposobu toosecure Twojego rozwiązania IoT na platformie Azure. "
services: security
documentationcenter: na
author: TomShinder
manager: MBaldwin
editor: TomSh
ms.assetid: 1473c8dd-8669-48fb-86db-b3c50e2eaf59
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/23/2017
ms.author: terrylan
ms.openlocfilehash: b6cb2ea1c1facada854fb52c55066f34a8289e47
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="internet-of-things-security-overview"></a>Przegląd zabezpieczeń Internetu rzeczy
Azure Internetu rzeczy (IoT) usług oferuje szeroką gamę możliwości. Są to usługi klasy korporacyjnej, które pozwalają wykonywać następujące operacje:

* Zbieranie danych z urządzeń
* Analizowanie strumieni danych w ruchu
* Przechowywanie dużych zestawów danych i tworzenie dotyczących ich zapytań
* Wizualizowanie danych w czasie rzeczywistym i danych historycznych
* Integrowanie z systemami zaplecza biura

toodeliver te możliwości pakiet IoT Azure pakiety ze sobą Azure wielu usług z rozszerzeniami niestandardowymi jako wstępnie skonfigurowanych rozwiązań. Te wstępnie skonfigurowanych rozwiązań jest podstawowych implementacji typowe wzorce rozwiązania IoT pomagających w czasie hello tooreduce zająć toodeliver Twojego rozwiązania IoT. Przy użyciu hello IoT software development kit, można dostosowywanie i rozszerzanie toomeet tych rozwiązań do własnych wymagań. Można ich także użyć jako przykładów lub szablonów podczas tworzenia nowych rozwiązań IoT.

Pakiet Azure IoT Hello jest niezwykle wydajnym rozwiązaniem dla potrzeb IoT. Warto jednak znaczenie upmost czy Twojego rozwiązania IoT zostały zaprojektowane z myślą od początku hello o bezpieczeństwie. Z powodu wielość hello urządzeń IoT wszystkie zdarzenia zabezpieczeń może szybko stać się powszechnie zdarzeń z znaczący wpływ.

toohelp rozumiesz sposób toosecure Twojego rozwiązania IoT mamy hello następujących informacji.

## <a name="security-architecture"></a>Architektura zabezpieczeń
Podczas projektowania systemu, jest ważne toounderstand hello potencjalne zagrożenia toothat systemu i dodaj odpowiednie zabezpieczenia w związku z tym, jak hello system został zaprojektowany i zaprojektowana. Koniecznie toodesign ponieważ zrozumienie, jak osoba atakująca może być możliwe toocompromise systemu pomaga, upewnij się, że odpowiednie środki zaradcze są stosowane od początku hello hello produktu od początku hello z myślą o bezpieczeństwie.

Informacje na temat architektury IoT zabezpieczeń, odczytując [Internet rzeczy Architektura zabezpieczeń](../iot-suite/iot-security-architecture.md).

W tym artykule omówiono hello następujące tematy:

* [Rozpoczyna się modelu zagrożeń zabezpieczeń](../iot-suite/iot-security-architecture.md#security-starts-with-a-threat-model)
* [Zabezpieczenia w IoT](../iot-suite/iot-security-architecture.md#security-in-iot)
* [Witaj modelowania zagrożeń architektura referencyjna IoT Azure](../iot-suite/iot-security-architecture.md#threat-modeling-the-azure-iot-reference-architecture)

## <a name="security-from-hello-ground-up"></a>Zabezpieczeń z hello tła w
Witaj IoT stanowi unikatowy zabezpieczeń, prywatności i zgodności wyzwania toobusinesses na całym świecie. W przeciwieństwie do tradycyjnych przez technologii gdzie te problemy koncentrują się wokół oprogramowania i jak jest implementowane IoT dotyczy, co się stanie po hello ataków i hello względem fizycznego łączenia. Ochrona rozwiązania IoT wymaga zapewnienia bezpiecznego inicjowania obsługi urządzeń i bezpieczna łączność między tymi urządzeniami i chmury hello i ochronę danych w chmurze hello podczas przetwarzania i przechowywania. Praca z takich funkcji, są jednak ograniczone zasobów urządzeń, rozmieszczenie geograficzne wdrożeń i wiele urządzeń w ramach rozwiązania.

Dowiedz się jak toohandle zabezpieczeń w następujących obszarach odczytując [zabezpieczeń Internetu rzeczy z hello tła](../iot-suite/securing-iot-ground-up.md).

Witaj omówiono hello następujące tematy:

* [Zabezpieczanie infrastruktury z hello tła w](../iot-suite/securing-iot-ground-up.md#secure-infrastructure-from-the-ground-up)
* [Microsoft Azure — bezpiecznej infrastruktury IoT dla biznesu](../iot-suite/securing-iot-ground-up.md#microsoft-azure---secure-iot-infrastructure-for-your-business)

## <a name="best-practices"></a>Najlepsze rozwiązania
Zabezpieczanie infrastruktury IoT wymaga rygorystyczne strategii zabezpieczeń zabezpieczeń. Z Zabezpieczanie danych w chmurze hello ochronę integralności danych podczas przesyłania w hello publicznej sieci internet, inicjowania obsługi administracyjnej urządzeń toosecurely, każda warstwa kompilacje gwarancję zabezpieczeń hello całej infrastruktury.

Informacje na temat zabezpieczeń Internetu rzeczy najlepsze rozwiązania w zakresie odczytując [najlepszych rozwiązań dotyczących zabezpieczeń Internetu rzeczy](../iot-suite/iot-security-best-practices.md).

Witaj omówiono hello następujące tematy:

* [Producenta sprzętu IoT/integrator](../iot-suite/iot-security-best-practices.md#iot-hardware-manufacturerintegrator)
* [Deweloper rozwiązania IoT](../iot-suite/iot-security-best-practices.md#iot-solution-developer)
* [Narzędzie wdrażania rozwiązania IoT](../iot-suite/iot-security-best-practices.md#iot-solution-deployer)
* [Operator rozwiązania IoT](../iot-suite/iot-security-best-practices.md#iot-solution-operator)
