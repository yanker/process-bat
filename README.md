# Process-bat
Bat process for my businnes

## activate-network-card
Hace un ping a google.com y en caso de obtener error activa y desactiva la tarjeta de red con un sleep de 10 segundos
```
echo off

echo _________________________________________ >> C:\_pingtest\reporte_ping.txt
echo Fecha : %date% >> C:\_pingtest\reporte_ping.txt
echo Hora : %time%  >> C:\_pingtest\reporte_ping.txt

REM Hacemos 4 pings a google y no mostramos información
ping -n 4 google.com  > nul
REM ping -n 1 google.com  >> C:\_pingtest\reporte_ping.txt

REM Verificar el resultado del ping
if %errorlevel% equ 0 (
	
	REM msg
    echo "Se recibió respuesta al ping." >> C:\_pingtest\reporte_ping.txt    
	
) else (
    echo "No se recibió respuesta al ping." >> C:\_pingtest\reporte_ping.txt
    
	REM Desactivo tarjeta
	netsh interface ser interface "Ethernet" admin-disable
	
	REM Esperar 10 segundos
	timeout /t 10 >nul
	
	REM Activo tarjeta
	netsh interface ser interface "Ethernet" admin-enable
)
exit
```
