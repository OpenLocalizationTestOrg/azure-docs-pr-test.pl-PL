---
title: "aaaDeploy usługi scalania podziału | Dokumentacja firmy Microsoft"
description: "Dzielenie i scalanie z narzędzi elastycznej bazy danych"
services: sql-database
documentationcenter: 
author: ddove
manager: jhubbard
editor: 
ms.assetid: 9a993c0f-7052-46cd-aa59-073bea8d535a
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: 6fef641cbc1e73ce34a851c53298a072dade8f9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-split-merge-service"></a>Wdrażanie usługi z podziałem i scalaniem
Narzędzie do scalania podziału Hello umożliwia przenoszenie danych między bazami danych podzielonej. Zobacz [przenoszenia danych między bazami danych w chmurze skalowalnych w poziomie](sql-database-elastic-scale-overview-split-and-merge.md)

## <a name="download-hello-split-merge-packages"></a>Pobieranie hello scalania podziału pakietów
1. Pobieranie najnowszej wersji NuGet hello z [NuGet](http://docs.nuget.org/docs/start-here/installing-nuget).
2. Otwórz wiersz polecenia i przejdź do katalogu toohello, którego pobrano nuget.exe. pobranie Hello obejmuje commmands środowiska PowerShell.
3. Pobierz najnowszy pakiet scalania podziału hello do bieżącego katalogu hello z hello poniżej polecenia:
   ```
   nuget install Microsoft.Azure.SqlDatabase.ElasticScale.Service.SplitMerge
   ```  

pliki Hello są umieszczane w katalogu o nazwie **Microsoft.Azure.SqlDatabase.ElasticScale.Service.SplitMerge.x.x.xxx.x** gdzie *x.x.xxx.x* odzwierciedla hello numer wersji. Znajdź hello scalania podziału usługi plików w hello **content\splitmerge\service** podkatalogu, hello skryptów programu PowerShell podziału scalania (i biblioteki wymagane klienta) w hello **content\splitmerge\powershell** podkatalogu.

## <a name="prerequisites"></a>Wymagania wstępne
1. Utwórz bazę danych bazy danych SQL Azure, która będzie służyć jako hello scalania podziału stanu z bazy danych. Przejdź toohello [portalu Azure](https://portal.azure.com). Utwórz nową **bazy danych SQL**. Nadaj nazwę hello bazy danych i utworzenie nowego administratora i hasła. Należy się toorecord hello nazwę i hasło do późniejszego użycia.
2. Upewnij się, że serwer bazy danych SQL Azure umożliwia tooit tooconnect usług Azure. W portalu hello w hello **ustawienia zapory**, upewnij się, że hello **dostęp do usług tooAzure** ustawioną zbyt**na**. Kliknij przycisk hello przycisk Zapisz, ikona.
   
   ![Dozwolone usług][1]
3. Tworzenie konta usługi Azure Storage, który będzie używany dla danych wyjściowych diagnostyki. Przejdź toohello portalu Azure. Na pasku po lewej stronie powitania kliknij **nowy**, kliknij przycisk **dane i magazyn**, następnie **magazynu**.
4. Tworzenie usługi w chmurze Azure zawierających usługi podziału scalania.  Przejdź toohello portalu Azure. Na pasku po lewej stronie powitania kliknij **nowy**, następnie **obliczeniowe**, **usługi w chmurze**, i **Utwórz**. 

## <a name="configure-your-split-merge-service"></a>Konfigurowanie usługi scalania podziału
### <a name="split-merge-service-configuration"></a>Konfiguracja usługi scalania podziału
1. W folderze hello którego pobrano zestawy hello podziału scalania, Utwórz kopię hello **ServiceConfiguration.Template.cscfg** plik obok **SplitMergeService.cspkg** i zmień jego nazwę **Pliku ServiceConfiguration.cscfg**.
2. Otwórz **pliku ServiceConfiguration.cscfg** w edytorze tekstu, takiego jak Visual Studio, która sprawdza poprawność danych wejściowych, takich jak format hello odcisków palców certyfikatów.
3. Utwórz nową bazę danych lub wybierz istniejący tooserve bazy danych jako hello stanu z bazy danych dla operacji scalania podziału i pobrać parametry połączenia hello tej bazy danych. 
   
   > [!IMPORTANT]
   > W tej chwili hello stanu z bazy danych musi używać sortowania alfabetu łacińskiego hello (SQL\_Latin1\_ogólne\_CP1\_CI\_AS). Aby uzyskać więcej informacji, zobacz [Nazwa sortowania systemu Windows (Transact-SQL)](https://msdn.microsoft.com/library/ms188046.aspx).
   >

   Z bazy danych SQL Azure ciąg połączenia hello jest zwykle hello formularza:
      ```
      Server=myservername.database.windows.net; Database=mydatabasename;User ID=myuserID; Password=mypassword; Encrypt=True; Connection Timeout=30
      ```

4. Wprowadź parametry połączenia w pliku cscfg hello w obu hello **SplitMergeWeb** i **SplitMergeWorker** sekcje roli w ustawieniu ElasticScaleMetadata hello.
5. Dla hello **SplitMergeWorker** rolę, wprowadzić prawidłowe połączenie magazynu tooAzure ciąg hello **WorkerRoleSynchronizationStorageAccountConnectionString** ustawienie.

### <a name="configure-security"></a>Konfigurowanie zabezpieczeń
Szczegółowe instrukcje tooconfigure hello zabezpieczeń hello usługi można znaleźć w temacie toohello [konfiguracji zabezpieczeń scalania podziału](sql-database-elastic-scale-split-merge-security-configuration.md).

Do celów hello wdrożenia simple testu dla tego samouczka minimalny zbiór kroki konfiguracji wykonywane tooget hello usługi do pracy. Kroki te włączają tylko hello jeden/konto komputera wykonywanie ich toocommunicate z usługą hello.

### <a name="create-a-self-signed-certificate"></a>Utwórz certyfikat z podpisem własnym
Utwórz nowy katalog i z tego hello execute katalogu po użyciu polecenia [wiersz polecenia dla programu Visual Studio deweloperów](http://msdn.microsoft.com/library/ms229859.aspx) okno:

   ```
    makecert ^
    -n "CN=*.cloudapp.net" ^
    -r -cy end -sky exchange -eku "1.3.6.1.5.5.7.3.1,1.3.6.1.5.5.7.3.2" ^
    -a sha1 -len 2048 ^
    -sr currentuser -ss root ^
    -sv MyCert.pvk MyCert.cer
   ```

Są wyświetlane pytanie o hasło klucza prywatnego hello tooprotect. Wpisz silne hasło i potwierdź je. Następnie zostanie wyświetlony monit o toobe hasło hello używany po raz. Kliknij przycisk **tak** na powitania zakończenia tooimport on toohello magazynu zaufanych głównych urzędów certyfikacji.

### <a name="create-a-pfx-file"></a>Utwórz plik PFX
Wykonaj następujące polecenie z hello hello tym samym oknie, w którym wykonano makecert; Użyj hello tego samego hasła możesz używane toocreate hello certyfikatu:

    pvk2pfx -pvk MyCert.pvk -spc MyCert.cer -pfx MyCert.pfx -pi <password>

### <a name="import-hello-client-certificate-into-hello-personal-store"></a>Zaimportuj certyfikat klienta na powitania do magazynu osobistego hello
1. W Eksploratorze Windows, kliknij dwukrotnie **MyCert.pfx**.
2. W hello **Kreatora importu certyfikatów** wybierz **bieżącego użytkownika** i kliknij przycisk **dalej**.
3. Sprawdź ścieżkę pliku hello i kliknij przycisk **dalej**.
4. Wpisz hasło hello, pozostaw **obejmują wszystkie rozszerzone właściwości** zaznaczony, a następnie kliknij przycisk **dalej**.
5. Pozostaw **hello automatycznie wybierz magazyn certyfikatów [...]**  zaznaczony, a następnie kliknij przycisk **dalej**.
6. Kliknij przycisk **Zakończ** i **OK**.

### <a name="upload-hello-pfx-file-toohello-cloud-service"></a>Przekaż usługi chmury toohello pliku PFX hello
1. Przejdź toohello [Azure Portal](https://portal.azure.com).
2. Wybierz **usługi w chmurze**.
3. Wybierz usługi w chmurze hello utworzoną wcześniej hello podziału/Merge usługi.
4. Kliknij przycisk **certyfikaty** na powitania menu u góry.
5. Kliknij przycisk **przekazać** hello dolnym pasku.
6. Wybierz plik PFX hello i wprowadź hello tego samego hasła jak powyżej.
7. Po zakończeniu skopiuj odcisk palca certyfikatu hello z hello nowy wpis na liście hello.

### <a name="update-hello-service-configuration-file"></a>Aktualizuj plik konfiguracji usługi hello
Odcisk palca certyfikatu hello Wklej skopiowane powyżej do hello odcisk palca i wartości atrybutu z tych ustawień.
Dla roli proces roboczy hello:
   ```
    <Setting name="DataEncryptionPrimaryCertificateThumbprint" value="" />
    <Certificate name="DataEncryptionPrimary" thumbprint="" thumbprintAlgorithm="sha1" />
   ```

Dla roli sieci web hello:

   ```
    <Setting name="AdditionalTrustedRootCertificationAuthorities" value="" />
    <Setting name="AllowedClientCertificateThumbprints" value="" />
    <Setting name="DataEncryptionPrimaryCertificateThumbprint" value="" />
    <Certificate name="SSL" thumbprint="" thumbprintAlgorithm="sha1" />
    <Certificate name="CA" thumbprint="" thumbprintAlgorithm="sha1" />
    <Certificate name="DataEncryptionPrimary" thumbprint="" thumbprintAlgorithm="sha1" />
   ```

Zwróć uwagę, że wdrożeń produkcyjnych oddzielne certyfikaty powinny być używane dla hello urzędu certyfikacji, dla celów szyfrowania, hello certyfikatu serwera i certyfikatów klientów. Aby uzyskać szczegółowe instrukcje na to, zobacz [konfiguracji zabezpieczeń](sql-database-elastic-scale-split-merge-security-configuration.md).

## <a name="deploy-your-service"></a>Wdrażanie usługi
1. Przejdź toohello [portalu Azure](https://manage.windowsazure.com).
2. Kliknij przycisk hello **usługi w chmurze** powitania po lewej stronie, a następnie wybierz usługę w chmurze hello utworzony wcześniej.
3. Kliknij przycisk **pulpitu nawigacyjnego**.
4. Wybierz hello przemieszczania środowiska, a następnie kliknij przycisk **przekazania nowego wdrożenia przemieszczania**.
   
   ![Przemieszczania][3]
5. Okno dialogowe hello wprowadź etykietę wdrożenia. "Pakietu" i "Konfiguracja", kliknij przycisk "Z lokalnego" i wybierz polecenie hello **SplitMergeService.cspkg** plików i skonfigurowaną wcześniej pliku .cscfg.
6. Upewnij się, że pole wyboru hello **Wdróż, nawet jeśli co najmniej jedna rola zawiera pojedyncze wystąpienie** jest zaznaczony.
7. Kliknij przycisk znaczników hello we wdrożeniu hello toobegin prawy dolny hello. Oczekiwany tootake kilka toocomplete minut.

   ![Upload][4]

## <a name="troubleshoot-hello-deployment"></a>Rozwiązywanie problemów z wdrażaniem hello
W przypadku niepowodzenia toocome online roli sieci web prawdopodobnie jest to problem z konfiguracją zabezpieczeń hello. Sprawdź hello, że protokół SSL jest skonfigurowany zgodnie z powyższym opisem.

Jeśli swojej roli procesu roboczego nie powiedzie się toocome w trybie online, ale roli sieci web zakończy się powodzeniem, najprawdopodobniej jest problem z połączeniem bazy danych stanu toohello utworzony wcześniej.

* Upewnij się, że parametry połączenia hello w Twojej .cscfg są prawidłowe.
* Sprawdź, czy istnieją powitania serwera i bazy danych i hello identyfikator użytkownika i hasło są poprawne.
* Dla bazy danych SQL Azure hello parametry połączenia muszą mieć format hello:

   ```  
   Server=myservername.database.windows.net; Database=mydatabasename;User ID=myuserID; Password=mypassword; Encrypt=True; Connection Timeout=30
   ```

* Upewnij się, że nazwa serwera hello nie zaczyna się od **https://**.
* Upewnij się, że serwer bazy danych SQL Azure umożliwia tooit tooconnect usług Azure. toodo, otwórz https://manage.windowsazure.com, wybierz polecenie "Baz danych SQL" hello po lewej, kliknij przycisk "Serwery" u góry hello i wybierz Twój serwer. Kliknij przycisk **Konfiguruj** na powitania z góry i upewnij się, że hello **usług Azure** ustawioną zbyt "Yes". (Patrz wymagania wstępne hello sekcji u góry hello w tym artykule).

## <a name="test-hello-service-deployment"></a>Wdrożenie usługi hello testu
### <a name="connect-with-a-web-browser"></a>Połącz przy użyciu przeglądarki sieci web
Określ hello punktu końcowego sieci web usługi podziału scalania. Można je znaleźć w hello klasycznego portalu Azure przez przejście toohello **pulpitu nawigacyjnego** usługi w chmurze oraz pod **adres URL witryny** hello prawej strony. Zastąp **http://** z **https://** ponieważ hello domyślnych ustawień zabezpieczeń wyłączenie punktu końcowego hello HTTP. Strona hello obciążenia dla tego adresu URL w przeglądarce.

### <a name="test-with-powershell-scripts"></a>Testowanie za pomocą skryptów środowiska PowerShell
Wdrażanie Hello i środowiska można przetestować, uruchamiając hello uwzględnione przykładowe skrypty programu PowerShell.

pliki skryptów Hello uwzględnione są:

1. **SetupSampleSplitMergeEnvironment.ps1** — konfiguruje warstwy danych testu dla podziału/Merge (zobacz tabelę poniżej, aby uzyskać szczegółowy opis)
2. **ExecuteSampleSplitMerge.ps1** — wykonuje operacje testu dla testu hello warstwy danych (zobacz tabelę poniżej, aby uzyskać szczegółowy opis)
3. **GetMappings.ps1** — najwyższego poziomu przykładowy skrypt, który do drukowania hello bieżący stan hello niezależnego fragmentu mapowania.
4. **ShardManagement.psm1** -pomocnika skrypt, który opakowuje hello ShardManagement interfejsu API
5. **SqlDatabaseHelpers.psm1** -skryptu pomocnika do tworzenia i zarządzania bazy danych SQL
   
   <table style="width:100%">
     <tr>
       <th>Plik programu PowerShell</th>
       <th>Kroki</th>
     </tr>
     <tr>
       <th rowspan="5">SetupSampleSplitMergeEnvironment.ps1</th>
       <td>1.    Tworzy bazę danych Menedżera niezależnego fragmentu mapy</td>
     </tr>
     <tr>
       <td>2.    Tworzy 2 niezależnego fragmentu bazy danych.
     </tr>
     <tr>
       <td>3.    Tworzy mapę niezależnego fragmentu te bazy danych (usuwa wszystkie istniejące niezależnego fragmentu mapy na tych baz danych). </td>
     </tr>
     <tr>
       <td>4.    Tworzy tabelę małej przykładowej w obu odłamków hello i wypełnia hello tabeli w jednym z odłamków hello.</td>
     </tr>
     <tr>
       <td>5.    Deklaruje hello SchemaInfo hello podzielony na niezależne fragmenty tabeli.</td>
     </tr>
   </table>
   <table style="width:100%">
     <tr>
       <th>Plik programu PowerShell</th>
       <th>Kroki</th>
     </tr>
   <tr>
       <th rowspan="4">ExecuteSampleSplitMerge.ps1 </th>
       <td>1.    Wysyła podziału żądania toohello scalania podziału usługi sieci web frontonu, która dzieli połowa danych hello z hello pierwszego niezależnego fragmentu toohello drugi niezależnego fragmentu.</td>
     </tr>
     <tr>
       <td>2.    Ankiety hello frontonu sieci web dla hello podziału stan żądania i czeka, aż do zakończenia żądania hello.</td>
     </tr>
     <tr>
       <td>3.    Wysyła scalania żądania toohello scalania podziału usługi sieci web frontonu, które przenosi dane hello z hello drugi niezależnego fragmentu wstecz toohello pierwszego niezależnego fragmentu.</td>
     </tr>
     <tr>
       <td>4.    Ankiety hello frontonu sieci web dla stan żądania scalania hello i czeka, aż do zakończenia żądania hello.</td>
     </tr>
   </table>
   
## <a name="use-powershell-tooverify-your-deployment"></a>Użyj programu PowerShell tooverify wdrożenia
1. Otwórz nowe okno programu PowerShell i przejdź do katalogu toohello, którego pobrano hello scalania podziału pakietu, a następnie przejdź do katalogu "powershell" hello.
2. Tworzenie serwera bazy danych Azure SQL (lub wybierz istniejący serwer) której zostanie utworzona hello niezależnego fragmentu mapy manager i fragmentów.
   
   > [!NOTE]
   > Witaj SetupSampleSplitMergeEnvironment.ps1 skrypt tworzy tych baz danych na powitania tego samego serwera za pomocą prostego skryptu hello tookeep domyślne. To nie jest ograniczenie hello usługi scalania podziału samej siebie.
   >
   
   Nazwa logowania uwierzytelniania SQL z toohello dostęp do odczytu/zapisu, bazami danych będzie wymagana dla hello danych toomove usługi scalania podziału, a następnie mapować niezależnego fragmentu hello aktualizacji. Ponieważ uruchamia hello scalania podziału usługi w chmurze hello, go nie obsługuje obecnie zintegrowane uwierzytelnianie.
   
   Upewnij się, że hello Azure SQL server jest skonfigurowany tooallow dostępu z adresu IP hello maszyny hello uruchamianie tych skryptów. To ustawienie w obszarze hello Azure SQL server można znaleźć / configuration / dozwolone adresy IP.
3. Wykonanie hello SetupSampleSplitMergeEnvironment.ps1 skryptu toocreate hello próbki środowiska.
   
   Uruchomienie tego skryptu zostanie wymazać wszystkie istniejące dane zarządzania mapy niezależnego fragmentu struktury na powitania niezależnego fragmentu mapy manager w bazie danych i odłamków hello. Jeśli chcesz, aby zainicjować toore hello niezależnego fragmentu mapy lub odłamków może być przydatne toorerun hello skryptu.
   
   Przykładowy wiersz polecenia:

   ```   
     .\SetupSampleSplitMergeEnvironment.ps1 
   
         -UserName 'mysqluser' 
         -Password 'MySqlPassw0rd' 
         -ShardMapManagerServerName 'abcdefghij.database.windows.net'
   ```      
4. Wykonanie hello Getmappings.ps1 tooview hello mapowania skryptów znajdujące się obecnie w środowisku próbki hello.
   
   ```
     .\GetMappings.ps1 
   
         -UserName 'mysqluser' 
         -Password 'MySqlPassw0rd' 
         -ShardMapManagerServerName 'abcdefghij.database.windows.net'

   ```         
5. Wykonanie hello ExecuteSampleSplitMerge.ps1 skryptu tooexecute operację podziału (przenoszenie połowa danych hello na powitania pierwszego niezależnego fragmentu toohello drugi niezależnego fragmentu), a następnie operacji scalania (przenoszenie danych hello wstecz na powitania pierwszego niezależnego fragmentu). Skonfigurowanie protokołu SSL i wyłączyć punkt końcowy http powitania po lewej stronie, upewnij się, użyj punktu końcowego https:// hello.
   
   Przykładowy wiersz polecenia:

   ```   
     .\ExecuteSampleSplitMerge.ps1
   
         -UserName 'mysqluser' 
         -Password 'MySqlPassw0rd' 
         -ShardMapManagerServerName 'abcdefghij.database.windows.net' 
         -SplitMergeServiceEndpoint 'https://mysplitmergeservice.cloudapp.net' 
         -CertificateThumbprint '0123456789abcdef0123456789abcdef01234567'
   ```      
   
   Jeśli zostanie wyświetlony hello poniżej błąd, najprawdopodobniej jest problem z certyfikatem punkt końcowy sieci Web. Spróbuj nawiązać połączenie toohello punktu końcowego sieci Web z ulubionej przeglądarce sieci Web i sprawdź, czy błąd certyfikatu.
   
     ```
     Invoke-WebRequest : hello underlying connection was closed: Could not establish trust relationship for hello SSL/TLSsecure channel.
     ```
   
   Jeśli zakończyło się pomyślnie, hello dane wyjściowe powinny wyglądać podobnie jak poniżej hello:
   
   ```
   > .\ExecuteSampleSplitMerge.ps1 -UserName 'mysqluser' -Password 'MySqlPassw0rd' -ShardMapManagerServerName 'abcdefghij.database.windows.net' -SplitMergeServiceEndpoint 'http://mysplitmergeservice.cloudapp.net' -CertificateThumbprint 0123456789abcdef0123456789abcdef01234567
   > Sending split request
   > Began split operation with id dc68dfa0-e22b-4823-886a-9bdc903c80f3
   > Polling split-merge request status. Press Ctrl-C tooend
   > Progress: 0% | Status: Queued | Details: [Informational] Queued request
   > Progress: 5% | Status: Starting | Details: [Informational] Starting split-merge state machine for request.
   > Progress: 5% | Status: Starting | Details: [Informational] Performing data consistency checks on target     shards.
   > Progress: 20% | Status: CopyingReferenceTables | Details: [Informational] Moving reference tables from     source tootarget shard.
   > Progress: 20% | Status: CopyingReferenceTables | Details: [Informational] Waiting for reference tables copy     completion.
   > Progress: 20% | Status: CopyingReferenceTables | Details: [Informational] Moving reference tables from     source tootarget shard.
   > Progress: 44% | Status: CopyingShardedTables | Details: [Informational] Moving key range [100:110) of     Sharded tables
   > Progress: 44% | Status: CopyingShardedTables | Details: [Informational] Successfully copied key range     [100:110) for table [dbo].[MyShardedTable]
   > ...
   > ...
   > Progress: 90% | Status: Completing | Details: [Informational] Successfully deleted shardlets in table     [dbo].[MyShardedTable].
   > Progress: 90% | Status: Completing | Details: [Informational] Deleting any temp tables that were created     while processing hello request.
   > Progress: 100% | Status: Succeeded | Details: [Informational] Successfully processed request.
   > Sending merge request
   > Began merge operation with id 6ffc308f-d006-466b-b24e-857242ec5f66
   > Polling request status. Press Ctrl-C tooend
   > Progress: 0% | Status: Queued | Details: [Informational] Queued request
   > Progress: 5% | Status: Starting | Details: [Informational] Starting split-merge state machine for request.
   > Progress: 5% | Status: Starting | Details: [Informational] Performing data consistency checks on target     shards.
   > Progress: 20% | Status: CopyingReferenceTables | Details: [Informational] Moving reference tables from     source tootarget shard.
   > Progress: 44% | Status: CopyingShardedTables | Details: [Informational] Moving key range [100:110) of     Sharded tables
   > Progress: 44% | Status: CopyingShardedTables | Details: [Informational] Successfully copied key range     [100:110) for table [dbo].[MyShardedTable]
   > ...
   > ...
   > Progress: 90% | Status: Completing | Details: [Informational] Successfully deleted shardlets in table     [dbo].[MyShardedTable].
   > Progress: 90% | Status: Completing | Details: [Informational] Deleting any temp tables that were created     while processing hello request.
   > Progress: 100% | Status: Succeeded | Details: [Informational] Successfully processed request.
   > 
   ```
6. Poeksperymentuj z innymi typami danych! Opcjonalny parametr - ShardKeyType umożliwiający typ klucza hello toospecify wszystkie skrypty potrwać. Domyślnie Hello jest Int32, ale można również określić Int64, Guid lub dane binarne.

## <a name="create-requests"></a>Żądania utworzenia
można używać usługi Hello przy użyciu interfejsu użytkownika sieci web hello lub przez zaimportowanie i przy użyciu modułu SplitMerge.psm1 PowerShell hello, którego będzie przesyłanie żądań za pośrednictwem hello roli sieci web.

Usługa Hello można przenieść dane w tabelach podzielonej i tabele odwołań. Podzielony na niezależne fragmenty tabeli ma kolumny klucza dzielenia na fragmenty i ma inny wiersz danych na każdym niezależnego fragmentu. Nie jest podzielony na niezależne fragmenty tabeli odwołań tak, aby zawierał hello na każdym niezależnych sam wiersz danych. Tabele odwołań są przydatne w przypadku danych, które nie zmieniają się często, jest używane tooJOIN z tabelami podzielonej w zapytaniach.

W kolejności tooperform operacji scalania podziału należy zadeklarować hello podzielonej tabele i tabele odwołań, które chcesz przenieść toohave. Jest to realizowane przy użyciu hello **SchemaInfo** interfejsu API. Ten interfejs API jest hello **Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.Schema** przestrzeni nazw.

1. Dla każdej tabeli podzielonej, Utwórz **ShardedTableInfo** Obiekt opisujący nazwy schematu hello tabeli nadrzędnej (opcjonalne, domyślnie przyjmowana jest zbyt "właściciela"), hello nazwy tabeli i nazwę kolumny w tabeli zawierającej klucz dzielenia na fragmenty hello hello.
2. Dla każdej tabeli odniesienia należy utworzyć **ReferenceTableInfo** Obiekt opisujący nazwy schematu hello tabeli nadrzędnej (opcjonalne, domyślnie przyjmowana jest zbyt "właściciela") i hello nazwy tabeli.
3. Dodaj hello powyżej tooa obiektów TableInfo nowe **SchemaInfo** obiektu.
4. Pobierz tooa odwołanie **ShardMapManager** obiekt i wywołanie **GetSchemaInfoCollection**.
5. Dodaj hello **SchemaInfo** toohello **SchemaInfoCollection**, podanie nazwy mapy niezależnego fragmentu hello.

Na przykład może być widoczny w hello SetupSampleSplitMergeEnvironment.ps1 skryptu.

Hello usługi podziału scalania nie tworzy hello docelowej bazy danych (lub schemat dla wszystkich tabel w bazie danych hello). Musi być wstępnie utworzone przed wysłaniem żądania toohello usługi.

## <a name="troubleshooting"></a>Rozwiązywanie problemów
Witaj poniżej komunikat może zostać wyświetlony podczas uruchamiania hello przykładowe skrypty programu powershell:

   ```
   Invoke-WebRequest : hello underlying connection was closed: Could not establish trust relationship for hello SSL/TLS secure channel.
   ```

Ten błąd oznacza, że certyfikat SSL nie jest poprawnie skonfigurowany. Wykonaj instrukcje hello w sekcji "Łączenie z przeglądarką sieci web".

Jeśli nie można przesłać żądania może wystąpić błąd to:

```
[Exception] System.Data.SqlClient.SqlException (0x80131904): Could not find stored procedure 'dbo.InsertRequest'. 
```

W takim przypadku sprawdź plik konfiguracji, w szczególności hello ustawieniu **WorkerRoleSynchronizationStorageAccountConnectionString**. Ten błąd zazwyczaj oznacza, że ta rola procesu roboczego hello nie można zainicjować pomyślnie bazy danych metadanych hello przy pierwszym użyciu. 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-scale-configure-deploy-split-and-merge/allowed-services.png
[2]: ./media/sql-database-elastic-scale-configure-deploy-split-and-merge/manage.png
[3]: ./media/sql-database-elastic-scale-configure-deploy-split-and-merge/staging.png
[4]: ./media/sql-database-elastic-scale-configure-deploy-split-and-merge/upload.png
[5]: ./media/sql-database-elastic-scale-configure-deploy-split-and-merge/storage.png

