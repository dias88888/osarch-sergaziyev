# Lab 0 — Inventory

Пара: Sergaziyev (работал один, напарник не участвовал)  Первый водитель: Sergaziyev
Машина: MacBook Air (Apple M2), macOS, без виртуальной машины
Дата: 05.11.2026, 17:00

## Что я сделал

Все значения получены только из терминала, окно «Об этом Mac» не открывалось.

```bash
sysctl -n machdep.cpu.brand_string
sysctl hw.physicalcpu hw.logicalcpu
system_profiler SPMemoryDataType
sysctl hw.memsize
system_profiler SPStorageDataType SPNVMeDataType
diskutil info /
df -h /
df -h /System/Volumes/Data
system_profiler SPHardwareDataType | grep -i -E "firmware|model"
sysctl kern.hv_support
sysctl machdep.cpu.features
sw_vers; uname -m
```

## Результат

| Что | Значение | Где я его получил |
|---|---|---|
| Процессор | Apple M2 | `sysctl -n machdep.cpu.b| Прtring` |
| Ядра / потоки | 8 физич| Ядра / потгических (SMT нет) | `sysctl hw.physicalcpu hw.logicalcpu` |
| Память, объём | 16 ГБ (17 179 869 184 байт) | `sysctl hw.memsize` |
| Память, тип и модули | LPDDR5, Hynix. Одна запись, слотов и �| Память, тип �е�| Память, тип и модули | LPDDR5, Hynix. Одна запись, слотов и �| Память, тип �е�| Память�рость | Команда не показы| Память, тип и моду Silicon, поэтому значе| Памятьзм| Память, тип и модули | LPDDR5 |
| Диск, м�| Ди�ь | APPLE SSD AP0256Z, 251 ГБ, GPT | `system_profiler SPNVMeDataType` |
| Диск, тип | SSD, NVMe (Apple Fabric), SMART Verified | `syst| Диск, т�torageDataType` |
| Свобо�| Свобо�| Свобо�| Свобо�| Свобо�| Своб из 245,11 ГБ (том Data, `/System/Volumes/Data`) | `system_profiler SPStorageDataT| Свобо�| Свобо�| Свобо�| Свобо�| Свобо�| Своб из 245,11 ГБ (том Data, `/System/Volumes/Data�енную загрузку (iBoot). System Firmware Version 20457.1.29. Дату прошивки macOS не выводит | `system_profiler SPHardwareDataType` |
| Аппаратная виртуализация | Есть и включена: `kern.hv_support: 1` (Hypervisor.framework) | `sysctl kern.hv_support` |

Про виртуализацию: проверка `VMX` (термин Intel) на M2 ничего не вывела, потому что в архитектуре ARM такого флага нет. Поддержку показывает `kern.hv_support`.

