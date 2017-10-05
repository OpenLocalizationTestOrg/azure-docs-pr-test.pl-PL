---
title: "Korzystanie z protokołu SSH w usłudze Hadoop — Azure HDInsight | Microsoft Docs"
description: "Do usługi HDInsight można uzyskać dostęp przy użyciu protokołu Secure Shell (SSH). Ten dokument zawiera informacje dotyczące nawiązywania połączenia z usługą HDInsight przy użyciu poleceń ssh i scp z klientów systemów Windows, Linux, Unix lub macOS."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
keywords: "polecenia w usłudze hadoop w systemie linux,polecenia hadoop linux,hadoop macos,ssh hadoop,klaster ssh hadoop"
ms.assetid: a6a16405-a4a7-4151-9bbf-ab26972216c5
ms.service: hdinsight
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/03/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive,hdiseo17may2017
ms.openlocfilehash: df0feb51469333bac42c779d860192d46f24ac62
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="connect-to-hdinsight-hadoop-using-ssh"></a>Łączenie się z usługą HDInsight (Hadoop) przy użyciu protokołu SSH

Dowiedz się, jak nawiązać bezpieczne połączenie z usługą Hadoop w usłudze Azure HDInsight przy użyciu protokołu [Secure Shell (SSH)](https://en.wikipedia.org/wiki/Secure_Shell). 

Usługa HDInsight może używać systemu Linux (Ubuntu) jako systemu operacyjnego dla węzłów klastra usługi Hadoop. Poniższa tabela zawiera informacje dotyczące adresów i portów wymagane podczas nawiązywania połączenia z usługą HDInsight opartą na systemie Linux przy użyciu klienta protokołu SSH:

| Adres | Port | Element docelowy połączenia |
| ----- | ----- | ----- |
| `<clustername>-ed-ssh.azurehdinsight.net` | 22 | Węzeł krawędzi (program R Server w usłudze HDInsight) |
| `<edgenodename>.<clustername>-ssh.azurehdinsight.net` | 22 | Węzeł krawędzi (inny dowolny typ klastra, jeśli istnieje węzeł krawędzi) |
| `<clustername>-ssh.azurehdinsight.net` | 22 | Podstawowy węzeł główny |
| `<clustername>-ssh.azurehdinsight.net` | 23 | Dodatkowy węzeł główny |

> [!NOTE]
> Element `<edgenodename>` należy zastąpić nazwą węzła krawędzi.
>
> Zastąp ciąg `<clustername>` nazwą klastra.
>
> Jeśli klaster zawiera węzeł krawędzi, zalecamy, aby __zawsze łączyć się z węzłem krawędzi__ przy użyciu protokołu SSH. Węzły główne hostują usługi o krytycznym znaczeniu dla kondycji usługi Hadoop. W węźle krawędzi działają tylko obciążenia umieszczone przez użytkownika.
>
> Więcej informacji dotyczących używania węzłów krawędzi można znaleźć w temacie [Use edge nodes in HDInsight](hdinsight-apps-use-edge-node.md#access-an-edge-node) (Używanie węzłów krawędzi w usłudze HDInsight).

## <a name="ssh-clients"></a>Klienci SSH

Systemy Linux, Unix i macOS obejmują polecenia `ssh` i `scp`. Klient `ssh` jest najczęściej używany do tworzenia zdalnej sesji wiersza polecenia za pomocą systemu Linux lub Unix. Klient `scp` służy do bezpiecznego kopiowania plików między klientem użytkownika a systemem zdalnym.

System Microsoft Windows domyślnie nie udostępnia żadnych klientów SSH. Klienci `ssh` i `scp` są dostępni dla systemu Windows za pośrednictwem następujących pakietów:

* [Azure Cloud Shell](../cloud-shell/quickstart.md): usługa Cloud Shell zapewnia środowisko powłoki Bash w przeglądarce i polecenia `ssh`, `scp` oraz inne typowe polecenia systemu Linux.

* [Powłoka Bash w systemie Ubuntu w systemie Windows 10](https://msdn.microsoft.com/commandline/wsl/about): polecenia `ssh` i `scp` są dostępne za pośrednictwem powłoki Bash w wierszu polecenia systemu Windows.

* [Git (https://git-scm.com/)](https://git-scm.com/): polecenia `ssh` i `scp` są dostępne za pośrednictwem wiersza polecenia GitBash.

* [GitHub Desktop (https://desktop.github.com/)](https://desktop.github.com/) polecenia `ssh` i `scp` są dostępne za pośrednictwem wiersza polecenia powłoki GitHub Shell. W rozwiązaniu GitHub Desktop można skonfigurować wiersz polecenia dla powłoki Git Shell, wybierając funkcję Bash, wiersz polecenia systemu Windows lub program PowerShell.

* [OpenSSH (https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH)](https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH): obecnie zespół ds. programu PowerShell pracuje nad przeniesieniem pakietu OpenSSH do systemu Windows. Dodatkowo są udostępniane wersje testowe.

    > [!WARNING]
    > Pakiet OpenSSH zawiera składnik serwera SSH — `sshd`. Składnik ten pozwala uruchomić w systemie serwer SSH i umożliwia innym osobom połączenie się z tym serwerem. Nie konfiguruj tego składnika ani nie otwieraj portu 22, chyba że chcesz hostować w systemie serwer SSH. Składnik ten nie jest wymagany do komunikowania się z usługą HDInsight.

Dostępnych jest również kilka graficznych klientów SSH, takich jak [PuTTY (http://www.chiark.greenend.org.uk/~sgtatham/putty/)](http://www.chiark.greenend.org.uk/~sgtatham/putty/) i [MobaXterm (http://mobaxterm.mobatek.net/)](http://mobaxterm.mobatek.net/). Mimo że ci klienci umożliwiają nawiązywanie połączeń z usługą HDInsight, proces łączenia się jest inny niż w przypadku narzędzia `ssh`. Aby uzyskać więcej informacji, zobacz dokumentację graficznego klienta, którego używasz.

## <a id="sshkey"></a>Uwierzytelnianie: klucze SSH

Klucze SSH używają [kryptografii klucza publicznego](https://en.wikipedia.org/wiki/Public-key_cryptography) do uwierzytelnienia sesji SSH. Klucze SSH są bezpieczniejsze niż hasła i umożliwiają łatwe zabezpieczenie dostępu do klastra usługi Hadoop.

Jeśli konto SSH zostanie zabezpieczone za pomocą klucza, podczas nawiązywania połączenia klient musi podać zgodny klucz prywatny:

* Większość klientów można skonfigurować do używania __domyślnego klucza__. Na przykład w środowiskach Linux i Unix klient `ssh` szuka klucza prywatnego w lokalizacji `~/.ssh/id_rsa`.

* Można określić __ścieżkę do klucza prywatnego__. W przypadku klienta `ssh` do określenia ścieżki do klucza prywatnego służy parametr `-i`. Na przykład `ssh -i ~/.ssh/id_rsa sshuser@myedge.mycluster-ssh.azurehdinsight.net`.

* Jeśli masz __wiele kluczy prywatnych__, których używasz dla różnych serwerów, rozważ użycie takiego narzędzia jak [ssh-agent (https://en.wikipedia.org/wiki/Ssh-agent)](https://en.wikipedia.org/wiki/Ssh-agent). Narzędzie `ssh-agent` może służyć do automatycznego wybierania klucza do użycia podczas ustanawiania sesji SSH.

> [!IMPORTANT]
>
> W przypadku zabezpieczenia klucza prywatnego za pomocą hasła musisz je podać przed użyciem klucza. Takie narzędzia, jak `ssh-agent`, umożliwiają wygodne przechowywanie haseł w pamięci podręcznej.

### <a name="create-an-ssh-key-pair"></a>Tworzenie pary kluczy SSH

Do tworzenia plików klucza publicznego i prywatnego służy polecenie `ssh-keygen`. Następujące polecenie generuje parę 2048-bitowych kluczy RSA, która pozwala połączyć się z usługą HDInsight:

    ssh-keygen -t rsa -b 2048

W trakcie procesu tworzenia kluczy zostaną wyświetlone monity o podanie informacji. Mogą one dotyczyć na przykład hasła lub lokalizacji przechowywania kluczy. Po zakończeniu tego procesu zostaną utworzone dwa pliki: klucz publiczny i klucz prywatny.

* __Klucz publiczny__ służy do tworzenia klastra usługi HDInsight i ma rozszerzenie `.pub`.

* __Klucz prywatny__ służy do uwierzytelniania klienta w klastrze usługi HDInsight.

> [!IMPORTANT]
> Klucze można zabezpieczyć przy użyciu hasła. W praktyce hasłem zabezpiecza się klucz prywatny. Nawet w przypadku uzyskania klucza prywatnego przez inną osobę do jego użycia jest potrzebne hasło.

### <a name="create-hdinsight-using-the-public-key"></a>Tworzenie klastrów usługi HDInsight przy użyciu klucza publicznego

| Metoda tworzenia | Sposób użycia klucza publicznego |
| ------- | ------- |
| **Witryna Azure Portal** | Usuń zaznaczenie pola __Użyj tego samego hasła podczas logowania do klastra__, a następnie wybierz opcję __Klucz publiczny__ jako typ uwierzytelniania SSH. Na koniec wybierz plik klucza publicznego lub wklej zawartość tekstową pliku w polu __Klucz publiczny SSH__.</br>![Okno dialogowe dotyczące klucza publicznego SSH w procesie tworzenia klastra usługi HDInsight](./media/hdinsight-hadoop-linux-use-ssh-unix/create-hdinsight-ssh-public-key.png) |
| **Azure PowerShell** | Użyj parametru `-SshPublicKey` polecenia cmdlet `New-AzureRmHdinsightCluster` i przekaż zawartość klucza publicznego jako ciąg.|
| **Interfejs wiersza polecenia platformy Azure 1.0** | Użyj parametru `--sshPublicKey` polecenia `azure hdinsight cluster create` i przekaż zawartość klucza publicznego jako ciąg. |
| **Szablon usługi Resource Manager** | Przykład użycia kluczy SSH razem z szablonem można znaleźć w temacie [Deploy HDInsight on Linux with SSH key](https://azure.microsoft.com/resources/templates/101-hdinsight-linux-ssh-publickey/) (Wdrażanie usługi HDInsight w systemie Linux przy użyciu klucza SSH). Element `publicKeys` w pliku [azuredeploy.json](https://github.com/Azure/azure-quickstart-templates/blob/master/101-hdinsight-linux-ssh-publickey/azuredeploy.json) umożliwia przekazanie kluczy do platformy Azure podczas tworzenia klastra. |

## <a id="sshpassword"></a>Uwierzytelnianie: hasło

Konta SSH mogą być chronione przy użyciu hasła. Podczas łączenia się z usługą HDInsight przy użyciu protokołu SSH pojawia się monit o podanie hasła.

> [!WARNING]
> W przypadku protokołu SSH nie zalecamy korzystania z uwierzytelniania za pomocą hasła. Hasła można złamać i są one podatne na ataki siłowe. Zamiast tego zalecamy używanie [kluczy SSH w celu uwierzytelniania](#sshkey).

### <a name="create-hdinsight-using-a-password"></a>Tworzenie klastrów usługi HDInsight przy użyciu hasła

| Metoda tworzenia | Sposób określenia hasła |
| --------------- | ---------------- |
| **Azure Portal** | Domyślnie hasło do konta użytkownika SSH jest takie samo jak hasło do konta umożliwiającego logowanie do klastra. Aby użyć innego hasła, usuń zaznaczenie pola __Użyj tego samego hasła podczas logowania do klastra__, a następnie wprowadź hasło w polu __Hasło SSH__.</br>![Okno dialogowe dotyczące hasła SSH w procesie tworzenia klastra usługi HDInsight](./media/hdinsight-hadoop-linux-use-ssh-unix/create-hdinsight-ssh-password.png)|
| **Azure PowerShell** | Użyj parametru `--SshCredential` polecenia cmdlet `New-AzureRmHdinsightCluster` i przekaż obiekt `PSCredential` zawierający nazwę użytkownika i hasło do konta SSH. |
| **Interfejs wiersza polecenia platformy Azure 1.0** | Użyj parametru `--sshPassword` polecenia `azure hdinsight cluster create` i podaj hasło. |
| **Szablon usługi Resource Manager** | Przykład użycia hasła razem z szablonem można znaleźć w temacie [Deploy HDInsight on Linux with SSH password](https://azure.microsoft.com/resources/templates/101-hdinsight-linux-ssh-password/) (Wdrażanie usługi HDInsight w systemie Linux przy użyciu hasła SSH). Element `linuxOperatingSystemProfile` w pliku [azuredeploy.json](https://github.com/Azure/azure-quickstart-templates/blob/master/101-hdinsight-linux-ssh-password/azuredeploy.json) umożliwia przekazanie nazwy konta SSH i hasła do platformy Azure podczas tworzenia klastra.|

### <a name="change-the-ssh-password"></a>Zmienianie hasła SSH

Informacje dotyczące zmiany hasła użytkownika konta SSH można znaleźć w sekcji __Change passwords__ (Zmienianie haseł) dokumentu [Manage HDInsight](hdinsight-administer-use-portal-linux.md#change-passwords) (Zarządzanie usługą HDInsight).

## <a id="domainjoined"></a>Uwierzytelnianie: przyłączony do domeny klaster usługi HDInsight

Jeśli używasz __przyłączonego do domeny klastra usługi HDInsight__, po nawiązaniu połączenia przy użyciu protokołu SSH musisz uruchomić polecenie `kinit`. Spowoduje to wyświetlenie monitu o podanie nazwy użytkownika domeny i hasła oraz uwierzytelnienie sesji w domenie usługi Azure Active Directory skojarzonej z klastrem.

Aby uzyskać więcej informacji, zobacz [Configure domain-joined HDInsight](hdinsight-domain-joined-configure.md) (Konfigurowanie przyłączonej do domeny usługi HDInsight).

## <a name="connect-to-nodes"></a>Nawiązywanie połączeń z węzłami

Do węzłów głównych i węzła brzegowego (jeśli taki istnieje) można uzyskiwać dostęp za pośrednictwem Internetu przez porty 22 i 23.

* Podczas nawiązywania połączenia z __węzłami głównymi__ użyj portu __22__, aby łączyć się z podstawowym węzłem głównym, oraz portu __23__, aby łączyć się z pomocniczym węzłem głównym. W pełni kwalifikowana nazwa domeny do zastosowania to `clustername-ssh.azurehdinsight.net`, gdzie `clustername` jest nazwą Twojego klastra.

    ```bash
    # Connect to primary head node
    # port not specified since 22 is the default
    ssh sshuser@clustername-ssh.azurehdinsight.net

    # Connect to secondary head node
    ssh -p 23 sshuser@clustername-ssh.azurehdinsight.net
    ```
    
* W przypadku nawiązywania połączenia z __węzłem brzegowym__ użyj portu 22. W pełni kwalifikowana nazwa domeny to `edgenodename.clustername-ssh.azurehdinsight.net`, gdzie `edgenodename` jest nazwą podaną podczas tworzenia węzła brzegowego. `clustername` jest nazwą klastra.

    ```bash
    # Connect to edge node
    ssh sshuser@edgnodename.clustername-ssh.azurehdinsight.net
    ```

> [!IMPORTANT]
> Poprzednie przykłady zakładają, że korzystasz z uwierzytelniania przy użyciu hasła lub że uwierzytelnianie certyfikatu odbywa się automatycznie. Jeśli korzystasz z pary kluczy SSH do uwierzytelniania, a certyfikat nie jest używany automatycznie, skorzystaj z parametru `-i`, aby określić klucz prywatny. Na przykład `ssh -i ~/.ssh/mykey sshuser@clustername-ssh.azurehdinsight.net`.

Po nawiązaniu połączenia wiersz polecenia zmieni się, aby wskazać nazwę użytkownika SSH i węzeł, z którym nawiązano połączenie. Na przykład w przypadku połączenia z podstawowym węzłem głównym jako użytkownik `sshuser` wiersz polecenia będzie wyglądać następująco: `sshuser@hn0-clustername:~$`.

### <a name="connect-to-worker-and-zookeeper-nodes"></a>Łączenie się z węzłami procesu roboczego i węzłami dozorcy

Węzły procesu roboczego i węzły dozorcy nie są dostępne bezpośrednio z Internetu. Można uzyskać do nich dostęp z węzłów głównych lub węzłów krawędzi klastra. Poniżej przedstawiono ogólny zarys czynności, które należy wykonać w celu nawiązania połączenia z innymi węzłami:

1. Połącz się z węzłem głównym lub węzłem krawędzi za pomocą protokołu SSH:

        ssh sshuser@myedge.mycluster-ssh.azurehdinsight.net

2. Z poziomu połączenia SSH z węzłem głównym lub węzłem krawędzi połącz się z węzłem procesu roboczego w klastrze za pomocą polecenia `ssh`:

        ssh sshuser@wn0-myhdi

    Aby pobrać listę nazw domen węzłów w klastrze, zobacz artykuł [Manage HDInsight by using the Ambari REST API](hdinsight-hadoop-manage-ambari-rest-api.md#example-get-the-fqdn-of-cluster-nodes) (Zarządzanie usługą HDInsight przy użyciu interfejsu API REST Ambari).

Jeśli konto SSH jest zabezpieczone przy użyciu __hasła__, wprowadź hasło podczas nawiązywania połączenia.

Jeśli konto SSH jest zabezpieczone przy użyciu __kluczy SSH__, upewnij się, że na kliencie jest włączone przekazywanie SSH.

> [!NOTE]
> Innym sposobem uzyskiwania bezpośredniego dostępu do wszystkich węzłów w klastrze jest zainstalowanie usługi HDInsight w usłudze Azure Virtual Network. Pozwoli to na przyłączenie komputera zdalnego do tej samej sieci wirtualnej i uzyskiwanie bezpośredniego dostępu do wszystkich węzłów w klastrze.
>
> Aby uzyskać więcej informacji, zobacz [Use a virtual network with HDInsight](hdinsight-extend-hadoop-virtual-network.md) (Używanie sieci wirtualnej z usługą HDInsight).

### <a name="configure-ssh-agent-forwarding"></a>Konfigurowanie przekazywania przez agenta SSH

> [!IMPORTANT]
> W poniższej procedurze założono korzystanie z systemu opartego na systemie Linux lub UNIX, ale działa ona również w przypadku powłoki Bash w systemie Windows 10. Jeśli te czynności nie działają w Twoim systemie, zapoznaj się z dokumentacją używanego klienta SSH.

1. Za pomocą edytora tekstów otwórz plik `~/.ssh/config`. Jeśli ten plik nie istnieje, możesz go utworzyć, wprowadzając polecenie `touch ~/.ssh/config` w wierszu polecenia.

2. Dodaj następujący tekst do pliku `config`.

        Host <edgenodename>.<clustername>-ssh.azurehdinsight.net
          ForwardAgent yes

    Informacje w sekcji __Host__ zastąp adresem węzła, z którym łączysz się przy użyciu protokołu SSH. W poprzednim przykładzie użyto węzła krawędzi. Wpis ten umożliwia skonfigurowanie przekazywania przez agenta SSH dla określonego węzła.

3. Przetestuj agenta przekazywania SSH za pomocą następującego polecenia z terminala:

        echo "$SSH_AUTH_SOCK"

    To polecenie zwraca informacje podobne do następującego tekstu:

        /tmp/ssh-rfSUL1ldCldQ/agent.1792

    Jeśli nie zostaną zwrócone żadne informacje, oznacza to, że agent `ssh-agent` nie działa. Aby dowiedzieć się więcej, zapoznaj się z informacjami na temat skryptów uruchamiania agenta na stronie [Using ssh-agent with ssh (http://mah.everybody.org/docs/ssh)](http://mah.everybody.org/docs/ssh) (Korzystanie z agenta SSH z protokołem SSH) lub z dokumentacją używanego klienta SSH.

4. Po upewnieniu się, że program **ssh-agent** działa, należy wykonać następujące czynności, aby dodać klucz prywatny SSH do agenta:

        ssh-add ~/.ssh/id_rsa

    Jeśli klucz prywatny jest przechowywany w innym pliku, zastąp `~/.ssh/id_rsa` ścieżką do pliku.

5. Połącz się z węzłem krawędzi lub węzłami głównymi klastra przy użyciu protokołu SSH. Następnie połącz się z węzłem procesu roboczego lub węzłem dozorcy przy użyciu polecenia SSH. Połączenie zostanie nawiązane przy użyciu przekazanego klucza.

## <a name="copy-files"></a>Kopiowanie plików

Narzędzia `scp` można użyć do kopiowania plików do i z poszczególnych węzłów w klastrze. Na przykład następujące polecenie kopiuje katalog `test.txt` z systemu lokalnego do podstawowego węzła głównego:

```bash
scp test.txt sshuser@clustername-ssh.azurehdinsight.net:
```

Ponieważ po znaku `:` nie określono ścieżki, plik zostanie umieszczony w katalogu macierzystym użytkownika `sshuser`.

Poniższy przykład kopiuje plik `test.txt` z katalogu macierzystego użytkownika `sshuser` w podstawowym węźle głównym do systemu lokalnego:

```bash
scp sshuser@clustername-ssh.azurehdinsight.net:test.txt .
```

> [!IMPORTANT]
> Narzędzie `scp` może uzyskać dostęp tylko do systemu plików poszczególnych węzłów w klastrze. Nie może zostać użyte w celu uzyskania dostępu do danych w magazynie zgodnym z systemem HDFS dla klastra.
>
> Użyj narzędzia `scp`, jeśli musisz przekazać zasób do użycia z sesji SSH. Na przykład przekaż skrypt języka Python, a następnie uruchom go z sesji SSH.
>
> Aby uzyskać informacje o bezpośrednim ładowaniu danych do magazynu zgodnego z systemem HDFS, zobacz następujące dokumenty:
>
> * [Usługa HDInsight korzystająca z usługi Azure Storage](hdinsight-hadoop-use-blob-storage.md).
>
> * [Usługa HDInsight korzystająca z usługi Azure Data Lake Store](hdinsight-hadoop-use-data-lake-store.md).

## <a name="next-steps"></a>Następne kroki

* [Use SSH tunneling with HDInsight](hdinsight-linux-ambari-ssh-tunnel.md) (Używanie tunelowania SSH z usługą HDInsight)
* [Use a virtual network with HDInsight](hdinsight-extend-hadoop-virtual-network.md) (Używanie sieci wirtualnej z usługą HDInsight)
* [Use edge nodes in HDInsight](hdinsight-apps-use-edge-node.md#access-an-edge-node) (Używanie węzłów krawędzi w usłudze HDInsight)