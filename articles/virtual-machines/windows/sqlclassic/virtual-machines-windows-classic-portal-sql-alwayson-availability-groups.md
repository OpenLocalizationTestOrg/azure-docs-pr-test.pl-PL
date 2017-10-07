---
title: "aaaConfigure zawsze włączone grupy dostępności w maszynach wirtualnych platformy Azure (klasyczne) | Dokumentacja firmy Microsoft"
description: "Utwórz zawsze włączonej grupy dostępności o maszynach wirtualnych platformy Azure. Ten samouczek używa głównie hello interfejsu użytkownika i narzędzia zamiast skryptów."
services: virtual-machines-windows
documentationcenter: na
author: MikeRayMSFT
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 8d48a3d2-79f8-4ab0-9327-2f30ee0b2ff1
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 03/17/2017
ms.author: mikeray
ms.openlocfilehash: f428ad994a55378c281c959f4696fdcaf50632b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-always-on-availability-group-in-azure-virtual-machines-classic"></a>Konfigurowanie zawsze włączonej grupy dostępności w maszynach wirtualnych platformy Azure (klasyczne)
> [!div class="op_single_selector"]
> * [Klasycznym: interfejsu użytkownika](../classic/portal-sql-alwayson-availability-groups.md)
> * [Klasycznym: środowiska PowerShell](../classic/ps-sql-alwayson-availability-groups.md)
<br/>

Przed rozpoczęciem należy wziąć pod uwagę może teraz ukończyć tego zadania w modelu usługi Azure Resource Manager. Firma Microsoft zaleca modelu usługi Azure Resource Manager dla nowych wdrożeń. Zobacz [programu SQL Server zawsze włączonych grup dostępności na maszynach wirtualnych Azure](../sql/virtual-machines-windows-portal-sql-availability-group-overview.md).

> [!IMPORTANT] 
> Firma Microsoft zaleca, aby większości nowych wdrożeń korzystać hello modelu Resource Manager. Platforma Azure ma dwa inne wdrożenie toocreate modeli i pracy z zasobami: [Resource Manager i Model Klasyczny](../../../azure-resource-manager/resource-manager-deployment-model.md). W tym artykule opisano, jak toouse hello klasycznego modelu wdrażania. 

Zobacz to zadanie z modelem usługi Azure Resource Manager hello toocomplete [programu SQL Server zawsze włączonych grup dostępności na maszynach wirtualnych Azure](../sql/virtual-machines-windows-portal-sql-availability-group-overview.md).

W tym samouczku end-to-end przedstawiono, jak grup dostępności tooimplement przy użyciu programu SQL Server zawsze na uruchomione na maszynach wirtualnych platformy Azure.

Końcem hello samouczka hello rozwiązania programu SQL Server zawsze na platformie Azure będzie składać się z hello następujące elementy:

* Sieć wirtualna, która zawiera wiele podsieci i frontonu i podsieci wewnętrznej bazy danych
* Kontroler domeny z domeny usługi Active Directory (Azure AD)
* Dwie maszyny wirtualne, uruchom program SQL Server, które są wdrożone toohello podsieci wewnętrznej bazy danych i domeny toohello dołączonego do usługi Azure AD
* Klaster trybu failover węzła trzech modelu kworum Większość węzłów hello
* Grupy dostępności, która ma dwa zatwierdzania synchronicznego repliki bazy danych dostępności

Witaj następującej ilustracji jest graficzną reprezentację hello rozwiązania.

![Architektura laboratorium testowego dla grup dostępności w systemie Azure](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC791912.png)

Należy pamiętać, że jest jedną z możliwych konfiguracji. Na przykład można zminimalizować hello liczbę maszyn wirtualnych do grupy dostępności dwie repliki. Ta konfiguracja ogranicza godziny obliczeń na platformie Azure przy użyciu kontrolera domeny hello jako monitor udziału plików hello kworum w klastrze z dwoma węzłami. Ta metoda zmniejsza liczbę maszyn wirtualnych hello przez jeden z opisami hello konfiguracji.

Ten samouczek zakłada hello następujące czynności:

