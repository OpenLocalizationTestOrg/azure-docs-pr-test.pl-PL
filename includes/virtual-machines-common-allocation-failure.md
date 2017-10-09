
Jeśli problem Azure nie jest opisany w tym artykule, odwiedź hello [Azure fora MSDN i przepełnienie stosu](https://azure.microsoft.com/support/forums/). Problem można umieścić na tych fora lub too@AzureSupport w serwisie Twitter. Ponadto można pliku żądania pomocy technicznej platformy Azure, wybierając **uzyskać pomoc techniczną** na powitania [pomocy technicznej platformy Azure](https://azure.microsoft.com/support/options/) lokacji.

## <a name="general-troubleshooting-steps"></a>Ogólne kroki rozwiązywania problemów
### <a name="troubleshoot-common-allocation-failures-in-hello-classic-deployment-model"></a>Rozwiązywanie problemów z typowych błędów alokacji w hello klasycznego modelu wdrażania
Te czynności może pomóc rozwiązać wiele błędów alokacji w przypadku maszyn wirtualnych:

* Zmień rozmiar hello wirtualna tooa inny rozmiar maszyny Wirtualnej.<br>
    Kliknij przycisk **Przeglądaj wszystkie** > **maszyn wirtualnych (klasyczne)** > maszyny wirtualnej > **ustawienia** > **rozmiar**. Aby uzyskać szczegółowe instrukcje, zobacz [zmienić rozmiaru maszyny wirtualnej hello](https://msdn.microsoft.com/library/dn168976.aspx).
* Usunięcie wszystkich maszyn wirtualnych z usługi w chmurze hello i ponowne utworzenie maszyn wirtualnych.<br>
    Kliknij przycisk **Przeglądaj wszystkie** > **maszyn wirtualnych (klasyczne)** > maszyny wirtualnej > **usunąć**. Następnie kliknij przycisk **nowy** > **obliczeniowe** > [Obraz maszyny wirtualnej].

### <a name="troubleshoot-common-allocation-failures-in-hello-azure-resource-manager-deployment-model"></a>Rozwiązywanie problemów z typowych błędów alokacji w modelu wdrażania usługi Azure Resource Manager hello
Te czynności może pomóc rozwiązać wiele błędów alokacji w przypadku maszyn wirtualnych:

* Zatrzymaj (deallocate) wszystkich maszyn wirtualnych w hello dostępności tej samej ustawić, a następnie uruchom ponownie każdej z nich.<br>
    toostop: kliknij **grup zasobów** > grupy zasobów > **zasobów** > zestawu dostępności > **maszyn wirtualnych** > maszyny wirtualnej >  **Zatrzymaj**.
  
    Po zatrzymanie wszystkich maszyn wirtualnych, wybierz hello pierwsza maszyna wirtualna i kliknij przycisk **Start**.

## <a name="background-information"></a>Informacje uzupełniające
### <a name="how-allocation-works"></a>Jak działa alokacji
Witaj serwerach w centrach danych platformy Azure są dzielone w klastrach. Zwykle żądanie alokacji nastąpiła w wielu klastrach, ale istnieje możliwość, że niektóre ograniczenia na podstawie żądanie alokacji hello wymusić hello platformy Azure tooattempt hello żądania w tylko jednym klastrze. W tym artykule firma Microsoft będzie odwoływać się toothis jako "przypiętych tooa klastra." Diagram 1 poniżej przedstawia hello przypadku normalnych alokacji, który zostanie użyty w wielu klastrach. Diagram 2 przedstawia przypadku hello alokacji który zawiera przypięta tooCluster 2, ponieważ jest to, gdzie jest hostowana hello istniejący zestaw CS_1 usługi w chmurze lub dostępności.
![Diagram alokacji](./media/virtual-machines-common-allocation-failure/Allocation1.png)

### <a name="why-allocation-failures-happen"></a>Dlaczego stanie błędów alokacji
Żądanie alokacji jest przypięty tooa klastra, ma wyższy stopień niepowodzeniem toofind zwolnić zasoby, ponieważ pula zasobów dostępnych hello jest mniejszy. Ponadto jeśli żądanie alokacji jest przypięty tooa klastra, ale hello typ zasobu, która miała nie jest obsługiwany przez ten klaster, żądanie zakończy się niepowodzeniem nawet wtedy, gdy klaster hello ma zwolnić zasoby. Diagram 3 poniżej przedstawia przypadku hello gdzie przypiętych alokacja nie powiedzie się, ponieważ hello candidate tylko klastra nie ma wolnego zasobów. Diagram 4 przedstawia przypadku hello których alokacji przypiętych nie powiedzie się, ponieważ hello tylko candidate klastra nie obsługuje hello żądany rozmiar maszyny Wirtualnej, nawet jeśli klaster hello ma zwolnić zasoby.

![Błąd alokacji przypiętych](./media/virtual-machines-common-allocation-failure/Allocation2.png)

## <a name="detailed-troubleshoot-steps-specific-allocation-failure-scenarios-in-hello-classic-deployment-model"></a>Szczegółowe Rozwiązywanie problemów z scenariuszy awarii alokacji określonych czynności w hello klasycznego modelu wdrażania
Poniżej przedstawiono typowe scenariusze alokacji, które powodują toobe żądanie alokacji przypięty. Firma Microsoft będzie Poznaj każdego scenariusza w dalszej części tego artykułu.

* Zmień rozmiar maszyny Wirtualnej lub Dodaj maszyny wirtualne lub roli wystąpień tooan istniejącą usługę w chmurze
* Uruchom ponownie częściowo zatrzymania maszyny wirtualnej (cofnięciu przydziału)
* Uruchom ponownie pełni zatrzymania maszyny wirtualnej (cofnięciu przydziału)
* Wdrożeń przemieszczania/produkcyjnych (platforma jako usługa tylko)
* Grupa koligacji (zbliżeniowe maszyny Wirtualnej lub usługi)
* Oparte na grupach koligacji sieci wirtualnej

Gdy zostanie wyświetlony błąd alokacji, zobacz, jeśli dowolny z opisanych scenariuszy hello dotyczy błąd tooyour. Użyj hello alokacji błędu zwróconego przez hello platformy Azure tooidentify hello odpowiednim scenariuszem. Jeśli żądanie jest przypięty, usuń niektóre hello przypinania tooopen ograniczenia klastrów toomore żądania, co powoduje zwiększenie hello prawdopodobieństwo pomyślnego alokacji.

Ogólnie rzecz biorąc, tak długo, jak błąd hello nie wskazuje na "hello żądany rozmiar maszyny Wirtualnej nie jest obsługiwany", możesz zawsze ponowić w późniejszym czasie, jak wystarczająca liczba zasobów może zostać zwolniony w hello klastra tooaccommodate Twojego żądania. Jeśli hello problem jest tym hello żądany rozmiar maszyny Wirtualnej nie jest obsługiwana, spróbuj inny rozmiar maszyny Wirtualnej. W przeciwnym razie opcja tylko hello jest hello tooremove przypinanie ograniczenia.

Dwie typowe scenariusze niepowodzenia są grupami tooaffinity pokrewne. W ciągu ostatnich hello, grupy koligacji były używane tooprovide sąsiedztwie tooVMs/wystąpienia, lub używanych tooenable hello tworzenie sieci wirtualnej. Z wprowadzeniem regionalnych sieci wirtualnych hello grup koligacji nie są już wymagane toocreate sieci wirtualnej. Z hello zmniejszenia opóźnienia sieci w infrastrukturze Azure grup koligacji toouse hello zalecenia dla maszyny Wirtualnej lub usługi zbliżeniowe została zmieniona.

Rysunek 5 poniżej przedstawia taksonomii hello scenariuszy alokacji hello (przypięte).
![Taksonomii przypiętych alokacji](./media/virtual-machines-common-allocation-failure/Allocation3.png)

> [!NOTE]
> Błąd Hello wymienionych w każdym scenariuszu alokacji jest krótkich fragmentów. Zobacz toohello [błąd ciąg wyszukiwania](#Error string lookup) dla ciągów szczegółowe informacje o błędzie.
> 
> 

## <a name="allocation-scenario-resize-a-vm-or-add-vms-or-role-instances-tooan-existing-cloud-service"></a>Alokacja scenariusz: zmiana rozmiaru maszyny Wirtualnej lub Dodaj maszyny wirtualne lub roli wystąpienia tooan istniejącą usługę w chmurze
**Błąd**

Upgrade_VMSizeNotSupported lub GeneralError

**Przyczyną przypinanie klastra**

A żądanie tooresize maszyny Wirtualnej lub dodać maszyny Wirtualnej lub roli wystąpienia tooan istniejącej usługi w chmurze ma toobe podjęto na powitania oryginalnego klastra obsługującego hello istniejącą usługę w chmurze. Tworzenie nowej usługi w chmurze pozwala innego klastra, który zwolnić zasoby lub obsługuje hello rozmiar maszyny Wirtualnej, którego zażądano hello toofind platformy Azure.

**Obejście problemu**

Błąd hello Upgrade_VMSizeNotSupported * spróbuj inny rozmiar maszyny Wirtualnej. Jeśli przy użyciu innego rozmiaru maszyny Wirtualnej nie ma możliwości użycia, ale jeśli jest dopuszczalne toouse innego wirtualnego adresu IP (VIP), należy utworzyć nowe toohost usługi w chmurze hello nowej maszyny Wirtualnej i Dodaj hello nowe chmury usługi toohello regionalną sieć wirtualną gdzie hello istniejące maszyny wirtualne są uruchomione. Użycie istniejącej usługi w chmurze nie regionalną sieć wirtualną, możesz utworzyć nową sieć wirtualną dla hello nową usługę w chmurze, a następnie połącz z [istniejącej sieci wirtualnej toohello nową sieć wirtualną](https://azure.microsoft.com/blog/vnet-to-vnet-connecting-virtual-networks-in-azure-across-different-regions/). Zobacz więcej informacji [regionalnych sieci wirtualnych](https://azure.microsoft.com/blog/2014/05/14/regional-virtual-networks/).

W przypadku błędu hello GeneralError *, prawdopodobnie hello typ zasobu (np. dla określonego rozmiaru maszyny Wirtualnej) jest obsługiwana przez klaster hello, że klaster hello nie ma w chwili hello zwolnić zasoby. Podobne toohello powyżej scenariuszu dodać zasób obliczeniowy hello wymaganą przez proces tworzenia nowej usługi w chmurze (Zauważ, że hello nową usługę w chmurze ma toouse różnych adresów VIP) i używać tooconnect regionalnej sieci wirtualnej usługi w chmurze.

## <a name="allocation-scenario-restart-partially-stopped-deallocated-vms"></a>Scenariusz alokacji: ponowne uruchomienie częściowo zatrzymano (cofnięciu przydziału) maszyn wirtualnych
**Błąd**

GeneralError *

**Przyczyną przypinanie klastra**

Częściowe dezalokacji oznacza, że zatrzymane (cofnięciu przydziału) jeden lub więcej, ale nie wszystkich maszyn wirtualnych w usłudze w chmurze. Po zatrzymaniu (deallocate) maszyny Wirtualnej, hello skojarzone zasoby zostały zwolnione. Ponowne uruchomienie tego zatrzymanej maszyny Wirtualnej (cofnięciu przydziału) w związku z tym jest nowe żądanie alokacji. Ponowne uruchamianie maszyn wirtualnych w usłudze w chmurze częściowo deallocated jest równoważne tooadding maszyn wirtualnych tooan istniejącą usługę w chmurze. żądanie alokacji Hello ma toobe podjęto na powitania oryginalnego klastra obsługującego hello istniejącą usługę w chmurze. Trwa tworzenie innej usługi chmury umożliwia innego klastra, który bezpłatnego zasobu lub obsługuje hello rozmiar maszyny Wirtualnej, którego zażądano hello toofind platformy Azure.

**Obejście problemu**

Jeśli dopuszcza toouse różnych adresów VIP hello Usuń zatrzymane (cofnięciu przydziału) maszyn wirtualnych (ale zachować hello skojarzone dyski) i Dodaj hello maszyn wirtualnych powrotem przy użyciu innej usługi chmury. Użyj tooconnect regionalnej sieci wirtualnej usługi w chmurze:

* Jeśli istniejącą usługę w chmurze używa regionalną sieć wirtualną, po prostu Dodaj nowe toohello usługi chmury hello tej samej sieci wirtualnej.
* Użycie istniejącej usługi w chmurze nie regionalną sieć wirtualną, Utwórz nową sieć wirtualną dla hello nową usługę w chmurze, a następnie [połączyć istniejącej sieci wirtualnej toohello nowej sieci wirtualnej](https://azure.microsoft.com/blog/vnet-to-vnet-connecting-virtual-networks-in-azure-across-different-regions/). Zobacz więcej informacji [regionalnych sieci wirtualnych](https://azure.microsoft.com/blog/2014/05/14/regional-virtual-networks/).

## <a name="allocation-scenario-restart-fully-stopped-deallocated-vms"></a>Scenariusz alokacji: ponowne uruchomienie całkowicie zatrzymana (cofnięciu przydziału) maszyn wirtualnych
**Błąd**

GeneralError *

**Przyczyną przypinanie klastra**

Pełna dezalokacji oznacza, że został zatrzymany (cofnięciu przydziału) wszystkich maszyn wirtualnych z usługą w chmurze. Witaj toorestart żądań alokacji te maszyny wirtualne mają toobe podjęto na powitania oryginalnego klastra obsługującego hello usługi w chmurze. Tworzenie nowej usługi w chmurze pozwala innego klastra, który zwolnić zasoby lub obsługuje hello rozmiar maszyny Wirtualnej, którego zażądano hello toofind platformy Azure.

**Obejście problemu**

Jeśli jest dopuszczalne toouse innego adresu VIP, Usuń hello oryginalnego zatrzymane (cofnięciu przydziału) maszyn wirtualnych (ale zachować hello skojarzone dyski) i Usuń hello odpowiedniej chmury usługi (hello skojarzone obliczeniowej już wydane zasobów, gdy zostanie zatrzymane (cofnięciu przydziału) Witaj maszyn wirtualnych). Tworzenie maszyn wirtualnych nowe hello tooadd usługi chmury ponownie.

## <a name="allocation-scenario-stagingproduction-deployments-platform-as-a-service-only"></a>Scenariusz alokacji: wdrożeń przemieszczania/produkcyjnych (platforma jako usługa tylko)
**Błąd**

New_General * lub New_VMSizeNotSupported *

**Przyczyną przypinanie klastra**

Hello wdrożenia i hello wdrożenia produkcyjnego usługi w chmurze na potrzeby przemieszczania znajdują się w hello tego samego klastra. Po dodaniu hello drugie wdrożenie hello odpowiednie żądanie alokacji będą podejmowane w hello tego samego klastra, który jest hostem hello pierwszym wdrożeniu.

**Obejście problemu**

Usuń hello pierwszym wdrożeniu i hello oryginalnego usługi w chmurze, a następnie ponownie wdrożyć usługę w chmurze hello. Ta akcja może grunt hello pierwszym wdrożeniu w klastrze, który ma za mało wolnych zasobów toofit oba wdrożenia lub w klastrze, który obsługuje hello rozmiarów maszyn wirtualnych, które zostały wybrane.

## <a name="allocation-scenario-affinity-group-vmservice-proximity"></a>Scenariusz alokacji: Grupa koligacji (zbliżeniowe maszyny Wirtualnej lub usługi)
**Błąd**

New_General * lub New_VMSizeNotSupported *

**Przyczyną przypinanie klastra**

Wszystkich zasobów obliczeniowych tooan przypisanej grupie koligacji jest powiązany tooone klastra. Nowe żądania dotyczące zasobów obliczeniowych w tej grupie koligacji są próby w hello sam klastra, gdzie hostowane są hello istniejących zasobów. Jest to możliwe, czy nowe zasoby hello są tworzone przez nową usługę w chmurze albo przez istniejącą usługę w chmurze.

**Obejście problemu**

Grupy koligacji nie jest konieczne, nie używać grupy koligacji, czy grupa zasobów obliczeniowych do wielu grup koligacji.

## <a name="allocation-scenario-affinity-group-based-virtual-network"></a>Scenariusz alokacji: oparte na grupach koligacji sieci wirtualnej
**Błąd**

New_General * lub New_VMSizeNotSupported *

**Przyczyną przypinanie klastra**

Przed wprowadzeniem regionalnych sieci wirtualnych, było wymagane tooassociate sieci wirtualnej z grupą koligacji. W związku z tym związane są umieszczane w grupie koligacji zasoby obliczeniowe hello takich samych ograniczeń, zgodnie z opisem w hello "alokacji scenariusz: Grupa koligacji (zbliżeniowe maszyny Wirtualnej lub usługi)" powyższej sekcji. zasoby obliczeniowe Hello są wiązanej tooone klastra.

**Obejście problemu**

Nie należy do grupy koligacji Utwórz nową regionalną sieć wirtualną dla hello nowe zasoby, które dodajesz, a następnie [połączyć istniejącej sieci wirtualnej toohello nowej sieci wirtualnej](https://azure.microsoft.com/blog/vnet-to-vnet-connecting-virtual-networks-in-azure-across-different-regions/). Zobacz więcej informacji [regionalnych sieci wirtualnych](https://azure.microsoft.com/blog/2014/05/14/regional-virtual-networks/).

Można też [migracji sieci wirtualnej na podstawie grupy koligacji tooa regionalnej sieci wirtualnej](https://azure.microsoft.com/blog/2014/11/26/migrating-existing-services-to-regional-scope/), a następnie ponownie Dodaj zasoby hello potrzebne.

## <a name="detailed-troubleshooting-steps-specific-allocation-failure-scenarios-in-hello-azure-resource-manager-deployment-model"></a>Szczegółowe Rozwiązywanie problemów z scenariuszy awarii alokacji określonych kroków w modelu wdrażania usługi Azure Resource Manager hello
Poniżej przedstawiono typowe scenariusze alokacji, które powodują toobe żądanie alokacji przypięty. Firma Microsoft będzie Poznaj każdego scenariusza w dalszej części tego artykułu.

* Zmień rozmiar maszyny Wirtualnej lub Dodaj maszyny wirtualne lub roli wystąpień tooan istniejącą usługę w chmurze
* Uruchom ponownie częściowo zatrzymania maszyny wirtualnej (cofnięciu przydziału)
* Uruchom ponownie pełni zatrzymania maszyny wirtualnej (cofnięciu przydziału)

Gdy zostanie wyświetlony błąd alokacji, zobacz, jeśli dowolny z opisanych scenariuszy hello dotyczy błąd tooyour. Użyj hello alokacji błędu zwróconego przez hello platformy Azure tooidentify hello odpowiednim scenariuszem. Jeśli żądanie jest przypięty tooan istniejącego klastra, usuń niektóre hello przypinania tooopen ograniczenia klastrów toomore żądania, co powoduje zwiększenie hello prawdopodobieństwo pomyślnego alokacji.

Ogólnie rzecz biorąc, tak długo, jak błąd hello nie wskazuje na "hello żądany rozmiar maszyny Wirtualnej nie jest obsługiwany", możesz zawsze ponowić w późniejszym czasie, jak wystarczająca liczba zasobów może zostać zwolniony w hello klastra tooaccommodate Twojego żądania. Jeśli hello problem jest tym hello żądany rozmiar maszyny Wirtualnej nie jest obsługiwana, wymienione poniżej obejścia.

## <a name="allocation-scenario-resize-a-vm-or-add-vms-tooan-existing-availability-set"></a>Alokacja scenariusz: zmiana rozmiaru maszyny Wirtualnej lub Dodaj maszyny wirtualne tooan istniejącego zestawu dostępności
**Błąd**

Upgrade_VMSizeNotSupported * lub GeneralError *

**Przyczyną przypinanie klastra**

A żądanie tooresize maszyny Wirtualnej lub dodać tooan maszyny Wirtualnej, istniejącego zestawu dostępności ma toobe podjęto na powitania oryginalnego klastra obsługującego hello istniejącego zestawu dostępności. Tworzenie nowego zestawu dostępności umożliwia innego klastra, który zwolnić zasoby lub obsługuje hello rozmiar maszyny Wirtualnej, którego zażądano hello toofind platformy Azure.

**Obejście problemu**

Błąd hello Upgrade_VMSizeNotSupported * spróbuj inny rozmiar maszyny Wirtualnej. Jeśli przy użyciu innego rozmiaru maszyny Wirtualnej nie jest opcją, zatrzymanie wszystkich maszyn wirtualnych w zestawie dostępności hello. Możesz, a następnie zmień rozmiar hello hello maszyny wirtualnej, który przyzna hello klastra tooa maszyny Wirtualnej, który obsługuje hello żądany rozmiar maszyny Wirtualnej.

W przypadku błędu hello GeneralError *, prawdopodobnie hello typ zasobu (np. dla określonego rozmiaru maszyny Wirtualnej) jest obsługiwana przez klaster hello, że klaster hello nie ma w chwili hello zwolnić zasoby. Jeśli hello maszyny Wirtualnej może być częścią zestawu dostępności różnych, tworzenie nowej maszyny Wirtualnej w innym zestawem dostępności (w hello tego samego regionu). Ta nowa maszyna wirtualna może być dodane toohello tej samej sieci wirtualnej.  

## <a name="allocation-scenario-restart-partially-stopped-deallocated-vms"></a>Scenariusz alokacji: ponowne uruchomienie częściowo zatrzymano (cofnięciu przydziału) maszyn wirtualnych
**Błąd**

GeneralError *

**Przyczyną przypinanie klastra**

Częściowe dezalokacji oznacza, że zatrzymane (cofnięciu przydziału) co najmniej jeden, ale nie wszystkie, maszyn wirtualnych w dostępności ustawione. Po zatrzymaniu (deallocate) maszyny Wirtualnej, hello skojarzone zasoby zostały zwolnione. Ponowne uruchomienie tego zatrzymanej maszyny Wirtualnej (cofnięciu przydziału) w związku z tym jest nowe żądanie alokacji. Ponowne uruchamianie maszyn wirtualnych w zestawie dostępności częściowo deallocated równoważne tooadding dostępności istniejących maszyn wirtualnych tooan ustawiono. żądanie alokacji Hello ma toobe podjęto na powitania oryginalnego klastra obsługującego hello istniejącego zestawu dostępności.

**Obejście problemu**

Zatrzymanie wszystkich maszyn wirtualnych w zestawie przed ponowne uruchomienie hello pierwszego dostępności hello. Dzięki uruchomieniu nowego próba alokacji i że nowy klaster można wybrać z dostępnej pojemności.

## <a name="allocation-scenario-restart-fully-stopped-deallocated"></a>Scenariusz alokacji: ponowne uruchomienie całkowicie zatrzymana (cofnięciu przydziału)
**Błąd**

GeneralError *

**Przyczyną przypinanie klastra**

Pełna dezalokacji oznacza, że został zatrzymany (cofnięciu przydziału) wszystkich maszyn wirtualnych w zestawie dostępności. żądanie alokacji Hello toorestart tych maszyn wirtualnych będzie obowiązywać wszystkich klastrów, które obsługują hello wymagany rozmiar.

**Obejście problemu**

Wybierz nowe tooallocate rozmiar maszyny Wirtualnej. Jeśli to nie zadziała, spróbuj ponownie później.

## <a name="error-string-lookup"></a>Błąd podczas wyszukiwania ciągu
**New_VMSizeNotSupported***

"hello wirtualna rozmiaru (lub kombinacja rozmiarów maszyn wirtualnych) wymagany przez to wdrożenie nie mogą być udostępniane powodu ograniczeń żądania toodeployment. Jeśli to możliwe, spróbuj złagodzić ograniczenia, np. powiązania sieci wirtualnej, wdrażając tooa hostowanej usługi nie zawiera żadnych innych wdrożeń w nim i tooa koligacji innej grupy lub bez grupy koligacji i spróbuj wdrażanie tooa inny region. "

**New_General***

"Nie można przydzielić; Nie można toosatisfy ograniczenia w żądaniu. Hello żądanego nowe wdrożenie usługi jest tooan powiązanej grupie koligacji, jego celem sieci wirtualnej lub Brak istniejącego wdrożenia w ramach tej usługi hostowanej. Jeden z następujących warunków ogranicza toospecific wdrażania nowych hello Azure zasobów. Spróbuj ponownie później lub spróbuj zredukować rozmiar maszyny Wirtualnej hello lub liczbą wystąpień roli. Alternatywnie Jeśli to możliwe, usuń ograniczenia wyżej wymienione hello lub spróbuj użyć wdrażanie tooa inny region."

**Upgrade_VMSizeNotSupported***

"Tooupgrade hello wdrożenia. Witaj żądany rozmiar maszyny Wirtualnej XXX może nie być dostępne w hello zasobach obsługujących istniejące wdrożenie hello. Spróbuj ponownie później, spróbuj z mniejszym rozmiarem maszyny Wirtualnej lub mniejszą liczbą wystąpień roli lub Utwórz wdrożenie w ramach pustej usługi hostowanej z nową grupą koligacji lub bez powiązania z grupą koligacji."

**GeneralError***

"hello serwer napotkał błąd wewnętrzny. Ponów żądanie hello." Lub "Niepowodzenie tooproduce alokacji dla usługi hello".

