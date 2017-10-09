---
title: "aaaCreate odbiornika grupy dostępności programu SQL Server na maszynach wirtualnych platformy Azure | Dokumentacja firmy Microsoft"
description: "Instrukcje krok po kroku dotyczące tworzenia odbiornika dla grupy dostępności AlwaysOn dla programu SQL Server na maszynach wirtualnych Azure"
services: virtual-machines
documentationcenter: na
author: MikeRayMSFT
manager: jhubbard
editor: monicar
ms.assetid: d1f291e9-9af2-41ba-9d29-9541e3adcfcf
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 05/01/2017
ms.author: mikeray
ms.openlocfilehash: c6a44dc5c7c18b572c2bf5772b4651b7210aacbd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-load-balancer-for-an-always-on-availability-group-in-azure"></a>Konfigurowanie usługi równoważenia obciążenia zawsze włączonej grupy dostępności na platformie Azure
W tym artykule opisano, jak toocreate modułu równoważenia obciążenia dla programu SQL Server zawsze włączone grupy dostępności na platformie Azure wirtualnego maszynami, na których działają z usługą Azure Resource Manager. Grupy dostępności wymaga usługi równoważenia obciążenia w przypadku hello wystąpień programu SQL Server na maszynach wirtualnych Azure. Moduł równoważenia obciążenia Hello przechowuje hello adresu IP dla odbiornika grupy dostępności hello. Jeśli grupy dostępności obejmuje wielu regionach, każdy region musi modułu równoważenia obciążenia.

toocomplete to zadanie należy toohave wdrożone grupy dostępności programu SQL Server na maszynach wirtualnych Azure, których są uruchomione za pomocą Menedżera zasobów. Maszyny wirtualne zarówno programu SQL Server, trzeba należeć toohello tego samego zestawu dostępności. Można użyć hello [szablonów Microsoft](virtual-machines-windows-portal-sql-alwayson-availability-groups.md) tooautomatically utworzyć grupy dostępności hello w Menedżerze zasobów. Ten szablon automatycznie utworzy wewnętrznego modułu równoważenia obciążenia. 

Jeśli wolisz, możesz [ręcznie skonfigurować grupę dostępności](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md).

W tym artykule wymaga już skonfigurowania grup dostępności.  

Tematy pokrewne obejmują:

* [Konfigurowanie zawsze włączonych grup dostępności maszyny Wirtualnej Azure (GUI)](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md)   
* [Konfigurowanie połączenia do wirtualnymi przy użyciu usługi Azure Resource Manager i programu PowerShell](../../../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md)

Instruktaż w tym artykule, możesz utworzyć i skonfigurowania funkcji równoważenia obciążenia w hello portalu Azure. Po ukończeniu procesu hello skonfigurujesz hello adres IP hello toouse klastra z hello modułu równoważenia obciążenia dla odbiornika grupy dostępności hello.

## <a name="create-and-configure-hello-load-balancer-in-hello-azure-portal"></a>Tworzenie i konfigurowanie usługi równoważenia obciążenia hello w hello portalu Azure
W tej części zadań hello hello następujące:

1. W portalu Azure hello Utwórz hello modułu równoważenia obciążenia i skonfiguruj hello adres IP.
2. Skonfiguruj pulę zaplecza hello.
3. Utwórz hello sondowania. 
4. Ustaw reguły równoważenia obciążenia hello.

> [!NOTE]
> Jeśli hello wystąpień programu SQL Server znajdują się w wielu grup zasobów i regionów, wykonać każdy krok dwa razy, raz w każdej grupie zasobów.
> 
> 

### <a name="step-1-create-hello-load-balancer-and-configure-hello-ip-address"></a>Krok 1: Tworzenie usługi równoważenia obciążenia hello i skonfiguruj hello adres IP
Najpierw utwórz hello modułu równoważenia obciążenia. 

1. Hello portalu Azure Otwórz hello grupę zasobów, która zawiera maszyny wirtualne hello programu SQL Server. 

2. Witaj w grupie zasobów, kliknij przycisk **Dodaj**.

3. Wyszukaj **modułu równoważenia obciążenia** , a następnie w wynikach wyszukiwania hello, wybierz **moduł równoważenia obciążenia**, opublikowana przez **Microsoft**.

