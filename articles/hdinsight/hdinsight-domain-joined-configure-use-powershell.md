---
title: "klastry HDInsight przyłączonych do domeny za pomocą programu PowerShell - Azure aaaConfigure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooset Konfigurowanie i skonfigurować przyłączonych do domeny w usłudze hdinsight przy użyciu programu Azure PowerShell"
services: hdinsight
documentationcenter: 
author: saurinsh
manager: jhubbard
editor: cgronlun
tags: 
ms.assetid: a13b2f7a-612d-4800-bc92-7fc0524f3e89
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 11/02/2016
ms.author: saurinsh
ms.openlocfilehash: 49da3439513d1e51171f0f7f7f9c3d967d55cb7b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-domain-joined-hdinsight-clusters-preview-using-azure-powershell"></a>Konfigurowanie klastrów HDInsight przyłączonych do domeny (wersja zapoznawcza) przy użyciu programu Azure PowerShell
Dowiedz się, jak klastra tooset zapasowej Azure HDInsight z usługą Azure Active Directory (Azure AD) i [zakres Apache](http://hortonworks.com/apache/ranger/) przy użyciu programu Azure PowerShell. Skrypt programu Azure PowerShell podano konfiguracji hello toomake szybsze i mniej podatna. HDInsight przyłączonych do domeny można skonfigurować tylko w klastrach opartych na systemie Linux. Aby uzyskać więcej informacji, zobacz [klastrów HDInsight przyłączonych do domeny wprowadź](hdinsight-domain-joined-introduction.md).

> [!IMPORTANT]
> Oozie nie jest włączona w usłudze HDInsight z przyłączonych do domeny.

Typowej konfiguracji klastra domeny w usłudze HDInsight obejmuje hello następujące kroki:

1. Utwórz sieć wirtualną platformy Azure classic usługi Azure AD.  
2. Tworzenie i konfigurowanie usługi Azure AD i Azure AD DS.
3. Dodaj toohello wirtualna klasycznej sieci wirtualnej do tworzenia jednostki organizacyjnej. 
4. Utwórz jednostkę organizacyjną dla usługi Azure AD DS.
5. Tworzenie sieci wirtualnej usługi HDInsight w trybie zarządzania hello zasobów platformy Azure.
6. Instalator wstecznego stref hello Azure usług AD DS.
7. Równorzędnej Witaj dwie sieci wirtualne.
8. Tworzenie klastra usługi HDInsight.

Witaj skryptu PowerShell wykonuje kroki od 3 do 7. Przejdź do kroku 1 i 2 ręcznie.  Jeśli wolisz toouse programu Azure PowerShell, zobacz [klastrów HDInsight przyłączonych do domeny skonfiguruj](hdinsight-domain-joined-configure.md). 

Przykład topologii końcowego hello wygląda następująco:

![Topologia HDInsight przyłączonych do domeny](./media/hdinsight-domain-joined-configure/hdinsight-domain-joined-topology.png)

Ponieważ aktualnie usługi Azure AD obsługuje tylko klasycznych sieci wirtualnych (sieci wirtualne) i opartych na systemie Linux klastrów usługi HDInsight obsługują tylko usługi Azure Resource Manager na podstawie sieci wirtualnych, integracja HDInsight usługi Azure AD wymaga dwóch sieci wirtualnych i komunikacji równorzędnej między nimi. Uzyskać hello porównanie między hello dwa modele wdrażania, zobacz [usługi Azure Resource Manager, a wdrożenie klasyczne: zrozumienie modele wdrażania i stan zasobów hello](../azure-resource-manager/resource-manager-deployment-model.md). Witaj dwie sieci wirtualne muszą znajdować się w hello tego samego regionu hello Azure usług AD DS.

> [!NOTE]
> Ten samouczek zakłada, że nie masz usługi Azure AD. Jeśli masz, możesz pominąć części hello w kroku 2.
> 
> 

## <a name="prerequisites"></a>Wymagania wstępne
Musi mieć następujące elementy toogo opisanych w tym samouczku hello:

* Zapoznaj się z [usług domenowych Azure AD](https://azure.microsoft.com/services/active-directory-ds/) jej [cennik](https://azure.microsoft.com/pricing/details/active-directory-ds/) struktury.
* Upewnij się, że Twoja subskrypcja jest białej dla tej publicznej wersji zapoznawczej. Możesz to zrobić, wysyłając wiadomość e-mail toohdipreview@microsoft.com z identyfikatorem subskrypcji
* Certyfikat SSL, który jest podpisany przez urząd podpisywania dla domeny. Witaj certyfikat jest wymagany przez skonfigurowanie bezpiecznego protokołu LDAP. Nie można używać certyfikatów z podpisem własnym.
* Azure PowerShell.  Zobacz [Instalowanie i konfigurowanie programu Azure PowerShell](/powershell/azure/overview).

## <a name="create-an-azure-classic-vnet-for-your-azure-ad"></a>Utwórz sieć wirtualną platformy Azure classic usługi Azure AD.
Witaj instrukcje, zobacz [tutaj](hdinsight-domain-joined-configure.md#create-an-azure-virtual-network-classic).

## <a name="create-and-configure-azure-ad-and-azure-ad-ds"></a>Tworzenie i konfigurowanie usługi Azure AD i Azure AD DS.
Witaj instrukcje, zobacz [tutaj](hdinsight-domain-joined-configure.md#create-and-configure-azure-ad-ds-for-your-azure-ad).

## <a name="run-hello-powershell-script"></a>Uruchom skrypt programu PowerShell hello
Witaj skrypt programu PowerShell można pobrać z [GitHub](https://github.com/hdinsight/DomainJoinedHDInsight). Wyodrębnij plik zip hello i zapisywać pliki hello lokalnie.

**Witaj tooedit skrypt programu PowerShell**

1. Otwórz run.ps1 przy użyciu programu Windows PowerShell ISE lub edytorze tekstu.
2. Należy wypełnić wartości hello hello następujące zmienne:
   
   * **$SubscriptionName** — Witaj nazwa hello subskrypcji platformy Azure, w którym ma toocreate z klastrem usługi HDInsight. Utworzono już klasycznej sieci wirtualnej w ramach tej subskrypcji, a następnie zostanie tworzenie sieci wirtualnej platformy Azure Resource Manager dla klastra usługi HDInsight hello w ramach subskrypcji.
   * **$ClassicVNetName** -hello klasycznej sieci wirtualnej, która zawiera hello Azure usług AD DS. Ta sieć wirtualna musi być w hello tej samej subskrypcji, które podano powyżej. Ta sieć wirtualna musi zostać utworzony przy użyciu hello portalu Azure, a nie przy użyciu klasycznego portalu. Po wykonaniu instrukcji hello w [przyłączonych do domeny skonfiguruj klastrów usługi HDInsight (wersja zapoznawcza)](hdinsight-domain-joined-configure.md#create-an-azure-virtual-network-classic), hello nazwa domyślna to contosoaadvnet.
   * **$ClassicResourceGroupName** — Nazwa grupy Resource Manager hello hello klasycznej sieci wirtualnej, który został podany powyżej. Na przykład contosoaadrg. 
   * **$ArmResourceGroupName** — Witaj Nazwa grupy zasobów w ramach których mają klastra usługi HDInsight hello toocreate. Witaj można użyć tej samej grupie zasobów co $ArmResourceGroupName.  Jeśli grupa zasobów hello nie istnieje, hello skrypt tworzy hello grupy zasobów.
   * **$ArmVNetName** -hello Resource Manager wirtualnej nazwy sieciowej w ramach którego ma zostać klastra usługi HDInsight hello toocreate. Ta sieć wirtualna zostaną umieszczone w $ArmResourceGroupName.  Jeśli hello sieć wirtualna nie istnieje, zostanie utworzony hello skrypt programu PowerShell. Istnieje, powinien być częścią grupy zasobów hello podane powyżej.
   * **$AddressVnetAddressSpace** — Witaj sieci przestrzeni adresowej dla sieci wirtualnej hello Menedżera zasobów. Upewnij się, że ta przestrzeń adresowa jest dostępny. Ta przestrzeń adresowa nie może nakładać się hello klasycznej sieci wirtualnej przestrzeni adresowej. Na przykład "10.1.0.0/16"
   * **$ArmVnetSubnetName** -hello Resource Manager nazwę podsieci sieci wirtualnej w ramach którego ma zostać klastra usługi HDInsight hello tooplace maszyn wirtualnych. Jeśli hello podsieć nie istnieje, zostanie utworzony hello skrypt programu PowerShell. Jeśli istnieje, należy go częścią sieci wirtualnej hello podane powyżej.
   * **$AddressSubnetAddressSpace** — Witaj sieci zakres adresów dla podsieci sieci wirtualnej hello Menedżera zasobów. Witaj klastra usługi HDInsight jest od ten zakres adresów podsieci adresów IP maszyny Wirtualnej. Na przykład "10.1.0.0/24".
   * **$ActiveDirectoryDomainName** — nazwa domeny hello Azure AD, które mają toojoin hello HDInsight cluster maszyn wirtualnych do. Na przykład "contoso.onmicrosoft.com"
   * **$ClusterUsersGroups** — nazwa pospolita hello hello grup zabezpieczeń usługi AD, które mają klastra usługi HDInsight toohello toosync. Użytkownicy Hello w ramach tej grupy zabezpieczeń będą mogli toolog na pulpicie nawigacyjnym klastra toohello przy użyciu swoich poświadczeń domeny usługi active directory. Te grupy zabezpieczeń musi istnieć w usłudze active directory hello. Na przykład "hiveusers" lub "clusteroperatorusers".
   * **$OrganizationalUnitName** -hello jednostki organizacyjnej w domenie hello, w którym klaster usługi HDInsight hello tooplace maszyn wirtualnych i hello jednostki usługi używane przez klaster hello. Hello skrypt programu PowerShell spowoduje utworzenie tej jednostki Organizacyjnej, jeśli nie istnieje. Na przykład "HDInsightOU".
3. Zapisz zmiany hello.

**toorun hello skryptu**

1. Uruchom **programu Windows PowerShell** jako administrator.
2. Przeglądaj w folderze toohello run.ps1. 
3. Uruchom skrypt hello, wpisując nazwę pliku hello i naciśnij przycisk **ENTER**.  Wyskakującej 3 logowanie dialogów:
   
   1. **Zaloguj się w portalu klasycznym tooAzure** — wprowadź swoje poświadczenia, których używasz toosign w portalu klasycznym tooAzure. Należy utworzyć hello Azure AD i Azure AD DS przy użyciu tych poświadczeń.
   2. **Zaloguj się w portalu usługi Resource Manager tooAzure** — wprowadź swoje poświadczenia, których używasz toosign w portalu usługi Resource Manager tooAzure.
   3. **Nazwa użytkownika domeny** — wprowadź poświadczenia hello hello nazw użytkowników, które mają toobe administratora w klastrze usługi HDInsight hello. Jeśli utworzono usługi Azure AD od początku, należy je utworzyć tego użytkownika za pomocą tej dokumentacji. 
      
      > [!IMPORTANT]
      > Wprowadź nazwę użytkownika hello w następującym formacie: 
      > 
      > Nazwa_domeny (na przykład contoso.onmicrosoft.com\clusteradmin)
      > 
      > 
      
      Ten użytkownik musi mieć uprawnienia 3: toohello maszyny toojoin podane domeny usługi Active Directory. nazwy główne usług toocreate i obiekty komputera w ramach hello udostępniane jednostka organizacyjna. i tooadd wstecznego DNS serwera proxy zasady.

Podczas tworzenia stref wyszukiwania wstecznego DNS, hello skryptu spowoduje wyświetlenie monitu tooenter identyfikator sieciowy. Ten identyfikator sieci musi być prefiksem adresu hello Menedżera zasobów sieci wirtualnej. Na przykład jeśli przestrzeń adresowa podsieci sieci wirtualnej Menedżera zasobów jest 10.2.0.0/24, wprowadź 10.2.0.0/24 podczas hello narzędzie wyświetla monit o podanie identyfikatora hello sieci. 

## <a name="create-hdinsight-cluster"></a>Tworzenie klastra usługi HDInsight
W tej sekcji tworzenia klastra opartą na systemie Linux platformą Hadoop w usłudze HDInsight przy użyciu albo hello portalu Azure lub [szablonu usługi Azure Resource Manager](../azure-resource-manager/resource-group-template-deploy.md). Inne metody tworzenia klastrów i opis ustawień hello, zobacz [Tworzenie klastrów usługi HDInsight](hdinsight-hadoop-provision-linux-clusters.md). Więcej informacji o używaniu toocreate szablonu usługi Resource Manager Hadoop klastrów w usłudze HDInsight, zobacz [klastrów utworzyć Hadoop w HDInsight przy użyciu szablonów usługi Resource Manager](hdinsight-hadoop-create-windows-clusters-arm-templates.md)

**klaster HDInsight przyłączonych do domeny za pomocą toocreate hello portalu Azure**

1. Zaloguj się na toohello [portalu Azure](https://portal.azure.com).
2. Kliknij przycisk **nowy**, **analizy i analiza**, a następnie **HDInsight**.
3. Z hello **klastra usługi HDInsight nowe** bloku, wprowadź lub wybierz hello następujące wartości:
   
   * **Nazwa klastra**: Wprowadź nazwę nowego klastra hello przyłączonych do domeny klastra usługi HDInsight.
   * **Subskrypcja**: Wybierz subskrypcję platformy Azure używana do tworzenia tego klastra.
   * **Konfiguracja klastra**:
     
     * **Typ klastra**: Hadoop. HDInsight przyłączonych do domeny jest obecnie klastrów tylko obsługiwana w Hadoop.
     * **System operacyjny**: systemu Linux.  HDInsight przyłączonych do domeny jest obsługiwana tylko w klastrach HDInsight opartych na systemie Linux.
     * **Wersja**: Hadoop 2.7.3 (HDI 3.5). HDInsight przyłączonych do domeny jest obsługiwana tylko w klastrze usługi HDInsight w wersji 3.5.
     * **Typ klastra**: PREMIUM
       
       Kliknij przycisk **wybierz** toosave hello zmiany.
   * **Poświadczenia**: Skonfiguruj hello poświadczenia dla użytkownika klastra hello i hello użytkownika SSH.
   * **Źródło danych**: Tworzenie nowego konta magazynu lub użyj istniejącego konta magazynu, ponieważ hello domyślne konto magazynu dla klastra usługi HDInsight hello. lokalizacji Hello musi być hello taka sama, jak Witaj dwie sieci wirtualne.  Lokalizacja Hello jest również hello lokalizację hello klastra usługi HDInsight.
   * **Cennik**: Wybierz hello liczbę węzłów procesu roboczego w klastrze.
   * **Zaawansowane konfiguracje**: 
     
     * **Sprzęganie domeny & podsieci/sieci wirtualnej**: 
       
       * **Ustawienia domeny**: 
         
         * **Nazwa domeny**: contoso.onmicrosoft.com
         * **Nazwa użytkownika domeny**: Wprowadź nazwę użytkownika domeny. Ta domena musi mieć następujące uprawnienia hello: Dołącz do domeny toohello maszyn i umieścić je w jednostce organizacyjnej hello skonfigurowane wcześniej; Tworzenie nazwy główne usług w ramach jednostki organizacyjnej hello przez skonfigurowane wcześniej; Utworzenie wpisów DNS odwrotnej. Ten użytkownik domeny będzie hello administratora klastra usługi HDInsight to przyłączonych do domeny.
         * **Hasła domeny**: Wprowadź hasło użytkownika domeny hello.
         * **Jednostka organizacyjna**: Wprowadź nazwę wyróżniającą hello hello jednostki Organizacyjnej, który został wcześniej skonfigurowany. Na przykład: OU = HDInsightOU, DC = contoso, DC = onmicrosoft, DC = com
         * **Adres URL LDAPS**: ldaps://contoso.onmicrosoft.com:636
         * **Grupy użytkowników dostępu**: Określ hello grupy zabezpieczeń użytkownicy, których ma toosync toohello klastra. Na przykład HiveUsers.
           
           Kliknij przycisk **wybierz** toosave hello zmiany.
           
           ![Portal usługi HDInsight przyłączonych do domeny skonfiguruj ustawienia domeny](./media/hdinsight-domain-joined-configure/hdinsight-domain-joined-portal-domain-setting.png)
       * **Sieć wirtualna**: contosohdivnet
       * **Podsieci**: podsieć1
         
         Kliknij przycisk **wybierz** toosave hello zmiany.        
         Kliknij przycisk **wybierz** toosave hello zmiany.
   * **Grupa zasobów**: grupy zasobów wybierz hello używany dla hello HDInsight sieciami wirtualnymi (contosohdirg).
4. Kliknij przycisk **Utwórz**.  

Inną opcją w przypadku tworzenia klastra usługi HDInsight z przyłączonych do domeny jest toouse zarządzania zasobami Azure szablonu. Witaj procedury przedstawiono sposób:

**toocreate przyłączonych do domeny klastra usługi HDInsight przy użyciu szablonu zarządzanie zasobami**

1. Kliknij przycisk powitania po tooopen obrazu szablonu usługi Resource Manager w hello portalu Azure. Szablon usługi Resource Manager Hello znajduje się w publicznym kontenerze obiektów blob. 
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-domain-joined-hdinsight-cluster.json" target="_blank"><img src="./media/hdinsight-domain-joined-configure-use-powershell/deploy-to-azure.png" alt="Deploy tooAzure"></a>
2. Z hello **parametry** bloku, wprowadź hello następujące wartości:
   
   * **Subskrypcja**: (Wybierz subskrypcję platformy Azure).
   * **Grupa zasobów**: kliknij **Użyj istniejącego**i określ hello tej samej grupie zasobów, które były używane.  Na przykład contosohdirg. 
   * **Lokalizacja**: Określ lokalizacja grupy zasobów.
   * **Nazwa klastra**: Wprowadź nazwę klastra usługi Hadoop hello, która zostanie utworzona. Na przykład contosohdicluster.
   * **Typ klastra**: Wybierz typ klastra.  Witaj, wartość domyślna to **hadoop**.
   * **Lokalizacja**: Wybierz lokalizację dla hello klastra.  Witaj domyślne konto magazynu, używa hello tej samej lokalizacji.
   * **Liczba węzłów procesu roboczego klastra**: Wybierz hello liczba węzłów procesu roboczego.
   * **Nazwa logowania i hasło klastra**: hello domyślna nazwa logowania jest **admin**.
   * **Nazwa użytkownika SSH i hasło**: hello domyślna nazwa użytkownika to **sshuser**.  Tę nazwę można zmienić. 
   * **Identyfikator sieci wirtualnej**: /subscriptions/&lt;identyfikator subskrypcji > /resourceGroups/&lt;ResourceGroupName > /providers/Microsoft.Network/virtualNetworks/&lt;VNetName >
   * **Podsieci sieci wirtualnej**: /subscriptions/&lt;identyfikator subskrypcji > /resourceGroups/&lt;ResourceGroupName > /providers/Microsoft.Network/virtualNetworks/&lt;VNetName >/podsieci/podsieć1
   * **Nazwa domeny**: contoso.onmicrosoft.com
   * **DN jednostkę organizacji**: jednostki Organizacyjnej = HDInsightOU, DC = contoso, DC = onmicrosoft, DC = com
   * **Grupa użytkowników klastra D Ns**: "\"CN HiveUsers, OU = AADDC użytkownicy, DC = =<DomainName>, DC = onmicrosoft, DC = com\""
   * **LDAPUrls**: ["ldaps://contoso.onmicrosoft.com:636"]
   * **DomainAdminUserName**: (wprowadź hello domeny nazwa użytkownika administratora)
   * **DomainAdminPassword**: (Wprowadź hasło użytkownika Administrator domeny hello)
   * **Zgadzam się toohello warunki i postanowienia, o których wspomniano**: (Sprawdź)
   * **Numer PIN toodashboard**: (Sprawdź)
3. Kliknij pozycję **Kup**. Zobaczysz nowy kafelek zatytułowany **Wdrażanie szablonu wdrożenia**. Trwa około 20 minut toocreate klastra. Po utworzeniu klastra hello, możesz kliknąć hello bloku klastra w portalu tooopen hello go.

Po ukończeniu samouczka hello można toodelete hello klastra. Dzięki usłudze HDInsight dane są przechowywane w usłudze Azure Storage, więc można bezpiecznie usunąć klaster, gdy nie jest używany. Opłaty za klaster usługi HDInsight są naliczane nawet wtedy, gdy nie jest używany. Ponieważ hello opłaty za klaster hello są wielokrotnie większe niż hello opłaty za magazyn, warto gospodarczego toodelete klastrów, gdy nie są używane. Witaj instrukcje dotyczące usuwania klastra znajdują się [klastrów zarządzania Hadoop w usłudze HDInsight przy użyciu hello portalu Azure](hdinsight-administer-use-management-portal.md#delete-clusters).

## <a name="next-steps"></a>Następne kroki

* Aby znaleźć informacje na temat konfigurowania zasad Hive i uruchamiania kwerend Hive, zobacz [Konfigurowanie zasad usługi Hive dla przyłączonych do domeny klastrów usługi HDInsight](hdinsight-domain-joined-run-hive.md).
* Uzyskać przy użyciu tooconnect SSH przyłączone tooDomain klastrów usługi HDInsight, zobacz [używanie SSH z usługą HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md#domainjoined).

