---
title: wprowadzenie do inspekcji bazy danych Azure SQL aaaGet | Dokumentacja firmy Microsoft
description: Rozpoczynanie pracy z inspekcji bazy danych Azure SQL
services: sql-database
documentationcenter: 
author: giladm
manager: jhubbard
editor: giladm
ms.assetid: 89c2a155-c2fb-4b67-bc19-9b4e03c6d3bc
ms.service: sql-database
ms.custom: security
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/07/2017
ms.author: giladm
ms.openlocfilehash: 5494c602d702ac41992520f900c393a98cc7c989
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-sql-database-auditing"></a>Rozpoczynanie pracy z inspekcją bazy danych SQL
Usługa Azure SQL database auditing śledzi zdarzenia bazy danych i zapisuje je tooan dziennik inspekcji na koncie magazynu Azure. Inspekcja również:

* Pomaga zachować zgodność z przepisami, analizować aktywność bazy danych oraz uzyskać wgląd w odchylenia i anomalie, które mogą oznaczać problemy biznesowe lub podejrzane naruszenia zabezpieczeń.

* Włącza i ułatwia przestrzeganie standardów toocompliance, chociaż nie gwarantuje zgodności. Aby uzyskać więcej informacji na temat usługi Azure programy tego zgodność ze standardami pomocy technicznej, zobacz hello [Centrum zaufania Azure](https://azure.microsoft.com/support/trust-center/compliance/).


## <a id="subheading-1"></a>Omówienie inspekcji Azure bazy danych SQL
Program SQL inspekcji bazy danych:


* **Zachowaj** dziennik inspekcji wybranych zdarzeń. Można zdefiniować rodzaje toobe działania bazy danych inspekcji.
* **Raport** na działanie bazy danych. Można użyć wstępnie skonfigurowane raporty i tooget pulpitu nawigacyjnego, szybkie wprowadzenie aktywności i raportowanie zdarzeń.
* **Analizowanie** raportów. Można znaleźć podejrzane zdarzenia, nietypowe działania i trendów.

Inspekcję można skonfigurować dla różnych kategorii, zgodnie z objaśnieniem w hello [inspekcja bazy danych](#subheading-2) sekcji.

Dzienniki inspekcji są zapisywane tooAzure magazynu obiektów Blob w ramach subskrypcji platformy Azure.


## <a id="subheading-8"></a>Zdefiniuj na poziomie serwera, a zasady inspekcji na poziomie bazy danych

Zasady inspekcji mogą być definiowane dla określonej bazy danych lub jako domyślne zasady serwera:

* Zasady serwera stosuje tooall istniejących i nowo utworzone bazy danych na powitania serwera.

* Jeśli *Inspekcja obiektów blob serwera jest włączone*, on *stosowana jest zawsze toohello bazy danych* (to znaczy hello bazy danych zostanie przeprowadzona), niezależnie od bazy danych hello ustawienia inspekcji.

* Włączenie inspekcji na powitania bazy danych, w tooenabling dodanie go na powitania serwera, obiektów blob będzie *nie* zastąpić lub zmienić dowolne z ustawień hello powitania serwera obiektu blob inspekcji. Zarówno inspekcji będą istniały obok siebie. Innymi słowy hello bazy danych zostanie dwukrotnie równolegle inspekcji (raz zasadom powitania serwera i raz zasadom hello bazy danych).

   > [!NOTE]
   > Należy unikać włączania inspekcji obiektu blob serwera i inspekcja obiektów blob dla bazy danych, chyba że:
    > * Ma inną toouse *konta magazynu* lub *okres przechowywania* dla określonej bazy danych.
    > * Dla określonej bazy danych różnią się od typów zdarzeń lub kategorie, które są są poddawane inspekcji dla hello reszty baz danych hello na powitania serwera ma typy zdarzeń tooaudit lub kategorii. Na przykład może być wstawia tabeli, wymagające toobe inspekcji tylko dla określonej bazy danych.
   > 
   > W przeciwnym razie zalecane jest włączenie inspekcji tylko poziom serwera, obiektów blob i pozostaw hello poziom bazy danych inspekcji wyłączona dla wszystkich baz danych.


## <a id="subheading-2"></a>Inspekcja bazy danych
Witaj poniższej sekcji opisano konfigurację hello inspekcji przy użyciu hello portalu Azure.

1. Przejdź toohello [portalu Azure](https://portal.azure.com).
2. Przejdź toohello **ustawienia** bloku powitania serwera bazy danych/SQL SQL ma tooaudit. W hello **ustawienia** bloku, wybierz opcję **Inspekcja i wykrywanie zagrożeń**.

    <a id="auditing-screenshot"></a>![Okienka nawigacji][1]
3. Jeśli wolisz tooset się zasady inspekcji serwera (która zostanie zastosowana tooall istniejących i nowo utworzone bazy danych na tym serwerze), można wybrać hello **wyświetlić ustawienia serwera** łącze w bloku inspekcji hello bazy danych. Można następnie wyświetlić lub zmodyfikować ustawienia inspekcji serwera hello.

    ![Okienko nawigacji][2]
4. Jeśli wolisz tooenable Inspekcja obiektów blob na poziomie bazy danych hello (w tooor dodanie zamiast inspekcję na poziomie serwera), aby uzyskać **inspekcji**, wybierz pozycję **ON**oraz **inspekcji typu** , wybierz **obiektu Blob**.

    Po włączeniu inspekcji obiektu blob serwera hello skonfigurowane bazy danych inspekcji będą istniały równolegle powitania serwera obiektu blob inspekcji.  

    ![Okienko nawigacji][3]
5. Witaj tooopen **magazyn dzienników inspekcji** bloku, wybierz opcję **szczegóły magazynu**. Wybierz konto magazynu Azure hello, gdzie zostaną zapisane dzienniki, a następnie wybierz okres przechowywania hello, po którym hello będą usuwane stare dzienniki. Następnie kliknij przycisk **OK**. 
   >[!TIP] 
   >Witaj tooget maksymalne wykorzystanie możliwości inspekcji hello raporty szablony, użyj hello tego samego konta magazynu dla wszystkich baz danych inspekcji. 

    <a id="storage-screenshot"></a>![Okienka nawigacji][4]
6. Jeśli chcesz toocustomize hello inspekcji zdarzeń, możesz to zrobić za pomocą programu PowerShell lub hello interfejsu API REST. Aby uzyskać więcej informacji, zobacz hello [automatyzacji (interfejsu API programu PowerShell/REST)](#subheading-7) sekcji.
7. Po skonfigurowaniu ustawień inspekcji można włączyć hello nowych funkcji wykrywania zagrożeń i skonfigurować alerty zabezpieczeń tooreceive wiadomości e-mail. Gdy używasz wykrywanie zagrożeń, pojawi się aktywne alerty w przypadku nietypowe działania bazy danych, które mogą wskazywać możliwe zagrożenia bezpieczeństwa. Aby uzyskać więcej informacji, zobacz [wprowadzenie wykrywanie zagrożeń](sql-database-threat-detection-get-started.md).
8. Kliknij pozycję **Zapisz**.





## <a id="subheading-3"></a>Analizowanie dzienników inspekcji i raportów
Dzienniki inspekcji są agregowane w hello kontem magazynu platformy Azure, wybrana podczas instalacji. Dzienniki inspekcji można sprawdzić za pomocą narzędzia, takie jak [Eksploratora usługi Storage Azure](http://storageexplorer.com/).

Dzienniki inspekcji obiektów blob są zapisywane jako kolekcja plików obiektów blob w kontenerze o nazwie **sqldbauditlogs**.

Aby uzyskać szczegółowe informacje o hierarchii hello folderu przechowywania dzienników inspekcji obiektu blob hello, konwencje nazewnictwa obiektów blob i format dziennika, zobacz hello [odwołanie obiektu Blob inspekcji dziennika formatu (do pobrania plik .docx)](https://go.microsoft.com/fwlink/?linkid=829599).

Istnieje kilka metod, można użyć obiektu blob tooview dzienniki inspekcji:

* Użyj hello [portalu Azure](https://portal.azure.com).  Otwórz hello odpowiednie bazy danych. Witaj AT na początku hello bazy danych **Inspekcja i wykrywanie zagrożeń** bloku, kliknij przycisk **Przeglądanie dzienników inspekcji**.

    ![Okienko nawigacji][7]

    **Rekordów inspekcji** zostanie otwarty blok, z których będziesz w stanie tooview hello dzienników.

    - Konkretne daty można wyświetlić, klikając **filtru** u góry hello hello **rekordów inspekcji** bloku.
    - Można przełączać się między rekordów inspekcji, które zostały utworzone przez serwer zasad lub bazy danych zasad kontroli.

       ![Okienko nawigacji][8]

* Użyj funkcji systemowej hello **sys.fn_get_audit_file** (T-SQL) tooreturn hello danych z dziennika inspekcji w formacie tabelarycznym. Aby uzyskać więcej informacji na temat używania tej funkcji, zobacz hello [dokumentacji sys.fn_get_audit_file](https://docs.microsoft.com/sql/relational-databases/system-functions/sys-fn-get-audit-file-transact-sql).


* Użyj **scalania plików inspekcji** w programu SQL Server Management Studio (począwszy od SSMS 17):  
    1. Wybierz z menu Narzędzia SSMS hello **pliku** > **Otwórz** > **scalania plików inspekcji**.

        ![Okienko nawigacji][9]
    2. Witaj **Dodaj pliki inspekcji** zostanie otwarte okno dialogowe. Wybierz jedną z hello **Dodaj** opcji, aby wybrać, czy inspekcji toomerge pliki z dysku lokalnego na dysku lub zaimportować je z usługi Azure Storage (użytkownik będzie tooprovide wymagane szczegóły usługi Azure Storage, a klucz konta).

    3. Po dodaniu wszystkich plików toomerge kliknij **OK** toocomplete hello: Operacja scalania.

    4. Hello scalony plik zostanie otwarty w programie SSMS, w którym można wyświetlać i analizować je, a także eksportu go tooan pliku XEL lub CSV pliku lub tooa tabeli.

* Użyj hello [synchronizacji aplikacji](https://github.com/Microsoft/Azure-SQL-DB-auditing-OMS-integration) , który został utworzony. Działa na platformie Azure, a używa analizy dzienników Operations Management Suite (OMS) publiczne interfejsy API toopush SQL dzienników inspekcji na OMS. Hello synchronizacji aplikacji wypchnięcia dzienników inspekcji SQL do analizy dzienników OMS zużycia za pośrednictwem pulpitu nawigacyjnego Analytics dziennika OMS hello. 

* Przy użyciu usługi Power BI. Można wyświetlać i analizować dane dzienników inspekcji w usłudze Power BI. Dowiedz się więcej o [usługi Power BI i dostęp do pobrania szablonu](https://blogs.msdn.microsoft.com/azuresqldbsupport/2017/05/26/sql-azure-blob-auditing-basic-power-bi-dashboard/).

* Pobierz pliki dziennika z kontenera obiektów blob magazynu Azure za pośrednictwem portalu hello lub przy użyciu narzędzia, takie jak [Eksploratora usługi Storage Azure](http://storageexplorer.com/).
    * Po pobraniu pliku dziennika, który jest lokalnie, możesz kliknąć dwukrotnie tooopen pliku hello, wyświetlać i analizować dzienniki hello w programie SSMS.
    * Możesz również pobrać wielu plików jednocześnie za pomocą Eksploratora usługi Storage platformy Azure. Kliknij prawym przyciskiem myszy określony podfolder (na przykład podfolder, który zawiera wszystkie pliki dziennika dotyczące określonej daty) i wybierz **Zapisz jako** toosave w folderze lokalnym.

* Dodatkowe metody:
   * Po pobraniu kilka plików (lub podfolder, który zawiera pliki dziennika dla całego dnia, zgodnie z opisem w hello poprzedniego elementu na tej liście), można połączyć je lokalnie zgodnie z opisem w instrukcjach plików inspekcji scalania SSMS hello opisany wcześniej.

   * Inspekcja obiektów blob widoku programowo dzienników:

     * Użyj hello [czytnika zdarzeń rozszerzonych](https://blogs.msdn.microsoft.com/extended_events/2011/07/20/introducing-the-extended-events-reader/) biblioteki C#.
     * [Zapytanie rozszerzonych plików zdarzenia](https://sqlscope.wordpress.com/2014/11/15/reading-extended-event-files-using-client-side-tools-only/) przy użyciu programu PowerShell.




## <a id="subheading-5"></a>Wskazówki produkcji
<!--hello description in this section refers toopreceding screen captures.-->

### <a id="subheading-6">Inspekcja bazy danych z replikacją geograficzną</a>
Korzystając z bazy danych z replikacją geograficzną, jest możliwe tooset inspekcja na powitania podstawowej bazy danych, hello pomocniczej bazy danych lub obu w zależności od typu inspekcji hello.

Wykonaj te instrukcje (należy pamiętać, że inspekcja obiektów blob można włączyć lub wyłączyć tylko z ustawień inspekcji bazy danych podstawowego hello):

* **Podstawowa baza danych**. Włącz Inspekcja obiektów blob, albo na powitania serwera na powitania bazy danych, zgodnie z opisem w hello [inspekcja bazy danych](#subheading-2) sekcji.
* **Dodatkowej bazy danych**. Włącz inspekcję obiektów blob na powitania podstawowej bazy danych, zgodnie z opisem w hello [inspekcja bazy danych](#subheading-2) sekcji. 
   * Inspekcja obiektów blob musi być włączona na powitania *podstawowa baza danych sam*, nie powitania serwera.
   * Po włączeniu inspekcji obiektu blob na powitania podstawowej bazy danych, również będą stają się włączone na powitania dodatkowej bazy danych.

     >[!IMPORTANT]
     >Domyślnie hello ustawienia magazynu dla hello pomocniczej bazy danych będzie identyczne toothose hello głównej bazy danych, powodując ruchu między regionalne. Można tego uniknąć, włączając Inspekcja obiektów blob na powitania serwera pomocniczego i konfigurowania magazynu lokalnego w ustawieniach magazynu pomocniczego serwera hello. Spowoduje to zmianę lokalizacji magazynu hello hello pomocniczej bazy danych i wyników w każdej bazie danych, zapisanie jej magazynem toolocal dzienniki inspekcji.  
<br>

### <a id="subheading-6">Ponowne generowanie klucza magazynu</a>
W środowisku produkcyjnym jest prawdopodobnie toorefresh Twojego magazynu kluczy okresowo. Podczas odświeżania kluczy, należy zasady inspekcji hello tooresave. Witaj proces przebiega następująco:

1. Otwórz hello **szczegóły magazynu** bloku. W hello **klucz dostępu do magazynu** wybierz opcję **dodatkowej**i kliknij przycisk **OK**. Następnie kliknij przycisk **zapisać** u góry hello hello inspekcji blok konfiguracji.

    ![Okienko nawigacji][5]
2. Przejdź do bloku konfiguracji magazynu toohello i ponowne wygenerowanie hello podstawowy klucz dostępu.

    ![Okienko nawigacji][6]
3. Przejdź wstecz toohello inspekcji blok konfiguracji, Przełącz hello klucz dostępu do magazynu z tooprimary dodatkowej, a następnie kliknij **OK**. Następnie kliknij przycisk **zapisać** u góry hello hello inspekcji blok konfiguracji.
4. Blok konfiguracji magazynu toohello i regenerate hello pomocniczy klucz dostępu (w ramach przygotowania do cyklu odświeżania hello klawisza Następna), przejdź wstecz.

## <a id="subheading-7"></a>Automatyzacja (programu PowerShell/REST API)
Można również skonfigurować inspekcji w bazie danych SQL Azure za pomocą powitania po narzędziami automatyzacji:

* **Polecenia cmdlet programu PowerShell**:

   * [Get-AzureRMSqlDatabaseAuditingPolicy][101]
   * [Get-AzureRMSqlServerAuditingPolicy][102]
   * [Usuń AzureRMSqlDatabaseAuditing][103]
   * [Usuń AzureRMSqlServerAuditing][104]
   * [Zestaw AzureRMSqlDatabaseAuditingPolicy][105]
   * [Zestaw AzureRMSqlServerAuditingPolicy][106]
   * [Użyj AzureRMSqlServerAuditingPolicy][107]

   Na przykład skryptu, zobacz [konfigurowania inspekcji i wykrywania zagrożeń przy użyciu programu PowerShell](scripts/sql-database-auditing-and-threat-detection-powershell.md).

* **Interfejs API REST - Inspekcja obiektów Blob**:

   * [Utwórz lub zaktualizuj bazę danych obiektów Blob zasady inspekcji](https://msdn.microsoft.com/library/azure/mt695939.aspx)
   * [Utwórz lub zaktualizuj Blob serwera zasady inspekcji](https://msdn.microsoft.com/library/azure/mt771861.aspx)
   * [Pobierz bazy danych obiektów Blob zasady inspekcji](https://msdn.microsoft.com/library/azure/mt695938.aspx)
   * [Pobierz obiekt Blob serwera zasady inspekcji](https://msdn.microsoft.com/library/azure/mt771860.aspx)
   * [Pobierz Blob serwera inspekcji wynik operacji](https://msdn.microsoft.com/library/azure/mt771862.aspx)


<!--Anchors-->
[Azure SQL Database Auditing overview]: #subheading-1
[Set up auditing for your database]: #subheading-2
[Analyze audit logs and reports]: #subheading-3
[Practices for usage in production]: #subheading-5
[Storage Key Regeneration]: #subheading-6
[Automation (PowerShell / REST API)]: #subheading-7
[Blob/Table differences in Server auditing policy inheritance]: (#subheading-8)  

<!--Image references-->
[1]: ./media/sql-database-auditing-get-started/1_auditing_get_started_settings.png
[2]: ./media/sql-database-auditing-get-started/2_auditing_get_started_server_inherit.png
[3]: ./media/sql-database-auditing-get-started/3_auditing_get_started_turn_on.png
[4]: ./media/sql-database-auditing-get-started/4_auditing_get_started_storage_details.png
[5]: ./media/sql-database-auditing-get-started/5_auditing_get_started_storage_key_regeneration.png
[6]: ./media/sql-database-auditing-get-started/6_auditing_get_started_regenerate_key.png
[7]: ./media/sql-database-auditing-get-started/7_auditing_get_started_blob_view_audit_logs.png
[8]: ./media/sql-database-auditing-get-started/8_auditing_get_started_blob_audit_records.png
[9]: ./media/sql-database-auditing-get-started/9_auditing_get_started_ssms_1.png
[10]: ./media/sql-database-auditing-get-started/10_auditing_get_started_ssms_2.png

[101]: /powershell/module/azurerm.sql/get-azurermsqldatabaseauditingpolicy
[102]: /powershell/module/azurerm.sql/Get-AzureRMSqlServerAuditingPolicy
[103]: /powershell/module/azurerm.sql/Remove-AzureRMSqlDatabaseAuditing
[104]: /powershell/module/azurerm.sql/Remove-AzureRMSqlServerAuditing
[105]: /powershell/module/azurerm.sql/Set-AzureRMSqlDatabaseAuditingPolicy
[106]: /powershell/module/azurerm.sql/Set-AzureRMSqlServerAuditingPolicy
[107]: /powershell/module/azurerm.sql/Use-AzureRMSqlServerAuditingPolicy
