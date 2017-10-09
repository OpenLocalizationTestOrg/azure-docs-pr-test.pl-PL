1. <span data-ttu-id="1391f-101">W Menedżerze klastra trybu Failover rozwiń **ról**, a następnie zaznacz tej grupy dostępności.</span><span class="sxs-lookup"><span data-stu-id="1391f-101">In Failover Cluster Manager, expand **Roles**, and then highlight your availability group.</span></span>  

2. <span data-ttu-id="1391f-102">Na powitania **zasobów** , kliknij prawym przyciskiem myszy nazwę odbiornika hello, a następnie kliknij **właściwości**.</span><span class="sxs-lookup"><span data-stu-id="1391f-102">On hello **Resources** tab, right-click hello listener name, and then click **Properties**.</span></span>

3. <span data-ttu-id="1391f-103">Kliknij przycisk hello **zależności** kartę. Jeśli wiele zasobów nie są wyświetlane, sprawdź, czy adresy IP hello mają lub nie oraz zależności.</span><span class="sxs-lookup"><span data-stu-id="1391f-103">Click hello **Dependencies** tab. If multiple resources are listed, verify that hello IP addresses have OR, not AND, dependencies.</span></span>  

4. <span data-ttu-id="1391f-104">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="1391f-104">Click **OK**.</span></span>

5. <span data-ttu-id="1391f-105">Kliknij prawym przyciskiem myszy nazwę odbiornika hello, a następnie kliknij przycisk **przejdź do trybu Online**.</span><span class="sxs-lookup"><span data-stu-id="1391f-105">Right-click hello listener name, and then click **Bring Online**.</span></span>

6. <span data-ttu-id="1391f-106">Odbiornik po hello jest w trybie online na powitania **zasobów** , kliknij prawym przyciskiem myszy hello grupy dostępności, a następnie kliknij **właściwości**.</span><span class="sxs-lookup"><span data-stu-id="1391f-106">After hello listener is online, on hello **Resources** tab, right-click hello availability group, and then click **Properties**.</span></span>
   
    ![Skonfiguruj hello dostępności grupy zasobów](./media/virtual-machines-sql-server-configure-alwayson-availability-group-listener/IC678772.gif)

7. <span data-ttu-id="1391f-108">Zależność od zasobu Nazwa odbiornika hello (nie hello nazwę adresów IP zasobów), a następnie kliknij polecenie **OK**.</span><span class="sxs-lookup"><span data-stu-id="1391f-108">Create a dependency on hello listener name resource (not hello IP address resources name), and then click **OK**.</span></span>
   
    ![Dodaj zależności na nazwę odbiornika hello](./media/virtual-machines-sql-server-configure-alwayson-availability-group-listener/IC678773.gif)

8. <span data-ttu-id="1391f-110">Uruchom program SQL Server Management Studio, a następnie połącz toohello repliki podstawowej.</span><span class="sxs-lookup"><span data-stu-id="1391f-110">Start SQL Server Management Studio, and then connect toohello primary replica.</span></span>

9. <span data-ttu-id="1391f-111">Przejdź za**wysokiej dostępności funkcji AlwaysOn** > **grup dostępności** > **\<AvailabilityGroupName\>**   >  **Odbiorniki grupy dostępności**.</span><span class="sxs-lookup"><span data-stu-id="1391f-111">Go too**AlwaysOn High Availability** > **Availability Groups** > **\<AvailabilityGroupName\>** > **Availability Group Listeners**.</span></span>  
    <span data-ttu-id="1391f-112">Nazwa odbiornika Hello utworzonego w Menedżerze klastra trybu Failover powinny być wyświetlane.</span><span class="sxs-lookup"><span data-stu-id="1391f-112">hello listener name that you created in Failover Cluster Manager should be displayed.</span></span>

10. <span data-ttu-id="1391f-113">Kliknij prawym przyciskiem myszy nazwę odbiornika hello, a następnie kliknij przycisk **właściwości**.</span><span class="sxs-lookup"><span data-stu-id="1391f-113">Right-click hello listener name, and then click **Properties**.</span></span>

11. <span data-ttu-id="1391f-114">W hello **portu** Określ numer portu odbiornika grupy dostępności hello hello przy użyciu hello $EndpointPort używanego wcześniej (w tym samouczku 1433 była hello domyślna), a następnie kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="1391f-114">In hello **Port** box, specify hello port number for hello availability group listener by using hello $EndpointPort that you used earlier (in this tutorial, 1433 was hello default), and then click **OK**.</span></span>

