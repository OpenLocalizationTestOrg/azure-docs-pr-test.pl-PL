---
title: "aaaTroubleshoot grup zabezpieczeń sieci - PowerShell | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak grup zabezpieczeń sieci tootroubleshoot we wdrożeniu usługi Azure Resource Manager hello modelu przy użyciu programu Azure PowerShell."
services: virtual-network
documentationcenter: na
author: AnithaAdusumilli
manager: narayan
editor: 
tags: azure-resource-manager
ms.assetid: 4c732bb7-5cb1-40af-9e6d-a2a307c2a9c4
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/23/2016
ms.author: anithaa
ms.openlocfilehash: 95fd60fa72cf6d17fa990e3c3eb7d980878f7c15
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-network-security-groups-using-azure-powershell"></a><span data-ttu-id="e18b5-103">Rozwiązywanie problemów z grup zabezpieczeń sieci przy użyciu programu Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="e18b5-103">Troubleshoot Network Security Groups using Azure PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e18b5-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="e18b5-104">Azure Portal</span></span>](virtual-network-nsg-troubleshoot-portal.md)
> * [<span data-ttu-id="e18b5-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e18b5-105">PowerShell</span></span>](virtual-network-nsg-troubleshoot-powershell.md)
> 
> 

<span data-ttu-id="e18b5-106">Jeśli skonfigurowana grup zabezpieczeń sieci (NSG) na maszynie wirtualnej (VM) i występują problemy z połączeniem maszyny Wirtualnej, ten artykuł zawiera omówienie funkcji diagnostyki dla grup NSG toohelp dalsze poszukiwanie rozwiązania problemu.</span><span class="sxs-lookup"><span data-stu-id="e18b5-106">If you configured Network Security Groups (NSGs) on your virtual machine (VM) and are experiencing VM connectivity issues, this article provides an overview of diagnostics capabilities for NSGs toohelp troubleshoot further.</span></span>

<span data-ttu-id="e18b5-107">Grupy NSG pozwalają toocontrol hello rodzaje ruchu przepływające i maszyn wirtualnych (VM).</span><span class="sxs-lookup"><span data-stu-id="e18b5-107">NSGs enable you toocontrol hello types of traffic that flow in and out of your virtual machines (VMs).</span></span> <span data-ttu-id="e18b5-108">Grupy NSG mogą być zastosowane toosubnets w sieci wirtualnej platformy Azure (VNet) i/lub interfejsów sieciowych (NIC).</span><span class="sxs-lookup"><span data-stu-id="e18b5-108">NSGs can be applied toosubnets in an Azure Virtual Network (VNet), network interfaces (NIC), or both.</span></span> <span data-ttu-id="e18b5-109">Hello tooa skuteczne reguły stosowane karty Sieciowej są hello reguł, które istnieją w hello zastosować grupy NSG tooa kart Sieciowych i hello podsieci, w której jest dołączona do agregacji.</span><span class="sxs-lookup"><span data-stu-id="e18b5-109">hello effective rules applied tooa NIC are an aggregation of hello rules that exist in hello NSGs applied tooa NIC and hello subnet it is connected to.</span></span> <span data-ttu-id="e18b5-110">Reguły w tych grup NSG można czasami konflikt ze sobą i mieć wpływ na łączność sieciową z maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="e18b5-110">Rules across these NSGs can sometimes conflict with each other and impact a VM's network connectivity.</span></span>  

<span data-ttu-id="e18b5-111">Można wyświetlić wszystkie reguły efektywnym elementem systemu zabezpieczeń hello z grup NSG, jak stosować kart sieciowych maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="e18b5-111">You can view all hello effective security rules from your NSGs, as applied on your VM's NICs.</span></span> <span data-ttu-id="e18b5-112">W tym artykule opisano, jak przy użyciu tych reguł w problemy z łącznością wirtualna tootroubleshoot hello modelu wdrażania usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="e18b5-112">This article shows how tootroubleshoot VM connectivity issues using these rules in hello Azure Resource Manager deployment model.</span></span> <span data-ttu-id="e18b5-113">Jeśli nie znasz z sieci wirtualnej i NSG pojęcia, przeczytaj hello [sieci wirtualnej](virtual-networks-overview.md) i [sieciowej grupy zabezpieczeń](virtual-networks-nsg.md) omówienie artykułów.</span><span class="sxs-lookup"><span data-stu-id="e18b5-113">If you're not familiar with VNet and NSG concepts, read hello [Virtual network](virtual-networks-overview.md) and [Network security groups](virtual-networks-nsg.md) overview articles.</span></span>

