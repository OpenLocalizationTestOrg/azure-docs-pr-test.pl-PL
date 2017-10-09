---
title: "tooAzure aaaIntroduction Centrum zabezpieczeń | Dokumentacja firmy Microsoft"
description: "Uzyskaj informacje na temat Centrum zabezpieczeń Azure, jego kluczowych możliwości i sposobu działania."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 45b9756b-6449-49ec-950b-5ed1e7c56daa
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: terrylan
ms.openlocfilehash: 287dbaaa7e2004c522f103595bc316261daf05b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooazure-security-center"></a>Wprowadzenie tooAzure Centrum zabezpieczeń
Uzyskaj informacje na temat Centrum zabezpieczeń Azure, jego kluczowych możliwości i sposobu działania.

> [!NOTE]
> Począwszy od początku czerwca 2017, Centrum zabezpieczeń użyj toocollect Microsoft Monitoring Agent hello i przechowywania danych. Zobacz [migracji Platform Centrum zabezpieczeń Azure](security-center-platform-migration.md) toolearn więcej. Witaj informacje w tym artykule reprezentuje funkcji Centrum zabezpieczeń po toohello przejścia programu Microsoft Monitoring Agent.
>
>

## <a name="what-is-azure-security-center"></a>Co to jest Centrum zabezpieczeń Azure?
 Centrum zabezpieczeń ułatwia zapobieganie, wykrywania i odpowie toothreats lepszy wgląd w i kontroli nad hello zabezpieczeń zasobów platformy Azure. Zapewnia zintegrowane monitorowanie zabezpieczeń i zarządzanie zasadami subskrypcji platformy Azure, pomaga wykrywać zagrożenia, które w przeciwnym razie mogłyby pozostać niezauważone, a także współpracuje z szerokim ekosystemem rozwiązań z zakresu zabezpieczeń.

## <a name="key-capabilities"></a>Najważniejsze możliwości
 Centrum zabezpieczeń zapewnia łatwe w użyciu i skuteczne zapobieganie, wykrywanie i odpowiedzi możliwości, które są wbudowane w tooAzure. Do najważniejszych możliwości należą:

| Etap | Możliwości |
| --- | --- |
| Zapobieganie |Monitory hello stan zabezpieczeń zasobów platformy Azure |
| Zapobieganie | Definiuje zasady dla subskrypcji platformy Azure na podstawie wymagań zabezpieczeń w firmie, hello typów aplikacji przy użyciu, a hello wrażliwość danych |
| Zapobieganie | Używa oparte na zasadach zabezpieczeń zalecenia tooguide właścicieli hello proces wdrażania potrzebnych elementów sterujących |
| Zapobieganie | Szybko wdraża usługi oraz urządzenia zabezpieczające firmy Microsoft i partnerów |
| Wykrywanie |Automatycznie zbiera i analizuje dane dotyczące zabezpieczeń z zasobów platformy Azure, hello sieci i rozwiązań partnerskich, takich jak programy chroniące przed złośliwym kodem i zapór |
| Wykrywanie | Zagrożenia używa globalnej analizy z Microsoft produktów i usług, hello Microsoft cyfrowego ds. przestępstw jednostki (DCU), hello Microsoft Security odpowiedzi Center (MSRC) i zewnętrznych źródeł danych |
| Wykrywanie | Stosuje zaawansowane metody analizy, w tym uczenie maszynowe i analizę behawioralną |
| Reakcja |Szereguje incydenty/alerty zabezpieczeń według priorytetów |
| Reakcja | Oferuje wgląd w źródło hello atak powitania i wpływ na zasoby |
| Reakcja | Sugeruje metody toostop hello bieżącego ataku i pomaga w zapobieganiu atakom w przyszłości |

## <a name="introductory-walkthrough"></a>Przewodnik wprowadzający

