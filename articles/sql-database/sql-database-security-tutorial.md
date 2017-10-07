---
title: aaaSecure bazy danych Azure SQL | Dokumentacja firmy Microsoft
description: "Dowiedz się więcej o toosecure techniki i funkcje bazy danych Azure SQL."
services: sql-database
documentationcenter: 
author: DRediske
manager: jhubbard
editor: 
tags: 
ms.assetid: 
ms.service: sql-database
ms.custom: mvc,security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 06/28/2017
ms.author: daredis
ms.openlocfilehash: 1450d633d6f65faf1b8a2dc0dc7dfe996fb0719d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="secure-your-azure-sql-database"></a>Zabezpieczenia bazy danych Azure SQL

Baza danych SQL zabezpiecza dane poprzez ograniczenie przy użyciu reguł zapory, wymagających tooprove użytkowników, tożsamości i autoryzacji toodata za pośrednictwem członkostwa na podstawie ról i uprawnień, a także za pomocą mechanizmów uwierzytelniania tooyour dostępu do bazy danych zabezpieczenia na poziomie wiersza i maskowania danych dynamicznych.

Można zwiększyć hello ochrony bazy danych przed złośliwymi użytkownikami lub nieautoryzowanego dostępu, wystarczy kilka prostych kroków. W tym samouczku dowiesz się: 

> [!div class="checklist"]
> * Konfigurowanie reguł zapory poziomu serwera dla serwera w hello portalu Azure
> * Konfigurowanie reguł zapory na poziomie bazy danych dla bazy danych przy użyciu narzędzia SSMS
> * Połącz tooyour bazy danych przy użyciu ciągu bezpiecznego połączenia
> * Zarządzanie dostępem użytkowników
> * Ochrona danych za pomocą szyfrowania
> * Włączanie inspekcji bazy danych SQL
> * Włączyć wykrywanie zagrożeń bazy danych SQL

