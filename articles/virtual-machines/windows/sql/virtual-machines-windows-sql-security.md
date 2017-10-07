---
title: aaaSecurity programu SQL Server na platformie Azure | Dokumentacja firmy Microsoft
description: "Ten temat zawiera ogólne wskazówki dotyczące zabezpieczania programu SQL Server uruchomionego w maszynie wirtualnej platformy Azure."
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: d710c296-e490-43e7-8ca9-8932586b71da
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 06/02/2017
ms.author: jroth
ms.openlocfilehash: 14c3d828fa87446da67beea6d28886de254afe15
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="security-considerations-for-sql-server-in-azure-virtual-machines"></a>Zagadnienia dotyczące zabezpieczeń programu SQL Server na maszynach wirtualnych platformy Azure

Ten temat zawiera ogólne wskazówki dotyczące zabezpieczeń, które pomaga ustalić wystąpienia serwera tooSQL bezpiecznego dostępu w maszynie wirtualnej platformy Azure (VM).

Azure jest zgodna z kilku przepisów branżowych i standardy, które można toobuild rozwiązanie zgodne z programem SQL Server działa na maszynie wirtualnej. Aby uzyskać informacje o zgodności z przepisami z platformy Azure, zobacz [Centrum zaufania Azure](https://azure.microsoft.com/support/trust-center/).

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="control-access-toohello-sql-vm"></a>Kontrola dostępu toohello maszyny Wirtualnej SQL

Podczas tworzenia maszyny wirtualnej programu SQL Server, należy rozważyć sposób toocarefully kontrolować, kto ma dostęp toohello maszyny i tooSQL serwera. Ogólnie rzecz biorąc, należy wykonać następujące hello:

- Ograniczanie dostępu tooSQL serwera tooonly hello aplikacji i klientów, którzy go potrzebują.
- Należy stosować najlepsze rozwiązania dotyczące zarządzania konta użytkownika i hasła.

Hello następujące sekcje zawierają sugestie dotyczące planowania przy użyciu tych punktów.

## <a name="secure-connections"></a>Bezpieczne połączenia

Po utworzeniu maszyny wirtualnej programu SQL Server z obrazem galerii hello **łączności z serwerem SQL** zapewnia hello wybór opcji **lokalnego (wewnątrz maszyny Wirtualnej)**, **prywatne (wewnątrz sieci wirtualnej)** , lub **publiczne (Internet)**.

![Łączność serwera SQL](./media/virtual-machines-windows-sql-security/sql-vm-connectivity-option.png)

Najlepiej hello opcję hello najbardziej restrykcyjne dla danego scenariusza. Na przykład, jeśli używasz aplikacji, która uzyskuje dostęp do programu SQL Server na hello tej samej maszyny Wirtualnej, następnie **lokalnego** jest najbezpieczniejszy wybór hello. Jeśli używasz aplikacji Azure wymaga dostępu toohello programu SQL Server, następnie **prywatnej** zabezpiecza tooSQL komunikacji serwera tylko w obrębie hello określony [sieci wirtualnej Azure](../../../virtual-network/virtual-networks-overview.md). Jeśli potrzebujesz **publicznego** (internest) toohello dostęp do maszyny Wirtualnej z serwera SQL, następnie upewnij się, że toofollow innych najlepszych rozwiązań w tym tooreduce tematu obszaru powierzchni ataku.

Witaj wybranych opcji w portalu hello użyć reguły zabezpieczeń ruchu przychodzącego na powitania maszyn wirtualnych [sieciowej grupy zabezpieczeń](../../../virtual-network/virtual-networks-nsg.md) tooallow (NSG) lub odmówić maszyny wirtualnej tooyour ruchu sieciowego. Można zmodyfikować lub utworzyć nowe reguły NSG przychodzące port serwera SQL (domyślnie 1433) dla ruchu toohello tooallow. Można również określić określonych adresów IP, które mogą toocommunicate za pośrednictwem tego portu.

![Reguły grupy zabezpieczeń sieci](./media/virtual-machines-windows-sql-security/sql-vm-network-security-group-rules.png)

Ponadto tooNSG reguły ruchu sieciowego toorestrict, umożliwia także hello zapory systemu Windows na maszynie wirtualnej hello.

Jeśli korzystasz z punktów końcowych z hello klasycznego modelu wdrażania, jeśli nie należy używać, Usuń żadnych punktów końcowych na maszynie wirtualnej hello. Aby uzyskać instrukcje dotyczące przy użyciu list kontroli dostępu z punktami końcowymi, zobacz [Zarządzaj hello listy ACL punktu końcowego](../classic/setup-endpoints.md#manage-the-acl-on-an-endpoint). To nie jest niezbędna dla maszyn wirtualnych korzystających z hello Menedżera zasobów.

Zaleca się włączenie połączeń szyfrowanych dla wystąpienia hello hello aparatu bazy danych programu SQL Server w sieci maszyny wirtualnej platformy Azure. Skonfiguruj wystąpienie programu SQL server przy użyciu podpisanego certyfikatu. Aby uzyskać więcej informacji, zobacz [toohello Włącz połączenia szyfrowane aparatu bazy danych](https://docs.microsoft.com/sql/database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine) i [składnia ciągu połączenia](https://msdn.microsoft.com/library/ms254500.aspx).

## <a name="use-a-non-default-port"></a>Korzystanie z portu inny niż domyślny

Domyślnie program SQL Server nasłuchuje na dobrze znanego portu 1433. Aby zwiększyć bezpieczeństwo należy skonfigurować toolisten programu SQL Server na port inny niż domyślny, na przykład 1401. Jeśli dostarczasz obraz galerii programu SQL Server w portalu Azure hello ten port można określić w hello **ustawienia programu SQL Server** bloku.

tooconfigure to po zainicjowaniu obsługi administracyjnej, dostępne są dwie opcje:

- Dla maszyn wirtualnych Menedżera zasobów, można wybrać **konfigurację programu SQL Server** z bloku omówienie maszyny Wirtualnej hello. Zapewnia to opcja toochange hello portu.

  ![Zmień TCP port w portalu](./media/virtual-machines-windows-sql-security/sql-vm-change-tcp-port.png)

- Klasycznych maszyn wirtualnych lub maszyn wirtualnych serwera SQL, które nie zostały udostępnione za pomocą portalu hello można ręcznie skonfigurować hello port przy połączeniu zdalnym toohello maszyny Wirtualnej. Witaj kroki konfiguracji, zobacz [skonfigurować tooListen serwera na konkretnym porcie TCP](https://docs.microsoft.com/sql/database-engine/configure-windows/configure-a-server-to-listen-on-a-specific-tcp-port). Jeśli używasz tej techniki ręczne, należy również tooadd zapory systemu Windows regułę tooallow ruch przychodzący na tym porcie TCP.

> [!IMPORTANT]
> Określenie z systemem innym niż domyślny port jest dobrym rozwiązaniem, jeśli port programu SQL Server jest otwarty toopublic połączeń internetowych.

Jeśli serwer SQL nasłuchuje na porcie innych niż domyślne, należy określić hello port podczas nawiązywania połączenia. Na przykład Rozważmy scenariusz, w którym adres IP serwera hello jest 13.55.255.255 i SQL Server nasłuchuje na porcie 1401. tooSQL tooconnect serwera, należy określić `13.55.255.255,1401` w parametrach połączenia hello.

## <a name="manage-accounts"></a>Zarządzanie kontami

Nie ma nazwy kont wynik tooeasily osoby atakujące lub hasła. Użyj powitania po toohelp porady:

- Utwórz konto administratora lokalnego unikatowy, który nie ma nazwy **administratora**.

- Użyj złożonych silnych haseł dla wszystkich kont. Aby uzyskać więcej informacji o tym, jak toocreate silnego hasła, zobacz [Utwórz silne hasło](https://support.microsoft.com/instantanswers/9bd5223b-efbe-aa95-b15a-2fb37bef637d/create-a-strong-password) artykułu.

- Domyślnie program Azure wybiera uwierzytelniania systemu Windows podczas instalacji maszyny wirtualnej programu SQL Server. W związku z tym hello **SA** logowania jest wyłączona, a hasło jest przypisywany przez Instalatora. Firma Microsoft zaleca tego hello **SA** logowania nie należy używać ani włączony. Jeśli identyfikator logowania SQL, użyj jednej z następujących strategii hello:

  - Utwórz konto SQL o unikatowej nazwie, która ma **sysadmin** członkostwa. Można to zrobić w portalu hello włączając **uwierzytelniania SQL** podczas inicjowania obsługi.

    > [!TIP] 
    > Jeśli nie zostanie włączone uwierzytelnianie SQL podczas inicjowania obsługi, należy ręcznie zmienić tryb uwierzytelniania hello zbyt**programu SQL Server i tryb uwierzytelniania systemu Windows**. Aby uzyskać więcej informacji, zobacz [Zmień tryb uwierzytelniania serwera](https://docs.microsoft.com/sql/database-engine/configure-windows/change-server-authentication-mode).

  - Jeśli musisz użyć hello **SA** logowania, Włącz hello logowania po inicjowania obsługi administracyjnej i przypisz nowe silne hasło.

## <a name="follow-on-premises-best-practices"></a>Należy stosować najlepsze rozwiązania lokalnego

Ponadto toohello rozwiązania opisane w tym temacie, firma Microsoft zaleca możesz sprawdzić i wdrożenia rozwiązania w zakresie zabezpieczeń hello tradycyjnych, lokalnie, jeśli to możliwe. Aby uzyskać więcej informacji, zobacz [zagadnienia dotyczące zabezpieczeń dla instalacji serwera SQL](https://docs.microsoft.com/sql/sql-server/install/security-considerations-for-a-sql-server-installation)

## <a name="next-steps"></a>Następne kroki

Jeśli interesuje Cię również najlepsze rozwiązania dotyczące wydajności, zobacz [wydajności najlepsze rozwiązania dotyczące programu SQL Server w usłudze Azure Virtual Machines](virtual-machines-windows-sql-performance.md).

Dla innych tematach dotyczących toorunning programu SQL Server na maszynach wirtualnych Azure, zobacz [programu SQL Server na maszynach wirtualnych platformy Azure — omówienie](virtual-machines-windows-sql-server-iaas-overview.md).

