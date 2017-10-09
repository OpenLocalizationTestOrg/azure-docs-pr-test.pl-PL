
<!--
includes/sql-database-include-ip-address-22-v12portal.md

Latest Freshness check:  2016-03-21 , daleche.

As of circa 2015-09-04, hello following topics might include this include:
articles/sql-database/sql-database-configure-firewall-settings.md
articles/sql-database/sql-database-connect-query.md


## Server-level firewall rules

### Add a server-level firewall rule through hello new Azure portal
-->


1. Zaloguj się za toohello [portalu Azure](https://portal.azure.com/) na http://portal.azure.com/.
2. Witaj transparencie po lewej stronie, kliknij przycisk **PRZEGLĄDAJ wszystko**. Witaj **Przeglądaj** bloku jest wyświetlany.
3. Przewiń i kliknij przycisk **serwerów SQL**. Witaj **serwerów SQL** bloku jest wyświetlany.
   
    ![Znajdź serwer bazy danych SQL Azure w portalu hello][b21-FindServerInPortal]
4. Dla wygody, kliknij przycisk hello zminimalizować formantu na powitania wcześniej **Przeglądaj** bloku.
5. W polu tekstowym hello filtru zacznij wpisywać ciąg hello nazwy serwera. Twoje wiersz jest wyświetlany.
6. Kliknij wiersz powitania serwera. Zostanie wyświetlony blok serwera.
7. W bloku serwera, kliknij przycisk **ustawienia**. Witaj **ustawienia** bloku jest wyświetlany.
8. Kliknij przycisk **zapory**. Witaj **ustawienia zapory** bloku jest wyświetlany.
   
    ![Kliknij przycisk Ustawienia > zapory][b31-SettingsFirewallNavig]
9. Kliknij przycisk **Dodawanie klienta IP**. Wpisz nazwę nowej reguły na powitania pierwsze pole tekstowe.
10. Typ w hello niski i wysoki wartości zakresu hello ma adres IP tooenable.
    
    * Może być przydatny toohave hello niskiej wartości kończyć się **.0** i hello wysokiej z **.255**.
    
    ![Dodaj tooallow zakres adresów IP][b41-AddRange]
11. Kliknij pozycję **Zapisz**.

<!-- Image references. -->

[b21-FindServerInPortal]: ./media/sql-database-include-ip-address-22-v12portal/firewall-ip-b21-v12portal-findsvr.png

[b31-SettingsFirewallNavig]: ./media/sql-database-include-ip-address-22-v12portal/firewall-ip-b31-v12portal-settingsfirewall.png

[b41-AddRange]: ./media/sql-database-include-ip-address-22-v12portal/firewall-ip-b41-v12portal-addrange.png



<!--
These includes/ files are a sequenced set, but you can pick and choose:

includes/sql-database-include-ip-address-22-v12portal.md
? includes/sql-database-include-ip-address-*.md
-->
