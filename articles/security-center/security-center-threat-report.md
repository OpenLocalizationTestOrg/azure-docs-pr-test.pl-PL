---
title: "aaaAzure raportu analizy zagrożeń Centrum zabezpieczeń | Dokumentacja firmy Microsoft"
description: "Ten dokument ułatwia toouse Azure Security Center zagrożeń inteligentnego raportów podczas badania toofind więcej informacji na temat alertu zabezpieczeń."
services: security-center
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: 
ms.assetid: 5662e312-e8c2-4736-974e-576eeb333484
ms.service: security-center
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: yurid
ms.openlocfilehash: c888cfac1dd8b057616a6b8e6c6f6b67b552f2e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-security-center-threat-intelligence-report"></a>Raport analizy zagrożeń usługi Azure Security Center
W tym dokumencie wyjaśniono, w jaki sposób raporty analizy zagrożeń usługi Azure Security Center mogą ułatwić uzyskanie większej ilości informacji na temat zagrożenia, które spowodowało wygenerowanie alertu zabezpieczeń.

## <a name="what-is-a-threat-intelligence-report"></a>Czym jest raport analizy zagrożeń?
Wykrywanie zagrożeń Centrum zabezpieczeń polega na monitorowanie informacji o zabezpieczeniach z zasobów platformy Azure, hello sieci i rozwiązań partnerskich połączonych. Te informacje, często korelowanie informacji z wielu źródeł, zagrożenia tooidentify analizę. Ten proces jest częścią hello Centrum zabezpieczeń [możliwości wykrywania](security-center-detection-capabilities.md).

Gdy usługa Security Center zidentyfikuje zagrożenie, wywoła [alert zabezpieczeń](security-center-managing-and-responding-alerts.md), który zawiera szczegółowe informacje dotyczące określonego zdarzenia — w tym propozycje rozwiązania problemu. zespoły odpowiedzi na zdarzenia tooassist zbadać i eliminowanie zagrożeń, Centrum zabezpieczeń zawiera raport analizy zagrożeń, który zawiera informacje dotyczące zagrożenia hello, który został wykryty, takich jak wraz z informacjami:

* tożsamość lub powiązania osoby atakującej (jeśli takie informacje są dostępne);
* cele osoby atakującej;
* bieżące i wcześniejsze kampanie ataków (jeśli takie informacje są dostępne);
* taktyka, narzędzia i procedury osoby atakującej;
* skojarzone wskaźniki naruszenia (IoC), np. adresy URL i skróty plików;
* Victimology, hello branżowych i tooassist geograficzne występowania w określenie, czy zasobów platformy Azure, są narażeni na ataki
* informacje dotyczące ograniczania i usuwania zagrożeń.

> [!NOTE]
> Witaj ilość informacji w żadnych raportów określonego różnią się; poziom szczegółowości Hello opiera się na działania i występowanie hello złośliwego oprogramowania.
>
>

Centrum zabezpieczeń ma trzy typy zagrożeń raporty, które mogą się różnić zgodnie z toohello ataku. dostępne raporty Hello są:

* **Raport grupy działań**: zawiera dokładne informacje dotyczące atakujących osób, ich celów oraz taktyki.
* **Raport kampanii**: koncentruje się na szczegółach określonych kampanii ataków.
* **Raport z podsumowaniem zagrożenia**: obejmuje wszystkie elementy hello hello poprzednich dwóch raportów.

Informacje tego typu jest bardzo przydatny podczas hello [odpowiedzi na zdarzenia](security-center-incident-response.md) proces, w przypadku, gdy jest źródłem trwających badań toounderstand hello atak powitania, atakujący hello motywacji i co toodo toomitigate to problem przenoszenie do przodu.

## <a name="how-tooaccess-hello-threat-intelligence-report"></a>Jak tooaccess hello raportu analizy zagrożeń?
Bieżące alerty można przeglądać, analizując hello **alerty zabezpieczeń** kafelka. Otwórz hello portalu Azure i wykonaj kroki hello poniżej toosee więcej szczegółów dotyczących poszczególnych alertów:

1. Na pulpicie nawigacyjnym Centrum zabezpieczeń hello, zobaczysz hello **alerty zabezpieczeń** kafelka.
2. Kliknij hello kafelka tooopen hello **alerty zabezpieczeń** bloku, który zawiera szczegółowe informacje o hello alerty, a następnie kliknij przycisk w hello alert zabezpieczeń, które mają tooobtain więcej informacji na temat.

    ![Alerty zabezpieczeń](./media/security-center-threat-report/security-center-threat-report-fig1.png)
3. W takim przypadku hello **podejrzane proces wykonywany** bloku pokazuje hello szczegóły alertu hello, jak pokazano na poniższej ilustracji hello:

    ![Szczegóły alertu zabezpieczeń](./media/security-center-threat-report/security-center-threat-report-fig2.png)
4. Witaj ilość informacji dla każdego alertu zabezpieczeń różnią się zgodnie z toohello typu alertu. W hello **raporty** pola raportu analizy łącza toohello zagrożeń. Po jego kliknięciu zostanie wyświetlone kolejne okno przeglądarki z plikiem PDF.

   ![Wybór magazynu](./media/security-center-threat-report/security-center-threat-report-fig3.png)

W tym miejscu można pobrać powitalne PDF dla tego raportu i odczytu więcej informacji na temat zabezpieczeń hello wydawać, która została wykryta i podejmuj działania na podstawie informacji hello.

## <a name="see-also"></a>Zobacz też
W tym dokumencie opisano, jak przydatne mogą być raporty analizy zagrożeń usługi Azure Security Center w trakcie sprawdzania alertów zabezpieczeń. toolearn więcej informacji na temat Centrum zabezpieczeń Azure, zobacz następujące hello:

* [Azure Security Center — często zadawane pytania](security-center-faq.md). Znajdź często zadawane pytania dotyczące korzystania z usługi hello.
* [Korzystanie z usługi Azure Security Center w celu reagowania na zdarzenia](security-center-incident-response.md)
* [Funkcje wykrywania usługi Azure Security Center](security-center-detection-capabilities.md)
* [Przewodnik planowania i obsługi usługi Azure Security Center](security-center-planning-and-operations-guide.md). Dowiedz się, jak tooplan i zrozumieć zagadnienia dotyczące projektowania hello tooadopt Centrum zabezpieczeń Azure.
* [Zarządzanie i odpowiada toosecurity alertów w Centrum zabezpieczeń Azure](security-center-managing-and-responding-alerts.md). Dowiedz się, jak alerty toosecurity toomanage i odpowiada.
* [Obsługa zdarzeń naruszenia zabezpieczeń w usłudze Azure Security Center](security-center-incident.md)
* [Blog Azure Security](http://blogs.msdn.com/b/azuresecurity/). Wpisy na blogu dotyczące zabezpieczeń i zgodności platformy Azure.
