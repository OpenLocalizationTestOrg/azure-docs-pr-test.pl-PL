Nie zawsze instalowanie pakietów w sieci Azure przy użyciu programu pip kończy się powodzeniem.  Może się zdarzyć, że pakiet hello nie jest dostępny na powitania indeksu pakietów języka Python.  Jest to możliwe, że wymagane jest kompilatora (kompilator nie jest dostępny na powitania maszyny uruchomionych hello aplikacji sieci web w usłudze Azure App Service).

W tej sekcji wyjaśniono sposób toodeal dotyczącą tego problemu.

### <a name="request-wheels"></a>Żądanie plików w formacie Wheel
Jeśli hello instalacja pakietu wymaga kompilatora, możesz spróbować skontaktować się hello toorequest właściciela pakietu, który koła udostępniane hello pakietu.

Z hello udostępnieniu [Microsoft Visual C++ Compiler for Python 2.7][Microsoft Visual C++ Compiler for Python 2.7], jest teraz łatwiejsze pakiety toobuild mający kodu macierzystego języka Python 2.7.

### <a name="build-wheels-requires-windows"></a>Tworzenie plików w formacie Wheel (wymaga systemu Windows)
Uwaga: Korzystając z tej opcji, upewnij się, że pakiet hello toocompile przy użyciu środowiska Python, odpowiadający hello platformie/architekturze/wersji, jaka jest używana na powitania aplikacji sieci web w usłudze Azure App Service (Windows/32-bit/2.7 lub 3.4).

Jeśli pakiet hello nie instaluje, ponieważ wymaga kompilatora, można zainstalować kompilator hello na komputerze lokalnym i kompilacji w formacie wheel hello pakiet, który następnie zostanie dołączony do repozytorium.

Użytkownicy systemów Mac/Linux: Jeśli nie masz komputera z systemem Windows tooa dostępu, zobacz [tworzenie maszyny wirtualnej systemem Windows] [ Create a Virtual Machine Running Windows] jak toocreate Maszynę wirtualną na platformie Azure.  Można go użyć koła hello toobuild, je dodać toohello repozytorium i odrzucić hello maszyny Wirtualnej, jeśli chcesz. 

For Python 2.7 można zainstalować [Microsoft Visual C++ Compiler for Python 2.7][Microsoft Visual C++ Compiler for Python 2.7].

W przypadku języka Python 3.4 można zainstalować [Microsoft Visual C++ 2010 Express][Microsoft Visual C++ 2010 Express].

koła toobuild potrzebne hello pakiet wheel:

    env\scripts\pip install wheel

Użyjesz `pip wheel` toocompile zależności:

    env\scripts\pip wheel azure==0.8.4

Spowoduje to utworzenie pliku .whl w folderze \wheelhouse hello.  Dodaj hello \wheelhouse folder i kółka pliki tooyour repozytorium.

Edytuj hello tooadd Twojego pliku requirements.txt `--find-links` opcji u góry hello. Ta wartość informuje narzędzie pip toolook dla dokładnego dopasowania w folderze lokalnym hello przed indeksu pakietów języka python toohello będzie.

    --find-links wheelhouse
    azure==0.8.4

Jeśli chcesz tooinclude wszystkie zależności w hello \wheelhouse folderze i używaj hello pakiet języka python indeksu na wszystkich indeksu pakietów hello tooignore pip można wymusić przez dodanie `--no-index` toohello góry pliku requirements.txt.

    --no-index

### <a name="customize-installation"></a>Instalacja niestandardowa
Można dostosować hello wdrożenia skryptu tooinstall pakietu w środowisku wirtualnym hello przy użyciu Instalatora alternatywnego, takiego jak easy\_zainstalować.  Zapoznaj się z plikiem deploy.cmd, w którym odpowiedni przykład jest zakomentowany.  Upewnij się, że takie pakiety nie są wymienione w pliku requirements.txt, pip tooprevent z ich instalowania.

Dodaj ten skrypt wdrażania toohello:

    env\scripts\easy_install somepackage

Może być również toouse można łatwo\_zainstalować tooinstall z Instalatorem exe (niektóre są rozpoznają format zip, dlatego łatwo\_je obsługuje instalację).  Dodaj hello Instalator tooyour repozytorium, a następnie Wywołaj program easy\_install, przekazując hello toohello ścieżki pliku wykonywalnego.

Dodaj ten skrypt wdrażania toohello:

    env\scripts\easy_install "%DEPLOYMENT_SOURCE%\installers\somepackage.exe"

### <a name="include-hello-virtual-environment-in-hello-repository-requires-windows"></a>Zawierają środowisko wirtualne hello hello repozytorium (wymaga systemu Windows)
Uwaga: Podczas korzystania z tej opcji upewnij się, że toouse środowisku wirtualnym, które odpowiada hello platformie/architekturze/wersji, jaka jest używana na powitania aplikacji sieci web w usłudze Azure App Service (Windows/32-bit/2.7 lub 3.4).

Jeśli dołączysz hello środowiska wirtualnego do repozytorium hello można zapobiec zarządzaniu środowiskiem wirtualnym na platformie Azure, tworząc pusty plik skryptu wdrażania hello:

    .skipPythonDeployment

Zaleca się usunięcie istniejącego środowiska wirtualnego hello w aplikacji hello, tooprevent pozostawieniu plików z podczas hello środowisko wirtualne było zarządzane automatycznie.

[Create a Virtual Machine Running Windows]: http://azure.microsoft.com/documentation/articles/virtual-machines-windows-hero-tutorial/
[Microsoft Visual C++ Compiler for Python 2.7]: http://aka.ms/vcpython27
[Microsoft Visual C++ 2010 Express]: http://go.microsoft.com/?linkid=9709949
