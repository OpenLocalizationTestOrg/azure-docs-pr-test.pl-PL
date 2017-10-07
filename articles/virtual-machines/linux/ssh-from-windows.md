---
title: aaaUse SSH kluczy z systemem Windows dla maszyn wirtualnych systemu Linux | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak klucze toogenerate i używanie SSH na maszynie wirtualnej Windows komputera tooconnect tooa systemu Linux na platformie Azure."
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: 2cacda3b-7949-4036-bd5d-837e8b09a9c8
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/08/2017
ms.author: danlep
ms.openlocfilehash: 6c44217332538857cc2ca2e85de4b476aa71251c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-ssh-keys-with-windows-on-azure"></a>Jak klucze tooUse SSH z usługą Microsoft Azure
> [!div class="op_single_selector"]
> * [Windows](ssh-from-windows.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
> * [Linux/Mac](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
>
>

Po podłączeniu tooLinux maszynach wirtualnych (VM) na platformie Azure, należy użyć [kryptografii klucza publicznego](https://wikipedia.org/wiki/Public-key_cryptography) tooprovide bezpieczniejsze toolog sposób w tooyour maszyny Wirtualnej systemu Linux. Ten proces obejmuje wymianę kluczy publicznych i prywatnych przy użyciu hello bezpiecznej powłoki (SSH) polecenia tooauthenticate samodzielnie zamiast nazwy użytkownika i hasła. Hasła są narażone toobrute-siłową, szczególnie w przypadku maszyn wirtualnych połączonych z Internetem, takich jak serwery sieci web. Ten artykuł zawiera omówienie kluczy SSH i jak toogenerate hello odpowiednich kluczy na komputerze z systemem Windows.

## <a name="overview-of-ssh-and-keys"></a>Omówienie protokołu SSH oraz kluczy
Możesz bezpiecznie zalogować tooyour maszyny Wirtualnej systemu Linux przy użyciu kluczy publicznych i prywatnych:

* Witaj **klucz publiczny** znajduje się w sieci maszyny Wirtualnej systemu Linux lub innych usług, że chcesz toouse kryptografii klucza publicznego.
* Witaj **klucza prywatnego** jest wykonywanych obecny tooyour maszyny Wirtualnej systemu Linux podczas logowania, tooverify Twoją tożsamość. Klucz prywatny należy chronić. Nie należy go udostępniać.

Te klucze publiczne i prywatne mogą być używane na wiele maszyn wirtualnych i usług. Nie trzeba pary kluczy dla każdej maszyny Wirtualnej lub usługi, które chcesz tooaccess. Aby uzyskać bardziej szczegółowe informacje, zobacz [kryptografii klucza publicznego](https://wikipedia.org/wiki/Public-key_cryptography).

SSH jest protokołem zaszyfrowanego połączenia, który umożliwia bezpiecznego logowania za pośrednictwem niezabezpieczonego połączenia. Jest hello domyślnego połączenia protokołu dla maszyn wirtualnych systemu Linux hostowanych w systemie Azure. SSH sam zapewnia połączenie szyfrowane, jednak nadal za pomocą hasła przy użyciu połączeń SSH pozostawia hello wirtualna narażone toobrute-force ataków lub zgadywania haseł. Większe bezpieczeństwo i preferowaną metody tooa łączącego maszyny Wirtualnej przy użyciu protokołu SSH jest przy użyciu tych kluczy publicznych i prywatnych, znanej także jako kluczy SSH.

Jeśli nie chcesz, aby toouse kluczy SSH, nadal można rejestrować w tooyour maszyn wirtualnych systemu Linux przy użyciu hasła. Jeśli maszyna wirtualna nie jest narażonych toohello Internetu, przy użyciu hasła może być wystarczające. Można jednak nadal konieczne toomanage hasła dla każdej maszyny Wirtualnej systemu Linux i obsługa zasad haseł w dobrej kondycji i rozwiązań, takich jak minimalna długość hasła i ich regularne aktualizowanie. używanie kluczy SSH Hello zmniejsza się złożoność hello zarządzania poszczególnych poświadczeń między wieloma maszynami wirtualnymi.

## <a name="windows-packages-and-ssh-clients"></a>Pakiety systemu Windows i klientów SSH
Połącz tooand zarządzać maszyn wirtualnych systemu Linux w programie Azure przy użyciu **klienta SSH**. Komputery z systemem Windows nie zazwyczaj jest zainstalowany klient SSH. Hello systemu Windows 10 Anniversary aktualizacji dodawania Bash dla systemu Windows oraz hello najnowszą aktualizację twórców 10 systemu Windows zapewnia dodatkowe aktualizacje. Podsystem ten systemu Windows dla systemu Linux pozwala toorun i dostęp do narzędzi takich jak klient SSH natywnie w powłoki Bash. Można następnie wykonasz którąkolwiek z hello Linux docs, takich jak [parowaniem toogenerate klucza SSH dla systemu Linux](mac-create-ssh-keys.md). Bash systemu Windows jest nadal w fazie projektowania i jest uznawany za wydania beta. Aby uzyskać więcej informacji na temat Bash systemu Windows, zobacz [Bash na Ubuntu w systemie Windows](https://msdn.microsoft.com/commandline/wsl/about).

W razie potrzeby toouse coś innego niż Bash dla systemu Windows, typowe Windows SSH klienci które można zainstalować znajdują się w następujących pakietów hello:

* [Git dla systemu Windows](https://git-for-windows.github.io/)
* [programu puTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/)
* [MobaXterm](http://mobaxterm.mobatek.net/)
* [Programów Cygwin](https://cygwin.com/)


## <a name="which-key-files-do-you-need-toocreate"></a>Które klucza pliki potrzebujesz toocreate?
Platforma Azure wymaga co najmniej 2048-bitowego, **ssh-rsa** sformatowany klucze publiczne i prywatne. Jeśli zarządzasz zasobów platformy Azure przy użyciu klasycznego modelu wdrożenia hello, należy również toogenerate PEM (`.pem` pliku).

Poniżej przedstawiono scenariusze wdrażania hello i hello typów plików, których można używać w każdym:

1. **SSH-rsa** klucze są wymagane dla każdego wdrożenia przy użyciu hello [portalu Azure](https://portal.azure.com)i wdrożenia usługi Resource Manager przy użyciu hello [interfejsu wiersza polecenia Azure](../../cli-install-nodejs.md).
   * Klucze te są zazwyczaj potrzebne wszystkie większości użytkowników.
2. A `.pem` pliku jest wymagana toocreate maszyn wirtualnych przy użyciu wdrożenia klasycznego hello. Klucze te mogą wykorzystywać w przypadku wdrożeń Classic hello [portalu Azure](https://portal.azure.com) lub [interfejsu wiersza polecenia Azure](../../cli-install-nodejs.md).
   * Wystarczy toocreate tych dodatkowych kluczy i certyfikatów zarządzania zasoby utworzone za pomocą hello klasycznego modelu wdrożenia.

## <a name="install-git-for-windows"></a>Zainstaluj usługę Git dla systemu Windows
Witaj poprzedniej sekcji wymienionych kilka pakietów, które zawierają hello `openssl` narzędzia dla systemu Windows. To narzędzie jest toocreate wymagane klucze publiczne i prywatne. Witaj, jak następujące przykłady szczegółów tooinstall i użyj **Git dla systemu Windows**, ale można wybrać niezależnie od tego pakietu preferowane. **Git dla systemu Windows** zapewnia dostęp toosome dodatkowe oprogramowanie open source ([OSS](https://en.wikipedia.org/wiki/Open-source_software)) narzędzi, które mogą być przydatne podczas pracy z maszyn wirtualnych systemu Linux.

1. Pobierz i zainstaluj **Git dla systemu Windows** z następującej lokalizacji hello: [https://git-for-windows.github.io/](https://git-for-windows.github.io/).
2. Zaakceptuj opcje domyślne hello podczas hello procesu instalacji, chyba że jest wymagana toochange je.
3. Uruchom **Git Bash** z hello **Start Menu** > **Git** > **Git Bash**. konsoli Hello wygląda podobnie toohello poniższy przykład:

    ![Git dla Bash systemu Windows shell](./media/ssh-from-windows/git-bash-window.png)

## <a name="create-a-private-key"></a>Utwórz klucz prywatny
1. W Twojej **Git Bash** okna, użyj `openssl.exe` toocreate klucza prywatnego. Witaj poniższym przykładzie jest tworzony klucz o nazwie `myPrivateKey` i certyfikat o nazwie `myCert.pem`:

    ```bash
    openssl.exe req -x509 -nodes -days 365 -newkey rsa:2048 \
        -keyout myPrivateKey.key -out myCert.pem
    ```

    Witaj dane wyjściowe wyglądają toohello podobnie poniższy przykład:

    ```bash
    Generating a 2048 bit RSA private key
    .......................................+++
    .......................+++
    writing new private key too'myPrivateKey.key'
    -----
    You are about toobe asked tooenter information that will be incorporated
    into your certificate request.
    What you are about tooenter is what is called a Distinguished Name or a DN.
    There are quite a few fields but you can leave some blank
    For some fields there will be a default value,
    If you enter '.', hello field will be left blank.
    -----
    Country Name (2 letter code) [AU]:
    ```

   Jeśli bash zgłasza błąd, spróbuj otworzyć nowy **Git Bash** okno z podwyższonym poziomem uprawnień. Następnie uruchom ponownie hello `openssl` polecenia.

2. Witaj odpowiedzi monituje o podanie nazwy kraju, lokalizację, nazwę organizacji, itp.
3. Twoje nowy klucz prywatny i certyfikat są tworzone w bieżącym katalogu roboczym. Ze względów bezpieczeństwa należy ustawić uprawnienia hello na klucz prywatny, aby tylko można do niego dostęp:

    ```bash
    chmod 0600 myPrivateKey.key
    ```

4. Witaj [następnej sekcji](#create-a-private-key-for-putty) szczegółów przy użyciu PuTTYgen tooboth wyświetlanie i Użyj klucza publicznego hello i tworzenie klucza prywatnego określone dla przy użyciu programu PuTTY tooSSH tooLinux maszyn wirtualnych. Witaj następujące polecenie generuje plik klucza publicznego o nazwie `myPublicKey.key` od razu pomocne:

    ```bash
    openssl.exe rsa -pubout -in myPrivateKey.key -out myPublicKey.key
    ```

5. Również toomanage Classic zasobów, należy przekonwertować hello `myCert.pem` zbyt`myCert.cer` (algorytmem DER X509 certyfikatu). Wykonaj ten krok opcjonalny, tylko wtedy, gdy potrzebujesz toospecifically zarządzanie zasobami Classic starszej.

    Konwertuj hello certyfikatu przy użyciu hello następujące polecenie:

    ```bash
    openssl.exe  x509 -outform der -in myCert.pem -out myCert.cer
    ```

## <a name="create-a-private-key-for-putty"></a>Utwórz klucz prywatny dla programu PuTTY
PuTTY jest typowe klient SSH dla systemu Windows. Możesz są wolne toouse klienta SSH, który chcesz. toouse PuTTY należy toocreate dodatkowy typ klucza - prywatnego klucza PuTTY (PPK). Jeśli nie chcesz, aby toouse programu PuTTY, Pomiń tę sekcję.

Witaj poniższy przykład tworzy dodatkowe klucz prywatny specjalnie z myślą o PuTTY toouse:

1. Użyj **Git Bash** tooconvert Twojego prywatnego klucza do prywatnego klucza RSA zrozumiałe PuTTYgen. Witaj poniższym przykładzie jest tworzony klucz o nazwie `myPrivateKey_rsa` z hello istniejący klucz o nazwie `myPrivateKey`:

    ```bash
    openssl rsa -in ./myPrivateKey.key -out myPrivateKey_rsa
    ```

    Ze względów bezpieczeństwa należy ustawić uprawnienia hello na klucz prywatny, aby tylko można do niego dostęp:

    ```bash
    chmod 0600 myPrivateKey_rsa
    ```
2. Pobierz i uruchom PuTTYgen z następującej lokalizacji hello: [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html)
3. Kliknij hello menu: **pliku** > **klucza prywatnego obciążenia**
4. Zlokalizuj klucz prywatny (`myPrivateKey_rsa` hello poprzedniego przykładu). Witaj domyślnego katalogu podczas uruchamiania **Git Bash** jest `C:\Users\%username%`. Zmień hello pliku filtru tooshow **wszystkie pliki (\*.\*)** :

    ![Ładowanie hello istniejącego klucza prywatnego do PuTTYgen](./media/ssh-from-windows/load-private-key.png)
5. Kliknij przycisk **Otwórz**. Wiersz wskazuje, że ten klucz hello został pomyślnie zaimportowany:

    ![Pomyślnie zaimportowano klucza tooPuTTYgen](./media/ssh-from-windows/successfully-imported-key.png)
6. Kliknij przycisk **OK** tooclose hello wiersza.
7. klucz publiczny Hello jest wyświetlany u góry hello hello **PuTTYgen** okna. Skopiuj i wklej ten klucz publiczny do hello portalu Azure lub usługi Azure Resource Manager szablonu podczas tworzenia maszyny Wirtualnej systemu Linux. Możesz również kliknąć **Zapisz klucz publiczny** toosave komputera tooyour kopiowania:

    ![Zapisz PuTTY pliku klucza publicznego](./media/ssh-from-windows/save-public-key.png)

    Witaj poniższy przykład przedstawia sposób czy skopiuj i wklej ten klucz publiczny do hello portalu Azure, podczas tworzenia maszyny Wirtualnej systemu Linux. klucz publiczny Hello następnie jest zwykle przechowywany w `~/.ssh/authorized_keys` na nowej maszynie Wirtualnej.

    ![Klucz publiczny używany podczas tworzenia maszyny Wirtualnej w portalu Azure hello](./media/ssh-from-windows/use-public-key-azure-portal.png)
8. W **PuTTYgen**, kliknij przycisk **zapisać klucz prywatny**:

    ![Zapisz plik klucza prywatnego PuTTY](./media/ssh-from-windows/save-ppk-file.png)

   > [!WARNING]
   > Monit z pytaniem, jeśli chcesz toocontinue bez wprowadzania hasła dla klucza. Hasło jest takie jak hasło klucza prywatnego tooyour dołączone. Nawet wtedy, gdy ktoś zostały tooobtain klucz prywatny one nadal nie będzie możliwe tooauthenticate przy użyciu tylko hello klucza. Czy muszą hello hasło. Bez hasła Jeśli ktoś uzyskuje klucz prywatny one można zalogować się w tooany maszyny Wirtualnej lub usługi użyje tego klucza. Zaleca się Utwórz hasło. Jednak Jeśli zapomnisz hasło hello, nie ma żadnych toorecover sposób go.
   >
   >

    Tooenter hasło, kliknij przycisk **nr**, wprowadź hasło w oknie głównym PuTTYgen hello, a następnie kliknij przycisk **Zapisz klucz prywatny** ponownie. W przeciwnym razie kliknij przycisk **tak** toocontinue bez podawania hello opcjonalne hasło.
9. Wprowadź plik PPK toosave nazwy i lokalizacji.

## <a name="use-putty-toossh-tooa-linux-machine"></a>Użyj programu Putty tooSSH tooa maszyny systemu Linux
Ponownie PuTTY jest typowe klient SSH dla systemu Windows. Możesz są wolne toouse klienta SSH, który chcesz. Witaj, jak następujące kroki, szczegóły toouse Twojego prywatnego klucza tooauthenticate z maszyny Wirtualnej platformy Azure przy użyciu protokołu SSH. Witaj kroki są podobne w innym klientom klucza SSH pod względem konieczności tooload Twojego hello tooauthenticate klucza prywatnego połączenia SSH.

1. Pobierz i uruchom program putty z hello następujących lokalizacji: [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html)
2. Wypełnij hello nazwę hosta lub adres IP maszyny Wirtualnej z hello portalu Azure:

    ![Otwórz nowe połączenie programu PuTTY](./media/ssh-from-windows/putty-new-connection.png)
3. Przed wybraniem **Otwórz**, kliknij przycisk **połączenia** > **SSH** > **uwierzytelniania** kartę. Przeglądaj tooand wybierz klucz prywatny:

    ![Wybierz klucza prywatnego PuTTY dla uwierzytelniania](./media/ssh-from-windows/putty-auth-dialog.png)
4. Kliknij przycisk **Otwórz** maszyny wirtualnej tooyour tooconnect

## <a name="next-steps"></a>Następne kroki
Można również generować klucze publiczne i prywatne hello [przy użyciu OS X i Linux](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Aby uzyskać więcej informacji na temat Bash systemu Windows i hello korzyści narzędzia OSS gotowe na komputerze z systemem Windows, temacie [Bash na Ubuntu w systemie Windows](https://msdn.microsoft.com/commandline/wsl/about).

Jeśli masz problem przy użyciu protokołu SSH tooconnect tooyour maszyn wirtualnych systemu Linux, zobacz [Rozwiązywanie problemów z SSH połączeń tooan maszyny Wirtualnej systemu Linux Azure](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
