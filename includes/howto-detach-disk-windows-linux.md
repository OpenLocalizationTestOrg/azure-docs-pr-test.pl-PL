Jeśli nie ma potrzeby dysku danych, który jest dołączony tooa maszyny wirtualnej, możesz ją łatwo odłączyć. Odłączanie dysku usuwa hello dysk od maszyny wirtualnej hello, ale nie powoduje usunięcia dysku hello z hello kontem magazynu platformy Azure.

Jeśli chcesz ponownie toouse hello istniejące dane na dysku hello, użytkownik może dołączyć go toohello tej samej maszyny wirtualnej lub innej.  

> [!NOTE]
> toodetach dysku systemu operacyjnego, należy najpierw maszyny wirtualnej hello toodelete.
>

## <a name="find-hello-disk"></a>Znajdź hello dysku
Jeśli nie znasz nazwy hello z hello dysku lub mają tooverify zanim ją odłączyć, wykonaj następujące kroki.

1. Zaloguj się toohello [portalu Azure](https://portal.azure.com).

2. Kliknij przycisk **maszyn wirtualnych**, a następnie wybierz hello odpowiedniej maszyny Wirtualnej.

3. Kliknij przycisk **dysków** wzdłuż hello lewej krawędzi hello pulpitu nawigacyjnego maszyny wirtualnej, w obszarze **ustawienia**.

 pulpit nawigacyjny maszyny wirtualnej Hello Wyświetla hello nazwę i typ wszystkich dołączonych dysków. Na przykład na tym ekranie przedstawiono maszynę wirtualną z jednym dyskiem systemu operacyjnego (OS) i jednym dyskiem danych:

    ![Znajdowanie dysku danych](./media/howto-detach-disk-windows-linux/vmwithdisklist.png)

## <a name="detach-hello-disk"></a>Odłączanie dysku hello
1. Witaj portalu Azure kliknij **maszyn wirtualnych**, a następnie kliknij przycisk hello nazwę hello maszynę wirtualną, która ma być toodetach dysk danych hello.

2. Kliknij przycisk **dysków** wzdłuż hello lewej krawędzi hello pulpitu nawigacyjnego maszyny wirtualnej, w obszarze **ustawienia**.

3. Kliknij dysk hello ma toodetach.

  ![Zidentyfikuj hello toodetach dysku](./media/howto-detach-disk-windows-linux/disklist.png)

4. Na pasku poleceń hello, kliknij **Detach**.

  ![Zlokalizuj hello odłączyć polecenia](./media/howto-detach-disk-windows-linux/diskdetachcommand.png)

5. W oknie potwierdzenia powitania kliknij **tak** toodetach hello dysku.

  ![Potwierdź Trwa odłączanie dysku hello](./media/howto-detach-disk-windows-linux/confirmdetach.png)

dysk Hello pozostaje w pamięci masowej, ale nie jest już dołączony tooa maszyny wirtualnej.
