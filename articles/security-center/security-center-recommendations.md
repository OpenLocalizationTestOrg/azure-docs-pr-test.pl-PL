---
title: "aaaManaging zalecenia dotyczące zabezpieczeń w Centrum zabezpieczeń Azure | Dokumentacja firmy Microsoft"
description: "Ten dokument przeprowadzi Cię przez jaki sposób zalecenia w Centrum zabezpieczeń Azure ułatwiają ochronę zasobów platformy Azure i są aktualizowane zgodnie z zasadami zabezpieczeń."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 86c50c9f-eb6b-4d97-acb3-6d599c06133e
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/19/2017
ms.author: terrylan
ms.openlocfilehash: f6bbe36a7a5636095b339b3e9765b87cc0ab669a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="managing-security-recommendations-in-azure-security-center"></a>Zarządzanie zaleceniami dotyczącymi zabezpieczeń w Centrum zabezpieczeń Azure
Ten dokument przeprowadzi Cię przez kolejne jak toouse zalecenia w Centrum zabezpieczeń Azure toohelp chronić zasobów platformy Azure.

> [!NOTE]
> Tym dokumencie przedstawiono hello usługi za pomocą przykładowego wdrożenia.  Ten dokument nie jest przewodnik krok po kroku.
>
>

## <a name="what-are-security-recommendations"></a>Jakie są zalecenia dotyczące zabezpieczeń?
Centrum zabezpieczeń okresowo analizuje stan zabezpieczeń hello zasobów platformy Azure. Po znalezieniu potencjalnych luk w zabezpieczeniach usługa Security Center tworzy odpowiednie zalecenia. zalecenia Hello pomocne hello proces konfigurowania kontrolek hello potrzebne.

## <a name="implementing-security-recommendations"></a>Wdrażanie zaleceń dotyczących zabezpieczeń
### <a name="set-recommendations"></a>Zestaw zaleceń
W [Ustawianie zasad zabezpieczeń w Centrum zabezpieczeń Azure](security-center-policies.md), Dowiedz się, jak:

* Konfigurowanie zasad zabezpieczeń.
* Włącz zbieranie danych.
* Wybierz toosee zaleceń, które jako część zasad zabezpieczeń.

Bieżący Centrum zalecenia dotyczące zasad wokół aktualizacji systemu, reguły linii bazowej, programy chroniące przed złośliwym kodem [sieciowej grupy zabezpieczeń](../virtual-network/virtual-networks-nsg.md) na podsieci i interfejsów sieciowych, inspekcja bazy danych SQL, SQL bazy danych przezroczystego szyfrowania danych i zapór aplikacji sieci web.  [Ustawianie zasad zabezpieczeń](security-center-policies.md) zawiera opis poszczególnych opcji zalecenia.

### <a name="monitor-recommendations"></a>Zalecenia dotyczące monitorowania
Po ustawieniu zasad zabezpieczeń, Centrum zabezpieczeń analizuje stan zabezpieczeń hello z zasobów tooidentify potencjalnych luk w zabezpieczeniach. Witaj **zalecenia** Kafelek na powitania **Centrum zabezpieczeń** bloku informuje o tym hello łączna liczba zalecenia określone przez Centrum zabezpieczeń.

![Zalecenia dotyczące kafelka][1]

Szczegóły hello toosee poszczególne zalecenia:

Wybierz hello **kafelka zalecenia** na powitania **Centrum zabezpieczeń** bloku. Witaj **zalecenia** zostanie otwarty blok.

zalecenia Hello są wyświetlane w formacie tabeli, w którym każdy wiersz zawiera jeden zaleceń. Witaj kolumny tabeli są:

* **Opis elementu**: wyjaśniono zalecenie hello i co należy zrobić tooaddress toobe go.
* **ZASÓB**: Wyświetla listę toowhich zasobów hello zastosowanie tego zalecenia.
* **Stan**: w tym artykule opisano hello bieżący stan zalecenia hello:
  * **Otwórz**: hello zalecenie nie zostały jeszcze zarejestrowane.
  * **Trwa**: hello zalecenie jest obecnie zastosowane toohello zasobów i jest wymagana żadna akcja.
  * **Rozwiązane**: hello zalecenie zostało już zakończone (w tym przypadku wiersza hello jest wyszarzona).
