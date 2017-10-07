---
title: "aaaSecurity monitorowania w Centrum zabezpieczeń Azure | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano tooget wprowadzenie do funkcji monitorowania w Centrum zabezpieczeń Azure."
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: 3bd5b122-1695-495f-ad9a-7c2a4cd1c808
ms.service: security-center
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/09/2017
ms.author: yurid
ms.openlocfilehash: 43c2a8864d5fe27ba44b0d7bc979db970305ec17
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="security-health-monitoring-in-azure-security-center"></a>Monitorowanie kondycji zabezpieczeń w Centrum zabezpieczeń Azure
W tym artykule opisano, jak używać hello możliwości monitorowania w Centrum zabezpieczeń Azure toomonitor zgodności z zasadami.

## <a name="what-is-security-health-monitoring"></a>Czym jest monitorowanie kondycji zabezpieczeń?
Często postrzegane monitorowanie jako obserwowanie i Oczekiwanie na toooccur zdarzeń, aby firma Microsoft zareagować toohello sytuacji. Monitorowanie zabezpieczeń polega toohaving aktywnej strategii przeprowadzania inspekcji używanych systemach tooidentify zasoby, które nie spełniają standardów organizacji lub najlepszych rozwiązań.

## <a name="monitoring-security-health"></a>Monitorowanie kondycji zabezpieczeń
Po włączeniu [zasady zabezpieczeń](security-center-policies.md) dla zasobów subskrypcji Centrum zabezpieczeń analizuje zabezpieczenia hello z zasobów tooidentify potencjalnych luk w zabezpieczeniach. Informacje o konfiguracji sieci są dostępne natychmiast. Może potrwać godzinę lub więcej informacji o konfiguracji maszyny wirtualnej, takie jak zabezpieczenia aktualizacji stanu i konfiguracji systemu operacyjnego, toobecome dostępne. Można wyświetlić hello stan zabezpieczeń zasobów oraz wszelkie problemy w hello **zapobiegania** sekcji. Można także wyświetlić listę tych problemów na powitania **zalecenia** kafelka.

Aby uzyskać więcej informacji o tym, jak tooapply zalecenia, przeczytaj [wdrażanie zaleceń dotyczących zabezpieczeń w Centrum zabezpieczeń Azure](security-center-recommendations.md).

W obszarze hello **zapobiegania** sekcji, można monitorować stan zabezpieczeń hello zasobów. Poniższy przykład hello, zawiera kafelku każdego zasobu (obliczeniowych, sieci, magazynu i danych i aplikacji) mający hello łączna liczba problemów, które zostały zidentyfikowane.

![Kafelek Kondycja zabezpieczeń zasobów](./media/security-center-monitoring/security-center-monitoring-fig1-newUI-2017.png)


### <a name="monitor-compute"></a>Monitorowanie mocy obliczeniowej
Po kliknięciu **obliczeniowe** kafelku hello **obliczeniowe** blok, którego kliknięcie spowoduje otwarcie zawiera trzy karty:

- **Omówienie**: zalecenia dotyczące monitorowania i maszyny wirtualnej.
- **Maszyny wirtualne**: lista wszystkich maszyn wirtualnych i bieżącego stanu zabezpieczeń.
- **Usługi w chmurze**: lista wszystkich ról sieci Web i procesów roboczych monitorowanych przez usługę Security Center.

![Brak aktualizacji systemu na maszynie wirtualnej](./media/security-center-monitoring/security-center-monitoring-fig1-new002-2017.png)

Na każdej karcie może mieć wiele sekcji, a w każdej sekcji można wybrać poszczególne opcje toosee więcej szczegółów na temat hello zalecane kroki tooaddress tego konkretnego problemu. 

#### <a name="monitoring-recommendations"></a>Zalecenia dotyczące monitorowania
W tej sekcji przedstawiono hello łączna liczba maszyn wirtualnych, których zainicjowano obsługę zbierania danych i ich stany bieżącego. Po wszystkie maszyny wirtualne mają zainicjowaniu obsługi zbierania danych, zostaną one zasad zabezpieczeń Centrum zabezpieczeń tooreceive gotowe. Po kliknięciu tego wpisu hello **brakuje agenta maszyny Wirtualnej lub nie odpowiada** zostanie otwarty blok. 

![Brak aktualizacji systemu na maszynie wirtualnej](./media/security-center-monitoring/security-center-monitoring-fig1-new003-2017.png)


