---
title: "Badanie zdarzeń i alertów w usłudze Azure Security Center | Microsoft Docs"
description: "Ten dokument ułatwia korzystanie z funkcji badania zdarzeń zabezpieczeń i alertów w usłudze Azure Security Center."
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: a8e894a9-8781-4749-ae8f-8c8e01658566
ms.service: security-center
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 09/18/2017
ms.author: yurid
ms.openlocfilehash: 818c257d1959936f0dc326486e372677aacb065a
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/11/2017
---
# <a name="investigate-incidents-and-alerts-in-azure-security-center-preview"></a>Badanie zdarzeń i alertów w usłudze Azure Security Center (wersja zapoznawcza)
Ten dokument ułatwia korzystanie z funkcji badania zdarzeń zabezpieczeń i alertów w usłudze Azure Security Center.

## <a name="what-is-investigation-in-security-center"></a>Czym jest badanie w usłudze Security Center?
Funkcja Badanie w usłudze Security Center umożliwia klasyfikowanie, określanie zakresu i śledzenie głównej przyczyny potencjalnego [zdarzenia zabezpieczeń](https://docs.microsoft.com/azure/security-center/security-center-incident).
 
Celem jest ułatwienie procesu badania dzięki połączeniu wszystkich jednostek ([alertów zabezpieczeń](https://docs.microsoft.com/azure/security-center/security-center-alerts-type), użytkowników, komputerów i zdarzeń) biorących udział w badanym zdarzeniu.  Usługa Security Center umożliwia skorelowanie odpowiednich danych ze wszystkimi zaangażowanymi jednostkami oraz udostępnienie tej korelacji za pomocą dynamicznego wykresu, który ułatwia nawigowanie po obiektach i wizualizowanie istotnych informacji.


## <a name="how-investigation-works"></a>Jak działa funkcja Badanie?
Funkcja Badanie składa się z wykresu, który zajmuje centralny obszar pulpitu nawigacyjnego badania. Wykres zawsze koncentruje się na określonej jednostce i przedstawia związane z nią jednostki. Jednostką może być alert zabezpieczeń, użytkownik, komputer lub zdarzenie.
 
![Mapa](./media/security-center-investigation/security-center-investigation-fig1.png)

Użytkownik może przechodzić z jednej jednostki do innej, klikając ją na wykresie. Wykres automatycznie koncentruje się na wybranej jednostce i związanych z nią jednostkach. Jednostki, które nie są już istotne, mogą zostać usunięte z wykresu.

### <a name="investigation-path"></a>Ścieżka badania
Gdy użytkownik przechodzi do innych jednostek, ścieżka badania ułatwia śledzenie kontekstu badania i umożliwia szybką nawigację. Zdarzenie zawierające wyniki badania jest zawsze lewym skrajnym zdarzeniem na ścieżce badania.

![Ścieżka](./media/security-center-investigation/security-center-investigation-fig2.png)

### <a name="general-information"></a>Informacje ogólne
Gdy jednostka jest wyświetlana na wykresie, na kartach znajdują się dodatkowe informacje na jej temat. Karta **Informacje** zawiera ogólne informacje na temat danej jednostki pochodzące z różnych dostępnych źródeł informacji. 

![Informacje ogólne](./media/security-center-investigation/security-center-investigation-fig3.png)

Karta Informacje przedstawia informacje dotyczące zdarzenia wybranego na mapie. Zdarzenie to kontener zawierający wyniki badania. Każde badanie odbywa się w kontekście zdarzenia.

Zdarzenie jest tworzone tylko wtedy, gdy użytkownik kliknie przycisk **Rozpocznij badanie** dla określonego alertu. Podstawową funkcją dostępną dla analityka jest oznaczanie jednostek, takich jak użytkownik, komputer lub alert. Po oznaczeniu jednostki jako powiązanej jest podawana przyczyna. Od tego momentu jednostka jest wyświetlana na wykresie i na liście jednostek zdarzenia bezpośrednio pod zdarzeniem.

### <a name="entities"></a>Jednostki

Na karcie **Jednostki** są wyświetlane wszystkie powiązane jednostki pogrupowane według typu. Jest to przydatne w dwóch przypadkach: gdy istnieje zbyt wiele jednostek do przedstawienia na wykresie i gdy nazwy jednostek są zbyt długie, przez co ich ocena jest łatwiejsza w formie tabelarycznej.

![Jednostki](./media/security-center-investigation/security-center-investigation-fig4.png)

### <a name="search"></a>Wyszukiwanie

Karta **Wyszukiwanie** przedstawia wszystkie typy dzienników dostępne dla danej jednostki. W przypadku każdego typu dziennika można wyświetlić liczbę dostępnych rekordów. Kliknięcie każdego typu dziennika powoduje przejście do ekranu wyszukiwania. Na ekranie wyszukiwania można uściślić wyszukiwanie i skorzystać z różnych funkcji wyszukiwania, takich jak alerty ustawień. W bieżącej wersji karta Wyszukiwanie jest dostępna tylko w przypadku jednostek użytkownicy i komputery.

![Wyszukiwanie](./media/security-center-investigation/security-center-investigation-fig5.png)

### <a name="exploration"></a>Eksploracja

Karta **Eksploracja** umożliwia analitykowi ocenę danych dotyczących różnych problemów, które są związane z jednostką. Na przykład w przypadku badania komputera na karcie Eksploracja jest wyświetlana lista wykonanych na nim procesów. W niektórych przypadkach na karcie Eksploracja są wyświetlane dane, które mogą wskazywać na podejrzany problem. Analityk może ocenić dane na karcie lub otworzyć je na ekranie wyszukiwania, aby przejrzeć duże zestawy danych i skorzystać z opcji wyszukiwania zaawansowanego, takich jak filtrowanie i eksportowanie do programu Excel.

![Eksploracja](./media/security-center-investigation/security-center-investigation-fig6.png)

### <a name="timeline"></a>Oś czasu

Większość danych prezentowanych na wykresie i na różnych kartach dotyczy określonego przedziału czasu. Ten zakres czasu ustawia się za pomocą selektora zakresu czasu w lewym górnym rogu wykresu. Analityk może wybrać zakres czasu różnymi metodami. 

![Oś czasu](./media/security-center-investigation/security-center-investigation-fig7.png)

Następujące elementy są wrażliwe na zakres czasu:

- Relacja użytkownik-komputer na wykresie: prezentowani są tylko użytkownicy, którzy zalogowali się na komputerze w danym zakresie czasu.
- Alerty prezentowane podczas badania komputerów i użytkowników: prezentowane są tylko alerty, które wystąpiły w danym zakresie czasu.
- Logika na karcie Jednostki jest taka sama jak na wykresie.

Następujące elementy będą prezentowane niezależnie od wybranego zakresu czasu:

- Podczas wyświetlania alertu zawsze prezentowane są wszystkie zawarte w nim jednostki, takie jak użytkownicy i komputery.
- Jeśli zdarzenie zawiera jednostkę, będzie ona prezentowana.

> [!NOTE]
> Na kartach **Wyszukiwanie** i **Eksploracja** są wyświetlane tylko rekordy mieszczące się w tym zakresie czasu.

## <a name="how-to-perform-an-investigation"></a>Jak przeprowadzić badanie?

Badanie można rozpocząć z poziomu zdarzenia zabezpieczeń lub alertu. Wybrana opcja zależy od Twoich potrzeb. Poniższa procedura umożliwia rozpoczęcie badania z poziomu alertu:

1.  Otwórz pulpit nawigacyjny usługi **Security Center**.
2.  Kliknij pozycję **Alerty zabezpieczeń** i wybierz zdarzenie, które chcesz zbadać.
3.  Na stronie zdarzenia kliknij przycisk **Rozpocznij badanie**. Zostanie wyświetlony pulpit nawigacyjny funkcji **Badanie**.

    ![Alerty](./media/security-center-investigation/security-center-investigation-fig8.png)

4. Z tego pulpitu nawigacyjnego można wybrać jednostkę na mapie. Po prawej stronie ekranu pojawią się odpowiednie informacje na temat tej jednostki.

    ![Pulpit nawigacyjny funkcji Badanie](./media/security-center-investigation/security-center-investigation-fig9.png)

W tym miejscu można zbadać jednostki, które brały udział w tym zdarzeniu, i uzyskać więcej szczegółowych informacji na temat każdej z nich. 

## <a name="see-also"></a>Zobacz też
W tym dokumencie przedstawiono sposób użycia funkcji badania w usłudze Security Center. Aby dowiedzieć się więcej na temat Centrum zabezpieczeń, zobacz następujące artykuły:

* [Reagowanie na alerty zabezpieczeń i zarządzanie nimi w usłudze Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-managing-and-responding-alerts). Dowiedz się, jak zarządzać alertami i reagować na zdarzenia związane z bezpieczeństwem w usłudze Security Center.
* [Monitorowanie kondycji zabezpieczeń w usłudze Azure Security Center](security-center-monitoring.md). Informacje na temat sposobu monitorowania kondycji zasobów platformy Azure.
* [Informacje o alertach zabezpieczeń w usłudze Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-alerts-type). Poznaj różne typy alertów zabezpieczeń.
* [Przewodnik rozwiązywania problemów z usługą Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-troubleshooting-guide). Dowiedz się, jak rozwiązywać typowe problemy z usługą Security Center. 
* [Azure Security Center — często zadawane pytania](security-center-faq.md). Odpowiedzi na często zadawane pytania dotyczące korzystania z usługi.
* [Blog Azure Security](http://blogs.msdn.com/b/azuresecurity/). Wpisy na blogu dotyczące zabezpieczeń i zgodności platformy Azure.

