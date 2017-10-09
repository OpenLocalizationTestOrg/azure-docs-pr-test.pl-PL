
1. Zaloguj się tooyour subskrypcji platformy Azure przy użyciu hello czynności opisane w [połączyć tooAzure z hello Azure CLI 1.0](../articles/xplat-cli-connect.md).

2. Upewnij się, że są w trybie wdrożenia klasycznego hello w następujący sposób:

    ```azurecli
    azure config mode asm
    ```

3. Sprawdzić hello obrazu systemu Linux, które mają tooload z hello dostępnych obrazów w następujący sposób:

   ```azurecli   
    azure vm image list | grep "Linux"
    ```
   
    W oknie wiersza polecenia systemu Windows użyj polecenia **find** zamiast grep.
   
4. Użyj `azure vm create` toocreate maszyny Wirtualnej z obrazu systemu Linux hello z poprzedniej liście hello. Ten krok powoduje utworzenie konta magazynu i usługi w chmurze. Można także połączyć tej maszyny Wirtualnej tooan istniejącej usługi w chmurze z `-c` opcji. Utwórz toolog punkt końcowy SSH w maszyny wirtualnej systemu Linux toohello z hello `-e` opcji. Witaj poniższy przykład tworzy Maszynę wirtualną o nazwie `myVM` przy użyciu hello `Ubuntu-14_04_4-LTS` obrazu w hello `West US` lokalizacji i dodaje nazwę użytkownika `ops`:
   
    ```azurecli
    azure vm create myVM \
        b39f27a8b8c64d52b05eac6a62ebad85__Ubuntu-14_04_4-LTS-amd64-server-20160516-en-us-30GB \
        -g ops -p P@ssw0rd! -z "Small" -e -l "West US"
    ```

    Witaj danych wyjściowych jest toohello podobnie poniższy przykład:

    ```azurecli
    info:    Executing command vm create
    + Looking up image b39f27a8b8c64d52b05eac6a62ebad85__Ubuntu-14_04_4-LTS-amd64-server-20160516-en-us-30GB
    + Looking up cloud service
    info:    cloud service myVM not found.
    + Creating cloud service
    + Retrieving storage accounts
    + Creating VM
    info:    vm create command OK
    ```
   
   > [!NOTE]
   > Dla maszyny wirtualnej systemu Linux, należy podać hello `-e` opcji `vm create`. Nie jest możliwe tooenable SSH po utworzeniu maszyny wirtualnej hello. Aby uzyskać więcej szczegółów na SSH, przeczytaj [jak tooUse SSH z systemem Linux na platformie Azure](../articles/virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

5. Atrybuty hello hello maszyny Wirtualnej można sprawdzić za pomocą hello `azure vm show` polecenia. Witaj poniższy przykład zawiera informacje dotyczące hello maszyny Wirtualnej o nazwie `myVM`:

    ```azurecli   
    azure vm show myVM
    ```

6. Uruchom maszyny Wirtualnej z hello `azure vm start` polecenia w następujący sposób:

    ```azurecli
    azure vm start myVM
    ```

## <a name="next-steps"></a>Następne kroki
Aby uzyskać więcej informacji na temat wszystkich tych poleceń maszyny wirtualnej Azure CLI w wersji 1.0, przeczytaj hello [hello Using Azure CLI 1.0 z hello wdrażania klasycznego interfejsu API](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).