#### <a name="virtual-machine-recommendations"></a>Zalecenia dotyczące maszyny wirtualnej
Ta sekcja zawiera zestaw [zaleceń dotyczących każdej maszyny wirtualnej](security-center-virtual-machine-recommendations.md) monitorowanej przez usługę Azure Security Center. Witaj pierwsza kolumna zawiera zalecenia hello. druga kolumna Hello pokazuje hello łączna liczba maszyn wirtualnych, których dotyczy tego zalecenia. Hello trzecia kolumna zawiera hello ważność problemu hello, jak pokazano na powitania po zrzut ekranu.

![Zalecenia dotyczące maszyny wirtualnej](./media/security-center-monitoring/security-center-monitoring-fig1-new004-2017.png)

> [!NOTE]
> Tylko maszyny wirtualne, które mają co najmniej jeden publiczny punkt końcowy są wyświetlane w hello **kondycji sieci** bloku w hello **topologii sieci** listy.
>
>

Każdy zalecenie obejmuje zestaw akcji możliwych do wykonania po jego kliknięciu. Na przykład, jeśli klikniesz przycisk **Brak aktualizacji systemu**, hello **Brak aktualizacji systemu** zostanie otwarty blok. Wyświetla listę hello maszyny wirtualne, których brakuje poprawek i hello ważności brakujących aktualizacji hello, jak pokazano poniżej hello zrzut ekranu.

![Brak aktualizacji systemu na maszynach wirtualnych](./media/security-center-monitoring/security-center-monitoring-fig5-ga.png)

Witaj **Brak aktualizacji systemu** bloku jest wyświetlana tabela hello następujących informacji:

* **Maszyna wirtualna**: Nazwa hello hello maszyny wirtualnej, której brakuje aktualizacji.
* **AKTUALIZACJE systemu**: hello liczba brakujących aktualizacji systemu.
* **Czas ostatniego skanowania**: czas hello Centrum zabezpieczeń będzie ostatniego skanowania maszyny wirtualnej hello aktualizacji.
* **Stan**: hello bieżący stan zalecenia hello:
  * **Otwórz**: hello zalecenie nie zostały jeszcze zarejestrowane.
  * **Trwa**: hello zalecenie jest obecnie zastosowane toothose zasobów i jest wymagana żadna akcja.
  * **Rozwiązane**: hello zalecenie zostało już zakończone. (Po hello problem został rozwiązany, wpis hello jest wyszarzony).
* **WAŻNOŚĆ**: Opisuje ważność określonego zalecenia hello:
  * **Wysoka**: istnieje luka w zabezpieczeniach, która dotyczy istotnego zasobu (aplikacji, maszyny wirtualnej, sieciowej grupy zabezpieczeń) i wymaga uwagi.
  * **Średnia liczba godzin**: niekrytyczne lub dodatkowe kroki są wymagane toocomplete procesu lub wyeliminowania luki w zabezpieczeniach.
  * **Niska**: luka w zabezpieczeniach powinna zostać usunięta, ale nie wymaga natychmiastowej uwagi. (Domyślnie zalecenia o niskiej ważności nie są prezentowane, ale można filtrować według zalecenia o niskiej ważności, jeśli chcesz, aby tooview je.)

tooview hello szczegóły zalecenia, kliknij nazwę hello hello maszyny wirtualnej. Hello listę aktualizacji otwiera nowy blok dla tej maszyny wirtualnej, pokazane na powitania po zrzut ekranu.

![Brak aktualizacji systemu na określonej maszynie wirtualnej](./media/security-center-monitoring/security-center-monitoring-fig6-ga.png)

> [!NOTE]
> Witaj tutaj zalecenia dotyczące zabezpieczeń są hello takie same jak w hello **zalecenia** bloku. Zobacz hello [wdrażanie zaleceń dotyczących zabezpieczeń w Centrum zabezpieczeń Azure](security-center-recommendations.md) artykułu, aby uzyskać więcej informacji o tym, jak tooresolve zalecenia. Ma to zastosowanie nie tylko dla maszyn wirtualnych, ale także dla wszystkich zasobów, które są dostępne w hello **kondycja zasobów** kafelka.
>
>

#### <a name="virtual-machines-section"></a>Sekcja Maszyny wirtualne
sekcja maszyny wirtualne Hello zapewnia przegląd wszystkich maszyn wirtualnych i zaleceń. Każda kolumna reprezentuje jeden zestaw zaleceń, jak pokazano w powitania po zrzut ekranu:

![Przegląd wszystkich maszyn wirtualnych i zaleceń](./media/security-center-monitoring/security-center-monitoring-fig1-new005-2017.png)

