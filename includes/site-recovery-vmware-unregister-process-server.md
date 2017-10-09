toounregister kroki powitania serwera przetwarzania różni się w zależności od stanu połączenia z powitania serwera konfiguracji.

### <a name="unregister-a-process-server-that-is-in-a-connected-state"></a>Wyrejestrowywanie serwera przetwarzania, który jest w stanie Połączono

1. Zdalne na powitania serwera przetwarzania jako Administrator.
2. Uruchamianie hello **Panelu sterowania** , a następnie otwórz **programy > Odinstaluj program**
3. Odinstaluj program o nazwie hello **Microsoft Azure lokacji odzyskiwania procesu konfiguracji serwera**
4. Po ukończeniu kroku 3 możesz odinstalować **zależności serwera konfiguracji/przetwarzania usługi Microsoft Azure Site Recovery**

### <a name="unregister-a-process-server-that-is-in-a-disconnected-state"></a>Wyrejestrowywanie serwera przetwarzania, który jest w stanie Rozłączono

> [!WARNING]
> Użyj hello następujące czynności, należy używać, gdy nie ma żadnego sposób toorevive hello wirtualnej komputera na powitania, który został zainstalowany serwer przetwarzania.

1. Zaloguj się na serwerze konfiguracji tooyour jako Administrator.
2. Otwórz administracyjny wiersz polecenia i przejdź do katalogu toohello `%ProgramData%\ASR\home\svsystems\bin`.
3. Teraz uruchom polecenie hello.

    ```
    perl Unregister-ASRComponent.pl -IPAddress <IP_of_Process_Server> -Component PS
    ```
4. Usunie hello szczegóły serwera przetwarzania hello z hello systemu.
