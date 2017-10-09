---
title: "aaaUse zabezpieczeń tooenhance zaleceń Centrum zabezpieczeń Azure | Dokumentacja firmy Microsoft"
description: " Dowiedz się, jak toouse zasady zabezpieczeń i zalecenia w Centrum zabezpieczeń Azure toohelp ograniczenia atak na zabezpieczenia. "
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/08/2017
ms.author: terrylan
ms.openlocfilehash: bd314350a5abfceea3e171f2e1b55afe4549c1b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-security-center-recommendations-tooenhance-security"></a>Korzystanie z Centrum zabezpieczeń Azure zalecenia tooenhance zabezpieczeń
Można zmniejszyć szanse hello zdarzenia zabezpieczeń, konfigurując zasady zabezpieczeń, a następnie wdrażanie hello zaleceń dotyczących świadczona przez Centrum zabezpieczeń Azure. W tym artykule opisano, jak toouse zasady zabezpieczeń i zalecenia w Centrum zabezpieczeń toohelp ograniczenia atak na zabezpieczenia.

> [!NOTE]
> W tym artykule, bazując na powitania ról i założenia hello Centrum zabezpieczeń [przewodnik dotyczący planowania i operacje](security-center-planning-and-operations-guide.md). Przewodnik planowania hello tooreview dobrym rozwiązaniem jest przed kontynuowaniem.
>
>

## <a name="managing-security-recommendations"></a>Zarządzanie zaleceniami dotyczącymi zabezpieczeń
Zasady zabezpieczeń definiuje zestaw hello formantów, które są zalecane dla zasobów w ramach hello określonej subskrypcji lub grupy zasobów. W Centrum zabezpieczeń można zdefiniować zasady zgodnie z wymaganiami zabezpieczeń firmy tooyour. toolearn więcej, zobacz [ustawić zasady zabezpieczeń w Centrum zabezpieczeń](security-center-policies.md).

Zasady zabezpieczeń dla grupy zasobów są dziedziczone z poziomu subskrypcji hello.

![Dziedziczenie zasad zabezpieczeń][1]

Jeśli potrzebujesz niestandardowych zasad w określonych grupach zasobów, można wyłączyć dziedziczenia w grupie zasobów hello. toodisable, ustaw tooUnique dziedziczenia w bloku zasady zabezpieczeń hello i dostosować hello formantów, które Centrum zabezpieczeń zawiera zalecenia dotyczące.

Na przykład jeśli masz obciążeń, które nie wymagają zasad SQL bazy danych przezroczysty danych szyfrowania (funkcji TDE) hello wyłączyć hello zasad na poziomie subskrypcji hello i włącz je tylko w grupach zasobów hello, gdy wymagane jest funkcji SQL TDE.

> [!NOTE]
> W przypadku konfliktu między zasadami na poziomie subskrypcji a zasadami poziomu grupy zasobów, pierwszeństwo ma poziom zasad grupy zasobów hello.
>
>

Centrum zabezpieczeń analizuje stan zabezpieczeń hello zasobów platformy Azure. Gdy Centrum zabezpieczeń identyfikuje potencjalnych luk w zabezpieczeniach, tworzy oparte na formanty hello wartość w zasadach zabezpieczeń hello zalecenia. zalecenia Hello pomocne hello proces konfigurowania opcji zabezpieczeń hello potrzebne.

Bieżące zasady zalecenia w Centrum zabezpieczeń fokus na aktualizacje systemu, konfiguracja systemu operacyjnego, sieciowej grupy zabezpieczeń w podsieci i maszyn wirtualnych (VM), SQL Database Auditing funkcji TDE bazy danych SQL, i zapory aplikacji sieci web. Najbardziej aktualne pokrycia hello zaleceń Centrum zabezpieczeń, zobacz [Zarządzanie zaleceniami dotyczącymi zabezpieczeń w Centrum zabezpieczeń](security-center-recommendations.md).

