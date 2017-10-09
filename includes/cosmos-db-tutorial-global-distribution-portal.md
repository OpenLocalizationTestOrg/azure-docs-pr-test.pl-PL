
<span data-ttu-id="f02ce-101">Informacje na temat bazy danych Azure rozwiązania Cosmos globalne dystrybucji w tym Azure piątek wideo z Scott Hanselman i Ramana Karthik główny Menedżer zespołu inżynieryjnego.</span><span class="sxs-lookup"><span data-stu-id="f02ce-101">You can learn about Azure Cosmos DB global distribution in this Azure Friday video with Scott Hanselman and Principal Engineering Manager Karthik Raman.</span></span>

>[!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Planet-Scale-NoSQL-with-DocumentDB/player]  

<span data-ttu-id="f02ce-102">Aby uzyskać więcej informacji na temat sposobu globalnej replikacji bazy danych działa w bazie danych rozwiązania Cosmos, zobacz [dystrybucji danych globalnie z rozwiązania Cosmos DB](../articles/documentdb/documentdb-distribute-data-globally.md).</span><span class="sxs-lookup"><span data-stu-id="f02ce-102">For more information about how global database replication works in Cosmos DB, see [Distribute data globally with Cosmos DB](../articles/documentdb/documentdb-distribute-data-globally.md).</span></span>

## <span data-ttu-id="f02ce-103"><a id="addregion"></a>Dodawanie przy użyciu portalu Azure hello regionów globalna baza danych</span><span class="sxs-lookup"><span data-stu-id="f02ce-103"><a id="addregion"></a>Add global database regions using hello Azure Portal</span></span>
<span data-ttu-id="f02ce-104">Azure DB rozwiązania Cosmos jest dostępna we wszystkich [regiony platformy Azure] [ azureregions] na całym świecie.</span><span class="sxs-lookup"><span data-stu-id="f02ce-104">Azure Cosmos DB is available in all [Azure regions][azureregions] world-wide.</span></span> <span data-ttu-id="f02ce-105">Po wybraniu hello domyślny poziom spójności konta bazy danych, można skojarzyć jeden lub więcej regionów (w zależności od wybrana domyślna spójność dystrybucji globalnych i poziomu potrzeb).</span><span class="sxs-lookup"><span data-stu-id="f02ce-105">After selecting hello default consistency level for your database account, you can associate one or more regions (depending on your choice of default consistency level and global distribution needs).</span></span>

