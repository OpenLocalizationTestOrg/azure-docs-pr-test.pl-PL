---
title: "aaaSet wysokiej dostępności dla maszyn wirtualnych platformy Azure Resource Manager | Dokumentacja firmy Microsoft"
description: "Ten samouczek pokazuje, jak toocreate dostępności zawsze włączone grupy z maszyn wirtualnych platformy Azure w trybie Azure Resource Manager."
services: virtual-machines-windows
documentationcenter: na
author: MikeRayMSFT
manager: jhubbard
editor: 
tags: azure-resource-manager
ms.assetid: 64e85527-d5c8-40d9-bbe2-13045d25fc68
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 03/17/2017
ms.author: mikeray
ms.openlocfilehash: 6f0a253d3502259a487e66fd62d92e41c379a6b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-always-on-availability-groups-in-azure-virtual-machines-automatically-resource-manager"></a>Konfigurowanie zawsze włączonych grup dostępności w maszynach wirtualnych platformy Azure automatycznie: Menedżer zasobów

Ten samouczek pokazuje, jak toocreate dostępności programu SQL Server grupy które używa maszyny wirtualne Azure Resource Manager. samouczku Hello Azure bloki tooconfigure szablonu. Można przejrzeć ustawienia domyślne hello, wpisz wymagane ustawienia i aktualizować hello bloków w portalu hello, zgodnie z wyświetlanymi w tym samouczku.

Samouczek pełną Hello tworzy grupy dostępności programu SQL Server na maszynach wirtualnych platformy Azure zawierających hello następujące elementy:

* Sieć wirtualna, która ma wiele podsieci, w tym frontonu i podsieci wewnętrznej bazy danych
* Dwa kontrolery domeny, które mają domenę usługi Active Directory
* Dwie maszyny wirtualne, uruchom program SQL Server, które są wdrożone toohello podsieci wewnętrznej bazy danych i toohello przyłączone do domeny usługi Active Directory
* Klaster trybu failover węzła trzech modelu kworum Większość węzłów hello
* Grupy dostępności, która ma dwa zatwierdzania synchronicznego repliki bazy danych dostępności

Witaj następującej ilustracji reprezentuje hello kompletnego rozwiązania.

![Architektura laboratorium testowego dla grup dostępności w systemie Azure](./media/virtual-machines-windows-portal-sql-alwayson-availability-groups/0-EndstateSample.png)

Wszystkie zasoby w tym rozwiązaniu należeć tooa pojedyncza grupa zasobów.

Przed rozpoczęciem tego samouczka, upewnij się, hello następujące czynności:

