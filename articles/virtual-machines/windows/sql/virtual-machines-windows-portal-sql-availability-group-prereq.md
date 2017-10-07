---
title: "grupuje aaaSQL dostępność serwera - maszyn wirtualnych platformy Azure — wymagania wstępne | Dokumentacja firmy Microsoft"
description: "Ten samouczek pokazuje, jak tooconfigure hello wymagania wstępne dotyczące tworzenia dostępności programu SQL Server zawsze włączone grupy na maszynach wirtualnych Azure."
services: virtual-machines
documentationCenter: na
authors: MikeRayMSFT
manager: jhubbard
editor: monicar
tags: azure-service-management
ms.assetid: c492db4c-3faa-4645-849f-5a1a663be55a
ms.service: virtual-machines-sql
ms.devlang: na
ms.custom: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 05/09/2017
ms.author: mikeray
ms.openlocfilehash: eed0729ead25c7793bb17a04cd7fd996c7dc8c9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="complete-hello-prerequisites-for-creating-always-on-availability-groups-on-azure-virtual-machines"></a>Wymagania wstępne pełną hello do tworzenia zawsze włączonych grup dostępności na maszynach wirtualnych Azure

Ten samouczek pokazuje, jak toocomplete hello wymagania wstępne dotyczące tworzenia [programu SQL Server zawsze włączone grupy dostępności na maszynach wirtualnych platformy Azure (VM)](virtual-machines-windows-portal-sql-availability-group-tutorial.md). Po zakończeniu hello wymagania wstępne są kontrolera domeny, dwóch maszyn wirtualnych programu SQL Server i serwera monitora w pojedynczej grupy zasobów.

**Szacowanie czasu**: może potrwać kilka godzin toocomplete hello wstępnie wymagane składniki. Większość tego czasu jest spędzana na tworzenie maszyn wirtualnych.

Witaj poniższym diagramie przedstawiono kompilacji w samouczku hello.

![Grupy dostępności](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/00-EndstateSampleNoELB.png)

## <a name="review-availability-group-documentation"></a>Przejrzyj dokumentację grupy dostępności

