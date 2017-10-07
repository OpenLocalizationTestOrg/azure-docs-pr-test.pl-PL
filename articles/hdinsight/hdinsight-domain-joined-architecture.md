---
title: "Architektura przyłączone aaaDomain Azure HDInsight | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooplan przyłączonych do domeny usługi HDInsight."
services: hdinsight
documentationcenter: 
author: saurinsh
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 7dc6847d-10d4-4b5c-9c83-cc513cf91965
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 02/03/2017
ms.author: saurinsh
ms.openlocfilehash: 1c3ecedf3739b4f8fa54160225be9c1d6e2ca6cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="plan-azure-domain-joined-hadoop-clusters-in-hdinsight"></a>Planowanie klastrów Hadoop przyłączonych do domeny platformy Azure w usłudze HDInsight

Witaj tradycyjnych Hadoop jest klastra jednego użytkownika. Odpowiada to większości firm, które mają mniejsze zespoły ds. aplikacji tworzące obciążenia składające się z dużych ilości danych. Ponieważ usługa Hadoop zyskuje popularność, wiele firm przechodzi na model, w którym klastry są zarządzane przez zespoły IT, a wiele zespołów ds. aplikacji współużytkuje te same klastry. W związku z tym funkcje są udziałem sieciowym klastrów między hello najbardziej żądanej funkcji w usłudze Azure HDInsight.

Zamiast tworzenia własnego wielodostępnym uwierzytelniania i autoryzacji, HDInsight polega na powitania dostawcy najpopularniejszych tożsamości — Active Directory (AD). Hello funkcji zaawansowanych zabezpieczeń w usłudze AD może być używane toomanage autoryzacji użytkowników w usłudze HDInsight. Dzięki integracji usługi HDInsight z usługą Active Directory, mogą komunikować się z klastrami hello przy użyciu poświadczeń usługi AD. HDInsight mapuje AD użytkownika tooa Hadoop użytkownika lokalnego, więc wszystkie hello usług uruchomionych w usłudze HDInsight (Ambari, Hive serwera, zakres, Spark thrift serwera i inne) pracy bezproblemowo dla hello uwierzytelnianego użytkownika.

## <a name="integrate-hdinsight-with-ad-and-ad-on-iaas-vm"></a>Integracja usługi HDInsight z AD i usługi AD na maszynie Wirtualnej IaaS

Dzięki integracji usługi HDInsight z usługi Azure AD lub AD na maszynie Wirtualnej Iaas, węzły klastra usługi HDInsight hello są domeny tooa przyłączonych do domeny. HDInsight tworzy nazwy główne usług dla hello uruchomiona w klastrze hello usług Hadoop i umieszcza je w określonej jednostce organizacyjnej (OU) w usłudze Azure AD lub AD na maszynie Wirtualnej IaaS. HDInsight tworzy również wstecznego mapowania DNS w domenie hello hello adresów IP określonych węzłów hello toohello przyłączone do domeny.

Taką konfigurację można uzyskać za pomocą różnych architektur. Można wybrać z powitania po architektury.

**HDInsight zintegrowane z usługą Active Directory z systemem Azure IaaS**

Jest to najprostsza architektura hello integrowanie HDInsight z usługą Active Directory. Witaj kontroler domeny usługi AD jest uruchamiany na jednej (lub wielu) maszynach wirtualnych (VM) na platformie Azure. Zwykle te maszyny wirtualne znajdują się w sieci wirtualnej. Konfigurowanie klastra usługi HDInsight hello innej sieci wirtualnej. Dla usługi HDInsight toohave tooActive wiersza procesów z katalogu, należy toopeer tych sieci wirtualnych za pomocą [równorzędna do wirtualnymi](../virtual-network/virtual-network-create-peering.md). Jeśli utworzysz hello usługi Active Directory w usłudze ARM, można utworzyć hello usługi Active Directory i usługi HDInsight w hello tej samej sieci wirtualnej i nie ma potrzeby toodo komunikacji równorzędnej. 

![Topologia klastra HDInsight z przyłączaniem do domeny](./media/hdinsight-domain-joined-architecture/hdinsight-domain-joined-architecture_1.png)

> [!NOTE]
> W ramach tej architektury usługi Azure Data Lake Store nie można używać z klastrem usługi HDInsight hello.


Wymagania wstępne dotyczące usługi Active Directory:

