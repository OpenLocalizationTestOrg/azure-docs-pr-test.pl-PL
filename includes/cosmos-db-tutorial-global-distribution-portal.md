
Informacje na temat bazy danych Azure rozwiązania Cosmos globalne dystrybucji w tym Azure piątek wideo z Scott Hanselman i Ramana Karthik główny Menedżer zespołu inżynieryjnego.

>[!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Planet-Scale-NoSQL-with-DocumentDB/player]  

Aby uzyskać więcej informacji na temat sposobu globalnej replikacji bazy danych działa w bazie danych rozwiązania Cosmos, zobacz [dystrybucji danych globalnie z rozwiązania Cosmos DB](../articles/documentdb/documentdb-distribute-data-globally.md).

## <a id="addregion"></a>Dodawanie przy użyciu portalu Azure hello regionów globalna baza danych
Azure DB rozwiązania Cosmos jest dostępna we wszystkich [regiony platformy Azure] [ azureregions] na całym świecie. Po wybraniu hello domyślny poziom spójności konta bazy danych, można skojarzyć jeden lub więcej regionów (w zależności od wybrana domyślna spójność dystrybucji globalnych i poziomu potrzeb).

1. W hello [portalu Azure](https://portal.azure.com/), w hello pasek po lewej stronie, kliknij przycisk **bazy danych Azure rozwiązania Cosmos**.
2. W hello **bazy danych Azure rozwiązania Cosmos** bloku, toomodify konta bazy danych wybierz hello.
3. W bloku konta usługi powitania kliknij **globalnie replikacji danych** hello menu.
4. W hello **globalnie replikacji danych** bloku, wybierz tooadd regionów hello lub usunąć, klikając regiony w mapie hello, a następnie kliknij **zapisać**. Brak regionów tooadding kosztów, zobacz hello [cennikiem](https://azure.microsoft.com/pricing/details/documentdb/) lub hello [dystrybucji danych globalnie za pomocą usługi DocumentDB](../articles/documentdb/documentdb-distribute-data-globally.md) artykułu, aby uzyskać więcej informacji.
   
    ![Kliknij przycisk hello regionach tooadd mapy hello lub usuń je][1]
    
Po dodaniu drugiego region hello **ręczną pracę awaryjną** hello jest włączona opcja **globalnie replikacji danych** bloku w portalu hello. Można użyć tej opcji tootest hello trybu failover procesu lub zmienić regionu podstawowego zapisu hello. Po dodaniu trzeci region hello **priorytetów trybu Failover** jest włączona opcja hello tego samego bloku, dzięki czemu można zmienić kolejność pracy awaryjnej powitania dla odczytów.  

### <a name="selecting-global-database-regions"></a>Wybieranie regionów globalna baza danych
Istnieją dwa typowych scenariuszy dotyczących konfigurowania dwóch lub więcej regionów:

1. Dostarczanie małych opóźnieniach dostępu użytkowników tooend toodata niezależnie od tego, gdzie znajdują się wokół Witaj świecie
2. Dodawanie regionalnych odporności ciągłość prowadzenia działalności biznesowej i odzyskiwania po awarii (BCDR)

Dla rozprowadzają tooend małych opóźnieniach — użytkownicy zalecane jest toodeploy zarówno hello aplikacji i Dodaj rozwiązania Cosmos bazy danych Azure w regionach hello odpowiadające użytkowników aplikacji hello toowhere znajdują się.

BCDR, zalecane jest regionów tooadd na podstawie par region hello opisanego w hello [firm ciągłości i odzyskiwanie po awarii (BCDR): Azure łączyć regionów] [ bcdr] artykułu.

<!--

## <a id="selectwriteregion"></a>Select hello write region

While all regions associated with your Cosmos DB database account can serve reads (both, single item as well as multi-item paginated reads) and queries, only one region can actively receive hello write (insert, upsert, replace, delete) requests. tooset hello active write region, do hello following  


1. In hello **Azure Cosmos DB** blade, select hello database account toomodify.
2. In hello account blade, click **Replicate data globally** from hello menu.
3. In hello **Replicate data globally** blade, click **Manual Failover** from hello top bar.
    ![Change hello write region under Azure Cosmos DB Account > Replicate data globally > Manual Failover][2]
4. Select a read region toobecome hello new write region, click hello checkbox tooconfirm triggering a failover, and click OK
    ![Change hello write region by selecting a new region in list under Azure Cosmos DB Account > Replicate data globally > Manual Failover][3]

--->

<!--Image references-->
[1]: ./media/cosmos-db-tutorial-global-distribution-portal/azure-cosmos-db-add-region.png
[2]: ./media/cosmos-db-tutorial-global-distribution-portal/azure-cosmos-db-manual-failover-1.png
[3]: ./media/cosmos-db-tutorial-global-distribution-portal/azure-cosmos-db-manual-failover-2.png

<!--Reference style links - using these makes hello source content way more readable than using inline links-->
[bcdr]: https://azure.microsoft.com/documentation/articles/best-practices-availability-paired-regions/
[consistency]: ../articles/cosmos-db/consistency-levels.md
[azureregions]: https://azure.microsoft.com/regions/#services
[offers]: https://azure.microsoft.com/pricing/details/cosmos-db/
