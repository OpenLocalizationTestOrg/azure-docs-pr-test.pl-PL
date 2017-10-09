### <a name="create-a-tcp-endpoint-for-hello-virtual-machine"></a>Tworzenie punktu końcowego TCP hello maszyny wirtualnej
W kolejności tooaccess programu SQL Server z hello internet, maszyna wirtualna hello musi mieć toolisten punktu końcowego TCP komunikacji przychodzącej. Ten krok konfiguracji platformy Azure Określa, że przychodzący port TCP, port ruchu tooa TCP jest dostępny toohello maszyny wirtualnej.

> [!NOTE]
> Jeśli łączysz się w obrębie hello takie same w chmurze, usługi lub wirtualnych sieci, nie masz toocreate publicznie dostępnym punkcie końcowym. W takim przypadku można kontynuować toohello następnego kroku. Aby uzyskać więcej informacji, zobacz [scenariuszach połączeń](../articles/virtual-machines/windows/sqlclassic/virtual-machines-windows-classic-sql-connect.md#connection-scenarios).
> 
> 

1. Na powitania portalu Azure, wybierz **maszyn wirtualnych (klasyczne)**.
2. Następnie wybierz maszynę wirtualną programu SQL Server.
3. Wybierz **punkty końcowe**, a następnie kliknij przycisk hello **Dodaj** przycisk u góry bloku punkty końcowe hello hello.
   
    ![Portal kroki tworzenia punktu końcowego](./media/virtual-machines-sql-server-connection-steps/portal-endpoint-creation.png)
4. Na powitania **Dodawanie punktu końcowego** bloku, podaj **nazwa** takich jak SQLEndpoint.
5. Wybierz **TCP** dla hello **protokołu**.
6. Aby uzyskać **port publiczny**, określ numer portu, takich jak **57500**.
7. Aby uzyskać **port prywatny**, określ port nasłuchiwania programu SQL Server, która domyślnie określa zbyt**1433**.
8. Kliknij przycisk **Ok** toocreate hello endpoint.

