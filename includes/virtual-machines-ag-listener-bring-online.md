1. W Menedżerze klastra trybu Failover rozwiń **ról**, a następnie zaznacz tej grupy dostępności.  

2. Na powitania **zasobów** , kliknij prawym przyciskiem myszy nazwę odbiornika hello, a następnie kliknij **właściwości**.

3. Kliknij przycisk hello **zależności** kartę. Jeśli wiele zasobów nie są wyświetlane, sprawdź, czy adresy IP hello mają lub nie oraz zależności.  

4. Kliknij przycisk **OK**.

5. Kliknij prawym przyciskiem myszy nazwę odbiornika hello, a następnie kliknij przycisk **przejdź do trybu Online**.

6. Odbiornik po hello jest w trybie online na powitania **zasobów** , kliknij prawym przyciskiem myszy hello grupy dostępności, a następnie kliknij **właściwości**.
   
    ![Skonfiguruj hello dostępności grupy zasobów](./media/virtual-machines-sql-server-configure-alwayson-availability-group-listener/IC678772.gif)

7. Zależność od zasobu Nazwa odbiornika hello (nie hello nazwę adresów IP zasobów), a następnie kliknij polecenie **OK**.
   
    ![Dodaj zależności na nazwę odbiornika hello](./media/virtual-machines-sql-server-configure-alwayson-availability-group-listener/IC678773.gif)

8. Uruchom program SQL Server Management Studio, a następnie połącz toohello repliki podstawowej.

9. Przejdź za**wysokiej dostępności funkcji AlwaysOn** > **grup dostępności** > **\<AvailabilityGroupName\>**   >  **Odbiorniki grupy dostępności**.  
    Nazwa odbiornika Hello utworzonego w Menedżerze klastra trybu Failover powinny być wyświetlane.

10. Kliknij prawym przyciskiem myszy nazwę odbiornika hello, a następnie kliknij przycisk **właściwości**.

11. W hello **portu** Określ numer portu odbiornika grupy dostępności hello hello przy użyciu hello $EndpointPort używanego wcześniej (w tym samouczku 1433 była hello domyślna), a następnie kliknij przycisk **OK**.

