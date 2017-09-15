## <a name="scenario"></a><span data-ttu-id="9cefb-101">Scenariusz</span><span class="sxs-lookup"><span data-stu-id="9cefb-101">Scenario</span></span>
<span data-ttu-id="9cefb-102">Aby lepiej zilustrować tworzenie sieci wirtualnej i jej podsieci, w niniejszym dokumencie zawarto odwołania do poniższego scenariusza.</span><span class="sxs-lookup"><span data-stu-id="9cefb-102">To better illustrate how to create a VNet and subnets, this document will use the scenario below.</span></span>

![Scenariusz sieci wirtualnych](./media/virtual-networks-create-vnet-scenario-include/vnet-scenario.png)

<span data-ttu-id="9cefb-104">W tym scenariuszu utworzysz sieć wirtualną o nazwie **TestVNet** z zarezerwowanym blokiem CIDR **192.168.0.0./16**.</span><span class="sxs-lookup"><span data-stu-id="9cefb-104">In this scenario you will create a VNet named **TestVNet** with a reserved CIDR block of **192.168.0.0./16**.</span></span> <span data-ttu-id="9cefb-105">Twoja sieć wirtualna będzie zawierać następujące podsieci:</span><span class="sxs-lookup"><span data-stu-id="9cefb-105">Your VNet will contain the following subnets:</span></span> 

* <span data-ttu-id="9cefb-106">**FrontEnd**, używająca bloku CIDR **192.168.1.0/24**.</span><span class="sxs-lookup"><span data-stu-id="9cefb-106">**FrontEnd**, using **192.168.1.0/24** as its CIDR block.</span></span>
* <span data-ttu-id="9cefb-107">**BackEnd**, używająca bloku CIDR **192.168.2.0/24**.</span><span class="sxs-lookup"><span data-stu-id="9cefb-107">**BackEnd**, using **192.168.2.0/24** as its CIDR block.</span></span>

