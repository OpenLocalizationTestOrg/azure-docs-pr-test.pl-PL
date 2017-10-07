---
title: tooa aaaConnect programu SQL Server Virtual Machine (Resource Manager) | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak tooconnect tooSQL Server uruchomiony na maszynie wirtualnej na platformie Azure. W tym temacie używa hello klasycznego modelu wdrażania. scenariusze Hello różnią się w zależności od konfiguracji sieci hello i lokalizację hello powitania klienta."
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
tags: azure-resource-manager
ms.assetid: aa5bf144-37a3-4781-892d-e0e300913d03
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 08/14/2017
ms.author: jroth
ms.openlocfilehash: 7b127c14c37b9a72c19ed17f8b1dad61c7bc2d38
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooa-sql-server-virtual-machine-on-azure-resource-manager"></a>Połącz tooa maszyny wirtualnej programu SQL Server na platformie Azure (Resource Manager)
> [!div class="op_single_selector"]
> * [Resource Manager](virtual-machines-windows-sql-connect.md)
> * [Wdrożenie klasyczne](../classic/sql-connect.md)
> 
> 

## <a name="overview"></a>Omówienie

W tym temacie opisano, jak wystąpienie tooyour tooconnect programu SQL Server uruchomiony na maszynie wirtualnej platformy Azure. Obejmuje on niektóre [scenariusze ogólne łączności](#connection-scenarios) , a następnie oferuje [szczegółowe kroki związane z konfigurowaniem łączności z serwerem SQL w maszynie Wirtualnej platformy Azure](#steps-for-manually-configuring-sql-server-connectivity-in-an-azure-vm).

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

Jeśli trzeba będzie raczej pełny przewodnik inicjowania obsługi administracyjnej i łączność, zobacz [inicjowania obsługi maszyny wirtualnej programu SQL Server na platformie Azure](virtual-machines-windows-portal-sql-server-provision.md).

## <a name="connection-scenarios"></a>Scenariusze łączenia

sposób powitania klienta łączy tooSQL, który serwer z uruchomioną na maszynie wirtualnej różni się w zależności od lokalizacji hello powitania klienta i konfiguracji sieci hello.

Jeśli dostarczasz maszyna wirtualna serwera SQL w hello portalu Azure, masz możliwość określenia typu hello hello **łączność z serwerem SQL**.

![Publiczny opcji łączności SQL podczas inicjowania obsługi](./media/virtual-machines-windows-sql-connect/sql-vm-portal-connectivity.png)

Dostępne opcje dla połączenia:

| Opcja | Opis |
|---|---|
| **Publiczna** | Połącz tooSQL serwera na powitania internet |
| **Prywatne** | Połącz tooSQL serwera w hello tej samej sieci wirtualnej |
| **Lokalne** | Połącz tooSQL serwera lokalnie na powitania tej samej maszyny wirtualnej | 

Witaj poniższe sekcje zawierają opis hello **publicznego** i **prywatnej** szczegółowo opcje.

## <a name="connect-toosql-server-over-hello-internet"></a>Połącz tooSQL serwera na powitania Internet

Aparat bazy danych programu SQL Server tooyour tooconnect z hello Internet, wybierz opcję **publicznego** dla hello **łączność z serwerem SQL** typu w portalu hello podczas inicjowania obsługi. Hello portal automatycznie hello następujące kroki:

* Włącza hello protokołu TCP/IP dla programu SQL Server.
* Umożliwia skonfigurowanie zapory hello tooopen reguły port TCP programu SQL Server (domyślnie 1433).
* Umożliwia uwierzytelnianie programu SQL Server wymagane dla dostępu publicznego.
* Konfiguruje hello sieciowej grupy zabezpieczeń na powitania ruch TCP tooall maszyn wirtualnych na powitania port programu SQL Server.

> [!IMPORTANT]
> Hello obrazy maszyny wirtualnej dla programu SQL Server Developer hello i wersji Express nie automatycznie włącza protokół hello TCP/IP. Dla deweloperów i ekspresowej wersji, należy użyć programu SQL Server Configuration Manager za[ręcznie włączyć protokół hello TCP/IP](#manualtcp) po utworzeniu hello maszyny Wirtualnej.

Dowolny klient z dostępem do Internetu mogą łączyć się z toohello wystąpienia programu SQL Server, określając hello publicznego adresu IP maszyny wirtualnej hello lub jakakolwiek Etykieta DNS przypisany adres IP toothat. Jeśli hello port programu SQL Server jest port 1433, nie ma potrzeby toospecify go w parametrach połączenia hello. Witaj następujące parametry połączenia tooa maszyny Wirtualnej SQL łączy się z usługą etykietę DNS z `sqlvmlabel.eastus.cloudapp.azure.com` przy użyciu uwierzytelniania programu SQL (można także użyć hello publiczny adres IP).

```
Server=sqlvmlabel.eastus.cloudapp.azure.com;Integrated Security=false;User ID=<login_name>;Password=<your_password>
```

Mimo że to umożliwia łączność klientów za pośrednictwem Internetu Witaj, nie oznacza to, że każdy użytkownik może połączyć tooyour programu SQL Server. Poza klienci mają toohello prawidłową nazwę użytkownika i hasło. Jednak aby dodatkowo zwiększyć bezpieczeństwo, można uniknąć hello dobrze znanego portu 1433. Na przykład jeśli skonfigurowano toolisten programu SQL Server na porcie 1500 i ustalonych prawidłowego zapory i reguł grup zabezpieczeń sieci, można połączyć przez dodanie nazwy serwera toohello numer portu hello. Witaj poniższy przykład powoduje zmianę hello poprzedniego przez dodanie niestandardowy numer portu, **1500**, toohello nazwa serwera:

```
Server=sqlvmlabel.eastus.cloudapp.azure.com,1500;Integrated Security=false;User ID=<login_name>;Password=<your_password>"
```

> [!NOTE]
> Kwerendy SQL Server na maszynie wirtualnej za pośrednictwem Internetu, wszystkie dane wychodzące hello z hello Azure datacenter jest podmiotu toonormal [ceny na transfer danych wychodzących](https://azure.microsoft.com/pricing/details/data-transfers/).

## <a name="connect-toosql-server-within-a-virtual-network"></a>Połącz tooSQL serwera w sieci wirtualnej

Po wybraniu **prywatnej** dla hello **łączność z serwerem SQL** typu w portalu hello Azure konfiguruje większość ustawień hello identyczne zbyt**publicznego**. Hello jeden różnica polega na tym, czy jest nie sieci zabezpieczeń grupy reguł tooallow poza ruchu na powitania port serwera SQL (domyślnie 1433).

> [!IMPORTANT]
> Hello obrazy maszyny wirtualnej dla programu SQL Server Developer hello i wersji Express nie automatycznie włącza protokół hello TCP/IP. Dla deweloperów i ekspresowej wersji, należy użyć programu SQL Server Configuration Manager za[ręcznie włączyć protokół hello TCP/IP](#manualtcp) po utworzeniu hello maszyny Wirtualnej.

Prywatne łączności jest często używana w połączeniu z [sieci wirtualnej](../../../virtual-network/virtual-networks-overview.md), co pozwala kilka scenariuszy. Możesz połączyć maszyny wirtualne w tej samej sieci wirtualnej, nawet jeśli te maszyny wirtualne istnieją w różnych grupach zasobów hello. I [sieci VPN typu lokacja lokacja](../../../vpn-gateway/vpn-gateway-site-to-site-create.md), możesz utworzyć to architektura hybrydowego łączy maszyn wirtualnych z lokalnymi sieciami i maszyn.

Sieci wirtualne umożliwiają również toojoin można domenę tooa maszynach wirtualnych platformy Azure. Jest to hello tylko sposób toouse uwierzytelniania systemu Windows tooSQL serwera. Witaj inne połączenie scenariusze wymagają uwierzytelniania SQL z nazwy użytkownika i hasła.

Przy założeniu, że skonfigurowano DNS w sieci wirtualnej, można połączyć, określając nazwę komputera maszyny Wirtualnej programu SQL Server hello w parametrach połączenia hello tooyour wystąpienia programu SQL Server. Poniższy przykład również Hello założono, że również skonfigurowano uwierzytelnianie systemu Windows i użytkownika hello udzielono wystąpienia programu SQL Server toohello dostępu.

```
Server=mysqlvm;Integrated Security=true
```

## <a id="change"></a>Zmień ustawienia połączenia SQL

Ustawienia łączności hello można zmienić dla maszyny wirtualnej programu SQL Server w hello portalu Azure.

1. Hello portalu Azure, wybierz **maszyn wirtualnych**.

2. Wybierz program SQL Server maszyny Wirtualnej.

3. W obszarze **ustawienia**, kliknij przycisk **konfigurację programu SQL Server**.

4. Zmień hello **poziom Połączenie SQL** tooyour wymagane ustawienia. Można opcjonalnie użyć tego obszaru toochange hello port programu SQL Server lub hello ustawienia uwierzytelniania SQL.

   ![Zmień łączność z serwerem SQL](./media/virtual-machines-windows-sql-connect/sql-vm-portal-connectivity-change.png)

5. Poczekaj kilka minut dla hello toocomplete aktualizacji.

   ![Powiadomienie o aktualizacji maszyny Wirtualnej SQL](./media/virtual-machines-windows-sql-connect/sql-vm-updating-notification.png)

## <a id="manualtcp"></a>Włącz protokół TCP/IP dla deweloperów i Express w wersji

Zmieniając ustawienia łączności serwera SQL Azure nie powoduje automatycznego włączenia protokołu hello TCP/IP dla programu SQL Server Developer i wersji Express. Witaj poniżej objaśniono sposób toomanually Włącz protokół TCP/IP, dzięki czemu można łączyć zdalnie za pomocą adresu IP.

Najpierw połącz toohello komputera programu SQL Server przy użyciu pulpitu zdalnego.

> [!INCLUDE [Connect tooSQL Server VM with remote desktop](../../../../includes/virtual-machines-sql-server-remote-desktop-connect.md)]

Następnie Włącz protokół hello TCP/IP z **SQL Server Configuration Manager**.

> [!INCLUDE [Connect tooSQL Server VM with remote desktop](../../../../includes/virtual-machines-sql-server-connection-tcp-protocol.md)]

## <a name="connect-with-ssms"></a>Nawiązywanie połączenia z programem SSMS

Witaj poniższe kroki Pokaż jak toocreate opcjonalne DNS etykietę dla maszyny Wirtualnej platformy Azure i następnie nawiąż połączenie z SQL Server Management Studio (SSMS).

[!INCLUDE [Connect tooSQL Server in a VM Resource Manager](../../../../includes/virtual-machines-sql-server-connection-steps-resource-manager.md)]

## <a name="next-steps"></a>Następne kroki

Zobacz instrukcje inicjowania obsługi administracyjnej toosee wraz z tych kroków łączności, [inicjowania obsługi maszyny wirtualnej programu SQL Server na platformie Azure](virtual-machines-windows-portal-sql-server-provision.md).

Dla innych tematach dotyczących toorunning programu SQL Server na maszynach wirtualnych Azure, zobacz [programu SQL Server na maszynach wirtualnych Azure](virtual-machines-windows-sql-server-iaas-overview.md).