4. Na powitania **modułu równoważenia obciążenia** bloku, kliknij przycisk **Utwórz**.

5. W hello **modułu równoważenia obciążenia Utwórz** okna dialogowego Skonfiguruj hello modułu równoważenia obciążenia w następujący sposób:

   | Ustawienie | Wartość |
   | --- | --- |
   | **Nazwa** |Nazwa tekst reprezentujący hello modułu równoważenia obciążenia. Na przykład **sqlLB**. |
   | **Typ** |**Wewnętrzny**: większości wdrożeń używać wewnętrznego modułu równoważenia obciążenia, dzięki czemu aplikacji w obrębie hello tej samej sieci wirtualnej tooconnect toohello grupy dostępności.  </br> **Zewnętrzne**: umożliwia aplikacji tooconnect toohello dostępności grupy za pośrednictwem publicznego połączenia internetowego. |
   | **Sieć wirtualna** |Wybierz hello sieci wirtualnej hello intances programu SQL Server znajdują się w. |
   | **Podsieć** |Wybierz podsieć hello hello wystąpień programu SQL Server znajdują się w. |
   | **Przypisywanie adresów IP** |**Statyczne** |
   | **Prywatny adres IP** |Podaj dostępny adres IP z podsieci hello. Podczas tworzenia klastra hello odbiornik, należy użyć tego adresu IP. W skrypcie programu PowerShell w dalszej części tego artykułu, użyj tego samego adresu dla hello `$ILBIP` zmiennej. |
   | **Subskrypcja** |Jeśli masz wiele subskrypcji, w tym polu może być wyświetlany. Wybierz subskrypcję hello, które mają tooassociate z tego zasobu. Jego jest zwykle hello tej samej subskrypcji wszystkich zasobów hello hello grupy dostępności. |
   | **Grupa zasobów** |Wybierz grupę zasobów hello hello wystąpień programu SQL Server znajdują się w. |
   | **Lokalizacja** |Wybierz hello Azure hello wystąpień programu SQL Server znajdują się w lokalizacji. |

6. Kliknij przycisk **Utwórz**. 

Platforma Azure tworzy hello modułu równoważenia obciążenia. Moduł równoważenia obciążenia Hello należy tooa określoną sieć, podsieci, lokalizacji i grupy zasobów. Po zakończeniu zadania hello Azure Sprawdź ustawienia usługi równoważenia obciążenia hello na platformie Azure. 

### <a name="step-2-configure-hello-back-end-pool"></a>Krok 2: Konfigurowanie puli zaplecza hello
Pula adresów zaplecza hello Azure wywołania *puli zaplecza*. W takim przypadku pula zaplecza hello jest adresy hello hello dwóch wystąpień programu SQL Server w grupie dostępności. 

1. W grupie zasobów kliknij przycisk hello równoważenia obciążenia, który został utworzony. 

2. Na **ustawienia**, kliknij przycisk **pul zaplecza**.

3. Na **pul zaplecza**, kliknij przycisk **Dodaj** toocreate puli adresów zaplecza. 

4. Na **Dodaj pulę zaplecza**w obszarze **nazwa**, wpisz nazwę puli zaplecza hello.

5. W obszarze **maszyn wirtualnych**, kliknij przycisk **Dodaj maszynę wirtualną**. 

6. W obszarze **wybierz maszyny wirtualne**, kliknij przycisk **wybierz zestaw dostępności**, a następnie określ, że maszyny wirtualne hello programu SQL Server należy do zestawu danych o dostępności hello.

7. Po wybraniu zestawu dostępności powitania kliknij **wybierz maszyny wirtualne hello**, wybierz Witaj dwie maszyny wirtualne, które hello wystąpień programu SQL Server w grupie dostępności hello hosta, a następnie kliknij przycisk **wybierz**. 

8. Kliknij przycisk **OK** tooclose hello bloków dla **wybierz maszyny wirtualne**, i **Dodaj pulę zaplecza**. 

Azure aktualizuje ustawienia hello hello puli adresów zaplecza. Zestaw dostępności ma teraz puli dwa wystąpienia programu SQL Server.

### <a name="step-3-create-a-probe"></a>Krok 3: Tworzenie sondę
Sonda Hello definiuje sposób Azure sprawdza, które hello wystąpień programu SQL Server jest bieżącym właścicielem odbiornika grupy dostępności hello. Azure sondy hello usługi na podstawie adresu IP hello na porcie definiowany podczas tworzenia hello sondowania.

