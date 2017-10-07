---
title: "aaaManage alerty zabezpieczeń w Centrum zabezpieczeń Azure | Dokumentacja firmy Microsoft"
description: "Ten dokument pomaga możesz toouse Centrum zabezpieczeń Azure możliwości toomanage i Odpowiedz toosecurity alertów."
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: b88a8df7-6979-479b-8039-04da1b8737a7
ms.service: security-center
ms.topic: hero-article
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/19/2017
ms.author: yurid
ms.openlocfilehash: f1cb7e4770776827b75ed15893914678c1f44216
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="managing-and-responding-toosecurity-alerts-in-azure-security-center"></a>Reagowanie na alerty toosecurity w Centrum zabezpieczeń Azure i zarządzanie nimi
Ten dokument ułatwia Użyj toomanage Centrum zabezpieczeń Azure i reagowania na alerty toosecurity.

> [!NOTE]
> wykryć tooenable zaawansowane, uaktualnienia tooAzure Security Center Standard. Dostępna jest bezpłatna 60-dniowa wersja próbna. tooupgrade, wybierz opcję warstwy cenowej w hello [zasady zabezpieczeń](security-center-policies.md). Zobacz [cennik Centrum zabezpieczeń Azure](security-center-pricing.md) toolearn więcej.
>
>

## <a name="what-are-security-alerts"></a>Czym są alerty zabezpieczeń?
Centrum zabezpieczeń automatycznie gromadzi informacje, analizuje i integruje dane dzienników z zasobów platformy Azure, sieci hello, połączone rozwiązań partnerskich, takich jak zapory i punktu końcowego rozwiązań do ochrony, toodetect prawdziwe zagrożenia i redukować liczbę fałszywych alarmów. Lista alertów zabezpieczeń uporządkowanych według priorytetu jest wyświetlany w Centrum zabezpieczeń oraz hello informacje potrzebne tooquickly Zbadaj hello problem i zalecenia dotyczące tooremediate atak.


> [!NOTE]
> Aby uzyskać więcej informacji na temat sposobu działania funkcji wykrywania usługi Security Center, przeczytaj [Funkcje wykrywania usługi Azure Security Center](security-center-detection-capabilities.md).
>
>

## <a name="managing-security-alerts"></a>Zarządzanie alertami zabezpieczeń
Bieżące alerty można przeglądać, analizując hello **alerty zabezpieczeń** kafelka. Otwórz Azure Portal i wykonaj kroki hello poniżej toosee więcej szczegółów dotyczących poszczególnych alertów:

1. Na pulpicie nawigacyjnym Centrum zabezpieczeń hello, zobaczysz hello **alerty zabezpieczeń** kafelka.

    ![Kafelek Alerty zabezpieczeń w usłudze Security Center](./media/security-center-managing-and-responding-alerts/security-center-managing-and-responding-alerts-fig1-ga.png)

2. Kliknij przycisk hello kafelka tooopen hello **alerty zabezpieczeń** blok zawierający więcej szczegółów na temat hello alertów, jak pokazano poniżej.

   ![Witaj blok alerty zabezpieczeń w Centrum zabezpieczeń](./media/security-center-managing-and-responding-alerts/security-center-managing-and-responding-alerts-fig2-ga.png)

W dolnej części tego bloku hello są hello uzyskać szczegółowe informacje o każdym alercie. toosort, kliknij kolumnę hello, który ma toosort przez. Poniżej podano Hello definicje poszczególnych kolumn:

* **Opis elementu**: Krótki opis alertu hello.
* **Liczba**: lista wszystkich alertów określonego typu, które zostały wykryte w określonym dniu.
* **Wykryte przez**: hello usługa, która jest odpowiedzialna za wyzwolenie alertu hello.
* **Data**: hello Data zdarzenie hello wystąpił.
* **Stan**: hello bieżący stan alertu. Istnieją dwa typy stanów:
  * **Aktywne**: wykryto alert zabezpieczeń hello.
* **Ważność**: hello poziom ważności, który może być wysoki, średni lub niski.

### <a name="filtering-alerts"></a>Filtrowanie alertów
Alerty można filtrować na podstawie daty, stanu i ważności. Filtrowanie alertów może być przydatne w scenariuszach wymagających toonarrow hello zakres wyświetlanych alertów zabezpieczeń. Na przykład użytkownik ma tooaddress alerty zabezpieczeń, które wystąpiły w hello ostatnich 24 godzinach, ponieważ badasz potencjalne naruszenie zabezpieczeń w systemie hello.

