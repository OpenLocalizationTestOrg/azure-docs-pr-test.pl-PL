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
# <a name="troubleshoot-network-security-groups-using-azure-powershell"></a>Rozwiązywanie problemów z grup zabezpieczeń sieci przy użyciu programu Azure PowerShell
> [!div class="op_single_selector"]
> * [Azure Portal](virtual-network-nsg-troubleshoot-portal.md)
> * [PowerShell](virtual-network-nsg-troubleshoot-powershell.md)
> 
> 

Jeśli skonfigurowana grup zabezpieczeń sieci (NSG) na maszynie wirtualnej (VM) i występują problemy z połączeniem maszyny Wirtualnej, ten artykuł zawiera omówienie funkcji diagnostyki dla grup NSG toohelp dalsze poszukiwanie rozwiązania problemu.

Grupy NSG pozwalają toocontrol hello rodzaje ruchu przepływające i maszyn wirtualnych (VM). Grupy NSG mogą być zastosowane toosubnets w sieci wirtualnej platformy Azure (VNet) i/lub interfejsów sieciowych (NIC). Hello tooa skuteczne reguły stosowane karty Sieciowej są hello reguł, które istnieją w hello zastosować grupy NSG tooa kart Sieciowych i hello podsieci, w której jest dołączona do agregacji. Reguły w tych grup NSG można czasami konflikt ze sobą i mieć wpływ na łączność sieciową z maszyny Wirtualnej.  

Można wyświetlić wszystkie reguły efektywnym elementem systemu zabezpieczeń hello z grup NSG, jak stosować kart sieciowych maszyny Wirtualnej. W tym artykule opisano, jak przy użyciu tych reguł w problemy z łącznością wirtualna tootroubleshoot hello modelu wdrażania usługi Azure Resource Manager. Jeśli nie znasz z sieci wirtualnej i NSG pojęcia, przeczytaj hello [sieci wirtualnej](virtual-networks-overview.md) i [sieciowej grupy zabezpieczeń](virtual-networks-nsg.md) omówienie artykułów.

## <a name="using-effective-security-rules-tootroubleshoot-vm-traffic-flow"></a>Przy użyciu przepływu ruchu maszyny Wirtualnej tootroubleshoot skuteczne reguły zabezpieczeń
Hello scenariusz, w którym następuje jest przykładem to powszechny problem połączenia:

Maszyna wirtualna o nazwie *VM1* jest częścią podsieci o nazwie *podsieć1* w ramach sieci wirtualnej o nazwie *WestUS VNet1*. Próba tooconnect toohello maszyny Wirtualnej przy użyciu protokołu RDP za pośrednictwem portu 3389 protokołu TCP nie powiedzie się. Grupy NSG są stosowane w obu hello kart *VM1 NIC1* i hello podsieci *podsieć1*. Ruch tooTCP portu 3389 jest dozwolony w hello grupy NSG skojarzonej z interfejsem sieciowym hello *VM1 NIC1*, jednak TCP polecenie ping na tooVM1 portu 3389 kończy się niepowodzeniem.

Gdy w tym przykładzie korzysta z portu 3389 protokołu TCP, hello następujących kroków można używane toodetermine błędów połączenia przychodzącego i wychodzącego przez dowolnego portu.

## <a name="detailed-troubleshooting-steps"></a>Szczegółowe kroki rozwiązywania problemów
Wykonaj hello następujące kroki tootroubleshoot grup NSG dla maszyny Wirtualnej:

