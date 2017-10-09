---
title: aaaCreate klasyczne maszyny Wirtualnej Azure systemem MySQL | Dokumentacja firmy Microsoft
description: "Utwórz maszynę wirtualną platformy Azure systemem Windows Server 2012 R2 i hello przy użyciu modelu klasycznego wdrażania hello baza danych MySQL."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 98fa06d2-9b92-4d05-ac16-3f8e9fd4feaa
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: cynthn
ms.openlocfilehash: 2c9564955c2bab197a8e494e939ce16c0b9bb605
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="install-mysql-on-a-virtual-machine-created-with-hello-classic-deployment-model-running-windows-server-2016"></a>Zainstaluj MySQL na maszynie wirtualnej utworzone za pomocą hello klasycznego modelu wdrażania systemem Windows Server 2016
[MySQL](https://www.mysql.com) jest popularnych typu open source, bazy danych SQL. W tym samouczku przedstawiono sposób hello tooinstall i uruchom **społecznościową wersję MySQL 5.7.18** jako serwer MySQL na maszynie wirtualnej z systemem **systemu Windows Server 2016**. Środowiska mogą być nieco inne w przypadku innych wersji MySQL lub Windows Server.

Aby uzyskać instrukcje dotyczące instalowania MySQL w systemie Linux, zapoznaj się: [jak tooinstall MySQL na platformie Azure](../../linux/mysql-install.md).

> [!IMPORTANT]
> Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [Resource Manager i Model Klasyczny](../../../resource-manager-deployment-model.md). W tym artykule omówiono przy użyciu klasycznego modelu wdrożenia hello. Firma Microsoft zaleca, aby większości nowych wdrożeń korzystać hello modelu Resource Manager.

## <a name="create-a-virtual-machine-running-windows-server-2016"></a>Utwórz maszynę wirtualną z systemem Windows Server 2016
Jeśli nie masz jeszcze maszyny Wirtualnej z systemem Windows Server 2016, możesz użyć tej funkcji [samouczek](./tutorial.md) maszyny wirtualnej hello toocreate.

## <a name="attach-a-data-disk"></a>Dołączanie dysku danych
Po utworzeniu maszyny wirtualnej hello, można opcjonalnie dołączyć dysku danych. Dodawanie dysku danych jest zalecane w przypadku obciążeń produkcyjnych i tooavoid kończy się wolne miejsce na dysku systemu operacyjnego (C:) hello, która obejmuje hello systemu operacyjnego.

Zobacz [jak tooattach danych na dysku maszyny wirtualnej systemu Windows tooa](../attach-managed-disk-portal.md) i wykonaj instrukcje hello dołączanie pusty dysk. Ustawienie hello hosta pamięci podręcznej zbyt**Brak** lub **tylko do odczytu**.

## <a name="log-on-toohello-virtual-machine"></a>Zaloguj się na maszynie wirtualnej toohello
Następnie będzie [Zaloguj się na maszynie wirtualnej toohello](./connect-logon.md) , można zainstalować MySQL.

## <a name="install-and-run-mysql-community-server-on-hello-virtual-machine"></a>Zainstaluj i uruchom program MySQL Community Server na maszynie wirtualnej hello
Wykonaj te kroki tooinstall, skonfigurować i uruchomić wersja ciągu identyfikacyjnego hello MySQL serwera:

> [!NOTE]
> Podczas pobierania elementów za pomocą programu Internet Explorer, można ustawić hello IE **Konfiguracja zwiększonych zabezpieczeń** tooOff oraz uprościć hello proces pobierania. Z hello Start menu, kliknij administracyjne serwera Narzędzia Menedżera/lokalnego serwera, a następnie IE **Konfiguracja zwiększonych zabezpieczeń** i ustaw hello konfiguracji tooOff).
>
>

