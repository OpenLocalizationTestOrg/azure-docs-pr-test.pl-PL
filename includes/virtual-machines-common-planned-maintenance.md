Azure wykonuje okresowo aktualizacje do poprawy niezawodności, wydajności i zabezpieczeń infrastruktury hosta dla maszyny wirtualnej. Zakres te aktualizacje z poprawki składników oprogramowania w środowisku macierzystym (na przykład systemu operacyjnego, funkcji hypervisor i różnych agentów wdrożonych na hoście), uaktualnienie składników sieciowych do likwidacji sprzętu. Większość tych aktualizacji są wykonywane bez wpływu na maszyny wirtualne. Istnieją jednak przypadki, w których aktualizacje mają wpływ:

- Jeśli konserwacji nie wymaga ponownego uruchomienia systemu, platforma Azure korzysta migracji w miejscu wstrzymanie maszyny Wirtualnej, gdy host jest aktualizowany.

- Jeśli konserwacji wymaga ponownego uruchomienia, możesz uzyskać zawiadomienia o podczas jest planowanych konserwacji. W takich przypadkach będziesz też mieć przedział czasu, w którym można uruchomić obsługi samodzielnie, w czasie, który należy.

Na tej stronie opisano, jak Microsoft Azure wykonuje obu typów konserwacji. Aby uzyskać więcej informacji o zdarzeniach nieplanowane (awarii), zobacz Zarządzanie dostępnością maszyn wirtualnych [systemu Windows] (../articles/virtual-machines/windows/manage-availability.md) lub [Linux](../articles/virtual-machines/linux/manage-availability.md).

Aplikacje działające na maszynie wirtualnej umożliwia zebranie informacji o nadchodzących aktualizacji za pomocą usługi Azure metadanych dla [Windows](../articles/virtual-machines/windows/instance-metadata-service.md) lub [Linux] (../articles/virtual-machines/linux/instance-metadata-service.md).

"Porad" uzyskać na zarządzanie maintence planowane, zobacz "Obsługa planowanych konserwacji powiadomienia" do [Linux](../articles/virtual-machines/linux/maintenance-notifications.md) lub [Windows](../articles/virtual-machines/windows/maintenance-notifications.md).

## <a name="in-place-vm-migration"></a>Migracja maszyny Wirtualnej w miejscu

Gdy aktualizacje nie wymagają ponownego uruchomienia pełnej, migracji na żywo w miejscu jest używany. Podczas aktualizacji maszyna wirtualna jest wstrzymana około 30 sekund, zachowując pamięci w pamięci RAM, środowisko macierzyste dotyczy niezbędne aktualizacje i poprawki. Maszyna wirtualna jest następnie wznowiona i zegara maszyny wirtualnej jest synchronizowana automatycznie.

Dla maszyn wirtualnych w zestawach dostępności aktualizacji domeny są zaktualizowane pojedynczo. Wszystkie maszyny wirtualne w jednej domenie aktualizacji (UD) są wstrzymany, aktualizacji i następnie ponownie uruchomiony przed zaplanowanej konserwacji przechodzi do następnego UD.

Niektóre aplikacje może mieć wpływ na tego rodzaju aktualizacji. Aplikacje wykonujące przetwarzania, takich jak przesyłania strumieniowego multimediów lub transkodowanie lub uzyskać wysoką przepustowość sieci scenariuszy, w czasie rzeczywistym zdarzeń nie mogą być przeznaczone do tolerować 30 jednosekundową przerwę. <!-- sooooo, what should they do? --> 


## <a name="maintenance-requiring-a-reboot"></a>Konserwacja konieczności ponownego uruchamiania

W przypadku maszyn wirtualnych wymagać ponownego dla zaplanowanych konserwacji, użytkownik jest powiadamiany wcześniej. Planowana konserwacja ma dwie fazy: okno samoobsługi i okno zaplanowanej konserwacji.

**Samoobsługi okna** umożliwia inicjowanie obsługi na maszyny wirtualne. W tym czasie można badać każdej maszyny Wirtualnej, aby wyświetlić ich stan i sprawdź wynik ostatniego żądania obsługi.

