---
title: "aaaUse SSH z usługą Hadoop - Azure HDInsight | Dokumentacja firmy Microsoft"
description: "Do usługi HDInsight można uzyskać dostęp przy użyciu protokołu Secure Shell (SSH). Ten dokument zawiera informacje dotyczące łączenia z klientów systemu Windows, Linux, Unix lub macOS tooHDInsight przy użyciu hello ssh i scp poleceń."
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
ms.openlocfilehash: ac9e70ce3c70693c1b81c9514ba4fd47686070ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-toohdinsight-hadoop-using-ssh"></a>Połącz tooHDInsight (Hadoop) przy użyciu protokołu SSH

Dowiedz się, jak toouse [Secure Shell (SSH)](https://en.wikipedia.org/wiki/Secure_Shell) toosecurely połączyć tooHadoop w usłudze Azure HDInsight. 

HDInsight można użyć jako system operacyjny hello systemu Linux (Ubuntu) dla węzłów w klastrze Hadoop hello. Witaj Poniższa tabela zawiera informacje adres i port hello potrzebne podczas nawiązywania połączenia na podstawie tooLinux HDInsight przy użyciu klienta SSH:

| Adres | Port | Element docelowy połączenia |
| ----- | ----- | ----- |
| `<clustername>-ed-ssh.azurehdinsight.net` | 22 | Węzeł krawędzi (program R Server w usłudze HDInsight) |
| `<edgenodename>.<clustername>-ssh.azurehdinsight.net` | 22 | Węzeł krawędzi (inny dowolny typ klastra, jeśli istnieje węzeł krawędzi) |
| `<clustername>-ssh.azurehdinsight.net` | 22 | Podstawowy węzeł główny |
| `<clustername>-ssh.azurehdinsight.net` | 23 | Dodatkowy węzeł główny |

> [!NOTE]
> Zastąp `<edgenodename>` o nazwie hello hello węzła krawędzi.
>
> Zastąp `<clustername>` o nazwie hello klastra.
>
> Jeśli klaster zawiera węzeł krawędzi, zalecamy, aby użytkownik __zawsze połączyć z węzłem krawędzi toohello__ przy użyciu protokołu SSH. głównymi węzłami Hello hosta usług, które są krytyczne toohello kondycji usługi Hadoop. węzeł brzegowy Hello działa tylko umieszczona na nim.
>
> Więcej informacji dotyczących używania węzłów krawędzi można znaleźć w temacie [Use edge nodes in HDInsight](hdinsight-apps-use-edge-node.md#access-an-edge-node) (Używanie węzłów krawędzi w usłudze HDInsight).

## <a name="ssh-clients"></a>Klienci SSH

Systemy Linux, Unix i macOS zapewniają hello `ssh` i `scp` poleceń. Witaj `ssh` klienta jest często używane toocreate zdalnej sesji wiersza polecenia systemu Unix lub Linux. Witaj `scp` klienta jest używane toosecurely kopiowania plików między klienta i hello systemu zdalnego.

System Microsoft Windows domyślnie nie udostępnia żadnych klientów SSH. Witaj `ssh` i `scp` klientów są dostępne dla systemu Windows hello następujące pakiety:

* [Powłoka chmury Azure](../cloud-shell/quickstart.md): hello powłoki chmury udostępnia środowisko Bash w przeglądarce, a także hello `ssh`, `scp`oraz inne typowe polecenia systemu Linux.

* [Bash na Ubuntu w systemie Windows 10](https://msdn.microsoft.com/commandline/wsl/about): hello `ssh` i `scp` polecenia są dostępne za pośrednictwem hello Bash w wierszu polecenia systemu Windows.

* [Git (https://git-scm.com/)](https://git-scm.com/): hello `ssh` i `scp` polecenia są dostępne za pomocą wiersza polecenia GitBash hello.

* [Pulpitu GitHub (https://desktop.github.com/)](https://desktop.github.com/) hello `ssh` i `scp` polecenia są dostępne za pośrednictwem hello wiersza polecenia powłoki GitHub. Pulpitu GitHub może być skonfigurowany toouse Bash, hello w wierszu polecenia systemu Windows lub programu PowerShell jako hello wiersz polecenia dla hello powłoki Git.

* [OpenSSH (https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH)](https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH): hello zespołu programu PowerShell jest eksportowanie OpenSSH tooWindows, a także wersje testu.

    > [!WARNING]
    > Pakiet OpenSSH Hello zawiera składnik serwera SSH hello, `sshd`. Ten składnik uruchamia obsługującym serwer SSH w systemie, dzięki czemu inne tooconnect tooit. Skonfiguruj ten składnik lub nie Otwórz port 22, chyba że chcesz toohost obsługującym serwer SSH w systemie. Nie jest wymagane toocommunicate z usługą HDInsight.

Dostępnych jest również kilka graficznych klientów SSH, takich jak [PuTTY (http://www.chiark.greenend.org.uk/~sgtatham/putty/)](http://www.chiark.greenend.org.uk/~sgtatham/putty/) i [MobaXterm (http://mobaxterm.mobatek.net/)](http://mobaxterm.mobatek.net/). Ci klienci mogą być używane tooconnect tooHDInsight, hello proces łączenia jest różni się od stosowania hello `ssh` narzędzia. Aby uzyskać więcej informacji zobacz dokumentację hello powitania klienta graficznego używanego.

## <a id="sshkey"></a>Uwierzytelnianie: klucze SSH

SSH klucze używają [kryptografii klucza publicznego](https://en.wikipedia.org/wiki/Public-key_cryptography) tooauthenticate sesji SSH. Kluczy SSH są bezpieczniejsze niż hasła i zapewniają prosty sposób toosecure dostępu tooyour Hadoop klastra.

W przypadku konta SSH jest zabezpieczone przy użyciu klucza, powitania klienta należy podać hello dopasowania klucz prywatny, podczas nawiązywania połączenia:

* Większość klientów może być skonfigurowany toouse __domyślny klucz__. Na przykład Witaj `ssh` klienta szuka klucza prywatnego na `~/.ssh/id_rsa` w środowiskach Linux i Unix.

* Można określić hello __klucza prywatnego tooa ścieżki__. Z hello `ssh` klienta, hello `-i` parametr jest używany toospecify hello ścieżki tooprivate klucza. Na przykład `ssh -i ~/.ssh/id_rsa sshuser@myedge.mycluster-ssh.azurehdinsight.net`.

* Jeśli masz __wiele kluczy prywatnych__, których używasz dla różnych serwerów, rozważ użycie takiego narzędzia jak [ssh-agent (https://en.wikipedia.org/wiki/Ssh-agent)](https://en.wikipedia.org/wiki/Ssh-agent). Witaj `ssh-agent` narzędzie może być używane tooautomatically wybierz hello klucza toouse podczas ustanawiania sesji SSH.

> [!IMPORTANT]
>
> Jeśli zabezpieczenie klucza prywatnego za pomocą hasła, należy wprowadzić hasło hello przypadku używania klucza hello. Narzędzia, takie jak `ssh-agent` mogą buforować hasła powitania dla Twojej wygody.

### <a name="create-an-ssh-key-pair"></a>Tworzenie pary kluczy SSH

Użyj hello `ssh-keygen` toocreate publicznego i prywatnego klucza pliki poleceń. Witaj następujące polecenie generuje parę kluczy RSA 2048-bitowego, które mogą być używane z usługą HDInsight:

    ssh-keygen -t rsa -b 2048

Zostanie wyświetlony monit o informacje o procesie tworzenia klucza hello. Na przykład, którym są przechowywane klucze hello lub czy toouse hasło. Po zakończeniu procesu hello są tworzone dwa pliki; klucz publiczny i klucz prywatny.

* Witaj __klucz publiczny__ jest używane toocreate klastra usługi HDInsight. klucz publiczny Hello ma rozszerzenie `.pub`.

* Witaj __klucza prywatnego__ jest używane tooauthenticate z klastrem usługi HDInsight toohello klienta.

> [!IMPORTANT]
> Klucze można zabezpieczyć przy użyciu hasła. W praktyce hasłem zabezpiecza się klucz prywatny. Nawet wtedy, gdy ktoś uzyskuje klucz prywatny, muszą mieć hello hasło toouse hello klucza.

### <a name="create-hdinsight-using-hello-public-key"></a>Tworzenie usługi HDInsight przy użyciu klucza publicznego hello

| Metoda tworzenia | Jak toouse hello klucza publicznego |
| ------- | ------- |
| **Witryna Azure Portal** | Usuń zaznaczenie pola wyboru __Użyj tego samego hasła jak logowania do klastra__, a następnie wybierz __klucz publiczny__ jako hello typ uwierzytelniania SSH. Na koniec wybierz plik klucza publicznego hello lub Wklej zawartość tekstową pliku hello hello hello __klucz publiczny SSH__ pola.</br>![Okno dialogowe dotyczące klucza publicznego SSH w procesie tworzenia klastra usługi HDInsight](./media/hdinsight-hadoop-linux-use-ssh-unix/create-hdinsight-ssh-public-key.png) |
| **Azure PowerShell** | Użyj hello `-SshPublicKey` parametru hello `New-AzureRmHdinsightCluster` polecenia cmdlet i przekazać zawartość hello hello klucz publiczny w postaci ciągu.|
| **Interfejs wiersza polecenia platformy Azure 1.0** | Użyj hello `--sshPublicKey` parametru hello `azure hdinsight cluster create` polecenia i przekaż hello zawartość klucza publicznego hello jako ciąg. |
| **Szablon usługi Resource Manager** | Przykład użycia kluczy SSH razem z szablonem można znaleźć w temacie [Deploy HDInsight on Linux with SSH key](https://azure.microsoft.com/resources/templates/101-hdinsight-linux-ssh-publickey/) (Wdrażanie usługi HDInsight w systemie Linux przy użyciu klucza SSH). Witaj `publicKeys` element hello [azuredeploy.json](https://github.com/Azure/azure-quickstart-templates/blob/master/101-hdinsight-linux-ssh-publickey/azuredeploy.json) plik jest tooAzure klucze hello toopass używane podczas tworzenia klastra hello. |

## <a id="sshpassword"></a>Uwierzytelnianie: hasło

Konta SSH mogą być chronione przy użyciu hasła. Po ustanowieniu połączenia przy użyciu protokołu SSH tooHDInsight jesteś tooenter zostanie wyświetlony monit o hasło hello.

> [!WARNING]
> W przypadku protokołu SSH nie zalecamy korzystania z uwierzytelniania za pomocą hasła. Hasła można złamać i są narażone toobrute siłową. Zamiast tego zalecamy używanie [kluczy SSH w celu uwierzytelniania](#sshkey).

### <a name="create-hdinsight-using-a-password"></a>Tworzenie klastrów usługi HDInsight przy użyciu hasła

| Metoda tworzenia | Jak toospecify hello hasła |
| --------------- | ---------------- |
| **Witryna Azure Portal** | Domyślnie hello konta użytkownika SSH ma hello tego samego hasła jako konto logowania hello klastra. Usuń zaznaczenie pola wyboru toouse inne hasło __Użyj tego samego hasła jak logowania do klastra__, a następnie wprowadź hasło hello w hello __hasło SSH__ pola.</br>![Okno dialogowe dotyczące hasła SSH w procesie tworzenia klastra usługi HDInsight](./media/hdinsight-hadoop-linux-use-ssh-unix/create-hdinsight-ssh-password.png)|
| **Azure PowerShell** | Użyj hello `--SshCredential` parametru hello `New-AzureRmHdinsightCluster` polecenia cmdlet, a następnie przekaż `PSCredential` obiekt, który zawiera nazwę konta użytkownika SSH hello i hasło. |
| **Interfejs wiersza polecenia platformy Azure 1.0** | Użyj hello `--sshPassword` parametru hello `azure hdinsight cluster create` poleceń i podaj wartości hasła hello. |
| **Szablon usługi Resource Manager** | Przykład użycia hasła razem z szablonem można znaleźć w temacie [Deploy HDInsight on Linux with SSH password](https://azure.microsoft.com/resources/templates/101-hdinsight-linux-ssh-password/) (Wdrażanie usługi HDInsight w systemie Linux przy użyciu hasła SSH). Witaj `linuxOperatingSystemProfile` element hello [azuredeploy.json](https://github.com/Azure/azure-quickstart-templates/blob/master/101-hdinsight-linux-ssh-password/azuredeploy.json) plik jest używany toopass hello SSH konta nazwy i hasła tooAzure podczas tworzenia klastra hello.|

### <a name="change-hello-ssh-password"></a>Zmień hasło SSH hello

Aby uzyskać informacje dotyczące zmiany hasła konta użytkownika SSH hello, zobacz hello __zmiany haseł__ sekcji hello [Zarządzanie HDInsight](hdinsight-administer-use-portal-linux.md#change-passwords) dokumentu.

## <a id="domainjoined"></a>Uwierzytelnianie: przyłączony do domeny klaster usługi HDInsight

Jeśli używasz __przyłączonych do domeny klastra usługi HDInsight__, należy użyć hello `kinit` polecenia po nawiązaniu połączenia przy użyciu protokołu SSH. Tego polecenia monit dla użytkownika domeny i hasło, a sesja jest uwierzytelniany w usłudze hello Azure Active Directory domeny skojarzony z klastrem hello.

Aby uzyskać więcej informacji, zobacz [Configure domain-joined HDInsight](hdinsight-domain-joined-configure.md) (Konfigurowanie przyłączonej do domeny usługi HDInsight).

## <a name="connect-toonodes"></a>Połącz toonodes

Witaj węzłów głównych i węzłem krawędzi (jeśli istnieje) jest dostępna za pośrednictwem hello Internetu na portach, 22 i 23.

* Podczas łączenia z toohello __węzły główne__, używają portu __22__ toohello tooconnect głównej head, węzła i port __23__ tooconnect toohello drugiego węzła głównego. Witaj toouse nazwy FQDN jest `clustername-ssh.azurehdinsight.net`, gdzie `clustername` jest hello nazwą klastra.

    ```bash
    # Connect tooprimary head node
    # port not specified since 22 is hello default
    ssh sshuser@clustername-ssh.azurehdinsight.net

    # Connect toosecondary head node
    ssh -p 23 sshuser@clustername-ssh.azurehdinsight.net
    ```
    
* Gdy connectiung toohello __węzła krawędzi__, korzystanie z portu 22. Witaj pełni kwalifikowana nazwa domeny jest `edgenodename.clustername-ssh.azurehdinsight.net`, gdzie `edgenodename` jest nazwą podane podczas tworzenia węzła krawędzi hello. `clustername`jest nazwą hello hello klastra.

    ```bash
    # Connect tooedge node
    ssh sshuser@edgnodename.clustername-ssh.azurehdinsight.net
    ```

> [!IMPORTANT]
> Hello poprzednich przykładach założono, że używasz uwierzytelniania hasła lub uwierzytelnianie certyfikatu jest automatycznie występujących. Jeśli używasz parę klucza SSH do uwierzytelniania, i hello certyfikat nie jest automatycznie używany, użyj hello `-i` klucza prywatnego hello toospecify parametru. Na przykład `ssh -i ~/.ssh/mykey sshuser@clustername-ssh.azurehdinsight.net`.

Po nawiązaniu połączenia hello zmieni tooindicate hello SSH użytkownika nazwa hello węzeł i są podłączone do. Na przykład, jeśli połączone toohello głównej węzła głównego jako `sshuser`, wiersz hello jest `sshuser@hn0-clustername:~$`.

### <a name="connect-tooworker-and-zookeeper-nodes"></a>Połącz tooworker i węzły dozorcy

Witaj węzłów procesu roboczego i dozorcy węzłów nie ma bezpośredniego połączenia z hello internet. Aby były dostępne z głównymi węzłami klastra hello lub węzłów krawędzi. Oto Hello hello ogólne kroki tooconnect tooother węzłów:

1. Za pomocą protokołu SSH tooconnect tooa head lub krawędzi węzła:

        ssh sshuser@myedge.mycluster-ssh.azurehdinsight.net

2. Witaj head toohello połączenia SSH lub węzłem krawędzi, użyj funkcji hello `ssh` polecenia tooconnect tooa procesu roboczego w węźle klastra hello:

        ssh sshuser@wn0-myhdi

    tooretrieve listę nazw domen hello hello węzłów w klastrze hello, zobacz hello [Zarządzanie HDInsight przy użyciu hello interfejsu API REST Ambari](hdinsight-hadoop-manage-ambari-rest-api.md#example-get-the-fqdn-of-cluster-nodes) dokumentu.

Jeśli konto SSH hello jest zabezpieczone przy użyciu __hasło__, wprowadź hasło hello podczas nawiązywania połączenia.

Jeśli konto SSH hello jest zabezpieczone przy użyciu __kluczy SSH__, upewnij się, że na powitania klienta jest włączone przekazywanie SSH.

> [!NOTE]
> Innym sposobem toodirectly dostęp do wszystkich węzłów w klastrze hello jest tooinstall HDInsight w sieci wirtualnej platformy Azure. Następnie można dołączyć toohello Twojego komputera zdalnego sam wirtualnych sieci i uzyskać bezpośredni dostęp do wszystkich węzłów w klastrze hello.
>
> Aby uzyskać więcej informacji, zobacz [Use a virtual network with HDInsight](hdinsight-extend-hadoop-virtual-network.md) (Używanie sieci wirtualnej z usługą HDInsight).

### <a name="configure-ssh-agent-forwarding"></a>Konfigurowanie przekazywania przez agenta SSH

> [!IMPORTANT]
> Hello kroków założono, Linux lub UNIX z systemem oraz pracować z Bash w systemie Windows 10. Jeśli te kroki nie działają w systemie, może być konieczne tooconsult dokumentacji powitania klienta SSH.

1. Za pomocą edytora tekstów otwórz plik `~/.ssh/config`. Jeśli ten plik nie istnieje, możesz go utworzyć, wprowadzając polecenie `touch ~/.ssh/config` w wierszu polecenia.

2. Dodaj następujące toohello tekst hello `config` pliku.

        Host <edgenodename>.<clustername>-ssh.azurehdinsight.net
          ForwardAgent yes

    Zastąp hello __hosta__ informacji o adresie hello węzła hello połączyć toousing SSH. Poprzedni przykład Hello korzysta z węzłem krawędzi hello. Ten wpis umożliwia skonfigurowanie Agenta przekazywania SSH dla hello określonego węzła.

3. Przetestuj agenta przekazywania SSH za pomocą następującego polecenia z terminala hello hello:

        echo "$SSH_AUTH_SOCK"

    To polecenie zwraca informacje toohello podobne następującego tekstu:

        /tmp/ssh-rfSUL1ldCldQ/agent.1792

    Jeśli nie zostaną zwrócone żadne informacje, oznacza to, że agent `ssh-agent` nie działa. Aby uzyskać więcej informacji, zobacz informacje skrypty uruchamiania agenta hello na [przy użyciu ssh-agent z ssh (http://mah.everybody.org/docs/ssh)](http://mah.everybody.org/docs/ssh) lub zapoznaj się z dokumentacją klienta SSH.

4. Po upewnieniu się, że **ssh-agent** jest uruchomiona, użyj powitania po tooadd agenta toohello klucza prywatnego SSH:

        ssh-add ~/.ssh/id_rsa

    Jeśli klucz prywatny jest przechowywany w innym pliku, Zastąp `~/.ssh/id_rsa` z hello ścieżki toohello pliku.

5. Połączenie toohello węzła krawędzi lub węzłów głównych przy użyciu protokołu SSH. Następnie można użyć procesu roboczego tooa tooconnect hello SSH polecenie lub węzeł dozorcy. Witaj, połączenie zostanie nawiązane, przy użyciu klucza hello przekazywane.

## <a name="copy-files"></a>Kopiowanie plików

Witaj `scp` narzędzie może być tooand pliki toocopy używanych w poszczególnych węzłach w klastrze hello. Na przykład Witaj następujące polecenia kopie hello `test.txt` katalogu z hello systemu lokalnego toohello głównego węzła podstawowego:

```bash
scp test.txt sshuser@clustername-ssh.azurehdinsight.net:
```

Ponieważ nie określono ścieżki po hello `:`, plik hello jest umieszczany w hello `sshuser` katalogu macierzystego.

Witaj następujący przykład kopii hello `test.txt` pliku z hello `sshuser` katalogu macierzystego w systemie lokalnym toohello głównej węzła głównego hello:

```bash
scp sshuser@clustername-ssh.azurehdinsight.net:test.txt .
```

> [!IMPORTANT]
> `scp`ma dostęp tylko do systemu plików hello pojedynczych węzłów w klastrze hello. Nie można go dane tooaccess używanych w magazynie hello zgodnego systemem plików HDFS hello klastra.
>
> Użyj `scp` potrzebne tooupload zasób do użytku w sesji SSH. Na przykład przekazać skrypt w języku Python, a następnie uruchom skrypt hello w sesji SSH.
>
> Uzyskać na bezpośrednio ładowania danych do hello magazynu zgodny z systemem plików HDFS Zobacz hello w następujących dokumentach:
>
> * [Usługa HDInsight korzystająca z usługi Azure Storage](hdinsight-hadoop-use-blob-storage.md).
>
> * [Usługa HDInsight korzystająca z usługi Azure Data Lake Store](hdinsight-hadoop-use-data-lake-store.md).

## <a name="next-steps"></a>Następne kroki

* [Use SSH tunneling with HDInsight](hdinsight-linux-ambari-ssh-tunnel.md) (Używanie tunelowania SSH z usługą HDInsight)
* [Use a virtual network with HDInsight](hdinsight-extend-hadoop-virtual-network.md) (Używanie sieci wirtualnej z usługą HDInsight)
* [Use edge nodes in HDInsight](hdinsight-apps-use-edge-node.md#access-an-edge-node) (Używanie węzłów krawędzi w usłudze HDInsight)