> [!NOTE]
> Tym dokumencie przedstawiono hello usługi za pomocą przykładowego wdrożenia. Ten dokument nie jest przewodnik krok po kroku.
>
>

 Dostęp do Centrum zabezpieczeń hello [portalu Azure](https://azure.microsoft.com/features/azure-portal/). [Zaloguj się w portalu toohello](https://portal.azure.com). W menu głównym portalu hello, przewiń toohello **Centrum zabezpieczeń** opcji lub wybierz hello **Centrum zabezpieczeń** kafelka, przypięty wcześniej toohello pulpitu nawigacyjnego portalu.

![Kafelek Zabezpieczenia w witrynie Azure Portal][1]

W Centrum zabezpieczeń można ustawiać zasady zabezpieczeń, monitorować konfigurację zabezpieczeń i wyświetlać alerty zabezpieczeń.

### <a name="security-policies"></a>Zasady zabezpieczeń
Zasady można definiować dla Twojej subskrypcji platformy Azure, zgodnie z wymaganiami zabezpieczeń firmy tooyour. Można również dostosować je toohello typów aplikacji, którego używasz lub toohello wrażliwości danych hello w każdej subskrypcji. Na przykład zasoby używane dla rozwoju lub testowania mogą mieć inne wymagania dotyczące zabezpieczeń niż te, które są wykorzystywane przez aplikacje produkcyjne. Podobnie aplikacje z danymi podlegającymi ochronie, jak dane osobowe, mogą wymagać wyższego poziomu zabezpieczeń.

> [!NOTE]
> toomodify zasady zabezpieczeń, musisz być właścicielem lub współautorem subskrypcji administratora zabezpieczeń lub hello. toolearn więcej informacji na temat ról i akcji dozwolonych w Centrum zabezpieczeń, zobacz [uprawnienia w Centrum zabezpieczeń Azure](security-center-permissions.md).
>
>

Na powitania **Centrum zabezpieczeń** bloku, wybierz hello **zasad** kafelku listę Twojej subskrypcji i grup zasobów.   

![Blok Centrum zabezpieczeń][2]

Na powitania **zasady zabezpieczeń** bloku, wybierz szczegóły zasad hello tooview subskrypcji.

**Zbieranie danych** umożliwia zbieranie danych dla zasad zabezpieczeń. Włączenie umożliwia:

* Codzienne skanowanie wszystkich obsługiwanych maszyn wirtualnych (VM) monitorowania zabezpieczeń i zalecenia.
* Zbieranie zdarzeń zabezpieczeń w celu analizy i wykrywania zagrożeń.

> [!NOTE]
> Zbieranie danych jest skonfigurowana na poziomie subskrypcji hello.
>
>

Wybierz **zasady zapobiegania** tooopen hello **zasady zapobiegania** bloku. **Pokaż zalecenia dotyczące** pozwala wybrać hello sterujących zabezpieczeń, które chcesz toomonitor i hello zaleceń, które mają toosee zgodnie z wymaganiami zabezpieczeń hello hello zasobów w ramach subskrypcji hello.

### <a name="security-recommendations"></a>Zalecenia dotyczące zabezpieczeń
 Centrum zabezpieczeń analizuje stan zabezpieczeń hello z zasobów platformy Azure tooidentify potencjalnych luk w zabezpieczeniach. Lista zaleceń prowadzi użytkownika przez proces konfigurowania wymaganych elementów sterujących hello. Przykłady:

* Inicjowanie obsługi ochrony przed złośliwym kodem toohelp identyfikacji i usuwania złośliwego oprogramowania
* Konfigurowanie sieci zabezpieczeń grup i reguł toocontrol ruchu tooVMs
* Inicjowanie obsługi administracyjnej zapór aplikacji sieci web toohelp chronić przed atakami, które odnoszą się do aplikacji sieci web
* Wdrażanie brakujących aktualizacji systemu
* Modyfikowanie konfiguracji systemu operacyjnego, które nie odpowiadają hello zalecanych planów bazowych

Kliknij przycisk hello **zalecenia** kafelku lista zaleceń. Kliknij każdy zalecenie tooview dodatkowe informacje lub tootake akcji tooresolve hello problem.

![Zalecenia dotyczące zabezpieczeń w Centrum zabezpieczeń Azure][5]

### <a name="security-state-of-azure-resources"></a>Stan zabezpieczeń zasobów platformy Azure
Witaj **zapobiegania** sekcji hello pulpitu nawigacyjnego przedstawia hello ogólny stan zabezpieczeń środowiska hello według typów zasobów, w tym maszyn wirtualnych, aplikacji sieci web i innych zasobów.   

Wybierz typ zasobu w obszarze **zapobiegania** tooview więcej informacji, w tym listę wszelkich potencjalnych luk w zabezpieczeniach, które zostały zidentyfikowane. (**Obliczeniowe** wybrano w poniższym przykładzie hello.)

![Kafelek Kondycja zasobów][6]

### <a name="security-alerts"></a>Alerty zabezpieczeń
 Centrum zabezpieczeń automatycznie gromadzi, analizuje i integruje dane dzienników z zasobów platformy Azure, hello sieci i rozwiązań partnerskich, takich jak programy ochrony przed złośliwym oprogramowaniem i zapory. Po wykryciu zagrożenia tworzony jest alert zabezpieczeń. Przykłady obejmują wykrywanie:

* Złamany maszyny wirtualnej komunikowania się ze znanymi złośliwymi adresami IP
* Zaawansowanego złośliwego oprogramowania wykrytego za pomocą funkcji raportowania błędów systemu Windows
* Ataków siłowych wobec maszyn wirtualnych
* Alerty zabezpieczeń ze zintegrowanych programów chroniących przed złośliwym oprogramowaniem i zapór

Kliknięcie przycisku hello **alerty zabezpieczeń** kafelka wyświetlenie listy alertów uszeregowanych według priorytetów.

![Alerty zabezpieczeń][7]

Wybieranie alertu zawiera więcej informacji na temat atak powitania i sugestie dotyczące tooremediate go.

![Szczegóły alertu zabezpieczeń][8]

### <a name="partner-solutions"></a>Rozwiązania partnerskie
Witaj **rozwiązania partnerskie** kafelka umożliwia monitorowanie stanu zabezpieczeń hello w skrócie rozwiązań partnerskich zintegrowanych z subskrypcją platformy Azure. Centrum zabezpieczeń wyświetlane są alerty pochodzące z rozwiązań hello.

Wybierz hello **rozwiązania partnerskie** kafelka. Zostanie otwarty blok zawierający listę wszystkich połączonych rozwiązań partnerskich.

![Rozwiązania partnerskie][9]

## <a name="get-started"></a>Rozpoczęcie pracy
wprowadzenie do Centrum zabezpieczeń tooget, należy tooMicrosoft subskrypcji Azure. Centrum zabezpieczeń jest włączone w ramach subskrypcji platformy Azure. Jeśli nie masz subskrypcji, możesz zarejestrować się, aby uzyskać dostęp do [bezpłatnej wersji próbnej](https://azure.microsoft.com/pricing/free-trial/).

 Dostęp do Centrum zabezpieczeń hello [portalu Azure](https://azure.microsoft.com/features/azure-portal/). Zobacz hello [dokumentację portalu](https://azure.microsoft.com/documentation/services/azure-portal/) toolearn więcej.

[Wprowadzenie do Centrum zabezpieczeń Azure](security-center-get-started.md) szybko przeprowadzi Cię przez składniki monitorowania zabezpieczeń i zarządzania zasadami hello Centrum zabezpieczeń.

## <a name="next-steps"></a>Następne kroki
W tym dokumencie zostały wprowadzone Center tooSecurity, jego kluczowych możliwości i sposobu uruchamiania tooget. toolearn więcej, zobacz następujące zasoby hello:

* [Ustawianie zasad zabezpieczeń w Centrum zabezpieczeń Azure](security-center-policies.md) — Dowiedz się jak tooconfigure zasad zabezpieczeń dla subskrypcji platformy Azure i grup zasobów.
* [Zarządzanie zaleceniami dotyczącymi zabezpieczeń w Centrum zabezpieczeń Azure](security-center-recommendations.md) — Dowiedz się, w jaki sposób zalecenia ułatwiają ochronę zasobów platformy Azure.
* [Monitorowanie kondycji zabezpieczeń w Centrum zabezpieczeń Azure](security-center-monitoring.md) — Dowiedz się, jak toomonitor hello kondycji zasobów platformy Azure.
* [Zarządzanie i odpowiada toosecurity alertów w Centrum zabezpieczeń Azure](security-center-managing-and-responding-alerts.md) — Dowiedz się jak alerty toosecurity toomanage i odpowiada.
* [Monitorowanie rozwiązań partnerskich w Centrum zabezpieczeń Azure](security-center-partner-solutions.md) — Dowiedz się, jak toomonitor hello stanu kondycji rozwiązań partnerskich.
- [Bezpieczeństwo danych w Centrum zabezpieczeń Azure](security-center-data-security.md) — Dowiedz się, jak dane są zarządzane i w Centrum zabezpieczeń.
* [Centrum zabezpieczeń Azure — często zadawane pytania](security-center-faq.md) — często zadawane pytania dotyczące korzystania z usługi hello Znajdź.
* [Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) — hello najnowsze zabezpieczeń platformy Azure i informacji.

<!--Image references-->
[1]: ./media/security-center-intro/security-tile.png
[2]: ./media/security-center-intro/security-center.png
[3]: ./media/security-center-intro/security-policy.png
[4]: ./media/security-center-intro/security-policy-blade.png
[5]: ./media/security-center-intro/recommendations.png
[6]: ./media/security-center-intro/resources-health.png
[7]: ./media/security-center-intro/security-alert.png
[8]: ./media/security-center-intro/security-alert-detail.png
[9]: ./media/security-center-intro/partner-solutions.png
