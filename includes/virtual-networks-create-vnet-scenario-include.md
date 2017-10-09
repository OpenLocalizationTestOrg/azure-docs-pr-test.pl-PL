## <a name="scenario"></a><span data-ttu-id="e35c7-101">Scenariusz</span><span class="sxs-lookup"><span data-stu-id="e35c7-101">Scenario</span></span>
<span data-ttu-id="e35c7-102">toobetter ilustrują sposób toocreate sieci wirtualnej i podsieci, ten dokument użyje scenariusz hello poniżej.</span><span class="sxs-lookup"><span data-stu-id="e35c7-102">toobetter illustrate how toocreate a VNet and subnets, this document will use hello scenario below.</span></span>

![Scenariusz sieci wirtualnych](./media/virtual-networks-create-vnet-scenario-include/vnet-scenario.png)

<span data-ttu-id="e35c7-104">W tym scenariuszu utworzysz sieć wirtualną o nazwie **TestVNet** z zarezerwowanym blokiem CIDR **192.168.0.0./16**.</span><span class="sxs-lookup"><span data-stu-id="e35c7-104">In this scenario you will create a VNet named **TestVNet** with a reserved CIDR block of **192.168.0.0./16**.</span></span> <span data-ttu-id="e35c7-105">Sieci wirtualnej będzie zawierać następujące podsieci hello:</span><span class="sxs-lookup"><span data-stu-id="e35c7-105">Your VNet will contain hello following subnets:</span></span> 

* <span data-ttu-id="e35c7-106">**FrontEnd**, używająca bloku CIDR **192.168.1.0/24**.</span><span class="sxs-lookup"><span data-stu-id="e35c7-106">**FrontEnd**, using **192.168.1.0/24** as its CIDR block.</span></span>
* <span data-ttu-id="e35c7-107">**BackEnd**, używająca bloku CIDR **192.168.2.0/24**.</span><span class="sxs-lookup"><span data-stu-id="e35c7-107">**BackEnd**, using **192.168.2.0/24** as its CIDR block.</span></span>

