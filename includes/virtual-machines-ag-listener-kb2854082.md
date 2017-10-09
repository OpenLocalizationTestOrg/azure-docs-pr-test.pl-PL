Następnie wszystkie serwery w klastrze hello korzystający z systemu Windows Server 2008 R2 lub Windows Server 2012, należy sprawdzić tej poprawki hello [KB2854082](http://support.microsoft.com/kb/2854082) jest instalowane na każdym z serwerów lokalnych hello lub maszynach wirtualnych platformy Azure, które są częścią klastra hello. Dowolnego serwera lub maszyny Wirtualnej w klastrze hello, ale nie w grupie dostępności hello powinien również zawierać po zainstalowaniu tej poprawki.

W hello sesji usług pulpitu zdalnego dla każdego z węzłów klastra hello, Pobierz [KB2854082](http://support.microsoft.com/kb/2854082) tooa katalogu lokalnego. Następnie po kolei Zainstaluj poprawkę hello w każdym węźle klastra. Jeśli usługa klastrowania hello obecnie jest uruchomiona w węźle klastra hello, serwer hello jest ponownie uruchamiany na końcu hello hello instalacji poprawki.

> [!WARNING]
> Zatrzymanie usługi klastrowania hello lub ponowne uruchomienie serwera hello wpływa na powitania kondycji kworum klastra i hello grupy dostępności i może spowodować, że Twoje toogo klastra w tryb offline. toomaintain hello wysoką dostępność klastra podczas instalacji, upewnij się, że:
> 
> * klaster Hello znajduje się w optymalny kworum kondycji. 
> * Przed zainstalowaniem poprawki hello w każdym węźle, wszystkie węzły klastra są w trybie online.
> * Przed zainstalowaniem poprawki hello na jednym z węzłów w klastrze hello Zezwalaj toocompletion toorun instalacji poprawki hello na jednym węźle, w tym pełni ponowne uruchomienie serwera hello.
> 
> 

