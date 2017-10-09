---
title: "aaaCreate używającego zestawu skalowania maszyn wirtualnych hello portalu Azure | Dokumentacja firmy Microsoft"
description: "Wdrażanie zestawów skalowania za pomocą portalu Azure."
keywords: zestawy skalowania maszyny wirtualnej
services: virtual-machine-scale-sets
documentationcenter: 
author: gatneil
manager: madhana
editor: tysonn
tags: azure-resource-manager
ms.assetid: 9c1583f0-bcc7-4b51-9d64-84da76de1fda
ms.service: virtual-machine-scale-sets
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm
ms.devlang: na
ms.topic: article
ms.date: 05/01/2017
ms.author: negat
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 23c88f4b1ba99994a38f8886f60735da74e5c17e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-virtual-machine-scale-set-with-hello-azure-portal"></a>Jak toocreate w zestawie skalowania maszyn wirtualnych z hello portalu Azure
Ten samouczek pokazuje, jak łatwo jest toocreate zestawu skalowania maszyn wirtualnych w ciągu kilku minut za pomocą hello portalu Azure. Jeśli nie masz subskrypcji platformy Azure, przed rozpoczęciem utwórz [bezpłatne konto](https://azure.microsoft.com/free/).

## <a name="choose-hello-vm-image-from-hello-marketplace"></a>Wybierz obraz maszyny Wirtualnej hello hello w witrynie Marketplace
Witaj portalu możesz z łatwością wdrożyć skali ustawiony za pomocą CentOS, Red Hat Enterprise Linux, CoreOS, otwórz Suse, SUSE Linux Enterprise Server, Debian, Ubuntu Server lub obrazów systemu Windows Server.

Przejdź najpierw toohello [portalu Azure](https://portal.azure.com) w przeglądarce sieci web. Kliknij przycisk `New`, wyszukaj `scale set`, a następnie wybierz hello `Virtual machine scale set` wpis:

![ScaleSetPortalOverview](./media/virtual-machine-scale-sets-portal-create/ScaleSetPortalOverview.PNG)

## <a name="create-hello-scale-set"></a>Utwórz zestaw skali hello
Teraz można użyć ustawień domyślnych hello i szybko utworzyć hello zestaw skali.

* Na powitania `Basics` bloku, wprowadź nazwę dla zestawu skalowania hello. Ta nazwa będzie hello podstawowej z hello FQDN modułu równoważenia obciążenia hello przed hello zestaw skali, dlatego upewnij się, nazwa hello jest unikatowa na wszystkich Azure.
* Wybierz żądaną system operacyjny wpisz, wprowadź odpowiednie nazwy użytkownika i wybierz typ uwierzytelniania, które są preferowane. Jeśli wybierzesz hasło musi być co najmniej 12 znaków i spełniają trzy poza hello cztery następujące wymagania dotyczące złożoności: mała litera, Wielka litera, cyfra i znak specjalny. Więcej informacji na temat [wymagań dotyczących nazwy użytkownika i hasła](../virtual-machines/windows/faq.md#what-are-the-username-requirements-when-creating-a-vm). Jeśli wybierzesz `SSH public key`, jest tooonly się Wklej klucz publiczny nie klucz prywatny:

![ScaleSetPortalBasics](./media/virtual-machine-scale-sets-portal-create/ScaleSetPortalBasics.PNG)

* Wybierz, czy będzie jak zestawu skalowania hello toolimit tooa umieszczania jednej grupy lub czy powinny obejmować wiele grup umieszczania. Stosowanie zestawu skali hello toospan umieszczania grupy pozwala na skali ustawia ponad 100 maszyn wirtualnych w charakterze (up too1, 000) z pewnymi ograniczeniami. Aby uzyskać więcej informacji, zobacz [tej dokumentacji](./virtual-machine-scale-sets-placement-groups.md).
* Wprowadź nazwę grupy żądanego zasobu oraz lokalizacja, a następnie kliknij przycisk `OK`.
* Na powitania `Virtual machine scale set service settings` bloku: Wprowadź etykiety nazwa żądanej domeny (Podstawa hello hello nazwy FQDN dla usługi równoważenia obciążenia hello przed zestaw skali hello). Etykieta musi być unikatowa we wszystkich Azure.
* Wybierz obraz dysku odpowiedni system operacyjny, liczba wystąpień i rozmiaru maszyny.
* Wybierz typ żądany dysk: zarządzane lub niezarządzane. Aby uzyskać więcej informacji, zobacz [tej dokumentacji](./virtual-machine-scale-sets-managed-disks.md). Jeśli została wybrana opcja zestaw skali hello toohave span wiele grup umieszczania, ta opcja nie będą dostępne, ponieważ dysków zarządzanych jest wymagany dla zestawów toospan umieszczania grupach.
* Włącz lub wyłącz skalowania automatycznego i skonfigurować włączenie:

![ScaleSetPortalService](./media/virtual-machine-scale-sets-portal-create/ScaleSetPortalService.PNG)

* Na powitania `Summary` bloku, po zakończeniu weryfikacji kliknij `OK` zestawu toostart hello skalowania wdrożenia.


## <a name="connect-tooa-vm-in-hello-scale-set"></a>Połącz tooa maszyny Wirtualnej w zestawie skalowania hello
W przypadku wybrania toolimit Twojego skali Ustaw tooa umieszczania jednej grupy, a następnie zestaw skali hello jest wdrażany z połączenia łatwe ustawianie skalowania toohello toolet skonfigurowanych reguł NAT (Jeśli nie, maszyn wirtualnych toohello tooconnect w skali hello jest ustawiona, zazwyczaj należy toocreate jumpbox w hello tej samej sieci wirtualnej jako zestaw skali hello). toosee, przejdź toohello `Inbound NAT Rules` kartę hello modułu równoważenia obciążenia dla zestawu skalowania hello:

![ScaleSetPortalNatRules](./media/virtual-machine-scale-sets-portal-create/ScaleSetPortalNatRules.PNG)

Możesz połączyć maszyny Wirtualnej w skali hello ustawić przy użyciu tych reguł NAT tooeach. Na przykład dla zestawu skalowania systemu Windows, jeśli brak reguły NAT na przychodzący port 50000, możesz można połączyć maszyny toothat za pomocą protokołu RDP na `<load-balancer-ip-address>:50000`. Dla zestawu skalowania Linux, można połączyć za pomocą polecenia hello `ssh -p 50000 <username>@<load-balancer-ip-address>`.

## <a name="next-steps"></a>Następne kroki
Dokumentację dotyczącą sposobu skalowania toodeploy ustawia z hello interfejsu wiersza polecenia, zobacz [tej dokumentacji](virtual-machine-scale-sets-cli-quick-create.md).

Dokumentację dotyczącą sposobu skalowania toodeploy ustawia z programu PowerShell, zobacz [tej dokumentacji](virtual-machine-scale-sets-windows-create.md).

Dokumentację dotyczącą sposobu skalowania toodeploy ustawia z programu Visual Studio, zobacz [tej dokumentacji](virtual-machine-scale-sets-vs-create.md).

Dokumentacja ogólna, zapoznaj się z hello [strony Przegląd dokumentacji dla zestawów skalowania](virtual-machine-scale-sets-overview.md).

Aby uzyskać ogólne informacje, zapoznaj się z hello [strony głównej docelowej dla zestawów skalowania](https://azure.microsoft.com/services/virtual-machine-scale-sets/).