1. Po nawiązaniu połączenia toohello maszyny wirtualnej za pomocą pulpitu zdalnego, kliknij przycisk **programu Internet Explorer** z ekranu startowego hello.
2. Wybierz hello **narzędzia** przycisku na powitania prawym górnym rogu (ikona kółka cogged hello), a następnie kliknij przycisk **Opcje internetowe**. Kliknij hello **zabezpieczeń** , kliknij pozycję hello **Zaufane witryny** ikony, a następnie kliknij przycisk hello **witryn** przycisk. Dodaj http://*.mysql.com toohello listy zaufanych witryn. Kliknij przycisk **Zamknij**, a następnie kliknij przycisk **OK**.
3. W hello adres pasek programu Internet Explorer, wpisz https://dev.mysql.com/downloads/mysql/.
4. Użyj hello MySQL lokacji toolocate i Pobierz najnowszą wersję hello MySQL Instalatora dla systemu Windows hello. W przypadku wybrania hello Instalator MySQL, pobierania wersji hello hello Ukończ zestawu plików (na przykład hello mysql — Instalator — społeczność 5.7.18.0.msi pliku o rozmiarze 352.8 MB) i Zapisz hello Instalatora.
5. Gdy Instalator hello zakończył pobieranie, kliknij przycisk **Uruchom** toolaunch Instalatora.
6. Na powitania **umowy licencyjnej** , zaakceptuj umowę licencyjną hello i kliknij przycisk **dalej**.
7. Na powitania **Wybieranie typu instalacji** kliknij hello typ instalacji, który, a następnie kliknij pozycję **dalej**. Witaj następujących krokach założono hello wybór hello **tylko serwera** typ instalacji.
8. Jeśli hello **Sprawdź wymagania** wyświetlana, kliknij przycisk **Execute** toolet hello Instalatora zainstaluj brakujące składniki. Postępuj zgodnie z instrukcjami zawierające takie jak środowiska uruchomieniowego C++ Redistributable hello.
9. Na powitania **instalacji** kliknij przycisk **Execute**. Po zakończeniu instalacji kliknij przycisk **dalej**.

10. Na powitania **konfiguracji produktu** kliknij przycisk **dalej**.

11. Na powitania **typu i sieci** strony, określ wymaganą konfiguracją typu i łączności opcje, w tym porcie TCP hello w razie potrzeby. Wybierz **Pokaż opcje zaawansowane**, a następnie kliknij przycisk **dalej**.
    ![](./media/mysql-2008r2/MySQL_TypeNetworking.png)

12. Na powitania **kont i ról** Określ silne hasło główne MySQL. W razie potrzeby dodaj dodatkowe konta użytkowników MySQL, a następnie kliknij przycisk **dalej**.

    ![](./media/mysql-2008r2/MySQL_AccountsRoles_Filled.png)
13. Na powitania **usługi systemu Windows** , określ ustawienia domyślne toohello zmiany do uruchamiania jako usługa systemu Windows hello serwer MySQL, zgodnie z potrzebami, a następnie kliknij przycisk **dalej**.

    ![](./media/mysql-2008r2/MySQL_WindowsService.png)
14. Witaj opcje dostępne na powitania **dodatki i rozszerzenia** strony są opcjonalne. Kliknij przycisk **dalej** toocontinue.
15. Na powitania **zaawansowane opcje** Określ opcje toologging zmiany, w razie potrzeby, a następnie kliknij pozycję **dalej**.

    ![](./media/mysql-2008r2/MySQL_AdvOptions.png)
