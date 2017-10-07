---
title: "aaaViewing i modyfikowanie nazwy hostów | Dokumentacja firmy Microsoft"
description: "Jak tooview i zmiana nazwy hostów maszyn wirtualnych platformy Azure, sieci web i proces roboczy do rozpoznawania nazw"
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
ms.assetid: c668cd8e-4e43-4d05-acc3-db64fa78d828
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/27/2016
ms.author: jdial
ms.openlocfilehash: 17d0dd7911754a94db3f37b924b4687da1c70aca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="viewing-and-modifying-hostnames"></a>Wyświetlanie i modyfikowanie nazwy hostów
tooallow Twojego toobe wystąpień roli odwołuje się nazwa hosta, należy ustawić wartość hello hello nazwy hosta w pliku konfiguracji usługi powitania dla każdej roli. Można to zrobić przez dodanie toohello nazwy hosta hello potrzeby **vmName** atrybutu hello **roli** elementu. Witaj wartość hello **vmName** atrybutu jest używana jako podstawa dla nazwy hosta hello każdego wystąpienia roli. Na przykład jeśli **vmName** jest *sieć Web* istnieją trzy wystąpień tej roli, nazwy hosta hello wystąpień hello będą *webrole0*, *webrole1* , i *webrole2*. Nie trzeba toospecify nazwę hosta dla maszyn wirtualnych w pliku konfiguracyjnym hello, ponieważ hello nazwy hosta dla maszyny wirtualnej jest wypełniana na podstawie nazwy maszyny wirtualnej hello. Aby uzyskać więcej informacji o konfigurowaniu usługi Microsoft Azure, zobacz [schemat konfiguracji usługi Azure (cscfg plików)](https://msdn.microsoft.com/library/azure/ee758710.aspx)

## <a name="viewing-hostnames"></a>Wyświetlanie nazwy hostów
Przy użyciu dowolnej z poniższych narzędzi hello można wyświetlić hello nazwy hostów maszyn wirtualnych i wystąpień roli w usłudze w chmurze.

### <a name="azure-portal"></a>Azure Portal
Można użyć hello [portalu Azure](http://portal.azure.com) nazwy hostów hello tooview dla maszyn wirtualnych na powitania omówienie bloku dla maszyny wirtualnej. Należy pamiętać, że hello blok zawiera wartość **nazwa** i **nazwy hosta**. Chociaż hello początkowo są takie same, zmiana nazwy hosta hello nie spowoduje zmiany nazwy hello hello maszyny wirtualnej lub wystąpienia roli.

Wystąpień roli można również wyświetlać w hello portalu Azure, ale jeśli lista wystąpień hello w usłudze w chmurze, hello nazwy hosta nie jest wyświetlana. Zobaczysz nazwy dla każdego wystąpienia, ale ta nazwa nie reprezentuje hello nazwy hosta.

### <a name="service-configuration-file"></a>Plik konfiguracji usługi
Możesz pobrać hello pliku konfiguracji usługi dla wdrożonej usługi z hello **Konfiguruj** bloku usługi hello w hello portalu Azure. Następnie można wyszukać hello **vmName** atrybutu hello **nazwy roli** nazwy hosta hello toosee elementu. Należy pamiętać, że ta nazwa hosta jest używana jako podstawa dla nazwy hosta hello każdego wystąpienia roli. Na przykład jeśli **vmName** jest *sieć Web* istnieją trzy wystąpień tej roli, nazwy hosta hello wystąpień hello będą *webrole0*, *webrole1* , i *webrole2*.

### <a name="remote-desktop"></a>Pulpit zdalny
Po włączeniu pulpitu zdalnego (system Windows), komunikacji zdalnej programu Windows PowerShell (Windows) lub maszyny wirtualne tooyour połączenia SSH (Linux i Windows) lub wystąpień roli, można wyświetlić nazwy hosta hello z aktywnego połączenia pulpitu zdalnego na różne sposoby:

* W wierszu polecenia hello lub SSH terminal, wpisz nazwę hosta.
* Wpisz polecenie ipconfig/wszystko na powitania polecenia monit (tylko system Windows).
* Nazwa komputera hello widoku w systemie hello ustawienia (tylko system Windows).

### <a name="azure-service-management-rest-api"></a>Usługa Azure Service Management REST API
W kliencie REST wykonaj następujące instrukcje:

1. Upewnij się, że masz klienta toohello tooconnect certyfikatu portalu Azure. tooobtain certyfikat klienta, wykonaj kroki hello przedstawionych w [porady: pobieranie i importowanie ustawień publikowania i informacji o subskrypcji](https://msdn.microsoft.com/library/dn385850.aspx). 
2. Ustaw wpis nagłówka o nazwie x-ms-version o wartości 2013-11-01.
3. Wyślij żądanie w hello następującego formatu: https://management.core.windows.net/\<identyfikator subscrition\>/services/hostedservices/\<nazwa usługi\>? osadzić szczegółów = true
4. Wyszukaj hello **HostName** elementu dla każdego **RoleInstance** elementu.

> [!WARNING]
> Możesz również wyświetlić hello sufiks domeny wewnętrznej dla usługi w chmurze z hello odpowiedzi wywołań REST, sprawdzając hello **InternalDnsSuffix** elementu, lub przez uruchomienie polecenia ipconfig/z wiersza polecenia w sesji pulpitu zdalnego (system Windows) lub uruchomione /etc/resolv.conf cat z terminalu SSH (Linux).
> 
> 

## <a name="modifying-a-hostname"></a>Modyfikowanie nazwy hosta
Można zmodyfikować hello nazwy hosta dla maszyny wirtualnej lub wystąpienia roli, przekazując plik konfiguracji usługi zmodyfikowanych lub zmieniając hello komputera z sesji pulpitu zdalnego.

## <a name="next-steps"></a>Następne kroki
[Rozpoznawanie nazw (domen DNS)](virtual-networks-name-resolution-for-vms-and-role-instances.md)

[Schemat konfiguracji usługi Azure (cscfg)](https://msdn.microsoft.com/library/windowsazure/ee758710.aspx)

[Schemat konfiguracji sieci wirtualnej platformy Azure](http://go.microsoft.com/fwlink/?LinkId=248093)

[Określ ustawienia DNS za pomocą plików konfiguracji sieci](virtual-networks-specifying-a-dns-settings-in-a-virtual-network-configuration-file.md)

