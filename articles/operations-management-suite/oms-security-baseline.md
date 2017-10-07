---
title: "aaaOperations zabezpieczeń pakietu administracyjnego i inspekcji rozwiązania bazową | Dokumentacja firmy Microsoft"
description: "W tym dokumencie opisano sposób toouse OMS zabezpieczeń i inspekcji tooperform rozwiązania na podstawie oceny linii bazowej wszystkich monitorowanych komputerów w celu zgodności i zabezpieczeń."
services: operations-management-suite
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: 
ms.assetid: 17837c8b-3e79-47c0-9b83-a51c6ca44ca6
ms.service: operations-management-suite
ms.custom: oms-security
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: yurid
ms.openlocfilehash: ea52408cb9d2598728fe3826a946067e1c99318f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="baseline-assessment-in-operations-management-suite-security-and-audit-solution"></a>Ocena linii bazowej w rozwiązaniu Zabezpieczenia i inspekcja w pakiecie Operations Management Suite
Ten dokument ułatwia toouse [zabezpieczeń Operations Management Suite (OMS) i rozwiązania inspekcji](operations-management-suite-overview.md) oceny linii bazowej tooaccess możliwości hello bezpieczny stan monitorowanych zasobów.

## <a name="what-is-baseline-assessment"></a>Co to jest ocena linii bazowej?
Firma Microsoft, wraz z instytucjami branżowymi i rządowymi na całym świecie, zdefiniowała konfigurację systemu Windows, która reprezentuje wdrożenia serwera o wysokim poziomie zabezpieczeń. Konfiguracja ta stanowi zestaw kluczy rejestru, ustawień zasad inspekcji i ustawień zasad zabezpieczeń wraz z zalecanymi przez firmę Microsoft wartościami tych ustawień. Ten zestaw reguł jest określany jako linia bazowa zabezpieczeń. Ocena linii bazowej w rozwiązaniu Zabezpieczenia i inspekcja w pakiecie OMS umożliwia bezproblemowe skanowanie wszystkich komputerów pod kątem zgodności. 

Możliwe typy reguł to:

* **Reguły rejestru**: sprawdzenie, czy klucze rejestru są prawidłowo ustawione.
* **Reguły zasad inspekcji**: reguły dotyczące zasad inspekcji.
* **Reguły zasad zabezpieczeń**: zasady dotyczące hello uprawnień na komputerze hello.

