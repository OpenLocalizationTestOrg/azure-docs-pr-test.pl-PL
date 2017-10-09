---
title: "aaaExtend tooAzure zawsze włączonych grup dostępności lokalnymi | Dokumentacja firmy Microsoft"
description: "W tym samouczku są używane zasoby utworzone za pomocą hello klasycznego modelu wdrażania i w tym artykule opisano, jak toouse hello kreatora Dodawanie repliki w tooadd programu SQL Server Management Studio (SSMS) replice zawsze włączonej grupy dostępności na platformie Azure."
services: virtual-machines-windows
documentationcenter: na
author: MikeRayMSFT
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 7ca7c423-8342-4175-a70b-d5101dfb7f23
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 05/31/2017
ms.author: mikeray
ms.openlocfilehash: 51fe117b40d69706b35f30101538a7a36116e128
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="extend-on-premises-always-on-availability-groups-tooazure"></a>Rozszerzanie tooAzure zawsze włączonych grup dostępności lokalnego
Zawsze włączone grupy dostępności zapewnia wysoką dostępność dla grup bazy danych, dodając replikach pomocniczych. Zezwalaj na tych replik przechodzenie w tryb failover baz danych w przypadku awarii. Ponadto mogą być używane toooffload odczytu obciążeń lub zadania tworzenia kopii zapasowych.

Inicjowanie obsługi administracyjnej przynajmniej jednej maszyny wirtualnej Azure z programem SQL Server, a następnie dodanie ich jako tooyour replik grupy dostępności lokalnymi można rozszerzyć lokalnych grup dostępności tooMicrosoft Azure.

Ten samouczek zakłada, że masz następujące hello:

