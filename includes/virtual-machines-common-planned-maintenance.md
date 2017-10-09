Azure okresowo przesyła aktualizacje tooimprove hello niezawodności, wydajności i zabezpieczeń hello infrastruktury hosta dla maszyn wirtualnych. Te aktualizacje należeć do zakresu od stosowania poprawek składników oprogramowania w hello hosting środowisku (na przykład systemu operacyjnego, funkcji hypervisor i różnych agentów wdrożonych na hoście hello), uaktualnienie składników sieciowych, likwidowanie toohardware. Większość Hello te aktualizacje są wykonywane bez żadnych maszyn wirtualnych hostowanych toohello wpływu. Istnieją jednak przypadki, w których aktualizacje mają wpływ:

- Jeśli hello konserwacji nie wymaga ponownego uruchomienia systemu, platforma Azure korzysta migracji w miejscu toopause hello maszyny Wirtualnej podczas hosta hello jest aktualizowany.

- Jeśli konserwacji wymaga ponownego uruchomienia, możesz uzyskać zawiadomienia o podczas konserwacji hello jest planowane. W takich przypadkach będziesz też mieć przedział czasu, w którym można uruchomić obsługi hello samodzielnie, w czasie, który można.

Na tej stronie opisano, jak Microsoft Azure wykonuje obu typów konserwacji. Aby uzyskać więcej informacji o zdarzeniach nieplanowane (awarii), zobacz Zarządzanie hello dostępność maszyn wirtualnych [systemu Windows] (.. / articles/virtual-machines/windows/manage-availability.md) lub [Linux](../articles/virtual-machines/linux/manage-availability.md).

Aplikacje działające na maszynie wirtualnej może zbieranie informacji na temat nadchodzących aktualizacji przy użyciu hello Azure metadane usługi dla [Windows](../articles/virtual-machines/windows/instance-metadata-service.md) lub [Linux] (.. / articles/virtual-machines/linux/instance-metadata-service.md).

## <a name="in-place-vm-migration"></a>Migracja maszyny Wirtualnej w miejscu

Gdy aktualizacje nie wymagają ponownego uruchomienia pełnej, migracji na żywo w miejscu jest używany. Podczas aktualizacji hello hello maszyna wirtualna jest wstrzymana około 30 sekund, zachowując hello pamięci RAM, hello środowisko macierzyste dotyczy hello niezbędne aktualizacje i poprawki. następnie zostanie wznowione Hello maszyny wirtualnej i zegara hello hello maszyny wirtualnej zostanie automatycznie zsynchronizowana.

Dla maszyn wirtualnych w zestawach dostępności aktualizacji domeny są zaktualizowane pojedynczo. Wszystkie maszyny wirtualne w jednej domenie aktualizacji (UD) są wstrzymane, aktualizowane i następnie wznowiona przed zaplanowanej konserwacji zostanie przeniesiony na toohello UD dalej.

Niektóre aplikacje może mieć wpływ na tego rodzaju aktualizacji. Aplikacje wykonujące przetwarzania, takich jak przesyłania strumieniowego multimediów lub transkodowanie lub uzyskać wysoką przepustowość sieci scenariuszy, w czasie rzeczywistym zdarzeń nie może być zaprojektowana tootolerate 30 jednosekundową przerwę. <!-- sooooo, what should they do? --> 


## <a name="maintenance-requiring-a-reboot"></a>Konserwacja konieczności ponownego uruchamiania

Jeśli maszyny wirtualne muszą toobe ponownego uruchomienia dla zaplanowanej konserwacji, użytkownik jest powiadamiany wcześniej. Planowana konserwacja ma dwie fazy: hello samoobsługi okno i okno zaplanowanej konserwacji.

Witaj **samoobsługi okna** umożliwia inicjowanie obsługi hello na maszyny wirtualne. W tym czasie można zbadać ich stan toosee każdej maszyny Wirtualnej i sprawdź hello wynik ostatniego żądania obsługi.

