---
title: "aaaCheck łączność z obserwatora sieciowego Azure - Azure portal | Dokumentacja firmy Microsoft"
description: "Ta strona wyjaśniono, jak łączność toouse skontaktuj się z obserwatora sieciowego przy użyciu hello portalu Azure"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/03/2017
ms.author: gwallace
ms.openlocfilehash: ef6ecccd688f06f70003a5b59771c15bcbe8f3e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="check-connectivity-with-azure-network-watcher-using-hello-azure-portal"></a><span data-ttu-id="91632-103">Sprawdź łączność z obserwatora sieciowego Azure przy użyciu hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="91632-103">Check connectivity with Azure Network Watcher using hello Azure portal</span></span>

> [!div class="op_single_selector"]
> - [<span data-ttu-id="91632-104">Portal</span><span class="sxs-lookup"><span data-stu-id="91632-104">Portal</span></span>](network-watcher-connectivity-portal.md)
> - [<span data-ttu-id="91632-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="91632-105">PowerShell</span></span>](network-watcher-connectivity-powershell.md)
> - [<span data-ttu-id="91632-106">Interfejs wiersza polecenia 2.0</span><span class="sxs-lookup"><span data-stu-id="91632-106">CLI 2.0</span></span>](network-watcher-connectivity-cli.md)
> - [<span data-ttu-id="91632-107">Interfejs API Azure REST</span><span class="sxs-lookup"><span data-stu-id="91632-107">Azure REST API</span></span>](network-watcher-connectivity-rest.md)

<span data-ttu-id="91632-108">Dowiedz się, jak można ustalić toouse łączności tooverify Jeśli bezpośrednie połączenie TCP z tooa maszyny wirtualnej, danego punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="91632-108">Learn how toouse connectivity tooverify if a direct TCP connection from a virtual machine tooa given endpoint can be established.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="91632-109">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="91632-109">Before you begin</span></span>

<span data-ttu-id="91632-110">W tym artykule przyjęto założenie, że masz hello następujące zasoby:</span><span class="sxs-lookup"><span data-stu-id="91632-110">This article assumes you have hello following resources:</span></span>

* <span data-ttu-id="91632-111">Wystąpienia obserwatora sieciowego w regionie hello ma toocheck łączności.</span><span class="sxs-lookup"><span data-stu-id="91632-111">An instance of Network Watcher in hello region you want toocheck connectivity.</span></span>

* <span data-ttu-id="91632-112">Maszyny wirtualne toocheck łączność z.</span><span class="sxs-lookup"><span data-stu-id="91632-112">Virtual machines toocheck connectivity with.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="91632-113">Sprawdź łączność wymaga rozszerzenia maszyny wirtualnej `AzureNetworkWatcherExtension`.</span><span class="sxs-lookup"><span data-stu-id="91632-113">Connectivity check requires a virtual machine extension `AzureNetworkWatcherExtension`.</span></span> <span data-ttu-id="91632-114">Instalowanie hello rozszerzenia na maszynie Wirtualnej systemu Windows można znaleźć [rozszerzenie maszyny wirtualnej Azure sieci obserwatorów agenta dla systemu Windows](../virtual-machines/windows/extensions-nwa.md) i dla maszyny Wirtualnej systemu Linux, odwiedź [rozszerzenie maszyny wirtualnej Azure sieci obserwatorów agenta dla systemu Linux](../virtual-machines/linux/extensions-nwa.md).</span><span class="sxs-lookup"><span data-stu-id="91632-114">For installing hello extension on a Windows VM visit [Azure Network Watcher Agent virtual machine extension for Windows](../virtual-machines/windows/extensions-nwa.md) and for Linux VM visit [Azure Network Watcher Agent virtual machine extension for Linux](../virtual-machines/linux/extensions-nwa.md).</span></span>

## <a name="check-connectivity-tooa-virtual-machine"></a><span data-ttu-id="91632-115">Sprawdź maszyny wirtualnej tooa łączności</span><span class="sxs-lookup"><span data-stu-id="91632-115">Check connectivity tooa virtual machine</span></span>

<span data-ttu-id="91632-116">W tym przykładzie sprawdza łączność tooa docelowej maszyny wirtualnej za pośrednictwem portu 80.</span><span class="sxs-lookup"><span data-stu-id="91632-116">This example checks connectivity tooa destination virtual machine over port 80.</span></span>

<span data-ttu-id="91632-117">Przejdź tooyour obserwatora sieciowego i kliknij **sprawdzenia łączności z serwerem (wersja zapoznawcza)**.</span><span class="sxs-lookup"><span data-stu-id="91632-117">Navigate tooyour Network Watcher and click **Connectivity check (Preview)**.</span></span> <span data-ttu-id="91632-118">Wybierz hello łączności toocheck maszyn wirtualnych z.</span><span class="sxs-lookup"><span data-stu-id="91632-118">Select hello virtual machine toocheck connectivity from.</span></span> <span data-ttu-id="91632-119">W hello **docelowego** wybierz **wybierz maszynę wirtualną** i wybierz hello poprawne maszyny wirtualnej i portu tootest.</span><span class="sxs-lookup"><span data-stu-id="91632-119">In hello **Destination** section choose **Select a virtual machine** and choose hello correct virtual machine and port tootest.</span></span>

<span data-ttu-id="91632-120">Po kliknięciu **Sprawdź**, hello łączności między maszynami wirtualnymi hello na określony port hello są sprawdzane.</span><span class="sxs-lookup"><span data-stu-id="91632-120">Once you click **Check**, hello connectivity between hello virtual machines on hello port specified are checked.</span></span> <span data-ttu-id="91632-121">W przykładzie hello hello docelowej maszyny Wirtualnej jest nieosiągalny, lista przeskoków są wyświetlane.</span><span class="sxs-lookup"><span data-stu-id="91632-121">In hello example, hello destination VM is unreachable, a listing of hops are shown.</span></span>

![Wyniki sprawdzania łączności dla maszyny wirtualnej][1]

## <a name="check-remote-endpoint-connectivity"></a><span data-ttu-id="91632-123">Sprawdź łączność zdalny punkt końcowy</span><span class="sxs-lookup"><span data-stu-id="91632-123">Check remote endpoint connectivity</span></span>

<span data-ttu-id="91632-124">toocheck hello łączności i opóźnienia tooa zdalny punkt końcowy, wybierz hello **ręcznie określ** przycisk radiowy na powitania **docelowego** sekcji należy wprowadzić hello adresu url i hello port i kliknij przycisk **Sprawdź** .</span><span class="sxs-lookup"><span data-stu-id="91632-124">toocheck hello connectivity and latency tooa remote endpoint, choose hello **Specify manually** radio button in hello **Destination** section, input hello url and hello port and click **Check**.</span></span>  <span data-ttu-id="91632-125">Służy to do zdalnego punktów końcowych, takie jak punktów końcowych witryn sieci Web i magazynu.</span><span class="sxs-lookup"><span data-stu-id="91632-125">This is used for remote endpoints like websites and storage endpoints.</span></span>

![Wyniki sprawdzania łączności dla witryny sieci web][2]

## <a name="next-steps"></a><span data-ttu-id="91632-127">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="91632-127">Next steps</span></span>

<span data-ttu-id="91632-128">Dowiedz się, jak przechwytywanie pakietów tooautomate z alertami maszyny wirtualnej, wyświetlając [utworzyć przechwytywania alertów wyzwalanych pakietów](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="91632-128">Learn how tooautomate packet captures with Virtual machine alerts by viewing [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>

<span data-ttu-id="91632-129">Znajdź, jeśli niektórych ruch jest dozwolony w lub z maszyny Wirtualnej, odwiedzając [Sprawdź przepływ Sprawdź IP](network-watcher-check-ip-flow-verify-portal.md)</span><span class="sxs-lookup"><span data-stu-id="91632-129">Find if certain traffic is allowed in or out of your VM by visiting [Check IP flow verify](network-watcher-check-ip-flow-verify-portal.md)</span></span>

[1]: ./media/network-watcher-connectivity-portal/figure1.png
[2]: ./media/network-watcher-connectivity-portal/figure2.png
