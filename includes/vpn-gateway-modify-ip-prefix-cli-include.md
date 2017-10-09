### <a name="noconnection"></a>prefiksy adresów brama IP toomodify sieci lokalnej — Brak połączenia bramy

Jeśli nie masz połączenia bramy i mają tooadd lub usunąć prefiksy adresów IP, użyj hello same polecenie użycie bramy sieci lokalnej hello toocreate, [Tworzenie bramy lokalnej sieci az](https://docs.microsoft.com/cli/azure/network/local-gateway#create). Umożliwia także ten adres IP bramy hello polecenia tooupdate hello urządzenia sieci VPN. toooverwrite hello bieżące ustawienia użyj istniejącej nazwy hello bramy sieci lokalnej. Jeśli używasz innej nazwy, Utwórz nową bramę sieci lokalnej, zamiast zastępowanie hello istniejący.

Zawsze, wprowadzone zmiany, hello całą listę prefiksów musi być określona, nie tylko hello prefiksy, które mają toochange. Określ tylko prefiksy hello, które mają tookeep. W tym przypadku są to prefiksy 10.0.0.0/24 i 20.0.0.0/24

```azurecli
az network local-gateway create --gateway-ip-address 23.99.221.164 --name Site2 --connection-name TestRG1 --local-address-prefixes 10.0.0.0/24 20.0.0.0/24
```

### <a name="withconnection"></a>toomodify sieci lokalnej bramy prefiksów adresów IP - istniejące połączenie z bramą

Połączenie bramy i tooadd lub usunąć prefiksy adresów IP, możesz zaktualizować prefiksy hello przy użyciu [aktualizacji bramy lokalnej sieci az](https://docs.microsoft.com/cli/azure/network/local-gateway#update). Spowoduje to pewien przestój połączenia sieci VPN. Podczas modyfikowania adresu IP hello prefiksy, nie potrzebujesz bramy sieci VPN hello toodelete.

Zawsze, wprowadzone zmiany, hello całą listę prefiksów musi być określona, nie tylko hello prefiksy, które mają toochange. W tym przykładzie już istnieją prefiksy 10.0.0.0/24 i 20.0.0.0/24. Możemy dodać hello prefiksy 30.0.0.0/24 i 40.0.0.0/24 i określ wszystkie 4 prefiksów hello, podczas aktualizacji.

```azurecli
az network local-gateway update --local-address-prefixes 10.0.0.0/24 20.0.0.0/24 30.0.0.0/24 40.0.0.0/24 --name VNet1toSite2 --connection-name TestRG1
```