* Masz już konto platformy Azure.
* Wiesz już, jak toouse hello graficznego interfejsu użytkownika w tooprovision galerii maszyny wirtualnej hello klasyczne maszyny wirtualnej z programem SQL Server.
* Masz już pełny opis zawsze włączonych grup dostępności. Aby uzyskać więcej informacji, zobacz [zawsze włączonych grup dostępności (SQL Server)](https://msdn.microsoft.com/library/hh510230.aspx).

> [!NOTE]
> Jeśli interesuje Cię przy użyciu zawsze włączonych grup dostępności z programu SharePoint, zobacz też [konfigurowania programu SQL Server 2012 grup dostępności Always On programu SharePoint 2013](https://technet.microsoft.com/library/jj715261.aspx).
> 
> 

## <a name="create-hello-virtual-network-and-domain-controller-server"></a>Tworzenie sieci wirtualnej hello i serwer kontrolera domeny
Rozpocznij nowe konto wersji próbnej platformy Azure. Po skonfigurowaniu konta, należy na ekranie macierzystego hello hello klasycznego portalu Azure.

1. Kliknij przycisk hello **nowy** przycisk w hello lewym rogu hello u dołu strony hello, jak pokazano w hello następującego zrzutu ekranu.
   
    ![Kliknij przycisk Nowa, w portalu hello](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC665511.gif)
2. Kliknij przycisk **usług sieciowych** > **sieci wirtualnej** > **Utwórz niestandardowy**, jak pokazano w hello następującego zrzutu ekranu.
   
    ![Utwórz sieć wirtualną](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC665512.gif)
3. W hello **Utwórz sieć WIRTUALNĄ** okna dialogowego Utwórz nową sieć wirtualną przechodzenie między stronami hello i przy użyciu ustawień hello w hello w poniższej tabeli. 
   
   | Strona | Ustawienia |
   | --- | --- |
   | Szczegóły sieci wirtualnej |**Nazwa = ContosoNET**<br/>**REGION = zachodnie stany USA** |
   | Serwery DNS i połączenie z siecią VPN |Brak |
   | Przestrzeniami adresów sieci wirtualnej |Ustawienia zostały pokazane powitania po zrzut ekranu: ![Utwórz sieć wirtualną](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC784620.png) |
4. Utwórz maszynę wirtualną hello, który będzie używany jako hello kontrolera domeny (DC). Kliknij przycisk **nowy** > **obliczeniowe** > **maszyny wirtualnej** > **z galerii**, jak pokazano w Witaj, wykonując zrzut ekranu.
   
    ![Tworzenie maszyny wirtualnej](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC784621.png)
5. W hello **Utwórz MASZYNĘ WIRTUALNĄ A** okna dialogowego Skonfiguruj nową maszynę wirtualną przechodzenie między stronami hello i przy użyciu ustawień hello w hello w poniższej tabeli. 
   
   | Strona | Ustawienia |
   | --- | --- |
   | Wybierz system operacyjny maszyny wirtualnej hello |Windows Server 2012 R2 Datacenter |
   | Konfiguracja maszyny wirtualnej |**Data wydania wersji** = (Najnowsza wersja)<br/>**Nazwa maszyny WIRTUALNEJ** = ContosoDC<br/>**WARSTWA** = STANDARD<br/>**ROZMIAR** = A2 (2 rdzenie)<br/>**NOWĄ nazwę użytkownika** = AzureAdmin<br/>**NOWE hasło** = Contoso! 000<br/>**POTWIERDŹ** = Contoso! 000 |
   | Konfiguracja maszyny wirtualnej |**USŁUGI w CHMURZE** = Tworzenie nowej usługi w chmurze<br/>**Nazwa DNS usługi w CHMURZE** = nazwa usługi w chmurze unikatowy<br/>**Nazwa DNS** unikatową nazwę = (przykład: ContosoDC123)<br/>**REGION/grupy KOLIGACJI i WIRTUALNEJ sieci** = ContosoNET<br/>**PODSIECI sieci WIRTUALNEJ** = Back(10.10.2.0/24)<br/>**Konto MAGAZYNU** = Użyj konta usługi storage automatycznie generowanych<br/>**ZESTAW dostępności** = (Brak) |
   | Opcje maszyny wirtualnej |Użyj wartości domyślnych |

Po skonfigurowaniu hello nowej maszyny wirtualnej, poczekaj na powitania maszyny wirtualnej toobe provsioned. Ten proces trwa niektórych toofinish czasu. Jeśli klikniesz przycisk hello **maszyny wirtualnej** kartę w hello Azure classic portalu, można wyświetlić na ContosoDC stanów następuje z **uruchamianie (inicjowania obsługi administracyjnej)** za**zatrzymane**, **Uruchamianie**, **uruchomiona (inicjowania obsługi administracyjnej)**, a na końcu **systemem**.

Serwer kontrolera domeny Hello pomyślnie jest teraz udostępniony. Następnie skonfiguruj domeny usługi Active Directory hello na tym serwerze kontrolera domeny.

## <a name="configure-hello-domain-controller"></a>Konfiguracja kontrolera domeny hello
W hello następujące kroki możesz skonfigurować hello ContosoDC maszyny jako kontroler domeny corp.contoso.com.

1. W portalu hello wybierz hello **ContosoDC** maszyny. Na powitania **pulpitu nawigacyjnego** , kliknij pozycję **Connect** tooopen pulpitu zdalnego (RDP) plików do dostępu do pulpitu zdalnego.
   
    ![Połącz tooVritual maszyny](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC784622.png)
2. Zaloguj się przy użyciu konta administratora skonfigurowane (**\AzureAdmin**) i hasło (**Contoso! 000**).
3. Domyślnie program hello **Menedżera serwera** powinien zostać wyświetlony pulpit nawigacyjny.
4. Kliknij przycisk hello **Dodaj role i funkcje** łącze na powitania pulpitu nawigacyjnego.
   
    ![W Eksploratorze serwera Dodawanie ról](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC784623.png)
5. Kliknij przycisk **dalej** do momentu uzyskania toohello **ról serwera** sekcji.
6. Wybierz hello **usług domenowych w usłudze Active Directory** i **serwera DNS** ról. Po wyświetleniu monitu, Dodaj więcej funkcji, które wymagają tych ról.
   
   > [!NOTE]
   > Zostanie wyświetlone ostrzeżenie, że nie istnieje żaden adres IP weryfikacji. Jeśli testujesz hello konfiguracji, kliknij przycisk **Kontynuuj**. W scenariuszach produkcji [Użyj programu PowerShell tooset hello statycznego adresu IP maszyny kontrolera domeny hello](../../../virtual-network/virtual-networks-reserved-private-ip.md).
   > 
   > 
   
    ![Dodawanie ról okna dialogowego](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC784624.png)
7. Kliknij przycisk **dalej** aż hello **potwierdzenie** sekcji. Wybierz hello **ponowne uruchomienie serwera docelowego hello automatycznie w razie potrzeby** pole wyboru.
8. Kliknij pozycję **Zainstaluj**.
9. Po zainstalowaniu funkcji hello powrócić toohello **Menedżera serwera** pulpitu nawigacyjnego.
10. Wybierz nowe hello **usług AD DS** opcji w okienku po lewej stronie powitania.
11. Kliknij przycisk hello **więcej** łącze na powitania żółty pasek ostrzeżenie.
    
     ![Usługi AD DS okno dialogowe na maszynie wirtualnej serwera DNS](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC784625.png)
12. W hello **akcji** kolumny hello **wszystkie szczegóły zadania serwera** okno dialogowe, kliknij przycisk **podwyższania poziomu kontrolera domeny tego serwera tooa**.
13. W hello **Kreator konfiguracji usług domenowych Active Directory**, użyj hello następujące wartości:
    
    | Strona | Ustawienie |
    | --- | --- |
    | Konfiguracja wdrażania |**Dodaj nowy las** = wybrane<br/>**Nazwa domeny głównej** = corp.contoso.com |
    | Opcje kontrolera domeny |**Hasło** = Contoso! 000<br/>**Potwierdź hasło** = Contoso! 000 |
14. Kliknij przycisk **dalej** toogo za pośrednictwem hello innych stron w Kreatorze hello. Na powitania **Sprawdzanie wymagań wstępnych** upewnij się, że jest wyświetlany po wiadomość hello: **sprawdzanie wszystkich wymagań wstępnych zakończyło się pomyślnie**. Należy pamiętać, należy przejrzeć wszystkie odpowiednie komunikaty ostrzegawcze, że jest możliwe toocontinue hello instalacji.
15. Kliknij pozycję **Zainstaluj**. Witaj **ContosoDC** maszyny wirtualnej zostanie automatycznie ponownie uruchomiony.

## <a name="configure-domain-accounts"></a>Konfigurowanie kont domeny
Następne kroki Hello skonfiguruj hello kont usługi Active Directory do późniejszego użycia.

1. Zaloguj się ponownie toohello **ContosoDC** maszyny.
2. W **Menedżera serwera**, kliknij przycisk **narzędzia** > **Centrum administracyjne usługi Active Directory**.
   
    ![Centrum administracyjne usługi Active Directory](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC784626.png)
3. W hello **Centrum administracyjne usługi Active Directory**, wybierz pozycję **corp (lokalna)** w okienku po lewej stronie powitania.
4. Na powitania prawo **zadania** okienku, kliknij przycisk **nowy** > **użytkownika**. Użyj hello następujące ustawienia:
   
   | Ustawienie | Wartość |
   | --- | --- |
   | **Imię** |Instalowanie |
   | **SamAccountName użytkownika** |Instalowanie |
   | **Hasło** |Contoso! 000 |
   | **Potwierdź hasło** |Contoso! 000 |
   | **Inne opcje haseł** |Wybrano |
   | **Hasło nigdy nie wygasa** |Zaznaczone |
5. Kliknij przycisk **OK** toocreate hello **zainstalować** użytkownika. To konto będzie używane tooconfigure hello trybu failover klastra i hello grupy dostępności.
6. Tworzenie dwóch dodatkowych użytkowników, **CORP\SQLSvc1** i **CORP\SQLSvc2**, z hello te same czynności. Te konta będą używane dla hello wystąpień programu SQL Server. Następnie należy toogive **CORP\Install** hello klaster pracy awaryjnej systemu Windows tooconfigure niezbędne uprawnienia.
7. W hello **Centrum administracyjne usługi Active Directory**, kliknij przycisk **corp (lokalna)** w okienku po lewej stronie powitania. W hello **zadania** okienku, kliknij przycisk **właściwości**.
   
    ![Właściwości użytkownika CORP](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC784627.png)
8. Wybierz **rozszerzenia**, a następnie kliknij przycisk hello **zaawansowane** przycisk na powitania **zabezpieczeń** kartę.
9. W hello **Zaawansowane ustawienia zabezpieczeń dla corp** okno dialogowe, kliknij przycisk **Dodaj**.
10. Kliknij przycisk **Wybierz podmiot zabezpieczeń**, wyszukaj **CORP\Install**, a następnie kliknij przycisk **OK**.
11. Wybierz hello **odczytywanie wszystkich właściwości** i **Tworzenie obiektów komputerów** uprawnienia.
    
     ![Uprawnienia użytkownika Corp](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC784628.png)
12. Kliknij przycisk **OK**, a następnie kliknij przycisk **OK** ponownie. Zamknij hello corp okna właściwości.

Teraz, gdy skonfigurowano usługi Active Directory i obiektów użytkowników hello utworzysz trzech maszyn wirtualnych programu SQL Server i dołącz je toothis domeny.

## <a name="create-hello-sql-server-virtual-machines"></a>Tworzenie hello maszyn wirtualnych programu SQL Server
Utwórz trzy maszyny wirtualne. Jeden jest węzłem klastra i są dwa dla programu SQL Server. toocreate hello maszyn wirtualnych, przejdź z powrotem toohello klasycznego portalu Azure, kliknij przycisk **nowy** > **obliczeniowe** > **maszyny wirtualnej**  >  **z galerii**. Następnie za pomocą szablonów hello w powitania po tworzenia maszyn wirtualnych na powitania toohelp tabeli.

| Strona | VM1 | MASZYNY VM2 | VM3 |
| --- | --- | --- | --- |
| Wybierz system operacyjny maszyny wirtualnej hello |**Windows Server 2012 R2 Datacenter** |**SQL Server 2014 Enterprise RTM** |**SQL Server 2014 Enterprise RTM** |
| Konfiguracja maszyny wirtualnej |**Data wydania wersji** = (Najnowsza wersja)<br/>**Nazwa maszyny WIRTUALNEJ** = ContosoWSFCNode<br/>**WARSTWA** = STANDARD<br/>**ROZMIAR** = A2 (2 rdzenie)<br/>**NOWĄ nazwę użytkownika** = AzureAdmin<br/>**NOWE hasło** = Contoso! 000<br/>**POTWIERDŹ** = Contoso! 000 |**Data wydania wersji** = (Najnowsza wersja)<br/>**Nazwa maszyny WIRTUALNEJ** = ContosoSQL1<br/>**WARSTWA** = STANDARD<br/>**ROZMIAR** = A3 (4 rdzenie)<br/>**NOWĄ nazwę użytkownika** = AzureAdmin<br/>**NOWE hasło** = Contoso! 000<br/>**POTWIERDŹ** = Contoso! 000 |**Data wydania wersji** = (Najnowsza wersja)<br/>**Nazwa maszyny WIRTUALNEJ** = ContosoSQL2<br/>**WARSTWA** = STANDARD<br/>**ROZMIAR** = A3 (4 rdzenie)<br/>**NOWĄ nazwę użytkownika** = AzureAdmin<br/>**NOWE hasło** = Contoso! 000<br/>**POTWIERDŹ** = Contoso! 000 |
| Konfiguracja maszyny wirtualnej |**USŁUGI w CHMURZE** = nazwa DNS usługi utworzonej wcześniej unikatowe chmury (przykład: ContosoDC123)<br/>**REGION/grupy KOLIGACJI i WIRTUALNEJ sieci** = ContosoNET<br/>**PODSIECI sieci WIRTUALNEJ** = Back(10.10.2.0/24)<br/>**Konto MAGAZYNU** = Użyj konta usługi storage automatycznie generowanych<br/>**ZESTAWU dostępności** = Tworzenie dostępności ustawić<br/>**NAZWA ZBIORU DOSTĘPNOŚCI** = SQLHADR |**USŁUGI w CHMURZE** = nazwa DNS usługi utworzonej wcześniej unikatowe chmury (przykład: ContosoDC123)<br/>**REGION/grupy KOLIGACJI i WIRTUALNEJ sieci** = ContosoNET<br/>**PODSIECI sieci WIRTUALNEJ** = Back(10.10.2.0/24)<br/>**Konto MAGAZYNU** = Użyj konta usługi storage automatycznie generowanych<br/>**ZESTAWU dostępności** = SQLHADR (można również skonfigurować dostępność hello ustawić po utworzeniu maszyny hello. Wszystkie trzy maszyny powinien być przypisany zestaw dostępności SQLHADR toohello.) |**USŁUGI w CHMURZE** = nazwa DNS usługi utworzonej wcześniej unikatowe chmury (przykład: ContosoDC123)<br/>**REGION/grupy KOLIGACJI i WIRTUALNEJ sieci** = ContosoNET<br/>**PODSIECI sieci WIRTUALNEJ** = Back(10.10.2.0/24)<br/>**Konto MAGAZYNU** = Użyj konta usługi storage automatycznie generowanych<br/>**ZESTAWU dostępności** = SQLHADR (można również skonfigurować dostępność hello ustawić po utworzeniu maszyny hello. Wszystkie trzy maszyny powinien być przypisany zestaw dostępności SQLHADR toohello.) |
| Opcje maszyny wirtualnej |Użyj wartości domyślnych |Użyj wartości domyślnych |Użyj wartości domyślnych |

<br/>

> [!NOTE]
> Witaj poprzedniej konfiguracji sugeruje maszyn wirtualnych w warstwie standardowa, ponieważ maszyny warstwy BASIC nie obsługuje punktów końcowych z równoważeniem obciążenia. Należy punktów końcowych z równoważeniem obciążenia nowsze toocreate odbiornik grupy dostępności. Ponadto hello rozmiary sugerowanych w tym miejscu są przeznaczone dla testowania grup dostępności w maszynach wirtualnych platformy Azure. Witaj najlepszą wydajność obciążeń produkcyjnych, zobacz hello zalecenia dotyczące programu SQL Server rozmiary i konfiguracji [wydajności najlepsze rozwiązania dotyczące programu SQL Server w usłudze Azure Virtual Machines](../sql/virtual-machines-windows-sql-performance.md).
> 
> 

Po hello trzy maszyny wirtualne są w pełni zaaprowizowanym, należy toojoin je toohello **corp.contoso.com** domeny i przyznać CORP\Install maszyny toohello prawa administracyjne. toodo tego hello Użyj następujące kroki dla każdego hello trzech maszyn wirtualnych.

1. Najpierw zmień adres serwera DNS hello preferowany. Pobieranie katalogu lokalnego tooyour plik RDP każdej maszyny wirtualnej zaznaczając maszyny wirtualnej hello hello na liście i klikając hello **Connect** przycisku. tooselect maszynę wirtualną, kliknij w dowolnym ale hello pierwszej komórki w wierszu hello, jak pokazano w powitania po zrzut ekranu.
   
    ![Pobierz plik RDP hello](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC664953.jpg)
2. Otwórz hello RDP pliku, którego pobrano i logowania toohello maszyny wirtualnej przy użyciu konta administratora skonfigurowane (**BUILTIN\AzureAdmin**) i hasło (**Contoso! 000**).
3. Po zalogowaniu, powinien zostać wyświetlony hello **Menedżera serwera** pulpitu nawigacyjnego. Kliknij przycisk **lokalnego serwera** w okienku po lewej stronie powitania.
4. Kliknij przycisk hello **adres IPv4 przypisany przez serwer DHCP IPv6 włączone** łącza.
5. W hello **połączenia sieciowe** okna dialogowego kliknij ikonę sieci hello.
   
    ![Serwer DNS preferowanych maszyny wirtualnej hello zmiany](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC784629.png)
6. Na pasku poleceń powitania kliknij **zmiany ustawień hello tego połączenia**. (W zależności od wielkości hello okna, konieczne może być tooclick hello Podwójna strzałka w prawo toosee tego polecenia).
7. Wybierz **protokół internetowy w wersji 4 (TCP/IPv4)**, a następnie kliknij przycisk **właściwości**.
8. Wybierz **hello Użyj następujących adresów serwerów DNS** , a następnie określ **10.10.2.4** w **preferowany serwer DNS**.
9. Witaj **10.10.2.4** adres jest adresem hello, który jest przypisany tooa maszyny wirtualnej w hello 10.10.2.0/24 podsieci w sieci wirtualnej platformy Azure. Czy maszyna wirtualna jest **ContosoDC**. tooverify **ContosoDC**na adres IP, użyj **nslookup contosodc** w oknie wiersza polecenia hello, jak pokazano w hello następującego zrzutu ekranu.
   
    ![Użyj adresu IP toofind NSLOOKUP dla kontrolera domeny](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC664954.jpg)
10. Kliknij przycisk **OK** > **Zamknij** toocommit hello zmiany. Teraz można dołączyć maszyny wirtualnej hello zbyt**corp.contoso.com**.
11. Po powrocie do hello **lokalnego serwera** okna, kliknij hello **grupy roboczej** łącza.
12. W hello **nazwy komputera** kliknij **zmiany**.
13. Wybierz hello **domeny** pole wyboru, typ **corp.contoso.com** w hello pola tekstowego, a następnie kliknij przycisk **OK**.
14. W hello **zabezpieczenia systemu Windows** oknie dialogowym Określ hello poświadczenia dla konta administratora domeny domyślnej hello (**CORP\AzureAdmin**) i hasło hello (**Contoso! 000**).
15. Po wyświetleniu komunikatu "domeny corp.contoso.com toohello powitalnej" hello, kliknij przycisk **OK**.
16. Kliknij przycisk **Zamknij** > **Uruchom ponownie teraz** w oknie dialogowym hello.

### <a name="add-hello-corpinstall-user-as-an-administrator-on-each-virtual-machine"></a>Dodaj użytkownika Corp\Install hello jako administrator na każdej maszynie wirtualnej
1. Poczekaj na ponowne uruchomienie maszyny wirtualnej hello, a następnie otwórz hello RDP plików ponownie toosign toohello maszyny wirtualnej przy użyciu hello **BUILTIN\AzureAdmin** konta.
2. W **Menedżera serwera** kliknij **narzędzia** > **Zarządzanie komputerem**.
   
    ![Zarządzanie komputerem](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC784630.png)
3. W hello **Zarządzanie komputerem** okna dialogowego rozwiń **lokalnych użytkowników i grup**, a następnie kliknij przycisk **grup**.
4. Kliknij dwukrotnie hello **Administratorzy** grupy.
5. W hello **właściwości Administratorzy** okna dialogowego kliknij hello **Dodaj** przycisku.
6. Wprowadź nazwę użytkownika hello **CORP\Install**, a następnie kliknij przycisk **OK**. Po wyświetleniu monitu o poświadczenia, użyj hello **AzureAdmin** konto z hello **Contoso! 000** hasła.
7. Kliknij przycisk **OK** tooclose hello **właściwości administratora** okno dialogowe.

### <a name="add-hello-failover-clustering-feature-tooeach-virtual-machine"></a>Dodaj hello klaster pracy awaryjnej, funkcji i maszynę wirtualną tooeach
1. W hello **Menedżera serwera** pulpitu nawigacyjnego, kliknij przycisk **Dodaj role i funkcje**.
2. W hello **Kreatora dodawania ról i funkcji**, kliknij przycisk **dalej** do momentu uzyskania toohello **funkcje** strony.
3. Wybierz **klaster pracy awaryjnej**. Po wyświetleniu monitu, Dodaj inne funkcje zależne.
   
    ![Dodaj funkcję Klaster pracy awaryjnej toovirtual maszyny](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC784631.png)
4. Kliknij przycisk **dalej**, a następnie kliknij przycisk **zainstalować** na powitania **potwierdzenie** strony.
5. Gdy hello **klaster pracy awaryjnej** instalacja funkcji została zakończona, kliknij przycisk **Zamknij**.
6. Wyloguj hello maszyny wirtualnej.
7. Powtórz kroki hello w tej sekcji, dla wszystkich trzech serwerów: **ContosoWSFCNode**, **ContosoSQL1**, i **ContosoSQL2**.

Witaj przydzielania maszyny wirtualnej programu SQL Server i uruchomiona, ale każda ma hello domyślne opcje dla programu SQL Server.

## <a name="create-hello-failover-cluster"></a>Tworzenie klastra pracy awaryjnej hello
W tej sekcji utworzysz hello klastra trybu failover, który będzie obsługiwał hello grupy dostępności, która zostanie utworzona później. W razie należy przeprowadzić powitania po tooeach hello trzech maszyn wirtualnych, które będą używane w klastrze pracy awaryjnej hello:

* Pełni hello maszyny wirtualnej platformy Azure
* Przyłączony do domeny toohello maszyny wirtualnej hello
* Dodaje **CORP\Install** toohello lokalnej grupy administratorów
* Dodano hello funkcji klastra pracy awaryjnej

Wszystkie są wymagania wstępne na każdej maszynie wirtualnej zanim można było przyłączyć ją toohello klastra pracy awaryjnej.

Ponadto należy pamiętać, że hello sieci wirtualnej platformy Azure nie zachowują się w hello sam sposób jak sieci lokalnej. Należy toocreate hello klastra w hello w następującej kolejności:

1. Utwórz w jednym węźle klastra z jednym węzłem (**ContosoSQL1**).
2. Modyfikowanie tooan adres IP klastra hello nieużywany adres IP (**10.10.2.101**).
3. Przełącz hello online nazwy klastra.
4. Dodaj hello innych węzłów (**ContosoSQL2** i **ContosoWSFCNode**).

Użyj hello następujące kroki toocomplete hello zadań, które pełnej konfiguracji hello klastra.

1. Witaj Otwórz plik RDP dla **ContosoSQL1**i zaloguj się przy użyciu konta domeny hello **CORP\Install**.
2. W hello **Menedżera serwera** pulpitu nawigacyjnego, kliknij przycisk **narzędzia** > **Menedżera klastra trybu Failover**.
3. W okienku po lewej stronie powitania kliknij prawym przyciskiem myszy **Menedżera klastra trybu Failover**, a następnie kliknij przycisk **utworzyć klaster**, jak pokazano w hello następującego zrzutu ekranu.
   
    ![Tworzenie klastra](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC784632.png)
4. W hello Kreatora tworzenia klastra, tworzenie klastra z jednym węzłem przechodzenie między stronami hello i przy użyciu ustawień hello w hello w poniższej tabeli:
   
   | Strona | Ustawienia |
   | --- | --- |
   | Przed rozpoczęciem |Użyj wartości domyślnych |
   | Wybierz serwery |Typ **ContosoSQL1** w **wprowadź nazwę serwera** i kliknij przycisk **Dodaj** |
   | Ostrzeżenie dotyczące sprawdzania poprawności |Wybierz **testów nr nie jest wymagana obsługa firmy Microsoft dla tego klastra, a w związku z tym nie ma toorun hello weryfikacji. Po kliknięciu przycisku dalej kontynuować tworzenie klastra hello**. |
   | Punkt dostępu do hello administrowanie klastra |Typ **klaster_1** w **nazwa klastra** |
   | Potwierdzenie |Użyj wartości domyślnych, chyba że w przypadku korzystania z funkcji miejsca do magazynowania. Zobacz ostrzeżenie hello poniżej tej tabeli. |
   
   > [!WARNING]
   > Jeśli używasz [miejsca do magazynowania](https://technet.microsoft.com/library/hh831739), który grupuje wiele dysków w pule magazynu, należy wyczyścić hello **Dodaj wszystkie odpowiednie magazyny toohello klaster** pole wyboru na powitania **potwierdzenia** strony. Jeśli ta opcja nie zostanie wyczyszczone, hello wirtualnych dysków będzie można odłączyć podczas hello procesu klastrowania. W związku z tym również nie pojawią się w Menedżerze dysków lub w Eksploratorze dopóki hello miejsca do magazynowania nie zostaną usunięte z klastra hello i ponownie nałożona za pomocą programu PowerShell.
   > 
   > 
5. W okienku po lewej stronie powitania rozwiń **Menedżera klastra trybu Failover**, a następnie kliknij przycisk **Cluster1.corp.contoso.com**.
6. W środkowym okienku hello przewiń w dół toohello **zasoby podstawowe klastra** sekcji, a następnie rozwiń węzeł hello **Name: Clutser1** szczegóły. Powinny być widoczne oba hello **nazwa** i hello **adres IP** zasobów w hello **** stanu. Hello zasobu adresu IP nie może być przełączony w tryb online przypisane klastra hello hello sam adres IP hello komputerze, który jest zduplikowany adres.
7. Kliknij prawym przyciskiem myszy hello nie powiodło się **adres IP** zasobów, a następnie kliknij przycisk **właściwości**.
   
    ![Właściwości klastra](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC784633.png)
8. Wybierz **statyczny adres IP**, określ **10.10.2.101** w hello **adres** polu tekstowym, a następnie kliknij przycisk **OK**.
9. W hello **zasoby podstawowe klastra** sekcji, kliknij prawym przyciskiem myszy **Name: Klaster1**, a następnie kliknij przycisk **przejdź do trybu Online**. Zaczekaj, aż oba zasoby są w trybie online. Zasób Nazwa klastra hello przejściu do trybu online, serwerem kontrolera hello zostaje zaktualizowany przy użyciu nowego konta komputerów usługi Active Directory. To konto usługi Active Directory będzie używana później grupy dostępności hello toorun klastrowanej usługi.
10. Dodaj hello pozostałych węzłów klastra toohello. W drzewie przeglądarki hello, kliknij prawym przyciskiem myszy **Cluster1.corp.contoso.com**, a następnie kliknij przycisk **Dodaj węzeł**, jak pokazano w hello następującego zrzutu ekranu.
    
     ![Dodawanie węzła klastra toohello](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC784634.png)
11. W hello **Kreatora dodawania węzłów**, kliknij przycisk **dalej** na powitania **Wybieranie serwerów** Dodaj **ContosoSQL2** i **ContosoWSFCNode**  toohello listy, wpisując nazwę serwera hello **wprowadź nazwę serwera** , a następnie klikając polecenie **Dodaj**. Gdy wszystko będzie gotowe, kliknij przycisk **dalej**.
12. Na powitania **ostrzeżenie dotyczące sprawdzania poprawności** kliknij przycisk **nr**, mimo że w środowisku produkcyjnym, należy wykonać testy weryfikacyjne hello. Następnie kliknij przycisk **Dalej**.
13. Na powitania **potwierdzenie** kliknij przycisk **dalej** tooadd hello węzłów.
    
    > [!WARNING]
    > Jeśli używasz [miejsca do magazynowania](https://technet.microsoft.com/library/hh831739), który grupuje wiele dysków w pule magazynu, należy wyczyścić hello **Dodaj wszystkie odpowiednie magazyny toohello klaster** pole wyboru. Jeśli ta opcja nie zostanie wyczyszczone, hello wirtualnych dysków będzie można odłączyć podczas hello procesu klastrowania. W związku z tym również nie pojawi się w Menedżerze dysków lub w Eksploratorze dopóki hello miejsca do magazynowania są usuwane z klastra i ponownie nałożona przy użyciu programu PowerShell.
    > 
    > 
14. Po dodaniu klastra toohello hello węzłów, kliknij przycisk **Zakończ**. Menedżer klastra trybu failover powinna zostać wyświetlona, czy klaster ma trzy węzły i wyświetlić je w hello **węzłów** kontenera.
15. Wyloguj hello sesji usług pulpitu zdalnego.

## <a name="prepare-hello-sql-server-instances-for-availability-groups"></a>Przygotowanie hello wystąpień programu SQL Server do grupy dostępności
W tej sekcji będziesz wykonywać hello na obu **ContosoSQL1** i **contosoSQL2**:

* Dodaj dane logowania dla **NT AUTHORITY\System** niezbędne uprawnienia ustawienie toohello domyślnego wystąpienia programu SQL Server.
* Dodaj **CORP\Install** jako wystąpienie programu SQL Server domyślne toohello roli sysadmin.
* Otwórz zaporę Windows hello dla dostępu zdalnego programu SQL Server.
* Włącz hello zawsze włączone grupy funkcji dostępności.
* Zmienianie konta usługi programu SQL Server hello zbyt**CORP\SQLSvc1** i **CORP\SQLSvc2**odpowiednio.

Te akcje można wykonać w dowolnej kolejności. Niemniej jednak hello następujące kroki przeprowadzi je w kolejności. Wykonaj kroki hello zarówno **ContosoSQL1** i **ContosoSQL2**:

1. Jeśli nie nastąpiło wylogowanie hello sesji usług pulpitu zdalnego dla maszyny wirtualnej hello, należy to zrobić teraz.
2. Pliki otwarte hello RDP **ContosoSQL1** i **ContosoSQL2**i zaloguj się jako **BUILTIN\AzureAdmin**.
3. Dodaj **NT AUTHORITY\System** toohello logowania programu SQL Server z niezbędne uprawnienia. Otwórz program **SQL Server Management Studio**.
4. Kliknij przycisk **Connect** programu tooconnect toohello domyślnego wystąpienia programu SQL Server.
5. W **Eksplorator obiektów**, rozwiń węzeł **zabezpieczeń**, a następnie rozwiń węzeł **logowania**.
6. Kliknij prawym przyciskiem myszy hello **NT AUTHORITY\System** logowania, a następnie kliknij przycisk **właściwości**.
7. Na powitania **zabezpieczanych obiektów** stronie powitania serwera lokalnego, wybierz pozycję **Grant** dla hello następujących uprawnień, a następnie kliknij przycisk **OK**.
   
   * Instrukcja ALTER żadnej grupy dostępności
   * Połączenia SQL
   * Widok stanu serwera
8. Dodaj **CORP\Install** jako **sysadmin** wystąpienia programu SQL Server domyślne toohello roli. W **Eksplorator obiektów**, kliknij prawym przyciskiem myszy **logowania**, a następnie kliknij przycisk **nowe dane logowania**.
9. Typ **CORP\Install** w **nazwa logowania**.
10. Na powitania **ról serwera** wybierz pozycję **sysadmin**, a następnie kliknij przycisk **OK**. Po utworzeniu hello logowania, można to sprawdzić rozwijając **logowania** w **Eksplorator obiektów**.
11. reguły zapory dla programu SQL Server na powitania toocreate **Start** ekranu, otwórz **Zapora systemu Windows z zabezpieczeniami zaawansowanymi**.
12. Wybierz w okienku po lewej stronie powitania **reguły ruchu przychodzącego**. W okienku po prawej stronie powitania, kliknij przycisk **nową regułę**.
13. Na powitania **typ reguły** kliknij przycisk **Program** > **dalej**.
14. Na powitania **Program** wybierz pozycję **ta ścieżka programu**, typ **%ProgramFiles%\Microsoft SQL Server\MSSQL12. MSSQLSERVER\MSSQL\Binn\sqlservr.exe** w hello pola tekstowego, a następnie kliknij przycisk **dalej**. Jeśli po te kierunkach, ale przy użyciu programu SQL Server 2012, katalog programu SQL Server hello jest **MSSQL11. MSSQLSERVER**.
15. Na powitania **akcji** Zachowaj **przyłączenia hello** zaznaczone, a następnie kliknij przycisk **dalej**.
16. Na powitania **profilu** zaakceptować ustawienia domyślne hello, a następnie kliknij pozycję **dalej**.
17. Na powitania **nazwa** Określ nazwę reguły, takie jak **programu SQL Server (reguły programu)**, w hello **nazwa** tekstu, a następnie kliknij przycisk **Zakończ**.
18. Witaj tooenable **zawsze włączonych grup dostępności** funkcji na powitania **Start** ekranu, otwórz **SQL Server Configuration Manager**.
19. W drzewie przeglądarki hello, kliknij przycisk **usług SQL Server**, kliknij prawym przyciskiem myszy hello **programu SQL Server (MSSQLSERVER)** usługi, a następnie kliknij przycisk **właściwości**.
20. Kliknij przycisk hello **zawsze na wysoką dostępność** wybierz opcję **Włącz zawsze włączone grupy dostępności**, jak pokazano w hello następujący zrzut ekranu, a następnie kliknij przycisk **Zastosuj**. Kliknij przycisk **OK** w hello — okno dialogowe, a nie zamykaj hello **właściwości** jeszcze — okno dialogowe. Po zmianie konta usługi hello zostanie uruchomiony ponownie hello usługi SQL Server.
    
     ![Włącz zawsze na grupy dostępności](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC665520.gif)
21. toochange hello konto usługi programu SQL Server, kliknij przycisk hello **logowanie** , wpisz **CORP\SQLSvc1** (dla **ContosoSQL1**) lub **CORP\SQLSvc2** () Aby uzyskać **ContosoSQL2**) w **nazwa konta**, wprowadź i Potwierdź hasło hello, a następnie kliknij **OK**.
22. Okno dialogowe hello, który zostanie otwarty, kliknij przycisk **tak** toorestart hello usługi SQL Server. Po ponownym uruchomieniu hello usługi SQL Server, zmiany wprowadzone w hello **właściwości** obowiązują okno dialogowe.
23. Wyloguj hello maszyn wirtualnych.

## <a name="create-hello-availability-group"></a>Utwórz grupę dostępności hello
Wszystko jest teraz gotowy tooconfigure grupy dostępności. Poniżej znajdują się zarys będzie wykonywać:

* Utwórz nową bazę danych (**MyDB1**) na **ContosoSQL1**.
* Przełączyć pełnej kopii zapasowej i kopii zapasowej dziennika transakcji bazy danych hello.
* Przywróć hello pełne i kopii zapasowych dziennika zbyt**ContosoSQL2** z hello **NORECOVERY** opcji.
* Utwórz grupę dostępności hello (**AG1**) z zatwierdzanie synchroniczne, automatycznej pracy awaryjnej i do odczytu replikach pomocniczych.

### <a name="create-hello-mydb1-database-on-contososql1"></a>Utwórz bazę danych MyDB1 hello ContosoSQL1
1. Jeśli użytkownik ma już niepodpisana poza hello sesji pulpitu zdalnego dla **ContosoSQL1** i **ContosoSQL2**, zrób to teraz.
2. Witaj Otwórz plik RDP dla **ContosoSQL1**i zaloguj się jako **CORP\Install**.
3. W **Eksploratora plików**w obszarze **C:\\**, Utwórz katalog o nazwie **kopii zapasowej**. Będzie zużywać tooback tego katalogu i przywracania bazy danych.
4. Kliknij prawym przyciskiem myszy nowy katalog hello, wskaż zbyt**udostępniać**, a następnie kliknij przycisk **określone osoby**, jak pokazano w hello następującego zrzutu ekranu.
   
    ![Tworzenie folderu kopii zapasowej](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC665521.gif)
5. Dodaj **CORP\SQLSvc1**, a następnie nadaj hello **odczytu/zapisu** uprawnienia. Dodaj **CORP\SQLSvc2**i nadaj mu po hello **odczytu** uprawnienia, jak pokazano w hello następujący zrzut ekranu, a następnie kliknij przycisk **udziału**. Po zakończeniu procesu udostępniania plików powitania kliknij **gotowe**.
   
    ![Udzielanie uprawnień dla folderu kopii zapasowej](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC665522.gif)
6. toocreate hello bazy danych z hello **Start** menu, otwórz **programu SQL Server Management Studio**, a następnie kliknij przycisk **Connect** programu tooconnect toohello domyślnego wystąpienia programu SQL Server.
7. W **Eksplorator obiektów**, kliknij prawym przyciskiem myszy **baz danych**, a następnie kliknij przycisk **nową bazę danych**.
8. W **Nazwa bazy danych**, typ **MyDB1**, a następnie kliknij przycisk **OK**.

### <a name="make-a-full-backup-of-mydb1-and-restore-it-on-contososql2"></a>Utwórz kopię zapasową MyDB1 pełne i przywróć ją na ContosoSQL2
1. toomake hello pełną kopię zapasową bazy danych w **Eksplorator obiektów**, rozwiń węzeł **baz danych**, kliknij prawym przyciskiem myszy **MyDB1**, punktu zbyt**zadania**, i następnie kliknij przycisk **kopię zapasową**.
2. W hello **źródła** sekcji, Zachowaj **typ kopii zapasowej** ustawić także**pełne**. W hello **docelowego** kliknij **Usuń** tooremove hello domyślna ścieżka do pliku dla pliku kopii zapasowej hello.
3. W hello **docelowego** kliknij **Dodaj**.
4. W hello **nazwę pliku** polu tekstowym  **\\ContosoSQL1\backup\MyDB1.bak**, kliknij przycisk **OK**, a następnie kliknij przycisk **OK** ponownie tooback hello bazy danych. Po zakończeniu operacji tworzenia kopii zapasowej hello, kliknij przycisk **OK** ponownie tooclose powitalne okno dialogowe.
5. toomake transakcji dziennika kopii zapasowej bazy danych hello, **Eksplorator obiektów**, rozwiń węzeł **baz danych**, kliknij prawym przyciskiem myszy **MyDB1**, punktu zbyt**zadania**, a następnie kliknij przycisk **kopię zapasową**.
6. W **typ kopii zapasowej**, wybierz pozycję **dziennika transakcji**. Zachowaj hello **docelowego** toohello zestaw ścieżki, co określony wcześniej plik, a następnie kliknij przycisk **OK**. Po zakończeniu operacji tworzenia kopii zapasowej hello, kliknij przycisk **OK** ponownie.
7. hello toorestore pełne i dziennika transakcji, kopie zapasowe **ContosoSQL2**, otwórz plik hello RDP **ContosoSQL2**i zaloguj się jako **CORP\Install**. Pozostaw hello sesji usług pulpitu zdalnego dla **ContosoSQL1** otworzyć.
8. Z hello **Start** menu, otwórz **programu SQL Server Management Studio**, a następnie kliknij przycisk **Connect** programu tooconnect toohello domyślnego wystąpienia programu SQL Server.
9. W **Eksplorator obiektów**, kliknij prawym przyciskiem myszy **baz danych**, a następnie kliknij przycisk **Restore Database**.
10. W hello **źródła** zaznacz **urządzenia**i kliknij przycisk wielokropka hello **...** Dodaj...
11. W **wybierz urządzenia kopii zapasowej**, kliknij przycisk **Dodaj**.
12. W **lokalizacja pliku kopii zapasowej**, typ  **\\ContosoSQL1\backup**, kliknij przycisk **Odśwież**, wybierz pozycję **MyDB1.bak**, kliknij przycisk **OK**, a następnie kliknij przycisk **OK** ponownie. Powinien zostać wyświetlony hello pełnej kopii zapasowej i kopii zapasowej dziennika hello w hello **toorestore zestawy kopii zapasowych** okienka.
13. Przejdź toohello **opcje** wybierz pozycję **PRZYWRÓCIĆ WITH NORECOVERY** w **stan odzyskiwania**, a następnie kliknij przycisk **OK** toorestore hello w bazie danych. Po hello przywrócić zakończenie operacji, kliknij przycisk **OK**.

### <a name="create-hello-availability-group"></a>Utwórz grupę dostępności hello
1. Przejdź kopii toohello sesji usług pulpitu zdalnego dla **ContosoSQL1**. W **Eksplorator obiektów** w programu SQL Server Management Studio, kliknij prawym przyciskiem myszy **zawsze na wysoką dostępność**, a następnie kliknij przycisk **Kreatora nowej grupy dostępności**, jak pokazano w hello Poniższy zrzut ekranu.
   
    ![Uruchom Kreatora nowej grupy dostępności](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC665523.gif)
2. Na powitania **wprowadzenie** kliknij przycisk **dalej**. Na powitania **Określ nazwę grupy dostępności** wpisz **AG1** w **Nazwa grupy dostępności**, następnie kliknij przycisk **dalej** ponownie.
   
    ![Kreatora nowej grupy dostępności, nazwa grupy dostępności Określ](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC665524.gif)
3. Na powitania **wybierz baz danych** wybierz **MyDB1**, a następnie kliknij przycisk **dalej**. Hello bazy danych spełnia wymagania wstępne powitania dla grupy dostępności, ponieważ co najmniej jedną pełną kopię zapasową wykonano na powitania zamierzone repliki podstawowej.
   
    ![Kreatora nowej grupy Availabilty, wybierz opcję baz danych](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC665525.gif)
4. na powitania **Określanie replik** kliknij przycisk **dodać repliki**.
   
    ![Kreatora nowej grupy Availabilty, określ repliki](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC665526.gif)
5. W hello **połączyć tooServer** okno dialogowe, typ **ContosoSQL2** w **nazwy serwera**, a następnie kliknij przycisk **Connect**.
   
    ![Kreatora nowej grupy Availabilty, Connect tooserver](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC665527.gif)
6. Wróć na powitania **Określanie replik** strony, powinien zostać wyświetlony **ContosoSQL2** na liście **replik dostępności**. Konfigurowanie replik hello, jak pokazano w hello następującego zrzutu ekranu. Gdy skończysz, kliknij przycisk **dalej**.
   
    ![Kreatora nowej grupy Availabilty, określ repliki (Zakończ)](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC665528.gif)
7. Na powitania **Wybierz początkową synchronizację danych** wybierz **tylko Dołącz**, a następnie kliknij przycisk **dalej**. Już wykonanego synchronizacji danych ręcznie wprowadzone hello transakcji i pełne kopie zapasowe na **ContosoSQL1** i przywrócić je na **ContosoSQL2**. Można wybrać nie tooperform hello operacji tworzenia kopii zapasowej i przywracania bazy danych i zamiast tego wybrać **pełne** toolet powitania w Kreatorze nowej grupy dostępności przeprowadzenia synchronizacji danych należy. Jednak zaleca się tę opcję dla bardzo dużych baz danych, które znajdują się w niektóre przedsiębiorstwa.
   
    ![Kreator nowej grupy Availabilty, wybierz początkową synchronizację danych](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC665529.gif)
8. Na powitania **weryfikacji** kliknij przycisk **dalej**. Ta strona powinna wyglądać podobnie toohello następującego zrzutu ekranu. Brak ostrzeżenia dla konfiguracji odbiornika hello ponieważ odbiornik grupy dostępności nie zostały skonfigurowane. Można zignorować to ostrzeżenie, ponieważ w tym samouczku nie konfiguruje odbiornik. odbiornik hello tooconfigure po ukończeniu tego samouczka, zobacz [skonfigurować odbiornik ILB dla zawsze włączonych grup dostępności na platformie Azure](../classic/ps-sql-int-listener.md).
   
    ![Availabilty Kreatora nowej grupy sprawdzania poprawności](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC665530.gif)
9. Na powitania **Podsumowanie** kliknij przycisk **Zakończ**, a następnie zaczekaj, aż Kreator hello konfiguruje hello nowej grupy dostępności. Na powitania **postępu** strony, możesz kliknąć **szczegółowe** tooview hello szczegółowe postępu. Po zakończeniu pracy Kreatora hello, sprawdź hello **wyniki** tooverify strony tej grupy dostępności hello została pomyślnie utworzona, jak pokazano w hello następującego zrzutu ekranu, a następnie kliknij **Zamknij** tooexit hello Kreator.
   
    ![Availabilty Kreatora nowej grupy wyników](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC665531.gif)
10. W **Eksplorator obiektów**, rozwiń węzeł **zawsze na wysoką dostępność**, a następnie rozwiń węzeł **grup dostępności**. Powinna zostać wyświetlona hello nowej grupy dostępności w tym kontenerze. Kliknij prawym przyciskiem myszy **AG1 (podstawowe)**, a następnie kliknij przycisk **Pokaż pulpit nawigacyjny**.
    
     ![Pokaż grupy dostępności pulpitu nawigacyjnego](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC665532.gif)
11. Twoje **zawsze na pulpicie nawigacyjnym** powinien wyglądać podobnie toohello jeden w hello po zrzut ekranu. Widać hello replik, tryb pracy awaryjnej hello każdej repliki i hello stan synchronizacji.
    
     ![Pulpit nawigacyjny grupy dostępności](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC665533.gif)
12. Zwraca zbyt**Menedżera serwera**, kliknij przycisk **narzędzia**, a następnie otwórz **Menedżera klastra trybu Failover**.
13. Rozwiń węzeł **Cluster1.corp.contoso.com**, a następnie rozwiń węzeł **usługi i aplikacje**. Wybierz **ról** i należy pamiętać, że hello **AG1** rola grupy dostępności została utworzona. Należy pamiętać, że AG1 nie ma adresu IP przez bazę danych, która klienci mogą łączyć się toohello grupy dostępności, ponieważ nie może skonfigurować odbiornik. Możesz połączyć bezpośrednio toohello węzła podstawowego dla operacji odczytu i zapisu oraz hello węzła pomocniczego dla zapytań tylko do odczytu.
    
     ![W Menedżerze klastra trybu Failover grupy dostępności](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC665534.gif)

> [!WARNING]
> Nie próbuj toofail za pośrednictwem grupy dostępności hello z hello Menedżera klastra trybu Failover. Należy wykonać wszystkie operacje trybu failover z poziomu **zawsze na pulpicie nawigacyjnym** w programie SQL Server Management Studio. Aby uzyskać więcej informacji, zobacz [ograniczenia dotyczące Using hello Menedżera klastra trybu Failover z grupami dostępności](https://msdn.microsoft.com/library/ff929171.aspx).
> 
> 

## <a name="next-steps"></a>Następne kroki
Możesz teraz pomyślnie wdrożono programu SQL Server AlwaysOn przez utworzenie grupy dostępności na platformie Azure. tooconfigure odbiornika dla tej grupy dostępności, zobacz [skonfigurować odbiornik ILB dla zawsze włączonych grup dostępności na platformie Azure](../classic/ps-sql-int-listener.md).

Aby uzyskać inne informacje o korzystaniu z programu SQL Server na platformie Azure, zobacz [programu SQL Server na maszynach wirtualnych Azure](../sql/virtual-machines-windows-sql-server-iaas-overview.md).

