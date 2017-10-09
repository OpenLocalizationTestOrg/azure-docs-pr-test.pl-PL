W tym kroku należy przetestować odbiornika grupy dostępności hello za pomocą aplikacji klienckiej, która działa na powitania tej samej sieci.

Połączenie klienta ma hello następujące wymagania:

* Odbiornik toohello połączeń klienta muszą pochodzić z maszyny, które znajdują się w innej usługi chmury niż hello jeden czy hosty hello zawsze na replik dostępności.
* Jeśli hello zawsze na repliki są w różnych podsieciach, klienci muszą określić *MultisubnetFailover = True* w parametrach połączenia hello. Powoduje to warunek połączenia równoległego podejmuje tooreplicas w hello różnych podsieci. Taki scenariusz obejmuje między region zawsze na dostępność grupy wdrożenia.

Przykładem jest tooconnect toohello odbiornika z jednym hello maszyn wirtualnych w hello tej samej sieci wirtualnej platformy Azure (ale nie jeden, który jest hostem repliki). Toocomplete łatwy sposób ten test jest odbiornika grupy dostępności programu SQL Server Management Studio toohello tootry tooconnect. Inną metodą prostego jest toorun [SQLCMD.exe](https://technet.microsoft.com/library/ms162773.aspx)w następujący sposób:

    sqlcmd -S "<ListenerName>,<EndpointPort>" -d "<DatabaseName>" -Q "select @@servername, db_name()" -l 15

> [!NOTE]
> W przypadku hello wartość EndpointPort *1433*, nie jest wymagane toospecify go w wywołaniu hello. Witaj poprzedniego wywołania założono również, czy powitania klienta maszyna jest toohello przyłączone do tej samej domeny i że wywołującego hello udzielono uprawnień w bazie danych hello przy użyciu uwierzytelniania systemu Windows.
> 
> 

Podczas testowania odbiornika hello być toofail się za pośrednictwem toomake grupy dostępności hello się, że klienci mogą odbiornika toohello w tryb failover.

