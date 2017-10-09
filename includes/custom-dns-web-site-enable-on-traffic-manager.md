Po zostaną rozpropagowane hello rekordów dla nazwy domeny, należy być stanie toouse tooverify przeglądarki, z których mogą z niestandardowej nazwy domeny można tooaccess używanych aplikacji sieci web w usłudze Azure App Service.

> [!NOTE]
> Może upłynąć trochę czasu, zanim toopropagate Twojego CNAME za pośrednictwem hello systemu DNS. Można użyć usługi, takie jak <a href="http://www.digwebinterface.com/">http://www.digwebinterface.com/</a> tooverify, który hello CNAME jest dostępna.
> 
> 

Jeśli aplikacja sieci web nie ma jeszcze dodany jako punkt końcowy Menedżera ruchu, należy to zrobić przed rozpoznawanie nazw działa jako hello domeny niestandardowej nazwy tras tooTraffic menedżera. Menedżer ruchu jest następnie przekierowuje tooyour aplikacji sieci web. Użyj informacji hello w [Dodawanie lub usuwanie punktów końcowych](../articles/traffic-manager/traffic-manager-endpoints.md) tooadd aplikacji sieci web jako punktu końcowego w profilu usługi Traffic Manager.

> [!NOTE]
> Jeśli aplikacja sieci web nie jest wyświetlana podczas dodawania punktu końcowego, sprawdź, czy jest ono skonfigurowane dla **standardowe** tryb planu usługi aplikacji. Należy użyć **standardowe** tryb dla aplikacji sieci web w kolejności toowork Menedżera ruchu.
> 
> 

1. W przeglądarce otwórz hello [Azure Portal](https://portal.azure.com).
2. W hello **aplikacje sieci Web** , kliknij pozycję hello nazwę aplikacji sieci web, wybierz opcję **ustawienia**, a następnie wybierz **domen niestandardowych**
   
    ![](./media/custom-dns-web-site/dncmntask-cname-6.png)
3. W hello **domen niestandardowych** bloku, kliknij przycisk **dodać nazwę hosta**.
4. Użyj hello **Hostname** tekst pola tooenter hello Traffic Manager domeny nazwa tooassociate z tej aplikacji sieci web.
   
    ![](./media/custom-dns-web-site/dncmntask-cname-8.png)
5. Kliknij przycisk **weryfikacji** toosave hello domeny nazwy konfiguracji.
6. Po kliknięciu **weryfikacji** Azure będzie rozpocząć wyłączyć weryfikację domeny przepływu pracy. Spowoduje to zaewidencjonowanie własność domeny, a także Hostname Powodzenie dostępności i raportów lub szczegółowe informacje o błędzie z przetestowanego wskazowki w sposób toofix hello błędu.    
7. Po pomyślnym zweryfikowaniem **dodać nazwę hosta** przycisk staną się aktywne i będą mogli toohello Przypisz hostname. Teraz przejdź tooyour niestandardową nazwę domeny w przeglądarce. Powinna zostać wyświetlona Twojej pracy aplikacji przy użyciu niestandardowej nazwy domeny. 
   
   Po zakończeniu konfiguracji hello niestandardowej nazwy domeny będzie wyświetlane w hello **nazwy domen** części aplikacji sieci web.

W tym momencie powinna być nazwa nazwy domeny usługi Traffic Manager hello stanie tooenter w przeglądarce i zobacz, czy pomyślnie zajmuje tooyour aplikacji sieci web.