1. Moduł równoważenia obciążenia na powitania **ustawienia** bloku, kliknij przycisk **sondy kondycji**. 

2. Na powitania **sondy kondycji** bloku, kliknij przycisk **Dodaj**.

3. Skonfiguruj sondowania hello na powitania **sondowania Dodaj** bloku. Użyj hello następujące wartości tooconfigure hello sondowania:

   | Ustawienie | Wartość |
   | --- | --- |
   | **Nazwa** |Nazwa tekst reprezentujący hello sondowania. Na przykład **SQLAlwaysOnEndPointProbe**. |
   | **Protokół** |**TCP** |
   | **Port** |Umożliwia dowolny dostępny port. Na przykład *59999*. |
   | **Interwał** |*5* |
   | **Próg złej kondycji** |*2* |

4.  Kliknij przycisk **OK**. 

> [!NOTE]
> Upewnij się, że port hello określony jest otwarty na zaporze hello obu wystąpień programu SQL Server. Oba wystąpienia wymagają regułę ruchu przychodzącego dla portu TCP, którego używasz hello. Aby uzyskać więcej informacji, zobacz [Dodawanie lub edytowanie reguły zapory](http://technet.microsoft.com/library/cc753558.aspx). 
> 
> 

Azure tworzy badanie hello i używa go po wystąpieniu programu SQL Server, z którym ma hello odbiornika dla grupy dostępności hello tootest.

### <a name="step-4-set-hello-load-balancing-rules"></a>Krok 4: Ustaw reguły równoważenia obciążenia hello
reguły równoważenia obciążenia Hello skonfigurować sposób hello load balancer kieruje wystąpień programu SQL Server toohello ruchu. Ten moduł równoważenia obciążenia istnieje, włączyć bezpośredni zwrot serwera ponieważ tylko jeden z dwóch wystąpień programu SQL Server hello jest właścicielem zasobu odbiornika grupy dostępności hello naraz.

1. Moduł równoważenia obciążenia na powitania **ustawienia** bloku, kliknij przycisk **reguły równoważenia obciążenia**. 

2. Na powitania **reguły równoważenia obciążenia** bloku, kliknij przycisk **Dodaj**.

3. Na powitania **reguły równoważenia obciążenia Dodaj** bloku, skonfiguruj regułę równoważenia obciążenia hello. Użyj hello następujące ustawienia: 

   | Ustawienie | Wartość |
   | --- | --- |
   | **Nazwa** |Nazwa tekst reprezentujący reguły równoważenia obciążenia hello. Na przykład **SQLAlwaysOnEndPointListener**. |
   | **Protokół** |**TCP** |
   | **Port** |*1433* |
   | **Port zaplecza** |*1433*. Ta wartość jest ignorowana, ponieważ ta zasada używa **pływającego adresu IP (bezpośredni zwrot serwera)**. |
   | **Sondy** |Użyj nazwy hello hello sondy utworzonego dla tej usługi równoważenia obciążenia. |
   | **Trwałość sesji** |**Brak** |
   | **Limit czasu bezczynności (w minutach)** |*4* |
   | **Zmienny adres IP (bezpośredni zwrot serwera)** |**Włączone** |

   > [!NOTE]
   > Konieczne może być wszystkie ustawienia hello tooscroll dół hello tooview bloku.
   > 

4. Kliknij przycisk **OK**. 
5. Azure konfiguruje reguły równoważenia obciążenia hello. Teraz hello modułu równoważenia obciążenia jest wystąpienie programu SQL Server toohello ruchu tooroute skonfigurowany, obsługującym hello odbiornika dla grupy dostępności hello. 

W tym momencie hello grupa zasobów ma równoważenia obciążenia, który łączy tooboth maszyny programu SQL Server. usługi równoważenia obciążenia Hello zawiera także adresu IP hello programu SQL Server AlwaysOn odbiornika grupy dostępności, dzięki czemu maszyna może odpowiadać toorequests dla grup dostępności hello.

> [!NOTE]
> W przypadku wystąpienia programu SQL Server w dwóch oddzielnych regionach, powtórz kroki hello w hello inny region. Każdy region wymaga usługi równoważenia obciążenia. 
> 
> 

## <a name="configure-hello-cluster-toouse-hello-load-balancer-ip-address"></a>Skonfiguruj adres IP usługi równoważenia obciążenia hello hello klastra toouse
następnym krokiem Hello odbiornik hello tooconfigure w klastrze hello, a następnie przełącz odbiornika hello w trybie online. Witaj, po: 

1. Tworzenie odbiornika grupy dostępności hello na powitania klastra pracy awaryjnej. 

2. Przełącz odbiornika hello w trybie online.

### <a name="step-5-create-hello-availability-group-listener-on-hello-failover-cluster"></a>Krok 5: Tworzenie odbiornika grupy dostępności hello w klastrze trybu failover hello
W tym kroku ręcznie utworzyć hello odbiornika grupy dostępności w Menedżerze klastra trybu Failover i SQL Server Management Studio.

[!INCLUDE [ag-listener-configure](../../../../includes/virtual-machines-ag-listener-configure.md)]

### <a name="verify-hello-configuration-of-hello-listener"></a>Sprawdź konfigurację hello hello odbiornika

Zasoby klastra hello i zależności są poprawnie skonfigurowane, należy tooview stanie hello odbiornika w programie SQL Server Management Studio. tooset hello port odbiornika, hello następujące:

1. Uruchom program SQL Server Management Studio, a następnie połącz toohello repliki podstawowej.

2. Przejdź za**wysokiej dostępności funkcji AlwaysOn** > **grup dostępności** > **odbiorniki grupy dostępności**.  
    Powinna zostać wyświetlona nazwa odbiornika hello utworzonego w Menedżerze klastra trybu Failover. 

3. Kliknij prawym przyciskiem myszy nazwę odbiornika hello, a następnie kliknij przycisk **właściwości**.

4. W hello **portu** Określ numer portu odbiornika grupy dostępności hello hello przy użyciu hello $EndpointPort używany w starszych (1433 była hello domyślna), a następnie kliknij przycisk **OK**.

Masz teraz grupy dostępności na maszynach wirtualnych Azure działających w trybie Menedżera zasobów. 

## <a name="test-hello-connection-toohello-listener"></a>Odbiornik toohello połączenia hello testu
Testuj połączenie hello hello następujący:

1. Wystąpienie programu SQL Server tooa RDP, który znajduje się w hello sam wirtualnych sieci, ale nie nie własnych hello repliki. Ten serwer może hello inne wystąpienie programu SQL Server w klastrze hello.

2. Użyj **sqlcmd** narzędzie tootest hello połączenia. Na przykład ustanawia hello następującego skryptu **sqlcmd** repliki podstawowej toohello połączenia za pośrednictwem hello odbiornika z uwierzytelnianiem systemu Windows:
   
        sqlcmd -S <listenerName> -E

Witaj połączenia SQLCMD automatycznie łączy toohello wystąpienia programu SQL Server, który obsługuje replikę podstawową hello. 

## <a name="create-an-ip-address-for-an-additional-availability-group"></a>Utwórz adres IP dla grupy dostępności dodatkowe

Każda grupa dostępności używa oddzielnych odbiornika. Każdy odbiornika ma swój własny adres IP. Użyj hello sam załadować adres IP hello toohold równoważenia dla dodatkowych odbiorników. Po utworzeniu grupy dostępności, Dodaj usługi równoważenia obciążenia toohello adres IP hello, a następnie skonfiguruj hello odbiornika.

tooadd IP address tooa modułu równoważenia obciążenia z hello portalu Azure, hello następujące:

1. W portalu Azure hello Otwórz hello grupę zasobów, która zawiera hello modułu równoważenia obciążenia, a następnie kliknij hello modułu równoważenia obciążenia. 

2. W obszarze **ustawienia**, kliknij przycisk **puli adresów IP frontonu**, a następnie kliknij przycisk **Dodaj**. 

3. W obszarze **Dodaj adres IP frontonu**, Przypisz nazwę hello frontonu. 

4. Sprawdź, że hello **sieci wirtualnej** i hello **podsieci** są hello tak samo jak hello wystąpień programu SQL Server.

5. Ustawienie hello adresu IP dla odbiornika hello. 
   
   >[!TIP]
   >Można ustawić toostatic adres IP hello i wpisz adres, który nie jest obecnie używana w hello podsieci. Alternatywnie można ustawić toodynamic adres IP hello i zapisać puli nowego adresu IP frontonu hello. Po wykonaniu tej hello portalu Azure automatycznie przypisuje dostępną pulę toohello adresów IP. Następnie można ponownie otworzyć puli adresów IP frontonu hello i zmienić hello toostatic przypisania. 

6. Zapisz hello adresu IP dla odbiornika hello. 

7. Dodaj sondy kondycji za pomocą hello następujące ustawienia:

   |Ustawienie |Wartość
   |:-----|:----
   |**Nazwa** |Badanie hello tooidentify nazwy.
   |**Protokół** |TCP
   |**Port** |Nieużywany port TCP, które muszą być dostępne na wszystkich maszynach wirtualnych. Nie można używać do innych celów. Nie dwa odbiorniki służy hello sam sondowania portu. 
   |**Interwał** |próbuje Hello ilość czasu między sondowania. Użyj domyślnej hello [5].
   |**Próg złej kondycji** |Liczba Hello kolejnych progów, które powinno zakończyć się niepowodzeniem przed maszyny wirtualnej jest określana jako zła.

8. Kliknij przycisk **OK** toosave hello sondowania. 

9. Utwórz regułę równoważenia obciążenia. Kliknij przycisk **reguły równoważenia obciążenia**, a następnie kliknij przycisk **Dodaj**.

10. Skonfiguruj hello nowe równoważenia obciążenia reguły za pomocą hello następujące ustawienia:

   |Ustawienie |Wartość
   |:-----|:----
   |**Nazwa** |Witaj tooidentify nazwa załadować reguły równoważenia. 
   |**Adres IP frontonu** |Wybierz hello adresu IP, który został utworzony. 
   |**Protokół** |TCP
   |**Port** |Użyj wystąpienia programu SQL Server hello jest używany port hello. Domyślne wystąpienie korzysta z portu 1433, chyba że zostało zmienione. 
   |**Port zaplecza** |Użyj hello samą wartość jak **portu**.
   |**Puli wewnętrznej bazy danych** |Pula Hello zawierający hello maszyn wirtualnych z hello wystąpień programu SQL Server. 
   |**Badania kondycji** |Wybierz sondowania hello, który został utworzony.
   |**Trwałość sesji** |Brak
   |**Limit czasu bezczynności (w minutach)** |Domyślne (4)
   |**Zmienny adres IP (bezpośredni zwrot serwera)** | Enabled (Włączony)

### <a name="configure-hello-availability-group-toouse-hello-new-ip-address"></a>Skonfiguruj hello dostępności grupy toouse hello nowego adresu IP

toofinish Konfigurowanie klastra hello hello powtarzania czynności, które należy przestrzegać podczas wprowadzone hello pierwszej grupy dostępności. Oznacza to, skonfiguruj hello [toouse hello nowy adres IP klastra](#configure-the-cluster-to-use-the-load-balancer-ip-address). 

Po dodaniu adresu IP dla odbiornika hello, należy skonfigurować grupę dostępności dodatkowe hello hello następujący: 

1. Sprawdź, czy port sondy hello hello nowy adres IP jest otwarty na obu maszynach wirtualnych programu SQL Server. 

2. [W Menedżerze klastra Dodaj punkt dostępu klienta hello](#addcap).

3. [Skonfiguruj hello IP zasobu dla grupy dostępności hello](#congroup).

   >[!IMPORTANT]
   >Podczas tworzenia hello adresu IP, należy użyć adresu IP hello dodania toohello modułu równoważenia obciążenia.  

4. [Skonfiguruj zasób grupy dostępności programu SQL Server hello zależał od punktu dostępu klienta hello](#dependencyGroup).

5. [Dostępu powitania klienta do punktu zasobów zależnych od adresu IP hello](#listname).
 
6. [Ustaw parametry klastra hello w programie PowerShell](#setparam).

Po skonfigurowaniu hello dostępności grupy toouse hello nowego adresu IP, należy skonfigurować hello połączenia toohello odbiornika. 

## <a name="next-steps"></a>Następne kroki

- [Konfigurowanie programu SQL Server zawsze włączonej grupy dostępności na maszynach wirtualnych Azure w różnych regionach](virtual-machines-windows-portal-sql-availability-group-dr.md)