## <a name="using-effective-security-rules-tootroubleshoot-vm-traffic-flow"></a><span data-ttu-id="e18b5-114">Przy użyciu przepływu ruchu maszyny Wirtualnej tootroubleshoot skuteczne reguły zabezpieczeń</span><span class="sxs-lookup"><span data-stu-id="e18b5-114">Using Effective Security Rules tootroubleshoot VM traffic flow</span></span>
<span data-ttu-id="e18b5-115">Hello scenariusz, w którym następuje jest przykładem to powszechny problem połączenia:</span><span class="sxs-lookup"><span data-stu-id="e18b5-115">hello scenario that follows is an example of a common connection problem:</span></span>

<span data-ttu-id="e18b5-116">Maszyna wirtualna o nazwie *VM1* jest częścią podsieci o nazwie *podsieć1* w ramach sieci wirtualnej o nazwie *WestUS VNet1*.</span><span class="sxs-lookup"><span data-stu-id="e18b5-116">A VM named *VM1* is part of a subnet named *Subnet1* within a VNet named *WestUS-VNet1*.</span></span> <span data-ttu-id="e18b5-117">Próba tooconnect toohello maszyny Wirtualnej przy użyciu protokołu RDP za pośrednictwem portu 3389 protokołu TCP nie powiedzie się.</span><span class="sxs-lookup"><span data-stu-id="e18b5-117">An attempt tooconnect toohello VM using RDP over TCP port 3389 fails.</span></span> <span data-ttu-id="e18b5-118">Grupy NSG są stosowane w obu hello kart *VM1 NIC1* i hello podsieci *podsieć1*.</span><span class="sxs-lookup"><span data-stu-id="e18b5-118">NSGs are applied at both hello NIC *VM1-NIC1* and hello subnet *Subnet1*.</span></span> <span data-ttu-id="e18b5-119">Ruch tooTCP portu 3389 jest dozwolony w hello grupy NSG skojarzonej z interfejsem sieciowym hello *VM1 NIC1*, jednak TCP polecenie ping na tooVM1 portu 3389 kończy się niepowodzeniem.</span><span class="sxs-lookup"><span data-stu-id="e18b5-119">Traffic tooTCP port 3389 is allowed in hello NSG associated with hello network interface *VM1-NIC1*, however TCP ping tooVM1's port 3389 fails.</span></span>

<span data-ttu-id="e18b5-120">Gdy w tym przykładzie korzysta z portu 3389 protokołu TCP, hello następujących kroków można używane toodetermine błędów połączenia przychodzącego i wychodzącego przez dowolnego portu.</span><span class="sxs-lookup"><span data-stu-id="e18b5-120">While this example uses TCP port 3389, hello following steps can be used toodetermine inbound and outbound connection failures over any port.</span></span>

## <a name="detailed-troubleshooting-steps"></a><span data-ttu-id="e18b5-121">Szczegółowe kroki rozwiązywania problemów</span><span class="sxs-lookup"><span data-stu-id="e18b5-121">Detailed Troubleshooting Steps</span></span>
<span data-ttu-id="e18b5-122">Wykonaj hello następujące kroki tootroubleshoot grup NSG dla maszyny Wirtualnej:</span><span class="sxs-lookup"><span data-stu-id="e18b5-122">Complete hello following steps tootroubleshoot NSGs for a VM:</span></span>

