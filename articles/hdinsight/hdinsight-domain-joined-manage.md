---
title: "klastry HDInsight przyłączonych do domeny aaaManage - Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toomanage przyłączonych do domeny klastrów usługi HDInsight"
services: hdinsight
documentationcenter: 
author: saurinsh
manager: jhubbard
editor: cgronlun
tags: 
ms.assetid: 6ebc4d2f-2f6a-4e1e-ab6d-af4db6b4c87c
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 10/25/2016
ms.author: saurinsh
ms.openlocfilehash: 233ddf0953e981f9a24b77d9dde194d590e5e6d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-domain-joined-hdinsight-clusters-preview"></a>Zarządzanie klastrami HDInsight przyłączonych do domeny (wersja zapoznawcza)
Dowiedz się hello użytkownikami i rolami hello przyłączonych do domeny usługi HDInsight i jak toomanage przyłączonych do domeny klastrów usługi HDInsight.

## <a name="users-of-domain-joined-hdinsight-clusters"></a>Użytkownicy domeny w usłudze hdinsight
Klaster usługi HDInsight, który nie jest przyłączony do domeny ma dwa konta użytkownika, które są tworzone podczas tworzenia klastra hello:

* **Administrator Ambari**: to konto jest także znana jako *użytkownika Hadoop* lub *użytkowników HTTP*. To konto może być używane toolog na tooAmbari na https://&lt;clustername >. azurehdinsight.net. On również być zapytania toorun używanych w widokach Ambari, wykonywanie zadania za pomocą narzędzia zewnętrzne (np. programu PowerShell, Templeton, Visual Studio) i uwierzytelniania za pomocą sterownika ODBC programu Hive hello i narzędzi do analizy Biznesowej (tj. Excel usługi Power Bi i Tableau).
* **Użytkownik SSH**: to konto może być używany z SSH i wykonywać polecenia sudo. Ma ona toohello uprawnienia główny maszyn wirtualnych systemu Linux.

Klaster HDInsight przyłączonych do domeny ma trzy nowych użytkowników w tooAmbari dodanie użytkownika administratora, jak i SSH.

* **Zakres admin**: to konto jest kontem administratora zakres Apache lokalne powitania. Nie jest użytkownikiem domeny usługi active directory. To konto można być toosetup używane zasady i innych użytkowników Administratorzy lub delegowani administratorzy (tak aby tym użytkownikom można zarządzać zasadami). Domyślnie nazwa użytkownika hello jest *admin* i hasło hello jest taki sam, jak hasło administratora Ambari hello hello. Witaj hasło może zostać zaktualizowana ze strony ustawień hello w zakres.
* **Użytkownik domeny administratora klastra**: jest to konto użytkownika domeny usługi active directory jako hello tym Ambari i zakres administratora klastra usługi Hadoop. Musisz podać poświadczenia użytkownika podczas tworzenia klastra. Ten użytkownik ma hello następujące uprawnienia:

  * Dołącz do domeny toohello maszyn i umieścić je w ramach hello jednostki Organizacyjnej, którą można określić podczas tworzenia klastra.
  * Utwórz jednostki usługi w ramach hello jednostki Organizacyjnej, którą można określić podczas tworzenia klastra.
  * Utworzenie wpisów DNS odwrotnej.

    Uwaga hello innych użytkowników usługi AD również mieć te uprawnienia.

    Brak niektórych punktów końcowych w ramach klastra hello (na przykład Templeton), które nie są zarządzane przez zakres i dlatego nie jest bezpieczna. Te punkty końcowe są zablokowany dla wszystkich użytkowników z wyjątkiem hello klastra Administrator domeny.
* **Regularne**: podczas tworzenia klastra, możesz podać wiele grup usługi active directory. Hello użytkownicy w tych grupach jest zsynchronizowany tooRanger i Ambari. Ci użytkownicy są użytkownicy domeny i będzie miał dostęp tooonly zarządzane zakres punktów końcowych (na przykład serwera Hiveserver2). Wszystkie hello RBAC zasad i inspekcji będą toothese odpowiednich użytkowników.

## <a name="roles-of-domain-joined-hdinsight-clusters"></a>Role z klastrów HDInsight przyłączonych do domeny
HDInsight przyłączonych do domeny mają hello następujące role:

* Administrator klastra
* Operator klastra
* Administrator usługi
* Operator usługi
* Użytkownika klastra

**uprawnienia hello toosee tych ról**

