---
title: "aaaSecure a klastra z systemem Windows przy użyciu zabezpieczeń systemu Windows | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooconfigure węzła do węzła i węzeł klient zabezpieczeń w autonomicznym klastra z systemem w systemie Windows przy użyciu zabezpieczeń systemu Windows."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: ce3bf686-ffc4-452f-b15a-3c812aa9e672
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/24/2017
ms.author: dekapur
ms.openlocfilehash: 44f3011eb630357f342052a48d6c852b17dccec4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="secure-a-standalone-cluster-on-windows-by-using-windows-security"></a>Zabezpieczanie klastra autonomicznego w systemie Windows przy użyciu zabezpieczeń systemu Windows
tooprevent nieautoryzowany klastra usługi sieć szkieletowa tooa dostępu, należy zabezpieczyć hello klastra. Bezpieczeństwa jest szczególnie ważne, uruchomienie klastra hello obciążeń produkcyjnych. W tym artykule opisano sposób tooconfigure węzła do węzła i węzeł klient zabezpieczeń przy użyciu zabezpieczeń systemu Windows w hello *pliku ClusterConfig.JSON* pliku.  proces Hello odpowiada toohello skonfigurować zabezpieczenia krok [tworzenia autonomicznych klastra z systemem Windows](service-fabric-cluster-creation-for-windows-server.md). Aby uzyskać więcej informacji o używaniu sieci szkieletowej usług zabezpieczeń systemu Windows, temacie [klastra scenariusze zabezpieczeń](service-fabric-cluster-security.md).

> [!NOTE]
> Należy zastanów wybór hello zabezpieczeń węzła do węzła, ponieważ nie istnieje żadne Uaktualnianie klastra z jednym tooanother wybór zabezpieczeń. Wybór zabezpieczeń hello toochange, masz toorebuild hello pełne klastra.
>
>

