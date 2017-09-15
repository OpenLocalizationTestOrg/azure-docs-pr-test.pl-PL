<!--author=alkohli last changed: 9/16/15-->


#### <a name="to-cable-your-device-for-power"></a><span data-ttu-id="d15f4-101">Aby Podłączanie kabli do urządzenia zasilania</span><span class="sxs-lookup"><span data-stu-id="d15f4-101">To cable your device for power</span></span>
> [!NOTE]
> <span data-ttu-id="d15f4-102">Zarówno obudowy na urządzeniu StorSimple obejmują PCMs nadmiarowe.</span><span class="sxs-lookup"><span data-stu-id="d15f4-102">Both enclosures on your StorSimple device include redundant PCMs.</span></span> <span data-ttu-id="d15f4-103">Dla każdej obudowy PCMs musi być zainstalowane i połączone z różnych źródeł napędu aby zapewnić wysoką dostępność.</span><span class="sxs-lookup"><span data-stu-id="d15f4-103">For each enclosure, the PCMs must be installed and connected to different power sources to ensure high availability.</span></span>
> 
> 

1. <span data-ttu-id="d15f4-104">Upewnij się, że przełączniki zasilania na wszystkich PCMs znajdują się w pozycji OFF.</span><span class="sxs-lookup"><span data-stu-id="d15f4-104">Make sure that the power switches on all the PCMs are in the OFF position.</span></span>
2. <span data-ttu-id="d15f4-105">Podstawowy obudowa Połącz kable do obu PCMs.</span><span class="sxs-lookup"><span data-stu-id="d15f4-105">On the primary enclosure, connect the power cords to both PCMs.</span></span> <span data-ttu-id="d15f4-106">Kable są oznaczone na czerwono na diagramie okablowania zasilania poniżej.</span><span class="sxs-lookup"><span data-stu-id="d15f4-106">The power cords are identified in red in the power cabling diagram, below.</span></span>
3. <span data-ttu-id="d15f4-107">Należy upewnić się czy dwa PCMs na obudowę podstawowego źródła zasilania oddzielne.</span><span class="sxs-lookup"><span data-stu-id="d15f4-107">Make sure that the two PCMs on the primary enclosure use separate power sources.</span></span>
4. <span data-ttu-id="d15f4-108">Dołącz przewodów zasilania do włączania stojak jednostki dystrybucji zasilania pokazane zasilania okablowania diagramu.</span><span class="sxs-lookup"><span data-stu-id="d15f4-108">Attach the power cords to the power on the rack distribution units as shown in the power cabling diagram.</span></span>
5. <span data-ttu-id="d15f4-109">Powtórz kroki od 2 do 4 dla obudowa EBOD.</span><span class="sxs-lookup"><span data-stu-id="d15f4-109">Repeat steps 2 through 4 for the EBOD enclosure.</span></span>
6. <span data-ttu-id="d15f4-110">Włącz obudowa EBOD przestawiając przycisk zasilania w każdej PCM pozycji dalej.</span><span class="sxs-lookup"><span data-stu-id="d15f4-110">Turn on the EBOD enclosure by flipping the power switch on each PCM to the ON position.</span></span>
7. <span data-ttu-id="d15f4-111">Sprawdź, czy obudowa EBOD jest włączona przez sprawdzenie, czy zielony LED tyłu kontrolera EBOD są włączone.</span><span class="sxs-lookup"><span data-stu-id="d15f4-111">Verify that the EBOD enclosure is turned on by checking that the green LEDs on the back of the EBOD controller are turned ON.</span></span>
8. <span data-ttu-id="d15f4-112">Włącz głównej obudowy przestawiając każdy przełącznik PCM pozycji dalej.</span><span class="sxs-lookup"><span data-stu-id="d15f4-112">Turn on the primary enclosure by flipping each PCM switch to the ON position.</span></span>
9. <span data-ttu-id="d15f4-113">Sprawdź, czy system na zapewniając kontroler urządzenia, dla którego włączono LED.</span><span class="sxs-lookup"><span data-stu-id="d15f4-113">Verify that the system is on by ensuring the device controller LEDs have turned ON.</span></span>
10. <span data-ttu-id="d15f4-114">Upewnij się, że połączenia między kontrolerem EBOD i kontrolerów urządzeń jest aktywny, upewniając się, że cztery LED obok portów SAS na kontrolerze EBOD są zielone.</span><span class="sxs-lookup"><span data-stu-id="d15f4-114">Make sure that the connection between the EBOD controller and the device controller is active by verifying that the four LEDs next to the SAS port on the EBOD controller are green.</span></span>
    
    > [!IMPORTANT]
    > <span data-ttu-id="d15f4-115">Aby zapewnić wysoką dostępność dla systemu, firma Microsoft zaleca ściśle zgodna zasilania okablowania schemat pokazano na poniższym diagramie.</span><span class="sxs-lookup"><span data-stu-id="d15f4-115">To ensure high availability for your system, we recommend that you strictly adhere to the power cabling scheme shown in the following diagram.</span></span>
    > 
    > 
    
    ![Podłączanie kabli do urządzenia 4U zasilania](./media/storsimple-cable-8600-for-power/HCSCableYour4UDeviceforPower.png)
    
    <span data-ttu-id="d15f4-117">**Okablowanie zasilania**</span><span class="sxs-lookup"><span data-stu-id="d15f4-117">**Power cabling**</span></span>
    
    | <span data-ttu-id="d15f4-118">Etykieta</span><span class="sxs-lookup"><span data-stu-id="d15f4-118">Label</span></span> | <span data-ttu-id="d15f4-119">Opis</span><span class="sxs-lookup"><span data-stu-id="d15f4-119">Description</span></span> |
    |:--- |:--- |
    | <span data-ttu-id="d15f4-120">1</span><span class="sxs-lookup"><span data-stu-id="d15f4-120">1</span></span> |<span data-ttu-id="d15f4-121">Obudowa podstawowego</span><span class="sxs-lookup"><span data-stu-id="d15f4-121">Primary enclosure</span></span> |
    | <span data-ttu-id="d15f4-122">2</span><span class="sxs-lookup"><span data-stu-id="d15f4-122">2</span></span> |<span data-ttu-id="d15f4-123">PCM 0</span><span class="sxs-lookup"><span data-stu-id="d15f4-123">PCM 0</span></span> |
    | <span data-ttu-id="d15f4-124">3</span><span class="sxs-lookup"><span data-stu-id="d15f4-124">3</span></span> |<span data-ttu-id="d15f4-125">PCM 1</span><span class="sxs-lookup"><span data-stu-id="d15f4-125">PCM 1</span></span> |
    | <span data-ttu-id="d15f4-126">4</span><span class="sxs-lookup"><span data-stu-id="d15f4-126">4</span></span> |<span data-ttu-id="d15f4-127">Kontrolera 0</span><span class="sxs-lookup"><span data-stu-id="d15f4-127">Controller 0</span></span> |
    | <span data-ttu-id="d15f4-128">5</span><span class="sxs-lookup"><span data-stu-id="d15f4-128">5</span></span> |<span data-ttu-id="d15f4-129">Kontrolera 1</span><span class="sxs-lookup"><span data-stu-id="d15f4-129">Controller 1</span></span> |
    | <span data-ttu-id="d15f4-130">6</span><span class="sxs-lookup"><span data-stu-id="d15f4-130">6</span></span> |<span data-ttu-id="d15f4-131">EBOD kontrolera 0</span><span class="sxs-lookup"><span data-stu-id="d15f4-131">EBOD controller 0</span></span> |
    | <span data-ttu-id="d15f4-132">7</span><span class="sxs-lookup"><span data-stu-id="d15f4-132">7</span></span> |<span data-ttu-id="d15f4-133">EBOD kontrolera 1</span><span class="sxs-lookup"><span data-stu-id="d15f4-133">EBOD controller 1</span></span> |
    | <span data-ttu-id="d15f4-134">8</span><span class="sxs-lookup"><span data-stu-id="d15f4-134">8</span></span> |<span data-ttu-id="d15f4-135">Obudowa EBOD</span><span class="sxs-lookup"><span data-stu-id="d15f4-135">EBOD enclosure</span></span> |
    | <span data-ttu-id="d15f4-136">9</span><span class="sxs-lookup"><span data-stu-id="d15f4-136">9</span></span> |<span data-ttu-id="d15f4-137">PDU</span><span class="sxs-lookup"><span data-stu-id="d15f4-137">PDUs</span></span> |