1. <span data-ttu-id="e18b5-123">Uruchom tooAzure sesji i logowania programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e18b5-123">Start an Azure PowerShell session and login tooAzure.</span></span> <span data-ttu-id="e18b5-124">Jeśli nie masz doświadczenia w obsłudze przy użyciu programu Azure PowerShell, przeczytaj hello [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview) artykułu.</span><span class="sxs-lookup"><span data-stu-id="e18b5-124">If you're not familiar with using Azure PowerShell, read hello [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) article.</span></span>
2. <span data-ttu-id="e18b5-125">Wprowadź hello następujące polecenia tooreturn wszystkie reguły NSG stosowane tooa karty Sieciowej o nazwie *VM1 NIC1* w grupie zasobów hello *RG1*:</span><span class="sxs-lookup"><span data-stu-id="e18b5-125">Enter hello following command tooreturn all NSG rules applied tooa NIC named *VM1-NIC1* in hello resource group *RG1*:</span></span>
   
        Get-AzureRmEffectiveNetworkSecurityGroup -NetworkInterfaceName VM1-NIC1 -ResourceGroupName RG1
   
   > [!TIP]
   > <span data-ttu-id="e18b5-126">Jeśli nie znasz nazwy hello karty sieciowej, wprowadź hello następujące polecenia tooretrieve hello nazwy wszystkich kart sieciowych w grupie zasobów:</span><span class="sxs-lookup"><span data-stu-id="e18b5-126">If you don't know hello name of a NIC, enter hello following command tooretrieve hello names of all NICs in a resource group:</span></span> 
   > 
   > `Get-AzureRmNetworkInterface -ResourceGroupName RG1 | Format-Table Name`
   > 
   > 
   
    <span data-ttu-id="e18b5-127">Witaj następujący tekst jest przykładowe dane wyjściowe skuteczne reguły hello zwrócony dla hello *VM1 NIC1* karty Sieciowej:</span><span class="sxs-lookup"><span data-stu-id="e18b5-127">hello following text is a sample of hello effective rules output returned for hello *VM1-NIC1* NIC:</span></span>
   
        NetworkSecurityGroup   : {
                                   "Id": "/subscriptions/[Subscription ID]/resourceGroups/RG1/providers/Microsoft.Network/networkSecurityGroups/VM1-NIC1-NSG"
                                 }
        Association            : {
                                   "NetworkInterface": {
                                     "Id": "/subscriptions/[Subscription ID]/resourceGroups/RG1/providers/Microsoft.Network/networkInterfaces/VM1-NIC1"
                                   }
                                 }
        EffectiveSecurityRules : [
                                 {
                                 "Name": "securityRules/allowRDP",
                                 "Protocol": "Tcp",
                                 "SourcePortRange": "0-65535",
                                 "DestinationPortRange": "3389-3389",
                                 "SourceAddressPrefix": "Internet",
                                 "DestinationAddressPrefix": "0.0.0.0/0",
                                 "ExpandedSourceAddressPrefix": [… ],
                                 "ExpandedDestinationAddressPrefix": [],
                                 "Access": "Allow",
                                 "Priority": 1000,
                                 "Direction": "Inbound"
                                 },
                                 {
                                 "Name": "defaultSecurityRules/AllowVnetInBound",
                                 "Protocol": "All",
                                 "SourcePortRange": "0-65535",
                                 "DestinationPortRange": "0-65535",
                                 "SourceAddressPrefix": "VirtualNetwork",
                                 "DestinationAddressPrefix": "VirtualNetwork",
                                 "ExpandedSourceAddressPrefix": [
                                  "10.9.0.0/16",
                                  "168.63.129.16/32",
                                  "10.0.0.0/16",
                                  "10.1.0.0/16"
                                  ],
                                 "ExpandedDestinationAddressPrefix": [
                                  "10.9.0.0/16",
                                  "168.63.129.16/32",
                                  "10.0.0.0/16",
                                  "10.1.0.0/16"
                                  ],
                                  "Access": "Allow",
                                  "Priority": 65000,
                                  "Direction": "Inbound"
                                  },…
                         ]
   
        NetworkSecurityGroup   : {
                                   "Id": 
                                 "/subscriptions/[Subscription ID]/resourceGroups/RG1/providers/Microsoft.Network/networkSecurityGroups/Subnet1-NSG"
                                 }
        Association            : {
                                   "Subnet": {
                                     "Id": 
                                 "/subscriptions/[Subscription ID]/resourceGroups/RG1/providers/Microsoft.Network/virtualNetworks/WestUS-VNet1/subnets/Subnet1"
                                 }
                                 }
        EffectiveSecurityRules : [
                                 {
                                "Name": "securityRules/denyRDP",
                                "Protocol": "Tcp",
                                "SourcePortRange": "0-65535",
                                "DestinationPortRange": "3389-3389",
                                "SourceAddressPrefix": "Internet",
                                "DestinationAddressPrefix": "0.0.0.0/0",
                                "ExpandedSourceAddressPrefix": [
                                   ... ],
                                "ExpandedDestinationAddressPrefix": [],
                                "Access": "Deny",
                                "Priority": 1000,
                                "Direction": "Inbound"
                                },
                                {
                                "Name": "defaultSecurityRules/AllowVnetInBound",
                                "Protocol": "All",
                                "SourcePortRange": "0-65535",
                                "DestinationPortRange": "0-65535",
                                "SourceAddressPrefix": "VirtualNetwork",
                                "DestinationAddressPrefix": "VirtualNetwork",
                                "ExpandedSourceAddressPrefix": [
                                "10.9.0.0/16",
                                "168.63.129.16/32",
                                "10.0.0.0/16",
                                "10.1.0.0/16"
                                ],
                                "ExpandedDestinationAddressPrefix": [
                                "10.9.0.0/16",
                                "168.63.129.16/32",
                                "10.0.0.0/16",
                                "10.1.0.0/16"
                                ],
                                "Access": "Allow",
                                "Priority": 65000,
                                "Direction": "Inbound"
                                },...
                                ]
   
    <span data-ttu-id="e18b5-128">Należy uwzględnić następujące informacje w danych wyjściowych hello hello:</span><span class="sxs-lookup"><span data-stu-id="e18b5-128">Note hello following information in hello output:</span></span>
   
   * <span data-ttu-id="e18b5-129">Istnieją dwa **grupy NetworkSecurityGroup** sekcje: jedna jest skojarzony z podsiecią (*podsieć1*) i jest ono skojarzone z jedną kartą Sieciową (*VM1 NIC1*).</span><span class="sxs-lookup"><span data-stu-id="e18b5-129">There are two **NetworkSecurityGroup** sections: One is associated with a subnet (*Subnet1*) and one is associated with a NIC (*VM1-NIC1*).</span></span> <span data-ttu-id="e18b5-130">W tym przykładzie grupy NSG została zastosowana tooeach.</span><span class="sxs-lookup"><span data-stu-id="e18b5-130">In this example, an NSG has been applied tooeach.</span></span>
   * <span data-ttu-id="e18b5-131">**Skojarzenie** pokazuje hello zasobów (podsieci lub kartę interfejsu Sieciowego) danego grupa NSG jest skojarzona z.</span><span class="sxs-lookup"><span data-stu-id="e18b5-131">**Association** shows hello resource (subnet or NIC) a given NSG is associated with.</span></span> <span data-ttu-id="e18b5-132">W przypadku hello zasób NSG przenieść/usunąć skojarzenia bezpośrednio przed uruchomieniem tego polecenia, może być konieczne toowait kilka sekund dla hello tooreflect zmiany w danych wyjściowych polecenia hello.</span><span class="sxs-lookup"><span data-stu-id="e18b5-132">If hello NSG resource is moved/disassociated immediately before running this command, you may need toowait a few seconds for hello change tooreflect in hello command output.</span></span> 
   * <span data-ttu-id="e18b5-133">nazwy reguł, które są poprzedzone znakiem Hello *defaultSecurityRules*: gdy grupa NSG jest tworzona, kilka domyślnych reguł zabezpieczeń są tworzone w niej.</span><span class="sxs-lookup"><span data-stu-id="e18b5-133">hello rule names that are prefaced with *defaultSecurityRules*: When an NSG is created, several default security rules are created within it.</span></span> <span data-ttu-id="e18b5-134">Nie można usunąć domyślnej reguły, ale mogą być zastąpione wyższy priorytet reguły.</span><span class="sxs-lookup"><span data-stu-id="e18b5-134">Default rules can't be removed, but they can be overridden with higher priority rules.</span></span>
     <span data-ttu-id="e18b5-135">Witaj odczytu [omówienie NSG](virtual-networks-nsg.md#default-rules) toolearn artykułu więcej informacji na temat NSG domyślne zasady zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="e18b5-135">Read hello [NSG overview](virtual-networks-nsg.md#default-rules) article toolearn more about NSG default security rules.</span></span>
   * <span data-ttu-id="e18b5-136">**ExpandedAddressPrefix** rozszerza hello prefiksy adresów dla znaczników domyślnych NSG.</span><span class="sxs-lookup"><span data-stu-id="e18b5-136">**ExpandedAddressPrefix** expands hello address prefixes for NSG default tags.</span></span> <span data-ttu-id="e18b5-137">Tagi reprezentują wiele prefiksów adresów.</span><span class="sxs-lookup"><span data-stu-id="e18b5-137">Tags represent multiple address prefixes.</span></span> <span data-ttu-id="e18b5-138">Rozszerzenia znaczników hello mogą być przydatne podczas rozwiązywania problemów z łącznością maszyny Wirtualnej z określonego adresu prefiksy.</span><span class="sxs-lookup"><span data-stu-id="e18b5-138">Expansion of hello tags can be useful when troubleshooting VM connectivity to/from specific address prefixes.</span></span> <span data-ttu-id="e18b5-139">Na przykład z sieci Wirtualnej komunikacji równorzędnej, VIRTUAL_NETWORK tag rozszerza tooshow połączyć za pomocą prefiksy sieci wirtualnej w danych wyjściowych poprzedniej hello.</span><span class="sxs-lookup"><span data-stu-id="e18b5-139">For example, with VNET peering, VIRTUAL_NETWORK tag expands tooshow peered VNet prefixes in hello previous output.</span></span>
     
     > [!NOTE]
     > <span data-ttu-id="e18b5-140">Witaj polecenia tylko pokazuje skuteczne reguły, jeśli grupa NSG jest skojarzona z podsiecią, karta sieciowa lub obu.</span><span class="sxs-lookup"><span data-stu-id="e18b5-140">hello command only shows effective rules if an NSG is associated with either a subnet, a NIC, or both.</span></span> <span data-ttu-id="e18b5-141">Maszyna wirtualna może mieć wiele kart sieciowych z różnych grup NSG stosowana.</span><span class="sxs-lookup"><span data-stu-id="e18b5-141">A VM may have multiple NICs with different NSGs applied.</span></span> <span data-ttu-id="e18b5-142">Podczas rozwiązywania problemu, uruchom polecenie powitania dla poszczególnych kart sieciowych.</span><span class="sxs-lookup"><span data-stu-id="e18b5-142">When troubleshooting, run hello command for each NIC.</span></span>
     > 
     > 
3. <span data-ttu-id="e18b5-143">tooease filtrowania przez większą liczbę reguły NSG, wprowadź następujące dodatkowe polecenia tootroubleshoot hello:</span><span class="sxs-lookup"><span data-stu-id="e18b5-143">tooease filtering over larger number of NSG rules, enter hello following commands tootroubleshoot further:</span></span> 
   
        $NSGs = Get-AzureRmEffectiveNetworkSecurityGroup -NetworkInterfaceName VM1-NIC1 -ResourceGroupName RG1
        $NSGs.EffectiveSecurityRules | Sort-Object Direction, Access, Priority | Out-GridView
   
    <span data-ttu-id="e18b5-144">Filtr dla ruchu protokołu RDP (TCP port 3389), jest stosowane toohello widoku siatki, jak pokazano na poniższej ilustracji hello:</span><span class="sxs-lookup"><span data-stu-id="e18b5-144">A filter for RDP traffic (TCP port 3389), is applied toohello grid view, as shown in hello following picture:</span></span>
   
    ![Lista reguł](./media/virtual-network-nsg-troubleshoot-powershell/rules.png)
4. <span data-ttu-id="e18b5-146">Jak widać w widoku siatki hello, istnieją zarówno zezwalania i odmowy reguły protokołu RDP.</span><span class="sxs-lookup"><span data-stu-id="e18b5-146">As you can see in hello grid view, there are both allow and deny rules for RDP.</span></span> <span data-ttu-id="e18b5-147">Witaj dane wyjściowe z kroku 2 zawierają hello tego *DenyRDP* reguła jest hello grupa NSG stosowana toohello podsieci.</span><span class="sxs-lookup"><span data-stu-id="e18b5-147">hello output from step 2 shows that hello *DenyRDP* rule is in hello NSG applied toohello subnet.</span></span> <span data-ttu-id="e18b5-148">Dla reguł ruchu przychodzącego grupy NSG stosowana toohello podsieci są przetwarzane jako pierwsze.</span><span class="sxs-lookup"><span data-stu-id="e18b5-148">For inbound rules, NSGs applied toohello subnet are processed first.</span></span> <span data-ttu-id="e18b5-149">W przypadku odnalezienia pasującego interfejsu sieciowego toohello grupa NSG stosowana hello nie został przetworzony.</span><span class="sxs-lookup"><span data-stu-id="e18b5-149">If a match is found, hello NSG applied toohello network interface is not processed.</span></span> <span data-ttu-id="e18b5-150">W takim przypadku hello *DenyRDP* reguła z podsieci hello blokuje toohello RDP maszyny Wirtualnej (**VM1**).</span><span class="sxs-lookup"><span data-stu-id="e18b5-150">In this case, hello *DenyRDP* rule from hello subnet blocks RDP toohello VM (**VM1**).</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="e18b5-151">Maszyna wirtualna może mieć wiele kart sieciowych tooit dołączone.</span><span class="sxs-lookup"><span data-stu-id="e18b5-151">A VM may have multiple NICs attached tooit.</span></span> <span data-ttu-id="e18b5-152">Każdy może być połączone tooa innej podsieci.</span><span class="sxs-lookup"><span data-stu-id="e18b5-152">Each may be connected tooa different subnet.</span></span> <span data-ttu-id="e18b5-153">Ponieważ polecenia hello w poprzednich krokach hello są uruchamiane przed karty Sieciowej, ważne jest, tooensure, który określisz hello w przypadku wystąpienia awarii łączności hello do karty Sieciowej.</span><span class="sxs-lookup"><span data-stu-id="e18b5-153">Since hello commands in hello previous steps are run against a NIC, it's important tooensure that you specify hello NIC you're having hello connectivity failure to.</span></span> <span data-ttu-id="e18b5-154">Jeśli nie masz pewności, będzie można uruchamiać polecenia hello przed każdym toohello kartę Sieciową podłączoną maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="e18b5-154">If you're not sure, you can always run hello commands against each NIC attached toohello VM.</span></span>
   > 
   > 
5. <span data-ttu-id="e18b5-155">tooRDP do VM1, zmień hello *odmowy protokołu RDP (3389)* reguły zbyt*Zezwalaj RDP(3389)* w hello **NSG podsieć1** NSG.</span><span class="sxs-lookup"><span data-stu-id="e18b5-155">tooRDP into VM1, change hello *Deny RDP (3389)* rule too*Allow RDP(3389)* in hello **Subnet1-NSG** NSG.</span></span> <span data-ttu-id="e18b5-156">Upewnij się, że portu 3389 protokołu TCP jest otwarty przez otwarcie toohello połączenia RDP maszyny Wirtualnej lub za pomocą narzędzia narzędzia PsPing hello.</span><span class="sxs-lookup"><span data-stu-id="e18b5-156">Confirm that TCP port 3389 is open by opening an RDP connection toohello VM or using hello PsPing tool.</span></span> <span data-ttu-id="e18b5-157">Użytkownik może dowiedzieć się więcej o narzędzia PsPing za odczytywanie hello [stronę pobierania narzędzia PsPing](https://technet.microsoft.com/sysinternals/psping.aspx)</span><span class="sxs-lookup"><span data-stu-id="e18b5-157">You can learn more about PsPing by reading hello [PsPing download page](https://technet.microsoft.com/sysinternals/psping.aspx)</span></span>
   
    <span data-ttu-id="e18b5-158">Można lub usuń reguły z grupy NSG przy użyciu hello informacji w danych wyjściowych hello z hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="e18b5-158">You can or remove rules from an NSG by using hello information in hello output from hello following command:</span></span>
   
        Get-Help *-AzureRmNetworkSecurityRuleConfig

## <a name="considerations"></a><span data-ttu-id="e18b5-159">Zagadnienia do rozważenia</span><span class="sxs-lookup"><span data-stu-id="e18b5-159">Considerations</span></span>
<span data-ttu-id="e18b5-160">Należy wziąć pod uwagę następujące punkty podczas rozwiązywania problemów z łącznością hello:</span><span class="sxs-lookup"><span data-stu-id="e18b5-160">Consider hello following points when troubleshooting connectivity problems:</span></span>

* <span data-ttu-id="e18b5-161">Reguły NSG domyślne zablokuje dostęp przychodzący do z hello internet i zezwolenia sieci wirtualnej ruch przychodzący.</span><span class="sxs-lookup"><span data-stu-id="e18b5-161">Default NSG rules will block inbound access from hello internet and only permit VNet inbound traffic.</span></span> <span data-ttu-id="e18b5-162">Zasady należy jawnie dodać tooallow ruchu przychodzącego dla dostępu z Internetu, zgodnie z potrzebami.</span><span class="sxs-lookup"><span data-stu-id="e18b5-162">Rules should be explicitly added tooallow inbound access from Internet, as required.</span></span>
* <span data-ttu-id="e18b5-163">Jeśli nie żadnych reguł zabezpieczeń grupy NSG powoduje toofail łączności sieciowej maszyny Wirtualnej, hello problem może być:</span><span class="sxs-lookup"><span data-stu-id="e18b5-163">If there are no NSG security rules causing a VM’s network connectivity toofail, hello problem may be due to:</span></span>
  * <span data-ttu-id="e18b5-164">Oprogramowanie zapory w systemie operacyjnym hello maszyny Wirtualnej</span><span class="sxs-lookup"><span data-stu-id="e18b5-164">Firewall software running within hello VM's operating system</span></span>
  * <span data-ttu-id="e18b5-165">Trasy skonfigurowanych dla urządzenia wirtualnego lub ruch lokalny.</span><span class="sxs-lookup"><span data-stu-id="e18b5-165">Routes configured for virtual appliances or on-premises traffic.</span></span> <span data-ttu-id="e18b5-166">Ruch internetowy może być przekierowane tooon lokalnych przy użyciu tunelowania wymuszonego.</span><span class="sxs-lookup"><span data-stu-id="e18b5-166">Internet traffic can be redirected tooon-premises via forced-tunneling.</span></span> <span data-ttu-id="e18b5-167">Połączenia protokołu RDP/SSH z tooyour Internet hello maszyna wirtualna może nie działać to ustawienie, w zależności od tego, jak sprzętu sieciowego lokalne powitania obsługuje ten ruch.</span><span class="sxs-lookup"><span data-stu-id="e18b5-167">An RDP/SSH connection from hello Internet tooyour VM may not work with this setting, depending on how hello on-premises network hardware handles this traffic.</span></span> <span data-ttu-id="e18b5-168">Odczyt hello [Rozwiązywanie problemów z tras](virtual-network-routes-troubleshoot-powershell.md) toolearn artykułu, jak toodiagnose trasy problemów, które mogą utrudnić hello przepływu ruchu w hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="e18b5-168">Read hello [Troubleshooting Routes](virtual-network-routes-troubleshoot-powershell.md) article toolearn how toodiagnose route problems that may be impeding hello flow of traffic in and out of hello VM.</span></span> 
* <span data-ttu-id="e18b5-169">Jeśli ma połączyć za pomocą sieci wirtualnych, domyślnie, hello VIRTUAL_NETWORK tag automatycznie rozwiń tooinclude prefiksy dla połączyć za pomocą sieci wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="e18b5-169">If you have peered VNets, by default, hello VIRTUAL_NETWORK tag will automatically expand tooinclude prefixes for peered VNets.</span></span> <span data-ttu-id="e18b5-170">Prefiksy te można wyświetlić w hello **ExpandedAddressPrefix** listy tootroubleshoot żadnych problemów powiązanych tooVNet równorzędna łączności.</span><span class="sxs-lookup"><span data-stu-id="e18b5-170">You can view these prefixes in hello **ExpandedAddressPrefix** list, tootroubleshoot any issues related tooVNet peering connectivity.</span></span> 
* <span data-ttu-id="e18b5-171">Reguły efektywnym elementem systemu zabezpieczeń są wyświetlane tylko jeśli istnieje grupa NSG skojarzonego z hello maszyny Wirtualnej karty Sieciowej i podsieci.</span><span class="sxs-lookup"><span data-stu-id="e18b5-171">Effective security rules are only shown if there is an NSG associated with hello VM’s NIC and or subnet.</span></span> 
* <span data-ttu-id="e18b5-172">Jeśli nie ma żadnych grup NSG skojarzone z hello karty Sieciowej lub w podsieci i publicznego adresu IP przypisany tooyour maszyna wirtualna, wszystkie porty jest otwarte dla przychodzący i wychodzący dostęp.</span><span class="sxs-lookup"><span data-stu-id="e18b5-172">If there are no NSGs associated with hello NIC or subnet and you have a public IP address assigned tooyour VM, all ports will be open for inbound and outbound access.</span></span> <span data-ttu-id="e18b5-173">Jeśli hello maszyna wirtualna ma publiczny adres IP, zdecydowanie zalecane jest stosowanie toohello grup NSG karty Sieciowej lub podsieci.</span><span class="sxs-lookup"><span data-stu-id="e18b5-173">If hello VM has a public IP address, applying NSGs toohello NIC or subnet is strongly recommended.</span></span>  

