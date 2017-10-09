Każdy obiekt blob w usłudze Azure Storage musi znajdować się w kontenerze. Witaj kontenera stanowi część hello nazwa obiektu blob. Na przykład `mycontainer` jest nazwą hello hello kontenera w tych przykładowych identyfikatorach URI obiektów blob:

    https://storagesample.blob.core.windows.net/mycontainer/blob1.txt
    https://storagesample.blob.core.windows.net/mycontainer/photos/myphoto.jpg

Nazwa kontenera musi być prawidłową nazwą DNS, zgodnych toohello reguły nazewnictwa:

1. Nazwy kontenerów muszą zaczynać się literą lub cyfrą i może zawierać tylko litery, cyfry i znak kreski (-) hello.
2. Bezpośrednio przed każdym znakiem kreski (-) i bezpośrednio po nim musi występować litera lub cyfra. W nazwach kontenerów następujące po sobie kreski są niedozwolone.
3. Wszystkie litery w nazwie kontenera muszą być małymi literami.
4. Nazwy kontenerów muszą zawierać od 3 do 63 znaków.

> [!IMPORTANT]
> Należy pamiętać, że hello nazwę kontenera zawsze muszą być małymi literami. Jeśli zawierać wielką literę w nazwie kontenera lub w przeciwnym razie naruszają hello kontenera nazewnictwa, może zostać wyświetlony błąd 400 (nieprawidłowe żądanie). 
> 
> 

