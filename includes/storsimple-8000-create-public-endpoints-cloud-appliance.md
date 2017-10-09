#### <a name="toocreate-public-endpoints-on-hello-cloud-appliance"></a><span data-ttu-id="a4bd9-101">toocreate publiczne punkty końcowe na powitania urządzenia chmury</span><span class="sxs-lookup"><span data-stu-id="a4bd9-101">toocreate public endpoints on hello cloud appliance</span></span>

1. <span data-ttu-id="a4bd9-102">Zaloguj się toohello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="a4bd9-102">Sign in toohello Azure portal.</span></span>
2. <span data-ttu-id="a4bd9-103">Przejdź za**maszyn wirtualnych**, a następnie wybierz opcję i kliknij hello maszyny wirtualnej, która jest używana jako urządzenia chmury.</span><span class="sxs-lookup"><span data-stu-id="a4bd9-103">Go too**Virtual Machines**, and then select and click hello virtual machine that is being used as your cloud appliance.</span></span>
    
3. <span data-ttu-id="a4bd9-104">Należy toocreate sieci zabezpieczeń grupy (NSG) reguły toocontrol hello przepływu ruchu do i z maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="a4bd9-104">You need toocreate a network security group (NSG) rule toocontrol hello flow of traffic in and out of your virtual machine.</span></span> <span data-ttu-id="a4bd9-105">Wykonaj następujące kroki toocreate reguły NSG hello.</span><span class="sxs-lookup"><span data-stu-id="a4bd9-105">Perform hello following steps toocreate an NSG rule.</span></span>
    1. <span data-ttu-id="a4bd9-106">Wybierz pozycję **Sieciowa grupa zabezpieczeń**.</span><span class="sxs-lookup"><span data-stu-id="a4bd9-106">Select **Network security group**.</span></span>
        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt1.png)

    2. <span data-ttu-id="a4bd9-107">Kliknij przycisk grupy zabezpieczeń sieci domyślne hello, które są prezentowane.</span><span class="sxs-lookup"><span data-stu-id="a4bd9-107">Click hello default network security group that is presented.</span></span>
        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt2.png)

    3. <span data-ttu-id="a4bd9-108">W obszarze **Reguły zabezpieczeń dla ruchu przychodzącego**.</span><span class="sxs-lookup"><span data-stu-id="a4bd9-108">Select **Inbound security rules**.</span></span>
        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt3.png)

    4. <span data-ttu-id="a4bd9-109">Kliknij przycisk **+ Dodaj** toocreate reguły zabezpieczeń dla ruchu przychodzącego.</span><span class="sxs-lookup"><span data-stu-id="a4bd9-109">Click **+ Add** toocreate an inbound security rule.</span></span>
        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt4.png)

        <span data-ttu-id="a4bd9-110">W bloku zasady zabezpieczeń dla ruchu przychodzącego Dodaj hello:</span><span class="sxs-lookup"><span data-stu-id="a4bd9-110">In hello Add inbound security rule blade:</span></span>

        1. <span data-ttu-id="a4bd9-111">Dla hello **nazwa**, typ hello następujące nazwy dla punktu końcowego hello: WinRMHttps.</span><span class="sxs-lookup"><span data-stu-id="a4bd9-111">For hello **Name**, type hello following name for hello endpoint: WinRMHttps.</span></span>
        
        2. <span data-ttu-id="a4bd9-112">Dla hello **priorytet**, wybierz numer wcześniejsza niż 1000 (czyli hello priorytet reguły domyślnej hello).</span><span class="sxs-lookup"><span data-stu-id="a4bd9-112">For hello **Priority**, select a number lesser than 1000 (which is hello priority for hello default rule).</span></span> <span data-ttu-id="a4bd9-113">Wyższa wartość hello, niższy priorytet hello.</span><span class="sxs-lookup"><span data-stu-id="a4bd9-113">Higher hello value, lower hello priority.</span></span>

        3. <span data-ttu-id="a4bd9-114">Zestaw hello **źródła** za**żadnych**.</span><span class="sxs-lookup"><span data-stu-id="a4bd9-114">Set hello **Source** too**Any**.</span></span>

        4. <span data-ttu-id="a4bd9-115">Dla hello **usługi**, wybierz pozycję **WinRM**.</span><span class="sxs-lookup"><span data-stu-id="a4bd9-115">For hello **Service**, select **WinRM**.</span></span> <span data-ttu-id="a4bd9-116">Witaj **protokołu** jest automatycznie ustawiana za**TCP** i hello **zakres portów** ustawiono zbyt**5986**.</span><span class="sxs-lookup"><span data-stu-id="a4bd9-116">hello **Protocol** is automatically set too**TCP** and hello **Port range** is set too**5986**.</span></span>

        5. <span data-ttu-id="a4bd9-117">Kliknij przycisk **OK** toocreate hello reguły.</span><span class="sxs-lookup"><span data-stu-id="a4bd9-117">Click **OK** toocreate hello rule.</span></span>

            ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt5.png)

4. <span data-ttu-id="a4bd9-118">Z ostatnim krokiem jest tooassociate grupy zabezpieczeń sieci z podsiecią lub w konkretnym interfejsie sieciowym.</span><span class="sxs-lookup"><span data-stu-id="a4bd9-118">Your final step is tooassociate your network security group with a subnet or a specific network interface.</span></span> <span data-ttu-id="a4bd9-119">Wykonaj następujące kroki tooassociate hello sieciową grupę zabezpieczeń z podsiecią.</span><span class="sxs-lookup"><span data-stu-id="a4bd9-119">Perform hello following steps tooassociate your network security group with a subnet.</span></span>
    1. <span data-ttu-id="a4bd9-120">Przejdź za**podsieci**.</span><span class="sxs-lookup"><span data-stu-id="a4bd9-120">Go too**Subnets**.</span></span>
    2. <span data-ttu-id="a4bd9-121">Kliknij pozycję **+ Skojarz**.</span><span class="sxs-lookup"><span data-stu-id="a4bd9-121">Click **+ Associate**.</span></span>
        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt7.png)

    3. <span data-ttu-id="a4bd9-122">Wybierz sieci wirtualnej, a następnie wybierz hello odpowiedniej podsieci.</span><span class="sxs-lookup"><span data-stu-id="a4bd9-122">Select your virtual network, and then select hello appropriate subnet.</span></span>
    4. <span data-ttu-id="a4bd9-123">Kliknij przycisk **OK** toocreate hello reguły.</span><span class="sxs-lookup"><span data-stu-id="a4bd9-123">Click **OK** toocreate hello rule.</span></span>

        ![](./media/storsimple-8000-create-public-endpoints-cloud-appliance/sca-create-public-endpt11.png)

<span data-ttu-id="a4bd9-124">Po utworzeniu reguły hello można wyświetlić adres publiczny wirtualnego adresu IP (VIP) hello toodetermine szczegóły.</span><span class="sxs-lookup"><span data-stu-id="a4bd9-124">After hello rule is created, you can view its details toodetermine hello Public Virtual IP (VIP) address.</span></span> <span data-ttu-id="a4bd9-125">Zapisz ten adres.</span><span class="sxs-lookup"><span data-stu-id="a4bd9-125">Record this address.</span></span>


