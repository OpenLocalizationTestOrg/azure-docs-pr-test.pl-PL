---
title: "aaaSQL wirtualna połączenia tooAzure wyszukiwania | Dokumentacja firmy Microsoft"
description: "Włączanie połączeń szyfrowanych i skonfigurować hello zapory tooallow połączeń tooSQL serwera na maszynie wirtualnej platformy Azure (VM) z indeksatora w usłudze Azure Search."
services: search
documentationcenter: 
author: HeidiSteen
manager: pablocas
editor: 
ms.assetid: 46e42e0e-c8de-4fec-b11a-ed132db7e7bc
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 01/23/2017
ms.author: heidist
ms.openlocfilehash: 1f0db8a2812b0a7d012e58bb873c4b2b29fa1338
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-connection-from-an-azure-search-indexer-toosql-server-on-an-azure-vm"></a>Skonfiguruj połączenie z tooSQL indeksator usługi Azure Search Server na maszynie Wirtualnej platformy Azure
Zgodnie z opisem w [tooAzure połączenie bazy danych SQL Azure wyszukiwania przy użyciu indeksatorów](search-howto-connecting-azure-sql-database-to-azure-search-using-indexers.md#faq), tworzenie indeksatory przed **programu SQL Server na maszynach wirtualnych Azure** (lub **maszynach wirtualnych Azure SQL** skrócie) jest obsługiwane przez usługi Azure Search, ale ma kilka wymagań wstępnych związanych z zabezpieczeń tootake nad pierwszy. 

**Czas trwania:** około 30 minut, zakładając, że możesz już zainstalowany certyfikat na powitania maszyny Wirtualnej.

## <a name="enable-encrypted-connections"></a>Włączanie połączeń szyfrowanych
Usługa Azure Search wymaga zaszyfrowanego kanału dla wszystkich żądań indeksatora za pośrednictwem publicznego połączenia internetowego. Ta sekcja zawiera toomake kroki hello tę pracę.

1. Sprawdź właściwości hello nazwa podmiotu hello hello certyfikatu tooverify hello pełną nazwę domeny (FQDN) z hello maszyny Wirtualnej platformy Azure. Można użyć narzędzia, takiego jak CertUtils lub hello właściwości hello tooview przystawki Certyfikaty. Witaj nazwy FQDN można pobrać z bloku hello maszyny Wirtualnej usługi Essentials części, hello **publiczny adres IP na adres/etykieta nazwy DNS** w hello [portalu Azure](https://portal.azure.com/).
   
   * Dla maszyn wirtualnych utworzonych przy użyciu nowszej hello **Resource Manager** szablonu, hello nazwy FQDN jest w formacie `<your-VM-name>.<region>.cloudapp.azure.com`. 
   * Dla starszych maszyny wirtualne utworzone jako **klasycznego** maszyny Wirtualnej, jest w formacie FQDN hello `<your-cloud-service-name.cloudapp.net>`. 
2. Konfigurowanie certyfikatu hello toouse programu SQL Server przy użyciu hello Edytora rejestru (regedit). 
   
    Chociaż Menedżer konfiguracji programu SQL Server jest często używany do tego zadania, nie można używać go w tym scenariuszu. Brakuje hello zaimportowane certyfikatu, ponieważ hello FQDN hello maszyny Wirtualnej na platformie Azure nie jest zgodny hello FQDN zgodnie z ustaleniami hello maszyny Wirtualnej (identyfikuje hello domeny jako hello komputera lokalnego lub hello toowhich domeny sieciowej, który jest przyłączony do). Gdy nazwy nie są zgodne, należy użyć certyfikatu hello toospecify regedit.
   
   * W programie regedit, przejdź toothis klucz rejestru: `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\[MSSQL13.MSSQLSERVER]\MSSQLServer\SuperSocketNetLib\Certificate`.
     
     Witaj `[MSSQL13.MSSQLSERVER]` części w zależności od wersji i nazwę wystąpienia. 
   * Ustaw wartość hello hello **certyfikatu** klucza toohello **odcisk palca** certyfikatu SSL hello zaimportowane toohello maszyny Wirtualnej.
     
     Istnieje kilka sposobów tooget hello odcisku palca, niektóre lepiej od innych. Skopiowanie z hello **certyfikaty** przystawkę programu MMC, użytkownik prawdopodobnie przejmą niewidoczne wiodących znaków [zgodnie z opisem w tym artykule pomocy technicznej](https://support.microsoft.com/kb/2023869/), które powoduje błąd przy próbie połączenie. Istnieje kilka obejścia dla rozwiązania tego problemu. Najprostszym Hello jest toobackspace powyżej, a następnie ponownie wpisz hello pierwszym znakiem hello odcisk palca tooremove hello wiodących znaków w polu wartość klucza hello w programie regedit. Alternatywnie można użyć odcisk palca hello toocopy innego narzędzia.
3. Przyznaj uprawnienia toohello konta usługi. 
   
    Upewnij się, że udzieleniu odpowiednich uprawnień na powitania klucza prywatnego certyfikatu SSL hello hello konto usługi programu SQL Server. Jeśli pomijane ten krok, programu SQL Server nie zostanie uruchomiona. Można użyć hello **certyfikaty** przystawki lub **CertUtils** dla tego zadania.
4. Uruchom ponownie usługę SQL Server hello.

## <a name="configure-sql-server-connectivity-in-hello-vm"></a>Skonfiguruj połączenie programu SQL Server w hello maszyny Wirtualnej
Po skonfigurowaniu połączenia hello szyfrowane wymagane przez usługę Azure Search są wewnętrzne tooSQL kroki dodatkowej konfiguracji serwera na maszynach wirtualnych Azure. Jeśli jeszcze tego nie zrobiono tego wcześniej, następnym krokiem hello jest toofinish konfiguracji przy użyciu jednej z tych artykułach:

* Dla **Resource Manager** maszyny Wirtualnej, zobacz [połączyć tooa maszyny wirtualnej programu SQL Server na platformie Azure przy użyciu usługi Resource Manager](../virtual-machines/windows/sql/virtual-machines-windows-sql-connect.md). 
* Dla **klasycznego** maszyny Wirtualnej, zobacz [połączyć tooa maszyny wirtualnej serwera SQL w klasycznym Azure](../virtual-machines/windows/classic/sql-connect.md).

W szczególności, przejrzyj sekcję hello w każdym artykule "połączenie za pośrednictwem hello internet".

## <a name="configure-hello-network-security-group-nsg"></a>Skonfiguruj hello grupy zabezpieczeń sieci (NSG)
Nie jest nietypowe tooconfigure hello NSG i odpowiedniego punktu końcowego platformy Azure lub listy kontroli dostępu (ACL) toomake strony tooother dostępny z maszyny Wirtualnej platformy Azure. Prawdopodobnie czynności zostały wykonane przed tooallow własnych aplikacji logiki tooconnect tooyour maszyny Wirtualnej Azure SQL. Nie różni się dla usługi Azure Search tooyour połączenia maszyny Wirtualnej Azure SQL się go. 

poniższe linki Hello zawierają instrukcje konfiguracji wdrażania maszyny Wirtualnej w konfiguracji grupy NSG. Wykonaj te instrukcje tooACL punktu końcowego usługi Azure SEarch na podstawie jego adresu IP.

> [!NOTE]
> W tle, zobacz [co to jest grupa zabezpieczeń sieci?](../virtual-network/virtual-networks-nsg.md)
> 
> 

* Dla **Resource Manager** maszyny Wirtualnej, zobacz [jak toocreate grup NSG wdrożeń ARM](../virtual-network/virtual-networks-create-nsg-arm-pportal.md). 
* Dla **klasycznego** maszyny Wirtualnej, zobacz [jak toocreate grup NSG wdrożeń Classic](../virtual-network/virtual-networks-create-nsg-classic-ps.md).

Adresy IP mogą wiązać się z kilku wyzwania, które są łatwo rozwiązać, jeśli masz świadomość hello problemu i potencjalnych rozwiązań. Witaj pozostałych sekcjach zalecenia dotyczące obsługi problemów powiązanych tooIP adresów w hello listy ACL.

#### <a name="restrict-access-toohello-search-service-ip-address"></a>Ograniczenia adresu IP usługi wyszukiwania toohello dostępu
Zdecydowanie zaleca się ograniczyć hello dostępu toohello adres IP usługi wyszukiwania w hello ACL zamiast wprowadzania maszynach wirtualnych platformy SQL Azure całego Otwórz tooany żądania połączenia. Można łatwo znaleźć hello IP adres, wysyłając polecenie ping hello nazwy FQDN (na przykład `<your-search-service-name>.search.windows.net`) usługi wyszukiwania.

#### <a name="managing-ip-address-fluctuations"></a>Zarządzanie zmianami adresu IP
Jeśli usługa wyszukiwania ma tylko jedną jednostkę wyszukiwania (czyli jedna replika i jednej partycji), adres IP hello zmieni się podczas ponownego uruchamiania komputera usługa rutynowych unieważnia istniejące listy ACL z adresu IP usługi wyszukiwania.

Wystąpił błąd połączenia kolejnych hello jednokierunkowej tooavoid jest toouse więcej niż jednej repliki i jedną partycję w usłudze Azure Search. Dzięki temu zwiększa koszt hello, ale również rozwiązuje problem adres IP hello. W usłudze Azure Search nie zmian adresów IP, jeśli masz więcej niż jednej jednostki wyszukiwania.

Drugiej metody jest tooallow hello połączenia toofail, a następnie ponownie skonfigurować hello listy ACL w hello NSG. Średnia można oczekiwać, że toochange adresy IP co kilka tygodni. Dla klientów, którzy są kontrolowane indeksowania na podstawie rzadkim ta metoda może być działało.

Trzeci podejście działało (lecz nie szczególnie bezpieczny) jest toospecify hello zakres adresów IP hello region platformy Azure, których obsługa została zainicjowana usługi wyszukiwania. Lista Hello zakresy adresów IP, z których publiczne adresy IP są przydzielane zasoby tooAzure jest opublikowana w [zakresy IP centrum danych Azure](https://www.microsoft.com/download/details.aspx?id=41653). 

#### <a name="include-hello-azure-search-portal-ip-addresses"></a>Obejmują usługi Azure Search hello portalu adresy IP
Jeśli używasz hello Azure toocreate portalu indeksatora logiki portalu usługi Azure Search wymaga także tooyour dostęp do maszyny Wirtualnej Azure SQL podczas tworzenia. Usługa Azure search portalu adresów IP można znaleźć wysyłając polecenie ping `stamp2.search.ext.azure.com`.

## <a name="next-steps"></a>Następne kroki
W konfiguracji poza hello sposób można teraz wskazać serwer SQL na maszynie Wirtualnej Azure, jako źródło danych hello indeksator usługi Azure Search. Zobacz [tooAzure połączenie bazy danych SQL Azure wyszukiwania przy użyciu indeksatorów](search-howto-connecting-azure-sql-database-to-azure-search-using-indexers.md) Aby uzyskać więcej informacji.