1. Uruchom tooAzure sesji i logowania programu Azure PowerShell. Jeśli nie masz doświadczenia w obsłudze przy użyciu programu Azure PowerShell, przeczytaj hello [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview) artykułu.
2. Wprowadź hello następujące polecenia tooreturn wszystkie reguły NSG stosowane tooa karty Sieciowej o nazwie *VM1 NIC1* w grupie zasobów hello *RG1*:
   
        Get-AzureRmEffectiveNetworkSecurityGroup -NetworkInterfaceName VM1-NIC1 -ResourceGroupName RG1
   
   > [!TIP]
   > Jeśli nie znasz nazwy hello karty sieciowej, wprowadź hello następujące polecenia tooretrieve hello nazwy wszystkich kart sieciowych w grupie zasobów: 
   > 
   > `Get-AzureRmNetworkInterface -ResourceGroupName RG1 | Format-Table Name`
   > 
   > 
   
    Witaj następujący tekst jest przykładowe dane wyjściowe skuteczne reguły hello zwrócony dla hello *VM1 NIC1* karty Sieciowej:
   
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
   
    Należy uwzględnić następujące informacje w danych wyjściowych hello hello:
   
   * Istnieją dwa **grupy NetworkSecurityGroup** sekcje: jedna jest skojarzony z podsiecią (*podsieć1*) i jest ono skojarzone z jedną kartą Sieciową (*VM1 NIC1*). W tym przykładzie grupy NSG została zastosowana tooeach.
   * **Skojarzenie** pokazuje hello zasobów (podsieci lub kartę interfejsu Sieciowego) danego grupa NSG jest skojarzona z. W przypadku hello zasób NSG przenieść/usunąć skojarzenia bezpośrednio przed uruchomieniem tego polecenia, może być konieczne toowait kilka sekund dla hello tooreflect zmiany w danych wyjściowych polecenia hello. 
   * nazwy reguł, które są poprzedzone znakiem Hello *defaultSecurityRules*: gdy grupa NSG jest tworzona, kilka domyślnych reguł zabezpieczeń są tworzone w niej. Nie można usunąć domyślnej reguły, ale mogą być zastąpione wyższy priorytet reguły.
     Witaj odczytu [omówienie NSG](virtual-networks-nsg.md#default-rules) toolearn artykułu więcej informacji na temat NSG domyślne zasady zabezpieczeń.
   * **ExpandedAddressPrefix** rozszerza hello prefiksy adresów dla znaczników domyślnych NSG. Tagi reprezentują wiele prefiksów adresów. Rozszerzenia znaczników hello mogą być przydatne podczas rozwiązywania problemów z łącznością maszyny Wirtualnej z określonego adresu prefiksy. Na przykład z sieci Wirtualnej komunikacji równorzędnej, VIRTUAL_NETWORK tag rozszerza tooshow połączyć za pomocą prefiksy sieci wirtualnej w danych wyjściowych poprzedniej hello.
     
     > [!NOTE]
     > Witaj polecenia tylko pokazuje skuteczne reguły, jeśli grupa NSG jest skojarzona z podsiecią, karta sieciowa lub obu. Maszyna wirtualna może mieć wiele kart sieciowych z różnych grup NSG stosowana. Podczas rozwiązywania problemu, uruchom polecenie powitania dla poszczególnych kart sieciowych.
     > 
     > 
3. tooease filtrowania przez większą liczbę reguły NSG, wprowadź następujące dodatkowe polecenia tootroubleshoot hello: 
   
        $NSGs = Get-AzureRmEffectiveNetworkSecurityGroup -NetworkInterfaceName VM1-NIC1 -ResourceGroupName RG1
        $NSGs.EffectiveSecurityRules | Sort-Object Direction, Access, Priority | Out-GridView
   
    Filtr dla ruchu protokołu RDP (TCP port 3389), jest stosowane toohello widoku siatki, jak pokazano na poniższej ilustracji hello:
   
    ![Lista reguł](./media/virtual-network-nsg-troubleshoot-powershell/rules.png)
4. Jak widać w widoku siatki hello, istnieją zarówno zezwalania i odmowy reguły protokołu RDP. Witaj dane wyjściowe z kroku 2 zawierają hello tego *DenyRDP* reguła jest hello grupa NSG stosowana toohello podsieci. Dla reguł ruchu przychodzącego grupy NSG stosowana toohello podsieci są przetwarzane jako pierwsze. W przypadku odnalezienia pasującego interfejsu sieciowego toohello grupa NSG stosowana hello nie został przetworzony. W takim przypadku hello *DenyRDP* reguła z podsieci hello blokuje toohello RDP maszyny Wirtualnej (**VM1**).
   
   > [!NOTE]
   > Maszyna wirtualna może mieć wiele kart sieciowych tooit dołączone. Każdy może być połączone tooa innej podsieci. Ponieważ polecenia hello w poprzednich krokach hello są uruchamiane przed karty Sieciowej, ważne jest, tooensure, który określisz hello w przypadku wystąpienia awarii łączności hello do karty Sieciowej. Jeśli nie masz pewności, będzie można uruchamiać polecenia hello przed każdym toohello kartę Sieciową podłączoną maszyny Wirtualnej.
   > 
   > 
5. tooRDP do VM1, zmień hello *odmowy protokołu RDP (3389)* reguły zbyt*Zezwalaj RDP(3389)* w hello **NSG podsieć1** NSG. Upewnij się, że portu 3389 protokołu TCP jest otwarty przez otwarcie toohello połączenia RDP maszyny Wirtualnej lub za pomocą narzędzia narzędzia PsPing hello. Użytkownik może dowiedzieć się więcej o narzędzia PsPing za odczytywanie hello [stronę pobierania narzędzia PsPing](https://technet.microsoft.com/sysinternals/psping.aspx)
   
    Można lub usuń reguły z grupy NSG przy użyciu hello informacji w danych wyjściowych hello z hello następujące polecenie:
   
        Get-Help *-AzureRmNetworkSecurityRuleConfig

## <a name="considerations"></a>Zagadnienia do rozważenia
Należy wziąć pod uwagę następujące punkty podczas rozwiązywania problemów z łącznością hello:

* Reguły NSG domyślne zablokuje dostęp przychodzący do z hello internet i zezwolenia sieci wirtualnej ruch przychodzący. Zasady należy jawnie dodać tooallow ruchu przychodzącego dla dostępu z Internetu, zgodnie z potrzebami.
* Jeśli nie żadnych reguł zabezpieczeń grupy NSG powoduje toofail łączności sieciowej maszyny Wirtualnej, hello problem może być:
  * Oprogramowanie zapory w systemie operacyjnym hello maszyny Wirtualnej
  * Trasy skonfigurowanych dla urządzenia wirtualnego lub ruch lokalny. Ruch internetowy może być przekierowane tooon lokalnych przy użyciu tunelowania wymuszonego. Połączenia protokołu RDP/SSH z tooyour Internet hello maszyna wirtualna może nie działać to ustawienie, w zależności od tego, jak sprzętu sieciowego lokalne powitania obsługuje ten ruch. Odczyt hello [Rozwiązywanie problemów z tras](virtual-network-routes-troubleshoot-powershell.md) toolearn artykułu, jak toodiagnose trasy problemów, które mogą utrudnić hello przepływu ruchu w hello maszyny Wirtualnej. 
* Jeśli ma połączyć za pomocą sieci wirtualnych, domyślnie, hello VIRTUAL_NETWORK tag automatycznie rozwiń tooinclude prefiksy dla połączyć za pomocą sieci wirtualnych. Prefiksy te można wyświetlić w hello **ExpandedAddressPrefix** listy tootroubleshoot żadnych problemów powiązanych tooVNet równorzędna łączności. 
* Reguły efektywnym elementem systemu zabezpieczeń są wyświetlane tylko jeśli istnieje grupa NSG skojarzonego z hello maszyny Wirtualnej karty Sieciowej i podsieci. 
* Jeśli nie ma żadnych grup NSG skojarzone z hello karty Sieciowej lub w podsieci i publicznego adresu IP przypisany tooyour maszyna wirtualna, wszystkie porty jest otwarte dla przychodzący i wychodzący dostęp. Jeśli hello maszyna wirtualna ma publiczny adres IP, zdecydowanie zalecane jest stosowanie toohello grup NSG karty Sieciowej lub podsieci.  

