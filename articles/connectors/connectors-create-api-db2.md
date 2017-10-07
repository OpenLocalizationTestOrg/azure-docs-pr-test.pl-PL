---
title: "Łącznik hello DB2 aaaAdd w aplikacjach logiki | Dokumentacja firmy Microsoft"
description: "Omówienie łącznik DB2 z parametrami interfejsu API REST"
services: 
documentationcenter: 
author: gplarsen
manager: erikre
editor: 
tags: connectors
ms.assetid: 1c6b010c-beee-496d-943a-a99e168c99aa
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 09/26/2016
ms.author: plarsen; ladocs
ms.openlocfilehash: d836c61231d3c9cfdb30ff9c40a48b1718f3ffb9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-db2-connector"></a>Rozpoczynanie pracy z hello łącznik DB2
Łącznik usługi Microsoft dla bazy danych DB2 łączy przechowywane w bazie danych programu IBM DB2 tooresources Logic Apps. Ten łącznik obejmuje toocommunicate klienta firmy Microsoft, ze zdalnymi komputerami serwera bazy danych DB2 w sieci TCP/IP. Obejmuje chmury baz danych, takich jak dashDB IBM Bluemix lub IBM DB2 dla systemu Windows Azure wirtualizacji i baz danych za pomocą bramy danych lokalne powitania lokalnymi. Zobacz hello [obsługiwane listy](connectors-create-api-db2.md#supported-db2-platforms-and-versions) IBM DB2 platform i wersji (w tym temacie).

Łącznik Hello DB2 obsługuje hello następujące operacje bazy danych:

* Listy tabel bazy danych
* Odczyt przy użyciu wybierz jeden wiersz.
* Wszystkie wiersze, używając wybierz do odczytu
* Dodaj jeden wiersz za pomocą polecenia Wstaw
* Instrukcja ALTER jeden wiersz za pomocą aktualizacji
* Usuń jeden wiersz używanie opcji usuwania

W tym temacie pokazano, jak toouse hello łącznika w tooprocess aplikacji logiki bazy danych operacji.

toolearn więcej informacji na temat aplikacji logiki, zobacz [tworzenie aplikacji logiki](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="available-actions"></a>Dostępne akcje
Łącznik Hello DB2 obsługuje następujące akcje usługi logic aplikacji hello:

* GetTables
* GetRow
* Funkcja GetRows
* InsertRow
* UpdateRow
* DeleteRow

## <a name="list-tables"></a>Wyświetlenie listy tabel
Tworzenie aplikacji logiki do żadnej operacji składa się z wielu czynności wykonywanych przez hello portalu Microsoft Azure.

W aplikacji logiki hello możesz dodać akcji toolist tabele w bazie danych DB2. Witaj akcji powoduje, że hello instrukcji schema tooprocess bazy danych DB2 łącznika, takich jak `CALL SYSIBM.SQLTABLES`.

### <a name="create-a-logic-app"></a>Tworzenie aplikacji logiki
1. W hello **Azure start tablicy**, wybierz pozycję ** + ** (znak plus) **sieci Web i mobilność**, a następnie **aplikacji logiki**.
2. Wprowadź hello **nazwa**, takich jak `Db2getTables`, **subskrypcji**, **grupy zasobów**, **lokalizacji**, i **aplikacji Plan usługi**. Wybierz **toodashboard numeru Pin**, a następnie wybierz **Utwórz**.

### <a name="add-a-trigger-and-action"></a>Dodaj trigger i action
1. W hello **projektanta aplikacji logiki**, wybierz pozycję **puste LogicApp** w hello **szablony** listy.
2. W hello **wyzwalaczy** listy, wybierz **cyklu**. 
3. W hello **cyklu** wyzwalacza, wybierz opcję **Edytuj**, wybierz pozycję **częstotliwość** tooselect listy rozwijanej **dzień**, a następnie ustaw hello **Interwał** tootype **7**.  
4. Wybierz hello **+ nowy krok** , a następnie wybierz **Dodaj akcję**.
5. W hello **akcje** listy, wpisz `db2` w hello **Wyszukaj więcej akcji** pole edycji, a następnie wybierz **bazy danych DB2 — tabele Get (wersja zapoznawcza)**.
   
   ![](./media/connectors-create-api-db2/Db2connectorActions.png)  
6. W hello **bazy danych DB2 — tabele Get** okienko konfiguracji, wybierz opcję **wyboru** tooenable **Połącz za pośrednictwem bramy danych lokalnych**. Należy zauważyć, że ustawienia hello zmiany z lokalnych tooon chmury.
   
   * Wpisz wartość **serwera**, w formie hello adres lub alias numer portu dwukropkiem. Na przykład wpisz `ibmserver01:50000`.
   * Wpisz wartość **bazy danych**. Na przykład wpisz `nwind`.
   * Wybierz wartość dla **uwierzytelniania**. Na przykład wybierz **podstawowe**.
   * Wpisz wartość **Username**. Na przykład wpisz `db2admin`.
   * Wpisz wartość **hasło**. Na przykład wpisz `Password1`.
   * Wybierz wartość dla **bramy**. Na przykład wybierz **datagateway01**.
7. Wybierz **Utwórz**, a następnie wybierz **zapisać**. 
   
    ![](./media/connectors-create-api-db2/Db2connectorOnPremisesDataGatewayConnection.png)
8. W hello **Db2getTables** bloku, w ramach hello **wszystkie elementy** w obszarze **Podsumowanie**, wybierz hello wymienione pierwszego elementu (Uruchom ostatniego).
9. W hello **Uruchom aplikację logiki** bloku, wybierz opcję **Uruchom szczegóły**. W ramach hello **akcji** listy, wybierz **Get_tables**. Zobacz wartość hello **stan**, które powinny być **zakończyło się pomyślnie**. Wybierz hello **dane wejściowe, łącza** tooview hello w danych wejściowych. Wybierz hello **dane wyjściowe link**i wyświetla widok hello; który powinna zawierać listę tabel.
   
   ![](./media/connectors-create-api-db2/Db2connectorGetTablesLogicAppRunOutputs.png)

## <a name="create-hello-connections"></a>Utwórz połączenia hello
Ten łącznik obsługuje połączenia toodatabases obsługiwana lokalnie i w chmurze hello przy użyciu hello następujące właściwości połączenia. 

| Właściwość | Opis |
| --- | --- |
| serwer |Wymagany. Przyjmuje wartość ciągu, która reprezentuje adres TCP/IP lub alias w formacie IPv4 lub IPv6, a następnie (rozdzielany średnikami) przez numer portu TCP/IP. |
| Bazy danych |Wymagany. Przyjmuje wartość ciągu, która reprezentuje DRDA relacyjne nazwę bazy danych (RDBNAM). Bazy danych DB2 dla z/OS akceptuje ciąg 16-bajtowych (baza danych jest znany jako IBM DB2 dla lokalizacji z/OS). Bazy danych DB2 dla i5/OS akceptuje ciąg 18-bajtowych (baza danych jest nazywany IBM DB2 dla i relacyjnej bazy danych). Bazy danych DB2 dla LUW akceptuje ciąg 8-bajtowych. |
| Uwierzytelnianie |Opcjonalny. Akceptuje wartości elementu listy, Basic lub systemu Windows (kerberos). |
| nazwa użytkownika |Wymagany. Akceptuje wartości ciągu. Bazy danych DB2 dla z/OS akceptuje ciąg 8-bajtowych. Bazy danych DB2 dla i akceptuje ciąg 10-bajtowych. Bazy danych DB2 dla systemu Linux lub UNIX akceptuje ciąg 8-bajtowych. Bazy danych DB2 dla systemu Windows akceptuje ciąg 30-bajtowych. |
| hasło |Wymagany. Akceptuje wartości ciągu. |
| Bramy |Wymagany. Akceptuje wartości elementu listy, reprezentujący hello lokalnych danych bramy zdefiniowany tooLogic aplikacji w grupie magazynów hello. |

## <a name="create-hello-on-premises-gateway-connection"></a>Utwórz lokalne powitania połączenia bramy
Ten łącznik można uzyskać dostępu do bazy danych DB2 lokalnie przy użyciu bramy lokalne powitania. Zobacz Tematy bramy, aby uzyskać więcej informacji. 

1. W hello **bram** okienko konfiguracji, wybierz opcję **wyboru** tooenable **Połącz za pośrednictwem bramy**. Należy zauważyć, że ustawienia hello zmiany z lokalnych tooon chmury.
2. Wpisz wartość **serwera**, w formie hello adres lub alias numer portu dwukropkiem. Na przykład wpisz `ibmserver01:50000`.
3. Wpisz wartość **bazy danych**. Na przykład wpisz `nwind`.
4. Wybierz wartość dla **uwierzytelniania**. Na przykład wybierz **podstawowe**.
5. Wpisz wartość **Username**. Na przykład wpisz `db2admin`.
6. Wpisz wartość **hasło**. Na przykład wpisz `Password1`.
7. Wybierz wartość dla **bramy**. Na przykład wybierz **datagateway01**.
8. Wybierz **Utwórz** toocontinue. 
   
    ![](./media/connectors-create-api-db2/Db2connectorOnPremisesDataGatewayConnection.png)

## <a name="create-hello-cloud-connection"></a>Tworzenie połączenia chmury hello
Ten łącznik można uzyskać dostępu do bazy danych DB2 chmury. 

1. W hello **bram** okienko konfiguracji, pozostaw hello **wyboru** wyłączone (które nie były kliknięte) **Połącz za pośrednictwem bramy**. 
2. Wpisz wartość **nazwa połączenia**. Na przykład wpisz `hisdemo2`.
3. Wpisz wartość **nazwę serwera bazy danych DB2**, w formie hello adres lub alias numer portu dwukropkiem. Na przykład wpisz `hisdemo2.cloudapp.net:50000`.
4. Wpisz wartość **Nazwa bazy danych DB2**. Na przykład wpisz `nwind`.
5. Wpisz wartość **Username**. Na przykład wpisz `db2admin`.
6. Wpisz wartość **hasło**. Na przykład wpisz `Password1`.
7. Wybierz **Utwórz** toocontinue. 
   
    ![](./media/connectors-create-api-db2/Db2connectorCloudConnection.png)

## <a name="fetch-all-rows-using-select"></a>Pobierz wszystkie wiersze, używając wybierz
Można zdefiniować toofetch działania aplikacji logiki wszystkie wiersze w tabeli bazy danych DB2. Takie jak poleca tooprocess łącznika hello instrukcję wybierz bazy danych DB2 `SELECT * FROM AREA`.

### <a name="create-a-logic-app"></a>Tworzenie aplikacji logiki
1. W hello **Azure start tablicy**, wybierz pozycję ** + ** (znak plus) **sieci Web i mobilność**, a następnie **aplikacji logiki**.
2. Wprowadź hello **nazwa**, takich jak `Db2getRows`, **subskrypcji**, **grupy zasobów**, **lokalizacji**, i **aplikacji Plan usługi**. Wybierz **toodashboard numeru Pin**, a następnie wybierz **Utwórz**.

### <a name="add-a-trigger-and-action"></a>Dodaj trigger i action
1. W hello **projektanta aplikacji logiki**, wybierz pozycję **puste LogicApp** w hello **szablony** listy.
2. W hello **wyzwalaczy** listy, wybierz **cyklu**. 
3. W hello **cyklu** wyzwalacza, wybierz **Edytuj**, wybierz pozycję **częstotliwość** tooselect listy rozwijanej **dzień**, a następnie wybierz ** Interwał** tootype **7**. 
4. Wybierz hello **+ nowy krok** , a następnie wybierz **Dodaj akcję**.
5. W hello **akcje** listy, wpisz `db2` w hello **Wyszukaj więcej akcji** pole edycji, a następnie wybierz **bazy danych DB2 — Get wierszy (wersja zapoznawcza)**.
6. W hello **Pobierz wiersze (wersja zapoznawcza)** akcji wybierz **zmienić połączenie**.
7. W hello **połączeń** okienko konfiguracji, wybierz opcję **Utwórz nowy**. 
   
    ![](./media/connectors-create-api-db2/Db2connectorNewConnection.png)
8. W hello **bram** okienko konfiguracji, pozostaw hello **wyboru** wyłączone (które nie były kliknięte) **Połącz za pośrednictwem bramy**.
   
   * Wpisz wartość **nazwa połączenia**. Na przykład wpisz `HISDEMO2`.
   * Wpisz wartość **nazwę serwera bazy danych DB2**, w formie hello adres lub alias numer portu dwukropkiem. Na przykład wpisz `HISDEMO2.cloudapp.net:50000`.
   * Wpisz wartość **Nazwa bazy danych DB2**. Na przykład wpisz `NWIND`.
   * Wpisz wartość **Username**. Na przykład wpisz `db2admin`.
   * Wpisz wartość **hasło**. Na przykład wpisz `Password1`.
9. Wybierz **Utwórz** toocontinue.
   
    ![](./media/connectors-create-api-db2/Db2connectorCloudConnection.png)
10. W hello **nazwy tabeli** listy, wybierz opcję hello **Strzałka w dół**, a następnie wybierz **obszaru**.
11. Opcjonalnie wybierz **Pokaż zaawansowane opcje** toospecify opcje zapytania.
12. Wybierz pozycję **Zapisz**. 
    
    ![](./media/connectors-create-api-db2/Db2connectorGetRowsTableName.png)
13. W hello **Db2getRows** bloku, w ramach hello **wszystkie elementy** w obszarze **Podsumowanie**, wybierz hello wymienione pierwszego elementu (Uruchom ostatniego).
14. W hello **Uruchom aplikację logiki** bloku, wybierz opcję **Uruchom szczegóły**. W ramach hello **akcji** listy, wybierz **Get_rows**. Zobacz wartość hello **stan**, które powinny być **zakończyło się pomyślnie**. Wybierz hello **dane wejściowe, łącza** tooview hello w danych wejściowych. Wybierz hello **dane wyjściowe link**i wyświetla widok hello; który powinna zawierać listę wierszy.
    
    ![](./media/connectors-create-api-db2/Db2connectorGetRowsOutputs.png)

## <a name="add-one-row-using-insert"></a>Dodaj jeden wiersz za pomocą polecenia Wstaw
Można zdefiniować logiki aplikacji akcji tooadd jeden wiersz w tabeli bazy danych DB2. Ta akcja powoduje, że hello tooprocess łącznik DB2 Wstaw instrukcję, takich jak `INSERT INTO AREA (AREAID, AREADESC, REGIONID) VALUES ('99999', 'Area 99999', 102)`.

### <a name="create-a-logic-app"></a>Tworzenie aplikacji logiki
1. W hello **Azure start tablicy**, wybierz pozycję ** + ** (znak plus) **sieci Web i mobilność**, a następnie **aplikacji logiki**.
2. Wprowadź hello **nazwa**, takich jak `Db2insertRow`, **subskrypcji**, **grupy zasobów**, **lokalizacji**, i **aplikacji Plan usługi**. Wybierz **toodashboard numeru Pin**, a następnie wybierz **Utwórz**.

### <a name="add-a-trigger-and-action"></a>Dodaj trigger i action
1. W hello **projektanta aplikacji logiki**, wybierz pozycję **puste LogicApp** w hello **szablony** listy.
2. W hello **wyzwalaczy** listy, wybierz **cyklu**. 
3. W hello **cyklu** wyzwalacza, wybierz **Edytuj**, wybierz pozycję **częstotliwość** tooselect listy rozwijanej **dzień**, a następnie wybierz ** Interwał** tootype **7**. 
4. Wybierz hello **+ nowy krok** , a następnie wybierz **Dodaj akcję**.
5. W hello **akcje** listy, wpisz **bazy danych db2** w hello **Wyszukaj więcej akcji** pole edycji, a następnie wybierz **bazy danych DB2 — Wstaw wiersz (wersja zapoznawcza)**.
6. W hello **bazy danych DB2 — Wstaw wiersz (wersja zapoznawcza)** akcji wybierz **zmienić połączenie**. 
7. W hello **połączeń** okienko konfiguracji, wybierz połączenie. Na przykład wybierz **hisdemo2**.
   
    ![](./media/connectors-create-api-db2/Db2connectorChangeConnection.png)
8. W hello **nazwy tabeli** listy, wybierz opcję hello **Strzałka w dół**, a następnie wybierz **obszaru**.
9. Wprowadź wartości dla wszystkich wymaganych kolumn (zobacz czerwoną gwiazdką). Na przykład wpisz `99999` dla **AREAID**, typ `Area 99999`i wpisz `102` dla **REGIONID**. 
10. Wybierz pozycję **Zapisz**.
    
    ![](./media/connectors-create-api-db2/Db2connectorInsertRowValues.png)
11. W hello **Db2insertRow** bloku, w ramach hello **wszystkie elementy** w obszarze **Podsumowanie**, wybierz hello wymienione pierwszego elementu (Uruchom ostatniego).
12. W hello **Uruchom aplikację logiki** bloku, wybierz opcję **Uruchom szczegóły**. W ramach hello **akcji** listy, wybierz **Get_rows**. Zobacz wartość hello **stan**, które powinny być **zakończyło się pomyślnie**. Wybierz hello **dane wejściowe, łącza** tooview hello w danych wejściowych. Wybierz hello **dane wyjściowe link**i wyświetla widok hello; obejmującą hello nowego wiersza.
    
    ![](./media/connectors-create-api-db2/Db2connectorInsertRowOutputs.png)

## <a name="fetch-one-row-using-select"></a>Pobieranie przy użyciu wybierz jeden wiersz.
Można zdefiniować logiki aplikacji akcji toofetch jeden wiersz w tabeli bazy danych DB2. Ta akcja powoduje, że tooprocess łącznika hello instrukcję wybierz bazy danych DB2 gdzie takich jak `SELECT FROM AREA WHERE AREAID = '99999'`.

### <a name="create-a-logic-app"></a>Tworzenie aplikacji logiki
1. W hello **Azure start tablicy**, wybierz pozycję ** + ** (znak plus) **sieci Web i mobilność**, a następnie **aplikacji logiki**.
2. Wprowadź hello **nazwa** (np. "**Db2getRow**"), **subskrypcji**, **grupy zasobów**, **lokalizacji**, i **planu usługi App Service**. Wybierz **toodashboard numeru Pin**, a następnie wybierz **Utwórz**.

### <a name="add-a-trigger-and-action"></a>Dodaj trigger i action
1. W hello **projektanta aplikacji logiki**, wybierz pozycję **puste LogicApp** w hello **szablony** listy. 
2. W hello **wyzwalaczy** listy, wybierz **cyklu**. 
3. W hello **cyklu** wyzwalacza, wybierz **Edytuj**, wybierz pozycję **częstotliwość** tooselect listy rozwijanej **dzień**, a następnie wybierz ** Interwał** tootype **7**. 
4. Wybierz hello **+ nowy krok** , a następnie wybierz **Dodaj akcję**.
5. W hello **akcje** listy, wpisz **bazy danych db2** w hello **Wyszukaj więcej akcji** pole edycji, a następnie wybierz **bazy danych DB2 — Get wierszy (wersja zapoznawcza)**.
6. W hello **Pobierz wiersze (wersja zapoznawcza)** akcji wybierz **zmienić połączenie**. 
7. W hello **połączeń** okienko konfiguracje, wybrać istniejące połączenie. Na przykład wybierz **hisdemo2**.
   
    ![](./media/connectors-create-api-db2/Db2connectorChangeConnection.png)
8. W hello **nazwy tabeli** listy, wybierz opcję hello **Strzałka w dół**, a następnie wybierz **obszaru**.
9. Wprowadź wartości dla wszystkich wymaganych kolumn (zobacz czerwoną gwiazdką). Na przykład wpisz `99999` dla **AREAID**. 
10. Opcjonalnie wybierz **Pokaż zaawansowane opcje** toospecify opcje zapytania.
11. Wybierz pozycję **Zapisz**. 
    
    ![](./media/connectors-create-api-db2/Db2connectorGetRowValues.png)
12. W hello **Db2getRow** bloku, w ramach hello **wszystkie elementy** w obszarze **Podsumowanie**, wybierz hello wymienione pierwszego elementu (Uruchom ostatniego).
13. W hello **Uruchom aplikację logiki** bloku, wybierz opcję **Uruchom szczegóły**. W ramach hello **akcji** listy, wybierz **Get_rows**. Zobacz wartość hello **stan**, które powinny być **zakończyło się pomyślnie**. Wybierz hello **dane wejściowe, łącza** tooview hello w danych wejściowych. Wybierz hello **dane wyjściowe link**i wyświetla widok hello; obejmującą wiersza.
    
    ![](./media/connectors-create-api-db2/Db2connectorGetRowOutputs.png)

## <a name="change-one-row-using-update"></a>Zmień jeden wiersz za pomocą aktualizacji
Można zdefiniować logiki aplikacji akcji toochange jeden wiersz w tabeli bazy danych DB2. Ta akcja powoduje, że tooprocess łącznika hello instrukcję aktualizacji bazy danych DB2 takich jak `UPDATE AREA SET AREAID = '99999', AREADESC = 'Area 99999', REGIONID = 102)`.

### <a name="create-a-logic-app"></a>Tworzenie aplikacji logiki
1. W hello **Azure start tablicy**, wybierz pozycję ** + ** (znak plus) **sieci Web i mobilność**, a następnie **aplikacji logiki**.
2. Wprowadź hello **nazwa**, takich jak `Db2updateRow`, **subskrypcji**, **grupy zasobów**, **lokalizacji**, i **aplikacji Plan usługi**. Wybierz **toodashboard numeru Pin**, a następnie wybierz **Utwórz**.

### <a name="add-a-trigger-and-action"></a>Dodaj trigger i action
1. W hello **projektanta aplikacji logiki**, wybierz pozycję **puste LogicApp** w hello **szablony** listy.
2. W hello **wyzwalaczy** listy, wybierz **cyklu**. 
3. W hello **cyklu** wyzwalacza, wybierz **Edytuj**, wybierz pozycję **częstotliwość** tooselect listy rozwijanej **dzień**, a następnie wybierz ** Interwał** tootype **7**. 
4. Wybierz hello **+ nowy krok** , a następnie wybierz **Dodaj akcję**.
5. W hello **akcje** listy, wpisz **bazy danych db2** w hello **Wyszukaj więcej akcji** pole edycji, a następnie wybierz **bazy danych DB2 — aktualizacja wiersza (wersja zapoznawcza)**.
6. W hello **bazy danych DB2 — aktualizacja wiersza (wersja zapoznawcza)** akcji wybierz **zmienić połączenie**. 
7. W hello **połączeń** konfiguracje okienku wybierz tooselect istniejącego połączenia. Na przykład wybierz **hisdemo2**.
   
    ![](./media/connectors-create-api-db2/Db2connectorChangeConnection.png)
8. W hello **nazwy tabeli** listy, wybierz opcję hello **Strzałka w dół**, a następnie wybierz **obszaru**.
9. Wprowadź wartości dla wszystkich wymaganych kolumn (zobacz czerwoną gwiazdką). Na przykład wpisz `99999` dla **AREAID**, typ `Updated 99999`i wpisz `102` dla **REGIONID**. 
10. Wybierz pozycję **Zapisz**. 
    
    ![](./media/connectors-create-api-db2/Db2connectorUpdateRowValues.png)
11. W hello **Db2updateRow** bloku, w ramach hello **wszystkie elementy** w obszarze **Podsumowanie**, wybierz hello wymienione pierwszego elementu (Uruchom ostatniego).
12. W hello **Uruchom aplikację logiki** bloku, wybierz opcję **Uruchom szczegóły**. W ramach hello **akcji** listy, wybierz **Get_rows**. Zobacz wartość hello **stan**, które powinny być **zakończyło się pomyślnie**. Wybierz hello **dane wejściowe, łącza** tooview hello w danych wejściowych. Wybierz hello **dane wyjściowe link**i wyświetla widok hello; obejmującą hello nowego wiersza.
    
    ![](./media/connectors-create-api-db2/Db2connectorUpdateRowOutputs.png)

## <a name="remove-one-row-using-delete"></a>Usuń jeden wiersz używanie opcji usuwania
Można zdefiniować logiki aplikacji akcji tooremove jeden wiersz w tabeli bazy danych DB2. Ta akcja powoduje, że tooprocess łącznika hello instrukcję usunąć bazy danych DB2 takich jak `DELETE FROM AREA WHERE AREAID = '99999'`.

### <a name="create-a-logic-app"></a>Tworzenie aplikacji logiki
1. W hello **Azure start tablicy**, wybierz pozycję ** + ** (znak plus) **sieci Web i mobilność**, a następnie **aplikacji logiki**.
2. Wprowadź hello **nazwa**, takich jak `Db2deleteRow`, **subskrypcji**, **grupy zasobów**, **lokalizacji**, i **aplikacji Plan usługi**. Wybierz **toodashboard numeru Pin**, a następnie wybierz **Utwórz**.

### <a name="add-a-trigger-and-action"></a>Dodaj trigger i action
1. W hello **projektanta aplikacji logiki**, wybierz pozycję **puste LogicApp** w hello **szablony** listy. 
2. W hello **wyzwalaczy** listy, wybierz **cyklu**. 
3. W hello **cyklu** wyzwalacza, wybierz **Edytuj**, wybierz pozycję **częstotliwość** tooselect listy rozwijanej **dzień**, a następnie wybierz ** Interwał** tootype **7**. 
4. Wybierz hello **+ nowy krok** , a następnie wybierz **Dodaj akcję**.
5. W hello **akcje** listy, wybierz **bazy danych db2** w hello **Wyszukaj więcej akcji** pole edycji, a następnie wybierz **bazy danych DB2 — Usuń wiersz (wersja zapoznawcza)**.
6. W hello **bazy danych DB2 — Usuń wiersz (wersja zapoznawcza)** akcji wybierz **zmienić połączenie**. 
7. W hello **połączeń** okienko konfiguracje, wybrać istniejące połączenie. Na przykład wybierz **hisdemo2**.
   
    ![](./media/connectors-create-api-db2/Db2connectorChangeConnection.png)
8. W hello **nazwy tabeli** listy, wybierz opcję hello **Strzałka w dół**, a następnie wybierz **obszaru**.
9. Wprowadź wartości dla wszystkich wymaganych kolumn (zobacz czerwoną gwiazdką). Na przykład wpisz `99999` dla **AREAID**. 
10. Wybierz pozycję **Zapisz**. 
    
    ![](./media/connectors-create-api-db2/Db2connectorDeleteRowValues.png)
11. W hello **Db2deleteRow** bloku, w ramach hello **wszystkie elementy** w obszarze **Podsumowanie**, wybierz hello wymienione pierwszego elementu (Uruchom ostatniego).
12. W hello **Uruchom aplikację logiki** bloku, wybierz opcję **Uruchom szczegóły**. W ramach hello **akcji** listy, wybierz **Get_rows**. Zobacz wartość hello **stan**, które powinny być **zakończyło się pomyślnie**. Wybierz hello **dane wejściowe, łącza** tooview hello w danych wejściowych. Wybierz hello **dane wyjściowe link**i wyświetla widok hello; obejmującą hello usunąć wiersza.
    
    ![](./media/connectors-create-api-db2/Db2connectorDeleteRowOutputs.png)

## <a name="supported-db2-platforms-and-versions"></a>Obsługiwane platformy bazy danych DB2 i wersje
Ten łącznik obsługuje powitania po IBM DB2 platform i wersji, a także produkty zgodne IBM DB2 (np. IBM Bluemix dashDB), które obsługują SQL Menedżera dostępu (SQLAM) rozproszonych relacyjnej bazy danych architektury DRDA () w wersji 10 lub 11:

* IBM DB2 dla 11.1 z/OS
* IBM DB2 dla z/OS 10.1
* IBM DB2 dla i 7.3
* IBM DB2 dla i 7.2
* IBM DB2 dla i 7.1
* IBM DB2 LUW 11
* IBM DB2 dla LUW 10.5

## <a name="connector-specific-details"></a>Szczegóły dotyczące łącznika

Wyświetl wszystkie wyzwalacze i akcje zdefiniowane w hello swagger i zobacz też żadnych limitów w hello [szczegóły łącznika](/connectors/db2/). 

## <a name="next-steps"></a>Następne kroki
[Tworzenie aplikacji logiki](../logic-apps/logic-apps-create-a-logic-app.md). Eksploruj hello innych dostępnych łączników w aplikacjach logiki w naszym [listy interfejsów API](apis-list.md).