16. Na powitania **zastosować konfiguracji serwera** kliknij przycisk **Execute**. Po ukończeniu czynności konfiguracyjnych powitania kliknij **Zakończ**.
17. Na powitania **konfiguracji produktu** kliknij przycisk **dalej**.
18. Na powitania **zakończenia instalacji** kliknij przycisk **tooClipboard kopii dziennika** Jeśli tooexamine go później, a następnie kliknij przycisk **Zakończ**.
19. Na ekranie startowym hello wpisz **mysql**, a następnie kliknij przycisk **klient wiersza polecenia 5.7 MySQL**.
20. Wprowadź hasła użytkownika root hello określoną w kroku 12, a otrzymasz monit o których możesz wykonywać polecenia tooconfigure MySQL. Szczegółowe hello poleceń i składni, zobacz [instrukcje MySQL](https://dev.mysql.com/doc/refman/5.7/en/server-configuration.html).

    ![](./media/mysql-2008r2/MySQL_CommandPrompt.png)
21. Można również skonfigurować ustawienia domyślne konfiguracji serwera, takich jak hello podstawowej i katalogi danych i dysków. Aby uzyskać więcej informacji, zobacz [6.1.2 domyślnie przyjmowana jest konfiguracja serwera](https://dev.mysql.com/doc/refman/5.7/en/server-configuration-defaults.html).

## <a name="configure-endpoints"></a>Konfigurowanie punktów końcowych

Hello MySQL usługi toobe tooclient dostępnych komputerów na powitania Internet należy skonfigurować punkt końcowy dla hello portu TCP i utworzyć regułę zapory systemu Windows. wartość portu domyślnego Hello nasłuchuje na których serwer MySQL hello MySQL klientów usługi jest 3306. Można określić innego portu, tak długo, jak hello port jest zgodny z wartością hello na powitania **typu i sieci** (krok 11 hello poprzedniej procedury).

> [!NOTE]
> W środowisku produkcyjnym należy wziąć pod uwagę hello na zabezpieczenia dokonywania komputerów tooall dostępne usługi hello MySQL serwera na powitania Internet. Możesz zdefiniować zestaw hello źródłowych adresów IP, które są dozwolone punktu końcowego hello toouse z listy kontroli dostępu (ACL). Aby uzyskać więcej informacji, zobacz [jak tooSet się punkty końcowe tooa maszyny wirtualnej](setup-endpoints.md).
>
>

tooconfigure punktu końcowego dla hello usługi MySQL serwera:

1. W portalu Azure hello, kliknij przycisk **maszyn wirtualnych (klasyczne)**, kliknij nazwę hello MySQL maszyny wirtualnej, a następnie kliknij przycisk **punkty końcowe**.
2. Na pasku poleceń hello, kliknij przycisk **Dodaj**.
3. Na powitania **dodać punkt końcowy** wpisz unikatową nazwę **nazwa**.
4. Wybierz **TCP** jako protokół hello.
5. Wpisz numer portu hello, takich jak **3306**, zarówno w **Port publiczny** i **Port prywatny**, a następnie kliknij przycisk **OK**.

## <a name="add-a-windows-firewall-rule-tooallow-mysql-traffic"></a>Dodaj tooallow reguły zapory systemu Windows ruchu MySQL
reguły zapory systemu Windows, która zezwala na ruch MySQL z hello Internet, uruchom następujące polecenia na powitania tooadd _wiersza polecenia programu Windows PowerShell z podwyższonym poziomem uprawnień_ na maszynie wirtualnej serwera MySQL hello.

    New-NetFirewallRule -DisplayName "MySQL57" -Direction Inbound –Protocol TCP –LocalPort 3306 -Action Allow -Profile Public

## <a name="test-your-remote-connection"></a>Testowanie połączenia zdalnego
tootest Twojego połączenia zdalnego toohello maszyny Wirtualnej Azure uruchomionych hello MySQL serwera usługi, należy podać nazwę DNS hello hello zawierający hello VN usługi w chmurze.

1. W portalu Azure hello, kliknij przycisk **maszyn wirtualnych (klasyczne)**, kliknij nazwę hello MySQL maszyny wirtualnej serwera, a następnie kliknij przycisk **omówienie**.
2. Z poziomu pulpitu nawigacyjnego hello maszyny wirtualnej, należy zwrócić uwagę hello **nazwy DNS** wartość. Oto przykład:

   ![](media/mysql-2008r2/MySQL_DNSName.png)
3. Z komputera lokalnego z systemem MySQL lub powitania klienta MySQL uruchom następujące polecenie toolog w jako użytkownik MySQL hello.

     MySQL -u <yourMysqlUsername> - p -h<yourDNSname>

   Na przykład przy użyciu nazwy użytkownika MySQL hello _dbadmin3_ i hello _testmysql.cloudapp.net_ nazwy DNS dla maszyny wirtualnej hello, można uruchomić przy użyciu następującego polecenia hello MySQL:

     testmysql.cloudapp.net -h -p dbadmin3 -u MySQL

## <a name="next-steps"></a>Następne kroki
toolearn więcej informacji na temat uruchamiania MySQL, zobacz hello [dokumentacji MySQL](http://dev.mysql.com/doc/).
