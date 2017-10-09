Hello skrypt wdrożenia pominie etap tworzenia środowiska wirtualnego hello na platformie Azure, jeśli wykryje, że zgodne środowisko wirtualne już istnieje.  Może to znacznie przyspieszyć wdrożenie.  Pakiety, które zostały już zainstalowane, zostaną pominięte przez narzędzie pip.

W niektórych sytuacjach może być tooforce usunięcie tego środowiska wirtualnego.  Należy toodo to w razie tooinclude środowiska wirtualnego jako część repozytorium.  Można również toodo to jeśli potrzebujesz tooget niektóre pakiety lub testu toorequirements.txt zmiany.

Istnieje kilka opcji toomanage hello istniejące środowisko wirtualne na platformie Azure:

### <a name="option-1-use-ftp"></a>Opcja 1: użycie protokołu FTP
Za pomocą klienta FTP należy podłączyć serwer toohello i będzie folderu env hello toodelete stanie.  Należy pamiętać, że niektórzy klienci FTP (na przykład przeglądarki sieci web) mogą być tylko do odczytu i nie pozwalają toodelete folderów, dlatego należy toomake toouse się, że klient FTP taką możliwość.  Nazwa hosta Hello FTP i użytkowników są wyświetlane w bloku aplikacja sieci web na powitania [Azure Portal](https://portal.azure.com).

### <a name="option-2-toggle-runtime"></a>Opcja 2: przełączenie w czasie wykonywania
Poniżej przedstawiono ten wariant wykorzystuje hello faktu, że skrypt wdrożenia hello spowoduje usunięcie folderu env hello, jeśli nie odpowiada on żądanej wersji języka Python hello.  To spowoduje skutecznie usunięcie istniejącego środowiska hello i Utwórz nowe.

1. Przełącznik tooa inną wersję języka Python (za pośrednictwem pliku runtime.txt lub hello **ustawienia aplikacji** bloku w hello Azure Portal)
2. wyślij pewne zmiany do usługi git (ignoruj błędy instalacji narzędzia pip, jeśli wystąpią)
3. Przełącz wstecz tooinitial wersji języka Python
4. ponownie wyślij pewne zmiany do usługi git

### <a name="option-3-customize-deployment-script"></a>Opcja 3: dostosowywanie skryptu wdrożenia
Jeśli hello skrypt wdrożenia został dostosowany, można zmienić hello kod w pliku deploy.cmd tooforce go folderu env hello toodelete.

