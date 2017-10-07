---
title: "aaaHigh dostępności i odzyskiwania po awarii dla programu SQL Server | Dokumentacja firmy Microsoft"
description: "Omówienie hello różnych typów HADR strategii dla programu SQL Server uruchomionego w maszynach wirtualnych platformy Azure."
services: virtual-machines-windows
documentationcenter: na
author: MikeRayMSFT
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 53981f7e-8370-4979-b26a-93a5988d905f
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 06/27/2017
ms.author: mikeray
ms.openlocfilehash: 2b62d8b30520952ba6b7da7177a2c2de95bea8ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="high-availability-and-disaster-recovery-for-sql-server-in-azure-virtual-machines"></a>Wysoka dostępność i odzyskiwanie awaryjne na potrzeby programu SQL Server na maszynach wirtualnych platformy Azure

Maszyny wirtualne Microsoft Azure (maszyn wirtualnych) z programem SQL Server może ułatwić niższy koszt hello wysokiej dostępności i odzyskiwaniem po awarii (HADR) bazy danych rozwiązania służącego do odzyskiwania. Większość rozwiązań HADR serwera SQL są obsługiwane w maszynach wirtualnych platformy Azure, tylko do platformy Azure oraz w hybrydowych rozwiązań. W rozwiązaniu Azure — tylko do całego systemu HADR hello działa na platformie Azure. W konfiguracji hybrydowych część rozwiązania hello działa na platformie Azure i hello innych części przebiegów lokalnych w Twojej organizacji. Witaj elastyczność hello środowiska platformy Azure pozwala toomove częściowo lub całkowicie tooAzure toosatisfy hello budżetu i HADR wymagania programu SQL Server bazy danych systemów.

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="understanding-hello-need-for-an-hadr-solution"></a>Opis hello potrzebę HADR rozwiązania
Jest zapasowej tooyou tooensure czy system bazy danych, posiada hello HADR możliwości, które wymaga hello umowy poziomu usług (SLA). fakt Hello Azure zapewnia mechanizmy wysokiej dostępności, takich jak naprawą usługi dla usługi w chmurze i wykrywanie awarii odzyskiwania dla maszyn wirtualnych, sam gwarantuje, że mogą spełnić hello potrzeby umowy dotyczącej poziomu usług. Te mechanizmy ochrony hello wysoką dostępność hello maszyn wirtualnych, ale hello wysokiej dostępności programu SQL Server uruchomiony hello maszyn wirtualnych. Istnieje możliwość toofail wystąpienia programu SQL Server hello, podczas gdy hello maszyna wirtualna jest online i czy działa prawidłowo. Ponadto mechanizmów wysokiej dostępności nawet hello dostarczany przez platformę Azure Zezwalaj przestoje hello maszyn wirtualnych z powodu tooevents, takich jak odzyskiwania po awarii oprogramowania lub sprzętu i uaktualnień systemu operacyjnego.