Hello ikonę, która jest wyświetlana w obszarze każdy zalecenie ułatwia tooquickly można zidentyfikować hello maszyn wirtualnych, które wymagają uwagi i hello typu zalecenie.

W poprzednim przykładzie hello jednej maszyny wirtualnej widoczne jest krytyczne zalecenie dotyczące programu endpoint protection. tooget więcej informacji na temat hello maszyny wirtualnej, kliknij go. Nowy blok, którego kliknięcie spowoduje otwarcie reprezentuje tej maszyny wirtualnej, jak pokazano w powitania po zrzut ekranu.

![Szczegóły dotyczące zabezpieczeń maszyny wirtualnej](./media/security-center-monitoring/security-center-monitoring-fig8-ga.png)

Ten blok zawiera szczegóły zabezpieczeń hello hello maszyny wirtualnej. U dołu hello tego bloku można zauważyć, że hello zalecana Akcja i ważność poszczególnych problemów hello.

#### <a name="cloud-services-section"></a>Sekcja Usługi w chmurze
Usługi w chmurze zalecenie jest tworzone przy wersji systemu operacyjnego hello jest nieaktualny pokazane na powitania po zrzut ekranu:

![Stan kondycji dla usług w chmurze](./media/security-center-monitoring/security-center-monitoring-fig1-new006-2017.png)

W scenariuszu, w którym masz zalecenie (który nie jest hello przypadku hello w poprzednim przykładzie) należy toofollow hello kroków w wersji systemu operacyjnego hello hello zalecenie tooupdate. Gdy aktualizacja jest dostępna, konieczne będzie alert (czerwony lub kolor pomarańczowy - zależy hello ważność problemu hello). Po kliknięciu tego alertu w wierszach hello WebRole1 (systemem Windows Server z Twojej tooIIS automatycznie wdrożona aplikacja sieci web) lub WorkerRole1 (systemem Windows Server z Twojej tooIIS automatycznie wdrożona aplikacja sieci web), zawierający więcej szczegółów na ten temat zostanie otwarty nowy blok zalecenie, jak pokazano w powitania po zrzut ekranu:

![Szczegóły dotyczące usługi w chmurze](./media/security-center-monitoring/security-center-monitoring-fig8-new3.png)

toosee więcej przetestowanego wyjaśnienie zalecenie, kliknij przycisk **wersji systemu operacyjnego aktualizacji** w obszarze hello **opis** kolumny. Witaj **wersji aktualizacji systemu operacyjnego (wersja zapoznawcza)** zostanie otwarty blok zawierający więcej szczegółów.

![Zalecenia dotyczące usług w chmurze](./media/security-center-monitoring/security-center-monitoring-fig8-new4.png)  

### <a name="monitor-virtual-networks"></a>Monitorowanie sieci wirtualnych
Po kliknięciu **sieci** kafelku hello **sieci** zostanie otwarty blok zawierający więcej szczegółów, pokazane na powitania po zrzut ekranu:

![Blok Sieć](./media/security-center-monitoring/security-center-monitoring-fig9-new3.png)

#### <a name="networking-recommendations"></a>Zalecenia dotyczące sieci
Jak hello informacji o kondycji zasobów maszyny wirtualnej, ten blok zawiera skrócona lista problemów hello górnej części bloku hello i lista monitorowanych sieci na dole hello.

Hello sekcji podziału stanu sieci zawiera listę potencjalnych problemów z zabezpieczeniami i oferuje [zalecenia](security-center-network-recommendations.md). Mogą wystąpić następujące problemy:

* Zapora nowej generacji (NGFW) nie jest zainstalowana
* Sieciowe grupy zabezpieczeń w podsieciach nie są włączone
* Sieciowe grupy zabezpieczeń w maszynach wirtualnych nie są włączone
* Ograniczanie dostępu zewnętrznego za pośrednictwem publicznego zewnętrznego punktu końcowego
* Punkty końcowe mające połączenie z Internetem w dobrej kondycji

Po kliknięciu zalecenie, zawierający więcej szczegółów dotyczących zalecenia hello zostanie otwarty nowy blok, jak pokazano w hello poniższy przykład.

![Szczegóły zalecenia w bloku sieci hello](./media/security-center-monitoring/security-center-monitoring-fig9-ga.png)