> [!NOTE]
> Odczyt [tooassess zabezpieczeń OMS Użyj hello linii bazowej konfiguracji zabezpieczeń](https://blogs.technet.microsoft.com/msoms/2016/08/12/use-oms-security-to-assess-the-security-configuration-baseline/) dla krótkie omówienie tej funkcji.
> 
> 

## <a name="security-baseline-assessment"></a>Ocena linii bazowej zabezpieczeń
Możesz przejrzeć bieżącej oceny linii bazowej wszystkie komputery, które są monitorowane przez OMS zabezpieczeń i inspekcji przy użyciu pulpitu nawigacyjnego hello zabezpieczeń.  Wykonaj powitania po tooaccess kroki hello planu bazowego zabezpieczeń oceny pulpitu nawigacyjnego:

1. W hello **programu Microsoft Operations Management Suite** głównym pulpicie nawigacyjnym, kliknij przycisk **zabezpieczeń i inspekcji** kafelka.
2. W hello **zabezpieczeń i inspekcji** pulpitu nawigacyjnego, kliknij przycisk **oceny linii bazowej** w obszarze **domen zabezpieczeń**. Witaj **oceny linii bazowej zabezpieczeń** pulpitu nawigacyjnego pojawia się, jak pokazano w powitania po obrazu:
   
    ![Ocena linii bazowej w rozwiązaniu Zabezpieczenia i inspekcja w pakiecie OMS](./media/oms-security-baseline/oms-security-baseline-fig1.png)

Ten pulpit nawigacyjny dzieli się na trzy główne obszary:

* **Komputery w porównaniu toobaseline**: w tej sekcji przedstawiono podsumowanie hello liczbę komputerów, które były dostępne i hello procent komputerów, których ocena hello zakończyło się powodzeniem. Udostępnia także hello top 10 komputerów i wynik procent hello hello oceny.
* **Wymagany stan reguł**: Ta sekcja zawiera hello konwersji toobring pogłębianie wiedzy na temat reguł nie powiodło się hello według ważności i nie powiodło się reguły według typu. Przeszukując toohello pierwszego wykresu, który umożliwi szybkie identyfikowanie Jeśli hello większości reguł nie powiodła się są kluczowe, czy nie. Udostępnia listę hello top reguły nie powiodło się 10 i ich ważność. Witaj drugi wykres przedstawia hello typu reguły, które zakończyły się niepowodzeniem podczas oceny hello. 
* **Komputery z brakującą oceny linii bazowej**: w tej sekcji listy hello komputerów, które nie były dostępne toooperating niezgodności systemu lub błędów. 

### <a name="accessing-computers-compared-toobaseline"></a>Uzyskiwanie dostępu do komputerów w porównaniu toobaseline
W idealnym przypadku wszystkie komputery znajdują się być zgodny z oceny linii bazowej zabezpieczeń hello. Jednak można się spodziewać, że w pewnych okolicznościach tak nie będzie. W ramach procesu zarządzania hello zabezpieczeń jest ważne tooinclude recenzowania hello komputerów, których nie powiodła się toopass wszystkie testy oceny zabezpieczeń. Toovisualize szybkie, nie jest wybranie opcji hello **dostęp do komputerów** znajduje się w hello **komputery w porównaniu toobaseline** sekcji. Jak przedstawiono w powitania po ekranie powinien zostać wyświetlony hello dziennika listy wyników wyszukiwania przedstawiający hello komputerów:

![Wyniki wyszukiwania komputerów, do których uzyskano dostęp](./media/oms-security-baseline/oms-security-baseline-fig2.png)

wynik wyszukiwania Hello jest wyświetlana w formacie tabeli, w którym hello pierwsza kolumna została podana nazwa komputera hello, a drugi kolor hello ma hello liczbę reguł, których nie powiodła się. tooretrieve hello informacje dotyczące typu hello reguły, które zakończyły się niepowodzeniem, kliknij hello liczba nieudanych reguł oprócz hello nazwy komputera. Powinny pojawić się wynik toohello podobne, co pokazano na powitania po obrazu:

![Szczegółowe wyniki wyszukiwania komputerów, do których uzyskano dostęp](./media/oms-security-baseline/oms-security-baseline-fig3.png)

W tym wynik wyszukiwania znajdują się łącznie hello reguł dostępu, hello liczba krytycznych zasady, których nie powiodła się, hello ostrzeżenie reguły a hello reguły informacji nie powiodło się.

### <a name="accessing-required-rules-status"></a>Uzyskiwanie dostępu do stanu wymaganych reguł
Po uzyskaniu hello informacje dotyczące hello procent liczby komputerów, których ocena hello zakończyło się powodzeniem, może być tooobtain więcej informacji o regułach, które kończą się niepowodzeniem zgodnie z toohello zagrożenia. Dzięki temu wizualizacji tooprioritize komputery, które powinny być adresowane tooensure pierwszy będą zgodne w ocenie dalej hello. Umieść kursor nad hello krytyczną częścią wykresu hello znajduje się w hello **nie powiodło się reguły według ważności** kafelka w obszarze **wymagany stan reguł** i kliknij ją. Wynik toohello podobne, po ekranie powinien zostać wyświetlony:

![Niespełnione reguły według ważności — szczegóły](./media/oms-security-baseline/oms-security-baseline-fig4.png) 

W wyniku tego dziennika widać hello typu reguły linii bazowej, który uległ awarii, hello opis tej zasady i identyfikator typowych konfiguracji wyliczenie CCE () hello tę regułę zabezpieczeń. Te atrybuty powinny być za mało tooperform toofix działań naprawczych tego problemu w hello komputera docelowego.

> [!NOTE]
> Aby uzyskać więcej informacji na temat CCE dostępu hello [National luki w zabezpieczeniach bazy danych](https://nvd.nist.gov/cce/index.cfm).
> 
> 

### <a name="accessing-computers-missing-baseline-assessment"></a>Dostęp do komputerów, dla których brak oceny linii bazowej
OMS obsługuje hello członkiem domeny i profilu planu bazowego kontrolera domeny systemu Windows Server 2008 R2 tooWindows Server 2012 R2. Ostateczna wersja linii bazowej dla systemu Windows Server 2016 nie jest jeszcze opracowana i zostanie dodana natychmiast po jej opublikowaniu. Wszystkie inne systemy operacyjne skanowania za pomocą oceny linii bazowej OMS zabezpieczeń i inspekcji jest wyświetlany w obszarze hello **komputery z brakującą oceny linii bazowej** sekcji.

## <a name="see-also"></a>Zobacz też
Ten dokument przedstawia informacje na temat oceny linii bazowej w rozwiązaniu Zabezpieczenia i inspekcja w pakiecie OMS. toolearn więcej informacji na temat zabezpieczeń OMS, zobacz następujące artykuły hello:

* [Omówienie pakietu Operations Management Suite (OMS)](operations-management-suite-overview.md)
* [Monitorowanie i alerty tooSecurity odpowiada Operations Management Suite zabezpieczeń i rozwiązanie inspekcji](oms-security-responding-alerts.md)
* [Monitorowanie zasobów w rozwiązaniu Zabezpieczenia i inspekcja w pakiecie Operations Management Suite](oms-security-monitoring-resources.md)