1. Otwórz hello interfejsu Ambari zarządzania użytkownika.  Zobacz [hello Otwórz interfejs użytkownika zarządzania Ambari](#open-the-ambari-management-ui).
2. W menu po lewej stronie powitania kliknij **ról**.
3. Kliknij przycisk hello niebieski znak zapytania toosee hello uprawnienia:

    ![Przyłączonych do domeny uprawnienia ról usługi HDInsight](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-roles-permissions.png)

## <a name="open-hello-ambari-management-ui"></a>Otwórz hello interfejsu użytkownika zarządzania Ambari
1. Zaloguj się na toohello [portalu Azure](https://portal.azure.com).
2. Otwórz z klastrem usługi HDInsight w bloku. Zobacz [klastrów listy i Pokaż](hdinsight-administer-use-management-portal.md#list-and-show-clusters).
3. Kliknij przycisk **pulpitu nawigacyjnego** z hello menu u góry tooopen Ambari.
4. Zaloguj się na tooAmbari przy użyciu nazwy użytkownika hello klastra administrator domeny i hasła.
5. Kliknij przycisk hello **Admin** menu rozwijane z hello prawym górnym rogu ekranu, a następnie kliknij **Zarządzanie Ambari**.

    ![HDInsight przyłączonych do domeny zarządzania Ambari](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-manage-ambari.png)

    Witaj interfejsu użytkownika wygląda następująco:

    ![Przyłączonych do domeny zarządzania HDInsight Ambari interfejsu użytkownika](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-ambari-management-ui.png)

## <a name="list-hello-domain-users-synchronized-from-your-active-directory"></a>Lista użytkowników domeny hello synchronizowane z usługi Active Directory
1. Otwórz hello interfejsu Ambari zarządzania użytkownika.  Zobacz [hello Otwórz interfejs użytkownika zarządzania Ambari](#open-the-ambari-management-ui).
2. W menu po lewej stronie powitania kliknij **użytkowników**. Zostanie wyświetlona wszyscy użytkownicy hello synchronizowane z klastrem usługi HDInsight toohello usługi Active Directory.

    ![Przyłączonych do domeny HDInsight Ambari zarządzania interfejsu użytkownika lista użytkowników](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-ambari-management-ui-users.png)

## <a name="list-hello-domain-groups-synchronized-from-your-active-directory"></a>Wyświetlanie listy grup domeny hello synchronizowane z usługi Active Directory
1. Otwórz hello interfejsu Ambari zarządzania użytkownika.  Zobacz [hello Otwórz interfejs użytkownika zarządzania Ambari](#open-the-ambari-management-ui).
2. W menu po lewej stronie powitania kliknij **grup**. Zostanie wyświetlona wszystkich grup hello synchronizowane z klastrem usługi HDInsight toohello usługi Active Directory.

    ![Przyłączonych do domeny HDInsight Ambari zarządzania interfejsu użytkownika listy grup](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-ambari-management-ui-groups.png)

## <a name="configure-hive-views-permissions"></a>Konfigurowanie uprawnień widoki Hive
1. Otwórz hello interfejsu Ambari zarządzania użytkownika.  Zobacz [hello Otwórz interfejs użytkownika zarządzania Ambari](#open-the-ambari-management-ui).
2. W menu po lewej stronie powitania kliknij **widoków**.
3. Kliknij przycisk **HIVE** tooshow hello szczegóły.

    ![Przyłączonych do domeny zarządzania HDInsight Ambari widoki Hive interfejsu użytkownika](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-ambari-management-ui-hive-views.png)
4. Kliknij przycisk hello **Hive View** link tooconfigure widoki Hive.
5. Przewiń w dół toohello **uprawnienia** sekcji.

    ![Przyłączonych do domeny zarządzania HDInsight Ambari widoki Hive interfejsu użytkownika konfigurowania uprawnień](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-ambari-management-ui-hive-views-permissions.png)
6. Kliknij przycisk **Dodaj użytkownika** lub **Dodaj grupę**, a następnie określ hello użytkowników lub grupy, które mogą używać widoki Hive.

## <a name="configure-users-for-hello-roles"></a>Konfiguruj użytkowników, ról hello
 toosee listę ról i uprawnień, zobacz [role domeny w usłudze hdinsight](#roles-of-domain---joined-hdinsight-clusters).

1. Otwórz hello interfejsu Ambari zarządzania użytkownika.  Zobacz [hello Otwórz interfejs użytkownika zarządzania Ambari](#open-the-ambari-management-ui).
2. W menu po lewej stronie powitania kliknij **ról**.
3. Kliknij przycisk **Dodaj użytkownika** lub **Dodaj grupę** ról toodifferent tooassign użytkowników i grup.

## <a name="next-steps"></a>Następne kroki
* Aby skonfigurować przyłączony do domeny klaster usługi HDInsight, zobacz [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md) (Konfigurowanie przyłączonych do domeny klastrów usługi HDInsight).
* Aby znaleźć informacje na temat konfigurowania zasad Hive i uruchamiania kwerend Hive, zobacz [Konfigurowanie zasad usługi Hive dla przyłączonych do domeny klastrów usługi HDInsight](hdinsight-domain-joined-run-hive.md).
* Do uruchamiania zapytań Hive przy użyciu protokołu SSH w klastrach HDInsight przyłączonych do domeny, zobacz [używanie SSH z usługą HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md#domainjoined).
