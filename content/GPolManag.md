Start – Administrative Tools – Group Policy Management – nastavit se na organizační jednotku (Expedice) – PT – Create a GPO… - v okně New GPO zadat jméno politiky (ExPol)

![[Pasted image 20240420180927.png]]

Nastavit se  na politiku – PT – Edit

![[Pasted image 20240420180946.png]]

Nastavení tapety:

![[Pasted image 20240420181017.png]]

Desktop Wallpaper – CLICK – Enabled

![[Pasted image 20240420181034.png]]

Zadá se cesta k obrázku včetně přípony ([\\TEVI-SERVER\ZZZ\administrator\My Documents\My Pictures\zeme.jpg](file:///\\TEVI-SERVER\ZZZ\administrator\My%20Documents\My%20Pictures\zeme.jpg)).

Spuštění programů po přihlášení uživatele:

![[Pasted image 20240420181049.png]]

Začátek je stejný jako při nastavení tapety, pak „Run these programs at user logon“ – Enabled – Show – doplní se seznam programů, které se mají spustit (kalkulačka – calc.exe)

![[Pasted image 20240420181123.png]]

Postupy jsouzcela analogické jako v nastavování lokálních zásad pomocí GPEdit.msc na PC s Windows 7.

V případě klientských počítačů konfigurovaných pomocí objektu zásad skupiny založeného na doméně bude aktualizace zásad skupiny (tedy použití jakýchkoli nových nastavení zásad v klientském počítači) trvat asi 20 minut. Při výchozím nastavení se zásady skupiny aktualizují na pozadí každých 90 minut s náhodným posunem od 0 do 30 minut. Pokud chcete aktualizovat zásady skupiny dříve, můžete v klientském počítači přejít do příkazového řádku a zadat příkaz **gpupdate /force**.