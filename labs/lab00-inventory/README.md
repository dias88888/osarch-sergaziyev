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
| Процессор | Apple M2 | `sysctl -n machdep.cpu.brand_string` |
| Ядра / потоки | 8 физических / 8 логических (SMT нет) | `sysctl hw.physicalcpu hw.logicalcpu` |
| Память, объём | 16 ГБ (17 179 869 184 байт) | `sysctl hw.memsize` |
| Память, тип и модули | LPDDR5, Hynix. Одна запись, слотов и �| Память, тип �е�| Память, тип и модули | LPDDR5, Hynix. Одна запись, слотов и �| Память, тип �е�| Память�р| Паь | Команда не показы| Память, тип и мод�e Silicon, поэтому значе| Память,�мерено | `system_profiler SPMemoryDataType` |
| Диск, м�| Д�ль | APPLE SSD AP0256Z, 251 ГБ, GPT | `system_profiler SPNVMeDataType` |
| Диск, тип| Диск, тип| �abric), SMART Verified | `system_profiler SPStorageDataType` |
| Свобо�| Свобо�| Свобо�| Свобо�| Свобо�| Своо из 245,11 Г�| Свобо�| Свобо�| Свобо�| Свобо�| Свобо�| С�taT| Свобо�| Свобо�| Свобо�| Свобо�| Свобо�| Своо из 245,11 Г�| Свобо�| Свобо�| Свобвенную загрузку (iBoot). System Firmware Version 20457.1.29. Дату прошивки macOS не выводит | `system_profiler SPHardwareDataType` |
| Аппаратная виртуализация | Есть и включена: `kern.hv_support: 1` (Hypervisor.framework) | `sysctl kern.hv_support` |

Про виртуализацию: проверка `VMX` (термин Intel) на M2 ничего не вывела, потому что в архитектуре ARM такого флага нет. Поддержку показывает `kern.hv_support`.

Важное для следующих лаб: процессор ARM, поэтому нужны ARM64-образы (Ubuntu Server ARM64, Windows 11 ARM). Для Lab 1 и Lab 2 надо уточнить у преподавателя, подойдёт ли это.

## Что не сработало в первый раз

1. **Команды Git в неправильной папке.** `git status`, `git add`, `git commit`, `git push` я запускал в домашней папке `~` и получил `fatal: not a git repository`. Git работает только внутри папки репозитория. Решение: `cd ~/osarch-sergaziyev` и повторить.
2. **Push не прошёл по паролю.** GitHub ответил `Password authentication is not supported for Git operations`. Пароль аккаунта больше не принимается, нужен Personal Access Token. Решение: создать токен (Settings → Developer settings → Tokens, прав2. **Push не прошёл по паролю.** GitHub ответил `Password authentication is not supported for Git operations`. Пароль аккаунта больше не принимается, нужен Personal Access Token. Решение: соз`git remote set-url origin https://github.com/sergaziyevdias/osarch-sergaziyev.git`.
4. **Объём диска и свободное место.** Сначала легко взять число 245 ГБ, но это ёмкость, а не свободное место. Свободное место на томе: 178,86 ГБ.

## Доказательства

- [evidence/cpu.txt](evidence/cpu.txt) — модель процессора и число ядер и потоков.
- [evidence/memory.txt](evidence/memory.txt) — 16 ГБ LPDDR5, вывод `system_profiler` и `hw.memsize`.
- [evidence/disk.txt](evidence/disk.txt) — модель и тип диска, свободное место на томе.
- [evidence/firmware.txt](evidence/firmware.txt) — версия системной прошивки.
- [evidence/virtualization.txt](evidence/virtualization.txt) — `kern.hv_support: 1`.
- [evidence/os.txt](evidence/os.txt) — версия macOS и архитектура arm64.