1. <span data-ttu-id="f02ce-106">W hello [portalu Azure](https://portal.azure.com/), w hello pasek po lewej stronie, kliknij przycisk **bazy danych Azure rozwiązania Cosmos**.</span><span class="sxs-lookup"><span data-stu-id="f02ce-106">In hello [Azure portal](https://portal.azure.com/), in hello left bar, click **Azure Cosmos DB**.</span></span>
2. <span data-ttu-id="f02ce-107">W hello **bazy danych Azure rozwiązania Cosmos** bloku, toomodify konta bazy danych wybierz hello.</span><span class="sxs-lookup"><span data-stu-id="f02ce-107">In hello **Azure Cosmos DB** blade, select hello database account toomodify.</span></span>
3. <span data-ttu-id="f02ce-108">W bloku konta usługi powitania kliknij **globalnie replikacji danych** hello menu.</span><span class="sxs-lookup"><span data-stu-id="f02ce-108">In hello account blade, click **Replicate data globally** from hello menu.</span></span>
4. <span data-ttu-id="f02ce-109">W hello **globalnie replikacji danych** bloku, wybierz tooadd regionów hello lub usunąć, klikając regiony w mapie hello, a następnie kliknij **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="f02ce-109">In hello **Replicate data globally** blade, select hello regions tooadd or remove by clicking regions in hello map, and then click **Save**.</span></span> <span data-ttu-id="f02ce-110">Brak regionów tooadding kosztów, zobacz hello [cennikiem](https://azure.microsoft.com/pricing/details/documentdb/) lub hello [dystrybucji danych globalnie za pomocą usługi DocumentDB](../articles/documentdb/documentdb-distribute-data-globally.md) artykułu, aby uzyskać więcej informacji.</span><span class="sxs-lookup"><span data-stu-id="f02ce-110">There is a cost tooadding regions, see hello [pricing page](https://azure.microsoft.com/pricing/details/documentdb/) or hello [Distribute data globally with DocumentDB](../articles/documentdb/documentdb-distribute-data-globally.md) article for more information.</span></span>
   
    ![Kliknij przycisk hello regionach tooadd mapy hello lub usuń je][1]
    
<span data-ttu-id="f02ce-112">Po dodaniu drugiego region hello **ręczną pracę awaryjną** hello jest włączona opcja **globalnie replikacji danych** bloku w portalu hello.</span><span class="sxs-lookup"><span data-stu-id="f02ce-112">Once you add a second region, hello **Manual Failover** option is enabled on hello **Replicate data globally** blade in hello portal.</span></span> <span data-ttu-id="f02ce-113">Można użyć tej opcji tootest hello trybu failover procesu lub zmienić regionu podstawowego zapisu hello.</span><span class="sxs-lookup"><span data-stu-id="f02ce-113">You can use this option tootest hello failover process or change hello primary write region.</span></span> <span data-ttu-id="f02ce-114">Po dodaniu trzeci region hello **priorytetów trybu Failover** jest włączona opcja hello tego samego bloku, dzięki czemu można zmienić kolejność pracy awaryjnej powitania dla odczytów.</span><span class="sxs-lookup"><span data-stu-id="f02ce-114">Once you add a third region, hello **Failover Priorities** option is enabled on hello same blade so that you can change hello failover order for reads.</span></span>  

### <a name="selecting-global-database-regions"></a><span data-ttu-id="f02ce-115">Wybieranie regionów globalna baza danych</span><span class="sxs-lookup"><span data-stu-id="f02ce-115">Selecting global database regions</span></span>
<span data-ttu-id="f02ce-116">Istnieją dwa typowych scenariuszy dotyczących konfigurowania dwóch lub więcej regionów:</span><span class="sxs-lookup"><span data-stu-id="f02ce-116">There are two common scenarios for configuring two or more regions:</span></span>

1. <span data-ttu-id="f02ce-117">Dostarczanie małych opóźnieniach dostępu użytkowników tooend toodata niezależnie od tego, gdzie znajdują się wokół Witaj świecie</span><span class="sxs-lookup"><span data-stu-id="f02ce-117">Delivering low-latency access toodata tooend users no matter where they are located around hello globe</span></span>
2. <span data-ttu-id="f02ce-118">Dodawanie regionalnych odporności ciągłość prowadzenia działalności biznesowej i odzyskiwania po awarii (BCDR)</span><span class="sxs-lookup"><span data-stu-id="f02ce-118">Adding regional resiliency for business continuity and disaster recovery (BCDR)</span></span>

<span data-ttu-id="f02ce-119">Dla rozprowadzają tooend małych opóźnieniach — użytkownicy zalecane jest toodeploy zarówno hello aplikacji i Dodaj rozwiązania Cosmos bazy danych Azure w regionach hello odpowiadające użytkowników aplikacji hello toowhere znajdują się.</span><span class="sxs-lookup"><span data-stu-id="f02ce-119">For delivering low-latency tooend-users, it is recommended toodeploy both hello application and add Azure Cosmos DB in hello regions thats correspond toowhere hello application's users are located.</span></span>

<span data-ttu-id="f02ce-120">BCDR, zalecane jest regionów tooadd na podstawie par region hello opisanego w hello [firm ciągłości i odzyskiwanie po awarii (BCDR): Azure łączyć regionów] [ bcdr] artykułu.</span><span class="sxs-lookup"><span data-stu-id="f02ce-120">For BCDR, it is recommended tooadd regions based on hello region pairs described in hello [Business continuity and disaster recovery (BCDR): Azure Paired Regions][bcdr] article.</span></span>

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
