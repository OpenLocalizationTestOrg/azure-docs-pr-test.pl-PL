---
title: aaaReprotect z lokacji lokalnej Azure tooan | Dokumentacja firmy Microsoft
description: "Po pracy w trybie failover tooAzure maszyn wirtualnych można zainicjować toobring powrotu po awarii lokalnych tooon wstecz maszyn wirtualnych. Dowiedz się, jak tooreprotect przed powrotu po awarii."
services: site-recovery
documentationcenter: 
author: ruturaj
manager: gauravd
editor: 
ms.assetid: 44813a48-c680-4581-a92e-cecc57cc3b1e
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/05/2017
ms.author: ruturajd
ms.openlocfilehash: 94c86e79cba4cd3f0c5821fdd5509cca1d0e7820
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="reprotect-from-azure-tooan-on-premises-site"></a>Włącz ponownie ochronę z lokacji lokalnej Azure tooan



## <a name="overview"></a>Omówienie
W tym artykule opisano sposób tooreprotect Azure maszyn wirtualnych z lokacji lokalnej tooan platformy Azure. Witaj instrukcje w tym artykule, gdy wszystko jest gotowe toofail z powrotem z maszyn wirtualnych VMware lub serwerach fizycznych systemu Windows i Linux po zostały one przejścia w tryb failover z tooAzure lokacji lokalne powitania (zgodnie z opisem w [replikować wirtualne VMware maszyny i tooAzure serwery fizyczne z usługą Azure Site Recovery](site-recovery-failover.md)).

