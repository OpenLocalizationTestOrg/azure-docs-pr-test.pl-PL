---
title: tooa aaaConnect maszyny wirtualnej programu SQL Server na platformie Azure (klasyczne) | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak tooconnect tooSQL Server uruchomiony na maszynie wirtualnej na platformie Azure. W tym temacie używa hello klasycznego modelu wdrażania. scenariusze Hello różnią się w zależności od konfiguracji sieci hello i lokalizację hello powitania klienta."
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
tags: azure-service-management
ms.assetid: 416948af-454f-4cfe-8fd2-7cf971cbd3e9
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 01/31/2017
ms.author: jroth
experimental_id: d51f3cc6-753b-4e
ms.openlocfilehash: 4fff3936ad0bcfd3a56855a8436991e19b92522b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooa-sql-server-virtual-machine-on-azure-classic-deployment"></a>Połącz tooa maszyny wirtualnej programu SQL Server na platformie Azure (wdrożenia klasyczne)
> [!div class="op_single_selector"]
> * [Resource Manager](../sql/virtual-machines-windows-sql-connect.md)
> * [Wdrożenie klasyczne](../classic/sql-connect.md)
> 
> 

## <a name="overview"></a>Omówienie
W tym temacie opisano, jak wystąpienie tooyour tooconnect programu SQL Server uruchomiony na maszynie wirtualnej platformy Azure. Obejmuje on niektóre [scenariusze ogólne łączności](#connection-scenarios) , a następnie oferuje [szczegółowe kroki związane z konfigurowaniem łączności z serwerem SQL w maszynie Wirtualnej platformy Azure](#steps-for-configuring-sql-server-connectivity-in-an-azure-vm).

> [!IMPORTANT] 
> Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [Resource Manager i Model Klasyczny](../../../azure-resource-manager/resource-manager-deployment-model.md). W tym artykule omówiono przy użyciu klasycznego modelu wdrożenia hello. Firma Microsoft zaleca, aby większości nowych wdrożeń korzystać hello modelu Resource Manager. Jeśli używasz Menedżera zasobów maszyn wirtualnych, zobacz [połączyć tooa maszyny wirtualnej programu SQL Server na platformie Azure przy użyciu usługi Resource Manager](../sql/virtual-machines-windows-sql-connect.md).

## <a name="connection-scenarios"></a>Scenariusze łączenia
sposób powitania klienta łączy tooSQL, który serwer z uruchomioną na maszynie wirtualnej różni się w zależności od lokalizacji hello powitania klienta i konfiguracji sieci/maszyny hello. Te scenariusze obejmują:

* [Połącz tooSQL serwera w hello sama usługa w chmurze](#connect-to-sql-server-in-the-same-cloud-service)
* [Połącz tooSQL serwera na powitania internet](#connect-to-sql-server-over-the-internet)
* [Połącz tooSQL serwera w hello tej samej sieci wirtualnej](#connect-to-sql-server-in-the-same-virtual-network)

> [!NOTE]
> Przed nawiązaniem połączenia z żadnym z tych metod, należy wykonać hello [kroków w tym artykule tooconfigure łączność](#steps-for-configuring-sql-server-connectivity-in-an-azure-vm).
> 
> 

### <a name="connect-toosql-server-in-hello-same-cloud-service"></a>Połącz tooSQL serwera w hello sama usługa w chmurze
Wiele maszyn wirtualnych można tworzyć w hello sama usługa w chmurze. Ta ścieżka wirtualna toounderstand maszyny scenariusza, zobacz [jak tooconnect maszyn wirtualnych za pomocą wirtualnej sieci lub w chmurze usługi](../classic/connect-vms.md#connect-vms-in-a-standalone-cloud-service). Ten scenariusz jest klienta na jednej maszynie wirtualnej próbujący tooconnect tooSQL serwera działający na inną maszynę wirtualną w hello sama usługa w chmurze.

W tym scenariuszu można połączyć za pomocą hello wirtualna **nazwa** (także wyświetlane jako **nazwy komputera** lub **hostname** w portalu hello). Jest to nazwa hello, podać na powitania maszyny Wirtualnej podczas tworzenia. Na przykład, jeśli nazwę maszyny Wirtualnej SQL **mysqlvm**, klient maszyny Wirtualnej w hello można użyć tej samej usługi w chmurze hello po tooconnect ciąg połączenia:

    "Server=mysqlvm;Integrated Security=false;User ID=<login_name>;Password=<your_password>"

### <a name="connect-toosql-server-over-hello-internet"></a>Połącz tooSQL serwera na powitania Internet
Aparat bazy danych programu SQL Server tooyour tooconnect z hello Internet, należy utworzyć punktu końcowego maszyny wirtualnej, TCP komunikacji przychodzącej. Ten krok konfiguracji platformy Azure Określa, że przychodzący port TCP, port ruchu tooa TCP jest dostępny toohello maszyny wirtualnej.

tooconnect za pośrednictwem hello internet, należy użyć hello wirtualna DNS nazwy i hello wirtualna punktu końcowego numer portu (skonfigurowanej w dalszej części tego artykułu). toohello Azure portalu i wybierz pozycję Przejdź hello toofind nazwy DNS **maszyn wirtualnych (klasyczne)**. Następnie wybierz maszynę wirtualną. Witaj **nazwy DNS** jest wyświetlany w obszarze hello **omówienie** sekcji.

Rozważmy na przykład klasyczne maszyny wirtualnej o nazwie **mysqlvm** o nazwie DNS **mysqlvm7777.cloudapp.net** i punkt końcowy maszyny Wirtualnej **57500**. Zakładając, że poprawnie skonfigurowane połączenie, hello następujące parametry połączenia może być używane tooaccess maszyny wirtualnej hello z dowolnego miejsca na hello internet:

    "Server=mycloudservice.cloudapp.net,57500;Integrated Security=false;User ID=<login_name>;Password=<your_password>"

Mimo że to umożliwia łączność klientów za pośrednictwem Internetu Witaj, nie oznacza to, że każdy użytkownik może połączyć tooyour programu SQL Server. Poza klienci mają toohello prawidłową nazwę użytkownika i hasło. Aby dodatkowo zwiększyć bezpieczeństwo nie używaj hello dobrze znanego portu 1433 dla punktu końcowego hello publicznego maszyny wirtualnej. A jeśli to możliwe, należy rozważyć dodanie listy ACL na punkt końcowy toorestrict ruchu toohello tylko klientów można zezwolić. Aby uzyskać instrukcje dotyczące przy użyciu list kontroli dostępu z punktami końcowymi, zobacz [Zarządzaj hello listy ACL punktu końcowego](../classic/setup-endpoints.md#manage-the-acl-on-an-endpoint).

> [!NOTE]
> Ważne jest, że, korzystając z tej techniki toocommunicate z programem SQL Server, wszystkie dane wychodzące z hello centrum danych Azure toonote był toonormal podmiotu [ceny na transfer danych wychodzących](https://azure.microsoft.com/pricing/details/data-transfers/).
> 
> 

### <a name="connect-toosql-server-in-hello-same-virtual-network"></a>Połącz tooSQL serwera w hello tej samej sieci wirtualnej
[Sieć wirtualna](../../../virtual-network/virtual-networks-overview.md) umożliwia dodatkowe scenariusze. Możesz połączyć maszyny wirtualne w tej samej sieci wirtualnej, nawet jeśli te maszyny wirtualne istnieją w innej chmurze usługi hello. I [sieci VPN typu lokacja lokacja](../../../vpn-gateway/vpn-gateway-site-to-site-create.md), możesz utworzyć to architektura hybrydowego łączy maszyn wirtualnych z lokalnymi sieciami i maszyn.

Sieci wirtualne umożliwia również należy toojoin domenę tooa maszynach wirtualnych platformy Azure. Jest to hello tylko sposób toouse uwierzytelniania systemu Windows tooSQL serwera. Witaj inne połączenie scenariusze wymagają uwierzytelniania SQL z nazwy użytkownika i hasła.

Jeśli zamierzasz tooconfigure środowisku domeny i uwierzytelniania systemu Windows, nie trzeba toouse hello kroków w tym artykule tooconfigure hello publiczny punkt końcowy lub hello uwierzytelnianie SQL i logowania. W tym scenariuszu można połączyć, określając nazwę maszyny Wirtualnej programu SQL Server hello w parametrach połączenia hello tooyour wystąpienia programu SQL Server. Poniższy przykład Hello założono, że również skonfigurowano uwierzytelnianie systemu Windows i użytkownik hello udzielono wystąpienia programu SQL Server toohello dostępu.

    "Server=mysqlvm;Integrated Security=true"

## <a name="steps-for-configuring-sql-server-connectivity-in-an-azure-vm"></a>Kroki konfigurowania połączenia programu SQL Server w maszynie Wirtualnej platformy Azure
Witaj następujące kroki pokazują, jak wystąpienie programu SQL Server toohello tooconnect za pośrednictwem hello Internetem przy użyciu programu SQL Server Management Studio (SSMS). Jednak hello te same czynności mają zastosowanie toomaking dostępne dla aplikacji, a także uruchomiona lokalnie i na platformie Azure maszyny wirtualnej programu SQL Server.

Zanim można łączyć z toohello wystąpienia programu SQL Server z inną maszynę Wirtualną lub hello internet, należy wykonać następujące zadania opisane w kolejnych sekcjach hello hello:

* [Tworzenie punktu końcowego TCP hello maszyny wirtualnej](#create-a-tcp-endpoint-for-the-virtual-machine)
* [Otwartych portów TCP w Zaporze systemu Windows hello](#open-tcp-ports-in-the-windows-firewall-for-the-default-instance-of-the-database-engine)
* [Skonfiguruj toolisten programu SQL Server na powitania protokołu TCP](#configure-sql-server-to-listen-on-the-tcp-protocol)
* [Konfigurowanie programu SQL Server na potrzeby uwierzytelniania w trybie mieszanym](#configure-sql-server-for-mixed-mode-authentication)
* [Tworzenie identyfikatorów logowania uwierzytelniania programu SQL Server](#create-sql-server-authentication-logins)
* [Określić nazwy DNS hello hello maszyny wirtualnej](#determine-the-dns-name-of-the-virtual-machine)
* [Połącz toohello aparatu bazy danych z innego komputera](#connect-to-the-database-engine-from-another-computer)

Ścieżka połączenia Hello jest podsumowane według powitania po diagramu:

![Łączenie maszyny wirtualnej programu SQL Server tooa](../../../../includes/media/virtual-machines-sql-server-connection-steps/SQLServerinVMConnectionMap.png)

[!INCLUDE [Connect tooSQL Server in a VM Classic TCP Endpoint](../../../../includes/virtual-machines-sql-server-connection-steps-classic-tcp-endpoint.md)]

[!INCLUDE [Connect tooSQL Server in a VM](../../../../includes/virtual-machines-sql-server-connection-steps.md)]

[!INCLUDE [Connect tooSQL Server in a VM Classic Steps](../../../../includes/virtual-machines-sql-server-connection-steps-classic.md)]

## <a name="next-steps"></a>Następne kroki
Jeśli planujesz również toouse zawsze włączonych grup dostępności, wysokiej dostępności i odzyskiwania po awarii, należy rozważyć wdrożenie odbiornik. Klienci bazy danych łączyć odbiornika toohello zamiast bezpośrednio tooone hello wystąpień programu SQL Server. Witaj odbiornika trasy klientów toohello repliki podstawowej grupy dostępności hello. Aby uzyskać więcej informacji, zobacz [skonfigurować odbiornik ILB dla zawsze włączonych grup dostępności na platformie Azure](../classic/ps-sql-int-listener.md).

Jest ważne tooreview wszystkie hello zabezpieczeń najlepsze rozwiązania dotyczące programu SQL Server uruchomionego na maszynie wirtualnej platformy Azure. Aby uzyskać więcej informacji, zobacz [Zagadnienia dotyczące zabezpieczeń programu SQL Server w usłudze Azure Virtual Machines](../sql/virtual-machines-windows-sql-security.md).

[Eksploruj hello ścieżka szkoleniowa dotycząca](https://azure.microsoft.com/documentation/learning-paths/sql-azure-vm/) dla programu SQL Server na maszynach wirtualnych Azure. 

Dla innych tematach dotyczących toorunning programu SQL Server na maszynach wirtualnych Azure, zobacz [programu SQL Server na maszynach wirtualnych Azure](../sql/virtual-machines-windows-sql-server-iaas-overview.md).

