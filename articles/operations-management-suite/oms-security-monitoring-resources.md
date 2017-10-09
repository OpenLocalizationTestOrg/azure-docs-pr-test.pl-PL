---
title: "aaaMonitoring zasobów Operations Management Suite zabezpieczeń i inspekcji rozwiązania | Dokumentacja firmy Microsoft"
description: "Ten dokument ułatwia toouse OMS zabezpieczeń i toomonitor możliwości inspekcji zasobów i zidentyfikować problemy z zabezpieczeniami."
services: operations-management-suite
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: 
ms.assetid: d6752120-821f-4aa7-a049-25bf5a653b95
ms.service: operations-management-suite
ms.custom: oms-security
ms.topic: article
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: yurid
ms.openlocfilehash: 932b946ae1ffa3b979c02f419702d42d46abf7ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="monitoring-resources-in-operations-management-suite-security-and-audit-solution"></a>Monitorowanie zasobów Operations Management Suite zabezpieczeń i rozwiązanie inspekcji
Ten dokument ułatwia OMS zabezpieczeń i użyć toomonitor możliwości inspekcji zasobów oraz identyfikowanie problemów z zabezpieczeniami.

## <a name="what-is-oms"></a>Co to jest pakiet OMS?
Microsoft Operations Management Suite (OMS) to rozwiązanie do zarządzania IT, które pomaga zarządzać i chronić lokalnej i w chmurze infrastruktury opartej na chmurze firmy Microsoft. Aby uzyskać więcej informacji na temat pakietu OMS, przeczytaj artykuł hello [Operations Management Suite](https://technet.microsoft.com/library/mt484091.aspx).

## <a name="monitoring-resources"></a>Monitorowanie zasobów
Zawsze, gdy jest to możliwe, należy tooprevent naruszających zapobiec w miejscu pierwszego hello. Jest jednak możliwe tooprevent wszystkie zdarzenia zabezpieczeń. Gdy wystąpi zdarzenie zabezpieczeń, konieczne będzie tooensure zminimalizowane wpływu.  Istnieją trzy krytyczne zaleceń, które mogą być używane toominimize hello numeru i hello wpływu naruszenia zabezpieczeń:

* Regularnie oceny luk w zabezpieczeniach w danym środowisku.
* Sprawdź rutynowo wszystkich systemów komputerowych i tooensure urządzeń sieciowych, które mają wszystkie zainstalowane najnowsze poprawki hello.
* Regularnie sprawdzić wszystkie dzienniki i mechanizmów rejestrowania, w tym dzienniki zdarzeń systemu operacyjnego, określonych Dzienniki aplikacji i dzienniki systemu wykrywania nieautoryzowanego dostępu.

OMS zabezpieczeń i inspekcji umożliwia rozwiązanie IT tooactively monitorowanie wszystkich zasobów, które mogą pomóc zminimalizować wpływ hello zdarzeń zabezpieczeń. Zabezpieczenia OMS i inspekcji ma domen zabezpieczeń, które mogą służyć do monitorowania zasobów. domen zabezpieczeń Hello zapewnia szybki dostęp do opcji tooa, dla hello monitorowania zabezpieczeń następujących domen zostaną opisane bardziej szczegółowe informacje:

* oceny złośliwego oprogramowania
* Ocena aktualizacji
* Tożsamość i dostęp

> [!NOTE]
> Omówienie tych opcji, należy przeczytać [wprowadzenie Operations Management Suite zabezpieczeń i rozwiązanie inspekcji](oms-security-getting-started.md).
> 
> 

### <a name="monitoring-system-protection"></a>Monitorowanie systemu ochrony
W bardziej głębokość podejście jest ważna w przypadku hello co warstwę ochrony ogólny stan zabezpieczeń zawartości. Komputery z wykrył, że zagrożenia i komputery z niewystarczającą ochroną są wyświetlane w hello kafelka oceny złośliwego oprogramowania w obszarze domen zabezpieczeń. Korzystając z informacji hello na powitania oceny złośliwego oprogramowania, należy zidentyfikować serwery toohello ochrony tooapply planu, które go potrzebują. tooaccess tej opcji hello wykonaj kroki opisane poniżej:

1. W hello **programu Microsoft Operations Management Suite** głównym pulpicie nawigacyjnym kliknij **zabezpieczeń i inspekcji** kafelka.
   
    ![Bezpieczeństwo i inspekcji](./media/oms-security-responding-alerts/oms-security-responding-alerts-fig1.png)
2. W hello **zabezpieczeń i inspekcji** pulpitu nawigacyjnego, kliknij przycisk **oceny ochrony przed złośliwym kodem** w obszarze **domen zabezpieczeń**. Witaj **oceny ochrony przed złośliwym kodem** pulpitu nawigacyjnego pojawia się, jak pokazano poniżej:

![oceny złośliwego oprogramowania](./media/oms-security-monitoring-resources/oms-security-monitoring-resources-fig2-ga.png)

Można użyć hello **oceny złośliwego oprogramowania** hello tooidentify pulpitu nawigacyjnego następujące problemy z zabezpieczeniami:

* **Zagrożenia Active**: komputery, które zostały naruszone i ma aktywne zagrożenia w systemie hello.
* **Skorygowane zagrożenia**: komputery, które zostały naruszone, ale zagrożenia hello zostały skorygowane.
* **Nieaktualny podpis**: komputery, które mają włączony, ale hello sygnatury ochrony przed złośliwym oprogramowaniem jest nieaktualny.
* **Brak ochrony w czasie rzeczywistym**: komputery, które nie mają ochrony przed złośliwym kodem, zainstalować.

### <a name="monitoring-updates"></a>monitorowanie aktualizacji
Stosowanie najnowszych aktualizacji zabezpieczeń hello jest ze względów bezpieczeństwa i powinny zostać włączone w strategii zarządzania aktualizacji. Usługa Microsoft Monitoring Agent (HealthService.exe) odczytuje informacje dotyczące aktualizacji z monitorowanych komputerów, a następnie wysyła to zaktualizowane informacje toohello usługę w chmurze hello do przetwarzania. Hello usługi Microsoft Monitoring Agent jest skonfigurowany jako Usługa automatyczna i powinna być zawsze uruchomiona w hello komputera docelowego.

![monitorowanie aktualizacji](./media/oms-security-monitoring-resources/oms-security-monitoring-resources-fig3.png)

Logika jest toohello zastosowanych aktualizacji danych i usługi w chmurze hello rejestruje dane hello. W przypadku znalezienia brakujących aktualizacji są wyświetlane na powitania **aktualizacje** pulpitu nawigacyjnego. Można użyć hello **aktualizacje** toowork pulpitu nawigacyjnego z brakującymi aktualizacji i opracowanie tooapply planu ich toohello serwerów, które są potrzebne. Wykonaj kroki hello poniżej tooaccess hello **aktualizacje** pulpitu nawigacyjnego:

1. W hello **programu Microsoft Operations Management Suite** głównym pulpicie nawigacyjnym kliknij **zabezpieczeń i inspekcji** kafelka.
2. W hello **zabezpieczeń i inspekcji** pulpitu nawigacyjnego, kliknij przycisk **oceny aktualizacji** w obszarze **domen zabezpieczeń**. pulpit nawigacyjny aktualizacji Hello pojawia się, jak pokazano poniżej:

![Oceny aktualizacji](./media/oms-security-monitoring-resources/oms-security-monitoring-resources-fig4.png)

Na tym pulpicie nawigacyjnym można wykonać aktualizacji oceny toounderstand hello bieżącego stanu komputerów i adresów hello najważniejszych zagrożenia. Za pomocą hello **aktualizacje krytyczne lub zabezpieczeń** kafelka, Administratorzy IT będą mogli tooaccess szczegółowe informacje na temat hello aktualizacje, które nie są spełnione, jak pokazano poniżej:

![Wynik wyszukiwania](./media/oms-security-monitoring-resources/oms-security-monitoring-resources-fig5.png)

W tym raporcie obejmują krytyczne informacje, które mogą być używane tooidentify hello rodzaju zagrożenia ten system jest zagrożony, zawiera artykuły bazy wiedzy Microsoft KB hello skojarzonych z hello aktualizacji zabezpieczeń i hello MS Bulletin zawierający więcej szczegółów na temat hello luki w zabezpieczeniach.

### <a name="monitoring-identity-and-access"></a>Monitorowanie tożsamościami i dostępem
Użytkownikom pracy z dowolnego miejsca, przy użyciu różnych urządzeń i uzyskiwanie dostępu do dużych ilości aplikacji w chmurze i lokalnych konieczne jest ochronę poświadczeń. Ataki kradzieży poświadczeń to takie, w których atakujący początkowo uzyska tooaccess poświadczenia dostępu tooa regularne użytkownika systemu w ramach sieci hello. Wiele razy atak początkowej jest tylko sposób tooget toohello sieć dostępu, hello ostatecznym celem jest toodiscover uprawnień konta. 

Osoby atakujące pozostanie w sieci hello przy użyciu bezpłatnych narzędzi tooextract poświadczenia z sesji hello innych kont logowania. W zależności od konfiguracji systemu hello można wyodrębnić te poświadczenia w postaci hello skrótów, biletów lub haseł, nawet w postaci zwykłego tekstu.  

> [!NOTE]
> maszyny, które są bezpośrednio widoczne toohello Internet zostanie wyświetlone wiele nie powiodło się prób tego toologin try przy użyciu wszystkich rodzajów dobrze znane nazwy użytkowników (np. administratora). W większości przypadków jest OK hello dobrze znane nazwy użytkowników nie są używane i jest wystarczająco silne hasło hello.
> 
> 

Go przed ich naruszyć bezpieczeństwo konta uprawnienie tooidentify możliwe jest tych intruzów. Można wykorzystać **OMS zabezpieczeń i rozwiązanie inspekcji** toomonitor tożsamościami i dostępem. Wykonaj kroki hello poniżej tooaccess hello **tożsamościami i dostępem** pulpitu nawigacyjnego:

1. W hello **programu Microsoft Operations Management Suite** głównym pulpicie nawigacyjnym kliknij zabezpieczeń i inspekcji kafelka.
2. W hello **zabezpieczeń i inspekcji** pulpitu nawigacyjnego, kliknij przycisk **tożsamościami i dostępem** w obszarze **domen zabezpieczeń**. Witaj **tożsamościami i dostępem** pulpitu nawigacyjnego pojawia się, jak pokazano poniżej:

![Tożsamość i dostęp](./media/oms-security-monitoring-resources/oms-security-monitoring-resources-fig6-ga.png)

W ramach strategii regularnego monitorowania należy uwzględnić monitorowanie tożsamości. Administrator IT powinien wyglądać w przypadku określonych prawidłowej nazwy użytkownika, który ma wiele prób. To może wskazywać każda osoba atakująca nabytej hello rzeczywistą nazwę użytkownika i spróbuj toobrute force lub automatyczne narzędzie, które używa ustalony hasło wygasło.

Włącz ten pulpit nawigacyjny IT tooquickly zidentyfikować potencjalne zagrożenia powiązane dostępu i tooidentity toocompany w zasobów. Jest konkretnym ważne tooalso trendów potencjalnych, na przykład hello kafelka logowania w czasie, zawiera w czasie, ile razy wykonano nieudane próby logowania. W takim przypadku hello komputera **plików** Odebrano 35 prób logowania. Więcej informacji na temat tego komputera można sprawdzić, klikając go. 

![więcej informacji](./media/oms-security-monitoring-resources/oms-security-monitoring-resources-fig7-new.png)

Raport Hello wygenerowany dla tego komputera powoduje cenne szczegółów dotyczących tego wzorca. Zauważyć, że hello **konta** zapewnia kolumny hello konta użytkownika, który był używany tootry tooaccess hello systemu, hello **TIMEGENERATED** zapewnia kolumny hello interwał czasu, w którym hello Wykonano próbę i Witaj **LOGONTYPENAME** hello lokalizacji, gdzie była wykonywana ta próba zapewnia kolumny. Jeśli te próby były wykonywane lokalnie w systemie hello przez program, hello **procesu** kolumny będą wyświetlane nazwa procesu hello. W scenariuszach, w którym hello próba logowania pochodzi z programu masz już hello nazwa procesu jest dostępna i można teraz wykonywać dalszych badań w systemie docelowym hello.

## <a name="see-also"></a>Zobacz też
W tym dokumencie możesz przedstawiono sposób toomonitor rozwiązania toouse OMS zabezpieczeń i inspekcji zasobów. toolearn więcej informacji na temat zabezpieczeń OMS, zobacz następujące artykuły hello:

* [Omówienie pakietu Operations Management Suite (OMS)](operations-management-suite-overview.md)
* [Wprowadzenie do programu Operations Management Suite zabezpieczeń i rozwiązanie inspekcji](oms-security-getting-started.md)
* [Monitorowanie i alerty tooSecurity odpowiada Operations Management Suite zabezpieczeń i rozwiązanie inspekcji](oms-security-responding-alerts.md)

