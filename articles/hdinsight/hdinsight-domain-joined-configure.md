---
title: "klastry HDInsight przyłączonych do domeny aaaConfigure - Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooset Konfigurowanie i konfigurować klastry HDInsight przyłączonych do domeny"
services: hdinsight
documentationcenter: 
author: saurinsh
manager: jhubbard
editor: cgronlun
tags: 
ms.assetid: 0cbb49cc-0de1-4a1a-b658-99897caf827c
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 11/02/2016
ms.author: saurinsh
ms.openlocfilehash: 8c4b3d269a7662d27a49b839e5cd05a3e24f7023
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-domain-joined-hdinsight-clusters-preview"></a>Konfigurowanie klastrów HDInsight przyłączonych do domeny (wersja zapoznawcza)

Dowiedz się, jak klastra tooset zapasowej Azure HDInsight z usługą Azure Active Directory (Azure AD) i [zakres Apache](http://hortonworks.com/apache/ranger/) tootake zaletą silnego uwierzytelniania i zasady kontroli (RBAC) sformatowany dostępu opartej na rolach.  HDInsight przyłączonych do domeny można skonfigurować tylko w klastrach opartych na systemie Linux. Aby uzyskać więcej informacji, zobacz [klastrów HDInsight przyłączonych do domeny wprowadź](hdinsight-domain-joined-introduction.md).

> [!IMPORTANT]
> Oozie nie jest włączona w usłudze HDInsight z przyłączonych do domeny.

W tym artykule jest pierwszy samouczek hello serii:

* Utwórz tooAzure klastra połączone HDInsight AD (przy użyciu funkcji usług domenowych Azure Directory hello) z zakres Apache włączone.
* Tworzenie i stosowanie zasad Hive za pośrednictwem zakres Apache oraz użytkownicy (na przykład analityków danych) tooHive tooconnect przy użyciu narzędzia oparte na ODBC, na przykład programu Excel, Tableau itp. Firma Microsoft pracuje wkrótce Dodawanie innych obciążeń, takich jak bazy danych HBase, Spark i Storm, tooDomain przyłączonych do usługi HDInsight.

Przykład topologii końcowego hello wygląda następująco:

![Topologia HDInsight przyłączonych do domeny](./media/hdinsight-domain-joined-configure/hdinsight-domain-joined-topology.png)

Ponieważ aktualnie usługi Azure AD obsługuje tylko klasycznych sieci wirtualnych (sieci wirtualne) i opartych na systemie Linux klastrów usługi HDInsight obsługują tylko usługi Azure Resource Manager na podstawie sieci wirtualnych, integracja HDInsight usługi Azure AD wymaga dwóch sieci wirtualnych i komunikacji równorzędnej między nimi. Uzyskać hello porównanie między hello dwa modele wdrażania, zobacz [usługi Azure Resource Manager, a wdrożenie klasyczne: zrozumienie modele wdrażania i stan zasobów hello](../azure-resource-manager/resource-manager-deployment-model.md). Witaj dwie sieci wirtualne muszą znajdować się w hello tego samego regionu hello Azure usług AD DS.

Musi być globalnie unikatowe nazwy usługi Azure. następujące nazwy Hello są używane w tym samouczku. Firma Contoso używa nazwy fikcyjne. Należy zastąpić *contoso* o innej nazwie podczas wykonywania kroków samouczka hello. 

**Nazwy:**

| Właściwość | Wartość |
| --- | --- |
| Azure AD sieci wirtualnej |contosoaadvnet |
| Grupy zasobów w usłudze Azure AD w sieci wirtualnej |contosoaadrg |
| Katalog usługi Azure AD |contosoaaddirectory |
| Nazwa domeny w usłudze Azure AD |Contoso (contoso.onmicrosoft.com) |
| HDInsight sieci wirtualnej |contosohdivnet |
| Grupa zasobów usługi HDInsight w sieci wirtualnej |contosohdirg |
| Klaster usługi HDInsight |contosohdicluster |

W tym samouczku instrukcje hello konfigurowania klastra usługi HDInsight przyłączonych do domeny. Każda sekcja zawiera artykuły tooother łącza z dodatkowymi informacjami tła.

## <a name="prerequisite"></a>Wymaganie wstępne:
* Zapoznaj się z [usług domenowych Azure AD](https://azure.microsoft.com/services/active-directory-ds/) jej [cennik](https://azure.microsoft.com/pricing/details/active-directory-ds/) struktury.
* Upewnij się, że Twoja subskrypcja jest białej dla tej publicznej wersji zapoznawczej. Możesz to zrobić, wysyłając wiadomość e-mail toohdipreview@microsoft.com z identyfikatorem subskrypcji
* Certyfikat SSL, który jest podpisany przez urząd podpisywania dla domeny. Witaj certyfikat jest wymagany przez skonfigurowanie bezpiecznego protokołu LDAP. Nie można używać certyfikatów z podpisem własnym.

## <a name="procedures"></a>Procedury
1. Utwórz sieć wirtualną platformy Azure classic usługi Azure AD.  
2. Tworzenie i konfigurowanie usługi Azure AD i Azure AD DS.
3. Tworzenie sieci wirtualnej usługi HDInsight w trybie zarządzania hello zasobów platformy Azure.
4. Równorzędnej Witaj dwie sieci wirtualne.
5. Tworzenie klastra usługi HDInsight.

> [!NOTE]
> Ten samouczek zakłada, że nie masz usługi Azure AD. Jeśli masz, możesz pominąć części hello w kroku 2.
> 
> 

Brak skrypt programu PowerShell, który zautomatyzuje kroki od 3 do 7.  Aby uzyskać więcej informacji, zobacz [klastrów HDInsight przyłączonych do domeny skonfiguruj przy użyciu programu Azure PowerShell](hdinsight-domain-joined-configure-use-powershell.md).

## <a name="create-an-azure-virtual-network-classic"></a>Tworzenie sieci wirtualnej platformy Azure (klasyczne)
W tej sekcji utworzysz sieć wirtualną (klasyczne) przy użyciu hello portalu Azure. W następnej sekcji hello zostanie włączone dla usługi Azure AD w sieci wirtualnej hello hello Azure usług AD DS. Aby uzyskać więcej informacji na temat hello procedury i przy użyciu innych metod tworzenia sieci wirtualnej, zobacz [tworzenie sieci wirtualnej (wdrożenia klasyczne) przy użyciu portalu Azure hello](../virtual-network/virtual-networks-create-vnet-classic-pportal.md).

**toocreate klasycznej sieci wirtualnej**

1. Zaloguj się na toohello [portalu Azure](https://portal.azure.com). 
2. Kliknij przycisk **nowe** > **sieci** > **sieci wirtualnej**.
3. W **wybierz model wdrożenia**, wybierz pozycję **klasycznego**, a następnie kliknij przycisk **Utwórz**.
4. Wprowadź lub wybierz hello następujące wartości:
   
   * **Nazwa**: contosoaadvnet
   * **Przestrzeń adresowa**: 10.1.0.0/16
   * **Nazwa podsieci**: podsieć1
   * **Zakres adresów podsieci**: 10.1.0.0/24
   * **Subskrypcja**: (Wybierz subskrypcję, używane podczas tworzenia tej sieci wirtualnej).
   * **Grupa zasobów**: contosoaadrg
   * **Lokalizacja**: (Wybierz region dla klastra usługi HDInsight).
     
     > [!IMPORTANT]
     > Musisz wybrać lokalizację, która obsługuje usługi Azure AD DS. Aby uzyskać więcej informacji, zobacz [Dostępność produktów według regionów](https://azure.microsoft.com/en-us/regions/services/). 
     > 
     > Zarówno hello klasycznej sieci wirtualnej i hello grupy zasobów w sieci wirtualnej muszą być pisane hello tego samego regionu hello Azure usług AD DS.
     > 
     > 
5. Kliknij przycisk **Utwórz** hello toocreate sieci wirtualnej.

## <a name="create-and-configure-azure-ad-ds-for-your-azure-ad"></a>Tworzenie i konfigurowanie usługi Azure AD DS dla usługi Azure AD
W tej sekcji obejmują:

1. Tworzenie usługi Azure AD.
2. Tworzenie użytkowników usługi Azure AD. Ci użytkownicy są użytkownikami domeny. Pierwszy użytkownik hello możesz użyć do skonfigurowania klastra usługi HDInsight hello z hello Azure AD.  Witaj innych dwóch użytkowników są opcjonalne, w tym samouczku. Będą one używane w [Hive skonfigurować zasady dla przyłączonych do domeny w usłudze hdinsight](hdinsight-domain-joined-run-hive.md) podczas konfigurowania zasad Apache zakres.
3. Utwórz grupę Administratorzy kontrolera domeny usługi AAD hello i Dodaj grupę toohello użytkowników usługi Azure AD hello. Możesz użyć tego użytkownika toocreate hello jednostki organizacyjnej.
4. Korzystanie z usług domenowych Azure AD (Azure AD DS) dla hello Azure AD.
5. Skonfiguruj LDAPS hello Azure AD. Witaj dostępu protokołu LDAP (Lightweight Directory) jest używane tooread z i zapisu tooAzure AD.

Jeśli wolisz toouse do istniejącej usługi Azure AD, można pominąć kroki 1 i 2.

**toocreate usługi Azure AD**

1. Z hello [klasycznego portalu Azure](https://manage.windowsazure.com), kliknij przycisk **nowy** > **usługi aplikacji** > **usługi Active Directory**  >  **Katalogu** > **Utwórz niestandardowy**. 
2. Wprowadź lub wybierz hello następujące wartości:
   
   * **Nazwa**: contosoaaddirectory
   * **Nazwa domeny**: contoso.  Ta nazwa musi być globalnie unikatowa.
   * **Kraj lub region**: Wybierz kraj lub region.
3. Kliknij przycisk **Complete** (Zakończ).

**Utwórz użytkownika usługi Azure AD**

1. Z hello [klasycznego portalu Azure](https://manage.windowsazure.com), kliknij przycisk **usługi Active Directory** -> **contosoaaddirectory**. 
2. Kliknij przycisk **użytkowników** z górnego menu hello.
3. Kliknij przycisk **dodać użytkownika**.
4. Wprowadź **nazwy użytkownika**, a następnie kliknij przycisk **dalej**. 
5. Konfigurowanie profilu użytkownika; W **roli**, wybierz pozycję **administratora globalnego**; a następnie kliknij przycisk **dalej**.  Rola administratora globalnego Hello jest wymagane toocreate jednostek organizacyjnych.
6. Kliknij przycisk **Utwórz** tooget hasło tymczasowe.
7. Utwórz kopię hello hasło, a następnie kliknij przycisk **Complete**. W dalszej części tego samouczka użyjesz tego klastra usługi HDInsight hello toocreate administratora globalnego użytkownika.

Wykonaj hello tej samej procedury toocreate dwóch dodatkowych użytkowników z hello **użytkownika** roli, hiveuser1 i hiveuser2. Witaj następujący użytkownicy będą używane w [Hive skonfigurować zasady dla przyłączonych do domeny w usłudze hdinsight](hdinsight-domain-joined-run-hive.md).

**toocreate hello grupy Administratorzy kontrolera domeny usługi AAD, a następnie dodaj użytkownika usługi Azure AD**

1. Z hello [klasycznego portalu Azure](https://manage.windowsazure.com), kliknij przycisk **usługi Active Directory** > **contosoaaddirectory**. 
2. Kliknij przycisk **grup** z górnego menu hello.
3. Kliknij przycisk **Dodaj grupę** lub **Dodaj grupę**.
4. Wprowadź lub wybierz hello następujące wartości:
   
   * **Nazwa**: Administratorzy kontrolera domeny usługi AAD.  Nie zmieniaj nazwy grupy hello.
   * **Typ grupy**: zabezpieczeń.
5. Kliknij przycisk **Complete** (Zakończ).
6. Kliknij przycisk **Administratorzy kontrolera domeny usługi AAD** tooopen hello grupy.
7. Kliknij przycisk **dodawać członków**.
8. Wybierz pierwszy użytkownik hello utworzony w poprzednim kroku hello, a następnie kliknij przycisk **Complete**.
9. Hello powtarzania tej samej czynności toocreate inną grupę o nazwie **HiveUsers**, i Dodaj grupę toohello użytkowników Hive hello dwa.

Aby uzyskać więcej informacji, zobacz [usług domenowych Azure AD (wersja zapoznawcza) — tworzenie hello "Administratorzy usługi AAD kontrolera domeny" grupy](../active-directory-domain-services/active-directory-ds-getting-started.md).

**tooenable usługi Azure AD DS dla usługi Azure AD**

1. Z hello [klasycznego portalu Azure](https://manage.windowsazure.com), kliknij przycisk **usługi Active Directory** > **contosoaaddirectory**. 
2. Kliknij przycisk **Konfigurowanie** z górnego menu hello.
3. Przewiń w dół za**usług domenowych w usłudze**, i hello ustaw następujące wartości:
   
   * **Włączyć usługi domenowe dla tego katalogu**: tak.
   * **Nazwa domeny DNS, usług domenowych**: Pokazuje hello domyślną nazwę DNS hello katalogu platformy Azure. Na przykład: contoso.onmicrosoft.com.
   * **Połączenie wirtualnej sieci toothis usług domenowych**: Wybierz hello klasycznej sieci wirtualnej został utworzony wcześniej, tj. **contosoaadvnet**.
4. Kliknij przycisk **zapisać** od dołu hello hello strony. Zobaczysz **oczekujących...**  dalej zbyt**włączyć usługi domenowe dla tego katalogu**.  
5. Poczekaj na **oczekujących...**  znika, i **adres IP** pobiera wypełnione. Dwa adresy IP zostanie wypełniony. Są to adresy IP hello kontrolerów domeny hello udostępniane przez usługi domenowe. Każdy adres IP będą widoczne po hello odpowiedniego kontrolera domeny jest inicjowana i gotowe. Zapisz hello dwa adresy IP. Będą Ci potrzebne później.

Aby uzyskać więcej informacji, zobacz [usług domenowych Azure AD (wersja zapoznawcza) — usługi domenowe AD Azure włączyć](../active-directory-domain-services/active-directory-ds-getting-started-enableaadds.md).

**hasło toosynchronize**

Jeśli używasz własnej domeny, należy toosynchronize hello hasła. Zobacz [Włączanie usług domenowych tooAzure AD synchronizacji haseł dla tylko w chmurze platformy Azure AD directory](../active-directory-domain-services/active-directory-ds-getting-started-password-sync.md).

**tooconfigure LDAPS dla hello Azure AD**

1. Pobierz certyfikat SSL podpisany przez urząd podpisywania dla danej domeny. Jeśli chcesz toouse certyfikatu z podpisem własnym, proszę dotrzeć toohdipreview@microsoft.com dla wyjątku.
2. Z hello [klasycznego portalu Azure](https://manage.windowsazure.com), kliknij przycisk **usługi Active Directory** > **contosoaaddirectory**. 
3. Kliknij przycisk **Konfigurowanie** z górnego menu hello.
4. Przewiń zbyt**usług domenowych w usłudze**.
5. Kliknij przycisk **Konfigurowanie certyfikatu**.
6. Wykonaj hello instrukcji toospecify hello certyfikatu i hasła hello. Zobaczysz **oczekujących...**  dalej zbyt**włączyć usługi domenowe dla tego katalogu**.  
7. Poczekaj na **oczekujących...**  znika, i **certyfikatu bezpiecznego LDAP** otrzymano wypełnione.  To może potrwać 10 minut lub dłużej.

> [!NOTE]
> Jeśli niektóre zadania w tle są uruchomione na hello Azure usług AD DS, może zostać wyświetlony błąd podczas przekazywania certyfikat — <i>jest operacja wykonywana dla tej dzierżawy. Spróbuj ponownie później</i>.  W przypadku, gdy wystąpi błąd, spróbuj ponownie za jakiś czas. druga domena Hello IP kontrolera może trwać toobe godziny too3 udostępnione.
> 
> 

Aby uzyskać więcej informacji, zobacz [skonfigurować bezpiecznego protokołu LDAP (LDAPS) dla usługi domenowe Azure AD zarządzane domeny](../active-directory-domain-services/active-directory-ds-admin-guide-configure-secure-ldap.md).

## <a name="create-a-resource-manager-vnet-for-hdinsight-cluster"></a>Tworzenie sieci wirtualnej Menedżera zasobów dla klastra usługi HDInsight
W tej sekcji utworzysz sieć wirtualną Menedżera zasobów Azure, która będzie służyć do klastra usługi HDInsight hello. Aby uzyskać więcej informacji na temat tworzenia sieci Wirtualnej platformy Azure przy użyciu innych metod, zobacz [tworzenie sieci wirtualnej](../virtual-network/virtual-networks-create-vnet-arm-pportal.md)

Po utworzeniu sieci wirtualnej hello, skonfiguruj hello toouse Menedżera zasobów w sieci wirtualnej hello tego samego serwerów DNS jako hello Azure AD w sieci wirtualnej. Po wykonaniu kroków tego samouczka toocreate hello hello klasyczną sieć wirtualną i hello Azure AD, serwery DNS hello są 10.1.0.4 i 10.1.0.5.

**toocreate Menedżera zasobów sieci wirtualnej**

1. Zaloguj się na toohello [portalu Azure](https://portal.azure.com).
2. Kliknij przycisk **nowy**, **sieci**, a następnie **sieci wirtualnej**. 
3. W **wybierz model wdrożenia**, wybierz pozycję **Resource Manager**, a następnie kliknij przycisk **Utwórz**.
4. Wpisz lub wybierz hello następujące wartości:
   
   * **Nazwa**: contosohdivnet
   * **Przestrzeń adresowa**: 10.2.0.0/16. Upewnij się, że zakres adresów hello nie może nakładać się z zakresem adresów IP hello hello klasycznej sieci wirtualnej.
   * **Nazwa podsieci**: podsieć1
   * **Zakres adresów podsieci**: 10.2.0.0/24
   * **Subskrypcja**: (Wybierz subskrypcję platformy Azure).
   * **Grupa zasobów**: contosohdirg
   * **Lokalizacja**: (Wybierz hello tej samej lokalizacji, ponieważ hello Azure AD VNet, np. contosoaadvnet.)
5. Kliknij przycisk **Utwórz**.

**tooconfigure DNS dla hello Menedżera zasobów w sieci wirtualnej**

1. Z hello [portalu Azure](https://portal.azure.com), kliknij przycisk **więcej usług** -> **sieci wirtualnych**. Upewnij się, nie tooclick **sieci wirtualnych (klasyczne)**.
2. Kliknij przycisk **contosohdivnet**.
3. Kliknij przycisk **serwerów DNS** z powitania po lewej stronie powitania nowy blok.
4. Kliknij przycisk **niestandardowe**, a następnie wprowadź hello następujące wartości:
   
   * 10.1.0.4
   * 10.1.0.5
     
     Te adresy IP serwera DNS muszą być zgodne toohello serwerów DNS w hello sieć wirtualną Azure AD (VNet klasycznego).
5. Kliknij pozycję **Zapisz**.

## <a name="peer-hello-azure-ad-vnet-and-hello-hdinsight-vnet"></a>Elementy równorzędne hello Azure AD w sieci wirtualnej i hello HDInsight sieci wirtualnej
**toopeer Witaj dwie sieci wirtualnej**

1. Zaloguj się na toohello [portalu Azure](https://portal.azure.com).
2. Kliknij przycisk **więcej usług** z menu po lewej stronie powitania.
3. Kliknij przycisk **sieci wirtualnych**. Nie klikaj pozycji **sieci wirtualnych (klasyczne)**.
4. Kliknij przycisk **contosohdivnet**.  Jest to hello HDInsight sieci wirtualnej.
5. Kliknij przycisk **komunikacji równorzędnych** menu po lewej stronie powitania hello bloku.
6. Kliknij przycisk **Dodaj** z górnego menu hello. Spowoduje to otwarcie hello **dodać równorzędna** bloku.
7. Na powitania **równorzędna Dodaj** bloku, hello ustawiona lub wybierz następujące wartości:
   
   * **Nazwa**: ContosoAADHDIVNetPeering
   * **Model wdrażania sieci wirtualnej**: klasycznym
   * **Subskrypcja**: Wybierz nazwę subskrypcji używane hello klasyczny (Azure AD) w sieci wirtualnej.
   * **Sieć wirtualna**: contosoaadvnet.
   * **Zezwalaj na dostęp do sieci wirtualnej**: (Sprawdź)
   * **Zezwalaj na związanego z przekazywaniem ruchu**: (Sprawdź). Nie zaznaczaj hello innych dwa pola wyboru.
8. Kliknij przycisk **OK**.

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
     * **Wersja**: HDI 3,6. HDInsight przyłączonych do domeny jest obsługiwana tylko w klastrze usługi HDInsight w wersji 3,6.
     * **Typ klastra**: PREMIUM
       
       Kliknij przycisk **wybierz** toosave hello zmiany.
   * **Poświadczenia**: Skonfiguruj hello poświadczenia dla użytkownika klastra hello i hello użytkownika SSH.
   * **Źródło danych**: Tworzenie nowego konta magazynu lub użyj istniejącego konta magazynu, ponieważ hello domyślne konto magazynu dla klastra usługi HDInsight hello. lokalizacji Hello musi być hello taka sama, jak Witaj dwie sieci wirtualne.  Lokalizacja Hello jest również hello lokalizację hello klastra usługi HDInsight.
   * **Cennik**: Wybierz hello liczbę węzłów procesu roboczego w klastrze.
   * **Zaawansowane konfiguracje**: 
     
     * **Sprzęganie domeny & podsieci/sieci wirtualnej**: 
       
       * **Ustawienia domeny**: 
         
         * **Nazwa domeny**: contoso.onmicrosoft.com
         * **Nazwa użytkownika domeny**: Wprowadź nazwę użytkownika domeny. Ta domena musi mieć następujące uprawnienia hello: Dołącz do domeny toohello maszyn i umieścić je w jednostce organizacyjnej hello określić podczas tworzenia klastra; Tworzenie nazwy główne usług w ramach jednostki organizacyjnej hello, które można określić podczas tworzenia klastra; Utworzenie wpisów DNS odwrotnej. Ten użytkownik domeny będzie hello administratora klastra usługi HDInsight to przyłączonych do domeny.
         * **Hasła domeny**: Wprowadź hasło użytkownika domeny hello.
         * **Jednostka organizacyjna**: Wprowadź nazwę wyróżniającą hello hello jednostek organizacyjnych, które mają toouse z klastrem usługi HDInsight. Na przykład: OU = HDInsightOU, DC = contoso, DC = onmicrosoft, DC = com. Jeśli nie istnieje tej jednostki Organizacyjnej, klaster usługi HDInsight podejmie toocreate tej jednostki Organizacyjnej. Upewnij się, hello jednostki Organizacyjnej znajduje się już lub konto domeny hello ma uprawnienia toocreate nowy. Jeśli używasz konta domeny hello, który należy do grupy administratorów AADDC ma niezbędne uprawnienia hello toocreate jednostki Organizacyjnej.
         * **Adres URL LDAPS**: ldaps://contoso.onmicrosoft.com:636
         * **Grupy użytkowników dostępu**: Określ hello grupy zabezpieczeń użytkowników, którzy mają toosync toohello klastra. Na przykład HiveUsers.
           
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
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-domain-joined-hdinsight-cluster.json" target="_blank"><img src="./media/hdinsight-domain-joined-configure/deploy-to-azure.png" alt="Deploy tooAzure"></a>
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
   * **Grupa użytkowników klastra DNs**: [\"HiveUsers\"]
   * **LDAPUrls**: ["ldaps://contoso.onmicrosoft.com:636"]
   * **DomainAdminUserName**: (wprowadź hello domeny nazwa użytkownika administratora)
   * **DomainAdminPassword**: (Wprowadź hasło użytkownika Administrator domeny hello)
   * **Zgadzam się toohello warunki i postanowienia, o których wspomniano**: (Sprawdź)
   * **Numer PIN toodashboard**: (Sprawdź)
3. Kliknij pozycję **Kup**. Zobaczysz nowy kafelek zatytułowany **Wdrażanie szablonu wdrożenia**. Trwa około 20 minut toocreate klastra. Po utworzeniu klastra hello, możesz kliknąć hello bloku klastra w portalu tooopen hello go.

Po ukończeniu samouczka hello można toodelete hello klastra. Dzięki usłudze HDInsight dane są przechowywane w usłudze Azure Storage, więc można bezpiecznie usunąć klaster, gdy nie jest używany. Opłaty za klaster usługi HDInsight są naliczane nawet wtedy, gdy nie jest używany. Ponieważ hello opłaty za klaster hello są wielokrotnie większe niż hello opłaty za magazyn, warto gospodarczego toodelete klastrów, gdy nie są używane. Witaj instrukcje dotyczące usuwania klastra znajdują się [klastrów zarządzania Hadoop w usłudze HDInsight przy użyciu hello portalu Azure](hdinsight-administer-use-management-portal.md#delete-clusters).

## <a name="next-steps"></a>Następne kroki
* Aby znaleźć informacje na temat konfigurowania zasad Hive i uruchamiania kwerend Hive, zobacz [Konfigurowanie zasad usługi Hive dla przyłączonych do domeny klastrów usługi HDInsight](hdinsight-domain-joined-run-hive.md).
* Uzyskać przy użyciu tooconnect SSH przyłączone tooDomain klastrów usługi HDInsight, zobacz [używanie SSH z opartą na systemie Linux platformą Hadoop w usłudze HDInsight z systemów Linux, Unix lub OS X](hdinsight-hadoop-linux-use-ssh-unix.md#domainjoined).