* Aktywna subskrypcja platformy Azure. Możesz [utworzyć konto bezpłatnej wersji próbnej](https://azure.microsoft.com/pricing/free-trial/).
* Istniejące zawsze włączonej grupy dostępności lokalnego. Aby uzyskać więcej informacji dotyczących grup dostępności, zobacz [zawsze włączonych grup dostępności](https://msdn.microsoft.com/library/hh510230.aspx).
* Łączność między hello lokalnej sieci i sieci wirtualnej platformy Azure. Aby uzyskać więcej informacji o tworzeniu tej sieci wirtualnej, zobacz [Utwórz Site-to-Site połączenia za pomocą hello portalu Azure (klasyczne)](../../../vpn-gateway/vpn-gateway-howto-site-to-site-classic-portal.md).

> [!IMPORTANT] 
> Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [Resource Manager i Model Klasyczny](../../../azure-resource-manager/resource-manager-deployment-model.md). W tym artykule omówiono przy użyciu klasycznego modelu wdrożenia hello. Firma Microsoft zaleca, aby większości nowych wdrożeń korzystać hello modelu Resource Manager.

## <a name="add-azure-replica-wizard"></a>Dodaj kreatora Azure repliki
W tej sekcji opisano sposób toouse hello **Kreatora dodawania repliki Azure** tooextend Twojego zawsze włączonej grupy dostępności tooinclude rozwiązania Azure replik.

> [!IMPORTANT]
> Witaj **Kreatora dodawania repliki Azure** obsługuje tylko maszyny wirtualne utworzone za pomocą hello klasycznego modelu wdrożenia. Nowe wdrożenia maszyny Wirtualnej należy używać hello nowszej modelu Resource Manager. Jeśli korzystasz z maszyn wirtualnych za pomocą Menedżera zasobów, należy ręcznie dodać hello pomocniczej replice Azure przy użyciu języka Transact-SQL commmands (nie jest tutaj widoczny). Ten kreator nie będzie działać w hello scenariusza Menedżera zasobów.

1. Od w ramach programu SQL Server Management Studio rozwiń **zawsze na wysoką dostępność** > **grup dostępności** > **[Nazwa grupy dostępności]**.
2. Kliknij prawym przyciskiem myszy **replik dostępności**, następnie kliknij przycisk **dodać repliki**.
3. Domyślnie program hello **tooAvailability repliki, Dodaj kreatora grupy** jest wyświetlany. Kliknij przycisk **Dalej**.  Jeśli wybrano hello **nie pokazuj tej strony ponownie** opcji u dołu strony hello hello podczas poprzedniego uruchomienia tego kreatora, ten ekran nie będą wyświetlane.
   
    ![SQL](./media/virtual-machines-windows-classic-sql-onprem-availability/IC742861.png)
4. Będzie wymagane tooconnect tooall istniejących replik pomocniczych. Możesz kliknąć **połączenia...** obok każdej replice lub kliknąć **wszystkie połączenia...** u dołu hello hello ekranu. Po uwierzytelnieniu kliknij **dalej** tooadvance toohello następnego ekranu.
5. Na powitania **Określanie replik** strony, wiele kart są wyświetlane u góry hello: **replik**, **punkty końcowe**, **preferencji tworzenia kopii zapasowej**, i **Odbiornika**. Z hello **replik** , kliknij pozycję **dodać repliki Azure...** toolaunch hello Azure repliki Kreatora dodawania.
   
    ![SQL](./media/virtual-machines-windows-classic-sql-onprem-availability/IC742863.png)
6. Wybierz istniejący certyfikat zarządzania platformy Azure z lokalnego magazynu certyfikatów systemu Windows hello, jeśli została zainstalowana przed. Wybierz lub wprowadź identyfikator hello subskrypcji platformy Azure, jeśli użyto jednego przed. Można kliknąć toodownload pobierania i zainstaluj certyfikat zarządzania platformy Azure i Pobierz hello listy subskrypcji przy użyciu konta platformy Azure.
   
    ![SQL](./media/virtual-machines-windows-classic-sql-onprem-availability/IC742864.png)
7. Wypełnisz każdego pola na stronie powitania z wartościami, które będą używane toocreate hello Azure maszyny wirtualnej (VM), który będzie hostem repliki hello.
   
   | Ustawienie | Opis |
   | --- | --- |
   | **Obraz** |Wybierz kombinację hello żądanego systemu operacyjnego i programu SQL Server |
   | **Rozmiar maszyny Wirtualnej** |Wybierz rozmiar maszyny Wirtualnej, która najlepiej odpowiada Twoim potrzebom firm hello |
   | **Nazwa maszyny Wirtualnej** |Określ unikatową nazwę dla hello nowej maszyny Wirtualnej. Nazwa Hello musi zawierać od 3 do 15 znaków, może zawierać tylko litery, cyfry i łączniki, musi zaczynać się literą i kończyć literą lub cyfrą. |
   | **Nazwa użytkownika maszyny Wirtualnej** |Określ nazwę użytkownika, który ma zostać hello konta administratora na powitania maszyny Wirtualnej |
   | **Hasło administratora maszyny Wirtualnej** |Określ hasło dla nowego konta hello |
   | **Potwierdź hasło** |Potwierdź hasło hello hello nowego konta |
   | **Virtual Network** |Określ hello powitalne tej nowej maszyny Wirtualnej należy używać sieci wirtualnej platformy Azure. Aby uzyskać więcej informacji o sieciach wirtualnych, zobacz [omówienie sieci wirtualnych](../../../virtual-network/virtual-networks-overview.md). |
   | **Podsieć sieci wirtualnej** |Określ podsieć sieci wirtualnej hello tego hello używanego nowej maszyny Wirtualnej |
   | **Domeny** |Upewnij się, że wartość wstępnie wypełnione hello hello domeny jest poprawna |
   | **Nazwa użytkownika domeny** |Określ konto, które znajduje się w grupie administratorów lokalnych hello w węzłach klastra lokalne powitania |
   | **Hasło** |Określ nazwę użytkownika domeny hello hello hasło |
8. Kliknij przycisk **OK** toovalidate hello wdrażania ustawień.
9. Postanowienia prawne są wyświetlane obok. Przeczytaj i kliknij przycisk **OK** Jeśli akceptujesz toothese warunki.
10. Witaj **Określanie replik** ponownie zostanie wyświetlona strona. Sprawdź ustawienia hello nowej repliki Azure hello na powitania **replik**, **punkty końcowe**, i **preferencji tworzenia kopii zapasowej** karty. Zmodyfikuj ustawienia toomeet wymagań biznesowych.  Aby uzyskać więcej informacji o parametrach hello zawartych w tych kartach zobacz [określanie strony repliki (Kreatora nowej grupy dostępności Kreator/Dodaj repliki)](https://msdn.microsoft.com/library/hh213088.aspx). Należy pamiętać, że odbiorników nie można utworzyć przy użyciu karty odbiornika powitania dla grupy dostępności, które zawierają Azure replik. Ponadto jeśli odbiornik został już utworzony hello wcześniejsze toolaunching kreatora, zostanie wyświetlony komunikat informujący, że nie jest obsługiwana na platformie Azure. Firma Microsoft będzie wyglądać jak odbiorników toocreate w hello **tworzenia odbiornika grupy dostępności** sekcji.
    
     ![SQL](./media/virtual-machines-windows-classic-sql-onprem-availability/IC742865.png)
11. Kliknij przycisk **Dalej**.
12. Wybierz metodę synchronizacji danych hello ma toouse na powitania **Wybierz początkową synchronizację danych** i kliknij przycisk **dalej**. W przypadku większości scenariuszy wybrać **pełną synchronizację danych**. Aby uzyskać więcej informacji o metodach synchronizowania danych, zobacz [wybierz danych synchronizacji stronę początkową (zawsze na dostępność grupy kreatorów)](https://msdn.microsoft.com/library/hh231021.aspx).
13. Przejrzyj wyniki hello na powitania **weryfikacji** strony. Popraw nierozwiązane problemy i ponownie uruchom hello weryfikacji w razie potrzeby. Kliknij przycisk **Dalej**.
    
     ![SQL](./media/virtual-machines-windows-classic-sql-onprem-availability/IC742866.png)
14. Przejrzyj ustawienia hello na powitania **Podsumowanie** strony, a następnie kliknij przycisk **Zakończ**.
15. rozpoczyna się Hello w procesie inicjowania obsługi. Po pomyślnym zakończeniu działania kreatora hello, kliknij przycisk **Zamknij** tooexit poza hello kreatora.

> [!NOTE]
> Witaj Kreatora dodawania repliki Azure tworzy plik dziennika w Users\User Name\AppData\Local\SQL Server\AddReplicaWizard. Ten plik dziennika może być wdrożeń Azure repliki używane tootroubleshoot nie powiodło się. W przypadku niepowodzenia hello Kreatora wykonywania żadnych czynności wszystkich poprzednich operacji są wycofywane, włącznie z usunięciem hello zainicjowano obsługę administracyjną maszyn wirtualnych.
> 
> 

## <a name="create-an-availability-group-listener"></a>Utwórz odbiornik grupy dostępności
Po utworzeniu grupy dostępności hello, należy utworzyć odbiornika dla klientów tooconnect toohello repliki. Odbiorniki bezpośrednie przychodzących połączeń tooeither hello podstawowej lub pomocniczej replice tylko do odczytu. Aby uzyskać więcej informacji na odbiorników, zobacz [skonfigurować odbiornik ILB dla zawsze włączonych grup dostępności na platformie Azure](../classic/ps-sql-int-listener.md).

## <a name="next-steps"></a>Następne kroki
W dodatku toousing hello **Kreatora dodawania repliki Azure** tooextend Twojego tooAzure zawsze włączonej grupy dostępności może również przenieść niektórych obciążeń programu SQL Server całkowicie tooAzure. Zobacz tooget pracę, [inicjowania obsługi maszyny wirtualnej programu SQL Server na platformie Azure](../sql/virtual-machines-windows-portal-sql-server-provision.md).

Dla innych tematach dotyczących toorunning programu SQL Server na maszynach wirtualnych Azure, zobacz [programu SQL Server na maszynach wirtualnych Azure](../sql/virtual-machines-windows-sql-server-iaas-overview.md).