1. Kliknij przycisk **filtru** na powitania **alerty zabezpieczeń** bloku. Witaj **filtru** zostanie otwarty blok i wybierz wartości daty, stanu i ważności hello mają toosee.

    ![Filtrowanie alertów w usłudze Security Center](./media/security-center-managing-and-responding-alerts/security-center-managing-and-responding-alerts-fig3-2017.png)

### <a name="respond-toosecurity-alerts"></a>Odpowiadanie na alerty toosecurity
Wybierz toolearn alertu zabezpieczeń wymagają więcej informacji na temat hello zdarzenia, która wyzwoliła hello alert i co, jeśli kroki, możesz tooremediate tootake atak. Alerty zabezpieczeń są grupowane według typu i daty. Kliknięcie alertu zabezpieczeń spowoduje otwarcie bloku zawierającego listę hello pogrupowanych alertów.

![Odpowiadanie na alerty toosecurity w Centrum zabezpieczeń Azure](./media/security-center-managing-and-responding-alerts/security-center-managing-and-responding-alerts-fig5-ga.png)

W tym przypadku wyzwolone alerty hello można znaleźć toosuspicious działania protokołu RDP (Remote Desktop). Witaj pierwsza kolumna zawiera zaatakowane zasoby; Witaj drugi Pokazuje ile razy zaatakowany zasób hello; Witaj innej przedstawia czas hello atak powitania; Witaj czwarty pokazuje stan alertu hello; i hello piąte pokazuje hello ważność atak powitania. Po przejrzeniu tych informacji kliknij zaatakowany zasób hello i zostanie otwarty nowy blok.

![Sugestie dotyczące alertów jakie toodo dotyczących zabezpieczeń w Centrum zabezpieczeń Azure](./media/security-center-managing-and-responding-alerts/security-center-managing-and-responding-alerts-fig6-ga.png)

W hello **opis** tego bloku można znaleźć więcej szczegółów dotyczących tego zdarzenia. Te dodatkowe szczegóły zapewniają wgląd w jaki wyzwalanych hello zabezpieczeń alertów, hello zasobu docelowego, gdy dotyczy hello źródłowy adres IP i zaleceń dotyczących tooremediate.  W niektórych przypadkach hello źródłowy adres IP będzie pusty (niedostępny), ponieważ nie wszystkie dzienniki zdarzeń zabezpieczeń systemu Windows obejmują adres IP hello.

Witaj naprawcze sugerowane w Centrum zabezpieczeń będą się różnić zgodnie z alert zabezpieczeń toohello. W niektórych przypadkach może być toouse tooimplement innych funkcji platformy Azure hello zalecane korygowania. Na przykład Witaj korygowania takiego ataku jest adres IP hello tooblacklist generujących atak przy użyciu [sieciowej listy ACL](../virtual-network/virtual-networks-acl.md) lub [sieciowej grupy zabezpieczeń](../virtual-network/virtual-networks-nsg.md) reguły.

> [!NOTE]
> Aby uzyskać więcej informacji na powitania różnych typów alertów, przeczytaj [alerty zabezpieczeń według typu w Centrum zabezpieczeń Azure](security-center-alerts-type.md).
>
>

## <a name="see-also"></a>Zobacz też
W tym dokumencie możesz przedstawiono sposób tooconfigure zasad zabezpieczeń w Centrum zabezpieczeń. toolearn więcej informacji na temat Centrum zabezpieczeń, zobacz następujące hello:

* [Obsługa zdarzeń naruszenia zabezpieczeń w usłudze Azure Security Center](security-center-incident.md)
* [Funkcje wykrywania usługi Azure Security Center](security-center-detection-capabilities.md)
* [Przewodnik planowania i obsługi usługi Azure Security Center](security-center-planning-and-operations-guide.md)
* [Centrum zabezpieczeń Azure — często zadawane pytania](security-center-faq.md) — często zadawane pytania dotyczące korzystania z usługi hello Znajdź.
* [Blog Azure Security](http://blogs.msdn.com/b/azuresecurity/) — wpisy na blogu dotyczące zabezpieczeń i zgodności platformy Azure.
