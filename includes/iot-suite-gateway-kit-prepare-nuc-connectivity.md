## <a name="prepare-your-intel-nuc"></a>Przygotowanie programu Intel NUC

ustawienia sprzętu hello toocomplete, musisz:

- Połącz Intel NUC toohello zasilacza zawarte w zestawie hello.
- Łączenie sieci tooyour Intel NUC za pomocą kabla Ethernet.

Ustawienia sprzętu hello urządzenie bramy Intel NUC zostało zakończone.

### <a name="sign-in-and-access-hello-terminal"></a>Zaloguj się i uzyskać dostęp hello terminali

Masz dwie opcje tooaccess środowisku terminal na Twojej NUC Intel:

- Klawiatura i monitorowanie połączonych tooyour NUC firmy Intel, można przejść do powłoki hello bezpośrednio. poświadczenia domyślne Hello są nazwy użytkownika **głównego** i hasło **głównego**.

- Powłoka hello dostępu na Twojej NUC Intel przy użyciu protokołu SSH z komputera stacjonarnego.

#### <a name="sign-in-with-ssh"></a>Zaloguj się przy użyciu protokołu SSH

toosign się przy użyciu protokołu SSH, należy hello adres IP Twojego NUC Intel. Jeśli klawiatura i monitorowanie połączonych tooyour NUC firmy Intel, użyj hello `ifconfig` adres IP hello toofind polecenia. Alternatywnie można połączyć z tooyour router toolist hello adresów urządzeń w sieci.

Zaloguj się przy użyciu nazwy użytkownika **głównego** i hasło **głównego**.

#### <a name="optional-share-a-folder-on-your-intel-nuc"></a>Opcjonalnie: Udostępnianie folderu w Twojej NUC Intel

Opcjonalnie możesz tooshare folderem na Twojej NUC Intel ze środowiskiem pulpitu. Udostępnianie folderu umożliwia możesz toouse w edytorze tekstów pulpitu preferowanych (takich jak [Visual Studio Code](https://code.visualstudio.com/) lub [Sublime tekst](http://www.sublimetext.com/)) plików tooedit na NUC Twojego Intel zamiast `nano` lub `vi`.

tooshare folder z systemem Windows, skonfiguruj serwer Samba na powitania Intel NUC. Można również użyć hello SFTP serwera na powitania Intel NUC za pomocą protokołu SFTP klienta na komputerze pulpitu.
