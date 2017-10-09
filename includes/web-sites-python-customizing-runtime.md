Platforma Azure określi wersję hello toouse języka Python dla swojego środowiska wirtualnego z powitania po priorytet:

1. Wersja określona w pliku runtime.txt w folderze głównym hello
2. Wersja określona przez ustawienie języka Python w konfiguracji aplikacji sieci web hello (hello **ustawienia** > **ustawienia aplikacji** bloku aplikacji sieci web w portalu Azure hello)
3. Python-2.7 jest domyślnym hello, jeśli nie określono żadnego z powyższych hello są

Prawidłowe wartości dla zawartości hello 

    \runtime.txt

są:

* python-2.7
* python-3.4

Jeśli hello wersja mikro (trzecia cyfra) jest określona, zostanie zignorowana.