Po uruchomieniu konserwacji samoobsługi maszyny Wirtualnej jest przeniesionego tooa węzła, który został już zaktualizowany i uprawnień go ponownie. Ponieważ hello maszyny Wirtualnej wykonuje ponowny rozruch, dysku tymczasowym hello zostaną utracone i dynamicznych adresów IP skojarzonych z interfejsu sieci wirtualnej zostały zaktualizowane.

Jeśli start samoobsługi konserwacji i występuje błąd podczas procesu hello, operacja hello jest zatrzymana, hello maszyny Wirtualnej nie jest aktualizowany, a także zostanie usunięty z hello planowanych konserwacji iteracji. Będzie można z Tobą kontaktu w późniejszym czasie z nowego harmonogramu i oferowane nowe możliwości toodo samoobsługi konserwacji. 

Po upływie okna samoobsługi hello hello **zaplanowanego okna obsługi** rozpoczyna się. W tym oknie możesz nadal kwerendy hello okna obsługi, ale nie będzie już możliwe toostart hello konserwacji samodzielnie.

## <a name="availability-considerations-during-planned-maintenance"></a>Zagadnienia dotyczące dostępności podczas zaplanowanej konserwacji 

Jeśli zdecydujesz się toowait, dopóki hello planowane okna obsługi, istnieje kilka rzeczy tooconsider obsługę hello najwyższy availabilty sieci maszyn wirtualnych. 

### <a name="paired-regions"></a>Sparowanego regionów

Każdy region platformy Azure jest łączyć się z innego regionu w hello tej samej lokalizacji geograficznej, wraz z wprowadzeniem regionalnych pary. Podczas zaplanowanej konserwacji Azure zaktualizuje tylko hello maszyn wirtualnych w pojedynczym regionie pary regionu. Na przykład podczas aktualizowania hello maszyn wirtualnych w północno-środkowe stany, Azure nie może zaktualizować wszystkie maszyny wirtualne w południowo-środkowe stany na powitania tym samym czasie. Jednak innych regionów, takie jak Europa Północna, Europa może być w trakcie konserwacji na hello sam czas jako wschodnie stany USA. Zrozumienie, jak działają pary region może ułatwić lepsze dystrybucji maszyn wirtualnych w regionach. Aby uzyskać więcej informacji, zobacz [pary regionu Azure](https://docs.microsoft.com/azure/best-practices-availability-paired-regions).

### <a name="availability-sets-and-scale-sets"></a>Zestawy skali i zestawów dostępności

Podczas wdrażania obciążenia na maszynach wirtualnych Azure, można utworzyć maszyny wirtualne hello w aplikacji tooyour wysokiej dostępności tooprovide zestawu dostępności. Dzięki temu, że podczas awarii albo obsługi zdarzeń, jest dostępny co najmniej jednej maszyny wirtualnej.

W zestawie dostępności poszczególnych maszyn wirtualnych są rozkładane między zapasowej domen aktualizacji too20 (UDs). Podczas zaplanowanej konserwacji pogarsza tylko jedną aktualizację domeny w danym momencie. Należy pamiętać, że kolejność hello domen aktualizacji jest w pełni funkcjonalne nie niekoniecznie odbywa się po kolei. 

Zestawy skalowania maszyny wirtualnej są zasobami obliczeń platformy Azure umożliwiającą toodeploy i zarządzać zestawem identycznych maszyn wirtualnych jako pojedynczy zasób. zestaw skali Hello jest automatycznie wdrażane między domenami aktualizacji, takich jak maszyn wirtualnych w zestawie dostępności. Podobnie jak z zestawami dostępności zestawów skalowania tylko jedną aktualizację domeny pogarsza w danym momencie.

Aby uzyskać więcej informacji na temat konfigurowania maszyn wirtualnych wysokiej dostępności, zobacz Zarządzanie hello dostępność maszyn wirtualnych dla systemu Windows (.. / articles/virtual-machines/windows/manage-availability.md) lub [Linux](../articles/virtual-machines/linux/manage-availability.md).