## <a name="configure-windows-security-using-gmsa"></a>Konfigurowanie zabezpieczeń systemu Windows przy użyciu usługi zarządzane przez grupę  
przykład Witaj *ClusterConfig.gMSA.Windows.MultiMachine.JSON* pliku konfiguracji są pobierane z hello [Microsoft.Azure.ServiceFabric.WindowsServer.<version>. ZIP](http://go.microsoft.com/fwlink/?LinkId=730690) pakiet klastra autonomiczny zawiera szablon do konfigurowania systemu Windows zabezpieczeń za pomocą [konta usług zarządzanych grupy (gMSA)](https://technet.microsoft.com/library/hh831782.aspx):  

```  
"security": {  
            "WindowsIdentities": {  
                "ClustergMSAIdentity": "accountname@fqdn"  
                "ClusterSPN": "fqdn"  
                "ClientIdentities": [  
                    {  
                        "Identity": "domain\\username",  
                        "IsAdmin": true  
                    }  
                ]  
            }  
        }  
```  
  
| **Ustawienie konfiguracji** | **Opis** |  
| --- | --- |  
| WindowsIdentities |Zawiera hello tożsamości klastra i klienta. |  
| ClustergMSAIdentity |Konfiguruje zabezpieczeń węzła do węzła. Konto usługi zarządzane przez grupę. |  
| ClusterSPN |Pełni kwalifikowaną nazwę SPN konta gMSA|  
| ClientIdentities |Konfiguruje zabezpieczeń węzeł klienta. Tablica konta użytkownika klienta. |  
| Tożsamość |powitania klienta tożsamości, użytkownika domeny. |  
| IsAdmin |Wartość TRUE oznacza hello domeny, które użytkownik ma uprawnienia dostępu administratora klienta, wartość false dla dostępu klientów użytkownika. |  
  
[Węzeł toonode zabezpieczeń](service-fabric-cluster-security.md#node-to-node-security) skonfigurowano ustawienie **ClustergMSAIdentity** gdy sieć szkieletowa usług musi toorun mocy przez grupę. W kolejności toobuild relacje zaufania między węzłami ich należy pamiętać o sobie nawzajem. Można to zrobić na dwa sposoby: można określić konta usługi zarządzanego grupy obejmującą wszystkie węzły w klastrze hello hello lub hello domeny grupy na komputerze, który zawiera wszystkie węzły w klastrze hello. Zdecydowanie zaleca się używanie hello [konta usług zarządzanych grupy (gMSA)](https://technet.microsoft.com/library/hh831782.aspx) podejście, szczególnie w przypadku dużych klastrów (więcej niż 10 węzłów) lub klastrów, które są prawdopodobnie toogrow lub zmniejszyć.  
To rozwiązanie nie wymaga hello tworzenia grupy domeny, dla której administratorzy klastra przyznano tooadd prawa dostępu i Usuń członków. Te konta są również przydatne w przypadku automatyczne zarządzanie hasłami. Aby uzyskać więcej informacji, zobacz [wprowadzenie do kont usług zarządzanych grupy](http://technet.microsoft.com/library/jj128431.aspx).  
 
[Klient toonode zabezpieczeń](service-fabric-cluster-security.md#client-to-node-security) jest konfigurowana przy użyciu **ClientIdentities**. W kolejności tooestablish relacji zaufania między klienta i hello klastra należy skonfigurować tooknow klastra hello które tożsamości klienta, które on zaufany. Można to zrobić na dwa sposoby: Określ hello domeny grupy użytkowników, którzy się połączyć lub określ hello użytkownicy węzeł domeny, które mogą nawiązywać połączenia. Sieć szkieletowa usług obsługuje dwa typy kontroli różny dostęp dla klientów, które są połączone tooa klastra sieci szkieletowej usług: administratora i użytkownika. Kontrola dostępu umożliwia określenie hello dla hello typy toolimit administratora klastra toocertain dostępu do operacji klastra dla różnych grup użytkowników, co klaster hello bardziej bezpieczne.  Administratorzy mają pełny dostęp toomanagement możliwości (w tym możliwości odczytu/zapisu). Użytkownicy mają domyślnie tylko możliwości toomanagement dostęp do odczytu (na przykład możliwość wykonywania kwerend), a hello możliwości tooresolve aplikacji i usług. Aby uzyskać więcej informacji dotyczących kontroli dostępu, zobacz [kontrola dostępu oparta na rolach dla klientów usługi sieć szkieletowa](service-fabric-cluster-security-roles.md).  
 
Witaj następujący przykład **zabezpieczeń** sekcji konfiguruje zabezpieczenia systemu Windows przy użyciu usługi zarządzane przez grupę i określa, że hello maszyn w *ServiceFabric.clusterA.contoso.com* gMSA są częścią klastra hello oraz że *CONTOSO\usera* ma dostęp klient administratora:  
  
```  
"security": {  
    "WindowsIdentities": {  
        "ClustergMSAIdentity" : "ServiceFabric.clusterA.contoso.com",  
        "ClusterSPN" : "clusterA.contoso.com",  
        "ClientIdentities": [{  
            "Identity": "CONTOSO\\usera",  
            "IsAdmin": true  
        }]  
    }  
}  
```  
  
## <a name="configure-windows-security-using-a-machine-group"></a>Konfigurowanie zabezpieczeń systemu Windows przy użyciu grupy na komputerze  
przykład Witaj *ClusterConfig.Windows.MultiMachine.JSON* pliku konfiguracji są pobierane z hello [Microsoft.Azure.ServiceFabric.WindowsServer.<version>. ZIP](http://go.microsoft.com/fwlink/?LinkId=730690) pakiet klastra autonomiczny zawiera szablon do konfigurowania zabezpieczeń systemu Windows.  Zabezpieczenia systemu Windows jest skonfigurowany w hello **właściwości** sekcji: 

```
"security": {
            "ClusterCredentialType": "Windows",
            "ServerCredentialType": "Windows",
            "WindowsIdentities": {
                "ClusterIdentity" : "[domain\machinegroup]",
                "ClientIdentities": [{
                    "Identity": "[domain\username]",
                    "IsAdmin": true
                }]
            }
        }
```

| **Ustawienie konfiguracji** | **Opis** |
| --- | --- |
| ClusterCredentialType |**ClusterCredentialType** ustawiono zbyt*Windows* Jeśli ClusterIdentity określa nazwa grupy komputera usługi Active Directory. |  
| ServerCredentialType |Ustaw zbyt*Windows* tooenable zabezpieczenia systemu Windows dla klientów.<br /><br />Oznacza to, że klienci hello hello klastra i hello samego klastra są uruchomione w ramach domeny usługi Active Directory. |  
| WindowsIdentities |Zawiera hello tożsamości klastra i klienta. |  
| ClusterIdentity |Użyj nazwy grupy komputera, domain\machinegroup, tooconfigure zabezpieczeń węzła do węzła. |  
| ClientIdentities |Konfiguruje zabezpieczeń węzeł klienta. Tablica konta użytkownika klienta. |  
| Tożsamość |Dodaj hello domeny użytkownika, domena azwa_użytkownika powitania klienta tożsamości. |  
| IsAdmin |Toospecify tootrue zestawu, który hello użytkownika domeny ma dostęp administratora klienta lub false dla dostępu klientów użytkownika. |  

[Węzeł zabezpieczenia toonode](service-fabric-cluster-security.md#node-to-node-security) jest konfigurowana przy użyciu ustawienia **ClusterIdentity** Jeśli chcesz toouse grupy na komputerze w ramach domeny usługi Active Directory. Aby uzyskać więcej informacji, zobacz [Utwórz grupę maszyny w usłudze Active Directory](https://msdn.microsoft.com/library/aa545347(v=cs.70).aspx).

[Węzeł Klient zabezpieczeń](service-fabric-cluster-security.md#client-to-node-security) jest konfigurowana przy użyciu **ClientIdentities**. tooestablish zaufania między klastrem klienta i hello, musisz skonfigurować hello klastra tooknow powitania klienta tożsamości, które hello klastra można ufać. Można ustanowić relacji zaufania na dwa sposoby:

- Określ hello domeny grupy użytkowników, które mogą nawiązywać połączenia.
- Określ hello domeny węzła Użytkownicy mogą łączyć.

Sieć szkieletowa usług obsługuje dwa typy kontroli różny dostęp dla klientów, które są połączone tooa klastra sieci szkieletowej usług: administratora i użytkownika. Kontrola dostępu umożliwia hello klastra administrator toolimit toocertain typy dostępu operacji klastra dla różnych grup użytkowników, co czyni klastra hello bardziej bezpieczne.  Administratorzy mają pełny dostęp toomanagement możliwości (w tym możliwości odczytu/zapisu). Użytkownicy mają domyślnie tylko możliwości toomanagement dostęp do odczytu (na przykład możliwość wykonywania kwerend), a hello możliwości tooresolve aplikacji i usług.  

Witaj następujący przykład **zabezpieczeń** konfiguruje zabezpieczenia systemu Windows, określa, że hello maszyn w sekcji *ServiceFabric/clusterA.contoso.com* są częścią klastra hello i określa, że  *CONTOSO\usera* ma dostęp klient administratora:

```
"security": {
    "ClusterCredentialType": "Windows",
    "ServerCredentialType": "Windows",
    "WindowsIdentities": {
        "ClusterIdentity" : "ServiceFabric/clusterA.contoso.com",
        "ClientIdentities": [{
            "Identity": "CONTOSO\\usera",
            "IsAdmin": true
        }]
    }
},
```

> [!NOTE]
> Sieć szkieletowa usług nie powinny zostać wdrożone na kontrolerze domeny. Upewnij się, że pliku ClusterConfig.json nie zawierają hello adres IP kontrolera domeny hello, korzystając z grupy na komputerze lub konta grupy usługi zarządzanej (gMSA).
>
>

## <a name="next-steps"></a>Następne kroki
Po skonfigurowaniu zabezpieczeń systemu Windows w hello *pliku ClusterConfig.JSON* plików, wznowić hello procesu tworzenia klastra w [tworzenia autonomicznych klastra z systemem Windows](service-fabric-cluster-creation-for-windows-server.md).

Aby uzyskać więcej informacji na temat sposobu węzeł węzeł zabezpieczeń, węzeł klient zabezpieczeń i kontroli dostępu opartej na rolach, zobacz [klastra scenariusze zabezpieczeń](service-fabric-cluster-security.md).

Zobacz [klastra bezpiecznego połączenia tooa](service-fabric-connect-to-secure-cluster.md) przykłady połączenie przy użyciu programu PowerShell lub klienta fabricclient z rolą.