* Masz już konto platformy Azure. Jeśli nie masz, [Załóż konto próbne](http://azure.microsoft.com/pricing/free-trial/).
* Znasz już, jak toouse hello tooprovision graficznego interfejsu użytkownika maszyny wirtualnej programu SQL Server z hello galerii maszyn wirtualnych. Aby uzyskać więcej informacji, zobacz [obsługi maszyny wirtualnej programu SQL Server na platformie Azure](virtual-machines-windows-portal-sql-server-provision.md).
* Masz już pełny opis grup dostępności. Aby uzyskać więcej informacji, zobacz [zawsze włączonych grup dostępności (SQL Server)](http://msdn.microsoft.com/library/hh510230.aspx).

> [!NOTE]
> Jeśli interesuje Cię przy użyciu grup dostępności z programu SharePoint, zobacz też [konfigurowania programu SQL Server 2012 zawsze włączone grupy dostępności programu SharePoint 2013](http://technet.microsoft.com/library/jj715261.aspx).
>
>

W tym samouczku, użyj hello Azure portalu do:

* Wybierz hello zawsze na szablon z portalu hello.
* Przejrzyj ustawienia szablonu hello i zaktualizować kilka ustawień konfiguracji w danym środowisku.
* Azure monitora, ponieważ tworzy hello całego środowiska.
* Połącz tooa kontrolera domeny, a następnie tooa serwerze, na którym działa program SQL Server.

[!INCLUDE [availability-group-template](../../../../includes/virtual-machines-windows-portal-sql-alwayson-ag-template.md)]

## <a name="provision-hello-cluster-from-hello-gallery"></a>Zainicjuj obsługę hello klastra z galerii hello
Azure zapewnia obrazu galerii hello całego rozwiązania. Szablon hello toolocate:

1. Zaloguj się toohello portalu Azure przy użyciu swojego konta.
2. W portalu Azure hello, kliknij przycisk **+ nowy** tooopen hello **nowy** bloku.
3. Na powitania **nowy** bloku, wyszukiwanie **AlwaysOn**.
   ![Znajdź szablon (AlwaysOn)](./media/virtual-machines-windows-portal-sql-alwayson-availability-groups/16-findalwayson.png)
4. W wynikach wyszukiwania hello, Znajdź **klastra programu SQL Server AlwaysOn**.
   ![Szablon (AlwaysOn)](./media/virtual-machines-windows-portal-sql-alwayson-availability-groups/17-alwaysontemplate.png)
5. Na **wybierz model wdrożenia**, wybierz **Resource Manager**.

### <a name="basics"></a>Podstawy
Kliknij przycisk **podstawy** i skonfigurować hello następujące ustawienia:

* **Nazwa użytkownika administratora** jest konto użytkownika z uprawnieniami administratora domeny i jest członkiem hello programu SQL Server stałej roli serwera sysadmin na obu wystąpień programu SQL Server. W tym samouczku, użyj **administrator domeny**.
* **Hasło** jest hello hasło dla konta administratora domeny hello. Użyj złożone hasło. Potwierdź hasło hello.
* **Subskrypcja** subskrypcja hello czy Azure rachunków zasobów toorun wdrożona dla grupy dostępności hello. Jeśli konto ma wiele subskrypcji, możesz określić inną subskrypcję.
* **Grupa zasobów** jest nazwą hello toowhich grupy hello należą wszystkie zasoby platformy Azure, które zostały utworzone przy użyciu tego szablonu. W tym samouczku, użyj **SQL-HA-zarządcy zasobów**. Aby uzyskać więcej informacji, zobacz [Omówienie usługi Azure Resource Manager](../../../azure-resource-manager/resource-group-overview.md#resource-groups).
* **Lokalizacja** jest hello region platformy Azure, w którym samouczek hello tworzy hello zasobów. Wybierz region platformy Azure.

Witaj Poniższy zrzut ekranu jest wypełniony **podstawy** bloku:

![Podstawy](./media/virtual-machines-windows-portal-sql-alwayson-availability-groups/1-basics.png)

Kliknij przycisk **OK**.

### <a name="domain-and-network-settings"></a>Ustawienia domeny i sieci
Ten szablon galerii Azure tworzy kontrolery domeny i domeny. Tworzy także sieć z dwoma podsieciami. Witaj szablonu nie można utworzyć serwerów w istniejącej domenie lub sieci wirtualnej. następnym krokiem Hello konfiguruje hello ustawienia domeny i sieci.

Na powitania **ustawienia domeny i sieci** bloku, przejrzyj hello ustawienia wartości ustawień hello domeny i sieci:

* **Nazwa domeny głównej lasu** jest hello nazwę domeny dla domeny usługi Active Directory hello hello klastra hostów. Samouczek hello, użyj **contoso.com**.
* **Nazwa sieci wirtualnej** jest nazwą sieci hello hello sieci wirtualnej platformy Azure. Samouczek hello, użyj **autohaVNET**.
* **Nazwa podsieci kontrolera domeny** jest nazwą hello części sieci wirtualnej hello tego kontrolera domeny hello hostów. Użyj **podsieć 1**. Prefiks adresu używa tej podsieci **10.0.0.0/24**.
* **Nazwa podsieci programu SQL Server** jest nazwą hello części sieci wirtualnej hello hostów hello serwery programu SQL Server i plik hello monitor udostępniania. Użyj **2 podsieci**. Prefiks adresu używa tej podsieci **10.0.1.0/26**.

toolearn więcej informacji na temat sieci wirtualnych na platformie Azure, zobacz [omówienie sieci wirtualnej](../../../virtual-network/virtual-networks-overview.md).  

Witaj **ustawienia domeny i sieci** powinien wyglądać podobnie jak powitania po zrzut ekranu:

![Ustawienia domeny i sieci](./media/virtual-machines-windows-portal-sql-alwayson-availability-groups/2-domain.png)

W razie potrzeby można zmienić tych wartości. W tym samouczku, użyj wartości ustawienia wstępnego hello.

Przejrzyj ustawienia hello, a następnie kliknij przycisk **OK**.

### <a name="availability-group-settings"></a>Ustawienia grupy dostępności
Na **ustawienia grupy dostępności**, hello Przejrzyj ustawienia wartości dla grupy dostępności hello i hello odbiornika.

* **Nazwa grupy dostępności** to nazwa zasobu klastrowanego hello hello grupy dostępności. W tym samouczku, użyj **Contoso ag**.
* **Nazwa odbiornika grupy dostępności** jest używane przez klaster hello i hello wewnętrznego modułu równoważenia obciążenia. Klienci łączący tooSQL serwera można użyć tej nazwy tooconnect toohello odpowiednie repliki hello bazy danych. W tym samouczku, użyj **odbiornika Contoso**.
* **Port odbiornika grupy dostępności** Określa port TCP hello hello odbiornika programu SQL Server. W tym samouczku, użyj hello domyślnego portu, **1433**.

W razie potrzeby można zmienić tych wartości. W tym samouczku, użyj wartości ustawienia wstępnego hello.  

![Ustawienia grupy dostępności](./media/virtual-machines-windows-portal-sql-alwayson-availability-groups/3-availabilitygroup.png)

Kliknij przycisk **OK**.

### <a name="virtual-machine-size-storage-settings"></a>Rozmiar maszyny wirtualnej, ustawień magazynu
Na **rozmiar maszyny Wirtualnej, ustawienia magazynu**, wybierz rozmiar maszyny wirtualnej programu SQL Server i inne ustawienia hello przeglądu.

* **Rozmiar maszyny wirtualnej programu SQL Server** hello rozmiar dla maszyn wirtualnych, zarówno z programem SQL Server. Wybierz rozmiar odpowiedniej maszyny wirtualnej dla obciążenia. Jeśli tworzysz to środowisko hello samouczek, użyj **DS2**. Wybierz rozmiar maszyny wirtualnej, który może obsługiwać obciążenie hello obciążeń produkcyjnych. Wiele obciążeń produkcyjnych wymagają **DS4** lub większą. Szablon Hello tworzy dwie maszyny wirtualne o tym rozmiarze i instaluje program SQL Server w każdej z nich. Aby uzyskać więcej informacji, zobacz [rozmiary maszyn wirtualnych](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

> [!NOTE]
> Hello Azure powoduje zainstalowanie wersji Enterprise programu SQL Server. Koszt Hello zależy od wersji hello i hello rozmiar maszyny wirtualnej. Aby uzyskać szczegółowe informacje o bieżącym kosztów, zobacz [cennik maszyn wirtualnych](http://azure.microsoft.com/pricing/details/virtual-machines/#Sql).
>
>

* **Rozmiar maszyny wirtualnej kontrolera domeny** jest hello rozmiar maszyny wirtualnej dla hello kontrolerów domeny. Dla tego samouczka użyj **D2**.
* **Rozmiar maszyny wirtualnej monitora udostępniania plików** jest hello rozmiar maszyny wirtualnej dla monitora udziału plików hello. W tym samouczku, użyj **A1**.
* **Konto magazynu SQL** jest hello nazwę konta magazynu hello, który zawiera dane programu SQL Server hello i dysków systemu operacyjnego. W tym samouczku, użyj **alwaysonsql01**.
* **Konto magazynu DC** jest hello nazwę konta magazynu hello hello kontrolerów domeny. W tym samouczku, użyj **alwaysondc01**.
* **Rozmiar dysku danych programu SQL Server** TB jest hello rozmiar dysku danych programu SQL Server hello w TB. Określ liczbę z zakresu od 1 do 4. W tym samouczku, użyj **1**.
* **Optymalizacja magazynu** Ustawia ustawienia konfiguracji określonego magazynu dla maszyn wirtualnych programu SQL Server hello na podstawie typu obciążenia hello. Wszystkie maszyny wirtualne programu SQL Server, w tym scenariuszu za pomocą magazyn w warstwie premium ustawione jako tylko do tooread hosta dysku platformy Azure w pamięci podręcznej. Ponadto można zoptymalizować ustawienia programu SQL Server dla obciążeń hello, wybierając jedną z tych trzech ustawień:

  * **Ogólne obciążenie** ustawia nie określonych ustawień konfiguracji.
  * **Przetwarzania transakcyjnego** zestawy śledzenie flagę 1117 i 1118.
  * **Magazynowanie danych** zestawy śledzenie flagę 1117 i 610.

W tym samouczku, użyj **ogólne obciążenie**.

![Ustawienia magazynu rozmiar maszyny Wirtualnej](./media/virtual-machines-windows-portal-sql-alwayson-availability-groups/4-vm.png)

Przejrzyj ustawienia hello, a następnie kliknij przycisk **OK**.

#### <a name="a-note-about-storage"></a>Uwagi dotyczące magazynu
Dodatkowe optymalizacje zależą od rozmiaru hello hello dysków z danymi programu SQL Server. Dla każdego terabajt dysku danych Azure dodaje dodatkowego magazynu premium 1 TB. Jeśli serwer wymaga 2 TB lub więcej, hello szablonu powoduje utworzenie puli magazynu na każdej maszynie wirtualnej programu SQL Server. Puli magazynu jest formą wirtualizacji pamięci masowej, gdzie wiele dysków są skonfigurowane tooprovide lepszą wydajność, odporności i wydajności.  Szablon Hello następnie tworzy miejsca do magazynowania w puli magazynu hello i przedstawia informacje o danych jednego dysku toohello serwerowym systemem operacyjnym. Szablon Hello określa ten dysk jako dysk danych hello dla programu SQL Server. Szablon Hello Dostraja hello puli magazynu dla programu SQL Server przy użyciu hello następujące ustawienia:

* Rozmiar usługi STRIPE to hello interleave ustawienie hello dysku wirtualnego. Obciążeń transakcyjnych użyj 64 KB. Obciążeń magazynowania danych użyj 256 KB.
* Odporność jest prosty (Brak odporności).

> [!NOTE]
> Magazyn w warstwie premium systemu Azure jest magazyn lokalnie nadmiarowy i przechowuje trzy kopie danych hello w pojedynczym regionie, dlatego dodatkowe odporności na powitania puli magazynu nie jest wymagane.
>
>

* Liczba kolumn jest równe hello liczby dysków w puli magazynu hello.

Aby uzyskać dodatkowe informacje na temat miejsca do magazynowania i pule magazynu zobacz:

* [Omówienie funkcji miejsca do magazynowania](http://technet.microsoft.com/library/hh831739.aspx)
* [Kopia zapasowa systemu Windows Server i pule magazynu](http://technet.microsoft.com/library/dn390929.aspx)

Aby uzyskać więcej informacji o najlepszych rozwiązaniach konfiguracji programu SQL Server, zobacz [wydajności najlepsze rozwiązania dotyczące programu SQL Server na maszynach wirtualnych Azure](virtual-machines-windows-sql-performance.md).

### <a name="sql-server-settings"></a>Ustawienia programu SQL Server
Na **ustawienia programu SQL Server**Przejrzyj i zmodyfikuj prefiks nazwy maszyny wirtualnej programu SQL Server hello, wersja programu SQL Server, konto usługi serwera SQL i hasło, a hello harmonogramu konserwacji automatyczne stosowanie poprawek SQL.

* **Prefiks nazwy serwera SQL** jest używane toocreate nazwą dla każdej maszyny wirtualnej programu SQL Server. W tym samouczku, użyj **sqlserver**. Witaj szablon nazwy hello maszyn wirtualnych programu SQL Server *sqlserver 0* i *sqlserver 1*.
* **Wersja programu SQL Server** jest hello wersji programu SQL Server. Dla tego samouczka użyj **programu SQL Server 2014**. Można również wybrać **programu SQL Server 2012** lub **programu SQL Server 2016**.
* **Nazwa użytkownika konta usługi programu SQL Server** to nazwa konta domeny hello hello usługi SQL Server. W tym samouczku, użyj **SQL Service**.
* **Hasło** jest hasło hello hello konto usługi programu SQL Server.  Użyj złożone hasło. Potwierdź hasło hello.
* **Automatyczne stosowanie poprawek SQL harmonogramu konserwacji** identyfikuje hello dzień tygodnia hello czy Azure automatycznie poprawek hello serwerów SQL. W tym samouczku, wpisz **niedziela**.
* **Godzina rozpoczęcia konserwacji automatyczne stosowanie poprawek SQL** jest godzinę hello hello region platformy Azure, po rozpoczęciu automatyczne stosowanie poprawek.

> [!NOTE]
> Witaj poprawki okna dla każdej maszyny wirtualnej jest rozłożona przez jedną godzinę. Tylko jedna maszyna wirtualna jest poprawiono w czasie tooprevent zakłócenia usługi.
>
>

![Ustawienia programu SQL Server](./media/virtual-machines-windows-portal-sql-alwayson-availability-groups/5-sql.png)

Przejrzyj ustawienia hello, a następnie kliknij przycisk **OK**.

### <a name="summary"></a>Podsumowanie
Na stronie Podsumowanie hello Azure sprawdza ustawienia hello. Możesz również pobrać hello szablonu. Witaj Przejrzyj podsumowania. Kliknij przycisk **OK**.

### <a name="buy"></a>Kup
Ten blok końcowy zawiera **warunki użytkowania**, i **zasady zachowania poufności informacji**. Przejrzyj te informacje. Gdy wszystko będzie gotowe do maszyn wirtualnych systemu Azure toostart toocreate hello i hello wszystkich innych wymaganych zasobów dla grupy dostępności hello, kliknij przycisk **Utwórz**.

Witaj portalu Azure tworzy hello grupy zasobów i wszystkie zasoby hello.

## <a name="monitor-deployment"></a>Monitor wdrażania
Monitorować postęp wdrażania hello hello portalu Azure. Ikona reprezentuje hello wdrożenia jest automatycznie przypiętych toohello pulpitu nawigacyjnego portalu Azure.

![Pulpit nawigacyjny platformy Azure](./media/virtual-machines-windows-portal-sql-alwayson-availability-groups/11-deploydashboard.png)

## <a name="connect-toosql-server"></a>Połącz tooSQL serwera
Hello nowe wystąpienia programu SQL Server są uruchomione na maszynach wirtualnych mających podłączonej do Internetu adresów IP. Możesz zdalnego pulpitu (RDP) bezpośrednio tooeach maszyny wirtualnej SQL Server.

tooa tooRDP programu SQL Server, wykonaj następujące kroki:

1. Z hello pulpitu nawigacyjnego portalu Azure Sprawdź, czy wdrożenie hello zakończyła się pomyślnie.
2. Kliknij przycisk **zasobów**.
3. W hello **zasobów** bloku, kliknij przycisk **sqlserver 0**, która jest nazwą komputera hello jednego hello maszyn wirtualnych, które działa program SQL Server.
4. W bloku hello **sqlserver 0**, kliknij przycisk **Connect**. Przeglądarka zapyta, jeśli chcesz tooopen lub zapisać hello obiektu połączenia zdalnego. Kliknij przycisk **Otwórz**.
5. **Podłączanie pulpitu zdalnego** może wyświetlić ostrzeżenie przed tym hello nie można zidentyfikować wydawcy tego połączenia zdalnego. Kliknij przycisk **Połącz**.
6. Zabezpieczenia systemu Windows monituje możesz tooenter Twoje poświadczenia tooconnect toohello adres IP hello podstawowego kontrolera domeny. Kliknij przycisk **Użyj innego konta**. Aby uzyskać **nazwy użytkownika**, typ **contoso\DomainAdmin**. To konto jest skonfigurowane, gdy nazwa użytkownika administratora hello jest ustawiona w szablonie hello. Użyj hello złożone hasło wybrany podczas konfigurowania hello szablonu.
7. **Pulpit zdalny** może ostrzeżenie, że na komputerze zdalnym hello nie można uwierzytelnić z powodu tooproblems z jego certyfikatem zabezpieczeń. Przedstawia on nazwę certyfikatu zabezpieczeń hello. Po wykonaniu samouczek hello nazwa hello jest **sqlserver 0.contoso.com**. Kliknij przycisk **tak**.

Teraz masz połączenie z maszyną wirtualną programu SQL Server toohello RDP. Można Otwórz program SQL Server Management Studio, połączenie toohello domyślnego wystąpienia programu SQL Server i sprawdź, czy skonfigurowano hello grupy dostępności.
