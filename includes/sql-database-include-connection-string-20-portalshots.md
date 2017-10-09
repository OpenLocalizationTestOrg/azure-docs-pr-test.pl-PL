
<!--
includes/sql-database-include-connection-string-20-portalshots.md

Latest Freshness check:  2015-09-02 , GeneMi.

## Connection string
-->


### <a name="obtain-hello-connection-string-from-hello-azure-portal"></a><span data-ttu-id="2dd4f-101">Uzyskaj hello parametry połączenia z hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="2dd4f-101">Obtain hello connection string from hello Azure portal</span></span>
<span data-ttu-id="2dd4f-102">Użyj hello [portalu Azure](https://portal.azure.com/) parametry połączenia hello tooobtain niezbędne do Twojej toointeract program klienta z bazy danych SQL Azure:</span><span class="sxs-lookup"><span data-stu-id="2dd4f-102">Use hello [Azure portal](https://portal.azure.com/) tooobtain hello connection string necessary for your client program toointeract with Azure SQL Database:</span></span> 

1. <span data-ttu-id="2dd4f-103">Kliknij przycisk **PRZEGLĄDAJ** > **baz danych SQL**.</span><span class="sxs-lookup"><span data-stu-id="2dd4f-103">Click **BROWSE** > **SQL databases**.</span></span>
2. <span data-ttu-id="2dd4f-104">Wprowadź nazwę hello bazy danych do hello filtru polu tekstowym w pobliżu lewej górnej hello hello **baz danych SQL** bloku.</span><span class="sxs-lookup"><span data-stu-id="2dd4f-104">Enter hello name of your database into hello filter text box near hello upper-left of hello **SQL databases** blade.</span></span>
3. <span data-ttu-id="2dd4f-105">Kliknij wiersz hello bazy danych.</span><span class="sxs-lookup"><span data-stu-id="2dd4f-105">Click hello row for your database.</span></span>
4. <span data-ttu-id="2dd4f-106">Po bazy danych zostanie wyświetlony blok hello, hello standardowe dla wygody visual, możesz kliknąć przycisk zminimalizować formanty toocollapse hello bloków, używane do przeglądania i filtrowania bazy danych.</span><span class="sxs-lookup"><span data-stu-id="2dd4f-106">After hello blade appears for your database, for visual convenience you can click hello standard minimize controls toocollapse hello blades  you used for browsing and database filtering.</span></span> 
   
    ![Filtruj tooisolate bazy danych][10-FilterDatabase]
5. <span data-ttu-id="2dd4f-108">W bloku hello bazy danych, kliknij **Pokaż parametry połączenia bazy danych**.</span><span class="sxs-lookup"><span data-stu-id="2dd4f-108">On hello blade for your database, click **Show database connection strings**.</span></span>
6. <span data-ttu-id="2dd4f-109">Jeśli planujesz biblioteki połączenia ADO.NET hello toouse, skopiuj ciąg hello etykietą **ADO**.</span><span class="sxs-lookup"><span data-stu-id="2dd4f-109">If you intend toouse hello ADO.NET connection library, copy hello string labeled **ADO**.</span></span> 
   
    ![Skopiuj parametry połączenia ADO hello bazy danych][20-CopyAdoConnectionString]
7. <span data-ttu-id="2dd4f-111">W jeden format lub innym Wklej hello ciągu połączenia w kodzie klienta programu.</span><span class="sxs-lookup"><span data-stu-id="2dd4f-111">In one format or another, paste hello connection string information into your client program code.</span></span>

<span data-ttu-id="2dd4f-112">Aby uzyskać więcej informacji, zobacz:</span><span class="sxs-lookup"><span data-stu-id="2dd4f-112">For more information, see:</span></span><br/><span data-ttu-id="2dd4f-113">[Parametry połączenia i pliki konfiguracyjne](http://msdn.microsoft.com/library/ms254494.aspx).</span><span class="sxs-lookup"><span data-stu-id="2dd4f-113">[Connection Strings and Configuration Files](http://msdn.microsoft.com/library/ms254494.aspx).</span></span>

<!-- Image references. -->

[10-FilterDatabase]: ./media/sql-database-include-connection-string-20-portalshots/connqry-connstr-a.png

[20-CopyAdoConnectionString]: ./media/sql-database-include-connection-string-20-portalshots/connqry-connstr-b.png


<!--
These three includes/ files are a sequenced set, but you can pick and choose:

includes/sql-database-include-connection-string-20-portalshots.md
includes/sql-database-include-connection-string-30-compare.md
includes/sql-database-include-connection-string-40-config.md
-->