Podczas uruchamiania obsługi samoobsługi maszyny Wirtualnej jest przenoszony do węzła, który został już zaktualizowany i uprawnień go ponownie. Ponieważ ponownego uruchamiania maszyny Wirtualnej, tymczasowego dysku zostaną utracone i dynamicznych adresów IP skojarzonych z interfejsu sieci wirtualnej zostały zaktualizowane.

Występuje błąd podczas uruchamiania samoobsługi konserwacji, operacja nie zostanie zatrzymana, maszyna wirtualna nie zostanie zaktualizowana i powoduje również usunięcie z iteracji zaplanowanej konserwacji. Będzie można z Tobą kontaktu w późniejszym czasie z nowego harmonogramu i oferowane nową możliwość przeprowadzenia konserwacji samoobsługi. 

Po upływie okna samoobsługi **zaplanowanego okna obsługi** rozpoczyna się. W tym oknie można nadal zapytania dla okna obsługi, ale nie będzie można uruchomić obsługi samodzielnie.

## <a name="availability-considerations-during-planned-maintenance"></a>Zagadnienia dotyczące dostępności podczas zaplanowanej konserwacji 

Jeśli zdecydujesz się po upływie okno zaplanowanej konserwacji, jest kilka rzeczy, wziąć pod uwagę obsługę najwyższy availabilty sieci maszyn wirtualnych. 

### <a name="paired-regions"></a>Sparowanego regionów

Każdy region platformy Azure jest łączyć się z innego regionu w tej samej lokalizacji geograficznej, składają do regionalnych pary. Podczas zaplanowanej konserwacji Azure zaktualizuje tylko maszyn wirtualnych w pojedynczym regionie pary regionu. Na przykład podczas aktualizowania maszyn wirtualnych w regionie Północno-środkowe stany USA platforma Azure nie będzie jednocześnie przeprowadzać aktualizacji żadnych maszyn wirtualnych w regionie Południowo-środkowe stany USA. Inne regiony, takie jak Europa Północna, mogą być jednak w trakcie konserwacji w tym samym czasie, co region Wschodnie stany USA. Zrozumienie, jak działają pary region może ułatwić lepsze dystrybucji maszyn wirtualnych w regionach. Aby uzyskać więcej informacji, zobacz [pary regionu Azure](https://docs.microsoft.com/azure/best-practices-availability-paired-regions).

### <a name="availability-sets-and-scale-sets"></a>Zestawy skali i zestawów dostępności

W przypadku wdrażania obciążenia na maszynach wirtualnych Azure, można tworzyć maszyn wirtualnych w ramach dostępności skonfigurowany w celu zapewnienia wysokiej dostępności do aplikacji. Dzięki temu, że podczas awarii albo obsługi zdarzeń, jest dostępny co najmniej jednej maszyny wirtualnej.

W zestawie dostępności poszczególnych maszyn wirtualnych są rozkładane między domenami aktualizacji do 20 (UDs). Podczas zaplanowanej konserwacji pogarsza tylko jedną aktualizację domeny w danym momencie. Należy pamiętać, że kolejność domen aktualizacji jest w pełni funkcjonalne nie zawsze odbywa się po kolei. 

Zestawy skalowania maszyny wirtualnej są zasobów obliczeń platformy Azure, która umożliwia wdrażanie i zarządzanie nimi zestaw identycznych maszyn wirtualnych jako pojedynczy zasób. Zestaw skalowania jest automatycznie wdrażane między domenami aktualizacji, takich jak maszyn wirtualnych w zestawie dostępności. Podobnie jak z zestawami dostępności zestawów skalowania tylko jedną aktualizację domeny pogarsza w danym momencie.

Aby uzyskać więcej informacji na temat konfigurowania maszyn wirtualnych wysokiej dostępności, zobacz Zarządzanie dostępność maszyn wirtualnych dla [Windows](../articles/virtual-machines/windows/manage-availability.md) lub [Linux](../articles/virtual-machines/linux/manage-availability.md).
