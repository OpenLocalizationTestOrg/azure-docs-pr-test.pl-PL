---
title: "aaaConfigure zabezpieczyć Azure Service Fabric połączenia klastra | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse tooconfigure programu Visual Studio bezpiecznych połączeń, które są obsługiwane przez klaster sieci szkieletowej usług Azure hello."
services: service-fabric
documentationcenter: na
author: cawaMS
manager: paulyuk
editor: tglee
ms.assetid: 80501867-dd7a-4648-8bd6-d4f26b68402d
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 8/04/2017
ms.author: cawa
ms.openlocfilehash: ed3e5043264cf026f74e24ca09b40ccc70086cf2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-secure-connections-tooa-service-fabric-cluster-from-visual-studio"></a>Konfigurowanie klastra sieci szkieletowej usług tooa bezpiecznych połączeń w programie Visual Studio
Dowiedz się, jak toouse toosecurely programu Visual Studio do uzyskiwania dostępu do klastra usługi sieć szkieletowa usług Azure skonfigurowane zasady kontroli dostępu.

## <a name="cluster-connection-types"></a>Typy połączeń z klastra
Dwa typy połączeń są obsługiwane przez klaster sieci szkieletowej usług Azure hello: **niezabezpieczonego** połączeń i **x509 opartego na certyfikatach** bezpiecznych połączeń. (Dla klastrów sieci szkieletowej usług hostowanych w infrastrukturze lokalnej, **Windows** i **dSTS** uwierzytelnienia są również obsługiwane.) Masz typ połączenia klastra hello tooconfigure po utworzeniu klastra hello. Po utworzeniu, nie można zmienić typu połączenia hello.

narzędzia Visual Studio usługi Service Fabric Hello obsługuje wszystkie typy uwierzytelniania dla łączenia klastra tooa publikowania. Zobacz [konfigurowania klastra sieci szkieletowej usług z portalu Azure hello](service-fabric-cluster-creation-via-portal.md) instrukcje na temat tooset zapasowej bezpiecznego klastra sieci szkieletowej usług.

## <a name="configure-cluster-connections-in-publish-profiles"></a>Konfigurowanie połączeń z klastrem w profilów publikowania
Jeśli podczas publikowania projektu sieci szkieletowej usług w programie Visual Studio, użyj hello **publikowania aplikacji sieci szkieletowej usług** toochoose — okno dialogowe klastra usługi sieć szkieletowa usług Azure. W obszarze **punktu końcowego połączenia**, wybierz istniejący klaster, w ramach Twojej subskrypcji.

![Witaj ** okno dialogowe publikowania usługi sieć szkieletowa aplikacji ** jest używane tooconfigure połączenia sieci szkieletowej usług.][publishdialog]

Witaj **publikowania aplikacji sieci szkieletowej usług** okno dialogowe automatycznie sprawdza poprawność hello połączenia klastra. W przypadku wyświetlenia monitu zaloguj się tooyour konto platformy Azure. Jeśli weryfikacja zakończy się pomyślnie, oznacza to, że system jest hello prawidłowe certyfikaty zainstalowane bezpiecznie tooconnect toohello klastra lub klaster jest niebezpieczne. Wystąpiły błędy sprawdzania poprawności może być spowodowane przez problemy z siecią lub nie ma bezpiecznego klastra tooa tooconnect systemu poprawnie skonfigurowany.

![Witaj ** opublikować usługi sieci szkieletowej aplikacji ** — okno dialogowe weryfikuje istniejące, poprawnie skonfigurowany połączenia klastra sieci szkieletowej usług.][selectsfcluster]

### <a name="tooconnect-tooa-secure-cluster"></a>tooconnect tooa bezpiecznego klastra
1. Upewnij się, że dostęp do jednego z hello certyfikaty klienta, które hello zaufania klastra docelowego. certyfikat Hello zwykle jest udostępniany jako plik wymiany informacji osobistych (pfx). Zobacz [konfigurowania klastra sieci szkieletowej usług z portalu Azure hello](service-fabric-cluster-creation-via-portal.md) dla jak tooconfigure powitania serwera toogrant dostępu tooa klienta.
2. Zainstaluj hello zaufanych certyfikatów. toodo, kliknij dwukrotnie plik PFX hello, certyfikaty lub używają ich hello PowerShell skryptu importu PfxCertificate tooimport hello. Zainstaluj certyfikat hello zbyt**Cert: \LocalMachine\My**. Jest OK tooaccept wszystkie ustawienia domyślne podczas importowania certyfikatu hello.
3. Wybierz hello **publikowania... ** polecenia menu skrótów hello hello projektu tooopen hello **publikowanie aplikacji platformy Azure** okno dialogowe i hello następnie wybierz klaster docelowy. Narzędzie Hello automatycznie rozpoznaje hello połączenia i zapisuje hello bezpiecznego połączenia, który parametrów w hello profilu.
4. Opcjonalnie: Można edytować hello toospecify profilu połączenia klastra bezpiecznego publikowania.
   
   Ponieważ ręcznego edytowania hello format XML profilu publikowania pliku toospecify hello certyfikatu informacje, czy nazwa magazynu certyfikatów hello toonote, przechowywania lokalizacji i odcisk palca certyfikatu. Będziesz potrzebować tooprovide te wartości magazynu certyfikatów hello nazwy i lokalizacji magazynu. Zobacz [porady: pobieranie hello odcisk palca certyfikatu](https://msdn.microsoft.com/library/ms734695\(v=vs.110\).aspx) Aby uzyskać więcej informacji.
   
   Można użyć hello *ClusterConnectionParameters* parametry toospecify hello PowerShell parametry toouse łączenie toohello klastra sieci szkieletowej usług. Prawidłowe parametry to, że są akceptowane przez polecenie cmdlet Connect-ServiceFabricCluster hello. Zobacz [Connect-ServiceFabricCluster](https://msdn.microsoft.com/library/mt125938.aspx) listę dostępnych parametrów.
   
   W przypadku publikowania tooa klastra zdalnego, należy najpierw toospecify hello odpowiednie parametry dla tego konkretnego klastra. Witaj, poniżej przedstawiono przykładowy łączącego tooa niezabezpieczonego klastra:
   
   `<ClusterConnectionParameters ConnectionEndpoint="mycluster.westus.cloudapp.azure.com:19000" />`
   
   Oto przykład łączącego tooan x509 opartego na certyfikatach bezpiecznego klastra:
   
   ```xml
   <ClusterConnectionParameters
   ConnectionEndpoint="mycluster.westus.cloudapp.azure.com:19000"
   X509Credential="true"
   ServerCertThumbprint="0123456789012345678901234567890123456789"
   FindType="FindByThumbprint"
   FindValue="9876543210987654321098765432109876543210"
   StoreLocation="CurrentUser"
   StoreName="My" />
   ```
5. Edytuj inne wymagane ustawienia, takie jak parametry uaktualniania i lokalizacja pliku parametrów aplikacji, a następnie opublikować aplikacji hello **publikowania aplikacji sieci szkieletowej usług** okno dialogowe w programie Visual Studio.

## <a name="next-steps"></a>Następne kroki
Aby uzyskać więcej informacji na temat uzyskiwania dostępu do sieci szkieletowej usług klastrów, zobacz [wizualizacja klastra przy użyciu Eksploratora usługi sieć szkieletowa](service-fabric-visualizing-your-cluster.md).

<!--Image references-->
[publishdialog]:./media/service-fabric-visualstudio-configure-secure-connections/publishdialog.png
[selectsfcluster]:./media/service-fabric-visualstudio-configure-secure-connections/selectsfcluster.png