## <a name="scenario"></a>Scenariusz
W tym scenariuszu pokazano, jak toohelp Centrum zabezpieczeń toouse zmniejszyć szanse hello zdarzenia zabezpieczeń przez monitorowanie zaleceń Centrum zabezpieczeń i podejmowania działań. Witaj scenariusz używa hello fikcyjnej firmy Contoso, i ról przedstawionych w hello Centrum zabezpieczeń [przewodnik dotyczący planowania i operacje](security-center-planning-and-operations-guide.md#security-roles-and-access-controls). role Hello reprezentują osób oraz zespołów mogą używających zadań związanych z zabezpieczeniami w Centrum zabezpieczeń tooperform inny. role Hello są:

![Scenariusz ról][2]

Contoso niedawno migracji niektórych ich tooAzure zasobów lokalnych. Contoso chce tooimplement i zabezpieczenia udostępniane przez zmniejszyć ich luki w zabezpieczeniach tooa atak na zabezpieczenia ich zasobów w chmurze hello Obsługa.

## <a name="recommended-solution"></a>Zalecane rozwiązanie
Rozwiązanie jest toouse tooprevent Centrum zabezpieczeń i Wykrywanie luk w zabezpieczeniach. Firma Contoso ma dostęp do Centrum tooSecurity za pośrednictwem ich subskrypcji platformy Azure. Witaj [warstwę bezpłatna](security-center-pricing.md) z Centrum zabezpieczeń jest automatycznie włączone na wszystkich subskrypcji platformy Azure i zbieranie danych jest włączone na wszystkich maszynach wirtualnych w swoich subskrypcji.

Konfiguruje Dominik działu zabezpieczeń IT firmy Contoso, **zasady zabezpieczeń** przy użyciu Centrum zabezpieczeń. Centrum zabezpieczeń analizuje stan zabezpieczeń zasobów platformy Azure firmy Contoso hello. Jeśli Centrum zabezpieczeń zostanie zidentyfikowana potencjalnych luk w zabezpieczeniach, tworzy **zalecenia** oparte na formanty hello wartość w zasadach zabezpieczeń hello.

Jan, właściciel obciążenia chmury, jest odpowiedzialny za wykonanie i utrzymywanie ochrony zgodnie z zasadami zabezpieczeń firmy Contoso. Jan można monitorować zalecenia hello utworzone przez Centrum zabezpieczeń tooapply ochrony. zalecenia Hello przeprowadzają Jeff hello proces konfigurowania opcji zabezpieczeń hello potrzebne.

W kolejności dla Jeff tooimplement i obsługa ochrony i eliminowania luk w zabezpieczeniach, musi on:

- Zalecenia dotyczące zabezpieczeń Monitor świadczona przez Centrum zabezpieczeń
- Oceń zalecenia dotyczące zabezpieczeń i zdecyduj, czy powinien on zastosować lub odrzucać
- Zastosuj zalecenia dotyczące zabezpieczeń

Teraz wykonaj jego Jeff toosee kroki jak używa tooguide zaleceń Centrum zabezpieczeń mu hello proces konfigurowania luk w zabezpieczeniach tooeliminate kontrolki.

## <a name="how-tooimplement-this-solution"></a>Jak tooimplement tego rozwiązania
Jan zaloguje się za[portalu Azure](https://azure.microsoft.com/features/azure-portal/) i otwiera hello konsoli Centrum zabezpieczeń. W ramach codziennej monitorowania działań sprawdza on toosee, czy istnieją zalecenia dotyczące zabezpieczeń, wykonując następujące kroki hello:

1. Jan wybiera hello **zalecenia** hello tooopen kafelka **zalecenia** bloku.
   ![Wybierz hello zalecenia kafelka][3]
2. Jan przegląda hello lista zaleceń. Zauważa podania w Centrum zabezpieczeń hello lista zaleceń według priorytetu z najwyższym priorytetem toolowest priorytet. Ocenił tooaddress zalecenie o wysokim priorytecie, na liście hello. Wybiera **Zainstaluj program Endpoint Protection** na powitania **zalecenia** bloku.
3. Witaj **Zainstaluj program Endpoint Protection** zostanie otwarty blok zawierający listę maszyn wirtualnych bez ochrony przed złośliwym kodem jest włączona. Jan przegląda hello listy maszyn wirtualnych, wybiera wszystkich maszyn wirtualnych i następnie wybiera **zainstalować na maszynach wirtualnych 3**.
   ![Instalowanie ochrony punktu końcowego][4]
4. Witaj **wybierz program Endpoint Protection** udostępnienie Jeff zostanie otwarty blok z dwóch rozwiązań do ochrony przed złośliwym oprogramowaniem. Jan wybiera hello **Microsoft Antimalware** rozwiązania.
5. Dodatkowe informacje na temat rozwiązania chroniące przed złośliwym kodem hello jest wyświetlany. Jan wybiera **Utwórz**.
   ![Ochrony przed złośliwym oprogramowaniem firmy Microsoft][5]
6. Jan wprowadza hello wymagane ustawienia konfiguracji na powitania **zainstalować** bloku i wybiera **OK**.

[Microsoft Antimalware](../security/azure-security-antimalware.md) jest teraz aktywny na powitania wybrane maszyny wirtualne.

Jan kontynuuje toomove za pośrednictwem hello o wysokim priorytecie i zalecenia średni priorytet, podejmowanie decyzji o implementacji. Jan odwołuje się do hello [Zarządzanie zaleceniami dotyczącymi zabezpieczeń](security-center-recommendations.md) artykuł toounderstand hello zalecenia i co każdego z nich pojawia się on ma zastosowanie.

Jan uzyskuje informacje o który [Microsoft Security odpowiedzi Center (MSRC)](../security/azure-security-response-center.md) wykonuje monitorowanie zabezpieczeń wybierz hello sieć platformy Azure i infrastruktury i odbiera zagrożeń analizy i nadużycia utrudnień od osób trzecich. Jeśli Jeff zawiera szczegóły dotyczące kontaktu zabezpieczeń dla subskrypcji platformy Azure firmy Contoso, kontakty Microsoft firmy Contoso, jeśli hello MSRC umożliwia odnalezienie danych klienta firmy Contoso uzyskaniu dostępu przez stronę bezprawnego lub nieautoryzowane. Teraz należy wykonać Jeff dotyczy on hello **podać szczegóły dotyczące kontaktu zabezpieczeń** zalecenie (zalecenie o ważności nośnika hello liście powyższe zalecenia).

1. Jan wybiera **podać szczegóły dotyczące kontaktu zabezpieczeń** na powitania **zalecenia** bloku, które umożliwia otwarcie hello **podać szczegóły dotyczące kontaktu zabezpieczeń** bloku.
2. Jan wybiera hello informacje kontaktowe tooprovide subskrypcji platformy Azure na. Drugi **podać szczegóły dotyczące kontaktu zabezpieczeń** zostanie otwarty blok.
   ![Szczegóły dotyczące kontaktu zabezpieczeń][6]
3. Na powitania drugi **podać szczegóły dotyczące kontaktu zabezpieczeń** wprowadza Jeff bloku:

  - adresy e-mail kontaktu zabezpieczeń Hello rozdzielonych przecinkami (Brak nie jest Ogranicz liczbę toohello adresów e-mail, które może wprowadzić)
  - numer telefonu skontaktuj się z jednego zabezpieczeń

4. Jan włącza również opcję hello **Wyślij do mnie wiadomość e-mail o alertach** tooreceive powiadomienia dotyczące alerty o wysokim znaczeniu.
5. Jan wybiera **OK** tooapply hello zabezpieczeń subskrypcji tooContoso informacji, skontaktuj się z pomocą.

Na koniec Jan przegląda hello zalecenie o niskim priorytecie **luk w zabezpieczeniach skorygować OS** i określa, że nie ma zastosowania tego zalecenia. Maciej chce toodismiss hello zalecenia. Jan wybiera hello trzech punktów, które pojawiają się toohello prawo, a następnie wybiera **odrzucenia**.
   ![Odrzuć zalecenia][7]

## <a name="conclusion"></a>Podsumowanie
Monitorowanie zalecenia w Centrum zabezpieczeń może pomóc wyeliminować luk w zabezpieczeniach, zanim wystąpi atak. Zdarzenia zabezpieczeń można zapobiec przez wykonanie i utrzymywanie ochrony przy użyciu zasad zabezpieczeń w Centrum zabezpieczeń.

<!--Image references-->
[1]: ./media/security-center-using-recommendations/security-center-policy-inheritance.png
[2]: ./media/security-center-using-recommendations/scenario-roles.png
[3]: ./media/security-center-using-recommendations/select-recommendations-tile.png
[4]: ./media/security-center-using-recommendations/install-endpoint-protection.png
[5]:./media/security-center-using-recommendations/microsoft-antimalware.png
[6]: ./media/security-center-using-recommendations/provide-security-contact-details.png
[7]: ./media/security-center-using-recommendations/dismiss-recommendation.png