W tym przykładzie hello **Konfiguruj brakujące grupy zabezpieczeń sieci dla podsieci** bloku ma listę podsieci i ochronę grupy zabezpieczeń sieci maszyn wirtualnych, które nie są spełnione. Kliknięcie toowhich podsieci hello ma tooapply hello sieciowej grupy zabezpieczeń, zostanie otwarty kolejny blok.

W hello **Wybieranie grupy zabezpieczeń sieci** bloku, można wybrać hello najbardziej odpowiednią sieciową grupę zabezpieczeń dla podsieci hello, lub można utworzyć nową grupę zabezpieczeń sieci.

#### <a name="internet-facing-endpoints-section"></a>Sekcja Internet facing endpoints (Punkty końcowe umożliwiające dostęp do Internetu)
W hello **internetowy punkty końcowe** sekcji, zostanie wyświetlony hello maszyn wirtualnych, które są aktualnie skonfigurowane z internetowego punktu końcowego i jego bieżący stan.

![Maszyny wirtualne skonfigurowane z użyciem punktu końcowego połączonego z Internetem oraz stan](./media/security-center-monitoring/security-center-monitoring-fig10-ga.png)

Ta tabela ma nazwę punktu końcowego hello, która reprezentuje hello maszyny wirtualnej, hello internetowy adres IP i hello bieżący stan ważności dla sieciowej grupy zabezpieczeń hello i hello zapory nowej generacji. Witaj w tabeli są posortowane według ważności:

* Kolor czerwony (u góry): wysoki priorytet, konieczne jest natychmiastowe rozwiązanie problemu
* Kolor pomarańczowy: średni priorytet, konieczne jest możliwie szybkie rozwiązanie problemu
* Kolor zielony (ostatni): stan prawidłowy

#### <a name="networking-topology-section"></a>Sekcja Topologia sieci
Witaj **topologia sieci** sekcja zawiera hierarchiczny widok zasobów hello, jak pokazano w powitania po zrzut ekranu:

![Hierarchiczny widok zasobów w sekcji Topologia sieci](./media/security-center-monitoring/security-center-monitoring-fig121-new4.png)

Informacje w tej tabeli (dotyczące maszyn wirtualnych i podsieci) zostały posortowane według ważności:

* Kolor czerwony (u góry): wysoki priorytet, konieczne jest natychmiastowe rozwiązanie problemu
* Kolor pomarańczowy: średni priorytet, konieczne jest możliwie szybkie rozwiązanie problemu
* Kolor zielony (ostatni): stan prawidłowy

W tym widoku topologii pierwszy poziom hello ma [sieci wirtualnych](../virtual-network/virtual-networks-overview.md), [bram sieci wirtualnej](/vpn-gateway/vpn-gateway-site-to-site-create.md), i [sieciami wirtualnymi (klasyczne)](/virtual-network/virtual-networks-create-vnet-classic-pportal.md). Hello drugi poziom obejmuje podsieci, a trzeci poziom hello ma hello maszyn wirtualnych, które należy toothose podsieci. Hello prawa kolumna ma hello bieżący stan hello sieciowej grupy zabezpieczeń dla tych zasobów, jak pokazano w hello poniższy przykład:

![Stan grupy zabezpieczeń sieci hello w sekcja topologia sieci](./media/security-center-monitoring/security-center-monitoring-fig12-ga.png)

Witaj dolnej części tego bloku ma hello zalecenia dotyczące tej maszyny wirtualnej, która jest podobna toowhat jest opisane wcześniej. Można kliknąć toolearn zalecenie więcej lub zastosować kontrolę zabezpieczeń potrzebne hello lub konfiguracji.

### <a name="monitor-storage--data"></a>Monitorowanie usługi Storage i danych

Po kliknięciu **magazyn & danych** w hello **zapobiegania** sekcji, hello **zasobów danych** zostanie otwarty blok zawierający zalecenia dotyczące SQL i magazynu. Obejmuje ona również [zalecenia](security-center-sql-service-recommendations.md) hello ogólnej kondycji stanu hello bazy danych. Aby uzyskać więcej informacji dotyczących szyfrowania magazynu, przeczytaj artykuł [Enable encryption for Azure storage account in Azure Security Center](security-center-enable-encryption-for-storage-account.md) (Włączanie szyfrowania dla konta usługi Azure Storage w usłudze Azure Security Center).

![Zasoby danych](./media/security-center-monitoring/security-center-monitoring-fig13-newUI-2017.png)

W obszarze **zalecenia SQL**, możesz kliknąć każde zalecenie i get więcej szczegółowych informacji o dalszych akcji tooresolve problemu. Witaj poniższy przykład pokazuje rozszerzenie hello hello **inspekcji bazy danych i wykrywanie zagrożeń baz danych SQL** zalecenia.

