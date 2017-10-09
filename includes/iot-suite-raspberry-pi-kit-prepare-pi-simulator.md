## <a name="prepare-your-raspberry-pi"></a>Przygotowanie Twojego malinowe Pi

### <a name="install-raspbian"></a>Zainstaluj Raspbian

Jeśli po raz pierwszy używasz programu Pi malina to hello należy tooinstall hello Raspbian systemu operacyjnego za pomocą NOOBS na karcie SD hello zawarte w zestawie hello. Hello [malina Pi oprogramowania przewodnik] [ lnk-install-raspbian] w tym artykule opisano sposób tooinstall systemu operacyjnego na Twoje malina Pi. W tym samouczku założono, że zainstalowano system operacyjny Raspbian hello na Twoje Pi malina.

> [!NOTE]
> Karta Hello SD objęte hello [Microsoft Azure IoT Starter Kit malina Pi 3] [ lnk-starter-kits] ma już NOOBS zainstalowane. Można uruchomić hello Pi malina z tej karty i wybrać hello tooinstall Raspbian systemu operacyjnego.

ustawienia sprzętu hello toocomplete, musisz:

- Połącz Pi malina toohello zasilacza zawarte w zestawie hello.
- Łączenie sieci tooyour Pi malina za pomocą kabla Ethernet hello zawarte w zestawie. Alternatywnie możesz skonfigurować [łączności bezprzewodowej] [ lnk-pi-wireless] Twojego malina pi.

Ustawienia sprzętu hello Twojej pi malina zostało zakończone.

### <a name="sign-in-and-access-hello-terminal"></a>Zaloguj się i uzyskać dostęp hello terminali

Masz dwie opcje tooaccess terminali środowiska użytkownika Pi malina:

- Jeśli klawiatura i monitorowanie połączonych tooyour Pi malina, możesz użyć hello Raspbian GUI tooaccess okno terminalu.

- Dostęp z wiersza polecenia hello na Twoje Pi malina przy użyciu protokołu SSH z komputera stacjonarnego.

#### <a name="use-a-terminal-window-in-hello-gui"></a>Okno terminalu w hello graficznego interfejsu użytkownika

username są Hello domyślne poświadczenia dla Raspbian **pi** i hasło **malina**. Na pasku zadań hello w hello graficznego interfejsu użytkownika, możesz uruchomić hello **Terminal** narzędzie za pomocą ikony hello, która wygląda jak monitora.

#### <a name="sign-in-with-ssh"></a>Zaloguj się przy użyciu protokołu SSH

Można użyć SSH dla wiersza polecenia dostępu tooyour malina Pi. Artykuł Hello [SSH (Secure Shell)] [ lnk-pi-ssh] w tym artykule opisano sposób tooconfigure SSH na Twoje Pi malina i w jaki sposób tooconnect z [Windows] [ lnk-ssh-windows] lub [Systemu operacyjnego Linux & Mac][lnk-ssh-linux].

Zaloguj się przy użyciu nazwy użytkownika **pi** i hasło **malina**.

#### <a name="optional-share-a-folder-on-your-raspberry-pi"></a>Opcjonalnie: Udostępnianie folderu w Twojej Pi malina

Opcjonalnie możesz tooshare folderem na Twoje Pi malina ze środowiskiem pulpitu. Udostępnianie folderu umożliwia możesz toouse w edytorze tekstów pulpitu preferowanych (takich jak [Visual Studio Code](https://code.visualstudio.com/) lub [Sublime tekst](http://www.sublimetext.com/)) plików tooedit na Twoje Pi malina zamiast `nano` lub `vi`.

tooshare folder z systemem Windows, skonfiguruj serwer Samba na powitania malina Pi. Alternatywnie można użyć wbudowanych hello [SFTP](https://www.raspberrypi.org/documentation/remote-access/) serwera za pomocą klienta protokołu SFTP na pulpicie.

[lnk-install-raspbian]: https://www.raspberrypi.org/learning/software-guide/quickstart/
[lnk-pi-wireless]: https://www.raspberrypi.org/documentation/configuration/wireless/README.md
[lnk-pi-ssh]: https://www.raspberrypi.org/documentation/remote-access/ssh/README.md
[lnk-ssh-windows]: https://www.raspberrypi.org/documentation/remote-access/ssh/windows.md
[lnk-ssh-linux]: https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md
[lnk-starter-kits]: https://azure.microsoft.com/develop/iot/starter-kits/