> [!WARNING]
> Nie można przerwać powrotem po [ukończenia migracji](site-recovery-migrate-to-azure.md#what-do-we-mean-by-migration), przenieść grupy zasobów tooanother maszyny wirtualnej lub Usuń maszynę wirtualną platformy Azure.


Po zakończeniu przełączonej i hello chronionych maszyn wirtualnych jest replikowana, można zainicjować powrót po awarii na powitania maszyn wirtualnych toobring ich toohello lokacji lokalnej.

Opublikuj komentarze lub pytania na końcu hello tym artykułem lub na powitania [Forum usług odzyskiwania Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

Aby szybko zapoznać Obejrzyj powitania po klip wideo dotyczący sposobu toofail za pośrednictwem z Azure tooan lokalnej lokacji.
> [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video5-Failback-from-Azure-to-On-premises/player]


## <a name="prerequisites"></a>Wymagania wstępne
Podczas przygotowywania maszyn wirtualnych tooreprotect podjąć lub należy wziąć pod uwagę następujące wstępnie wymagane akcje hello:

* Jeśli serwer vCenter zarządza hello maszyn wirtualnych, które mają toofail z powrotem do, upewnij się, że masz hello [wymagane uprawnienia](site-recovery-vmware-to-azure-classic.md) odnajdywania maszyn wirtualnych na serwer vCenter.

  > [!WARNING]
  > Jeśli migawki znajdują się na powitania lokalnymi wzorca docelowego lub hello maszyny wirtualnej przełączonej kończy się niepowodzeniem. Przed kontynuowaniem tooreprotect, można usunąć migawki hello w głównym celu hello. Witaj migawki na maszynie wirtualnej hello są scalane automatycznie podczas wykonywania zadania ponownej ochrony.

* Przed powrotem nie, należy utworzyć dwa dodatkowe składniki:

  * **Serwer przetwarzania**: hello [serwera przetwarzania](site-recovery-vmware-setup-azure-ps-resource-manager.md) odbiera dane z hello chronione maszyny wirtualnej platformy Azure i wysyła dane toohello lokalnej lokacji. Sieciach z małym opóźnieniami jest wymagany między hello serwer przetwarzania i hello chronione maszyny wirtualnej. W związku z tym może mieć lokalny serwer przetwarzania, jeśli używasz połączenia Azure ExpressRoute lub z serwera opartego na platformie Azure i sieci VPN.
  
  * **Główny serwer docelowy**: hello główny serwer docelowy odbiera dane powrotu po awarii. Serwer zarządzania lokalnymi Hello utworzony ma głównego serwera docelowego instalowane domyślnie. Jednak w zależności od hello ilość ruchu Wstecz nie powiodło się, może być konieczne toocreate oddzielne głównego serwera docelowego do powrotu po awarii.
    * [Maszyny wirtualnej systemu Linux wymaga Linux głównego serwera docelowego](site-recovery-how-to-install-linux-master-target.md).
    * Maszyny wirtualnej systemu Windows wymaga systemu Windows głównego serwera docelowego. Hello lokalnymi procesu serwera i wzorzec komputerów docelowych można użyć ponownie.

    główny cel Hello ma inne wymagania wstępne wymienione w [wspólnej toocheck rzeczy w głównym celu przed ponownej ochrony](site-recovery-how-to-reprotect.md#common-things-to-check-after-completing-installation-of-the-master-target-server).

* Serwer konfiguracji jest wymagana lokalnymi przechodzenia wstecz. Podczas powrotu po awarii hello maszyny wirtualnej musi istnieć w bazie danych hello konfiguracji serwera. W przeciwnym razie powrotu po awarii zakończy się niepowodzeniem. 

> [!IMPORTANT]
> Upewnij się, wykonanie zaplanowanego tworzenia kopii zapasowych serwera konfiguracji. W przypadku awarii, należy przywrócić serwer hello z hello adresów tego samego adresu IP, dzięki czemu działa w przypadku powrotu po awarii.

* Zestaw hello `disk.EnableUUID=true` ustawienie w hello parametry konfiguracji maszyny wirtualnej główny cel hello w środowisku programu VMware. Jeśli ten wiersz nie istnieje, dodaj ją. To ustawienie jest wymagane tooprovide spójny UUID dysku maszyny wirtualnej toohello (VMDK), aby go instaluje poprawnie.

* *Nie można użyć narzędzia Storage vMotion na powitania główny serwer docelowy*. Może to spowodować hello toofail powrotu po awarii. Nie można uruchomić maszyny wirtualnej Hello, ponieważ hello dyski nie są dostępne tooit. tooprevent ten problem, Wyklucz hello głównych serwerów docelowych z listy vMotion.

* Dodaj nowy serwer główny cel toohello dysku: dysk przechowywania. Dodaj nowy dysk hello dysku i formatu.


### <a name="frequently-asked-questions"></a>Często zadawane pytania

#### <a name="why-do-i-need-a-s2s-vpn-or-an-expressroute-connection-tooreplicate-data-back-toohello-on-premises-site"></a>Dlaczego potrzebujesz S2S sieci VPN lub ExpressRoute połączenia tooreplicate danych wstecz toohello lokalnej lokacji?
Replikacja z lokalnymi tooAzure może się zdarzyć, za pośrednictwem Internetu hello lub połączenie, które ma publicznej komunikacji równorzędnej ExpressRoute, przełączonej i powrotu po awarii lokacja lokacja (S2S) wymagają danych tooreplicate sieci VPN. Zapewniają hello sieci, dzięki czemu hello maszyn wirtualnych przełączona w tryb failover na platformie Azure może nawiązać połączenie serwera konfiguracji lokalne powitania (ping). Może również wdrożyć serwer procesu w hello Azure sieć maszyny wirtualnej hello przełączona w tryb failover. Ten serwer procesu należy również stanie toocommunicate z serwera konfiguracji lokalne powitania.

#### <a name="when-should-i-install-a-process-server-in-azure"></a>Podczas instalowania serwera przetwarzania na platformie Azure?


maszyny wirtualne Hello na platformie Azure, które mają tooreprotect wysyłają serwera przetwarzania tooa danych replikacji. Konfigurowanie sieci tak, aby hello maszyn wirtualnych na platformie Azure można osiągnąć powitania serwera przetwarzania.

Można wdrożyć serwer przetwarzania na platformie Azure lub użyj hello istniejący serwer przetwarzania używany podczas pracy awaryjnej. ważne tooconsider punktu Hello jest hello opóźnienia toosend hello danych z hello maszyn wirtualnych na serwerze przetwarzania toohello platformy Azure.

Jeśli masz Konfigurowanie połączenia ExpressRoute, można użyć lokalnego przetwarzania danych toosend serwera ponieważ hello opóźnienia między hello maszyny wirtualnej i serwera przetwarzania hello jest niski.

 ![Diagram architektury usługi ExpressRoute](./media/site-recovery-failback-azure-to-vmware-classic/architecture.png)



Jednak jeśli VPN S2S, zalecamy wdrożenie serwera przetwarzania hello na platformie Azure.

 ![Diagram architektury dla sieci VPN](./media/site-recovery-failback-azure-to-vmware-classic/architecture2.png)


Należy pamiętać, że replikacja odbywa się tylko za pośrednictwem połączenia VPN S2S hello lub hello prywatnej komunikacji równorzędnej ExpressRoute sieci. Upewnij się, że wystarczającą przepustowość jest dostępny za pośrednictwem tego kanału sieci.

Aby uzyskać informacje o instalowaniu serwera opartego na platformie Azure, zobacz [zarządzać serwerem procesów działających na platformie Azure](site-recovery-vmware-setup-azure-ps-resource-manager.md).

> [!TIP]
> Zalecamy używanie serwera opartego na platformie Azure podczas powrotu po awarii. wydajność procesu replikacji Hello jest większe, jeśli serwer przetwarzania hello jest bliżej toohello replikacji maszyny wirtualnej (hello maszynę przełączona w tryb failover na platformie Azure). Jednak podczas fazy weryfikacji koncepcji lub demonstracji, można użyć serwera przetwarzania lokalne powitania wraz z usługi ExpressRoute z prywatnej komunikacji równorzędnej hello toocomplete szybsze weryfikacji Koncepcji.



#### <a name="what-ports-should-i-open-on-different-components-so-that-reprotection-can-work"></a>Jakie porty należy otworzyć w różnych składników, dzięki czemu można pracować przełączonej?

![Porty dla trybu failover i powrotu po awarii](./media/site-recovery-failback-azure-to-vmware-classic/Failover-Failback.png)

#### <a name="which-master-target-server-should-i-use-for-reprotection"></a>Które główny serwer docelowy powinien używać przełączonej?
Lokalny główny serwer docelowy tooreceive wymagane dane z serwera przetwarzania hello, a następnie wpisz VMDK toohello na lokalnej maszynie wirtualnej firmy. W przypadku ochrony maszyn wirtualnych systemu Windows, należy Windows głównego serwera docelowego. Można użyć ponownie serwer przetwarzania lokalne powitania i główny serwer docelowy<!-- !todo component -->. Dla maszyn wirtualnych systemu Linux należy tooset dodatkowych lokalnych Linux głównego celu.


Informacje o instalowaniu głównego serwera docelowego zobacz:

* [Jak tooinstall Windows głównego serwera docelowego](site-recovery-vmware-to-azure.md)
* [Jak tooinstall Linux głównego serwera docelowego](site-recovery-how-to-install-linux-master-target.md)


#### <a name="what-datastore-types-are-supported-on-hello-on-premises-esxi-host-during-failback"></a>Jakie typy magazynu danych są obsługiwane na hoście ESXi lokalne powitania podczas powrotu po awarii?

Obecnie obsługuje usługi Azure Site Recovery nie może utworzyć kopię tylko system plików maszyny wirtualnej tooa (VMFS) lub sieci vSAN magazynu danych. Magazyn danych systemu plików NFS nie jest obsługiwane. Ze względu na ograniczenia toothis hello wybór magazynu danych wejściowych na powitania ekranu ponownej ochrony jest puste w przypadku hello datastores systemu plików NFS lub pokazuje hello vSAN z magazynu danych, ale nie powiedzie się podczas wykonywania zadania hello. Jeśli planujesz ponownie toofail, można tworzyć VMFS magazyn danych lokalnych i niepowodzenie tooit Wstecz. Pełnego pobierania hello VMDK spowoduje, że ta powrotu po awarii.

### <a name="common-things-toocheck-after-completing-installation-of-hello-master-target-server"></a>Typowe toocheck czynności po zakończeniu instalacji hello główny serwer docelowy

* Jeśli hello jest obecna maszyna wirtualna lokalnie na hello serwera vCenter, hello główny serwer docelowy musi dostęp VMDK toohello na lokalnej maszynie wirtualnej firmy. Dostęp jest wymagane toowrite hello replikowane dane toohello dyski maszyny wirtualnej. Upewnij się, że magazyn maszyny wirtualnej lokalne powitania danych jest zainstalowany na hoście hello główny cel z dostępem do odczytu/zapisu.

* Jeśli maszyna wirtualna hello nie jest obecny lokalne powitania vCenter Server, hello usługi Site Recovery musi toocreate nowej maszyny wirtualnej podczas zastosowania. Ta maszyna wirtualna jest tworzony na hoście ESX hello utworzenia hello głównego celu. Wybierz hello ESX host, tak, aby maszyna wirtualna powrotu po awarii hello jest tworzona na hoście hello, który ma.

* *Nie można użyć narzędzia Storage vMotion hello główny serwer docelowy*. Może to spowodować hello toofail powrotu po awarii. Nie można uruchomić maszyny wirtualnej Hello, ponieważ hello dyski nie są dostępne tooit.

  > [!WARNING]
  > Jeśli główny cel ulega zadań vMotion magazynu po przełączonej, hello chronionych maszyn wirtualnych dysków, które są dołączone toohello główny cel migracji docelowej toohello hello vMotion zadania. Jeśli spróbujesz toofail po to, oderwania hello dysku nie powiedzie się, ponieważ hello dyski nie zostały znalezione. Następnie staje się on toofind twardych dysków hello kont magazynu. Należy toofind je ręcznie i dołącz je toohello maszyny wirtualnej. Następnie można uruchomić hello na lokalnej maszynie wirtualnej.

* Dodaj przechowywania dysku tooyour istniejących Windows głównego serwera docelowego. Dodaj nowy dysk hello dysku i formatu. dysk przechowywania Hello są używane toostop hello punkty w czasie moment hello maszyny wirtualnej replikacji lokacji lokalnej toohello Wstecz. Poniżej przedstawiono niektóre kryteria dysk przechowywania. Bez tych kryteriów hello dysku nie są wyświetlane dla hello główny serwer docelowy.

   * Witaj wolumin nie jest używany do innych celów, takich jak element docelowy replikacji.

   * Witaj wolumin nie jest w trybie blokady.

   * Witaj wolumin nie jest woluminem pamięci podręcznej. Witaj główny cel nie należy zainstalować na tym woluminie. Hello niestandardowej instalacji woluminu docelowego serwera i głównego procesu hello jest nieodpowiedni dla woluminu przechowywania. Gdy hello serwer przetwarzania i główny serwer docelowy są zainstalowane na woluminie, hello wolumin jest pamięć podręczna hello głównego elementu docelowego.

   * Typ systemu plików Hello hello woluminu nie jest FAT lub FAT32.

   * pojemność woluminu Hello jest różna od zera.

   * wolumin przechowywania domyślnego powitania dla systemu Windows jest hello R.

   * wolumin przechowywania domyślne Hello Linux jest /mnt/retention.

  > [!IMPORTANT]
  > Jeśli używasz istniejącej maszyny serwera konfiguracji serwera/procesu lub skali lub proces serwera/główną maszynę docelową, na serwerze należy tooadd nowego dysku. nowy dysk Hello powinna spełniać hello poprzedzających wymagania. Jeśli nie ma dysku przechowywania hello, nie zostanie wyświetlone na liście rozwijanej wyboru hello na powitania portalu. Po dodaniu dysku toohello lokalnymi główny cel zajmuje minut too15 tooappear dysku hello w zaznaczeniu hello na powitania portalu. Można również odświeżyć hello konfiguracji serwera, jeśli nie ma dysku powitania po 15 minutach.

* Maszyny wirtualne systemu Linux przełączona w tryb failover wymaga Linux głównego serwera docelowego. Przełączona w tryb failover maszyny wirtualnej systemu Windows wymaga systemu Windows głównego serwera docelowego.

* Zainstaluj narzędzia VMware na powitania główny serwer docelowy. Bez hello narzędzi VMware nie można wykryć datastores hello na hoście ESXi hello głównego celu.

* Włącz hello `disk.EnableUUID=true` parametru na maszynie wirtualnej główny cel hello za pomocą właściwości vCenter hello. <!-- !todo Needs link. -->

* główny cel Hello powinien mieć co najmniej jeden datastore VMFS dołączony. Jeśli nie ma none, hello **Datastore** dane wejściowe na stronie ponownej ochrony hello będzie pusta, i nie może kontynuować.

* Witaj główny serwer docelowy nie może mieć migawek na dyskach hello. W przypadku migawki nie przełączonej i powrotu po awarii.

* główny cel Hello nie może mieć kontroler Paravirtual SCSI. można tylko kontrolera LSI Logic Hello kontrolera. Bez kontrolera LSI Logic przełączonej kończy się niepowodzeniem.

<!--
### Failback policy
tooreplicate back tooon-premises, you will need a failback policy. This policy get automatically created when you create a forward direction policy. Note that

1. This policy gets auto associated with hello configuration server during creation.
2. This policy is not editable.
3. hello set values of hello policy are (RPO Threshold = 15 Mins, Recovery Point Retention = 24 Hours, App Consistency Snapshot Frequency = 60 Mins)
   ![](./media/site-recovery-failback-azure-to-vmware-new/failback-policy.png)

-->

## <a name="steps-tooreprotect"></a>Kroki tooreprotect

> [!NOTE]
> Po uruchomieniu maszyny wirtualnej na platformie Azure, dopiero po pewnym czasie dla agenta hello tooregister wstecz toohello konfiguracji serwera (too15 minut). W tym czasie ponowne włączenie ochrony kończy się niepowodzeniem, a komunikat o błędzie wskazuje, że nie jest zainstalowany hello agent. Poczekaj kilka minut, a następnie spróbuj ponownie zastosowania.



1. W **magazynu** > **elementy replikowane**, kliknij prawym przyciskiem myszy hello maszyny wirtualnej, która jest Failover, a następnie wybierz **ponownego włączenia ochrony**. Możesz również kliknąć hello komputera i wybierz pozycję **ponownego włączenia ochrony** z hello przyciski poleceń.
2. W bloku hello zauważyć kierunku hello ochrony, **Azure lokalnych tooOn**, jest już wybrana.
3. W **główny serwer docelowy** i **serwera przetwarzania**, wybierz hello lokalny główny serwer docelowy i hello serwera przetwarzania.
4. Aby uzyskać **Datastore**, wybierz hello toowhich magazynu danych ma toorecover hello dyski lokalne. Ta opcja jest używana, gdy hello na lokalnej maszynie wirtualnej zostanie usunięta, a należy toocreate nowych dysków. Ta opcja jest ignorowana, jeśli dyski hello już istnieje, ale nadal potrzebujesz toospecify wartość.
5. Wybierz dysk przechowywania hello.
6. zasady powrotu po awarii Hello jest automatycznie wybierany.
7. Kliknij przycisk **OK** toobegin zastosowania. Zadanie rozpoczyna się maszyny wirtualnej hello tooreplicate z lokacji lokalnej toohello platformy Azure. Możesz śledzić postępy hello na powitania **zadania** kartę.

Jeśli chcesz, aby toorecover tooan lokalizacji alternatywnej (po usunięciu hello na lokalnej maszynie wirtualnej), wybierz dysk przechowywania hello i magazynu danych skonfigurowanego dla hello główny serwer docelowy. Przechodzenia wstecz toohello lokalnej lokacji hello VMware maszyn wirtualnych w użyciu plan ochrony powrotu po awarii hello hello tego samego magazynu danych, jak hello głównym serwerze docelowym. W programie vCenter zostanie utworzona nowa maszyna wirtualna.

Jeśli chcesz maszyny wirtualnej hello toorecover na Azure tooan istniejącej lokalnej maszyny wirtualnej, hello instalacji lokalnej datastores maszyny wirtualnej z dostępem do odczytu/zapisu na hoście ESXi hello głównego serwera docelowego jest.
    ![Okno dialogowe ponownego włączenia ochrony](./media/site-recovery-failback-azure-to-vmware-new/reprotectinputs.png)

Można również Obejmij ochroną na poziomie hello planu odzyskiwania. Grupa replikacji może przełączona do trybu tylko do planu odzyskiwania. Gdy użytkownik zacznij ponownie chronić przy użyciu planu odzyskiwania, należy tooprovide hello wartości dla każdego chronionego komputera.

> [!NOTE]
> Użyj hello tego samego tooreprotect serwer główny serwer docelowy do grupy replikacji. Jeśli używasz tooreprotect serwera różnych główny serwer docelowy do grupy replikacji, powitania serwera nie może dostarczyć wspólnego punktu w czasie.

> [!NOTE]
> Witaj na lokalnej maszynie wirtualnej jest wyłączony podczas zastosowania. Pomaga to zapewnić spójność danych podczas replikacji. Nie należy włączać maszyny wirtualnej hello, po zakończeniu zastosowania.

Po pomyślnym zainicjowaniu przełączonej hello, hello maszyny wirtualnej przechodzą w stan chronionych.

## <a name="next-steps"></a>Następne kroki

Po wprowadzeniu chronionych stan maszyny wirtualnej hello można [zainicjować powrotu po awarii](site-recovery-how-to-failback-azure-to-vmware.md#steps-to-fail-back). 

Powrót po awarii Hello zamknie hello maszyny wirtualnej platformy Azure i maszyny wirtualnej lokalne powitania rozruchu. Oczekiwane przestój dla aplikacji hello. Wybierz czas powrotu po awarii, jeśli aplikacja hello może tolerować przestoju.

## <a name="common-problems"></a>Typowe problemy

* Jeśli używasz toocreate szablon maszyn wirtualnych, upewnij się, że każda maszyna wirtualna ma własny identyfikator UUID hello dysków. Jeśli hello lokalnymi kolizji UUID maszyny wirtualnej ze elementu głównego celu hello ponieważ oba utworzone przy użyciu hello sam szablonu, ponowne włączenie ochrony kończy się niepowodzeniem. Wdrażanie innego główny cel, który nie został utworzony z hello sam szablonu.

* Jeśli odnajdywanie vCenter użytkownika tylko do odczytu i ochrony maszyn wirtualnych, ochrona zakończy się pomyślnie i tryb failover działa prawidłowo. Podczas zastosowania trybu failover nie powiedzie się, ponieważ nie można odnaleźć hello datastores. Objawem jest tym powitalne datastores nie są wyświetlane podczas zastosowania. tooresolve ten problem, można zaktualizować poświadczeń vCenter hello przy użyciu odpowiedniego konta, które ma uprawnienia, i spróbuj ponownie uruchomić zadanie hello. Aby uzyskać więcej informacji, zobacz [VMware replikowanie maszyn wirtualnych i serwerów fizycznych tooAzure z usługą Azure Site Recovery](site-recovery-vmware-to-azure-classic.md).

* Gdy nastąpił powrót po awarii maszyny wirtualnej systemu Linux i uruchomić ją lokalnie, można zauważyć, że pakietu Menedżera sieci, aby hello został odinstalowany z komputera hello. Ta dezinstalacja spowodowany hello Menedżera sieci pakiet zostanie usunięty po odzyskaniu hello maszyny wirtualnej na platformie Azure.

* Maszyny wirtualnej systemu Linux jest skonfigurowane za pomocą statycznego adresu IP i przeszła w tryb failover tooAzure, adres IP hello są uzyskiwane z serwera DHCP. Podczas przejścia w tryb failover tooon lokalnych, maszyna wirtualna hello jest nadal toouse — adres IP hello tooacquire DHCP. Ręcznie Zaloguj toohello maszyny i ustawić adres statyczny tooa wstecz adres IP hello, w razie potrzeby. Maszyny wirtualnej systemu Windows można ponownie uzyskać jego statyczny adres IP.

* Jeśli używany jest bezpłatna wersja ESXi 5.5 lub bezpłatna wersja funkcji Hypervisor vSphere 6, trybu failover zakończy się pomyślnie, ale powrotu po awarii nie powiedzie się. tooenable powrotu po awarii licencji ewaluacyjnej programu tooeither uaktualnienia.

* Jeśli nie można osiągnąć powitania serwera konfiguracji z serwera przetwarzania hello, użyj Telnet toocheck łączności toohello konfiguracji serwera na porcie 443. Można też spróbować tooping hello konfiguracji serwera z serwera przetwarzania hello. Serwer przetwarzania powinny mieć również pulsu jest toohello połączony serwer konfiguracji.

* Jeśli próbujesz toofail tooan wstecz alternatywny vCenter, upewnij się, Twoje nowe vCenter i hello główny serwer docelowy są odnajdywane. Typowy objaw jest czy hello datastores nie są dostępne lub widoczne w hello **Wznów** okno dialogowe.

* Serwer systemu Windows Server 2008 R2 z dodatkiem SP1, który jest chroniony jako fizycznego lokalnego serwera nie może nie z lokacji lokalnej tooan platformy Azure.