![Szczegółowe informacje o zaleceniach SQL](./media/security-center-monitoring/security-center-monitoring-fig14-ga-new.png)

Witaj **Włączanie inspekcji i wykrywanie zagrożeń baz danych SQL** bloku ma hello następujących informacji:

* Lista baz danych SQL
* powitania serwera, na którym znajdują się
* Informacje dotyczące tego, czy to ustawienie jest dziedziczone z serwera hello lub czy jest unikatowe w tej bazie danych
* bieżący stan Hello
* ważność Hello hello wydania

Po kliknięciu hello tooaddress bazy danych to zalecenie hello **Inspekcja i wykrywanie zagrożeń** zostanie otwarty blok, jak pokazano w powitania po ekranie.

![Blok Inspekcja i wykrywanie zagrożeń](./media/security-center-monitoring/security-center-monitoring-fig15-ga.png)

Inspekcja tooenable, wybierz opcję **ON** w obszarze hello **inspekcji** opcji.

### <a name="monitor-applications"></a>Monitorowanie aplikacji

Jeśli obciążenie platformy Azure obejmuje aplikacje znajdujące się w [maszyn wirtualnych (utworzonych za pomocą usługi Azure Resource Manager)](../azure-resource-manager/resource-manager-deployment-model.md) z uwidocznionymi portami sieci web (porty TCP 80 i 443), Centrum zabezpieczeń można monitorować tych tooidentify potencjalnych problemów z zabezpieczeniami oraz rekomendowania czynności naprawczych. Po kliknięciu hello **aplikacji** kafelku hello **aplikacji** z serię zaleceń w hello zostanie otwarty blok **zalecenia aplikacji** sekcji. Przedstawiono również hello podział aplikacji według hosta/wirtualnego adresu IP, jak pokazano w hello następującego zrzutu ekranu.

![Kondycja zabezpieczeń aplikacji](./media/security-center-monitoring/security-center-monitoring-fig16-ga.png)

Podobnie można odpowiednio z hello inne zalecenia, można kliknąć toosee zalecenie więcej szczegółów o problemie hello i w jaki sposób tooremediate. przykład Witaj pokazano na następującej ilustracji hello jest aplikacja, która została zidentyfikowana jako niezabezpieczona aplikacja sieci web. Po wybraniu aplikacji hello, który został uznany za bezpieczne kolejny blok otwiera z hello następujące możliwości:

![Szczegółowe informacje o niezabezpieczonej aplikacji](./media/security-center-monitoring/security-center-monitoring-fig17-ga.png)

Ten blok będzie zawierać listę wszystkich zaleceń dla tej aplikacji. Po kliknięciu hello **Dodawanie zapory aplikacji sieci web** zalecenie, hello **Dodawanie zapory aplikacji sieci Web** zostanie otwarty blok z opcjami możesz tooinstall zapory aplikacji sieci web (WAF) z partnerem jako pokazano hello następującego zrzutu ekranu.

![Okno dialogowe Dodaj zaporę aplikacji sieci Web](./media/security-center-monitoring/security-center-monitoring-fig18-ga.png)

## <a name="see-also"></a>Zobacz też
W tym artykule należy przedstawiono sposób toouse funkcji monitorowania w Centrum zabezpieczeń Azure. toolearn więcej informacji na temat Centrum zabezpieczeń Azure, zobacz następujące hello:

* [Ustawianie zasad zabezpieczeń w Centrum zabezpieczeń Azure](security-center-policies.md): Dowiedz się, jak tooconfigure ustawienia zabezpieczeń w Centrum zabezpieczeń Azure.
* [Zarządzanie i odpowiada toosecurity alertów w Centrum zabezpieczeń Azure](security-center-managing-and-responding-alerts.md): Dowiedz się, jak alerty toosecurity toomanage i odpowiada.
* [Monitorowanie rozwiązań partnerskich w Centrum zabezpieczeń Azure](security-center-partner-solutions.md): Dowiedz się, jak toomonitor hello stanu kondycji rozwiązań partnerskich.
* [Centrum zabezpieczeń Azure — często zadawane pytania](security-center-faq.md): często zadawane pytania dotyczące korzystania z usługi hello Znajdź.
* [Blog Azure Security](http://blogs.msdn.com/b/azuresecurity/) — wpisy na blogu dotyczące zabezpieczeń i zgodności platformy Azure.
