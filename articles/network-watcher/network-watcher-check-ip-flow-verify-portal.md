---
title: "Sprawdź aaaVerify ruchu z przepływem IP obserwatora sieci platformy Azure - Azure portal | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano sposób toocheck Jeśli tooor ruch z maszyny wirtualnej jest dozwolony lub niedozwolony"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: e0e3e9a8-70eb-409a-a744-0ce9deb27148
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: abf639f36d32f3416dd927e66b635267b746e62f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="check-if-traffic-is-allowed-or-denied-tooor-from-a-vm-with-ip-flow-verify-a-component-of-azure-network-watcher"></a><span data-ttu-id="2a5dd-103">Sprawdź, czy ruch jest dozwolony lub z maszyny Wirtualnej z przepływem Sprawdź IP zabronione tooor a składnik Azure obserwatora sieciowego</span><span class="sxs-lookup"><span data-stu-id="2a5dd-103">Check if traffic is allowed or denied tooor from a VM with IP Flow Verify a component of Azure Network Watcher</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="2a5dd-104">Witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="2a5dd-104">Azure portal</span></span>](network-watcher-check-ip-flow-verify-portal.md)
> - [<span data-ttu-id="2a5dd-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="2a5dd-105">PowerShell</span></span>](network-watcher-check-ip-flow-verify-powershell.md)
> - [<span data-ttu-id="2a5dd-106">Interfejs wiersza polecenia 1.0</span><span class="sxs-lookup"><span data-stu-id="2a5dd-106">CLI 1.0</span></span>](network-watcher-check-ip-flow-verify-cli-nodejs.md)
> - [<span data-ttu-id="2a5dd-107">Interfejs wiersza polecenia 2.0</span><span class="sxs-lookup"><span data-stu-id="2a5dd-107">CLI 2.0</span></span>](network-watcher-check-ip-flow-verify-cli.md)
> - [<span data-ttu-id="2a5dd-108">Interfejs API Azure REST</span><span class="sxs-lookup"><span data-stu-id="2a5dd-108">Azure REST API</span></span>](network-watcher-check-ip-flow-verify-rest.md)


<span data-ttu-id="2a5dd-109">Sprawdź przepływ IP jest funkcją obserwatora sieciowego, który umożliwia tooverify Jeśli ruch jest dozwolony tooor z maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="2a5dd-109">IP flow verify is a feature of Network Watcher that allows you tooverify if traffic is allowed tooor from a virtual machine.</span></span> <span data-ttu-id="2a5dd-110">Sprawdzanie poprawności Hello mogą być uruchamiane dla ruchu przychodzącego lub wychodzącego.</span><span class="sxs-lookup"><span data-stu-id="2a5dd-110">hello validation can be run for incoming or outgoing traffic.</span></span> <span data-ttu-id="2a5dd-111">Ten scenariusz jest przydatne tooget bieżący stan czy maszynę wirtualną można rozmawiać zasobu zewnętrznego tooan lub innego zasobu.</span><span class="sxs-lookup"><span data-stu-id="2a5dd-111">This scenario is useful tooget a current state of whether a virtual machine can talk tooan external resource or another resource.</span></span> <span data-ttu-id="2a5dd-112">Sprawdź przepływ IP można tooverify używane w regułach grupy zabezpieczeń sieci (NSG) są prawidłowo skonfigurowane i rozwiązywania problemów z przepływów, które są blokowane przez reguły NSG.</span><span class="sxs-lookup"><span data-stu-id="2a5dd-112">IP flow verify can be used tooverify if your Network Security Group (NSG) rules are properly configured and troubleshoot flows that are being blocked by NSG rules.</span></span> <span data-ttu-id="2a5dd-113">Inną przyczyną przy użyciu protokołu IP przepływu Sprawdź tooensure ruchu, które mają zablokowany jest prawidłowo blokowane przez hello NSG.</span><span class="sxs-lookup"><span data-stu-id="2a5dd-113">Another reason for using IP flow verify is tooensure traffic that you want blocked is being blocked properly by hello NSG.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="2a5dd-114">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="2a5dd-114">Before you begin</span></span>

<span data-ttu-id="2a5dd-115">W tym scenariuszu przyjęto zostały już wykonane kroki hello [utworzyć obserwatora sieciowego](network-watcher-create.md) toocreate obserwatora sieciowego lub istniejącego wystąpienia obserwatora sieciowego.</span><span class="sxs-lookup"><span data-stu-id="2a5dd-115">This scenario assumes you have already followed hello steps in [Create a Network Watcher](network-watcher-create.md) toocreate a Network Watcher or have an existing instance of Network Watcher.</span></span> <span data-ttu-id="2a5dd-116">Scenariusz Hello również założono, że grupa zasobów o prawidłową maszynę wirtualną istnieje toobe używane.</span><span class="sxs-lookup"><span data-stu-id="2a5dd-116">hello scenario also assumes that a Resource Group with a valid virtual machine exists toobe used.</span></span>

## <a name="scenario"></a><span data-ttu-id="2a5dd-117">Scenariusz</span><span class="sxs-lookup"><span data-stu-id="2a5dd-117">Scenario</span></span>

<span data-ttu-id="2a5dd-118">W tym scenariuszu tooverify IP przepływu Sprawdź, czy maszynę wirtualną można rozmawiać tooanother komputera za pośrednictwem portu 443.</span><span class="sxs-lookup"><span data-stu-id="2a5dd-118">This scenario uses IP Flow Verify tooverify if a virtual machine can talk tooanother machine over port 443.</span></span> <span data-ttu-id="2a5dd-119">Ruch hello jest niedozwolone, zwraca hello reguły zabezpieczeń, która odrzuciła ten ruch.</span><span class="sxs-lookup"><span data-stu-id="2a5dd-119">If hello traffic is denied, it returns hello security rule that is denying that traffic.</span></span> <span data-ttu-id="2a5dd-120">toolearn więcej informacji na temat przepływu Sprawdź IP, odwiedź stronę [przepływu IP Sprawdź — omówienie](network-watcher-ip-flow-verify-overview.md)</span><span class="sxs-lookup"><span data-stu-id="2a5dd-120">toolearn more about IP Flow Verify, visit [IP Flow Verify Overview](network-watcher-ip-flow-verify-overview.md)</span></span>

### <a name="run-ip-flow-verify"></a><span data-ttu-id="2a5dd-121">Sprawdź uruchomienia przepływu IP</span><span class="sxs-lookup"><span data-stu-id="2a5dd-121">Run IP flow verify</span></span>

<span data-ttu-id="2a5dd-122">Przejdź tooyour obserwatora sieciowego i kliknij **Sprawdź przepływ IP**.</span><span class="sxs-lookup"><span data-stu-id="2a5dd-122">Navigate tooyour Network Watcher and click **IP flow verify**.</span></span> <span data-ttu-id="2a5dd-123">Wybierz maszynę wirtualną hello i interfejsu sieciowego interesujące tooverify ruch z.</span><span class="sxs-lookup"><span data-stu-id="2a5dd-123">Select hello virtual machine and network interface you want tooverify traffic from.</span></span> <span data-ttu-id="2a5dd-124">Wprowadź wszelkie dodatkowe informacje filtrowania, a następnie kliknij przycisk **Sprawdź**.</span><span class="sxs-lookup"><span data-stu-id="2a5dd-124">Enter any additional filtering information and click **Check**.</span></span>

<span data-ttu-id="2a5dd-125">Po kliknięciu **Sprawdź**, hello przepływem na podstawie podanych kryteriów hello jest zaznaczony.</span><span class="sxs-lookup"><span data-stu-id="2a5dd-125">Once you click **Check**, hello flow based on hello criteria you provided is checked.</span></span> <span data-ttu-id="2a5dd-126">wynik Hello jest **dozwolony dostęp do** lub **odmowa dostępu**.</span><span class="sxs-lookup"><span data-stu-id="2a5dd-126">hello result is either **Access allowed** or **Access denied**.</span></span> <span data-ttu-id="2a5dd-127">W przypadku odmowy dostępu hello grupy zabezpieczeń sieci (NSG) i podano reguły zabezpieczeń, która blokowania ruchu.</span><span class="sxs-lookup"><span data-stu-id="2a5dd-127">If access is denied, hello Network Security Group (NSG) and security rule that block traffic is provided.</span></span> <span data-ttu-id="2a5dd-128">Jeśli odmowa hello ruchu jest oczekiwane zachowanie, reguła hello zakończyło się pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="2a5dd-128">If hello denial of traffic is expected behavior, then hello rule was successful.</span></span>

> [!NOTE]
> <span data-ttu-id="2a5dd-129">Sprawdź przepływ IP wymaga, aby hello zasobu maszyny Wirtualnej jest przydzielona.</span><span class="sxs-lookup"><span data-stu-id="2a5dd-129">IP flow verify requires that hello VM resource is allocated.</span></span>

<span data-ttu-id="2a5dd-130">Jak widać na powitania po obrazu, ruch wychodzący protokołu HTTPS hello jest dozwolone.</span><span class="sxs-lookup"><span data-stu-id="2a5dd-130">As you can see from hello following image, hello outbound HTTPS traffic was allowed.</span></span>

![Przepływ IP Sprawdź — omówienie][1]

<span data-ttu-id="2a5dd-132">Jak pokazano w powitania po obrazu, ruch zostanie zmieniona tooinbound i hello ruchu przychodzącego too123 zmienić port.</span><span class="sxs-lookup"><span data-stu-id="2a5dd-132">As seen in hello following image, traffic is changed tooinbound and hello inbound port changed too123.</span></span> <span data-ttu-id="2a5dd-133">Teraz odmówiono ruchu, wiadomości powitania "Odmowa dostępu" jest dostarczany wraz z hello reguły zabezpieczeń sieci grupy i zabezpieczeń które Odmów hello ruchu.</span><span class="sxs-lookup"><span data-stu-id="2a5dd-133">Traffic is now denied, hello message "Access denied" is provided along with hello network security group and security rule that deny hello traffic.</span></span>

![wyniki przepływu IP][2]

## <a name="next-steps"></a><span data-ttu-id="2a5dd-135">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="2a5dd-135">Next steps</span></span>

<span data-ttu-id="2a5dd-136">Jeśli ruch jest blokowane i nie należy, zobacz [Zarządzaj grupami zabezpieczeń sieci](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack hello reguły zabezpieczeń sieciowych grupy i zabezpieczeń, które są zdefiniowane w dół.</span><span class="sxs-lookup"><span data-stu-id="2a5dd-136">If traffic is being blocked and it should not be, see [Manage Network Security Groups](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack down hello network security group and security rules that are defined.</span></span>

[1]: ./media/network-watcher-check-ip-flow-verify-portal/figure1.png
[2]: ./media/network-watcher-check-ip-flow-verify-portal/figure2.png