Важное для следующих лаб:Важное для следующих лаб:Важное для следующих лаб:Важ� 11Важное для следующих лаб:Важное для следующих лаб:Важное для следующих лаб:Важ� 11Важное для следующих лаб:Важное для следующих лаб:Важное для следующих лаб:Важ� 11Важное для следующих лаб:Важное для следующих лаб:Важное для следующих лаб:Важ� 11Важное�пВажное для следующих лаб:Важное для следующих лаб:Важное для следующих лаб:Важ� 11Ва `PaВажное для следующих лаб:Важное для следующих лаб:Важное для следующих лаб:Важ� 11Важное для следующих лаб:Важное для следующих лаб:Важное длав
cd ~/osarch-sergaziyev

# Недостающие доказательства
{ sw_vers; uname -m; } | tee labs/lab00-inventory/evidence/os.txt
system_profiler SPHardwareDataType | grep -i -E "model name|model identifier|chip|firmware" | tee labs/lab00-inventory/evidence/firmware.txt
{ sysctl kern.hv_support; sysctl machdep.cpu.features; } 2>&1 | tee labs/lab00-inventory/evidence/virtualization.txt
df -h /System/Volumes/Data | tee -a labs/lab00-inventory/evidence/disk.txt

# README
cat > labs/lab00-inventory/README.md << 'EOF'
# Lab 0 — Inventory

Пара: Sergaziyev (работал один, напарник не участвовал)  Первый водитель: Sergaziyev
Машина: MacBook Air (Apple M2), macOS, без виртуальной машины
Дата: 05.11.2026, 17:00

## Что я сделал

Все значения получены только из терминала, окно «Об этом Mac» не открывалось.

```bash
sysctl -n machdep.cpu.brand_string
sysctl hw.physicalcpu hw.logicalcpu
system_profiler SPMemoryDataType
sysctl hw.memsize
system_profiler SPStorageDataType SPNVMeDataType
diskutil info /diskutil info /diskutil info /diskutil info /diskutil info /diskutil info /diskutil info /diskutil info /diskutil info /diskutil info /dep.cpu.features
sw_vers; uname -m
```

## Результат

| Что | Значение | Где я его получил |
|---|---|---|
| Процессор | Apple M2 | `sysctl -n machdep.cpu.brand_stri| Процессор | Apple M2 | `sysctl -�ческих / 8 логи| Процессор | Apple M2 | `sysctl -n machdep.cpu.brand_stri| Процессор | Apple M2 | `sysctl -�ческих / 8 ло `| Процессор | Apple M2 | `sysctl -n machdep.cpu.brand_stri| Процессо�з| Процессор | Apи сменных модуле�| Процессор | Apple M2 | `sysctl -n machdep.cpu.brand_stri| Процессор | Apple M2 | `sysctl -�ческих / 8 логиорость| Процессор | Apple M2 |ывает частоту на Apple Silicon, поэтому значение не изм| Процессор | Apple M2 | `sysctl -n ma |
| Диск, модель | APPLE SSD AP0256Z, 251 ГБ, GPT | `system_profiler SPNVMeDataType` |
| Диск, тип | SSD, NVMe (Apple Fabric), SMART Verified | `system_profiler SPStorageDataType` |
| Свободно на томе для ВМ | 178,86 ГБ свободно �| Своб�ГБ (том Data, `/System/Volumes/Data`) | `system_profiler SPStorageDataType`, `df -h /System/Volumes/Data` |
| Прошивка | Не BIOS и не UEFI: Apple Silicon использует собственную загрузку (iBoot). System Firmware Version 20457.1.29. Дату прошивки macOS не выводит | `system_profiler SPHardwareDataType` |
| Аппаратная виртуализация | Есть и включена: `kern.hv_support: 1` (Hypervisor.framework) | `sysctl kern.hv_support` |

Про виртуализацию: проверка `VMX` (термин Intel) на M2 ничего не вывела, потому что в архитектуре ARM такого флага нет. Подд�Про виртуализацию: проверка `VMX` (термин Intel) на M2 нич�б: процессор ARM, поэтому нужны ARM64-образы (Ubuntu Server ARM64, Windows 11 ARM). Для Lab 1 и Lab 2 надо уточнить у преподавателя, подойдёт ли это.

## Что не сработало в первый раз

1. **Команды Git в неправильной папке.** `git status`, `git add`, `git commit`, `git push` я запускал в домашней папке `~` и получил `fatal: not a git repository`. Git работает только внутри папки репозитория. Решение: `cd ~/osarch-sergaziyev` и повторить.
2. **Push не прошёл по паролю.** GitHub ответил `Password authentication is not supported for Git operations`. Пароль аккаунта больше не принимается, нужен Personal Access Token. Решение: создать токен (Settings → Developer settings → Tokens, право `repo`) и вставить его вместо пароля.
3. **Смена логина GitHub.** Я переименовал аккаунт, и старый адрес репозитория перестал быть правильным. Решение: `gi3. **Смена логина GitHub.** Я переимias/osarch-sergaziyev.git`.
4. **Объём диска и свободное место.** Сначала легко взять число 245 ГБ, но это ёмкость, а не свободное место. Свободное место на томе: 178,86 ГБ.

## Доказательства

- [evidence/cpu.txt](evidence/cpu.txt) — модель про- [evidence/cpu.txt](evidence/cpu.txt) — модель про- [evidence/cpu.txt](evidence/cpu.txt) — модель про- [evidence/cpu.txt](evidence/cpu.txt) — модель про- [evidence/cpu.txt](evidence/cpu.txt) — модель про- [evidence/cpu.txt](evidence/cpu.txt) — модель про- [evidence/cpu.txt](evidence/cpu.txt) — модель про- [evidence/cpu.txt](evide[evidence/virtualization.txt](evidence/virtualization.txt) — `kern.hv_support: 1`.
- [evidence/os.txt](evidence/os.txt) — версия macOS и архитектура arm64.