Ponadto z magazynu geograficznie nadmiarowego magazynu (GRS) na platformie Azure, która jest zaimplementowana przy użyciu funkcji o nazwie — replikacja geograficzna, nie może być rozwiązanie odzyskiwania po awarii odpowiednie dla baz danych. Ponieważ replikacja geograficzna wysyła dane asynchronicznie, najnowsze aktualizacje mogą utracone w przypadku powitania po awarii. Więcej informacji na temat ograniczeń — replikacja geograficzna są objęte hello [replikacja geograficzna nie jest obsługiwana dla plików danych i dziennika na oddzielnych dyskach](#geo-replication-support) sekcji.

## <a name="hadr-deployment-architectures"></a>HADR wdrożenia architektury
Technologii HADR serwera SQL, które są obsługiwane na platformie Azure, obejmują:

* [Zawsze włączone grupy dostępności](https://technet.microsoft.com/library/hh510230.aspx)
* [Zawsze włączone wystąpienia klastra trybu Failover](https://technet.microsoft.com/library/ms189134.aspx)
* [Wysyłanie dziennika](https://technet.microsoft.com/library/ms187103.aspx)
* [Kopia zapasowa programu SQL Server i przywracania usługi magazynu obiektów Blob platformy Azure](https://msdn.microsoft.com/library/jj919148.aspx)
* [Funkcja dublowania baz danych](https://technet.microsoft.com/library/ms189852.aspx) — przestarzałe w programie SQL Server 2016

Jest możliwe toocombine hello technologii razem tooimplement rozwiązania programu SQL Server, która ma wysoką dostępność i możliwości odzyskiwania po awarii. W zależności od używanych technologii hello wdrożenia hybrydowego może wymagać tunel sieci VPN z hello sieci wirtualnej platformy Azure. Poniższe rozdziały zawierają Hello pokazują hello przykład wdrożenia architektur.

## <a name="azure-only-high-availability-solutions"></a>Tylko do platformy Azure: rozwiązania wysokiej dostępności

Rozwiązanie zapewniające wysoką dostępność dla programu SQL Server może być na poziomie bazy danych z zawsze włączonych grup dostępności - o nazwie grupy dostępności. Można również utworzyć rozwiązanie zapewniające wysoką dostępność na poziomie wystąpienia z zawsze na wystąpienia klastra trybu Failover — trybu failover wystąpienia klastra. Dla dodatkowych nadmiarowość można utworzyć nadmiarowości na obu poziomach przez utworzenie grupy dostępności na trybu failover wystąpienia klastra. 

| Technologia | Przykład architektury |
| --- | --- |
| **Grupy dostępności** |Repliki dostępności uruchomionych w maszynach wirtualnych platformy Azure w hello sam region zapewnić wysoką dostępność. Należy tooconfigure kontroler domeny maszyny Wirtualnej, ponieważ klaster pracy awaryjnej systemu Windows wymaga domeny usługi Active Directory.<br/> ![Grupy dostępności](./media/virtual-machines-windows-sql-high-availability-dr/azure_only_ha_always_on.gif)<br/>Aby uzyskać więcej informacji, zobacz [Konfigurowanie grup dostępności Azure (GUI)](virtual-machines-windows-portal-sql-alwayson-availability-groups.md). |
| **Wystąpienia klastra trybu failover** |Klastra trybu failover wystąpienia (FCI), które wymagają magazynu udostępnionego, mogą być tworzone na 3 sposoby.<br/><br/>1. Klaster trybu failover z dwoma węzłami uruchomionych w maszynach wirtualnych platformy Azure z dołączonym magazynem za pomocą [systemu Windows Server 2016 bezpośrednie miejsca do magazynowania \(S2D\) ](virtual-machines-windows-portal-sql-create-failover-cluster.md) tooprovide wirtualnej sieci SAN opartych na oprogramowaniu.<br/><br/>2. Klaster trybu failover z dwoma węzłami uruchomionych w maszynach wirtualnych platformy Azure z magazynem obsługiwanego przez rozwiązanie do klastrowania innych firm. Na przykład określonych, który używa SIOS DataKeeper, zobacz [wysokiej dostępności udziału plików przy użyciu klastra trybu failover i 3 firmy SIOS DataKeeper](https://azure.microsoft.com/blog/high-availability-for-a-file-share-using-wsfc-ilb-and-3rd-party-software-sios-datakeeper/).<br/><br/>3. Uruchomionych w maszynach wirtualnych platformy Azure z obiektów docelowych iSCSI zdalnego klastra trybu failover z dwoma węzłami udostępnionego magazynu blokowego za pośrednictwem usługi ExpressRoute. Na przykład NetApp prywatnego magazynu (NPS) udostępnia obiektu docelowego iSCSI za pośrednictwem usługi ExpressRoute z tooAzure Equinix maszyn wirtualnych.<br/><br/>Magazyn udostępniony innej firmy i rozwiązania dotyczące replikacji danych powinien skontaktuj się z dostawcą hello dla dowolnych danych powiązanych tooaccessing problemów w pracy awaryjnej.<br/><br/>Należy pamiętać, że przy użyciu infrastruktury klasyfikacji plików nad [magazyn plików Azure](https://azure.microsoft.com/services/storage/files/) nie jest jeszcze obsługiwany, ponieważ Magazyn w warstwie Premium nie korzysta z tego rozwiązania. Pracujemy nad toosupport tym wkrótce. |

## <a name="azure-only-disaster-recovery-solutions"></a>Tylko do platformy Azure: rozwiązania w zakresie odzyskiwania po awarii
Możesz mieć rozwiązanie odzyskiwania po awarii dla baz danych programu SQL Server na platformie Azure przy użyciu grup dostępności, dublowania bazy danych lub kopii zapasowej i przywracanie z magazynu obiektów blob.

| Technologia | Przykład architektury |
| --- | --- |
| **Grupy dostępności** |Repliki dostępności z wielu centrów w maszynach wirtualnych platformy Azure dla odzyskiwania po awarii. To rozwiązanie między region chroni przed awarią całej lokacji. <br/> ![Grupy dostępności](./media/virtual-machines-windows-sql-high-availability-dr/azure_only_dr_alwayson.png)<br/>W obrębie regionu wszystkie repliki należy w ramach hello sama usługa w chmurze i hello tej samej sieci wirtualnej. Ponieważ każdy region będzie mieć osobne sieci wirtualnej, te rozwiązania wymagają łączności tooVNet sieci wirtualnej. Aby uzyskać więcej informacji, zobacz [Konfiguruj do wirtualnymi połączenia za pomocą hello portalu Azure](../../../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md). Aby uzyskać szczegółowe instrukcje, zobacz [konfigurowania grupy dostępności programu SQL Server na maszynach wirtualnych Azure w różnych regionach](virtual-machines-windows-portal-sql-availability-group-dr.md).|
| **Funkcja dublowania baz danych** |Podmiot zabezpieczeń i dublowane i serwerów działających w różnych centrach danych, odzyskiwania po awarii. Należy wdrożyć przy użyciu certyfikatów serwera, ponieważ domeny usługi active directory nie może obejmować wiele centrów danych.<br/>![Funkcja dublowania baz danych](./media/virtual-machines-windows-sql-high-availability-dr/azure_only_dr_dbmirroring.gif) |
| **Kopia zapasowa i przywracanie z usługi Magazyn obiektów Blob platformy Azure** |Produkcyjnych baz danych kopii zapasowej bezpośrednio tooblob magazynu w różnych centrach danych, odzyskiwania po awarii.<br/>![Tworzenie kopii zapasowej i przywracanie](./media/virtual-machines-windows-sql-high-availability-dr/azure_only_dr_backup_restore.gif)<br/>Aby uzyskać więcej informacji, zobacz [kopii zapasowej i przywracania dla programu SQL Server w usłudze Azure Virtual Machines](virtual-machines-windows-sql-backup-recovery.md). |

## <a name="hybrid-it-disaster-recovery-solutions"></a>Hybrydowego IT: Rozwiązania w zakresie odzyskiwania po awarii
Możesz mieć rozwiązanie odzyskiwania po awarii dla baz danych programu SQL Server w środowisku IT hybrydowych przy użyciu grup dostępności, dublowania bazy danych wysyłania dziennika i tworzenia kopii zapasowej i przywracanie z magazynem Azure blog.

| Technologia | Przykład architektury |
| --- | --- |
| **Grupy dostępności** |Niektóre repliki dostępności uruchomionych w maszynach wirtualnych platformy Azure i innych replik uruchamiane lokalnie do odzyskiwania po awarii między witrynami. Witaj lokacji produkcyjnej może być lokalnie lub w centrum danych Azure.<br/>![Grupy dostępności](./media/virtual-machines-windows-sql-high-availability-dr/hybrid_dr_alwayson.gif)<br/>Ponieważ wszystkie repliki dostępności muszą znajdować się w hello tego samego klastra pracy awaryjnej, hello klastra musi obejmować zarówno sieci (klastra trybu failover wielu podsieci). Ta konfiguracja wymaga połączenia sieci VPN między Azure i hello sieci lokalnej.<br/><br/>Pomyślnym awarii baz danych należy również zainstalować repliki kontrolera domeny w lokacji odzyskiwania po awarii hello.<br/><br/>Jest możliwe toouse hello Kreatora dodawania repliki w programie SSMS tooadd tooan Azure repliki istniejących zawsze włączonej grupy dostępności. Aby uzyskać więcej informacji, zobacz samouczek: rozszerzenie tooAzure Twojego zawsze włączonej grupy dostępności. |
| **Funkcja dublowania baz danych** |Jednego partnera działający w maszynie Wirtualnej platformy Azure i hello inne uruchomione w siedzibie firmy do odzyskiwania awaryjnego międzylokacyjnej przy użyciu certyfikatów serwera. Partnerzy nie ma potrzeby toobe w hello tej samej domeny usługi Active Directory, a żadne połączenie sieci VPN nie jest wymagane.<br/>![Funkcja dublowania baz danych](./media/virtual-machines-windows-sql-high-availability-dr/hybrid_dr_dbmirroring.gif)<br/>Innej bazy danych dublowania scenariusz obejmuje jednego partnera uruchomione w maszynie Wirtualnej platformy Azure i hello inne uruchomione lokalnie w hello sam domeny usługi Active Directory do odzyskiwania po awarii między witrynami. A [połączenia sieci VPN między hello Azure wirtualnych sieci i hello lokalnej sieci](../../../vpn-gateway/vpn-gateway-site-to-site-create.md) jest wymagana.<br/><br/>Pomyślnym awarii baz danych należy również zainstalować repliki kontrolera domeny w lokacji odzyskiwania po awarii hello. |
| **Wysyłanie dziennika** |Jeden serwer działający w maszynie Wirtualnej platformy Azure i hello inne uruchomione w siedzibie firmy do odzyskiwania po awarii między witrynami. Wysyłanie dziennika zależy od udostępnianie plików systemu Windows, więc połączenie sieci VPN między hello sieci wirtualnej platformy Azure i hello lokalnej sieci nie jest wymagane.<br/>![Wysyłanie dziennika](./media/virtual-machines-windows-sql-high-availability-dr/hybrid_dr_log_shipping.gif)<br/>Pomyślnym awarii baz danych należy również zainstalować repliki kontrolera domeny w lokacji odzyskiwania po awarii hello. |
| **Kopia zapasowa i przywracanie z usługi Magazyn obiektów Blob platformy Azure** |Lokalne produkcyjnych baz danych kopii zapasowej bezpośrednio tooAzure magazynu obiektów blob do odzyskiwania po awarii.<br/>![Tworzenie kopii zapasowej i przywracanie](./media/virtual-machines-windows-sql-high-availability-dr/hybrid_dr_backup_restore.gif)<br/>Aby uzyskać więcej informacji, zobacz [kopii zapasowej i przywracania dla programu SQL Server w usłudze Azure Virtual Machines](virtual-machines-windows-sql-backup-recovery.md). |

## <a name="important-considerations-for-sql-server-hadr-in-azure"></a>Ważne uwagi dotyczące HADR serwera SQL na platformie Azure
Maszyny wirtualne platformy Azure, magazynu i sieci charakteryzują się innymi cechami operacyjne, niż lokalne, niezwirtualizowanych infrastruktury IT. Pomyślne zaimplementowanie rozwiązania HADR programu SQL Server na platformie Azure wymaga opis tych różnic i projektowania tooaccommodate Twojego rozwiązania ich.

### <a name="high-availability-nodes-in-an-availability-set"></a>Węzły o wysokiej dostępności w zestawie dostępności
Zestawy dostępności w systemie Azure Włącz tooplace hello wysokiej dostępności węzłów w oddzielnych domen błędów (FDs) i aktualizację domeny (UDs). Dla maszyn wirtualnych Azure toobe umieszczone w hello sam zestaw dostępności, należy je wdrożyć w hello sama usługa w chmurze. Tylko węzły w powitalne tej samej usługi w chmurze mogą uczestniczyć w hello tego samego zestawu dostępności. Aby uzyskać więcej informacji, zobacz [hello Zarządzaj dostępność maszyn wirtualnych](../manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

### <a name="failover-cluster-behavior-in-azure-networking"></a>Zachowanie klastra pracy awaryjnej w sieci Azure
Hello nie zgodne ze standardem RFC usługi DHCP w usłudze Azure może spowodować utworzenie hello niektórych trybu failover klastra konfiguracje toofail, ponieważ nazwa sieciowa klastra toohello przypisywane zduplikowanego adresu IP, takich jak hello tego samego adresu IP adresów jako jeden z węzłów klastra hello. Jest to problem podczas implementowania grup dostępności, która jest zależna od funkcji klastra pracy awaryjnej systemu Windows hello.

Rozważmy scenariusz hello, podczas tworzenia klastra z dwoma węzłami i przełączony w tryb online:

1. klaster Hello przejściu do trybu online, a następnie NODE1 żądań przypisywany dynamicznie adres IP dla nazwy sieciowej klastra hello.
2. Żaden adres IP innego niż własny NODE1 adres IP jest określany przez hello usługi DHCP, ponieważ hello usługi DHCP rozpoznaje hello żądanie pochodzi z NODE1 samej siebie.
3. System Windows wykrywa, że zduplikowanego adresu przypisano zarówno tooNODE1 i toohello nazwy sieciowej klastra trybu failover, i hello domyślna grupa klastra toocome w trybie online nie powiodło się.
4. Witaj domyślna grupa klastra przenosi tooNODE2, który traktuje jako adres IP klastra hello NODE1 na adres IP i powoduje hello domyślne klastra grupy do trybu online.
5. Gdy NODE2 próbuje tooestablish łączność z Węzeł1, pakiety skierowany NODE1 nigdy nie opuszczają NODE2 ponieważ rozpoznawany tooitself adresów IP w NODE1. NODE2 nie może ustanowić połączenia z NODE1 następnie utraty kworum i zamyka hello klastra.
6. W międzyczasie hello NODE1 może wysyłać tooNODE2 pakietów, ale nie może wysłać odpowiedzi NODE2. Węzeł1 utraty kworum i zamyka hello klastra.

W tym scenariuszu można uniknąć, przypisując nieużywane statyczny adres IP, takie jak adres IP połączenia lokalnego, takie jak 169.254.1.1, Nazwa sieciowa klastra toohello w kolejności toobring hello Nazwa sieciowa klastra online. toosimplify to przetwarzania, zobacz [Windows konfigurowania klastra trybu failover na platformie Azure dla grup dostępności](http://social.technet.microsoft.com/wiki/contents/articles/14776.configuring-windows-failover-cluster-in-windows-azure-for-alwayson-availability-groups.aspx).

Aby uzyskać więcej informacji, zobacz [Konfigurowanie grup dostępności Azure (GUI)](virtual-machines-windows-portal-sql-alwayson-availability-groups.md).

### <a name="availability-group-listener-support"></a>Obsługa odbiornika grupy dostępności
Odbiorniki grupy dostępności są obsługiwane na maszynach wirtualnych Azure systemem Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2 i Windows Server 2016. Ta obsługa jest możliwe przez użycie hello punktów końcowych z równoważeniem obciążenia, włączone na maszynach wirtualnych Azure hello, które są węzłami grupy dostępności. Należy wykonać kroki specjalnej konfiguracji dla hello toowork odbiorników dla obu aplikacji klienckich, które są uruchomione w Azure, a także systemami lokalnymi.

Istnieją dwie główne opcje dotyczące konfigurowania programu odbiornika: zewnętrznych (publicznych) lub wewnętrzny. Witaj zewnętrznych (publicznych) odbiornika używa modułu równoważenia obciążenia z Internetem oraz jest skojarzony z publicznych wirtualnych IP (VIP), który jest dostępny za pośrednictwem hello internet. Odbiornik wewnętrzny używa wewnętrznego modułu równoważenia obciążenia i tylko obsługuje klientów w ramach hello tej samej sieci wirtualnej. W obu załadować typu modułu równoważenia, należy włączyć bezpośredniego zwrotu serwera. 

Jeśli grupy dostępności hello obejmujących wiele podsieci platformy Azure (na przykład wdrożenia, które przecina regiony platformy Azure), musi zawierać ciąg połączenia powitania klienta "**MultisubnetFailover = True**". Powoduje to połączenie równoległe prób toohello replik w różnych podsieciach hello. Aby uzyskać instrukcje na temat konfigurowania odbiornik zobacz

* [Skonfiguruj odbiornik ILB dla grupy dostępności na platformie Azure](virtual-machines-windows-portal-sql-ps-alwayson-int-listener.md).
* [Skonfiguruj odbiornik zewnętrzny dla grup dostępności w systemie Azure](../classic/ps-sql-ext-listener.md).

Replika dostępności tooeach można połączyć oddzielnie, bezpośrednio łącząc toohello wystąpienie usługi. Ponadto ponieważ grupy dostępności są zgodne z klientów dublowania bazy danych, możesz połączyć toohello repliki dostępności, takich jak dublowania partnerów tak długo, jak skonfigurowano hello repliki bazy danych podobny dublowania toodatabase:

* Jedna replika podstawowa i jedna replika pomocnicza
* Witaj replika pomocnicza została skonfigurowana jako bez możliwości odczytu (**czytelny dodatkowej** ustawienie zbyt**nr**)

Przykład parametry połączenia klienta, które odpowiada konfiguracji podobnych funkcji dublowania bazy danych toothis za pomocą ADO.NET lub SQL Server Native Client znajduje się poniżej:

    Data Source=ReplicaServer1;Failover Partner=ReplicaServer2;Initial Catalog=AvailabilityDatabase;

Aby uzyskać więcej informacji dotyczących łączności klienta Zobacz:

* [Przy użyciu słowa kluczowe parametrów połączenia w usłudze SQL Server Native Client](https://msdn.microsoft.com/library/ms130822.aspx)
* [Połączenia klientów tooa sesji dublowania bazy danych (SQL Server)](https://technet.microsoft.com/library/ms175484.aspx)
* [Łączenie tooAvailability odbiornika grupy w hybrydowego](http://blogs.msdn.com/b/sqlalwayson/archive/2013/02/14/connecting-to-availability-group-listener-in-hybrid-it.aspx)
* [Odbiorniki grupy dostępności, łączności klienta i pracy awaryjnej aplikacji (SQL Server)](https://technet.microsoft.com/library/hh213417.aspx)
* [Przy użyciu parametrów połączenia dublowania bazy danych z grupy dostępności](https://technet.microsoft.com/library/hh213417.aspx)

### <a name="network-latency-in-hybrid-it"></a>Opóźnienie sieci hybrydowy IT
Należy wdrożyć rozwiązanie HADR z hello założenie, że mogą być okresów z sieci wysokiego opóźnienia między siecią lokalną a Azure. Podczas wdrażania tooAzure repliki, należy użyć zatwierdzania asynchronicznego zamiast zatwierdzanie synchroniczne hello trybu synchronizacji. Podczas wdrażania serwerów dublowania bazy danych zarówno lokalnie i na platformie Azure, użyj trybu wysokiej wydajności hello zamiast trybu wysokiej bezpieczeństwa hello.

### <a name="geo-replication-support"></a>Replikacja geograficzna pomocy technicznej
Replikacja geograficzna, w przypadku dysków Azure nie obsługuje hello plik danych i plik dziennika dotyczący tej samej bazy danych toobe przechowywane na oddzielnych dyskach hello. GRS są replikowane zmian na każdym dysku niezależnie i asynchronicznie. Ten mechanizm gwarantuje kolejność zapisu hello w ramach jednego dysku na powitania kopiowania replikacją geograficzną, a nie na replikacją geograficzną kopie wiele dysków. Jeśli konfigurujesz toostore bazy danych, jego plików danych i jego pliku dziennika na oddzielnych dyskach, hello odzyskać dyski po awarii może zawierać aktualniejszej kopii pliku danych hello niż hello pliku dziennika, jakich hello zapisu z wyprzedzeniem dziennika w programie SQL Server i hello kwasu właściwości transakcji. Jeśli nie masz hello opcja toodisable — replikacja geograficzna hello konta magazynu, należy go przechowywać wszystkie dane i pliki dziennika określonej bazy danych na powitania sam dysku. Należy użyć więcej niż jednego dysku powodu toohello rozmiar hello bazy danych, należy najpierw toodeploy jednego rozwiązania w zakresie odzyskiwania po awarii hello powyższej tooensure nadmiarowość danych.

## <a name="next-steps"></a>Następne kroki
Jeśli potrzebujesz toocreate maszyny wirtualnej platformy Azure z programem SQL Server, zobacz [inicjowania obsługi maszyny wirtualnej programu SQL Server na platformie Azure](virtual-machines-windows-portal-sql-server-provision.md).

tooget hello najlepszą wydajność z programu SQL Server uruchomionego na maszynie Wirtualnej platformy Azure, zobacz wskazówki hello w [wydajności najlepsze rozwiązania dotyczące programu SQL Server w usłudze Azure Virtual Machines](virtual-machines-windows-sql-performance.md).

Dla innych tematach dotyczących toorunning programu SQL Server na maszynach wirtualnych Azure, zobacz [programu SQL Server na maszynach wirtualnych Azure](virtual-machines-windows-sql-server-iaas-overview.md).

### <a name="other-resources"></a>Inne zasoby
* [Instalowanie nowego lasu usługi Active Directory na platformie Azure](../../../active-directory/active-directory-new-forest-virtual-machine.md)
* [Tworzenie klastra trybu Failover dla grupy dostępności w maszynie Wirtualnej platformy Azure](http://gallery.technet.microsoft.com/scriptcenter/Create-WSFC-Cluster-for-7c207d3a)