Ten samouczek zakłada, że masz podstawową wiedzę na temat programu SQL Server zawsze włączonych grup dostępności. Jeśli nie masz doświadczenia w obsłudze tej technologii, zobacz [Omówienie programu zawsze włączonych grup dostępności (SQL Server)](http://msdn.microsoft.com/library/ff877884.aspx).


## <a name="create-an-azure-account"></a>Utwórz konto systemu Azure
Musisz mieć konto platformy Azure. Możesz [Załóż bezpłatne konto platformy Azure](/pricing/free-trial/?WT.mc_id=A261C142F) lub [aktywować korzyści dla subskrybentów programu Visual Studio](/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).

## <a name="create-a-resource-group"></a>Tworzenie grupy zasobów
1. Zaloguj się toohello [portalu Azure](http://portal.azure.com).
2. Kliknij przycisk  **+**  toocreate nowy obiekt w portalu hello.

   ![Nowy obiekt](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/01-portalplus.png)

3. Typ **grupy zasobów** w hello **Marketplace** okno wyszukiwania.

   ![Grupa zasobów](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/01-resourcegroupsymbol.png)
4. Kliknij przycisk **grupy zasobów**.
5. Kliknij przycisk **Utwórz**.
6. Na powitania **grupy zasobów** bloku, w obszarze **Nazwa grupy zasobów**, wpisz nazwę grupy zasobów hello. Na przykład wpisz **sql-ha-zarządcy zasobów**.
7. Jeśli masz wiele subskrypcji Azure, sprawdź subskrypcji hello hello subskrypcji platformy Azure, który ma być toocreate hello dostępności grupy.
8. Wybierz lokalizację. Lokalizacja Hello jest hello Azure region, w którym ma być toocreate hello dostępności grupy. W tym samouczku chcemy toobuild wszystkie zasoby w jednej lokalizacji platformy Azure.
9. Sprawdź, czy **toodashboard numeru Pin** jest zaznaczony. To ustawienie opcjonalne umieszcza skrót dla grupy zasobów hello na powitania pulpitu nawigacyjnego portalu Azure.

   ![Grupa zasobów](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/01-resourcegroup.png)

10. Kliknij przycisk **Utwórz** grupy zasobów hello toocreate.

Azure tworzy hello grupy zasobów i numerów PIN skrótów toohello grupę zasobów w portalu hello.

## <a name="create-hello-network-and-subnets"></a>Utwórz hello sieci i podsieci
Witaj następnym krokiem jest toocreate hello sieci i podsieci w hello grupy zasobów platformy Azure.

rozwiązanie Hello używa jedną sieć wirtualną z dwiema podsieciami. Witaj [omówienie sieci wirtualnej](../../../virtual-network/virtual-networks-overview.md) zawiera więcej informacji dotyczących sieci na platformie Azure.

sieć wirtualna hello toocreate:

1. W portalu Azure, w grupie zasobów, hello kliknij **+ Dodaj**. Otwiera Azure hello **wszystko** bloku.

   ![Nowy element](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/02-newiteminrg.png)
2. Wyszukaj **sieci wirtualnej**.

     ![Sieć wirtualna wyszukiwania](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/04-findvirtualnetwork.png)
3. Kliknij przycisk **sieci wirtualnej**.
4. Na powitania **sieci wirtualnej** bloku, kliknij przycisk hello **Menedżera zasobów** model wdrażania, a następnie kliknij **Utwórz**.

    Witaj poniższej tabeli przedstawiono ustawienia hello hello sieci wirtualnej:

   | **Pole** | Wartość |
   | --- | --- |
   | **Nazwa** |autoHAVNET |
   | **Przestrzeń adresowa** |10.33.0.0/24 |
   | **Nazwa podsieci** |Administrator |
   | **Zakres adresów podsieci** |10.33.0.0/29 |
   | **Subskrypcja** |Określ, czy zamierzasz toouse subskrypcji hello. **Subskrypcja** jest puste, jeśli masz tylko jedną subskrypcję. |
   | **Grupa zasobów** |Wybierz **Użyj istniejącego** i wybierz nazwę hello hello grupy zasobów. |
   | **Lokalizacja** |Określ hello lokalizacji platformy Azure. |

   Zakres adresów miejsca i podsieć adresu mogą się różnić od hello tabeli. W zależności od subskrypcji hello portal sugeruje przestrzeni adresów dostępne i odpowiedni zakres adresów podsieci. Jeśli nie ma wystarczającej przestrzeni adresów dostępne, użyj innej subskrypcji.

   przykład Witaj używa hello nazwy podsieci **Admin**. Ta podsieć jest hello kontrolerów domeny.

5. Kliknij przycisk **Utwórz**.

   ![Skonfiguruj sieć wirtualną hello](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/06-configurevirtualnetwork.png)

Azure zwraca wartość toohello pulpitu nawigacyjnego portalu i informuje o utworzeniu hello nowej sieci.

### <a name="create-a-second-subnet"></a>Tworzenie drugiej podsieci
Witaj nowej sieci wirtualnej ma jedną podsieć o nazwie **Admin**. hello kontrolery domeny używają tej podsieci. Witaj maszyn wirtualnych programu SQL Server użyć drugiej podsieci o nazwie **SQL**. tooconfigure tej podsieci:

1. Na pulpicie nawigacyjnym kliknij hello grupy zasobów, które zostały utworzone, **SQL-HA-zarządcy zasobów**. Lokalizowanie hello sieci w grupie zasobów hello w obszarze **zasobów**.

    Jeśli **SQL-HA-zarządcy zasobów** nie jest widoczny, znaleźć, klikając **grup zasobów** i filtrowanie według nazwy grupy zasobów hello.
2. Kliknij przycisk **autoHAVNET** na powitania listy zasobów. Azure zostanie otwarty blok konfiguracji sieci hello.
3. Na powitania **autoHAVNET** bloku sieci wirtualnej, w obszarze **ustawienia** , kliknij przycisk **podsieci**.

    Uwaga hello podsieci, która już utworzone.

   ![Skonfiguruj sieć wirtualną hello](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/07-addsubnet.png)
5. Tworzenie drugiej podsieci. Kliknij przycisk **+ podsieci**.
6. Na powitania **Dodaj podsieć** bloku, skonfiguruj hello podsieci, wpisując **sqlsubnet** w obszarze **nazwa**. Azure automatycznie określa prawidłową **zakres adresów**. Sprawdź, czy ten zakres adresów ma co najmniej 10 adresów w nim. W środowisku produkcyjnym może wymagać więcej adresów.
7. Kliknij przycisk **OK**.

    ![Skonfiguruj sieć wirtualną hello](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/08-configuresubnet.png)

Witaj w poniższej tabeli przedstawiono ustawienia konfiguracji sieciowej hello:

| **Pole** | Wartość |
| --- | --- |
| **Nazwa** |**autoHAVNET** |
| **Przestrzeń adresowa** |Ta wartość zależy od hello przestrzeni adresów dostępne w ramach subskrypcji. Typowe wartości to 10.0.0.0/16. |
| **Nazwa podsieci** |**Administrator** |
| **Zakres adresów podsieci** |Ta wartość zależy od hello dostępne zakresy adresów w ramach subskrypcji. Typowe wartości to 10.0.0.0/24. |
| **Nazwa podsieci** |**sqlsubnet** |
| **Zakres adresów podsieci** |Ta wartość zależy od hello dostępne zakresy adresów w ramach subskrypcji. Typowe wartości to 10.0.1.0/24. |
| **Subskrypcja** |Określ, czy zamierzasz toouse subskrypcji hello. |
| **Grupa zasobów** |**SQL-HA-ZARZĄDCY ZASOBÓW** |
| **Lokalizacja** |Określ hello samą lokalizację, która została wybrana opcja hello grupy zasobów. |

## <a name="create-availability-sets"></a>Tworzenie zestawów dostępności

Przed utworzeniem maszyny wirtualnej należy toocreate zestawów dostępności. Zestawy dostępności skrócić czas przestojów hello planowana lub nieplanowana konserwacja zdarzeń. Zestaw dostępności Azure jest logiczną grupa zasobów Azure umieszcza w fizycznych domenach awarii i Aktualizacja domeny. Domeny błędów gwarantuje, że hello członkami zestawu dostępności hello oddzielne zasilania i zasobów sieciowych. Domeny aktualizacji gwarantuje, że członkowie hello zestawu dostępności nie są obniżył konserwacji na powitania sam czas. Aby uzyskać więcej informacji, zobacz [Zarządzanie hello dostępność maszyn wirtualnych](../manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

Należy dwóch zestawów dostępności. Jedna jest hello kontrolerów domeny. Hello jest drugi dla maszyn wirtualnych hello programu SQL Server.

toocreate dostępności ustawić, przejdź toohello grupy zasobów i kliknij przycisk **Dodaj**. Filtrowanie wyników hello wpisując **zestawu dostępności**. Kliknij przycisk **zestawu dostępności** w hello wyniki, a następnie kliknij przycisk **Utwórz**.

Skonfiguruj dwa zestawy dostępności zgodnie z parametrami toohello w hello w poniższej tabeli:

| **Pole** | Zestaw dostępności kontrolera domeny | Zestaw dostępności programu SQL Server |
| --- | --- | --- |
| **Nazwa** |adavailabilityset |sqlavailabilityset |
| **Grupa zasobów** |SQL-HA-ZARZĄDCY ZASOBÓW |SQL-HA-ZARZĄDCY ZASOBÓW |
| **Domen błędów** |3 |3 |
| **Aktualizowanie domeny** |5 |3 |

Po utworzeniu zestawów dostępności hello Zwróć grupy zasobów toohello hello portalu Azure.

## <a name="create-domain-controllers"></a>Utworzyć kontrolerów domeny
Po utworzeniu sieci hello, podsieci, zestawów dostępności i równoważenia obciążenia internetowy, wszystko gotowe toocreate maszyn wirtualnych hello hello kontrolerów domeny.

### <a name="create-virtual-machines-for-hello-domain-controllers"></a>Tworzenie maszyn wirtualnych dla hello kontrolerów domeny
toocreate i skonfigurować hello kontrolerów domeny, aby uzyskać toohello **SQL-HA-zarządcy zasobów** grupy zasobów.

1. Kliknij pozycję **Dodaj**. Witaj **wszystko** zostanie otwarty blok.
2. Typ **systemu Windows Server 2016 Datacenter**.
3. Kliknij przycisk **systemu Windows Server 2016 Datacenter**. W hello **systemu Windows Server Datacenter 2016** bloku, sprawdź modelu wdrażania hello jest **Menedżera zasobów**, a następnie kliknij przycisk **Utwórz**. Otwiera Azure hello **tworzenia maszyny wirtualnej** bloku.

Powtórz hello poprzedzających kroki toocreate dwóch maszyn wirtualnych. Nazwa Witaj dwie maszyny wirtualne:

* kontrolerów domeny podstawowej AD
* kontrolerów domeny pomocniczy AD

  > [!NOTE]
  > Witaj **kontrolerów domeny pomocniczy ad** maszyny wirtualnej jest opcjonalny, tooprovide wysokiej dostępności dla usług domenowych w usłudze Active Directory.
  >
  >

Witaj poniższej tabeli przedstawiono ustawienia powitania dla tych dwóch maszyn:

| **Pole** | Wartość |
| --- | --- |
| **Nazwa** |Pierwszy kontroler domeny: *kontrolerów domeny podstawowej ad*.</br>Drugi kontroler domeny *kontrolerów domeny pomocniczy ad*. |
| **Typ dysku maszyny wirtualnej** |SSD |
| **Nazwa użytkownika** |Administrator domeny |
| **Hasło** |Contoso! 0000 |
| **Subskrypcja** |*Twoja subskrypcja* |
| **Grupa zasobów** |SQL-HA-ZARZĄDCY ZASOBÓW |
| **Lokalizacja** |*Lokalizacja* |
| **Rozmiar** |DS1_V2 |
| **Storage** | **Użyj zarządzanego dysków** - **tak** |
| **Sieć wirtualna** |autoHAVNET |
| **Podsieć** |Administrator |
| **Publiczny adres IP** |*Samą nazwę jak hello maszyny Wirtualnej* |
| **Grupy zabezpieczeń sieci** |*Samą nazwę jak hello maszyny Wirtualnej* |
| **Zestaw dostępności** |adavailabilityset </br>**Odporność domen**: 2</br>**Aktualizowanie domeny**: 2|
| **Diagnostyka** |Enabled (Włączony) |
| **Konto magazynu diagnostyki** |*Automatycznie utworzone* |

   >[!IMPORTANT]
   >Maszyny Wirtualnej można umieścić tylko w dostępności po jego utworzeniu. Nie można zmienić dostępności hello ustawić po utworzeniu maszyny Wirtualnej. Zobacz [Zarządzanie hello dostępność maszyn wirtualnych](../manage-availability.md).

Platforma Azure tworzy hello maszyn wirtualnych.

Po utworzeniu maszyny wirtualnej hello, skonfiguruj hello kontrolera domeny.

### <a name="configure-hello-domain-controller"></a>Konfiguracja kontrolera domeny hello
W hello następujące kroki, skonfiguruj hello **kontrolerów domeny podstawowej ad** komputera jako kontroler domeny corp.contoso.com.

1. Otwórz hello portal hello **SQL-HA-zarządcy zasobów** grupy zasobów i wybierz hello **kontrolerów domeny podstawowej ad** maszyny. Na powitania **kontrolerów domeny podstawowej ad** bloku, kliknij przycisk **Connect** tooopen RDP plików do dostępu do pulpitu zdalnego.

    ![Połącz tooa maszyny wirtualnej](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/20-connectrdp.png)
2. Zaloguj się przy użyciu konta administratora skonfigurowane (**\DomainAdmin**) i hasło (**Contoso! 0000**).
3. Domyślnie program hello **Menedżera serwera** powinien zostać wyświetlony pulpit nawigacyjny.
4. Kliknij przycisk hello **Dodaj role i funkcje** łącze na powitania pulpitu nawigacyjnego.

    ![Menedżer serwera — Dodawanie ról](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/22-addfeatures.png)
5. Wybierz **dalej** do momentu uzyskania toohello **ról serwera** sekcji.
6. Wybierz hello **usług domenowych w usłudze Active Directory** i **serwera DNS** ról. Po wyświetleniu monitu, Dodaj wszelkie dodatkowe funkcje, które są wymagane przez tych ról.

   > [!NOTE]
   > System Windows wyświetli ostrzeżenie, że nie istnieje żaden adres IP. Jeśli testujesz konfiguracji powitania kliknij **Kontynuuj**. W scenariuszach produkcji, należy ustawić toostatic adres IP hello w hello portalu Azure, lub [Użyj programu PowerShell tooset hello statycznego adresu IP maszyny kontrolera domeny hello](../../../virtual-network/virtual-networks-reserved-private-ip.md).
   >
   >

    ![Dodawanie ról okna dialogowego](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/23-addroles.png)
7. Kliknij przycisk **dalej** aż hello **potwierdzenie** sekcji. Wybierz hello **ponowne uruchomienie serwera docelowego hello automatycznie w razie potrzeby** pole wyboru.
8. Kliknij pozycję **Zainstaluj**.
9. Po funkcji hello zakończenia instalowania, zwróć toohello **Menedżera serwera** pulpitu nawigacyjnego.
10. Wybierz nowe hello **usług AD DS** opcji w okienku po lewej stronie powitania.
11. Kliknij przycisk hello **więcej** łącze na powitania żółty pasek ostrzeżenie.

    ![Usługi AD DS z okna dialogowego na powitania maszyny Wirtualnej serwera DNS](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/24-addsmore.png)
12. W hello **akcji** kolumny hello **wszystkie szczegóły zadania serwera** okna dialogowego, kliknij przycisk **podwyższania poziomu kontrolera domeny tego serwera tooa**.
13. W hello **Kreator konfiguracji usług domenowych Active Directory**, użyj hello następujące wartości:

    | **Strona** | Ustawienie |
    | --- | --- |
    | **Konfiguracja wdrażania** |**Dodaj nowy las**<br/> **Nazwa domeny głównej** = corp.contoso.com |
    | **Opcje kontrolera domeny** |**Hasło trybu DSRM** = Contoso! 0000<br/>**Potwierdź hasło** = Contoso! 0000 |
14. Kliknij przycisk **dalej** toogo za pośrednictwem hello innych stron w Kreatorze hello. Na powitania **Sprawdzanie wymagań wstępnych** upewnij się, że jest wyświetlany po wiadomość hello: **sprawdzanie wszystkich wymagań wstępnych zakończyło się pomyślnie**. Możesz przejrzeć wszystkie odpowiednie komunikaty ostrzegawcze, ale jest możliwe toocontinue hello instalacji.
15. Kliknij pozycję **Zainstaluj**. Witaj **kontrolerów domeny podstawowej ad** maszyny wirtualnej zostanie automatycznie uruchomiony ponownie.

### <a name="note-hello-ip-address-of-hello-primary-domain-controller"></a>Należy pamiętać, adres IP hello hello podstawowego kontrolera domeny

Użyj hello podstawowego kontrolera domeny dla serwera DNS. Należy pamiętać, adres IP kontrolera domeny podstawowej hello.

Adres IP kontrolera domeny podstawowej hello jednokierunkowej tooget odbywa się za pośrednictwem hello portalu Azure.

1. Na powitania portalu Azure Otwórz hello grupy zasobów.

2. Kliknij przycisk hello podstawowego kontrolera domeny.

3. W bloku kontrolera domeny podstawowej hello, kliknij **interfejsy sieciowe**.

![Interfejsy sieciowe](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/25-primarydcip.png)

Należy zwrócić uwagę hello prywatnego adresu IP dla tego serwera.

### <a name="configure-hello-virtual-network-dns"></a>Skonfiguruj sieć wirtualną hello DNS
Po utworzeniu pierwszego kontrolera domeny hello i Włącz DNS na pierwszym serwerze hello, skonfiguruj toouse sieci wirtualnej hello tego serwera dla serwera DNS.

1. W portalu Azure hello kliknij hello sieci wirtualnej.

2. W obszarze **ustawienia**, kliknij przycisk **serwera DNS**.

3. Kliknij przycisk **niestandardowe**i wpisz hello prywatnego adresu IP hello podstawowego kontrolera domeny.

4. Kliknij pozycję **Zapisz**.

### <a name="configure-hello-second-domain-controller"></a>Skonfiguruj hello kontrolera domeny
Po ponownym uruchomieniu hello podstawowego kontrolera domeny, można skonfigurować hello kontrolera domeny. Jest to krok opcjonalny wysokiej dostępności. Wykonaj te kroki tooconfigure hello kontrolera domeny:

1. Otwórz hello portal hello **SQL-HA-zarządcy zasobów** grupy zasobów i wybierz hello **kontrolerów domeny pomocniczy ad** maszyny. Na powitania **kontrolerów domeny pomocniczy ad** bloku, kliknij przycisk **Connect** tooopen RDP plików do dostępu do pulpitu zdalnego.
2. Zaloguj się przy użyciu konta administratora skonfigurowane toohello maszyny Wirtualnej (**BUILTIN\DomainAdmin**) i hasło (**Contoso! 0000**).
3. Zmień hello preferowany adres serwera DNS adres toohello hello kontrolera domeny.
4. W **Centrum sieci i udostępniania**, kliknij przycisk hello interfejsu sieciowego.
   ![Interfejs sieciowy](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/26-networkinterface.png)

5. Kliknij pozycję **Właściwości**.
6. Wybierz **protokół internetowy w wersji 4 (TCP/IPv4)** i kliknij przycisk **właściwości**.
7. Wybierz **hello Użyj następujących adresów serwerów DNS** i określenie adresu hello hello podstawowego kontrolera domeny w **preferowany serwer DNS**.
8. Kliknij przycisk **OK**, a następnie **Zamknij** toocommit hello zmiany. Jesteś teraz hello toojoin stanie maszyny Wirtualnej za**corp.contoso.com**.

   >[!IMPORTANT]
   >Jeśli utracisz hello pulpitu zdalnego tooyour połączenie po zmianie ustawienia DNS hello Przejdź toohello portalu i ponownie uruchom hello maszyny wirtualnej platformy Azure.

9. Z hello toohello pulpitu zdalnego dodatkowy kontroler domeny, otwórz **pulpitu nawigacyjnego Menedżera serwera**.
10. Kliknij przycisk hello **Dodaj role i funkcje** łącze na powitania pulpitu nawigacyjnego.

    ![Menedżer serwera — Dodawanie ról](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/22-addfeatures.png)
11. Wybierz **dalej** do momentu uzyskania toohello **ról serwera** sekcji.
12. Wybierz hello **usług domenowych w usłudze Active Directory** i **serwera DNS** ról. Po wyświetleniu monitu, Dodaj wszelkie dodatkowe funkcje, które są wymagane przez tych ról.
13. Po funkcji hello zakończenia instalowania, zwróć toohello **Menedżera serwera** pulpitu nawigacyjnego.
14. Wybierz nowe hello **usług AD DS** opcji w okienku po lewej stronie powitania.
15. Kliknij przycisk hello **więcej** łącze na powitania żółty pasek ostrzeżenie.
16. W hello **akcji** kolumny hello **wszystkie szczegóły zadania serwera** okna dialogowego, kliknij przycisk **podwyższania poziomu kontrolera domeny tego serwera tooa**.
17. W obszarze **konfiguracji wdrożenia**, wybierz pozycję **Dodawanie domeny istniejących tooan kontrolera domeny**.
   ![Konfiguracja wdrażania](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/28-deploymentconfig.png)
18. Kliknij pozycję **Wybierz**.
19. Połącz przy użyciu konta administratora hello (**CORP. CONTOSO.COM\domainadmin**) i hasło (**Contoso! 0000**).
20. W **wybierz domenę z lasu hello**, kliknij swoją domenę, a następnie kliknij przycisk **OK**.
21. W **opcje kontrolera domeny**, użyj wartości domyślnych hello i ustawić hasło DSRM.

   >[!NOTE]
   >Witaj **opcje DNS** strony może ostrzeżenie, że nie można utworzyć delegowania dla tego serwera DNS. Można zignorować to ostrzeżenie w środowiskach nieprodukcyjnych.
22. Kliknij przycisk **dalej** dopóki nie osiągnie okna dialogowego hello hello **wymagania wstępne** Sprawdź. Następnie kliknij pozycję **Zainstaluj**.

Po zakończeniu zmiany konfiguracji hello powitania serwera należy ponownie uruchomić serwer hello.

### <a name="add-hello-private-ip-address-toohello-second-domain-controller-toohello-vpn-dns-server"></a>Dodaj hello prywatny adres IP toohello drugi toohello kontrolera domeny serwera DNS w sieci VPN

W hello portalu Azure w sieci wirtualnej należy zmienić powitania serwera DNS tooinclude hello adres IP hello dodatkowy kontroler domeny. Dzięki temu hello DNS usługi nadmiarowości.

### <a name=DomainAccounts></a>Konfigurowanie kont domeny hello

W następnych krokach hello skonfigurujesz hello kont usługi Active Directory. Witaj poniższej tabeli przedstawiono hello kont:

| |Konto instalacji<br/> |SQLServer 0 <br/>Konto programu SQL Server i usługi agenta SQL |SQLServer-1<br/>Konto programu SQL Server i usługi agenta SQL
| --- | --- | --- | ---
|**Imię** |Instalowanie |SQLSvc1 | SQLSvc2
|**SamAccountName użytkownika** |Instalowanie |SQLSvc1 | SQLSvc2

Użyj następujących hello kroki toocreate poszczególnych kont.

1. Zaloguj się toohello **kontrolerów domeny podstawowej ad** maszyny.
2. W **Menedżera serwera**, wybierz pozycję **narzędzia**, a następnie kliknij przycisk **Centrum administracyjne usługi Active Directory**.   
3. Wybierz **corp (lokalna)** w okienku po lewej stronie powitania.
4. Na powitania prawo **zadania** okienku wybierz **nowy**, a następnie kliknij przycisk **użytkownika**.
   ![Centrum administracyjne usługi Active Directory](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/29-addcnewuser.png)

   >[!TIP]
   >Ustaw złożone hasło dla poszczególnych kont.<br/> W środowiskach nieprodukcyjnych toonever konta użytkownika hello zestaw wygaśnie.

5. Kliknij przycisk **OK** toocreate hello użytkownika.
6. Powtórz hello w poprzednich krokach dla każdego konta trzy hello.

### <a name="grant-hello-required-permissions-toohello-installation-account"></a>Udzielanie uprawnień hello wymagane konta instalacji toohello
1. W hello **Centrum administracyjne usługi Active Directory**, wybierz pozycję **corp (lokalna)** w okienku po lewej stronie powitania. Następnie w prawej hello **zadania** okienku, kliknij przycisk **właściwości**.

    ![Właściwości użytkownika CORP](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/31-addcproperties.png)
2. Wybierz **rozszerzenia**, a następnie kliknij przycisk hello **zaawansowane** przycisk na powitania **zabezpieczeń** kartę.
3. W hello **Zaawansowane ustawienia zabezpieczeń dla corp** okna dialogowego, kliknij przycisk **Dodaj**.
4. Kliknij przycisk **Wybierz podmiot zabezpieczeń**, wyszukaj **CORP\Install**, a następnie kliknij przycisk **OK**.
5. Wybierz hello **odczytywanie wszystkich właściwości** pole wyboru.

6. Wybierz hello **Tworzenie obiektów komputerów** pole wyboru.

     ![Uprawnienia użytkownika Corp](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/33-addpermissions.png)
7. Kliknij przycisk **OK**, a następnie kliknij przycisk **OK** ponownie. Zamknij hello **corp** okna właściwości.

Teraz, po zakończeniu konfigurowania usługi Active Directory i obiektów użytkowników hello, Utwórz dwie maszyny wirtualne z serwera SQL i serwera monitora maszyny Wirtualnej. Wszystkie trzy domeny toohello przyłączyć.

## <a name="create-sql-server-vms"></a>Tworzenie maszyn wirtualnych programu SQL Server

Utwórz trzy dodatkowe maszyny wirtualne. rozwiązanie Hello wymaga dwóch maszyn wirtualnych z wystąpień programu SQL Server. Trzeci maszyny wirtualnej będą działać jako monitor. Można użyć systemu Windows Server 2016 [chmury monitora](http://docs.microsoft.com/windows-server/failover-clustering/deploy-cloud-witness), jednak zgodności ze starszymi systemami operacyjnymi niniejszym dokumencie użyto maszyny wirtualnej dla monitora.  

Przed kontynuowaniem należy wziąć pod uwagę następujące decyzje deisign hello.

* **Magazyn — dyskach zarządzanych Azure**

   Do przechowywania maszyn wirtualnych hello dysków Azure zarządzanych. Firma Microsoft zaleca zarządzane dyski dla maszyn wirtualnych programu SQL Server. Zarządzane dysków dojść do magazynu w tle hello. Ponadto jeśli maszyny wirtualne z dyskami zarządzane są obsługiwane w hello tego samego zestawu dostępności Azure dystrybuuje nadmiarowość odpowiednie zasoby tooprovide hello magazynu. Aby uzyskać więcej informacji, zobacz [Omówienie usługi Azure Managed Disks](../managed-disks-overview.md). Aby uzyskać szczegóły dotyczące dysków zarządzanych w zestawie dostępności, zobacz [używać dysków zarządzanych maszyn wirtualnych w zestawie dostępności](../manage-availability.md#use-managed-disks-for-vms-in-an-availability-set).

* **Adresy IP prywatnej sieci — w środowisku produkcyjnym**

   W przypadku maszyn wirtualnych hello samouczku publicznych adresów IP. Dzięki temu połączenia zdalnego bezpośrednio toohello maszyny wirtualnej za pośrednictwem hello internet — ułatwia czynności konfiguracyjne. W środowiskach produkcyjnych firma Microsoft zaleca tylko prywatnych adresów IP w kolejności tooreduce hello luk wystąpienia programu SQL Server hello zasobu maszyny Wirtualnej.

### <a name="create-and-configure-hello-sql-server-vms"></a>Tworzenie i konfigurowanie maszyn wirtualnych hello programu SQL Server
Następnie należy utworzyć trzy maszyny wirtualne — dwóch maszyn wirtualnych serwera SQL i maszyny Wirtualnej na dodatkowym węźle klastra. toocreate hello maszyn wirtualnych, przejdź wstecz toohello **SQL-HA-zarządcy zasobów** grupy zasobów, kliknij przycisk **Dodaj**, Wyszukiwanie elementu galerii odpowiednie hello, kliknij przycisk **maszyny wirtualnej**, a następnie Kliknij przycisk **z galerii**. Użyj informacji hello w powitania po toohelp tabeli tworzenia maszyn wirtualnych hello:


| Strona | VM1 | MASZYNY VM2 | VM3 |
| --- | --- | --- | --- |
| Wybierz element galerii odpowiednie hello |**Windows Server 2016 Datacenter** |**SQL Server 2016 SP1 Enterprise w systemie Windows Server 2016** |**SQL Server 2016 SP1 Enterprise w systemie Windows Server 2016** |
| Konfiguracja maszyny wirtualnej **podstawy** |**Nazwa** = fsw klastra<br/>**Nazwa użytkownika** = administrator domeny<br/>**Hasło** = Contoso! 0000<br/>**Subskrypcja** = subskrypcji<br/>**Grupa zasobów** = SQL-HA-zarządcy zasobów<br/>**Lokalizacja** = Twojej lokalizacji platformy azure |**Nazwa** sqlserver-0 =<br/>**Nazwa użytkownika** = administrator domeny<br/>**Hasło** = Contoso! 0000<br/>**Subskrypcja** = subskrypcji<br/>**Grupa zasobów** = SQL-HA-zarządcy zasobów<br/>**Lokalizacja** = Twojej lokalizacji platformy azure |**Nazwa** sqlserver-1<br/>**Nazwa użytkownika** = administrator domeny<br/>**Hasło** = Contoso! 0000<br/>**Subskrypcja** = subskrypcji<br/>**Grupa zasobów** = SQL-HA-zarządcy zasobów<br/>**Lokalizacja** = Twojej lokalizacji platformy azure |
| Konfiguracja maszyny wirtualnej **rozmiaru** |**ROZMIAR** = DS1\_V2 (1 rdzeń, 3.5 GB) |**ROZMIAR** = DS2\_V2 (2 rdzenie, 7 GB)</br>rozmiar Hello musi obsługiwać magazynu SSD (obsługi dysków Premium. )) |**ROZMIAR** = DS2\_V2 (2 rdzenie, 7 GB) |
| Konfiguracja maszyny wirtualnej **ustawienia** |**Magazyn**: Użyj zarządzanego dysków.<br/>**Sieć wirtualna** = autoHAVNET<br/>**Podsieci** = sqlsubnet(10.1.1.0/24)<br/>**Publiczny adres IP** wygenerowanej automatycznie.<br/>**Grupy zabezpieczeń sieci** = Brak<br/>**Monitorowanie diagnostyki** = włączone<br/>**Konto magazynu diagnostyki** = Użyj konta usługi storage automatycznie generowanych<br/>**Zestaw dostępności** = sqlAvailabilitySet<br/> |**Magazyn**: Użyj zarządzanego dysków.<br/>**Sieć wirtualna** = autoHAVNET<br/>**Podsieci** = sqlsubnet(10.1.1.0/24)<br/>**Publiczny adres IP** wygenerowanej automatycznie.<br/>**Grupy zabezpieczeń sieci** = Brak<br/>**Monitorowanie diagnostyki** = włączone<br/>**Konto magazynu diagnostyki** = Użyj konta usługi storage automatycznie generowanych<br/>**Zestaw dostępności** = sqlAvailabilitySet<br/> |**Magazyn**: Użyj zarządzanego dysków.<br/>**Sieć wirtualna** = autoHAVNET<br/>**Podsieci** = sqlsubnet(10.1.1.0/24)<br/>**Publiczny adres IP** wygenerowanej automatycznie.<br/>**Grupy zabezpieczeń sieci** = Brak<br/>**Monitorowanie diagnostyki** = włączone<br/>**Konto magazynu diagnostyki** = Użyj konta usługi storage automatycznie generowanych<br/>**Zestaw dostępności** = sqlAvailabilitySet<br/> |
| Konfiguracja maszyny wirtualnej **ustawienia programu SQL Server** |Nie dotyczy |**Łączność z serwerem SQL** = Private (w ramach sieci wirtualnej)<br/>**Port** = 1433<br/>**Uwierzytelnianie SQL** = wyłączone<br/>**Konfiguracja magazynu** = ogólne<br/>**Automatyczne stosowanie poprawek** = niedziela, 2:00<br/>**Automatyczne kopie zapasowe** = wyłączone</br>**Integracja magazynu kluczy Azure** = wyłączone |**Łączność z serwerem SQL** = Private (w ramach sieci wirtualnej)<br/>**Port** = 1433<br/>**Uwierzytelnianie SQL** = wyłączone<br/>**Konfiguracja magazynu** = ogólne<br/>**Automatyczne stosowanie poprawek** = niedziela, 2:00<br/>**Automatyczne kopie zapasowe** = wyłączone</br>**Integracja magazynu kluczy Azure** = wyłączone |

<br/>

> [!NOTE]
> rozmiary Hello sugerowane tutaj są przeznaczone do testowania grup dostępności w maszynach wirtualnych platformy Azure. Witaj najlepszą wydajność obciążeń produkcyjnych, zobacz hello zalecenia dotyczące programu SQL Server rozmiary i konfiguracji [wydajności najlepsze rozwiązania dotyczące programu SQL Server na maszynach wirtualnych Azure](virtual-machines-windows-sql-performance.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
>
>

Po hello trzy maszyny wirtualne są w pełni zaaprowizowanym, należy toojoin je toohello **corp.contoso.com** domeny i przyznać CORP\Install maszyny toohello prawa administracyjne.

### <a name="joinDomain"></a>Dołącz do domeny toohello serwerów hello

Jesteś teraz możliwe toojoin hello maszyn wirtualnych za**corp.contoso.com**. Następujące hello zarówno hello maszynach wirtualnych serwera SQL, jak i plik hello udziału serwera monitora:

1. Połączenie zdalne toohello maszynę wirtualną z **BUILTIN\DomainAdmin**.
2. W **Menedżera serwera**, kliknij przycisk **lokalnego serwera**.
3. Kliknij przycisk hello **grupy roboczej** łącza.
4. W hello **nazwy komputera** kliknij **zmiany**.
5. Wybierz hello **domeny** pole wyboru i wpisz **corp.contoso.com** w polu tekstowym hello. Kliknij przycisk **OK**.
6. W hello **zabezpieczenia systemu Windows** okno podręczne, podaj poświadczenia hello hello domyślnego konta administratora domeny (**CORP\DomainAdmin**) i hasło hello (**Contoso! 0000**).
7. Po wyświetleniu komunikatu "domeny corp.contoso.com toohello powitalnej" hello, kliknij przycisk **OK**.
8. Kliknij przycisk **Zamknij**, a następnie kliknij przycisk **Uruchom ponownie teraz** w oknie dialogowym podręcznego hello.

### <a name="add-hello-corpinstall-user-as-an-administrator-on-each-cluster-vm"></a>Dodaj użytkownika Corp\Install hello jako administrator na każdym klastrze maszyny Wirtualnej

Po uruchomieniu każdej maszyny wirtualnej jako członek domeny hello dodać **CORP\Install** jako członek grupy Administratorzy lokalni hello.

1. Poczekaj, aż hello maszyna wirtualna zostanie ponownie uruchomiony, a następnie uruchom plik RDP hello ponownie z toosign kontrolera domeny podstawowej hello w zbyt**sqlserver 0** przy użyciu hello **CORP\DomainAdmin** konta.
   >[!TIP]
   >Upewnij się, że zalogujesz się przy użyciu konta administratora domeny hello. W poprzednich krokach hello zostały przy użyciu konta administratora w WBUDOWANE hello. Teraz, hello serwera znajduje się w domenie hello, użyj konta domeny hello. W sesji protokołu RDP, określ *domeny*\\*username*.

2. W **Menedżera serwera**, wybierz pozycję **narzędzia**, a następnie kliknij przycisk **Zarządzanie komputerem**.
3. W hello **Zarządzanie komputerem** okna, rozwiń węzeł **lokalnych użytkowników i grup**, a następnie wybierz **grup**.
4. Kliknij dwukrotnie hello **Administratorzy** grupy.
5. W hello **właściwości Administratorzy** okna dialogowego, kliknij przycisk hello **Dodaj** przycisku.
6. Wprowadź nazwę użytkownika hello **CORP\Install**, a następnie kliknij przycisk **OK**.
7. Kliknij przycisk **OK** tooclose hello **właściwości administratora** okna dialogowego.
8. Powtórz poprzednie kroki hello na **sqlserver 1** i **fsw klastra**.

### <a name="setServiceAccount"></a>Ustawianie konta usługi programu SQL Server hello

Na każdej maszynie Wirtualnej serwera SQL Skonfiguruj konto usługi programu SQL Server hello. Za pomocą kont hello utworzony podczas możesz [skonfigurowane konta domeny hello](#DomainAccounts).

1. Otwórz **programu SQL Server Configuration Manager**.
2. Kliknij prawym przyciskiem myszy hello usługi SQL Server, a następnie kliknij przycisk **właściwości**.
3. Ustaw hello konta i hasło.
4. Powtórz te czynności na powitania innych maszyn wirtualnych serwera SQL.  

Dla grup dostępności programu SQL Server każda z maszyn wirtualnych serwera SQL musi toorun jako konto domeny.

### <a name="create-a-sign-in-on-each-sql-server-vm-for-hello-installation-account"></a>Utwórz logowanie na każdej maszynie Wirtualnej serwera SQL dla konta instalacji hello

Użyj grupy dostępności hello tooconfigure hello instalacji konta (CORP\install). To konto wymaga toobe członkiem hello **sysadmin** stałej roli serwera na każdej maszynie Wirtualnej serwera SQL. Witaj następujące kroki tworzenia logowanie dla konta instalacji hello:

1. Łączenie się toohello serwera za pośrednictwem hello protokołu RDP (Remote Desktop) przy użyciu hello  *\<MachineName\>\DomainAdmin* konta.

1. Otwórz program SQL Server Management Studio i połącz toohello lokalne wystąpienie programu SQL Server.

1. W **Eksplorator obiektów**, kliknij przycisk **zabezpieczeń**.

1. Kliknij prawym przyciskiem myszy **logowania**. Kliknij przycisk **nowe dane logowania**.

1. W **nowe dane logowania -**, kliknij przycisk **wyszukiwania**.

1. Kliknij przycisk **lokalizacje**.

1. Wprowadź poświadczenia hello domeny administratora sieci.

1. Użyj konta instalacji hello.

1. Ustaw hello logowania toobe członkiem hello **sysadmin** stałej roli serwera.

1. Kliknij przycisk **OK**.

Powtórz hello w poprzednich krokach na powitania innych maszyn wirtualnych serwera SQL.

## <a name="add-failover-clustering-features-tooboth-sql-server-vms"></a>Dodaj tooboth funkcji Klaster pracy awaryjnej maszyn wirtualnych programu SQL Server

funkcji Klaster pracy awaryjnej tooadd hello na obu maszynach wirtualnych serwera SQL:

1. Łączenie maszyny wirtualnej programu SQL Server toohello za pośrednictwem hello protokołu RDP (Remote Desktop) przy użyciu hello *CORP\install* konta. Otwórz **pulpitu nawigacyjnego Menedżera serwera**.
2. Kliknij przycisk hello **Dodaj role i funkcje** łącze na powitania pulpitu nawigacyjnego.

    ![Menedżer serwera — Dodawanie ról](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/22-addfeatures.png)
3. Wybierz **dalej** do momentu uzyskania toohello **funkcji serwera** sekcji.
4. W **funkcje**, wybierz pozycję **klaster pracy awaryjnej**.
5. Dodaj wszelkie dodatkowe funkcje wymagane.
6. Kliknij przycisk **zainstalować** tooadd hello funkcji.

Powtórz kroki hello na powitania od innych maszyn wirtualnych serwera SQL.

## <a name="a-nameendpoint-firewall-configure-hello-firewall-on-each-sql-server-vm"></a><a name="endpoint-firewall">Skonfiguruj zaporę hello na każdej maszynie Wirtualnej serwera SQL

rozwiązanie Hello wymaga hello następujące porty TCP toobe otwarcia w zaporze hello:

- **Program SQL Server wirtualna**:<br/>
   Port 1433 dla domyślnego wystąpienia programu SQL Server.
- **Sondę modułu równoważenia obciążenia Azure:**<br/>
   Dowolny dostępny port. Przykłady często używają 59999.
- **Punktu końcowego dublowania bazy danych:** <br/>
   Dowolny dostępny port. Przykłady często używają 5022.

Witaj zapory portów należy toobe otwarty na obu maszynach wirtualnych serwera SQL.

Otwieranie portów hello metody Hello zależy od hello zaporę, którego używasz. Hello następnej sekcji opisano, jak tooopen hello portów w Zaporze systemu Windows. Otwórz porty hello wymagane dla wszystkich maszyn wirtualnych programu SQL Server.

### <a name="open-a-tcp-port-in-hello-firewall"></a>Otwórz TCP port w zaporze hello

1. Na hello pierwszy serwer SQL **Start** ekranu, uruchom **Zapora systemu Windows z zabezpieczeniami zaawansowanymi**.
2. W okienku po lewej stronie powitania wybierz **reguły ruchu przychodzącego**. W okienku po prawej stronie powitania, kliknij polecenie **nową regułę**.
3. Aby uzyskać **typ reguły**, wybierz **portu**.
4. Dla portu hello określ **TCP** i hello typu odpowiednie numery portów. Zobacz poniższy przykład hello:

   ![Zapory SQL](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/35-tcpports.png)

5. Kliknij przycisk **Dalej**.
6. Na powitania **akcji** Zachowaj **przyłączenia hello** zaznaczone, a następnie kliknij przycisk **dalej**.
7. Na powitania **profilu** zaakceptować ustawienia domyślne hello, a następnie kliknij pozycję **dalej**.
8. Na powitania **nazwa** Określ nazwę reguły (takich jak **Azure LB sondowania**) w hello **nazwa** polu tekstowym, a następnie kliknij przycisk **Zakończ**.

Powtórz te kroki na hello drugi maszyna wirtualna programu SQL Server.

## <a name="next-steps"></a>Następne kroki

* [Utwórz grupę dostępności programu SQL Server AlwaysOn na maszynach wirtualnych Azure](virtual-machines-windows-portal-sql-availability-group-tutorial.md)