* **WAŻNOŚĆ**: Opisuje ważność określonego zalecenia hello:
  * **Wysoka**: Luka w zabezpieczeniach istnieje istotnego zasobu (np. aplikacji, maszyny Wirtualnej lub grupy zabezpieczeń sieci) i wymaga uwagi.
  * **Średnia liczba godzin**: istnieje luka w zabezpieczeniach i niekrytyczne lub dodatkowe kroki są wymagane tooeliminate lub toocomplete procesu.
  * **Niski**: istnieje luka w zabezpieczeniach, które powinny być kierowane, ale nie wymaga natychmiastowej uwagi. (Domyślnie zalecenia o niskiej ważności nie są prezentowane, ale można filtrować według zalecenia o niskiej ważności, jeśli chcesz, aby toosee je.)

Użyj hello poniższej tabeli jako toohelp odwołanie zrozumieć dostępne zalecenia hello i jak każdej z nich działa w przypadku zastosowania.

> [!NOTE]
> Można toounderstand hello [klasycznego i modeli wdrażania usługi Resource Manager](../azure-classic-rm.md) dla zasobów platformy Azure.
>
>

| Zalecenie | Opis |
| --- | --- |
| [Włącz zbieranie danych dla subskrypcji](security-center-enable-data-collection.md) |Zaleca się włączenie funkcji zbierania danych w zasadach zabezpieczeń powitania dla każdej subskrypcji i wszystkich maszynach wirtualnych (VM) w subskrypcji. |
| [Koryguj luki w zabezpieczeniach systemu operacyjnego](security-center-remediate-os-vulnerabilities.md) |Zaleca się, że wyrównania konfiguracje systemu operacyjnego z hello zalecane reguły konfiguracji, na przykład, nie zezwalaj na toobe hasła zapisane. |
| [Zastosuj aktualizacje systemu](security-center-apply-system-updates.md) |Zaleca się wdrożenie Brak zabezpieczenia systemu i tooVMs aktualizacje krytyczne. |
| [Zastosuj Just In Time kontroli dostępu do sieci](security-center-just-in-time.md) | Zaleca się zastosowanie tylko w dostęp maszyny Wirtualnej. Witaj tylko w funkcji czasu jest w wersji zapoznawczej i jest dostępny na powitania warstwy standardowa, Centrum zabezpieczeń. Zobacz [cennik](security-center-pricing.md) toolearn więcej informacji na temat Centrum zabezpieczeń firmy warstw cenowych. |
| [Uruchom ponownie po zaktualizowaniu systemu](security-center-apply-system-updates.md#reboot-after-system-updates) |Zaleca się ponowne uruchomienie procesu hello wirtualna toocomplete stosowanie aktualizacji systemu. |
| [Dodawanie zapory aplikacji sieci Web](security-center-add-web-application-firewall.md) |Zaleca się, że wdrażania zapory aplikacji sieci web (WAF) dla punktów końcowych sieci web. Wszelkie publicznego połączonej adresu IP (IP poziomie wystąpienia lub IP równoważenia obciążenia) zawierający sieciową grupę zabezpieczeń skojarzoną z portami Otwórz przychodzący sieci web (80,443) jest wyświetlane zalecenie zapory aplikacji sieci Web. </br>Centrum zabezpieczeń zaleca się, że przepisy toohelp zapory aplikacji sieci Web chronić przed atakami przeznaczonych dla aplikacji sieci web na maszynach wirtualnych i środowiska usługi aplikacji. Środowisko aplikacji (ASE) jest [Premium](https://azure.microsoft.com/pricing/details/app-service/) opcji plan usługi aplikacji Azure, która udostępnia środowisko pełni izolowanym środowisku, aby bezpiecznie pracować z aplikacjami usługi App service. toolearn więcej informacji na temat ASE, zobacz hello [dokumentację środowiska usługi aplikacji](../app-service/app-service-app-service-environments-readme.md).</br>Wiele aplikacji sieci web w Centrum zabezpieczeń można chronić przez dodanie tych aplikacji tooyour istniejące zapory aplikacji sieci Web wdrożenia. |
| [Finalizowanie ochrony aplikacji](security-center-add-web-application-firewall.md#finalize-application-protection) |toocomplete hello konfigurację zapory aplikacji sieci Web, ruch musi być przekierowany toohello zapory aplikacji sieci Web urządzenia. Po tego zalecenia kończy hello konfiguracji niezbędne zmiany. |
| [Dodawanie zapory nowej generacji](security-center-add-next-generation-firewall.md) |Zaleca się, że dodasz dalej zapory generacji (NGFW) z tooincrease partnera firmy Microsoft z ochrony zabezpieczeń. |
| [Kierowanie ruchu sieciowego tylko za pośrednictwem zapory następnej generacji](security-center-add-next-generation-firewall.md#route-traffic-through-ngfw-only) |Zaleca się, aby skonfigurować reguły grupy (NSG) zabezpieczeń sieciowych, który wymusza ruch przychodzący tooyour maszyny Wirtualnej za pośrednictwem sieci NGFW. |
| [Zainstaluj punkt końcowy](security-center-install-endpoint-protection.md) |Zaleca się, że alokowanie tooVMs programy chroniące przed złośliwym kodem (tylko maszyn wirtualnych systemu Windows). |
| [Rozwiąż alerty dotyczące kondycji punktu końcowego](security-center-resolve-endpoint-protection-health-alerts.md) |Zaleca rozwiązanie problemów dotyczących ochrony punktów końcowych. |
| [Włączenie grup zabezpieczeń sieci dla podsieci lub maszyny wirtualne](security-center-enable-network-security-groups.md) |Zaleca się włączenie grup NSG dla podsieci lub maszyn wirtualnych. |
| [Ogranicz dostęp za pośrednictwem internetowy punkt końcowy](security-center-restrict-access-through-internet-facing-endpoints.md) |Zaleca się, aby skonfigurować reguły ruchu przychodzącego dla grup NSG. |
| [Włączanie inspekcji i wykrywania zagrożeń na serwerach SQL](security-center-enable-auditing-on-sql-servers.md) |Zaleca się włączenie inspekcji i wykrywania zagrożeń dla serwerów SQL platformy Azure. (Tylko w przypadku usługi azure SQL. Nie obejmuje SQL uruchomionych na maszynach wirtualnych). |
| [Włączanie inspekcji i wykrywania zagrożeń w bazach danych SQL](security-center-enable-auditing-on-sql-databases.md) |Zaleca się włączenie inspekcji i wykrywania zagrożeń dla baz danych Azure SQL. (Tylko w przypadku usługi azure SQL. Nie obejmuje SQL uruchomionych na maszynach wirtualnych). |
| [Funkcja przezroczystego szyfrowania danych, Włącz bazy danych SQL](security-center-enable-transparent-data-encryption.md) |Zaleca się, aby włączyć szyfrowanie dla bazy danych SQL. (Tylko usługa azure SQL). |
| [Włącz agenta maszyny wirtualnej](security-center-enable-vm-agent.md) |Umożliwia toosee możesz maszyny wirtualne wymagające hello agenta maszyny Wirtualnej. Witaj agenta maszyny Wirtualnej musi być zainstalowany na skanowanie skanowanie linii bazowej i programy chroniące przed złośliwym kodem poprawki tooprovision maszyn wirtualnych. Witaj agenta maszyny Wirtualnej jest instalowany domyślnie dla maszyn wirtualnych, które zostały wdrożone z hello Azure Marketplace. Artykuł Hello [agenta maszyny Wirtualnej i rozszerzenia — część 2](http://azure.microsoft.com/blog/2014/04/15/vm-agent-and-extensions-part-2/) zawiera informacje na temat sposobu tooinstall hello agenta maszyny Wirtualnej. |
| [Zastosuj szyfrowanie dysków](security-center-apply-disk-encryption.md) |Zaleca szyfrowanie dysków maszyny wirtualnej przy użyciu usługi Azure Disk Encryption (maszyny wirtualne z systemami Windows i Linux). Szyfrowanie jest zalecane dla hello systemu operacyjnego i woluminów danych na maszynie Wirtualnej. |
| [Podawanie szczegółów dotyczących kontaktu ds. zabezpieczeń](security-center-provide-security-contact-details.md) |Zaleca, aby zapewnić ochronę informacji kontaktowych dla każdej subskrypcji. Informacje kontaktowe są wiadomości e-mail adres i numer telefonu. Witaj informacje są używane toocontact Jeśli nasz zespół zabezpieczeń stwierdzi, że zasoby są uszkodzone. |
| [Aktualizacja wersji systemu operacyjnego](security-center-update-os-version.md) |Zaleca się, zaktualizuj wersję systemu operacyjnego (OS) hello usługi w chmurze toohello najnowszej wersji dostępnej w do Twojej rodziny systemów operacyjnych.  toolearn więcej informacji na temat usługi w chmurze, zobacz hello [Omówienie usługi w chmurze](../cloud-services/cloud-services-choose-me.md). |
| [Funkcja oceny luk w zabezpieczeniach nie jest zainstalowana](security-center-vulnerability-assessment-recommendations.md) |Zaleca się zainstalowanie na maszynie wirtualnej rozwiązania do oceny luk w zabezpieczeniach. |
| [Korygowanie luk w zabezpieczeniach](security-center-vulnerability-assessment-recommendations.md#review-the-recommendation) |Umożliwia toosee systemu i aplikacji luk w zabezpieczeniach wykrywanych przez rozwiązanie do oceny luk w zabezpieczeniach hello zainstalowany na maszynie Wirtualnej. |
| [Włącz szyfrowanie dla konta magazynu Azure](security-center-enable-encryption-for-storage-account.md) | Zaleca się, Włącz szyfrowanie usługi Magazyn Azure dla przechowywanych danych. Szyfrowanie usługi Magazyn (SSE) działa hello dane są szyfrowane podczas ich zapisywania tooAzure magazynu i odszyfrowuje przed pobierania. SSE jest obecnie dostępny tylko dla hello usługi obiektów Blob platformy Azure i może służyć do blokowe i stronicowe obiekty BLOB i uzupełnialnych obiektów blob. toolearn więcej, zobacz [szyfrowanie usługi Magazyn danych magazynowanych](../storage/common/storage-service-encryption.md).</br>SSE jest obsługiwana tylko na kontach magazynu Menedżera zasobów. |

Można filtrować i odrzucić zalecenia.

1. Wybierz **filtru** na powitania **zalecenia** bloku. Witaj **filtru** zostanie otwarty blok i wybierz hello ważność i stan wartości mają toosee.

    ![Zalecenia dotyczące filtru][2]
2. Jeśli okaże się, że zalecenia nie ma zastosowania, możesz zignorować zalecenie hello i odfiltrować z widoku. Istnieją dwa sposoby toodismiss zalecenia. Jednym ze sposobów jest tooright kliknij element, a następnie wybierz **odrzucenia**. Witaj innych jest toohover nad elementem, kliknij przycisk hello trzech punktów, które są wyświetlane toohello prawo, a następnie wybierz **odrzucenia**. Odrzucony zalecenia można wyświetlić, klikając **filtru**, a następnie wybierając **odrzucone**.

    ![Odrzuć zalecenia][3]

### <a name="apply-recommendations"></a>Stosować zalecenia
Po przejrzeniu wszystkie zalecenia decyzji, które co należy najpierw zastosować. Firma Microsoft zaleca się używanie hello ważności jako hello tooevaluate główny parametr zaleceń, które powinny być stosowane najpierw.

W tabeli hello powyższe zalecenia, wybierz zalecenia i przeprowadzenie go jako przykład tooapply zalecenia.

## <a name="next-steps"></a>Następne kroki
W tym dokumencie było toosecurity wprowadzane zaleceń w Centrum zabezpieczeń. toolearn więcej informacji na temat Centrum zabezpieczeń, zobacz następujące hello:

* [Ustawianie zasad zabezpieczeń w Centrum zabezpieczeń Azure](security-center-policies.md) — Dowiedz się jak tooconfigure zasad zabezpieczeń dla subskrypcji platformy Azure i grup zasobów.
* [Monitorowanie kondycji zabezpieczeń w Centrum zabezpieczeń Azure](security-center-monitoring.md) — Dowiedz się, jak toomonitor hello kondycji zasobów platformy Azure.
* [Zarządzanie i odpowiada toosecurity alertów w Centrum zabezpieczeń Azure](security-center-managing-and-responding-alerts.md) — Dowiedz się jak alerty toosecurity toomanage i odpowiada.
* [Monitorowanie rozwiązań partnerskich w Centrum zabezpieczeń Azure](security-center-partner-solutions.md) — Dowiedz się, jak toomonitor hello stanu kondycji rozwiązań partnerskich.
* [Centrum zabezpieczeń Azure — często zadawane pytania](security-center-faq.md) — często zadawane pytania dotyczące korzystania z usługi hello Znajdź.
* [Blog Azure Security](http://blogs.msdn.com/b/azuresecurity/) — wpisy na blogu dotyczące zabezpieczeń i zgodności platformy Azure.

<!--Image references-->
[1]: ./media/security-center-recommendations/recommendations-tile.png
[2]: ./media/security-center-recommendations/filter-recommendations.png
[3]: ./media/security-center-recommendations/dismiss-recommendations.png
