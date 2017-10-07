---
title: "Łącznik programu Informix hello aaaAdd w aplikacjach logiki | Dokumentacja firmy Microsoft"
description: "Omówienie programu Informix łącznika z parametrami interfejsu API REST"
services: 
documentationcenter: 
author: gplarsen
manager: anneta
editor: 
tags: connectors
ms.assetid: ca2393f0-3073-4dc2-8438-747f5bc59689
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 09/26/2016
ms.author: plarsen; ladocs
ms.openlocfilehash: 7a163e2ebf00fa3109b93e34845d922c2174a48d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-informix-connector"></a>Rozpoczynanie pracy z hello łącznika programu Informix
Łącznik usługi Microsoft dla programu Informix łączy przechowywane w bazie danych programu IBM Informix tooresources Logic Apps. Łącznik programu Informix Hello zawiera Microsoft toocommunicate tooremote Informix serwera komputery w sieci TCP/IP. Obejmuje chmury baz danych, takich jak IBM Informix dla systemu Windows Azure wirtualizacji i baz danych za pomocą bramy danych lokalne powitania lokalnymi. Zobacz hello [obsługiwane listy](connectors-create-api-informix.md#supported-informix-platforms-and-versions) IBM Informix platform i wersji (w tym temacie).

Witaj, łącznik obsługuje hello następujące operacje bazy danych:

* Listy tabel bazy danych
* Odczyt przy użyciu wybierz jeden wiersz.
* Wszystkie wiersze, używając wybierz do odczytu
* Dodaj jeden wiersz za pomocą polecenia Wstaw
* Instrukcja ALTER jeden wiersz za pomocą aktualizacji
* Usuń jeden wiersz używanie opcji usuwania

W tym temacie pokazano, jak toouse hello łącznika w tooprocess aplikacji logiki bazy danych operacji.

toolearn więcej informacji na temat aplikacji logiki, zobacz [tworzenie aplikacji logiki](../logic-apps/logic-apps-create-a-logic-app.md).

## <a name="available-actions"></a>Dostępne akcje
Ten łącznik obsługuje następujące akcje usługi logic app hello:

* Getables
* GetRow
* Funkcja GetRows
* InsertRow
* UpdateRow
* DeleteRow

## <a name="list-tables"></a>Wyświetlenie listy tabel
Tworzenie aplikacji logiki do żadnej operacji składa się z wielu czynności wykonywanych przez hello portalu Microsoft Azure.

W aplikacji logiki hello można dodać akcję toolist tabele w bazie danych programu Informix. Ta akcja powoduje, że tooprocess łącznika hello instrukcję schematu Informix takich jak `CALL SYSIBM.SQLTABLES`.

### <a name="create-a-logic-app"></a>Tworzenie aplikacji logiki
1. W hello **Azure start tablicy**, wybierz pozycję  **+**  (znak plus) **sieci Web i mobilność**, a następnie **aplikacji logiki**.
2. Wprowadź hello **nazwa**, takich jak `InformixgetTables`, **subskrypcji**, **grupy zasobów**, **lokalizacji**, i **aplikacji Plan usługi**. Wybierz **toodashboard numeru Pin**, a następnie wybierz **Utwórz**.

### <a name="add-a-trigger-and-action"></a>Dodaj trigger i action
1. W hello **projektanta aplikacji logiki**, wybierz pozycję **puste LogicApp** w hello **szablony** listy.
2. W hello **wyzwalaczy** listy, wybierz **cyklu**. 
3. W hello **cyklu** wyzwalacza, wybierz **Edytuj**, wybierz pozycję **częstotliwość** tooselect listy rozwijanej **dzień**, a następnie wybierz  **Interwał** tootype **7**.  
4. Wybierz hello **+ nowy krok** , a następnie wybierz **Dodaj akcję**.
5. W hello **akcje** listy, wpisz **informix** w hello **Wyszukaj więcej akcji** pole edycji, a następnie wybierz **Informix - Get tabele (wersja zapoznawcza)**.
   
   ![](./media/connectors-create-api-informix/InformixconnectorActions.png)  
6. W hello **Informix - Get tabel** okienko konfiguracji, wybierz opcję **wyboru** tooenable **Połącz za pośrednictwem bramy danych lokalnych**. Należy zauważyć, że ustawienia hello zmiany z lokalnych tooon chmury.
   
   * Wpisz wartość **serwera**, w formie hello adres lub alias numer portu dwukropkiem. Na przykład wpisz `ibmserver01:9089`.
   * Wpisz wartość **bazy danych**. Na przykład wpisz `nwind`.
   * Wybierz wartość dla **uwierzytelniania**. Na przykład wybierz **podstawowe**.
   * Wpisz wartość **Username**. Na przykład wpisz `informix`.
   * Wpisz wartość **hasło**. Na przykład wpisz `Password1`.
   * Wybierz wartość dla **bramy**. Na przykład wybierz **datagateway01**.
7. Wybierz **Utwórz**, a następnie wybierz **zapisać**. 
   
    ![](./media/connectors-create-api-informix/InformixconnectorOnPremisesDataGatewayConnection.png)
8. W hello **InformixgetTables** bloku, w ramach hello **wszystkie elementy** w obszarze **Podsumowanie**, wybierz hello wymienione pierwszego elementu (Uruchom ostatniego).
9. W hello **Uruchom aplikację logiki** bloku, wybierz opcję **Uruchom szczegóły**. W ramach hello **akcji** listy, wybierz **Get_tables**. Zobacz wartość hello **stan**, które powinny być **zakończyło się pomyślnie**. Wybierz hello **dane wejściowe, łącza** tooview hello w danych wejściowych. Wybierz hello **dane wyjściowe link**i wyświetla widok hello; który powinna zawierać listę tabel.
   
   ![](./media/connectors-create-api-informix/InformixconnectorGetTablesLogicAppRunOutputs.png)

## <a name="create-hello-connections"></a>Utwórz połączenia hello
Ten łącznik obsługuje połączenia toodatabase lokalnie i w chmurze hello przy użyciu hello następujące właściwości połączenia. 

| Właściwość | Opis |
| --- | --- |
| serwer |Wymagany. Akceptuje wartości ciągu reprezentujący adres TCP/IP lub alias w formacie IPv4 lub IPv6, a następnie (-średnikami) przez numer portu TCP/IP. |
| Bazy danych |Wymagany. Akceptuje wartości ciągu reprezentujący DRDA relacyjne nazwę bazy danych (RDBNAM). Informix akceptuje ciąg 128-bajtowych (baza danych jest znany jako nazwa bazy danych programu IBM Informix (dbname)). |
| Uwierzytelnianie |Opcjonalny. Akceptuje wartości elementu listy, Basic lub systemu Windows (kerberos). |
| nazwa użytkownika |Wymagany. Akceptuje wartości ciągu. |
| hasło |Wymagany. Akceptuje wartości ciągu. |
| Bramy |Wymagany. Akceptuje wartości elementu listy, reprezentujący hello lokalnych danych bramy zdefiniowany tooLogic aplikacji w grupie magazynów hello. |

## <a name="create-hello-on-premises-gateway-connection"></a>Utwórz lokalne powitania połączenia bramy
Tego łącznika można uzyskać dostępu do bazy danych programu Informix lokalnej za pomocą bramy danych lokalne powitania. Zobacz Tematy bramy, aby uzyskać więcej informacji. 

1. W hello **bram** okienko konfiguracji, wybierz opcję **wyboru** tooenable **Połącz za pośrednictwem bramy**. Zobacz powitalne ustawienia zmiany z lokalnych tooon chmury.
2. Wpisz wartość **serwera**, w formie hello adres lub alias numer portu dwukropkiem. Na przykład wpisz `ibmserver01:9089`.
3. Wpisz wartość **bazy danych**. Na przykład wpisz `nwind`.
4. Wybierz wartość dla **uwierzytelniania**. Na przykład wybierz **podstawowe**.
5. Wpisz wartość **Username**. Na przykład wpisz `informix`.
6. Wpisz wartość **hasło**. Na przykład wpisz `Password1`.
7. Wybierz wartość dla **bramy**. Na przykład wybierz **datagateway01**.
8. Wybierz **Utwórz** toocontinue. 
   
    ![](./media/connectors-create-api-informix/InformixconnectorOnPremisesDataGatewayConnection.png)

## <a name="create-hello-cloud-connection"></a>Tworzenie połączenia chmury hello
Ten łącznik mogą uzyskiwać dostęp do bazy danych programu Informix chmurę. 

1. W hello **bram** okienko konfiguracji, pozostaw hello **wyboru** wyłączone (które nie były kliknięte) **Połącz za pośrednictwem bramy**. 
2. Wpisz wartość **nazwa połączenia**. Na przykład wpisz `hisdemo2`.
3. Wpisz wartość **nazwa serwera programu Informix**, w formie hello adres lub alias numer portu dwukropkiem. Na przykład wpisz `hisdemo2.cloudapp.net:9089`.
4. Wpisz wartość **Nazwa bazy danych programu Informix**. Na przykład wpisz `nwind`.
5. Wpisz wartość **Username**. Na przykład wpisz `informix`.
6. Wpisz wartość **hasło**. Na przykład wpisz `Password1`.
7. Wybierz **Utwórz** toocontinue. 
   
    ![](./media/connectors-create-api-informix/InformixconnectorCloudConnection.png)

## <a name="fetch-all-rows-using-select"></a>Pobierz wszystkie wiersze, używając wybierz
Możesz utworzyć toofetch działania aplikacji logiki wszystkie wiersze w tabeli Informix hello. Ta akcja powoduje, że tooprocess łącznika hello instrukcję Informix SELECT takich jak `SELECT * FROM AREA`.

### <a name="create-a-logic-app"></a>Tworzenie aplikacji logiki
1. W hello **Azure start tablicy**, wybierz pozycję  **+**  (znak plus) **sieci Web i mobilność**, a następnie **aplikacji logiki**.
2. Wprowadź hello **nazwa** (np. "**InformixgetRows**"), **subskrypcji**, **grupy zasobów**, **lokalizacji**, i **planu usługi App Service**. Wybierz **toodashboard numeru Pin**, a następnie wybierz **Utwórz**.

### <a name="add-a-trigger-and-action"></a>Dodaj trigger i action
1. W hello **projektanta aplikacji logiki**, wybierz pozycję **puste LogicApp** w hello **szablony** listy.
2. W hello **wyzwalaczy** listy, wybierz **cyklu**. 
3. W hello **cyklu** wyzwalacza, wybierz **Edytuj**, wybierz pozycję **częstotliwość** tooselect listy rozwijanej **dzień**, a następnie wybierz  **Interwał** tootype **7**. 
4. Wybierz hello **+ nowy krok** , a następnie wybierz **Dodaj akcję**.
5. W hello **akcje** listy, wpisz **informix** w hello **Wyszukaj więcej akcji** pole edycji, a następnie wybierz **Informix - Get wierszy (wersja zapoznawcza)** .
6. W hello **Pobierz wiersze (wersja zapoznawcza)** akcji wybierz **zmienić połączenie**.
7. W hello **połączeń** okienko konfiguracji, wybierz opcję **Utwórz nowy**. 
   
    ![](./media/connectors-create-api-informix/InformixconnectorNewConnection.png)
8. W hello **bram** okienko konfiguracji, pozostaw hello **wyboru** wyłączone (które nie były kliknięte) **Połącz za pośrednictwem bramy**.
   
   * Wpisz wartość **nazwa połączenia**. Na przykład wpisz `HISDEMO2`.
   * Wpisz wartość **nazwa serwera programu Informix**, w formie hello adres lub alias numer portu dwukropkiem. Na przykład wpisz `HISDEMO2.cloudapp.net:9089`.
   * Wpisz wartość **Nazwa bazy danych programu Informix**. Na przykład wpisz `NWIND`.
   * Wpisz wartość **Username**. Na przykład wpisz `informix`.
   * Wpisz wartość **hasło**. Na przykład wpisz `Password1`.
9. Wybierz **Utwórz** toocontinue.
   
    ![](./media/connectors-create-api-informix/InformixconnectorCloudConnection.png)
10. W hello **nazwy tabeli** listy, wybierz opcję hello **Strzałka w dół**, a następnie wybierz **obszaru**.
11. Opcjonalnie wybierz **Pokaż zaawansowane opcje** toospecify opcje zapytania.
12. Wybierz pozycję **Zapisz**. 
    
    ![](./media/connectors-create-api-informix/InformixconnectorGetRowsTableName.png)
13. W hello **InformixgetRows** bloku, w ramach hello **wszystkie elementy** w obszarze **Podsumowanie**, wybierz hello wymienione pierwszego elementu (Uruchom ostatniego).
14. W hello **Uruchom aplikację logiki** bloku, wybierz opcję **Uruchom szczegóły**. W ramach hello **akcji** listy, wybierz **Get_rows**. Zobacz wartość hello **stan**, które powinny być **zakończyło się pomyślnie**. Wybierz hello **dane wejściowe, łącza** tooview hello w danych wejściowych. Wybierz hello **dane wyjściowe link**i wyświetla widok hello; który powinna zawierać listę wierszy.
    
    ![](./media/connectors-create-api-informix/InformixconnectorGetRowsOutputs.png)

## <a name="add-one-row-using-insert"></a>Dodaj jeden wiersz za pomocą polecenia Wstaw
Możesz utworzyć logiki aplikacji akcji tooadd jeden wiersz w tabeli programu Informix. Ta akcja powoduje, że tooprocess łącznika hello instrukcji Informix INSERT, takich jak `INSERT INTO AREA (AREAID, AREADESC, REGIONID) VALUES ('99999', 'Area 99999', 102)`.

### <a name="create-a-logic-app"></a>Tworzenie aplikacji logiki
1. W hello **Azure start tablicy**, wybierz pozycję  **+**  (znak plus) **sieci Web i mobilność**, a następnie **aplikacji logiki**.
2. Wprowadź hello **nazwa**, takich jak `InformixinsertRow`, **subskrypcji**, **grupy zasobów**, **lokalizacji**, i **aplikacji Plan usługi**. Wybierz **toodashboard numeru Pin**, a następnie wybierz **Utwórz**.

### <a name="add-a-trigger-and-action"></a>Dodaj trigger i action
1. W hello **projektanta aplikacji logiki**, wybierz pozycję **puste LogicApp** w hello **szablony** listy.
2. W hello **wyzwalaczy** listy, wybierz **cyklu**. 
3. W hello **cyklu** wyzwalacza, wybierz **Edytuj**, wybierz pozycję **częstotliwość** tooselect listy rozwijanej **dzień**, a następnie wybierz  **Interwał** tootype **7**. 
4. Wybierz hello **+ nowy krok** , a następnie wybierz **Dodaj akcję**.
5. W hello **akcje** listy, wpisz **informix** w hello **Wyszukaj więcej akcji** pole edycji, a następnie wybierz **Informix - Wstaw wiersz (wersja zapoznawcza)**.
6. W hello **Pobierz wiersze (wersja zapoznawcza)** akcji wybierz **zmienić połączenie**. 
7. W hello **połączeń** okienko konfiguracji, wybierz opcję tooselect jako połączenie. Na przykład wybierz **hisdemo2**.
   
    ![](./media/connectors-create-api-informix/InformixconnectorChangeConnection.png)
8. W hello **nazwy tabeli** listy, wybierz opcję hello **Strzałka w dół**, a następnie wybierz **obszaru**.
9. Wprowadź wartości dla wszystkich wymaganych kolumn (zobacz czerwoną gwiazdką). Na przykład wpisz `99999` dla **AREAID**, typ `Area 99999`i wpisz `102` dla **REGIONID**. 
10. Wybierz pozycję **Zapisz**.
    
    ![](./media/connectors-create-api-informix/InformixconnectorInsertRowValues.png)
11. W hello **InformixinsertRow** bloku, w ramach hello **wszystkie elementy** w obszarze **Podsumowanie**, wybierz hello wymienione pierwszego elementu (Uruchom ostatniego).
12. W hello **Uruchom aplikację logiki** bloku, wybierz opcję **Uruchom szczegóły**. W ramach hello **akcji** listy, wybierz **Get_rows**. Zobacz wartość hello **stan**, które powinny być **zakończyło się pomyślnie**. Wybierz hello **dane wejściowe, łącza** tooview hello w danych wejściowych. Wybierz hello **dane wyjściowe link**i wyświetla widok hello; obejmującą hello nowego wiersza.
    
    ![](./media/connectors-create-api-informix/InformixconnectorInsertRowOutputs.png)

## <a name="fetch-one-row-using-select"></a>Pobieranie przy użyciu wybierz jeden wiersz.
Możesz utworzyć logiki aplikacji akcji toofetch jeden wiersz w tabeli programu Informix. Ta akcja powoduje, że tooprocess łącznika hello instrukcję Informix wybierz gdzie takich jak `SELECT FROM AREA WHERE AREAID = '99999'`.

### <a name="create-a-logic-app"></a>Tworzenie aplikacji logiki
1. W hello **Azure start tablicy**, wybierz pozycję  **+**  (znak plus) **sieci Web i mobilność**, a następnie **aplikacji logiki**.
2. Wprowadź hello **nazwa**, takich jak `InformixgetRow`, **subskrypcji**, **grupy zasobów**, **lokalizacji**, i **aplikacji Plan usługi**. Wybierz **toodashboard numeru Pin**, a następnie wybierz **Utwórz**.

### <a name="add-a-trigger-and-action"></a>Dodaj trigger i action
1. W hello **projektanta aplikacji logiki**, wybierz pozycję **puste LogicApp** w hello **szablony** listy.
2. W hello **wyzwalaczy** listy, wybierz **cyklu**. 
3. W hello **cyklu** wyzwalacza, wybierz **Edytuj**, wybierz pozycję **częstotliwość** tooselect listy rozwijanej **dzień**, a następnie wybierz  **Interwał** tootype **7**. 
4. Wybierz hello **+ nowy krok** , a następnie wybierz **Dodaj akcję**.
5. W hello **akcje** listy, wpisz **informix** w hello **Wyszukaj więcej akcji** pole edycji, a następnie wybierz **Informix - Get wierszy (wersja zapoznawcza)** .
6. W hello **Pobierz wiersze (wersja zapoznawcza)** akcji wybierz **zmienić połączenie**. 
7. W hello **połączeń** konfiguracje okienku wybierz tooselect istniejącego połączenia. Na przykład wybierz **hisdemo2**.
   
    ![](./media/connectors-create-api-informix/InformixconnectorChangeConnection.png)
8. W hello **nazwy tabeli** listy, wybierz opcję hello **Strzałka w dół**, a następnie wybierz **obszaru**.
9. Wprowadź wartości dla wszystkich wymaganych kolumn (zobacz czerwoną gwiazdką). Na przykład wpisz `99999` dla **AREAID**. 
10. Opcjonalnie wybierz **Pokaż zaawansowane opcje** toospecify opcje zapytania.
11. Wybierz pozycję **Zapisz**. 
    
    ![](./media/connectors-create-api-informix/InformixconnectorGetRowValues.png)
12. W hello **InformixgetRow** bloku, w ramach hello **wszystkie elementy** w obszarze **Podsumowanie**, wybierz hello wymienione pierwszego elementu (Uruchom ostatniego).
13. W hello **Uruchom aplikację logiki** bloku, wybierz opcję **Uruchom szczegóły**. W ramach hello **akcji** listy, wybierz **Get_rows**. Zobacz wartość hello **stan**, które powinny być **zakończyło się pomyślnie**. Wybierz hello **dane wejściowe, łącza** tooview hello w danych wejściowych. Wybierz hello **dane wyjściowe link**i wyświetla widok hello; obejmującą wiersza.
    
    ![](./media/connectors-create-api-informix/InformixconnectorGetRowOutputs.png)

## <a name="change-one-row-using-update"></a>Zmień jeden wiersz za pomocą aktualizacji
Możesz utworzyć logiki aplikacji akcji toochange jeden wiersz w tabeli programu Informix. Ta akcja powoduje, że hello łącznika tooprocess instrukcji Informix UPDATE, takich jak `UPDATE AREA SET AREAID = '99999', AREADESC = 'Area 99999', REGIONID = 102)`.

### <a name="create-a-logic-app"></a>Tworzenie aplikacji logiki
1. W hello **Azure start tablicy**, wybierz pozycję  **+**  (znak plus) **sieci Web i mobilność**, a następnie **aplikacji logiki**.
2. Wprowadź hello **nazwa**, takich jak `InformixupdateRow`, **subskrypcji**, **grupy zasobów**, **lokalizacji**, i **aplikacji Plan usługi**. Wybierz **toodashboard numeru Pin**, a następnie wybierz **Utwórz**.

### <a name="add-a-trigger-and-action"></a>Dodaj trigger i action
1. W hello **projektanta aplikacji logiki**, wybierz pozycję **puste LogicApp** w hello **szablony** listy.
2. W hello **wyzwalaczy** listy, wybierz **cyklu**. 
3. W hello **cyklu** wyzwalacza, wybierz **Edytuj**, wybierz pozycję **częstotliwość** tooselect listy rozwijanej **dzień**, a następnie wybierz  **Interwał** tootype **7**. 
4. Wybierz hello **+ nowy krok** , a następnie wybierz **Dodaj akcję**.
5. W hello **akcje** listy, wpisz **informix** w hello **Wyszukaj więcej akcji** pole edycji, a następnie wybierz **Informix — aktualizacja wiersza (wersja zapoznawcza)**.
6. W hello **Pobierz wiersze (wersja zapoznawcza)** akcji wybierz **zmienić połączenie**. 
7. W hello **połączeń** konfiguracje okienku wybierz tooselect istniejącego połączenia. Na przykład wybierz **hisdemo2**.
   
    ![](./media/connectors-create-api-informix/InformixconnectorChangeConnection.png)
8. W hello **nazwy tabeli** listy, wybierz opcję hello **Strzałka w dół**, a następnie wybierz **obszaru**.
9. Wprowadź wartości dla wszystkich wymaganych kolumn (zobacz czerwoną gwiazdką). Na przykład wpisz `99999` dla **AREAID**, typ `Updated 99999`i wpisz `102` dla **REGIONID**. 
10. Wybierz pozycję **Zapisz**. 
    
    ![](./media/connectors-create-api-informix/InformixconnectorUpdateRowValues.png)
11. W hello **InformixupdateRow** bloku, w ramach hello **wszystkie elementy** w obszarze **Podsumowanie**, wybierz hello wymienione pierwszego elementu (Uruchom ostatniego).
12. W hello **Uruchom aplikację logiki** bloku, wybierz opcję **Uruchom szczegóły**. W ramach hello **akcji** listy, wybierz **Get_rows**. Zobacz wartość hello **stan**, które powinny być **zakończyło się pomyślnie**. Wybierz hello **dane wejściowe, łącza** tooview hello w danych wejściowych. Wybierz hello **dane wyjściowe link**i wyświetla widok hello; obejmującą hello nowego wiersza.
    
    ![](./media/connectors-create-api-informix/InformixconnectorUpdateRowOutputs.png)

## <a name="remove-one-row-using-delete"></a>Usuń jeden wiersz używanie opcji usuwania
Możesz utworzyć logiki aplikacji akcji tooremove jeden wiersz w tabeli programu Informix. Ta akcja powoduje, że tooprocess łącznika hello instrukcję usunąć Informix takich jak `DELETE FROM AREA WHERE AREAID = '99999'`.

### <a name="create-a-logic-app"></a>Tworzenie aplikacji logiki
1. W hello **Azure start tablicy**, wybierz pozycję  **+**  (znak plus) **sieci Web i mobilność**, a następnie **aplikacji logiki**.
2. Wprowadź hello **nazwa**, takich jak `InformixdeleteRow`, **subskrypcji**, **grupy zasobów**, **lokalizacji**, i **aplikacji Plan usługi**. Wybierz **toodashboard numeru Pin**, a następnie wybierz **Utwórz**.

### <a name="add-a-trigger-and-action"></a>Dodaj trigger i action
1. W hello **projektanta aplikacji logiki**, wybierz pozycję **puste LogicApp** w hello **szablony** listy.
2. W hello **wyzwalaczy** listy, wybierz **cyklu**. 
3. W hello **cyklu** wyzwalacza, wybierz **Edytuj**, wybierz pozycję **częstotliwość** tooselect listy rozwijanej **dzień**, a następnie wybierz  **Interwał** tootype **7**. 
4. Wybierz hello **+ nowy krok** , a następnie wybierz **Dodaj akcję**.
5. W hello **akcje** listy, wpisz **informix** w hello **Wyszukaj więcej akcji** pole edycji, a następnie wybierz **Informix - Usuń wiersz (wersja zapoznawcza)**.
6. W hello **Pobierz wiersze (wersja zapoznawcza)** akcji wybierz **zmienić połączenie**. 
7. W hello **połączeń** okienko konfiguracje, wybrać istniejące połączenie. Na przykład wybierz **hisdemo2**.
   
    ![](./media/connectors-create-api-informix/InformixconnectorChangeConnection.png)
8. W hello **nazwy tabeli** listy, wybierz opcję hello **Strzałka w dół**, a następnie wybierz **obszaru**.
9. Wprowadź wartości dla wszystkich wymaganych kolumn (zobacz czerwoną gwiazdką). Na przykład wpisz `99999` dla **AREAID**. 
10. Wybierz pozycję **Zapisz**. 
    
    ![](./media/connectors-create-api-informix/InformixconnectorDeleteRowValues.png)
11. W hello **InformixdeleteRow** bloku, w ramach hello **wszystkie elementy** w obszarze **Podsumowanie**, wybierz hello wymienione pierwszego elementu (Uruchom ostatniego).
12. W hello **Uruchom aplikację logiki** bloku, wybierz opcję **Uruchom szczegóły**. W ramach hello **akcji** listy, wybierz **Get_rows**. Zobacz wartość hello **stan**, które powinny być **zakończyło się pomyślnie**. Wybierz hello **dane wejściowe, łącza** tooview hello w danych wejściowych. Wybierz hello **dane wyjściowe link**i wyświetla widok hello; obejmującą hello usunąć wiersza.
    
    ![](./media/connectors-create-api-informix/InformixconnectorDeleteRowOutputs.png)

## <a name="supported-informix-platforms-and-versions"></a>Obsługiwane platformy Informix i wersje
Ten łącznik obsługuje następujące wersje programu IBM Informix po skonfigurowaniu hello połączeń klienckich toosupport rozproszonych relacyjnej bazy danych architektury DRDA ().

* IBM Informix 12.1
* IBM Informix 11,7

## <a name="connector-specific-details"></a>Szczegóły dotyczące łącznika

Wyświetl wszystkie wyzwalacze i akcje zdefiniowane w hello swagger i zobacz też żadnych limitów w hello [szczegóły łącznika](/connectors/informix/). 

## <a name="next-steps"></a>Następne kroki
[Tworzenie aplikacji logiki](../logic-apps/logic-apps-create-a-logic-app.md). Eksploruj hello innych dostępnych łączników w aplikacjach logiki w naszym [listy interfejsów API](apis-list.md).

