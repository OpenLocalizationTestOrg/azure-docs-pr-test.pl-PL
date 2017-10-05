---
title: "Architektura przyłączonych do domeny usługi Azure HDInsight | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak zaplanować usługę HDInsight przyłączoną do domeny."
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
ms.openlocfilehash: 7e34f47f09466a40993b4cc797ff1cad2bdaeafe
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="plan-azure-domain-joined-hadoop-clusters-in-hdinsight"></a>Planowanie klastrów Hadoop przyłączonych do domeny platformy Azure w usłudze HDInsight

Tradycyjny klaster Hadoop jest przeznaczony dla jednego użytkownika. Odpowiada to większości firm, które mają mniejsze zespoły ds. aplikacji tworzące obciążenia składające się z dużych ilości danych. Ponieważ usługa Hadoop zyskuje popularność, wiele firm przechodzi na model, w którym klastry są zarządzane przez zespoły IT, a wiele zespołów ds. aplikacji współużytkuje te same klastry. W związku z tym użytkownicy usługi Azure HDInsight często domagają się wprowadzenia obsługi klastrów przeznaczonych dla wielu użytkowników.

Zamiast tworzenia własnego wielodostępnym uwierzytelniania i autoryzacji, HDInsight polega na najbardziej popularnych dostawcy tożsamości — Active Directory (AD). Funkcji zaawansowanych zabezpieczeń w usłudze AD może służyć do zarządzania wielodostępnym autoryzacji w usłudze HDInsight. Dzięki integracji usługi HDInsight z usługą Active Directory, może komunikować się z klastrów przy użyciu poświadczeń usługi AD. HDInsight mapuje użytkownik usługi AD do lokalnego użytkownika Hadoop, wszystkie usługi działające w usłudze HDInsight (Ambari, Hive serwera, zakres, Spark thrift serwera i inne) pracy bezproblemowo dla tego uwierzytelnionego użytkownika.

## <a name="integrate-hdinsight-with-ad-and-ad-on-iaas-vm"></a>Integracja usługi HDInsight z AD i usługi AD na maszynie Wirtualnej IaaS

Dzięki integracji usługi HDInsight z usługi Azure AD lub AD na maszynie Wirtualnej Iaas, węzły klastra usługi HDInsight są przyłączonych do domeny. HDInsight tworzy nazwy główne usług dla usługi Hadoop działające w klastrze i umieszcza je w określonej jednostce organizacyjnej (OU) w usłudze Azure AD lub AD na maszynie Wirtualnej IaaS. HDInsight tworzy również wstecznego mapowania DNS w domenie dla adresów IP węzłów, które są przyłączone do domeny.

Taką konfigurację można uzyskać za pomocą różnych architektur. Dostępne są następujące architektury.

**HDInsight zintegrowane z usługą Active Directory z systemem Azure IaaS**

Jest to najprostsza architektura integrowania usługi HDInsight z usługą Active Directory. Uruchamia kontroler domeny usługi AD w jednej (lub wielu) maszynach wirtualnych (VM) na platformie Azure. Zwykle te maszyny wirtualne znajdują się w sieci wirtualnej. Dla klastra HDInsight konfiguruje się kolejną sieć wirtualną. HDInsight mają rzut oka wiersza w usłudze Active Directory, należy przy użyciu elementu równorzędnego te sieci wirtualne [równorzędna do wirtualnymi](../virtual-network/virtual-network-create-peering.md). W usłudze ARM w przypadku utworzenia usługi Active Directory, można utworzyć usługi Active Directory i usługi HDInsight w tej samej sieci wirtualnej i nie trzeba wykonać komunikacji równorzędnej. 

![Topologia klastra HDInsight z przyłączaniem do domeny](./media/hdinsight-domain-joined-architecture/hdinsight-domain-joined-architecture_1.png)

> [!NOTE]
> W tej architekturze nie można używać usługi Azure Data Lake Store z klastrem HDInsight.


Wymagania wstępne dotyczące usługi Active Directory:

* Musi zostać utworzona [jednostka organizacyjna](../active-directory-domain-services/active-directory-ds-admin-guide-create-ou.md), w której mają zostać umieszczone maszyny wirtualne klastra HDInsight i nazwy główne usług używane przez klaster.
* [Protokoły dostępu do katalogu lekkie](../active-directory-domain-services/active-directory-ds-admin-guide-configure-secure-ldap.md) (LDAPs) musi zostać skonfigurowany do komunikowania się z usługą Active Directory. Certyfikat użyty do skonfigurowania protokołu LDAPS musi być prawdziwy (nie może być certyfikatem z podpisem własnym).
* W domenie muszą zostać utworzone odwrotne strefy DNS dla zakresu adresów IP podsieci usługi HDInsight (na przykład 10.2.0.0/24 na poprzedniej ilustracji).
* Potrzebne jest konto usługi lub konto użytkownika. Zostanie ono użyte do utworzenia klastra HDInsight. To konto musi mieć następujące uprawnienia:

    - Uprawnienia do tworzenia obiektów nazw głównych usług i obiektów maszyn w jednostce organizacyjnej.
    - Uprawnienia do tworzenia reguł serwera proxy odwrotnej usługi DNS.
    - Uprawnienia do przyłączania maszyn do domeny usługi Active Directory.

**Usługa HDInsight zintegrowana z usługą Azure AD tylko w chmurze**

W przypadku usługi Azure AD działającej tylko na chmurze należy skonfigurować kontroler domeny, aby umożliwić integrację usługi HDInsight z usługą Azure AD. Jest to realizowane za pośrednictwem [Azure Active Directory Domain Services](../active-directory-domain-services/active-directory-ds-overview.md) (Azure AD DS). Usługi Azure AD DS tworzą maszyny kontrolera domeny w chmurze i udostępniają ich adresy IP. W celu zapewnienia wysokiej dostępności tworzone są dwa kontrolery domeny.

Obecnie usługi Azure AD DS istnieją tylko w klasycznych sieciach wirtualnych. Są one dostępne tylko za pomocą klasycznej witryny Azure Portal. Sieć wirtualna usługi HDInsight istnieje w witrynie Azure Portal i trzeba ją połączyć równorzędnie z klasyczną siecią wirtualną za pomocą równorzędnego łączenia sieci wirtualnych.

> [!NOTE]
> Równorzędne łączenie klasycznej sieci wirtualnej i sieci wirtualnej usługi Azure Resource Manager wymaga, aby obie sieci wirtualne znajdowały się w tym samym regionie i tej samej subskrypcji platformy Azure.

![Topologia klastra HDInsight z przyłączaniem do domeny](./media/hdinsight-domain-joined-architecture/hdinsight-domain-joined-architecture_2.png)

Wymagania wstępne dotyczące usługi Azure AD:

* Musi zostać utworzona [jednostka organizacyjna](../active-directory-domain-services/active-directory-ds-admin-guide-create-ou.md), w której mają zostać umieszczone maszyny wirtualne klastra HDInsight i nazwy główne usług używane przez klaster.
* Podczas konfigurowania usług Azure AD DS musi zostać skonfigurowany protokół [LDAPS](../active-directory-domain-services/active-directory-ds-admin-guide-configure-secure-ldap.md). Certyfikat użyty do skonfigurowania protokołu LDAPS musi być prawdziwy (nie może być certyfikatem z podpisem własnym).
* W domenie muszą zostać utworzone odwrotne strefy DNS dla zakresu adresów IP podsieci usługi HDInsight (na przykład 10.2.0.0/24 na poprzedniej ilustracji).
* Między usługą Azure AD a usługą Azure AD DS muszą zostać zsynchronizowane [skróty haseł](../active-directory-domain-services/active-directory-ds-getting-started-password-sync.md).
* Potrzebne jest konto usługi lub konto użytkownika. Zostanie ono użyte do utworzenia klastra HDInsight. To konto musi mieć następujące uprawnienia:

    - Uprawnienia do tworzenia obiektów nazw głównych usług i obiektów maszyn w jednostce organizacyjnej.
    - Uprawnienia do tworzenia reguł serwera proxy odwrotnej usługi DNS.
    - Uprawnienia do przyłączania maszyn do domeny usługi Azure AD.

## <a name="next-steps"></a>Następne kroki
* Aby skonfigurować przyłączony do domeny klaster usługi HDInsight, zobacz [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md) (Konfigurowanie przyłączonych do domeny klastrów usługi HDInsight).
* Aby zarządzać przyłączonymi do domeny klastrami usługi HDInsight, zobacz [Manage Domain-joined HDInsight clusters](hdinsight-domain-joined-manage.md) (Zarządzanie przyłączonymi do domeny klastrami usługi HDInsight).
* Aby znaleźć informacje na temat konfigurowania zasad usługi Hive i uruchamiania zapytań usługi Hive, zobacz [Konfigurowanie zasad usługi Hive dla przyłączonych do domeny klastrów usługi HDInsight](hdinsight-domain-joined-run-hive.md).
* Uruchamianie zapytań Hive przy użyciu protokołu SSH w klastrach HDInsight przyłączonych do domeny, zobacz [używanie SSH z usługą HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).
