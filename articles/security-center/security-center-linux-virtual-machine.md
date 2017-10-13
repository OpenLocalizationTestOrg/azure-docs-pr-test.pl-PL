---
title: "Usługi Azure Security Center i Azure Virtual Machines z systemem Linux | Microsoft Docs"
description: "Ten dokument pomaga zrozumieć, jak usługa Azure Security Center chroni maszyny wirtualne Azure Virtual Machines."
services: security-center
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: 
ms.assetid: 5fe5a12c-5d25-430c-9d47-df9438b1d7c5
ms.service: security-center
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/03/2017
ms.author: yurid
ms.openlocfilehash: 0df4fca59575bd8e18e91fea2066a9e694ed320d
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/11/2017
---
# <a name="azure-security-center-and-azure-virtual-machines-with-linux"></a>Usługi Azure Security Center i Azure Virtual Machines z systemem Linux
Usługa [Azure Security Center](https://azure.microsoft.com/services/security-center/) pomaga w zapobieganiu zagrożeniom, wykrywaniu ich i reagowaniu na nie. Zapewnia zintegrowane monitorowanie zabezpieczeń i zarządzanie zasadami subskrypcji platformy Azure, pomaga wykrywać zagrożenia, które w przeciwnym razie mogłyby pozostać niezauważone, a także współpracuje z szerokim ekosystemem rozwiązań z zakresu zabezpieczeń.

W tym artykule przedstawiono, jak usługa Security Center może pomóc w ochronie maszyn wirtualnych Azure Virtual Machines z systemem operacyjnym Linux.

## <a name="why-use-security-center"></a>Dlaczego warto korzystać z usługi Security Center?
Usługa Security Center pomaga chronić dane maszyny wirtualnej na platformie Azure, zapewniając wgląd w ustawienia zabezpieczeń na maszynie wirtualnej i monitorując zagrożenia. Usługa Security Center może monitorować maszyny wirtualne pod kątem następujących elementów: 

* Ustawienia zabezpieczeń systemu operacyjnego z zalecanymi regułami konfiguracji
* Informacje o brakujących zabezpieczeniach systemu i aktualizacjach krytycznych
* Zalecenia dotyczące ochrony punktów końcowych
* Weryfikowanie szyfrowania dysków
* Ataki oparte na sieci (opcja dostępna tylko w [wersji standardowej](https://azure.microsoft.com/en-us/pricing/details/security-center/))

Oprócz wspomagania ochrony maszyn wirtualnych platformy Azure usługa Security Center zapewnia także monitorowanie zabezpieczeń i zarządzanie nimi w zakresie usług Cloud Services, App Services, Virtual Networks i innych. 

> [!NOTE]
> Aby dowiedzieć się więcej na temat usługi Azure Security Center, zobacz [Wprowadzenie do usługi Azure Security Center](security-center-intro.md).
> 
> 

## <a name="prerequisites"></a>Wymagania wstępne
Aby rozpocząć pracę z usługą Azure Security Center, należy uwzględnić następujące informacje:

* Potrzebna jest subskrypcja platformy Microsoft Azure. Aby uzyskać więcej informacji o warstwach Bezpłatna i Standardowa usługi Security Center, zobacz [Cennik usługi Security Center](https://azure.microsoft.com/pricing/details/security-center/).
* Zaplanuj wdrożenie usługi Security Center. Aby uzyskać więcej informacji o zagadnieniach związanych z planowaniem i obsługą, zobacz [Przewodnik planowania i obsługi usługi Azure Security Center](security-center-planning-and-operations-guide.md).
* Aby uzyskać informacje dotyczące możliwości obsługi systemu operacyjnego, zobacz [Azure Security Center — często zadawane pytania](security-center-faq.md). 

## <a name="set-security-policy"></a>Ustawianie zasad zabezpieczeń
Aby usługa Azure Security Center mogła zbierać informacje niezbędne do udostępniania zaleceń i alertów generowanych na podstawie skonfigurowanych zasad zabezpieczeń, trzeba włączyć zbieranie danych. Na poniższej ilustracji przedstawiono zrzut ekranu, na którym **Zbieranie danych** jest **Włączone**.

Zasady zabezpieczeń określają zestaw mechanizmów kontrolnych, które są zalecane dla zasobów w określonej subskrypcji lub grupie zasobów. Przed włączeniem zasad zabezpieczeń należy włączyć zbieranie danych. Usługa Security Center zbiera dane z maszyn wirtualnych w celu oceny ich stanu zabezpieczeń, przekazywania zaleceń dotyczących zabezpieczeń oraz alertów dotyczących zagrożeń. W usłudze Security Center można zdefiniować zasady dla grup zasobów lub subskrypcji Azure zgodnie z potrzebami zabezpieczeń firmy i typem aplikacji oraz poufnością danych w poszczególnych subskrypcjach. 

![Zasady zabezpieczeń](./media/security-center-linux-virtual-machine/security-center-linux-virtual-machine-fig1.png)

> [!NOTE]
> Aby dowiedzieć się więcej na temat poszczególnych dostępnych **zasad zapobiegania**, zobacz artykuł [Ustawianie zasad zabezpieczeń](security-center-policies.md).
> 

## <a name="manage-security-recommendations"></a>Zarządzanie zaleceniami dotyczącymi zabezpieczeń
Usługa Security Center analizuje stan zabezpieczeń zasobów platformy Azure. Po znalezieniu potencjalnych luk w zabezpieczeniach usługa Security Center tworzy odpowiednie zalecenia. Przewodnik dotyczący zaleceń prowadzi użytkownika przez proces konfigurowania wymaganych kontrolek.

Po skonfigurowaniu zasad zabezpieczeń usługa Security Center analizuje stan zabezpieczeń zasobów w celu identyfikowania potencjalnych luk w zabezpieczeniach. Zalecenia są wyświetlane w postaci tabeli, gdzie każdy wiersz reprezentuje jedno zalecenie. W poniższej tabeli przedstawiono przykładowe zalecenia dotyczące maszyn wirtualnych platformy Azure z systemem operacyjnym Linux oraz efekt zastosowania poszczególnych zaleceń. Po wybraniu zalecenia są wyświetlane informacje przedstawiające sposób realizacji zalecenia w usłudze Security Center.

| Zalecenie | Opis |
| --- | --- |
| [Włącz zbieranie danych dla subskrypcji](security-center-enable-data-collection.md) |Zaleca włączenie zbierania danych w zasadach zabezpieczeń dla każdej subskrypcji i wszystkich maszyn wirtualnych w subskrypcjach. |
| [Koryguj luki w zabezpieczeniach systemu operacyjnego](security-center-remediate-os-vulnerabilities.md) |Zaleca dostosowanie konfiguracji systemu operacyjnego do zalecanych reguł konfiguracji (np. uniemożliwienie zapisywania haseł). |
| [Zastosuj aktualizacje systemu](security-center-apply-system-updates.md) |Zaleca wdrożenie na maszynach wirtualnych brakujących zabezpieczeń systemu i aktualizacji krytycznych. |
| [Uruchom ponownie po zaktualizowaniu systemu](security-center-apply-system-updates.md#reboot-after-system-updates) |Zaleca ponowne uruchomienie maszyny wirtualnej w celu ukończenia procesu stosowania aktualizacji systemu. |
| [Włącz agenta maszyny wirtualnej](security-center-enable-vm-agent.md) |Umożliwia zobaczenie, które maszyny wirtualne wymagają agenta maszyny wirtualnej. Agent maszyny wirtualnej musi być zainstalowany na maszynach wirtualnych, aby zapewnić aprowizację skanowania w poszukiwaniu poprawek, skanowania linii bazowej i programów chroniących przed złośliwym oprogramowaniem. Agent maszyny wirtualnej jest instalowany domyślnie w przypadku maszyn wirtualnych wdrażanych z poziomu portalu Azure Marketplace. Informacje na temat instalowania agenta maszyny wirtualnej można znaleźć w artykule [Agent maszyny wirtualnej i rozszerzenia — część 2](http://azure.microsoft.com/blog/2014/04/15/vm-agent-and-extensions-part-2/). |
| [Zastosuj szyfrowanie dysków](security-center-apply-disk-encryption.md) |Zaleca szyfrowanie dysków maszyny wirtualnej przy użyciu usługi Azure Disk Encryption (maszyny wirtualne z systemami Windows i Linux). Szyfrowanie jest zalecane zarówno w przypadku woluminów z systemem operacyjnym, jak i z danymi maszyny wirtualnej. |


> [!NOTE]
> Aby dowiedzieć się więcej o zaleceniach, zobacz artykuł [Zarządzanie zaleceniami dotyczącymi zabezpieczeń](security-center-recommendations.md).
> 

## <a name="monitor-security-health"></a>Monitoruj kondycję zabezpieczeń
Po włączeniu [zasad zabezpieczeń](security-center-policies.md) dla zasobów subskrypcji Centrum zabezpieczeń będzie analizować zabezpieczenia zasobów, aby zidentyfikować potencjalne luki.  Stan zabezpieczeń zasobów oraz informacje o problemach można wyświetlić w bloku **Kondycja zabezpieczeń zasobów**. Jeśli klikniesz pozycję **Maszyny wirtualne** w ramach kafelka **Kondycja zabezpieczeń zasobów**, zostanie otwarty blok **Maszyny wirtualne** z zaleceniami dotyczącymi maszyn wirtualnych. 

![Kondycja zabezpieczeń](./media/security-center-virtual-machine/security-center-virtual-machine-fig2.png)

## <a name="manage-and-respond-to-security-alerts"></a>Zarządzanie alertami zabezpieczeń i reagowanie na nie
Usługa Security Center automatycznie gromadzi, analizuje i integruje dane dzienników z zasobów platformy Azure, sieci oraz połączonych rozwiązań partnerskich (takich jak rozwiązania zapory i ochrony punktów końcowych), aby wykrywać prawdziwe zagrożenia i redukować liczbę fałszywych alarmów. Dzięki korzystaniu z rozmaitych [funkcji wykrywania](security-center-detection-capabilities.md) usługa Security Center generuje alerty zabezpieczeń uporządkowane według priorytetu, aby pomóc w szybkim zbadaniu danego problemu i przedstawić zalecenia dotyczące działań zaradczych w przypadku ewentualnego ataku.

![Alerty zabezpieczeń](./media/security-center-virtual-machine/security-center-virtual-machine-fig3.png)

Wybierz alert zabezpieczeń, aby dowiedzieć się więcej o zdarzeniach, które go wywołały, oraz o czynnościach, które należy wykonać w celu wyeliminowania skutków ataku (jeśli ma to zastosowanie). Alerty zabezpieczeń są grupowane według [typu](security-center-alerts-type.md) i daty.

## <a name="monitor-security-health"></a>Monitoruj kondycję zabezpieczeń
Po włączeniu [zasad zabezpieczeń](security-center-policies.md) dla zasobów subskrypcji Centrum zabezpieczeń będzie analizować zabezpieczenia zasobów, aby zidentyfikować potencjalne luki.  Stan zabezpieczeń zasobów oraz informacje o problemach można wyświetlić w bloku **Kondycja zabezpieczeń zasobów**. Jeśli klikniesz pozycję **Maszyny wirtualne** w ramach kafelka **Kondycja zabezpieczeń zasobów**, zostanie otwarty blok **Maszyny wirtualne** z zaleceniami dotyczącymi maszyn wirtualnych. 

![Kondycja zabezpieczeń](./media/security-center-linux-virtual-machine/security-center-linux-virtual-machine-fig4.png)

Po kliknięciu tego zalecenia zobaczysz więcej szczegółów na temat określonych działań, które należy podjąć w celu rozwiązania tych problemów. Szczegóły pojawią się w dolnej części bloku, w obszarze **Zalecenia**. 

![Kondycja zabezpieczeń 2](./media/security-center-linux-virtual-machine/security-center-linux-virtual-machine-fig5.png)


## <a name="see-also"></a>Zobacz też
Aby dowiedzieć się więcej na temat Centrum zabezpieczeń, zobacz następujące artykuły:

* [Ustawianie zasad zabezpieczeń w usłudze Azure Security Center](security-center-policies.md) — informacje na temat konfigurowania zasad zabezpieczeń dla subskrypcji i grup zasobów na platformie Azure.
* [Reagowanie na alerty zabezpieczeń i zarządzanie nimi w usłudze Azure Security Center](security-center-managing-and-responding-alerts.md) — informacje na temat reagowania na alerty zabezpieczeń i zarządzania nimi.
* [Azure Security Center — często zadawane pytania](security-center-faq.md) — odpowiedzi na często zadawane pytania dotyczące korzystania z usługi.

