# mif_hyperv_template

Шаблон Zabbix 7.2 для мониторинга Hyper-V хостов через Zabbix Agent 2 (без SCVMM, чистый Get-VM/Get-CimInstance на самом хосте).

## Что собирает
- Память хоста-гипервизора: total / free / used / used %
- По каждой запущенной ВМ (LLD, выключенные не отображаются): state, status, dynamic memory on/off, startup/minimum/maximum/assigned/demand
- Для ВМ со статической памятью прототипы minimum/maximum не создаются (бессмысленны для статики)
- Расчётные элементы: сколько ОЗУ реально доступно под новые ВМ (с учётом резерва на стабильность хоста `{$HV.MEM.RESERVE}`, по умолчанию 4 ГиБ) — обычный и "худший случай" (с учётом потенциального роста ВМ с динамической памятью до их Maximum)

## Требования на хосте
Zabbix Agent 2, PowerShell-скрипты и UserParameter, отдающие JSON:
- `hyperv.mem.host` — память хоста
- `hyperv.vm.data` — массив ВМ со всеми полями памяти

## Импорт
Data collection → Templates → Import → `mif_hyperv_template.yaml`