Jeśli nie masz subskrypcji platformy Azure, [utworzyć bezpłatne konto](https://azure.microsoft.com/free/) przed rozpoczęciem.

## <a name="prerequisites"></a>Wymagania wstępne

toocomplete tego samouczka, upewnij się, że masz następujące hello:

- Hello zainstalowana najnowsza wersja [programu SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) (SSMS). 
- Zainstalowany program Microsoft Excel
- Utworzone usługi Azure SQL server i bazy danych — zobacz [tworzenie bazy danych Azure SQL w portalu Azure hello](sql-database-get-started-portal.md), [tworzenia pojedynczej bazy danych Azure SQL przy użyciu interfejsu wiersza polecenia Azure hello](sql-database-get-started-cli.md), i [Utwórz pojedynczy SQL Azure bazy danych przy użyciu programu PowerShell](sql-database-get-started-powershell.md). 

## <a name="log-in-toohello-azure-portal"></a>Zaloguj się za toohello portalu Azure

Zaloguj się za toohello [portalu Azure](https://portal.azure.com/).

## <a name="create-a-server-level-firewall-rule-in-hello-azure-portal"></a>Utworzyć regułę zapory poziomu serwera w hello portalu Azure

Baz danych są chronione przez zaporę Windows na platformie Azure. Domyślnie wszystkie połączenia toohello serwera i hello bazy danych wewnątrz powitania serwera są odrzucane, z wyjątkiem połączeń z innymi usługami Azure. Aby uzyskać więcej informacji, zobacz [reguły zapory poziomu serwera i bazy danych na poziomie bazy danych SQL Azure](sql-database-firewall-configure.md).

Najbezpieczniejszą konfigurację Hello jest tooset tooOFF "Zezwalaj na dostęp do usług tooAzure". Jeśli potrzebujesz tooconnect toohello z bazy danych z maszyny Wirtualnej platformy Azure lub usługę w chmurze, należy utworzyć [zastrzeżonego adresu IP](../virtual-network/virtual-networks-reserved-public-ip.md) i umożliwiają tylko hello zastrzeżone IP address dostęp przez zaporę Windows hello. 

Wykonaj te kroki toocreate [regułę zapory poziomu serwera bazy danych SQL](sql-database-firewall-configure.md) dla połączeń tooallow serwera z określonego adresu IP. 

> [!NOTE]
> Po utworzeniu przykładowej bazy danych na platformie Azure przy użyciu jednej z poprzednich samouczki hello lub poradniki Szybki Start i są wykonywania tego samouczka na komputerze z hello tego samego adresu IP jego znajdował się, gdy udał przez te samouczki, można pominąć ten krok jako będą mieć utworzone reguły zapory poziomu serwera.
>

1. Kliknij przycisk **baz danych SQL** z hello lewym menu kliknij hello bazy danych i chcesz tooconfigure reguły zapory powitania dla na powitania **baz danych SQL** strony. Witaj strona przeglądu otwartym bazy danych przedstawiający hello w pełni kwalifikowana nazwa serwera (takich jak **mynewserver 20170313.database.windows.net**) i udostępnia opcje dla dalszej konfiguracji.

      ![reguła zapory serwera](./media/sql-database-security-tutorial/server-firewall-rule.png) 

2. Kliknij przycisk **ustawić Zapora serwera** na powitania narzędzi, jak pokazano na poprzedniej ilustracji hello. Witaj **ustawienia zapory** zostanie otwarta strona hello bazy danych SQL Server. 

3. Kliknij przycisk **Dodaj adres IP klienta** na hello narzędzi tooadd hello publiczny adres IP portalu toohello podłączonego komputera hello z lub ręcznie wprowadzić hello reguły zapory, a następnie kliknij przycisk **zapisać**.

      ![ustawianie reguły zapory serwera](./media/sql-database-security-tutorial/server-firewall-rule-set.png) 

4. Kliknij przycisk **OK** , a następnie kliknij przycisk hello **X** tooclose hello **ustawienia zapory** strony.

Teraz możesz połączyć tooany powitania serwera bazy danych z hello określony adres IP lub zakres adresów IP.

> [!NOTE]
> Usługa SQL Database nawiązuje komunikację na porcie 1433. Jeśli próbujesz tooconnect z sieci firmowej, ruch wychodzący przez port 1433 może nie być dozwolone przez zaporę w sieci. Jeśli tak, nie będzie serwera bazy danych SQL Azure tooyour stanie tooconnect, chyba że dział IT otwiera port 1433.
>

## <a name="create-a-database-level-firewall-rule-using-ssms"></a>Utworzyć regułę zapory poziomu bazy danych przy użyciu narzędzia SSMS

Reguły zapory poziomu bazy danych pozwalają toocreate ustawienia innej zapory dla różnych baz danych w ramach hello tej samej logicznej zapory serwera i toocreate reguł, które można przenosić — co oznacza, że należy wykonać hello bazy danych, podczas [trybu failover ](sql-database-geo-replication-overview.md) zamiast przechowywane na powitania serwera SQL. Reguły zapory poziomu bazy danych może być skonfigurowany za pomocą instrukcji języka Transact-SQL lub tylko po skonfigurowaniu hello pierwszą regułę zapory poziomu serwera. Aby uzyskać więcej informacji, zobacz [reguły zapory poziomu serwera i bazy danych na poziomie bazy danych SQL Azure](sql-database-firewall-configure.md).

Wykonuje te czynności toocreate reguły zapory dotyczące bazy danych.

1. Połącz tooyour bazy danych, na przykład za pomocą [programu SQL Server Management Studio](./sql-database-connect-query-ssms.md).

2. W Eksploratorze obiektów kliknij prawym przyciskiem myszy hello bazy danych ma tooadd reguły dla zapory i kliknij przycisk **nowe zapytanie**. Puste zapytanie zostanie otwarte okno czyli tooyour połączenia bazy danych.

3. W oknie zapytania hello zmodyfikować hello IP address tooyour publicznego adresu IP, a następnie wykonaj hello następujące zapytania:

    ```sql
    EXECUTE sp_set_database_firewall_rule N'Example DB Rule','0.0.0.4','0.0.0.4';
    ```

4. Na pasku narzędzi hello, kliknij przycisk **Execute** reguły zapory hello toocreate.

## <a name="view-how-tooconnect-an-application-tooyour-database-using-a-secure-connection-string"></a>Wyświetl jak tooconnect tooyour aplikacji bazy danych przy użyciu ciągu bezpiecznego połączenia

tooensure bezpiecznego zaszyfrowanego połączenia między aplikacji klienckiej i bazy danych SQL, ciąg połączenia hello ma toobe skonfigurowany tak, aby:

- Żądanie połączenia szyfrowanego i
- toonot zaufania hello certyfikatu serwera. 

Ustanawia połączenie przy użyciu zabezpieczeń TLS (Transport Layer) i zmniejsza zagrożenie hello man-in--middle. Można uzyskać poprawnie skonfigurowane parametry połączenia bazy danych SQL, aby obsługiwany klient sterowniki z hello portalu Azure pokazany dla ADO.net w tym zrzucie ekranu.

1. Wybierz **baz danych SQL** z menu po lewej stronie powitania i kliknij bazę danych na powitania **baz danych SQL** strony.

2. Na powitania **omówienie** stron dla bazy danych, kliknij przycisk **Pokaż parametry połączenia bazy danych**.

3. Przejrzyj hello pełną **ADO.NET** parametry połączenia.

    ![Parametry połączenia sterownika ADO.NET](./media/sql-database-security-tutorial/adonet-connection-string.png)

## <a name="creating-database-users"></a>Tworzenie bazy danych użytkowników

Przed utworzeniem żadnych użytkowników, należy najpierw wybrać jedną z dwóch typów uwierzytelniania obsługiwanych przez bazę danych SQL Azure: 

**Uwierzytelnianie SQL**, który używa nazwy użytkownika i hasła do logowania i użytkowników, którzy są prawidłowe tylko w hello kontekst określonej bazy danych w ramach serwera logicznego. 

**Uwierzytelniania usługi Azure Active Directory**, który używa tożsamości zarządzanych przez usługę Azure Active Directory. 

Jeśli chcesz, aby toouse [usługi Azure Active Directory](./sql-database-aad-authentication.md) tooauthenticate w bazie danych SQL, musi istnieć wypełnione usługi Azure Active Directory, zanim będzie można kontynuować.

Wykonaj te kroki toocreate użytkownika za pomocą uwierzytelniania SQL:

1. Połącz tooyour bazy danych, na przykład za pomocą [programu SQL Server Management Studio](./sql-database-connect-query-ssms.md) przy użyciu poświadczeń administratora serwera.

2. W Eksploratorze obiektów kliknij prawym przyciskiem myszy hello bazę danych tooadd nowego użytkownika na kliknij **nowe zapytanie**. Puste zapytanie zostanie otwarte okno czyli połączonych toohello wybranej bazy danych.

3. W oknie zapytania hello wprowadź hello następujące zapytanie:

    ```sql
    CREATE USER ApplicationUser WITH PASSWORD = 'YourStrongPassword1';
    ```

4. Na pasku narzędzi hello, kliknij przycisk **Execute** toocreate hello użytkownika.

5. Domyślnie program hello użytkownika połączenie toohello bazy danych, ale nie ma uprawnienia zapisu lub tooread danych. toogrant toohello te uprawnienia nowo utworzony użytkownik, wykonaj następujące dwa polecenia w nowym oknie zapytania hello

    ```sql
    ALTER ROLE db_datareader ADD MEMBER ApplicationUser;
    ALTER ROLE db_datawriter ADD MEMBER ApplicationUser;
    ```

Jest najlepszym toocreate praktyki te konta bez uprawnień administratora na powitania bazy danych tooconnect poziomu tooyour bazy danych, chyba że potrzebne tooexecute administratora zadania, takie jak tworzenie nowych użytkowników. Zapoznaj się z tematem hello [samouczek usługi Azure Active Directory](./sql-database-aad-authentication-configure.md) na temat tooauthenticate przy użyciu usługi Azure Active Directory.


## <a name="protect-your-data-with-encryption"></a>Ochrona danych za pomocą szyfrowania

Azure SQL Database przezroczystego szyfrowania danych (funkcji TDE) automatycznie szyfruje dane przechowywane, bez konieczności wprowadzania żadnych zmian toohello podczas uzyskiwania dostępu do hello zaszyfrowanych bazy danych aplikacji. W przypadku nowo utworzonego baz danych funkcji TDE jest domyślnie włączone. tooenable funkcji TDE dla bazy danych lub tooverify, który funkcji TDE jest włączone, wykonaj następujące kroki:

1. Wybierz **baz danych SQL** z menu po lewej stronie powitania i kliknij bazę danych na powitania **baz danych SQL** strony. 

2. Polecenie **przezroczystego szyfrowania danych** strony konfiguracji hello tooopen dla funkcji TDE.

    ![Przezroczyste szyfrowanie danych](./media/sql-database-security-tutorial/transparent-data-encryption-enabled.png)

3. W razie potrzeby ustaw **szyfrowanie danych** tooON i kliknij przycisk **zapisać**.

proces szyfrowania Hello jest uruchamiany w tle hello. Możesz monitorować postęp hello przy użyciu połączenia bazy danych tooSQL [programu SQL Server Management Studio](./sql-database-connect-query-ssms.md) badając kolumny encryption_state hello hello `sys.dm_database_encryption_keys` widoku.

## <a name="enable-sql-database-auditing-if-necessary"></a>Włączanie inspekcji bazy danych SQL, w razie potrzeby

Usługa Azure SQL Database Auditing śledzi zdarzenia bazy danych i zapisuje je tooan dziennik inspekcji na koncie magazynu Azure. Inspekcja pomaga zachować zgodność z przepisami, analizować aktywność bazy danych oraz uzyskać wgląd w odchylenia i anomalie, które mogą wskazywać potencjalne naruszenie zabezpieczeń. Wykonaj te kroki toocreate domyślne zasady inspekcji bazy danych SQL:

1. Wybierz **baz danych SQL** z menu po lewej stronie powitania i kliknij bazę danych na powitania **baz danych SQL** strony. 

2. W bloku ustawienia hello, wybierz **Inspekcja i wykrywanie zagrożeń**. Powiadomienie, że inspekcję na poziomie serwera jest diabled i że istnieje **wyświetlić ustawienia serwera** łącze pozwala tooview lub zmodyfikować ustawienia inspekcji serwera hello w tym kontekście.

    ![Inspekcja bloku](./media/sql-database-security-tutorial/auditing-get-started-settings.png)

3. Jeśli wolisz tooenable inspekcji typu (lub lokalizacji?) inne niż hello określona na poziomie serwera hello, Włącz **ON** inspekcji i wybierz polecenie hello **obiektu Blob** typu inspekcji. Po włączeniu inspekcji obiektu Blob serwera inspekcji bazy danych skonfigurowane hello będą istniały równolegle powitania serwera obiektu Blob inspekcji.

    ![Włączanie inspekcji](./media/sql-database-security-tutorial/auditing-get-started-turn-on.png)

4. Wybierz **szczegóły magazynu** hello tooopen bloku magazynu dzienników inspekcji. Wybierz hello kontem magazynu platformy Azure, gdzie zostaną zapisane dzienniki i hello okres przechowywania, po którym hello będą usuwane stare dzienniki, następnie kliknij przycisk **OK** u dołu hello. 

   > [!TIP]
   > Użyj hello samo konto magazynu dla wszystkich hello tooget inspekcji bazy danych maksymalne wykorzystanie możliwości inspekcji hello raporty szablonów.
   > 

5. Kliknij pozycję **Zapisz**.

> [!IMPORTANT]
> Jeśli chcesz toocustomize hello inspekcji zdarzeń, można to zrobić za pomocą programu PowerShell lub interfejsu API REST — Zobacz hello [automatyzacji (programu PowerShell / interfejsu API REST)](sql-database-auditing.md#subheading-7) sekcji, aby uzyskać więcej informacji.
>

## <a name="enable-sql-database-threat-detection"></a>Włączyć wykrywanie zagrożeń bazy danych SQL

Wykrywanie zagrożeń udostępnia nową warstwę zabezpieczeń, co umożliwia klientom toodetect i odpowiadać toopotential zagrożeń w miarę ich występowania, zapewniając alerty zabezpieczeń w nietypowych działań. Użytkownicy mogą eksplorować hello zdarzenia podejrzane przy użyciu toodetermine inspekcji bazy danych SQL, jeśli wynikiem próby tooaccess, naruszenia lub wykorzystania danych w bazie danych hello. Wykrywanie zagrożeń umożliwia proste tooaddress potencjalne zagrożenia toohello bazy danych bez toobe potrzeby hello ekspert zabezpieczeń lub zarządzać zabezpieczeniami zaawansowanymi, monitorowanie systemów.
Na przykład wykrywanie zagrożeń wykrywa niektóre działania nietypowych bazy danych, które wskazują potencjalne prób iniekcji kodu SQL. Iniekcja kodu SQL jest jednym z hello typowych problemów sieci Web aplikacji zabezpieczeń na powitania internetowe, aplikacje używane tooattack opartych na danych. Osoby atakujące korzystać z aplikacji tooinject luk w zabezpieczeniach złośliwego instrukcji SQL do pola wejścia aplikacji, naruszenia i modyfikacji danych w bazie danych hello.

1. Przejdź bloku konfiguracji toohello hello ma toomonitor bazy danych SQL. W bloku ustawienia hello, wybierz **Inspekcja i wykrywanie zagrożeń**.

    ![Okienko nawigacji](./media/sql-database-security-tutorial/auditing-get-started-settings.png)
2. W hello **Inspekcja i wykrywanie zagrożeń** Włącz bloku konfiguracji **ON** inspekcji, które będzie wyświetlane ustawienia wykrywania zagrożeń hello.

3. Włącz **ON** wykrywanie zagrożeń.

4. Skonfiguruj listę hello wiadomości e-mail, które będą wysyłane alerty zabezpieczeń po wykryciu nietypowe działania bazy danych.

5. Kliknij przycisk **zapisać** w hello **Inspekcja i wykrywanie zagrożeń** toosave bloku hello nowych lub zaktualizowanych inspekcji i zagrożeń zasady wykrywania.

    ![Okienko nawigacji](./media/sql-database-security-tutorial/td-turn-on-threat-detection.png)

    W przypadku wykrycia są nietypowe działania bazy danych, otrzymasz wiadomość e-mail z powiadomieniem po wykryciu nietypowe działania bazy danych. e-mail Hello dostarcza informacji o zdarzeń zabezpieczeń podejrzane hello tym rodzaj hello hello nietypowych działań, nazwa bazy danych, server name i hello czas trwania zdarzenia. Ponadto zawierają informacje dotyczące możliwe przyczyny i zalecane akcje tooinvestigate i ograniczyć hello potencjalne zagrożenie toohello w bazie danych. dalej przeszukiwania kroki Hello, przez jaki toodo użytkownik powinien otrzymywać wiadomości e-mail:

    ![Wykrywanie zagrożeń w wiadomości e-mail](./media/sql-database-threat-detection-get-started/4_td_email.png)

6. W wiadomości powitania kliknij hello **dziennik inspekcji SQL Azure** łącza, co spowoduje uruchomienie hello portalu Azure i wyświetlić odpowiednie rekordy hello wokół czasu hello hello podejrzane zdarzenia inspekcji.

    ![Rekordy inspekcji](./media/sql-database-threat-detection-get-started/5_td_audit_records.png)

7. Polecenie tooview rekordów inspekcji hello więcej szczegółów na powitania bazy danych podejrzane działania, takie jak instrukcji SQL, Niepowodzenie IP Przyczyna i klienta.

    ![Szczegóły rekordu](./media/sql-database-security-tutorial/6_td_audit_record_details.png)

8. W bloku rekordów inspekcji powitania kliknij **Otwórz w programie Excel** tooopen wstępnie skonfigurowane w programie excel tooimport szablonu i wykonywania dokładniejszej analizy dziennika inspekcji hello wokół czasu hello hello podejrzane zdarzenia.

    > [!NOTE]
    > W programu Excel 2010 lub nowszej, dodatku Power Query i hello **szybkie łączenie** ustawienie jest wymagane.

    ![Otwarte rekordy w programie Excel](./media/sql-database-threat-detection-get-started/7_td_audit_records_open_excel.png)

9. Witaj tooconfigure **szybkie łączenie** ustawienie - hello **dodatku POWER QUERY** karty wstążki, wybierz opcję **opcje** toodisplay hello opcje w oknie dialogowym. Zaznacz hello sekcji prywatności i wybierz opcję drugi hello — "Ignoruj hello poziomów prywatności i potencjalne poprawianie wydajności":

    ![Łączenie programu Excel fast](./media/sql-database-threat-detection-get-started/8_td_excel_fast_combine.png)

10. tooload dzienników inspekcji SQL, upewnij się, że parametry hello na karcie Ustawienia hello są poprawnie ustawione i wybierz wstążki "Dane" hello i kliknij przycisk "Odśwież wszystko" hello.

    ![Parametry programu Excel](./media/sql-database-threat-detection-get-started/9_td_excel_parameters.png)

11. Witaj wyniki są wyświetlane na powitania **dzienników inspekcji SQL** arkusza, co pozwala toorun dokładniejszej analizy hello nietypowych działań, które zostały wykryte i ograniczyć wpływ hello hello zdarzeń zabezpieczeń w aplikacji.


## <a name="next-steps"></a>Następne kroki
Można zwiększyć hello ochrony bazy danych przed złośliwymi użytkownikami lub nieautoryzowanego dostępu, wystarczy kilka prostych kroków. W tym samouczku dowiesz się: 

> [!div class="checklist"]
> * Konfigurowanie reguł zapory serwera i lub bazy danych
> * Połącz tooyour bazy danych przy użyciu ciągu bezpiecznego połączenia
> * Zarządzanie dostępem użytkowników
> * Ochrona danych za pomocą szyfrowania
> * Włączanie inspekcji bazy danych SQL
> * Włączyć wykrywanie zagrożeń bazy danych SQL

> [!div class="nextstepaction"]
>[Podnoszenie wydajności usługi SQL Database](sql-database-performance-tutorial.md)

