
<!--
includes/sql-database-include-connection-string-20-portalshots.md

Latest Freshness check:  2015-09-02 , GeneMi.

## Connection string
-->


### <a name="obtain-hello-connection-string-from-hello-azure-portal"></a>Uzyskaj hello parametry połączenia z hello portalu Azure
Użyj hello [portalu Azure](https://portal.azure.com/) parametry połączenia hello tooobtain niezbędne do Twojej toointeract program klienta z bazy danych SQL Azure: 

1. Kliknij przycisk **PRZEGLĄDAJ** > **baz danych SQL**.
2. Wprowadź nazwę hello bazy danych do hello filtru polu tekstowym w pobliżu lewej górnej hello hello **baz danych SQL** bloku.
3. Kliknij wiersz hello bazy danych.
4. Po bazy danych zostanie wyświetlony blok hello, hello standardowe dla wygody visual, możesz kliknąć przycisk zminimalizować formanty toocollapse hello bloków, używane do przeglądania i filtrowania bazy danych. 
   
    ![Filtruj tooisolate bazy danych][10-FilterDatabase]
5. W bloku hello bazy danych, kliknij **Pokaż parametry połączenia bazy danych**.
6. Jeśli planujesz biblioteki połączenia ADO.NET hello toouse, skopiuj ciąg hello etykietą **ADO**. 
   
    ![Skopiuj parametry połączenia ADO hello bazy danych][20-CopyAdoConnectionString]
7. W jeden format lub innym Wklej hello ciągu połączenia w kodzie klienta programu.

Aby uzyskać więcej informacji, zobacz:<br/>[Parametry połączenia i pliki konfiguracyjne](http://msdn.microsoft.com/library/ms254494.aspx).

<!-- Image references. -->

[10-FilterDatabase]: ./media/sql-database-include-connection-string-20-portalshots/connqry-connstr-a.png

[20-CopyAdoConnectionString]: ./media/sql-database-include-connection-string-20-portalshots/connqry-connstr-b.png


<!--
These three includes/ files are a sequenced set, but you can pick and choose:

includes/sql-database-include-connection-string-20-portalshots.md
includes/sql-database-include-connection-string-30-compare.md
includes/sql-database-include-connection-string-40-config.md
-->
