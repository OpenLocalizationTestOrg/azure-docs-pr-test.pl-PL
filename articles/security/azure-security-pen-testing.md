---
title: aaaPen testowanie | Dokumentacja firmy Microsoft
description: "Hello artykuł zawiera omówienie penetracji hello testowanie procesu (pentest) oraz jak wykonywać pentest względem aplikacji uruchomionych w infrastrukturze Azure."
services: security
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: TomSh
ms.assetid: 695d918c-a9ac-4eba-8692-af4526734ccc
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: yurid
ms.openlocfilehash: 202c239f46d8693ab7aa85e237235372e743e108
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="pen-testing"></a>Testowanie pióra
Jedną z najważniejszych hello o do testowania aplikacji i wdrażania przy użyciu programu Microsoft Azure jest to, że nie ma potrzeby tooput razem toodevelop infrastruktury lokalnej, testowania i wdrażania aplikacji. Wszystkie infrastruktury hello jest poświęcony na obsługę przez usług platformy Microsoft Azure hello. Nie masz tooworry o tworzenia zapotrzebowania, pobieranie, a "rozlania i układania" sprzętu lokalnymi.

Jest to doskonały — jednak nadal toomake się, że należy wykonać normalnego zabezpieczeń z powodu starannością. Jeden z elementów hello potrzebnych toodo jest aplikacji hello testowych penetracji wdrażanie na platformie Azure.

Może już wiedzieć, że Microsoft wykonuje [penetracji testowania naszym środowisku Azure](https://gallery.technet.microsoft.com/Cloud-Red-Teaming-b837392e). To pomoże nam w ulepszeniu platformy i przeprowadza działania pod względem poprawy zabezpieczeń, wprowadzenie nowych kontrolach zabezpieczeń i poprawy naszych procesów zabezpieczeń.

Nie możemy pióra przetestować aplikację dla Ciebie, ale Rozumiemy będzie mają i wymagają tooperform pióra testowania na własnych aplikacji. Że jest to przydatne, ponieważ podczas można zwiększyć bezpieczeństwo hello aplikacji, należy zabezpieczyć cały ekosystem Azure hello.

Gdy pióro należy przetestować aplikacje, może wyglądać toous atak. Firma Microsoft [na stałe monitorowanie](http://blogs.msdn.com/b/azuresecurity/archive/2015/07/05/best-practices-to-protect-your-azure-deployment-against-cloud-drive-by-attacks.aspx) dla wzorców ataków i zainicjuje proces odpowiedzi na zdarzenia, jeśli chcemy. Go nie będą pomocne, a nie pomoże nam, jeśli wyzwalana odpowiedzi na zdarzenia z powodu tooyour własnych powodu testowania pióra starannością.

Jakie toodo?

Jeśli wszystko jest gotowe toopen przetestuj hostowanymi na platformie Azure aplikacje, istnieje możliwość zbyt[Daj nam znać](https://portal.msrc.microsoft.com/en-us/engage/pentest). Po wiemy, że będzie toobe wykonywania określonych testów, firma Microsoft nie będą przypadkowo zamknięty (na przykład blokowanie hello adres IP, który w przypadku testowania z), ile testów jest zgodna z toohello Azure pióra testowania warunki i postanowienia, które opisano w [Firmy Microsoft w chmurze Unified penetracji testowania zasad zaangażowania](https://technet.microsoft.com/en-us/mt784683).
Standardowych testów, które można wykonać obejmują:

* Testy na powitania toouncover Twojego punkty końcowe [Otwórz sieci Web aplikacji zabezpieczeń projektu (OWASP) pierwszych 10 luk w zabezpieczeniach](https://www.owasp.org/index.php/Category:OWASP_Top_Ten_Project)
* [Testowanie argumentu rozmycie](https://blogs.microsoft.com/cybertrust/2007/09/20/fuzz-testing-at-microsoft-and-the-triage-process/) z punktami końcowymi
* [Skanowanie portów](https://en.wikipedia.org/wiki/Port_scanner) z punktami końcowymi

Jeden typ testu, który nie może wykonać jest dowolnego rodzaju [przeprowadzenie ataku typu "odmowa usługi" (DoS)](https://en.wikipedia.org/wiki/Denial-of-service_attack) ataku. Dotyczy to również inicjowanie sam atak DoS lub przy użyciu powiązanych testy, które może ustalić, pokazują lub symulować dowolnego typu atak DoS.

Czy gotowe tooget uruchomiona za pomocą pióra testowanie aplikacji hostowanej na platformie Microsoft Azure? Jeśli tak, a następnie head na za pośrednictwem toohello [omówienie testów penetracji](https://technet.microsoft.com/library/mt784683.aspx) (i kliknij przycisk hello testowania żądania przycisk u dołu strony hello hello Utwórz. Będzie także znaleźć więcej informacji na temat pióra hello testowania warunki i przydatne łącza w sposób może raportować tooAzure powiązane wady zabezpieczeń lub innych usług firmy Microsoft.
