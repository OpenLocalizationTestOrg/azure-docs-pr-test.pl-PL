---
title: "aaaAzure Centrum zabezpieczeń i maszyn wirtualnych platformy Azure z systemem Linux | Dokumentacja firmy Microsoft"
description: "Ten dokument ułatwia toounderstand jak Centrum zabezpieczeń Azure można ochronić maszynach wirtualnych platformy Azure."
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
ms.openlocfilehash: d7aa9e54032272839dabfefa30c4c614d5e5610a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-security-center-and-azure-virtual-machines-with-linux"></a>Usługi Azure Security Center i Azure Virtual Machines z systemem Linux
[Centrum zabezpieczeń Azure](https://azure.microsoft.com/services/security-center/) pomaga zapobiec, wykrywania i reagowania toothreats. Zapewnia zintegrowane monitorowanie zabezpieczeń i zarządzanie zasadami subskrypcji platformy Azure, pomaga wykrywać zagrożenia, które w przeciwnym razie mogłyby pozostać niezauważone, a także współpracuje z szerokim ekosystemem rozwiązań z zakresu zabezpieczeń.

W tym artykule przedstawiono, jak usługa Security Center może pomóc w ochronie maszyn wirtualnych Azure Virtual Machines z systemem operacyjnym Linux.

## <a name="why-use-security-center"></a>Dlaczego warto korzystać z usługi Security Center?
Usługa Security Center pomaga chronić dane maszyny wirtualnej na platformie Azure, zapewniając wgląd w ustawienia zabezpieczeń na maszynie wirtualnej i monitorując zagrożenia. Usługa Security Center może monitorować maszyny wirtualne pod kątem następujących elementów: 

* Ustawienia zabezpieczeń systemu operacyjnego (OS) z hello zalecane reguły konfiguracji
* Informacje o brakujących zabezpieczeniach systemu i aktualizacjach krytycznych
* Zalecenia dotyczące ochrony punktów końcowych
* Weryfikowanie szyfrowania dysków
* Ataki oparte na sieci (opcja dostępna tylko w [wersji standardowej](https://azure.microsoft.com/en-us/pricing/details/security-center/))

Ponadto toohelping ochrony maszynach wirtualnych platformy Azure, Centrum zabezpieczeń zawiera także monitorowanie zabezpieczeń i zarządzania dla usługi w chmurze, usługi aplikacji, sieci wirtualnych i inne. 

> [!NOTE]
> Zobacz [tooAzure wprowadzenie Centrum zabezpieczeń](security-center-intro.md) toolearn więcej informacji na temat Centrum zabezpieczeń Azure.
> 
> 

## <a name="prerequisites"></a>Wymagania wstępne
tooget wprowadzenie do Centrum zabezpieczeń Azure, będzie konieczne tooknow i należy wziąć pod uwagę następujące hello:

* Musi mieć tooMicrosoft subskrypcji Azure. Aby uzyskać więcej informacji o warstwach Bezpłatna i Standardowa usługi Security Center, zobacz [Cennik usługi Security Center](https://azure.microsoft.com/pricing/details/security-center/).
* Planowanie wdrożenia z Centrum zabezpieczeń, zobacz [przewodnik dotyczący planowania i operacji Centrum zabezpieczeń Azure](security-center-planning-and-operations-guide.md) toolearn więcej informacji na temat zagadnienia dotyczące planowania i operacji.
* Aby uzyskać informacje dotyczące możliwości obsługi systemu operacyjnego, zobacz [Azure Security Center — często zadawane pytania](security-center-faq.md). 

## <a name="set-security-policy"></a>Ustawianie zasad zabezpieczeń
Toobe potrzeby zbierania danych włączone, dzięki czemu tego Centrum zabezpieczeń Azure umożliwia zebranie informacji hello potrzebne tooprovide zalecenia i alerty, które są generowane w oparciu hello zasady zabezpieczeń, które można skonfigurować. W poniższym rysunku hello, można stwierdzić, że **zbierania danych** wyłączono **na**.

Zasady zabezpieczeń określają hello zestaw mechanizmów kontrolnych, które są zalecane dla zasobów w ramach hello określonej subskrypcji lub grupy zasobów. Przed włączeniem zasady zabezpieczeń, musi mieć włączone zbieranie danych, Centrum zabezpieczeń zbiera dane z maszyn wirtualnych w kolejności tooassess stanu zabezpieczeń Podaj zalecenia dotyczące zabezpieczeń i alertów toothreats. W Centrum zabezpieczeń można zdefiniować zasady dla subskrypcji Azure lub grup zasobów zgodnie z związanych z zabezpieczeniami tooyour firmy i typem aplikacji hello lub czułości hello danych w każdej subskrypcji. 

![Zasady zabezpieczeń](./media/security-center-linux-virtual-machine/security-center-linux-virtual-machine-fig1.png)

> [!NOTE]
> więcej informacji na temat każdego toolearn **zasady zapobiegania** dostępne, zobacz [ustawiania zasad zabezpieczeń](security-center-policies.md) artykułu.
> 

## <a name="manage-security-recommendations"></a>Zarządzanie zaleceniami dotyczącymi zabezpieczeń
Centrum zabezpieczeń analizuje stan zabezpieczeń hello zasobów platformy Azure. Po znalezieniu potencjalnych luk w zabezpieczeniach usługa Security Center tworzy odpowiednie zalecenia. zalecenia Hello pomocne hello proces konfigurowania kontrolek hello potrzebne.

Po ustawieniu zasad zabezpieczeń, Centrum zabezpieczeń analizuje stan zabezpieczeń hello z zasobów tooidentify potencjalnych luk w zabezpieczeniach. zalecenia Hello są wyświetlane w formacie tabeli, w którym każdy wiersz zawiera jeden zaleceń. Witaj w poniższej tabeli podano przykłady zalecenia dotyczące maszyn wirtualnych platformy Azure, zainstalowano system operacyjny Linux oraz co każdej z nich zrobić w przypadku zastosowania. Po wybraniu zalecenia należy podać informacje, które wskazują, jak tooimplement hello zalecenia w Centrum zabezpieczeń.

| Zalecenie | Opis |
| --- | --- |
| [Włącz zbieranie danych dla subskrypcji](security-center-enable-data-collection.md) |Zaleca się włączenie funkcji zbierania danych w zasadach zabezpieczeń powitania dla każdej subskrypcji i wszystkich maszynach wirtualnych (VM) w subskrypcji. |
| [Koryguj luki w zabezpieczeniach systemu operacyjnego](security-center-remediate-os-vulnerabilities.md) |Zaleca wyrównania konfiguracje systemu operacyjnego z hello zalecane reguły konfiguracji, np. nie zezwalają na toobe hasła zapisane. |
| [Zastosuj aktualizacje systemu](security-center-apply-system-updates.md) |Zaleca się wdrożenie Brak zabezpieczenia systemu i tooVMs aktualizacje krytyczne. |
| [Uruchom ponownie po zaktualizowaniu systemu](security-center-apply-system-updates.md#reboot-after-system-updates) |Zaleca się ponowne uruchomienie procesu hello wirtualna toocomplete stosowanie aktualizacji systemu. |
| [Włącz agenta maszyny wirtualnej](security-center-enable-vm-agent.md) |Umożliwia toosee możesz maszyny wirtualne wymagające hello agenta maszyny Wirtualnej. Witaj agenta maszyny Wirtualnej musi być zainstalowany na maszynach wirtualnych w kolejności tooprovision poprawki skanowanie skanowanie linii bazowej i programy chroniące przed złośliwym kodem. Witaj agenta maszyny Wirtualnej jest instalowany domyślnie dla maszyn wirtualnych, które zostały wdrożone z hello Azure Marketplace. Artykuł Hello [agenta maszyny Wirtualnej i rozszerzenia — część 2](http://azure.microsoft.com/blog/2014/04/15/vm-agent-and-extensions-part-2/) zawiera informacje na temat sposobu tooinstall hello agenta maszyny Wirtualnej. |
| [Zastosuj szyfrowanie dysków](security-center-apply-disk-encryption.md) |Zaleca szyfrowanie dysków maszyny wirtualnej przy użyciu usługi Azure Disk Encryption (maszyny wirtualne z systemami Windows i Linux). Szyfrowanie jest zalecane dla hello systemu operacyjnego i woluminów danych na maszynie Wirtualnej. |


> [!NOTE]
> toolearn więcej informacji na temat zalecenia, zobacz [Zarządzanie zaleceniami dotyczącymi zabezpieczeń](security-center-recommendations.md) artykułu.
> 

## <a name="monitor-security-health"></a>Monitoruj kondycję zabezpieczeń
Po włączeniu [zasady zabezpieczeń](security-center-policies.md) dla zasobów subskrypcji Centrum zabezpieczeń będzie analizować zabezpieczenia hello z zasobów tooidentify potencjalnych luk w zabezpieczeniach.  Możesz wyświetlić stan zabezpieczeń zasobów oraz wszelkie problemy w hello hello **kondycja zabezpieczeń zasobów** bloku. Po kliknięciu **maszyn wirtualnych** w hello **zabezpieczeń zasobów** Kafelek kondycja, hello **maszyn wirtualnych** zostanie otwarty blok zawierający zalecenia dotyczące maszyn wirtualnych. 

![Kondycja zabezpieczeń](./media/security-center-virtual-machine/security-center-virtual-machine-fig2.png)

## <a name="manage-and-respond-toosecurity-alerts"></a>Zarządzanie i reagowanie na alerty toosecurity
Centrum zabezpieczeń automatycznie gromadzi, analizuje i integruje dane dzienników z zasobów platformy Azure, hello sieci i rozwiązań partnerskich połączonych (takie jak zapory i programu endpoint protection rozwiązania), toodetect prawdziwe zagrożenia i redukować liczbę fałszywych alarmów. Dzięki wykorzystaniu różnych agregacji [możliwości wykrywania](security-center-detection-capabilities.md), Centrum zabezpieczeń jest toogenerate można nadać priorytet alert zabezpieczeń toohelp szybkie Zbadaj hello problem i podano zalecenia dotyczące tooremediate możliwych ataków.

![Alerty zabezpieczeń](./media/security-center-virtual-machine/security-center-virtual-machine-fig3.png)

Wybierz toolearn alertu zabezpieczeń wymagają więcej informacji na temat hello zdarzenia, która wyzwoliła hello alert i co, jeśli kroki, możesz tooremediate tootake atak. Alerty zabezpieczeń są grupowane według [typu](security-center-alerts-type.md) i daty.

## <a name="monitor-security-health"></a>Monitoruj kondycję zabezpieczeń
Po włączeniu [zasady zabezpieczeń](security-center-policies.md) dla zasobów subskrypcji Centrum zabezpieczeń będzie analizować zabezpieczenia hello z zasobów tooidentify potencjalnych luk w zabezpieczeniach.  Możesz wyświetlić stan zabezpieczeń zasobów oraz wszelkie problemy w hello hello **kondycja zabezpieczeń zasobów** bloku. Po kliknięciu **maszyn wirtualnych** w hello **zabezpieczeń zasobów** Kafelek kondycja, hello **maszyn wirtualnych** zostanie otwarty blok zawierający zalecenia dotyczące maszyn wirtualnych. 

![Kondycja zabezpieczeń](./media/security-center-linux-virtual-machine/security-center-linux-virtual-machine-fig4.png)

Po kliknięciu tego zalecenia zostanie zobaczyć więcej szczegółów o hello określonych czynności, które mają zostać podjęte tooaddress tych problemów. Hello są wyświetlane szczegóły w hello dolnej części bloku hello, w obszarze **zalecenia**. 

![Kondycja zabezpieczeń 2](./media/security-center-linux-virtual-machine/security-center-linux-virtual-machine-fig5.png)


## <a name="see-also"></a>Zobacz też
toolearn więcej informacji na temat Centrum zabezpieczeń, zobacz następujące hello:

* [Ustawianie zasad zabezpieczeń w Centrum zabezpieczeń Azure](security-center-policies.md) — Dowiedz się, jak tooconfigure zasad zabezpieczeń dla subskrypcji platformy Azure i grup zasobów.
* [Zarządzanie i odpowiada toosecurity alertów w Centrum zabezpieczeń Azure](security-center-managing-and-responding-alerts.md) — Dowiedz się, jak alerty toosecurity toomanage i odpowiada.
* [Centrum zabezpieczeń Azure — często zadawane pytania](security-center-faq.md) — często zadawane pytania dotyczące korzystania z usługi hello Znajdź.

