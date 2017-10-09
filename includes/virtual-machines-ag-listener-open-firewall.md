W tym kroku zostanie utworzony port sondy hello tooopen reguły zapory dla endpoint z równoważeniem obciążenia hello (określone wcześniej 59999) i drugi port odbiornika grupy dostępności hello tooopen reguły. Ponieważ utworzono punkt końcowy hello równoważeniem obciążenia na powitania maszyn wirtualnych, które zawierają repliki grupy dostępności, wystarczy tooopen hello sondowania port i port odbiornika hello na powitania odpowiednich maszyn wirtualnych.

1. Na maszynach wirtualnych, które obsługują replik, należy uruchomić **Zapora systemu Windows z zabezpieczeniami zaawansowanymi**.

2. Kliknij prawym przyciskiem myszy **reguły ruchu przychodzącego**, a następnie kliknij przycisk **nową regułę**.

3. Na powitania **typ reguły** wybierz pozycję **portu**, a następnie kliknij przycisk **dalej**.

4. Na powitania **protokoły i porty** wybierz pozycję **TCP**, typ **59999** w hello **określone porty lokalne** , a następnie kliknij przycisk **Dalej**.

5. Na powitania **akcji** Zachowaj **przyłączenia hello** zaznaczone, a następnie kliknij przycisk **dalej**.

6. Na powitania **profilu** zaakceptować ustawienia domyślne hello, a następnie kliknij pozycję **dalej**.

7. Na powitania **nazwa** strony w hello **nazwa** tekst Określ nazwę reguły, takie jak **zawsze na sondowania Port odbiornika**, a następnie kliknij przycisk **Zakończ**.

8. Powtórz hello w poprzednich krokach dla hello port odbiornika grupy dostępności (określone we wcześniejszej części parametru hello $EndpointPort hello skryptu), a następnie podaj nazwę odpowiednią regułę, takich jak **zawsze na Port odbiornika**.