* [Jednostki organizacyjnej](../active-directory-domain-services/active-directory-ds-admin-guide-create-ou.md) musi zostać utworzony, w którym zostanie umieszczony hello maszyn wirtualnych z klastra usługi HDInsight i hello jednostki usługi używane przez klaster hello.
* [Protokoły dostępu do katalogu lekkie](../active-directory-domain-services/active-directory-ds-admin-guide-configure-secure-ldap.md) (LDAPs) musi zostać skonfigurowany do komunikowania się z usługą Active Directory. tooset certyfikat używany Hello zapasowej LDAPS musi być rzeczywistym certyfikatu (nie certyfikatu z podpisem własnym).
* Stref wyszukiwania wstecznego DNS należy utworzyć w domenie hello zakresu adresów IP hello hello HDInsight podsieci (na przykład 10.2.0.0/24 poprzedni obraz powitania).
* Potrzebne jest konto usługi lub konto użytkownika. Użyj tego konta toocreate hello klastra usługi HDInsight. To konto musi mieć hello następujących uprawnień:

    - Obiekty główne usługi toocreate uprawnienia i obiekty komputera w ramach jednostki organizacyjnej hello
    - Uprawnienia toocreate wstecznego DNS serwera proxy reguły
    - Domena usługi Active Directory toohello maszyny toojoin uprawnień

**Usługa HDInsight zintegrowana z usługą Azure AD tylko w chmurze**

W przypadku usługi Azure AD działającej tylko na chmurze należy skonfigurować kontroler domeny, aby umożliwić integrację usługi HDInsight z usługą Azure AD. Jest to realizowane za pośrednictwem [Azure Active Directory Domain Services](../active-directory-domain-services/active-directory-ds-overview.md) (Azure AD DS). Azure AD DS tworzy maszyny kontrolera domeny w chmurze hello i udostępnia adresy IP dla nich. W celu zapewnienia wysokiej dostępności tworzone są dwa kontrolery domeny.

Obecnie usługi Azure AD DS istnieją tylko w klasycznych sieciach wirtualnych. Są one dostępne wyłącznie przy użyciu hello klasycznego portalu Azure. Witaj HDInsight w portalu Azure, którą należy toobe hello istnieje sieci wirtualnej połączyć za pomocą z hello klasycznej sieci wirtualnej przy użyciu sieci wirtualnej do sieci wirtualnej komunikacji równorzędnej.

> [!NOTE]
> Komunikacji równorzędnej między klasycznej sieci wirtualnej i sieci wirtualnej wymaga, aby obie sieci wirtualne znajdują się w usłudze Azure Resource Manager hello na tym samym regionie i w obszarze hello sam subskrypcji platformy Azure.

![Topologia klastra HDInsight z przyłączaniem do domeny](./media/hdinsight-domain-joined-architecture/hdinsight-domain-joined-architecture_2.png)

Wymagania wstępne dotyczące usługi Azure AD:

* [Jednostki organizacyjnej](../active-directory-domain-services/active-directory-ds-admin-guide-create-ou.md) musi zostać utworzony, w którym zostanie umieszczony hello maszyn wirtualnych z klastra usługi HDInsight i hello jednostki usługi używane przez klaster hello.
* Podczas konfigurowania usług Azure AD DS musi zostać skonfigurowany protokół [LDAPS](../active-directory-domain-services/active-directory-ds-admin-guide-configure-secure-ldap.md). tooset certyfikat używany Hello zapasowej LDAPS musi być rzeczywistym certyfikatu (nie certyfikatu z podpisem własnym).
* Stref wyszukiwania wstecznego DNS należy utworzyć w domenie hello zakresu adresów IP hello hello HDInsight podsieci (na przykład 10.2.0.0/24 poprzedni obraz powitania).
* [Skrótów haseł](../active-directory-domain-services/active-directory-ds-getting-started-password-sync.md) musi być synchronizowane z usługi Azure AD tooAzure usług AD DS.
* Potrzebne jest konto usługi lub konto użytkownika. Użyj tego konta toocreate hello klastra usługi HDInsight. To konto musi mieć hello następujących uprawnień:

    - Obiekty główne usługi toocreate uprawnienia i obiekty komputera w ramach jednostki organizacyjnej hello
    - Uprawnienia toocreate wstecznego DNS serwera proxy reguły
    - Uprawnienia toojoin maszyny toohello usługi Azure AD domeny

## <a name="next-steps"></a>Następne kroki
* tooconfigure klastra usługi HDInsight przyłączonych do domeny, zobacz [skonfigurować przyłączonych do domeny w usłudze hdinsight](hdinsight-domain-joined-configure.md).
* toomanage przyłączonych do domeny w usłudze hdinsight, zobacz [zarządzania klastrami HDInsight przyłączonych do domeny](hdinsight-domain-joined-manage.md).
* zasady Hive tooconfigure i wykonywania zapytań programu Hive, zobacz [Hive skonfigurować zasady dla przyłączonych do domeny w usłudze hdinsight](hdinsight-domain-joined-run-hive.md).
* toorun zapytań Hive przy użyciu protokołu SSH w klastrach HDInsight przyłączonych do domeny, zobacz [używanie SSH z usługą HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).
